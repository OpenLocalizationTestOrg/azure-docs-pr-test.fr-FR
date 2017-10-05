---
title: "Échantillonner des données dans le stockage d'objets blob Azure | Microsoft Docs"
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
ms.openlocfilehash: aa9ab454706429682a393c3d5758cebe20790e19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="3a609-103"><a name="heading"></a>Échantillonner des données dans le stockage d’objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="3a609-103"><a name="heading"></a>Sample data in Azure blob storage</span></span>
<span data-ttu-id="3a609-104">Ce document traite de l’échantillonnage des données conservées dans le stockage d’objets blob Azure par le biais du téléchargement de ces données par programmation, puis de leur échantillonnage à l’aide de procédures écrites dans Python.</span><span class="sxs-lookup"><span data-stu-id="3a609-104">This document covers sampling data stored in Azure blob storage by downloading it programmatically and then sampling it using procedures written in Python.</span></span>

<span data-ttu-id="3a609-105">Le **menu** ci-après pointe vers des rubriques qui expliquent comment échantillonner des données dans différents environnements de stockage.</span><span class="sxs-lookup"><span data-stu-id="3a609-105">The following **menu** links to topics that describe how to sample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="3a609-106">**Pourquoi échantillonner vos données ?**</span><span class="sxs-lookup"><span data-stu-id="3a609-106">**Why sample your data?**</span></span>
<span data-ttu-id="3a609-107">Si vous prévoyez d’analyser un jeu de données volumineux, il est généralement recommandé de sous-échantillonner les données afin de réduire leur taille sous une forme plus facilement exploitable, mais toujours représentative.</span><span class="sxs-lookup"><span data-stu-id="3a609-107">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="3a609-108">Cette opération facilite la compréhension et l’exploration des données, ainsi que la conception de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="3a609-108">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="3a609-109">Son rôle dans le processus Cortana Analytics consiste à permettre le prototypage rapide des fonctions de traitement des données et des modèles d’apprentissage automatique.</span><span class="sxs-lookup"><span data-stu-id="3a609-109">Its role in the Cortana Analytics Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

<span data-ttu-id="3a609-110">Cette tâche d’échantillonnage est une étape du [processus TDSP (Team Data Science Process)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="3a609-110">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="download-and-down-sample-data"></a><span data-ttu-id="3a609-111">Télécharger et sous-échantillonner les données</span><span class="sxs-lookup"><span data-stu-id="3a609-111">Download and down-sample data</span></span>
1. <span data-ttu-id="3a609-112">Téléchargez les données du stockage d’objets blob Azure à l’aide du service BLOB en utilisant l’exemple de code suivant :</span><span class="sxs-lookup"><span data-stu-id="3a609-112">Download the data from Azure blob storage using the blob service from the following sample Python code:</span></span> 
   
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

2. <span data-ttu-id="3a609-113">Lisez les données dans une trame de données pandas à partir du fichier téléchargé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="3a609-113">Read data into a Pandas data-frame from the file downloaded above.</span></span>
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. <span data-ttu-id="3a609-114">Sous-échantillonnez les données en utilisant l’élément `random.choice` de `numpy`, comme suit :</span><span class="sxs-lookup"><span data-stu-id="3a609-114">Down-sample the data using the `numpy`'s `random.choice` as follows:</span></span>
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

<span data-ttu-id="3a609-115">Vous pouvez à présent travailler sur l’échantillon de 1 % de la trame de données ci-dessus à d’autres fins d’exploration et de génération de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="3a609-115">Now you can work with the above data frame with the 1 Percent sample for further exploration and feature generation.</span></span>

## <span data-ttu-id="3a609-116"><a name="heading"></a>Télécharger les données et les lire dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3a609-116"><a name="heading"></a>Upload data and read it into Azure Machine Learning</span></span>
<span data-ttu-id="3a609-117">Vous pouvez sous-échantillonner les données et les utiliser directement dans Azure Machine Learning en utilisant l’exemple de code ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3a609-117">You can use the following sample code to down-sample the data and use it directly in Azure Machine Learning:</span></span>

1. <span data-ttu-id="3a609-118">Écrivez la trame de données dans un fichier local :</span><span class="sxs-lookup"><span data-stu-id="3a609-118">Write the data frame to a local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. <span data-ttu-id="3a609-119">Chargez le fichier local dans un objet blob Azure au moyen de l’exemple de code suivant :</span><span class="sxs-lookup"><span data-stu-id="3a609-119">Upload the local file to an Azure blob using the following sample code:</span></span>
   
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
            print ("Something went wrong with uploading to the blob:"+ BLOBNAME)

3. <span data-ttu-id="3a609-120">Lisez les données de l’objet blob Azure à l’aide du module [Importer les données](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) Azure Machine Learning, comme l’illustre l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3a609-120">Read the data from the Azure blob using Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) as shown in the image below:</span></span>

![objet blob de lecteur](./media/machine-learning-data-science-sample-data-blob/reader_blob.png)

