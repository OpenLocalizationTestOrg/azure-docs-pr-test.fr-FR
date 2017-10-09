---
title: aaaGet main Android applications Azure Mobile Engagement
description: "Découvrez comment toouse Azure Mobile Engagement avec analytique et des notifications push pour les applications Android."
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
ms.openlocfilehash: e8c92607691104750cdf1c4f7639a041d8a7bcd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a><span data-ttu-id="a02ff-103">Prise en main d’Azure Mobile Engagement pour les applications Android</span><span class="sxs-lookup"><span data-stu-id="a02ff-103">Get started with Azure Mobile Engagement for Android apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="a02ff-104">Cette rubrique vous montre comment toouse Azure Mobile Engagement toounderstand votre utilisation de l’application et comment toosend push utilisateurs toosegmented de notifications d’une application Android.</span><span class="sxs-lookup"><span data-stu-id="a02ff-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of an Android application.</span></span>
<span data-ttu-id="a02ff-105">Ce didacticiel illustre un scénario simple diffusion hello à l’aide de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a02ff-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="a02ff-106">À cette occasion, vous allez créer une application Android vide qui recueille des données de base et reçoit des notifications Push à l'aide de Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="a02ff-106">In it, you create a blank Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a02ff-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a02ff-107">Prerequisites</span></span>
<span data-ttu-id="a02ff-108">Ils auront terminé ce didacticiel requiert hello [Android Developer Tools](https://developer.android.com/sdk/index.html), qui inclut l’environnement de développement intégré Android hello et la plateforme Android hello la plus récente.</span><span class="sxs-lookup"><span data-stu-id="a02ff-108">Completing this tutorial requires hello [Android Developer Tools](https://developer.android.com/sdk/index.html), which includes hello Android Studio integrated development environment, and hello latest Android platform.</span></span>

<span data-ttu-id="a02ff-109">Elle requiert également hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="a02ff-109">It also requires hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a02ff-110">toocomplete ce didacticiel, vous avez besoin d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="a02ff-110">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="a02ff-111">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="a02ff-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a02ff-112">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="a02ff-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span></span>
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a><span data-ttu-id="a02ff-113">Configuration de Mobile Engagement pour votre application Android</span><span class="sxs-lookup"><span data-stu-id="a02ff-113">Set up Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="a02ff-114">Se connecter à votre serveur principal d’application toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="a02ff-114">Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="a02ff-115">Ce didacticiel présente une « intégration de base », qui est hello minimal requis toocollect données et envoyer une notification push.</span><span class="sxs-lookup"><span data-stu-id="a02ff-115">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="a02ff-116">Vous créez une application de base avec l’intégration de hello toodemonstrate Android Studio.</span><span class="sxs-lookup"><span data-stu-id="a02ff-116">You create a basic app with Android Studio toodemonstrate hello integration.</span></span>

<span data-ttu-id="a02ff-117">Vous trouverez la documentation sur l’intégration complète Hello dans hello [intégration de Mobile Engagement Android SDK](mobile-engagement-android-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a02ff-117">hello complete integration documentation can be found in hello [Mobile Engagement Android SDK integration](mobile-engagement-android-sdk-overview.md).</span></span>

### <a name="create-an-android-project"></a><span data-ttu-id="a02ff-118">Création d’une application Android</span><span class="sxs-lookup"><span data-stu-id="a02ff-118">Create an Android project</span></span>
1. <span data-ttu-id="a02ff-119">Démarrer **Android Studio**et dans la fenêtre contextuelle hello, sélectionnez **démarrer un nouveau projet Android Studio**.</span><span class="sxs-lookup"><span data-stu-id="a02ff-119">Start **Android Studio**, and in hello pop-up, select **Start a new Android Studio project**.</span></span>

    ![][1]
2. <span data-ttu-id="a02ff-120">Indiquez un nom d’application et un domaine d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="a02ff-120">Provide an app name and company domain.</span></span> <span data-ttu-id="a02ff-121">Notez les valeurs que vous saisissez, car vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="a02ff-121">Make a note of what you are filling, because you need it later.</span></span> <span data-ttu-id="a02ff-122">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="a02ff-122">Click **Next**.</span></span>

    ![][2]
3. <span data-ttu-id="a02ff-123">Sélectionnez le facteur de forme hello cible et le niveau de l’API, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="a02ff-123">Select hello target form factor and API level, and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a02ff-124">Mobile Engagement requiert au minimum le niveau d'API 10 (Android 2.3.3).</span><span class="sxs-lookup"><span data-stu-id="a02ff-124">Mobile Engagement requires API level 10 minimum (Android 2.3.3).</span></span>
   >
   >

    ![][3]
4. <span data-ttu-id="a02ff-125">Sélectionnez **activité vide** ici, écran uniquement hello pour cette application et le clic **suivant**.</span><span class="sxs-lookup"><span data-stu-id="a02ff-125">Select **Blank Activity** here, which is hello only screen for this app and click **Next**.</span></span>

    ![][4]
5. <span data-ttu-id="a02ff-126">Enfin, laissez les valeurs par défaut hello et cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="a02ff-126">Finally, leave hello defaults as is and click **Finish**.</span></span>

    ![][5]

<span data-ttu-id="a02ff-127">Android Studio crée app de démo hello dans laquelle nous intégrer Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a02ff-127">Android Studio now creates hello demo app into which we integrate Mobile Engagement.</span></span>

### <a name="include-hello-sdk-library-in-your-project"></a><span data-ttu-id="a02ff-128">Inclure la bibliothèque du Kit de développement logiciel hello dans votre projet</span><span class="sxs-lookup"><span data-stu-id="a02ff-128">Include hello SDK library in your project</span></span>
1. <span data-ttu-id="a02ff-129">Télécharger hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="a02ff-129">Download hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>
2. <span data-ttu-id="a02ff-130">Extrayez hello fichier tooa dossier d’archivage dans votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a02ff-130">Extract hello archive file tooa folder in your computer.</span></span>
3. <span data-ttu-id="a02ff-131">Identifier la bibliothèque de .jar hello pour la version actuelle de hello de ce Kit de développement logiciel et copiez-le toohello du Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="a02ff-131">Identify hello .jar library for hello current version of this SDK and copy it toohello Clipboard.</span></span>

      ![][6]
4. <span data-ttu-id="a02ff-132">Accédez toohello **projet** section (1) et collez hello .jar dans le dossier de bibliothèques hello (2).</span><span class="sxs-lookup"><span data-stu-id="a02ff-132">Navigate toohello **Project** section (1) and paste hello .jar in hello libs folder (2).</span></span>

      ![][7]
5. <span data-ttu-id="a02ff-133">bibliothèque de hello tooload, projet hello de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="a02ff-133">tooload hello library, sync hello project .</span></span>

      ![][8]

### <a name="connect-your-app-toomobile-engagement-backend-with-hello-connection-string"></a><span data-ttu-id="a02ff-134">Rejoignez votre serveur principal d’application tooMobile Engagement hello chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="a02ff-134">Connect your app tooMobile Engagement backend with hello Connection String</span></span>
1. <span data-ttu-id="a02ff-135">Copiez hello après des lignes de code dans la création de l’activité hello (doit être effectuée uniquement dans un emplacement de votre application, généralement une activité principale hello).</span><span class="sxs-lookup"><span data-stu-id="a02ff-135">Copy hello following lines of code into hello activity creation (must be done only in one place of your application, usually hello main activity).</span></span> <span data-ttu-id="a02ff-136">Pour cet exemple d’application, ouvrez hello MainActivity sous src -> principal -> dossier java et ajoutez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="a02ff-136">For this sample app, open up hello MainActivity under src -> main -> java folder and add hello following:</span></span>

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. <span data-ttu-id="a02ff-137">Résoudre les références de hello en appuyant sur Alt + Entrée ou en ajoutant des hello suivant les instructions d’importation :</span><span class="sxs-lookup"><span data-stu-id="a02ff-137">Resolve hello references by pressing Alt + Enter or adding hello following import statements:</span></span>

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. <span data-ttu-id="a02ff-138">Revenir en arrière toohello portail classique de Azure dans votre application **informations de connexion** page et copie hello **chaîne de connexion**.</span><span class="sxs-lookup"><span data-stu-id="a02ff-138">Go back toohello Azure Classic Portal in your app's **Connection Info** page and copy hello **Connection String**.</span></span>

      ![][9]
4. <span data-ttu-id="a02ff-139">Collez-le dans hello `setConnectionString` paramètre, en remplaçant la chaîne entière de hello Bonjour suivant de code :</span><span class="sxs-lookup"><span data-stu-id="a02ff-139">Paste it into hello `setConnectionString` parameter, replacing hello entire string shown in hello following code:</span></span>

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="a02ff-140">Ajouter des autorisations et une déclaration de service</span><span class="sxs-lookup"><span data-stu-id="a02ff-140">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="a02ff-141">Ajoutez ces toohello autorisations Manifest.xml de votre projet immédiatement avant ou après hello `<application>` balise :</span><span class="sxs-lookup"><span data-stu-id="a02ff-141">Add these permissions toohello Manifest.xml of your project immediately before or after hello `<application>` tag:</span></span>

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. <span data-ttu-id="a02ff-142">toodeclare hello du service de l’agent, ajoutez le code entre hello `<application>` et `</application>` balises :</span><span class="sxs-lookup"><span data-stu-id="a02ff-142">toodeclare hello agent service, add this code between hello `<application>` and `</application>` tags:</span></span>

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. <span data-ttu-id="a02ff-143">Dans le code hello vous avez collé, remplacez `"<Your application name>"` dans l’étiquette de hello, qui s’affichent dans hello **paramètres** menu où vous pouvez consulter les services en cours d’exécution sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="a02ff-143">In hello code you pasted, replace `"<Your application name>"` in hello label, which is displayed in hello **Settings** menu where you can see services running on hello device.</span></span> <span data-ttu-id="a02ff-144">Vous pouvez ajouter le mot hello « Service » de cette étiquette par exemple.</span><span class="sxs-lookup"><span data-stu-id="a02ff-144">You can add hello word "Service" in that label for example.</span></span>

### <a name="send-a-screen-toomobile-engagement"></a><span data-ttu-id="a02ff-145">Envoyer un tooMobile écran Engagement</span><span class="sxs-lookup"><span data-stu-id="a02ff-145">Send a screen tooMobile Engagement</span></span>
<span data-ttu-id="a02ff-146">toostart envoi de données et vous assurer que les utilisateurs hello sont actifs, vous devez envoyer au moins un principal de Mobile Engagement toohello écran (activité).</span><span class="sxs-lookup"><span data-stu-id="a02ff-146">toostart sending data and ensure that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

<span data-ttu-id="a02ff-147">Accédez trop**MainActivity.java** et ajoutez hello après la classe de base pour hello tooreplace **MainActivity** trop**EngagementActivity**:</span><span class="sxs-lookup"><span data-stu-id="a02ff-147">Go too**MainActivity.java** and add hello following tooreplace hello base class of **MainActivity** too**EngagementActivity**:</span></span>

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> <span data-ttu-id="a02ff-148">Si votre classe de base n’est pas *activité*, consultez [avancé de Reporting Android](mobile-engagement-android-advanced-reporting.md) sur la manière de tooinherit à partir de différentes classes.</span><span class="sxs-lookup"><span data-stu-id="a02ff-148">If your base class is not *Activity*, consult [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) for how tooinherit from different classes.</span></span>
>
>

<span data-ttu-id="a02ff-149">Commentaire hello ligne pour ce scénario d’exemple simple suivante :</span><span class="sxs-lookup"><span data-stu-id="a02ff-149">Comment out hello following line for this simple sample scenario:</span></span>

    // setSupportActionBar(toolbar);

<span data-ttu-id="a02ff-150">Si vous souhaitez tookeep hello `ActionBar` dans votre application, consultez [avancé de Reporting Android](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="a02ff-150">If you want tookeep hello `ActionBar` in your app, see [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).</span></span>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="a02ff-151">Connexion d’application avec l’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="a02ff-151">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a><span data-ttu-id="a02ff-152">Activation des notifications push et de la messagerie in-app</span><span class="sxs-lookup"><span data-stu-id="a02ff-152">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="a02ff-153">Pendant une campagne, Mobile Engagement vous permet d’interagir avec vos utilisateurs à l’aide de notifications Push et de messages dans l’application.</span><span class="sxs-lookup"><span data-stu-id="a02ff-153">During a campaign, Mobile Engagement lets you interact with and REACH your users with push notifications and in-app messaging.</span></span> <span data-ttu-id="a02ff-154">Ce module est appelé portée dans le portail Mobile Engagement de hello.</span><span class="sxs-lookup"><span data-stu-id="a02ff-154">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="a02ff-155">Hello suivant la section des tooreceive de votre application les définit.</span><span class="sxs-lookup"><span data-stu-id="a02ff-155">hello following section sets up your app tooreceive them.</span></span>

### <a name="copy-sdk-resources-in-your-project"></a><span data-ttu-id="a02ff-156">Copier les ressources du SDK dans votre projet</span><span class="sxs-lookup"><span data-stu-id="a02ff-156">Copy SDK resources in your project</span></span>
1. <span data-ttu-id="a02ff-157">Accédez tooyour arrière du téléchargement contenu et la copie du hello du Kit de développement logiciel **res** dossier.</span><span class="sxs-lookup"><span data-stu-id="a02ff-157">Navigate back tooyour SDK download content and copy hello **res** folder.</span></span>

    ![][10]
2. <span data-ttu-id="a02ff-158">Revenir en arrière tooAndroid Studio, sélectionnez hello **principal** répertoire de vos fichiers projet, puis collez-la tooadd hello de ressources tooyour project.</span><span class="sxs-lookup"><span data-stu-id="a02ff-158">Go back tooAndroid Studio, select hello **main** directory of your project files, and then paste it tooadd hello resources tooyour project.</span></span>

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="a02ff-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a02ff-159">Next steps</span></span>
<span data-ttu-id="a02ff-160">Accédez trop[du SDK Android](mobile-engagement-android-sdk-overview.md) tooget connaissance sur hello intégration du Kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="a02ff-160">Go too[Android SDK](mobile-engagement-android-sdk-overview.md) tooget detailed knowledge about hello SDK integration.</span></span>

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
