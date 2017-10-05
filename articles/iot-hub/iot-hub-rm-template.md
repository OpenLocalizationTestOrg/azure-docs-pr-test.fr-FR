---
title: "Créer un IoT Hub Azure à l’aide d’un modèle (.NET) | Microsoft Docs"
description: "Comment utiliser un modèle Azure Resource Manager pour créer un IoT Hub avec un programme C#."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a447b40c-c728-487e-875d-db554db5adc3
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 0f197a28e0c51b06d0b47a03c29fe1fde0c6b78d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a><span data-ttu-id="aa4fc-103">Créer un IoT Hub avec un modèle Azure Resource Manager (.NET)</span><span class="sxs-lookup"><span data-stu-id="aa4fc-103">Create an IoT hub using Azure Resource Manager template (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="aa4fc-104">Vous pouvez utiliser Azure Resource Manager pour créer et gérer des hubs Azure IoT de façon programmée.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-104">You can use Azure Resource Manager to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="aa4fc-105">Ce didacticiel vous montre comment utiliser un modèle Azure Resource Manager pour créer un IoT Hub à partir d’un programme C#.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-105">This tutorial shows you how to use an Azure Resource Manager template to create an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="aa4fc-106">Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="aa4fc-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="aa4fc-107">Cet article traite de l’utilisation du modèle de déploiement Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-107">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="aa4fc-108">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="aa4fc-108">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="aa4fc-109">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="aa4fc-110">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-110">An active Azure account.</span></span> <br/><span data-ttu-id="aa4fc-111">Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="aa4fc-112">Un [compte Stockage Azure][lnk-storage-account] dans lequel vous pouvez stocker vos fichiers de modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-112">An [Azure Storage account][lnk-storage-account] where you can store your Azure Resource Manager template files.</span></span>
* <span data-ttu-id="aa4fc-113">[Azure PowerShell 1.0][lnk-powershell-install] ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-113">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="aa4fc-114">Préparer votre projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="aa4fc-114">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="aa4fc-115">Dans Visual Studio, créez un projet Visual C# Bureau classique Windows en utilisant le modèle de projet **Application console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-115">In Visual Studio, create a Visual C# Windows Classic Desktop project using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="aa4fc-116">Nommez ce projet **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-116">Name the project **CreateIoTHub**.</span></span>

2. <span data-ttu-id="aa4fc-117">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur votre projet, puis cliquez sur **GÉRER LES PACKAGES NUGET**.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-117">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="aa4fc-118">Dans le gestionnaire de packages NuGet, activez **Inclure la version préliminaire** et sur la page **Parcourir**, recherchez **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-118">In NuGet Package Manager, check **Include prerelease**, and on the **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="aa4fc-119">Sélectionnez le package et cliquez sur **Installer**. Sous **Réviser les modifications**, cliquez sur **OK**, puis sur **J’accepte** pour accepter les licences.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-119">Select the package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the licenses.</span></span>

4. <span data-ttu-id="aa4fc-120">Dans le gestionnaire de packages NuGet, recherchez **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-120">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="aa4fc-121">Cliquez sur **Installer**, dans **Réviser les modifications**, cliquez sur **OK**, puis cliquez sur **J’accepte** pour accepter la licence.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-121">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the license.</span></span>

5. <span data-ttu-id="aa4fc-122">Dans Program.cs, remplacez les instructions **using** existantes par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="aa4fc-122">In Program.cs, replace the existing **using** statements with the following code:</span></span>

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. <span data-ttu-id="aa4fc-123">Dans Program.cs, ajoutez les variables statiques suivantes en remplaçant les valeurs des espaces réservés.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-123">In Program.cs, add the following static variables replacing the placeholder values.</span></span> <span data-ttu-id="aa4fc-124">Vous avez noté les éléments **ApplicationId**, **SubscriptionId**, **TenantId** et **Password** précédemment dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-124">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="aa4fc-125">**Nom de votre compte de stockage Azure** est le nom du compte de stockage Azure où vous stockez vos fichiers de modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-125">**Your Azure Storage account name** is the name of the Azure Storage account where you store your Azure Resource Manager template files.</span></span> <span data-ttu-id="aa4fc-126">**Nom du groupe de ressources** est le nom du groupe de ressources que vous utiliserez pour créer le hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-126">**Resource group name** is the name of the resource group you use when you create the IoT hub.</span></span> <span data-ttu-id="aa4fc-127">Il peut s’agir d’un groupe de ressources existant ou nouveau.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-127">The name can be a pre-existing or new resource group.</span></span> <span data-ttu-id="aa4fc-128">**Nom du déploiement** est le nom du déploiement, par exemple **Déploiement_01**.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-128">**Deployment name** is a name for the deployment, such as **Deployment_01**.</span></span>

    ```csharp
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";
    static string storageAddress = "https://{Your storage account name}.blob.core.windows.net";
    static string rgName = "{Resource group name}";
    static string deploymentName = "{Deployment name}";
    ```

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="submit-a-template-to-create-an-iot-hub"></a><span data-ttu-id="aa4fc-129">Envoyer un modèle pour créer un hub IoT</span><span class="sxs-lookup"><span data-stu-id="aa4fc-129">Submit a template to create an IoT hub</span></span>

<span data-ttu-id="aa4fc-130">Utilisez un fichier de paramètres et un modèle JSON pour créer un IoT Hub dans votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-130">Use a JSON template and parameter file to create an IoT hub in your resource group.</span></span> <span data-ttu-id="aa4fc-131">Vous pouvez également utiliser un modèle Azure Resource Manager pour apporter des modifications à un IoT Hub existant.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-131">You can also use an Azure Resource Manager template to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="aa4fc-132">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur votre projet, cliquez sur **Ajouter**, puis sur **Nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-132">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="aa4fc-133">Ajoutez un fichier JSON appelé **template.json** à votre projet.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-133">Add a JSON file called **template.json** to your project.</span></span>

2. <span data-ttu-id="aa4fc-134">Pour ajouter un IoT Hub standard à la région **Est des États-Unis**, remplacez le contenu de **template.json** par la définition de ressource suivante.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-134">To add a standard IoT hub to the **East US** region, replace the contents of **template.json** with the following resource definition.</span></span> <span data-ttu-id="aa4fc-135">Pour obtenir la liste des régions qui prennent en charge IoT Hub, consultez [Statut Azure][lnk-status] :</span><span class="sxs-lookup"><span data-stu-id="aa4fc-135">For the current list of regions that support IoT Hub see [Azure Status][lnk-status]:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

3. <span data-ttu-id="aa4fc-136">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur votre projet, cliquez sur **Ajouter**, puis sur **Nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-136">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="aa4fc-137">Ajoutez un fichier JSON appelé **parameters.json** à votre projet.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-137">Add a JSON file called **parameters.json** to your project.</span></span>

4. <span data-ttu-id="aa4fc-138">Remplacez le contenu de **parameters.json** avec les informations des paramètres ci-dessous qui définissent le nom du nouvel IoT Hub sur **{vos initiales}mynewiothub**.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-138">Replace the contents of **parameters.json** with the following parameter information that sets a name for the new IoT hub such as **{your initials}mynewiothub**.</span></span> <span data-ttu-id="aa4fc-139">Le nom du IoT Hub doit être globalement unique et inclure votre nom ou vos initiales :</span><span class="sxs-lookup"><span data-stu-id="aa4fc-139">The IoT hub name must be globally unique so it should include your name or initials:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": { "value": "mynewiothub" }
      }
    }
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

5. <span data-ttu-id="aa4fc-140">Dans l’**Explorateur de serveurs**, connectez-vous à votre abonnement Azure et, dans votre compte de stockage Azure, créez un conteneur appelé **modèles**.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-140">In **Server Explorer**, connect to your Azure subscription, and in your Azure Storage account create a container called **templates**.</span></span> <span data-ttu-id="aa4fc-141">Dans le panneau **Propriétés**, définissez les autorisations **Accès public en lecture** pour le conteneur **modèles** sur **Blob**.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-141">In the **Properties** panel, set the **Public Read Access** permissions for the **templates** container to **Blob**.</span></span>

6. <span data-ttu-id="aa4fc-142">Dans l’**Explorateur de serveurs**, cliquez avec le bouton droit sur le conteneur **modèles**, puis cliquez sur **Afficher le conteneur d’objets blob**.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-142">In **Server Explorer**, right-click on the **templates** container and then click **View Blob Container**.</span></span> <span data-ttu-id="aa4fc-143">Cliquez sur le bouton **Télécharger l’objet blob**, sélectionnez les fichiers **parameters.json** et **templates.json**, puis cliquez sur **Ouvrir** pour télécharger les fichiers JSON dans le conteneur **modèles**.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-143">Click the **Upload Blob** button, select the two files, **parameters.json** and **templates.json**, and then click **Open** to upload the JSON files to the **templates** container.</span></span> <span data-ttu-id="aa4fc-144">Les URL des objets blob contenant les données JSON sont :</span><span class="sxs-lookup"><span data-stu-id="aa4fc-144">The URLs of the blobs containing the JSON data are:</span></span>

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. <span data-ttu-id="aa4fc-145">Ajoutez la méthode suivante au fichier Program.cs :</span><span class="sxs-lookup"><span data-stu-id="aa4fc-145">Add the following method to Program.cs:</span></span>

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. <span data-ttu-id="aa4fc-146">Ajoutez le code suivant à la méthode **CreateIoTHub** pour envoyer le fichier de modèle et le fichier de paramètres à Azure Resource Manager :</span><span class="sxs-lookup"><span data-stu-id="aa4fc-146">Add the following code to the **CreateIoTHub** method to submit the template and parameter files to the Azure Resource Manager:</span></span>

    ```csharp
    var createResponse = client.Deployments.CreateOrUpdate(
        rgName,
        deploymentName,
        new Deployment()
        {
          Properties = new DeploymentProperties
          {
            Mode = DeploymentMode.Incremental,
            TemplateLink = new TemplateLink
            {
              Uri = storageAddress + "/templates/template.json"
            },
            ParametersLink = new ParametersLink
            {
              Uri = storageAddress + "/templates/parameters.json"
            }
          }
        });
    ```

9. <span data-ttu-id="aa4fc-147">Ajoutez le code suivant à la méthode **CreateIoTHub** qui affiche l’état et les clés du nouvel IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="aa4fc-147">Add the following code to the **CreateIoTHub** method that displays the status and the keys for the new IoT hub:</span></span>

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed to create iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-the-application"></a><span data-ttu-id="aa4fc-148">Terminer et exécuter l’application</span><span class="sxs-lookup"><span data-stu-id="aa4fc-148">Complete and run the application</span></span>

<span data-ttu-id="aa4fc-149">Vous pouvez maintenant terminer l’application en appelant la méthode **CreateIoTHub** avant sa génération et son exécution.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-149">You can now complete the application by calling the **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="aa4fc-150">Ajoutez le code suivant à la fin de la méthode **Main** :</span><span class="sxs-lookup"><span data-stu-id="aa4fc-150">Add the following code to the end of the **Main** method:</span></span>

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. <span data-ttu-id="aa4fc-151">Cliquez sur **Build**, puis sur **Générer la solution**.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-151">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="aa4fc-152">Corrigez les éventuelles erreurs.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-152">Correct any errors.</span></span>

3. <span data-ttu-id="aa4fc-153">Cliquez sur **Déboguer**, puis **Démarrer le débogage** pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-153">Click **Debug** and then **Start Debugging** to run the application.</span></span> <span data-ttu-id="aa4fc-154">Le déploiement peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-154">It may take several minutes for the deployment to run.</span></span>

4. <span data-ttu-id="aa4fc-155">Pour vérifier que votre application a bien ajouté le nouvel IoT Hub, accédez au [portail Azure][lnk-azure-portal] et affichez votre liste de ressources.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-155">To verify your application added the new IoT hub, visit the [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="aa4fc-156">Vous pouvez également utiliser l’applet de commande PowerShell **Get-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-156">Alternatively, use the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="aa4fc-157">Cet exemple d’application ajoute un IoT Hub S1 Standard qui vous est facturé.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-157">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="aa4fc-158">Lorsque vous avez terminé, vous pouvez supprimer le IoT Hub via le [portail Azure][lnk-azure-portal] ou à l’aide de l’applet de commande PowerShell **Remove-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="aa4fc-158">You can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa4fc-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aa4fc-159">Next steps</span></span>
<span data-ttu-id="aa4fc-160">Maintenant que vous avez déployé un IoT Hub à l’aide d’un modèle Azure Resource Manager avec un programme C#, vous pouvez aller encore plus loin :</span><span class="sxs-lookup"><span data-stu-id="aa4fc-160">Now you have deployed an IoT hub using an Azure Resource Manager template with a C# program, you may want to explore further:</span></span>

* <span data-ttu-id="aa4fc-161">Découvrez les capacités de [l’API REST du fournisseur de ressources IoT Hub][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="aa4fc-161">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="aa4fc-162">Pour plus d’informations sur les capacités d’Azure Resource Manager, voir [Vue d’ensemble d’Azure Resource Manager][lnk-azure-rm-overview].</span><span class="sxs-lookup"><span data-stu-id="aa4fc-162">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="aa4fc-163">Pour en savoir plus sur le développement pour IoT Hub, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="aa4fc-163">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="aa4fc-164">[Présentation du Kit de développement logiciel (SDK) C][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="aa4fc-164">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="aa4fc-165">[Kits de développement logiciel (SDK) Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="aa4fc-165">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="aa4fc-166">Pour explorer davantage les capacités de IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="aa4fc-166">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="aa4fc-167">[Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="aa4fc-167">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-storage-account]:../storage/common/storage-create-storage-account.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
