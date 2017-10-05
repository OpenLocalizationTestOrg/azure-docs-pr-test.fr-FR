---
title: Gestion des inscriptions
description: "Cette rubrique explique comment inscrire des appareils auprès des hubs de notification en vue de recevoir des notifications Push."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: fd0ee230-132c-4143-b4f9-65cef7f463a1
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: a1a349150ef4c7837932706f0c4fcc8d022ec7ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="registration-management"></a><span data-ttu-id="d620f-103">Gestion des inscriptions</span><span class="sxs-lookup"><span data-stu-id="d620f-103">Registration management</span></span>
## <a name="overview"></a><span data-ttu-id="d620f-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="d620f-104">Overview</span></span>
<span data-ttu-id="d620f-105">Cette rubrique explique comment inscrire des appareils auprès des hubs de notification en vue de recevoir des notifications Push.</span><span class="sxs-lookup"><span data-stu-id="d620f-105">This topic explains how to register devices with notification hubs in order to receive push notifications.</span></span> <span data-ttu-id="d620f-106">Elle donne une description générale des inscriptions, puis présente les deux principaux modes d’inscription des appareils : l’inscription de l’appareil directement auprès du hub de notification et l’inscription via un serveur principal d’application.</span><span class="sxs-lookup"><span data-stu-id="d620f-106">The topic describes registrations at a high level, then introduces the two main patterns for registering devices: registering from the device directly to the notification hub, and registering through an application backend.</span></span> 

## <a name="what-is-device-registration"></a><span data-ttu-id="d620f-107">Présentation de l’inscription d’un appareil</span><span class="sxs-lookup"><span data-stu-id="d620f-107">What is device registration</span></span>
<span data-ttu-id="d620f-108">L’inscription d’un appareil auprès d’un hub de notification s’effectue à l’aide d’une **inscription** ou d’une **installation**.</span><span class="sxs-lookup"><span data-stu-id="d620f-108">Device registration with a Notification Hub is accomplished using a **Registration** or **Installation**.</span></span>

#### <a name="registrations"></a><span data-ttu-id="d620f-109">Inscriptions</span><span class="sxs-lookup"><span data-stu-id="d620f-109">Registrations</span></span>
<span data-ttu-id="d620f-110">Une inscription associe le handle PNS (Platform Notification Service, service de notification de plateforme) à des balises et éventuellement à un modèle.</span><span class="sxs-lookup"><span data-stu-id="d620f-110">A registration associates the Platform Notification Service (PNS) handle for a device with tags and possibly a template.</span></span> <span data-ttu-id="d620f-111">Le handle PNS peut être un ChannelURI, un jeton d’appareil ou un ID d’inscription GCM.</span><span class="sxs-lookup"><span data-stu-id="d620f-111">The PNS handle could be a ChannelURI, device token, or GCM registration id.</span></span> <span data-ttu-id="d620f-112">Les balises permettent d’acheminer des notifications vers l’ensemble approprié de handles d’appareils.</span><span class="sxs-lookup"><span data-stu-id="d620f-112">Tags are used to route notifications to the correct set of device handles.</span></span> <span data-ttu-id="d620f-113">Pour plus d’informations, consultez [Routage et expressions de balises](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="d620f-113">For more information, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span> <span data-ttu-id="d620f-114">Les modèles permettent d’implémenter la transformation par inscription.</span><span class="sxs-lookup"><span data-stu-id="d620f-114">Templates are used to implement per-registration transformation.</span></span> <span data-ttu-id="d620f-115">Pour plus d’informations, consultez [Modèles](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="d620f-115">For more information, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>

#### <a name="installations"></a><span data-ttu-id="d620f-116">Installations</span><span class="sxs-lookup"><span data-stu-id="d620f-116">Installations</span></span>
<span data-ttu-id="d620f-117">Une installation est une inscription améliorée qui inclut un conteneur de propriétés associées à des opérations push.</span><span class="sxs-lookup"><span data-stu-id="d620f-117">An Installation is an enhanced registration that includes a bag of push related properties.</span></span> <span data-ttu-id="d620f-118">C’est la meilleure approche, et la plus récente, pour inscrire vos appareils.</span><span class="sxs-lookup"><span data-stu-id="d620f-118">It is the latest and best approach to registering your devices.</span></span> <span data-ttu-id="d620f-119">Toutefois, elle n’est actuellement pas prise en charge par le Kit de développement logiciel .NET côté client ([SDK Notification Hub pour les opérations de serveur principal](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)).</span><span class="sxs-lookup"><span data-stu-id="d620f-119">However, it is not supported by client side .NET SDK ([Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) as of yet.</span></span>  <span data-ttu-id="d620f-120">Cela signifie que si vous vous inscrivez à partir de l'appareil client lui-même, vous devrez utiliser l’approche [API REST Notification Hubs](https://msdn.microsoft.com/library/mt621153.aspx) pour prendre en charge ces installations.</span><span class="sxs-lookup"><span data-stu-id="d620f-120">This means if you are registering from the client device itself, you would have to use the [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx) approach to support installations.</span></span> <span data-ttu-id="d620f-121">Si vous utilisez un service principal, vous devriez être en mesure d'utiliser [SDK Notification Hub pour les opérations de serveur principal](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="d620f-121">If you are using a backend service, you should be able to use [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="d620f-122">Voici certains avantages essentiels que présente l’utilisation d’installations :</span><span class="sxs-lookup"><span data-stu-id="d620f-122">The following are some key advantages to using installations:</span></span>

* <span data-ttu-id="d620f-123">La création ou la mise à jour d’une installation est entièrement idempotente.</span><span class="sxs-lookup"><span data-stu-id="d620f-123">Creating or updating an installation is fully idempotent.</span></span> <span data-ttu-id="d620f-124">Vous pouvez donc la retenter sans vous soucier des inscriptions en double.</span><span class="sxs-lookup"><span data-stu-id="d620f-124">So you can retry it without any concerns about duplicate registrations.</span></span>
* <span data-ttu-id="d620f-125">Le modèle Installation facilite les opérations push individuelles, ciblant des appareils spécifiques.</span><span class="sxs-lookup"><span data-stu-id="d620f-125">The installation model makes it easy to do individual pushes - targeting specific device.</span></span> <span data-ttu-id="d620f-126">Une balise système **« $InstallationId:[installationId] »** est ajoutée automatiquement avec chaque inscription basée sur l’installation.</span><span class="sxs-lookup"><span data-stu-id="d620f-126">A system tag **"$InstallationId:[installationId]"** is automatically added with each installation based registration.</span></span> <span data-ttu-id="d620f-127">Vous pouvez donc appeler un envoi à cette balise pour cibler un appareil spécifique sans avoir à effectuer aucun codage supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="d620f-127">So you can call a send to this tag to target a specific device without having to do any additional coding.</span></span>
* <span data-ttu-id="d620f-128">L’utilisation d’installations vous permet également d’effectuer des mises à jour partielles d’inscriptions.</span><span class="sxs-lookup"><span data-stu-id="d620f-128">Using installations also enables you to do partial registration updates.</span></span> <span data-ttu-id="d620f-129">La mise à jour partielle d’une installation est demandée avec une méthode PATCH utilisant la [norme JSON-Patch](https://tools.ietf.org/html/rfc6902).</span><span class="sxs-lookup"><span data-stu-id="d620f-129">The partial update of an installation is requested with a PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902).</span></span> <span data-ttu-id="d620f-130">Cela est particulièrement utile lorsque vous voulez mettre à jour des balises sur l’inscription.</span><span class="sxs-lookup"><span data-stu-id="d620f-130">This is particularly useful when you want to update tags on the registration.</span></span> <span data-ttu-id="d620f-131">Il n’est pas nécessaire de retirer la totalité de l’inscription et de renvoyer à nouveau toutes les balises précédentes.</span><span class="sxs-lookup"><span data-stu-id="d620f-131">You don't have to pull down the entire registration and then resend all the previous tags again.</span></span>

<span data-ttu-id="d620f-132">Une installation peut contenir les propriétés suivantes : </span><span class="sxs-lookup"><span data-stu-id="d620f-132">An installation can contain the the following properties.</span></span> <span data-ttu-id="d620f-133">Pour obtenir la liste complète des propriétés d’installation, consultez [Créer ou remplacer une installation avec l’API REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) ou [Propriétés d’installation](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx).</span><span class="sxs-lookup"><span data-stu-id="d620f-133">For a complete listing of the installation properties see, [Create or Overwrite an Installation with REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) or [Installation Properties](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) for the .</span></span>

    // Example installation format to show some supported properties
    {
        installationId: "",
        expirationTime: "",
        tags: [],
        platform: "",
        pushChannel: "",
        ………
        templates: {
            "templateName1" : {
                body: "",
                tags: [] },
            "templateName2" : {
                body: "",
                // Headers are for Windows Store only
                headers: {
                    "X-WNS-Type": "wns/tile" }
                tags: [] }
        },
        secondaryTiles: {
            "tileId1": {
                pushChannel: "",
                tags: [],
                templates: {
                    "otherTemplate": {
                        bodyTemplate: "",
                        headers: {
                            ... }
                        tags: [] }
                }
            }
        }
    }



<span data-ttu-id="d620f-134">Il est important de noter que les inscriptions et les installations par défaut n'expirent plus.</span><span class="sxs-lookup"><span data-stu-id="d620f-134">It is important to note that registrations and installations by default no longer expire.</span></span>

<span data-ttu-id="d620f-135">Les inscriptions et les installations doivent contenir un handle PNS valide pour chaque appareil/canal.</span><span class="sxs-lookup"><span data-stu-id="d620f-135">Registrations and installations must contain a valid PNS handle for each device/channel.</span></span> <span data-ttu-id="d620f-136">Comme les handles PNS peuvent être obtenus uniquement dans une application cliente sur l’appareil, l’une des méthodes consiste à effectuer l’inscription directement sur cet appareil avec l’application cliente.</span><span class="sxs-lookup"><span data-stu-id="d620f-136">Because PNS handles can only be obtained in a client app on the device, one pattern is to register directly on that device with the client app.</span></span> <span data-ttu-id="d620f-137">D’un autre côté, les considérations sur la sécurité et la logique métier associée aux balises impliquent que vous devez gérer l’inscription des appareils dans le serveur principal de l’application.</span><span class="sxs-lookup"><span data-stu-id="d620f-137">On the other hand, security considerations and business logic related to tags might require you to manage device registration in the app back-end.</span></span> 

#### <a name="templates"></a><span data-ttu-id="d620f-138">Modèles</span><span class="sxs-lookup"><span data-stu-id="d620f-138">Templates</span></span>
<span data-ttu-id="d620f-139">Si vous voulez utiliser des [modèles](notification-hubs-templates-cross-platform-push-messages.md), l’installation de l’appareil contient également tous les modèles associés à cet appareil au format JSON (voir l’exemple ci-dessus).</span><span class="sxs-lookup"><span data-stu-id="d620f-139">If you want to use [Templates](notification-hubs-templates-cross-platform-push-messages.md), the device installation also hold all templates associated with that device in a JSON format (see sample above).</span></span> <span data-ttu-id="d620f-140">Les noms de modèles permettent de cibler différents modèles pour le même appareil.</span><span class="sxs-lookup"><span data-stu-id="d620f-140">The template names help target different templates for the same device.</span></span>

<span data-ttu-id="d620f-141">Notez que le nom de chaque modèle mappe à un corps de modèle et à un ensemble de balises en option.</span><span class="sxs-lookup"><span data-stu-id="d620f-141">Note that each template name maps to a template body and an optional set of tags.</span></span> <span data-ttu-id="d620f-142">De plus, chaque plateforme peut avoir des propriétés de modèle supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="d620f-142">Moreover, each platform can have additional template properties.</span></span> <span data-ttu-id="d620f-143">Dans le cas de Windows Store (via WNS) et de Windows Phone 8 (à l’aide de MPNS), un ensemble supplémentaire d’en-têtes peut faire partie du modèle.</span><span class="sxs-lookup"><span data-stu-id="d620f-143">For Windows Store (using WNS) and Windows Phone 8 (using MPNS), an additional set of headers can be part of the template.</span></span> <span data-ttu-id="d620f-144">Dans le cas d’APNs, vous pouvez définir une propriété d’expiration sur une constante ou une expression de modèle.</span><span class="sxs-lookup"><span data-stu-id="d620f-144">In the case of APNs, you can set an expiry property to either a constant or to a template expression.</span></span> <span data-ttu-id="d620f-145">Pour obtenir la liste complète des propriétés d’installation, consultez [Créer ou remplacer une installation avec REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d620f-145">For a complete listing of the installation properties see, [Create or Overwrite an Installation with REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) topic.</span></span>

#### <a name="secondary-tiles-for-windows-store-apps"></a><span data-ttu-id="d620f-146">Vignettes secondaires pour les applications Windows Store</span><span class="sxs-lookup"><span data-stu-id="d620f-146">Secondary Tiles for Windows Store Apps</span></span>
<span data-ttu-id="d620f-147">Pour les applications clientes Windows Store, le fait d’envoyer des notifications à des vignettes secondaires revient à les envoyer à la vignette principale.</span><span class="sxs-lookup"><span data-stu-id="d620f-147">For Windows Store client applications, sending notifications to secondary tiles is the same as sending them to the primary one.</span></span> <span data-ttu-id="d620f-148">Ce comportement est également pris en charge dans les installations.</span><span class="sxs-lookup"><span data-stu-id="d620f-148">This is also supported in installations.</span></span> <span data-ttu-id="d620f-149">Notez que les vignettes secondaires ont un ChannelUri différent, ce que le Kit de développement logiciel (SDK) sur votre application cliente gère en toute transparence.</span><span class="sxs-lookup"><span data-stu-id="d620f-149">Note that secondary tiles have a different ChannelUri, which the SDK on your client app handles transparently.</span></span>

<span data-ttu-id="d620f-150">Le dictionnaire SecondaryTiles utilise le même paramètre TileId que celui qui permet de créer l’objet SecondaryTiles dans votre application Windows Store.</span><span class="sxs-lookup"><span data-stu-id="d620f-150">The SecondaryTiles dictionary uses the same TileId that is used to create the SecondaryTiles object in your Windows Store app.</span></span>
<span data-ttu-id="d620f-151">Comme pour le paramètre principal ChannelUri, le paramètre ChannelUris des vignettes secondaires peut changer à tout moment.</span><span class="sxs-lookup"><span data-stu-id="d620f-151">As with the primary ChannelUri, ChannelUris of secondary tiles can change at any moment.</span></span> <span data-ttu-id="d620f-152">Afin de garder à jour les inscriptions dans le hub de notification, l’appareil doit les actualiser avec le paramètre ChannelUris actuel des vignettes secondaires.</span><span class="sxs-lookup"><span data-stu-id="d620f-152">In order to keep the installations in the notification hub updated, the device must refresh them with the current ChannelUris of the secondary tiles.</span></span>

## <a name="registration-management-from-the-device"></a><span data-ttu-id="d620f-153">Gestion de l’inscription à partir de l’appareil</span><span class="sxs-lookup"><span data-stu-id="d620f-153">Registration management from the device</span></span>
<span data-ttu-id="d620f-154">Lors de la gestion de l’inscription d’un appareil à partir des applications clientes, le serveur principal est uniquement chargé d’envoyer des notifications.</span><span class="sxs-lookup"><span data-stu-id="d620f-154">When managing device registration from client apps, the backend is only responsible for sending notifications.</span></span> <span data-ttu-id="d620f-155">Les applications clientes conservent les handles PNS à jour et inscrivent les balises.</span><span class="sxs-lookup"><span data-stu-id="d620f-155">Client apps keep PNS handles up to date, and register tags.</span></span> <span data-ttu-id="d620f-156">L’image suivante illustre ce modèle :</span><span class="sxs-lookup"><span data-stu-id="d620f-156">The following picture illustrates this pattern.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

<span data-ttu-id="d620f-157">L’appareil extrait d’abord le handle PNS du PNS, puis s’inscrit directement auprès du hub de notification.</span><span class="sxs-lookup"><span data-stu-id="d620f-157">The device first retrieves the PNS handle from the PNS, then registers with the notification hub directly.</span></span> <span data-ttu-id="d620f-158">Une fois l’inscription effectuée, le serveur principal de l’application peut envoyer une notification ciblant cette inscription.</span><span class="sxs-lookup"><span data-stu-id="d620f-158">After the registration is successful, the app backend can send a notification targeting that registration.</span></span> <span data-ttu-id="d620f-159">Pour plus d’informations sur l’envoi de notifications, consultez [Routage et expressions de balises](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="d620f-159">For more information about how to send notifications, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>
<span data-ttu-id="d620f-160">Notez que, dans ce cas, vous utiliserez les droits Listen (Écouter) pour accéder à vos hubs de notification à partir de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="d620f-160">Note that in this case, you will use only Listen rights to access your notification hubs from the device.</span></span> <span data-ttu-id="d620f-161">Pour plus d’informations, consultez [Sécurité](notification-hubs-push-notification-security.md).</span><span class="sxs-lookup"><span data-stu-id="d620f-161">For more information, see [Security](notification-hubs-push-notification-security.md).</span></span>

<span data-ttu-id="d620f-162">L’inscription à partir de l’appareil est la méthode la plus simple, mais présente quelques inconvénients.</span><span class="sxs-lookup"><span data-stu-id="d620f-162">Registering from the device is the simplest method, but it has some drawbacks.</span></span>
<span data-ttu-id="d620f-163">Le premier inconvénient est qu’une application cliente peut mettre à jour ses balises uniquement lorsqu’elle est active.</span><span class="sxs-lookup"><span data-stu-id="d620f-163">The first drawback is that a client app can only update its tags when the app is active.</span></span> <span data-ttu-id="d620f-164">Par exemple, si un utilisateur a deux appareils qui inscrivent des balises associées à des équipes sportives, lorsque le premier appareil inscrit une balise supplémentaire (par exemple, Seahawks), le second appareil ne reçoit pas les notifications concernant les Seahawks tant que l’application présente sur le second appareil n’a pas été exécutée une deuxième fois.</span><span class="sxs-lookup"><span data-stu-id="d620f-164">For example, if a user has two devices that register tags related to sport teams, when the first device registers for an additional tag (for example, Seahawks), the second device will not receive the notifications about the Seahawks until the app on the second device is executed a second time.</span></span> <span data-ttu-id="d620f-165">De manière plus générale, lorsque les balises sont affectées par plusieurs appareils, la gestion des balises à partir du serveur principal est une option intéressante.</span><span class="sxs-lookup"><span data-stu-id="d620f-165">More generally, when tags are affected by multiple devices, managing tags from the backend is a desirable option.</span></span>
<span data-ttu-id="d620f-166">Le second inconvénient de la gestion des inscriptions à partir de l’application cliente réside dans le fait qu’étant donné que les applications peuvent être piratées, la limitation de l’inscription à des balises spécifiques nécessite de prendre des précautions supplémentaires, comme décrit dans la section « Sécurité au niveau des balises ».</span><span class="sxs-lookup"><span data-stu-id="d620f-166">The second drawback of registration management from the client app is that, since apps can be hacked, securing the registration to specific tags requires extra care, as explained in the section “Tag-level security.”</span></span>

#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-an-installation"></a><span data-ttu-id="d620f-167">Exemple de code permettant de s’inscrire auprès d’un hub de notification à partir d’un appareil à l’aide d’une installation</span><span class="sxs-lookup"><span data-stu-id="d620f-167">Example code to register with a notification hub from a device using an installation</span></span>
<span data-ttu-id="d620f-168">Pour l’instant, il n’est pris en charge qu’à l’aide de l’ [API REST Notification Hubs](https://msdn.microsoft.com/library/mt621153.aspx).</span><span class="sxs-lookup"><span data-stu-id="d620f-168">At this time, this is only supported using the [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx).</span></span>

<span data-ttu-id="d620f-169">Vous pouvez également utiliser la méthode PATCH utilisant la [norme JSON-Patch](https://tools.ietf.org/html/rfc6902) pour la mise à jour de l’installation.</span><span class="sxs-lookup"><span data-stu-id="d620f-169">You can also use the PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating the installation.</span></span>

    class DeviceInstallation
    {
        public string installationId { get; set; }
        public string platform { get; set; }
        public string pushChannel { get; set; }
        public string[] tags { get; set; }
    }

    private async Task<HttpStatusCode> CreateOrUpdateInstallationAsync(DeviceInstallation deviceInstallation,
         string hubName, string listenConnectionString)
    {
        if (deviceInstallation.installationId == null)
            return HttpStatusCode.BadRequest;

        // Parse connection string (https://msdn.microsoft.com/library/azure/dn495627.aspx)
        ConnectionStringUtility connectionSaSUtil = new ConnectionStringUtility(listenConnectionString);
        string hubResource = "installations/" + deviceInstallation.installationId + "?";
        string apiVersion = "api-version=2015-04";

        // Determine the targetUri that we will sign
        string uri = connectionSaSUtil.Endpoint + hubName + "/" + hubResource + apiVersion;

        //=== Generate SaS Security Token for Authorization header ===
        // See, https://msdn.microsoft.com/library/azure/dn495627.aspx
        string SasToken = connectionSaSUtil.getSaSToken(uri, 60);

        using (var httpClient = new HttpClient())
        {
            string json = JsonConvert.SerializeObject(deviceInstallation);

            httpClient.DefaultRequestHeaders.Add("Authorization", SasToken);

            var response = await httpClient.PutAsync(uri, new StringContent(json, System.Text.Encoding.UTF8, "application/json"));
            return response.StatusCode;
        }
    }

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    string installationId = null;
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a installation id in application data, create and store as application data.
    if (!settings.ContainsKey("__NHInstallationId"))
    {
        installationId = Guid.NewGuid().ToString();
        settings.Add("__NHInstallationId", installationId);
    }

    installationId = (string)settings["__NHInstallationId"];

    var deviceInstallation = new DeviceInstallation
    {
        installationId = installationId,
        platform = "wns",
        pushChannel = channel.Uri,
        //tags = tags.ToArray<string>()
    };

    var statusCode = await CreateOrUpdateInstallationAsync(deviceInstallation, 
                        "<HUBNAME>", "<SHARED LISTEN CONNECTION STRING>");

    if (statusCode != HttpStatusCode.Accepted)
    {
        var dialog = new MessageDialog(statusCode.ToString(), "Registration failed. Installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
    else
    {
        var dialog = new MessageDialog("Registration successful using installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }



#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-a-registration"></a><span data-ttu-id="d620f-170">Exemple de code permettant de s’inscrire auprès d’un hub de notification à partir d’un appareil à l’aide d’une inscription</span><span class="sxs-lookup"><span data-stu-id="d620f-170">Example code to register with a notification hub from a device using a registration</span></span>
<span data-ttu-id="d620f-171">Ces méthodes créent ou mettent à jour une inscription de l’appareil sur lequel elles sont appelées.</span><span class="sxs-lookup"><span data-stu-id="d620f-171">These methods create or update a registration for the device on which they are called.</span></span> <span data-ttu-id="d620f-172">Cela signifie que pour mettre à jour le handle ou les balises, vous devez remplacer la totalité de l’inscription.</span><span class="sxs-lookup"><span data-stu-id="d620f-172">This means that in order to update the handle or the tags, you must overwrite the entire registration.</span></span> <span data-ttu-id="d620f-173">Sachez que les inscriptions sont temporaires, et que vous devez donc toujours disposer d’un stockage fiable avec les balises actuelles dont a besoin un appareil spécifique.</span><span class="sxs-lookup"><span data-stu-id="d620f-173">Remember that registrations are transient, so you should always have a reliable store with the current tags that a specific device needs.</span></span>

    // Initialize the Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // The Device id from the PNS
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // If you are registering from the client itself, then store this registration id in device
    // storage. Then when the app starts, you can check if a registration id already exists or not before
    // creating.
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a registration id in application data, store in application data.
    if (!settings.ContainsKey("__NHRegistrationId"))
    {
        // make sure there are no existing registrations for this push handle (used for iOS and Android)    
        string newRegistrationId = null;
        var registrations = await hub.GetRegistrationsByChannelAsync(pushChannel.Uri, 100);
        foreach (RegistrationDescription registration in registrations)
        {
            if (newRegistrationId == null)
            {
                newRegistrationId = registration.RegistrationId;
            }
            else
            {
                await hub.DeleteRegistrationAsync(registration);
            }
        }

        newRegistrationId = await hub.CreateRegistrationIdAsync();

        settings.Add("__NHRegistrationId", newRegistrationId);
    }

    string regId = (string)settings["__NHRegistrationId"];

    RegistrationDescription registration = new WindowsRegistrationDescription(pushChannel.Uri);
    registration.RegistrationId = regId;
    registration.Tags = new HashSet<string>(YourTags);

    try
    {
        await hub.CreateOrUpdateRegistrationAsync(registration);
    }
    catch (Microsoft.WindowsAzure.Messaging.RegistrationGoneException e)
    {
        settings.Remove("__NHRegistrationId");
    }


## <a name="registration-management-from-a-backend"></a><span data-ttu-id="d620f-174">Gestion des inscriptions à partir d’un serveur principal</span><span class="sxs-lookup"><span data-stu-id="d620f-174">Registration management from a backend</span></span>
<span data-ttu-id="d620f-175">La gestion des inscriptions à partir du serveur principal nécessite l’écriture de code supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="d620f-175">Managing registrations from the backend requires writing additional code.</span></span> <span data-ttu-id="d620f-176">L’application de l’appareil doit fournir le handle PNS mis à jour au serveur principal à chaque démarrage de l’application (avec les balises et les modèles), et le serveur principal doit mettre à jour ce handle sur le hub de notification.</span><span class="sxs-lookup"><span data-stu-id="d620f-176">The app from the device must provide the updated PNS handle to the backend every time the app starts (along with tags and templates), and the backend must update this handle on the notification hub.</span></span> <span data-ttu-id="d620f-177">L’image suivante illustre cette conception :</span><span class="sxs-lookup"><span data-stu-id="d620f-177">The following picture illustrates this design.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

<span data-ttu-id="d620f-178">Les avantages de la gestion des inscriptions à partir du serveur principal incluent la possibilité de modifier les balises aux inscriptions, même lorsque l’application correspondante est inactive sur l’appareil, et d’authentifier l’application cliente avant d’ajouter une balise à son inscription.</span><span class="sxs-lookup"><span data-stu-id="d620f-178">The advantages of managing registrations from the backend include the ability to modify tags to registrations even when the corresponding app on the device is inactive, and to authenticate the client app before adding a tag to its registration.</span></span>

#### <a name="example-code-to-register-with-a-notification-hub-from-a-backend-using-an-installation"></a><span data-ttu-id="d620f-179">Exemple de code permettant de s’inscrire auprès d’un hub de notification à partir d’un serveur principal à l’aide d’une installation</span><span class="sxs-lookup"><span data-stu-id="d620f-179">Example code to register with a notification hub from a backend using an installation</span></span>
<span data-ttu-id="d620f-180">L’appareil client obtient toujours son handle PNS et les propriétés d’installation pertinentes comme auparavant et appelle une API personnalisée sur le serveur principal qui peut effectuer l’inscription, autoriser les balises, etc. Le serveur principal peut tirer parti du [SDK Notification Hubs pour les opérations de serveur principal](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="d620f-180">The client device still gets its PNS handle and relevant installation properties as before and calls a custom API on the backend that can perform the registration and authorize tags etc. The backend can leverage the [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="d620f-181">Vous pouvez également utiliser la méthode PATCH utilisant la [norme JSON-Patch](https://tools.ietf.org/html/rfc6902) pour la mise à jour de l’installation.</span><span class="sxs-lookup"><span data-stu-id="d620f-181">You can also use the PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating the installation.</span></span>

    // Initialize the Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // Custom API on the backend
    public async Task<HttpResponseMessage> Put(DeviceInstallation deviceUpdate)
    {

        Installation installation = new Installation();
        installation.InstallationId = deviceUpdate.InstallationId;
        installation.PushChannel = deviceUpdate.Handle;
        installation.Tags = deviceUpdate.Tags;

        switch (deviceUpdate.Platform)
        {
            case "mpns":
                installation.Platform = NotificationPlatform.Mpns;
                break;
            case "wns":
                installation.Platform = NotificationPlatform.Wns;
                break;
            case "apns":
                installation.Platform = NotificationPlatform.Apns;
                break;
            case "gcm":
                installation.Platform = NotificationPlatform.Gcm;
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }


        // In the backend we can control if a user is allowed to add tags
        //installation.Tags = new List<string>(deviceUpdate.Tags);
        //installation.Tags.Add("username:" + username);

        await hub.CreateOrUpdateInstallationAsync(installation);

        return Request.CreateResponse(HttpStatusCode.OK);
    }


#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-a-registration-id"></a><span data-ttu-id="d620f-182">Exemple de code permettant de s’inscrire auprès d’un hub de notification à partir d’un appareil à l’aide d’un ID d’inscription</span><span class="sxs-lookup"><span data-stu-id="d620f-182">Example code to register with a notification hub from a device using a registration id</span></span>
<span data-ttu-id="d620f-183">À partir de votre serveur principal d’application, vous pouvez effectuer les opérations CRUD de base sur les inscriptions.</span><span class="sxs-lookup"><span data-stu-id="d620f-183">From your app backend, you can perform basic CRUDS operations on registrations.</span></span> <span data-ttu-id="d620f-184">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d620f-184">For example:</span></span>

    var hub = NotificationHubClient.CreateClientFromConnectionString("{connectionString}", "hubName");

    // create a registration description object of the correct type, e.g.
    var reg = new WindowsRegistrationDescription(channelUri, tags);

    // Create
    await hub.CreateRegistrationAsync(reg);

    // Get by id
    var r = await hub.GetRegistrationAsync<RegistrationDescription>("id");

    // update
    r.Tags.Add("myTag");

    // update on hub
    await hub.UpdateRegistrationAsync(r);

    // delete
    await hub.DeleteRegistrationAsync(r);


<span data-ttu-id="d620f-185">Le serveur principal doit gérer l’accès concurrentiel entre les mises à jour des inscriptions.</span><span class="sxs-lookup"><span data-stu-id="d620f-185">The backend must handle concurrency between registration updates.</span></span> <span data-ttu-id="d620f-186">Service Bus offre un contrôle de l’accès concurrentiel optimiste pour la gestion des inscriptions.</span><span class="sxs-lookup"><span data-stu-id="d620f-186">Service Bus offers optimistic concurrency control for registration management.</span></span> <span data-ttu-id="d620f-187">Au niveau HTTP, cette implémentation est effectuée à l’aide d’ETag lors des opérations de gestion des inscriptions.</span><span class="sxs-lookup"><span data-stu-id="d620f-187">At the HTTP level, this is implemented with the use of ETag on registration management operations.</span></span> <span data-ttu-id="d620f-188">Cette fonctionnalité est utilisée de manière transparente dans les Kits de développement logiciel (SDK) Microsoft, lesquels lèvent une exception si une mise à jour est refusée en raison d’accès concurrentiel.</span><span class="sxs-lookup"><span data-stu-id="d620f-188">This feature is transparently used by Microsoft SDKs, which throw an exception if an update is rejected for concurrency reasons.</span></span> <span data-ttu-id="d620f-189">Le serveur principal d’application est chargé de gérer ces exceptions et, le cas échéant, de tenter une nouvelle mise à jour.</span><span class="sxs-lookup"><span data-stu-id="d620f-189">The app backend is responsible for handling these exceptions and retrying the update if required.</span></span>

