---
title: "Bibliothèques de gestion Azure Event Hubs | Microsoft Docs"
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
ms.openlocfilehash: 0d659cb860a6c98342b548212820efe046decfcc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-management-libraries"></a><span data-ttu-id="aca3f-103">Bibliothèque de gestion des Event Hubs</span><span class="sxs-lookup"><span data-stu-id="aca3f-103">Event Hubs management libraries</span></span>

<span data-ttu-id="aca3f-104">Les bibliothèques de gestion des Event Hubs peuvent approvisionner dynamiquement des entités et des espaces de noms d’Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="aca3f-104">The Event Hubs management libraries can dynamically provision Event Hubs namespaces and entities.</span></span> <span data-ttu-id="aca3f-105">Ceci permet des déploiements et des scénarios de messagerie complexes, et de déterminer ainsi par programmation les entités à approvisionner.</span><span class="sxs-lookup"><span data-stu-id="aca3f-105">This enables complex deployments and messaging scenarios, so that you can programmatically determine what entities to provision.</span></span> <span data-ttu-id="aca3f-106">Ces bibliothèques sont actuellement disponibles pour .NET.</span><span class="sxs-lookup"><span data-stu-id="aca3f-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="aca3f-107">Fonctionnalités prises en charge</span><span class="sxs-lookup"><span data-stu-id="aca3f-107">Supported functionality</span></span>

* <span data-ttu-id="aca3f-108">Création, mise à jour et suppression d’espaces de noms</span><span class="sxs-lookup"><span data-stu-id="aca3f-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="aca3f-109">Création, mise à jour et suppression d’Event Hubs</span><span class="sxs-lookup"><span data-stu-id="aca3f-109">Event Hubs creation, update, deletion</span></span>
* <span data-ttu-id="aca3f-110">Création, mise à jour et suppression de groupes de consommateurs</span><span class="sxs-lookup"><span data-stu-id="aca3f-110">Consumer Group creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aca3f-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="aca3f-111">Prerequisites</span></span>

<span data-ttu-id="aca3f-112">Pour commencer à utiliser les bibliothèques de gestion d’Event Hubs, vous devez vous authentifier avec Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="aca3f-112">To get started using the Event Hubs management libraries, you must authenticate with Azure Active Directory (AAD).</span></span> <span data-ttu-id="aca3f-113">AAD vous oblige à vous authentifier en tant que principal du service pour pouvoir accéder à vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="aca3f-113">AAD requires that you authenticate as a service principal, which provides access to your Azure resources.</span></span> <span data-ttu-id="aca3f-114">Pour plus d’informations sur la création d’un principal du service, consultez ces articles :</span><span class="sxs-lookup"><span data-stu-id="aca3f-114">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="aca3f-115">Utiliser le portail Azure pour créer une application et un principal du service Active Directory pouvant accéder aux ressources</span><span class="sxs-lookup"><span data-stu-id="aca3f-115">Use the Azure portal to create Active Directory application and service principal that can access resources</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="aca3f-116">Créer un principal du service pour accéder aux ressources à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="aca3f-116">Use Azure PowerShell to create a service principal to access resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="aca3f-117">Créer un principal du service pour accéder aux ressources à l’aide de l’interface de ligne de commande (CLI) Azure</span><span class="sxs-lookup"><span data-stu-id="aca3f-117">Use Azure CLI to create a service principal to access resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

<span data-ttu-id="aca3f-118">Ces didacticiels vous fournissent un `AppId` (ID de client), un `TenantId` et un `ClientSecret` (clé d’authentification), tous étant utilisés pour l’authentification par les bibliothèques de gestion.</span><span class="sxs-lookup"><span data-stu-id="aca3f-118">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by the management libraries.</span></span> <span data-ttu-id="aca3f-119">Vous devez disposer des autorisations **Propriétaire** pour le groupe de ressources à utiliser pour l’exécution.</span><span class="sxs-lookup"><span data-stu-id="aca3f-119">You must have **Owner** permissions for the resource group on which you want to run.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="aca3f-120">Modèle de programmation</span><span class="sxs-lookup"><span data-stu-id="aca3f-120">Programming pattern</span></span>

<span data-ttu-id="aca3f-121">Le modèle pour manipuler une ressource Event Hubs quelconque suit un protocole commun :</span><span class="sxs-lookup"><span data-stu-id="aca3f-121">The pattern to manipulate any Event Hubs resource follows a common protocol:</span></span>

1. <span data-ttu-id="aca3f-122">Obtenez un jeton AAD à l’aide de la bibliothèque `Microsoft.IdentityModel.Clients.ActiveDirectory`.</span><span class="sxs-lookup"><span data-stu-id="aca3f-122">Obtain a token from AAD using the `Microsoft.IdentityModel.Clients.ActiveDirectory` library.</span></span>
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. <span data-ttu-id="aca3f-123">Créer l’objet `EventHubManagementClient`.</span><span class="sxs-lookup"><span data-stu-id="aca3f-123">Create the `EventHubManagementClient` object.</span></span>
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. <span data-ttu-id="aca3f-124">Définissez les paramètres `CreateOrUpdate` sur vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="aca3f-124">Set the `CreateOrUpdate` parameters to your specified values.</span></span>
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. <span data-ttu-id="aca3f-125">Exécuter l’appel.</span><span class="sxs-lookup"><span data-stu-id="aca3f-125">Execute the call.</span></span>
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a><span data-ttu-id="aca3f-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aca3f-126">Next steps</span></span>
* [<span data-ttu-id="aca3f-127">Exemple de gestion .NET</span><span class="sxs-lookup"><span data-stu-id="aca3f-127">.NET Management sample</span></span>](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [<span data-ttu-id="aca3f-128">Espace de noms Microsoft.Azure.Management.EventHub</span><span class="sxs-lookup"><span data-stu-id="aca3f-128">Microsoft.Azure.Management.EventHub Reference</span></span>](/dotnet/api/Microsoft.Azure.Management.EventHub) 
