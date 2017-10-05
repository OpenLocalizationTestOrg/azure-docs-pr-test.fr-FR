---
title: "Explorer les données d’une machine virtuelle SQL Server sur Azure | Microsoft Docs"
description: "Comment explorer les données stockées dans une machine virtuelle SQL Server sur Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ccbb3085-af9e-4ec2-9df2-15dcab261d05
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: a2be21ef15b9209db1e97150e0297558fa69a7be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a><span data-ttu-id="f463f-103">Explorer les données d’une machine virtuelle SQL Server sur Azure</span><span class="sxs-lookup"><span data-stu-id="f463f-103">Explore data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="f463f-104">Ce document explique comment explorer les données stockées dans une machine virtuelle SQL Server sur Azure.</span><span class="sxs-lookup"><span data-stu-id="f463f-104">This document covers how to explore data that is stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="f463f-105">Cela est possible avec le retraitement des données à l'aide de SQL ou en utilisant un langage de programmation comme Python.</span><span class="sxs-lookup"><span data-stu-id="f463f-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

<span data-ttu-id="f463f-106">Le **menu** suivant pointe vers des rubriques qui expliquent comment utiliser des outils pour explorer des données dans différents environnements de stockage.</span><span class="sxs-lookup"><span data-stu-id="f463f-106">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span> <span data-ttu-id="f463f-107">Cette tâche est une étape du processus Cortana Analytics (CAP).</span><span class="sxs-lookup"><span data-stu-id="f463f-107">This task is a step in the Cortana Analytics Process (CAP).</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> <span data-ttu-id="f463f-108">Les exemples d’instructions SQL qui figurent dans ce document reposent sur l’hypothèse que les données sont stockées dans SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f463f-108">The sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="f463f-109">Dans le cas contraire, reportez-vous à la cartographie du processus de science des données du cloud pour découvrir comment déplacer vos données vers SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f463f-109">If it isn't, refer to the cloud data science process map to learn how to move your data to SQL Server.</span></span>
> 
> 

## <span data-ttu-id="f463f-110"><a name="sql-dataexploration"></a>Explorer les données SQL avec des scripts SQL</span><span class="sxs-lookup"><span data-stu-id="f463f-110"><a name="sql-dataexploration"></a>Explore SQL data with SQL scripts</span></span>
<span data-ttu-id="f463f-111">Voici quelques exemples de scripts SQL utilisables pour l’exploration de magasins de données dans SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f463f-111">Here are a few sample SQL scripts that can be used to explore data stores in SQL Server.</span></span>

1. <span data-ttu-id="f463f-112">Obtenir le nombre d’observations par jour</span><span class="sxs-lookup"><span data-stu-id="f463f-112">Get the count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="f463f-113">Obtenir les niveaux dans une colonne catégorielle</span><span class="sxs-lookup"><span data-stu-id="f463f-113">Get the levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="f463f-114">Obtenir le nombre de niveaux en combinant deux colonnes catégorielles</span><span class="sxs-lookup"><span data-stu-id="f463f-114">Get the number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="f463f-115">Obtenir la distribution relative aux colonnes numériques </span><span class="sxs-lookup"><span data-stu-id="f463f-115">Get the distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> <span data-ttu-id="f463f-116">Pour découvrir un exemple pratique, vous pouvez utiliser le [jeu de données des taxis new-yorkais NYC Taxi](http://www.andresmh.com/nyctaxitrips/) et vous reporter au notebook IPython intitulé [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) (Retraitement des données de New-York City à l’aide de Notebook IPython et de SQL Server) pour connaître la procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="f463f-116">For a practical example, you can use the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <span data-ttu-id="f463f-117"><a name="python"></a>Explorer les données SQL avec Python</span><span class="sxs-lookup"><span data-stu-id="f463f-117"><a name="python"></a>Explore SQL data with Python</span></span>
<span data-ttu-id="f463f-118">L’utilisation de Python pour explorer les données et générer des fonctionnalités quand les données sont stockées dans SQL Server est comparable au traitement des données dans l’objet blob Azure à l’aide de Python comme expliqué dans [Traiter les données Azure Blob dans votre environnement de science des données](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="f463f-118">Using Python to explore data and generate features when the data is in SQL Server is similar to processing data in Azure blob using Python, as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="f463f-119">Les données doivent être chargées à partir de la base de données dans une trame de données pandas, puis faire l’objet d’un traitement complémentaire.</span><span class="sxs-lookup"><span data-stu-id="f463f-119">The data needs to be loaded from the database into a pandas DataFrame and then can be processed further.</span></span> <span data-ttu-id="f463f-120">Nous décrivons dans cette section le processus de connexion à la base de données et de chargement des données dans la trame de données.</span><span class="sxs-lookup"><span data-stu-id="f463f-120">We document the process of connecting to the database and loading the data into the DataFrame in this section.</span></span>

<span data-ttu-id="f463f-121">Le format de chaîne de connexion ci-après vous permet de vous connecter à une base de données SQL Server à partir de Python à l’aide de pyodbc (en remplaçant les variables servername, dbname, username et password par les valeurs qui vous correspondent) :</span><span class="sxs-lookup"><span data-stu-id="f463f-121">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="f463f-122">La [bibliothèque Pandas](http://pandas.pydata.org/) de Python offre un ensemble élaboré de structures de données et d’outils d’analyse des données pour la manipulation des données dans le cadre d’une programmation en Python.</span><span class="sxs-lookup"><span data-stu-id="f463f-122">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="f463f-123">Le code suivant lit les résultats renvoyés par une base de données SQL Server dans une trame de données Pandas :</span><span class="sxs-lookup"><span data-stu-id="f463f-123">The following code reads the results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="f463f-124">Vous pouvez à présent utiliser la trame de données Pandas comme décrit dans la rubrique [Traiter les données Azure Blob dans votre environnement de science des données](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="f463f-124">Now you can work with the Pandas DataFrame as covered in the topic [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="cortana-analytics-process-in-action-example"></a><span data-ttu-id="f463f-125">Exemple de processus Cortana Analytics en action</span><span class="sxs-lookup"><span data-stu-id="f463f-125">Cortana Analytics Process in Action Example</span></span>
<span data-ttu-id="f463f-126">Pour obtenir un exemple de procédure pas à pas complet du processus Cortana Analytics à l’aide d’un jeu de données public, consultez [Processus TDSP (Team Data Science Process) en action : utilisation de SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="f463f-126">For an end-to-end walkthrough example of the Cortana Analytics Process using a public dataset, see [The Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

