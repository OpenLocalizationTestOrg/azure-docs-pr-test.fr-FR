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
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a>Solutions de stockage Azure pour R Server sur HDInsight

Microsoft R Server sur HDInsight possède un éventail de données de toopersist de solutions de stockage, votre code ou les objets qui contiennent des résultats d’analyse. Elles incluent notamment hello options suivantes :

- [Blob Azure](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage](https://azure.microsoft.com/services/data-lake-store/)
- [Stockage Fichier Azure](https://azure.microsoft.com/services/storage/files/)

Vous avez également option hello d’accès à plusieurs comptes de stockage Azure ou les conteneurs avec votre cluster HDI. Stockage de fichier Azure est une option de stockage de données pratique pour une utilisation sur le nœud de bord hello qui vous permet de toomount un partage de fichiers de stockage Azure pour, par exemple, les système de fichiers Linux hello. Mais les partages de fichiers Azure peuvent être montés et utilisés par tous les systèmes qui disposent d’un système d’exploitation pris en charge, par exemple Windows ou Linux. 

Lors de la création d’un cluster Hadoop dans HDInsight, vous spécifiez un compte de **stockage Azure** ou bien un **magasin Data Lake**. Un conteneur de stockage spécifique à partir de ce compte conserve un système de fichiers hello pour cluster hello que vous créez (par exemple, le système de fichiers distribués Hadoop de hello). Pour plus d’informations et pour obtenir de l’aide, consultez les pages :

- [Utiliser le stockage Azure avec HDInsight](hdinsight-hadoop-use-blob-storage.md)
- [Utiliser Data Lake Store avec des clusters Azure HDInsight](hdinsight-hadoop-use-data-lake-store.md) 

Pour plus d’informations sur les solutions de stockage Azure hello, consultez [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md). 

Pour obtenir des conseils sur la sélection hello toouse option stockage plus appropriée pour votre scénario, consultez [choix entre lorsque les objets BLOB de Azure toouse, des fichiers de Azure ou des disques de données Azure](../storage/common/storage-decide-blobs-files-disks.md) 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a>Utiliser des comptes de stockage Blob Azure avec R Server

Si nécessaire, vous pouvez accéder à plusieurs conteneurs ou comptes de stockage Azure avec votre cluster HDI. toodo, vous pouvez donc comptes de stockage supplémentaires toospecify hello Bonjour l’interface utilisateur lorsque vous créez le cluster de hello, puis suivez ces étapes toouse avec R Server.

> [!WARNING]
> Pour des raisons de performances, hello cluster HDInsight est créé dans hello même centre de données en tant que compte de stockage principal hello que vous spécifiez. À l’aide d’un compte de stockage dans un emplacement autre que le cluster HDInsight de hello n’est pas pris en charge.

1. Créez un cluster HDInsight avec un nom de compte de stockage **storage1** et un conteneur par défaut appelé **container1**.
2. Spécifiez un compte de stockage supplémentaire appelé **storage2**.  
3. Copiez le répertoire /share toohello hello mycsv.csv fichiers et effectuer une analyse sur ce fichier.  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. Dans le code R, jeu de nœud de nom hello trop**par défaut,** et définissez votre tooprocess de répertoires et de fichiers.  

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

Tous hello répertoires et les fichiers du compte de stockage références point toohello wasb://container1@storage1.blob.core.windows.net. Il s’agit de hello **compte de stockage par défaut** associé cluster HDInsight de hello.

Maintenant, supposons que vous vouliez tooprocess un fichier appelé mySpecial.csv qui se trouve dans hello /private de **au conteneur container2** dans **stockage2**.

Dans votre code R, pointez hello nom du nœud référence toohello **stockage2** compte de stockage.


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

Tous les hello répertoire et fichier références maintenant point toohello compte de stockage wasb://container2@storage2.blob.core.windows.net. Il s’agit de hello **nom de nœud** que vous avez spécifiés.

Vous avez tooconfigure hello /user RevoShare/<SSH username> répertoire **stockage2** comme suit :


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a>Utiliser un magasin Azure Data Lake avec R Server

toouse Data Lake stocke avec votre compte HDInsight, vous devez toogive votre magasin d’Azure Data Lake tooeach cluster accès que vous souhaitez toouse. Pour obtenir des instructions sur la façon dont toouse hello toocreate portail Azure un HDInsight de cluster avec un compte Azure Data Lake Store comme stockage par défaut de hello ou un magasin supplémentaire, consultez [créer un cluster HDInsight avec Data Lake Store à l’aide du portail Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

Vous ensuite utilisez le magasin de hello dans votre script R beaucoup comme vous l’avez fait un compte de stockage Azure secondaire comme décrit dans la procédure précédente de hello.

### <a name="add-cluster-access-tooyour-azure-data-lake-stores"></a>Ajouter tooyour d’accès de cluster Qu'azure Data Lake stocke
Vous accédez à un magasin Data Lake en utilisant un principal du service Azure Active Directory (Azure AD) associé à votre cluster HDInsight.

tooadd un Principal du Service Azure AD :

1. Lorsque vous créez votre cluster HDInsight, sélectionnez **Cluster AAD identité** de hello **Source de données** onglet.

2. Bonjour **Cluster AAD identité** boîte de dialogue **sélectionnez un Principal de Service AD**, sélectionnez **nouvel**.

Une fois que vous donnez un nom à hello Principal du Service et créez un mot de passe pour celle-ci, cliquez sur **gérer l’accès ADLS** hello tooassociate stocke de Principal du Service avec votre Data Lake.

Il est également possible tooadd cluster accès tooone ou plus Data Lake stocke après la création du cluster. Ouvrez hello Azure entrée portail pour un magasin Data Lake et trop**Explorateur de données > accès > ajouter**. 

### <a name="how-tooaccess-hello-data-lake-store-from-r-server"></a>Comment tooaccess hello magasin lac de données à partir de R Server

Une fois que vous avez donné magasin Data Lake de tooa d’accès, vous pouvez utiliser le magasin hello dans R Server sur la façon de hello HDInsight que vous le feriez pour un compte de stockage Azure secondaire. Hello la seule différence est le préfixe hello **wasb : / /** change également**adl : / /** comme suit :


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


Hello commandes suivantes sont utilisées tooconfigure hello compte de stockage de LAC de données avec le répertoire de RevoShare hello et ajouter un fichier .csv d’exemple hello à partir de l’exemple précédent de hello :


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a>Utiliser le Stockage Fichier Azure avec R Server

Il existe également une option de stockage de données pratique pour une utilisation sur le nœud de bord hello appelé [Azure Files] ((https://azure.microsoft.com/services/storage/files/). Il vous permet de toomount un toohello de partage de fichier de stockage Azure système de fichiers Linux. Cette option peut être pratique pour stocker les fichiers de données, les scripts R et les objets de résultats peuvent être nécessaire ultérieurement, en particulier lorsqu’il rend le système de fichiers natif sens toouse hello sur hello bord plutôt que HDFS. 

Le principal avantage des fichiers Azure est ce fichier hello partages peuvent être montés et utilisés par n’importe quel système disposant d’un système d’exploitation pris en charge, tels que Windows ou Linux. Par exemple, ils peuvent être utilisés par un autre cluster HDInsight que vous ou un membre de votre équipe avez, par une machine virtuelle Azure ou même par un système local. Pour plus d'informations, consultez les pages suivantes :

- [Comment toouse stockage Azure files avec Linux](../storage/files/storage-how-to-use-files-linux.md)
- [Comment toouse stockage de fichier Azure sur Windows](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous comprenez les options de stockage Azure hello, suivant de hello utilisez lie toodiscover des façons d’obtenir les tâches courantes relatives aux données effectuées avec le serveur R sur HDInsight.

* [Vue d’ensemble : R Server sur HDInsight (version préliminaire)](hdinsight-hadoop-r-server-overview.md)
* [Prise en main de R Server sur Hadoop](hdinsight-hadoop-r-server-get-started.md)
* [Ajouter RStudio Server tooHDInsight (si elle ne pas lors de la création du cluster)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Options de contexte de calcul pour R Server sur HDInsight (version préliminaire)](hdinsight-hadoop-r-server-compute-contexts.md)

