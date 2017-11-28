---
title: "tooAzure de données aaaCopy ou déplacer le stockage avec AzCopy sur Windows | Documents Microsoft"
description: "Utilisez hello AzCopy sur Windows utilitaire toomove ou copie de données tooor à partir des objets blob, table et le contenu du fichier. Copier des données tooAzure stockage à partir de fichiers locales, ou copier des données dans ou entre des comptes de stockage. Migrer facilement vos données de tooAzure stockage."
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
ms.openlocfilehash: a77db84c3a3e06f0ad4e87d02b14a5c62ed8d9ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-azcopy-on-windows"></a><span data-ttu-id="e1963-105">Transfert de données avec hello AzCopy sur Windows</span><span class="sxs-lookup"><span data-stu-id="e1963-105">Transfer data with hello AzCopy on Windows</span></span>
<span data-ttu-id="e1963-106">AzCopy est un utilitaire de ligne de commande conçu pour la copie des données tooand à partir du stockage d’objets Blob Microsoft Azure, de fichier et de Table à l’aide de commandes simples avec des performances optimales.</span><span class="sxs-lookup"><span data-stu-id="e1963-106">AzCopy is a command-line utility designed for copying data tooand from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="e1963-107">Vous pouvez copier des données à partir d’un objet tooanother dans votre compte de stockage, ou entre des comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="e1963-107">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="e1963-108">Il existe deux versions d’AzCopy que vous pouvez télécharger.</span><span class="sxs-lookup"><span data-stu-id="e1963-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="e1963-109">AzCopy sur Windows est intégré à .NET Framework et offre des options en ligne de commande de style Windows.</span><span class="sxs-lookup"><span data-stu-id="e1963-109">AzCopy on Windows is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="e1963-110">[AzCopy sur Linux](storage-use-azcopy-linux.md) est intégré à .NET Core Framework, qui cible les plateformes Linux en offrant des options en ligne de commande de style POSIX.</span><span class="sxs-lookup"><span data-stu-id="e1963-110">[AzCopy on Linux](storage-use-azcopy-linux.md) is built with .NET Core Framework which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="e1963-111">Cet article est consacré à AzCopy sur Windows.</span><span class="sxs-lookup"><span data-stu-id="e1963-111">This article covers AzCopy on Windows.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="e1963-112">Téléchargement et installation d’AzCopy</span><span class="sxs-lookup"><span data-stu-id="e1963-112">Download and install AzCopy</span></span>
### <a name="azcopy-on-windows"></a><span data-ttu-id="e1963-113">AzCopy sur Windows</span><span class="sxs-lookup"><span data-stu-id="e1963-113">AzCopy on Windows</span></span>
<span data-ttu-id="e1963-114">Télécharger hello [version la plus récente de AzCopy sur Windows](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="e1963-114">Download hello [latest version of AzCopy on Windows](http://aka.ms/downloadazcopy).</span></span>

#### <a name="installation-on-windows"></a><span data-ttu-id="e1963-115">Installation sur Windows</span><span class="sxs-lookup"><span data-stu-id="e1963-115">Installation on Windows</span></span>
<span data-ttu-id="e1963-116">Après avoir installé AzCopy sur Windows à l’aide du programme d’installation Bonjour, ouvrez une fenêtre de commande et accédez répertoire d’installation toohello AzCopy sur votre ordinateur - où hello `AzCopy.exe` exécutable se trouve.</span><span class="sxs-lookup"><span data-stu-id="e1963-116">After installing AzCopy on Windows using hello installer, open a command window and navigate toohello AzCopy installation directory on your computer - where hello `AzCopy.exe` executable is located.</span></span> <span data-ttu-id="e1963-117">Si vous le souhaitez, vous pouvez ajouter le chemin d’accès de hello AzCopy installation emplacement tooyour système.</span><span class="sxs-lookup"><span data-stu-id="e1963-117">If desired, you can add hello AzCopy installation location tooyour system path.</span></span> <span data-ttu-id="e1963-118">Par défaut, AzCopy est installé trop`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` ou `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="e1963-118">By default, AzCopy is installed too`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` or `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span></span>

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="e1963-119">Écriture de votre première commande AzCopy</span><span class="sxs-lookup"><span data-stu-id="e1963-119">Writing your first AzCopy command</span></span>
<span data-ttu-id="e1963-120">syntaxe de base Hello pour les commandes AzCopy est la suivante :</span><span class="sxs-lookup"><span data-stu-id="e1963-120">hello basic syntax for AzCopy commands is:</span></span>

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

<span data-ttu-id="e1963-121">Hello suivant exemples illustrent une variété de scénarios pour la copie des données tooand à partir d’objets BLOB Microsoft Azure, les fichiers et les Tables.</span><span class="sxs-lookup"><span data-stu-id="e1963-121">hello following examples demonstrate a variety of scenarios for copying data tooand from Microsoft Azure Blobs, Files, and Tables.</span></span> <span data-ttu-id="e1963-122">Consultez toohello [AzCopy paramètres](#azcopy-parameters) section pour obtenir une explication détaillée des paramètres hello utilisées dans chaque exemple.</span><span class="sxs-lookup"><span data-stu-id="e1963-122">Refer toohello [AzCopy Parameters](#azcopy-parameters) section for a detailed explanation of hello parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="e1963-123">Blob : Téléchargement</span><span class="sxs-lookup"><span data-stu-id="e1963-123">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="e1963-124">Télécharger un seul objet blob</span><span class="sxs-lookup"><span data-stu-id="e1963-124">Download single blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="e1963-125">Notez que si le dossier de hello `C:\myfolder` n’existe pas, AzCopy crée et télécharger `abc.txt ` dans le dossier hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-125">Note that if hello folder `C:\myfolder` does not exist, AzCopy will create it and download `abc.txt ` into hello new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="e1963-126">Télécharger un objet blob unique depuis la région secondaire</span><span class="sxs-lookup"><span data-stu-id="e1963-126">Download single blob from secondary region</span></span>

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="e1963-127">Notez que vous devez avoir un accès en lecture activé pour le stockage géo-redondant.</span><span class="sxs-lookup"><span data-stu-id="e1963-127">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="e1963-128">Télécharger tous les objets blob</span><span class="sxs-lookup"><span data-stu-id="e1963-128">Download all blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="e1963-129">Supposons suivant de hello BLOB réside dans le conteneur spécifié de hello :</span><span class="sxs-lookup"><span data-stu-id="e1963-129">Assume hello following blobs reside in hello specified container:</span></span>  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="e1963-130">Après l’opération de téléchargement hello hello active `C:\myfolder` inclura hello fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="e1963-130">After hello download operation, hello directory `C:\myfolder` will include hello following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

<span data-ttu-id="e1963-131">Si vous ne spécifiez pas l’option `/S`, aucun objet blob n’est téléchargé.</span><span class="sxs-lookup"><span data-stu-id="e1963-131">If you do not specify option `/S`, no blobs will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="e1963-132">Téléchargement d’objets blob avec le préfixe spécifié</span><span class="sxs-lookup"><span data-stu-id="e1963-132">Download blobs with specified prefix</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

<span data-ttu-id="e1963-133">Supposons suivant de hello BLOB réside dans le conteneur spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-133">Assume hello following blobs reside in hello specified container.</span></span> <span data-ttu-id="e1963-134">Tous les objets BLOB commençant par préfixe de hello `a` seront téléchargés :</span><span class="sxs-lookup"><span data-stu-id="e1963-134">All blobs beginning with hello prefix `a` will be downloaded:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="e1963-135">Après l’opération de téléchargement hello hello dossier `C:\myfolder` inclura hello fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="e1963-135">After hello download operation, hello folder `C:\myfolder` will include hello following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

<span data-ttu-id="e1963-136">préfixe de Hello applique le répertoire virtuel toohello, ce qui constitue hello première partie du nom d’objet blob hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-136">hello prefix applies toohello virtual directory, which forms hello first part of hello blob name.</span></span> <span data-ttu-id="e1963-137">Exemple hello ci-dessus, répertoire virtuel de hello ne correspond pas au préfixe spécifié de hello, donc il n’est pas téléchargé.</span><span class="sxs-lookup"><span data-stu-id="e1963-137">In hello example shown above, hello virtual directory does not match hello specified prefix, so it is not downloaded.</span></span> <span data-ttu-id="e1963-138">En outre, si hello option `\S` n’est pas spécifié, AzCopy ne télécharge pas de tous les objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="e1963-138">In addition, if hello option `\S` is not specified, AzCopy will not download any blobs.</span></span>

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a><span data-ttu-id="e1963-139">Définir l’heure de dernière modification de hello de fichiers exportés toobe identique hello d’objets BLOB sources</span><span class="sxs-lookup"><span data-stu-id="e1963-139">Set hello last-modified time of exported files toobe same as hello source blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

<span data-ttu-id="e1963-140">Vous pouvez également exclure des objets BLOB à partir de l’opération de téléchargement hello en fonction de leur heure de dernière modification.</span><span class="sxs-lookup"><span data-stu-id="e1963-140">You can also exclude blobs from hello download operation based on their last-modified time.</span></span> <span data-ttu-id="e1963-141">Par exemple, si vous souhaitez que les objets BLOB de tooexclude dont heure de dernière modification est hello même ou plus récent que le fichier de destination hello, ajouter hello `/XN` option :</span><span class="sxs-lookup"><span data-stu-id="e1963-141">For example, if you want tooexclude blobs whose last modified time is hello same or newer than hello destination file, add hello `/XN` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

<span data-ttu-id="e1963-142">Ou si vous souhaitez que les objets BLOB de tooexclude dont heure de dernière modification est hello même ou antérieure à celle de fichier de destination hello, ajoutez hello `/XO` option :</span><span class="sxs-lookup"><span data-stu-id="e1963-142">Or if you want tooexclude blobs whose last modified time is hello same or older than hello destination file, add hello `/XO` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a><span data-ttu-id="e1963-143">Objet blob : Téléchargement</span><span class="sxs-lookup"><span data-stu-id="e1963-143">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="e1963-144">Télécharger un fichier unique</span><span class="sxs-lookup"><span data-stu-id="e1963-144">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="e1963-145">Si le conteneur de destination spécifié hello n’existe pas, AzCopy crée et télécharger le fichier de hello dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="e1963-145">If hello specified destination container does not exist, AzCopy will create it and upload hello file into it.</span></span>

### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="e1963-146">Téléchargement de fichier unique toovirtual Active</span><span class="sxs-lookup"><span data-stu-id="e1963-146">Upload single file toovirtual directory</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="e1963-147">Si hello spécifié le répertoire virtuel n’existe pas, AzCopy téléchargera hello fichier tooinclude hello répertoire virtuel dans son nom (*par exemple,*, `vd/abc.txt` dans l’exemple hello ci-dessus).</span><span class="sxs-lookup"><span data-stu-id="e1963-147">If hello specified virtual directory does not exist, AzCopy will upload hello file tooinclude hello virtual directory in its name (*e.g.*, `vd/abc.txt` in hello example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="e1963-148">Télécharger tous les fichiers</span><span class="sxs-lookup"><span data-stu-id="e1963-148">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

<span data-ttu-id="e1963-149">L’option `/S` contenu hello de téléchargements de hello spécifié directory tooBlob stockage de manière récursive, c'est-à-dire que tous les sous-dossiers et fichiers seront téléchargés également.</span><span class="sxs-lookup"><span data-stu-id="e1963-149">Specifying option `/S` uploads hello contents of hello specified directory tooBlob storage recursively, meaning that all subfolders and their files will be uploaded as well.</span></span> <span data-ttu-id="e1963-150">Par exemple, supposons que suivant de hello fichiers résident dans le dossier `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="e1963-150">For instance, assume hello following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="e1963-151">Après l’opération de téléchargement de hello, conteneur de hello inclura hello fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="e1963-151">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="e1963-152">Si vous ne spécifiez pas l’option `/S`, AzCopy ne charge pas de manière récursive.</span><span class="sxs-lookup"><span data-stu-id="e1963-152">If you do not specify option `/S`, AzCopy will not upload recursively.</span></span> <span data-ttu-id="e1963-153">Après l’opération de téléchargement de hello, conteneur de hello inclura hello fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="e1963-153">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="e1963-154">Télécharger des fichiers correspondant au modèle spécifié</span><span class="sxs-lookup"><span data-stu-id="e1963-154">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

<span data-ttu-id="e1963-155">Supposons suivant de hello fichiers résident dans le dossier `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="e1963-155">Assume hello following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="e1963-156">Après l’opération de téléchargement de hello, conteneur de hello inclura hello fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="e1963-156">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="e1963-157">Si vous ne spécifiez pas l’option `/S`, AzCopy téléchargera uniquement les objets blob qui ne se trouvent pas dans un répertoire virtuel :</span><span class="sxs-lookup"><span data-stu-id="e1963-157">If you do not specify option `/S`, AzCopy will only upload blobs that don't reside in a virtual directory:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="e1963-158">Spécifiez le type de contenu MIME hello d’un objet blob de destination</span><span class="sxs-lookup"><span data-stu-id="e1963-158">Specify hello MIME content type of a destination blob</span></span>
<span data-ttu-id="e1963-159">Par défaut, AzCopy définit les type de contenu hello d’un objet blob de destination trop`application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="e1963-159">By default, AzCopy sets hello content type of a destination blob too`application/octet-stream`.</span></span> <span data-ttu-id="e1963-160">Depuis la version 3.1.0, vous pouvez spécifier explicitement le type de contenu hello via l’option de hello `/SetContentType:[content-type]`.</span><span class="sxs-lookup"><span data-stu-id="e1963-160">Beginning with version 3.1.0, you can explicitly specify hello content type via hello option `/SetContentType:[content-type]`.</span></span> <span data-ttu-id="e1963-161">Cette syntaxe définit le type de contenu hello pour tous les objets BLOB dans une opération de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="e1963-161">This syntax sets hello content type for all blobs in an upload operation.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

<span data-ttu-id="e1963-162">Si vous spécifiez `/SetContentType` sans valeur, puis AzCopy définit chaque objet blob ou le type de contenu du fichier selon tooits extension de fichier.</span><span class="sxs-lookup"><span data-stu-id="e1963-162">If you specify `/SetContentType` without a value, then AzCopy will set each blob or file's content type according tooits file extension.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a><span data-ttu-id="e1963-163">Objet blob : copie</span><span class="sxs-lookup"><span data-stu-id="e1963-163">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="e1963-164">Copie d’un objet blob unique au sein d’un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="e1963-164">Copy single blob within Storage account</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="e1963-165">Lorsque vous copiez un objet blob au sein d’un compte de stockage, une opération de [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) est exécutée.</span><span class="sxs-lookup"><span data-stu-id="e1963-165">When you copy a blob within a Storage account, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="e1963-166">Copier un objet blob unique sur plusieurs comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="e1963-166">Copy single blob across Storage accounts</span></span>

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="e1963-167">Lorsque vous copiez un objet blob sur plusieurs comptes de stockage, une opération de [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) est exécutée.</span><span class="sxs-lookup"><span data-stu-id="e1963-167">When you copy a blob across Storage accounts, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a><span data-ttu-id="e1963-168">Copier un seul objet blob à partir de la région de tooprimary région secondaire</span><span class="sxs-lookup"><span data-stu-id="e1963-168">Copy single blob from secondary region tooprimary region</span></span>

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="e1963-169">Notez que vous devez avoir un accès en lecture activé pour le stockage géo-redondant.</span><span class="sxs-lookup"><span data-stu-id="e1963-169">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="e1963-170">Copier un objet blob unique et ses captures instantanées sur plusieurs comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="e1963-170">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

<span data-ttu-id="e1963-171">Après l’opération de copie hello, conteneur cible de hello inclura les blob hello et ses instantanés.</span><span class="sxs-lookup"><span data-stu-id="e1963-171">After hello copy operation, hello target container will include hello blob and its snapshots.</span></span> <span data-ttu-id="e1963-172">En supposant que blob hello dans l’exemple hello ci-dessus a deux instantanés, le conteneur de hello inclura hello qui suit blob et captures instantanées :</span><span class="sxs-lookup"><span data-stu-id="e1963-172">Assuming hello blob in hello example above has two snapshots, hello container will include hello following blob and snapshots:</span></span>

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="e1963-173">Copier des objets blob de façon synchrone dans des comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="e1963-173">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="e1963-174">AzCopy copie par défaut les données entre deux points de terminaison de stockage de façon asynchrone.</span><span class="sxs-lookup"><span data-stu-id="e1963-174">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="e1963-175">Par conséquent, opération de copie hello s’exécutera en arrière-plan hello à l’aide de la capacité de la bande passante de rechange avec aucun contrat SLA en termes de rapidité un objet blob doivent être copié et AzCopy vérifie régulièrement l’état de la copie hello jusqu'à ce que la copie de hello est terminée ou a échoué.</span><span class="sxs-lookup"><span data-stu-id="e1963-175">Therefore, hello copy operation will run in hello background using spare bandwidth capacity that has no SLA in terms of how fast a blob will be copied, and AzCopy will periodically check hello copy status until hello copying is completed or failed.</span></span>

<span data-ttu-id="e1963-176">Hello `/SyncCopy` option permet de s’assurer que l’opération de copie hello obtiennent des vitesse cohérente.</span><span class="sxs-lookup"><span data-stu-id="e1963-176">hello `/SyncCopy` option ensures that hello copy operation will get consistent speed.</span></span> <span data-ttu-id="e1963-177">AzCopy effectue la copie synchrone de hello en téléchargeant les objets BLOB de hello toocopy de hello spécifié source toolocal la mémoire et les télécharger la destination de stockage d’objets Blob toohello.</span><span class="sxs-lookup"><span data-stu-id="e1963-177">AzCopy performs hello synchronous copy by downloading hello blobs toocopy from hello specified source toolocal memory, and then uploading them toohello Blob storage destination.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

<span data-ttu-id="e1963-178">`/SyncCopy`peut générer une sortie supplémentaire coût comparés tooasynchronous copie, hello approche recommandée est toouse cette option dans une machine virtuelle Azure qui se trouve dans hello même région que votre coût sortie tooavoid de compte de stockage source.</span><span class="sxs-lookup"><span data-stu-id="e1963-178">`/SyncCopy` might generate additional egress cost compared tooasynchronous copy, hello recommended approach is toouse this option in an Azure VM that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="e1963-179">Fichier : Téléchargement</span><span class="sxs-lookup"><span data-stu-id="e1963-179">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="e1963-180">Télécharger un fichier unique</span><span class="sxs-lookup"><span data-stu-id="e1963-180">Download single file</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="e1963-181">Si hello spécifié source est un partage de fichiers Azure, vous devez spécifier soit le nom de fichier exact hello, (*par exemple,* `abc.txt`) toodownload un seul fichier, ou spécifiez l’option `/S` toodownload tous les fichiers dans le partage de hello récursive.</span><span class="sxs-lookup"><span data-stu-id="e1963-181">If hello specified source is an Azure file share, then you must either specify hello exact file name, (*e.g.* `abc.txt`) toodownload a single file, or specify option `/S` toodownload all files in hello share recursively.</span></span> <span data-ttu-id="e1963-182">Tentative de toospecify un modèle de fichier et l’option `/S` ensemble entraîne une erreur.</span><span class="sxs-lookup"><span data-stu-id="e1963-182">Attempting toospecify both a file pattern and option `/S` together will result in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="e1963-183">Charger tous les fichiers</span><span class="sxs-lookup"><span data-stu-id="e1963-183">Download all files</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="e1963-184">Notez que les dossiers vides ne seront pas téléchargés.</span><span class="sxs-lookup"><span data-stu-id="e1963-184">Note that any empty folders will not be downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="e1963-185">Fichier : Télécharger</span><span class="sxs-lookup"><span data-stu-id="e1963-185">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="e1963-186">Télécharger un fichier unique</span><span class="sxs-lookup"><span data-stu-id="e1963-186">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="e1963-187">Télécharger tous les fichiers</span><span class="sxs-lookup"><span data-stu-id="e1963-187">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

<span data-ttu-id="e1963-188">Notez que les dossiers vides ne sont pas téléchargés.</span><span class="sxs-lookup"><span data-stu-id="e1963-188">Note that any empty folders will not be uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="e1963-189">Télécharger des fichiers correspondant au modèle spécifié</span><span class="sxs-lookup"><span data-stu-id="e1963-189">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a><span data-ttu-id="e1963-190">Fichier : Copier</span><span class="sxs-lookup"><span data-stu-id="e1963-190">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="e1963-191">Copier d’un partage de fichier à l’autre</span><span class="sxs-lookup"><span data-stu-id="e1963-191">Copy across file shares</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="e1963-192">Lorsque vous copiez un fichier sur plusieurs partage de fichiers, une opération de [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) est exécutée.</span><span class="sxs-lookup"><span data-stu-id="e1963-192">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-tooblob"></a><span data-ttu-id="e1963-193">Copier à partir de tooblob de partage de fichier</span><span class="sxs-lookup"><span data-stu-id="e1963-193">Copy from file share tooblob</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="e1963-194">Lorsque vous copiez un fichier à partir du fichier partage tooblob, un [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) opération est effectuée.</span><span class="sxs-lookup"><span data-stu-id="e1963-194">When you copy a file from file share tooblob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>


### <a name="copy-from-blob-toofile-share"></a><span data-ttu-id="e1963-195">Copier à partir du partage de toofile d’objets blob</span><span class="sxs-lookup"><span data-stu-id="e1963-195">Copy from blob toofile share</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="e1963-196">Lorsque vous copiez un fichier à partir d’un partage toofile blob, une [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) opération est effectuée.</span><span class="sxs-lookup"><span data-stu-id="e1963-196">When you copy a file from blob toofile share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="e1963-197">Copier les fichiers de façon synchrone</span><span class="sxs-lookup"><span data-stu-id="e1963-197">Synchronously copy files</span></span>
<span data-ttu-id="e1963-198">Vous pouvez spécifier hello `/SyncCopy` option toocopy des données à partir de tooFile de stockage de fichiers de stockage, de stockage de fichiers tooBlob stockage et de stockage d’objets Blob tooFile stockage de façon synchrone, AzCopy fait cela en téléchargeant mémoire toolocal hello source et le télécharger nouveau toodestination.</span><span class="sxs-lookup"><span data-stu-id="e1963-198">You can specify hello `/SyncCopy` option toocopy data from File Storage tooFile Storage, from File Storage tooBlob Storage and from Blob Storage tooFile Storage synchronously, AzCopy does this by downloading hello source data toolocal memory and upload it again toodestination.</span></span> <span data-ttu-id="e1963-199">Des coûts de sortie standard s’appliquent.</span><span class="sxs-lookup"><span data-stu-id="e1963-199">Standard egress cost will apply.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

<span data-ttu-id="e1963-200">Lors de la copie à partir du stockage de fichiers tooBlob stockage, type d’objet blob hello par défaut est l’objet blob de blocs, utilisateur peut spécifier l’option `/BlobType:page` type d’objet blob destination toochange hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-200">When copying from File Storage tooBlob Storage, hello default blob type is block blob, user can specify option `/BlobType:page` toochange hello destination blob type.</span></span>

<span data-ttu-id="e1963-201">Notez que `/SyncCopy` peut générer des sorties supplémentaires coût comparaison tooasynchronous copie, hello est recommandé de toouse cette option dans hello machine virtuelle Azure qui se trouve dans hello même région que votre coût sortie tooavoid de compte de stockage source.</span><span class="sxs-lookup"><span data-stu-id="e1963-201">Note that `/SyncCopy` might generate additional egress cost comparing tooasynchronous copy, hello recommended approach is toouse this option in hello Azure VM which is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="table-export"></a><span data-ttu-id="e1963-202">Table : Exportation</span><span class="sxs-lookup"><span data-stu-id="e1963-202">Table: Export</span></span>
### <a name="export-table"></a><span data-ttu-id="e1963-203">Table d’exportation</span><span class="sxs-lookup"><span data-stu-id="e1963-203">Export table</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

<span data-ttu-id="e1963-204">AzCopy écrit un dossier de destination spécifié toohello fichier manifeste.</span><span class="sxs-lookup"><span data-stu-id="e1963-204">AzCopy writes a manifest file toohello specified destination folder.</span></span> <span data-ttu-id="e1963-205">fichier de manifeste Hello est utilisé dans les fichiers de données nécessaires du processus toolocate hello hello importation et effectuer la validation des données.</span><span class="sxs-lookup"><span data-stu-id="e1963-205">hello manifest file is used in hello import process toolocate hello necessary data files and perform data validation.</span></span> <span data-ttu-id="e1963-206">fichier de manifeste Hello utilise hello suit la convention d’affectation de noms par défaut :</span><span class="sxs-lookup"><span data-stu-id="e1963-206">hello manifest file uses hello following naming convention by default:</span></span>

    <account name>_<table name>_<timestamp>.manifest

<span data-ttu-id="e1963-207">Utilisateur peut également spécifier hello option `/Manifest:<manifest file name>` nom du fichier manifeste tooset hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-207">User can also specify hello option `/Manifest:<manifest file name>` tooset hello manifest file name.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a><span data-ttu-id="e1963-208">Fractionnement de l’exportation en plusieurs fichiers</span><span class="sxs-lookup"><span data-stu-id="e1963-208">Split export into multiple files</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

<span data-ttu-id="e1963-209">AzCopy utilise un *index de volume* Bonjour fractionner les données de noms de fichier toodistinguish plusieurs fichiers.</span><span class="sxs-lookup"><span data-stu-id="e1963-209">AzCopy uses a *volume index* in hello split data file names toodistinguish multiple files.</span></span> <span data-ttu-id="e1963-210">index de volume Hello se compose de deux parties, un *index de plage de clés de partition* et un *fractionnement fichier index*.</span><span class="sxs-lookup"><span data-stu-id="e1963-210">hello volume index consists of two parts, a *partition key range index* and a *split file index*.</span></span> <span data-ttu-id="e1963-211">Ces deux index commencent à zéro.</span><span class="sxs-lookup"><span data-stu-id="e1963-211">Both indexes are zero-based.</span></span>

<span data-ttu-id="e1963-212">index de plage de clés de partition Hello est égal à 0 si l’utilisateur ne spécifie pas d’option `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="e1963-212">hello partition key range index will be 0 if user does not specify option `/PKRS`.</span></span>

<span data-ttu-id="e1963-213">Par exemple, supposons que AzCopy génère deux fichiers de données une fois que l’utilisateur de hello Spécifie l’option `/SplitSize`.</span><span class="sxs-lookup"><span data-stu-id="e1963-213">For instance, suppose AzCopy generates two data files after hello user specifies option `/SplitSize`.</span></span> <span data-ttu-id="e1963-214">Hello, ce qui entraîne des noms de fichiers de données peut être :</span><span class="sxs-lookup"><span data-stu-id="e1963-214">hello resulting data file names might be:</span></span>

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

<span data-ttu-id="e1963-215">Notez que hello minimale possible pour l’option `/SplitSize` est 32 Mo.</span><span class="sxs-lookup"><span data-stu-id="e1963-215">Note that hello minimum possible value for option `/SplitSize` is 32MB.</span></span> <span data-ttu-id="e1963-216">Si hello spécifié d’une destination de stockage d’objets Blob, AzCopy est fractionné de fichier de données hello une fois sa limite de taille de blob tailles atteint hello (200 Go), indépendamment de si l’option `/SplitSize` a été spécifié par l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-216">If hello specified destination is Blob storage, AzCopy will split hello data file once its sizes reaches hello blob size limitation (200GB), regardless of whether option `/SplitSize` has been specified by hello user.</span></span>

### <a name="export-table-toojson-or-csv-data-file-format"></a><span data-ttu-id="e1963-217">Exporter la table tooJSON ou format de fichier de données CSV</span><span class="sxs-lookup"><span data-stu-id="e1963-217">Export table tooJSON or CSV data file format</span></span>
<span data-ttu-id="e1963-218">AzCopy par défaut exporte des fichiers de données de tables tooJSON.</span><span class="sxs-lookup"><span data-stu-id="e1963-218">AzCopy by default exports tables tooJSON data files.</span></span> <span data-ttu-id="e1963-219">Vous pouvez spécifier hello option `/PayloadFormat:JSON|CSV` tooexport les tables de hello en tant que JSON ou CSV.</span><span class="sxs-lookup"><span data-stu-id="e1963-219">You can specify hello option `/PayloadFormat:JSON|CSV` tooexport hello tables as JSON or CSV.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

<span data-ttu-id="e1963-220">Lors de la spécification de format de charge utile hello CSV, AzCopy génère également un fichier de schéma avec l’extension de fichier `.schema.csv` pour chaque fichier de données.</span><span class="sxs-lookup"><span data-stu-id="e1963-220">When specifying hello CSV payload format, AzCopy will also generate a schema file with file extension `.schema.csv` for each data file.</span></span>

### <a name="export-table-entities-concurrently"></a><span data-ttu-id="e1963-221">Exportation simultanée d’entités de table</span><span class="sxs-lookup"><span data-stu-id="e1963-221">Export table entities concurrently</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

<span data-ttu-id="e1963-222">AzCopy démarre les entités tooexport opérations simultanées lors de l’utilisateur de hello Spécifie l’option `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="e1963-222">AzCopy will start concurrent operations tooexport entities when hello user specifies option `/PKRS`.</span></span> <span data-ttu-id="e1963-223">Chaque opération exporte une plage de clés de partition.</span><span class="sxs-lookup"><span data-stu-id="e1963-223">Each operation exports one partition key range.</span></span>

<span data-ttu-id="e1963-224">Notez que hello nombre d’opérations simultanées est également contrôlé par l’option `/NC`.</span><span class="sxs-lookup"><span data-stu-id="e1963-224">Note that hello number of concurrent operations is also controlled by option `/NC`.</span></span> <span data-ttu-id="e1963-225">AzCopy utilise le nombre de hello de processeurs de base comme valeur par défaut hello `/NC` lors de la copie des entités de table, même si `/NC` n’a été spécifié.</span><span class="sxs-lookup"><span data-stu-id="e1963-225">AzCopy uses hello number of core processors as hello default value of `/NC` when copying table entities, even if `/NC` was not specified.</span></span> <span data-ttu-id="e1963-226">Lorsque les utilisateur hello spécifie option `/PKRS`, AzCopy utilise hello plus petit nombre hello deux valeurs - partition plages de clés par rapport aux opérations simultanées implicitement ou explicitement spécifiées - toodetermine hello de toostart des opérations simultanées.</span><span class="sxs-lookup"><span data-stu-id="e1963-226">When hello user specifies option `/PKRS`, AzCopy uses hello smaller of hello two values - partition key ranges versus implicitly or explicitly specified concurrent operations - toodetermine hello number of concurrent operations toostart.</span></span> <span data-ttu-id="e1963-227">Pour plus d’informations, tapez `AzCopy /?:NC` à la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-227">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

### <a name="export-table-tooblob"></a><span data-ttu-id="e1963-228">Exporter la table tooblob</span><span class="sxs-lookup"><span data-stu-id="e1963-228">Export table tooblob</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

<span data-ttu-id="e1963-229">AzCopy génère un fichier de données JSON dans un conteneur d’objets blob hello avec suivant la convention d’affectation de noms :</span><span class="sxs-lookup"><span data-stu-id="e1963-229">AzCopy will generate a JSON data file into hello blob container with following naming convention:</span></span>

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

<span data-ttu-id="e1963-230">fichier de données JSON Hello généré suit le format de charge utile hello pour les métadonnées minimales.</span><span class="sxs-lookup"><span data-stu-id="e1963-230">hello generated JSON data file follows hello payload format for minimal metadata.</span></span> <span data-ttu-id="e1963-231">Pour des informations sur le format de charge utile, consultez la page [Format de charge utile pour les opérations du service de Table](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span><span class="sxs-lookup"><span data-stu-id="e1963-231">For details on this payload format, see [Payload Format for Table Service Operations](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span></span>

<span data-ttu-id="e1963-232">Notez que lorsque vous exportez des tables tooblobs, AzCopy télécharger les fichiers de données temporaires hello Table entités toolocal et puis télécharger les blob de toohello d’entités.</span><span class="sxs-lookup"><span data-stu-id="e1963-232">Note that when exporting tables tooblobs, AzCopy will download hello Table entities toolocal temporary data files and then upload those entities toohello blob.</span></span> <span data-ttu-id="e1963-233">Ces fichiers de données temporaires sont placés dans le dossier de fichier journal hello avec le chemin d’accès de hello par défaut «<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>», vous pouvez spécifier d’option/Z: [dossier de fichier journal] toochange hello d’emplacement de dossier du fichier journal et ainsi modifier emplacement de fichiers de données temporaires hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-233">These temporary data files are put into hello journal file folder with hello default path "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", you can specify option /Z:[journal-file-folder] toochange hello journal file folder location and thus change hello temporary data files location.</span></span> <span data-ttu-id="e1963-234">Hello données temporaires de taille des fichiers est décidée par des entités de votre table taille et taille hello spécifiée avec hello option /SplitSize, bien que le fichier de données temporaires hello disque local sera supprimé instantanément dès qu’il a été téléchargement toohello blob, assurez-vous que vous avoir suffisamment toostore d’espace disque local de ces fichiers de données temporaire avant d’être supprimés.</span><span class="sxs-lookup"><span data-stu-id="e1963-234">hello temporary data files' size is decided by your table entities' size and hello size you specified with hello option /SplitSize, although hello temporary data file in local disk will be deleted instantly once it has been uploaded toohello blob, please make sure you have enough local disk space toostore these temporary data files before they are deleted.</span></span>

## <a name="table-import"></a><span data-ttu-id="e1963-235">Table : importation</span><span class="sxs-lookup"><span data-stu-id="e1963-235">Table: Import</span></span>
### <a name="import-table"></a><span data-ttu-id="e1963-236">Table d’importation</span><span class="sxs-lookup"><span data-stu-id="e1963-236">Import table</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

<span data-ttu-id="e1963-237">Hello option `/EntityOperation` indique la façon dont les entités tooinsert dans hello table.</span><span class="sxs-lookup"><span data-stu-id="e1963-237">hello option `/EntityOperation` indicates how tooinsert entities into hello table.</span></span> <span data-ttu-id="e1963-238">Les valeurs possibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="e1963-238">Possible values are:</span></span>

* <span data-ttu-id="e1963-239">`InsertOrSkip`: Ignore une entité existante ou insère une nouvelle entité si elle n’existe pas dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-239">`InsertOrSkip`: Skips an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="e1963-240">`InsertOrMerge`: Fusionne une entité existante ou insère une nouvelle entité si elle n’existe pas dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-240">`InsertOrMerge`: Merges an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="e1963-241">`InsertOrReplace`: Remplace une entité existante ou insère une nouvelle entité si elle n’existe pas dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-241">`InsertOrReplace`: Replaces an existing entity or inserts a new entity if it does not exist in hello table.</span></span>

<span data-ttu-id="e1963-242">Notez que vous ne pouvez pas spécifier d’option `/PKRS` dans le scénario d’importation hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-242">Note that you cannot specify option `/PKRS` in hello import scenario.</span></span> <span data-ttu-id="e1963-243">Contrairement au scénario d’exportation hello, dans laquelle vous devez spécifier option `/PKRS` toostart des opérations simultanées, AzCopy par défaut démarre des opérations simultanées lorsque vous importez une table.</span><span class="sxs-lookup"><span data-stu-id="e1963-243">Unlike hello export scenario, in which you must specify option `/PKRS` toostart concurrent operations, AzCopy will by default start concurrent operations when you import a table.</span></span> <span data-ttu-id="e1963-244">nombre d’opérations simultanées démarré par défaut de Hello est nombre égal toohello de processeurs de base ; Toutefois, vous pouvez spécifier un nombre différent de simultanées avec l’option `/NC`.</span><span class="sxs-lookup"><span data-stu-id="e1963-244">hello default number of concurrent operations started is equal toohello number of core processors; however, you can specify a different number of concurrent with option `/NC`.</span></span> <span data-ttu-id="e1963-245">Pour plus d’informations, tapez `AzCopy /?:NC` à la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-245">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

<span data-ttu-id="e1963-246">Notez qu’AzCopy ne prend en charge que l’importation pour JSON, et non CSV.</span><span class="sxs-lookup"><span data-stu-id="e1963-246">Note that AzCopy only supports importing for JSON, not CSV.</span></span> <span data-ttu-id="e1963-247">AzCopy ne prend pas en charge les importations de table à partir de fichiers JSON créés par l’utilisateur et de fichiers manifeste.</span><span class="sxs-lookup"><span data-stu-id="e1963-247">AzCopy does not support table imports from user-created JSON and manifest files.</span></span> <span data-ttu-id="e1963-248">Ces deux types de fichiers doivent provenir d’une exportation de table AzCopy.</span><span class="sxs-lookup"><span data-stu-id="e1963-248">Both of these files must come from an AzCopy table export.</span></span> <span data-ttu-id="e1963-249">erreurs de tooavoid, ne modifiez pas hello exportée JSON ou un fichier manifeste.</span><span class="sxs-lookup"><span data-stu-id="e1963-249">tooavoid errors, please do not modify hello exported JSON or manifest file.</span></span>

### <a name="import-entities-tootable-using-blobs"></a><span data-ttu-id="e1963-250">Importer les entités tootable à l’aide d’objets BLOB</span><span class="sxs-lookup"><span data-stu-id="e1963-250">Import entities tootable using blobs</span></span>
<span data-ttu-id="e1963-251">Supposons qu’un conteneur d’objets Blob contient suivant de hello : fichier JSON d’un représentant une Table Azure et son fichier manifeste associé.</span><span class="sxs-lookup"><span data-stu-id="e1963-251">Assume a Blob container contains hello following: A JSON file representing an Azure Table and its accompanying manifest file.</span></span>

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

<span data-ttu-id="e1963-252">Vous pouvez exécuter hello suivant entités tooimport de commande dans une table à l’aide du fichier de manifeste hello dans ce conteneur d’objets blob :</span><span class="sxs-lookup"><span data-stu-id="e1963-252">You can run hello following command tooimport entities into a table using hello manifest file in that blob container:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a><span data-ttu-id="e1963-253">Autres fonctionnalités AzCopy</span><span class="sxs-lookup"><span data-stu-id="e1963-253">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a><span data-ttu-id="e1963-254">Copier uniquement les données qui n’existent pas dans la destination de hello</span><span class="sxs-lookup"><span data-stu-id="e1963-254">Only copy data that doesn't exist in hello destination</span></span>
<span data-ttu-id="e1963-255">Hello `/XO` et `/XN` paramètres vous permettent de tooexclude des ressources de source ancien ou plus récent à partir de la copie, respectivement.</span><span class="sxs-lookup"><span data-stu-id="e1963-255">hello `/XO` and `/XN` parameters allow you tooexclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="e1963-256">Si vous souhaitez uniquement les ressources de la source toocopy qui n’existent pas dans la destination de hello, vous pouvez spécifier les deux paramètres Bonjour AzCopy commande :</span><span class="sxs-lookup"><span data-stu-id="e1963-256">If you only want toocopy source resources that don't exist in hello destination, you can specify both parameters in hello AzCopy command:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

<span data-ttu-id="e1963-257">Notez que cela n'est pas pris en charge lorsque hello source ou destination est une table.</span><span class="sxs-lookup"><span data-stu-id="e1963-257">Note that this is not supported when either hello source or destination is a table.</span></span>

### <a name="use-a-response-file-toospecify-command-line-parameters"></a><span data-ttu-id="e1963-258">Utiliser un paramètres de ligne de commande toospecify du fichier de réponse</span><span class="sxs-lookup"><span data-stu-id="e1963-258">Use a response file toospecify command-line parameters</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

<span data-ttu-id="e1963-259">Vous pouvez inclure n’importe quels paramètres de ligne de commande AzCopy dans un fichier réponse.</span><span class="sxs-lookup"><span data-stu-id="e1963-259">You can include any AzCopy command-line parameters in a response file.</span></span> <span data-ttu-id="e1963-260">AzCopy processus hello paramètres hello fichier comme s’ils avaient été spécifiés sur la ligne de commande hello, effectuer une substitution directe avec le contenu de hello du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-260">AzCopy processes hello parameters in hello file as if they had been specified on hello command line, performing a direct substitution with hello contents of hello file.</span></span>

<span data-ttu-id="e1963-261">Supposons un fichier de réponse nommé `copyoperation.txt`, qui contient les lignes suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-261">Assume a response file named `copyoperation.txt`, that contains hello following lines.</span></span> <span data-ttu-id="e1963-262">Chaque paramètre AzCopy peut être spécifié sur une seule ligne</span><span class="sxs-lookup"><span data-stu-id="e1963-262">Each AzCopy parameter can be specified on a single line</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

<span data-ttu-id="e1963-263">ou sur des lignes distinctes :</span><span class="sxs-lookup"><span data-stu-id="e1963-263">or on separate lines:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

<span data-ttu-id="e1963-264">AzCopy échoue si vous fractionnez le paramètre hello entre deux lignes, comme indiqué ici pour hello `/sourcekey` paramètre :</span><span class="sxs-lookup"><span data-stu-id="e1963-264">AzCopy will fail if you split hello parameter across two lines, as shown here for hello `/sourcekey` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-toospecify-command-line-parameters"></a><span data-ttu-id="e1963-265">Utilisation de plusieurs paramètres de ligne de commande réponse fichiers toospecify</span><span class="sxs-lookup"><span data-stu-id="e1963-265">Use multiple response files toospecify command-line parameters</span></span>
<span data-ttu-id="e1963-266">Si un fichier réponse dénommé `source.txt` qui spécifie un conteneur source :</span><span class="sxs-lookup"><span data-stu-id="e1963-266">Assume a response file named `source.txt` that specifies a source container:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer

<span data-ttu-id="e1963-267">Et un fichier de réponse nommé `dest.txt` qui spécifie un dossier de destination dans le système de fichiers hello :</span><span class="sxs-lookup"><span data-stu-id="e1963-267">And a response file named `dest.txt` that specifies a destination folder in hello file system:</span></span>

    /Dest:C:\myfolder

<span data-ttu-id="e1963-268">Et un fichier réponse nommé `options.txt` qui spécifie les options pour AzCopy :</span><span class="sxs-lookup"><span data-stu-id="e1963-268">And a response file named `options.txt` that specifies options for AzCopy:</span></span>

    /S /Y

<span data-ttu-id="e1963-269">toocall AzCopy de ces fichiers de réponse, qui se trouvent dans un répertoire `C:\responsefiles`, utilisez la commande :</span><span class="sxs-lookup"><span data-stu-id="e1963-269">toocall AzCopy with these response files, all of which reside in a directory `C:\responsefiles`, use this command:</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

<span data-ttu-id="e1963-270">AzCopy traite cette commande, comme il le ferait si vous avez inclus tous les paramètres individuels de hello sur la ligne de commande hello :</span><span class="sxs-lookup"><span data-stu-id="e1963-270">AzCopy processes this command just as it would if you included all of hello individual parameters on hello command line:</span></span>

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="e1963-271">Spécification d’une signature d’accès partagé (SAP)</span><span class="sxs-lookup"><span data-stu-id="e1963-271">Specify a shared access signature (SAS)</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

<span data-ttu-id="e1963-272">Vous pouvez également spécifier une SAP sur l’URI du conteneur hello :</span><span class="sxs-lookup"><span data-stu-id="e1963-272">You can also specify a SAS on hello container URI:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a><span data-ttu-id="e1963-273">Dossier du fichier journal</span><span class="sxs-lookup"><span data-stu-id="e1963-273">Journal file folder</span></span>
<span data-ttu-id="e1963-274">Chaque fois que vous exécutez une commande tooAzCopy, il vérifie si un fichier journal existe dans le dossier par défaut de hello, ou si elle existe dans un dossier que vous avez spécifié à l’aide de cette option.</span><span class="sxs-lookup"><span data-stu-id="e1963-274">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="e1963-275">Si le fichier journal de hello n’existe pas à cet emplacement, AzCopy traite l’opération de hello en tant que nouvelle et génère un nouveau fichier journal.</span><span class="sxs-lookup"><span data-stu-id="e1963-275">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="e1963-276">Si le fichier journal de hello existe, AzCopy vérifiera si ligne de commande hello que vous avez entré correspond à la ligne de commande hello dans un fichier de journal hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-276">If hello journal file does exist, AzCopy will check whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="e1963-277">Si les deux lignes de commande hello correspondent, AzCopy reprend les opérations d’incomplète hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-277">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="e1963-278">Si elles ne correspondent pas, vous serez tooeither invité à remplacer hello journal fichier toostart une nouvelle opération ou toocancel hello opération en cours.</span><span class="sxs-lookup"><span data-stu-id="e1963-278">If they do not match, you will be prompted tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="e1963-279">Si vous souhaitez toouse hello emplacement par défaut hello journal fichier :</span><span class="sxs-lookup"><span data-stu-id="e1963-279">If you want toouse hello default location for hello journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

<span data-ttu-id="e1963-280">Si vous omettez l’option `/Z`, ou spécifiez l’option `/Z` sans chemin d’accès du dossier hello, comme indiqué ci-dessus, AzCopy crée hello journal fichier dans l’emplacement par défaut hello, qui est `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="e1963-280">If you omit option `/Z`, or specify option `/Z` without hello folder path, as shown above, AzCopy creates hello journal file in hello default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="e1963-281">Si le fichier journal de hello existe déjà, AzCopy reprend les opérations de hello basée sur le fichier journal de hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-281">If hello journal file already exists, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="e1963-282">Si vous souhaitez toospecify un emplacement personnalisé pour le fichier journal de hello :</span><span class="sxs-lookup"><span data-stu-id="e1963-282">If you want toospecify a custom location for hello journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

<span data-ttu-id="e1963-283">Cet exemple crée le fichier journal de hello si elle n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="e1963-283">This example creates hello journal file if it does not already exist.</span></span> <span data-ttu-id="e1963-284">S’il n’existe pas, AzCopy reprend les opérations de hello basée sur le fichier journal de hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-284">If it does exist, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="e1963-285">Si vous souhaitez tooresume une opération AzCopy :</span><span class="sxs-lookup"><span data-stu-id="e1963-285">If you want tooresume an AzCopy operation:</span></span>

```azcopy
AzCopy /Z:C:\journalfolder\
```

<span data-ttu-id="e1963-286">Cet exemple reprend hello dernière opération, ce qui peut avoir échoué toocomplete.</span><span class="sxs-lookup"><span data-stu-id="e1963-286">This example resumes hello last operation, which may have failed toocomplete.</span></span>

### <a name="generate-a-log-file"></a><span data-ttu-id="e1963-287">Génération d’un fichier journal</span><span class="sxs-lookup"><span data-stu-id="e1963-287">Generate a log file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

<span data-ttu-id="e1963-288">Si vous spécifiez l’option `/V` sans fournir un journal détaillé de fichier chemin d’accès toohello, puis AzCopy crée hello fichier journal dans l’emplacement par défaut hello, qui est `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="e1963-288">If you specify option `/V` without providing a file path toohello verbose log, then AzCopy creates hello log file in hello default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span>

<span data-ttu-id="e1963-289">Autrement, vous pouvez créer un fichier journal dans un emplacement personnalisé :</span><span class="sxs-lookup"><span data-stu-id="e1963-289">Otherwise, you can create an log file in a custom location:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

<span data-ttu-id="e1963-290">Notez que si vous spécifiez un chemin d’accès relatif suivant option `/V`, tel que `/V:test/azcopy1.log`, la journalisation documentée hello est alors créé dans le répertoire de travail actuel hello dans un sous-dossier nommé `test`.</span><span class="sxs-lookup"><span data-stu-id="e1963-290">Note that if you specify a relative path following option `/V`, such as `/V:test/azcopy1.log`, then hello verbose log is created in hello current working directory within a subfolder named `test`.</span></span>

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a><span data-ttu-id="e1963-291">Spécifiez le nombre hello d’opérations simultanées toostart</span><span class="sxs-lookup"><span data-stu-id="e1963-291">Specify hello number of concurrent operations toostart</span></span>
<span data-ttu-id="e1963-292">Option `/NC` Spécifie le nombre de hello d’opérations de copie simultanées.</span><span class="sxs-lookup"><span data-stu-id="e1963-292">Option `/NC` specifies hello number of concurrent copy operations.</span></span> <span data-ttu-id="e1963-293">Par défaut, AzCopy démarre un certain nombre de débit de transfert de données des opérations simultanées tooincrease hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-293">By default, AzCopy starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="e1963-294">Pour les opérations de Table, nombre hello d’opérations simultanées est nombre égal toohello de processeurs que vous avez.</span><span class="sxs-lookup"><span data-stu-id="e1963-294">For Table operations, hello number of concurrent operations is equal toohello number of processors you have.</span></span> <span data-ttu-id="e1963-295">Pour les opérations Blob et de fichier, nombre hello d’opérations simultanées est égal à nombre de hello de 8 heures de processeurs que vous avez.</span><span class="sxs-lookup"><span data-stu-id="e1963-295">For Blob and File operations, hello number of concurrent operations is equal 8 times hello number of processors you have.</span></span> <span data-ttu-id="e1963-296">Si vous exécutez AzCopy sur un réseau à faible bande passante, vous pouvez spécifier une valeur inférieure pour le paramètre/NC tooavoid a échoué en concurrence de la ressource.</span><span class="sxs-lookup"><span data-stu-id="e1963-296">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for /NC tooavoid failure caused by resource competition.</span></span>

### <a name="run-azcopy-against-azure-storage-emulator"></a><span data-ttu-id="e1963-297">Exécutez AzCopy sur l’émulateur de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="e1963-297">Run AzCopy against Azure Storage Emulator</span></span>
<span data-ttu-id="e1963-298">Vous pouvez exécuter AzCopy pour hello [émulateur de stockage Azure](storage-use-emulator.md) pour les objets BLOB :</span><span class="sxs-lookup"><span data-stu-id="e1963-298">You can run AzCopy against hello [Azure Storage Emulator](storage-use-emulator.md) for Blobs:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

<span data-ttu-id="e1963-299">et les tables :</span><span class="sxs-lookup"><span data-stu-id="e1963-299">and Tables:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a><span data-ttu-id="e1963-300">Paramètres AzCopy</span><span class="sxs-lookup"><span data-stu-id="e1963-300">AzCopy Parameters</span></span>
<span data-ttu-id="e1963-301">Les paramètres d’AzCopy sont décrits ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e1963-301">Parameters for AzCopy are described below.</span></span> <span data-ttu-id="e1963-302">Vous pouvez également taper une des hello suivant les commandes à partir de la ligne de commande hello pour vous aider à l’aide de AzCopy :</span><span class="sxs-lookup"><span data-stu-id="e1963-302">You can also type one of hello following commands from hello command line for help in using AzCopy:</span></span>

* <span data-ttu-id="e1963-303">Pour l'aide détaillée sur la ligne de commande AzCopy : `AzCopy /?`</span><span class="sxs-lookup"><span data-stu-id="e1963-303">For detailed command-line help for AzCopy: `AzCopy /?`</span></span>
* <span data-ttu-id="e1963-304">Pour l'aide détaillée sur un paramètre AzCopy : `AzCopy /?:SourceKey`</span><span class="sxs-lookup"><span data-stu-id="e1963-304">For detailed help with any AzCopy parameter: `AzCopy /?:SourceKey`</span></span>
* <span data-ttu-id="e1963-305">Pour des exemples de ligne de commande : `AzCopy /?:Samples`</span><span class="sxs-lookup"><span data-stu-id="e1963-305">For command-line examples: `AzCopy /?:Samples`</span></span>

### <a name="sourcesource"></a><span data-ttu-id="e1963-306">/Source:"source"</span><span class="sxs-lookup"><span data-stu-id="e1963-306">/Source:"source"</span></span>
<span data-ttu-id="e1963-307">Spécifie les données de source de hello à partir de quels toocopy.</span><span class="sxs-lookup"><span data-stu-id="e1963-307">Specifies hello source data from which toocopy.</span></span> <span data-ttu-id="e1963-308">Hello source peut être un répertoire de système de fichiers, un conteneur d’objets blob, un répertoire virtuel d’objets blob, un partage de fichiers de stockage, un répertoire de fichiers de stockage ou une table Azure.</span><span class="sxs-lookup"><span data-stu-id="e1963-308">hello source can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="e1963-309">**S’applique à :** objets blob, fichiers, tables</span><span class="sxs-lookup"><span data-stu-id="e1963-309">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destdestination"></a><span data-ttu-id="e1963-310">/Dest:"destination"</span><span class="sxs-lookup"><span data-stu-id="e1963-310">/Dest:"destination"</span></span>
<span data-ttu-id="e1963-311">Spécifie les toocopy de destination hello pour.</span><span class="sxs-lookup"><span data-stu-id="e1963-311">Specifies hello destination toocopy to.</span></span> <span data-ttu-id="e1963-312">Hello destination peut être un répertoire de système de fichiers, un conteneur d’objets blob, un répertoire virtuel d’objets blob, un partage de fichiers de stockage, un répertoire de fichiers de stockage ou une table Azure.</span><span class="sxs-lookup"><span data-stu-id="e1963-312">hello destination can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="e1963-313">**S’applique à :** objets blob, fichiers, tables</span><span class="sxs-lookup"><span data-stu-id="e1963-313">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="patternfile-pattern"></a><span data-ttu-id="e1963-314">/Pattern:"file-pattern"</span><span class="sxs-lookup"><span data-stu-id="e1963-314">/Pattern:"file-pattern"</span></span>
<span data-ttu-id="e1963-315">Spécifie un modèle de fichier qui indique quel toocopy de fichiers.</span><span class="sxs-lookup"><span data-stu-id="e1963-315">Specifies a file pattern that indicates which files toocopy.</span></span> <span data-ttu-id="e1963-316">comportement de Hello du paramètre de /Pattern hello est déterminé par emplacement hello de source de données hello et présence hello de l’option de mode hello récursive.</span><span class="sxs-lookup"><span data-stu-id="e1963-316">hello behavior of hello /Pattern parameter is determined by hello location of hello source data, and hello presence of hello recursive mode option.</span></span> <span data-ttu-id="e1963-317">Le mode récursif est spécifié via l’option /S.</span><span class="sxs-lookup"><span data-stu-id="e1963-317">Recursive mode is specified via option /S.</span></span>

<span data-ttu-id="e1963-318">Si la source spécifiée de hello est un répertoire dans le système de fichiers hello, des caractères génériques standard sont en vigueur et le modèle de fichier hello fourni est mis en correspondance avec les fichiers dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-318">If hello specified source is a directory in hello file system, then standard wildcards are in effect, and hello file pattern provided is matched against files within hello directory.</span></span> <span data-ttu-id="e1963-319">Si l’option que /s est spécifié, puis AzCopy correspond également à modèle spécifié de hello sur tous les fichiers dans les sous-dossiers sous le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-319">If option /S is specified, then AzCopy also matches hello specified pattern against all files in any subfolders beneath hello directory.</span></span>

<span data-ttu-id="e1963-320">Si la source spécifiée de hello est un conteneur d’objets blob ou le répertoire virtuel, les caractères génériques ne sont pas appliquées.</span><span class="sxs-lookup"><span data-stu-id="e1963-320">If hello specified source is a blob container or virtual directory, then wildcards are not applied.</span></span> <span data-ttu-id="e1963-321">Si l’option que /s est spécifié, puis AzCopy interprète un modèle de fichier spécifié hello comme un préfixe d’objet blob.</span><span class="sxs-lookup"><span data-stu-id="e1963-321">If option /S is specified, then AzCopy interprets hello specified file pattern as a blob prefix.</span></span> <span data-ttu-id="e1963-322">Si l’option que /s n’est pas spécifié, puis AzCopy correspond au modèle de fichier de hello par rapport aux noms d’objets blob exacte.</span><span class="sxs-lookup"><span data-stu-id="e1963-322">If option /S is not specified, then AzCopy matches hello file pattern against exact blob names.</span></span>

<span data-ttu-id="e1963-323">Si hello spécifié source est un partage de fichiers Azure, vous devez spécifier soit le nom de fichier exact hello, (par exemple, abc.txt) toocopy un seul fichier, ou spécifiez option /S toocopy tous les fichiers dans le partage de hello de manière récursive.</span><span class="sxs-lookup"><span data-stu-id="e1963-323">If hello specified source is an Azure file share, then you must either specify hello exact file name, (e.g. abc.txt) toocopy a single file, or specify option /S toocopy all files in hello share recursively.</span></span> <span data-ttu-id="e1963-324">Toute tentative toospecify un modèle de fichier et l’option /S ensemble entraîne une erreur.</span><span class="sxs-lookup"><span data-stu-id="e1963-324">Attempting toospecify both a file pattern and option /S together will result in an error.</span></span>

<span data-ttu-id="e1963-325">AzCopy utilise la correspondance qui respecte la casse lorsque hello/source est un conteneur d’objets blob ou le répertoire virtuel d’objets blob, et utilise la casse dans toutes les hello autres cas.</span><span class="sxs-lookup"><span data-stu-id="e1963-325">AzCopy uses case-sensitive matching when hello /Source is a blob container or blob virtual directory, and uses case-insensitive matching in all hello other cases.</span></span>

<span data-ttu-id="e1963-326">Hello modèle de fichier par défaut utilisé lorsqu’aucun modèle de fichier n’est spécifié est *.*</span><span class="sxs-lookup"><span data-stu-id="e1963-326">hello default file pattern used when no file pattern is specified is *.*</span></span> <span data-ttu-id="e1963-327">pour un emplacement de système de fichiers, ou un préfixe vide pour un emplacement Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="e1963-327">for a file system location or an empty prefix for an Azure Storage location.</span></span> <span data-ttu-id="e1963-328">La spécification de plusieurs modèles de fichiers n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="e1963-328">Specifying multiple file patterns is not supported.</span></span>

<span data-ttu-id="e1963-329">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="e1963-329">**Applicable to:** Blobs, Files</span></span>

### <a name="destkeystorage-key"></a><span data-ttu-id="e1963-330">/DestKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="e1963-330">/DestKey:"storage-key"</span></span>
<span data-ttu-id="e1963-331">Spécifie la clé de compte de stockage hello pour la ressource de destination hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-331">Specifies hello storage account key for hello destination resource.</span></span>

<span data-ttu-id="e1963-332">**S’applique à :** objets blob, fichiers, tables</span><span class="sxs-lookup"><span data-stu-id="e1963-332">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destsassas-token"></a><span data-ttu-id="e1963-333">/DestSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="e1963-333">/DestSAS:"sas-token"</span></span>
<span data-ttu-id="e1963-334">Spécifie une Signature d’accès partagé (SAS) avec des autorisations de lecture et d’écriture pour la destination de hello (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="e1963-334">Specifies a Shared Access Signature (SAS) with READ and WRITE permissions for hello destination (if applicable).</span></span> <span data-ttu-id="e1963-335">Hello surround SAS de doubles guillemets, telle qu’elle peut contient des caractères spéciaux de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="e1963-335">Surround hello SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="e1963-336">Si la ressource de destination hello est un conteneur d’objets blob, partage de fichiers ou une table, vous pouvez spécifier cette option de suivi d’un jeton SAS hello, ou vous pouvez spécifier hello SAP en tant que partie du conteneur d’objets blob de destination de hello, partage de fichiers ou un URI de la table, sans cette option.</span><span class="sxs-lookup"><span data-stu-id="e1963-336">If hello destination resource is a blob container, file share or table, you can either specify this option followed by hello SAS token, or you can specify hello SAS as part of hello destination blob container, file share or table's URI, without this option.</span></span>

<span data-ttu-id="e1963-337">Si hello source et destination sont les deux objets BLOB, objet blob de destination hello doit résider dans hello même compte de stockage en tant qu’objet blob source de hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-337">If hello source and destination are both blobs, then hello destination blob must reside within hello same storage account as hello source blob.</span></span>

<span data-ttu-id="e1963-338">**S’applique à :** objets blob, fichiers, tables</span><span class="sxs-lookup"><span data-stu-id="e1963-338">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcekeystorage-key"></a><span data-ttu-id="e1963-339">/SourceKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="e1963-339">/SourceKey:"storage-key"</span></span>
<span data-ttu-id="e1963-340">Spécifie la clé de compte de stockage hello pour la ressource de source de hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-340">Specifies hello storage account key for hello source resource.</span></span>

<span data-ttu-id="e1963-341">**S’applique à :** objets blob, fichiers, tables</span><span class="sxs-lookup"><span data-stu-id="e1963-341">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcesassas-token"></a><span data-ttu-id="e1963-342">/SourceSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="e1963-342">/SourceSAS:"sas-token"</span></span>
<span data-ttu-id="e1963-343">Spécifie une Signature d’accès partagé avec les autorisations de lecture et de la liste pour la source de hello (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="e1963-343">Specifies a Shared Access Signature with READ and LIST permissions for hello source (if applicable).</span></span> <span data-ttu-id="e1963-344">Hello surround SAS de doubles guillemets, telle qu’elle peut contient des caractères spéciaux de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="e1963-344">Surround hello SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="e1963-345">Si la ressource de source de hello est un conteneur d’objets blob, et une clé, ni une SAP est fournie, conteneur d’objets blob hello est lues via l’accès anonyme.</span><span class="sxs-lookup"><span data-stu-id="e1963-345">If hello source resource is a blob container, and neither a key nor a SAS is provided, then hello blob container will be read via anonymous access.</span></span>

<span data-ttu-id="e1963-346">Si la source de hello est un partage de fichiers ou une table, une clé ou une SAP doit être fournie.</span><span class="sxs-lookup"><span data-stu-id="e1963-346">If hello source is a file share or table, a key or a SAS must be provided.</span></span>

<span data-ttu-id="e1963-347">**S’applique à :** objets blob, fichiers, tables</span><span class="sxs-lookup"><span data-stu-id="e1963-347">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="s"></a><span data-ttu-id="e1963-348">/S</span><span class="sxs-lookup"><span data-stu-id="e1963-348">/S</span></span>
<span data-ttu-id="e1963-349">Spécifie le mode récursif pour les opérations de copie.</span><span class="sxs-lookup"><span data-stu-id="e1963-349">Specifies recursive mode for copy operations.</span></span> <span data-ttu-id="e1963-350">En mode de récursive, AzCopy copie tous les objets BLOB ou les fichiers qui correspondent au modèle de fichier spécifié hello, y compris celles figurant dans les sous-dossiers.</span><span class="sxs-lookup"><span data-stu-id="e1963-350">In recursive mode, AzCopy will copy all blobs or files that match hello specified file pattern, including those in subfolders.</span></span>

<span data-ttu-id="e1963-351">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="e1963-351">**Applicable to:** Blobs, Files</span></span>

### <a name="blobtypeblock--page--append"></a><span data-ttu-id="e1963-352">/BlobType:"block" | "page" | "append"</span><span class="sxs-lookup"><span data-stu-id="e1963-352">/BlobType:"block" | "page" | "append"</span></span>
<span data-ttu-id="e1963-353">Spécifie si l’objet blob de destination hello est un objet blob de blocs, un objet blob de pages ou un objet blob d’ajout.</span><span class="sxs-lookup"><span data-stu-id="e1963-353">Specifies whether hello destination blob is a block blob, a page blob, or an append blob.</span></span> <span data-ttu-id="e1963-354">Cette option s’applique uniquement lorsque vous téléchargez un objet blob.</span><span class="sxs-lookup"><span data-stu-id="e1963-354">This option is applicable only when you are uploading a blob.</span></span> <span data-ttu-id="e1963-355">Sinon, une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="e1963-355">Otherwise, an error is generated.</span></span> <span data-ttu-id="e1963-356">Si la destination de hello est un objet blob et que cette option n’est pas spécifiée, par défaut, AzCopy crée un objet blob de blocs.</span><span class="sxs-lookup"><span data-stu-id="e1963-356">If hello destination is a blob and this option is not specified, by default, AzCopy creates a block blob.</span></span>

<span data-ttu-id="e1963-357">**S’applique à :** objets blob</span><span class="sxs-lookup"><span data-stu-id="e1963-357">**Applicable to:** Blobs</span></span>

### <a name="checkmd5"></a><span data-ttu-id="e1963-358">/CheckMD5</span><span class="sxs-lookup"><span data-stu-id="e1963-358">/CheckMD5</span></span>
<span data-ttu-id="e1963-359">Calcule un hachage MD5 pour les données téléchargées et vérifie que hachage MD5 de hello stockées dans l’objet blob de hello ou propriété de Content-MD5 du fichier correspond au hachage de hello calculée.</span><span class="sxs-lookup"><span data-stu-id="e1963-359">Calculates an MD5 hash for downloaded data and verifies that hello MD5 hash stored in hello blob or file's Content-MD5 property matches hello calculated hash.</span></span> <span data-ttu-id="e1963-360">vérification de Hello MD5 est désactivée par défaut, vous devez spécifier cette vérification de MD5 option tooperform hello lors du téléchargement de données.</span><span class="sxs-lookup"><span data-stu-id="e1963-360">hello MD5 check is turned off by default, so you must specify this option tooperform hello MD5 check when downloading data.</span></span>

<span data-ttu-id="e1963-361">Notez que le stockage Azure ne garantit pas que hello hachage MD5 stockée pour l’objet blob de hello ou le fichier est à jour.</span><span class="sxs-lookup"><span data-stu-id="e1963-361">Note that Azure Storage doesn't guarantee that hello MD5 hash stored for hello blob or file is up-to-date.</span></span> <span data-ttu-id="e1963-362">Il est hello tooupdate de responsabilité du client MD5 chaque fois que l’objet blob de hello ou un fichier est modifié.</span><span class="sxs-lookup"><span data-stu-id="e1963-362">It is client's responsibility tooupdate hello MD5 whenever hello blob or file is modified.</span></span>

<span data-ttu-id="e1963-363">AzCopy affecte hello Content-MD5 propriété pour un objet blob Azure ou le fichier après son téléchargement toohello service.</span><span class="sxs-lookup"><span data-stu-id="e1963-363">AzCopy always sets hello Content-MD5 property for an Azure blob or file after uploading it toohello service.</span></span>  

<span data-ttu-id="e1963-364">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="e1963-364">**Applicable to:** Blobs, Files</span></span>

### <a name="snapshot"></a><span data-ttu-id="e1963-365">/Snapshot</span><span class="sxs-lookup"><span data-stu-id="e1963-365">/Snapshot</span></span>
<span data-ttu-id="e1963-366">Indique si les instantanés tootransfer.</span><span class="sxs-lookup"><span data-stu-id="e1963-366">Indicates whether tootransfer snapshots.</span></span> <span data-ttu-id="e1963-367">Cette option est valide uniquement lorsque la source de hello est un objet blob.</span><span class="sxs-lookup"><span data-stu-id="e1963-367">This option is only valid when hello source is a blob.</span></span>

<span data-ttu-id="e1963-368">instantanés d’objet blob transférées Hello sont renommés dans ce format : nom d’objet blob (instantané-time) .extension</span><span class="sxs-lookup"><span data-stu-id="e1963-368">hello transferred blob snapshots are renamed in this format: blob-name (snapshot-time).extension</span></span>

<span data-ttu-id="e1963-369">Par défaut, les captures instantanées ne sont pas copiées.</span><span class="sxs-lookup"><span data-stu-id="e1963-369">By default, snapshots are not copied.</span></span>

<span data-ttu-id="e1963-370">**S’applique à :** objets blob</span><span class="sxs-lookup"><span data-stu-id="e1963-370">**Applicable to:** Blobs</span></span>

### <a name="vverbose-log-file"></a><span data-ttu-id="e1963-371">/V:[verbose-log-file]</span><span class="sxs-lookup"><span data-stu-id="e1963-371">/V:[verbose-log-file]</span></span>
<span data-ttu-id="e1963-372">Stocke les messages de statut détaillés dans un fichier journal.</span><span class="sxs-lookup"><span data-stu-id="e1963-372">Outputs verbose status messages into a log file.</span></span>

<span data-ttu-id="e1963-373">Par défaut, fichier journal détaillé de hello est nommé AzCopyVerbose.log dans `%LocalAppData%\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="e1963-373">By default, hello verbose log file is named AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="e1963-374">Si vous spécifiez un emplacement du fichier existant pour cette option, la journalisation documentée hello sera ajouté toothat fichier.</span><span class="sxs-lookup"><span data-stu-id="e1963-374">If you specify an existing file location for this option, hello verbose log will be appended toothat file.</span></span>  

<span data-ttu-id="e1963-375">**S’applique à :** objets blob, fichiers, tables</span><span class="sxs-lookup"><span data-stu-id="e1963-375">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="zjournal-file-folder"></a><span data-ttu-id="e1963-376">/Z:[journal-file-folder]</span><span class="sxs-lookup"><span data-stu-id="e1963-376">/Z:[journal-file-folder]</span></span>
<span data-ttu-id="e1963-377">Spécifie un dossier de fichier journal pour reprendre une opération.</span><span class="sxs-lookup"><span data-stu-id="e1963-377">Specifies a journal file folder for resuming an operation.</span></span>

<span data-ttu-id="e1963-378">AzCopy peut toujours reprendre une opération qui a été interrompue.</span><span class="sxs-lookup"><span data-stu-id="e1963-378">AzCopy always supports resuming if an operation has been interrupted.</span></span>

<span data-ttu-id="e1963-379">Si cette option n’est pas spécifiée ou il est spécifié sans un chemin d’accès du dossier, puis AzCopy crée hello fichier journal dans l’emplacement par défaut hello, qui est % LocalAppData%\Microsoft\Azure\AzCopy.</span><span class="sxs-lookup"><span data-stu-id="e1963-379">If this option is not specified, or it is specified without a folder path, then AzCopy will create hello journal file in hello default location, which is %LocalAppData%\Microsoft\Azure\AzCopy.</span></span>

<span data-ttu-id="e1963-380">Chaque fois que vous exécutez une commande tooAzCopy, il vérifie si un fichier journal existe dans le dossier par défaut de hello, ou si elle existe dans un dossier que vous avez spécifié à l’aide de cette option.</span><span class="sxs-lookup"><span data-stu-id="e1963-380">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="e1963-381">Si le fichier journal de hello n’existe pas à cet emplacement, AzCopy traite l’opération de hello en tant que nouvelle et génère un nouveau fichier journal.</span><span class="sxs-lookup"><span data-stu-id="e1963-381">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="e1963-382">Si le fichier journal de hello existe, AzCopy vérifiera si ligne de commande hello que vous avez entré correspond à la ligne de commande hello dans un fichier de journal hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-382">If hello journal file does exist, AzCopy will check whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="e1963-383">Si les deux lignes de commande hello correspondent, AzCopy reprend les opérations d’incomplète hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-383">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="e1963-384">Si elles ne correspondent pas, vous serez tooeither invité à remplacer hello journal fichier toostart une nouvelle opération ou toocancel hello opération en cours.</span><span class="sxs-lookup"><span data-stu-id="e1963-384">If they do not match, you will be prompted tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="e1963-385">fichier de journal Hello est supprimé en cas de réussite de l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-385">hello journal file is deleted upon successful completion of hello operation.</span></span>

<span data-ttu-id="e1963-386">Remarque : reprendre une opération à partir d’un fichier journal créé par une version précédente d’AzCopy n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="e1963-386">Note that resuming an operation from a journal file created by a previous version of AzCopy is not supported.</span></span>

<span data-ttu-id="e1963-387">**S’applique à :** objets blob, fichiers, tables</span><span class="sxs-lookup"><span data-stu-id="e1963-387">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="parameter-file"></a><span data-ttu-id="e1963-388">/@:"parameter-file"</span><span class="sxs-lookup"><span data-stu-id="e1963-388">/@:"parameter-file"</span></span>
<span data-ttu-id="e1963-389">Spécifie un fichier qui contient des paramètres.</span><span class="sxs-lookup"><span data-stu-id="e1963-389">Specifies a file that contains parameters.</span></span> <span data-ttu-id="e1963-390">AzCopy processus hello paramètres hello fichier comme s’ils avaient été spécifiés sur la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-390">AzCopy processes hello parameters in hello file just as if they had been specified on hello command line.</span></span>

<span data-ttu-id="e1963-391">Dans un fichier réponse, vous pouvez soit spécifier de multiples paramètres sur une seule ligne, soit spécifier chaque paramètre sur sa propre ligne.</span><span class="sxs-lookup"><span data-stu-id="e1963-391">In a response file, you can either specify multiple parameters on a single line, or specify each parameter on its own line.</span></span> <span data-ttu-id="e1963-392">Remarque : un paramètre individuel ne peut pas couvrir plusieurs lignes.</span><span class="sxs-lookup"><span data-stu-id="e1963-392">Note that an individual parameter cannot span multiple lines.</span></span>

<span data-ttu-id="e1963-393">Fichiers réponse peuvent inclure des lignes de commentaires qui commencent par le symbole « # » hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-393">Response files can include comments lines that begin with hello # symbol.</span></span>

<span data-ttu-id="e1963-394">Vous pouvez spécifier plusieurs fichiers réponse.</span><span class="sxs-lookup"><span data-stu-id="e1963-394">You can specify multiple response files.</span></span> <span data-ttu-id="e1963-395">Toutefois, AzCopy ne prend pas en charge les fichiers réponse imbriqués.</span><span class="sxs-lookup"><span data-stu-id="e1963-395">However, note that AzCopy does not support nested response files.</span></span>

<span data-ttu-id="e1963-396">**S’applique à :** objets blob, fichiers, tables</span><span class="sxs-lookup"><span data-stu-id="e1963-396">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="y"></a><span data-ttu-id="e1963-397">/Y</span><span class="sxs-lookup"><span data-stu-id="e1963-397">/Y</span></span>
<span data-ttu-id="e1963-398">Supprime toutes les invites de confirmation d’AzCopy.</span><span class="sxs-lookup"><span data-stu-id="e1963-398">Suppresses all AzCopy confirmation prompts.</span></span>

<span data-ttu-id="e1963-399">**S’applique à :** objets blob, fichiers, tables</span><span class="sxs-lookup"><span data-stu-id="e1963-399">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="l"></a><span data-ttu-id="e1963-400">/L</span><span class="sxs-lookup"><span data-stu-id="e1963-400">/L</span></span>
<span data-ttu-id="e1963-401">Spécifie une opération de listing uniquement : aucune donnée n’est copiée.</span><span class="sxs-lookup"><span data-stu-id="e1963-401">Specifies a listing operation only; no data is copied.</span></span>

<span data-ttu-id="e1963-402">AzCopy interprétera hello à l’aide de cette option comme une simulation de ligne de commande hello en cours d’exécution sans cette option /L et compter le nombre d’objets est copié, vous pouvez spécifier option /V à hello même moment toocheck quels objets seront copiés dans le journal détaillé de hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-402">AzCopy will interpret hello using of this option as a simulation for running hello command line without this option /L and count how many objects will be copied, you can specify option /V at hello same time toocheck which objects will be copied in hello verbose log.</span></span>

<span data-ttu-id="e1963-403">Hello comportement de cette option est également déterminé par emplacement hello de source de données hello et de la présence de hello hello récursive mode option /S et le fichier de modèle de l’option de /Pattern.</span><span class="sxs-lookup"><span data-stu-id="e1963-403">hello behavior of this option is also determined by hello location of hello source data and hello presence of hello recursive mode option /S and file pattern option /Pattern.</span></span>

<span data-ttu-id="e1963-404">AzCopy nécessite les autorisations de listing et de lecture sur cet emplacement source quand cette option est utilisée.</span><span class="sxs-lookup"><span data-stu-id="e1963-404">AzCopy requires LIST and READ permission of this source location when using this option.</span></span>

<span data-ttu-id="e1963-405">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="e1963-405">**Applicable to:** Blobs, Files</span></span>

### <a name="mt"></a><span data-ttu-id="e1963-406">/MT</span><span class="sxs-lookup"><span data-stu-id="e1963-406">/MT</span></span>
<span data-ttu-id="e1963-407">Définit l’heure de dernière modification du fichier téléchargé hello toobe même hello en tant qu’objet blob source de hello ou du fichier.</span><span class="sxs-lookup"><span data-stu-id="e1963-407">Sets hello downloaded file's last-modified time toobe hello same as hello source blob or file's.</span></span>

<span data-ttu-id="e1963-408">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="e1963-408">**Applicable to:** Blobs, Files</span></span>

### <a name="xn"></a><span data-ttu-id="e1963-409">/XN</span><span class="sxs-lookup"><span data-stu-id="e1963-409">/XN</span></span>
<span data-ttu-id="e1963-410">Exclut une ressource de source plus récente.</span><span class="sxs-lookup"><span data-stu-id="e1963-410">Excludes a newer source resource.</span></span> <span data-ttu-id="e1963-411">ressource de Hello n’est pas copié si l’heure de dernière modification de la source de hello hello est hello identique ou ultérieure à la destination.</span><span class="sxs-lookup"><span data-stu-id="e1963-411">hello resource will not be copied if hello last modified time of hello source is hello same or newer than destination.</span></span>

<span data-ttu-id="e1963-412">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="e1963-412">**Applicable to:** Blobs, Files</span></span>

### <a name="xo"></a><span data-ttu-id="e1963-413">/XO</span><span class="sxs-lookup"><span data-stu-id="e1963-413">/XO</span></span>
<span data-ttu-id="e1963-414">Exclut une ressource de source plus ancienne.</span><span class="sxs-lookup"><span data-stu-id="e1963-414">Excludes an older source resource.</span></span> <span data-ttu-id="e1963-415">ressource de Hello n’est pas copié si l’heure de dernière modification de la source de hello hello est hello même ou antérieure à celle de destination.</span><span class="sxs-lookup"><span data-stu-id="e1963-415">hello resource will not be copied if hello last modified time of hello source is hello same or older than destination.</span></span>

<span data-ttu-id="e1963-416">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="e1963-416">**Applicable to:** Blobs, Files</span></span>

### <a name="a"></a><span data-ttu-id="e1963-417">/A</span><span class="sxs-lookup"><span data-stu-id="e1963-417">/A</span></span>
<span data-ttu-id="e1963-418">Télécharge uniquement les fichiers qui ont attribut hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-418">Uploads only files that have hello Archive attribute set.</span></span>

<span data-ttu-id="e1963-419">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="e1963-419">**Applicable to:** Blobs, Files</span></span>

### <a name="iarashcnetoi"></a><span data-ttu-id="e1963-420">/IA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="e1963-420">/IA:[RASHCNETOI]</span></span>
<span data-ttu-id="e1963-421">Téléchargements uniquement les fichiers ayant une des hello spécifié ensemble d’attributs.</span><span class="sxs-lookup"><span data-stu-id="e1963-421">Uploads only files that have any of hello specified attributes set.</span></span>

<span data-ttu-id="e1963-422">Les attributs disponibles incluent :</span><span class="sxs-lookup"><span data-stu-id="e1963-422">Available attributes include:</span></span>

* <span data-ttu-id="e1963-423">R = Fichiers en lecture seule</span><span class="sxs-lookup"><span data-stu-id="e1963-423">R = Read-only files</span></span>
* <span data-ttu-id="e1963-424">A = Fichiers prêts à être archivés</span><span class="sxs-lookup"><span data-stu-id="e1963-424">A = Files ready for archiving</span></span>
* <span data-ttu-id="e1963-425">S = Fichiers système</span><span class="sxs-lookup"><span data-stu-id="e1963-425">S = System files</span></span>
* <span data-ttu-id="e1963-426">H = Fichiers masqués</span><span class="sxs-lookup"><span data-stu-id="e1963-426">H = Hidden files</span></span>
* <span data-ttu-id="e1963-427">C = Fichiers compressés</span><span class="sxs-lookup"><span data-stu-id="e1963-427">C = Compressed files</span></span>
* <span data-ttu-id="e1963-428">N = Fichiers normaux</span><span class="sxs-lookup"><span data-stu-id="e1963-428">N = Normal files</span></span>
* <span data-ttu-id="e1963-429">E = Fichiers cryptés</span><span class="sxs-lookup"><span data-stu-id="e1963-429">E = Encrypted files</span></span>
* <span data-ttu-id="e1963-430">T = Fichiers temporaires</span><span class="sxs-lookup"><span data-stu-id="e1963-430">T = Temporary files</span></span>
* <span data-ttu-id="e1963-431">O = Fichiers hors ligne</span><span class="sxs-lookup"><span data-stu-id="e1963-431">O = Offline files</span></span>
* <span data-ttu-id="e1963-432">I = Fichiers non indexés</span><span class="sxs-lookup"><span data-stu-id="e1963-432">I = Non-indexed files</span></span>

<span data-ttu-id="e1963-433">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="e1963-433">**Applicable to:** Blobs, Files</span></span>

### <a name="xarashcnetoi"></a><span data-ttu-id="e1963-434">/XA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="e1963-434">/XA:[RASHCNETOI]</span></span>
<span data-ttu-id="e1963-435">Exclut les fichiers qui ont des hello spécifié jeu d’attributs.</span><span class="sxs-lookup"><span data-stu-id="e1963-435">Excludes files that have any of hello specified attributes set.</span></span>

<span data-ttu-id="e1963-436">Les attributs disponibles incluent :</span><span class="sxs-lookup"><span data-stu-id="e1963-436">Available attributes include:</span></span>

* <span data-ttu-id="e1963-437">R = Fichiers en lecture seule</span><span class="sxs-lookup"><span data-stu-id="e1963-437">R = Read-only files</span></span>
* <span data-ttu-id="e1963-438">A = Fichiers prêts à être archivés</span><span class="sxs-lookup"><span data-stu-id="e1963-438">A = Files ready for archiving</span></span>
* <span data-ttu-id="e1963-439">S = Fichiers système</span><span class="sxs-lookup"><span data-stu-id="e1963-439">S = System files</span></span>
* <span data-ttu-id="e1963-440">H = Fichiers masqués</span><span class="sxs-lookup"><span data-stu-id="e1963-440">H = Hidden files</span></span>
* <span data-ttu-id="e1963-441">C = Fichiers compressés</span><span class="sxs-lookup"><span data-stu-id="e1963-441">C = Compressed files</span></span>
* <span data-ttu-id="e1963-442">N = Fichiers normaux</span><span class="sxs-lookup"><span data-stu-id="e1963-442">N = Normal files</span></span>
* <span data-ttu-id="e1963-443">E = Fichiers cryptés</span><span class="sxs-lookup"><span data-stu-id="e1963-443">E = Encrypted files</span></span>
* <span data-ttu-id="e1963-444">T = Fichiers temporaires</span><span class="sxs-lookup"><span data-stu-id="e1963-444">T = Temporary files</span></span>
* <span data-ttu-id="e1963-445">O = Fichiers hors ligne</span><span class="sxs-lookup"><span data-stu-id="e1963-445">O = Offline files</span></span>
* <span data-ttu-id="e1963-446">I = Fichiers non indexés</span><span class="sxs-lookup"><span data-stu-id="e1963-446">I = Non-indexed files</span></span>

<span data-ttu-id="e1963-447">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="e1963-447">**Applicable to:** Blobs, Files</span></span>

### <a name="delimiterdelimiter"></a><span data-ttu-id="e1963-448">/Delimiter:"délimiteur"</span><span class="sxs-lookup"><span data-stu-id="e1963-448">/Delimiter:"delimiter"</span></span>
<span data-ttu-id="e1963-449">Indique le délimiteur hello utilisé toodelimit des répertoires virtuels dans un nom d’objet blob.</span><span class="sxs-lookup"><span data-stu-id="e1963-449">Indicates hello delimiter character used toodelimit virtual directories in a blob name.</span></span>

<span data-ttu-id="e1963-450">Par défaut, AzCopy utilise / en tant que caractère de délimiteur hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-450">By default, AzCopy uses / as hello delimiter character.</span></span> <span data-ttu-id="e1963-451">Toutefois, AzCopy prend en charge n’importe quel caractère commun (tel que @, #, ou %) comme délimiteur.</span><span class="sxs-lookup"><span data-stu-id="e1963-451">However, AzCopy supports using any common character (such as @, #, or %) as a delimiter.</span></span> <span data-ttu-id="e1963-452">Si vous devez tooinclude un de ces caractères spéciaux sur la ligne de commande hello, placez le nom de fichier hello avec des guillemets doubles.</span><span class="sxs-lookup"><span data-stu-id="e1963-452">If you need tooinclude one of these special characters on hello command line, enclose hello file name with double quotes.</span></span>

<span data-ttu-id="e1963-453">Cette option est applicable uniquement au téléchargement d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="e1963-453">This option is only applicable for downloading blobs.</span></span>

<span data-ttu-id="e1963-454">**S’applique à :** objets blob</span><span class="sxs-lookup"><span data-stu-id="e1963-454">**Applicable to:** Blobs</span></span>

### <a name="ncnumber-of-concurrent-operations"></a><span data-ttu-id="e1963-455">/NC:"nombre-d’opérations-simultanées"</span><span class="sxs-lookup"><span data-stu-id="e1963-455">/NC:"number-of-concurrent-operations"</span></span>
<span data-ttu-id="e1963-456">Spécifie le nombre de hello d’opérations simultanées.</span><span class="sxs-lookup"><span data-stu-id="e1963-456">Specifies hello number of concurrent operations.</span></span>

<span data-ttu-id="e1963-457">AzCopy par défaut démarre un certain nombre de débit de transfert de données des opérations simultanées tooincrease hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-457">AzCopy by default starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="e1963-458">Notez que le grand nombre d’opérations simultanées dans un environnement à faible bande passante peut surcharger la connexion de réseau hello et empêcher complètement exécution des opérations hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-458">Note that large number of concurrent operations in a low-bandwidth environment may overwhelm hello network connection and prevent hello operations from fully completing.</span></span> <span data-ttu-id="e1963-459">Limitez les opérations simultanées en fonction de la bande passante de réseau qui est disponible.</span><span class="sxs-lookup"><span data-stu-id="e1963-459">Throttle concurrent operations based on actual available network bandwidth.</span></span>

<span data-ttu-id="e1963-460">limite supérieure de Hello pour les opérations simultanées est 512.</span><span class="sxs-lookup"><span data-stu-id="e1963-460">hello upper limit for concurrent operations is 512.</span></span>

<span data-ttu-id="e1963-461">**S’applique à :** objets blob, fichiers, tables</span><span class="sxs-lookup"><span data-stu-id="e1963-461">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcetypeblob--table"></a><span data-ttu-id="e1963-462">/SourceType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="e1963-462">/SourceType:"Blob" | "Table"</span></span>
<span data-ttu-id="e1963-463">Spécifie que hello `source` ressource est un objet blob disponible dans l’environnement de développement local hello, en cours d’exécution dans l’émulateur de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-463">Specifies that hello `source` resource is a blob available in hello local development environment, running in hello storage emulator.</span></span>

<span data-ttu-id="e1963-464">**S’applique à :** objets blob, tables</span><span class="sxs-lookup"><span data-stu-id="e1963-464">**Applicable to:** Blobs, Tables</span></span>

### <a name="desttypeblob--table"></a><span data-ttu-id="e1963-465">/DestType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="e1963-465">/DestType:"Blob" | "Table"</span></span>
<span data-ttu-id="e1963-466">Spécifie que hello `destination` ressource est un objet blob disponible dans l’environnement de développement local hello, en cours d’exécution dans l’émulateur de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-466">Specifies that hello `destination` resource is a blob available in hello local development environment, running in hello storage emulator.</span></span>

<span data-ttu-id="e1963-467">**S’applique à :** objets blob, tables</span><span class="sxs-lookup"><span data-stu-id="e1963-467">**Applicable to:** Blobs, Tables</span></span>

### <a name="pkrskey1key2key3"></a><span data-ttu-id="e1963-468">/PKRS:"key1#key2#key3#..."</span><span class="sxs-lookup"><span data-stu-id="e1963-468">/PKRS:"key1#key2#key3#..."</span></span>
<span data-ttu-id="e1963-469">Fractionnements hello tooenable de plage de clés de partition exportation de données de table en parallèle, ce qui augmente la vitesse de l’opération d’exportation hello hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-469">Splits hello partition key range tooenable exporting table data in parallel, which increases hello speed of hello export operation.</span></span>

<span data-ttu-id="e1963-470">Si cette option n’est pas spécifiée, AzCopy utilise des entités de table tooexport un thread unique.</span><span class="sxs-lookup"><span data-stu-id="e1963-470">If this option is not specified, then AzCopy uses a single thread tooexport table entities.</span></span> <span data-ttu-id="e1963-471">Par exemple, si hello utilisateur spécifie /PKRS : « aa #bb », puis AzCopy démarre trois opérations simultanées.</span><span class="sxs-lookup"><span data-stu-id="e1963-471">For example, if hello user specifies /PKRS:"aa#bb", then AzCopy starts three concurrent operations.</span></span>

<span data-ttu-id="e1963-472">Chaque opération exporte une des trois plages de clés de partition (voir ci-dessous) :</span><span class="sxs-lookup"><span data-stu-id="e1963-472">Each operation exports one of three partition key ranges, as shown below:</span></span>

  <span data-ttu-id="e1963-473">[first-partition-key, aa)</span><span class="sxs-lookup"><span data-stu-id="e1963-473">[first-partition-key, aa)</span></span>

  <span data-ttu-id="e1963-474">[aa, bb)</span><span class="sxs-lookup"><span data-stu-id="e1963-474">[aa, bb)</span></span>

  <span data-ttu-id="e1963-475">[bb, dernière-clé-de-partition]</span><span class="sxs-lookup"><span data-stu-id="e1963-475">[bb, last-partition-key]</span></span>

<span data-ttu-id="e1963-476">**S’applique à :** tables</span><span class="sxs-lookup"><span data-stu-id="e1963-476">**Applicable to:** Tables</span></span>

### <a name="splitsizefile-size"></a><span data-ttu-id="e1963-477">/SplitSize:"file-size"</span><span class="sxs-lookup"><span data-stu-id="e1963-477">/SplitSize:"file-size"</span></span>
<span data-ttu-id="e1963-478">Spécifie hello fichier exporté fractionner la taille en Mo, hello de valeur minimale autorisée est de 32.</span><span class="sxs-lookup"><span data-stu-id="e1963-478">Specifies hello exported file split size in MB, hello minimal value allowed is 32.</span></span>

<span data-ttu-id="e1963-479">Si cette option n’est pas spécifiée, AzCopy exporte table fichier toosingle de données.</span><span class="sxs-lookup"><span data-stu-id="e1963-479">If this option is not specified, AzCopy will export table data toosingle file.</span></span>

<span data-ttu-id="e1963-480">Si les données de la table hello sont exporté tooa blob et limite de 200 Go hello pour la taille des objets blob atteint hello taille du fichier exporté, AzCopy fractionner le fichier exporté hello, même si cette option n’est pas spécifiée.</span><span class="sxs-lookup"><span data-stu-id="e1963-480">If hello table data is exported tooa blob, and hello exported file size reaches hello 200 GB limit for blob size, then AzCopy will split hello exported file, even if this option is not specified.</span></span>

<span data-ttu-id="e1963-481">**S’applique à :** tables</span><span class="sxs-lookup"><span data-stu-id="e1963-481">**Applicable to:** Tables</span></span>

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a><span data-ttu-id="e1963-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span><span class="sxs-lookup"><span data-stu-id="e1963-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span></span>
<span data-ttu-id="e1963-483">Spécifie le comportement d’importation hello table données.</span><span class="sxs-lookup"><span data-stu-id="e1963-483">Specifies hello table data import behavior.</span></span>

* <span data-ttu-id="e1963-484">InsertOrSkip - ignore une entité existante ou insère une nouvelle entité si elle n’existe pas dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-484">InsertOrSkip - Skips an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="e1963-485">InsertOrMerge - fusionne une entité existante ou insère une nouvelle entité si elle n’existe pas dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-485">InsertOrMerge - Merges an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="e1963-486">InsertOrReplace - remplace une entité existante ou insère une nouvelle entité si elle n’existe pas dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-486">InsertOrReplace - Replaces an existing entity or inserts a new entity if it does not exist in hello table.</span></span>

<span data-ttu-id="e1963-487">**S’applique à :** tables</span><span class="sxs-lookup"><span data-stu-id="e1963-487">**Applicable to:** Tables</span></span>

### <a name="manifestmanifest-file"></a><span data-ttu-id="e1963-488">/Manifest:"manifest-file"</span><span class="sxs-lookup"><span data-stu-id="e1963-488">/Manifest:"manifest-file"</span></span>
<span data-ttu-id="e1963-489">Spécifie le fichier de manifeste hello pour la table de hello d’exportation et l’opération d’importation.</span><span class="sxs-lookup"><span data-stu-id="e1963-489">Specifies hello manifest file for hello table export and import operation.</span></span>

<span data-ttu-id="e1963-490">Cette option est facultative lors de l’opération d’exportation hello, AzCopy génère un fichier manifeste avec le nom prédéfini si cette option n’est pas spécifiée.</span><span class="sxs-lookup"><span data-stu-id="e1963-490">This option is optional during hello export operation, AzCopy will generate a manifest file with predefined name if this option is not specified.</span></span>

<span data-ttu-id="e1963-491">Cette option est requise pendant l’opération d’importation hello pour localiser les fichiers de données hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-491">This option is required during hello import operation for locating hello data files.</span></span>

<span data-ttu-id="e1963-492">**S’applique à :** tables</span><span class="sxs-lookup"><span data-stu-id="e1963-492">**Applicable to:** Tables</span></span>

### <a name="synccopy"></a><span data-ttu-id="e1963-493">/SyncCopy</span><span class="sxs-lookup"><span data-stu-id="e1963-493">/SyncCopy</span></span>
<span data-ttu-id="e1963-494">Indique si toosynchronously copier des objets BLOB ou des fichiers entre deux points de terminaison de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e1963-494">Indicates whether toosynchronously copy blobs or files between two Azure Storage endpoints.</span></span>

<span data-ttu-id="e1963-495">AzCopy utilise par défaut la copie asynchrone du côté serveur.</span><span class="sxs-lookup"><span data-stu-id="e1963-495">AzCopy by default uses server-side asynchronous copy.</span></span> <span data-ttu-id="e1963-496">Spécifiez cette option tooperform synchrone copier, qui télécharge les objets BLOB ou fichiers toolocal mémoire et les charge tooAzure stockage.</span><span class="sxs-lookup"><span data-stu-id="e1963-496">Specify this option tooperform a synchronous copy, which downloads blobs or files toolocal memory and then uploads them tooAzure Storage.</span></span>

<span data-ttu-id="e1963-497">Vous pouvez utiliser cette option pour copier les fichiers dans le stockage d’objets Blob, dans le stockage de fichiers ou à partir de l’objet Blob stockage tooFile stockage et inversement.</span><span class="sxs-lookup"><span data-stu-id="e1963-497">You can use this option when copying files within Blob storage, within File storage, or from Blob storage tooFile storage or vice versa.</span></span>

<span data-ttu-id="e1963-498">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="e1963-498">**Applicable to:** Blobs, Files</span></span>

### <a name="setcontenttypecontent-type"></a><span data-ttu-id="e1963-499">/SetContentType:"content-type"</span><span class="sxs-lookup"><span data-stu-id="e1963-499">/SetContentType:"content-type"</span></span>
<span data-ttu-id="e1963-500">Spécifie le type de contenu MIME hello pour les fichiers ou les objets BLOB de destination.</span><span class="sxs-lookup"><span data-stu-id="e1963-500">Specifies hello MIME content type for destination blobs or files.</span></span>

<span data-ttu-id="e1963-501">Jeux de AzCopy hello du type de contenu d’un objet blob ou de fichiers tooapplication/octet-stream par défaut.</span><span class="sxs-lookup"><span data-stu-id="e1963-501">AzCopy sets hello content type for a blob or file tooapplication/octet-stream by default.</span></span> <span data-ttu-id="e1963-502">Vous pouvez définir le type de contenu hello pour tous les objets BLOB ou les fichiers en spécifiant explicitement une valeur pour cette option.</span><span class="sxs-lookup"><span data-stu-id="e1963-502">You can set hello content type for all blobs or files by explicitly specifying a value for this option.</span></span>

<span data-ttu-id="e1963-503">Si vous spécifiez cette option sans valeur, AzCopy définit chaque objet blob ou le type de contenu du fichier selon tooits extension de fichier.</span><span class="sxs-lookup"><span data-stu-id="e1963-503">If you specify this option without a value, then AzCopy will set each blob or file's content type according tooits file extension.</span></span>

<span data-ttu-id="e1963-504">**S’applique à :** objets blob, fichiers</span><span class="sxs-lookup"><span data-stu-id="e1963-504">**Applicable to:** Blobs, Files</span></span>

### <a name="payloadformatjson--csv"></a><span data-ttu-id="e1963-505">/PayloadFormat:"JSON" | "CSV"</span><span class="sxs-lookup"><span data-stu-id="e1963-505">/PayloadFormat:"JSON" | "CSV"</span></span>
<span data-ttu-id="e1963-506">Spécifie le format hello hello table exportée du fichier de données.</span><span class="sxs-lookup"><span data-stu-id="e1963-506">Specifies hello format of hello table exported data file.</span></span>

<span data-ttu-id="e1963-507">Si cette option n’est pas spécifiée, AzCopy exporte le fichier de données de table au format JSON par défaut.</span><span class="sxs-lookup"><span data-stu-id="e1963-507">If this option is not specified, by default AzCopy exports table data file in JSON format.</span></span>

<span data-ttu-id="e1963-508">**S’applique à :** tables</span><span class="sxs-lookup"><span data-stu-id="e1963-508">**Applicable to:** Tables</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="e1963-509">Problèmes connus et les meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="e1963-509">Known Issues and Best Practices</span></span>
### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="e1963-510">Limitation des écritures simultanées lors de la copie des données</span><span class="sxs-lookup"><span data-stu-id="e1963-510">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="e1963-511">Lorsque vous copiez des objets BLOB ou fichiers avec AzCopy, gardez à l’esprit qu’une autre application peut être modification des données de hello pendant que vous effectuez la copie.</span><span class="sxs-lookup"><span data-stu-id="e1963-511">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying hello data while you are copying it.</span></span> <span data-ttu-id="e1963-512">Si possible, assurez-vous que vous copiez les données de salutation ne sont pas modifiées pendant l’opération de copie hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-512">If possible, ensure that hello data you are copying is not being modified during hello copy operation.</span></span> <span data-ttu-id="e1963-513">Par exemple, lors de la copie d’un disque dur virtuel associé à une machine virtuelle Azure, assurez-vous qu’aucune autre application n’écrivez actuellement toohello disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="e1963-513">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing toohello VHD.</span></span> <span data-ttu-id="e1963-514">Un bon moyen toodo qu'est en louant hello ressource toobe copié.</span><span class="sxs-lookup"><span data-stu-id="e1963-514">A good way toodo this is by leasing hello resource toobe copied.</span></span> <span data-ttu-id="e1963-515">Ou bien, vous pouvez créez d’abord un instantané de hello disque dur virtuel, puis copiez instantané d’hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-515">Alternately, you can create a snapshot of hello VHD first and then copy hello snapshot.</span></span>

<span data-ttu-id="e1963-516">Si vous ne pouvez pas empêcher les autres applications à partir de l’écriture de tooblobs ou des fichiers pendant qu’ils sont copiés, puis que vous n’oubliez pas que par hello temps hello tâche se termine, hello ressources copiées peuvent ne plus avoir parité complète avec les ressources de la source hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-516">If you cannot prevent other applications from writing tooblobs or files while they are being copied, then keep in mind that by hello time hello job finishes, hello copied resources may no longer have full parity with hello source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="e1963-517">Exécuter une instance de AzCopy sur un même ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e1963-517">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="e1963-518">AzCopy est l’utilisation de hello toomaximize conçu votre ordinateur ressource tooaccelerate hello de transfert de données, nous vous recommandons exécutez qu’une seule instance AzCopy sur un ordinateur et spécifiez l’option de hello `/NC` si vous avez besoin d’opérations simultanées plus.</span><span class="sxs-lookup"><span data-stu-id="e1963-518">AzCopy is designed toomaximize hello utilization of your machine resource tooaccelerate hello data transfer, we recommend you run only one AzCopy instance on one machine, and specify hello option `/NC` if you need more concurrent operations.</span></span> <span data-ttu-id="e1963-519">Pour plus d’informations, tapez `AzCopy /?:NC` à la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="e1963-519">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a><span data-ttu-id="e1963-520">Activer les algorithmes MD5 compatibles FIPS pour AzCopy quand vous « utilisez des algorithmes compatibles FIPS pour le chiffrement, le hachage et la signature ».</span><span class="sxs-lookup"><span data-stu-id="e1963-520">Enable FIPS compliant MD5 algorithms for AzCopy when you "Use FIPS compliant algorithms for encryption, hashing and signing".</span></span>
<span data-ttu-id="e1963-521">AzCopy par défaut utilise toocalculate hello MD5 de MD5 .NET implémentation lors de la copie des objets, mais il existe certaines exigences de sécurité nécessitant le paramètre de MD5 conforme AzCopy tooenable FIPS.</span><span class="sxs-lookup"><span data-stu-id="e1963-521">AzCopy by default uses .NET MD5 implementation toocalculate hello MD5 when copying objects, but there are some security requirements that need AzCopy tooenable FIPS compliant MD5 setting.</span></span>

<span data-ttu-id="e1963-522">Vous pouvez créer un fichier app.config `AzCopy.exe.config` avec la propriété `AzureStorageUseV1MD5` et le mettre à part avec AzCopy.exe.</span><span class="sxs-lookup"><span data-stu-id="e1963-522">You can create an app.config file `AzCopy.exe.config` with property `AzureStorageUseV1MD5` and put it aside with AzCopy.exe.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

<span data-ttu-id="e1963-523">Pour la propriété « AzureStorageUseV1MD5 » • True : hello par défaut, AzCopy utilisera implémentation .NET MD5.</span><span class="sxs-lookup"><span data-stu-id="e1963-523">For property "AzureStorageUseV1MD5" • True - hello default value, AzCopy will use .NET MD5 implementation.</span></span>
<span data-ttu-id="e1963-524">Si elle a pour valeur false, AzCopy utilise l’algorithme MD5 compatible FIPS.</span><span class="sxs-lookup"><span data-stu-id="e1963-524">• False – AzCopy will use FIPS compliant MD5 algorithm.</span></span>

<span data-ttu-id="e1963-525">Notez que les algorithmes compatibles FIPS sont désactivés par défaut sur votre ordinateur Windows ; vous pouvez taper secpol.msc dans la fenêtre Exécuter et activer le commutateur « Chiffrement système : utilisez des algorithmes compatibles FIPS pour le chiffrement, le hachage et la signature » (Paramètres de sécurité -> Stratégies locales -> Options de sécurité).</span><span class="sxs-lookup"><span data-stu-id="e1963-525">Note that FIPS compliant algorithms is disabled by default on your Windows machine, you can type secpol.msc in your Run window and check this switch at Security Setting->Local Policy->Security Options->System cryptography: Use FIPS compliant algorithms for encryption, hashing and signing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1963-526">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e1963-526">Next steps</span></span>
<span data-ttu-id="e1963-527">Pour plus d’informations sur le stockage Azure et AzCopy, reportez-vous à toohello suivant des ressources.</span><span class="sxs-lookup"><span data-stu-id="e1963-527">For more information about Azure Storage and AzCopy, refer toohello following resources.</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="e1963-528">Documentation d’Azure Storage :</span><span class="sxs-lookup"><span data-stu-id="e1963-528">Azure Storage documentation:</span></span>
* [<span data-ttu-id="e1963-529">Introduction tooAzure stockage</span><span class="sxs-lookup"><span data-stu-id="e1963-529">Introduction tooAzure Storage</span></span>](storage-introduction.md)
* [<span data-ttu-id="e1963-530">Comment toouse stockage d’objets Blob à partir de .NET</span><span class="sxs-lookup"><span data-stu-id="e1963-530">How toouse Blob storage from .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="e1963-531">Comment toouse stockage de fichiers à partir de .NET</span><span class="sxs-lookup"><span data-stu-id="e1963-531">How toouse File storage from .NET</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="e1963-532">Comment toouse le stockage de Table à partir de .NET</span><span class="sxs-lookup"><span data-stu-id="e1963-532">How toouse Table storage from .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="e1963-533">Comment toocreate, gérer ou supprimer un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="e1963-533">How toocreate, manage, or delete a storage account</span></span>](storage-create-storage-account.md)
* [<span data-ttu-id="e1963-534">Transférer des données avec AzCopy sur Linux</span><span class="sxs-lookup"><span data-stu-id="e1963-534">Transfer data with AzCopy on Linux</span></span>](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="e1963-535">Billets de blog Azure Storage :</span><span class="sxs-lookup"><span data-stu-id="e1963-535">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="e1963-536">Présentation de la bibliothèque de déplacement des données dans Azure Storage en version préliminaire</span><span class="sxs-lookup"><span data-stu-id="e1963-536">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="e1963-537">AzCopy : Présentation de la copie synchrone et du type de contenu personnalisé</span><span class="sxs-lookup"><span data-stu-id="e1963-537">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="e1963-538">AzCopy : Annonce de la disponibilité générale d'AzCopy 3.0 plus version préliminaire d'AzCopy 4.0 avec prise en charge de fichier et de table</span><span class="sxs-lookup"><span data-stu-id="e1963-538">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="e1963-539">AzCopy : Optimisation pour les scénarios de copie à grande échelle</span><span class="sxs-lookup"><span data-stu-id="e1963-539">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="e1963-540">AzCopy : Prise en charge des comptes de stockage géo-redondants avec accès en lecture</span><span class="sxs-lookup"><span data-stu-id="e1963-540">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="e1963-541">AzCopy : Transfert des données avec mode reprise et jeton SAP</span><span class="sxs-lookup"><span data-stu-id="e1963-541">AzCopy: Transfer data with re-startable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="e1963-542">AzCopy : Utilisation de copie d'objets blob sur plusieurs comptes</span><span class="sxs-lookup"><span data-stu-id="e1963-542">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="e1963-543">AzCopy : Chargement/téléchargement des fichiers pour les objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="e1963-543">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

