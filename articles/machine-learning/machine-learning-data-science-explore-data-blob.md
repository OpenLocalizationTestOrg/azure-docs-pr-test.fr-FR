---
title: "données aaaExplore dans Azure blob storage avec Pandas | Documents Microsoft"
description: "Comment tooexplore les données stockées dans Azure blob conteneur à l’aide de Pandas."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: feaa9e54-01e0-48c8-a917-1eba0f9d9ec7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 28f3c0aebf2300006066c4b19dcb1f0a76a1deb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a><span data-ttu-id="ab154-103">Explorer les données dans le stockage d’objets blob Azure avec Pandas</span><span class="sxs-lookup"><span data-stu-id="ab154-103">Explore data in Azure blob storage with Pandas</span></span>
<span data-ttu-id="ab154-104">Ce document décrit comment tooexplore les données stockées dans Azure blob à l’aide du conteneur [Pandas](http://pandas.pydata.org/) package Python.</span><span class="sxs-lookup"><span data-stu-id="ab154-104">This document covers how tooexplore data that is stored in Azure blob container using [Pandas](http://pandas.pydata.org/) Python package.</span></span>

<span data-ttu-id="ab154-105">suivant de Hello **menu** tootopics qui décrivent comment toouse outils tooexplore des données à partir de différents environnements de stockage est liée.</span><span class="sxs-lookup"><span data-stu-id="ab154-105">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span> <span data-ttu-id="ab154-106">Cette tâche est une étape Bonjour [processus de science des données]().</span><span class="sxs-lookup"><span data-stu-id="ab154-106">This task is a step in hello [Data Science Process]().</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="ab154-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ab154-107">Prerequisites</span></span>
<span data-ttu-id="ab154-108">Cet article suppose que vous avez :</span><span class="sxs-lookup"><span data-stu-id="ab154-108">This article assumes that you have:</span></span>

* <span data-ttu-id="ab154-109">Créé un compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ab154-109">Created an Azure storage account.</span></span> <span data-ttu-id="ab154-110">Pour des instructions, voir [Créer un compte Stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="ab154-110">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="ab154-111">Stocké vos données dans un compte de stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="ab154-111">Stored your data in an Azure blob storage account.</span></span> <span data-ttu-id="ab154-112">Si vous avez besoin d’instructions, consultez [tooand de données de déplacement du stockage Azure](../storage/common/storage-moving-data.md)</span><span class="sxs-lookup"><span data-stu-id="ab154-112">If you need instructions, see [Moving data tooand from Azure Storage](../storage/common/storage-moving-data.md)</span></span>

## <a name="load-hello-data-into-a-pandas-dataframe"></a><span data-ttu-id="ab154-113">Charger des données dans une trame de données Pandas hello</span><span class="sxs-lookup"><span data-stu-id="ab154-113">Load hello data into a Pandas DataFrame</span></span>
<span data-ttu-id="ab154-114">tooexplore et manipuler un jeu de données, il doit tout d’abord être téléchargé à partir de hello blob source tooa fichier local, qui peut ensuite être chargé dans une trame de données Pandas.</span><span class="sxs-lookup"><span data-stu-id="ab154-114">tooexplore and manipulate a dataset, it must first be downloaded from hello blob source tooa local file, which can then be loaded in a Pandas DataFrame.</span></span> <span data-ttu-id="ab154-115">Voici toofollow d’étapes hello pour cette procédure :</span><span class="sxs-lookup"><span data-stu-id="ab154-115">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="ab154-116">Télécharger les données de salutation à partir d’Azure blob avec hello suivant l’exemple de code Python à l’aide du service d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="ab154-116">Download hello data from Azure blob with hello following Python code sample using blob service.</span></span> <span data-ttu-id="ab154-117">Remplacez la variable hello Bonjour suivant de code avec les valeurs spécifiques :</span><span class="sxs-lookup"><span data-stu-id="ab154-117">Replace hello variable in hello following code with your specific values:</span></span> 
   
        from azure.storage.blob import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        LOCALFILENAME= <local_file_name>        
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        #download from blob
        t1=time.time()
        blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
        blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILENAME)
        t2=time.time()
        print(("It takes %s seconds toodownload "+blobname) % (t2 - t1))
2. <span data-ttu-id="ab154-118">Lire les données dans une trame de données Pandas de hello hello téléchargement le fichier.</span><span class="sxs-lookup"><span data-stu-id="ab154-118">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="ab154-119">Maintenant vous tooexplore prêt hello données, générez des fonctionnalités sur ce jeu de données.</span><span class="sxs-lookup"><span data-stu-id="ab154-119">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="ab154-120"><a name="blob-dataexploration"></a>Exemples d’exploration de données à l’aide de Pandas</span><span class="sxs-lookup"><span data-stu-id="ab154-120"><a name="blob-dataexploration"></a>Examples of data exploration using Pandas</span></span>
<span data-ttu-id="ab154-121">Voici quelques exemples de méthodes tooexplore les données à l’aide de Pandas :</span><span class="sxs-lookup"><span data-stu-id="ab154-121">Here are a few examples of ways tooexplore data using Pandas:</span></span>

1. <span data-ttu-id="ab154-122">Inspecter hello **nombre de lignes et colonnes**</span><span class="sxs-lookup"><span data-stu-id="ab154-122">Inspect hello **number of rows and columns**</span></span> 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="ab154-123">**Inspecter** hello quelques-uns premier ou derniers **lignes** Bonjour suivant le jeu de données :</span><span class="sxs-lookup"><span data-stu-id="ab154-123">**Inspect** hello first or last few **rows** in hello following dataset:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="ab154-124">Vérifiez hello **type de données** chaque colonne a été importée sous la forme à l’aide de hello suivant l’exemple de code</span><span class="sxs-lookup"><span data-stu-id="ab154-124">Check hello **data type** each column was imported as using hello following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="ab154-125">Vérifiez hello **base statistiques** pour les colonnes hello dans hello le jeu de données comme suit</span><span class="sxs-lookup"><span data-stu-id="ab154-125">Check hello **basic stats** for hello columns in hello data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="ab154-126">Se présenter comme suit au numéro hello des entrées pour chaque valeur de colonne</span><span class="sxs-lookup"><span data-stu-id="ab154-126">Look at hello number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="ab154-127">**Nombre de valeurs manquantes** par rapport au nombre réel de hello d’entrées dans chaque colonne à l’aide de hello suivant l’exemple de code</span><span class="sxs-lookup"><span data-stu-id="ab154-127">**Count missing values** versus hello actual number of entries in each column using hello following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="ab154-128">Si vous avez **les valeurs manquantes** pour une colonne spécifique dans les données de salutation, vous pouvez les supprimer comme suit :</span><span class="sxs-lookup"><span data-stu-id="ab154-128">If you have **missing values** for a specific column in hello data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="ab154-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="ab154-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="ab154-130">Les valeurs manquantes une autre façon tooreplace est fonction du mode hello :</span><span class="sxs-lookup"><span data-stu-id="ab154-130">Another way tooreplace missing values is with hello mode function:</span></span>
   
     <span data-ttu-id="ab154-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<nom_colonne>':dataframe_blobdata['<nom_colonne>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="ab154-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="ab154-132">Créer un **histogramme** tracer à l’aide d’un nombre variable de distribution de hello tooplot emplacements d’une variable</span><span class="sxs-lookup"><span data-stu-id="ab154-132">Create a **histogram** plot using variable number of bins tooplot hello distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="ab154-133">Examinez **corrélations** entre les variables à l’aide d’un scatterplot ou à l’aide de la fonction de corrélation intégrée hello</span><span class="sxs-lookup"><span data-stu-id="ab154-133">Look at **correlations** between variables using a scatterplot or using hello built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

