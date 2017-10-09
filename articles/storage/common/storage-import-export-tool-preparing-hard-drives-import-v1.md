---
title: importer le travail - v1, les disques durs aaaPreparing pour une importation/exportation Azure | Documents Microsoft
description: "Découvrez comment tooprepare les disques durs à l’aide de hello WAImportExport v1 outil toocreate un travail d’importation pour le service d’importation/exportation Azure hello."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 3d818245-8b1b-4435-a41f-8e5ec1f194b2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 1eb0c3c51e984e2869b5268254f468d4b43e9d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-hard-drives-for-an-import-job"></a>Préparation des disques durs pour un travail d’importation
tooprepare un ou plusieurs disques durs pour un travail d’importation, procédez comme suit :

-   Identifier les tooimport de données hello en hello service Blob

-   Identifier les répertoires virtuels cibles et les objets BLOB dans hello service Blob

-   Déterminer le nombre de disques nécessaires

-   Copiez tooeach de données hello vos disques durs

 Pour un exemple de workflow, consultez [tooPrepare exemple de Workflow les disques durs pour un travail d’importation](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md).

## <a name="identify-hello-data-toobe-imported"></a>Identifier hello toobe de données importée
 Hello première étape toocreating un travail d’importation est toodetermine les répertoires et fichiers que vous allez tooimport. Il peut s’agir d’une liste de répertoires, d’une liste de fichiers uniques ou d’une combinaison des deux. Lorsqu’un répertoire est inclus, tous les fichiers dans le répertoire de hello et ses sous-répertoires feront partie du travail d’importation hello.

> [!NOTE]
>  Étant donné que les sous-répertoires sont inclus de manière récursive lorsqu’un répertoire parent est inclus, spécifiez uniquement le répertoire de parent hello. Ne spécifiez pas un de ses sous-répertoires.
>
>  Actuellement, hello Microsoft Azure Import/Export Tool a hello après limitation : si un répertoire contient plus de données que peut contenir un disque dur, répertoire de hello doit toobe divisé en répertoires de plus petits. Par exemple, si un répertoire contient 2,5 To de données et hello capacité du disque dur est uniquement 2 To, vous devez le répertoire de 2,5 to toobreak hello en répertoires de plus petits. Cette limitation sera traitée dans une version plus récente de l’outil de hello.

## <a name="identify-hello-destination-locations-in-hello-blob-service"></a>Identifier les emplacements de destination hello dans le service blob hello
 Pour chaque répertoire ou un fichier qui sera importé, vous devez tooidentify un répertoire virtuel de destination ou un objet blob Bonjour service Blob Azure. Vous utiliserez ces cibles en tant qu’entrées toohello outil d’importation/exportation Azure. Notez que les répertoires doivent être délimités par le caractère barre oblique hello « / ».

 Hello tableau suivant présente quelques exemples de cibles blob :

|Fichier ou répertoire source|Répertoire virtuel ou objet blob cibles|
|------------------------------|-------------------------------------------|
|H:\Video|https://mystorageaccount.blob.core.windows.net/video|
|H:\Photo|https://mystorageaccount.blob.core.windows.net/photo|
|K:\Temp\FavoriteVideo.ISO|https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO|
|\\\myshare\john\music|https://mystorageaccount.blob.core.windows.net/music|

## <a name="determine-how-many-drives-are-needed"></a>Déterminer le nombre de disques nécessaires
 Ensuite, vous devez toodetermine :

-   nombre de Hello de disques durs nécessaires toostore les données de salutation.

-   répertoires de Hello et/ou les fichiers autonomes qui seront copié tooeach de votre disque dur.

 Assurez-vous que vous disposez de nombre hello de disques durs, que vous devez transférer les données de salutation toostore.

## <a name="copy-data-tooyour-hard-drive"></a>Copiez le disque dur de données tooyour
 Cette section décrit comment toocall hello toocopy de l’outil d’importation/exportation Azure tooone de vos données ou de plusieurs disques durs. Chaque fois que vous appelez hello outil d’importation/exportation Azure, vous créez un nouveau *session de copie*. Vous créez au moins une session de copie pour chaque lecteur toowhich vous copiez des données ; Dans certains cas, vous devrez peut-être plusieurs toocopy de session de copie tous les de votre lecteur de toosingle de données. Voici quelques raisons pour lesquelles vous devrez peut-être créer plusieurs sessions de copie :

-   Vous devez créer une session de copie distincte pour chaque disque sur lequel vous souhaitez copier des données.

-   Une session de copie peut copier un seul répertoire ou un lecteur de toohello d’objet blob unique. Si vous copiez plusieurs répertoires, plusieurs objets BLOB ou une combinaison des deux, vous devez toocreate plusieurs sessions de copie.

-   Vous pouvez spécifier les propriétés et les métadonnées qui seront définies sur les objets BLOB de hello importés en tant que partie d’un travail d’importation. propriétés de Hello ou les métadonnées que vous spécifiez pour une session de copie seront appliqueront BLOB tooall spécifié par cette session de copie. Si vous souhaitez toospecify différentes propriétés ou les métadonnées pour certains objets BLOB, vous devez toocreate distinct session de copie. Consultez [définition des propriétés et des métadonnées au cours de processus d’importation de hello](storage-import-export-tool-setting-properties-metadata-import-v1.md)pour plus d’informations.

> [!NOTE]
>  Si vous avez plusieurs ordinateurs qui répondent aux exigences de hello décrites dans [configuration hello, outil d’importation/exportation Azure](storage-import-export-tool-setup-v1.md), vous pouvez copier les disques durs toomultiple de données en parallèle en exécutant une instance de cet outil sur chaque ordinateur.

 Pour chaque disque dur que vous préparez avec l’outil d’importation/exportation Azure de hello, outil de hello crée un seul fichier journal. Vous devez de votre travail d’importation hello lecteurs toocreate tous les fichiers de journal hello. fichier de journal Hello peut également être préparation du lecteur tooresume utilisé si l’outil de hello est interrompue.

### <a name="azure-importexport-tool-syntax-for-an-import-job"></a>Syntaxe de l’outil Azure Import/Export pour un travail d’importation
 lecteurs tooprepare pour un travail d’importation, appelez hello outil d’importation/exportation Azure avec hello **PrepImport** commande. Les paramètres inclus dépend de si cela est hello première session de copie ou d’une session de copie suivante.

 première session de copie pour un lecteur Hello requiert des paramètres supplémentaires toospecify hello clé du compte ; lettre de lecteur cible Hello ; Indique si le lecteur de hello doit être formaté ; Si le lecteur de hello doit être chiffré et si tel est le cas, hello clé BitLocker ; et le répertoire du journal hello. Voici hello syntaxe d’une toocopy de session de copie initiale un répertoire ou un seul fichier :

 **Tout d’abord copier session toocopy un seul répertoire**

 `WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 **Tout d’abord copier session toocopy un seul fichier**

 `WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcfile:<SourceFile> /dstblob:<DestinationBlobPath> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 Dans les sessions de copie suivantes, il est inutile des paramètres initiaux de toospecify hello. Un répertoire ou un seul fichier, voici syntaxe hello pour un toocopy de session de copie suivantes :

 **Sessions de copie suivantes toocopy un seul répertoire**

 `WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 **Sessions de copie suivantes toocopy un seul fichier**

 `WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /srcfile:<SourceFile> /dstblob:<DestinationBlobPath> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

### <a name="parameters-for-hello-first-copy-session-for-a-hard-drive"></a>Paramètres pour hello tout d’abord copieront la session pour un disque dur
 Chaque fois que vous exécutez des fichiers de toocopy d’outil d’importation/exportation Azure hello toohello de disque dur, outil de hello crée une session de copie. Chaque session de copie copie un seul répertoire ou un disque dur tooa de fichier unique. état Hello de session de copie hello est écrit le fichier de feuille de toohello. Si une session de copie est interrompue (par exemple, en raison de tooa coupure de courant), il peut être reprise par réexécuter l’outil de hello et en spécifiant le fichier du journal sur la ligne de commande hello hello.

> [!WARNING]
>  Si vous spécifiez hello **/format** paramètre hello première session de copie, hello lecteur est formaté et toutes les données sur le lecteur de hello seront effacées. Nous vous recommandons d’utiliser des disques vides uniquement pour votre session de copie.

 commande Hello utilisée pour hello première session de copie pour chaque disque requiert des paramètres différents de ceux des commandes hello pour les sessions de copie suivantes. Hello tableau suivant répertorie les paramètres supplémentaires hello qui sont disponibles pour hello première session de copie :

|Paramètre de ligne de commande|Description|
|-----------------------------|-----------------|
|**/sk:**&lt;StorageAccountKey\>|`Optional.`clé de compte de stockage Hello pour les données hello toowhich de compte de stockage hello est importée. Vous devez inclure **/sk :**< StorageAccountKey\> ou **/csas :**< ContainerSas\> dans la commande hello.|
|**/csas:**&lt;ContainerSas\>|`Optional`. conteneur Hello compte de stockage SAS toouse tooimport données toohello. Vous devez inclure **/sk :**< StorageAccountKey\> ou **/csas :**< ContainerSas\> dans la commande hello.<br /><br /> valeur Hello pour ce paramètre doit commencer par le nom du conteneur hello, suivi d’un point d’interrogation ( ?) et un jeton SAS de hello. Par exemple :<br /><br /> `mycontainer?sv=2014-02-14&sr=c&si=abcde&sig=LiqEmV%2Fs1LF4loC%2FJs9ZM91%2FkqfqHKhnz0JM6bqIqN0%3D&se=2014-11-20T23%3A54%3A14Z&sp=rwdl`<br /><br /> autorisations de Hello, qu’elles soient spécifiées sur l’URL de hello ou dans une stratégie d’accès stockée, doivent inclure en lecture, écriture et suppression pour les travaux d’importation et en lecture, écriture et liste de travaux d’exportation.<br /><br /> Lorsque ce paramètre est spécifié, tous les objets BLOB toobe, importé ou exporté doit être dans le conteneur hello spécifié dans la signature d’accès partagé hello.|
|**/t:**&lt;TargetDriveLetter\>|`Required.`lettre de lecteur Hello du disque dur de cible hello pour hello session actuelle de copie, sans hello deux-points de fin.|
|**/format**|`Optional.`Spécifiez ce paramètre lorsque le lecteur de hello doit être toobe mise en forme ; Sinon, omettez-le. Avant de l’outil de hello des formats de disque de hello, il demande une confirmation à partir de la console. toosuppress hello confirmation, spécifiez le paramètre /silentmode de hello.|
|**/silentmode**|`Optional.`Spécifiez ce paramètre toosuppress hello une confirmation pour hello formatage du disque.|
|**/encrypt**|`Optional.`Spécifiez ce paramètre lorsque le lecteur de hello n’a pas encore été chiffré avec BitLocker et les besoins toobe chiffré par hello outil. Si le lecteur de hello a déjà été chiffré avec BitLocker, puis omettre ce paramètre et spécifiez hello `/bk` paramètre, en fournissant la clé BitLocker existante de hello.<br /><br /> Si vous spécifiez hello `/format` paramètre, vous devez également spécifier hello `/encrypt` paramètre.|
|**/bk:**&lt;BitLockerKey\>|`Optional.`Si `/encrypt` est spécifié, omettez ce paramètre. Si `/encrypt` est omis, vous devez toohave déjà avoir chiffré lecteur hello avec BitLocker. Utilisez cette clé de paramètre toospecify hello BitLocker. Le chiffrement BitLocker est requis pour tous les disques durs pour les travaux d’importation.|
|**/logdir:**&lt;LogDirectory\>|`Optional.`répertoire du journal Hello spécifie qu'un toobe active utilisée toostore les journaux détaillés, ainsi que les fichiers manifestes temporaires. Si non spécifié, répertoire actuel de hello sera utilisé comme répertoire de journal hello.|

### <a name="parameters-required-for-all-copy-sessions"></a>Paramètres requis pour toutes les sessions de copie
 fichier journal de Hello contient l’état de hello pour toutes les sessions de copie pour un disque dur. Il contient également des hello informations nécessaires toocreate hello importer le travail. Vous devez toujours spécifier un fichier journal lors de l’exécution hello outil d’importation/exportation Azure, ainsi que d’un ID de session de copie :

|||
|-|-|
|Paramètre de ligne de commande|Description|
|**/j:**&lt;JournalFile\>|`Required.`fichier de journal toohello Hello chemin d’accès. Chaque disque doit avoir un seul fichier journal. Notez que ce fichier de journal hello ne doit pas résider sur le lecteur cible hello. extension de fichier journal Hello est `.jrn`.|
|**/id:**&lt;SessionId\>|`Required.`ID de session Hello identifie une session de copie. Il est utilisé tooensure précise de récupération d’une session de copie interrompue. Les fichiers qui sont copiés dans une session de copie sont stockés dans un répertoire nommé d’après l’ID de session hello sur le lecteur cible hello.|

### <a name="parameters-for-copying-a-single-directory"></a>Paramètres de copie d’un seul répertoire
 Lorsque vous copiez un seul répertoire, suivantes hello et des paramètres facultatifs s’appliquent :

|Paramètre de ligne de commande|Description|
|----------------------------|-----------------|
|**/srcdir:**&lt;SourceDirectory\>|`Required.`répertoire source Hello qui contient les fichiers toobe copiés toohello le lecteur cible. chemin d’accès du répertoire Hello doit être un chemin d’accès absolu (pas un chemin d’accès relatif).|
|**/dstdir:**&lt;DestinationBlobVirtualDirectory\>|`Required.`Hello chemin d’accès toohello répertoire virtuel de destination dans votre compte de stockage Windows Azure. répertoire virtuel de Hello peut ou ne peut pas exister.<br /><br /> Vous pouvez spécifier un conteneur ou un préfixe de blob comme `music/70s/`. répertoire de destination Hello doit commencer par le nom du conteneur hello, suivi par une barre oblique « / » et peut éventuellement inclure un répertoire virtuel d’objets blob qui se termine par « / ».<br /><br /> Lorsque le conteneur de destination hello est le conteneur racine de hello, vous devez spécifier explicitement le conteneur racine de hello, y compris hello barre oblique, comme `$root/`. Étant donné que les objets BLOB sous le conteneur racine de hello ne peut pas inclure « / » dans leurs noms, tous les sous-répertoires dans le répertoire source hello ne seront pas copiés lorsque le répertoire de destination hello est le conteneur racine de hello.<br /><br /> Lorsque vous spécifiez des répertoires virtuels de destination ou des objets BLOB, être toouse que les noms de conteneur valide. N’oubliez pas que les noms de conteneur doivent être en minuscules. Pour connaître les règles d’affectation de noms aux conteneurs, consultez [Naming and Referencing Containers, Blobs, and Metadata (Affectation de noms et références aux conteneurs, blobs et métadonnées)](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata).|
|**/Disposition:**&lt;rename&amp;#124;no-overwrite&amp;#124;overwrite&gt;|`Optional.`Spécifie le comportement de hello lorsqu’un objet blob avec hello spécifié d’adresse existe déjà. Les valeurs valides pour ce paramètre sont : `rename`, `no-overwrite` et `overwrite`. Notez que ces valeurs sont sensibles à la casse. Si aucune valeur n’est spécifiée, valeur par défaut de hello est `rename`.<br /><br /> Hello la valeur spécifiée pour ce paramètre affecte tous les fichiers hello dans le répertoire hello spécifié par hello `/srcdir` paramètre.|
|**/BlobType:**&lt;BlockBlob&amp;#124;PageBlob&gt;|`Optional.`Spécifie le type d’objet blob hello pour les objets BLOB de destination hello. Les valeurs autorisées sont : `BlockBlob` et `PageBlob`. Notez que ces valeurs sont sensibles à la casse. Si aucune valeur n’est spécifiée, valeur par défaut de hello est `BlockBlob`.<br /><br /> Dans la plupart des cas, `BlockBlob` est recommandé. Si vous spécifiez `PageBlob`, la longueur de chaque fichier dans le répertoire de hello hello doit être un multiple de 512, taille hello d’une page pour les objets BLOB de pages.|
|**/PropertyFile:**&lt;PropertyFile\>|`Optional.`Fichier de propriétés chemin d’accès toohello pour les objets BLOB de destination hello. Pour plus d’informations, consultez [Format de fichier de propriétés et de métadonnées du service d’importation/exportation](../storage-import-export-file-format-metadata-and-properties.md).|
|**/MetadataFile:**&lt;MetadataFile\>|`Optional.`Fichier de métadonnées chemin d’accès toohello pour les objets BLOB de destination hello. Pour plus d’informations, consultez [Format de fichier de propriétés et de métadonnées du service d’importation/exportation](../storage-import-export-file-format-metadata-and-properties.md).|

### <a name="parameters-for-copying-a-single-file"></a>Paramètres de copie d’un seul fichier
 Lorsque vous copiez un seul fichier, hello paramètres obligatoires et facultatifs suivants s’appliquent :

|Paramètre de ligne de commande|Description|
|----------------------------|-----------------|
|**/srcfile:**&lt;SourceFile\>|`Required.`Hello chemin d’accès complet toohello fichier toobe copié. chemin d’accès du répertoire Hello doit être un chemin d’accès absolu (pas un chemin d’accès relatif).|
|**/dstblob:**&lt;DestinationBlobPath\>|`Required.`Hello chemin d’accès toohello objet blob de destination dans votre compte de stockage Windows Azure. objet blob de Hello peut ou ne peut pas exister.<br /><br /> Spécifiez hello blob dont le nom commence par le nom de conteneur hello. nom d’objet blob Hello ne peut pas commencer par « / » ou le nom de compte de stockage hello. Pour connaître les règles d’affectation de noms aux blobs, consultez [Naming and Referencing Containers, Blobs, and Metadata (Affectation de noms et références aux conteneurs, blobs et métadonnées)](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata).<br /><br /> Lorsque le conteneur de destination hello est le conteneur racine de hello, vous devez explicitement spécifier `$root` comme hello conteneur, tel que `$root/sample.txt`. Notez que les objets BLOB sous le conteneur racine de hello ne peut pas inclure « / » dans leur nom.|
|**/Disposition:**&lt;rename&amp;#124;no-overwrite&amp;#124;overwrite&gt;|`Optional.`Spécifie le comportement de hello lorsqu’un objet blob avec hello spécifié d’adresse existe déjà. Les valeurs valides pour ce paramètre sont : `rename`, `no-overwrite` et `overwrite`. Notez que ces valeurs sont sensibles à la casse. Si aucune valeur n’est spécifiée, valeur par défaut de hello est `rename`.|
|**/BlobType:**&lt;BlockBlob&amp;#124;PageBlob&gt;|`Optional.`Spécifie le type d’objet blob hello pour les objets BLOB de destination hello. Les valeurs autorisées sont : `BlockBlob` et `PageBlob`. Notez que ces valeurs sont sensibles à la casse. Si aucune valeur n’est spécifiée, valeur par défaut de hello est `BlockBlob`.<br /><br /> Dans la plupart des cas, `BlockBlob` est recommandé. Si vous spécifiez `PageBlob`, la longueur de chaque fichier dans le répertoire de hello hello doit être un multiple de 512, taille hello d’une page pour les objets BLOB de pages.|
|**/PropertyFile:**&lt;PropertyFile\>|`Optional.`Fichier de propriétés chemin d’accès toohello pour les objets BLOB de destination hello. Pour plus d’informations, consultez [Format de fichier de propriétés et de métadonnées du service d’importation/exportation](../storage-import-export-file-format-metadata-and-properties.md).|
|**/MetadataFile:**&lt;MetadataFile\>|`Optional.`Fichier de métadonnées chemin d’accès toohello pour les objets BLOB de destination hello. Pour plus d’informations, consultez [Format de fichier de propriétés et de métadonnées du service d’importation/exportation](../storage-import-export-file-format-metadata-and-properties.md).|

### <a name="resuming-an-interrupted-copy-session"></a>Reprise d’une session de copie interrompue
 Si une session de copie est interrompue pour une raison quelconque, vous pouvez le reprendre en exécutant l’outil de hello avec le fichier journal hello spécifié :

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /ResumeSession
```

 Seule hello dernière session de copie, s’est terminé anormalement, peut être reprise.

> [!IMPORTANT]
>  Lorsque vous reprenez une session de copie, ne modifiez pas répertoires et fichiers de données sources hello en ajoutant ou supprimant des fichiers.

### <a name="aborting-an-interrupted-copy-session"></a>Annulation d’une session de copie interrompue
 Si une session de copie est interrompue et il n’est pas possible de tooresume (par exemple, si un répertoire source est inaccessible), vous devez annuler hello session active afin qu’elle peut être annulée précédent et nouvelles sessions de copie peuvent être démarrées :

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AbortSession
```

 Hello uniquement dernière session de copie s’est terminé anormalement, peut être annulée. Notez que vous ne pouvez pas abandonner hello première session de copie pour un lecteur. Au lieu de cela, vous devez redémarrer la session de copie hello avec un nouveau fichier journal.

## <a name="next-steps"></a>Étapes suivantes

* [Configuration des hello, outil d’importation/exportation Azure](storage-import-export-tool-setup-v1.md)
* [Définition des propriétés et métadonnées pendant hello processus d’importation](storage-import-export-tool-setting-properties-metadata-import-v1.md)
* [Exemple workflow tooprepare les disques durs pour un travail d’importation](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
* [Référence rapide pour les commandes fréquemment utilisées](storage-import-export-tool-quick-reference-v1.md) 
* [Consultation de l’état du travail avec les fichiers journaux de copie](storage-import-export-tool-reviewing-job-status-v1.md)
* [Réparation d’un travail d’importation](storage-import-export-tool-repairing-an-import-job-v1.md)
* [Réparation d’un travail d’exportation](storage-import-export-tool-repairing-an-export-job-v1.md)
* [Résolution des problèmes de hello outil d’importation/exportation Azure](storage-import-export-tool-troubleshooting-v1.md)
