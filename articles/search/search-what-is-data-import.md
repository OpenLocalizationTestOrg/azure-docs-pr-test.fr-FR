---
title: "téléchargement aaaData dans Azure Search | Documents Microsoft"
description: "Découvrez comment tooupload données tooan d’index dans Azure Search."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: aa8d47c1-4ae6-4209-a8ce-48d5a9474707
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: ashmaka
ms.openlocfilehash: a95eae94f72c1d0926804ff7e1152f21773fcabf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search"></a>Télécharger des données tooAzure recherche
> [!div class="op_single_selector"]
> * [Vue d'ensemble](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
> 
> 

Il existe deux façons toopopulate un index avec vos données. option de première Hello repousse manuellement vos données dans les index hello à l’aide de hello Azure Search [API REST](search-import-data-rest-api.md) ou [.NET SDK](search-import-data-dotnet.md). deuxième option de Hello est trop[pointez une source de données pris en charge](search-indexer-overview.md) tooyour d’index et permettent d’extraire automatiquement les données de salutation Azure Search.

## <a name="push-data-tooan-index"></a>Index de tooan données push
Cette approche fait référence tooprogrammatically envoyer votre toomake de recherche de données tooAzure disponibles pour la recherche. Pour les applications ayant des exigences d’une latence très faible (par exemple, si vous devez rechercher toobe opérations synchronisée avec les bases de données stock dynamique), le modèle d’émission hello est la seule option.

Vous pouvez utiliser hello [API REST](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) ou [.NET SDK](search-import-data-dotnet.md) toopush données tooan index. Il n’existe actuellement aucune prise en charge de l’outil de push de données via le portail de hello.

Cette approche est plus flexible que le modèle d’extraction hello, car vous pouvez télécharger des documents individuellement ou par lots (les too1000 par lot ou 16 Mo, quelle que soit la limite en premier). modèle d’émission Hello vous permet également de tooupload documents tooAzure recherche quel que soit l’endroit où vos données sont.

format de données Hello compris par Azure Search est JSON, et tous les documents dans le jeu de données hello doivent avoir des champs qui mappent toofields définis dans votre schéma d’index. 

## <a name="pull-data-into-an-index"></a>Extraire des données dans un index
modèle d’extraction Hello analyse d’une source de données pris en charge et télécharge automatiquement les données de salutation dans votre index. Dans Azure Search, cette fonctionnalité est implémentée via des *indexeurs*, actuellement disponibles pour le [stockage d’objets blob](search-howto-indexing-azure-blob-storage.md), le [stockage de tables](search-howto-indexing-azure-tables.md), [Azure Cosmos DB](http://aka.ms/documentdb-search-indexer) et la [base de données SQL Azure et SQL Server sur les machines virtuelles Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md). 

Les indexeurs connecter à une source de données tooa index (généralement une table, vue ou structure équivalente) et mappent les champs de tooequivalent champs source dans les index hello. Pendant l’exécution, ensemble de lignes hello est tooJSON automatiquement transformée et chargées dans l’index spécifié de hello. Tous les indexeurs prend en charge la planification afin que vous pouvez spécifier la fréquence à laquelle les données de salutation sont toobe actualisé. La plupart des indexeurs fournissent le suivi des modifications si la source de données hello prend en charge. Par le suivi des modifications et suppressions tooexisting des documents en outre toorecognizing des documents, indexeurs supprimer la nécessité de hello tooactively gérer les données de salutation dans votre index. 

Fonctionnalité de l’indexeur est exposée dans hello [portail Azure](search-import-data-portal.md), hello [API REST](/rest/api/searchservice/Indexer-operations)et hello [.NET SDK](/dotnet/api/microsoft.azure.search.indexersoperations). 

Un portail de hello toousing avantage est que Azure Search peut générer un schéma d’index par défaut généralement pour vous par la lecture des métadonnées hello du jeu de données source hello. Vous pouvez modifier les index généré hello jusqu'à ce que les index hello est traité, après le hello uniquement les modifications de schéma autorisées sont celles qui ne nécessitent pas la réindexation. Si des modifications de hello souhaitées toomake impact hello schéma directement, vous devez les index de hello toorebuild. 

Une fois les index hello est remplie, vous pouvez utiliser **rechercher dans l’Explorateur** dans la barre de commandes portail hello comme une étape de vérification.

## <a name="query-an-index-using-search-explorer"></a>Interrogation d’un index à l’aide de l’Explorateur de recherche

Un tooperform rapidement une vérification préliminaire lors du téléchargement de document hello est toouse **rechercher dans l’Explorateur** dans le portail de hello. l’Explorateur Hello vous permet d’interroger un index sans avoir toowrite n’importe quel code. expérience de recherche Hello est basée sur les paramètres par défaut, par exemple hello [syntaxe simple](/rest/api/searchservice/simple-query-syntax-in-azure-search) et la valeur par défaut [paramètre de requête searchMode](/rest/api/searchservice/search-documents). Résultats sont retournés au format JSON, afin que vous pouvez inspecter la totalité du document hello.

> [!TIP]
> Nombreuses [exemples de code Azure Search](https://github.com/Azure-Samples/?utf8=%E2%9C%93&query=search) inclure des datasets incorporés ou prête, offre un moyen simple de tooget a démarré. portail de Hello fournit également un indexeur d’exemples et de la source de données composé d’un jeu de données de petite immobilier (nommé « realestate-us-sample »). Lorsque vous exécutez un indexeur préconfigurées de hello sur la source de données exemple hello, un index est créé et chargé avec des documents qui peuvent ensuite être interrogées dans l’Explorateur de recherche ou par le code que vous écrivez.
