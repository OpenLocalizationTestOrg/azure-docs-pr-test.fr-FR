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
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a><span data-ttu-id="1758a-104">Téléchargement de données pour les tâches Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="1758a-104">Upload data for Hadoop jobs in HDInsight</span></span>
<span data-ttu-id="1758a-105">Azure HDInsight fournit un système HDFS (Hadoo Distributed File System) complet pour le stockage d'objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="1758a-105">Azure HDInsight provides a full-featured Hadoop distributed file system (HDFS) over Azure Blob storage.</span></span> <span data-ttu-id="1758a-106">Il est conçu comme un tooprovide d’extension HDFS soudure expérience toocustomers.</span><span class="sxs-lookup"><span data-stu-id="1758a-106">It is designed as an HDFS extension tooprovide a seamless experience toocustomers.</span></span> <span data-ttu-id="1758a-107">Il permet d’ensemble complète de hello de composants dans hello Hadoop écosystème toooperate directement sur les données hello qu’il gère.</span><span class="sxs-lookup"><span data-stu-id="1758a-107">It enables hello full set of components in hello Hadoop ecosystem toooperate directly on hello data it manages.</span></span> <span data-ttu-id="1758a-108">Le stockage d'objets blob Azure et HDFS sont des systèmes de fichiers distincts qui sont optimisés pour le stockage de données et pour les calculs réalisés à partir de ces données.</span><span class="sxs-lookup"><span data-stu-id="1758a-108">Azure Blob storage and HDFS are distinct file systems that are optimized for storage of data and computations on that data.</span></span> <span data-ttu-id="1758a-109">Pour plus d’informations sur les avantages de hello d’utiliser le stockage d’objets Blob Azure, consultez [le stockage Blob de Azure utilisation hdinsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="1758a-109">For information about hello benefits of using Azure Blob storage, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="1758a-110">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="1758a-110">**Prerequisites**</span></span>

<span data-ttu-id="1758a-111">Notez hello suivant demande avant de commencer :</span><span class="sxs-lookup"><span data-stu-id="1758a-111">Note hello following requirement before you begin:</span></span>

* <span data-ttu-id="1758a-112">Un cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1758a-112">An Azure HDInsight cluster.</span></span> <span data-ttu-id="1758a-113">Pour obtenir des instructions, consultez le didacticiel [Prise en main d’Azure HDInsight][hdinsight-get-started] ou la rubrique [Mise en service de clusters HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="1758a-113">For instructions, see [Get started with Azure HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span>

## <a name="why-blob-storage"></a><span data-ttu-id="1758a-114">Qu'est-ce que le stockage d'objets blob ?</span><span class="sxs-lookup"><span data-stu-id="1758a-114">Why blob storage?</span></span>
<span data-ttu-id="1758a-115">Azure HDInsight clusters sont généralement déployés toorun les tâches MapReduce et les clusters hello sont supprimés une fois que ces travaux terminent.</span><span class="sxs-lookup"><span data-stu-id="1758a-115">Azure HDInsight clusters are typically deployed toorun MapReduce jobs, and hello clusters are dropped after these jobs complete.</span></span> <span data-ttu-id="1758a-116">En conservant les données hello dans des clusters HDFS hello issue des calculs serait un toostore onéreuse ces données.</span><span class="sxs-lookup"><span data-stu-id="1758a-116">Keeping hello data in hello HDFS clusters after computations are complete would be an expensive way toostore this data.</span></span> <span data-ttu-id="1758a-117">Stockage d’objets Blob Azure est une option de stockage économique et pouvant être partagé pour les données qui sont traitée à l’aide de HDInsight de toobe capacité, hautement disponible et évolutive.</span><span class="sxs-lookup"><span data-stu-id="1758a-117">Azure Blob storage is a highly available, highly scalable, high capacity, low cost, and shareable storage option for data that is toobe processed using HDInsight.</span></span> <span data-ttu-id="1758a-118">Le stockage des données dans un objet blob permet de clusters HDInsight hello qui sont utilisés pour toobe calcul libéré en toute sécurité sans perte de données.</span><span class="sxs-lookup"><span data-stu-id="1758a-118">Storing data in a blob enables hello HDInsight clusters that are used for computation toobe safely released without losing data.</span></span>

### <a name="directories"></a><span data-ttu-id="1758a-119">Répertoires</span><span class="sxs-lookup"><span data-stu-id="1758a-119">Directories</span></span>
<span data-ttu-id="1758a-120">Les conteneurs de stockage d'objets blob Azure stockent des données en tant que paires clé/valeur et sans hiérarchie de répertoires.</span><span class="sxs-lookup"><span data-stu-id="1758a-120">Azure Blob storage containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="1758a-121">Toutefois hello « / » caractère peut être utilisé dans toomake de nom de la clé hello il apparaît comme si un fichier est stocké dans une structure de répertoire.</span><span class="sxs-lookup"><span data-stu-id="1758a-121">However hello "/" character can be used within hello key name toomake it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="1758a-122">HDInsight les interprète comme des répertoires réels.</span><span class="sxs-lookup"><span data-stu-id="1758a-122">HDInsight sees these as if they are actual directories.</span></span>

<span data-ttu-id="1758a-123">Par exemple, une clé d'objet blob peut être *input/log1.txt*.</span><span class="sxs-lookup"><span data-stu-id="1758a-123">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="1758a-124">Aucun répertoire « entrée » réel n’existe, mais en raison de la présence de toohello de hello caractère « / » dans le nom de la clé hello, il semble hello un chemin d’accès de fichier.</span><span class="sxs-lookup"><span data-stu-id="1758a-124">No actual "input" directory exists, but due toohello presence of hello "/" character in hello key name, it has hello appearance of a file path.</span></span>

<span data-ttu-id="1758a-125">Pour cette raison, quand vous utilisez les outils d'Azure Explorer, vous pouvez remarquer la présence de fichiers de 0 octet.</span><span class="sxs-lookup"><span data-stu-id="1758a-125">Because of this, if you use Azure Explorer tools you may notice some 0 byte files.</span></span> <span data-ttu-id="1758a-126">Ces fichiers ont deux utilités :</span><span class="sxs-lookup"><span data-stu-id="1758a-126">These files serve two purposes:</span></span>

* <span data-ttu-id="1758a-127">S’il existe les dossiers vides, ils marquent d’existence hello du dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="1758a-127">If there are empty folders, they mark of hello existence of hello folder.</span></span> <span data-ttu-id="1758a-128">Stockage d’objets Blob Azure est assez intelligent tooknow qu’en cas d’un objet blob appelé foo/barre, il existe un dossier appelé **foo**.</span><span class="sxs-lookup"><span data-stu-id="1758a-128">Azure Blob storage is clever enough tooknow that if a blob called foo/bar exists, there is a folder called **foo**.</span></span> <span data-ttu-id="1758a-129">Mais hello toosignify de façon uniquement un dossier vide appelé **foo** est par l’absence de ce fichier spécial de 0 octet.</span><span class="sxs-lookup"><span data-stu-id="1758a-129">But hello only way toosignify an empty folder called **foo** is by having this special 0 byte file in place.</span></span>
* <span data-ttu-id="1758a-130">Elles contiennent des métadonnées spéciale qui sont requis par hello Hadoop système de fichiers, notamment les autorisations hello et des dossiers de hello.</span><span class="sxs-lookup"><span data-stu-id="1758a-130">They hold special metadata that is needed by hello Hadoop file system, notably hello permissions and owners for hello folders.</span></span>

## <a name="command-line-utilities"></a><span data-ttu-id="1758a-131">Utilitaires de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="1758a-131">Command-line utilities</span></span>
<span data-ttu-id="1758a-132">Microsoft fournit hello suivant toowork utilitaires avec le stockage d’objets Blob Azure :</span><span class="sxs-lookup"><span data-stu-id="1758a-132">Microsoft provides hello following utilities toowork with Azure Blob storage:</span></span>

| <span data-ttu-id="1758a-133">Outil</span><span class="sxs-lookup"><span data-stu-id="1758a-133">Tool</span></span> | <span data-ttu-id="1758a-134">Linux</span><span class="sxs-lookup"><span data-stu-id="1758a-134">Linux</span></span> | <span data-ttu-id="1758a-135">OS X</span><span class="sxs-lookup"><span data-stu-id="1758a-135">OS X</span></span> | <span data-ttu-id="1758a-136">Windows</span><span class="sxs-lookup"><span data-stu-id="1758a-136">Windows</span></span> |
| --- |:---:|:---:|:---:|
| <span data-ttu-id="1758a-137">[Interface de ligne de commande Azure][azurecli]</span><span class="sxs-lookup"><span data-stu-id="1758a-137">[Azure Command-Line Interface][azurecli]</span></span> |<span data-ttu-id="1758a-138">✔</span><span class="sxs-lookup"><span data-stu-id="1758a-138">✔</span></span> |<span data-ttu-id="1758a-139">✔</span><span class="sxs-lookup"><span data-stu-id="1758a-139">✔</span></span> |<span data-ttu-id="1758a-140">✔</span><span class="sxs-lookup"><span data-stu-id="1758a-140">✔</span></span> |
| <span data-ttu-id="1758a-141">[Azure PowerShell][azure-powershell]</span><span class="sxs-lookup"><span data-stu-id="1758a-141">[Azure PowerShell][azure-powershell]</span></span> | | |<span data-ttu-id="1758a-142">✔</span><span class="sxs-lookup"><span data-stu-id="1758a-142">✔</span></span> |
| <span data-ttu-id="1758a-143">[AzCopy][azure-azcopy]</span><span class="sxs-lookup"><span data-stu-id="1758a-143">[AzCopy][azure-azcopy]</span></span> | | |<span data-ttu-id="1758a-144">✔</span><span class="sxs-lookup"><span data-stu-id="1758a-144">✔</span></span> |
| [<span data-ttu-id="1758a-145">Commande Hadoop</span><span class="sxs-lookup"><span data-stu-id="1758a-145">Hadoop command</span></span>](#commandline) |<span data-ttu-id="1758a-146">✔</span><span class="sxs-lookup"><span data-stu-id="1758a-146">✔</span></span> |<span data-ttu-id="1758a-147">✔</span><span class="sxs-lookup"><span data-stu-id="1758a-147">✔</span></span> |<span data-ttu-id="1758a-148">✔</span><span class="sxs-lookup"><span data-stu-id="1758a-148">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="1758a-149">Alors que hello CLI d’Azure, Azure PowerShell et AzCopy peuvent toutes être utilisée en dehors d’Azure, hello Hadoop commande est disponible uniquement sur le cluster HDInsight de hello et autorise uniquement le chargement des données à partir du système de fichiers local hello dans le stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="1758a-149">While hello Azure CLI, Azure PowerShell, and AzCopy can all be used from outside Azure, hello Hadoop command is only available on hello HDInsight cluster and only allows loading data from hello local file system into Azure Blob storage.</span></span>
>
>

### <span data-ttu-id="1758a-150"><a id="xplatcli"></a>Interface CLI Azure</span><span class="sxs-lookup"><span data-stu-id="1758a-150"><a id="xplatcli"></a>Azure CLI</span></span>
<span data-ttu-id="1758a-151">Hello CLI d’Azure est un outil inter-plateformes qui vous permet de toomanage Azure services.</span><span class="sxs-lookup"><span data-stu-id="1758a-151">hello Azure CLI is a cross-platform tool that allows you toomanage Azure services.</span></span> <span data-ttu-id="1758a-152">Utilisez hello suivant le stockage d’objets Blob tooAzure étapes tooupload données :</span><span class="sxs-lookup"><span data-stu-id="1758a-152">Use hello following steps tooupload data tooAzure Blob storage:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="1758a-153">[Installer et configurer hello CLI d’Azure pour Mac, Linux et Windows](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="1758a-153">[Install and configure hello Azure CLI for Mac, Linux and Windows](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="1758a-154">Ouvrez une invite de commandes, un interpréteur de commandes ou autres interpréteur de commandes et utilisez hello suivant tooauthenticate tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="1758a-154">Open a command prompt, bash, or other shell, and use hello following tooauthenticate tooyour Azure subscription.</span></span>

        azure login

    <span data-ttu-id="1758a-155">Lorsque vous y êtes invité, entrez le nom d’utilisateur hello et le mot de passe pour votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="1758a-155">When prompted, enter hello user name and password for your subscription.</span></span>
3. <span data-ttu-id="1758a-156">Entrez hello suivant des comptes de stockage commande toolist hello pour votre abonnement :</span><span class="sxs-lookup"><span data-stu-id="1758a-156">Enter hello following command toolist hello storage accounts for your subscription:</span></span>

        azure storage account list
4. <span data-ttu-id="1758a-157">Sélectionner compte de stockage hello qui contient le blob hello souhaité toowork avec, puis utilisez hello commande tooretrieve hello clé pour ce compte suivante :</span><span class="sxs-lookup"><span data-stu-id="1758a-157">Select hello storage account that contains hello blob you want toowork with, then use hello following command tooretrieve hello key for this account:</span></span>

        azure storage account keys list <storage-account-name>

    <span data-ttu-id="1758a-158">Cette commande doit renvoyer les clés **primaires** et **secondaires**.</span><span class="sxs-lookup"><span data-stu-id="1758a-158">This should return **Primary** and **Secondary** keys.</span></span> <span data-ttu-id="1758a-159">Hello de copie **principal** valeur de la clé, car il sera utilisé dans les étapes suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="1758a-159">Copy hello **Primary** key value because it will be used in hello next steps.</span></span>
5. <span data-ttu-id="1758a-160">Utilisez hello suivant commande tooretrieve une liste de conteneurs d’objets blob dans le compte de stockage hello :</span><span class="sxs-lookup"><span data-stu-id="1758a-160">Use hello following command tooretrieve a list of blob containers within hello storage account:</span></span>

        azure storage container list -a <storage-account-name> -k <primary-key>
6. <span data-ttu-id="1758a-161">Utilisez hello suivant tooupload de commandes et télécharger des objets blob toohello de fichiers :</span><span class="sxs-lookup"><span data-stu-id="1758a-161">Use hello following commands tooupload and download files toohello blob:</span></span>

   * <span data-ttu-id="1758a-162">tooupload un fichier :</span><span class="sxs-lookup"><span data-stu-id="1758a-162">tooupload a file:</span></span>

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * <span data-ttu-id="1758a-163">toodownload un fichier :</span><span class="sxs-lookup"><span data-stu-id="1758a-163">toodownload a file:</span></span>

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> <span data-ttu-id="1758a-164">Si vous travaillez toujours avec hello même compte de stockage, vous pouvez définir hello suivant des variables d’environnement au lieu de spécifier le compte de hello et la clé pour chaque commande :</span><span class="sxs-lookup"><span data-stu-id="1758a-164">If you will always be working with hello same storage account, you can set hello following environment variables instead of specifying hello account and key for every command:</span></span>
>
> * <span data-ttu-id="1758a-165">**AZURE\_stockage\_compte**: nom de compte de stockage hello</span><span class="sxs-lookup"><span data-stu-id="1758a-165">**AZURE\_STORAGE\_ACCOUNT**: hello storage account name</span></span>
> * <span data-ttu-id="1758a-166">**AZURE\_stockage\_accès\_clé**: clé de compte de stockage hello</span><span class="sxs-lookup"><span data-stu-id="1758a-166">**AZURE\_STORAGE\_ACCESS\_KEY**: hello storage account key</span></span>
>
>

### <span data-ttu-id="1758a-167"><a id="powershell"></a>Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1758a-167"><a id="powershell"></a>Azure PowerShell</span></span>
<span data-ttu-id="1758a-168">Azure PowerShell est un environnement de script que vous pouvez utiliser toocontrol et automatiser le déploiement de hello et la gestion de vos charges de travail dans Azure.</span><span class="sxs-lookup"><span data-stu-id="1758a-168">Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="1758a-169">Pour plus d’informations sur la configuration de votre station de travail de toorun Azure PowerShell, consultez [installer et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1758a-169">For information about configuring your workstation toorun Azure PowerShell, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="1758a-170">**tooupload un stockage d’objets Blob de tooAzure fichier local**</span><span class="sxs-lookup"><span data-stu-id="1758a-170">**tooupload a local file tooAzure Blob storage**</span></span>

1. <span data-ttu-id="1758a-171">Console d’Azure PowerShell hello ouvert comme indiqué dans [installer et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1758a-171">Open hello Azure PowerShell console as instructed in [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="1758a-172">Définir des cinq premières variables valeurs hello Hello Bonjour script suivant :</span><span class="sxs-lookup"><span data-stu-id="1758a-172">Set hello values of hello first five variables in hello following script:</span></span>

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
3. <span data-ttu-id="1758a-173">Hello de coller dans hello Azure PowerShell console toorun il toocopy hello fichier script.</span><span class="sxs-lookup"><span data-stu-id="1758a-173">Paste hello script into hello Azure PowerShell console toorun it toocopy hello file.</span></span>

<span data-ttu-id="1758a-174">Par exemple toowork de création de scripts PowerShell hdinsight, consultez [outils HDInsight](https://github.com/blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="1758a-174">For example PowerShell scripts created toowork with HDInsight, see [HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span></span>

### <span data-ttu-id="1758a-175"><a id="azcopy"></a>AzCopy</span><span class="sxs-lookup"><span data-stu-id="1758a-175"><a id="azcopy"></a>AzCopy</span></span>
<span data-ttu-id="1758a-176">AzCopy est un outil de ligne de commande qui est conçu de tâche de hello toosimplify de transfert de données dans et hors d’un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="1758a-176">AzCopy is a command-line tool that is designed toosimplify hello task of transferring data into and out of an Azure Storage account.</span></span> <span data-ttu-id="1758a-177">Vous pouvez l'utiliser comme un outil indépendant ou l'incorporer dans une application existante.</span><span class="sxs-lookup"><span data-stu-id="1758a-177">You can use it as a standalone tool or incorporate this tool in an existing application.</span></span> <span data-ttu-id="1758a-178">[Téléchargement d’AzCopy][azure-azcopy-download].</span><span class="sxs-lookup"><span data-stu-id="1758a-178">[Download AzCopy][azure-azcopy-download].</span></span>

<span data-ttu-id="1758a-179">Hello AzCopy syntaxe est la suivante :</span><span class="sxs-lookup"><span data-stu-id="1758a-179">hello AzCopy syntax is:</span></span>

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

<span data-ttu-id="1758a-180">Pour plus d’informations, consultez la page [AzCopy : téléchargement de fichiers pour les objets blob Azure][azure-azcopy].</span><span class="sxs-lookup"><span data-stu-id="1758a-180">For more information, see [AzCopy - Uploading/Downloading files for Azure Blobs][azure-azcopy].</span></span>

### <span data-ttu-id="1758a-181"><a id="commandline"></a>Ligne de commande Hadoop</span><span class="sxs-lookup"><span data-stu-id="1758a-181"><a id="commandline"></a>Hadoop command line</span></span>
<span data-ttu-id="1758a-182">ligne de commande Hadoop Hello est uniquement utile pour le stockage des données dans le stockage d’objets blob lorsque les données de salutation sont déjà présentes sur le nœud principal du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1758a-182">hello Hadoop command line is only useful for storing data into blob storage when hello data is already present on hello cluster head node.</span></span>

<span data-ttu-id="1758a-183">Bonjour toouse de commande Hadoop commande, vous devez d’abord connecter nœud principal toohello en utilisant l’une des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="1758a-183">In order toouse hello Hadoop command, you must first connect toohello headnode using one of hello following methods:</span></span>

* <span data-ttu-id="1758a-184">**HDInsight Windows**: [connexion à l'aide du Bureau à distance](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="1758a-184">**Windows-based HDInsight**: [Connect using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>
* <span data-ttu-id="1758a-185">**HDInsight de basés sur Linux**: se connecter à l’aide de SSH ([hello commande SSH](hdinsight-hadoop-linux-use-ssh-unix.md) ou [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span><span class="sxs-lookup"><span data-stu-id="1758a-185">**Linux-based HDInsight**: Connect using SSH ([hello SSH command](hdinsight-hadoop-linux-use-ssh-unix.md) or [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span></span>

<span data-ttu-id="1758a-186">Une fois connecté, vous pouvez utiliser hello suivant tooupload de syntaxe un toostorage de fichier.</span><span class="sxs-lookup"><span data-stu-id="1758a-186">Once connected, you can use hello following syntax tooupload a file toostorage.</span></span>

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

<span data-ttu-id="1758a-187">Par exemple, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span><span class="sxs-lookup"><span data-stu-id="1758a-187">For example, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span></span>

<span data-ttu-id="1758a-188">Système de fichiers par défaut hello pour HDInsight se trouve dans le stockage Blob Azure, /example/data.txt est réellement dans le stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="1758a-188">Because hello default file system for HDInsight is in Azure Blob storage, /example/data.txt is actually in Azure Blob storage.</span></span> <span data-ttu-id="1758a-189">Vous pouvez également consulter le fichier toohello en tant que :</span><span class="sxs-lookup"><span data-stu-id="1758a-189">You can also refer toohello file as:</span></span>

    wasb:///example/data/data.txt

<span data-ttu-id="1758a-190">ou</span><span class="sxs-lookup"><span data-stu-id="1758a-190">or</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

<span data-ttu-id="1758a-191">Pour obtenir la liste des autres commandes Hadoop qui fonctionnent avec des fichiers, consultez [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span><span class="sxs-lookup"><span data-stu-id="1758a-191">For a list of other Hadoop commands that work with files, see [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span></span>

> [!WARNING]
> <span data-ttu-id="1758a-192">Sur des clusters HBase, taille de bloc hello par défaut utilisé lors de l’écriture de données est de 256 Ko.</span><span class="sxs-lookup"><span data-stu-id="1758a-192">On HBase clusters, hello default block size used when writing data is 256KB.</span></span> <span data-ttu-id="1758a-193">Alors que cela fonctionne bien lorsque vous utilisez HBase APIs ou des API REST, à l’aide de hello `hadoop` ou `hdfs dfs` supérieure à environ 12 Go de données de toowrite commandes génère une erreur.</span><span class="sxs-lookup"><span data-stu-id="1758a-193">While this works fine when using HBase APIs or REST APIs, using hello `hadoop` or `hdfs dfs` commands toowrite data larger than ~12GB results in an error.</span></span> <span data-ttu-id="1758a-194">Consultez hello [exception de stockage pour l’écriture sur l’objet blob](#storageexception) section ci-dessous pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="1758a-194">See hello [storage exception for write on blob](#storageexception) section below for more information.</span></span>
>
>

## <a name="graphical-clients"></a><span data-ttu-id="1758a-195">Clients graphiques</span><span class="sxs-lookup"><span data-stu-id="1758a-195">Graphical clients</span></span>
<span data-ttu-id="1758a-196">Plusieurs applications fournissent également une interface graphique pour utiliser Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="1758a-196">There are also several applications that provide a graphical interface for working with Azure Storage.</span></span> <span data-ttu-id="1758a-197">Hello Voici une liste de quelques-unes de ces applications :</span><span class="sxs-lookup"><span data-stu-id="1758a-197">hello following is a list of a few of these applications:</span></span>

| <span data-ttu-id="1758a-198">Client</span><span class="sxs-lookup"><span data-stu-id="1758a-198">Client</span></span> | <span data-ttu-id="1758a-199">Linux</span><span class="sxs-lookup"><span data-stu-id="1758a-199">Linux</span></span> | <span data-ttu-id="1758a-200">OS X</span><span class="sxs-lookup"><span data-stu-id="1758a-200">OS X</span></span> | <span data-ttu-id="1758a-201">Windows</span><span class="sxs-lookup"><span data-stu-id="1758a-201">Windows</span></span> |
| --- |:---:|:---:|:---:|
| [<span data-ttu-id="1758a-202">Outils Microsoft Visual Studio pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="1758a-202">Microsoft Visual Studio Tools for HDInsight</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |<span data-ttu-id="1758a-203">✔</span><span class="sxs-lookup"><span data-stu-id="1758a-203">✔</span></span> |<span data-ttu-id="1758a-204">✔</span><span class="sxs-lookup"><span data-stu-id="1758a-204">✔</span></span> |<span data-ttu-id="1758a-205">✔</span><span class="sxs-lookup"><span data-stu-id="1758a-205">✔</span></span> |
| [<span data-ttu-id="1758a-206">Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="1758a-206">Azure Storage Explorer</span></span>](http://storageexplorer.com/) |<span data-ttu-id="1758a-207">✔</span><span class="sxs-lookup"><span data-stu-id="1758a-207">✔</span></span> |<span data-ttu-id="1758a-208">✔</span><span class="sxs-lookup"><span data-stu-id="1758a-208">✔</span></span> |<span data-ttu-id="1758a-209">✔</span><span class="sxs-lookup"><span data-stu-id="1758a-209">✔</span></span> |
| [<span data-ttu-id="1758a-210">Cloud Storage Studio 2</span><span class="sxs-lookup"><span data-stu-id="1758a-210">Cloud Storage Studio 2</span></span>](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |<span data-ttu-id="1758a-211">✔</span><span class="sxs-lookup"><span data-stu-id="1758a-211">✔</span></span> |
| [<span data-ttu-id="1758a-212">CloudXplorer</span><span class="sxs-lookup"><span data-stu-id="1758a-212">CloudXplorer</span></span>](http://clumsyleaf.com/products/cloudxplorer) | | |<span data-ttu-id="1758a-213">✔</span><span class="sxs-lookup"><span data-stu-id="1758a-213">✔</span></span> |
| [<span data-ttu-id="1758a-214">Azure Explorer</span><span class="sxs-lookup"><span data-stu-id="1758a-214">Azure Explorer</span></span>](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |<span data-ttu-id="1758a-215">✔</span><span class="sxs-lookup"><span data-stu-id="1758a-215">✔</span></span> |
| [<span data-ttu-id="1758a-216">Cyberduck</span><span class="sxs-lookup"><span data-stu-id="1758a-216">Cyberduck</span></span>](https://cyberduck.io/) | |<span data-ttu-id="1758a-217">✔</span><span class="sxs-lookup"><span data-stu-id="1758a-217">✔</span></span> |<span data-ttu-id="1758a-218">✔</span><span class="sxs-lookup"><span data-stu-id="1758a-218">✔</span></span> |

### <a name="visual-studio-tools-for-hdinsight"></a><span data-ttu-id="1758a-219">Outils Visual Studio pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="1758a-219">Visual Studio Tools for HDInsight</span></span>
<span data-ttu-id="1758a-220">Pour plus d’informations, consultez [naviguer hello de ressources liées](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span><span class="sxs-lookup"><span data-stu-id="1758a-220">For more information, see [Navigate hello linked resources](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span></span>

### <span data-ttu-id="1758a-221"><a id="storageexplorer"></a>Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="1758a-221"><a id="storageexplorer"></a>Azure Storage Explorer</span></span>
<span data-ttu-id="1758a-222">*Explorateur de stockage Azure* est un outil utile pour examiner et modifier les données de salutation dans des objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="1758a-222">*Azure Storage Explorer* is a useful tool for inspecting and altering hello data in blobs.</span></span> <span data-ttu-id="1758a-223">Il s’agit d’un outil gratuit que vous pouvez télécharger depuis la page [http://storageexplorer.com/](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="1758a-223">It is a free, open source tool that can be downloaded from [http://storageexplorer.com/](http://storageexplorer.com/).</span></span> <span data-ttu-id="1758a-224">code source de Hello est disponible à partir de ce lien également.</span><span class="sxs-lookup"><span data-stu-id="1758a-224">hello source code is available from this link as well.</span></span>

<span data-ttu-id="1758a-225">Avant d’utiliser l’outil de hello, vous devez connaître votre clé et le nom du compte stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="1758a-225">Before using hello tool, you must know your Azure storage account name and account key.</span></span> <span data-ttu-id="1758a-226">Pour obtenir des instructions sur l’obtention de ces informations, consultez hello « Comment : afficher, copier et régénérer stockage clés d’accès « section de [créer, gérer ou supprimer un compte de stockage][azure-create-storage-account].</span><span class="sxs-lookup"><span data-stu-id="1758a-226">For instructions about getting this information, see hello "How to: View, copy and regenerate storage access keys" section of [Create, manage, or delete a storage account][azure-create-storage-account].</span></span>

1. <span data-ttu-id="1758a-227">Exécutez Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="1758a-227">Run Azure Storage Explorer.</span></span> <span data-ttu-id="1758a-228">S’il s’agit hello première fois que vous avez exécuté hello Explorateur de stockage, vous demandera hello **nom du compte de _stockage** et **clé de compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="1758a-228">If this is hello first time you have run hello Storage Explorer, you will be prompted for hello **_Storage account name** and **Storage account key**.</span></span> <span data-ttu-id="1758a-229">Si vous avez exécuté avant, utilisez hello **ajouter** bouton tooadd un nouveau nom de compte de stockage et la clé.</span><span class="sxs-lookup"><span data-stu-id="1758a-229">If you have run it before, use hello **Add** button tooadd a new storage account name and key.</span></span>

    <span data-ttu-id="1758a-230">Entrez hello nom et clé hello compte de stockage utilisé par votre cluster HDInsight, puis sélectionnez **Enregistrer & Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="1758a-230">Enter hello name and key for hello storage account used by your HDInsight cluster and then select **SAVE & OPEN**.</span></span>

    ![HDI.AzureStorageExplorer][image-azure-storage-explorer]
2. <span data-ttu-id="1758a-232">Dans la liste hello de gauche de toohello de conteneurs de l’interface de hello, cliquez sur nom hello conteneur hello qui est associé à votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1758a-232">In hello list of containers toohello left of hello interface, click hello name of hello container that is associated with your HDInsight cluster.</span></span> <span data-ttu-id="1758a-233">Par défaut, ce nom hello du cluster HDInsight de hello, mais peut être différent si vous avez entré un nom spécifique lors de la création du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="1758a-233">By default, this is hello name of hello HDInsight cluster, but may be different if you entered a specific name when creating hello cluster.</span></span>
3. <span data-ttu-id="1758a-234">À partir de la barre d’outils hello, sélectionnez l’icône de téléchargement hello.</span><span class="sxs-lookup"><span data-stu-id="1758a-234">From hello tool bar, select hello upload icon.</span></span>

    ![Barre d’outils avec icône téléchargement mise en surbrillance](./media/hdinsight-upload-data/toolbar.png)
4. <span data-ttu-id="1758a-236">Spécifiez un tooupload de fichier, puis cliquez sur **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="1758a-236">Specify a file tooupload, and then click **Open**.</span></span> <span data-ttu-id="1758a-237">Lorsque vous y êtes invité, sélectionnez **télécharger** racine de toohello tooupload hello fichier hello du conteneur de stockage.</span><span class="sxs-lookup"><span data-stu-id="1758a-237">When prompted, select **Upload** tooupload hello file toohello root of hello storage container.</span></span> <span data-ttu-id="1758a-238">Si vous souhaitez tooupload hello fichier tooa chemin d’accès spécifique, entrez le chemin d’accès hello dans hello **Destination** champ, puis sélectionnez **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="1758a-238">If you want tooupload hello file tooa specific path, enter hello path in hello **Destination** field and then select **Upload**.</span></span>

    ![Boîte de dialogue de téléchargement de fichier](./media/hdinsight-upload-data/fileupload.png)

    <span data-ttu-id="1758a-240">Une fois le téléchargement du fichier hello a terminé, vous pouvez l’utiliser à partir des travaux sur le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="1758a-240">Once hello file has finished uploading, you can use it from jobs on hello HDInsight cluster.</span></span>

## <a name="mount-azure-blob-storage-as-local-drive"></a><span data-ttu-id="1758a-241">Monter le stockage d'objets Blob Azure comme un lecteur Local</span><span class="sxs-lookup"><span data-stu-id="1758a-241">Mount Azure Blob Storage as Local Drive</span></span>
<span data-ttu-id="1758a-242">Consultez [Monter un objet Blob Azure en tant que lecteur Local](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span><span class="sxs-lookup"><span data-stu-id="1758a-242">See [Mount Azure Blob Storage as Local Drive](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span></span>

## <a name="services"></a><span data-ttu-id="1758a-243">Services</span><span class="sxs-lookup"><span data-stu-id="1758a-243">Services</span></span>
### <a name="azure-data-factory"></a><span data-ttu-id="1758a-244">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1758a-244">Azure Data Factory</span></span>
<span data-ttu-id="1758a-245">Hello service Azure Data Factory est un service entièrement géré pour composer des services de déplacement de données de stockage et le traitement des données de données dans des pipelines de production de données simplifiée, évolutive et fiable.</span><span class="sxs-lookup"><span data-stu-id="1758a-245">hello Azure Data Factory service is a fully managed service for composing data storage, data processing, and data movement services into streamlined, scalable, and reliable data production pipelines.</span></span>

<span data-ttu-id="1758a-246">Azure Data Factory peut être utilisé toomove des données dans le stockage d’objets Blob Azure, ou toocreate des pipelines de données qui utilisent directement HDInsight fonctionnalités telles que la ruche et porc.</span><span class="sxs-lookup"><span data-stu-id="1758a-246">Azure Data Factory can be used toomove data into Azure Blob storage, or toocreate data pipelines that directly use HDInsight features such as Hive and Pig.</span></span>

<span data-ttu-id="1758a-247">Pour plus d’informations, consultez hello [documentation d’Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="1758a-247">For more information, see hello [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/).</span></span>

### <span data-ttu-id="1758a-248"><a id="sqoop"></a>Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="1758a-248"><a id="sqoop"></a>Apache Sqoop</span></span>
<span data-ttu-id="1758a-249">Sqoop est un outil conçu de données tootransfer entre Hadoop et des bases de données relationnelles.</span><span class="sxs-lookup"><span data-stu-id="1758a-249">Sqoop is a tool designed tootransfer data between Hadoop and relational databases.</span></span> <span data-ttu-id="1758a-250">Vous pouvez l’utiliser tooimport des données à partir d’un système de gestion de base de données relationnelle (SGBDR), telles que SQL Server, MySQL ou Oracle dans le système de fichiers DFS Hadoop hello (HDFS), transformer des données dans Hadoop MapReduce ou ruche hello et puis exporter les données hello dans un SGBDR.</span><span class="sxs-lookup"><span data-stu-id="1758a-250">You can use it tooimport data from a relational database management system (RDBMS), such as SQL Server, MySQL, or Oracle into hello Hadoop distributed file system (HDFS), transform hello data in Hadoop with MapReduce or Hive, and then export hello data back into an RDBMS.</span></span>

<span data-ttu-id="1758a-251">Pour plus d’informations, consultez [Utilisation de Sqoop avec HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="1758a-251">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

## <a name="development-sdks"></a><span data-ttu-id="1758a-252">Kits de développement logiciel (SDK) de développement</span><span class="sxs-lookup"><span data-stu-id="1758a-252">Development SDKs</span></span>
<span data-ttu-id="1758a-253">Stockage d’objets Blob Azure également accessibles à l’aide d’un kit de développement Azure à partir de hello suivant des langages de programmation :</span><span class="sxs-lookup"><span data-stu-id="1758a-253">Azure Blob storage can also be accessed using an Azure SDK from hello following programming languages:</span></span>

* <span data-ttu-id="1758a-254">.NET</span><span class="sxs-lookup"><span data-stu-id="1758a-254">.NET</span></span>
* <span data-ttu-id="1758a-255">Java</span><span class="sxs-lookup"><span data-stu-id="1758a-255">Java</span></span>
* <span data-ttu-id="1758a-256">Node.js</span><span class="sxs-lookup"><span data-stu-id="1758a-256">Node.js</span></span>
* <span data-ttu-id="1758a-257">PHP</span><span class="sxs-lookup"><span data-stu-id="1758a-257">PHP</span></span>
* <span data-ttu-id="1758a-258">Python</span><span class="sxs-lookup"><span data-stu-id="1758a-258">Python</span></span>
* <span data-ttu-id="1758a-259">Ruby</span><span class="sxs-lookup"><span data-stu-id="1758a-259">Ruby</span></span>

<span data-ttu-id="1758a-260">Pour plus d’informations sur l’installation Bonjour Azure SDK, consultez [téléchargements Azure](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="1758a-260">For more information on installing hello Azure SDKs, see [Azure downloads](https://azure.microsoft.com/downloads/)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1758a-261">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="1758a-261">Troubleshooting</span></span>
### <span data-ttu-id="1758a-262"><a id="storageexception"></a>Exception de stockage pour l’écriture sur un objet blob</span><span class="sxs-lookup"><span data-stu-id="1758a-262"><a id="storageexception"></a>Storage exception for write on blob</span></span>
<span data-ttu-id="1758a-263">**Symptômes**: lors de l’utilisation de hello `hadoop` ou `hdfs dfs` toowrite des fichiers de commandes sont environ 12 Go ou plus sur un cluster HBase, vous pouvez rencontrer hello l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="1758a-263">**Symptoms**: When using hello `hadoop` or `hdfs dfs` commands toowrite files that are ~12GB or larger on an HBase cluster, you may encounter hello following error:</span></span>

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

<span data-ttu-id="1758a-264">**Cause**: taille de bloc tooa par défaut de 256 Ko des clusters HBase sur HDInsight lors de l’écriture de tooAzure stockage.</span><span class="sxs-lookup"><span data-stu-id="1758a-264">**Cause**: HBase on HDInsight clusters default tooa block size of 256KB when writing tooAzure storage.</span></span> <span data-ttu-id="1758a-265">Bien que cela fonctionne pour HBase APIs ou des API REST, il entraîne une erreur lors de l’utilisation de hello `hadoop` ou `hdfs dfs` des utilitaires de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="1758a-265">While this works for HBase APIs or REST APIs, it will result in an error when using hello `hadoop` or `hdfs dfs` command-line utilities.</span></span>

<span data-ttu-id="1758a-266">**Résolution**: utilisez `fs.azure.write.request.size` toospecify une plus grande taille de bloc.</span><span class="sxs-lookup"><span data-stu-id="1758a-266">**Resolution**: Use `fs.azure.write.request.size` toospecify a larger block size.</span></span> <span data-ttu-id="1758a-267">Cela à l’aide de hello sur une base individuelle `-D` paramètre.</span><span class="sxs-lookup"><span data-stu-id="1758a-267">You can do this on a per-use basis by using hello `-D` parameter.</span></span> <span data-ttu-id="1758a-268">Hello Voici un exemple d’utilisation de ce paramètre avec hello `hadoop` commande :</span><span class="sxs-lookup"><span data-stu-id="1758a-268">hello following is an example using this parameter with hello `hadoop` command:</span></span>

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

<span data-ttu-id="1758a-269">Vous pouvez également augmenter la valeur hello `fs.azure.write.request.size` globalement à l’aide de Ambari.</span><span class="sxs-lookup"><span data-stu-id="1758a-269">You can also increase hello value of `fs.azure.write.request.size` globally by using Ambari.</span></span> <span data-ttu-id="1758a-270">Hello suit peut être utilisé la valeur de hello de toochange Bonjour l’interface utilisateur de Ambari Web :</span><span class="sxs-lookup"><span data-stu-id="1758a-270">hello following steps can be used toochange hello value in hello Ambari Web UI:</span></span>

1. <span data-ttu-id="1758a-271">Dans votre navigateur, accédez à toohello l’interface utilisateur de Ambari Web pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="1758a-271">In your browser, go toohello Ambari Web UI for your cluster.</span></span> <span data-ttu-id="1758a-272">Il s’agit de https://CLUSTERNAME.azurehdinsight.net, où **CLUSTERNAME** est le nom hello de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="1758a-272">This is https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your cluster.</span></span>

    <span data-ttu-id="1758a-273">Lorsque vous y êtes invité, entrez le nom de l’administrateur hello et le mot de passe pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="1758a-273">When prompted, enter hello admin name and password for hello cluster.</span></span>
2. <span data-ttu-id="1758a-274">Bonjour à gauche de l’écran hello, sélectionnez **HDFS**, puis sélectionnez hello **configurations** onglet.</span><span class="sxs-lookup"><span data-stu-id="1758a-274">From hello left side of hello screen, select **HDFS**, and then select hello **Configs** tab.</span></span>
3. <span data-ttu-id="1758a-275">Bonjour **filtre...**  , saisissez `fs.azure.write.request.size`.</span><span class="sxs-lookup"><span data-stu-id="1758a-275">In hello **Filter...** field, enter `fs.azure.write.request.size`.</span></span> <span data-ttu-id="1758a-276">Champ de hello et la valeur actuelle s’affiche au milieu de hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="1758a-276">This will display hello field and current value in hello middle of hello page.</span></span>
4. <span data-ttu-id="1758a-277">Remplacez hello 262144 (256 Ko) toohello nouvelle valeur par.</span><span class="sxs-lookup"><span data-stu-id="1758a-277">Change hello value from 262144 (256KB) toohello new value.</span></span> <span data-ttu-id="1758a-278">Par exemple, 4194304 (4 Mo).</span><span class="sxs-lookup"><span data-stu-id="1758a-278">For example, 4194304 (4MB).</span></span>

![Image de la modification de valeur hello via l’interface utilisateur de Ambari Web](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

<span data-ttu-id="1758a-280">Pour plus d’informations sur l’utilisation de Ambari, consultez [gérer les clusters HDInsight à l’aide de hello l’interface utilisateur de Ambari Web](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="1758a-280">For more information on using Ambari, see [Manage HDInsight clusters using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1758a-281">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1758a-281">Next steps</span></span>
<span data-ttu-id="1758a-282">Maintenant que vous comprenez comment lire les données de tooget dans HDInsight, hello suivant articles toolearn comment tooperform analyse :</span><span class="sxs-lookup"><span data-stu-id="1758a-282">Now that you understand how tooget data into HDInsight, read hello following articles toolearn how tooperform analysis:</span></span>

* <span data-ttu-id="1758a-283">[Prise en main d’Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="1758a-283">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="1758a-284">[Envoi de tâches Hadoop par programme][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="1758a-284">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="1758a-285">[Utilisation de Hive avec HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="1758a-285">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="1758a-286">[Utilisation de Pig avec HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="1758a-286">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>

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
