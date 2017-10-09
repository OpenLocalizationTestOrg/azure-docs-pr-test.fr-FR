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
# <a name="how-toouse-notification-hubs-from-php"></a><span data-ttu-id="5031e-103">Comment toouse concentrateurs de Notification à partir de PHP</span><span class="sxs-lookup"><span data-stu-id="5031e-103">How toouse Notification Hubs from PHP</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="5031e-104">Vous pouvez accéder à toutes les fonctionnalités de concentrateurs de Notification à partir d’un Java/PHP/Ruby back-end à l’aide d’interface REST de concentrateur de Notification de hello comme décrit dans la rubrique MSDN hello [API REST de concentrateurs de Notification](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="5031e-104">You can access all Notification Hubs features from a Java/PHP/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

<span data-ttu-id="5031e-105">Dans cette rubrique, nous vous montrons comment :</span><span class="sxs-lookup"><span data-stu-id="5031e-105">In this topic we show how to:</span></span>

* <span data-ttu-id="5031e-106">créer un client REST pour les fonctionnalités de Notification Hubs en PHP ;</span><span class="sxs-lookup"><span data-stu-id="5031e-106">Build a REST client for Notification Hubs features in PHP;</span></span>
* <span data-ttu-id="5031e-107">Suivez hello [didacticiel Get](notification-hubs-ios-apple-push-notification-apns-get-started.md) pour votre plateforme mobile de choix, l’implémentation de la partie des principaux de hello en PHP.</span><span class="sxs-lookup"><span data-stu-id="5031e-107">Follow hello [Get started tutorial](notification-hubs-ios-apple-push-notification-apns-get-started.md) for your mobile platform of choice, implementing hello back-end portion in PHP.</span></span>

## <a name="client-interface"></a><span data-ttu-id="5031e-108">Interface client</span><span class="sxs-lookup"><span data-stu-id="5031e-108">Client interface</span></span>
<span data-ttu-id="5031e-109">interface principale du client de Hello peut fournir hello mêmes méthodes que celles qui sont disponibles dans hello [.NET SDK de concentrateurs de Notification](http://msdn.microsoft.com/library/jj933431.aspx), cela vous permettra de toodirectly traduit tous les didacticiels de hello et exemples actuellement disponibles sur ce site, et par la Communauté hello sur hello internet.</span><span class="sxs-lookup"><span data-stu-id="5031e-109">hello main client interface can provide hello same methods that are available in hello [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx), this will allow you toodirectly translate all hello tutorials and samples currently available on this site, and contributed by hello community on hello internet.</span></span>

<span data-ttu-id="5031e-110">Vous trouverez tout code hello disponible dans hello [exemple de wrapper PHP reste].</span><span class="sxs-lookup"><span data-stu-id="5031e-110">You can find all hello code available in hello [PHP REST wrapper sample].</span></span>

<span data-ttu-id="5031e-111">Par exemple, toocreate un client :</span><span class="sxs-lookup"><span data-stu-id="5031e-111">For example, toocreate a client:</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="5031e-112">toosend une notification native iOS :</span><span class="sxs-lookup"><span data-stu-id="5031e-112">toosend an iOS native notification:</span></span>

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a><span data-ttu-id="5031e-113">Implémentation</span><span class="sxs-lookup"><span data-stu-id="5031e-113">Implementation</span></span>
<span data-ttu-id="5031e-114">Si vous n’avez pas déjà, suivez notre [didacticiel Get] toohello dernière section dans laquelle vous avez tooimplement hello principal vers le haut.</span><span class="sxs-lookup"><span data-stu-id="5031e-114">If you did not already, please follow our [Get started tutorial] up toohello last section where you have tooimplement hello back-end.</span></span>
<span data-ttu-id="5031e-115">En outre, si vous souhaitez que vous pouvez utiliser le code hello hello [exemple de wrapper PHP reste] et accédez directement toohello [didacticiel de hello complète](#complete-tutorial) section.</span><span class="sxs-lookup"><span data-stu-id="5031e-115">Also, if you want you can use hello code from hello [PHP REST wrapper sample] and go directly toohello [Complete hello tutorial](#complete-tutorial) section.</span></span>

<span data-ttu-id="5031e-116">Tous les hello tooimplement détails se trouvent sur un wrapper reste complète [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="5031e-116">All hello details tooimplement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="5031e-117">Dans cette section, nous allons examiner mise en œuvre de PHP hello de hello étapes principales tooaccess requis points de terminaison REST de concentrateurs de Notification :</span><span class="sxs-lookup"><span data-stu-id="5031e-117">In this section we will describe hello PHP implementation of hello main steps required tooaccess Notification Hubs REST endpoints:</span></span>

1. <span data-ttu-id="5031e-118">Analyser la chaîne de connexion hello</span><span class="sxs-lookup"><span data-stu-id="5031e-118">Parse hello connection string</span></span>
2. <span data-ttu-id="5031e-119">Générer le jeton d’autorisation hello</span><span class="sxs-lookup"><span data-stu-id="5031e-119">Generate hello authorization token</span></span>
3. <span data-ttu-id="5031e-120">Effectuer l’appel de hello HTTP</span><span class="sxs-lookup"><span data-stu-id="5031e-120">Perform hello HTTP call</span></span>

### <a name="parse-hello-connection-string"></a><span data-ttu-id="5031e-121">Analyser la chaîne de connexion hello</span><span class="sxs-lookup"><span data-stu-id="5031e-121">Parse hello connection string</span></span>
<span data-ttu-id="5031e-122">Voici hello classe principale application hello client, dont le constructeur qui analyse la chaîne de connexion hello :</span><span class="sxs-lookup"><span data-stu-id="5031e-122">Here is hello main class implementing hello client, whose constructor that parses hello connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="5031e-123">Création du jeton de sécurité</span><span class="sxs-lookup"><span data-stu-id="5031e-123">Create security token</span></span>
<span data-ttu-id="5031e-124">Détails de Hello de création de jetons de sécurité hello sont disponibles [ici](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="5031e-124">hello details of hello security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="5031e-125">méthode suivante Hello a toobe ajouté toohello **NotificationHub** jeton de classe toocreate hello selon hello URI de demande en cours de hello et les informations d’identification hello extraites à partir de la chaîne de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="5031e-125">hello following method has toobe added toohello **NotificationHub** class toocreate hello token based on hello URI of hello current request and hello credentials extracted from hello connection string.</span></span>

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

### <a name="send-a-notification"></a><span data-ttu-id="5031e-126">Envoi d’une notification</span><span class="sxs-lookup"><span data-stu-id="5031e-126">Send a notification</span></span>
<span data-ttu-id="5031e-127">Commençons par définir une classe représentant une notification.</span><span class="sxs-lookup"><span data-stu-id="5031e-127">First, let us define a class representing a notification.</span></span>

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

<span data-ttu-id="5031e-128">Cette classe est un conteneur pour un corps de notification natif ou un ensemble de propriétés dans le cas d'un modèle de notification, et un ensemble d'en-têtes contenant le format (plateforme native ou modèle) et des propriétés spécifiques de la plateforme (telles que la propriété expiration d'Apple et les en-têtes WNS).</span><span class="sxs-lookup"><span data-stu-id="5031e-128">This class is a container for a native notification body, or a set of properties on case of a template notification, and a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="5031e-129">Reportez-vous toohello [documentation de l’API REST de concentrateurs Notification](http://msdn.microsoft.com/library/dn495827.aspx) et hello les formats des plateformes de notification spécifique pour tous les hello options disponibles.</span><span class="sxs-lookup"><span data-stu-id="5031e-129">Please refer toohello [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and hello specific notification platforms' formats for all hello options available.</span></span>

<span data-ttu-id="5031e-130">Grâce à cette classe, nous pouvons maintenant écrire hello envoi des méthodes de notification à l’intérieur de hello **NotificationHub** classe.</span><span class="sxs-lookup"><span data-stu-id="5031e-130">Armed with this class, we can now write hello send notification methods inside of hello **NotificationHub** class.</span></span>

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

<span data-ttu-id="5031e-131">Hello au-dessus de méthodes d’envoyer une requête HTTP POST demande toohello /messages point de terminaison de votre concentrateur de notification avec corps correct de hello et notification de hello toosend en-têtes.</span><span class="sxs-lookup"><span data-stu-id="5031e-131">hello above methods send an HTTP POST request toohello /messages endpoint of your notification hub, with hello correct body and headers toosend hello notification.</span></span>

## <span data-ttu-id="5031e-132"><a name="complete-tutorial"></a>Didacticiel de hello terminée</span><span class="sxs-lookup"><span data-stu-id="5031e-132"><a name="complete-tutorial"></a>Complete hello tutorial</span></span>
<span data-ttu-id="5031e-133">Maintenant, vous pouvez effectuer didacticiel de mise en route de hello en envoyant des notifications de hello depuis un PHP back-end.</span><span class="sxs-lookup"><span data-stu-id="5031e-133">Now you can complete hello Get Started tutorial by sending hello notification from a PHP back-end.</span></span>

<span data-ttu-id="5031e-134">Initialiser vos concentrateurs de Notification de client (remplacez le nom de hub et la chaîne de connexion hello comme indiqué dans hello [didacticiel Get]) :</span><span class="sxs-lookup"><span data-stu-id="5031e-134">Initialize your Notification Hubs client (substitute hello connection string and hub name as instructed in hello [Get started tutorial]):</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="5031e-135">Ajoutez ensuite du code d’envoi hello selon votre plateforme mobile cible.</span><span class="sxs-lookup"><span data-stu-id="5031e-135">Then add hello send code depending on your target mobile platform.</span></span>

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="5031e-136">Windows Store et Windows Phone 8.1 (non-Silverlight)</span><span class="sxs-lookup"><span data-stu-id="5031e-136">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a><span data-ttu-id="5031e-137">iOS</span><span class="sxs-lookup"><span data-stu-id="5031e-137">iOS</span></span>
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a><span data-ttu-id="5031e-138">Android</span><span class="sxs-lookup"><span data-stu-id="5031e-138">Android</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="5031e-139">Windows Phone 8.0 et 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="5031e-139">Windows Phone 8.0 and 8.1 Silverlight</span></span>
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


### <a name="kindle-fire"></a><span data-ttu-id="5031e-140">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="5031e-140">Kindle Fire</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

<span data-ttu-id="5031e-141">L'exécution de votre code PHP produit normalement une notification qui apparaît sur votre appareil cible.</span><span class="sxs-lookup"><span data-stu-id="5031e-141">Running your PHP code should produce now a notification appearing on your target device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5031e-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5031e-142">Next Steps</span></span>
<span data-ttu-id="5031e-143">Dans cette rubrique, nous vous avons montré comment toocreate REST simple Java client pour les concentrateurs de Notification.</span><span class="sxs-lookup"><span data-stu-id="5031e-143">In this topic we showed how toocreate a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="5031e-144">À ce stade, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="5031e-144">From here you can:</span></span>

* <span data-ttu-id="5031e-145">Télécharger hello complète [exemple de wrapper PHP reste], qui contient tout code hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="5031e-145">Download hello full [PHP REST wrapper sample], which contains all hello code above.</span></span>
* <span data-ttu-id="5031e-146">Continuer à découvrir des concentrateurs de Notification marquage fonctionnalité Bonjour [didacticiel dernières nouvelles]</span><span class="sxs-lookup"><span data-stu-id="5031e-146">Continue learning about Notification Hubs tagging feature in hello [Breaking News tutorial]</span></span>
* <span data-ttu-id="5031e-147">En savoir plus sur l’envoi de notifications tooindividual les utilisateurs dans [didacticiel d’avertir les utilisateurs]</span><span class="sxs-lookup"><span data-stu-id="5031e-147">Learn about pushing notifications tooindividual users in [Notify Users tutorial]</span></span>

<span data-ttu-id="5031e-148">Pour plus d’informations, consultez également hello [centre de développement PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="5031e-148">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[exemple de wrapper PHP reste]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php
[didacticiel Get]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/

