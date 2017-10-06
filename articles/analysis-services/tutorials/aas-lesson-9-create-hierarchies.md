---
<span data-ttu-id="ab2e1-101">titre : aaa « leçon du didacticiel Azure Analysis Services 9 : créer des hiérarchies | Description de Microsoft Docs » : services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».</span><span class="sxs-lookup"><span data-stu-id="ab2e1-101">title: aaa"Azure Analysis Services tutorial lesson 9: Create hierarchies | Microsoft Docs" description: services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="ab2e1-102">MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 26/05/2017 ms.author : owend</span><span class="sxs-lookup"><span data-stu-id="ab2e1-102">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-9-create-hierarchies"></a><span data-ttu-id="ab2e1-103">Leçon 9 : Créer des hiérarchies</span><span class="sxs-lookup"><span data-stu-id="ab2e1-103">Lesson 9: Create hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="ab2e1-104">Dans cette leçon, vous allez créer des hiérarchies.</span><span class="sxs-lookup"><span data-stu-id="ab2e1-104">In this lesson, you create hierarchies.</span></span> <span data-ttu-id="ab2e1-105">Les hiérarchies sont des groupes de colonnes organisées en niveaux. Par exemple, la hiérarchie Géographie peut comporter des sous-niveaux correspondant à des pays, des régions, des départements et des villes.</span><span class="sxs-lookup"><span data-stu-id="ab2e1-105">Hierarchies are groups of columns arranged in levels; for example, a Geography hierarchy might have sublevels for Country, State, County, and City.</span></span> <span data-ttu-id="ab2e1-106">Les hiérarchies peuvent apparaître séparément des autres colonnes dans une liste de champs à application client de création de rapports, ce qui les rend plus facile pour les clients utilisateurs toonavigate et inclure dans un rapport.</span><span class="sxs-lookup"><span data-stu-id="ab2e1-106">Hierarchies can appear separate from other columns in a reporting client application field list, making them easier for client users toonavigate and include in a report.</span></span> <span data-ttu-id="ab2e1-107">toolearn, voir [hiérarchies](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="ab2e1-107">toolearn more, see [Hierarchies](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span></span>
  
<span data-ttu-id="ab2e1-108">toocreate hiérarchies, utilisez le Générateur de modèles hello dans *vue de diagramme*.</span><span class="sxs-lookup"><span data-stu-id="ab2e1-108">toocreate hierarchies, use hello model designer in *Diagram View*.</span></span> <span data-ttu-id="ab2e1-109">La création et la gestion des hiérarchies ne sont pas prises en charge dans la vue de données.</span><span class="sxs-lookup"><span data-stu-id="ab2e1-109">Creating and managing hierarchies is not supported in Data View.</span></span>  
  
<span data-ttu-id="ab2e1-110">Estimé temps toocomplete cette leçon : **20 minutes**</span><span class="sxs-lookup"><span data-stu-id="ab2e1-110">Estimated time toocomplete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="ab2e1-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ab2e1-111">Prerequisites</span></span>  
<span data-ttu-id="ab2e1-112">Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu.</span><span class="sxs-lookup"><span data-stu-id="ab2e1-112">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="ab2e1-113">Avant d’effectuer les tâches de hello dans cette leçon, vous devez avoir terminé les leçon précédente hello : [leçon 8 : créer des perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="ab2e1-113">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>  
  
## <a name="create-hierarchies"></a><span data-ttu-id="ab2e1-114">Créer des hiérarchies</span><span class="sxs-lookup"><span data-stu-id="ab2e1-114">Create hierarchies</span></span>  
  
#### <a name="toocreate-a-category-hierarchy-in-hello-dimproduct-table"></a><span data-ttu-id="ab2e1-115">toocreate une hiérarchie de catégorie dans la table DimProduct de hello</span><span class="sxs-lookup"><span data-stu-id="ab2e1-115">toocreate a Category hierarchy in hello DimProduct table</span></span>  
  
1.  <span data-ttu-id="ab2e1-116">Dans le Concepteur de modèle hello (vue de diagramme), avec le bouton droit hello **DimProduct** table > **créer une hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="ab2e1-116">In hello model designer (diagram view), right-click hello **DimProduct** table > **Create Hierarchy**.</span></span> <span data-ttu-id="ab2e1-117">Une nouvelle hiérarchie apparaît au bas de hello de fenêtre de la table hello.</span><span class="sxs-lookup"><span data-stu-id="ab2e1-117">A new hierarchy appears at hello bottom of hello table window.</span></span> <span data-ttu-id="ab2e1-118">Renommer la hiérarchie de hello **catégorie**.</span><span class="sxs-lookup"><span data-stu-id="ab2e1-118">Rename hello hierarchy **Category**.</span></span>  
  
2.  <span data-ttu-id="ab2e1-119">Cliquez et faites glisser hello **ProductCategoryName** toohello colonne nouvelle **catégorie** hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="ab2e1-119">Click and drag hello **ProductCategoryName** column toohello new **Category** hierarchy.</span></span>  
  
3.  <span data-ttu-id="ab2e1-120">Bonjour **catégorie** hiérarchie, avec le bouton hello **ProductCategoryName** > **renommer**, puis tapez **catégorie**.</span><span class="sxs-lookup"><span data-stu-id="ab2e1-120">In hello **Category** hierarchy, right-click hello **ProductCategoryName** > **Rename**, and then type **Category**.</span></span>  
  
    > [!NOTE]  
    > <span data-ttu-id="ab2e1-121">Si vous renommez une colonne dans une hiérarchie ne renomme pas cette colonne dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="ab2e1-121">Renaming a column in a hierarchy does not rename that column in hello table.</span></span> <span data-ttu-id="ab2e1-122">Une colonne dans une hiérarchie est simplement une représentation sous forme de colonne hello dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="ab2e1-122">A column in a hierarchy is just a representation of hello column in hello table.</span></span>  
  
4.  <span data-ttu-id="ab2e1-123">Cliquez et faites glisser hello **ProductSubcategoryName** colonne toohello **catégorie** hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="ab2e1-123">Click and drag hello **ProductSubcategoryName** column toohello **Category** hierarchy.</span></span> <span data-ttu-id="ab2e1-124">Renommez cette colonne **Sous-catégorie**.</span><span class="sxs-lookup"><span data-stu-id="ab2e1-124">Rename it **Subcategory**.</span></span> 
  
5.  <span data-ttu-id="ab2e1-125">Avec le bouton hello **ModelName** colonne > **ajouter toohierarchy**, puis sélectionnez **catégorie**.</span><span class="sxs-lookup"><span data-stu-id="ab2e1-125">Right-click hello **ModelName** column > **Add toohierarchy**, and then select **Category**.</span></span> <span data-ttu-id="ab2e1-126">Renommez cette colonne **Modèle**.</span><span class="sxs-lookup"><span data-stu-id="ab2e1-126">Rename it **Model**.</span></span>

6.  <span data-ttu-id="ab2e1-127">Enfin, ajoutez **EnglishProductName** toohello hiérarchie de catégorie.</span><span class="sxs-lookup"><span data-stu-id="ab2e1-127">Finally, add **EnglishProductName** toohello Category hierarchy.</span></span> <span data-ttu-id="ab2e1-128">Renommez cette colonne **Produit**.</span><span class="sxs-lookup"><span data-stu-id="ab2e1-128">Rename it **Product**.</span></span>  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="toocreate-hierarchies-in-hello-dimdate-table"></a><span data-ttu-id="ab2e1-130">hiérarchies toocreate dans la table DimDate de hello</span><span class="sxs-lookup"><span data-stu-id="ab2e1-130">toocreate hierarchies in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="ab2e1-131">Bonjour **DimDate** table, créer une hiérarchie nommée **calendrier**.</span><span class="sxs-lookup"><span data-stu-id="ab2e1-131">In hello **DimDate** table, create a hierarchy named **Calendar**.</span></span>  
  
3.  <span data-ttu-id="ab2e1-132">Ajoutez hello suivant des colonnes dans l’ordre :</span><span class="sxs-lookup"><span data-stu-id="ab2e1-132">Add hello following columns in-order:</span></span>

    *  <span data-ttu-id="ab2e1-133">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="ab2e1-133">CalendarYear</span></span>
    *  <span data-ttu-id="ab2e1-134">CalendarSemester</span><span class="sxs-lookup"><span data-stu-id="ab2e1-134">CalendarSemester</span></span>
    *  <span data-ttu-id="ab2e1-135">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="ab2e1-135">CalendarQuarter</span></span>
    *  <span data-ttu-id="ab2e1-136">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="ab2e1-136">MonthCalendar</span></span>
    *  <span data-ttu-id="ab2e1-137">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="ab2e1-137">DayNumberOfMonth</span></span>
    
4.  <span data-ttu-id="ab2e1-138">Bonjour **DimDate** table, créez un **Fiscal** hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="ab2e1-138">In hello **DimDate** table, create a **Fiscal** hierarchy.</span></span> <span data-ttu-id="ab2e1-139">Inclure hello suivant des colonnes dans l’ordre :</span><span class="sxs-lookup"><span data-stu-id="ab2e1-139">Include hello following columns in-order:</span></span>  
  
    *  <span data-ttu-id="ab2e1-140">FiscalYear</span><span class="sxs-lookup"><span data-stu-id="ab2e1-140">FiscalYear</span></span>
    *  <span data-ttu-id="ab2e1-141">FiscalSemester</span><span class="sxs-lookup"><span data-stu-id="ab2e1-141">FiscalSemester</span></span>
    *  <span data-ttu-id="ab2e1-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="ab2e1-142">FiscalQuarter</span></span>
    *  <span data-ttu-id="ab2e1-143">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="ab2e1-143">MonthCalendar</span></span>
    *  <span data-ttu-id="ab2e1-144">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="ab2e1-144">DayNumberOfMonth</span></span>
  
5.  <span data-ttu-id="ab2e1-145">Enfin, dans hello **DimDate** table, créez un **ProductionCalendar** hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="ab2e1-145">Finally, in hello **DimDate** table, create a **ProductionCalendar** hierarchy.</span></span> <span data-ttu-id="ab2e1-146">Inclure hello suivant des colonnes dans l’ordre :</span><span class="sxs-lookup"><span data-stu-id="ab2e1-146">Include hello following columns in-order:</span></span>  
    *  <span data-ttu-id="ab2e1-147">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="ab2e1-147">CalendarYear</span></span>
    *  <span data-ttu-id="ab2e1-148">WeekNumberOfYear</span><span class="sxs-lookup"><span data-stu-id="ab2e1-148">WeekNumberOfYear</span></span>
    *  <span data-ttu-id="ab2e1-149">DayNumberOfWeek</span><span class="sxs-lookup"><span data-stu-id="ab2e1-149">DayNumberOfWeek</span></span>
  
 ## <a name="whats-next"></a><span data-ttu-id="ab2e1-150">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="ab2e1-150">What's next?</span></span>
<span data-ttu-id="ab2e1-151">[Leçon 10 : Créer des partitions](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="ab2e1-151">[Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span> 
  
  
