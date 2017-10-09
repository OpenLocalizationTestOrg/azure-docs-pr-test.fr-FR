---
title: "aaaUsing hello tooaccess de l’API REST API des services Azure Mobile Engagement"
description: "Décrit comment toouse hello Mobile Engagement REST API tooaccess API des services Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: wesmc7777
manager: erikre
editor: 
ms.assetid: e8df4897-55ee-45df-b41e-ff187e3d9d12
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 315761299a42df6f65e81df20e632f9713844b0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-rest-tooaccess-azure-mobile-engagement-service-apis"></a><span data-ttu-id="3735e-103">À l’aide de REST tooaccess API des services Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="3735e-103">Using REST tooaccess Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="3735e-104">Azure Mobile Engagement fournit hello [API REST de Azure Mobile Engagement](https://msdn.microsoft.com/library/azure/mt683754.aspx) vous toomanage périphériques, etc. les campagnes Reach/Push.</span><span class="sxs-lookup"><span data-stu-id="3735e-104">Azure Mobile Engagement provides hello [Azure Mobile Engagement REST API](https://msdn.microsoft.com/library/azure/mt683754.aspx) for you toomanage Devices, Reach/Push campaigns etc.</span></span>

> [!NOTE]
> <span data-ttu-id="3735e-105">Hello Azure Mobile Engagement service mars 2018 est retirée et est actuellement que les clients tooexisting disponibles.</span><span class="sxs-lookup"><span data-stu-id="3735e-105">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="3735e-106">Pour plus d’informations, consultez [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="3735e-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="3735e-107">Si vous ne souhaitez pas directement toouse hello API REST, nous fournissons également une [fichier Swagger](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) que vous pouvez utiliser avec des outils toogenerate kits de développement logiciel pour votre langue par défaut.</span><span class="sxs-lookup"><span data-stu-id="3735e-107">If you do not want toouse hello REST APIs directly, we also provide a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools toogenerate SDKs for your preferred language.</span></span> <span data-ttu-id="3735e-108">Nous vous recommandons d’utiliser des hello [AutoRest](https://github.com/Azure/AutoRest) outil toogenerate votre Kit de développement logiciel à partir de notre fichier Swagger.</span><span class="sxs-lookup"><span data-stu-id="3735e-108">We recommend using hello [AutoRest](https://github.com/Azure/AutoRest) tool toogenerate your SDK from our Swagger file.</span></span> <span data-ttu-id="3735e-109">Nous avons créé un kit de développement .NET de la même manière qui vous permet de toointeract avec ces API à l’aide d’un wrapper c#, et vous n’avez toodo hello négociation du jeton d’authentification et d’actualiser vous-même.</span><span class="sxs-lookup"><span data-stu-id="3735e-109">We have created a .NET SDK in a similar manner which allows you toointeract with these APIs using a C# wrapper and you don't have toodo hello authentication token negotiation and refresh yourself.</span></span> <span data-ttu-id="3735e-110">Consultez [Service API .NET SDK Sample](mobile-engagement-dotnet-sdk-service-api.md) toolearn comment toouse hello .net SDK pour l’API</span><span class="sxs-lookup"><span data-stu-id="3735e-110">See [Service API .NET SDK Sample](mobile-engagement-dotnet-sdk-service-api.md) toolearn how toouse hello .net SDK for API</span></span>
