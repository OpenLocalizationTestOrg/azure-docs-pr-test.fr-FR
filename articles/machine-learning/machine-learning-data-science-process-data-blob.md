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
# <span data-ttu-id="fbced-103"><a name="heading"></a>Traitement des données d’objets blob Azure avec des analyses de données avancées</span><span class="sxs-lookup"><span data-stu-id="fbced-103"><a name="heading"></a>Process Azure blob data with advanced analytics</span></span>
<span data-ttu-id="fbced-104">Ce document concerne l’exploration des données et la génération de fonctionnalités à partir de données stockées dans le stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="fbced-104">This document covers exploring data and generating features from data stored in Azure Blob storage.</span></span> 

## <a name="load-hello-data-into-a-pandas-data-frame"></a><span data-ttu-id="fbced-105">Charger des données dans une trame de données Pandas hello</span><span class="sxs-lookup"><span data-stu-id="fbced-105">Load hello data into a Pandas data frame</span></span>
<span data-ttu-id="fbced-106">Dans l’ordre tooexplore et manipuler un jeu de données, il doit être téléchargé à partir de hello blob source tooa fichier local qui peut ensuite être chargé dans une trame de données Pandas.</span><span class="sxs-lookup"><span data-stu-id="fbced-106">In order tooexplore and manipulate a dataset, it must be downloaded from hello blob source tooa local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="fbced-107">Voici toofollow d’étapes hello pour cette procédure :</span><span class="sxs-lookup"><span data-stu-id="fbced-107">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="fbced-108">Télécharger les données de salutation à partir d’Azure blob avec hello suivant l’exemple de code Python à l’aide du service d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="fbced-108">Download hello data from Azure blob with hello following sample Python code using blob service.</span></span> <span data-ttu-id="fbced-109">Remplacez la variable hello dans le code hello ci-dessous avec les valeurs spécifiques :</span><span class="sxs-lookup"><span data-stu-id="fbced-109">Replace hello variable in hello code below with your specific values:</span></span> 
   
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
2. <span data-ttu-id="fbced-110">Lire les données dans une trame de données Pandas de hello hello téléchargement le fichier.</span><span class="sxs-lookup"><span data-stu-id="fbced-110">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="fbced-111">Maintenant vous tooexplore prêt hello données, générez des fonctionnalités sur ce jeu de données.</span><span class="sxs-lookup"><span data-stu-id="fbced-111">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="fbced-112"><a name="blob-dataexploration"></a>Exploration des données</span><span class="sxs-lookup"><span data-stu-id="fbced-112"><a name="blob-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="fbced-113">Voici quelques exemples de méthodes tooexplore les données à l’aide de Pandas :</span><span class="sxs-lookup"><span data-stu-id="fbced-113">Here are a few examples of ways tooexplore data using Pandas:</span></span>

1. <span data-ttu-id="fbced-114">Inspecter le nombre de hello de lignes et colonnes</span><span class="sxs-lookup"><span data-stu-id="fbced-114">Inspect hello number of rows and columns</span></span> 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="fbced-115">Inspecter hello premier ou dernier peu de lignes dans le jeu de données hello comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="fbced-115">Inspect hello first or last few rows in hello dataset as below:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="fbced-116">Vérifier le type de données hello que chaque colonne a été importée sous la forme à l’aide de hello suivant l’exemple de code</span><span class="sxs-lookup"><span data-stu-id="fbced-116">Check hello data type each column was imported as using hello following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="fbced-117">Vérifier les statistiques de base hello pour les colonnes dans le jeu de données hello hello procédez comme suit</span><span class="sxs-lookup"><span data-stu-id="fbced-117">Check hello basic stats for hello columns in hello data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="fbced-118">Se présenter comme suit au numéro hello des entrées pour chaque valeur de colonne</span><span class="sxs-lookup"><span data-stu-id="fbced-118">Look at hello number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="fbced-119">Nombre de valeurs manquantes par rapport au nombre réel de hello d’entrées dans chaque colonne à l’aide de hello suivant l’exemple de code</span><span class="sxs-lookup"><span data-stu-id="fbced-119">Count missing values versus hello actual number of entries in each column using hello following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="fbced-120">Si vous avez des valeurs manquantes pour une colonne spécifique dans les données de salutation, vous pouvez les supprimer comme suit :</span><span class="sxs-lookup"><span data-stu-id="fbced-120">If you have missing values for a specific column in hello data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="fbced-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="fbced-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="fbced-122">Les valeurs manquantes une autre façon tooreplace est fonction du mode hello :</span><span class="sxs-lookup"><span data-stu-id="fbced-122">Another way tooreplace missing values is with hello mode function:</span></span>
   
     <span data-ttu-id="fbced-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<nom_colonne>':dataframe_blobdata['<nom_colonne>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="fbced-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="fbced-124">Créer un tracé de l’histogramme à l’aide d’un nombre variable de distribution de hello tooplot emplacements d’une variable</span><span class="sxs-lookup"><span data-stu-id="fbced-124">Create a histogram plot using variable number of bins tooplot hello distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="fbced-125">Examinez les corrélations entre les variables à l’aide d’un scatterplot ou à l’aide de la fonction de corrélation intégrée hello</span><span class="sxs-lookup"><span data-stu-id="fbced-125">Look at correlations between variables using a scatterplot or using hello built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <span data-ttu-id="fbced-126"><a name="blob-featuregen"></a>Génération de fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="fbced-126"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="fbced-127">Pour générer des caractéristiques à l’aide de Python, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fbced-127">We can generate features using Python as follows:</span></span>

### <span data-ttu-id="fbced-128"><a name="blob-countfeature"></a>Génération de caractéristiques à partir de valeurs d’indicateur</span><span class="sxs-lookup"><span data-stu-id="fbced-128"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="fbced-129">Pour créer des caractéristiques de catégorie, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fbced-129">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="fbced-130">Examiner la distribution hello de colonne catégorielle de hello :</span><span class="sxs-lookup"><span data-stu-id="fbced-130">Inspect hello distribution of hello categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="fbced-131">Générer des valeurs d’indicateur pour chacune des valeurs de colonne hello</span><span class="sxs-lookup"><span data-stu-id="fbced-131">Generate indicator values for each of hello column values</span></span>
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="fbced-132">Joindre la colonne d’indicateur hello avec trame de données d’origine hello</span><span class="sxs-lookup"><span data-stu-id="fbced-132">Join hello indicator column with hello original data frame</span></span> 
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="fbced-133">Supprimer hello d’origine proprement dite :</span><span class="sxs-lookup"><span data-stu-id="fbced-133">Remove hello original variable itself:</span></span>
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="fbced-134"><a name="blob-binningfeature"></a>Génération de caractéristiques de compartimentage</span><span class="sxs-lookup"><span data-stu-id="fbced-134"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="fbced-135">Pour générer des fonctionnalités compartimentées, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fbced-135">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="fbced-136">Ajouter une séquence de colonnes toobin une colonne numérique</span><span class="sxs-lookup"><span data-stu-id="fbced-136">Add a sequence of columns toobin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="fbced-137">Convertir une séquence de tooa placement dans un conteneur de variables booléennes</span><span class="sxs-lookup"><span data-stu-id="fbced-137">Convert binning tooa sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="fbced-138">Enfin, de variables de jointure hello factices retour toohello trame de données d’origine</span><span class="sxs-lookup"><span data-stu-id="fbced-138">Finally, Join hello dummy variables back toohello original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)    

## <span data-ttu-id="fbced-139"><a name="sql-featuregen"></a>Écriture de données sauvegarde tooAzure blob et consommé dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="fbced-139"><a name="sql-featuregen"></a>Writing data back tooAzure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="fbced-140">Après avoir exploré les données hello et créé hello fonctionnalités nécessaires, vous pouvez télécharger les données de salutation (échantillonnées ou fonctionnalités) tooan Azure d’objets blob et le consommer dans Azure Machine Learning à l’aide de hello comme suit : Notez que les fonctionnalités supplémentaires peuvent être créées dans hello Azure Machine Learning Studio également.</span><span class="sxs-lookup"><span data-stu-id="fbced-140">After you have explored hello data and created hello necessary features, you can upload hello data (sampled or featurized) tooan Azure blob and consume it in Azure Machine Learning using hello following steps: Note that additional features can be created in hello Azure Machine Learning Studio as well.</span></span> 

1. <span data-ttu-id="fbced-141">Écrire le fichier de toolocal hello données frame</span><span class="sxs-lookup"><span data-stu-id="fbced-141">Write hello data frame toolocal file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="fbced-142">Charger les blob de tooAzure données hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="fbced-142">Upload hello data tooAzure blob as follows:</span></span>
   
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
3. <span data-ttu-id="fbced-143">À présent les données de salutation peuvent être lu à l’aide des objets blob hello hello Azure Machine Learning [importer des données] [ import-data] module, comme indiqué dans l’écran hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="fbced-143">Now hello data can be read from hello blob using hello Azure Machine Learning [Import Data][import-data] module as shown in hello screen below:</span></span>

![objet blob de lecteur][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

