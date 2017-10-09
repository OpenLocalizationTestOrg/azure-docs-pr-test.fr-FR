---
title: "AAA « perspectives de créer de leçon du didacticiel 8 Azure Analysis Services | Documents Microsoft »"
description: "Décrit comment les perspectives toocreate dans hello projet du didacticiel Azure Analysis Services."
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
ms.openlocfilehash: 25391813e1969ecb22af4d6f9c1ccd8358d812fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-8-create-perspectives"></a><span data-ttu-id="0c913-103">Leçon 8 : Créer des perspectives</span><span class="sxs-lookup"><span data-stu-id="0c913-103">Lesson 8: Create perspectives</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="0c913-104">Dans cette leçon, vous allez créer une perspective de ventes sur Internet.</span><span class="sxs-lookup"><span data-stu-id="0c913-104">In this lesson, you create an Internet Sales perspective.</span></span> <span data-ttu-id="0c913-105">Une perspective correspond à un sous-ensemble visualisable d’un modèle qui fournit des points de vue précis, spécifiques à l’entreprise ou à l’application.</span><span class="sxs-lookup"><span data-stu-id="0c913-105">A perspective defines a viewable subset of a model that provides focused, business-specific, or application-specific viewpoints.</span></span> <span data-ttu-id="0c913-106">Lorsqu’un utilisateur connecte tooa modèle à l’aide d’un point de vue, ils voient uniquement les objets de modèle (tables, colonnes, mesures, hiérarchies et KPI) en tant que champs définis dans cette perspective.</span><span class="sxs-lookup"><span data-stu-id="0c913-106">When a user connects tooa model by using a perspective, they see only those model objects (tables, columns, measures, hierarchies, and KPIs) as fields defined in that perspective.</span></span> <span data-ttu-id="0c913-107">toolearn, voir [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="0c913-107">toolearn more, see [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span></span>
  
<span data-ttu-id="0c913-108">objet de la table DimCustomer hello exclut les Hello perspective Internet Sales que vous créez dans cette leçon.</span><span class="sxs-lookup"><span data-stu-id="0c913-108">hello Internet Sales perspective you create in this lesson excludes hello DimCustomer table object.</span></span> <span data-ttu-id="0c913-109">Lorsque vous créez une perspective qui exclut certains objets de vue, cet objet existe toujours dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="0c913-109">When you create a perspective that excludes certain objects from view, that object still exists in hello model.</span></span> <span data-ttu-id="0c913-110">Cependant, ils ne s’affichent pas dans la liste de champs du client de création de rapports.</span><span class="sxs-lookup"><span data-stu-id="0c913-110">However, it is not visible in a reporting client field list.</span></span> <span data-ttu-id="0c913-111">Les colonnes et les mesures calculées, qu’elles soient ou non incluses dans une perspective, peuvent toujours effectuer des calculs à partir des données des objets exclus.</span><span class="sxs-lookup"><span data-stu-id="0c913-111">Calculated columns and measures either included in a perspective or not can still calculate from object data that is excluded.</span></span>  
  
<span data-ttu-id="0c913-112">objectif Hello de cette leçon est toodescribe comment toocreate perspectives et vous familiariser avec les outils de création du modèle tabulaire hello.</span><span class="sxs-lookup"><span data-stu-id="0c913-112">hello purpose of this lesson is toodescribe how toocreate perspectives and become familiar with hello tabular model authoring tools.</span></span> <span data-ttu-id="0c913-113">Si vous développez ultérieurement des tables supplémentaires cette tooinclude modèle, vous pouvez créer des perspectives supplémentaires toodefine différents points de vue du modèle de hello, par exemple, l’inventaire et les ventes.</span><span class="sxs-lookup"><span data-stu-id="0c913-113">If you later expand this model tooinclude additional tables, you can create additional perspectives toodefine different viewpoints of hello model, for example, Inventory and Sales.</span></span>  
  
<span data-ttu-id="0c913-114">Estimé temps toocomplete cette leçon : **cinq minutes**</span><span class="sxs-lookup"><span data-stu-id="0c913-114">Estimated time toocomplete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="0c913-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0c913-115">Prerequisites</span></span>  
<span data-ttu-id="0c913-116">Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu.</span><span class="sxs-lookup"><span data-stu-id="0c913-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="0c913-117">Avant d’effectuer les tâches de hello dans cette leçon, vous devez avoir terminé les leçon précédente hello : [leçon 7 : créer des indicateurs de Performance clés](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="0c913-117">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  
  
## <a name="create-perspectives"></a><span data-ttu-id="0c913-118">Créer des perspectives</span><span class="sxs-lookup"><span data-stu-id="0c913-118">Create perspectives</span></span>  
  
#### <a name="toocreate-an-internet-sales-perspective"></a><span data-ttu-id="0c913-119">toocreate une perspective Internet Sales</span><span class="sxs-lookup"><span data-stu-id="0c913-119">toocreate an Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="0c913-120">Cliquez sur hello **modèle** menu > **Perspectives** > **créer et gérer**.</span><span class="sxs-lookup"><span data-stu-id="0c913-120">Click hello **Model** menu > **Perspectives** > **Create and Manage**.</span></span>  
  
2.  <span data-ttu-id="0c913-121">Bonjour **Perspectives** boîte de dialogue, cliquez sur **nouvelle Perspective**.</span><span class="sxs-lookup"><span data-stu-id="0c913-121">In hello **Perspectives** dialog box, click **New Perspective**.</span></span>  
  
3.  <span data-ttu-id="0c913-122">Double-cliquez sur hello **nouvelle Perspective** en-tête de colonne, puis renommez **Internet Sales**.</span><span class="sxs-lookup"><span data-stu-id="0c913-122">Double-click hello **New Perspective** column heading, and then rename **Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="0c913-123">Sélectionnez hello toutes les tables hello *sauf* **DimCustomer**.</span><span class="sxs-lookup"><span data-stu-id="0c913-123">Select hello all hello tables *except* **DimCustomer**.</span></span>  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    <span data-ttu-id="0c913-125">Dans une prochaine leçon, vous utilisez hello analyser dans Excel fonctionnalité tootest cette perspective.</span><span class="sxs-lookup"><span data-stu-id="0c913-125">In a later lesson, you use hello Analyze in Excel feature tootest this perspective.</span></span> <span data-ttu-id="0c913-126">Hello liste de champs de tableau croisé dynamique Excel inclut chaque table sauf la table DimCustomer de hello.</span><span class="sxs-lookup"><span data-stu-id="0c913-126">hello Excel PivotTable Fields List includes each table except hello DimCustomer table.</span></span>  

## <a name="whats-next"></a><span data-ttu-id="0c913-127">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="0c913-127">What's next?</span></span>
<span data-ttu-id="0c913-128">[Leçon 9 : Créer des hiérarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="0c913-128">[Lesson 9: Create hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>
  
  
  
  
