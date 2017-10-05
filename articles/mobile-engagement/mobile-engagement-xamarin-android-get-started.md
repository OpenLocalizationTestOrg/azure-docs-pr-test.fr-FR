---
title: "Prise en main d’Azure Mobile Engagement pour Xamarin.Android"
description: "Découvrez comment utiliser Azure Mobile Engagement avec les analyses et les notifications Push pour les applications Xamarin.Android."
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
ms.openlocfilehash: 7b3d01b32c2d5a40448fc22861cd45f612238f2f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a><span data-ttu-id="4b626-103">Prise en main d’Azure Mobile Engagement pour les applications Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="4b626-103">Get Started with Azure Mobile Engagement for Xamarin.Android Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="4b626-104">Cette rubrique montre comment utiliser Azure Mobile Engagement pour comprendre l’utilisation de votre application et envoyer des notifications Push à des utilisateurs segmentés d’une application Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="4b626-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Xamarin.Android application.</span></span>
<span data-ttu-id="4b626-105">Ce didacticiel montre un scénario de diffusion simple à l'aide de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="4b626-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="4b626-106">À cette occasion, vous allez créer une application Xamarin.Android vide qui recueille des données de base et reçoit des notifications Push à l’aide de Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="4b626-106">In it, you create a blank Xamarin.Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

> [!NOTE]
> <span data-ttu-id="4b626-107">Le service Azure Mobile Engagement ne sera plus disponible à partir de mars 2018. Actuellement, il reste uniquement accessible aux clients déjà abonnés à ce service.</span><span class="sxs-lookup"><span data-stu-id="4b626-107">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="4b626-108">Pour plus d’informations, consultez la page [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="4b626-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="4b626-109">Ce didacticiel requiert les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4b626-109">This tutorial requires the following:</span></span>

* <span data-ttu-id="4b626-110">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="4b626-110">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="4b626-111">Vous pouvez également utiliser Visual Studio avec Xamarin, mais ce didacticiel utilise Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="4b626-111">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="4b626-112">Pour obtenir des instructions sur l’installation, consultez la page [Configuration et installation pour Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="4b626-112">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* [<span data-ttu-id="4b626-113">Kit de développement logiciel (SDK) Mobile Engagement pour Xamarin</span><span class="sxs-lookup"><span data-stu-id="4b626-113">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="4b626-114">Pour suivre ce didacticiel, vous avez besoin d'un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="4b626-114">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="4b626-115">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="4b626-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="4b626-116">Pour plus d'informations, consultez la page [Essai gratuit d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="4b626-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="4b626-117"><a id="setup-azme"></a>Configuration de Mobile Engagement pour votre application Android</span><span class="sxs-lookup"><span data-stu-id="4b626-117"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="4b626-118"><a id="connecting-app"></a>Connexion de votre application au serveur principal Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="4b626-118"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="4b626-119">Ce didacticiel aborde l'intégration de base qui correspond aux éléments nécessaires à la collection de données et à l'envoi de notifications push.</span><span class="sxs-lookup"><span data-stu-id="4b626-119">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> 

<span data-ttu-id="4b626-120">Nous allons créer une application de base à l’aide de Xamarin Studio pour illustrer l’intégration.</span><span class="sxs-lookup"><span data-stu-id="4b626-120">We will create a basic app with Xamarin Studio to demonstrate the integration.</span></span>

### <a name="create-a-new-xamarinandroid-project"></a><span data-ttu-id="4b626-121">Créer un projet Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="4b626-121">Create a new Xamarin.Android project</span></span>
1. <span data-ttu-id="4b626-122">Démarrez **Xamarin Studio**. Accédez à **File** -> **New** -> **Solution** (Fichier > Nouveau > Solution).</span><span class="sxs-lookup"><span data-stu-id="4b626-122">Launch **Xamarin Studio** Go to **File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="4b626-123">Sélectionnez **Android App** (Application Android) et vérifiez que **C#** est le langage sélectionné, puis cliquez sur **Next** (Suivant).</span><span class="sxs-lookup"><span data-stu-id="4b626-123">Select **Android App** then make sure the selected language is **C#** and click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="4b626-124">Renseignez les champs **App Name** (Nom de l’application) et **Organization Identifier** (Identifiant de l’organisation).</span><span class="sxs-lookup"><span data-stu-id="4b626-124">Fill in the **App Name** and the **Organization Identifier**.</span></span> <span data-ttu-id="4b626-125">Veillez à cocher la case **Google Play Services** (Services Google Play), puis cliquez sur **Next** (Suivant).</span><span class="sxs-lookup"><span data-stu-id="4b626-125">Make sure to checkmark **Google Play Services** and then click **Next**.</span></span> 
   
    ![][3]
4. <span data-ttu-id="4b626-126">Mettez à jour les champs **Project Name** (Nom du projet), **Solution Name** (Nom de la solution) et **Location** (Emplacement) si nécessaire, puis cliquez sur **Create** (Créer).</span><span class="sxs-lookup"><span data-stu-id="4b626-126">Update the **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="4b626-127">Xamarin Studio crée l’application dans laquelle nous allons intégrer Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="4b626-127">Xamarin Studio will create the app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="4b626-128">Connexion de votre application au serveur principal Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="4b626-128">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="4b626-129">Dans la fenêtre des solutions, cliquez avec le bouton droit sur le dossier **Packages** (Packages), puis sélectionnez **Add Packages...** (Ajouter des packages...).</span><span class="sxs-lookup"><span data-stu-id="4b626-129">Right click the **Packages** folder in the Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="4b626-130">Recherchez **Microsoft Azure Mobile Engagement Xamarin SDK** et ajoutez-le à votre solution.</span><span class="sxs-lookup"><span data-stu-id="4b626-130">Search for the **Microsoft Azure Mobile Engagement Xamarin SDK** and add it to your solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="4b626-131">Ouvrez **MainActivity.cs** et ajoutez les instructions using suivantes :</span><span class="sxs-lookup"><span data-stu-id="4b626-131">Open **MainActivity.cs** and add the following using statements:</span></span>
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. <span data-ttu-id="4b626-132">Dans la méthode `OnCreate` , ajoutez ce qui suit pour initialiser la connexion avec le serveur principal Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="4b626-132">In the `OnCreate` method, add the following to initialize the connection with Mobile Engagement backend.</span></span> <span data-ttu-id="4b626-133">Veillez à ajouter la chaîne **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="4b626-133">Make sure to add your **ConnectionString**.</span></span> 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="4b626-134">Ajouter des autorisations et une déclaration de service</span><span class="sxs-lookup"><span data-stu-id="4b626-134">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="4b626-135">Ouvrez le fichier **Manifest.xml** sous le dossier Properties.</span><span class="sxs-lookup"><span data-stu-id="4b626-135">Open up the **Manifest.xml** file under the Properties folder.</span></span> <span data-ttu-id="4b626-136">Sélectionnez l’onglet Source afin de mettre directement à jour la source XML.</span><span class="sxs-lookup"><span data-stu-id="4b626-136">Select Source tab so that you directly update the XML source.</span></span>
2. <span data-ttu-id="4b626-137">Ajoutez ces autorisations au fichier Manifest.xml (qui se trouve sous le dossier **Properties**) de votre projet, juste avant ou après la balise `<application>` :</span><span class="sxs-lookup"><span data-stu-id="4b626-137">Add these permissions to the Manifest.xml (which can be found under the **Properties** folder) of your project immediately before or after the `<application>` tag:</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. <span data-ttu-id="4b626-138">Ajoutez le code suivant entre les balises `<application>`et`</application>` pour déclarer le service de l'agent :</span><span class="sxs-lookup"><span data-stu-id="4b626-138">Add the following between the `<application>` and `</application>` tags to declare the agent service:</span></span>
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. <span data-ttu-id="4b626-139">Dans le code que vous venez de coller, remplacez `"<Your application name>"` dans l’étiquette.</span><span class="sxs-lookup"><span data-stu-id="4b626-139">In the code you just pasted, replace `"<Your application name>"` in the label.</span></span> <span data-ttu-id="4b626-140">Cet élément s’affiche dans le menu **Paramètres** où les utilisateurs peuvent voir les services qui sont en cours d’exécution sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="4b626-140">This is displayed in the **Settings** menu where users can see services running on the device.</span></span> <span data-ttu-id="4b626-141">Vous pouvez, par exemple, ajouter le mot « Service » dans cette étiquette.</span><span class="sxs-lookup"><span data-stu-id="4b626-141">You can add the word "Service" in that label for example.</span></span>

### <a name="send-a-screen-to-mobile-engagement"></a><span data-ttu-id="4b626-142">Envoyer un écran à Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="4b626-142">Send a screen to Mobile Engagement</span></span>
<span data-ttu-id="4b626-143">Pour commencer à envoyer des données et à vous assurer que les utilisateurs sont actifs, vous devez envoyer au moins un écran au serveur principal Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="4b626-143">In order to start sending data and ensuring the users are active, you must send at least one screen to the Mobile Engagement backend.</span></span> <span data-ttu-id="4b626-144">Pour ce faire, vérifiez que `MainActivity` hérite de `EngagementActivity` à la place de `Activity`.</span><span class="sxs-lookup"><span data-stu-id="4b626-144">For doing this - ensure that the `MainActivity` inherits from `EngagementActivity` instead of `Activity`.</span></span>

    public class MainActivity : EngagementActivity

<span data-ttu-id="4b626-145">Si vous ne pouvez pas hériter de `EngagementActivity`, vous devez alors ajouter les méthodes `.StartActivity` et `.EndActivity` respectivement dans `OnResume` et `OnPause`.</span><span class="sxs-lookup"><span data-stu-id="4b626-145">Alternatively, if you cannot inherit from `EngagementActivity` then you must add `.StartActivity` and `.EndActivity` methods in `OnResume` and `OnPause` respectively.</span></span>  

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

## <span data-ttu-id="4b626-146"><a id="monitor"></a>Connexion d’application avec l’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="4b626-146"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="4b626-147"><a id="integrate-push"></a>Activation des notifications Push et de la messagerie in-app</span><span class="sxs-lookup"><span data-stu-id="4b626-147"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="4b626-148">Mobile Engagement vous permet d’interagir et d’ATTEINDRE vos utilisateurs à l’aide de notifications Push et de la messagerie in-app dans le cadre de campagnes.</span><span class="sxs-lookup"><span data-stu-id="4b626-148">Mobile Engagement allows you to interact with and REACH your users with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="4b626-149">Ce module s'appelle Couverture dans le portail Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="4b626-149">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="4b626-150">Les sections suivantes vous permettent de configurer votre application pour la réception des notifications.</span><span class="sxs-lookup"><span data-stu-id="4b626-150">The following sections sets up your app to receive them.</span></span>

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
