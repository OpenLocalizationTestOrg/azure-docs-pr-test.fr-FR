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
# <a name="registration-management"></a>Gestion des inscriptions
## <a name="overview"></a>Vue d'ensemble
Cette rubrique explique comment tooregister les appareils avec des concentrateurs de notification dans l’ordre tooreceive des notifications push. rubrique de Hello décrit les enregistrements à un niveau élevé, puis présente des modèles de hello deux principales pour l’inscription des appareils : l’inscription à partir de l’appareil de hello directement le hub de notification toohello et l’inscription via un serveur principal d’application. 

## <a name="what-is-device-registration"></a>Présentation de l’inscription d’un appareil
L’inscription d’un appareil auprès d’un hub de notification s’effectue à l’aide d’une **inscription** ou d’une **installation**.

#### <a name="registrations"></a>Inscriptions
Une inscription associe hello plateforme Notification Service (PNS) gérer pour un périphérique avec balises et éventuellement un modèle. Hello PNS handle peut être un ChannelURI, jeton de périphérique ou l’id d’inscription GCM. Les balises sont des notifications de tooroute utilisés ensemble correct de toohello de handles du périphérique. Pour plus d’informations, consultez [Routage et expressions de balises](notification-hubs-tags-segment-push-message.md). Les modèles sont utilisés tooimplement par inscription transformation. Pour plus d’informations, consultez [Modèles](notification-hubs-templates-cross-platform-push-messages.md).

#### <a name="installations"></a>Installations
Une installation est une inscription améliorée qui inclut un conteneur de propriétés associées à des opérations push. Il s’agit de hello meilleure approche tooregistering vos appareils. Toutefois, elle n’est actuellement pas prise en charge par le Kit de développement logiciel .NET côté client ([SDK Notification Hub pour les opérations de serveur principal](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)).  Cela signifie que si l’inscription d’appareil client de hello lui-même, vous devriez toouse hello [API REST de concentrateurs de Notification](https://msdn.microsoft.com/library/mt621153.aspx) approche toosupport installations. Si vous utilisez un service principal, vous devez être en mesure de toouse [SDK de concentrateur de Notification pour les opérations de serveur principal](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

Hello Voici certaines installations de toousing avantages clés :

* La création ou la mise à jour d’une installation est entièrement idempotente. Vous pouvez donc la retenter sans vous soucier des inscriptions en double.
* modèle d’installation Hello facilite toodo facile de push individuels - ciblage des appareils spécifiques. Une balise système **« $InstallationId:[installationId] »** est ajoutée automatiquement avec chaque inscription basée sur l’installation. Par conséquent, vous pouvez appeler un tootarget de balise toothis envoyer un périphérique spécifique sans avoir à toodo de codage supplémentaire.
* L’utilisation des installations permet également de mises à jour partielles d’inscription toodo vous. mise à jour partielle d’une installation Hello est demandée avec une méthode de correctif à l’aide de hello [standard de JSON-correctif](https://tools.ietf.org/html/rfc6902). Cela est particulièrement utile lorsque vous souhaitez que les balises tooupdate sur l’inscription de hello. Vous n’avez toopull vers le bas de l’inscription de la totalité de hello et puis de renvoyer toutes les balises précédente hello à nouveau.

Une installation peut contenir hello hello propriétés suivantes. Pour une liste complète des hello installation des propriétés, consultez [créer ou remplacer une Installation avec l’API REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) ou [propriétés d’Installation](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) pour hello.

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



Il est important toonote que les enregistrements et les installations par défaut n’expirent plus.

Les inscriptions et les installations doivent contenir un handle PNS valide pour chaque appareil/canal. Étant donné que les handles PNS ne peuvent être obtenus dans une application cliente sur le périphérique de hello, un modèle est tooregister directement sur l’appareil avec l’application cliente de hello. Hello main, autres considérations sur la sécurité et la logique métier associés tootags peuvent nécessiter que vous toomanage d’inscription de périphérique dans hello application back-end. 

#### <a name="templates"></a>Modèles
Si vous souhaitez toouse [modèles](notification-hubs-templates-cross-platform-push-messages.md), l’installation du périphérique hello contiennent également tous les modèles associés à ce périphérique dans JSON de format (voir l’exemple ci-dessus). Hello les noms de modèle aider à cibler différents modèles pour hello même appareil.

Notez que chaque nom de modèle mappe les corps de modèle tooa et un ensemble facultatif de balises. De plus, chaque plateforme peut avoir des propriétés de modèle supplémentaires. Pour Windows Store (à l’aide de WNS) et Windows Phone 8 (à l’aide de MPNS), un ensemble d’en-têtes supplémentaire peut être partie du modèle de hello. Dans les cas de hello de APNs, vous pouvez définir un tooeither de propriété d’expiration une expression constante ou tooa de modèle. Pour une liste complète des hello installation des propriétés, consultez [créer ou remplacer une Installation avec reste](https://msdn.microsoft.com/library/azure/mt621153.aspx) rubrique.

#### <a name="secondary-tiles-for-windows-store-apps"></a>Vignettes secondaires pour les applications Windows Store
Pour les applications clientes du Windows Store, envoi de notifications toosecondary vignettes est même hello en envoyant toohello principale. Ce comportement est également pris en charge dans les installations. Notez que les vignettes secondaires ont un autre ChannelUri, le Kit de développement logiciel hello sur votre application cliente gère en toute transparence.

Hello SecondaryTiles dictionnaire utilise hello même TileId qui est utilisé toocreate hello SecondaryTiles objet dans votre application du Windows Store.
Comme avec hello principal ChannelUri, ChannelUris de vignettes secondaires peuvent changer à tout moment. Dans l’ordre tookeep hello les installations dans le hub de notification hello mis à jour, les appareils hello doivent les actualiser avec hello ChannelUris actuel de vignettes secondaire de hello.

## <a name="registration-management-from-hello-device"></a>Gestion de l’inscription de périphérique de hello
Lors de la gestion de l’inscription de périphérique à partir d’applications clientes, hello principal n’est chargé d’envoyer des notifications. Les applications clientes conserver des handles PNS des toodate et enregistrement des balises. Hello illustration suivante illustre ce modèle.

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

Appareil de Hello récupère hello PNS gérer hello PNS tout d’abord, puis inscrit avec le hub de notification hello directement. Après que l’inscription de hello a réussi, serveur principal d’application hello peut envoyer une notification de ciblage que l’inscription. Pour plus d’informations sur la façon toosend notifications, consultez [routage et Expressions de balises](notification-hubs-tags-segment-push-message.md).
Notez que dans ce cas, vous allez utiliser à l’écoute que droits tooaccess vos hubs de notification à partir de l’appareil de hello. Pour plus d’informations, consultez [Sécurité](notification-hubs-push-notification-security.md).

L’inscription à partir de l’appareil de hello hello méthode est plus simple, mais il présente certains inconvénients.
l’inconvénient de première Hello est qu’une application cliente peut uniquement mettre à jour ses balises lors de l’application hello est active. Par exemple, si un utilisateur a deux périphériques qui inscrivent des balises associées toosport équipes, lorsque le premier périphérique de hello inscrit pour une balise supplémentaire (par exemple, Seahawks), deuxième appareil de hello ne recevra pas notifications hello sur hello Seahawks jusqu'à ce que l’application hello sur hello deuxième appareil est exécutée une seconde fois. Plus généralement, lorsque les balises sont affectées par différents appareils, la gestion des balises à partir de hello principal sont une option souhaitable.
Hello deuxième inconvénient de gestion de l’inscription à partir de l’application cliente de hello est que, étant donné que les applications peuvent être piratées, sécurisation de l’inscription de hello toospecific balises nécessite un soin particulier, comme expliqué dans la section de hello « sécurité au niveau de l’étiquette. »

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-an-installation"></a>Tooregister de code d’exemple avec un concentrateur de notification à partir d’un appareil à l’aide d’une installation
À ce stade, cela est uniquement pris en charge à l’aide de hello [API REST de concentrateurs de Notification](https://msdn.microsoft.com/library/mt621153.aspx).

Vous pouvez également utiliser la méthode de correctif hello à l’aide de hello [standard de JSON-correctif](https://tools.ietf.org/html/rfc6902) de mise à jour d’installation de hello.

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



#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration"></a>Tooregister de code d’exemple avec un concentrateur de notification à partir d’un appareil à l’aide de l’inscription d’une
Ces méthodes, créent ou mettre à jour une inscription de périphérique hello sur lequel elles sont appelées. Cela signifie que tooupdate hello handle ou hello balises, vous devez remplacer l’enregistrement de la totalité de hello. N’oubliez pas que les enregistrements sont temporaires, vous devez toujours disposer d’un magasin fiable avec les balises actives hello qui a besoin d’un périphérique spécifique.

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


## <a name="registration-management-from-a-backend"></a>Gestion des inscriptions à partir d’un serveur principal
La gestion des inscriptions de hello principal requiert l’écriture de code supplémentaire. application Hello à partir de l’appareil de hello doit fournir hello back-end du toohello de handle PNS mis à jour chaque démarrage d’application hello, (ainsi que les balises et les modèles) et hello principal doit mettre à jour ce descripteur de concentrateur de notification hello. Hello illustration suivante montre cette conception.

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

Hello de la gestion des inscriptions de hello principaux avantages hello capacité toomodify balises tooregistrations même lorsque l’application correspondante hello sur l’appareil de hello est inactive et tooauthenticate hello client application avant d’ajouter un enregistrement tooits de balise.

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-backend-using-an-installation"></a>Tooregister de code d’exemple avec un concentrateur de notification à partir d’un serveur principal à l’aide d’une installation
périphérique de client Hello toujours obtient son handle PNS et les propriétés d’installation approprié comme avant et appelle une API personnalisée sur le principal hello qui peut effectuer l’inscription de hello et autoriser des balises etc. hello principal peut tirer parti de hello [Kit de développement logiciel de concentrateur de Notification opérations de serveur principal](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

Vous pouvez également utiliser la méthode de correctif hello à l’aide de hello [standard de JSON-correctif](https://tools.ietf.org/html/rfc6902) de mise à jour d’installation de hello.

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


#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration-id"></a>Tooregister de code d’exemple avec un concentrateur de notification à partir d’un appareil à l’aide d’un id d’inscription
À partir de votre serveur principal d’application, vous pouvez effectuer les opérations CRUD de base sur les inscriptions. Par exemple :

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


Hello principal doit gérer la concurrence entre les mises à jour de l’inscription. Service Bus offre un contrôle de l’accès concurrentiel optimiste pour la gestion des inscriptions. Au niveau de hello HTTP, cela est implémenté avec utilisation hello d’ETag sur les opérations de gestion de l’inscription. Cette fonctionnalité est utilisée de manière transparente dans les Kits de développement logiciel (SDK) Microsoft, lesquels lèvent une exception si une mise à jour est refusée en raison d’accès concurrentiel. serveur principal d’application Hello est responsable de la gestion de ces exceptions et une nouvelle tentative de mise à jour hello si nécessaire.

