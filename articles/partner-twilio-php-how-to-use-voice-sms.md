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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-php"></a><span data-ttu-id="236fa-104">Comment tooUse Twilio pour les fonctionnalités de SMS en PHP et de la voix</span><span class="sxs-lookup"><span data-stu-id="236fa-104">How tooUse Twilio for Voice and SMS Capabilities in PHP</span></span>
<span data-ttu-id="236fa-105">Ce guide montre comment tooperform des tâches de programmation courantes avec hello Twilio API de service sur Azure.</span><span class="sxs-lookup"><span data-stu-id="236fa-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="236fa-106">scénarios de Hello couvertes incluent un appel téléphonique et envoi d’un message de Service SMS (Short Message).</span><span class="sxs-lookup"><span data-stu-id="236fa-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="236fa-107">Pour plus d’informations sur Twilio et à l’aide de la voix et SMS dans vos applications, consultez hello [étapes](#NextSteps) section.</span><span class="sxs-lookup"><span data-stu-id="236fa-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="236fa-108"><a id="WhatIs"></a>Présentation de Twilio</span><span class="sxs-lookup"><span data-stu-id="236fa-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="236fa-109">Twilio est futures hello de communications professionnelles de mise sous tension, l’activation de voix de tooembed les développeurs, VoIP et dans les applications de messagerie.</span><span class="sxs-lookup"><span data-stu-id="236fa-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="236fa-110">La virtualisation toute infrastructure nécessaires dans un environnement en nuage, global, exposant via la plateforme de hello Twilio communications API.</span><span class="sxs-lookup"><span data-stu-id="236fa-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="236fa-111">Les applications sont toobuild simple et évolutive.</span><span class="sxs-lookup"><span data-stu-id="236fa-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="236fa-112">Tirez parti de la souplesse du paiement à l'utilisation et de la fiabilité du cloud.</span><span class="sxs-lookup"><span data-stu-id="236fa-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="236fa-113">**Twilio vocal** permet à votre toomake d’applications et de recevoir des appels téléphoniques.</span><span class="sxs-lookup"><span data-stu-id="236fa-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="236fa-114">**Twilio SMS** Active toosend de votre application et de recevoir des messages texte.</span><span class="sxs-lookup"><span data-stu-id="236fa-114">**Twilio SMS** enables your application toosend and receive text messages.</span></span> <span data-ttu-id="236fa-115">**Client twilio sur** vous permet d’appels de VoIP toomake à partir de n’importe quel téléphone, tablette ou un navigateur et prend en charge WebRTC.</span><span class="sxs-lookup"><span data-stu-id="236fa-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="236fa-116"><a id="Pricing"></a>Tarification de Twilio et offres spéciales</span><span class="sxs-lookup"><span data-stu-id="236fa-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="236fa-117">Les clients Azure reçoivent une [offre spéciale](http://www.twilio.com/azure)de 10 $ en crédit Twilio lorsqu'ils mettent à niveau leur compte Twilio.</span><span class="sxs-lookup"><span data-stu-id="236fa-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="236fa-118">Ce Twilio crédit peut être appliqué tooany l’utilisation de Twilio (10 $ crédit équivalent toosending jusqu'à 1 000 messages SMS et la réception des too1000 entrants voix minutes, selon emplacement hello de votre destination de nombre et de message ou d’appel téléphonique).</span><span class="sxs-lookup"><span data-stu-id="236fa-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="236fa-119">Profitez de ce crédit Twilio et démarrez en consultant la page : [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="236fa-119">Redeem this Twilio credit and get started at: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="236fa-120">Twilio est un service de paiement à l'utilisation.</span><span class="sxs-lookup"><span data-stu-id="236fa-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="236fa-121">Il n'existe pas de frais d'entrée et vous pouvez fermer votre compte quand vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="236fa-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="236fa-122">Pour plus d’informations, consultez la page [Tarification de Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="236fa-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="236fa-123"><a id="Concepts"></a>Concepts</span><span class="sxs-lookup"><span data-stu-id="236fa-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="236fa-124">Hello Twilio API est une API RESTful qui fournit la voix et fonctionnalités SMS pour les applications.</span><span class="sxs-lookup"><span data-stu-id="236fa-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="236fa-125">Les bibliothèques clientes sont disponibles dans plusieurs langues : pour en obtenir la liste, consultez la page [Bibliothèques de l’API Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="236fa-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="236fa-126">Les principaux aspects du hello Twilio API sont Twilio verbes et Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="236fa-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="236fa-127"><a id="Verbs"></a>Verbes Twilio</span><span class="sxs-lookup"><span data-stu-id="236fa-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="236fa-128">Hello API se sert de Twilio verbes ; par exemple, hello  **&lt;prononcer&gt;**  verbe fait en sorte que Twilio tooaudibly remettre un message sur un appel.</span><span class="sxs-lookup"><span data-stu-id="236fa-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="236fa-129">Hello Voici une liste de verbes de Twilio.</span><span class="sxs-lookup"><span data-stu-id="236fa-129">hello following is a list of Twilio verbs.</span></span> <span data-ttu-id="236fa-130">En savoir plus sur hello autres verbes et les fonctionnalités via [documentation de langage de balisage Twilio](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="236fa-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="236fa-131">**&lt;Accès à distance&gt;**: se connecte phone de tooanother hello appelant.</span><span class="sxs-lookup"><span data-stu-id="236fa-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="236fa-132">**&lt;Collecter des&gt;**: collecte les chiffres entrés sur le clavier de téléphone hello.</span><span class="sxs-lookup"><span data-stu-id="236fa-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="236fa-133">**&lt;Hangup&gt;** : met fin à un appel.</span><span class="sxs-lookup"><span data-stu-id="236fa-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="236fa-134">**&lt;Play&gt;** : lit un fichier audio.</span><span class="sxs-lookup"><span data-stu-id="236fa-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="236fa-135">**&lt;Pause&gt;** : patiente silencieusement pendant un nombre déterminé de secondes.</span><span class="sxs-lookup"><span data-stu-id="236fa-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="236fa-136">**&lt;Enregistrement&gt;**: enregistre la voix de l’appelant hello et retourne une URL d’un fichier contenant un enregistrement de hello.</span><span class="sxs-lookup"><span data-stu-id="236fa-136">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="236fa-137">**&lt;Rediriger&gt;**: transfère le contrôle d’un appel ou un SMS toohello TwiML à une autre URL.</span><span class="sxs-lookup"><span data-stu-id="236fa-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="236fa-138">**&lt;Rejeter&gt;**: rejette un entrant appeler tooyour Twilio nombre sans vous de facturation</span><span class="sxs-lookup"><span data-stu-id="236fa-138">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="236fa-139">**&lt;Par exemple&gt;**: toospeech texte convertit effectuée sur un appel.</span><span class="sxs-lookup"><span data-stu-id="236fa-139">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="236fa-140">**&lt;Sms&gt;** : envoie un SMS.</span><span class="sxs-lookup"><span data-stu-id="236fa-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="236fa-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="236fa-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="236fa-142">TwiML est un ensemble d’instructions basé sur XML en fonction de verbes Twilio hello qui informent Twilio de façon tooprocess un appel ou un SMS.</span><span class="sxs-lookup"><span data-stu-id="236fa-142">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="236fa-143">Par exemple, hello suivant TwiML permet de convertir le texte hello **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="236fa-143">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="236fa-144">Lorsque votre application appelle hello Twilio API, un des paramètres d’API hello est hello URL qui renvoie la réponse de TwiML hello.</span><span class="sxs-lookup"><span data-stu-id="236fa-144">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="236fa-145">À des fins de développement, vous pouvez utiliser l’URL fournie par Twilio tooprovide hello TwiML les réponses employées par vos applications.</span><span class="sxs-lookup"><span data-stu-id="236fa-145">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="236fa-146">Vous pourriez également héberger vos réponses de TwiML URL tooproduce hello et une autre option consiste à toouse hello **TwiMLResponse** objet.</span><span class="sxs-lookup"><span data-stu-id="236fa-146">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="236fa-147">Pour plus d’informations sur les verbes Twilio, leurs attributs et le langage TwiML, consultez la page [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="236fa-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="236fa-148">Pour plus d’informations sur hello Twilio API, consultez [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="236fa-148">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="236fa-149"><a id="CreateAccount"></a>Créer un compte Twilio</span><span class="sxs-lookup"><span data-stu-id="236fa-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="236fa-150">Lorsque vous êtes prêt tooget un compte de Twilio, inscrivez-vous dans [essayez de Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="236fa-150">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="236fa-151">Vous pouvez commencer avec un compte gratuit, avant de le mettre à niveau ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="236fa-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="236fa-152">Lorsque vous créez un compte Twilio, vous recevez un ID de compte et un jeton d'authentification.</span><span class="sxs-lookup"><span data-stu-id="236fa-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="236fa-153">Les deux seront les appels d’API de Twilio toomake nécessaires.</span><span class="sxs-lookup"><span data-stu-id="236fa-153">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="236fa-154">tooprevent non autorisé à accéder à tooyour compte, de sécuriser votre jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="236fa-154">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="236fa-155">Votre ID de compte et l’authentification jeton peuvent être consultés à hello [page de compte Twilio][twilio_account], dans hello champs **SID de compte** et **dujetond’authentification**, respectivement.</span><span class="sxs-lookup"><span data-stu-id="236fa-155">Your account ID and authentication token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="236fa-156"><a id="create_app"></a>Création d’une application PHP</span><span class="sxs-lookup"><span data-stu-id="236fa-156"><a id="create_app"></a>Create a PHP Application</span></span>
<span data-ttu-id="236fa-157">Une application PHP qui utilise le service de Twilio hello et s’exécute dans Azure n’est pas différente de toute autre application PHP qui utilise le service de Twilio hello.</span><span class="sxs-lookup"><span data-stu-id="236fa-157">A PHP application that uses hello Twilio service and is running in Azure is no different than any other PHP application that uses hello Twilio service.</span></span> <span data-ttu-id="236fa-158">Twilio services sont basés sur REST et peuvent être appelées à partir de PHP de plusieurs façons, cet article se concentrera sur le fonctionnement des services avec toouse Twilio [bibliothèque Twilio pour PHP à partir de GitHub][twilio_php].</span><span class="sxs-lookup"><span data-stu-id="236fa-158">While Twilio services are REST-based and can be called from PHP in several ways, this article will focus on how toouse Twilio services with [Twilio library for PHP from GitHub][twilio_php].</span></span> <span data-ttu-id="236fa-159">Pour plus d’informations sur l’utilisation de la bibliothèque de Twilio hello pour PHP, consultez [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="236fa-159">For more information about using hello Twilio library for PHP, see [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="236fa-160">Obtenir des instructions détaillées pour créer et déployer un tooAzure d’application Twilio/PHP sont disponibles à [comment tooMake un Twilio à l’aide d’un appel téléphonique dans une Application PHP sur Azure][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="236fa-160">Detailed instructions for building and deploying a Twilio/PHP application tooAzure are available at [How tooMake a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="236fa-161"><a id="configure_app"></a>Configurez des bibliothèques de votre Application tooUse Twilio</span><span class="sxs-lookup"><span data-stu-id="236fa-161"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="236fa-162">Vous pouvez configurer votre bibliothèque de Twilio application toouse hello pour PHP de deux manières :</span><span class="sxs-lookup"><span data-stu-id="236fa-162">You can configure your application toouse hello Twilio library for PHP in two ways:</span></span>

1. <span data-ttu-id="236fa-163">Télécharger la bibliothèque de Twilio hello pour PHP à partir de GitHub ([https://github.com/twilio/twilio-php][twilio_php]) et ajoutez hello **Services** application tooyour d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="236fa-163">Download hello Twilio library for PHP from GitHub ([https://github.com/twilio/twilio-php][twilio_php]) and add hello **Services** directory tooyour application.</span></span>
   
    <span data-ttu-id="236fa-164">OU</span><span class="sxs-lookup"><span data-stu-id="236fa-164">-OR-</span></span>
2. <span data-ttu-id="236fa-165">Installer la bibliothèque de Twilio hello pour PHP en tant que package poire.</span><span class="sxs-lookup"><span data-stu-id="236fa-165">Install hello Twilio library for PHP as a PEAR package.</span></span> <span data-ttu-id="236fa-166">Il peut être installé avec hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="236fa-166">It can be installed with hello following commands:</span></span>
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

<span data-ttu-id="236fa-167">Une fois que vous avez installé la bibliothèque de Twilio hello pour PHP, vous pouvez ensuite ajouter un **require_once** instruction début hello de votre PHP fichiers bibliothèque de hello tooreference :</span><span class="sxs-lookup"><span data-stu-id="236fa-167">Once you have installed hello Twilio library for PHP, you can then add a **require_once** statement at hello top of your PHP files tooreference hello library:</span></span>

        require_once 'Services/Twilio.php';

<span data-ttu-id="236fa-168">Pour plus d’informations, consultez [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="236fa-168">For more information, see [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="236fa-169"><a id="howto_make_call"></a>Procédure : passer un appel sortant</span><span class="sxs-lookup"><span data-stu-id="236fa-169"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="236fa-170">Hello suivant montre comment toomake sortante appeler à l’aide de hello **Services_Twilio** classe.</span><span class="sxs-lookup"><span data-stu-id="236fa-170">hello following shows how toomake an outgoing call using hello **Services_Twilio** class.</span></span> <span data-ttu-id="236fa-171">Ce code utilise également un Bonjour de tooreturn site fournie par Twilio réponse de Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="236fa-171">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="236fa-172">Remplacez par vos valeurs hello **de** et **à** les numéros de téléphone et assurez-vous que vous vérifiez hello **à partir de** numéro de téléphone de votre code hello de Twilio compte toorunning préalable.</span><span class="sxs-lookup"><span data-stu-id="236fa-172">Substitute your values for hello **From** and **To** phone numbers, and ensure that you verify hello **From** phone number for your Twilio account prior toorunning hello code.</span></span>

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

<span data-ttu-id="236fa-173">Comme indiqué, ce code utilise un Bonjour de tooreturn TwiML réponse Twilio fournie par site.</span><span class="sxs-lookup"><span data-stu-id="236fa-173">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="236fa-174">Vous pouvez utiliser votre propre hello tooprovide de site TwiML réponse ; Pour plus d’informations, consultez [comment tooProvide TwiML les réponses à partir de votre propre Site Web](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="236fa-174">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

* <span data-ttu-id="236fa-175">**Remarque**: erreurs de validation de certificat SSL de tootroubleshoot, consultez [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span><span class="sxs-lookup"><span data-stu-id="236fa-175">**Note**: tootroubleshoot SSL certificate validation errors, see [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span></span> 

## <span data-ttu-id="236fa-176"><a id="howto_send_sms"></a>Procédure : envoi d'un message SMS</span><span class="sxs-lookup"><span data-stu-id="236fa-176"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="236fa-177">Hello suivant montre comment un message SMS à l’aide de toosend hello **Services_Twilio** classe.</span><span class="sxs-lookup"><span data-stu-id="236fa-177">hello following shows how toosend an SMS message using hello **Services_Twilio** class.</span></span> <span data-ttu-id="236fa-178">Hello **de** numéro est fourni par Twilio pour évaluation comptes toosend de SMS.</span><span class="sxs-lookup"><span data-stu-id="236fa-178">hello **From** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="236fa-179">Hello **à** nombre doit être vérifié pour votre code de hello Twilio compte toorunning préalable.</span><span class="sxs-lookup"><span data-stu-id="236fa-179">hello **To** number must be verified for your Twilio account prior toorunning hello code.</span></span>

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

## <span data-ttu-id="236fa-180"><a id="howto_provide_twiml_responses"></a>Procédure : envoi de réponses TwiML depuis votre propre site web</span><span class="sxs-lookup"><span data-stu-id="236fa-180"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="236fa-181">Lorsque votre application lance un appel de toohello Twilio API, Twilio enverra votre URL tooa demande attendu tooreturn une réponse TwiML.</span><span class="sxs-lookup"><span data-stu-id="236fa-181">When your application initiates a call toohello Twilio API, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="236fa-182">exemple Hello ci-dessus utilise les URL fournie par Twilio hello [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="236fa-182">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="236fa-183">(TwiML est conçu pour une utilisation par Twilio, vous pouvez afficher il hello dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="236fa-183">(While TwiML is designed for use by Twilio, you can view hello it in your browser.</span></span> <span data-ttu-id="236fa-184">Par exemple, cliquez sur [http://twimlets.com/message] [ twimlet_message_url] toosee vide `<Response>` élément ; un autre exemple, cliquez sur [http://twimlets.com/message? Message % 5B0 %5, D = Hello % 20World] [ twimlet_message_url_hello_world] toosee un `<Response>` élément contenant un `<Say>` élément.)</span><span class="sxs-lookup"><span data-stu-id="236fa-184">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] toosee a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="236fa-185">Au lieu d’utiliser les URL fournie par Twilio hello, vous pouvez créer votre propre site qui renvoie des réponses HTTP.</span><span class="sxs-lookup"><span data-stu-id="236fa-185">Instead of relying on hello Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="236fa-186">Vous pouvez créer le site de hello dans n’importe quel langage qui retourne les réponses XML ; Cette rubrique suppose que vous allez utiliser hello de toocreate PHP TwiML.</span><span class="sxs-lookup"><span data-stu-id="236fa-186">You can create hello site in any language that returns XML responses; this topic assumes you'll be using PHP toocreate hello TwiML.</span></span>

<span data-ttu-id="236fa-187">Hello suivant page PHP qui en résulte dans une réponse TwiML indiquant que **Hello World** sur l’appel de hello.</span><span class="sxs-lookup"><span data-stu-id="236fa-187">hello following PHP page results in a TwiML response that says **Hello World** on hello call.</span></span>

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

<span data-ttu-id="236fa-188">Comme vous pouvez le voir à partir de l’exemple hello ci-dessus, hello TwiML réponse est simplement un document XML.</span><span class="sxs-lookup"><span data-stu-id="236fa-188">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="236fa-189">bibliothèque de Twilio Hello pour PHP contient des classes qui génèrent TwiML pour vous.</span><span class="sxs-lookup"><span data-stu-id="236fa-189">hello Twilio library for PHP contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="236fa-190">exemple Hello ci-dessous génère réponse équivalent de hello comme indiqué ci-dessus, mais utilise hello **Services\_Twilio\_Twiml** classe dans la bibliothèque de Twilio hello pour PHP :</span><span class="sxs-lookup"><span data-stu-id="236fa-190">hello example below produces hello equivalent response as shown above, but uses hello **Services\_Twilio\_Twiml** class in hello Twilio library for PHP:</span></span>

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

<span data-ttu-id="236fa-191">Pour plus d’informations sur TwiML, consultez la page [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="236fa-191">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span> 

<span data-ttu-id="236fa-192">Une fois que vous avez votre page PHP configurer tooprovide TwiML réponses, utilisez des URL de hello de page PHP hello comme hello URL passée hello `Services_Twilio->account->calls->create` (méthode).</span><span class="sxs-lookup"><span data-stu-id="236fa-192">Once you have your PHP page set up tooprovide TwiML responses, use hello URL of hello PHP page as hello URL passed into hello  `Services_Twilio->account->calls->create`  method.</span></span> <span data-ttu-id="236fa-193">Par exemple, si vous avez une application Web nommée **MyTwiML** tooan déployé Azure le service hébergé, et le nom de la page PHP hello hello est **mytwiml.php**, hello URL peut être passé trop **Services_ Twilio -> comptes -> appels -> créer** comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="236fa-193">For example, if you have a Web application named **MyTwiML** deployed tooan Azure hosted service, and hello name of hello PHP page is **mytwiml.php**, hello URL can be passed too **Services_Twilio->account->calls->create**  as shown in hello following example:</span></span>

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

<span data-ttu-id="236fa-194">Pour plus d’informations sur l’utilisation de Twilio dans Azure avec PHP, consultez [comment tooMake un Twilio à l’aide d’un appel téléphonique dans une Application PHP sur Azure][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="236fa-194">For additional information about using Twilio in Azure with PHP, see [How tooMake a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="236fa-195"><a id="AdditionalServices"></a>Utilisation de services Twilio supplémentaires</span><span class="sxs-lookup"><span data-stu-id="236fa-195"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="236fa-196">En outre toohello les exemples indiqués ici, que twilio propose des API basées sur le web qui vous pouvez utiliser des fonctionnalités Twilio tooleverage supplémentaires à partir de votre application Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="236fa-196">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="236fa-197">Pour plus d’informations, consultez hello [documentation de l’API de Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="236fa-197">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="236fa-198"><a id="NextSteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="236fa-198"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="236fa-199">Maintenant que vous avez appris les notions de base de hello Hello Twilio service, suivez ces liens de toolearn plus :</span><span class="sxs-lookup"><span data-stu-id="236fa-199">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="236fa-200">[Conseils de sécurité Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="236fa-200">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="236fa-201">[Procédures et exemples de code Twilio][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="236fa-201">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="236fa-202">[Didacticiels de démarrage rapide Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="236fa-202">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="236fa-203">[Twilio sur GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="236fa-203">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="236fa-204">[Communiquer avec tooTwilio prise en charge][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="236fa-204">[Talk tooTwilio Support][twilio_support]</span></span>

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
