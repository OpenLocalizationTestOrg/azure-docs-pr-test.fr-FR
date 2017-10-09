---
title: aaaCreating une image de machine virtuelle locale pour hello Azure Marketplace | Documents Microsoft
description: "Comprendre et déployer toohello Azure Marketplace pour d’autres utilisateurs et exécutez hello étapes toocreate une image de machine virtuelle locale toopurchase."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 26dfbd5a-8685-4b19-987e-c20ca60540ec
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c7a265330f1e494db8d0e981a38ee00d85746bb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-hello-azure-marketplace"></a>Développer une image de machine virtuelle locale pour hello Azure Marketplace
Nous vous recommandons fortement de développer des disques durs virtuels (VHD) Azure directement dans le cloud de hello à l’aide du protocole Bureau à distance. Toutefois, si nécessaire, il est possible de toodownload un disque dur virtuel et son développement à l’aide de l’infrastructure locale.  

Pour le développement local, vous devez télécharger le système d’exploitation de hello disque dur virtuel de hello créé machine virtuelle. Ces étapes s’intègrent à l’étape 3.3 présentée plus haut.  

## <a name="download-a-vhd-image"></a>Télécharger une image de disque dur virtuel
### <a name="locate-a-blob-url"></a>Localiser une URL d’objet blob
Bonjour toodownload de commande disque dur virtuel, d’abord localiser les URL de blob hello pour le disque du système d’exploitation hello.

Recherchez les URL de blob hello de hello nouvelle [portail Microsoft Azure](https://portal.azure.com):

1. Accédez trop**Parcourir** > **machines virtuelles**, et puis sélectionnez hello déployé la machine virtuelle.
2. Sous **configurer**, sélectionnez hello **disques** vignette, qui ouvre le panneau des disques hello.
   
   ![dessin](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. Sélectionnez hello **disque de système d’exploitation**, qui ouvre un autre panneau qui affiche les propriétés du disque, y compris l’emplacement du disque dur virtuel hello.
4. Copiez cette URL d’objet blob.
   
   ![dessin](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. Supprimez maintenant, hello déployé la machine virtuelle sans supprimer les disques de stockage hello. Vous pouvez également arrêter hello VM au lieu de sa suppression. Ne pas télécharger les VHD de système d’exploitation hello lorsque hello machine virtuelle est en cours d’exécution.
   
   ![dessin](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a>Télécharger un disque dur virtuel
Une fois que vous connaissez les URL de blob hello, vous pouvez télécharger hello disque dur virtuel à l’aide de hello [portail Azure](http://manage.windowsazure.com/) ou PowerShell.  

> [!NOTE]
> Au moment de hello de la création de ce guide, toodownload de fonctionnalité hello un disque dur virtuel n’est pas encore présente dans le nouveau portail de Microsoft Azure hello.  
> 
> 

**Télécharger hello, système d’exploitation VHD via hello actuel [portail Azure](http://manage.windowsazure.com/)**

1. Connectez-vous toohello portail Azure, si vous n'avez pas déjà fait.
2. Cliquez sur hello **stockage** onglet.
3. Sélectionnez le compte de stockage hello dans le hello disque dur virtuel est stocké.
   
   ![dessin](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. Les propriétés du compte de stockage s’affichent. Sélectionnez hello **conteneurs** onglet.
   
   ![dessin](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. Sélectionnez le conteneur hello dans le hello disque dur virtuel est stocké. Par défaut, lors de la création à partir du portail de hello, hello disque dur virtuel est stocké dans un conteneur de disques durs virtuels.
   
   ![dessin](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. Sélectionnez le disque dur virtuel du système d’exploitation correct hello en comparant les toohello URL hello une que vous avez enregistré.
7. Cliquez sur **Télécharger**.
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a>Télécharger un disque dur virtuel à l’aide de PowerShell
En outre toousing hello portail Azure, vous pouvez utiliser hello [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) système d’exploitation disque dur virtuel d’applet de commande toodownload hello.

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
Par exemple, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String>

> [!NOTE]
> **Save-AzureVhd** a également un **NumberOfThreads** option qui peut être utilisé tooincrease parallélisme toomake hello meilleure utilisation de la bande passante disponible pour le téléchargement de hello.
> 
> 

## <a name="upload-vhds-tooan-azure-storage-account"></a>Télécharger le compte de stockage Azure tooan de disques durs virtuels
Si vous avez préparé vos disques durs virtuels locaux, vous devez tooupload dans un stockage de compte dans Azure. Cette étape a lieu après la création de votre disque dur virtuel local, mais avant d’obtenir la certification pour votre image de machine virtuelle.

### <a name="create-a-storage-account-and-container"></a>Créer un compte de stockage et un conteneur
Nous vous recommandons de télécharger des disques durs virtuels dans un compte de stockage dans une région de hello aux États-Unis. Tous les disques durs virtuels pour une seule référence doivent être placés dans un seul conteneur au sein d’un seul compte de stockage.

toocreate un compte de stockage, vous pouvez utiliser hello [portail Microsoft Azure](https://portal.azure.com/), PowerShell, ou l’outil de ligne de commande hello Linux.  

**Créer un compte de stockage à partir du portail Microsoft Azure hello**

1. Cliquez sur **Nouveau**.
2. Sélectionnez **Stockage**.
3. Renseignez le nom de compte de stockage hello et sélectionnez un emplacement.
   
   ![dessin](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. Cliquez sur **Créer**.
5. panneau Hello pour hello créé le compte de stockage doit être ouvert. Dans le cas contraire, sélectionnez **Parcourir** > **Comptes de stockage**. Sur le stockage de hello compte panneau, sélectionnez le compte de stockage hello créé.
6. Sélectionnez **Conteneurs**.
   
   ![dessin](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. Dans le panneau de conteneurs hello, sélectionnez **ajouter**, puis entrez un conteneur hello et nom de conteneur des autorisations. Sélectionnez **Privé** pour les autorisations du conteneur.

> [!TIP]
> Nous vous recommandons de créer un conteneur par référence (SKU) que vous envisagez de toopublish.
> 
> 

  ![dessin](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a>Créer un compte de stockage à l’aide de PowerShell
À l’aide de PowerShell, créer un compte de stockage à l’aide de hello [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) applet de commande.

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

Vous pouvez ensuite créer un conteneur au sein de ce compte de stockage à l’aide de hello [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) applet de commande.

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> Ces commandes supposent que ce contexte de compte de stockage actuel hello a déjà été défini dans PowerShell.   Consultez trop[configurer Azure PowerShell](marketplace-publishing-powershell-setup.md) pour plus d’informations sur le programme d’installation de PowerShell.  
> 
> ### <a name="create-a-storage-account-by-using-hello-command-line-tool-for-mac-and-linux"></a>Créer un compte de stockage en utilisant l’outil de ligne de commande hello pour Mac et Linux
> Dans l’ [outil en ligne de commande Linux](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), créez un compte de stockage comme suit :
> 
> 

        azure storage account create mystorageaccount --location "West US"

Créez un conteneur comme suit :

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a>Télécharger un disque dur virtuel
Une fois que le compte de stockage hello et un conteneur sont créés, vous pouvez télécharger vos disques durs virtuels préparés. Vous pouvez utiliser PowerShell, outil de ligne de commande hello Linux ou autres outils de gestion du stockage Azure.

### <a name="upload-a-vhd-via-powershell"></a>Télécharger un disque dur virtuel à l’aide de PowerShell
Hello d’utilisation [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) applet de commande.

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-hello-command-line-tool-for-mac-and-linux"></a>Télécharger un disque dur virtuel en utilisant l’outil de ligne de commande hello pour Mac et Linux
Avec hello [outil de ligne de commande Linux](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), utilisez hello suivante : créer des images de machine virtuelle azure <image name> --emplacement <Location of hello data center> --système d’exploitation Linux<LocationOfLocalVHD>

## <a name="see-also"></a>Voir aussi
* [Création d’une image de machine virtuelle pour hello Marketplace](marketplace-publishing-vm-image-creation.md)
* [Configuration d’Azure PowerShell](marketplace-publishing-powershell-setup.md)

