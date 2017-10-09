---
title: "aaaCreate et téléchargement d’un ordinateur virtuel de l’image à l’aide de Powershell | Documents Microsoft"
description: "En savoir plus toocreate et télécharger une image Windows Server généralisée (VHD) à l’aide du modèle de déploiement classique hello et Azure Powershell."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8c4a08fe-7714-4bf0-be87-c728a7806d3f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: 093b57c9157cea5f348c8ba02b5700c917adbcdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-windows-server-vhd-tooazure"></a>Créer et télécharger un tooAzure le disque dur virtuel de Windows Server
Cet article vous explique comment tooupload votre propre machine virtuelle généralisée de l’image en tant qu’un disque dur virtuel (VHD) qui vous permet de toocreate virtuels. Pour en savoir plus sur les disques et les disques durs virtuels dans Microsoft Azure, consultez [À propos des disques et VHD pour machines virtuelles](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Vous pouvez également [télécharger](../upload-generalized-managed.md) un ordinateur virtuel à l’aide du modèle de gestionnaire de ressources hello.

## <a name="prerequisites"></a>Composants requis
Cet article suppose que vous disposez de :

* **Un abonnement Azure** : si vous n’en avez pas, vous pouvez [ouvrir un compte Azure gratuitement](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
* **[Microsoft Azure PowerShell](/powershell/azure/overview)**  -vous avez hello Microsoft Azure PowerShell module installé et configuré toouse votre abonnement.
* **UN FICHIER. Fichier de disque dur virtuel** - Windows pris en charge stocké dans un fichier .vhd et les joint tooa virtual machine de système d’exploitation. Vérifiez toosee si les rôles de serveur hello en cours d’exécution sur le disque dur virtuel de hello sont pris en charge par Sysprep. Pour plus d’informations, consultez [Prise en charge de Sysprep pour les rôles serveur](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).

    > [!IMPORTANT]
    > format VHDX Hello n’est pas pris en charge dans Microsoft Azure. Vous pouvez convertir le format de tooVHD hello disque à l’aide du Gestionnaire Hyper-V ou hello [applet de commande Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx). Pour plus de détail, voir [ce billet de blog](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).

## <a name="step-1-prep-hello-vhd"></a>Étape 1 : Préparer un disque dur virtuel de hello
Avant de télécharger tooAzure de disque dur virtuel hello, il doit toobe généralisé à l’aide de l’outil Sysprep hello. Elle prépare hello toobe de disque dur virtuel utilisé en tant qu’image. Pour plus d’informations sur Sysprep, consultez [comment tooUse Sysprep : Introduction](http://technet.microsoft.com/library/bb457073.aspx). Sauvegardez hello machine virtuelle avant d’exécuter Sysprep.

Machine virtuelle hello hello du système d’exploitation a été installé pour terminer hello procédure :

1. Système d’exploitation de toohello vous connecter.
2. Ouvrez une fenêtre d’invite de commandes en tant qu’administrateur. Basculez hello trop**%windir%\system32\sysprep**, puis exécutez `sysprep.exe`.

    ![Ouvrir une fenêtre d’invite de commandes](./media/createupload-vhd/sysprep_commandprompt.png)
3. Hello **outil de préparation système** boîte de dialogue s’affiche.

   ![Démarrer Sysprep](./media/createupload-vhd/sysprepgeneral.png)
4. Bonjour **outil de préparation système**, sélectionnez **Entrez système boîte expérience OOBE (Out of)** et assurez-vous que **Generalize** est activée.
5. Dans **Options d’arrêt**, sélectionnez **Arrêter**.
6. Cliquez sur **OK**.

## <a name="step-2-create-a-storage-account-and-a-container"></a>Étape 2 : Créer un compte de stockage et un conteneur
Vous avez besoin d’un compte de stockage dans Azure afin que vous ayez un fichier .vhd de place tooupload hello. Cette étape vous montre comment toocreate un compte ou get hello info vous avez besoin d’un compte existant. Remplacer les variables hello dans &lsaquo; crochets &rsaquo; avec vos propres informations.

1. Connexion

    ```powershell
    Add-AzureAccount
    ```

2. Définissez votre abonnement Azure.

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. Créez un nouveau compte de stockage. nom Hello hello du compte de stockage doit être unique, 3 et 24 caractères. nom de Hello peut être n’importe quelle combinaison de lettres et chiffres. Vous devez également toospecify un emplacement comme « East US »

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. Définir le nouveau compte de stockage hello comme valeur par défaut hello.

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. Créez un conteneur.

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-hello-vhd-file"></a>Étape 3 : Téléchargez le fichier .vhd de hello
Hello d’utilisation [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) hello de tooupload disque dur virtuel.

À partir de la fenêtre d’Azure PowerShell hello utilisé à l’étape précédente de hello, tapez ce qui suit hello commande et remplacer les variables hello dans &lsaquo; crochets &rsaquo; avec vos propres informations.

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-hello-image-tooyour-list-of-custom-images"></a>Étape 4 : Ajouter la liste de tooyour image hello d’images personnalisées
Hello d’utilisation [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) applet de commande tooadd hello toohello liste d’images vos images personnalisées.

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez désormais [créer une machine virtuelle personnalisée](createportal.md) vous avez téléchargée à l’aide de hello l’image.
