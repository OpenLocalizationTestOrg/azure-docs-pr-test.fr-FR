---
<span data-ttu-id="37d08-101">titre : aaa « leçon supplémentaire du didacticiel Azure Analysis Services : les lignes de détails | Description de Microsoft Docs » : décrit comment toocreate une Expression de lignes de détail dans hello didacticiel Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="37d08-101">title: aaa"Azure Analysis Services tutorial supplemental lesson: Detail Rows | Microsoft Docs" description: Describes how toocreate a Detail Rows Expression in hello Azure Analysis Services tutorial.</span></span>
<span data-ttu-id="37d08-102">Services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».</span><span class="sxs-lookup"><span data-stu-id="37d08-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="37d08-103">MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 26/05/2017 ms.author : owend</span><span class="sxs-lookup"><span data-stu-id="37d08-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="supplemental-lesson---detail-rows"></a><span data-ttu-id="37d08-104">Leçon supplémentaire – Lignes de détails</span><span class="sxs-lookup"><span data-stu-id="37d08-104">Supplemental lesson - Detail Rows</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="37d08-105">Dans cette leçon supplémentaire, vous utilisez une Expression de lignes de détail personnalisée hello éditeur DAX toodefine.</span><span class="sxs-lookup"><span data-stu-id="37d08-105">In this supplemental lesson, you use hello DAX Editor toodefine a custom Detail Rows Expression.</span></span> <span data-ttu-id="37d08-106">Une Expression de lignes de détail est une propriété sur une mesure, en fournissant aux utilisateurs plus d’informations sur les résultats hello agrégée d’une mesure.</span><span class="sxs-lookup"><span data-stu-id="37d08-106">A Detail Rows Expression is a property on a measure, providing end-users more information about hello aggregated results of a measure.</span></span> 
  
<span data-ttu-id="37d08-107">Estimé temps toocomplete cette leçon : **10 minutes**</span><span class="sxs-lookup"><span data-stu-id="37d08-107">Estimated time toocomplete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="37d08-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="37d08-108">Prerequisites</span></span>  
<span data-ttu-id="37d08-109">Cette rubrique de leçon supplémentaire fait partie d’un didacticiel de modélisation tabulaire.</span><span class="sxs-lookup"><span data-stu-id="37d08-109">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="37d08-110">Avant d’effectuer les tâches de hello dans cette leçon supplémentaire, vous devez avoir terminé toutes les leçons précédentes ou avoir un projet de modèle d’exemple Adventure Works Internet Sales terminé.</span><span class="sxs-lookup"><span data-stu-id="37d08-110">Before performing hello tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span>  
  
## <a name="what-do-we-need-toosolve"></a><span data-ttu-id="37d08-111">Comment nous avons besoin de toosolve ?</span><span class="sxs-lookup"><span data-stu-id="37d08-111">What do we need toosolve?</span></span>
<span data-ttu-id="37d08-112">Examinez les détails hello de votre mesure InternetTotalSales, avant d’ajouter une Expression de lignes de détail.</span><span class="sxs-lookup"><span data-stu-id="37d08-112">Let's look at hello details of our InternetTotalSales measure, before adding a Detail Rows Expression.</span></span>

1.  <span data-ttu-id="37d08-113">Dans SSDT, cliquez sur hello **modèle** menu > **analyser dans Excel** tooopen Excel et créer un tableau croisé dynamique vide.</span><span class="sxs-lookup"><span data-stu-id="37d08-113">In SSDT, click hello **Model** menu > **Analyze in Excel** tooopen Excel and create a blank PivotTable.</span></span>
  
2.  <span data-ttu-id="37d08-114">Dans **PivotTable Fields**, ajouter hello **InternetTotalSales** trop de mesures à partir de la table FactInternetSales de hello**valeurs**, **CalendarYear**à partir de hello DimDate table trop**colonnes**, et **EnglishCountryRegionName** trop**lignes**.</span><span class="sxs-lookup"><span data-stu-id="37d08-114">In **PivotTable Fields**, add hello **InternetTotalSales** measure from hello FactInternetSales table too**Values**, **CalendarYear** from hello DimDate table too**Columns**, and **EnglishCountryRegionName** too**Rows**.</span></span> <span data-ttu-id="37d08-115">Notre tableau croisé dynamique permet à présent nous des résultats agrégés à partir de la mesure de InternetTotalSales hello en régions et l’année.</span><span class="sxs-lookup"><span data-stu-id="37d08-115">Our PivotTable now gives us aggregated results from hello InternetTotalSales measure by regions and year.</span></span> 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. <span data-ttu-id="37d08-117">Bonjour tableau croisé dynamique, double-cliquez sur une valeur agrégée pour une année et un nom de région.</span><span class="sxs-lookup"><span data-stu-id="37d08-117">In hello PivotTable, double-click an aggregated value for a year and a region name.</span></span> <span data-ttu-id="37d08-118">Nous avons double-cliqué valeur hello pour l’Australie et hello ici année 2014.</span><span class="sxs-lookup"><span data-stu-id="37d08-118">Here we double-clicked hello value for Australia and hello year 2014.</span></span> <span data-ttu-id="37d08-119">Cette opération affiche une nouvelle feuille contenant des données dont nous n’avons pas l’utilité.</span><span class="sxs-lookup"><span data-stu-id="37d08-119">A new sheet opens containing data, but not useful data.</span></span>

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
<span data-ttu-id="37d08-121">Ce que nous veut toosee ici est une table contenant des colonnes et lignes de données qui contribuent le résultat toohello agrégée de votre mesure InternetTotalSales.</span><span class="sxs-lookup"><span data-stu-id="37d08-121">What we would like toosee here is a table containing columns and rows of data that contribute toohello aggregated result of our InternetTotalSales measure.</span></span> <span data-ttu-id="37d08-122">toodo que, nous pouvons ajouter une Expression de lignes de détail en tant que propriété de mesure de hello.</span><span class="sxs-lookup"><span data-stu-id="37d08-122">toodo that, we can add a Detail Rows Expression as a property of hello measure.</span></span>

## <a name="add-a-detail-rows-expression"></a><span data-ttu-id="37d08-123">Ajouter une expression de lignes de détail</span><span class="sxs-lookup"><span data-stu-id="37d08-123">Add a Detail Rows Expression</span></span>

#### <a name="toocreate-a-detail-rows-expression"></a><span data-ttu-id="37d08-124">toocreate une Expression de lignes de détail</span><span class="sxs-lookup"><span data-stu-id="37d08-124">toocreate a Detail Rows Expression</span></span> 
  
1. <span data-ttu-id="37d08-125">Dans SSDT, dans la grille de mesures de la table hello FactInternetSales, cliquez sur hello **InternetTotalSales** mesure.</span><span class="sxs-lookup"><span data-stu-id="37d08-125">In SSDT, in hello FactInternetSales table's measure grid, click hello **InternetTotalSales** measure.</span></span> 

2. <span data-ttu-id="37d08-126">Dans **propriétés** > **Expression de lignes de détail**, cliquez sur Bonjour éditeur bouton tooopen Bonjour éditeur DAX.</span><span class="sxs-lookup"><span data-stu-id="37d08-126">In **Properties** > **Detail Rows Expression**, click hello editor button tooopen hello DAX Editor.</span></span>

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. <span data-ttu-id="37d08-128">Dans l’éditeur DAX, entrez hello expression suivante :</span><span class="sxs-lookup"><span data-stu-id="37d08-128">In DAX Editor, enter hello following expression:</span></span>

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    <span data-ttu-id="37d08-129">Cette expression spécifie les noms de colonnes, et les résultats de mesure à partir de la table FactInternetSales de hello et les tables associées sont retournés lorsqu’un utilisateur double-clique sur un résultat agrégé dans un tableau croisé dynamique ou un rapport.</span><span class="sxs-lookup"><span data-stu-id="37d08-129">This expression specifies names, columns, and measure results from hello FactInternetSales table and related tables are returned when a user double-clicks an aggregated result in a PivotTable or report.</span></span>

4. <span data-ttu-id="37d08-130">Dans Excel, supprimer une feuille hello créé à l’étape 3, puis double-cliquez sur une valeur agrégée.</span><span class="sxs-lookup"><span data-stu-id="37d08-130">Back in Excel, delete hello sheet created in Step 3, then double-click an aggregated value.</span></span> <span data-ttu-id="37d08-131">Cette fois, avec une propriété Expression de lignes de détail définie pour la mesure de hello, une nouvelle feuille s’ouvre contenant des données beaucoup plus utiles.</span><span class="sxs-lookup"><span data-stu-id="37d08-131">This time, with a Detail Rows Expression property defined for hello measure, a new sheet opens containing a lot more useful data.</span></span>

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. <span data-ttu-id="37d08-133">Redéployez votre modèle.</span><span class="sxs-lookup"><span data-stu-id="37d08-133">Redeploy your model.</span></span>

  
## <a name="see-also"></a><span data-ttu-id="37d08-134">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="37d08-134">See Also</span></span>  
<span data-ttu-id="37d08-135">[SELECTCOLUMNS, fonction (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span><span class="sxs-lookup"><span data-stu-id="37d08-135">[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span></span>  
[<span data-ttu-id="37d08-136">Leçon supplémentaire – Sécurité dynamique</span><span class="sxs-lookup"><span data-stu-id="37d08-136">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="37d08-137">Leçon supplémentaire – Hiérarchies déséquilibrées</span><span class="sxs-lookup"><span data-stu-id="37d08-137">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
