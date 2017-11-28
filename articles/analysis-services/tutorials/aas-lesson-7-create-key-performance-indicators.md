---
<span data-ttu-id="01b8a-101">titre : aaa « leçon du didacticiel Azure Analysis Services 7 : créer des indicateurs de Performance clés | Description de Microsoft Docs » : décrit comment toocreate des indicateurs de Performance clés dans hello projet du didacticiel Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="01b8a-101">title: aaa"Azure Analysis Services tutorial lesson 7: Create Key Performance Indicators | Microsoft Docs" description: Describes how toocreate Key Performance Indicators in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="01b8a-102">Services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».</span><span class="sxs-lookup"><span data-stu-id="01b8a-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="01b8a-103">MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 26/05/2017 ms.author : owend</span><span class="sxs-lookup"><span data-stu-id="01b8a-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-7-create-key-performance-indicators"></a><span data-ttu-id="01b8a-104">Leçon 7 : Créer des indicateurs de performance clés</span><span class="sxs-lookup"><span data-stu-id="01b8a-104">Lesson 7: Create Key Performance Indicators</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="01b8a-105">Dans cette leçon, vous allez créer des indicateurs de performance clés (KPI).</span><span class="sxs-lookup"><span data-stu-id="01b8a-105">In this lesson, you create Key Performance Indicators (KPIs).</span></span> <span data-ttu-id="01b8a-106">Indicateurs de performance clés sont utilisées toogauge les performances d’une valeur définie par un *Base* mesure, par rapport à un *cible* valeur également définie par une mesure ou par une valeur absolue.</span><span class="sxs-lookup"><span data-stu-id="01b8a-106">KPIs are used toogauge performance of a value defined by a *Base* measure, against a *Target* value also defined by a measure, or by an absolute value.</span></span> <span data-ttu-id="01b8a-107">Dans les applications clientes de création de rapports, indicateurs de performance clés offrent aux professionnels un toounderstand rapidement et facilement un résumé des tendances de réussite ou tooidentify business.</span><span class="sxs-lookup"><span data-stu-id="01b8a-107">In reporting client applications, KPIs can provide business professionals a quick and easy way toounderstand a summary of business success or tooidentify trends.</span></span> <span data-ttu-id="01b8a-108">toolearn, voir [indicateurs de performance clés](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="01b8a-108">toolearn more, see [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span></span>
  
<span data-ttu-id="01b8a-109">Estimé temps toocomplete cette leçon : **15 minutes**</span><span class="sxs-lookup"><span data-stu-id="01b8a-109">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="01b8a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="01b8a-110">Prerequisites</span></span>  
<span data-ttu-id="01b8a-111">Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu.</span><span class="sxs-lookup"><span data-stu-id="01b8a-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="01b8a-112">Avant d’effectuer les tâches de hello dans cette leçon, vous devez avoir terminé les leçon précédente hello : [Leçon 6 : créer des mesures](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="01b8a-112">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>   
  
## <a name="create-key-performance-indicators"></a><span data-ttu-id="01b8a-113">Créer des indicateurs de performance clés (KPI)</span><span class="sxs-lookup"><span data-stu-id="01b8a-113">Create Key Performance Indicators</span></span>  
  
#### <a name="toocreate-an-internetcurrentquartersalesperformance-kpi"></a><span data-ttu-id="01b8a-114">toocreate un KPI InternetCurrentQuarterSalesPerformance</span><span class="sxs-lookup"><span data-stu-id="01b8a-114">toocreate an InternetCurrentQuarterSalesPerformance KPI</span></span>  
  
1.  <span data-ttu-id="01b8a-115">Dans le Concepteur de modèle hello, cliquez sur hello **FactInternetSales** table.</span><span class="sxs-lookup"><span data-stu-id="01b8a-115">In hello model designer, click hello **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="01b8a-116">Dans la grille de mesures hello, cliquez sur une cellule vide.</span><span class="sxs-lookup"><span data-stu-id="01b8a-116">In hello measure grid, click an empty cell.</span></span>  
  
3.  <span data-ttu-id="01b8a-117">Dans la barre de formule hello, au-dessus de table de hello, tapez hello formule suivante :</span><span class="sxs-lookup"><span data-stu-id="01b8a-117">In hello formula bar, above hello table, type hello following formula:</span></span> 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    <span data-ttu-id="01b8a-118">Cette mesure sert de mesure de Base hello pour hello indicateur de performance clé.</span><span class="sxs-lookup"><span data-stu-id="01b8a-118">This measure serves as hello Base measure for hello KPI.</span></span>  
  
4.  <span data-ttu-id="01b8a-119">Cliquez avec le bouton droit sur **InternetCurrentQuarterSalesPerformance** > **Créer un KPI**.</span><span class="sxs-lookup"><span data-stu-id="01b8a-119">Right-click **InternetCurrentQuarterSalesPerformance** > **Create KPI**.</span></span>   
  
5.  <span data-ttu-id="01b8a-120">Dans la boîte de dialogue indicateur de Performance clé (KPI) hello dans **cible** sélectionnez **valeur absolue**, puis tapez **1.1**.</span><span class="sxs-lookup"><span data-stu-id="01b8a-120">In hello Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.1**.</span></span>  
  
7.  <span data-ttu-id="01b8a-121">Dans le champ de gauche (bas) du curseur hello, tapez **1**, puis dans le curseur de hello droit (élevé), tapez **1.07**.</span><span class="sxs-lookup"><span data-stu-id="01b8a-121">In hello left (low) slider field, type **1**, and then in hello right (high) slider field, type **1.07**.</span></span>  
  
8.  <span data-ttu-id="01b8a-122">Dans **sélectionner le Style d’icône**, sélectionnez le triangle de losange (rouge), hello (jaune), cercle de type d’icône (vert).</span><span class="sxs-lookup"><span data-stu-id="01b8a-122">In **Select Icon Style**, select hello diamond (red), triangle (yellow), circle (green) icon type.</span></span>
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > <span data-ttu-id="01b8a-124">Hello avis extensible **Descriptions** étiquette au-dessous des styles d’icône disponibles hello.</span><span class="sxs-lookup"><span data-stu-id="01b8a-124">Notice hello expandable **Descriptions** label below hello available icon styles.</span></span> <span data-ttu-id="01b8a-125">Utilisez les descriptions de hello toomake d’éléments différents indicateurs de performance clés les plus identifiable dans les applications clientes.</span><span class="sxs-lookup"><span data-stu-id="01b8a-125">Use descriptions for hello various KPI elements toomake them more identifiable in client applications.</span></span>  
  
9. <span data-ttu-id="01b8a-126">Cliquez sur **OK** toocomplete hello indicateur de performance clé.</span><span class="sxs-lookup"><span data-stu-id="01b8a-126">Click **OK** toocomplete hello KPI.</span></span>  
  
    <span data-ttu-id="01b8a-127">Dans la grille de mesures hello, notez toohello suivante icône de hello **InternetCurrentQuarterSalesPerformance** mesure.</span><span class="sxs-lookup"><span data-stu-id="01b8a-127">In hello measure grid, notice hello icon next toohello **InternetCurrentQuarterSalesPerformance** measure.</span></span> <span data-ttu-id="01b8a-128">Cette icône indique que cette mesure sert de valeur de base pour un indicateur KPI.</span><span class="sxs-lookup"><span data-stu-id="01b8a-128">This icon indicates that this measure serves as a Base value for a KPI.</span></span>  
  
#### <a name="toocreate-an-internetcurrentquartermarginperformance-kpi"></a><span data-ttu-id="01b8a-129">toocreate un KPI InternetCurrentQuarterMarginPerformance</span><span class="sxs-lookup"><span data-stu-id="01b8a-129">toocreate an InternetCurrentQuarterMarginPerformance KPI</span></span>  
  
1.  <span data-ttu-id="01b8a-130">Dans la grille de mesures hello pour hello **FactInternetSales** , cliquez sur une cellule vide.</span><span class="sxs-lookup"><span data-stu-id="01b8a-130">In hello measure grid for hello **FactInternetSales** table, click an empty cell.</span></span>  
  
2.  <span data-ttu-id="01b8a-131">Dans la barre de formule hello, au-dessus de table de hello, tapez hello formule suivante :</span><span class="sxs-lookup"><span data-stu-id="01b8a-131">In hello formula bar, above hello table, type hello following formula:</span></span>  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  <span data-ttu-id="01b8a-132">Cliquez avec le bouton droit sur **InternetCurrentQuarterMarginPerformance** > **Créer un KPI**.</span><span class="sxs-lookup"><span data-stu-id="01b8a-132">Right-click **InternetCurrentQuarterMarginPerformance** > **Create KPI**.</span></span>  
  
4.  <span data-ttu-id="01b8a-133">Dans la boîte de dialogue indicateur de Performance clé (KPI) hello dans **cible** sélectionnez **valeur absolue**, puis tapez **1.25**.</span><span class="sxs-lookup"><span data-stu-id="01b8a-133">In hello Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.25**.</span></span>   
  
5.  <span data-ttu-id="01b8a-134">Dans le champ de gauche (bas) du curseur hello, faites glisser jusqu'à ce que le champ de hello affiche **0,8**, et puis hello de diapositive avec le bouton droit champ de curseur (élevé), jusqu'à ce que le champ de hello affiche **1.03**.</span><span class="sxs-lookup"><span data-stu-id="01b8a-134">In hello left (low) slider field, slide until hello field displays **0.8**, and then slide hello right (high) slider field, until hello field displays **1.03**.</span></span>  
  
6.  <span data-ttu-id="01b8a-135">Dans **sélectionner le Style d’icône**, sélectionnez losange hello (rouge), triangle (jaune), type d’icône de cercle (vert), puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="01b8a-135">In **Select Icon Style**, select hello diamond (red), triangle (yellow), circle (green) icon type, and then click **OK**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="01b8a-136">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="01b8a-136">What's next?</span></span>
<span data-ttu-id="01b8a-137">[Leçon 8 : Créer des perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="01b8a-137">[Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>
  
  
