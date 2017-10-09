---
title: "aaaCreate et gérer une Azure Machine virtuelle à l’aide de C# | Documents Microsoft"
description: Utiliser c# et Azure Resource Manager toodeploy une machine virtuelle et toutes ses ressources de prise en charge.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 87524373-5f52-4f4b-94af-50bf7b65c277
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 8beeabde731bbaa25e68d2b9c5abbf71acbe377f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a><span data-ttu-id="42380-103">Créer et gérer des machines virtuelles Windows dans Azure à l’aide de C#</span><span class="sxs-lookup"><span data-stu-id="42380-103">Create and manage Windows VMs in Azure using C#</span></span> #

<span data-ttu-id="42380-104">Une [machine virtuelle Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) a besoin de plusieurs ressources de prise en charge Azure.</span><span class="sxs-lookup"><span data-stu-id="42380-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="42380-105">Cet article décrit comment créer, gérer et supprimer des ressources de machine virtuelle à l’aide de C#.</span><span class="sxs-lookup"><span data-stu-id="42380-105">This article covers creating, managing, and deleting VM resources using C#.</span></span> <span data-ttu-id="42380-106">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="42380-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="42380-107">Créer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="42380-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="42380-108">Installer le package de hello</span><span class="sxs-lookup"><span data-stu-id="42380-108">Install hello package</span></span>
> * <span data-ttu-id="42380-109">Créer des informations d’identification</span><span class="sxs-lookup"><span data-stu-id="42380-109">Create credentials</span></span>
> * <span data-ttu-id="42380-110">Créer des ressources</span><span class="sxs-lookup"><span data-stu-id="42380-110">Create resources</span></span>
> * <span data-ttu-id="42380-111">Effectuer les tâches de gestion</span><span class="sxs-lookup"><span data-stu-id="42380-111">Perform management tasks</span></span>
> * <span data-ttu-id="42380-112">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="42380-112">Delete resources</span></span>
> * <span data-ttu-id="42380-113">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="42380-113">Run hello application</span></span>

<span data-ttu-id="42380-114">Il prend environ 20 minutes toodo ces étapes.</span><span class="sxs-lookup"><span data-stu-id="42380-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="42380-115">Créer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="42380-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="42380-116">Si vous ne l’avez pas déjà fait, installez [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="42380-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="42380-117">Sélectionnez **développement de bureau .NET** sur hello page de charges de travail, puis cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="42380-117">Select **.NET desktop development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="42380-118">Bonjour résumé, vous pouvez voir que **outils de développement .NET Framework 4-4.6** est automatiquement sélectionné pour vous.</span><span class="sxs-lookup"><span data-stu-id="42380-118">In hello summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="42380-119">Si vous avez déjà installé Visual Studio, vous pouvez ajouter les charges de travail hello .NET à l’aide de hello du Lanceur de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="42380-119">If you have already installed Visual Studio, you can add hello .NET workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="42380-120">Dans Visual Studio, cliquez sur **Fichier** > **Nouveau** > **Projet**.</span><span class="sxs-lookup"><span data-stu-id="42380-120">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="42380-121">Dans **modèles** > **Visual C#**, sélectionnez **l’application Console (.NET Framework)**, entrez *myDotnetProject* nom hello de Hello du projet, emplacement hello sélectionnez hello du projet d’et puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="42380-121">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-hello-package"></a><span data-ttu-id="42380-122">Installer le package de hello</span><span class="sxs-lookup"><span data-stu-id="42380-122">Install hello package</span></span>

<span data-ttu-id="42380-123">Les packages NuGet sont hello plus simple façon tooinstall hello bibliothèques que vous devez toofinish ces étapes.</span><span class="sxs-lookup"><span data-stu-id="42380-123">NuGet packages are hello easiest way tooinstall hello libraries that you need toofinish these steps.</span></span> <span data-ttu-id="42380-124">bibliothèques hello tooget dont vous avez besoin dans Visual Studio, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="42380-124">tooget hello libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="42380-125">Cliquez sur **Outils** > **Gestionnaire de package NuGet**, puis sur **Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="42380-125">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="42380-126">Tapez la commande suivante dans la console hello :</span><span class="sxs-lookup"><span data-stu-id="42380-126">Type this command in hello console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a><span data-ttu-id="42380-127">Créer des informations d’identification</span><span class="sxs-lookup"><span data-stu-id="42380-127">Create credentials</span></span>

<span data-ttu-id="42380-128">Avant de commencer cette étape, assurez-vous que vous avez accès tooan [principal du service Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="42380-128">Before you start this step, make sure that you have access tooan [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="42380-129">Vous devez également enregistrer les ID de l’application hello, clé d’authentification hello et ID de client hello dont vous avez besoin dans une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="42380-129">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="42380-130">Créer le fichier d’autorisations de hello</span><span class="sxs-lookup"><span data-stu-id="42380-130">Create hello authorization file</span></span>

1. <span data-ttu-id="42380-131">Dans l’Explorateur de solutions, cliquez sur *myDotnetProject* > **Ajouter** > **Nouvel élément**, puis sélectionnez **Fichier texte** dans *Éléments Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="42380-131">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="42380-132">Nom de fichier hello *azureauth.properties*, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="42380-132">Name hello file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="42380-133">Ajoutez ces propriétés d’autorisation :</span><span class="sxs-lookup"><span data-stu-id="42380-133">Add these authorization properties:</span></span>

    ```
    subscription=<subscription-id>
    client=<application-id>
    key=<authentication-key>
    tenant=<tenant-id>
    managementURI=https://management.core.windows.net/
    baseURL=https://management.azure.com/
    authURL=https://login.windows.net/
    graphURL=https://graph.windows.net/
    ```

    <span data-ttu-id="42380-134">Remplacez  **&lt;id d’abonnement&gt;**  avec votre identificateur d’abonnement,  **&lt;id d’application&gt;**  avec hello application Active Directory identificateur,  **&lt;clé d’authentification&gt;**  avec la clé d’application hello, et  **&lt;id de client&gt;**  avec le client de hello identificateur.</span><span class="sxs-lookup"><span data-stu-id="42380-134">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

3. <span data-ttu-id="42380-135">Enregistrez le fichier de azureauth.properties hello.</span><span class="sxs-lookup"><span data-stu-id="42380-135">Save hello azureauth.properties file.</span></span> 
4. <span data-ttu-id="42380-136">Définir une variable d’environnement dans Windows nommé AZURE_AUTH_LOCATION avec les fichiers tooauthorization hello chemin d’accès complet que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="42380-136">Set an environment variable in Windows named AZURE_AUTH_LOCATION with hello full path tooauthorization file that you created.</span></span> <span data-ttu-id="42380-137">Par exemple, hello suivant de commande PowerShell peut être utilisé :</span><span class="sxs-lookup"><span data-stu-id="42380-137">For example, hello following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-hello-management-client"></a><span data-ttu-id="42380-138">Créer le client de gestion hello</span><span class="sxs-lookup"><span data-stu-id="42380-138">Create hello management client</span></span>

1. <span data-ttu-id="42380-139">Ouvrir le fichier Program.cs de hello pour le projet hello que vous avez créé, puis ajoutez-les à l’aide de toohello instructions existantes en haut du fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="42380-139">Open hello Program.cs file for hello project that you created, and then add these using statements toohello existing statements at top of hello file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. <span data-ttu-id="42380-140">client de gestion toocreate hello, ajoutez ce code de toohello méthode Main :</span><span class="sxs-lookup"><span data-stu-id="42380-140">toocreate hello management client, add this code toohello Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a><span data-ttu-id="42380-141">Créer des ressources</span><span class="sxs-lookup"><span data-stu-id="42380-141">Create resources</span></span>

### <a name="create-hello-resource-group"></a><span data-ttu-id="42380-142">Créer le groupe de ressources hello</span><span class="sxs-lookup"><span data-stu-id="42380-142">Create hello resource group</span></span>

<span data-ttu-id="42380-143">Toutes les ressources doivent être contenues dans un [groupe de ressources](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="42380-143">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="42380-144">valeurs toospecify hello application et créer le groupe de ressources hello, ajoutez ce code de toohello méthode Main :</span><span class="sxs-lookup"><span data-stu-id="42380-144">toospecify values for hello application and create hello resource group, add this code toohello Main method:</span></span>

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-hello-availability-set"></a><span data-ttu-id="42380-145">Créer le groupe à haute disponibilité hello</span><span class="sxs-lookup"><span data-stu-id="42380-145">Create hello availability set</span></span>

<span data-ttu-id="42380-146">[Haute disponibilité](tutorial-availability-sets.md) facilitent pour vous toomaintain hello virtuels utilisés par votre application.</span><span class="sxs-lookup"><span data-stu-id="42380-146">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

<span data-ttu-id="42380-147">disponibilité de hello toocreate définie, ajoutez ce code de toohello méthode Main :</span><span class="sxs-lookup"><span data-stu-id="42380-147">toocreate hello availability set, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-hello-public-ip-address"></a><span data-ttu-id="42380-148">Créer une adresse IP publique hello</span><span class="sxs-lookup"><span data-stu-id="42380-148">Create hello public IP address</span></span>

<span data-ttu-id="42380-149">A [adresse IP publique](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) est toocommunicate nécessaire avec l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="42380-149">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

<span data-ttu-id="42380-150">toocreate hello adresse IP publique pour l’ordinateur virtuel de hello, ajoutez ce code de toohello méthode Main :</span><span class="sxs-lookup"><span data-stu-id="42380-150">toocreate hello public IP address for hello virtual machine, add this code toohello Main method:</span></span>
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-hello-virtual-network"></a><span data-ttu-id="42380-151">Créer le réseau virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="42380-151">Create hello virtual network</span></span>

<span data-ttu-id="42380-152">Une machine virtuelle doit être incluse dans un sous-réseau d’un [réseau virtuel](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="42380-152">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="42380-153">toocreate un sous-réseau et un réseau virtuel, ajoutez ce code de toohello méthode Main :</span><span class="sxs-lookup"><span data-stu-id="42380-153">toocreate a subnet and a virtual network, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-hello-network-interface"></a><span data-ttu-id="42380-154">Créer l’interface de réseau hello</span><span class="sxs-lookup"><span data-stu-id="42380-154">Create hello network interface</span></span>

<span data-ttu-id="42380-155">Un ordinateur virtuel doit un toocommunicate d’interface réseau sur le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="42380-155">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

<span data-ttu-id="42380-156">toocreate une interface réseau, ajoutez ce code de toohello méthode Main :</span><span class="sxs-lookup"><span data-stu-id="42380-156">toocreate a network interface, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating network interface...");
var networkInterface = azure.NetworkInterfaces.Define("myNIC")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetwork(network)
    .WithSubnet("mySubnet")
    .WithPrimaryPrivateIPAddressDynamic()
    .WithExistingPrimaryPublicIPAddress(publicIPAddress)
    .Create();
 ```

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="42380-157">Créer la machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="42380-157">Create hello virtual machine</span></span>

<span data-ttu-id="42380-158">Maintenant que vous avez créé hello toutes les ressources de support, vous pouvez créer un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="42380-158">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="42380-159">toocreate hello d’ordinateur virtuel, ajoutez ce code de toohello méthode Main :</span><span class="sxs-lookup"><span data-stu-id="42380-159">toocreate hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating virtual machine...");
azure.VirtualMachines.Define(vmName)
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .WithAdminUsername("azureuser")
    .WithAdminPassword("Azure12345678")
    .WithComputerName(vmName)
    .WithExistingAvailabilitySet(availabilitySet)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

> [!NOTE]
> <span data-ttu-id="42380-160">Ce didacticiel crée une machine virtuelle exécutant une version du système d’exploitation de serveur Windows hello.</span><span class="sxs-lookup"><span data-stu-id="42380-160">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="42380-161">toolearn plus sur la sélection d’autres images, consultez [naviguer et sélectionnez les images de machine virtuelle Azure avec Windows PowerShell et hello CLI d’Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="42380-161">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="42380-162">Si vous voulez toouse un disque existant au lieu d’une image de marketplace, utilisez ce code :</span><span class="sxs-lookup"><span data-stu-id="42380-162">If you want toouse an existing disk instead of a marketplace image, use this code:</span></span>

```
var managedDisk = azure.Disks.Define("myosdisk")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithWindowsFromVhd("https://mystorage.blob.core.windows.net/vhds/myosdisk.vhd")
    .WithSizeInGB(128)
    .WithSku(DiskSkuTypes.PremiumLRS)
    .Create();

azure.VirtualMachines.Define("myVM")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithSpecializedOSDisk(managedDisk, OperatingSystemTypes.Windows)
    .WithExistingAvailabilitySet(availabilitySet)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

## <a name="perform-management-tasks"></a><span data-ttu-id="42380-163">Effectuer les tâches de gestion</span><span class="sxs-lookup"><span data-stu-id="42380-163">Perform management tasks</span></span>

<span data-ttu-id="42380-164">Au cours de hello du cycle de vie d’un ordinateur virtuel, vous souhaiterez toorun des tâches de gestion telles que le démarrage, arrêt ou suppression d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="42380-164">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="42380-165">En outre, vous souhaiterez toocreate tooautomate répétitives ou complexes des tâches de code.</span><span class="sxs-lookup"><span data-stu-id="42380-165">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

<span data-ttu-id="42380-166">Lorsque vous devez toodo quoi que ce soit par hello machine virtuelle, vous devez tooget une instance de celui-ci :</span><span class="sxs-lookup"><span data-stu-id="42380-166">When you need toodo anything with hello VM, you need tooget an instance of it:</span></span>

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="42380-167">Obtenir des informations sur la machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="42380-167">Get information about hello VM</span></span>

<span data-ttu-id="42380-168">tooget plus d’informations sur la machine virtuelle de hello, ajoutez ce code de toohello méthode Main :</span><span class="sxs-lookup"><span data-stu-id="42380-168">tooget information about hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Getting information about hello virtual machine...");
Console.WriteLine("hardwareProfile");
Console.WriteLine("   vmSize: " + vm.Size);
Console.WriteLine("storageProfile");
Console.WriteLine("  imageReference");
Console.WriteLine("    publisher: " + vm.StorageProfile.ImageReference.Publisher);
Console.WriteLine("    offer: " + vm.StorageProfile.ImageReference.Offer);
Console.WriteLine("    sku: " + vm.StorageProfile.ImageReference.Sku);
Console.WriteLine("    version: " + vm.StorageProfile.ImageReference.Version);
Console.WriteLine("  osDisk");
Console.WriteLine("    osType: " + vm.StorageProfile.OsDisk.OsType);
Console.WriteLine("    name: " + vm.StorageProfile.OsDisk.Name);
Console.WriteLine("    createOption: " + vm.StorageProfile.OsDisk.CreateOption);
Console.WriteLine("    caching: " + vm.StorageProfile.OsDisk.Caching);
Console.WriteLine("osProfile");
Console.WriteLine("  computerName: " + vm.OSProfile.ComputerName);
Console.WriteLine("  adminUsername: " + vm.OSProfile.AdminUsername);
Console.WriteLine("  provisionVMAgent: " + vm.OSProfile.WindowsConfiguration.ProvisionVMAgent.Value);
Console.WriteLine("  enableAutomaticUpdates: " + vm.OSProfile.WindowsConfiguration.EnableAutomaticUpdates.Value);
Console.WriteLine("networkProfile");
foreach (string nicId in vm.NetworkInterfaceIds)
{
    Console.WriteLine("  networkInterface id: " + nicId);
}
Console.WriteLine("vmAgent");
Console.WriteLine("  vmAgentVersion" + vm.InstanceView.VmAgent.VmAgentVersion);
Console.WriteLine("    statuses");
foreach (InstanceViewStatus stat in vm.InstanceView.VmAgent.Statuses)
{
    Console.WriteLine("    code: " + stat.Code);
    Console.WriteLine("    level: " + stat.Level);
    Console.WriteLine("    displayStatus: " + stat.DisplayStatus);
    Console.WriteLine("    message: " + stat.Message);
    Console.WriteLine("    time: " + stat.Time);
}
Console.WriteLine("disks");
foreach (DiskInstanceView disk in vm.InstanceView.Disks)
{
    Console.WriteLine("  name: " + disk.Name);
    Console.WriteLine("  statuses");
    foreach (InstanceViewStatus stat in disk.Statuses)
    {
        Console.WriteLine("    code: " + stat.Code);
        Console.WriteLine("    level: " + stat.Level);
        Console.WriteLine("    displayStatus: " + stat.DisplayStatus);
        Console.WriteLine("    time: " + stat.Time);
    }
}
Console.WriteLine("VM general status");
Console.WriteLine("  provisioningStatus: " + vm.ProvisioningState);
Console.WriteLine("  id: " + vm.Id);
Console.WriteLine("  name: " + vm.Name);
Console.WriteLine("  type: " + vm.Type);
Console.WriteLine("  location: " + vm.Region);
Console.WriteLine("VM instance status");
foreach (InstanceViewStatus stat in vm.InstanceView.Statuses)
{
    Console.WriteLine("  code: " + stat.Code);
    Console.WriteLine("  level: " + stat.Level);
    Console.WriteLine("  displayStatus: " + stat.DisplayStatus);
}
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="stop-hello-vm"></a><span data-ttu-id="42380-169">Arrêter hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="42380-169">Stop hello VM</span></span>

<span data-ttu-id="42380-170">Vous pouvez arrêter une machine virtuelle et conserver tous ses paramètres, mais continuer toobe facturé pour celui-ci, ou vous pouvez arrêter une machine virtuelle et désallouer.</span><span class="sxs-lookup"><span data-stu-id="42380-170">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="42380-171">Lorsqu’une machine virtuelle est libérée, toutes les ressources qui lui sont associées sont également libérées et la facturation de la machine virtuelle prend fin.</span><span class="sxs-lookup"><span data-stu-id="42380-171">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="42380-172">toostop hello virtual machine sans le désallouer, ajoutez ce code de toohello méthode Main :</span><span class="sxs-lookup"><span data-stu-id="42380-172">toostop hello virtual machine without deallocating it, add this code toohello Main method:</span></span>

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

<span data-ttu-id="42380-173">Si vous voulez toodeallocate hello virtual machine, modifier le code de toothis d’appel hello hors tension :</span><span class="sxs-lookup"><span data-stu-id="42380-173">If you want toodeallocate hello virtual machine, change hello PowerOff call toothis code:</span></span>

```
vm.Deallocate();
```

### <a name="start-hello-vm"></a><span data-ttu-id="42380-174">Démarrer hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="42380-174">Start hello VM</span></span>

<span data-ttu-id="42380-175">toostart hello d’ordinateur virtuel, ajoutez ce code de toohello méthode Main :</span><span class="sxs-lookup"><span data-stu-id="42380-175">toostart hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="resize-hello-vm"></a><span data-ttu-id="42380-176">Redimensionner hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="42380-176">Resize hello VM</span></span>

<span data-ttu-id="42380-177">De nombreux aspects du déploiement doivent être pris en considération lors du choix d’une taille pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="42380-177">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="42380-178">Pour plus d’informations, voir [Tailles des machines virtuelles](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="42380-178">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="42380-179">taille toochange de machine virtuelle de hello, ajoutez ce code de toohello méthode Main :</span><span class="sxs-lookup"><span data-stu-id="42380-179">toochange size of hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="42380-180">Ajouter un toohello de disque de données machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="42380-180">Add a data disk toohello VM</span></span>

<span data-ttu-id="42380-181">tooadd un ordinateur virtuel des toohello du disque de données, ajoutez ce principal de code toohello méthode tooadd un disque de données est de 2 Go de taille, han un numéro d’unité logique de 0 et un type de mise en cache de lecture/écriture :</span><span class="sxs-lookup"><span data-stu-id="42380-181">tooadd a data disk toohello virtual machine, add this code toohello Main method tooadd a data disk that is 2 GB in size, han a LUN of 0 and a caching type of ReadWrite:</span></span>

```
Console.WriteLine("Adding data disk toovm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter toodelete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a><span data-ttu-id="42380-182">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="42380-182">Delete resources</span></span>

<span data-ttu-id="42380-183">Vous êtes facturé pour les ressources utilisées dans Azure, il est toujours ressources toodelete bonnes pratiques qui ne sont plus nécessaires.</span><span class="sxs-lookup"><span data-stu-id="42380-183">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="42380-184">Si vous souhaitez toodelete hello virtual machines et hello toutes les ressources de support, toutes les toodo est hello supprimer le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="42380-184">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

<span data-ttu-id="42380-185">ressource de hello toodelete groupe, ajoutez ce code de toohello méthode Main :</span><span class="sxs-lookup"><span data-stu-id="42380-185">toodelete hello resource group, add this code toohello Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a><span data-ttu-id="42380-186">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="42380-186">Run hello application</span></span>

<span data-ttu-id="42380-187">Il doit prendre environ cinq minutes pour que cette toorun d’application console complètement à partir de toofinish de début.</span><span class="sxs-lookup"><span data-stu-id="42380-187">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> 

1. <span data-ttu-id="42380-188">application de console toorun hello, cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="42380-188">toorun hello console application, click **Start**.</span></span>

2. <span data-ttu-id="42380-189">Avant d’appuyer sur **entrée** toostart suppression des ressources, vous pouvez prendre quelques minutes la création de hello tooverify des ressources de hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="42380-189">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="42380-190">Cliquez sur hello déploiement état toosee plus d’informations sur le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="42380-190">Click hello deployment status toosee information about hello deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42380-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="42380-191">Next steps</span></span>
* <span data-ttu-id="42380-192">Profiter de l’utilisation d’un modèle toocreate un ordinateur virtuel à l’aide des informations de hello dans [déployer une Machine virtuelle de Azure à l’aide de c# et un modèle de gestionnaire de ressources](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="42380-192">Take advantage of using a template toocreate a virtual machine by using hello information in [Deploy an Azure Virtual Machine using C# and a Resource Manager template](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="42380-193">En savoir plus sur l’utilisation de hello [Azure libraries pour .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="42380-193">Learn more about using hello [Azure libraries for .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span></span>

