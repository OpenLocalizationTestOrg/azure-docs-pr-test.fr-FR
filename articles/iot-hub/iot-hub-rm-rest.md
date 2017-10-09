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
# <a name="create-an-iot-hub-using-hello-resource-provider-rest-api-net"></a>Créez un IoT hub à l’aide du fournisseur de ressources hello REST API (.NET)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Vous pouvez utiliser hello [fournisseur de ressources IoT Hub API REST] [ lnk-rest-api] toocreate et gérer les hubs Azure IoT par programme. Ce didacticiel vous montre comment toouse hello toocreate de API REST de fournisseur de ressources IoT Hub un IoT hub à partir d’un programme c#.

> [!NOTE]
> Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).  Cet article décrit à l’aide du modèle de déploiement du Gestionnaire de ressources Azure hello.

toocomplete ce didacticiel, vous devez hello suivant :

* Visual Studio 2015 ou Visual Studio 2017.
* Un compte Azure actif. <br/>Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.
* [Azure PowerShell 1.0][lnk-powershell-install] ou version ultérieure.

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a>Préparer votre projet Visual Studio

1. Dans Visual Studio, créez un projet Visual c# bureau classique de Windows à l’aide de hello **l’application Console (.NET Framework)** modèle de projet. Projet de hello nom **CreateIoTHubREST**.

2. Dans l’Explorateur de solutions, cliquez avec le bouton droit sur votre projet, puis cliquez sur **GÉRER LES PACKAGES NUGET**.

3. Dans le Gestionnaire de Package NuGet, vérifiez **inclure la version préliminaire**et sur hello **Parcourir** recherche de page pour **Microsoft.Azure.Management.ResourceManager**. Sélectionnez le package de hello, cliquez sur **installer**, dans **réviser les modifications** cliquez sur **OK**, puis cliquez sur **J’accepte** tooaccept des licences hello.

4. Dans le gestionnaire de packages NuGet, recherchez **Microsoft.IdentityModel.Clients.ActiveDirectory**.  Cliquez sur **installer**, dans **réviser les modifications** cliquez sur **OK**, puis cliquez sur **J’accepte** licence de hello tooaccept.

5. Dans le fichier Program.cs, remplacer hello **à l’aide de** instructions avec hello suivant de code :

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

6. Dans Program.cs, ajoutez hello suivant en remplaçant les valeurs d’espace réservé hello de variables statiques. Vous avez noté les éléments **ApplicationId**, **SubscriptionId**, **TenantId** et **Password** précédemment dans ce didacticiel. **Nom de groupe de ressources** est le nom hello hello du groupe de ressources vous utilisez quand vous créez hello IoT hub. Vous pouvez utiliser un groupe de ressources nouveau ou préexistant. **Nom d’IoT Hub** hello désigne hello IoT Hub, vous créez, tel que **MyIoTHub**. nom de Hello de votre IoT hub doit être globalement unique. **Nom du déploiement** est un nom pour le déploiement de hello, tel que **Deployment_01**.

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

## <a name="use-hello-resource-provider-rest-api-toocreate-an-iot-hub"></a>Utilisez toocreate d’API REST de fournisseur de ressources hello un IoT hub

Hello d’utilisation [fournisseur de ressources IoT Hub API REST] [ lnk-rest-api] toocreate un IoT hub dans votre groupe de ressources. Vous pouvez également utiliser hello ressource fournisseur API REST toomake modifications tooan existant IoT hub.

1. Ajoutez hello suivant tooProgram.cs de méthode :

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. Ajouter hello suivant code toohello **CreateIoTHub** (méthode). Ce code crée un **HttpClient** objet avec le jeton d’authentification hello dans les en-têtes de hello :

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. Ajouter hello suivant code toohello **CreateIoTHub** (méthode). Ce code explique hello IoT hub toocreate et génère une représentation JSON. Pour la liste actuelle des emplacements qui prennent en charge de IoT Hub hello consultez [Azure Status][lnk-status]:

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

4. Ajouter hello suivant code toohello **CreateIoTHub** (méthode). Ce code soumet hello reste demande tooAzure. code de Hello, puis vérifie la réponse de hello et récupère les URL hello vous pouvez utiliser l’état de hello de toomonitor de la tâche de déploiement hello :

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

5. Ajouter hello suivant fin toohello de code Hello **CreateIoTHub** (méthode). Ce code utilise hello **asyncStatusUri** adresse récupérée dans hello précédente étape toowait pour hello déploiement toocomplete :

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. Ajouter hello suivant fin toohello de code Hello **CreateIoTHub** (méthode). Ce code récupère les clés hello Hello IoT hub, vous avez créé et imprime les toohello console :

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-hello-application"></a>Application hello complet et exécution

Vous pouvez maintenant terminer application hello en appelant hello **CreateIoTHub** méthode avant de générer et exécutez-le.

1. Ajouter hello suivant fin toohello de code Hello **Main** méthode :

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. Cliquez sur **Build**, puis sur **Générer la solution**. Corrigez les éventuelles erreurs.

3. Cliquez sur **déboguer** , puis **démarrer le débogage** application hello de toorun. Il peut prendre plusieurs minutes pour hello déploiement toorun.

4. tooverify votre application ajoutée hello nouveau hub IoT, visitez hello [portail Azure] [ lnk-azure-portal] et afficher la liste des ressources. Vous pouvez également utiliser hello **Get-AzureRmResource** applet de commande PowerShell.

> [!NOTE]
> Cet exemple d’application ajoute un IoT Hub S1 Standard qui vous est facturé. Lorsque vous avez terminé, vous pouvez supprimer hello IoT hub via hello [portail Azure] [ lnk-azure-portal] ou à l’aide de hello **Remove-AzureRmResource** applet de commande PowerShell lorsque vous avez terminé.

## <a name="next-steps"></a>Étapes suivantes
Maintenant vous avez déployé un IoT hub à l’aide du fournisseur de ressources hello API REST, vous souhaiterez peut-être tooexplore supplémentaire :

* En savoir plus sur les fonctions hello Hello [fournisseur de ressources IoT Hub API REST][lnk-rest-api].
* Lecture [vue d’ensemble du Gestionnaire de ressources Azure] [ lnk-azure-rm-overview] toolearn plus sur les fonctionnalités du Gestionnaire de ressources Azure hello.

toolearn plus sur le développement pour IoT Hub, consultez hello suivant des articles :

* [Introduction tooC SDK][lnk-c-sdk]
* [Kits de développement logiciel (SDK) Azure IoT][lnk-sdks]

toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :

* [Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]

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
