---
title: "Notifications Push sécurisées avec Azure Notification Hubs"
description: "Découvrez comment envoyer des notifications Push sécurisées dans Azure. Exemples de code écrits en C# à l’aide de l’API .NET."
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 5aef50f4-80b3-460e-a9a7-7435001273bd
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 9c626ec1534c4899588150a58c0da57b9d963f6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="444a8-104">Notifications Push sécurisées avec Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="444a8-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="444a8-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="444a8-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="444a8-106">iOS</span><span class="sxs-lookup"><span data-stu-id="444a8-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="444a8-107">Android</span><span class="sxs-lookup"><span data-stu-id="444a8-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="444a8-108">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="444a8-108">Overview</span></span>
<span data-ttu-id="444a8-109">La prise en charge des notifications Push dans Microsoft Azure vous permet d’accéder à une infrastructure Push conviviale, multiplateforme avec montée en charge qui simplifie fortement l’implémentation des notifications Push pour les applications grand public et d’entreprise destinées aux plateformes mobiles.</span><span class="sxs-lookup"><span data-stu-id="444a8-109">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="444a8-110">En raison de contraintes liées à la réglementation ou à la sécurité, une application peut avoir besoin d'inclure dans la notification des informations qui ne peuvent pas être transmises via l'infrastructure de notification Push standard.</span><span class="sxs-lookup"><span data-stu-id="444a8-110">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="444a8-111">Ce didacticiel montre comment procéder en envoyant des informations sensibles par l'intermédiaire d'une connexion authentifiée sécurisée entre l'appareil client et le serveur principal de l'application.</span><span class="sxs-lookup"><span data-stu-id="444a8-111">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client device and the app backend.</span></span>

<span data-ttu-id="444a8-112">Globalement, le processus est le suivant :</span><span class="sxs-lookup"><span data-stu-id="444a8-112">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="444a8-113">Le serveur principal de l'application :</span><span class="sxs-lookup"><span data-stu-id="444a8-113">The app back-end:</span></span>
   * <span data-ttu-id="444a8-114">stocke la charge utile sécurisée dans la base de données principale ;</span><span class="sxs-lookup"><span data-stu-id="444a8-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="444a8-115">envoie l'ID de cette notification à l'appareil (aucune information sécurisée n'est envoyée).</span><span class="sxs-lookup"><span data-stu-id="444a8-115">Sends the ID of this notification to the device (no secure information is sent).</span></span>
2. <span data-ttu-id="444a8-116">L'application qui se trouve sur l'appareil, lorsqu'elle reçoit la notification :</span><span class="sxs-lookup"><span data-stu-id="444a8-116">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="444a8-117">L'appareil contacte le serveur principal en demandant la charge utile sécurisée.</span><span class="sxs-lookup"><span data-stu-id="444a8-117">The device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="444a8-118">L'application peut afficher la charge utile sous la forme d'une notification sur l'appareil.</span><span class="sxs-lookup"><span data-stu-id="444a8-118">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="444a8-119">Veuillez noter que dans le flux précédent (et dans ce didacticiel), nous partons du principe que l’appareil stocke un jeton d’authentification dans un stockage local, une fois l’utilisateur connecté.</span><span class="sxs-lookup"><span data-stu-id="444a8-119">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="444a8-120">Cela simplifie nettement l’expérience, car l’appareil peut récupérer la charge utile sécurisée en utilisant ce jeton.</span><span class="sxs-lookup"><span data-stu-id="444a8-120">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="444a8-121">Si votre application ne stocke pas les jetons d'authentification sur l'appareil, ou si ces jetons sont susceptibles d'expirer, lorsque l'application sur l'appareil reçoit la notification, elle doit afficher une notification générique demandant à l'utilisateur de lancer l'application.</span><span class="sxs-lookup"><span data-stu-id="444a8-121">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="444a8-122">L'application authentifie alors l'utilisateur et affiche la charge utile de la notification.</span><span class="sxs-lookup"><span data-stu-id="444a8-122">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="444a8-123">Ce didacticiel sur les notifications Push sécurisées montre comment envoyer une notification Push en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="444a8-123">This Secure Push tutorial shows how to send a push notification securely.</span></span> <span data-ttu-id="444a8-124">Il s’appuie sur le didacticiel [Envoi de notifications à des utilisateurs](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md). Vous devez donc suivre ce dernier au préalable.</span><span class="sxs-lookup"><span data-stu-id="444a8-124">The tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, so you should complete the steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="444a8-125">Ce didacticiel part du principe que vous avez créé et configuré votre hub de notification comme décrit dans [Prise en main de Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="444a8-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span></span>
> <span data-ttu-id="444a8-126">Notez également que Windows Phone 8.1 nécessite des informations d’identification Windows (pas Windows Phone) et que les tâches en arrière-plan ne fonctionnent pas sur Windows Phone 8.0 ou Silverlight 8.1.</span><span class="sxs-lookup"><span data-stu-id="444a8-126">Also, note that Windows Phone 8.1 requires Windows (not Windows Phone) credentials, and that background tasks do not work on Windows Phone 8.0 or Silverlight 8.1.</span></span> <span data-ttu-id="444a8-127">Pour les applications Windows Store, vous pouvez recevoir des notifications via une tâche en arrière-plan uniquement si l'écran de verrouillage activé pour l'application (activez la case à cocher dans Appmanifest).</span><span class="sxs-lookup"><span data-stu-id="444a8-127">For Windows Store applications, you can receive notifications via a background task only if the app is lock-screen enabled (click the checkbox in the Appmanifest).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-windows-phone-project"></a><span data-ttu-id="444a8-128">Modification du projet Windows Phone</span><span class="sxs-lookup"><span data-stu-id="444a8-128">Modify the Windows Phone Project</span></span>
1. <span data-ttu-id="444a8-129">Dans le projet **NotifyUserWindowsPhone** , ajoutez le code suivant à App.xaml.cs afin d'enregistrer la tâche en arrière-plan pour les notifications Push.</span><span class="sxs-lookup"><span data-stu-id="444a8-129">In the **NotifyUserWindowsPhone** project, add the following code to App.xaml.cs to register the push background task.</span></span> <span data-ttu-id="444a8-130">Ajoutez la ligne de code ci-après à la fin de la méthode `OnLaunched()` :</span><span class="sxs-lookup"><span data-stu-id="444a8-130">Add the following line of code at the end of the `OnLaunched()` method:</span></span>
   
        RegisterBackgroundTask();
2. <span data-ttu-id="444a8-131">Toujours dans App.xaml.cs, ajoutez le code ci-dessous juste après la méthode `OnLaunched()` :</span><span class="sxs-lookup"><span data-stu-id="444a8-131">Still in App.xaml.cs, add the following code immediately after the `OnLaunched()` method:</span></span>
   
        private async void RegisterBackgroundTask()
        {
            if (!Windows.ApplicationModel.Background.BackgroundTaskRegistration.AllTasks.Any(i => i.Value.Name == "PushBackgroundTask"))
            {
                var result = await BackgroundExecutionManager.RequestAccessAsync();
                var builder = new BackgroundTaskBuilder();
   
                builder.Name = "PushBackgroundTask";
                builder.TaskEntryPoint = typeof(PushBackgroundComponent.PushBackgroundTask).FullName;
                builder.SetTrigger(new Windows.ApplicationModel.Background.PushNotificationTrigger());
                BackgroundTaskRegistration task = builder.Register();
            }
        }
3. <span data-ttu-id="444a8-132">Ajoutez les instructions `using` suivantes au début du fichier App.xaml.cs :</span><span class="sxs-lookup"><span data-stu-id="444a8-132">Add the following `using` statements at the top of the App.xaml.cs file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. <span data-ttu-id="444a8-133">Dans Visual Studio, dans le menu **Fichier**, cliquez sur **Enregistrer tout**.</span><span class="sxs-lookup"><span data-stu-id="444a8-133">From the **File** menu in Visual Studio, click **Save All**.</span></span>

## <a name="create-the-push-background-component"></a><span data-ttu-id="444a8-134">Création du composant en arrière-plan pour les notifications Push</span><span class="sxs-lookup"><span data-stu-id="444a8-134">Create the Push Background Component</span></span>
<span data-ttu-id="444a8-135">L’étape suivante consiste à créer le composant en arrière-plan pour les notifications Push.</span><span class="sxs-lookup"><span data-stu-id="444a8-135">The next step is to create the push background component.</span></span>

1. <span data-ttu-id="444a8-136">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le nœud de niveau supérieur de la solution (**Solution SecurePush** dans le cas présent). Cliquez ensuite sur **Ajouter**, puis sur **Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="444a8-136">In Solution Explorer, right-click the top-level node of the solution (**Solution SecurePush** in this case), then click **Add**, then click **New Project**.</span></span>
2. <span data-ttu-id="444a8-137">Développez **Applications du Windows Store** et cliquez sur **Applications Windows Phone**, puis sur **Composant Windows Runtime (Windows Phone)**.</span><span class="sxs-lookup"><span data-stu-id="444a8-137">Expand **Store Apps**, then click **Windows Phone Apps**, then click **Windows Runtime Component (Windows Phone)**.</span></span> <span data-ttu-id="444a8-138">Nommez le projet **PushBackgroundComponent**, puis cliquez sur **OK** pour créer le projet.</span><span class="sxs-lookup"><span data-stu-id="444a8-138">Name the project **PushBackgroundComponent**, and then click **OK** to create the project.</span></span>
   
    ![][12]
3. <span data-ttu-id="444a8-139">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **PushBackgroundComponent (Windows Phone 8.1)**. Cliquez ensuite sur **Ajouter**, puis sur **Classe**.</span><span class="sxs-lookup"><span data-stu-id="444a8-139">In Solution Explorer, right-click the **PushBackgroundComponent (Windows Phone 8.1)** project, then click **Add**, then click **Class**.</span></span> <span data-ttu-id="444a8-140">Nommez la nouvelle classe **PushBackgroundTask.cs**.</span><span class="sxs-lookup"><span data-stu-id="444a8-140">Name the new class **PushBackgroundTask.cs**.</span></span> <span data-ttu-id="444a8-141">Cliquez sur **Ajouter** pour générer la classe.</span><span class="sxs-lookup"><span data-stu-id="444a8-141">Click **Add** to generate the class.</span></span>
4. <span data-ttu-id="444a8-142">Remplacez l’ensemble du contenu de la définition de l’espace de noms **PushBackgroundComponent** par le code ci-après en remplaçant l’espace réservé `{back-end endpoint}` par le point de terminaison du serveur principal obtenu lors du déploiement de votre serveur principal :</span><span class="sxs-lookup"><span data-stu-id="444a8-142">Replace the entire contents of the **PushBackgroundComponent** namespace definition with the following code, substituting the placeholder `{back-end endpoint}` with the back-end endpoint obtained while deploying your back-end:</span></span>
   
        public sealed class Notification
            {
                public int Id { get; set; }
                public string Payload { get; set; }
                public bool Read { get; set; }
            }
   
            public sealed class PushBackgroundTask : IBackgroundTask
            {
                private string GET_URL = "{back-end endpoint}/api/notifications/";
   
                async void IBackgroundTask.Run(IBackgroundTaskInstance taskInstance)
                {
                    // Store the content received from the notification so it can be retrieved from the UI.
                    RawNotification raw = (RawNotification)taskInstance.TriggerDetails;
                    var notificationId = raw.Content;
   
                    // retrieve content
                    BackgroundTaskDeferral deferral = taskInstance.GetDeferral();
                    var httpClient = new HttpClient();
                    var settings = ApplicationData.Current.LocalSettings.Values;
                    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                    var notificationString = await httpClient.GetStringAsync(GET_URL + notificationId);
   
                    var notification = JsonConvert.DeserializeObject<Notification>(notificationString);
   
                    ShowToast(notification);
   
                    deferral.Complete();
                }
   
                private void ShowToast(Notification notification)
                {
                    ToastTemplateType toastTemplate = ToastTemplateType.ToastText01;
                    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(toastTemplate);
                    XmlNodeList toastTextElements = toastXml.GetElementsByTagName("text");
                    toastTextElements[0].AppendChild(toastXml.CreateTextNode(notification.Payload));
                    ToastNotification toast = new ToastNotification(toastXml);
                    ToastNotificationManager.CreateToastNotifier().Show(toast);
                }
            }
5. <span data-ttu-id="444a8-143">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **PushBackgroundComponent (Windows Phone 8.1)**, puis cliquez sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="444a8-143">In Solution Explorer, right-click the **PushBackgroundComponent (Windows Phone 8.1)** project and then click **Manage NuGet Packages**.</span></span>
6. <span data-ttu-id="444a8-144">Dans la partie gauche, cliquez sur **En ligne**.</span><span class="sxs-lookup"><span data-stu-id="444a8-144">On the left-hand side, click **Online**.</span></span>
7. <span data-ttu-id="444a8-145">Dans la zone **Rechercher**, entrez **Client Http**.</span><span class="sxs-lookup"><span data-stu-id="444a8-145">In the **Search** box, type **Http Client**.</span></span>
8. <span data-ttu-id="444a8-146">Dans la liste de résultats, cliquez sur **Bibliothèques clientes HTTP Microsoft**, puis cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="444a8-146">In the results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="444a8-147">Terminez l'installation.</span><span class="sxs-lookup"><span data-stu-id="444a8-147">Complete the installation.</span></span>
9. <span data-ttu-id="444a8-148">De retour dans la zone **Recherche** NuGet, tapez **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="444a8-148">Back in the NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="444a8-149">Installez le package **Json.NET** , puis fermez la fenêtre du Gestionnaire de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="444a8-149">Install the **Json.NET** package, then close the NuGet Package Manager window.</span></span>
10. <span data-ttu-id="444a8-150">Ajoutez les instructions `using` suivantes au début du fichier **PushBackgroundTask.cs** :</span><span class="sxs-lookup"><span data-stu-id="444a8-150">Add the following `using` statements at the top of the **PushBackgroundTask.cs** file:</span></span>
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. <span data-ttu-id="444a8-151">Dans l’Explorateur de solutions, dans le projet **NotifyUserWindowsPhone (Windows Phone 8.1)**, cliquez avec le bouton droit sur **Références**, puis cliquez sur **Ajouter une référence...**.</span><span class="sxs-lookup"><span data-stu-id="444a8-151">In Solution Explorer, in the **NotifyUserWindowsPhone (Windows Phone 8.1)** project, right-click **References**, then click **Add Reference...**.</span></span> <span data-ttu-id="444a8-152">Dans la boîte de dialogue Gestionnaire de références, cochez la case en regard de **PushBackgroundComponent**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="444a8-152">In the Reference Manager dialog, check the box next to **PushBackgroundComponent**, and then click **OK**.</span></span>
12. <span data-ttu-id="444a8-153">Dans l’Explorateur de solutions, double-cliquez sur **Package.appxmanifest** dans le projet **NotifyUserWindowsPhone (Windows Phone 8.1)**.</span><span class="sxs-lookup"><span data-stu-id="444a8-153">In Solution Explorer, double-click **Package.appxmanifest** in the **NotifyUserWindowsPhone (Windows Phone 8.1)** project.</span></span> <span data-ttu-id="444a8-154">Sous **Notifications**, définissez **Compatible toast** sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="444a8-154">Under **Notifications**, set **Toast Capable** to **Yes**.</span></span>
    
    ![][3]
13. <span data-ttu-id="444a8-155">Toujours dans **Package.appxmanifest**, cliquez en haut sur le menu **Déclarations**.</span><span class="sxs-lookup"><span data-stu-id="444a8-155">Still in **Package.appxmanifest**, click the **Declarations** menu near the top.</span></span> <span data-ttu-id="444a8-156">Dans la liste déroulante **Déclarations disponibles**, cliquez sur **Tâches en arrière-plan**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="444a8-156">In the **Available Declarations** dropdown, click **Background Tasks**, and then click **Add**.</span></span>
14. <span data-ttu-id="444a8-157">Dans **Package.appxmanifest**, sous **Propriétés**, cochez **Notification Push**.</span><span class="sxs-lookup"><span data-stu-id="444a8-157">In **Package.appxmanifest**, under **Properties**, check **Push notification**.</span></span>
15. <span data-ttu-id="444a8-158">Dans **Package.appxmanifest**, sous **Paramètres de l’application**, tapez **PushBackgroundComponent.PushBackgroundTask** dans le champ **Point d’entrée**.</span><span class="sxs-lookup"><span data-stu-id="444a8-158">In **Package.appxmanifest**, under **App Settings**, type **PushBackgroundComponent.PushBackgroundTask** in the **Entry Point** field.</span></span>
    
    ![][13]
16. <span data-ttu-id="444a8-159">Dans le menu **Fichier**, cliquez sur **Enregistrer tout**.</span><span class="sxs-lookup"><span data-stu-id="444a8-159">From the **File** menu, click **Save All**.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="444a8-160">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="444a8-160">Run the Application</span></span>
<span data-ttu-id="444a8-161">Pour exécuter l'application, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="444a8-161">To run the application, do the following:</span></span>

1. <span data-ttu-id="444a8-162">Dans Visual Studio, exécutez l'application d'API web **AppBackend** .</span><span class="sxs-lookup"><span data-stu-id="444a8-162">In Visual Studio, run the **AppBackend** Web API application.</span></span> <span data-ttu-id="444a8-163">Une page web ASP.NET s'affiche.</span><span class="sxs-lookup"><span data-stu-id="444a8-163">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="444a8-164">Dans Visual Studio, exécutez l'application Windows Phone **NotifyUserWindowsPhone (Windows Phone 8.1)** .</span><span class="sxs-lookup"><span data-stu-id="444a8-164">In Visual Studio, run the **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone app.</span></span> <span data-ttu-id="444a8-165">L'émulateur Windows Phone s'exécute et charge l'application automatiquement.</span><span class="sxs-lookup"><span data-stu-id="444a8-165">The Windows Phone emulator runs and loads the app automatically.</span></span>
3. <span data-ttu-id="444a8-166">Dans l'interface utilisateur de l'application **NotifyUserWindowsPhone** , entrez un nom d'utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="444a8-166">In the **NotifyUserWindowsPhone** app UI, enter a username and password.</span></span> <span data-ttu-id="444a8-167">La valeur peut être une chaîne quelconque, mais elle doit être identique pour les deux.</span><span class="sxs-lookup"><span data-stu-id="444a8-167">These can be any string, but they must be the same value.</span></span>
4. <span data-ttu-id="444a8-168">Dans l’interface utilisateur de l’application **NotifyUserWindowsPhone**, cliquez sur **Se connecter et s’inscrire**.</span><span class="sxs-lookup"><span data-stu-id="444a8-168">In the **NotifyUserWindowsPhone** app UI, click **Log in and register**.</span></span> <span data-ttu-id="444a8-169">Cliquez ensuite sur **Send push**.</span><span class="sxs-lookup"><span data-stu-id="444a8-169">Then click **Send push**.</span></span>

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
