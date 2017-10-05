---
title: "Utilisation de Twilio pour les fonctionnalités vocales et de SMS (Ruby) | Microsoft Docs"
description: "Découvrez comment passer un appel téléphonique et envoyer un message texte avec le service d'API Twilio sur Azure. Exemples de code écrits en Ruby."
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
ms.openlocfilehash: 69e50e7fe0e1f302e96c309878b8dea6869dff4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-ruby"></a><span data-ttu-id="38ccf-104">Utilisation de Twilio pour les fonctionnalités vocales et de SMS dans Ruby</span><span class="sxs-lookup"><span data-stu-id="38ccf-104">How to Use Twilio for Voice and SMS Capabilities in Ruby</span></span>
<span data-ttu-id="38ccf-105">Ce guide présente l'exécution de tâches de programmation courantes avec le service API Twilio sur Azure.</span><span class="sxs-lookup"><span data-stu-id="38ccf-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="38ccf-106">Les scénarios abordés comprennent notamment les appels téléphoniques et l'envoi de SMS.</span><span class="sxs-lookup"><span data-stu-id="38ccf-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="38ccf-107">Pour plus d'informations sur Twilio et sur l'utilisation des fonctionnalités vocales et de SMS de vos applications, consultez la section [Étapes suivantes](#NextSteps) .</span><span class="sxs-lookup"><span data-stu-id="38ccf-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="38ccf-108"><a id="WhatIs"></a>Présentation de Twilio</span><span class="sxs-lookup"><span data-stu-id="38ccf-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="38ccf-109">Twilio est une API de service Web de téléphonie vous permettant d'utiliser vos aptitudes et langages Web existants pour générer des applications vocales et de SMS.</span><span class="sxs-lookup"><span data-stu-id="38ccf-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills to build voice and SMS applications.</span></span> <span data-ttu-id="38ccf-110">Twilio est un service tiers, et non une fonctionnalité Azure ni un produit Microsoft.</span><span class="sxs-lookup"><span data-stu-id="38ccf-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="38ccf-111">**Twilio Voice** permet à vos applications de passer et de recevoir des appels téléphoniques.</span><span class="sxs-lookup"><span data-stu-id="38ccf-111">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="38ccf-112">**Twilio SMS** permet à vos applications de créer et de recevoir des SMS.</span><span class="sxs-lookup"><span data-stu-id="38ccf-112">**Twilio SMS** allows your applications to make and receive SMS messages.</span></span> <span data-ttu-id="38ccf-113">**Twilio Client** permet à vos applications d'activer les communications vocales au moyen de connexions Internet existantes, y compris des connexions mobiles.</span><span class="sxs-lookup"><span data-stu-id="38ccf-113">**Twilio Client** allows your applications to enable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="38ccf-114"><a id="Pricing"></a>Tarification de Twilio et offres spéciales</span><span class="sxs-lookup"><span data-stu-id="38ccf-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="38ccf-115">Des informations sur les prix de Twilio sont disponibles dans la page [Tarification de Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="38ccf-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="38ccf-116">Les clients Azure reçoivent une [offre spéciale][special_offer] : un crédit gratuit de 1 000 SMS ou de 1 000 minutes d’appel en entrée.</span><span class="sxs-lookup"><span data-stu-id="38ccf-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="38ccf-117">Pour bénéficier de cette offre ou pour obtenir des informations supplémentaires, visitez la page [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="38ccf-117">To sign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>  

## <span data-ttu-id="38ccf-118"><a id="Concepts"></a>Concepts</span><span class="sxs-lookup"><span data-stu-id="38ccf-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="38ccf-119">L'API Twilio est une API RESTful qui offre des fonctionnalités vocales et de SMS aux applications.</span><span class="sxs-lookup"><span data-stu-id="38ccf-119">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="38ccf-120">Les bibliothèques clientes sont disponibles dans plusieurs langues : pour en obtenir la liste, consultez la page [Bibliothèques de l’API Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="38ccf-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

### <span data-ttu-id="38ccf-121"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="38ccf-121"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="38ccf-122">TwiML est un jeu d'instructions XML qui informent Twilio sur la façon de traiter un appel ou un SMS.</span><span class="sxs-lookup"><span data-stu-id="38ccf-122">TwiML is a set of XML-based instructions that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="38ccf-123">À titre d'exemple, le code TwiML suivant convertit le texte **Hello World** en parole.</span><span class="sxs-lookup"><span data-stu-id="38ccf-123">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="38ccf-124">Tous les documents TwiML ont un élément racine `<Response>` .</span><span class="sxs-lookup"><span data-stu-id="38ccf-124">All TwiML documents have `<Response>` as their root element.</span></span> <span data-ttu-id="38ccf-125">Vous pouvez donc utiliser des verbes Twilio pour définir le comportement de votre application.</span><span class="sxs-lookup"><span data-stu-id="38ccf-125">From there, you use Twilio Verbs to define the behavior of your application.</span></span>

### <span data-ttu-id="38ccf-126"><a id="Verbs"></a>Verbes TwiML</span><span class="sxs-lookup"><span data-stu-id="38ccf-126"><a id="Verbs"></a>TwiML Verbs</span></span>
<span data-ttu-id="38ccf-127">Les verbes Twilio sont des balises XML qui indiquent à Twilio les **actions**à effectuer.</span><span class="sxs-lookup"><span data-stu-id="38ccf-127">Twilio Verbs are XML tags that tell Twilio what to **do**.</span></span> <span data-ttu-id="38ccf-128">Par exemple, le verbe **&lt;Say&gt;** indique à Twilio de délivrer un message audible lors d'un appel.</span><span class="sxs-lookup"><span data-stu-id="38ccf-128">For example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span> 

<span data-ttu-id="38ccf-129">La liste suivante présente les verbes Twilio.</span><span class="sxs-lookup"><span data-stu-id="38ccf-129">The following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="38ccf-130">**&lt;Dial&gt;** : connecte l'appelant à un autre téléphone.</span><span class="sxs-lookup"><span data-stu-id="38ccf-130">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="38ccf-131">**&lt;Gather&gt;** : rassemble les chiffres numériques entrés sur le clavier du téléphone.</span><span class="sxs-lookup"><span data-stu-id="38ccf-131">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="38ccf-132">**&lt;Hangup&gt;** : met fin à un appel.</span><span class="sxs-lookup"><span data-stu-id="38ccf-132">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="38ccf-133">**&lt;Play&gt;** : lit un fichier audio.</span><span class="sxs-lookup"><span data-stu-id="38ccf-133">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="38ccf-134">**&lt;Pause&gt;** : patiente silencieusement pendant un nombre déterminé de secondes.</span><span class="sxs-lookup"><span data-stu-id="38ccf-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="38ccf-135">**&lt;Record&gt;** : enregistre la voix de l'appelant et renvoie une URL permettant d'accéder à un fichier contenant l'enregistrement.</span><span class="sxs-lookup"><span data-stu-id="38ccf-135">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="38ccf-136">**&lt;Redirect&gt;** : transfère le contrôle d'un appel ou d'un SMS au TwiML à une autre URL.</span><span class="sxs-lookup"><span data-stu-id="38ccf-136">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="38ccf-137">**&lt;Reject&gt;** : refuse un appel entrant sur votre numéro Twilio sans vous facturer</span><span class="sxs-lookup"><span data-stu-id="38ccf-137">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="38ccf-138">**&lt;Say&gt;** : convertit le texte d'un appel en parole.</span><span class="sxs-lookup"><span data-stu-id="38ccf-138">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="38ccf-139">**&lt;Sms&gt;** : envoie un SMS.</span><span class="sxs-lookup"><span data-stu-id="38ccf-139">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

<span data-ttu-id="38ccf-140">Pour plus d’informations sur les verbes Twilio, leurs attributs et le langage TwiML, consultez la page [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="38ccf-140">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="38ccf-141">Pour plus d’informations sur l’API Twilio, consultez la page [API Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="38ccf-141">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="38ccf-142"><a id="CreateAccount"></a>Créer un compte Twilio</span><span class="sxs-lookup"><span data-stu-id="38ccf-142"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="38ccf-143">Lorsque vous êtes prêt à créer votre compte Twilio, inscrivez-vous sur la page [Essayer Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="38ccf-143">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="38ccf-144">Vous pouvez commencer avec un compte gratuit, avant de le mettre à niveau ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="38ccf-144">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="38ccf-145">Lors de la création d'un compte Twilio, vous obtenez un numéro de téléphone gratuit pour votre application.</span><span class="sxs-lookup"><span data-stu-id="38ccf-145">When you sign up for a Twilio account, you'll get a free phone number for your application.</span></span> <span data-ttu-id="38ccf-146">Vous recevez également un SID de compte et un jeton d'authentification.</span><span class="sxs-lookup"><span data-stu-id="38ccf-146">You'll also receive an account SID and an auth token.</span></span> <span data-ttu-id="38ccf-147">Les deux sont nécessaires pour passer des appels d'API Twilio.</span><span class="sxs-lookup"><span data-stu-id="38ccf-147">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="38ccf-148">Pour éviter qu'une personne non autorisée n'accède à votre compte, conservez votre jeton d'authentification en lieu sûr.</span><span class="sxs-lookup"><span data-stu-id="38ccf-148">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="38ccf-149">Vous pouvez consulter vos ID de compte et jeton d’authentification sur la [page du compte Twilio][twilio_account], dans les champs intitulés **ACCOUNT SID** et **AUTH TOKEN**, respectivement.</span><span class="sxs-lookup"><span data-stu-id="38ccf-149">Your account SID and auth token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

### <span data-ttu-id="38ccf-150"><a id="VerifyPhoneNumbers"></a>Vérifier les numéros de téléphone</span><span class="sxs-lookup"><span data-stu-id="38ccf-150"><a id="VerifyPhoneNumbers"></a>Verify Phone Numbers</span></span>
<span data-ttu-id="38ccf-151">Outre le numéro donné par Twilio, vous pouvez également vérifier les numéros que vous contrôlez (votre numéro de portable ou de téléphone fixe) pour les utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="38ccf-151">In addition to the number you are given by Twilio, you can also verify numbers that you control (i.e. your cell phone or home phone number) for use in your applications.</span></span> 

<span data-ttu-id="38ccf-152">Pour en savoir plus sur la vérification d'un numéro de téléphone, consultez la page [Gestion des numéros][verify_phone].</span><span class="sxs-lookup"><span data-stu-id="38ccf-152">For information on how to verify a phone number, see [Manage Numbers][verify_phone].</span></span>

## <span data-ttu-id="38ccf-153"><a id="create_app"></a>Créer une application Ruby</span><span class="sxs-lookup"><span data-stu-id="38ccf-153"><a id="create_app"></a>Create a Ruby Application</span></span>
<span data-ttu-id="38ccf-154">Une application Ruby qui utilise le service Twilio et qui s'exécute dans Azure est identique aux autres applications Ruby qui utilisent le service Twilio.</span><span class="sxs-lookup"><span data-stu-id="38ccf-154">A Ruby application that uses the Twilio service and is running in Azure is no different than any other Ruby application that uses the Twilio service.</span></span> <span data-ttu-id="38ccf-155">Bien que les services Twilio soient basés sur RESTful et puissent être appelés de différentes manières depuis Ruby, cet article met l’accent sur l’utilisation des services Twilio avec la [bibliothèque d’aide Twilio pour Ruby][twilio_ruby].</span><span class="sxs-lookup"><span data-stu-id="38ccf-155">While Twilio services are RESTful and can be called from Ruby in several ways, this article will focus on how to use Twilio services with [Twilio helper library for Ruby][twilio_ruby].</span></span>

<span data-ttu-id="38ccf-156">Tout d’abord, [configurez une nouvelle machine virtuelle Linux Azure][azure_vm_setup] afin qu’elle joue le rôle d’hôte pour votre nouvelle application web Ruby.</span><span class="sxs-lookup"><span data-stu-id="38ccf-156">First, [set-up a new Azure Linux VM][azure_vm_setup] to act as a host for your new Ruby web application.</span></span> <span data-ttu-id="38ccf-157">Ignorez les étapes concernant la création de l'application Rails. Il vous suffit de configurer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="38ccf-157">Ignore the steps involving the creation of a Rails app, just set-up the VM.</span></span> <span data-ttu-id="38ccf-158">Veillez à créer un point de terminaison avec un port externe défini sur 80 et un port interne défini sur 5000.</span><span class="sxs-lookup"><span data-stu-id="38ccf-158">Make sure you create an Endpoint with an external port of 80 and an internal port of 5000.</span></span>

<span data-ttu-id="38ccf-159">Dans les exemples ci-dessous, nous utilisons [Sinatra][sinatra], une infrastructure web très simple pour Ruby.</span><span class="sxs-lookup"><span data-stu-id="38ccf-159">In the examples below, we will be using [Sinatra][sinatra], a very simple web framework for Ruby.</span></span> <span data-ttu-id="38ccf-160">Vous pouvez certainement utiliser la bibliothèque d'aide Twilio pour Ruby avec une autre infrastructure Web, dont Ruby on Rails.</span><span class="sxs-lookup"><span data-stu-id="38ccf-160">But you can certainly use the Twilio helper library for Ruby with any other web framework, including Ruby on Rails.</span></span>

<span data-ttu-id="38ccf-161">Utilisez SSH dans votre nouvelle machine virtuelle et créez un répertoire pour votre nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="38ccf-161">SSH into your new VM and create a directory for your new app.</span></span> <span data-ttu-id="38ccf-162">Dans ce répertoire, créez un fichier nommé Gemfile et copiez-y le code suivant :</span><span class="sxs-lookup"><span data-stu-id="38ccf-162">Inside that directory, create a file called Gemfile and copy the following code into it:</span></span>

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

<span data-ttu-id="38ccf-163">Sur la ligne de commande, exécutez `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="38ccf-163">On the command line run `bundle install`.</span></span> <span data-ttu-id="38ccf-164">Ceci permet d'installer les dépendances ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="38ccf-164">This will install the dependencies above.</span></span> <span data-ttu-id="38ccf-165">Ensuite, créez un fichier appelé `web.rb`.</span><span class="sxs-lookup"><span data-stu-id="38ccf-165">Next create a file called `web.rb`.</span></span> <span data-ttu-id="38ccf-166">C'est là que va résider le code de votre application Web.</span><span class="sxs-lookup"><span data-stu-id="38ccf-166">This will be where the code for your web app lives.</span></span> <span data-ttu-id="38ccf-167">Collez-y le code suivant :</span><span class="sxs-lookup"><span data-stu-id="38ccf-167">Paste the following code into it:</span></span>

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

<span data-ttu-id="38ccf-168">À ce stade, vous devez pouvoir exécuter la commande `ruby web.rb -p 5000`.</span><span class="sxs-lookup"><span data-stu-id="38ccf-168">At this point you should be able the run the command `ruby web.rb -p 5000`.</span></span> <span data-ttu-id="38ccf-169">Ceci met en place un petit serveur web sur le port 5000.</span><span class="sxs-lookup"><span data-stu-id="38ccf-169">This will spin-up a small web server on port 5000.</span></span> <span data-ttu-id="38ccf-170">Vous devez pouvoir accéder à cette application dans votre navigateur en vous rendant à l'URL définie pour la création de votre machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="38ccf-170">You should be able to browse to this app in your browser by visiting the URL you set-up for your Azure VM.</span></span> <span data-ttu-id="38ccf-171">Lorsque vous accédez à votre application Web dans le navigateur, vous êtes prêt à créer une application Twilio.</span><span class="sxs-lookup"><span data-stu-id="38ccf-171">Once you can reach your web app in the browser, you're ready to start building a Twilio app.</span></span>

## <span data-ttu-id="38ccf-172"><a id="configure_app"></a>Configurer l’application pour utiliser Twilio</span><span class="sxs-lookup"><span data-stu-id="38ccf-172"><a id="configure_app"></a>Configure Your Application to Use Twilio</span></span>
<span data-ttu-id="38ccf-173">Vous pouvez configurer votre application web afin qu’elle utilise la bibliothèque Twilio en mettant à jour votre fichier `Gemfile` pour y inclure la ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="38ccf-173">You can configure your web app to use the Twilio library by updating your `Gemfile` to include this line:</span></span>

    gem 'twilio-ruby'

<span data-ttu-id="38ccf-174">Sur la ligne de commande, exécutez `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="38ccf-174">On the command line, run `bundle install`.</span></span> <span data-ttu-id="38ccf-175">Ensuite, ouvrez `web.rb` et ajoutez cette ligne au début du code :</span><span class="sxs-lookup"><span data-stu-id="38ccf-175">Now open `web.rb` and including this line at the top:</span></span>

    require 'twilio-ruby'

<span data-ttu-id="38ccf-176">Vous pouvez maintenant utiliser la bibliothèque d'aide Twilio dans votre application web.</span><span class="sxs-lookup"><span data-stu-id="38ccf-176">You're now all set to use the Twilio helper library for Ruby in your web app.</span></span>

## <span data-ttu-id="38ccf-177"><a id="howto_make_call"></a>Procédure : passer un appel sortant</span><span class="sxs-lookup"><span data-stu-id="38ccf-177"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="38ccf-178">Le code suivant permet d'exécuter un appel sortant.</span><span class="sxs-lookup"><span data-stu-id="38ccf-178">The following shows how to make an outgoing call.</span></span> <span data-ttu-id="38ccf-179">Les concepts principaux incluent l'utilisation de la bibliothèque d'aide Twilio pour Ruby afin de passer des appels d'API REST et d'assurer le rendu TwiML.</span><span class="sxs-lookup"><span data-stu-id="38ccf-179">Key concepts include using the Twilio helper library for Ruby to make REST API calls and rendering TwiML.</span></span> <span data-ttu-id="38ccf-180">Remplacez vos valeurs pour les numéros de téléphone **From** (De) et **To** (À), puis assurez-vous de vérifier le numéro de téléphone **From** de votre compte Twilio avant d'exécuter le code.</span><span class="sxs-lookup"><span data-stu-id="38ccf-180">Substitute your values for the **From** and **To** phone numbers, and ensure that you verify the **From** phone number for your Twilio account prior to running the code.</span></span>

<span data-ttu-id="38ccf-181">Ajoutez cette fonction à `web.md`:</span><span class="sxs-lookup"><span data-stu-id="38ccf-181">Add this function to `web.md`:</span></span>

    # Set your account ID and authentication token.
    sid = "your_twilio_account_sid";
    token = "your_twilio_authentication_token";

    # The number of the phone initiating the the call.
    # This should either be a Twilio number or a number that you've verified
    from = "NNNNNNNNNNN";

    # The number of the phone receiving call.
    to = "NNNNNNNNNNN";

    # Use the Twilio-provided site for the TwiML response.
    url = "http://yourdomain.cloudapp.net/voice_url";

    get '/make_call' do
      # Create the call client.
      client = Twilio::REST::Client.new(sid, token);

      # Make the call
      client.account.calls.create(to: to, from: from, url: url)
    end

    post '/voice_url' do
      "<Response>
         <Say>Hello Monkey!</Say>
       </Response>"
    end

<span data-ttu-id="38ccf-182">Si vous ouvrez l’adresse `http://yourdomain.cloudapp.net/make_call` dans un navigateur, cela déclenche l’appel de l’API Twilio qui passe alors l’appel téléphonique.</span><span class="sxs-lookup"><span data-stu-id="38ccf-182">If you open-up `http://yourdomain.cloudapp.net/make_call` in a browser, that will trigger the call to the Twilio API to make the phone call.</span></span> <span data-ttu-id="38ccf-183">Les deux premiers paramètres dans `client.account.calls.create` sont relativement explicites : le numéro d’où provient l’appel (`from`) et le numéro appelé (`to`).</span><span class="sxs-lookup"><span data-stu-id="38ccf-183">The first two parameters in `client.account.calls.create` are fairly self-explanatory: the number the call is `from` and the number the call is `to`.</span></span> 

<span data-ttu-id="38ccf-184">Le troisième paramètre (`url`) est l’URL demandée par Twilio pour obtenir les instructions à suivre une fois l’appel connecté.</span><span class="sxs-lookup"><span data-stu-id="38ccf-184">The third parameter (`url`) is the URL that Twilio requests to get instructions on what to do once the call is connected.</span></span> <span data-ttu-id="38ccf-185">Dans notre exemple, nous avons défini une URL (`http://yourdomain.cloudapp.net`) qui renvoie un document TwiML simple utilisant le verbe `<Say>` pour convertir du texte en parole et dire « Hello Monkey » à la personne qui reçoit l’appel.</span><span class="sxs-lookup"><span data-stu-id="38ccf-185">In this case we set-up a URL (`http://yourdomain.cloudapp.net`) that returns a simple TwiML document and uses the `<Say>` verb to do some text-to-speech and say "Hello Monkey" to the person recieving the call.</span></span>

## <span data-ttu-id="38ccf-186"><a id="howto_recieve_sms"></a>Réception d’un SMS</span><span class="sxs-lookup"><span data-stu-id="38ccf-186"><a id="howto_recieve_sms"></a>How to: Recieve an SMS message</span></span>
<span data-ttu-id="38ccf-187">Dans l'exemple précédent, nous avons émis un appel **sortant** .</span><span class="sxs-lookup"><span data-stu-id="38ccf-187">In the previous example we initiated an **outgoing** phone call.</span></span> <span data-ttu-id="38ccf-188">Cette fois, nous allons utiliser le numéro de téléphone fourni par Twilio lors de l'inscription pour traiter un SMS **entrant** .</span><span class="sxs-lookup"><span data-stu-id="38ccf-188">This time, let's use the phone number that Twilio gave us during sign-up to process an **incoming** SMS message.</span></span>

<span data-ttu-id="38ccf-189">Commencez par vous connecter à votre [tableau de bord Twilio][twilio_account].</span><span class="sxs-lookup"><span data-stu-id="38ccf-189">First, log-in to your [Twilio dashboard][twilio_account].</span></span> <span data-ttu-id="38ccf-190">Cliquez sur « Numbers » dans la zone de navigation supérieure, puis sur le numéro fourni par Twilio.</span><span class="sxs-lookup"><span data-stu-id="38ccf-190">Click on "Numbers" in the top nav and then click on the Twilio number you were provided.</span></span> <span data-ttu-id="38ccf-191">Deux URL sont disponibles pour configuration :</span><span class="sxs-lookup"><span data-stu-id="38ccf-191">You'll see two URLs that you can configure.</span></span> <span data-ttu-id="38ccf-192">une URL de requête vocale et une URL de requête SMS.</span><span class="sxs-lookup"><span data-stu-id="38ccf-192">A Voice Request URL and an SMS Request URL.</span></span> <span data-ttu-id="38ccf-193">Il s'agit des URL que Twilio appelle lors de toute émission d'appel ou toute réception de SMS.</span><span class="sxs-lookup"><span data-stu-id="38ccf-193">These are the URLs that Twilio calls whenever a phone call is made or an SMS is sent to your number.</span></span> <span data-ttu-id="38ccf-194">On parle de « raccordements Web » pour désigner ces URL.</span><span class="sxs-lookup"><span data-stu-id="38ccf-194">The URLs are also known as "web hooks".</span></span>

<span data-ttu-id="38ccf-195">Nous voulons traiter les messages SMS entrants ; nous allons donc mettre à jour l’URL avec l’adresse `http://yourdomain.cloudapp.net/sms_url`.</span><span class="sxs-lookup"><span data-stu-id="38ccf-195">We would like to process incoming SMS messages, so let's update the URL to `http://yourdomain.cloudapp.net/sms_url`.</span></span> <span data-ttu-id="38ccf-196">Cliquez sur Save Changes en bas de la page pour poursuivre.</span><span class="sxs-lookup"><span data-stu-id="38ccf-196">Go ahead and click Save Changes at the bottom of the page.</span></span> <span data-ttu-id="38ccf-197">Revenons maintenant dans `web.rb` pour programmer notre application afin qu’elle exécute l’action suivante :</span><span class="sxs-lookup"><span data-stu-id="38ccf-197">Now, back in `web.rb` let's program our application to handle this:</span></span>

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for the ping! Twilio and Azure rock!</Message>
       </Response>"
    end

<span data-ttu-id="38ccf-198">Veillez à redémarrer l'application Web après avoir effectué cette modification.</span><span class="sxs-lookup"><span data-stu-id="38ccf-198">After making the change, make sure to re-start your web app.</span></span> <span data-ttu-id="38ccf-199">Maintenant, à l'aide de votre téléphone, envoyez un SMS à votre numéro Twilio.</span><span class="sxs-lookup"><span data-stu-id="38ccf-199">Now, take out your phone and send an SMS to your Twilio number.</span></span> <span data-ttu-id="38ccf-200">Vous devriez rapidement recevoir une réponse par SMS avec le message « Hey, merci pour le ping !</span><span class="sxs-lookup"><span data-stu-id="38ccf-200">You should promptly get an SMS response that says "Hey, thanks for the ping!</span></span> <span data-ttu-id="38ccf-201">Twilio et Azure sont les meilleurs ! »</span><span class="sxs-lookup"><span data-stu-id="38ccf-201">Twilio and Azure rock!".</span></span>

## <span data-ttu-id="38ccf-202"><a id="additional_services"></a>Utilisation de services Twilio supplémentaires</span><span class="sxs-lookup"><span data-stu-id="38ccf-202"><a id="additional_services"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="38ccf-203">En plus des exemples présentés ici, Twilio offre des API Web que vous pouvez utiliser pour tirer profit d'autres fonctionnalités de Twilio à partir de votre application Azure.</span><span class="sxs-lookup"><span data-stu-id="38ccf-203">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="38ccf-204">Pour plus d’informations, consultez la [documentation de l’API Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="38ccf-204">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

### <span data-ttu-id="38ccf-205"><a id="NextSteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="38ccf-205"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="38ccf-206">Maintenant que vous avez appris les bases du service Twilio, consultez ces liens pour en savoir plus :</span><span class="sxs-lookup"><span data-stu-id="38ccf-206">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="38ccf-207">[Conseils de sécurité Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="38ccf-207">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="38ccf-208">[Procédures et exemples de code Twilio][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="38ccf-208">[Twilio HowTos and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="38ccf-209">[Didacticiels de démarrage rapide Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="38ccf-209">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="38ccf-210">[Twilio sur GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="38ccf-210">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="38ccf-211">[Support Twilio][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="38ccf-211">[Talk to Twilio Support][twilio_support]</span></span>

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
