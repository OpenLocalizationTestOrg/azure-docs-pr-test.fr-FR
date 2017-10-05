---
title: "Copie ou déplacement des données vers le stockage Azure avec AzCopy sur Windows | Microsoft Docs"
description: "Utilisez l’utilitaire AzCopy sur Windows pour déplacer ou copier des données vers ou à partir de contenu de blob, de table et de fichier. Copiez des données vers Azure Storage à partir de fichiers locaux ou copiez des données dans ou entre des comptes de stockage. Migrez facilement vos données vers Azure Storage."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: aa155738-7c69-4a83-94f8-b97af4461274
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/14/2017
ms.author: seguler
ms.openlocfilehash: 045778822022752295bb634bdf734daaf36ab938
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="transfer-data-with-the-azcopy-on-windows"></a><span data-ttu-id="47684-105">Transférer des données avec AzCopy sur Windows</span><span class="sxs-lookup"><span data-stu-id="47684-105">Transfer data with the AzCopy on Windows</span></span>
<span data-ttu-id="47684-106">AzCopy est un utilitaire en ligne de commande conçu pour copier des données depuis et vers un stockage de fichier, de table et de blob Microsoft Azure en utilisant des commandes simples avec des performances optimales.</span><span class="sxs-lookup"><span data-stu-id="47684-106">AzCopy is a command-line utility designed for copying data to and from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="47684-107">Vous pouvez copier des données d’un objet vers un autre au sein de votre compte de stockage ou entre des comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="47684-107">You can copy data from one object to another within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="47684-108">Il existe deux versions d’AzCopy que vous pouvez télécharger.</span><span class="sxs-lookup"><span data-stu-id="47684-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="47684-109">AzCopy sur Windows est intégré à .NET Framework et offre des options en ligne de commande de style Windows.</span><span class="sxs-lookup"><span data-stu-id="47684-109">AzCopy on Windows is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="47684-110">[AzCopy sur Linux](storage-use-azcopy-linux.md) est intégré à .NET Core Framework, qui cible les plateformes Linux en offrant des options en ligne de commande de style POSIX.</span><span class="sxs-lookup"><span data-stu-id="47684-110">[AzCopy on Linux](storage-use-azcopy-linux.md) is built with .NET Core Framework which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="47684-111">Cet article est consacré à AzCopy sur Windows.</span><span class="sxs-lookup"><span data-stu-id="47684-111">This article covers AzCopy on Windows.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="47684-112">Téléchargement et installation d’AzCopy</span><span class="sxs-lookup"><span data-stu-id="47684-112">Download and install AzCopy</span></span>
### <a name="azcopy-on-windows"></a><span data-ttu-id="47684-113">AzCopy sur Windows</span><span class="sxs-lookup"><span data-stu-id="47684-113">AzCopy on Windows</span></span>
<span data-ttu-id="47684-114">Téléchargez la [dernière version d’AzCopy sur Windows](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="47684-114">Download the [latest version of AzCopy on Windows](http://aka.ms/downloadazcopy).</span></span>

#### <a name="installation-on-windows"></a><span data-ttu-id="47684-115">Installation sur Windows</span><span class="sxs-lookup"><span data-stu-id="47684-115">Installation on Windows</span></span>
<span data-ttu-id="47684-116">Après avoir installé AzCopy sur Windows via le programme d’installation, ouvrez une fenêtre de commande, puis naviguez jusqu’au répertoire d’installation d’AzCopy sur votre ordinateur, où se trouve l’exécutable `AzCopy.exe`.</span><span class="sxs-lookup"><span data-stu-id="47684-116">After installing AzCopy on Windows using the installer, open a command window and navigate to the AzCopy installation directory on your computer - where the `AzCopy.exe` executable is located.</span></span> <span data-ttu-id="47684-117">Si vous le souhaitez, vous pouvez ajouter l’emplacement d’installation d’AzCopy au chemin de votre système.</span><span class="sxs-lookup"><span data-stu-id="47684-117">If desired, you can add the AzCopy installation location to your system path.</span></span> <span data-ttu-id="47684-118">Par défaut, AzCopy est installé dans `%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` ou `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="47684-118">By default, AzCopy is installed to `%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` or `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span></span>

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="47684-119">Écriture de votre première commande AzCopy</span><span class="sxs-lookup"><span data-stu-id="47684-119">Writing your first AzCopy command</span></span>
<span data-ttu-id="47684-120">La syntaxe de base d’une commande AzCopy est :</span><span class="sxs-lookup"><span data-stu-id="47684-120">The basic syntax for AzCopy commands is:</span></span>

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

<span data-ttu-id="47684-121">Les exemples suivants montrent différents scénarios permettant de copier des données vers et à partir d’objets blob Microsoft Azure, les fichiers et les tables.</span><span class="sxs-lookup"><span data-stu-id="47684-121">The following examples demonstrate a variety of scenarios for copying data to and from Microsoft Azure Blobs, Files, and Tables.</span></span> <span data-ttu-id="47684-122">Reportez-vous à la section [Paramètres AzCopy](#azcopy-parameters) pour obtenir une explication détaillée des paramètres utilisés dans chaque échantillon.</span><span class="sxs-lookup"><span data-stu-id="47684-122">Refer to the [AzCopy Parameters](#azcopy-parameters) section for a detailed explanation of the parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="47684-123">Blob : Téléchargement</span><span class="sxs-lookup"><span data-stu-id="47684-123">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="47684-124">Télécharger un seul objet blob</span><span class="sxs-lookup"><span data-stu-id="47684-124">Download single blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="47684-125">Remarque : si le dossier `C:\myfolder` n’existe pas encore, AzCopy le crée dans le système de fichiers et télécharge `abc.txt ` dans le nouveau dossier.</span><span class="sxs-lookup"><span data-stu-id="47684-125">Note that if the folder `C:\myfolder` does not exist, AzCopy will create it and download `abc.txt ` into the new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="47684-126">Télécharger un objet blob unique depuis la région secondaire</span><span class="sxs-lookup"><span data-stu-id="47684-126">Download single blob from secondary region</span></span>

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="47684-127">Notez que vous devez avoir un accès en lecture activé pour le stockage géo-redondant.</span><span class="sxs-lookup"><span data-stu-id="47684-127">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="47684-128">Télécharger tous les objets blob</span><span class="sxs-lookup"><span data-stu-id="47684-128">Download all blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="47684-129">Si les objets blob suivants se trouvent dans le conteneur spécifié :</span><span class="sxs-lookup"><span data-stu-id="47684-129">Assume the following blobs reside in the specified container:</span></span>  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="47684-130">Après l’opération de téléchargement, le répertoire `C:\myfolder` inclut les fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="47684-130">After the download operation, the directory `C:\myfolder` will include the following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

<span data-ttu-id="47684-131">Si vous ne spécifiez pas l’option `/S`, aucun objet blob n’est téléchargé.</span><span class="sxs-lookup"><span data-stu-id="47684-131">If you do not specify option `/S`, no blobs will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="47684-132">Téléchargement d’objets blob avec le préfixe spécifié</span><span class="sxs-lookup"><span data-stu-id="47684-132">Download blobs with specified prefix</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

<span data-ttu-id="47684-133">Si les objets blob suivants se trouvent dans le conteneur spécifié,</span><span class="sxs-lookup"><span data-stu-id="47684-133">Assume the following blobs reside in the specified container.</span></span> <span data-ttu-id="47684-134">Tous les objets blob commençant par le préfixe `a` sont téléchargés :</span><span class="sxs-lookup"><span data-stu-id="47684-134">All blobs beginning with the prefix `a` will be downloaded:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="47684-135">Après l’opération de téléchargement, le dossier `C:\myfolder` inclut les fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="47684-135">After the download operation, the folder `C:\myfolder` will include the following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

<span data-ttu-id="47684-136">Le préfixe s’applique au répertoire virtuel, qui forme la première partie du nom de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="47684-136">The prefix applies to the virtual directory, which forms the first part of the blob name.</span></span> <span data-ttu-id="47684-137">Dans l’exemple ci-dessus, le répertoire virtuel ne correspond pas au préfixe spécifié ; il n’est donc pas téléchargé.</span><span class="sxs-lookup"><span data-stu-id="47684-137">In the example shown above, the virtual directory does not match the specified prefix, so it is not downloaded.</span></span> <span data-ttu-id="47684-138">En outre, si l’option `\S` n’est pas spécifiée, AzCopy ne télécharge pas les objets blob.</span><span class="sxs-lookup"><span data-stu-id="47684-138">In addition, if the option `\S` is not specified, AzCopy will not download any blobs.</span></span>

### <a name="set-the-last-modified-time-of-exported-files-to-be-same-as-the-source-blobs"></a><span data-ttu-id="47684-139">Définition de l’heure de la dernière modification des fichiers exportés pour qu’elle soit identique à celle des objets blob source</span><span class="sxs-lookup"><span data-stu-id="47684-139">Set the last-modified time of exported files to be same as the source blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

<span data-ttu-id="47684-140">Vous pouvez également exclure des objets blob de l’opération de téléchargement en vous basant sur l’heure de leur dernière modification</span><span class="sxs-lookup"><span data-stu-id="47684-140">You can also exclude blobs from the download operation based on their last-modified time.</span></span> <span data-ttu-id="47684-141">Par exemple, si vous souhaitez exclure les objets blob dont la dernière heure de modification est identique ou plus récente que celle du fichier de destination `/XN` :</span><span class="sxs-lookup"><span data-stu-id="47684-141">For example, if you want to exclude blobs whose last modified time is the same or newer than the destination file, add the `/XN` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

<span data-ttu-id="47684-142">Ou si vous souhaitez exclure les objets blob dont la dernière heure de modification est identique ou plus ancienne que celle du fichier de destination `/XO` :</span><span class="sxs-lookup"><span data-stu-id="47684-142">Or if you want to exclude blobs whose last modified time is the same or older than the destination file, add the `/XO` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a><span data-ttu-id="47684-143">Objet blob : Téléchargement</span><span class="sxs-lookup"><span data-stu-id="47684-143">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="47684-144">Télécharger un fichier unique</span><span class="sxs-lookup"><span data-stu-id="47684-144">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="47684-145">Si le conteneur de destination spécifié n’existe pas, AzCopy le crée et y charge le fichier.</span><span class="sxs-lookup"><span data-stu-id="47684-145">If the specified destination container does not exist, AzCopy will create it and upload the file into it.</span></span>

### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="47684-146">Télécharger un fichier unique dans le répertoire virtuel</span><span class="sxs-lookup"><span data-stu-id="47684-146">Upload single file to virtual directory</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="47684-147">Si le répertoire virtuel spécifié n’existe pas, AzCopy charge le fichier pour y inclure le répertoire virtuel dans son nom (*par exemple*, `vd/abc.txt` dans l’exemple ci-dessus).</span><span class="sxs-lookup"><span data-stu-id="47684-147">If the specified virtual directory does not exist, AzCopy will upload the file to include the virtual directory in its name (*e.g.*, `vd/abc.txt` in the example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="47684-148">Télécharger tous les fichiers</span><span class="sxs-lookup"><span data-stu-id="47684-148">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

<span data-ttu-id="47684-149">La spécification de l’option `/S` engendre le téléchargement des contenus du répertoire spécifié vers le stockage d’objets blob récursivement, ce qui implique également la copie de tous les sous-dossiers et de leurs fichiers.</span><span class="sxs-lookup"><span data-stu-id="47684-149">Specifying option `/S` uploads the contents of the specified directory to Blob storage recursively, meaning that all subfolders and their files will be uploaded as well.</span></span> <span data-ttu-id="47684-150">Par exemple, si les fichiers suivants se trouvent dans le dossier `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="47684-150">For instance, assume the following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="47684-151">Après l’opération de téléchargement, le conteneur inclut les fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="47684-151">After the upload operation, the container will include the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="47684-152">Si vous ne spécifiez pas l’option `/S`, AzCopy ne charge pas de manière récursive.</span><span class="sxs-lookup"><span data-stu-id="47684-152">If you do not specify option `/S`, AzCopy will not upload recursively.</span></span> <span data-ttu-id="47684-153">Après l’opération de téléchargement, le conteneur inclut les fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="47684-153">After the upload operation, the container will include the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="47684-154">Télécharger des fichiers correspondant au modèle spécifié</span><span class="sxs-lookup"><span data-stu-id="47684-154">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

<span data-ttu-id="47684-155">Si les fichiers suivants se trouvent dans le dossier `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="47684-155">Assume the following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="47684-156">Après l’opération de téléchargement, le conteneur inclut les fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="47684-156">After the upload operation, the container will include the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="47684-157">Si vous ne spécifiez pas l’option `/S`, AzCopy téléchargera uniquement les objets blob qui ne se trouvent pas dans un répertoire virtuel :</span><span class="sxs-lookup"><span data-stu-id="47684-157">If you do not specify option `/S`, AzCopy will only upload blobs that don't reside in a virtual directory:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-the-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="47684-158">Spécifier le type de contenu MIME d’un objet blob de destination</span><span class="sxs-lookup"><span data-stu-id="47684-158">Specify the MIME content type of a destination blob</span></span>
<span data-ttu-id="47684-159">Par défaut, AzCopy définit le type de contenu d'un objet blob de destination comme `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="47684-159">By default, AzCopy sets the content type of a destination blob to `application/octet-stream`.</span></span> <span data-ttu-id="47684-160">Depuis la version 3.1.0, vous pouvez spécifier explicitement le type de contenu via l'option `/SetContentType:[content-type]`.</span><span class="sxs-lookup"><span data-stu-id="47684-160">Beginning with version 3.1.0, you can explicitly specify the content type via the option `/SetContentType:[content-type]`.</span></span> <span data-ttu-id="47684-161">Cette syntaxe définit le type de contenu de tous les objets blob dans une opération de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="47684-161">This syntax sets the content type for all blobs in an upload operation.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

<span data-ttu-id="47684-162">Si vous spécifiez `/SetContentType` sans valeur, AzCopy définit chaque type de contenu d'objet blob ou de fichier en fonction de son extension de fichier.</span><span class="sxs-lookup"><span data-stu-id="47684-162">If you specify `/SetContentType` without a value, then AzCopy will set each blob or file's content type according to its file extension.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a><span data-ttu-id="47684-163">Objet blob : copie</span><span class="sxs-lookup"><span data-stu-id="47684-163">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="47684-164">Copie d’un objet blob unique au sein d’un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="47684-164">Copy single blob within Storage account</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="47684-165">Lorsque vous copiez un objet blob au sein d’un compte de stockage, une opération de [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) est exécutée.</span><span class="sxs-lookup"><span data-stu-id="47684-165">When you copy a blob within a Storage account, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="47684-166">Copier un objet blob unique sur plusieurs comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="47684-166">Copy single blob across Storage accounts</span></span>

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="47684-167">Lorsque vous copiez un objet blob sur plusieurs comptes de stockage, une opération de [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) est exécutée.</span><span class="sxs-lookup"><span data-stu-id="47684-167">When you copy a blob across Storage accounts, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-to-primary-region"></a><span data-ttu-id="47684-168">Copier un objet blob unique de la région secondaire à la région principale</span><span class="sxs-lookup"><span data-stu-id="47684-168">Copy single blob from secondary region to primary region</span></span>

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="47684-169">Notez que vous devez avoir un accès en lecture activé pour le stockage géo-redondant.</span><span class="sxs-lookup"><span data-stu-id="47684-169">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="47684-170">Copier un objet blob unique et ses captures instantanées sur plusieurs comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="47684-170">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

<span data-ttu-id="47684-171">Après l’opération de copie, le conteneur cible inclut l’objet blob et ses captures instantanées.</span><span class="sxs-lookup"><span data-stu-id="47684-171">After the copy operation, the target container will include the blob and its snapshots.</span></span> <span data-ttu-id="47684-172">Si on part du principe que l’exemple ci-dessus comprend deux captures instantanées, le conteneur inclut l’objet blob et les captures instantanées suivants :</span><span class="sxs-lookup"><span data-stu-id="47684-172">Assuming the blob in the example above has two snapshots, the container will include the following blob and snapshots:</span></span>

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="47684-173">Copier des objets blob de façon synchrone dans des comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="47684-173">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="47684-174">AzCopy copie par défaut les données entre deux points de terminaison de stockage de façon asynchrone.</span><span class="sxs-lookup"><span data-stu-id="47684-174">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="47684-175">Par conséquent, l’opération de copie s’exécute dans l’arrière-plan à l’aide de la capacité de la bande passante, non soumise à un SLA en matière de vitesse de copie d’un objet blob. AzCopy vérifie périodiquement l’état de copie jusqu’à ce que la copie soit terminée ou ait échoué.</span><span class="sxs-lookup"><span data-stu-id="47684-175">Therefore, the copy operation will run in the background using spare bandwidth capacity that has no SLA in terms of how fast a blob will be copied, and AzCopy will periodically check the copy status until the copying is completed or failed.</span></span>

<span data-ttu-id="47684-176">L'option `/SyncCopy` garantit que l'opération de copie a une vitesse constante.</span><span class="sxs-lookup"><span data-stu-id="47684-176">The `/SyncCopy` option ensures that the copy operation will get consistent speed.</span></span> <span data-ttu-id="47684-177">AzCopy effectue la copie synchrone en téléchargeant les objets blob à copier à partir de la source spécifiée dans la mémoire locale, puis en les téléchargeant sur la destination de stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="47684-177">AzCopy performs the synchronous copy by downloading the blobs to copy from the specified source to local memory, and then uploading them to the Blob storage destination.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

<span data-ttu-id="47684-178">`/SyncCopy` peut générer des coûts de sortie supplémentaires par rapport à la copie asynchrone, l’approche recommandée consiste à utiliser cette option dans une machine virtuelle Azure qui se trouve dans la même région que votre compte de stockage source afin d’éviter les frais de sortie.</span><span class="sxs-lookup"><span data-stu-id="47684-178">`/SyncCopy` might generate additional egress cost compared to asynchronous copy, the recommended approach is to use this option in an Azure VM that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="47684-179">Fichier : Téléchargement</span><span class="sxs-lookup"><span data-stu-id="47684-179">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="47684-180">Télécharger un fichier unique</span><span class="sxs-lookup"><span data-stu-id="47684-180">Download single file</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="47684-181">Si la source spécifiée est un partage de fichier Azure, vous devez soit spécifier le nom de fichier exact, (*par exemple,* `abc.txt`) pour télécharger un fichier unique, soit spécifier l’option `/S` pour télécharger tous les fichiers dans le partage de manière récursive.</span><span class="sxs-lookup"><span data-stu-id="47684-181">If the specified source is an Azure file share, then you must either specify the exact file name, (*e.g.* `abc.txt`) to download a single file, or specify option `/S` to download all files in the share recursively.</span></span> <span data-ttu-id="47684-182">Une erreur se produit si vous tentez de spécifier à la fois un modèle de fichier et l'option `/S` .</span><span class="sxs-lookup"><span data-stu-id="47684-182">Attempting to specify both a file pattern and option `/S` together will result in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="47684-183">Charger tous les fichiers</span><span class="sxs-lookup"><span data-stu-id="47684-183">Download all files</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="47684-184">Notez que les dossiers vides ne seront pas téléchargés.</span><span class="sxs-lookup"><span data-stu-id="47684-184">Note that any empty folders will not be downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="47684-185">Fichier : Télécharger</span><span class="sxs-lookup"><span data-stu-id="47684-185">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="47684-186">Télécharger un fichier unique</span><span class="sxs-lookup"><span data-stu-id="47684-186">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="47684-187">Télécharger tous les fichiers</span><span class="sxs-lookup"><span data-stu-id="47684-187">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

<span data-ttu-id="47684-188">Notez que les dossiers vides ne sont pas téléchargés.</span><span class="sxs-lookup"><span data-stu-id="47684-188">Note that any empty folders will not be uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="47684-189">Télécharger des fichiers correspondant au modèle spécifié</span><span class="sxs-lookup"><span data-stu-id="47684-189">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a><span data-ttu-id="47684-190">Fichier : Copier</span><span class="sxs-lookup"><span data-stu-id="47684-190">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="47684-191">Copier d’un partage de fichier à l’autre</span><span class="sxs-lookup"><span data-stu-id="47684-191">Copy across file shares</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="47684-192">Lorsque vous copiez un fichier sur plusieurs partage de fichiers, une opération de [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) est exécutée.</span><span class="sxs-lookup"><span data-stu-id="47684-192">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-to-blob"></a><span data-ttu-id="47684-193">Copier d’un partage de fichiers vers un objet blob</span><span class="sxs-lookup"><span data-stu-id="47684-193">Copy from file share to blob</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="47684-194">Lorsque vous copiez un fichier d’un partage de fichiers vers un objet blob, une opération de [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) est exécutée.</span><span class="sxs-lookup"><span data-stu-id="47684-194">When you copy a file from file share to blob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>


### <a name="copy-from-blob-to-file-share"></a><span data-ttu-id="47684-195">Copier d’un objet blob vers le partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="47684-195">Copy from blob to file share</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="47684-196">Lorsque vous copiez un fichier d’un objet blob vers un partage de fichiers, une opération de [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) est exécutée.</span><span class="sxs-lookup"><span data-stu-id="47684-196">When you copy a file from blob to file share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="47684-197">Copier les fichiers de façon synchrone</span><span class="sxs-lookup"><span data-stu-id="47684-197">Synchronously copy files</span></span>
<span data-ttu-id="47684-198">Vous pouvez spécifier l’option `/SyncCopy` pour copier d’un stockage de fichiers vers un autre stockage de fichiers, d’un stockage de fichiers vers un stockage d’objet blob et d’un stockage d’objet blob o un stockage de fichiers de façon synchrone. Pour ce faire, AzCopy télécharge les données sources dans la mémoire locale, puis les charge à nouveau vers la destination.</span><span class="sxs-lookup"><span data-stu-id="47684-198">You can specify the `/SyncCopy` option to copy data from File Storage to File Storage, from File Storage to Blob Storage and from Blob Storage to File Storage synchronously, AzCopy does this by downloading the source data to local memory and upload it again to destination.</span></span> <span data-ttu-id="47684-199">Des coûts de sortie standard s’appliquent.</span><span class="sxs-lookup"><span data-stu-id="47684-199">Standard egress cost will apply.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

<span data-ttu-id="47684-200">Pendant la copie depuis le stockage de fichier vers le stockage d'objets Blob, le type d'objet Blob par défaut est l'objet Blob de blocs. L'utilisateur peut spécifier l'option `/BlobType:page` pour modifier le type d'objet Blob de destination.</span><span class="sxs-lookup"><span data-stu-id="47684-200">When copying from File Storage to Blob Storage, the default blob type is block blob, user can specify option `/BlobType:page` to change the destination blob type.</span></span>

<span data-ttu-id="47684-201">Notez que `/SyncCopy` peut occasionner des coûts supplémentaires par rapport à une copie asynchrone. L'approche recommandée consiste à utiliser cette option dans la machine virtuelle Azure qui se trouve dans la même région que votre compte de stockage source afin d'éviter les coûts de sortie.</span><span class="sxs-lookup"><span data-stu-id="47684-201">Note that `/SyncCopy` might generate additional egress cost comparing to asynchronous copy, the recommended approach is to use this option in the Azure VM which is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="table-export"></a><span data-ttu-id="47684-202">Table : Exportation</span><span class="sxs-lookup"><span data-stu-id="47684-202">Table: Export</span></span>
### <a name="export-table"></a><span data-ttu-id="47684-203">Table d’exportation</span><span class="sxs-lookup"><span data-stu-id="47684-203">Export table</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

<span data-ttu-id="47684-204">AzCopy écrit un fichier manifeste dans le dossier de destination spécifié.</span><span class="sxs-lookup"><span data-stu-id="47684-204">AzCopy writes a manifest file to the specified destination folder.</span></span> <span data-ttu-id="47684-205">Le processus d’importation utilise ce fichier manifeste pour localiser les fichiers de données nécessaires et effectuer la validation des données.</span><span class="sxs-lookup"><span data-stu-id="47684-205">The manifest file is used in the import process to locate the necessary data files and perform data validation.</span></span> <span data-ttu-id="47684-206">Le fichier manifeste utilise la convention de noms suivante par défaut :</span><span class="sxs-lookup"><span data-stu-id="47684-206">The manifest file uses the following naming convention by default:</span></span>

    <account name>_<table name>_<timestamp>.manifest

<span data-ttu-id="47684-207">L'utilisateur peut également spécifier l'option `/Manifest:<manifest file name>` pour définir le nom du fichier manifeste.</span><span class="sxs-lookup"><span data-stu-id="47684-207">User can also specify the option `/Manifest:<manifest file name>` to set the manifest file name.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a><span data-ttu-id="47684-208">Fractionnement de l’exportation en plusieurs fichiers</span><span class="sxs-lookup"><span data-stu-id="47684-208">Split export into multiple files</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

<span data-ttu-id="47684-209">AzCopy utilise un *index de volume* dans les noms des fichiers de données fractionnés pour distinguer les fichiers.</span><span class="sxs-lookup"><span data-stu-id="47684-209">AzCopy uses a *volume index* in the split data file names to distinguish multiple files.</span></span> <span data-ttu-id="47684-210">L’index de volume se compose de deux parties : un *index de plage de clés de partition* et un *index de fichier fractionné*.</span><span class="sxs-lookup"><span data-stu-id="47684-210">The volume index consists of two parts, a *partition key range index* and a *split file index*.</span></span> <span data-ttu-id="47684-211">Ces deux index commencent à zéro.</span><span class="sxs-lookup"><span data-stu-id="47684-211">Both indexes are zero-based.</span></span>

<span data-ttu-id="47684-212">L’index de plage de clés de partition est égal à 0 si l’utilisateur ne spécifie pas l’option `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="47684-212">The partition key range index will be 0 if user does not specify option `/PKRS`.</span></span>

<span data-ttu-id="47684-213">Exemple : supposons qu'AzCopy crée deux fichiers de données après que l'utilisateur a spécifié l'option `/SplitSize`.</span><span class="sxs-lookup"><span data-stu-id="47684-213">For instance, suppose AzCopy generates two data files after the user specifies option `/SplitSize`.</span></span> <span data-ttu-id="47684-214">Les noms des fichiers de données qui en résultent peuvent être :</span><span class="sxs-lookup"><span data-stu-id="47684-214">The resulting data file names might be:</span></span>

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

<span data-ttu-id="47684-215">Remarque : la valeur minimale possible pour l’option `/SplitSize` est 32 Mo.</span><span class="sxs-lookup"><span data-stu-id="47684-215">Note that the minimum possible value for option `/SplitSize` is 32MB.</span></span> <span data-ttu-id="47684-216">Si la destination spécifiée est un stockage d'objets blob, AzCopy fractionne le fichier de données lorsque sa taille atteint la limite de taille des objets blob (200 Go), que l'utilisateur ait spécifié ou non l'option `/SplitSize` .</span><span class="sxs-lookup"><span data-stu-id="47684-216">If the specified destination is Blob storage, AzCopy will split the data file once its sizes reaches the blob size limitation (200GB), regardless of whether option `/SplitSize` has been specified by the user.</span></span>

### <a name="export-table-to-json-or-csv-data-file-format"></a><span data-ttu-id="47684-217">Table d’exportation vers un format de fichier de données CSV ou JSON</span><span class="sxs-lookup"><span data-stu-id="47684-217">Export table to JSON or CSV data file format</span></span>
<span data-ttu-id="47684-218">AzCopy par défaut exporte des tables dans des fichiers de données JSON.</span><span class="sxs-lookup"><span data-stu-id="47684-218">AzCopy by default exports tables to JSON data files.</span></span> <span data-ttu-id="47684-219">Vous pouvez spécifier l’option `/PayloadFormat:JSON|CSV` pour exporter les tables en tant que JSON ou CSV.</span><span class="sxs-lookup"><span data-stu-id="47684-219">You can specify the option `/PayloadFormat:JSON|CSV` to export the tables as JSON or CSV.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

<span data-ttu-id="47684-220">Lorsque vous spécifiez le format de charge utile CSV, AzCopy génère également un fichier de schéma avec l’extension `.schema.csv` pour chaque fichier de données.</span><span class="sxs-lookup"><span data-stu-id="47684-220">When specifying the CSV payload format, AzCopy will also generate a schema file with file extension `.schema.csv` for each data file.</span></span>

### <a name="export-table-entities-concurrently"></a><span data-ttu-id="47684-221">Exportation simultanée d’entités de table</span><span class="sxs-lookup"><span data-stu-id="47684-221">Export table entities concurrently</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

<span data-ttu-id="47684-222">AzCopy lance des opérations simultanées d'exportation d'entités lorsque l'utilisateur spécifie l'option `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="47684-222">AzCopy will start concurrent operations to export entities when the user specifies option `/PKRS`.</span></span> <span data-ttu-id="47684-223">Chaque opération exporte une plage de clés de partition.</span><span class="sxs-lookup"><span data-stu-id="47684-223">Each operation exports one partition key range.</span></span>

<span data-ttu-id="47684-224">Remarque : l'option `/NC`contrôle également le nombre d'opérations simultanées.</span><span class="sxs-lookup"><span data-stu-id="47684-224">Note that the number of concurrent operations is also controlled by option `/NC`.</span></span> <span data-ttu-id="47684-225">AzCopy utilise le nombre de processeurs Core comme valeur par défaut de `/NC` pendant la copie d'entités de table, même si l'option `/NC` n'a pas été spécifiée.</span><span class="sxs-lookup"><span data-stu-id="47684-225">AzCopy uses the number of core processors as the default value of `/NC` when copying table entities, even if `/NC` was not specified.</span></span> <span data-ttu-id="47684-226">Lorsque l'utilisateur spécifie l'option `/PKRS`, AzCopy utilise la plus petite des deux valeurs (plages de clés de partition par rapport aux opérations simultanées implicitement ou explicitement spécifiées) pour déterminer le nombre d'opérations simultanées à démarrer.</span><span class="sxs-lookup"><span data-stu-id="47684-226">When the user specifies option `/PKRS`, AzCopy uses the smaller of the two values - partition key ranges versus implicitly or explicitly specified concurrent operations - to determine the number of concurrent operations to start.</span></span> <span data-ttu-id="47684-227">Pour plus d'informations, tapez `AzCopy /?:NC` dans la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="47684-227">For more details, type `AzCopy /?:NC` at the command line.</span></span>

### <a name="export-table-to-blob"></a><span data-ttu-id="47684-228">Table d’exportation d’objet blob</span><span class="sxs-lookup"><span data-stu-id="47684-228">Export table to blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

<span data-ttu-id="47684-229">AzCopy crée un fichier de données JSON dans le conteneur d’objets blob en respectant la convention de noms suivante :</span><span class="sxs-lookup"><span data-stu-id="47684-229">AzCopy will generate a JSON data file into the blob container with following naming convention:</span></span>

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

<span data-ttu-id="47684-230">Le fichier de données JSON créé respecte le format de charge utile pour les métadonnées minimales.</span><span class="sxs-lookup"><span data-stu-id="47684-230">The generated JSON data file follows the payload format for minimal metadata.</span></span> <span data-ttu-id="47684-231">Pour des informations sur le format de charge utile, consultez la page [Format de charge utile pour les opérations du service de Table](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span><span class="sxs-lookup"><span data-stu-id="47684-231">For details on this payload format, see [Payload Format for Table Service Operations](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span></span>

<span data-ttu-id="47684-232">Notez que lors de l’exportation des tables vers les objets blob, AzCopy télécharge les entités de Table vers les fichiers de données temporaires locaux et téléchargez ensuite ces entités dans l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="47684-232">Note that when exporting tables to blobs, AzCopy will download the Table entities to local temporary data files and then upload those entities to the blob.</span></span> <span data-ttu-id="47684-233">Ces fichiers de données temporaires sont placés dans le dossier du fichier journal avec le chemin par défaut « <code>%LocalAppData%\Microsoft\Azure\AzCopy</code> ». Vous pouvez spécifier l’option /Z:[dossier du fichier journal] pour modifier l’emplacement du dossier du fichier et changer ainsi l’emplacement des fichiers de données temporaires.</span><span class="sxs-lookup"><span data-stu-id="47684-233">These temporary data files are put into the journal file folder with the default path "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", you can specify option /Z:[journal-file-folder] to change the journal file folder location and thus change the temporary data files location.</span></span> <span data-ttu-id="47684-234">La taille des fichiers de données temporaires est définie par la taille de vos entités de table et la taille spécifiée avec l’option /SplitSize, bien que le fichier de données temporaire dans le disque local soit supprimé instantanément une fois qu’il a été chargé vers l’objet blob. Vérifiez que vous disposez de suffisamment d’espace sur le disque local pour stocker ces fichiers de données temporaires avant qu’ils soient supprimés.</span><span class="sxs-lookup"><span data-stu-id="47684-234">The temporary data files' size is decided by your table entities' size and the size you specified with the option /SplitSize, although the temporary data file in local disk will be deleted instantly once it has been uploaded to the blob, please make sure you have enough local disk space to store these temporary data files before they are deleted.</span></span>

## <a name="table-import"></a><span data-ttu-id="47684-235">Table : importation</span><span class="sxs-lookup"><span data-stu-id="47684-235">Table: Import</span></span>
### <a name="import-table"></a><span data-ttu-id="47684-236">Table d’importation</span><span class="sxs-lookup"><span data-stu-id="47684-236">Import table</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

<span data-ttu-id="47684-237">L'option `/EntityOperation` indique comment insérer des entités dans la table.</span><span class="sxs-lookup"><span data-stu-id="47684-237">The option `/EntityOperation` indicates how to insert entities into the table.</span></span> <span data-ttu-id="47684-238">Les valeurs possibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="47684-238">Possible values are:</span></span>

* <span data-ttu-id="47684-239">`InsertOrSkip`: ignore une entité existante ou insère une nouvelle entité si elle n'existe pas dans la table.</span><span class="sxs-lookup"><span data-stu-id="47684-239">`InsertOrSkip`: Skips an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="47684-240">`InsertOrMerge`: fusionne une entité existante ou insère une nouvelle entité si elle n'existe pas dans la table.</span><span class="sxs-lookup"><span data-stu-id="47684-240">`InsertOrMerge`: Merges an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="47684-241">`InsertOrReplace` : remplace une entité existante ou insère une nouvelle entité si elle n'existe pas dans la table.</span><span class="sxs-lookup"><span data-stu-id="47684-241">`InsertOrReplace`: Replaces an existing entity or inserts a new entity if it does not exist in the table.</span></span>

<span data-ttu-id="47684-242">Remarque : vous ne pouvez pas spécifier l'option `/PKRS` dans le scénario d'importation.</span><span class="sxs-lookup"><span data-stu-id="47684-242">Note that you cannot specify option `/PKRS` in the import scenario.</span></span> <span data-ttu-id="47684-243">À la différence du scénario d’exportation dans lequel vous devez spécifier l’option `/PKRS` pour démarrer des opérations simultanées, AzCopy lance par défaut des opérations simultanées lorsque vous importez une table.</span><span class="sxs-lookup"><span data-stu-id="47684-243">Unlike the export scenario, in which you must specify option `/PKRS` to start concurrent operations, AzCopy will by default start concurrent operations when you import a table.</span></span> <span data-ttu-id="47684-244">Le nombre par défaut d’opérations simultanées démarrées est égal au nombre de processeurs Core. Cependant, vous pouvez spécifier un nombre différent d’opérations simultanées avec l’option `/NC`.</span><span class="sxs-lookup"><span data-stu-id="47684-244">The default number of concurrent operations started is equal to the number of core processors; however, you can specify a different number of concurrent with option `/NC`.</span></span> <span data-ttu-id="47684-245">Pour plus d'informations, tapez `AzCopy /?:NC` dans la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="47684-245">For more details, type `AzCopy /?:NC` at the command line.</span></span>

<span data-ttu-id="47684-246">Notez qu’AzCopy ne prend en charge que l’importation pour JSON, et non CSV.</span><span class="sxs-lookup"><span data-stu-id="47684-246">Note that AzCopy only supports importing for JSON, not CSV.</span></span> <span data-ttu-id="47684-247">AzCopy ne prend pas en charge les importations de table à partir de fichiers JSON créés par l’utilisateur et de fichiers manifeste.</span><span class="sxs-lookup"><span data-stu-id="47684-247">AzCopy does not support table imports from user-created JSON and manifest files.</span></span> <span data-ttu-id="47684-248">Ces deux types de fichiers doivent provenir d’une exportation de table AzCopy.</span><span class="sxs-lookup"><span data-stu-id="47684-248">Both of these files must come from an AzCopy table export.</span></span> <span data-ttu-id="47684-249">Pour éviter les erreurs, ne modifiez pas le fichier JSON ou le fichier manifeste exporté.</span><span class="sxs-lookup"><span data-stu-id="47684-249">To avoid errors, please do not modify the exported JSON or manifest file.</span></span>

### <a name="import-entities-to-table-using-blobs"></a><span data-ttu-id="47684-250">Importez des entités vers la table à l’aide d’objets blob</span><span class="sxs-lookup"><span data-stu-id="47684-250">Import entities to table using blobs</span></span>
<span data-ttu-id="47684-251">Supposons qu’un conteneur d’objets blob contient les éléments suivants : fichier JSON représentant une table Azure et le fichier manifeste associé.</span><span class="sxs-lookup"><span data-stu-id="47684-251">Assume a Blob container contains the following: A JSON file representing an Azure Table and its accompanying manifest file.</span></span>

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

<span data-ttu-id="47684-252">Vous pouvez exécuter la commande suivante pour importer des entités dans une table en utilisant le fichier manifeste dans le conteneur d’objets blob :</span><span class="sxs-lookup"><span data-stu-id="47684-252">You can run the following command to import entities into a table using the manifest file in that blob container:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a><span data-ttu-id="47684-253">Autres fonctionnalités AzCopy</span><span class="sxs-lookup"><span data-stu-id="47684-253">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-the-destination"></a><span data-ttu-id="47684-254">Copier uniquement les données qui n’existent pas dans la destination</span><span class="sxs-lookup"><span data-stu-id="47684-254">Only copy data that doesn't exist in the destination</span></span>
<span data-ttu-id="47684-255">Les paramètres `/XO` et `/XN` vous permettent d’exclure les ressources source plus anciennes ou plus récentes d’être copiées respectivement.</span><span class="sxs-lookup"><span data-stu-id="47684-255">The `/XO` and `/XN` parameters allow you to exclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="47684-256">Si vous souhaitez copier uniquement des ressources de code source qui n’existent pas dans la destination, vous pouvez spécifier les deux paramètres dans la commande AzCopy :</span><span class="sxs-lookup"><span data-stu-id="47684-256">If you only want to copy source resources that don't exist in the destination, you can specify both parameters in the AzCopy command:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

<span data-ttu-id="47684-257">Notez que cela n’est pas pris en charge lorsque la source ou la destination est une table.</span><span class="sxs-lookup"><span data-stu-id="47684-257">Note that this is not supported when either the source or destination is a table.</span></span>

### <a name="use-a-response-file-to-specify-command-line-parameters"></a><span data-ttu-id="47684-258">Utilisation d’un fichier réponse pour spécifier les paramètres de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="47684-258">Use a response file to specify command-line parameters</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

<span data-ttu-id="47684-259">Vous pouvez inclure n’importe quels paramètres de ligne de commande AzCopy dans un fichier réponse.</span><span class="sxs-lookup"><span data-stu-id="47684-259">You can include any AzCopy command-line parameters in a response file.</span></span> <span data-ttu-id="47684-260">AzCopy traite les paramètres du fichier comme s’ils avaient été spécifiés sur la ligne de commande, réalisant une substitution directe avec les contenus du fichier.</span><span class="sxs-lookup"><span data-stu-id="47684-260">AzCopy processes the parameters in the file as if they had been specified on the command line, performing a direct substitution with the contents of the file.</span></span>

<span data-ttu-id="47684-261">Si un fichier réponse nommé `copyoperation.txt`, qui contient les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="47684-261">Assume a response file named `copyoperation.txt`, that contains the following lines.</span></span> <span data-ttu-id="47684-262">Chaque paramètre AzCopy peut être spécifié sur une seule ligne</span><span class="sxs-lookup"><span data-stu-id="47684-262">Each AzCopy parameter can be specified on a single line</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

<span data-ttu-id="47684-263">ou sur des lignes distinctes :</span><span class="sxs-lookup"><span data-stu-id="47684-263">or on separate lines:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

<span data-ttu-id="47684-264">AzCopy échouera si vous écrivez le paramètre sur deux lignes, comme démontré ici pour le paramètre `/sourcekey` :</span><span class="sxs-lookup"><span data-stu-id="47684-264">AzCopy will fail if you split the parameter across two lines, as shown here for the `/sourcekey` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-to-specify-command-line-parameters"></a><span data-ttu-id="47684-265">Utilisation de plusieurs fichiers réponse pour spécifier les paramètres de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="47684-265">Use multiple response files to specify command-line parameters</span></span>
<span data-ttu-id="47684-266">Si un fichier réponse dénommé `source.txt` qui spécifie un conteneur source :</span><span class="sxs-lookup"><span data-stu-id="47684-266">Assume a response file named `source.txt` that specifies a source container:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer

<span data-ttu-id="47684-267">Et un fichier réponse nommé `dest.txt` qui spécifie un dossier de destination dans le système de fichiers :</span><span class="sxs-lookup"><span data-stu-id="47684-267">And a response file named `dest.txt` that specifies a destination folder in the file system:</span></span>

    /Dest:C:\myfolder

<span data-ttu-id="47684-268">Et un fichier réponse nommé `options.txt` qui spécifie les options pour AzCopy :</span><span class="sxs-lookup"><span data-stu-id="47684-268">And a response file named `options.txt` that specifies options for AzCopy:</span></span>

    /S /Y

<span data-ttu-id="47684-269">Appellent AzCopy avec ces fichiers réponse résidant tous dans un répertoire `C:\responsefiles`, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="47684-269">To call AzCopy with these response files, all of which reside in a directory `C:\responsefiles`, use this command:</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

<span data-ttu-id="47684-270">AzCopy traite cette commande comme si vous aviez inclus tous les paramètres individuels de la ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="47684-270">AzCopy processes this command just as it would if you included all of the individual parameters on the command line:</span></span>

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="47684-271">Spécification d’une signature d’accès partagé (SAP)</span><span class="sxs-lookup"><span data-stu-id="47684-271">Specify a shared access signature (SAS)</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

<span data-ttu-id="47684-272">Vous pouvez également spécifier une SAP sur l’URI du conteneur :</span><span class="sxs-lookup"><span data-stu-id="47684-272">You can also specify a SAS on the container URI:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a><span data-ttu-id="47684-273">Dossier du fichier journal</span><span class="sxs-lookup"><span data-stu-id="47684-273">Journal file folder</span></span>
<span data-ttu-id="47684-274">Chaque fois que vous émettez une commande sur AzCopy, il vérifie si un fichier journal existe dans le dossier par défaut ou dans un dossier que vous avez spécifié via cette option.</span><span class="sxs-lookup"><span data-stu-id="47684-274">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="47684-275">Si le fichier journal n’existe à aucun de ces emplacements, AzCopy considère l’opération comme nouvelle et génère un nouveau fichier journal.</span><span class="sxs-lookup"><span data-stu-id="47684-275">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="47684-276">Si le fichier journal existe, AzCopy vérifie si la ligne de commande que vous entrez correspond à la ligne de commande du fichier journal.</span><span class="sxs-lookup"><span data-stu-id="47684-276">If the journal file does exist, AzCopy will check whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="47684-277">Si les deux lignes de commande correspondent, AzCopy reprend l’opération incomplète.</span><span class="sxs-lookup"><span data-stu-id="47684-277">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="47684-278">Si elles ne correspondent pas, il vous sera demandé soit d’écraser le fichier journal pour démarrer une nouvelle opération, soit d’annuler l’opération actuelle.</span><span class="sxs-lookup"><span data-stu-id="47684-278">If they do not match, you will be prompted to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="47684-279">Si vous souhaitez utiliser l’emplacement par défaut pour le fichier journal :</span><span class="sxs-lookup"><span data-stu-id="47684-279">If you want to use the default location for the journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

<span data-ttu-id="47684-280">Si vous omettez l'option `/Z`, ou spécifiez l'option `/Z` sans le chemin du dossier, comme démontré ci-dessus, AzCopy crée le fichier journal à l'emplacement par défaut, qui est `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="47684-280">If you omit option `/Z`, or specify option `/Z` without the folder path, as shown above, AzCopy creates the journal file in the default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="47684-281">Si le fichier journal existe déjà, AzCopy reprend l’opération en se basant sur le fichier journal.</span><span class="sxs-lookup"><span data-stu-id="47684-281">If the journal file already exists, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="47684-282">Si vous souhaitez spécifier un emplacement personnalisé pour le fichier journal :</span><span class="sxs-lookup"><span data-stu-id="47684-282">If you want to specify a custom location for the journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

<span data-ttu-id="47684-283">Cet exemple crée le fichier journal s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="47684-283">This example creates the journal file if it does not already exist.</span></span> <span data-ttu-id="47684-284">S’il existe, AzCopy reprend l’opération en se basant sur le fichier journal.</span><span class="sxs-lookup"><span data-stu-id="47684-284">If it does exist, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="47684-285">Si vous souhaitez reprendre une opération AzCopy :</span><span class="sxs-lookup"><span data-stu-id="47684-285">If you want to resume an AzCopy operation:</span></span>

```azcopy
AzCopy /Z:C:\journalfolder\
```

<span data-ttu-id="47684-286">Cet exemple reprend la dernière opération, qui est susceptible de ne pas avoir abouti.</span><span class="sxs-lookup"><span data-stu-id="47684-286">This example resumes the last operation, which may have failed to complete.</span></span>

### <a name="generate-a-log-file"></a><span data-ttu-id="47684-287">Génération d’un fichier journal</span><span class="sxs-lookup"><span data-stu-id="47684-287">Generate a log file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

<span data-ttu-id="47684-288">Si vous spécifiez l’option `/V` sans fournir de chemin de fichier pour le journal détaillé, AzCopy crée le fichier journal à l’emplacement par défaut, qui est `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="47684-288">If you specify option `/V` without providing a file path to the verbose log, then AzCopy creates the log file in the default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span>

<span data-ttu-id="47684-289">Autrement, vous pouvez créer un fichier journal dans un emplacement personnalisé :</span><span class="sxs-lookup"><span data-stu-id="47684-289">Otherwise, you can create an log file in a custom location:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

<span data-ttu-id="47684-290">Remarque : si vous spécifiez un chemin relatif suivant l'option `/V`, tel que `/V:test/azcopy1.log`, le journal détaillé est alors créé dans le répertoire en cours d'utilisation dans un sous-dossier nommé `test`.</span><span class="sxs-lookup"><span data-stu-id="47684-290">Note that if you specify a relative path following option `/V`, such as `/V:test/azcopy1.log`, then the verbose log is created in the current working directory within a subfolder named `test`.</span></span>

### <a name="specify-the-number-of-concurrent-operations-to-start"></a><span data-ttu-id="47684-291">Spécification du nombre d’opérations simultanées pour démarrer</span><span class="sxs-lookup"><span data-stu-id="47684-291">Specify the number of concurrent operations to start</span></span>
<span data-ttu-id="47684-292">L'option `/NC` spécifie le nombre d'opérations de copie simultanées.</span><span class="sxs-lookup"><span data-stu-id="47684-292">Option `/NC` specifies the number of concurrent copy operations.</span></span> <span data-ttu-id="47684-293">Par défaut, AzCopy lance un certain nombre d’opérations simultanées pour augmenter la vitesse de transfert des données.</span><span class="sxs-lookup"><span data-stu-id="47684-293">By default, AzCopy starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="47684-294">Pour les opérations sur les tables, le nombre d’opérations simultanées est égal au nombre de processeurs dont vous disposez.</span><span class="sxs-lookup"><span data-stu-id="47684-294">For Table operations, the number of concurrent operations is equal to the number of processors you have.</span></span> <span data-ttu-id="47684-295">Pour les opérations sur les objets blob et les fichiers, le nombre d’opérations simultanées est égal à 8 fois le nombre de processeurs dont vous disposez.</span><span class="sxs-lookup"><span data-stu-id="47684-295">For Blob and File operations, the number of concurrent operations is equal 8 times the number of processors you have.</span></span> <span data-ttu-id="47684-296">Si vous exécutez AzCopy sur un réseau à bande passante étroite, vous pouvez spécifier un nombre inférieur pour /NC afin d’éviter l’échec causé par la compétition de ressources.</span><span class="sxs-lookup"><span data-stu-id="47684-296">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for /NC to avoid failure caused by resource competition.</span></span>

### <a name="run-azcopy-against-azure-storage-emulator"></a><span data-ttu-id="47684-297">Exécutez AzCopy sur l’émulateur de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="47684-297">Run AzCopy against Azure Storage Emulator</span></span>
<span data-ttu-id="47684-298">Vous pouvez exécuter AzCopy sur l’ [émulateur de stockage Azure](storage-use-emulator.md) pour les objets blob :</span><span class="sxs-lookup"><span data-stu-id="47684-298">You can run AzCopy against the [Azure Storage Emulator](storage-use-emulator.md) for Blobs:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

<span data-ttu-id="47684-299">et les tables :</span><span class="sxs-lookup"><span data-stu-id="47684-299">and Tables:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a><span data-ttu-id="47684-300">Paramètres AzCopy</span><span class="sxs-lookup"><span data-stu-id="47684-300">AzCopy Parameters</span></span>
<span data-ttu-id="47684-301">Les paramètres d’AzCopy sont décrits ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="47684-301">Parameters for AzCopy are described below.</span></span> <span data-ttu-id="47684-302">Vous pouvez également taper une des commandes suivantes dans la ligne de commande pour obtenir de l’aide sur l’utilisation d’AzCopy :</span><span class="sxs-lookup"><span data-stu-id="47684-302">You can also type one of the following commands from the command line for help in using AzCopy:</span></span>

* <span data-ttu-id="47684-303">Pour l'aide détaillée sur la ligne de commande AzCopy : `AzCopy /?`</span><span class="sxs-lookup"><span data-stu-id="47684-303">For detailed command-line help for AzCopy: `AzCopy /?`</span></span>
* <span data-ttu-id="47684-304">Pour l'aide détaillée sur un paramètre AzCopy : `AzCopy /?:SourceKey`</span><span class="sxs-lookup"><span data-stu-id="47684-304">For detailed help with any AzCopy parameter: `AzCopy /?:SourceKey`</span></span>
* <span data-ttu-id="47684-305">Pour des exemples de ligne de commande : `AzCopy /?:Samples`</span><span class="sxs-lookup"><span data-stu-id="47684-305">For command-line examples: `AzCopy /?:Samples`</span></span>

### <a name="sourcesource"></a><span data-ttu-id="47684-306">/Source:"source"</span><span class="sxs-lookup"><span data-stu-id="47684-306">/Source:"source"</span></span>
<span data-ttu-id="47684-307">Spécifie les données sources à partir desquelles la copie peut s’effectuer.</span><span class="sxs-lookup"><span data-stu-id="47684-307">Specifies the source data from which to copy.</span></span> <span data-ttu-id="47684-308">La source peut être un répertoire du système de fichiers, un conteneur d’objets blob, un répertoire virtuel d’objets blob, un partage de fichiers de stockage, un répertoire de fichiers de stockage ou une table Azure.</span><span class="sxs-lookup"><span data-stu-id="47684-308">The source can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="47684-309">**S’applique à :** objets blob, fichiers, tables</span><span class="sxs-lookup"><span data-stu-id="47684-309">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destdestination"></a><span data-ttu-id="47684-310">/Dest:"destination"</span><span class="sxs-lookup"><span data-stu-id="47684-310">/Dest:"destination"</span></span>
<span data-ttu-id="47684-311">Spécifie la destination vers laquelle la copie va s’effectuer.</span><span class="sxs-lookup"><span data-stu-id="47684-311">Specifies the destination to copy to.</span></span> <span data-ttu-id="47684-312">La destination peut être un répertoire du système de fichiers, un conteneur d’objets blob, un répertoire virtuel d’objets blob, un partage de fichiers de stockage, un répertoire de fichiers de stockage ou une table Azure.</span><span class="sxs-lookup"><span data-stu-id="47684-312">The destination can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="47684-313">**S’applique à :** objets blob, fichiers, tables</span><span class="sxs-lookup"><span data-stu-id="47684-313">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="patternfile-pattern"></a><span data-ttu-id="47684-314">/Pattern:"file-pattern"</span><span class="sxs-lookup"><span data-stu-id="47684-314">/Pattern:"file-pattern"</span></span>
<span data-ttu-id="47684-315">Spécifie un modèle de fichier qui indique les fichiers à copier.</span><span class="sxs-lookup"><span data-stu-id="47684-315">Specifies a file pattern that indicates which files to copy.</span></span> <span data-ttu-id="47684-316">Le comportement du paramètre /Pattern est déterminé par l’emplacement des données sources et la présence de l’option mode récursif.</span><span class="sxs-lookup"><span data-stu-id="47684-316">The behavior of the /Pattern parameter is determined by the location of the source data, and the presence of the recursive mode option.</span></span> <span data-ttu-id="47684-317">Le mode récursif est spécifié via l’option /S.</span><span class="sxs-lookup"><span data-stu-id="47684-317">Recursive mode is specified via option /S.</span></span>

<span data-ttu-id="47684-318">Si la source spécifiée est un répertoire dans le système de fichiers, les caractères génériques standard sont appliqués et le modèle de fichier fourni est comparé aux fichiers présents dans le répertoire.</span><span class="sxs-lookup"><span data-stu-id="47684-318">If the specified source is a directory in the file system, then standard wildcards are in effect, and the file pattern provided is matched against files within the directory.</span></span> <span data-ttu-id="47684-319">Si l’option /S est spécifiée, AzCopy compare également le modèle spécifié à tous les fichiers présents dans les sous-dossiers du répertoire.</span><span class="sxs-lookup"><span data-stu-id="47684-319">If option /S is specified, then AzCopy also matches the specified pattern against all files in any subfolders beneath the directory.</span></span>

<span data-ttu-id="47684-320">Si la source spécifiée est un conteneur d’objets blob ou un répertoire virtuel, les caractères génériques ne sont pas appliqués.</span><span class="sxs-lookup"><span data-stu-id="47684-320">If the specified source is a blob container or virtual directory, then wildcards are not applied.</span></span> <span data-ttu-id="47684-321">Si l’option /S est spécifiée, AzCopy interprète le modèle de fichier spécifié comme un préfixe d’objet blob.</span><span class="sxs-lookup"><span data-stu-id="47684-321">If option /S is specified, then AzCopy interprets the specified file pattern as a blob prefix.</span></span> <span data-ttu-id="47684-322">Si l’option /S n’est pas spécifiée, AzCopy compare le modèle de fichier aux noms exacts d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="47684-322">If option /S is not specified, then AzCopy matches the file pattern against exact blob names.</span></span>

<span data-ttu-id="47684-323">Si la source spécifiée est un partage de fichiers Azure, vous devez soit spécifier le nom exact du fichier (abc.txt) pour copier un seul fichier, soit spécifier l’option /S pour copier récursivement tous les fichiers dans le partage.</span><span class="sxs-lookup"><span data-stu-id="47684-323">If the specified source is an Azure file share, then you must either specify the exact file name, (e.g. abc.txt) to copy a single file, or specify option /S to copy all files in the share recursively.</span></span> <span data-ttu-id="47684-324">Une erreur se produit si vous tentez de spécifier à la fois un modèle de fichier et l’option /S.</span><span class="sxs-lookup"><span data-stu-id="47684-324">Attempting to specify both a file pattern and option /S together will result in an error.</span></span>

<span data-ttu-id="47684-325">AzCopy tient compte de la casse uniquement quand la /Source est un conteneur d’objets blob ou un répertoire virtuel d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="47684-325">AzCopy uses case-sensitive matching when the /Source is a blob container or blob virtual directory, and uses case-insensitive matching in all the other cases.</span></span>

<span data-ttu-id="47684-326">Le modèle de fichier par défaut utilisé lorsqu’aucun modèle de fichier n’est spécifié est *.*</span><span class="sxs-lookup"><span data-stu-id="47684-326">The default file pattern used when no file pattern is specified is *.*</span></span> <span data-ttu-id="47684-327">pour un emplacement de système de fichiers, ou un préfixe vide pour un emplacement Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="47684-327">for a file system location or an empty prefix for an Azure Storage location.</span></span> <span data-ttu-id="47684-328">La spécification de plusieurs modèles de fichiers n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="47684-328">Specifying multiple file patterns is not supported.</span></span>

<span data-ttu-id="47684-329">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="47684-329">**Applicable to:** Blobs, Files</span></span>

### <a name="destkeystorage-key"></a><span data-ttu-id="47684-330">/DestKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="47684-330">/DestKey:"storage-key"</span></span>
<span data-ttu-id="47684-331">Spécifie la clé du compte de stockage pour la ressource de destination.</span><span class="sxs-lookup"><span data-stu-id="47684-331">Specifies the storage account key for the destination resource.</span></span>

<span data-ttu-id="47684-332">**S’applique à :** objets blob, fichiers, tables</span><span class="sxs-lookup"><span data-stu-id="47684-332">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destsassas-token"></a><span data-ttu-id="47684-333">/DestSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="47684-333">/DestSAS:"sas-token"</span></span>
<span data-ttu-id="47684-334">Spécifie une signature d’accès partagé (SAP) avec les autorisations de lecture et d’écriture pour la destination (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="47684-334">Specifies a Shared Access Signature (SAS) with READ and WRITE permissions for the destination (if applicable).</span></span> <span data-ttu-id="47684-335">Ajoutez des guillemets à la SAP, car elle peut contenir des caractères spéciaux de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="47684-335">Surround the SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="47684-336">Si la ressource de destination est un conteneur d’objets blob, un partage de fichiers ou une table, vous pouvez spécifier soit cette option suivie du jeton SAP, soit la SAP comme élément d’URI de l’objet blob, du partage de fichiers ou de la table de destination, sans cette option.</span><span class="sxs-lookup"><span data-stu-id="47684-336">If the destination resource is a blob container, file share or table, you can either specify this option followed by the SAS token, or you can specify the SAS as part of the destination blob container, file share or table's URI, without this option.</span></span>

<span data-ttu-id="47684-337">Si la source et la destination sont toutes les deux des objets blob, l’objet blob de destination doit se trouver dans le même compte de stockage que l’objet blob source.</span><span class="sxs-lookup"><span data-stu-id="47684-337">If the source and destination are both blobs, then the destination blob must reside within the same storage account as the source blob.</span></span>

<span data-ttu-id="47684-338">**S’applique à :** objets blob, fichiers, tables</span><span class="sxs-lookup"><span data-stu-id="47684-338">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcekeystorage-key"></a><span data-ttu-id="47684-339">/SourceKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="47684-339">/SourceKey:"storage-key"</span></span>
<span data-ttu-id="47684-340">Spécifie la clé du compte de stockage pour la ressource source.</span><span class="sxs-lookup"><span data-stu-id="47684-340">Specifies the storage account key for the source resource.</span></span>

<span data-ttu-id="47684-341">**S’applique à :** objets blob, fichiers, tables</span><span class="sxs-lookup"><span data-stu-id="47684-341">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcesassas-token"></a><span data-ttu-id="47684-342">/SourceSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="47684-342">/SourceSAS:"sas-token"</span></span>
<span data-ttu-id="47684-343">Spécifie une signature d’accès partagé avec les autorisations de lecture et de listing pour la source (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="47684-343">Specifies a Shared Access Signature with READ and LIST permissions for the source (if applicable).</span></span> <span data-ttu-id="47684-344">Ajoutez des guillemets à la SAP, car elle peut contenir des caractères spéciaux de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="47684-344">Surround the SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="47684-345">Si la ressource source est un conteneur d’objets blob et si aucune clé ou SAP n’est fournie, le conteneur est lu via un accès anonyme.</span><span class="sxs-lookup"><span data-stu-id="47684-345">If the source resource is a blob container, and neither a key nor a SAS is provided, then the blob container will be read via anonymous access.</span></span>

<span data-ttu-id="47684-346">Si la source est un partage de fichiers ou une table, une clé ou une SAP doit être fournie.</span><span class="sxs-lookup"><span data-stu-id="47684-346">If the source is a file share or table, a key or a SAS must be provided.</span></span>

<span data-ttu-id="47684-347">**S’applique à :** objets blob, fichiers, tables</span><span class="sxs-lookup"><span data-stu-id="47684-347">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="s"></a><span data-ttu-id="47684-348">/S</span><span class="sxs-lookup"><span data-stu-id="47684-348">/S</span></span>
<span data-ttu-id="47684-349">Spécifie le mode récursif pour les opérations de copie.</span><span class="sxs-lookup"><span data-stu-id="47684-349">Specifies recursive mode for copy operations.</span></span> <span data-ttu-id="47684-350">En mode récursif, AzCopy copie tous les objets blob ou fichiers correspondant au modèle de fichier spécifié, incluant ceux qui se trouvent dans les sous-dossiers.</span><span class="sxs-lookup"><span data-stu-id="47684-350">In recursive mode, AzCopy will copy all blobs or files that match the specified file pattern, including those in subfolders.</span></span>

<span data-ttu-id="47684-351">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="47684-351">**Applicable to:** Blobs, Files</span></span>

### <a name="blobtypeblock--page--append"></a><span data-ttu-id="47684-352">/BlobType:"block" | "page" | "append"</span><span class="sxs-lookup"><span data-stu-id="47684-352">/BlobType:"block" | "page" | "append"</span></span>
<span data-ttu-id="47684-353">Spécifie si la destination est un objet blob de blocs, un objet blob de pages ou un objet blob d’ajout.</span><span class="sxs-lookup"><span data-stu-id="47684-353">Specifies whether the destination blob is a block blob, a page blob, or an append blob.</span></span> <span data-ttu-id="47684-354">Cette option s’applique uniquement lorsque vous téléchargez un objet blob.</span><span class="sxs-lookup"><span data-stu-id="47684-354">This option is applicable only when you are uploading a blob.</span></span> <span data-ttu-id="47684-355">Sinon, une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="47684-355">Otherwise, an error is generated.</span></span> <span data-ttu-id="47684-356">Si la destination est un objet blob et si cette option n’est pas spécifiée, AzCopy crée par défaut un objet blob de blocs.</span><span class="sxs-lookup"><span data-stu-id="47684-356">If the destination is a blob and this option is not specified, by default, AzCopy creates a block blob.</span></span>

<span data-ttu-id="47684-357">**S’applique à :** objets blob</span><span class="sxs-lookup"><span data-stu-id="47684-357">**Applicable to:** Blobs</span></span>

### <a name="checkmd5"></a><span data-ttu-id="47684-358">/CheckMD5</span><span class="sxs-lookup"><span data-stu-id="47684-358">/CheckMD5</span></span>
<span data-ttu-id="47684-359">Calcule un hachage MD5 pour les données téléchargées et vérifie que le hachage MD5 stocké dans la propriété Content-MD5 de l'objet blob ou du fichier correspond au hachage calculé.</span><span class="sxs-lookup"><span data-stu-id="47684-359">Calculates an MD5 hash for downloaded data and verifies that the MD5 hash stored in the blob or file's Content-MD5 property matches the calculated hash.</span></span> <span data-ttu-id="47684-360">La vérification MD5 est désactivée par défaut ; vous devez donc spécifier cette option pour lancer la vérification MD5 lorsque vous téléchargez des données.</span><span class="sxs-lookup"><span data-stu-id="47684-360">The MD5 check is turned off by default, so you must specify this option to perform the MD5 check when downloading data.</span></span>

<span data-ttu-id="47684-361">Remarque : Azure Storage ne garantit pas que le hachage MD5 stocké pour l’objet blob ou le fichier est à jour.</span><span class="sxs-lookup"><span data-stu-id="47684-361">Note that Azure Storage doesn't guarantee that the MD5 hash stored for the blob or file is up-to-date.</span></span> <span data-ttu-id="47684-362">Il est de la responsabilité du client de mettre à jour le MD5 lorsque l’objet blob ou le fichier est modifié.</span><span class="sxs-lookup"><span data-stu-id="47684-362">It is client's responsibility to update the MD5 whenever the blob or file is modified.</span></span>

<span data-ttu-id="47684-363">AzCopy établit toujours la propriété Content-MD5 pour un objet blob ou fichier Azure après l’avoir chargé sur le service.</span><span class="sxs-lookup"><span data-stu-id="47684-363">AzCopy always sets the Content-MD5 property for an Azure blob or file after uploading it to the service.</span></span>  

<span data-ttu-id="47684-364">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="47684-364">**Applicable to:** Blobs, Files</span></span>

### <a name="snapshot"></a><span data-ttu-id="47684-365">/Snapshot</span><span class="sxs-lookup"><span data-stu-id="47684-365">/Snapshot</span></span>
<span data-ttu-id="47684-366">Indique si le transfert de captures instantanées est activé ou non.</span><span class="sxs-lookup"><span data-stu-id="47684-366">Indicates whether to transfer snapshots.</span></span> <span data-ttu-id="47684-367">Cette option est valide uniquement lorsque la source est un objet blob.</span><span class="sxs-lookup"><span data-stu-id="47684-367">This option is only valid when the source is a blob.</span></span>

<span data-ttu-id="47684-368">Les captures instantanées d’objets blob transférées sont renommées de cette façon : nom_d’objet_Blob (durée de capture instantanée).extension</span><span class="sxs-lookup"><span data-stu-id="47684-368">The transferred blob snapshots are renamed in this format: blob-name (snapshot-time).extension</span></span>

<span data-ttu-id="47684-369">Par défaut, les captures instantanées ne sont pas copiées.</span><span class="sxs-lookup"><span data-stu-id="47684-369">By default, snapshots are not copied.</span></span>

<span data-ttu-id="47684-370">**S’applique à :** objets blob</span><span class="sxs-lookup"><span data-stu-id="47684-370">**Applicable to:** Blobs</span></span>

### <a name="vverbose-log-file"></a><span data-ttu-id="47684-371">/V:[verbose-log-file]</span><span class="sxs-lookup"><span data-stu-id="47684-371">/V:[verbose-log-file]</span></span>
<span data-ttu-id="47684-372">Stocke les messages de statut détaillés dans un fichier journal.</span><span class="sxs-lookup"><span data-stu-id="47684-372">Outputs verbose status messages into a log file.</span></span>

<span data-ttu-id="47684-373">Par défaut, le fichier journal détaillé est nommé dans `%LocalAppData%\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="47684-373">By default, the verbose log file is named AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="47684-374">Si vous spécifiez un emplacement de fichier existant pour cette option, le journal détaillé est ajouté à ce fichier.</span><span class="sxs-lookup"><span data-stu-id="47684-374">If you specify an existing file location for this option, the verbose log will be appended to that file.</span></span>  

<span data-ttu-id="47684-375">**S’applique à :** objets blob, fichiers, tables</span><span class="sxs-lookup"><span data-stu-id="47684-375">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="zjournal-file-folder"></a><span data-ttu-id="47684-376">/Z:[journal-file-folder]</span><span class="sxs-lookup"><span data-stu-id="47684-376">/Z:[journal-file-folder]</span></span>
<span data-ttu-id="47684-377">Spécifie un dossier de fichier journal pour reprendre une opération.</span><span class="sxs-lookup"><span data-stu-id="47684-377">Specifies a journal file folder for resuming an operation.</span></span>

<span data-ttu-id="47684-378">AzCopy peut toujours reprendre une opération qui a été interrompue.</span><span class="sxs-lookup"><span data-stu-id="47684-378">AzCopy always supports resuming if an operation has been interrupted.</span></span>

<span data-ttu-id="47684-379">Si cette option n’est pas spécifiée ou est spécifiée sans chemin de dossier, AzCopy crée le fichier journal à l’emplacement par défaut, qui est %LocalAppData%\Microsoft\Azure\AzCopy.</span><span class="sxs-lookup"><span data-stu-id="47684-379">If this option is not specified, or it is specified without a folder path, then AzCopy will create the journal file in the default location, which is %LocalAppData%\Microsoft\Azure\AzCopy.</span></span>

<span data-ttu-id="47684-380">Chaque fois que vous émettez une commande sur AzCopy, il vérifie si un fichier journal existe dans le dossier par défaut ou dans un dossier que vous avez spécifié via cette option.</span><span class="sxs-lookup"><span data-stu-id="47684-380">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="47684-381">Si le fichier journal n’existe à aucun de ces emplacements, AzCopy considère l’opération comme nouvelle et génère un nouveau fichier journal.</span><span class="sxs-lookup"><span data-stu-id="47684-381">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="47684-382">Si le fichier journal existe, AzCopy vérifie si la ligne de commande que vous entrez correspond à la ligne de commande du fichier journal.</span><span class="sxs-lookup"><span data-stu-id="47684-382">If the journal file does exist, AzCopy will check whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="47684-383">Si les deux lignes de commande correspondent, AzCopy reprend l’opération incomplète.</span><span class="sxs-lookup"><span data-stu-id="47684-383">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="47684-384">Si elles ne correspondent pas, il vous sera demandé soit d’écraser le fichier journal pour démarrer une nouvelle opération, soit d’annuler l’opération actuelle.</span><span class="sxs-lookup"><span data-stu-id="47684-384">If they do not match, you will be prompted to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="47684-385">Le fichier journal est supprimé lorsque l’opération est achevée avec succès.</span><span class="sxs-lookup"><span data-stu-id="47684-385">The journal file is deleted upon successful completion of the operation.</span></span>

<span data-ttu-id="47684-386">Remarque : reprendre une opération à partir d’un fichier journal créé par une version précédente d’AzCopy n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="47684-386">Note that resuming an operation from a journal file created by a previous version of AzCopy is not supported.</span></span>

<span data-ttu-id="47684-387">**S’applique à :** objets blob, fichiers, tables</span><span class="sxs-lookup"><span data-stu-id="47684-387">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="parameter-file"></a><span data-ttu-id="47684-388">/@:"parameter-file"</span><span class="sxs-lookup"><span data-stu-id="47684-388">/@:"parameter-file"</span></span>
<span data-ttu-id="47684-389">Spécifie un fichier qui contient des paramètres.</span><span class="sxs-lookup"><span data-stu-id="47684-389">Specifies a file that contains parameters.</span></span> <span data-ttu-id="47684-390">AzCopy traite les paramètres dans le fichier comme s’ils avaient été spécifiés dans la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="47684-390">AzCopy processes the parameters in the file just as if they had been specified on the command line.</span></span>

<span data-ttu-id="47684-391">Dans un fichier réponse, vous pouvez soit spécifier de multiples paramètres sur une seule ligne, soit spécifier chaque paramètre sur sa propre ligne.</span><span class="sxs-lookup"><span data-stu-id="47684-391">In a response file, you can either specify multiple parameters on a single line, or specify each parameter on its own line.</span></span> <span data-ttu-id="47684-392">Remarque : un paramètre individuel ne peut pas couvrir plusieurs lignes.</span><span class="sxs-lookup"><span data-stu-id="47684-392">Note that an individual parameter cannot span multiple lines.</span></span>

<span data-ttu-id="47684-393">Les fichiers réponse peuvent inclure des lignes de commentaires qui commencent par le symbole #.</span><span class="sxs-lookup"><span data-stu-id="47684-393">Response files can include comments lines that begin with the # symbol.</span></span>

<span data-ttu-id="47684-394">Vous pouvez spécifier plusieurs fichiers réponse.</span><span class="sxs-lookup"><span data-stu-id="47684-394">You can specify multiple response files.</span></span> <span data-ttu-id="47684-395">Toutefois, AzCopy ne prend pas en charge les fichiers réponse imbriqués.</span><span class="sxs-lookup"><span data-stu-id="47684-395">However, note that AzCopy does not support nested response files.</span></span>

<span data-ttu-id="47684-396">**S’applique à :** objets blob, fichiers, tables</span><span class="sxs-lookup"><span data-stu-id="47684-396">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="y"></a><span data-ttu-id="47684-397">/Y</span><span class="sxs-lookup"><span data-stu-id="47684-397">/Y</span></span>
<span data-ttu-id="47684-398">Supprime toutes les invites de confirmation d’AzCopy.</span><span class="sxs-lookup"><span data-stu-id="47684-398">Suppresses all AzCopy confirmation prompts.</span></span>

<span data-ttu-id="47684-399">**S’applique à :** objets blob, fichiers, tables</span><span class="sxs-lookup"><span data-stu-id="47684-399">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="l"></a><span data-ttu-id="47684-400">/L</span><span class="sxs-lookup"><span data-stu-id="47684-400">/L</span></span>
<span data-ttu-id="47684-401">Spécifie une opération de listing uniquement : aucune donnée n’est copiée.</span><span class="sxs-lookup"><span data-stu-id="47684-401">Specifies a listing operation only; no data is copied.</span></span>

<span data-ttu-id="47684-402">AzCopy interprète l’utilisation de cette option comme une simulation de l’exécution de la ligne de commande sans cette option /L et compte le nombre d’objets copiés. Vous pouvez spécifier l’option /V en même temps pour déterminer les objets destinés à être copiés dans le journal détaillé.</span><span class="sxs-lookup"><span data-stu-id="47684-402">AzCopy will interpret the using of this option as a simulation for running the command line without this option /L and count how many objects will be copied, you can specify option /V at the same time to check which objects will be copied in the verbose log.</span></span>

<span data-ttu-id="47684-403">Le comportement de cette option est également déterminé par l’emplacement des données sources et la présence de l’option mode récursif /S et de l’option modèle de fichier /Pattern.</span><span class="sxs-lookup"><span data-stu-id="47684-403">The behavior of this option is also determined by the location of the source data and the presence of the recursive mode option /S and file pattern option /Pattern.</span></span>

<span data-ttu-id="47684-404">AzCopy nécessite les autorisations de listing et de lecture sur cet emplacement source quand cette option est utilisée.</span><span class="sxs-lookup"><span data-stu-id="47684-404">AzCopy requires LIST and READ permission of this source location when using this option.</span></span>

<span data-ttu-id="47684-405">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="47684-405">**Applicable to:** Blobs, Files</span></span>

### <a name="mt"></a><span data-ttu-id="47684-406">/MT</span><span class="sxs-lookup"><span data-stu-id="47684-406">/MT</span></span>
<span data-ttu-id="47684-407">Définit l’heure de la dernière modification du fichier pour qu’elle soit identique à celle de l’objet blob ou du fichier source.</span><span class="sxs-lookup"><span data-stu-id="47684-407">Sets the downloaded file's last-modified time to be the same as the source blob or file's.</span></span>

<span data-ttu-id="47684-408">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="47684-408">**Applicable to:** Blobs, Files</span></span>

### <a name="xn"></a><span data-ttu-id="47684-409">/XN</span><span class="sxs-lookup"><span data-stu-id="47684-409">/XN</span></span>
<span data-ttu-id="47684-410">Exclut une ressource de source plus récente.</span><span class="sxs-lookup"><span data-stu-id="47684-410">Excludes a newer source resource.</span></span> <span data-ttu-id="47684-411">La ressource n’est pas copiée si la dernière heure de modification de la source est identique ou plus récente que la destination.</span><span class="sxs-lookup"><span data-stu-id="47684-411">The resource will not be copied if the last modified time of the source is the same or newer than destination.</span></span>

<span data-ttu-id="47684-412">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="47684-412">**Applicable to:** Blobs, Files</span></span>

### <a name="xo"></a><span data-ttu-id="47684-413">/XO</span><span class="sxs-lookup"><span data-stu-id="47684-413">/XO</span></span>
<span data-ttu-id="47684-414">Exclut une ressource de source plus ancienne.</span><span class="sxs-lookup"><span data-stu-id="47684-414">Excludes an older source resource.</span></span> <span data-ttu-id="47684-415">La ressource n’est pas copiée si la dernière heure de modification de la source est identique ou plus ancienne que la destination.</span><span class="sxs-lookup"><span data-stu-id="47684-415">The resource will not be copied if the last modified time of the source is the same or older than destination.</span></span>

<span data-ttu-id="47684-416">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="47684-416">**Applicable to:** Blobs, Files</span></span>

### <a name="a"></a><span data-ttu-id="47684-417">/A</span><span class="sxs-lookup"><span data-stu-id="47684-417">/A</span></span>
<span data-ttu-id="47684-418">Charge uniquement les fichiers dont l’attribut Archive est défini.</span><span class="sxs-lookup"><span data-stu-id="47684-418">Uploads only files that have the Archive attribute set.</span></span>

<span data-ttu-id="47684-419">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="47684-419">**Applicable to:** Blobs, Files</span></span>

### <a name="iarashcnetoi"></a><span data-ttu-id="47684-420">/IA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="47684-420">/IA:[RASHCNETOI]</span></span>
<span data-ttu-id="47684-421">Télécharge uniquement les fichiers qui ont le jeu d’attributs spécifiés.</span><span class="sxs-lookup"><span data-stu-id="47684-421">Uploads only files that have any of the specified attributes set.</span></span>

<span data-ttu-id="47684-422">Les attributs disponibles incluent :</span><span class="sxs-lookup"><span data-stu-id="47684-422">Available attributes include:</span></span>

* <span data-ttu-id="47684-423">R = Fichiers en lecture seule</span><span class="sxs-lookup"><span data-stu-id="47684-423">R = Read-only files</span></span>
* <span data-ttu-id="47684-424">A = Fichiers prêts à être archivés</span><span class="sxs-lookup"><span data-stu-id="47684-424">A = Files ready for archiving</span></span>
* <span data-ttu-id="47684-425">S = Fichiers système</span><span class="sxs-lookup"><span data-stu-id="47684-425">S = System files</span></span>
* <span data-ttu-id="47684-426">H = Fichiers masqués</span><span class="sxs-lookup"><span data-stu-id="47684-426">H = Hidden files</span></span>
* <span data-ttu-id="47684-427">C = Fichiers compressés</span><span class="sxs-lookup"><span data-stu-id="47684-427">C = Compressed files</span></span>
* <span data-ttu-id="47684-428">N = Fichiers normaux</span><span class="sxs-lookup"><span data-stu-id="47684-428">N = Normal files</span></span>
* <span data-ttu-id="47684-429">E = Fichiers cryptés</span><span class="sxs-lookup"><span data-stu-id="47684-429">E = Encrypted files</span></span>
* <span data-ttu-id="47684-430">T = Fichiers temporaires</span><span class="sxs-lookup"><span data-stu-id="47684-430">T = Temporary files</span></span>
* <span data-ttu-id="47684-431">O = Fichiers hors ligne</span><span class="sxs-lookup"><span data-stu-id="47684-431">O = Offline files</span></span>
* <span data-ttu-id="47684-432">I = Fichiers non indexés</span><span class="sxs-lookup"><span data-stu-id="47684-432">I = Non-indexed files</span></span>

<span data-ttu-id="47684-433">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="47684-433">**Applicable to:** Blobs, Files</span></span>

### <a name="xarashcnetoi"></a><span data-ttu-id="47684-434">/XA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="47684-434">/XA:[RASHCNETOI]</span></span>
<span data-ttu-id="47684-435">Exclut les fichiers dont l’un des attributs spécifiés est défini.</span><span class="sxs-lookup"><span data-stu-id="47684-435">Excludes files that have any of the specified attributes set.</span></span>

<span data-ttu-id="47684-436">Les attributs disponibles incluent :</span><span class="sxs-lookup"><span data-stu-id="47684-436">Available attributes include:</span></span>

* <span data-ttu-id="47684-437">R = Fichiers en lecture seule</span><span class="sxs-lookup"><span data-stu-id="47684-437">R = Read-only files</span></span>
* <span data-ttu-id="47684-438">A = Fichiers prêts à être archivés</span><span class="sxs-lookup"><span data-stu-id="47684-438">A = Files ready for archiving</span></span>
* <span data-ttu-id="47684-439">S = Fichiers système</span><span class="sxs-lookup"><span data-stu-id="47684-439">S = System files</span></span>
* <span data-ttu-id="47684-440">H = Fichiers masqués</span><span class="sxs-lookup"><span data-stu-id="47684-440">H = Hidden files</span></span>
* <span data-ttu-id="47684-441">C = Fichiers compressés</span><span class="sxs-lookup"><span data-stu-id="47684-441">C = Compressed files</span></span>
* <span data-ttu-id="47684-442">N = Fichiers normaux</span><span class="sxs-lookup"><span data-stu-id="47684-442">N = Normal files</span></span>
* <span data-ttu-id="47684-443">E = Fichiers cryptés</span><span class="sxs-lookup"><span data-stu-id="47684-443">E = Encrypted files</span></span>
* <span data-ttu-id="47684-444">T = Fichiers temporaires</span><span class="sxs-lookup"><span data-stu-id="47684-444">T = Temporary files</span></span>
* <span data-ttu-id="47684-445">O = Fichiers hors ligne</span><span class="sxs-lookup"><span data-stu-id="47684-445">O = Offline files</span></span>
* <span data-ttu-id="47684-446">I = Fichiers non indexés</span><span class="sxs-lookup"><span data-stu-id="47684-446">I = Non-indexed files</span></span>

<span data-ttu-id="47684-447">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="47684-447">**Applicable to:** Blobs, Files</span></span>

### <a name="delimiterdelimiter"></a><span data-ttu-id="47684-448">/Delimiter:"délimiteur"</span><span class="sxs-lookup"><span data-stu-id="47684-448">/Delimiter:"delimiter"</span></span>
<span data-ttu-id="47684-449">Indique le caractère délimiteur utilisé pour délimiter les répertoires virtuels dans un nom d’objet blob.</span><span class="sxs-lookup"><span data-stu-id="47684-449">Indicates the delimiter character used to delimit virtual directories in a blob name.</span></span>

<span data-ttu-id="47684-450">Par défaut, AzCopy utilise / comme caractère délimiteur.</span><span class="sxs-lookup"><span data-stu-id="47684-450">By default, AzCopy uses / as the delimiter character.</span></span> <span data-ttu-id="47684-451">Toutefois, AzCopy prend en charge n’importe quel caractère commun (tel que @, #, ou %) comme délimiteur.</span><span class="sxs-lookup"><span data-stu-id="47684-451">However, AzCopy supports using any common character (such as @, #, or %) as a delimiter.</span></span> <span data-ttu-id="47684-452">Si vous avez besoin d’inclure l’un de ces caractères spéciaux dans la ligne de commande, ajoutez des guillemets doubles au nom du fichier.</span><span class="sxs-lookup"><span data-stu-id="47684-452">If you need to include one of these special characters on the command line, enclose the file name with double quotes.</span></span>

<span data-ttu-id="47684-453">Cette option est applicable uniquement au téléchargement d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="47684-453">This option is only applicable for downloading blobs.</span></span>

<span data-ttu-id="47684-454">**S’applique à :** objets blob</span><span class="sxs-lookup"><span data-stu-id="47684-454">**Applicable to:** Blobs</span></span>

### <a name="ncnumber-of-concurrent-operations"></a><span data-ttu-id="47684-455">/NC:"nombre-d’opérations-simultanées"</span><span class="sxs-lookup"><span data-stu-id="47684-455">/NC:"number-of-concurrent-operations"</span></span>
<span data-ttu-id="47684-456">Spécifie le nombre d’opérations simultanées.</span><span class="sxs-lookup"><span data-stu-id="47684-456">Specifies the number of concurrent operations.</span></span>

<span data-ttu-id="47684-457">AzCopy lance par défaut un certain nombre d’opérations simultanées pour augmenter la vitesse de transfert des données.</span><span class="sxs-lookup"><span data-stu-id="47684-457">AzCopy by default starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="47684-458">Remarque : un grand nombre d’opérations simultanées dans un environnement à faible bande passante peut surcharger la connexion réseau et entraver le bon déroulement des opérations.</span><span class="sxs-lookup"><span data-stu-id="47684-458">Note that large number of concurrent operations in a low-bandwidth environment may overwhelm the network connection and prevent the operations from fully completing.</span></span> <span data-ttu-id="47684-459">Limitez les opérations simultanées en fonction de la bande passante de réseau qui est disponible.</span><span class="sxs-lookup"><span data-stu-id="47684-459">Throttle concurrent operations based on actual available network bandwidth.</span></span>

<span data-ttu-id="47684-460">Le nombre maximal d’opérations simultanées est égal à 512.</span><span class="sxs-lookup"><span data-stu-id="47684-460">The upper limit for concurrent operations is 512.</span></span>

<span data-ttu-id="47684-461">**S’applique à :** objets blob, fichiers, tables</span><span class="sxs-lookup"><span data-stu-id="47684-461">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcetypeblob--table"></a><span data-ttu-id="47684-462">/SourceType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="47684-462">/SourceType:"Blob" | "Table"</span></span>
<span data-ttu-id="47684-463">Spécifie que la ressource `source` est un objet blob disponible dans l’environnement de développement local, exécuté sur l’émulateur de stockage.</span><span class="sxs-lookup"><span data-stu-id="47684-463">Specifies that the `source` resource is a blob available in the local development environment, running in the storage emulator.</span></span>

<span data-ttu-id="47684-464">**S’applique à :** objets blob, tables</span><span class="sxs-lookup"><span data-stu-id="47684-464">**Applicable to:** Blobs, Tables</span></span>

### <a name="desttypeblob--table"></a><span data-ttu-id="47684-465">/DestType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="47684-465">/DestType:"Blob" | "Table"</span></span>
<span data-ttu-id="47684-466">Spécifie que la ressource `destination` est un objet blob disponible dans l’environnement de développement local, exécuté sur l’émulateur de stockage.</span><span class="sxs-lookup"><span data-stu-id="47684-466">Specifies that the `destination` resource is a blob available in the local development environment, running in the storage emulator.</span></span>

<span data-ttu-id="47684-467">**S’applique à :** objets blob, tables</span><span class="sxs-lookup"><span data-stu-id="47684-467">**Applicable to:** Blobs, Tables</span></span>

### <a name="pkrskey1key2key3"></a><span data-ttu-id="47684-468">/PKRS:"key1#key2#key3#..."</span><span class="sxs-lookup"><span data-stu-id="47684-468">/PKRS:"key1#key2#key3#..."</span></span>
<span data-ttu-id="47684-469">Fractionne la plage de clés de partition pour activer l’exportation des données de la table en parallèle, ce qui augmente la vitesse d’exportation.</span><span class="sxs-lookup"><span data-stu-id="47684-469">Splits the partition key range to enable exporting table data in parallel, which increases the speed of the export operation.</span></span>

<span data-ttu-id="47684-470">Si cette option n’est pas spécifiée, AzCopy utilise un seul thread pour exporter des entités de table.</span><span class="sxs-lookup"><span data-stu-id="47684-470">If this option is not specified, then AzCopy uses a single thread to export table entities.</span></span> <span data-ttu-id="47684-471">Exemple : si l’utilisateur spécifie /PKRS:"aa#bb", AzCopy lance trois opérations simultanées.</span><span class="sxs-lookup"><span data-stu-id="47684-471">For example, if the user specifies /PKRS:"aa#bb", then AzCopy starts three concurrent operations.</span></span>

<span data-ttu-id="47684-472">Chaque opération exporte une des trois plages de clés de partition (voir ci-dessous) :</span><span class="sxs-lookup"><span data-stu-id="47684-472">Each operation exports one of three partition key ranges, as shown below:</span></span>

  <span data-ttu-id="47684-473">[first-partition-key, aa)</span><span class="sxs-lookup"><span data-stu-id="47684-473">[first-partition-key, aa)</span></span>

  <span data-ttu-id="47684-474">[aa, bb)</span><span class="sxs-lookup"><span data-stu-id="47684-474">[aa, bb)</span></span>

  <span data-ttu-id="47684-475">[bb, dernière-clé-de-partition]</span><span class="sxs-lookup"><span data-stu-id="47684-475">[bb, last-partition-key]</span></span>

<span data-ttu-id="47684-476">**S’applique à :** tables</span><span class="sxs-lookup"><span data-stu-id="47684-476">**Applicable to:** Tables</span></span>

### <a name="splitsizefile-size"></a><span data-ttu-id="47684-477">/SplitSize:"file-size"</span><span class="sxs-lookup"><span data-stu-id="47684-477">/SplitSize:"file-size"</span></span>
<span data-ttu-id="47684-478">Spécifie la taille de fractionnement du fichier exporté en Mo. La valeur minimale autorisée est de 32.</span><span class="sxs-lookup"><span data-stu-id="47684-478">Specifies the exported file split size in MB, the minimal value allowed is 32.</span></span>

<span data-ttu-id="47684-479">Si cette option n’est pas spécifiée, AzCopy exporte les données de la table dans un seul fichier.</span><span class="sxs-lookup"><span data-stu-id="47684-479">If this option is not specified, AzCopy will export table data to single file.</span></span>

<span data-ttu-id="47684-480">Si les données de la table sont exportées dans un objet blob et si la taille du fichier exporté atteint la limite de 200 Go pour la taille de l’objet blob, AzCopy fractionne le fichier exporté, même si cette option n’est pas spécifiée.</span><span class="sxs-lookup"><span data-stu-id="47684-480">If the table data is exported to a blob, and the exported file size reaches the 200 GB limit for blob size, then AzCopy will split the exported file, even if this option is not specified.</span></span>

<span data-ttu-id="47684-481">**S’applique à :** tables</span><span class="sxs-lookup"><span data-stu-id="47684-481">**Applicable to:** Tables</span></span>

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a><span data-ttu-id="47684-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span><span class="sxs-lookup"><span data-stu-id="47684-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span></span>
<span data-ttu-id="47684-483">Spécifie le comportement pour l’importation des données d’une table.</span><span class="sxs-lookup"><span data-stu-id="47684-483">Specifies the table data import behavior.</span></span>

* <span data-ttu-id="47684-484">InsertOrSkip - Ignore une entité existante ou insère une nouvelle entité si elle n’existe pas dans la table.</span><span class="sxs-lookup"><span data-stu-id="47684-484">InsertOrSkip - Skips an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="47684-485">InsertOrMerge - Fusionne une entité existante ou insère une nouvelle entité si elle n’existe pas dans la table.</span><span class="sxs-lookup"><span data-stu-id="47684-485">InsertOrMerge - Merges an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="47684-486">InsertOrReplace - Remplace une entité existante ou insère une nouvelle entité si elle n’existe pas dans la table.</span><span class="sxs-lookup"><span data-stu-id="47684-486">InsertOrReplace - Replaces an existing entity or inserts a new entity if it does not exist in the table.</span></span>

<span data-ttu-id="47684-487">**S’applique à :** tables</span><span class="sxs-lookup"><span data-stu-id="47684-487">**Applicable to:** Tables</span></span>

### <a name="manifestmanifest-file"></a><span data-ttu-id="47684-488">/Manifest:"manifest-file"</span><span class="sxs-lookup"><span data-stu-id="47684-488">/Manifest:"manifest-file"</span></span>
<span data-ttu-id="47684-489">Spécifie le fichier manifeste pour l’importation et l’exportation de la table.</span><span class="sxs-lookup"><span data-stu-id="47684-489">Specifies the manifest file for the table export and import operation.</span></span>

<span data-ttu-id="47684-490">Cette option est facultative pendant l’exportation ; AzCopy génère un fichier manifeste avec un nom prédéfini si cette option n’est pas spécifiée.</span><span class="sxs-lookup"><span data-stu-id="47684-490">This option is optional during the export operation, AzCopy will generate a manifest file with predefined name if this option is not specified.</span></span>

<span data-ttu-id="47684-491">Cette option est nécessaire pendant l’importation pour localiser les fichiers de données.</span><span class="sxs-lookup"><span data-stu-id="47684-491">This option is required during the import operation for locating the data files.</span></span>

<span data-ttu-id="47684-492">**S’applique à :** tables</span><span class="sxs-lookup"><span data-stu-id="47684-492">**Applicable to:** Tables</span></span>

### <a name="synccopy"></a><span data-ttu-id="47684-493">/SyncCopy</span><span class="sxs-lookup"><span data-stu-id="47684-493">/SyncCopy</span></span>
<span data-ttu-id="47684-494">Indique s’il faut copier de manière synchronisée les objets blob ou les fichiers entre deux points de terminaison Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="47684-494">Indicates whether to synchronously copy blobs or files between two Azure Storage endpoints.</span></span>

<span data-ttu-id="47684-495">AzCopy utilise par défaut la copie asynchrone du côté serveur.</span><span class="sxs-lookup"><span data-stu-id="47684-495">AzCopy by default uses server-side asynchronous copy.</span></span> <span data-ttu-id="47684-496">Spécifiez cette option pour effectuer une copie synchrone, qui télécharge les objets blob ou les fichiers vers la mémoire locale et les télécharge Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="47684-496">Specify this option to perform a synchronous copy, which downloads blobs or files to local memory and then uploads them to Azure Storage.</span></span>

<span data-ttu-id="47684-497">Vous pouvez utiliser cette option pour la copie de fichiers dans le stockage d’objets blob, le stockage de fichiers ou depuis le stockage d’objets blob vers le stockage de fichiers ou vice versa.</span><span class="sxs-lookup"><span data-stu-id="47684-497">You can use this option when copying files within Blob storage, within File storage, or from Blob storage to File storage or vice versa.</span></span>

<span data-ttu-id="47684-498">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="47684-498">**Applicable to:** Blobs, Files</span></span>

### <a name="setcontenttypecontent-type"></a><span data-ttu-id="47684-499">/SetContentType:"content-type"</span><span class="sxs-lookup"><span data-stu-id="47684-499">/SetContentType:"content-type"</span></span>
<span data-ttu-id="47684-500">Spécifie le type de contenu MIME pour les fichiers ou les objets blob de destination.</span><span class="sxs-lookup"><span data-stu-id="47684-500">Specifies the MIME content type for destination blobs or files.</span></span>

<span data-ttu-id="47684-501">AzCopy définit le type de contenu d’un objet blob ou un fichier sur application/octet-stream par défaut.</span><span class="sxs-lookup"><span data-stu-id="47684-501">AzCopy sets the content type for a blob or file to application/octet-stream by default.</span></span> <span data-ttu-id="47684-502">Vous pouvez définir le type de contenu pour tous les objets blob ou les fichiers en spécifiant explicitement une valeur pour cette option.</span><span class="sxs-lookup"><span data-stu-id="47684-502">You can set the content type for all blobs or files by explicitly specifying a value for this option.</span></span>

<span data-ttu-id="47684-503">Si vous spécifiez cette option sans valeur, AzCopy définit chaque type de contenu d’objet blob ou de fichier en fonction de son extension de fichier.</span><span class="sxs-lookup"><span data-stu-id="47684-503">If you specify this option without a value, then AzCopy will set each blob or file's content type according to its file extension.</span></span>

<span data-ttu-id="47684-504">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="47684-504">**Applicable to:** Blobs, Files</span></span>

### <a name="payloadformatjson--csv"></a><span data-ttu-id="47684-505">/PayloadFormat:"JSON" | "CSV"</span><span class="sxs-lookup"><span data-stu-id="47684-505">/PayloadFormat:"JSON" | "CSV"</span></span>
<span data-ttu-id="47684-506">Spécifie le format du fichier de données de table exporté.</span><span class="sxs-lookup"><span data-stu-id="47684-506">Specifies the format of the table exported data file.</span></span>

<span data-ttu-id="47684-507">Si cette option n’est pas spécifiée, AzCopy exporte le fichier de données de table au format JSON par défaut.</span><span class="sxs-lookup"><span data-stu-id="47684-507">If this option is not specified, by default AzCopy exports table data file in JSON format.</span></span>

<span data-ttu-id="47684-508">**S’applique à :** tables</span><span class="sxs-lookup"><span data-stu-id="47684-508">**Applicable to:** Tables</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="47684-509">Problèmes connus et les meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="47684-509">Known Issues and Best Practices</span></span>
### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="47684-510">Limitation des écritures simultanées lors de la copie des données</span><span class="sxs-lookup"><span data-stu-id="47684-510">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="47684-511">Lorsque vous copiez des objets blob ou des fichiers avec AzCopy, gardez en tête qu’une autre application peut être en train de modifier les données pendant que vous les copiez.</span><span class="sxs-lookup"><span data-stu-id="47684-511">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying the data while you are copying it.</span></span> <span data-ttu-id="47684-512">Si possible, assurez-vous que les données que vous copiez ne sont pas modifiées pendant l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="47684-512">If possible, ensure that the data you are copying is not being modified during the copy operation.</span></span> <span data-ttu-id="47684-513">Par exemple, lorsque vous copiez un disque dur virtuel (VHD) associé à une machine virtuelle Azure, assurez-vous qu’aucune autre application n’est en train d’écrire sur le disque VHD.</span><span class="sxs-lookup"><span data-stu-id="47684-513">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing to the VHD.</span></span> <span data-ttu-id="47684-514">Un bon moyen pour ce faire consiste à louer la ressource à copier.</span><span class="sxs-lookup"><span data-stu-id="47684-514">A good way to do this is by leasing the resource to be copied.</span></span> <span data-ttu-id="47684-515">Sinon, vous pouvez commencer par créer une capture instantanée du disque VHD et copier ensuite la capture instantanée.</span><span class="sxs-lookup"><span data-stu-id="47684-515">Alternately, you can create a snapshot of the VHD first and then copy the snapshot.</span></span>

<span data-ttu-id="47684-516">Si vous ne pouvez pas empêcher d’autres applications d’écrire sur les objets blob ou les fichiers pendant qu’ils sont copiés, gardez en tête qu’au moment où la tâche sera terminée, les ressources copiées n’auront peut-être plus une parité complète avec les ressources source.</span><span class="sxs-lookup"><span data-stu-id="47684-516">If you cannot prevent other applications from writing to blobs or files while they are being copied, then keep in mind that by the time the job finishes, the copied resources may no longer have full parity with the source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="47684-517">Exécuter une instance de AzCopy sur un même ordinateur.</span><span class="sxs-lookup"><span data-stu-id="47684-517">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="47684-518">AzCopy est conçu pour optimiser l'utilisation de votre ressource de l'ordinateur afin d’accélérer le transfert de données. Nous vous recommandons d'exécuter une seule instance de AzCopy sur un même ordinateur et de spécifier l'option `/NC` si vous avez besoin de plus d'opérations simultanées.</span><span class="sxs-lookup"><span data-stu-id="47684-518">AzCopy is designed to maximize the utilization of your machine resource to accelerate the data transfer, we recommend you run only one AzCopy instance on one machine, and specify the option `/NC` if you need more concurrent operations.</span></span> <span data-ttu-id="47684-519">Pour plus d'informations, tapez `AzCopy /?:NC` dans la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="47684-519">For more details, type `AzCopy /?:NC` at the command line.</span></span>

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a><span data-ttu-id="47684-520">Activer les algorithmes MD5 compatibles FIPS pour AzCopy quand vous « utilisez des algorithmes compatibles FIPS pour le chiffrement, le hachage et la signature ».</span><span class="sxs-lookup"><span data-stu-id="47684-520">Enable FIPS compliant MD5 algorithms for AzCopy when you "Use FIPS compliant algorithms for encryption, hashing and signing".</span></span>
<span data-ttu-id="47684-521">Par défaut, AzCopy utilise l’implémentation MD5 .NET pour calculer le hachage MD5 pendant la copie d’objets, mais en raison de certaines exigences de sécurité, AzCopy doit activer le paramètre MD5 compatible FIPS.</span><span class="sxs-lookup"><span data-stu-id="47684-521">AzCopy by default uses .NET MD5 implementation to calculate the MD5 when copying objects, but there are some security requirements that need AzCopy to enable FIPS compliant MD5 setting.</span></span>

<span data-ttu-id="47684-522">Vous pouvez créer un fichier app.config `AzCopy.exe.config` avec la propriété `AzureStorageUseV1MD5` et le mettre à part avec AzCopy.exe.</span><span class="sxs-lookup"><span data-stu-id="47684-522">You can create an app.config file `AzCopy.exe.config` with property `AzureStorageUseV1MD5` and put it aside with AzCopy.exe.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

<span data-ttu-id="47684-523">Si la propriété « AzureStorageUseV1MD5 » a pour valeur true (la valeur par défaut), AzCopy utilise l’implémentation MD5 .NET.</span><span class="sxs-lookup"><span data-stu-id="47684-523">For property "AzureStorageUseV1MD5" • True - The default value, AzCopy will use .NET MD5 implementation.</span></span>
<span data-ttu-id="47684-524">Si elle a pour valeur false, AzCopy utilise l’algorithme MD5 compatible FIPS.</span><span class="sxs-lookup"><span data-stu-id="47684-524">• False – AzCopy will use FIPS compliant MD5 algorithm.</span></span>

<span data-ttu-id="47684-525">Notez que les algorithmes compatibles FIPS sont désactivés par défaut sur votre ordinateur Windows ; vous pouvez taper secpol.msc dans la fenêtre Exécuter et activer le commutateur « Chiffrement système : utilisez des algorithmes compatibles FIPS pour le chiffrement, le hachage et la signature » (Paramètres de sécurité -> Stratégies locales -> Options de sécurité).</span><span class="sxs-lookup"><span data-stu-id="47684-525">Note that FIPS compliant algorithms is disabled by default on your Windows machine, you can type secpol.msc in your Run window and check this switch at Security Setting->Local Policy->Security Options->System cryptography: Use FIPS compliant algorithms for encryption, hashing and signing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47684-526">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="47684-526">Next steps</span></span>
<span data-ttu-id="47684-527">Pour plus d’informations sur Azure Storage et AzCopy, reportez-vous aux ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="47684-527">For more information about Azure Storage and AzCopy, refer to the following resources.</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="47684-528">Documentation d’Azure Storage :</span><span class="sxs-lookup"><span data-stu-id="47684-528">Azure Storage documentation:</span></span>
* [<span data-ttu-id="47684-529">Introduction à Azure Storage</span><span class="sxs-lookup"><span data-stu-id="47684-529">Introduction to Azure Storage</span></span>](storage-introduction.md)
* [<span data-ttu-id="47684-530">Utilisation du stockage d’objets blob à partir de .NET</span><span class="sxs-lookup"><span data-stu-id="47684-530">How to use Blob storage from .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="47684-531">Utilisation du stockage de fichiers à partir de .NET</span><span class="sxs-lookup"><span data-stu-id="47684-531">How to use File storage from .NET</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="47684-532">Utilisation du stockage de tables à partir de .NET</span><span class="sxs-lookup"><span data-stu-id="47684-532">How to use Table storage from .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="47684-533">Création, gestion ou suppression d'un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="47684-533">How to create, manage, or delete a storage account</span></span>](storage-create-storage-account.md)
* [<span data-ttu-id="47684-534">Transférer des données avec AzCopy sur Linux</span><span class="sxs-lookup"><span data-stu-id="47684-534">Transfer data with AzCopy on Linux</span></span>](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="47684-535">Billets de blog Azure Storage :</span><span class="sxs-lookup"><span data-stu-id="47684-535">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="47684-536">Présentation de la bibliothèque de déplacement des données dans Azure Storage en version préliminaire</span><span class="sxs-lookup"><span data-stu-id="47684-536">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="47684-537">AzCopy : Présentation de la copie synchrone et du type de contenu personnalisé</span><span class="sxs-lookup"><span data-stu-id="47684-537">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="47684-538">AzCopy : Annonce de la disponibilité générale d'AzCopy 3.0 plus version préliminaire d'AzCopy 4.0 avec prise en charge de fichier et de table</span><span class="sxs-lookup"><span data-stu-id="47684-538">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="47684-539">AzCopy : Optimisation pour les scénarios de copie à grande échelle</span><span class="sxs-lookup"><span data-stu-id="47684-539">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="47684-540">AzCopy : Prise en charge des comptes de stockage géo-redondants avec accès en lecture</span><span class="sxs-lookup"><span data-stu-id="47684-540">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="47684-541">AzCopy : Transfert des données avec mode reprise et jeton SAP</span><span class="sxs-lookup"><span data-stu-id="47684-541">AzCopy: Transfer data with re-startable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="47684-542">AzCopy : Utilisation de copie d'objets blob sur plusieurs comptes</span><span class="sxs-lookup"><span data-stu-id="47684-542">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="47684-543">AzCopy : Chargement/téléchargement des fichiers pour les objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="47684-543">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

