---
title: aaaAzure des solutions de stockage pour le serveur R sur HDInsight - Azure | Documents Microsoft
description: "En savoir plus sur hello stockage différentes options disponibles toousers avec R Server sur HDInsight"
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
ms.openlocfilehash: ff5e80fee14d5e74cbc22e873e6bc1439a3b6037
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a><span data-ttu-id="1608b-103">Solutions de stockage Azure pour R Server sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="1608b-103">Azure Storage solutions for R Server on HDInsight</span></span>

<span data-ttu-id="1608b-104">Microsoft R Server sur HDInsight possède un éventail de données de toopersist de solutions de stockage, votre code ou les objets qui contiennent des résultats d’analyse.</span><span class="sxs-lookup"><span data-stu-id="1608b-104">Microsoft R Server on HDInsight has a variety of storage solutions toopersist data, code, or objects that contain results from analysis.</span></span> <span data-ttu-id="1608b-105">Elles incluent notamment hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="1608b-105">These include hello following options:</span></span>

- [<span data-ttu-id="1608b-106">Blob Azure</span><span class="sxs-lookup"><span data-stu-id="1608b-106">Azure Blob</span></span>](https://azure.microsoft.com/services/storage/blobs/)
- [<span data-ttu-id="1608b-107">Azure Data Lake Storage</span><span class="sxs-lookup"><span data-stu-id="1608b-107">Azure Data Lake Storage</span></span>](https://azure.microsoft.com/services/data-lake-store/)
- [<span data-ttu-id="1608b-108">Stockage Fichier Azure</span><span class="sxs-lookup"><span data-stu-id="1608b-108">Azure File storage</span></span>](https://azure.microsoft.com/services/storage/files/)

<span data-ttu-id="1608b-109">Vous avez également option hello d’accès à plusieurs comptes de stockage Azure ou les conteneurs avec votre cluster HDI.</span><span class="sxs-lookup"><span data-stu-id="1608b-109">You also have hello option of accessing multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="1608b-110">Stockage de fichier Azure est une option de stockage de données pratique pour une utilisation sur le nœud de bord hello qui vous permet de toomount un partage de fichiers de stockage Azure pour, par exemple, les système de fichiers Linux hello.</span><span class="sxs-lookup"><span data-stu-id="1608b-110">Azure File storage is a convenient data storage option for use on hello edge node that enables you toomount an Azure Storage file share to, for example, hello Linux file system.</span></span> <span data-ttu-id="1608b-111">Mais les partages de fichiers Azure peuvent être montés et utilisés par tous les systèmes qui disposent d’un système d’exploitation pris en charge, par exemple Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="1608b-111">But Azure File shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> 

<span data-ttu-id="1608b-112">Lors de la création d’un cluster Hadoop dans HDInsight, vous spécifiez un compte de **stockage Azure** ou bien un **magasin Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="1608b-112">When you create an Hadoop cluster in HDInsight, you specify either an **Azure storage** account or a **Data Lake store**.</span></span> <span data-ttu-id="1608b-113">Un conteneur de stockage spécifique à partir de ce compte conserve un système de fichiers hello pour cluster hello que vous créez (par exemple, le système de fichiers distribués Hadoop de hello).</span><span class="sxs-lookup"><span data-stu-id="1608b-113">A specific storage container from that account holds hello file system for hello cluster that you create (for example, hello Hadoop Distributed File System).</span></span> <span data-ttu-id="1608b-114">Pour plus d’informations et pour obtenir de l’aide, consultez les pages :</span><span class="sxs-lookup"><span data-stu-id="1608b-114">For more information and guidance, see:</span></span>

- [<span data-ttu-id="1608b-115">Utiliser le stockage Azure avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="1608b-115">Use Azure storage with HDInsight</span></span>](hdinsight-hadoop-use-blob-storage.md)
- <span data-ttu-id="1608b-116">[Utiliser Data Lake Store avec des clusters Azure HDInsight](hdinsight-hadoop-use-data-lake-store.md)</span><span class="sxs-lookup"><span data-stu-id="1608b-116">[Use Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> 

<span data-ttu-id="1608b-117">Pour plus d’informations sur les solutions de stockage Azure hello, consultez [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1608b-117">For more information on hello Azure storage solutions, see [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span></span> 

<span data-ttu-id="1608b-118">Pour obtenir des conseils sur la sélection hello toouse option stockage plus appropriée pour votre scénario, consultez [choix entre lorsque les objets BLOB de Azure toouse, des fichiers de Azure ou des disques de données Azure](../storage/common/storage-decide-blobs-files-disks.md)</span><span class="sxs-lookup"><span data-stu-id="1608b-118">For guidance on selecting hello most appropriate storage option toouse for your scenario, see [Deciding when toouse Azure Blobs, Azure Files, or Azure Data Disks](../storage/common/storage-decide-blobs-files-disks.md)</span></span> 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a><span data-ttu-id="1608b-119">Utiliser des comptes de stockage Blob Azure avec R Server</span><span class="sxs-lookup"><span data-stu-id="1608b-119">Use Azure Blob storage accounts with R Server</span></span>

<span data-ttu-id="1608b-120">Si nécessaire, vous pouvez accéder à plusieurs conteneurs ou comptes de stockage Azure avec votre cluster HDI.</span><span class="sxs-lookup"><span data-stu-id="1608b-120">If necessary, you can access multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="1608b-121">toodo, vous pouvez donc comptes de stockage supplémentaires toospecify hello Bonjour l’interface utilisateur lorsque vous créez le cluster de hello, puis suivez ces étapes toouse avec R Server.</span><span class="sxs-lookup"><span data-stu-id="1608b-121">toodo so, you need toospecify hello additional storage accounts in hello UI when you create hello cluster, and then follow these steps toouse them with R Server.</span></span>

> [!WARNING]
> <span data-ttu-id="1608b-122">Pour des raisons de performances, hello cluster HDInsight est créé dans hello même centre de données en tant que compte de stockage principal hello que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="1608b-122">For performance purposes, hello HDInsight cluster is created in hello same data center as hello primary storage account that you specify.</span></span> <span data-ttu-id="1608b-123">À l’aide d’un compte de stockage dans un emplacement autre que le cluster HDInsight de hello n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="1608b-123">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span>

1. <span data-ttu-id="1608b-124">Créez un cluster HDInsight avec un nom de compte de stockage **storage1** et un conteneur par défaut appelé **container1**.</span><span class="sxs-lookup"><span data-stu-id="1608b-124">Create an HDInsight cluster with a storage account name of **storage1** and a default container called **container1**.</span></span>
2. <span data-ttu-id="1608b-125">Spécifiez un compte de stockage supplémentaire appelé **storage2**.</span><span class="sxs-lookup"><span data-stu-id="1608b-125">Specify an additional storage account called **storage2**.</span></span>  
3. <span data-ttu-id="1608b-126">Copiez le répertoire /share toohello hello mycsv.csv fichiers et effectuer une analyse sur ce fichier.</span><span class="sxs-lookup"><span data-stu-id="1608b-126">Copy hello mycsv.csv file toohello /share directory, and perform analysis on that file.</span></span>  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. <span data-ttu-id="1608b-127">Dans le code R, jeu de nœud de nom hello trop**par défaut,** et définissez votre tooprocess de répertoires et de fichiers.</span><span class="sxs-lookup"><span data-stu-id="1608b-127">In R code, set hello name node too**default,** and set your directory and file tooprocess.</span></span>  

        myNameNode <- "default"
        myPort <- 0

        #Location of hello data:  
        bigDataDirRoot <- "/share"  

        #Define Spark compute context:
        mySparkCluster <- RxSpark(consoleOutput=TRUE)

        #Set compute context:
        rxSetComputeContext(mySparkCluster)

        #Define hello Hadoop Distributed File System (HDFS) file system:
        hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

        #Specify hello input file tooanalyze in HDFS:
        inputFile <-file.path(bigDataDirRoot,"mycsv.csv")

<span data-ttu-id="1608b-128">Tous hello répertoires et les fichiers du compte de stockage références point toohello wasb://container1@storage1.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="1608b-128">All hello directory and file references point toohello storage account wasb://container1@storage1.blob.core.windows.net.</span></span> <span data-ttu-id="1608b-129">Il s’agit de hello **compte de stockage par défaut** associé cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="1608b-129">This is hello **default storage account** that's associated with hello HDInsight cluster.</span></span>

<span data-ttu-id="1608b-130">Maintenant, supposons que vous vouliez tooprocess un fichier appelé mySpecial.csv qui se trouve dans hello /private de **au conteneur container2** dans **stockage2**.</span><span class="sxs-lookup"><span data-stu-id="1608b-130">Now, suppose you want tooprocess a file called mySpecial.csv that's located in hello  /private directory of **container2** in **storage2**.</span></span>

<span data-ttu-id="1608b-131">Dans votre code R, pointez hello nom du nœud référence toohello **stockage2** compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="1608b-131">In your R code, point hello name node reference toohello **storage2** storage account.</span></span>


    myNameNode <- "wasb://container2@storage2.blob.core.windows.net"
    myPort <- 0

    #Location of hello data:
    bigDataDirRoot <- "/private"

    #Define Spark compute context:
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    #Set compute context:
    rxSetComputeContext(mySparkCluster)

    #Define HDFS file system:
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    #Specify hello input file tooanalyze in HDFS:
    inputFile <-file.path(bigDataDirRoot,"mySpecial.csv")

<span data-ttu-id="1608b-132">Tous les hello répertoire et fichier références maintenant point toohello compte de stockage wasb://container2@storage2.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="1608b-132">All of hello directory and file references now point toohello storage account wasb://container2@storage2.blob.core.windows.net.</span></span> <span data-ttu-id="1608b-133">Il s’agit de hello **nom de nœud** que vous avez spécifiés.</span><span class="sxs-lookup"><span data-stu-id="1608b-133">This is hello **Name Node** that you’ve specified.</span></span>

<span data-ttu-id="1608b-134">Vous avez tooconfigure hello /user RevoShare/<SSH username> répertoire **stockage2** comme suit :</span><span class="sxs-lookup"><span data-stu-id="1608b-134">You have tooconfigure hello /user/RevoShare/<SSH username> directory on **storage2** as follows:</span></span>


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a><span data-ttu-id="1608b-135">Utiliser un magasin Azure Data Lake avec R Server</span><span class="sxs-lookup"><span data-stu-id="1608b-135">Use an Azure Data Lake store with R Server</span></span>

<span data-ttu-id="1608b-136">toouse Data Lake stocke avec votre compte HDInsight, vous devez toogive votre magasin d’Azure Data Lake tooeach cluster accès que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="1608b-136">toouse Data Lake stores with your HDInsight account, you need toogive your cluster access tooeach Azure Data Lake store that you want toouse.</span></span> <span data-ttu-id="1608b-137">Pour obtenir des instructions sur la façon dont toouse hello toocreate portail Azure un HDInsight de cluster avec un compte Azure Data Lake Store comme stockage par défaut de hello ou un magasin supplémentaire, consultez [créer un cluster HDInsight avec Data Lake Store à l’aide du portail Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1608b-137">For instructions on how toouse hello Azure portal toocreate a HDInsight cluster with an Azure Data Lake Store account as hello default storage or as an additional store, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

<span data-ttu-id="1608b-138">Vous ensuite utilisez le magasin de hello dans votre script R beaucoup comme vous l’avez fait un compte de stockage Azure secondaire comme décrit dans la procédure précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="1608b-138">You then use hello store in your R script much like you did a secondary Azure storage account as described in hello previous procedure.</span></span>

### <a name="add-cluster-access-tooyour-azure-data-lake-stores"></a><span data-ttu-id="1608b-139">Ajouter tooyour d’accès de cluster Qu'azure Data Lake stocke</span><span class="sxs-lookup"><span data-stu-id="1608b-139">Add cluster access tooyour Azure Data Lake stores</span></span>
<span data-ttu-id="1608b-140">Vous accédez à un magasin Data Lake en utilisant un principal du service Azure Active Directory (Azure AD) associé à votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1608b-140">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span></span>

<span data-ttu-id="1608b-141">tooadd un Principal du Service Azure AD :</span><span class="sxs-lookup"><span data-stu-id="1608b-141">tooadd an Azure AD Service Principal:</span></span>

1. <span data-ttu-id="1608b-142">Lorsque vous créez votre cluster HDInsight, sélectionnez **Cluster AAD identité** de hello **Source de données** onglet.</span><span class="sxs-lookup"><span data-stu-id="1608b-142">When you create your HDInsight cluster, select **Cluster AAD Identity** from hello **Data Source** tab.</span></span>

2. <span data-ttu-id="1608b-143">Bonjour **Cluster AAD identité** boîte de dialogue **sélectionnez un Principal de Service AD**, sélectionnez **nouvel**.</span><span class="sxs-lookup"><span data-stu-id="1608b-143">In hello **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span></span>

<span data-ttu-id="1608b-144">Une fois que vous donnez un nom à hello Principal du Service et créez un mot de passe pour celle-ci, cliquez sur **gérer l’accès ADLS** hello tooassociate stocke de Principal du Service avec votre Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1608b-144">After you give hello Service Principal a name and create a password for it, click **Manage ADLS Access** tooassociate hello Service Principal with your Data Lake stores.</span></span>

<span data-ttu-id="1608b-145">Il est également possible tooadd cluster accès tooone ou plus Data Lake stocke après la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="1608b-145">It’s also possible tooadd cluster access tooone or more Data Lake stores following cluster creation.</span></span> <span data-ttu-id="1608b-146">Ouvrez hello Azure entrée portail pour un magasin Data Lake et trop**Explorateur de données > accès > ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1608b-146">Open hello Azure portal entry for a Data Lake store and go too**Data Explorer > Access > Add**.</span></span> 

### <a name="how-tooaccess-hello-data-lake-store-from-r-server"></a><span data-ttu-id="1608b-147">Comment tooaccess hello magasin lac de données à partir de R Server</span><span class="sxs-lookup"><span data-stu-id="1608b-147">How tooaccess hello Data Lake store from R Server</span></span>

<span data-ttu-id="1608b-148">Une fois que vous avez donné magasin Data Lake de tooa d’accès, vous pouvez utiliser le magasin hello dans R Server sur la façon de hello HDInsight que vous le feriez pour un compte de stockage Azure secondaire.</span><span class="sxs-lookup"><span data-stu-id="1608b-148">Once you’ve given access tooa Data Lake store, you can use hello store in R Server on HDInsight hello way you would a secondary Azure storage account.</span></span> <span data-ttu-id="1608b-149">Hello la seule différence est le préfixe hello **wasb : / /** change également**adl : / /** comme suit :</span><span class="sxs-lookup"><span data-stu-id="1608b-149">hello only difference is that hello prefix **wasb://** changes too**adl://** as follows:</span></span>


    # Point toohello ADL store (e.g. ADLtest)
    myNameNode <- "adl://rkadl1.azuredatalakestore.net"
    myPort <- 0

    # Location of hello data (assumes a /share directory on hello ADL account)
    bigDataDirRoot <- "/share"  

    # Define Spark compute context
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    # Set compute context
    rxSetComputeContext(mySparkCluster)

    # Define HDFS file system
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    # Specify hello input file in HDFS tooanalyze
    inputFile <-file.path(bigDataDirRoot,"AirlineDemoSmall.csv")

    # Create factors for days of hello week
    colInfo <- list(DayOfWeek = list(type = "factor",
               levels = c("Monday", "Tuesday", "Wednesday", "Thursday",
                          "Friday", "Saturday", "Sunday")))

    # Define hello data source
    airDS <- RxTextData(file = inputFile, missingValueString = "M",
                    colInfo  = colInfo, fileSystem = hdfsFS)

    # Run a linear regression
    model <- rxLinMod(ArrDelay~CRSDepTime+DayOfWeek, data = airDS)


<span data-ttu-id="1608b-150">Hello commandes suivantes sont utilisées tooconfigure hello compte de stockage de LAC de données avec le répertoire de RevoShare hello et ajouter un fichier .csv d’exemple hello à partir de l’exemple précédent de hello :</span><span class="sxs-lookup"><span data-stu-id="1608b-150">hello following commands are used tooconfigure hello Data Lake storage account with hello RevoShare directory and add hello sample .csv file from hello previous example:</span></span>


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a><span data-ttu-id="1608b-151">Utiliser le Stockage Fichier Azure avec R Server</span><span class="sxs-lookup"><span data-stu-id="1608b-151">Use Azure File storage with R Server</span></span>

<span data-ttu-id="1608b-152">Il existe également une option de stockage de données pratique pour une utilisation sur le nœud de bord hello appelé [Azure Files] ((https://azure.microsoft.com/services/storage/files/).</span><span class="sxs-lookup"><span data-stu-id="1608b-152">There is also a convenient data storage option for use on hello edge node called [Azure Files]((https://azure.microsoft.com/services/storage/files/).</span></span> <span data-ttu-id="1608b-153">Il vous permet de toomount un toohello de partage de fichier de stockage Azure système de fichiers Linux.</span><span class="sxs-lookup"><span data-stu-id="1608b-153">It enables you toomount an Azure Storage file share toohello Linux file system.</span></span> <span data-ttu-id="1608b-154">Cette option peut être pratique pour stocker les fichiers de données, les scripts R et les objets de résultats peuvent être nécessaire ultérieurement, en particulier lorsqu’il rend le système de fichiers natif sens toouse hello sur hello bord plutôt que HDFS.</span><span class="sxs-lookup"><span data-stu-id="1608b-154">This option can be handy for storing data files, R scripts, and result objects that might be needed later, especially when it makes sense toouse hello native file system on hello edge node rather than HDFS.</span></span> 

<span data-ttu-id="1608b-155">Le principal avantage des fichiers Azure est ce fichier hello partages peuvent être montés et utilisés par n’importe quel système disposant d’un système d’exploitation pris en charge, tels que Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="1608b-155">A major benefit of Azure Files is that hello file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> <span data-ttu-id="1608b-156">Par exemple, ils peuvent être utilisés par un autre cluster HDInsight que vous ou un membre de votre équipe avez, par une machine virtuelle Azure ou même par un système local.</span><span class="sxs-lookup"><span data-stu-id="1608b-156">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span></span> <span data-ttu-id="1608b-157">Pour plus d'informations, consultez les pages suivantes :</span><span class="sxs-lookup"><span data-stu-id="1608b-157">For more information, see:</span></span>

- [<span data-ttu-id="1608b-158">Comment toouse stockage Azure files avec Linux</span><span class="sxs-lookup"><span data-stu-id="1608b-158">How toouse Azure File storage with Linux</span></span>](../storage/files/storage-how-to-use-files-linux.md)
- [<span data-ttu-id="1608b-159">Comment toouse stockage de fichier Azure sur Windows</span><span class="sxs-lookup"><span data-stu-id="1608b-159">How toouse Azure File storage on Windows</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a><span data-ttu-id="1608b-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1608b-160">Next steps</span></span>

<span data-ttu-id="1608b-161">Maintenant que vous comprenez les options de stockage Azure hello, suivant de hello utilisez lie toodiscover des façons d’obtenir les tâches courantes relatives aux données effectuées avec le serveur R sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1608b-161">Now that you understand hello Azure storage options, use hello following links toodiscover ways of getting data science tasks done with R Server on HDInsight.</span></span>

* [<span data-ttu-id="1608b-162">Vue d’ensemble : R Server sur HDInsight (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="1608b-162">Overview of R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="1608b-163">Prise en main de R Server sur Hadoop</span><span class="sxs-lookup"><span data-stu-id="1608b-163">Get started with R server on Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="1608b-164">Ajouter RStudio Server tooHDInsight (si elle ne pas lors de la création du cluster)</span><span class="sxs-lookup"><span data-stu-id="1608b-164">Add RStudio Server tooHDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="1608b-165">Options de contexte de calcul pour R Server sur HDInsight (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="1608b-165">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)

