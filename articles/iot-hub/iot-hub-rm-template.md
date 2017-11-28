---
title: "aaaCreate un IoT Hub de Azure à l’aide d’un modèle (.NET) | Documents Microsoft"
description: "Comment toouse un toocreate de modèle Azure Resource Manager un IoT Hub avec un programme c#."
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
ms.openlocfilehash: 6140deff3553701f994502fd4a60178f874e27cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a><span data-ttu-id="a30ae-103">Créer un IoT Hub avec un modèle Azure Resource Manager (.NET)</span><span class="sxs-lookup"><span data-stu-id="a30ae-103">Create an IoT hub using Azure Resource Manager template (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="a30ae-104">Vous pouvez utiliser le Gestionnaire de ressources Azure toocreate et gérer les hubs Azure IoT par programme.</span><span class="sxs-lookup"><span data-stu-id="a30ae-104">You can use Azure Resource Manager toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="a30ae-105">Ce didacticiel vous montre comment toouse un toocreate de modèle Azure Resource Manager un IoT hub à partir d’un programme c#.</span><span class="sxs-lookup"><span data-stu-id="a30ae-105">This tutorial shows you how toouse an Azure Resource Manager template toocreate an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="a30ae-106">Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a30ae-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="a30ae-107">Cet article décrit à l’aide du modèle de déploiement du Gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a30ae-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="a30ae-108">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="a30ae-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="a30ae-109">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="a30ae-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="a30ae-110">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="a30ae-110">An active Azure account.</span></span> <br/><span data-ttu-id="a30ae-111">Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="a30ae-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="a30ae-112">Un [compte Stockage Azure][lnk-storage-account] dans lequel vous pouvez stocker vos fichiers de modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a30ae-112">An [Azure Storage account][lnk-storage-account] where you can store your Azure Resource Manager template files.</span></span>
* <span data-ttu-id="a30ae-113">[Azure PowerShell 1.0][lnk-powershell-install] ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="a30ae-113">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="a30ae-114">Préparer votre projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a30ae-114">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="a30ae-115">Dans Visual Studio, créez un projet Visual c# bureau classique de Windows à l’aide de hello **l’application Console (.NET Framework)** modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="a30ae-115">In Visual Studio, create a Visual C# Windows Classic Desktop project using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="a30ae-116">Projet de hello nom **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="a30ae-116">Name hello project **CreateIoTHub**.</span></span>

2. <span data-ttu-id="a30ae-117">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur votre projet, puis cliquez sur **GÉRER LES PACKAGES NUGET**.</span><span class="sxs-lookup"><span data-stu-id="a30ae-117">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="a30ae-118">Dans le Gestionnaire de Package NuGet, vérifiez **inclure la version préliminaire**et sur hello **Parcourir** recherche de page pour **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="a30ae-118">In NuGet Package Manager, check **Include prerelease**, and on hello **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="a30ae-119">Sélectionnez le package de hello, cliquez sur **installer**, dans **réviser les modifications** cliquez sur **OK**, puis cliquez sur **J’accepte** tooaccept des licences hello.</span><span class="sxs-lookup"><span data-stu-id="a30ae-119">Select hello package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello licenses.</span></span>

4. <span data-ttu-id="a30ae-120">Dans le gestionnaire de packages NuGet, recherchez **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="a30ae-120">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="a30ae-121">Cliquez sur **installer**, dans **réviser les modifications** cliquez sur **OK**, puis cliquez sur **J’accepte** licence de hello tooaccept.</span><span class="sxs-lookup"><span data-stu-id="a30ae-121">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello license.</span></span>

5. <span data-ttu-id="a30ae-122">Dans le fichier Program.cs, remplacer hello **à l’aide de** instructions avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="a30ae-122">In Program.cs, replace hello existing **using** statements with hello following code:</span></span>

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. <span data-ttu-id="a30ae-123">Dans Program.cs, ajoutez hello suivant en remplaçant les valeurs d’espace réservé hello de variables statiques.</span><span class="sxs-lookup"><span data-stu-id="a30ae-123">In Program.cs, add hello following static variables replacing hello placeholder values.</span></span> <span data-ttu-id="a30ae-124">Vous avez noté les éléments **ApplicationId**, **SubscriptionId**, **TenantId** et **Password** précédemment dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="a30ae-124">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="a30ae-125">**Le nom de votre compte de stockage Azure** désigne hello hello compte de stockage Azure où vous stockez vos fichiers de modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a30ae-125">**Your Azure Storage account name** is hello name of hello Azure Storage account where you store your Azure Resource Manager template files.</span></span> <span data-ttu-id="a30ae-126">**Nom de groupe de ressources** est le nom hello hello du groupe de ressources vous utilisez quand vous créez hello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a30ae-126">**Resource group name** is hello name of hello resource group you use when you create hello IoT hub.</span></span> <span data-ttu-id="a30ae-127">nom de Hello peut être un groupe de ressources existant ou nouveau.</span><span class="sxs-lookup"><span data-stu-id="a30ae-127">hello name can be a pre-existing or new resource group.</span></span> <span data-ttu-id="a30ae-128">**Nom du déploiement** est un nom pour le déploiement de hello, tel que **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="a30ae-128">**Deployment name** is a name for hello deployment, such as **Deployment_01**.</span></span>

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

## <a name="submit-a-template-toocreate-an-iot-hub"></a><span data-ttu-id="a30ae-129">Envoyer un toocreate de modèle un IoT hub</span><span class="sxs-lookup"><span data-stu-id="a30ae-129">Submit a template toocreate an IoT hub</span></span>

<span data-ttu-id="a30ae-130">Utilisez un JSON modèle et le paramètre de fichier toocreate un IoT hub dans votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a30ae-130">Use a JSON template and parameter file toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="a30ae-131">Vous pouvez également utiliser un gestionnaire de ressources Azure modèle toomake modifications tooan existant IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a30ae-131">You can also use an Azure Resource Manager template toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="a30ae-132">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur votre projet, cliquez sur **Ajouter**, puis sur **Nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="a30ae-132">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="a30ae-133">Ajouter un fichier JSON appelé **template.json** tooyour projet.</span><span class="sxs-lookup"><span data-stu-id="a30ae-133">Add a JSON file called **template.json** tooyour project.</span></span>

2. <span data-ttu-id="a30ae-134">tooadd un toohello de hub IoT standard **États-Unis** contenu hello de remplacement de la région **template.json** avec hello après la définition de ressource.</span><span class="sxs-lookup"><span data-stu-id="a30ae-134">tooadd a standard IoT hub toohello **East US** region, replace hello contents of **template.json** with hello following resource definition.</span></span> <span data-ttu-id="a30ae-135">Pour la liste actuelle des régions qui prennent en charge de IoT Hub hello consultez [Azure Status][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="a30ae-135">For hello current list of regions that support IoT Hub see [Azure Status][lnk-status]:</span></span>

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

3. <span data-ttu-id="a30ae-136">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur votre projet, cliquez sur **Ajouter**, puis sur **Nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="a30ae-136">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="a30ae-137">Ajouter un fichier JSON appelé **parameters.json** tooyour projet.</span><span class="sxs-lookup"><span data-stu-id="a30ae-137">Add a JSON file called **parameters.json** tooyour project.</span></span>

4. <span data-ttu-id="a30ae-138">Remplacez le contenu hello de **parameters.json** avec hello suit les informations de paramètre qui définit un nom pour le nouveau concentrateur de IoT hello telles que **{vos initiales} mynewiothub**.</span><span class="sxs-lookup"><span data-stu-id="a30ae-138">Replace hello contents of **parameters.json** with hello following parameter information that sets a name for hello new IoT hub such as **{your initials}mynewiothub**.</span></span> <span data-ttu-id="a30ae-139">nom de hub IoT Hello doit être globalement unique afin qu’il doit inclure votre nom ou les initiales :</span><span class="sxs-lookup"><span data-stu-id="a30ae-139">hello IoT hub name must be globally unique so it should include your name or initials:</span></span>

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

5. <span data-ttu-id="a30ae-140">Dans **l’Explorateur de serveurs**connecter tooyour abonnement Azure et dans le stockage Azure votre compte créer un conteneur appelé **modèles**.</span><span class="sxs-lookup"><span data-stu-id="a30ae-140">In **Server Explorer**, connect tooyour Azure subscription, and in your Azure Storage account create a container called **templates**.</span></span> <span data-ttu-id="a30ae-141">Bonjour **propriétés** Panneau de configuration, le jeu hello **accès en lecture Public** autorisations pour hello **modèles** conteneur trop**Blob**.</span><span class="sxs-lookup"><span data-stu-id="a30ae-141">In hello **Properties** panel, set hello **Public Read Access** permissions for hello **templates** container too**Blob**.</span></span>

6. <span data-ttu-id="a30ae-142">Dans **l’Explorateur de serveurs**, avec le bouton droit sur hello **modèles** conteneur, puis cliquez sur **conteneur d’objets Blob vue**.</span><span class="sxs-lookup"><span data-stu-id="a30ae-142">In **Server Explorer**, right-click on hello **templates** container and then click **View Blob Container**.</span></span> <span data-ttu-id="a30ae-143">Cliquez sur hello **télécharger un objet Blob** bouton, sélectionnez les deux fichiers de hello, **parameters.json** et **templates.json**, puis cliquez sur **ouvrir** hello de tooupload JSON fichiers toohello **modèles** conteneur.</span><span class="sxs-lookup"><span data-stu-id="a30ae-143">Click hello **Upload Blob** button, select hello two files, **parameters.json** and **templates.json**, and then click **Open** tooupload hello JSON files toohello **templates** container.</span></span> <span data-ttu-id="a30ae-144">URL de Hello d’objets BLOB de hello contenant des données JSON de hello sont :</span><span class="sxs-lookup"><span data-stu-id="a30ae-144">hello URLs of hello blobs containing hello JSON data are:</span></span>

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. <span data-ttu-id="a30ae-145">Ajoutez hello suivant tooProgram.cs de méthode :</span><span class="sxs-lookup"><span data-stu-id="a30ae-145">Add hello following method tooProgram.cs:</span></span>

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. <span data-ttu-id="a30ae-146">Ajouter hello suivant code toohello **CreateIoTHub** méthode toosubmit hello modèle et le paramètre fichiers toohello Azure Resource Manager :</span><span class="sxs-lookup"><span data-stu-id="a30ae-146">Add hello following code toohello **CreateIoTHub** method toosubmit hello template and parameter files toohello Azure Resource Manager:</span></span>

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

9. <span data-ttu-id="a30ae-147">Ajouter hello suivant code toohello **CreateIoTHub** méthode qui affiche l’état de hello et clés hello pour le nouveau concentrateur de IoT hello :</span><span class="sxs-lookup"><span data-stu-id="a30ae-147">Add hello following code toohello **CreateIoTHub** method that displays hello status and hello keys for hello new IoT hub:</span></span>

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed toocreate iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-hello-application"></a><span data-ttu-id="a30ae-148">Application hello complet et exécution</span><span class="sxs-lookup"><span data-stu-id="a30ae-148">Complete and run hello application</span></span>

<span data-ttu-id="a30ae-149">Vous pouvez maintenant terminer application hello en appelant hello **CreateIoTHub** méthode avant de générer et exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="a30ae-149">You can now complete hello application by calling hello **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="a30ae-150">Ajouter hello suivant fin toohello de code Hello **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="a30ae-150">Add hello following code toohello end of hello **Main** method:</span></span>

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. <span data-ttu-id="a30ae-151">Cliquez sur **Build**, puis sur **Générer la solution**.</span><span class="sxs-lookup"><span data-stu-id="a30ae-151">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="a30ae-152">Corrigez les éventuelles erreurs.</span><span class="sxs-lookup"><span data-stu-id="a30ae-152">Correct any errors.</span></span>

3. <span data-ttu-id="a30ae-153">Cliquez sur **déboguer** , puis **démarrer le débogage** application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="a30ae-153">Click **Debug** and then **Start Debugging** toorun hello application.</span></span> <span data-ttu-id="a30ae-154">Il peut prendre plusieurs minutes pour hello déploiement toorun.</span><span class="sxs-lookup"><span data-stu-id="a30ae-154">It may take several minutes for hello deployment toorun.</span></span>

4. <span data-ttu-id="a30ae-155">tooverify votre application ajoutée hello nouveau hub IoT, visitez hello [portail Azure] [ lnk-azure-portal] et afficher la liste des ressources.</span><span class="sxs-lookup"><span data-stu-id="a30ae-155">tooverify your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="a30ae-156">Vous pouvez également utiliser hello **Get-AzureRmResource** applet de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a30ae-156">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="a30ae-157">Cet exemple d’application ajoute un IoT Hub S1 Standard qui vous est facturé.</span><span class="sxs-lookup"><span data-stu-id="a30ae-157">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="a30ae-158">Vous pouvez supprimer hello IoT hub via hello [portail Azure] [ lnk-azure-portal] ou à l’aide de hello **Remove-AzureRmResource** applet de commande PowerShell lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="a30ae-158">You can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a30ae-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a30ae-159">Next steps</span></span>
<span data-ttu-id="a30ae-160">Maintenant vous avez déployé un IoT hub à l’aide d’un modèle Azure Resource Manager avec un programme c#, vous souhaiterez peut-être tooexplore supplémentaire :</span><span class="sxs-lookup"><span data-stu-id="a30ae-160">Now you have deployed an IoT hub using an Azure Resource Manager template with a C# program, you may want tooexplore further:</span></span>

* <span data-ttu-id="a30ae-161">En savoir plus sur les fonctions hello Hello [fournisseur de ressources IoT Hub API REST][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="a30ae-161">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="a30ae-162">Lecture [vue d’ensemble du Gestionnaire de ressources Azure] [ lnk-azure-rm-overview] toolearn plus sur les fonctionnalités du Gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a30ae-162">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="a30ae-163">toolearn plus sur le développement pour IoT Hub, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="a30ae-163">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="a30ae-164">[Introduction tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="a30ae-164">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="a30ae-165">[Kits de développement logiciel (SDK) Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="a30ae-165">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="a30ae-166">toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="a30ae-166">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="a30ae-167">[Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="a30ae-167">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
