---
title: aaaHow tooUse Twilio pour la voix et SMS (Python) | Documents Microsoft
description: "Découvrez comment toomake un appel téléphonique et envoyer un SMS de message avec le service de l’API de Twilio hello sur Azure. Exemples de code écrits en Python."
services: 
documentationcenter: python
author: devinrader
manager: twilio
editor: 
ms.assetid: 561bc75b-4ac4-40ba-bcba-48e901f27cc3
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: 1f16a107d95c94589b8d61a0971c5b62d639c571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-python"></a><span data-ttu-id="3fbb9-104">Comment tooUse Twilio pour la voix et les fonctionnalités de SMS dans Python</span><span class="sxs-lookup"><span data-stu-id="3fbb9-104">How tooUse Twilio for Voice and SMS Capabilities in Python</span></span>
<span data-ttu-id="3fbb9-105">Ce guide montre comment tooperform des tâches de programmation courantes avec hello Twilio API de service sur Azure.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="3fbb9-106">scénarios de Hello couvertes incluent un appel téléphonique et envoi d’un message de Service SMS (Short Message).</span><span class="sxs-lookup"><span data-stu-id="3fbb9-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="3fbb9-107">Pour plus d’informations sur Twilio et à l’aide de la voix et SMS dans vos applications, consultez hello [étapes](#NextSteps) section.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="3fbb9-108"><a id="WhatIs"></a>Présentation de Twilio</span><span class="sxs-lookup"><span data-stu-id="3fbb9-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="3fbb9-109">Twilio est futures hello de communications professionnelles de mise sous tension, l’activation de voix de tooembed les développeurs, VoIP et dans les applications de messagerie.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="3fbb9-110">La virtualisation toute infrastructure nécessaires dans un environnement en nuage, global, exposant via la plateforme de hello Twilio communications API.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="3fbb9-111">Les applications sont toobuild simple et évolutive.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="3fbb9-112">Tirez parti de la souplesse du paiement à l'utilisation et de la fiabilité du cloud.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="3fbb9-113">**Twilio vocal** permet à votre toomake d’applications et de recevoir des appels téléphoniques.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span>
<span data-ttu-id="3fbb9-114">**Twilio SMS** Active toosend de votre application et de recevoir des messages texte.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-114">**Twilio SMS** enables your application toosend and receive text messages.</span></span>
<span data-ttu-id="3fbb9-115">**Client twilio sur** vous permet d’appels de VoIP toomake à partir de n’importe quel téléphone, tablette ou un navigateur et prend en charge WebRTC.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="3fbb9-116"><a id="Pricing"></a>Tarification de Twilio et offres spéciales</span><span class="sxs-lookup"><span data-stu-id="3fbb9-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="3fbb9-117">Les clients Azure reçoivent une [offre spéciale][special_offer] de 10 $ en crédit Twilio quand ils mettent à niveau leur compte Twilio.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-117">Azure customers receive a [special offer][special_offer] $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="3fbb9-118">Ce Twilio crédit peut être appliqué tooany l’utilisation de Twilio (10 $ crédit équivalent toosending jusqu'à 1 000 messages SMS et la réception des too1000 entrants voix minutes, selon emplacement hello de votre destination de nombre et de message ou d’appel téléphonique).</span><span class="sxs-lookup"><span data-stu-id="3fbb9-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="3fbb9-119">Profitez de ce [crédit Twilio][special_offer] et lancez-vous.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-119">Redeem this [Twilio credit][special_offer] and get started.</span></span>

<span data-ttu-id="3fbb9-120">Twilio est un service de paiement à l'utilisation.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="3fbb9-121">Il n'existe pas de frais d'entrée et vous pouvez fermer votre compte quand vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="3fbb9-122">Pour plus d’informations, consultez la page [Tarification de Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="3fbb9-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="3fbb9-123"><a id="Concepts"></a>Concepts</span><span class="sxs-lookup"><span data-stu-id="3fbb9-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="3fbb9-124">Hello Twilio API est une API RESTful qui fournit la voix et fonctionnalités SMS pour les applications.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="3fbb9-125">Les bibliothèques clientes sont disponibles dans plusieurs langues : pour en obtenir la liste, consultez la page [Bibliothèques de l’API Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="3fbb9-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="3fbb9-126">Les principaux aspects du hello Twilio API sont Twilio verbes et Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="3fbb9-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="3fbb9-127"><a id="Verbs"></a>Verbes Twilio</span><span class="sxs-lookup"><span data-stu-id="3fbb9-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="3fbb9-128">Hello API se sert de Twilio verbes ; par exemple, hello  **&lt;prononcer&gt;**  verbe fait en sorte que Twilio tooaudibly remettre un message sur un appel.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="3fbb9-129">Hello Voici une liste de verbes de Twilio.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-129">hello following is a list of Twilio verbs.</span></span> <span data-ttu-id="3fbb9-130">En savoir plus sur hello autres verbes et les fonctionnalités via [documentation de langage de balisage Twilio][twiml].</span><span class="sxs-lookup"><span data-stu-id="3fbb9-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation][twiml].</span></span>

* <span data-ttu-id="3fbb9-131">**&lt;Accès à distance&gt;**: se connecte phone de tooanother hello appelant.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="3fbb9-132">**&lt;Collecter des&gt;**: collecte les chiffres entrés sur le clavier de téléphone hello.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="3fbb9-133">**&lt;Hangup&gt;** : met fin à un appel.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="3fbb9-134">**&lt;Pause&gt;** : patiente silencieusement pendant un nombre déterminé de secondes.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="3fbb9-135">**&lt;Play&gt;** : lit un fichier audio.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-135">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="3fbb9-136">**&lt;File d’attente&gt;**: ajouter la file d’attente de tooa hello des appelants.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-136">**&lt;Queue&gt;**: Add hello tooa queue of callers.</span></span>
* <span data-ttu-id="3fbb9-137">**&lt;Enregistrement&gt;**: enregistre les voix hello de l’appelant de hello et retourne une URL d’un fichier contenant un enregistrement de hello.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-137">**&lt;Record&gt;**: Records hello voice of hello caller and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="3fbb9-138">**&lt;Rediriger&gt;**: transfère le contrôle d’un appel ou un SMS toohello TwiML à une autre URL.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-138">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="3fbb9-139">**&lt;Rejeter&gt;**: rejette un entrant appeler tooyour Twilio nombre sans vous de facturation.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-139">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you.</span></span>
* <span data-ttu-id="3fbb9-140">**&lt;Par exemple&gt;**: toospeech texte convertit effectuée sur un appel.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-140">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="3fbb9-141">**&lt;Sms&gt;** : envoie un SMS.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-141">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="3fbb9-142"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="3fbb9-142"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="3fbb9-143">TwiML est un ensemble d’instructions basé sur XML en fonction de verbes Twilio hello qui informent Twilio de façon tooprocess un appel ou un SMS.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-143">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="3fbb9-144">Par exemple, hello suivant TwiML permet de convertir le texte hello **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-144">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="3fbb9-145">Lorsque votre application appelle hello Twilio API, un des paramètres d’API hello est hello URL qui renvoie la réponse de TwiML hello.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-145">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="3fbb9-146">À des fins de développement, vous pouvez utiliser l’URL fournie par Twilio tooprovide hello TwiML les réponses employées par vos applications.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-146">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="3fbb9-147">Vous pourriez également héberger vos réponses de TwiML URL tooproduce hello et une autre option consiste à toouse hello `TwiMLResponse` objet.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-147">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello `TwiMLResponse` object.</span></span>

<span data-ttu-id="3fbb9-148">Pour plus d’informations sur les verbes Twilio, leurs attributs et le langage TwiML, consultez la page [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="3fbb9-148">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="3fbb9-149">Pour plus d’informations sur hello Twilio API, consultez [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="3fbb9-149">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="3fbb9-150"><a id="CreateAccount"></a>Créer un compte Twilio</span><span class="sxs-lookup"><span data-stu-id="3fbb9-150"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="3fbb9-151">Lorsque vous êtes prêt tooget un compte de Twilio, inscrivez-vous dans [essayez de Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="3fbb9-151">When you are ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="3fbb9-152">Vous pouvez commencer avec un compte gratuit, avant de le mettre à niveau ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-152">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="3fbb9-153">Quand vous vous inscrivez pour obtenir un compte Twilio, vous recevez un SID de compte et un jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-153">When you sign up for a Twilio account, you receive an account SID and an authentication token.</span></span> <span data-ttu-id="3fbb9-154">Les deux seront les appels d’API de Twilio toomake nécessaires.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-154">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="3fbb9-155">tooprevent non autorisé à accéder à tooyour compte, de sécuriser votre jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-155">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="3fbb9-156">Votre compte SID et le jeton d’authentification peuvent être consultés dans hello [Twilio Console][twilio_console], dans hello champs **SID de compte** et **dujetond’authentification**, respectivement.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-156">Your account SID and authentication token are viewable in hello [Twilio Console][twilio_console], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="3fbb9-157"><a id="create_app"></a>Créer une application Python</span><span class="sxs-lookup"><span data-stu-id="3fbb9-157"><a id="create_app"></a>Create a Python Application</span></span>
<span data-ttu-id="3fbb9-158">Une application de Python qui utilise le service de Twilio hello et s’exécute dans Azure n’est pas différente de toute autre application Python qui utilise le service de Twilio hello.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-158">A Python application that uses hello Twilio service and is running in Azure is no different than any other Python application that uses hello Twilio service.</span></span> <span data-ttu-id="3fbb9-159">Twilio services sont basés sur REST et peuvent être appelées à partir de Python de plusieurs façons, cet article se concentrera sur le fonctionnement des services avec toouse Twilio [bibliothèque Twilio pour Python à partir de GitHub][twilio_python].</span><span class="sxs-lookup"><span data-stu-id="3fbb9-159">While Twilio services are REST-based and can be called from Python in several ways, this article will focus on how toouse Twilio services with [Twilio library for Python from GitHub][twilio_python].</span></span> <span data-ttu-id="3fbb9-160">Pour plus d’informations sur l’utilisation de la bibliothèque de Twilio hello pour Python, consultez [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="3fbb9-160">For more information about using hello Twilio library for Python, see [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="3fbb9-161">Première, [configurer un nouvel ordinateur virtuel Azure Linux] tooact [azure_vm_setup] en tant qu’hôte pour votre nouvelle application web de Python.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-161">First, [set-up a new Azure Linux VM][azure_vm_setup] tooact as a host for your new Python web application.</span></span> <span data-ttu-id="3fbb9-162">Une fois que hello ordinateur virtuel est en cours d’exécution, vous devez tooexpose votre application sur un port public comme décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-162">Once hello Virtual Machine is running, you will need tooexpose your application on a public port as described below.</span></span>

### <a name="add-an-incoming-rule"></a><span data-ttu-id="3fbb9-163">Ajouter une règle entrante</span><span class="sxs-lookup"><span data-stu-id="3fbb9-163">Add An Incoming Rule</span></span>
  1. <span data-ttu-id="3fbb9-164">Accédez toohello [groupe de sécurité réseau] [azure_nsg] page.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-164">Go toohello [Network Security Group][azure_nsg] page.</span></span>
  2. <span data-ttu-id="3fbb9-165">Sélectionnez hello réseau de groupe de sécurité qui correspond à votre Machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-165">Select hello Network Security Group that corresponds with your Virtual Machine.</span></span>
  3. <span data-ttu-id="3fbb9-166">Ajoutez une **règle sortante** pour le **port 80**.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-166">Add and **Outgoing Rule** for **port 80**.</span></span> <span data-ttu-id="3fbb9-167">Être tooallow vraiment entrante à partir de n’importe quelle adresse.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-167">Be sure tooallow incoming from any address.</span></span>

### <a name="set-hello-dns-name-label"></a><span data-ttu-id="3fbb9-168">Ensemble hello étiquette de nom DNS</span><span class="sxs-lookup"><span data-stu-id="3fbb9-168">Set hello DNS Name Label</span></span>
  1. <span data-ttu-id="3fbb9-169">Accédez toohello [hello des Adresses IP publiques] [azure_ips] page.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-169">Go toohello [hello Public IP Adresses][azure_ips] page.</span></span>
  2. <span data-ttu-id="3fbb9-170">Sélectionnez hello adresse IP publique que correspends avec votre Machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-170">Select hello Public IP that correspends with your Virtual Machine.</span></span>
  3. <span data-ttu-id="3fbb9-171">Ensemble hello **étiquette de nom DNS** Bonjour **Configuration** section.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-171">Set hello **DNS Name Label** in hello **Configuration** section.</span></span> <span data-ttu-id="3fbb9-172">Dans les cas de hello de cet exemple montre comment il ressemble à ceci *votre nom de domaine*. centralus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="3fbb9-172">In hello case of this example it will look something like this *your-domain-label*.centralus.cloudapp.azure.com</span></span>

<span data-ttu-id="3fbb9-173">Une fois que vous êtes en mesure de tooconnect via SSH toohello Machine virtuelle que vous pouvez installer hello infrastructure Web de votre choix (hello plus connus dans Python étant deux [ballon](http://flask.pocoo.org/) et [Django](https://www.djangoproject.com)).</span><span class="sxs-lookup"><span data-stu-id="3fbb9-173">Once you are able tooconnect through SSH toohello Virtual Machine you can install hello Web Framework of your choice (hello two most well known in Python being [Flask](http://flask.pocoo.org/) and [Django](https://www.djangoproject.com)).</span></span> <span data-ttu-id="3fbb9-174">Vous pouvez installer un d’eux simplement en exécutant hello `pip install` commande.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-174">You can install either of them just by running hello `pip install` command.</span></span>

<span data-ttu-id="3fbb9-175">Gardez à l’esprit que nous avons configuré tooallow le trafic de la Machine virtuelle hello uniquement sur le port 80.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-175">Keep in mind that we configured hello Virtual Machine tooallow traffic only on port 80.</span></span> <span data-ttu-id="3fbb9-176">Par conséquent, assurez-vous que tooconfigure hello application toouse ce port.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-176">So make sure tooconfigure hello application toouse this port.</span></span>

## <span data-ttu-id="3fbb9-177"><a id="configure_app"></a>Configurez des bibliothèques de votre Application tooUse Twilio</span><span class="sxs-lookup"><span data-stu-id="3fbb9-177"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="3fbb9-178">Vous pouvez configurer votre bibliothèque de Twilio application toouse hello pour Python de deux manières :</span><span class="sxs-lookup"><span data-stu-id="3fbb9-178">You can configure your application toouse hello Twilio library for Python in two ways:</span></span>

* <span data-ttu-id="3fbb9-179">Installer la bibliothèque de Twilio hello pour Python en tant que package Pip.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-179">Install hello Twilio library for Python as a Pip package.</span></span> <span data-ttu-id="3fbb9-180">Il peut être installé avec hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="3fbb9-180">It can be installed with hello following commands:</span></span>
   
        $ pip install twilio

    <span data-ttu-id="3fbb9-181">OU</span><span class="sxs-lookup"><span data-stu-id="3fbb9-181">-OR-</span></span>

* <span data-ttu-id="3fbb9-182">Télécharger la bibliothèque de Twilio hello pour Python à partir de GitHub ([https://github.com/twilio/twilio-python][twilio_python]) et l’installer comme suit :</span><span class="sxs-lookup"><span data-stu-id="3fbb9-182">Download hello Twilio library for Python from GitHub ([https://github.com/twilio/twilio-python][twilio_python]) and install it like this:</span></span>

        $ python setup.py install

<span data-ttu-id="3fbb9-183">Une fois que vous avez installé la bibliothèque de Twilio hello pour Python, vous pouvez ensuite `import` dans vos fichiers Python :</span><span class="sxs-lookup"><span data-stu-id="3fbb9-183">Once you have installed hello Twilio library for Python, you can then `import` it in your Python files:</span></span>

        import twilio

<span data-ttu-id="3fbb9-184">Pour plus d’informations, consultez [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="3fbb9-184">For more information, see [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="3fbb9-185"><a id="howto_make_call"></a>Procédure : passer un appel sortant</span><span class="sxs-lookup"><span data-stu-id="3fbb9-185"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="3fbb9-186">Hello suivant montre comment appeler le toomake sortante.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-186">hello following shows how toomake an outgoing call.</span></span> <span data-ttu-id="3fbb9-187">Ce code utilise également un Bonjour de tooreturn site fournie par Twilio réponse de Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="3fbb9-187">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="3fbb9-188">Remplacez par vos valeurs hello **from_number** et **to_number** les numéros de téléphone et assurez-vous que vous avez vérifié hello **from_number** numéro de téléphone de votre compte Twilio avant d’exécuter un code hello.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-188">Substitute your values for hello **from_number** and **to_number** phone numbers, and ensure that you've verified hello **from_number** phone number for your Twilio account before running hello code.</span></span>

    from urllib.parse import urlencode

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from_number = "NNNNNNNNNNN"

    # hello number of hello phone receiving call.
    to_number = "NNNNNNNNNNN"

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://twimlets.com/message?"

    # hello phone message text.
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url + urlencode({'Message': message}))
    print(call.sid)

<span data-ttu-id="3fbb9-189">Comme indiqué, ce code utilise un Bonjour de tooreturn TwiML réponse Twilio fournie par site.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-189">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="3fbb9-190">Vous pouvez utiliser votre propre hello tooprovide de site TwiML réponse ; Pour plus d’informations, consultez [comment tooProvide TwiML les réponses à partir de votre propre Site Web](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="3fbb9-190">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="3fbb9-191"><a id="howto_send_sms"></a>Procédure : envoi d'un message SMS</span><span class="sxs-lookup"><span data-stu-id="3fbb9-191"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="3fbb9-192">Hello suivant montre comment un message SMS à l’aide de toosend hello `TwilioRestClient` classe.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-192">hello following shows how toosend an SMS message using hello `TwilioRestClient` class.</span></span> <span data-ttu-id="3fbb9-193">Hello **from_number** numéro est fourni par Twilio pour évaluation comptes toosend de SMS.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-193">hello **from_number** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="3fbb9-194">Hello **to_number** nombre doit être vérifié pour votre compte Twilio avant d’exécuter le code de hello.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-194">hello **to_number** number must be verified for your Twilio account before running hello code.</span></span>

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    from_number = "NNNNNNNNNNN"  # With trial account, texts can only be sent from your Twilio number.
    to_number = "NNNNNNNNNNN"
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Send hello SMS message.
    message = client.messages.create(to=to_number,
                                     from_=from_number,
                                     body=message)

## <span data-ttu-id="3fbb9-195"><a id="howto_provide_twiml_responses"></a>Procédure : envoi de réponses TwiML depuis votre propre site web</span><span class="sxs-lookup"><span data-stu-id="3fbb9-195"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="3fbb9-196">Lorsque votre application lance un appel de toohello Twilio API, Twilio enverra votre URL tooa demande attendu tooreturn une réponse TwiML.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-196">When your application initiates a call toohello Twilio API, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="3fbb9-197">exemple Hello ci-dessus utilise les URL fournie par Twilio hello [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="3fbb9-197">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="3fbb9-198">Comme TwiML est conçu pour être utilisé par Twilio, vous pouvez l’afficher dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-198">(While TwiML is designed for use by Twilio, you can view it in your browser.</span></span> <span data-ttu-id="3fbb9-199">Par exemple, cliquez sur [http://twimlets.com/message] [ twimlet_message_url] toosee vide `<Response>` élément ; un autre exemple, cliquez sur [http://twimlets.com/message? Message % 5B0 %5, D = Hello % 20World] [ twimlet_message_url_hello_world] toosee un `<Response>` élément contenant un `<Say>` élément.)</span><span class="sxs-lookup"><span data-stu-id="3fbb9-199">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] toosee a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="3fbb9-200">Au lieu d’utiliser les URL fournie par Twilio hello, vous pouvez créer votre propre site qui renvoie des réponses HTTP.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-200">Instead of relying on hello Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="3fbb9-201">Vous pouvez créer le site de hello dans n’importe quel langage qui retourne les réponses XML ; Cette rubrique suppose que vous utiliserez hello toocreate de Python TwiML.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-201">You can create hello site in any language that returns XML responses; this topic assumes you will be using Python toocreate hello TwiML.</span></span>

<span data-ttu-id="3fbb9-202">Hello exemples suivants produira une réponse TwiML indiquant que **Hello World** sur l’appel de hello.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-202">hello following examples will output a TwiML response that says **Hello World** on hello call.</span></span>

<span data-ttu-id="3fbb9-203">Avec Flask :</span><span class="sxs-lookup"><span data-stu-id="3fbb9-203">With Flask:</span></span>

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

<span data-ttu-id="3fbb9-204">Avec Django :</span><span class="sxs-lookup"><span data-stu-id="3fbb9-204">With Django:</span></span>

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

<span data-ttu-id="3fbb9-205">Comme vous pouvez le voir à partir de l’exemple hello ci-dessus, hello TwiML réponse est simplement un document XML.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-205">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="3fbb9-206">bibliothèque de Twilio Hello pour Python contient des classes qui génèrent TwiML pour vous.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-206">hello Twilio library for Python contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="3fbb9-207">Hello exemple ci-dessous génère réponse équivalent de hello comme indiqué ci-dessus, mais utilise hello `twiml` module dans la bibliothèque de Twilio hello pour Python :</span><span class="sxs-lookup"><span data-stu-id="3fbb9-207">hello example below produces hello equivalent response as shown above, but uses hello `twiml` module in hello Twilio library for Python:</span></span>

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

<span data-ttu-id="3fbb9-208">Pour plus d’informations sur TwiML, consultez la page [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="3fbb9-208">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span>

<span data-ttu-id="3fbb9-209">Une fois que votre application Python configurer tooprovide TwiML réponses, utilisez hello les URL de l’application hello comme hello URL passée hello `client.calls.create` (méthode).</span><span class="sxs-lookup"><span data-stu-id="3fbb9-209">Once you have your Python application set up tooprovide TwiML responses, use hello URL of hello application as hello URL passed into hello `client.calls.create`  method.</span></span> <span data-ttu-id="3fbb9-210">Par exemple, si vous avez une application Web nommée **MyTwiML** tooan déployé Azure le service hébergé, vous pouvez utiliser des son url en tant que webhook, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="3fbb9-210">For example, if you have a Web application named **MyTwiML** deployed tooan Azure hosted service, you can use its url as webhook as shown in hello following example:</span></span>

    from twilio.rest import TwilioRestClient

    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"
    from_number = "NNNNNNNNNNN"
    to_number = "NNNNNNNNNNN"
    url = "http://your-domain-label.centralus.cloudapp.azure.com/MyTwiML/"

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url)
    print(call.sid)

## <span data-ttu-id="3fbb9-211"><a id="AdditionalServices"></a>Utilisation de services Twilio supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3fbb9-211"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="3fbb9-212">En outre toohello les exemples indiqués ici, que twilio propose des API basées sur le web qui vous pouvez utiliser des fonctionnalités Twilio tooleverage supplémentaires à partir de votre application Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="3fbb9-212">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="3fbb9-213">Pour plus d’informations, consultez hello [documentation de l’API de Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="3fbb9-213">For full details, see hello [Twilio API documentation][twilio_api].</span></span>

## <span data-ttu-id="3fbb9-214"><a id="NextSteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3fbb9-214"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="3fbb9-215">Maintenant que vous avez appris les notions de base de hello Hello Twilio service, suivez ces liens de toolearn plus :</span><span class="sxs-lookup"><span data-stu-id="3fbb9-215">Now that you have learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="3fbb9-216">[Conseils de sécurité Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="3fbb9-216">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="3fbb9-217">[Procédures et exemples de code Twilio][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="3fbb9-217">[Twilio HowTo Guides and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="3fbb9-218">[Didacticiels de démarrage rapide Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="3fbb9-218">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="3fbb9-219">[Twilio sur GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="3fbb9-219">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="3fbb9-220">[Communiquer avec tooTwilio prise en charge][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="3fbb9-220">[Talk tooTwilio Support][twilio_support]</span></span>

[special_offer]: http://ahoy.twilio.com/azure
[twilio_python]: https://github.com/twilio/twilio-python
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-python/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-python/blob/master/README.md

[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
[twilio_pricing]: http://www.twilio.com/pricing

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
