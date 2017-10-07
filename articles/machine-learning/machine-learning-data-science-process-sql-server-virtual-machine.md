---
title: "aaaExplore des données dans une machine virtuelle de SQL Server sur Azure | Documents Microsoft"
description: "Explorer des données et générer des fonctionnalités dans une machine virtuelle SQL Server sur Azure"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: 
ms.assetid: 3949fb2c-ffab-49fb-908d-27d5e42f743b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 67f4b058b0f6557ee15fd42795c918d68f1a9871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="74e85-103"><a name="heading"></a>Traitement des données d’une machine virtuelle SQL Server sur Azure</span><span class="sxs-lookup"><span data-stu-id="74e85-103"><a name="heading"></a>Process Data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="74e85-104">Ce document décrit comment les données tooexplore et générer des fonctionnalités pour les données stockées dans une machine virtuelle SQL Server sur Azure.</span><span class="sxs-lookup"><span data-stu-id="74e85-104">This document covers how tooexplore data and generate features for data stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="74e85-105">Cela est possible avec le retraitement des données à l'aide de SQL ou en utilisant un langage de programmation comme Python.</span><span class="sxs-lookup"><span data-stu-id="74e85-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

> [!NOTE]
> <span data-ttu-id="74e85-106">Hello exemples d’instructions SQL dans ce document supposent que les données sont dans SQL Server.</span><span class="sxs-lookup"><span data-stu-id="74e85-106">hello sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="74e85-107">Si elle n’est pas le cas, consultez Comment toohello cloud données science processus carte toolearn toomove votre tooSQL de données serveur.</span><span class="sxs-lookup"><span data-stu-id="74e85-107">If it isn't, refer toohello cloud data science process map toolearn how toomove your data tooSQL Server.</span></span>
> 
> 

## <span data-ttu-id="74e85-108"><a name="SQL"></a>Utilisation de SQL</span><span class="sxs-lookup"><span data-stu-id="74e85-108"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="74e85-109">Nous allons décrire hello données batailler avec des tâches de cette section à l’aide de SQL suivantes :</span><span class="sxs-lookup"><span data-stu-id="74e85-109">We describe hello following data wrangling tasks in this section using SQL:</span></span>

1. [<span data-ttu-id="74e85-110">Exploration des données</span><span class="sxs-lookup"><span data-stu-id="74e85-110">Data Exploration</span></span>](#sql-dataexploration)
2. [<span data-ttu-id="74e85-111">Génération de fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="74e85-111">Feature Generation</span></span>](#sql-featuregen)

### <span data-ttu-id="74e85-112"><a name="sql-dataexploration"></a>Exploration des données</span><span class="sxs-lookup"><span data-stu-id="74e85-112"><a name="sql-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="74e85-113">Voici quelques exemples de scripts SQL qui peuvent être utilisés tooexplore des magasins de données dans SQL Server.</span><span class="sxs-lookup"><span data-stu-id="74e85-113">Here are a few sample SQL scripts that can be used tooexplore data stores in SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="74e85-114">Pour obtenir un exemple pratique, vous pouvez utiliser hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) et toohello IPNB intitulée [NYC données ensuivirent à l’aide du bloc-notes de IPython et de SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) pour une procédure pas à pas de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="74e85-114">For a practical example, you can use hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

1. <span data-ttu-id="74e85-115">Obtenir le nombre de hello d’observations par jour</span><span class="sxs-lookup"><span data-stu-id="74e85-115">Get hello count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="74e85-116">Obtenir des niveaux de hello dans une colonne catégorielle</span><span class="sxs-lookup"><span data-stu-id="74e85-116">Get hello levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="74e85-117">Obtenir le nombre hello de niveaux dans la combinaison de deux colonnes catégorielles</span><span class="sxs-lookup"><span data-stu-id="74e85-117">Get hello number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="74e85-118">Obtenir distribution hello pour les colonnes numériques</span><span class="sxs-lookup"><span data-stu-id="74e85-118">Get hello distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <span data-ttu-id="74e85-119"><a name="sql-featuregen"></a>Génération de fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="74e85-119"><a name="sql-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="74e85-120">Dans cette section, nous décrivons plusieurs manières de générer des fonctionnalités via SQL :</span><span class="sxs-lookup"><span data-stu-id="74e85-120">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="74e85-121">Génération de fonctionnalités utilisant des décomptes</span><span class="sxs-lookup"><span data-stu-id="74e85-121">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="74e85-122">Génération de caractéristiques de compartimentage</span><span class="sxs-lookup"><span data-stu-id="74e85-122">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="74e85-123">Déploiement de fonctionnalités de hello à partir d’une seule colonne</span><span class="sxs-lookup"><span data-stu-id="74e85-123">Rolling out hello features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="74e85-124">Une fois que vous générez des fonctionnalités supplémentaires, vous pouvez les ajouter en tant que table de colonnes toohello existante ou créer une table avec des fonctionnalités supplémentaires hello et la clé primaire, ce qui peut être jointe avec la table d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="74e85-124">Once you generate additional features, you can either add them as columns toohello existing table or create a new table with hello additional features and primary key, that can be joined with hello original table.</span></span> 
> 
> 

### <span data-ttu-id="74e85-125"><a name="sql-countfeature"></a>Génération de fonctionnalités utilisant des décomptes</span><span class="sxs-lookup"><span data-stu-id="74e85-125"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="74e85-126">Hello exemples suivants illustrent deux façons de générer des fonctionnalités de nombre.</span><span class="sxs-lookup"><span data-stu-id="74e85-126">hello following examples demonstrate two ways of generating count features.</span></span> <span data-ttu-id="74e85-127">Hello première méthode utilise la somme conditionnelle et utilise deuxième hello hello clause « where ».</span><span class="sxs-lookup"><span data-stu-id="74e85-127">hello first method uses conditional sum and hello second method uses hello 'where' clause.</span></span> <span data-ttu-id="74e85-128">Ils peuvent être joints avec hello d’origine (à l’aide des colonnes de clé primaire) de table toohave nombre des fonctionnalités en même temps que les données d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="74e85-128">These can then be joined with hello original table (using primary key columns) toohave count features alongside hello original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <span data-ttu-id="74e85-129"><a name="sql-binningfeature"></a>Génération de caractéristiques de compartimentage</span><span class="sxs-lookup"><span data-stu-id="74e85-129"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="74e85-130">Hello suivant montre comment toogenerate placées fonctionnalités par compartimentage (à l’aide de cinq emplacements), une colonne numérique qui peut être utilisée en tant que fonctionnalité à la place :</span><span class="sxs-lookup"><span data-stu-id="74e85-130">hello following example shows how toogenerate binned features by binning (using five bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="74e85-131"><a name="sql-featurerollout"></a>Déploiement de fonctionnalités de hello à partir d’une seule colonne</span><span class="sxs-lookup"><span data-stu-id="74e85-131"><a name="sql-featurerollout"></a>Rolling out hello features from a single column</span></span>
<span data-ttu-id="74e85-132">Dans cette section, nous allons montrer comment tooroll à une seule colonne dans une table toogenerate supplémentaire des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="74e85-132">In this section, we demonstrate how tooroll out a single column in a table toogenerate additional features.</span></span> <span data-ttu-id="74e85-133">Hello exemple suppose qu’il existe une colonne de latitude ou de longitude dans la table hello à partir de laquelle vous essayez de toogenerate fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="74e85-133">hello example assumes that there is a latitude or longitude column in hello table from which you are trying toogenerate features.</span></span>

<span data-ttu-id="74e85-134">Voici une brève introduction sur les données d’emplacement latitude/longitude (avec une ressource à partir de stackoverflow [comment toomeasure hello précision de latitude et longitude ?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span><span class="sxs-lookup"><span data-stu-id="74e85-134">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow [How toomeasure hello accuracy of latitude and longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span></span> <span data-ttu-id="74e85-135">Cela est utile toounderstand avant le champ d’emplacement featurizing hello :</span><span class="sxs-lookup"><span data-stu-id="74e85-135">This is useful toounderstand before featurizing hello location field:</span></span>

* <span data-ttu-id="74e85-136">signe de Hello nous indique que nous sont Nord ou sud, est ou ouest globe de hello.</span><span class="sxs-lookup"><span data-stu-id="74e85-136">hello sign tells us whether we are north or south, east or west on hello globe.</span></span>
* <span data-ttu-id="74e85-137">Un chiffre des centaines différent de zéro indique que nous utilisons la longitude, et non la latitude.</span><span class="sxs-lookup"><span data-stu-id="74e85-137">A nonzero hundreds digit tells us that we're using longitude, not latitude!</span></span>
* <span data-ttu-id="74e85-138">les chiffres des dizaines de Hello donne un tooabout position 1 000 kilomètres.</span><span class="sxs-lookup"><span data-stu-id="74e85-138">hello tens digit gives a position tooabout 1,000 kilometers.</span></span> <span data-ttu-id="74e85-139">Il nous fournit des informations utiles sur le continent ou l’océan dans lequel nous nous trouvons.</span><span class="sxs-lookup"><span data-stu-id="74e85-139">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="74e85-140">chiffre des unités Hello (un degré décimale) donne une position de too111 kilomètres (60 milles, environ 69 miles).</span><span class="sxs-lookup"><span data-stu-id="74e85-140">hello units digit (one decimal degree) gives a position up too111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="74e85-141">Il nous permet de déterminer approximativement le département de grande superficie ou le pays dans lequel nous sommes.</span><span class="sxs-lookup"><span data-stu-id="74e85-141">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="74e85-142">première décimale Hello vaut des too11.1 km : elle peut distinguer la position hello d’une ville volumineuse à partir d’une grande ville voisinage.</span><span class="sxs-lookup"><span data-stu-id="74e85-142">hello first decimal place is worth up too11.1 km: it can distinguish hello position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="74e85-143">deuxième décimale Hello vaut des too1.1 km : il peut séparer un village hello ensuite.</span><span class="sxs-lookup"><span data-stu-id="74e85-143">hello second decimal place is worth up too1.1 km: it can separate one village from hello next.</span></span>
* <span data-ttu-id="74e85-144">est intéressant too110 m: Hello troisième décimale, il peut identifier un grand champ agricole ou un campus institutionnel.</span><span class="sxs-lookup"><span data-stu-id="74e85-144">hello third decimal place is worth up too110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="74e85-145">est intéressant too11 m: Hello quatrième décimale, il peut identifier un paquet de terrain.</span><span class="sxs-lookup"><span data-stu-id="74e85-145">hello fourth decimal place is worth up too11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="74e85-146">Il est toohello comparable au niveau de précision classique d’une unité GPS corrigée avec sans interférence.</span><span class="sxs-lookup"><span data-stu-id="74e85-146">It is comparable toohello typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="74e85-147">cinquième décimale Hello vaut des too1.1 m: qu'il arborescences fait la distinction entre eux.</span><span class="sxs-lookup"><span data-stu-id="74e85-147">hello fifth decimal place is worth up too1.1 m: it distinguishes trees from each other.</span></span> <span data-ttu-id="74e85-148">Niveau de toothis de précision avec des unités commerciales GPS ne peut être obtenu avec une correction différentielle.</span><span class="sxs-lookup"><span data-stu-id="74e85-148">Accuracy toothis level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="74e85-149">Hello sixième décimale est intéressant m: too0.11 que vous pouvez l’utiliser pour la disposition des structures en détail, pour la conception des architectures, des routes de génération.</span><span class="sxs-lookup"><span data-stu-id="74e85-149">hello sixth decimal place is worth up too0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="74e85-150">Elle devrait se révéler amplement suffisante pour assurer le suivi des mouvements des glaciers et des rivières.</span><span class="sxs-lookup"><span data-stu-id="74e85-150">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="74e85-151">L’obtention d’une telle précision sur un GPS nécessite l’emploi de mesures rigoureuses, telles qu’une correction différentielle.</span><span class="sxs-lookup"><span data-stu-id="74e85-151">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="74e85-152">informations d’emplacement Hello peuvent être caractéristiques, procédez comme suit séparation des informations sur la ville, l’emplacement et la région.</span><span class="sxs-lookup"><span data-stu-id="74e85-152">hello location information can be featurized as follows, separating out region, location, and city information.</span></span> <span data-ttu-id="74e85-153">Notez que vous pouvez également appeler un point de terminaison REST telles que les API Bing Maps disponible à l’adresse [de trouver un emplacement par Point](https://msdn.microsoft.com/library/ff701710.aspx) informations de région/district tooget hello.</span><span class="sxs-lookup"><span data-stu-id="74e85-153">Note that you can also call a REST end point such as Bing Maps API available at [Find a Location by Point](https://msdn.microsoft.com/library/ff701710.aspx) tooget hello region/district information.</span></span>

    select 
        <location_columnname>
        ,round(<location_columnname>,0) as l1        
        ,l2=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 1 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),1,1) else '0' end     
        ,l3=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 2 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),2,1) else '0' end     
        ,l4=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 3 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),3,1) else '0' end     
        ,l5=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 4 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),4,1) else '0' end     
        ,l6=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 5 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),5,1) else '0' end     
        ,l7=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 6 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),6,1) else '0' end     
    from <tablename>

<span data-ttu-id="74e85-154">Ces fonctionnalités basée sur l’emplacement peuvent être davantage fonctionnalités nombre supplémentaire de toogenerate utilisés comme décrit précédemment.</span><span class="sxs-lookup"><span data-stu-id="74e85-154">These location-based features can be further used toogenerate additional count features as described earlier.</span></span> 

> [!TIP]
> <span data-ttu-id="74e85-155">Vous pouvez insérer par programme des enregistrements de hello à l’aide de la langue de votre choix.</span><span class="sxs-lookup"><span data-stu-id="74e85-155">You can programmatically insert hello records using your language of choice.</span></span> <span data-ttu-id="74e85-156">Vous devrez peut-être les données de salutation tooinsert dans l’efficacité de segments tooimprove écriture (pour obtenir un exemple de procédure toodo cette pyodbc, voir les [A HelloWorld exemple tooaccess SQLServer avec python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span><span class="sxs-lookup"><span data-stu-id="74e85-156">You may need tooinsert hello data in chunks tooimprove write efficiency (for an example of how toodo this using pyodbc, see [A HelloWorld sample tooaccess SQLServer with python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span></span> <span data-ttu-id="74e85-157">Une autre solution consiste à données tooinsert hello de base de données à l’aide de hello [utilitaire BCP](https://msdn.microsoft.com/library/ms162802.aspx).</span><span class="sxs-lookup"><span data-stu-id="74e85-157">Another alternative is tooinsert data in hello database using hello [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx).</span></span>
> 
> 

### <span data-ttu-id="74e85-158"><a name="sql-aml"></a>Connexion tooAzure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="74e85-158"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="74e85-159">Hello généré récemment fonctionnalité peut être ajoutée en tant que colonne tooan existant table stockée dans une nouvelle table et jointe à la table d’origine de hello pour l’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="74e85-159">hello newly generated feature can be added as a column tooan existing table or stored in a new table and joined with hello original table for machine learning.</span></span> <span data-ttu-id="74e85-160">Fonctionnalités peuvent être générées ou accessibles si déjà créé, à l’aide de hello [importer des données] [ import-data] module dans Azure Machine Learning, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="74e85-160">Features can be generated or accessed if already created, using hello [Import Data][import-data] module in Azure Machine Learning as shown below:</span></span>

![lecteurs azureml][1] 

## <span data-ttu-id="74e85-162"><a name="python"></a>Utilisation d’un langage de programmation tel que Python</span><span class="sxs-lookup"><span data-stu-id="74e85-162"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="74e85-163">À l’aide de données de tooexplore Python et générer des fonctionnalités lorsque hello sont de données dans SQL Server est données tooprocessing similaires dans des objets blob Azure à l’aide de Python comme documenté dans [données d’objets Blob Azure de processus dans votre environnement de science des données](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="74e85-163">Using Python tooexplore data and generate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="74e85-164">les données de salutation doit toobe chargé à partir de la base de données hello dans une trame de données pandas et peuvent ensuite être traitées ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="74e85-164">hello data needs toobe loaded from hello database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="74e85-165">Nous processus hello de connexion de base de données toohello et de charger les données de hello de trame de données hello dans cette section de document.</span><span class="sxs-lookup"><span data-stu-id="74e85-165">We document hello process of connecting toohello database and loading hello data into hello data frame in this section.</span></span>

<span data-ttu-id="74e85-166">Hello, suivant le format de chaîne de connexion peut être utilisé tooconnect tooa base de données SQL à partir de Python à l’aide de pyodbc (remplacez servername, dbname, nom d’utilisateur et mot de passe avec les valeurs spécifiques) :</span><span class="sxs-lookup"><span data-stu-id="74e85-166">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="74e85-167">Hello [bibliothèque de Pandas](http://pandas.pydata.org/) dans Python fournit un ensemble complet d’outils d’analyse de données et des structures de données pour la manipulation de données pour la programmation de Python.</span><span class="sxs-lookup"><span data-stu-id="74e85-167">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="74e85-168">code Hello ci-dessous lit hello résultats à partir d’une base de données SQL Server dans une trame de données Pandas :</span><span class="sxs-lookup"><span data-stu-id="74e85-168">hello code below reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="74e85-169">Maintenant que vous pouvez travailler avec la trame de données hello Pandas comme indiqué dans l’article de hello [données d’objets Blob Azure de processus dans votre environnement de science des données](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="74e85-169">Now you can work with hello Pandas data frame as covered in hello article [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="azure-data-science-in-action-example"></a><span data-ttu-id="74e85-170">Exemple de processus de science des données Azure en action</span><span class="sxs-lookup"><span data-stu-id="74e85-170">Azure Data Science in Action Example</span></span>
<span data-ttu-id="74e85-171">Pour obtenir un exemple de procédure pas à pas de bout en bout de hello processus de science des données Azure à l’aide d’un jeu de données public, consultez [processus de science des données Azure dans l’Action](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="74e85-171">For an end-to-end walkthrough example of hello Azure Data Science Process using a public dataset, see [Azure Data Science Process in Action](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

