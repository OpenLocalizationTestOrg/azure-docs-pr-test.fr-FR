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
# <a name="create-and-manage-windows-vms-in-azure-using-java"></a>Créer et gérer des machines virtuelles Windows dans Azure à l’aide de Java

Une [machine virtuelle Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) a besoin de plusieurs ressources de prise en charge Azure. Cet article traite de la création, de la gestion et de la suppression de ressources de machines virtuelles avec Java. Vous allez apprendre à effectuer les actions suivantes :

> [!div class="checklist"]
> * Création d’un projet Maven
> * Ajout de dépendances
> * Créer des informations d’identification
> * Créer des ressources
> * Effectuer les tâches de gestion
> * Supprimer des ressources
> * Exécutez l’application hello

Il prend environ 20 minutes toodo ces étapes.

## <a name="create-a-maven-project"></a>Création d’un projet Maven

1. Si ce n’est pas déjà fait, installez [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
2. Installez [Maven](http://maven.apache.org/download.cgi).
3. Créez un nouveau projet de dossier et hello :
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a>Ajout de dépendances

1. Sous hello `testAzureApp` dossier, ouvrez hello `pom.xml` de fichiers et d’ajouter trop de configuration de build hello&lt;projet&gt; construction de hello tooenable de votre application :

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

2. Ajouter des dépendances de hello sont nécessaires tooaccess hello Kit de développement Java Azure.

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

3. Enregistrez le fichier de hello.

## <a name="create-credentials"></a>Créer des informations d’identification

Avant de commencer cette étape, assurez-vous que vous avez accès tooan [principal du service Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md). Vous devez également enregistrer les ID de l’application hello, clé d’authentification hello et ID de client hello dont vous avez besoin dans une étape ultérieure.

### <a name="create-hello-authorization-file"></a>Créer le fichier d’autorisations de hello

1. Créez un fichier nommé `azureauth.properties` et ajouter ces tooit propriétés :

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

2. Enregistrez le fichier de hello.
3. Définissez une variable d’environnement nommée AZURE_AUTH_LOCATION dans votre environnement avec le fichier d’authentification toohello hello chemin d’accès complet.

### <a name="create-hello-management-client"></a>Créer le client de gestion hello

1. Ouvrez hello `App.java` de fichiers sous `src\main\java\com\fabrikam` et assurez-vous que cette déclaration de package est en haut de hello :

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. Sous l’instruction de package hello, ajoutez ces instructions import :
   
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

2. informations d’identification de toocreate hello Active Directory que vous avez besoin de demandes de toomake, ajoutez cette méthode main toohello de code Hello classe App :
   
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

## <a name="create-resources"></a>Créer des ressources

### <a name="create-hello-resource-group"></a>Créer le groupe de ressources hello

Toutes les ressources doivent être contenues dans un [groupe de ressources](../../azure-resource-manager/resource-group-overview.md).

valeurs toospecify hello application et créer le groupe de ressources hello, ajoutez ce bloc try de toohello code dans la méthode principale de hello :

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-hello-availability-set"></a>Créer le groupe à haute disponibilité hello

[Haute disponibilité](tutorial-availability-sets.md) facilitent pour vous toomaintain hello virtuels utilisés par votre application.

disponibilité de hello toocreate définie, ajoutez ce bloc try de toohello code dans la méthode principale de hello :

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-hello-public-ip-address"></a>Créer une adresse IP publique hello

A [adresse IP publique](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) est toocommunicate nécessaire avec l’ordinateur virtuel de hello.

toocreate hello adresse IP publique pour l’ordinateur virtuel de hello, ajoutez ce bloc try de toohello code dans la méthode principale de hello :

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-hello-virtual-network"></a>Créer le réseau virtuel de hello

Une machine virtuelle doit être incluse dans un sous-réseau d’un [réseau virtuel](../../virtual-network/virtual-networks-overview.md).

toocreate un sous-réseau et un réseau virtuel, ajoutez ce bloc try de toohello code dans la méthode principale de hello :

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

### <a name="create-hello-network-interface"></a>Créer l’interface de réseau hello

Un ordinateur virtuel doit un toocommunicate d’interface réseau sur le réseau virtuel de hello.

toocreate une interface réseau, ajoutez ce bloc try de toohello code dans la méthode principale de hello :

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

### <a name="create-hello-virtual-machine"></a>Créer la machine virtuelle de hello

Maintenant que vous avez créé hello toutes les ressources de support, vous pouvez créer un ordinateur virtuel.

toocreate hello de machine virtuelle, ajoutez ce bloc try de toohello code dans la méthode principale de hello :

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
> Ce didacticiel crée une machine virtuelle exécutant une version du système d’exploitation de serveur Windows hello. toolearn plus sur la sélection d’autres images, consultez [naviguer et sélectionnez les images de machine virtuelle Azure avec Windows PowerShell et hello CLI d’Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
>

Si vous voulez toouse un disque existant au lieu d’une image de marketplace, utilisez ce code : 

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

## <a name="perform-management-tasks"></a>Effectuer les tâches de gestion

Au cours de hello du cycle de vie d’un ordinateur virtuel, vous souhaiterez toorun des tâches de gestion telles que le démarrage, arrêt ou suppression d’une machine virtuelle. En outre, vous souhaiterez toocreate tooautomate répétitives ou complexes des tâches de code.

Lorsque vous devez toodo quoi que ce soit par hello machine virtuelle, vous devez tooget une instance de celui-ci. Ajoutez ce bloc try toohello code méthode principale hello :

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-hello-vm"></a>Obtenir des informations sur la machine virtuelle de hello

tooget plus d’informations sur la machine virtuelle de hello, ajoutez ce bloc try de toohello code dans la méthode principale de hello :

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

### <a name="stop-hello-vm"></a>Arrêter hello machine virtuelle

Vous pouvez arrêter une machine virtuelle et conserver tous ses paramètres, mais continuer toobe facturé pour celui-ci, ou vous pouvez arrêter une machine virtuelle et désallouer. Lorsqu’une machine virtuelle est libérée, toutes les ressources qui lui sont associées sont également libérées et la facturation de la machine virtuelle prend fin.

toostop hello virtual machine sans le désallouer, ajoutez ce bloc try de toohello code dans la méthode principale de hello :

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

Si vous voulez toodeallocate hello virtual machine, modifier le code de toothis d’appel hello hors tension :

```java
vm.deallocate();
```

### <a name="start-hello-vm"></a>Démarrer hello machine virtuelle

toostart hello de machine virtuelle, ajoutez ce bloc try de toohello code dans la méthode principale de hello :

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="resize-hello-vm"></a>Redimensionner hello machine virtuelle

De nombreux aspects du déploiement doivent être pris en considération lors du choix d’une taille pour votre machine virtuelle. Pour plus d’informations, voir [Tailles des machines virtuelles](sizes.md).  

taille toochange de machine virtuelle de hello, ajoutez ce bloc try de toohello code dans la méthode principale de hello :

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="add-a-data-disk-toohello-vm"></a>Ajouter un toohello de disque de données machine virtuelle

tooadd une machine virtuelle toohello disque données qui est de 2 Go, la taille a un numéro d’unité logique de 0 et un type de mise en cache de lecture/écriture, ajoutez ce bloc try de toohello code dans la méthode principale de hello :

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter toodelete resources...");
input.nextLine();
```

## <a name="delete-resources"></a>Supprimer des ressources

Vous êtes facturé pour les ressources utilisées dans Azure, il est toujours ressources toodelete bonnes pratiques qui ne sont plus nécessaires. Si vous souhaitez toodelete hello virtual machines et hello toutes les ressources de support, toutes les toodo est hello supprimer le groupe de ressources.

1. ressource de hello toodelete groupe, ajoutez ce bloc try de toohello code dans la méthode principale de hello :
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. Enregistrez le fichier de App.java hello.

## <a name="run-hello-application"></a>Exécutez l’application hello

Il doit prendre environ cinq minutes pour que cette toorun d’application console complètement à partir de toofinish de début.

1. toorun hello application, utilisez la commande Maven :

    ```
    mvn compile exec:java
    ```

2. Avant d’appuyer sur **entrée** toostart suppression des ressources, vous pouvez prendre quelques minutes la création de hello tooverify des ressources de hello Bonjour portail Azure. Cliquez sur hello déploiement état toosee plus d’informations sur le déploiement de hello.


## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur l’utilisation de hello [bibliothèques Azure pour Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).

