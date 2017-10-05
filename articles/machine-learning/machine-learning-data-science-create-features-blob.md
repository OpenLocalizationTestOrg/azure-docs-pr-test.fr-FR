---
title: "Créer des fonctionnalités pour les données de stockage d’objets blob Azure à l’aide de Pandas | Microsoft Docs"
description: "Comment créer des fonctionnalités pour les données stockées dans un conteneur d’objets blob Azure avec le package Python Pandas."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 676b5fb0-4c89-4516-b3a8-e78ae3ca078d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;garye
ms.openlocfilehash: 2ef2acfea2372ac7fd52d099a2b4203ee2242d81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a><span data-ttu-id="89445-103">Créer des fonctionnalités pour les données de stockage d’objets blob Azure à l’aide de Pandas</span><span class="sxs-lookup"><span data-stu-id="89445-103">Create features for Azure blob storage data using Panda</span></span>
<span data-ttu-id="89445-104">Ce document montre comment créer des fonctionnalités pour les données stockées dans un conteneur d’objets blob Azure à l’aide du package Python [Pandas](http://pandas.pydata.org/) .</span><span class="sxs-lookup"><span data-stu-id="89445-104">This document shows how to create features for data that is stored in Azure blob container using the [Pandas](http://pandas.pydata.org/) Python package.</span></span> <span data-ttu-id="89445-105">Après avoir décrit le chargement des données dans une trame de données Pandas, il montre comment générer des fonctionnalités catégorielles à l’aide de scripts Python avec des valeurs d’indicateur et des caractéristiques de compartimentage.</span><span class="sxs-lookup"><span data-stu-id="89445-105">After outlining how to load the data into a Panda data frame, it shows how to generate categorical features using Python scripts with indicator values and binning features.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="89445-106">Ce **menu** pointe vers des rubriques qui expliquent comment créer des fonctionnalités pour les données dans différents environnements.</span><span class="sxs-lookup"><span data-stu-id="89445-106">This **menu** links to topics that describe how to create features for data in various environments.</span></span> <span data-ttu-id="89445-107">Cette tâche est une étape du [processus TDSP (Team Data Science Process)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="89445-107">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89445-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="89445-108">Prerequisites</span></span>
<span data-ttu-id="89445-109">Cet article part du principe que vous avez créé un compte de stockage d’objets blob Azure et que vous y avez stocké vos données.</span><span class="sxs-lookup"><span data-stu-id="89445-109">This article assumes that you have created an Azure blob storage account and have stored your data there.</span></span> <span data-ttu-id="89445-110">Si vous avez besoin d’instructions pour configurer un compte, voir [Créer un compte Stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="89445-110">If you need instructions to set up an account, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>

## <a name="load-the-data-into-a-pandas-data-frame"></a><span data-ttu-id="89445-111">Chargement des données dans une trame de données Pandas</span><span class="sxs-lookup"><span data-stu-id="89445-111">Load the data into a Pandas data frame</span></span>
<span data-ttu-id="89445-112">Pour explorer et manipuler un jeu de données, celui-ci doit être téléchargé depuis la source Blob vers un fichier local qui peut ensuite être chargé dans une trame de données Pandas.</span><span class="sxs-lookup"><span data-stu-id="89445-112">In order to do explore and manipulate a dataset, it must be downloaded from the blob source to a local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="89445-113">Voici les étapes à suivre pour cette procédure :</span><span class="sxs-lookup"><span data-stu-id="89445-113">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="89445-114">Téléchargez les données à partir du blob Azure avec l’exemple de code Python à l’aide du service du blob.</span><span class="sxs-lookup"><span data-stu-id="89445-114">Download the data from Azure blob with the following sample Python code using blob service.</span></span> <span data-ttu-id="89445-115">Remplacez la variable dans le code ci-dessous par vos propres valeurs :</span><span class="sxs-lookup"><span data-stu-id="89445-115">Replace the variable in the code below with your specific values:</span></span>
   
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
        print(("It takes %s seconds to download "+blobname) % (t2 - t1))
2. <span data-ttu-id="89445-116">Lisez les données du fichier téléchargé dans une table Pandas.</span><span class="sxs-lookup"><span data-stu-id="89445-116">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="89445-117">Vous êtes maintenant prêt à explorer les données et à générer des fonctionnalités sur cet ensemble de données.</span><span class="sxs-lookup"><span data-stu-id="89445-117">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <span data-ttu-id="89445-118"><a name="blob-featuregen"></a>Génération de fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="89445-118"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="89445-119">Les deux sections suivantes indiquent comment générer des fonctionnalités catégorielles avec des valeurs d’indicateur et des caractéristiques de compartimentage à l’aide de scripts Python.</span><span class="sxs-lookup"><span data-stu-id="89445-119">The next two sections show how to generate categorical features with indicator values and binning features using Python scripts.</span></span>

### <span data-ttu-id="89445-120"><a name="blob-countfeature"></a>Génération de caractéristiques à partir de valeurs d’indicateur</span><span class="sxs-lookup"><span data-stu-id="89445-120"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="89445-121">Pour créer des caractéristiques de catégorie, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="89445-121">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="89445-122">Examinez la distribution de la colonne de catégorie :</span><span class="sxs-lookup"><span data-stu-id="89445-122">Inspect the distribution of the categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="89445-123">Générez les valeurs d’indicateur pour chacune des valeurs de colonne :</span><span class="sxs-lookup"><span data-stu-id="89445-123">Generate indicator values for each of the column values</span></span>
   
        #generate the indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="89445-124">Créez une jointure entre la colonne d’indicateurs et le bloc de données d’origine :</span><span class="sxs-lookup"><span data-stu-id="89445-124">Join the indicator column with the original data frame</span></span>
   
            #Join the dummy variables back to the original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="89445-125">Supprimez la variable d’origine :</span><span class="sxs-lookup"><span data-stu-id="89445-125">Remove the original variable itself:</span></span>
   
        #Remove the original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="89445-126"><a name="blob-binningfeature"></a>Génération de caractéristiques de compartimentage</span><span class="sxs-lookup"><span data-stu-id="89445-126"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="89445-127">Pour générer des fonctionnalités compartimentées, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="89445-127">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="89445-128">Ajoutez une séquence de colonnes pour compartimenter une colonne numérique :</span><span class="sxs-lookup"><span data-stu-id="89445-128">Add a sequence of columns to bin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="89445-129">Convertissez le compartimentage en une séquence de variables booléennes :</span><span class="sxs-lookup"><span data-stu-id="89445-129">Convert binning to a sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="89445-130">Enfin, créez une jointure entre les variables factices et le bloc de données d’origine :</span><span class="sxs-lookup"><span data-stu-id="89445-130">Finally, Join the dummy variables back to the original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <span data-ttu-id="89445-131"><a name="sql-featuregen"></a>Réécriture de données dans l’objet blob Azure et exploitation dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="89445-131"><a name="sql-featuregen"></a>Writing data back to Azure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="89445-132">Après avoir exploré les données et créé les fonctionnalités nécessaires, vous pouvez charger les données (exemples ou caractéristiques) dans un objet blob Azure et les exploiter dans Azure Machine Learning en procédant comme suit : notez qu’il est également possible de créer d’autres fonctionnalités dans Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="89445-132">After you have explored the data and created the necessary features, you can upload the data (sampled or featurized) to an Azure blob and consume it in Azure Machine Learning using the following steps: Note that additional features can be created in the Azure Machine Learning Studio as well.</span></span>

1. <span data-ttu-id="89445-133">Écrivez le bloc de données dans le fichier local.</span><span class="sxs-lookup"><span data-stu-id="89445-133">Write the data frame to local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="89445-134">Chargez les données dans le blob Azure, en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="89445-134">Upload the data to Azure blob as follows:</span></span>
   
        from azure.storage.blob import BlobService
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
3. <span data-ttu-id="89445-135">À présent, les données sont lisibles à partir de l’objet blob à l’aide du module [Importer des données](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) d’Azure Machine Learning comme le montre l’écran ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="89445-135">Now the data can be read from the blob using the Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module as shown in the screen below:</span></span>

![objet blob de lecteur](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

