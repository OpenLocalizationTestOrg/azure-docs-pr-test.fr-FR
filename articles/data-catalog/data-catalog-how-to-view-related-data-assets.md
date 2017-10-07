---
title: "aaaHow tooview liées à des ressources de données dans Azure Data Catalog | Documents Microsoft"
description: "Cet article explique comment tooview associés à des ressources de données d’une ressource de données sélectionnée dans Azure Data Catalog."
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
ms.openlocfilehash: b69686737070ac563a0318f48e693215c605f90b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-related-data-assets-in-azure-data-catalog"></a><span data-ttu-id="9591b-103">Comment tooview associées à des ressources de données dans Azure Data Catalog ?</span><span class="sxs-lookup"><span data-stu-id="9591b-103">How tooview related data assets in Azure Data Catalog?</span></span>
<span data-ttu-id="9591b-104">Azure Data Catalog vous permet de tooview données actifs tooa connexes sélectionné données actif et affichage des relations entre elles.</span><span class="sxs-lookup"><span data-stu-id="9591b-104">Azure Data Catalog allows you tooview data assets related tooa selected data asset and view relationships between them.</span></span> 

## <a name="supported-data-sources"></a><span data-ttu-id="9591b-105">Sources de données prises en charge</span><span class="sxs-lookup"><span data-stu-id="9591b-105">Supported data sources</span></span> 
<span data-ttu-id="9591b-106">Lorsque vous inscrivez des ressources de données à partir de hello les sources de données suivantes, Azure Data Catalog enregistre automatiquement les métadonnées sur les relations de jointure entre les ressources de données hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="9591b-106">When you register data assets from hello following data sources, Azure Data Catalog automatically registers metadata about join relationships between hello selected data assets.</span></span> 

- <span data-ttu-id="9591b-107">SQL Server</span><span class="sxs-lookup"><span data-stu-id="9591b-107">SQL Server</span></span>
- <span data-ttu-id="9591b-108">Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="9591b-108">Azure SQL Database</span></span>
- <span data-ttu-id="9591b-109">MySQL</span><span class="sxs-lookup"><span data-stu-id="9591b-109">MySQL</span></span>
- <span data-ttu-id="9591b-110">Oracle</span><span class="sxs-lookup"><span data-stu-id="9591b-110">Oracle</span></span>

## <a name="view-related-data-assets"></a><span data-ttu-id="9591b-111">Afficher les ressources de données associées</span><span class="sxs-lookup"><span data-stu-id="9591b-111">View related data assets</span></span>
<span data-ttu-id="9591b-112">ressources de données tooview sont le jeu de données connexes tooa sélectionné, utilisez hello **relations** onglet comme indiqué dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="9591b-112">tooview data assets that are related tooa selected dataset, use hello **Relationships** tab as shown in hello following image:</span></span> 

![Azure Data Catalog - Afficher les ressources de données associées](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

<span data-ttu-id="9591b-114">Dans cet exemple, il existe deux relations pour hello sélectionné **ProductSubcategory** ressource de données :</span><span class="sxs-lookup"><span data-stu-id="9591b-114">In this example, there are two relationships for hello selected **ProductSubcategory** data asset:</span></span> 

- <span data-ttu-id="9591b-115">Colonne ProductSubcategoryID de la table Product de hello a une relation de clé étrangère avec la colonne ProductSubcategoryID de la table ProductSubcategory de hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="9591b-115">ProductSubcategoryID column of hello Product table has a foreign key relationship with ProductSubcategoryID column of hello selected ProductSubcategory table.</span></span> 
- <span data-ttu-id="9591b-116">Colonne ProductCategoryID de table ProductSubCategory de hello a une relation de clé étrangère avec la colonne ProductCategoryID de table ProductCategory de hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="9591b-116">ProductCategoryID column of hello ProductSubCategory table has a foreign key relationship with ProductCategoryID column of hello selected ProductCategory table.</span></span>

> [!NOTE]
> <span data-ttu-id="9591b-117">Notez la direction hello de flèche hello dans l’arborescence de relations hello.</span><span class="sxs-lookup"><span data-stu-id="9591b-117">Notice hello direction of hello arrow in hello relationships tree view.</span></span>  

<span data-ttu-id="9591b-118">toosee plus d’informations, telles que nom complet de hello de colonne de hello, déplacez la souris de hello sur et vous voyez un toohello similaire de fenêtre contextuelle suit l’image :</span><span class="sxs-lookup"><span data-stu-id="9591b-118">toosee more details such as hello fully qualified name of hello column, move hello mouse over and you see a popup similar toohello following image:</span></span> 

![Azure Data Catalog - Menu contextuel Relation](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

<span data-ttu-id="9591b-120">tooinclude des relations entre des ressources qui ont déjà été inscrit, réinscrivez ces ressources.</span><span class="sxs-lookup"><span data-stu-id="9591b-120">tooinclude relationships between assets that have already been registered, re-register those assets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9591b-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9591b-121">Next steps</span></span>
- [<span data-ttu-id="9591b-122">Comment les ressources de données toomanage</span><span class="sxs-lookup"><span data-stu-id="9591b-122">How toomanage data assets</span></span>](data-catalog-how-to-manage.md)
