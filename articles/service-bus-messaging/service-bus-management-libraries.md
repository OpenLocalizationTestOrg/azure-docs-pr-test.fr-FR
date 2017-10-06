---
title: "bibliothèques de gestion Service Bus aaaAzure | Documents Microsoft"
description: "Gérez les espaces de noms et les entités de messagerie Service Bus à partir de .NET."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: 9e4ad91f22815ca0838e6e4647a3606109b2b441
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-management-libraries"></a>Bibliothèques de gestion Service Bus

bibliothèques de gestion Azure Service Bus Hello peuvent configurer dynamiquement des entités et espaces de noms Service Bus. Cela permet des scénarios de messagerie et de déploiements complexes et rend possible tooprogrammatically déterminer quel tooprovision d’entités. Ces bibliothèques sont actuellement disponibles pour .NET.

## <a name="supported-functionality"></a>Fonctionnalités prises en charge

* Création, mise à jour et suppression d’espaces de noms
* Création, mise à jour et suppression de files d’attente
* Création, mise à jour et suppression de rubriques
* Création, mise à jour et suppression d’abonnements

## <a name="prerequisites"></a>Composants requis

tooget démarré à l’aide des bibliothèques de gestion Service Bus hello, vous devez vous authentifier avec hello service Azure Active Directory (AAD). AAD nécessite que vous authentifier en tant que service principal, qui fournit l’accès tooyour ressources Azure. Pour plus d’informations sur la création d’un principal du service, consultez ces articles :  

* [Utiliser l’application de hello toocreate portail Azure Active Directory et de principal du service qui peut accéder aux ressources](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [Utiliser Azure PowerShell toocreate une ressources tooaccess principal du service](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Utilisez Azure CLI toocreate une ressources tooaccess principal du service](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

Ces didacticiels vous donnent une `AppId` (ID Client), `TenantId`, et `ClientSecret` (clé d’authentification), qui sont utilisés pour l’authentification par des bibliothèques de gestion hello. Vous devez avoir **propriétaire** autorisations pour le groupe de ressources hello sur laquelle vous souhaitez toorun.

## <a name="programming-pattern"></a>Modèle de programmation

Hello modèle toomanipulate n’importe quelle ressource de Service Bus suit un protocole commun :

1. Obtenir un jeton d’Azure Active Directory à l’aide de hello **Microsoft.IdentityModel.Clients.ActiveDirectory** bibliothèque.
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. Créer hello `ServiceBusManagementClient` objet.

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. Ensemble hello `CreateOrUpdate` tooyour de paramètres des valeurs spécifiées.

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. Hello appel d’exécution.

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a>Étapes suivantes
* [Exemple de gestion .NET](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [Informations de référence sur l’API Microsoft.Azure.Management.ServiceBus](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
