---
title: aaaUse stockage Azure files avec Linux | Documents Microsoft
description: "Découvrez comment toomount un fichier Azure partager sur SMB sur Linux."
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6edc37ce-698f-4d50-8fc1-591ad456175d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/8/2017
ms.author: renash
ms.openlocfilehash: ed6ba9b98f121d6629d858320ca3760384303ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-storage-with-linux"></a>Utilisation du stockage de fichiers Azure avec Linux
[Stockage de fichier Azure](storage-dotnet-how-to-use-files.md) est le système de fichiers de cloud de Microsoft toouse facile. Les partages de fichiers Azure peuvent être montés dans des distributions de Linux à l’aide de hello [cifs-utils package](https://wiki.samba.org/index.php/LinuxCIFS_utils) de hello [projet de Samba](https://www.samba.org/). Cet article montre deux façons toomount un partage de fichiers Azure : flux de données à la demande avec hello `mount` de commande et de démarrage en créant une entrée dans `/etc/fstab`.

> [!NOTE]  
> Dans l’ordre toomount un partage de fichiers Azure en dehors de hello région Azure, qu'il est hébergé dans, telles que localement ou dans une autre région Azure hello du système d’exploitation doit prendre en charge la fonctionnalité de chiffrement hello de SMB 3.0. La fonctionnalité de chiffrement pour SMB 3.0 pour Linux a été introduite dans le noyau 4.11. Cette fonctionnalité permet le montage du partage de fichiers Azure en local ou à partir d’une autre région Azure. Au moment de hello du processus de publication, cette fonctionnalité a été tooUbuntu utilisées à partir de 16.04 et versions ultérieures.


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-hello-cifs-utils-package"></a>Préalables pour le montage d’un partage de fichiers Azure avec Linux et hello package de cifs-utils
* **Choisir une distribution Linux qui peut avoir des package de cifs-utils hello installé**: Microsoft vous recommande de hello suivant des distributions de Linux dans la galerie d’images Azure hello :

    * Ubuntu Server 14.04+
    * RHEL 7+
    * CentOS 7+
    * Debian 8
    * openSUSE 13.2+
    * SUSE Linux Enterprise Server 12

* <a id="install-cifs-utils"></a>**Hello cifs-utils installation**: hello cifs-utils peut être installé à l’aide du Gestionnaire de package hello sur la distribution de Linux hello de votre choix. 

    Sur **Ubuntu** et **basée sur Debian** distributions, utilisez hello `apt-get` Gestionnaire de package :

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    Sur **RHEL** et **CentOS**, utilisez hello `yum` Gestionnaire de package :

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    Sur **openSUSE**, utilisez hello `zypper` Gestionnaire de package :

    ```
    sudo zypper install samba*
    ```

    Sur les autres distributions, utilisez le Gestionnaire de package approprié hello ou [une compilation à partir de la source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).

* **Décider des autorisations de répertoire/fichier hello du partage de monté hello**: dans les exemples de hello ci-dessous, nous utilisons 0777, toogive lire, écrire et exécuter des autorisations accordées aux utilisateurs de tooall. Vous pouvez les remplacer par d’autres [autorisations chmod](https://en.wikipedia.org/wiki/Chmod) comme vous le souhaitez. 

* **Nom de compte de stockage**: partage d’un fichier Azure toomount, vous devez serez hello nom hello du compte de stockage.

* **Clé de compte de stockage**: partage d’un fichier Azure toomount, vous devez serez hello la clé primaire (ou secondaire). Actuellement, les clés SAS ne sont pas prises en charge pour le montage.

* **Assurez-vous que le port 445 est ouvert**: SMB communique via le port TCP 445 - Vérifiez toosee si votre pare-feu ne bloque pas les TCP ports 445 à partir de l’ordinateur client.

## <a name="mount-hello-azure-file-share-on-demand-with-mount"></a>Monter hello à la demande avec un partage de fichiers de Azure`mount`
1. **[Installer le package de cifs-utils hello pour votre distribution Linux](#install-cifs-utils)**.

2. **Créez un dossier pour le point de montage hello**: cela n’importe où sur le système de fichiers hello.

    ```
    mkdir mymountpoint
    ```

3. **Utilisez hello montage commande toomount hello Azure File share**: n’oubliez pas de tooreplace `<storage-account-name>`, `<share-name>`, et `<storage-account-key>` avec des informations correctes hello.

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> Lorsque vous avez terminé à l’aide de hello le partage de fichiers Azure, vous pouvez utiliser `sudo umount ./mymountpoint` partage de hello toounmount.

## <a name="create-a-persistent-mount-point-for-hello-azure-file-share-with-etcfstab"></a>Créer un point de montage persistant pour le partage de fichiers Azure hello avec`/etc/fstab`
1. **[Installer le package de cifs-utils hello pour votre distribution Linux](#install-cifs-utils)**.

2. **Créez un dossier pour le point de montage hello**: cela n’importe où sur le système de fichiers hello, mais vous avez besoin de chemin d’accès absolu toonote hello du dossier de hello. Hello, l’exemple suivant crée un dossier sous la racine.

    ```
    sudo mkdir /mymountpoint
    ```

3. **Hello tooappend suivant trop de ligne de commande de suivante de hello utilisation`/etc/fstab`**: n’oubliez pas de tooreplace `<storage-account-name>`, `<share-name>`, et `<storage-account-key>` avec des informations correctes hello.

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> Vous pouvez utiliser `sudo mount -a` toomount partage de fichiers Azure hello après la modification `/etc/fstab` au lieu de redémarrer.

## <a name="feedback"></a>Commentaires
Les utilisateurs Linux, nous souhaitons toohear vous !

Hello stockage de fichier Azure pour le groupe d’utilisateurs Linux propose un forum pour vous tooshare commentaires que vous évaluez et adoptez le stockage de fichier sur Linux. Messagerie [le stockage de fichiers Azure les utilisateurs Linux](mailto:azurefileslinuxusers@microsoft.com) groupe d’utilisateurs toojoin hello.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur le stockage de fichiers Azure, consultez ces liens.
* [Référence de l’API REST du service de fichiers](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [Utilisation d’Azure PowerShell avec Stockage Azure](storage-powershell-guide-full.md)
* [Comment toouse AzCopy avec le stockage Microsoft Azure](storage-use-azcopy.md)
* [À l’aide de hello CLI d’Azure avec le stockage Azure](storage-azure-cli.md#create-and-manage-file-shares)
* [FAQ](storage-files-faq.md)
* [Dépannage](storage-troubleshoot-file-connection-problems.md)
