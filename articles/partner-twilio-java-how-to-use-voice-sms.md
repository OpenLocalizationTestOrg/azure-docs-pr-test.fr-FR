---
title: "Utilisation de Twilio pour les fonctionnalités vocales et de SMS (Java) | Microsoft Docs"
description: "Découvrez comment passer un appel téléphonique et envoyer un message texte avec le service d'API Twilio sur Azure. Exemples de code écrits en Java."
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
ms.openlocfilehash: 5a1b2ffa160a31b639605242b651dc8d14e7a01b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-java"></a><span data-ttu-id="bcf3c-104">Utilisation de Twilio pour les fonctionnalités vocales et de SMS dans Java</span><span class="sxs-lookup"><span data-stu-id="bcf3c-104">How to Use Twilio for Voice and SMS Capabilities in Java</span></span>
<span data-ttu-id="bcf3c-105">Ce guide présente l'exécution de tâches de programmation courantes avec le service API Twilio sur Azure.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="bcf3c-106">Les scénarios abordés comprennent notamment les appels téléphoniques et l'envoi de SMS.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="bcf3c-107">Pour plus d'informations sur Twilio et sur l'utilisation des fonctionnalités vocales et de SMS de vos applications, consultez la section [Étapes suivantes](#NextSteps) .</span><span class="sxs-lookup"><span data-stu-id="bcf3c-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="bcf3c-108"><a id="WhatIs"></a>Présentation de Twilio</span><span class="sxs-lookup"><span data-stu-id="bcf3c-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="bcf3c-109">Twilio est une API de service Web de téléphonie vous permettant d'utiliser vos aptitudes et langages Web existants pour générer des applications vocales et de SMS.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills to build voice and SMS applications.</span></span> <span data-ttu-id="bcf3c-110">Twilio est un service tiers, et non une fonctionnalité Azure ni un produit Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="bcf3c-111">**Twilio Voice** permet à vos applications de passer et de recevoir des appels téléphoniques.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-111">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="bcf3c-112">**Twilio SMS** permet à vos applications de créer et de recevoir des SMS.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-112">**Twilio SMS** allows your applications to make and receive SMS messages.</span></span> <span data-ttu-id="bcf3c-113">**Twilio Client** permet à vos applications d'activer les communications vocales au moyen de connexions Internet existantes, y compris des connexions mobiles.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-113">**Twilio Client** allows your applications to enable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="bcf3c-114"><a id="Pricing"></a>Tarification de Twilio et offres spéciales</span><span class="sxs-lookup"><span data-stu-id="bcf3c-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="bcf3c-115">Des informations sur les prix de Twilio sont disponibles dans la page [Tarification de Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="bcf3c-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="bcf3c-116">Les clients Azure reçoivent une [offre spéciale][special_offer] : un crédit gratuit de 1 000 SMS ou de 1 000 minutes d’appel en entrée.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="bcf3c-117">Pour bénéficier de cette offre ou pour obtenir des informations supplémentaires, visitez la page [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="bcf3c-117">To sign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>

## <span data-ttu-id="bcf3c-118"><a id="Concepts"></a>Concepts</span><span class="sxs-lookup"><span data-stu-id="bcf3c-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="bcf3c-119">L'API Twilio est une API RESTful qui offre des fonctionnalités vocales et de SMS aux applications.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-119">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="bcf3c-120">Les bibliothèques clientes sont disponibles dans plusieurs langues : pour en obtenir la liste, consultez la page [Bibliothèques de l’API Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="bcf3c-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="bcf3c-121">Les éléments les plus importants de l'API Twilio sont les verbes Twilio et TwiML (Twilio Markup Language).</span><span class="sxs-lookup"><span data-stu-id="bcf3c-121">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="bcf3c-122"><a id="Verbs"></a>Verbes Twilio</span><span class="sxs-lookup"><span data-stu-id="bcf3c-122"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="bcf3c-123">L'API utilise les verbes Twilio ; par exemple, le verbe **&lt;Say&gt;** (Dire) indique à Twilio de transmettre un message de manière audible lors d'un appel.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-123">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="bcf3c-124">La liste suivante présente les verbes Twilio.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-124">The following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="bcf3c-125">**&lt;Dial&gt;** : connecte l'appelant à un autre téléphone.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-125">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="bcf3c-126">**&lt;Gather&gt;** : rassemble les chiffres numériques entrés sur le clavier du téléphone.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-126">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="bcf3c-127">**&lt;Hangup&gt;** : met fin à un appel.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-127">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="bcf3c-128">**&lt;Play&gt;** : lit un fichier audio.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-128">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="bcf3c-129">**&lt;Queue&gt;** : ajoute l’appelant à une file d’attente d’appelants.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-129">**&lt;Queue&gt;**: Add the to a queue of callers.</span></span>
* <span data-ttu-id="bcf3c-130">**&lt;Pause&gt;** : patiente silencieusement pendant un nombre déterminé de secondes.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-130">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="bcf3c-131">**&lt;Record&gt;** : enregistre la voix de l'appelant et renvoie une URL permettant d'accéder à un fichier contenant l'enregistrement.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-131">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="bcf3c-132">**&lt;Redirect&gt;** : transfère le contrôle d'un appel ou d'un SMS au TwiML à une autre URL.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-132">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="bcf3c-133">**&lt;Reject&gt;** : refuse un appel entrant sur votre numéro Twilio sans vous facturer.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-133">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you.</span></span>
* <span data-ttu-id="bcf3c-134">**&lt;Say&gt;** : convertit le texte d'un appel en parole.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-134">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="bcf3c-135">**&lt;Sms&gt;** : envoie un SMS.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-135">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="bcf3c-136"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="bcf3c-136"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="bcf3c-137">TwiML est un jeu d'instructions XML reposant sur les verbes Twilio qui informent Twilio sur la façon de traiter un appel ou un SMS.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-137">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="bcf3c-138">À titre d’exemple, le code TwiML suivant convertit le texte **Hello World**</span><span class="sxs-lookup"><span data-stu-id="bcf3c-138">As an example, the following TwiML would convert the text **Hello World!**</span></span> <span data-ttu-id="bcf3c-139">en parole.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-139">to speech.</span></span>

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="bcf3c-140">Lorsque votre application appelle l'API Twilio, l'un des paramètres de l'API est l'URL qui renvoie la réponse TwiML.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-140">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="bcf3c-141">À des fins de développement, vous pouvez utiliser les URL Twilio pour fournir les réponses TwiML utilisées par vos applications.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-141">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="bcf3c-142">Vous pouvez également héberger vos propres URL afin de produire les réponses TwiML, ou encore utiliser l'objet **TwiMLResponse** .</span><span class="sxs-lookup"><span data-stu-id="bcf3c-142">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="bcf3c-143">Pour plus d’informations sur les verbes Twilio, leurs attributs et le langage TwiML, consultez la page [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="bcf3c-143">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="bcf3c-144">Pour plus d’informations sur l’API Twilio, consultez la page [API Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="bcf3c-144">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="bcf3c-145"><a id="CreateAccount"></a>Créer un compte Twilio</span><span class="sxs-lookup"><span data-stu-id="bcf3c-145"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="bcf3c-146">Lorsque vous êtes prêt à créer votre compte Twilio, inscrivez-vous sur la page [Essayer Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="bcf3c-146">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="bcf3c-147">Vous pouvez commencer avec un compte gratuit, avant de le mettre à niveau ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-147">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="bcf3c-148">Lorsque vous créez un compte Twilio, vous recevez un ID de compte et un jeton d'authentification.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-148">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="bcf3c-149">Les deux sont nécessaires pour passer des appels d'API Twilio.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-149">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="bcf3c-150">Pour éviter qu'une personne non autorisée n'accède à votre compte, conservez votre jeton d'authentification en lieu sûr.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-150">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="bcf3c-151">Vous pouvez consulter vos ID de compte et jeton d’authentification dans la [console Twilio][twilio_console], dans les champs intitulés **ACCOUNT SID** et **AUTH TOKEN**, respectivement.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-151">Your account ID and authentication token are viewable at the [Twilio Console][twilio_console], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="bcf3c-152"><a id="create_app"></a>Création d’une application Java</span><span class="sxs-lookup"><span data-stu-id="bcf3c-152"><a id="create_app"></a>Create a Java Application</span></span>
1. <span data-ttu-id="bcf3c-153">Obtenez le JAR Twilio et ajoutez-le à votre chemin d'accès de build Java et à votre assembly de déploiement WAR.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-153">Obtain the Twilio JAR and add it to your Java build path and your WAR deployment assembly.</span></span> <span data-ttu-id="bcf3c-154">Sur [https://github.com/twilio/twilio-java][twilio_java], vous pouvez télécharger les sources GitHub et créer votre propre JAR, ou télécharger un JAR préconstruit (avec ou sans dépendances).</span><span class="sxs-lookup"><span data-stu-id="bcf3c-154">At [https://github.com/twilio/twilio-java][twilio_java], you can download the GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
2. <span data-ttu-id="bcf3c-155">Vérifiez que le keystore **cacerts** de votre JDK contient le certificat ESCA (Equifax Secure Certificate Authority) avec l'empreinte MD5 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (le numéro de série est 35:DE:F4:CF et l'empreinte de SHA1 est D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="bcf3c-155">Ensure your JDK's **cacerts** keystore contains the Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (the serial number is 35:DE:F4:CF and the SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="bcf3c-156">Il s’agit du certificat d’autorité de certification pour le service [https://api.twilio.com][twilio_api_service], qui est appelé lorsque vous utilisez les API Twilio.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-156">This is the certificate authority (CA) certificate for the [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="bcf3c-157">Pour plus d’informations sur la façon de s’assurer que le keystore **cacerts** de votre JDK contient le certificat d’autorité de certification correct, consultez la rubrique [Ajout d’un certificat au magasin de certificats d’autorité de certification Java][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="bcf3c-157">For information about ensuring your JDK's **cacerts** keystore contains the correct CA certificate, see [Adding a Certificate to the Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="bcf3c-158">Des instructions détaillées sur l’utilisation de la bibliothèque cliente Twilio pour Java sont disponibles dans la rubrique [Exécution d’un appel téléphonique au moyen de Twilio dans une application Java sur Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="bcf3c-158">Detailed instructions for using the Twilio client library for Java are available at [How to Make a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="bcf3c-159"><a id="configure_app"></a>Configurer l’application pour utiliser les bibliothèques Twilio</span><span class="sxs-lookup"><span data-stu-id="bcf3c-159"><a id="configure_app"></a>Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="bcf3c-160">Dans votre code, vous pouvez ajouter des instructions **import** en haut de vos fichiers sources pour les classes ou packages Twilio que vous voulez utiliser dans votre application.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-160">Within your code, you can add **import** statements at the top of your source files for the Twilio packages or classes you want to use in your application.</span></span>

<span data-ttu-id="bcf3c-161">Pour les fichiers sources Java :</span><span class="sxs-lookup"><span data-stu-id="bcf3c-161">For Java source files:</span></span>

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

<span data-ttu-id="bcf3c-162">Pour les fichiers sources JSP (Java Server Page) :</span><span class="sxs-lookup"><span data-stu-id="bcf3c-162">For Java Server Page (JSP) source files:</span></span>

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
<span data-ttu-id="bcf3c-163">Selon les packages ou classes Twilio que vous voulez utiliser, vos instructions **import** peuvent être différentes.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-163">Depending on which Twilio packages or classes you want to use, your **import** statements may be different.</span></span>

## <span data-ttu-id="bcf3c-164"><a id="howto_make_call"></a>Procédure : passer un appel sortant</span><span class="sxs-lookup"><span data-stu-id="bcf3c-164"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="bcf3c-165">Le code suivant montre comment passer un appel téléphonique à l’aide de la classe **Call**.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-165">The following shows how to make an outgoing call using the **Call** class.</span></span> <span data-ttu-id="bcf3c-166">Il utilise également un site Twilio afin de renvoyer la réponse TwiML (Twilio Markup Language).</span><span class="sxs-lookup"><span data-stu-id="bcf3c-166">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="bcf3c-167">Remplacez les numéros de téléphone **d’origine** et **de destination** par vos valeurs, puis vérifiez le numéro de téléphone **d’origine** de votre compte Twilio avant d’exécuter le code.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-167">Substitute your values for the **from** and **to** phone numbers, and ensure that you verify the **from** phone number for your Twilio account prior to running the code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize the Twilio client.
    Twilio.init(accountSID, authToken);

    // Use the Twilio-provided site for the TwiML response.
    URI uri = new URI("http://twimlets.com/message" +
            "?Message%5B0%5D=Hello%20World%21");

    // Declare To and From numbers
    PhoneNumber to = new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");

    // Create a Call creator passing From, To and URL values
    // then make the call by executing the create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="bcf3c-168">Pour plus d’informations sur les paramètres transmis dans la méthode **Call.creator**, consultez la page [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="bcf3c-168">For more information about the parameters passed in to the **Call.creator** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="bcf3c-169">Comme indiqué, ce code utilise un site Twilio afin de renvoyer la réponse TwiML, À la place, vous pouvez utiliser votre propre site pour fournir la réponse TwiML.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-169">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="bcf3c-170">À la place, vous pouvez utiliser votre propre site pour fournir la réponse TwiML ; pour plus d'informations, consultez la rubrique [Envoi de réponses TwiML dans une application Java sur Azure](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="bcf3c-170">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses in a Java Application on Azure](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="bcf3c-171"><a id="howto_send_sms"></a>Procédure : envoi d'un message SMS</span><span class="sxs-lookup"><span data-stu-id="bcf3c-171"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="bcf3c-172">La procédure suivante montre comment envoyer un SMS à l’aide de la classe **Message**.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-172">The following shows how to send an SMS message using the **Message** class.</span></span> <span data-ttu-id="bcf3c-173">Le numéro **d’origine**, **4155992671**, est fourni par Twilio pour permettre aux comptes d’évaluation d’envoyer des SMS.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-173">The **from** number, **4155992671**, is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="bcf3c-174">Le numéro **de destination** doit être vérifié pour votre compte Twilio avant d’exécuter le code.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-174">The **to** number must be verified for your Twilio account prior to running the code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize the Twilio client.
    Twilio.init(accountSID, authToken);

    // Declare To and From numbers and the Body of the SMS message
    PhoneNumber to = new PhoneNumber("+14159352345"); // Replace with a valid phone number for your account.
    PhoneNumber from = new PhoneNumber("+14158141829"); // Replace with a valid phone number for your account.
    String body = "Where's Wallace?";

    // Create a Message creator passing From, To and Body values
    // then send the SMS message by calling the create() method
    Message sms = Message.creator(to, from, body).create();
```

<span data-ttu-id="bcf3c-175">Pour plus d’informations sur les paramètres transmis dans la méthode **Message.creator**, consultez la page [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span><span class="sxs-lookup"><span data-stu-id="bcf3c-175">For more information about the parameters passed in to the **Message.creator** method, see [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span></span>

## <span data-ttu-id="bcf3c-176"><a id="howto_provide_twiml_responses"></a>Procédure : envoi de réponses TwiML depuis votre propre site web</span><span class="sxs-lookup"><span data-stu-id="bcf3c-176"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="bcf3c-177">Quand votre application démarre un appel vers l’API Twilio, par exemple via la méthode **CallCreator.create**, Twilio envoie votre demande à une URL qui est censée renvoyer une réponse TwiML.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-177">When your application initiates a call to the Twilio API, for example via the **CallCreator.create** method, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="bcf3c-178">L’exemple ci-dessus utilise l’URL fournie par Twilio [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="bcf3c-178">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="bcf3c-179">TwiML est conçu pour être utilisé par des services Web, vous pouvez donc afficher TwiML dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-179">(While TwiML is designed for use by Web services, you can view the TwiML in your browser.</span></span> <span data-ttu-id="bcf3c-180">Par exemple, cliquez sur [http://twimlets.com/message][twimlet_message_url] pour afficher un élément **&lt;Response&gt;** vide ; autre exemple, cliquez sur [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] pour afficher un élément **&lt;Response&gt;** contenant un élément **&lt;Say&gt;**.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-180">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty **&lt;Response&gt;** element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] to see a **&lt;Response&gt;** element that contains a **&lt;Say&gt;** element.)</span></span>

<span data-ttu-id="bcf3c-181">Au lieu de compter sur l'URL Twilio, vous pouvez créer votre propre site d'URL qui renvoie des réponses HTTP.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-181">Instead of relying on the Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="bcf3c-182">Vous pouvez créer le site dans n'importe quelle langage renvoyant des réponses HTTP ; cette rubrique suppose que vous hébergerez l'URL sur une page JSP.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-182">You can create the site in any language that returns HTTP responses; this topic assumes you'll be hosting the URL in a JSP page.</span></span>

<span data-ttu-id="bcf3c-183">La page JSP suivante génère une réponse TwiML prononçant **Hello World**</span><span class="sxs-lookup"><span data-stu-id="bcf3c-183">The following JSP page results in a TwiML response that says **Hello World!**</span></span> <span data-ttu-id="bcf3c-184">lors de l’appel.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-184">on the call.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="bcf3c-185">La page JSP suivante génère une réponse TwiML qui prononce un texte spécifique, contient plusieurs pauses et fournit des informations sur la version d'API Twilio et le nom de rôle Azure.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-185">The following JSP page results in a TwiML response that says some text, has several pauses, and says information about the Twilio API version and the Azure role name.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello from Azure!</Say>
        <Pause></Pause>
        <Say>The Twilio API version is <%= request.getParameter("ApiVersion") %>.</Say>
        <Say>The Azure role name is <%= System.getenv("RoleName") %>.</Say>
        <Pause></Pause>
        <Say>Good bye.</Say>
    </Response>
```

<span data-ttu-id="bcf3c-186">Le paramètre **ApiVersion** est disponible dans les demandes vocales Twilio (pas pour les demandes par SMS).</span><span class="sxs-lookup"><span data-stu-id="bcf3c-186">The **ApiVersion** parameter is available in Twilio voice requests (not SMS requests).</span></span> <span data-ttu-id="bcf3c-187">Pour afficher les paramètres de demande disponibles pour les demandes vocales et SMS de Twilio, consultez respectivement les pages <https://www.twilio.com/docs/api/twiml/twilio_request> et <https://www.twilio.com/docs/api/twiml/sms/twilio_request>.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-187">To see the available request parameters for Twilio voice and SMS requests, see <https://www.twilio.com/docs/api/twiml/twilio_request> and <https://www.twilio.com/docs/api/twiml/sms/twilio_request>, respectively.</span></span> <span data-ttu-id="bcf3c-188">La variable d'environnement **RoleName** est disponible au sein du déploiement Azure.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-188">The **RoleName** environment variable is available as part of an Azure deployment.</span></span> <span data-ttu-id="bcf3c-189">Si vous voulez ajouter des variables d’environnement personnalisées de façon à ce qu’elles puissent être sélectionnées à partir de **System.getenv**, consultez la section des variables d’environnement dans la page [Paramètres de configuration de rôle divers][misc_role_config_settings].</span><span class="sxs-lookup"><span data-stu-id="bcf3c-189">(If you want to add custom environment variables so they could be picked up from **System.getenv**, see the environment variables section at [Miscellaneous Role Configuration Settings][misc_role_config_settings].)</span></span>

<span data-ttu-id="bcf3c-190">Une fois que votre page JSP est configurée et prête à envoyer des réponses TwiML, utilisez son URL en tant qu’URL transmise à la méthode **Call.creator**.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-190">Once you have your JSP page set up to provide TwiML responses, use the URL of the JSP page as the URL passed into the **Call.creator** method.</span></span> <span data-ttu-id="bcf3c-191">Par exemple, si une application web intitulée MyTwiML est déployée sur un service hébergé Azure, et que le nom de la page JSP est mytwiml.jsp, l’URL peut être transmise à **Call.creator**, comme indiqué ci-après :</span><span class="sxs-lookup"><span data-stu-id="bcf3c-191">For example, if you have a Web application named MyTwiML deployed to an Azure hosted service, and the name of the JSP page is mytwiml.jsp, the URL can be passed to **Call.creator** as shown in the following:</span></span>

```java
    // Declare To and From numbers and the URL of your JSP page
    PhoneNumber to = new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, To and URL values
    // then make the call by executing the create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="bcf3c-192">Une autre possibilité de réponse avec TwiML consiste à utiliser la classe **VoiceResponse**, qui est disponible dans le package **com.twilio.twiml**.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-192">Another option for responding with TwiML is via the **VoiceResponse** class, which is available in the **com.twilio.twiml** package.</span></span>

<span data-ttu-id="bcf3c-193">Pour plus d’informations sur l’utilisation de Twilio dans Azure avec Java, consultez la page [Exécution d’un appel téléphonique à l’aide de Twilio dans une application Java sur Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="bcf3c-193">For additional information about using Twilio in Azure with Java, see [How to Make a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="bcf3c-194"><a id="AdditionalServices"></a>Utilisation de services Twilio supplémentaires</span><span class="sxs-lookup"><span data-stu-id="bcf3c-194"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="bcf3c-195">En plus des exemples présentés ici, Twilio offre des API Web que vous pouvez utiliser pour tirer profit d'autres fonctionnalités de Twilio à partir de votre application Azure.</span><span class="sxs-lookup"><span data-stu-id="bcf3c-195">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="bcf3c-196">Pour plus d’informations, consultez la [documentation de l’API Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="bcf3c-196">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="bcf3c-197"><a id="NextSteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bcf3c-197"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="bcf3c-198">Maintenant que vous avez appris les bases du service Twilio, consultez ces liens pour en savoir plus :</span><span class="sxs-lookup"><span data-stu-id="bcf3c-198">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="bcf3c-199">[Conseils de sécurité Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="bcf3c-199">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="bcf3c-200">[Procédures et exemples de code Twilio][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="bcf3c-200">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="bcf3c-201">[Didacticiels de démarrage rapide Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="bcf3c-201">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="bcf3c-202">[Twilio sur GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="bcf3c-202">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="bcf3c-203">[Support Twilio][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="bcf3c-203">[Talk to Twilio Support][twilio_support]</span></span>

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
