---
title: "Bibliothèques de gestion Azure Service Bus | Microsoft Docs"
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
ms.openlocfilehash: 1db00dc1f91e8976b622030450445babbe547ad8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="service-bus-management-libraries"></a><span data-ttu-id="954e8-103">Bibliothèques de gestion Service Bus</span><span class="sxs-lookup"><span data-stu-id="954e8-103">Service Bus management libraries</span></span>

<span data-ttu-id="954e8-104">Les bibliothèques de gestion Azure Service Bus peuvent approvisionner dynamiquement des entités et des espaces de noms Service Bus.</span><span class="sxs-lookup"><span data-stu-id="954e8-104">The Azure Service Bus management libraries can dynamically provision Service Bus namespaces and entities.</span></span> <span data-ttu-id="954e8-105">Cela permet des déploiements et des scénarios de messagerie complexes, et rend possible la définition des entités à approvisionner par programmation.</span><span class="sxs-lookup"><span data-stu-id="954e8-105">This enables complex deployments and messaging scenarios, and makes it possible to programmatically determine what entities to provision.</span></span> <span data-ttu-id="954e8-106">Ces bibliothèques sont actuellement disponibles pour .NET.</span><span class="sxs-lookup"><span data-stu-id="954e8-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="954e8-107">Fonctionnalités prises en charge</span><span class="sxs-lookup"><span data-stu-id="954e8-107">Supported functionality</span></span>

* <span data-ttu-id="954e8-108">Création, mise à jour et suppression d’espaces de noms</span><span class="sxs-lookup"><span data-stu-id="954e8-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="954e8-109">Création, mise à jour et suppression de files d’attente</span><span class="sxs-lookup"><span data-stu-id="954e8-109">Queue creation, update, deletion</span></span>
* <span data-ttu-id="954e8-110">Création, mise à jour et suppression de rubriques</span><span class="sxs-lookup"><span data-stu-id="954e8-110">Topic creation, update, deletion</span></span>
* <span data-ttu-id="954e8-111">Création, mise à jour et suppression d’abonnements</span><span class="sxs-lookup"><span data-stu-id="954e8-111">Subscription creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="954e8-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="954e8-112">Prerequisites</span></span>

<span data-ttu-id="954e8-113">Pour commencer à utiliser les bibliothèques de gestion Service Bus, vous devez vous authentifier auprès du service Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="954e8-113">To get started using the Service Bus management libraries, you must authenticate with the Azure Active Directory (AAD) service.</span></span> <span data-ttu-id="954e8-114">AAD vous oblige à vous authentifier en tant que principal du service pour pouvoir accéder à vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="954e8-114">AAD requires that you authenticate as a service principal, which provides access to your Azure resources.</span></span> <span data-ttu-id="954e8-115">Pour plus d’informations sur la création d’un principal du service, consultez ces articles :</span><span class="sxs-lookup"><span data-stu-id="954e8-115">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="954e8-116">Utiliser le portail Azure pour créer une application et un principal du service Active Directory pouvant accéder aux ressources</span><span class="sxs-lookup"><span data-stu-id="954e8-116">Use the Azure portal to create Active Directory application and service principal that can access resources</span></span>](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [<span data-ttu-id="954e8-117">Créer un principal du service pour accéder aux ressources à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="954e8-117">Use Azure PowerShell to create a service principal to access resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="954e8-118">Créer un principal du service pour accéder aux ressources à l’aide de l’interface de ligne de commande (CLI) Azure</span><span class="sxs-lookup"><span data-stu-id="954e8-118">Use Azure CLI to create a service principal to access resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

<span data-ttu-id="954e8-119">Ces didacticiels vous fournissent un `AppId` (ID de client), un `TenantId` et un `ClientSecret` (clé d’authentification), tous étant utilisés pour l’authentification par les bibliothèques de gestion.</span><span class="sxs-lookup"><span data-stu-id="954e8-119">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by the management libraries.</span></span> <span data-ttu-id="954e8-120">Vous devez disposer des autorisations **Propriétaire** pour le groupe de ressources à utiliser pour l’exécution.</span><span class="sxs-lookup"><span data-stu-id="954e8-120">You must have **Owner** permissions for the resource group on which you wish to run.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="954e8-121">Modèle de programmation</span><span class="sxs-lookup"><span data-stu-id="954e8-121">Programming pattern</span></span>

<span data-ttu-id="954e8-122">Le modèle pour manipuler une ressource Service Bus quelconque suit un protocole commun :</span><span class="sxs-lookup"><span data-stu-id="954e8-122">The pattern to manipulate any Service Bus resource follows a common protocol:</span></span>

1. <span data-ttu-id="954e8-123">Obtenez un jeton d’Azure Active Directory à l’aide de la bibliothèque **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="954e8-123">Obtain a token from Azure Active Directory using the **Microsoft.IdentityModel.Clients.ActiveDirectory** library.</span></span>
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. <span data-ttu-id="954e8-124">Créer l’objet `ServiceBusManagementClient`.</span><span class="sxs-lookup"><span data-stu-id="954e8-124">Create the `ServiceBusManagementClient` object.</span></span>

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. <span data-ttu-id="954e8-125">Définissez les paramètres `CreateOrUpdate` sur vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="954e8-125">Set the `CreateOrUpdate` parameters to your specified values.</span></span>

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. <span data-ttu-id="954e8-126">Exécuter l’appel.</span><span class="sxs-lookup"><span data-stu-id="954e8-126">Execute the call.</span></span>

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a><span data-ttu-id="954e8-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="954e8-127">Next steps</span></span>
* [<span data-ttu-id="954e8-128">Exemple de gestion .NET</span><span class="sxs-lookup"><span data-stu-id="954e8-128">.NET management sample</span></span>](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [<span data-ttu-id="954e8-129">Informations de référence sur l’API Microsoft.Azure.Management.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="954e8-129">Microsoft.Azure.Management.ServiceBus API reference</span></span>](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
