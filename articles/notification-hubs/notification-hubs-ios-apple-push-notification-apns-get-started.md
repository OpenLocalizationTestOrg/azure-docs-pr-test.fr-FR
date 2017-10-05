---
title: Envoi de notifications Push vers iOS avec Azure Notification Hubs | Microsoft Docs
description: "Dans ce didacticiel, vous découvrirez comment utiliser Azure Notification Hubs pour envoyer des notifications Push à une application iOS."
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
ms.openlocfilehash: ab0777f859e80afcd61e371056b44d018c7b7ab9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-to-ios-with-azure-notification-hubs"></a><span data-ttu-id="470e8-104">Envoi de notifications Push vers iOS avec Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="470e8-104">Sending push notifications to iOS with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="470e8-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="470e8-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="470e8-106">Pour suivre ce didacticiel, vous avez besoin d'un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="470e8-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="470e8-107">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="470e8-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="470e8-108">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="470e8-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="470e8-109">Ce didacticiel vous montre comment utiliser Azure Notification Hubs pour envoyer des notifications Push vers une application iOS.</span><span class="sxs-lookup"><span data-stu-id="470e8-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to an iOS application.</span></span> <span data-ttu-id="470e8-110">Vous allez créer une application iOS vide qui reçoit des notifications push à l’aide du [service de notification Push Apple](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html)(APNs, Apple Push Notification service).</span><span class="sxs-lookup"><span data-stu-id="470e8-110">You'll create a blank iOS app that receives push notifications by using the [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span></span> 

<span data-ttu-id="470e8-111">Une fois l’opération terminée, vous pouvez utiliser votre hub de notification pour diffuser des notifications Push sur tous les appareils exécutant votre application.</span><span class="sxs-lookup"><span data-stu-id="470e8-111">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="470e8-112">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="470e8-112">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="470e8-113">Le code complet de ce didacticiel est disponible [sur GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="470e8-113">The completed code for this tutorial can be found [on GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="470e8-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="470e8-114">Prerequisites</span></span>
<span data-ttu-id="470e8-115">Ce didacticiel requiert les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="470e8-115">This tutorial requires the following:</span></span>

* <span data-ttu-id="470e8-116">[version 1.2.4 du kit de développement logiciel (SDK) Mobile Services iOS]</span><span class="sxs-lookup"><span data-stu-id="470e8-116">[Mobile Services iOS SDK version 1.2.4]</span></span>
* <span data-ttu-id="470e8-117">Version la plus récente de [Xcode]</span><span class="sxs-lookup"><span data-stu-id="470e8-117">Latest version of [Xcode]</span></span>
* <span data-ttu-id="470e8-118">Un appareil compatible iOS 8 (ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="470e8-118">An iOS 8 (or later version)-capable device</span></span>
* <span data-ttu-id="470e8-119">[programme pour développeurs Apple](https://developer.apple.com/programs/) </span><span class="sxs-lookup"><span data-stu-id="470e8-119">[Apple Developer Program](https://developer.apple.com/programs/) membership.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="470e8-120">En raison des exigences de configuration requise pour les notifications Push, vous devez déployer et tester les notifications Push sur un appareil iOS physique (iPhone ou iPad) au lieu du simulateur iOS.</span><span class="sxs-lookup"><span data-stu-id="470e8-120">Because of configuration requirements for push notifications, you must deploy and test push notifications on a physical iOS device (iPhone or iPad) instead of the iOS Simulator.</span></span>
  > 
  > 

<span data-ttu-id="470e8-121">Vous devez terminer ce didacticiel avant de pouvoir suivre tous les autres didacticiels Notification Hubs pour les applications iOS.</span><span class="sxs-lookup"><span data-stu-id="470e8-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a><span data-ttu-id="470e8-122">Configurer votre hub de notification pour les notifications Push iOS</span><span class="sxs-lookup"><span data-stu-id="470e8-122">Configure your Notification Hub for iOS push notifications</span></span>
<span data-ttu-id="470e8-123">Cette section vous guide dans la création d’un hub de notification et la configuration APNS à l’aide du certificat Push **.p12** que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="470e8-123">This section walks you through creating a new notification hub and configuring authentication with APNS using the **.p12** push certificate that you created.</span></span> <span data-ttu-id="470e8-124">Si vous souhaitez utiliser un hub de notification que vous avez déjà créé, vous pouvez passer directement à l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="470e8-124">If you want to use a notification hub that you have already created, you can skip to step 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p><span data-ttu-id="470e8-125">Cliquez sur le bouton <b>Notification Services</b> situé dans le panneau <b>Paramètres</b>, puis sélectionnez <b>Apple (APNS)</b>.</span><span class="sxs-lookup"><span data-stu-id="470e8-125">Click the <b>Notification Services</b> button in the <b>Settings</b> blade, then select <b>Apple (APNS)</b>.</span></span> <span data-ttu-id="470e8-126">Cliquez sur <b>Télécharger le certificat</b> et sélectionnez le fichier <b>.p12</b> que vous avez exporté précédemment.</span><span class="sxs-lookup"><span data-stu-id="470e8-126">Click on <b>Upload Certificate</b> and select the <b>.p12</b> file that you exported earlier.</span></span> <span data-ttu-id="470e8-127">Assurez-vous que le mot de passe spécifié est correct.</span><span class="sxs-lookup"><span data-stu-id="470e8-127">Make sure you also specify the correct password.</span></span></p>

<p><span data-ttu-id="470e8-128">Comme il s’agit de développement, veillez à sélectionner le mode <b>Sandbox</b>.</span><span class="sxs-lookup"><span data-stu-id="470e8-128">Make sure to select <b>Sandbox</b> mode since this is for development.</span></span> <span data-ttu-id="470e8-129">Utilisez uniquement <b>Production</b> si vous souhaitez envoyer des notifications Push aux utilisateurs ayant acheté votre application dans Windows Store.</span><span class="sxs-lookup"><span data-stu-id="470e8-129">Only use the <b>Production</b> if you want to send push notifications to users who purchased your app from the store.</span></span></p>
</li>
</ol>
<span data-ttu-id="470e8-130">&emsp;&emsp;&emsp;&emsp;![Configurer APNS dans le portail Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span><span class="sxs-lookup"><span data-stu-id="470e8-130">&emsp;&emsp;&emsp;&emsp;![Configure APNS in Azure Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span></span>

&emsp;&emsp;&emsp;&emsp;![Configurer la certification APNS dans le portail Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

<span data-ttu-id="470e8-132">Votre hub de notification est maintenant configuré pour APNS, et vous disposez des chaînes de connexion pour inscrire votre application et envoyer des notifications Push.</span><span class="sxs-lookup"><span data-stu-id="470e8-132">Your notification hub is now configured to work with APNS, and you have the connection strings to register your app and send push notifications.</span></span>

## <a name="connect-your-ios-app-to-notification-hubs"></a><span data-ttu-id="470e8-133">Connexion de votre application iOS à Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="470e8-133">Connect your iOS app to Notification Hubs</span></span>
1. <span data-ttu-id="470e8-134">Dans Xcode, créez un projet iOS et sélectionnez le modèle **Single View Application** .</span><span class="sxs-lookup"><span data-stu-id="470e8-134">In Xcode, create a new iOS project and select the **Single View Application** template.</span></span>
   
    ![Xcode - Application à vue unique][8]
    
2. <span data-ttu-id="470e8-136">Lorsque vous définissez les options de votre nouveau projet, veillez à utiliser les mêmes **Product Name** et **Organization Identifier** que ceux utilisés lors de la définition de l’ID d’offre groupée sur le portail des développeurs Apple.</span><span class="sxs-lookup"><span data-stu-id="470e8-136">When setting the options for your new project, make sure to use the same **Product Name** and **Organization Identifier** that you used when you previously set the bundle ID on the Apple Developer portal.</span></span>
   
    ![Xcode - options de projet][11]
    
3. <span data-ttu-id="470e8-138">Sous **Targets**, cliquez sur le nom de votre projet, cliquez sur l’onglet **Build Settings** et développez **Code Signing Identity**, puis sous **Debug**, sélectionnez votre identité de signature du code.</span><span class="sxs-lookup"><span data-stu-id="470e8-138">Under **Targets**, click your project name, click the **Build Settings** tab and expand **Code Signing Identity**, and then under **Debug**, set your code-signing identity.</span></span> <span data-ttu-id="470e8-139">Basculez **Levels** de **Basic** à **All** et définissez **Provisioning Profile** sur le profil d’approvisionnement que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="470e8-139">Toggle **Levels** from **Basic** to **All**, and set **Provisioning Profile** to the provisioning profile that you created previously.</span></span>
   
    <span data-ttu-id="470e8-140">Si vous ne voyez pas le nouveau profil d’approvisionnement que vous avez créé dans Xcode, essayez d’actualiser les profils pour votre identité de signature.</span><span class="sxs-lookup"><span data-stu-id="470e8-140">If you don't see the new provisioning profile that you created in Xcode, try refreshing the profiles for your signing identity.</span></span> <span data-ttu-id="470e8-141">Cliquez sur **Xcode** dans la barre de menus, sur **Preferences**, sur l’onglet **Account**, sur le bouton **View Details**, sur votre identité de signature, puis cliquez sur le bouton d’actualisation dans le coin inférieur droit.</span><span class="sxs-lookup"><span data-stu-id="470e8-141">Click **Xcode** on the menu bar, click **Preferences**, click the **Account** tab, click the **View Details** button, click your signing identity, and then click the refresh button in the bottom-right corner.</span></span>
   
    ![Xcode - profil d’approvisionnement][9]
4. <span data-ttu-id="470e8-143">Téléchargez la [version 1.2.4 du kit de développement logiciel (SDK) Mobile Services iOS] et décompressez le fichier.</span><span class="sxs-lookup"><span data-stu-id="470e8-143">Download the [Mobile Services iOS SDK version 1.2.4] and unzip the file.</span></span> <span data-ttu-id="470e8-144">Dans Xcode, cliquez avec le bouton droit sur votre projet et sélectionnez l’option **Add Files to** pour ajouter le dossier **WindowsAzureMessaging.framework** à votre projet Xcode.</span><span class="sxs-lookup"><span data-stu-id="470e8-144">In Xcode, right-click your project and click the **Add Files to** option to add the **WindowsAzureMessaging.framework** folder to your Xcode project.</span></span> <span data-ttu-id="470e8-145">Sélectionnez **Copy items if needed**, puis cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="470e8-145">Select **Copy items if needed**, and then click **Add**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="470e8-146">Le kit de développement logiciel Notification Hubs ne prend pas en charge le bitcode sur Xcode7.</span><span class="sxs-lookup"><span data-stu-id="470e8-146">The notification hubs SDK does not currently support bitcode on Xcode 7.</span></span>  <span data-ttu-id="470e8-147">Vous devez définir **Activer le bitcode** sur **Non** dans les **Options de build** de votre projet.</span><span class="sxs-lookup"><span data-stu-id="470e8-147">You must set **Enable Bitcode** to **No** in the **Build Options** for your project.</span></span>
   > 
   > 
   
    ![Décompresser le SDK Azure][10]
5. <span data-ttu-id="470e8-149">Ajoutez un nouveau fichier d’en-tête à votre projet nommé `HubInfo.h`.</span><span class="sxs-lookup"><span data-stu-id="470e8-149">Add a new header file to your project named `HubInfo.h`.</span></span> <span data-ttu-id="470e8-150">Ce fichier contiendra les constantes de votre hub de notification.</span><span class="sxs-lookup"><span data-stu-id="470e8-150">This file will hold the constants for your notification hub.</span></span>  <span data-ttu-id="470e8-151">Ajoutez les définitions suivantes et remplacez les espaces réservés des littéraux de chaîne par le *nom de votre hub* et la chaîne *DefaultListenSharedAccessSignature* notée précédemment.</span><span class="sxs-lookup"><span data-stu-id="470e8-151">Add the following definitions and replace the string literal placeholders with your *hub name* and the *DefaultListenSharedAccessSignature* that you noted earlier.</span></span>
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter the name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. <span data-ttu-id="470e8-152">Ouvrez le fichier `AppDelegate.h` et ajoutez l’instruction d’importation suivante :</span><span class="sxs-lookup"><span data-stu-id="470e8-152">Open your `AppDelegate.h` file add the following import directives:</span></span>
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. <span data-ttu-id="470e8-153">Dans le fichier `AppDelegate.m file`, ajoutez le code suivant dans la méthode `didFinishLaunchingWithOptions` basée sur votre version d’iOS.</span><span class="sxs-lookup"><span data-stu-id="470e8-153">In your `AppDelegate.m file`, add the following code in the `didFinishLaunchingWithOptions` method based on your version of iOS.</span></span> <span data-ttu-id="470e8-154">Ce code enregistre le handle de votre appareil avec APNs :</span><span class="sxs-lookup"><span data-stu-id="470e8-154">This code registers your device handle with APNs:</span></span>
   
    <span data-ttu-id="470e8-155">Pour iOS 8 :</span><span class="sxs-lookup"><span data-stu-id="470e8-155">For iOS 8:</span></span>
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    <span data-ttu-id="470e8-156">Pour les versions d’iOS antérieures à 8 :</span><span class="sxs-lookup"><span data-stu-id="470e8-156">For iOS versions prior to 8:</span></span>
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. <span data-ttu-id="470e8-157">Dans le même fichier, ajoutez les méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="470e8-157">In the same file, add the following methods.</span></span> <span data-ttu-id="470e8-158">Ce code se connecte au hub de notification utilisant les informations de connexion que vous avez spécifiées dans HubInfo.h.</span><span class="sxs-lookup"><span data-stu-id="470e8-158">This code connects to the notification hub using the connection information you specified in HubInfo.h.</span></span> <span data-ttu-id="470e8-159">Il transmet ensuite le jeton de l’appareil au hub de notification, de sorte que le hub de notification puisse envoyer des notifications :</span><span class="sxs-lookup"><span data-stu-id="470e8-159">It then gives the device token to the notification hub so that the notification hub can send notifications:</span></span>
   
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
9. <span data-ttu-id="470e8-160">Dans le même fichier, ajoutez la méthode suivante pour afficher une **UIAlert** si la notification est reçue alors que l’application est active :</span><span class="sxs-lookup"><span data-stu-id="470e8-160">In the same file, add the following method to display a **UIAlert** if the notification is received while the app is active:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. <span data-ttu-id="470e8-161">Générez et exécutez l’application sur votre appareil pour vérifier l’absence d’échecs.</span><span class="sxs-lookup"><span data-stu-id="470e8-161">Build and run the app on your device to verify that there are no failures.</span></span>

## <a name="send-test-push-notifications"></a><span data-ttu-id="470e8-162">Envoi de notifications Push de test</span><span class="sxs-lookup"><span data-stu-id="470e8-162">Send test push notifications</span></span>
<span data-ttu-id="470e8-163">Vous pouvez tester la réception de notifications dans votre application en envoyant des notifications Push dans le [portail Azure] via la section **Dépannage** dans le panneau Hub (à l’aide de l’option *Test d’envoi* ).</span><span class="sxs-lookup"><span data-stu-id="470e8-163">You can test receiving notifications in your app by sending push notifications in the [Azure Portal] via the **Troubleshooting** section in the hub blade (use the *Test Send* option).</span></span>

![Portail Azure - Test d’envoi][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-the-app"></a><span data-ttu-id="470e8-165">(Facultatif) Envoyer des notifications Push depuis l’application</span><span class="sxs-lookup"><span data-stu-id="470e8-165">(Optional) Send push notifications from the app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="470e8-166">Cet exemple d’envoi de notifications à partir de l’application cliente est fourni à des fins d’apprentissage uniquement.</span><span class="sxs-lookup"><span data-stu-id="470e8-166">This example of sending notifications from the client app is provided for learning purposes only.</span></span> <span data-ttu-id="470e8-167">Étant donné que cette opération exige la présence de la `DefaultFullSharedAccessSignature` sur l’application cliente, cela implique le risque pour votre hub de notification qu’un utilisateur puisse y accéder pour envoyer des notifications non autorisées à vos clients.</span><span class="sxs-lookup"><span data-stu-id="470e8-167">Since this will require the `DefaultFullSharedAccessSignature` to be present on the client app, it exposes your notification hub to the risk that a user may gain access to send unauthorized notifications to your clients.</span></span>
> 
> 

<span data-ttu-id="470e8-168">Si vous souhaitez envoyer des notifications Push à partir d’une application, cette section vous explique comment procéder à l’aide de l’interface REST.</span><span class="sxs-lookup"><span data-stu-id="470e8-168">If you want to send push notifications from within an app, this section provides an example of how to do this using the REST interface.</span></span>

1. <span data-ttu-id="470e8-169">Dans Xcode, ouvrez `Main.storyboard` et ajoutez les composants d’interface utilisateur suivants à partir de la bibliothèque d’objets pour permettre à l’utilisateur d’envoyer des notifications Push dans l’application :</span><span class="sxs-lookup"><span data-stu-id="470e8-169">In Xcode, open `Main.storyboard` and add the following UI components from the object library to allow the user to send push notifications in the app:</span></span>
   
   * <span data-ttu-id="470e8-170">Une étiquette sans texte d’étiquette.</span><span class="sxs-lookup"><span data-stu-id="470e8-170">A label with no label text.</span></span> <span data-ttu-id="470e8-171">Elle sera utilisée pour signaler les erreurs d’envoi des notifications.</span><span class="sxs-lookup"><span data-stu-id="470e8-171">It will be used to report errors in sending notifications.</span></span> <span data-ttu-id="470e8-172">La propriété **Lines** doit être définie sur **0**, pour dimensionner automatiquement le contenu en fonction des marges droite et gauche ainsi que du haut de la vue.</span><span class="sxs-lookup"><span data-stu-id="470e8-172">The **Lines** property should be set to **0** so that it will automatically size constrained to the right and left margins and the top of the view.</span></span>
   * <span data-ttu-id="470e8-173">Un champ de texte avec du texte de l’**espace réservé** défini sur **Enter Notification Message**.</span><span class="sxs-lookup"><span data-stu-id="470e8-173">A text field with **Placeholder** text set to **Enter Notification Message**.</span></span> <span data-ttu-id="470e8-174">Limitez le champ juste en dessous de l'étiquette, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="470e8-174">Constrain the field just below the label as shown below.</span></span> <span data-ttu-id="470e8-175">Définissez le Contrôleur d'affichage comme délégué de sortie.</span><span class="sxs-lookup"><span data-stu-id="470e8-175">Set the View Controller as the outlet delegate.</span></span>
   * <span data-ttu-id="470e8-176">Un bouton **Envoyer une notification** limité juste en dessous du champ de texte, de manière horizontale et centrée.</span><span class="sxs-lookup"><span data-stu-id="470e8-176">A button titled **Send Notification** constrained just below the text field and in the horizontal center.</span></span>
     
     <span data-ttu-id="470e8-177">La vue doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="470e8-177">The view should look as follows:</span></span>
     
     ![Concepteur Xcode][32]
2. <span data-ttu-id="470e8-179">[Ajoutez des sorties](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) pour les champs de texte et d’étiquette connectés à votre affichage et mettez à jour votre définition `interface` pour prendre en charge `UITextFieldDelegate` et `NSXMLParserDelegate`.</span><span class="sxs-lookup"><span data-stu-id="470e8-179">[Add outlets](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) for the label and text field connected your view, and update your `interface` definition to support `UITextFieldDelegate` and `NSXMLParserDelegate`.</span></span> <span data-ttu-id="470e8-180">Ajoutez les trois déclarations de propriété ci-dessous pour aider le support à appeler l'API REST et à analyser la réponse.</span><span class="sxs-lookup"><span data-stu-id="470e8-180">Add the three property declarations shown below to help support calling the REST API and parsing the response.</span></span>
   
    <span data-ttu-id="470e8-181">Votre fichier ViewController.h doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="470e8-181">Your ViewController.h file should look as follows:</span></span>
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected to your UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. <span data-ttu-id="470e8-182">Ouvrez `HubInfo.h` et ajoutez les constantes suivantes, qui seront utilisées pour envoyer des notifications à votre hub.</span><span class="sxs-lookup"><span data-stu-id="470e8-182">Open `HubInfo.h` and add the following constants which will be used for sending notifications to your hub.</span></span> <span data-ttu-id="470e8-183">Remplacez le littéral de chaîne d’espace réservé par votre chaîne de connexion *DefaultFullSharedAccessSignature* actuelle.</span><span class="sxs-lookup"><span data-stu-id="470e8-183">Replace the placeholder string literal with your actual *DefaultFullSharedAccessSignature* connection string.</span></span>
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. <span data-ttu-id="470e8-184">Ajoutez les instructions `#import` suivantes à votre fichier `ViewController.h`.</span><span class="sxs-lookup"><span data-stu-id="470e8-184">Add the following `#import` statements to your `ViewController.h` file.</span></span>
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. <span data-ttu-id="470e8-185">Dans `ViewController.m` , ajoutez le code qui suit à l’implémentation de l’interface.</span><span class="sxs-lookup"><span data-stu-id="470e8-185">In `ViewController.m` add the following code to the interface implementation.</span></span> <span data-ttu-id="470e8-186">Ce code analysera la chaîne de connexion *DefaultFullSharedAccessSignature* .</span><span class="sxs-lookup"><span data-stu-id="470e8-186">This code will parse your *DefaultFullSharedAccessSignature* connection string.</span></span> <span data-ttu-id="470e8-187">Comme indiqué dans la [référence de l’API REST](http://msdn.microsoft.com/library/azure/dn495627.aspx), ces informations analysées permettront de générer un jeton SaS pour l’en-tête de demande **Authorization** .</span><span class="sxs-lookup"><span data-stu-id="470e8-187">As mentioned in the [REST API reference](http://msdn.microsoft.com/library/azure/dn495627.aspx), this parsed information will be used to generate a SaS token for the **Authorization** request header.</span></span>
   
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
6. <span data-ttu-id="470e8-188">Dans `ViewController.m`, mettez à jour la méthode `viewDidLoad` pour qu’elle analyse la chaîne de connexion lors du chargement de la vue.</span><span class="sxs-lookup"><span data-stu-id="470e8-188">In `ViewController.m`, update the `viewDidLoad` method to parse the connection string when the view loads.</span></span> <span data-ttu-id="470e8-189">Ajoutez également les méthodes d’utilitaire, figurant ci-dessous, à l’implémentation d’interface.</span><span class="sxs-lookup"><span data-stu-id="470e8-189">Also add the utility methods, shown below, to the interface implementation.</span></span>  

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





1. <span data-ttu-id="470e8-190">Dans `ViewController.m`, ajoutez le code suivant à l’implémentation de l’interface pour générer le jeton d’autorisation SaS qui sera fourni dans l’en-tête **Authorization** , comme indiqué dans la [référence de l’API REST](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="470e8-190">In `ViewController.m`, add the following code to the interface implementation to generate the SaS authorization token that will be provided in the **Authorization** header, as mentioned in the [REST API Reference](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span></span>
   
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
   
                // Get an hmac_sha1 Mac instance and initialize with the signing key
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
2. <span data-ttu-id="470e8-191">Tout en appuyant sur la touche Ctrl, faites glisser le bouton **Envoyer une notification** vers `ViewController.m` pour ajouter une action nommée **SendNotificationMessage** pour l’événement **Touch Down**.</span><span class="sxs-lookup"><span data-stu-id="470e8-191">Ctrl+drag from the **Send Notification** button to `ViewController.m` to add an action named **SendNotificationMessage** for the **Touch Down** event.</span></span> <span data-ttu-id="470e8-192">Mettez à jour la méthode à l’aide du code suivant pour envoyer la notification à l’aide de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="470e8-192">Update method with the following code to send the notification using the REST API.</span></span>
   
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
   
            // Apple Notification format of the notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct the message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate the token to be used in the authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create the request to add the APNs notification message to the hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate the notification message POST request with the SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add the notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send the REST request
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
3. <span data-ttu-id="470e8-193">Dans `ViewController.m`, ajoutez la méthode déléguée suivante pour prendre en charge la fermeture du clavier pour la zone de texte.</span><span class="sxs-lookup"><span data-stu-id="470e8-193">In `ViewController.m`, add the following delegate method to support closing the keyboard for the text field.</span></span> <span data-ttu-id="470e8-194">Utilisez la commande Ctrl+glisser depuis le champ de texte vers l’icône du contrôleur d’affichage dans le concepteur d’interface pour définir le contrôleur d’affichage comme sortie déléguée.</span><span class="sxs-lookup"><span data-stu-id="470e8-194">Ctrl+drag from the text field to the View Controller icon in the interface designer to set the view controller as the outlet delegate.</span></span>
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. <span data-ttu-id="470e8-195">Dans `ViewController.m`, ajoutez les méthodes déléguées suivantes pour prendre en charge l’analyse de la réponse à l’aide de `NSXMLParser`.</span><span class="sxs-lookup"><span data-stu-id="470e8-195">In `ViewController.m`, add the following delegate methods to support parsing the response by using `NSXMLParser`.</span></span>
   
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
           // Set the status label text on the UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. <span data-ttu-id="470e8-196">Générez le projet et vérifiez qu’il ne présente pas d’erreurs.</span><span class="sxs-lookup"><span data-stu-id="470e8-196">Build the project and verify that there are no errors.</span></span>

> [!NOTE]
> <span data-ttu-id="470e8-197">Si vous rencontrez une erreur de génération dans Xcode7 sur le support bitcode, vous devez modifier les **Paramètres de build** > **Activer Bitcode (ENABLE_BITCODE)** en indiquant **NON** dans Xcode.</span><span class="sxs-lookup"><span data-stu-id="470e8-197">If you encounter a build error in Xcode7 about bitcode support, you should change the **Build Settings** > **Enable Bitcode (ENABLE_BITCODE)** to **NO** in Xcode.</span></span> <span data-ttu-id="470e8-198">Le kit de développement logiciel Notification Hubs ne prend pas en charge bitcode.</span><span class="sxs-lookup"><span data-stu-id="470e8-198">The Notification Hubs SDK does not currently support bitcode.</span></span> 
> 
> 

<span data-ttu-id="470e8-199">Vous trouverez toutes les charges de notification possibles dans le [Guide de programmation des notifications locales et push]d’Apple.</span><span class="sxs-lookup"><span data-stu-id="470e8-199">You can find all the possible notification payloads in the Apple [Local and Push Notification Programming Guide].</span></span>

## <a name="checking-if-your-app-can-receive-push-notifications"></a><span data-ttu-id="470e8-200">Vérifier si votre application peut recevoir des notifications Push</span><span class="sxs-lookup"><span data-stu-id="470e8-200">Checking if your app can receive push notifications</span></span>
<span data-ttu-id="470e8-201">Pour tester les notifications Push sur iOS, vous devez déployer l’application sur un appareil iOS physique.</span><span class="sxs-lookup"><span data-stu-id="470e8-201">To test push notifications on iOS, you must deploy the app to a physical iOS device.</span></span> <span data-ttu-id="470e8-202">Vous ne pouvez pas envoyer de notifications push Apple en utilisant le simulateur iOS.</span><span class="sxs-lookup"><span data-stu-id="470e8-202">You cannot send Apple push notifications by using the iOS Simulator.</span></span>

1. <span data-ttu-id="470e8-203">Exécutez l’application, vérifiez que l’inscription est effectuée, puis appuyez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="470e8-203">Run the app and verify that registration succeeds, and then press **OK**.</span></span>
   
    ![Test d’inscription de notifications Push pour applications iOS][33]
2. <span data-ttu-id="470e8-205">Vous pouvez envoyer une notification de test depuis le [portail Azure], comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="470e8-205">You can send a test push notification from the [Azure Portal], as described above.</span></span> <span data-ttu-id="470e8-206">Si vous avez ajouté du code pour l’envoi de notifications Push dans l’application, touchez le champ de texte pour entrer un message de notification.</span><span class="sxs-lookup"><span data-stu-id="470e8-206">If you added code for sending push notifications in the app, touch inside the text field to enter a notification message.</span></span> <span data-ttu-id="470e8-207">Appuyez sur le bouton d’**envoi** du clavier ou sur le bouton **Envoyer une notification** de l’affichage pour envoyer le message de notification.</span><span class="sxs-lookup"><span data-stu-id="470e8-207">Then press the **Send** button on the keyboard or the **Send Notification** button in the view to send the notification message.</span></span>
   
    ![Test d’envoi de notifications Push pour applications iOS][34]
3. <span data-ttu-id="470e8-209">La notification Push est envoyée à tous les appareils qui sont inscrits pour recevoir les notifications depuis le hub de notification concerné.</span><span class="sxs-lookup"><span data-stu-id="470e8-209">The push notification is sent to all devices that are registered to receive the notifications from the particular Notification Hub.</span></span>
   
    ![Test de réception de notifications Push pour applications iOS][35]

## <a name="next-steps"></a><span data-ttu-id="470e8-211">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="470e8-211">Next steps</span></span>
<span data-ttu-id="470e8-212">Dans cet exemple simple, vous avez envoyé des notifications Push à tous vos appareils iOS inscrits.</span><span class="sxs-lookup"><span data-stu-id="470e8-212">In this simple example, you broadcasted push notifications to all your registered iOS devices.</span></span> <span data-ttu-id="470e8-213">Nous vous suggérons de poursuivre votre apprentissage en passant au didacticiel [Azure Notification Hubs notifie les utilisateurs pour iOS avec backend .NET] qui vous guidera dans la création d’un serveur principal pour l’envoi de notifications Push à l’aide de balises.</span><span class="sxs-lookup"><span data-stu-id="470e8-213">We suggest as a next step in your learning that you proceed to the [Azure Notification Hubs Notify Users for iOS with .NET backend] tutorial, which will walk you through creating a backend to send push notifications using tags.</span></span> 

<span data-ttu-id="470e8-214">Si vous souhaitez segmenter vos utilisateurs par groupes d’intérêt, vous pouvez passer au didacticiel [Utilisation de Notification Hubs pour diffuser les dernières nouvelles] .</span><span class="sxs-lookup"><span data-stu-id="470e8-214">If you want to segment your users by interest groups, you can additionally move on to the [Use Notification Hubs to send breaking news] tutorial.</span></span> 

<span data-ttu-id="470e8-215">Pour obtenir des informations générales sur Notification Hubs, consultez [Recommandations relatives à Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="470e8-215">For general information about Notification Hubs, see [Notification Hubs Guidance].</span></span>

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
<span data-ttu-id="470e8-216">[version 1.2.4 du kit de développement logiciel (SDK) Mobile Services iOS]: http://aka.ms/kymw2g</span><span class="sxs-lookup"><span data-stu-id="470e8-216">[Mobile Services iOS SDK version 1.2.4]: http://aka.ms/kymw2g</span></span>
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
<span data-ttu-id="470e8-217">[Recommandations relatives à Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="470e8-217">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="470e8-218">[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532</span><span class="sxs-lookup"><span data-stu-id="470e8-218">[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532</span></span>
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
<span data-ttu-id="470e8-219">[Azure Notification Hubs notifie les utilisateurs pour iOS avec backend .NET]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md</span><span class="sxs-lookup"><span data-stu-id="470e8-219">[Azure Notification Hubs Notify Users for iOS with .NET backend]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md</span></span>
<span data-ttu-id="470e8-220">[Utilisation de Notification Hubs pour diffuser les dernières nouvelles]: notification-hubs-ios-xplat-segmented-apns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="470e8-220">[Use Notification Hubs to send breaking news]: notification-hubs-ios-xplat-segmented-apns-push-notification.md</span></span>

<span data-ttu-id="470e8-221">[Guide de programmation des notifications locales et push]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1</span><span class="sxs-lookup"><span data-stu-id="470e8-221">[Local and Push Notification Programming Guide]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1</span></span>
<span data-ttu-id="470e8-222">[portail Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="470e8-222">[Azure Portal]: https://portal.azure.com</span></span>
