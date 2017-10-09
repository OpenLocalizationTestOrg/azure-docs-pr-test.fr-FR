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
# <a name="create-and-upload-a-windows-server-vhd-tooazure"></a><span data-ttu-id="e0038-103">Créer et télécharger un tooAzure le disque dur virtuel de Windows Server</span><span class="sxs-lookup"><span data-stu-id="e0038-103">Create and upload a Windows Server VHD tooAzure</span></span>
<span data-ttu-id="e0038-104">Cet article vous explique comment tooupload votre propre machine virtuelle généralisée de l’image en tant qu’un disque dur virtuel (VHD) qui vous permet de toocreate virtuels.</span><span class="sxs-lookup"><span data-stu-id="e0038-104">This article shows you how tooupload your own generalized VM image as a virtual hard disk (VHD) so you can use it toocreate virtual machines.</span></span> <span data-ttu-id="e0038-105">Pour en savoir plus sur les disques et les disques durs virtuels dans Microsoft Azure, consultez [À propos des disques et VHD pour machines virtuelles](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e0038-105">For more details about disks and VHDs in Microsoft Azure, see [About Disks and VHDs for Virtual Machines](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0038-106">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e0038-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e0038-107">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="e0038-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="e0038-108">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="e0038-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="e0038-109">Vous pouvez également [télécharger](../upload-generalized-managed.md) un ordinateur virtuel à l’aide du modèle de gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="e0038-109">You can also [upload](../upload-generalized-managed.md) a virtual machine using hello Resource Manager model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0038-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e0038-110">Prerequisites</span></span>
<span data-ttu-id="e0038-111">Cet article suppose que vous disposez de :</span><span class="sxs-lookup"><span data-stu-id="e0038-111">This article assumes you have:</span></span>

* <span data-ttu-id="e0038-112">**Un abonnement Azure** : si vous n’en avez pas, vous pouvez [ouvrir un compte Azure gratuitement](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="e0038-112">**An Azure subscription** - If you don't have one, you can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
* <span data-ttu-id="e0038-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)**  -vous avez hello Microsoft Azure PowerShell module installé et configuré toouse votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="e0038-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)** - You have hello Microsoft Azure PowerShell module installed and configured toouse your subscription.</span></span>
* <span data-ttu-id="e0038-114">**UN FICHIER. Fichier de disque dur virtuel** - Windows pris en charge stocké dans un fichier .vhd et les joint tooa virtual machine de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="e0038-114">**A .VHD file** - supported Windows operating system stored in a .vhd file and attached tooa virtual machine.</span></span> <span data-ttu-id="e0038-115">Vérifiez toosee si les rôles de serveur hello en cours d’exécution sur le disque dur virtuel de hello sont pris en charge par Sysprep.</span><span class="sxs-lookup"><span data-stu-id="e0038-115">Check toosee if hello server roles running on hello VHD are supported by Sysprep.</span></span> <span data-ttu-id="e0038-116">Pour plus d’informations, consultez [Prise en charge de Sysprep pour les rôles serveur](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="e0038-116">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e0038-117">format VHDX Hello n’est pas pris en charge dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e0038-117">hello VHDX format is not supported in Microsoft Azure.</span></span> <span data-ttu-id="e0038-118">Vous pouvez convertir le format de tooVHD hello disque à l’aide du Gestionnaire Hyper-V ou hello [applet de commande Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0038-118">You can convert hello disk tooVHD format using Hyper-V Manager or hello [Convert-VHD cmdlet](http://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="e0038-119">Pour plus de détail, voir [ce billet de blog](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0038-119">For details, see this [blogpost](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span></span>

## <a name="step-1-prep-hello-vhd"></a><span data-ttu-id="e0038-120">Étape 1 : Préparer un disque dur virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="e0038-120">Step 1: Prep hello VHD</span></span>
<span data-ttu-id="e0038-121">Avant de télécharger tooAzure de disque dur virtuel hello, il doit toobe généralisé à l’aide de l’outil Sysprep hello.</span><span class="sxs-lookup"><span data-stu-id="e0038-121">Before you upload hello VHD tooAzure, it needs toobe generalized by using hello Sysprep tool.</span></span> <span data-ttu-id="e0038-122">Elle prépare hello toobe de disque dur virtuel utilisé en tant qu’image.</span><span class="sxs-lookup"><span data-stu-id="e0038-122">This prepares hello VHD toobe used as an image.</span></span> <span data-ttu-id="e0038-123">Pour plus d’informations sur Sysprep, consultez [comment tooUse Sysprep : Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0038-123">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span> <span data-ttu-id="e0038-124">Sauvegardez hello machine virtuelle avant d’exécuter Sysprep.</span><span class="sxs-lookup"><span data-stu-id="e0038-124">Back up hello VM before running Sysprep.</span></span>

<span data-ttu-id="e0038-125">Machine virtuelle hello hello du système d’exploitation a été installé pour terminer hello procédure :</span><span class="sxs-lookup"><span data-stu-id="e0038-125">From hello virtual machine that hello operating system was installed to, complete hello following procedure:</span></span>

1. <span data-ttu-id="e0038-126">Système d’exploitation de toohello vous connecter.</span><span class="sxs-lookup"><span data-stu-id="e0038-126">Sign in toohello operating system.</span></span>
2. <span data-ttu-id="e0038-127">Ouvrez une fenêtre d’invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="e0038-127">Open a command prompt window as an administrator.</span></span> <span data-ttu-id="e0038-128">Basculez hello trop**%windir%\system32\sysprep**, puis exécutez `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="e0038-128">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>

    ![Ouvrir une fenêtre d’invite de commandes](./media/createupload-vhd/sysprep_commandprompt.png)
3. <span data-ttu-id="e0038-130">Hello **outil de préparation système** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="e0038-130">hello **System Preparation Tool** dialog box appears.</span></span>

   ![Démarrer Sysprep](./media/createupload-vhd/sysprepgeneral.png)
4. <span data-ttu-id="e0038-132">Bonjour **outil de préparation système**, sélectionnez **Entrez système boîte expérience OOBE (Out of)** et assurez-vous que **Generalize** est activée.</span><span class="sxs-lookup"><span data-stu-id="e0038-132">In hello **System Preparation Tool**, select **Enter System Out of Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span>
5. <span data-ttu-id="e0038-133">Dans **Options d’arrêt**, sélectionnez **Arrêter**.</span><span class="sxs-lookup"><span data-stu-id="e0038-133">In **Shutdown Options**, select **Shutdown**.</span></span>
6. <span data-ttu-id="e0038-134">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e0038-134">Click **OK**.</span></span>

## <a name="step-2-create-a-storage-account-and-a-container"></a><span data-ttu-id="e0038-135">Étape 2 : Créer un compte de stockage et un conteneur</span><span class="sxs-lookup"><span data-stu-id="e0038-135">Step 2: Create a storage account and a container</span></span>
<span data-ttu-id="e0038-136">Vous avez besoin d’un compte de stockage dans Azure afin que vous ayez un fichier .vhd de place tooupload hello.</span><span class="sxs-lookup"><span data-stu-id="e0038-136">You need a storage account in Azure so you have a place tooupload hello .vhd file.</span></span> <span data-ttu-id="e0038-137">Cette étape vous montre comment toocreate un compte ou get hello info vous avez besoin d’un compte existant.</span><span class="sxs-lookup"><span data-stu-id="e0038-137">This step shows you how toocreate an account, or get hello info you need from an existing account.</span></span> <span data-ttu-id="e0038-138">Remplacer les variables hello dans &lsaquo; crochets &rsaquo; avec vos propres informations.</span><span class="sxs-lookup"><span data-stu-id="e0038-138">Replace hello variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

1. <span data-ttu-id="e0038-139">Connexion</span><span class="sxs-lookup"><span data-stu-id="e0038-139">Login</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="e0038-140">Définissez votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="e0038-140">Set your Azure subscription.</span></span>

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. <span data-ttu-id="e0038-141">Créez un nouveau compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="e0038-141">Create a new storage account.</span></span> <span data-ttu-id="e0038-142">nom Hello hello du compte de stockage doit être unique, 3 et 24 caractères.</span><span class="sxs-lookup"><span data-stu-id="e0038-142">hello name of hello storage account should be unique, 3-24 characters.</span></span> <span data-ttu-id="e0038-143">nom de Hello peut être n’importe quelle combinaison de lettres et chiffres.</span><span class="sxs-lookup"><span data-stu-id="e0038-143">hello name can be any combination of letters and numbers.</span></span> <span data-ttu-id="e0038-144">Vous devez également toospecify un emplacement comme « East US »</span><span class="sxs-lookup"><span data-stu-id="e0038-144">You also need toospecify a location like "East US"</span></span>

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. <span data-ttu-id="e0038-145">Définir le nouveau compte de stockage hello comme valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="e0038-145">Set hello new storage account as hello default.</span></span>

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. <span data-ttu-id="e0038-146">Créez un conteneur.</span><span class="sxs-lookup"><span data-stu-id="e0038-146">Create a new container.</span></span>

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-hello-vhd-file"></a><span data-ttu-id="e0038-147">Étape 3 : Téléchargez le fichier .vhd de hello</span><span class="sxs-lookup"><span data-stu-id="e0038-147">Step 3: Upload hello .vhd file</span></span>
<span data-ttu-id="e0038-148">Hello d’utilisation [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) hello de tooupload disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="e0038-148">Use hello [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) tooupload hello VHD.</span></span>

<span data-ttu-id="e0038-149">À partir de la fenêtre d’Azure PowerShell hello utilisé à l’étape précédente de hello, tapez ce qui suit hello commande et remplacer les variables hello dans &lsaquo; crochets &rsaquo; avec vos propres informations.</span><span class="sxs-lookup"><span data-stu-id="e0038-149">From hello Azure PowerShell window you used in hello previous step, type hello following command and replace hello variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-hello-image-tooyour-list-of-custom-images"></a><span data-ttu-id="e0038-150">Étape 4 : Ajouter la liste de tooyour image hello d’images personnalisées</span><span class="sxs-lookup"><span data-stu-id="e0038-150">Step 4: Add hello image tooyour list of custom images</span></span>
<span data-ttu-id="e0038-151">Hello d’utilisation [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) applet de commande tooadd hello toohello liste d’images vos images personnalisées.</span><span class="sxs-lookup"><span data-stu-id="e0038-151">Use hello [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) cmdlet tooadd hello image toohello list of your custom images.</span></span>

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a><span data-ttu-id="e0038-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e0038-152">Next steps</span></span>
<span data-ttu-id="e0038-153">Vous pouvez désormais [créer une machine virtuelle personnalisée](createportal.md) vous avez téléchargée à l’aide de hello l’image.</span><span class="sxs-lookup"><span data-stu-id="e0038-153">You can now [create a custom VM](createportal.md) using hello image you uploaded.</span></span>
