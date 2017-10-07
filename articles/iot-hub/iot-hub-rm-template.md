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
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a>Créer un IoT Hub avec un modèle Azure Resource Manager (.NET)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Vous pouvez utiliser le Gestionnaire de ressources Azure toocreate et gérer les hubs Azure IoT par programme. Ce didacticiel vous montre comment toouse un toocreate de modèle Azure Resource Manager un IoT hub à partir d’un programme c#.

> [!NOTE]
> Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).  Cet article décrit à l’aide du modèle de déploiement du Gestionnaire de ressources Azure hello.

toocomplete ce didacticiel, vous devez hello suivant :

* Visual Studio 2015 ou Visual Studio 2017.
* Un compte Azure actif. <br/>Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.
* Un [compte Stockage Azure][lnk-storage-account] dans lequel vous pouvez stocker vos fichiers de modèles Azure Resource Manager.
* [Azure PowerShell 1.0][lnk-powershell-install] ou version ultérieure.

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a>Préparer votre projet Visual Studio

1. Dans Visual Studio, créez un projet Visual c# bureau classique de Windows à l’aide de hello **l’application Console (.NET Framework)** modèle de projet. Projet de hello nom **CreateIoTHub**.

2. Dans l’Explorateur de solutions, cliquez avec le bouton droit sur votre projet, puis cliquez sur **GÉRER LES PACKAGES NUGET**.

3. Dans le Gestionnaire de Package NuGet, vérifiez **inclure la version préliminaire**et sur hello **Parcourir** recherche de page pour **Microsoft.Azure.Management.ResourceManager**. Sélectionnez le package de hello, cliquez sur **installer**, dans **réviser les modifications** cliquez sur **OK**, puis cliquez sur **J’accepte** tooaccept des licences hello.

4. Dans le gestionnaire de packages NuGet, recherchez **Microsoft.IdentityModel.Clients.ActiveDirectory**.  Cliquez sur **installer**, dans **réviser les modifications** cliquez sur **OK**, puis cliquez sur **J’accepte** licence de hello tooaccept.

5. Dans le fichier Program.cs, remplacer hello **à l’aide de** instructions avec hello suivant de code :

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. Dans Program.cs, ajoutez hello suivant en remplaçant les valeurs d’espace réservé hello de variables statiques. Vous avez noté les éléments **ApplicationId**, **SubscriptionId**, **TenantId** et **Password** précédemment dans ce didacticiel. **Le nom de votre compte de stockage Azure** désigne hello hello compte de stockage Azure où vous stockez vos fichiers de modèle Azure Resource Manager. **Nom de groupe de ressources** est le nom hello hello du groupe de ressources vous utilisez quand vous créez hello IoT hub. nom de Hello peut être un groupe de ressources existant ou nouveau. **Nom du déploiement** est un nom pour le déploiement de hello, tel que **Deployment_01**.

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

## <a name="submit-a-template-toocreate-an-iot-hub"></a>Envoyer un toocreate de modèle un IoT hub

Utilisez un JSON modèle et le paramètre de fichier toocreate un IoT hub dans votre groupe de ressources. Vous pouvez également utiliser un gestionnaire de ressources Azure modèle toomake modifications tooan existant IoT hub.

1. Dans l’Explorateur de solutions, cliquez avec le bouton droit sur votre projet, cliquez sur **Ajouter**, puis sur **Nouvel élément**. Ajouter un fichier JSON appelé **template.json** tooyour projet.

2. tooadd un toohello de hub IoT standard **États-Unis** contenu hello de remplacement de la région **template.json** avec hello après la définition de ressource. Pour la liste actuelle des régions qui prennent en charge de IoT Hub hello consultez [Azure Status][lnk-status]:

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

3. Dans l’Explorateur de solutions, cliquez avec le bouton droit sur votre projet, cliquez sur **Ajouter**, puis sur **Nouvel élément**. Ajouter un fichier JSON appelé **parameters.json** tooyour projet.

4. Remplacez le contenu hello de **parameters.json** avec hello suit les informations de paramètre qui définit un nom pour le nouveau concentrateur de IoT hello telles que **{vos initiales} mynewiothub**. nom de hub IoT Hello doit être globalement unique afin qu’il doit inclure votre nom ou les initiales :

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

5. Dans **l’Explorateur de serveurs**connecter tooyour abonnement Azure et dans le stockage Azure votre compte créer un conteneur appelé **modèles**. Bonjour **propriétés** Panneau de configuration, le jeu hello **accès en lecture Public** autorisations pour hello **modèles** conteneur trop**Blob**.

6. Dans **l’Explorateur de serveurs**, avec le bouton droit sur hello **modèles** conteneur, puis cliquez sur **conteneur d’objets Blob vue**. Cliquez sur hello **télécharger un objet Blob** bouton, sélectionnez les deux fichiers de hello, **parameters.json** et **templates.json**, puis cliquez sur **ouvrir** hello de tooupload JSON fichiers toohello **modèles** conteneur. URL de Hello d’objets BLOB de hello contenant des données JSON de hello sont :

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. Ajoutez hello suivant tooProgram.cs de méthode :

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. Ajouter hello suivant code toohello **CreateIoTHub** méthode toosubmit hello modèle et le paramètre fichiers toohello Azure Resource Manager :

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

9. Ajouter hello suivant code toohello **CreateIoTHub** méthode qui affiche l’état de hello et clés hello pour le nouveau concentrateur de IoT hello :

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed toocreate iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-hello-application"></a>Application hello complet et exécution

Vous pouvez maintenant terminer application hello en appelant hello **CreateIoTHub** méthode avant de générer et exécutez-le.

1. Ajouter hello suivant fin toohello de code Hello **Main** méthode :

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. Cliquez sur **Build**, puis sur **Générer la solution**. Corrigez les éventuelles erreurs.

3. Cliquez sur **déboguer** , puis **démarrer le débogage** application hello de toorun. Il peut prendre plusieurs minutes pour hello déploiement toorun.

4. tooverify votre application ajoutée hello nouveau hub IoT, visitez hello [portail Azure] [ lnk-azure-portal] et afficher la liste des ressources. Vous pouvez également utiliser hello **Get-AzureRmResource** applet de commande PowerShell.

> [!NOTE]
> Cet exemple d’application ajoute un IoT Hub S1 Standard qui vous est facturé. Vous pouvez supprimer hello IoT hub via hello [portail Azure] [ lnk-azure-portal] ou à l’aide de hello **Remove-AzureRmResource** applet de commande PowerShell lorsque vous avez terminé.

## <a name="next-steps"></a>Étapes suivantes
Maintenant vous avez déployé un IoT hub à l’aide d’un modèle Azure Resource Manager avec un programme c#, vous souhaiterez peut-être tooexplore supplémentaire :

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
[lnk-storage-account]:../storage/common/storage-create-storage-account.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
