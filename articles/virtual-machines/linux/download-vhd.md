---
title: "aaaDownload un VHD Linux à partir de Azure | Documents Microsoft"
description: "Télécharger un VHD Linux à l’aide de hello CLI d’Azure et hello portail Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: 7e08e985a64a6be581b8f5eedcce60fbd314eaf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-linux-vhd-from-azure"></a>Télécharger un disque VHD Linux à partir d’Azure

Dans cet article, vous apprendrez comment toodownload un [(VHD) du disque dur virtuel Linux](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) fichier à partir d’Azure à l’aide hello CLI d’Azure et le portail Azure. 

Machines virtuelles (VM) en cours d’utilisation Azure [disques](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) comme un toostore place un système d’exploitation, des applications et des données. Toutes les machines virtuelles Azure possèdent au moins deux disques : un disque de système d’exploitation Windows et un disque temporaire. disque de système d’exploitation Hello est initialement créé à partir d’une image et disque de système d’exploitation hello et image de hello sont des disques durs virtuels stockés dans un compte de stockage Azure. Les machines virtuelles peuvent également disposer d’un ou plusieurs disques de données, également stockés sur les VHD.

Si ce n’est déjà fait, installez [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).

## <a name="stop-hello-vm"></a>Arrêter hello machine virtuelle

Un disque dur virtuel ne peut être téléchargé à partir d’Azure, si elle est attachée tooa machine virtuelle en cours d’exécution. Vous devez toodownload de machine virtuelle hello toostop un disque dur virtuel. Si vous voulez toouse un disque dur virtuel en tant qu’un [image](tutorial-custom-images.md) toocreate autres machines virtuelles avec de nouveaux disques, vous devez toodeprovision et généraliser le système d’exploitation de hello contenue dans hello de fichiers et d’arrêter hello machine virtuelle. toouse hello disque dur virtuel en tant que disque d’une nouvelle instance d’un ordinateur virtuel existant ou d’un disque de données, vous seulement devez toostop et désallouer hello machine virtuelle.

toouse hello de disque dur virtuel en tant qu’une image toocreate autres machines virtuelles, procédez comme suit :

1. Utiliser SSH, nom du compte hello et hello adresse IP publique de hello VM tooconnect tooit et annuler le déploiement. Bonjour + utilisateur paramètre supprime également le dernier compte d’utilisateur configuré hello. Si vous sont cuisson des informations d’identification de compte dans toohello VM, laissez cette + paramètre de l’utilisateur. Hello exemple suivant supprime hello dernier compte d’utilisateur configuré :

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. Se connecter tooyour compte Azure avec [ouverture de session az](https://docs.microsoft.com/cli/azure/#login).
3. Arrêter et désallouer hello machine virtuelle.

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. Généraliser hello machine virtuelle. 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

toouse hello disque dur virtuel en tant que disque d’une nouvelle instance d’un ordinateur virtuel existant ou d’un disque de données, procédez comme suit :

1.  Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2.  Dans le menu du Hub hello, cliquez sur **virtuels**.
3.  Sélectionnez hello machine virtuelle à partir de la liste de hello.
4.  Dans le panneau hello pour hello machine virtuelle, cliquez sur **arrêter**.

    ![Arrêter la machine virtuelle](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a>Générer une URL de SAP

fichier de disque dur virtuel toodownload hello, vous devez toogenerate une [signature d’accès partagé (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL. Lorsque l’URL de hello est généré, un délai d’expiration est affecté toohello URL.

1.  Dans menu hello du panneau hello pour hello machine virtuelle, cliquez sur **disques**.
2.  Sélectionnez le disque du système d’exploitation hello pour hello machine virtuelle, puis cliquez sur **exporter**.
3.  Cliquez sur **Générer l’URL**.

    ![Générer une URL](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a>Télécharger un VHD

1.  URL hello qui a été généré, cliquez sur fichier de disque dur virtuel de téléchargement hello.

    ![Télécharger un VHD](./media/download-vhd/export-download.png)

2.  Vous devrez peut-être tooclick **enregistrer** dans le téléchargement de hello navigateur toostart hello. nom par défaut de Hello pour le fichier de disque dur virtuel hello est *abcd*.

    ![Cliquez sur Enregistrer dans le navigateur de hello](./media/download-vhd/export-save.png)

## <a name="next-steps"></a>Étapes suivantes

- Découvrez comment trop[télécharger et de créer un VM Linux à partir du disque personnalisé avec hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 
- [Gérer les disques Azure hello CLI d’Azure](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

