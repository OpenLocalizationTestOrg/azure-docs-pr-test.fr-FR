---
title: aaaWhat est Azure Search | Documents Microsoft
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
ms.openlocfilehash: b38a7e93a7f0e0d5f8a3779858032271b3883778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-search"></a>Présentation d’Azure Search
Recherche Azure est une solution cloud de recherche en tant que service, qui offre aux développeurs des API et des outils permettant d’ajouter une expérience de recherche riche concernant vos données dans les applications web, mobiles et d’entreprise.

Fonctionnalités sont exposées via une simple [API REST](/rest/api/searchservice/) ou [.NET SDK](search-howto-dotnet-sdk.md) qui masque la complexité inhérente de hello de technologie de recherche. Dans Ajout tooAPIs, hello portail Azure permet l’administration et prise en charge de la création de prototypes. L’infrastructure et la disponibilité sont gérées par Microsoft.

<a name="feature-drilldown"></a>

## <a name="feature-summary"></a>Résumé des fonctionnalités

| Catégorie | Caractéristiques |
|----------|----------|
|Recherche en texte intégral et analyse de texte | La [**recherche en texte intégral**](search-lucene-query-architecture.md) est le cas d’usage principal pour la plupart des applications basées sur la recherche. Vous pouvez formuler des requêtes à l’aide d’une syntaxe prise en charge : <br/><br/>La [**syntaxe de requête simple**](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) offre des opérateurs logiques, de recherche d’expression, de suffixe et de précédence.<br/><br/>La [**syntaxe de requête Lucene**](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) offre une prise en charge des requêtes simples et permet des recherches approximatives, des recherches de proximité, la valorisation de termes et des expressions régulières.| 
| Intégration des données | Les index Recherche Azure acceptent les données de n’importe quelle source, sous réserve qu’elles soient soumises en tant que structure de données JSON. <br/><br/> Pour les sources de données pris en charge dans Azure, vous pouvez éventuellement utiliser [ **indexeurs** ](search-indexer-overview.md) tooautomatically analyse [base de données SQL Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md), [base de données Azure Cosmos](search-howto-index-documentdb.md), ou [le stockage Blob Azure](search-howto-indexing-azure-blob-storage.md) toosync votre index de recherche de contenu avec votre banque de données principale. Les indexeurs d’objets blob Azure peuvent effectuer une *recherche de document* pour [indexer la plupart des formats de fichier](search-howto-indexing-azure-blob-storage.md), y compris Microsoft Office, ainsi que les documents PDF et HTML. |
| Analyse de recherche | Les [**analyseurs lexicaux personnalisés**](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) sont disponibles pour des requêtes de recherche complexes au moyen de la mise en correspondance phonétique et des expressions régulières. |
| Support multilingue | [**Analyseurs de langage** ](https://docs.microsoft.com/rest/api/searchservice/language-support) Lucene, ainsi que Microsoft de processeurs de langage naturel dans linguistics de 56 différentes langues toointelligently descripteur spécifiques au langage notamment verbaux, sexe, pluriel irrégulière noms (par exemple, « souris' et 'mice'), word Annuler de composition, l’analyse lexicale (pour les langues sans espaces) et bien plus encore. |
| Recherche basée sur la localisation | Azure Search traite, filtre et affiche les emplacements géographiques de manière intelligente. Il permet aux utilisateurs tooexplore données basée sur la proximité hello d’un emplacement physique de tooa de résultats de recherche. [Regardez cette vidéo](https://channel9.msdn.com/Shows/Data-Exposed/Azure-Search-and-Geospatial-Data) ou [Examinez cet exemple](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs) toolearn plus. |
| Fonctionnalités de l’expérience utilisateur | [**Suggestions de recherche**](https://docs.microsoft.com/rest/api/searchservice/suggesters) peut être activée pour les requêtes prédictives dans une barre de recherche. Les documents de votre index sont suggérés lorsque les utilisateurs saisissent une entrée de recherche partielle. <br/><br/>La [**navigation par facettes**](https://docs.microsoft.com/azure/search/search-faceted-navigation) est activée par le biais d’un seul paramètre de requête. Azure Search retourne une structure de navigation par facettes que vous pouvez utiliser en tant que code hello derrière une liste de catégories pour le filtrage des autonome (par exemple, toofilter éléments de catalogue par gamme de prix ou marque). <br/><br/> [**Filtres** ](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) peut être une navigation par facettes tooincorporate utilisé dans l’interface utilisateur de votre application, améliorer la formulation de requêtes et filtre en fonction de critères d’utilisateur ou développeur spécifié. Créer des filtres à l’aide de la syntaxe d’OData hello.<br/><br/> [**Mise en surbrillance d’accès** ](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) s’applique tooa de mise en forme visuelle mot clé dans les résultats de la recherche de correspondance. Vous pouvez choisir quels champs renvoient les extraits de texte en surbrillance.<br/><br/>[**Tri** ](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) est proposé pour plusieurs champs via le schéma d’index hello et puis activé ou désactivé au moment de la requête avec un paramètre de recherche unique.<br/><br/> [**La pagination** ](search-pagination-page-layout.md) et la limitation de vos résultats de recherche est simple avec contrôle de hello ajusté Azure Search offre par rapport à vos résultats de recherche.  
| Pertinence | [**Notation simple**](/rest/api/searchservice/add-scoring-profiles-to-a-search-index) est l’un des principaux avantages de Recherche Azure. Profils de calcul de score sont utilisés toomodel pertinence comme une fonction des valeurs hello documents eux-mêmes. Par exemple, vous souhaiterez peut-être produits nouveaux ou tooappear produits plus haut dans les résultats de la recherche hello à prix réduit. Vous pouvez également créer des profils de score à l'aide de balises pour obtenir un score personnalisé en fonction de préférences de recherche de client que vous avez suivies et stockées séparément. |
| Surveillance et création de rapports | [**Recherche analytique de trafic** ](search-traffic-analytics.md) sont insights toounlock collectées et analysées à partir de ce que les utilisateurs sont en tapant dans la zone de recherche hello. <br/><br/>Des mesures sur les requêtes par seconde, la latence et la limitation sont capturées et affichées sur les pages du portail sans aucune configuration supplémentaire. Vous pouvez également facilement surveiller le nombre d’index et de documents afin d’ajuster la capacité en fonction des besoins. Pour en savoir plus, consultez [Administration de service](search-manage.md) |
| Outils de prototypage et d’inspection | Dans le portail hello, vous pouvez utiliser hello [ **Assistant Importer des données** ](search-import-data-portal.md) tooconfigure indexeurs, Concepteur toostand un index, l’index et [ **rechercher dans l’Explorateur** ](search-explorer.md) tootest interroge et affiner les profils de calcul de score. Vous pouvez également ouvrir n’importe quel tooview index son schéma. |
| Infrastructure | Hello **plateforme hautement disponible** garantit une expérience de service de recherche extrêmement fiable. Lorsqu’il est correctement mis à l'échelle, [Azure Search offre un SLA de 99,9 %](https://azure.microsoft.com/support/legal/sla/search/v1_0/).<br/><br/> En tant que solution complète **entièrement gérée et extensible**, Recherche Azure n’exige absolument aucune gestion d’infrastructure. Votre service peut être tooyour aux besoins en mise à l’échelle dans les deux dimensions toohandle plus de stockage de document, plus les charges de requête ou les deux.

## <a name="how-it-works"></a>Fonctionnement
### <a name="step-1-provision-service"></a>Étape 1 : configurer le service
Vous pouvez lancer un service Azure Search Bonjour [portail Azure](https://portal.azure.com/) ou via hello [API de gestion des ressources Azure](/rest/api/searchmanagement/). Vous pouvez choisir un service gratuit hello partagée avec d’autres abonnés, ou un [payé couche](https://azure.microsoft.com/pricing/details/search/) qui consacre les ressources utilisées uniquement par votre service. Pour les niveaux payants, vous pouvez mettre à l’échelle un service dans deux dimensions : 

- Ajoutez toogrow réplicas que charge de votre requête importante toohandle de capacité.   
- Ajouter un stockage toogrow Partitions plus de documents. 

En gérant le stockage de documents et le débit de requêtes séparément, vous pouvez étalonner l’allocation de ressources en fonction des besoins de production.

### <a name="step-2-create-index"></a>Étape 2 : créer un index
Avant de pouvoir charger du contenu qui peut faire l’objet de recherches, vous devez d’abord définir un index Recherche Azure. Un index est comparable à une table de base de données qui conserve vos données et peut accepter des requêtes de recherche. Vous définissez hello index schéma toomap tooreflect hello structure des documents de hello vous souhaitez toosearch, toofields semblable dans une base de données.

Un schéma peut être créé dans hello Azure hello portail, ou par programme à l’aide [.NET SDK](search-howto-dotnet-sdk.md) ou [API REST](/rest/api/searchservice/).

### <a name="step-3-index-data"></a>Étape 3 : indexer les données
Après avoir défini un index, vous êtes le contenu tooupload prêt. Vous pouvez utiliser un modèle push ou pull.

modèle d’extraction Hello récupère les données à partir de sources de données externes. Ce modèle est pris en charge grâce aux *indexeurs* qui simplifient et automatisent certains aspects de l’ingestion de données, comme la connexion aux données, leur lecture et leur sérialisation. Des [indexeurs](/rest/api/searchservice/Indexer-operations) sont disponibles pour Azure Cosmos DB, Azure SQL Database, Stockage Blob Azure et SQL Server hébergé dans une machine virtuelle Azure. Vous pouvez configurer un indexeur pour une actualisation de données à la demande ou planifiée.

modèle d’émission Hello est fournie par hello SDK ou des API REST, utilisés pour l’envoi de l’index de tooan documents mis à jour. Vous pouvez transmettre des données à partir de pratiquement n’importe quel jeu de données à l’aide du format JSON de hello. Consultez [ajouter, mettre à jour ou supprimer des Documents](/rest/api/searchservice/addupdate-or-delete-documents) ou [comment toouse hello .NET SDK)](search-howto-dotnet-sdk.md) pour obtenir des conseils sur le chargement des données.

### <a name="step-4-search"></a>Étape 4 : lancer la recherche
Après avoir rempli un index, vous pouvez [émettre des requêtes de recherche](/rest/api/searchservice/Search-Documents) tooyour point de terminaison de service à l’aide de HTTP simple demande avec l’API REST ou hello du SDK .NET.

## <a name="how-it-compares"></a>Comparaison

Les clients demandent souvent comment la [recherche en texte intégral dans Recherche Azure](search-lucene-query-architecture.md) se situe par rapport à la [recherche en texte intégral](https://en.wikipedia.org/wiki/Full_text_search) au sein de leur produit de base de données. Notre réponse est que les fonctionnalités de langage d’Azure Search sont plus riche et plus souple, avec prise en charge pour les requêtes de Lucene, les analyseurs de langage Lucene et Microsoft, des analyseurs personnalisés pour phonétiques ou d’autres entrées spécialisées et hello capacité toomerge les données plusieurs sources de l’index de recherche hello. 

Un autre point d’inflexion est qu’une solution de recherche d’adresses expérience de recherche hello. Par exemple, vous pouvez mettre en place une notation personnalisée des résultats, une navigation par facettes pour le filtrage autonome, une mise en surbrillance des résultats et des suggestions de requête prédictives. 

Les outils permettant de surveiller et de comprendre l’activité des requêtes peuvent aussi compter dans une décision de solution de recherche. Par exemple, Recherche Azure prend en charge l’[analyse du trafic de recherche](search-traffic-analytics.md) pour les métriques relatives aux taux de clics publicitaires, aux recherches les plus fréquentes, aux recherches sans clics, etc. Dans les produits pour lesquels la recherche est un module complémentaire, vous êtes toofind peu probable que ces fonctionnalités.

L’utilisation des ressources est un autre élément à prendre en considération. La recherche en langage naturel demande généralement beaucoup de ressources de calcul. Certains de nos clients déchargées tooAzure opérations de recherche recherche comme un moyen toopreserve machine des ressources pour le traitement des transactions. Externalisation recherche, vous pouvez facilement ajuster échelle toomatch requête volume.

Une fois que vous avez décidé de toogo avec une recherche dédiée, votre décision suivante existe entre un service cloud ou un serveur local. Un service cloud est hello bon choix si vous souhaitez un [solution clé en main avec une surcharge minimale et la maintenance et l’échelle réglable](#cloud-service-advantage).

Dans le paradigme du cloud hello, plusieurs fournisseurs offrent des fonctionnalités de comparable au niveau de la ligne de base, avec recherche en texte intégral, recherche géographique et hello capacité toohandle un certain niveau de toute ambiguïté dans les entrées de la recherche. En règle générale, il a un [fonctionnalité spécialement](#feature-drilldown), ou facilité de hello et la simplicité générale d’API, d’outils et de gestion qui détermine le mieux hello.

Parmi les fournisseurs de services cloud, Recherche Azure s’avère plus efficace pour ce qui est des charges de travail de recherche en texte intégral sur les bases de données et les magasins de contenu sur Azure, dans le cas des applications qui s’appuient principalement sur la recherche pour récupérer les informations et parcourir le contenu. Voici les principaux atouts :

+ Intégration de données Azure (robots) au niveau de la couche d’indexation hello
+ Portail Azure de gestion centralisée
+ Mise à l’échelle Azure, fiabilité et disponibilité de premier ordre
+ Analyse linguistique et personnalisée, incluant des analyseurs de recherche en texte intégral solide en 56 langues
+ [Principales fonctionnalités des applications centrées sur les toosearch courantes](#feature-drilldown): calcul de score, des facettes, des suggestions, synonymes, recherche géographique et bien plus encore.

> [!Note]
> sources de données clair et non-Azure toobe sont entièrement pris en charge, mais s’appuient sur une méthodologie de push beaucoup plus du code au lieu des indexeurs. À l’aide de notre API, vous pouvez diriger n’importe quel index Azure Search tooan de collection de document JSON.

Parmi nos clients, ces tooleverage en mesure de hello plus large éventail de fonctionnalités dans Azure Search incluent des catalogues en ligne, line-of-business, applications et programmes document découverte.

## <a name="rest-api--net-sdk"></a>API REST | .Net SDK

Alors que de nombreuses tâches peuvent être effectuées dans le portail de hello, Azure Search est destiné aux développeurs qui veulent toointegrate les fonctionnalités de recherche dans les applications existantes. Hello suit les interfaces de programmation est disponible.

|Plateforme |Description |
|-----|------------|
|[REST](/rest/api/searchservice/) | Commandes HTTP prises en charge par tous les langages et toutes les plateformes de programmation, y compris Xamarin, Java et JavaScript.|
|[Kit SDK .NET](search-howto-dotnet-sdk.md) | Wrapper .NET pour l’API REST de hello offre un codage efficace en c# et d’autres langages de code managé qui ciblent hello .NET Framework |

## <a name="free-trial"></a>Essai gratuit
Les abonnés Azure peuvent [configurer un service de niveau gratuit de hello](search-create-service-portal.md).

Si vous n’êtes pas abonné, vous pouvez [ouvrir gratuitement un compte Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F). Vous obtenez alors des crédits pour tester les services Azure payants. Une fois qu’ils sont utilisés, vous pouvez conserver le compte de hello et utiliser [libérer des services Azure](https://azure.microsoft.com/free/). Votre carte de crédit n’est jamais facturé, sauf si vous modifiez vos paramètres et demandez toobe facturé explicitement.

Vous pouvez aussi [activer les avantages de l’abonnement MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) : votre abonnement MSDN vous donne droit chaque mois à des crédits dont vous pouvez vous servir pour les services Azure payants. 

## <a name="how-tooget-started"></a>Mode de démarrage tooget

1. Créer un service Bonjour [niveau gratuit](search-create-service-portal.md).

2. Exécuter une ou plusieurs des hello suivant des didacticiels. 

  + [Comment toouse hello .NET SDK](search-howto-dotnet-sdk.md) illustre les étapes hello principal dans le code managé.  
  + [Prise en main hello API REST](https://github.com/Azure-Samples/search-rest-api-getting-started) montre même hello étapes à l’aide des API REST de hello.  
  + [Créer votre premier index dans le portail de hello](search-get-started-portal.md) montre les fonctionnalités intégrées de l’indexation et de prototype du portail hello.   

Moteurs de recherche sont hello courantes de récupération d’informations dans les applications mobiles, sur le web de hello et dans des magasins de données d’entreprise. Azure Search offre des outils pour la création d’un toothose similaire expérience de recherche pour les grands sites web commerciaux.

Dans cette vidéo de 9 minutes du responsable de programme Liam Cavanagh, découvrez en quoi l’intégration d’un moteur de recherche peut profiter à votre application. Les principales fonctionnalités de Recherche Azure vous sont présentées dans de courtes démonstrations, et vous découvrirez ce qu’est un flux de travail type. 

>[!VIDEO https://channel9.msdn.com/Events/Connect/2016/138/player]
 
+ Entre 0 et 3 minutes : présentation des principales fonctionnalités et cas d’emploi.
+ Entre 3 et 4 minutes : approvisionnement du service. 
+ 4 à 6 minutes couvre toocreate d’Assistant Importer des données un index à l’aide de jeu de données intégrées immobilier hello.
+ Entre 6 et 9 minutes : présentation de l’Explorateur de recherche et de différentes requêtes.


