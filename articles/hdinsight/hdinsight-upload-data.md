---
title: "Téléchargement de données pour les tâches Hadoop dans HDInsight | Microsoft Docs"
description: "Découvrez comment télécharger des données pour les tâches Hadoop et y accéder dans HDInsight avec l'interface CLI Azure, Azure Storage Explorer, Azure PowerShell, la ligne de commande Hadoop ou Sqoop."
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
ms.openlocfilehash: 6867f96c8ea0e31ed0e682cef48e7aa5e3f65f86
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a><span data-ttu-id="14950-104">Téléchargement de données pour les tâches Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="14950-104">Upload data for Hadoop jobs in HDInsight</span></span>
<span data-ttu-id="14950-105">Azure HDInsight fournit un système HDFS (Hadoo Distributed File System) complet pour le stockage d'objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="14950-105">Azure HDInsight provides a full-featured Hadoop distributed file system (HDFS) over Azure Blob storage.</span></span> <span data-ttu-id="14950-106">Il est conçu en tant qu’extension HDFS pour fournir une expérience transparente aux clients.</span><span class="sxs-lookup"><span data-stu-id="14950-106">It is designed as an HDFS extension to provide a seamless experience to customers.</span></span> <span data-ttu-id="14950-107">Il permet à l'ensemble des composants de l'écosystème Hadoop de fonctionner directement sur les données qu'il gère.</span><span class="sxs-lookup"><span data-stu-id="14950-107">It enables the full set of components in the Hadoop ecosystem to operate directly on the data it manages.</span></span> <span data-ttu-id="14950-108">Le stockage d'objets blob Azure et HDFS sont des systèmes de fichiers distincts qui sont optimisés pour le stockage de données et pour les calculs réalisés à partir de ces données.</span><span class="sxs-lookup"><span data-stu-id="14950-108">Azure Blob storage and HDFS are distinct file systems that are optimized for storage of data and computations on that data.</span></span> <span data-ttu-id="14950-109">Pour connaître les avantages que constitue l’utilisation du stockage d’objets blob Azure, consultez la page [Utilisation du stockage d’objets blob Azure avec HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="14950-109">For information about the benefits of using Azure Blob storage, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="14950-110">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="14950-110">**Prerequisites**</span></span>

<span data-ttu-id="14950-111">Notez la configuration requise avant de démarrer :</span><span class="sxs-lookup"><span data-stu-id="14950-111">Note the following requirement before you begin:</span></span>

* <span data-ttu-id="14950-112">Un cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="14950-112">An Azure HDInsight cluster.</span></span> <span data-ttu-id="14950-113">Pour obtenir des instructions, consultez le didacticiel [Prise en main d’Azure HDInsight][hdinsight-get-started] ou la rubrique [Mise en service de clusters HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="14950-113">For instructions, see [Get started with Azure HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span>

## <a name="why-blob-storage"></a><span data-ttu-id="14950-114">Qu'est-ce que le stockage d'objets blob ?</span><span class="sxs-lookup"><span data-stu-id="14950-114">Why blob storage?</span></span>
<span data-ttu-id="14950-115">Les clusters Azure HDInsight sont généralement déployés pour exécuter des tâches MapReduce et sont supprimés une fois ces tâches terminées.</span><span class="sxs-lookup"><span data-stu-id="14950-115">Azure HDInsight clusters are typically deployed to run MapReduce jobs, and the clusters are dropped after these jobs complete.</span></span> <span data-ttu-id="14950-116">Conserver les données dans les clusters HDFS une fois les calculs terminés serait une façon onéreuse de stocker ces données.</span><span class="sxs-lookup"><span data-stu-id="14950-116">Keeping the data in the HDFS clusters after computations are complete would be an expensive way to store this data.</span></span> <span data-ttu-id="14950-117">Le stockage d'objets blob Azure constitue une option de stockage à long terme économique, partageable, hautement évolutive et disponible pour les données qui doivent être traitées à l'aide de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="14950-117">Azure Blob storage is a highly available, highly scalable, high capacity, low cost, and shareable storage option for data that is to be processed using HDInsight.</span></span> <span data-ttu-id="14950-118">Le stockage de données dans un objet blob permet de libérer en toute sécurité les clusters HDInsight utilisés pour les calculs, sans perte de données.</span><span class="sxs-lookup"><span data-stu-id="14950-118">Storing data in a blob enables the HDInsight clusters that are used for computation to be safely released without losing data.</span></span>

### <a name="directories"></a><span data-ttu-id="14950-119">Répertoires</span><span class="sxs-lookup"><span data-stu-id="14950-119">Directories</span></span>
<span data-ttu-id="14950-120">Les conteneurs de stockage d'objets blob Azure stockent des données en tant que paires clé/valeur et sans hiérarchie de répertoires.</span><span class="sxs-lookup"><span data-stu-id="14950-120">Azure Blob storage containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="14950-121">Cependant, vous pouvez utiliser le caractère « / » dans le nom de la clé pour la faire apparaître comme un fichier stocké dans une structure de répertoires.</span><span class="sxs-lookup"><span data-stu-id="14950-121">However the "/" character can be used within the key name to make it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="14950-122">HDInsight les interprète comme des répertoires réels.</span><span class="sxs-lookup"><span data-stu-id="14950-122">HDInsight sees these as if they are actual directories.</span></span>

<span data-ttu-id="14950-123">Par exemple, une clé d'objet blob peut être *input/log1.txt*.</span><span class="sxs-lookup"><span data-stu-id="14950-123">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="14950-124">Il n'existe pas de répertoire « input », mais le caractère « / » figurant dans le nom de la clé lui donne l'aspect d'un chemin d'accès de fichier.</span><span class="sxs-lookup"><span data-stu-id="14950-124">No actual "input" directory exists, but due to the presence of the "/" character in the key name, it has the appearance of a file path.</span></span>

<span data-ttu-id="14950-125">Pour cette raison, quand vous utilisez les outils d'Azure Explorer, vous pouvez remarquer la présence de fichiers de 0 octet.</span><span class="sxs-lookup"><span data-stu-id="14950-125">Because of this, if you use Azure Explorer tools you may notice some 0 byte files.</span></span> <span data-ttu-id="14950-126">Ces fichiers ont deux utilités :</span><span class="sxs-lookup"><span data-stu-id="14950-126">These files serve two purposes:</span></span>

* <span data-ttu-id="14950-127">S'il existe des dossiers vides, ils servent à indiquer l'existence du dossier.</span><span class="sxs-lookup"><span data-stu-id="14950-127">If there are empty folders, they mark of the existence of the folder.</span></span> <span data-ttu-id="14950-128">Le stockage d'objets blob Azure sait que si un objet blob est nommé foo/bar, c'est qu'il y a un dossier nommé **foo**.</span><span class="sxs-lookup"><span data-stu-id="14950-128">Azure Blob storage is clever enough to know that if a blob called foo/bar exists, there is a folder called **foo**.</span></span> <span data-ttu-id="14950-129">Mais la seule façon d'indiquer un dossier vide nommé **foo** est de disposer de ces fichiers de 0 octet.</span><span class="sxs-lookup"><span data-stu-id="14950-129">But the only way to signify an empty folder called **foo** is by having this special 0 byte file in place.</span></span>
* <span data-ttu-id="14950-130">Ils contiennent des métadonnées spécifiques requises par le système de fichiers Hadoop, notamment les autorisations et les propriétaires des dossiers.</span><span class="sxs-lookup"><span data-stu-id="14950-130">They hold special metadata that is needed by the Hadoop file system, notably the permissions and owners for the folders.</span></span>

## <a name="command-line-utilities"></a><span data-ttu-id="14950-131">Utilitaires de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="14950-131">Command-line utilities</span></span>
<span data-ttu-id="14950-132">Microsoft fournit les utilitaires suivants pour utiliser le stockage d'objets blob Azure :</span><span class="sxs-lookup"><span data-stu-id="14950-132">Microsoft provides the following utilities to work with Azure Blob storage:</span></span>

| <span data-ttu-id="14950-133">Outil</span><span class="sxs-lookup"><span data-stu-id="14950-133">Tool</span></span> | <span data-ttu-id="14950-134">Linux</span><span class="sxs-lookup"><span data-stu-id="14950-134">Linux</span></span> | <span data-ttu-id="14950-135">OS X</span><span class="sxs-lookup"><span data-stu-id="14950-135">OS X</span></span> | <span data-ttu-id="14950-136">Windows</span><span class="sxs-lookup"><span data-stu-id="14950-136">Windows</span></span> |
| --- |:---:|:---:|:---:|
| <span data-ttu-id="14950-137">[Interface de ligne de commande Azure][azurecli]</span><span class="sxs-lookup"><span data-stu-id="14950-137">[Azure Command-Line Interface][azurecli]</span></span> |<span data-ttu-id="14950-138">✔</span><span class="sxs-lookup"><span data-stu-id="14950-138">✔</span></span> |<span data-ttu-id="14950-139">✔</span><span class="sxs-lookup"><span data-stu-id="14950-139">✔</span></span> |<span data-ttu-id="14950-140">✔</span><span class="sxs-lookup"><span data-stu-id="14950-140">✔</span></span> |
| <span data-ttu-id="14950-141">[Azure PowerShell][azure-powershell]</span><span class="sxs-lookup"><span data-stu-id="14950-141">[Azure PowerShell][azure-powershell]</span></span> | | |<span data-ttu-id="14950-142">✔</span><span class="sxs-lookup"><span data-stu-id="14950-142">✔</span></span> |
| <span data-ttu-id="14950-143">[AzCopy][azure-azcopy]</span><span class="sxs-lookup"><span data-stu-id="14950-143">[AzCopy][azure-azcopy]</span></span> | | |<span data-ttu-id="14950-144">✔</span><span class="sxs-lookup"><span data-stu-id="14950-144">✔</span></span> |
| [<span data-ttu-id="14950-145">Commande Hadoop</span><span class="sxs-lookup"><span data-stu-id="14950-145">Hadoop command</span></span>](#commandline) |<span data-ttu-id="14950-146">✔</span><span class="sxs-lookup"><span data-stu-id="14950-146">✔</span></span> |<span data-ttu-id="14950-147">✔</span><span class="sxs-lookup"><span data-stu-id="14950-147">✔</span></span> |<span data-ttu-id="14950-148">✔</span><span class="sxs-lookup"><span data-stu-id="14950-148">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="14950-149">Alors que l'interface CLI Azure, Azure PowerShell et AzCopy peuvent tous être utilisés en dehors d'Azure, la commande Hadoop est disponible uniquement sur le cluster HDInsight et autorise uniquement le chargement de données du système de fichiers local dans le stockage d'objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="14950-149">While the Azure CLI, Azure PowerShell, and AzCopy can all be used from outside Azure, the Hadoop command is only available on the HDInsight cluster and only allows loading data from the local file system into Azure Blob storage.</span></span>
>
>

### <span data-ttu-id="14950-150"><a id="xplatcli"></a>Interface CLI Azure</span><span class="sxs-lookup"><span data-stu-id="14950-150"><a id="xplatcli"></a>Azure CLI</span></span>
<span data-ttu-id="14950-151">L'interface CLI Azure est un outil interplateforme qui vous permet de gérer les services Azure.</span><span class="sxs-lookup"><span data-stu-id="14950-151">The Azure CLI is a cross-platform tool that allows you to manage Azure services.</span></span> <span data-ttu-id="14950-152">Pour télécharger des données vers le stockage d'objets blob Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="14950-152">Use the following steps to upload data to Azure Blob storage:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="14950-153">[Installation et configuration de l'interface de ligne de commande Azure pour Mac, Linux et Windows](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="14950-153">[Install and configure the Azure CLI for Mac, Linux and Windows](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="14950-154">Ouvrez une invite de commandes, un bash ou un autre shell et procédez comme suit pour vous authentifier auprès de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="14950-154">Open a command prompt, bash, or other shell, and use the following to authenticate to your Azure subscription.</span></span>

        azure login

    <span data-ttu-id="14950-155">Lorsque vous y êtes invité, entrez le nom d'utilisateur et le mot de passe de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="14950-155">When prompted, enter the user name and password for your subscription.</span></span>
3. <span data-ttu-id="14950-156">Entrez la commande suivante pour répertorier les comptes de stockage pour votre abonnement :</span><span class="sxs-lookup"><span data-stu-id="14950-156">Enter the following command to list the storage accounts for your subscription:</span></span>

        azure storage account list
4. <span data-ttu-id="14950-157">Sélectionnez le compte de stockage qui contient l'objet blob que vous souhaitez utiliser, puis entrez la commande suivante pour récupérer la clé de ce compte :</span><span class="sxs-lookup"><span data-stu-id="14950-157">Select the storage account that contains the blob you want to work with, then use the following command to retrieve the key for this account:</span></span>

        azure storage account keys list <storage-account-name>

    <span data-ttu-id="14950-158">Cette commande doit renvoyer les clés **primaires** et **secondaires**.</span><span class="sxs-lookup"><span data-stu-id="14950-158">This should return **Primary** and **Secondary** keys.</span></span> <span data-ttu-id="14950-159">Copiez la valeur de la clé **primaire** , car vous devrez l’utiliser lors des étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="14950-159">Copy the **Primary** key value because it will be used in the next steps.</span></span>
5. <span data-ttu-id="14950-160">Utilisez la commande suivante pour récupérer une liste de conteneurs d'objets blob dans le compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="14950-160">Use the following command to retrieve a list of blob containers within the storage account:</span></span>

        azure storage container list -a <storage-account-name> -k <primary-key>
6. <span data-ttu-id="14950-161">Utilisez les commandes suivantes pour charger et télécharger des fichiers vers l'objet blob :</span><span class="sxs-lookup"><span data-stu-id="14950-161">Use the following commands to upload and download files to the blob:</span></span>

   * <span data-ttu-id="14950-162">Pour charger un fichier :</span><span class="sxs-lookup"><span data-stu-id="14950-162">To upload a file:</span></span>

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * <span data-ttu-id="14950-163">Pour télécharger un fichier :</span><span class="sxs-lookup"><span data-stu-id="14950-163">To download a file:</span></span>

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> <span data-ttu-id="14950-164">Si vous utilisez toujours le même compte de stockage, vous pouvez définir les variables d'environnement suivantes au lieu de spécifier le compte et la clé de chaque commande :</span><span class="sxs-lookup"><span data-stu-id="14950-164">If you will always be working with the same storage account, you can set the following environment variables instead of specifying the account and key for every command:</span></span>
>
> * <span data-ttu-id="14950-165">**AZURE\_STORAGE\_ACCOUNT** : le nom du compte de stockage</span><span class="sxs-lookup"><span data-stu-id="14950-165">**AZURE\_STORAGE\_ACCOUNT**: The storage account name</span></span>
> * <span data-ttu-id="14950-166">**AZURE\_STORAGE\_ACCESS\_KEY** : la clé du compte de stockage</span><span class="sxs-lookup"><span data-stu-id="14950-166">**AZURE\_STORAGE\_ACCESS\_KEY**: The storage account key</span></span>
>
>

### <span data-ttu-id="14950-167"><a id="powershell"></a>Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="14950-167"><a id="powershell"></a>Azure PowerShell</span></span>
<span data-ttu-id="14950-168">Azure PowerShell est un environnement de création de scripts qui vous permet de contrôler et d'automatiser le déploiement et la gestion de vos charges de travail dans Azure.</span><span class="sxs-lookup"><span data-stu-id="14950-168">Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="14950-169">Pour plus d'informations sur la configuration de votre poste de travail pour exécuter Azure PowerShell, consultez l'article [Installation et configuration d'Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="14950-169">For information about configuring your workstation to run Azure PowerShell, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="14950-170">**Téléchargement d'un fichier local vers un stockage d'objets blob Azure**</span><span class="sxs-lookup"><span data-stu-id="14950-170">**To upload a local file to Azure Blob storage**</span></span>

1. <span data-ttu-id="14950-171">Ouvrez la fenêtre de la console Azure PowerShell, comme indiqué dans la section [Installation et configuration d'Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="14950-171">Open the Azure PowerShell console as instructed in [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="14950-172">Définissez les valeurs des cinq premières variables dans le script suivant :</span><span class="sxs-lookup"><span data-stu-id="14950-172">Set the values of the first five variables in the following script:</span></span>

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get the storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create the storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy the file from local workstation to the Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. <span data-ttu-id="14950-173">Collez le script dans la console Azure PowerShell pour l'exécuter afin de copier le fichier.</span><span class="sxs-lookup"><span data-stu-id="14950-173">Paste the script into the Azure PowerShell console to run it to copy the file.</span></span>

<span data-ttu-id="14950-174">Pour des exemples de scripts PowerShell créés pour fonctionner avec HDInsight, consultez les [outils HDInsight](https://github.com/blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="14950-174">For example PowerShell scripts created to work with HDInsight, see [HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span></span>

### <span data-ttu-id="14950-175"><a id="azcopy"></a>AzCopy</span><span class="sxs-lookup"><span data-stu-id="14950-175"><a id="azcopy"></a>AzCopy</span></span>
<span data-ttu-id="14950-176">AzCopy est un utilitaire de ligne de commande conçu pour simplifier la tâche de transfert de données à destination et en provenance d'un compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="14950-176">AzCopy is a command-line tool that is designed to simplify the task of transferring data into and out of an Azure Storage account.</span></span> <span data-ttu-id="14950-177">Vous pouvez l'utiliser comme un outil indépendant ou l'incorporer dans une application existante.</span><span class="sxs-lookup"><span data-stu-id="14950-177">You can use it as a standalone tool or incorporate this tool in an existing application.</span></span> <span data-ttu-id="14950-178">[Téléchargement d’AzCopy][azure-azcopy-download].</span><span class="sxs-lookup"><span data-stu-id="14950-178">[Download AzCopy][azure-azcopy-download].</span></span>

<span data-ttu-id="14950-179">La syntaxe d'AzCopy est :</span><span class="sxs-lookup"><span data-stu-id="14950-179">The AzCopy syntax is:</span></span>

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

<span data-ttu-id="14950-180">Pour plus d’informations, consultez la page [AzCopy : téléchargement de fichiers pour les objets blob Azure][azure-azcopy].</span><span class="sxs-lookup"><span data-stu-id="14950-180">For more information, see [AzCopy - Uploading/Downloading files for Azure Blobs][azure-azcopy].</span></span>

### <span data-ttu-id="14950-181"><a id="commandline"></a>Ligne de commande Hadoop</span><span class="sxs-lookup"><span data-stu-id="14950-181"><a id="commandline"></a>Hadoop command line</span></span>
<span data-ttu-id="14950-182">La ligne de commande Hadoop est utile uniquement pour stocker les données dans le stockage d'objets blob quand celles-ci sont déjà présentes sur le nœud principal du cluster.</span><span class="sxs-lookup"><span data-stu-id="14950-182">The Hadoop command line is only useful for storing data into blob storage when the data is already present on the cluster head node.</span></span>

<span data-ttu-id="14950-183">Pour utiliser la commande Hadoop, vous devez d'abord vous connecter au nœud principal à l'aide de l'une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="14950-183">In order to use the Hadoop command, you must first connect to the headnode using one of the following methods:</span></span>

* <span data-ttu-id="14950-184">**HDInsight Windows**: [connexion à l'aide du Bureau à distance](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="14950-184">**Windows-based HDInsight**: [Connect using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>
* <span data-ttu-id="14950-185">**HDInsight Linux** : connexion à l’aide de SSH ([commande SSH](hdinsight-hadoop-linux-use-ssh-unix.md) ou [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span><span class="sxs-lookup"><span data-stu-id="14950-185">**Linux-based HDInsight**: Connect using SSH ([the SSH command](hdinsight-hadoop-linux-use-ssh-unix.md) or [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span></span>

<span data-ttu-id="14950-186">Une fois connecté, vous pouvez utiliser la syntaxe suivante pour télécharger un fichier dans le stockage.</span><span class="sxs-lookup"><span data-stu-id="14950-186">Once connected, you can use the following syntax to upload a file to storage.</span></span>

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

<span data-ttu-id="14950-187">Par exemple, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span><span class="sxs-lookup"><span data-stu-id="14950-187">For example, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span></span>

<span data-ttu-id="14950-188">Comme le système de fichiers par défaut pour HDInsight se trouve dans le stockage d'objets blob Azure, /example/data.txt s'y trouve également.</span><span class="sxs-lookup"><span data-stu-id="14950-188">Because the default file system for HDInsight is in Azure Blob storage, /example/data.txt is actually in Azure Blob storage.</span></span> <span data-ttu-id="14950-189">Vous pouvez également faire référence au fichier comme ceci :</span><span class="sxs-lookup"><span data-stu-id="14950-189">You can also refer to the file as:</span></span>

    wasb:///example/data/data.txt

<span data-ttu-id="14950-190">ou</span><span class="sxs-lookup"><span data-stu-id="14950-190">or</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

<span data-ttu-id="14950-191">Pour obtenir la liste des autres commandes Hadoop qui fonctionnent avec des fichiers, consultez [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span><span class="sxs-lookup"><span data-stu-id="14950-191">For a list of other Hadoop commands that work with files, see [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span></span>

> [!WARNING]
> <span data-ttu-id="14950-192">Sur les clusters HBase, la taille de bloc par défaut lors de l’écriture de données est de 256 Ko.</span><span class="sxs-lookup"><span data-stu-id="14950-192">On HBase clusters, the default block size used when writing data is 256KB.</span></span> <span data-ttu-id="14950-193">Bien que cela fonctionne bien lorsque vous utilisez les API HBase ou les API REST, l’utilisation des commandes `hadoop` ou `hdfs dfs` pour écrire des données supérieures à ~12 Go génère une erreur.</span><span class="sxs-lookup"><span data-stu-id="14950-193">While this works fine when using HBase APIs or REST APIs, using the `hadoop` or `hdfs dfs` commands to write data larger than ~12GB results in an error.</span></span> <span data-ttu-id="14950-194">Consultez la section [Exception de stockage pour l’écriture sur un objet blob](#storageexception) ci-dessous pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="14950-194">See the [storage exception for write on blob](#storageexception) section below for more information.</span></span>
>
>

## <a name="graphical-clients"></a><span data-ttu-id="14950-195">Clients graphiques</span><span class="sxs-lookup"><span data-stu-id="14950-195">Graphical clients</span></span>
<span data-ttu-id="14950-196">Plusieurs applications fournissent également une interface graphique pour utiliser Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="14950-196">There are also several applications that provide a graphical interface for working with Azure Storage.</span></span> <span data-ttu-id="14950-197">Voici une liste de quelques-unes de ces applications :</span><span class="sxs-lookup"><span data-stu-id="14950-197">The following is a list of a few of these applications:</span></span>

| <span data-ttu-id="14950-198">Client</span><span class="sxs-lookup"><span data-stu-id="14950-198">Client</span></span> | <span data-ttu-id="14950-199">Linux</span><span class="sxs-lookup"><span data-stu-id="14950-199">Linux</span></span> | <span data-ttu-id="14950-200">OS X</span><span class="sxs-lookup"><span data-stu-id="14950-200">OS X</span></span> | <span data-ttu-id="14950-201">Windows</span><span class="sxs-lookup"><span data-stu-id="14950-201">Windows</span></span> |
| --- |:---:|:---:|:---:|
| [<span data-ttu-id="14950-202">Outils Microsoft Visual Studio pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="14950-202">Microsoft Visual Studio Tools for HDInsight</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |<span data-ttu-id="14950-203">✔</span><span class="sxs-lookup"><span data-stu-id="14950-203">✔</span></span> |<span data-ttu-id="14950-204">✔</span><span class="sxs-lookup"><span data-stu-id="14950-204">✔</span></span> |<span data-ttu-id="14950-205">✔</span><span class="sxs-lookup"><span data-stu-id="14950-205">✔</span></span> |
| [<span data-ttu-id="14950-206">Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="14950-206">Azure Storage Explorer</span></span>](http://storageexplorer.com/) |<span data-ttu-id="14950-207">✔</span><span class="sxs-lookup"><span data-stu-id="14950-207">✔</span></span> |<span data-ttu-id="14950-208">✔</span><span class="sxs-lookup"><span data-stu-id="14950-208">✔</span></span> |<span data-ttu-id="14950-209">✔</span><span class="sxs-lookup"><span data-stu-id="14950-209">✔</span></span> |
| [<span data-ttu-id="14950-210">Cloud Storage Studio 2</span><span class="sxs-lookup"><span data-stu-id="14950-210">Cloud Storage Studio 2</span></span>](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |<span data-ttu-id="14950-211">✔</span><span class="sxs-lookup"><span data-stu-id="14950-211">✔</span></span> |
| [<span data-ttu-id="14950-212">CloudXplorer</span><span class="sxs-lookup"><span data-stu-id="14950-212">CloudXplorer</span></span>](http://clumsyleaf.com/products/cloudxplorer) | | |<span data-ttu-id="14950-213">✔</span><span class="sxs-lookup"><span data-stu-id="14950-213">✔</span></span> |
| [<span data-ttu-id="14950-214">Azure Explorer</span><span class="sxs-lookup"><span data-stu-id="14950-214">Azure Explorer</span></span>](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |<span data-ttu-id="14950-215">✔</span><span class="sxs-lookup"><span data-stu-id="14950-215">✔</span></span> |
| [<span data-ttu-id="14950-216">Cyberduck</span><span class="sxs-lookup"><span data-stu-id="14950-216">Cyberduck</span></span>](https://cyberduck.io/) | |<span data-ttu-id="14950-217">✔</span><span class="sxs-lookup"><span data-stu-id="14950-217">✔</span></span> |<span data-ttu-id="14950-218">✔</span><span class="sxs-lookup"><span data-stu-id="14950-218">✔</span></span> |

### <a name="visual-studio-tools-for-hdinsight"></a><span data-ttu-id="14950-219">Outils Visual Studio pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="14950-219">Visual Studio Tools for HDInsight</span></span>
<span data-ttu-id="14950-220">Pour plus d’informations, consultez [Accéder aux ressources liées](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span><span class="sxs-lookup"><span data-stu-id="14950-220">For more information, see [Navigate the linked resources](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span></span>

### <span data-ttu-id="14950-221"><a id="storageexplorer"></a>Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="14950-221"><a id="storageexplorer"></a>Azure Storage Explorer</span></span>
<span data-ttu-id="14950-222">*Azure Storage Explorer* est un outil utile pour examiner et modifier les données de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="14950-222">*Azure Storage Explorer* is a useful tool for inspecting and altering the data in blobs.</span></span> <span data-ttu-id="14950-223">Il s’agit d’un outil gratuit que vous pouvez télécharger depuis la page [http://storageexplorer.com/](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="14950-223">It is a free, open source tool that can be downloaded from [http://storageexplorer.com/](http://storageexplorer.com/).</span></span> <span data-ttu-id="14950-224">Le code source est également disponible à partir de ce lien.</span><span class="sxs-lookup"><span data-stu-id="14950-224">The source code is available from this link as well.</span></span>

<span data-ttu-id="14950-225">Avant de l'utiliser, vous devez connaître le nom et la clé de votre compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="14950-225">Before using the tool, you must know your Azure storage account name and account key.</span></span> <span data-ttu-id="14950-226">Pour obtenir des instructions permettant d’obtenir ces informations, consultez la section « Affichage, copie et régénération des clés d’accès de stockage » de l’article [Création, gestion et suppression d’un compte de stockage][azure-create-storage-account].</span><span class="sxs-lookup"><span data-stu-id="14950-226">For instructions about getting this information, see the "How to: View, copy and regenerate storage access keys" section of [Create, manage, or delete a storage account][azure-create-storage-account].</span></span>

1. <span data-ttu-id="14950-227">Exécutez Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="14950-227">Run Azure Storage Explorer.</span></span> <span data-ttu-id="14950-228">Si vous exécutez l’Explorateur de stockage pour la première fois, vous êtes invité à saisir le **_Nom du compte de stockage** et la **Clé du compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="14950-228">If this is the first time you have run the Storage Explorer, you will be prompted for the **_Storage account name** and **Storage account key**.</span></span> <span data-ttu-id="14950-229">Si vous avez déjà exécuté l’Explorateur de stockage, utilisez le bouton **Ajouter** pour ajouter un nom et une clé de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="14950-229">If you have run it before, use the **Add** button to add a new storage account name and key.</span></span>

    <span data-ttu-id="14950-230">Entrez le nom et la clé du compte de stockage utilisé par votre cluster HDinsight, puis sélectionnez **ENREGISTRER ET OUVRIR**.</span><span class="sxs-lookup"><span data-stu-id="14950-230">Enter the name and key for the storage account used by your HDInsight cluster and then select **SAVE & OPEN**.</span></span>

    ![HDI.AzureStorageExplorer][image-azure-storage-explorer]
2. <span data-ttu-id="14950-232">Dans la liste de conteneurs située à gauche de l’interface, cliquez sur le nom du conteneur associé à votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="14950-232">In the list of containers to the left of the interface, click the name of the container that is associated with your HDInsight cluster.</span></span> <span data-ttu-id="14950-233">Par défaut, il s’agit du nom du cluster HDInsight, mais il peut être différent si vous avez entré un nom spécifique lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="14950-233">By default, this is the name of the HDInsight cluster, but may be different if you entered a specific name when creating the cluster.</span></span>
3. <span data-ttu-id="14950-234">Dans la barre d’outils, sélectionnez l’icône de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="14950-234">From the tool bar, select the upload icon.</span></span>

    ![Barre d’outils avec icône téléchargement mise en surbrillance](./media/hdinsight-upload-data/toolbar.png)
4. <span data-ttu-id="14950-236">Indiquez un fichier à télécharger, puis cliquez sur **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="14950-236">Specify a file to upload, and then click **Open**.</span></span> <span data-ttu-id="14950-237">Lorsque vous y êtes invité, sélectionnez **Télécharger** pour télécharger le fichier vers la racine du conteneur de stockage.</span><span class="sxs-lookup"><span data-stu-id="14950-237">When prompted, select **Upload** to upload the file to the root of the storage container.</span></span> <span data-ttu-id="14950-238">Si vous souhaitez télécharger le fichier vers un chemin d’accès spécifique, entrez-le dans le champ **Destination**, puis sélectionnez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="14950-238">If you want to upload the file to a specific path, enter the path in the **Destination** field and then select **Upload**.</span></span>

    ![Boîte de dialogue de téléchargement de fichier](./media/hdinsight-upload-data/fileupload.png)

    <span data-ttu-id="14950-240">Une fois le téléchargement du fichier terminé, vous pouvez l’utiliser à partir des tâches du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="14950-240">Once the file has finished uploading, you can use it from jobs on the HDInsight cluster.</span></span>

## <a name="mount-azure-blob-storage-as-local-drive"></a><span data-ttu-id="14950-241">Monter le stockage d'objets Blob Azure comme un lecteur Local</span><span class="sxs-lookup"><span data-stu-id="14950-241">Mount Azure Blob Storage as Local Drive</span></span>
<span data-ttu-id="14950-242">Consultez [Monter un objet Blob Azure en tant que lecteur Local](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span><span class="sxs-lookup"><span data-stu-id="14950-242">See [Mount Azure Blob Storage as Local Drive](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span></span>

## <a name="services"></a><span data-ttu-id="14950-243">Services</span><span class="sxs-lookup"><span data-stu-id="14950-243">Services</span></span>
### <a name="azure-data-factory"></a><span data-ttu-id="14950-244">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="14950-244">Azure Data Factory</span></span>
<span data-ttu-id="14950-245">Le service Azure Data Factory est un service entièrement géré pour composer des services de stockage de données, de traitement de données et de déplacement de données dans des pipelines de production rationalisés, évolutifs et fiables.</span><span class="sxs-lookup"><span data-stu-id="14950-245">The Azure Data Factory service is a fully managed service for composing data storage, data processing, and data movement services into streamlined, scalable, and reliable data production pipelines.</span></span>

<span data-ttu-id="14950-246">Azure Data Factory permet de déplacer des données dans le stockage d'objets blob Azure ou de créer des pipelines de données qui utilisent directement des fonctionnalités HDInsight telles que Hive et Pig.</span><span class="sxs-lookup"><span data-stu-id="14950-246">Azure Data Factory can be used to move data into Azure Blob storage, or to create data pipelines that directly use HDInsight features such as Hive and Pig.</span></span>

<span data-ttu-id="14950-247">Pour plus d'informations, consultez la [Documentation Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="14950-247">For more information, see the [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/).</span></span>

### <span data-ttu-id="14950-248"><a id="sqoop"></a>Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="14950-248"><a id="sqoop"></a>Apache Sqoop</span></span>
<span data-ttu-id="14950-249">Sqoop est un outil conçu pour transférer des données entre Hadoop et des bases de données relationnelles.</span><span class="sxs-lookup"><span data-stu-id="14950-249">Sqoop is a tool designed to transfer data between Hadoop and relational databases.</span></span> <span data-ttu-id="14950-250">Vous pouvez l’utiliser pour importer des données depuis un système de gestion de base de données relationnelle (SGBDR) tel que SQ Server, MySQL ou Oracle dans un système de fichiers distribués Hadoop (HDFS), transformer des données dans Hadoop avec MapReduce ou Hive et exporter à nouveau les données dans un SGBDR.</span><span class="sxs-lookup"><span data-stu-id="14950-250">You can use it to import data from a relational database management system (RDBMS), such as SQL Server, MySQL, or Oracle into the Hadoop distributed file system (HDFS), transform the data in Hadoop with MapReduce or Hive, and then export the data back into an RDBMS.</span></span>

<span data-ttu-id="14950-251">Pour plus d’informations, consultez [Utilisation de Sqoop avec HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="14950-251">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

## <a name="development-sdks"></a><span data-ttu-id="14950-252">Kits de développement logiciel (SDK) de développement</span><span class="sxs-lookup"><span data-stu-id="14950-252">Development SDKs</span></span>
<span data-ttu-id="14950-253">Le stockage d'objets blob Azure est également accessible à l'aide d'un kit de développement logiciel (SDK) Azure dans les langages de programmation suivants :</span><span class="sxs-lookup"><span data-stu-id="14950-253">Azure Blob storage can also be accessed using an Azure SDK from the following programming languages:</span></span>

* <span data-ttu-id="14950-254">.NET</span><span class="sxs-lookup"><span data-stu-id="14950-254">.NET</span></span>
* <span data-ttu-id="14950-255">Java</span><span class="sxs-lookup"><span data-stu-id="14950-255">Java</span></span>
* <span data-ttu-id="14950-256">Node.js</span><span class="sxs-lookup"><span data-stu-id="14950-256">Node.js</span></span>
* <span data-ttu-id="14950-257">PHP</span><span class="sxs-lookup"><span data-stu-id="14950-257">PHP</span></span>
* <span data-ttu-id="14950-258">Python</span><span class="sxs-lookup"><span data-stu-id="14950-258">Python</span></span>
* <span data-ttu-id="14950-259">Ruby</span><span class="sxs-lookup"><span data-stu-id="14950-259">Ruby</span></span>

<span data-ttu-id="14950-260">Pour plus d'informations sur l'installation des kits de développement logiciel (SDK) Azure, consultez [Téléchargements Azure](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="14950-260">For more information on installing the Azure SDKs, see [Azure downloads](https://azure.microsoft.com/downloads/)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="14950-261">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="14950-261">Troubleshooting</span></span>
### <span data-ttu-id="14950-262"><a id="storageexception"></a>Exception de stockage pour l’écriture sur un objet blob</span><span class="sxs-lookup"><span data-stu-id="14950-262"><a id="storageexception"></a>Storage exception for write on blob</span></span>
<span data-ttu-id="14950-263">**Symptômes** : lorsque vous utilisez la commande `hadoop` ou `hdfs dfs` pour écrire des fichiers supérieurs à ~12 Go sur un cluster HBase, vous pouvez rencontrer l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="14950-263">**Symptoms**: When using the `hadoop` or `hdfs dfs` commands to write files that are ~12GB or larger on an HBase cluster, you may encounter the following error:</span></span>

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
    Caused by: com.microsoft.azure.storage.StorageException: The request body is too large and exceeds the maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

<span data-ttu-id="14950-264">**Cause** : les clusters HBase sur HDInsight ont par défaut une taille de bloc de 256 Ko lors de l’écriture dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="14950-264">**Cause**: HBase on HDInsight clusters default to a block size of 256KB when writing to Azure storage.</span></span> <span data-ttu-id="14950-265">Bien que cela fonctionne pour les API HBase ou les API REST, cela génère une erreur lorsque vous utilisez les utilitaires de ligne de commande `hadoop` ou `hdfs dfs`.</span><span class="sxs-lookup"><span data-stu-id="14950-265">While this works for HBase APIs or REST APIs, it will result in an error when using the `hadoop` or `hdfs dfs` command-line utilities.</span></span>

<span data-ttu-id="14950-266">**Résolution** : utilisez `fs.azure.write.request.size` pour spécifier une plus grande taille de bloc.</span><span class="sxs-lookup"><span data-stu-id="14950-266">**Resolution**: Use `fs.azure.write.request.size` to specify a larger block size.</span></span> <span data-ttu-id="14950-267">Vous pouvez le faire sur une base par utilisation à l’aide du paramètre `-D`.</span><span class="sxs-lookup"><span data-stu-id="14950-267">You can do this on a per-use basis by using the `-D` parameter.</span></span> <span data-ttu-id="14950-268">Voici un exemple d’utilisation de ce paramètre avec la commande `hadoop` :</span><span class="sxs-lookup"><span data-stu-id="14950-268">The following is an example using this parameter with the `hadoop` command:</span></span>

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

<span data-ttu-id="14950-269">Vous pouvez également augmenter la valeur de `fs.azure.write.request.size` globalement à l’aide d’Ambari.</span><span class="sxs-lookup"><span data-stu-id="14950-269">You can also increase the value of `fs.azure.write.request.size` globally by using Ambari.</span></span> <span data-ttu-id="14950-270">Vous pouvez utiliser les étapes suivantes pour modifier la valeur dans l’interface utilisateur Web d’Ambari :</span><span class="sxs-lookup"><span data-stu-id="14950-270">The following steps can be used to change the value in the Ambari Web UI:</span></span>

1. <span data-ttu-id="14950-271">Dans votre navigateur, accédez à l’interface utilisateur Web d’Ambari pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="14950-271">In your browser, go to the Ambari Web UI for your cluster.</span></span> <span data-ttu-id="14950-272">L’URL est https://CLUSTERNAME.azurehdinsight.net, où **CLUSTERNAME** est le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="14950-272">This is https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your cluster.</span></span>

    <span data-ttu-id="14950-273">Lorsque vous y êtes invité, entrez le nom et le mot de passe administrateur correspondant au cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="14950-273">When prompted, enter the admin name and password for the cluster.</span></span>
2. <span data-ttu-id="14950-274">Sur le côté gauche de l’écran, sélectionnez **HDFS**, puis l’onglet **Configurations**.</span><span class="sxs-lookup"><span data-stu-id="14950-274">From the left side of the screen, select **HDFS**, and then select the **Configs** tab.</span></span>
3. <span data-ttu-id="14950-275">Dans le champ **Filtrer...**, entrez `fs.azure.write.request.size`.</span><span class="sxs-lookup"><span data-stu-id="14950-275">In the **Filter...** field, enter `fs.azure.write.request.size`.</span></span> <span data-ttu-id="14950-276">Le champ et la valeur actuelle s’affichent au milieu de la page.</span><span class="sxs-lookup"><span data-stu-id="14950-276">This will display the field and current value in the middle of the page.</span></span>
4. <span data-ttu-id="14950-277">Modifiez la valeur 262144 (256 Ko) sur la nouvelle valeur.</span><span class="sxs-lookup"><span data-stu-id="14950-277">Change the value from 262144 (256KB) to the new value.</span></span> <span data-ttu-id="14950-278">Par exemple, 4194304 (4 Mo).</span><span class="sxs-lookup"><span data-stu-id="14950-278">For example, 4194304 (4MB).</span></span>

![Image de la modification de la valeur via l’interface utilisateur Web d’Ambari](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

<span data-ttu-id="14950-280">Pour plus d’informations sur l’utilisation d’Ambari, voir [Gestion des clusters HDInsight à l’aide de l’interface utilisateur Web d’Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="14950-280">For more information on using Ambari, see [Manage HDInsight clusters using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="14950-281">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="14950-281">Next steps</span></span>
<span data-ttu-id="14950-282">Maintenant que vous savez comment obtenir des données avec HDInsight, consultez les articles suivants pour apprendre à effectuer des analyses :</span><span class="sxs-lookup"><span data-stu-id="14950-282">Now that you understand how to get data into HDInsight, read the following articles to learn how to perform analysis:</span></span>

* <span data-ttu-id="14950-283">[Prise en main d’Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="14950-283">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="14950-284">[Envoi de tâches Hadoop par programme][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="14950-284">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="14950-285">[Utilisation de Hive avec HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="14950-285">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="14950-286">[Utilisation de Pig avec HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="14950-286">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>

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
