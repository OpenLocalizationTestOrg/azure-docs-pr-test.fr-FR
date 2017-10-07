---
title: "aaaHow toomanage stockage Azure Files à partir de hello portail Azure | Documents Microsoft"
description: "Découvrez le stockage de fichiers Azure toouse hello toomanage portail Azure."
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
ms.openlocfilehash: 385b99ac1c3d97ca79059ae8229afb53f1e825cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-file-storage-from-hello-azure-portal"></a>Comment le stockage de fichier Azure toouse de hello portail Azure
Hello [portail Azure](https://portal.azure.com) fournit une interface utilisateur pour la gestion du stockage de fichiers Azure. Vous pouvez effectuer hello suivant des actions dans votre navigateur web :

* Créer un partage de fichiers
* Télécharger des fichiers tooand à partir de votre partage de fichiers.
* Surveillez l’utilisation réelle de hello de chaque partage de fichiers.
* Ajustez le quota de taille de partage de fichiers hello.
* Copiez hello montage commandes toouse toomount de partage de vos fichiers à partir d’un client Windows ou Linux.

## <a name="create-file-share"></a>Créer un partage de fichiers
1. Se connecter toohello portail Azure.
2. Dans le menu de navigation hello, cliquez sur **comptes de stockage** ou **comptes de stockage (classiques)**.
    
    ![Capture d’écran qui montre comment partager des fichiers de toocreate dans le portail de hello](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. Choisissez votre compte de stockage.

    ![Capture d’écran qui montre comment partager des fichiers de toocreate dans le portail de hello](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. Choisissez le service Fichiers.

    ![Capture d’écran qui montre comment partager des fichiers de toocreate dans le portail de hello](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. Cliquez sur « Partages de fichiers » et suivez les toocreate de lien de hello partager de votre premier fichier.

    ![Capture d’écran qui montre comment partager des fichiers de toocreate dans le portail de hello](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. Renseignez nom de partage de fichiers hello et taille hello de toocreate de partage (haut too5120 Go) fichier hello votre première partage de fichiers. Une fois que le partage de fichiers hello a été créé, vous pouvez le monter à partir de n’importe quel système de fichiers qui prend en charge SMB 2.1 ou SMB 3.0. Vous pouvez cliquer sur **Quota** hello taille de fichier partage toochange hello du fichier hello des too5120 go. Reportez-vous trop[calculatrice de tarification Azure](https://azure.microsoft.com/pricing/calculator/) tooestimate hello stockage à moindre coût de l’utilisation du stockage de fichiers Azure.

    ![Capture d’écran qui montre comment partager des fichiers de toocreate dans le portail de hello](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a>Charger et télécharger des fichiers
1. Choisissez un partage de fichiers que vous avez déjà créé.

    ![Capture d’écran qui illustre comment tooupload et téléchargez des fichiers à partir de hello portail](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. Cliquez sur **télécharger** pour ouvrir l’interface utilisateur de hello pour télécharger les fichiers.

    ![Capture d’écran qui illustre comment les fichiers à partir du portail de hello tooupload](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-toofile-share"></a>Se connecter toofile partage
-  Cliquez sur **connexion** pour obtenir la ligne de commande hello montage hello partage de fichiers à partir de Windows et Linux. Pour les utilisateurs Linux, vous pouvez également faire référence trop[comment toouse stockage Azure files avec Linux](storage-how-to-use-files-linux.md) pour plus d’instructions de montage pour les autres distributions de Linux.

    ![Capture d’écran qui illustre comment toomount hello partage de fichiers](media/storage-file-how-to-use-files-portal/use-files-portal-connect.png)
-  Vous pouvez copier hello commandes permettant de monter le fichier de partage sous Windows ou Linux et exécuter de votre ordinateur local ou de machine virtuelle Azure.

    ![Capture d’écran qui affiche les commandes de montage hello pour Windows et Linux](media/storage-file-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

**Conseil :**  
clé toofind hello accès de montage, cliquez sur **clés d’accès en lecture pour ce compte de stockage** bas hello hello page de connexion.

## <a name="see-also"></a>Voir aussi
Pour plus d’informations sur le stockage de fichiers Azure, consultez ces liens.

* [FAQ](storage-files-faq.md)
* [Dépannage](storage-troubleshoot-file-connection-problems.md)