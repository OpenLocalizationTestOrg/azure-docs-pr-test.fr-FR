---
title: partage de fichiers Azure aaaMount sur SMB avec macOS | Documents Microsoft
description: "Découvrez comment partager des toomount un fichier Azure sur SMB avec macOS."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 71aaec8a77b770fe147b783c0ab9f86830176bec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a>Montage du partage de fichiers Azure via SMB avec MacOS
[Stockage de fichier Azure](../storage-dotnet-how-to-use-files.md) est service de Microsoft qui vous permet de partages de fichiers réseau toocreate et utilisez Bonjour Azure à l’aide de norme industrielle de hello. Les partages de fichiers Azure peuvent être montés dans MacOS Sierra (10.12) et El Capitan (10.11). Cet article montre deux façons différentes toomount un partage de fichiers Azure sur macOS avec hello l’interface utilisateur de la recherche et à l’aide de hello Terminal Server.

> [!Note]  
> Avant de monter un partage de fichiers Azure via SMB, il est recommandé de désactiver la signature de paquet SMB. Sinon, peut entraîner des performances médiocres lors de l’accès de partage de fichiers Azure hello de macOS. Votre connexion SMB est chiffrée, donc cela n’affecte pas la sécurité hello de votre connexion. À partir de hello Terminal Server, hello commandes suivantes désactivera la signature des paquets SMB, comme décrit par cet [article du support technique Apple sur la désactivation de la signature de paquet SMB](https://support.apple.com/HT205926):  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a>Conditions préalables pour le montage d’un partage de fichiers Azure sous MacOS
* **Nom de compte de stockage**: partage d’un fichier Azure toomount, vous devez serez hello nom hello du compte de stockage.

* **Clé de compte de stockage**: partage d’un fichier Azure toomount, vous devez serez hello la clé primaire (ou secondaire). Actuellement, les clés SAS ne sont pas prises en charge pour le montage.

* **Assurez-vous que le port 445 est ouvert** : SMB communique via le port TCP 445. Sur votre ordinateur client (hello Mac), vérifiez que votre pare-feu ne bloque pas le port TCP 445 de toomake.

## <a name="mount-an-azure-file-share-via-finder"></a>Montage d’un partage de fichiers Azure via Finder
1. **Ouvrir le Finder**: Finder est ouvert sur macOS par défaut, mais vous pouvez vous assurer qu’il est hello sélectionné actuellement application en cliquant sur hello « macOS accessibles icône » sur la station d’accueil hello :  
    ![Hello macOS accessibles icône](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)

2. **Sélectionnez « Se connecter tooServer » à partir de hello « Go » Menu**: à l’aide du chemin d’accès UNC de hello de hello [conditions préalables](#preq), convertir hello début double barre oblique inverse (`\\`) trop`smb://` et toutes les autres barres obliques inverses (`\`) les barres obliques tooforwards (`/`). Votre lien doit ressembler à hello suivant : ![boîte de dialogue « Se connecter tooServer » hello](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)

3. **Utilisation hello partage stockage et le nom de clé de compte lorsque vous y êtes invité pour un nom d’utilisateur et un mot de passe**: lorsque vous cliquez sur « Se connecter » sur la boîte de dialogue « Se connecter tooServer » hello, vous demandera d’utilisateur de hello et le mot de passe (il s’agira autopopulated avec votre macOS nom d’utilisateur). Vous pouvez hello de placer la clé de compte/nom du stockage hello partage dans votre trousseau Mac OS.

4. **Partage de fichiers Azure hello utilisation comme vous le souhaitez**: après la substitution hello partage de stockage et le nom de clé de compte dans pour hello username et password, partage de hello est monté. Vous pouvez utiliser cette option comme vous utiliseriez normalement un partage de dossier ou fichier local, y compris le glisser -déplacer des fichiers dans le partage de fichiers hello :

    ![Une capture instantanée d’un partage de fichiers Azure monté](./media/storage-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a>Montage d’un partage de fichiers Azure via Terminal
1. Remplacez `<storage-account-name>` par nom de hello de votre compte de stockage. Lorsque vous y êtes invité, entrez la clé du compte de stockage comme mot de passe. 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. **Partage de fichiers Azure hello utilisation comme vous le souhaitez**: partage de fichiers Azure hello est monté au point de montage hello spécifié par la commande précédente hello.  

    ![Un instantané du partage de fichiers Azure hello monté](./media/storage-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur le stockage de fichiers Azure, consultez ces liens.

* [Article du support technique Apple - comment tooconnect avec partage de fichiers sur votre Mac](https://support.apple.com/HT204445)
* [FAQ](../storage-files-faq.md)
* [Résolution des problèmes sur Windows](storage-troubleshoot-windows-file-connection-problems.md)      
* [Résolution des problèmes sur Linux](storage-troubleshoot-linux-file-connection-problems.md)    