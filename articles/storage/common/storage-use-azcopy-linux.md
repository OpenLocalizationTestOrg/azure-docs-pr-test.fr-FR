---
title: "tooAzure de données aaaCopy ou déplacer le stockage avec AzCopy sur Linux | Documents Microsoft"
description: "Utilisez hello AzCopy sur Linux utilitaire toomove ou copie de données tooor à partir de l’objet blob et le fichier de contenu. Copier des données tooAzure stockage à partir de fichiers locales, ou copier des données dans ou entre des comptes de stockage. Migrer facilement vos données de tooAzure stockage."
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
ms.date: 05/11/2017
ms.author: seguler
ms.openlocfilehash: ee39c311d996a046999b7fd4a4eb873f25b4eb86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a><span data-ttu-id="26531-105">Transférer des données avec AzCopy sur Linux</span><span class="sxs-lookup"><span data-stu-id="26531-105">Transfer data with AzCopy on Linux</span></span>
<span data-ttu-id="26531-106">AzCopy sur Linux est un utilitaire de ligne de commande conçu pour la copie des données tooand à partir du stockage d’objets Blob Microsoft Azure et de fichier à l’aide de commandes simples avec des performances optimales.</span><span class="sxs-lookup"><span data-stu-id="26531-106">AzCopy on Linux is a command-line utility designed for copying data tooand from Microsoft Azure Blob and File storage using simple commands with optimal performance.</span></span> <span data-ttu-id="26531-107">Vous pouvez copier des données à partir d’un objet tooanother dans votre compte de stockage, ou entre des comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="26531-107">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="26531-108">Il existe deux versions d’AzCopy que vous pouvez télécharger.</span><span class="sxs-lookup"><span data-stu-id="26531-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="26531-109">AzCopy sur Linux est intégré à .NET Core Framework, qui cible les plateformes Linux en offrant des options en ligne de commande de style POSIX.</span><span class="sxs-lookup"><span data-stu-id="26531-109">AzCopy on Linux is built with .NET Core Framework, which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="26531-110">[AzCopy sur Windows](../storage-use-azcopy.md) est intégré à .NET Framework et offre des options en ligne de commande de style Windows.</span><span class="sxs-lookup"><span data-stu-id="26531-110">[AzCopy on Windows](../storage-use-azcopy.md) is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="26531-111">Cet article est consacré à AzCopy sur Linux.</span><span class="sxs-lookup"><span data-stu-id="26531-111">This article covers AzCopy on Linux.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="26531-112">Téléchargement et installation d’AzCopy</span><span class="sxs-lookup"><span data-stu-id="26531-112">Download and install AzCopy</span></span>
### <a name="installation-on-linux"></a><span data-ttu-id="26531-113">Installation sur Linux</span><span class="sxs-lookup"><span data-stu-id="26531-113">Installation on Linux</span></span>

<span data-ttu-id="26531-114">AzCopy sur Linux nécessite le framework .NET Core sur la plateforme de hello.</span><span class="sxs-lookup"><span data-stu-id="26531-114">AzCopy on Linux requires .NET Core framework on hello platform.</span></span> <span data-ttu-id="26531-115">Consultez les instructions d’installation de hello sur hello [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) page.</span><span class="sxs-lookup"><span data-stu-id="26531-115">See hello installation instructions on hello [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) page.</span></span>

<span data-ttu-id="26531-116">Par exemple, nous allons installer .NET Core sur Ubuntu 16.10.</span><span class="sxs-lookup"><span data-stu-id="26531-116">As an example, let's install .NET Core on Ubuntu 16.10.</span></span> <span data-ttu-id="26531-117">Guide d’installation hello plus récente, visitez [.NET Core sur Linux](https://www.microsoft.com/net/core#linuxubuntu) page d’installation.</span><span class="sxs-lookup"><span data-stu-id="26531-117">For hello latest installation guide, visit [.NET Core on Linux](https://www.microsoft.com/net/core#linuxubuntu) installation page.</span></span>


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

<span data-ttu-id="26531-118">Une fois que vous avez installé .NET Core, téléchargez et installez AzCopy.</span><span class="sxs-lookup"><span data-stu-id="26531-118">Once you have installed .NET Core, download and install AzCopy.</span></span>

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

<span data-ttu-id="26531-119">Vous pouvez supprimer des fichiers de hello extrait une fois AzCopy sur Linux est installé.</span><span class="sxs-lookup"><span data-stu-id="26531-119">You can remove hello extracted files once AzCopy on Linux is installed.</span></span> <span data-ttu-id="26531-120">Vous pouvez également si vous n’avez pas de privilèges de superutilisateur, vous pouvez également exécuter AzCopy à l’aide du script de shell hello 'azcopy' dans le dossier d’extraction hello.</span><span class="sxs-lookup"><span data-stu-id="26531-120">Alternatively if you do not have superuser privileges, you can also run AzCopy using hello shell script 'azcopy' in hello extracted folder.</span></span> 

### <a name="alternative-installation-on-ubuntu"></a><span data-ttu-id="26531-121">Installation alternative sur Ubuntu</span><span class="sxs-lookup"><span data-stu-id="26531-121">Alternative Installation on Ubuntu</span></span>

<span data-ttu-id="26531-122">**Ubuntu 14.04**</span><span class="sxs-lookup"><span data-stu-id="26531-122">**Ubuntu 14.04**</span></span>

<span data-ttu-id="26531-123">Ajoutez une source apt pour .Net Core :</span><span class="sxs-lookup"><span data-stu-id="26531-123">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="26531-124">Ajoutez une source apt pour le référentiel de produit Microsoft Linux et installez AzCopy :</span><span class="sxs-lookup"><span data-stu-id="26531-124">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

```bash
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

<span data-ttu-id="26531-125">**Ubuntu 16.04**</span><span class="sxs-lookup"><span data-stu-id="26531-125">**Ubuntu 16.04**</span></span>

<span data-ttu-id="26531-126">Ajoutez une source apt pour .Net Core :</span><span class="sxs-lookup"><span data-stu-id="26531-126">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="26531-127">Ajoutez une source apt pour le référentiel de produit Microsoft Linux et installez AzCopy :</span><span class="sxs-lookup"><span data-stu-id="26531-127">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

```bash
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

<span data-ttu-id="26531-128">**Ubuntu 16.10**</span><span class="sxs-lookup"><span data-stu-id="26531-128">**Ubuntu 16.10**</span></span>

<span data-ttu-id="26531-129">Ajoutez une source apt pour .Net Core :</span><span class="sxs-lookup"><span data-stu-id="26531-129">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="26531-130">Ajoutez une source apt pour le référentiel de produit Microsoft Linux et installez AzCopy :</span><span class="sxs-lookup"><span data-stu-id="26531-130">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

```bash
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="26531-131">Écriture de votre première commande AzCopy</span><span class="sxs-lookup"><span data-stu-id="26531-131">Writing your first AzCopy command</span></span>
<span data-ttu-id="26531-132">syntaxe de base Hello pour les commandes AzCopy est la suivante :</span><span class="sxs-lookup"><span data-stu-id="26531-132">hello basic syntax for AzCopy commands is:</span></span>

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

<span data-ttu-id="26531-133">Hello suivant exemples illustrent divers scénarios pour la copie des données tooand à partir de fichiers et les objets BLOB Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="26531-133">hello following examples demonstrate various scenarios for copying data tooand from Microsoft Azure Blobs and Files.</span></span> <span data-ttu-id="26531-134">Consultez toohello `azcopy --help` menu pour une explication détaillée des paramètres hello utilisées dans chaque exemple.</span><span class="sxs-lookup"><span data-stu-id="26531-134">Refer toohello `azcopy --help` menu for a detailed explanation of hello parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="26531-135">Blob : Téléchargement</span><span class="sxs-lookup"><span data-stu-id="26531-135">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="26531-136">Télécharger un seul objet blob</span><span class="sxs-lookup"><span data-stu-id="26531-136">Download single blob</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="26531-137">Si le dossier de hello `/mnt/myfiles` n’existe pas, AzCopy crée et télécharge `abc.txt ` dans le dossier hello.</span><span class="sxs-lookup"><span data-stu-id="26531-137">If hello folder `/mnt/myfiles` does not exist, AzCopy creates it and downloads `abc.txt ` into hello new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="26531-138">Télécharger un objet blob unique depuis la région secondaire</span><span class="sxs-lookup"><span data-stu-id="26531-138">Download single blob from secondary region</span></span>

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="26531-139">Notez que vous devez avoir un accès en lecture activé pour le stockage géo-redondant.</span><span class="sxs-lookup"><span data-stu-id="26531-139">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="26531-140">Télécharger tous les objets blob</span><span class="sxs-lookup"><span data-stu-id="26531-140">Download all blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="26531-141">Supposons suivant de hello BLOB réside dans le conteneur spécifié de hello :</span><span class="sxs-lookup"><span data-stu-id="26531-141">Assume hello following blobs reside in hello specified container:</span></span>  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

<span data-ttu-id="26531-142">Après l’opération de téléchargement hello hello active `/mnt/myfiles` inclut hello fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="26531-142">After hello download operation, hello directory `/mnt/myfiles` includes hello following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

<span data-ttu-id="26531-143">Si vous ne spécifiez pas l’option `--recursive`, aucun blob ne sera téléchargé.</span><span class="sxs-lookup"><span data-stu-id="26531-143">If you do not specify option `--recursive`, no blob will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="26531-144">Téléchargement d’objets blob avec le préfixe spécifié</span><span class="sxs-lookup"><span data-stu-id="26531-144">Download blobs with specified prefix</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

<span data-ttu-id="26531-145">Supposons suivant de hello BLOB réside dans le conteneur spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="26531-145">Assume hello following blobs reside in hello specified container.</span></span> <span data-ttu-id="26531-146">Tous les objets BLOB commençant par préfixe de hello `a` sont téléchargées.</span><span class="sxs-lookup"><span data-stu-id="26531-146">All blobs beginning with hello prefix `a` are downloaded.</span></span>

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

<span data-ttu-id="26531-147">Après l’opération de téléchargement hello hello dossier `/mnt/myfiles` inclut hello fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="26531-147">After hello download operation, hello folder `/mnt/myfiles` includes hello following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

<span data-ttu-id="26531-148">préfixe de Hello applique le répertoire virtuel toohello, ce qui constitue hello première partie du nom d’objet blob hello.</span><span class="sxs-lookup"><span data-stu-id="26531-148">hello prefix applies toohello virtual directory, which forms hello first part of hello blob name.</span></span> <span data-ttu-id="26531-149">Exemple hello ci-dessus, répertoire virtuel de hello ne correspond pas au préfixe spécifié de hello, donc aucun objet blob n’est téléchargé.</span><span class="sxs-lookup"><span data-stu-id="26531-149">In hello example shown above, hello virtual directory does not match hello specified prefix, so no blob is downloaded.</span></span> <span data-ttu-id="26531-150">En outre, si hello option `--recursive` n’est pas spécifié, AzCopy ne télécharge pas les objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="26531-150">In addition, if hello option `--recursive` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a><span data-ttu-id="26531-151">Définir l’heure de dernière modification de hello de fichiers exportés toobe identique hello d’objets BLOB sources</span><span class="sxs-lookup"><span data-stu-id="26531-151">Set hello last-modified time of exported files toobe same as hello source blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

<span data-ttu-id="26531-152">Vous pouvez également exclure des objets BLOB à partir de l’opération de téléchargement hello en fonction de leur heure de dernière modification.</span><span class="sxs-lookup"><span data-stu-id="26531-152">You can also exclude blobs from hello download operation based on their last-modified time.</span></span> <span data-ttu-id="26531-153">Par exemple, si vous souhaitez que les objets BLOB de tooexclude dont heure de dernière modification est hello même ou plus récent que le fichier de destination hello, ajouter hello `--exclude-newer` option :</span><span class="sxs-lookup"><span data-stu-id="26531-153">For example, if you want tooexclude blobs whose last modified time is hello same or newer than hello destination file, add hello `--exclude-newer` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

<span data-ttu-id="26531-154">Ou si vous souhaitez que les objets BLOB de tooexclude dont heure de dernière modification est hello même ou antérieure à celle de fichier de destination hello, ajoutez hello `--exclude-older` option :</span><span class="sxs-lookup"><span data-stu-id="26531-154">Or if you want tooexclude blobs whose last modified time is hello same or older than hello destination file, add hello `--exclude-older` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a><span data-ttu-id="26531-155">Objet blob : Téléchargement</span><span class="sxs-lookup"><span data-stu-id="26531-155">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="26531-156">Télécharger un fichier unique</span><span class="sxs-lookup"><span data-stu-id="26531-156">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="26531-157">Si le conteneur de destination spécifié hello n’existe pas, AzCopy crée et téléchargements hello fichier dedans.</span><span class="sxs-lookup"><span data-stu-id="26531-157">If hello specified destination container does not exist, AzCopy creates it and uploads hello file into it.</span></span>

### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="26531-158">Téléchargement de fichier unique toovirtual Active</span><span class="sxs-lookup"><span data-stu-id="26531-158">Upload single file toovirtual directory</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="26531-159">Si hello spécifié le répertoire virtuel n’existe pas, AzCopy télécharge hello fichier tooinclude hello répertoire virtuel dans le nom d’objet blob hello (*par exemple,*, `vd/abc.txt` dans l’exemple hello ci-dessus).</span><span class="sxs-lookup"><span data-stu-id="26531-159">If hello specified virtual directory does not exist, AzCopy uploads hello file tooinclude hello virtual directory in hello blob name (*e.g.*, `vd/abc.txt` in hello example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="26531-160">Télécharger tous les fichiers</span><span class="sxs-lookup"><span data-stu-id="26531-160">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="26531-161">L’option `--recursive` contenu hello de téléchargements de hello spécifié directory tooBlob stockage de manière récursive, c'est-à-dire que tous les sous-dossiers et fichiers sont également téléchargés.</span><span class="sxs-lookup"><span data-stu-id="26531-161">Specifying option `--recursive` uploads hello contents of hello specified directory tooBlob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="26531-162">Par exemple, supposons que suivant de hello fichiers résident dans le dossier `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="26531-162">For instance, assume hello following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="26531-163">Après l’opération de téléchargement de hello, conteneur de hello inclut hello fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="26531-163">After hello upload operation, hello container includes hello following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="26531-164">Lorsque hello option `--recursive` n’est pas spécifié, seul hello trois fichiers suivants sont téléchargés :</span><span class="sxs-lookup"><span data-stu-id="26531-164">When hello option `--recursive` is not specified, only hello following three files are uploaded:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="26531-165">Télécharger des fichiers correspondant au modèle spécifié</span><span class="sxs-lookup"><span data-stu-id="26531-165">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

<span data-ttu-id="26531-166">Supposons suivant de hello fichiers résident dans le dossier `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="26531-166">Assume hello following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="26531-167">Après l’opération de téléchargement de hello, conteneur de hello inclut hello fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="26531-167">After hello upload operation, hello container includes hello following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="26531-168">Lorsque hello option `--recursive` n’est pas spécifié, AzCopy ignore les fichiers qui se trouvent dans les sous-répertoires :</span><span class="sxs-lookup"><span data-stu-id="26531-168">When hello option `--recursive` is not specified, AzCopy skips files that are in sub-directories:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="26531-169">Spécifiez le type de contenu MIME hello d’un objet blob de destination</span><span class="sxs-lookup"><span data-stu-id="26531-169">Specify hello MIME content type of a destination blob</span></span>
<span data-ttu-id="26531-170">Par défaut, AzCopy définit les type de contenu hello d’un objet blob de destination trop`application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="26531-170">By default, AzCopy sets hello content type of a destination blob too`application/octet-stream`.</span></span> <span data-ttu-id="26531-171">Toutefois, vous pouvez spécifier explicitement le type de contenu hello via l’option de hello `--set-content-type [content-type]`.</span><span class="sxs-lookup"><span data-stu-id="26531-171">However, you can explicitly specify hello content type via hello option `--set-content-type [content-type]`.</span></span> <span data-ttu-id="26531-172">Cette syntaxe définit le type de contenu hello pour tous les objets BLOB dans une opération de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="26531-172">This syntax sets hello content type for all blobs in an upload operation.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

<span data-ttu-id="26531-173">Si hello option `--set-content-type` est spécifié sans valeur, puis AzCopy définit chaque objet blob ou le fichier du type de contenu en fonction de tooits extension de fichier.</span><span class="sxs-lookup"><span data-stu-id="26531-173">If hello option `--set-content-type` is specified without a value, then AzCopy sets each blob or file's content type according tooits file extension.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a><span data-ttu-id="26531-174">Objet blob : copie</span><span class="sxs-lookup"><span data-stu-id="26531-174">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="26531-175">Copie d’un objet blob unique au sein d’un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="26531-175">Copy single blob within Storage account</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="26531-176">Lorsque vous copiez un blob sans l’option --sync-copy, une opération de [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) est exécutée.</span><span class="sxs-lookup"><span data-stu-id="26531-176">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="26531-177">Copier un objet blob unique sur plusieurs comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="26531-177">Copy single blob across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="26531-178">Lorsque vous copiez un blob sans l’option --sync-copy, une opération de [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) est exécutée.</span><span class="sxs-lookup"><span data-stu-id="26531-178">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a><span data-ttu-id="26531-179">Copier un seul objet blob à partir de la région de tooprimary région secondaire</span><span class="sxs-lookup"><span data-stu-id="26531-179">Copy single blob from secondary region tooprimary region</span></span>

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="26531-180">Notez que vous devez avoir un accès en lecture activé pour le stockage géo-redondant.</span><span class="sxs-lookup"><span data-stu-id="26531-180">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="26531-181">Copier un objet blob unique et ses captures instantanées sur plusieurs comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="26531-181">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

<span data-ttu-id="26531-182">Après l’opération de copie hello, conteneur cible de hello inclut les blob hello et ses instantanés.</span><span class="sxs-lookup"><span data-stu-id="26531-182">After hello copy operation, hello target container includes hello blob and its snapshots.</span></span> <span data-ttu-id="26531-183">conteneur Hello inclut suivant de hello blob et ses instantanés :</span><span class="sxs-lookup"><span data-stu-id="26531-183">hello container includes hello following blob and its snapshots:</span></span>

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="26531-184">Copier des objets blob de façon synchrone dans des comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="26531-184">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="26531-185">AzCopy copie par défaut les données entre deux points de terminaison de stockage de façon asynchrone.</span><span class="sxs-lookup"><span data-stu-id="26531-185">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="26531-186">Par conséquent, opération de copie hello s’exécute en arrière-plan hello à l’aide de la capacité de la bande passante de rechange avec aucun contrat SLA en termes de rapidité un objet blob est copié.</span><span class="sxs-lookup"><span data-stu-id="26531-186">Therefore, hello copy operation runs in hello background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied.</span></span> 

<span data-ttu-id="26531-187">Hello `--sync-copy` option permet à opération de copie hello vitesse cohérente.</span><span class="sxs-lookup"><span data-stu-id="26531-187">hello `--sync-copy` option ensures that hello copy operation gets consistent speed.</span></span> <span data-ttu-id="26531-188">AzCopy effectue la copie synchrone de hello en téléchargeant les objets BLOB de hello toocopy de hello spécifié source toolocal la mémoire et les télécharger la destination de stockage d’objets Blob toohello.</span><span class="sxs-lookup"><span data-stu-id="26531-188">AzCopy performs hello synchronous copy by downloading hello blobs toocopy from hello specified source toolocal memory, and then uploading them toohello Blob storage destination.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

<span data-ttu-id="26531-189">`--sync-copy`peut générer une copie de tooasynchronous de coût par rapport de sortie supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="26531-189">`--sync-copy` might generate additional egress cost compared tooasynchronous copy.</span></span> <span data-ttu-id="26531-190">Hello approche recommandée est toouse cette option dans une machine virtuelle Azure, qui se trouve dans hello même région que votre coût sortie tooavoid de compte de stockage source.</span><span class="sxs-lookup"><span data-stu-id="26531-190">hello recommended approach is toouse this option in an Azure VM, that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="26531-191">Fichier : Téléchargement</span><span class="sxs-lookup"><span data-stu-id="26531-191">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="26531-192">Télécharger un fichier unique</span><span class="sxs-lookup"><span data-stu-id="26531-192">Download single file</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="26531-193">Si hello spécifié source est un partage de fichiers Azure, vous devez spécifier soit le nom de fichier exact hello, (*par exemple,* `abc.txt`) toodownload un seul fichier, ou spécifiez l’option `--recursive` toodownload tous les fichiers dans le partage de hello récursive.</span><span class="sxs-lookup"><span data-stu-id="26531-193">If hello specified source is an Azure file share, then you must either specify hello exact file name, (*e.g.* `abc.txt`) toodownload a single file, or specify option `--recursive` toodownload all files in hello share recursively.</span></span> <span data-ttu-id="26531-194">Tentative de toospecify un modèle de fichier et l’option `--recursive` entraîne une erreur.</span><span class="sxs-lookup"><span data-stu-id="26531-194">Attempting toospecify both a file pattern and option `--recursive` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="26531-195">Charger tous les fichiers</span><span class="sxs-lookup"><span data-stu-id="26531-195">Download all files</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="26531-196">Notez que les dossiers vides ne sont pas téléchargés.</span><span class="sxs-lookup"><span data-stu-id="26531-196">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="26531-197">Fichier : Télécharger</span><span class="sxs-lookup"><span data-stu-id="26531-197">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="26531-198">Télécharger un fichier unique</span><span class="sxs-lookup"><span data-stu-id="26531-198">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="26531-199">Télécharger tous les fichiers</span><span class="sxs-lookup"><span data-stu-id="26531-199">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="26531-200">Notez que les dossiers vides ne sont pas chargés.</span><span class="sxs-lookup"><span data-stu-id="26531-200">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="26531-201">Télécharger des fichiers correspondant au modèle spécifié</span><span class="sxs-lookup"><span data-stu-id="26531-201">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a><span data-ttu-id="26531-202">Fichier : Copier</span><span class="sxs-lookup"><span data-stu-id="26531-202">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="26531-203">Copier d’un partage de fichier à l’autre</span><span class="sxs-lookup"><span data-stu-id="26531-203">Copy across file shares</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="26531-204">Lorsque vous copiez un fichier sur plusieurs partage de fichiers, une opération de [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) est exécutée.</span><span class="sxs-lookup"><span data-stu-id="26531-204">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-tooblob"></a><span data-ttu-id="26531-205">Copier à partir de tooblob de partage de fichier</span><span class="sxs-lookup"><span data-stu-id="26531-205">Copy from file share tooblob</span></span>

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="26531-206">Lorsque vous copiez un fichier à partir du fichier partage tooblob, un [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) opération est effectuée.</span><span class="sxs-lookup"><span data-stu-id="26531-206">When you copy a file from file share tooblob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-blob-toofile-share"></a><span data-ttu-id="26531-207">Copier à partir du partage de toofile d’objets blob</span><span class="sxs-lookup"><span data-stu-id="26531-207">Copy from blob toofile share</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="26531-208">Lorsque vous copiez un fichier à partir d’un partage toofile blob, une [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) opération est effectuée.</span><span class="sxs-lookup"><span data-stu-id="26531-208">When you copy a file from blob toofile share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="26531-209">Copier les fichiers de façon synchrone</span><span class="sxs-lookup"><span data-stu-id="26531-209">Synchronously copy files</span></span>
<span data-ttu-id="26531-210">Vous pouvez spécifier hello `--sync-copy` option toocopy des données à partir du stockage de fichiers tooFile stockage, à partir du stockage de fichiers tooBlob stockage et de stockage d’objets Blob tooFile stockage de façon synchrone.</span><span class="sxs-lookup"><span data-stu-id="26531-210">You can specify hello `--sync-copy` option toocopy data from File Storage tooFile Storage, from File Storage tooBlob Storage and from Blob Storage tooFile Storage synchronously.</span></span> <span data-ttu-id="26531-211">AzCopy exécute cette opération en téléchargeant les données toolocal mémoire hello source et en téléchargeant toodestination.</span><span class="sxs-lookup"><span data-stu-id="26531-211">AzCopy runs this operation by downloading hello source data toolocal memory, and then uploading it toodestination.</span></span> <span data-ttu-id="26531-212">Dans ce cas, des coûts de sortie standard s’appliquent.</span><span class="sxs-lookup"><span data-stu-id="26531-212">In this case, standard egress cost applies.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

<span data-ttu-id="26531-213">Lors de la copie à partir du stockage de fichiers tooBlob stockage, type d’objet blob hello par défaut est l’objet blob de blocs, utilisateur peut spécifier l’option `/BlobType:page` type d’objet blob destination toochange hello.</span><span class="sxs-lookup"><span data-stu-id="26531-213">When copying from File Storage tooBlob Storage, hello default blob type is block blob, user can specify option `/BlobType:page` toochange hello destination blob type.</span></span>

<span data-ttu-id="26531-214">Notez que `--sync-copy` risque de générer des sorties supplémentaires comparaison tooasynchronous copie de coût.</span><span class="sxs-lookup"><span data-stu-id="26531-214">Note that `--sync-copy` might generate additional egress cost comparing tooasynchronous copy.</span></span> <span data-ttu-id="26531-215">Hello approche recommandée est toouse cette option dans une machine virtuelle Azure, qui se trouve dans hello même région que votre coût sortie tooavoid de compte de stockage source.</span><span class="sxs-lookup"><span data-stu-id="26531-215">hello recommended approach is toouse this option in an Azure VM, that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="other-azcopy-features"></a><span data-ttu-id="26531-216">Autres fonctionnalités AzCopy</span><span class="sxs-lookup"><span data-stu-id="26531-216">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a><span data-ttu-id="26531-217">Copier uniquement les données qui n’existent pas dans la destination de hello</span><span class="sxs-lookup"><span data-stu-id="26531-217">Only copy data that doesn't exist in hello destination</span></span>
<span data-ttu-id="26531-218">Hello `--exclude-older` et `--exclude-newer` paramètres vous permettent de tooexclude des ressources de source ancien ou plus récent à partir de la copie, respectivement.</span><span class="sxs-lookup"><span data-stu-id="26531-218">hello `--exclude-older` and `--exclude-newer` parameters allow you tooexclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="26531-219">Si vous souhaitez uniquement les ressources de la source toocopy qui n’existent pas dans la destination de hello, vous pouvez spécifier les deux paramètres Bonjour AzCopy commande :</span><span class="sxs-lookup"><span data-stu-id="26531-219">If you only want toocopy source resources that don't exist in hello destination, you can specify both parameters in hello AzCopy command:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-toospecify-command-line-parameters"></a><span data-ttu-id="26531-220">Utiliser un paramètres de ligne de commande de toospecify de fichier de configuration</span><span class="sxs-lookup"><span data-stu-id="26531-220">Use a configuration file toospecify command-line parameters</span></span>

```azcopy
azcopy --config-file "azcopy-config.ini"
```

<span data-ttu-id="26531-221">Vous pouvez inclure n’importe quels paramètres en ligne de commande AzCopy dans un fichier config.</span><span class="sxs-lookup"><span data-stu-id="26531-221">You can include any AzCopy command-line parameters in a configuration file.</span></span> <span data-ttu-id="26531-222">AzCopy processus hello paramètres hello fichier comme s’ils avaient été spécifiés sur la ligne de commande hello, effectuer une substitution directe avec le contenu de hello du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="26531-222">AzCopy processes hello parameters in hello file as if they had been specified on hello command line, performing a direct substitution with hello contents of hello file.</span></span>

<span data-ttu-id="26531-223">Supposons un fichier de configuration nommé `copyoperation`, qui contient les lignes suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="26531-223">Assume a configuration file named `copyoperation`, that contains hello following lines.</span></span> <span data-ttu-id="26531-224">Chaque paramètre AzCopy peut être spécifié sur une seule ligne.</span><span class="sxs-lookup"><span data-stu-id="26531-224">Each AzCopy parameter can be specified on a single line.</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

<span data-ttu-id="26531-225">ou sur des lignes distinctes :</span><span class="sxs-lookup"><span data-stu-id="26531-225">or on separate lines:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

<span data-ttu-id="26531-226">AzCopy échoue si vous fractionnez le paramètre hello entre deux lignes, comme indiqué ici pour hello `--source-key` paramètre :</span><span class="sxs-lookup"><span data-stu-id="26531-226">AzCopy fails if you split hello parameter across two lines, as shown here for hello `--source-key` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="26531-227">Spécification d’une signature d’accès partagé (SAP)</span><span class="sxs-lookup"><span data-stu-id="26531-227">Specify a shared access signature (SAS)</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

<span data-ttu-id="26531-228">Vous pouvez également spécifier une SAP sur l’URI du conteneur hello :</span><span class="sxs-lookup"><span data-stu-id="26531-228">You can also specify a SAS on hello container URI:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

<span data-ttu-id="26531-229">Notez que AzCopy actuellement prend uniquement en charge hello [compte SAP](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="26531-229">Note that AzCopy currently only supports hello [Account SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

### <a name="journal-file-folder"></a><span data-ttu-id="26531-230">Dossier du fichier journal</span><span class="sxs-lookup"><span data-stu-id="26531-230">Journal file folder</span></span>
<span data-ttu-id="26531-231">Chaque fois que vous exécutez une commande tooAzCopy, il vérifie si un fichier journal existe dans le dossier par défaut de hello, ou si elle existe dans un dossier que vous avez spécifié à l’aide de cette option.</span><span class="sxs-lookup"><span data-stu-id="26531-231">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="26531-232">Si le fichier journal de hello n’existe pas à cet emplacement, AzCopy traite l’opération de hello en tant que nouvelle et génère un nouveau fichier journal.</span><span class="sxs-lookup"><span data-stu-id="26531-232">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="26531-233">Si le fichier journal de hello existe, AzCopy vérifie si la ligne de commande hello que vous avez entré correspond à ligne de commande hello dans un fichier de journal hello.</span><span class="sxs-lookup"><span data-stu-id="26531-233">If hello journal file does exist, AzCopy checks whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="26531-234">Si les deux lignes de commande hello correspondent, AzCopy reprend les opérations d’incomplète hello.</span><span class="sxs-lookup"><span data-stu-id="26531-234">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="26531-235">Si elles ne correspondent pas, AzCopy invite utilisateur tooeither remplacer hello journal fichier toostart une nouvelle opération ou opération toocancel hello en cours.</span><span class="sxs-lookup"><span data-stu-id="26531-235">If they do not match, AzCopy prompts user tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="26531-236">Si vous souhaitez toouse hello emplacement par défaut hello journal fichier :</span><span class="sxs-lookup"><span data-stu-id="26531-236">If you want toouse hello default location for hello journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

<span data-ttu-id="26531-237">Si vous omettez l’option `--resume`, ou spécifiez l’option `--resume` sans chemin d’accès du dossier hello, comme indiqué ci-dessus, AzCopy crée hello journal fichier dans l’emplacement par défaut hello, qui est `~\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="26531-237">If you omit option `--resume`, or specify option `--resume` without hello folder path, as shown above, AzCopy creates hello journal file in hello default location, which is `~\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="26531-238">Si le fichier journal de hello existe déjà, AzCopy reprend les opérations de hello basée sur le fichier journal de hello.</span><span class="sxs-lookup"><span data-stu-id="26531-238">If hello journal file already exists, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="26531-239">Si vous souhaitez toospecify un emplacement personnalisé pour le fichier journal de hello :</span><span class="sxs-lookup"><span data-stu-id="26531-239">If you want toospecify a custom location for hello journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

<span data-ttu-id="26531-240">Cet exemple crée le fichier journal de hello si elle n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="26531-240">This example creates hello journal file if it does not already exist.</span></span> <span data-ttu-id="26531-241">S’il n’existe pas, AzCopy reprend les opérations de hello basée sur le fichier journal de hello.</span><span class="sxs-lookup"><span data-stu-id="26531-241">If it does exist, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="26531-242">Si vous souhaitez tooresume une opération AzCopy, répétez hello même commande.</span><span class="sxs-lookup"><span data-stu-id="26531-242">If you want tooresume an AzCopy operation, repeat hello same command.</span></span> <span data-ttu-id="26531-243">AzCopy sur Linux vous invitera à confirmer l’opération :</span><span class="sxs-lookup"><span data-stu-id="26531-243">AzCopy on Linux then will prompt for confirmation:</span></span>

```azcopy
Incomplete operation with same command line detected at hello journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want tooresume hello operation? Choose Yes tooresume, choose No toooverwrite hello journal toostart a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a><span data-ttu-id="26531-244">Journaux détaillés de sortie</span><span class="sxs-lookup"><span data-stu-id="26531-244">Output verbose logs</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a><span data-ttu-id="26531-245">Spécifiez le nombre hello d’opérations simultanées toostart</span><span class="sxs-lookup"><span data-stu-id="26531-245">Specify hello number of concurrent operations toostart</span></span>
<span data-ttu-id="26531-246">Option `--parallel-level` Spécifie le nombre de hello d’opérations de copie simultanées.</span><span class="sxs-lookup"><span data-stu-id="26531-246">Option `--parallel-level` specifies hello number of concurrent copy operations.</span></span> <span data-ttu-id="26531-247">Par défaut, AzCopy démarre un certain nombre de débit de transfert de données des opérations simultanées tooincrease hello.</span><span class="sxs-lookup"><span data-stu-id="26531-247">By default, AzCopy starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="26531-248">nombre de Hello d’opérations simultanées est égal huit fois hello le nombre de processeurs que vous avez.</span><span class="sxs-lookup"><span data-stu-id="26531-248">hello number of concurrent operations is equal eight times hello number of processors you have.</span></span> <span data-ttu-id="26531-249">Si vous exécutez AzCopy sur un réseau à faible bande passante, vous pouvez spécifier un nombre inférieur pour--parallèle au niveau tooavoid a échoué en concurrence de la ressource.</span><span class="sxs-lookup"><span data-stu-id="26531-249">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for --parallel-level tooavoid failure caused by resource competition.</span></span>

[!TIP]
><span data-ttu-id="26531-250">liste de tooview hello complète des paramètres de AzCopy, extraire 'azcopy--help' menu.</span><span class="sxs-lookup"><span data-stu-id="26531-250">tooview hello complete list of AzCopy parameters, check out 'azcopy --help' menu.</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="26531-251">Problèmes connus et meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="26531-251">Known issues and best practices</span></span>
### <a name="error-net-core-is-not-found-in-hello-system"></a><span data-ttu-id="26531-252">Erreur : Le .NET Core est introuvable dans le système de hello.</span><span class="sxs-lookup"><span data-stu-id="26531-252">Error: .NET Core is not found in hello system.</span></span>
<span data-ttu-id="26531-253">Si vous rencontrez une erreur indiquant que le .NET Core n’est pas installé dans le système de hello, hello binaire de chemin d’accès toohello .NET Core `dotnet` est absent.</span><span class="sxs-lookup"><span data-stu-id="26531-253">If you encounter an error stating that .NET Core is not installed in hello system, hello PATH toohello .NET Core binary `dotnet` may be missing.</span></span>

<span data-ttu-id="26531-254">Dans commande tooaddress ce problème, recherchez les binaires de .NET Core hello dans le système de hello :</span><span class="sxs-lookup"><span data-stu-id="26531-254">In order tooaddress this issue, find hello .NET Core binary in hello system:</span></span>
```bash
sudo find / -name dotnet
```

<span data-ttu-id="26531-255">Cela retourne hello chemin d’accès toohello dotnet binaire.</span><span class="sxs-lookup"><span data-stu-id="26531-255">This returns hello path toohello dotnet binary.</span></span> 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

<span data-ttu-id="26531-256">Maintenant, ajoutez cette variable de chemin d’accès au chemin d’accès toohello.</span><span class="sxs-lookup"><span data-stu-id="26531-256">Now add this path toohello PATH variable.</span></span> <span data-ttu-id="26531-257">Sudo, modifiez secure_path toocontain hello chemin d’accès toohello dotnet binaire :</span><span class="sxs-lookup"><span data-stu-id="26531-257">For sudo, edit secure_path toocontain hello path toohello dotnet binary:</span></span>
```bash 
sudo visudo
### Append hello path found in hello preceding example too'secure_path' variable
```

<span data-ttu-id="26531-258">Dans cet exemple, la variable secure_path se lit comme :</span><span class="sxs-lookup"><span data-stu-id="26531-258">In this example, secure_path variable reads as:</span></span>

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

<span data-ttu-id="26531-259">Pour l’utilisateur actuel de hello, modifier.bash_profile/.profile tooinclude hello chemin d’accès toohello dotnet binaire dans la variable de chemin d’accès</span><span class="sxs-lookup"><span data-stu-id="26531-259">For hello current user, edit .bash_profile/.profile tooinclude hello path toohello dotnet binary in PATH variable</span></span> 
```bash
vi ~/.bash_profile
### Append hello path found in hello preceding example too'PATH' variable
```

<span data-ttu-id="26531-260">Vérifiez que .NET Core est désormais dans PATH :</span><span class="sxs-lookup"><span data-stu-id="26531-260">Verify that .NET Core is now in PATH:</span></span>
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a><span data-ttu-id="26531-261">Erreur lors de l’installation d’AzCopy</span><span class="sxs-lookup"><span data-stu-id="26531-261">Error Installing AzCopy</span></span>
<span data-ttu-id="26531-262">Si vous rencontrez des problèmes avec l’installation de AzCopy, vous pouvez essayer de toorun AzCopy à l’aide du script d’interpréteur de commandes hello Bonjour extrait `azcopy` dossier.</span><span class="sxs-lookup"><span data-stu-id="26531-262">If you encounter issues with AzCopy installation, you may try toorun AzCopy using hello bash script in hello extracted `azcopy` folder.</span></span>

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="26531-263">Limitation des écritures simultanées lors de la copie des données</span><span class="sxs-lookup"><span data-stu-id="26531-263">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="26531-264">Lorsque vous copiez des objets BLOB ou fichiers avec AzCopy, gardez à l’esprit qu’une autre application peut être modification des données de hello pendant que vous effectuez la copie.</span><span class="sxs-lookup"><span data-stu-id="26531-264">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying hello data while you are copying it.</span></span> <span data-ttu-id="26531-265">Si possible, assurez-vous que vous copiez les données de salutation ne sont pas modifiées pendant l’opération de copie hello.</span><span class="sxs-lookup"><span data-stu-id="26531-265">If possible, ensure that hello data you are copying is not being modified during hello copy operation.</span></span> <span data-ttu-id="26531-266">Par exemple, lors de la copie d’un disque dur virtuel associé à une machine virtuelle Azure, assurez-vous qu’aucune autre application n’écrivez actuellement toohello disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="26531-266">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing toohello VHD.</span></span> <span data-ttu-id="26531-267">Un bon moyen toodo qu'est en louant hello ressource toobe copié.</span><span class="sxs-lookup"><span data-stu-id="26531-267">A good way toodo this is by leasing hello resource toobe copied.</span></span> <span data-ttu-id="26531-268">Ou bien, vous pouvez créez d’abord un instantané de hello disque dur virtuel, puis copiez instantané d’hello.</span><span class="sxs-lookup"><span data-stu-id="26531-268">Alternately, you can create a snapshot of hello VHD first and then copy hello snapshot.</span></span>

<span data-ttu-id="26531-269">Si vous ne pouvez pas empêcher les autres applications à partir de l’écriture de tooblobs ou des fichiers pendant qu’ils sont copiés, puis que vous n’oubliez pas que par hello temps hello tâche se termine, hello ressources copiées peuvent ne plus avoir parité complète avec les ressources de la source hello.</span><span class="sxs-lookup"><span data-stu-id="26531-269">If you cannot prevent other applications from writing tooblobs or files while they are being copied, then keep in mind that by hello time hello job finishes, hello copied resources may no longer have full parity with hello source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="26531-270">Exécuter une instance de AzCopy sur un même ordinateur.</span><span class="sxs-lookup"><span data-stu-id="26531-270">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="26531-271">AzCopy est l’utilisation de hello toomaximize conçu votre ordinateur ressource tooaccelerate hello de transfert de données, nous vous recommandons exécutez qu’une seule instance AzCopy sur un ordinateur et spécifiez l’option de hello `--parallel-level` si vous avez besoin d’opérations simultanées plus.</span><span class="sxs-lookup"><span data-stu-id="26531-271">AzCopy is designed toomaximize hello utilization of your machine resource tooaccelerate hello data transfer, we recommend you run only one AzCopy instance on one machine, and specify hello option `--parallel-level` if you need more concurrent operations.</span></span> <span data-ttu-id="26531-272">Pour plus d’informations, tapez `AzCopy --help parallel-level` à la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="26531-272">For more details, type `AzCopy --help parallel-level` at hello command line.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26531-273">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="26531-273">Next steps</span></span>
<span data-ttu-id="26531-274">Pour plus d’informations sur le stockage Azure et AzCopy, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="26531-274">For more information about Azure Storage and AzCopy, see hello following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="26531-275">Documentation d’Azure Storage :</span><span class="sxs-lookup"><span data-stu-id="26531-275">Azure Storage documentation:</span></span>
* [<span data-ttu-id="26531-276">Introduction tooAzure stockage</span><span class="sxs-lookup"><span data-stu-id="26531-276">Introduction tooAzure Storage</span></span>](../storage-introduction.md)
* [<span data-ttu-id="26531-277">Créer un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="26531-277">Create a storage account</span></span>](../storage-create-storage-account.md)
* [<span data-ttu-id="26531-278">Gérer les ressources de stockage Blob Azure avec l’explorateur de stockage (préversion)</span><span class="sxs-lookup"><span data-stu-id="26531-278">Manage blobs with Storage Explorer</span></span>](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [<span data-ttu-id="26531-279">À l’aide de hello Azure CLI 2.0 avec le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="26531-279">Using hello Azure CLI 2.0 with Azure Storage</span></span>](../storage-azure-cli.md)
* [<span data-ttu-id="26531-280">Comment toouse stockage d’objets Blob à partir de C++</span><span class="sxs-lookup"><span data-stu-id="26531-280">How toouse Blob storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="26531-281">Comment toouse stockage d’objets Blob à partir de Java</span><span class="sxs-lookup"><span data-stu-id="26531-281">How toouse Blob storage from Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="26531-282">Comment toouse stockage d’objets Blob à partir de Node.js</span><span class="sxs-lookup"><span data-stu-id="26531-282">How toouse Blob storage from Node.js</span></span>](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="26531-283">Comment toouse stockage d’objets Blob à partir de Python</span><span class="sxs-lookup"><span data-stu-id="26531-283">How toouse Blob storage from Python</span></span>](../blobs/storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="26531-284">Billets de blog Azure Storage :</span><span class="sxs-lookup"><span data-stu-id="26531-284">Azure Storage blog posts:</span></span>
* <span data-ttu-id="26531-285">[Announcing AzCopy on Linux Preview](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/) (Annonce de la préversion d’AzCopy sur Linux)</span><span class="sxs-lookup"><span data-stu-id="26531-285">[Announcing AzCopy on Linux Preview](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)</span></span>
* [<span data-ttu-id="26531-286">Présentation de la bibliothèque de déplacement des données dans Azure Storage en version préliminaire</span><span class="sxs-lookup"><span data-stu-id="26531-286">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="26531-287">AzCopy : Présentation de la copie synchrone et du type de contenu personnalisé</span><span class="sxs-lookup"><span data-stu-id="26531-287">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="26531-288">AzCopy : Annonce de la disponibilité générale d'AzCopy 3.0 plus version préliminaire d'AzCopy 4.0 avec prise en charge de fichier et de table</span><span class="sxs-lookup"><span data-stu-id="26531-288">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="26531-289">AzCopy : Optimisation pour les scénarios de copie à grande échelle</span><span class="sxs-lookup"><span data-stu-id="26531-289">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="26531-290">AzCopy : Prise en charge des comptes de stockage géo-redondants avec accès en lecture</span><span class="sxs-lookup"><span data-stu-id="26531-290">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* <span data-ttu-id="26531-291">[AzCopy – Transfer data with re-startable mode and SAS Token](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx) (AzCopy : Transfert des données avec mode reprise et jeton SAP)</span><span class="sxs-lookup"><span data-stu-id="26531-291">[AzCopy: Transfer data with restartable mode and SAS token](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)</span></span>
* [<span data-ttu-id="26531-292">AzCopy : Utilisation de copie d'objets blob sur plusieurs comptes</span><span class="sxs-lookup"><span data-stu-id="26531-292">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="26531-293">AzCopy : Chargement/téléchargement des fichiers pour les objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="26531-293">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

