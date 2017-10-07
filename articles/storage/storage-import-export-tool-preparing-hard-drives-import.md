---
title: "tâche d’importation aaaPreparing de disques durs pour une importation/exportation Azure | Documents Microsoft"
description: "Découvrez comment tooprepare les disques durs à l’aide de hello WAImportExport outil toocreate un travail d’importation pour hello service Azure Import/Export."
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
ms.date: 06/29/2017
ms.author: muralikk
ms.openlocfilehash: 3f247a9efee29da2d18140353edc9dd7103a0761
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-hard-drives-for-an-import-job"></a>Préparation des disques durs pour un travail d’importation

Bonjour outil WAImportExport est hello lecteur outil de préparation et réparation que vous pouvez utiliser avec hello [service Microsoft Azure Import/Export](storage-import-export-service.md). Vous pouvez utiliser cet outil toocopy données toohello disques durs que vous allez tooship tooan centre de données Azure. Lorsqu’une tâche d’importation est terminé, vous pouvez utiliser cette toorepair outil tous les objets BLOB qui ont été endommagés, étaient manquants ou qui est en conflit avec d’autres objets BLOB. Après avoir reçu les lecteurs hello d’un travail d’exportation terminé, vous pouvez utiliser cette toorepair outil tous les fichiers qui ont été endommagés ou manquants sur des lecteurs hello. Dans cet article, nous passer en revue l’utilisation de hello de cet outil.

## <a name="prerequisites"></a>Composants requis

### <a name="requirements-for-waimportexportexe"></a>Configuration requise pour WAImportExport.exe

- **Configuration de l’ordinateur**
  - Windows 7, Windows Server 2008 R2 ou système d’exploitation Windows plus récent
  - .NET framework 4 installé. Consultez [FAQ](#faq) sur la façon de toocheck si .net Framework est installé sur l’ordinateur de hello.
- **Clé de compte de stockage** -vous devez au moins une des clés de compte hello hello compte de stockage.

### <a name="preparing-disk-for-import-job"></a>Préparation de disques en vue du travail d’importation

- **BitLocker -** BitLocker doit être activé sur l’outil de WAImportExport hello machine en cours d’exécution hello. Consultez hello [FAQ](#faq) procédure tooenable BitLocker.
- **Disques** accessibles à partir de l’ordinateur sur lequel l’outil WAImportExport est exécuté. Consultez la section [Forum Aux Questions](#faq) pour savoir comment spécifier les disques.
- **Fichiers sources** -fichiers hello vous envisagez de tooimport doivent être accessibles à partir de l’ordinateur de copie hello, qu’ils soient sur un partage réseau ou un disque dur local.

### <a name="repairing-a-partially-failed-import-job"></a>Réparation d’un travail d’importation en échec partiel

- **Copiez le fichier journal** généré lorsque le service Azure Import/Export copie les données entre le compte de stockage et le disque. Ils se trouvent dans votre compte de stockage cible.

### <a name="repairing-a-partially-failed-export-job"></a>Réparation d’un travail d’exportation en échec partiel

- **Copiez le fichier journal** généré lorsque le service Azure Import/Export copie les données entre le compte de stockage et le disque. Il se trouve dans votre compte de stockage source.
- **Fichier manifeste** : (facultatif) situé sur le disque exporté, renvoyé par Microsoft.

## <a name="download-and-install-waimportexport"></a>Télécharger et installer WAImportExport

Télécharger hello [version la plus récente de WAImportExport.exe](https://www.microsoft.com/download/details.aspx?id=55280). Extraire le répertoire de tooa contenu compressé hello sur votre ordinateur.

La tâche suivante est toocreate les fichiers CSV.

## <a name="prepare-hello-dataset-csv-file"></a>Préparer un fichier CSV hello dataset

### <a name="what-is-dataset-csv"></a>Qu’est-ce que le fichier dataset.csv ?

Fichier CSV de DataSet est la valeur hello/jeu-données indicateur est un fichier CSV qui contient une liste de répertoires et/ou une liste de fichiers toobe copié tootarget lecteurs. Hello première étape toocreating un travail d’importation est toodetermine les répertoires et fichiers que vous allez tooimport. Il peut s’agir d’une liste de répertoires, d’une liste de fichiers uniques ou d’une combinaison des deux. Lorsqu’un répertoire est inclus, tous les fichiers dans le répertoire de hello et ses sous-répertoires feront partie du travail d’importation hello.

Pour chaque répertoire ou fichier toobe importé, vous devez identifier un répertoire virtuel de destination ou d’un objet blob dans hello service Blob Azure. Vous utiliserez ces cibles en tant qu’outil de WAImportExport toohello entrées. Répertoires doivent être délimités par caractère hello barre oblique « / ».

Hello tableau suivant présente quelques exemples de cibles blob :

| Fichier ou répertoire source | Répertoire virtuel ou objet blob cibles |
| --- | --- |
| H:\Video | https://mystorageaccount.blob.core.windows.net/video |
| H:\Photo | https://mystorageaccount.blob.core.windows.net/photo |
| K:\Temp\FavoriteVideo.ISO | https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO |
| \\myshare\john\music | https://mystorageaccount.blob.core.windows.net/music |

### <a name="sample-datasetcsv"></a>Exemple de fichier dataset.csv

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
"F:\50M_original\100M_1.csv.txt","containername/100M_1.csv.txt",BlockBlob,rename,"None",None
"F:\50M_original\","containername/",BlockBlob,rename,"None",None
```

### <a name="dataset-csv-file-fields"></a>Champs du fichier dataset.csv

| Champ | Description |
| --- | --- |
| Chemin de base | **[Obligatoire]**<br/>valeur Hello de ce paramètre représente la source hello où se trouve hello toobe de données importée. outil de Hello sera copie de manière récursive toutes les données situées sous ce chemin d’accès.<br><br/>**Valeurs autorisées**: cela a toobe un chemin d’accès valide sur l’ordinateur local ou un chemin d’accès de partage valide et doit être accessible par l’utilisateur de hello. chemin d’accès du répertoire Hello doit être un chemin d’accès absolu (pas un chemin d’accès relatif). Si le chemin d’accès hello se termine par «\\«, il représente un répertoire autre un chemin d’accès se terminant sans »\\» représente un fichier.<br/>Aucune expression régulière n’est autorisée dans ce champ. Si le chemin d’accès hello contient des espaces, placez-le dans « ».<br><br/>**Exemple** : "c:\Directory\c\Directory\File.txt"<br>"\\\\FBaseFilesharePath.domain.net\sharename\directory\"  |
| DstBlobPathOrPrefix | **[Obligatoire]**<br/> Hello chemin d’accès toohello répertoire virtuel de destination dans votre compte de stockage Windows Azure. répertoire virtuel de Hello peut ou ne peut pas exister. S’il n’existe pas, le service Import/Export le crée.<br/><br/>Lorsque vous spécifiez des répertoires virtuels de destination ou des objets BLOB, être toouse que les noms de conteneur valide. N’oubliez pas que les noms de conteneur doivent être en minuscules. Pour connaître les règles d’affectation de noms aux conteneurs, consultez [Naming and Referencing Containers, Blobs, and Metadata (Affectation de noms et références aux conteneurs, blobs et métadonnées)](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata). Si une seule racine est spécifiée, structure de répertoires hello de source de hello est répliquée dans le conteneur d’objets blob destination hello. Si vous souhaitez qu’une autre structure de répertoire hello dans la source, plusieurs lignes de mappage dans le fichier CSV<br/><br/>Vous pouvez spécifier un conteneur ou un préfixe d’objet blob comme music/70s/. répertoire de destination Hello doit commencer par le nom du conteneur hello, suivi par une barre oblique « / » et peut éventuellement inclure un répertoire virtuel d’objets blob qui se termine par « / ».<br/><br/>Lorsque le conteneur de destination hello est le conteneur racine de hello, vous devez spécifier explicitement le conteneur racine de hello, y compris hello barre oblique, comme $root /. Étant donné que les objets BLOB sous le conteneur racine de hello ne peut pas inclure « / » dans leurs noms, tous les sous-répertoires dans le répertoire source hello ne seront pas copiés lorsque le répertoire de destination hello est le conteneur racine de hello.<br/><br/>**Exemple**<br/>Si le chemin d’accès des objets blob de destination hello est https://mystorageaccount.blob.core.windows.net/video, valeur hello de ce champ peut être vidéo /  |
| /BlobType | **[Facultatif]**  block &amp;#124; page<br/>Pour l’instant, le service Import/Export prend en charge 2 types d’objet blob. les objets blob de pages et les objets blob de blocs. Par défaut, tous les fichiers sont importés comme des objets blob de blocs. Et \*.vhd et \*.vhdx seront importées comme Page BlobsThere est une limite hello-objet blob de blocs et objet blob de pages taille autorisée. Pour plus d’informations, consultez la page [Objectifs de performance et évolutivité d’Azure Storage](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files).  |
| Disposition | **[Facultatif]** rename &amp;#124; no-overwrite &amp;#124; overwrite <br/> Ce champ spécifie le comportement de copie hello pendant l’importation ex Lorsque les données sont téléchargées toohello compte de stockage à partir du disque de hello. Les options disponibles sont : changement de nom &#124;. Voulez-vous la remplacer &#124; non-overwrite. Valeurs par défaut trop « rename » si rien n’est spécifié. <br/><br/>**Rename** : si un objet portant le même nom est présent, l’outil crée une copie dans la destination.<br/>Remplacer : de remplace le fichier de hello du fichier le plus récent. fichier Hello avec la dernière modification de wins.<br/>**Non-remplacer**: ignore l’écriture hello fichier si elle existe déjà.|
| MetadataFile | **[Facultatif]** <br/>champ de toothis valeur Hello est un fichier de métadonnées hello qui peut être fourni si hello un a besoin de métadonnées de hello toopreserve d’objets de hello ou fournir des métadonnées personnalisées. Fichier de métadonnées chemin d’accès toohello pour les objets BLOB de destination hello. Pour plus d’informations, consultez [Format de fichier de propriétés et de métadonnées du service d’importation/exportation](storage-import-export-file-format-metadata-and-properties.md) |
| PropertiesFile | **[Facultatif]** <br/>Fichier de propriétés chemin d’accès toohello pour les objets BLOB de destination hello. Pour plus d’informations, consultez [Format de fichier de propriétés et de métadonnées du service d’importation/exportation](storage-import-export-file-format-metadata-and-properties.md). |

## <a name="prepare-initialdriveset-or-additionaldriveset-csv-file"></a>Préparer le fichier CSV InitialDriveSet ou AdditionalDriveSet

### <a name="what-is-driveset-csv"></a>Qu’est-ce que le fichier driveset.csv ?

Bonjour hello /InitialDriveSet ou /AdditionalDriveSet l’indicateur de valeur est un fichier CSV qui contient la liste hello de disques toowhich hello les lettres de lecteurs mappés pour que hello outil peut correctement hello une liste de choix de toobe disques préparé. Si la taille des données hello est supérieure à une taille de disque unique, outil WAImportExport de hello distribue les données de salutation sur plusieurs disques inscrites dans ce fichier CSV de manière optimisée.

Il existe aucune limite du nombre de hello de données hello de disques ne peut être écrites tooin une session unique. outil de Hello distribue des données en fonction de la taille du disque et la taille du dossier. Il sélectionne disque hello qui correspond le mieux optimisés pour hello-taille de l’objet. Hello lorsque le téléchargement de données compte de stockage toohello sera la structure de répertoire convergé toohello précédent qui a été spécifié dans le fichier de jeu de données. Dans l’ordre toocreate un volume partagé de cluster driveset, suivez les étapes de hello ci-dessous.

### <a name="create-basic-volume-and-assign-drive-letter"></a>Créer le volume de base et lui attribuer une lettre

Dans la commande toocreate un volume de base et affecter une lettre de lecteur, en suivant les instructions de hello pour « Création de partition plus simple » à [vue d’ensemble de gestion des disques](https://technet.microsoft.com/library/cc754936.aspx).

### <a name="sample-initialdriveset-and-additionaldriveset-csv-file"></a>Exemple de fichier CSV InitialDriveSet ou AdditionalDriveSet

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631
H,Format,SilentMode,Encrypt,
```

### <a name="driveset-csv-file-fields"></a>Champs du fichier driveset.csv

| Champs | Valeur |
| --- | --- |
| DriveLetter | **[Obligatoire]**<br/> Chaque disque qui est fournie outil toohello en tant que destination de hello doit avoir un volume NTFS simple d’et une lettre de lecteur affectée tooit.<br/> <br/>**Exemple** : R ou r |
| FormatOption | **[Obligatoire]**  Format &amp;#124; AlreadyFormatted<br/><br/> **Format**: la spécification de ce met en forme toutes les données hello sur le disque de hello. <br/>**AlreadyFormatted**: outil de hello ignorera la mise en forme lorsque cette valeur est spécifiée. |
| SilentOrPromptOnFormat | **[Obligatoire]** SilentMode &amp;#124; PromptOnFormat<br/><br/>**SilentMode**: cette valeur permettra l’outil de hello toorun utilisateur en Mode silencieux. <br/>**PromptOnFormat**: outil de hello invitera hello utilisateur tooconfirm si l’action de hello est prévue à chaque format.<br/><br/>Si ce paramètre n’est pas défini, la commande ne s’exécute pas et affiche le message d’erreur « Incorrect value for SilentOrPromptOnFormat: none » (« Valeur incorrecte de SilentOrPromptOnFormat : aucune ») |
| Chiffrement | **[Obligatoire]** Encrypt &amp;#124; AlreadyEncrypted<br/> valeur Hello de ce champ décide quels tooencrypt disque et qui ne pas. <br/><br/>**Chiffrer**: outil formatera le lecteur de hello. Si la valeur du champ de « FormatOption » est « Format » cette valeur est requise toobe « Encrypt ». Si vous spécifiez « AlreadyEncrypted » dans ce cas, l’erreur « When Format is specified, Encrypt must also be specified (Lorsque Format est spécifié, Encrypt doit aussi être spécifié) » s’affiche.<br/>**AlreadyEncrypted**: outil déchiffrera lecteur hello à l’aide de hello BitLockerKey fourni dans le champ de « ExistingBitLockerKey ». Si la valeur du champ « FormatOption » est « AlreadyFormatted », cette valeur peut être « Encrypt » ou « AlreadyEncrypted ». |
| ExistingBitLockerKey | **[Obligatoire]** Si la valeur du champ « Encryption » est « AlreadyEncrypted »,<br/> valeur Hello de ce champ est la clé BitLocker hello associé au disque hello. <br/><br/>Ce champ doit être laissé vide si la valeur hello du champ de « Chiffrement » est « Encrypt ».  Si la clé BitLocker est spécifiée, le message d’erreur « Bitlocker Key should not be specified (La clé BitLocker ne doit pas être spécifiée) » s’affiche.<br/>  **Exemple** : 060456-014509-132033-080300-252615-584177-672089-411631|

##  <a name="preparing-disk-for-import-job"></a>Préparation de disques en vue du travail d’importation

lecteurs tooprepare pour un travail d’importation, appelez hello WAImportExport avec hello **PrepImport** commande. Les paramètres inclus dépend de si cela est hello première session de copie ou d’une session de copie suivante.

### <a name="first-session"></a>Première session

Première Session de copie tooCopy un outil de WAImportExport de disque (en fonction de ce qui est spécifié dans le fichier CSV) Single/Multiple Active tooa unique/plusieurs commandes PrepImport pour hello tout d’abord copier les répertoires toocopy de session et/ou de fichiers avec une nouvelle session de copie :

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>] DataSet:<dataset.csv>
```

**Exemple :**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:\*\*\*\*\*\*\*\*\*\*\*\*\* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

### <a name="add-data-in-subsequent-session"></a>Ajouter des données dans la session suivante

Dans les sessions de copie suivantes, il est inutile des paramètres initiaux de toospecify hello. Vous devez toouse hello même fichier journal dans l’ordre pour hello outil tooremember là où elle se Bonjour session précédente. état Hello de session de copie hello est écrit le fichier de feuille de toohello. Voici hello de syntaxe pour une copie suivantes et autres répertoires de session toocopy ou les fichiers :

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<DifferentSessionId>  [DataSet:<differentdataset.csv>]
```

**Exemple :**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

### <a name="add-drives-toolatest-session"></a>Ajouter des lecteurs toolatest session

Si les données de salutation ne tiennent pas dans les lecteurs spécifiés dans InitialDriveset, un peut utiliser hello outil tooadd des lecteurs supplémentaires toosame la session de copie. 

>[!NOTE] 
>id de session Hello doit correspondre à des id de session précédente hello. Fichier journal doit correspondre au hello celui spécifié dans la session précédente.
>
```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AdditionalDriveSet:<newdriveset.csv>
```

**Exemple :**

```
WAImportExport.exe PrepImport /j:SameJournalTest.jrn /id:session#2  /AdditionalDriveSet:driveset-2.csv
```

### <a name="abort-hello-latest-session"></a>Abandonner hello dernière session :

Si une session de copie est interrompue et il n’est pas possible de tooresume (par exemple, si un répertoire source est inaccessible), vous devez annuler hello session active afin qu’elle peut être annulée précédent et nouvelles sessions de copie peuvent être démarrées :

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AbortSession
```

**Exemple :**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /AbortSession
```

Hello uniquement dernière session de copie s’est terminé anormalement, peut être annulée. Notez que vous ne pouvez pas abandonner hello première session de copie pour un lecteur. Au lieu de cela, vous devez redémarrer la session de copie hello avec un nouveau fichier journal.

### <a name="resume-a-latest-interrupted-session"></a>Reprise de la dernière session interrompue

Si une session de copie est interrompue pour une raison quelconque, vous pouvez le reprendre en exécutant l’outil de hello avec le fichier journal hello spécifié :

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /ResumeSession
```

**Exemple :**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /ResumeSession
```

> [!IMPORTANT] 
> Lorsque vous reprenez une session de copie, ne modifiez pas répertoires et fichiers de données sources hello en ajoutant ou supprimant des fichiers.

## <a name="waimportexport-parameters"></a>Paramètres de WAImportExport

| parameters | Description |
| --- | --- |
|     /j:&lt;Fichier_journal&gt;  | **Obligatoire**<br/> Chemin d’accès fichier journal toohello. Un fichier journal suit un ensemble de disques et enregistrements hello progression lors de la préparation de ces lecteurs. fichier de journal Hello doit toujours être spécifié.  |
|     /LogDir:&lt;Répertoire_journaux&gt;  | **Facultatif**. répertoire de journal Hello.<br/> Fichiers journaux détaillés, ainsi que certains fichiers temporaires seront écrites toothis active. Si la valeur n’est pas spécifié, Active directory sera utilisé comme répertoire de journal hello. Hello répertoire du journal peut être spécifié qu’une seule fois pour hello même fichier journal.  |
|     /id:&lt;ID_session&gt;  | **Obligatoire**<br/> Hello Id de session utilisé tooidentify une session de copie. Il est utilisé tooensure précise de récupération d’une session de copie interrompue.  |
|     /ResumeSession  | facultatif. Si hello dernière session de copie s’est arrêtée anormalement, ce paramètre peut être spécifié tooresume hello session.   |
|     /AbortSession  | facultatif. Si hello dernière session de copie s’est arrêtée anormalement, ce paramètre peut être spécifié tooabort hello session.  |
|     /sn:&lt;Nom_compte_stockage&gt;  | **Obligatoire**<br/> Applicable uniquement à RepairImport et RepairExport. nom Hello hello du compte de stockage.  |
|     /sk:&lt;Clé_compte_stockage&gt;  | **Obligatoire**<br/> clé Hello hello du compte de stockage. |
|     /InitialDriveSet:&lt;driveset.csv&gt;  | **Requis** lors de l’exécution hello première session de copie<br/> Un fichier CSV qui contient une liste de lecteurs tooprepare.  |
|     /AdditionalDriveSet:&lt;driveset.csv&gt; | **Requis**. Lors de l’ajout de disques toocurrent la session de copie. <br/> Un fichier CSV qui contient une liste d’autres lecteurs toobe ajouté.  |
|      /r:&lt;RepairFile&gt; | **Obligatoire** Applicable uniquement à RepairImport et RepairExport.<br/> Fichier toohello de chemin d’accès pour le suivi de la progression de la réparation. Chaque disque ne doit avoir qu’un fichier de réparation.  |
|     /d:&lt;Répertoires_cibles&gt; | **Requis**. Applicable uniquement à RepairImport et RepairExport. Pour RepairImport, un ou plusieurs toorepair séparés par des points-virgules des répertoires ; Pour RepairExport, toorepair d’un répertoire, par exemple, répertoire racine du lecteur de hello.  |
|     /CopyLogFile:&lt;Fichier_journal_copie_disque&gt; | **Obligatoire** Applicable uniquement à RepairImport et RepairExport. Fichier journal de chemin d’accès toohello lecteur copie (verbose ou erreur).  |
|     /ManifestFile:&lt;Fichier_manifeste_disque&gt; | **Obligatoire** Applicable uniquement à RepairExport.<br/> Fichier manifeste du lecteur de toohello chemin d’accès.  |
|     /PathMapFile:&lt;Fichier_mappage_chemin_disque&gt; | **Facultatif**. Applicable uniquement à RepairImport.<br/> Chemin d’accès fichier toohello contenant les mappages de fichier chemins d’accès relatif toohello lecteur racine toolocations de fichiers réels (délimité par des tabulations). Spécifié pour la première fois, il indique des chemins d’accès avec des cibles vides, ce qui signifie qu’ils sont introuvables dans les répertoires cibles, que leur accès est refusé, que leur nom est incorrect ou qu’ils existent dans plusieurs répertoires. fichier de mappage de chemin d’accès Hello peut être modifié manuellement tooinclude chemins d’accès cible correct de hello et spécifiées de nouveau des chemins d’accès du fichier de hello tooresolve hello outil correctement.  |
|     /ExportBlobListFile:&lt;Fichier_liste_blobs_à_exporter&gt; | **Requis**. Applicable uniquement à PreviewExport.<br/> Chemin d’accès toohello XML du fichier contenant la liste des chemins d’accès de l’objet blob ou préfixes de chemin d’accès pour toobe d’objets BLOB hello exportée d’objets blob. format de fichier Hello est même hello comme format d’objet blob hello blob liste Bonjour opération Put Job de l’API REST du service importation/exportation hello.  |
|     /DriveSize:&lt;Taille_disque&gt; | **Requis**. Applicable uniquement à PreviewExport.<br/>  Taille de toobe de lecteurs utilisé pour l’exportation. Par exemple, 500 Go, 1,5 To. Remarque : 1 Go = 1 000 000 000 octets ; 1 To = 1 000 000 000 000 octets  |
|     /DataSet:&lt;dataset.csv&gt; | **Obligatoire**<br/> Un fichier CSV qui contient une liste de répertoires et/ou une liste de fichiers toobe copiés tootarget lecteurs.  |
|     /silentmode  | **Facultatif**.<br/> Si non spécifié, il rappelle vous hello exigence de disques et que vous avez besoin de votre toocontinue de confirmation.  |

## <a name="tool-output"></a>Sortie de l’outil

### <a name="sample-drive-manifest-file"></a>Exemple de fichier manifeste de disque

```xml
<?xml version="1.0" encoding="UTF-8"?>
<DriveManifest Version="2011-MM-DD">
   <Drive>
      <DriveId>drive-id</DriveId>
      <StorageAccountKey>storage-account-key</StorageAccountKey>
      <ClientCreator>client-creator</ClientCreator>
      <!-- First Blob List -->
      <BlobList Id="session#1-0">
         <!-- Global properties and metadata that applies tooall blobs -->
         <MetadataPath Hash="md5-hash">global-metadata-file-path</MetadataPath>
         <PropertiesPath Hash="md5-hash">global-properties-file-path</PropertiesPath>
         <!-- First Blob -->
         <Blob>
            <BlobPath>blob-path-relative-to-account</BlobPath>
            <FilePath>file-path-relative-to-transfer-disk</FilePath>
            <ClientData>client-data</ClientData>
            <Length>content-length</Length>
            <ImportDisposition>import-disposition</ImportDisposition>
            <!-- page-range-list-or-block-list -->
            <!-- page-range-list -->
            <PageRangeList>
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
            </PageRangeList>
            <!-- block-list -->
            <BlockList>
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
            </BlockList>
            <MetadataPath Hash="md5-hash">metadata-file-path</MetadataPath>
            <PropertiesPath Hash="md5-hash">properties-file-path</PropertiesPath>
         </Blob>
      </BlobList>
   </Drive>
</DriveManifest>
```

### <a name="sample-journal-file-xml-for-each-drive"></a>Exemple de fichier journal (XML) pour chaque lecteur

```xml
[BeginUpdateRecord][2016/11/01 21:22:25.379][Type:ActivityRecord]
ActivityId: DriveInfo
DriveState: [BeginValue]
<?xml version="1.0" encoding="UTF-8"?>
<Drive>
   <DriveId>drive-id</DriveId>
   <BitLockerKey>*******</BitLockerKey>
   <ManifestFile>\DriveManifest.xml</ManifestFile>
   <ManifestHash>D863FE44F861AE0DA4DCEAEEFFCCCE68</ManifestHash> </Drive>
[EndValue]
SaveCommandOutput: Completed
[EndUpdateRecord]
```

### <a name="sample-journal-file-jrn-for-session-that-records-hello-trail-of-sessions"></a>Exemple de fichier journal (feuille) pour la session qui enregistre la piste hello de sessions

```
[BeginUpdateRecord][2016/11/02 18:24:14.735][Type:NewJournalFile]
VocabularyVersion: 2013-02-01
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.749][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
LogDirectory: F:\logs
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.754][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
StorageAccountKey: *******
[EndUpdateRecord]
```

## <a name="faq"></a>Forum Aux Questions

### <a name="general"></a>Généralités

#### <a name="what-is-waimportexport-tool"></a>Présentation de l’outil WAImportExport

outil de WAImportExport Hello est hello lecteur outil de préparation et réparation que vous pouvez utiliser avec hello service Microsoft Azure Import/Export. Vous pouvez utiliser cet outil toocopy données toohello disques durs que vous allez centre de données Azure tooship tooan. Lorsqu’une tâche d’importation est terminé, vous pouvez utiliser cette toorepair outil tous les objets BLOB qui ont été endommagés, étaient manquants ou qui est en conflit avec d’autres objets BLOB. Après avoir reçu les lecteurs hello d’un travail d’exportation terminé, vous pouvez utiliser cette toorepair outil tous les fichiers qui ont été endommagés ou manquants sur des lecteurs hello.

#### <a name="how-does-hello-waimportexport-tool-work-on-multiple-source-dir-and-disks"></a>Fonctionnement des fait hello outil WAImportExport sur plusieurs sources et des disques ?

Si la taille des données hello est supérieure à la taille du disque hello, outil de WAImportExport hello sera distribuer des données de hello sur des disques de hello de manière optimisée. copier les données Hello toomultiple disques est possible en parallèle ou séquentiellement. Il existe aucune limite du nombre de hello de données hello de disques ne peut être écrites toosimultaneously. outil de Hello distribue des données en fonction de la taille du disque et la taille du dossier. Il sélectionne disque hello qui correspond le mieux optimisés pour hello-taille de l’objet. Hello lorsque le téléchargement de données compte de stockage toohello sont convergée précédent toohello spécifié la structure de répertoires.

#### <a name="where-can-i-find-previous-version-of-waimportexport-tool"></a>Où puis-je trouver la version précédente de l’outil WAImportExport ?

L’outil WAImportExport propose toutes les fonctionnalités de l’outil WAImportExport V1. Outil WAImportExport permet toospecify d’utilisateurs de plusieurs sources et les lecteurs de toomultiple d’écriture. En outre, un peut gérer facilement plusieurs emplacements source à partir de laquelle les données de salutation doivent toobe copié dans un fichier CSV. Toutefois, dans le cas, vous devez SAP prend en charge ou souhaitez que le disque de toosingle toocopy source unique, vous pouvez [WAImportExport V1 outil télécharger] (http://go.Microsoft.com/fwlink/?) LinkID = 301900&amp;clcid = 0 x 409) et faire référence trop[WAImportExport V1 référence](storage-import-export-tool-how-to-v1.md) pour vous aider à l’utilisation de WAImportExport V1.

#### <a name="what-is-a-session-id"></a>Qu’est-ce qu’un ID de session ?

outil de Hello suppose que la session de copie hello (/ id) toobe de paramètre hello même si les données de salutation toospread avez l’intention hello sur plusieurs disques. Maintenance hello même nom de la session de copie hello permettra de données toocopy d’utilisateur à partir d’un ou plusieurs sites source en un ou plusieurs destination disques/répertoires. En conservant le même id de session active toopick d’outil hello copie hello de fichiers à l’endroit où il a été hello dernière fois.

Toutefois, même session de copie ne peut pas être des comptes de stockage utilisé tooimport données toodifferent.

Lorsque le nom de la session de copie est identique sur plusieurs exécutions de l’outil de hello, hello du fichier journal (/ logdir) et la clé de compte de stockage (/ sk) est également attendue toobe hello identiques.

L’ID de session peut contenir de 3 à 30 caractères : lettres, chiffres (de 0 à 9), trait de soulignement (\_), tiret (-) ou dièse (#).

Par exemple, session-1, session#1 ou session\_1.

#### <a name="what-is-a-journal-file"></a>Qu’est-ce qu’un fichier journal ?

Chaque fois que vous exécutez hello WAImportExport outil toocopy fichiers toohello disque dur, l’outil de hello crée une session de copie. état Hello de session de copie hello est écrit le fichier de feuille de toohello. Si une session de copie est interrompue (par exemple, en raison de tooa coupure de courant), il peut être reprise par réexécuter l’outil de hello et en spécifiant le fichier du journal sur la ligne de commande hello hello.

Pour chaque disque dur que vous préparez avec l’outil d’importation/exportation Azure de hello, outil de hello crée un seul fichier journal avec le nom «&lt;Id_lecteur&gt;.xml » où lecteur Id est le numéro de série hello associé lecteur toohello hello outil lit à partir de disque de Hello. Vous devez de votre travail d’importation hello lecteurs toocreate tous les fichiers de journal hello. fichier de journal Hello peut également être préparation du lecteur tooresume utilisé si l’outil de hello est interrompue.

#### <a name="what-is-a-log-directory"></a>Qu’est-ce qu’un répertoire de journaux ?

répertoire du journal Hello spécifie qu'un toobe active utilisée toostore les journaux détaillés, ainsi que les fichiers manifestes temporaires. Si non spécifié, répertoire actuel de hello sera utilisé comme répertoire de journal hello. les journaux de Hello sont des journaux détaillés.

### <a name="prerequisites"></a>Composants requis

#### <a name="what-are-hello-specifications-of-my-disk"></a>Quelles sont les spécifications hello de mon disque ?

Ordinateur de copie toohello connecté lecteurs à un ou plusieurs vide SATA II de 2,5 pouces ou 3,5 pouces ou III ou de SSD dur.

#### <a name="how-can-i-enable-bitlocker-on-my-machine"></a>Comment puis-je activer BitLocker sur mon ordinateur ?

Méthode simple toocheck est en cliquant sur le lecteur système. Elle vous montrera options pour Bitlocker si la fonctionnalité de hello est activée. Elles ne s’affichent pas si la fonctionnalité est désactivée.

![Consultez BitLocker.](./media/storage-import-export-tool-preparing-hard-drives-import/BitLocker.png)

Voici un article sur [comment tooenable BitLocker](https://technet.microsoft.com/library/cc766295.aspx)

Il est possible que votre ordinateur ne soit pas équipé d’une puce TPM. Si vous n’obtenez pas une sortie à l’aide de tpm.msc, examinez hello la question fréquemment posée suivante.

#### <a name="how-toodisable-trusted-platform-module-tpm-in-bitlocker"></a>Comment toodisable confiance Module de plateforme sécurisée (TPM) BitLocker ?
> [!NOTE]
> Uniquement si leurs serveurs ne contient aucun module de plateforme sécurisée, vous avez besoin de stratégie de module de plateforme sécurisée toodisable. Il n’est pas nécessaire toodisable TPM s’il existe un module de plateforme sécurisée approuvée dans le serveur de l’utilisateur. 
> 

Dans l’ordre toodisable TPM dans BitLocker, parcourez hello comme suit :<br/>
1. Démarrez l’**Éditeur de stratégie de groupe locale** en tapant gpedit.msc dans une invite de commande. Si **éditeur de stratégie de groupe** apparaît toobe indisponible, pour tout d’abord l’activation de BitLocker. Consultez la question précédente.
2. Ouvrez **Stratégie ordinateur local &gt; Configuration ordinateur &gt; Modèles d’administration &gt; Composants Windows&gt; Chiffrement de lecteur BitLocker &gt; Lecteurs du système d’exploitation**.
3. Modifiez la stratégie **Exiger une authentification supplémentaire au démarrage**.
4. Définir la stratégie de hello trop**activé** et assurez-vous que **Autoriser BitLocker sans un module de plateforme sécurisée compatible** est activée.

####  <a name="how-toocheck-if-net-4-or-higher-version-is-installed-on-my-machine"></a>Comment toocheck si .NET 4 ou version ultérieure est installée sur mon ordinateur ?

Toutes les versions de Microsoft .NET Framework sont installées dans le répertoire suivant : %windir%\Microsoft.NET\Framework\

Accédez toohello ci-dessus mentionnée partie sur votre ordinateur cible où hello outil a besoin toorun. Recherchez le répertoire dont le nom commence par « v4 ». L’absence de ce répertoire signifie que .NET 4 n’est pas installé sur votre ordinateur. Vous pouvez télécharger .Net v4 sur votre ordinateur à partir de la page [Microsoft .NET Framework 4 (programme d'installation Web)](https://www.microsoft.com/download/details.aspx?id=17851).

### <a name="limits"></a>limites

#### <a name="how-many-drives-can-i-preparesend-at-hello-same-time"></a>Le nombre de lecteurs puis-je je préparer / d’envoi à hello même temps ?

Il existe aucune limite du nombre de hello de disques qui hello outil ne peut préparer. Toutefois, outil de hello attend les lettres de lecteur en tant qu’entrées. Qui il limite la préparation du disque simultanées too25. Un travail peut gérer jusqu’à 10 disques à la fois. Si vous préparez des disques de plus de 10 ciblage hello même compte de stockage, les disques hello peuvent être distribués sur plusieurs travaux.

#### <a name="can-i-target-more-than-one-storage-account"></a>Puis-je cibler plusieurs comptes de stockage ?

Lors d’une session de copie, un seul compte de stockage peut être utilisé par travail.

### <a name="capabilities"></a>Fonctionnalités

#### <a name="does-waimportexportexe-encrypt-my-data"></a>L’outil WAImportExport.exe chiffre-t-il mes données ?

Oui. Le chiffrement BitLocker est activé et obligatoire pour ce processus.

#### <a name="what-will-be-hello-hierarchy-of-my-data-when-it-appears-in-hello-storage-account"></a>Quel sera hiérarchie hello mes données lorsqu’il apparaît dans le compte de stockage hello ?

Bien que les données sont réparties sur les disques, hello données téléchargées sont convergée compte de stockage toohello sauvegarder la structure de répertoires toohello spécifié dans un fichier CSV hello dataset.

#### <a name="how-many-of-hello-input-disks-will-have-active-io-in-parallel-when-copy-is-in-progress"></a>Combien de hello entrées disques ont les e/s active en parallèle, lors de la copie est en cours ?

outil de Hello distribue les données sur les disques d’entrée hello en fonction de taille hello des fichiers d’entrée de hello. Ceci dit, nombre de hello de disques actifs en parallèle delends complètement de nature hello des données d’entrée de hello. Selon la taille de hello des fichiers individuels dans le jeu de données d’entrée hello, un ou plusieurs disques peuvent afficher des e/s active en parallèle. Pour plus d’informations, consultez la question suivante.

#### <a name="how-does-hello-tool-distribute-hello-files-across-hello-disks"></a>Comment les outil hello distribuer les fichiers hello sur hello de disques ?

L’outil WAImportExport lit et écrit les fichiers par lots, un lot contenant au maximum 100 000 fichiers. Cela signifie que 100 000 fichiers peuvent être écrits en parallèle. Plusieurs disques sont écrits toosimultaneously si ces 100000 fichiers sont distribués toomulti lecteurs. Toutefois si hello outil écrit toomultiple disques simultanément ou un seul disque dépend de la taille cumulée de hello du lot de hello. Par exemple, dans le cas des fichiers plus petits, si tous les fichiers 10,0000 sont en mesure de toofit dans un seul lecteur, outil écrira tooonly un disque au cours du traitement de hello de ce lot.

### <a name="waimportexport-output"></a>Sortie de l’outil WAImportExport

#### <a name="there-are-two-journal-files-which-one-should-i-upload-tooazure-portal"></a>Il existe deux fichiers de journal, l’application doit charger tooAzure portail ?

**.XML** -pour chaque disque dur que vous avez préparé à l’outil WAImportExport hello, outil de hello crée un seul fichier journal nommé `<DriveID>.xml` où Id_lecteur est le numéro de série hello associé lecteur toohello hello outil lit à partir du disque de hello. Vous devez de votre travail d’importation lecteurs toocreate hello Bonjour Azure portal tous les fichiers de journal hello. Ce fichier journal peut également être préparation du lecteur tooresume utilisé si l’outil de hello est interrompue.

**.JRN** -fichier de journal hello avec le suffixe `.jrn` contient l’état de hello pour toutes les sessions de copie pour un disque dur. Il contient également des hello informations nécessaires toocreate hello importer le travail. Vous devez toujours spécifier un fichier journal lors de l’outil de WAImportExport hello en cours d’exécution, ainsi que d’une session de copie de code.

## <a name="next-steps"></a>Étapes suivantes

* [Configuration des hello, outil d’importation/exportation Azure](storage-import-export-tool-setup.md)
* [Définition des propriétés et métadonnées pendant hello processus d’importation](storage-import-export-tool-setting-properties-metadata-import.md)
* [Exemple workflow tooprepare les disques durs pour un travail d’importation](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
* [Référence rapide pour les commandes fréquemment utilisées](storage-import-export-tool-quick-reference.md) 
* [Consultation de l’état du travail avec les fichiers journaux de copie](storage-import-export-tool-reviewing-job-status-v1.md)
* [Réparation d’un travail d’importation](storage-import-export-tool-repairing-an-import-job-v1.md)
* [Réparation d’un travail d’exportation](storage-import-export-tool-repairing-an-export-job-v1.md)
* [Résolution des problèmes de hello outil d’importation/exportation Azure](storage-import-export-tool-troubleshooting-v1.md)
