---
title: "bibliothèques de gestion des concentrateurs d’événements aaaAzure | Documents Microsoft"
description: "Gérer les entités et espaces de noms des Event Hubs à partir de .NET"
services: event-hubs
cloud: na
documentationcenter: na
author: sethmanheim
manager: timlt
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: b7db0077f6f31397ae46e926c3c28630a157824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-management-libraries"></a>Bibliothèque de gestion des Event Hubs

bibliothèques de gestion des concentrateurs d’événements Hello peuvent configurer dynamiquement des entités et espaces de noms de concentrateurs d’événements. Ainsi, les déploiements complexes et les scénarios de messagerie, afin que vous pouvez déterminer par programme la tooprovision d’entités. Ces bibliothèques sont actuellement disponibles pour .NET.

## <a name="supported-functionality"></a>Fonctionnalités prises en charge

* Création, mise à jour et suppression d’espaces de noms
* Création, mise à jour et suppression d’Event Hubs
* Création, mise à jour et suppression de groupes de consommateurs

## <a name="prerequisites"></a>Composants requis

tooget démarré à l’aide des bibliothèques de gestion hello concentrateurs d’événements, vous devez vous authentifier avec Azure Active Directory (AAD). AAD nécessite que vous authentifier en tant que service principal, qui fournit l’accès tooyour ressources Azure. Pour plus d’informations sur la création d’un principal du service, consultez ces articles :  

* [Utiliser l’application de hello toocreate portail Azure Active Directory et de principal du service qui peut accéder aux ressources](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [Utiliser Azure PowerShell toocreate une ressources tooaccess principal du service](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [Utilisez Azure CLI toocreate une ressources tooaccess principal du service](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

Ces didacticiels vous donnent une `AppId` (ID Client), `TenantId`, et `ClientSecret` (clé d’authentification), qui sont utilisés pour l’authentification par des bibliothèques de gestion hello. Vous devez avoir **propriétaire** autorisations pour le groupe de ressources hello sur lequel vous souhaitez toorun.

## <a name="programming-pattern"></a>Modèle de programmation

Hello modèle toomanipulate n’importe quelle ressource de concentrateurs d’événements suit un protocole commun :

1. Obtenir un jeton d’AAD à l’aide de hello `Microsoft.IdentityModel.Clients.ActiveDirectory` bibliothèque.
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. Créer hello `EventHubManagementClient` objet.
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. Ensemble hello `CreateOrUpdate` tooyour de paramètres des valeurs spécifiées.
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. Hello appel d’exécution.
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a>Étapes suivantes
* [Exemple de gestion .NET](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [Espace de noms Microsoft.Azure.Management.EventHub](/dotnet/api/Microsoft.Azure.Management.EventHub) 
