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
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a>Créer et gérer des machines virtuelles Windows dans Azure à l’aide de C# #

Une [machine virtuelle Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) a besoin de plusieurs ressources de prise en charge Azure. Cet article décrit comment créer, gérer et supprimer des ressources de machine virtuelle à l’aide de C#. Vous allez apprendre à effectuer les actions suivantes :

> [!div class="checklist"]
> * Créer un projet Visual Studio
> * Installer le package de hello
> * Créer des informations d’identification
> * Créer des ressources
> * Effectuer les tâches de gestion
> * Supprimer des ressources
> * Exécutez l’application hello

Il prend environ 20 minutes toodo ces étapes.

## <a name="create-a-visual-studio-project"></a>Créer un projet Visual Studio

1. Si vous ne l’avez pas déjà fait, installez [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Sélectionnez **développement de bureau .NET** sur hello page de charges de travail, puis cliquez sur **installer**. Bonjour résumé, vous pouvez voir que **outils de développement .NET Framework 4-4.6** est automatiquement sélectionné pour vous. Si vous avez déjà installé Visual Studio, vous pouvez ajouter les charges de travail hello .NET à l’aide de hello du Lanceur de Visual Studio.
2. Dans Visual Studio, cliquez sur **Fichier** > **Nouveau** > **Projet**.
3. Dans **modèles** > **Visual C#**, sélectionnez **l’application Console (.NET Framework)**, entrez *myDotnetProject* nom hello de Hello du projet, emplacement hello sélectionnez hello du projet d’et puis cliquez sur **OK**.

## <a name="install-hello-package"></a>Installer le package de hello

Les packages NuGet sont hello plus simple façon tooinstall hello bibliothèques que vous devez toofinish ces étapes. bibliothèques hello tooget dont vous avez besoin dans Visual Studio, procédez comme suit :

1. Cliquez sur **Outils** > **Gestionnaire de package NuGet**, puis sur **Console du gestionnaire de package**.
2. Tapez la commande suivante dans la console hello :

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a>Créer des informations d’identification

Avant de commencer cette étape, assurez-vous que vous avez accès tooan [principal du service Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md). Vous devez également enregistrer les ID de l’application hello, clé d’authentification hello et ID de client hello dont vous avez besoin dans une étape ultérieure.

### <a name="create-hello-authorization-file"></a>Créer le fichier d’autorisations de hello

1. Dans l’Explorateur de solutions, cliquez sur *myDotnetProject* > **Ajouter** > **Nouvel élément**, puis sélectionnez **Fichier texte** dans *Éléments Visual C#*. Nom de fichier hello *azureauth.properties*, puis cliquez sur **ajouter**.
2. Ajoutez ces propriétés d’autorisation :

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

    Remplacez  **&lt;id d’abonnement&gt;**  avec votre identificateur d’abonnement,  **&lt;id d’application&gt;**  avec hello application Active Directory identificateur,  **&lt;clé d’authentification&gt;**  avec la clé d’application hello, et  **&lt;id de client&gt;**  avec le client de hello identificateur.

3. Enregistrez le fichier de azureauth.properties hello. 
4. Définir une variable d’environnement dans Windows nommé AZURE_AUTH_LOCATION avec les fichiers tooauthorization hello chemin d’accès complet que vous avez créé. Par exemple, hello suivant de commande PowerShell peut être utilisé :

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-hello-management-client"></a>Créer le client de gestion hello

1. Ouvrir le fichier Program.cs de hello pour le projet hello que vous avez créé, puis ajoutez-les à l’aide de toohello instructions existantes en haut du fichier de hello :

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. client de gestion toocreate hello, ajoutez ce code de toohello méthode Main :

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a>Créer des ressources

### <a name="create-hello-resource-group"></a>Créer le groupe de ressources hello

Toutes les ressources doivent être contenues dans un [groupe de ressources](../../azure-resource-manager/resource-group-overview.md).

valeurs toospecify hello application et créer le groupe de ressources hello, ajoutez ce code de toohello méthode Main :

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-hello-availability-set"></a>Créer le groupe à haute disponibilité hello

[Haute disponibilité](tutorial-availability-sets.md) facilitent pour vous toomaintain hello virtuels utilisés par votre application.

disponibilité de hello toocreate définie, ajoutez ce code de toohello méthode Main :

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-hello-public-ip-address"></a>Créer une adresse IP publique hello

A [adresse IP publique](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) est toocommunicate nécessaire avec l’ordinateur virtuel de hello.

toocreate hello adresse IP publique pour l’ordinateur virtuel de hello, ajoutez ce code de toohello méthode Main :
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-hello-virtual-network"></a>Créer le réseau virtuel de hello

Une machine virtuelle doit être incluse dans un sous-réseau d’un [réseau virtuel](../../virtual-network/virtual-networks-overview.md).

toocreate un sous-réseau et un réseau virtuel, ajoutez ce code de toohello méthode Main :

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-hello-network-interface"></a>Créer l’interface de réseau hello

Un ordinateur virtuel doit un toocommunicate d’interface réseau sur le réseau virtuel de hello.

toocreate une interface réseau, ajoutez ce code de toohello méthode Main :

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

### <a name="create-hello-virtual-machine"></a>Créer la machine virtuelle de hello

Maintenant que vous avez créé hello toutes les ressources de support, vous pouvez créer un ordinateur virtuel.

toocreate hello d’ordinateur virtuel, ajoutez ce code de toohello méthode Main :

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
> Ce didacticiel crée une machine virtuelle exécutant une version du système d’exploitation de serveur Windows hello. toolearn plus sur la sélection d’autres images, consultez [naviguer et sélectionnez les images de machine virtuelle Azure avec Windows PowerShell et hello CLI d’Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
>

Si vous voulez toouse un disque existant au lieu d’une image de marketplace, utilisez ce code :

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

## <a name="perform-management-tasks"></a>Effectuer les tâches de gestion

Au cours de hello du cycle de vie d’un ordinateur virtuel, vous souhaiterez toorun des tâches de gestion telles que le démarrage, arrêt ou suppression d’une machine virtuelle. En outre, vous souhaiterez toocreate tooautomate répétitives ou complexes des tâches de code.

Lorsque vous devez toodo quoi que ce soit par hello machine virtuelle, vous devez tooget une instance de celui-ci :

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-hello-vm"></a>Obtenir des informations sur la machine virtuelle de hello

tooget plus d’informations sur la machine virtuelle de hello, ajoutez ce code de toohello méthode Main :

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

### <a name="stop-hello-vm"></a>Arrêter hello machine virtuelle

Vous pouvez arrêter une machine virtuelle et conserver tous ses paramètres, mais continuer toobe facturé pour celui-ci, ou vous pouvez arrêter une machine virtuelle et désallouer. Lorsqu’une machine virtuelle est libérée, toutes les ressources qui lui sont associées sont également libérées et la facturation de la machine virtuelle prend fin.

toostop hello virtual machine sans le désallouer, ajoutez ce code de toohello méthode Main :

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

Si vous voulez toodeallocate hello virtual machine, modifier le code de toothis d’appel hello hors tension :

```
vm.Deallocate();
```

### <a name="start-hello-vm"></a>Démarrer hello machine virtuelle

toostart hello d’ordinateur virtuel, ajoutez ce code de toohello méthode Main :

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="resize-hello-vm"></a>Redimensionner hello machine virtuelle

De nombreux aspects du déploiement doivent être pris en considération lors du choix d’une taille pour votre machine virtuelle. Pour plus d’informations, voir [Tailles des machines virtuelles](sizes.md).  

taille toochange de machine virtuelle de hello, ajoutez ce code de toohello méthode Main :

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-toohello-vm"></a>Ajouter un toohello de disque de données machine virtuelle

tooadd un ordinateur virtuel des toohello du disque de données, ajoutez ce principal de code toohello méthode tooadd un disque de données est de 2 Go de taille, han un numéro d’unité logique de 0 et un type de mise en cache de lecture/écriture :

```
Console.WriteLine("Adding data disk toovm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter toodelete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a>Supprimer des ressources

Vous êtes facturé pour les ressources utilisées dans Azure, il est toujours ressources toodelete bonnes pratiques qui ne sont plus nécessaires. Si vous souhaitez toodelete hello virtual machines et hello toutes les ressources de support, toutes les toodo est hello supprimer le groupe de ressources.

ressource de hello toodelete groupe, ajoutez ce code de toohello méthode Main :

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a>Exécutez l’application hello

Il doit prendre environ cinq minutes pour que cette toorun d’application console complètement à partir de toofinish de début. 

1. application de console toorun hello, cliquez sur **Démarrer**.

2. Avant d’appuyer sur **entrée** toostart suppression des ressources, vous pouvez prendre quelques minutes la création de hello tooverify des ressources de hello Bonjour portail Azure. Cliquez sur hello déploiement état toosee plus d’informations sur le déploiement de hello.

## <a name="next-steps"></a>Étapes suivantes
* Profiter de l’utilisation d’un modèle toocreate un ordinateur virtuel à l’aide des informations de hello dans [déployer une Machine virtuelle de Azure à l’aide de c# et un modèle de gestionnaire de ressources](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* En savoir plus sur l’utilisation de hello [Azure libraries pour .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).

