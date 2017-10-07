---
title: format de fichier journal aaaAzure Import/Export | Documents Microsoft
description: "En savoir plus sur format hello de fichiers de journaux hello créé lors de l’exécution des étapes d’un travail de service d’importation/exportation."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 15a652455aa947922af0aa39ccefe68811a3db19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-log-file-format"></a>Format de fichier journal du service Azure Import/Export
Lorsque hello service Microsoft Azure Import/Export exécute une action sur un lecteur dans le cadre d’un travail d’importation ou d’exportation, les journaux sont écrits tooblock BLOB hello compte de stockage associé à ce travail.  
  
Il existe deux journaux pouvant être écrits par hello service d’importation/exportation :  
  
-   journal des erreurs Hello est toujours générée dans le cas de hello d’erreur.  
  
-   Hello journal détaillé n’est pas activé par défaut, mais peut être activée en définissant les hello `EnableVerboseLog` propriété sur un [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) ou [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) opération.  
  
## <a name="log-file-location"></a>Emplacement du fichier journal  
Hello dans les journaux tooblock BLOB dans le conteneur de hello ou un répertoire virtuel spécifié par hello `ImportExportStatesPath` paramètre que vous pouvez définir sur une `Put Job` opération. Hello emplacement toowhich hello dans les journaux dépend comment l’authentification est spécifiée pour la tâche hello, avec la valeur hello spécifiée pour `ImportExportStatesPath`. L’authentification pour le travail de hello peut être spécifiée via une clé de compte de stockage ou un conteneur de SAP (signature d’accès partagé).  
  
nom de Hello du conteneur de hello ou un répertoire virtuel peut être le nom par défaut hello `waimportexport`, ou un autre conteneur ou nom de répertoire virtuel que vous spécifiez.  
  
tableau Hello ci-dessous montre les options possibles hello :  
  
|Méthode d'authentification|Valeur de l’élément `ImportExportStatesPath`|Emplacement des objets blob de journal|  
|---------------------------|----------------------------------------------|---------------------------|  
|Clé du compte de stockage|Valeur par défaut|Un conteneur nommé `waimportexport`, qui est le conteneur par défaut de hello. Par exemple :<br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|Clé du compte de stockage|Valeur spécifiée par l’utilisateur|Un conteneur nommé par l’utilisateur de hello. Par exemple :<br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|SAP de conteneur|Valeur par défaut|Un répertoire virtuel nommé `waimportexport`, qui est le nom par défaut de hello, sous le conteneur hello spécifié dans hello SAS.<br /><br /> Par exemple, si hello SAS spécifié pour le travail de hello est `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, puis de l’emplacement du journal hello serait`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`|  
|SAP de conteneur|Valeur spécifiée par l’utilisateur|Un répertoire virtuel nommé par l’utilisateur hello, sous le conteneur hello spécifié dans hello SAS.<br /><br /> Par exemple, si hello SAS spécifié pour le travail de hello est `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, et hello spécifié le répertoire virtuel est appelé `mylogblobs`, puis de l’emplacement du journal hello serait `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.|  
  
Vous pouvez récupérer des URL hello pour erreur de hello et les journaux détaillés en appelant hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) opération. Hello journaux sont disponibles une fois le traitement du lecteur de hello est terminé.  
  
## <a name="log-file-format"></a>Format de fichier journal  
Hello format pour les journaux est hello même : un objet blob contenant des descriptions XML des événements hello qui s’est produite lors de la copie des objets BLOB entre le disque dur de hello et hello du compte client.  
  
la journalisation documentée Hello contient des informations complètes sur l’état de hello d’opération de copie hello pour chaque objet blob (pour un travail d’importation) ou un fichier (pour un travail d’exportation), tandis que le journal des erreurs hello contient uniquement les informations de hello pour les objets BLOB ou des fichiers qui ont rencontré des erreurs pendant hello importer ou exporter des travaux.  
  
format de journal détaillé Hello est indiqué ci-dessous. journal des erreurs Hello a hello même structure, mais filtre les opérations réussies.  

```xml
<DriveLog Version="2014-11-01">  
  <DriveId>drive-id</DriveId>  
  [<Blob Status="blob-status">  
   <BlobPath>blob-path</BlobPath>  
   <FilePath>file-path</FilePath>  
   [<Snapshot>snapshot</Snapshot>]  
   <Length>length</Length>  
   [<LastModified>last-modified</LastModified>]  
   [<ImportDisposition Status="import-disposition-status">import-disposition</ImportDisposition>]  
   [page-range-list-or-block-list]  
   [metadata-status]  
   [properties-status]  
  </Blob>]  
  [<Blob>  
    . . .  
  </Blob>]  
  <Status>drive-status</Status>  
</DriveLog>  
  
page-range-list-or-block-list ::= 
  page-range-list | block-list  
  
page-range-list ::=   
<PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
</PageRangeList>  
  
block-list ::=  
<BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       [Hash="md5-hash"] Status="block-status"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       [Hash="md5-hash"] Status="block-status"/>]  
</BlockList>  
  
metadata-status ::=  
<Metadata Status="metadata-status">  
   [<GlobalPath Hash="md5-hash">global-metadata-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">metadata-file-path</Path>]  
</Metadata>  
  
properties-status ::=  
<Properties Status="properties-status">  
   [<GlobalPath Hash="md5-hash">global-properties-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">properties-file-path</Path>]  
</Properties>  
```

Hello tableau suivant décrit les éléments hello du fichier journal de hello.  
  
|Élément XML|Type|Description|  
|-----------------|----------|-----------------|  
|`DriveLog`|Élément XML|Représente un journal de lecteur.|  
|`Version`|Attribut, Chaîne|version de Hello du format de journal hello.|  
|`DriveId`|String|Bonjour numéro de série du matériel du lecteur.|  
|`Status`|String|État de traitement du lecteur hello. Consultez hello `Drive Status Codes` tableau ci-dessous pour plus d’informations.|  
|`Blob`|Élément XML imbriqué|Représente un objet blob.|  
|`Blob/BlobPath`|String|Hello URI d’objet blob de hello.|  
|`Blob/FilePath`|String|fichier de toohello Hello chemin d’accès relatif sur le lecteur de hello.|  
|`Blob/Snapshot`|DateTime|version d’instantané Hello d’objet blob hello pour un travail d’exportation uniquement.|  
|`Blob/Length`|Entier |longueur totale de Hello du blob hello en octets.|  
|`Blob/LastModified`|DateTime|Hello date/heure dernière modification de cet objet blob hello pour un travail d’exportation uniquement.|  
|`Blob/ImportDisposition`|String|disposition d’objet blob hello pour un travail d’importation d’importation Hello.|  
|`Blob/ImportDisposition/@Status`|Attribut, Chaîne|état Hello Hello disposition d’importation.|  
|`PageRangeList`|Élément XML imbriqué|Représente une liste de plages de pages pour un objet blob de pages.|  
|`PageRange`|Élément XML|Représente une plage de pages.|  
|`PageRange/@Offset`|Attribut, Entier|Décalage de début de plage de pages hello dans l’objet blob de hello.|  
|`PageRange/@Length`|Attribut, Entier|Longueur en octets de la plage de pages hello.|  
|`PageRange/@Hash`|Attribut, Chaîne|Hachage de MD5 encodé en Base16 hello de plage de pages.|  
|`PageRange/@Status`|Attribut, Chaîne|État de traitement de plage de pages hello.|  
|`BlockList`|Élément XML imbriqué|Représente une liste de blocs pour un objet blob de blocs.|  
|`Block`|Élément XML|Représente un bloc.|  
|`Block/@Offset`|Attribut, Entier|Décalage de départ du bloc hello dans l’objet blob de hello.|  
|`Block/@Length`|Attribut, Entier|Longueur en octets du bloc de hello.|  
|`Block/@Id`|Attribut, Chaîne|ID de bloc de Hello.|  
|`Block/@Hash`|Attribut, Chaîne|Hachage de MD5 encodé en Base16 du bloc de hello.|  
|`Block/@Status`|Attribut, Chaîne|État de traitement hello bloc.|  
|`Metadata`|Élément XML imbriqué|Représente les métadonnées de l’objet blob de hello.|  
|`Metadata/@Status`|Attribut, Chaîne|État de traitement des métadonnées d’objet blob hello.|  
|`Metadata/GlobalPath`|String|Fichier de métadonnées global toohello chemin d’accès relatif.|  
|`Metadata/GlobalPath/@Hash`|Attribut, Chaîne|Encodé en Base16 hachage MD5 du fichier de métadonnées globales hello.|  
|`Metadata/Path`|String|Fichier de métadonnées de toohello de chemin d’accès relatif.|  
|`Metadata/Path/@Hash`|Attribut, Chaîne|Hachage de MD5 encodé en Base16 du fichier de métadonnées hello.|  
|`Properties`|Élément XML imbriqué|Représente les propriétés d’objet blob hello.|  
|`Properties/@Status`|Attribut, Chaîne|État de traitement des propriétés d’objet blob hello, par exemple, fichier introuvable, s’est terminée.|  
|`Properties/GlobalPath`|String|Fichier de propriétés globales de toohello de chemin d’accès relatif.|  
|`Properties/GlobalPath/@Hash`|Attribut, Chaîne|Hachage de MD5 encodé en Base16 du fichier de propriétés globales hello.|  
|`Properties/Path`|String|Fichier de propriétés de toohello de chemin d’accès relatif.|  
|`Properties/Path/@Hash`|Attribut, Chaîne|Hachage de MD5 encodé en Base16 du fichier de propriétés hello.|  
|`Blob/Status`|String|État de traitement des objets blob de hello.|  
  
# <a name="drive-status-codes"></a>Codes d’état du lecteur  
Hello tableau suivant répertorie les codes d’état hello pour le traitement d’un lecteur.  
  
|Code d’état|Description|  
|-----------------|-----------------|  
|`Completed`|lecteur de Hello a terminé le traitement sans erreurs.|  
|`CompletedWithWarnings`|lecteur de Hello a terminé le traitement des avertissements dans un ou plusieurs des objets BLOB par dispositions d’importation hello spécifiées pour les objets BLOB de hello.|  
|`CompletedWithErrors`|lecteur de Hello a terminé avec des erreurs dans un ou plusieurs objets BLOB ou segments.|  
|`DiskNotFound`|Aucun disque ne se trouve sur le lecteur de hello.|  
|`VolumeNotNtfs`|Hello premier volume de données sur disque de hello n’est pas au format NTFS.|  
|`DiskOperationFailed`|Une erreur inconnue s’est produite lors de l’exécution d’opérations sur le lecteur de hello.|  
|`BitLockerVolumeNotFound`|Aucun volume BitLocker chiffrable n’a été trouvé.|  
|`BitLockerNotActivated`|BitLocker n’est pas activé sur le volume de hello.|  
|`BitLockerProtectorNotFound`|protecteur de clé de mot de passe numérique Hello n’existe pas sur le volume de hello.|  
|`BitLockerKeyInvalid`|mot de passe numérique Hello fourni ne peut pas déverrouiller hello.|  
|`BitLockerUnlockVolumeFailed`|Erreur inconnue s’est produite lors de la tentative de volume de hello toounlock.|  
|`BitLockerFailed`|Une erreur inconnue s’est produite lors de l’exécution d’opérations BitLocker.|  
|`ManifestNameInvalid`|nom du fichier manifeste Hello n’est pas valide.|  
|`ManifestNameTooLong`|nom du fichier manifeste Hello est trop long.|  
|`ManifestNotFound`|fichier de manifeste Hello est introuvable.|  
|`ManifestAccessDenied`|Fichier de manifeste toohello accès est refusé.|  
|`ManifestCorrupted`|Hello fichier manifeste est endommagé (hello contenu ne correspond pas à son hachage).|  
|`ManifestFormatInvalid`|contenu du manifeste Hello ne respecte pas le format requis de toohello.|  
|`ManifestDriveIdMismatch`|lecteur Hello ID dans le fichier de manifeste hello ne correspond pas hello une lecture à partir du lecteur de hello.|  
|`ReadManifestFailed`|Un erreur d’e/s disque s’est produite lors de la lecture du manifeste de hello.|  
|`BlobListFormatInvalid`|Hello exportation blob liste d’objets blob ne respecte pas le format requis de toohello.|  
|`BlobRequestForbidden`|Accéder aux objets BLOB de toohello dans le compte de stockage hello est interdite. Cela est peut-être en raison de la clé de compte de stockage tooinvalid ou SAP de conteneur.|  
|`InternalError`|Et une erreur interne s’est produite lors du traitement du lecteur de hello.|  
  
## <a name="blob-status-codes"></a>Codes d’état de l’objet blob  
Hello tableau suivant répertorie les codes d’état hello pour le traitement d’un objet blob.  
  
|Code d’état|Description|  
|-----------------|-----------------|  
|`Completed`|objet blob de Hello a terminé le traitement sans erreurs.|  
|`CompletedWithErrors`|objet blob de Hello a terminé le traitement avec des erreurs dans une ou plusieurs plages de pages ou blocs, métadonnées ou propriétés.|  
|`FileNameInvalid`|nom de fichier Hello n’est pas valide.|  
|`FileNameTooLong`|nom de fichier Hello est trop long.|  
|`FileNotFound`|fichier de Hello est introuvable.|  
|`FileAccessDenied`|Fichier de toohello d’accès est refusé.|  
|`BlobRequestFailed`|demande de service Blob Hello tooaccess hello blob a échoué.|  
|`BlobRequestForbidden`|demande de service Blob Hello tooaccess hello blob est interdite. Cela est peut-être en raison de la clé de compte de stockage tooinvalid ou SAP de conteneur.|  
|`RenameFailed`|Échec de l’objet blob de hello toorename (pour un travail d’importation) ou un fichier hello (pour un travail d’exportation).|  
|`BlobUnexpectedChange`|Une modification inattendue s’est produite avec l’objet blob de hello (pour un travail d’exportation).|  
|`LeasePresent`|Il existe un bail présent sur l’objet blob de hello.|  
|`IOFailed`|Un disque ou une erreur d’e/s de réseau s’est produite lors du traitement d’objets blob de hello.|  
|`Failed`|Une erreur inconnue s’est produite lors du traitement d’objets blob de hello.|  
  
## <a name="import-disposition-status-codes"></a>Codes d’état de disposition d’importation  
Hello tableau suivant répertorie les codes d’état hello pour résoudre une disposition d’importation.  
  
|Code d’état|Description|  
|-----------------|-----------------|  
|`Created`|objet blob de Hello a été créé.|  
|`Renamed`|objet blob de Hello a été renommé par disposition d’importation de changement de nom. Hello `Blob/BlobPath` élément contient hello URI pour l’objet blob de hello renommé.|  
|`Skipped`|objet blob de Hello a été ignoré par `no-overwrite` disposition d’importation.|  
|`Overwritten`|objet blob de Hello a remplacé un objet blob existant par `overwrite` disposition d’importation.|  
|`Cancelled`|Une erreur précédente a arrêté le traitement de disposition d’importation hello.|  
  
## <a name="page-rangeblock-status-codes"></a>Codes d’état de plage de pages/de bloc  
Hello tableau suivant répertorie les codes d’état hello pour le traitement d’une plage de pages ou un bloc.  
  
|Code d’état|Description|  
|-----------------|-----------------|  
|`Completed`|plage de pages Hello ou un bloc a terminé le traitement sans erreurs.|  
|`Committed`|Hello bloc a été validé, mais pas dans hello liste complète de blocs, car les autres blocs ont a échoué, ou placez la liste complète de blocs a échoué.|  
|`Uncommitted`|bloc de Hello est téléchargé mais non validée.|  
|`Corrupted`|plage de pages Hello ou un bloc est endommagé (hello contenu ne correspond pas à son hachage).|  
|`FileUnexpectedEnd`|Une fin de fichier inattendue a été rencontrée.|  
|`BlobUnexpectedEnd`|Une fin d’objet blob inattendue a été rencontrée.|  
|`BlobRequestFailed`|Hello tooaccess hello plage de pages de la demande du service Blob ou bloc a échoué.|  
|`IOFailed`|Un disque ou une erreur d’e/s de réseau s’est produite lors du traitement de la plage de pages hello ou un bloc.|  
|`Failed`|Une erreur inconnue s’est produite lors du traitement de la plage de pages hello ou un bloc.|  
|`Cancelled`|Une erreur précédente a arrêté le traitement de la plage de pages hello ou un bloc.|  
  
## <a name="metadata-status-codes"></a>Codes d’état des métadonnées  
Hello tableau suivant répertorie les codes d’état hello pour le traitement des métadonnées d’objet blob.  
  
|Code d’état|Description|  
|-----------------|-----------------|  
|`Completed`|les métadonnées Hello a terminé le traitement sans erreurs.|  
|`FileNameInvalid`|nom de fichier de métadonnées Hello n’est pas valide.|  
|`FileNameTooLong`|nom de fichier de métadonnées Hello est trop long.|  
|`FileNotFound`|fichier de métadonnées Hello est introuvable.|  
|`FileAccessDenied`|Fichier de métadonnées toohello accès est refusé.|  
|`Corrupted`|fichier de métadonnées Hello est endommagé (hello contenu ne correspond pas à son hachage).|  
|`XmlReadFailed`|contenu de métadonnées Hello ne respecte pas le format requis de toohello.|  
|`XmlWriteFailed`|Lors de l’écriture hello que XML a échoué.|  
|`BlobRequestFailed`|demande de service Blob Hello tooaccess hello métadonnées a échoué.|  
|`IOFailed`|Une erreur d’e/s disque ou réseau s’est produite lors du traitement des métadonnées de hello.|  
|`Failed`|Une erreur inconnue s’est produite lors du traitement des métadonnées de hello.|  
|`Cancelled`|Une erreur précédente a arrêté le traitement des métadonnées de hello.|  
  
## <a name="properties-status-codes"></a>Codes d’état des propriétés  
Hello tableau suivant répertorie les codes d’état hello pour le traitement des propriétés d’objet blob.  
  
|Code d’état|Description|  
|-----------------|-----------------|  
|`Completed`|les propriétés de Hello ont terminé le traitement sans erreurs.|  
|`FileNameInvalid`|nom de fichier de propriétés Hello n’est pas valide.|  
|`FileNameTooLong`|nom de fichier de propriétés Hello est trop long.|  
|`FileNotFound`|fichier de propriétés Hello est introuvable.|  
|`FileAccessDenied`|Fichier de propriétés toohello accès est refusé.|  
|`Corrupted`|fichier de propriétés Hello est endommagé (hello contenu ne correspond pas à son hachage).|  
|`XmlReadFailed`|contenu des propriétés Hello ne respecte pas le format requis de toohello.|  
|`XmlWriteFailed`|L’écriture de propriétés hello que XML a échoué.|  
|`BlobRequestFailed`|demande de service Blob Hello tooaccess hello propriétés a échoué.|  
|`IOFailed`|Une erreur d’e/s disque ou réseau s’est produite lors du traitement des propriétés de hello.|  
|`Failed`|Une erreur inconnue s’est produite lors du traitement des propriétés de hello.|  
|`Cancelled`|Une erreur précédente a arrêté le traitement des propriétés de hello.|  
  
## <a name="sample-logs"></a>Exemples de journaux  
Hello Voici un exemple de journal détaillé.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV123456</DriveId>  
    <Blob Status="Completed">  
       <BlobPath>pictures/bob/wild/desert.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\wild\desert.jpg</FilePath>  
       <Length>98304</Length>  
       <ImportDisposition Status="Created">overwrite</ImportDisposition>  
       <BlockList>  
          <Block Offset="0" Length="65536" Id="AAAAAA==" Hash=" 9C8AE14A55241F98533C4D80D85CDC68" Status="Completed"/>  
          <Block Offset="65536" Length="32768" Id="AQAAAA==" Hash=" DF54C531C9B3CA2570FDDDB3BCD0E27D" Status="Completed"/>  
       </BlockList>  
       <Metadata Status="Completed">  
          <GlobalPath Hash=" E34F54B7086BCF4EC1601D056F4C7E37">\Users\bob\Pictures\wild\metadata.xml</GlobalPath>  
       </Metadata>  
    </Blob>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="0" Length="65536" Hash="19701B8877418393CB3CB567F53EE225" Status="Completed"/>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
          <PageRange Offset="131072" Length="4096" Hash="9BA552E1C3EEAFFC91B42B979900A996" Status="Completed"/>  
       </PageRangeList>  
       <Properties Status="Completed">  
          <Path Hash="38D7AE80653F47F63C0222FEE90EC4E7">\Users\bob\Pictures\animals\koala.jpg.properties</Path>  
       </Properties>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
journal des erreurs Hello correspondant est indiqué ci-dessous.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV6965824</DriveId>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
       </PageRangeList>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

 journal des erreurs Hello pour un travail d’importation contient une erreur sur un fichier introuvable sur le lecteur d’importation hello. Notez qu’état hello des composants suivants est `Cancelled`.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="FileNotFound">  
    <BlobPath>pictures/animals/koala.jpg</BlobPath>  
    <FilePath>\animals\koala.jpg</FilePath>  
    <Length>30310</Length>  
    <ImportDisposition Status="Cancelled">rename</ImportDisposition>  
    <BlockList>  
      <Block Offset="0" Length="6062" Id="MD5/cAzn4h7VVSWXf696qp5Uaw==" Hash="700CE7E21ED55525977FAF7AAA9E546B" Status="Cancelled" />  
      <Block Offset="6062" Length="6062" Id="MD5/PEnGwYOI8LPLNYdfKr7kAg==" Hash="3C49C6C18388F0B3CB35875F2ABEE402" Status="Cancelled" />  
      <Block Offset="12124" Length="6062" Id="MD5/FG4WxqfZKuUWZ2nGTU2qVA==" Hash="146E16C6A7D92AE5166769C64D4DAA54" Status="Cancelled" />  
      <Block Offset="18186" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
      <Block Offset="24248" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

Hello journal des erreurs pour un travail d’exportation indique que le contenu blob hello a été correctement écrit toohello lecteur, mais qu’une erreur s’est produite lors de l’exportation des propriétés de l’objet blob de hello.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C3U</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
    <FilePath>\pictures\wild\canyon.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList />  
    <Properties Status="Failed" />  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
## <a name="next-steps"></a>Étapes suivantes
 
* [API REST d’importation/exportation de stockage](/rest/api/storageimportexport/)
