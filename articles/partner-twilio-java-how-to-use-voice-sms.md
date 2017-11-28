---
title: aaaHow tooUse Twilio pour la voix et SMS (Java) | Documents Microsoft
description: "Découvrez comment toomake un appel téléphonique et envoyer un SMS de message avec le service de l’API de Twilio hello sur Azure. Exemples de code écrits en Java."
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: f3508965-5527-4255-9d51-5d5f926f4d43
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: a186e2c8e73ced928bd0dec348971034f10ba82c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-java"></a><span data-ttu-id="2610c-104">Comment tooUse Twilio pour la voix et les fonctionnalités de SMS dans Java</span><span class="sxs-lookup"><span data-stu-id="2610c-104">How tooUse Twilio for Voice and SMS Capabilities in Java</span></span>
<span data-ttu-id="2610c-105">Ce guide montre comment tooperform des tâches de programmation courantes avec hello Twilio API de service sur Azure.</span><span class="sxs-lookup"><span data-stu-id="2610c-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="2610c-106">scénarios de Hello couvertes incluent un appel téléphonique et envoi d’un message de Service SMS (Short Message).</span><span class="sxs-lookup"><span data-stu-id="2610c-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="2610c-107">Pour plus d’informations sur Twilio et à l’aide de la voix et SMS dans vos applications, consultez hello [étapes](#NextSteps) section.</span><span class="sxs-lookup"><span data-stu-id="2610c-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="2610c-108"><a id="WhatIs"></a>Présentation de Twilio</span><span class="sxs-lookup"><span data-stu-id="2610c-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="2610c-109">Twilio est une API de service web de téléphonie qui vous permet d’utiliser votre langages web existants et les voix toobuild de compétences et les applications de SMS.</span><span class="sxs-lookup"><span data-stu-id="2610c-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills toobuild voice and SMS applications.</span></span> <span data-ttu-id="2610c-110">Twilio est un service tiers, et non une fonctionnalité Azure ni un produit Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2610c-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="2610c-111">**Twilio vocal** permet à votre toomake d’applications et de recevoir des appels téléphoniques.</span><span class="sxs-lookup"><span data-stu-id="2610c-111">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="2610c-112">**Twilio SMS** permet à votre toomake d’applications et de recevoir des messages SMS.</span><span class="sxs-lookup"><span data-stu-id="2610c-112">**Twilio SMS** allows your applications toomake and receive SMS messages.</span></span> <span data-ttu-id="2610c-113">**Client twilio sur** tooenable la communication vocale via les connexions Internet, y compris les connexions mobiles permet à vos applications.</span><span class="sxs-lookup"><span data-stu-id="2610c-113">**Twilio Client** allows your applications tooenable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="2610c-114"><a id="Pricing"></a>Tarification de Twilio et offres spéciales</span><span class="sxs-lookup"><span data-stu-id="2610c-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="2610c-115">Des informations sur les prix de Twilio sont disponibles dans la page [Tarification de Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="2610c-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="2610c-116">Les clients Azure reçoivent une [offre spéciale][special_offer] : un crédit gratuit de 1 000 SMS ou de 1 000 minutes d’appel en entrée.</span><span class="sxs-lookup"><span data-stu-id="2610c-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="2610c-117">toosign pour cette offre ou obtenir plus d’informations, visitez [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="2610c-117">toosign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>

## <span data-ttu-id="2610c-118"><a id="Concepts"></a>Concepts</span><span class="sxs-lookup"><span data-stu-id="2610c-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="2610c-119">Hello Twilio API est une API RESTful qui fournit la voix et fonctionnalités SMS pour les applications.</span><span class="sxs-lookup"><span data-stu-id="2610c-119">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="2610c-120">Les bibliothèques clientes sont disponibles dans plusieurs langues : pour en obtenir la liste, consultez la page [Bibliothèques de l’API Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="2610c-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="2610c-121">Les principaux aspects du hello Twilio API sont Twilio verbes et Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="2610c-121">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="2610c-122"><a id="Verbs"></a>Verbes Twilio</span><span class="sxs-lookup"><span data-stu-id="2610c-122"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="2610c-123">Hello API se sert de Twilio verbes ; par exemple, hello  **&lt;prononcer&gt;**  verbe fait en sorte que Twilio tooaudibly remettre un message sur un appel.</span><span class="sxs-lookup"><span data-stu-id="2610c-123">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="2610c-124">Hello Voici une liste de verbes de Twilio.</span><span class="sxs-lookup"><span data-stu-id="2610c-124">hello following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="2610c-125">**&lt;Accès à distance&gt;**: se connecte phone de tooanother hello appelant.</span><span class="sxs-lookup"><span data-stu-id="2610c-125">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="2610c-126">**&lt;Collecter des&gt;**: collecte les chiffres entrés sur le clavier de téléphone hello.</span><span class="sxs-lookup"><span data-stu-id="2610c-126">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="2610c-127">**&lt;Hangup&gt;** : met fin à un appel.</span><span class="sxs-lookup"><span data-stu-id="2610c-127">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="2610c-128">**&lt;Play&gt;** : lit un fichier audio.</span><span class="sxs-lookup"><span data-stu-id="2610c-128">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="2610c-129">**&lt;File d’attente&gt;**: ajouter la file d’attente de tooa hello des appelants.</span><span class="sxs-lookup"><span data-stu-id="2610c-129">**&lt;Queue&gt;**: Add hello tooa queue of callers.</span></span>
* <span data-ttu-id="2610c-130">**&lt;Pause&gt;** : patiente silencieusement pendant un nombre déterminé de secondes.</span><span class="sxs-lookup"><span data-stu-id="2610c-130">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="2610c-131">**&lt;Enregistrement&gt;**: enregistre la voix de l’appelant hello et retourne une URL d’un fichier contenant un enregistrement de hello.</span><span class="sxs-lookup"><span data-stu-id="2610c-131">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="2610c-132">**&lt;Rediriger&gt;**: transfère le contrôle d’un appel ou un SMS toohello TwiML à une autre URL.</span><span class="sxs-lookup"><span data-stu-id="2610c-132">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="2610c-133">**&lt;Rejeter&gt;**: rejette un entrant appeler tooyour Twilio nombre sans vous de facturation.</span><span class="sxs-lookup"><span data-stu-id="2610c-133">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you.</span></span>
* <span data-ttu-id="2610c-134">**&lt;Par exemple&gt;**: toospeech texte convertit effectuée sur un appel.</span><span class="sxs-lookup"><span data-stu-id="2610c-134">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="2610c-135">**&lt;Sms&gt;** : envoie un SMS.</span><span class="sxs-lookup"><span data-stu-id="2610c-135">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="2610c-136"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="2610c-136"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="2610c-137">TwiML est un ensemble d’instructions basé sur XML en fonction de verbes Twilio hello qui informent Twilio de façon tooprocess un appel ou un SMS.</span><span class="sxs-lookup"><span data-stu-id="2610c-137">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="2610c-138">Par exemple, hello suivant TwiML permet de convertir le texte hello **Hello World !**</span><span class="sxs-lookup"><span data-stu-id="2610c-138">As an example, hello following TwiML would convert hello text **Hello World!**</span></span> <span data-ttu-id="2610c-139">toospeech.</span><span class="sxs-lookup"><span data-stu-id="2610c-139">toospeech.</span></span>

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="2610c-140">Lorsque votre application appelle hello Twilio API, un des paramètres d’API hello est hello URL qui renvoie la réponse de TwiML hello.</span><span class="sxs-lookup"><span data-stu-id="2610c-140">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="2610c-141">À des fins de développement, vous pouvez utiliser l’URL fournie par Twilio tooprovide hello TwiML les réponses employées par vos applications.</span><span class="sxs-lookup"><span data-stu-id="2610c-141">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="2610c-142">Vous pourriez également héberger vos réponses de TwiML URL tooproduce hello et une autre option consiste à toouse hello **TwiMLResponse** objet.</span><span class="sxs-lookup"><span data-stu-id="2610c-142">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="2610c-143">Pour plus d’informations sur les verbes Twilio, leurs attributs et le langage TwiML, consultez la page [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="2610c-143">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="2610c-144">Pour plus d’informations sur hello Twilio API, consultez [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="2610c-144">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="2610c-145"><a id="CreateAccount"></a>Créer un compte Twilio</span><span class="sxs-lookup"><span data-stu-id="2610c-145"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="2610c-146">Lorsque vous êtes prêt tooget un compte de Twilio, inscrivez-vous dans [essayez de Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="2610c-146">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="2610c-147">Vous pouvez commencer avec un compte gratuit, avant de le mettre à niveau ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="2610c-147">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="2610c-148">Lorsque vous créez un compte Twilio, vous recevez un ID de compte et un jeton d'authentification.</span><span class="sxs-lookup"><span data-stu-id="2610c-148">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="2610c-149">Les deux seront les appels d’API de Twilio toomake nécessaires.</span><span class="sxs-lookup"><span data-stu-id="2610c-149">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="2610c-150">tooprevent non autorisé à accéder à tooyour compte, de sécuriser votre jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="2610c-150">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="2610c-151">Votre ID de compte et l’authentification jeton peuvent être consultés à hello [Twilio Console][twilio_console], dans hello champs **SID de compte** et **dujetond’authentification**, respectivement.</span><span class="sxs-lookup"><span data-stu-id="2610c-151">Your account ID and authentication token are viewable at hello [Twilio Console][twilio_console], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="2610c-152"><a id="create_app"></a>Création d’une application Java</span><span class="sxs-lookup"><span data-stu-id="2610c-152"><a id="create_app"></a>Create a Java Application</span></span>
1. <span data-ttu-id="2610c-153">Obtenir hello Twilio JAR et l’ajouter tooyour chemin d’accès et votre assembly de déploiement WAR de build Java.</span><span class="sxs-lookup"><span data-stu-id="2610c-153">Obtain hello Twilio JAR and add it tooyour Java build path and your WAR deployment assembly.</span></span> <span data-ttu-id="2610c-154">À [https://github.com/twilio/twilio-java][twilio_java], vous pouvez télécharger hello GitHub sources et créer vos propres JAR ou télécharger le fichier JAR prédéfini (avec ou sans dépendances).</span><span class="sxs-lookup"><span data-stu-id="2610c-154">At [https://github.com/twilio/twilio-java][twilio_java], you can download hello GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
2. <span data-ttu-id="2610c-155">Assurez-vous de votre JDK **cacerts** keystore contient le certificat d’autorité de certification Equifax Secure hello avec 67:CB:9 d’empreinte digitale MD5 D : C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (numéro de série hello est 35:DE:F4:CF et hello SHA1 empreinte digitale est D2:32:09:AD:23:D3:14:23:21:74:E4:0 D : 7F:9 D : 62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="2610c-155">Ensure your JDK's **cacerts** keystore contains hello Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello serial number is 35:DE:F4:CF and hello SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="2610c-156">Il s’agit hello autorité de certification pour hello [https://api.twilio.com] [ twilio_api_service] service, qui est appelée lors de l’utilisation de Twilio APIs.</span><span class="sxs-lookup"><span data-stu-id="2610c-156">This is hello certificate authority (CA) certificate for hello [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="2610c-157">Pour plus d’informations sur la capacité de votre JDK **cacerts** keystore contient le certificat d’autorité de certification approprié hello, consultez [Ajout d’un magasin de certificats d’autorité de certification Java de toohello certificat][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="2610c-157">For information about ensuring your JDK's **cacerts** keystore contains hello correct CA certificate, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="2610c-158">Obtenir des instructions détaillées pour l’utilisation de la bibliothèque cliente de Twilio hello pour Java sont disponibles sur [comment tooMake un Twilio à l’aide d’un appel téléphonique dans une Application Java sur Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="2610c-158">Detailed instructions for using hello Twilio client library for Java are available at [How tooMake a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="2610c-159"><a id="configure_app"></a>Configurez des bibliothèques de votre Application tooUse Twilio</span><span class="sxs-lookup"><span data-stu-id="2610c-159"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="2610c-160">Dans votre code, vous pouvez ajouter **importer** instructions haut hello de vos fichiers sources pour hello Twilio packages ou des classes vous souhaitez toouse dans votre application.</span><span class="sxs-lookup"><span data-stu-id="2610c-160">Within your code, you can add **import** statements at hello top of your source files for hello Twilio packages or classes you want toouse in your application.</span></span>

<span data-ttu-id="2610c-161">Pour les fichiers sources Java :</span><span class="sxs-lookup"><span data-stu-id="2610c-161">For Java source files:</span></span>

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

<span data-ttu-id="2610c-162">Pour les fichiers sources JSP (Java Server Page) :</span><span class="sxs-lookup"><span data-stu-id="2610c-162">For Java Server Page (JSP) source files:</span></span>

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
<span data-ttu-id="2610c-163">Selon les packages de Twilio ou les classes, vous souhaitez toouse, votre **importer** instructions peuvent être différents.</span><span class="sxs-lookup"><span data-stu-id="2610c-163">Depending on which Twilio packages or classes you want toouse, your **import** statements may be different.</span></span>

## <span data-ttu-id="2610c-164"><a id="howto_make_call"></a>Procédure : passer un appel sortant</span><span class="sxs-lookup"><span data-stu-id="2610c-164"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="2610c-165">Hello suivant montre comment toomake sortante appeler à l’aide de hello **appeler** classe.</span><span class="sxs-lookup"><span data-stu-id="2610c-165">hello following shows how toomake an outgoing call using hello **Call** class.</span></span> <span data-ttu-id="2610c-166">Ce code utilise également un Bonjour de tooreturn site fournie par Twilio réponse de Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="2610c-166">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="2610c-167">Remplacez par vos valeurs hello **de** et **à** les numéros de téléphone et assurez-vous que vous vérifiez hello **à partir de** numéro de téléphone de votre code hello de Twilio compte toorunning préalable.</span><span class="sxs-lookup"><span data-stu-id="2610c-167">Substitute your values for hello **from** and **to** phone numbers, and ensure that you verify hello **from** phone number for your Twilio account prior toorunning hello code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    URI uri = new URI("http://twimlets.com/message" +
            "?Message%5B0%5D=Hello%20World%21");

    // Declare tooand From numbers
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="2610c-168">Pour plus d’informations sur les paramètres de hello passés dans toohello **Call.creator** méthode, consultez [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="2610c-168">For more information about hello parameters passed in toohello **Call.creator** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="2610c-169">Comme indiqué, ce code utilise un Bonjour de tooreturn TwiML réponse Twilio fournie par site.</span><span class="sxs-lookup"><span data-stu-id="2610c-169">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="2610c-170">Vous pouvez utiliser votre propre hello tooprovide de site TwiML réponse ; Pour plus d’informations, consultez [comment tooProvide réponses TwiML dans une Application Java sur Azure](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="2610c-170">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses in a Java Application on Azure](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="2610c-171"><a id="howto_send_sms"></a>Procédure : envoi d'un message SMS</span><span class="sxs-lookup"><span data-stu-id="2610c-171"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="2610c-172">Hello suivant montre comment un message SMS à l’aide de toosend hello **Message** classe.</span><span class="sxs-lookup"><span data-stu-id="2610c-172">hello following shows how toosend an SMS message using hello **Message** class.</span></span> <span data-ttu-id="2610c-173">Hello **de** nombre, **4155992671**, est fournie par Twilio pour évaluation comptes toosend de SMS.</span><span class="sxs-lookup"><span data-stu-id="2610c-173">hello **from** number, **4155992671**, is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="2610c-174">Hello **à** nombre doit être vérifié pour votre code de hello Twilio compte toorunning préalable.</span><span class="sxs-lookup"><span data-stu-id="2610c-174">hello **to** number must be verified for your Twilio account prior toorunning hello code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Declare tooand From numbers and hello Body of hello SMS message
    PhoneNumber too= new PhoneNumber("+14159352345"); // Replace with a valid phone number for your account.
    PhoneNumber from = new PhoneNumber("+14158141829"); // Replace with a valid phone number for your account.
    String body = "Where's Wallace?";

    // Create a Message creator passing From, tooand Body values
    // then send hello SMS message by calling hello create() method
    Message sms = Message.creator(to, from, body).create();
```

<span data-ttu-id="2610c-175">Pour plus d’informations sur les paramètres de hello passés dans toohello **Message.creator** méthode, consultez [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span><span class="sxs-lookup"><span data-stu-id="2610c-175">For more information about hello parameters passed in toohello **Message.creator** method, see [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span></span>

## <span data-ttu-id="2610c-176"><a id="howto_provide_twiml_responses"></a>Procédure : envoi de réponses TwiML depuis votre propre site web</span><span class="sxs-lookup"><span data-stu-id="2610c-176"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="2610c-177">Lorsque votre application démarre un toohello appel API de Twilio, par exemple via hello **CallCreator.create** méthode, Twilio enverra votre URL tooa demande tooreturn attendu une réponse TwiML.</span><span class="sxs-lookup"><span data-stu-id="2610c-177">When your application initiates a call toohello Twilio API, for example via hello **CallCreator.create** method, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="2610c-178">exemple Hello ci-dessus utilise les URL fournie par Twilio hello [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="2610c-178">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="2610c-179">(TwiML est conçu pour une utilisation par les services Web, vous pouvez afficher hello TwiML dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="2610c-179">(While TwiML is designed for use by Web services, you can view hello TwiML in your browser.</span></span> <span data-ttu-id="2610c-180">Par exemple, cliquez sur [http://twimlets.com/message] [ twimlet_message_url] toosee vide  **&lt;réponse&gt;**  élément ; un autre exemple, cliquez sur [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21] [ twimlet_message_url_hello_world] toosee un  **&lt;réponse&gt;**  élément contenant un  **&lt;prononcer &gt;**  élément.)</span><span class="sxs-lookup"><span data-stu-id="2610c-180">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty **&lt;Response&gt;** element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] toosee a **&lt;Response&gt;** element that contains a **&lt;Say&gt;** element.)</span></span>

<span data-ttu-id="2610c-181">Au lieu d’utiliser les URL fournie par Twilio hello, vous pouvez créer votre propre site URL qui renvoie des réponses HTTP.</span><span class="sxs-lookup"><span data-stu-id="2610c-181">Instead of relying on hello Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="2610c-182">Vous pouvez créer le site de hello dans n’importe quel langage qui retourne des réponses HTTP ; Cette rubrique suppose que vous allez héberger URL hello dans une page JSP.</span><span class="sxs-lookup"><span data-stu-id="2610c-182">You can create hello site in any language that returns HTTP responses; this topic assumes you'll be hosting hello URL in a JSP page.</span></span>

<span data-ttu-id="2610c-183">Hello suivant page JSP qui en résulte dans une réponse TwiML indiquant que **Hello World !**</span><span class="sxs-lookup"><span data-stu-id="2610c-183">hello following JSP page results in a TwiML response that says **Hello World!**</span></span> <span data-ttu-id="2610c-184">appel de hello.</span><span class="sxs-lookup"><span data-stu-id="2610c-184">on hello call.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="2610c-185">Bonjour suivant des résultats de la page JSP dans une réponse TwiML indiquant que du texte, a plusieurs pauses et affiche des informations sur la version de l’API de Twilio hello et le nom du rôle Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2610c-185">hello following JSP page results in a TwiML response that says some text, has several pauses, and says information about hello Twilio API version and hello Azure role name.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello from Azure!</Say>
        <Pause></Pause>
        <Say>hello Twilio API version is <%= request.getParameter("ApiVersion") %>.</Say>
        <Say>hello Azure role name is <%= System.getenv("RoleName") %>.</Say>
        <Pause></Pause>
        <Say>Good bye.</Say>
    </Response>
```

<span data-ttu-id="2610c-186">Hello **ApiVersion** paramètre n’est disponible dans les demandes de voix Twilio (pas de demandes SMS).</span><span class="sxs-lookup"><span data-stu-id="2610c-186">hello **ApiVersion** parameter is available in Twilio voice requests (not SMS requests).</span></span> <span data-ttu-id="2610c-187">paramètres de demande disponible toosee hello pour Twilio vocal et les demandes SMS, consultez <https://www.twilio.com/docs/api/twiml/twilio_request> et <https://www.twilio.com/docs/api/twiml/sms/twilio_request >, respectivement.</span><span class="sxs-lookup"><span data-stu-id="2610c-187">toosee hello available request parameters for Twilio voice and SMS requests, see <https://www.twilio.com/docs/api/twiml/twilio_request> and <https://www.twilio.com/docs/api/twiml/sms/twilio_request>, respectively.</span></span> <span data-ttu-id="2610c-188">Hello **RoleName** variable d’environnement n’est disponible dans le cadre d’un déploiement d’Azure.</span><span class="sxs-lookup"><span data-stu-id="2610c-188">hello **RoleName** environment variable is available as part of an Azure deployment.</span></span> <span data-ttu-id="2610c-189">(Si vous souhaitez que les variables d’environnement personnalisées tooadd afin qu’ils peut être récupérés à partir de **System.getenv**, consultez la section de variables d’environnement hello à [divers paramètres de Configuration de rôle] [misc_role_config_settings].)</span><span class="sxs-lookup"><span data-stu-id="2610c-189">(If you want tooadd custom environment variables so they could be picked up from **System.getenv**, see hello environment variables section at [Miscellaneous Role Configuration Settings][misc_role_config_settings].)</span></span>

<span data-ttu-id="2610c-190">Une fois que vous avez votre page JSP configurer tooprovide TwiML réponses, utilisez des URL de hello de page JSP hello comme hello URL passée hello **Call.creator** (méthode).</span><span class="sxs-lookup"><span data-stu-id="2610c-190">Once you have your JSP page set up tooprovide TwiML responses, use hello URL of hello JSP page as hello URL passed into hello **Call.creator** method.</span></span> <span data-ttu-id="2610c-191">Par exemple, si vous avez une application Web nommée MyTwiML déployé tooan Azure le service hébergé et nom hello de page JSP hello est mytwiml.jsp, hello URL peut être passé trop**Call.creator** comme indiqué dans les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="2610c-191">For example, if you have a Web application named MyTwiML deployed tooan Azure hosted service, and hello name of hello JSP page is mytwiml.jsp, hello URL can be passed too**Call.creator** as shown in hello following:</span></span>

```java
    // Declare tooand From numbers and hello URL of your JSP page
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="2610c-192">Une autre option pour répondre avec TwiML est via hello **VoiceResponse** (classe), qui est disponible dans hello **com.twilio.twiml** package.</span><span class="sxs-lookup"><span data-stu-id="2610c-192">Another option for responding with TwiML is via hello **VoiceResponse** class, which is available in hello **com.twilio.twiml** package.</span></span>

<span data-ttu-id="2610c-193">Pour plus d’informations sur l’utilisation de Twilio dans Azure avec Java, consultez [comment tooMake un Twilio à l’aide d’un appel téléphonique dans une Application Java sur Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="2610c-193">For additional information about using Twilio in Azure with Java, see [How tooMake a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="2610c-194"><a id="AdditionalServices"></a>Utilisation de services Twilio supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2610c-194"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="2610c-195">En outre toohello les exemples indiqués ici, que twilio propose des API basées sur le web qui vous pouvez utiliser des fonctionnalités Twilio tooleverage supplémentaires à partir de votre application Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="2610c-195">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="2610c-196">Pour plus d’informations, consultez hello [documentation de l’API de Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="2610c-196">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="2610c-197"><a id="NextSteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2610c-197"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="2610c-198">Maintenant que vous avez appris les notions de base de hello Hello Twilio service, suivez ces liens de toolearn plus :</span><span class="sxs-lookup"><span data-stu-id="2610c-198">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="2610c-199">[Conseils de sécurité Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="2610c-199">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="2610c-200">[Procédures et exemples de code Twilio][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="2610c-200">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="2610c-201">[Didacticiels de démarrage rapide Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="2610c-201">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="2610c-202">[Twilio sur GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="2610c-202">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="2610c-203">[Communiquer avec tooTwilio prise en charge][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="2610c-203">[Talk tooTwilio Support][twilio_support]</span></span>

[twilio_java]: https://github.com/twilio/twilio-java
[twilio_api_service]: https://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[howto_phonecall_java]: partner-twilio-java-phone-call-example.md
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World%21
[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls
[twilio_rest_sending_sms]: http://www.twilio.com/docs/api/rest/sending-sms
[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/docs
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
