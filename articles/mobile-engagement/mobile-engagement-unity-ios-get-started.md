---
title: "Prise en main d’Azure Mobile Engagement pour le déploiement de l’application Unity pour iOS"
description: "Découvrez comment utiliser Azure Mobile Engagement avec les analyses et les notifications Push pour les applications Unity déployées sur des appareils iOS."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7ddfbac3-8d13-4ebe-b061-c865f357297f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c8f50404771965ec636065346ac04e059d264c3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a><span data-ttu-id="9e0d7-103">Prise en main d’Azure Mobile Engagement pour le déploiement de l’application Unity pour iOS</span><span class="sxs-lookup"><span data-stu-id="9e0d7-103">Get Started with Azure Mobile Engagement for Unity iOS deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="9e0d7-104">Cette rubrique montre comment utiliser Azure Mobile Engagement pour comprendre l’utilisation de votre application et envoyer des notifications Push à des utilisateurs segmentés d’une application Unity lors de son déploiement sur un appareil iOS.</span><span class="sxs-lookup"><span data-stu-id="9e0d7-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Unity application when deploying to an iOS device.</span></span>
<span data-ttu-id="9e0d7-105">Ce didacticiel utilise le didacticiel classique Unity Roll-a-Ball comme point de départ.</span><span class="sxs-lookup"><span data-stu-id="9e0d7-105">This tutorial uses the classic Unity Roll a Ball tutorial as the starting point.</span></span> <span data-ttu-id="9e0d7-106">Vous devez suivre la procédure décrite dans ce [didacticiel](mobile-engagement-unity-roll-a-ball.md) avant de procéder à l’intégration de Mobile Engagement que nous présentons dans le didacticiel ci-après.</span><span class="sxs-lookup"><span data-stu-id="9e0d7-106">You should follow the steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with the Mobile Engagement integration we showcase in the tutorial below.</span></span> 

<span data-ttu-id="9e0d7-107">Ce didacticiel requiert les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9e0d7-107">This tutorial requires the following:</span></span>

* [<span data-ttu-id="9e0d7-108">Unity Editor</span><span class="sxs-lookup"><span data-stu-id="9e0d7-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="9e0d7-109">Kit de développement logiciel (SDK) Mobile Engagement pour Unity</span><span class="sxs-lookup"><span data-stu-id="9e0d7-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="9e0d7-110">Éditeur XCode</span><span class="sxs-lookup"><span data-stu-id="9e0d7-110">XCode Editor</span></span>

> [!NOTE]
> <span data-ttu-id="9e0d7-111">Pour suivre ce didacticiel, vous avez besoin d'un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="9e0d7-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="9e0d7-112">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="9e0d7-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9e0d7-113">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="9e0d7-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="9e0d7-114"><a id="setup-azme"></a>Configuration de Mobile Engagement pour votre application iOS</span><span class="sxs-lookup"><span data-stu-id="9e0d7-114"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="9e0d7-115"><a id="connecting-app"></a>Connexion de votre application au serveur principal Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="9e0d7-115"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
### <a name="import-the-unity-package"></a><span data-ttu-id="9e0d7-116">Importer le package Unity</span><span class="sxs-lookup"><span data-stu-id="9e0d7-116">Import the Unity package</span></span>
1. <span data-ttu-id="9e0d7-117">Téléchargez le [package Unity pour Mobile Engagement](https://aka.ms/azmeunitysdk) et enregistrez-le sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="9e0d7-117">Download the [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it to your local machine.</span></span> 
2. <span data-ttu-id="9e0d7-118">Accédez à **Assets -> Import Package -> Custom Package** (Ressources -> Importer le package -> Package personnalisé) et sélectionnez le package que vous avez téléchargé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="9e0d7-118">Go to **Assets -> Import Package -> Custom Package** and select the package you downloaded in the above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="9e0d7-119">Vérifiez que tous les fichiers sont sélectionnés, puis cliquez sur le bouton **Import** .</span><span class="sxs-lookup"><span data-stu-id="9e0d7-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="9e0d7-120">Une fois l’importation effectuée, les fichiers du Kit de développement logiciel (SDK) importé dans votre projet s’affichent.</span><span class="sxs-lookup"><span data-stu-id="9e0d7-120">Once Import is successful, you will see the imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="9e0d7-121">Mettre à jour le fichier EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="9e0d7-121">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="9e0d7-122">Ouvrez le fichier de script **EngagementConfiguration** contenu dans le dossier SDK et mettez à jour la chaîne **IOS\_CONNECTION\_STRING** en la remplaçant par la chaîne de connexion obtenue plus tôt à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9e0d7-122">Open up the **EngagementConfiguration** script file from the SDK folder and update the **IOS\_CONNECTION\_STRING** with the connection string you obtained earlier from the Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="9e0d7-123">Enregistrez le fichier .</span><span class="sxs-lookup"><span data-stu-id="9e0d7-123">Save the file.</span></span> 

### <a name="configure-the-app-for-basic-tracking"></a><span data-ttu-id="9e0d7-124">Configurer l’application pour un suivi de base</span><span class="sxs-lookup"><span data-stu-id="9e0d7-124">Configure the app for basic tracking</span></span>
1. <span data-ttu-id="9e0d7-125">Ouvrez le script **PlayerController** joint à l’objet Player pour le modifier.</span><span class="sxs-lookup"><span data-stu-id="9e0d7-125">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="9e0d7-126">Ajoutez les instructions using suivantes :</span><span class="sxs-lookup"><span data-stu-id="9e0d7-126">Add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="9e0d7-127">Ajoutez ce qui suit à la méthode `Start()` :</span><span class="sxs-lookup"><span data-stu-id="9e0d7-127">Add the following to the `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-the-app"></a><span data-ttu-id="9e0d7-128">Déployer et exécuter l’application</span><span class="sxs-lookup"><span data-stu-id="9e0d7-128">Deploy and run the app</span></span>
1. <span data-ttu-id="9e0d7-129">Connectez un appareil iOS à votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="9e0d7-129">Connect an iOS device to your machine.</span></span> 
2. <span data-ttu-id="9e0d7-130">Accédez à **File -> Build Settings** (Fichier -> Paramètres de build).</span><span class="sxs-lookup"><span data-stu-id="9e0d7-130">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="9e0d7-131">Sélectionnez **Android** (Android), puis cliquez sur **Switch Platform** (Changer de plateforme).</span><span class="sxs-lookup"><span data-stu-id="9e0d7-131">Select **iOS** and then click on **Switch Platform**</span></span>
   
    ![][41]
   
    ![][42]
4. <span data-ttu-id="9e0d7-132">Cliquez sur **Player settings** et indiquez un identificateur Bundle Identifier valide.</span><span class="sxs-lookup"><span data-stu-id="9e0d7-132">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="9e0d7-133">Pour finir, cliquez sur **Build And Run**</span><span class="sxs-lookup"><span data-stu-id="9e0d7-133">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="9e0d7-134">Vous pouvez être invité à fournir un nom de dossier pour y stocker le package iOS.</span><span class="sxs-lookup"><span data-stu-id="9e0d7-134">You may be asked to provide a folder name to store the iOS package.</span></span> 
   
    ![][43]
7. <span data-ttu-id="9e0d7-135">Si tout se passe bien, le projet est compilé, et vous devez l’ouvrir dans votre application XCode.</span><span class="sxs-lookup"><span data-stu-id="9e0d7-135">If everything goes fine, then the project will be compiled and you should open it up on your XCode application.</span></span> 
8. <span data-ttu-id="9e0d7-136">Vérifiez que l’identificateur **Bundle identifier** est correct dans le projet.</span><span class="sxs-lookup"><span data-stu-id="9e0d7-136">Make sure that the **Bundle identifier** is correct in the project.</span></span>  
   
    ![][75]
9. <span data-ttu-id="9e0d7-137">Exécutez l’application en XCode afin que le package soit déployé sur votre appareil connecté. Votre jeu Unity doit apparaître sur votre téléphone.</span><span class="sxs-lookup"><span data-stu-id="9e0d7-137">Now run the app in XCode so that the package is deployed to your connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="9e0d7-138"><a id="monitor"></a>Connexion d’application avec l’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="9e0d7-138"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="9e0d7-139"><a id="integrate-push"></a>Activation des notifications push et de la messagerie in-app</span><span class="sxs-lookup"><span data-stu-id="9e0d7-139"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="9e0d7-140">Mobile Engagement vous permet d’interagir et d’atteindre vos utilisateurs et REACH à l’aide de notifications push et de la messagerie in-app, dans le cadre d’une campagne.</span><span class="sxs-lookup"><span data-stu-id="9e0d7-140">Mobile Engagement allows you to interact with your users and REACH with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="9e0d7-141">Ce module s'appelle Couverture dans le portail Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="9e0d7-141">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="9e0d7-142">Inutile d’effectuer d’autres tâches de configuration dans votre application pour recevoir des notifications, car elle est déjà configurée à cet effet.</span><span class="sxs-lookup"><span data-stu-id="9e0d7-142">You don't have to do any additional configuration in your app to receive notifications and it is already setup for it.</span></span>

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[40]: ./media/mobile-engagement-unity-ios-get-started/40.png
[41]: ./media/mobile-engagement-unity-ios-get-started/41.png
[42]: ./media/mobile-engagement-unity-ios-get-started/42.png
[43]: ./media/mobile-engagement-unity-ios-get-started/43.png
[53]: ./media/mobile-engagement-unity-ios-get-started/53.png
[54]: ./media/mobile-engagement-unity-ios-get-started/54.png
[70]: ./media/mobile-engagement-unity-ios-get-started/70.png
[71]: ./media/mobile-engagement-unity-ios-get-started/71.png
[72]: ./media/mobile-engagement-unity-ios-get-started/72.png
[73]: ./media/mobile-engagement-unity-ios-get-started/73.png
[74]: ./media/mobile-engagement-unity-ios-get-started/74.png
[75]: ./media/mobile-engagement-unity-ios-get-started/75.png
