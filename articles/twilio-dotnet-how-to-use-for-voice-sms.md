---
title: aaaHow tooUse Twilio pour la voix et SMS (.NET) | Documents Microsoft
description: "Découvrez comment toomake un appel téléphonique et envoyer un SMS de message avec le service de l’API de Twilio hello sur Azure. Exemples de code écrits en .NET."
services: 
documentationcenter: .net
author: devinrader
manager: twilio
editor: 
ms.assetid: 74d4f3c9-f1cb-4968-b744-36b32cd0e834
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/24/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: f568da87ef15e9f540fee9674de31e983d4acb6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-from-azure"></a><span data-ttu-id="5961b-104">Comment toouse Twilio pour la voix et les fonctionnalités SMS à partir de Azure</span><span class="sxs-lookup"><span data-stu-id="5961b-104">How toouse Twilio for voice and SMS capabilities from Azure</span></span>
<span data-ttu-id="5961b-105">Ce guide montre comment tooperform des tâches de programmation courantes avec hello Twilio API de service sur Azure.</span><span class="sxs-lookup"><span data-stu-id="5961b-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="5961b-106">scénarios de Hello couvertes incluent un appel téléphonique et envoi d’un message de Service SMS (Short Message).</span><span class="sxs-lookup"><span data-stu-id="5961b-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="5961b-107">Pour plus d’informations sur Twilio et à l’aide de la voix et SMS dans vos applications, consultez hello [étapes](#NextSteps) section.</span><span class="sxs-lookup"><span data-stu-id="5961b-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next steps](#NextSteps) section.</span></span>

## <span data-ttu-id="5961b-108"><a id="WhatIs"></a>Présentation de Twilio</span><span class="sxs-lookup"><span data-stu-id="5961b-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="5961b-109">Twilio est futures hello de communications professionnelles de mise sous tension, l’activation de voix de tooembed les développeurs, VoIP et dans les applications de messagerie.</span><span class="sxs-lookup"><span data-stu-id="5961b-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="5961b-110">La virtualisation toute infrastructure nécessaires dans un environnement en nuage, global, exposant via la plateforme de hello Twilio communications API.</span><span class="sxs-lookup"><span data-stu-id="5961b-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="5961b-111">Les applications sont toobuild simple et évolutive.</span><span class="sxs-lookup"><span data-stu-id="5961b-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="5961b-112">Tirez parti de la souplesse du paiement à l’utilisation et de la fiabilité du cloud.</span><span class="sxs-lookup"><span data-stu-id="5961b-112">Enjoy flexibility with pay-as-you-go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="5961b-113">**Twilio vocal** permet à votre toomake d’applications et de recevoir des appels téléphoniques.</span><span class="sxs-lookup"><span data-stu-id="5961b-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="5961b-114">**Twilio SMS** Active toosend de vos applications et de recevoir des messages SMS.</span><span class="sxs-lookup"><span data-stu-id="5961b-114">**Twilio SMS** enables your applications toosend and receive SMS messages.</span></span> <span data-ttu-id="5961b-115">**Client twilio sur** vous permet d’appels de VoIP toomake à partir de n’importe quel téléphone, tablette ou un navigateur et prend en charge WebRTC.</span><span class="sxs-lookup"><span data-stu-id="5961b-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="5961b-116"><a id="Pricing"></a>Tarification de Twilio et offres spéciales</span><span class="sxs-lookup"><span data-stu-id="5961b-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="5961b-117">Les clients Azure reçoivent une [offre spéciale](http://www.twilio.com/azure)de 10 $ en crédit Twilio lorsqu'ils mettent à niveau leur compte Twilio.</span><span class="sxs-lookup"><span data-stu-id="5961b-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="5961b-118">Ce Twilio crédit peut être appliqué tooany l’utilisation de Twilio (10 $ crédit équivalent toosending jusqu'à 1 000 messages SMS et la réception des too1000 entrants voix minutes, selon emplacement hello de votre destination de nombre et de message ou d’appel téléphonique).</span><span class="sxs-lookup"><span data-stu-id="5961b-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="5961b-119">Profitez de ce crédit Twilio et démarrez en consultant la page [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="5961b-119">Redeem this Twilio credit and get started at [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="5961b-120">Twilio est un service de paiement à l'utilisation.</span><span class="sxs-lookup"><span data-stu-id="5961b-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="5961b-121">Il n’y a pas de frais d’entrée et vous pouvez fermer votre compte quand vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="5961b-121">There are no set-up fees, and you can close your account at any time.</span></span> <span data-ttu-id="5961b-122">Pour plus d'informations, consultez la page [Tarification de Twilio](http://www.twilio.com/voice/pricing).</span><span class="sxs-lookup"><span data-stu-id="5961b-122">You can find more details at [Twilio Pricing](http://www.twilio.com/voice/pricing).</span></span>

## <span data-ttu-id="5961b-123"><a id="Concepts"></a>Concepts</span><span class="sxs-lookup"><span data-stu-id="5961b-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="5961b-124">Hello Twilio API est une API RESTful qui fournit la voix et fonctionnalités SMS pour les applications.</span><span class="sxs-lookup"><span data-stu-id="5961b-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="5961b-125">Les bibliothèques clientes sont disponibles dans plusieurs langues : pour en obtenir la liste, consultez la page [Bibliothèques de l’API Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="5961b-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="5961b-126">Les principaux aspects du hello Twilio API sont Twilio verbes et Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="5961b-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="5961b-127"><a id="Verbs"></a>Verbes Twilio</span><span class="sxs-lookup"><span data-stu-id="5961b-127"><a id="Verbs"></a>Twilio verbs</span></span>
<span data-ttu-id="5961b-128">Hello API se sert de Twilio verbes ; par exemple, hello  **&lt;prononcer&gt;**  verbe fait en sorte que Twilio tooaudibly remettre un message sur un appel.</span><span class="sxs-lookup"><span data-stu-id="5961b-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="5961b-129">Hello Voici une liste de verbes de Twilio.</span><span class="sxs-lookup"><span data-stu-id="5961b-129">hello following is a list of Twilio verbs.</span></span>  <span data-ttu-id="5961b-130">En savoir plus sur hello autres verbes et les fonctionnalités via [documentation de langage de balisage Twilio](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="5961b-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="5961b-131">**&lt;Accès à distance&gt;**: se connecte phone de tooanother hello appelant.</span><span class="sxs-lookup"><span data-stu-id="5961b-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="5961b-132">**&lt;Collecter des&gt;**: collecte les chiffres entrés sur le clavier de téléphone hello.</span><span class="sxs-lookup"><span data-stu-id="5961b-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="5961b-133">**&lt;Hangup&gt;** : met fin à un appel.</span><span class="sxs-lookup"><span data-stu-id="5961b-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="5961b-134">**&lt;Play&gt;** : lit un fichier audio.</span><span class="sxs-lookup"><span data-stu-id="5961b-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="5961b-135">**&lt;Pause&gt;** : patiente silencieusement pendant un nombre déterminé de secondes.</span><span class="sxs-lookup"><span data-stu-id="5961b-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="5961b-136">**&lt;Enregistrement&gt;**: enregistre la voix de l’appelant hello et retourne une URL d’un fichier contenant un enregistrement de hello.</span><span class="sxs-lookup"><span data-stu-id="5961b-136">**&lt;Record&gt;**: Records hello caller's voice and returns an URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="5961b-137">**&lt;Rediriger&gt;**: transfère le contrôle d’un appel ou un SMS toohello TwiML à une autre URL.</span><span class="sxs-lookup"><span data-stu-id="5961b-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="5961b-138">**&lt;Rejeter&gt;**: rejette un entrant appeler tooyour Twilio nombre sans vous de facturation</span><span class="sxs-lookup"><span data-stu-id="5961b-138">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="5961b-139">**&lt;Par exemple&gt;**: toospeech texte convertit effectuée sur un appel.</span><span class="sxs-lookup"><span data-stu-id="5961b-139">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="5961b-140">**&lt;Sms&gt;** : envoie un SMS.</span><span class="sxs-lookup"><span data-stu-id="5961b-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="5961b-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="5961b-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="5961b-142">TwiML est un ensemble d’instructions basé sur XML en fonction de verbes Twilio hello qui informent Twilio de façon tooprocess un appel ou un SMS.</span><span class="sxs-lookup"><span data-stu-id="5961b-142">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="5961b-143">Par exemple, hello suivant TwiML permet de convertir le texte hello **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="5961b-143">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="5961b-144">Lorsque votre application appelle hello Twilio API, un des paramètres d’API hello est hello URL qui renvoie la réponse de TwiML hello.</span><span class="sxs-lookup"><span data-stu-id="5961b-144">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="5961b-145">À des fins de développement, vous pouvez utiliser l’URL fournie par Twilio tooprovide hello TwiML les réponses employées par vos applications.</span><span class="sxs-lookup"><span data-stu-id="5961b-145">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="5961b-146">Vous pourriez également héberger vos réponses de TwiML URL tooproduce hello et une autre option consiste à toouse hello **TwiMLResponse** objet.</span><span class="sxs-lookup"><span data-stu-id="5961b-146">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="5961b-147">Pour plus d’informations sur les verbes Twilio, leurs attributs et le langage TwiML, consultez la page [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="5961b-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="5961b-148">Pour plus d’informations sur hello Twilio API, consultez [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="5961b-148">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="5961b-149"><a id="CreateAccount"></a>Créer un compte Twilio</span><span class="sxs-lookup"><span data-stu-id="5961b-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="5961b-150">Lorsque vous êtes prêt tooget un compte de Twilio, inscrivez-vous dans [essayez de Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="5961b-150">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="5961b-151">Vous pouvez commencer avec un compte gratuit, avant de le mettre à niveau ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="5961b-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="5961b-152">Lorsque vous créez un compte Twilio, vous recevez un ID de compte et un jeton d'authentification.</span><span class="sxs-lookup"><span data-stu-id="5961b-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="5961b-153">Les deux seront les appels d’API de Twilio toomake nécessaires.</span><span class="sxs-lookup"><span data-stu-id="5961b-153">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="5961b-154">tooprevent non autorisé à accéder à tooyour compte, de sécuriser votre jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="5961b-154">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="5961b-155">Votre ID de compte et l’authentification jeton peuvent être consultés à hello [page de compte Twilio][twilio_account], dans hello champs **SID de compte** et **dujetond’authentification**, respectivement.</span><span class="sxs-lookup"><span data-stu-id="5961b-155">Your account ID and authentication token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="5961b-156"><a id="create_app"></a>Créer une application Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5961b-156"><a id="create_app"></a>Create an Azure Application</span></span>
<span data-ttu-id="5961b-157">Une application Azure qui héberge une application Twilio n'est pas différente d'une autre application Azure.</span><span class="sxs-lookup"><span data-stu-id="5961b-157">An Azure application that hosts a Twilio enabled application is no different from any other Azure application.</span></span> <span data-ttu-id="5961b-158">Ajout d’une bibliothèque de Twilio .NET hello et de configurer hello rôle toouse hello Twilio les bibliothèques .NET.</span><span class="sxs-lookup"><span data-stu-id="5961b-158">You add hello Twilio .NET library and configure hello role toouse hello Twilio .NET libraries.</span></span>
<span data-ttu-id="5961b-159">Pour plus d’informations sur la création d’un projet Azure initial, consultez la page [Création d’un projet Azure avec Visual Studio][vs_project].</span><span class="sxs-lookup"><span data-stu-id="5961b-159">For information on creating an initial Azure project, see [Creating an Azure project with Visual Studio][vs_project].</span></span>

## <span data-ttu-id="5961b-160"><a id="configure_app"></a>Configurez des bibliothèques de votre Application toouse Twilio</span><span class="sxs-lookup"><span data-stu-id="5961b-160"><a id="configure_app"></a>Configure Your Application toouse Twilio Libraries</span></span>
<span data-ttu-id="5961b-161">Twilio fournit un ensemble de bibliothèques .NET d’assistance qui encapsulent les divers aspects de Twilio tooprovide facilement et simple toointeract avec hello API REST de Twilio et Twilio Client toogenerate TwiML réponses.</span><span class="sxs-lookup"><span data-stu-id="5961b-161">Twilio provides a set of .NET helper libraries that wrap various aspects of Twilio tooprovide simple and easy ways toointeract with hello Twilio REST API and Twilio Client toogenerate TwiML responses.</span></span>

<span data-ttu-id="5961b-162">Twilio offre cinq bibliothèques destinées aux développeurs .NET :</span><span class="sxs-lookup"><span data-stu-id="5961b-162">Twilio provides five libraries for .NET developers:</span></span>
<span data-ttu-id="5961b-163">Bibliothèque</span><span class="sxs-lookup"><span data-stu-id="5961b-163">Library</span></span>|<span data-ttu-id="5961b-164">Description</span><span class="sxs-lookup"><span data-stu-id="5961b-164">Description</span></span>
---|---
<span data-ttu-id="5961b-165">Twilio.API</span><span class="sxs-lookup"><span data-stu-id="5961b-165">Twilio.API</span></span>|<span data-ttu-id="5961b-166">Hello Twilio bibliothèque principale qui encapsule hello API REST de Twilio dans une bibliothèque .NET conviviale.</span><span class="sxs-lookup"><span data-stu-id="5961b-166">hello core Twilio library that wraps hello Twilio REST API in a friendly .NET library.</span></span> <span data-ttu-id="5961b-167">Cette bibliothèque est disponible pour .NET, Silverlight et Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="5961b-167">This library is available for .NET, Silverlight, and Windows Phone 7.</span></span>
<span data-ttu-id="5961b-168">Twilio.TwiML</span><span class="sxs-lookup"><span data-stu-id="5961b-168">Twilio.TwiML</span></span>|<span data-ttu-id="5961b-169">Fournit un balisage de TwiML toogenerate .NET manière conviviale.</span><span class="sxs-lookup"><span data-stu-id="5961b-169">Provides a .NET friendly way toogenerate TwiML markup.</span></span>
<span data-ttu-id="5961b-170">Twilio.MVC</span><span class="sxs-lookup"><span data-stu-id="5961b-170">Twilio.MVC</span></span>|<span data-ttu-id="5961b-171">Pour les développeurs utilisant ASP.NET MVC, cette bibliothèque inclut TwilioController, TwiML ActionResult et un attribut de validation de demande.</span><span class="sxs-lookup"><span data-stu-id="5961b-171">For developers using ASP.NET MVC, this library includes a TwilioController, TwiML ActionResult, and request validation attribute.</span></span>
<span data-ttu-id="5961b-172">Twilio.WebMatrix</span><span class="sxs-lookup"><span data-stu-id="5961b-172">Twilio.WebMatrix</span></span>|<span data-ttu-id="5961b-173">Pour les développeurs utilisant l'outil de développement WebMatrix gratuit de Microsoft, cette bibliothèque contient les aides à la syntaxe Razor pour différentes actions Twilio.</span><span class="sxs-lookup"><span data-stu-id="5961b-173">For developers using Microsoft's free WebMatrix development tool, this library contains Razor syntax helpers for various Twilio actions.</span></span>
<span data-ttu-id="5961b-174">Twilio.Client.Capability</span><span class="sxs-lookup"><span data-stu-id="5961b-174">Twilio.Client.Capability</span></span>|<span data-ttu-id="5961b-175">Contient le Générateur de jetons de capacité hello pour une utilisation avec hello Twilio Client JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="5961b-175">Contains hello Capability token generator for use with hello Twilio Client JavaScript SDK.</span></span>

<span data-ttu-id="5961b-176">Notez que toutes les bibliothèques nécessitent .NET 3.5, Silverlight 4 ou Windows Phone 7 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="5961b-176">Note that all libraries require .NET 3.5, Silverlight 4, or Windows Phone 7 or later.</span></span>

<span data-ttu-id="5961b-177">les exemples de Hello fournies dans ce guide utilisent la bibliothèque de Twilio.API hello.</span><span class="sxs-lookup"><span data-stu-id="5961b-177">hello samples provided in this guide use hello Twilio.API library.</span></span>

<span data-ttu-id="5961b-178">Hello bibliothèques peuvent être [installé à l’aide d’extension hello du Gestionnaire de package NuGet](http://www.twilio.com/docs/csharp/install) too2015 disponibles pour Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="5961b-178">hello libraries can be [installed using hello NuGet package manager extension](http://www.twilio.com/docs/csharp/install) available for Visual Studio 2010 up too2015.</span></span>  <span data-ttu-id="5961b-179">code source Hello est hébergé sur [GitHub][twilio_github_repo], qui inclut un site Wiki qui contient une documentation complète pour l’utilisation de bibliothèques de hello.</span><span class="sxs-lookup"><span data-stu-id="5961b-179">hello source code is hosted on [GitHub][twilio_github_repo], which includes a Wiki that contains complete documentation for using hello libraries.</span></span>

<span data-ttu-id="5961b-180">Par défaut, Microsoft Visual Studio 2010 installe la version 1.2 de NuGet.</span><span class="sxs-lookup"><span data-stu-id="5961b-180">By default, Microsoft Visual Studio 2010 installs version 1.2 of NuGet.</span></span> <span data-ttu-id="5961b-181">L’installation des bibliothèques de Twilio hello requiert la version 1.6 de NuGet ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="5961b-181">Installing hello Twilio libraries requires version 1.6 of NuGet or higher.</span></span> <span data-ttu-id="5961b-182">Pour plus d’informations sur l’installation ou la mise à jour de NuGet, consultez le site [http://nuget.org/][nuget].</span><span class="sxs-lookup"><span data-stu-id="5961b-182">For information on installing or updating NuGet, see [http://nuget.org/][nuget].</span></span>

> [!NOTE]
> <span data-ttu-id="5961b-183">version la plus récente hello tooinstall de NuGet, vous devez d’abord désinstaller hello de version chargée à l’aide de hello Gestionnaire d’extensions Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5961b-183">tooinstall hello latest version of NuGet, you must first uninstall hello loaded version using hello Visual Studio Extension Manager.</span></span> <span data-ttu-id="5961b-184">toodo par conséquent, vous devez exécuter Visual Studio en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5961b-184">toodo so, you must run Visual Studio as administrator.</span></span> <span data-ttu-id="5961b-185">Sinon, le bouton de désinstaller hello est désactivée.</span><span class="sxs-lookup"><span data-stu-id="5961b-185">Otherwise, hello Uninstall button is disabled.</span></span>
>
>

### <span data-ttu-id="5961b-186"><a id="use_nuget"></a>tooadd hello Twilio bibliothèques tooyour Visual Studio un projet :</span><span class="sxs-lookup"><span data-stu-id="5961b-186"><a id="use_nuget"></a>tooadd hello Twilio libraries tooyour Visual Studio project:</span></span>
1. <span data-ttu-id="5961b-187">Ouvrez votre solution dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5961b-187">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="5961b-188">Cliquez avec le bouton droit sur **Références**.</span><span class="sxs-lookup"><span data-stu-id="5961b-188">Right-click **References**.</span></span>
3. <span data-ttu-id="5961b-189">Cliquez sur **Gérer les packages NuGet...**</span><span class="sxs-lookup"><span data-stu-id="5961b-189">Click **Manage NuGet Packages...**</span></span>
4. <span data-ttu-id="5961b-190">Cliquez sur **En ligne**.</span><span class="sxs-lookup"><span data-stu-id="5961b-190">Click **Online**.</span></span>
5. <span data-ttu-id="5961b-191">Dans la zone en ligne de recherche hello, tapez *twilio*.</span><span class="sxs-lookup"><span data-stu-id="5961b-191">In hello search online box, type *twilio*.</span></span>
6. <span data-ttu-id="5961b-192">Cliquez sur **installer** sur le package de Twilio hello.</span><span class="sxs-lookup"><span data-stu-id="5961b-192">Click **Install** on hello Twilio package.</span></span>

## <span data-ttu-id="5961b-193"><a id="howto_make_call"></a>Procédure : passer un appel sortant</span><span class="sxs-lookup"><span data-stu-id="5961b-193"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="5961b-194">Hello suivant montre comment toomake sortante appeler à l’aide de hello **CallResource** classe.</span><span class="sxs-lookup"><span data-stu-id="5961b-194">hello following shows how toomake an outgoing call using hello **CallResource** class.</span></span> <span data-ttu-id="5961b-195">Ce code utilise également un Bonjour de tooreturn site fournie par Twilio réponse de Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="5961b-195">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="5961b-196">Remplacez par vos valeurs hello **à** et **de** les numéros de téléphone et assurez-vous que vous vérifiez hello **de** numéro de téléphone de votre compte Twilio avant d’exécuter le code de hello.</span><span class="sxs-lookup"><span data-stu-id="5961b-196">Substitute your values for hello **to** and **from** phone numbers, and ensure that you verify hello **from** phone number for your Twilio account before running hello code.</span></span>

    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize hello TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    var url = "http://twimlets.com/message";
    url = $"{url}?Message%5B0%5D=Hello%20World";

    // Set hello call From, To, and URL values toouse for hello call.
    // This sample uses hello sandbox number provided by
    // Twilio toomake hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri(url));
        }

<span data-ttu-id="5961b-197">Pour plus d’informations sur les paramètres de hello passés dans toohello **CallResource.Create** méthode, consultez [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="5961b-197">For more information about hello parameters passed in toohello **CallResource.Create** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="5961b-198">Comme indiqué, ce code utilise un Bonjour de tooreturn TwiML réponse Twilio fournie par site.</span><span class="sxs-lookup"><span data-stu-id="5961b-198">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="5961b-199">Vous pouvez utiliser votre propre hello tooprovide de site TwiML réponse.</span><span class="sxs-lookup"><span data-stu-id="5961b-199">You could instead use your own site tooprovide hello TwiML response.</span></span> <span data-ttu-id="5961b-200">Pour plus d’informations, consultez [Envoi de réponses TwiML à partir de votre propre site web](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="5961b-200">For more information, see [How to: Provide TwiML responses from your own website](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="5961b-201"><a id="howto_send_sms"></a>Procédure : envoi d'un message SMS</span><span class="sxs-lookup"><span data-stu-id="5961b-201"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="5961b-202">Hello capture d’écran suivante montre comment un message SMS à l’aide de toosend hello **MessageResource** classe.</span><span class="sxs-lookup"><span data-stu-id="5961b-202">hello following screenshot shows how toosend an SMS message using hello **MessageResource**  class.</span></span> <span data-ttu-id="5961b-203">Hello **de** numéro est fourni par Twilio pour évaluation comptes toosend de SMS.</span><span class="sxs-lookup"><span data-stu-id="5961b-203">hello **from** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="5961b-204">Hello **à** nombre doit être vérifié pour votre compte Twilio avant d’exécuter le code de hello.</span><span class="sxs-lookup"><span data-stu-id="5961b-204">hello **to** number must be verified for your Twilio account before you run hello code.</span></span>

    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize hello TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    try
    {
        // Send an SMS message.
        var message = MessageResource.Create(
            to: new PhoneNumber("+12069419717"),
            from: new PhoneNumber("+14155992671"),
            body: "This is my SMS message.");
    }
    catch (TwilioException ex)
    {
        // An exception occurred making hello REST call
        Console.WriteLine(ex.Message);
    }

## <span data-ttu-id="5961b-205"><a id="howto_provide_twiml_responses"></a>Procédure : envoi de réponses TwiML depuis votre propre site Web</span><span class="sxs-lookup"><span data-stu-id="5961b-205"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own website</span></span>
<span data-ttu-id="5961b-206">Lorsque votre application démarre, par exemple, un toohello d’appels API de Twilio - via hello **CallResource.Create** méthode - Twilio votre URL tooan demande tooreturn attendu envoie une réponse TwiML.</span><span class="sxs-lookup"><span data-stu-id="5961b-206">When your application initiates a call toohello Twilio API - for example, via hello **CallResource.Create** method - Twilio sends your request tooan URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="5961b-207">exemple Hello dans [Comment : effectuer un appel sortant](#howto_make_call) utilise hello URL fournie par Twilio [http://twimlets.com/message] [ twimlet_message_url] réponse de hello tooreturn.</span><span class="sxs-lookup"><span data-stu-id="5961b-207">hello example in [How to: Make an outgoing call](#howto_make_call) uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url] tooreturn hello response.</span></span>

> [!NOTE]
> <span data-ttu-id="5961b-208">TwiML est conçu pour une utilisation par les services web, vous pouvez afficher hello TwiML dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="5961b-208">While TwiML is designed for use by web services, you can view hello TwiML in your browser.</span></span> <span data-ttu-id="5961b-209">Par exemple, cliquez sur [http://twimlets.com/message] [ twimlet_message_url] toosee vide &lt;réponse&gt; élément ; un autre exemple, cliquez sur [http://twimlets.com/message ? Message % 5B0 %5, D = Hello % 20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee un &lt;réponse&gt; élément contenant un &lt;prononcer&gt; élément.</span><span class="sxs-lookup"><span data-stu-id="5961b-209">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty &lt;Response&gt; element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee a &lt;Response&gt; element that contains a &lt;Say&gt; element.</span></span>
>
>

<span data-ttu-id="5961b-210">Au lieu d’utiliser les URL fournie par Twilio hello, vous pouvez créer votre propre site URL qui renvoie des réponses HTTP.</span><span class="sxs-lookup"><span data-stu-id="5961b-210">Instead of relying on hello Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="5961b-211">Vous pouvez créer le site de hello dans n’importe quel langage qui renvoie des réponses HTTP.</span><span class="sxs-lookup"><span data-stu-id="5961b-211">You can create hello site in any language that returns HTTP responses.</span></span> <span data-ttu-id="5961b-212">Cette rubrique suppose que vous allez héberger URL hello à partir d’un gestionnaire générique ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5961b-212">This topic assumes you'll be hosting hello URL from an ASP.NET generic handler.</span></span>

<span data-ttu-id="5961b-213">Hello suivant gestionnaire ASP.NET développe une réponse TwiML indiquant que **Hello World** sur l’appel de hello.</span><span class="sxs-lookup"><span data-stu-id="5961b-213">hello following ASP.NET Handler crafts a TwiML response that says **Hello World** on hello call.</span></span>

    using System.Text;
    using System.Web;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {
            public void ProcessRequest(HttpContext context)
            {
                const string twiMLResponse =
                    "<Response><Say>Hello World.</Say></Response>";
                
                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.ContentEncoding = Encoding.UTF8;
                context.Response.Write(twiMLResponse);
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }
    
<span data-ttu-id="5961b-214">Comme vous pouvez le voir à partir de l’exemple hello ci-dessus, hello TwiML réponse est simplement un document XML.</span><span class="sxs-lookup"><span data-stu-id="5961b-214">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="5961b-215">bibliothèque de Twilio.TwiML Hello contient des classes qui génèrent TwiML pour vous.</span><span class="sxs-lookup"><span data-stu-id="5961b-215">hello Twilio.TwiML library contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="5961b-216">Hello exemple ci-dessous génère réponse équivalent de hello comme indiqué ci-dessus, mais utilise hello **VoiceResponse** classe.</span><span class="sxs-lookup"><span data-stu-id="5961b-216">hello example below produces hello equivalent response as shown above, but uses hello **VoiceResponse** class.</span></span>

    using System.Web;
    using Twilio.TwiML;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {

            public void ProcessRequest(HttpContext context)
            {
                var twiml = new VoiceResponse();
                twiml.Say("Hello World.");

                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.Write(twiml.ToString());
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }

<span data-ttu-id="5961b-217">Pour plus d'informations sur TwiML, consultez la page [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="5961b-217">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span></span>

<span data-ttu-id="5961b-218">Une fois que vous avez configuré une réponse de TwiML tooprovide moyen, vous pouvez passer ce toohello URL **CallResource.Create** (méthode).</span><span class="sxs-lookup"><span data-stu-id="5961b-218">Once you have set up a way tooprovide TwiML responses, you can pass that URL toohello **CallResource.Create** method.</span></span> <span data-ttu-id="5961b-219">Par exemple, si vous disposez d’une application web nommée MyTwiML déployé tooan service cloud Azure, et hello le nom de votre gestionnaire d’ASP.NET est mytwiml.ashx, hello URL peut être transmise trop**CallResource.Create** comme indiqué dans hello suivant de code exemple :</span><span class="sxs-lookup"><span data-stu-id="5961b-219">For example, if you have a web application named MyTwiML deployed tooan Azure cloud service, and hello name of your ASP.NET Handler is mytwiml.ashx, hello URL can be passed too**CallResource.Create** as shown in hello following code sample:</span></span>

    // This sample uses hello sandbox number provided by Twilio toomake hello call.
    // Place hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

<span data-ttu-id="5961b-220">Pour plus d’informations sur l’utilisation de Twilio sur Azure avec ASP.NET, consultez [comment toomake un appel téléphonique dans un rôle web sur Azure à l’aide de Twilio][howto_phonecall_dotnet].</span><span class="sxs-lookup"><span data-stu-id="5961b-220">For additional information about using Twilio on Azure with ASP.NET, see [How toomake a phone call using Twilio in a web role on Azure][howto_phonecall_dotnet].</span></span>

[!INCLUDE [twilio-additional-services-and-next-steps](../includes/twilio-additional-services-and-next-steps.md)]

[howto_phonecall_dotnet]: partner-twilio-cloud-services-dotnet-phone-call-web-role.md

[twimlet_message_url]: http://twimlets.com/message

[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls

[vs_project]:http://msdn.microsoft.com/library/windowsazure/ee405487.aspx
[nuget]:http://nuget.org/
[twilio_github_repo]:https://github.com/twilio/twilio-csharp

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified
