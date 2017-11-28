---
title: "stockage d’objets blob aaaSample des données dans Azure | Documents Microsoft"
description: "Échantillonner des données dans le stockage d’objets blob Azure"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8d9ad2c-86c5-43d6-80b8-d355b5c0dccf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: cceadf1fb1fb4804fc5b5a3da55c82854651026e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="cf550-103"><a name="heading"></a>Échantillonner des données dans le stockage d’objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="cf550-103"><a name="heading"></a>Sample data in Azure blob storage</span></span>
<span data-ttu-id="cf550-104">Ce document traite de l’échantillonnage des données conservées dans le stockage d’objets blob Azure par le biais du téléchargement de ces données par programmation, puis de leur échantillonnage à l’aide de procédures écrites dans Python.</span><span class="sxs-lookup"><span data-stu-id="cf550-104">This document covers sampling data stored in Azure blob storage by downloading it programmatically and then sampling it using procedures written in Python.</span></span>

<span data-ttu-id="cf550-105">suivant de Hello **menu** lie tootopics qui décrivent comment toosample des données à partir de différents environnements de stockage.</span><span class="sxs-lookup"><span data-stu-id="cf550-105">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="cf550-106">**Pourquoi échantillonner vos données ?**</span><span class="sxs-lookup"><span data-stu-id="cf550-106">**Why sample your data?**</span></span>
<span data-ttu-id="cf550-107">Si dataset hello vous envisagez de tooanalyze est grand, il est généralement un tooreduce de données recommandé toodown-exemple hello il tooa plus petite mais représentatif et plus facile à gérer la taille.</span><span class="sxs-lookup"><span data-stu-id="cf550-107">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="cf550-108">Cette opération facilite la compréhension et l’exploration des données, ainsi que la conception de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="cf550-108">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="cf550-109">Son rôle dans hello Cortana Analytique processus est tooenable le prototypage rapide des fonctions de traitement des données de hello et modèles d’apprentissage automatique.</span><span class="sxs-lookup"><span data-stu-id="cf550-109">Its role in hello Cortana Analytics Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="cf550-110">Cette tâche d’échantillonnage est une étape Bonjour [processus de science des données équipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="cf550-110">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="download-and-down-sample-data"></a><span data-ttu-id="cf550-111">Télécharger et sous-échantillonner les données</span><span class="sxs-lookup"><span data-stu-id="cf550-111">Download and down-sample data</span></span>
1. <span data-ttu-id="cf550-112">Télécharger les données de salutation à partir du stockage d’objets blob Azure à l’aide du service d’objets blob hello hello suivant l’exemple de code Python à partir de :</span><span class="sxs-lookup"><span data-stu-id="cf550-112">Download hello data from Azure blob storage using hello blob service from hello following sample Python code:</span></span> 
   
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

2. <span data-ttu-id="cf550-113">Lire les données dans une trame de données Pandas à partir du fichier hello téléchargé.</span><span class="sxs-lookup"><span data-stu-id="cf550-113">Read data into a Pandas data-frame from hello file downloaded above.</span></span>
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. <span data-ttu-id="cf550-114">Bas-exemple données hello à l’aide de hello `numpy`de `random.choice` comme suit :</span><span class="sxs-lookup"><span data-stu-id="cf550-114">Down-sample hello data using hello `numpy`'s `random.choice` as follows:</span></span>
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

<span data-ttu-id="cf550-115">Vous pouvez maintenant travailler avec hello au-dessus de trame de données avec l’exemple de 1 pour cent hello pour une exploration plus approfondie et la génération de la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="cf550-115">Now you can work with hello above data frame with hello 1 Percent sample for further exploration and feature generation.</span></span>

## <span data-ttu-id="cf550-116"><a name="heading"></a>Télécharger les données et les lire dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="cf550-116"><a name="heading"></a>Upload data and read it into Azure Machine Learning</span></span>
<span data-ttu-id="cf550-117">Vous pouvez utiliser hello exemple code toodown-exemple hello données suivantes et l’utiliser directement dans Azure Machine Learning :</span><span class="sxs-lookup"><span data-stu-id="cf550-117">You can use hello following sample code toodown-sample hello data and use it directly in Azure Machine Learning:</span></span>

1. <span data-ttu-id="cf550-118">Écrire le fichier local de hello données frame tooa</span><span class="sxs-lookup"><span data-stu-id="cf550-118">Write hello data frame tooa local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. <span data-ttu-id="cf550-119">Télécharger hello fichier local tooan Azure blob à l’aide de hello suivant l’exemple de code :</span><span class="sxs-lookup"><span data-stu-id="cf550-119">Upload hello local file tooan Azure blob using hello following sample code:</span></span>
   
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
            print ("Something went wrong with uploading toohello blob:"+ BLOBNAME)

3. <span data-ttu-id="cf550-120">Lire les données de hello hello blob Azure à l’aide d’Azure Machine Learning [importer des données](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) comme indiqué dans l’image hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="cf550-120">Read hello data from hello Azure blob using Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) as shown in hello image below:</span></span>

![objet blob de lecteur](./media/machine-learning-data-science-sample-data-blob/reader_blob.png)

