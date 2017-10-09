---
title: "aaaReplicate un déploiement à plusieurs niveaux Citrix XenDesktop et XenApp à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Cet article décrit comment tooprotect et récupérez de Citrix XenDesktop et XenApp les déploiements à l’aide d’Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: ponatara
ms.openlocfilehash: c4ea9f95f91c585cdcf9d776b02c0967f4c16ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a>Répliquer un déploiement Citrix XenApp et XenDesktop multiniveau à l’aide d’Azure Site Recovery

## <a name="overview"></a>Vue d'ensemble

Citrix XenDesktop est une solution de virtualisation de bureau qui fournit des ordinateurs de bureau et des applications sous la forme d’un utilisateur de tooany à la demande de service, n’importe où. Avec une technologie de remise FlexCast XenDesktop peut rapidement et en toute sécurité fournir des applications et bureaux toousers.
Aujourd’hui, Citrix XenApp ne fournit aucune fonctionnalité de récupération d’urgence.

Une solution de récupération d’urgence, devraient permettre la modélisation des plans de récupération autour hello au-dessus des architectures d’applications complexes et également avoir hello capacité tooadd personnalisé étapes toohandle mappages d’application entre les différents niveaux assurant ainsi une par simple clic que capture la solution dans l’événement hello d’un sinistre début tooa diminuer RTO.

Ce document fournit des instructions pas à pas pour la création d’une solution de récupération d’urgence pour vos déploiements locaux de Citrix XenApp sur les plateformes Hyper-V et VMware vSphere. Ce document décrit également comment tooperform un test de basculement (extraction de récupération d’urgence) et tooAzure basculement non planifié à l’aide de plans de récupération, les configurations de hello pris en charge et les composants requis.


## <a name="prerequisites"></a>Composants requis

Avant de commencer, assurez-vous que vous comprenez les suivant hello :

1. [Réplication d’un tooAzure de machine virtuelle](site-recovery-vmware-to-azure.md)
1. Comment trop[concevoir un réseau de récupération](site-recovery-network-design.md)
1. [Effectuer un tooAzure de basculement de test](site-recovery-test-failover-to-azure.md)
1. [Effectuer un basculement tooAzure](site-recovery-failover.md)
1. Comment trop[répliquer un contrôleur de domaine](site-recovery-active-directory.md)
1. Comment trop[répliquer de SQL Server](site-recovery-sql.md)

## <a name="deployment-patterns"></a>Modèles de déploiement

Une batterie de serveurs Citrix XenApp et XenDesktop a généralement hello suivant le modèle de déploiement :

**Modèle de déploiement**

Déploiement Citrix XenApp et XenDesktop avec serveur DNS Active Directory, serveur de base de données SQL, Citrix Delivery Controller, serveur StoreFront, XenApp Master (VDA) et serveur de licences Citrix XenApp

![Modèle de déploiement 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a>Prise en charge de Site Recovery

Pour les besoins de hello de cet article, Citrix des déploiements sur des machines virtuelles VMware gérées par vSphere 6.0 / System Center VMM 2012 R2 ont été utilisé toosetup de récupération d’urgence.

### <a name="source-and-target"></a>Source et cible

**Scénario** | **site secondaire de tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Non compris | Oui
**VMware** | Non compris | Oui
**Serveur physique** | Non compris | Oui

### <a name="versions"></a>Versions
Les clients peuvent déployer des composants XenApp en tant que machines virtuelles s’exécutant sur Hyper-V ou VMware ou en tant que serveurs physiques. Azure Site Recovery peut protéger les deux tooAzure déploiements physiques et virtuels.
Étant donné que XenApp 7.7 ou version ultérieure est pris en charge dans Azure, seuls les déploiements avec ces versions peuvent être basculés tooAzure pour la migration ou de récupération d’urgence.

### <a name="things-tookeep-in-mind"></a>Tookeep choses à l’esprit

1. Protection et la récupération de site sur les déploiements à l’aide du système d’exploitation serveur machines toodeliver XenApp applications publiées et XenApp publié des postes de travail est pris en charge.

2. Protection et récupération des déploiements sur site à l’aide du bureau du système d’exploitation de machines toodeliver Desktop VDI pour les bureaux virtuels du client, y compris Windows 10, n’est pas pris en charge. Il s’agit, car la récupération automatique du système ne prend pas en charge la récupération hello d’ordinateurs avec le bureau OS'es.  De plus, certaines versions de postes de travail virtuels clients (par exemple Windows 7) ne sont pas encore prises en charge pour la gestion des licences dans Azure. [Apprenez-en plus](https://azure.microsoft.com/pricing/licensing-faq/) sur les licences pour les bureaux client/serveur dans Azure.

3.  Azure Site Recovery ne peut pas répliquer et protéger les clones MCS ou PVS locaux existants.
Vous devez toorecreate ces clones Azure RM configuration à partir du contrôleur de remise.

4. NetScaler ne peut pas être protégé à l’aide d’Azure Site Recovery, car NetScaler repose sur FreeBSD et Azure Site Recovery ne prend pas en charge la protection du système d’exploitation FreeBSD. Vous devez toodeploy et configurer un nouveau dispositif NetScaler de marché d’Azure après basculement tooAzure.


## <a name="replicating-virtual-machines"></a>Réplication des machines virtuelles

Hello suivant des composants de hello Citrix XenApp déploiement devez toobe protégé tooenable réplication et la récupération.

* Protection du serveur DNS Active Directory
* Protection du serveur de base de données SQL
* Protection de Citrix Delivery Controller
* Protection du serveur StoreFront
* Protection de XenApp Master (VDA)
* Protection du serveur de licences Citrix XenApp


**Réplication du serveur DNS Active Directory**

Reportez-vous trop[protéger Active Directory et DNS avec Azure Site Recovery](site-recovery-active-directory.md) sur des conseils pour la réplication et la configuration d’un contrôleur de domaine dans Azure.

**Réplication du serveur de base de données SQL**

Reportez-vous trop[protéger SQL Server avec la récupération d’urgence de SQL Server et Azure Site Recovery](site-recovery-sql.md) pour des conseils techniques détaillés sur hello recommandé d’options de protection de serveurs SQL Server.

Suivez [ce guide](site-recovery-vmware-to-azure.md) toostart réplication hello autres tooAzure de machines virtuelles de composant.

![Protection des composants XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

**Paramètres Calcul et réseau**

Une fois les ordinateurs hello sont protégés (état est affiché comme « Protégées » sous les éléments répliqués), hello calcul et les paramètres de réseau doivent toobe configuré.
Dans le calcul et réseau > calcul des propriétés, vous pouvez spécifier la taille de nom et la cible de la machine virtuelle Azure hello.
Modifiez toocomply de nom hello aux exigences d’Azure si vous avez besoin. Vous pouvez également afficher et ajouter des informations sur le réseau cible de hello, du sous-réseau et adresse IP qui sera assigné toohello machine virtuelle Azure.

Notez hello suivantes :

* Vous pouvez définir l’adresse IP de hello cible. Si vous ne fournissez une adresse, hello a échoué sur l’ordinateur utilise DHCP. Si vous définissez une adresse qui n’est pas disponible lors du basculement, hello basculement ne fonctionne pas. Hello même adresse IP peut servir pour le test de basculement si l’adresse de hello est disponible dans le réseau de basculement de test hello.

* Pour le serveur DNS/Active Directory de hello, en conservant hello local adresse vous permet de que spécifier hello même adresse en tant que serveur DNS de hello pour le réseau virtuel Azure de hello.

nombre de Hello de cartes réseau est dicté par taille hello que vous spécifiez pour la machine virtuelle de cible hello, comme suit :

*   Si le nombre de hello de cartes réseau sur l’ordinateur source de hello est inférieur ou égal toohello le nombre de cartes autorisé pour la taille de la machine cible hello, puis cible de hello aura hello même nombre de cartes en tant que source de hello.
*   Si nombre hello de cartes pour l’ordinateur virtuel de hello source dépasse nombre hello autorisé pour la taille cible hello puis la taille maximale de la cible hello est utilisé.
* Par exemple, si un ordinateur source possède deux cartes réseau et la taille de la machine cible hello prend en charge quatre, l’ordinateur cible hello aura deux cartes. Si hello source ordinateur possède deux cartes, mais hello taille cible pris en charge uniquement en charge l’un de l’ordinateur cible hello aura qu’un seul adaptateur.
*   Si l’ordinateur virtuel de hello possède plusieurs cartes réseau qu’ils seront connectent tous toohello même réseau.
*   Si l’ordinateur virtuel de hello possède plusieurs cartes réseau, puis hello premier celui illustré dans la liste de hello devient carte de réseau par défaut hello Bonjour machine virtuelle Azure.


## <a name="creating-a-recovery-plan"></a>Création d’un plan de récupération

Une fois la réplication est activée pour hello XenApp, composant machines virtuelles, étape suivante de hello est toocreate un plan de récupération.
Un plan de récupération regroupe les machines virtuelles ayant les mêmes exigences de basculement et de récupération.  

**Étapes toocreate un plan de récupération**

1. Ajoutez hello XenApp composant virtuels Bonjour un Plan de récupération.
2. Cliquez sur Plans de récupération -> + Plan de récupération. Fournit un nom intuitif hello plan de récupération.
3. Pour les machines virtuelles VMware : sélectionnez Serveur de processus VMware comme source, Microsoft Azure comme cible et Resource Manager comme modèle de déploiement, puis cliquez sur Sélectionner les éléments.
4. Pour les ordinateurs virtuels Hyper-V : sélectionnez source en tant que serveur VMM, cible en tant que Microsoft Azure et le modèle de déploiement en tant que le Gestionnaire de ressources et cliquez sur Sélectionner des éléments, puis déploiement de XenApp hello machines virtuelles.

### <a name="adding-virtual-machines-toofailover-groups"></a>Ajout de groupes de machines virtuelles toofailover

Plans de récupération peuvent être personnalisé tooadd des groupes de basculement pour les actions de commande, des scripts ou manuel de démarrage spécifique. Hello, les groupes suivants doivent plan de récupération toobe toohello ajouté.

1. Groupe de basculement 1 : DNS Active Directory
2. Groupe de basculement 2 : Machines virtuelles SQL Server
2. Groupe de basculement 3 : Machine virtuelle d’image maîtresse VDA
3. Groupe de basculement 4 : Delivery Controller et machines virtuelles de serveur StoreFront


### <a name="adding-scripts-toohello-recovery-plan"></a>Ajout de scripts de plan de récupération toohello

Vous pouvez exécuter des scripts avant ou après un groupe spécifique dans un plan de récupération. Vous pouvez aussi inclure et effectuer des actions manuelles pendant le basculement.

plan de récupération personnalisée Hello ressemble à hello ci-dessous :

1. Groupe de basculement 1 : DNS Active Directory
2. Groupe de basculement 2 : Machines virtuelles SQL Server
3. Groupe de basculement 3 : Machine virtuelle d’image maîtresse VDA

   >[!NOTE]     
   >Les étapes 4, 6 et 7 contenant des actions manuelles ou un script sont applicable tooonly un XenApp local > environnement avec des catalogues MCS/PVS.

4. Action manuelle ou un script de groupe 3 : hello de VDA VM master arrêt Master VDA VM lorsque basculé tooAzure sera en cours d’exécution. toocreate nouveaux MCS catalogues à l’aide de l’hébergement de Azure ARM, le maître de hello VDA VM est requis toobe arrêté (de allouée) état. Hello arrêt machine virtuelle à partir du portail Azure.

5. Groupe de basculement 4 : Delivery Controller et machines virtuelles de serveur StoreFront
6. Action manuelle ou de script 1 de Groupe 3 :

    ***Ajouter une connexion hôte Azure ARM***

    Créer la connexion d’hôte Azure ARM dans tooprovision d’ordinateur de contrôleur de remise nouveaux catalogues MCS dans Azure. Suivez les étapes de hello comme expliqué dans cet [article](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).

7. Action manuelle ou de script 2 de Groupe 3 :

    ***Recréer les catalogues MCS dans Azure***

    Hello existant MCS ou PVS clones sur le site principal de hello ne seront pas répliquée tooAzure. Vous devez toorecreate ces clones à l’aide de hello répliquées VDA maître et ARM Azure de configuration à partir du contrôleur de remise. Suivez les étapes de hello comme expliqué dans cet [article](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS catalogues dans Azure.

![Plan de récupération pour les composants XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   >Vous pouvez utiliser des scripts à [emplacement](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) tooupdate hello DNS avec hello basculé de nouvelles adresses IP de hello > ordinateurs virtuels ou tooattach un équilibrage de charge sur hello a échoué sur l’ordinateur virtuel, si nécessaire.


## <a name="doing-a-test-failover"></a>Exécution d’un test de basculement

Suivez [ce guide](site-recovery-test-failover-to-azure.md) toodo un test de basculement.

![Plan de récupération](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a>Exécution d’un basculement

Suivez [ce guide](site-recovery-failover.md) lorsque vous effectuez un basculement.

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur la réplication des déploiements Citrix XenApp et XenDesktop, consultez [ce livre blanc](https://aka.ms/citrix-xenapp-xendesktop-with-asr). Examinez les conseils hello trop[répliquer des autres applications](site-recovery-workload.md) à l’aide de la récupération de Site.
