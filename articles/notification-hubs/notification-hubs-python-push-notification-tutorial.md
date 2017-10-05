---
title: Utilisation de Notification Hubs avec Python
description: "Découvrez comment utiliser Azure Notification Hubs à partir d'un serveur principal Python."
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
ms.openlocfilehash: 9ceedb9940759427fc8cec74a1307e42472563a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-notification-hubs-from-python"></a><span data-ttu-id="013c1-103">Utilisation de Notification Hubs à partir de Python</span><span class="sxs-lookup"><span data-stu-id="013c1-103">How to use Notification Hubs from Python</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="013c1-104">Vous pouvez accéder à toutes les fonctionnalités Notification Hubs à partir d'un serveur principal Java/PHP/Python/Ruby en utilisant l'interface REST Notification Hub, comme décrit dans la rubrique MSDN [API REST Notification Hubs](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="013c1-104">You can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="013c1-105">Ceci est un exemple d’implémentation de référence pour l’implémentation des envois de notifications dans Python. Il ne s’agit pas du Kit de développement logiciel (SDK) de Notification Hub Python officiellement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="013c1-105">This is a sample reference implementation for implementing the notification sends in Python and is not the officially supported Notifications Hub Python SDK.</span></span>
> 
> <span data-ttu-id="013c1-106">Cet exemple a été écrit à l’aide de Python 3.4.</span><span class="sxs-lookup"><span data-stu-id="013c1-106">This sample is written using Python 3.4.</span></span>
> 
> 

<span data-ttu-id="013c1-107">Dans cette rubrique, nous vous montrons comment :</span><span class="sxs-lookup"><span data-stu-id="013c1-107">In this topic we show how to:</span></span>

* <span data-ttu-id="013c1-108">créer un client REST pour les fonctionnalités de Notification Hubs dans Python ;</span><span class="sxs-lookup"><span data-stu-id="013c1-108">Build a REST client for Notification Hubs features in Python.</span></span>
* <span data-ttu-id="013c1-109">envoyer des notifications à l’aide de l’interface de Python vers les API REST Notification Hub ;</span><span class="sxs-lookup"><span data-stu-id="013c1-109">Send notifications using the Python interface to the Notification Hub REST APIs.</span></span> 
* <span data-ttu-id="013c1-110">obtenir un vidage de la demande/réponse HTTP REST à des fins pédagogiques/de débogage.</span><span class="sxs-lookup"><span data-stu-id="013c1-110">Get a dump of the HTTP REST request/response for debugging/educational purpose.</span></span> 

<span data-ttu-id="013c1-111">Vous pouvez suivre le [didacticiel de prise en main](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) pour la plateforme mobile de votre choix, en implémentant la partie concernant le serveur principal dans Python.</span><span class="sxs-lookup"><span data-stu-id="013c1-111">You can follow the [Get started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) for your mobile platform of choice, implementing the back-end portion in Python.</span></span>

> [!NOTE]
> <span data-ttu-id="013c1-112">L’étendue de l’exemple est limitée uniquement à l’envoi de notifications et il n’effectue aucune gestion des inscriptions.</span><span class="sxs-lookup"><span data-stu-id="013c1-112">The scope of the sample is only limited to send notifications and it doesn't do any registration management.</span></span>
> 
> 

## <a name="client-interface"></a><span data-ttu-id="013c1-113">Interface client</span><span class="sxs-lookup"><span data-stu-id="013c1-113">Client interface</span></span>
<span data-ttu-id="013c1-114">L'interface client principale peut fournir les mêmes méthodes que celles disponibles dans le [Kit de développement logiciel (SDK) .NET Notification Hubs](http://msdn.microsoft.com/library/jj933431.aspx).</span><span class="sxs-lookup"><span data-stu-id="013c1-114">The main client interface can provide the same methods that are available in the [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx).</span></span> <span data-ttu-id="013c1-115">Cela vous permet de traduire directement les didacticiels et les exemples actuellement disponibles sur ce site et fournis par la communauté sur Internet.</span><span class="sxs-lookup"><span data-stu-id="013c1-115">This will allow you to directly translate all the tutorials and samples currently available on this site, and contributed by the community on the internet.</span></span>

<span data-ttu-id="013c1-116">Tout le code est disponible dans l' [exemple de wrapper REST Python].</span><span class="sxs-lookup"><span data-stu-id="013c1-116">You can find all the code available in the [Python REST wrapper sample].</span></span>

<span data-ttu-id="013c1-117">Par exemple, pour créer un client :</span><span class="sxs-lookup"><span data-stu-id="013c1-117">For example, to create a client:</span></span>

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="013c1-118">Pour envoyer une notification toast de Windows :</span><span class="sxs-lookup"><span data-stu-id="013c1-118">To send a Windows toast notification:</span></span>

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a><span data-ttu-id="013c1-119">Implémentation</span><span class="sxs-lookup"><span data-stu-id="013c1-119">Implementation</span></span>
<span data-ttu-id="013c1-120">Si ce n'est déjà fait, suivez notre [didacticiel de prise en main] jusqu'à la dernière section, dans laquelle vous devrez implémenter le serveur principal.</span><span class="sxs-lookup"><span data-stu-id="013c1-120">If you did not already, please follow our [Get started tutorial] up to the last section where you have to implement the back-end.</span></span>

<span data-ttu-id="013c1-121">Tous les détails de l'implémentation d'un wrapper REST complet se trouvent sur [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="013c1-121">All the details to implement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="013c1-122">Dans cette section, nous allons décrire l’implémentation Python des principales étapes requises pour accéder aux point de terminaison REST de Notification Hubs et envoyer des notifications :</span><span class="sxs-lookup"><span data-stu-id="013c1-122">In this section we will describe the Python implementation of the main steps required to access Notification Hubs REST endpoints and send notifications</span></span>

1. <span data-ttu-id="013c1-123">Analyse de la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="013c1-123">Parse the connection string</span></span>
2. <span data-ttu-id="013c1-124">Génération du jeton d'autorisation</span><span class="sxs-lookup"><span data-stu-id="013c1-124">Generate the authorization token</span></span>
3. <span data-ttu-id="013c1-125">Envoyer une notification à l’aide de l’API REST de HTTP</span><span class="sxs-lookup"><span data-stu-id="013c1-125">Send a notification using HTTP REST API</span></span>

### <a name="parse-the-connection-string"></a><span data-ttu-id="013c1-126">Analyse de la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="013c1-126">Parse the connection string</span></span>
<span data-ttu-id="013c1-127">Voici la classe principale implémentant le client, dont le constructeur analyse la chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="013c1-127">Here is the main class implementing the client, whose constructor parses the connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="013c1-128">Création du jeton de sécurité</span><span class="sxs-lookup"><span data-stu-id="013c1-128">Create security token</span></span>
<span data-ttu-id="013c1-129">Les détails concernant la création d'un jeton de sécurité sont disponibles [ici](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="013c1-129">The details of the security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="013c1-130">Les méthodes suivantes doivent être ajoutées à la classe **NotificationHub** pour créer le jeton à partir de l'URI de la demande actuelle et des informations d'identification extraites de la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="013c1-130">The following methods have to be added to the **NotificationHub** class to create the token based on the URI of the current request and the credentials extracted from the connection string.</span></span>

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

### <a name="send-a-notification-using-http-rest-api"></a><span data-ttu-id="013c1-131">Envoyer une notification à l’aide de l’API REST de HTTP</span><span class="sxs-lookup"><span data-stu-id="013c1-131">Send a notification using HTTP REST API</span></span>
<span data-ttu-id="013c1-132">Commençons par définir une classe représentant une notification.</span><span class="sxs-lookup"><span data-stu-id="013c1-132">First, let use define a class representing a notification.</span></span>

    class Notification:
        def __init__(self, notification_format=None, payload=None, debug=0):
            valid_formats = ['template', 'apple', 'gcm', 'windows', 'windowsphone', "adm", "baidu"]
            if not any(x in notification_format for x in valid_formats):
                raise Exception(
                    "Invalid Notification format. " +
                    "Must be one of the following - 'template', 'apple', 'gcm', 'windows', 'windowsphone', 'adm', 'baidu'")

            self.format = notification_format
            self.payload = payload

            # array with keynames for headers
            # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
            # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry
            # in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
            self.headers = None

<span data-ttu-id="013c1-133">Cette classe est un conteneur pour un corps de notification natif ou un ensemble de propriétés dans le cas d’un modèle de notification, et un ensemble d’en-têtes contenant le format (plateforme native ou modèle) et des propriétés spécifiques de la plateforme (telles que la propriété d’expiration d’Apple et les en-têtes WNS).</span><span class="sxs-lookup"><span data-stu-id="013c1-133">This class is a container for a native notification body or a set of properties in case of a template notification, a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="013c1-134">Pour connaître toutes les options disponibles, reportez-vous à la [documentation sur les API REST de Notification Hubs](http://msdn.microsoft.com/library/dn495827.aspx) et aux formats spécifiques des plateformes de notification.</span><span class="sxs-lookup"><span data-stu-id="013c1-134">Please refer to the [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and the specific notification platforms' formats for all the options available.</span></span>

<span data-ttu-id="013c1-135">Avec cette classe, nous pouvons à présent écrire les méthodes d'envoi des notifications à l'intérieur de la classe **NotificationHub** .</span><span class="sxs-lookup"><span data-stu-id="013c1-135">Now with this class, we can write the send notification methods inside of the **NotificationHub** class.</span></span>

    def make_http_request(self, url, payload, headers):
        parsed_url = urllib.parse.urlparse(url)
        connection = http.client.HTTPSConnection(parsed_url.hostname, parsed_url.port)

        if self.Debug > 0:
            connection.set_debuglevel(self.Debug)
            # adding this querystring parameter gets detailed information about the PNS send notification outcome
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

        # add the tags/tag expressions to the headers collection
        if tag_list != "":
            headers.update({'ServiceBusNotification-Tags': tag_list})

        # add any custom headers to the headers collection that the user may have added
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

<span data-ttu-id="013c1-136">Les méthodes ci-dessus envoient une demande POST HTTP au point de terminaison /messages de votre hub de notification, avec le corps et les en-têtes corrects pour envoyer la notification.</span><span class="sxs-lookup"><span data-stu-id="013c1-136">The above methods send an HTTP POST request to the /messages endpoint of your notification hub, with the correct body and headers to send the notification.</span></span>

### <a name="using-debug-property-to-enable-detailed-logging"></a><span data-ttu-id="013c1-137">Utilisation de la propriété debug pour activer la journalisation détaillée</span><span class="sxs-lookup"><span data-stu-id="013c1-137">Using debug property to enable detailed logging</span></span>
<span data-ttu-id="013c1-138">L’activation de la propriété debug lors de l’initialisation du hub de notification permet de rédiger des informations de journalisation détaillées sur le vidage des requêtes et réponses HTTP, ainsi que le résultat détaillé de l’envoi des messages de notification.</span><span class="sxs-lookup"><span data-stu-id="013c1-138">Enabling debug property while initializing the Notification Hub will write out detailed logging information about the HTTP request and response dump as well as detailed Notification message send outcome.</span></span> <span data-ttu-id="013c1-139">Nous avons récemment ajouté cette propriété appelée [propriété TestSend Notification Hubs](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) , qui retourne des informations détaillées sur le résultat de l'envoi de notification.</span><span class="sxs-lookup"><span data-stu-id="013c1-139">We recently added this property called [Notification Hubs TestSend property](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) which returns detailed information about the notification send outcome.</span></span> <span data-ttu-id="013c1-140">Pour l’utiliser, réalisez une initialisation à l’aide de ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="013c1-140">To use it - initialize using the following:</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="013c1-141">L’URL HTTP de demande d’envoi de hub de notification est ajoutée avec une chaîne de requête « test ».</span><span class="sxs-lookup"><span data-stu-id="013c1-141">The Notification Hub Send request HTTP URL gets appended with a "test" querystring as a result.</span></span> 

## <span data-ttu-id="013c1-142"><a name="complete-tutorial"></a>Suivi du didacticiel</span><span class="sxs-lookup"><span data-stu-id="013c1-142"><a name="complete-tutorial"></a>Complete the tutorial</span></span>
<span data-ttu-id="013c1-143">Vous pouvez à présent terminer le didacticiel de prise en main en envoyant la notification à partir d’un serveur principal Python.</span><span class="sxs-lookup"><span data-stu-id="013c1-143">Now you can complete the Get Started tutorial by sending the notification from a Python back-end.</span></span>

<span data-ttu-id="013c1-144">Initialisez votre client Notification Hubs (remplacez la chaîne de connexion et le nom du hub comme indiqué dans le [didacticiel de prise en main]) :</span><span class="sxs-lookup"><span data-stu-id="013c1-144">Initialize your Notification Hubs client (substitute the connection string and hub name as instructed in the [Get started tutorial]):</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

<span data-ttu-id="013c1-145">Ajoutez ensuite le code d'envoi en fonction de la plateforme mobile cible.</span><span class="sxs-lookup"><span data-stu-id="013c1-145">Then add the send code depending on your target mobile platform.</span></span> <span data-ttu-id="013c1-146">Cet exemple ajoute également des méthodes de plus haut niveau pour activer l’envoi de notifications basées sur la plateforme, par exemple send_windows_notification pour Windows, send_apple_notification (pour Apple), etc.</span><span class="sxs-lookup"><span data-stu-id="013c1-146">This sample also adds higher level methods to enable sending notifications based on the platform e.g. send_windows_notification for windows; send_apple_notification (for apple) etc.</span></span> 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="013c1-147">Windows Store et Windows Phone 8.1 (non-Silverlight)</span><span class="sxs-lookup"><span data-stu-id="013c1-147">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="013c1-148">Windows Phone 8.0 et 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="013c1-148">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    hub.send_mpns_notification(toast)

### <a name="ios"></a><span data-ttu-id="013c1-149">iOS</span><span class="sxs-lookup"><span data-stu-id="013c1-149">iOS</span></span>
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a><span data-ttu-id="013c1-150">Android</span><span class="sxs-lookup"><span data-stu-id="013c1-150">Android</span></span>
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a><span data-ttu-id="013c1-151">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="013c1-151">Kindle Fire</span></span>
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a><span data-ttu-id="013c1-152">Baidu</span><span class="sxs-lookup"><span data-stu-id="013c1-152">Baidu</span></span>
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

<span data-ttu-id="013c1-153">L’exécution de votre code Python produit normalement une notification qui apparaît sur votre appareil cible.</span><span class="sxs-lookup"><span data-stu-id="013c1-153">Running your Python code should produce a notification appearing on your target device.</span></span>

## <a name="examples"></a><span data-ttu-id="013c1-154">Exemples :</span><span class="sxs-lookup"><span data-stu-id="013c1-154">Examples:</span></span>
### <a name="enabling-debug-property"></a><span data-ttu-id="013c1-155">Activation de la propriété debug</span><span class="sxs-lookup"><span data-stu-id="013c1-155">Enabling debug property</span></span>
<span data-ttu-id="013c1-156">Quand vous activez l'indicateur de débogage pendant l'initialisation de la classe NotificationHub, vous voyez un vidage détaillé des requêtes et réponses HTTP, ainsi que NotificationOutcome, comme suit, où vous pouvez comprendre quels en-têtes HTTP sont transmis dans la demande et quelle réponse HTTP a été reçue à partir du hub de notification : ![][1]</span><span class="sxs-lookup"><span data-stu-id="013c1-156">When you enable debug flag while initializing the NotificationHub then you will see detailed HTTP request and response dump as well as NotificationOutcome like the following where you can understand what HTTP headers are passed in the request and what HTTP response was received from the Notification Hub: ![][1]</span></span>

<span data-ttu-id="013c1-157">Vous verrez un résultat détaillé de hub de notification, par exemple</span><span class="sxs-lookup"><span data-stu-id="013c1-157">You will see detailed Notification Hub result e.g.</span></span> 

* <span data-ttu-id="013c1-158">lorsque le message est envoyé au service de notification Push.</span><span class="sxs-lookup"><span data-stu-id="013c1-158">when the message is successfully sent to the Push Notification Service.</span></span> 
  
        <Outcome>The Notification was successfully sent to the Push Notification System</Outcome>
* <span data-ttu-id="013c1-159">Si aucune cible n’a été trouvée pour les notifications Push, vous verrez probablement les éléments suivants dans la réponse (ce qui indique qu’il n’y a eu aucun enregistrement trouvé pour fournir la notification, probablement parce que certaines balises des inscriptions ne correspondaient pas)</span><span class="sxs-lookup"><span data-stu-id="013c1-159">If there were no targets found for any push notification then you are likely going to see the following in the response (which indicates that there were no registrations found to deliver the notification probably because the registrations had some mismatched tags)</span></span>
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-to-windows"></a><span data-ttu-id="013c1-160">Notification toast de diffusion à Windows</span><span class="sxs-lookup"><span data-stu-id="013c1-160">Broadcast toast notification to Windows</span></span>
<span data-ttu-id="013c1-161">Notez les en-têtes qui sont envoyés lorsque vous envoyez une notification toast de diffusion au client Windows.</span><span class="sxs-lookup"><span data-stu-id="013c1-161">Notice the headers that get sent out when you are sending a broadcast toast notification to Windows client.</span></span> 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a><span data-ttu-id="013c1-162">Envoyer une notification indiquant une balise (ou une expression de balise)</span><span class="sxs-lookup"><span data-stu-id="013c1-162">Send notification specifying a tag (or tag expression)</span></span>
<span data-ttu-id="013c1-163">Notez l'en-tête HTTP de balises qui est ajouté à la requête HTTP (dans l'exemple ci-dessous, vous envoyez la notification uniquement aux inscriptions avec la charge utile « sports »)</span><span class="sxs-lookup"><span data-stu-id="013c1-163">Notice the Tags HTTP header which gets added to the HTTP request (in the example below, we are sending the notification only to registrations with 'sports' payload)</span></span>

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a><span data-ttu-id="013c1-164">Envoyer une notification spécifiant plusieurs balises</span><span class="sxs-lookup"><span data-stu-id="013c1-164">Send notification specifying multiple tags</span></span>
<span data-ttu-id="013c1-165">Notez comment l’en-tête HTTP des balises change lorsque plusieurs balises sont envoyées.</span><span class="sxs-lookup"><span data-stu-id="013c1-165">Notice how the Tags HTTP header changes when multiple tags are sent.</span></span> 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a><span data-ttu-id="013c1-166">Notification avec modèle</span><span class="sxs-lookup"><span data-stu-id="013c1-166">Templated notification</span></span>
<span data-ttu-id="013c1-167">Notez que l’en-tête HTTP de format change et que le corps de charge utile est envoyé en tant que partie intégrante du corps de requête HTTP :</span><span class="sxs-lookup"><span data-stu-id="013c1-167">Notice that the Format HTTP header changes and the payload body is sent as part of the HTTP request body:</span></span>

<span data-ttu-id="013c1-168">**Côté client - modèle enregistré**</span><span class="sxs-lookup"><span data-stu-id="013c1-168">**Client side - registered template**</span></span>

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

<span data-ttu-id="013c1-169">**Côté serveur - envoi de la charge utile**</span><span class="sxs-lookup"><span data-stu-id="013c1-169">**Server side - sending the payload**</span></span>

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a><span data-ttu-id="013c1-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="013c1-170">Next Steps</span></span>
<span data-ttu-id="013c1-171">Dans cette rubrique, nous vous avons montré comment créer un client REST Python simple pour Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="013c1-171">In this topic we showed how to create a simple Python REST client for Notification Hubs.</span></span> <span data-ttu-id="013c1-172">À ce stade, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="013c1-172">From here you can:</span></span>

* <span data-ttu-id="013c1-173">télécharger l'intégralité de l' [exemple de wrapper REST Python], qui contient tout le code ci-dessus ;</span><span class="sxs-lookup"><span data-stu-id="013c1-173">Download the full [Python REST wrapper sample], which contains all the code above.</span></span>
* <span data-ttu-id="013c1-174">poursuivre l'apprentissage de la fonctionnalité de balisage de Notification Hubs dans le [didacticiel Nouvelles de dernière minute]</span><span class="sxs-lookup"><span data-stu-id="013c1-174">Continue learning about Notification Hubs tagging feature in the [Breaking News tutorial]</span></span>
* <span data-ttu-id="013c1-175">poursuivre l'apprentissage de la fonctionnalité des modèles de Notification Hubs dans le [didacticiel de localisation des dernières nouvelles]</span><span class="sxs-lookup"><span data-stu-id="013c1-175">Continue learning about Notification Hubs Templates feature in the [Localizing News tutorial]</span></span>

<!-- URLs -->
<span data-ttu-id="013c1-176">[exemple de wrapper REST Python]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python</span><span class="sxs-lookup"><span data-stu-id="013c1-176">[Python REST wrapper sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python</span></span>
<span data-ttu-id="013c1-177">[didacticiel de prise en main]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span><span class="sxs-lookup"><span data-stu-id="013c1-177">[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span></span>
<span data-ttu-id="013c1-178">[didacticiel Nouvelles de dernière minute]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/</span><span class="sxs-lookup"><span data-stu-id="013c1-178">[Breaking News tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/</span></span>
<span data-ttu-id="013c1-179">[didacticiel de localisation des dernières nouvelles]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/</span><span class="sxs-lookup"><span data-stu-id="013c1-179">[Localizing News tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-python-backend-how-to/DetailedLoggingInfo.png
[2]: ./media/notification-hubs-python-backend-how-to/BroadcastScenario.png
[3]: ./media/notification-hubs-python-backend-how-to/SendWithOneTag.png
[4]: ./media/notification-hubs-python-backend-how-to/SendWithMultipleTags.png
[5]: ./media/notification-hubs-python-backend-how-to/TemplatedNotification.png

