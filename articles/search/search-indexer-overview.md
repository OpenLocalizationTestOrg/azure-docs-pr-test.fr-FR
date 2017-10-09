---
title: aaaIndexers dans Azure Search | Documents Microsoft
description: "Analyse de base de données SQL Azure, base de données Azure Cosmos ou données interrogeables tooextract de stockage Azure et remplir un index Azure Search."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 34a7694c-8fd9-46b1-8900-cefdd7236323
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: 6a816252ec5d6032491a12651c05cb1fe77d3d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="indexers-in-azure-search"></a>Indexeurs dans Azure Search
> [!div class="op_single_selector"]
>
> * [Vue d'ensemble](search-indexer-overview.md)
> * [Portail](search-import-data-portal.md)
> * [Azure SQL](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
> * [Azure Cosmos DB](search-howto-index-documentdb.md)
> * [Stockage Blob Azure](search-howto-indexing-azure-blob-storage.md)
> * [Stockage de tables Azure](search-howto-indexing-azure-tables.md)
>
>

Un **indexeur** dans Azure Search est un robot d’indexation qui extrait des données de recherche et les métadonnées à partir de la source de données externe et remplit un index basé sur le champ à des mappages entre les index hello et votre source de données. Cette approche est parfois désignée tooas un modèle d’extraction, car le service de hello extrait des données dans sans que vous ayez toowrite tout code qui exécute un push de données tooan index.

Vous pouvez utiliser un indexeur comme moyen de hello unique pour l’ingestion de données, ou utiliser une combinaison de techniques qui incluent l’utilisation de hello d’un indexeur pour le chargement que quelques champs hello dans votre index.

Vous pouvez exécuter des indexeurs à la demande ou en fonction d’une planification d’actualisation des données périodique qui s’exécute jusqu’à une fois toutes les quinze minutes. Des mises à jour plus fréquentes requièrent un modèle d’émission qui met à jour simultanément les données dans Azure Search et dans votre source de données externe.

## <a name="approaches-for-creating-and-managing-indexers"></a>Méthodes de création et de gestion des indexeurs
Pour les indexeurs mis à la disposition générale tels qu’Azure SQL ou Azure Cosmos DB, vous pouvez créer et gérer les indexeurs à l’aide des méthodes suivantes :

* [Portail &gt; Assistant Importer des données](search-get-started-portal.md)
* [API REST du service](https://msdn.microsoft.com/library/azure/dn946891.aspx)
* [Kit SDK .NET](https://msdn.microsoft.com/library/azure/microsoft.azure.search.iindexersoperations.aspx)

## <a name="basic-configuration-steps"></a>Étapes de configuration de base
Les indexeurs peuvent offrent des fonctionnalités qui sont source de données toohello unique. À cet égard, certains aspects de la configuration de l’indexeur ou de la source de données varient en fonction du type d’indexeur. Toutefois, tous les indexeurs partagent hello même composition de base et la configuration requise. Étapes qui sont tooall common indexeurs sont abordés ci-dessous.

### <a name="step-1-create-an-index"></a>Étape 1 : Création d’un index
Un indexeur automatiser certains ingestion toodata associés de tâches, mais la création d’un index n’est pas un d’eux. Au préalable, vous devez disposer d’un index prédéfini présentant des champs qui correspondent à ceux de votre source de données externe. Pour plus d’informations sur la structuration d’un index, consultez l’article [Create an Index (Azure Search REST API)](https://msdn.microsoft.com/library/azure/dn798941.aspx)(Création d’un index (API REST Azure Search)).

### <a name="step-2-create-a-data-source"></a>Étape 2 : Création d’une source de données
Un indexeur extrait les données d’une **source de données** qui contient des informations telles qu’une chaîne de connexion. Hello les sources de données suivantes est actuellement prises en charge :

* [Base de données SQL Azure ou SQL Server sur une machine virtuelle Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Azure Cosmos DB](search-howto-index-documentdb.md)
* [Stockage d’objets Blob Azure](search-howto-indexing-azure-blob-storage.md), texte tooextract de PDF, documents Office, HTML ou XML utilisé
* [Stockage de tables Azure](search-howto-indexing-azure-tables.md)

Sources de données sont configurés et gérés indépendamment des indexeurs hello les utilisent, ce qui signifie une source de données peut être utilisée par plusieurs tooload d’indexeurs plus d’un index à la fois.

### <a name="step-3create-and-schedule-hello-indexer"></a>Étape 3 : créer et planifier l’indexeur de hello
définition d’indexeur Hello est une construction en spécifiant les index hello, source de données et une planification. Un indexeur peut faire référence à une source de données à partir d’un autre service, tant que cette source de données est de hello même abonnement. Pour plus d’informations sur la structuration d’un indexeur, consultez l’article [Create Indexer (Azure Search REST API)](https://msdn.microsoft.com/library/azure/dn946899.aspx)(Création d’un indexeur (API REST Azure Search)).

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez idée de base hello, étape suivante de hello est tooreview exigences et le type de source de données spécifique tooeach tâches.

* [Base de données SQL Azure ou SQL Server sur une machine virtuelle Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Azure Cosmos DB](search-howto-index-documentdb.md)
* [Stockage d’objets Blob Azure](search-howto-indexing-azure-blob-storage.md), texte tooextract de PDF, documents Office, HTML ou XML utilisé
* [Stockage de tables Azure](search-howto-indexing-azure-tables.md)
* [L’indexation des objets BLOB de volume partagé de cluster à l’aide d’indexeur d’objet Blob de Azure recherche hello](search-howto-index-csv-blobs.md)
* [Indexation d’objets blob JSON avec l’indexeur d’objets blob Recherche Azure](search-howto-index-json-blobs.md)
