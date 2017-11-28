---
title: "Leçon 8 du didacticiel Azure Analysis Services : Créer des perspectives | Microsoft Docs"
description: "Explique comment créer des perspectives dans le projet du didacticiel Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 491500909b0de0360afae45e172e85999d764fe0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-8-create-perspectives"></a><span data-ttu-id="b0238-103">Leçon 8 : Créer des perspectives</span><span class="sxs-lookup"><span data-stu-id="b0238-103">Lesson 8: Create perspectives</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="b0238-104">Dans cette leçon, vous allez créer une perspective de ventes sur Internet.</span><span class="sxs-lookup"><span data-stu-id="b0238-104">In this lesson, you create an Internet Sales perspective.</span></span> <span data-ttu-id="b0238-105">Une perspective correspond à un sous-ensemble visualisable d’un modèle qui fournit des points de vue précis, spécifiques à l’entreprise ou à l’application.</span><span class="sxs-lookup"><span data-stu-id="b0238-105">A perspective defines a viewable subset of a model that provides focused, business-specific, or application-specific viewpoints.</span></span> <span data-ttu-id="b0238-106">Lorsqu’un utilisateur se connecte à un modèle à l’aide d’une perspective, il voit uniquement les objets de modèle (tables, colonnes, mesures, hiérarchies et KPI) comme des champs définis dans cette perspective.</span><span class="sxs-lookup"><span data-stu-id="b0238-106">When a user connects to a model by using a perspective, they see only those model objects (tables, columns, measures, hierarchies, and KPIs) as fields defined in that perspective.</span></span> <span data-ttu-id="b0238-107">Pour plus d’informations, consultez [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="b0238-107">To learn more, see [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span></span>
  
<span data-ttu-id="b0238-108">La perspective Ventes sur Internet que vous créez dans cette leçon exclut l’objet de la table DimCustomer.</span><span class="sxs-lookup"><span data-stu-id="b0238-108">The Internet Sales perspective you create in this lesson excludes the DimCustomer table object.</span></span> <span data-ttu-id="b0238-109">Lorsque vous créez une perspective qui exclut certains objets, ces objets ne sont pas supprimés du modèle.</span><span class="sxs-lookup"><span data-stu-id="b0238-109">When you create a perspective that excludes certain objects from view, that object still exists in the model.</span></span> <span data-ttu-id="b0238-110">Cependant, ils ne s’affichent pas dans la liste de champs du client de création de rapports.</span><span class="sxs-lookup"><span data-stu-id="b0238-110">However, it is not visible in a reporting client field list.</span></span> <span data-ttu-id="b0238-111">Les colonnes et les mesures calculées, qu’elles soient ou non incluses dans une perspective, peuvent toujours effectuer des calculs à partir des données des objets exclus.</span><span class="sxs-lookup"><span data-stu-id="b0238-111">Calculated columns and measures either included in a perspective or not can still calculate from object data that is excluded.</span></span>  
  
<span data-ttu-id="b0238-112">L’objectif de cette leçon est de décrire comment créer des perspectives et de vous familiariser avec les outils de création de modèles tabulaires.</span><span class="sxs-lookup"><span data-stu-id="b0238-112">The purpose of this lesson is to describe how to create perspectives and become familiar with the tabular model authoring tools.</span></span> <span data-ttu-id="b0238-113">Si vous décidez plus tard d’ajouter des tables à ce modèle, vous pourrez créer des perspectives supplémentaires pour définir les différents points de vue du modèle, tels que l’inventaire et les ventes.</span><span class="sxs-lookup"><span data-stu-id="b0238-113">If you later expand this model to include additional tables, you can create additional perspectives to define different viewpoints of the model, for example, Inventory and Sales.</span></span>  
  
<span data-ttu-id="b0238-114">Durée estimée pour suivre cette leçon : **5 minutes**</span><span class="sxs-lookup"><span data-stu-id="b0238-114">Estimated time to complete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="b0238-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b0238-115">Prerequisites</span></span>  
<span data-ttu-id="b0238-116">Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu.</span><span class="sxs-lookup"><span data-stu-id="b0238-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="b0238-117">Avant d’effectuer les tâches de cette leçon, vous devez avoir terminé la leçon précédente : [Leçon 7 : Créer des indicateurs de performance clés](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="b0238-117">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  
  
## <a name="create-perspectives"></a><span data-ttu-id="b0238-118">Créer des perspectives</span><span class="sxs-lookup"><span data-stu-id="b0238-118">Create perspectives</span></span>  
  
#### <a name="to-create-an-internet-sales-perspective"></a><span data-ttu-id="b0238-119">Pour créer une perspective de ventes sur Internet</span><span class="sxs-lookup"><span data-stu-id="b0238-119">To create an Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="b0238-120">Cliquez sur le menu **Modèle** > **Perspectives** > **Créer et gérer**.</span><span class="sxs-lookup"><span data-stu-id="b0238-120">Click the **Model** menu > **Perspectives** > **Create and Manage**.</span></span>  
  
2.  <span data-ttu-id="b0238-121">Dans la boîte de dialogue **Perspectives**, cliquez sur **Nouvelle perspective**.</span><span class="sxs-lookup"><span data-stu-id="b0238-121">In the **Perspectives** dialog box, click **New Perspective**.</span></span>  
  
3.  <span data-ttu-id="b0238-122">Double-cliquez sur l’en-tête de colonne **Nouvelle perspective**, puis renommez-le **Ventes sur Internet**.</span><span class="sxs-lookup"><span data-stu-id="b0238-122">Double-click the **New Perspective** column heading, and then rename **Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="b0238-123">Sélectionnez toutes les tables *sauf* **DimCustomer**.</span><span class="sxs-lookup"><span data-stu-id="b0238-123">Select the all the tables *except* **DimCustomer**.</span></span>  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    <span data-ttu-id="b0238-125">Dans une leçon ultérieure, vous allez utiliser la fonctionnalité Analyser dans Excel pour tester cette perspective.</span><span class="sxs-lookup"><span data-stu-id="b0238-125">In a later lesson, you use the Analyze in Excel feature to test this perspective.</span></span> <span data-ttu-id="b0238-126">La liste de champs du tableau croisé dynamique Excel inclut toutes les tables, à l’exception de la table DimCustomer.</span><span class="sxs-lookup"><span data-stu-id="b0238-126">The Excel PivotTable Fields List includes each table except the DimCustomer table.</span></span>  

## <a name="whats-next"></a><span data-ttu-id="b0238-127">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="b0238-127">What's next?</span></span>
<span data-ttu-id="b0238-128">[Leçon 9 : Créer des hiérarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="b0238-128">[Lesson 9: Create hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>
  
  
  
  
