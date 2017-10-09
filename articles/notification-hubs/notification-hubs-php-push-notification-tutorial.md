---
title: aaaHow toouse concentrateurs de Notification avec PHP
description: "Découvrez comment toouse Azure Notification Hubs à partir d’un PHP back-end."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 0156f994-96d0-4878-b07b-49b7be4fd856
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: php
ms.devlang: php
ms.topic: article
ms.date: 06/07/2016
ms.author: yuaxu
ms.openlocfilehash: 6cd426286a684006a07867fcf44a8ff71be7efa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-php"></a>Comment toouse concentrateurs de Notification à partir de PHP
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

Vous pouvez accéder à toutes les fonctionnalités de concentrateurs de Notification à partir d’un Java/PHP/Ruby back-end à l’aide d’interface REST de concentrateur de Notification de hello comme décrit dans la rubrique MSDN hello [API REST de concentrateurs de Notification](http://msdn.microsoft.com/library/dn223264.aspx).

Dans cette rubrique, nous vous montrons comment :

* créer un client REST pour les fonctionnalités de Notification Hubs en PHP ;
* Suivez hello [didacticiel Get](notification-hubs-ios-apple-push-notification-apns-get-started.md) pour votre plateforme mobile de choix, l’implémentation de la partie des principaux de hello en PHP.

## <a name="client-interface"></a>Interface client
interface principale du client de Hello peut fournir hello mêmes méthodes que celles qui sont disponibles dans hello [.NET SDK de concentrateurs de Notification](http://msdn.microsoft.com/library/jj933431.aspx), cela vous permettra de toodirectly traduit tous les didacticiels de hello et exemples actuellement disponibles sur ce site, et par la Communauté hello sur hello internet.

Vous trouverez tout code hello disponible dans hello [exemple de wrapper PHP reste].

Par exemple, toocreate un client :

    $hub = new NotificationHub("connection string", "hubname");    

toosend une notification native iOS :

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a>Implémentation
Si vous n’avez pas déjà, suivez notre [didacticiel Get] toohello dernière section dans laquelle vous avez tooimplement hello principal vers le haut.
En outre, si vous souhaitez que vous pouvez utiliser le code hello hello [exemple de wrapper PHP reste] et accédez directement toohello [didacticiel de hello complète](#complete-tutorial) section.

Tous les hello tooimplement détails se trouvent sur un wrapper reste complète [MSDN](http://msdn.microsoft.com/library/dn530746.aspx). Dans cette section, nous allons examiner mise en œuvre de PHP hello de hello étapes principales tooaccess requis points de terminaison REST de concentrateurs de Notification :

1. Analyser la chaîne de connexion hello
2. Générer le jeton d’autorisation hello
3. Effectuer l’appel de hello HTTP

### <a name="parse-hello-connection-string"></a>Analyser la chaîne de connexion hello
Voici hello classe principale application hello client, dont le constructeur qui analyse la chaîne de connexion hello :

    class NotificationHub {
        const API_VERSION = "?api-version=2013-10";

        private $endpoint;
        private $hubPath;
        private $sasKeyName;
        private $sasKeyValue;

        function __construct($connectionString, $hubPath) {
            $this->hubPath = $hubPath;

            $this->parseConnectionString($connectionString);
        }

        private function parseConnectionString($connectionString) {
            $parts = explode(";", $connectionString);
            if (sizeof($parts) != 3) {
                throw new Exception("Error parsing connection string: " . $connectionString);
            }

            foreach ($parts as $part) {
                if (strpos($part, "Endpoint") === 0) {
                    $this->endpoint = "https" . substr($part, 11);
                } else if (strpos($part, "SharedAccessKeyName") === 0) {
                    $this->sasKeyName = substr($part, 20);
                } else if (strpos($part, "SharedAccessKey") === 0) {
                    $this->sasKeyValue = substr($part, 16);
                }
            }
        }
    }


### <a name="create-security-token"></a>Création du jeton de sécurité
Détails de Hello de création de jetons de sécurité hello sont disponibles [ici](http://msdn.microsoft.com/library/dn495627.aspx).
méthode suivante Hello a toobe ajouté toohello **NotificationHub** jeton de classe toocreate hello selon hello URI de demande en cours de hello et les informations d’identification hello extraites à partir de la chaîne de connexion hello.

    private function generateSasToken($uri) {
        $targetUri = strtolower(rawurlencode(strtolower($uri)));

        $expires = time();
        $expiresInMins = 60;
        $expires = $expires + $expiresInMins * 60;
        $toSign = $targetUri . "\n" . $expires;

        $signature = rawurlencode(base64_encode(hash_hmac('sha256', $toSign, $this->sasKeyValue, TRUE)));

        $token = "SharedAccessSignature sr=" . $targetUri . "&sig="
                    . $signature . "&se=" . $expires . "&skn=" . $this->sasKeyName;

        return $token;
    }

### <a name="send-a-notification"></a>Envoi d’une notification
Commençons par définir une classe représentant une notification.

    class Notification {
        public $format;
        public $payload;

        # array with keynames for headers
        # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
        # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
        public $headers;

        function __construct($format, $payload) {
            if (!in_array($format, ["template", "apple", "windows", "gcm", "windowsphone"])) {
                throw new Exception('Invalid format: ' . $format);
            }

            $this->format = $format;
            $this->payload = $payload;
        }
    }

Cette classe est un conteneur pour un corps de notification natif ou un ensemble de propriétés dans le cas d'un modèle de notification, et un ensemble d'en-têtes contenant le format (plateforme native ou modèle) et des propriétés spécifiques de la plateforme (telles que la propriété expiration d'Apple et les en-têtes WNS).

Reportez-vous toohello [documentation de l’API REST de concentrateurs Notification](http://msdn.microsoft.com/library/dn495827.aspx) et hello les formats des plateformes de notification spécifique pour tous les hello options disponibles.

Grâce à cette classe, nous pouvons maintenant écrire hello envoi des méthodes de notification à l’intérieur de hello **NotificationHub** classe.

    public function sendNotification($notification, $tagsOrTagExpression="") {
        if (is_array($tagsOrTagExpression)) {
            $tagExpression = implode(" || ", $tagsOrTagExpression);
        } else {
            $tagExpression = $tagsOrTagExpression;
        }

        # build uri
        $uri = $this->endpoint . $this->hubPath . "/messages" . NotificationHub::API_VERSION;
        $ch = curl_init($uri);

        if (in_array($notification->format, ["template", "apple", "gcm"])) {
            $contentType = "application/json";
        } else {
            $contentType = "application/xml";
        }

        $token = $this->generateSasToken($uri);

        $headers = [
            'Authorization: '.$token,
            'Content-Type: '.$contentType,
            'ServiceBusNotification-Format: '.$notification->format
        ];

        if ("" !== $tagExpression) {
            $headers[] = 'ServiceBusNotification-Tags: '.$tagExpression;
        }

        # add headers for other platforms
        if (is_array($notification->headers)) {
            $headers = array_merge($headers, $notification->headers);
        }

        curl_setopt_array($ch, array(
            CURLOPT_POST => TRUE,
            CURLOPT_RETURNTRANSFER => TRUE,
            CURLOPT_SSL_VERIFYPEER => FALSE,
            CURLOPT_HTTPHEADER => $headers,
            CURLOPT_POSTFIELDS => $notification->payload
        ));

        // Send hello request
        $response = curl_exec($ch);

        // Check for errors
        if($response === FALSE){
            throw new Exception(curl_error($ch));
        }

        $info = curl_getinfo($ch);

        if ($info['http_code'] <> 201) {
            throw new Exception('Error sending notificaiton: '. $info['http_code'] . ' msg: ' . $response);
        }
    } 

Hello au-dessus de méthodes d’envoyer une requête HTTP POST demande toohello /messages point de terminaison de votre concentrateur de notification avec corps correct de hello et notification de hello toosend en-têtes.

## <a name="complete-tutorial"></a>Didacticiel de hello terminée
Maintenant, vous pouvez effectuer didacticiel de mise en route de hello en envoyant des notifications de hello depuis un PHP back-end.

Initialiser vos concentrateurs de Notification de client (remplacez le nom de hub et la chaîne de connexion hello comme indiqué dans hello [didacticiel Get]) :

    $hub = new NotificationHub("connection string", "hubname");    

Ajoutez ensuite du code d’envoi hello selon votre plateforme mobile cible.

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a>Windows Store et Windows Phone 8.1 (non-Silverlight)
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a>iOS
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a>Android
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a>Windows Phone 8.0 et 8.1 Silverlight
    $toast = '<?xml version="1.0" encoding="utf-8"?>' .
                '<wp:Notification xmlns:wp="WPNotification">' .
                   '<wp:Toast>' .
                        '<wp:Text1>Hello from PHP!</wp:Text1>' .
                   '</wp:Toast> ' .
                '</wp:Notification>';
    $notification = new Notification("windowsphone", $toast);
    $notification->headers[] = 'X-WindowsPhone-Target : toast';
    $notification->headers[] = 'X-NotificationClass : 2';
    $hub->sendNotification($notification, null);


### <a name="kindle-fire"></a>Kindle Fire
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

L'exécution de votre code PHP produit normalement une notification qui apparaît sur votre appareil cible.

## <a name="next-steps"></a>Étapes suivantes
Dans cette rubrique, nous vous avons montré comment toocreate REST simple Java client pour les concentrateurs de Notification. À ce stade, vous pouvez :

* Télécharger hello complète [exemple de wrapper PHP reste], qui contient tout code hello ci-dessus.
* Continuer à découvrir des concentrateurs de Notification marquage fonctionnalité Bonjour [didacticiel dernières nouvelles]
* En savoir plus sur l’envoi de notifications tooindividual les utilisateurs dans [didacticiel d’avertir les utilisateurs]

Pour plus d’informations, consultez également hello [centre de développement PHP](/develop/php/).

[exemple de wrapper PHP reste]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php
[didacticiel Get]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/

