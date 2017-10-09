---
title: "définit des aaaDeploy une application sur l’échelle de machines virtuelles"
description: Utiliser des extensions toodepoy une application sur Azure, machines virtuelles identiques.
services: virtual-machine-scale-sets
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8892199-f2e2-4b82-988a-28ca8a7fd1eb
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: 5f3988b9511d80370a8be1fc042c21fee212506e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a><span data-ttu-id="59c81-103">Déployer votre application sur des groupes de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="59c81-103">Deploy your application on virtual machine scale sets</span></span>

<span data-ttu-id="59c81-104">Cet article décrit les différentes façons de définition de logiciel tooinstall hello hello temporel est configuré.</span><span class="sxs-lookup"><span data-stu-id="59c81-104">This article describes different ways of how tooinstall software at hello time hello scale set is provisioned.</span></span>

<span data-ttu-id="59c81-105">Vous souhaiterez peut-être tooreview hello [échelle Set conception Overview](virtual-machine-scale-sets-design-overview.md) article, qui décrit quelques-unes des hello les limites imposées par les machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="59c81-105">You may want tooreview hello [Scale Set Design Overview](virtual-machine-scale-sets-design-overview.md) article, which describes some of hello limits imposed by virtual machine scale sets.</span></span>

## <a name="capture-and-reuse-an-image"></a><span data-ttu-id="59c81-106">Capturer et réutiliser une image</span><span class="sxs-lookup"><span data-stu-id="59c81-106">Capture and reuse an image</span></span>

<span data-ttu-id="59c81-107">Vous pouvez utiliser un ordinateur virtuel que vous avez dans Azure tooprepare une image de base pour votre échelle défini.</span><span class="sxs-lookup"><span data-stu-id="59c81-107">You can use a virtual machine you have in Azure tooprepare a base-image for your scale set.</span></span> <span data-ttu-id="59c81-108">Ce processus crée un disque géré dans votre compte de stockage, vous pouvez faire référence en tant qu’image de base hello pour votre jeu de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="59c81-108">This process creates a managed disk in your storage account, which you can reference as hello base image for your scale set.</span></span> 

<span data-ttu-id="59c81-109">Hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="59c81-109">Do hello following steps:</span></span>

1. <span data-ttu-id="59c81-110">Créer une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="59c81-110">Create an Azure Virtual Machine</span></span>
   * <span data-ttu-id="59c81-111">[Linux][linux-vm-create]</span><span class="sxs-lookup"><span data-stu-id="59c81-111">[Linux][linux-vm-create]</span></span>
   * <span data-ttu-id="59c81-112">[Windows][windows-vm-create]</span><span class="sxs-lookup"><span data-stu-id="59c81-112">[Windows][windows-vm-create]</span></span>

2. <span data-ttu-id="59c81-113">À distance dans hello de machine virtuelle et de personnaliser les besoins de tooyour système hello.</span><span class="sxs-lookup"><span data-stu-id="59c81-113">Remote into hello virtual machine and customize hello system tooyour liking.</span></span>

   <span data-ttu-id="59c81-114">Si vous le souhaitez, vous pouvez installer votre application maintenant.</span><span class="sxs-lookup"><span data-stu-id="59c81-114">If you want, you can install your application now.</span></span> <span data-ttu-id="59c81-115">Toutefois, sachez que par l’installation de votre application maintenant, vous pouvez effectuer de mise à niveau de votre application plus complexe, car vous devrez peut-être tooremove il premier.</span><span class="sxs-lookup"><span data-stu-id="59c81-115">However, know that by installing your application now, you may make upgrading your application more complicated because you may need tooremove it first.</span></span> <span data-ttu-id="59c81-116">Au lieu de cela, vous pouvez utiliser cette tooinstall étape les conditions préalables que votre application peut avoir besoin, comme une fonctionnalité spécifique de l’exécution ou le système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="59c81-116">Instead, you can use this step tooinstall any prerequisites your application may need, like a specific runtime or operating system feature.</span></span>

3. <span data-ttu-id="59c81-117">Suivez hello « capturer une machine » didacticiel pour soit [Linux] [ linux-vm-capture] ou [Windows][windows-vm-capture].</span><span class="sxs-lookup"><span data-stu-id="59c81-117">Follow hello "capture a machine" tutorial for either [Linux][linux-vm-capture] or [Windows][windows-vm-capture].</span></span>

4. <span data-ttu-id="59c81-118">Créer un [ensemble d’échelle de Machine virtuelle] [ vmss-create] avec hello image URI que vous avez capturée dans l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="59c81-118">Create a [Virtual Machine Scale Set][vmss-create] with hello image URI you captured in hello previous step.</span></span>

<span data-ttu-id="59c81-119">Pour plus d’informations sur les disques, consultez [Vue d’ensemble de Managed Disks](../virtual-machines/windows/managed-disks-overview.md) et [Utiliser des disques de données attachés](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="59c81-119">For more information about disks, see [Managed Disks Overview](../virtual-machines/windows/managed-disks-overview.md) and [Use Attached Data Disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

## <a name="install-when-hello-scale-set-is-provisioned"></a><span data-ttu-id="59c81-120">Installer lors de la configuration de l’ensemble d’échelle hello</span><span class="sxs-lookup"><span data-stu-id="59c81-120">Install when hello scale set is provisioned</span></span>

<span data-ttu-id="59c81-121">Extensions de machine virtuelle peuvent être appliqué tooa machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="59c81-121">Virtual machine extensions can be applied tooa virtual machine scale set.</span></span> <span data-ttu-id="59c81-122">Avec une extension de machine virtuelle, vous pouvez personnaliser des machines virtuelles de hello dans une échelle définie en tant qu’ensemble d’un groupe.</span><span class="sxs-lookup"><span data-stu-id="59c81-122">With a virtual machine extension, you can customize hello virtual machines in a scale set as a whole group.</span></span> <span data-ttu-id="59c81-123">Pour plus d’informations sur les extensions, consultez [Extensions de machine virtuelle](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="59c81-123">For more information about extensions, see [Virtual Machine Extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="59c81-124">Il existe trois extensions principales que vous pouvez utiliser, selon que votre système d’exploitation est Linux ou Windows.</span><span class="sxs-lookup"><span data-stu-id="59c81-124">There are three main extensions you can use, depending on if your operating system is Linux-based or Windows-based.</span></span>

### <a name="windows"></a><span data-ttu-id="59c81-125">Windows</span><span class="sxs-lookup"><span data-stu-id="59c81-125">Windows</span></span>

<span data-ttu-id="59c81-126">Pour un système d’exploitation Windows, utilisez soit hello **Script personnalisé v1.8** extension ou hello **DSC PowerShell** extension.</span><span class="sxs-lookup"><span data-stu-id="59c81-126">For a Windows-based operating system, use either hello **Custom Script v1.8** extension, or hello **PowerShell DSC** extension.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="59c81-127">Script personnalisé</span><span class="sxs-lookup"><span data-stu-id="59c81-127">Custom Script</span></span>

<span data-ttu-id="59c81-128">extension de Script personnalisé de Hello exécute un script sur chaque instance de machine virtuelle dans un ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="59c81-128">hello Custom Script extension runs a script on each virtual machine instance in hello scale set.</span></span> <span data-ttu-id="59c81-129">Un fichier de configuration ou une variable indique quels fichiers sont téléchargés toohello virtual machine, puis quelle commande s’exécute.</span><span class="sxs-lookup"><span data-stu-id="59c81-129">A config file or variable indicates which files are downloaded toohello virtual machine, and then what command runs.</span></span> <span data-ttu-id="59c81-130">Vous pouvez par exemple utiliser cette toorun un programme d’installation, un script, un fichier de commandes, tout fichier exécutable.</span><span class="sxs-lookup"><span data-stu-id="59c81-130">You could use this toorun an installer, a script, a batch file, any executable for example.</span></span>

<span data-ttu-id="59c81-131">PowerShell utilise une table de hachage pour les paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="59c81-131">PowerShell uses a hashtable for hello settings.</span></span> <span data-ttu-id="59c81-132">Cet exemple configure toorun extension de script personnalisé hello un script PowerShell qui installe les services IIS.</span><span class="sxs-lookup"><span data-stu-id="59c81-132">This example configures hello custom script extension toorun a PowerShell script that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="59c81-133">Hello d’utilisation `-ProtectedSetting` basculer pour tous les paramètres qui contiennent des informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="59c81-133">Use hello `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

---------


<span data-ttu-id="59c81-134">Azure CLI utilise un fichier json pour les paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="59c81-134">Azure CLI uses a json file for hello settings.</span></span> <span data-ttu-id="59c81-135">Cet exemple configure toorun extension de script personnalisé hello un script PowerShell qui installe les services IIS.</span><span class="sxs-lookup"><span data-stu-id="59c81-135">This example configures hello custom script extension toorun a PowerShell script that installs IIS.</span></span> <span data-ttu-id="59c81-136">Enregistrer hello en tant que le fichier json suivant _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="59c81-136">Save hello following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

<span data-ttu-id="59c81-137">Ensuite, exécutez cette commande Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="59c81-137">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="59c81-138">Hello d’utilisation `--protected-settings` basculer pour tous les paramètres qui contiennent des informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="59c81-138">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="powershell-dsc"></a><span data-ttu-id="59c81-139">DSC PowerShell</span><span class="sxs-lookup"><span data-stu-id="59c81-139">PowerShell DSC</span></span>

<span data-ttu-id="59c81-140">Vous pouvez utiliser des instances de machine virtuelle DSC PowerShell toocustomize hello échelle ensemble.</span><span class="sxs-lookup"><span data-stu-id="59c81-140">You can use PowerShell DSC toocustomize hello scale set vm instances.</span></span> <span data-ttu-id="59c81-141">Hello **DSC** extension publié par **Microsoft.Powershell** déploie et exécute la configuration DSC de hello fourni sur chaque instance de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="59c81-141">hello **DSC** extension published by **Microsoft.Powershell** deploys and runs hello provided DSC configuration on each virtual machine instance.</span></span> <span data-ttu-id="59c81-142">Un fichier de configuration ou une variable indique l’extension de hello où *.zip* package est et qui _fonction de script_ toorun de combinaison.</span><span class="sxs-lookup"><span data-stu-id="59c81-142">A config file or variable tells hello extension where *.zip* package is, and which _script-function_ combination toorun.</span></span>

<span data-ttu-id="59c81-143">PowerShell utilise une table de hachage pour les paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="59c81-143">PowerShell uses a hashtable for hello settings.</span></span> <span data-ttu-id="59c81-144">Cet exemple déploie un package DSC qui installe IIS.</span><span class="sxs-lookup"><span data-stu-id="59c81-144">This example deploys a DSC package that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$dscConfig = @{
  "wmfVersion" = "latest";
  "configuration" = @{
    "url" = "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip";
    "script" = "configure-http.ps1";
    "function" = "WebsiteTest";
  };
}

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="59c81-145">Hello d’utilisation `-ProtectedSetting` basculer pour tous les paramètres qui contiennent des informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="59c81-145">Use hello `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

-----------

<span data-ttu-id="59c81-146">CLI Azure utilise json pour les paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="59c81-146">Azure CLI uses a json for hello settings.</span></span> <span data-ttu-id="59c81-147">Cet exemple déploie un package DSC qui installe IIS.</span><span class="sxs-lookup"><span data-stu-id="59c81-147">This example deploys a DSC package that installs IIS.</span></span> <span data-ttu-id="59c81-148">Enregistrer hello en tant que le fichier json suivant _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="59c81-148">Save hello following json file as _settings.json_.</span></span>

```json
{
  "wmfVersion": "latest",
  "configuration": {
    "url": "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip",
    "script": "configure-http.ps1",
    "function": "WebsiteTest"
  }
}
```

<span data-ttu-id="59c81-149">Ensuite, exécutez cette commande Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="59c81-149">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="59c81-150">Hello d’utilisation `--protected-settings` basculer pour tous les paramètres qui contiennent des informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="59c81-150">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="linux"></a><span data-ttu-id="59c81-151">Linux</span><span class="sxs-lookup"><span data-stu-id="59c81-151">Linux</span></span>

<span data-ttu-id="59c81-152">Linux permettre utiliser soit hello **Script personnalisé v2.0** extension ou utilisez **cloud-init** lors de la création.</span><span class="sxs-lookup"><span data-stu-id="59c81-152">Linux can use either hello **Custom Script v2.0** extension or use **cloud-init** during creation.</span></span>

<span data-ttu-id="59c81-153">Script personnalisé est une extension simple qui télécharge les instances de machine virtuelle toohello de fichiers et exécute une commande.</span><span class="sxs-lookup"><span data-stu-id="59c81-153">Custom script is a simple extension that downloads files toohello virtual machine instances, and runs a command.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="59c81-154">Script personnalisé</span><span class="sxs-lookup"><span data-stu-id="59c81-154">Custom Script</span></span>

<span data-ttu-id="59c81-155">Enregistrer hello en tant que le fichier json suivant _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="59c81-155">Save hello following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

<span data-ttu-id="59c81-156">Utilisez hello CLI d’Azure tooadd cette tooan extension existante de machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="59c81-156">Use hello Azure CLI tooadd this extension tooan existing virtual machine scale set.</span></span> <span data-ttu-id="59c81-157">Chaque ordinateur virtuel dans l’échelle de hello définir automatiquement s’exécute hello extension.</span><span class="sxs-lookup"><span data-stu-id="59c81-157">Each virtual machine in hello scale set automatically runs hello extension.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="59c81-158">Hello d’utilisation `--protected-settings` basculer pour tous les paramètres qui contiennent des informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="59c81-158">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

#### <a name="cloud-init"></a><span data-ttu-id="59c81-159">Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="59c81-159">Cloud-Init</span></span>

<span data-ttu-id="59c81-160">Init-cloud est utilisée lors de la création d’un ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="59c81-160">Cloud-Init is used when hello scale set is created.</span></span> <span data-ttu-id="59c81-161">Commencez par créer un fichier local nommé _cloud-init.txt_ et ajoutez votre tooit de configuration.</span><span class="sxs-lookup"><span data-stu-id="59c81-161">First, create a local file named _cloud-init.txt_ and add your configuration tooit.</span></span> <span data-ttu-id="59c81-162">Par exemple, consultez [ce Gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span><span class="sxs-lookup"><span data-stu-id="59c81-162">For example, see [this gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span></span>

<span data-ttu-id="59c81-163">Hello d’utiliser Azure CLI toocreate une échelle définie.</span><span class="sxs-lookup"><span data-stu-id="59c81-163">Use hello Azure CLI toocreate a scale set.</span></span> <span data-ttu-id="59c81-164">Hello `--custom-data` champ accepte le nom de fichier hello d’un script d’initialisation de cloud.</span><span class="sxs-lookup"><span data-stu-id="59c81-164">hello `--custom-data` field accepts hello file name of a cloud-init script.</span></span>

```azurecli
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image Canonical:UbuntuServer:14.04.4-LTS:latest \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

## <a name="how-do-i-manage-application-updates"></a><span data-ttu-id="59c81-165">Comment gérer les mises à jour de l’application ?</span><span class="sxs-lookup"><span data-stu-id="59c81-165">How do I manage application updates?</span></span>

<span data-ttu-id="59c81-166">Si vous avez déployé votre application via une extension, modifiez la définition d’extension hello d’une certaine façon.</span><span class="sxs-lookup"><span data-stu-id="59c81-166">If you deployed your application through an extension, alter hello extension definition in some way.</span></span> <span data-ttu-id="59c81-167">Cette modification entraîne des instances de machine virtuelle tooall hello extension toobe redéployé.</span><span class="sxs-lookup"><span data-stu-id="59c81-167">This change causes hello extension toobe redeployed tooall virtual machine instances.</span></span> <span data-ttu-id="59c81-168">Un élément **doit** être modifié sur l’extension hello, comme le renommage d’un fichier référencé, dans le cas contraire, Azure fait pas les voir qui hello extension a changé.</span><span class="sxs-lookup"><span data-stu-id="59c81-168">Something **must** be changed about hello extension, such as renaming a referenced file, otherwise, Azure does not see that hello extension has changed.</span></span>

<span data-ttu-id="59c81-169">Si l’application hello intégrées de votre propre image de système d’exploitation, utilisez un pipeline de déploiement automatisé des mises à jour de l’application.</span><span class="sxs-lookup"><span data-stu-id="59c81-169">If you baked hello application into your own operating system image, use an automated deployment pipeline for application updates.</span></span> <span data-ttu-id="59c81-170">Concevoir votre toofacilitate architecture rapide le remplacement d’une échelle intermédiaire en production.</span><span class="sxs-lookup"><span data-stu-id="59c81-170">Design your architecture toofacilitate rapid swapping of a staged scale set into production.</span></span> <span data-ttu-id="59c81-171">Un bon exemple de cette approche est hello [fonctionne-t-elle Azure Spinnaker](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span><span class="sxs-lookup"><span data-stu-id="59c81-171">A good example of this approach is hello [Azure Spinnaker driver work](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span></span>

<span data-ttu-id="59c81-172">[Programme de compression](https://www.packer.io/) et [Terraform](https://www.terraform.io/) prise en charge Azure Resource Manager, donc vous pouvez également définir vos images « en tant que code » et les générer dans Azure, puis utiliser hello disque dur virtuel dans votre ensemble d’échelle.</span><span class="sxs-lookup"><span data-stu-id="59c81-172">[Packer](https://www.packer.io/) and [Terraform](https://www.terraform.io/) support Azure Resource Manager, so you can also define your images "as code" and build them in Azure, then use hello VHD in your scale set.</span></span> <span data-ttu-id="59c81-173">Cependant, cette opération devient problématique pour les images de place de marché, pour lesquelles les extensions / scripts personnalisés deviennent plus importants, car vous ne manipulez pas directement les éléments exécutables de la Place de marché.</span><span class="sxs-lookup"><span data-stu-id="59c81-173">However, doing so would become problematic for marketplace images, where extensions/custom scripts become more important since you don’t directly manipulate bits from marketplace.</span></span>

## <a name="what-happens-when-a-scale-set-scales-out"></a><span data-ttu-id="59c81-174">Que se passe-t-il quand le nombre de machines virtuelles d’un groupe de machines virtuelles identiques augmente ?</span><span class="sxs-lookup"><span data-stu-id="59c81-174">What happens when a scale set scales out?</span></span>
<span data-ttu-id="59c81-175">Lorsque vous ajoutez un ou plusieurs ordinateurs virtuels tooa identiques, application hello est installée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="59c81-175">When you add one or more virtual machines tooa scale set, hello application is automatically installed.</span></span> <span data-ttu-id="59c81-176">Pour exemple, si la valeur de l’échelle de hello a extensions définies, ils s’exécuter sur un nouvel ordinateur virtuel chaque fois qu’il est créé.</span><span class="sxs-lookup"><span data-stu-id="59c81-176">For example if hello scale set has extensions defined, they run on a new virtual machine each time it is created.</span></span> <span data-ttu-id="59c81-177">Si l’ensemble d’échelle hello est basé sur une image personnalisée, tout nouvel ordinateur virtuel est une copie de l’image personnalisée de hello source.</span><span class="sxs-lookup"><span data-stu-id="59c81-177">If hello scale set is based on a custom image, any new virtual machine is a copy of hello source custom image.</span></span> <span data-ttu-id="59c81-178">Si hello échelle jeu d’ordinateurs virtuels sont des hôtes de conteneur, peut-être conteneurs de démarrage du code tooload hello dans une Extension de Script personnalisé.</span><span class="sxs-lookup"><span data-stu-id="59c81-178">If hello scale set virtual machines are container hosts, then you might have startup code tooload hello containers in a Custom Script Extension.</span></span> <span data-ttu-id="59c81-179">Une extension peut aussi installer un agent qui s’inscrit auprès d’un orchestrateur de cluster, comme Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="59c81-179">Or, an extension might install an agent that registers with a cluster orchestrator, such as Azure Container Service.</span></span>


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a><span data-ttu-id="59c81-180">Comment déployer une mise à jour du système d’exploitation sur plusieurs domaines de mise à jour ?</span><span class="sxs-lookup"><span data-stu-id="59c81-180">How do you roll out an OS update across update domains?</span></span>
<span data-ttu-id="59c81-181">Supposons que vous tooupdate votre image de système d’exploitation tout en conservant l’échelle de machines virtuelles hello configuré pour s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="59c81-181">Suppose you want tooupdate your OS image while keeping hello virtual machine scale set running.</span></span> <span data-ttu-id="59c81-182">PowerShell et hello CLI d’Azure peuvent mettre à jour des images de machine virtuelle hello, un seul ordinateur virtuel à la fois.</span><span class="sxs-lookup"><span data-stu-id="59c81-182">PowerShell and hello Azure CLI can update hello virtual machine images, one virtual machine at a time.</span></span> <span data-ttu-id="59c81-183">Hello [mise à niveau d’un ensemble d’échelle de Machine virtuelle](./virtual-machine-scale-sets-upgrade-scale-set.md) article fournit également des informations supplémentaires sur les options disponible tooperform mise à niveau du système d’exploitation sur un ensemble d’échelle de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="59c81-183">hello [Upgrade a Virtual Machine Scale Set](./virtual-machine-scale-sets-upgrade-scale-set.md) article also provides further information on what options are available tooperform an operating system upgrade across a virtual machine scale set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59c81-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="59c81-184">Next steps</span></span>

* [<span data-ttu-id="59c81-185">Utilisez PowerShell toomanage votre ensemble d’échelle.</span><span class="sxs-lookup"><span data-stu-id="59c81-185">Use PowerShell toomanage your scale set.</span></span>](virtual-machine-scale-sets-windows-manage.md)
* <span data-ttu-id="59c81-186">[Créez un modèle de groupe identique](virtual-machine-scale-sets-mvss-start.md).</span><span class="sxs-lookup"><span data-stu-id="59c81-186">[Create a scale set template.](virtual-machine-scale-sets-mvss-start.md)</span></span>


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

