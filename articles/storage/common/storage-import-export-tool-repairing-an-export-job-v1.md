---
title: "aaaRepairing un travail d’exportation Azure Import/Export - v1 | Documents Microsoft"
description: "Découvrez comment un travail d’exportation qui a été créé et exécuté à l’aide de toorepair hello Azure Import/Export service."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 728e2a42-04ce-4be8-9375-e9e2bc6827a5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: e54bc66495c8a3473b8ec51bb254bce8bdc9eab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-export-job"></a>Réparation d’un travail d’exportation
Lorsqu’un travail d’exportation est terminé, vous pouvez exécuter hello outil de Microsoft Azure Import/Export localement pour :  
  
1.  Le téléchargement de fichiers que le service d’importation/exportation Azure hello a tooexport impossible.  
  
2.  Valider que les fichiers sur le lecteur de hello hello ont été correctement exportés.  
  
Cette fonctionnalité, vous devez avoir toouse de stockage tooAzure de connectivité.  
  
commande Hello pour réparer un travail d’importation est **RepairExport**.

## <a name="repairexport-parameters"></a>Paramètres de RepairExport

Hello paramètres suivants peuvent être spécifiés avec **RepairExport**:  
  
|Paramètre|Description|  
|---------------|-----------------|  
|**/r:&lt;RepairFile\>**|Obligatoire. Chemin d’accès toohello fichier de réparation qui suit la progression de la réparation de hello hello et vous permet de tooresume une réparation interrompue. Chaque disque ne doit avoir qu’un fichier de réparation. Lorsque vous démarrez une réparation pour un lecteur donné, vous passez hello chemin d’accès tooa réparer un fichier qui n’existe pas. tooresume une réparation interrompue, vous devez passer dans le nom d’un fichier existant de la réparation de hello. lecteur cible correspondant toohello d’Hello réparation fichier doit toujours être spécifié.|  
|**/logdir:&lt;LogDirectory\>**|facultatif. répertoire de journal Hello. Les fichiers journaux détaillés seront écrit toothis active. Si aucun répertoire de journal est spécifié, répertoire actuel de hello sera utilisé comme répertoire de journal hello.|  
|**/d:&lt;TargetDirectory\>**|Obligatoire. Hello Active toovalidate et la réparation. Cela est généralement hello répertoire racine du lecteur d’exportation hello, mais peut également être un partage de fichiers réseau qui contient une copie des fichiers de hello exportée.|  
|**/bk:&lt;BitLockerKey\>**|facultatif. Vous devez spécifier la clé de BitLocker hello si vous souhaitez toounlock d’outil hello chiffré hello où les fichiers exportés sont stockés.|  
|**/sn:&lt;StorageAccountName\>**|Obligatoire. tâche d’exportation de nom Hello hello du compte de stockage pour hello.|  
|**/sk:&lt;StorageAccountKey\>**|**Obligatoire** si et seulement si une SAP de conteneur n’est pas spécifiée. tâche d’exportation de clé de compte Hello hello compte de stockage pour hello.|  
|**/csas:&lt;ContainerSas\>**|**Requis** si et seulement si la clé de compte de stockage hello n’est pas spécifiée. Hello SAP de conteneur pour accéder aux objets BLOB de hello associé au travail d’exportation hello.|  
|**/CopyLogFile:&lt;DriveCopyLogFile\>**|Obligatoire. Hello chemin d’accès toohello lecteur fichier journal de copie. fichier de Hello est généré par hello service Windows Azure Import/Export et peut être téléchargé à partir du stockage d’objets blob hello associé hello travail. fichier journal de copie Hello contient des informations sur les objets BLOB en échec ou les fichiers qui sont toobe réparé.|  
|**/ManifestFile:&lt;DriveManifestFile\>**|facultatif. fichier manifeste de lecteur exportation Hello chemin d’accès toohello. Ce fichier est généré par le service de Windows Azure Import/Export hello et stocké sur le lecteur d’exportation hello et, éventuellement dans un objet blob dans le compte de stockage hello associé hello travail.<br /><br /> Hello contenu des fichiers hello sur le lecteur d’exportation hello sera vérifié avec hello les hachages MD5 contenus dans ce fichier. Les fichiers qui sont déterminé toobe endommagé seront téléchargés et réécrits toohello cible répertoires.|  
  
## <a name="using-repairexport-mode-toocorrect-failed-exports"></a>Utilisation de RepairExport mode toocorrect les échecs d’exportation  
Vous pouvez utiliser les fichiers toodownload hello outil d’importation/exportation Azure qui a échoué tooexport. fichier journal de copie Hello contient une liste de fichiers qui ont échoué tooexport.  
  
Hello causes des échecs d’exportation hello suivant les possibilités suivantes :  
  
-   Lecteurs endommagés  
  
-   clé de compte de stockage Hello modifiée pendant le processus de transfert hello  
  
outil de hello toorun dans **RepairExport** mode, vous devez tout d’abord lecteur de hello tooconnect contenant l’ordinateur de tooyour hello fichiers exportés. Ensuite, exécutez hello outil d’importation/exportation Azure, spécifiant hello chemin toothat lecteur avec hello `/d` paramètre. Vous devez également le fichier journal de copie du lecteur toohello toospecify hello chemin d’accès que vous avez téléchargé. Hello exemple de ligne de commande suivante exécute hello outil toorepair tous les fichiers qui ont échoué tooexport :  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
Hello Voici un exemple d’un fichier journal de copie qui montre un bloc dans hello blob échoué tooexport :  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/desert.jpg</BlobPath>  
    <FilePath>\pictures\wild\desert.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList>  
      <Block Offset="65536" Length="65536" Id="AQAAAA==" Status="Failed" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
fichier journal de copie Hello indique qu’une défaillance s’est produite pendant que hello service Windows Azure Import/Export téléchargeait un du fichier de toohello de l’objet blob de hello blocs sur le lecteur d’exportation hello. Hello d’autres composants du fichier de hello téléchargé avec succès et longueur du fichier hello a été correctement définie. Dans ce cas, outil de hello sera ouvrir le fichier hello sur le lecteur de hello, téléchargez le bloc de hello hello compte de stockage et écrire toohello plage de fichiers à partir de décalage 65536 avec la longueur 65536.  
  
## <a name="using-repairexport-toovalidate-drive-contents"></a>À l’aide du contenu du lecteur RepairExport toovalidate  
Vous pouvez également utiliser Azure Import/Export avec hello **RepairExport** option toovalidate hello contenu sur le lecteur de hello est correct. fichier de manifeste Hello sur chaque lecteur d’exportation contient MD5s pour contenu hello du lecteur de hello.  
  
Hello service Azure Import/Export peut également enregistrer les fichiers manifeste hello compte de stockage tooa pendant le processus d’exportation hello. Hello emplacement des fichiers de manifeste hello est disponible via hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) opération lorsque hello est terminée. Consultez [service d’importation/exportation Format de fichier manifeste](storage-import-export-file-format-metadata-and-properties.md) pour plus d’informations sur le format de hello d’un fichier de manifeste de lecteur.  
  
Hello suivant montre comment toorun hello outil d’importation/exportation Azure avec hello **MANIFESTFILE** et **/CopyLogFile** paramètres :  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
Hello Voici un exemple d’un fichier manifeste :  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveManifest Version="2011-10-01">  
  <Drive>  
    <DriveId>9WM35C3U</DriveId>  
    <ClientCreator>Windows Azure Import/Export service</ClientCreator>  
    <BlobList>
      <Blob>  
        <BlobPath>pictures/city/redmond.jpg</BlobPath>  
        <FilePath>\pictures\city\redmond.jpg</FilePath>  
        <Length>15360</Length>  
        <PageRangeList>  
          <PageRange Offset="0" Length="3584" Hash="72FC55ED9AFDD40A0C8D5C4193208416" />  
          <PageRange Offset="3584" Length="3584" Hash="68B28A561B73D1DA769D4C24AA427DB8" />  
          <PageRange Offset="7168" Length="512" Hash="F521DF2F50C46BC5F9EA9FB787A23EED" />  
        </PageRangeList>  
        <PropertiesPath Hash="E72A22EA959566066AD89E3B49020C0A">\pictures\city\redmond.jpg.properties</PropertiesPath>  
      </Blob>  
      <Blob>  
        <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
        <FilePath>\pictures\wild\canyon.jpg</FilePath>  
        <Length>10884</Length>  
        <BlockList>  
          <Block Offset="0" Length="2721" Id="AAAAAA==" Hash="263DC9C4B99C2177769C5EBE04787037" />  
          <Block Offset="2721" Length="2721" Id="AQAAAA==" Hash="0C52BAE2CC20EFEC15CC1E3045517AA6" />  
          <Block Offset="5442" Length="2721" Id="AgAAAA==" Hash="73D1CB62CB426230C34C9F57B7148F10" />  
          <Block Offset="8163" Length="2721" Id="AwAAAA==" Hash="11210E665C5F8E7E4F136D053B243E6A" />  
        </BlockList>  
        <PropertiesPath Hash="81D7F81B2C29F10D6E123D386C3A4D5A">\pictures\wild\canyon.jpg.properties</PropertiesPath>  
      </Blob> 
    </BlobList>  
 </Drive>  
</DriveManifest>  
``` 
  
Après le processus de réparation en terminant hello, outil de hello parcourt chaque fichier référencé dans le fichier de manifeste hello et vérifier l’intégrité du fichier hello d’avec des hachages de hello MD5. Pour le manifeste hello ci-dessus, il parcourt hello suivant des composants.  

```  
G:\pictures\city\redmond.jpg, offset 0, length 3584  
  
G:\pictures\city\redmond.jpg, offset 3584, length 3584  
  
G:\pictures\city\redmond.jpg, offset 7168, length 3584  
  
G:\pictures\city\redmond.jpg.properties  
  
G:\pictures\wild\canyon.jpg, offset 0, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 2721, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 5442, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 8163, length 2721  
  
G:\pictures\wild\canyon.jpg.properties  
```

N’importe quel composant échecs hello sera téléchargé par hello outil et réécrit toohello même fichier sur le lecteur de hello.  
  
## <a name="next-steps"></a>Étapes suivantes
 
* [Configuration des hello, outil d’importation/exportation Azure](storage-import-export-tool-setup-v1.md)   
* [Préparation des disques durs pour un travail d’importation](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Consultation de l’état du travail avec les fichiers journaux de copie](storage-import-export-tool-reviewing-job-status-v1.md)   
* [Réparation d’un travail d’importation](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [Résolution des problèmes de hello outil d’importation/exportation Azure](storage-import-export-tool-troubleshooting-v1.md)
