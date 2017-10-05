---
title: "Prise en main d’Azure Notification Hubs pour les applications de plateforme Windows universelle | Microsoft Docs"
description: "Dans ce didacticiel, vous découvrirez comment utiliser Azure Notification Hubs pour envoyer des notifications Push à une application de plateforme Windows universelle."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: erikre
ms.assetid: cf307cf3-8c58-4628-9c63-8751e6a0ef43
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 9b50f1cca81348b69f7ff2d702c6c72871afe0a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a><span data-ttu-id="0af26-103">Prise en main de Notification Hubs pour les applications de plateforme Windows universelle</span><span class="sxs-lookup"><span data-stu-id="0af26-103">Getting started with Notification Hubs for Windows Universal Platform Apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="0af26-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="0af26-104">Overview</span></span>
<span data-ttu-id="0af26-105">Ce didacticiel vous indique comment utiliser Azure Notification Hubs pour envoyer des notifications Push à une application de plateforme Windows universelle (UWP).</span><span class="sxs-lookup"><span data-stu-id="0af26-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Universal Windows Platform (UWP) app.</span></span>

<span data-ttu-id="0af26-106">Le didacticiel vous apprend à créer une application Windows Store vide qui reçoit des notifications Push au moyen du Service de notifications Windows Push (WNS).</span><span class="sxs-lookup"><span data-stu-id="0af26-106">In this tutorial, you create a blank Windows Store app that receives push notifications by using the Windows Push Notification Service (WNS).</span></span> <span data-ttu-id="0af26-107">Une fois l’opération terminée, vous pouvez utiliser votre hub de notification pour diffuser des notifications Push sur tous les appareils exécutant votre application.</span><span class="sxs-lookup"><span data-stu-id="0af26-107">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0af26-108">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="0af26-108">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="0af26-109">Le code complet de ce didacticiel est disponible sur GitHub [ici](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span><span class="sxs-lookup"><span data-stu-id="0af26-109">The completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0af26-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0af26-110">Prerequisites</span></span>
<span data-ttu-id="0af26-111">Ce didacticiel requiert les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0af26-111">This tutorial requires the following:</span></span>

* <span data-ttu-id="0af26-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="0af26-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) or later</span></span>
* [<span data-ttu-id="0af26-113">Outils de développement d’applications Windows universelles installés</span><span class="sxs-lookup"><span data-stu-id="0af26-113">Universal Windows App Development Tools installed</span></span>](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* <span data-ttu-id="0af26-114">Un compte Azure actif </span><span class="sxs-lookup"><span data-stu-id="0af26-114">An active Azure account</span></span> <br/><span data-ttu-id="0af26-115">Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="0af26-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0af26-116">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="0af26-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span></span>
* <span data-ttu-id="0af26-117">Un compte Windows Store actif</span><span class="sxs-lookup"><span data-stu-id="0af26-117">An active Windows Store account</span></span>

<span data-ttu-id="0af26-118">Vous devez suivre ce didacticiel avant de pouvoir suivre tous les autres didacticiels Notification Hubs pour les applications de plateforme Windows universelle.</span><span class="sxs-lookup"><span data-stu-id="0af26-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Universal Platform apps.</span></span>

## <a name="register-your-app-for-the-windows-store"></a><span data-ttu-id="0af26-119">Inscription de votre application pour le Windows Store</span><span class="sxs-lookup"><span data-stu-id="0af26-119">Register your app for the Windows Store</span></span>
<span data-ttu-id="0af26-120">Pour envoyer des notifications Push à des applications UWP, vous devez associer votre application au Windows Store.</span><span class="sxs-lookup"><span data-stu-id="0af26-120">To send push notifications to UWP apps, you must associate your app to the Windows Store.</span></span> <span data-ttu-id="0af26-121">Vous devez ensuite configurer votre Notification Hub pour l'intégrer à WNS.</span><span class="sxs-lookup"><span data-stu-id="0af26-121">You must then configure your notification hub to integrate with WNS.</span></span>

1. <span data-ttu-id="0af26-122">Si vous n’avez pas déjà inscrit votre application, accédez à la page [Centre de développement Windows](https://dev.windows.com/overview), connectez-vous avec votre compte Microsoft, puis cliquez sur **Créer une application**.</span><span class="sxs-lookup"><span data-stu-id="0af26-122">If you have not already registered your app, navigate to the [Windows Dev Center](https://dev.windows.com/overview), sign in with your Microsoft account, and then click **Create a new app**.</span></span>

2. <span data-ttu-id="0af26-123">Saisissez un nom pour votre application et cliquez sur **Réserver le nom d’application**.</span><span class="sxs-lookup"><span data-stu-id="0af26-123">Type a name for your app and click **Reserve app name**.</span></span> <span data-ttu-id="0af26-124">La nouvelle inscription au Windows Store pour votre application est créée.</span><span class="sxs-lookup"><span data-stu-id="0af26-124">This creates a new Windows Store registration for your app.</span></span>

3. <span data-ttu-id="0af26-125">Dans Visual Studio, créez un projet d’application du Windows Store Visual C# en utilisant le modèle **Application vide** Windows Universal, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0af26-125">In Visual Studio, create a new Visual C# Store Apps project by using the Windows Universal **Blank App** template and click **OK**.</span></span>

4. <span data-ttu-id="0af26-126">Acceptez les valeurs par défaut pour les versions de plateforme cible et minimale.</span><span class="sxs-lookup"><span data-stu-id="0af26-126">Accept the defaults for the target and minimum platform versions.</span></span>

5. <span data-ttu-id="0af26-127">Dans l'Explorateur de solutions, cliquez avec le bouton droit sur le projet d'application Windows Store, cliquez sur **Store**, puis sur **Associer l'application au Windows Store...**.</span><span class="sxs-lookup"><span data-stu-id="0af26-127">In Solution Explorer, right-click the Windows Store app project, click **Store**, and then click **Associate App with the Store...**.</span></span> <span data-ttu-id="0af26-128">L'Assistant **Associer votre application au Windows Store** s'affiche.</span><span class="sxs-lookup"><span data-stu-id="0af26-128">The **Associate Your App with the Windows Store** wizard appears.</span></span>

6. <span data-ttu-id="0af26-129">Dans l’Assistant, connectez-vous avec votre compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0af26-129">In the wizard, sign in with your Microsoft account.</span></span>

7. <span data-ttu-id="0af26-130">Cliquez sur l'application inscrite à l'étape 2, puis sur **Suivant** et sur **Associer**.</span><span class="sxs-lookup"><span data-stu-id="0af26-130">Click the app that you registered in step 2, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="0af26-131">Cela ajoute les informations d'inscription Windows Store requises au manifeste de l'application.</span><span class="sxs-lookup"><span data-stu-id="0af26-131">This adds the required Windows Store registration information to the application manifest.</span></span>

8. <span data-ttu-id="0af26-132">De nouveau sur la page [Centre de développement Windows](http://dev.windows.com/overview) pour votre nouvelle application, cliquez sur **Services**, puis sur **Notifications Push** et enfin sur **WNS/MPNS**.</span><span class="sxs-lookup"><span data-stu-id="0af26-132">Back on the [Windows Dev Center](http://dev.windows.com/overview) page for your new app, click **Services**, click **Push notifications**, and then click **WNS/MPNS**.</span></span>

9. <span data-ttu-id="0af26-133">Cliquez sur **Nouvelle notification**.</span><span class="sxs-lookup"><span data-stu-id="0af26-133">Click **New Notification**.</span></span>

10. <span data-ttu-id="0af26-134">Cliquez sur le modèle **Blank (Toast)** (Vide (Toast), puis sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0af26-134">Click **Blank (Toast)** template and then click **OK**.</span></span>

11. <span data-ttu-id="0af26-135">Saisissez un **nom** et un message de **contexte** Visual pour la notification.</span><span class="sxs-lookup"><span data-stu-id="0af26-135">Enter a notification **Name** and Visual **Context** message.</span></span> <span data-ttu-id="0af26-136">Cliquez ensuite sur **Enregistrer en tant que brouillon**.</span><span class="sxs-lookup"><span data-stu-id="0af26-136">Then click **Save as draft**.</span></span>

12. <span data-ttu-id="0af26-137">Accédez au [portail d’inscription des applications](http://apps.dev.microsoft.com) et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="0af26-137">Navigate to the [Application Registration Portal](http://apps.dev.microsoft.com) and log in.</span></span>

13. <span data-ttu-id="0af26-138">Cliquez sur le nom de votre application.</span><span class="sxs-lookup"><span data-stu-id="0af26-138">Click on your application name.</span></span> <span data-ttu-id="0af26-139">Notez le mot de passe **Clé secrète d’application** et la valeur **Identificateur de sécurité (SID) du package** figurant dans les paramètres de la plateforme **Windows Store**.</span><span class="sxs-lookup"><span data-stu-id="0af26-139">Make a note of the **Application Secret** password and the **Package security identifier (SID)** located in the **Windows Store** platform settings.</span></span>

     > [AZURE.WARNING]
    <span data-ttu-id="0af26-140">Le secret d’application et le SID du package sont des informations d'identification de sécurité importantes.</span><span class="sxs-lookup"><span data-stu-id="0af26-140">The application secret and package SID are important security credentials.</span></span> <span data-ttu-id="0af26-141">Ne partagez pas ces valeurs avec quiconque et ne les distribuez pas avec votre application.</span><span class="sxs-lookup"><span data-stu-id="0af26-141">Do not share these values with anyone or distribute them with your app.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="0af26-142">Configuration de votre hub de notification</span><span class="sxs-lookup"><span data-stu-id="0af26-142">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="0af26-143">Sélectionnez les options <b>Services de notification</b> et <b>Windows (WNS)</b>.</span><span class="sxs-lookup"><span data-stu-id="0af26-143">Select the <b>Notification Services</b> option and the <b>Windows (WNS)</b> option.</span></span> <span data-ttu-id="0af26-144">Puis entrez le mot de passe <b>Clé secrète d’application</b> dans le champ <b>Clé de sécurité</b>.</span><span class="sxs-lookup"><span data-stu-id="0af26-144">Then enter the <b>Application secret</b> password in the <b>Security Key</b> field.</span></span> <span data-ttu-id="0af26-145">Entrez la valeur <b>SID du package</b> que vous avez obtenue auprès de WNS à la section précédente, puis cliquez sur <b>Enregistrer</b>.</span><span class="sxs-lookup"><span data-stu-id="0af26-145">Enter your <b>Package SID</b> value that you obtained from WNS in the previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

<span data-ttu-id="0af26-146">Votre Notification Hub est désormais configuré pour WNS, et vous disposez des chaînes de connexion pour inscrire votre application et envoyer des notifications.</span><span class="sxs-lookup"><span data-stu-id="0af26-146">Your notification hub is now configured to work with WNS, and you have the connection strings to register your app and send notifications.</span></span>

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="0af26-147">Connexion de votre application au hub de notification</span><span class="sxs-lookup"><span data-stu-id="0af26-147">Connect your app to the notification hub</span></span>
1. <span data-ttu-id="0af26-148">Dans Visual Studio, cliquez avec le bouton droit sur la solution, puis cliquez sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="0af26-148">In Visual Studio, right-click the solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="0af26-149">La boîte de dialogue **Gérer les packages NuGet** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="0af26-149">This displays the **Manage NuGet Packages** dialog box.</span></span>
2. <span data-ttu-id="0af26-150">Recherchez `WindowsAzure.Messaging.Managed` , puis cliquez sur **Installer**et acceptez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="0af26-150">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and accept the terms of use.</span></span>
   
    ![][20]
   
    <span data-ttu-id="0af26-151">Une référence à la bibliothèque Azure Messaging pour Windows est alors téléchargée, installée et ajoutée à l’aide du <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">package NuGet WindowsAzure.Messaging.Managed</a>.</span><span class="sxs-lookup"><span data-stu-id="0af26-151">This downloads, installs, and adds a reference to the Azure Messaging library for Windows by using the <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
3. <span data-ttu-id="0af26-152">Ouvrez le fichier projet App.xaml.cs et ajoutez les instructions `using` qui suivent.</span><span class="sxs-lookup"><span data-stu-id="0af26-152">Open the App.xaml.cs project file and add the following `using` statements.</span></span> 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. <span data-ttu-id="0af26-153">Toujours dans le fichier App.xaml.cs, ajoutez la définition de méthode **InitNotificationsAsync** suivante à la classe **App** :</span><span class="sxs-lookup"><span data-stu-id="0af26-153">Also in App.xaml.cs, add the following **InitNotificationsAsync** method definition to the **App** class:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    <span data-ttu-id="0af26-154">Ce code récupère l’URI de canal pour l’application dans WNS et l’inscrit avec votre Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="0af26-154">This code retrieves the channel URI for the app from WNS, and then registers that channel URI with your notification hub.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0af26-155">Remplacez l’espace réservé pour votre nom de hub par le nom du hub de notification affiché sur le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0af26-155">Make sure to replace the "your hub name" placeholder with the name of the notification hub that appears in the Azure Portal.</span></span> <span data-ttu-id="0af26-156">Remplacez également l’espace réservé de la chaîne de connexion par la chaîne de connexion **DefaultListenSharedAccessSignature** que vous avez obtenue sur la page **Stratégies d’accès** de votre hub de notification dans une section précédente.</span><span class="sxs-lookup"><span data-stu-id="0af26-156">Also replace the connection string placeholder with the **DefaultListenSharedAccessSignature** connection string that you obtained from the **Access Polices** page of your Notification Hub in a previous section.</span></span>
   > 
   > 
5. <span data-ttu-id="0af26-157">En haut du gestionnaire d'événements **OnLaunched** dans App.xaml.cs, ajoutez l'appel suivant à la nouvelle méthode **InitNotificationsAsync** :</span><span class="sxs-lookup"><span data-stu-id="0af26-157">At the top of the **OnLaunched** event handler in App.xaml.cs, add the following call to the new **InitNotificationsAsync** method:</span></span>
   
        InitNotificationsAsync();
   
    <span data-ttu-id="0af26-158">Cela garantit que l’inscription de l’URI de canal dans votre Notification Hub chaque fois que l’application est lancée.</span><span class="sxs-lookup"><span data-stu-id="0af26-158">This guarantees that the channel URI is registered in your notification hub each time the application is launched.</span></span>
6. <span data-ttu-id="0af26-159">Appuyez sur **F5** pour lancer l'application.</span><span class="sxs-lookup"><span data-stu-id="0af26-159">Press the **F5** key to run the app.</span></span> <span data-ttu-id="0af26-160">Une boîte de dialogue s’affiche avec la clé d’inscription.</span><span class="sxs-lookup"><span data-stu-id="0af26-160">A pop-up dialog that contains the registration key is displayed.</span></span>

<span data-ttu-id="0af26-161">Votre application est maintenant prête à recevoir des notifications toast.</span><span class="sxs-lookup"><span data-stu-id="0af26-161">Your app is now ready to receive toast notifications.</span></span>

## <a name="send-notifications"></a><span data-ttu-id="0af26-162">Envoi de notifications</span><span class="sxs-lookup"><span data-stu-id="0af26-162">Send notifications</span></span>
<span data-ttu-id="0af26-163">Vous pouvez tester rapidement la réception de notifications dans votre application en envoyant des notifications dans le [Portail Azure](https://portal.azure.com/) à l’aide du bouton **Test d’envoi** sur le hub de notification, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0af26-163">You can quickly test receiving notifications in your app by sending notifications in the [Azure Portal](https://portal.azure.com/) using the **Test Send** button on the notification hub, as shown in the screen below.</span></span>

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

<span data-ttu-id="0af26-164">Les notifications Push sont normalement envoyées dans un service principal tel que Mobile Services ou ASP.NET à l’aide d’une bibliothèque compatible.</span><span class="sxs-lookup"><span data-stu-id="0af26-164">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="0af26-165">Vous pouvez également utiliser l’API REST directement pour envoyer des messages de notification si aucune bibliothèque n’est disponible pour votre serveur principal.</span><span class="sxs-lookup"><span data-stu-id="0af26-165">You can also use the REST API directly to send notification messages if a library is not available for your back-end.</span></span> 

<span data-ttu-id="0af26-166">Dans ce didacticiel, nous nous contenterons pour plus de simplicité de tester votre application cliente en envoyant des notifications à l'aide du Kit de développement logiciel (SDK) .NET pour Notification Hubs dans une application de console au lieu d'un service principal.</span><span class="sxs-lookup"><span data-stu-id="0af26-166">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using the .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="0af26-167">Nous vous recommandons de consulter le didacticiel [Utiliser Notification Hubs pour envoyer des notifications Push aux utilisateurs] comme prochaine étape pour envoyer des notifications à partir d’un serveur principal ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="0af26-167">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="0af26-168">Toutefois, les approches suivantes peuvent servir à envoyer des notifications :</span><span class="sxs-lookup"><span data-stu-id="0af26-168">However, the following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="0af26-169">**Interface REST** : vous pouvez prendre en charge les notifications sur n’importe quel serveur principal à l’aide de [l’interface REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="0af26-169">**REST Interface**:  You can support notification on any backend platform using  the [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="0af26-170">**SDK .NET Microsoft Azure Notification Hubs**: dans le Gestionnaire de package Nuget pour Visual Studio, exécutez [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="0af26-170">**Microsoft Azure Notification Hubs .NET SDK**: In the Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="0af26-171">**Node.js** : [Utilisation de Notification Hubs à partir de Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="0af26-171">**Node.js** : [How to use Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="0af26-172">**Applications mobiles Azure**: pour découvrir un exemple de la procédure d’envoi de notifications à partir d’une application mobile Azure intégrée à Notification Hubs, consultez l’article [Add push notifications for Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md)(Ajouter des notifications Push pour Mobile Apps).</span><span class="sxs-lookup"><span data-stu-id="0af26-172">**Azure Mobile Apps**: For an example of how to send notifications from an Azure Mobile App that's integrated with Notification Hubs, see [Add push notifications for Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="0af26-173">**Java/PHP** : pour voir un exemple d’envoi de notifications au moyen des API REST, consultez « Utilisation de Notification Hubs depuis Java/PHP » ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="0af26-173">**Java / PHP**: For an example of how to send notifications by using the REST APIs, see "How to use Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-console-app"></a><span data-ttu-id="0af26-174">(Facultatif) Envoi de notifications à partir d’une application de console</span><span class="sxs-lookup"><span data-stu-id="0af26-174">(Optional) Send notifications from a console app</span></span>
<span data-ttu-id="0af26-175">Procédez comme suit pour envoyer des notifications à l’aide d’une application de console .NET.</span><span class="sxs-lookup"><span data-stu-id="0af26-175">To send notifications by using a .NET console application follow these steps.</span></span> 

1. <span data-ttu-id="0af26-176">Cliquez avec le bouton droit sur la solution, sélectionnez **Ajouter** et **Nouveau projet**, puis sous **Visual C#**, cliquez sur **Windows** et **Application Console**. Enfin, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0af26-176">Right-click the solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
    <span data-ttu-id="0af26-177">Une nouvelle application console Visual C# est ajoutée à la solution.</span><span class="sxs-lookup"><span data-stu-id="0af26-177">This adds a new Visual C# console application to the solution.</span></span> <span data-ttu-id="0af26-178">Vous pouvez également réaliser cette opération dans une solution distincte.</span><span class="sxs-lookup"><span data-stu-id="0af26-178">You can also do this in a separate solution.</span></span>

2. <span data-ttu-id="0af26-179">Dans Visual Studio, cliquez successivement sur **Outils**, **Gestionnaire de package NuGet** et **Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="0af26-179">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="0af26-180">La console du gestionnaire de package s’affiche dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0af26-180">This displays the Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="0af26-181">Dans la fenêtre Console du gestionnaire de package, choisissez **Projet par défaut** comme nouveau projet d’application console, puis exécutez la commande suivante dans la fenêtre de console :</span><span class="sxs-lookup"><span data-stu-id="0af26-181">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="0af26-182">Cette opération ajoute une référence au Kit de développement logiciel (SDK) Azure Notification Hubs à l’aide du <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">package NuGet Microsoft.Azure.Notification Hubs</a>.</span><span class="sxs-lookup"><span data-stu-id="0af26-182">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="0af26-183">Ouvrez le fichier Program.cs et ajoutez l’instruction `using` suivante :</span><span class="sxs-lookup"><span data-stu-id="0af26-183">Open the Program.cs file and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="0af26-184">Dans la classe **Program** , ajoutez la méthode suivante :</span><span class="sxs-lookup"><span data-stu-id="0af26-184">In the **Program** class, add the following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure to replace the "hub name" placeholder with the name of the notification hub that as it appears in the Azure Portal. Also, replace the connection string placeholder with the **DefaultFullSharedAccessSignature** connection string that you obtained from the **Access Policies** page of your Notification Hub in the section called "Configure your notification hub."
   
   > [!NOTE]
   > <span data-ttu-id="0af26-185">Veillez à utiliser la chaîne de connexion avec un accès **Total**, et non un accès **Écouter**.</span><span class="sxs-lookup"><span data-stu-id="0af26-185">Make sure that you use the connection string that has **Full** access, not **Listen** access.</span></span> <span data-ttu-id="0af26-186">La chaîne d’accès en écoute seule ne dispose pas des autorisations pour envoyer des notifications.</span><span class="sxs-lookup"><span data-stu-id="0af26-186">The listen-access string does not have permissions to send notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="0af26-187">Ajoutez les lignes suivantes à la méthode **Main** :</span><span class="sxs-lookup"><span data-stu-id="0af26-187">Add the following lines in the **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="0af26-188">Cliquez avec le bouton droit sur le projet d’application de console dans Visual Studio, puis cliquez sur **Définir comme projet de démarrage** .</span><span class="sxs-lookup"><span data-stu-id="0af26-188">Right-click the console application project in Visual Studio, and click **Set as StartUp Project** to set it as the startup project.</span></span> <span data-ttu-id="0af26-189">Appuyez ensuite sur la touche **F5** pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="0af26-189">Then press the **F5** key to run the application.</span></span>
   
    <span data-ttu-id="0af26-190">Vous recevrez une notification toast sur tous les appareils enregistrés.</span><span class="sxs-lookup"><span data-stu-id="0af26-190">You will receive a toast notification on all registered devices.</span></span> <span data-ttu-id="0af26-191">Cliquez sur la bannière toast ou appuyez dessus pour charger l’application.</span><span class="sxs-lookup"><span data-stu-id="0af26-191">Clicking or tapping the toast banner loads the app.</span></span>

<span data-ttu-id="0af26-192">Vous trouverez toutes les charges utiles prises en charge dans les rubriques [Catalogue de modèles de toast], [Catalogue de modèles de vignette] et [Vue d’ensemble des badges] sur MSDN.</span><span class="sxs-lookup"><span data-stu-id="0af26-192">You can find all the supported payloads in the [toast catalog], [tile catalog], and [badge overview] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0af26-193">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0af26-193">Next steps</span></span>
<span data-ttu-id="0af26-194">Dans cet exemple simple, vous avez envoyé des notifications à tous vos appareils Windows en utilisant le portail ou une application de console.</span><span class="sxs-lookup"><span data-stu-id="0af26-194">In this simple example, you sent broadcast notifications to all your Windows devices using the portal or a console app.</span></span> <span data-ttu-id="0af26-195">Nous vous recommandons de consulter le didacticiel [Utiliser Notification Hubs pour envoyer des notifications Push aux utilisateurs] comme prochaine étape.</span><span class="sxs-lookup"><span data-stu-id="0af26-195">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step.</span></span> <span data-ttu-id="0af26-196">Il vous expliquera comment envoyer des notifications à partir d’un serveur principal ASP.NET en utilisant des balises pour cibler des utilisateurs spécifiques.</span><span class="sxs-lookup"><span data-stu-id="0af26-196">It will show you how to send notifications from an ASP.NET backend using tags to target specific users.</span></span>

<span data-ttu-id="0af26-197">Pour segmenter vos utilisateurs par groupes d'intérêt, consultez la page [Utilisation des Notification Hubs pour diffuser les dernières nouvelles].</span><span class="sxs-lookup"><span data-stu-id="0af26-197">If you want to segment your users by interest groups, see [Use Notification Hubs to send breaking news].</span></span> 

<span data-ttu-id="0af26-198">Pour obtenir des informations générales sur Notification Hubs, consultez la section [Recommandations relatives à Notification Hubs](notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0af26-198">To learn more general information about Notification Hubs, see [Notification Hubs Guidance](notification-hubs-push-notification-overview.md).</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

<span data-ttu-id="0af26-199">[Utiliser Notification Hubs pour envoyer des notifications Push aux utilisateurs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="0af26-199">[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
<span data-ttu-id="0af26-200">[Utilisation des Notification Hubs pour diffuser les dernières nouvelles]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="0af26-200">[Use Notification Hubs to send breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>

<span data-ttu-id="0af26-201">[Catalogue de modèles de toast]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx</span><span class="sxs-lookup"><span data-stu-id="0af26-201">[toast catalog]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx</span></span>
<span data-ttu-id="0af26-202">[Catalogue de modèles de vignette]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx</span><span class="sxs-lookup"><span data-stu-id="0af26-202">[tile catalog]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx</span></span>
<span data-ttu-id="0af26-203">[Vue d’ensemble des badges]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx</span><span class="sxs-lookup"><span data-stu-id="0af26-203">[badge overview]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx</span></span>
