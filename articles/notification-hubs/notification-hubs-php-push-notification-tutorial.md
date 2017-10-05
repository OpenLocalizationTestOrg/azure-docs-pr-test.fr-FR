---
title: Utilisation de Notification Hubs avec PHP
description: "Découvrez comment utiliser Azure Notification Hubs à partir d’un serveur principal PHP."
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
ms.openlocfilehash: c27b6308ff528224a0398e0ff40537db05417bb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-notification-hubs-from-php"></a><span data-ttu-id="cb0d9-103">Utilisation de Notification Hubs à partir de PHP</span><span class="sxs-lookup"><span data-stu-id="cb0d9-103">How to use Notification Hubs from PHP</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="cb0d9-104">Vous pouvez accéder à toutes les fonctionnalités de Notification Hubs à partir d'un serveur principal Java/PHP/Ruby en utilisant l'interface REST des hubs de notifications, comme décrit dans la rubrique MSDN [API REST de Notification Hubs](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb0d9-104">You can access all Notification Hubs features from a Java/PHP/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

<span data-ttu-id="cb0d9-105">Dans cette rubrique, nous vous montrons comment :</span><span class="sxs-lookup"><span data-stu-id="cb0d9-105">In this topic we show how to:</span></span>

* <span data-ttu-id="cb0d9-106">créer un client REST pour les fonctionnalités de Notification Hubs en PHP ;</span><span class="sxs-lookup"><span data-stu-id="cb0d9-106">Build a REST client for Notification Hubs features in PHP;</span></span>
* <span data-ttu-id="cb0d9-107">suivre le [didacticiel de prise en main](notification-hubs-ios-apple-push-notification-apns-get-started.md) pour la plateforme mobile de votre choix, en implémentant la partie concernant le serveur principal en PHP.</span><span class="sxs-lookup"><span data-stu-id="cb0d9-107">Follow the [Get started tutorial](notification-hubs-ios-apple-push-notification-apns-get-started.md) for your mobile platform of choice, implementing the back-end portion in PHP.</span></span>

## <a name="client-interface"></a><span data-ttu-id="cb0d9-108">Interface client</span><span class="sxs-lookup"><span data-stu-id="cb0d9-108">Client interface</span></span>
<span data-ttu-id="cb0d9-109">L'interface client principale peut fournir les mêmes méthodes que celles disponibles dans le [Kit de développement logiciel (SDK) .NET Notification Hubs](http://msdn.microsoft.com/library/jj933431.aspx), ce qui vous permet de traduire directement l'ensemble des didacticiels et des exemples actuellement disponibles sur ce site, enrichis par les contributions de la communauté Internet.</span><span class="sxs-lookup"><span data-stu-id="cb0d9-109">The main client interface can provide the same methods that are available in the [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx), this will allow you to directly translate all the tutorials and samples currently available on this site, and contributed by the community on the internet.</span></span>

<span data-ttu-id="cb0d9-110">Tout le code est disponible dans l' [l’exemple de wrapper PHP REST].</span><span class="sxs-lookup"><span data-stu-id="cb0d9-110">You can find all the code available in the [PHP REST wrapper sample].</span></span>

<span data-ttu-id="cb0d9-111">Par exemple, pour créer un client :</span><span class="sxs-lookup"><span data-stu-id="cb0d9-111">For example, to create a client:</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="cb0d9-112">Pour envoyer une notification iOS native :</span><span class="sxs-lookup"><span data-stu-id="cb0d9-112">To send an iOS native notification:</span></span>

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a><span data-ttu-id="cb0d9-113">Implémentation</span><span class="sxs-lookup"><span data-stu-id="cb0d9-113">Implementation</span></span>
<span data-ttu-id="cb0d9-114">Si ce n'est déjà fait, suivez notre [didacticiel de prise en main] jusqu'à la dernière section, dans laquelle vous devrez implémenter le serveur principal.</span><span class="sxs-lookup"><span data-stu-id="cb0d9-114">If you did not already, please follow our [Get started tutorial] up to the last section where you have to implement the back-end.</span></span>
<span data-ttu-id="cb0d9-115">En outre, si vous le souhaitez, vous pouvez utiliser le code de [l’exemple de wrapper PHP REST] et accéder directement à la section du didacticiel [Suivi du didacticiel](#complete-tutorial).</span><span class="sxs-lookup"><span data-stu-id="cb0d9-115">Also, if you want you can use the code from the [PHP REST wrapper sample] and go directly to the [Complete the tutorial](#complete-tutorial) section.</span></span>

<span data-ttu-id="cb0d9-116">Tous les détails de l'implémentation d'un wrapper REST complet se trouvent sur [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb0d9-116">All the details to implement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="cb0d9-117">Dans cette section, nous allons décrire l'implémentation PHP des principales étapes requises pour accéder aux point de terminaison REST de Notification Hubs :</span><span class="sxs-lookup"><span data-stu-id="cb0d9-117">In this section we will describe the PHP implementation of the main steps required to access Notification Hubs REST endpoints:</span></span>

1. <span data-ttu-id="cb0d9-118">Analyse de la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="cb0d9-118">Parse the connection string</span></span>
2. <span data-ttu-id="cb0d9-119">Génération du jeton d'autorisation</span><span class="sxs-lookup"><span data-stu-id="cb0d9-119">Generate the authorization token</span></span>
3. <span data-ttu-id="cb0d9-120">Réalisation de l'appel HTTP</span><span class="sxs-lookup"><span data-stu-id="cb0d9-120">Perform the HTTP call</span></span>

### <a name="parse-the-connection-string"></a><span data-ttu-id="cb0d9-121">Analyse de la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="cb0d9-121">Parse the connection string</span></span>
<span data-ttu-id="cb0d9-122">Voici la classe principale implémentant le client, dont le constructeur analyse la chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="cb0d9-122">Here is the main class implementing the client, whose constructor that parses the connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="cb0d9-123">Création du jeton de sécurité</span><span class="sxs-lookup"><span data-stu-id="cb0d9-123">Create security token</span></span>
<span data-ttu-id="cb0d9-124">Les détails concernant la création d'un jeton de sécurité sont disponibles [ici](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb0d9-124">The details of the security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="cb0d9-125">La méthode suivante doit être ajoutée à la classe **NotificationHub** pour créer le jeton à partir de l'URI de la demande actuelle et des informations d'identification extraites de la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="cb0d9-125">The following method has to be added to the **NotificationHub** class to create the token based on the URI of the current request and the credentials extracted from the connection string.</span></span>

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

### <a name="send-a-notification"></a><span data-ttu-id="cb0d9-126">Envoi d’une notification</span><span class="sxs-lookup"><span data-stu-id="cb0d9-126">Send a notification</span></span>
<span data-ttu-id="cb0d9-127">Commençons par définir une classe représentant une notification.</span><span class="sxs-lookup"><span data-stu-id="cb0d9-127">First, let us define a class representing a notification.</span></span>

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

<span data-ttu-id="cb0d9-128">Cette classe est un conteneur pour un corps de notification natif ou un ensemble de propriétés dans le cas d'un modèle de notification, et un ensemble d'en-têtes contenant le format (plateforme native ou modèle) et des propriétés spécifiques de la plateforme (telles que la propriété expiration d'Apple et les en-têtes WNS).</span><span class="sxs-lookup"><span data-stu-id="cb0d9-128">This class is a container for a native notification body, or a set of properties on case of a template notification, and a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="cb0d9-129">Pour connaître toutes les options disponibles, reportez-vous à la [documentation sur les API REST de Notification Hubs](http://msdn.microsoft.com/library/dn495827.aspx) et aux formats spécifiques des plateformes de notification.</span><span class="sxs-lookup"><span data-stu-id="cb0d9-129">Please refer to the [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and the specific notification platforms' formats for all the options available.</span></span>

<span data-ttu-id="cb0d9-130">Munis de cette classe, nous pouvons à présent écrire les méthodes d'envoi des notifications à l'intérieur de la classe **NotificationHub** .</span><span class="sxs-lookup"><span data-stu-id="cb0d9-130">Armed with this class, we can now write the send notification methods inside of the **NotificationHub** class.</span></span>

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

        // Send the request
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

<span data-ttu-id="cb0d9-131">Les méthodes ci-dessus envoient une demande POST HTTP au point de terminaison /messages de votre hub de notification, avec le corps et les en-têtes corrects pour envoyer la notification.</span><span class="sxs-lookup"><span data-stu-id="cb0d9-131">The above methods send an HTTP POST request to the /messages endpoint of your notification hub, with the correct body and headers to send the notification.</span></span>

## <span data-ttu-id="cb0d9-132"><a name="complete-tutorial"></a>Suivi du didacticiel</span><span class="sxs-lookup"><span data-stu-id="cb0d9-132"><a name="complete-tutorial"></a>Complete the tutorial</span></span>
<span data-ttu-id="cb0d9-133">Vous pouvez à présent suivre le didacticiel de prise en main en envoyant la notification à partir d’un serveur principal PHP.</span><span class="sxs-lookup"><span data-stu-id="cb0d9-133">Now you can complete the Get Started tutorial by sending the notification from a PHP back-end.</span></span>

<span data-ttu-id="cb0d9-134">Initialisez votre client Notification Hubs (remplacez la chaîne de connexion et le nom du concentrateur comme indiqué dans le [didacticiel de prise en main]) :</span><span class="sxs-lookup"><span data-stu-id="cb0d9-134">Initialize your Notification Hubs client (substitute the connection string and hub name as instructed in the [Get started tutorial]):</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="cb0d9-135">Ajoutez ensuite le code d'envoi en fonction de la plateforme mobile cible.</span><span class="sxs-lookup"><span data-stu-id="cb0d9-135">Then add the send code depending on your target mobile platform.</span></span>

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="cb0d9-136">Windows Store et Windows Phone 8.1 (non-Silverlight)</span><span class="sxs-lookup"><span data-stu-id="cb0d9-136">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a><span data-ttu-id="cb0d9-137">iOS</span><span class="sxs-lookup"><span data-stu-id="cb0d9-137">iOS</span></span>
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a><span data-ttu-id="cb0d9-138">Android</span><span class="sxs-lookup"><span data-stu-id="cb0d9-138">Android</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="cb0d9-139">Windows Phone 8.0 et 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="cb0d9-139">Windows Phone 8.0 and 8.1 Silverlight</span></span>
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


### <a name="kindle-fire"></a><span data-ttu-id="cb0d9-140">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="cb0d9-140">Kindle Fire</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

<span data-ttu-id="cb0d9-141">L'exécution de votre code PHP produit normalement une notification qui apparaît sur votre appareil cible.</span><span class="sxs-lookup"><span data-stu-id="cb0d9-141">Running your PHP code should produce now a notification appearing on your target device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb0d9-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cb0d9-142">Next Steps</span></span>
<span data-ttu-id="cb0d9-143">Dans cette rubrique, nous vous avons montré comment créer un client REST Java simple pour Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="cb0d9-143">In this topic we showed how to create a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="cb0d9-144">À ce stade, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="cb0d9-144">From here you can:</span></span>

* <span data-ttu-id="cb0d9-145">télécharger l'intégralité de l' [l’exemple de wrapper PHP REST], qui contient tout le code ci-dessus ;</span><span class="sxs-lookup"><span data-stu-id="cb0d9-145">Download the full [PHP REST wrapper sample], which contains all the code above.</span></span>
* <span data-ttu-id="cb0d9-146">poursuivre l'apprentissage de la fonction de balisage dans le [didacticiel Nouvelles de dernière minute] ;</span><span class="sxs-lookup"><span data-stu-id="cb0d9-146">Continue learning about Notification Hubs tagging feature in the [Breaking News tutorial]</span></span>
* <span data-ttu-id="cb0d9-147">vous familiariser avec l'envoi de notifications Push à des utilisateurs individuels dans le [didacticiel Envoi de notifications à des utilisateurs]</span><span class="sxs-lookup"><span data-stu-id="cb0d9-147">Learn about pushing notifications to individual users in [Notify Users tutorial]</span></span>

<span data-ttu-id="cb0d9-148">Pour plus d’informations, consultez également le [Centre pour développeurs PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="cb0d9-148">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="cb0d9-149">[l’exemple de wrapper PHP REST]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php</span><span class="sxs-lookup"><span data-stu-id="cb0d9-149">[PHP REST wrapper sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php</span></span>
<span data-ttu-id="cb0d9-150">[didacticiel de prise en main]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/</span><span class="sxs-lookup"><span data-stu-id="cb0d9-150">[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/</span></span>

