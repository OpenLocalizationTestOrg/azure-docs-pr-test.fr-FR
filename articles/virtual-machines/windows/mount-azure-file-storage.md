---
title: "aaaMount stockage de fichier Azure à partir d’une machine virtuelle de Windows Azure | Documents Microsoft"
description: "Stockez le fichier dans le cloud hello avec stockage de fichiers Azure et monter votre partage de fichiers de cloud à partir d’une machine virtuelle Azure (VM)."
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 965f1c1b3f0d07fec6d86f9312a05e02e8ce7fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a>Utiliser des partages de fichiers Azure avec des machines virtuelles Windows 

Vous pouvez utiliser des partages de fichiers Azure comme un moyen toostore et accèdent aux fichiers à partir de votre machine virtuelle. Par exemple, vous pouvez stocker un script ou un fichier de configuration que vous souhaitez toutes les tooshare de vos machines virtuelles. Dans cette rubrique, nous vous indiquons comment toocreate et montez Azure de partage de fichiers et tooupload et téléchargez des fichiers.

## <a name="connect-tooa-file-share-from-a-vm"></a>Connecter le partage de fichiers tooa d’une machine virtuelle

Cette section suppose que vous avez déjà un fichier que vous souhaitez tooconnect à du partage. Si vous devez toocreate une, consultez [créer un partage de fichiers](#create-a-file-share) plus loin dans cette rubrique.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans le menu de gauche hello, cliquez sur **comptes de stockage**.
3. Choisissez votre compte de stockage.
4. Bonjour **vue d’ensemble** sous **Services**, sélectionnez **fichiers**.
5. Sélectionnez un partage de fichiers.
6. Cliquez sur **Connect** tooopen une page qui affiche la syntaxe de ligne de commande de hello montage hello partage de fichiers Windows ou Linux.
7. Mettez en surbrillance la syntaxe hello de commande hello et collez-le dans le bloc-notes ou un autre endroit où vous pouvez y accéder facilement. 
8. Modifier la valeur principale de hello syntaxe tooremove hello ** > ** et remplacez *[lettre de lecteur]* avec la lettre de lecteur hello (par exemple, **Y:**) où vous souhaitez que le partage de fichiers toomount hello.
8. Se connecter tooyour machine virtuelle et ouvrez une invite de commandes.
9. Coller dans hello modifié la syntaxe de connexion et d’accès **entrée**.
10. Lors de la connexion de hello a été créée, vous obtenez le message de type hello **hello commande s’est terminée avec succès.**
11. Vérifiez la connexion de hello en tapant dans hello lettre tooswitch toothat lecteur et tapez **dir** contenu de hello toosee hello du partage de fichiers.



## <a name="create-a-file-share"></a>Créer un partage de fichiers 
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans le menu de gauche hello, cliquez sur **comptes de stockage**.
3. Choisissez votre compte de stockage.
4. Bonjour **vue d’ensemble** sous **Services**, sélectionnez **fichiers**.
5. Dans la page du Service de fichiers hello, cliquez sur **+ partage de fichiers** toocreate votre premier fichier partager. \
6. Renseignez le nom de partage de fichiers hello. Le nom des partages de fichiers peut inclure des lettres minuscules, des chiffres et des traits d’union. nom de Hello ne peut pas commencer par un trait d’union, et vous ne pouvez pas utiliser plusieurs traits d’union consécutifs. 
7. Remplissage dans une limite sur le fichier de hello quelle taille possible, too5120 go.
8. Cliquez sur **OK** partage de fichiers toodeploy hello.
   
## <a name="upload-files"></a>Charger des fichiers
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans le menu de gauche hello, cliquez sur **comptes de stockage**.
3. Choisissez votre compte de stockage.
4. Bonjour **vue d’ensemble** sous **Services**, sélectionnez **fichiers**.
5. Sélectionnez un partage de fichiers.
6. Cliquez sur **télécharger** tooopen hello **télécharger des fichiers** page.
7. Cliquez sur hello dossier icône toobrowse le système de fichiers local pour un tooupload de fichier.   
8. Cliquez sur **télécharger** partage de fichiers toohello tooupload hello fichier.

## <a name="download-files"></a>Téléchargement de fichiers
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans le menu de gauche hello, cliquez sur **comptes de stockage**.
3. Choisissez votre compte de stockage.
4. Bonjour **vue d’ensemble** sous **Services**, sélectionnez **fichiers**.
5. Sélectionnez un partage de fichiers.
6. Avec le bouton droit sur le fichier de hello et choisissez **télécharger** toodownload il tooyour les ordinateur local.
   

## <a name="next-steps"></a>Étapes suivantes

Vous pouvez également créer et gérer des partages de fichiers à l’aide de PowerShell. Pour plus d’informations, consultez [Prise en main du stockage de fichiers Azure sur Windows](../../storage/files/storage-dotnet-how-to-use-files.md).
