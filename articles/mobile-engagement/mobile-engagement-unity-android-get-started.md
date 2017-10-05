---
title: "Prise en main d’Azure Mobile Engagement pour le déploiement de l’application Unity pour Android"
description: "Découvrez comment utiliser Azure Mobile Engagement avec les analyses et les notifications Push pour les applications Unity déployées sur des appareils iOS."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: d5f0ef79-be00-4cec-97a5-a0b2fdaa380e
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bf0b758159d475b4ed7eadb84227e4824e11ba86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a><span data-ttu-id="d65dd-103">Prise en main d’Azure Mobile Engagement pour le déploiement de l’application Unity pour Android</span><span class="sxs-lookup"><span data-stu-id="d65dd-103">Get Started with Azure Mobile Engagement for Unity Android deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="d65dd-104">Cette rubrique montre comment utiliser Azure Mobile Engagement pour comprendre l’utilisation de votre application et envoyer des notifications Push à des utilisateurs segmentés d’une application Unity lors de son déploiement sur un appareil Android.</span><span class="sxs-lookup"><span data-stu-id="d65dd-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Unity application when deploying to an Android device.</span></span>
<span data-ttu-id="d65dd-105">Ce didacticiel utilise le didacticiel classique Unity Roll-a-Ball comme point de départ.</span><span class="sxs-lookup"><span data-stu-id="d65dd-105">This tutorial uses the classic Unity Roll a Ball tutorial as the starting point.</span></span> <span data-ttu-id="d65dd-106">Vous devez suivre la procédure décrite dans ce [didacticiel](mobile-engagement-unity-roll-a-ball.md) avant de procéder à l’intégration de Mobile Engagement que nous présentons dans le didacticiel ci-après.</span><span class="sxs-lookup"><span data-stu-id="d65dd-106">You should follow the steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with the Mobile Engagement integration we showcase in the tutorial below.</span></span> 

<span data-ttu-id="d65dd-107">Ce didacticiel requiert les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d65dd-107">This tutorial requires the following:</span></span>

* [<span data-ttu-id="d65dd-108">Unity Editor</span><span class="sxs-lookup"><span data-stu-id="d65dd-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="d65dd-109">Kit de développement logiciel (SDK) Mobile Engagement pour Unity</span><span class="sxs-lookup"><span data-stu-id="d65dd-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="d65dd-110">Kit de développement logiciel (SDK) pour Google Android</span><span class="sxs-lookup"><span data-stu-id="d65dd-110">Google Android SDK</span></span>

> [!NOTE]
> <span data-ttu-id="d65dd-111">Pour suivre ce didacticiel, vous avez besoin d'un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="d65dd-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="d65dd-112">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="d65dd-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d65dd-113">Pour plus d'informations, consultez la page [Essai gratuit d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="d65dd-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="d65dd-114"><a id="setup-azme"></a>Configuration de Mobile Engagement pour votre application Android</span><span class="sxs-lookup"><span data-stu-id="d65dd-114"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="d65dd-115"><a id="connecting-app"></a>Connexion de votre application au serveur principal Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d65dd-115"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
### <a name="import-the-unity-package"></a><span data-ttu-id="d65dd-116">Importer le package Unity</span><span class="sxs-lookup"><span data-stu-id="d65dd-116">Import the Unity package</span></span>
1. <span data-ttu-id="d65dd-117">Téléchargez le [package Unity pour Mobile Engagement](https://aka.ms/azmeunitysdk) et enregistrez-le sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="d65dd-117">Download the [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it to your local machine.</span></span> 
2. <span data-ttu-id="d65dd-118">Accédez à **Assets -> Import Package -> Custom Package** (Ressources -> Importer le package -> Package personnalisé) et sélectionnez le package que vous avez téléchargé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="d65dd-118">Go to **Assets -> Import Package -> Custom Package** and select the package you downloaded in the above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="d65dd-119">Vérifiez que tous les fichiers sont sélectionnés, puis cliquez sur le bouton **Import** .</span><span class="sxs-lookup"><span data-stu-id="d65dd-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="d65dd-120">Une fois l’importation effectuée, les fichiers du Kit de développement logiciel (SDK) importé dans votre projet s’affichent.</span><span class="sxs-lookup"><span data-stu-id="d65dd-120">Once Import is successful, you will see the imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="d65dd-121">Mettre à jour le fichier EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="d65dd-121">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="d65dd-122">Ouvrez le fichier de script **EngagementConfiguration** contenu dans le dossier SDK et mettez à jour la chaîne **ANDROID\_CONNECTION\_STRING** en la remplaçant par la chaîne de connexion obtenue plus tôt à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d65dd-122">Open up the **EngagementConfiguration** script file from the SDK folder and update the **ANDROID\_CONNECTION\_STRING** with the connection string you obtained earlier from the Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="d65dd-123">Enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="d65dd-123">Save the file</span></span> 
3. <span data-ttu-id="d65dd-124">Exécutez **File -> Engagement -> Generate Android Manifest** (Fichier -> Engagement -> Générer le manifeste Android).</span><span class="sxs-lookup"><span data-stu-id="d65dd-124">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="d65dd-125">Il s’agit du plug-in ajouté par le Kit de développement logiciel (SDK) Mobile Engagement. Cliquez dessus pour mettre à jour automatiquement les paramètres du projet.</span><span class="sxs-lookup"><span data-stu-id="d65dd-125">This is the plugin added by the Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

> [!IMPORTANT]
> <span data-ttu-id="d65dd-126">Veillez à exécuter cette procédure à chaque mise à jour du fichier **EngagementConfiguration** , faute de quoi vos modifications ne seront pas prises en compte dans l’application.</span><span class="sxs-lookup"><span data-stu-id="d65dd-126">Make sure to execute this every time you update the **EngagementConfiguration** file otherwise your changes will not be reflected in the app.</span></span> 
> 
> 

### <a name="configure-the-app-for-basic-tracking"></a><span data-ttu-id="d65dd-127">Configurer l’application pour un suivi de base</span><span class="sxs-lookup"><span data-stu-id="d65dd-127">Configure the app for basic tracking</span></span>
1. <span data-ttu-id="d65dd-128">Ouvrez le script **PlayerController** joint à l’objet Player pour le modifier.</span><span class="sxs-lookup"><span data-stu-id="d65dd-128">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="d65dd-129">Ajoutez les instructions using suivantes :</span><span class="sxs-lookup"><span data-stu-id="d65dd-129">Add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="d65dd-130">Ajoutez ce qui suit à la méthode `Start()` :</span><span class="sxs-lookup"><span data-stu-id="d65dd-130">Add the following to the `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-the-app"></a><span data-ttu-id="d65dd-131">Déployer et exécuter l’application</span><span class="sxs-lookup"><span data-stu-id="d65dd-131">Deploy and run the app</span></span>
<span data-ttu-id="d65dd-132">Vérifiez que le Kit de développement logiciel (SDK) Android est installé sur votre ordinateur avant d’essayer de déployer l’application Unity sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="d65dd-132">Make sure that you have Android SDK installed on your machine before attempting to deploy this Unity app to your device.</span></span> 

1. <span data-ttu-id="d65dd-133">Connectez un appareil Android à votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d65dd-133">Connect an Android device to your machine.</span></span> 
2. <span data-ttu-id="d65dd-134">Accédez à **File -> Build Settings** (Fichier -> Paramètres de build).</span><span class="sxs-lookup"><span data-stu-id="d65dd-134">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="d65dd-135">Sélectionnez **Android** (Android), puis cliquez sur **Switch Platform** (Changer de plateforme).</span><span class="sxs-lookup"><span data-stu-id="d65dd-135">Select **Android** and then click on **Switch Platform**</span></span>
   
    ![][51]
   
    ![][52]
4. <span data-ttu-id="d65dd-136">Cliquez sur **Player settings** et indiquez un identificateur Bundle Identifier valide.</span><span class="sxs-lookup"><span data-stu-id="d65dd-136">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="d65dd-137">Pour finir, cliquez sur **Build And Run**</span><span class="sxs-lookup"><span data-stu-id="d65dd-137">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="d65dd-138">Vous pouvez être invité à fournir un nom de dossier pour y stocker le package Android.</span><span class="sxs-lookup"><span data-stu-id="d65dd-138">You may be asked to provide a folder name to store the Android package.</span></span> 
7. <span data-ttu-id="d65dd-139">Si tout se passe bien, le package doit être déployé sur votre appareil connecté, et votre jeu Unity doit apparaître sur votre téléphone.</span><span class="sxs-lookup"><span data-stu-id="d65dd-139">If everything goes fine, then the package will be deployed to your connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="d65dd-140"><a id="monitor"></a>Connexion d’application avec l’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="d65dd-140"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="d65dd-141"><a id="integrate-push"></a>Activation des notifications Push et de la messagerie in-app</span><span class="sxs-lookup"><span data-stu-id="d65dd-141"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="d65dd-142">Mettre à jour le fichier EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="d65dd-142">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="d65dd-143">Ouvrez le fichier de script **EngagementConfiguration** contenu dans le dossier SDK et mettez à jour la chaîne **ANDROID\_GOOGLE\_NUMBER** en la remplaçant par le numéro **Google Project Number** obtenu plus tôt à partir du portail Google Cloud Developer.</span><span class="sxs-lookup"><span data-stu-id="d65dd-143">Open up the **EngagementConfiguration** script file from the SDK folder and update the **ANDROID\_GOOGLE\_NUMBER** with the **Google Project Number** you obtained earlier from the Google Cloud Developer portal.</span></span> <span data-ttu-id="d65dd-144">Comme il s’agit d’une chaîne de valeur, veillez à l’insérer entre des guillemets.</span><span class="sxs-lookup"><span data-stu-id="d65dd-144">This is a string value so make sure to enclose it in double quotes.</span></span> 
   
    ![][75]
2. <span data-ttu-id="d65dd-145">Enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="d65dd-145">Save the file.</span></span> 
3. <span data-ttu-id="d65dd-146">Exécutez **File -> Engagement -> Generate Android Manifest** (Fichier -> Engagement -> Générer le manifeste Android).</span><span class="sxs-lookup"><span data-stu-id="d65dd-146">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="d65dd-147">Il s’agit du plug-in ajouté par le Kit de développement logiciel (SDK) Mobile Engagement. Cliquez dessus pour mettre à jour automatiquement les paramètres du projet.</span><span class="sxs-lookup"><span data-stu-id="d65dd-147">This is the plugin added by the Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

### <a name="configure-the-app-to-receive-notifications"></a><span data-ttu-id="d65dd-148">Configurer l’application pour recevoir des notifications</span><span class="sxs-lookup"><span data-stu-id="d65dd-148">Configure the app to receive notifications</span></span>
1. <span data-ttu-id="d65dd-149">Ouvrez le script **PlayerController** joint à l’objet Player pour le modifier.</span><span class="sxs-lookup"><span data-stu-id="d65dd-149">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="d65dd-150">Ajoutez ce qui suit à la méthode `Start()` :</span><span class="sxs-lookup"><span data-stu-id="d65dd-150">Add the following to the `Start()` method</span></span>
   
        EngagementReachAgent.Initialize();
3. <span data-ttu-id="d65dd-151">À présent que l’application est mise à jour, déployez et exécutez l’application sur un appareil conformément aux instructions ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d65dd-151">Now that the app is updated, deploy and run the app on a device per the instructions provided below.</span></span> 

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[40]: ./media/mobile-engagement-unity-android-get-started/40.png
[70]: ./media/mobile-engagement-unity-android-get-started/70.png
[71]: ./media/mobile-engagement-unity-android-get-started/71.png
[72]: ./media/mobile-engagement-unity-android-get-started/72.png
[73]: ./media/mobile-engagement-unity-android-get-started/73.png
[74]: ./media/mobile-engagement-unity-android-get-started/74.png
[75]: ./media/mobile-engagement-unity-android-get-started/75.png
[51]: ./media/mobile-engagement-unity-android-get-started/51.png
[52]: ./media/mobile-engagement-unity-android-get-started/52.png
[53]: ./media/mobile-engagement-unity-android-get-started/53.png
[54]: ./media/mobile-engagement-unity-android-get-started/54.png
