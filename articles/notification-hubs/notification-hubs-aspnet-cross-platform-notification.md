---
title: aaaSend inter-plateformes notifications toousers avec Notification Hubs (ASP.NET)
description: "Découvrez comment toosend de modèles de Notification Hubs toouse, dans une requête unique, une notification de plateforme agnostique ciblant toutes les plateformes."
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
ms.openlocfilehash: f105b871b809e739dd5c05ea819ad135e842ebb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cross-platform-notifications-toousers-with-notification-hubs"></a><span data-ttu-id="dbb4c-103">Envoyer toousers inter-plateformes notifications avec Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="dbb4c-103">Send cross-platform notifications toousers with Notification Hubs</span></span>
<span data-ttu-id="dbb4c-104">Dans le cadre du didacticiel précédent hello [avertir les utilisateurs avec des concentrateurs de Notification], vous avez appris comment les appareils tooall toopush notifications inscrit par un utilisateur authentifié spécifique.</span><span class="sxs-lookup"><span data-stu-id="dbb4c-104">In hello previous tutorial [Notify users with Notification Hubs], you learned how toopush notifications tooall devices registered by a specific authenticated user.</span></span> <span data-ttu-id="dbb4c-105">Dans ce didacticiel, plusieurs requêtes ont été toosend requis une plateforme de client de notification tooeach pris en charge.</span><span class="sxs-lookup"><span data-stu-id="dbb4c-105">In that tutorial, multiple requests were required toosend a notification tooeach supported client platform.</span></span> <span data-ttu-id="dbb4c-106">Notification Hubs prend en charge les modèles qui vous permettent de spécifier comment un périphérique spécifique veut tooreceive notifications.</span><span class="sxs-lookup"><span data-stu-id="dbb4c-106">Notification Hubs supports templates, which let you specify how a specific device wants tooreceive notifications.</span></span> <span data-ttu-id="dbb4c-107">Cela simplifie l'envoi de notifications interplateforme.</span><span class="sxs-lookup"><span data-stu-id="dbb4c-107">This simplifies sending cross-platform notifications.</span></span> <span data-ttu-id="dbb4c-108">Cette rubrique montre comment parti tootake de toosend de modèles, dans une requête unique, une notification de plateforme agnostique ciblant toutes les plateformes.</span><span class="sxs-lookup"><span data-stu-id="dbb4c-108">This topic demonstrates how tootake advantage of templates toosend, in a single request, a platform-agnostic notification that targets all platforms.</span></span> <span data-ttu-id="dbb4c-109">Pour plus d’informations sur les modèles, consultez [Vue d’ensemble d’Azure Notification Hubs][Templates].</span><span class="sxs-lookup"><span data-stu-id="dbb4c-109">For more detailed information about templates, see [Azure Notification Hubs Overview][Templates].</span></span>
> [!IMPORTANT]
> <span data-ttu-id="dbb4c-110">Les projets Windows Phone 8.1 et versions antérieures ne sont pas pris en charge dans Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="dbb4c-110">Windows Phone projects 8.1 and earlier are not supported using Visual Studio 2017.</span></span> <span data-ttu-id="dbb4c-111">Pour en savoir plus, consultez [Plateforme cible et compatibilité dans Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="dbb4c-111">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="dbb4c-112">Concentrateurs de notification permet un tooregister appareil plusieurs modèles hello même balise.</span><span class="sxs-lookup"><span data-stu-id="dbb4c-112">Notification Hubs allows a device tooregister multiple templates with hello same tag.</span></span> <span data-ttu-id="dbb4c-113">Dans ce cas, un message entrant de ciblage que balise génère plusieurs notifications remis toohello périphérique, un pour chaque modèle.</span><span class="sxs-lookup"><span data-stu-id="dbb4c-113">In this case, an incoming message targeting that tag results in multiple notifications delivered toohello device, one for each template.</span></span> <span data-ttu-id="dbb4c-114">Cela permet de vous toodisplay hello même message dans plusieurs notifications visual, tels que les deux comme un badge et comme une notification toast dans une application Windows Store.</span><span class="sxs-lookup"><span data-stu-id="dbb4c-114">This enables you toodisplay hello same message in multiple visual notifications, such as both as a badge and as a toast notification in a Windows Store app.</span></span>
> 
> 

<span data-ttu-id="dbb4c-115">Terminer hello suivant notifications étapes toosend inter-plateformes à l’aide de modèles :</span><span class="sxs-lookup"><span data-stu-id="dbb4c-115">Complete hello following steps toosend cross-platform notifications using templates:</span></span>

1. <span data-ttu-id="dbb4c-116">Dans l’Explorateur de solutions dans Visual Studio de hello, développez hello **contrôleurs** dossier, puis fichier RegisterController.cs de hello ouvert.</span><span class="sxs-lookup"><span data-stu-id="dbb4c-116">In hello Solution Explorer in Visual Studio, expand hello **Controllers** folder, then open hello RegisterController.cs file.</span></span>
2. <span data-ttu-id="dbb4c-117">Localisez le bloc hello de code Bonjour **Put** méthode qui crée une inscription remplacer hello `switch` avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="dbb4c-117">Locate hello block of code in hello **Put** method that creates a new registration replace hello `switch` content with hello following code:</span></span>
   
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
   
    <span data-ttu-id="dbb4c-118">Ce code appelle hello spécifique à la plateforme méthode toocreate une inscription de modèle au lieu d’une inscription native.</span><span class="sxs-lookup"><span data-stu-id="dbb4c-118">This code calls hello platform-specific method toocreate a template registration instead of a native registration.</span></span> <span data-ttu-id="dbb4c-119">Les inscriptions existantes n'ont pas besoin d'être modifiées, car les inscriptions de modèle sont dérivées d'inscriptions natives.</span><span class="sxs-lookup"><span data-stu-id="dbb4c-119">Existing registrations need not be modified because template registrations derive from native registrations.</span></span>
3. <span data-ttu-id="dbb4c-120">Bonjour **Notifications** contrôleur, remplacer hello **sendNotification** méthode avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="dbb4c-120">In hello **Notifications** controller, replace hello **sendNotification** method with hello following code:</span></span>
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    <span data-ttu-id="dbb4c-121">Ce code envoie une notification tooall plateformes à hello même temps et sans devoir toospecify une charge utile native.</span><span class="sxs-lookup"><span data-stu-id="dbb4c-121">This code sends a notification tooall platforms at hello same time and without having toospecify a native payload.</span></span> <span data-ttu-id="dbb4c-122">Génère des concentrateurs de notification et remet hello appareil tooevery de charge utile correct avec hello fourni *balise* valeur, comme indiqué dans les modèles de hello inscrit.</span><span class="sxs-lookup"><span data-stu-id="dbb4c-122">Notification Hubs builds and delivers hello correct payload tooevery device with hello provided *tag* value, as specified in hello registered templates.</span></span>
4. <span data-ttu-id="dbb4c-123">Republiez votre projet principal WebApi.</span><span class="sxs-lookup"><span data-stu-id="dbb4c-123">Re-publish your WebApi back-end project.</span></span>
5. <span data-ttu-id="dbb4c-124">Réexécutez l’application cliente de hello et vérifier que l’inscription réussit.</span><span class="sxs-lookup"><span data-stu-id="dbb4c-124">Run hello client app again and verify that registration succeeds.</span></span>
6. <span data-ttu-id="dbb4c-125">(Facultatif) Deuxième appareil hello client application tooa de déployer, puis exécuter l’application hello.</span><span class="sxs-lookup"><span data-stu-id="dbb4c-125">(Optional) Deploy hello client app tooa second device, then run hello app.</span></span>
   
    <span data-ttu-id="dbb4c-126">À noter qu'une notification s'affiche sur chaque appareil.</span><span class="sxs-lookup"><span data-stu-id="dbb4c-126">Note that a notification is displayed on each device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dbb4c-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dbb4c-127">Next Steps</span></span>
<span data-ttu-id="dbb4c-128">Maintenant que vous avez terminé ce didacticiel, vous trouverez des informations supplémentaires sur Notification Hubs et les modèles dans les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="dbb4c-128">Now that you have completed this tutorial, find out more about Notification Hubs and templates in these topics:</span></span>

* <span data-ttu-id="dbb4c-129">**[Utilisez toosend concentrateurs de Notification dernières actualités]**</span><span class="sxs-lookup"><span data-stu-id="dbb4c-129">**[Use Notification Hubs toosend breaking news]**</span></span> <br/><span data-ttu-id="dbb4c-130">Présente un autre scénario d'utilisation des modèles.</span><span class="sxs-lookup"><span data-stu-id="dbb4c-130">Demonstrates another scenario for using templates</span></span>
* <span data-ttu-id="dbb4c-131">**[Vue d’ensemble d’Azure Notification Hubs][Templates]**</span><span class="sxs-lookup"><span data-stu-id="dbb4c-131">**[Azure Notification Hubs Overview][Templates]**</span></span><br/><span data-ttu-id="dbb4c-132">Rubrique générale offrant des informations plus détaillées sur les modèles.</span><span class="sxs-lookup"><span data-stu-id="dbb4c-132">Overview topic has more detailed information on templates.</span></span>

<!-- Anchors. -->

<!-- Images. -->




<!-- URLs. -->
[Push toousers ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Push toousers Mobile Services]: /manage/services/notification-hubs/notify-users/
[Visual Studio 2012 Express for Windows 8]: http://go.microsoft.com/fwlink/?LinkId=257546

[Utilisez toosend concentrateurs de Notification dernières actualités]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[Azure Notification Hubs]: http://go.microsoft.com/fwlink/p/?LinkId=314257
[avertir les utilisateurs avec des concentrateurs de Notification]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Templates]: http://go.microsoft.com/fwlink/p/?LinkId=317339
[Notification Hub How toofor Windows Store]: http://msdn.microsoft.com/library/windowsazure/jj927172.aspx
