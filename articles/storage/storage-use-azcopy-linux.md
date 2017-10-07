---
title: "tooAzure de données aaaCopy ou déplacer le stockage avec AzCopy sur Linux | Documents Microsoft"
description: "Utilisez hello AzCopy sur Linux utilitaire toomove ou copie de données tooor à partir de l’objet blob et le fichier de contenu. Copier des données tooAzure stockage à partir de fichiers locales, ou copier des données dans ou entre des comptes de stockage. Migrer facilement vos données de tooAzure stockage."
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
ms.date: 05/11/2017
ms.author: seguler
ms.openlocfilehash: dccb03c9e8cc3ea661494e7834f307b0e3e30cb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a>Transférer des données avec AzCopy sur Linux
AzCopy sur Linux est un utilitaire de ligne de commande conçu pour la copie des données tooand à partir du stockage d’objets Blob Microsoft Azure et de fichier à l’aide de commandes simples avec des performances optimales. Vous pouvez copier des données à partir d’un objet tooanother dans votre compte de stockage, ou entre des comptes de stockage.

Il existe deux versions d’AzCopy que vous pouvez télécharger. AzCopy sur Linux est intégré à .NET Core Framework, qui cible les plateformes Linux en offrant des options en ligne de commande de style POSIX. [AzCopy sur Windows](storage-use-azcopy.md) est intégré à .NET Framework et offre des options en ligne de commande de style Windows. Cet article est consacré à AzCopy sur Linux.

## <a name="download-and-install-azcopy"></a>Téléchargement et installation d’AzCopy
### <a name="installation-on-linux"></a>Installation sur Linux

AzCopy sur Linux nécessite le framework .NET Core sur la plateforme de hello. Consultez les instructions d’installation de hello sur hello [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) page.

Par exemple, nous allons installer .NET Core sur Ubuntu 16.10. Guide d’installation hello plus récente, visitez [.NET Core sur Linux](https://www.microsoft.com/net/core#linuxubuntu) page d’installation.


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

Une fois que vous avez installé .NET Core, téléchargez et installez AzCopy.

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

Vous pouvez supprimer des fichiers de hello extrait une fois AzCopy sur Linux est installé. Vous pouvez également si vous n’avez pas de privilèges de superutilisateur, vous pouvez également exécuter AzCopy à l’aide du script de shell hello 'azcopy' dans le dossier d’extraction hello. 

### <a name="alternative-installation-on-ubuntu"></a>Installation alternative sur Ubuntu

**Ubuntu 14.04**

Ajoutez une source apt pour .Net Core :

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Ajoutez une source apt pour le référentiel de produit Microsoft Linux et installez AzCopy :

```bash
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

**Ubuntu 16.04**

Ajoutez une source apt pour .Net Core :

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Ajoutez une source apt pour le référentiel de produit Microsoft Linux et installez AzCopy :

```bash
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

**Ubuntu 16.10**

Ajoutez une source apt pour .Net Core :

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Ajoutez une source apt pour le référentiel de produit Microsoft Linux et installez AzCopy :

```bash
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

## <a name="writing-your-first-azcopy-command"></a>Écriture de votre première commande AzCopy
syntaxe de base Hello pour les commandes AzCopy est la suivante :

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

Hello suivant exemples illustrent divers scénarios pour la copie des données tooand à partir de fichiers et les objets BLOB Microsoft Azure. Consultez toohello `azcopy --help` menu pour une explication détaillée des paramètres hello utilisées dans chaque exemple.

## <a name="blob-download"></a>Blob : Téléchargement
### <a name="download-single-blob"></a>Télécharger un seul objet blob

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Si le dossier de hello `/mnt/myfiles` n’existe pas, AzCopy crée et télécharge `abc.txt ` dans le dossier hello.

### <a name="download-single-blob-from-secondary-region"></a>Télécharger un objet blob unique depuis la région secondaire

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Notez que vous devez avoir un accès en lecture activé pour le stockage géo-redondant.

### <a name="download-all-blobs"></a>Télécharger tous les objets blob

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

Supposons suivant de hello BLOB réside dans le conteneur spécifié de hello :  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

Après l’opération de téléchargement hello hello active `/mnt/myfiles` inclut hello fichiers suivants :

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

Si vous ne spécifiez pas l’option `--recursive`, aucun blob ne sera téléchargé.

### <a name="download-blobs-with-specified-prefix"></a>Téléchargement d’objets blob avec le préfixe spécifié

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

Supposons suivant de hello BLOB réside dans le conteneur spécifié de hello. Tous les objets BLOB commençant par préfixe de hello `a` sont téléchargées.

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

Après l’opération de téléchargement hello hello dossier `/mnt/myfiles` inclut hello fichiers suivants :

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

préfixe de Hello applique le répertoire virtuel toohello, ce qui constitue hello première partie du nom d’objet blob hello. Exemple hello ci-dessus, répertoire virtuel de hello ne correspond pas au préfixe spécifié de hello, donc aucun objet blob n’est téléchargé. En outre, si hello option `--recursive` n’est pas spécifié, AzCopy ne télécharge pas les objets BLOB.

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a>Définir l’heure de dernière modification de hello de fichiers exportés toobe identique hello d’objets BLOB sources

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

Vous pouvez également exclure des objets BLOB à partir de l’opération de téléchargement hello en fonction de leur heure de dernière modification. Par exemple, si vous souhaitez que les objets BLOB de tooexclude dont heure de dernière modification est hello même ou plus récent que le fichier de destination hello, ajouter hello `--exclude-newer` option :

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

Ou si vous souhaitez que les objets BLOB de tooexclude dont heure de dernière modification est hello même ou antérieure à celle de fichier de destination hello, ajoutez hello `--exclude-older` option :

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a>Objet blob : Téléchargement
### <a name="upload-single-file"></a>Télécharger un fichier unique

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

Si le conteneur de destination spécifié hello n’existe pas, AzCopy crée et téléchargements hello fichier dedans.

### <a name="upload-single-file-toovirtual-directory"></a>Téléchargement de fichier unique toovirtual Active

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

Si hello spécifié le répertoire virtuel n’existe pas, AzCopy télécharge hello fichier tooinclude hello répertoire virtuel dans le nom d’objet blob hello (*par exemple,*, `vd/abc.txt` dans l’exemple hello ci-dessus).

### <a name="upload-all-files"></a>Télécharger tous les fichiers

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

L’option `--recursive` contenu hello de téléchargements de hello spécifié directory tooBlob stockage de manière récursive, c'est-à-dire que tous les sous-dossiers et fichiers sont également téléchargés. Par exemple, supposons que suivant de hello fichiers résident dans le dossier `/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

Après l’opération de téléchargement de hello, conteneur de hello inclut hello fichiers suivants :

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

Lorsque hello option `--recursive` n’est pas spécifié, seul hello trois fichiers suivants sont téléchargés :

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a>Télécharger des fichiers correspondant au modèle spécifié

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

Supposons suivant de hello fichiers résident dans le dossier `/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

Après l’opération de téléchargement de hello, conteneur de hello inclut hello fichiers suivants :

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

Lorsque hello option `--recursive` n’est pas spécifié, AzCopy ignore les fichiers qui se trouvent dans les sous-répertoires :

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a>Spécifiez le type de contenu MIME hello d’un objet blob de destination
Par défaut, AzCopy définit les type de contenu hello d’un objet blob de destination trop`application/octet-stream`. Toutefois, vous pouvez spécifier explicitement le type de contenu hello via l’option de hello `--set-content-type [content-type]`. Cette syntaxe définit le type de contenu hello pour tous les objets BLOB dans une opération de téléchargement.

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

Si hello option `--set-content-type` est spécifié sans valeur, puis AzCopy définit chaque objet blob ou le fichier du type de contenu en fonction de tooits extension de fichier.

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a>Objet blob : copie
### <a name="copy-single-blob-within-storage-account"></a>Copie d’un objet blob unique au sein d’un compte de stockage

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

Lorsque vous copiez un blob sans l’option --sync-copy, une opération de [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) est exécutée.

### <a name="copy-single-blob-across-storage-accounts"></a>Copier un objet blob unique sur plusieurs comptes de stockage

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

Lorsque vous copiez un blob sans l’option --sync-copy, une opération de [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) est exécutée.

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a>Copier un seul objet blob à partir de la région de tooprimary région secondaire

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

Notez que vous devez avoir un accès en lecture activé pour le stockage géo-redondant.

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a>Copier un objet blob unique et ses captures instantanées sur plusieurs comptes de stockage

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

Après l’opération de copie hello, conteneur cible de hello inclut les blob hello et ses instantanés. conteneur Hello inclut suivant de hello blob et ses instantanés :

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a>Copier des objets blob de façon synchrone dans des comptes de stockage
AzCopy copie par défaut les données entre deux points de terminaison de stockage de façon asynchrone. Par conséquent, opération de copie hello s’exécute en arrière-plan hello à l’aide de la capacité de la bande passante de rechange avec aucun contrat SLA en termes de rapidité un objet blob est copié. 

Hello `--sync-copy` option permet à opération de copie hello vitesse cohérente. AzCopy effectue la copie synchrone de hello en téléchargeant les objets BLOB de hello toocopy de hello spécifié source toolocal la mémoire et les télécharger la destination de stockage d’objets Blob toohello.

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

`--sync-copy`peut générer une copie de tooasynchronous de coût par rapport de sortie supplémentaires. Hello approche recommandée est toouse cette option dans une machine virtuelle Azure, qui se trouve dans hello même région que votre coût sortie tooavoid de compte de stockage source.

## <a name="file-download"></a>Fichier : Téléchargement
### <a name="download-single-file"></a>Télécharger un fichier unique

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Si hello spécifié source est un partage de fichiers Azure, vous devez spécifier soit le nom de fichier exact hello, (*par exemple,* `abc.txt`) toodownload un seul fichier, ou spécifiez l’option `--recursive` toodownload tous les fichiers dans le partage de hello récursive. Tentative de toospecify un modèle de fichier et l’option `--recursive` entraîne une erreur.

### <a name="download-all-files"></a>Charger tous les fichiers

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

Notez que les dossiers vides ne sont pas téléchargés.

## <a name="file-upload"></a>Fichier : Télécharger
### <a name="upload-single-file"></a>Télécharger un fichier unique

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a>Télécharger tous les fichiers

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

Notez que les dossiers vides ne sont pas chargés.

### <a name="upload-files-matching-specified-pattern"></a>Télécharger des fichiers correspondant au modèle spécifié

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a>Fichier : Copier
### <a name="copy-across-file-shares"></a>Copier d’un partage de fichier à l’autre

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Lorsque vous copiez un fichier sur plusieurs partage de fichiers, une opération de [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) est exécutée.

### <a name="copy-from-file-share-tooblob"></a>Copier à partir de tooblob de partage de fichier

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Lorsque vous copiez un fichier à partir du fichier partage tooblob, un [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) opération est effectuée.

### <a name="copy-from-blob-toofile-share"></a>Copier à partir du partage de toofile d’objets blob

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Lorsque vous copiez un fichier à partir d’un partage toofile blob, une [copie côté serveur](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) opération est effectuée.

### <a name="synchronously-copy-files"></a>Copier les fichiers de façon synchrone
Vous pouvez spécifier hello `--sync-copy` option toocopy des données à partir du stockage de fichiers tooFile stockage, à partir du stockage de fichiers tooBlob stockage et de stockage d’objets Blob tooFile stockage de façon synchrone. AzCopy exécute cette opération en téléchargeant les données toolocal mémoire hello source et en téléchargeant toodestination. Dans ce cas, des coûts de sortie standard s’appliquent.

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

Lors de la copie à partir du stockage de fichiers tooBlob stockage, type d’objet blob hello par défaut est l’objet blob de blocs, utilisateur peut spécifier l’option `/BlobType:page` type d’objet blob destination toochange hello.

Notez que `--sync-copy` risque de générer des sorties supplémentaires comparaison tooasynchronous copie de coût. Hello approche recommandée est toouse cette option dans une machine virtuelle Azure, qui se trouve dans hello même région que votre coût sortie tooavoid de compte de stockage source.

## <a name="other-azcopy-features"></a>Autres fonctionnalités AzCopy
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a>Copier uniquement les données qui n’existent pas dans la destination de hello
Hello `--exclude-older` et `--exclude-newer` paramètres vous permettent de tooexclude des ressources de source ancien ou plus récent à partir de la copie, respectivement. Si vous souhaitez uniquement les ressources de la source toocopy qui n’existent pas dans la destination de hello, vous pouvez spécifier les deux paramètres Bonjour AzCopy commande :

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-toospecify-command-line-parameters"></a>Utiliser un paramètres de ligne de commande de toospecify de fichier de configuration

```azcopy
azcopy --config-file "azcopy-config.ini"
```

Vous pouvez inclure n’importe quels paramètres en ligne de commande AzCopy dans un fichier config. AzCopy processus hello paramètres hello fichier comme s’ils avaient été spécifiés sur la ligne de commande hello, effectuer une substitution directe avec le contenu de hello du fichier de hello.

Supposons un fichier de configuration nommé `copyoperation`, qui contient les lignes suivantes de hello. Chaque paramètre AzCopy peut être spécifié sur une seule ligne.

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

ou sur des lignes distinctes :

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

AzCopy échoue si vous fractionnez le paramètre hello entre deux lignes, comme indiqué ici pour hello `--source-key` paramètre :

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a>Spécification d’une signature d’accès partagé (SAP)

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

Vous pouvez également spécifier une SAP sur l’URI du conteneur hello :

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

Notez que AzCopy actuellement prend uniquement en charge hello [compte SAP](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).

### <a name="journal-file-folder"></a>Dossier du fichier journal
Chaque fois que vous exécutez une commande tooAzCopy, il vérifie si un fichier journal existe dans le dossier par défaut de hello, ou si elle existe dans un dossier que vous avez spécifié à l’aide de cette option. Si le fichier journal de hello n’existe pas à cet emplacement, AzCopy traite l’opération de hello en tant que nouvelle et génère un nouveau fichier journal.

Si le fichier journal de hello existe, AzCopy vérifie si la ligne de commande hello que vous avez entré correspond à ligne de commande hello dans un fichier de journal hello. Si les deux lignes de commande hello correspondent, AzCopy reprend les opérations d’incomplète hello. Si elles ne correspondent pas, AzCopy invite utilisateur tooeither remplacer hello journal fichier toostart une nouvelle opération ou opération toocancel hello en cours.

Si vous souhaitez toouse hello emplacement par défaut hello journal fichier :

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

Si vous omettez l’option `--resume`, ou spécifiez l’option `--resume` sans chemin d’accès du dossier hello, comme indiqué ci-dessus, AzCopy crée hello journal fichier dans l’emplacement par défaut hello, qui est `~\Microsoft\Azure\AzCopy`. Si le fichier journal de hello existe déjà, AzCopy reprend les opérations de hello basée sur le fichier journal de hello.

Si vous souhaitez toospecify un emplacement personnalisé pour le fichier journal de hello :

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

Cet exemple crée le fichier journal de hello si elle n’existe pas déjà. S’il n’existe pas, AzCopy reprend les opérations de hello basée sur le fichier journal de hello.

Si vous souhaitez tooresume une opération AzCopy, répétez hello même commande. AzCopy sur Linux vous invitera à confirmer l’opération :

```azcopy
Incomplete operation with same command line detected at hello journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want tooresume hello operation? Choose Yes tooresume, choose No toooverwrite hello journal toostart a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a>Journaux détaillés de sortie

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a>Spécifiez le nombre hello d’opérations simultanées toostart
Option `--parallel-level` Spécifie le nombre de hello d’opérations de copie simultanées. Par défaut, AzCopy démarre un certain nombre de débit de transfert de données des opérations simultanées tooincrease hello. nombre de Hello d’opérations simultanées est égal huit fois hello le nombre de processeurs que vous avez. Si vous exécutez AzCopy sur un réseau à faible bande passante, vous pouvez spécifier un nombre inférieur pour--parallèle au niveau tooavoid a échoué en concurrence de la ressource.

[!TIP]
>liste de tooview hello complète des paramètres de AzCopy, extraire 'azcopy--help' menu.

## <a name="known-issues-and-best-practices"></a>Problèmes connus et meilleures pratiques
### <a name="error-net-core-is-not-found-in-hello-system"></a>Erreur : Le .NET Core est introuvable dans le système de hello.
Si vous rencontrez une erreur indiquant que le .NET Core n’est pas installé dans le système de hello, hello binaire de chemin d’accès toohello .NET Core `dotnet` est absent.

Dans commande tooaddress ce problème, recherchez les binaires de .NET Core hello dans le système de hello :
```bash
sudo find / -name dotnet
```

Cela retourne hello chemin d’accès toohello dotnet binaire. 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

Maintenant, ajoutez cette variable de chemin d’accès au chemin d’accès toohello. Sudo, modifiez secure_path toocontain hello chemin d’accès toohello dotnet binaire :
```bash 
sudo visudo
### Append hello path found in hello preceding example too'secure_path' variable
```

Dans cet exemple, la variable secure_path se lit comme :

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

Pour l’utilisateur actuel de hello, modifier.bash_profile/.profile tooinclude hello chemin d’accès toohello dotnet binaire dans la variable de chemin d’accès 
```bash
vi ~/.bash_profile
### Append hello path found in hello preceding example too'PATH' variable
```

Vérifiez que .NET Core est désormais dans PATH :
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a>Erreur lors de l’installation d’AzCopy
Si vous rencontrez des problèmes avec l’installation de AzCopy, vous pouvez essayer de toorun AzCopy à l’aide du script d’interpréteur de commandes hello Bonjour extrait `azcopy` dossier.

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a>Limitation des écritures simultanées lors de la copie des données
Lorsque vous copiez des objets BLOB ou fichiers avec AzCopy, gardez à l’esprit qu’une autre application peut être modification des données de hello pendant que vous effectuez la copie. Si possible, assurez-vous que vous copiez les données de salutation ne sont pas modifiées pendant l’opération de copie hello. Par exemple, lors de la copie d’un disque dur virtuel associé à une machine virtuelle Azure, assurez-vous qu’aucune autre application n’écrivez actuellement toohello disque dur virtuel. Un bon moyen toodo qu'est en louant hello ressource toobe copié. Ou bien, vous pouvez créez d’abord un instantané de hello disque dur virtuel, puis copiez instantané d’hello.

Si vous ne pouvez pas empêcher les autres applications à partir de l’écriture de tooblobs ou des fichiers pendant qu’ils sont copiés, puis que vous n’oubliez pas que par hello temps hello tâche se termine, hello ressources copiées peuvent ne plus avoir parité complète avec les ressources de la source hello.

### <a name="run-one-azcopy-instance-on-one-machine"></a>Exécuter une instance de AzCopy sur un même ordinateur.
AzCopy est l’utilisation de hello toomaximize conçu votre ordinateur ressource tooaccelerate hello de transfert de données, nous vous recommandons exécutez qu’une seule instance AzCopy sur un ordinateur et spécifiez l’option de hello `--parallel-level` si vous avez besoin d’opérations simultanées plus. Pour plus d’informations, tapez `AzCopy --help parallel-level` à la ligne de commande hello.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur le stockage Azure et AzCopy, consultez hello suivant des ressources :

### <a name="azure-storage-documentation"></a>Documentation d’Azure Storage :
* [Introduction tooAzure stockage](storage-introduction.md)
* [Créer un compte de stockage](storage-create-storage-account.md)
* [Gérer les ressources de stockage Blob Azure avec l’explorateur de stockage (préversion)](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [À l’aide de hello Azure CLI 2.0 avec le stockage Azure](storage-azure-cli.md)
* [Comment toouse stockage d’objets Blob à partir de C++](storage-c-plus-plus-how-to-use-blobs.md)
* [Comment toouse stockage d’objets Blob à partir de Java](storage-java-how-to-use-blob-storage.md)
* [Comment toouse stockage d’objets Blob à partir de Node.js](storage-nodejs-how-to-use-blob-storage.md)
* [Comment toouse stockage d’objets Blob à partir de Python](storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a>Billets de blog Azure Storage :
* [Announcing AzCopy on Linux Preview](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/) (Annonce de la préversion d’AzCopy sur Linux)
* [Présentation de la bibliothèque de déplacement des données dans Azure Storage en version préliminaire](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy : Présentation de la copie synchrone et du type de contenu personnalisé](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [AzCopy : Annonce de la disponibilité générale d'AzCopy 3.0 plus version préliminaire d'AzCopy 4.0 avec prise en charge de fichier et de table](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [AzCopy : Optimisation pour les scénarios de copie à grande échelle](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy : Prise en charge des comptes de stockage géo-redondants avec accès en lecture](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [AzCopy – Transfer data with re-startable mode and SAS Token](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx) (AzCopy : Transfert des données avec mode reprise et jeton SAP)
* [AzCopy : Utilisation de copie d'objets blob sur plusieurs comptes](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [AzCopy : Chargement/téléchargement des fichiers pour les objets blob Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

