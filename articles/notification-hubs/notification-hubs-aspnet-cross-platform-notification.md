---
title: Envoi de notifications interplateformes aux utilisateurs avec Notification Hubs (ASP.NET)
description: "Découvrez comment utiliser des modèles Notification Hubs pour envoyer, dans une même demande, une notification indépendante de la plateforme qui cible toutes les plateformes."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 11d2131b-f683-47fd-a691-4cdfc696f62b
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: ef971fcfe68978ea9ce0810c69efbe134bb15f8a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="send-cross-platform-notifications-to-users-with-notification-hubs"></a><span data-ttu-id="4191e-103">Envoi de notifications interplateforme aux utilisateurs avec Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="4191e-103">Send cross-platform notifications to users with Notification Hubs</span></span>
<span data-ttu-id="4191e-104">Dans le didacticiel précédent [Notification des utilisateurs avec Notification Hubs], vous avez appris à envoyer des notifications Push à tous les appareils inscrits par un utilisateur authentifié.</span><span class="sxs-lookup"><span data-stu-id="4191e-104">In the previous tutorial [Notify users with Notification Hubs], you learned how to push notifications to all devices registered by a specific authenticated user.</span></span> <span data-ttu-id="4191e-105">Dans ce didacticiel, l'envoi d'une notification à chaque plateforme cliente prise en charge nécessitait plusieurs demandes.</span><span class="sxs-lookup"><span data-stu-id="4191e-105">In that tutorial, multiple requests were required to send a notification to each supported client platform.</span></span> <span data-ttu-id="4191e-106">Notification Hubs prend en charge des modèles qui permettent de spécifier le mode de réception préféré d'un appareil déterminé.</span><span class="sxs-lookup"><span data-stu-id="4191e-106">Notification Hubs supports templates, which let you specify how a specific device wants to receive notifications.</span></span> <span data-ttu-id="4191e-107">Cela simplifie l'envoi de notifications interplateforme.</span><span class="sxs-lookup"><span data-stu-id="4191e-107">This simplifies sending cross-platform notifications.</span></span> <span data-ttu-id="4191e-108">Cette rubrique montre comment exploiter les modèles pour envoyer, dans une même demande, une notification qui cible toutes les plateformes, quelles qu’elles soient.</span><span class="sxs-lookup"><span data-stu-id="4191e-108">This topic demonstrates how to take advantage of templates to send, in a single request, a platform-agnostic notification that targets all platforms.</span></span> <span data-ttu-id="4191e-109">Pour plus d’informations sur les modèles, consultez [Vue d’ensemble d’Azure Notification Hubs][Templates].</span><span class="sxs-lookup"><span data-stu-id="4191e-109">For more detailed information about templates, see [Azure Notification Hubs Overview][Templates].</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4191e-110">Les projets Windows Phone 8.1 et versions antérieures ne sont pas pris en charge dans Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="4191e-110">Windows Phone projects 8.1 and earlier are not supported using Visual Studio 2017.</span></span> <span data-ttu-id="4191e-111">Pour en savoir plus, consultez [Plateforme cible et compatibilité dans Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="4191e-111">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="4191e-112">Notification Hubs permet à un appareil d’inscrire plusieurs modèles avec la même balise.</span><span class="sxs-lookup"><span data-stu-id="4191e-112">Notification Hubs allows a device to register multiple templates with the same tag.</span></span> <span data-ttu-id="4191e-113">Dans ce cas, un message entrant ciblant cette balise déclenche l'envoi de plusieurs notifications à destination de l'appareil, une pour chaque modèle.</span><span class="sxs-lookup"><span data-stu-id="4191e-113">In this case, an incoming message targeting that tag results in multiple notifications delivered to the device, one for each template.</span></span> <span data-ttu-id="4191e-114">Cela vous permet d'afficher le même message dans plusieurs notifications visuelles, par exemple, sous la forme d'un badge et d'une notification toast dans une application Windows Store.</span><span class="sxs-lookup"><span data-stu-id="4191e-114">This enables you to display the same message in multiple visual notifications, such as both as a badge and as a toast notification in a Windows Store app.</span></span>
> 
> 

<span data-ttu-id="4191e-115">Pour envoyer des notifications interplateforme à l'aide de modèles, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4191e-115">Complete the following steps to send cross-platform notifications using templates:</span></span>

1. <span data-ttu-id="4191e-116">Dans l'Explorateur de solutions de Visual Studio, développez le dossier **Controllers** , puis ouvrez le fichier RegisterController.cs.</span><span class="sxs-lookup"><span data-stu-id="4191e-116">In the Solution Explorer in Visual Studio, expand the **Controllers** folder, then open the RegisterController.cs file.</span></span>
2. <span data-ttu-id="4191e-117">Recherchez le bloc de code dans la méthode **Put** qui crée une inscription. Remplacez le contenu de `switch` par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="4191e-117">Locate the block of code in the **Put** method that creates a new registration replace the `switch` content with the following code:</span></span>
   
        switch (deviceUpdate.Platform)
        {
            case "mpns":
                var toastTemplate = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>$(message)</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
                registration = new MpnsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "wns":
                toastTemplate = @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(message)</text></binding></visual></toast>";
                registration = new WindowsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "apns":
                var alertTemplate = "{\"aps\":{\"alert\":\"$(message)\"}}";
                registration = new AppleTemplateRegistrationDescription(deviceUpdate.Handle, alertTemplate);
                break;
            case "gcm":
                var messageTemplate = "{\"data\":{\"message\":\"$(message)\"}}";
                registration = new GcmTemplateRegistrationDescription(deviceUpdate.Handle, messageTemplate);
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }
   
    <span data-ttu-id="4191e-118">Ce code permet d’appeler la méthode propre à la plateforme pour créer une inscription de modèle et non une inscription native.</span><span class="sxs-lookup"><span data-stu-id="4191e-118">This code calls the platform-specific method to create a template registration instead of a native registration.</span></span> <span data-ttu-id="4191e-119">Les inscriptions existantes n'ont pas besoin d'être modifiées, car les inscriptions de modèle sont dérivées d'inscriptions natives.</span><span class="sxs-lookup"><span data-stu-id="4191e-119">Existing registrations need not be modified because template registrations derive from native registrations.</span></span>
3. <span data-ttu-id="4191e-120">Dans le contrôleur **Notifications**, remplacez la méthode **sendNotification** par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="4191e-120">In the **Notifications** controller, replace the **sendNotification** method with the following code:</span></span>
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    <span data-ttu-id="4191e-121">Ce code permet d'envoyer une notification à toutes les plateformes à la fois et sans avoir à spécifier de charge utile native.</span><span class="sxs-lookup"><span data-stu-id="4191e-121">This code sends a notification to all platforms at the same time and without having to specify a native payload.</span></span> <span data-ttu-id="4191e-122">Notification Hubs génère et remet la charge utile appropriée à chaque appareil avec la valeur de *balise* fournie, comme spécifié dans les modèles inscrits.</span><span class="sxs-lookup"><span data-stu-id="4191e-122">Notification Hubs builds and delivers the correct payload to every device with the provided *tag* value, as specified in the registered templates.</span></span>
4. <span data-ttu-id="4191e-123">Republiez votre projet principal WebApi.</span><span class="sxs-lookup"><span data-stu-id="4191e-123">Re-publish your WebApi back-end project.</span></span>
5. <span data-ttu-id="4191e-124">Réexécutez l'application cliente et vérifiez la réussite de l'inscription.</span><span class="sxs-lookup"><span data-stu-id="4191e-124">Run the client app again and verify that registration succeeds.</span></span>
6. <span data-ttu-id="4191e-125">(Facultatif) Déployez l'application cliente sur un deuxième appareil, puis exécutez l'application.</span><span class="sxs-lookup"><span data-stu-id="4191e-125">(Optional) Deploy the client app to a second device, then run the app.</span></span>
   
    <span data-ttu-id="4191e-126">À noter qu'une notification s'affiche sur chaque appareil.</span><span class="sxs-lookup"><span data-stu-id="4191e-126">Note that a notification is displayed on each device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4191e-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4191e-127">Next Steps</span></span>
<span data-ttu-id="4191e-128">Maintenant que vous avez terminé ce didacticiel, vous trouverez des informations supplémentaires sur Notification Hubs et les modèles dans les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="4191e-128">Now that you have completed this tutorial, find out more about Notification Hubs and templates in these topics:</span></span>

* <span data-ttu-id="4191e-129">**[Utilisation des Notification Hubs pour diffuser les dernières nouvelles]**</span><span class="sxs-lookup"><span data-stu-id="4191e-129">**[Use Notification Hubs to send breaking news]**</span></span> <br/><span data-ttu-id="4191e-130">Présente un autre scénario d'utilisation des modèles.</span><span class="sxs-lookup"><span data-stu-id="4191e-130">Demonstrates another scenario for using templates</span></span>
* <span data-ttu-id="4191e-131">**[Vue d’ensemble d’Azure Notification Hubs][Templates]**</span><span class="sxs-lookup"><span data-stu-id="4191e-131">**[Azure Notification Hubs Overview][Templates]**</span></span><br/><span data-ttu-id="4191e-132">Rubrique générale offrant des informations plus détaillées sur les modèles.</span><span class="sxs-lookup"><span data-stu-id="4191e-132">Overview topic has more detailed information on templates.</span></span>

<!-- Anchors. -->

<!-- Images. -->




<!-- URLs. -->
[Push to users ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Push to users Mobile Services]: /manage/services/notification-hubs/notify-users/
[Visual Studio 2012 Express for Windows 8]: http://go.microsoft.com/fwlink/?LinkId=257546

<span data-ttu-id="4191e-133">[Utilisation des Notification Hubs pour diffuser les dernières nouvelles]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="4191e-133">[Use Notification Hubs to send breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>
[Azure Notification Hubs]: http://go.microsoft.com/fwlink/p/?LinkId=314257
<span data-ttu-id="4191e-134">[Notification des utilisateurs avec Notification Hubs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="4191e-134">[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
[Templates]: http://go.microsoft.com/fwlink/p/?LinkId=317339
[Notification Hub How to for Windows Store]: http://msdn.microsoft.com/library/windowsazure/jj927172.aspx
