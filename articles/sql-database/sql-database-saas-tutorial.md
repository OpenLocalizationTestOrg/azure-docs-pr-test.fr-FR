---
title: "aaaDeploy et Explorer les application SaaS de Wingtip hello mutualisée qui utilise la base de données SQL Azure | Documents Microsoft"
description: "Déployer et Explorer l’application hello Wingtip SaaS mutualisée, qui illustre les modèles SaaS à l’aide de la base de données SQL Azure."
keywords: "didacticiel sur les bases de données SQL"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: sstein
ms.openlocfilehash: 7c528ee19472d3b8c7a285b2f86013945e8f4bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-explore-a-multi-tenant-application-that-uses-azure-sql-database---wingtip-saas"></a>Déployer et explorer une application mutualisée qui utilise Azure SQL Database - Wingtip SaaS

Dans ce didacticiel, vous déployez et explorez hello Wingtip SaaS application. application Hello utilise un base de données-par-client, modèle d’application SaaS, tooservice plusieurs clients. l’application Hello est conçue tooshowcase les fonctionnalités de base de données SQL Azure qui simplifient l’activation de scénarios de SaaS.

Cinq minutes après avoir cliqué sur hello *déployer tooAzure* bouton ci-dessous, vous avez une application SaaS mutualisée, à l’aide de base de données SQL, jusqu'à et en cours d’exécution dans le cloud de hello. application Hello est déployée dans les clients exemple trois, chacun avec sa propre base de données, tous déployé dans un pool élastique SQL. application Hello est déployé tooyour abonnement Azure, vous offrant un accès complet tooexplore et utiliser des composants d’application individuels hello. scripts de gestion et de code source d’application Hello sont disponibles dans hello référentiel WingtipSaaS GitHub.


Ce didacticiel vous apprend à effectuer les opérations suivantes :

> [!div class="checklist"]

> * Comment toodeploy hello application Wingtip SaaS
> * Où tooget hello code source d’applications et les scripts d’administration
> * Sur les serveurs de hello, les pools et les bases de données qui composent application hello
> * Comment les clients sont mappées les données tootheir par hello *catalogue*
> * Comment tooprovision un nouveau client.
> * Comment toomonitor locataire activité dans une application hello

tooexplore divers SaaS conception et gestion des modèles, un [série de didacticiels associées](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials) n’est disponible qui reposent sur ce déploiement initial. Tout en parcourant les didacticiels hello, plonger dans les scripts hello fourni et examinez l’implémentation de différents modèles de SaaS hello. Parcourir les scripts de hello dans chaque didacticiel toogain une compréhension plus approfondie comment tooimplement hello base de données SQL de nombreuses fonctionnalités qui simplifient le développement d’applications SaaS.

## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel, assurez-vous que hello est suivant des conditions préalables requises sont effectuées :

* Azure PowerShell est installé. Pour plus d’informations, consultez [Bien démarrer avec Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).

## <a name="deploy-hello-wingtip-saas-application"></a>Déployer l’application de Wingtip SaaS hello

Déploiement d’une application de Wingtip SaaS hello :

1. En cliquant sur hello **déployer tooAzure** bouton ouvre le modèle de déploiement Wingtip SaaS hello toohello portail Azure. modèle de Hello nécessite deux valeurs de paramètre ; un nom pour un groupe de ressources et un nom d’utilisateur qui distingue ce déploiement à partir d’autres déploiements d’application de Wingtip SaaS hello. étape suivante de Hello fournit des détails sur la définition de ces valeurs.

   Assurez-vous que toonote hello exactement les valeurs que vous utilisez, car vous devrez tooenter dans une configuration de fichier plus tard.

   <a href="http://aka.ms/deploywtpapp" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

1. Entrez les valeurs des paramètres requis pour le déploiement de hello :

    > [!IMPORTANT]
    > Certaines authentifications et pare-feu de serveur sont volontairement non sécurisés à des fins de démonstration. **Créez un nouveau groupe de ressources** et n’utilisez pas de groupes de ressources, serveurs ou pools existants. N’utilisez pas cette application, ni les ressources qu’elle crée, pour la production. Supprimer cette ressource de groupe lorsque vous avez terminé avec hello application toostop liées à la facturation.

    * **Groupe de ressources** : sélectionnez **nouvel** et fournir un **nom** pour le groupe de ressources hello. Sélectionnez un **emplacement** à partir de la liste déroulante de hello.
    * **Utilisateur** : certaines ressources nécessitent des noms globalement uniques. l’unicité de tooensure, chaque fois que vous déployez l’application hello fournir une valeur ressources toodifferentiate créer, à partir des ressources créées par d’autres déploiements de hello application de Wingtip. Il est recommandé de toouse un court **utilisateur** nom, tels que vos initiales plus un nombre (par exemple, *bg1*) et l’utiliser ensuite dans le nom de groupe de ressources hello (par exemple, *wingtip-bg1*). Le paramètre **Utilisateur** peut contenir uniquement des lettres, des chiffres et des traits d’union (sans espaces). premier et dernier caractères Hello doit être une lettre ou un chiffre (toutes les minuscules recommandé).


1. **Déployer l’application hello**.

    * Cliquez sur tooagree toohello termes et conditions.
    * Cliquez sur **Achat**.

1. Surveiller l’état du déploiement en cliquant sur **Notifications** (icône de cloche hello à droite de la zone de recherche hello). Application de Wingtip SaaS hello déploiement prend environ cinq minutes.

   ![déploiement réussi](media/sql-database-saas-tutorial/succeeded.png)

## <a name="download-and-unblock-hello-wingtip-saas-scripts"></a>Téléchargez et débloquer des scripts de hello Wingtip SaaS

Pendant le déploiement de l’application hello, téléchargez les scripts de gestion et de code source hello.

> [!IMPORTANT]
> Le contenu exécutable (scripts, DLL) peut être bloqué par Windows lorsque des fichiers zip sont téléchargés à partir d’une source externe puis extraits. Lorsque vous extrayez les scripts hello à partir d’un fichier zip, suivez les étapes de hello ci-dessous le fichier .zip de hello toounblock avant l’extraction. Cela garantit que les scripts de hello sont autorisés à toorun.

1. Parcourir trop[du référentiel github hello Wingtip SaaS](https://github.com/Microsoft/WingtipSaaS).
1. Cliquez sur **Cloner ou télécharger**.
1. Cliquez sur **ZIP de téléchargement** et enregistrez le fichier de hello.
1. Avec le bouton hello **WingtipSaaS-master.zip** de fichiers, puis sélectionnez **propriétés**.
1. Sur hello **général** onglet, sélectionnez **Unblock**, puis cliquez sur **appliquer**.
1. Cliquez sur **OK**.
1. Extrayez les fichiers hello.

Les scripts se trouvent dans hello *... \\WingtipSaaS-master\\Modules d’apprentissage* dossier.

## <a name="update-hello-configuration-file-for-this-deployment"></a>Mettre à jour le fichier de configuration hello pour ce déploiement

Avant d’exécuter des scripts, définissez hello *groupe de ressources* et *utilisateur* valeurs **UserConfig.psm1**. Permet de définir des valeurs toohello que vous avez défini pendant le déploiement de ces variables.

1. Ouvrir... \\Modules d’apprentissage\\*UserConfig.psm1* Bonjour *PowerShell ISE*
1. Mise à jour *ResourceGroupName* et *nom* avec des valeurs spécifiques hello pour votre déploiement (sur les lignes 10 et 11 uniquement).
1. Enregistrer les modifications de hello !

Ce paramètre ici simplement vous évite d’avoir tooupdate ces valeurs spécifiques au déploiement dans chaque script.

## <a name="run-hello-application"></a>Exécutez l’application hello

application Hello présente des systèmes, tels que les salles de concert, service jazz, sportives, etc., qui hébergent des événements. Les lieux inscrire en tant que clients (ou locataires) de plateforme de Wingtip hello, pour un moyen simple toolist d’événements et de vendent des tickets. Chaque salle Obtient un toomanage d’application web personnalisée et répertorier leurs événements et vendre des tickets, indépendantes et isolés des autres clients. Dans les coulisses hello, chaque locataire Obtient une base de données SQL déployé dans un pool élastique SQL.

Un centre **concentrateur d’événements** fournit une liste de client URL spécifique tooyour déploiement.

1. Ouvrez hello _concentrateur d’événements_ dans votre navigateur web : http://events.wtp.&lt; UTILISATEUR&gt;. trafficmanager.net (à remplacer par le nom d’utilisateur de votre déploiement) :

    ![events hub](media/sql-database-saas-tutorial/events-hub.png)

1. Cliquez sur **Fabrikam Jazz Club** dans le *concentrateur d’événements*.

   ![Événements](./media/sql-database-saas-tutorial/fabrikam.png)


distribution de hello toocontrol des demandes entrantes, hello application utilise [ *Azure Traffic Manager*](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview). pages d’événements Hello, qui sont spécifiques du client, requièrent que les noms de client sont inclus dans les URL de hello. Tous les hello client les URL sont spécifiques à votre *utilisateur* valeur et de suivre ce format : http://events.wtp.&lt; UTILISATEUR&gt;.trafficmanager.net/*fabrikamjazzclub*. Hello événements application analyse le nom du client à partir de l’URL de hello hello et utilise une clé tooaccess un catalogue à l’aide de toocreate [ *gestion de carte de partitions*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-scale-shard-map-management). mappages de catalogue Hello hello emplacement de base de données du client de la clé toohello. Hello **concentrateur d’événements** utilise des métadonnées dans le nom du locataire hello hello catalogue tooretrieve associé à chaque liste de hello tooprovide de base de données d’URL.

Dans un environnement de production, vous devez généralement créer un enregistrement DNS CNAME pour [ *pointer un domaine internet de société* ](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-point-internet-domain) pour le profil traffic manager hello.

## <a name="start-generating-load-on-hello-tenant-databases"></a>Démarrer la génération de charge sur les bases de données clientes hello

Maintenant que hello application est déployée, disons toowork ! Hello *LoadGenerator de démonstration* script PowerShell démarre une charge de travail en cours d’exécution sur toutes les bases de données client. chargement du monde réel Hello sur de nombreuses applications SaaS est généralement sporadique et imprévisibles. toosimulate ce type de charge, le Générateur de hello génère une charge distribuée entre tous les locataires, rafales aléatoire sur chaque client qui se produisent à intervalles aléatoires. Pour cette raison qu’il prend quelques minutes tooemerge de modèle de charge hello, il est donc meilleures Générateur de hello toolet exécuter au moins trois ou quatre minutes avant d’analyser hello charger.

1. Bonjour *PowerShell ISE*, ouvrez hello... \\Modules d’apprentissage\\utilitaires\\*LoadGenerator.ps1 de démonstration* script.
1. Appuyez sur **F5** pour exécuter le script de hello et démarrer le Générateur de charge hello (laissez hello valeurs par défaut pour l’instant).

> [!IMPORTANT]
> toorun autres scripts, ouvrez une nouvelle fenêtre de PowerShell ISE. Générateur de charge Hello est en cours d’exécution comme une série de tâches dans votre session PowerShell locale. Hello *LoadGenerator.ps1 de démonstration* script lance le script de génération hello charge réelle, ce qui s’exécute comme une tâche de premier plan ainsi qu’une série de tâches de génération de charge en arrière-plan. Une tâche du Générateur de charge est appelée pour chaque base de données enregistré dans le catalogue de hello. travaux de Hello est en cours d’exécution dans votre session PowerShell locale, afin que la fermeture de session de PowerShell hello s’arrête tous les travaux. Si vous mettez en veille l’ordinateur, la génération de la charge est interrompue et reprendra dès la sortie de veille de votre ordinateur.

Une fois que le Générateur de charge hello appelle les tâches de génération de charge pour chaque client, la tâche de premier plan hello reste dans un état d’appel de travail, où elle démarre les tâches en arrière-plan supplémentaire pour les nouveaux clients sont ensuite configurés. Vous pouvez utiliser *Ctrl-C* ou appuyez sur hello *arrêter* tâche de premier plan bouton toostop hello, mais en arrière-plan existant travaux continuent de génération de la charge sur chaque base de données. Si vous devez toomonitor et contrôlez les tâches en arrière-plan hello, utilisez *Get-Job*, *Receive-Job* et *Stop-Job*. Lors de la tâche de premier plan hello est en cours d’exécution vous ne peut pas utiliser hello même tooexecute de session PowerShell autres scripts. toorun autres scripts, ouvrez une nouvelle fenêtre de PowerShell ISE.

Si vous souhaitez toorestart hello charge générateur session, par exemple avec des paramètres différents, vous pouvez arrêter tâche de premier plan hello, puis exécutez de nouveau le hello *LoadGenerator.ps1 de démonstration* script. Réexécuter *LoadGenerator.ps1 de démonstration* arrête d’abord les tâches en cours et puis générateur redémarrages hello, qui lance un nouveau jeu de travaux à l’aide des paramètres actuels de hello.

Pour l’instant, laissez le Générateur de charge hello en cours d’exécution dans l’état d’appel de travail hello.


## <a name="provision-a-new-tenant"></a>Approvisionner un nouveau locataire

déploiement initial de Hello crée trois locataires d’exemple, mais nous allons créer une autre locataire toosee comment cela affecte l’application hello déployé. flux de travail Hello Wingtip SaaS approvisionnement-locataires est détaillée dans hello [didacticiel fourniture et catalogue](sql-database-saas-tutorial-provision-and-catalog.md). Dans cette étape, vous créez rapidement un nouveau locataire.

1. Ouvrir... \\Modules\Provision d’apprentissage et de catalogue\\*ProvisionAndCatalog.ps1 de démonstration* Bonjour *PowerShell ISE*.
1. Appuyez sur **F5** pour exécuter le script hello (laissez hello par défaut pour l’instant).

   > [!NOTE]
   > Utilisent de nombreux scripts Wingtip SaaS *$PSScriptRoot* tooallow navigation dans les fonctions de toocall de dossiers dans d’autres scripts. Cette variable est évaluée uniquement lorsque le script de hello est exécuté en appuyant sur **F5**.  La mise en surbrillance et l’exécution d’une sélection (**F8**) pouvant entraîner des erreurs, appuyez sur **F5** lors de l’exécution des scripts.

Hello nouvelle base de données est créé dans un pool élastique SQL, initialisé et enregistré dans le catalogue de hello. Après le déploiement réussi, client hello de vente incitative ticket *événements* site s’affiche dans votre navigateur :

![Nouveau locataire](./media/sql-database-saas-tutorial/red-maple-racing.png)

Actualiser hello *concentrateur d’événements* et client hello apparaît maintenant dans la liste de hello.


## <a name="explore-hello-servers-pools-and-tenant-databases"></a>Explorer des serveurs hello, pools et bases de données de client

Maintenant que vous avez démarré une charge en cours d’exécution sur le regroupement de hello de clients, examinons quelques-unes des ressources hello qui ont été déployés :

1. Dans le [portail Azure](http://portal.azure.com), accédez tooyour la liste des serveurs SQL Server et le **catalogue -&lt;utilisateur&gt;**  server. serveur de catalogue Hello contient deux bases de données. Hello **tenantcatalog**et hello **basetenantdb** (vide *or* ou de la base de données de modèle qui est copié toocreate nouveaux clients).

   ![bases de données](./media/sql-database-saas-tutorial/databases.png)

1. Revenir en arrière tooyour la liste des serveurs SQL Server et ouvrez hello **tenants1 -&lt;utilisateur&gt;**  serveur qui contient les bases de données clientes hello. Chaque base de données de locataires est une base de données _élastique standard_ dans un pool standard de 50 eDTU. Notez également est un _érable rouge course_ de base de données, la base de données client hello vous avez configuré précédemment.

   ![server](./media/sql-database-saas-tutorial/server.png)

## <a name="monitor-hello-pool"></a>Moniteur hello pool

Si le Générateur de charge hello s’exécute pendant plusieurs minutes, suffisamment de données doit être disponible toostart examiner certaines hello fonctionnalités intégrées aux bases de données et des pools d’analyse.

1. Parcourir le serveur de toohello **tenants1 -&lt;utilisateur&gt;**, puis cliquez sur **Pool1** pour afficher l’utilisation des ressources pour le pool de hello (Générateur de charge hello exécuté pendant une heure Bonjour suivant graphiques) :

   ![surveiller un pool](./media/sql-database-saas-tutorial/monitor-pool.png)

Ces deux graphiques montrent bien que les pools élastiques et SQL Database sont parfaitement adaptés aux charges de travail de l’application SaaS. Quatre bases de données qui sont chacun éclatement tooas autant 40 Edtu est facilement pris en charge dans un pool 50 eDTU. Si elles ont été déployées en tant que bases de données autonomes, ils le feraient chaque toobe besoin une S2 (DTU 50) toosupport hello pics. coût Hello de 4 bases de données autonome S2 est près de 3 fois hello du pool de hello et pool de hello dispose toujours de suffisamment d’espace disponible pour plusieurs bases de données. Dans des situations réelles, les clients de base de données SQL en cours d’exécution des bases de données too500 dans des pools d’eDTU 200. Pour plus d’informations, consultez hello [didacticiel l’analyse des performances](sql-database-saas-tutorial-performance-monitoring.md).


## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris à effectuer les opérations suivantes :

> [!div class="checklist"]

> * Comment toodeploy hello application Wingtip SaaS
> * Sur les serveurs de hello, les pools et les bases de données qui composent application hello
> * Les clients sont des données tootheir mappé avec hello *catalogue*
> * Comment tooprovision nouveaux clients
> * Comment toomonitor de l’utilisation du pool tooview locataire activité
> * Comment toodelete exemple ressources toostop liées à la facturation

Essayez maintenant hello [didacticiel approvisionner et de catalogue](sql-database-saas-tutorial-provision-and-catalog.md)



## <a name="additional-resources"></a>Ressources supplémentaires

* Supplémentaires [didacticiels qui s’appuient sur hello application Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* toolearn sur les pools élastiques, consultez [ *qu’est un pool élastique SQL Azure*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool)
* toolearn sur les tâches élastiques, consultez [ *gestion des bases de données de cloud de montée en charge*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)
* toolearn sur les applications SaaS mutualisées, consultez [ *concevoir des modèles pour des applications SaaS mutualisées*](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)
