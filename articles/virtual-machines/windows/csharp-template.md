---
title: "aaaDeploy une machine virtuelle à l’aide de c# et un modèle de gestionnaire de ressources | Documents Microsoft"
description: "Découvrez toohow toouse c# et une toodeploy de modèle de gestionnaire de ressources une machine virtuelle Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: bfba66e8-c923-4df2-900a-0c2643b81240
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: davidmu
ms.openlocfilehash: 91d470228cfeed72336b488ffef4dfbb25bc3a40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a>Déployer une machine virtuelle Azure à l’aide de C# et d’un modèle Resource Manager
Cet article vous explique comment toodeploy un modèle Azure Resource Manager à l’aide de c#. modèle Hello que vous créez déploie une seule machine virtuelle exécutant Windows Server dans un réseau virtuel avec un sous-réseau unique.

Pour obtenir une description détaillée de la ressource d’ordinateur virtuel hello, consultez [machines virtuelles dans un modèle Azure Resource Manager](template-description.md). Pour plus d’informations sur toutes les ressources hello dans un modèle, consultez [procédure pas à pas de gestionnaire de ressources Azure modèle](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Il prend environ 10 minutes toodo ces étapes.

## <a name="create-a-visual-studio-project"></a>Créer un projet Visual Studio

Dans cette étape, vous vous assurer que Visual Studio est installé et que vous créez un modèle de console application utilisée toodeploy hello.

1. Si vous ne l’avez pas déjà fait, installez [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Sélectionnez **développement de bureau .NET** sur hello page de charges de travail, puis cliquez sur **installer**. Bonjour résumé, vous pouvez voir que **outils de développement .NET Framework 4-4.6** est automatiquement sélectionné pour vous. Si vous avez déjà installé Visual Studio, vous pouvez ajouter les charges de travail hello .NET à l’aide de hello du Lanceur de Visual Studio.
2. Dans Visual Studio, cliquez sur **Fichier** > **Nouveau** > **Projet**.
3. Dans **modèles** > **Visual C#**, sélectionnez **l’application Console (.NET Framework)**, entrez *myDotnetProject* nom hello de Hello du projet, emplacement hello sélectionnez hello du projet d’et puis cliquez sur **OK**.

## <a name="install-hello-packages"></a>Installer des packages hello

Les packages NuGet sont hello plus simple façon tooinstall hello bibliothèques que vous devez toofinish ces étapes. bibliothèques hello tooget dont vous avez besoin dans Visual Studio, procédez comme suit :

1. Cliquez sur **Outils** > **Gestionnaire de package NuGet**, puis sur **Console du gestionnaire de package**.
2. Dans la console hello, tapez les commandes :

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    Install-Package WindowsAzure.Storage
    ```

## <a name="create-hello-files"></a>Créer des fichiers hello

Dans cette étape, vous créez un fichier de modèle qui déploie les ressources hello et un fichier de paramètres qui fournit le modèle de toohello de valeurs de paramètre. Vous créez également un fichier d’autorisation qui est utilisé tooperform Azure Resource Manager operations.

### <a name="create-hello-template-file"></a>Crée un fichier de modèle hello

1. Dans l’Explorateur de solutions, cliquez sur *myDotnetProject* > **Ajouter** > **Nouvel élément**, puis sélectionnez **Fichier texte** dans *Éléments Visual C#*. Nom de fichier hello *CreateVMTemplate.json*, puis cliquez sur **ajouter**.
2. Ajoutez ce fichier toohello de code JSON que vous avez créé :

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]", 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
              "adminUsername": "[parameters('adminUsername')]",
              "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
              "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "2012-R2-Datacenter",
                "version": "latest"
              },
              "osDisk": {
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

3. Enregistrez le fichier de CreateVMTemplate.json hello.

### <a name="create-hello-parameters-file"></a>Créer le fichier de paramètres hello

toospecify les valeurs des paramètres de ressource de hello qui sont définis dans le modèle de hello, vous créez un fichier de paramètres qui contient les valeurs hello.

1. Dans l’Explorateur de solutions, cliquez sur *myDotnetProject* > **Ajouter** > **Nouvel élément**, puis sélectionnez **Fichier texte** dans *Éléments Visual C#*. Nom de fichier hello *Parameters.json*, puis cliquez sur **ajouter**.
2. Ajoutez ce fichier toohello de code JSON que vous avez créé :

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

4. Enregistrez le fichier de Parameters.json hello.

### <a name="create-hello-authorization-file"></a>Créer le fichier d’autorisations de hello

Avant de pouvoir déployer un modèle, assurez-vous d’avoir accès tooan [principal du service Active Directory](../../resource-group-authenticate-service-principal.md). À partir de principal du service hello, vous acquérir un jeton d’authentification des demandes tooAzure Gestionnaire de ressources. Vous devez également enregistrer les ID de l’application hello, clé d’authentification hello et ID de client hello dont vous avez besoin dans le fichier d’autorisations de hello.

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
4. La valeur d’une variable d’environnement dans Windows nommé AZURE_AUTH_LOCATION avec les fichiers tooauthorization hello chemin d’accès complet que vous avez créé, par exemple hello suivant PowerShell commande peut être utilisée :

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```
    
## <a name="create-hello-management-client"></a>Créer le client de gestion hello

1. Ouvrir le fichier Program.cs de hello pour le projet hello que vous avez créé, puis ajoutez-les à l’aide de toohello instructions existantes en haut du fichier de hello :

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
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

## <a name="create-a-resource-group"></a>Créer un groupe de ressources

valeurs toospecify pour l’application hello, ajoutez la méthode Main toohello code :

```
var groupName = "myResourceGroup";
var location = Region.USWest;

var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

## <a name="create-a-storage-account"></a>Créez un compte de stockage.

paramètres et modèle de hello sont déployés à partir d’un compte de stockage dans Azure. Dans cette étape, vous créez le compte de hello et téléchargez des fichiers de hello. 

toocreate hello compte, ajoutez ce code de toohello méthode Main :

```
string storageAccountName = SdkContext.RandomResourceName("st", 10);

Console.WriteLine("Creating storage account...");
var storage = azure.StorageAccounts.Define(storageAccountName)
    .WithRegion(Region.USWest)
    .WithExistingResourceGroup(resourceGroup)
    .Create();

var storageKeys = storage.GetKeys();
string storageConnectionString = "DefaultEndpointsProtocol=https;"
    + "AccountName=" + storage.Name
    + ";AccountKey=" + storageKeys[0].Value
    + ";EndpointSuffix=core.windows.net";

var account = CloudStorageAccount.Parse(storageConnectionString);
var serviceClient = account.CreateCloudBlobClient();

Console.WriteLine("Creating container...");
var container = serviceClient.GetContainerReference("templates");
container.CreateIfNotExistsAsync().Wait();
var containerPermissions = new BlobContainerPermissions()
    { PublicAccess = BlobContainerPublicAccessType.Container };
container.SetPermissionsAsync(containerPermissions).Wait();

Console.WriteLine("Uploading template file...");
var templateblob = container.GetBlockBlobReference("CreateVMTemplate.json");
templateblob.UploadFromFile("..\\..\\CreateVMTemplate.json");

Console.WriteLine("Uploading parameters file...");
var paramblob = container.GetBlockBlobReference("Parameters.json");
paramblob.UploadFromFile("..\\..\\Parameters.json");
```

## <a name="deploy-hello-template"></a>Déployer le modèle de hello

Déployer le modèle de hello et les paramètres de compte de stockage hello qui a été créé. 

modèle de hello toodeploy, ajoutez ce code de toohello méthode Main :

```
var templatePath = "https://" + storageAccountName + ".blob.core.windows.net/templates/CreateVMTemplate.json";
var paramPath = "https://" + storageAccountName + ".blob.core.windows.net/templates/Parameters.json";
var deployment = azure.Deployments.Define("myDeployment")
    .WithExistingResourceGroup(groupName)
    .WithTemplateLink(templatePath, "1.0.0.0")
    .WithParametersLink(paramPath, "1.0.0.0")
    .WithMode(Microsoft.Azure.Management.ResourceManager.Fluent.Models.DeploymentMode.Incremental)
    .Create();
Console.WriteLine("Press enter toodelete hello resource group...");
Console.ReadLine();
```

## <a name="delete-hello-resources"></a>Supprimer des ressources de hello

Vous êtes facturé pour les ressources utilisées dans Azure, il est toujours ressources toodelete bonnes pratiques qui ne sont plus nécessaires. Vous n’avez pas besoin toodelete chaque ressource séparément à partir d’un groupe de ressources. Supprimer le groupe de ressources hello et toutes ses ressources sont automatiquement supprimés. 

ressource de hello toodelete groupe, ajoutez ce code de toohello méthode Main :

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a>Exécutez l’application hello

Il doit prendre environ cinq minutes pour que cette toorun d’application console complètement à partir de toofinish de début. 

1. application de console toorun hello, cliquez sur **Démarrer**.

2. Avant d’appuyer sur **entrée** toostart suppression des ressources, vous pouvez prendre quelques minutes la création de hello tooverify des ressources de hello Bonjour portail Azure. Cliquez sur hello déploiement état toosee plus d’informations sur le déploiement de hello.

## <a name="next-steps"></a>Étapes suivantes
* S’il existe des problèmes de déploiement de hello, une étape suivante consisterait toolook à [résoudre les erreurs courantes de déploiement Azure avec Azure Resource Manager](../../resource-manager-common-deployment-errors.md).
* Découvrez comment toodeploy un ordinateur virtuel et ses ressources de prise en charge en consultant [déployer un Azure Virtual Machine à l’aide de C#](csharp.md).
