---
title: "aaaSetting des hello outil d’importation/exportation Azure | Documents Microsoft"
description: "Découvrez comment tooset des hello lecteur préparation et l’outil de réparation de service d’importation/exportation Azure hello."
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
ms.openlocfilehash: 3d8897f2783112e07123669f1ba5b22576770e60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-hello-azure-importexport-tool"></a>Configuration de hello outil d’importation/exportation Azure

Hello, outil d’importation/exportation de Microsoft Azure est hello lecteur outil de préparation et réparation que vous pouvez utiliser avec hello service Microsoft Azure Import/Export. Vous pouvez utiliser l’outil de hello pour hello suivant des fonctions :

* Avant de créer un travail d’importation, vous pouvez utiliser cet outil toocopy données toohello disques durs que vous allez centre de données Azure tooship tooan.
* Lorsqu’une tâche d’importation est terminé, vous pouvez utiliser cette toorepair outil tous les objets BLOB qui ont été endommagés, étaient manquants ou qui est en conflit avec d’autres objets BLOB.
* Après avoir reçu les lecteurs hello d’un travail d’exportation terminé, vous pouvez utiliser cette toorepair outil tous les fichiers qui ont été endommagés ou manquants sur des lecteurs hello.

## <a name="prerequisites"></a>Composants requis

Si vous êtes **préparation des lecteurs** pour un travail d’importation, hello suivant les conditions préalables doit être remplie :

* Vous devez avoir un abonnement Azure actif.
* Votre abonnement doit inclure un compte de stockage avec assez d’espace disponible toostore hello de fichiers que vous vous apprêtez tooimport.
* Vous devez au moins une des clés de l’accès du compte de stockage hello.
* Vous avez besoin d’un ordinateur (hello « ordinateur copie ») avec Windows 7, Windows Server 2008 R2 ou un système d’exploitation Windows plus récent installé.
* Hello .NET Framework 4 doit être installé sur l’ordinateur de copie hello.
* BitLocker doit être activé sur l’ordinateur de copie hello.
* Vous devez installer un ou plusieurs vide 3,5 disques durs SATA connecté ordinateur de copie toohello.
* fichiers Hello vous envisagez de tooimport doivent être accessibles à partir de l’ordinateur de copie hello, qu’ils soient sur un partage réseau ou un disque dur local.

Si vous essayez de trop**réparer une importation** qui a partiellement échoué, vous devez :

* fichiers journaux de copie Hello
* clé de compte de stockage Hello

Si vous essayez de trop**réparer une exportation** qui a partiellement échoué, vous devez :

* fichiers journaux de copie Hello
* fichiers de manifeste Hello (facultatifs)
* clé de compte de stockage Hello

## <a name="installing-hello-azure-importexport-tool"></a>Lors de l’installation hello outil d’importation/exportation Azure

Tout d’abord, [télécharger hello outil d’importation/exportation Azure](https://www.microsoft.com/download/details.aspx?id=55280) et extrayez-le répertoire tooa sur votre ordinateur, par exemple `c:\WAImportExport`.

Hello, outil d’importation/exportation Azure se compose de hello fichiers suivants :

* dataset.csv
* driveset.csv
* hddid.dll
* Microsoft.Data.Services.Client.dll
* Microsoft.WindowsAzure.Storage.dll
* Microsoft.WindowsAzure.Storage.pdb
* Microsoft.WindowsAzure.Storage.xml
* WAImportExport.exe
* WAImportExport.exe.config
* WAImportExport.pdb
* WAImportExportCore.dll
* WAImportExportCore.pdb
* WAImportExportRepair.dll
* WAImportExportRepair.pdb

Ensuite, ouvrez une fenêtre d’invite de commandes dans **mode administrateur**, et la modification dans l’annuaire hello contenant hello extrait les fichiers.

commande hello, exécutez l’outil de hello aide toooutput (`WAImportExport.exe`) sans paramètres :

```
WAImportExport, a client tool for Windows Azure Import/Export Service. Microsoft (c) 2013


Copy directories and/or files with a new copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>]
        [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>]
        DataSet:<dataset.csv>

Add more drives:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AdditionalDriveSet:<driveset.csv>

Abort an interrupted copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AbortSession

Resume an interrupted copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /ResumeSession

List drives:
    WAImportExport.exe PrepImport /j:<JournalFile> /ListDrives

List copy sessions:
    WAImportExport.exe PrepImport /j:<JournalFile> /ListCopySessions

Repair a Drive:
    WAImportExport.exe RepairImport | RepairExport
        /r:<RepairFile> [/logdir:<LogDirectory>]
        [/d:<TargetDirectories>] [/bk:<BitLockerKey>]
        /sn:<StorageAccountName> /sk:<StorageAccountKey>
        [/CopyLogFile:<DriveCopyLogFile>] [/ManifestFile:<DriveManifestFile>]
        [/PathMapFile:<DrivePathMapFile>]

Preview an Export Job:
    WAImportExport.exe PreviewExport
        [/logdir:<LogDirectory>]
        /sn:<StorageAccountName> /sk:<StorageAccountKey>
        /ExportBlobListFile:<ExportBlobListFile> /DriveSize:<DriveSize>

Parameters:

    /j:<JournalFile>
        - Required. Path toohello journal file. A journal file tracks a set of drives and
          records hello progress in preparing these drives. hello journal file must always
          be specified.
    /logdir:<LogDirectory>
        - Optional. hello log directory. Verbose log files as well as some temporary
          files will be written toothis directory. If not specified, current directory
          will be used as hello log directory. hello log directory can be specified only
          once for hello same journal file.
    /id:<SessionId>
        - Optional. hello session Id is used tooidentify a copy session. It is used to
          ensure accurate recovery of an interrupted copy session.
    /ResumeSession
        - Optional. If hello last copy session was terminated abnormally, this parameter
          can be specified tooresume hello session.
    /AbortSession
        - Optional. If hello last copy session was terminated abnormally, this parameter
          can be specified tooabort hello session.
    /sn:<StorageAccountName>
        - Required. Only applicable for RepairImport and RepairExport. hello name of
          hello storage account.
    /sk:<StorageAccountKey>
        - Required. hello key of hello storage account.
    /InitialDriveSet:<driveset.csv>
        - Required. A .csv file that contains a list of drives tooprepare.
    /AdditionalDriveSet:<driveset.csv>
        - Required. A .csv file that contains a list of additional drives toobe added.
    /r:<RepairFile>
        - Required. Only applicable for RepairImport and RepairExport.
          Path toohello file for tracking repair progress. Each drive must have one
          and only one repair file.
    /d:<TargetDirectories>
        - Required. Only applicable for RepairImport and RepairExport.
          For RepairImport, one or more semicolon-separated directories toorepair;
          For RepairExport, one directory toorepair, e.g. root directory of hello drive.
    /CopyLogFile:<DriveCopyLogFile>
        - Required. Only applicable for RepairImport and RepairExport. Path toothe
          drive copy log file (verbose or error).
    /ManifestFile:<DriveManifestFile>
        - Required. Only applicable for RepairExport. Path toohello drive manifest file.
    /PathMapFile:<DrivePathMapFile>
        - Optional. Only applicable for RepairImport. Path toohello file containing
          mappings of file paths relative toohello drive root toolocations of actual files
          (tab-delimited). When first specified, it will be populated with file paths
          with empty targets, which means either they are not found in TargetDirectories,
          access denied, with invalid name, or they exist in multiple directories. The
          path map file can be manually edited tooinclude hello correct target paths and
          specified again for hello tool tooresolve hello file paths correctly.
    /ExportBlobListFile:<ExportBlobListFile>
        - Required. Path toohello XML file containing list of blob paths or blob path
          prefixes for hello blobs toobe exported. hello file format is hello same as the
          blob list blob format in hello Put Job operation of hello Import/Export Service
          REST API.
    /DriveSize:<DriveSize>
        - Required. Size of drives toobe used for export. For example, 500GB, 1.5TB.
          Note: 1 GB = 1,000,000,000 bytes
                1 TB = 1,000,000,000,000 bytes
    /DataSet:<dataset.csv>
        - Required. A .csv file that contains a list of directories and/or a list files
          toobe copied tootarget drives.

    /silentmode
        - Optional. If not specified, it will remind you hello requirement of drives and
          need your confirmation toocontinue.

Examples:

    Copy a data set tooa drive:
    WAImportExport.exe PrepImport
        /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GEL
        xmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /InitialDriveSet:driveset1.csv
        /DataSet:data.csv

    Copy another dataset toohello same drive following hello above command:
    WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#2 /DataSet:dataset2.csv

    Preview how many 1.5 TB drives are needed for an export job:
    WAImportExport.exe PreviewExport
        /sn:mytestaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7K
        ysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\temp\myexportbloblist.xml
        /DriveSize:1.5TB

    Repair an finished import job:
    WAImportExport.exe RepairImport
        /r:9WM35C2V.rep /d:X:\ /bk:442926-020713-108086-436744-137335-435358-242242-2795
        98 /sn:mytestaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94
        f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\temp\9WM35C2V_error.log
```

## <a name="next-steps"></a>Étapes suivantes

* [Préparation des disques durs pour un travail d’importation](../storage-import-export-tool-preparing-hard-drives-import.md)
* [Aperçu de l’utilisation des lecteurs pour un travail d’exportation](../storage-import-export-tool-previewing-drive-usage-export-v1.md)
* [Consultation de l’état du travail avec les fichiers journaux de copie](../storage-import-export-tool-reviewing-job-status-v1.md)
* [Réparation d’un travail d’importation](../storage-import-export-tool-repairing-an-import-job-v1.md)
* [Réparation d’un travail d’exportation](../storage-import-export-tool-repairing-an-export-job-v1.md)
* [Résolution des problèmes de hello outil d’importation/exportation Azure](storage-import-export-tool-troubleshooting-v1.md)
