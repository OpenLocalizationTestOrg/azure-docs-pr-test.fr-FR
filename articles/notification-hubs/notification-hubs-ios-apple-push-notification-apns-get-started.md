---
title: aaaSending tooiOS de notifications push avec Azure Notification Hubs | Documents Microsoft
description: "Dans ce didacticiel, vous découvrez comment toouse Azure Notification Hubs toosend push application iOS de tooan des notifications."
services: notification-hubs
documentationcenter: ios
keywords: notification push,notifications push,notifications push ios
author: ysxu
manager: erikre
editor: 
ms.assetid: b7fcd916-8db8-41a6-ae88-fc02d57cb914
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: d8bb47fee4c229b3ed2a7a4dbff25a56a7a7d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooios-with-azure-notification-hubs"></a><span data-ttu-id="7bc37-104">Envoi de tooiOS de notifications push avec Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="7bc37-104">Sending push notifications tooiOS with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="7bc37-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="7bc37-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="7bc37-106">toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="7bc37-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="7bc37-107">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="7bc37-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="7bc37-108">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="7bc37-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="7bc37-109">Ce didacticiel vous montre comment toouse Azure Notification Hubs toosend push application iOS de tooan des notifications.</span><span class="sxs-lookup"><span data-stu-id="7bc37-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan iOS application.</span></span> <span data-ttu-id="7bc37-110">Vous allez créer une application iOS vide qui reçoit des notifications push à l’aide de hello [les services de notifications Push Apple (APN)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span><span class="sxs-lookup"><span data-stu-id="7bc37-110">You'll create a blank iOS app that receives push notifications by using hello [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span></span> 

<span data-ttu-id="7bc37-111">Lorsque vous avez terminé, vous serez en mesure de toouse votre toobroadcast de concentrateur de notification push des appareils de hello notifications tooall votre application en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="7bc37-111">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7bc37-112">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="7bc37-112">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="7bc37-113">le code Hello terminée pour ce didacticiel se trouve [sur GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="7bc37-113">hello completed code for this tutorial can be found [on GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7bc37-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7bc37-114">Prerequisites</span></span>
<span data-ttu-id="7bc37-115">Ce didacticiel requiert hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="7bc37-115">This tutorial requires hello following:</span></span>

* <span data-ttu-id="7bc37-116">[Services mobiles iOS SDK version 1.2.4]</span><span class="sxs-lookup"><span data-stu-id="7bc37-116">[Mobile Services iOS SDK version 1.2.4]</span></span>
* <span data-ttu-id="7bc37-117">Version la plus récente de [Xcode]</span><span class="sxs-lookup"><span data-stu-id="7bc37-117">Latest version of [Xcode]</span></span>
* <span data-ttu-id="7bc37-118">Un appareil compatible iOS 8 (ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="7bc37-118">An iOS 8 (or later version)-capable device</span></span>
* <span data-ttu-id="7bc37-119">[programme pour développeurs Apple](https://developer.apple.com/programs/)</span><span class="sxs-lookup"><span data-stu-id="7bc37-119">[Apple Developer Program](https://developer.apple.com/programs/) membership.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="7bc37-120">En raison de la configuration requise pour les notifications push, vous devez déployer et tester des notifications push sur un appareil physique iOS (iPhone ou iPad) au lieu de hello, iOS Simulator.</span><span class="sxs-lookup"><span data-stu-id="7bc37-120">Because of configuration requirements for push notifications, you must deploy and test push notifications on a physical iOS device (iPhone or iPad) instead of hello iOS Simulator.</span></span>
  > 
  > 

<span data-ttu-id="7bc37-121">Vous devez terminer ce didacticiel avant de pouvoir suivre tous les autres didacticiels Notification Hubs pour les applications iOS.</span><span class="sxs-lookup"><span data-stu-id="7bc37-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a><span data-ttu-id="7bc37-122">Configurer votre hub de notification pour les notifications Push iOS</span><span class="sxs-lookup"><span data-stu-id="7bc37-122">Configure your Notification Hub for iOS push notifications</span></span>
<span data-ttu-id="7bc37-123">Cette section présente la création d’un concentrateur de notification et de configuration de l’authentification avec APNS à l’aide de hello **.p12** : certificat push que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="7bc37-123">This section walks you through creating a new notification hub and configuring authentication with APNS using hello **.p12** push certificate that you created.</span></span> <span data-ttu-id="7bc37-124">Si vous voulez toouse un concentrateur de notification que vous avez déjà créé, vous pouvez ignorer toostep 5.</span><span class="sxs-lookup"><span data-stu-id="7bc37-124">If you want toouse a notification hub that you have already created, you can skip toostep 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p><span data-ttu-id="7bc37-125">Cliquez sur hello <b>Notification Services</b> bouton Bonjour <b>paramètres</b> panneau, puis sélectionnez <b>Apple (APN)</b>.</span><span class="sxs-lookup"><span data-stu-id="7bc37-125">Click hello <b>Notification Services</b> button in hello <b>Settings</b> blade, then select <b>Apple (APNS)</b>.</span></span> <span data-ttu-id="7bc37-126">Cliquez sur <b>télécharger un certificat</b> et sélectionnez hello <b>.p12</b> que vous avez exporté précédemment.</span><span class="sxs-lookup"><span data-stu-id="7bc37-126">Click on <b>Upload Certificate</b> and select hello <b>.p12</b> file that you exported earlier.</span></span> <span data-ttu-id="7bc37-127">Assurez-vous que vous spécifiez également un mot de passe correct hello.</span><span class="sxs-lookup"><span data-stu-id="7bc37-127">Make sure you also specify hello correct password.</span></span></p>

<p><span data-ttu-id="7bc37-128">Assurez-vous que tooselect <b>Sandbox</b> mode car il s’agit pour le développement.</span><span class="sxs-lookup"><span data-stu-id="7bc37-128">Make sure tooselect <b>Sandbox</b> mode since this is for development.</span></span> <span data-ttu-id="7bc37-129">Utilisez uniquement hello <b>Production</b> si vous souhaitez que toousers de notifications push toosend qui ont acheté votre application à partir du magasin de hello.</span><span class="sxs-lookup"><span data-stu-id="7bc37-129">Only use hello <b>Production</b> if you want toosend push notifications toousers who purchased your app from hello store.</span></span></p>
</li>
</ol>
<span data-ttu-id="7bc37-130">&emsp;&emsp;&emsp;&emsp;![Configurer APNS dans le portail Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span><span class="sxs-lookup"><span data-stu-id="7bc37-130">&emsp;&emsp;&emsp;&emsp;![Configure APNS in Azure Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span></span>

&emsp;&emsp;&emsp;&emsp;![Configurer la certification APNS dans le portail Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

<span data-ttu-id="7bc37-132">Votre concentrateur de notification est maintenant configuré toowork avec APNS, et vous avez tooregister de chaînes de connexion hello votre application et envoyez des notifications push.</span><span class="sxs-lookup"><span data-stu-id="7bc37-132">Your notification hub is now configured toowork with APNS, and you have hello connection strings tooregister your app and send push notifications.</span></span>

## <a name="connect-your-ios-app-toonotification-hubs"></a><span data-ttu-id="7bc37-133">Se connecter à votre tooNotification d’application iOS concentrateurs</span><span class="sxs-lookup"><span data-stu-id="7bc37-133">Connect your iOS app tooNotification Hubs</span></span>
1. <span data-ttu-id="7bc37-134">Dans Xcode, créez un projet iOS, puis sélectionnez hello **Application vue unique** modèle.</span><span class="sxs-lookup"><span data-stu-id="7bc37-134">In Xcode, create a new iOS project and select hello **Single View Application** template.</span></span>
   
    ![Xcode - Application à vue unique][8]
    
2. <span data-ttu-id="7bc37-136">Lors de la définition des options de hello pour votre nouveau projet, assurez-vous que toouse hello même **Product Name** et **identifiant d’organisation** que vous avez utilisé lorsque vous définissez précédemment des ID d’offre groupée hello sur hello Apple Developer portail.</span><span class="sxs-lookup"><span data-stu-id="7bc37-136">When setting hello options for your new project, make sure toouse hello same **Product Name** and **Organization Identifier** that you used when you previously set hello bundle ID on hello Apple Developer portal.</span></span>
   
    ![Xcode - options de projet][11]
    
3. <span data-ttu-id="7bc37-138">Sous **cibles**, cliquez sur le nom de votre projet hello **paramètres de génération** onglet et développez **identité de signature de Code**, puis sous **déboguer**, définir votre identité de signature de code.</span><span class="sxs-lookup"><span data-stu-id="7bc37-138">Under **Targets**, click your project name, click hello **Build Settings** tab and expand **Code Signing Identity**, and then under **Debug**, set your code-signing identity.</span></span> <span data-ttu-id="7bc37-139">Activer/désactiver **niveaux** de **base** trop**tous les**et définissez **profil de préparation** toohello configuration du profil que vous avez créé précédemment .</span><span class="sxs-lookup"><span data-stu-id="7bc37-139">Toggle **Levels** from **Basic** too**All**, and set **Provisioning Profile** toohello provisioning profile that you created previously.</span></span>
   
    <span data-ttu-id="7bc37-140">Si vous ne voyez pas hello nouvelle configuration du profil que vous avez créé dans Xcode, essayez d’actualiser les profils hello pour votre identité de signature.</span><span class="sxs-lookup"><span data-stu-id="7bc37-140">If you don't see hello new provisioning profile that you created in Xcode, try refreshing hello profiles for your signing identity.</span></span> <span data-ttu-id="7bc37-141">Cliquez sur **Xcode** hello barre de menus, cliquez sur **préférences**, cliquez sur hello **compte** , cliquez sur hello **afficher les détails** , sur votre identité de signature, puis cliquez sur le bouton d’actualisation hello dans le coin inférieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="7bc37-141">Click **Xcode** on hello menu bar, click **Preferences**, click hello **Account** tab, click hello **View Details** button, click your signing identity, and then click hello refresh button in hello bottom-right corner.</span></span>
   
    ![Xcode - profil d’approvisionnement][9]
4. <span data-ttu-id="7bc37-143">Télécharger hello [Services mobiles iOS SDK version 1.2.4] et décompressez les fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="7bc37-143">Download hello [Mobile Services iOS SDK version 1.2.4] and unzip hello file.</span></span> <span data-ttu-id="7bc37-144">Dans Xcode, avec le bouton droit de votre projet, puis cliquez sur hello **Ajout de fichiers à** hello de tooadd option **WindowsAzureMessaging.framework** projet Xcode de tooyour dossier.</span><span class="sxs-lookup"><span data-stu-id="7bc37-144">In Xcode, right-click your project and click hello **Add Files to** option tooadd hello **WindowsAzureMessaging.framework** folder tooyour Xcode project.</span></span> <span data-ttu-id="7bc37-145">Sélectionnez **Copy items if needed**, puis cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="7bc37-145">Select **Copy items if needed**, and then click **Add**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7bc37-146">concentrateurs de notification Hello SDK ne prend pas en charge bitcode sur Xcode 7.</span><span class="sxs-lookup"><span data-stu-id="7bc37-146">hello notification hubs SDK does not currently support bitcode on Xcode 7.</span></span>  <span data-ttu-id="7bc37-147">Vous devez définir **Bitcode d’activer** trop**non** Bonjour **Options de Build** pour votre projet.</span><span class="sxs-lookup"><span data-stu-id="7bc37-147">You must set **Enable Bitcode** too**No** in hello **Build Options** for your project.</span></span>
   > 
   > 
   
    ![Décompresser le SDK Azure][10]
5. <span data-ttu-id="7bc37-149">Ajouter un en-tête fichier tooyour projet nommé `HubInfo.h`.</span><span class="sxs-lookup"><span data-stu-id="7bc37-149">Add a new header file tooyour project named `HubInfo.h`.</span></span> <span data-ttu-id="7bc37-150">Ce fichier conserve les constantes hello pour votre concentrateur de notification.</span><span class="sxs-lookup"><span data-stu-id="7bc37-150">This file will hold hello constants for your notification hub.</span></span>  <span data-ttu-id="7bc37-151">Ajouter hello suivant des définitions et de remplacer la réservation de littéral de chaîne hello avec votre *nom de hub* et hello *DefaultListenSharedAccessSignature* que vous avez notée précédemment.</span><span class="sxs-lookup"><span data-stu-id="7bc37-151">Add hello following definitions and replace hello string literal placeholders with your *hub name* and hello *DefaultListenSharedAccessSignature* that you noted earlier.</span></span>
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter hello name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. <span data-ttu-id="7bc37-152">Ouvrez votre `AppDelegate.h` fichier ajouter hello suit les directives d’importation :</span><span class="sxs-lookup"><span data-stu-id="7bc37-152">Open your `AppDelegate.h` file add hello following import directives:</span></span>
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. <span data-ttu-id="7bc37-153">Dans votre `AppDelegate.m file`, ajouter hello suivant code Bonjour `didFinishLaunchingWithOptions` méthode selon votre version d’iOS.</span><span class="sxs-lookup"><span data-stu-id="7bc37-153">In your `AppDelegate.m file`, add hello following code in hello `didFinishLaunchingWithOptions` method based on your version of iOS.</span></span> <span data-ttu-id="7bc37-154">Ce code enregistre le handle de votre appareil avec APNs :</span><span class="sxs-lookup"><span data-stu-id="7bc37-154">This code registers your device handle with APNs:</span></span>
   
    <span data-ttu-id="7bc37-155">Pour iOS 8 :</span><span class="sxs-lookup"><span data-stu-id="7bc37-155">For iOS 8:</span></span>
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    <span data-ttu-id="7bc37-156">Pour too8 de précédentes versions iOS :</span><span class="sxs-lookup"><span data-stu-id="7bc37-156">For iOS versions prior too8:</span></span>
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. <span data-ttu-id="7bc37-157">Dans hello du même fichier, ajouter des méthodes suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="7bc37-157">In hello same file, add hello following methods.</span></span> <span data-ttu-id="7bc37-158">Ce code connecte toohello hub de notification à l’aide des informations de connexion hello spécifié dans HubInfo.h.</span><span class="sxs-lookup"><span data-stu-id="7bc37-158">This code connects toohello notification hub using hello connection information you specified in HubInfo.h.</span></span> <span data-ttu-id="7bc37-159">Il fournit ensuite une hub de notification de jeton toohello hello appareil afin que hello hub de notification peut envoyer des notifications :</span><span class="sxs-lookup"><span data-stu-id="7bc37-159">It then gives hello device token toohello notification hub so that hello notification hub can send notifications:</span></span>
   
        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken {
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:HUBLISTENACCESS
                                        notificationHubPath:HUBNAME];
   
            [hub registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError* error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
                else {
                    [self MessageBox:@"Registration Status" message:@"Registered"];
                }
            }];
        }
   
        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }
9. <span data-ttu-id="7bc37-160">Dans l’hello du même fichier, ajoutez hello suivant de méthode toodisplay un **UIAlert** si la notification de hello est reçue lors de l’application hello est active :</span><span class="sxs-lookup"><span data-stu-id="7bc37-160">In hello same file, add hello following method toodisplay a **UIAlert** if hello notification is received while hello app is active:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. <span data-ttu-id="7bc37-161">Générez et exécutez l’application hello sur votre tooverify appareil qu’il n’y a aucun échec.</span><span class="sxs-lookup"><span data-stu-id="7bc37-161">Build and run hello app on your device tooverify that there are no failures.</span></span>

## <a name="send-test-push-notifications"></a><span data-ttu-id="7bc37-162">Envoi de notifications Push de test</span><span class="sxs-lookup"><span data-stu-id="7bc37-162">Send test push notifications</span></span>
<span data-ttu-id="7bc37-163">Vous pouvez tester la réception de notifications dans votre application en envoyant des notifications push dans hello [Azure Portal] via hello **dépannage** section dans le panneau de concentrateur hello (utilisez hello *d’envoiTest* option).</span><span class="sxs-lookup"><span data-stu-id="7bc37-163">You can test receiving notifications in your app by sending push notifications in hello [Azure Portal] via hello **Troubleshooting** section in hello hub blade (use hello *Test Send* option).</span></span>

![Portail Azure - Test d’envoi][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-hello-app"></a><span data-ttu-id="7bc37-165">(Facultatif) Envoyer des notifications push à partir de l’application hello</span><span class="sxs-lookup"><span data-stu-id="7bc37-165">(Optional) Send push notifications from hello app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7bc37-166">Cet exemple montre comment envoyer des notifications à partir de l’application cliente de hello est fourni uniquement à des fins pédagogiques.</span><span class="sxs-lookup"><span data-stu-id="7bc37-166">This example of sending notifications from hello client app is provided for learning purposes only.</span></span> <span data-ttu-id="7bc37-167">Étant donné que vous devrez hello `DefaultFullSharedAccessSignature` toobe présent sur l’application cliente de hello, il expose les risques de toohello de concentrateur de notification qu’un utilisateur peut obtenir les notifications d’accès non autorisé de toosend tooyour clients.</span><span class="sxs-lookup"><span data-stu-id="7bc37-167">Since this will require hello `DefaultFullSharedAccessSignature` toobe present on hello client app, it exposes your notification hub toohello risk that a user may gain access toosend unauthorized notifications tooyour clients.</span></span>
> 
> 

<span data-ttu-id="7bc37-168">Si vous souhaitez toosend notifications push au sein d’une application, cette section fournit un exemple de procédure toodo à l’aide de cette hello interface REST.</span><span class="sxs-lookup"><span data-stu-id="7bc37-168">If you want toosend push notifications from within an app, this section provides an example of how toodo this using hello REST interface.</span></span>

1. <span data-ttu-id="7bc37-169">Dans Xcode, ouvrez `Main.storyboard` et ajoutez hello suivant des composants d’interface utilisateur à partir de hello objet bibliothèque tooallow hello utilisateur toosend des notifications push dans l’application hello :</span><span class="sxs-lookup"><span data-stu-id="7bc37-169">In Xcode, open `Main.storyboard` and add hello following UI components from hello object library tooallow hello user toosend push notifications in hello app:</span></span>
   
   * <span data-ttu-id="7bc37-170">Une étiquette sans texte d’étiquette.</span><span class="sxs-lookup"><span data-stu-id="7bc37-170">A label with no label text.</span></span> <span data-ttu-id="7bc37-171">Il s’agit des erreurs tooreport utilisé lors de l’envoi des notifications.</span><span class="sxs-lookup"><span data-stu-id="7bc37-171">It will be used tooreport errors in sending notifications.</span></span> <span data-ttu-id="7bc37-172">Hello **lignes** propriété doit être définie trop**0** afin qu’il se redimensionne automatiquement toohello la droite et les marges gauche et haut hello de vue de hello.</span><span class="sxs-lookup"><span data-stu-id="7bc37-172">hello **Lines** property should be set too**0** so that it will automatically size constrained toohello right and left margins and hello top of hello view.</span></span>
   * <span data-ttu-id="7bc37-173">Un champ de texte avec **espace réservé** texte défini trop**entrer un Message de Notification**.</span><span class="sxs-lookup"><span data-stu-id="7bc37-173">A text field with **Placeholder** text set too**Enter Notification Message**.</span></span> <span data-ttu-id="7bc37-174">Limiter le champ hello juste en dessous d’étiquette hello comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7bc37-174">Constrain hello field just below hello label as shown below.</span></span> <span data-ttu-id="7bc37-175">Définissez hello View Controller que le délégué de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="7bc37-175">Set hello View Controller as hello outlet delegate.</span></span>
   * <span data-ttu-id="7bc37-176">Un bouton intitulé **envoyer une Notification** contraint juste en dessous de champ de texte hello et dans le centre de horizontal hello.</span><span class="sxs-lookup"><span data-stu-id="7bc37-176">A button titled **Send Notification** constrained just below hello text field and in hello horizontal center.</span></span>
     
     <span data-ttu-id="7bc37-177">affichage de Hello doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="7bc37-177">hello view should look as follows:</span></span>
     
     ![Concepteur Xcode][32]
2. <span data-ttu-id="7bc37-179">[Ajoutez des prises de courant](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) de champ d’étiquette et le texte hello connectée à votre affichage et mettre à jour votre `interface` définition toosupport `UITextFieldDelegate` et `NSXMLParserDelegate`.</span><span class="sxs-lookup"><span data-stu-id="7bc37-179">[Add outlets](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) for hello label and text field connected your view, and update your `interface` definition toosupport `UITextFieldDelegate` and `NSXMLParserDelegate`.</span></span> <span data-ttu-id="7bc37-180">Ajoutez les trois déclarations de propriété hello ci-dessous de prise en charge toohelp appelant hello API REST et analyse de la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="7bc37-180">Add hello three property declarations shown below toohelp support calling hello REST API and parsing hello response.</span></span>
   
    <span data-ttu-id="7bc37-181">Votre fichier ViewController.h doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="7bc37-181">Your ViewController.h file should look as follows:</span></span>
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected tooyour UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. <span data-ttu-id="7bc37-182">Ouvrez `HubInfo.h` et ajoutez hello suivant des constantes qui seront utilisés pour l’envoi de hub de notifications tooyour.</span><span class="sxs-lookup"><span data-stu-id="7bc37-182">Open `HubInfo.h` and add hello following constants which will be used for sending notifications tooyour hub.</span></span> <span data-ttu-id="7bc37-183">Remplacez le littéral de chaîne espace réservé hello avec votre véritable *DefaultFullSharedAccessSignature* chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="7bc37-183">Replace hello placeholder string literal with your actual *DefaultFullSharedAccessSignature* connection string.</span></span>
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. <span data-ttu-id="7bc37-184">Ajoutez hello suivant `#import` instructions tooyour `ViewController.h` fichier.</span><span class="sxs-lookup"><span data-stu-id="7bc37-184">Add hello following `#import` statements tooyour `ViewController.h` file.</span></span>
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. <span data-ttu-id="7bc37-185">Dans `ViewController.m` ajouter hello après l’implémentation d’interface toohello code.</span><span class="sxs-lookup"><span data-stu-id="7bc37-185">In `ViewController.m` add hello following code toohello interface implementation.</span></span> <span data-ttu-id="7bc37-186">Ce code analysera la chaîne de connexion *DefaultFullSharedAccessSignature* .</span><span class="sxs-lookup"><span data-stu-id="7bc37-186">This code will parse your *DefaultFullSharedAccessSignature* connection string.</span></span> <span data-ttu-id="7bc37-187">Comme mentionné dans hello [référence d’API REST](http://msdn.microsoft.com/library/azure/dn495627.aspx), ces informations analysées seront toogenerate utilisé un jeton SAP pour hello **autorisation** en-tête de demande.</span><span class="sxs-lookup"><span data-stu-id="7bc37-187">As mentioned in hello [REST API reference](http://msdn.microsoft.com/library/azure/dn495627.aspx), this parsed information will be used toogenerate a SaS token for hello **Authorization** request header.</span></span>
   
        NSString *HubEndpoint;
        NSString *HubSasKeyName;
        NSString *HubSasKeyValue;
   
        -(void)ParseConnectionString
        {
            NSArray *parts = [HUBFULLACCESS componentsSeparatedByString:@";"];
            NSString *part;
   
            if ([parts count] != 3)
            {
                NSException* parseException = [NSException exceptionWithName:@"ConnectionStringParseException"
                    reason:@"Invalid full shared access connection string" userInfo:nil];
   
                @throw parseException;
            }
   
            for (part in parts)
            {
                if ([part hasPrefix:@"Endpoint"])
                {
                    HubEndpoint = [NSString stringWithFormat:@"https%@",[part substringFromIndex:11]];
                }
                else if ([part hasPrefix:@"SharedAccessKeyName"])
                {
                    HubSasKeyName = [part substringFromIndex:20];
                }
                else if ([part hasPrefix:@"SharedAccessKey"])
                {
                    HubSasKeyValue = [part substringFromIndex:16];
                }
            }
        }
6. <span data-ttu-id="7bc37-188">Dans `ViewController.m`, mise à jour hello `viewDidLoad` chaîne de connexion méthode tooparse hello lors de la charge de la vue de hello.</span><span class="sxs-lookup"><span data-stu-id="7bc37-188">In `ViewController.m`, update hello `viewDidLoad` method tooparse hello connection string when hello view loads.</span></span> <span data-ttu-id="7bc37-189">Également ajouter des méthodes d’utilitaire hello, illustrés ci-dessous, l’implémentation d’interface toohello.</span><span class="sxs-lookup"><span data-stu-id="7bc37-189">Also add hello utility methods, shown below, toohello interface implementation.</span></span>  

        - (void)viewDidLoad
        {
            [super viewDidLoad];
            [self ParseConnectionString];
            [_notificationMessage setDelegate:self];
        }

        -(NSString *)CF_URLEncodedString:(NSString *)inputString
        {
           return (__bridge NSString *)CFURLCreateStringByAddingPercentEscapes(NULL, (CFStringRef)inputString,
                NULL, (CFStringRef)@"!*'();:@&=+$,/?%#[]", kCFStringEncodingUTF8);
        }

        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }





1. <span data-ttu-id="7bc37-190">Dans `ViewController.m`, ajouter hello suivant code toohello interface implémentation toogenerate hello SaS jeton d’autorisation qui sera fournie dans hello **autorisation** en-tête, comme indiqué dans hello [API REST Référence](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="7bc37-190">In `ViewController.m`, add hello following code toohello interface implementation toogenerate hello SaS authorization token that will be provided in hello **Authorization** header, as mentioned in hello [REST API Reference](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span></span>
   
        -(NSString*) generateSasToken:(NSString*)uri
        {
            NSString *targetUri;
            NSString* utf8LowercasedUri = NULL;
            NSString *signature = NULL;
            NSString *token = NULL;
   
            @try
            {
                // Add expiration
                uri = [uri lowercaseString];
                utf8LowercasedUri = [self CF_URLEncodedString:uri];
                targetUri = [utf8LowercasedUri lowercaseString];
                NSTimeInterval expiresOnDate = [[NSDate date] timeIntervalSince1970];
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60;
                UInt64 expires = trunc(expiresOnDate);
                NSString* toSign = [NSString stringWithFormat:@"%@\n%qu", targetUri, expires];
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                const char *cKey  = [HubSasKeyValue cStringUsingEncoding:NSUTF8StringEncoding];
                const char *cData = [toSign cStringUsingEncoding:NSUTF8StringEncoding];
                unsigned char cHMAC[CC_SHA256_DIGEST_LENGTH];
                CCHmac(kCCHmacAlgSHA256, cKey, strlen(cKey), cData, strlen(cData), cHMAC);
                NSData *rawHmac = [[NSData alloc] initWithBytes:cHMAC length:sizeof(cHMAC)];
                signature = [self CF_URLEncodedString:[rawHmac base64EncodedStringWithOptions:0]];
   
                // Construct authorization token string
                token = [NSString stringWithFormat:@"SharedAccessSignature sig=%@&se=%qu&skn=%@&sr=%@",
                    signature, expires, HubSasKeyName, targetUri];
            }
            @catch (NSException *exception)
            {
                [self MessageBox:@"Exception Generating SaS Token" message:[exception reason]];
            }
            @finally
            {
                if (utf8LowercasedUri != NULL)
                    CFRelease((CFStringRef)utf8LowercasedUri);
                if (signature != NULL)
                CFRelease((CFStringRef)signature);
            }
   
            return token;
        }
2. <span data-ttu-id="7bc37-191">CTRL + glisser à partir de hello **envoyer une Notification** bouton trop`ViewController.m` tooadd une action nommée **SendNotificationMessage** pour hello **Touch bas** événement.</span><span class="sxs-lookup"><span data-stu-id="7bc37-191">Ctrl+drag from hello **Send Notification** button too`ViewController.m` tooadd an action named **SendNotificationMessage** for hello **Touch Down** event.</span></span> <span data-ttu-id="7bc37-192">Mettre à jour méthode hello suivant code toosend hello notification à l’aide des API REST de hello.</span><span class="sxs-lookup"><span data-stu-id="7bc37-192">Update method with hello following code toosend hello notification using hello REST API.</span></span>
   
        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";
            [self SendNotificationRESTAPI];
        }
   
        - (void)SendNotificationRESTAPI
        {
            NSURLSession* session = [NSURLSession
                             sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                             delegate:nil delegateQueue:nil];
   
            // Apple Notification format of hello notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct hello message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate hello token toobe used in hello authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello APNs notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (error || (httpResponse.statusCode != 200 && httpResponse.statusCode != 201))
                {
                    NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                }
                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                       [xmlParser parse];
                }
            }];
            [dataTask resume];
        }
3. <span data-ttu-id="7bc37-193">Dans `ViewController.m`, ajoutez hello suivant toosupport de méthode délégué fermeture clavier hello pour le champ de texte hello.</span><span class="sxs-lookup"><span data-stu-id="7bc37-193">In `ViewController.m`, add hello following delegate method toosupport closing hello keyboard for hello text field.</span></span> <span data-ttu-id="7bc37-194">CTRL + glisser à partir de hello texte champ toohello View Controller icône hello de concepteur tooset interface hello afficher contrôleur que le délégué de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="7bc37-194">Ctrl+drag from hello text field toohello View Controller icon in hello interface designer tooset hello view controller as hello outlet delegate.</span></span>
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. <span data-ttu-id="7bc37-195">Dans `ViewController.m`, ajouter suivant de hello déléguer réponse hello analyse de méthodes toosupport à l’aide de `NSXMLParser`.</span><span class="sxs-lookup"><span data-stu-id="7bc37-195">In `ViewController.m`, add hello following delegate methods toosupport parsing hello response by using `NSXMLParser`.</span></span>
   
       //===[ Implement NSXMLParserDelegate methods ]===
   
       -(void)parserDidStartDocument:(NSXMLParser *)parser
       {
           self.statusResult = @"";
       }
   
       -(void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName
           namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName
           attributes:(NSDictionary *)attributeDict
       {
           NSString * element = [elementName lowercaseString];
           NSLog(@"*** New element parsed : %@ ***",element);
   
           if ([element isEqualToString:@"code"] | [element isEqualToString:@"detail"])
           {
               self.currentElement = element;
           }
       }
   
       -(void) parser:(NSXMLParser *)parser foundCharacters:(NSString *)parsedString
       {
           self.statusResult = [self.statusResult stringByAppendingString:
               [NSString stringWithFormat:@"%@ : %@\n", self.currentElement, parsedString]];
       }
   
       -(void)parserDidEndDocument:(NSXMLParser *)parser
       {
           // Set hello status label text on hello UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. <span data-ttu-id="7bc37-196">Générez le projet de hello et vérifiez qu’il n’y a aucune erreur.</span><span class="sxs-lookup"><span data-stu-id="7bc37-196">Build hello project and verify that there are no errors.</span></span>

> [!NOTE]
> <span data-ttu-id="7bc37-197">Si vous rencontrez une erreur de build dans Xcode7 sur la prise en charge bitcode, vous devez modifier hello **paramètres de génération** > **Bitcode activer (ENABLE_BITCODE)** trop**non** dans Xcode.</span><span class="sxs-lookup"><span data-stu-id="7bc37-197">If you encounter a build error in Xcode7 about bitcode support, you should change hello **Build Settings** > **Enable Bitcode (ENABLE_BITCODE)** too**NO** in Xcode.</span></span> <span data-ttu-id="7bc37-198">Hello SDK de concentrateurs de Notification ne prend pas en charge bitcode.</span><span class="sxs-lookup"><span data-stu-id="7bc37-198">hello Notification Hubs SDK does not currently support bitcode.</span></span> 
> 
> 

<span data-ttu-id="7bc37-199">Vous pouvez trouver toutes les charges utiles de notifications possibles hello Bonjour Apple [Local et le Guide de programmation de Notification Push].</span><span class="sxs-lookup"><span data-stu-id="7bc37-199">You can find all hello possible notification payloads in hello Apple [Local and Push Notification Programming Guide].</span></span>

## <a name="checking-if-your-app-can-receive-push-notifications"></a><span data-ttu-id="7bc37-200">Vérifier si votre application peut recevoir des notifications Push</span><span class="sxs-lookup"><span data-stu-id="7bc37-200">Checking if your app can receive push notifications</span></span>
<span data-ttu-id="7bc37-201">des notifications push tootest sur iOS, vous devez déployer le périphérique d’e/s physiques tooa hello application.</span><span class="sxs-lookup"><span data-stu-id="7bc37-201">tootest push notifications on iOS, you must deploy hello app tooa physical iOS device.</span></span> <span data-ttu-id="7bc37-202">Impossible d’envoyer des notifications de push Apple à l’aide de hello, iOS Simulator.</span><span class="sxs-lookup"><span data-stu-id="7bc37-202">You cannot send Apple push notifications by using hello iOS Simulator.</span></span>

1. <span data-ttu-id="7bc37-203">Exécutez l’application hello et vérifiez que l’inscription réussit, puis appuyez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7bc37-203">Run hello app and verify that registration succeeds, and then press **OK**.</span></span>
   
    ![Test d’inscription de notifications Push pour applications iOS][33]
2. <span data-ttu-id="7bc37-205">Vous pouvez envoyer une notification push de test à partir de hello [Azure Portal], comme décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="7bc37-205">You can send a test push notification from hello [Azure Portal], as described above.</span></span> <span data-ttu-id="7bc37-206">Si vous avez ajouté le code pour l’envoi de notifications push dans l’application hello, touchez tooenter de champ de texte hello à l’intérieur d’un message de notification.</span><span class="sxs-lookup"><span data-stu-id="7bc37-206">If you added code for sending push notifications in hello app, touch inside hello text field tooenter a notification message.</span></span> <span data-ttu-id="7bc37-207">Appuyez sur hello **envoyer** bouton sur le clavier de hello ou hello **envoyer une Notification** bouton dans le message de notification hello vue toosend hello.</span><span class="sxs-lookup"><span data-stu-id="7bc37-207">Then press hello **Send** button on hello keyboard or hello **Send Notification** button in hello view toosend hello notification message.</span></span>
   
    ![Test d’envoi de notifications Push pour applications iOS][34]
3. <span data-ttu-id="7bc37-209">Hello notifications sont envoyées tooall périphériques inscrit tooreceive notifications hello hello Hub de Notification particulier.</span><span class="sxs-lookup"><span data-stu-id="7bc37-209">hello push notification is sent tooall devices that are registered tooreceive hello notifications from hello particular Notification Hub.</span></span>
   
    ![Test de réception de notifications Push pour applications iOS][35]

## <a name="next-steps"></a><span data-ttu-id="7bc37-211">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7bc37-211">Next steps</span></span>
<span data-ttu-id="7bc37-212">Dans cet exemple simple, vous diffusées tooall de notifications push à vos appareils iOS inscrits.</span><span class="sxs-lookup"><span data-stu-id="7bc37-212">In this simple example, you broadcasted push notifications tooall your registered iOS devices.</span></span> <span data-ttu-id="7bc37-213">Nous vous suggérons de franchir une étape supplémentaire dans votre apprentissage que vous passez toohello [Azure Notification Hubs d’avertir les utilisateurs pour iOS avec le serveur principal .NET] didacticiel qui vous guidera dans la création d’un push de toosend principal des notifications à l’aide de balises.</span><span class="sxs-lookup"><span data-stu-id="7bc37-213">We suggest as a next step in your learning that you proceed toohello [Azure Notification Hubs Notify Users for iOS with .NET backend] tutorial, which will walk you through creating a backend toosend push notifications using tags.</span></span> 

<span data-ttu-id="7bc37-214">Si vous souhaitez toosegment vos utilisateurs en groupes d’intérêt, vous pouvez également déplacer sur toohello [toosend utiliser Notification Hubs actualités] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="7bc37-214">If you want toosegment your users by interest groups, you can additionally move on toohello [Use Notification Hubs toosend breaking news] tutorial.</span></span> 

<span data-ttu-id="7bc37-215">Pour obtenir des informations générales sur Notification Hubs, consultez [Recommandations relatives à Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="7bc37-215">For general information about Notification Hubs, see [Notification Hubs Guidance].</span></span>

<!-- Images. -->

[6]: ./media/notification-hubs-ios-get-started/notification-hubs-configure-ios.png
[8]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app.png
[9]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app2.png
[10]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app3.png
[11]: ./media/notification-hubs-ios-get-started/notification-hubs-xcode-product-name.png

[30]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png

[31]: ./media/notification-hubs-ios-get-started/notification-hubs-ios-ui.png
[32]: ./media/notification-hubs-ios-get-started/notification-hubs-storyboard-view.png
[33]: ./media/notification-hubs-ios-get-started/notification-hubs-test1.png
[34]: ./media/notification-hubs-ios-get-started/notification-hubs-test2.png
[35]: ./media/notification-hubs-ios-get-started/notification-hubs-test3.png



<!-- URLs. -->
[Services mobiles iOS SDK version 1.2.4]: http://aka.ms/kymw2g
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
[Recommandations relatives à Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
[Azure Notification Hubs d’avertir les utilisateurs pour iOS avec le serveur principal .NET]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md
[toosend utiliser Notification Hubs actualités]: notification-hubs-ios-xplat-segmented-apns-push-notification.md

[Local et le Guide de programmation de Notification Push]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1
[Azure Portal]: https://portal.azure.com
