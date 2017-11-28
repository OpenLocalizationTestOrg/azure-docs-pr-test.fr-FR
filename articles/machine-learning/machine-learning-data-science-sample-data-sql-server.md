---
title: "Échantillonner des données dans SQL Server sur Azure | Microsoft Docs"
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
ms.openlocfilehash: 1bdcc7175dac325de1144d805e977264524b3fbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="98d5b-103"><a name="heading"></a>Échantillonner des données dans SQL Server sur Azure</span><span class="sxs-lookup"><span data-stu-id="98d5b-103"><a name="heading"></a>Sample data in SQL Server on Azure</span></span>
<span data-ttu-id="98d5b-104">Ce document montre comment échantillonner des données stockées dans SQL Server sur Azure à l’aide de SQL ou du langage de programmation Python.</span><span class="sxs-lookup"><span data-stu-id="98d5b-104">This document shows how to sample data stored in SQL Server on Azure using either SQL or the Python programming language.</span></span> <span data-ttu-id="98d5b-105">Il montre également comment déplacer les données échantillonnées vers Azure Machine Learning en les enregistrant dans un fichier, en les chargeant vers un objet blob Azure, puis en les lisant dans Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="98d5b-105">It also shows how to move sampled data into Azure Machine Learning by saving it to a file, uploading it to an Azure blob, and then reading it into Azure Machine Learning Studio.</span></span>

<span data-ttu-id="98d5b-106">L’échantillonnage Python utilise la bibliothèque ODBC [pyodbc](https://code.google.com/p/pyodbc/) pour se connecter à SQL Server sur Azure et la bibliothèque [Pandas](http://pandas.pydata.org/) pour effectuer l’échantillonnage proprement dit.</span><span class="sxs-lookup"><span data-stu-id="98d5b-106">The Python sampling uses the [pyodbc](https://code.google.com/p/pyodbc/) ODBC library to connect to SQL Server on Azure and the [Pandas](http://pandas.pydata.org/) library to do the sampling.</span></span>

> [!NOTE]
> <span data-ttu-id="98d5b-107">L’exemple de code SQL figurant dans ce document repose sur l’hypothèse que les données sont stockées dans SQL Server sur Azure.</span><span class="sxs-lookup"><span data-stu-id="98d5b-107">The sample SQL code in this document assumes that the data is in a SQL Server on Azure.</span></span> <span data-ttu-id="98d5b-108">Si ce n’est pas le cas, reportez-vous à la rubrique [Déplacer des données vers SQL Server sur Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) pour savoir comment déplacer vos données vers SQL Server sur Azure.</span><span class="sxs-lookup"><span data-stu-id="98d5b-108">If it is not, please refer to [Move data to SQL Server on Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) topic for instructions on how to move your data to SQL Server on Azure.</span></span>
> 
> 

<span data-ttu-id="98d5b-109">Le **menu** ci-après pointe vers des rubriques qui expliquent comment échantillonner des données dans différents environnements de stockage.</span><span class="sxs-lookup"><span data-stu-id="98d5b-109">The following **menu** links to topics that describe how to sample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="98d5b-110">**Pourquoi échantillonner vos données ?**</span><span class="sxs-lookup"><span data-stu-id="98d5b-110">**Why sample your data?**</span></span>
<span data-ttu-id="98d5b-111">Si vous prévoyez d’analyser un jeu de données volumineux, il est généralement recommandé de sous-échantillonner les données afin de réduire leur taille sous une forme plus facilement exploitable, mais toujours représentative.</span><span class="sxs-lookup"><span data-stu-id="98d5b-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="98d5b-112">Cette opération facilite la compréhension et l’exploration des données, ainsi que la conception de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="98d5b-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="98d5b-113">Son rôle dans le [processus TDSP (Team Data Science Process)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) consiste à permettre le prototypage rapide des fonctions de traitement des données et des modèles d’apprentissage automatique.</span><span class="sxs-lookup"><span data-stu-id="98d5b-113">Its role in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

<span data-ttu-id="98d5b-114">Cette tâche d’échantillonnage est une étape du [processus TDSP (Team Data Science Process)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="98d5b-114">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <span data-ttu-id="98d5b-115"><a name="SQL"></a>Utilisation de SQL</span><span class="sxs-lookup"><span data-stu-id="98d5b-115"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="98d5b-116">Cette section décrit différentes méthodes permettant d’effectuer un échantillonnage aléatoire simple des données de la base de données via SQL.</span><span class="sxs-lookup"><span data-stu-id="98d5b-116">This section describes several methods using SQL to perform simple random sampling against the data in the database.</span></span> <span data-ttu-id="98d5b-117">Choisissez une méthode en fonction de la taille de vos données et de leur distribution.</span><span class="sxs-lookup"><span data-stu-id="98d5b-117">Please choose a method based on your data size and its distribution.</span></span>

<span data-ttu-id="98d5b-118">Les deux options ci-après indiquent comment utiliser l’élément newid dans SQL Server pour procéder à l’échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="98d5b-118">The two items below show how to use newid in SQL Server to perform the sampling.</span></span> <span data-ttu-id="98d5b-119">La méthode que vous choisissez dépend du degré aléatoire qui doit caractériser l’échantillon (dans l’exemple de code ci-après, l’élément pk_id est supposé correspondre à une clé primaire générée automatiquement).</span><span class="sxs-lookup"><span data-stu-id="98d5b-119">The method you choose depends on how random you want the sample to be (pk_id in the sample code below is assumed to be an auto-generated primary key).</span></span>

1. <span data-ttu-id="98d5b-120">Échantillon aléatoire moins strict</span><span class="sxs-lookup"><span data-stu-id="98d5b-120">Less strict random sample</span></span>
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. <span data-ttu-id="98d5b-121">Échantillon plus aléatoire</span><span class="sxs-lookup"><span data-stu-id="98d5b-121">More random sample</span></span> 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

<span data-ttu-id="98d5b-122">Vous pouvez également utiliser l’élément TABLESAMPLE pour l’échantillonnage, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="98d5b-122">Tablesample can be used for sampling as well as demonstrated below.</span></span> <span data-ttu-id="98d5b-123">L’utilisation de cette méthode peut constituer une meilleure approche si vos données sont volumineuses (en supposant que les données figurant sur des pages différentes ne sont pas corrélées) et que vous souhaitez que la requête s’exécute dans un délai acceptable.</span><span class="sxs-lookup"><span data-stu-id="98d5b-123">This may be a better approach if your data size is large (assuming that data on different pages is not correlated) and for the query to complete in a reasonable time.</span></span>

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> <span data-ttu-id="98d5b-124">Vous pouvez explorer et générer des fonctionnalités à partir de ces données échantillonnées en les stockant dans une nouvelle table.</span><span class="sxs-lookup"><span data-stu-id="98d5b-124">You can explore and generate features from this sampled data by storing it in a new table</span></span>
> 
> 

### <span data-ttu-id="98d5b-125"><a name="sql-aml"></a>Connexion à Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="98d5b-125"><a name="sql-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="98d5b-126">Vous pouvez utiliser directement les exemples de requêtes ci-dessus dans le module [Importer les données][import-data] d’Azure Machine Learning afin de sous-échantillonner les données à la volée et de les importer dans une expérience Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="98d5b-126">You can directly  use the sample queries above in the Azure Machine Learning [Import Data][import-data] module to down-sample the data on the fly and bring it into an Azure Machine Learning experiment.</span></span> <span data-ttu-id="98d5b-127">La capture d’écran ci-après illustre l’utilisation du module Lecteur pour lire les données échantillonnées :</span><span class="sxs-lookup"><span data-stu-id="98d5b-127">A screen shot of using the reader module to read the sampled data is shown below:</span></span>

![lecteur sql][1]

## <span data-ttu-id="98d5b-129"><a name="python"></a>Utilisation du langage de programmation Python</span><span class="sxs-lookup"><span data-stu-id="98d5b-129"><a name="python"></a>Using the Python programming language</span></span>
<span data-ttu-id="98d5b-130">Cette section décrit l’utilisation de la [bibliothèque pyodbc](https://code.google.com/p/pyodbc/) pour établir une connexion ODBC à une base de données SQL Server dans Python.</span><span class="sxs-lookup"><span data-stu-id="98d5b-130">This section demonstrates using the [pyodbc library](https://code.google.com/p/pyodbc/) to establish an ODBC connect to a SQL server database in Python.</span></span> <span data-ttu-id="98d5b-131">La chaîne de connexion de base de données se présente comme suit :(remplacez les variables servername, dbname, username et password par les valeurs de votre configuration) :</span><span class="sxs-lookup"><span data-stu-id="98d5b-131">The database connection string is as follows: (replace servername, dbname, username and password with your configuration):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="98d5b-132">La bibliothèque [Pandas](http://pandas.pydata.org/) de Python offre un ensemble élaboré de structures de données et d’outils d’analyse des données pour la manipulation des données dans le cadre d’une programmation en Python.</span><span class="sxs-lookup"><span data-stu-id="98d5b-132">The [Pandas](http://pandas.pydata.org/) library in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="98d5b-133">Le code ci-après lit un échantillon de 0,1 % des données d’une table de la base de données Azure SQL dans une trame de données pandas :</span><span class="sxs-lookup"><span data-stu-id="98d5b-133">The code below reads a 0.1% sample of the data from a table in Azure SQL database into a Pandas data :</span></span>

    import pandas as pd

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

<span data-ttu-id="98d5b-134">Vous pouvez à présent travailler sur les données échantillonnées dans la trame de données pandas.</span><span class="sxs-lookup"><span data-stu-id="98d5b-134">You can now work with the sampled data in the Pandas data frame.</span></span> 

### <span data-ttu-id="98d5b-135"><a name="python-aml"></a>Connexion à Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="98d5b-135"><a name="python-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="98d5b-136">Vous pouvez utiliser l’exemple de code ci-après pour enregistrer les données sous-échantillonnées dans un fichier et les charger dans un objet blob Azure.</span><span class="sxs-lookup"><span data-stu-id="98d5b-136">You can use the following sample code to save the down-sampled data to a file and upload it to an Azure blob.</span></span> <span data-ttu-id="98d5b-137">Les données figurant dans l’objet blob peuvent être lues directement dans une expérimentation Azure Machine Learning à l’aide du module [Importer les données][import-data].</span><span class="sxs-lookup"><span data-stu-id="98d5b-137">The data in the blob can be directly read into an Azure Machine Learning Experiment using the [Import Data][import-data] module.</span></span> <span data-ttu-id="98d5b-138">La procédure comporte trois étapes :</span><span class="sxs-lookup"><span data-stu-id="98d5b-138">The steps are as follows:</span></span> 

1. <span data-ttu-id="98d5b-139">Écrire la trame de données pandas dans un fichier local</span><span class="sxs-lookup"><span data-stu-id="98d5b-139">Write the pandas data frame to a local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="98d5b-140">Charger le fichier local dans un objet blob Azure</span><span class="sxs-lookup"><span data-stu-id="98d5b-140">Upload local file to Azure blob</span></span>
   
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
3. <span data-ttu-id="98d5b-141">Lisez les données de l’objet blob Azure à l’aide du module [Importer les données][import-data] d’Azure Machine Learning, comme l’illustre la capture d’écran ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="98d5b-141">Read data from Azure blob using Azure Machine Learning [Import Data][import-data] module as shown in the screen grab below:</span></span>

![objet blob de lecteur][2]

## <a name="the-team-data-science-process-in-action-example"></a><span data-ttu-id="98d5b-143">Exemple de processus TDSP (Team Data Science Process) en action</span><span class="sxs-lookup"><span data-stu-id="98d5b-143">The Team Data Science Process in Action example</span></span>
<span data-ttu-id="98d5b-144">Pour obtenir un exemple de procédure pas à pas complet du processus TDSP (Team Data Science Process) à l’aide d’un jeu de données public, consultez [Processus TDSP (Team Data Science Process) en action : utilisation de SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="98d5b-144">For an end-to-end walkthrough example of the Team Data Science Process a using a public dataset, see [Team Data Science Process in Action: using SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
