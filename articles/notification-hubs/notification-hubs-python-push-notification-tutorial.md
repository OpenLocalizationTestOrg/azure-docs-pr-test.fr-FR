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
# <a name="how-toouse-notification-hubs-from-python"></a>Comment toouse concentrateurs de Notification à partir de Python
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

Vous pouvez accéder à toutes les fonctionnalités de concentrateurs de Notification à partir d’un Java/PHP/Python/Ruby back-end à l’aide d’interface REST de concentrateur de Notification de hello comme décrit dans la rubrique MSDN hello [API REST de concentrateurs de Notification](http://msdn.microsoft.com/library/dn223264.aspx).

> [!NOTE]
> Ceci est un exemple d’implémentation de référence pour l’implémentation de hello notification envoie dans Python et n’est pas hello officiellement pris en charge que le SDK de Python de Hub de Notifications.
> 
> Cet exemple a été écrit à l’aide de Python 3.4.
> 
> 

Dans cette rubrique, nous vous montrons comment :

* créer un client REST pour les fonctionnalités de Notification Hubs dans Python ;
* Envoyer des notifications à l’aide de hello Python interface toohello API REST de concentrateur de Notification. 
* Obtenir un vidage de hello HTTP REST demande/réponse à des fins pédagogiques/débogage. 

Vous pouvez suivre hello [didacticiel Get](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) pour votre plateforme mobile de choix, l’implémentation de la partie des principaux de hello dans Python.

> [!NOTE]
> Hello la portée de l’exemple hello est uniquement les notifications toosend limitée et qu’il n’effectue pas une gestion de l’inscription.
> 
> 

## <a name="client-interface"></a>Interface client
interface principale du client de Hello peut fournir hello mêmes méthodes que celles qui sont disponibles dans hello [concentrateurs de Notification .NET SDK](http://msdn.microsoft.com/library/jj933431.aspx). Cela vous permettra de toodirectly traduire tous les didacticiels de hello et exemples actuellement disponibles sur ce site et fournis par la Communauté hello sur hello internet.

Vous trouverez tout code hello disponible dans hello [exemple de wrapper Python reste].

Par exemple, toocreate un client :

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

notification de toast toosend Windows :

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a>Implémentation
Si vous n’avez pas déjà, suivez notre [didacticiel Get] toohello dernière section dans laquelle vous avez tooimplement hello principal vers le haut.

Tous les hello tooimplement détails se trouvent sur un wrapper reste complète [MSDN](http://msdn.microsoft.com/library/dn530746.aspx). Dans cette section nous décrivent l’implémentation de Python hello de hello étapes principales tooaccess requis points de terminaison REST de concentrateurs de Notification et envoyer des notifications

1. Analyser la chaîne de connexion hello
2. Générer le jeton d’autorisation hello
3. Envoyer une notification à l’aide de l’API REST de HTTP

### <a name="parse-hello-connection-string"></a>Analyser la chaîne de connexion hello
Voici la classe principale de hello implémentation hello client, dont le constructeur analyse la chaîne de connexion hello :

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


### <a name="create-security-token"></a>Création du jeton de sécurité
Détails de Hello de création de jetons de sécurité hello sont disponibles [ici](http://msdn.microsoft.com/library/dn495627.aspx).
Hello méthodes suivantes ont ajouté de toobe toohello **NotificationHub** jeton de classe toocreate hello selon hello URI de demande en cours de hello et les informations d’identification hello extraites à partir de la chaîne de connexion hello.

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

### <a name="send-a-notification-using-http-rest-api"></a>Envoyer une notification à l’aide de l’API REST de HTTP
Commençons par définir une classe représentant une notification.

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

Cette classe est un conteneur pour un corps de notification natif ou un ensemble de propriétés dans le cas d’un modèle de notification, et un ensemble d’en-têtes contenant le format (plateforme native ou modèle) et des propriétés spécifiques de la plateforme (telles que la propriété d’expiration d’Apple et les en-têtes WNS).

Reportez-vous toohello [documentation de l’API REST de concentrateurs Notification](http://msdn.microsoft.com/library/dn495827.aspx) et hello les formats des plateformes de notification spécifique pour tous les hello options disponibles.

Maintenant avec cette classe, nous pouvons écrire vos méthodes de notification à l’intérieur de hello hello envoi **NotificationHub** classe.

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

Hello au-dessus de méthodes d’envoyer une requête HTTP POST demande toohello /messages point de terminaison de votre concentrateur de notification avec corps correct de hello et notification de hello toosend en-têtes.

### <a name="using-debug-property-tooenable-detailed-logging"></a>Tooenable de propriété de débogage à l’aide de la journalisation détaillée
L’activation de la propriété de débogage lors de l’initialisation hello Hub de Notification écrira les informations de journalisation détaillées sur hello HTTP demande et vidage de réponse, ainsi que message de Notification détaillée envoyer le résultat. Nous avons récemment ajouté cette propriété appelée [TestSend de concentrateurs de Notification propriété](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) qui retourne des informations détaillées sur la sortie d’envoi de notification hello. toouse il - initialisation utilisation hello qui suit :

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

demande d’envoi de Notification Hub Hello URL HTTP obtient ainsi ajoutée avec une chaîne de requête « test ». 

## <a name="complete-tutorial"></a>Didacticiel de hello terminée
Maintenant, vous pouvez effectuer didacticiel de mise en route de hello en envoyant des notifications de hello depuis un Python back-end.

Initialiser vos concentrateurs de Notification de client (remplacez le nom de hub et la chaîne de connexion hello comme indiqué dans hello [didacticiel Get]) :

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

Ajoutez ensuite du code d’envoi hello selon votre plateforme mobile cible. Cet exemple ajoute également la plus élevée tooenable méthodes au niveau envoi de notifications basées sur une plateforme de hello, par exemple send_windows_notification pour windows. send_apple_notification (pour apple) etc.. 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a>Windows Store et Windows Phone 8.1 (non-Silverlight)
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a>Windows Phone 8.0 et 8.1 Silverlight
    hub.send_mpns_notification(toast)

### <a name="ios"></a>iOS
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a>Android
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a>Kindle Fire
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a>Baidu
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

L’exécution de votre code Python produit normalement une notification qui apparaît sur votre appareil cible.

## <a name="examples"></a>Exemples :
### <a name="enabling-debug-property"></a>Activation de la propriété debug
Lorsque vous activez le débogage indicateur lors de l’initialisation hello NotificationHub vous observez détaillées dump de demande et de réponse HTTP, ainsi que NotificationOutcome suivante hello où vous pouvez comprendre les en-têtes HTTP sont passés dans la demande hello et quelles HTTP réponse a été reçue à partir de hello Hub de Notification :![][1]

Vous verrez un résultat détaillé de hub de notification, par exemple 

* Lorsque message de type hello est envoyé avec succès toohello services de notifications Push. 
  
        <Outcome>hello Notification was successfully sent toohello Push Notification System</Outcome>
* S’il y avait aucune cible n’est trouvé pour les notifications push, puis vous allez probablement toosee qui suit hello dans la réponse hello (ce qui indique qu’il n’existait aucun enregistrement trouvé notification de hello toodeliver probablement parce que les enregistrements de hello eu balises ne correspondent pas)
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-toowindows"></a>Diffusion tooWindows de notification toast
Notez que les en-têtes hello obtient envoyés lorsque vous envoyez un client de tooWindows notification toast diffusion. 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a>Envoyer une notification indiquant une balise (ou une expression de balise)
En-tête HTTP de balises hello avis est ajouté à la demande de toohello HTTP (dans l’exemple hello ci-dessous, nous envoyons tooregistrations uniquement de notification hello avec sa charge utile 'sports')

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a>Envoyer une notification spécifiant plusieurs balises
Notez comment les en-tête de balises HTTP hello change lorsque plusieurs balises sont envoyés. 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a>Notification avec modèle
Notez que hello les modifications d’en-tête HTTP de Format et corps de la charge utile de hello est envoyée en tant que partie du corps de la demande hello HTTP :

**Côté client - modèle enregistré**

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

**Côté serveur - envoyer la charge utile de hello**

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a>Étapes suivantes
Dans cette rubrique, nous vous avons montré comment toocreate une simple Python REST client pour les concentrateurs de Notification. À ce stade, vous pouvez :

* Télécharger hello complète [exemple de wrapper Python reste], qui contient tout code hello ci-dessus.
* Continuer à découvrir des concentrateurs de Notification marquage fonctionnalité Bonjour [didacticiel des dernières nouvelles]
* Continuer à découvrir la fonctionnalité de Notification Hubs modèles Bonjour [didacticiel de localisation des actualités]

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

