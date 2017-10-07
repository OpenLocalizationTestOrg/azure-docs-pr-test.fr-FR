---
title: "aaaCreate et gérer un Java à l’aide de Machine virtuelle Azure | Documents Microsoft"
description: Utilisez toodeploy Java et Azure Resource Manager un ordinateur virtuel et toutes ses ressources de prise en charge.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 31ac8d59f92ecff887e64906940933dd6fd50815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-java"></a><span data-ttu-id="cfe58-103">Créer et gérer des machines virtuelles Windows dans Azure à l’aide de Java</span><span class="sxs-lookup"><span data-stu-id="cfe58-103">Create and manage Windows VMs in Azure using Java</span></span>

<span data-ttu-id="cfe58-104">Une [machine virtuelle Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) a besoin de plusieurs ressources de prise en charge Azure.</span><span class="sxs-lookup"><span data-stu-id="cfe58-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="cfe58-105">Cet article traite de la création, de la gestion et de la suppression de ressources de machines virtuelles avec Java.</span><span class="sxs-lookup"><span data-stu-id="cfe58-105">This article covers creating, managing, and deleting VM resources using Java.</span></span> <span data-ttu-id="cfe58-106">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="cfe58-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cfe58-107">Création d’un projet Maven</span><span class="sxs-lookup"><span data-stu-id="cfe58-107">Create a Maven project</span></span>
> * <span data-ttu-id="cfe58-108">Ajout de dépendances</span><span class="sxs-lookup"><span data-stu-id="cfe58-108">Add dependencies</span></span>
> * <span data-ttu-id="cfe58-109">Créer des informations d’identification</span><span class="sxs-lookup"><span data-stu-id="cfe58-109">Create credentials</span></span>
> * <span data-ttu-id="cfe58-110">Créer des ressources</span><span class="sxs-lookup"><span data-stu-id="cfe58-110">Create resources</span></span>
> * <span data-ttu-id="cfe58-111">Effectuer les tâches de gestion</span><span class="sxs-lookup"><span data-stu-id="cfe58-111">Perform management tasks</span></span>
> * <span data-ttu-id="cfe58-112">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="cfe58-112">Delete resources</span></span>
> * <span data-ttu-id="cfe58-113">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="cfe58-113">Run hello application</span></span>

<span data-ttu-id="cfe58-114">Il prend environ 20 minutes toodo ces étapes.</span><span class="sxs-lookup"><span data-stu-id="cfe58-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="cfe58-115">Création d’un projet Maven</span><span class="sxs-lookup"><span data-stu-id="cfe58-115">Create a Maven project</span></span>

1. <span data-ttu-id="cfe58-116">Si ce n’est pas déjà fait, installez [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="cfe58-116">If you haven't already done so, install [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
2. <span data-ttu-id="cfe58-117">Installez [Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="cfe58-117">Install [Maven](http://maven.apache.org/download.cgi).</span></span>
3. <span data-ttu-id="cfe58-118">Créez un nouveau projet de dossier et hello :</span><span class="sxs-lookup"><span data-stu-id="cfe58-118">Create a new folder and hello project:</span></span>
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a><span data-ttu-id="cfe58-119">Ajout de dépendances</span><span class="sxs-lookup"><span data-stu-id="cfe58-119">Add dependencies</span></span>

1. <span data-ttu-id="cfe58-120">Sous hello `testAzureApp` dossier, ouvrez hello `pom.xml` de fichiers et d’ajouter trop de configuration de build hello&lt;projet&gt; construction de hello tooenable de votre application :</span><span class="sxs-lookup"><span data-stu-id="cfe58-120">Under hello `testAzureApp` folder, open hello `pom.xml` file and add hello build configuration too&lt;project&gt; tooenable hello building of your application:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <configuration>
                <mainClass>com.fabrikam.testAzureApp.App</mainClass>
            </configuration>
        </plugin>
      </plugins>
    </build>
    ```

2. <span data-ttu-id="cfe58-121">Ajouter des dépendances de hello sont nécessaires tooaccess hello Kit de développement Java Azure.</span><span class="sxs-lookup"><span data-stu-id="cfe58-121">Add hello dependencies that are needed tooaccess hello Azure Java SDK.</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-compute</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-resources</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-network</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.squareup.okio</groupId>
      <artifactId>okio</artifactId>
      <version>1.13.0</version>
    </dependency>
    <dependency> 
      <groupId>com.nimbusds</groupId>
      <artifactId>nimbus-jose-jwt</artifactId>
      <version>3.6</version>
    </dependency>
    <dependency>
      <groupId>net.minidev</groupId>
      <artifactId>json-smart</artifactId>
      <version>1.0.6.3</version>
    </dependency>
    <dependency>
      <groupId>javax.mail</groupId>
      <artifactId>mail</artifactId>
      <version>1.4.5</version>
    </dependency>
    ```

3. <span data-ttu-id="cfe58-122">Enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="cfe58-122">Save hello file.</span></span>

## <a name="create-credentials"></a><span data-ttu-id="cfe58-123">Créer des informations d’identification</span><span class="sxs-lookup"><span data-stu-id="cfe58-123">Create credentials</span></span>

<span data-ttu-id="cfe58-124">Avant de commencer cette étape, assurez-vous que vous avez accès tooan [principal du service Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cfe58-124">Before you start this step, make sure that you have access tooan [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="cfe58-125">Vous devez également enregistrer les ID de l’application hello, clé d’authentification hello et ID de client hello dont vous avez besoin dans une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="cfe58-125">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="cfe58-126">Créer le fichier d’autorisations de hello</span><span class="sxs-lookup"><span data-stu-id="cfe58-126">Create hello authorization file</span></span>

1. <span data-ttu-id="cfe58-127">Créez un fichier nommé `azureauth.properties` et ajouter ces tooit propriétés :</span><span class="sxs-lookup"><span data-stu-id="cfe58-127">Create a file named `azureauth.properties` and add these properties tooit:</span></span>

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

    <span data-ttu-id="cfe58-128">Remplacez  **&lt;id d’abonnement&gt;**  avec votre identificateur d’abonnement,  **&lt;id d’application&gt;**  avec hello application Active Directory identificateur,  **&lt;clé d’authentification&gt;**  avec la clé d’application hello, et  **&lt;id de client&gt;**  avec le client de hello identificateur.</span><span class="sxs-lookup"><span data-stu-id="cfe58-128">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

2. <span data-ttu-id="cfe58-129">Enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="cfe58-129">Save hello file.</span></span>
3. <span data-ttu-id="cfe58-130">Définissez une variable d’environnement nommée AZURE_AUTH_LOCATION dans votre environnement avec le fichier d’authentification toohello hello chemin d’accès complet.</span><span class="sxs-lookup"><span data-stu-id="cfe58-130">Set an environment variable named AZURE_AUTH_LOCATION in your shell with hello full path toohello authentication file.</span></span>

### <a name="create-hello-management-client"></a><span data-ttu-id="cfe58-131">Créer le client de gestion hello</span><span class="sxs-lookup"><span data-stu-id="cfe58-131">Create hello management client</span></span>

1. <span data-ttu-id="cfe58-132">Ouvrez hello `App.java` de fichiers sous `src\main\java\com\fabrikam` et assurez-vous que cette déclaration de package est en haut de hello :</span><span class="sxs-lookup"><span data-stu-id="cfe58-132">Open hello `App.java` file under `src\main\java\com\fabrikam` and make sure this package statement is at hello top:</span></span>

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. <span data-ttu-id="cfe58-133">Sous l’instruction de package hello, ajoutez ces instructions import :</span><span class="sxs-lookup"><span data-stu-id="cfe58-133">Under hello package statement, add these import statements:</span></span>
   
    ```java
    import com.microsoft.azure.management.Azure;
    import com.microsoft.azure.management.compute.AvailabilitySet;
    import com.microsoft.azure.management.compute.AvailabilitySetSkuTypes;
    import com.microsoft.azure.management.compute.CachingTypes;
    import com.microsoft.azure.management.compute.InstanceViewStatus;
    import com.microsoft.azure.management.compute.DiskInstanceView;
    import com.microsoft.azure.management.compute.VirtualMachine;
    import com.microsoft.azure.management.compute.VirtualMachineSizeTypes;
    import com.microsoft.azure.management.network.PublicIPAddress;
    import com.microsoft.azure.management.network.Network;
    import com.microsoft.azure.management.network.NetworkInterface;
    import com.microsoft.azure.management.resources.ResourceGroup;
    import com.microsoft.azure.management.resources.fluentcore.arm.Region;
    import com.microsoft.azure.management.resources.fluentcore.model.Creatable;
    import com.microsoft.rest.LogLevel;
    import java.io.File;
    import java.util.Scanner;
    ```

2. <span data-ttu-id="cfe58-134">informations d’identification de toocreate hello Active Directory que vous avez besoin de demandes de toomake, ajoutez cette méthode main toohello de code Hello classe App :</span><span class="sxs-lookup"><span data-stu-id="cfe58-134">toocreate hello Active Directory credentials that you need toomake requests, add this code toohello main method of hello App class:</span></span>
   
    ```java
    try {    
        final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
        Azure azure = Azure.configure()
            .withLogLevel(LogLevel.BASIC)
            .authenticate(credFile)
            .withDefaultSubscription();
    } catch (Exception e) {
        System.out.println(e.getMessage());
        e.printStackTrace();
    }

    ```

## <a name="create-resources"></a><span data-ttu-id="cfe58-135">Créer des ressources</span><span class="sxs-lookup"><span data-stu-id="cfe58-135">Create resources</span></span>

### <a name="create-hello-resource-group"></a><span data-ttu-id="cfe58-136">Créer le groupe de ressources hello</span><span class="sxs-lookup"><span data-stu-id="cfe58-136">Create hello resource group</span></span>

<span data-ttu-id="cfe58-137">Toutes les ressources doivent être contenues dans un [groupe de ressources](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cfe58-137">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="cfe58-138">valeurs toospecify hello application et créer le groupe de ressources hello, ajoutez ce bloc try de toohello code dans la méthode principale de hello :</span><span class="sxs-lookup"><span data-stu-id="cfe58-138">toospecify values for hello application and create hello resource group, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-hello-availability-set"></a><span data-ttu-id="cfe58-139">Créer le groupe à haute disponibilité hello</span><span class="sxs-lookup"><span data-stu-id="cfe58-139">Create hello availability set</span></span>

<span data-ttu-id="cfe58-140">[Haute disponibilité](tutorial-availability-sets.md) facilitent pour vous toomaintain hello virtuels utilisés par votre application.</span><span class="sxs-lookup"><span data-stu-id="cfe58-140">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

<span data-ttu-id="cfe58-141">disponibilité de hello toocreate définie, ajoutez ce bloc try de toohello code dans la méthode principale de hello :</span><span class="sxs-lookup"><span data-stu-id="cfe58-141">toocreate hello availability set, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-hello-public-ip-address"></a><span data-ttu-id="cfe58-142">Créer une adresse IP publique hello</span><span class="sxs-lookup"><span data-stu-id="cfe58-142">Create hello public IP address</span></span>

<span data-ttu-id="cfe58-143">A [adresse IP publique](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) est toocommunicate nécessaire avec l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="cfe58-143">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

<span data-ttu-id="cfe58-144">toocreate hello adresse IP publique pour l’ordinateur virtuel de hello, ajoutez ce bloc try de toohello code dans la méthode principale de hello :</span><span class="sxs-lookup"><span data-stu-id="cfe58-144">toocreate hello public IP address for hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-hello-virtual-network"></a><span data-ttu-id="cfe58-145">Créer le réseau virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="cfe58-145">Create hello virtual network</span></span>

<span data-ttu-id="cfe58-146">Une machine virtuelle doit être incluse dans un sous-réseau d’un [réseau virtuel](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cfe58-146">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="cfe58-147">toocreate un sous-réseau et un réseau virtuel, ajoutez ce bloc try de toohello code dans la méthode principale de hello :</span><span class="sxs-lookup"><span data-stu-id="cfe58-147">toocreate a subnet and a virtual network, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating virtual network...");
Network network = azure.networks()
    .define("myVN")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withAddressSpace("10.0.0.0/16")
    .withSubnet("mySubnet","10.0.0.0/24")
    .create();
```

### <a name="create-hello-network-interface"></a><span data-ttu-id="cfe58-148">Créer l’interface de réseau hello</span><span class="sxs-lookup"><span data-stu-id="cfe58-148">Create hello network interface</span></span>

<span data-ttu-id="cfe58-149">Un ordinateur virtuel doit un toocommunicate d’interface réseau sur le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="cfe58-149">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

<span data-ttu-id="cfe58-150">toocreate une interface réseau, ajoutez ce bloc try de toohello code dans la méthode principale de hello :</span><span class="sxs-lookup"><span data-stu-id="cfe58-150">toocreate a network interface, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating network interface...");
NetworkInterface networkInterface = azure.networkInterfaces()
    .define("myNIC")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withExistingPrimaryNetwork(network)
    .withSubnet("mySubnet")
    .withPrimaryPrivateIPAddressDynamic()
    .withExistingPrimaryPublicIPAddress(publicIPAddress)
    .create();
```

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="cfe58-151">Créer la machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="cfe58-151">Create hello virtual machine</span></span>

<span data-ttu-id="cfe58-152">Maintenant que vous avez créé hello toutes les ressources de support, vous pouvez créer un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="cfe58-152">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="cfe58-153">toocreate hello de machine virtuelle, ajoutez ce bloc try de toohello code dans la méthode principale de hello :</span><span class="sxs-lookup"><span data-stu-id="cfe58-153">toocreate hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating virtual machine...");
VirtualMachine virtualMachine = azure.virtualMachines()
    .define("myVM")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withExistingPrimaryNetworkInterface(networkInterface)
    .withLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .withAdminUsername("azureuser")
    .withAdminPassword("Azure12345678")
    .withComputerName("myVM")
    .withExistingAvailabilitySet(availabilitySet)
    .withSize("Standard_DS1")
    .create();
Scanner input = new Scanner(System.in);
System.out.println("Press enter tooget information about hello VM...");
input.nextLine();
```

> [!NOTE]
> <span data-ttu-id="cfe58-154">Ce didacticiel crée une machine virtuelle exécutant une version du système d’exploitation de serveur Windows hello.</span><span class="sxs-lookup"><span data-stu-id="cfe58-154">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="cfe58-155">toolearn plus sur la sélection d’autres images, consultez [naviguer et sélectionnez les images de machine virtuelle Azure avec Windows PowerShell et hello CLI d’Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cfe58-155">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="cfe58-156">Si vous voulez toouse un disque existant au lieu d’une image de marketplace, utilisez ce code :</span><span class="sxs-lookup"><span data-stu-id="cfe58-156">If you want toouse an existing disk instead of a marketplace image, use this code:</span></span> 

```java
ManagedDisk managedDisk = azure.disks.define("myosdisk") 
    .withRegion(Region.US_EAST) 
    .withExistingResourceGroup("myResourceGroup") 
    .withWindowsFromVhd("https://mystorage.blob.core.windows.net/vhds/myosdisk.vhd") 
    .withSizeInGB(128) 
    .withSku(DiskSkuTypes.PremiumLRS) 
    .create(); 

azure.virtualMachines.define("myVM") 
    .withRegion(Region.US_EAST) 
    .withExistingResourceGroup("myResourceGroup") 
    .withExistingPrimaryNetworkInterface(networkInterface) 
    .withSpecializedOSDisk(managedDisk, OperatingSystemTypes.Windows) 
    .withExistingAvailabilitySet(availabilitySet) 
    .withSize(VirtualMachineSizeTypes.StandardDS1) 
    .create(); 
``` 

## <a name="perform-management-tasks"></a><span data-ttu-id="cfe58-157">Effectuer les tâches de gestion</span><span class="sxs-lookup"><span data-stu-id="cfe58-157">Perform management tasks</span></span>

<span data-ttu-id="cfe58-158">Au cours de hello du cycle de vie d’un ordinateur virtuel, vous souhaiterez toorun des tâches de gestion telles que le démarrage, arrêt ou suppression d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="cfe58-158">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="cfe58-159">En outre, vous souhaiterez toocreate tooautomate répétitives ou complexes des tâches de code.</span><span class="sxs-lookup"><span data-stu-id="cfe58-159">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

<span data-ttu-id="cfe58-160">Lorsque vous devez toodo quoi que ce soit par hello machine virtuelle, vous devez tooget une instance de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="cfe58-160">When you need toodo anything with hello VM, you need tooget an instance of it.</span></span> <span data-ttu-id="cfe58-161">Ajoutez ce bloc try toohello code méthode principale hello :</span><span class="sxs-lookup"><span data-stu-id="cfe58-161">Add this code toohello try block of hello main method:</span></span>

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="cfe58-162">Obtenir des informations sur la machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="cfe58-162">Get information about hello VM</span></span>

<span data-ttu-id="cfe58-163">tooget plus d’informations sur la machine virtuelle de hello, ajoutez ce bloc try de toohello code dans la méthode principale de hello :</span><span class="sxs-lookup"><span data-stu-id="cfe58-163">tooget information about hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("hardwareProfile");
System.out.println("    vmSize: " + vm.size());
System.out.println("storageProfile");
System.out.println("  imageReference");
System.out.println("    publisher: " + vm.storageProfile().imageReference().publisher());
System.out.println("    offer: " + vm.storageProfile().imageReference().offer());
System.out.println("    sku: " + vm.storageProfile().imageReference().sku());
System.out.println("    version: " + vm.storageProfile().imageReference().version());
System.out.println("  osDisk");
System.out.println("    osType: " + vm.storageProfile().osDisk().osType());
System.out.println("    name: " + vm.storageProfile().osDisk().name());
System.out.println("    createOption: " + vm.storageProfile().osDisk().createOption());
System.out.println("    caching: " + vm.storageProfile().osDisk().caching());
System.out.println("osProfile");
System.out.println("    computerName: " + vm.osProfile().computerName());
System.out.println("    adminUserName: " + vm.osProfile().adminUsername());
System.out.println("    provisionVMAgent: " + vm.osProfile().windowsConfiguration().provisionVMAgent());
System.out.println("    enableAutomaticUpdates: " + vm.osProfile().windowsConfiguration().enableAutomaticUpdates());
System.out.println("networkProfile");
System.out.println("    networkInterface: " + vm.primaryNetworkInterfaceId());
System.out.println("vmAgent");
System.out.println("  vmAgentVersion: " + vm.instanceView().vmAgent().vmAgentVersion());
System.out.println("    statuses");
for(InstanceViewStatus status : vm.instanceView().vmAgent().statuses()) {
    System.out.println("    code: " + status.code());
    System.out.println("    displayStatus: " + status.displayStatus());
    System.out.println("    message: " + status.message());
    System.out.println("    time: " + status.time());
}
System.out.println("disks");
for(DiskInstanceView disk : vm.instanceView().disks()) {
    System.out.println("  name: " + disk.name());
    System.out.println("  statuses");
    for(InstanceViewStatus status : disk.statuses()) {
        System.out.println("    code: " + status.code());
        System.out.println("    displayStatus: " + status.displayStatus());
        System.out.println("    time: " + status.time());
    }
}
System.out.println("VM general status");
System.out.println("  provisioningStatus: " + vm.provisioningState());
System.out.println("  id: " + vm.id());
System.out.println("  name: " + vm.name());
System.out.println("  type: " + vm.type());
System.out.println("VM instance status");
for(InstanceViewStatus status : vm.instanceView().statuses()) {
    System.out.println("  code: " + status.code());
    System.out.println("  displayStatus: " + status.displayStatus());
}
System.out.println("Press enter toocontinue...");
input.nextLine();   
```

### <a name="stop-hello-vm"></a><span data-ttu-id="cfe58-164">Arrêter hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="cfe58-164">Stop hello VM</span></span>

<span data-ttu-id="cfe58-165">Vous pouvez arrêter une machine virtuelle et conserver tous ses paramètres, mais continuer toobe facturé pour celui-ci, ou vous pouvez arrêter une machine virtuelle et désallouer.</span><span class="sxs-lookup"><span data-stu-id="cfe58-165">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="cfe58-166">Lorsqu’une machine virtuelle est libérée, toutes les ressources qui lui sont associées sont également libérées et la facturation de la machine virtuelle prend fin.</span><span class="sxs-lookup"><span data-stu-id="cfe58-166">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="cfe58-167">toostop hello virtual machine sans le désallouer, ajoutez ce bloc try de toohello code dans la méthode principale de hello :</span><span class="sxs-lookup"><span data-stu-id="cfe58-167">toostop hello virtual machine without deallocating it, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

<span data-ttu-id="cfe58-168">Si vous voulez toodeallocate hello virtual machine, modifier le code de toothis d’appel hello hors tension :</span><span class="sxs-lookup"><span data-stu-id="cfe58-168">If you want toodeallocate hello virtual machine, change hello PowerOff call toothis code:</span></span>

```java
vm.deallocate();
```

### <a name="start-hello-vm"></a><span data-ttu-id="cfe58-169">Démarrer hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="cfe58-169">Start hello VM</span></span>

<span data-ttu-id="cfe58-170">toostart hello de machine virtuelle, ajoutez ce bloc try de toohello code dans la méthode principale de hello :</span><span class="sxs-lookup"><span data-stu-id="cfe58-170">toostart hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="resize-hello-vm"></a><span data-ttu-id="cfe58-171">Redimensionner hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="cfe58-171">Resize hello VM</span></span>

<span data-ttu-id="cfe58-172">De nombreux aspects du déploiement doivent être pris en considération lors du choix d’une taille pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="cfe58-172">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="cfe58-173">Pour plus d’informations, voir [Tailles des machines virtuelles](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="cfe58-173">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="cfe58-174">taille toochange de machine virtuelle de hello, ajoutez ce bloc try de toohello code dans la méthode principale de hello :</span><span class="sxs-lookup"><span data-stu-id="cfe58-174">toochange size of hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="cfe58-175">Ajouter un toohello de disque de données machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="cfe58-175">Add a data disk toohello VM</span></span>

<span data-ttu-id="cfe58-176">tooadd une machine virtuelle toohello disque données qui est de 2 Go, la taille a un numéro d’unité logique de 0 et un type de mise en cache de lecture/écriture, ajoutez ce bloc try de toohello code dans la méthode principale de hello :</span><span class="sxs-lookup"><span data-stu-id="cfe58-176">tooadd a data disk toohello virtual machine that is 2 GB in size, has a LUN of 0, and a caching type of ReadWrite, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter toodelete resources...");
input.nextLine();
```

## <a name="delete-resources"></a><span data-ttu-id="cfe58-177">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="cfe58-177">Delete resources</span></span>

<span data-ttu-id="cfe58-178">Vous êtes facturé pour les ressources utilisées dans Azure, il est toujours ressources toodelete bonnes pratiques qui ne sont plus nécessaires.</span><span class="sxs-lookup"><span data-stu-id="cfe58-178">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="cfe58-179">Si vous souhaitez toodelete hello virtual machines et hello toutes les ressources de support, toutes les toodo est hello supprimer le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="cfe58-179">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

1. <span data-ttu-id="cfe58-180">ressource de hello toodelete groupe, ajoutez ce bloc try de toohello code dans la méthode principale de hello :</span><span class="sxs-lookup"><span data-stu-id="cfe58-180">toodelete hello resource group, add this code toohello try block in hello main method:</span></span>
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. <span data-ttu-id="cfe58-181">Enregistrez le fichier de App.java hello.</span><span class="sxs-lookup"><span data-stu-id="cfe58-181">Save hello App.java file.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="cfe58-182">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="cfe58-182">Run hello application</span></span>

<span data-ttu-id="cfe58-183">Il doit prendre environ cinq minutes pour que cette toorun d’application console complètement à partir de toofinish de début.</span><span class="sxs-lookup"><span data-stu-id="cfe58-183">It should take about five minutes for this console application toorun completely from start toofinish.</span></span>

1. <span data-ttu-id="cfe58-184">toorun hello application, utilisez la commande Maven :</span><span class="sxs-lookup"><span data-stu-id="cfe58-184">toorun hello application, use this Maven command:</span></span>

    ```
    mvn compile exec:java
    ```

2. <span data-ttu-id="cfe58-185">Avant d’appuyer sur **entrée** toostart suppression des ressources, vous pouvez prendre quelques minutes la création de hello tooverify des ressources de hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cfe58-185">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="cfe58-186">Cliquez sur hello déploiement état toosee plus d’informations sur le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="cfe58-186">Click hello deployment status toosee information about hello deployment.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cfe58-187">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cfe58-187">Next steps</span></span>
* <span data-ttu-id="cfe58-188">En savoir plus sur l’utilisation de hello [bibliothèques Azure pour Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span><span class="sxs-lookup"><span data-stu-id="cfe58-188">Learn more about using hello [Azure libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span></span>

