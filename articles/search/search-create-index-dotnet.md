---
title: "AAA « créer un index (API .NET - Azure Search) | Documents Microsoft »"
description: "Créer un index dans le code à l’aide de hello Azure Search .NET SDK."
services: search
documentationcenter: 
author: brjohnstmsft
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 3a851647-fc7b-4fb6-8506-6aaa519e77cd
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 7fa4030b8c3565bc02b1d6bb4426331657cf3a5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-net-sdk"></a>Créer un index Azure Search à l’aide de hello .NET SDK
> [!div class="op_single_selector"]
> * [Vue d'ensemble](search-what-is-an-index.md)
> * [Portail](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

Cet article vous guide tout au long des processus de hello de création d’un indexeur Azure Search [index](https://docs.microsoft.com/rest/api/searchservice/Create-Index) à l’aide de hello [Azure Search .NET SDK](https://aka.ms/search-sdk).

Avant de suivre ce guide et de passer à la création d’un index, vous devez avoir déjà [créé un service Azure Search](search-create-service-portal.md).

> [!NOTE]
> Tous les exemples de code figurant dans cet article sont écrits en C#. Vous pouvez trouver le code source complet hello [sur GitHub](http://aka.ms/search-dotnet-howto). Vous pouvez également lire sur hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) pour une présentation plus détaillée de l’exemple de code hello.


## <a name="identify-your-azure-search-services-admin-api-key"></a>Identifier la clé API d’administration de votre service Azure Search
Maintenant que vous avez configuré un service Azure Search, vous êtes presque prêt tooissue demandes sur votre point de terminaison de service à l’aide de hello du SDK .NET. Vous devez tout d’abord, tooobtain d'entre hello api-clés d’administration qui a été généré pour le service de recherche hello que vous avez configuré. Hello .NET SDK envoie cette clé d’api sur chaque service tooyour de demande. Avoir une clé valide établit l’approbation, sur une base de chaque demande, entre la demande d’application de hello envoi hello et service hello qui prend en charge.

1. toofind les clés de votre service api, connectez-vous toohello [portail Azure](https://portal.azure.com/)
2. Panneau du service tooyour accédez Azure Search
3. Cliquez sur hello icône « Clés »

Votre service comporte à la fois des *clés d’administration* et des *clés de requête*.

* Vos sites principaux et secondaires *clés d’administration* accorder des droits d’accès complets tooall opérations, y compris hello capacité toomanage hello service, créer et supprimer des index, indexeurs et sources de données. Il existe deux clés afin que vous puissiez continuer clé secondaire du hello toouse si vous décidez de tooregenerate hello primary key et vice versa.
* Votre *clés de requête* accorder l’accès en lecture seule tooindexes et des documents, et sont des applications distribuées généralement tooclient qui émettent des demandes de recherche.

Pour des raisons de hello de création d’un index, vous pouvez utiliser votre clé d’administration principal ou secondaire.

<a name="CreateSearchServiceClient"></a>

## <a name="create-an-instance-of-hello-searchserviceclient-class"></a>Créez une instance de hello SearchServiceClient classe
à l’aide de toostart hello Azure Search .NET SDK, vous devez toocreate une instance de hello `SearchServiceClient` classe. Cette classe dispose de plusieurs constructeurs. Hello celui que vous souhaitez prend le nom de votre service de recherche et un `SearchCredentials` objet en tant que paramètres. `SearchCredentials` encapsule votre clé API.

code Hello ci-dessous crée un nouveau `SearchServiceClient` à l’aide des valeurs pour le nom de service de recherche hello et clé d’api qui sont stockés dans le fichier de configuration de l’application hello (`appsettings.json` dans les cas de hello Hello [exemple d’application](http://aka.ms/search-dotnet-howto)) :

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

`SearchServiceClient` a une propriété `Indexes`. Cette propriété fournit toutes les méthodes hello toocreate, liste, mise à jour, ou que vous supprimez les index de recherche de Azure.

> [!NOTE]
> Hello `SearchServiceClient` classe gère le service de recherche de connexions tooyour. Dans tooavoid ordre ouverture trop grand nombre de connexions, vous devez essayer tooshare à une instance unique de `SearchServiceClient` dans votre application, si possible. Ses méthodes est thread-safe tooenable le partage.
> 
> 

<a name="DefineIndex"></a>

## <a name="define-your-azure-search-index"></a>Définir votre index Recherche Azure
Un seul appel toohello `Indexes.Create` méthode crée l’index. Cette méthode prend comme paramètre un objet `Index` qui définit votre index Azure Search. Vous devez toocreate une `Index` de l’objet et l’initialiser comme suit :

1. Ensemble hello `Name` propriété Hello `Index` toohello nom de l’objet de l’index.
2. Ensemble hello `Fields` propriété Hello `Index` tableau tooan de `Field` objets. hello toocreate moyen plus simple de Hello `Field` objets est en appelant hello `FieldBuilder.BuildForType` méthode, en passant une classe de modèle pour le paramètre de type hello. Une classe de modèle a des propriétés qui mappent toohello des champs de l’index. Cela vous permet de toobind des documents à partir de votre tooinstances d’index de recherche de votre classe de modèle.

> [!NOTE]
> Si vous ne prévoyez pas toouse une classe de modèle, vous pouvez toujours définir votre index en créant `Field` directement des objets. Vous pouvez fournir le nom hello du constructeur de toohello champ hello, ainsi que le type de données hello (ou l’analyseur pour les champs de chaîne). Vous pouvez également définir d'autres propriétés comme `IsSearchable`, `IsFilterable`, etc.
>
>

Il est important de conserver votre recherche utilisateur expérience et des besoins à l’esprit lorsque vous concevez votre index en tant que chaque champ doit être attribuée hello [appropriées des propriétés](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Contrôle de ces propriétés qui recherche les fonctionnalités (filtrage, des facettes, le tri de la recherche en texte intégral, etc.) s’appliquent toowhich champs. Pour toute propriété que vous ne définissez pas explicitement, hello `Field` classe par défaut est fonction de recherche correspondante toodisabling hello, sauf si vous activez en particulier.

Dans notre exemple, nous avons nommé notre index « hotels » et nous avons défini nos champs à l’aide d’une classe de modèle. Chaque propriété de classe de modèle hello possède des attributs qui déterminent les comportements associés à la recherche hello du champ correspondant de l’index hello. classe de modèle Hello est défini comme suit :

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// hello SerializePropertyNamesAsCamelCase attribute is defined in hello Azure Search .NET SDK.
// It ensures that Pascal-case property names in hello model class are mapped toocamel-case
// field names in hello index.
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [System.ComponentModel.DataAnnotations.Key]
    [IsFilterable]
    public string HotelId { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public double? BaseRate { get; set; }

    [IsSearchable]
    public string Description { get; set; }

    [IsSearchable]
    [Analyzer(AnalyzerName.AsString.FrLucene)]
    [JsonProperty("description_fr")]
    public string DescriptionFr { get; set; }

    [IsSearchable, IsFilterable, IsSortable]
    public string HotelName { get; set; }

    [IsSearchable, IsFilterable, IsSortable, IsFacetable]
    public string Category { get; set; }

    [IsSearchable, IsFilterable, IsFacetable]
    public string[] Tags { get; set; }

    [IsFilterable, IsFacetable]
    public bool? ParkingIncluded { get; set; }

    [IsFilterable, IsFacetable]
    public bool? SmokingAllowed { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public DateTimeOffset? LastRenovationDate { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public int? Rating { get; set; }

    [IsFilterable, IsSortable]
    public GeographyPoint Location { get; set; }
}
```

Nous avons choisi avec soin les attributs hello pour chaque propriété basée sur la manière dont nous ils seront utilisés dans une application. Par exemple, il est probable que les personnes recherchant hôtels sera intéressés par les correspondances de mots-clés sur hello `description` champ, donc nous pas activer la recherche en texte intégral pour ce champ en ajoutant hello `IsSearchable` attribut toohello `Description` propriété.

Veuillez noter qu’exactement un champ dans l’index de type `string` doit être hello en hello *clé* champ en ajoutant hello `Key` attribut (voir `HotelId` Bonjour à l’exemple ci-dessus).

définition de l’index Hello ci-dessus utilise un analyseur de langage pour hello `description_fr` , car il s’agit de texte Français de toostore prévue. Consultez [rubrique prise en charge du langage hello](https://docs.microsoft.com/rest/api/searchservice/Language-support) , ainsi que de hello correspondant [billet de blog](https://azure.microsoft.com/blog/language-support-in-azure-search/) pour plus d’informations sur les analyseurs de langage.

> [!NOTE]
> Par défaut, nom hello de chaque propriété dans votre classe de modèle est utilisé comme nom de hello du champ correspondant de hello dans les index hello. Si vous souhaitez toomap les noms de champs de cas toocamel de noms de propriété, marquez la classe hello avec hello `SerializePropertyNamesAsCamelCase` attribut. Si vous souhaitez toomap tooa autre nom, vous pouvez utiliser hello `JsonProperty` attribut comme hello `DescriptionFr` propriété ci-dessus. Hello `JsonProperty` attribut est prioritaire sur hello `SerializePropertyNamesAsCamelCase` attribut.
> 
> 

À présent que nous avons défini une classe de modèle, nous pouvons créer une définition d’index très facilement :

```csharp
var definition = new Index()
{
    Name = "hotels",
    Fields = FieldBuilder.BuildForType<Hotel>()
};
```

## <a name="create-hello-index"></a>Créer des index de hello
Maintenant que vous avez initialisé `Index` de l’objet, vous pouvez créer des index de hello simplement en appelant `Indexes.Create` sur votre `SearchServiceClient` objet :

```csharp
serviceClient.Indexes.Create(definition);
```

Pour une demande réussie, méthode hello retourne normalement. S’il existe un problème avec la demande hello comme un paramètre non valide, méthode hello lèvera `CloudException`.

Lorsque vous avez terminé une toodelete index et que vous souhaitez qu’il, appelez uniquement hello `Indexes.Delete` méthode sur votre `SearchServiceClient`. Il s’agit par exemple, comment nous serait supprimer les index de « hôtels » hello :

```csharp
serviceClient.Indexes.Delete("hotels");
```

> [!NOTE]
> exemple de code Hello dans cet article utilise des méthodes synchrones de hello Hello Azure Search .NET SDK pour plus de simplicité. Nous vous recommandons d’utiliser les méthodes asynchrones hello dans vos propres applications tookeep les évolutives et réactives. Par exemple, les exemples ci-dessus, vous pouvez utiliser Bonjour `CreateAsync` et `DeleteAsync` au lieu de `Create` et `Delete`.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Après avoir créé un index Azure Search, vous serez prêt trop[télécharger votre contenu dans les index hello](search-what-is-data-import.md) pour que vous puissiez rechercher vos données.

