---
title: "Explorer les données d’une machine virtuelle SQL Server sur Azure | Microsoft Docs"
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
ms.openlocfilehash: 16fabb29bdc8ec770efd843e18e9016e338a8f4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="f7dbf-103"><a name="heading"></a>Traitement des données d’une machine virtuelle SQL Server sur Azure</span><span class="sxs-lookup"><span data-stu-id="f7dbf-103"><a name="heading"></a>Process Data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="f7dbf-104">Ce document décrit l'exploration des données et la génération de fonctionnalités pour les données stockées dans une machine virtuelle SQL Server sur Azure.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-104">This document covers how to explore data and generate features for data stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="f7dbf-105">Cela est possible avec le retraitement des données à l'aide de SQL ou en utilisant un langage de programmation comme Python.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

> [!NOTE]
> <span data-ttu-id="f7dbf-106">Les exemples d’instructions SQL qui figurent dans ce document reposent sur l’hypothèse que les données sont stockées dans SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-106">The sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="f7dbf-107">Dans le cas contraire, reportez-vous à la cartographie du processus de science des données du cloud pour découvrir comment déplacer vos données vers SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-107">If it isn't, refer to the cloud data science process map to learn how to move your data to SQL Server.</span></span>
> 
> 

## <span data-ttu-id="f7dbf-108"><a name="SQL"></a>Utilisation de SQL</span><span class="sxs-lookup"><span data-stu-id="f7dbf-108"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="f7dbf-109">Dans cette section, nous décrivons les tâches de retraitement des données via SQL ci-après :</span><span class="sxs-lookup"><span data-stu-id="f7dbf-109">We describe the following data wrangling tasks in this section using SQL:</span></span>

1. [<span data-ttu-id="f7dbf-110">Exploration des données</span><span class="sxs-lookup"><span data-stu-id="f7dbf-110">Data Exploration</span></span>](#sql-dataexploration)
2. [<span data-ttu-id="f7dbf-111">Génération de fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="f7dbf-111">Feature Generation</span></span>](#sql-featuregen)

### <span data-ttu-id="f7dbf-112"><a name="sql-dataexploration"></a>Exploration des données</span><span class="sxs-lookup"><span data-stu-id="f7dbf-112"><a name="sql-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="f7dbf-113">Voici quelques exemples de scripts SQL utilisables pour l’exploration de magasins de données dans SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-113">Here are a few sample SQL scripts that can be used to explore data stores in SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="f7dbf-114">Pour découvrir un exemple pratique, vous pouvez utiliser le [jeu de données des taxis new-yorkais NYC Taxi](http://www.andresmh.com/nyctaxitrips/) et vous reporter au notebook IPython intitulé [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) (Retraitement des données de New-York City à l’aide de Notebook IPython et de SQL Server) pour connaître la procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-114">For a practical example, you can use the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

1. <span data-ttu-id="f7dbf-115">Obtenir le nombre d’observations par jour</span><span class="sxs-lookup"><span data-stu-id="f7dbf-115">Get the count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="f7dbf-116">Obtenir les niveaux dans une colonne catégorielle</span><span class="sxs-lookup"><span data-stu-id="f7dbf-116">Get the levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="f7dbf-117">Obtenir le nombre de niveaux en combinant deux colonnes catégorielles</span><span class="sxs-lookup"><span data-stu-id="f7dbf-117">Get the number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="f7dbf-118">Obtenir la distribution relative aux colonnes numériques</span><span class="sxs-lookup"><span data-stu-id="f7dbf-118">Get the distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <span data-ttu-id="f7dbf-119"><a name="sql-featuregen"></a>Génération de fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="f7dbf-119"><a name="sql-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="f7dbf-120">Dans cette section, nous décrivons plusieurs manières de générer des fonctionnalités via SQL :</span><span class="sxs-lookup"><span data-stu-id="f7dbf-120">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="f7dbf-121">Génération de fonctionnalités utilisant des décomptes</span><span class="sxs-lookup"><span data-stu-id="f7dbf-121">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="f7dbf-122">Génération de caractéristiques de compartimentage</span><span class="sxs-lookup"><span data-stu-id="f7dbf-122">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="f7dbf-123">Déploiement des caractéristiques à partir d’une seule colonne</span><span class="sxs-lookup"><span data-stu-id="f7dbf-123">Rolling out the features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="f7dbf-124">Une fois que vous avez généré des fonctionnalités supplémentaires, vous pouvez soit les ajouter sous forme de colonnes à la table existante, soit créer une autre table avec les fonctionnalités supplémentaires et la clé primaire que vous pouvez joindre à la table d’origine.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-124">Once you generate additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, that can be joined with the original table.</span></span> 
> 
> 

### <span data-ttu-id="f7dbf-125"><a name="sql-countfeature"></a>Génération de fonctionnalités utilisant des décomptes</span><span class="sxs-lookup"><span data-stu-id="f7dbf-125"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="f7dbf-126">Les exemples suivants décrivent deux manières de générer des fonctionnalités utilisant des décomptes.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-126">The following examples demonstrate two ways of generating count features.</span></span> <span data-ttu-id="f7dbf-127">La première méthode a recours à une somme conditionnelle, tandis que la seconde méthode utilise la clause « where ».</span><span class="sxs-lookup"><span data-stu-id="f7dbf-127">The first method uses conditional sum and the second method uses the 'where' clause.</span></span> <span data-ttu-id="f7dbf-128">Vous pouvez ensuite associer ces dernières à la table d’origine (à l’aide des colonnes de clé primaire) pour disposer de fonctionnalités de décompte parallèlement aux données d’origine.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-128">These can then be joined with the original table (using primary key columns) to have count features alongside the original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <span data-ttu-id="f7dbf-129"><a name="sql-binningfeature"></a>Génération de caractéristiques de compartimentage</span><span class="sxs-lookup"><span data-stu-id="f7dbf-129"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="f7dbf-130">L’exemple ci-dessous illustre comment générer des fonctionnalités compartimentées en divisant (à l’aide de cinq emplacements) une colonne numérique qui peut être plutôt utilisée sous la forme d’une fonctionnalité :</span><span class="sxs-lookup"><span data-stu-id="f7dbf-130">The following example shows how to generate binned features by binning (using five bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="f7dbf-131"><a name="sql-featurerollout"></a>Déploiement des caractéristiques à partir d’une seule colonne</span><span class="sxs-lookup"><span data-stu-id="f7dbf-131"><a name="sql-featurerollout"></a>Rolling out the features from a single column</span></span>
<span data-ttu-id="f7dbf-132">Dans cette section, nous décrivons comment déployer une seule colonne dans une table afin de générer des fonctionnalités supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-132">In this section, we demonstrate how to roll out a single column in a table to generate additional features.</span></span> <span data-ttu-id="f7dbf-133">Cet exemple présuppose l’existence d’une colonne de latitude ou de longitude dans la table à partir de laquelle vous essayez de générer des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-133">The example assumes that there is a latitude or longitude column in the table from which you are trying to generate features.</span></span>

<span data-ttu-id="f7dbf-134">Voici une petite présentation des données de latitude/longitude issue du site stackoverflow : [How to measure the accuracy of latitude and longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)(Comment mesurer la précision de la latitude et de la longitude).</span><span class="sxs-lookup"><span data-stu-id="f7dbf-134">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow [How to measure the accuracy of latitude and longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span></span> <span data-ttu-id="f7dbf-135">Vous pourrez ainsi vous familiariser avec ces notions avant d’implémenter le champ d’emplacement :</span><span class="sxs-lookup"><span data-stu-id="f7dbf-135">This is useful to understand before featurizing the location field:</span></span>

* <span data-ttu-id="f7dbf-136">Le signe indique si nous nous trouvons au nord, au sud, à l’est ou à l’ouest.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-136">The sign tells us whether we are north or south, east or west on the globe.</span></span>
* <span data-ttu-id="f7dbf-137">Un chiffre des centaines différent de zéro indique que nous utilisons la longitude, et non la latitude.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-137">A nonzero hundreds digit tells us that we're using longitude, not latitude!</span></span>
* <span data-ttu-id="f7dbf-138">Le chiffre des dizaines équivaut à environ 1 000 kilomètres.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-138">The tens digit gives a position to about 1,000 kilometers.</span></span> <span data-ttu-id="f7dbf-139">Il nous fournit des informations utiles sur le continent ou l’océan dans lequel nous nous trouvons.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-139">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="f7dbf-140">Le chiffre des unités (un degré décimal) équivaut à 111 kilomètres maximum (60 milles marins, soit environ 69 milles terrestres).</span><span class="sxs-lookup"><span data-stu-id="f7dbf-140">The units digit (one decimal degree) gives a position up to 111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="f7dbf-141">Il nous permet de déterminer approximativement le département de grande superficie ou le pays dans lequel nous sommes.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-141">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="f7dbf-142">La première décimale équivaut à 11,1 km maximum : elle permet de distinguer la position d’une grande ville de celle d’une autre grande localité voisine.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-142">The first decimal place is worth up to 11.1 km: it can distinguish the position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="f7dbf-143">La deuxième décimale équivaut à 1,1 km maximum : elle permet de différencier un village du suivant.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-143">The second decimal place is worth up to 1.1 km: it can separate one village from the next.</span></span>
* <span data-ttu-id="f7dbf-144">La troisième décimale équivaut à 110 m maximum : elle permet d’identifier un domaine agricole ou un campus universitaire de grande taille.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-144">The third decimal place is worth up to 110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="f7dbf-145">La quatrième décimale correspond à 11 m maximum : elle permet d’identifier une parcelle de terre.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-145">The fourth decimal place is worth up to 11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="f7dbf-146">Cette information est comparable à la précision classique d’un appareil GPS non corrigé sans aucune interférence.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-146">It is comparable to the typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="f7dbf-147">La cinquième décimale équivaut à 1,1 m maximum : elle permet de distinguer un arbre d’un autre.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-147">The fifth decimal place is worth up to 1.1 m: it distinguishes trees from each other.</span></span> <span data-ttu-id="f7dbf-148">Un tel niveau de précision sur les appareils GPS commerciaux ne peut être atteint qu’au moyen d’une correction différentielle.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-148">Accuracy to this level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="f7dbf-149">La sixième décimale équivaut à 0,11 m maximum : vous pouvez notamment l’utiliser pour représenter des structures en détail, pour concevoir des plans d’aménagement paysager et pour construire des routes.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-149">The sixth decimal place is worth up to 0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="f7dbf-150">Elle devrait se révéler amplement suffisante pour assurer le suivi des mouvements des glaciers et des rivières.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-150">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="f7dbf-151">L’obtention d’une telle précision sur un GPS nécessite l’emploi de mesures rigoureuses, telles qu’une correction différentielle.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-151">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="f7dbf-152">Vous pouvez implémenter les informations de localisation comme illustré ci-dessous, en les répartissant par région, par emplacement et par ville.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-152">The location information can be featurized as follows, separating out region, location, and city information.</span></span> <span data-ttu-id="f7dbf-153">Notez que vous pouvez aussi appeler un point de terminaison REST, tel que l’API Bing Cartes disponible dans [Rechercher un emplacement par point](https://msdn.microsoft.com/library/ff701710.aspx) , pour obtenir des informations sur la région/le secteur.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-153">Note that you can also call a REST end point such as Bing Maps API available at [Find a Location by Point](https://msdn.microsoft.com/library/ff701710.aspx) to get the region/district information.</span></span>

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

<span data-ttu-id="f7dbf-154">Vous pouvez en outre exploiter ces fonctionnalités de localisation pour générer d’autres fonctionnalités utilisant des décomptes comme décrit précédemment.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-154">These location-based features can be further used to generate additional count features as described earlier.</span></span> 

> [!TIP]
> <span data-ttu-id="f7dbf-155">Vous pouvez insérer les enregistrements par programmation en utilisant le langage de votre choix.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-155">You can programmatically insert the records using your language of choice.</span></span> <span data-ttu-id="f7dbf-156">Vous aurez peut-être besoin d’insérer les données dans des blocs pour améliorer l’efficacité des écritures (pour obtenir un exemple illustrant la marche à suivre, consultez cet [exemple HelloWorld qui montre comment accéder à SQL Server avec python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span><span class="sxs-lookup"><span data-stu-id="f7dbf-156">You may need to insert the data in chunks to improve write efficiency (for an example of how to do this using pyodbc, see [A HelloWorld sample to access SQLServer with python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span></span> <span data-ttu-id="f7dbf-157">Une autre solution consiste à insérer les données dans la base de données à l’aide de l’ [utilitaire BCP](https://msdn.microsoft.com/library/ms162802.aspx).</span><span class="sxs-lookup"><span data-stu-id="f7dbf-157">Another alternative is to insert data in the database using the [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx).</span></span>
> 
> 

### <span data-ttu-id="f7dbf-158"><a name="sql-aml"></a>Connexion à Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f7dbf-158"><a name="sql-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="f7dbf-159">La fonctionnalité que vous venez de générer peut être ajoutée sous la forme d’une colonne à une table existante ou stockée dans une nouvelle table et associée à la table d’origine pour l’apprentissage automatique.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-159">The newly generated feature can be added as a column to an existing table or stored in a new table and joined with the original table for machine learning.</span></span> <span data-ttu-id="f7dbf-160">Vous pouvez générer des fonctionnalités ou y accéder si elles sont déjà créées à l’aide du module [Importer des données][import-data] dans Azure Machine Learning comme expliqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f7dbf-160">Features can be generated or accessed if already created, using the [Import Data][import-data] module in Azure Machine Learning as shown below:</span></span>

![lecteurs azureml][1] 

## <span data-ttu-id="f7dbf-162"><a name="python"></a>Utilisation d’un langage de programmation tel que Python</span><span class="sxs-lookup"><span data-stu-id="f7dbf-162"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="f7dbf-163">L’utilisation de Python pour explorer les données et générer des fonctionnalités quand les données sont stockées dans SQL Server est comparable au traitement des données dans l’objet blob Azure à l’aide de Python comme expliqué dans [Traiter les données Azure Blob dans votre environnement de science des données](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="f7dbf-163">Using Python to explore data and generate features when the data is in SQL Server is similar to processing data in Azure blob using Python as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="f7dbf-164">Les données doivent être chargées à partir de la base de données dans une trame de données pandas, puis faire l’objet d’un traitement complémentaire.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-164">The data needs to be loaded from the database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="f7dbf-165">Nous décrivons dans cette section le processus de connexion à la base de données et de chargement des données dans la trame de données.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-165">We document the process of connecting to the database and loading the data into the data frame in this section.</span></span>

<span data-ttu-id="f7dbf-166">Le format de chaîne de connexion ci-après vous permet de vous connecter à une base de données SQL Server à partir de Python à l’aide de pyodbc (en remplaçant les variables servername, dbname, username et password par les valeurs qui vous correspondent) :</span><span class="sxs-lookup"><span data-stu-id="f7dbf-166">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="f7dbf-167">La [bibliothèque Pandas](http://pandas.pydata.org/) de Python offre un ensemble élaboré de structures de données et d’outils d’analyse des données pour la manipulation des données dans le cadre d’une programmation en Python.</span><span class="sxs-lookup"><span data-stu-id="f7dbf-167">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="f7dbf-168">Le code ci-après lit les résultats renvoyés par une base de données SQL Server dans une trame de données pandas :</span><span class="sxs-lookup"><span data-stu-id="f7dbf-168">The code below reads the results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="f7dbf-169">Vous pouvez à présent utiliser la trame de données Pandas comme décrit dans l’article [Traiter les données Azure Blob dans votre environnement de science des données](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="f7dbf-169">Now you can work with the Pandas data frame as covered in the article [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="azure-data-science-in-action-example"></a><span data-ttu-id="f7dbf-170">Exemple de processus de science des données Azure en action</span><span class="sxs-lookup"><span data-stu-id="f7dbf-170">Azure Data Science in Action Example</span></span>
<span data-ttu-id="f7dbf-171">Pour découvrir un exemple de procédure pas à pas du processus de science des données Azure à l’aide d’un jeu de données public, consultez la rubrique [Processus de science des données Azure en action](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="f7dbf-171">For an end-to-end walkthrough example of the Azure Data Science Process using a public dataset, see [Azure Data Science Process in Action](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

