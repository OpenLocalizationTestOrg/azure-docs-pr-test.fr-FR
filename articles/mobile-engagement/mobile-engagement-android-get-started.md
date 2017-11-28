---
title: "Prise en main d’Azure Mobile Engagement pour les applications Android"
description: "Découvrez comment utiliser Azure Mobile Engagement avec les analyses et les notifications Push pour les applications Android."
services: mobile-engagement
documentationcenter: android
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3c286c6d-cfef-4e3e-9b2c-715429fe82db
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: dc255a930bf71e6ef6d964bc5e3472a38ce4e467
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a><span data-ttu-id="c872d-103">Prise en main d’Azure Mobile Engagement pour les applications Android</span><span class="sxs-lookup"><span data-stu-id="c872d-103">Get started with Azure Mobile Engagement for Android apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="c872d-104">Cette rubrique montre comment utiliser Azure Mobile Engagement pour comprendre l’utilisation de votre application et envoyer des notifications Push à des utilisateurs segmentés d’une application Android.</span><span class="sxs-lookup"><span data-stu-id="c872d-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of an Android application.</span></span>
<span data-ttu-id="c872d-105">Ce didacticiel montre un scénario de diffusion simple à l'aide de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="c872d-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="c872d-106">À cette occasion, vous allez créer une application Android vide qui recueille des données de base et reçoit des notifications Push à l'aide de Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="c872d-106">In it, you create a blank Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c872d-107">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="c872d-107">Prerequisites</span></span>
<span data-ttu-id="c872d-108">Pour suivre ce didacticiel, vous avez besoin des [Outils de développement Android](https://developer.android.com/sdk/index.html), qui incluent l'environnement de développement intégré Android Studio et la dernière plateforme Android.</span><span class="sxs-lookup"><span data-stu-id="c872d-108">Completing this tutorial requires the [Android Developer Tools](https://developer.android.com/sdk/index.html), which includes the Android Studio integrated development environment, and the latest Android platform.</span></span>

<span data-ttu-id="c872d-109">Le [Kit de développement logiciel (SDK) Mobile Engagement Android](https://aka.ms/vq9mfn)est également requis.</span><span class="sxs-lookup"><span data-stu-id="c872d-109">It also requires the [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c872d-110">Pour effectuer ce didacticiel, vous avez besoin d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="c872d-110">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="c872d-111">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="c872d-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c872d-112">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="c872d-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span></span>
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a><span data-ttu-id="c872d-113">Configuration de Mobile Engagement pour votre application Android</span><span class="sxs-lookup"><span data-stu-id="c872d-113">Set up Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="c872d-114">Connexion de votre application au serveur principal Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="c872d-114">Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="c872d-115">Ce didacticiel aborde l'intégration de base qui correspond aux éléments nécessaires à la collection de données et à l'envoi de notifications push.</span><span class="sxs-lookup"><span data-stu-id="c872d-115">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="c872d-116">Vous allez créer une application de base avec Android Studio afin d’illustrer l’intégration.</span><span class="sxs-lookup"><span data-stu-id="c872d-116">You create a basic app with Android Studio to demonstrate the integration.</span></span>

<span data-ttu-id="c872d-117">Vous trouverez la documentation complète sur l’intégration dans le [Kit de développement logiciel (SDK) Mobile Engagement pour Android](mobile-engagement-android-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c872d-117">The complete integration documentation can be found in the [Mobile Engagement Android SDK integration](mobile-engagement-android-sdk-overview.md).</span></span>

### <a name="create-an-android-project"></a><span data-ttu-id="c872d-118">Création d’une application Android</span><span class="sxs-lookup"><span data-stu-id="c872d-118">Create an Android project</span></span>
1. <span data-ttu-id="c872d-119">Démarrez **Android Studio** et, dans le menu contextuel, sélectionnez **Démarrer un nouveau projet Android Studio**.</span><span class="sxs-lookup"><span data-stu-id="c872d-119">Start **Android Studio**, and in the pop-up, select **Start a new Android Studio project**.</span></span>

    ![][1]
2. <span data-ttu-id="c872d-120">Indiquez un nom d’application et un domaine d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="c872d-120">Provide an app name and company domain.</span></span> <span data-ttu-id="c872d-121">Notez les valeurs que vous saisissez, car vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="c872d-121">Make a note of what you are filling, because you need it later.</span></span> <span data-ttu-id="c872d-122">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="c872d-122">Click **Next**.</span></span>

    ![][2]
3. <span data-ttu-id="c872d-123">Sélectionnez le niveau d’API et le facteur de forme cible, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="c872d-123">Select the target form factor and API level, and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c872d-124">Mobile Engagement requiert au minimum le niveau d'API 10 (Android 2.3.3).</span><span class="sxs-lookup"><span data-stu-id="c872d-124">Mobile Engagement requires API level 10 minimum (Android 2.3.3).</span></span>
   >
   >

    ![][3]
4. <span data-ttu-id="c872d-125">Sélectionnez ici **Blank Activity** (Activité vide), qui sera le seul écran de cette application, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="c872d-125">Select **Blank Activity** here, which is the only screen for this app and click **Next**.</span></span>

    ![][4]
5. <span data-ttu-id="c872d-126">Enfin, laissez les valeurs par défaut et cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="c872d-126">Finally, leave the defaults as is and click **Finish**.</span></span>

    ![][5]

<span data-ttu-id="c872d-127">Android Studio crée l’application de démonstration à laquelle nous allons intégrer Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="c872d-127">Android Studio now creates the demo app into which we integrate Mobile Engagement.</span></span>

### <a name="include-the-sdk-library-in-your-project"></a><span data-ttu-id="c872d-128">Inclure la bibliothèque du Kit de développement logiciel (SDK) dans votre projet</span><span class="sxs-lookup"><span data-stu-id="c872d-128">Include the SDK library in your project</span></span>
1. <span data-ttu-id="c872d-129">Téléchargez le [Kit SDK Mobile Engagement Android](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="c872d-129">Download the [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>
2. <span data-ttu-id="c872d-130">Extrayez le fichier d'archive dans un dossier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c872d-130">Extract the archive file to a folder in your computer.</span></span>
3. <span data-ttu-id="c872d-131">Identifiez la bibliothèque .jar correspondant à la version actuelle de ce Kit SDK et copiez-la dans le Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="c872d-131">Identify the .jar library for the current version of this SDK and copy it to the Clipboard.</span></span>

      ![][6]
4. <span data-ttu-id="c872d-132">Accédez à la section **Projet** (1) et collez le fichier .jar dans le dossier libs (2).</span><span class="sxs-lookup"><span data-stu-id="c872d-132">Navigate to the **Project** section (1) and paste the .jar in the libs folder (2).</span></span>

      ![][7]
5. <span data-ttu-id="c872d-133">Pour charger la bibliothèque, synchronisez le projet.</span><span class="sxs-lookup"><span data-stu-id="c872d-133">To load the library, sync the project .</span></span>

      ![][8]

### <a name="connect-your-app-to-mobile-engagement-backend-with-the-connection-string"></a><span data-ttu-id="c872d-134">Connectez votre application au serveur principal Mobile Engagement à l'aide de la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="c872d-134">Connect your app to Mobile Engagement backend with the Connection String</span></span>
1. <span data-ttu-id="c872d-135">Copiez les lignes de code suivantes dans la création d’activité (cette opération doit être effectuée à un seul emplacement de votre application, généralement dans l’activité principale).</span><span class="sxs-lookup"><span data-stu-id="c872d-135">Copy the following lines of code into the activity creation (must be done only in one place of your application, usually the main activity).</span></span> <span data-ttu-id="c872d-136">Pour cet exemple d’application, ouvrez MainActivity sous src -> main -> dossier java et ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="c872d-136">For this sample app, open up the MainActivity under src -> main -> java folder and add the following:</span></span>

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. <span data-ttu-id="c872d-137">Résolvez les références en appuyant sur Alt + Entrée ou en ajoutant les instructions d’importation suivantes :</span><span class="sxs-lookup"><span data-stu-id="c872d-137">Resolve the references by pressing Alt + Enter or adding the following import statements:</span></span>

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. <span data-ttu-id="c872d-138">De retour sur le portail Azure Classic, dans la page **Informations de connexion** de votre application, copiez la **chaîne de connexion**.</span><span class="sxs-lookup"><span data-stu-id="c872d-138">Go back to the Azure Classic Portal in your app's **Connection Info** page and copy the **Connection String**.</span></span>

      ![][9]
4. <span data-ttu-id="c872d-139">Collez-la dans le paramètre `setConnectionString`, en remplaçant la chaîne entière comme indiqué dans le code suivant :</span><span class="sxs-lookup"><span data-stu-id="c872d-139">Paste it into the `setConnectionString` parameter, replacing the entire string shown in the following code:</span></span>

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="c872d-140">Ajouter des autorisations et une déclaration de service</span><span class="sxs-lookup"><span data-stu-id="c872d-140">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="c872d-141">Ajoutez ces autorisations au fichier Manifest.xml de votre projet, juste avant ou après la balise `<application>` :</span><span class="sxs-lookup"><span data-stu-id="c872d-141">Add these permissions to the Manifest.xml of your project immediately before or after the `<application>` tag:</span></span>

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. <span data-ttu-id="c872d-142">Pour déclarer le service de l’agent, ajoutez ce code entre les balises `<application>` et `</application>` :</span><span class="sxs-lookup"><span data-stu-id="c872d-142">To declare the agent service, add this code between the `<application>` and `</application>` tags:</span></span>

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. <span data-ttu-id="c872d-143">Dans le code que vous avez collé, remplacez `"<Your application name>"` dans l’étiquette qui s’affiche dans le menu **Paramètres** indiquant les services exécutés sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="c872d-143">In the code you pasted, replace `"<Your application name>"` in the label, which is displayed in the **Settings** menu where you can see services running on the device.</span></span> <span data-ttu-id="c872d-144">Vous pouvez, par exemple, ajouter le mot « Service » dans cette étiquette.</span><span class="sxs-lookup"><span data-stu-id="c872d-144">You can add the word "Service" in that label for example.</span></span>

### <a name="send-a-screen-to-mobile-engagement"></a><span data-ttu-id="c872d-145">Envoyer un écran à Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="c872d-145">Send a screen to Mobile Engagement</span></span>
<span data-ttu-id="c872d-146">Pour commencer à envoyer des données et vérifier que les utilisateurs sont actifs, vous devez envoyer au moins un écran (activité) au serveur principal Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="c872d-146">To start sending data and ensure that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

<span data-ttu-id="c872d-147">Accédez à **MainActivity.java** et ajoutez le code suivant pour remplacer la classe de base **MainActivity** par **EngagementActivity** :</span><span class="sxs-lookup"><span data-stu-id="c872d-147">Go to **MainActivity.java** and add the following to replace the base class of **MainActivity** to **EngagementActivity**:</span></span>

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> <span data-ttu-id="c872d-148">Si vous n’utilisez pas la classe de base *Activity*, consultez l’article relatif aux [fonctionnalités de rapports avancées d’Android](mobile-engagement-android-advanced-reporting.md) pour savoir comment hériter de classes différentes.</span><span class="sxs-lookup"><span data-stu-id="c872d-148">If your base class is not *Activity*, consult [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) for how to inherit from different classes.</span></span>
>
>

<span data-ttu-id="c872d-149">Mettez en commentaire la ligne suivante pour cet exemple simple de scénario :</span><span class="sxs-lookup"><span data-stu-id="c872d-149">Comment out the following line for this simple sample scenario:</span></span>

    // setSupportActionBar(toolbar);

<span data-ttu-id="c872d-150">Si vous souhaitez conserver le `ActionBar` dans votre application, consultez [Options de génération de rapports avec Engagement sur Android](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="c872d-150">If you want to keep the `ActionBar` in your app, see [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).</span></span>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="c872d-151">Connexion d’application avec l’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="c872d-151">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a><span data-ttu-id="c872d-152">Activation des notifications push et de la messagerie in-app</span><span class="sxs-lookup"><span data-stu-id="c872d-152">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="c872d-153">Pendant une campagne, Mobile Engagement vous permet d’interagir avec vos utilisateurs à l’aide de notifications Push et de messages dans l’application.</span><span class="sxs-lookup"><span data-stu-id="c872d-153">During a campaign, Mobile Engagement lets you interact with and REACH your users with push notifications and in-app messaging.</span></span> <span data-ttu-id="c872d-154">Ce module s'appelle Couverture dans le portail Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="c872d-154">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="c872d-155">La section suivante vous permet de configurer votre application pour la réception des notifications.</span><span class="sxs-lookup"><span data-stu-id="c872d-155">The following section sets up your app to receive them.</span></span>

### <a name="copy-sdk-resources-in-your-project"></a><span data-ttu-id="c872d-156">Copier les ressources du SDK dans votre projet</span><span class="sxs-lookup"><span data-stu-id="c872d-156">Copy SDK resources in your project</span></span>
1. <span data-ttu-id="c872d-157">Revenez au contenu de téléchargement de votre Kit de développement logiciel (SDK) et copiez le dossier **res** .</span><span class="sxs-lookup"><span data-stu-id="c872d-157">Navigate back to your SDK download content and copy the **res** folder.</span></span>

    ![][10]
2. <span data-ttu-id="c872d-158">Revenez à Android Studio, sélectionnez le répertoire **main** de vos fichiers de projet, puis collez-le pour ajouter les ressources à votre projet.</span><span class="sxs-lookup"><span data-stu-id="c872d-158">Go back to Android Studio, select the **main** directory of your project files, and then paste it to add the resources to your project.</span></span>

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="c872d-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c872d-159">Next steps</span></span>
<span data-ttu-id="c872d-160">Accédez au [Kit de développement logiciel (SDK) Android](mobile-engagement-android-sdk-overview.md) pour obtenir des informations détaillées sur l’intégration du kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="c872d-160">Go to [Android SDK](mobile-engagement-android-sdk-overview.md) to get detailed knowledge about the SDK integration.</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-android-get-started/android-studio-new-project.png
[2]: ./media/mobile-engagement-android-get-started/android-studio-project-props.png
[3]: ./media/mobile-engagement-android-get-started/android-studio-project-props2.png
[4]: ./media/mobile-engagement-android-get-started/android-studio-add-activity.png
[5]: ./media/mobile-engagement-android-get-started/android-studio-activity-name.png
[6]: ./media/mobile-engagement-android-get-started/sdk-content.png
[7]: ./media/mobile-engagement-android-get-started/paste-jar.png
[8]: ./media/mobile-engagement-android-get-started/sync-project.png
[9]: ./media/mobile-engagement-android-get-started/app-connection-info-page.png
[10]: ./media/mobile-engagement-android-get-started/copy-resources.png
[11]: ./media/mobile-engagement-android-get-started/paste-resources.png
