---
title: "Créer une application iOS sur Azure App Service Mobile Apps | Microsoft Docs"
description: "Suivez ce didacticiel pour commencer à utiliser des backends Azure Mobile App pour le développement iOS en Objective-C ou Swift"
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 6461a899-9340-42dd-b118-ffc5ba00e846
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 36936ae66c458fcbedeec95cfa2f573a40c8af53
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-ios-app"></a><span data-ttu-id="44019-103">Création d'une application iOS</span><span class="sxs-lookup"><span data-stu-id="44019-103">Create an iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="44019-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="44019-104">Overview</span></span>
<span data-ttu-id="44019-105">Ce didacticiel présente l’ajout d’ [Azure Mobile Apps](app-service-mobile-value-prop.md), un service principal cloud, à une application iOS.</span><span class="sxs-lookup"><span data-stu-id="44019-105">This tutorial shows how to add [Azure Mobile Apps](app-service-mobile-value-prop.md), a cloud backend service, to an iOS app.</span></span> <span data-ttu-id="44019-106">Nous créerons tout d’abord un serveur principal mobile.</span><span class="sxs-lookup"><span data-stu-id="44019-106">We'll first create a new mobile backend.</span></span> <span data-ttu-id="44019-107">Ensuite, nous utiliserons une simple application iOS de *To do list* pour stocker des données dans Azure.</span><span class="sxs-lookup"><span data-stu-id="44019-107">Then, we'll use a simple *Todo list* iOS app to store data in Azure.</span></span>

<span data-ttu-id="44019-108">Pour suivre ce didacticiel, vous avez besoin d’un Mac et d’un [compte Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="44019-108">To complete this tutorial, you need a Mac and [an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>

## <a name="step-i-create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="44019-109">Étape I : créer un serveur principal d’applications mobiles Azure</span><span class="sxs-lookup"><span data-stu-id="44019-109">Step I: Create a new Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="step-ii-configure-the-backend-project"></a><span data-ttu-id="44019-110">Étape II : configurer le projet de serveur principal</span><span class="sxs-lookup"><span data-stu-id="44019-110">Step II: Configure the backend project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="step-iii-download-and-run-the-ios-app"></a><span data-ttu-id="44019-111">Étape III : télécharger et exécuter l’application iOS</span><span class="sxs-lookup"><span data-stu-id="44019-111">Step III: Download and run the iOS app</span></span>
[!INCLUDE [app-service-mobile-ios-run-app](../../includes/app-service-mobile-ios-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
