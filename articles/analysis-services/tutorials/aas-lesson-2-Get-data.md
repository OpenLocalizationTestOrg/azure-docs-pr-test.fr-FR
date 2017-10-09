---
<span data-ttu-id="5f308-101">titre : aaa « leçon du didacticiel Azure Analysis Services 2 : obtenir les données | Description de Microsoft Docs » : décrit comment tooget et importer des données dans hello projet du didacticiel Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="5f308-101">title: aaa"Azure Analysis Services tutorial lesson 2: Get data | Microsoft Docs" description: Describes how tooget and import data in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="5f308-102">Services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».</span><span class="sxs-lookup"><span data-stu-id="5f308-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="5f308-103">MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 01/06/2017 ms.author : owend</span><span class="sxs-lookup"><span data-stu-id="5f308-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---

# <a name="lesson-2-get-data"></a><span data-ttu-id="5f308-104">Leçon 2 : Obtenir des données</span><span class="sxs-lookup"><span data-stu-id="5f308-104">Lesson 2: Get data</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="5f308-105">Dans cette leçon, vous utilisez obtenir des données dans la base de données exemple tooconnect toohello AdventureWorksDW2014 SSDT, sélectionnez les données, aperçu et filtrer et ensuite importerez dans votre espace de travail modèle.</span><span class="sxs-lookup"><span data-stu-id="5f308-105">In this lesson, you use Get Data in SSDT tooconnect toohello AdventureWorksDW2014 sample database, select data, preview and filter, and then import into your model workspace.</span></span>  
  
<span data-ttu-id="5f308-106">L’option Obtenir des données vous permet d’importer des données à partir d’une grande variété de sources : Azure SQL Database, Oracle, Sybase, flux OData, bases de données Teradata, fichiers, entre autres.</span><span class="sxs-lookup"><span data-stu-id="5f308-106">By using Get Data, you can import data from a wide variety of sources: Azure SQL Database, Oracle, Sybase, OData Feed, Teradata, files and more.</span></span> <span data-ttu-id="5f308-107">Les données peuvent également être interrogées à l’aide d’une expression de formule M Power Query.</span><span class="sxs-lookup"><span data-stu-id="5f308-107">Data can also be queried using a Power Query M formula expression.</span></span>
  
<span data-ttu-id="5f308-108">Estimé temps toocomplete cette leçon : **10 minutes**</span><span class="sxs-lookup"><span data-stu-id="5f308-108">Estimated time toocomplete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="5f308-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5f308-109">Prerequisites</span></span>  
<span data-ttu-id="5f308-110">Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu.</span><span class="sxs-lookup"><span data-stu-id="5f308-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="5f308-111">Avant d’effectuer les tâches de hello dans cette leçon, vous devez avoir terminé les leçon précédente hello : [leçon 1 : créer un projet de modèle tabulaire](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span><span class="sxs-lookup"><span data-stu-id="5f308-111">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 1: Create a new tabular model project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
## <a name="create-a-connection"></a><span data-ttu-id="5f308-112">Créer une connexion</span><span class="sxs-lookup"><span data-stu-id="5f308-112">Create a connection</span></span>  
  
#### <a name="toocreate-a-connection-toohello-adventureworksdw2014-database"></a><span data-ttu-id="5f308-113">toocreate une base de données toohello AdventureWorksDW2014 de connexion</span><span class="sxs-lookup"><span data-stu-id="5f308-113">toocreate a connection toohello AdventureWorksDW2014 database</span></span>  
  
1.  <span data-ttu-id="5f308-114">Dans l’Explorateur de modèles tabulaires, cliquez avec le bouton droit sur **Sources de données** > **Importer à partir de la source de données**.</span><span class="sxs-lookup"><span data-stu-id="5f308-114">In Tabular Model Explorer, right-click **Data Sources** > **Import from Data Source**.</span></span>  
  
    <span data-ttu-id="5f308-115">Obtenir des données, qui vous guide tout au long de source de données tooa connexion démarre.</span><span class="sxs-lookup"><span data-stu-id="5f308-115">This launches Get Data, which guides you through connecting tooa data source.</span></span> <span data-ttu-id="5f308-116">Si vous ne voyez pas dans l’Explorateur de modèles tabulaires, **l’Explorateur de solutions**, double-cliquez sur **Model.bim** modèle de hello tooopen dans le Concepteur de hello.</span><span class="sxs-lookup"><span data-stu-id="5f308-116">If you don't see Tabular Model Explorer, in **Solution Explorer**, double-click **Model.bim** tooopen hello model in hello designer.</span></span> 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  <span data-ttu-id="5f308-118">Dans l’option Obtenir des données, cliquez sur **Base de données** > **Base de données SQL Server** > **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="5f308-118">In Get Data, click **Database** > **SQL Server Database** > **Connect**.</span></span>  
  
3.  <span data-ttu-id="5f308-119">Bonjour **base de données SQL Server** boîte de dialogue, dans **Server**, tapez nom hello du serveur hello où vous avez installé la base de données hello AdventureWorksDW2014, puis cliquez sur **connexion**.</span><span class="sxs-lookup"><span data-stu-id="5f308-119">In hello **SQL Server Database** dialog, in **Server**, type hello name of hello server where you installed hello AdventureWorksDW2014 database, and then click **Connect**.</span></span>  

4.  <span data-ttu-id="5f308-120">Lorsque vous y êtes invité informations d’identification de tooenter, vous avez besoin d’informations d’identification de hello toospecify Analysis Services utilise la source de données toohello tooconnect lors de l’importation et le traitement des données.</span><span class="sxs-lookup"><span data-stu-id="5f308-120">When prompted tooenter credentials, you need toospecify hello credentials Analysis Services uses tooconnect toohello data source when importing and processing data.</span></span> <span data-ttu-id="5f308-121">Dans **Mode d’emprunt d’identité**, sélectionnez **Emprunter l’identité du compte**, entrez les informations d’identification, puis cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="5f308-121">In **Impersonation Mode**, select **Impersonate Account**, then enter credentials, and then click **Connect**.</span></span> <span data-ttu-id="5f308-122">Il est recommandé de qu'utiliser un compte dans lequel le mot de passe hello n’expire jamais.</span><span class="sxs-lookup"><span data-stu-id="5f308-122">It's recommended you use an account where hello password doesn't expire.</span></span>

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > <span data-ttu-id="5f308-124">À l’aide d’un compte d’utilisateur Windows et un mot de passe fournit la méthode la plus sûre de hello connexion tooa de source de données.</span><span class="sxs-lookup"><span data-stu-id="5f308-124">Using a Windows user account and password provides hello most secure method of connecting tooa data source.</span></span>
  
5.  <span data-ttu-id="5f308-125">Dans le navigateur, sélectionnez hello **AdventureWorksDW2014** de base de données, puis cliquez sur **OK**. Cela crée la base de données toohello hello connexion.</span><span class="sxs-lookup"><span data-stu-id="5f308-125">In Navigator, select hello **AdventureWorksDW2014** database, and then click **OK**.This creates hello connection toohello database.</span></span> 
  
6.  <span data-ttu-id="5f308-126">Dans le navigateur, sélectionnez hello case à cocher pour hello les tableaux suivants : **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**,  **DimProductCategory**, **DimProductSubcategory**, et **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="5f308-126">In Navigator, select hello check box for hello following tables: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales**.</span></span>  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
<span data-ttu-id="5f308-128">Après que vous avez cliqué sur OK, l’éditeur de requête s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="5f308-128">After you click OK, Query Editor opens.</span></span> <span data-ttu-id="5f308-129">Dans la section suivante de hello, vous sélectionnez uniquement hello données tooimport.</span><span class="sxs-lookup"><span data-stu-id="5f308-129">In hello next section, you select only hello data you want tooimport.</span></span>

  
## <a name="filter-hello-table-data"></a><span data-ttu-id="5f308-130">Filtrer les données de table hello</span><span class="sxs-lookup"><span data-stu-id="5f308-130">Filter hello table data</span></span>  
<span data-ttu-id="5f308-131">Tables dans la base de données exemple hello AdventureWorksDW2014 contiennent des données qui n’est pas nécessaire tooinclude dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="5f308-131">Tables in hello AdventureWorksDW2014 sample database have data that isn't necessary tooinclude in your model.</span></span> <span data-ttu-id="5f308-132">Lorsque cela est possible, vous souhaitez toofilter l’espace de mémoire des données inutiles toosave utilisé par le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="5f308-132">When possible, you want toofilter out unnecessary data toosave in-memory space used by hello model.</span></span> <span data-ttu-id="5f308-133">Filtrer certaines des colonnes hello à partir des tables afin de n'être pas importés dans la base de données hello espace de travail ou base de données model hello après que qu’il a été déployé.</span><span class="sxs-lookup"><span data-stu-id="5f308-133">You filter out some of hello columns from tables so they're not imported into hello workspace database, or hello model database after it has been deployed.</span></span> 
  
#### <a name="toofilter-hello-table-data-before-importing"></a><span data-ttu-id="5f308-134">données de la table hello toofilter avant l’importation</span><span class="sxs-lookup"><span data-stu-id="5f308-134">toofilter hello table data before importing</span></span>  
  
1.  <span data-ttu-id="5f308-135">Dans l’éditeur de requête, sélectionnez hello **DimCustomer** table.</span><span class="sxs-lookup"><span data-stu-id="5f308-135">In Query Editor, select hello **DimCustomer** table.</span></span> <span data-ttu-id="5f308-136">Une vue de la table DimCustomer hello datasource de hello (votre base de données exemple AdventureWorksDWQ2014) s’affiche.</span><span class="sxs-lookup"><span data-stu-id="5f308-136">A view of hello DimCustomer table at hello datasource (your AdventureWorksDWQ2014 sample database) appears.</span></span> 
  
2.  <span data-ttu-id="5f308-137">Effectuez une sélection multiple (Ctrl + clic) de **SpanishEducation**, **FrenchEducation**, **SpanishOccupation** et **FrenchOccupation**. Cliquez avec le bouton droit, puis cliquez sur **Supprimer les colonnes**.</span><span class="sxs-lookup"><span data-stu-id="5f308-137">Multi-select (Ctrl + click) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, then right-click, and then click **Remove Columns**.</span></span> 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    <span data-ttu-id="5f308-139">Valeurs hello pour ces colonnes ne sont pas pertinentes tooInternet analyse des ventes, n’est pas tooimport besoin de ces colonnes.</span><span class="sxs-lookup"><span data-stu-id="5f308-139">Since hello values for these columns are not relevant tooInternet sales analysis, there is no need tooimport these columns.</span></span> <span data-ttu-id="5f308-140">L’élimination des colonnes inutiles permet de réduire la taille de votre modèle et de le rendre plus efficace.</span><span class="sxs-lookup"><span data-stu-id="5f308-140">Eliminating unnecessary columns makes your model smaller and more efficient.</span></span>  
  
4.  <span data-ttu-id="5f308-141">Filtrer hello restant des tables en supprimant hello suivant des colonnes dans chaque table :</span><span class="sxs-lookup"><span data-stu-id="5f308-141">Filter hello remaining tables by removing hello following columns in each table:</span></span>  
    
    <span data-ttu-id="5f308-142">**DimDate**</span><span class="sxs-lookup"><span data-stu-id="5f308-142">**DimDate**</span></span>
    
      |<span data-ttu-id="5f308-143">Colonne</span><span class="sxs-lookup"><span data-stu-id="5f308-143">Column</span></span>|  
      |--------|  
      |<span data-ttu-id="5f308-144">DateKey</span><span class="sxs-lookup"><span data-stu-id="5f308-144">DateKey</span></span>|  
      |<span data-ttu-id="5f308-145">**SpanishDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="5f308-145">**SpanishDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="5f308-146">**FrenchDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="5f308-146">**FrenchDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="5f308-147">**SpanishMonthName**</span><span class="sxs-lookup"><span data-stu-id="5f308-147">**SpanishMonthName**</span></span>|  
      |<span data-ttu-id="5f308-148">**FrenchMonthName**</span><span class="sxs-lookup"><span data-stu-id="5f308-148">**FrenchMonthName**</span></span>|  
  
    <span data-ttu-id="5f308-149">**DimGeography**</span><span class="sxs-lookup"><span data-stu-id="5f308-149">**DimGeography**</span></span>
  
      |<span data-ttu-id="5f308-150">Colonne</span><span class="sxs-lookup"><span data-stu-id="5f308-150">Column</span></span>|  
      |-------------|  
      |<span data-ttu-id="5f308-151">**SpanishCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="5f308-151">**SpanishCountryRegionName**</span></span>|  
      |<span data-ttu-id="5f308-152">**FrenchCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="5f308-152">**FrenchCountryRegionName**</span></span>|  
      |<span data-ttu-id="5f308-153">**IpAddressLocator**</span><span class="sxs-lookup"><span data-stu-id="5f308-153">**IpAddressLocator**</span></span>|  
  
    <span data-ttu-id="5f308-154">**DimProduct**</span><span class="sxs-lookup"><span data-stu-id="5f308-154">**DimProduct**</span></span>
  
      |<span data-ttu-id="5f308-155">Colonne</span><span class="sxs-lookup"><span data-stu-id="5f308-155">Column</span></span>|  
      |-----------|  
      |<span data-ttu-id="5f308-156">**SpanishProductName**</span><span class="sxs-lookup"><span data-stu-id="5f308-156">**SpanishProductName**</span></span>|  
      |<span data-ttu-id="5f308-157">**FrenchProductName**</span><span class="sxs-lookup"><span data-stu-id="5f308-157">**FrenchProductName**</span></span>|  
      |<span data-ttu-id="5f308-158">**FrenchDescription**</span><span class="sxs-lookup"><span data-stu-id="5f308-158">**FrenchDescription**</span></span>|  
      |<span data-ttu-id="5f308-159">**ChineseDescription**</span><span class="sxs-lookup"><span data-stu-id="5f308-159">**ChineseDescription**</span></span>|  
      |<span data-ttu-id="5f308-160">**ArabicDescription**</span><span class="sxs-lookup"><span data-stu-id="5f308-160">**ArabicDescription**</span></span>|  
      |<span data-ttu-id="5f308-161">**HebrewDescription**</span><span class="sxs-lookup"><span data-stu-id="5f308-161">**HebrewDescription**</span></span>|  
      |<span data-ttu-id="5f308-162">**ThaiDescription**</span><span class="sxs-lookup"><span data-stu-id="5f308-162">**ThaiDescription**</span></span>|  
      |<span data-ttu-id="5f308-163">**GermanDescription**</span><span class="sxs-lookup"><span data-stu-id="5f308-163">**GermanDescription**</span></span>|  
      |<span data-ttu-id="5f308-164">**JapaneseDescription**</span><span class="sxs-lookup"><span data-stu-id="5f308-164">**JapaneseDescription**</span></span>|  
      |<span data-ttu-id="5f308-165">**TurkishDescription**</span><span class="sxs-lookup"><span data-stu-id="5f308-165">**TurkishDescription**</span></span>|  
  
    <span data-ttu-id="5f308-166">**DimProductCategory**</span><span class="sxs-lookup"><span data-stu-id="5f308-166">**DimProductCategory**</span></span>
  
      |<span data-ttu-id="5f308-167">Colonne</span><span class="sxs-lookup"><span data-stu-id="5f308-167">Column</span></span>|  
      |--------------------|  
      |<span data-ttu-id="5f308-168">**SpanishProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="5f308-168">**SpanishProductCategoryName**</span></span>|  
      |<span data-ttu-id="5f308-169">**FrenchProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="5f308-169">**FrenchProductCategoryName**</span></span>|  
  
    <span data-ttu-id="5f308-170">**DimProductSubcategory**</span><span class="sxs-lookup"><span data-stu-id="5f308-170">**DimProductSubcategory**</span></span>
  
      |<span data-ttu-id="5f308-171">Colonne</span><span class="sxs-lookup"><span data-stu-id="5f308-171">Column</span></span>|  
      |-----------------------|  
      |<span data-ttu-id="5f308-172">**SpanishProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="5f308-172">**SpanishProductSubcategoryName**</span></span>|  
      |<span data-ttu-id="5f308-173">**FrenchProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="5f308-173">**FrenchProductSubcategoryName**</span></span>|  
  
    <span data-ttu-id="5f308-174">**FactInternetSales**</span><span class="sxs-lookup"><span data-stu-id="5f308-174">**FactInternetSales**</span></span>
  
      |<span data-ttu-id="5f308-175">Colonne</span><span class="sxs-lookup"><span data-stu-id="5f308-175">Column</span></span>|  
      |------------------|  
      |<span data-ttu-id="5f308-176">**OrderDateKey**</span><span class="sxs-lookup"><span data-stu-id="5f308-176">**OrderDateKey**</span></span>|  
      |<span data-ttu-id="5f308-177">**DueDateKey**</span><span class="sxs-lookup"><span data-stu-id="5f308-177">**DueDateKey**</span></span>|  
      |<span data-ttu-id="5f308-178">**ShipDateKey**</span><span class="sxs-lookup"><span data-stu-id="5f308-178">**ShipDateKey**</span></span>|   
  
## <span data-ttu-id="5f308-179"><a name="Import"></a>Importer les tables de hello sélectionnée et les données de la colonne</span><span class="sxs-lookup"><span data-stu-id="5f308-179"><a name="Import"></a>Import hello selected tables and column data</span></span>  
<span data-ttu-id="5f308-180">Maintenant que vous avez prévisualisé et filtré les données inutiles, vous pouvez importer reste hello de données hello souhaités.</span><span class="sxs-lookup"><span data-stu-id="5f308-180">Now that you've previewed and filtered out unnecessary data, you can import hello rest of hello data you do want.</span></span> <span data-ttu-id="5f308-181">Assistant de Hello importe des données de la table hello avec toutes les relations entre les tables.</span><span class="sxs-lookup"><span data-stu-id="5f308-181">hello wizard imports hello table data along with any relationships between tables.</span></span> <span data-ttu-id="5f308-182">Nouvelles tables et colonnes sont créés dans le modèle de hello et les données filtrées n’est pas importé.</span><span class="sxs-lookup"><span data-stu-id="5f308-182">New tables and columns are created in hello model and data that you filtered out is not be imported.</span></span>  
  
#### <a name="tooimport-hello-selected-tables-and-column-data"></a><span data-ttu-id="5f308-183">tooimport hello sélectionné les tables et les données de colonne</span><span class="sxs-lookup"><span data-stu-id="5f308-183">tooimport hello selected tables and column data</span></span>  
  
1.  <span data-ttu-id="5f308-184">Passez en revue vos sélections.</span><span class="sxs-lookup"><span data-stu-id="5f308-184">Review your selections.</span></span> <span data-ttu-id="5f308-185">Si tout semble correct, cliquez sur **Importer**.</span><span class="sxs-lookup"><span data-stu-id="5f308-185">If everything looks okay, click **Import**.</span></span> <span data-ttu-id="5f308-186">boîte de dialogue de traitement des données Hello affiche état hello des données importées à partir de votre source de données dans votre base de données de l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="5f308-186">hello Data Processing dialog shows hello status of data being imported from your datasource into your workspace database.</span></span>
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  <span data-ttu-id="5f308-188">Cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="5f308-188">Click **Close**.</span></span>  

  
## <a name="save-your-model-project"></a><span data-ttu-id="5f308-189">Enregistrer votre projet de modèle</span><span class="sxs-lookup"><span data-stu-id="5f308-189">Save your model project</span></span>  
<span data-ttu-id="5f308-190">Il est important, elles sonttrop enregistrer votre projet de modèle.</span><span class="sxs-lookup"><span data-stu-id="5f308-190">It's important toofrequently save your model project.</span></span>  
  
#### <a name="toosave-hello-model-project"></a><span data-ttu-id="5f308-191">projet de modèle hello toosave</span><span class="sxs-lookup"><span data-stu-id="5f308-191">toosave hello model project</span></span>  
  
-   <span data-ttu-id="5f308-192">Cliquez sur **Fichier** > **Enregistrer tout**.</span><span class="sxs-lookup"><span data-stu-id="5f308-192">Click **File** > **Save All**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="5f308-193">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="5f308-193">What's next?</span></span>
<span data-ttu-id="5f308-194">[Leçon 3 : Marquer en tant que Table de dates](../tutorials/aas-lesson-3-mark-as-date-table.md).</span><span class="sxs-lookup"><span data-stu-id="5f308-194">[Lesson 3: Mark as Date Table](../tutorials/aas-lesson-3-mark-as-date-table.md).</span></span>

  
  
