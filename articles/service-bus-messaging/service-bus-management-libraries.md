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
# <a name="service-bus-management-libraries"></a><span data-ttu-id="b8a62-103">Bibliothèques de gestion Service Bus</span><span class="sxs-lookup"><span data-stu-id="b8a62-103">Service Bus management libraries</span></span>

<span data-ttu-id="b8a62-104">bibliothèques de gestion Azure Service Bus Hello peuvent configurer dynamiquement des entités et espaces de noms Service Bus.</span><span class="sxs-lookup"><span data-stu-id="b8a62-104">hello Azure Service Bus management libraries can dynamically provision Service Bus namespaces and entities.</span></span> <span data-ttu-id="b8a62-105">Cela permet des scénarios de messagerie et de déploiements complexes et rend possible tooprogrammatically déterminer quel tooprovision d’entités.</span><span class="sxs-lookup"><span data-stu-id="b8a62-105">This enables complex deployments and messaging scenarios, and makes it possible tooprogrammatically determine what entities tooprovision.</span></span> <span data-ttu-id="b8a62-106">Ces bibliothèques sont actuellement disponibles pour .NET.</span><span class="sxs-lookup"><span data-stu-id="b8a62-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="b8a62-107">Fonctionnalités prises en charge</span><span class="sxs-lookup"><span data-stu-id="b8a62-107">Supported functionality</span></span>

* <span data-ttu-id="b8a62-108">Création, mise à jour et suppression d’espaces de noms</span><span class="sxs-lookup"><span data-stu-id="b8a62-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="b8a62-109">Création, mise à jour et suppression de files d’attente</span><span class="sxs-lookup"><span data-stu-id="b8a62-109">Queue creation, update, deletion</span></span>
* <span data-ttu-id="b8a62-110">Création, mise à jour et suppression de rubriques</span><span class="sxs-lookup"><span data-stu-id="b8a62-110">Topic creation, update, deletion</span></span>
* <span data-ttu-id="b8a62-111">Création, mise à jour et suppression d’abonnements</span><span class="sxs-lookup"><span data-stu-id="b8a62-111">Subscription creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8a62-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b8a62-112">Prerequisites</span></span>

<span data-ttu-id="b8a62-113">tooget démarré à l’aide des bibliothèques de gestion Service Bus hello, vous devez vous authentifier avec hello service Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="b8a62-113">tooget started using hello Service Bus management libraries, you must authenticate with hello Azure Active Directory (AAD) service.</span></span> <span data-ttu-id="b8a62-114">AAD nécessite que vous authentifier en tant que service principal, qui fournit l’accès tooyour ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="b8a62-114">AAD requires that you authenticate as a service principal, which provides access tooyour Azure resources.</span></span> <span data-ttu-id="b8a62-115">Pour plus d’informations sur la création d’un principal du service, consultez ces articles :</span><span class="sxs-lookup"><span data-stu-id="b8a62-115">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="b8a62-116">Utiliser l’application de hello toocreate portail Azure Active Directory et de principal du service qui peut accéder aux ressources</span><span class="sxs-lookup"><span data-stu-id="b8a62-116">Use hello Azure portal toocreate Active Directory application and service principal that can access resources</span></span>](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [<span data-ttu-id="b8a62-117">Utiliser Azure PowerShell toocreate une ressources tooaccess principal du service</span><span class="sxs-lookup"><span data-stu-id="b8a62-117">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="b8a62-118">Utilisez Azure CLI toocreate une ressources tooaccess principal du service</span><span class="sxs-lookup"><span data-stu-id="b8a62-118">Use Azure CLI toocreate a service principal tooaccess resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

<span data-ttu-id="b8a62-119">Ces didacticiels vous donnent une `AppId` (ID Client), `TenantId`, et `ClientSecret` (clé d’authentification), qui sont utilisés pour l’authentification par des bibliothèques de gestion hello.</span><span class="sxs-lookup"><span data-stu-id="b8a62-119">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by hello management libraries.</span></span> <span data-ttu-id="b8a62-120">Vous devez avoir **propriétaire** autorisations pour le groupe de ressources hello sur laquelle vous souhaitez toorun.</span><span class="sxs-lookup"><span data-stu-id="b8a62-120">You must have **Owner** permissions for hello resource group on which you wish toorun.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="b8a62-121">Modèle de programmation</span><span class="sxs-lookup"><span data-stu-id="b8a62-121">Programming pattern</span></span>

<span data-ttu-id="b8a62-122">Hello modèle toomanipulate n’importe quelle ressource de Service Bus suit un protocole commun :</span><span class="sxs-lookup"><span data-stu-id="b8a62-122">hello pattern toomanipulate any Service Bus resource follows a common protocol:</span></span>

1. <span data-ttu-id="b8a62-123">Obtenir un jeton d’Azure Active Directory à l’aide de hello **Microsoft.IdentityModel.Clients.ActiveDirectory** bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="b8a62-123">Obtain a token from Azure Active Directory using hello **Microsoft.IdentityModel.Clients.ActiveDirectory** library.</span></span>
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. <span data-ttu-id="b8a62-124">Créer hello `ServiceBusManagementClient` objet.</span><span class="sxs-lookup"><span data-stu-id="b8a62-124">Create hello `ServiceBusManagementClient` object.</span></span>

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. <span data-ttu-id="b8a62-125">Ensemble hello `CreateOrUpdate` tooyour de paramètres des valeurs spécifiées.</span><span class="sxs-lookup"><span data-stu-id="b8a62-125">Set hello `CreateOrUpdate` parameters tooyour specified values.</span></span>

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. <span data-ttu-id="b8a62-126">Hello appel d’exécution.</span><span class="sxs-lookup"><span data-stu-id="b8a62-126">Execute hello call.</span></span>

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a><span data-ttu-id="b8a62-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b8a62-127">Next steps</span></span>
* [<span data-ttu-id="b8a62-128">Exemple de gestion .NET</span><span class="sxs-lookup"><span data-stu-id="b8a62-128">.NET management sample</span></span>](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [<span data-ttu-id="b8a62-129">Informations de référence sur l’API Microsoft.Azure.Management.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="b8a62-129">Microsoft.Azure.Management.ServiceBus API reference</span></span>](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
