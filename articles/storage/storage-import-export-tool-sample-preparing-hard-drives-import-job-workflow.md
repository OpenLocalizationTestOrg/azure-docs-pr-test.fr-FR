---
title: "tâche d’importation de disques durs aaaSample workflow tooprep pour une importation/exportation Azure | Documents Microsoft"
description: "Consultez une procédure pas à pas de hello complète du processus de préparation des lecteurs pour un travail d’importation Bonjour service Azure Import/Export."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: muralikk
ms.openlocfilehash: 560220b7dc9f87416f1fec1ff30fa5cd65812ce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a><span data-ttu-id="56bba-103">Exemple workflow tooprepare les disques durs pour un travail d’importation</span><span class="sxs-lookup"><span data-stu-id="56bba-103">Sample workflow tooprepare hard drives for an import job</span></span>

<span data-ttu-id="56bba-104">Cet article vous guide tout au long des processus de préparation des lecteurs pour un travail d’importation hello.</span><span class="sxs-lookup"><span data-stu-id="56bba-104">This article walks you through hello complete process of preparing drives for an import job.</span></span>

## <a name="sample-data"></a><span data-ttu-id="56bba-105">Exemples de données</span><span class="sxs-lookup"><span data-stu-id="56bba-105">Sample data</span></span>

<span data-ttu-id="56bba-106">Cet exemple importe hello suivant des données dans un compte de stockage Azure nommé `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="56bba-106">This example imports hello following data into an Azure storage account named `mystorageaccount`:</span></span>

|<span data-ttu-id="56bba-107">Lieu</span><span class="sxs-lookup"><span data-stu-id="56bba-107">Location</span></span>|<span data-ttu-id="56bba-108">Description</span><span class="sxs-lookup"><span data-stu-id="56bba-108">Description</span></span>|<span data-ttu-id="56bba-109">Taille des données</span><span class="sxs-lookup"><span data-stu-id="56bba-109">Data size</span></span>|
|--------------|-----------------|-----|
|<span data-ttu-id="56bba-110">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="56bba-110">H:\Video\\</span></span> |<span data-ttu-id="56bba-111">Collection de vidéos</span><span class="sxs-lookup"><span data-stu-id="56bba-111">A collection of videos</span></span>|<span data-ttu-id="56bba-112">12 To</span><span class="sxs-lookup"><span data-stu-id="56bba-112">12 TB</span></span>|
|<span data-ttu-id="56bba-113">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="56bba-113">H:\Photo\\</span></span> |<span data-ttu-id="56bba-114">Collection de photos</span><span class="sxs-lookup"><span data-stu-id="56bba-114">A collection of photos</span></span>|<span data-ttu-id="56bba-115">30 Go</span><span class="sxs-lookup"><span data-stu-id="56bba-115">30 GB</span></span>|
|<span data-ttu-id="56bba-116">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="56bba-116">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="56bba-117">Image de disque Blu-ray™</span><span class="sxs-lookup"><span data-stu-id="56bba-117">A Blu-Ray™ disk image</span></span>|<span data-ttu-id="56bba-118">25 Go</span><span class="sxs-lookup"><span data-stu-id="56bba-118">25 GB</span></span>|
|<span data-ttu-id="56bba-119">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="56bba-119">\\\bigshare\john\music\\</span></span>|<span data-ttu-id="56bba-120">Collection de fichiers de musique sur un partage réseau</span><span class="sxs-lookup"><span data-stu-id="56bba-120">A collection of music files on a network share</span></span>|<span data-ttu-id="56bba-121">10 Go</span><span class="sxs-lookup"><span data-stu-id="56bba-121">10 GB</span></span>|

## <a name="storage-account-destinations"></a><span data-ttu-id="56bba-122">Destinations dans le compte de stockage</span><span class="sxs-lookup"><span data-stu-id="56bba-122">Storage account destinations</span></span>

<span data-ttu-id="56bba-123">travail d’importation Hello va importer les données de hello en hello suivant destinations dans le compte de stockage hello :</span><span class="sxs-lookup"><span data-stu-id="56bba-123">hello import job will import hello data into hello following destinations in hello storage account:</span></span>

|<span data-ttu-id="56bba-124">Source</span><span class="sxs-lookup"><span data-stu-id="56bba-124">Source</span></span>|<span data-ttu-id="56bba-125">Répertoire virtuel ou objet blob de destination</span><span class="sxs-lookup"><span data-stu-id="56bba-125">Destination virtual directory or blob</span></span>|
|------------|-------------------------------------------|
|<span data-ttu-id="56bba-126">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="56bba-126">H:\Video\\</span></span> |<span data-ttu-id="56bba-127">video/</span><span class="sxs-lookup"><span data-stu-id="56bba-127">video/</span></span>|
|<span data-ttu-id="56bba-128">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="56bba-128">H:\Photo\\</span></span> |<span data-ttu-id="56bba-129">photo/</span><span class="sxs-lookup"><span data-stu-id="56bba-129">photo/</span></span>|
|<span data-ttu-id="56bba-130">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="56bba-130">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="56bba-131">favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="56bba-131">favorite/FavoriteMovies.ISO</span></span>|
|<span data-ttu-id="56bba-132">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="56bba-132">\\\bigshare\john\music\\</span></span> |<span data-ttu-id="56bba-133">music</span><span class="sxs-lookup"><span data-stu-id="56bba-133">music</span></span>|

<span data-ttu-id="56bba-134">Avec ce mappage, hello fichier `H:\Video\Drama\GreatMovie.mov` seront importés toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="56bba-134">With this mapping, hello file `H:\Video\Drama\GreatMovie.mov` will be imported toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>

## <a name="determine-hard-drive-requirements"></a><span data-ttu-id="56bba-135">Déterminer la configuration requise du disque dur</span><span class="sxs-lookup"><span data-stu-id="56bba-135">Determine hard drive requirements</span></span>

<span data-ttu-id="56bba-136">Toodetermine suivant, le nombre de disques dur nécessaires, taille de hello de calcul des données de hello :</span><span class="sxs-lookup"><span data-stu-id="56bba-136">Next, toodetermine how many hard drives are needed, compute hello size of hello data:</span></span>

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

<span data-ttu-id="56bba-137">Pour cet exemple, deux disques durs de 8 To devraient suffire.</span><span class="sxs-lookup"><span data-stu-id="56bba-137">For this example, two 8TB hard drives should be sufficient.</span></span> <span data-ttu-id="56bba-138">Toutefois, puisque le répertoire source hello `H:\Video` a 12 To de données et la capacité de votre disque dur unique est uniquement 8 To, vous serez en mesure de toospecify dans hello suivants moyen Bonjour **driveset.csv** fichier :</span><span class="sxs-lookup"><span data-stu-id="56bba-138">However, since hello source directory `H:\Video` has 12TB of data and your single hard drive's capacity is only 8TB, you will be able toospecify this in hello following way in hello **driveset.csv** file:</span></span>

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
<span data-ttu-id="56bba-139">outil de Hello distribuer les données sur deux disques durs de manière optimisée.</span><span class="sxs-lookup"><span data-stu-id="56bba-139">hello tool will distribute data across two hard drives in an optimized way.</span></span>

## <a name="attach-drives-and-configure-hello-job"></a><span data-ttu-id="56bba-140">Attacher des disques et de configurer la tâche de hello</span><span class="sxs-lookup"><span data-stu-id="56bba-140">Attach drives and configure hello job</span></span>
<span data-ttu-id="56bba-141">Vous allez attacher à la fois ordinateur toohello de disques et créer des volumes.</span><span class="sxs-lookup"><span data-stu-id="56bba-141">You will attach both disks toohello machine and create volumes.</span></span> <span data-ttu-id="56bba-142">Créez ensuite le fichier **dataset.csv** :</span><span class="sxs-lookup"><span data-stu-id="56bba-142">Then author **dataset.csv** file:</span></span>
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

<span data-ttu-id="56bba-143">En outre, vous pouvez définir hello suivant des métadonnées pour tous les fichiers :</span><span class="sxs-lookup"><span data-stu-id="56bba-143">In addition, you can set hello following metadata for all files:</span></span>

* <span data-ttu-id="56bba-144">**UploadMethod :** Service Windows Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="56bba-144">**UploadMethod:** Windows Azure Import/Export service</span></span>
* <span data-ttu-id="56bba-145">**DataSetName :** SampleData</span><span class="sxs-lookup"><span data-stu-id="56bba-145">**DataSetName:** SampleData</span></span>
* <span data-ttu-id="56bba-146">**CreationDate :** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="56bba-146">**CreationDate:** 10/1/2013</span></span>

<span data-ttu-id="56bba-147">métadonnées tooset pour les fichiers de hello importé, créez un fichier texte, `c:\WAImportExport\SampleMetadata.txt`, avec hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="56bba-147">tooset metadata for hello imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with hello following content:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="56bba-148">Vous pouvez également définir des propriétés pour hello `FavoriteMovie.ISO` blob :</span><span class="sxs-lookup"><span data-stu-id="56bba-148">You can also set some properties for hello `FavoriteMovie.ISO` blob:</span></span>

* <span data-ttu-id="56bba-149">**Content-Type :** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="56bba-149">**Content-Type:** application/octet-stream</span></span>
* <span data-ttu-id="56bba-150">**Content-MD5 :** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="56bba-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>
* <span data-ttu-id="56bba-151">**Cache-Control :** no-cache</span><span class="sxs-lookup"><span data-stu-id="56bba-151">**Cache-Control:** no-cache</span></span>

<span data-ttu-id="56bba-152">tooset ces propriétés, créez un fichier texte, `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="56bba-152">tooset these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-hello-azure-importexport-tool-waimportexportexe"></a><span data-ttu-id="56bba-153">Exécution hello outil d’importation/exportation Azure (WAImportExport.exe)</span><span class="sxs-lookup"><span data-stu-id="56bba-153">Run hello Azure Import/Export Tool (WAImportExport.exe)</span></span>

<span data-ttu-id="56bba-154">Vous êtes maintenant prêt toorun hello outil d’importation/exportation Azure tooprepare hello deux disques durs.</span><span class="sxs-lookup"><span data-stu-id="56bba-154">Now you are ready toorun hello Azure Import/Export Tool tooprepare hello two hard drives.</span></span>

<span data-ttu-id="56bba-155">**Pourquoi la première session :**</span><span class="sxs-lookup"><span data-stu-id="56bba-155">**For hello first session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

<span data-ttu-id="56bba-156">Si des données doivent toobe ajouté, créez un autre fichier de jeu de données (même format que Initialdataset).</span><span class="sxs-lookup"><span data-stu-id="56bba-156">If any more data needs toobe added, create another dataset file (same format as Initialdataset).</span></span>

<span data-ttu-id="56bba-157">**Pourquoi la deuxième session :**</span><span class="sxs-lookup"><span data-stu-id="56bba-157">**For hello second session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

<span data-ttu-id="56bba-158">Une fois les sessions de copie hello terminés, vous pouvez vous déconnecter de deux lecteurs de hello à partir de l’ordinateur de copie hello et expédiez-les centre de données Azure approprié toohello.</span><span class="sxs-lookup"><span data-stu-id="56bba-158">Once hello copy sessions have completed, you can disconnect hello two drives from hello copy computer and ship them toohello appropriate Azure data center.</span></span> <span data-ttu-id="56bba-159">Vous allez télécharger les fichiers de journal hello deux, `<FirstDriveSerialNumber>.xml` et `<SecondDriveSerialNumber>.xml`, lorsque vous créez un travail d’importation hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="56bba-159">You'll upload hello two journal files, `<FirstDriveSerialNumber>.xml` and `<SecondDriveSerialNumber>.xml`, when you create hello import job in hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56bba-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="56bba-160">Next steps</span></span>

* [<span data-ttu-id="56bba-161">Préparation des disques durs pour un travail d’importation</span><span class="sxs-lookup"><span data-stu-id="56bba-161">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import.md)
* [<span data-ttu-id="56bba-162">Référence rapide pour les commandes fréquemment utilisées</span><span class="sxs-lookup"><span data-stu-id="56bba-162">Quick reference for frequently used commands</span></span>](storage-import-export-tool-quick-reference.md)