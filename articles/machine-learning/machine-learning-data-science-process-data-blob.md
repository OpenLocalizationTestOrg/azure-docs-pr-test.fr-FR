---
title: "Traitement des données d’objets blob Azure avec l’analytique avancée | Microsoft Docs"
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
ms.openlocfilehash: 36d950fd81029af82d9f2f652b2f01dba5fc8cc9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="9d667-103"><a name="heading"></a>Traitement des données d’objets blob Azure avec des analyses de données avancées</span><span class="sxs-lookup"><span data-stu-id="9d667-103"><a name="heading"></a>Process Azure blob data with advanced analytics</span></span>
<span data-ttu-id="9d667-104">Ce document concerne l’exploration des données et la génération de fonctionnalités à partir de données stockées dans le stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="9d667-104">This document covers exploring data and generating features from data stored in Azure Blob storage.</span></span> 

## <a name="load-the-data-into-a-pandas-data-frame"></a><span data-ttu-id="9d667-105">Chargement des données dans une trame de données Pandas</span><span class="sxs-lookup"><span data-stu-id="9d667-105">Load the data into a Pandas data frame</span></span>
<span data-ttu-id="9d667-106">Pour explorer et manipuler un jeu de données, celui-ci doit être téléchargé depuis la source Blob vers un fichier local qui peut ensuite être chargé dans une trame de données Pandas.</span><span class="sxs-lookup"><span data-stu-id="9d667-106">In order to explore and manipulate a dataset, it must be downloaded from the blob source to a local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="9d667-107">Voici les étapes à suivre pour cette procédure :</span><span class="sxs-lookup"><span data-stu-id="9d667-107">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="9d667-108">Téléchargez les données à partir du blob Azure avec l’exemple de code Python à l’aide du service du blob.</span><span class="sxs-lookup"><span data-stu-id="9d667-108">Download the data from Azure blob with the following sample Python code using blob service.</span></span> <span data-ttu-id="9d667-109">Remplacez la variable dans le code ci-dessous par vos propres valeurs :</span><span class="sxs-lookup"><span data-stu-id="9d667-109">Replace the variable in the code below with your specific values:</span></span> 
   
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
2. <span data-ttu-id="9d667-110">Lisez les données du fichier téléchargé dans une table Pandas.</span><span class="sxs-lookup"><span data-stu-id="9d667-110">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="9d667-111">Vous êtes maintenant prêt à explorer les données et à générer des fonctionnalités sur cet ensemble de données.</span><span class="sxs-lookup"><span data-stu-id="9d667-111">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <span data-ttu-id="9d667-112"><a name="blob-dataexploration"></a>Exploration des données</span><span class="sxs-lookup"><span data-stu-id="9d667-112"><a name="blob-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="9d667-113">Voici quelques méthodes pour explorer des données à l’aide de Pandas :</span><span class="sxs-lookup"><span data-stu-id="9d667-113">Here are a few examples of ways to explore data using Pandas:</span></span>

1. <span data-ttu-id="9d667-114">Vérifiez le nombre de lignes et de colonnes.</span><span class="sxs-lookup"><span data-stu-id="9d667-114">Inspect the number of rows and columns</span></span> 
   
        print 'the size of the data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="9d667-115">Vérifiez les premières ou dernières lignes de l’ensemble de données, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="9d667-115">Inspect the first or last few rows in the dataset as below:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="9d667-116">Vérifiez le type de données dans lequel chaque colonne a été importée, à l’aide du code suivant :</span><span class="sxs-lookup"><span data-stu-id="9d667-116">Check the data type each column was imported as using the following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="9d667-117">Vérifiez les statistiques de base des colonnes dans l’ensemble de données, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="9d667-117">Check the basic stats for the columns in the data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="9d667-118">Regardez le nombre d’entrées pour chaque valeur de colonne, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="9d667-118">Look at the number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="9d667-119">Comptez les valeurs manquantes par rapport au nombre réel d’entrées dans chaque colonne, à l’aide du code suivant :</span><span class="sxs-lookup"><span data-stu-id="9d667-119">Count missing values versus the actual number of entries in each column using the following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="9d667-120">Si des valeurs sont manquantes dans une colonne spécifique, vous pouvez les supprimer comme suit :</span><span class="sxs-lookup"><span data-stu-id="9d667-120">If you have missing values for a specific column in the data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="9d667-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="9d667-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="9d667-122">L’autre solution pour remplacer les valeurs manquantes consiste à utiliser la fonction mode :</span><span class="sxs-lookup"><span data-stu-id="9d667-122">Another way to replace missing values is with the mode function:</span></span>
   
     <span data-ttu-id="9d667-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<nom_colonne>':dataframe_blobdata['<nom_colonne>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="9d667-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="9d667-124">Créez un histogramme à l’aide d’un nombre variable de compartiments pour tracer la distribution d’une variable :</span><span class="sxs-lookup"><span data-stu-id="9d667-124">Create a histogram plot using variable number of bins to plot the distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="9d667-125">Examinez les corrélations entre les variables à l’aide d’un nuage de points ou de la fonction de corrélation intégrée :</span><span class="sxs-lookup"><span data-stu-id="9d667-125">Look at correlations between variables using a scatterplot or using the built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <span data-ttu-id="9d667-126"><a name="blob-featuregen"></a>Génération de fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="9d667-126"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="9d667-127">Pour générer des caractéristiques à l’aide de Python, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9d667-127">We can generate features using Python as follows:</span></span>

### <span data-ttu-id="9d667-128"><a name="blob-countfeature"></a>Génération de caractéristiques à partir de valeurs d’indicateur</span><span class="sxs-lookup"><span data-stu-id="9d667-128"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="9d667-129">Pour créer des caractéristiques de catégorie, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9d667-129">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="9d667-130">Examinez la distribution de la colonne de catégorie :</span><span class="sxs-lookup"><span data-stu-id="9d667-130">Inspect the distribution of the categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="9d667-131">Générez les valeurs d’indicateur pour chacune des valeurs de colonne :</span><span class="sxs-lookup"><span data-stu-id="9d667-131">Generate indicator values for each of the column values</span></span>
   
        #generate the indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="9d667-132">Créez une jointure entre la colonne d’indicateurs et le bloc de données d’origine :</span><span class="sxs-lookup"><span data-stu-id="9d667-132">Join the indicator column with the original data frame</span></span> 
   
            #Join the dummy variables back to the original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="9d667-133">Supprimez la variable d’origine :</span><span class="sxs-lookup"><span data-stu-id="9d667-133">Remove the original variable itself:</span></span>
   
        #Remove the original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="9d667-134"><a name="blob-binningfeature"></a>Génération de caractéristiques de compartimentage</span><span class="sxs-lookup"><span data-stu-id="9d667-134"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="9d667-135">Pour générer des fonctionnalités compartimentées, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9d667-135">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="9d667-136">Ajoutez une séquence de colonnes pour compartimenter une colonne numérique :</span><span class="sxs-lookup"><span data-stu-id="9d667-136">Add a sequence of columns to bin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="9d667-137">Convertissez le compartimentage en une séquence de variables booléennes :</span><span class="sxs-lookup"><span data-stu-id="9d667-137">Convert binning to a sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="9d667-138">Enfin, créez une jointure entre les variables factices et le bloc de données d’origine :</span><span class="sxs-lookup"><span data-stu-id="9d667-138">Finally, Join the dummy variables back to the original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)    

## <span data-ttu-id="9d667-139"><a name="sql-featuregen"></a>Réécriture de données dans l’objet blob Azure et exploitation dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9d667-139"><a name="sql-featuregen"></a>Writing data back to Azure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="9d667-140">Après avoir exploré les données et créé les fonctionnalités nécessaires, vous pouvez charger les données (exemples ou caractéristiques) dans un objet blob Azure et les exploiter dans Azure Machine Learning en procédant comme suit : notez qu’il est également possible de créer d’autres fonctionnalités dans Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="9d667-140">After you have explored the data and created the necessary features, you can upload the data (sampled or featurized) to an Azure blob and consume it in Azure Machine Learning using the following steps: Note that additional features can be created in the Azure Machine Learning Studio as well.</span></span> 

1. <span data-ttu-id="9d667-141">Écrivez le bloc de données dans le fichier local.</span><span class="sxs-lookup"><span data-stu-id="9d667-141">Write the data frame to local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="9d667-142">Chargez les données dans le blob Azure, en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="9d667-142">Upload the data to Azure blob as follows:</span></span>
   
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
3. <span data-ttu-id="9d667-143">À présent, les données sont lisibles à partir de l’objet blob à l’aide du module [Importer des données][import-data] d’Azure Machine Learning comme le montre l’écran ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="9d667-143">Now the data can be read from the blob using the Azure Machine Learning [Import Data][import-data] module as shown in the screen below:</span></span>

![objet blob de lecteur][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

