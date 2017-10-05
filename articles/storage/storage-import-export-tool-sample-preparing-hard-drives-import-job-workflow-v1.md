---
title: "Exemple de workflow pour préparer des disques durs pour un travail d’importation Azure Import/Export - v1 | Microsoft Docs"
description: "Obtenez la procédure pas à pas relative au processus de préparation des disques à un travail d’importation dans le service Azure Import/Export."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 6eb1b1b7-c69f-4365-b5ef-3cd5e05eb72a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 313f8c1f3962a943b4c98c530c324ff28aa84c10
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="sample-workflow-to-prepare-hard-drives-for-an-import-job"></a><span data-ttu-id="5eaac-103">Exemple de workflow pour préparer des disques durs à un travail d’importation</span><span class="sxs-lookup"><span data-stu-id="5eaac-103">Sample workflow to prepare hard drives for an import job</span></span>
<span data-ttu-id="5eaac-104">Cette rubrique vous guide tout au long du processus de préparation des disques pour un travail d’importation.</span><span class="sxs-lookup"><span data-stu-id="5eaac-104">This topic walks you through the complete process of preparing drives for an import job.</span></span>  
  
<span data-ttu-id="5eaac-105">Cet exemple importe les données suivantes dans un compte de stockage Azure Windows nommé `mystorageaccount` :</span><span class="sxs-lookup"><span data-stu-id="5eaac-105">This example imports the following data into a Window Azure storage account named `mystorageaccount`:</span></span>  
  
|<span data-ttu-id="5eaac-106">Lieu</span><span class="sxs-lookup"><span data-stu-id="5eaac-106">Location</span></span>|<span data-ttu-id="5eaac-107">Description</span><span class="sxs-lookup"><span data-stu-id="5eaac-107">Description</span></span>|  
|--------------|-----------------|  
|<span data-ttu-id="5eaac-108">H:\Video</span><span class="sxs-lookup"><span data-stu-id="5eaac-108">H:\Video</span></span>|<span data-ttu-id="5eaac-109">Collection de vidéos, 5 To au total.</span><span class="sxs-lookup"><span data-stu-id="5eaac-109">A collection of videos, 5 TB in total.</span></span>|  
|<span data-ttu-id="5eaac-110">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="5eaac-110">H:\Photo</span></span>|<span data-ttu-id="5eaac-111">Collection de photos, 30 Go au total.</span><span class="sxs-lookup"><span data-stu-id="5eaac-111">A collection of photos, 30 GB in total.</span></span>|  
|<span data-ttu-id="5eaac-112">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="5eaac-112">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="5eaac-113">Image de disque Blu-ray™, 25 Go.</span><span class="sxs-lookup"><span data-stu-id="5eaac-113">A Blu-Ray™ disk image, 25 GB.</span></span>|  
|<span data-ttu-id="5eaac-114">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="5eaac-114">\\\bigshare\john\music</span></span>|<span data-ttu-id="5eaac-115">Collection de fichiers de musique sur un partage réseau, 10 Go au total.</span><span class="sxs-lookup"><span data-stu-id="5eaac-115">A collection of music files on a network share, 10 GB in total.</span></span>|  
  
<span data-ttu-id="5eaac-116">Le travail d’importation importe ces données dans les destinations suivantes dans le compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="5eaac-116">The import job will import this data into the following destinations in the storage account:</span></span>  
  
|<span data-ttu-id="5eaac-117">Source</span><span class="sxs-lookup"><span data-stu-id="5eaac-117">Source</span></span>|<span data-ttu-id="5eaac-118">Répertoire virtuel ou objet blob de destination</span><span class="sxs-lookup"><span data-stu-id="5eaac-118">Destination virtual directory or blob</span></span>|  
|------------|-------------------------------------------|  
|<span data-ttu-id="5eaac-119">H:\Video</span><span class="sxs-lookup"><span data-stu-id="5eaac-119">H:\Video</span></span>|<span data-ttu-id="5eaac-120">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="5eaac-120">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="5eaac-121">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="5eaac-121">H:\Photo</span></span>|<span data-ttu-id="5eaac-122">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="5eaac-122">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="5eaac-123">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="5eaac-123">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="5eaac-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="5eaac-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="5eaac-125">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="5eaac-125">\\\bigshare\john\music</span></span>|<span data-ttu-id="5eaac-126">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="5eaac-126">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
<span data-ttu-id="5eaac-127">Avec ce mappage, le fichier `H:\Video\Drama\GreatMovie.mov` sera importé dans l’objet blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="5eaac-127">With this mapping, the file `H:\Video\Drama\GreatMovie.mov` will be imported to the blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>  
  
<span data-ttu-id="5eaac-128">Ensuite, pour déterminer le nombre de disques durs nécessaires, calculez la taille des données :</span><span class="sxs-lookup"><span data-stu-id="5eaac-128">Next, to determine how many hard drives are needed, compute the size of the data:</span></span>  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
<span data-ttu-id="5eaac-129">Pour cet exemple, deux disques durs de 3 To devraient suffire.</span><span class="sxs-lookup"><span data-stu-id="5eaac-129">For this example, two 3TB hard drives should be sufficient.</span></span> <span data-ttu-id="5eaac-130">Toutefois, puisque le répertoire source `H:\Video` contient 5 To de données et que la capacité de votre disque dur unique est de 3 To seulement, il est nécessaire de diviser `H:\Video` en deux répertoires plus petits avant d’exécuter l’outil Microsoft Azure Import/Export : `H:\Video1` et `H:\Video2`.</span><span class="sxs-lookup"><span data-stu-id="5eaac-130">However, since the source directory `H:\Video` has 5TB of data and your single hard drive's capacity is only 3TB, it's necessary to break `H:\Video` into two smaller directories before running the Microsoft Azure Import/Export Tool: `H:\Video1` and `H:\Video2`.</span></span> <span data-ttu-id="5eaac-131">Cette étape génère les répertoires sources suivants :</span><span class="sxs-lookup"><span data-stu-id="5eaac-131">This step yields the following source directories:</span></span>  
  
|<span data-ttu-id="5eaac-132">Lieu</span><span class="sxs-lookup"><span data-stu-id="5eaac-132">Location</span></span>|<span data-ttu-id="5eaac-133">Taille</span><span class="sxs-lookup"><span data-stu-id="5eaac-133">Size</span></span>|<span data-ttu-id="5eaac-134">Répertoire virtuel ou objet blob de destination</span><span class="sxs-lookup"><span data-stu-id="5eaac-134">Destination virtual directory or blob</span></span>|  
|--------------|----------|-------------------------------------------|  
|<span data-ttu-id="5eaac-135">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="5eaac-135">H:\Video1</span></span>|<span data-ttu-id="5eaac-136">2,5 To</span><span class="sxs-lookup"><span data-stu-id="5eaac-136">2.5TB</span></span>|<span data-ttu-id="5eaac-137">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="5eaac-137">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="5eaac-138">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="5eaac-138">H:\Video2</span></span>|<span data-ttu-id="5eaac-139">2,5 To</span><span class="sxs-lookup"><span data-stu-id="5eaac-139">2.5TB</span></span>|<span data-ttu-id="5eaac-140">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="5eaac-140">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="5eaac-141">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="5eaac-141">H:\Photo</span></span>|<span data-ttu-id="5eaac-142">30 Go</span><span class="sxs-lookup"><span data-stu-id="5eaac-142">30GB</span></span>|<span data-ttu-id="5eaac-143">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="5eaac-143">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="5eaac-144">K:\Temp\FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="5eaac-144">K:\Temp\FavoriteMovies.ISO</span></span>|<span data-ttu-id="5eaac-145">25 Go</span><span class="sxs-lookup"><span data-stu-id="5eaac-145">25GB</span></span>|<span data-ttu-id="5eaac-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="5eaac-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="5eaac-147">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="5eaac-147">\\\bigshare\john\music</span></span>|<span data-ttu-id="5eaac-148">10 Go</span><span class="sxs-lookup"><span data-stu-id="5eaac-148">10GB</span></span>|<span data-ttu-id="5eaac-149">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="5eaac-149">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
 <span data-ttu-id="5eaac-150">Notez que même si le répertoire `H:\Video` a été divisé en deux répertoires, ils pointent tous deux vers le même répertoire virtuel de destination dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="5eaac-150">Note that even though the `H:\Video`directory has been split to two directories, they point to the same destination virtual directory in the storage account.</span></span> <span data-ttu-id="5eaac-151">De cette façon, tous les fichiers vidéo sont conservés dans un seul conteneur `video` au sein du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="5eaac-151">This way, all video files are maintained under a single `video` container in the storage account.</span></span>  
  
 <span data-ttu-id="5eaac-152">Ensuite, les répertoires sources ci-dessus sont répartis uniformément sur les deux disques durs :</span><span class="sxs-lookup"><span data-stu-id="5eaac-152">Next, the above source directories are evenly distributed to the two hard drives:</span></span>  
  
||||  
|-|-|-|  
|<span data-ttu-id="5eaac-153">Disque dur</span><span class="sxs-lookup"><span data-stu-id="5eaac-153">Hard drive</span></span>|<span data-ttu-id="5eaac-154">Répertoires sources</span><span class="sxs-lookup"><span data-stu-id="5eaac-154">Source directories</span></span>|<span data-ttu-id="5eaac-155">Taille totale</span><span class="sxs-lookup"><span data-stu-id="5eaac-155">Total size</span></span>|  
|<span data-ttu-id="5eaac-156">Premier disque</span><span class="sxs-lookup"><span data-stu-id="5eaac-156">First Drive</span></span>|<span data-ttu-id="5eaac-157">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="5eaac-157">H:\Video1</span></span>|<span data-ttu-id="5eaac-158">2,5 To + 30 Go</span><span class="sxs-lookup"><span data-stu-id="5eaac-158">2.5TB + 30GB</span></span>|  
||<span data-ttu-id="5eaac-159">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="5eaac-159">H:\Photo</span></span>||  
|<span data-ttu-id="5eaac-160">Deuxième disque</span><span class="sxs-lookup"><span data-stu-id="5eaac-160">Second Drive</span></span>|<span data-ttu-id="5eaac-161">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="5eaac-161">H:\Video2</span></span>|<span data-ttu-id="5eaac-162">2,5 To + 35 Go</span><span class="sxs-lookup"><span data-stu-id="5eaac-162">2.5TB + 35GB</span></span>|  
||<span data-ttu-id="5eaac-163">K:\Temp\BlueRay.ISO</span><span class="sxs-lookup"><span data-stu-id="5eaac-163">K:\Temp\BlueRay.ISO</span></span>||  
||<span data-ttu-id="5eaac-164">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="5eaac-164">\\\bigshare\john\music</span></span>||  
  
<span data-ttu-id="5eaac-165">En outre, vous pouvez définir les métadonnées suivantes pour tous les fichiers :</span><span class="sxs-lookup"><span data-stu-id="5eaac-165">In addition, you can set the following metadata for all files:</span></span>  
  
-   <span data-ttu-id="5eaac-166">**UploadMethod :** Service Windows Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="5eaac-166">**UploadMethod:** Windows Azure Import/Export service</span></span>  
  
-   <span data-ttu-id="5eaac-167">**DataSetName :** SampleData</span><span class="sxs-lookup"><span data-stu-id="5eaac-167">**DataSetName:** SampleData</span></span>  
  
-   <span data-ttu-id="5eaac-168">**CreationDate :** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="5eaac-168">**CreationDate:** 10/1/2013</span></span>  
  
<span data-ttu-id="5eaac-169">Pour définir les métadonnées pour les fichiers importés, créez un fichier texte, `c:\WAImportExport\SampleMetadata.txt`, avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="5eaac-169">To set metadata for the imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with the following content:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="5eaac-170">Vous pouvez également définir des propriétés pour l’objet blob `FavoriteMovie.ISO` :</span><span class="sxs-lookup"><span data-stu-id="5eaac-170">You can also set some properties for the `FavoriteMovie.ISO` blob:</span></span>  
  
-   <span data-ttu-id="5eaac-171">**Content-Type :** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="5eaac-171">**Content-Type:** application/octet-stream</span></span>  
  
-   <span data-ttu-id="5eaac-172">**Content-MD5 :** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="5eaac-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>  
  
-   <span data-ttu-id="5eaac-173">**Cache-Control :** no-cache</span><span class="sxs-lookup"><span data-stu-id="5eaac-173">**Cache-Control:** no-cache</span></span>  
  
<span data-ttu-id="5eaac-174">Pour définir ces propriétés, créez un fichier texte, `c:\WAImportExport\SampleProperties.txt` :</span><span class="sxs-lookup"><span data-stu-id="5eaac-174">To set these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="5eaac-175">Vous êtes maintenant prêt à exécuter l’outil Azure Import/Export pour préparer les deux disques durs.</span><span class="sxs-lookup"><span data-stu-id="5eaac-175">Now you are ready to run the Azure Import/Export Tool to prepare the two hard drives.</span></span> <span data-ttu-id="5eaac-176">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="5eaac-176">Note that:</span></span>  
  
-   <span data-ttu-id="5eaac-177">Le premier disque est monté en tant que disque X.</span><span class="sxs-lookup"><span data-stu-id="5eaac-177">The first drive is mounted as drive X.</span></span>  
  
-   <span data-ttu-id="5eaac-178">Le deuxième disque est monté en tant que disque Y.</span><span class="sxs-lookup"><span data-stu-id="5eaac-178">The second drive is mounted as drive Y.</span></span>  
  
-   <span data-ttu-id="5eaac-179">La clé du compte de stockage `mystorageaccount` est `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span><span class="sxs-lookup"><span data-stu-id="5eaac-179">The key for the storage account `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span></span>  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a><span data-ttu-id="5eaac-180">Préparation du disque à l’importation lorsque des données sont pré-chargées</span><span class="sxs-lookup"><span data-stu-id="5eaac-180">Preparing disk for import when data is pre-loaded</span></span>
 
 <span data-ttu-id="5eaac-181">Si les données à importer sont déjà présentes sur le disque, utilisez l’indicateur /skipwrite.</span><span class="sxs-lookup"><span data-stu-id="5eaac-181">If the data to be imported is already present on the disk, use the flag /skipwrite.</span></span> <span data-ttu-id="5eaac-182">La valeur de /t et de /srcdir doit pointer vers le disque en cours de préparation à l’importation.</span><span class="sxs-lookup"><span data-stu-id="5eaac-182">Value of /t and /srcdir both should point to the disk being prepared for import.</span></span> <span data-ttu-id="5eaac-183">S’il n’est pas nécessaire que toutes les données sur le disque soient dirigées vers le même répertoire virtuel de destination ou la même racine du compte de stockage, exécutez la même commande pour chaque répertoire séparément en conservant la même valeur /id pour toutes les exécutions.</span><span class="sxs-lookup"><span data-stu-id="5eaac-183">If not all the data on the disk needs to go to the same destination virtual directory or root of the storage account, run the same command for each directory separately keeping the value of /id same across all runs.</span></span>

>[!NOTE] 
><span data-ttu-id="5eaac-184">Ne spécifiez pas la valeur /format car elle efface les données sur le disque.</span><span class="sxs-lookup"><span data-stu-id="5eaac-184">Do not specify /format as it will wipe the data on the disk.</span></span> <span data-ttu-id="5eaac-185">Vous pouvez spécifier la valeur /encrypt ou /bk selon que le disque est déjà chiffré ou non.</span><span class="sxs-lookup"><span data-stu-id="5eaac-185">You can specify /encrypt or /bk depending on whether the disk is already encrypted or not.</span></span> 
>

```
    When data is already present on the disk for each drive run the following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a><span data-ttu-id="5eaac-186">Session de copie - premier lecteur</span><span class="sxs-lookup"><span data-stu-id="5eaac-186">Copy sessions - first drive</span></span>

<span data-ttu-id="5eaac-187">Pour le premier disque, exécutez l’outil Azure Import/Export deux fois pour copier les deux répertoires sources :</span><span class="sxs-lookup"><span data-stu-id="5eaac-187">For the first drive, run the Azure Import/Export Tool twice to copy the two source directories:</span></span>  

<span data-ttu-id="5eaac-188">**Première session de copie**</span><span class="sxs-lookup"><span data-stu-id="5eaac-188">**First copy session**</span></span>
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

<span data-ttu-id="5eaac-189">**Deuxième session de copie**</span><span class="sxs-lookup"><span data-stu-id="5eaac-189">**Second copy session**</span></span>

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a><span data-ttu-id="5eaac-190">Session de copie - deuxième lecteur</span><span class="sxs-lookup"><span data-stu-id="5eaac-190">Copy sessions - second drive</span></span>
 
<span data-ttu-id="5eaac-191">Pour le deuxième disque, exécutez l’outil Azure Import/Export trois fois (une fois pour chaque répertoire source et une fois pour le fichier d’image Blu-Ray™ autonome) :</span><span class="sxs-lookup"><span data-stu-id="5eaac-191">For the second drive, run the Azure Import/Export Tool three times, once each for the source directories, and once for the standalone Blu-Ray™ image file):</span></span>  
  
<span data-ttu-id="5eaac-192">**Première session de copie**</span><span class="sxs-lookup"><span data-stu-id="5eaac-192">**First copy session**</span></span> 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
<span data-ttu-id="5eaac-193">**Deuxième session de copie**</span><span class="sxs-lookup"><span data-stu-id="5eaac-193">**Second copy session**</span></span>

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
<span data-ttu-id="5eaac-194">**Troisième session de copie**</span><span class="sxs-lookup"><span data-stu-id="5eaac-194">**Third copy session**</span></span>  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a><span data-ttu-id="5eaac-195">Fin de la session de copie</span><span class="sxs-lookup"><span data-stu-id="5eaac-195">Copy session completion</span></span>

<span data-ttu-id="5eaac-196">Une fois les sessions de copie terminées, vous pouvez déconnecter les deux disques de l’ordinateur de copie et les expédier au centre de données Windows Azure approprié.</span><span class="sxs-lookup"><span data-stu-id="5eaac-196">Once the copy sessions have completed, you can disconnect the two drives from the copy computer and ship them to the appropriate Windows Azure data center.</span></span> <span data-ttu-id="5eaac-197">Vous allez télécharger les deux fichiers journaux, `FirstDrive.jrn` et `SecondDrive.jrn`, lors de la création du travail d’importation dans le [portail de gestion Windows Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="5eaac-197">You'll upload the two journal files, `FirstDrive.jrn` and `SecondDrive.jrn`, when you create the import job in the [Windows Azure Management Portal](https://manage.windowsazure.com/).</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="5eaac-198">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5eaac-198">Next steps</span></span>

* [<span data-ttu-id="5eaac-199">Préparation des disques durs pour un travail d’importation</span><span class="sxs-lookup"><span data-stu-id="5eaac-199">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="5eaac-200">Référence rapide pour les commandes fréquemment utilisées</span><span class="sxs-lookup"><span data-stu-id="5eaac-200">Quick reference for frequently used commands</span></span>](storage-import-export-tool-quick-reference-v1.md) 
