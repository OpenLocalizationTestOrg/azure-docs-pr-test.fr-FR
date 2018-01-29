---
title: "Gérer le schéma Azure SQL Database dans une application mutualisée | Microsoft Docs"
description: "Gérer un schéma pour plusieurs locataires dans une application mutualisée qui utilise Azure SQL Database"
keywords: "didacticiel sur les bases de données SQL"
services: sql-database
documentationcenter: 
author: MightyPen
manager: craigg
editor: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: Inactive
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/03/2018
ms.reviewers: billgib
ms.author: genemi
ms.openlocfilehash: 135764a7d89dcf711ff7fe9416850f1af9329479
ms.sourcegitcommit: df4ddc55b42b593f165d56531f591fdb1e689686
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/04/2018
---
# <a name="manage-schema-for-multiple-tenants-in-a-multi-tenant-application-that-uses-azure-sql-database"></a>Gérer un schéma pour plusieurs locataires dans une application mutualisée qui utilise Azure SQL Database

Ce didacticiel examine les défis liés à la gestion d’un parc potentiellement massif de bases de données dans une application SaaS (Software as a Service) dans le cloud. Des solutions sont illustrées pour gérer les améliorations de schéma qui sont développées et implémentées pendant la durée de vie d’une application.

Lors de l’évolution de n’importe quelle application, des modifications peuvent se produire dans ses colonnes de table ou autre schéma, dans ses données de référence ou les éléments liés aux performances. Avec une application SaaS, ces modifications doivent être déployées de façon coordonnée entre plusieurs bases de données de locataire existantes. Et ces modifications doivent être incluses dans les bases de données de locataire futures qui seront ajoutées à l’application. Par conséquent, les modifications doivent également être incorporées dans le processus qui provisionne les nouvelles bases de données.

#### <a name="two-scenarios"></a>Deux scénarios

Ce didacticiel explore les deux scénarios suivants :
- Déployer des mises à jour des données de référence pour tous les locataires.
- Retourner un index sur la table qui contient les données de référence.

La fonctionnalité [Tâches élastiques](sql-database-elastic-jobs-overview.md) d’Azure SQL Database est utilisée pour exécuter ces opérations sur les bases de données de locataire. Les tâches fonctionnent également sur le modèle final de la base de données de locataire. Ce modèle est utilisé lors du provisionnement des nouvelles bases de données.

Ce didacticiel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Créer un compte de travail.
> * Interroger plusieurs locataires.
> * Mettre à jour les données dans toutes les bases de données de locataire.
> * Créer un index sur une table dans toutes les bases de données de locataire.

## <a name="prerequisites"></a>Conditions préalables

- L’application Wingtip Tickets doit déjà être déployée :
    - Pour obtenir des instructions, consultez le premier didacticiel qui présente l’application de base de données mutualisée SaaS *Wingtip Tickets* :<br />[Déployer et explorer une application mutualisée partitionnée qui utilise Azure SQL Database](saas-multitenantdb-get-started-deploy.md).
        - Le processus de déploiement dure moins de cinq minutes.
    - Vous devez avoir la version *mutualisée partitionnée* de Wingtip installée. Les versions *Autonome* et *Base de données par locataire* ne prennent pas en charge ce didacticiel.

- La dernière version de SQL Server Management Studio (SSMS) doit être installée. [Téléchargez et installez SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

- Azure PowerShell doit être installé. Pour plus d’informations, consultez [Prise en main d’Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).

> [!NOTE]
> Ce didacticiel utilise des fonctionnalités du service Azure SQL Database en préversion limitée ([tâches de base de données élastiques](sql-database-elastic-database-client-library.md)). Si vous souhaitez réaliser ce didacticiel, envoyez votre ID d’abonnement à *SaaSFeedback@microsoft.com* avec l’objet Préversion des tâches élastiques. Une fois que vous avez reçu la confirmation que votre abonnement a été activé, [téléchargez et installez les dernières applets de commande pour les travaux en version préliminaire](https://github.com/jaredmoo/azure-powershell/releases). Cette préversion est limitée. Contactez *SaaSFeedback@microsoft.com* pour toute question ou demande de prise en charge associée.

## <a name="introduction-to-saas-schema-management-patterns"></a>Présentation des modèles de gestion de schéma SaaS

Le modèle de base de données partitionnée mutualisée utilisé dans cet exemple permet à une base de données de locataire de contenir un ou plusieurs locataires. Cet exemple présente la possibilité d’utiliser une combinaison de bases de données mutualisées et à locataire unique, créant ainsi un modèle de gestion de locataire *hybride*. La gestion de ces bases de données est complexe. Les [travaux élastiques](sql-database-elastic-jobs-overview.md) facilitent l’administration et la gestion de la couche de données SQL. Les tâches vous permettent d’exécuter de façon sécurisée et fiable des scripts Transact-SQL en tant que tâches, sur un groupe de bases de données de locataire. Les tâches sont indépendants de la saisie ou de l’interaction utilisateur. Cette méthode peut être utilisée pour déployer les modifications de schéma ou de données de référence commune sur tous les locataires d’une application. Les Tâches élastiques permettent également de conserver une copie du modèle finale de la base de données. Le modèle est utilisé pour créer de nouveaux locataires, afin de s’assurer que le schéma et les données de référence les plus récents sont utilisés.

![Écran](media/saas-multitenantdb-schema-management/schema-management.png)

## <a name="elastic-jobs-limited-preview"></a>Préversion limitée des travaux élastiques

Il existe une nouvelle version des travaux élastiques qui est désormais une fonctionnalité intégrée d’Azure SQL Database. Par « intégrée », nous entendons qu’elle ne nécessite aucun service ni composant supplémentaire. Cette nouvelle version des travaux élastiques est pour le moment en préversion limitée. La préversion limitée prend actuellement en charge PowerShell pour créer des comptes de travail et T-SQL pour créer et gérer des tâches.

## <a name="get-the-wingtip-tickets-saas-multi-tenant-database-application-source-code-and-scripts"></a>Obtenir les scripts et le code source de l’application de base de données multi-locataire SaaS Wingtip Tickets

Les scripts de base de données Wingtip Tickets SaaS mutualisée et le code source de l’application sont disponibles dans le référentiel [WingtipTicketsSaaS-MultiTenantDB](https://github.com/microsoft/WingtipTicketsSaaS-MultiTenantDB) sur GitHub. Consultez les [conseils généraux](saas-tenancy-wingtip-app-guidance-tips.md) avant de télécharger et de débloquer les scripts Wingtip Tickets SaaS. 

## <a name="create-a-job-account-database-and-new-job-account"></a>Créer une base de données de compte de travail et un compte de travail

Ce didacticiel nécessite l’utilisation de PowerShell pour créer la base de données de compte de travail et le compte de travail. Comme la base de données MSDB utilisée par SQL Agent, les Tâches élastiques s’appuient sur une base de données SQL Azure pour stocker les définitions, l’état et l’historique des tâches. Une fois le compte de travail créé, vous pouvez immédiatement créer et surveiller des tâches.

1. Dans **PowerShell ISE**, ouvrez *...\\Learning Modules\\Schema Management\\Demo-SchemaManagement.ps1*.
2. Appuyez sur **F5** pour exécuter le script.

Le script *Demo-SchemaManagement.ps1* appelle le script *Deploy-SchemaManagement.ps1* pour créer une base de données *S2* nommée **jobaccount** sur le serveur de catalogue. Le script crée ensuite le compte de travail en transmettant la base de données jobaccount en tant que paramètre à l’appel de création du compte de travail.

## <a name="create-a-job-to-deploy-new-reference-data-to-all-tenants"></a>Créer un travail pour déployer les nouvelles données de référence sur tous les locataires

#### <a name="prepare"></a>Préparation

Chaque base de données de locataire comprend un ensemble de types de lieux dans la table **VenueTypes**. Les types de lieux définissent le type d’événements qui se déroulent dans un lieu. Dans cet exercice, vous allez déployer une mise à jour dans toutes les bases de données afin d’ajouter deux types de lieux supplémentaires : *Motorcycle Racing* (Courses de moto) et *Swimming Club* (Club de natation). Ces types de lieux correspondent à l’image d’arrière-plan visible dans l’application que s’affiche dans l’application Events.

Avant de déployer les nouvelles données de référence, notez le nombre de types de lieux qui existent déjà, et qui peut être égal à 10. Prenez note en cliquant sur le lien suivant menant à l’interface utilisateur web de Wingtip, puis en cliquant sur le menu déroulant **Type de lieu** :
- http://events.wingtip-mt.<USER>.trafficmanager.net

Vous pouvez maintenant compter le nombre de types de lieux d’origine. Notez, en particulier, que *Motorcycle Racing* et *Swimming Club* n’existent pas encore.

#### <a name="steps"></a>Étapes

Maintenant, vous créez une tâche pour mettre à jour la table **VenueTypes** dans chaque base de données de locataire en ajoutant les deux nouveaux types de lieux.

Pour créer une tâche, vous utilisez l’ensemble de procédures stockées système dédiées aux tâches créées dans la base de données *jobaccount*. Les procédures ont été créées lorsque le compte de travail a été créé.

1. Dans SSMS, connectez-vous également au serveur de locataire tenants1-mt-\<user\>.database.windows.net

2. Accédez à la base de données *tenants1* sur le serveur *tenants1-mt-\<user\>.database.windows.net*.

3. Interrogez la table *VenueTypes* pour confirmer que *Motorcycle Racing* et *Swimming Club* ne sont pas encore dans la liste des résultats.

4. Connectez-vous au serveur de catalogue *catalog-mt-\<user\>.database.windows.net*.

5. Connectez-vous à la base de données *jobaccount* dans le serveur de catalogue.

6. Dans SSMS, ouvrez le fichier *...\\Learning Modules\\Schema Management\\DeployReferenceData.sql*.

7. Modifiez l’instruction : set @User = &lt;utilisateur&gt; et remplacer la valeur de l’utilisateur utilisée lors du déploiement de l’application de base de données Wingtip Tickets SaaS mutualisée.

8. Appuyez sur **F5** pour exécuter le script.

#### <a name="observe"></a>Observer

Observez les éléments suivants dans le script *DeployReferenceData.sql* :

- **sp\_add\_target\_group** crée le nom de groupe cible *DemoServerGroup* et ajoute des membres cibles au groupe.

- **sp\_add\_target\_group\_member** ajoute les éléments suivants :
    - Un type de membre cible *serveur*.
        - Il s’agit du serveur *tenants1-mt-&lt;user&gt;* qui contient les bases de données de locataire.
        - Par conséquent, toutes les bases de données sur le serveur sont incluses dans la tâche lorsqu’elle s’exécute.
    - Un type de membre cible *base de données* pour la base de données finale (*basetenantdb*) qui réside sur le serveur *catalog-mt-&lt;user&gt;*.
    - Un type de membre cible *base de données* pour inclure la base de données *adhocreporting* utilisée dans un autre didacticiel.

- **sp\_add\_job** crée une tâche appelée *Reference Data Deployment* (Déploiement des données de référence).

- **sp\_add\_jobstep** crée l’étape du travail contenant le texte de la commande T-SQL pour mettre à jour la table de référence, VenueTypes.

- Les autres vues dans le script indiquent l’existence des objets et contrôlent l’exécution du travail. Utilisez ces requêtes pour passer en revue la valeur d’état dans la colonne **cycle de vie** afin de déterminer le moment où la tâche a été terminée. La tâche met à jour la base de données de locataire et met à jour les deux bases de données supplémentaires contenant la table de référence.

Dans SSMS, accédez à la base de données de locataire sur le serveur *tenants1-mt -&lt;user&gt;*. Interrogez la table *VenueTypes* pour confirmer que *Motorcycle Racing* et *Swimming Club* sont désormais dans la liste des résultats. Le nombre total de types de lieux doit avoir augmenté par deux unités.

## <a name="create-a-job-to-manage-the-reference-table-index"></a>Créer une tâche pour gérer l’index de la table de référence

Cet exercice est similaire à l’exercice précédent. Cet exercice crée une tâche pour reconstruire l’index sur la clé primaire de la table de référence. Une reconstruction d’index est une opération de gestion de base de données qu’un administrateur peut exécuter après le chargement de données volumineuses dans une table, afin d’améliorer les performances.

1. Dans SSMS, connectez-vous à la base de données *jobaccount* sur le serveur *catalog-mt-&lt;User&gt;.database.windows.net*.

2. Dans SSMS, ouvrez *...\\Learning Modules\\Schema Management\\OnlineReindex.sql*.

3. Appuyez sur **F5** pour exécuter le script.

#### <a name="observe"></a>Observer

Observez les éléments suivants dans le script *OnlineReindex.sql* :

* **sp\_add\_job** crée une tâche nommée *Online Reindex PK\_\_VenueTyp\_\_265E44FD7FD4C885*.

* **sp\_add\_jobstep** crée l’étape du travail contenant le texte de la commande T-SQL pour mettre à jour l’index.

* Les vues restantes dans le script surveillent l’exécution du travail. Utilisez ces requêtes pour passer en revue la valeur d’état dans la colonne **cycle de vie** afin de déterminer le moment où la tâche a été terminée avec succès sur tous les membres du groupe cible.

## <a name="additional-resources"></a>Ressources supplémentaires

<!-- TODO: Additional tutorials that build upon the Wingtip Tickets SaaS Multi-tenant Database application deployment (*Tutorial link to come*)
(saas-multitenantdb-wingtip-app-overview.md#sql-database-wingtip-saas-tutorials)
-->
* [Gestion des bases de données cloud avec montée en charge](sql-database-elastic-jobs-overview.md)
* [Créer et gérer des bases de données cloud avec montée en charge](sql-database-elastic-jobs-create-and-manage.md)

## <a name="next-steps"></a>étapes suivantes

Dans ce tutoriel, vous avez appris à effectuer les opérations suivantes :

> [!div class="checklist"]
> - Créer un compte de travail pour interroger plusieurs locataires.
> - Mettre à jour les données dans toutes les bases de données de locataire.
> - Créer un index sur une table dans toutes les bases de données de locataire.

Suivez maintenant le [didacticiel de génération de rapports ad-hoc](saas-multitenantdb-adhoc-reporting.md).

