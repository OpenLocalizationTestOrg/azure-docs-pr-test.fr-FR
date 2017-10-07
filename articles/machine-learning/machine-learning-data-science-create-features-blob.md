---
title: "fonctionnalités aaaCreate pour Azure d’objets blob des données de stockage à l’aide de Panda | Documents Microsoft"
description: "Comment toocreate fonctionnalités pour les données stockées dans le conteneur d’objets blob Azure avec le package de Panda Python hello."
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
ms.openlocfilehash: 8594046c5d76a36ad87fc77e407752489d30afcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a><span data-ttu-id="b2202-103">Créer des fonctionnalités pour les données de stockage d’objets blob Azure à l’aide de Pandas</span><span class="sxs-lookup"><span data-stu-id="b2202-103">Create features for Azure blob storage data using Panda</span></span>
<span data-ttu-id="b2202-104">Ce document montre comment les fonctionnalités pour les données stockées dans le conteneur d’objets blob Azure à l’aide de hello toocreate [Pandas](http://pandas.pydata.org/) package Python.</span><span class="sxs-lookup"><span data-stu-id="b2202-104">This document shows how toocreate features for data that is stored in Azure blob container using hello [Pandas](http://pandas.pydata.org/) Python package.</span></span> <span data-ttu-id="b2202-105">Après le mode plan comment tooload hello des données dans une trame de données Panda, il montre comment toogenerate les fonctionnalités par catégorie à l’aide de scripts Python avec les valeurs d’indicateur et placement des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="b2202-105">After outlining how tooload hello data into a Panda data frame, it shows how toogenerate categorical features using Python scripts with indicator values and binning features.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="b2202-106">Cela **menu** lie tootopics qui décrivent comment toocreate pour les données dans différents environnements.</span><span class="sxs-lookup"><span data-stu-id="b2202-106">This **menu** links tootopics that describe how toocreate features for data in various environments.</span></span> <span data-ttu-id="b2202-107">Cette tâche est une étape Bonjour [processus de science des données équipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="b2202-107">This task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2202-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b2202-108">Prerequisites</span></span>
<span data-ttu-id="b2202-109">Cet article part du principe que vous avez créé un compte de stockage d’objets blob Azure et que vous y avez stocké vos données.</span><span class="sxs-lookup"><span data-stu-id="b2202-109">This article assumes that you have created an Azure blob storage account and have stored your data there.</span></span> <span data-ttu-id="b2202-110">Si vous avez besoin de tooset d’instructions d’un compte, consultez [créer un compte de stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="b2202-110">If you need instructions tooset up an account, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>

## <a name="load-hello-data-into-a-pandas-data-frame"></a><span data-ttu-id="b2202-111">Charger des données dans une trame de données Pandas hello</span><span class="sxs-lookup"><span data-stu-id="b2202-111">Load hello data into a Pandas data frame</span></span>
<span data-ttu-id="b2202-112">Dans l’ordre toodo examiner et manipuler un jeu de données, il doit être téléchargé à partir de hello blob source tooa fichier local qui peut ensuite être chargé dans une trame de données Pandas.</span><span class="sxs-lookup"><span data-stu-id="b2202-112">In order toodo explore and manipulate a dataset, it must be downloaded from hello blob source tooa local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="b2202-113">Voici toofollow d’étapes hello pour cette procédure :</span><span class="sxs-lookup"><span data-stu-id="b2202-113">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="b2202-114">Télécharger les données de salutation à partir d’Azure blob avec hello suivant l’exemple de code Python à l’aide du service d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="b2202-114">Download hello data from Azure blob with hello following sample Python code using blob service.</span></span> <span data-ttu-id="b2202-115">Remplacez la variable hello dans le code hello ci-dessous avec les valeurs spécifiques :</span><span class="sxs-lookup"><span data-stu-id="b2202-115">Replace hello variable in hello code below with your specific values:</span></span>
   
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
2. <span data-ttu-id="b2202-116">Lire les données dans une trame de données Pandas de hello hello téléchargement le fichier.</span><span class="sxs-lookup"><span data-stu-id="b2202-116">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="b2202-117">Maintenant vous tooexplore prêt hello données, générez des fonctionnalités sur ce jeu de données.</span><span class="sxs-lookup"><span data-stu-id="b2202-117">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="b2202-118"><a name="blob-featuregen"></a>Génération de fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="b2202-118"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="b2202-119">Hello deux sections suivantes montrent comment toogenerate les fonctionnalités catégorielles avec les valeurs d’indicateur et placement des fonctionnalités à l’aide de scripts Python.</span><span class="sxs-lookup"><span data-stu-id="b2202-119">hello next two sections show how toogenerate categorical features with indicator values and binning features using Python scripts.</span></span>

### <span data-ttu-id="b2202-120"><a name="blob-countfeature"></a>Génération de caractéristiques à partir de valeurs d’indicateur</span><span class="sxs-lookup"><span data-stu-id="b2202-120"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="b2202-121">Pour créer des caractéristiques de catégorie, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b2202-121">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="b2202-122">Examiner la distribution hello de colonne catégorielle de hello :</span><span class="sxs-lookup"><span data-stu-id="b2202-122">Inspect hello distribution of hello categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="b2202-123">Générer des valeurs d’indicateur pour chacune des valeurs de colonne hello</span><span class="sxs-lookup"><span data-stu-id="b2202-123">Generate indicator values for each of hello column values</span></span>
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="b2202-124">Joindre la colonne d’indicateur hello avec trame de données d’origine hello</span><span class="sxs-lookup"><span data-stu-id="b2202-124">Join hello indicator column with hello original data frame</span></span>
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="b2202-125">Supprimer hello d’origine proprement dite :</span><span class="sxs-lookup"><span data-stu-id="b2202-125">Remove hello original variable itself:</span></span>
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="b2202-126"><a name="blob-binningfeature"></a>Génération de caractéristiques de compartimentage</span><span class="sxs-lookup"><span data-stu-id="b2202-126"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="b2202-127">Pour générer des fonctionnalités compartimentées, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b2202-127">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="b2202-128">Ajouter une séquence de colonnes toobin une colonne numérique</span><span class="sxs-lookup"><span data-stu-id="b2202-128">Add a sequence of columns toobin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="b2202-129">Convertir une séquence de tooa placement dans un conteneur de variables booléennes</span><span class="sxs-lookup"><span data-stu-id="b2202-129">Convert binning tooa sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="b2202-130">Enfin, de variables de jointure hello factices retour toohello trame de données d’origine</span><span class="sxs-lookup"><span data-stu-id="b2202-130">Finally, Join hello dummy variables back toohello original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <span data-ttu-id="b2202-131"><a name="sql-featuregen"></a>Écriture de données sauvegarde tooAzure blob et consommé dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="b2202-131"><a name="sql-featuregen"></a>Writing data back tooAzure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="b2202-132">Après avoir exploré les données hello et créé hello fonctionnalités nécessaires, vous pouvez télécharger les données de salutation (échantillonnées ou fonctionnalités) tooan Azure d’objets blob et le consommer dans Azure Machine Learning à l’aide de hello comme suit : Notez que les fonctionnalités supplémentaires peuvent être créées dans hello Azure Machine Learning Studio également.</span><span class="sxs-lookup"><span data-stu-id="b2202-132">After you have explored hello data and created hello necessary features, you can upload hello data (sampled or featurized) tooan Azure blob and consume it in Azure Machine Learning using hello following steps: Note that additional features can be created in hello Azure Machine Learning Studio as well.</span></span>

1. <span data-ttu-id="b2202-133">Écrire le fichier de toolocal hello données frame</span><span class="sxs-lookup"><span data-stu-id="b2202-133">Write hello data frame toolocal file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="b2202-134">Charger les blob de tooAzure données hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b2202-134">Upload hello data tooAzure blob as follows:</span></span>
   
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
3. <span data-ttu-id="b2202-135">À présent les données de salutation peuvent être lu à l’aide des objets blob hello hello Azure Machine Learning [importer des données](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module, comme indiqué dans l’écran hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b2202-135">Now hello data can be read from hello blob using hello Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module as shown in hello screen below:</span></span>

![objet blob de lecteur](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

