---
title: "Créer une application Android sur Azure App Service Mobile Apps | Microsoft Docs"
description: "Suivez ce didacticiel pour commencer à utiliser des backends d’applications mobiles Azure pour le développement Android"
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
ms.openlocfilehash: 418a5229a084d570bc6cab5925dbd8d30945a3c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-android-app"></a><span data-ttu-id="fdc2f-103">Créer une application Android</span><span class="sxs-lookup"><span data-stu-id="fdc2f-103">Create an Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="fdc2f-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="fdc2f-104">Overview</span></span>
<span data-ttu-id="fdc2f-105">Ce didacticiel montre comment ajouter un backend cloud à une application mobile Android à l’aide d’un backend d’application mobile Azure.</span><span class="sxs-lookup"><span data-stu-id="fdc2f-105">This tutorial shows you how to add a cloud-based backend service to an Android mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="fdc2f-106">Vous allez créer un backend d’application mobile et une simple application Android *Todo list* qui stocke les données d’application dans Azure.</span><span class="sxs-lookup"><span data-stu-id="fdc2f-106">You will create both a new mobile app backend and a simple *Todo list* Android app that stores app data in Azure.</span></span>

<span data-ttu-id="fdc2f-107">Le suivi de ce didacticiel est un prérequis pour tous les autres didacticiels Android sur l’utilisation de la fonctionnalité Mobile Apps dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="fdc2f-107">Completing this tutorial is a prerequisite for all other Android tutorials about using the Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fdc2f-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fdc2f-108">Prerequisites</span></span>
<span data-ttu-id="fdc2f-109">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="fdc2f-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="fdc2f-110">[Outils de développement Android](https://developer.android.com/sdk/index.html), qui incluent l’environnement de développement intégré Android Studio et la dernière plateforme Android.</span><span class="sxs-lookup"><span data-stu-id="fdc2f-110">[Android Developer Tools](https://developer.android.com/sdk/index.html), which includes the Android Studio integrated development environment, and the latest Android platform.</span></span>
* <span data-ttu-id="fdc2f-111">Kit de développement logiciel (SDK) Azure Mobile Android, qui est automatiquement inclus dans le projet de démarrage rapide que vous téléchargez.</span><span class="sxs-lookup"><span data-stu-id="fdc2f-111">Azure Mobile Android SDK, which is automatically referenced as part of the quickstart project you download.</span></span>
* <span data-ttu-id="fdc2f-112">Un [compte Azure actif](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fdc2f-112">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="fdc2f-113">Créer un serveur principal d'applications mobiles Azure</span><span class="sxs-lookup"><span data-stu-id="fdc2f-113">Create a new Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-the-server-project"></a><span data-ttu-id="fdc2f-114">Configurer le projet de serveur</span><span class="sxs-lookup"><span data-stu-id="fdc2f-114">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-android-app"></a><span data-ttu-id="fdc2f-115">Télécharger et exécuter l’application Android</span><span class="sxs-lookup"><span data-stu-id="fdc2f-115">Download and run the Android app</span></span>
[!INCLUDE [app-service-mobile-android-run-app](../../includes/app-service-mobile-android-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
