---
title: "Création d’un IoT Hub Azure à l’aide de l’API REST du fournisseur de ressources | Microsoft Docs"
description: "Utilisation de l’API REST du fournisseur de ressources pour créer un IoT Hub."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 52814ee5-bc10-4abe-9eb2-f8973096c2d8
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: e443259507aacbefca141be4c9c1688ab19bf6ec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-iot-hub-using-the-resource-provider-rest-api-net"></a><span data-ttu-id="b56b8-103">Création d’un IoT Hub à l’aide de l’API REST du fournisseur de ressources (.NET)</span><span class="sxs-lookup"><span data-stu-id="b56b8-103">Create an IoT hub using the resource provider REST API (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="b56b8-104">Vous pouvez utiliser [l’API REST du fournisseur de ressources IoT Hub][lnk-rest-api] pour créer et gérer des IoT Hubs Azure par programme.</span><span class="sxs-lookup"><span data-stu-id="b56b8-104">You can use the [IoT Hub resource provider REST API][lnk-rest-api] to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="b56b8-105">Ce didacticiel vous montre comment utiliser l’API REST du fournisseur de ressources IoT Hub pour créer un IoT Hub à partir d’un programme C#.</span><span class="sxs-lookup"><span data-stu-id="b56b8-105">This tutorial shows you how to use the IoT Hub resource provider REST API to create an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="b56b8-106">Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b56b8-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="b56b8-107">Cet article traite de l’utilisation du modèle de déploiement Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b56b8-107">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="b56b8-108">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b56b8-108">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="b56b8-109">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="b56b8-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="b56b8-110">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="b56b8-110">An active Azure account.</span></span> <br/><span data-ttu-id="b56b8-111">Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="b56b8-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="b56b8-112">[Azure PowerShell 1.0][lnk-powershell-install] ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="b56b8-112">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="b56b8-113">Préparer votre projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b56b8-113">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="b56b8-114">Dans Visual Studio, créez un projet Visual C# Bureau classique Windows en utilisant le modèle de projet **Application console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="b56b8-114">In Visual Studio, create a Visual C# Windows Classic Desktop project using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="b56b8-115">Nommez ce projet **CreateIoTHubREST**.</span><span class="sxs-lookup"><span data-stu-id="b56b8-115">Name the project **CreateIoTHubREST**.</span></span>

2. <span data-ttu-id="b56b8-116">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur votre projet, puis cliquez sur **GÉRER LES PACKAGES NUGET**.</span><span class="sxs-lookup"><span data-stu-id="b56b8-116">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="b56b8-117">Dans le gestionnaire de packages NuGet, activez **Inclure la version préliminaire** et sur la page **Parcourir**, recherchez **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="b56b8-117">In NuGet Package Manager, check **Include prerelease**, and on the **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="b56b8-118">Sélectionnez le package et cliquez sur **Installer**. Sous **Réviser les modifications**, cliquez sur **OK**, puis sur **J’accepte** pour accepter les licences.</span><span class="sxs-lookup"><span data-stu-id="b56b8-118">Select the package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the licenses.</span></span>

4. <span data-ttu-id="b56b8-119">Dans le gestionnaire de packages NuGet, recherchez **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="b56b8-119">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="b56b8-120">Cliquez sur **Installer**, dans **Réviser les modifications**, cliquez sur **OK**, puis cliquez sur **J’accepte** pour accepter la licence.</span><span class="sxs-lookup"><span data-stu-id="b56b8-120">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the license.</span></span>

5. <span data-ttu-id="b56b8-121">Dans Program.cs, remplacez les instructions **using** existantes par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="b56b8-121">In Program.cs, replace the existing **using** statements with the following code:</span></span>

    ```csharp
    using System;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Text;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Newtonsoft.Json;
    using Microsoft.Rest;
    using System.Linq;
    using System.Threading;
    ```

6. <span data-ttu-id="b56b8-122">Dans Program.cs, ajoutez les variables statiques suivantes en remplaçant les valeurs des espaces réservés.</span><span class="sxs-lookup"><span data-stu-id="b56b8-122">In Program.cs, add the following static variables replacing the placeholder values.</span></span> <span data-ttu-id="b56b8-123">Vous avez noté les éléments **ApplicationId**, **SubscriptionId**, **TenantId** et **Password** précédemment dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="b56b8-123">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="b56b8-124">**Nom du groupe de ressources** est le nom du groupe de ressources que vous utiliserez pour créer le hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b56b8-124">**Resource group name** is the name of the resource group you use when you create the IoT hub.</span></span> <span data-ttu-id="b56b8-125">Vous pouvez utiliser un groupe de ressources nouveau ou préexistant.</span><span class="sxs-lookup"><span data-stu-id="b56b8-125">You can use a pre-existing or a new resource group.</span></span> <span data-ttu-id="b56b8-126">**Nom du hub IoT** est le nom de l’IoT Hub que vous créez, par exemple **MonIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="b56b8-126">**IoT Hub name** is the name of the IoT Hub you create, such as **MyIoTHub**.</span></span> <span data-ttu-id="b56b8-127">Le nom de votre IoT Hub doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="b56b8-127">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="b56b8-128">**Nom du déploiement** est le nom du déploiement, par exemple **Déploiement_01**.</span><span class="sxs-lookup"><span data-stu-id="b56b8-128">**Deployment name** is a name for the deployment, such as **Deployment_01**.</span></span>

    ```csharp
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";

    static string rgName = "{Resource group name}";
    static string iotHubName = "{IoT Hub name including your initials}";
    ```
[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="use-the-resource-provider-rest-api-to-create-an-iot-hub"></a><span data-ttu-id="b56b8-129">Utilisation de l’API REST du fournisseur de ressources pour créer un IoT Hub</span><span class="sxs-lookup"><span data-stu-id="b56b8-129">Use the resource provider REST API to create an IoT hub</span></span>

<span data-ttu-id="b56b8-130">Utilisez [l’API REST du fournisseur de ressources IoT Hub][lnk-rest-api] pour créer un IoT Hub dans votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b56b8-130">Use the [IoT Hub resource provider REST API][lnk-rest-api] to create an IoT hub in your resource group.</span></span> <span data-ttu-id="b56b8-131">Vous pouvez également utiliser l’API REST du fournisseur de ressources pour apporter des modifications à un IoT Hub existant.</span><span class="sxs-lookup"><span data-stu-id="b56b8-131">You can also use the resource provider REST API to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="b56b8-132">Ajoutez la méthode suivante au fichier Program.cs :</span><span class="sxs-lookup"><span data-stu-id="b56b8-132">Add the following method to Program.cs:</span></span>

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. <span data-ttu-id="b56b8-133">Ajoutez le code suivant à la méthode **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="b56b8-133">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="b56b8-134">Ce code crée un objet **HttpClient** avec le jeton d’authentification dans les en-têtes :</span><span class="sxs-lookup"><span data-stu-id="b56b8-134">This code creates an **HttpClient** object with the authentication token in the headers:</span></span>

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. <span data-ttu-id="b56b8-135">Ajoutez le code suivant à la méthode **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="b56b8-135">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="b56b8-136">Ce code décrit l’IoT Hub à créer et génère une représentation JSON.</span><span class="sxs-lookup"><span data-stu-id="b56b8-136">This code describes the IoT hub to create and generates a JSON representation.</span></span> <span data-ttu-id="b56b8-137">Pour obtenir la liste des emplacements qui prennent en charge IoT Hub, consultez [Statut Azure][lnk-status] :</span><span class="sxs-lookup"><span data-stu-id="b56b8-137">For the current list of locations that support IoT Hub see [Azure Status][lnk-status]:</span></span>

    ```csharp
    var description = new
    {
      name = iotHubName,
      location = "East US",
      sku = new
      {
        name = "S1",
        tier = "Standard",
        capacity = 1
      }
    };

    var json = JsonConvert.SerializeObject(description, Formatting.Indented);
    ```

4. <span data-ttu-id="b56b8-138">Ajoutez le code suivant à la méthode **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="b56b8-138">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="b56b8-139">Ce code envoie la demande REST à Azure.</span><span class="sxs-lookup"><span data-stu-id="b56b8-139">This code submits the REST request to Azure.</span></span> <span data-ttu-id="b56b8-140">Il vérifie ensuite la réponse et récupère l’URL que vous pouvez utiliser pour surveiller l’état de la tâche de déploiement :</span><span class="sxs-lookup"><span data-stu-id="b56b8-140">The code then checks the response and retrieves the URL you can use to monitor the state of the deployment task:</span></span>

    ```csharp
    var content = new StringContent(JsonConvert.SerializeObject(description), Encoding.UTF8, "application/json");
    var requestUri = string.Format("https://management.azure.com/subscriptions/{0}/resourcegroups/{1}/providers/Microsoft.devices/IotHubs/{2}?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var result = client.PutAsync(requestUri, content).Result;

    if (!result.IsSuccessStatusCode)
    {
      Console.WriteLine("Failed {0}", result.Content.ReadAsStringAsync().Result);
      return;
    }

    var asyncStatusUri = result.Headers.GetValues("Azure-AsyncOperation").First();
    ```

5. <span data-ttu-id="b56b8-141">Ajoutez le code suivant à la fin de la méthode **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="b56b8-141">Add the following code to the end of the **CreateIoTHub** method.</span></span> <span data-ttu-id="b56b8-142">Ce code utilise l’adresse **asyncStatusUri** récupérée à l’étape précédente pour attendre la fin du déploiement :</span><span class="sxs-lookup"><span data-stu-id="b56b8-142">This code uses the **asyncStatusUri** address retrieved in the previous step to wait for the deployment to complete:</span></span>

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. <span data-ttu-id="b56b8-143">Ajoutez le code suivant à la fin de la méthode **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="b56b8-143">Add the following code to the end of the **CreateIoTHub** method.</span></span> <span data-ttu-id="b56b8-144">Ce code récupère les clés de l’IoT Hub que vous avez créé et les imprime sur la console :</span><span class="sxs-lookup"><span data-stu-id="b56b8-144">This code retrieves the keys of the IoT hub you created and prints them to the console:</span></span>

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-the-application"></a><span data-ttu-id="b56b8-145">Terminer et exécuter l’application</span><span class="sxs-lookup"><span data-stu-id="b56b8-145">Complete and run the application</span></span>

<span data-ttu-id="b56b8-146">Vous pouvez maintenant terminer l’application en appelant la méthode **CreateIoTHub** avant sa génération et son exécution.</span><span class="sxs-lookup"><span data-stu-id="b56b8-146">You can now complete the application by calling the **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="b56b8-147">Ajoutez le code suivant à la fin de la méthode **Main** :</span><span class="sxs-lookup"><span data-stu-id="b56b8-147">Add the following code to the end of the **Main** method:</span></span>

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. <span data-ttu-id="b56b8-148">Cliquez sur **Build**, puis sur **Générer la solution**.</span><span class="sxs-lookup"><span data-stu-id="b56b8-148">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="b56b8-149">Corrigez les éventuelles erreurs.</span><span class="sxs-lookup"><span data-stu-id="b56b8-149">Correct any errors.</span></span>

3. <span data-ttu-id="b56b8-150">Cliquez sur **Déboguer**, puis **Démarrer le débogage** pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="b56b8-150">Click **Debug** and then **Start Debugging** to run the application.</span></span> <span data-ttu-id="b56b8-151">Le déploiement peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="b56b8-151">It may take several minutes for the deployment to run.</span></span>

4. <span data-ttu-id="b56b8-152">Pour vérifier que votre application a bien ajouté le nouvel IoT Hub, accédez au [portail Azure][lnk-azure-portal] et affichez votre liste de ressources.</span><span class="sxs-lookup"><span data-stu-id="b56b8-152">To verify that your application added the new IoT hub, visit the [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="b56b8-153">Vous pouvez également utiliser l’applet de commande PowerShell **Get-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="b56b8-153">Alternatively, use the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="b56b8-154">Cet exemple d’application ajoute un IoT Hub S1 Standard qui vous est facturé.</span><span class="sxs-lookup"><span data-stu-id="b56b8-154">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="b56b8-155">Lorsque vous avez terminé, vous pouvez supprimer le IoT Hub par le biais du [portail Azure][lnk-azure-portal] ou à l’aide de l’applet de commande PowerShell **Remove-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="b56b8-155">When you are finished, you can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b56b8-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b56b8-156">Next steps</span></span>
<span data-ttu-id="b56b8-157">Maintenant que vous avez déployé un IoT Hub à l’aide de l’API REST du fournisseur de ressources, vous pouvez aller encore plus loin :</span><span class="sxs-lookup"><span data-stu-id="b56b8-157">Now you have deployed an IoT hub using the resource provider REST API, you may want to explore further:</span></span>

* <span data-ttu-id="b56b8-158">Découvrez les capacités de [l’API REST du fournisseur de ressources IoT Hub][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="b56b8-158">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="b56b8-159">Pour plus d’informations sur les capacités d’Azure Resource Manager, voir [Vue d’ensemble d’Azure Resource Manager][lnk-azure-rm-overview].</span><span class="sxs-lookup"><span data-stu-id="b56b8-159">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="b56b8-160">Pour en savoir plus sur le développement pour IoT Hub, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="b56b8-160">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="b56b8-161">[Présentation du Kit de développement logiciel (SDK) C][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="b56b8-161">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="b56b8-162">[Kits de développement logiciel (SDK) Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="b56b8-162">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="b56b8-163">Pour explorer davantage les capacités de IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="b56b8-163">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="b56b8-164">[Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="b56b8-164">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
