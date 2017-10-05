---
title: "Déployer une machine virtuelle à l’aide de C# et d’un modèle Resource Manager | Microsoft Docs"
description: "Apprenez à utiliser C# et un modèle Resource Manager pour déployer une machine virtuelle Azure."
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
ms.openlocfilehash: bd1c860db026f948202cd1f3aa763b4547c597b4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a><span data-ttu-id="e685f-103">Déployer une machine virtuelle Azure à l’aide de C# et d’un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e685f-103">Deploy an Azure Virtual Machine using C# and a Resource Manager template</span></span>
<span data-ttu-id="e685f-104">Cet article explique la procédure de déploiement d’un modèle Azure Resource Manager à l’aide de C#.</span><span class="sxs-lookup"><span data-stu-id="e685f-104">This article shows you how to deploy an Azure Resource Manager template using C#.</span></span> <span data-ttu-id="e685f-105">Le modèle que vous créez déploie une machine virtuelle unique exécutant Windows Server dans un nouveau réseau virtuel avec un seul sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="e685f-105">The template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="e685f-106">Pour obtenir une description détaillée de la ressource de machine virtuelle, consultez [Virtual machines in an Azure Resource Manager template (Machines virtuelles dans un modèle Azure Resource Manager)](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="e685f-106">For a detailed description of the virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="e685f-107">Pour plus d’informations sur toutes les ressources d’un modèle, consultez [Guide de création d’un modèle Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="e685f-107">For more information about all the resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="e685f-108">Ces étapes prennent environ 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="e685f-108">It takes about 10 minutes to do these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="e685f-109">Créer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e685f-109">Create a Visual Studio project</span></span>

<span data-ttu-id="e685f-110">Lors de cette étape, assurez-vous que Visual Studio est installé et que vous créez une application console utilisée pour déployer le modèle.</span><span class="sxs-lookup"><span data-stu-id="e685f-110">In this step, you make sure that Visual Studio is installed and you create a console application used to deploy the template.</span></span>

1. <span data-ttu-id="e685f-111">Si vous ne l’avez pas déjà fait, installez [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="e685f-111">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="e685f-112">Sélectionnez **Développement .NET Desktop** dans la page Charges de travail, puis cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="e685f-112">Select **.NET desktop development** on the Workloads page, and then click **Install**.</span></span> <span data-ttu-id="e685f-113">Dans le résumé, vous pouvez voir que les **Outils de développement .NET Framework 4 - 4.6** sont automatiquement sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="e685f-113">In the summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="e685f-114">Si vous avez déjà installé Visual Studio, vous pouvez ajouter la charge de travail .NET en utilisant le lanceur Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e685f-114">If you have already installed Visual Studio, you can add the .NET workload using the Visual Studio Launcher.</span></span>
2. <span data-ttu-id="e685f-115">Dans Visual Studio, cliquez sur **Fichier** > **Nouveau** > **Projet**.</span><span class="sxs-lookup"><span data-stu-id="e685f-115">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="e685f-116">Dans **Modèles** > **Visual C#**, sélectionnez **Application console (.NET Framework)**, entrez le nom de projet *myDotnetProject*, sélectionnez l’emplacement du projet, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e685f-116">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for the name of the project, select the location of the project, and then click **OK**.</span></span>

## <a name="install-the-packages"></a><span data-ttu-id="e685f-117">Installer les packages</span><span class="sxs-lookup"><span data-stu-id="e685f-117">Install the packages</span></span>

<span data-ttu-id="e685f-118">Les packages NuGet sont le moyen le plus simple pour installer les bibliothèques dont vous avez besoin pour terminer ces étapes.</span><span class="sxs-lookup"><span data-stu-id="e685f-118">NuGet packages are the easiest way to install the libraries that you need to finish these steps.</span></span> <span data-ttu-id="e685f-119">Pour obtenir les bibliothèques dont vous avez besoin dans Visual Studio, suivez ces étapes :</span><span class="sxs-lookup"><span data-stu-id="e685f-119">To get the libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="e685f-120">Cliquez sur **Outils** > **Gestionnaire de package NuGet**, puis sur **Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="e685f-120">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="e685f-121">Dans la console, tapez ces commandes :</span><span class="sxs-lookup"><span data-stu-id="e685f-121">Type these commands in the console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    Install-Package WindowsAzure.Storage
    ```

## <a name="create-the-files"></a><span data-ttu-id="e685f-122">Créer les fichiers</span><span class="sxs-lookup"><span data-stu-id="e685f-122">Create the files</span></span>

<span data-ttu-id="e685f-123">Lors de cette étape, vous créez un fichier de modèle qui déploie les ressources et un fichier de paramètres qui fournit les valeurs des paramètres au modèle.</span><span class="sxs-lookup"><span data-stu-id="e685f-123">In this step, you create a template file that deploys the resources and a parameters file that supplies parameter values to the template.</span></span> <span data-ttu-id="e685f-124">Vous créez également un fichier d’autorisation qui est utilisé pour effectuer des opérations Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e685f-124">You also create an authorization file that is used to perform Azure Resource Manager operations.</span></span>

### <a name="create-the-template-file"></a><span data-ttu-id="e685f-125">Créer le fichier de modèle</span><span class="sxs-lookup"><span data-stu-id="e685f-125">Create the template file</span></span>

1. <span data-ttu-id="e685f-126">Dans l’Explorateur de solutions, cliquez sur *myDotnetProject* > **Ajouter** > **Nouvel élément**, puis sélectionnez **Fichier texte** dans *Éléments Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="e685f-126">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="e685f-127">Nommez le fichier *CreateVMTemplate.json*, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e685f-127">Name the file *CreateVMTemplate.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="e685f-128">Ajoutez ce code JSON au fichier que vous avez créé :</span><span class="sxs-lookup"><span data-stu-id="e685f-128">Add this JSON code to the file that you created:</span></span>

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

3. <span data-ttu-id="e685f-129">Enregistrez le fichier CreateVMTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="e685f-129">Save the CreateVMTemplate.json file.</span></span>

### <a name="create-the-parameters-file"></a><span data-ttu-id="e685f-130">Créer le fichier de paramètres</span><span class="sxs-lookup"><span data-stu-id="e685f-130">Create the parameters file</span></span>

<span data-ttu-id="e685f-131">Pour spécifier des valeurs pour les paramètres de ressource qui ont été définis dans le modèle, créez un fichier de paramètres qui contient les valeurs.</span><span class="sxs-lookup"><span data-stu-id="e685f-131">To specify values for the resource parameters that are defined in the template, you create a parameters file that contains the values.</span></span>

1. <span data-ttu-id="e685f-132">Dans l’Explorateur de solutions, cliquez sur *myDotnetProject* > **Ajouter** > **Nouvel élément**, puis sélectionnez **Fichier texte** dans *Éléments Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="e685f-132">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="e685f-133">Nommez le fichier *Parameters.json*, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e685f-133">Name the file *Parameters.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="e685f-134">Ajoutez ce code JSON au fichier que vous avez créé :</span><span class="sxs-lookup"><span data-stu-id="e685f-134">Add this JSON code to the file that you created:</span></span>

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

4. <span data-ttu-id="e685f-135">Enregistrez le fichier Parameters.json.</span><span class="sxs-lookup"><span data-stu-id="e685f-135">Save the Parameters.json file.</span></span>

### <a name="create-the-authorization-file"></a><span data-ttu-id="e685f-136">Créer le fichier d’autorisation</span><span class="sxs-lookup"><span data-stu-id="e685f-136">Create the authorization file</span></span>

<span data-ttu-id="e685f-137">Avant de commencer cette étape, vérifiez que vous avez accès à un [principal de service Active Directory](../../resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="e685f-137">Before you can deploy a template, make sure that you have access to an [Active Directory service principal](../../resource-group-authenticate-service-principal.md).</span></span> <span data-ttu-id="e685f-138">Dans le principal de service, vous obtenez le jeton d'authentification des demandes pour Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e685f-138">From the service principal, you acquire a token for authenticating requests to Azure Resource Manager.</span></span> <span data-ttu-id="e685f-139">Vous devez également enregistrer l’ID d’application, la clé d’authentification et l’ID de locataire dont vous avez besoin dans le fichier d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="e685f-139">You should also record the application ID, the authentication key, and the tenant ID that you need in the authorization file.</span></span>

1. <span data-ttu-id="e685f-140">Dans l’Explorateur de solutions, cliquez sur *myDotnetProject* > **Ajouter** > **Nouvel élément**, puis sélectionnez **Fichier texte** dans *Éléments Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="e685f-140">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="e685f-141">Nommez le fichier *azureauth.properties*, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e685f-141">Name the file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="e685f-142">Ajoutez ces propriétés d’autorisation :</span><span class="sxs-lookup"><span data-stu-id="e685f-142">Add these authorization properties:</span></span>

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

    <span data-ttu-id="e685f-143">Remplacez **&lt;subscription-id&gt;** par votre identificateur d’abonnement, **&lt;application-id&gt;** par l’identificateur d’application Active Directory, **&lt;authentication-key&gt;** par la clé d’application et **&lt;tenant-id&gt;** par l’identificateur du locataire.</span><span class="sxs-lookup"><span data-stu-id="e685f-143">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with the Active Directory application identifier, **&lt;authentication-key&gt;** with the application key, and **&lt;tenant-id&gt;** with the tenant identifier.</span></span>

3. <span data-ttu-id="e685f-144">Enregistrez le fichier azureauth.properties.</span><span class="sxs-lookup"><span data-stu-id="e685f-144">Save the azureauth.properties file.</span></span>
4. <span data-ttu-id="e685f-145">Définissez une variable d’environnement dans Windows nommée AZURE_AUTH_LOCATION avec le chemin complet au fichier d’autorisation que vous avez créé. Vous pouvez par exemple utiliser la commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="e685f-145">Set an environment variable in Windows named AZURE_AUTH_LOCATION with the full path to authorization file that you created, for example the following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```
    
## <a name="create-the-management-client"></a><span data-ttu-id="e685f-146">Créer le client de gestion</span><span class="sxs-lookup"><span data-stu-id="e685f-146">Create the management client</span></span>

1. <span data-ttu-id="e685f-147">Ouvrez le fichier Program.cs du projet que vous avez créé, puis ajoutez les instructions suivantes à celles qui existent au début du fichier :</span><span class="sxs-lookup"><span data-stu-id="e685f-147">Open the Program.cs file for the project that you created, and then add these using statements to the existing statements at top of the file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

2. <span data-ttu-id="e685f-148">Pour créer le client de gestion, ajoutez ce code à la méthode Main :</span><span class="sxs-lookup"><span data-stu-id="e685f-148">To create the management client, add this code to the Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="e685f-149">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="e685f-149">Create a resource group</span></span>

<span data-ttu-id="e685f-150">Pour spécifier des valeurs pour l’application, ajoutez du code à la méthode Main :</span><span class="sxs-lookup"><span data-stu-id="e685f-150">To specify values for the application, add code to the Main method:</span></span>

```
var groupName = "myResourceGroup";
var location = Region.USWest;

var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

## <a name="create-a-storage-account"></a><span data-ttu-id="e685f-151">Créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="e685f-151">Create a storage account</span></span>

<span data-ttu-id="e685f-152">Le modèle et les paramètres sont déployés à partir d’un compte de stockage dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e685f-152">The template and parameters are deployed from a storage account in Azure.</span></span> <span data-ttu-id="e685f-153">Lors de cette étape, vous créez le compte et chargez les fichiers.</span><span class="sxs-lookup"><span data-stu-id="e685f-153">In this step, you create the account and upload the files.</span></span> 

<span data-ttu-id="e685f-154">Pour créer le compte, ajoutez ce code à la méthode Main :</span><span class="sxs-lookup"><span data-stu-id="e685f-154">To create the account, add this code to the Main method:</span></span>

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

## <a name="deploy-the-template"></a><span data-ttu-id="e685f-155">Déployer le modèle</span><span class="sxs-lookup"><span data-stu-id="e685f-155">Deploy the template</span></span>

<span data-ttu-id="e685f-156">Déployez le modèle et les paramètres du compte de stockage que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="e685f-156">Deploy the template and parameters from the storage account that was created.</span></span> 

<span data-ttu-id="e685f-157">Pour déployer le modèle, ajoutez ce code à la méthode Main :</span><span class="sxs-lookup"><span data-stu-id="e685f-157">To deploy the template, add this code to the Main method:</span></span>

```
var templatePath = "https://" + storageAccountName + ".blob.core.windows.net/templates/CreateVMTemplate.json";
var paramPath = "https://" + storageAccountName + ".blob.core.windows.net/templates/Parameters.json";
var deployment = azure.Deployments.Define("myDeployment")
    .WithExistingResourceGroup(groupName)
    .WithTemplateLink(templatePath, "1.0.0.0")
    .WithParametersLink(paramPath, "1.0.0.0")
    .WithMode(Microsoft.Azure.Management.ResourceManager.Fluent.Models.DeploymentMode.Incremental)
    .Create();
Console.WriteLine("Press enter to delete the resource group...");
Console.ReadLine();
```

## <a name="delete-the-resources"></a><span data-ttu-id="e685f-158">Supprimer les ressources</span><span class="sxs-lookup"><span data-stu-id="e685f-158">Delete the resources</span></span>

<span data-ttu-id="e685f-159">Étant donné que les ressources utilisées dans Microsoft Azure vous sont facturées, il est toujours conseillé de supprimer les ressources qui ne sont plus nécessaires.</span><span class="sxs-lookup"><span data-stu-id="e685f-159">Because you are charged for resources used in Azure, it is always good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="e685f-160">Vous n’avez pas besoin de supprimer séparément les ressources d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e685f-160">You don’t need to delete each resource separately from a resource group.</span></span> <span data-ttu-id="e685f-161">Supprimez le groupe de ressources pour supprimer automatiquement toutes ses ressources.</span><span class="sxs-lookup"><span data-stu-id="e685f-161">Delete the resource group and all its resources are automatically deleted.</span></span> 

<span data-ttu-id="e685f-162">Pour supprimer le groupe de ressources, ajoutez ce code à la méthode Main :</span><span class="sxs-lookup"><span data-stu-id="e685f-162">To delete the resource group, add this code to the Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-the-application"></a><span data-ttu-id="e685f-163">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="e685f-163">Run the application</span></span>

<span data-ttu-id="e685f-164">L’exécution complète de cette application console devrait durer cinq minutes environ.</span><span class="sxs-lookup"><span data-stu-id="e685f-164">It should take about five minutes for this console application to run completely from start to finish.</span></span> 

1. <span data-ttu-id="e685f-165">Pour exécuter l’application console, cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="e685f-165">To run the console application, click **Start**.</span></span>

2. <span data-ttu-id="e685f-166">Avant d’appuyer sur **Entrée** pour démarrer la suppression des ressources, prenez quelques minutes pour vérifier que les ressources dans le portail Azure ont bien été créées.</span><span class="sxs-lookup"><span data-stu-id="e685f-166">Before you press **Enter** to start deleting resources, you could take a few minutes to verify the creation of the resources in the Azure portal.</span></span> <span data-ttu-id="e685f-167">Cliquez sur l’état du déploiement pour afficher des informations sur le déploiement.</span><span class="sxs-lookup"><span data-stu-id="e685f-167">Click the deployment status to see information about the deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e685f-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e685f-168">Next steps</span></span>
* <span data-ttu-id="e685f-169">Si vous rencontrez des problèmes lors du déploiement, nous vous conseillons de consulter la section [Résolution des erreurs courantes dans un déploiement Azure avec Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="e685f-169">If there were issues with the deployment, a next step would be to look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="e685f-170">Découvrez comment déployer une machine virtuelle et ses ressources de soutien en consultant [Déployer une machine virtuelle Azure à l’aide de C#](csharp.md).</span><span class="sxs-lookup"><span data-stu-id="e685f-170">Learn how to deploy a virtual machine and its supporting resources by reviewing [Deploy an Azure Virtual Machine Using C#](csharp.md).</span></span>
