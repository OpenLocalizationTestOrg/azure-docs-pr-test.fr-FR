---
title: "aaaSample données dans SQL Server sur Azure | Documents Microsoft"
description: "Échantillonner des données dans SQL Server sur Azure"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 33c030d4-5cca-4cc9-99d7-2bd13a3926af
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: dc7f9529c771f6deb633775557e64a04b774f5b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="9b188-103"><a name="heading"></a>Échantillonner des données dans SQL Server sur Azure</span><span class="sxs-lookup"><span data-stu-id="9b188-103"><a name="heading"></a>Sample data in SQL Server on Azure</span></span>
<span data-ttu-id="9b188-104">Ce document montre comment les données de toosample stockées dans SQL Server sur Azure à l’aide de SQL ou hello langage de programmation Python.</span><span class="sxs-lookup"><span data-stu-id="9b188-104">This document shows how toosample data stored in SQL Server on Azure using either SQL or hello Python programming language.</span></span> <span data-ttu-id="9b188-105">Il montre également comment toomove les données échantillonnées dans Azure Machine Learning en l’enregistrant le fichier tooa, téléchargeant tooan objets blob Azure, puis de le lire dans Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="9b188-105">It also shows how toomove sampled data into Azure Machine Learning by saving it tooa file, uploading it tooan Azure blob, and then reading it into Azure Machine Learning Studio.</span></span>

<span data-ttu-id="9b188-106">échantillonnage de Python Hello utilise hello [pyodbc](https://code.google.com/p/pyodbc/) ODBC bibliothèque tooconnect tooSQL Server sur Azure et hello [Pandas](http://pandas.pydata.org/) échantillonnage de bibliothèque toodo hello.</span><span class="sxs-lookup"><span data-stu-id="9b188-106">hello Python sampling uses hello [pyodbc](https://code.google.com/p/pyodbc/) ODBC library tooconnect tooSQL Server on Azure and hello [Pandas](http://pandas.pydata.org/) library toodo hello sampling.</span></span>

> [!NOTE]
> <span data-ttu-id="9b188-107">Hello exemple de code SQL dans ce document part du principe que hello données sont dans un serveur SQL Server sur Azure.</span><span class="sxs-lookup"><span data-stu-id="9b188-107">hello sample SQL code in this document assumes that hello data is in a SQL Server on Azure.</span></span> <span data-ttu-id="9b188-108">Si elle n’est pas le cas, veuillez vous référer trop[déplacer les données tooSQL Server sur Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) rubrique pour obtenir des instructions sur la façon de toomove votre tooSQL données Server sur Azure.</span><span class="sxs-lookup"><span data-stu-id="9b188-108">If it is not, please refer too[Move data tooSQL Server on Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) topic for instructions on how toomove your data tooSQL Server on Azure.</span></span>
> 
> 

<span data-ttu-id="9b188-109">suivant de Hello **menu** lie tootopics qui décrivent comment toosample des données à partir de différents environnements de stockage.</span><span class="sxs-lookup"><span data-stu-id="9b188-109">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="9b188-110">**Pourquoi échantillonner vos données ?**</span><span class="sxs-lookup"><span data-stu-id="9b188-110">**Why sample your data?**</span></span>
<span data-ttu-id="9b188-111">Si dataset hello vous envisagez de tooanalyze est grand, il est généralement un tooreduce de données recommandé toodown-exemple hello il tooa plus petite mais représentatif et plus facile à gérer la taille.</span><span class="sxs-lookup"><span data-stu-id="9b188-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="9b188-112">Cette opération facilite la compréhension et l’exploration des données, ainsi que la conception de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="9b188-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="9b188-113">Son rôle dans hello [processus de science des données équipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) est tooenable le prototypage rapide des fonctions de traitement des données de hello et modèles d’apprentissage automatique.</span><span class="sxs-lookup"><span data-stu-id="9b188-113">Its role in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="9b188-114">Cette tâche d’échantillonnage est une étape Bonjour [processus de science des données équipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="9b188-114">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <span data-ttu-id="9b188-115"><a name="SQL"></a>Utilisation de SQL</span><span class="sxs-lookup"><span data-stu-id="9b188-115"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="9b188-116">Cette section décrit plusieurs méthodes à l’aide de SQL tooperform un échantillonnage aléatoire simple par rapport aux données de hello dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="9b188-116">This section describes several methods using SQL tooperform simple random sampling against hello data in hello database.</span></span> <span data-ttu-id="9b188-117">Choisissez une méthode en fonction de la taille de vos données et de leur distribution.</span><span class="sxs-lookup"><span data-stu-id="9b188-117">Please choose a method based on your data size and its distribution.</span></span>

<span data-ttu-id="9b188-118">deux éléments Hello ci-dessous montrent comment newid toouse dans SQL Server tooperform hello d’échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="9b188-118">hello two items below show how toouse newid in SQL Server tooperform hello sampling.</span></span> <span data-ttu-id="9b188-119">Hello méthode que vous choisissez dépend aléatoire hello exemple toobe (pk_id hello exemple de code ci-dessous est supposé toobe une clé primaire générée automatiquement).</span><span class="sxs-lookup"><span data-stu-id="9b188-119">hello method you choose depends on how random you want hello sample toobe (pk_id in hello sample code below is assumed toobe an auto-generated primary key).</span></span>

1. <span data-ttu-id="9b188-120">Échantillon aléatoire moins strict</span><span class="sxs-lookup"><span data-stu-id="9b188-120">Less strict random sample</span></span>
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. <span data-ttu-id="9b188-121">Échantillon plus aléatoire</span><span class="sxs-lookup"><span data-stu-id="9b188-121">More random sample</span></span> 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

<span data-ttu-id="9b188-122">Vous pouvez également utiliser l’élément TABLESAMPLE pour l’échantillonnage, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9b188-122">Tablesample can be used for sampling as well as demonstrated below.</span></span> <span data-ttu-id="9b188-123">Cela peut être une meilleure approche si vos données sont volumineuses (en supposant que les données sur des pages différentes ne sont pas mis en corrélation) et pour hello requête toocomplete dans un délai raisonnable.</span><span class="sxs-lookup"><span data-stu-id="9b188-123">This may be a better approach if your data size is large (assuming that data on different pages is not correlated) and for hello query toocomplete in a reasonable time.</span></span>

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> <span data-ttu-id="9b188-124">Vous pouvez explorer et générer des fonctionnalités à partir de ces données échantillonnées en les stockant dans une nouvelle table.</span><span class="sxs-lookup"><span data-stu-id="9b188-124">You can explore and generate features from this sampled data by storing it in a new table</span></span>
> 
> 

### <span data-ttu-id="9b188-125"><a name="sql-aml"></a>Connexion tooAzure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9b188-125"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="9b188-126">Vous pouvez utiliser directement les exemples de requêtes hello ci-dessus Bonjour Azure Machine Learning [importer des données] [ import-data] données toodown-exemple hello module hello rendiez et importez-les dans une expérience Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="9b188-126">You can directly  use hello sample queries above in hello Azure Machine Learning [Import Data][import-data] module toodown-sample hello data on hello fly and bring it into an Azure Machine Learning experiment.</span></span> <span data-ttu-id="9b188-127">Vous trouverez ci-dessous une capture d’écran de l’utilisation de données de hello échantillonnée tooread hello lecture du module :</span><span class="sxs-lookup"><span data-stu-id="9b188-127">A screen shot of using hello reader module tooread hello sampled data is shown below:</span></span>

![lecteur sql][1]

## <span data-ttu-id="9b188-129"><a name="python"></a>À l’aide du langage de programmation Python hello</span><span class="sxs-lookup"><span data-stu-id="9b188-129"><a name="python"></a>Using hello Python programming language</span></span>
<span data-ttu-id="9b188-130">Cette section illustre l’utilisation de hello [pyodbc bibliothèque](https://code.google.com/p/pyodbc/) tooestablish une application ODBC se connecter tooa la base de données SQL server dans Python.</span><span class="sxs-lookup"><span data-stu-id="9b188-130">This section demonstrates using hello [pyodbc library](https://code.google.com/p/pyodbc/) tooestablish an ODBC connect tooa SQL server database in Python.</span></span> <span data-ttu-id="9b188-131">chaîne de connexion de base de données Hello est comme suit : (replace servername, dbname, nom d’utilisateur et mot de passe à la configuration) :</span><span class="sxs-lookup"><span data-stu-id="9b188-131">hello database connection string is as follows: (replace servername, dbname, username and password with your configuration):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="9b188-132">Hello [Pandas](http://pandas.pydata.org/) dans Python fournit un ensemble complet d’outils d’analyse de données et des structures de données pour la manipulation de données pour la programmation de Python.</span><span class="sxs-lookup"><span data-stu-id="9b188-132">hello [Pandas](http://pandas.pydata.org/) library in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="9b188-133">code Hello ci-dessous lit un exemple de 0,1 % des données de hello à partir d’une table de base de données SQL Azure en données Pandas :</span><span class="sxs-lookup"><span data-stu-id="9b188-133">hello code below reads a 0.1% sample of hello data from a table in Azure SQL database into a Pandas data :</span></span>

    import pandas as pd

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

<span data-ttu-id="9b188-134">Vous pouvez désormais travailler avec des données dans une trame de données hello Pandas hello échantillonnée.</span><span class="sxs-lookup"><span data-stu-id="9b188-134">You can now work with hello sampled data in hello Pandas data frame.</span></span> 

### <span data-ttu-id="9b188-135"><a name="python-aml"></a>Connexion tooAzure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9b188-135"><a name="python-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="9b188-136">Vous pouvez utiliser hello toosave le code exemple hello échantillonnées en bas des données tooa fichier suivant et téléchargez-le tooan objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="9b188-136">You can use hello following sample code toosave hello down-sampled data tooa file and upload it tooan Azure blob.</span></span> <span data-ttu-id="9b188-137">Hello données dans l’objet blob de hello peuvent être directement lues dans une expérience d’apprentissage de Machine Azure à l’aide de hello [importer des données] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="9b188-137">hello data in hello blob can be directly read into an Azure Machine Learning Experiment using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="9b188-138">étapes de Hello sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="9b188-138">hello steps are as follows:</span></span> 

1. <span data-ttu-id="9b188-139">Écrire le fichier local tooa du frame données hello pandas</span><span class="sxs-lookup"><span data-stu-id="9b188-139">Write hello pandas data frame tooa local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="9b188-140">Télécharger l’objet blob de fichier local tooAzure</span><span class="sxs-lookup"><span data-stu-id="9b188-140">Upload local file tooAzure blob</span></span>
   
        from azure.storage import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        LOCALFILENAME= <local_file_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        output_blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)    
        localfileprocessed = os.path.join(os.getcwd(),LOCALFILENAME) #assuming file is in current working directory
   
        try:
   
        #perform upload
        output_blob_service.put_block_blob_from_path(CONTAINERNAME,BLOBNAME,localfileprocessed)
   
        except:            
            print ("Something went wrong with uploading blob:"+BLOBNAME)
3. <span data-ttu-id="9b188-141">Lire les données d’objets blob Azure à l’aide d’Azure Machine Learning [importer des données] [ import-data] module, comme indiqué dans la capture d’écran hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="9b188-141">Read data from Azure blob using Azure Machine Learning [Import Data][import-data] module as shown in hello screen grab below:</span></span>

![objet blob de lecteur][2]

## <a name="hello-team-data-science-process-in-action-example"></a><span data-ttu-id="9b188-143">Hello processus de science des données équipe dans l’exemple d’Action</span><span class="sxs-lookup"><span data-stu-id="9b188-143">hello Team Data Science Process in Action example</span></span>
<span data-ttu-id="9b188-144">Pour obtenir un exemple de procédure pas à pas de bout en bout de hello processus de science des données équipe un un jeu de données public, à l’aide voir [équipe processus de science des données en Action : à l’aide de SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="9b188-144">For an end-to-end walkthrough example of hello Team Data Science Process a using a public dataset, see [Team Data Science Process in Action: using SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
