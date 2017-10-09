---
title: "un hub IoT d’Azure à l’aide d’aaaCreate hello fournisseur de ressources API REST | Documents Microsoft"
description: Comment toouse hello toocreate de API REST de fournisseur de ressources un IoT Hub.
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
ms.openlocfilehash: 98d240ccce47dec13a255bce28943b40f5354ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-resource-provider-rest-api-net"></a><span data-ttu-id="1ba5f-103">Créez un IoT hub à l’aide du fournisseur de ressources hello REST API (.NET)</span><span class="sxs-lookup"><span data-stu-id="1ba5f-103">Create an IoT hub using hello resource provider REST API (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="1ba5f-104">Vous pouvez utiliser hello [fournisseur de ressources IoT Hub API REST] [ lnk-rest-api] toocreate et gérer les hubs Azure IoT par programme.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-104">You can use hello [IoT Hub resource provider REST API][lnk-rest-api] toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="1ba5f-105">Ce didacticiel vous montre comment toouse hello toocreate de API REST de fournisseur de ressources IoT Hub un IoT hub à partir d’un programme c#.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-105">This tutorial shows you how toouse hello IoT Hub resource provider REST API toocreate an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="1ba5f-106">Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="1ba5f-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="1ba5f-107">Cet article décrit à l’aide du modèle de déploiement du Gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="1ba5f-108">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="1ba5f-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="1ba5f-109">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="1ba5f-110">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-110">An active Azure account.</span></span> <br/><span data-ttu-id="1ba5f-111">Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="1ba5f-112">[Azure PowerShell 1.0][lnk-powershell-install] ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-112">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="1ba5f-113">Préparer votre projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ba5f-113">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="1ba5f-114">Dans Visual Studio, créez un projet Visual c# bureau classique de Windows à l’aide de hello **l’application Console (.NET Framework)** modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-114">In Visual Studio, create a Visual C# Windows Classic Desktop project using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="1ba5f-115">Projet de hello nom **CreateIoTHubREST**.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-115">Name hello project **CreateIoTHubREST**.</span></span>

2. <span data-ttu-id="1ba5f-116">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur votre projet, puis cliquez sur **GÉRER LES PACKAGES NUGET**.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-116">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="1ba5f-117">Dans le Gestionnaire de Package NuGet, vérifiez **inclure la version préliminaire**et sur hello **Parcourir** recherche de page pour **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-117">In NuGet Package Manager, check **Include prerelease**, and on hello **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="1ba5f-118">Sélectionnez le package de hello, cliquez sur **installer**, dans **réviser les modifications** cliquez sur **OK**, puis cliquez sur **J’accepte** tooaccept des licences hello.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-118">Select hello package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello licenses.</span></span>

4. <span data-ttu-id="1ba5f-119">Dans le gestionnaire de packages NuGet, recherchez **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-119">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="1ba5f-120">Cliquez sur **installer**, dans **réviser les modifications** cliquez sur **OK**, puis cliquez sur **J’accepte** licence de hello tooaccept.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-120">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello license.</span></span>

5. <span data-ttu-id="1ba5f-121">Dans le fichier Program.cs, remplacer hello **à l’aide de** instructions avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="1ba5f-121">In Program.cs, replace hello existing **using** statements with hello following code:</span></span>

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

6. <span data-ttu-id="1ba5f-122">Dans Program.cs, ajoutez hello suivant en remplaçant les valeurs d’espace réservé hello de variables statiques.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-122">In Program.cs, add hello following static variables replacing hello placeholder values.</span></span> <span data-ttu-id="1ba5f-123">Vous avez noté les éléments **ApplicationId**, **SubscriptionId**, **TenantId** et **Password** précédemment dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-123">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="1ba5f-124">**Nom de groupe de ressources** est le nom hello hello du groupe de ressources vous utilisez quand vous créez hello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-124">**Resource group name** is hello name of hello resource group you use when you create hello IoT hub.</span></span> <span data-ttu-id="1ba5f-125">Vous pouvez utiliser un groupe de ressources nouveau ou préexistant.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-125">You can use a pre-existing or a new resource group.</span></span> <span data-ttu-id="1ba5f-126">**Nom d’IoT Hub** hello désigne hello IoT Hub, vous créez, tel que **MyIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-126">**IoT Hub name** is hello name of hello IoT Hub you create, such as **MyIoTHub**.</span></span> <span data-ttu-id="1ba5f-127">nom de Hello de votre IoT hub doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-127">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="1ba5f-128">**Nom du déploiement** est un nom pour le déploiement de hello, tel que **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-128">**Deployment name** is a name for hello deployment, such as **Deployment_01**.</span></span>

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

## <a name="use-hello-resource-provider-rest-api-toocreate-an-iot-hub"></a><span data-ttu-id="1ba5f-129">Utilisez toocreate d’API REST de fournisseur de ressources hello un IoT hub</span><span class="sxs-lookup"><span data-stu-id="1ba5f-129">Use hello resource provider REST API toocreate an IoT hub</span></span>

<span data-ttu-id="1ba5f-130">Hello d’utilisation [fournisseur de ressources IoT Hub API REST] [ lnk-rest-api] toocreate un IoT hub dans votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-130">Use hello [IoT Hub resource provider REST API][lnk-rest-api] toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="1ba5f-131">Vous pouvez également utiliser hello ressource fournisseur API REST toomake modifications tooan existant IoT hub.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-131">You can also use hello resource provider REST API toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="1ba5f-132">Ajoutez hello suivant tooProgram.cs de méthode :</span><span class="sxs-lookup"><span data-stu-id="1ba5f-132">Add hello following method tooProgram.cs:</span></span>

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. <span data-ttu-id="1ba5f-133">Ajouter hello suivant code toohello **CreateIoTHub** (méthode).</span><span class="sxs-lookup"><span data-stu-id="1ba5f-133">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="1ba5f-134">Ce code crée un **HttpClient** objet avec le jeton d’authentification hello dans les en-têtes de hello :</span><span class="sxs-lookup"><span data-stu-id="1ba5f-134">This code creates an **HttpClient** object with hello authentication token in hello headers:</span></span>

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. <span data-ttu-id="1ba5f-135">Ajouter hello suivant code toohello **CreateIoTHub** (méthode).</span><span class="sxs-lookup"><span data-stu-id="1ba5f-135">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="1ba5f-136">Ce code explique hello IoT hub toocreate et génère une représentation JSON.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-136">This code describes hello IoT hub toocreate and generates a JSON representation.</span></span> <span data-ttu-id="1ba5f-137">Pour la liste actuelle des emplacements qui prennent en charge de IoT Hub hello consultez [Azure Status][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="1ba5f-137">For hello current list of locations that support IoT Hub see [Azure Status][lnk-status]:</span></span>

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

4. <span data-ttu-id="1ba5f-138">Ajouter hello suivant code toohello **CreateIoTHub** (méthode).</span><span class="sxs-lookup"><span data-stu-id="1ba5f-138">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="1ba5f-139">Ce code soumet hello reste demande tooAzure.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-139">This code submits hello REST request tooAzure.</span></span> <span data-ttu-id="1ba5f-140">code de Hello, puis vérifie la réponse de hello et récupère les URL hello vous pouvez utiliser l’état de hello de toomonitor de la tâche de déploiement hello :</span><span class="sxs-lookup"><span data-stu-id="1ba5f-140">hello code then checks hello response and retrieves hello URL you can use toomonitor hello state of hello deployment task:</span></span>

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

5. <span data-ttu-id="1ba5f-141">Ajouter hello suivant fin toohello de code Hello **CreateIoTHub** (méthode).</span><span class="sxs-lookup"><span data-stu-id="1ba5f-141">Add hello following code toohello end of hello **CreateIoTHub** method.</span></span> <span data-ttu-id="1ba5f-142">Ce code utilise hello **asyncStatusUri** adresse récupérée dans hello précédente étape toowait pour hello déploiement toocomplete :</span><span class="sxs-lookup"><span data-stu-id="1ba5f-142">This code uses hello **asyncStatusUri** address retrieved in hello previous step toowait for hello deployment toocomplete:</span></span>

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. <span data-ttu-id="1ba5f-143">Ajouter hello suivant fin toohello de code Hello **CreateIoTHub** (méthode).</span><span class="sxs-lookup"><span data-stu-id="1ba5f-143">Add hello following code toohello end of hello **CreateIoTHub** method.</span></span> <span data-ttu-id="1ba5f-144">Ce code récupère les clés hello Hello IoT hub, vous avez créé et imprime les toohello console :</span><span class="sxs-lookup"><span data-stu-id="1ba5f-144">This code retrieves hello keys of hello IoT hub you created and prints them toohello console:</span></span>

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-hello-application"></a><span data-ttu-id="1ba5f-145">Application hello complet et exécution</span><span class="sxs-lookup"><span data-stu-id="1ba5f-145">Complete and run hello application</span></span>

<span data-ttu-id="1ba5f-146">Vous pouvez maintenant terminer application hello en appelant hello **CreateIoTHub** méthode avant de générer et exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-146">You can now complete hello application by calling hello **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="1ba5f-147">Ajouter hello suivant fin toohello de code Hello **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="1ba5f-147">Add hello following code toohello end of hello **Main** method:</span></span>

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. <span data-ttu-id="1ba5f-148">Cliquez sur **Build**, puis sur **Générer la solution**.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-148">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="1ba5f-149">Corrigez les éventuelles erreurs.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-149">Correct any errors.</span></span>

3. <span data-ttu-id="1ba5f-150">Cliquez sur **déboguer** , puis **démarrer le débogage** application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-150">Click **Debug** and then **Start Debugging** toorun hello application.</span></span> <span data-ttu-id="1ba5f-151">Il peut prendre plusieurs minutes pour hello déploiement toorun.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-151">It may take several minutes for hello deployment toorun.</span></span>

4. <span data-ttu-id="1ba5f-152">tooverify votre application ajoutée hello nouveau hub IoT, visitez hello [portail Azure] [ lnk-azure-portal] et afficher la liste des ressources.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-152">tooverify that your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="1ba5f-153">Vous pouvez également utiliser hello **Get-AzureRmResource** applet de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-153">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="1ba5f-154">Cet exemple d’application ajoute un IoT Hub S1 Standard qui vous est facturé.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-154">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="1ba5f-155">Lorsque vous avez terminé, vous pouvez supprimer hello IoT hub via hello [portail Azure] [ lnk-azure-portal] ou à l’aide de hello **Remove-AzureRmResource** applet de commande PowerShell lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-155">When you are finished, you can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ba5f-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1ba5f-156">Next steps</span></span>
<span data-ttu-id="1ba5f-157">Maintenant vous avez déployé un IoT hub à l’aide du fournisseur de ressources hello API REST, vous souhaiterez peut-être tooexplore supplémentaire :</span><span class="sxs-lookup"><span data-stu-id="1ba5f-157">Now you have deployed an IoT hub using hello resource provider REST API, you may want tooexplore further:</span></span>

* <span data-ttu-id="1ba5f-158">En savoir plus sur les fonctions hello Hello [fournisseur de ressources IoT Hub API REST][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="1ba5f-158">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="1ba5f-159">Lecture [vue d’ensemble du Gestionnaire de ressources Azure] [ lnk-azure-rm-overview] toolearn plus sur les fonctionnalités du Gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1ba5f-159">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="1ba5f-160">toolearn plus sur le développement pour IoT Hub, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="1ba5f-160">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="1ba5f-161">[Introduction tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="1ba5f-161">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="1ba5f-162">[Kits de développement logiciel (SDK) Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="1ba5f-162">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="1ba5f-163">toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="1ba5f-163">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="1ba5f-164">[Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="1ba5f-164">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
