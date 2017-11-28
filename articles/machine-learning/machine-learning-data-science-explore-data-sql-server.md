---
title: "données d’aaaExplore dans SQL Server virtuels dans Azure | Documents Microsoft"
description: "Comment tooexplore les données stockées dans une machine virtuelle SQL Server sur Azure."
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
ms.openlocfilehash: fcc449fc0d0e49be9b673cfb2de347cf44804017
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a><span data-ttu-id="d92fe-103">Explorer les données d’une machine virtuelle SQL Server sur Azure</span><span class="sxs-lookup"><span data-stu-id="d92fe-103">Explore data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="d92fe-104">Ce document décrit comment les données tooexplore qui sont stockées dans une machine virtuelle SQL Server sur Azure.</span><span class="sxs-lookup"><span data-stu-id="d92fe-104">This document covers how tooexplore data that is stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="d92fe-105">Cela est possible avec le retraitement des données à l'aide de SQL ou en utilisant un langage de programmation comme Python.</span><span class="sxs-lookup"><span data-stu-id="d92fe-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

<span data-ttu-id="d92fe-106">suivant de Hello **menu** tootopics qui décrivent comment toouse outils tooexplore des données à partir de différents environnements de stockage est liée.</span><span class="sxs-lookup"><span data-stu-id="d92fe-106">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span> <span data-ttu-id="d92fe-107">Cette tâche est une étape Bonjour Cortana Analytique processus (CAP).</span><span class="sxs-lookup"><span data-stu-id="d92fe-107">This task is a step in hello Cortana Analytics Process (CAP).</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> <span data-ttu-id="d92fe-108">Hello exemples d’instructions SQL dans ce document supposent que les données sont dans SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d92fe-108">hello sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="d92fe-109">Si elle n’est pas le cas, consultez Comment toohello cloud données science processus carte toolearn toomove votre tooSQL de données serveur.</span><span class="sxs-lookup"><span data-stu-id="d92fe-109">If it isn't, refer toohello cloud data science process map toolearn how toomove your data tooSQL Server.</span></span>
> 
> 

## <span data-ttu-id="d92fe-110"><a name="sql-dataexploration"></a>Explorer les données SQL avec des scripts SQL</span><span class="sxs-lookup"><span data-stu-id="d92fe-110"><a name="sql-dataexploration"></a>Explore SQL data with SQL scripts</span></span>
<span data-ttu-id="d92fe-111">Voici quelques exemples de scripts SQL qui peuvent être utilisés tooexplore des magasins de données dans SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d92fe-111">Here are a few sample SQL scripts that can be used tooexplore data stores in SQL Server.</span></span>

1. <span data-ttu-id="d92fe-112">Obtenir le nombre de hello d’observations par jour</span><span class="sxs-lookup"><span data-stu-id="d92fe-112">Get hello count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="d92fe-113">Obtenir des niveaux de hello dans une colonne catégorielle</span><span class="sxs-lookup"><span data-stu-id="d92fe-113">Get hello levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="d92fe-114">Obtenir le nombre hello de niveaux dans la combinaison de deux colonnes catégorielles</span><span class="sxs-lookup"><span data-stu-id="d92fe-114">Get hello number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="d92fe-115">Obtenir distribution hello pour les colonnes numériques</span><span class="sxs-lookup"><span data-stu-id="d92fe-115">Get hello distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> <span data-ttu-id="d92fe-116">Pour obtenir un exemple pratique, vous pouvez utiliser hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) et toohello IPNB intitulée [NYC données ensuivirent à l’aide du bloc-notes de IPython et de SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) pour une procédure pas à pas de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="d92fe-116">For a practical example, you can use hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <span data-ttu-id="d92fe-117"><a name="python"></a>Explorer les données SQL avec Python</span><span class="sxs-lookup"><span data-stu-id="d92fe-117"><a name="python"></a>Explore SQL data with Python</span></span>
<span data-ttu-id="d92fe-118">L’utilisation de Python tooexplore données et générer des fonctionnalités lorsque hello sont de données dans SQL Server est données tooprocessing similaires dans des objets blob Azure à l’aide de Python, comme décrit dans [données d’objets Blob Azure de processus dans votre environnement de science des données](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="d92fe-118">Using Python tooexplore data and generate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python, as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="d92fe-119">les données de salutation doit toobe chargé à partir de la base de données hello dans une trame de données pandas et peuvent ensuite être traitées ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="d92fe-119">hello data needs toobe loaded from hello database into a pandas DataFrame and then can be processed further.</span></span> <span data-ttu-id="d92fe-120">Nous processus hello de connexion de base de données toohello et le chargement des données de hello en hello trame de données dans cette section de document.</span><span class="sxs-lookup"><span data-stu-id="d92fe-120">We document hello process of connecting toohello database and loading hello data into hello DataFrame in this section.</span></span>

<span data-ttu-id="d92fe-121">Hello, suivant le format de chaîne de connexion peut être utilisé tooconnect tooa base de données SQL à partir de Python à l’aide de pyodbc (remplacez servername, dbname, nom d’utilisateur et mot de passe avec les valeurs spécifiques) :</span><span class="sxs-lookup"><span data-stu-id="d92fe-121">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="d92fe-122">Hello [bibliothèque de Pandas](http://pandas.pydata.org/) dans Python fournit un ensemble complet d’outils d’analyse de données et des structures de données pour la manipulation de données pour la programmation de Python.</span><span class="sxs-lookup"><span data-stu-id="d92fe-122">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="d92fe-123">Hello de code suivant lit les résultats hello retourné à partir d’une base de données SQL Server dans une trame de données Pandas :</span><span class="sxs-lookup"><span data-stu-id="d92fe-123">hello following code reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="d92fe-124">Maintenant que vous pouvez travailler avec hello Pandas trame de données comme indiqué dans la rubrique de hello [données d’objets Blob Azure de processus dans votre environnement de science des données](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="d92fe-124">Now you can work with hello Pandas DataFrame as covered in hello topic [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="cortana-analytics-process-in-action-example"></a><span data-ttu-id="d92fe-125">Exemple de processus Cortana Analytics en action</span><span class="sxs-lookup"><span data-stu-id="d92fe-125">Cortana Analytics Process in Action Example</span></span>
<span data-ttu-id="d92fe-126">Pour obtenir un exemple de procédure pas à pas de bout en bout de hello processus Analytique de Cortana à l’aide d’un jeu de données public, consultez [hello du processus de science des données équipe en action : à l’aide de SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="d92fe-126">For an end-to-end walkthrough example of hello Cortana Analytics Process using a public dataset, see [hello Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

