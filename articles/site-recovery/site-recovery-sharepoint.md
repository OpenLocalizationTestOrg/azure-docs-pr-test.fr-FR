---
title: "aaaReplicate une application de SharePoint à plusieurs niveaux à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Cet article décrit comment tooreplicate une application de SharePoint à plusieurs niveaux à l’aide des fonctionnalités d’Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: sutalasi
ms.openlocfilehash: d856034ac2a3c95b0c1f0cf85e62c4e7a5a3210f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-sharepoint-application-for-disaster-recovery-using-azure-site-recovery"></a>Répliquer une application SharePoint multiniveau pour la récupération d’urgence à l’aide d’Azure Site Recovery

Cet article décrit en détail comment une application SharePoint à l’aide de tooprotect [Azure Site Recovery](site-recovery-overview.md).


## <a name="overview"></a>Vue d'ensemble

Microsoft SharePoint est une application puissante qui peut aider un groupe ou service à s’organiser, à collaborer et à partager des informations. SharePoint permet les portails intranet, la gestion des documents et fichiers, la collaboration, les réseaux sociaux, les réseaux extranet, les sites web, la recherche de contenu d’entreprise et le décisionnel. Elle offre également des capacités d’intégration de système, d’intégration de processus et d’automatisation de flux de travail. En règle générale, les organisations le considérer comme un niveau 1 application sensibles toodowntime des pertes de données.

Aujourd'hui, Microsoft SharePoint ne fournit aucune capacité de récupération d’urgence prête à l’emploi. Quel que soit le type de hello et l’échelle d’un incident, récupération implique l’utilisation de hello d’un centre de données de secours que vous pouvez récupérer la batterie de serveurs hello pour. Centres de données de secours sont requis pour les scénarios où les systèmes redondants locaux et les sauvegardes ne peut pas récupérer à partir de la panne hello au centre de données principal hello.

Une solution de récupération d’urgence doit permettre la modélisation des plans de récupération autour des architectures d’application complexe hello tels que SharePoint. Il doit également être hello capacité tooadd personnalisé étapes toohandle application mappages entre les différents niveaux et par conséquent permettent le basculement par simple clic avec une RTO inférieure dans les cas de hello d’urgence.

Cet article décrit en détail comment une application SharePoint à l’aide de tooprotect [Azure Site Recovery](site-recovery-overview.md). Cet article traite des meilleures pratiques pour la réplication d’un tooAzure d’application SharePoint à trois niveaux, comment vous pouvez effectuer un exercice de récupération d’urgence, et le mode de basculement hello application tooAzure.

Vous pouvez regarder hello sous vidéo sur la récupération d’un tooAzure d’application de couche multiples.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/Disaster-Recovery-of-load-balanced-multi-tier-applications-using-Azure-Site-Recovery/player]


## <a name="prerequisites"></a>Composants requis

Avant de commencer, assurez-vous que vous comprenez les suivant hello :

1. [Réplication d’un tooAzure de machine virtuelle](site-recovery-vmware-to-azure.md)
2. Comment trop[concevoir un réseau de récupération](site-recovery-network-design.md)
3. [Effectuer un tooAzure de basculement de test](site-recovery-test-failover-to-azure.md)
4. [Effectuer un basculement tooAzure](site-recovery-failover.md)
5. Comment trop[répliquer un contrôleur de domaine](site-recovery-active-directory.md)
6. Comment trop[répliquer de SQL Server](site-recovery-sql.md)

## <a name="sharepoint-architecture"></a>Architecture SharePoint

SharePoint peut être déployé sur un ou plusieurs serveurs à l’aide des topologies à plusieurs niveaux et les rôles de serveur tooimplement une conception de batterie de serveurs qui répond à des objectifs spécifiques. Une batterie de serveurs SharePoint de grande capacité et à forte demande qui prend en charge un grand nombre d’utilisateurs simultanés et un grand nombre d’éléments de contenu utilise le regroupement de service dans le cadre de sa stratégie d’évolutivité. Cette approche implique l’exécution des services sur des serveurs dédiés, regroupement de ces services et puis montée en puissance parallèle de serveurs de hello en tant que groupe. Hello topologie suivante illustre les service hello et serveur pour une batterie de serveurs SharePoint à trois niveaux de regroupement. Pour obtenir des instructions détaillées sur les différentes topologies de SharePoint, consultez tooSharePoint documentation et les architectures de ligne de produit. Vous trouverez plus d’informations sur le déploiement de SharePoint 2013 dans [ce document](https://technet.microsoft.com/en-us/library/cc303422.aspx).



![Modèle de déploiement 1](./media/site-recovery-sharepoint/sharepointarch.png)


## <a name="site-recovery-support"></a>Prise en charge de Site Recovery

Pour la création de cet article, des machines virtuelles VMware avec Windows Server 2012 R2 Enterprise ont été utilisées. Les applications SharePoint 2013 Enterprise Edition et SQL Server 2014 Enterprise Edition ont été utilisées. Comme la réplication de Site Recovery est indépendant de l’application, les recommandations hello fournies ici concernent toohold attendu sur également les scénarios suivants.

### <a name="source-and-target"></a>Source et cible

**Scénario** | **site secondaire de tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Oui | Oui
**VMware** | Oui | Oui
**Serveur physique** | Oui | Oui

### <a name="sharepoint-versions"></a>Versions de SharePoint
Hello SharePoint server versions suivantes est prises en charge.

* SharePoint Server 2013 Standard
* SharePoint Server 2013 Enterprise
* SharePoint Server 2016 Standard
* SharePoint Server 2016 Enterprise

### <a name="things-tookeep-in-mind"></a>Tookeep choses à l’esprit

Si vous utilisez un cluster basé sur le disque partagé en tant que n’importe quel niveau dans votre application, puis à ne pas être en mesure de toouse Site Recovery réplication tooreplicate ces ordinateurs virtuels. Vous pouvez utiliser la réplication native fournie par l’application hello, puis utiliser un [plan de récupération](site-recovery-create-recovery-plans.md) toofailover tous les niveaux.

## <a name="replicating-virtual-machines"></a>Réplication des machines virtuelles

Suivez [ce guide](site-recovery-vmware-to-azure.md) toostart tooAzure de machine virtuelle hello de réplication.

* Une fois la réplication hello est terminée, assurez-vous que vous ordinateur virtuel de tooeach de chaque couche et sélectionnez le même groupe à haute disponibilité ' répliqué élément > Paramètres > Propriétés > calcul et réseau ». Par exemple, si votre niveau web a 3 machines virtuelles, assurez-vous de hello toutes les machines 3 virtuelles sont configurés partie toobe du même groupe de disponibilité dans Azure.

    ![Set-Availability-Set](./media/site-recovery-sharepoint/select-av-set.png)

* Pour obtenir des conseils sur la protection de Active Directory et DNS, voir la rubrique trop[protéger Active Directory et DNS](site-recovery-active-directory.md) document.

* Pour obtenir des conseils sur la protection de niveau base de données en cours d’exécution sur SQL server, voir la rubrique trop[protéger SQL Server](site-recovery-active-directory.md) document.

## <a name="networking-configuration"></a>Configuration de la mise en réseau

### <a name="network-properties"></a>Propriétés du réseau

* Pour hello application et le niveau Web machines virtuelles, configurez les paramètres de réseau dans le portail Azure afin que machines virtuelles de hello toohello attaché droite DR réseau après le basculement.

    ![Sélectionner le réseau](./media/site-recovery-sharepoint/select-network.png)


* Si vous utilisez une adresse IP statique, puis spécifiez IP hello souhaité hello tootake de machine virtuelle Bonjour **adresse IP cible** champ

    ![Définir l’adresse IP statique](./media/site-recovery-sharepoint/set-static-ip.png)

### <a name="dns-and-traffic-routing"></a>Routage du trafic et DNS

Pour internet faisant face à des sites, [créer un profil Traffic Manager de type de 'Priority'](../traffic-manager/traffic-manager-create-profile.md) Bonjour abonnement Azure. Puis configurez votre profil Traffic Manager et de DNS Bonjour suivant manière.


| **Where** | **Source** | **Cible**|
| --- | --- | --- |
| DNS public | DNS public pour les sites SharePoint <br/><br/> Exemple : sharepoint.contoso.com | Traffic Manager <br/><br/> contososharepoint.trafficmanager.net |
| DNS local | sharepointonprem.contoso.com | Adresse IP publique sur la batterie de serveurs locale hello |


Bonjour, le profil Traffic Manager [créer des points de terminaison principal et de récupération hello](../traffic-manager/traffic-manager-configure-priority-routing-method.md). Utilisez le point de terminaison externe hello pour le point de terminaison local et l’adresse IP publique pour le point de terminaison Azure. Assurez-vous que priorité de hello est définie de point de terminaison local tooon plus élevée.

Hôte d’une page de test sur un port spécifique (par exemple, 800) de niveau de web SharePoint hello par ordre de Traffic Manager tooautomatically détecter disponibilité après basculement. Il s’agit d’une solution de contournement si vous ne pouvez pas activer l’authentification anonyme sur un de vos sites SharePoint.

[Configurer le profil Traffic Manager hello](../traffic-manager/traffic-manager-configure-priority-routing-method.md) avec hello sous les paramètres.

* Méthode de routage - « Priorité »
* DNS heure toolive (TTL) - « 30 secondes'
* Paramètres d’analyse de point de terminaison - Si vous pouvez activer l’authentification anonyme, vous pouvez donner un point de terminaison de site web spécifique. Ou bien, vous pouvez utiliser une page de test sur un port spécifique (800 par exemple).

## <a name="creating-a-recovery-plan"></a>Création d’un plan de récupération

Un plan de récupération permet de séquençage hello de basculement de différents niveaux dans une application multicouche, par conséquent, de maintenir la cohérence des applications. Lors de la création d’un plan de récupération pour une application web multicouche, suivez hello étapes ci-dessous. [En savoir plus sur la création d’un plan de récupération](site-recovery-runbook-automation.md#customize-the-recovery-plan).

### <a name="adding-virtual-machines-toofailover-groups"></a>Ajout de groupes de machines virtuelles toofailover

1. Créer un plan de récupération en ajoutant hello application et le niveau Web machines virtuelles.
2. Cliquez sur « Personnaliser » toogroup hello machines virtuelles. Par défaut, toutes les machines virtuelles font partie du « Groupe 1 ».

    ![Personnaliser un RP](./media/site-recovery-sharepoint/rp-groups.png)

3. Créer un autre groupe (groupe 2) et déplacer le niveau Web de hello machines virtuelles dans le nouveau groupe de hello. Vos machines virtuelles de niveau application doivent faire partie du « Groupe 1 » tandis que les machines virtuelles de niveau web doivent faire partie du « Groupe 2 ». Il s’agit de tooensure qui hello application machines virtuelles de couche démarrer tout d’abord suivi par les ordinateurs virtuels du niveau Web.


### <a name="adding-scripts-toohello-recovery-plan"></a>Ajout de scripts de plan de récupération toohello

Vous pouvez déployer les scripts d’Azure Site Recovery hello couramment utilisé dans votre compte Automation bouton hello « Déployer tooAzure » ci-dessous. Lorsque vous utilisez n’importe quel script publiée, assurez-vous que vous suivez les instructions de hello dans le script de hello.

[![Déployer tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)

1. Ajouter un script de pré too'Group 1' toofailover groupe de disponibilité SQL. Utiliser hello 'ASR-SQL-FailoverAG' script est publié dans les exemples de scripts hello. Assurez-vous de, suivez les instructions de hello de script de hello et apporter des modifications de hello requis dans le script de hello en conséquence.

    ![Add-AG-Script-Step-1](./media/site-recovery-sharepoint/add-ag-script-step1.png)

    ![Add-AG-Script-Step-2](./media/site-recovery-sharepoint/add-ag-script-step2.png)

2. Ajouter un tooattach de script action post un équilibrage de charge sur hello machines virtuelles ayant basculé de niveau de Web (groupe 2). Utiliser hello 'ASR-AddSingleLoadBalancer' script est publié dans les exemples de scripts hello. Assurez-vous de, suivez les instructions de hello de script de hello et apporter des modifications de hello requis dans le script de hello en conséquence.

    ![Add-LB-Script-Step-1](./media/site-recovery-sharepoint/add-lb-script-step1.png)

    ![Add-LB-Script-Step-2](./media/site-recovery-sharepoint/add-lb-script-step2.png)

3. Ajoutez une étape manuelle tooupdate hello DNS les enregistrements toopoint toohello nouvelle batterie de serveurs dans Azure.

    * Pour les sites accessibles sur Internet, aucune mise à jour des DNS n’est obligatoire après le basculement. Hello les étapes décrites dans la section tooconfigure Traffic Manager de hello « Guide de mise en réseau ». Si hello profil Traffic Manager a été configuré comme décrit dans la section précédente de hello, ajoutez un port de factice de tooopen (800 dans l’exemple de hello) de script sur hello machine virtuelle Azure.

    * Pour les sites internes exposés à ajouter charge équilibrage IP d’une étape manuelle tooupdate hello DNS toopoint enregistrement toohello Web niveau machine virtuelle.

4. Ajouter une application de recherche toorestore étape manuelle à partir d’une sauvegarde ou démarrer un nouveau service de recherche.

5. Pour restaurer l’application de service de recherche à partir d’une sauvegarde, suivez les étapes ci-dessous.

    * Cette méthode suppose qu’une sauvegarde de hello Application de Service de recherche a été effectuée avant les événements graves hello et que la sauvegarde hello est disponible sur le site de récupération d’urgence de hello.
    * Peut facilement être cela par la planification de sauvegarde de hello (par exemple, une fois par jour) et à l’aide d’une sauvegarde de copie procédure tooplace hello sur site de récupération d’urgence de hello. Les procédures de copie peuvent inclure des programmes par script comme AzCopy (Azure Copy) ou la configuration de DFSR (Distributed File Services Replication).
    * Maintenant que hello SharePoint batterie de serveurs est en cours d’exécution, accédez hello l’Administration centrale, « Sauvegarde et restauration » et sélectionnez Restaurer. emplacement de sauvegarde hello spécifié interroge Hello restauration (vous devrez peut-être valeur hello de tooupdate). Sélectionnez la sauvegarde de l’Application de Service de recherche hello toorestore voulue.
    * La recherche est restaurée. N’oubliez pas que hello restauration attend toofind hello même topologie (même nombre de serveurs) et le même disque dur lettres affectées toothose serveurs. Pour plus d’informations, consultez le document [« Restaurer une application de service de recherche dans SharePoint 2013 »](https://technet.microsoft.com/library/ee748654.aspx).


6. Pour démarrer avec une nouvelle application de service de recherche, suivez les étapes ci-dessous.

    * Cette méthode suppose qu’une sauvegarde de base de données « Administration de la recherche » hello est disponible sur le site de récupération d’urgence de hello.
    * Hello autres bases de données d’Application de Service de recherche ne sont pas répliqués, ils doivent toobe recréée. Par conséquent, les toodo accédez tooCentral Administration et supprimer l’Application de Service de recherche de hello. Sur les serveurs qui hello hôte Index de recherche, supprimer les fichiers d’index hello.
    * Recréer hello Application de Service de recherche et il recrée les bases de données hello. Il est recommandé de toohave préparée un script qui crée de nouveau cette application de service, car il n’est pas possible de tooperform toutes les actions via l’interface utilisateur graphique de hello. Par exemple, emplacement de lecteur d’index hello et la configuration de topologie de recherche hello sont uniquement possibles à l’aide des applets de commande PowerShell de SharePoint. Utilisez l’applet de commande Windows PowerShell hello SPEnterpriseSearchServiceApplication de restauration et spécifiez hello de journaux et la réplication de base de données de l’Administration de la recherche, Search_Service__DB. Cette applet de commande permet la configuration de la recherche hello, schéma, les propriétés gérées, règles et sources et crée un ensemble par défaut de hello autres composants.
    * Une fois que hello Qu'application de Service de recherche a être recréé, vous devez démarrer une analyse complète pour chaque hello toorestore de source du contenu du Service de recherche. Vous perdrez quelques informations analytique de batterie de local hello, telles que des recommandations de la recherche.

7. Une fois toutes les étapes de hello sont effectuées, enregistrez le plan de récupération hello et plan de récupération final hello doit ressembler à la suivante.

    ![RP enregistré](./media/site-recovery-sharepoint/saved-rp.png)

## <a name="doing-a-test-failover"></a>Exécution d’un test de basculement
Suivez [ce guide](site-recovery-test-failover-to-azure.md) toodo un test de basculement.

1.  TooAzure portail, sélectionnez le coffre de votre Service de récupération.
2.  Cliquez sur le plan de récupération hello créé pour l’application SharePoint.
3.  Cliquez sur Test de basculement.
4.  Sélectionnez le point de récupération et le processus de basculement de test de réseau virtuel Azure toostart hello.
5.  Une fois les environnement secondaire hello, vous pouvez effectuer vos validations.
6.  Une fois les validations hello sont terminées, vous pouvez cliquer sur « Test de basculement nettoyage » sur le plan de récupération hello et environnement de test de basculement hello est nettoyé.

Pour obtenir des conseils sur effectuant un test de basculement pour Active Directory et DNS, consultez trop[tester des considérations relatives au basculement pour Active Directory et DNS](site-recovery-active-directory.md#test-failover-considerations) document.

Pour obtenir des conseils sur la création de test de basculement pour SQL toujours sur les groupes de disponibilité, consultez trop[effectuer le Test du basculement de SQL Server Always On](site-recovery-sql.md#steps-to-do-a-test-failover) document.

## <a name="doing-a-failover"></a>Exécution d’un basculement
Suivez [ce guide](site-recovery-failover.md) pour réaliser un basculement.

1.  TooAzure portail, sélectionnez votre coffre Recovery Services.
2.  Cliquez sur le plan de récupération hello créé pour l’application SharePoint.
3.  Cliquez sur « Basculement ».
4.  Sélectionnez le processus de basculement de hello toostart de point de récupération.

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez en savoir plus sur la [réplication d’autres applications](site-recovery-workload.md) à l’aide de Site Recovery.
