---
title: "aaaProtect un déploiement d’application SAP NetWeaver à plusieurs niveaux à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Cet article décrit comment tooprotect SAP NetWeaver les déploiements d’applications à l’aide d’Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: manayar
ms.openlocfilehash: 34651c7b14d23a44005372f4f923c401e0224231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-a-multi-tier-sap-netweaver-application-deployment-using-azure-site-recovery"></a>Protéger un déploiement d’applications SAP NetWeaver multiniveau à l’aide d’Azure Site Recovery

La plupart des déploiements SAP, de moyenne et grande taille, disposent d’une forme de solution de récupération d’urgence.  importance Hello des solutions de récupération d’urgence fiables et testables a augmenté lors de leur déplacement plus principaux processus commerciaux tooapplications tels que SAP.  Azure Site Recovery a été testées et intégrées aux applications de SAP et dépasse les capacités de hello de la plupart des solutions de récupération d’urgence sur site, à moindre coût total de possession (TCO) que les solutions concurrentes.
Avec Azure Site Recovery, vous pouvez :
* Activez la protection des applications SAP NetWeaver et NetWeaver non-production exécuté localement, en répliquant tooAzure de composants.
* Activez la protection des applications SAP NetWeaver et NetWeaver non-production Azure, en cours d’exécution en répliquant les composants tooanother centre de données Azure.
* Simplifier la migration de cloud, à l’aide de récupération de Site toomigrate votre tooAzure de déploiement de SAP.
* Simplifiez les mises à niveau, les tests et la création de prototypes du projet SAP, par la création d’un clone de production à la demande pour tester les applications SAP.

Cet article décrit comment tooprotect SAP NetWeaver les déploiements d’applications à l’aide de [Azure Site Recovery](site-recovery-overview.md). Cet article traite des meilleures pratiques de hello pour protéger un déploiement de SAP NetWeaver à trois niveaux dans Azure en répliquant tooanother centre de données Azure à l’aide d’Azure Site Recovery, les scénarios hello pris en charge et les configurations, et comment les basculements tooperform, les deux tests basculements (exercices de récupération d’urgence) et les basculements réels.


## <a name="prerequisites"></a>Composants requis
Avant de commencer, assurez-vous que vous comprenez les suivant hello :

1. [Réplication d’un tooAzure de machine virtuelle](azure-to-azure-walkthrough-enable-replication.md)
2. Comment trop[concevoir un réseau de récupération](site-recovery-azure-to-azure-networking-guidance.md)
3. [Effectuer un tooAzure de basculement de test](azure-to-azure-walkthrough-test-failover.md)
4. [Effectuer un basculement tooAzure](site-recovery-failover.md)
5. Comment trop[répliquer un contrôleur de domaine](site-recovery-active-directory.md)
6. Comment trop[répliquer de SQL Server](site-recovery-sql.md)

## <a name="supported-scenarios"></a>Scénarios pris en charge
Avec Azure Site Recovery, vous pouvez implémenter une solution de récupération d’urgence pour hello les scénarios suivants :
* Systèmes SAP s’exécutant dans un centre de données Azure réplication tooanother centre de données Azure (Azure vers Azure DR), comme la mise en œuvre [ici](https://aka.ms/asr-a2a-architecture).
* Systèmes SAP s’exécutant sur des serveurs VMWare (ou physique) réplication tooa DR site local dans un centre de données Azure (VMware pour Azure DR), ce qui nécessite des composants supplémentaires comme la mise en œuvre [ici](https://aka.ms/asr-v2a-architecture).
* Systèmes SAP s’exécutant sur Hyper-V local Réplication site tooa récupération d’urgence dans un centre de données Azure (Hyper-V vers Azure DR), ce qui nécessite des composants supplémentaires comme la mise en œuvre [ici](https://aka.ms/asr-h2a-architecture).

Ce document utilise les fonctionnalités de récupération d’urgence hello premier cas Azure vers Azure récupération d’urgence - toodemonstrate Azure Site Recovery SAP. Comme la réplication d’Azure Site Recovery est indépendant de l’application, hello est décrite est toohold attendu pour d’autres scénarios ainsi.

### <a name="required-foundation-services"></a>Services de base nécessaires
Ce scénario de documentation tous été déployée avec hello suivant services foundation déployés :
* ExpressRoute ou réseau privé virtuel (VPN) site à site
* Au moins un contrôleur de domaine Active Directory et un serveur DNS s’exécutant dans Azure

Il est recommandé que l’infrastructure hello ci-dessus est toodeploying préalable établie Azure Site Recovery.


## <a name="typical-sap-application-deployment"></a>Déploiement classique des applications SAP
Les clients SAP volumineux déploient généralement entre les applications SAP individuelles too20 6.  La plupart de ces applications est basée sur les moteurs de SAP NetWeaver ABAP ou Java hello.  La prise en charge de ces applications NetWeaver vitales est assurée par de nombreux autres moteurs autonomes SAP plus petits, non-NetWeaver et spécifiques, et en général par quelques applications non-SAP.  

Il est critique tooinventory toutes les applications hello SAP s’exécutant dans un paysage et toodetermine hello mode de déploiement (niveau 2 ou 3 niveaux), des versions, des correctifs, tailles, évolution du taux et les exigences de persistance de disque.

![Modèle de déploiement](./media/site-recovery-sap/sap-typical-deployment.png)

couche de persistance Hello SAP de base de données doit être protégé via hello natif SGBD outils tels que SQL Server AlwaysOn, Oracle DataGuard ou HANA système de réplication. couche Hello du client n’est pas également protégé par Azure Site Recovery, mais il est important tooconsider rubriques ayant un impact sur cette couche, tels que le délai de Propagation DNS, sécurité et l’accès à distance toohello centre de données de récupération d’urgence.

Azure Site Recovery est hello solution pour la couche d’application hello, y compris (A) SCS recommandée. Autres applications telles que les applications non SAP NetWeaver et SAP non font partie de hello globale SAP environnement de déploiement et doit également être protégé par Azure Site Recovery.

## <a name="replicate-virtual-machines"></a>Répliquer des machines virtuelles
Suivez [ce guide](azure-to-azure-walkthrough-enable-replication.md) toostart répliquer tous hello toohello de machines virtuelles SAP application Centre de données de récupération d’urgence Azure.

Si vous utilisez une adresse IP statique, vous pouvez spécifier IP hello souhaité hello tootake d’ordinateur virtuel dans la section de cartes réseau interface hello dans les paramètres de calcul et réseau.

![IP cible](./media/site-recovery-sap/sap-static-ip.png)


## <a name="creating-a-recovery-plan"></a>Création d’un plan de récupération
Un plan de récupération permet de séquençage hello de basculement de différents niveaux dans une application multicouche, par conséquent, de maintenir la cohérence des applications. Suivez les étapes de hello décrites [ici](site-recovery-create-recovery-plans.md) lors de la création d’un plan de récupération pour une application web multicouche.

### <a name="adding-scripts-toohello-recovery-plan"></a>Ajout de scripts de plan de récupération toohello
Vous devrez peut-être toodo certaines opérations sur hello basculement de test de basculement/post machines virtuelles pour votre toofunction applications correctement. Vous pouvez automatiser l’opération de basculement hello post telles que l’entrée DNS de mise à jour et la modification des liaisons et les connexions, en ajoutant des scripts correspondant dans le plan de récupération hello comme décrit dans [cet article](site-recovery-create-recovery-plans.md#add-scripts).

### <a name="dns-update"></a>Mise à jour DNS
Si hello DNS est configuré pour une mise à jour DNS dynamique, alors que les machines virtuelles généralement mettre à jour hello DNS avec la nouvelle adresse IP de hello une fois qu’ils démarrent. Tooadd un tooupdate étape explicite DNS avec hello nouvelles adresses IP d’ordinateurs virtuels hello puis ajouter ce [tooupdate adresse IP dans DNS de script](https://aka.ms/asr-dns-update) comme une action sur les groupes de plan de récupération.  

## <a name="example-azure-to-azure-deployment"></a>Exemple de déploiement Azure vers Azure
Dans le diagramme hello ci-dessous un scénario de récupération d’urgence de Microsoft Azure Site Recovery Azure vers Azure hello montre :
* Bonjour centre de données principal est à Singapour (Asie du Sud-est Azure) et Bonjour centre de données de récupération d’urgence est Hong Kong (Asie orientale Azure).  Dans ce scénario, une haute disponibilité locale est fournie par la présence de deux machines virtuelles exécutant SQL Server AlwaysOn en mode synchrone à Singapour.
* Hello ASC de partage de fichier peut être utilisé tooprovide à haute disponibilité pour les points de défaillance uniques de SAP hello. L’ASCS de partage de fichiers ne nécessite pas de disque partagé en cluster, et les applications telles que SIOS ne sont pas utiles.
* Protection de récupération d’urgence pour la couche de SGBD hello est obtenue à l’aide de la réplication asynchrone.
* Ce scénario montre « récupération d’urgence symétrique » – un terme utilisé toodescribe une solution de récupération d’urgence qui est un réplica exact de la production, par conséquent hello solution de récupération d’urgence SQL Server possède une haute disponibilité locale. utilisation de Hello de récupération d’urgence symétrique n’est pas obligatoire pour la couche de base de données hello et de nombreux clients tirer parti des flexibilité hello de déploiements de cloud toobuild un nœud local à haute disponibilité rapidement après un événement de récupération d’urgence.
* diagramme de Hello représente hello SAP NetWeaver ASC et la couche d’Application serveur répliqué par Azure Site Recovery.

![Scénario de réplication](./media/site-recovery-sap/sap-replication-scenario.png)

## <a name="doing-a-test-failover"></a>Exécution d’un test de basculement
Suivez [ce guide](azure-to-azure-walkthrough-test-failover.md) toodo un test de basculement.

1.  TooAzure portail, sélectionnez votre coffre Recovery Services.
2.  Cliquez sur le plan de récupération hello créé pour les applications SAP (s).
3.  Cliquez sur Test de basculement.
4.  Sélectionnez le point de récupération et le processus de basculement de test de réseau virtuel Azure toostart hello.
5.  Une fois les environnement secondaire hello, vous pouvez effectuer vos validations.
6.  Une fois les validations hello sont terminées, cliquez sur « Nettoyage du test de basculement » et le basculement de hello tooclean environnement.

## <a name="doing-a-failover"></a>Exécution d’un basculement
Suivez [ce guide](site-recovery-failover.md) lorsque vous effectuez un basculement.

1.  TooAzure portail, sélectionnez votre coffre Recovery Services.
2.  Cliquez sur le plan de récupération hello créé pour les applications SAP.
3.  Cliquez sur « Basculement ».
4.  Sélectionnez le processus de basculement de hello toostart de point de récupération.

## <a name="next-steps"></a>Étapes suivantes
Découvrez en détail la création d’une solution de récupération d’urgence pour les déploiements SAP NetWeaver à l’aide d’Azure Site Recovery dans [ce livre blanc](http://aka.ms/asr-sap). livre blanc de Hello également présente les recommandations de différentes architectures SAP, répertorie les applications prises en charge et les types de machine virtuelle pour SAP sur Azure et décrit les plans de tests possibles pour votre solution de récupération d’urgence.

Découvrez en détail la [réplication d’autres charges de travail](site-recovery-workload.md) à l’aide de Site Recovery.
