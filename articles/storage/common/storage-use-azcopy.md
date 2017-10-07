---
title: "tooAzure de données aaaCopy ou déplacer le stockage avec AzCopy sur Windows | Documents Microsoft"
description: "Utilisez hello AzCopy sur Windows utilitaire toomove ou copie de données tooor à partir des objets blob, table et le contenu du fichier. Copier des données tooAzure stockage à partir de fichiers locales, ou copier des données dans ou entre des comptes de stockage. Migrer facilement vos données de tooAzure stockage."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: aa155738-7c69-4a83-94f8-b97af4461274
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/14/2017
ms.author: seguler
ms.openlocfilehash: a063a0380b7b8e6b212d0cec276f7d0f421936ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-azcopy-on-windows"></a>Transfert de données avec hello AzCopy sur Windows
AzCopy est un utilitaire de ligne de commande conçu pour la copie des données tooand à partir du stockage d’objets Blob Microsoft Azure, de fichier et de Table à l’aide de commandes simples avec des performances optimales. Vous pouvez copier des données à partir d’un objet tooanother dans votre compte de stockage, ou entre des comptes de stockage.

Il existe deux versions d’AzCopy que vous pouvez télécharger. AzCopy sur Windows est intégré à .NET Framework et offre des options en ligne de commande de style Windows. [AzCopy sur Linux](storage-use-azcopy-linux.md) est intégré à .NET Core Framework, qui cible les plateformes Linux en offrant des options en ligne de commande de style POSIX. Cet article est consacré à AzCopy sur Windows.

## <a name="download-and-install-azcopy"></a>Téléchargement et installation d’AzCopy
### <a name="azcopy-on-windows"></a>AzCopy sur Windows
Télécharger hello [version la plus récente de AzCopy sur Windows](http://aka.ms/downloadazcopy).

#### <a name="installation-on-windows"></a>Installation sur Windows
Après avoir installé AzCopy sur Windows à l’aide du programme d’installation Bonjour, ouvrez une fenêtre de commande et accédez répertoire d’installation toohello AzCopy sur votre ordinateur - où hello `AzCopy.exe` exécutable se trouve. Si vous le souhaitez, vous pouvez ajouter le chemin d’accès de hello AzCopy installation emplacement tooyour système. Par défaut, AzCopy est installé trop`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` ou `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.

## <a name="writing-your-first-azcopy-command"></a>Écriture de votre première commande AzCopy
syntaxe de base Hello pour les commandes AzCopy est la suivante :

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

Hello suivant exemples illustrent une variété de scénarios pour la copie des données tooand à partir d’objets BLOB Microsoft Azure, les fichiers et les Tables. Consultez toohello [AzCopy paramètres](#azcopy-parameters) section pour obtenir une explication détaillée des paramètres hello utilisées dans chaque exemple.

## <a name="blob-download"></a>Blob : Téléchargement
### <a name="download-single-blob"></a>Télécharger un seul objet blob

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

Notez que si le dossier de hello `C:\myfolder` n’existe pas, AzCopy crée il et téléchargement `abc.txt ` dans le dossier hello.

### <a name="download-single-blob-from-secondary-region"></a>Télécharger un objet blob unique depuis la région secondaire

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

Notez que vous devez avoir un accès en lecture activé pour le stockage géo-redondant.

### <a name="download-all-blobs"></a>Télécharger tous les objets blob

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

Supposons suivant de hello BLOB réside dans le conteneur spécifié de hello :  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

Après l’opération de téléchargement hello hello active `C:\myfolder` inclut hello fichiers suivants :

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

Si vous ne spécifiez pas l’option `/S`, aucun objet blob n’est téléchargé.

### <a name="download-blobs-with-specified-prefix"></a>Téléchargement d’objets blob avec le préfixe spécifié

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

Supposons suivant de hello BLOB réside dans le conteneur spécifié de hello. Tous les objets BLOB commençant par préfixe de hello `a` sont téléchargés :

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

Après l’opération de téléchargement hello hello dossier `C:\myfolder` inclut hello fichiers suivants :

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

préfixe de Hello applique le répertoire virtuel toohello, ce qui constitue hello première partie du nom d’objet blob hello. Exemple hello ci-dessus, répertoire virtuel de hello ne correspond pas au préfixe spécifié de hello, donc il n’est pas téléchargé. En outre, si hello option `\S` n’est pas spécifié, AzCopy ne télécharge pas les objets BLOB.

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a>Définir l’heure de dernière modification de hello de fichiers exportés toobe identique hello d’objets BLOB sources

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

Vous pouvez également exclure des objets BLOB à partir de l’opération de téléchargement hello en fonction de leur heure de dernière modification. Par exemple, si vous souhaitez que les objets BLOB de tooexclude dont heure de dernière modification est hello même ou plus récent que le fichier de destination hello, ajouter hello `/XN` option :

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

Ou si vous souhaitez que les objets BLOB de tooexclude dont heure de dernière modification est hello même ou antérieure à celle de fichier de destination hello, ajoutez hello `/XO` option :

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a>Objet blob : Téléchargement
### <a name="upload-single-file"></a>Télécharger un fichier unique

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

Si le conteneur de destination spécifié hello n’existe pas, AzCopy crée et téléchargements hello fichier dedans.

### <a name="upload-single-file-toovirtual-directory"></a>Téléchargement de fichier unique toovirtual Active

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

Si hello spécifié le répertoire virtuel n’existe pas, AzCopy télécharge hello fichier tooinclude hello répertoire virtuel dans son nom (*par exemple,*, `vd/abc.txt` dans l’exemple hello ci-dessus).

### <a name="upload-all-files"></a>Télécharger tous les fichiers

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

L’option `/S` contenu hello de téléchargements de hello spécifié directory tooBlob stockage de manière récursive, c'est-à-dire que tous les sous-dossiers et fichiers sont également téléchargés. Par exemple, supposons que suivant de hello fichiers résident dans le dossier `C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

Après l’opération de téléchargement de hello, conteneur de hello inclut hello fichiers suivants :

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

Si vous ne spécifiez pas l’option `/S`, AzCopy ne charge pas de manière récursive. Après l’opération de téléchargement de hello, conteneur de hello inclut hello fichiers suivants :

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a>Télécharger des fichiers correspondant au modèle spécifié

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

Supposons suivant de hello fichiers résident dans le dossier `C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

Après l’opération de téléchargement de hello, conteneur de hello inclut hello fichiers suivants :

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

Si vous ne spécifiez pas l’option `/S`, AzCopy télécharge uniquement les objets blob qui ne se trouvent pas dans un répertoire virtuel :

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a>Spécifiez le type de contenu MIME hello d’un objet blob de destination
Par défaut, AzCopy définit les type de contenu hello d’un objet blob de destination trop`application/octet-stream`. Depuis la version 3.1.0, vous pouvez spécifier explicitement le type de contenu hello via l’option de hello `/SetContentType:[content-type]`. Cette syntaxe définit le type de contenu hello pour tous les objets BLOB dans une opération de téléchargement.

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

Si vous spécifiez `/SetContentType` sans valeur, AzCopy définit chaque objet blob ou le type de contenu du fichier selon tooits extension de fichier.

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a>Objet blob : copie
### <a name="copy-single-blob-within-storage-account"></a>Copie d’un objet blob unique au sein d’un compte de stockage

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

Lorsque vous copiez un objet blob au sein d’un compte de stockage, une opération de [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) est exécutée.

### <a name="copy-single-blob-across-storage-accounts"></a>Copier un objet blob unique sur plusieurs comptes de stockage

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

Lorsque vous copiez un objet blob sur plusieurs comptes de stockage, une opération de [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) est exécutée.

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a>Copier un seul objet blob à partir de la région de tooprimary région secondaire

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

Notez que vous devez avoir un accès en lecture activé pour le stockage géo-redondant.

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a>Copier un objet blob unique et ses captures instantanées sur plusieurs comptes de stockage

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

Après l’opération de copie hello, conteneur cible de hello inclut les blob hello et ses instantanés. En supposant que blob hello dans l’exemple hello ci-dessus a deux instantanés, le conteneur de hello inclut des éléments suivants de hello blob et captures instantanées :

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a>Copier des objets blob de façon synchrone dans des comptes de stockage
AzCopy copie par défaut les données entre deux points de terminaison de stockage de façon asynchrone. Par conséquent, opération de copie hello s’exécute en arrière-plan hello à l’aide de la capacité de la bande passante de rechange avec aucun contrat SLA en termes de rapidité un objet blob est copié et AzCopy vérifie périodiquement le statut de la copie hello jusqu'à ce que la copie de hello est terminée ou a échoué.

Hello `/SyncCopy` option permet à opération de copie hello vitesse cohérente. AzCopy effectue la copie synchrone de hello en téléchargeant les objets BLOB de hello toocopy de hello spécifié source toolocal la mémoire et les télécharger la destination de stockage d’objets Blob toohello.

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

`/SyncCopy`peut générer une sortie supplémentaire coût comparés tooasynchronous copie, hello approche recommandée est toouse cette option dans une machine virtuelle Azure qui se trouve dans hello même région que votre coût sortie tooavoid de compte de stockage source.

## <a name="file-download"></a>Fichier : Téléchargement
### <a name="download-single-file"></a>Télécharger un fichier unique

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

Si hello spécifié source est un partage de fichiers Azure, vous devez spécifier soit le nom de fichier exact hello, (*par exemple,* `abc.txt`) toodownload un seul fichier, ou spécifiez l’option `/S` toodownload tous les fichiers dans le partage de hello récursive. Tentative de toospecify un modèle de fichier et l’option `/S` entraîne une erreur.

### <a name="download-all-files"></a>Charger tous les fichiers

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

Notez que les dossiers vides ne sont pas téléchargés.

## <a name="file-upload"></a>Fichier : Télécharger
### <a name="upload-single-file"></a>Télécharger un fichier unique

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a>Télécharger tous les fichiers

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

Notez que les dossiers vides ne sont pas chargés.

### <a name="upload-files-matching-specified-pattern"></a>Télécharger des fichiers correspondant au modèle spécifié

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a>Fichier : Copier
### <a name="copy-across-file-shares"></a>Copier d’un partage de fichier à l’autre

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
Lorsque vous copiez un fichier sur plusieurs partage de fichiers, une opération de [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) est exécutée.

### <a name="copy-from-file-share-tooblob"></a>Copier à partir de tooblob de partage de fichier

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
Lorsque vous copiez un fichier à partir du fichier partage tooblob, un [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) opération est effectuée.


### <a name="copy-from-blob-toofile-share"></a>Copier à partir du partage de toofile d’objets blob

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
Lorsque vous copiez un fichier à partir d’un partage toofile blob, une [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) opération est effectuée.

### <a name="synchronously-copy-files"></a>Copier les fichiers de façon synchrone
Vous pouvez spécifier hello `/SyncCopy` option toocopy des données à partir de tooFile de stockage de fichiers de stockage, de stockage de fichiers tooBlob stockage et de stockage d’objets Blob tooFile stockage de façon synchrone, AzCopy fait cela en téléchargeant mémoire toolocal hello source et le télécharger nouveau toodestination. Dans ce cas, des coûts de sortie standard s’appliquent.

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

Lors de la copie à partir du stockage de fichiers tooBlob stockage, type d’objet blob hello par défaut est l’objet blob de blocs, utilisateur peut spécifier l’option `/BlobType:page` type d’objet blob destination toochange hello.

Notez que `/SyncCopy` peut générer des sorties supplémentaires coût comparaison tooasynchronous copie, hello est recommandé de toouse cette option dans hello machine virtuelle Azure qui se trouve dans hello même région que votre coût sortie tooavoid de compte de stockage source.

## <a name="table-export"></a>Table : Exportation
### <a name="export-table"></a>Table d’exportation

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

AzCopy écrit un dossier de destination spécifié toohello fichier manifeste. fichier de manifeste Hello est utilisé dans les fichiers de données nécessaires du processus toolocate hello hello importation et effectuer la validation des données. fichier de manifeste Hello utilise hello suit la convention d’affectation de noms par défaut :

    <account name>_<table name>_<timestamp>.manifest

Utilisateur peut également spécifier hello option `/Manifest:<manifest file name>` nom du fichier manifeste tooset hello.

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a>Fractionnement de l’exportation en plusieurs fichiers

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

AzCopy utilise un *index de volume* Bonjour fractionner les données de noms de fichier toodistinguish plusieurs fichiers. index de volume Hello se compose de deux parties, un *index de plage de clés de partition* et un *fractionnement fichier index*. Ces deux index commencent à zéro.

index de plage de clés de partition Hello est 0 si l’utilisateur de hello ne spécifie pas d’option `/PKRS`.

Par exemple, supposons que AzCopy génère deux fichiers de données une fois que l’utilisateur de hello Spécifie l’option `/SplitSize`. Hello, ce qui entraîne des noms de fichiers de données peut être :

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

Notez que hello minimale possible pour l’option `/SplitSize` est 32 Mo. Si hello spécifié d’une destination de stockage d’objets Blob, AzCopy fractionne le fichier de données hello une fois que sa taille atteigne la limite de taille d’objet blob hello (200 Go), indépendamment de si l’option `/SplitSize` a été spécifié par l’utilisateur de hello.

### <a name="export-table-toojson-or-csv-data-file-format"></a>Exporter la table tooJSON ou format de fichier de données CSV
AzCopy par défaut exporte des fichiers de données de tables tooJSON. Vous pouvez spécifier hello option `/PayloadFormat:JSON|CSV` tooexport les tables de hello en tant que JSON ou CSV.

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

Lors de la spécification de format de charge utile hello CSV, AzCopy génère également un fichier de schéma avec l’extension de fichier `.schema.csv` pour chaque fichier de données.

### <a name="export-table-entities-concurrently"></a>Exportation simultanée d’entités de table

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

AzCopy démarre les entités tooexport opérations simultanées lors de l’utilisateur de hello Spécifie l’option `/PKRS`. Chaque opération exporte une plage de clés de partition.

Notez que hello nombre d’opérations simultanées est également contrôlé par l’option `/NC`. AzCopy utilise le nombre de hello de processeurs de base comme valeur par défaut hello `/NC` lors de la copie des entités de table, même si `/NC` n’a été spécifié. Lorsque les utilisateur hello spécifie option `/PKRS`, AzCopy utilise hello plus petit nombre hello deux valeurs - partition plages de clés par rapport aux opérations simultanées implicitement ou explicitement spécifiées - toodetermine hello de toostart des opérations simultanées. Pour plus d’informations, tapez `AzCopy /?:NC` à la ligne de commande hello.

### <a name="export-table-tooblob"></a>Exporter la table tooblob

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

AzCopy génère un fichier de données JSON dans un conteneur d’objets blob hello avec suivant la convention d’affectation de noms :

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

fichier de données JSON Hello généré suit le format de charge utile hello pour les métadonnées minimales. Pour des informations sur le format de charge utile, consultez la page [Format de charge utile pour les opérations du service de Table](http://msdn.microsoft.com/library/azure/dn535600.aspx).

Notez que lorsque vous exportez des tables tooblobs, AzCopy télécharge les fichiers de données temporaires hello Table entités toolocal et transmet ensuite les blob de toohello d’entités. Ces fichiers de données temporaires sont placés dans le dossier de fichier journal hello avec le chemin d’accès de hello par défaut «<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>», vous pouvez spécifier d’option/Z: [dossier de fichier journal] toochange hello d’emplacement de dossier du fichier journal et ainsi modifier emplacement de fichiers de données temporaires hello. Hello données temporaires de taille des fichiers est décidée par des entités de votre table taille et taille hello spécifiée avec hello option /SplitSize, bien que le fichier de données temporaire de hello au disque local est supprimé immédiatement une fois qu’il a été téléchargement toohello blob, vérifiez que vous disposez suffisamment local de disque espace toostore ces fichiers de données temporaire avant d’être supprimés.

## <a name="table-import"></a>Table : importation
### <a name="import-table"></a>Table d’importation

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

Hello option `/EntityOperation` indique la façon dont les entités tooinsert dans hello table. Les valeurs possibles sont les suivantes :

* `InsertOrSkip`: Ignore une entité existante ou insère une nouvelle entité si elle n’existe pas dans la table de hello.
* `InsertOrMerge`: Fusionne une entité existante ou insère une nouvelle entité si elle n’existe pas dans la table de hello.
* `InsertOrReplace`: Remplace une entité existante ou insère une nouvelle entité si elle n’existe pas dans la table de hello.

Notez que vous ne pouvez pas spécifier d’option `/PKRS` dans le scénario d’importation hello. Contrairement au scénario d’exportation hello, dans laquelle vous devez spécifier option `/PKRS` toostart des opérations simultanées, AzCopy démarre des opérations simultanées par défaut lorsque vous importez une table. nombre d’opérations simultanées démarré par défaut de Hello est nombre égal toohello de processeurs de base ; Toutefois, vous pouvez spécifier un nombre différent de simultanées avec l’option `/NC`. Pour plus d’informations, tapez `AzCopy /?:NC` à la ligne de commande hello.

Notez qu’AzCopy ne prend en charge que l’importation pour JSON, et non CSV. AzCopy ne prend pas en charge les importations de table à partir de fichiers JSON créés par l’utilisateur et de fichiers manifeste. Ces deux types de fichiers doivent provenir d’une exportation de table AzCopy. erreurs de tooavoid, ne modifiez pas hello exportée JSON ou un fichier manifeste.

### <a name="import-entities-tootable-using-blobs"></a>Importer les entités tootable à l’aide d’objets BLOB
Supposons qu’un conteneur d’objets Blob contient suivant de hello : fichier JSON d’un représentant une Table Azure et son fichier manifeste associé.

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

Vous pouvez exécuter hello suivant entités tooimport de commande dans une table à l’aide du fichier de manifeste hello dans ce conteneur d’objets blob :

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a>Autres fonctionnalités AzCopy
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a>Copier uniquement les données qui n’existent pas dans la destination de hello
Hello `/XO` et `/XN` paramètres vous permettent de tooexclude des ressources de source ancien ou plus récent à partir de la copie, respectivement. Si vous souhaitez uniquement les ressources de la source toocopy qui n’existent pas dans la destination de hello, vous pouvez spécifier les deux paramètres Bonjour AzCopy commande :

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

Notez que cela n'est pas pris en charge lorsque hello source ou destination est une table.

### <a name="use-a-response-file-toospecify-command-line-parameters"></a>Utiliser un paramètres de ligne de commande toospecify du fichier de réponse

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

Vous pouvez inclure n’importe quels paramètres de ligne de commande AzCopy dans un fichier réponse. AzCopy processus hello paramètres hello fichier comme s’ils avaient été spécifiés sur la ligne de commande hello, effectuer une substitution directe avec le contenu de hello du fichier de hello.

Supposons un fichier de réponse nommé `copyoperation.txt`, qui contient les lignes suivantes de hello. Chaque paramètre AzCopy peut être spécifié sur une seule ligne

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

ou sur des lignes distinctes :

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

AzCopy échoue si vous fractionnez le paramètre hello entre deux lignes, comme indiqué ici pour hello `/sourcekey` paramètre :

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-toospecify-command-line-parameters"></a>Utilisation de plusieurs paramètres de ligne de commande réponse fichiers toospecify
Si un fichier réponse dénommé `source.txt` qui spécifie un conteneur source :

    /Source:http://myaccount.blob.core.windows.net/mycontainer

Et un fichier de réponse nommé `dest.txt` qui spécifie un dossier de destination dans le système de fichiers hello :

    /Dest:C:\myfolder

Et un fichier réponse nommé `options.txt` qui spécifie les options pour AzCopy :

    /S /Y

toocall AzCopy de ces fichiers de réponse, qui se trouvent dans un répertoire `C:\responsefiles`, utilisez la commande :

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

AzCopy traite cette commande, comme il le ferait si vous avez inclus tous les paramètres individuels de hello sur la ligne de commande hello :

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a>Spécification d’une signature d’accès partagé (SAP)

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

Vous pouvez également spécifier une SAP sur l’URI du conteneur hello :

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a>Dossier du fichier journal
Chaque fois que vous exécutez une commande tooAzCopy, il vérifie si un fichier journal existe dans le dossier par défaut de hello, ou si elle existe dans un dossier que vous avez spécifié à l’aide de cette option. Si le fichier journal de hello n’existe pas à cet emplacement, AzCopy traite l’opération de hello en tant que nouvelle et génère un nouveau fichier journal.

Si le fichier journal de hello existe, AzCopy vérifie si la ligne de commande hello que vous avez entré correspond à ligne de commande hello dans un fichier de journal hello. Si les deux lignes de commande hello correspondent, AzCopy reprend les opérations d’incomplète hello. Si elles ne correspondent pas, vous êtes tooeither invité à remplacer hello journal fichier toostart une nouvelle opération ou toocancel hello opération en cours.

Si vous souhaitez toouse hello emplacement par défaut hello journal fichier :

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

Si vous omettez l’option `/Z`, ou spécifiez l’option `/Z` sans chemin d’accès du dossier hello, comme indiqué ci-dessus, AzCopy crée hello journal fichier dans l’emplacement par défaut hello, qui est `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`. Si le fichier journal de hello existe déjà, AzCopy reprend les opérations de hello basée sur le fichier journal de hello.

Si vous souhaitez toospecify un emplacement personnalisé pour le fichier journal de hello :

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

Cet exemple crée le fichier journal de hello si elle n’existe pas déjà. S’il n’existe pas, AzCopy reprend les opérations de hello basée sur le fichier journal de hello.

Si vous souhaitez tooresume une opération AzCopy :

```azcopy
AzCopy /Z:C:\journalfolder\
```

Cet exemple reprend hello dernière opération, ce qui peut avoir échoué toocomplete.

### <a name="generate-a-log-file"></a>Génération d’un fichier journal

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

Si vous spécifiez l’option `/V` sans fournir un journal détaillé de fichier chemin d’accès toohello, puis AzCopy crée hello fichier journal dans l’emplacement par défaut hello, qui est `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.

Autrement, vous pouvez créer un fichier journal dans un emplacement personnalisé :

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

Notez que si vous spécifiez un chemin d’accès relatif suivant option `/V`, tel que `/V:test/azcopy1.log`, la journalisation documentée hello est alors créé dans le répertoire de travail actuel hello dans un sous-dossier nommé `test`.

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a>Spécifiez le nombre hello d’opérations simultanées toostart
Option `/NC` Spécifie le nombre de hello d’opérations de copie simultanées. Par défaut, AzCopy démarre un certain nombre de débit de transfert de données des opérations simultanées tooincrease hello. Pour les opérations de Table, nombre hello d’opérations simultanées est nombre égal toohello de processeurs que vous avez. Pour les opérations Blob et de fichier, nombre hello d’opérations simultanées est égal à nombre de hello de 8 heures de processeurs que vous avez. Si vous exécutez AzCopy sur un réseau à faible bande passante, vous pouvez spécifier une valeur inférieure pour le paramètre/NC tooavoid a échoué en concurrence de la ressource.

### <a name="run-azcopy-against-azure-storage-emulator"></a>Exécutez AzCopy sur l’émulateur de stockage Azure
Vous pouvez exécuter AzCopy pour hello [émulateur de stockage Azure](storage-use-emulator.md) pour les objets BLOB :

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

et les tables :

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a>Paramètres AzCopy
Les paramètres d’AzCopy sont décrits ci-dessous. Vous pouvez également taper une des hello suivant les commandes à partir de la ligne de commande hello pour vous aider à l’aide de AzCopy :

* Pour l'aide détaillée sur la ligne de commande AzCopy : `AzCopy /?`
* Pour l'aide détaillée sur un paramètre AzCopy : `AzCopy /?:SourceKey`
* Pour des exemples de ligne de commande : `AzCopy /?:Samples`

### <a name="sourcesource"></a>/Source:"source"
Spécifie les données de source de hello à partir de quels toocopy. Hello source peut être un répertoire de système de fichiers, un conteneur d’objets blob, un répertoire virtuel d’objets blob, un partage de fichiers de stockage, un répertoire de fichiers de stockage ou une table Azure.

**S’applique à :** objets blob, fichiers, tables

### <a name="destdestination"></a>/Dest:"destination"
Spécifie les toocopy de destination hello pour. Hello destination peut être un répertoire de système de fichiers, un conteneur d’objets blob, un répertoire virtuel d’objets blob, un partage de fichiers de stockage, un répertoire de fichiers de stockage ou une table Azure.

**S’applique à :** objets blob, fichiers, tables

### <a name="patternfile-pattern"></a>/Pattern:"file-pattern"
Spécifie un modèle de fichier qui indique quel toocopy de fichiers. comportement de Hello du paramètre de /Pattern hello est déterminé par emplacement hello de source de données hello et présence hello de l’option de mode hello récursive. Le mode récursif est spécifié via l’option /S.

Si la source spécifiée de hello est un répertoire dans le système de fichiers hello, des caractères génériques standard sont en vigueur et le modèle de fichier hello fourni est mis en correspondance avec les fichiers dans le répertoire de hello. Si l’option que /s est spécifié, puis AzCopy correspond également à modèle spécifié de hello sur tous les fichiers dans les sous-dossiers sous le répertoire de hello.

Si la source spécifiée de hello est un conteneur d’objets blob ou le répertoire virtuel, les caractères génériques ne sont pas appliquées. Si l’option que /s est spécifié, puis AzCopy interprète un modèle de fichier spécifié hello comme un préfixe d’objet blob. Si l’option que /s n’est pas spécifié, puis AzCopy correspond au modèle de fichier de hello par rapport aux noms d’objets blob exacte.

Si hello spécifié source est un partage de fichiers Azure, vous devez spécifier soit le nom de fichier exact hello, (par exemple, abc.txt) toocopy un seul fichier, ou spécifiez option /S toocopy tous les fichiers dans le partage de hello de manière récursive. Tentative de toospecify à la fois un fichier modèle et option /S entraîne une erreur.

AzCopy utilise la correspondance qui respecte la casse lorsque hello/source est un conteneur d’objets blob ou le répertoire virtuel d’objets blob, et utilise la casse dans toutes les hello autres cas.

Hello modèle de fichier par défaut utilisé lorsqu’aucun modèle de fichier n’est spécifié est *.* pour un emplacement de système de fichiers, ou un préfixe vide pour un emplacement Azure Storage. La spécification de plusieurs modèles de fichiers n’est pas prise en charge.

**S’applique à :** objets blob, fichiers

### <a name="destkeystorage-key"></a>/DestKey:"storage-key"
Spécifie la clé de compte de stockage hello pour la ressource de destination hello.

**S’applique à :** objets blob, fichiers, tables

### <a name="destsassas-token"></a>/DestSAS:"sas-token"
Spécifie une Signature d’accès partagé (SAS) avec des autorisations de lecture et d’écriture pour la destination de hello (le cas échéant). Hello surround SAS de doubles guillemets, telle qu’elle peut contient des caractères spéciaux de ligne de commande.

Si la ressource de destination hello est un conteneur d’objets blob, partage de fichiers ou une table, vous pouvez spécifier cette option de suivi d’un jeton SAS hello, ou vous pouvez spécifier hello SAP en tant que partie du conteneur d’objets blob de destination de hello, partage de fichiers ou un URI de la table, sans cette option.

Si hello source et destination sont les deux objets BLOB, objet blob de destination hello doit résider dans hello même compte de stockage en tant qu’objet blob source de hello.

**S’applique à :** objets blob, fichiers, tables

### <a name="sourcekeystorage-key"></a>/SourceKey:"storage-key"
Spécifie la clé de compte de stockage hello pour la ressource de source de hello.

**S’applique à :** objets blob, fichiers, tables

### <a name="sourcesassas-token"></a>/SourceSAS:"sas-token"
Spécifie une Signature d’accès partagé avec les autorisations de lecture et de la liste pour la source de hello (le cas échéant). Hello surround SAS de doubles guillemets, telle qu’elle peut contient des caractères spéciaux de ligne de commande.

Si la ressource de source de hello est un conteneur d’objets blob, et une clé, ni une SAP est fournie, conteneur d’objets blob hello est en lecture via l’accès anonyme.

Si la source de hello est un partage de fichiers ou une table, une clé ou une SAP doit être fournie.

**S’applique à :** objets blob, fichiers, tables

### <a name="s"></a>/S
Spécifie le mode récursif pour les opérations de copie. En mode de récursive, AzCopy copie tous les objets BLOB ou les fichiers qui correspondent au modèle de fichier spécifié hello, y compris celles figurant dans les sous-dossiers.

**S’applique à :** objets blob, fichiers

### <a name="blobtypeblock--page--append"></a>/BlobType:"block" | "page" | "append"
Spécifie si l’objet blob de destination hello est un objet blob de blocs, un objet blob de pages ou un objet blob d’ajout. Cette option s’applique uniquement lorsque vous téléchargez un objet blob. Sinon, une erreur se produit. Si la destination de hello est un objet blob et que cette option n’est pas spécifiée, par défaut, AzCopy crée un objet blob de blocs.

**S’applique à :** objets blob

### <a name="checkmd5"></a>/CheckMD5
Calcule un hachage MD5 pour les données téléchargées et vérifie que hachage MD5 de hello stockées dans l’objet blob de hello ou propriété de Content-MD5 du fichier correspond au hachage de hello calculée. vérification de Hello MD5 est désactivée par défaut, vous devez spécifier cette vérification de MD5 option tooperform hello lors du téléchargement de données.

Notez que le stockage Azure ne garantit pas que hello hachage MD5 stockée pour l’objet blob de hello ou le fichier est à jour. Il est hello tooupdate de responsabilité du client MD5 chaque fois que l’objet blob de hello ou un fichier est modifié.

AzCopy affecte hello Content-MD5 propriété pour un objet blob Azure ou le fichier après son téléchargement toohello service.  

**S’applique à :** objets blob, fichiers

### <a name="snapshot"></a>/Snapshot
Indique si les instantanés tootransfer. Cette option est valide uniquement lorsque la source de hello est un objet blob.

instantanés d’objet blob transférées Hello sont renommés dans ce format : nom d’objet blob (instantané-time) .extension

Par défaut, les captures instantanées ne sont pas copiées.

**S’applique à :** objets blob

### <a name="vverbose-log-file"></a>/V:[verbose-log-file]
Stocke les messages de statut détaillés dans un fichier journal.

Par défaut, fichier journal détaillé de hello est nommé AzCopyVerbose.log dans `%LocalAppData%\Microsoft\Azure\AzCopy`. Si vous spécifiez un emplacement du fichier existant pour cette option, la journalisation documentée hello est ajouté toothat fichier.  

**S’applique à :** objets blob, fichiers, tables

### <a name="zjournal-file-folder"></a>/Z:[journal-file-folder]
Spécifie un dossier de fichier journal pour reprendre une opération.

AzCopy peut toujours reprendre une opération qui a été interrompue.

Si cette option n’est pas spécifiée ou il est spécifié sans un chemin d’accès du dossier, AzCopy crée de fichier journal de hello dans l’emplacement par défaut hello, qui est % LocalAppData%\Microsoft\Azure\AzCopy.

Chaque fois que vous exécutez une commande tooAzCopy, il vérifie si un fichier journal existe dans le dossier par défaut de hello, ou si elle existe dans un dossier que vous avez spécifié à l’aide de cette option. Si le fichier journal de hello n’existe pas à cet emplacement, AzCopy traite l’opération de hello en tant que nouvelle et génère un nouveau fichier journal.

Si le fichier journal de hello existe, AzCopy vérifie si la ligne de commande hello que vous avez entré correspond à ligne de commande hello dans un fichier de journal hello. Si les deux lignes de commande hello correspondent, AzCopy reprend les opérations d’incomplète hello. Si elles ne correspondent pas, vous êtes tooeither invité à remplacer hello journal fichier toostart une nouvelle opération ou toocancel hello opération en cours.

fichier de journal Hello est supprimé en cas de réussite de l’opération de hello.

Remarque : reprendre une opération à partir d’un fichier journal créé par une version précédente d’AzCopy n’est pas pris en charge.

**S’applique à :** objets blob, fichiers, tables

### <a name="parameter-file"></a>/@:"parameter-file"
Spécifie un fichier qui contient des paramètres. AzCopy processus hello paramètres hello fichier comme s’ils avaient été spécifiés sur la ligne de commande hello.

Dans un fichier réponse, vous pouvez soit spécifier de multiples paramètres sur une seule ligne, soit spécifier chaque paramètre sur sa propre ligne. Remarque : un paramètre individuel ne peut pas couvrir plusieurs lignes.

Fichiers réponse peuvent inclure des lignes de commentaires qui commencent par le symbole « # » hello.

Vous pouvez spécifier plusieurs fichiers réponse. Toutefois, AzCopy ne prend pas en charge les fichiers réponse imbriqués.

**S’applique à :** objets blob, fichiers, tables

### <a name="y"></a>/Y
Supprime toutes les invites de confirmation d’AzCopy.

**S’applique à :** objets blob, fichiers, tables

### <a name="l"></a>/L
Spécifie une opération de listing uniquement : aucune donnée n’est copiée.

AzCopy interprète hello à l’aide de cette option comme une simulation de ligne de commande hello en cours d’exécution sans cette option/l et le nombre d’objets est copié, vous pouvez spécifier des nombres option /V au même moment toocheck quels objets sont copiés dans le journal détaillé de hello de hello.

Hello comportement de cette option est également déterminé par emplacement hello de source de données hello et de la présence de hello hello récursive mode option /S et le fichier de modèle de l’option de /Pattern.

AzCopy nécessite les autorisations de listing et de lecture sur cet emplacement source quand cette option est utilisée.

**S’applique à :** objets blob, fichiers

### <a name="mt"></a>/MT
Définit l’heure de dernière modification du fichier téléchargé hello toobe même hello en tant qu’objet blob source de hello ou du fichier.

**S’applique à :** objets blob, fichiers

### <a name="xn"></a>/XN
Exclut une ressource de source plus récente. Hello ressource n’est pas été copiée si l’heure de dernière modification de la source de hello hello est hello identique ou ultérieure à la destination.

**S’applique à :** objets blob, fichiers

### <a name="xo"></a>/XO
Exclut une ressource de source plus ancienne. Hello ressource n’est pas été copiée si l’heure de dernière modification de la source de hello hello est hello même ou antérieure à celle de destination.

**S’applique à :** objets blob, fichiers

### <a name="a"></a>/A
Télécharge uniquement les fichiers qui ont attribut hello.

**S’applique à :** objets blob, fichiers

### <a name="iarashcnetoi"></a>/IA:[RASHCNETOI]
Téléchargements uniquement les fichiers ayant une des hello spécifié ensemble d’attributs.

Les attributs disponibles incluent :

* R = Fichiers en lecture seule
* A = Fichiers prêts à être archivés
* S = Fichiers système
* H = Fichiers masqués
* C = Fichiers compressés
* N = Fichiers normaux
* E = Fichiers cryptés
* T = Fichiers temporaires
* O = Fichiers hors ligne
* I = Fichiers non indexés

**S’applique à :** objets blob, fichiers

### <a name="xarashcnetoi"></a>/XA:[RASHCNETOI]
Exclut les fichiers qui ont des hello spécifié jeu d’attributs.

Les attributs disponibles incluent :

* R = Fichiers en lecture seule
* A = Fichiers prêts à être archivés
* S = Fichiers système
* H = Fichiers masqués
* C = Fichiers compressés
* N = Fichiers normaux
* E = Fichiers cryptés
* T = Fichiers temporaires
* O = Fichiers hors ligne
* I = Fichiers non indexés

**S’applique à :** objets blob, fichiers

### <a name="delimiterdelimiter"></a>/Delimiter:"délimiteur"
Indique le délimiteur hello utilisé toodelimit des répertoires virtuels dans un nom d’objet blob.

Par défaut, AzCopy utilise / en tant que caractère de délimiteur hello. Toutefois, AzCopy prend en charge n’importe quel caractère commun (tel que @, #, ou %) comme délimiteur. Si vous devez tooinclude un de ces caractères spéciaux sur la ligne de commande hello, placez le nom de fichier hello avec des guillemets doubles.

Cette option est applicable uniquement au téléchargement d’objets blob.

**S’applique à :** objets blob

### <a name="ncnumber-of-concurrent-operations"></a>/NC:"nombre-d’opérations-simultanées"
Spécifie le nombre de hello d’opérations simultanées.

AzCopy par défaut démarre un certain nombre de débit de transfert de données des opérations simultanées tooincrease hello. Notez que le grand nombre d’opérations simultanées dans un environnement à faible bande passante peut surcharger la connexion de réseau hello et empêcher complètement exécution des opérations hello. Limitez les opérations simultanées en fonction de la bande passante de réseau qui est disponible.

limite supérieure de Hello pour les opérations simultanées est 512.

**S’applique à :** objets blob, fichiers, tables

### <a name="sourcetypeblob--table"></a>/SourceType:"Blob" | "Table"
Spécifie que hello `source` ressource est un objet blob disponible dans l’environnement de développement local hello, en cours d’exécution dans l’émulateur de stockage hello.

**S’applique à :** objets blob, tables

### <a name="desttypeblob--table"></a>/DestType:"Blob" | "Table"
Spécifie que hello `destination` ressource est un objet blob disponible dans l’environnement de développement local hello, en cours d’exécution dans l’émulateur de stockage hello.

**S’applique à :** objets blob, tables

### <a name="pkrskey1key2key3"></a>/PKRS:"key1#key2#key3#..."
Fractionnements hello tooenable de plage de clés de partition exportation de données de table en parallèle, ce qui augmente la vitesse de l’opération d’exportation hello hello.

Si cette option n’est pas spécifiée, AzCopy utilise des entités de table tooexport un thread unique. Par exemple, si hello utilisateur spécifie /PKRS : « aa #bb », puis AzCopy démarre trois opérations simultanées.

Chaque opération exporte une des trois plages de clés de partition (voir ci-dessous) :

  [first-partition-key, aa)

  [aa, bb)

  [bb, dernière-clé-de-partition]

**S’applique à :** tables

### <a name="splitsizefile-size"></a>/SplitSize:"file-size"
Spécifie hello fichier exporté fractionner la taille en Mo, hello de valeur minimale autorisée est de 32.

Si cette option n’est pas spécifiée, AzCopy exporte tooa de données de table de fichier unique.

Si les données de la table hello sont exporté tooa blob et limite de 200 Go hello pour la taille des objets blob atteint hello taille du fichier exporté, AzCopy fractionne le fichier exporté hello, même si cette option n’est pas spécifiée.

**S’applique à :** tables

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a>/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"
Spécifie le comportement d’importation hello table données.

* InsertOrSkip - ignore une entité existante ou insère une nouvelle entité si elle n’existe pas dans la table de hello.
* InsertOrMerge - fusionne une entité existante ou insère une nouvelle entité si elle n’existe pas dans la table de hello.
* InsertOrReplace - remplace une entité existante ou insère une nouvelle entité si elle n’existe pas dans la table de hello.

**S’applique à :** tables

### <a name="manifestmanifest-file"></a>/Manifest:"manifest-file"
Spécifie le fichier de manifeste hello pour la table de hello d’exportation et l’opération d’importation.

Cette option est facultative lors de l’opération d’exportation hello, AzCopy génère un fichier manifeste avec le nom prédéfini si cette option n’est pas spécifiée.

Cette option est requise pendant l’opération d’importation hello pour localiser les fichiers de données hello.

**S’applique à :** tables

### <a name="synccopy"></a>/SyncCopy
Indique si toosynchronously copier des objets BLOB ou des fichiers entre deux points de terminaison de stockage Azure.

AzCopy utilise par défaut la copie asynchrone du côté serveur. Spécifiez cette option tooperform synchrone copier, qui télécharge les objets BLOB ou fichiers toolocal mémoire et les charge tooAzure stockage.

Vous pouvez utiliser cette option pour copier les fichiers dans le stockage d’objets Blob, dans le stockage de fichiers ou à partir de l’objet Blob stockage tooFile stockage et inversement.

**S’applique à :** objets blob, fichiers

### <a name="setcontenttypecontent-type"></a>/SetContentType:"content-type"
Spécifie le type de contenu MIME hello pour les fichiers ou les objets BLOB de destination.

Jeux de AzCopy hello du type de contenu d’un objet blob ou de fichiers tooapplication/octet-stream par défaut. Vous pouvez définir le type de contenu hello pour tous les objets BLOB ou les fichiers en spécifiant explicitement une valeur pour cette option.

Si vous spécifiez cette option sans valeur, AzCopy définit chaque objet blob ou le type de contenu du fichier selon tooits extension de fichier.

**S’applique à :** objets blob, fichiers

### <a name="payloadformatjson--csv"></a>/PayloadFormat:"JSON" | "CSV"
Spécifie le format hello hello table exportée du fichier de données.

Si cette option n’est pas spécifiée, AzCopy exporte le fichier de données de table au format JSON par défaut.

**S’applique à :** tables

## <a name="known-issues-and-best-practices"></a>Problèmes connus et les meilleures pratiques
### <a name="limit-concurrent-writes-while-copying-data"></a>Limitation des écritures simultanées lors de la copie des données
Lorsque vous copiez des objets BLOB ou fichiers avec AzCopy, gardez à l’esprit qu’une autre application peut être modification des données de hello pendant que vous effectuez la copie. Si possible, assurez-vous que vous copiez les données de salutation ne sont pas modifiées pendant l’opération de copie hello. Par exemple, lors de la copie d’un disque dur virtuel associé à une machine virtuelle Azure, assurez-vous qu’aucune autre application n’écrivez actuellement toohello disque dur virtuel. Un bon moyen toodo qu'est en louant hello ressource toobe copié. Ou bien, vous pouvez créez d’abord un instantané de hello disque dur virtuel, puis copiez instantané d’hello.

Si vous ne pouvez pas empêcher les autres applications à partir de l’écriture de tooblobs ou des fichiers pendant qu’ils sont copiés, puis que vous n’oubliez pas que par hello temps hello tâche se termine, hello ressources copiées peuvent ne plus avoir parité complète avec les ressources de la source hello.

### <a name="run-one-azcopy-instance-on-one-machine"></a>Exécuter une instance de AzCopy sur un même ordinateur.
AzCopy est l’utilisation de hello toomaximize conçu votre ordinateur ressource tooaccelerate hello de transfert de données, nous vous recommandons exécutez qu’une seule instance AzCopy sur un ordinateur et spécifiez l’option de hello `/NC` si vous avez besoin d’opérations simultanées plus. Pour plus d’informations, tapez `AzCopy /?:NC` à la ligne de commande hello.

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a>Activer les algorithmes MD5 compatibles FIPS pour AzCopy quand vous « utilisez des algorithmes compatibles FIPS pour le chiffrement, le hachage et la signature ».
AzCopy par défaut utilise toocalculate hello MD5 de MD5 .NET implémentation lors de la copie des objets, mais il existe certaines exigences de sécurité nécessitant le paramètre de MD5 conforme AzCopy tooenable FIPS.

Vous pouvez créer un fichier app.config `AzCopy.exe.config` avec la propriété `AzureStorageUseV1MD5` et le mettre à part avec AzCopy.exe.

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

Pour la propriété « AzureStorageUseV1MD5 » • True : hello par défaut, AzCopy utilise implémentation .NET MD5.
Si elle a pour valeur false, AzCopy utilise l’algorithme MD5 compatible FIPS.

Notez que les algorithmes compatibles FIPS sont désactivés par défaut sur votre ordinateur Windows ; vous pouvez taper secpol.msc dans la fenêtre Exécuter et activer le commutateur « Chiffrement système : utilisez des algorithmes compatibles FIPS pour le chiffrement, le hachage et la signature » (Paramètres de sécurité -> Stratégies locales -> Options de sécurité).

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur le stockage Azure et AzCopy, consultez hello suivant des ressources :

### <a name="azure-storage-documentation"></a>Documentation d’Azure Storage :
* [Introduction tooAzure stockage](../storage-introduction.md)
* [Comment toouse stockage d’objets Blob à partir de .NET](../blobs/storage-dotnet-how-to-use-blobs.md)
* [Comment toouse stockage de fichiers à partir de .NET](../storage-dotnet-how-to-use-files.md)
* [Comment toouse le stockage de Table à partir de .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Comment toocreate, gérer ou supprimer un compte de stockage](../storage-create-storage-account.md)
* [Transférer des données avec AzCopy sur Linux](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a>Billets de blog Azure Storage :
* [Présentation de la bibliothèque de déplacement des données dans Azure Storage en version préliminaire](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy : Présentation de la copie synchrone et du type de contenu personnalisé](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [AzCopy : Annonce de la disponibilité générale d'AzCopy 3.0 plus version préliminaire d'AzCopy 4.0 avec prise en charge de fichier et de table](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [AzCopy : Optimisation pour les scénarios de copie à grande échelle](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy : Prise en charge des comptes de stockage géo-redondants avec accès en lecture](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [AzCopy : Transfert des données avec mode reprise et jeton SAP](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [AzCopy : Utilisation de copie d'objets blob sur plusieurs comptes](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [AzCopy : Chargement/téléchargement des fichiers pour les objets blob Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

