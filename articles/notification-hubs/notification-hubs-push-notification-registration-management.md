---
title: aaaRegistration gestion
description: "Cette rubrique explique comment tooregister les appareils avec des concentrateurs de notification dans l’ordre tooreceive des notifications push."
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
ms.openlocfilehash: 76471a45c7a0da1614ceed82b73cdb3319979ff7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="registration-management"></a><span data-ttu-id="581e7-103">Gestion des inscriptions</span><span class="sxs-lookup"><span data-stu-id="581e7-103">Registration management</span></span>
## <a name="overview"></a><span data-ttu-id="581e7-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="581e7-104">Overview</span></span>
<span data-ttu-id="581e7-105">Cette rubrique explique comment tooregister les appareils avec des concentrateurs de notification dans l’ordre tooreceive des notifications push.</span><span class="sxs-lookup"><span data-stu-id="581e7-105">This topic explains how tooregister devices with notification hubs in order tooreceive push notifications.</span></span> <span data-ttu-id="581e7-106">rubrique de Hello décrit les enregistrements à un niveau élevé, puis présente des modèles de hello deux principales pour l’inscription des appareils : l’inscription à partir de l’appareil de hello directement le hub de notification toohello et l’inscription via un serveur principal d’application.</span><span class="sxs-lookup"><span data-stu-id="581e7-106">hello topic describes registrations at a high level, then introduces hello two main patterns for registering devices: registering from hello device directly toohello notification hub, and registering through an application backend.</span></span> 

## <a name="what-is-device-registration"></a><span data-ttu-id="581e7-107">Présentation de l’inscription d’un appareil</span><span class="sxs-lookup"><span data-stu-id="581e7-107">What is device registration</span></span>
<span data-ttu-id="581e7-108">L’inscription d’un appareil auprès d’un hub de notification s’effectue à l’aide d’une **inscription** ou d’une **installation**.</span><span class="sxs-lookup"><span data-stu-id="581e7-108">Device registration with a Notification Hub is accomplished using a **Registration** or **Installation**.</span></span>

#### <a name="registrations"></a><span data-ttu-id="581e7-109">Inscriptions</span><span class="sxs-lookup"><span data-stu-id="581e7-109">Registrations</span></span>
<span data-ttu-id="581e7-110">Une inscription associe hello plateforme Notification Service (PNS) gérer pour un périphérique avec balises et éventuellement un modèle.</span><span class="sxs-lookup"><span data-stu-id="581e7-110">A registration associates hello Platform Notification Service (PNS) handle for a device with tags and possibly a template.</span></span> <span data-ttu-id="581e7-111">Hello PNS handle peut être un ChannelURI, jeton de périphérique ou l’id d’inscription GCM. Les balises sont des notifications de tooroute utilisés ensemble correct de toohello de handles du périphérique.</span><span class="sxs-lookup"><span data-stu-id="581e7-111">hello PNS handle could be a ChannelURI, device token, or GCM registration id. Tags are used tooroute notifications toohello correct set of device handles.</span></span> <span data-ttu-id="581e7-112">Pour plus d’informations, consultez [Routage et expressions de balises](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="581e7-112">For more information, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span> <span data-ttu-id="581e7-113">Les modèles sont utilisés tooimplement par inscription transformation.</span><span class="sxs-lookup"><span data-stu-id="581e7-113">Templates are used tooimplement per-registration transformation.</span></span> <span data-ttu-id="581e7-114">Pour plus d’informations, consultez [Modèles](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="581e7-114">For more information, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>

#### <a name="installations"></a><span data-ttu-id="581e7-115">Installations</span><span class="sxs-lookup"><span data-stu-id="581e7-115">Installations</span></span>
<span data-ttu-id="581e7-116">Une installation est une inscription améliorée qui inclut un conteneur de propriétés associées à des opérations push.</span><span class="sxs-lookup"><span data-stu-id="581e7-116">An Installation is an enhanced registration that includes a bag of push related properties.</span></span> <span data-ttu-id="581e7-117">Il s’agit de hello meilleure approche tooregistering vos appareils.</span><span class="sxs-lookup"><span data-stu-id="581e7-117">It is hello latest and best approach tooregistering your devices.</span></span> <span data-ttu-id="581e7-118">Toutefois, elle n’est actuellement pas prise en charge par le Kit de développement logiciel .NET côté client ([SDK Notification Hub pour les opérations de serveur principal](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)).</span><span class="sxs-lookup"><span data-stu-id="581e7-118">However, it is not supported by client side .NET SDK ([Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) as of yet.</span></span>  <span data-ttu-id="581e7-119">Cela signifie que si l’inscription d’appareil client de hello lui-même, vous devriez toouse hello [API REST de concentrateurs de Notification](https://msdn.microsoft.com/library/mt621153.aspx) approche toosupport installations.</span><span class="sxs-lookup"><span data-stu-id="581e7-119">This means if you are registering from hello client device itself, you would have toouse hello [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx) approach toosupport installations.</span></span> <span data-ttu-id="581e7-120">Si vous utilisez un service principal, vous devez être en mesure de toouse [SDK de concentrateur de Notification pour les opérations de serveur principal](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="581e7-120">If you are using a backend service, you should be able toouse [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="581e7-121">Hello Voici certaines installations de toousing avantages clés :</span><span class="sxs-lookup"><span data-stu-id="581e7-121">hello following are some key advantages toousing installations:</span></span>

* <span data-ttu-id="581e7-122">La création ou la mise à jour d’une installation est entièrement idempotente.</span><span class="sxs-lookup"><span data-stu-id="581e7-122">Creating or updating an installation is fully idempotent.</span></span> <span data-ttu-id="581e7-123">Vous pouvez donc la retenter sans vous soucier des inscriptions en double.</span><span class="sxs-lookup"><span data-stu-id="581e7-123">So you can retry it without any concerns about duplicate registrations.</span></span>
* <span data-ttu-id="581e7-124">modèle d’installation Hello facilite toodo facile de push individuels - ciblage des appareils spécifiques.</span><span class="sxs-lookup"><span data-stu-id="581e7-124">hello installation model makes it easy toodo individual pushes - targeting specific device.</span></span> <span data-ttu-id="581e7-125">Une balise système **« $InstallationId:[installationId] »** est ajoutée automatiquement avec chaque inscription basée sur l’installation.</span><span class="sxs-lookup"><span data-stu-id="581e7-125">A system tag **"$InstallationId:[installationId]"** is automatically added with each installation based registration.</span></span> <span data-ttu-id="581e7-126">Par conséquent, vous pouvez appeler un tootarget de balise toothis envoyer un périphérique spécifique sans avoir à toodo de codage supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="581e7-126">So you can call a send toothis tag tootarget a specific device without having toodo any additional coding.</span></span>
* <span data-ttu-id="581e7-127">L’utilisation des installations permet également de mises à jour partielles d’inscription toodo vous.</span><span class="sxs-lookup"><span data-stu-id="581e7-127">Using installations also enables you toodo partial registration updates.</span></span> <span data-ttu-id="581e7-128">mise à jour partielle d’une installation Hello est demandée avec une méthode de correctif à l’aide de hello [standard de JSON-correctif](https://tools.ietf.org/html/rfc6902).</span><span class="sxs-lookup"><span data-stu-id="581e7-128">hello partial update of an installation is requested with a PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902).</span></span> <span data-ttu-id="581e7-129">Cela est particulièrement utile lorsque vous souhaitez que les balises tooupdate sur l’inscription de hello.</span><span class="sxs-lookup"><span data-stu-id="581e7-129">This is particularly useful when you want tooupdate tags on hello registration.</span></span> <span data-ttu-id="581e7-130">Vous n’avez toopull vers le bas de l’inscription de la totalité de hello et puis de renvoyer toutes les balises précédente hello à nouveau.</span><span class="sxs-lookup"><span data-stu-id="581e7-130">You don't have toopull down hello entire registration and then resend all hello previous tags again.</span></span>

<span data-ttu-id="581e7-131">Une installation peut contenir hello hello propriétés suivantes.</span><span class="sxs-lookup"><span data-stu-id="581e7-131">An installation can contain hello hello following properties.</span></span> <span data-ttu-id="581e7-132">Pour une liste complète des hello installation des propriétés, consultez [créer ou remplacer une Installation avec l’API REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) ou [propriétés d’Installation](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) pour hello.</span><span class="sxs-lookup"><span data-stu-id="581e7-132">For a complete listing of hello installation properties see, [Create or Overwrite an Installation with REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) or [Installation Properties](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) for hello .</span></span>

    // Example installation format tooshow some supported properties
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



<span data-ttu-id="581e7-133">Il est important toonote que les enregistrements et les installations par défaut n’expirent plus.</span><span class="sxs-lookup"><span data-stu-id="581e7-133">It is important toonote that registrations and installations by default no longer expire.</span></span>

<span data-ttu-id="581e7-134">Les inscriptions et les installations doivent contenir un handle PNS valide pour chaque appareil/canal.</span><span class="sxs-lookup"><span data-stu-id="581e7-134">Registrations and installations must contain a valid PNS handle for each device/channel.</span></span> <span data-ttu-id="581e7-135">Étant donné que les handles PNS ne peuvent être obtenus dans une application cliente sur le périphérique de hello, un modèle est tooregister directement sur l’appareil avec l’application cliente de hello.</span><span class="sxs-lookup"><span data-stu-id="581e7-135">Because PNS handles can only be obtained in a client app on hello device, one pattern is tooregister directly on that device with hello client app.</span></span> <span data-ttu-id="581e7-136">Hello main, autres considérations sur la sécurité et la logique métier associés tootags peuvent nécessiter que vous toomanage d’inscription de périphérique dans hello application back-end.</span><span class="sxs-lookup"><span data-stu-id="581e7-136">On hello other hand, security considerations and business logic related tootags might require you toomanage device registration in hello app back-end.</span></span> 

#### <a name="templates"></a><span data-ttu-id="581e7-137">Modèles</span><span class="sxs-lookup"><span data-stu-id="581e7-137">Templates</span></span>
<span data-ttu-id="581e7-138">Si vous souhaitez toouse [modèles](notification-hubs-templates-cross-platform-push-messages.md), l’installation du périphérique hello contiennent également tous les modèles associés à ce périphérique dans JSON de format (voir l’exemple ci-dessus).</span><span class="sxs-lookup"><span data-stu-id="581e7-138">If you want toouse [Templates](notification-hubs-templates-cross-platform-push-messages.md), hello device installation also hold all templates associated with that device in a JSON format (see sample above).</span></span> <span data-ttu-id="581e7-139">Hello les noms de modèle aider à cibler différents modèles pour hello même appareil.</span><span class="sxs-lookup"><span data-stu-id="581e7-139">hello template names help target different templates for hello same device.</span></span>

<span data-ttu-id="581e7-140">Notez que chaque nom de modèle mappe les corps de modèle tooa et un ensemble facultatif de balises.</span><span class="sxs-lookup"><span data-stu-id="581e7-140">Note that each template name maps tooa template body and an optional set of tags.</span></span> <span data-ttu-id="581e7-141">De plus, chaque plateforme peut avoir des propriétés de modèle supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="581e7-141">Moreover, each platform can have additional template properties.</span></span> <span data-ttu-id="581e7-142">Pour Windows Store (à l’aide de WNS) et Windows Phone 8 (à l’aide de MPNS), un ensemble d’en-têtes supplémentaire peut être partie du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="581e7-142">For Windows Store (using WNS) and Windows Phone 8 (using MPNS), an additional set of headers can be part of hello template.</span></span> <span data-ttu-id="581e7-143">Dans les cas de hello de APNs, vous pouvez définir un tooeither de propriété d’expiration une expression constante ou tooa de modèle.</span><span class="sxs-lookup"><span data-stu-id="581e7-143">In hello case of APNs, you can set an expiry property tooeither a constant or tooa template expression.</span></span> <span data-ttu-id="581e7-144">Pour une liste complète des hello installation des propriétés, consultez [créer ou remplacer une Installation avec reste](https://msdn.microsoft.com/library/azure/mt621153.aspx) rubrique.</span><span class="sxs-lookup"><span data-stu-id="581e7-144">For a complete listing of hello installation properties see, [Create or Overwrite an Installation with REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) topic.</span></span>

#### <a name="secondary-tiles-for-windows-store-apps"></a><span data-ttu-id="581e7-145">Vignettes secondaires pour les applications Windows Store</span><span class="sxs-lookup"><span data-stu-id="581e7-145">Secondary Tiles for Windows Store Apps</span></span>
<span data-ttu-id="581e7-146">Pour les applications clientes du Windows Store, envoi de notifications toosecondary vignettes est même hello en envoyant toohello principale.</span><span class="sxs-lookup"><span data-stu-id="581e7-146">For Windows Store client applications, sending notifications toosecondary tiles is hello same as sending them toohello primary one.</span></span> <span data-ttu-id="581e7-147">Ce comportement est également pris en charge dans les installations.</span><span class="sxs-lookup"><span data-stu-id="581e7-147">This is also supported in installations.</span></span> <span data-ttu-id="581e7-148">Notez que les vignettes secondaires ont un autre ChannelUri, le Kit de développement logiciel hello sur votre application cliente gère en toute transparence.</span><span class="sxs-lookup"><span data-stu-id="581e7-148">Note that secondary tiles have a different ChannelUri, which hello SDK on your client app handles transparently.</span></span>

<span data-ttu-id="581e7-149">Hello SecondaryTiles dictionnaire utilise hello même TileId qui est utilisé toocreate hello SecondaryTiles objet dans votre application du Windows Store.</span><span class="sxs-lookup"><span data-stu-id="581e7-149">hello SecondaryTiles dictionary uses hello same TileId that is used toocreate hello SecondaryTiles object in your Windows Store app.</span></span>
<span data-ttu-id="581e7-150">Comme avec hello principal ChannelUri, ChannelUris de vignettes secondaires peuvent changer à tout moment.</span><span class="sxs-lookup"><span data-stu-id="581e7-150">As with hello primary ChannelUri, ChannelUris of secondary tiles can change at any moment.</span></span> <span data-ttu-id="581e7-151">Dans l’ordre tookeep hello les installations dans le hub de notification hello mis à jour, les appareils hello doivent les actualiser avec hello ChannelUris actuel de vignettes secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="581e7-151">In order tookeep hello installations in hello notification hub updated, hello device must refresh them with hello current ChannelUris of hello secondary tiles.</span></span>

## <a name="registration-management-from-hello-device"></a><span data-ttu-id="581e7-152">Gestion de l’inscription de périphérique de hello</span><span class="sxs-lookup"><span data-stu-id="581e7-152">Registration management from hello device</span></span>
<span data-ttu-id="581e7-153">Lors de la gestion de l’inscription de périphérique à partir d’applications clientes, hello principal n’est chargé d’envoyer des notifications.</span><span class="sxs-lookup"><span data-stu-id="581e7-153">When managing device registration from client apps, hello backend is only responsible for sending notifications.</span></span> <span data-ttu-id="581e7-154">Les applications clientes conserver des handles PNS des toodate et enregistrement des balises.</span><span class="sxs-lookup"><span data-stu-id="581e7-154">Client apps keep PNS handles up toodate, and register tags.</span></span> <span data-ttu-id="581e7-155">Hello illustration suivante illustre ce modèle.</span><span class="sxs-lookup"><span data-stu-id="581e7-155">hello following picture illustrates this pattern.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

<span data-ttu-id="581e7-156">Appareil de Hello récupère hello PNS gérer hello PNS tout d’abord, puis inscrit avec le hub de notification hello directement.</span><span class="sxs-lookup"><span data-stu-id="581e7-156">hello device first retrieves hello PNS handle from hello PNS, then registers with hello notification hub directly.</span></span> <span data-ttu-id="581e7-157">Après que l’inscription de hello a réussi, serveur principal d’application hello peut envoyer une notification de ciblage que l’inscription.</span><span class="sxs-lookup"><span data-stu-id="581e7-157">After hello registration is successful, hello app backend can send a notification targeting that registration.</span></span> <span data-ttu-id="581e7-158">Pour plus d’informations sur la façon toosend notifications, consultez [routage et Expressions de balises](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="581e7-158">For more information about how toosend notifications, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>
<span data-ttu-id="581e7-159">Notez que dans ce cas, vous allez utiliser à l’écoute que droits tooaccess vos hubs de notification à partir de l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="581e7-159">Note that in this case, you will use only Listen rights tooaccess your notification hubs from hello device.</span></span> <span data-ttu-id="581e7-160">Pour plus d’informations, consultez [Sécurité](notification-hubs-push-notification-security.md).</span><span class="sxs-lookup"><span data-stu-id="581e7-160">For more information, see [Security](notification-hubs-push-notification-security.md).</span></span>

<span data-ttu-id="581e7-161">L’inscription à partir de l’appareil de hello hello méthode est plus simple, mais il présente certains inconvénients.</span><span class="sxs-lookup"><span data-stu-id="581e7-161">Registering from hello device is hello simplest method, but it has some drawbacks.</span></span>
<span data-ttu-id="581e7-162">l’inconvénient de première Hello est qu’une application cliente peut uniquement mettre à jour ses balises lors de l’application hello est active.</span><span class="sxs-lookup"><span data-stu-id="581e7-162">hello first drawback is that a client app can only update its tags when hello app is active.</span></span> <span data-ttu-id="581e7-163">Par exemple, si un utilisateur a deux périphériques qui inscrivent des balises associées toosport équipes, lorsque le premier périphérique de hello inscrit pour une balise supplémentaire (par exemple, Seahawks), deuxième appareil de hello ne recevra pas notifications hello sur hello Seahawks jusqu'à ce que l’application hello sur hello deuxième appareil est exécutée une seconde fois.</span><span class="sxs-lookup"><span data-stu-id="581e7-163">For example, if a user has two devices that register tags related toosport teams, when hello first device registers for an additional tag (for example, Seahawks), hello second device will not receive hello notifications about hello Seahawks until hello app on hello second device is executed a second time.</span></span> <span data-ttu-id="581e7-164">Plus généralement, lorsque les balises sont affectées par différents appareils, la gestion des balises à partir de hello principal sont une option souhaitable.</span><span class="sxs-lookup"><span data-stu-id="581e7-164">More generally, when tags are affected by multiple devices, managing tags from hello backend is a desirable option.</span></span>
<span data-ttu-id="581e7-165">Hello deuxième inconvénient de gestion de l’inscription à partir de l’application cliente de hello est que, étant donné que les applications peuvent être piratées, sécurisation de l’inscription de hello toospecific balises nécessite un soin particulier, comme expliqué dans la section de hello « sécurité au niveau de l’étiquette. »</span><span class="sxs-lookup"><span data-stu-id="581e7-165">hello second drawback of registration management from hello client app is that, since apps can be hacked, securing hello registration toospecific tags requires extra care, as explained in hello section “Tag-level security.”</span></span>

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-an-installation"></a><span data-ttu-id="581e7-166">Tooregister de code d’exemple avec un concentrateur de notification à partir d’un appareil à l’aide d’une installation</span><span class="sxs-lookup"><span data-stu-id="581e7-166">Example code tooregister with a notification hub from a device using an installation</span></span>
<span data-ttu-id="581e7-167">À ce stade, cela est uniquement pris en charge à l’aide de hello [API REST de concentrateurs de Notification](https://msdn.microsoft.com/library/mt621153.aspx).</span><span class="sxs-lookup"><span data-stu-id="581e7-167">At this time, this is only supported using hello [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx).</span></span>

<span data-ttu-id="581e7-168">Vous pouvez également utiliser la méthode de correctif hello à l’aide de hello [standard de JSON-correctif](https://tools.ietf.org/html/rfc6902) de mise à jour d’installation de hello.</span><span class="sxs-lookup"><span data-stu-id="581e7-168">You can also use hello PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating hello installation.</span></span>

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

        // Determine hello targetUri that we will sign
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



#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration"></a><span data-ttu-id="581e7-169">Tooregister de code d’exemple avec un concentrateur de notification à partir d’un appareil à l’aide de l’inscription d’une</span><span class="sxs-lookup"><span data-stu-id="581e7-169">Example code tooregister with a notification hub from a device using a registration</span></span>
<span data-ttu-id="581e7-170">Ces méthodes, créent ou mettre à jour une inscription de périphérique hello sur lequel elles sont appelées.</span><span class="sxs-lookup"><span data-stu-id="581e7-170">These methods create or update a registration for hello device on which they are called.</span></span> <span data-ttu-id="581e7-171">Cela signifie que tooupdate hello handle ou hello balises, vous devez remplacer l’enregistrement de la totalité de hello.</span><span class="sxs-lookup"><span data-stu-id="581e7-171">This means that in order tooupdate hello handle or hello tags, you must overwrite hello entire registration.</span></span> <span data-ttu-id="581e7-172">N’oubliez pas que les enregistrements sont temporaires, vous devez toujours disposer d’un magasin fiable avec les balises actives hello qui a besoin d’un périphérique spécifique.</span><span class="sxs-lookup"><span data-stu-id="581e7-172">Remember that registrations are transient, so you should always have a reliable store with hello current tags that a specific device needs.</span></span>

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // hello Device id from hello PNS
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // If you are registering from hello client itself, then store this registration id in device
    // storage. Then when hello app starts, you can check if a registration id already exists or not before
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


## <a name="registration-management-from-a-backend"></a><span data-ttu-id="581e7-173">Gestion des inscriptions à partir d’un serveur principal</span><span class="sxs-lookup"><span data-stu-id="581e7-173">Registration management from a backend</span></span>
<span data-ttu-id="581e7-174">La gestion des inscriptions de hello principal requiert l’écriture de code supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="581e7-174">Managing registrations from hello backend requires writing additional code.</span></span> <span data-ttu-id="581e7-175">application Hello à partir de l’appareil de hello doit fournir hello back-end du toohello de handle PNS mis à jour chaque démarrage d’application hello, (ainsi que les balises et les modèles) et hello principal doit mettre à jour ce descripteur de concentrateur de notification hello.</span><span class="sxs-lookup"><span data-stu-id="581e7-175">hello app from hello device must provide hello updated PNS handle toohello backend every time hello app starts (along with tags and templates), and hello backend must update this handle on hello notification hub.</span></span> <span data-ttu-id="581e7-176">Hello illustration suivante montre cette conception.</span><span class="sxs-lookup"><span data-stu-id="581e7-176">hello following picture illustrates this design.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

<span data-ttu-id="581e7-177">Hello de la gestion des inscriptions de hello principaux avantages hello capacité toomodify balises tooregistrations même lorsque l’application correspondante hello sur l’appareil de hello est inactive et tooauthenticate hello client application avant d’ajouter un enregistrement tooits de balise.</span><span class="sxs-lookup"><span data-stu-id="581e7-177">hello advantages of managing registrations from hello backend include hello ability toomodify tags tooregistrations even when hello corresponding app on hello device is inactive, and tooauthenticate hello client app before adding a tag tooits registration.</span></span>

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-backend-using-an-installation"></a><span data-ttu-id="581e7-178">Tooregister de code d’exemple avec un concentrateur de notification à partir d’un serveur principal à l’aide d’une installation</span><span class="sxs-lookup"><span data-stu-id="581e7-178">Example code tooregister with a notification hub from a backend using an installation</span></span>
<span data-ttu-id="581e7-179">périphérique de client Hello toujours obtient son handle PNS et les propriétés d’installation approprié comme avant et appelle une API personnalisée sur le principal hello qui peut effectuer l’inscription de hello et autoriser des balises etc. hello principal peut tirer parti de hello [Kit de développement logiciel de concentrateur de Notification opérations de serveur principal](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="581e7-179">hello client device still gets its PNS handle and relevant installation properties as before and calls a custom API on hello backend that can perform hello registration and authorize tags etc. hello backend can leverage hello [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="581e7-180">Vous pouvez également utiliser la méthode de correctif hello à l’aide de hello [standard de JSON-correctif](https://tools.ietf.org/html/rfc6902) de mise à jour d’installation de hello.</span><span class="sxs-lookup"><span data-stu-id="581e7-180">You can also use hello PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating hello installation.</span></span>

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // Custom API on hello backend
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


        // In hello backend we can control if a user is allowed tooadd tags
        //installation.Tags = new List<string>(deviceUpdate.Tags);
        //installation.Tags.Add("username:" + username);

        await hub.CreateOrUpdateInstallationAsync(installation);

        return Request.CreateResponse(HttpStatusCode.OK);
    }


#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration-id"></a><span data-ttu-id="581e7-181">Tooregister de code d’exemple avec un concentrateur de notification à partir d’un appareil à l’aide d’un id d’inscription</span><span class="sxs-lookup"><span data-stu-id="581e7-181">Example code tooregister with a notification hub from a device using a registration id</span></span>
<span data-ttu-id="581e7-182">À partir de votre serveur principal d’application, vous pouvez effectuer les opérations CRUD de base sur les inscriptions.</span><span class="sxs-lookup"><span data-stu-id="581e7-182">From your app backend, you can perform basic CRUDS operations on registrations.</span></span> <span data-ttu-id="581e7-183">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="581e7-183">For example:</span></span>

    var hub = NotificationHubClient.CreateClientFromConnectionString("{connectionString}", "hubName");

    // create a registration description object of hello correct type, e.g.
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


<span data-ttu-id="581e7-184">Hello principal doit gérer la concurrence entre les mises à jour de l’inscription.</span><span class="sxs-lookup"><span data-stu-id="581e7-184">hello backend must handle concurrency between registration updates.</span></span> <span data-ttu-id="581e7-185">Service Bus offre un contrôle de l’accès concurrentiel optimiste pour la gestion des inscriptions.</span><span class="sxs-lookup"><span data-stu-id="581e7-185">Service Bus offers optimistic concurrency control for registration management.</span></span> <span data-ttu-id="581e7-186">Au niveau de hello HTTP, cela est implémenté avec utilisation hello d’ETag sur les opérations de gestion de l’inscription.</span><span class="sxs-lookup"><span data-stu-id="581e7-186">At hello HTTP level, this is implemented with hello use of ETag on registration management operations.</span></span> <span data-ttu-id="581e7-187">Cette fonctionnalité est utilisée de manière transparente dans les Kits de développement logiciel (SDK) Microsoft, lesquels lèvent une exception si une mise à jour est refusée en raison d’accès concurrentiel.</span><span class="sxs-lookup"><span data-stu-id="581e7-187">This feature is transparently used by Microsoft SDKs, which throw an exception if an update is rejected for concurrency reasons.</span></span> <span data-ttu-id="581e7-188">serveur principal d’application Hello est responsable de la gestion de ces exceptions et une nouvelle tentative de mise à jour hello si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="581e7-188">hello app backend is responsible for handling these exceptions and retrying hello update if required.</span></span>

