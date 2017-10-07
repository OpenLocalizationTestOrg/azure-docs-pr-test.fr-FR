---
title: "données aaaUpload pour les travaux Hadoop dans HDInsight | Documents Microsoft"
description: "Découvrez comment tooupload et accès aux données pour les travaux Hadoop dans HDInsight à l’aide hello CLI d’Azure, Explorateur de stockage Azure, Azure PowerShell, ligne de commande Hadoop hello ou Sqoop."
keywords: "etl hadoop, obtention de données dans hadoop, données de charge hadoop"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 56b913ee-0f9a-4e9f-9eaf-c571f8603dd6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: jgao
ms.openlocfilehash: 15da602085d41c19789e34800f3d9e238d7d1de8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a>Téléchargement de données pour les tâches Hadoop dans HDInsight
Azure HDInsight fournit un système HDFS (Hadoo Distributed File System) complet pour le stockage d'objets blob Azure. Il est conçu comme un tooprovide d’extension HDFS soudure expérience toocustomers. Il permet d’ensemble complète de hello de composants dans hello Hadoop écosystème toooperate directement sur les données hello qu’il gère. Le stockage d'objets blob Azure et HDFS sont des systèmes de fichiers distincts qui sont optimisés pour le stockage de données et pour les calculs réalisés à partir de ces données. Pour plus d’informations sur les avantages de hello d’utiliser le stockage d’objets Blob Azure, consultez [le stockage Blob de Azure utilisation hdinsight][hdinsight-storage].

**Configuration requise**

Notez hello suivant demande avant de commencer :

* Un cluster Azure HDInsight. Pour obtenir des instructions, consultez le didacticiel [Prise en main d’Azure HDInsight][hdinsight-get-started] ou la rubrique [Mise en service de clusters HDInsight][hdinsight-provision].

## <a name="why-blob-storage"></a>Qu'est-ce que le stockage d'objets blob ?
Azure HDInsight clusters sont généralement déployés toorun les tâches MapReduce et les clusters hello sont supprimés une fois que ces travaux terminent. En conservant les données hello dans des clusters HDFS hello issue des calculs serait un toostore onéreuse ces données. Stockage d’objets Blob Azure est une option de stockage économique et pouvant être partagé pour les données qui sont traitée à l’aide de HDInsight de toobe capacité, hautement disponible et évolutive. Le stockage des données dans un objet blob permet de clusters HDInsight hello qui sont utilisés pour toobe calcul libéré en toute sécurité sans perte de données.

### <a name="directories"></a>Répertoires
Les conteneurs de stockage d'objets blob Azure stockent des données en tant que paires clé/valeur et sans hiérarchie de répertoires. Toutefois hello « / » caractère peut être utilisé dans toomake de nom de la clé hello il apparaît comme si un fichier est stocké dans une structure de répertoire. HDInsight les interprète comme des répertoires réels.

Par exemple, une clé d'objet blob peut être *input/log1.txt*. Aucun répertoire « entrée » réel n’existe, mais en raison de la présence de toohello de hello caractère « / » dans le nom de la clé hello, il semble hello un chemin d’accès de fichier.

Pour cette raison, quand vous utilisez les outils d'Azure Explorer, vous pouvez remarquer la présence de fichiers de 0 octet. Ces fichiers ont deux utilités :

* S’il existe les dossiers vides, ils marquent d’existence hello du dossier de hello. Stockage d’objets Blob Azure est assez intelligent tooknow qu’en cas d’un objet blob appelé foo/barre, il existe un dossier appelé **foo**. Mais hello toosignify de façon uniquement un dossier vide appelé **foo** est par l’absence de ce fichier spécial de 0 octet.
* Elles contiennent des métadonnées spéciale qui sont requis par hello Hadoop système de fichiers, notamment les autorisations hello et des dossiers de hello.

## <a name="command-line-utilities"></a>Utilitaires de ligne de commande
Microsoft fournit hello suivant toowork utilitaires avec le stockage d’objets Blob Azure :

| Outil | Linux | OS X | Windows |
| --- |:---:|:---:|:---:|
| [Interface de ligne de commande Azure][azurecli] |✔ |✔ |✔ |
| [Azure PowerShell][azure-powershell] | | |✔ |
| [AzCopy][azure-azcopy] | | |✔ |
| [Commande Hadoop](#commandline) |✔ |✔ |✔ |

> [!NOTE]
> Alors que hello CLI d’Azure, Azure PowerShell et AzCopy peuvent toutes être utilisée en dehors d’Azure, hello Hadoop commande est disponible uniquement sur le cluster HDInsight de hello et autorise uniquement le chargement des données à partir du système de fichiers local hello dans le stockage Blob Azure.
>
>

### <a id="xplatcli"></a>Interface CLI Azure
Hello CLI d’Azure est un outil inter-plateformes qui vous permet de toomanage Azure services. Utilisez hello suivant le stockage d’objets Blob tooAzure étapes tooupload données :

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. [Installer et configurer hello CLI d’Azure pour Mac, Linux et Windows](../cli-install-nodejs.md).
2. Ouvrez une invite de commandes, un interpréteur de commandes ou autres interpréteur de commandes et utilisez hello suivant tooauthenticate tooyour abonnement Azure.

        azure login

    Lorsque vous y êtes invité, entrez le nom d’utilisateur hello et le mot de passe pour votre abonnement.
3. Entrez hello suivant des comptes de stockage commande toolist hello pour votre abonnement :

        azure storage account list
4. Sélectionner compte de stockage hello qui contient le blob hello souhaité toowork avec, puis utilisez hello commande tooretrieve hello clé pour ce compte suivante :

        azure storage account keys list <storage-account-name>

    Cette commande doit renvoyer les clés **primaires** et **secondaires**. Hello de copie **principal** valeur de la clé, car il sera utilisé dans les étapes suivantes hello.
5. Utilisez hello suivant commande tooretrieve une liste de conteneurs d’objets blob dans le compte de stockage hello :

        azure storage container list -a <storage-account-name> -k <primary-key>
6. Utilisez hello suivant tooupload de commandes et télécharger des objets blob toohello de fichiers :

   * tooupload un fichier :

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * toodownload un fichier :

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> Si vous travaillez toujours avec hello même compte de stockage, vous pouvez définir hello suivant des variables d’environnement au lieu de spécifier le compte de hello et la clé pour chaque commande :
>
> * **AZURE\_stockage\_compte**: nom de compte de stockage hello
> * **AZURE\_stockage\_accès\_clé**: clé de compte de stockage hello
>
>

### <a id="powershell"></a>Azure PowerShell
Azure PowerShell est un environnement de script que vous pouvez utiliser toocontrol et automatiser le déploiement de hello et la gestion de vos charges de travail dans Azure. Pour plus d’informations sur la configuration de votre station de travail de toorun Azure PowerShell, consultez [installer et configurer Azure PowerShell](/powershell/azure/overview).

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

**tooupload un stockage d’objets Blob de tooAzure fichier local**

1. Console d’Azure PowerShell hello ouvert comme indiqué dans [installer et configurer Azure PowerShell](/powershell/azure/overview).
2. Définir des cinq premières variables valeurs hello Hello Bonjour script suivant :

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get hello storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create hello storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy hello file from local workstation toohello Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. Hello de coller dans hello Azure PowerShell console toorun il toocopy hello fichier script.

Par exemple toowork de création de scripts PowerShell hdinsight, consultez [outils HDInsight](https://github.com/blackmist/hdinsight-tools).

### <a id="azcopy"></a>AzCopy
AzCopy est un outil de ligne de commande qui est conçu de tâche de hello toosimplify de transfert de données dans et hors d’un compte de stockage Azure. Vous pouvez l'utiliser comme un outil indépendant ou l'incorporer dans une application existante. [Téléchargement d’AzCopy][azure-azcopy-download].

Hello AzCopy syntaxe est la suivante :

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

Pour plus d’informations, consultez la page [AzCopy : téléchargement de fichiers pour les objets blob Azure][azure-azcopy].

### <a id="commandline"></a>Ligne de commande Hadoop
ligne de commande Hadoop Hello est uniquement utile pour le stockage des données dans le stockage d’objets blob lorsque les données de salutation sont déjà présentes sur le nœud principal du cluster hello.

Bonjour toouse de commande Hadoop commande, vous devez d’abord connecter nœud principal toohello en utilisant l’une des méthodes suivantes de hello :

* **HDInsight Windows**: [connexion à l'aide du Bureau à distance](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)
* **HDInsight de basés sur Linux**: se connecter à l’aide de SSH ([hello commande SSH](hdinsight-hadoop-linux-use-ssh-unix.md) ou [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))

Une fois connecté, vous pouvez utiliser hello suivant tooupload de syntaxe un toostorage de fichier.

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

Par exemple, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`

Système de fichiers par défaut hello pour HDInsight se trouve dans le stockage Blob Azure, /example/data.txt est réellement dans le stockage d’objets Blob Azure. Vous pouvez également consulter le fichier toohello en tant que :

    wasb:///example/data/data.txt

ou

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

Pour obtenir la liste des autres commandes Hadoop qui fonctionnent avec des fichiers, consultez [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)

> [!WARNING]
> Sur des clusters HBase, taille de bloc hello par défaut utilisé lors de l’écriture de données est de 256 Ko. Alors que cela fonctionne bien lorsque vous utilisez HBase APIs ou des API REST, à l’aide de hello `hadoop` ou `hdfs dfs` supérieure à environ 12 Go de données de toowrite commandes génère une erreur. Consultez hello [exception de stockage pour l’écriture sur l’objet blob](#storageexception) section ci-dessous pour plus d’informations.
>
>

## <a name="graphical-clients"></a>Clients graphiques
Plusieurs applications fournissent également une interface graphique pour utiliser Azure Storage. Hello Voici une liste de quelques-unes de ces applications :

| Client | Linux | OS X | Windows |
| --- |:---:|:---:|:---:|
| [Outils Microsoft Visual Studio pour HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |✔ |✔ |✔ |
| [Azure Storage Explorer](http://storageexplorer.com/) |✔ |✔ |✔ |
| [Cloud Storage Studio 2](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |✔ |
| [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) | | |✔ |
| [Azure Explorer](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |✔ |
| [Cyberduck](https://cyberduck.io/) | |✔ |✔ |

### <a name="visual-studio-tools-for-hdinsight"></a>Outils Visual Studio pour HDInsight
Pour plus d’informations, consultez [naviguer hello de ressources liées](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).

### <a id="storageexplorer"></a>Azure Storage Explorer
*Explorateur de stockage Azure* est un outil utile pour examiner et modifier les données de salutation dans des objets BLOB. Il s’agit d’un outil gratuit que vous pouvez télécharger depuis la page [http://storageexplorer.com/](http://storageexplorer.com/). code source de Hello est disponible à partir de ce lien également.

Avant d’utiliser l’outil de hello, vous devez connaître votre clé et le nom du compte stockage Azure. Pour obtenir des instructions sur l’obtention de ces informations, consultez hello « Comment : afficher, copier et régénérer stockage clés d’accès « section de [créer, gérer ou supprimer un compte de stockage][azure-create-storage-account].

1. Exécutez Azure Storage Explorer. S’il s’agit hello première fois que vous avez exécuté hello Explorateur de stockage, vous demandera hello **nom du compte de _stockage** et **clé de compte de stockage**. Si vous avez exécuté avant, utilisez hello **ajouter** bouton tooadd un nouveau nom de compte de stockage et la clé.

    Entrez hello nom et clé hello compte de stockage utilisé par votre cluster HDInsight, puis sélectionnez **Enregistrer & Ouvrir**.

    ![HDI.AzureStorageExplorer][image-azure-storage-explorer]
2. Dans la liste hello de gauche de toohello de conteneurs de l’interface de hello, cliquez sur nom hello conteneur hello qui est associé à votre cluster HDInsight. Par défaut, ce nom hello du cluster HDInsight de hello, mais peut être différent si vous avez entré un nom spécifique lors de la création du cluster de hello.
3. À partir de la barre d’outils hello, sélectionnez l’icône de téléchargement hello.

    ![Barre d’outils avec icône téléchargement mise en surbrillance](./media/hdinsight-upload-data/toolbar.png)
4. Spécifiez un tooupload de fichier, puis cliquez sur **ouvrir**. Lorsque vous y êtes invité, sélectionnez **télécharger** racine de toohello tooupload hello fichier hello du conteneur de stockage. Si vous souhaitez tooupload hello fichier tooa chemin d’accès spécifique, entrez le chemin d’accès hello dans hello **Destination** champ, puis sélectionnez **télécharger**.

    ![Boîte de dialogue de téléchargement de fichier](./media/hdinsight-upload-data/fileupload.png)

    Une fois le téléchargement du fichier hello a terminé, vous pouvez l’utiliser à partir des travaux sur le cluster HDInsight de hello.

## <a name="mount-azure-blob-storage-as-local-drive"></a>Monter le stockage d'objets Blob Azure comme un lecteur Local
Consultez [Monter un objet Blob Azure en tant que lecteur Local](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).

## <a name="services"></a>Services
### <a name="azure-data-factory"></a>Azure Data Factory
Hello service Azure Data Factory est un service entièrement géré pour composer des services de déplacement de données de stockage et le traitement des données de données dans des pipelines de production de données simplifiée, évolutive et fiable.

Azure Data Factory peut être utilisé toomove des données dans le stockage d’objets Blob Azure, ou toocreate des pipelines de données qui utilisent directement HDInsight fonctionnalités telles que la ruche et porc.

Pour plus d’informations, consultez hello [documentation d’Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/).

### <a id="sqoop"></a>Apache Sqoop
Sqoop est un outil conçu de données tootransfer entre Hadoop et des bases de données relationnelles. Vous pouvez l’utiliser tooimport des données à partir d’un système de gestion de base de données relationnelle (SGBDR), telles que SQL Server, MySQL ou Oracle dans le système de fichiers DFS Hadoop hello (HDFS), transformer des données dans Hadoop MapReduce ou ruche hello et puis exporter les données hello dans un SGBDR.

Pour plus d’informations, consultez [Utilisation de Sqoop avec HDInsight][hdinsight-use-sqoop].

## <a name="development-sdks"></a>Kits de développement logiciel (SDK) de développement
Stockage d’objets Blob Azure également accessibles à l’aide d’un kit de développement Azure à partir de hello suivant des langages de programmation :

* .NET
* Java
* Node.js
* PHP
* Python
* Ruby

Pour plus d’informations sur l’installation Bonjour Azure SDK, consultez [téléchargements Azure](https://azure.microsoft.com/downloads/)

## <a name="troubleshooting"></a>Résolution des problèmes
### <a id="storageexception"></a>Exception de stockage pour l’écriture sur un objet blob
**Symptômes**: lors de l’utilisation de hello `hadoop` ou `hdfs dfs` toowrite des fichiers de commandes sont environ 12 Go ou plus sur un cluster HBase, vous pouvez rencontrer hello l’erreur suivante :

    ERROR azure.NativeAzureFileSystem: Encountered Storage Exception for write on Blob : example/test_large_file.bin._COPYING_ Exception details: null Error Code : RequestBodyTooLarge
    copyFromLocal: java.io.IOException
            at com.microsoft.azure.storage.core.Utility.initIOException(Utility.java:661)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:366)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:350)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:471)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
            at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
            at java.lang.Thread.run(Thread.java:745)
    Caused by: com.microsoft.azure.storage.StorageException: hello request body is too large and exceeds hello maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

**Cause**: taille de bloc tooa par défaut de 256 Ko des clusters HBase sur HDInsight lors de l’écriture de tooAzure stockage. Bien que cela fonctionne pour HBase APIs ou des API REST, il entraîne une erreur lors de l’utilisation de hello `hadoop` ou `hdfs dfs` des utilitaires de ligne de commande.

**Résolution**: utilisez `fs.azure.write.request.size` toospecify une plus grande taille de bloc. Cela à l’aide de hello sur une base individuelle `-D` paramètre. Hello Voici un exemple d’utilisation de ce paramètre avec hello `hadoop` commande :

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

Vous pouvez également augmenter la valeur hello `fs.azure.write.request.size` globalement à l’aide de Ambari. Hello suit peut être utilisé la valeur de hello de toochange Bonjour l’interface utilisateur de Ambari Web :

1. Dans votre navigateur, accédez à toohello l’interface utilisateur de Ambari Web pour votre cluster. Il s’agit de https://CLUSTERNAME.azurehdinsight.net, où **CLUSTERNAME** est le nom hello de votre cluster.

    Lorsque vous y êtes invité, entrez le nom de l’administrateur hello et le mot de passe pour le cluster de hello.
2. Bonjour à gauche de l’écran hello, sélectionnez **HDFS**, puis sélectionnez hello **configurations** onglet.
3. Bonjour **filtre...**  , saisissez `fs.azure.write.request.size`. Champ de hello et la valeur actuelle s’affiche au milieu de hello de page de hello.
4. Remplacez hello 262144 (256 Ko) toohello nouvelle valeur par. Par exemple, 4194304 (4 Mo).

![Image de la modification de valeur hello via l’interface utilisateur de Ambari Web](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

Pour plus d’informations sur l’utilisation de Ambari, consultez [gérer les clusters HDInsight à l’aide de hello l’interface utilisateur de Ambari Web](hdinsight-hadoop-manage-ambari.md).

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous comprenez comment lire les données de tooget dans HDInsight, hello suivant articles toolearn comment tooperform analyse :

* [Prise en main d’Azure HDInsight][hdinsight-get-started]
* [Envoi de tâches Hadoop par programme][hdinsight-submit-jobs]
* [Utilisation de Hive avec HDInsight][hdinsight-use-hive]
* [Utilisation de Pig avec HDInsight][hdinsight-use-pig]

[azure-management-portal]: https://porta.azure.com
[azure-powershell]: http://msdn.microsoft.com/library/windowsazure/jj152841.aspx

[azure-storage-client-library]: /develop/net/how-to-guides/blob-storage/
[azure-create-storage-account]:../storage/common/storage-create-storage-account.md
[azure-azcopy-download]:../storage/common/storage-use-azcopy.md
[azure-azcopy]:../storage/common/storage-use-azcopy.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md

[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[sqldatabase-create-configure]: ../sql-database-create-configure.md

[apache-sqoop-guide]: http://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[azurecli]: ../cli-install-nodejs.md


[image-azure-storage-explorer]: ./media/hdinsight-upload-data/HDI.AzureStorageExplorer.png
[image-ase-addaccount]: ./media/hdinsight-upload-data/HDI.ASEAddAccount.png
[image-ase-blob]: ./media/hdinsight-upload-data/HDI.ASEBlob.png
