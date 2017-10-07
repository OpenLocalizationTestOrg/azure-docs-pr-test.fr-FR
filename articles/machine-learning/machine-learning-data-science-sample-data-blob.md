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
# <a name="heading"></a>Échantillonner des données dans le stockage d’objets blob Azure
Ce document traite de l’échantillonnage des données conservées dans le stockage d’objets blob Azure par le biais du téléchargement de ces données par programmation, puis de leur échantillonnage à l’aide de procédures écrites dans Python.

suivant de Hello **menu** lie tootopics qui décrivent comment toosample des données à partir de différents environnements de stockage. 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**Pourquoi échantillonner vos données ?**
Si dataset hello vous envisagez de tooanalyze est grand, il est généralement un tooreduce de données recommandé toodown-exemple hello il tooa plus petite mais représentatif et plus facile à gérer la taille. Cette opération facilite la compréhension et l’exploration des données, ainsi que la conception de fonctionnalités. Son rôle dans hello Cortana Analytique processus est tooenable le prototypage rapide des fonctions de traitement des données de hello et modèles d’apprentissage automatique.

Cette tâche d’échantillonnage est une étape Bonjour [processus de science des données équipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="download-and-down-sample-data"></a>Télécharger et sous-échantillonner les données
1. Télécharger les données de salutation à partir du stockage d’objets blob Azure à l’aide du service d’objets blob hello hello suivant l’exemple de code Python à partir de : 
   
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

2. Lire les données dans une trame de données Pandas à partir du fichier hello téléchargé.
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. Bas-exemple données hello à l’aide de hello `numpy`de `random.choice` comme suit :
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

Vous pouvez maintenant travailler avec hello au-dessus de trame de données avec l’exemple de 1 pour cent hello pour une exploration plus approfondie et la génération de la fonctionnalité.

## <a name="heading"></a>Télécharger les données et les lire dans Azure Machine Learning
Vous pouvez utiliser hello exemple code toodown-exemple hello données suivantes et l’utiliser directement dans Azure Machine Learning :

1. Écrire le fichier local de hello données frame tooa
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. Télécharger hello fichier local tooan Azure blob à l’aide de hello suivant l’exemple de code :
   
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

3. Lire les données de hello hello blob Azure à l’aide d’Azure Machine Learning [importer des données](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) comme indiqué dans l’image hello ci-dessous :

![objet blob de lecteur](./media/machine-learning-data-science-sample-data-blob/reader_blob.png)

