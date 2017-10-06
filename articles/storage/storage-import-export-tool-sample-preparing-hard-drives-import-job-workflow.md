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
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a>Exemple workflow tooprepare les disques durs pour un travail d’importation

Cet article vous guide tout au long des processus de préparation des lecteurs pour un travail d’importation hello.

## <a name="sample-data"></a>Exemples de données

Cet exemple importe hello suivant des données dans un compte de stockage Azure nommé `mystorageaccount`:

|Lieu|Description|Taille des données|
|--------------|-----------------|-----|
|H:\Video\ |Collection de vidéos|12 To|
|H:\Photo\ |Collection de photos|30 Go|
|K:\Temp\FavoriteMovie.ISO|Image de disque Blu-ray™|25 Go|
|\\\bigshare\john\music\|Collection de fichiers de musique sur un partage réseau|10 Go|

## <a name="storage-account-destinations"></a>Destinations dans le compte de stockage

travail d’importation Hello va importer les données de hello en hello suivant destinations dans le compte de stockage hello :

|Source|Répertoire virtuel ou objet blob de destination|
|------------|-------------------------------------------|
|H:\Video\ |video/|
|H:\Photo\ |photo/|
|K:\Temp\FavoriteMovie.ISO|favorite/FavoriteMovies.ISO|
|\\\bigshare\john\music\ |music|

Avec ce mappage, hello fichier `H:\Video\Drama\GreatMovie.mov` seront importés toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.

## <a name="determine-hard-drive-requirements"></a>Déterminer la configuration requise du disque dur

Toodetermine suivant, le nombre de disques dur nécessaires, taille de hello de calcul des données de hello :

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

Pour cet exemple, deux disques durs de 8 To devraient suffire. Toutefois, puisque le répertoire source hello `H:\Video` a 12 To de données et la capacité de votre disque dur unique est uniquement 8 To, vous serez en mesure de toospecify dans hello suivants moyen Bonjour **driveset.csv** fichier :

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
outil de Hello distribuer les données sur deux disques durs de manière optimisée.

## <a name="attach-drives-and-configure-hello-job"></a>Attacher des disques et de configurer la tâche de hello
Vous allez attacher à la fois ordinateur toohello de disques et créer des volumes. Créez ensuite le fichier **dataset.csv** :
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

En outre, vous pouvez définir hello suivant des métadonnées pour tous les fichiers :

* **UploadMethod :** Service Windows Azure Import/Export
* **DataSetName :** SampleData
* **CreationDate :** 10/1/2013

métadonnées tooset pour les fichiers de hello importé, créez un fichier texte, `c:\WAImportExport\SampleMetadata.txt`, avec hello suivant le contenu :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

Vous pouvez également définir des propriétés pour hello `FavoriteMovie.ISO` blob :

* **Content-Type :** application/octet-stream
* **Content-MD5 :** Q2hlY2sgSW50ZWdyaXR5IQ==
* **Cache-Control :** no-cache

tooset ces propriétés, créez un fichier texte, `c:\WAImportExport\SampleProperties.txt`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-hello-azure-importexport-tool-waimportexportexe"></a>Exécution hello outil d’importation/exportation Azure (WAImportExport.exe)

Vous êtes maintenant prêt toorun hello outil d’importation/exportation Azure tooprepare hello deux disques durs.

**Pourquoi la première session :**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

Si des données doivent toobe ajouté, créez un autre fichier de jeu de données (même format que Initialdataset).

**Pourquoi la deuxième session :**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

Une fois les sessions de copie hello terminés, vous pouvez vous déconnecter de deux lecteurs de hello à partir de l’ordinateur de copie hello et expédiez-les centre de données Azure approprié toohello. Vous allez télécharger les fichiers de journal hello deux, `<FirstDriveSerialNumber>.xml` et `<SecondDriveSerialNumber>.xml`, lorsque vous créez un travail d’importation hello Bonjour portail Azure.

## <a name="next-steps"></a>Étapes suivantes

* [Préparation des disques durs pour un travail d’importation](storage-import-export-tool-preparing-hard-drives-import.md)
* [Référence rapide pour les commandes fréquemment utilisées](storage-import-export-tool-quick-reference.md)
