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
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a><span data-ttu-id="a987e-103">Déployer une machine virtuelle Azure à l’aide de C# et d’un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a987e-103">Deploy an Azure Virtual Machine using C# and a Resource Manager template</span></span>
<span data-ttu-id="a987e-104">Cet article vous explique comment toodeploy un modèle Azure Resource Manager à l’aide de c#.</span><span class="sxs-lookup"><span data-stu-id="a987e-104">This article shows you how toodeploy an Azure Resource Manager template using C#.</span></span> <span data-ttu-id="a987e-105">modèle Hello que vous créez déploie une seule machine virtuelle exécutant Windows Server dans un réseau virtuel avec un sous-réseau unique.</span><span class="sxs-lookup"><span data-stu-id="a987e-105">hello template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="a987e-106">Pour obtenir une description détaillée de la ressource d’ordinateur virtuel hello, consultez [machines virtuelles dans un modèle Azure Resource Manager](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="a987e-106">For a detailed description of hello virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="a987e-107">Pour plus d’informations sur toutes les ressources hello dans un modèle, consultez [procédure pas à pas de gestionnaire de ressources Azure modèle](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="a987e-107">For more information about all hello resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="a987e-108">Il prend environ 10 minutes toodo ces étapes.</span><span class="sxs-lookup"><span data-stu-id="a987e-108">It takes about 10 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="a987e-109">Créer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a987e-109">Create a Visual Studio project</span></span>

<span data-ttu-id="a987e-110">Dans cette étape, vous vous assurer que Visual Studio est installé et que vous créez un modèle de console application utilisée toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="a987e-110">In this step, you make sure that Visual Studio is installed and you create a console application used toodeploy hello template.</span></span>

1. <span data-ttu-id="a987e-111">Si vous ne l’avez pas déjà fait, installez [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="a987e-111">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="a987e-112">Sélectionnez **développement de bureau .NET** sur hello page de charges de travail, puis cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="a987e-112">Select **.NET desktop development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="a987e-113">Bonjour résumé, vous pouvez voir que **outils de développement .NET Framework 4-4.6** est automatiquement sélectionné pour vous.</span><span class="sxs-lookup"><span data-stu-id="a987e-113">In hello summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="a987e-114">Si vous avez déjà installé Visual Studio, vous pouvez ajouter les charges de travail hello .NET à l’aide de hello du Lanceur de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a987e-114">If you have already installed Visual Studio, you can add hello .NET workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="a987e-115">Dans Visual Studio, cliquez sur **Fichier** > **Nouveau** > **Projet**.</span><span class="sxs-lookup"><span data-stu-id="a987e-115">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="a987e-116">Dans **modèles** > **Visual C#**, sélectionnez **l’application Console (.NET Framework)**, entrez *myDotnetProject* nom hello de Hello du projet, emplacement hello sélectionnez hello du projet d’et puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="a987e-116">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-hello-packages"></a><span data-ttu-id="a987e-117">Installer des packages hello</span><span class="sxs-lookup"><span data-stu-id="a987e-117">Install hello packages</span></span>

<span data-ttu-id="a987e-118">Les packages NuGet sont hello plus simple façon tooinstall hello bibliothèques que vous devez toofinish ces étapes.</span><span class="sxs-lookup"><span data-stu-id="a987e-118">NuGet packages are hello easiest way tooinstall hello libraries that you need toofinish these steps.</span></span> <span data-ttu-id="a987e-119">bibliothèques hello tooget dont vous avez besoin dans Visual Studio, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a987e-119">tooget hello libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="a987e-120">Cliquez sur **Outils** > **Gestionnaire de package NuGet**, puis sur **Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="a987e-120">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="a987e-121">Dans la console hello, tapez les commandes :</span><span class="sxs-lookup"><span data-stu-id="a987e-121">Type these commands in hello console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    Install-Package WindowsAzure.Storage
    ```

## <a name="create-hello-files"></a><span data-ttu-id="a987e-122">Créer des fichiers hello</span><span class="sxs-lookup"><span data-stu-id="a987e-122">Create hello files</span></span>

<span data-ttu-id="a987e-123">Dans cette étape, vous créez un fichier de modèle qui déploie les ressources hello et un fichier de paramètres qui fournit le modèle de toohello de valeurs de paramètre.</span><span class="sxs-lookup"><span data-stu-id="a987e-123">In this step, you create a template file that deploys hello resources and a parameters file that supplies parameter values toohello template.</span></span> <span data-ttu-id="a987e-124">Vous créez également un fichier d’autorisation qui est utilisé tooperform Azure Resource Manager operations.</span><span class="sxs-lookup"><span data-stu-id="a987e-124">You also create an authorization file that is used tooperform Azure Resource Manager operations.</span></span>

### <a name="create-hello-template-file"></a><span data-ttu-id="a987e-125">Crée un fichier de modèle hello</span><span class="sxs-lookup"><span data-stu-id="a987e-125">Create hello template file</span></span>

1. <span data-ttu-id="a987e-126">Dans l’Explorateur de solutions, cliquez sur *myDotnetProject* > **Ajouter** > **Nouvel élément**, puis sélectionnez **Fichier texte** dans *Éléments Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="a987e-126">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="a987e-127">Nom de fichier hello *CreateVMTemplate.json*, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a987e-127">Name hello file *CreateVMTemplate.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="a987e-128">Ajoutez ce fichier toohello de code JSON que vous avez créé :</span><span class="sxs-lookup"><span data-stu-id="a987e-128">Add this JSON code toohello file that you created:</span></span>

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

3. <span data-ttu-id="a987e-129">Enregistrez le fichier de CreateVMTemplate.json hello.</span><span class="sxs-lookup"><span data-stu-id="a987e-129">Save hello CreateVMTemplate.json file.</span></span>

### <a name="create-hello-parameters-file"></a><span data-ttu-id="a987e-130">Créer le fichier de paramètres hello</span><span class="sxs-lookup"><span data-stu-id="a987e-130">Create hello parameters file</span></span>

<span data-ttu-id="a987e-131">toospecify les valeurs des paramètres de ressource de hello qui sont définis dans le modèle de hello, vous créez un fichier de paramètres qui contient les valeurs hello.</span><span class="sxs-lookup"><span data-stu-id="a987e-131">toospecify values for hello resource parameters that are defined in hello template, you create a parameters file that contains hello values.</span></span>

1. <span data-ttu-id="a987e-132">Dans l’Explorateur de solutions, cliquez sur *myDotnetProject* > **Ajouter** > **Nouvel élément**, puis sélectionnez **Fichier texte** dans *Éléments Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="a987e-132">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="a987e-133">Nom de fichier hello *Parameters.json*, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a987e-133">Name hello file *Parameters.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="a987e-134">Ajoutez ce fichier toohello de code JSON que vous avez créé :</span><span class="sxs-lookup"><span data-stu-id="a987e-134">Add this JSON code toohello file that you created:</span></span>

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

4. <span data-ttu-id="a987e-135">Enregistrez le fichier de Parameters.json hello.</span><span class="sxs-lookup"><span data-stu-id="a987e-135">Save hello Parameters.json file.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="a987e-136">Créer le fichier d’autorisations de hello</span><span class="sxs-lookup"><span data-stu-id="a987e-136">Create hello authorization file</span></span>

<span data-ttu-id="a987e-137">Avant de pouvoir déployer un modèle, assurez-vous d’avoir accès tooan [principal du service Active Directory](../../resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="a987e-137">Before you can deploy a template, make sure that you have access tooan [Active Directory service principal](../../resource-group-authenticate-service-principal.md).</span></span> <span data-ttu-id="a987e-138">À partir de principal du service hello, vous acquérir un jeton d’authentification des demandes tooAzure Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="a987e-138">From hello service principal, you acquire a token for authenticating requests tooAzure Resource Manager.</span></span> <span data-ttu-id="a987e-139">Vous devez également enregistrer les ID de l’application hello, clé d’authentification hello et ID de client hello dont vous avez besoin dans le fichier d’autorisations de hello.</span><span class="sxs-lookup"><span data-stu-id="a987e-139">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in hello authorization file.</span></span>

1. <span data-ttu-id="a987e-140">Dans l’Explorateur de solutions, cliquez sur *myDotnetProject* > **Ajouter** > **Nouvel élément**, puis sélectionnez **Fichier texte** dans *Éléments Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="a987e-140">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="a987e-141">Nom de fichier hello *azureauth.properties*, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a987e-141">Name hello file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="a987e-142">Ajoutez ces propriétés d’autorisation :</span><span class="sxs-lookup"><span data-stu-id="a987e-142">Add these authorization properties:</span></span>

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

    <span data-ttu-id="a987e-143">Remplacez  **&lt;id d’abonnement&gt;**  avec votre identificateur d’abonnement,  **&lt;id d’application&gt;**  avec hello application Active Directory identificateur,  **&lt;clé d’authentification&gt;**  avec la clé d’application hello, et  **&lt;id de client&gt;**  avec le client de hello identificateur.</span><span class="sxs-lookup"><span data-stu-id="a987e-143">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

3. <span data-ttu-id="a987e-144">Enregistrez le fichier de azureauth.properties hello.</span><span class="sxs-lookup"><span data-stu-id="a987e-144">Save hello azureauth.properties file.</span></span>
4. <span data-ttu-id="a987e-145">La valeur d’une variable d’environnement dans Windows nommé AZURE_AUTH_LOCATION avec les fichiers tooauthorization hello chemin d’accès complet que vous avez créé, par exemple hello suivant PowerShell commande peut être utilisée :</span><span class="sxs-lookup"><span data-stu-id="a987e-145">Set an environment variable in Windows named AZURE_AUTH_LOCATION with hello full path tooauthorization file that you created, for example hello following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```
    
## <a name="create-hello-management-client"></a><span data-ttu-id="a987e-146">Créer le client de gestion hello</span><span class="sxs-lookup"><span data-stu-id="a987e-146">Create hello management client</span></span>

1. <span data-ttu-id="a987e-147">Ouvrir le fichier Program.cs de hello pour le projet hello que vous avez créé, puis ajoutez-les à l’aide de toohello instructions existantes en haut du fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="a987e-147">Open hello Program.cs file for hello project that you created, and then add these using statements toohello existing statements at top of hello file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

2. <span data-ttu-id="a987e-148">client de gestion toocreate hello, ajoutez ce code de toohello méthode Main :</span><span class="sxs-lookup"><span data-stu-id="a987e-148">toocreate hello management client, add this code toohello Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="a987e-149">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="a987e-149">Create a resource group</span></span>

<span data-ttu-id="a987e-150">valeurs toospecify pour l’application hello, ajoutez la méthode Main toohello code :</span><span class="sxs-lookup"><span data-stu-id="a987e-150">toospecify values for hello application, add code toohello Main method:</span></span>

```
var groupName = "myResourceGroup";
var location = Region.USWest;

var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

## <a name="create-a-storage-account"></a><span data-ttu-id="a987e-151">Créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a987e-151">Create a storage account</span></span>

<span data-ttu-id="a987e-152">paramètres et modèle de hello sont déployés à partir d’un compte de stockage dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a987e-152">hello template and parameters are deployed from a storage account in Azure.</span></span> <span data-ttu-id="a987e-153">Dans cette étape, vous créez le compte de hello et téléchargez des fichiers de hello.</span><span class="sxs-lookup"><span data-stu-id="a987e-153">In this step, you create hello account and upload hello files.</span></span> 

<span data-ttu-id="a987e-154">toocreate hello compte, ajoutez ce code de toohello méthode Main :</span><span class="sxs-lookup"><span data-stu-id="a987e-154">toocreate hello account, add this code toohello Main method:</span></span>

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

## <a name="deploy-hello-template"></a><span data-ttu-id="a987e-155">Déployer le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="a987e-155">Deploy hello template</span></span>

<span data-ttu-id="a987e-156">Déployer le modèle de hello et les paramètres de compte de stockage hello qui a été créé.</span><span class="sxs-lookup"><span data-stu-id="a987e-156">Deploy hello template and parameters from hello storage account that was created.</span></span> 

<span data-ttu-id="a987e-157">modèle de hello toodeploy, ajoutez ce code de toohello méthode Main :</span><span class="sxs-lookup"><span data-stu-id="a987e-157">toodeploy hello template, add this code toohello Main method:</span></span>

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

## <a name="delete-hello-resources"></a><span data-ttu-id="a987e-158">Supprimer des ressources de hello</span><span class="sxs-lookup"><span data-stu-id="a987e-158">Delete hello resources</span></span>

<span data-ttu-id="a987e-159">Vous êtes facturé pour les ressources utilisées dans Azure, il est toujours ressources toodelete bonnes pratiques qui ne sont plus nécessaires.</span><span class="sxs-lookup"><span data-stu-id="a987e-159">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="a987e-160">Vous n’avez pas besoin toodelete chaque ressource séparément à partir d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a987e-160">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="a987e-161">Supprimer le groupe de ressources hello et toutes ses ressources sont automatiquement supprimés.</span><span class="sxs-lookup"><span data-stu-id="a987e-161">Delete hello resource group and all its resources are automatically deleted.</span></span> 

<span data-ttu-id="a987e-162">ressource de hello toodelete groupe, ajoutez ce code de toohello méthode Main :</span><span class="sxs-lookup"><span data-stu-id="a987e-162">toodelete hello resource group, add this code toohello Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a><span data-ttu-id="a987e-163">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="a987e-163">Run hello application</span></span>

<span data-ttu-id="a987e-164">Il doit prendre environ cinq minutes pour que cette toorun d’application console complètement à partir de toofinish de début.</span><span class="sxs-lookup"><span data-stu-id="a987e-164">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> 

1. <span data-ttu-id="a987e-165">application de console toorun hello, cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="a987e-165">toorun hello console application, click **Start**.</span></span>

2. <span data-ttu-id="a987e-166">Avant d’appuyer sur **entrée** toostart suppression des ressources, vous pouvez prendre quelques minutes la création de hello tooverify des ressources de hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a987e-166">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="a987e-167">Cliquez sur hello déploiement état toosee plus d’informations sur le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="a987e-167">Click hello deployment status toosee information about hello deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a987e-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a987e-168">Next steps</span></span>
* <span data-ttu-id="a987e-169">S’il existe des problèmes de déploiement de hello, une étape suivante consisterait toolook à [résoudre les erreurs courantes de déploiement Azure avec Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="a987e-169">If there were issues with hello deployment, a next step would be toolook at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="a987e-170">Découvrez comment toodeploy un ordinateur virtuel et ses ressources de prise en charge en consultant [déployer un Azure Virtual Machine à l’aide de C#](csharp.md).</span><span class="sxs-lookup"><span data-stu-id="a987e-170">Learn how toodeploy a virtual machine and its supporting resources by reviewing [Deploy an Azure Virtual Machine Using C#](csharp.md).</span></span>
