---
title: "format de fichier manifeste d’importation/exportation aaaAzure | Documents Microsoft"
description: "En savoir plus sur format hello du fichier manifeste de lecteur hello qui décrit le mappage de hello entre les objets BLOB dans le stockage Blob Azure et les fichiers sur un lecteur dans un travail d’importation ou d’exportation dans le service d’importation/exportation hello."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f3119e1c-2c25-48ad-8752-a6ed4adadbb0
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: d7e5e1990482916f7ff5f891c97343b52e82b2f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-manifest-file-format"></a>Format de fichier de manifeste du service Azure Import/Export
fichier manifeste de lecteur Hello décrit le mappage hello entre les objets BLOB dans le stockage d’objets Blob Azure et les fichiers sur le lecteur comportant un travail d’importation ou d’exportation. Pour une opération d’importation, le fichier de manifeste de hello est créé dans le cadre du processus de préparation de lecteur hello et est stocké sur le lecteur de hello avant que le lecteur de hello est envoyé de centre de données Azure toohello. Pendant une opération d’exportation, manifeste de hello est créé et stocké sur le lecteur de hello en hello service Azure Import/Export.  
  
Pour les deux importation et de travaux d’exportation, fichier de manifeste de lecteur hello est stocké sur hello importer ou exporter des disque ; Il n’est pas transmis service toohello via une opération d’API.  
  
la section suivante de Hello décrit format général de hello d’un fichier de manifeste de lecteur :  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveManifest Version="2014-11-01">  
  <Drive>  
    <DriveId>drive-id</DriveId>  
    import-export-credential  
  
    <!-- First Blob List -->  
    <BlobList>  
      <!-- Global properties and metadata that applies tooall blobs -->  
      [<MetadataPath Hash="md5-hash">global-metadata-file-path</MetadataPath>]  
      [<PropertiesPath   
        Hash="md5-hash">global-properties-file-path</PropertiesPath>]  
  
      <!-- First Blob -->  
      <Blob>  
        <BlobPath>blob-path-relative-to-account</BlobPath>  
        <FilePath>file-path-relative-to-transfer-disk</FilePath>  
        [<ClientData>client-data</ClientData>]  
        [<Snapshot>snapshot</Snapshot>]  
        <Length>content-length</Length>  
        [<ImportDisposition>import-disposition</ImportDisposition>]  
        page-range-list-or-block-list          
        [<MetadataPath Hash="md5-hash">metadata-file-path</MetadataPath>]  
        [<PropertiesPath Hash="md5-hash">properties-file-path</PropertiesPath>]  
      </Blob>  
  
      <!-- Second Blob -->  
      <Blob>  
      . . .  
      </Blob>  
    </BlobList>  
  
    <!-- Second Blob List -->  
    <BlobList>  
    . . .  
    </BlobList>  
  </Drive>  
</DriveManifest>  
  
import-export-credential ::=   
  <StorageAccountKey>storage-account-key</StorageAccountKey> | <ContainerSas>container-sas</ContainerSas>  
  
page-range-list-or-block-list ::=   
  page-range-list | block-list  
  
page-range-list ::=   
    <PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       Hash="md5-hash"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       Hash="md5-hash"/>]  
    </PageRangeList>  
  
block-list ::=  
    <BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       Hash="md5-hash"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       Hash="md5-hash"/>]  
    </BlockList>  

```

## <a name="manifest-xml-elements-and-attributes"></a>Éléments et attributs XML d’un manifeste

éléments de données Hello et les attributs de format XML de manifeste lecteur hello sont spécifiés dans hello tableau suivant.  
  
|Élément XML|Type|Description|  
|-----------------|----------|-----------------|  
|`DriveManifest`|Élément racine|élément racine de Hello du fichier de manifeste hello. Tous les autres éléments dans le fichier de hello sont sous cet élément.|  
|`Version`|Attribut, Chaîne|version de Hello du fichier de manifeste hello.|  
|`Drive`|Élément XML imbriqué|Contient le manifeste hello pour chaque lecteur.|  
|`DriveId`|String|Bonjour identificateur unique de lecteur de hello. Identificateur Hello est disponible en interrogeant lecteur hello pour son numéro de série. numéro de série du lecteur Hello est généralement imprimé hello en dehors de lecteur hello. Hello `DriveID` élément doit apparaître avant tout `BlobList` dans fichier de manifeste hello.|  
|`StorageAccountKey`|String|Obligatoire pour les travaux d’importation si et seulement si `ContainerSas` n’est pas spécifié. clé de compte Hello pour hello compte de stockage Azure associé à la tâche de hello.<br /><br /> Cet élément est omis du manifeste de hello pour une opération d’exportation.|  
|`ContainerSas`|String|Obligatoire pour les travaux d’importation si et seulement si `StorageAccountKey` n’est pas spécifié. Hello SAP de conteneur pour accéder aux objets BLOB de hello associé hello travail. Consultez [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) pour son format. Cet élément est omis du manifeste de hello pour une opération d’exportation.|  
|`ClientCreator`|String|Spécifie le client hello qui a créé le fichier XML de hello. Cette valeur n’est pas interprétée par hello service Import/Export.|  
|`BlobList`|Élément XML imbriqué|Contient une liste d’objets BLOB qui font partie de l’importation de hello ou de travail d’exportation. Chaque objet blob dans une liste d’objets blob partages hello mêmes métadonnées et propriétés.|  
|`BlobList/MetadataPath`|String|facultatif. Spécifie le chemin d’accès relatif de hello d’un fichier sur disque hello qui contient des métadonnées par défaut hello qui seront définies sur les objets BLOB dans la liste d’objets blob hello pour une opération d’importation. Ces métadonnées peuvent éventuellement être remplacées, objet blob par objet blob.<br /><br /> Cet élément est omis du manifeste de hello pour une opération d’exportation.|  
|`BlobList/MetadataPath/@Hash`|Attribut, Chaîne|Spécifie la valeur de hachage MD5 encodé en Base16 hello pour le fichier de métadonnées hello.|  
|`BlobList/PropertiesPath`|String|facultatif. Spécifie le chemin d’accès relatif de hello d’un fichier sur disque hello qui contient les propriétés par défaut hello qui seront définies sur les objets BLOB dans la liste d’objets blob hello pour une opération d’importation. Ces propriétés peuvent éventuellement être remplacées, objet blob par objet blob.<br /><br /> Cet élément est omis du manifeste de hello pour une opération d’exportation.|  
|`BlobList/PropertiesPath/@Hash`|Attribut, Chaîne|Spécifie la valeur de hachage MD5 encodé en Base16 hello pour le fichier de propriétés hello.|  
|`Blob`|Élément XML imbriqué|Contient des informations sur chaque objet blob de chaque liste d’objets blob.|  
|`Blob/BlobPath`|String|Hello relatif URI toohello blob, commençant par le nom du conteneur hello. Si l’objet blob de hello est dans le conteneur racine, il doit commencer par `$root`.|  
|`Blob/FilePath`|String|Spécifie le fichier de toohello de chemin d’accès relatif de hello sur le lecteur de hello. Pour les travaux d’exportation, chemin d’objet blob de hello sera utilisé pour le chemin de fichier hello si possible ; *par exemple,*, `pictures/bob/wild/desert.jpg` seront exportées trop`\pictures\bob\wild\desert.jpg`. Toutefois, en raison de limitations toohello des noms NTFS, un objet blob peut être fichier tooa exporté avec un chemin d’accès qui ne ressemble pas le chemin d’accès de hello blob.|  
|`Blob/ClientData`|String|facultatif. Contient des commentaires du client de hello. Cette valeur n’est pas interprétée par hello service Import/Export.|  
|`Blob/Snapshot`|DateTime|Facultatif pour les travaux d’exportation. Spécifie l’identificateur hello d’un instantané d’objet blob exporté.|  
|`Blob/Length`|Entier |Spécifie la longueur totale de hello d’objet blob de hello en octets. valeur de Hello peut être Go too200 pour un objet blob de blocs et to too1 pour un objet blob de pages. Pour un objet blob de pages, cette valeur doit être un multiple de 512.|  
|`Blob/ImportDisposition`|String|Facultatif pour les travaux d’importation, omis pour les travaux d’exportation. Spécifie comment hello service d’importation/exportation doit gérer les cas de hello pour un travail d’importation dans lequel il existe un objet blob avec hello même nom que celui déjà. Si cette valeur est omise du manifeste d’importation hello, valeur par défaut de hello est `rename`.<br /><br /> les valeurs Hello pour cet élément sont les suivantes :<br /><br /> -   `no-overwrite`: Si un objet blob de destination existe déjà avec hello même nom, opération d’importation hello ignore l’importation de ce fichier.<br />-   `overwrite`: Tout objet blob de destination existant est remplacé par le fichier nouvellement importé hello.<br />-   `rename`: hello un nouvel objet blob est téléchargé avec un nom modifié.<br /><br /> Hello, modification du nom de la règle est la suivante :<br /><br /> -Si le nom d’objet blob hello ne contient pas un point, un nouveau nom est généré en ajoutant `(2)` toohello d’origine nom d’objet blob ; si ce nom est en conflit avec un nom d’objet blob existant, puis `(3)` est ajouté à la place de `(2)`; et ainsi de suite.<br />-Si le nom d’objet blob hello contient un point, partie hello suivant le dernier point de hello est considérée comme nom de l’extension hello. Toohello similaires au-dessus de la procédure, `(2)` est inséré avant hello du dernier point toogenerate un nouveau nom ; si le nouveau nom de hello toujours est en conflit avec un nom d’objet blob existant, puis hello service essaie de `(3)`, `(4)`, et ainsi de suite jusqu'à ce que le pas en conflit nom est trouvé.<br /><br /> Voici quelques exemples :<br /><br /> objet blob de Hello `BlobNameWithoutDot` sera renommé en :<br /><br /> `BlobNameWithoutDot (2)  // if BlobNameWithoutDot exists`<br /><br /> `BlobNameWithoutDot (3)  // if both BlobNameWithoutDot and BlobNameWithoutDot (2) exist`<br /><br /> objet blob de Hello `Seattle.jpg` sera renommé en :<br /><br /> `Seattle (2).jpg  // if Seattle.jpg exists`<br /><br /> `Seattle (3).jpg  // if both Seattle.jpg and Seattle (2).jpg exist`|  
|`PageRangeList`|Élément XML imbriqué|Obligatoire pour un objet blob de pages.<br /><br /> Pour une importation opération, spécifie une liste de plages d’octets d’un toobe fichier importé. Chaque plage de pages est décrite par un décalage et la longueur dans le fichier source hello qui décrit la plage de pages hello, ainsi que d’un hachage MD5 de région de hello. Hello `Hash` attribut d’une plage de pages est requis. service de Hello s’assure que hachage hello de données hello dans l’objet blob de hello correspond au hachage MD5 de hello calculée à partir de la plage de pages hello. N’importe quel nombre de plages de pages peut être toodescribe utilisé un fichier pour une importation, avec la taille totale de hello jusqu'à too1 to. Toutes les plages de pages doivent être triées par décalage et aucun chevauchement n’est autorisé.<br /><br /> Pour une opération d’exportation, spécifie un jeu de plages d’octets d’un objet blob qui ont été exportées toohello lecteur.<br /><br /> les plages de pages Hello ensemble peuvent couvrir des que les sous-plages d’un fichier ou un objet blob.  partie restante de Hello du fichier hello non couvert par une plage de pages est attendue et son contenu peut être indéfini.|  
|`PageRange`|Élément XML|Représente une plage de pages.|  
|`PageRange/@Offset`|Attribut, Entier|Spécifie le décalage hello dans le fichier de transfert hello et blob hello où hello spécifié la plage de pages commence. Cette valeur doit être un multiple de 512.|  
|`PageRange/@Length`|Attribut, Entier|Spécifie la longueur de plage de pages hello hello. Cette valeur doit être un multiple de 512 et inférieure à 4 Mo.|  
|`PageRange/@Hash`|Attribut, Chaîne|Spécifie la valeur de hachage MD5 encodé en Base16 hello pour la plage de pages hello.|  
|`BlockList`|Élément XML imbriqué|Obligatoire pour un objet blob de blocs avec des blocs nommés.<br /><br /> Pour une opération d’importation, liste de blocs hello spécifie un ensemble de blocs qui sera importé dans le stockage Azure. Pour une opération d’exportation, liste de blocs hello spécifie où chaque bloc a été stocké dans le fichier hello sur le disque d’exportation hello. Chaque bloc est décrite par un offset dans le fichier de hello et une longueur de bloc ; chaque bloc est en outre nommé par un attribut d’ID de bloc et contient un hachage MD5 pour le bloc de hello. Les too50, 000 blocs peuvent être utilisé toodescribe un objet blob.  Tous les blocs doivent être classées par décalage et ensemble doit couvrir la plage complète du fichier de hello, hello *c'est-à-dire*, il ne doit y être aucun espace entre les blocs. Si l’objet blob de hello n’est pas plus de 64 Mo, ID de bloc hello pour chaque bloc doit être soit tous absents ou tous présent. ID de bloc sont toobe requis des chaînes encodées en Base64. Consultez [Put Block](/rest/api/storageservices/put-block) pour plus d’informations sur les conditions requises pour les ID de bloc.|  
|`Block`|Élément XML|Représente un bloc.|  
|`Block/@Offset`|Attribut, Entier|Spécifie le décalage hello où le bloc spécifié de hello commence.|  
|`Block/@Length`|Attribut, Entier|Spécifie le nombre de hello d’octets dans le bloc de hello ; Cette valeur doit être pas plus de 4 Mo.|  
|`Block/@Id`|Attribut, Chaîne|Spécifie une chaîne représentant l’ID de bloc hello pour le bloc de hello.|  
|`Block/@Hash`|Attribut, Chaîne|Spécifie le hachage MD5 encodé en Base16 de hello du bloc de hello.|  
|`Blob/MetadataPath`|String|facultatif. Spécifie le chemin d’accès relatif de hello d’un fichier de métadonnées. Pendant une importation, les métadonnées hello sont définie sur l’objet blob de destination hello. Pendant une opération d’exportation, les métadonnées de l’objet blob de hello sont stockées dans le fichier de métadonnées hello sur le lecteur de hello.|  
|`Blob/MetadataPath/@Hash`|Attribut, Chaîne|Spécifie le hachage MD5 encodé en Base16 de hello du fichier de métadonnées de l’objet blob de hello.|  
|`Blob/PropertiesPath`|String|facultatif. Spécifie le chemin d’accès relatif de hello d’un fichier de propriétés. Pendant une importation, les propriétés de hello sont définies sur l’objet blob de destination hello. Pendant une opération d’exportation, les propriétés d’objet blob hello sont stockées dans le fichier de propriétés hello sur le lecteur de hello.|  
|`Blob/PropertiesPath/@Hash`|Attribut, Chaîne|Spécifie le hachage MD5 encodé en Base16 de hello du fichier de propriétés de l’objet blob de hello.|  
  
## <a name="next-steps"></a>Étapes suivantes
 
* [API REST d’importation/exportation de stockage](/rest/api/storageimportexport/)
