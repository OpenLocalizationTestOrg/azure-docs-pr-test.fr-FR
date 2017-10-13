---
title: "Qu’est-ce que la Recherche Azure ? | Microsoft Docs"
description: "Azure Search est un service de recherche cloud hébergé intégralement géré. En savoir plus dans la vue d'ensemble de cette fonctionnalité."
services: search
manager: jhubbard
author: ashmaka
documentationcenter: 
ms.assetid: 50bed849-b716-4cc9-bbbc-b5b34e2c6153
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/26/2017
ms.author: ashmaka
ms.openlocfilehash: baf73639eb6506b14d0d3a4de1bf55b66e973b95
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-azure-search"></a>Présentation d’Azure Search
Recherche Azure est une solution cloud de recherche en tant que service, qui offre aux développeurs des API et des outils permettant d’ajouter une expérience de recherche riche concernant vos données dans les applications web, mobiles et d’entreprise.

Cette fonctionnalité est exposée par le biais d’une [API REST](/rest/api/searchservice/) ou d’un [SDK .NET](search-howto-dotnet-sdk.md) simple, qui masque la complexité inhérente de la technologie de recherche. En plus des API, le portail Azure fournit un support administratif et de prototypage. L’infrastructure et la disponibilité sont gérées par Microsoft.

<a name="feature-drilldown"></a>

## <a name="feature-summary"></a>Résumé des fonctionnalités

| Catégorie | Caractéristiques |
|----------|----------|
|Recherche en texte intégral et analyse de texte | La [**recherche en texte intégral**](search-lucene-query-architecture.md) est le cas d’usage principal pour la plupart des applications basées sur la recherche. Vous pouvez formuler des requêtes à l’aide d’une syntaxe prise en charge : <br/><br/>La [**syntaxe de requête simple**](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) offre des opérateurs logiques, de recherche d’expression, de suffixe et de précédence.<br/><br/>La [**syntaxe de requête Lucene**](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) offre une prise en charge des requêtes simples et permet des recherches approximatives, des recherches de proximité, la valorisation de termes et des expressions régulières.| 
| Intégration des données | Les index Recherche Azure acceptent les données de n’importe quelle source, sous réserve qu’elles soient soumises en tant que structure de données JSON. <br/><br/> Pour les sources de données prises en charge dans Azure, vous pouvez aussi utiliser des [**indexeurs**](search-indexer-overview.md) qui analysent automatiquement [Azure SQL Database](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md), [Azure Cosmos DB](search-howto-index-documentdb.md) ou le [stockage blob Azure](search-howto-indexing-azure-blob-storage.md) afin de synchroniser le contenu de votre index de recherche avec votre magasin de données principal. Les indexeurs d’objets blob Azure peuvent effectuer une *recherche de document* pour [indexer la plupart des formats de fichier](search-howto-indexing-azure-blob-storage.md), y compris Microsoft Office, ainsi que les documents PDF et HTML. |
| Analyse de recherche | Les [**analyseurs lexicaux personnalisés**](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) sont disponibles pour des requêtes de recherche complexes au moyen de la mise en correspondance phonétique et des expressions régulières. |
| Support multilingue | [**Analyseurs de langage**](https://docs.microsoft.com/rest/api/searchservice/language-support) de Lucene, ainsi que les processeurs de langage naturel Microsoft disponibles dans 56 langues pour gérer intelligemment les caractéristiques linguistiques propres à la langue, notamment les temps des verbes, le masculin et le féminin, les noms au pluriel irrégulier (par exemple, « cheval » et « chevaux »), la décomposition des mots, la césure des mots (pour les langues sans espaces), etc. |
| Recherche basée sur la localisation | Azure Search traite, filtre et affiche les emplacements géographiques de manière intelligente. Les utilisateurs peuvent ainsi explorer les données selon la proximité d’un résultat de recherche par rapport à un emplacement physique. [Regardez cette vidéo](https://channel9.msdn.com/Shows/Data-Exposed/Azure-Search-and-Geospatial-Data) ou [étudiez cet exemple](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs) pour en savoir plus. |
| Fonctionnalités de l’expérience utilisateur | [**Suggestions de recherche**](https://docs.microsoft.com/rest/api/searchservice/suggesters) peut être activée pour les requêtes prédictives dans une barre de recherche. Les documents de votre index sont suggérés lorsque les utilisateurs saisissent une entrée de recherche partielle. <br/><br/>La [**navigation par facettes**](https://docs.microsoft.com/azure/search/search-faceted-navigation) est activée par le biais d’un seul paramètre de requête. La Recherche Azure renvoie une structure de navigation par facettes que vous pouvez utiliser en tant que code de liste de catégories pour le filtrage autonome (par exemple, pour filtrer les éléments de catalogue par plage de prix ou par marque). <br/><br/> L’option [**Filtres**](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) permet d’intégrer la navigation par facettes dans l’interface utilisateur de votre application, d’améliorer la formulation des requêtes et d’appliquer un filtre en fonction de critères spécifiés par les utilisateurs ou les développeurs. Créez des filtres à l’aide de la syntaxe OData.<br/><br/> Le [**surligneur d’éléments**](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) applique la mise en forme visuelle à un mot clé correspondant dans les résultats de la recherche. Vous pouvez choisir quels champs renvoient les extraits de texte en surbrillance.<br/><br/>[**Tri**](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) est proposée pour plusieurs champs par le biais du schéma d’index, et elle est activée ou désactivée au moment de la requête avec un paramètre de recherche unique.<br/><br/> [**Pagination**](search-pagination-page-layout.md) et la limitation des résultats de la recherche sont d’un fonctionnement très simple avec le contrôle finement ajusté qu’offre Recherche Azure sur vos résultats de recherche.  
| Pertinence | [**Notation simple**](/rest/api/searchservice/add-scoring-profiles-to-a-search-index) est l’un des principaux avantages de Recherche Azure. Les profils de score permettent de modéliser la pertinence en fonction des valeurs dans les documents eux-mêmes. Par exemple, vous souhaiterez peut-être que les nouveaux produits ou les produits en promotion apparaissent en priorité dans les résultats de la recherche. Vous pouvez également créer des profils de score à l'aide de balises pour obtenir un score personnalisé en fonction de préférences de recherche de client que vous avez suivies et stockées séparément. |
| Surveillance et création de rapports | Les [**analyses de trafic de recherche**](search-traffic-analytics.md) sont recueillies et analysées pour fournir une source d’information à partir des termes employés par les utilisateurs dans la zone de recherche. <br/><br/>Des mesures sur les requêtes par seconde, la latence et la limitation sont capturées et affichées sur les pages du portail sans aucune configuration supplémentaire. Vous pouvez également facilement surveiller le nombre d’index et de documents afin d’ajuster la capacité en fonction des besoins. Pour en savoir plus, consultez [Administration de service](search-manage.md) |
| Outils de prototypage et d’inspection | Dans le portail, vous pouvez utiliser l’[**Assistant Importation de données**](search-import-data-portal.md) pour configurer des indexeurs, le concepteur d’index pour créer un index, et l’[**Explorateur de recherche**](search-explorer.md) pour tester les requêtes et affiner les profils de score. Vous pouvez également ouvrir un index pour consulter son schéma. |
| Infrastructure | La **plateforme haute disponibilité** garantit une expérience de service de recherche extrêmement fiable. Lorsqu’il est correctement mis à l'échelle, [Azure Search offre un SLA de 99,9 %](https://azure.microsoft.com/support/legal/sla/search/v1_0/).<br/><br/> En tant que solution complète **entièrement gérée et extensible**, Recherche Azure n’exige absolument aucune gestion d’infrastructure. Votre service peut être adapté à vos besoins avec la mise à l’échelle en deux dimensions pour gérer plus de stockage de documents, plus de charge de requêtes, ou les deux.

## <a name="how-it-works"></a>Fonctionnement
### <a name="step-1-provision-service"></a>Étape 1 : configurer le service
Vous pouvez mettre en place un service Recherche Azure dans le [portail Azure](https://portal.azure.com/) ou via [l’API de gestion des ressources Azure](/rest/api/searchmanagement/). Vous pouvez opter pour le service gratuit partagé avec d’autres abonnés ou pour un [niveau payant](https://azure.microsoft.com/pricing/details/search/) qui dédie les ressources que seul votre service utilise. Pour les niveaux payants, vous pouvez mettre à l’échelle un service dans deux dimensions : 

- Ajoutez des réplicas pour accroître votre capacité à traiter de lourdes charges de requêtes.   
- Ajoutez des partitions pour accroître votre capacité à stocker plus de documents. 

En gérant le stockage de documents et le débit de requêtes séparément, vous pouvez étalonner l’allocation de ressources en fonction des besoins de production.

### <a name="step-2-create-index"></a>Étape 2 : créer un index
Avant de pouvoir charger du contenu qui peut faire l’objet de recherches, vous devez d’abord définir un index Recherche Azure. Un index est comparable à une table de base de données qui conserve vos données et peut accepter des requêtes de recherche. Vous devez définir le schéma d’index à mapper pour refléter la structure des documents dans lesquels vous voulez effectuer des recherches, de la même façon que les champs d’une base de données.

Il est possible de créer un schéma dans le portail Azure ou par programmation à l’aide du [Kit de développement logiciel (SDK) .NET](search-howto-dotnet-sdk.md) ou de [l’API REST](/rest/api/searchservice/).

### <a name="step-3-index-data"></a>Étape 3 : indexer les données
Une fois que vous avez défini un index, vous êtes prêt à charger du contenu. Vous pouvez utiliser un modèle push ou pull.

Le modèle push extrait des données auprès de sources de données externes. Ce modèle est pris en charge grâce aux *indexeurs* qui simplifient et automatisent certains aspects de l’ingestion de données, comme la connexion aux données, leur lecture et leur sérialisation. Des [indexeurs](/rest/api/searchservice/Indexer-operations) sont disponibles pour Azure Cosmos DB, Azure SQL Database, Stockage Blob Azure et SQL Server hébergé dans une machine virtuelle Azure. Vous pouvez configurer un indexeur pour une actualisation de données à la demande ou planifiée.

Le modèle d’émission est fourni via le Kit de développement logiciel (SDK) ou les API REST permettant d’envoyer les documents mis à jour à un index. Vous pouvez émettre des données à partir de n'importe quel groupe de données à l’aide du format JSON. Pour obtenir des conseils sur le chargement des données, consultez [Ajout, mise à jour ou suppression de documents](/rest/api/searchservice/addupdate-or-delete-documents) ou [Utilisation du Kit de développement logiciel (SDK) .NET](search-howto-dotnet-sdk.md).

### <a name="step-4-search"></a>Étape 4 : lancer la recherche
Après avoir rempli une index, vous pouvez [émettre des requêtes de recherche](/rest/api/searchservice/Search-Documents) à destination du point de terminaison du service en utilisant des requêtes HTTP simples avec l’API REST ou le SDK .NET.

## <a name="how-it-compares"></a>Comparaison

Les clients demandent souvent comment la [recherche en texte intégral dans Recherche Azure](search-lucene-query-architecture.md) se situe par rapport à la [recherche en texte intégral](https://en.wikipedia.org/wiki/Full_text_search) au sein de leur produit de base de données. Nous leur répondons que les capacités de langage de Recherche Azure sont plus riches et plus souples, grâce à une prise en charge des requêtes Lucene, des analyseurs de langage de Lucene et Microsoft, des analyseurs personnalisés pour les entrées phonétiques ou d’autres entrées spécialisées, et à la possibilité de fusionner des données issues de plusieurs sources dans l’index de recherche. 

L’autre point d’inflexion est qu’une solution de recherche porte sur l’intégralité de l’expérience de recherche. Par exemple, vous pouvez mettre en place une notation personnalisée des résultats, une navigation par facettes pour le filtrage autonome, une mise en surbrillance des résultats et des suggestions de requête prédictives. 

Les outils permettant de surveiller et de comprendre l’activité des requêtes peuvent aussi compter dans une décision de solution de recherche. Par exemple, Recherche Azure prend en charge l’[analyse du trafic de recherche](search-traffic-analytics.md) pour les métriques relatives aux taux de clics publicitaires, aux recherches les plus fréquentes, aux recherches sans clics, etc. Il est peu probable que vous rencontriez ces fonctionnalités dans les produits dont les fonctionnalités de recherche correspondent à un module complémentaire.

L’utilisation des ressources est un autre élément à prendre en considération. La recherche en langage naturel demande généralement beaucoup de ressources de calcul. Certains de nos clients ont délégué les opérations de recherche à Recherche Azure dans le but de réserver les ressources informatiques au traitement des transactions. En externalisant la recherche, vous pouvez facilement ajuster l’échelle en fonction du volume des requêtes.

Une fois que vous avez pris la décision d’utiliser une recherche dédiée, vous devez choisir entre un service cloud ou un serveur local. La décision d’opter pour un service cloud s’avère un bon choix si vous cherchez une [solution clé en main ajustable avec une surcharge et une maintenance minimes](#cloud-service-advantage).

Dans le paradigme du cloud, plusieurs fournisseurs proposent des fonctionnalités de base comparables, notamment une recherche en texte intégral, une recherche en fonction de la localisation et une capacité à gérer un certain niveau d’ambiguïté dans les entrées de recherche. En général, c’est une [fonctionnalité spécialisée](#feature-drilldown) ou l’ergonomie et la simplicité globales des API, des outils et de la gestion qui déterminent la meilleure option.

Parmi les fournisseurs de services cloud, Recherche Azure s’avère plus efficace pour ce qui est des charges de travail de recherche en texte intégral sur les bases de données et les magasins de contenu sur Azure, dans le cas des applications qui s’appuient principalement sur la recherche pour récupérer les informations et parcourir le contenu. Voici les principaux atouts :

+ Intégration de données Azure (robots) au niveau de la couche d’indexation
+ Portail Azure de gestion centralisée
+ Mise à l’échelle Azure, fiabilité et disponibilité de premier ordre
+ Analyse linguistique et personnalisée, incluant des analyseurs de recherche en texte intégral solide en 56 langues
+ [Principales fonctionnalités communes aux applications centrées sur les recherches](#feature-drilldown) : notation, recherche par facettes, suggestions, synonymes, recherche basée sur la localisation, etc.

> [!Note]
> Pour être clair, les sources de données non Azure sont entièrement prises en charge, mais elles s’appuient non pas sur des indexeurs mais sur une méthodologie Push qui fait largement appel au code. En utilisant nos API, vous pouvez diriger n’importe quelle collection de documents JSON vers un index Recherche Azure.

Parmi nos clients, ceux capables d’exploiter le plus large éventail de fonctionnalités Recherche Azure sont les catalogues en ligne, les programmes métier et les applications de découverte de documents.

## <a name="rest-api--net-sdk"></a>API REST | .Net SDK

Bien qu’il soit possible d’effectuer de nombreuses tâches dans le portail, Recherche Azure s’adresse avant tout aux développeurs désireux d’intégrer la fonctionnalité de recherche dans des applications existantes. Les interfaces de programmation suivantes sont disponibles.

|Plateforme |Description |
|-----|------------|
|[REST](/rest/api/searchservice/) | Commandes HTTP prises en charge par tous les langages et toutes les plateformes de programmation, y compris Xamarin, Java et JavaScript.|
|[Kit SDK .NET](search-howto-dotnet-sdk.md) | Le wrapper .NET pour l’API REST offre un codage efficace en C# et d’autres langages de code géré ciblant .NET Framework. |

## <a name="free-trial"></a>Essai gratuit
Les abonnés Azure peuvent [configurer un service dans le niveau Gratuit](search-create-service-portal.md).

Si vous n’êtes pas abonné, vous pouvez [ouvrir gratuitement un compte Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F). Vous obtenez alors des crédits pour tester les services Azure payants. Une fois ceux-ci épuisés, vous pouvez conserver le compte et utiliser les [services Azure gratuits](https://azure.microsoft.com/free/). Votre carte de crédit n’est pas débitée tant que vous n’avez pas explicitement modifié vos paramètres pour demander à l’être.

Vous pouvez aussi [activer les avantages de l’abonnement MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) : votre abonnement MSDN vous donne droit chaque mois à des crédits dont vous pouvez vous servir pour les services Azure payants. 

## <a name="how-to-get-started"></a>Pour commencer

1. Créez un service dans le [niveau Gratuit](search-create-service-portal.md).

2. Parcourez un ou plusieurs des didacticiels suivants. 

  + [Utilisation du kit de développement logiciel (SDK) .NET](search-howto-dotnet-sdk.md) illustre les principales étapes liées au code managé.  
  + [Getting started with Azure Search using the REST API ](https://github.com/Azure-Samples/search-rest-api-getting-started) (Prise en main de Recherche Azure à l’aide de l’API REST) présente les mêmes étapes avec l’API REST.  
  + [Créer votre premier index Recherche Azure dans le portail](search-get-started-portal.md) montre les fonctionnalités intégrées d’indexation et de prototypage du portail.   

Les moteurs de recherche servent généralement à récupérer les informations sur les applications mobiles, sur le web et dans les magasins de données d’entreprise. Avec la Recherche Azure, vous disposez d’outils permettant de créer une expérience de recherche semblable à celle des grands sites web commerciaux.

Dans cette vidéo de 9 minutes du responsable de programme Liam Cavanagh, découvrez en quoi l’intégration d’un moteur de recherche peut profiter à votre application. Les principales fonctionnalités de Recherche Azure vous sont présentées dans de courtes démonstrations, et vous découvrirez ce qu’est un flux de travail type. 

>[!VIDEO https://channel9.msdn.com/Events/Connect/2016/138/player]
 
+ Entre 0 et 3 minutes : présentation des principales fonctionnalités et cas d’emploi.
+ Entre 3 et 4 minutes : approvisionnement du service. 
+ Entre 4 et 6 minutes : utilisation de l’Assistant Importation de données pour créer un index à l’aide du jeu de données intégrées sur l’immobilier.
+ Entre 6 et 9 minutes : présentation de l’Explorateur de recherche et de différentes requêtes.


