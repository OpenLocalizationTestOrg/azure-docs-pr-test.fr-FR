---
title: importer des disques durs aaaSample workflow tooprep pour une importation/exportation Azure travail - v1 | Documents Microsoft
description: "Consultez une procédure pas à pas de hello complète du processus de préparation des lecteurs pour un travail d’importation Bonjour service Azure Import/Export."
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
ms.openlocfilehash: f836fc6104d8b4ad5660cb110a62f61b40b0b7ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a><span data-ttu-id="639a9-103">Exemple workflow tooprepare les disques durs pour un travail d’importation</span><span class="sxs-lookup"><span data-stu-id="639a9-103">Sample workflow tooprepare hard drives for an import job</span></span>
<span data-ttu-id="639a9-104">Cette rubrique vous guide tout au long des processus de préparation des lecteurs pour un travail d’importation hello.</span><span class="sxs-lookup"><span data-stu-id="639a9-104">This topic walks you through hello complete process of preparing drives for an import job.</span></span>  
  
<span data-ttu-id="639a9-105">Cet exemple importe hello suivant des données dans un compte de stockage Windows Azure nommé `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="639a9-105">This example imports hello following data into a Window Azure storage account named `mystorageaccount`:</span></span>  
  
|<span data-ttu-id="639a9-106">Lieu</span><span class="sxs-lookup"><span data-stu-id="639a9-106">Location</span></span>|<span data-ttu-id="639a9-107">Description</span><span class="sxs-lookup"><span data-stu-id="639a9-107">Description</span></span>|  
|--------------|-----------------|  
|<span data-ttu-id="639a9-108">H:\Video</span><span class="sxs-lookup"><span data-stu-id="639a9-108">H:\Video</span></span>|<span data-ttu-id="639a9-109">Collection de vidéos, 5 To au total.</span><span class="sxs-lookup"><span data-stu-id="639a9-109">A collection of videos, 5 TB in total.</span></span>|  
|<span data-ttu-id="639a9-110">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="639a9-110">H:\Photo</span></span>|<span data-ttu-id="639a9-111">Collection de photos, 30 Go au total.</span><span class="sxs-lookup"><span data-stu-id="639a9-111">A collection of photos, 30 GB in total.</span></span>|  
|<span data-ttu-id="639a9-112">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="639a9-112">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="639a9-113">Image de disque Blu-ray™, 25 Go.</span><span class="sxs-lookup"><span data-stu-id="639a9-113">A Blu-Ray™ disk image, 25 GB.</span></span>|  
|<span data-ttu-id="639a9-114">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="639a9-114">\\\bigshare\john\music</span></span>|<span data-ttu-id="639a9-115">Collection de fichiers de musique sur un partage réseau, 10 Go au total.</span><span class="sxs-lookup"><span data-stu-id="639a9-115">A collection of music files on a network share, 10 GB in total.</span></span>|  
  
<span data-ttu-id="639a9-116">travail d’importation Hello va importer ces données dans hello suivant destinations dans le compte de stockage hello :</span><span class="sxs-lookup"><span data-stu-id="639a9-116">hello import job will import this data into hello following destinations in hello storage account:</span></span>  
  
|<span data-ttu-id="639a9-117">Source</span><span class="sxs-lookup"><span data-stu-id="639a9-117">Source</span></span>|<span data-ttu-id="639a9-118">Répertoire virtuel ou objet blob de destination</span><span class="sxs-lookup"><span data-stu-id="639a9-118">Destination virtual directory or blob</span></span>|  
|------------|-------------------------------------------|  
|<span data-ttu-id="639a9-119">H:\Video</span><span class="sxs-lookup"><span data-stu-id="639a9-119">H:\Video</span></span>|<span data-ttu-id="639a9-120">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="639a9-120">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="639a9-121">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="639a9-121">H:\Photo</span></span>|<span data-ttu-id="639a9-122">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="639a9-122">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="639a9-123">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="639a9-123">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="639a9-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="639a9-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="639a9-125">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="639a9-125">\\\bigshare\john\music</span></span>|<span data-ttu-id="639a9-126">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="639a9-126">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
<span data-ttu-id="639a9-127">Avec ce mappage, hello fichier `H:\Video\Drama\GreatMovie.mov` seront importés toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="639a9-127">With this mapping, hello file `H:\Video\Drama\GreatMovie.mov` will be imported toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>  
  
<span data-ttu-id="639a9-128">Toodetermine suivant, le nombre de disques dur nécessaires, taille de hello de calcul des données de hello :</span><span class="sxs-lookup"><span data-stu-id="639a9-128">Next, toodetermine how many hard drives are needed, compute hello size of hello data:</span></span>  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
<span data-ttu-id="639a9-129">Pour cet exemple, deux disques durs de 3 To devraient suffire.</span><span class="sxs-lookup"><span data-stu-id="639a9-129">For this example, two 3TB hard drives should be sufficient.</span></span> <span data-ttu-id="639a9-130">Toutefois, puisque le répertoire source hello `H:\Video` contient 5 To de données et la capacité de votre disque dur unique est uniquement de 3 To, il est nécessaire toobreak `H:\Video` en deux répertoires de plus petits avant d’exécuter hello outil de Microsoft Azure Import/Export : `H:\Video1` et `H:\Video2`.</span><span class="sxs-lookup"><span data-stu-id="639a9-130">However, since hello source directory `H:\Video` has 5TB of data and your single hard drive's capacity is only 3TB, it's necessary toobreak `H:\Video` into two smaller directories before running hello Microsoft Azure Import/Export Tool: `H:\Video1` and `H:\Video2`.</span></span> <span data-ttu-id="639a9-131">Cette étape génère hello suivant des répertoires sources :</span><span class="sxs-lookup"><span data-stu-id="639a9-131">This step yields hello following source directories:</span></span>  
  
|<span data-ttu-id="639a9-132">Lieu</span><span class="sxs-lookup"><span data-stu-id="639a9-132">Location</span></span>|<span data-ttu-id="639a9-133">Taille</span><span class="sxs-lookup"><span data-stu-id="639a9-133">Size</span></span>|<span data-ttu-id="639a9-134">Répertoire virtuel ou objet blob de destination</span><span class="sxs-lookup"><span data-stu-id="639a9-134">Destination virtual directory or blob</span></span>|  
|--------------|----------|-------------------------------------------|  
|<span data-ttu-id="639a9-135">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="639a9-135">H:\Video1</span></span>|<span data-ttu-id="639a9-136">2,5 To</span><span class="sxs-lookup"><span data-stu-id="639a9-136">2.5TB</span></span>|<span data-ttu-id="639a9-137">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="639a9-137">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="639a9-138">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="639a9-138">H:\Video2</span></span>|<span data-ttu-id="639a9-139">2,5 To</span><span class="sxs-lookup"><span data-stu-id="639a9-139">2.5TB</span></span>|<span data-ttu-id="639a9-140">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="639a9-140">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="639a9-141">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="639a9-141">H:\Photo</span></span>|<span data-ttu-id="639a9-142">30 Go</span><span class="sxs-lookup"><span data-stu-id="639a9-142">30GB</span></span>|<span data-ttu-id="639a9-143">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="639a9-143">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="639a9-144">K:\Temp\FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="639a9-144">K:\Temp\FavoriteMovies.ISO</span></span>|<span data-ttu-id="639a9-145">25 Go</span><span class="sxs-lookup"><span data-stu-id="639a9-145">25GB</span></span>|<span data-ttu-id="639a9-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="639a9-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="639a9-147">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="639a9-147">\\\bigshare\john\music</span></span>|<span data-ttu-id="639a9-148">10 Go</span><span class="sxs-lookup"><span data-stu-id="639a9-148">10GB</span></span>|<span data-ttu-id="639a9-149">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="639a9-149">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
 <span data-ttu-id="639a9-150">Notez que même si hello `H:\Video`active a été fractionné tootwo répertoires, ils pointent toohello même répertoire virtuel de destination dans le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="639a9-150">Note that even though hello `H:\Video`directory has been split tootwo directories, they point toohello same destination virtual directory in hello storage account.</span></span> <span data-ttu-id="639a9-151">De cette manière, tous les fichiers vidéos sont conservés dans un seul `video` conteneur hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="639a9-151">This way, all video files are maintained under a single `video` container in hello storage account.</span></span>  
  
 <span data-ttu-id="639a9-152">Ensuite, hello ci-dessus source répertoires sont uniformément distribuées toohello de deux disques durs :</span><span class="sxs-lookup"><span data-stu-id="639a9-152">Next, hello above source directories are evenly distributed toohello two hard drives:</span></span>  
  
||||  
|-|-|-|  
|<span data-ttu-id="639a9-153">Disque dur</span><span class="sxs-lookup"><span data-stu-id="639a9-153">Hard drive</span></span>|<span data-ttu-id="639a9-154">Répertoires sources</span><span class="sxs-lookup"><span data-stu-id="639a9-154">Source directories</span></span>|<span data-ttu-id="639a9-155">Taille totale</span><span class="sxs-lookup"><span data-stu-id="639a9-155">Total size</span></span>|  
|<span data-ttu-id="639a9-156">Premier disque</span><span class="sxs-lookup"><span data-stu-id="639a9-156">First Drive</span></span>|<span data-ttu-id="639a9-157">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="639a9-157">H:\Video1</span></span>|<span data-ttu-id="639a9-158">2,5 To + 30 Go</span><span class="sxs-lookup"><span data-stu-id="639a9-158">2.5TB + 30GB</span></span>|  
||<span data-ttu-id="639a9-159">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="639a9-159">H:\Photo</span></span>||  
|<span data-ttu-id="639a9-160">Deuxième disque</span><span class="sxs-lookup"><span data-stu-id="639a9-160">Second Drive</span></span>|<span data-ttu-id="639a9-161">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="639a9-161">H:\Video2</span></span>|<span data-ttu-id="639a9-162">2,5 To + 35 Go</span><span class="sxs-lookup"><span data-stu-id="639a9-162">2.5TB + 35GB</span></span>|  
||<span data-ttu-id="639a9-163">K:\Temp\BlueRay.ISO</span><span class="sxs-lookup"><span data-stu-id="639a9-163">K:\Temp\BlueRay.ISO</span></span>||  
||<span data-ttu-id="639a9-164">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="639a9-164">\\\bigshare\john\music</span></span>||  
  
<span data-ttu-id="639a9-165">En outre, vous pouvez définir hello suivant des métadonnées pour tous les fichiers :</span><span class="sxs-lookup"><span data-stu-id="639a9-165">In addition, you can set hello following metadata for all files:</span></span>  
  
-   <span data-ttu-id="639a9-166">**UploadMethod :** Service Windows Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="639a9-166">**UploadMethod:** Windows Azure Import/Export service</span></span>  
  
-   <span data-ttu-id="639a9-167">**DataSetName :** SampleData</span><span class="sxs-lookup"><span data-stu-id="639a9-167">**DataSetName:** SampleData</span></span>  
  
-   <span data-ttu-id="639a9-168">**CreationDate :** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="639a9-168">**CreationDate:** 10/1/2013</span></span>  
  
<span data-ttu-id="639a9-169">métadonnées tooset pour les fichiers de hello importé, créez un fichier texte, `c:\WAImportExport\SampleMetadata.txt`, avec hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="639a9-169">tooset metadata for hello imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with hello following content:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="639a9-170">Vous pouvez également définir des propriétés pour hello `FavoriteMovie.ISO` blob :</span><span class="sxs-lookup"><span data-stu-id="639a9-170">You can also set some properties for hello `FavoriteMovie.ISO` blob:</span></span>  
  
-   <span data-ttu-id="639a9-171">**Content-Type :** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="639a9-171">**Content-Type:** application/octet-stream</span></span>  
  
-   <span data-ttu-id="639a9-172">**Content-MD5 :** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="639a9-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>  
  
-   <span data-ttu-id="639a9-173">**Cache-Control :** no-cache</span><span class="sxs-lookup"><span data-stu-id="639a9-173">**Cache-Control:** no-cache</span></span>  
  
<span data-ttu-id="639a9-174">tooset ces propriétés, créez un fichier texte, `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="639a9-174">tooset these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="639a9-175">Vous êtes maintenant prêt toorun hello outil d’importation/exportation Azure tooprepare hello deux disques durs.</span><span class="sxs-lookup"><span data-stu-id="639a9-175">Now you are ready toorun hello Azure Import/Export Tool tooprepare hello two hard drives.</span></span> <span data-ttu-id="639a9-176">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="639a9-176">Note that:</span></span>  
  
-   <span data-ttu-id="639a9-177">Hello premier disque est monté en tant que lecteur X.</span><span class="sxs-lookup"><span data-stu-id="639a9-177">hello first drive is mounted as drive X.</span></span>  
  
-   <span data-ttu-id="639a9-178">Hello deuxième disque est monté en tant que lecteur Y.</span><span class="sxs-lookup"><span data-stu-id="639a9-178">hello second drive is mounted as drive Y.</span></span>  
  
-   <span data-ttu-id="639a9-179">clé Hello pour le compte de stockage hello `mystorageaccount` est `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span><span class="sxs-lookup"><span data-stu-id="639a9-179">hello key for hello storage account `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span></span>  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a><span data-ttu-id="639a9-180">Préparation du disque à l’importation lorsque des données sont pré-chargées</span><span class="sxs-lookup"><span data-stu-id="639a9-180">Preparing disk for import when data is pre-loaded</span></span>
 
 <span data-ttu-id="639a9-181">Si hello toobe de données importé est déjà présent sur le disque de hello, utilisez hello indicateur /skipwrite.</span><span class="sxs-lookup"><span data-stu-id="639a9-181">If hello data toobe imported is already present on hello disk, use hello flag /skipwrite.</span></span> <span data-ttu-id="639a9-182">Valeur de /t et /srcdir doit pointer disque toohello en cours de préparation pour l’importation.</span><span class="sxs-lookup"><span data-stu-id="639a9-182">Value of /t and /srcdir both should point toohello disk being prepared for import.</span></span> <span data-ttu-id="639a9-183">Si pas toutes hello des données sur disque de hello doit toogo toohello même répertoire virtuel de destination ou racine hello du compte de stockage, exécution hello même commande pour chaque répertoire séparément en conservant la valeur hello /id même pour toutes les séries.</span><span class="sxs-lookup"><span data-stu-id="639a9-183">If not all hello data on hello disk needs toogo toohello same destination virtual directory or root of hello storage account, run hello same command for each directory separately keeping hello value of /id same across all runs.</span></span>

>[!NOTE] 
><span data-ttu-id="639a9-184">Ne spécifiez pas/format qu’il sera Réinitialiser les données de hello sur le disque de hello.</span><span class="sxs-lookup"><span data-stu-id="639a9-184">Do not specify /format as it will wipe hello data on hello disk.</span></span> <span data-ttu-id="639a9-185">Vous pouvez spécifier / chiffrer ou /bk selon si hello disque est déjà chiffré ou non.</span><span class="sxs-lookup"><span data-stu-id="639a9-185">You can specify /encrypt or /bk depending on whether hello disk is already encrypted or not.</span></span> 
>

```
    When data is already present on hello disk for each drive run hello following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a><span data-ttu-id="639a9-186">Session de copie - premier lecteur</span><span class="sxs-lookup"><span data-stu-id="639a9-186">Copy sessions - first drive</span></span>

<span data-ttu-id="639a9-187">Pour le premier lecteur de hello, exécutez hello outil d’importation/exportation Azure source des deux fois les hello toocopy deux répertoires :</span><span class="sxs-lookup"><span data-stu-id="639a9-187">For hello first drive, run hello Azure Import/Export Tool twice toocopy hello two source directories:</span></span>  

<span data-ttu-id="639a9-188">**Première session de copie**</span><span class="sxs-lookup"><span data-stu-id="639a9-188">**First copy session**</span></span>
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

<span data-ttu-id="639a9-189">**Deuxième session de copie**</span><span class="sxs-lookup"><span data-stu-id="639a9-189">**Second copy session**</span></span>

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a><span data-ttu-id="639a9-190">Session de copie - deuxième lecteur</span><span class="sxs-lookup"><span data-stu-id="639a9-190">Copy sessions - second drive</span></span>
 
<span data-ttu-id="639a9-191">Pourquoi second lecteur, exécutez hello outil d’importation/exportation Azure trois fois, une fois que chacun d’eux pour hello source des répertoires et qu’une seule fois pour la version autonome de hello Blu-Ray™ fichier image) :</span><span class="sxs-lookup"><span data-stu-id="639a9-191">For hello second drive, run hello Azure Import/Export Tool three times, once each for hello source directories, and once for hello standalone Blu-Ray™ image file):</span></span>  
  
<span data-ttu-id="639a9-192">**Première session de copie**</span><span class="sxs-lookup"><span data-stu-id="639a9-192">**First copy session**</span></span> 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
<span data-ttu-id="639a9-193">**Deuxième session de copie**</span><span class="sxs-lookup"><span data-stu-id="639a9-193">**Second copy session**</span></span>

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
<span data-ttu-id="639a9-194">**Troisième session de copie**</span><span class="sxs-lookup"><span data-stu-id="639a9-194">**Third copy session**</span></span>  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a><span data-ttu-id="639a9-195">Fin de la session de copie</span><span class="sxs-lookup"><span data-stu-id="639a9-195">Copy session completion</span></span>

<span data-ttu-id="639a9-196">Une fois les sessions de copie hello terminés, vous pouvez vous déconnecter de deux lecteurs de hello à partir de l’ordinateur de copie hello et expédiez-les toohello centre de données Windows Azure approprié.</span><span class="sxs-lookup"><span data-stu-id="639a9-196">Once hello copy sessions have completed, you can disconnect hello two drives from hello copy computer and ship them toohello appropriate Windows Azure data center.</span></span> <span data-ttu-id="639a9-197">Vous allez télécharger les fichiers de journal hello deux, `FirstDrive.jrn` et `SecondDrive.jrn`, lorsque vous créez un travail d’importation hello Bonjour [portail de gestion Windows Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="639a9-197">You'll upload hello two journal files, `FirstDrive.jrn` and `SecondDrive.jrn`, when you create hello import job in hello [Windows Azure Management Portal](https://manage.windowsazure.com/).</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="639a9-198">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="639a9-198">Next steps</span></span>

* [<span data-ttu-id="639a9-199">Préparation des disques durs pour un travail d’importation</span><span class="sxs-lookup"><span data-stu-id="639a9-199">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="639a9-200">Référence rapide pour les commandes fréquemment utilisées</span><span class="sxs-lookup"><span data-stu-id="639a9-200">Quick reference for frequently used commands</span></span>](storage-import-export-tool-quick-reference-v1.md) 
