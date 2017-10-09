---
title: "aaaDiscover, identifier et classer les données personnelles dans Microsoft Azure | Documents Microsoft"
description: "En savoir plus sur la recherche, la classification, la découverte et l’identification de données"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: af4ced1c57699dc751d55cfdf3229c7d294648a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="discover-identify-and-classify-personal-data-in-microsoft-azure"></a>Découvrir, identifier et classer des données personnelles dans Microsoft Azure

Cet article fournit des conseils sur la façon dont toodiscover, identifier et classer les données personnelles dans plusieurs services, notamment l’utilisation d’Azure Data Catalog, Azure Active Directory, de la base de données SQL, Power Query pour les clusters Hadoop dans HDInsight Azure, Azure et les outils Azure Protection des informations, Azure Search et les requêtes SQL pour la base de données Azure Cosmos.

## <a name="scenario-problem-statement-and-goal"></a>Scénario, énoncé du problème et objectifs

Une société américaine d’articles de sport recueille diverses données de nature personnelle et autre. Il s’agit notamment de données sur les clients et les employés. société de Hello conserve dans plusieurs bases de données et le stocke dans plusieurs emplacements dans leur environnement Azure. En outre d’équipement de sport tooselling, elles hébergeront et gérer l’inscription pour les événements de sport privilégiées monde hello, y compris Bonjour Europe, également, et dans certains hello cas qu’elles recueillent les données client comprennent des informations médicales.

Étant donné que la société de hello héberge plusieurs présentations de bicycling internationales chaque année et a le personnel temporaire dans des emplacements du monde hello, deux jeux de données hello sont assez volumineux. société de Hello possède également des applications créé par le développeur qui sont utilisées par les clients et les employés.

société de Hello veut hello tooaddress les problèmes suivants :

- Données personnelles de clients et des employés doivent être classées/distinguent hello autre société hello de données collecte dans accès ordre tooensure et la sécurité.
- administrateur de données Hello doit tooeasily découvrir emplacement hello des données personnelles de clients dans différents domaines de hello environnement Azure.
- Données personnelles clients et des employés qui s’affiche dans les documents partagés et les communications par courrier électronique doit être intitulées toohelp vous assurer qu’il est conservé en lieu sûr.
- les développeurs d’applications d’entreprise Hello besoin d’une recherche de tooeasily moyen pour les clients et des employés des données personnelles dans leurs applications web et mobiles.
- Les développeurs doivent également tooquery leur base de données du document pour les données personnelles.

### <a name="company-goals"></a>Objectifs de la société

- Toutes les données personnelles des clients et des employés doivent être balisées/annotées dans Azure Data Catalog pour faciliter leur recherche. Dans l’idéal, les données personnelles des clients et des employés doivent être balisés/annotées séparément.
- Les données personnelles tirées des informations professionnelles et de profil utilisateur des clients et des employés résidant dans Azure Active Directory doivent pouvoir être localisées facilement.
- Les données personnelles résidant dans plusieurs bases de données SQL doivent pouvoir être interrogées facilement. 
- Certaines des grands jeux de données de la société hello sont gérés via Azure HDInsight et stockées dans Hadoop. Ils doivent être importés dans Excel pour pouvoir faire l’objet de requêtes relatives aux données personnelles.
- Les données personnelles partagées dans les documents et les e-mails doivent être classées, étiquetées et sécurisées avec Azure Information Protection.
- Hello les développeurs d’applications d’entreprise doivent être en mesure de toodiscover clients et des employés données personnelles dans les applications hello qu'ils créées, laquelle ils peuvent le faire avec Azure Search.
- Les développeurs doivent être en mesure de toofind des données personnelles dans leur base de données du document.

## <a name="azure-active-directory-data-discovery"></a>Azure Active Directory : découverte de données

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) est le service Microsoft de gestion d’annuaires et d’identités multilocataire basé sur le cloud. Vous pouvez localiser les profils utilisateur clients et des employés et les informations de travail utilisateur qui contiennent des données personnelles de votre [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) environnement (AAD) à l’aide de hello [portail Azure](https://portal.azure.com/).

Cela est particulièrement utile si vous souhaitez toofind ou modifiez des données personnelles pour un utilisateur spécifique. Vous pouvez aussi ajouter ou modifier des informations professionnelles et de profil utilisateur. Vous devez vous connecter avec un compte qui est un administrateur global pour le répertoire de hello.

### <a name="how-do-i-locate-or-view-user-profile-and-work-information"></a>Comment localiser ou afficher des informations professionnelles et de profil utilisateur ?

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.

2. Sélectionnez **davantage de services**, entrez **utilisateurs et groupes** dans hello de zone de texte, puis sélectionnez **entrée**.

   ![comment localiser des informations professionnelles et de profil utilisateur](media/how-to-discover-classify-personal-data-azure/user-profile.png)

3. Sur hello **utilisateurs et groupes** panneau, sélectionnez **utilisateurs**.

  ![Ouverture du panneau Utilisateurs et groupes](media/how-to-discover-classify-personal-data-azure/users-groups.png)

4. Sur hello **les utilisateurs et groupes d’utilisateurs -** panneau, sélectionnez un utilisateur à partir de la liste de hello, puis, dans Panneau de hello pour l’utilisateur sélectionné de hello, **profil** tooview les informations de profil utilisateur qui peuvent contenir des données personnelles .

  ![sélectionner un utilisateur](media/how-to-discover-classify-personal-data-azure/select-user.png)

5. Si vous avez besoin de tooadd ou modifiez les informations de profil utilisateur, vous pouvez le faire et puis, dans la barre de commandes hello, sélectionnez **enregistrer.**
6. Dans le panneau hello pour l’utilisateur sélectionné de hello, sélectionnez **Info de travail** tooview les informations de travail utilisateur qui contiennent des données personnelles.

 ![affichage d’informations professionnelles](media/how-to-discover-classify-personal-data-azure/work-info.png)

7. Si vous avez besoin de tooadd ou modifiez les informations de travail utilisateur, vous pouvez le faire et puis, dans la barre de commandes hello, sélectionnez **enregistrer.**

## <a name="azure-sql-database-data-discovery"></a>Azure SQL Database : découverte de données

[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) est une base de données cloud qui permet aux développeurs de créer et de tenir à jour des applications. Il est possible de rechercher des données personnelles dans [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) à l’aide de requêtes SQL standard. Requête élastique SQL Azure (aperçu) permet de requêtes de bases de données croisées tooperform les utilisateurs.

Détaillées [base de données SQL](../sql-database/sql-database-technical-overview.md) didacticiel explique les nombreux aspects de l’utilisation d’une base de données SQL, y compris la manière toobuild une et la manière dont les requêtes de données toorun. Hello Voici un résumé des informations de hello disponibles dans didacticiel hello avec sections toospecific de liens.

### <a name="how-do-i-build-a-sql-database"></a>Comment créer une base de données SQL ?

Il existe trois façons toodo il :

- Une base de données SQL Azure peut être créé dans hello [portail Azure](https://portal.azure.com/). Dans le didacticiel de hello, vous allez utiliser un ensemble spécifique de ressources de calcul et de stockage dans un groupe de ressources et le serveur logique. Vous allez utiliser les données d’exemple d’une société fictive appelée AdventureWorks. Par ailleurs, vous allez créer une règle de pare-feu au niveau du serveur. toolearn comment toodo, hello visite [créer une base de données SQL Azure Bonjour Azure portal](../sql-database/sql-database-get-started-portal.md) didacticiel.

  ![Créer une base de données Azure SQL Database](media/how-to-discover-classify-personal-data-azure/create-database.png)
- Une base de données SQL peut également être créé dans hello [Azure Cloud Shell](https://azure.microsoft.com/features/cloud-shell/) CLI, un outil de ligne de commande basée sur navigateur. outil de Hello est disponible dans hello portail Azure et peut être exécuté directement à partir de là. Dans ce didacticiel, vous lancez l’outil de hello, définissez les variables de script, créez un groupe de ressources et le serveur logique et configurez une règle de pare-feu du serveur. Vous créerez ensuite une base de données à partir de données d’exemple. toolearn comment toocreate votre base de données de cette manière, visitez hello [créer une seule base de données SQL Azure à l’aide de hello CLI d’Azure](../sql-database/sql-database-get-started-cli.md) didacticiel.

  ![Didacticiel CLI](media/how-to-discover-classify-personal-data-azure/cli-tutorial.png)

>[!NOTE]
Azure CLI est couramment utilisé par les administrateurs et les développeurs Linux. Certains utilisateurs trouvent cet outil plus simple et plus intuitif que PowerShell, qui constitue la troisième option.

- Enfin, vous pouvez créer une base de données SQL à l’aide de PowerShell, qui est un toocreate outil de ligne de commande/script et gérer Azure et autres ressources. Dans ce didacticiel, vous lancez l’outil de hello, définissez les variables de script, créez un groupe de ressources et le serveur logique et configurez une règle de pare-feu du serveur. Vous créerez ensuite une base de données à partir de données d’exemple.

didacticiel de Hello requiert hello Azure PowerShell version 4.0 ou version ultérieur du module. Exécutez Get-Module - ListAvailable AzureRM toofind votre version. Si vous avez besoin de tooinstall ou mise à niveau, consultez le module installer Azure PowerShell.

```PowerShell
New-AzureRmSQLDatabase -ResourceGroupName $resourcegroupname `
-ServerName $servername `
-DatabaseName $databasename `
-RequestedServiceObjectiveName "s0"
```

toolearn comment toocreate votre base de données de cette manière, visitez hello [créer une seule base de données SQL Azure à l’aide de Powershell](../sql-database/sql-database-get-started-powershell.md) didacticiel.

>[!Note]
Les administrateurs Windows ont tendance à toouse PowerShell, mais certains d'entre eux préfèrent CLI d’Azure.

### <a name="how-do-i-search-for-personal-data-in-sql-database-in-hello-azure-portal"></a>Comment pour rechercher des données personnelles dans la base de données SQL dans hello portail Azure ? **

Vous pouvez utiliser l’outil d’éditeur de requête intégrées hello à l’intérieur de hello toosearch portail Azure pour vos données personnelles. Vous allez ouvrir une session dans l’outil toohello à l’aide de votre compte de connexion SQL server admin et le mot de passe, puis entrez une requête.

  ![sql de recherche à l’aide du portail de hello](media/how-to-discover-classify-personal-data-azure/search-sql-portal.png)

Étape 5 du didacticiel de hello montre un exemple de requête dans le volet de l’éditeur de requête hello, mais il ne vous concentrer sur les informations personnelles ou sensibles (il également combine les données provenant de deux tables et crée les alias de colonne de source de hello dans le jeu de données hello qui est retourné). Hello capture d’écran suivante montre hello requête étape 5, ainsi que hello volet des résultats qui est retournée :

  ![query editor](media/how-to-discover-classify-personal-data-azure/query-editor.png)

Si votre base de données s’intitule MaTable, un exemple de requête portant sur des informations personnelles pourrait inclure le nom, le numéro de sécurité sociale et le numéro d’identification et ressembler à ceci :

“SELECT Nom, SSN, Numero_identification FROM MaTable”

Vous exécutez la requête de hello et puis afficher les résultats de hello en hello **résultats** volet.

Pour plus d’informations sur comment tooquery SQL de base de données Bonjour portail Azure, visitez hello [base de données SQL de requête hello](../sql-database/sql-database-get-started-portal.md) section du didacticiel de hello.

### <a name="how-do-i-search-for-data-across-multiple-databases"></a>Comment rechercher des données dans plusieurs bases de données ?

Requête élastique SQL (version préliminaire) permet de vous tooperform entre bases de données et de plusieurs requêtes de base de données et retourner un résultat unique. Hello [vue d’ensemble du didacticiel](../sql-database/sql-database-elastic-query-overview.md) inclut une description détaillée des scénarios et explique la différence de hello entre le partitionnement vertical et horizontal de la base de données. Le partitionnement horizontal est appelé « sharding ».

  ![Partitionnement vertical](media/how-to-discover-classify-personal-data-azure/vertical-partition.png)

  ![partitionnement horizontal](media/how-to-discover-classify-personal-data-azure/horizontal.png)

tooget démarré, visitez hello [vue d’ensemble requête élastique de base de données SQL Azure (aperçu)](../sql-database/sql-database-elastic-query-overview.md) page.

#### <a name="power-query-for-importing-azure-hdinsight-hadoop-clusters-data-discovery-for-large-data-sets"></a>Power Query (pour l’importation de clusters Hadoop Azure HDInsight) : découverte de données pour les jeux de données volumineux

Hadoop est un service de stockage et de traitement Apache open source conçu pour les jeux de données volumineux, qui sont analysés et stockés dans des clusters Hadoop. [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/) permet toowork utilisateurs avec Hadoop de clusters dans Azure. Power Query est un complément Excel qui permet notamment aux utilisateurs de découvrir des données issues de différentes sources.

Les données personnelles associées aux clusters Hadoop dans HDInsight de Azure peuvent être importé tooExcel avec Power Query. Une fois les données de salutation dans Excel, vous pouvez utiliser une requête tooidentify il.

#### <a name="how-do-i-use-excel-power-query-tooimport-hadoop-clusters-in-azure-hdinsight-into-excel"></a>Comment utiliser des clusters Hadoop de tooimport Excel Power Query dans Azure HDInsight dans Excel ?

Il existe un didacticiel HDInsight qui vous guidera tout au long de ce processus. Il explique les conditions préalables et inclut un lien de tooa [prise en main Azure HDInsight](../hdinsight/hdinsight-hadoop-linux-tutorial-get-started.md) didacticiel. Instructions couvrent Excel 2016, ainsi que 2013 et 2010 (les étapes sont légèrement différentes pour les versions antérieures de hello d’Excel). Si vous n’avez pas du complément Excel Power Query hello, hello didacticiel vous montre comment tooget il. Vous allez démarrer le didacticiel de hello dans Excel et que vous devrez toohave un compte de stockage d’objets Blob Azure associé à votre cluster.

  ![Interroger dans Excel](media/how-to-discover-classify-personal-data-azure/excel.png)

toolearn comment toodo, hello visite [tooHadoop Excel de se connecter à l’aide de Power Query](../hdinsight/hdinsight-connect-excel-power-query.md) didacticiel.

Source : [tooHadoop Excel de se connecter à l’aide de Power Query](../hdinsight/hdinsight-connect-excel-power-query.md)

## <a name="azure-information-protection-personal-data-classification-for-documents-and-email"></a>Azure Information Protection : classification des données personnelles pour les documents et les e-mails

[Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) peut aider les clients Azure s’appliquent tooclassify d’étiquettes et de protéger des documents partagés interne ou externe et de messagerie électronique. Certains de ces éléments peuvent contenir des informations personnelles sur les clients ou les employés. Les règles et les conditions peuvent être définies automatiquement ou manuellement par les administrateurs ou les utilisateurs. Par exemple, si un utilisateur enregistre un document qui inclut des informations de carte de crédit, il ou elle visualiserez une recommandation d’étiquette qui a été configurée par l’administrateur de hello.

### <a name="how-do-i-try-it"></a>Comment tester le produit ?

Si vous souhaitez que toogive Azure Information Protection un toosee try si elle peut être une solution pour votre organisation, visitez hello [didacticiel de démarrage rapide](https://docs.microsoft.com/information-protection/get-started/infoprotect-quick-start-tutorial). Il vous guide dans les cinq étapes de base : à partir de l’installation tooconfiguring stratégie tooseeing classification, l’étiquetage et le partage en action et vous devez prendre moins d’une demi-heure.

### <a name="how-do-i-deploy-it"></a>Comment déployer le produit ?

Si vous souhaitez que toodeploy Azure Information Protection pour votre organisation, visitez hello [Guide de déploiement pour la classification, l’étiquetage et protection](https://docs.microsoft.com/information-protection/plan-design/deployment-roadmap).

### <a name="is-there-anything-else-i-should-know"></a>Y a-t-il autre chose à savoir ?

Pour plus d’informations complémentaires qui vous aideront à penser à la façon dont tooset il, visitez hello [prêt, définir, protéger !](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)
. Et vérification hello en savoir plus des liens ci-dessous pour plus d’informations sur Azure Information Protection.

## <a name="azure-search-data-discovery-for-developer-apps"></a>Recherche Azure : découverte de données pour les applications de développeurs

Le service [Recherche Azure](https://azure.microsoft.com/services/search/) est une solution de recherche cloud qui s’adresse aux développeurs et offre une expérience de recherche de données avancée pour vos applications. Azure Search vous permet de toolocate données sur les index définis par l’utilisateur, provenant de la base de données Azure Cosmo, base de données SQL Azure, Azure Blob Storage, stockage de Table Azure ou client personnalisée des données JSON. Vous pouvez également structurer les requêtes Lucene à l’aide de toosearch d’API REST Azure Search hello pour les types de données personnelles ou données personnelles de hello des personnes spécifiques. Elle intègre les fonctionnalités suivantes : recherche en texte intégral, syntaxe de requête simple et syntaxe de requête Lucene. 

## <a name="how-do-i-use-sql-tooquery-data"></a>Utilisation de données SQL tooquery

toobegin avec les concepts de base hello, visitez hello [base de données Azure CosmosD : comment tooquery à l’aide de SQL](../cosmos-db/tutorial-query-documentdb.md) didacticiel. didacticiel de Hello fournit un exemple de document et les deux exemples de requêtes SQL et les résultats.

Pour obtenir des instructions détaillées sur la création de requêtes SQL, consultez [Requêtes SQL pour l’API DocumentDB Azure Cosmos DB](../cosmos-db/documentdb-sql-query.md).

Si vous tooAzure nouvelle base de données Cosmos et comme toolearn toocreate une base de données, ajouter une collection, et ajouter des données, rendez-vous à hello [base de données Azure Cosmos : génération d’une application de web API DocumentDB](../cosmos-db/create-documentdb-dotnet.md) didacticiel de démarrage rapide. Si vous souhaitez que toodo dans une langue autre que .NET, tels que Java ou Python, choisissez votre langue par défaut une fois que vous avez toohello site.

## <a name="next-steps"></a>Étapes suivantes

[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50)

[Définition de la base de données SQL](../sql-database/sql-database-technical-overview.md)

[Éditeur de requêtes SQL Database disponible dans le portail Azure] (https://azure.microsoft.com/blog/t-sql-query-editor-in-browser-azure-portal/)

[Qu’est-ce qu’Azure Information Protection ?](https://docs.microsoft.com/information-protection/understand-explore/what-is-information-protection)

[En quoi consiste Azure Rights Management ?](https://docs.microsoft.com/information-protection/understand-explore/what-is-azure-rms)

[Azure Information Protection: Ready, set, protect!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)
