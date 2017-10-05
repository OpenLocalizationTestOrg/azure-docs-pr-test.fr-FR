---
title: "Leçon 7 du didacticiel Azure Analysis Services : Créer des indicateurs de performance clés | Microsoft Docs"
description: "Indique comment créer des indicateurs de performance clés dans le projet du didacticiel Azure Analysis Services."
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
ms.openlocfilehash: d78808421dd5acd907aa9e9000bb3b770a42c061
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-7-create-key-performance-indicators"></a><span data-ttu-id="b7b25-103">Leçon 7 : Créer des indicateurs de performance clés</span><span class="sxs-lookup"><span data-stu-id="b7b25-103">Lesson 7: Create Key Performance Indicators</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="b7b25-104">Dans cette leçon, vous allez créer des indicateurs de performance clés (KPI).</span><span class="sxs-lookup"><span data-stu-id="b7b25-104">In this lesson, you create Key Performance Indicators (KPIs).</span></span> <span data-ttu-id="b7b25-105">Les indicateurs de performance clés (KPI) évaluent la performance d’une valeur, définie par une mesure de *base*, par rapport à une valeur *cible*, également définie par une mesure ou par une valeur absolue.</span><span class="sxs-lookup"><span data-stu-id="b7b25-105">KPIs are used to gauge performance of a value defined by a *Base* measure, against a *Target* value also defined by a measure, or by an absolute value.</span></span> <span data-ttu-id="b7b25-106">Dans les applications clientes de création de rapports, les indicateurs de performance clés offrent aux professionnels un moyen d’obtenir rapidement et aisément un résumé d’un succès commercial ou d’identifier les tendances.</span><span class="sxs-lookup"><span data-stu-id="b7b25-106">In reporting client applications, KPIs can provide business professionals a quick and easy way to understand a summary of business success or to identify trends.</span></span> <span data-ttu-id="b7b25-107">Pour plus d’informations, consultez [Indicateurs de performance clés](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="b7b25-107">To learn more, see [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span></span>
  
<span data-ttu-id="b7b25-108">Durée estimée pour suivre cette leçon : **15 minutes**</span><span class="sxs-lookup"><span data-stu-id="b7b25-108">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="b7b25-109">Prérequis</span><span class="sxs-lookup"><span data-stu-id="b7b25-109">Prerequisites</span></span>  
<span data-ttu-id="b7b25-110">Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu.</span><span class="sxs-lookup"><span data-stu-id="b7b25-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="b7b25-111">Avant d’effectuer les tâches de cette leçon, vous devez avoir suivi la leçon précédente : [Leçon 6 : Créer des mesures](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="b7b25-111">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>   
  
## <a name="create-key-performance-indicators"></a><span data-ttu-id="b7b25-112">Créer des indicateurs de performance clés (KPI)</span><span class="sxs-lookup"><span data-stu-id="b7b25-112">Create Key Performance Indicators</span></span>  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a><span data-ttu-id="b7b25-113">Pour créer un indicateur de performance clé InternetCurrentQuarterSalesPerformance</span><span class="sxs-lookup"><span data-stu-id="b7b25-113">To create an InternetCurrentQuarterSalesPerformance KPI</span></span>  
  
1.  <span data-ttu-id="b7b25-114">Dans le Concepteur de modèles, cliquez sur la table **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="b7b25-114">In the model designer, click the **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="b7b25-115">Dans la grille de mesure, cliquez sur une cellule vide.</span><span class="sxs-lookup"><span data-stu-id="b7b25-115">In the measure grid, click an empty cell.</span></span>  
  
3.  <span data-ttu-id="b7b25-116">Dans la barre de formule située au-dessus de la table, tapez la formule suivante :</span><span class="sxs-lookup"><span data-stu-id="b7b25-116">In the formula bar, above the table, type the following formula:</span></span> 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    <span data-ttu-id="b7b25-117">Cette mesure sert de mesure de base pour l’indicateur de performance clé.</span><span class="sxs-lookup"><span data-stu-id="b7b25-117">This measure serves as the Base measure for the KPI.</span></span>  
  
4.  <span data-ttu-id="b7b25-118">Cliquez avec le bouton droit sur **InternetCurrentQuarterSalesPerformance** > **Créer un KPI**.</span><span class="sxs-lookup"><span data-stu-id="b7b25-118">Right-click **InternetCurrentQuarterSalesPerformance** > **Create KPI**.</span></span>   
  
5.  <span data-ttu-id="b7b25-119">Dans la boîte de dialogue Indicateur de performance clé (KPI), dans **Cible**, sélectionnez **Valeur absolue**, puis tapez **1.1**.</span><span class="sxs-lookup"><span data-stu-id="b7b25-119">In the Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.1**.</span></span>  
  
7.  <span data-ttu-id="b7b25-120">Dans le champ à curseur de gauche (valeurs basses), tapez **1**, puis dans le champ à curseur de droite (valeurs élevées), tapez **1.07**.</span><span class="sxs-lookup"><span data-stu-id="b7b25-120">In the left (low) slider field, type **1**, and then in the right (high) slider field, type **1.07**.</span></span>  
  
8.  <span data-ttu-id="b7b25-121">Dans **Sélectionnez le style d’icône**, sélectionnez le losange (rouge), le triangle (jaune) ou le cercle (vert) comme type d’icône.</span><span class="sxs-lookup"><span data-stu-id="b7b25-121">In **Select Icon Style**, select the diamond (red), triangle (yellow), circle (green) icon type.</span></span>
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > <span data-ttu-id="b7b25-123">Notez l’étiquette extensible **Descriptions** sous les styles d’icônes disponibles.</span><span class="sxs-lookup"><span data-stu-id="b7b25-123">Notice the expandable **Descriptions** label below the available icon styles.</span></span> <span data-ttu-id="b7b25-124">Utilisez les descriptions des différents éléments KPI pour faciliter l’identification de ces derniers dans les applications clientes.</span><span class="sxs-lookup"><span data-stu-id="b7b25-124">Use descriptions for the various KPI elements to make them more identifiable in client applications.</span></span>  
  
9. <span data-ttu-id="b7b25-125">Cliquez sur **OK** pour terminer l’indicateur KPI.</span><span class="sxs-lookup"><span data-stu-id="b7b25-125">Click **OK** to complete the KPI.</span></span>  
  
    <span data-ttu-id="b7b25-126">Dans la grille de mesure, notez l’icône en regard de la mesure **InternetCurrentQuarterSalesPerformance**.</span><span class="sxs-lookup"><span data-stu-id="b7b25-126">In the measure grid, notice the icon next to the **InternetCurrentQuarterSalesPerformance** measure.</span></span> <span data-ttu-id="b7b25-127">Cette icône indique que cette mesure sert de valeur de base pour un indicateur KPI.</span><span class="sxs-lookup"><span data-stu-id="b7b25-127">This icon indicates that this measure serves as a Base value for a KPI.</span></span>  
  
#### <a name="to-create-an-internetcurrentquartermarginperformance-kpi"></a><span data-ttu-id="b7b25-128">Pour créer un indicateur de performance clé InternetCurrentQuarterMarginPerformance</span><span class="sxs-lookup"><span data-stu-id="b7b25-128">To create an InternetCurrentQuarterMarginPerformance KPI</span></span>  
  
1.  <span data-ttu-id="b7b25-129">Dans la grille de mesure de la table **FactInternetSales**, cliquez sur une cellule vide.</span><span class="sxs-lookup"><span data-stu-id="b7b25-129">In the measure grid for the **FactInternetSales** table, click an empty cell.</span></span>  
  
2.  <span data-ttu-id="b7b25-130">Dans la barre de formule située au-dessus de la table, tapez la formule suivante :</span><span class="sxs-lookup"><span data-stu-id="b7b25-130">In the formula bar, above the table, type the following formula:</span></span>  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  <span data-ttu-id="b7b25-131">Cliquez avec le bouton droit sur **InternetCurrentQuarterMarginPerformance** > **Créer un KPI**.</span><span class="sxs-lookup"><span data-stu-id="b7b25-131">Right-click **InternetCurrentQuarterMarginPerformance** > **Create KPI**.</span></span>  
  
4.  <span data-ttu-id="b7b25-132">Dans la boîte de dialogue Indicateur de performance clé (KPI), dans **Cible**, sélectionnez **Valeur absolue**, puis tapez **1.25**.</span><span class="sxs-lookup"><span data-stu-id="b7b25-132">In the Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.25**.</span></span>   
  
5.  <span data-ttu-id="b7b25-133">Dans le champ à curseur de gauche (valeurs basses), faites glisser le curseur jusqu’à ce que le champ affiche **0.8**, puis faites glisser le curseur de droite (valeurs élevées) jusqu’à ce que le champ affiche **1.03**.</span><span class="sxs-lookup"><span data-stu-id="b7b25-133">In the left (low) slider field, slide until the field displays **0.8**, and then slide the right (high) slider field, until the field displays **1.03**.</span></span>  
  
6.  <span data-ttu-id="b7b25-134">Dans **Sélectionnez le style d’icône**, sélectionnez le losange (rouge), le triangle (jaune) ou le cercle (vert) comme type d’icône, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b7b25-134">In **Select Icon Style**, select the diamond (red), triangle (yellow), circle (green) icon type, and then click **OK**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="b7b25-135">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="b7b25-135">What's next?</span></span>
<span data-ttu-id="b7b25-136">[Leçon 8 : Créer des perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="b7b25-136">[Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>
  
  
