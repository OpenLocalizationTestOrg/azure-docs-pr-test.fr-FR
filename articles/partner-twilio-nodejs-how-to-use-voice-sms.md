---
title: aaaUsing Twilio pour la voix, VoIP et messagerie SMS dans Azure
description: "Découvrez comment toomake un appel téléphonique et envoyer un SMS de message avec le service de l’API de Twilio hello sur Azure. Exemples de code écrits en Node.js."
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
ms.openlocfilehash: 6c44d60e217fcdf51e69fd2a8197f979afbb507a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a><span data-ttu-id="67096-104">Utilisation de Twilio pour les fonctionnalités vocales, VoIP et de messagerie SMS dans Azure</span><span class="sxs-lookup"><span data-stu-id="67096-104">Using Twilio for Voice, VoIP, and SMS Messaging in Azure</span></span>
<span data-ttu-id="67096-105">Ce guide montre comment les applications toobuild qui communiquent avec Twilio et node.js dans Azure.</span><span class="sxs-lookup"><span data-stu-id="67096-105">This guide demonstrates how toobuild apps that communicate with Twilio and node.js on Azure.</span></span>

<a id="whatis"/>

## <a name="what-is-twilio"></a><span data-ttu-id="67096-106">Présentation de Twilio</span><span class="sxs-lookup"><span data-stu-id="67096-106">What is Twilio?</span></span>
<span data-ttu-id="67096-107">Twilio est une plateforme d’API qui permet aux développeurs toomake facilement et de recevoir des appels téléphoniques, envoyer et recevoir des messages texte et incorporer un appel VoIP dans les applications mobiles natives et basée sur navigateur.</span><span class="sxs-lookup"><span data-stu-id="67096-107">Twilio is an API platform that makes it easy for developers toomake and receive phone calls, send and receive text messages, and embed VoIP calling into browser-based and native mobile applications.</span></span> <span data-ttu-id="67096-108">Survolons rapidement le fonctionnement de Twilio avant de l'étudier plus en détail.</span><span class="sxs-lookup"><span data-stu-id="67096-108">Let's briefly go over how this works before diving in.</span></span>

### <a name="receiving-calls-and-text-messages"></a><span data-ttu-id="67096-109">Réception d'appels et de SMS</span><span class="sxs-lookup"><span data-stu-id="67096-109">Receiving Calls and Text Messages</span></span>
<span data-ttu-id="67096-110">Twilio permet aux développeurs de trop[acheter des numéros de téléphone programmable] [ purchase_phone] qui peut être utilisé tooboth envoyer et recevoir des appels et des messages texte.</span><span class="sxs-lookup"><span data-stu-id="67096-110">Twilio allows developers too[purchase programmable phone numbers][purchase_phone] which can be used tooboth send and receive calls and text messages.</span></span> <span data-ttu-id="67096-111">Lorsqu’un nombre de Twilio reçoit un appel entrant ou du texte, Twilio enverra votre application web un HTTP POST ou GET, vous demandant pour obtenir des instructions sur la façon dont toohandle hello appel ou texte.</span><span class="sxs-lookup"><span data-stu-id="67096-111">When a Twilio number receives an inbound call or text, Twilio will send your web application an HTTP POST or GET request, asking you for instructions on how toohandle hello call or text.</span></span> <span data-ttu-id="67096-112">Votre serveur répond à la demande HTTP de tooTwilio avec [TwiML][twiml], un ensemble simple de balises XML contenant des instructions sur la façon de toohandle un appel ou un texte.</span><span class="sxs-lookup"><span data-stu-id="67096-112">Your server will respond tooTwilio's HTTP request with [TwiML][twiml], a simple set of XML tags that contain instructions on how toohandle a call or text.</span></span> <span data-ttu-id="67096-113">Nous vous présenterons des exemples de TwiML un peu plus loin.</span><span class="sxs-lookup"><span data-stu-id="67096-113">We will see examples of TwiML in just a moment.</span></span>

### <a name="making-calls-and-sending-text-messages"></a><span data-ttu-id="67096-114">Passage d'appels et envoi de SMS</span><span class="sxs-lookup"><span data-stu-id="67096-114">Making Calls and Sending Text Messages</span></span>
<span data-ttu-id="67096-115">En rendant toohello de demandes HTTP Twilio API du service web, les développeurs peuvent envoyer des messages texte ou initier des appels sortants.</span><span class="sxs-lookup"><span data-stu-id="67096-115">By making HTTP requests toohello Twilio web service API, developers can send text messages or initiate outbound phone calls.</span></span> <span data-ttu-id="67096-116">Pour les appels sortants, développeur de hello doit également spécifier une URL qui renvoie les instructions TwiML pour comment hello toohandle sortant appeler une fois qu’il est connecté.</span><span class="sxs-lookup"><span data-stu-id="67096-116">For outbound calls, hello developer must also specify a URL that returns TwiML instructions for how toohandle hello outbound call once it is connected.</span></span>

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a><span data-ttu-id="67096-117">Incorporation des fonctionnalités VoIP dans un code de l'interface utilisateur (JavaScript, iOS ou Android)</span><span class="sxs-lookup"><span data-stu-id="67096-117">Embedding VoIP Capabilities in UI code (JavaScript, iOS, or Android)</span></span>
<span data-ttu-id="67096-118">Twilio offre un kit SDK côté client qui peut transformer n'importe quel navigateur web, application iOS ou Android en un téléphone VoIP.</span><span class="sxs-lookup"><span data-stu-id="67096-118">Twilio provides a client-side SDK which can turn any desktop web browser, iOS app, or Android app into a VoIP phone.</span></span> <span data-ttu-id="67096-119">Dans cet article, nous allons nous concentrer sur la façon de toouse VoIP appel dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="67096-119">In this article, we will focus on how toouse VoIP calling in hello browser.</span></span> <span data-ttu-id="67096-120">En outre toohello *Twilio JavaScript SDK* en cours d’exécution dans le navigateur de hello, une application côté serveur (notre application node.js) doit être utilisé tooissue un client JavaScript de toohello « jeton capacité ».</span><span class="sxs-lookup"><span data-stu-id="67096-120">In addition toohello *Twilio JavaScript SDK* running in hello browser, a server-side application (our node.js application) must be used tooissue a "capability token" toohello JavaScript client.</span></span> <span data-ttu-id="67096-121">Vous pouvez en savoir plus sur l’utilisation de VoIP avec node.js [sur le blog de développement hello Twilio][voipnode].</span><span class="sxs-lookup"><span data-stu-id="67096-121">You can read more about using VoIP with node.js [on hello Twilio dev blog][voipnode].</span></span>

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a><span data-ttu-id="67096-122">Inscription à Twilio (remise Microsoft)</span><span class="sxs-lookup"><span data-stu-id="67096-122">Sign Up For Twilio (Microsoft Discount)</span></span>
<span data-ttu-id="67096-123">Avant d’utiliser les services Twilio, vous devez [vous inscrire pour obtenir un compte][signup].</span><span class="sxs-lookup"><span data-stu-id="67096-123">Before using Twilio services, you must first [sign up for an account][signup].</span></span> <span data-ttu-id="67096-124">Les clients de Microsoft Azure reçoivent une remise spéciale - [être toosign vraiment ici][signup]!</span><span class="sxs-lookup"><span data-stu-id="67096-124">Microsoft Azure customers receive a special discount - [be sure toosign up here][signup]!</span></span>

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a><span data-ttu-id="67096-125">Création et déploiement d'un site web Azure node.js</span><span class="sxs-lookup"><span data-stu-id="67096-125">Create and Deploy a node.js Azure Website</span></span>
<span data-ttu-id="67096-126">Ensuite, vous devez toocreate un site Web de node.js s’exécutant sur Azure.</span><span class="sxs-lookup"><span data-stu-id="67096-126">Next, you will need toocreate a node.js website running on Azure.</span></span> <span data-ttu-id="67096-127">[documentation officielle de Hello pour cette opération se trouve ici][azure_new_site].</span><span class="sxs-lookup"><span data-stu-id="67096-127">[hello official documentation for doing this is located here][azure_new_site].</span></span> <span data-ttu-id="67096-128">À un niveau élevé, vous allez effectuer suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="67096-128">At a high level, you will be doing hello following:</span></span>

* <span data-ttu-id="67096-129">Création d'un compte Azure si vous n'en possédez pas déjà un</span><span class="sxs-lookup"><span data-stu-id="67096-129">Signing up for an Azure account, if you don't have one already</span></span>
* <span data-ttu-id="67096-130">À l’aide de hello Azure admin console toocreate un nouveau site Web</span><span class="sxs-lookup"><span data-stu-id="67096-130">Using hello Azure admin console toocreate a new website</span></span>
* <span data-ttu-id="67096-131">Ajout d'une prise en charge du contrôle de code source (nous présumons que vous avez utilisé git)</span><span class="sxs-lookup"><span data-stu-id="67096-131">Adding source control support (we will assume you used git)</span></span>
* <span data-ttu-id="67096-132">Création d’un fichier `server.js` avec une application web node.js simple</span><span class="sxs-lookup"><span data-stu-id="67096-132">Creating a file `server.js` with a simple node.js web application</span></span>
* <span data-ttu-id="67096-133">Déploiement tooAzure de cette application simple</span><span class="sxs-lookup"><span data-stu-id="67096-133">Deploying this simple application tooAzure</span></span>

<a id="twiliomodule"/>

## <a name="configure-hello-twilio-module"></a><span data-ttu-id="67096-134">Configurer hello Twilio Module</span><span class="sxs-lookup"><span data-stu-id="67096-134">Configure hello Twilio Module</span></span>
<span data-ttu-id="67096-135">Ensuite, nous allons commencer toowrite utilisent une application node.js simple, ce qui rend hello Twilio API.</span><span class="sxs-lookup"><span data-stu-id="67096-135">Next, we will begin toowrite a simple node.js application which makes use of hello Twilio API.</span></span> <span data-ttu-id="67096-136">Avant de commencer, nous devons tooconfigure nos informations d’identification du compte Twilio.</span><span class="sxs-lookup"><span data-stu-id="67096-136">Before we begin, we need tooconfigure our Twilio account credentials.</span></span>

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a><span data-ttu-id="67096-137">Configuration des informations d'identification Twilio dans des variables d'environnement système</span><span class="sxs-lookup"><span data-stu-id="67096-137">Configuring Twilio Credentials in System Environment Variables</span></span>
<span data-ttu-id="67096-138">Dans les requêtes de toomake authentifié ordre contre hello Twilio back-end, nous devons notre SID de compte et un jeton d’authentification, quelle est la fonction en tant que nom d’utilisateur hello et le mot de passe défini pour notre compte Twilio.</span><span class="sxs-lookup"><span data-stu-id="67096-138">In order toomake authenticated requests against hello Twilio back end, we need our account SID and auth token, which function as hello username and password set for our Twilio account.</span></span> <span data-ttu-id="67096-139">tooconfigure de façon plus sécurisée Hello pour une utilisation avec le module de nœud hello dans Azure est via des variables d’environnement système, que vous pouvez définir directement dans la console d’administration Azure hello.</span><span class="sxs-lookup"><span data-stu-id="67096-139">hello most secure way tooconfigure these for use with hello node module in Azure is via system environment variables, which you can set directly in hello Azure admin console.</span></span>

<span data-ttu-id="67096-140">Sélectionnez votre site Web node.js et cliquez sur le lien « Configurer » de hello.</span><span class="sxs-lookup"><span data-stu-id="67096-140">Select your node.js website, and click hello "CONFIGURE" link.</span></span>  <span data-ttu-id="67096-141">Si vous faites un peu défiler vers le bas, vous verrez une zone dans laquelle vous pouvez définir les propriétés de configuration de votre application.</span><span class="sxs-lookup"><span data-stu-id="67096-141">If you scroll down a bit, you will see an area where you can set configuration properties for your application.</span></span>  <span data-ttu-id="67096-142">Entrez vos informations d’identification du compte Twilio ([trouvé sur votre Twilio Console][twilio_console]) comme - Assurez-vous que tooname les `TWILIO_ACCOUNT_SID` et `TWILIO_AUTH_TOKEN`, respectivement :</span><span class="sxs-lookup"><span data-stu-id="67096-142">Enter your Twilio account credentials ([found on your Twilio Console][twilio_console]) as shown - make sure tooname them `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN`, respectively:</span></span>

![Console d'administration Azure][azure-admin-console]

<span data-ttu-id="67096-144">Une fois que vous avez configuré ces variables, redémarrez votre application Bonjour console Azure.</span><span class="sxs-lookup"><span data-stu-id="67096-144">Once you have configured these variables, restart your application in hello Azure console.</span></span>

### <a name="declaring-hello-twilio-module-in-packagejson"></a><span data-ttu-id="67096-145">Déclaration de module de Twilio hello dans package.json</span><span class="sxs-lookup"><span data-stu-id="67096-145">Declaring hello Twilio module in package.json</span></span>
<span data-ttu-id="67096-146">Ensuite, nous devons toocreate un toomanage package.json notre dépendances de modules de nœud via [npm].</span><span class="sxs-lookup"><span data-stu-id="67096-146">Next, we need toocreate a package.json toomanage our node module dependencies via [npm].</span></span> <span data-ttu-id="67096-147">À hello de même niveau en tant que hello `server.js` fichier que vous avez créé dans hello *Azure/node.js* (didacticiel), créez un fichier nommé `package.json`.</span><span class="sxs-lookup"><span data-stu-id="67096-147">At hello same level as hello `server.js` file you created in hello *Azure/node.js* tutorial, create a file named `package.json`.</span></span>  <span data-ttu-id="67096-148">À l’intérieur de ce fichier, placer les suivant hello :</span><span class="sxs-lookup"><span data-stu-id="67096-148">Inside this file, place hello following:</span></span>

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

<span data-ttu-id="67096-149">Cela déclare module de twilio hello comme une dépendance, ainsi que les hello populaires [Express infrastructure web] [ express] et le moteur de modèle EJS hello.</span><span class="sxs-lookup"><span data-stu-id="67096-149">This declares hello twilio module as a dependency, as well as hello popular [Express web framework][express] and hello EJS template engine.</span></span>  <span data-ttu-id="67096-150">Tout est maintenant prêt et nous pouvons passer à l'écriture du code.</span><span class="sxs-lookup"><span data-stu-id="67096-150">Okay, now we're all set - let's write some code!</span></span>

<a id="makecall"/>

## <a name="make-an-outbound-call"></a><span data-ttu-id="67096-151">Exécution d'un appel téléphonique</span><span class="sxs-lookup"><span data-stu-id="67096-151">Make an Outbound Call</span></span>
<span data-ttu-id="67096-152">Nous allons créer un formulaire simple qui place un nombre de tooa appel que vous choisissez.</span><span class="sxs-lookup"><span data-stu-id="67096-152">Let's create a simple form that will place a call tooa number we choose.</span></span> <span data-ttu-id="67096-153">Ouvrez `server.js`, puis entrez hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="67096-153">Open up `server.js`, and enter hello following code.</span></span> <span data-ttu-id="67096-154">Notez intitulée « CHANGE_ME » - y placées nom hello de votre site Web azure :</span><span class="sxs-lookup"><span data-stu-id="67096-154">Note where it says "CHANGE_ME" - put hello name of your azure website there:</span></span>

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

// Render an HTML user interface for hello application's home page
app.get('/', (request, response) => response.render('index'));

// Handle hello form POST tooplace a call
app.post('/call', (request, response) => {
  var client = twilio(accountSid, authToken);

  client.makeCall({
    // make a call toothis number
    to:request.body.number,

    // Change tooa Twilio number you bought - see:
    // https://www.twilio.com/console/phone-numbers/incoming
    from:'+15558675309',

    // A URL in our app which generates TwiML
    // Change "CHANGE_ME" tooyour app's name
    url:'https://CHANGE_ME.azurewebsites.net/outbound_call'
  }, () => {
      // Go back toohello home page
      response.redirect('/');
  });
});

// Generate TwiML toohandle an outbound call
app.post('/outbound_call', (request, response) => {
  var twiml = new twilio.TwimlResponse();

  // Say a message toohello call's receiver
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

<span data-ttu-id="67096-155">Ensuite, créez un répertoire appelé `views` - dans ce répertoire, créez un fichier nommé `index.ejs` avec hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="67096-155">Next, create a directory called `views` - inside this directory, create a file named `index.ejs` with hello following contents:</span></span>

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
      <input type="submit" value="Call hello number above"/>
  </form>
</body>
</html>
```

<span data-ttu-id="67096-156">Maintenant, déployez votre site Web tooAzure et ouvrir votre domicile.</span><span class="sxs-lookup"><span data-stu-id="67096-156">Now, deploy your website tooAzure and open your home.</span></span> <span data-ttu-id="67096-157">Vous devez être en mesure de tooenter votre numéro de téléphone dans le champ de texte hello et recevoir un appel à partir de votre numéro de Twilio !</span><span class="sxs-lookup"><span data-stu-id="67096-157">You should be able tooenter your phone number in hello text field, and receive a call from your Twilio number!</span></span>

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a><span data-ttu-id="67096-158">Envoi d'un SMS</span><span class="sxs-lookup"><span data-stu-id="67096-158">Send an SMS Message</span></span>
<span data-ttu-id="67096-159">Maintenant, nous allons définir une interface utilisateur et le formulaire toosend de la logique de la gestion des messages texte.</span><span class="sxs-lookup"><span data-stu-id="67096-159">Now, let's set up a user interface and form handling logic toosend a text message.</span></span> <span data-ttu-id="67096-160">Ouvrez `server.js`et ajoutez hello suivant de code après le dernier appel de hello trop`app.post`:</span><span class="sxs-lookup"><span data-stu-id="67096-160">Open up `server.js`, and add hello following code after hello last call too`app.post`:</span></span>

```javascript
app.post('/sms', (request, response) => {
  const client = twilio(accountSid, authToken);

  client.sendSms({
      // send a text toothis number
      to:request.body.number,

      // A Twilio number you bought - see:
      // https://www.twilio.com/console/phone-numbers/incoming
      from:'+15558675309',

      // hello body of hello text message
      body: request.body.message

  }, () => {
      // Go back toohello home page
      response.redirect('/');
  });
});
```

<span data-ttu-id="67096-161">Dans `views/index.ejs`, ajoutez une autre forme sous hello toosubmit tout d’abord un un nombre et un message texte :</span><span class="sxs-lookup"><span data-stu-id="67096-161">In `views/index.ejs`, add another form under hello first one toosubmit a number and a text message:</span></span>

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message toosend" name="message"/>
  <br/>
  <input type="submit" value="Send text toohello number above"/>
</form>
```

<span data-ttu-id="67096-162">Redéployez tooAzure de votre application, et vous devez maintenant être en mesure de toosubmit qui écran et envoyer des messages texte vous-même (ou un de vos amis le plus proche) !</span><span class="sxs-lookup"><span data-stu-id="67096-162">Re-deploy your application tooAzure, and you should now be able toosubmit that form and send yourself (or any of your closest friends) a text message!</span></span>

<a id="nextsteps"/>

## <a name="next-steps"></a><span data-ttu-id="67096-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="67096-163">Next Steps</span></span>
<span data-ttu-id="67096-164">Vous avez désormais appris les notions de base de hello d’à l’aide de node.js et Twilio toobuild applications qui communiquent.</span><span class="sxs-lookup"><span data-stu-id="67096-164">You have now learned hello basics of using node.js and Twilio toobuild apps that communicate.</span></span> <span data-ttu-id="67096-165">Mais ces exemples scratch à peine surface hello de ce qui est possible avec Twilio et node.js.</span><span class="sxs-lookup"><span data-stu-id="67096-165">But these examples barely scratch hello surface of what's possible with Twilio and node.js.</span></span> <span data-ttu-id="67096-166">Pour plus d’informations à l’aide de Twilio avec node.js, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="67096-166">For more information using Twilio with node.js, check out hello following resources:</span></span>

* <span data-ttu-id="67096-167">[Documentations officielles sur le module][docs]</span><span class="sxs-lookup"><span data-stu-id="67096-167">[Official module docs][docs]</span></span>
* <span data-ttu-id="67096-168">[Didacticiel sur VoIP avec des applications node.js][voipnode]</span><span class="sxs-lookup"><span data-stu-id="67096-168">[Tutorial on VoIP with node.js applications][voipnode]</span></span>
* <span data-ttu-id="67096-169">[Votr - application de vote par SMS en temps réel avec node.js et CouchDB (trois parties)][votr]</span><span class="sxs-lookup"><span data-stu-id="67096-169">[Votr - a real-time SMS voting application with node.js and CouchDB (three parts)][votr]</span></span>
* <span data-ttu-id="67096-170">[Programmation de paire dans le navigateur hello avec node.js][pair]</span><span class="sxs-lookup"><span data-stu-id="67096-170">[Pair programming in hello browser with node.js][pair]</span></span>

<span data-ttu-id="67096-171">Nous espérons que vous aimerez travailler sur node.js et Twilio sur Azure !</span><span class="sxs-lookup"><span data-stu-id="67096-171">We hope you love hacking node.js and Twilio on Azure!</span></span>

[purchase_phone]: https://www.twilio.com/console/phone-numbers/search
[twiml]: https://www.twilio.com/docs/api/twiml
[signup]: http://ahoy.twilio.com/azure
[azure_new_site]: app-service-web/app-service-web-get-started-nodejs.md
[twilio_console]: https://www.twilio.com/console
[npm]: http://npmjs.org
[express]: http://expressjs.com
[voipnode]: http://www.twilio.com/blog/2013/04/introduction-to-twilio-client-with-node-js.html
[docs]: http://twilio.github.io/twilio-node/
[votr]: http://www.twilio.com/blog/2012/09/building-a-real-time-sms-voting-app-part-1-node-js-couchdb.html
[pair]: http://www.twilio.com/blog/2013/06/pair-programming-in-the-browser-with-twilio.html
[azure-admin-console]: ./media/partner-twilio-nodejs-how-to-use-voice-sms/twilio_1.png
