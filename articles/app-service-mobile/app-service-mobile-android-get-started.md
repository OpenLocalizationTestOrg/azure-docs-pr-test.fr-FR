---
title: aaaCreate une application Android sur Azure App Service Mobile Apps | Documents Microsoft
description: "Suivez ce didacticiel tooget un bon départ avec les serveurs principaux de l’application mobile Azure pour le développement Android"
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 355f0959-aa7f-472c-a6c7-9eecea3a34a9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 0af85a3a4de9fc265976bbe3f34d73effc3807df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-android-app"></a><span data-ttu-id="02cde-103">Créer une application Android</span><span class="sxs-lookup"><span data-stu-id="02cde-103">Create an Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="02cde-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="02cde-104">Overview</span></span>
<span data-ttu-id="02cde-105">Ce didacticiel vous montre comment tooadd un backend de cloud service tooan des applications mobiles Android à l’aide d’un serveur principal d’application mobile Azure.</span><span class="sxs-lookup"><span data-stu-id="02cde-105">This tutorial shows you how tooadd a cloud-based backend service tooan Android mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="02cde-106">Vous allez créer un backend d’application mobile et une simple application Android *Todo list* qui stocke les données d’application dans Azure.</span><span class="sxs-lookup"><span data-stu-id="02cde-106">You will create both a new mobile app backend and a simple *Todo list* Android app that stores app data in Azure.</span></span>

<span data-ttu-id="02cde-107">Ils auront terminé ce didacticiel est un composant requis pour tous les autres didacticiels Android sur l’utilisation de la fonctionnalité des applications mobiles hello dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="02cde-107">Completing this tutorial is a prerequisite for all other Android tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02cde-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="02cde-108">Prerequisites</span></span>
<span data-ttu-id="02cde-109">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="02cde-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="02cde-110">[Les outils de développement Android](https://developer.android.com/sdk/index.html), qui inclut l’environnement de développement intégré Android hello et la plateforme Android hello la plus récente.</span><span class="sxs-lookup"><span data-stu-id="02cde-110">[Android Developer Tools](https://developer.android.com/sdk/index.html), which includes hello Android Studio integrated development environment, and hello latest Android platform.</span></span>
* <span data-ttu-id="02cde-111">Azure Mobile Android SDK, qui est référencé automatiquement dans le cadre du projet de démarrage rapide de hello que vous téléchargez.</span><span class="sxs-lookup"><span data-stu-id="02cde-111">Azure Mobile Android SDK, which is automatically referenced as part of hello quickstart project you download.</span></span>
* <span data-ttu-id="02cde-112">Un [compte Azure actif](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="02cde-112">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="02cde-113">Créer un serveur principal d'applications mobiles Azure</span><span class="sxs-lookup"><span data-stu-id="02cde-113">Create a new Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a><span data-ttu-id="02cde-114">Configurer le projet de serveur hello</span><span class="sxs-lookup"><span data-stu-id="02cde-114">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-android-app"></a><span data-ttu-id="02cde-115">Téléchargez et exécutez l’application Android hello</span><span class="sxs-lookup"><span data-stu-id="02cde-115">Download and run hello Android app</span></span>
[!INCLUDE [app-service-mobile-android-run-app](../../includes/app-service-mobile-android-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
