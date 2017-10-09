---
title: aaaHow tooUse Twilio pour la voix et SMS (PHP) | Documents Microsoft
description: "Découvrez comment toomake un appel téléphonique et envoyer un SMS de message avec le service de l’API de Twilio hello sur Azure. Exemples de code écrits en PHP."
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 007f22e3-ac75-4868-8315-da000c2e0dd0
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 9354df8de694826a0ff7ea92620ec4d7e5c2fd70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-php"></a>Comment tooUse Twilio pour les fonctionnalités de SMS en PHP et de la voix
Ce guide montre comment tooperform des tâches de programmation courantes avec hello Twilio API de service sur Azure. scénarios de Hello couvertes incluent un appel téléphonique et envoi d’un message de Service SMS (Short Message). Pour plus d’informations sur Twilio et à l’aide de la voix et SMS dans vos applications, consultez hello [étapes](#NextSteps) section.

## <a id="WhatIs"></a>Présentation de Twilio
Twilio est futures hello de communications professionnelles de mise sous tension, l’activation de voix de tooembed les développeurs, VoIP et dans les applications de messagerie. La virtualisation toute infrastructure nécessaires dans un environnement en nuage, global, exposant via la plateforme de hello Twilio communications API. Les applications sont toobuild simple et évolutive. Tirez parti de la souplesse du paiement à l'utilisation et de la fiabilité du cloud.

**Twilio vocal** permet à votre toomake d’applications et de recevoir des appels téléphoniques. **Twilio SMS** Active toosend de votre application et de recevoir des messages texte. **Client twilio sur** vous permet d’appels de VoIP toomake à partir de n’importe quel téléphone, tablette ou un navigateur et prend en charge WebRTC.

## <a id="Pricing"></a>Tarification de Twilio et offres spéciales
Les clients Azure reçoivent une [offre spéciale](http://www.twilio.com/azure)de 10 $ en crédit Twilio lorsqu'ils mettent à niveau leur compte Twilio. Ce Twilio crédit peut être appliqué tooany l’utilisation de Twilio (10 $ crédit équivalent toosending jusqu'à 1 000 messages SMS et la réception des too1000 entrants voix minutes, selon emplacement hello de votre destination de nombre et de message ou d’appel téléphonique). Profitez de ce crédit Twilio et démarrez en consultant la page : [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).

Twilio est un service de paiement à l'utilisation. Il n'existe pas de frais d'entrée et vous pouvez fermer votre compte quand vous le souhaitez. Pour plus d’informations, consultez la page [Tarification de Twilio][twilio_pricing].

## <a id="Concepts"></a>Concepts
Hello Twilio API est une API RESTful qui fournit la voix et fonctionnalités SMS pour les applications. Les bibliothèques clientes sont disponibles dans plusieurs langues : pour en obtenir la liste, consultez la page [Bibliothèques de l’API Twilio][twilio_libraries].

Les principaux aspects du hello Twilio API sont Twilio verbes et Twilio Markup Language (TwiML).

### <a id="Verbs"></a>Verbes Twilio
Hello API se sert de Twilio verbes ; par exemple, hello  **&lt;prononcer&gt;**  verbe fait en sorte que Twilio tooaudibly remettre un message sur un appel.

Hello Voici une liste de verbes de Twilio. En savoir plus sur hello autres verbes et les fonctionnalités via [documentation de langage de balisage Twilio](http://www.twilio.com/docs/api/twiml).

* **&lt;Accès à distance&gt;**: se connecte phone de tooanother hello appelant.
* **&lt;Collecter des&gt;**: collecte les chiffres entrés sur le clavier de téléphone hello.
* **&lt;Hangup&gt;** : met fin à un appel.
* **&lt;Play&gt;** : lit un fichier audio.
* **&lt;Pause&gt;** : patiente silencieusement pendant un nombre déterminé de secondes.
* **&lt;Enregistrement&gt;**: enregistre la voix de l’appelant hello et retourne une URL d’un fichier contenant un enregistrement de hello.
* **&lt;Rediriger&gt;**: transfère le contrôle d’un appel ou un SMS toohello TwiML à une autre URL.
* **&lt;Rejeter&gt;**: rejette un entrant appeler tooyour Twilio nombre sans vous de facturation
* **&lt;Par exemple&gt;**: toospeech texte convertit effectuée sur un appel.
* **&lt;Sms&gt;** : envoie un SMS.

### <a id="TwiML"></a>TwiML
TwiML est un ensemble d’instructions basé sur XML en fonction de verbes Twilio hello qui informent Twilio de façon tooprocess un appel ou un SMS.

Par exemple, hello suivant TwiML permet de convertir le texte hello **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

Lorsque votre application appelle hello Twilio API, un des paramètres d’API hello est hello URL qui renvoie la réponse de TwiML hello. À des fins de développement, vous pouvez utiliser l’URL fournie par Twilio tooprovide hello TwiML les réponses employées par vos applications. Vous pourriez également héberger vos réponses de TwiML URL tooproduce hello et une autre option consiste à toouse hello **TwiMLResponse** objet.

Pour plus d’informations sur les verbes Twilio, leurs attributs et le langage TwiML, consultez la page [TwiML][twiml]. Pour plus d’informations sur hello Twilio API, consultez [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Créer un compte Twilio
Lorsque vous êtes prêt tooget un compte de Twilio, inscrivez-vous dans [essayez de Twilio][try_twilio]. Vous pouvez commencer avec un compte gratuit, avant de le mettre à niveau ultérieurement.

Lorsque vous créez un compte Twilio, vous recevez un ID de compte et un jeton d'authentification. Les deux seront les appels d’API de Twilio toomake nécessaires. tooprevent non autorisé à accéder à tooyour compte, de sécuriser votre jeton d’authentification. Votre ID de compte et l’authentification jeton peuvent être consultés à hello [page de compte Twilio][twilio_account], dans hello champs **SID de compte** et **dujetond’authentification**, respectivement.

## <a id="create_app"></a>Création d’une application PHP
Une application PHP qui utilise le service de Twilio hello et s’exécute dans Azure n’est pas différente de toute autre application PHP qui utilise le service de Twilio hello. Twilio services sont basés sur REST et peuvent être appelées à partir de PHP de plusieurs façons, cet article se concentrera sur le fonctionnement des services avec toouse Twilio [bibliothèque Twilio pour PHP à partir de GitHub][twilio_php]. Pour plus d’informations sur l’utilisation de la bibliothèque de Twilio hello pour PHP, consultez [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].

Obtenir des instructions détaillées pour créer et déployer un tooAzure d’application Twilio/PHP sont disponibles à [comment tooMake un Twilio à l’aide d’un appel téléphonique dans une Application PHP sur Azure][howto_phonecall_php].

## <a id="configure_app"></a>Configurez des bibliothèques de votre Application tooUse Twilio
Vous pouvez configurer votre bibliothèque de Twilio application toouse hello pour PHP de deux manières :

1. Télécharger la bibliothèque de Twilio hello pour PHP à partir de GitHub ([https://github.com/twilio/twilio-php][twilio_php]) et ajoutez hello **Services** application tooyour d’annuaire.
   
    OU
2. Installer la bibliothèque de Twilio hello pour PHP en tant que package poire. Il peut être installé avec hello suivant de commandes :
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

Une fois que vous avez installé la bibliothèque de Twilio hello pour PHP, vous pouvez ensuite ajouter un **require_once** instruction début hello de votre PHP fichiers bibliothèque de hello tooreference :

        require_once 'Services/Twilio.php';

Pour plus d’informations, consultez [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].

## <a id="howto_make_call"></a>Procédure : passer un appel sortant
Hello suivant montre comment toomake sortante appeler à l’aide de hello **Services_Twilio** classe. Ce code utilise également un Bonjour de tooreturn site fournie par Twilio réponse de Twilio Markup Language (TwiML). Remplacez par vos valeurs hello **de** et **à** les numéros de téléphone et assurez-vous que vous vérifiez hello **à partir de** numéro de téléphone de votre code hello de Twilio compte toorunning préalable.

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";

    // hello number of hello phone initiating hello hello call.
    $from_number = "NNNNNNNNNNN";

    // hello number of hello phone receiving call.
    $to_number = "NNNNNNNNNNN";

    // Use hello Twilio-provided site for hello TwiML response.
    $url = "http://twimlets.com/message";

    // hello phone message text.
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    //Make hello call.
    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

Comme indiqué, ce code utilise un Bonjour de tooreturn TwiML réponse Twilio fournie par site. Vous pouvez utiliser votre propre hello tooprovide de site TwiML réponse ; Pour plus d’informations, consultez [comment tooProvide TwiML les réponses à partir de votre propre Site Web](#howto_provide_twiml_responses).

* **Remarque**: erreurs de validation de certificat SSL de tootroubleshoot, consultez [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation] 

## <a id="howto_send_sms"></a>Procédure : envoi d'un message SMS
Hello suivant montre comment un message SMS à l’aide de toosend hello **Services_Twilio** classe. Hello **de** numéro est fourni par Twilio pour évaluation comptes toosend de SMS. Hello **à** nombre doit être vérifié pour votre code de hello Twilio compte toorunning préalable.

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";


    $from_number = "NNNNNNNNNNN"; // With trial account, texts can only be sent from your Twilio number.
    $to_number = "NNNNNNNNNNN";
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    // Send hello SMS message.
    try
    {
        $client->$client->account->messages->sendMessage($from_number, $to_number, $message);
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

## <a id="howto_provide_twiml_responses"></a>Procédure : envoi de réponses TwiML depuis votre propre site web
Lorsque votre application lance un appel de toohello Twilio API, Twilio enverra votre URL tooa demande attendu tooreturn une réponse TwiML. exemple Hello ci-dessus utilise les URL fournie par Twilio hello [http://twimlets.com/message][twimlet_message_url]. (TwiML est conçu pour une utilisation par Twilio, vous pouvez afficher il hello dans votre navigateur. Par exemple, cliquez sur [http://twimlets.com/message] [ twimlet_message_url] toosee vide `<Response>` élément ; un autre exemple, cliquez sur [http://twimlets.com/message? Message % 5B0 %5, D = Hello % 20World] [ twimlet_message_url_hello_world] toosee un `<Response>` élément contenant un `<Say>` élément.)

Au lieu d’utiliser les URL fournie par Twilio hello, vous pouvez créer votre propre site qui renvoie des réponses HTTP. Vous pouvez créer le site de hello dans n’importe quel langage qui retourne les réponses XML ; Cette rubrique suppose que vous allez utiliser hello de toocreate PHP TwiML.

Hello suivant page PHP qui en résulte dans une réponse TwiML indiquant que **Hello World** sur l’appel de hello.

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

Comme vous pouvez le voir à partir de l’exemple hello ci-dessus, hello TwiML réponse est simplement un document XML. bibliothèque de Twilio Hello pour PHP contient des classes qui génèrent TwiML pour vous. exemple Hello ci-dessous génère réponse équivalent de hello comme indiqué ci-dessus, mais utilise hello **Services\_Twilio\_Twiml** classe dans la bibliothèque de Twilio hello pour PHP :

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

Pour plus d’informations sur TwiML, consultez la page [https://www.twilio.com/docs/api/twiml][twiml_reference]. 

Une fois que vous avez votre page PHP configurer tooprovide TwiML réponses, utilisez des URL de hello de page PHP hello comme hello URL passée hello `Services_Twilio->account->calls->create` (méthode). Par exemple, si vous avez une application Web nommée **MyTwiML** tooan déployé Azure le service hébergé, et le nom de la page PHP hello hello est **mytwiml.php**, hello URL peut être passé trop **Services_ Twilio -> comptes -> appels -> créer** comme indiqué dans hello l’exemple suivant :

    require_once 'Services/Twilio.php';

    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";
    $from_number = "NNNNNNNNNNN";
    $to_number = "NNNNNNNNNNN";
    $url = "http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.php";

    // hello phone message text.
    $message = "Hello world.";

    $client = new Services_Twilio($sid, $token, "2010-04-01");

    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

Pour plus d’informations sur l’utilisation de Twilio dans Azure avec PHP, consultez [comment tooMake un Twilio à l’aide d’un appel téléphonique dans une Application PHP sur Azure][howto_phonecall_php].

## <a id="AdditionalServices"></a>Utilisation de services Twilio supplémentaires
En outre toohello les exemples indiqués ici, que twilio propose des API basées sur le web qui vous pouvez utiliser des fonctionnalités Twilio tooleverage supplémentaires à partir de votre application Windows Azure. Pour plus d’informations, consultez hello [documentation de l’API de Twilio][twilio_api_documentation].

## <a id="NextSteps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello Hello Twilio service, suivez ces liens de toolearn plus :

* [Conseils de sécurité Twilio][twilio_security_guidelines]
* [Procédures et exemples de code Twilio][twilio_howtos]
* [Didacticiels de démarrage rapide Twilio][twilio_quickstarts] 
* [Twilio sur GitHub][twilio_on_github]
* [Communiquer avec tooTwilio prise en charge][twilio_support]

[twilio_php]: https://github.com/twilio/twilio-php
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-php/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-php/blob/master/README.md
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_api_service]: https://api.twilio.com
[howto_phonecall_php]: partner-twilio-php-make-phone-call.md
[twilio_voice_request]: https://www.twilio.com/docs/api/twiml/twilio_request
[twilio_sms_request]: https://www.twilio.com/docs/api/twiml/sms/twilio_request
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/user/account
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/api
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
