---
title: aaaAzure Notification Hubs Secure Push.
description: "Découvrez comment toosend sécurisée des notifications push dans Azure. Exemples de code écrits en c# à l’aide des API .NET de hello."
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
ms.openlocfilehash: b6fe16c96d28d75ff698278409fb012472ba6396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="ff022-104">Notifications Push sécurisées avec Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="ff022-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ff022-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="ff022-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="ff022-106">iOS</span><span class="sxs-lookup"><span data-stu-id="ff022-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="ff022-107">Android</span><span class="sxs-lookup"><span data-stu-id="ff022-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="ff022-108">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ff022-108">Overview</span></span>
<span data-ttu-id="ff022-109">Prise en charge des notifications push dans Microsoft Azure vous permet de tooaccess une infrastructure push facile à utiliser, multiplateforme, à grande échelle, ce qui simplifie considérablement l’implémentation hello de notifications push pour les applications consommateur et d’entreprise mobile plateformes.</span><span class="sxs-lookup"><span data-stu-id="ff022-109">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="ff022-110">En raison de contraintes de sécurité ou tooregulatory, une application peut parfois tooinclude quelque chose dans la notification hello ne peut pas être transmis au moyen de l’infrastructure de notification push standard hello.</span><span class="sxs-lookup"><span data-stu-id="ff022-110">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="ff022-111">Ce didacticiel explique comment tooachieve hello la même expérience en envoyant des informations sensibles via une connexion sécurisée, authentifiée entre le périphérique de hello client et serveur principal d’application hello.</span><span class="sxs-lookup"><span data-stu-id="ff022-111">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client device and hello app backend.</span></span>

<span data-ttu-id="ff022-112">À un niveau élevé, les flux hello sont comme suit :</span><span class="sxs-lookup"><span data-stu-id="ff022-112">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="ff022-113">Hello serveur principal d’application :</span><span class="sxs-lookup"><span data-stu-id="ff022-113">hello app back-end:</span></span>
   * <span data-ttu-id="ff022-114">stocke la charge utile sécurisée dans la base de données principale ;</span><span class="sxs-lookup"><span data-stu-id="ff022-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="ff022-115">Envoie un ID hello de cet appareil toohello de notification (aucune information sécurisée est envoyée).</span><span class="sxs-lookup"><span data-stu-id="ff022-115">Sends hello ID of this notification toohello device (no secure information is sent).</span></span>
2. <span data-ttu-id="ff022-116">application Hello sur périphérique hello, lors de la réception de notification de hello :</span><span class="sxs-lookup"><span data-stu-id="ff022-116">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="ff022-117">Appareil de Hello contacte hello principal demande hello sécurisé charge utile.</span><span class="sxs-lookup"><span data-stu-id="ff022-117">hello device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="ff022-118">application Hello peut afficher la charge utile de hello en tant que notification sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="ff022-118">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="ff022-119">Il est important de toonote que Bonjour précédant le flux (et, dans ce didacticiel), nous supposons que cet appareil hello stocke un jeton d’authentification dans le stockage local, une fois hello utilisateur se connecte.</span><span class="sxs-lookup"><span data-stu-id="ff022-119">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="ff022-120">Cela garantit une expérience entièrement transparente, comme périphérique de hello peut récupérer de données de la notification hello sécurisé à l’aide de ce jeton.</span><span class="sxs-lookup"><span data-stu-id="ff022-120">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="ff022-121">Si votre application n’enregistre pas les jetons d’authentification sur l’appareil de hello, ou si ces jetons peuvent avoir expiré, hello application d’appareil, à la réception de notification de hello doit afficher une notification générique invitant hello utilisateur toolaunch hello application.</span><span class="sxs-lookup"><span data-stu-id="ff022-121">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="ff022-122">application Hello puis authentifie l’utilisateur de hello et montre la charge utile de notification hello.</span><span class="sxs-lookup"><span data-stu-id="ff022-122">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="ff022-123">Ce didacticiel de Push de sécuriser montre comment toosend une notification push en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="ff022-123">This Secure Push tutorial shows how toosend a push notification securely.</span></span> <span data-ttu-id="ff022-124">didacticiel de Hello s’appuie sur hello [avertir les utilisateurs](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) (didacticiel), donc vous devez effectuer les étapes de hello tout d’abord dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ff022-124">hello tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, so you should complete hello steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="ff022-125">Ce didacticiel part du principe que vous avez créé et configuré votre hub de notification comme décrit dans [Prise en main de Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="ff022-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span></span>
> <span data-ttu-id="ff022-126">Notez également que Windows Phone 8.1 nécessite des informations d’identification Windows (pas Windows Phone) et que les tâches en arrière-plan ne fonctionnent pas sur Windows Phone 8.0 ou Silverlight 8.1.</span><span class="sxs-lookup"><span data-stu-id="ff022-126">Also, note that Windows Phone 8.1 requires Windows (not Windows Phone) credentials, and that background tasks do not work on Windows Phone 8.0 or Silverlight 8.1.</span></span> <span data-ttu-id="ff022-127">Pour les applications du Windows Store, vous pouvez recevoir des notifications via une tâche en arrière-plan uniquement si l’application hello est activé d’écran de verrouillage (cliquez sur la case à cocher hello Bonjour Appmanifest).</span><span class="sxs-lookup"><span data-stu-id="ff022-127">For Windows Store applications, you can receive notifications via a background task only if hello app is lock-screen enabled (click hello checkbox in hello Appmanifest).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-windows-phone-project"></a><span data-ttu-id="ff022-128">Modifier hello projet du Windows Phone</span><span class="sxs-lookup"><span data-stu-id="ff022-128">Modify hello Windows Phone Project</span></span>
1. <span data-ttu-id="ff022-129">Bonjour **NotifyUserWindowsPhone** de projet, ajoutez hello suivant la tâche en arrière-plan de la poussée du code tooApp.xaml.cs tooregister hello.</span><span class="sxs-lookup"><span data-stu-id="ff022-129">In hello **NotifyUserWindowsPhone** project, add hello following code tooApp.xaml.cs tooregister hello push background task.</span></span> <span data-ttu-id="ff022-130">Ajouter hello suivant la ligne de code à fin hello Hello `OnLaunched()` méthode :</span><span class="sxs-lookup"><span data-stu-id="ff022-130">Add hello following line of code at hello end of hello `OnLaunched()` method:</span></span>
   
        RegisterBackgroundTask();
2. <span data-ttu-id="ff022-131">Toujours dans App.xaml.cs, ajoutez hello suivant code immédiatement après hello `OnLaunched()` méthode :</span><span class="sxs-lookup"><span data-stu-id="ff022-131">Still in App.xaml.cs, add hello following code immediately after hello `OnLaunched()` method:</span></span>
   
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
3. <span data-ttu-id="ff022-132">Ajoutez hello suit `using` instructions haut hello du fichier de App.xaml.cs hello :</span><span class="sxs-lookup"><span data-stu-id="ff022-132">Add hello following `using` statements at hello top of hello App.xaml.cs file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. <span data-ttu-id="ff022-133">À partir de hello **fichier** menu dans Visual Studio, cliquez sur **Enregistrer tout**.</span><span class="sxs-lookup"><span data-stu-id="ff022-133">From hello **File** menu in Visual Studio, click **Save All**.</span></span>

## <a name="create-hello-push-background-component"></a><span data-ttu-id="ff022-134">Créer hello pousser le composant en arrière-plan</span><span class="sxs-lookup"><span data-stu-id="ff022-134">Create hello Push Background Component</span></span>
<span data-ttu-id="ff022-135">étape suivante de Hello est le composant toocreate hello par émission de données en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="ff022-135">hello next step is toocreate hello push background component.</span></span>

1. <span data-ttu-id="ff022-136">Dans l’Explorateur de solutions, cliquez sur nœud de niveau supérieur hello de solution de hello (**Solution SecurePush** dans ce cas), puis cliquez sur **ajouter**, puis cliquez sur **nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="ff022-136">In Solution Explorer, right-click hello top-level node of hello solution (**Solution SecurePush** in this case), then click **Add**, then click **New Project**.</span></span>
2. <span data-ttu-id="ff022-137">Développez **Applications du Windows Store** et cliquez sur **Applications Windows Phone**, puis sur **Composant Windows Runtime (Windows Phone)**.</span><span class="sxs-lookup"><span data-stu-id="ff022-137">Expand **Store Apps**, then click **Windows Phone Apps**, then click **Windows Runtime Component (Windows Phone)**.</span></span> <span data-ttu-id="ff022-138">Projet de hello nom **PushBackgroundComponent**, puis cliquez sur **OK** projet hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="ff022-138">Name hello project **PushBackgroundComponent**, and then click **OK** toocreate hello project.</span></span>
   
    ![][12]
3. <span data-ttu-id="ff022-139">Dans l’Explorateur de solutions, cliquez sur hello **PushBackgroundComponent (8.1 de Windows Phone)** de projet, puis cliquez sur **ajouter**, puis cliquez sur **classe**.</span><span class="sxs-lookup"><span data-stu-id="ff022-139">In Solution Explorer, right-click hello **PushBackgroundComponent (Windows Phone 8.1)** project, then click **Add**, then click **Class**.</span></span> <span data-ttu-id="ff022-140">Nommez la nouvelle classe de hello **PushBackgroundTask.cs**.</span><span class="sxs-lookup"><span data-stu-id="ff022-140">Name hello new class **PushBackgroundTask.cs**.</span></span> <span data-ttu-id="ff022-141">Cliquez sur **ajouter** classe hello de toogenerate.</span><span class="sxs-lookup"><span data-stu-id="ff022-141">Click **Add** toogenerate hello class.</span></span>
4. <span data-ttu-id="ff022-142">Remplacez hello tout contenu de hello **PushBackgroundComponent** définition d’espace de noms avec hello suivant de code, en remplaçant les espaces réservés de hello `{back-end endpoint}` avec point de terminaison principal hello obtenue lors du déploiement de votre principal :</span><span class="sxs-lookup"><span data-stu-id="ff022-142">Replace hello entire contents of hello **PushBackgroundComponent** namespace definition with hello following code, substituting hello placeholder `{back-end endpoint}` with hello back-end endpoint obtained while deploying your back-end:</span></span>
   
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
                    // Store hello content received from hello notification so it can be retrieved from hello UI.
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
5. <span data-ttu-id="ff022-143">Dans l’Explorateur de solutions, cliquez sur hello **PushBackgroundComponent (8.1 de Windows Phone)** de projet, puis cliquez sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ff022-143">In Solution Explorer, right-click hello **PushBackgroundComponent (Windows Phone 8.1)** project and then click **Manage NuGet Packages**.</span></span>
6. <span data-ttu-id="ff022-144">Dans la partie gauche hello, cliquez sur **Online**.</span><span class="sxs-lookup"><span data-stu-id="ff022-144">On hello left-hand side, click **Online**.</span></span>
7. <span data-ttu-id="ff022-145">Bonjour **recherche** , tapez **Http Client**.</span><span class="sxs-lookup"><span data-stu-id="ff022-145">In hello **Search** box, type **Http Client**.</span></span>
8. <span data-ttu-id="ff022-146">Dans la liste des résultats hello, cliquez sur **Microsoft HTTP Client Libraries**, puis cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="ff022-146">In hello results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="ff022-147">Terminer l’installation de hello.</span><span class="sxs-lookup"><span data-stu-id="ff022-147">Complete hello installation.</span></span>
9. <span data-ttu-id="ff022-148">Dans hello NuGet **recherche** , tapez **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="ff022-148">Back in hello NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="ff022-149">Installer hello **Json.NET** package, puis sur fenêtre du Gestionnaire de Package NuGet hello fermer.</span><span class="sxs-lookup"><span data-stu-id="ff022-149">Install hello **Json.NET** package, then close hello NuGet Package Manager window.</span></span>
10. <span data-ttu-id="ff022-150">Ajoutez hello suivant `using` instructions haut hello hello **PushBackgroundTask.cs** fichier :</span><span class="sxs-lookup"><span data-stu-id="ff022-150">Add hello following `using` statements at hello top of hello **PushBackgroundTask.cs** file:</span></span>
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. <span data-ttu-id="ff022-151">Dans l’Explorateur de solutions, Bonjour **NotifyUserWindowsPhone (8.1 de Windows Phone)** de projet, cliquez sur **références**, puis cliquez sur **ajouter une référence...** . Dans la boîte de dialogue Gestionnaire de références hello, hello case à cocher ensuite trop**PushBackgroundComponent**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ff022-151">In Solution Explorer, in hello **NotifyUserWindowsPhone (Windows Phone 8.1)** project, right-click **References**, then click **Add Reference...**. In hello Reference Manager dialog, check hello box next too**PushBackgroundComponent**, and then click **OK**.</span></span>
12. <span data-ttu-id="ff022-152">Dans l’Explorateur de solutions, double-cliquez sur **Package.appxmanifest** Bonjour **NotifyUserWindowsPhone (8.1 de Windows Phone)** projet.</span><span class="sxs-lookup"><span data-stu-id="ff022-152">In Solution Explorer, double-click **Package.appxmanifest** in hello **NotifyUserWindowsPhone (Windows Phone 8.1)** project.</span></span> <span data-ttu-id="ff022-153">Sous **Notifications**, définissez **compatible Toast** trop**Oui**.</span><span class="sxs-lookup"><span data-stu-id="ff022-153">Under **Notifications**, set **Toast Capable** too**Yes**.</span></span>
    
    ![][3]
13. <span data-ttu-id="ff022-154">Toujours dans **Package.appxmanifest**, cliquez sur hello **déclarations** menu haut hello.</span><span class="sxs-lookup"><span data-stu-id="ff022-154">Still in **Package.appxmanifest**, click hello **Declarations** menu near hello top.</span></span> <span data-ttu-id="ff022-155">Bonjour **déclarations disponibles** liste déroulante, cliquez sur **les tâches en arrière-plan**, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ff022-155">In hello **Available Declarations** dropdown, click **Background Tasks**, and then click **Add**.</span></span>
14. <span data-ttu-id="ff022-156">Dans **Package.appxmanifest**, sous **Propriétés**, cochez **Notification Push**.</span><span class="sxs-lookup"><span data-stu-id="ff022-156">In **Package.appxmanifest**, under **Properties**, check **Push notification**.</span></span>
15. <span data-ttu-id="ff022-157">Dans **Package.appxmanifest**, sous **paramètres de l’application**, type **PushBackgroundComponent.PushBackgroundTask** Bonjour **Point d’entrée** champ.</span><span class="sxs-lookup"><span data-stu-id="ff022-157">In **Package.appxmanifest**, under **App Settings**, type **PushBackgroundComponent.PushBackgroundTask** in hello **Entry Point** field.</span></span>
    
    ![][13]
16. <span data-ttu-id="ff022-158">À partir de hello **fichier** menu, cliquez sur **Enregistrer tout**.</span><span class="sxs-lookup"><span data-stu-id="ff022-158">From hello **File** menu, click **Save All**.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="ff022-159">Exécutez hello Application</span><span class="sxs-lookup"><span data-stu-id="ff022-159">Run hello Application</span></span>
<span data-ttu-id="ff022-160">toorun hello application, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="ff022-160">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="ff022-161">Dans Visual Studio, exécutez hello **AppBackend** application d’API Web.</span><span class="sxs-lookup"><span data-stu-id="ff022-161">In Visual Studio, run hello **AppBackend** Web API application.</span></span> <span data-ttu-id="ff022-162">Une page web ASP.NET s'affiche.</span><span class="sxs-lookup"><span data-stu-id="ff022-162">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="ff022-163">Dans Visual Studio, exécutez hello **NotifyUserWindowsPhone (8.1 de Windows Phone)** application du Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="ff022-163">In Visual Studio, run hello **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone app.</span></span> <span data-ttu-id="ff022-164">émulateur Windows Phone de Hello s’exécute et charge application hello automatiquement.</span><span class="sxs-lookup"><span data-stu-id="ff022-164">hello Windows Phone emulator runs and loads hello app automatically.</span></span>
3. <span data-ttu-id="ff022-165">Bonjour **NotifyUserWindowsPhone** application d’interface utilisateur, entrez un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="ff022-165">In hello **NotifyUserWindowsPhone** app UI, enter a username and password.</span></span> <span data-ttu-id="ff022-166">Il peuvent être n’importe quelle chaîne, mais ils doivent être hello la même valeur.</span><span class="sxs-lookup"><span data-stu-id="ff022-166">These can be any string, but they must be hello same value.</span></span>
4. <span data-ttu-id="ff022-167">Bonjour **NotifyUserWindowsPhone** application d’interface utilisateur, cliquez sur **connectez-vous et inscrivez**.</span><span class="sxs-lookup"><span data-stu-id="ff022-167">In hello **NotifyUserWindowsPhone** app UI, click **Log in and register**.</span></span> <span data-ttu-id="ff022-168">Cliquez ensuite sur **Send push**.</span><span class="sxs-lookup"><span data-stu-id="ff022-168">Then click **Send push**.</span></span>

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
