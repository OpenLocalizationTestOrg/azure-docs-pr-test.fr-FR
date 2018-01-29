---
title: "Utilisation de l’API REST pour accéder aux API du service Azure Mobile Engagement"
description: "Décrit comment utiliser les API REST Mobile Engagement pour accéder aux API du service Azure Mobile Engagement"
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
ms.openlocfilehash: 4b21bca6fee7012ce1dba96950ae075eded414f8
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="using-rest-to-access-azure-mobile-engagement-service-apis"></a>Utilisation de REST pour accéder aux API du service Azure Mobile Engagement
Azure Mobile Engagement fournit [l’API REST Azure Mobile Engagement](https://msdn.microsoft.com/library/azure/mt683754.aspx) pour vous permettre de gérer des appareils, des campagnes Push/Reach, etc.

> [!NOTE]
> Le service Azure Mobile Engagement ne sera plus disponible à partir de mars 2018. Actuellement, il reste uniquement disponible pour les clients déjà abonnés à ce service. Pour plus d’informations, consultez [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Si vous ne voulez pas utiliser les API REST directement, nous vous fournissons également un [fichier Swagger](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) que vous pouvez utiliser avec des outils pour générer des SDK dans votre langue par défaut. Nous vous recommandons d’utiliser l’outil [AutoRest](https://github.com/Azure/AutoRest)pour générer votre SDK à partir de notre fichier Swagger. Nous avons créé un Kit de développement logiciel (SDK) .NET de la même manière qui vous permet d’interagir avec ces API à l’aide d’un wrapper C#. Vous n’êtes pas obligé d’effectuer la négociation de jeton d'authentification et l’actualisation vous-même. Consultez [Utilisation du Kit de développement logiciel (SDK) .NET pour accéder aux API du service Azure Mobile Engagement](mobile-engagement-dotnet-sdk-service-api.md) pour apprendre à utiliser le Kit de développement logiciel (SDK) .Net pour les API
