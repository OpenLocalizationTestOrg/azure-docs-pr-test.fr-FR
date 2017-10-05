---
title: "Guide pratique pour afficher les ressources de données associées dans Azure Data Catalog | Microsoft Docs"
description: "Cet article explique comment afficher les ressources de données associées à la ressource de données sélectionnée dans Azure Data Catalog."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: d45f2cabe712a7982f99a9d280fed4494fc4d377
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-view-related-data-assets-in-azure-data-catalog"></a><span data-ttu-id="61aba-103">Comment afficher les ressources de données associées dans Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="61aba-103">How to view related data assets in Azure Data Catalog?</span></span>
<span data-ttu-id="61aba-104">Azure Data Catalog vous permet d’afficher les ressources de données associées à la ressource de données sélectionnée, ainsi que les relations qui sont établies entre elles.</span><span class="sxs-lookup"><span data-stu-id="61aba-104">Azure Data Catalog allows you to view data assets related to a selected data asset and view relationships between them.</span></span> 

## <a name="supported-data-sources"></a><span data-ttu-id="61aba-105">Sources de données prises en charge</span><span class="sxs-lookup"><span data-stu-id="61aba-105">Supported data sources</span></span> 
<span data-ttu-id="61aba-106">Lorsque vous inscrivez des ressources de données provenant des sources de données suivantes, Azure Data Catalog inscrit automatiquement les métadonnées concernant les relations de jointure qui existent entre les ressources de données sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="61aba-106">When you register data assets from the following data sources, Azure Data Catalog automatically registers metadata about join relationships between the selected data assets.</span></span> 

- <span data-ttu-id="61aba-107">SQL Server</span><span class="sxs-lookup"><span data-stu-id="61aba-107">SQL Server</span></span>
- <span data-ttu-id="61aba-108">Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="61aba-108">Azure SQL Database</span></span>
- <span data-ttu-id="61aba-109">MySQL</span><span class="sxs-lookup"><span data-stu-id="61aba-109">MySQL</span></span>
- <span data-ttu-id="61aba-110">Oracle</span><span class="sxs-lookup"><span data-stu-id="61aba-110">Oracle</span></span>

## <a name="view-related-data-assets"></a><span data-ttu-id="61aba-111">Afficher les ressources de données associées</span><span class="sxs-lookup"><span data-stu-id="61aba-111">View related data assets</span></span>
<span data-ttu-id="61aba-112">Pour afficher les ressources de données associées au jeu de données sélectionné, cliquez sur l’onglet **Relations**, comme illustré ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="61aba-112">To view data assets that are related to a selected dataset, use the **Relationships** tab as shown in the following image:</span></span> 

![Azure Data Catalog - Afficher les ressources de données associées](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

<span data-ttu-id="61aba-114">Dans cet exemple, la ressource de données **ProductSubcategory** a deux relations :</span><span class="sxs-lookup"><span data-stu-id="61aba-114">In this example, there are two relationships for the selected **ProductSubcategory** data asset:</span></span> 

- <span data-ttu-id="61aba-115">La colonne ProductSubcategoryID de la table Product a une relation de clé étrangère avec la colonne ProductSubcategoryID présente dans la table ProductSubcategory sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="61aba-115">ProductSubcategoryID column of the Product table has a foreign key relationship with ProductSubcategoryID column of the selected ProductSubcategory table.</span></span> 
- <span data-ttu-id="61aba-116">La colonne ProductCategoryID de la table ProductSubCategory a une relation de clé étrangère avec la colonne ProductCategoryID présente dans la table ProductCategory sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="61aba-116">ProductCategoryID column of the ProductSubCategory table has a foreign key relationship with ProductCategoryID column of the selected ProductCategory table.</span></span>

> [!NOTE]
> <span data-ttu-id="61aba-117">Remarquez la direction de la flèche dans l’arborescence des relations.</span><span class="sxs-lookup"><span data-stu-id="61aba-117">Notice the direction of the arrow in the relationships tree view.</span></span>  

<span data-ttu-id="61aba-118">Pour plus d’informations, telles que le nom complet de la colonne, déplacez la souris sur la colonne pour afficher une info-bulle semblable à celle-ci :</span><span class="sxs-lookup"><span data-stu-id="61aba-118">To see more details such as the fully qualified name of the column, move the mouse over and you see a popup similar to the following image:</span></span> 

![Azure Data Catalog - Menu contextuel Relation](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

<span data-ttu-id="61aba-120">Pour inclure des relations entre ressources qui ont déjà été inscrites, vous devez réinscrire les ressources.</span><span class="sxs-lookup"><span data-stu-id="61aba-120">To include relationships between assets that have already been registered, re-register those assets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61aba-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="61aba-121">Next steps</span></span>
- [<span data-ttu-id="61aba-122">Gestion des ressources de données</span><span class="sxs-lookup"><span data-stu-id="61aba-122">How to manage data assets</span></span>](data-catalog-how-to-manage.md)