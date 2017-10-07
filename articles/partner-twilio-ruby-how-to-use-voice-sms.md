---
title: aaaHow tooUse Twilio pour la voix et SMS (Ruby) | Documents Microsoft
description: "Découvrez comment toomake un appel téléphonique et envoyer un SMS de message avec le service de l’API de Twilio hello sur Azure. Exemples de code écrits en Ruby."
services: 
documentationcenter: ruby
author: devinrader
manager: twilio
editor: 
ms.assetid: 60e512f6-fa47-47c0-aedc-f19bb72a1158
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 11/25/2014
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: aca5ccb4663ff03c9c1f39c848469415f06dfb45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-ruby"></a><span data-ttu-id="06cc4-104">Comment tooUse Twilio pour la voix et les fonctionnalités de SMS dans Ruby</span><span class="sxs-lookup"><span data-stu-id="06cc4-104">How tooUse Twilio for Voice and SMS Capabilities in Ruby</span></span>
<span data-ttu-id="06cc4-105">Ce guide montre comment tooperform des tâches de programmation courantes avec hello Twilio API de service sur Azure.</span><span class="sxs-lookup"><span data-stu-id="06cc4-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="06cc4-106">scénarios de Hello couvertes incluent un appel téléphonique et envoi d’un message de Service SMS (Short Message).</span><span class="sxs-lookup"><span data-stu-id="06cc4-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="06cc4-107">Pour plus d’informations sur Twilio et à l’aide de la voix et SMS dans vos applications, consultez hello [étapes](#NextSteps) section.</span><span class="sxs-lookup"><span data-stu-id="06cc4-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="06cc4-108"><a id="WhatIs"></a>Présentation de Twilio</span><span class="sxs-lookup"><span data-stu-id="06cc4-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="06cc4-109">Twilio est une API de service web de téléphonie qui vous permet d’utiliser votre langages web existants et les voix toobuild de compétences et les applications de SMS.</span><span class="sxs-lookup"><span data-stu-id="06cc4-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills toobuild voice and SMS applications.</span></span> <span data-ttu-id="06cc4-110">Twilio est un service tiers, et non une fonctionnalité Azure ni un produit Microsoft.</span><span class="sxs-lookup"><span data-stu-id="06cc4-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="06cc4-111">**Twilio vocal** permet à votre toomake d’applications et de recevoir des appels téléphoniques.</span><span class="sxs-lookup"><span data-stu-id="06cc4-111">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="06cc4-112">**Twilio SMS** permet à votre toomake d’applications et de recevoir des messages SMS.</span><span class="sxs-lookup"><span data-stu-id="06cc4-112">**Twilio SMS** allows your applications toomake and receive SMS messages.</span></span> <span data-ttu-id="06cc4-113">**Client twilio sur** tooenable la communication vocale via les connexions Internet, y compris les connexions mobiles permet à vos applications.</span><span class="sxs-lookup"><span data-stu-id="06cc4-113">**Twilio Client** allows your applications tooenable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="06cc4-114"><a id="Pricing"></a>Tarification de Twilio et offres spéciales</span><span class="sxs-lookup"><span data-stu-id="06cc4-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="06cc4-115">Des informations sur les prix de Twilio sont disponibles dans la page [Tarification de Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="06cc4-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="06cc4-116">Les clients Azure reçoivent une [offre spéciale][special_offer] : un crédit gratuit de 1 000 SMS ou de 1 000 minutes d’appel en entrée.</span><span class="sxs-lookup"><span data-stu-id="06cc4-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="06cc4-117">toosign pour cette offre ou obtenir plus d’informations, visitez [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="06cc4-117">toosign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>  

## <span data-ttu-id="06cc4-118"><a id="Concepts"></a>Concepts</span><span class="sxs-lookup"><span data-stu-id="06cc4-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="06cc4-119">Hello Twilio API est une API RESTful qui fournit la voix et fonctionnalités SMS pour les applications.</span><span class="sxs-lookup"><span data-stu-id="06cc4-119">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="06cc4-120">Les bibliothèques clientes sont disponibles dans plusieurs langues : pour en obtenir la liste, consultez la page [Bibliothèques de l’API Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="06cc4-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

### <span data-ttu-id="06cc4-121"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="06cc4-121"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="06cc4-122">TwiML est un ensemble d’instructions basé sur XML qui informent Twilio de façon tooprocess un appel ou un SMS.</span><span class="sxs-lookup"><span data-stu-id="06cc4-122">TwiML is a set of XML-based instructions that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="06cc4-123">Par exemple, hello suivant TwiML permet de convertir le texte hello **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="06cc4-123">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="06cc4-124">Tous les documents TwiML ont un élément racine `<Response>` .</span><span class="sxs-lookup"><span data-stu-id="06cc4-124">All TwiML documents have `<Response>` as their root element.</span></span> <span data-ttu-id="06cc4-125">À partir de là, vous utilisez comportement de hello toodefine Twilio verbes de votre application.</span><span class="sxs-lookup"><span data-stu-id="06cc4-125">From there, you use Twilio Verbs toodefine hello behavior of your application.</span></span>

### <span data-ttu-id="06cc4-126"><a id="Verbs"></a>Verbes TwiML</span><span class="sxs-lookup"><span data-stu-id="06cc4-126"><a id="Verbs"></a>TwiML Verbs</span></span>
<span data-ttu-id="06cc4-127">Les verbes de Twilio sont des balises XML qui indiquent à Twilio que trop**faire**.</span><span class="sxs-lookup"><span data-stu-id="06cc4-127">Twilio Verbs are XML tags that tell Twilio what too**do**.</span></span> <span data-ttu-id="06cc4-128">Par exemple, hello  **&lt;prononcer&gt;**  verbe fait en sorte que Twilio tooaudibly remettre un message sur un appel.</span><span class="sxs-lookup"><span data-stu-id="06cc4-128">For example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span> 

<span data-ttu-id="06cc4-129">Hello Voici une liste de verbes de Twilio.</span><span class="sxs-lookup"><span data-stu-id="06cc4-129">hello following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="06cc4-130">**&lt;Accès à distance&gt;**: se connecte phone de tooanother hello appelant.</span><span class="sxs-lookup"><span data-stu-id="06cc4-130">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="06cc4-131">**&lt;Collecter des&gt;**: collecte les chiffres entrés sur le clavier de téléphone hello.</span><span class="sxs-lookup"><span data-stu-id="06cc4-131">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="06cc4-132">**&lt;Hangup&gt;** : met fin à un appel.</span><span class="sxs-lookup"><span data-stu-id="06cc4-132">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="06cc4-133">**&lt;Play&gt;** : lit un fichier audio.</span><span class="sxs-lookup"><span data-stu-id="06cc4-133">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="06cc4-134">**&lt;Pause&gt;** : patiente silencieusement pendant un nombre déterminé de secondes.</span><span class="sxs-lookup"><span data-stu-id="06cc4-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="06cc4-135">**&lt;Enregistrement&gt;**: enregistre la voix de l’appelant hello et retourne une URL d’un fichier contenant un enregistrement de hello.</span><span class="sxs-lookup"><span data-stu-id="06cc4-135">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="06cc4-136">**&lt;Rediriger&gt;**: transfère le contrôle d’un appel ou un SMS toohello TwiML à une autre URL.</span><span class="sxs-lookup"><span data-stu-id="06cc4-136">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="06cc4-137">**&lt;Rejeter&gt;**: rejette un entrant appeler tooyour Twilio nombre sans vous de facturation</span><span class="sxs-lookup"><span data-stu-id="06cc4-137">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="06cc4-138">**&lt;Par exemple&gt;**: toospeech texte convertit effectuée sur un appel.</span><span class="sxs-lookup"><span data-stu-id="06cc4-138">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="06cc4-139">**&lt;Sms&gt;** : envoie un SMS.</span><span class="sxs-lookup"><span data-stu-id="06cc4-139">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

<span data-ttu-id="06cc4-140">Pour plus d’informations sur les verbes Twilio, leurs attributs et le langage TwiML, consultez la page [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="06cc4-140">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="06cc4-141">Pour plus d’informations sur hello Twilio API, consultez [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="06cc4-141">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="06cc4-142"><a id="CreateAccount"></a>Créer un compte Twilio</span><span class="sxs-lookup"><span data-stu-id="06cc4-142"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="06cc4-143">Lorsque vous êtes prêt tooget un compte de Twilio, inscrivez-vous dans [essayez de Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="06cc4-143">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="06cc4-144">Vous pouvez commencer avec un compte gratuit, avant de le mettre à niveau ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="06cc4-144">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="06cc4-145">Lors de la création d'un compte Twilio, vous obtenez un numéro de téléphone gratuit pour votre application.</span><span class="sxs-lookup"><span data-stu-id="06cc4-145">When you sign up for a Twilio account, you'll get a free phone number for your application.</span></span> <span data-ttu-id="06cc4-146">Vous recevez également un SID de compte et un jeton d'authentification.</span><span class="sxs-lookup"><span data-stu-id="06cc4-146">You'll also receive an account SID and an auth token.</span></span> <span data-ttu-id="06cc4-147">Les deux seront les appels d’API de Twilio toomake nécessaires.</span><span class="sxs-lookup"><span data-stu-id="06cc4-147">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="06cc4-148">tooprevent non autorisé à accéder à tooyour compte, de sécuriser votre jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="06cc4-148">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="06cc4-149">Votre compte SID et le jeton d’authentification peuvent être consultés à hello [page de compte Twilio][twilio_account], dans hello champs **SID de compte** et **le jeton d’authentification** , respectivement.</span><span class="sxs-lookup"><span data-stu-id="06cc4-149">Your account SID and auth token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

### <span data-ttu-id="06cc4-150"><a id="VerifyPhoneNumbers"></a>Vérifier les numéros de téléphone</span><span class="sxs-lookup"><span data-stu-id="06cc4-150"><a id="VerifyPhoneNumbers"></a>Verify Phone Numbers</span></span>
<span data-ttu-id="06cc4-151">Nombre de toohello plus que vous donne Twilio, vous pouvez également vérifier les nombres que vous contrôlez (autrement dit, votre téléphone portable ou accueil numéro de téléphone) pour une utilisation dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="06cc4-151">In addition toohello number you are given by Twilio, you can also verify numbers that you control (i.e. your cell phone or home phone number) for use in your applications.</span></span> 

<span data-ttu-id="06cc4-152">Pour plus d’informations sur la façon de tooverify un numéro de téléphone, consultez [gérer les nombres][verify_phone].</span><span class="sxs-lookup"><span data-stu-id="06cc4-152">For information on how tooverify a phone number, see [Manage Numbers][verify_phone].</span></span>

## <span data-ttu-id="06cc4-153"><a id="create_app"></a>Créer une application Ruby</span><span class="sxs-lookup"><span data-stu-id="06cc4-153"><a id="create_app"></a>Create a Ruby Application</span></span>
<span data-ttu-id="06cc4-154">Une application Ruby qui utilise le service de Twilio hello et s’exécute dans Azure n’est pas différente de toute autre application Ruby qui utilise le service de Twilio hello.</span><span class="sxs-lookup"><span data-stu-id="06cc4-154">A Ruby application that uses hello Twilio service and is running in Azure is no different than any other Ruby application that uses hello Twilio service.</span></span> <span data-ttu-id="06cc4-155">Tandis que Twilio services sont RESTful qui peuvent être appelés depuis Ruby de plusieurs façons, cet article se concentrera sur le fonctionnement des services avec toouse Twilio [bibliothèque d’assistance de Twilio pour Ruby][twilio_ruby].</span><span class="sxs-lookup"><span data-stu-id="06cc4-155">While Twilio services are RESTful and can be called from Ruby in several ways, this article will focus on how toouse Twilio services with [Twilio helper library for Ruby][twilio_ruby].</span></span>

<span data-ttu-id="06cc4-156">Tout d’abord, [configurer un nouvel ordinateur virtuel Azure Linux] [ azure_vm_setup] tooact en tant qu’hôte pour votre nouvelle application web Ruby.</span><span class="sxs-lookup"><span data-stu-id="06cc4-156">First, [set-up a new Azure Linux VM][azure_vm_setup] tooact as a host for your new Ruby web application.</span></span> <span data-ttu-id="06cc4-157">Ignorez les étapes hello impliquant la création d’une application de quadrillage, simplement hello de configuration VM hello.</span><span class="sxs-lookup"><span data-stu-id="06cc4-157">Ignore hello steps involving hello creation of a Rails app, just set-up hello VM.</span></span> <span data-ttu-id="06cc4-158">Veillez à créer un point de terminaison avec un port externe défini sur 80 et un port interne défini sur 5000.</span><span class="sxs-lookup"><span data-stu-id="06cc4-158">Make sure you create an Endpoint with an external port of 80 and an internal port of 5000.</span></span>

<span data-ttu-id="06cc4-159">Dans les exemples de hello ci-dessous, nous allons utiliser [Sinatra][sinatra], une infrastructure web très simple pour Ruby.</span><span class="sxs-lookup"><span data-stu-id="06cc4-159">In hello examples below, we will be using [Sinatra][sinatra], a very simple web framework for Ruby.</span></span> <span data-ttu-id="06cc4-160">Mais vous pouvez certainement utiliser bibliothèque d’assistance de Twilio hello pour Ruby avec n’importe quel autre infrastructure web, y compris Ruby on Rails.</span><span class="sxs-lookup"><span data-stu-id="06cc4-160">But you can certainly use hello Twilio helper library for Ruby with any other web framework, including Ruby on Rails.</span></span>

<span data-ttu-id="06cc4-161">Utilisez SSH dans votre nouvelle machine virtuelle et créez un répertoire pour votre nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="06cc4-161">SSH into your new VM and create a directory for your new app.</span></span> <span data-ttu-id="06cc4-162">À l’intérieur de ce répertoire, créez un fichier appelé Gemfile et copie hello après le code dans celui-ci :</span><span class="sxs-lookup"><span data-stu-id="06cc4-162">Inside that directory, create a file called Gemfile and copy hello following code into it:</span></span>

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

<span data-ttu-id="06cc4-163">Sur la ligne de commande hello exécuter `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="06cc4-163">On hello command line run `bundle install`.</span></span> <span data-ttu-id="06cc4-164">Dépendances de hello ci-dessus seront installés.</span><span class="sxs-lookup"><span data-stu-id="06cc4-164">This will install hello dependencies above.</span></span> <span data-ttu-id="06cc4-165">Ensuite, créez un fichier appelé `web.rb`.</span><span class="sxs-lookup"><span data-stu-id="06cc4-165">Next create a file called `web.rb`.</span></span> <span data-ttu-id="06cc4-166">Il s’agit de résidence de code hello pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="06cc4-166">This will be where hello code for your web app lives.</span></span> <span data-ttu-id="06cc4-167">Collez hello après le code dans celui-ci :</span><span class="sxs-lookup"><span data-stu-id="06cc4-167">Paste hello following code into it:</span></span>

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

<span data-ttu-id="06cc4-168">À ce stade, vous devez être commande hello de hello en mesure de s’exécuter `ruby web.rb -p 5000`.</span><span class="sxs-lookup"><span data-stu-id="06cc4-168">At this point you should be able hello run hello command `ruby web.rb -p 5000`.</span></span> <span data-ttu-id="06cc4-169">Ceci met en place un petit serveur web sur le port 5000.</span><span class="sxs-lookup"><span data-stu-id="06cc4-169">This will spin-up a small web server on port 5000.</span></span> <span data-ttu-id="06cc4-170">Vous devez être en mesure de toobrowse toothis application dans votre navigateur en visitant l’URL de hello vous configuration pour votre machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="06cc4-170">You should be able toobrowse toothis app in your browser by visiting hello URL you set-up for your Azure VM.</span></span> <span data-ttu-id="06cc4-171">Une fois que vous pouvez atteindre votre application web dans le navigateur de hello, vous êtes prêt toostart création d’une application Twilio.</span><span class="sxs-lookup"><span data-stu-id="06cc4-171">Once you can reach your web app in hello browser, you're ready toostart building a Twilio app.</span></span>

## <span data-ttu-id="06cc4-172"><a id="configure_app"></a>Configurer votre Application tooUse Twilio</span><span class="sxs-lookup"><span data-stu-id="06cc4-172"><a id="configure_app"></a>Configure Your Application tooUse Twilio</span></span>
<span data-ttu-id="06cc4-173">Vous pouvez configurer votre bibliothèque de Twilio web application toouse hello en mettant à jour votre `Gemfile` tooinclude cette ligne :</span><span class="sxs-lookup"><span data-stu-id="06cc4-173">You can configure your web app toouse hello Twilio library by updating your `Gemfile` tooinclude this line:</span></span>

    gem 'twilio-ruby'

<span data-ttu-id="06cc4-174">Sur la ligne de commande hello, exécutez `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="06cc4-174">On hello command line, run `bundle install`.</span></span> <span data-ttu-id="06cc4-175">Ouvrez maintenant `web.rb` et incluant cette ligne en haut de hello :</span><span class="sxs-lookup"><span data-stu-id="06cc4-175">Now open `web.rb` and including this line at hello top:</span></span>

    require 'twilio-ruby'

<span data-ttu-id="06cc4-176">Vous êtes maintenant toutes définies bibliothèque d’assistance de toouse hello Twilio pour Ruby dans votre application web.</span><span class="sxs-lookup"><span data-stu-id="06cc4-176">You're now all set toouse hello Twilio helper library for Ruby in your web app.</span></span>

## <span data-ttu-id="06cc4-177"><a id="howto_make_call"></a>Procédure : passer un appel sortant</span><span class="sxs-lookup"><span data-stu-id="06cc4-177"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="06cc4-178">Hello suivant montre comment appeler le toomake sortante.</span><span class="sxs-lookup"><span data-stu-id="06cc4-178">hello following shows how toomake an outgoing call.</span></span> <span data-ttu-id="06cc4-179">Concepts clés incluent à l’aide de la bibliothèque d’assistance de Twilio hello pour Ruby toomake qu'appelle des API REST et TwiML de rendu.</span><span class="sxs-lookup"><span data-stu-id="06cc4-179">Key concepts include using hello Twilio helper library for Ruby toomake REST API calls and rendering TwiML.</span></span> <span data-ttu-id="06cc4-180">Remplacez par vos valeurs hello **de** et **à** les numéros de téléphone et assurez-vous que vous vérifiez hello **à partir de** numéro de téléphone de votre code hello de Twilio compte toorunning préalable.</span><span class="sxs-lookup"><span data-stu-id="06cc4-180">Substitute your values for hello **From** and **To** phone numbers, and ensure that you verify hello **From** phone number for your Twilio account prior toorunning hello code.</span></span>

<span data-ttu-id="06cc4-181">Ajouter cette fonction trop`web.md`:</span><span class="sxs-lookup"><span data-stu-id="06cc4-181">Add this function too`web.md`:</span></span>

    # Set your account ID and authentication token.
    sid = "your_twilio_account_sid";
    token = "your_twilio_authentication_token";

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from = "NNNNNNNNNNN";

    # hello number of hello phone receiving call.
    too= "NNNNNNNNNNN";

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://yourdomain.cloudapp.net/voice_url";

    get '/make_call' do
      # Create hello call client.
      client = Twilio::REST::Client.new(sid, token);

      # Make hello call
      client.account.calls.create(to: to, from: from, url: url)
    end

    post '/voice_url' do
      "<Response>
         <Say>Hello Monkey!</Say>
       </Response>"
    end

<span data-ttu-id="06cc4-182">Si l’ouverture des `http://yourdomain.cloudapp.net/make_call` dans un navigateur, qui déclenchera un appel téléphonique de hello appel toohello Twilio API toomake hello.</span><span class="sxs-lookup"><span data-stu-id="06cc4-182">If you open-up `http://yourdomain.cloudapp.net/make_call` in a browser, that will trigger hello call toohello Twilio API toomake hello phone call.</span></span> <span data-ttu-id="06cc4-183">Hello des deux premiers paramètres dans `client.account.calls.create` sont suffisamment explicites : hello numéro hello appel est `from` et appel de hello numéro hello est `to`.</span><span class="sxs-lookup"><span data-stu-id="06cc4-183">hello first two parameters in `client.account.calls.create` are fairly self-explanatory: hello number hello call is `from` and hello number hello call is `to`.</span></span> 

<span data-ttu-id="06cc4-184">Hello troisième paramètre (`url`) est l’URL de hello que Twilio demande tooget des instructions sur le toodo une fois que l’appel hello est connecté.</span><span class="sxs-lookup"><span data-stu-id="06cc4-184">hello third parameter (`url`) is hello URL that Twilio requests tooget instructions on what toodo once hello call is connected.</span></span> <span data-ttu-id="06cc4-185">Dans ce cas nous configurer une URL (`http://yourdomain.cloudapp.net`) qui retourne un document TwiML simple et utilise hello `<Say>` toodo verbe certains synthèse vocale, puis prononcez « Hello le » toohello destinataire hello appeler.</span><span class="sxs-lookup"><span data-stu-id="06cc4-185">In this case we set-up a URL (`http://yourdomain.cloudapp.net`) that returns a simple TwiML document and uses hello `<Say>` verb toodo some text-to-speech and say "Hello Monkey" toohello person recieving hello call.</span></span>

## <span data-ttu-id="06cc4-186"><a id="howto_recieve_sms"></a>Réception d’un SMS</span><span class="sxs-lookup"><span data-stu-id="06cc4-186"><a id="howto_recieve_sms"></a>How to: Recieve an SMS message</span></span>
<span data-ttu-id="06cc4-187">Dans l’exemple précédent de hello, nous avons lancé une **sortants** appel téléphonique.</span><span class="sxs-lookup"><span data-stu-id="06cc4-187">In hello previous example we initiated an **outgoing** phone call.</span></span> <span data-ttu-id="06cc4-188">Cette fois, nous allons utiliser le numéro de téléphone hello Twilio nous a donné au cours de l’inscription tooprocess un **entrant** message SMS.</span><span class="sxs-lookup"><span data-stu-id="06cc4-188">This time, let's use hello phone number that Twilio gave us during sign-up tooprocess an **incoming** SMS message.</span></span>

<span data-ttu-id="06cc4-189">Tout d’abord, ouverture de session de tooyour [tableau de bord Twilio][twilio_account].</span><span class="sxs-lookup"><span data-stu-id="06cc4-189">First, log-in tooyour [Twilio dashboard][twilio_account].</span></span> <span data-ttu-id="06cc4-190">Cliquez sur « Numéros » de navigation supérieure de hello, puis cliquez sur hello le nombre de Twilio que vous ont été fournis.</span><span class="sxs-lookup"><span data-stu-id="06cc4-190">Click on "Numbers" in hello top nav and then click on hello Twilio number you were provided.</span></span> <span data-ttu-id="06cc4-191">Deux URL sont disponibles pour configuration :</span><span class="sxs-lookup"><span data-stu-id="06cc4-191">You'll see two URLs that you can configure.</span></span> <span data-ttu-id="06cc4-192">une URL de requête vocale et une URL de requête SMS.</span><span class="sxs-lookup"><span data-stu-id="06cc4-192">A Voice Request URL and an SMS Request URL.</span></span> <span data-ttu-id="06cc4-193">Il s’agit des URL de hello Twilio appelle chaque fois qu’un appel téléphonique est effectuée ou un SMS envoyé tooyour nombre.</span><span class="sxs-lookup"><span data-stu-id="06cc4-193">These are hello URLs that Twilio calls whenever a phone call is made or an SMS is sent tooyour number.</span></span> <span data-ttu-id="06cc4-194">URL de Hello sont également définis en tant que « web hooks ».</span><span class="sxs-lookup"><span data-stu-id="06cc4-194">hello URLs are also known as "web hooks".</span></span>

<span data-ttu-id="06cc4-195">Nous aimerions tooprocess les messages SMS entrants, par conséquent, nous allons mettre à jour des URL de hello trop`http://yourdomain.cloudapp.net/sms_url`.</span><span class="sxs-lookup"><span data-stu-id="06cc4-195">We would like tooprocess incoming SMS messages, so let's update hello URL too`http://yourdomain.cloudapp.net/sms_url`.</span></span> <span data-ttu-id="06cc4-196">Pour commencer, cliquez sur Enregistrer les changements au bas de hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="06cc4-196">Go ahead and click Save Changes at hello bottom of hello page.</span></span> <span data-ttu-id="06cc4-197">Maintenant, de retour dans `web.rb` programme nous allons notre toohandle application cela :</span><span class="sxs-lookup"><span data-stu-id="06cc4-197">Now, back in `web.rb` let's program our application toohandle this:</span></span>

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for hello ping! Twilio and Azure rock!</Message>
       </Response>"
    end

<span data-ttu-id="06cc4-198">Après avoir apporté la modification de hello, assurez-vous que toore-démarrer votre application web.</span><span class="sxs-lookup"><span data-stu-id="06cc4-198">After making hello change, make sure toore-start your web app.</span></span> <span data-ttu-id="06cc4-199">Ensuite, retirez votre téléphone et envoyer un SMS de tooyour Twilio nombre.</span><span class="sxs-lookup"><span data-stu-id="06cc4-199">Now, take out your phone and send an SMS tooyour Twilio number.</span></span> <span data-ttu-id="06cc4-200">Vous devez obtenir rapidement une réponse SMS indiquant que « Hey, Merci de ping de hello !</span><span class="sxs-lookup"><span data-stu-id="06cc4-200">You should promptly get an SMS response that says "Hey, thanks for hello ping!</span></span> <span data-ttu-id="06cc4-201">Twilio et Azure sont les meilleurs ! »</span><span class="sxs-lookup"><span data-stu-id="06cc4-201">Twilio and Azure rock!".</span></span>

## <span data-ttu-id="06cc4-202"><a id="additional_services"></a>Utilisation de services Twilio supplémentaires</span><span class="sxs-lookup"><span data-stu-id="06cc4-202"><a id="additional_services"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="06cc4-203">En outre toohello les exemples indiqués ici, que twilio propose des API basées sur le web qui vous pouvez utiliser des fonctionnalités Twilio tooleverage supplémentaires à partir de votre application Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="06cc4-203">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="06cc4-204">Pour plus d’informations, consultez hello [documentation de l’API de Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="06cc4-204">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

### <span data-ttu-id="06cc4-205"><a id="NextSteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="06cc4-205"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="06cc4-206">Maintenant que vous avez appris les notions de base de hello Hello Twilio service, suivez ces liens de toolearn plus :</span><span class="sxs-lookup"><span data-stu-id="06cc4-206">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="06cc4-207">[Conseils de sécurité Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="06cc4-207">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="06cc4-208">[Procédures et exemples de code Twilio][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="06cc4-208">[Twilio HowTos and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="06cc4-209">[Didacticiels de démarrage rapide Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="06cc4-209">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="06cc4-210">[Twilio sur GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="06cc4-210">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="06cc4-211">[Communiquer avec tooTwilio prise en charge][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="06cc4-211">[Talk tooTwilio Support][twilio_support]</span></span>

[twilio_ruby]: https://www.twilio.com/docs/ruby/install





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
[sinatra]: http://www.sinatrarb.com/
[azure_vm_setup]: http://www.windowsazure.com/develop/ruby/tutorials/web-app-with-linux-vm/
