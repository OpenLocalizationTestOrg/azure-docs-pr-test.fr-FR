---
title: "aaaReplicate un déploiement de Dynamics AX à plusieurs niveaux à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Cet article décrit comment tooreplicate et protéger Dynamics AX à l’aide d’Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/24/2017
ms.author: asgang
ms.openlocfilehash: b974315ec50ab2ec43846b3d3f95c7de88b72fc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a>Répliquer une application Dynamics AX multiniveau à l’aide d’Azure Site Recovery

## <a name="overview"></a>Vue d'ensemble


Microsoft Dynamics AX est une des solution ERP les plus populaires de hello parmi les processus de toostandardized entreprises dans différents emplacements, gérer les ressources et simplifier la conformité. Rassembler application hello est entreprise ou organisation tooan critiques il est très important toobe que que si un sinistre, application doit être en cours d’exécution dans le temps minimal.

Aujourd'hui, Microsoft Dynamics AX ne fournit aucune capacité de récupération d’urgence prête à l’emploi. Microsoft Dynamics AX comprend de nombreux composants de serveur comme base de données objet serveur d’applications, Active Directory (AD), SQL Server, SharePoint Server, etc. de serveur Reporting toomanage hello la récupération d’urgence de chacun de ces composants manuellement est non seulement coûteux, mais également sujette à erreurs.

Cet article explique en détail comment créer une solution de récupération d’urgence pour votre application Dynamics AX à l’aide d’[Azure Site Recovery](site-recovery-overview.md). Sont également couverts les basculements planifiés/non planifiés/de test à l’aide d’un plan de récupération en un seul clic, les configurations prises en charge et les prérequis.
La solution de récupération d’urgence basée sur Azure Site Recovery est entièrement testée, certifiée et recommandée par Microsoft Dynamics AX.



## <a name="prerequisites"></a>Composants requis

Implémentation de la récupération d’urgence pour l’application Dynamics AX à l’aide d’Azure Site Recovery nécessite hello suivant des conditions préalables terminées.

•    Un déploiement local de Dynamics AX a été configuré

•    Un coffre Azure Site Recovery Services a été créé dans un abonnement Microsoft Azure

• Si Azure est le site de récupération, exécutez hello Azure Virtual Machine Readiness Assessment outil sur des machines virtuelles tooensure qu’ils sont compatibles avec les machines virtuelles Azure et Azure Site Recovery Services


## <a name="site-recovery-support"></a>Prise en charge de Site Recovery

Pour les besoins de hello de création de cet article, les machines virtuelles VMware 2012R3 Dynamics AX sur Windows Server 2012 R2, Enterprise ont été utilisés. Réplication de récupération de site est agnostique en termes d’application, les recommandations hello fournies ici sont toohold attendu sur également les scénarios suivants.

### <a name="source-and-target"></a>Source et cible

**Scénario** | **site secondaire de tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Oui | Oui
**VMware** | Oui | Oui
**Serveur physique** | Oui | Oui

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a>Activer la récupération d’urgence de l’application Dynamics AX à l’aide d’Azure Site Recovery
### <a name="protect-your-dynamics-ax-application"></a>Protéger votre application Dynamics AX
Chaque composant de hello Dynamics AX besoins toobe protégé tooenable hello application complète réplication et la récupération. Cette section couvre les points suivants :

**1. Protection d’Active Directory**

**2. Protection du niveau SQL**

**3. Protection des niveaux application et web**

**4. Configuration de la mise en réseau**

**5. Plan de récupération**

### <a name="1-setup-ad-and-dns-replication"></a>1. Configurer la réplication Active Directory et DNS

Active Directory est requis sur le site de récupération d’urgence hello pour Dynamics AX application toofunction. Il existe deux choix recommandés en fonction de la complexité de hello de l’environnement local du client de l’hello.

**Option 1 :**

Si hello client dispose d’un petit nombre d’applications et un seul contrôleur de domaine pour l’ensemble de son site local et sera en cas d’échec sur l’intégralité du site hello ensemble, il est recommandé à l’aide de réplication ASR tooreplicate hello DC machine toosecondary site ( applicable pour le Site tooSite et tooAzure de Site).

**Option 2 :**

Si hello client comporte un grand nombre d’applications et une forêt Active Directory est en cours d’exécution et bascule peu d’applications à la fois, nous vous recommandons de configurer le contrôleur de domaine supplémentaire sur le site de récupération d’urgence de hello (site secondaire ou dans Azure).

Reportez-vous trop[guide d’accompagnement sur la création d’un contrôleur de domaine disponible sur le site de récupération d’urgence](site-recovery-active-directory.md). Pour le reste de ce document, nous supposons qu'un contrôleur de domaine est disponible sur le site de récupération d’urgence.

### <a name="2-setup-sql-server-replication"></a>2. Configurer la réplication SQL Server
Pour des conseils techniques détaillés sur hello recommandé de l’option de protection, consultez guide de toocompanion [niveau SQL](site-recovery-sql.md).

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a>3. Activer la protection des machines virtuelles AOS et du client Dynamics AX
Effectuer une configuration Azure Site Recovery applique selon que les ordinateurs virtuels de hello sont déployés sur [Hyper-V](site-recovery-hyper-v-site-to-azure.md) ou sur [VMware](site-recovery-vmware-to-azure.md).

> [!TIP]
> Tooconfigure de fréquence de cohérence incident recommandée est de 15 minutes.
>

Hello ci-dessous instantané montre état de protection de hello des machines virtuelles de composant Dynamics dans le scénario de protection « TooAzure de site VMware ».
![Éléments protégés ](./media/site-recovery-dynamics-ax/protecteditems.png)

### <a name="4-configure-networking"></a>4. Configurer la mise en réseau
Configurer les paramètres Calcul et réseau des machines virtuelles

Pour le client AX hello et les machines virtuelles de AOS configurer les paramètres réseau dans Azure Site Recovery afin que les réseaux d’ordinateurs virtuels hello toohello attaché droite DR réseau après le basculement. Vérifiez le réseau de récupération d’urgence hello pour ces niveaux est le niveau SQL toohello routable.

Vous pouvez sélectionner hello VM Bonjour répliquées de paramètres de réseau éléments tooconfigure hello comme indiqué dans l’instantané hello ci-dessous.

* Pour les serveurs AOS sélectionnez hello à haute disponibilité correct.

* Si vous utilisez une adresse IP statique, puis spécifiez IP hello souhaité hello tootake de machine virtuelle Bonjour **adresse IP cible** champ ![paramètres réseau](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)



### <a name="5-creating-a-recovery-plan"></a>5. Création d’un plan de récupération

Vous pouvez créer un plan de récupération dans le processus de basculement d’Azure Site Recovery tooautomate hello. Ajouter des couches d’application et web Bonjour un Plan de récupération. Ordre dans différents groupes afin que hello frontal arrêt avant la couche application.

1)  Sélectionnez le coffre Azure Site Recovery hello dans votre abonnement, puis cliquez sur la vignette de Plans de la récupération.

2)  Cliquez sur « + Plan de récupération » et spécifiez un nom.

3)  Sélectionnez hello 'Source' et 'Target'. cible de Hello peut être le site Azure ou secondaire. Si vous choisissez d’Azure, vous devez spécifier le modèle de déploiement hello

![Créer un plan de récupération](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  Sélectionnez hello AOS et un plan de récupération client machines virtuelles toohello et cliquez sur ✓.
![Créer un plan de récupération](./media/site-recovery-dynamics-ax/selectvms.png)


![Plan de récupération](./media/site-recovery-dynamics-ax/recoveryplan.png)

Vous pouvez personnaliser le plan de récupération hello pour l’application Dynamics AX en ajoutant plusieurs étapes comme indiqué ci-dessous. Hello ci-dessus instantané montre hello plan de récupération complète après avoir ajouté toutes les étapes de hello.

*Étapes :*

*1. Étapes du basculement SQL Server*

Consultez trop['Solution de récupération d’urgence de SQL Server'](site-recovery-sql.md) guide d’accompagnement pour plus d’informations sur le serveur de récupération étapes tooSQL spécifique.

*2. Basculement groupe 1 : Basculer les machines virtuelles de hello AOS*

Assurez-vous que le point de récupération de hello sélectionné est aussi proche que possible toohello de base de données PIT mais pas de manière anticipée.

*3. Script : Équilibrage de charge ajouter (uniquement E-A)* ajouter un script (via Azure automation) après le groupe de AOS VM apparaît tooadd un tooit d’équilibrage de charge. Vous pouvez utiliser un script toodo cette tâche. Consultez l’article [comment tooadd équilibrage de charge pour l’application à plusieurs niveaux récupération d’urgence](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)

*4. Basculement groupe 2 : Basculer hello AX client machines virtuelles.*
Basculer le niveau hello web machines virtuelles dans le cadre du plan de récupération hello.


### <a name="doing-a-test-failover"></a>Exécution d’un test de basculement

Consultez too'AD Solution de récupération d’urgence » et « Solution de récupération d’urgence de SQL Server » guides d’accompagnement pour tooAD spécifiques des considérations et SQL server respectivement durant le Test de basculement.

1.  TooAzure portail, sélectionnez votre archivage Site Recovery.
2.  Cliquez sur le plan de récupération hello créé pour Dynamics AX.
3.  Cliquez sur « Test de basculement ».
4.  Sélectionnez le processus de basculement de test hello réseau virtuel toostart hello.
5.  Une fois les environnement secondaire hello, vous pouvez effectuer vos validations.
6.  Une fois les validations hello sont terminées, vous pouvez sélectionner 'Validations Terminer' et environnement de test de basculement hello est supprimé.

Suivez [ce guide](site-recovery-test-failover-to-azure.md) toodo un test de basculement.

### <a name="doing-a-failover"></a>Exécution d’un basculement

1.  TooAzure portail, sélectionnez votre archivage Site Recovery.
2.  Cliquez sur le plan de récupération hello créé pour Dynamics AX.
3.  Cliquez sur « Basculement » et sélectionnez « Basculement ».
4.  Sélectionnez le réseau cible de hello et cliquez sur le processus de basculement ✓ toostart hello.

Suivez [ce guide](site-recovery-failover.md) lorsque vous effectuez un basculement.

### <a name="perform-a-failback"></a>Effectuer une restauration automatique

Consultez too'SQL Solution de récupération d’urgence du serveur « guide d’accompagnement pour le serveur de tooSQL spécifique de considérations lors de la restauration automatique.

1.  TooAzure portail, sélectionnez votre archivage Site Recovery.
2.  Cliquez sur le plan de récupération hello créé pour Dynamics AX.
3.  Cliquez sur « Basculement » et sélectionnez le basculement.
4.  Cliquez sur « Changer de direction ».
5.  Sélectionner les options appropriées hello - synchronisation des données et les options de création de machines virtuelles
6.  Cliquez sur le processus de 'restauration automatique' ✓ toostart hello.


Suivez [ce guide](site-recovery-failback-azure-to-vmware.md) lorsque vous effectuez une restauration automatique.

##<a name="summary"></a>Résumé
À l’aide d’Azure Site Recovery, vous pouvez créer un plan de récupération d’urgence automatisée complet pour votre application Dynamics AX. Vous pouvez opérer le basculement de hello en quelques secondes à partir de n’importe où dans hello des événements d’une interruption de service et obtenir l’application hello opérationnel en quelques minutes.

## <a name="next-steps"></a>Étapes suivantes
Lecture [les charges de travail puis-je protéger ?](site-recovery-workload.md) toolearn plus sur la protection des charges de travail enterprise avec Azure Site Recovery.
