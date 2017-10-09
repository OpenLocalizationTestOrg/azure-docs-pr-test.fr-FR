---
title: "aaaGet main d’Azure Mobile Engagement pour Xamarin.Android"
description: "Découvrez comment toouse Azure Mobile Engagement avec Analytique et les Notifications Push pour les applications de Xamarin.Android."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: fb68cf98-08a2-41b5-8e59-757469de3fe7
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/16/2016
ms.author: piyushjo
ms.openlocfilehash: 9d584fea8e8153d511258cf9b6f87f31dac6aeca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a><span data-ttu-id="18ab4-103">Prise en main d’Azure Mobile Engagement pour les applications Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="18ab4-103">Get Started with Azure Mobile Engagement for Xamarin.Android Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="18ab4-104">Cette rubrique vous montre comment toouse Azure Mobile Engagement toounderstand votre utilisation de l’application et comment toosend push utilisateurs toosegmented de notifications d’une application Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="18ab4-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Xamarin.Android application.</span></span>
<span data-ttu-id="18ab4-105">Ce didacticiel illustre un scénario simple diffusion hello à l’aide de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="18ab4-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="18ab4-106">À cette occasion, vous allez créer une application Xamarin.Android vide qui recueille des données de base et reçoit des notifications Push à l’aide de Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="18ab4-106">In it, you create a blank Xamarin.Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

> [!NOTE]
> <span data-ttu-id="18ab4-107">Hello Azure Mobile Engagement service mars 2018 est retirée et est actuellement que les clients tooexisting disponibles.</span><span class="sxs-lookup"><span data-stu-id="18ab4-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="18ab4-108">Pour plus d’informations, consultez [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="18ab4-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="18ab4-109">Ce didacticiel requiert hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="18ab4-109">This tutorial requires hello following:</span></span>

* <span data-ttu-id="18ab4-110">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="18ab4-110">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="18ab4-111">Vous pouvez également utiliser Visual Studio avec Xamarin, mais ce didacticiel utilise Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="18ab4-111">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="18ab4-112">Pour obtenir des instructions sur l’installation, consultez la page [Configuration et installation pour Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="18ab4-112">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* [<span data-ttu-id="18ab4-113">Kit de développement logiciel (SDK) Mobile Engagement pour Xamarin</span><span class="sxs-lookup"><span data-stu-id="18ab4-113">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="18ab4-114">toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="18ab4-114">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="18ab4-115">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="18ab4-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="18ab4-116">Pour plus d'informations, consultez la page [Essai gratuit d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="18ab4-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="18ab4-117"><a id="setup-azme"></a>Configuration de Mobile Engagement pour votre application Android</span><span class="sxs-lookup"><span data-stu-id="18ab4-117"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="18ab4-118"><a id="connecting-app"></a>Se connecter à votre serveur principal d’application toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="18ab4-118"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="18ab4-119">Ce didacticiel présente une « intégration de base », qui est hello minimal requis toocollect données et envoyer une notification push.</span><span class="sxs-lookup"><span data-stu-id="18ab4-119">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> 

<span data-ttu-id="18ab4-120">Nous allons créer une application de base avec l’intégration de Xamarin Studio toodemonstrate hello.</span><span class="sxs-lookup"><span data-stu-id="18ab4-120">We will create a basic app with Xamarin Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-new-xamarinandroid-project"></a><span data-ttu-id="18ab4-121">Créer un projet Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="18ab4-121">Create a new Xamarin.Android project</span></span>
1. <span data-ttu-id="18ab4-122">Lancez **Xamarin Studio** accédez trop**fichier** -> **nouveau** -> **Solution**</span><span class="sxs-lookup"><span data-stu-id="18ab4-122">Launch **Xamarin Studio** Go too**File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="18ab4-123">Sélectionnez **application Android** puis assurez-vous que la langue hello sélectionné est **c#** et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="18ab4-123">Select **Android App** then make sure hello selected language is **C#** and click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="18ab4-124">Renseignez hello **nom de l’application** et hello **identifiant d’organisation**.</span><span class="sxs-lookup"><span data-stu-id="18ab4-124">Fill in hello **App Name** and hello **Organization Identifier**.</span></span> <span data-ttu-id="18ab4-125">Assurez-vous que toocheckmark **Services Google Play** puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="18ab4-125">Make sure toocheckmark **Google Play Services** and then click **Next**.</span></span> 
   
    ![][3]
4. <span data-ttu-id="18ab4-126">Hello de mise à jour **nom du projet**, **nom de la Solution** et **emplacement** si nécessaire et cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="18ab4-126">Update hello **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="18ab4-127">Xamarin Studio créera une application hello dans lequel nous intégrera Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="18ab4-127">Xamarin Studio will create hello app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="18ab4-128">Se connecter à votre serveur principal d’application tooMobile Engagement</span><span class="sxs-lookup"><span data-stu-id="18ab4-128">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="18ab4-129">Cliquez avec le bouton droit sur hello **Packages** dossier dans windows de Solution hello et sélectionnez **ajouter des Packages en cours...**</span><span class="sxs-lookup"><span data-stu-id="18ab4-129">Right click hello **Packages** folder in hello Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="18ab4-130">Recherchez hello **Microsoft Azure Mobile Engagement Xamarin SDK** et ajoutez-le tooyour solution.</span><span class="sxs-lookup"><span data-stu-id="18ab4-130">Search for hello **Microsoft Azure Mobile Engagement Xamarin SDK** and add it tooyour solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="18ab4-131">Ouvrez **MainActivity.cs** et ajoutez hello qui suit à l’aide des instructions :</span><span class="sxs-lookup"><span data-stu-id="18ab4-131">Open **MainActivity.cs** and add hello following using statements:</span></span>
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. <span data-ttu-id="18ab4-132">Bonjour `OnCreate` (méthode), ajouter hello après la connexion de hello tooinitialize avec le serveur principal Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="18ab4-132">In hello `OnCreate` method, add hello following tooinitialize hello connection with Mobile Engagement backend.</span></span> <span data-ttu-id="18ab4-133">Assurez-vous que tooadd votre **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="18ab4-133">Make sure tooadd your **ConnectionString**.</span></span> 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="18ab4-134">Ajouter des autorisations et une déclaration de service</span><span class="sxs-lookup"><span data-stu-id="18ab4-134">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="18ab4-135">Ouvrez hello **Manifest.xml** fichier sous le dossier Propriétés de hello.</span><span class="sxs-lookup"><span data-stu-id="18ab4-135">Open up hello **Manifest.xml** file under hello Properties folder.</span></span> <span data-ttu-id="18ab4-136">Sélectionnez l’onglet Source afin que la mise à jour source XML hello.</span><span class="sxs-lookup"><span data-stu-id="18ab4-136">Select Source tab so that you directly update hello XML source.</span></span>
2. <span data-ttu-id="18ab4-137">Ajoutez ces toohello autorisations Manifest.xml (qui peut être trouvé sous hello **propriétés** dossier) de votre projet immédiatement avant ou après hello `<application>` balise :</span><span class="sxs-lookup"><span data-stu-id="18ab4-137">Add these permissions toohello Manifest.xml (which can be found under hello **Properties** folder) of your project immediately before or after hello `<application>` tag:</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. <span data-ttu-id="18ab4-138">Ajoutez suit hello entre hello `<application>` et `</application>` balises de service de l’agent toodeclare hello :</span><span class="sxs-lookup"><span data-stu-id="18ab4-138">Add hello following between hello `<application>` and `</application>` tags toodeclare hello agent service:</span></span>
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. <span data-ttu-id="18ab4-139">Dans le code hello vous venez de coller, remplacez `"<Your application name>"` dans l’étiquette de hello.</span><span class="sxs-lookup"><span data-stu-id="18ab4-139">In hello code you just pasted, replace `"<Your application name>"` in hello label.</span></span> <span data-ttu-id="18ab4-140">Il est affiché dans hello **paramètres** menu dans lequel les utilisateurs peuvent voir les services qui s’exécutent sur le périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="18ab4-140">This is displayed in hello **Settings** menu where users can see services running on hello device.</span></span> <span data-ttu-id="18ab4-141">Vous pouvez ajouter le mot hello « Service » de cette étiquette par exemple.</span><span class="sxs-lookup"><span data-stu-id="18ab4-141">You can add hello word "Service" in that label for example.</span></span>

### <a name="send-a-screen-toomobile-engagement"></a><span data-ttu-id="18ab4-142">Envoyer un tooMobile écran Engagement</span><span class="sxs-lookup"><span data-stu-id="18ab4-142">Send a screen tooMobile Engagement</span></span>
<span data-ttu-id="18ab4-143">Dans l’ordre toostart envoi de données et en garantissant hello utilisateurs sont actifs, vous devez envoyer au moins un écran toohello Mobile Engagement principal.</span><span class="sxs-lookup"><span data-stu-id="18ab4-143">In order toostart sending data and ensuring hello users are active, you must send at least one screen toohello Mobile Engagement backend.</span></span> <span data-ttu-id="18ab4-144">Pour y parvenir-Vérifiez que hello `MainActivity` hérite `EngagementActivity` au lieu de `Activity`.</span><span class="sxs-lookup"><span data-stu-id="18ab4-144">For doing this - ensure that hello `MainActivity` inherits from `EngagementActivity` instead of `Activity`.</span></span>

    public class MainActivity : EngagementActivity

<span data-ttu-id="18ab4-145">Si vous ne pouvez pas hériter de `EngagementActivity`, vous devez alors ajouter les méthodes `.StartActivity` et `.EndActivity` respectivement dans `OnResume` et `OnPause`.</span><span class="sxs-lookup"><span data-stu-id="18ab4-145">Alternatively, if you cannot inherit from `EngagementActivity` then you must add `.StartActivity` and `.EndActivity` methods in `OnResume` and `OnPause` respectively.</span></span>  

        protected override void OnResume()
            {
                EngagementAgent.StartActivity(EngagementAgentUtils.BuildEngagementActivityName(Java.Lang.Class.FromType(this.GetType())), null);
                base.OnResume();             
            }

            protected override void OnPause()
            {
                EngagementAgent.EndActivity();
                base.OnPause();            
            }

## <span data-ttu-id="18ab4-146"><a id="monitor"></a>Connexion d’application avec l’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="18ab4-146"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="18ab4-147"><a id="integrate-push"></a>Activation des notifications push et de la messagerie in-app</span><span class="sxs-lookup"><span data-stu-id="18ab4-147"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="18ab4-148">Mobile Engagement vous permet de toointeract avec et atteindre vos utilisateurs avec des notifications push et les messages dans le contexte de hello de campagnes dans l’application.</span><span class="sxs-lookup"><span data-stu-id="18ab4-148">Mobile Engagement allows you toointeract with and REACH your users with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="18ab4-149">Ce module est appelé portée dans le portail Mobile Engagement de hello.</span><span class="sxs-lookup"><span data-stu-id="18ab4-149">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="18ab4-150">les sections suivantes de Hello configure tooreceive de votre application les.</span><span class="sxs-lookup"><span data-stu-id="18ab4-150">hello following sections sets up your app tooreceive them.</span></span>

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[1]: ./media/mobile-engagement-xamarin-android-get-started/1.png
[2]: ./media/mobile-engagement-xamarin-android-get-started/2.png
[3]: ./media/mobile-engagement-xamarin-android-get-started/3.png
[4]: ./media/mobile-engagement-xamarin-android-get-started/4.png
[5]: ./media/mobile-engagement-xamarin-android-get-started/5.png
[6]: ./media/mobile-engagement-xamarin-android-get-started/6.png
