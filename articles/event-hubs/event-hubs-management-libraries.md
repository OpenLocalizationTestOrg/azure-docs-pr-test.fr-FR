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
# <a name="event-hubs-management-libraries"></a><span data-ttu-id="bd640-103">Bibliothèque de gestion des Event Hubs</span><span class="sxs-lookup"><span data-stu-id="bd640-103">Event Hubs management libraries</span></span>

<span data-ttu-id="bd640-104">bibliothèques de gestion des concentrateurs d’événements Hello peuvent configurer dynamiquement des entités et espaces de noms de concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="bd640-104">hello Event Hubs management libraries can dynamically provision Event Hubs namespaces and entities.</span></span> <span data-ttu-id="bd640-105">Ainsi, les déploiements complexes et les scénarios de messagerie, afin que vous pouvez déterminer par programme la tooprovision d’entités.</span><span class="sxs-lookup"><span data-stu-id="bd640-105">This enables complex deployments and messaging scenarios, so that you can programmatically determine what entities tooprovision.</span></span> <span data-ttu-id="bd640-106">Ces bibliothèques sont actuellement disponibles pour .NET.</span><span class="sxs-lookup"><span data-stu-id="bd640-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="bd640-107">Fonctionnalités prises en charge</span><span class="sxs-lookup"><span data-stu-id="bd640-107">Supported functionality</span></span>

* <span data-ttu-id="bd640-108">Création, mise à jour et suppression d’espaces de noms</span><span class="sxs-lookup"><span data-stu-id="bd640-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="bd640-109">Création, mise à jour et suppression d’Event Hubs</span><span class="sxs-lookup"><span data-stu-id="bd640-109">Event Hubs creation, update, deletion</span></span>
* <span data-ttu-id="bd640-110">Création, mise à jour et suppression de groupes de consommateurs</span><span class="sxs-lookup"><span data-stu-id="bd640-110">Consumer Group creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd640-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bd640-111">Prerequisites</span></span>

<span data-ttu-id="bd640-112">tooget démarré à l’aide des bibliothèques de gestion hello concentrateurs d’événements, vous devez vous authentifier avec Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="bd640-112">tooget started using hello Event Hubs management libraries, you must authenticate with Azure Active Directory (AAD).</span></span> <span data-ttu-id="bd640-113">AAD nécessite que vous authentifier en tant que service principal, qui fournit l’accès tooyour ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="bd640-113">AAD requires that you authenticate as a service principal, which provides access tooyour Azure resources.</span></span> <span data-ttu-id="bd640-114">Pour plus d’informations sur la création d’un principal du service, consultez ces articles :</span><span class="sxs-lookup"><span data-stu-id="bd640-114">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="bd640-115">Utiliser l’application de hello toocreate portail Azure Active Directory et de principal du service qui peut accéder aux ressources</span><span class="sxs-lookup"><span data-stu-id="bd640-115">Use hello Azure portal toocreate Active Directory application and service principal that can access resources</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="bd640-116">Utiliser Azure PowerShell toocreate une ressources tooaccess principal du service</span><span class="sxs-lookup"><span data-stu-id="bd640-116">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="bd640-117">Utilisez Azure CLI toocreate une ressources tooaccess principal du service</span><span class="sxs-lookup"><span data-stu-id="bd640-117">Use Azure CLI toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

<span data-ttu-id="bd640-118">Ces didacticiels vous donnent une `AppId` (ID Client), `TenantId`, et `ClientSecret` (clé d’authentification), qui sont utilisés pour l’authentification par des bibliothèques de gestion hello.</span><span class="sxs-lookup"><span data-stu-id="bd640-118">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by hello management libraries.</span></span> <span data-ttu-id="bd640-119">Vous devez avoir **propriétaire** autorisations pour le groupe de ressources hello sur lequel vous souhaitez toorun.</span><span class="sxs-lookup"><span data-stu-id="bd640-119">You must have **Owner** permissions for hello resource group on which you want toorun.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="bd640-120">Modèle de programmation</span><span class="sxs-lookup"><span data-stu-id="bd640-120">Programming pattern</span></span>

<span data-ttu-id="bd640-121">Hello modèle toomanipulate n’importe quelle ressource de concentrateurs d’événements suit un protocole commun :</span><span class="sxs-lookup"><span data-stu-id="bd640-121">hello pattern toomanipulate any Event Hubs resource follows a common protocol:</span></span>

1. <span data-ttu-id="bd640-122">Obtenir un jeton d’AAD à l’aide de hello `Microsoft.IdentityModel.Clients.ActiveDirectory` bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="bd640-122">Obtain a token from AAD using hello `Microsoft.IdentityModel.Clients.ActiveDirectory` library.</span></span>
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. <span data-ttu-id="bd640-123">Créer hello `EventHubManagementClient` objet.</span><span class="sxs-lookup"><span data-stu-id="bd640-123">Create hello `EventHubManagementClient` object.</span></span>
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. <span data-ttu-id="bd640-124">Ensemble hello `CreateOrUpdate` tooyour de paramètres des valeurs spécifiées.</span><span class="sxs-lookup"><span data-stu-id="bd640-124">Set hello `CreateOrUpdate` parameters tooyour specified values.</span></span>
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. <span data-ttu-id="bd640-125">Hello appel d’exécution.</span><span class="sxs-lookup"><span data-stu-id="bd640-125">Execute hello call.</span></span>
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a><span data-ttu-id="bd640-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bd640-126">Next steps</span></span>
* [<span data-ttu-id="bd640-127">Exemple de gestion .NET</span><span class="sxs-lookup"><span data-stu-id="bd640-127">.NET Management sample</span></span>](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [<span data-ttu-id="bd640-128">Espace de noms Microsoft.Azure.Management.EventHub</span><span class="sxs-lookup"><span data-stu-id="bd640-128">Microsoft.Azure.Management.EventHub Reference</span></span>](/dotnet/api/Microsoft.Azure.Management.EventHub) 
