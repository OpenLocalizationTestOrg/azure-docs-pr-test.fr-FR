---
title: "Utilisation de Twilio pour les fonctionnalités vocales, VoIP et de messagerie SMS dans Azure"
description: "Découvrez comment passer un appel téléphonique et envoyer un message texte avec le service d'API Twilio sur Azure. Exemples de code écrits en Node.js."
services: 
documentationcenter: nodejs
author: devinrader
manager: wpickett
editor: 
ms.assetid: f558cbbd-13d2-416f-b9b1-33a99c426af9
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 11/25/2014
ms.author: wpickett
ms.openlocfilehash: 44ec97812130d41d75be98fc8e2d846b7cb5c913
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a><span data-ttu-id="b6d68-104">Utilisation de Twilio pour les fonctionnalités vocales, VoIP et de messagerie SMS dans Azure</span><span class="sxs-lookup"><span data-stu-id="b6d68-104">Using Twilio for Voice, VoIP, and SMS Messaging in Azure</span></span>
<span data-ttu-id="b6d68-105">Ce guide montre comment générer des applications qui communiquent avec Twilio et node.js sur Azure.</span><span class="sxs-lookup"><span data-stu-id="b6d68-105">This guide demonstrates how to build apps that communicate with Twilio and node.js on Azure.</span></span>

<a id="whatis"/>

## <a name="what-is-twilio"></a><span data-ttu-id="b6d68-106">Présentation de Twilio</span><span class="sxs-lookup"><span data-stu-id="b6d68-106">What is Twilio?</span></span>
<span data-ttu-id="b6d68-107">Twilio est une plateforme API qui facilite pour les développeurs le passage et la réception d'appels téléphoniques, l'envoi et la réception de SMS. Elle incorpore l'appel VoIP dans des applications basées sur un navigateur et mobiles natives.</span><span class="sxs-lookup"><span data-stu-id="b6d68-107">Twilio is an API platform that makes it easy for developers to make and receive phone calls, send and receive text messages, and embed VoIP calling into browser-based and native mobile applications.</span></span> <span data-ttu-id="b6d68-108">Survolons rapidement le fonctionnement de Twilio avant de l'étudier plus en détail.</span><span class="sxs-lookup"><span data-stu-id="b6d68-108">Let's briefly go over how this works before diving in.</span></span>

### <a name="receiving-calls-and-text-messages"></a><span data-ttu-id="b6d68-109">Réception d'appels et de SMS</span><span class="sxs-lookup"><span data-stu-id="b6d68-109">Receiving Calls and Text Messages</span></span>
<span data-ttu-id="b6d68-110">Twilio permet aux développeurs [d’acheter des numéros de téléphone programmables][purchase_phone] qui peuvent être utilisés à la fois pour envoyer et recevoir des appels et des SMS.</span><span class="sxs-lookup"><span data-stu-id="b6d68-110">Twilio allows developers to [purchase programmable phone numbers][purchase_phone] which can be used to both send and receive calls and text messages.</span></span> <span data-ttu-id="b6d68-111">Lorsqu'un numéro Twilio reçoit un appel ou un SMS, il envoie à votre application web une requête HTTP POST ou GET, vous demandant des instructions sur la gestion de l'appel ou du SMS.</span><span class="sxs-lookup"><span data-stu-id="b6d68-111">When a Twilio number receives an inbound call or text, Twilio will send your web application an HTTP POST or GET request, asking you for instructions on how to handle the call or text.</span></span> <span data-ttu-id="b6d68-112">Votre serveur répond à la requête HTTP de Twilio avec [TwiML][twiml], jeu simple de balises XML qui contient des instructions sur la gestion d’un appel ou d’un SMS.</span><span class="sxs-lookup"><span data-stu-id="b6d68-112">Your server will respond to Twilio's HTTP request with [TwiML][twiml], a simple set of XML tags that contain instructions on how to handle a call or text.</span></span> <span data-ttu-id="b6d68-113">Nous vous présenterons des exemples de TwiML un peu plus loin.</span><span class="sxs-lookup"><span data-stu-id="b6d68-113">We will see examples of TwiML in just a moment.</span></span>

### <a name="making-calls-and-sending-text-messages"></a><span data-ttu-id="b6d68-114">Passage d'appels et envoi de SMS</span><span class="sxs-lookup"><span data-stu-id="b6d68-114">Making Calls and Sending Text Messages</span></span>
<span data-ttu-id="b6d68-115">En émettant des requêtes HTTP vers l'API de service Web Twilio, les développeurs peuvent envoyer des SMS et passer des appels téléphoniques.</span><span class="sxs-lookup"><span data-stu-id="b6d68-115">By making HTTP requests to the Twilio web service API, developers can send text messages or initiate outbound phone calls.</span></span> <span data-ttu-id="b6d68-116">Pour les appels, le développeur doit également spécifier une URL qui renvoie des instructions TwiML relatives à la gestion de l'appel une fois qu'il est connecté.</span><span class="sxs-lookup"><span data-stu-id="b6d68-116">For outbound calls, the developer must also specify a URL that returns TwiML instructions for how to handle the outbound call once it is connected.</span></span>

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a><span data-ttu-id="b6d68-117">Incorporation des fonctionnalités VoIP dans un code de l'interface utilisateur (JavaScript, iOS ou Android)</span><span class="sxs-lookup"><span data-stu-id="b6d68-117">Embedding VoIP Capabilities in UI code (JavaScript, iOS, or Android)</span></span>
<span data-ttu-id="b6d68-118">Twilio offre un kit SDK côté client qui peut transformer n'importe quel navigateur web, application iOS ou Android en un téléphone VoIP.</span><span class="sxs-lookup"><span data-stu-id="b6d68-118">Twilio provides a client-side SDK which can turn any desktop web browser, iOS app, or Android app into a VoIP phone.</span></span> <span data-ttu-id="b6d68-119">Dans cet article, nous nous concentrerons sur l'utilisation de l'appel VoIP dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="b6d68-119">In this article, we will focus on how to use VoIP calling in the browser.</span></span> <span data-ttu-id="b6d68-120">En plus du kit *SDK JavaScript Twilio* s’exécutant dans le navigateur, vous devez utiliser une application côté serveur (notre application node.js) pour émettre un « jeton de fonctionnalité » pour le client JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b6d68-120">In addition to the *Twilio JavaScript SDK* running in the browser, a server-side application (our node.js application) must be used to issue a "capability token" to the JavaScript client.</span></span> <span data-ttu-id="b6d68-121">Vous trouverez plus d’informations sur l’utilisation de VoIP avec node.js [sur le blog des développeurs Twilio][voipnode].</span><span class="sxs-lookup"><span data-stu-id="b6d68-121">You can read more about using VoIP with node.js [on the Twilio dev blog][voipnode].</span></span>

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a><span data-ttu-id="b6d68-122">Inscription à Twilio (remise Microsoft)</span><span class="sxs-lookup"><span data-stu-id="b6d68-122">Sign Up For Twilio (Microsoft Discount)</span></span>
<span data-ttu-id="b6d68-123">Avant d’utiliser les services Twilio, vous devez [vous inscrire pour obtenir un compte][signup].</span><span class="sxs-lookup"><span data-stu-id="b6d68-123">Before using Twilio services, you must first [sign up for an account][signup].</span></span> <span data-ttu-id="b6d68-124">Les clients Microsoft Azure reçoivent une remise spéciale. Pour y avoir droit, [veillez à vous inscrire ici][signup] !</span><span class="sxs-lookup"><span data-stu-id="b6d68-124">Microsoft Azure customers receive a special discount - [be sure to sign up here][signup]!</span></span>

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a><span data-ttu-id="b6d68-125">Création et déploiement d'un site web Azure node.js</span><span class="sxs-lookup"><span data-stu-id="b6d68-125">Create and Deploy a node.js Azure Website</span></span>
<span data-ttu-id="b6d68-126">Ensuite, vous allez devoir créer un site web node.js s'exécutant sur Azure.</span><span class="sxs-lookup"><span data-stu-id="b6d68-126">Next, you will need to create a node.js website running on Azure.</span></span> <span data-ttu-id="b6d68-127">[La documentation officielle relative à cette création est située ici][azure_new_site].</span><span class="sxs-lookup"><span data-stu-id="b6d68-127">[The official documentation for doing this is located here][azure_new_site].</span></span> <span data-ttu-id="b6d68-128">À un niveau supérieur, vous réaliserez les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="b6d68-128">At a high level, you will be doing the following:</span></span>

* <span data-ttu-id="b6d68-129">Création d'un compte Azure si vous n'en possédez pas déjà un</span><span class="sxs-lookup"><span data-stu-id="b6d68-129">Signing up for an Azure account, if you don't have one already</span></span>
* <span data-ttu-id="b6d68-130">Utilisation de la console d'administration pour créer un site web</span><span class="sxs-lookup"><span data-stu-id="b6d68-130">Using the Azure admin console to create a new website</span></span>
* <span data-ttu-id="b6d68-131">Ajout d'une prise en charge du contrôle de code source (nous présumons que vous avez utilisé git)</span><span class="sxs-lookup"><span data-stu-id="b6d68-131">Adding source control support (we will assume you used git)</span></span>
* <span data-ttu-id="b6d68-132">Création d’un fichier `server.js` avec une application web node.js simple</span><span class="sxs-lookup"><span data-stu-id="b6d68-132">Creating a file `server.js` with a simple node.js web application</span></span>
* <span data-ttu-id="b6d68-133">Déploiement de cette application simple sur Azure</span><span class="sxs-lookup"><span data-stu-id="b6d68-133">Deploying this simple application to Azure</span></span>

<a id="twiliomodule"/>

## <a name="configure-the-twilio-module"></a><span data-ttu-id="b6d68-134">Configuration du module Twilio</span><span class="sxs-lookup"><span data-stu-id="b6d68-134">Configure the Twilio Module</span></span>
<span data-ttu-id="b6d68-135">Ensuite, nous commencerons à rédiger une simple application node.js qui utilise l'API Twilio.</span><span class="sxs-lookup"><span data-stu-id="b6d68-135">Next, we will begin to write a simple node.js application which makes use of the Twilio API.</span></span> <span data-ttu-id="b6d68-136">Avant de commencer, nous devons configurer les informations d'identification de notre compte Twilio.</span><span class="sxs-lookup"><span data-stu-id="b6d68-136">Before we begin, we need to configure our Twilio account credentials.</span></span>

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a><span data-ttu-id="b6d68-137">Configuration des informations d'identification Twilio dans des variables d'environnement système</span><span class="sxs-lookup"><span data-stu-id="b6d68-137">Configuring Twilio Credentials in System Environment Variables</span></span>
<span data-ttu-id="b6d68-138">Afin d'émettre des requêtes authentifiées au serveur principal Twilio, nous avons besoin de notre SID de compte et de notre jeton d'authentification, qui fonctionnent en tant que nom d'utilisateur et mot de passe pour notre compte Twilio.</span><span class="sxs-lookup"><span data-stu-id="b6d68-138">In order to make authenticated requests against the Twilio back end, we need our account SID and auth token, which function as the username and password set for our Twilio account.</span></span> <span data-ttu-id="b6d68-139">Le moyen le plus sécurisé de configurer ces deux éléments pour une utilisation avec le module Node dans Azure est d'utiliser les variables d'environnement système, que vous pouvez définir directement dans la console d'administration d'Azure.</span><span class="sxs-lookup"><span data-stu-id="b6d68-139">The most secure way to configure these for use with the node module in Azure is via system environment variables, which you can set directly in the Azure admin console.</span></span>

<span data-ttu-id="b6d68-140">Sélectionnez votre site web node.js et cliquez sur le lien « CONFIGURER ».</span><span class="sxs-lookup"><span data-stu-id="b6d68-140">Select your node.js website, and click the "CONFIGURE" link.</span></span>  <span data-ttu-id="b6d68-141">Si vous faites un peu défiler vers le bas, vous verrez une zone dans laquelle vous pouvez définir les propriétés de configuration de votre application.</span><span class="sxs-lookup"><span data-stu-id="b6d68-141">If you scroll down a bit, you will see an area where you can set configuration properties for your application.</span></span>  <span data-ttu-id="b6d68-142">Entrez les informations d’identification de votre compte Twilio ([disponibles dans la console Twilio][twilio_console]) comme illustré : assurez-vous de les nommer `TWILIO_ACCOUNT_SID` et `TWILIO_AUTH_TOKEN`, respectivement :</span><span class="sxs-lookup"><span data-stu-id="b6d68-142">Enter your Twilio account credentials ([found on your Twilio Console][twilio_console]) as shown - make sure to name them `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN`, respectively:</span></span>

![Console d'administration Azure][azure-admin-console]

<span data-ttu-id="b6d68-144">Une fois que vous avez configuré ces variables, redémarrez votre application dans la console Azure.</span><span class="sxs-lookup"><span data-stu-id="b6d68-144">Once you have configured these variables, restart your application in the Azure console.</span></span>

### <a name="declaring-the-twilio-module-in-packagejson"></a><span data-ttu-id="b6d68-145">Déclaration du module Twilio dans package.json</span><span class="sxs-lookup"><span data-stu-id="b6d68-145">Declaring the Twilio module in package.json</span></span>
<span data-ttu-id="b6d68-146">Ensuite, nous devons créer un fichier package.json pour gérer nos dépendances de module Node via [npm].</span><span class="sxs-lookup"><span data-stu-id="b6d68-146">Next, we need to create a package.json to manage our node module dependencies via [npm].</span></span> <span data-ttu-id="b6d68-147">Au même niveau que le fichier `server.js` que vous avez créé dans le didacticiel *Azure/node.js*, créez un fichier nommé `package.json`.</span><span class="sxs-lookup"><span data-stu-id="b6d68-147">At the same level as the `server.js` file you created in the *Azure/node.js* tutorial, create a file named `package.json`.</span></span>  <span data-ttu-id="b6d68-148">Placez-y les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b6d68-148">Inside this file, place the following:</span></span>

```json
{
  "name": "application-name",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node server"
  },
  "dependencies": {
    "body-parser": "^1.16.1",
    "ejs": "^2.5.5",
    "errorhandler": "^1.5.0",
    "express": "^4.14.1",
    "morgan": "^1.8.1",
    "twilio": "^2.11.1"
  }
}
```

<span data-ttu-id="b6d68-149">Cette instruction déclare le module Twilio en tant que dépendance ainsi que la [structure web Express][express] courante et le moteur de modèles EJS.</span><span class="sxs-lookup"><span data-stu-id="b6d68-149">This declares the twilio module as a dependency, as well as the popular [Express web framework][express] and the EJS template engine.</span></span>  <span data-ttu-id="b6d68-150">Tout est maintenant prêt et nous pouvons passer à l'écriture du code.</span><span class="sxs-lookup"><span data-stu-id="b6d68-150">Okay, now we're all set - let's write some code!</span></span>

<a id="makecall"/>

## <a name="make-an-outbound-call"></a><span data-ttu-id="b6d68-151">Exécution d'un appel téléphonique</span><span class="sxs-lookup"><span data-stu-id="b6d68-151">Make an Outbound Call</span></span>
<span data-ttu-id="b6d68-152">Créons un simple formulaire qui passera un appel vers un numéro que nous choisissons.</span><span class="sxs-lookup"><span data-stu-id="b6d68-152">Let's create a simple form that will place a call to a number we choose.</span></span> <span data-ttu-id="b6d68-153">Ouvrez `server.js` et saisissez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="b6d68-153">Open up `server.js`, and enter the following code.</span></span> <span data-ttu-id="b6d68-154">Lorsque le code indique "CHANGE_ME", placez le nom de votre site web Azure à cet endroit :</span><span class="sxs-lookup"><span data-stu-id="b6d68-154">Note where it says "CHANGE_ME" - put the name of your azure website there:</span></span>

```javascript
// Module dependencies
const express = require('express');
const path = require('path');
const http = require('http');
const twilio = require('twilio');
const logger = require('morgan');
const bodyParser = require('body-parser');
const errorHandler = require('errorhandler');
const accountSid = process.env.TWILIO_ACCOUNT_SID;
const authToken = process.env.TWILIO_AUTH_TOKEN;
// Create Express web application
const app = express();

// Express configuration
app.set('port', process.env.PORT || 3000);
app.set('views', __dirname + '/views');
app.set('view engine', 'ejs');
app.use(logger('tiny'));
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())
app.use(express.static(path.join(__dirname, 'public')));

if (app.get('env') !== 'production') {
  app.use(errorHandler());
}

// Render an HTML user interface for the application's home page
app.get('/', (request, response) => response.render('index'));

// Handle the form POST to place a call
app.post('/call', (request, response) => {
  var client = twilio(accountSid, authToken);

  client.makeCall({
    // make a call to this number
    to:request.body.number,

    // Change to a Twilio number you bought - see:
    // https://www.twilio.com/console/phone-numbers/incoming
    from:'+15558675309',

    // A URL in our app which generates TwiML
    // Change "CHANGE_ME" to your app's name
    url:'https://CHANGE_ME.azurewebsites.net/outbound_call'
  }, () => {
      // Go back to the home page
      response.redirect('/');
  });
});

// Generate TwiML to handle an outbound call
app.post('/outbound_call', (request, response) => {
  var twiml = new twilio.TwimlResponse();

  // Say a message to the call's receiver
  twiml.say('hello - thanks for checking out Twilio and Azure', {
      voice:'woman'
  });

  response.set('Content-Type', 'text/xml');
  response.send(twiml.toString());
});

// Start server
app.listen(app.get('port'), function(){
  console.log(`Express server listening on port ${app.get('port')}`);
});
```

<span data-ttu-id="b6d68-155">Ensuite, créez un répertoire appelé `views` et créez-y un fichier nommé `index.ejs` avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="b6d68-155">Next, create a directory called `views` - inside this directory, create a file named `index.ejs` with the following contents:</span></span>

```html
<!DOCTYPE html>
<html>
<head>
  <title>Twilio Test</title>
  <style>
    input { height:20px; width:300px; font-size:18px; margin:5px; padding:5px; }
  </style>
</head>
<body>
  <h1>Twilio Test</h1>
  <form action="/call" method="POST">
      <input placeholder="Enter a phone number" name="number"/>
      <br/>
      <input type="submit" value="Call the number above"/>
  </form>
</body>
</html>
```

<span data-ttu-id="b6d68-156">Maintenant, déployez votre site web sur Azure et ouvrez votre page d'accueil.</span><span class="sxs-lookup"><span data-stu-id="b6d68-156">Now, deploy your website to Azure and open your home.</span></span> <span data-ttu-id="b6d68-157">Vous devez être en mesure de saisir votre numéro de téléphone dans le champ de texte et de recevoir un appel depuis votre numéro Twilio !</span><span class="sxs-lookup"><span data-stu-id="b6d68-157">You should be able to enter your phone number in the text field, and receive a call from your Twilio number!</span></span>

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a><span data-ttu-id="b6d68-158">Envoi d'un SMS</span><span class="sxs-lookup"><span data-stu-id="b6d68-158">Send an SMS Message</span></span>
<span data-ttu-id="b6d68-159">À présent, configurons une interface utilisateur et une logique de gestion pour envoyer un SMS.</span><span class="sxs-lookup"><span data-stu-id="b6d68-159">Now, let's set up a user interface and form handling logic to send a text message.</span></span> <span data-ttu-id="b6d68-160">Ouvrez `server.js` et ajoutez le code suivant après le dernier appel à `app.post` :</span><span class="sxs-lookup"><span data-stu-id="b6d68-160">Open up `server.js`, and add the following code after the last call to `app.post`:</span></span>

```javascript
app.post('/sms', (request, response) => {
  const client = twilio(accountSid, authToken);

  client.sendSms({
      // send a text to this number
      to:request.body.number,

      // A Twilio number you bought - see:
      // https://www.twilio.com/console/phone-numbers/incoming
      from:'+15558675309',

      // The body of the text message
      body: request.body.message

  }, () => {
      // Go back to the home page
      response.redirect('/');
  });
});
```

<span data-ttu-id="b6d68-161">Dans `views/index.ejs`, ajoutez un autre formulaire sous le premier afin de soumettre un numéro et un SMS :</span><span class="sxs-lookup"><span data-stu-id="b6d68-161">In `views/index.ejs`, add another form under the first one to submit a number and a text message:</span></span>

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message to send" name="message"/>
  <br/>
  <input type="submit" value="Send text to the number above"/>
</form>
```

<span data-ttu-id="b6d68-162">Redéployez votre application sur Azure. Vous devriez désormais être en mesure d’envoyer ce formulaire et de vous envoyer (ou d’envoyer à un ami proche) un SMS !</span><span class="sxs-lookup"><span data-stu-id="b6d68-162">Re-deploy your application to Azure, and you should now be able to submit that form and send yourself (or any of your closest friends) a text message!</span></span>

<a id="nextsteps"/>

## <a name="next-steps"></a><span data-ttu-id="b6d68-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b6d68-163">Next Steps</span></span>
<span data-ttu-id="b6d68-164">Vous avez appris les bases d'utilisation de node.js et de Twilio pour générer des applications qui communiquent.</span><span class="sxs-lookup"><span data-stu-id="b6d68-164">You have now learned the basics of using node.js and Twilio to build apps that communicate.</span></span> <span data-ttu-id="b6d68-165">Mais ces exemples ne représentent d'une infime partie des possibilités offertes par Twilio et node.js.</span><span class="sxs-lookup"><span data-stu-id="b6d68-165">But these examples barely scratch the surface of what's possible with Twilio and node.js.</span></span> <span data-ttu-id="b6d68-166">Pour plus d'informations sur l'utilisation de Twilio avec node.js, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="b6d68-166">For more information using Twilio with node.js, check out the following resources:</span></span>

* <span data-ttu-id="b6d68-167">[Documentations officielles sur le module][docs]</span><span class="sxs-lookup"><span data-stu-id="b6d68-167">[Official module docs][docs]</span></span>
* <span data-ttu-id="b6d68-168">[Didacticiel sur VoIP avec des applications node.js][voipnode]</span><span class="sxs-lookup"><span data-stu-id="b6d68-168">[Tutorial on VoIP with node.js applications][voipnode]</span></span>
* <span data-ttu-id="b6d68-169">[Votr - application de vote par SMS en temps réel avec node.js et CouchDB (trois parties)][votr]</span><span class="sxs-lookup"><span data-stu-id="b6d68-169">[Votr - a real-time SMS voting application with node.js and CouchDB (three parts)][votr]</span></span>
* <span data-ttu-id="b6d68-170">[Programmation par paire dans le navigateur avec node.js][pair]</span><span class="sxs-lookup"><span data-stu-id="b6d68-170">[Pair programming in the browser with node.js][pair]</span></span>

<span data-ttu-id="b6d68-171">Nous espérons que vous aimerez travailler sur node.js et Twilio sur Azure !</span><span class="sxs-lookup"><span data-stu-id="b6d68-171">We hope you love hacking node.js and Twilio on Azure!</span></span>

[purchase_phone]: https://www.twilio.com/console/phone-numbers/search
[twiml]: https://www.twilio.com/docs/api/twiml
[signup]: http://ahoy.twilio.com/azure
[azure_new_site]: app-service-web/app-service-web-get-started-nodejs.md
[twilio_console]: https://www.twilio.com/console
<span data-ttu-id="b6d68-172">[npm]: http://npmjs.org</span><span class="sxs-lookup"><span data-stu-id="b6d68-172">[npm]: http://npmjs.org</span></span>
[express]: http://expressjs.com
[voipnode]: http://www.twilio.com/blog/2013/04/introduction-to-twilio-client-with-node-js.html
[docs]: http://twilio.github.io/twilio-node/
[votr]: http://www.twilio.com/blog/2012/09/building-a-real-time-sms-voting-app-part-1-node-js-couchdb.html
[pair]: http://www.twilio.com/blog/2013/06/pair-programming-in-the-browser-with-twilio.html
[azure-admin-console]: ./media/partner-twilio-nodejs-how-to-use-voice-sms/twilio_1.png
