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
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a>Créer des fonctionnalités pour les données de stockage d’objets blob Azure à l’aide de Pandas
Ce document montre comment les fonctionnalités pour les données stockées dans le conteneur d’objets blob Azure à l’aide de hello toocreate [Pandas](http://pandas.pydata.org/) package Python. Après le mode plan comment tooload hello des données dans une trame de données Panda, il montre comment toogenerate les fonctionnalités par catégorie à l’aide de scripts Python avec les valeurs d’indicateur et placement des fonctionnalités.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Cela **menu** lie tootopics qui décrivent comment toocreate pour les données dans différents environnements. Cette tâche est une étape Bonjour [processus de science des données équipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="prerequisites"></a>Composants requis
Cet article part du principe que vous avez créé un compte de stockage d’objets blob Azure et que vous y avez stocké vos données. Si vous avez besoin de tooset d’instructions d’un compte, consultez [créer un compte de stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)

## <a name="load-hello-data-into-a-pandas-data-frame"></a>Charger des données dans une trame de données Pandas hello
Dans l’ordre toodo examiner et manipuler un jeu de données, il doit être téléchargé à partir de hello blob source tooa fichier local qui peut ensuite être chargé dans une trame de données Pandas. Voici toofollow d’étapes hello pour cette procédure :

1. Télécharger les données de salutation à partir d’Azure blob avec hello suivant l’exemple de code Python à l’aide du service d’objets blob. Remplacez la variable hello dans le code hello ci-dessous avec les valeurs spécifiques :
   
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
2. Lire les données dans une trame de données Pandas de hello hello téléchargement le fichier.
   
        #LOCALFILE is hello file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

Maintenant vous tooexplore prêt hello données, générez des fonctionnalités sur ce jeu de données.

## <a name="blob-featuregen"></a>Génération de fonctionnalités
Hello deux sections suivantes montrent comment toogenerate les fonctionnalités catégorielles avec les valeurs d’indicateur et placement des fonctionnalités à l’aide de scripts Python.

### <a name="blob-countfeature"></a>Génération de caractéristiques à partir de valeurs d’indicateur
Pour créer des caractéristiques de catégorie, procédez comme suit :

1. Examiner la distribution hello de colonne catégorielle de hello :
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. Générer des valeurs d’indicateur pour chacune des valeurs de colonne hello
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. Joindre la colonne d’indicateur hello avec trame de données d’origine hello
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. Supprimer hello d’origine proprement dite :
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <a name="blob-binningfeature"></a>Génération de caractéristiques de compartimentage
Pour générer des fonctionnalités compartimentées, procédez comme suit :

1. Ajouter une séquence de colonnes toobin une colonne numérique
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. Convertir une séquence de tooa placement dans un conteneur de variables booléennes
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. Enfin, de variables de jointure hello factices retour toohello trame de données d’origine
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <a name="sql-featuregen"></a>Écriture de données sauvegarde tooAzure blob et consommé dans Azure Machine Learning
Après avoir exploré les données hello et créé hello fonctionnalités nécessaires, vous pouvez télécharger les données de salutation (échantillonnées ou fonctionnalités) tooan Azure d’objets blob et le consommer dans Azure Machine Learning à l’aide de hello comme suit : Notez que les fonctionnalités supplémentaires peuvent être créées dans hello Azure Machine Learning Studio également.

1. Écrire le fichier de toolocal hello données frame
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. Charger les blob de tooAzure données hello comme suit :
   
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
3. À présent les données de salutation peuvent être lu à l’aide des objets blob hello hello Azure Machine Learning [importer des données](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module, comme indiqué dans l’écran hello ci-dessous :

![objet blob de lecteur](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

