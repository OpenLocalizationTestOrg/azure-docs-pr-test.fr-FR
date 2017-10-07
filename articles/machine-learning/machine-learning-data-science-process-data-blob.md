---
title: "données à l’aide d’analytique avancée d’objets blob aaaProcess Azure | Documents Microsoft"
description: "Traitez les données dans un stockage d’objets blob Azure."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8a59078-91d3-4440-b85c-430363c3f4d1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5911d4211c4135680555a8cdd99e745499a24215
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>Traitement des données d’objets blob Azure avec des analyses de données avancées
Ce document concerne l’exploration des données et la génération de fonctionnalités à partir de données stockées dans le stockage d’objets blob. 

## <a name="load-hello-data-into-a-pandas-data-frame"></a>Charger des données dans une trame de données Pandas hello
Dans l’ordre tooexplore et manipuler un jeu de données, il doit être téléchargé à partir de hello blob source tooa fichier local qui peut ensuite être chargé dans une trame de données Pandas. Voici toofollow d’étapes hello pour cette procédure :

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

## <a name="blob-dataexploration"></a>Exploration des données
Voici quelques exemples de méthodes tooexplore les données à l’aide de Pandas :

1. Inspecter le nombre de hello de lignes et colonnes 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. Inspecter hello premier ou dernier peu de lignes dans le jeu de données hello comme indiqué ci-dessous :
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. Vérifier le type de données hello que chaque colonne a été importée sous la forme à l’aide de hello suivant l’exemple de code
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. Vérifier les statistiques de base hello pour les colonnes dans le jeu de données hello hello procédez comme suit
   
        dataframe_blobdata.describe()
5. Se présenter comme suit au numéro hello des entrées pour chaque valeur de colonne
   
        dataframe_blobdata['<column_name>'].value_counts()
6. Nombre de valeurs manquantes par rapport au nombre réel de hello d’entrées dans chaque colonne à l’aide de hello suivant l’exemple de code
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. Si vous avez des valeurs manquantes pour une colonne spécifique dans les données de salutation, vous pouvez les supprimer comme suit :
   
     dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape
   
   Les valeurs manquantes une autre façon tooreplace est fonction du mode hello :
   
     dataframe_blobdata_mode = dataframe_blobdata.fillna({'<nom_colonne>':dataframe_blobdata['<nom_colonne>'].mode()[0]})        
8. Créer un tracé de l’histogramme à l’aide d’un nombre variable de distribution de hello tooplot emplacements d’une variable    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. Examinez les corrélations entre les variables à l’aide d’un scatterplot ou à l’aide de la fonction de corrélation intégrée hello
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <a name="blob-featuregen"></a>Génération de fonctionnalités
Pour générer des caractéristiques à l’aide de Python, procédez comme suit :

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
3. À présent les données de salutation peuvent être lu à l’aide des objets blob hello hello Azure Machine Learning [importer des données] [ import-data] module, comme indiqué dans l’écran hello ci-dessous :

![objet blob de lecteur][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

