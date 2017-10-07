---
title: aaaHow toouse concentrateurs de Notification avec Python
description: "Découvrez comment toouse Azure Notification Hubs à partir d’un Python back-end."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 5640dd4a-a91e-4aa0-a833-93615bde49b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: python
ms.devlang: php
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 21d5aaf7fc24c9936fac8e0a8de640c66c51ab0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-python"></a><span data-ttu-id="ea36c-103">Comment toouse concentrateurs de Notification à partir de Python</span><span class="sxs-lookup"><span data-stu-id="ea36c-103">How toouse Notification Hubs from Python</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="ea36c-104">Vous pouvez accéder à toutes les fonctionnalités de concentrateurs de Notification à partir d’un Java/PHP/Python/Ruby back-end à l’aide d’interface REST de concentrateur de Notification de hello comme décrit dans la rubrique MSDN hello [API REST de concentrateurs de Notification](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea36c-104">You can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="ea36c-105">Ceci est un exemple d’implémentation de référence pour l’implémentation de hello notification envoie dans Python et n’est pas hello officiellement pris en charge que le SDK de Python de Hub de Notifications.</span><span class="sxs-lookup"><span data-stu-id="ea36c-105">This is a sample reference implementation for implementing hello notification sends in Python and is not hello officially supported Notifications Hub Python SDK.</span></span>
> 
> <span data-ttu-id="ea36c-106">Cet exemple a été écrit à l’aide de Python 3.4.</span><span class="sxs-lookup"><span data-stu-id="ea36c-106">This sample is written using Python 3.4.</span></span>
> 
> 

<span data-ttu-id="ea36c-107">Dans cette rubrique, nous vous montrons comment :</span><span class="sxs-lookup"><span data-stu-id="ea36c-107">In this topic we show how to:</span></span>

* <span data-ttu-id="ea36c-108">créer un client REST pour les fonctionnalités de Notification Hubs dans Python ;</span><span class="sxs-lookup"><span data-stu-id="ea36c-108">Build a REST client for Notification Hubs features in Python.</span></span>
* <span data-ttu-id="ea36c-109">Envoyer des notifications à l’aide de hello Python interface toohello API REST de concentrateur de Notification.</span><span class="sxs-lookup"><span data-stu-id="ea36c-109">Send notifications using hello Python interface toohello Notification Hub REST APIs.</span></span> 
* <span data-ttu-id="ea36c-110">Obtenir un vidage de hello HTTP REST demande/réponse à des fins pédagogiques/débogage.</span><span class="sxs-lookup"><span data-stu-id="ea36c-110">Get a dump of hello HTTP REST request/response for debugging/educational purpose.</span></span> 

<span data-ttu-id="ea36c-111">Vous pouvez suivre hello [didacticiel Get](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) pour votre plateforme mobile de choix, l’implémentation de la partie des principaux de hello dans Python.</span><span class="sxs-lookup"><span data-stu-id="ea36c-111">You can follow hello [Get started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) for your mobile platform of choice, implementing hello back-end portion in Python.</span></span>

> [!NOTE]
> <span data-ttu-id="ea36c-112">Hello la portée de l’exemple hello est uniquement les notifications toosend limitée et qu’il n’effectue pas une gestion de l’inscription.</span><span class="sxs-lookup"><span data-stu-id="ea36c-112">hello scope of hello sample is only limited toosend notifications and it doesn't do any registration management.</span></span>
> 
> 

## <a name="client-interface"></a><span data-ttu-id="ea36c-113">Interface client</span><span class="sxs-lookup"><span data-stu-id="ea36c-113">Client interface</span></span>
<span data-ttu-id="ea36c-114">interface principale du client de Hello peut fournir hello mêmes méthodes que celles qui sont disponibles dans hello [concentrateurs de Notification .NET SDK](http://msdn.microsoft.com/library/jj933431.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea36c-114">hello main client interface can provide hello same methods that are available in hello [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx).</span></span> <span data-ttu-id="ea36c-115">Cela vous permettra de toodirectly traduire tous les didacticiels de hello et exemples actuellement disponibles sur ce site et fournis par la Communauté hello sur hello internet.</span><span class="sxs-lookup"><span data-stu-id="ea36c-115">This will allow you toodirectly translate all hello tutorials and samples currently available on this site, and contributed by hello community on hello internet.</span></span>

<span data-ttu-id="ea36c-116">Vous trouverez tout code hello disponible dans hello [exemple de wrapper Python reste].</span><span class="sxs-lookup"><span data-stu-id="ea36c-116">You can find all hello code available in hello [Python REST wrapper sample].</span></span>

<span data-ttu-id="ea36c-117">Par exemple, toocreate un client :</span><span class="sxs-lookup"><span data-stu-id="ea36c-117">For example, toocreate a client:</span></span>

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="ea36c-118">notification de toast toosend Windows :</span><span class="sxs-lookup"><span data-stu-id="ea36c-118">toosend a Windows toast notification:</span></span>

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a><span data-ttu-id="ea36c-119">Implémentation</span><span class="sxs-lookup"><span data-stu-id="ea36c-119">Implementation</span></span>
<span data-ttu-id="ea36c-120">Si vous n’avez pas déjà, suivez notre [didacticiel Get] toohello dernière section dans laquelle vous avez tooimplement hello principal vers le haut.</span><span class="sxs-lookup"><span data-stu-id="ea36c-120">If you did not already, please follow our [Get started tutorial] up toohello last section where you have tooimplement hello back-end.</span></span>

<span data-ttu-id="ea36c-121">Tous les hello tooimplement détails se trouvent sur un wrapper reste complète [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea36c-121">All hello details tooimplement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="ea36c-122">Dans cette section nous décrivent l’implémentation de Python hello de hello étapes principales tooaccess requis points de terminaison REST de concentrateurs de Notification et envoyer des notifications</span><span class="sxs-lookup"><span data-stu-id="ea36c-122">In this section we will describe hello Python implementation of hello main steps required tooaccess Notification Hubs REST endpoints and send notifications</span></span>

1. <span data-ttu-id="ea36c-123">Analyser la chaîne de connexion hello</span><span class="sxs-lookup"><span data-stu-id="ea36c-123">Parse hello connection string</span></span>
2. <span data-ttu-id="ea36c-124">Générer le jeton d’autorisation hello</span><span class="sxs-lookup"><span data-stu-id="ea36c-124">Generate hello authorization token</span></span>
3. <span data-ttu-id="ea36c-125">Envoyer une notification à l’aide de l’API REST de HTTP</span><span class="sxs-lookup"><span data-stu-id="ea36c-125">Send a notification using HTTP REST API</span></span>

### <a name="parse-hello-connection-string"></a><span data-ttu-id="ea36c-126">Analyser la chaîne de connexion hello</span><span class="sxs-lookup"><span data-stu-id="ea36c-126">Parse hello connection string</span></span>
<span data-ttu-id="ea36c-127">Voici la classe principale de hello implémentation hello client, dont le constructeur analyse la chaîne de connexion hello :</span><span class="sxs-lookup"><span data-stu-id="ea36c-127">Here is hello main class implementing hello client, whose constructor parses hello connection string:</span></span>

    class NotificationHub:
        API_VERSION = "?api-version=2013-10"
        DEBUG_SEND = "&test"

        def __init__(self, connection_string=None, hub_name=None, debug=0):
            self.HubName = hub_name
            self.Debug = debug

            # Parse connection string
            parts = connection_string.split(';')
            if len(parts) != 3:
                raise Exception("Invalid ConnectionString.")

            for part in parts:
                if part.startswith('Endpoint'):
                    self.Endpoint = 'https' + part[11:]
                if part.startswith('SharedAccessKeyName'):
                    self.SasKeyName = part[20:]
                if part.startswith('SharedAccessKey'):
                    self.SasKeyValue = part[16:]


### <a name="create-security-token"></a><span data-ttu-id="ea36c-128">Création du jeton de sécurité</span><span class="sxs-lookup"><span data-stu-id="ea36c-128">Create security token</span></span>
<span data-ttu-id="ea36c-129">Détails de Hello de création de jetons de sécurité hello sont disponibles [ici](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea36c-129">hello details of hello security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="ea36c-130">Hello méthodes suivantes ont ajouté de toobe toohello **NotificationHub** jeton de classe toocreate hello selon hello URI de demande en cours de hello et les informations d’identification hello extraites à partir de la chaîne de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="ea36c-130">hello following methods have toobe added toohello **NotificationHub** class toocreate hello token based on hello URI of hello current request and hello credentials extracted from hello connection string.</span></span>

    @staticmethod
    def get_expiry():
        # By default returns an expiration of 5 minutes (=300 seconds) from now
        return int(round(time.time() + 300))

    @staticmethod
    def encode_base64(data):
        return base64.b64encode(data)

    def sign_string(self, to_sign):
        key = self.SasKeyValue.encode('utf-8')
        to_sign = to_sign.encode('utf-8')
        signed_hmac_sha256 = hmac.HMAC(key, to_sign, hashlib.sha256)
        digest = signed_hmac_sha256.digest()
        encoded_digest = self.encode_base64(digest)
        return encoded_digest

    def generate_sas_token(self):
        target_uri = self.Endpoint + self.HubName
        my_uri = urllib.parse.quote(target_uri, '').lower()
        expiry = str(self.get_expiry())
        to_sign = my_uri + '\n' + expiry
        signature = urllib.parse.quote(self.sign_string(to_sign))
        auth_format = 'SharedAccessSignature sig={0}&se={1}&skn={2}&sr={3}'
        sas_token = auth_format.format(signature, expiry, self.SasKeyName, my_uri)
        return sas_token

### <a name="send-a-notification-using-http-rest-api"></a><span data-ttu-id="ea36c-131">Envoyer une notification à l’aide de l’API REST de HTTP</span><span class="sxs-lookup"><span data-stu-id="ea36c-131">Send a notification using HTTP REST API</span></span>
<span data-ttu-id="ea36c-132">Commençons par définir une classe représentant une notification.</span><span class="sxs-lookup"><span data-stu-id="ea36c-132">First, let use define a class representing a notification.</span></span>

    class Notification:
        def __init__(self, notification_format=None, payload=None, debug=0):
            valid_formats = ['template', 'apple', 'gcm', 'windows', 'windowsphone', "adm", "baidu"]
            if not any(x in notification_format for x in valid_formats):
                raise Exception(
                    "Invalid Notification format. " +
                    "Must be one of hello following - 'template', 'apple', 'gcm', 'windows', 'windowsphone', 'adm', 'baidu'")

            self.format = notification_format
            self.payload = payload

            # array with keynames for headers
            # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
            # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry
            # in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
            self.headers = None

<span data-ttu-id="ea36c-133">Cette classe est un conteneur pour un corps de notification natif ou un ensemble de propriétés dans le cas d’un modèle de notification, et un ensemble d’en-têtes contenant le format (plateforme native ou modèle) et des propriétés spécifiques de la plateforme (telles que la propriété d’expiration d’Apple et les en-têtes WNS).</span><span class="sxs-lookup"><span data-stu-id="ea36c-133">This class is a container for a native notification body or a set of properties in case of a template notification, a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="ea36c-134">Reportez-vous toohello [documentation de l’API REST de concentrateurs Notification](http://msdn.microsoft.com/library/dn495827.aspx) et hello les formats des plateformes de notification spécifique pour tous les hello options disponibles.</span><span class="sxs-lookup"><span data-stu-id="ea36c-134">Please refer toohello [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and hello specific notification platforms' formats for all hello options available.</span></span>

<span data-ttu-id="ea36c-135">Maintenant avec cette classe, nous pouvons écrire vos méthodes de notification à l’intérieur de hello hello envoi **NotificationHub** classe.</span><span class="sxs-lookup"><span data-stu-id="ea36c-135">Now with this class, we can write hello send notification methods inside of hello **NotificationHub** class.</span></span>

    def make_http_request(self, url, payload, headers):
        parsed_url = urllib.parse.urlparse(url)
        connection = http.client.HTTPSConnection(parsed_url.hostname, parsed_url.port)

        if self.Debug > 0:
            connection.set_debuglevel(self.Debug)
            # adding this querystring parameter gets detailed information about hello PNS send notification outcome
            url += self.DEBUG_SEND
            print("--- REQUEST ---")
            print("URI: " + url)
            print("Headers: " + json.dumps(headers, sort_keys=True, indent=4, separators=(' ', ': ')))
            print("--- END REQUEST ---\n")

        connection.request('POST', url, payload, headers)
        response = connection.getresponse()

        if self.Debug > 0:
            # print out detailed response information for debugging purpose
            print("\n\n--- RESPONSE ---")
            print(str(response.status) + " " + response.reason)
            print(response.msg)
            print(response.read())
            print("--- END RESPONSE ---")

        elif response.status != 201:
            # Successful outcome of send message is HTTP 201 - Created
            raise Exception(
                "Error sending notification. Received HTTP code " + str(response.status) + " " + response.reason)

        connection.close()

    def send_notification(self, notification, tag_or_tag_expression=None):
        url = self.Endpoint + self.HubName + '/messages' + self.API_VERSION

        json_platforms = ['template', 'apple', 'gcm', 'adm', 'baidu']

        if any(x in notification.format for x in json_platforms):
            content_type = "application/json"
            payload_to_send = json.dumps(notification.payload)
        else:
            content_type = "application/xml"
            payload_to_send = notification.payload

        headers = {
            'Content-type': content_type,
            'Authorization': self.generate_sas_token(),
            'ServiceBusNotification-Format': notification.format
        }

        if isinstance(tag_or_tag_expression, set):
            tag_list = ' || '.join(tag_or_tag_expression)
        else:
            tag_list = tag_or_tag_expression

        # add hello tags/tag expressions toohello headers collection
        if tag_list != "":
            headers.update({'ServiceBusNotification-Tags': tag_list})

        # add any custom headers toohello headers collection that hello user may have added
        if notification.headers is not None:
            headers.update(notification.headers)

        self.make_http_request(url, payload_to_send, headers)

    def send_apple_notification(self, payload, tags=""):
        nh = Notification("apple", payload)
        self.send_notification(nh, tags)

    def send_gcm_notification(self, payload, tags=""):
        nh = Notification("gcm", payload)
        self.send_notification(nh, tags)

    def send_adm_notification(self, payload, tags=""):
        nh = Notification("adm", payload)
        self.send_notification(nh, tags)

    def send_baidu_notification(self, payload, tags=""):
        nh = Notification("baidu", payload)
        self.send_notification(nh, tags)

    def send_mpns_notification(self, payload, tags=""):
        nh = Notification("windowsphone", payload)

        if "<wp:Toast>" in payload:
            nh.headers = {'X-WindowsPhone-Target': 'toast', 'X-NotificationClass': '2'}
        elif "<wp:Tile>" in payload:
            nh.headers = {'X-WindowsPhone-Target': 'tile', 'X-NotificationClass': '1'}

        self.send_notification(nh, tags)

    def send_windows_notification(self, payload, tags=""):
        nh = Notification("windows", payload)

        if "<toast>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/toast'}
        elif "<tile>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/tile'}
        elif "<badge>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/badge'}

        self.send_notification(nh, tags)

    def send_template_notification(self, properties, tags=""):
        nh = Notification("template", properties)
        self.send_notification(nh, tags)

<span data-ttu-id="ea36c-136">Hello au-dessus de méthodes d’envoyer une requête HTTP POST demande toohello /messages point de terminaison de votre concentrateur de notification avec corps correct de hello et notification de hello toosend en-têtes.</span><span class="sxs-lookup"><span data-stu-id="ea36c-136">hello above methods send an HTTP POST request toohello /messages endpoint of your notification hub, with hello correct body and headers toosend hello notification.</span></span>

### <a name="using-debug-property-tooenable-detailed-logging"></a><span data-ttu-id="ea36c-137">Tooenable de propriété de débogage à l’aide de la journalisation détaillée</span><span class="sxs-lookup"><span data-stu-id="ea36c-137">Using debug property tooenable detailed logging</span></span>
<span data-ttu-id="ea36c-138">L’activation de la propriété de débogage lors de l’initialisation hello Hub de Notification écrira les informations de journalisation détaillées sur hello HTTP demande et vidage de réponse, ainsi que message de Notification détaillée envoyer le résultat.</span><span class="sxs-lookup"><span data-stu-id="ea36c-138">Enabling debug property while initializing hello Notification Hub will write out detailed logging information about hello HTTP request and response dump as well as detailed Notification message send outcome.</span></span> <span data-ttu-id="ea36c-139">Nous avons récemment ajouté cette propriété appelée [TestSend de concentrateurs de Notification propriété](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) qui retourne des informations détaillées sur la sortie d’envoi de notification hello.</span><span class="sxs-lookup"><span data-stu-id="ea36c-139">We recently added this property called [Notification Hubs TestSend property](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) which returns detailed information about hello notification send outcome.</span></span> <span data-ttu-id="ea36c-140">toouse il - initialisation utilisation hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="ea36c-140">toouse it - initialize using hello following:</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="ea36c-141">demande d’envoi de Notification Hub Hello URL HTTP obtient ainsi ajoutée avec une chaîne de requête « test ».</span><span class="sxs-lookup"><span data-stu-id="ea36c-141">hello Notification Hub Send request HTTP URL gets appended with a "test" querystring as a result.</span></span> 

## <span data-ttu-id="ea36c-142"><a name="complete-tutorial"></a>Didacticiel de hello terminée</span><span class="sxs-lookup"><span data-stu-id="ea36c-142"><a name="complete-tutorial"></a>Complete hello tutorial</span></span>
<span data-ttu-id="ea36c-143">Maintenant, vous pouvez effectuer didacticiel de mise en route de hello en envoyant des notifications de hello depuis un Python back-end.</span><span class="sxs-lookup"><span data-stu-id="ea36c-143">Now you can complete hello Get Started tutorial by sending hello notification from a Python back-end.</span></span>

<span data-ttu-id="ea36c-144">Initialiser vos concentrateurs de Notification de client (remplacez le nom de hub et la chaîne de connexion hello comme indiqué dans hello [didacticiel Get]) :</span><span class="sxs-lookup"><span data-stu-id="ea36c-144">Initialize your Notification Hubs client (substitute hello connection string and hub name as instructed in hello [Get started tutorial]):</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

<span data-ttu-id="ea36c-145">Ajoutez ensuite du code d’envoi hello selon votre plateforme mobile cible.</span><span class="sxs-lookup"><span data-stu-id="ea36c-145">Then add hello send code depending on your target mobile platform.</span></span> <span data-ttu-id="ea36c-146">Cet exemple ajoute également la plus élevée tooenable méthodes au niveau envoi de notifications basées sur une plateforme de hello, par exemple send_windows_notification pour windows. send_apple_notification (pour apple) etc..</span><span class="sxs-lookup"><span data-stu-id="ea36c-146">This sample also adds higher level methods tooenable sending notifications based on hello platform e.g. send_windows_notification for windows; send_apple_notification (for apple) etc.</span></span> 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="ea36c-147">Windows Store et Windows Phone 8.1 (non-Silverlight)</span><span class="sxs-lookup"><span data-stu-id="ea36c-147">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="ea36c-148">Windows Phone 8.0 et 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="ea36c-148">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    hub.send_mpns_notification(toast)

### <a name="ios"></a><span data-ttu-id="ea36c-149">iOS</span><span class="sxs-lookup"><span data-stu-id="ea36c-149">iOS</span></span>
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a><span data-ttu-id="ea36c-150">Android</span><span class="sxs-lookup"><span data-stu-id="ea36c-150">Android</span></span>
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a><span data-ttu-id="ea36c-151">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="ea36c-151">Kindle Fire</span></span>
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a><span data-ttu-id="ea36c-152">Baidu</span><span class="sxs-lookup"><span data-stu-id="ea36c-152">Baidu</span></span>
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

<span data-ttu-id="ea36c-153">L’exécution de votre code Python produit normalement une notification qui apparaît sur votre appareil cible.</span><span class="sxs-lookup"><span data-stu-id="ea36c-153">Running your Python code should produce a notification appearing on your target device.</span></span>

## <a name="examples"></a><span data-ttu-id="ea36c-154">Exemples :</span><span class="sxs-lookup"><span data-stu-id="ea36c-154">Examples:</span></span>
### <a name="enabling-debug-property"></a><span data-ttu-id="ea36c-155">Activation de la propriété debug</span><span class="sxs-lookup"><span data-stu-id="ea36c-155">Enabling debug property</span></span>
<span data-ttu-id="ea36c-156">Lorsque vous activez le débogage indicateur lors de l’initialisation hello NotificationHub vous observez détaillées dump de demande et de réponse HTTP, ainsi que NotificationOutcome suivante hello où vous pouvez comprendre les en-têtes HTTP sont passés dans la demande hello et quelles HTTP réponse a été reçue à partir de hello Hub de Notification :![][1]</span><span class="sxs-lookup"><span data-stu-id="ea36c-156">When you enable debug flag while initializing hello NotificationHub then you will see detailed HTTP request and response dump as well as NotificationOutcome like hello following where you can understand what HTTP headers are passed in hello request and what HTTP response was received from hello Notification Hub: ![][1]</span></span>

<span data-ttu-id="ea36c-157">Vous verrez un résultat détaillé de hub de notification, par exemple</span><span class="sxs-lookup"><span data-stu-id="ea36c-157">You will see detailed Notification Hub result e.g.</span></span> 

* <span data-ttu-id="ea36c-158">Lorsque message de type hello est envoyé avec succès toohello services de notifications Push.</span><span class="sxs-lookup"><span data-stu-id="ea36c-158">when hello message is successfully sent toohello Push Notification Service.</span></span> 
  
        <Outcome>hello Notification was successfully sent toohello Push Notification System</Outcome>
* <span data-ttu-id="ea36c-159">S’il y avait aucune cible n’est trouvé pour les notifications push, puis vous allez probablement toosee qui suit hello dans la réponse hello (ce qui indique qu’il n’existait aucun enregistrement trouvé notification de hello toodeliver probablement parce que les enregistrements de hello eu balises ne correspondent pas)</span><span class="sxs-lookup"><span data-stu-id="ea36c-159">If there were no targets found for any push notification then you are likely going toosee hello following in hello response (which indicates that there were no registrations found toodeliver hello notification probably because hello registrations had some mismatched tags)</span></span>
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-toowindows"></a><span data-ttu-id="ea36c-160">Diffusion tooWindows de notification toast</span><span class="sxs-lookup"><span data-stu-id="ea36c-160">Broadcast toast notification tooWindows</span></span>
<span data-ttu-id="ea36c-161">Notez que les en-têtes hello obtient envoyés lorsque vous envoyez un client de tooWindows notification toast diffusion.</span><span class="sxs-lookup"><span data-stu-id="ea36c-161">Notice hello headers that get sent out when you are sending a broadcast toast notification tooWindows client.</span></span> 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a><span data-ttu-id="ea36c-162">Envoyer une notification indiquant une balise (ou une expression de balise)</span><span class="sxs-lookup"><span data-stu-id="ea36c-162">Send notification specifying a tag (or tag expression)</span></span>
<span data-ttu-id="ea36c-163">En-tête HTTP de balises hello avis est ajouté à la demande de toohello HTTP (dans l’exemple hello ci-dessous, nous envoyons tooregistrations uniquement de notification hello avec sa charge utile 'sports')</span><span class="sxs-lookup"><span data-stu-id="ea36c-163">Notice hello Tags HTTP header which gets added toohello HTTP request (in hello example below, we are sending hello notification only tooregistrations with 'sports' payload)</span></span>

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a><span data-ttu-id="ea36c-164">Envoyer une notification spécifiant plusieurs balises</span><span class="sxs-lookup"><span data-stu-id="ea36c-164">Send notification specifying multiple tags</span></span>
<span data-ttu-id="ea36c-165">Notez comment les en-tête de balises HTTP hello change lorsque plusieurs balises sont envoyés.</span><span class="sxs-lookup"><span data-stu-id="ea36c-165">Notice how hello Tags HTTP header changes when multiple tags are sent.</span></span> 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a><span data-ttu-id="ea36c-166">Notification avec modèle</span><span class="sxs-lookup"><span data-stu-id="ea36c-166">Templated notification</span></span>
<span data-ttu-id="ea36c-167">Notez que hello les modifications d’en-tête HTTP de Format et corps de la charge utile de hello est envoyée en tant que partie du corps de la demande hello HTTP :</span><span class="sxs-lookup"><span data-stu-id="ea36c-167">Notice that hello Format HTTP header changes and hello payload body is sent as part of hello HTTP request body:</span></span>

<span data-ttu-id="ea36c-168">**Côté client - modèle enregistré**</span><span class="sxs-lookup"><span data-stu-id="ea36c-168">**Client side - registered template**</span></span>

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

<span data-ttu-id="ea36c-169">**Côté serveur - envoyer la charge utile de hello**</span><span class="sxs-lookup"><span data-stu-id="ea36c-169">**Server side - sending hello payload**</span></span>

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a><span data-ttu-id="ea36c-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ea36c-170">Next Steps</span></span>
<span data-ttu-id="ea36c-171">Dans cette rubrique, nous vous avons montré comment toocreate une simple Python REST client pour les concentrateurs de Notification.</span><span class="sxs-lookup"><span data-stu-id="ea36c-171">In this topic we showed how toocreate a simple Python REST client for Notification Hubs.</span></span> <span data-ttu-id="ea36c-172">À ce stade, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="ea36c-172">From here you can:</span></span>

* <span data-ttu-id="ea36c-173">Télécharger hello complète [exemple de wrapper Python reste], qui contient tout code hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ea36c-173">Download hello full [Python REST wrapper sample], which contains all hello code above.</span></span>
* <span data-ttu-id="ea36c-174">Continuer à découvrir des concentrateurs de Notification marquage fonctionnalité Bonjour [didacticiel des dernières nouvelles]</span><span class="sxs-lookup"><span data-stu-id="ea36c-174">Continue learning about Notification Hubs tagging feature in hello [Breaking News tutorial]</span></span>
* <span data-ttu-id="ea36c-175">Continuer à découvrir la fonctionnalité de Notification Hubs modèles Bonjour [didacticiel de localisation des actualités]</span><span class="sxs-lookup"><span data-stu-id="ea36c-175">Continue learning about Notification Hubs Templates feature in hello [Localizing News tutorial]</span></span>

<!-- URLs -->
[exemple de wrapper Python reste]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python
[didacticiel Get]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/
[didacticiel des dernières nouvelles]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/
[didacticiel de localisation des actualités]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/

<!-- Images. -->
[1]: ./media/notification-hubs-python-backend-how-to/DetailedLoggingInfo.png
[2]: ./media/notification-hubs-python-backend-how-to/BroadcastScenario.png
[3]: ./media/notification-hubs-python-backend-how-to/SendWithOneTag.png
[4]: ./media/notification-hubs-python-backend-how-to/SendWithMultipleTags.png
[5]: ./media/notification-hubs-python-backend-how-to/TemplatedNotification.png

