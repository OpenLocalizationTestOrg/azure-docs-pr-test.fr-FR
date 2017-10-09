---
title: "requêtes d’analytique ad-hoc aaaRun entre plusieurs bases de données SQL Azure | Documents Microsoft"
description: "Exécuter des requêtes ad-hoc analytique sur plusieurs bases de données SQL dans l’application de hello Wingtip SaaS mutualisée."
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
ms.date: 06/23/2017
ms.author: billgib; sstein
ms.openlocfilehash: 140cd51fdd03b5a548147282b51ceb0ad80c944d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-ad-hoc-analytics-queries-across-all-wingtip-saas-tenants"></a>Exécuter des requêtes d’analyse ad hoc sur tous les SaaS Wingtip

Dans ce didacticiel, vous exécutez des requêtes distribuées sur l’ensemble de hello de bases de données clientes tooenable ad-hoc analytique. Requête élastique est utilisé tooenable distribué requêtes, ce qui nécessite une base de données analytique supplémentaires est déployé (serveur de catalogue toohello). Ces requêtes peuvent extraire des informations utiles dans les données opérationnelles de hello quotidiennes d’application de Wingtip SaaS hello.


Ce didacticiel vous apprend à effectuer les opérations suivantes :

> [!div class="checklist"]

> * À propos des affichages globaux de hello dans chaque base de données, qui permettent l’interrogation efficace sur les clients
> * Comment toodeploy une base de données analytique ad hoc
> * Comment toorun les requêtes distribuées sur toutes les bases de données client



toocomplete ce didacticiel, assurez-vous que hello est suivant des conditions préalables requises sont effectuées :

* Hello Wingtip SaaS application est déployée. toodeploy en moins de cinq minutes, consultez [déployer et Explorer hello Wingtip SaaS application](sql-database-saas-tutorial.md)
* Azure PowerShell est installé. Pour plus d’informations, consultez [Bien démarrer avec Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).
* SQL Server Management Studio (SSMS) est installé. toodownload et installez SSMS, consultez [télécharger SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).


## <a name="ad-hoc-analytics-pattern"></a>Modèle d’analyse ad hoc

Une des opportunités de hello avec les applications SaaS est toouse hello grande quantité de données client stockées de manière centralisée dans le cloud de hello. Utilisez cette insights toogain de données dans l’opération de hello et de l’utilisation de votre application, vos clients, leurs utilisateurs, les préférences, comportements, etc.. Ces analyses peuvent guider le développement des fonctionnalités, les améliorations de convivialité et les autres investissements dans vos applications et services.

L’accès à ces données dans une base de données mutualisée est facile, mais pas si simple lors d’une distribution à grande échelle sur des milliers de bases de données. Une approche consiste à toouse [requête élastique](sql-database-elastic-query-overview.md), ce qui permet l’interrogation sur un ensemble distribué de bases de données avec un schéma commun. Requête élastique utilise un seul *head* base de données dans lequel les tables externes sont définies que les tables de mise en miroir ou des vues dans hello distribué bases de données (client). Les requêtes envoyées toothis principal de base de données est compilée tooproduce un plan de requête distribuée, avec des parties de requête hello poussée vers le bas toohello bases de données client en fonction des besoins. Requête élastique utilise la carte de partitions hello dans emplacement du hello tooprovide hello catalogue de base de données de bases de données clientes hello. La configuration et les requêtes sont simples grâce à l’utilisation de [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference) standard, et les requêtes ad hoc sont compatibles avec des outils tels que Power BI et Excel.

En répartissant les requêtes sur les bases de données clientes hello, requête élastique fournit l’idée immédiate des données de production. Toutefois, comme élastique requête extrait des données potentiellement de nombreuses bases de données, latence peut parfois être supérieure à celle des requêtes équivalentes de requête soumise tooa unique base de données. Soyez vigilant lors de la conception interroge les données de hello toominimize qui sont retournées. Requête élastique souvent convient pour l’interrogation de petites quantités de données en temps réel, rapports ou des requêtes complexes analytique ou opposition toobuilding fréquemment utilisés. Si les requêtes ne fonctionne bien, regardez hello [plan d’exécution](https://docs.microsoft.com/sql/relational-databases/performance/display-an-actual-execution-plan) toosee quelle partie de la requête de hello ont été envoyée vers le bas de la base de données distante toohello et la quantité de données est retournée. Les requêtes nécessitant un traitement d’analyse complexe renvoient parfois de meilleurs résultats si les données client sont extraites dans une base de données dédiée ou un entrepôt de données optimisé pour les requêtes d’analyse. Ce modèle est expliqué dans hello [didacticiel d’analytique locataire](sql-database-saas-tutorial-tenant-analytics.md). 

## <a name="get-hello-wingtip-application-scripts"></a>Obtenir les scripts d’application hello Wingtip

Hello Wingtip SaaS scripts et code source d’applications sont disponibles dans hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) référentiel github. [Étapes de scripts de Wingtip SaaS hello toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="create-ticket-sales-data"></a>Créer des données sur des ventes de tickets

toorun de requêtes sur un jeu de données plus intéressant, de créer des données de ventes de ticket en exécutant le Générateur de ticket hello.

1. Bonjour *PowerShell ISE*, ouvrez hello... \\Modules d’apprentissage\\Analytique opérationnelle\\ad hoc Analytique\\*AdhocAnalytics.ps1 de démonstration* de script et définir hello valeurs suivantes :
   * **$DemoScenario** = 1, **Acheter des tickets pour des événements dans tous les lieux**.
2. Appuyez sur **F5** pour exécuter le script de hello et générer des ventes de ticket. Lors de l’exécution du script hello, continuez les étapes de hello dans ce didacticiel. interrogation des données de ticket Hello Bonjour *exécuter des requêtes distribuée ad hoc* section, par conséquent, attendez hello ticket générateur toocomplete si elle est en cours d’exécution lorsque vous obtenez toothat exercice.

## <a name="explore-hello-global-views"></a>Explorer les affichages globaux hello

Hello application Wingtip SaaS est construit à l’aide d’un modèle client-base de données, schéma de base de données client hello est défini à partir d’un point de vue du locataire unique. Les informations propres au client existent dans une table nommée *Venue*, qui comporte une seule ligne et qui apparaît sous forme de segment de mémoire sans clé primaire. Autres tables dans le schéma de hello n’est pas nécessaire toobe lié toohello *lieu* de table, car en usage normal, il n’est jamais un doute sur les données de hello du client appartient à.

Toutefois, lors de l’interrogation sur toutes les bases de données, il est important que requête élastique peut traiter les données de salutation comme s’il fait partie d’une seule base de données logique partitionnée par le client. tooachieve cela, un ensemble de vues 'globales' sont ajouté toohello client base de données de projet un id de client dans chacune des tables de hello sont interrogées globalement. Par exemple, hello *VenueEvents* vue ajoute un calculée *VenueId* toohello colonnes projetées de hello *événements* table. En définissant la table externe de hello dans la base de données principal hello sur *VenueEvents* (au lieu de hello sous-jacent *événements* table), requête élastique est en mesure de toopush vers le bas des jointures basées sur *VenueId* afin qu’ils peuvent être exécutés en parallèle sur chaque base de données distante (et non sur la base de données principal hello). Cela réduit considérablement la quantité de hello de données qui sont retournées, ce qui entraîne une augmentation importante des performances pour de nombreuses requêtes. Ces vues globales ont été créées au préalable dans toutes les bases de données client (et dans *basetenantdb*).

1. Ouvrez SSMS et [connecter toohello tenants1 -&lt;utilisateur&gt; server](sql-database-wtp-overview.md#explore-database-schema-and-execute-sql-queries-using-ssms).
2. Développez **Bases de données**, cliquez avec le bouton droit sur **contosoconcerthall**, puis sélectionnez **Nouvelle requête**.
3. Exécutez hello suivant la différence de hello tooexplore requêtes entre les tables de locataire unique de hello et les affichages globaux hello :

   ```T-SQL
   -- hello base Venue table, that has no VenueId associated.
   SELECT * FROM Venue

   -- Notice hello plural name 'Venues'. This view projects a VenueId column.
   SELECT * FROM Venues

   -- hello base Events table, which has no VenueId column.
   SELECT * FROM Events

   -- This view projects hello VenueId retrieved from hello Venues table.
   SELECT * FROM VenueEvents
   ```

Dans ces modes, hello *VenueId* est calculée comme un hachage du nom de salle hello, mais une approche peut être utilisé toointroduce une valeur unique. Cette approche est toohello comme clé de locataire hello est calculée pour une utilisation dans le catalogue de hello.

définition de hello tooexamine Hello *lieux* vue :

1. Dans **Explorateur d’objets**, développez **contosoconcethall** > **Vues** :

   ![vues](media/sql-database-saas-tutorial-adhoc-analytics/views.png)

2. Cliquez avec le bouton droit sur **dbo.Venues**.
3. Sélectionnez **Générer un script de la vue en tant que** > **CRÉER vers** > **Nouvelle fenêtre d’éditeur de requête**

Générer un script des hello autres *lieu* vues toosee comment ils ajoutent hello *VenueId*.

## <a name="deploy-hello-database-used-for-ad-hoc-distributed-queries"></a>Déployer hello de base de données utilisé pour les requêtes distribuée ad hoc

Cet exercice déploie hello *adhocanalytics* base de données. Il s’agit de hello principal base de données qui contiendra le schéma hello utilisé pour l’interrogation de toutes les bases de données client. base de données Hello est déployé toohello existante du serveur de catalogue, qui est utilisé pour tous les liées à la gestion de bases de données dans l’exemple d’application hello hello le serveur.

1. Ouvrir... \\Modules d’apprentissage\\Analytique opérationnelle\\ad hoc Analytique\\*AdhocAnalytics.ps1 de démonstration* Bonjour *PowerShell ISE* et ensemble hello valeurs suivantes :
   * **$DemoScenario** = 2, **Déployer la base de données d’analyse ad hoc**.

2. Appuyez sur **F5** toorun hello script et créer hello *adhocanalytics* base de données.

Dans la section suivante de hello, vous ajoutez de base de données de schéma toohello afin qu’il peut être utilisé toorun distribué requêtes.

## <a name="configure-hello-database-for-running-distributed-queries"></a>Configurer hello de base de données pour l’exécution de requêtes distribuées

Cet exercice ajoute le schéma (source de données externe hello et définitions de table externe) toohello ad-hoc analytique de base de données qui permet l’interrogation de toutes les bases de données client.

1. Ouvrez SQL Server Management Studio et connectez-vous toohello créé à l’étape précédente de hello de la base de données ad hoc Analytique. nom Hello de base de données hello sera adhocanalytics.
2. Ouvrez ...\Modules d’apprentissage\Operational Analytics\Adhoc Analytics\ *Initialize-AdhocAnalyticsDB.sql* dans SSMS.
3. Passez en revue le script SQL de hello et notez hello suivantes :

   Élastique la requête utilise un tooaccess étendue de base de données d’informations d’identification chaque des bases de données client hello. Ces informations d’identification doit toobe disponible dans toutes les bases de données hello et doivent normalement être accordée minimales hello requis tooenable ces requêtes ad-hoc.

    ![créer des informations d’identification](media/sql-database-saas-tutorial-adhoc-analytics/create-credential.png)

   Hello source de données externe, qui est définie par carte de partitions toouse hello client dans la base de données de catalogue hello. Utilisez cette option en tant que source de données externe hello, les requêtes sont tooall distribuées de bases de données enregistrés dans le catalogue de hello lors de l’exécution de requête de hello. Étant donné que les noms de serveur sont différentes pour chaque déploiement, ce script d’initialisation obtient emplacement hello de base de données de catalogue hello en récupérant le serveur en cours de hello (@@servername) où le script de hello est exécutée.

    ![créer une source de données externe](media/sql-database-saas-tutorial-adhoc-analytics/create-external-data-source.png)

   Hello des tables externes qui référencent des affichages globaux de hello décrites dans la section précédente de hello et défini avec **DISTRIBUTION = SHARDED(VenueId)**. Étant donné que chaque *VenueId* mappe tooa de base de données unique, cela améliore les performances pour de nombreux scénarios comme indiqué dans la section suivante de hello.

    ![créer des tables externes](media/sql-database-saas-tutorial-adhoc-analytics/external-tables.png)

   table locale de Hello *VenueTypes* qui est créé et rempli. Cette table de données de référence étant courante dans toutes les bases de données client, il peut être représenté ici comme une table locale et remplis avec des données communes hello. Pour certaines requêtes, cela peut réduire hello quantité de données déplacées entre les bases de données clientes hello et hello *adhocanalytics* base de données.

    ![créer une table](media/sql-database-saas-tutorial-adhoc-analytics/create-table.png)

   Si vous incluez des tables de référence de cette manière, être sûr de schéma de table tooupdate hello et les données chaque fois que vous mettez à jour les bases de données clientes hello.

4. Appuyez sur **F5** toorun hello script et d’initialiser hello *adhocanalytics* base de données. 

Vous pouvez à présent exécuter des requêtes distribuées et collecter des informations sur l’ensemble des clients !

## <a name="run-ad-hoc-distributed-queries"></a>Exécuter des requêtes distribuées ad hoc

Maintenant que hello *adhocanalytics* base de données est configurée, continuez et exécuter des requêtes distribuées. Inclure le plan d’exécution hello pour mieux comprendre le fonctionnement d’où le traitement des requêtes hello se produit. 

Lors de l’inspection de plan d’exécution de hello, pointez sur les icônes du plan hello pour plus d’informations. 

Toonote important, est le paramètre **DISTRIBUTION = SHARDED(VenueId)** quand nous avons défini la source de données externe hello, améliore les performances pour de nombreux scénarios. Étant donné que chaque *VenueId* mappe tooa base de données unique, le filtrage est données facilement effectué à distance, qui retourne hello uniquement.

1. Ouvrir... \\Modules d’apprentissage\\Operational Analytics\\Adhoc Analytics\\*Demo-AdhocAnalyticsQueries.sql* dans SSMS.
2. Assurez-vous que vous êtes connecté toohello **adhocanalytics** base de données.
3. Sélectionnez hello **requête** menu et cliquez sur **inclure le Plan d’exécution réel**
4. Mettez en surbrillance hello *les lieux actuellement inscrits ?* requête, puis appuyez sur **F5**.

   requête de Hello renvoie la liste entière lieu hello, illustrant comment rapide et il est facile de tooquery sur tous les locataires et retourner des données de chaque client.

   Inspecter le plan de hello et que la totalité des coûts hello est requête distante de hello, car nous sommes simplement continu tooeach base de données client et en sélectionnant des informations de lieu hello.

   ![SELECT * FROM dbo.Venues](media/sql-database-saas-tutorial-adhoc-analytics/query1-plan.png)

5. Les requêtes suivant hello sélectionnez, puis appuyez sur **F5**.

   Cette requête joint les données de bases de données clientes hello et hello local *VenueTypes* table (locale, tel qu’il est une table dans hello *adhocanalytics* base de données).

   Inspecter le plan de hello et voir ce hello majorité des coûts est la requête distante de hello, car nous interroger les informations de lieu de chaque client (dbo. Salles), puis effectuez une jointure locale rapide avec hello local *VenueTypes* nom convivial de table toodisplay hello.

   ![Joindre des données locales et distantes](media/sql-database-saas-tutorial-adhoc-analytics/query2-plan.png)

6. Sélectionnez à présent hello *jour ont été hello la plupart des tickets vendues ?* requête, puis appuyez sur **F5**.

   Cette requête effectue une opération de jointure et d’agrégation un peu plus complexe. Toonote important est que la plupart du traitement de hello est effectuée à distance, et une fois encore, nous récupérer uniquement les lignes hello que nous avons besoin, retourner une seule ligne pour le nombre de vente de chaque salle ticket d’agrégation par jour.

   ![query](media/sql-database-saas-tutorial-adhoc-analytics/query3-plan.png)


## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris à effectuer les opérations suivantes :

> [!div class="checklist"]

> * Exécuter des requêtes distribuées sur toutes les bases de données client
> * Déployer une base de données analytique ad hoc et ajouter des requêtes de schéma tooit toorun distribué.


Essayez maintenant hello [didacticiel du locataire Analytique](sql-database-saas-tutorial-tenant-analytics.md) tooexplore extraction tooa analytique distincts de données pour un traitement plus complexe analytique...

## <a name="additional-resources"></a>Ressources supplémentaires

* Supplémentaires [didacticiels qui reposent sur hello application Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Requête élastique](sql-database-elastic-query-overview.md)
