---
title: "aaaUpload disque dur virtuel du fichier à l’aide de Microsoft Azure Storage Explorer de tooAzure DevTest Labs | Documents Microsoft"
description: "Télécharger le compte de stockage de toolab du fichier de disque dur virtuel à l’aide de l’Explorateur de stockage Microsoft Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 686691e3676cea4b2d7cd8bf045bc43a792c667e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-microsoft-azure-storage-explorer"></a>Télécharger le compte de stockage de toolab du fichier de disque dur virtuel à l’aide de l’Explorateur de stockage Microsoft Azure

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

Dans Azure DevTest Labs, les fichiers de disque dur virtuel peuvent être utilisé toocreate des images personnalisées, qui sont des ordinateurs virtuels tooprovision utilisé. Cet article explique comment toouse [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) compte de stockage du laboratoire tooa de fichiers tooupload un disque dur virtuel. Une fois que vous avez téléchargé votre fichier de disque dur virtuel, hello [étapes section](#next-steps) répertorie certains articles qui expliquent comment toocreate une image personnalisée à partir de hello téléchargé le fichier de disque dur virtuel. Pour plus d’informations sur les disques et les disques durs virtuels dans Azure, consultez [À propos des disques et des VHD pour les machines virtuelles Azure](../virtual-machines/linux/about-disks-and-vhds.md).

## <a name="step-by-step-instructions"></a>Instructions pas à pas

Hello après le parcours des étapes vous aide à télécharger un disque dur virtuel laboratoires tooDevTest à l’aide du fichier [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).

1. [Téléchargez et installez la version la plus récente de Microsoft Azure Storage Explorer de hello hello](http://www.storageexplorer.com).

1. Obtenir le nom de hello de du laboratoire hello compte de stockage à l’aide de hello portail Azure :

    1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
    
    1. Sélectionnez **davantage de services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.
    
    1. Dans liste hello labs, sélectionnez lab souhaité de hello.  
    
    1. Dans le panneau de hello lab, sélectionnez **Configuration**. 
    
    1. Atelier de hello **Configuration** panneau, sélectionnez **les images personnalisées (VHD)**.
    
    1. Sur hello **les images personnalisées** panneau, sélectionnez **+ ajouter**. 
    
    1. Sur hello **image personnalisée** panneau, sélectionnez **disque dur virtuel**.
    
    1. Sur hello **VHD** panneau, sélectionnez **télécharger un disque dur virtuel à l’aide de PowerShell**.
    
        ![Télécharger un disque dur virtuel à l’aide de PowerShell][0]
    
    1. Hello **télécharger une image à l’aide de PowerShell** panneau affiche un appel toohello **Add-AzureVhd** applet de commande. Hello du premier paramètre (*Destination*) contient le nom de compte de stockage hello pour laboratoire hello Bonjour suivant le format :
    
        https://<NOM-COMPTE-STOCKAGE>.blob.core.windows.net/uploads/... 

    1. Prenez note du nom de compte de stockage hello qu’il est utilisé dans les étapes ultérieures.
    
1. Se connecter tooan compte d’abonnement Azure à l’aide de l’Explorateur de stockage.

    > [!TIP] 
    > 
    > Ce dernier prend en charge plusieurs options de connexion. Cette section illustre le compte de stockage qui se connecte tooa associé à votre abonnement Azure. toosee hello d’autres options de connexion pris en charge par l’Explorateur de stockage, consultez l’article toohello [prise en main de l’Explorateur de stockage](../vs-azure-tools-storage-manage-with-storage-explorer.md).
 
    1. Ouvrez l’Explorateur de stockage.
    
    1. Dans l’Explorateur de stockage, sélectionnez **Paramètres de compte Azure**. 
    
        ![paramètres de compte Azure][1]
    
    1. volet de gauche de Hello affiche les comptes Microsoft hello que vous avez ouvert une session. tooconnect tooanother compte, sélectionnez **ajouter un compte**et suivez les toosign de boîtes de dialogue hello avec un compte Microsoft associé au moins un abonnement Azure actif.
    
        ![Ajouter un compte][2]
    
    1. Une fois que vous vous connectez avec succès avec un compte Microsoft, volet de gauche hello remplit avec hello Azure abonnements associés à ce compte. Sélectionnez hello abonnements Azure avec lequel vous souhaitez toowork, puis sélectionnez **appliquer**. (En sélectionnant **tous les abonnements** bascules hello sélection de l’ensemble ou aucun des hello répertorié abonnements Azure.)
    
        ![Sélectionner les abonnements Azure][3]
    
    1. volet de gauche Hello affiche les comptes de stockage hello associées aux abonnements Azure de hello sélectionné.
    
        ![Abonnements Azure sélectionnés][4]

1. Recherchez le compte de stockage du laboratoire hello :

    1. Dans le volet gauche de l’Explorateur de stockage hello, recherchez et développez le nœud hello pour hello abonnement Azure propriétaire du lab de hello.
    
    1. Sous le nœud de l’abonnement hello, développez **comptes de stockage**.

    1. Développez les nœuds de tooreveal du laboratoire hello stockage compte nœud pour **conteneurs d’objets Blob**, **des partages de fichiers**, **les files d’attente**, et **Tables**.
    
    1. Développez hello **conteneurs d’objets Blob** nœud.
    
    1. Sélectionnez hello téléchargements blob conteneur toodisplay son contenu dans le volet de droite hello.
        
        ![Répertoire du téléchargement][5]

1. Téléchargez le fichier de disque dur virtuel de hello à l’aide de l’Explorateur de stockage :

    1. Dans le volet droit de l’Explorateur de stockage hello, vous devez voir une liste d’objets BLOB de hello Bonjour **télécharge** conteneur d’objets blob de du laboratoire hello compte de stockage. Dans la barre d’outils de l’éditeur hello blob, sélectionnez **télécharger** 
        
        ![Bouton Télécharger][6]
    
    1. À partir de hello **télécharger** menu déroulant, sélectionnez **télécharger des fichiers...** .
    
    1. Sur hello **télécharger des fichiers** boîte de dialogue, les points de suspension hello select.
        
        ![Sélectionner un fichier][8]  

    1. Sur hello **tooupload de sélection de fichiers** boîte de dialogue Parcourir toohello souhaité fichier VHD, sélectionnez-le, puis sélectionnez **ouvrir**.
    
    1. Lorsque retourné toohello **télécharger des fichiers** boîte de dialogue, modification **type d’objets Blob** trop**objet Blob de pages**.
    
    1. Sélectionnez **Télécharger**.

        ![Sélectionner un fichier][9]  
    
    1. Hello Explorateur de stockage **le journal d’activité** volet affiche l’état du téléchargement hello (ainsi que des liens toocancel hello chargement). processus Hello de téléchargement d’un fichier de disque dur virtuel peut être longue, en fonction de la taille de hello du fichier de disque dur virtuel hello et votre vitesse de connexion. 

        ![État du téléchargement de fichier][10]  

## <a name="next-steps"></a>Étapes suivantes

- [Créer une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide de hello portail Azure](devtest-lab-create-template.md)
- [Créer une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide de PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

[0]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-image-using-psh.png
[1]: ./media/devtest-lab-upload-vhd-using-storage-explorer/settings-icon.png
[2]: ./media/devtest-lab-upload-vhd-using-storage-explorer/add-account-link.png
[3]: ./media/devtest-lab-upload-vhd-using-storage-explorer/subscriptions-list.png
[4]: ./media/devtest-lab-upload-vhd-using-storage-explorer/storage-accounts-list.png
[5]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-dir.png
[6]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-button.png
[7]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-files.png
[8]: ./media/devtest-lab-upload-vhd-using-storage-explorer/select-file.png
[9]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-file.png
[10]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-status.png
