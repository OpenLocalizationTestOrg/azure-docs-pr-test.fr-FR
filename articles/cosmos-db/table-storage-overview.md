---
title: "Vue d’ensemble du stockage de table Azure | Microsoft Docs"
description: "Stockez des données structurées dans le cloud à l’aide du stockage de tables Azure, un magasin de données NoSQL."
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fe46d883-7bed-49dd-980e-5c71df36adb3
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/23/2017
ms.author: mimig
ms.openlocfilehash: 9099e90c402185b371495379db943d64fb82cdb8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-table-storage-overview"></a><span data-ttu-id="30b88-103">Vue d’ensemble du stockage de table Azure</span><span class="sxs-lookup"><span data-stu-id="30b88-103">Azure Table storage overview</span></span>

[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="30b88-104">Le Stockage Table Azure est un service qui stocke des données NoSQL structurées dans le cloud, en fournissant une conception sans schéma à un magasin de clés/attributs.</span><span class="sxs-lookup"><span data-stu-id="30b88-104">Azure Table storage is a service that stores structured NoSQL data in the cloud, providing a key/attribute store with a schemaless design.</span></span> <span data-ttu-id="30b88-105">Comme le stockage de tables est sans schéma, il est aisé d’adapter vos données en fonction des besoins de votre application.</span><span class="sxs-lookup"><span data-stu-id="30b88-105">Because Table storage is schemaless, it's easy to adapt your data as the needs of your application evolve.</span></span> <span data-ttu-id="30b88-106">L’accès aux données du Stockage Table est rapide et économique pour de nombreux types d’applications, et généralement moins coûteux que le SQL traditionnel pour des volumes de données similaires.</span><span class="sxs-lookup"><span data-stu-id="30b88-106">Access to Table storage data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span></span>

<span data-ttu-id="30b88-107">Vous pouvez utiliser le Stockage Table pour stocker des jeux de données flexibles, comme des données utilisateur pour des applications Web, des carnets d’adresses, des informations sur les périphériques ou d’autres types de métadonnées requis par votre service.</span><span class="sxs-lookup"><span data-stu-id="30b88-107">You can use Table storage to store flexible datasets like user data for web applications, address books, device information, or other types of metadata your service requires.</span></span> <span data-ttu-id="30b88-108">Vous pouvez stocker un nombre quelconque d'entités dans une table, et un compte de stockage peut contenir un nombre quelconque de tables, jusqu'à la limite de capacité du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="30b88-108">You can store any number of entities in a table, and a storage account may contain any number of tables, up to the capacity limit of the storage account.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

## <a name="next-steps"></a><span data-ttu-id="30b88-109">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="30b88-109">Next steps</span></span>

* <span data-ttu-id="30b88-110">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome et gratuite de Microsoft qui vous permet d’exploiter visuellement les données de Stockage Azure sur Windows, macOS et Linux.</span><span class="sxs-lookup"><span data-stu-id="30b88-110">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

* [<span data-ttu-id="30b88-111">Getting Started with Azure Table Storage in .NET (Prise en main de Stockage Table Azure dans .NET)</span><span class="sxs-lookup"><span data-stu-id="30b88-111">Getting Started with Azure Table Storage in .NET</span></span>](table-storage-how-to-use-dotnet.md)

* <span data-ttu-id="30b88-112">Pour plus d'informations sur les API disponibles, consultez la documentation de référence du service de Table :</span><span class="sxs-lookup"><span data-stu-id="30b88-112">View the Table service reference documentation for complete details about available APIs:</span></span>

    * [<span data-ttu-id="30b88-113">Référence de la bibliothèque cliente de stockage pour .NET</span><span class="sxs-lookup"><span data-stu-id="30b88-113">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)

    * [<span data-ttu-id="30b88-114">Référence d’API REST</span><span class="sxs-lookup"><span data-stu-id="30b88-114">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
