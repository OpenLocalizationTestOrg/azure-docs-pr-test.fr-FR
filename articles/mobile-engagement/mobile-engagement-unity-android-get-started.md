---
title: "aaaGet main d’Azure Mobile Engagement pour Android Unity déploiement"
description: "Découvrez comment toouse Azure Mobile Engagement avec Analytique et les Notifications Push pour les applications Unity tooiOS périphériques de déploiement."
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
ms.openlocfilehash: c4d34691daeb7544b11c2d6895b2474af0f902b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a><span data-ttu-id="92602-103">Prise en main d’Azure Mobile Engagement pour le déploiement de l’application Unity pour Android</span><span class="sxs-lookup"><span data-stu-id="92602-103">Get Started with Azure Mobile Engagement for Unity Android deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="92602-104">Cette rubrique vous montre comment toouse Azure Mobile Engagement toounderstand votre utilisation de l’application et comment toosend push utilisateurs toosegmented de notifications d’une application Unity lors du déploiement tooan des appareils Android.</span><span class="sxs-lookup"><span data-stu-id="92602-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Unity application when deploying tooan Android device.</span></span>
<span data-ttu-id="92602-105">Ce didacticiel utilise hello restaurer de Unity classique un didacticiel boule en tant que point de départ de hello.</span><span class="sxs-lookup"><span data-stu-id="92602-105">This tutorial uses hello classic Unity Roll a Ball tutorial as hello starting point.</span></span> <span data-ttu-id="92602-106">Vous devez suivre des étapes hello dans ce [didacticiel](mobile-engagement-unity-roll-a-ball.md) avant de poursuivre hello intégration de Mobile Engagement nous exposer dans le didacticiel hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="92602-106">You should follow hello steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with hello Mobile Engagement integration we showcase in hello tutorial below.</span></span> 

<span data-ttu-id="92602-107">Ce didacticiel requiert hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="92602-107">This tutorial requires hello following:</span></span>

* [<span data-ttu-id="92602-108">Unity Editor</span><span class="sxs-lookup"><span data-stu-id="92602-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="92602-109">Kit de développement logiciel (SDK) Mobile Engagement pour Unity</span><span class="sxs-lookup"><span data-stu-id="92602-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="92602-110">Kit de développement logiciel (SDK) pour Google Android</span><span class="sxs-lookup"><span data-stu-id="92602-110">Google Android SDK</span></span>

> [!NOTE]
> <span data-ttu-id="92602-111">toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="92602-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="92602-112">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="92602-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="92602-113">Pour plus d'informations, consultez la page [Essai gratuit d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="92602-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="92602-114"><a id="setup-azme"></a>Configuration de Mobile Engagement pour votre application Android</span><span class="sxs-lookup"><span data-stu-id="92602-114"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="92602-115"><a id="connecting-app"></a>Se connecter à votre serveur principal d’application toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="92602-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
### <a name="import-hello-unity-package"></a><span data-ttu-id="92602-116">Importer un package Unity hello</span><span class="sxs-lookup"><span data-stu-id="92602-116">Import hello Unity package</span></span>
1. <span data-ttu-id="92602-117">Télécharger hello [package Mobile Engagement Unity](https://aka.ms/azmeunitysdk) et enregistrez-le tooyour les ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="92602-117">Download hello [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it tooyour local machine.</span></span> 
2. <span data-ttu-id="92602-118">Accédez trop**ressources -> Importer un Package -> Package personnalisé** et sélectionnez hello vous avez téléchargé dans hello ci-dessus étape.</span><span class="sxs-lookup"><span data-stu-id="92602-118">Go too**Assets -> Import Package -> Custom Package** and select hello package you downloaded in hello above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="92602-119">Vérifiez que tous les fichiers sont sélectionnés, puis cliquez sur le bouton **Import** .</span><span class="sxs-lookup"><span data-stu-id="92602-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="92602-120">Une fois l’importation a réussi, vous verrez les fichiers de kit de développement logiciel de hello importé dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="92602-120">Once Import is successful, you will see hello imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="92602-121">Mettre à jour hello EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="92602-121">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="92602-122">Ouvrez hello **EngagementConfiguration** fichier de script à partir de hello dossier et de mise à jour du Kit de développement logiciel hello **ANDROID\_connexion\_chaîne** avec la chaîne de connexion hello vous avez obtenu version antérieure de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="92602-122">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **ANDROID\_CONNECTION\_STRING** with hello connection string you obtained earlier from hello Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="92602-123">Enregistrez le fichier de hello</span><span class="sxs-lookup"><span data-stu-id="92602-123">Save hello file</span></span> 
3. <span data-ttu-id="92602-124">Exécutez **File -> Engagement -> Generate Android Manifest** (Fichier -> Engagement -> Générer le manifeste Android).</span><span class="sxs-lookup"><span data-stu-id="92602-124">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="92602-125">Il s’agit plug-in hello ajoutée par hello Kit de développement logiciel de Mobile Engagement et en cliquant sur elle met automatiquement à jour les paramètres du projet.</span><span class="sxs-lookup"><span data-stu-id="92602-125">This is hello plugin added by hello Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

> [!IMPORTANT]
> <span data-ttu-id="92602-126">Transformer en tooexecute que chaque fois que vous mettez à jour hello **EngagementConfiguration** fichier dans le cas contraire, vos modifications n’apparaîtront pas dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="92602-126">Make sure tooexecute this every time you update hello **EngagementConfiguration** file otherwise your changes will not be reflected in hello app.</span></span> 
> 
> 

### <a name="configure-hello-app-for-basic-tracking"></a><span data-ttu-id="92602-127">Configurer l’application hello pour le suivi de base</span><span class="sxs-lookup"><span data-stu-id="92602-127">Configure hello app for basic tracking</span></span>
1. <span data-ttu-id="92602-128">Ouvrez hello **PlayerController** script joint toohello d’objet lecteur pour la modification.</span><span class="sxs-lookup"><span data-stu-id="92602-128">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="92602-129">Ajoutez hello qui suit à l’aide d’instruction :</span><span class="sxs-lookup"><span data-stu-id="92602-129">Add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="92602-130">Ajouter hello suivant toohello `Start()` (méthode)</span><span class="sxs-lookup"><span data-stu-id="92602-130">Add hello following toohello `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a><span data-ttu-id="92602-131">Déployer et exécuter l’application hello</span><span class="sxs-lookup"><span data-stu-id="92602-131">Deploy and run hello app</span></span>
<span data-ttu-id="92602-132">Assurez-vous que vous disposez du SDK Android installés sur votre ordinateur avant de tenter de toodeploy ce périphérique tooyour d’application Unity.</span><span class="sxs-lookup"><span data-stu-id="92602-132">Make sure that you have Android SDK installed on your machine before attempting toodeploy this Unity app tooyour device.</span></span> 

1. <span data-ttu-id="92602-133">Connectez un ordinateur de tooyour appareil Android.</span><span class="sxs-lookup"><span data-stu-id="92602-133">Connect an Android device tooyour machine.</span></span> 
2. <span data-ttu-id="92602-134">Accédez à **File -> Build Settings** (Fichier -> Paramètres de build).</span><span class="sxs-lookup"><span data-stu-id="92602-134">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="92602-135">Sélectionnez **Android** (Android), puis cliquez sur **Switch Platform** (Changer de plateforme).</span><span class="sxs-lookup"><span data-stu-id="92602-135">Select **Android** and then click on **Switch Platform**</span></span>
   
    ![][51]
   
    ![][52]
4. <span data-ttu-id="92602-136">Cliquez sur **Player settings** et indiquez un identificateur Bundle Identifier valide.</span><span class="sxs-lookup"><span data-stu-id="92602-136">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="92602-137">Pour finir, cliquez sur **Build And Run**</span><span class="sxs-lookup"><span data-stu-id="92602-137">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="92602-138">Vous pouvez être invité tooprovide un package dossier nom toostore hello Android.</span><span class="sxs-lookup"><span data-stu-id="92602-138">You may be asked tooprovide a folder name toostore hello Android package.</span></span> 
7. <span data-ttu-id="92602-139">Si tout se passe bien, package de hello sera déployé tooyour connecté appareil et vous devez voir votre jeu Unity sur votre téléphone !</span><span class="sxs-lookup"><span data-stu-id="92602-139">If everything goes fine, then hello package will be deployed tooyour connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="92602-140"><a id="monitor"></a>Connexion d’application avec l’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="92602-140"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="92602-141"><a id="integrate-push"></a>Activation des notifications push et de la messagerie in-app</span><span class="sxs-lookup"><span data-stu-id="92602-141"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="92602-142">Mettre à jour hello EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="92602-142">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="92602-143">Ouvrez hello **EngagementConfiguration** fichier de script à partir de hello dossier et de mise à jour du Kit de développement logiciel hello **ANDROID\_GOOGLE\_nombre** avec hello **projet Google Nombre** obtenu précédemment à partir du portail des développeurs de Cloud de Google hello.</span><span class="sxs-lookup"><span data-stu-id="92602-143">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **ANDROID\_GOOGLE\_NUMBER** with hello **Google Project Number** you obtained earlier from hello Google Cloud Developer portal.</span></span> <span data-ttu-id="92602-144">Il s’agit d’une chaîne de valeur donc pas vraiment tooenclose dans des guillemets doubles.</span><span class="sxs-lookup"><span data-stu-id="92602-144">This is a string value so make sure tooenclose it in double quotes.</span></span> 
   
    ![][75]
2. <span data-ttu-id="92602-145">Enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="92602-145">Save hello file.</span></span> 
3. <span data-ttu-id="92602-146">Exécutez **File -> Engagement -> Generate Android Manifest** (Fichier -> Engagement -> Générer le manifeste Android).</span><span class="sxs-lookup"><span data-stu-id="92602-146">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="92602-147">Il s’agit plug-in hello ajoutée par hello Kit de développement logiciel de Mobile Engagement et en cliquant sur elle met automatiquement à jour les paramètres du projet.</span><span class="sxs-lookup"><span data-stu-id="92602-147">This is hello plugin added by hello Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

### <a name="configure-hello-app-tooreceive-notifications"></a><span data-ttu-id="92602-148">Configurer des notifications de tooreceive l’application hello</span><span class="sxs-lookup"><span data-stu-id="92602-148">Configure hello app tooreceive notifications</span></span>
1. <span data-ttu-id="92602-149">Ouvrez hello **PlayerController** script joint toohello d’objet lecteur pour la modification.</span><span class="sxs-lookup"><span data-stu-id="92602-149">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="92602-150">Ajouter hello suivant toohello `Start()` (méthode)</span><span class="sxs-lookup"><span data-stu-id="92602-150">Add hello following toohello `Start()` method</span></span>
   
        EngagementReachAgent.Initialize();
3. <span data-ttu-id="92602-151">Maintenant que hello application est mise à jour, déployer et exécuter l’application hello sur un appareil par les instructions ci-dessous hello.</span><span class="sxs-lookup"><span data-stu-id="92602-151">Now that hello app is updated, deploy and run hello app on a device per hello instructions provided below.</span></span> 

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
