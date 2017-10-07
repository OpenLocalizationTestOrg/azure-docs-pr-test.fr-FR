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
ms.openlocfilehash: eb77831a88c16c14838179a6432ddb06503067dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a>Exemple workflow tooprepare les disques durs pour un travail d’importation
Cette rubrique vous guide tout au long des processus de préparation des lecteurs pour un travail d’importation hello.  
  
Cet exemple importe hello suivant des données dans un compte de stockage Windows Azure nommé `mystorageaccount`:  
  
|Lieu|Description|  
|--------------|-----------------|  
|H:\Video|Collection de vidéos, 5 To au total.|  
|H:\Photo|Collection de photos, 30 Go au total.|  
|K:\Temp\FavoriteMovie.ISO|Image de disque Blu-ray™, 25 Go.|  
|\\\bigshare\john\music|Collection de fichiers de musique sur un partage réseau, 10 Go au total.|  
  
travail d’importation Hello importe ces données dans hello suivant destinations dans le compte de stockage hello :  
  
|Source|Répertoire virtuel ou objet blob de destination|  
|------------|-------------------------------------------|  
|H:\Video|https://mystorageaccount.blob.core.windows.net/video|  
|H:\Photo|https://mystorageaccount.blob.core.windows.net/photo|  
|K:\Temp\FavoriteMovie.ISO|https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO|  
|\\\bigshare\john\music|https://mystorageaccount.blob.core.windows.net/music|  
  
Avec ce mappage, hello fichier `H:\Video\Drama\GreatMovie.mov` toohello importé BLOB `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.  
  
Toodetermine suivant, le nombre de disques dur nécessaires, taille de hello de calcul des données de hello :  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
Pour cet exemple, deux disques durs de 3 To devraient suffire. Toutefois, puisque le répertoire source hello `H:\Video` contient 5 To de données et la capacité de votre disque dur unique est uniquement de 3 To, il est nécessaire toobreak `H:\Video` en deux répertoires de plus petits : `H:\Video1` et `H:\Video2`, avant d’en cours d’exécution hello Microsoft Outil d’importation/exportation Azure. Cette étape génère hello suivant des répertoires sources :  
  
|Lieu|Taille|Répertoire virtuel ou objet blob de destination|  
|--------------|----------|-------------------------------------------|  
|H:\Video1|2,5 To|https://mystorageaccount.blob.core.windows.net/video|  
|H:\Video2|2,5 To|https://mystorageaccount.blob.core.windows.net/video|  
|H:\Photo|30 Go|https://mystorageaccount.blob.core.windows.net/photo|  
|K:\Temp\FavoriteMovies.ISO|25 Go|https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO|  
|\\\bigshare\john\music|10 Go|https://mystorageaccount.blob.core.windows.net/music|  
  
 Bien que hello `H:\Video`active a été fractionné tootwo répertoires, ils pointent toohello même répertoire virtuel de destination dans le compte de stockage hello. De cette manière, tous les fichiers vidéos sont conservés dans un seul `video` conteneur hello compte de stockage.  
  
 Ensuite, les répertoires sources précédente hello sont distribuées uniformément toohello de deux disques durs :  
  
||||  
|-|-|-|  
|Disque dur|Répertoires sources|Taille totale|  
|Premier disque|H:\Video1|2,5 To + 30 Go|  
||H:\Photo||  
|Deuxième disque|H:\Video2|2,5 To + 35 Go|  
||K:\Temp\BlueRay.ISO||  
||\\\bigshare\john\music||  
  
En outre, vous pouvez définir hello suivant des métadonnées pour tous les fichiers :  
  
-   **UploadMethod :** Service Windows Azure Import/Export  
  
-   **DataSetName :** SampleData  
  
-   **CreationDate :** 10/1/2013  
  
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
  
-   **Content-Type :** application/octet-stream  
  
-   **Content-MD5 :** Q2hlY2sgSW50ZWdyaXR5IQ==  
  
-   **Cache-Control :** no-cache  
  
tooset ces propriétés, créez un fichier texte, `c:\WAImportExport\SampleProperties.txt`:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
Vous êtes maintenant prêt toorun hello outil d’importation/exportation Azure tooprepare hello deux disques durs. Notez les points suivants :  
  
-   Hello premier disque est monté en tant que lecteur X.  
  
-   Hello deuxième disque est monté en tant que lecteur Y.  
  
-   clé Hello pour le compte de stockage hello `mystorageaccount` est `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a>Préparation du disque à l’importation lorsque des données sont pré-chargées
 
 Si hello toobe de données importé est déjà présent sur le disque de hello, utilisez hello indicateur /skipwrite. valeur Hello /t et /srcdir doit les deux disques point toohello en cours de préparation pour l’importation. Si tous les hello toobe de données importé ne va pas toohello même répertoire virtuel de destination ou racine hello du compte de stockage, exécution hello même commande pour chaque répertoire de destination séparément, en conservant la valeur hello /id hello même entre toutes les séries.

>[!NOTE] 
>Ne spécifiez pas/format qu’il sera Réinitialiser les données de hello sur le disque de hello. Vous pouvez spécifier / chiffrer ou /bk selon si hello disque est déjà chiffré ou non. 
>

```
    When data is already present on hello disk for each drive run hello following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a>Session de copie - premier lecteur

Pour le premier lecteur de hello, exécutez hello outil d’importation/exportation Azure source des deux fois les hello toocopy deux répertoires :  

**Première session de copie**
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

**Deuxième session de copie**

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a>Session de copie - deuxième lecteur
 
Pourquoi second lecteur, exécutez hello outil d’importation/exportation Azure trois fois, une fois que chacun d’eux pour hello source des répertoires et qu’une seule fois pour la version autonome de hello Blu-Ray™ fichier image) :  
  
**Première session de copie** 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
**Deuxième session de copie**

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
**Troisième session de copie**  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a>Fin de la session de copie

Une fois les sessions de copie hello terminés, vous pouvez vous déconnecter de deux lecteurs de hello à partir de l’ordinateur de copie hello et expédiez-les toohello centre de données Windows Azure approprié. Télécharger des fichiers de journal hello deux, `FirstDrive.jrn` et `SecondDrive.jrn`, lorsque vous créez un travail d’importation hello Bonjour [portail Windows Azure](https://manage.windowsazure.com/).  
  
## <a name="next-steps"></a>Étapes suivantes

* [Préparation des disques durs pour un travail d’importation](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Référence rapide pour les commandes fréquemment utilisées](../storage-import-export-tool-quick-reference-v1.md) 
