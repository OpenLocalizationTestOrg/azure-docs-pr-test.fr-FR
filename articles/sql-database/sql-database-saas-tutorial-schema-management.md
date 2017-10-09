---
title: "schéma de base de données SQL Azure aaaManage dans une application mutualisée | Documents Microsoft"
description: "Gérer un schéma pour plusieurs locataires dans une application mutualisée qui utilise Azure SQL Database"
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
ms.date: 07/28/2017
ms.author: billgib; sstein
ms.openlocfilehash: ea946e556808dabd60dd39cb8173d0512d4bddec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-schema-for-multiple-tenants-in-hello-wingtip-saas-application"></a>Gérer le schéma pour plusieurs clients Bonjour application Wingtip SaaS

Hello [premier didacticiel Wingtip SaaS](sql-database-saas-tutorial.md) montre comment application hello peut configurer une base de données client et l’enregistrer dans le catalogue de hello. Comme n’importe quelle application, hello application Wingtip SaaS évolue au fil du temps et parfois nécessitera toohello de base de données les modifications. Modifications peuvent inclure en schéma nouvel ou modifié, les données de référence de nouveaux ou modifiés et les routines de la base de données Gestion des tâches tooensure optimal performances de l’application. Avec une application SaaS, ces modifications doivent toobe déployée de façon coordonnée entre un parc potentiellement massif de bases de données client. Pour ces toobe de modifications de client dans les futures bases de données, ils ont besoin toobe intégré hello processus de configuration.

Ce didacticiel explore les deux scénarios - déploiement de mises à jour des données de référence pour tous les locataires, et un index sur hello impliquait de nouveaux réglages de table contenant des données référence hello. Hello [travaux élastique](sql-database-elastic-jobs-overview.md) fonctionnalité est utilisée tooexecute ces opérations sur tous les locataires et hello *or* base de données client qui est utilisé comme modèle pour les nouvelles bases de données.

Ce didacticiel vous explique comment effectuer les opérations suivantes :

> [!div class="checklist"]

> * Créer un compte de travail
> * Interroger plusieurs clients
> * Mettre à jour les données dans toutes les bases de données de locataire
> * Créer un index sur une table dans toutes les bases de données de locataire


toocomplete ce didacticiel, assurez-vous que hello est suivant les conditions préalables sont remplies :

* Hello Wingtip SaaS application est déployée. toodeploy en moins de cinq minutes, consultez [déployer et Explorer hello Wingtip SaaS application](sql-database-saas-tutorial.md)
* Azure PowerShell est installé. Pour plus d’informations, consultez [Bien démarrer avec Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).
* version la plus récente Hello de SQL Server Management Studio (SSMS) est installée. [Télécharger et installer SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

*Ce didacticiel utilise des fonctionnalités de hello service de base de données SQL qui se trouvent dans une version d’évaluation limitée (travaux de base de données élastique). Si vous souhaitez toodo de ce didacticiel, fournissez votre id d’abonnement tooSaaSFeedback@microsoft.com associé au sujet = élastique aperçu de travaux. Après avoir reçu la confirmation que votre abonnement a été activé, [télécharger et installer les applets de commande hello dernière version préliminaire travaux](https://github.com/jaredmoo/azure-powershell/releases). Cette version préliminaire est limitée. Contactez SaaSFeedback@microsoft.com pour toute question ou demande de prise en charge associées.*


## <a name="introduction-toosaas-schema-management-patterns"></a>Introduction tooSaaS modèles de gestion des schémas

Hello client unique par base de données SaaS de modèle avantages dans nombreuses façons d’isolation des données hello qui résulte, mais à hello simultanément présente une complexité supplémentaire hello de maintenance et la gestion de bases de données. [Travaux élastique](sql-database-elastic-jobs-overview.md) facilite l’administration et la gestion de la couche de données SQL hello. Travaux vous toosecurely et fiable, exécuter des tâches (scripts T-SQL) indépendamment d’intervention de l’utilisateur ou d’entrée, par rapport à un groupe de bases de données. Cette méthode peut être utilisé toodeploy schéma et des modifications de données de référence communes sur tous les locataires dans une application. Travaux élastique peut également être utilisé toomaintain un *or* copie de base de données hello utilisée toocreate nouveaux clients, en vous assurant qu’il a toujours hello dernières référence de schéma et des données.

![Écran](media/sql-database-saas-tutorial-schema-management/schema-management.png)


## <a name="elastic-jobs-limited-preview"></a>Préversion limitée des travaux élastiques

Il existe une nouvelle version des travaux élastiques qui est désormais une fonctionnalité intégrée d’Azure SQL Database (qui ne nécessite pas de services ou de composants supplémentaires). Cette nouvelle version des travaux élastiques est pour le moment en préversion limitée. Actuellement, cette version d’évaluation limitée prend en charge les comptes de travail PowerShell toocreate et toocreate de T-SQL et gérer des tâches.

> [!NOTE]
> *Ce didacticiel utilise des fonctionnalités de hello service de base de données SQL qui se trouvent dans une version d’évaluation limitée (travaux de base de données élastique). Si vous souhaitez toodo de ce didacticiel, fournissez votre id d’abonnement tooSaaSFeedback@microsoft.com associé au sujet = élastique aperçu de travaux. Après avoir reçu la confirmation que votre abonnement a été activé, [télécharger et installer les applets de commande hello dernière version préliminaire travaux](https://github.com/jaredmoo/azure-powershell/releases). Cette version préliminaire est limitée. Contactez SaaSFeedback@microsoft.com pour toute question ou demande de prise en charge associées.*

## <a name="get-hello-wingtip-application-scripts"></a>Obtenir les scripts d’application hello Wingtip

Hello Wingtip SaaS scripts et code source d’applications sont disponibles dans hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) référentiel github. [Étapes de scripts de Wingtip SaaS hello toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="create-a-job-account-database-and-new-job-account"></a>Créer une base de données de compte de travail et un compte de travail

Ce didacticiel nécessite que vous utilisez PowerShell toocreate hello travail de base de données et le travail de compte. Comme MSDB et l’Agent SQL, les travaux élastique utilise SQL Azure base de données toostore les définitions de travail, état du travail et l’historique. Une fois que le compte de travail hello est créé, vous pouvez créer et surveiller les travaux immédiatement.

1. Ouvrir... \\Modules d’apprentissage\\gestion du schéma\\*SchemaManagement.ps1 de démonstration* Bonjour **PowerShell ISE**.
1. Appuyez sur **F5** script de hello toorun.

Hello *SchemaManagement.ps1 de démonstration* script appelle hello *déployer-SchemaManagement.ps1* toocreate de script un *S2* base de données nommée **jobaccount** sur le serveur de catalogue hello. Il crée ensuite le compte de travail hello, en passant de la base de données jobaccount hello comme un appel de création de compte de travail paramètre toohello.

## <a name="create-a-job-toodeploy-new-reference-data-tooall-tenants"></a>Créer un travail de toodeploy nouveaux référence données tooall clients

Chaque base de données client inclut un ensemble de types lieu qui définissent le type hello d’événements qui sont hébergés au niveau d’un lieu. Dans cet exercice, vous déployez un types lieu supplémentaires de mise à jour tooall hello client bases de données tooadd deux : *Moto course* et *natation Club*. Ces types de lieu correspondent image d’arrière-plan toohello que vous voyez dans l’application d’événements hello client.

Cliquez sur hello lieu Type menu déroulant et valider que des options de type lieu seulement 10 sont disponibles, et plus précisément que 'Moto course' et 'Natation Club' ne figurent pas dans la liste de hello.

Maintenant nous allons créer un Bonjour tooupdate de travail *VenueTypes* table dans toutes les bases de données de client hello et ajouter de nouveaux types de salle hello.

toocreate une nouvelle tâche, nous utilisons un ensemble de tâches créées dans la base de données jobaccount hello lors de la création de compte de travail hello des procédures stockées système.

1. Ouvrez SSMS et connecter le serveur de catalogue toohello : catalogue -\<utilisateur\>. database.windows.net server
1. Également connecter toohello client serveur : tenants1 -\<utilisateur\>. database.windows.net
1. Parcourir toohello *contosoconcerthall* base de données sur hello *tenants1* serveur et requête hello *VenueTypes* tooconfirm de table qui *Moto course*  et *natation Club* **ne sont pas** dans la liste des résultats hello.
1. Fichier ouvert hello... \\Modules d’apprentissage\\gestion du schéma\\DeployReferenceData.sql
1. Modifier l’instruction de hello : définissez @wtpUser = &lt;utilisateur&gt; et le remplacer par une valeur utilisateur hello utilisée lorsque vous avez déployé l’application de Wingtip hello
1. Assurez-vous que vous êtes connecté toohello jobaccount base de données, puis appuyez sur **F5** pour exécuter le script de hello

* **SP\_ajouter\_cible\_groupe** crée le nom du groupe cible hello DemoServerGroup, maintenant nous avons besoin de membres de cibles tooadd.
* **SP\_ajouter\_cible\_groupe\_membre** ajoute un *server* cibler un type de membre qui juge toutes les bases de données dans le serveur (Notez il s’agit de hello tenants1-&lt; Utilisateur&gt; serveur contenant les bases de données clientes hello) au moment du travail de l’exécution doit être incluse dans la tâche de hello, hello deuxième consiste à ajouter un *base de données* cibler un type de membre, en particulier hello () 'or' de la base de données basetenantdb) qui réside sur le catalogue -&lt;utilisateur&gt; server et enfin une autre *base de données* groupe membre type tooinclude hello adhocanalytics base de données cible qui est utilisé dans un prochain didacticiel.
* **sp\_add\_job** crée une tâche appelée « Reference Data Deployment » (Déploiement des données de référence).
* **SP\_ajouter\_jobstep** crée l’étape de travail hello contenant T-SQL commande texte tooupdate hello table de référence, VenueTypes
* vues restantes de Hello dans le script de hello affichent existence hello d’objets de hello et de surveiller l’exécution du travail. Utilisez ces valeur d’état requêtes tooreview hello Bonjour **cycle de vie** toodetermine colonne lors de la tâche de hello terminée avec succès sur toutes les bases de données client et les bases de données supplémentaires hello deux contenant la table de référence hello.

1. Dans SSMS, recherchez toohello *contosoconcerthall* base de données sur hello *tenants1* serveur et requête hello *VenueTypes* tooconfirm de table qui *Moto Course* et *natation Club* **sont** maintenant dans la liste des résultats hello.


## <a name="create-a-job-toomanage-hello-reference-table-index"></a>Créer un index de table de référence de projet toomanage hello

Exercice précédent toohello similaire cet exercice crée un index de hello de toorebuild de travail sur la clé primaire de la table de référence hello, une opération de gestion de base de données par défaut un administrateur peut s’exécuter après un chargement de données volumineux dans une table.

Créer un travail à l’aide de hello même travaux « système » des procédures stockées.

1. Ouvrez SSMS et se connecter toohello catalogue -&lt;utilisateur&gt;. database.windows.net server
1. Fichier ouvert hello... \\Modules d’apprentissage\\gestion du schéma\\OnlineReindex.sql
1. Clic droit et sélectionnez connexion connect toohello catalogue -&lt;utilisateur&gt;. database.windows.net server, si vous êtes pas déjà connecté
1. Vérifiez que vous sont la base de données connectée toohello jobaccount, appuyez sur le script de hello toorun F5

* sp\_add\_job crée un travail appelé « Online Reindex PK\_\_VenueTyp\_\_265E44FD7FD4C885 ».
* SP\_ajouter\_jobstep crée l’étape de travail hello contenant l’index de T-SQL commande texte tooupdate hello




## <a name="next-steps"></a>Étapes suivantes

Dans ce tutoriel, vous avez appris à effectuer les opérations suivantes :

> [!div class="checklist"]

> * Créer un tooquery de compte de travail sur plusieurs locataires
> * Mettre à jour les données dans toutes les bases de données de locataire
> * Créer un index sur une table dans toutes les bases de données de locataire

[Didacticiel sur les analyses ad hoc](sql-database-saas-tutorial-adhoc-analytics.md)


## <a name="additional-resources"></a>Ressources supplémentaires

* [D’autres didacticiels qui reposent sur hello déploiement d’application Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Gestion des bases de données cloud avec montée en charge](sql-database-elastic-jobs-overview.md)
* [Créer et gérer des bases de données cloud avec montée en charge](sql-database-elastic-jobs-create-and-manage.md)
