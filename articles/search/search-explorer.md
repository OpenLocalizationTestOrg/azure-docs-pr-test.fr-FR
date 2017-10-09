---
title: "AAA » interroger un index (portail - Azure Search) | Documents Microsoft »"
description: "Émettre une requête de recherche dans l’Explorateur de recherche du portail hello Azure."
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 8e524188-73a7-44db-9e64-ae8bf66b05d3
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 07/10/2017
ms.author: ashmaka
ms.openlocfilehash: 56bab3ef8a66eeb053fbbeb6d322acb6824fb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-hello-azure-portal"></a>Interroger un index Azure Search à l’aide de l’Explorateur de recherche Bonjour portail Azure
> [!div class="op_single_selector"]
> * [Vue d'ensemble](search-query-overview.md)
> * [Portail](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

Cet article vous explique comment tooquery un indexeur Azure Search index à l’aide de **rechercher dans l’Explorateur** Bonjour portail Azure. Vous pouvez utiliser l’Explorateur de recherche toosubmit simple ou complète Lucene requête chaînes tooany existant index dans votre service.

## <a name="open-hello-service-dashboard"></a>Tableau de bord de service hello ouvert
1. Cliquez sur **toutes les ressources** dans la barre saut hello hello à gauche de hello [portail Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).
2. Sélectionnez votre service Recherche Azure.

## <a name="select-an-index"></a>Sélection d’un index

Index hello sélectionnez vous aimeriez toosearch de hello **index** vignette.

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a>Ouverture de l’Explorateur de recherche

Cliquez sur hello barre de recherche de rechercher dans l’Explorateur vignette tooslide hello ouvert et le volet de résultats.

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a>Commencez la recherche

Lorsque vous utilisez hello rechercher dans l’Explorateur, vous pouvez spécifier [des paramètres de requête](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) requête de hello tooformulate.

1. Saisissez une requête dans **Chaîne de requête** puis appuyez sur **Rechercher**. 

   chaîne de requête Hello est automatiquement analysé dans la demande de bon de hello URL toosubmit une demande HTTP hello API REST Azure Search.   
   
   Vous pouvez utiliser n’importe quel valide simple ou complète Lucene syntaxe toocreate hello demande de requête. Hello `*` caractère est recherche vide ou non spécifiée tooan équivalente qui retourne tous les documents dans aucun ordre particulier.

2. Dans **résultats**, résultats de la requête sont présentés au format JSON brut, charge utile de toohello identiques sont retournées dans un corps de réponse HTTP lors de l’émission de demandes par programme.

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a>Étapes suivantes

Hello suivant ressources fournit des exemples et des informations de syntaxe de requête supplémentaires.

 + [Syntaxe de requête simple](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [Syntaxe de requête Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [Exemples de syntaxe de requête Lucene](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [Syntaxe d’expression de filtre OData](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 