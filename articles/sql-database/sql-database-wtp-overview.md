---
title: "aaaIntro Wingtip SaaS - application mutualisée de base de données SQL Azure | Documents Microsoft"
description: "En savoir plus à l’aide d’un exemple d’application mutualisée qui utilise la base de données SQL Azure, application de Wingtip SaaS hello"
keywords: "didacticiel sur les bases de données SQL"
services: sql-database
author: stevestein
manager: jhubbard
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: sstein
ms.openlocfilehash: daeed293116fca22718831b780533be6ef2ad178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-wingtip-saas-application"></a>Introduction toohello application Wingtip SaaS

Hello *Wingtip SaaS* application est une architecture mutualisée exemple d’application, qui présente des avantages uniques de hello de base de données SQL. application Hello utilise un base de données-par-client, modèle d’application SaaS, tooservice plusieurs clients. application Hello est tooshowcase conçu les fonctionnalités de base de données SQL Azure qui permettent des scénarios SaaS, y compris plusieurs modèles de conception et la gestion SaaS. tooquickly route et en cours d’exécution, hello Wingtip SaaS application déploie en moins de cinq minutes !

Scripts de gestion et de code source d’application sont disponibles dans hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) référentiel github. scripts de hello toorun, [télécharger le dossier de Modules d’apprentissage hello](#download-and-unblock-the-wingtip-saas-scripts) tooyour les ordinateur local.

## <a name="sql-database-wingtip-saas-tutorials"></a>Didacticiels de l’application SaaS Wingtip de SQL Database

Après avoir déployé l’application hello, explorez hello suivant des didacticiels qui reposent sur le déploiement initial de hello. Ces didacticiels explorent des modèles SaaS courants qui tirent parti des fonctionnalités intégrées de SQL Database, de SQL Data Warehouse et d’autres services Azure. Didacticiels incluent des scripts PowerShell, avec des explications détaillées qui simplifient considérablement le fonctionnement, et l’implémentation hello mêmes modèles de gestion SaaS dans vos applications.


| Didacticiel | Description |
|:--|:--|
|[Déployer et Explorer hello Wingtip SaaS application](sql-database-saas-tutorial.md)| **COMMENCEZ ICI** Déployer et Explorer hello Wingtip SaaS application tooyour abonnement Azure. |
|[Approvisionner des clients et les inscrire dans le catalogue](sql-database-saas-tutorial-provision-and-catalog.md)| Découvrez comment hello application connecte à l’aide d’une base de données du catalogue de tootenants et comment le catalogue de hello mappe les locataires tootheir données. |
|[Surveiller et gérer les performances](sql-database-saas-tutorial-performance-monitoring.md)| Découvrez comment toouse analyse les fonctionnalités de base de données SQL, et comment tooset des alertes lorsque les seuils de performances sont atteints. |
|[Surveiller avec Log Analytics (OMS)](sql-database-saas-tutorial-log-analytics.md) | En savoir plus sur l’utilisation de [Analytique de journal](../log-analytics/log-analytics-overview.md) toomonitor de grandes quantités de ressources, entre plusieurs pools. |
|[Restaurer un client unique](sql-database-saas-tutorial-restore-single-tenant.md)| Découvrez comment toorestore tooa d’une base de données client préalable point dans le temps. Étapes toorestore tooa parallèles, laissant hello client base de données existante en ligne, sont également inclus. |
|[Gérer les schémas de client](sql-database-saas-tutorial-schema-management.md)| Découvrez comment tooupdate schéma et la mise à jour les données de référence sur tous les locataires Wingtip SaaS. |
|[Exécuter une analyse ad hoc](sql-database-saas-tutorial-adhoc-analytics.md) | Créez une base de données analytique ad hoc, puis exécutez des requêtes distribuées en temps réel sur tous les clients.  |
|[Exécuter une analyse des clients](sql-database-saas-tutorial-tenant-analytics.md) | Extrayez les données client dans une base de données analytique ou un entrepôt de données pour l’exécution de requêtes analytiques en mode hors connexion. |



## <a name="application-architecture"></a>Architecture de l'application

Hello Wingtip SaaS application utilise le modèle de base de données pour chaque locataire hello et l’efficacité toomaximize de pools élastiques de SQL. Pour la configuration et de mappage de données tootheir de clients, une base de données de catalogue est utilisé. application de Wingtip SaaS Hello core, utilise un pool avec trois exemples de clients, ainsi que hello du catalogue de base de données. Fin de nombreux hello Wingtip SaaS didacticiels produit déploiement initial de modules complémentaires toohello, en introduisant des bases de données analytiques, entre bases de données Gestion des schémas, etc..


![Architecture de SaaS Wingtip](media/sql-database-wtp-overview/app-architecture.png)


Tout en parcourant les didacticiels hello et utilisation de l’application hello, il est toofocus important sur les modèles de SaaS hello en matière de niveau de données toohello. En d’autres termes, vous concentrer sur la couche de données hello et ne pas analyser plus application hello proprement dit. Comprendre l’implémentation d’un de ces modèles SaaS hello est tooimplementing clé ces modèles dans vos applications, en prenant en compte toutes les modifications nécessaires pour vos besoins professionnels spécifiques.

## <a name="download-and-unblock-hello-wingtip-saas-scripts"></a>Téléchargez et débloquer des scripts de hello Wingtip SaaS

Le contenu exécutable (scripts, DLL) peut être bloqué par Windows lorsque des fichiers zip sont téléchargés à partir d’une source externe puis extraits. Lors de l’extraction des scripts de hello à partir d’un fichier zip, ***étapes hello ci-dessous le fichier .zip de hello toounblock avant d’extraire***. Cela garantit que les scripts de hello sont autorisés à toorun.

1. Parcourir trop[du référentiel github hello Wingtip SaaS](https://github.com/Microsoft/WingtipSaaS).
1. Cliquez sur **Cloner ou télécharger**.
1. Cliquez sur **ZIP de téléchargement** et enregistrez le fichier de hello.
1. Avec le bouton hello **WingtipSaaS-master.zip** de fichiers, puis sélectionnez **propriétés**.
1. Sur hello **général** onglet, sélectionnez **Unblock**.
1. Cliquez sur **OK**.
1. Extrayez les fichiers hello.

Les scripts se trouvent dans hello *... \\WingtipSaaS-master\\Modules d’apprentissage* dossier.


## <a name="working-with-hello-wingtip-saas-powershell-scripts"></a>Utilisation de hello Wingtip SaaS PowerShell Scripts

tooget hello plus en dehors de l’exemple hello vous devez toodive dans les scripts hello fourni. Utiliser des points d’arrêt et de parcourir les scripts hello, examinant hello les détails d’implémentation des différents modèles de SaaS hello. étape tooeasily via des scripts de hello fourni et des modules pour mieux comprendre, nous vous recommandons d’utiliser des hello de hello [PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).

### <a name="update-hello-configuration-file-for-your-deployment"></a>Mettre à jour le fichier de configuration hello pour votre déploiement

Modifier hello **UserConfig.psm1** fichier avec la valeur de groupe et d’utilisateur de ressources hello que vous définissez au cours du déploiement :

1. Ouvrez hello *PowerShell ISE* et de charge... \\Modules d’apprentissage\\*UserConfig.psm1* 
1. Mise à jour *ResourceGroupName* et *nom* avec des valeurs spécifiques hello pour votre déploiement (sur les lignes 10 et 11 uniquement).
1. Enregistrer les modifications de hello !

Ces valeurs simplement vous évite d’avoir tooupdate ces valeurs spécifiques au déploiement dans chaque script.

### <a name="execute-scripts-by-pressing-f5"></a>Exécuter des scripts en appuyant sur F5

Utilisent de plusieurs scripts *$PSScriptRoot* toonavigate dossiers, et *$PSScriptRoot* est évaluée uniquement lorsque les scripts sont exécutés en appuyant sur **F5**.  La mise en surbrillance et l’exécution d’une sélection (**F8**) pouvant entraîner des erreurs, appuyez sur **F5** lors de l’exécution des scripts.

### <a name="step-through-hello-scripts-tooexamine-hello-implementation"></a>Parcourez la mise en œuvre de hello scripts tooexamine hello

les scripts Hello meilleure manière toounderstand hello est en parcourant les toosee ce qu’elles font. Extraire hello inclus **démonstration -** des scripts qui présentent un flux de travail de haut niveau toofollow facile. Hello **démonstration -** scripts illustrent tooaccomplish requis de hello suit chaque tâche, par conséquent, définissez les points d’arrêt et exploration plus approfondie dans hello individuels nécessite une toosee détails d’implémentation hello différents modèles SaaS.

Conseils pour l’exploration et le parcours des scripts PowerShell :

* Ouvrez **démonstration -** scripts Bonjour PowerShell ISE.
* Exécutez ou continuez à exécuter le script à l’aide de la touche **F5** (l’utilisation de la touche **F8** n’est pas conseillée, car *$PSScriptRoot* n’est pas évalué lors de l’exécution des sélections d’un script).
* Placez des points d’arrêt en cliquant ou en sélectionnant une ligne et en appuyant sur **F9**.
* Survolez l’appel d’une fonction ou d’un script à l’aide de la touche **F10**.
* Parcourez l’appel d’une fonction ou d’un script à l’aide de la touche **F11**.
* Sortir de fonction en cours de hello ou à l’aide de l’appel de script **MAJ + F11**.


## <a name="explore-database-schema-and-execute-sql-queries-using-ssms"></a>Explorez le schéma de base de données et exécutez des requêtes SQL à l’aide de SSMS

Utilisez [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) tooconnect et parcourir hello des serveurs d’applications et des bases de données.

déploiement de Hello a initialement deux de la base de données SQL serveurs tooconnect trop hello *tenants1 -&lt;utilisateur&gt;*  serveur et hello *catalogue -&lt;utilisateur&gt;* server. tooensure une connexion réussie de démonstration, les deux serveurs ont un [règle de pare-feu](sql-database-firewall-configure.md) autoriser toutes les adresses IP par le biais.


1. Ouvrez *SSMS* et connectez-vous toohello *tenants1 -&lt;utilisateur&gt;. database.windows.net* server.
1. Cliquez sur **Connexion** > **Moteur de base de données...** :

   ![catalog server](media/sql-database-wtp-overview/connect.png)

1. Les informations d’identification de la démonstration sont : nom d’utilisateur = *developer*, mot de passe = *P@ssword1*.

   ![connection](media\sql-database-wtp-overview\tenants1-connect.png)

1. Répétez les étapes 2 et 3 et se connecter toohello *catalogue -&lt;utilisateur&gt;. database.windows.net* server.

Une fois la connexion établie, vous devez voir les deux serveurs. La liste des bases de données peut être différente, selon les locataires hello que vous avez configuré :

![object explorer](media/sql-database-wtp-overview/object-explorer.png)



## <a name="next-steps"></a>Étapes suivantes

[Déployer l’application de Wingtip SaaS hello](sql-database-saas-tutorial.md)
