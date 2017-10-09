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
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a>Explorer les données dans le stockage d’objets blob Azure avec Pandas
Ce document décrit comment tooexplore les données stockées dans Azure blob à l’aide du conteneur [Pandas](http://pandas.pydata.org/) package Python.

suivant de Hello **menu** tootopics qui décrivent comment toouse outils tooexplore des données à partir de différents environnements de stockage est liée. Cette tâche est une étape Bonjour [processus de science des données]().

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a>Composants requis
Cet article suppose que vous avez :

* Créé un compte Azure Storage. Pour des instructions, voir [Créer un compte Stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account).
* Stocké vos données dans un compte de stockage d’objets blob Azure. Si vous avez besoin d’instructions, consultez [tooand de données de déplacement du stockage Azure](../storage/common/storage-moving-data.md)

## <a name="load-hello-data-into-a-pandas-dataframe"></a>Charger des données dans une trame de données Pandas hello
tooexplore et manipuler un jeu de données, il doit tout d’abord être téléchargé à partir de hello blob source tooa fichier local, qui peut ensuite être chargé dans une trame de données Pandas. Voici toofollow d’étapes hello pour cette procédure :

1. Télécharger les données de salutation à partir d’Azure blob avec hello suivant l’exemple de code Python à l’aide du service d’objets blob. Remplacez la variable hello Bonjour suivant de code avec les valeurs spécifiques : 
   
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

## <a name="blob-dataexploration"></a>Exemples d’exploration de données à l’aide de Pandas
Voici quelques exemples de méthodes tooexplore les données à l’aide de Pandas :

1. Inspecter hello **nombre de lignes et colonnes** 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. **Inspecter** hello quelques-uns premier ou derniers **lignes** Bonjour suivant le jeu de données :
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. Vérifiez hello **type de données** chaque colonne a été importée sous la forme à l’aide de hello suivant l’exemple de code
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. Vérifiez hello **base statistiques** pour les colonnes hello dans hello le jeu de données comme suit
   
        dataframe_blobdata.describe()
5. Se présenter comme suit au numéro hello des entrées pour chaque valeur de colonne
   
        dataframe_blobdata['<column_name>'].value_counts()
6. **Nombre de valeurs manquantes** par rapport au nombre réel de hello d’entrées dans chaque colonne à l’aide de hello suivant l’exemple de code
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. Si vous avez **les valeurs manquantes** pour une colonne spécifique dans les données de salutation, vous pouvez les supprimer comme suit :
   
     dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape
   
   Les valeurs manquantes une autre façon tooreplace est fonction du mode hello :
   
     dataframe_blobdata_mode = dataframe_blobdata.fillna({'<nom_colonne>':dataframe_blobdata['<nom_colonne>'].mode()[0]})        
8. Créer un **histogramme** tracer à l’aide d’un nombre variable de distribution de hello tooplot emplacements d’une variable    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. Examinez **corrélations** entre les variables à l’aide d’un scatterplot ou à l’aide de la fonction de corrélation intégrée hello
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

