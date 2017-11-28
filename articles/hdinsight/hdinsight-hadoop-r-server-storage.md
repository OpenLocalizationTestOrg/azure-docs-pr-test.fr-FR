---
title: "Solutions de stockage Azure pour R Server sur HDInsight - Azure | Microsoft Docs"
description: "Découvrez les différentes options de stockage disponibles pour les utilisateurs avec R Server sur HDInsight"
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 1cf30096-d3ca-45ea-b526-aa3954402f66
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: aef9c15636ccaecce07d4fa218a40ed26ebad9df
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a><span data-ttu-id="b2c81-103">Solutions de stockage Azure pour R Server sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2c81-103">Azure Storage solutions for R Server on HDInsight</span></span>

<span data-ttu-id="b2c81-104">Microsoft R Server sur HDInsight possède différentes solutions de stockage permettant de conserver les données, le code ou les objets qui contiennent des résultats d’analyse.</span><span class="sxs-lookup"><span data-stu-id="b2c81-104">Microsoft R Server on HDInsight has a variety of storage solutions to persist data, code, or objects that contain results from analysis.</span></span> <span data-ttu-id="b2c81-105">Il s’agit notamment des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="b2c81-105">These include the following options:</span></span>

- [<span data-ttu-id="b2c81-106">Blob Azure</span><span class="sxs-lookup"><span data-stu-id="b2c81-106">Azure Blob</span></span>](https://azure.microsoft.com/services/storage/blobs/)
- [<span data-ttu-id="b2c81-107">Azure Data Lake Storage</span><span class="sxs-lookup"><span data-stu-id="b2c81-107">Azure Data Lake Storage</span></span>](https://azure.microsoft.com/services/data-lake-store/)
- [<span data-ttu-id="b2c81-108">Stockage Fichier Azure</span><span class="sxs-lookup"><span data-stu-id="b2c81-108">Azure File storage</span></span>](https://azure.microsoft.com/services/storage/files/)

<span data-ttu-id="b2c81-109">Vous avez également la possibilité d’accéder à plusieurs conteneurs ou comptes de stockage Azure avec votre cluster HDI.</span><span class="sxs-lookup"><span data-stu-id="b2c81-109">You also have the option of accessing multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="b2c81-110">Le Stockage Fichier Azure est une option de stockage de données pratique, que l’on peut utiliser sur le nœud périphérique pour monter d’un partage de fichiers de stockage Azure sur, par exemple, le système de fichiers Linux.</span><span class="sxs-lookup"><span data-stu-id="b2c81-110">Azure File storage is a convenient data storage option for use on the edge node that enables you to mount an Azure Storage file share to, for example, the Linux file system.</span></span> <span data-ttu-id="b2c81-111">Mais les partages de fichiers Azure peuvent être montés et utilisés par tous les systèmes qui disposent d’un système d’exploitation pris en charge, par exemple Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="b2c81-111">But Azure File shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> 

<span data-ttu-id="b2c81-112">Lors de la création d’un cluster Hadoop dans HDInsight, vous spécifiez un compte de **stockage Azure** ou bien un **magasin Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="b2c81-112">When you create an Hadoop cluster in HDInsight, you specify either an **Azure storage** account or a **Data Lake store**.</span></span> <span data-ttu-id="b2c81-113">Un conteneur de stockage spécifique de ce compte contient le système de fichiers du cluster créé (par exemple, le système de fichiers DFS Hadoop).</span><span class="sxs-lookup"><span data-stu-id="b2c81-113">A specific storage container from that account holds the file system for the cluster that you create (for example, the Hadoop Distributed File System).</span></span> <span data-ttu-id="b2c81-114">Pour plus d’informations et pour obtenir de l’aide, consultez les pages :</span><span class="sxs-lookup"><span data-stu-id="b2c81-114">For more information and guidance, see:</span></span>

- [<span data-ttu-id="b2c81-115">Utiliser le stockage Azure avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2c81-115">Use Azure storage with HDInsight</span></span>](hdinsight-hadoop-use-blob-storage.md)
- <span data-ttu-id="b2c81-116">[Utiliser Data Lake Store avec des clusters Azure HDInsight](hdinsight-hadoop-use-data-lake-store.md)</span><span class="sxs-lookup"><span data-stu-id="b2c81-116">[Use Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> 

<span data-ttu-id="b2c81-117">Pour plus d’informations sur les solutions de stockage Azure, consultez la page [Introduction au Stockage Microsoft Azure](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b2c81-117">For more information on the Azure storage solutions, see [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md).</span></span> 

<span data-ttu-id="b2c81-118">Pour obtenir de l’aide sur la sélection de l’option de stockage la plus adaptée à votre scénario, consultez la page [Choisir quand utiliser des objets Blob Azure, des fichiers Azure ou des disques de données Azure](../storage/common/storage-decide-blobs-files-disks.md)</span><span class="sxs-lookup"><span data-stu-id="b2c81-118">For guidance on selecting the most appropriate storage option to use for your scenario, see [Deciding when to use Azure Blobs, Azure Files, or Azure Data Disks](../storage/common/storage-decide-blobs-files-disks.md)</span></span> 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a><span data-ttu-id="b2c81-119">Utiliser des comptes de stockage Blob Azure avec R Server</span><span class="sxs-lookup"><span data-stu-id="b2c81-119">Use Azure Blob storage accounts with R Server</span></span>

<span data-ttu-id="b2c81-120">Si nécessaire, vous pouvez accéder à plusieurs conteneurs ou comptes de stockage Azure avec votre cluster HDI.</span><span class="sxs-lookup"><span data-stu-id="b2c81-120">If necessary, you can access multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="b2c81-121">Pour cela, vous devez spécifier les comptes de stockage supplémentaires dans l’interface utilisateur au moment de la création du cluster, puis suivre ces étapes pour les utiliser avec R Server.</span><span class="sxs-lookup"><span data-stu-id="b2c81-121">To do so, you need to specify the additional storage accounts in the UI when you create the cluster, and then follow these steps to use them with R Server.</span></span>

> [!WARNING]
> <span data-ttu-id="b2c81-122">Pour des raisons de performances, le cluster HDInsight est créé dans le même centre de données que le compte de stockage principal que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="b2c81-122">For performance purposes, the HDInsight cluster is created in the same data center as the primary storage account that you specify.</span></span> <span data-ttu-id="b2c81-123">L’utilisation d’un compte de stockage dans un autre emplacement que le cluster HDInsight n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="b2c81-123">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span>

1. <span data-ttu-id="b2c81-124">Créez un cluster HDInsight avec un nom de compte de stockage **storage1** et un conteneur par défaut appelé **container1**.</span><span class="sxs-lookup"><span data-stu-id="b2c81-124">Create an HDInsight cluster with a storage account name of **storage1** and a default container called **container1**.</span></span>
2. <span data-ttu-id="b2c81-125">Spécifiez un compte de stockage supplémentaire appelé **storage2**.</span><span class="sxs-lookup"><span data-stu-id="b2c81-125">Specify an additional storage account called **storage2**.</span></span>  
3. <span data-ttu-id="b2c81-126">Copiez le fichier mycsv.csv dans le répertoire /share et effectuez une analyse sur ce fichier.</span><span class="sxs-lookup"><span data-stu-id="b2c81-126">Copy the mycsv.csv file to the /share directory, and perform analysis on that file.</span></span>  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. <span data-ttu-id="b2c81-127">Dans le code R, définissez le nœud du nom sur **par défaut** et définissez le répertoire et le fichier à traiter.</span><span class="sxs-lookup"><span data-stu-id="b2c81-127">In R code, set the name node to **default,** and set your directory and file to process.</span></span>  

        myNameNode <- "default"
        myPort <- 0

        #Location of the data:  
        bigDataDirRoot <- "/share"  

        #Define Spark compute context:
        mySparkCluster <- RxSpark(consoleOutput=TRUE)

        #Set compute context:
        rxSetComputeContext(mySparkCluster)

        #Define the Hadoop Distributed File System (HDFS) file system:
        hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

        #Specify the input file to analyze in HDFS:
        inputFile <-file.path(bigDataDirRoot,"mycsv.csv")

<span data-ttu-id="b2c81-128">Toutes les références de fichiers et de répertoires pointent vers le compte de stockage wasb://container1@storage1.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="b2c81-128">All the directory and file references point to the storage account wasb://container1@storage1.blob.core.windows.net.</span></span> <span data-ttu-id="b2c81-129">Il s’agit du **compte de stockage par défaut** associé au cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b2c81-129">This is the **default storage account** that's associated with the HDInsight cluster.</span></span>

<span data-ttu-id="b2c81-130">Supposons maintenant que vous souhaitiez traiter un fichier appelé mySpecial.csv qui se trouve dans le répertoire /private du conteneur **container2** dans le compte de stockage **storage2**.</span><span class="sxs-lookup"><span data-stu-id="b2c81-130">Now, suppose you want to process a file called mySpecial.csv that's located in the  /private directory of **container2** in **storage2**.</span></span>

<span data-ttu-id="b2c81-131">Dans votre code R, pointez la référence du nœud de nom vers le compte de stockage **storage2** .</span><span class="sxs-lookup"><span data-stu-id="b2c81-131">In your R code, point the name node reference to the **storage2** storage account.</span></span>


    myNameNode <- "wasb://container2@storage2.blob.core.windows.net"
    myPort <- 0

    #Location of the data:
    bigDataDirRoot <- "/private"

    #Define Spark compute context:
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    #Set compute context:
    rxSetComputeContext(mySparkCluster)

    #Define HDFS file system:
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    #Specify the input file to analyze in HDFS:
    inputFile <-file.path(bigDataDirRoot,"mySpecial.csv")

<span data-ttu-id="b2c81-132">Toutes les références de fichier et de répertoire pointent désormais vers le compte de stockage wasb://container2@storage2.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="b2c81-132">All of the directory and file references now point to the storage account wasb://container2@storage2.blob.core.windows.net.</span></span> <span data-ttu-id="b2c81-133">Il s’agit du **nom de nœud** que vous avez spécifié.</span><span class="sxs-lookup"><span data-stu-id="b2c81-133">This is the **Name Node** that you’ve specified.</span></span>

<span data-ttu-id="b2c81-134">Vous devez configurer ainsi le répertoire /user/RevoShare/<SSH username> sur **storage2** :</span><span class="sxs-lookup"><span data-stu-id="b2c81-134">You have to configure the /user/RevoShare/<SSH username> directory on **storage2** as follows:</span></span>


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a><span data-ttu-id="b2c81-135">Utiliser un magasin Azure Data Lake avec R Server</span><span class="sxs-lookup"><span data-stu-id="b2c81-135">Use an Azure Data Lake store with R Server</span></span>

<span data-ttu-id="b2c81-136">Pour utiliser des magasins Data Lake avec votre compte HDInsight, vous devez permettre à votre cluster d’accéder à tous les magasins Azure Data Lake que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="b2c81-136">To use Data Lake stores with your HDInsight account, you need to give your cluster access to each Azure Data Lake store that you want to use.</span></span> <span data-ttu-id="b2c81-137">Pour obtenir des instructions sur l’utilisation du Portail Azure pour créer un cluster HDInsight avec un compte Azure Data Lake Store comme stockage par défaut ou comme magasin supplémentaire, consultez la page [Créer un cluster HDInsight avec Data Lake Store à l’aide du Portail Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b2c81-137">For instructions on how to use the Azure portal to create a HDInsight cluster with an Azure Data Lake Store account as the default storage or as an additional store, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

<span data-ttu-id="b2c81-138">Vous utilisez alors le magasin de votre script R à peu près de la même manière qu’un compte de stockage Azure secondaire, comme le décrit la procédure précédente.</span><span class="sxs-lookup"><span data-stu-id="b2c81-138">You then use the store in your R script much like you did a secondary Azure storage account as described in the previous procedure.</span></span>

### <a name="add-cluster-access-to-your-azure-data-lake-stores"></a><span data-ttu-id="b2c81-139">Ajouter un accès de cluster à vos magasins Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="b2c81-139">Add cluster access to your Azure Data Lake stores</span></span>
<span data-ttu-id="b2c81-140">Vous accédez à un magasin Data Lake en utilisant un principal du service Azure Active Directory (Azure AD) associé à votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b2c81-140">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span></span>

<span data-ttu-id="b2c81-141">Pour ajouter un principal de service Azure AD :</span><span class="sxs-lookup"><span data-stu-id="b2c81-141">To add an Azure AD Service Principal:</span></span>

1. <span data-ttu-id="b2c81-142">Lorsque vous créez votre cluster HDInsight, sélectionnez **Identité AAD de cluster** à partir de l’onglet **Source de données**.</span><span class="sxs-lookup"><span data-stu-id="b2c81-142">When you create your HDInsight cluster, select **Cluster AAD Identity** from the **Data Source** tab.</span></span>

2. <span data-ttu-id="b2c81-143">Dans la boîte de dialogue **Identité AAD de cluster**, sous **Sélectionner un principal de service AD**, sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="b2c81-143">In the **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span></span>

<span data-ttu-id="b2c81-144">Après avoir attribué un nom et un mot de passe au principal du service, cliquez sur **Gérer l’accès ADLS** pour l’associer à vos magasins Data Lake.</span><span class="sxs-lookup"><span data-stu-id="b2c81-144">After you give the Service Principal a name and create a password for it, click **Manage ADLS Access** to associate the Service Principal with your Data Lake stores.</span></span>

<span data-ttu-id="b2c81-145">Il est également possible d’ajouter un accès à un ou plusieurs magasins Data Lake pour le cluster après sa création.</span><span class="sxs-lookup"><span data-stu-id="b2c81-145">It’s also possible to add cluster access to one or more Data Lake stores following cluster creation.</span></span> <span data-ttu-id="b2c81-146">Ouvrez l’entrée d’un magasin Data Lake sur le Portail Azure et accédez à **Explorateur de données > Accès > Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b2c81-146">Open the Azure portal entry for a Data Lake store and go to **Data Explorer > Access > Add**.</span></span> 

### <a name="how-to-access-the-data-lake-store-from-r-server"></a><span data-ttu-id="b2c81-147">Comment accéder au magasin Data Lake à partir de R Server</span><span class="sxs-lookup"><span data-stu-id="b2c81-147">How to access the Data Lake store from R Server</span></span>

<span data-ttu-id="b2c81-148">Après avoir créé un accès au magasin Data Lake, vous pouvez utiliser le magasin dans R Server sur HDInsight de la même façon qu’un compte de stockage Azure secondaire.</span><span class="sxs-lookup"><span data-stu-id="b2c81-148">Once you’ve given access to a Data Lake store, you can use the store in R Server on HDInsight the way you would a secondary Azure storage account.</span></span> <span data-ttu-id="b2c81-149">La seule différence est que le préfixe **wasb://** devient **adl://**, comme suit :</span><span class="sxs-lookup"><span data-stu-id="b2c81-149">The only difference is that the prefix **wasb://** changes to **adl://** as follows:</span></span>


    # Point to the ADL store (e.g. ADLtest)
    myNameNode <- "adl://rkadl1.azuredatalakestore.net"
    myPort <- 0

    # Location of the data (assumes a /share directory on the ADL account)
    bigDataDirRoot <- "/share"  

    # Define Spark compute context
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    # Set compute context
    rxSetComputeContext(mySparkCluster)

    # Define HDFS file system
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    # Specify the input file in HDFS to analyze
    inputFile <-file.path(bigDataDirRoot,"AirlineDemoSmall.csv")

    # Create factors for days of the week
    colInfo <- list(DayOfWeek = list(type = "factor",
               levels = c("Monday", "Tuesday", "Wednesday", "Thursday",
                          "Friday", "Saturday", "Sunday")))

    # Define the data source
    airDS <- RxTextData(file = inputFile, missingValueString = "M",
                    colInfo  = colInfo, fileSystem = hdfsFS)

    # Run a linear regression
    model <- rxLinMod(ArrDelay~CRSDepTime+DayOfWeek, data = airDS)


<span data-ttu-id="b2c81-150">Les commandes suivantes sont utilisées pour configurer le compte de stockage Data Lake avec le répertoire RevoShare et pour ajouter l’exemple de fichier .csv de l’exemple précédent :</span><span class="sxs-lookup"><span data-stu-id="b2c81-150">The following commands are used to configure the Data Lake storage account with the RevoShare directory and add the sample .csv file from the previous example:</span></span>


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a><span data-ttu-id="b2c81-151">Utiliser le Stockage Fichier Azure avec R Server</span><span class="sxs-lookup"><span data-stu-id="b2c81-151">Use Azure File storage with R Server</span></span>

<span data-ttu-id="b2c81-152">Il existe également une option de stockage de données pratique qui peut s’utiliser sur le nœud périphérique ; elle se nomme [Fichiers Azure]((https://azure.microsoft.com/services/storage/files/).</span><span class="sxs-lookup"><span data-stu-id="b2c81-152">There is also a convenient data storage option for use on the edge node called [Azure Files]((https://azure.microsoft.com/services/storage/files/).</span></span> <span data-ttu-id="b2c81-153">Elle vous permet de monter un partage de fichiers Azure Storage sur le système de fichiers Linux.</span><span class="sxs-lookup"><span data-stu-id="b2c81-153">It enables you to mount an Azure Storage file share to the Linux file system.</span></span> <span data-ttu-id="b2c81-154">Cette option peut être utile pour stocker des fichiers de données, des scripts R et des objets de résultats qui pourront se révéler nécessaires par la suite, lorsqu’il sera judicieux d’utiliser le système de fichiers natif sur le nœud périphérique plutôt que HDFS.</span><span class="sxs-lookup"><span data-stu-id="b2c81-154">This option can be handy for storing data files, R scripts, and result objects that might be needed later, especially when it makes sense to use the native file system on the edge node rather than HDFS.</span></span> 

<span data-ttu-id="b2c81-155">Le principal avantage des fichiers Azure est que les partages de fichiers peuvent être montés et utilisés par tout système disposant d’un système d’exploitation pris en charge, tel que Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="b2c81-155">A major benefit of Azure Files is that the file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> <span data-ttu-id="b2c81-156">Par exemple, ils peuvent être utilisés par un autre cluster HDInsight que vous ou un membre de votre équipe avez, par une machine virtuelle Azure ou même par un système local.</span><span class="sxs-lookup"><span data-stu-id="b2c81-156">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span></span> <span data-ttu-id="b2c81-157">Pour plus d'informations, consultez les pages suivantes :</span><span class="sxs-lookup"><span data-stu-id="b2c81-157">For more information, see:</span></span>

- [<span data-ttu-id="b2c81-158">Guide pratique pour utiliser le Stockage Fichier Azure avec Linux</span><span class="sxs-lookup"><span data-stu-id="b2c81-158">How to use Azure File storage with Linux</span></span>](../storage/files/storage-how-to-use-files-linux.md)
- [<span data-ttu-id="b2c81-159">Guide pratique pour utiliser le Stockage Fichier Azure sous Windows</span><span class="sxs-lookup"><span data-stu-id="b2c81-159">How to use Azure File storage on Windows</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a><span data-ttu-id="b2c81-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b2c81-160">Next steps</span></span>

<span data-ttu-id="b2c81-161">Maintenant que vous maîtrisez les options de stockage Azure, utilisez les liens suivants pour découvrir différents moyens d’effectuer des tâches de science des données avec R Server sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b2c81-161">Now that you understand the Azure storage options, use the following links to discover ways of getting data science tasks done with R Server on HDInsight.</span></span>

* [<span data-ttu-id="b2c81-162">Vue d’ensemble : R Server sur HDInsight (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="b2c81-162">Overview of R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="b2c81-163">Prise en main de R Server sur Hadoop</span><span class="sxs-lookup"><span data-stu-id="b2c81-163">Get started with R server on Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="b2c81-164">Ajouter RStudio Server à HDInsight (s’il n’est pas ajouté lors de la création du cluster)</span><span class="sxs-lookup"><span data-stu-id="b2c81-164">Add RStudio Server to HDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="b2c81-165">Options de contexte de calcul pour R Server sur HDInsight (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="b2c81-165">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)

