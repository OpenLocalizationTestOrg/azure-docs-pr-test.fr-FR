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
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a>Utilisation de Twilio pour les fonctionnalités vocales, VoIP et de messagerie SMS dans Azure
Ce guide montre comment les applications toobuild qui communiquent avec Twilio et node.js dans Azure.

<a id="whatis"/>

## <a name="what-is-twilio"></a>Présentation de Twilio
Twilio est une plateforme d’API qui permet aux développeurs toomake facilement et de recevoir des appels téléphoniques, envoyer et recevoir des messages texte et incorporer un appel VoIP dans les applications mobiles natives et basée sur navigateur. Survolons rapidement le fonctionnement de Twilio avant de l'étudier plus en détail.

### <a name="receiving-calls-and-text-messages"></a>Réception d'appels et de SMS
Twilio permet aux développeurs de trop[acheter des numéros de téléphone programmable] [ purchase_phone] qui peut être utilisé tooboth envoyer et recevoir des appels et des messages texte. Lorsqu’un nombre de Twilio reçoit un appel entrant ou du texte, Twilio enverra votre application web un HTTP POST ou GET, vous demandant pour obtenir des instructions sur la façon dont toohandle hello appel ou texte. Votre serveur répond à la demande HTTP de tooTwilio avec [TwiML][twiml], un ensemble simple de balises XML contenant des instructions sur la façon de toohandle un appel ou un texte. Nous vous présenterons des exemples de TwiML un peu plus loin.

### <a name="making-calls-and-sending-text-messages"></a>Passage d'appels et envoi de SMS
En rendant toohello de demandes HTTP Twilio API du service web, les développeurs peuvent envoyer des messages texte ou initier des appels sortants. Pour les appels sortants, développeur de hello doit également spécifier une URL qui renvoie les instructions TwiML pour comment hello toohandle sortant appeler une fois qu’il est connecté.

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a>Incorporation des fonctionnalités VoIP dans un code de l'interface utilisateur (JavaScript, iOS ou Android)
Twilio offre un kit SDK côté client qui peut transformer n'importe quel navigateur web, application iOS ou Android en un téléphone VoIP. Dans cet article, nous allons nous concentrer sur la façon de toouse VoIP appel dans le navigateur de hello. En outre toohello *Twilio JavaScript SDK* en cours d’exécution dans le navigateur de hello, une application côté serveur (notre application node.js) doit être utilisé tooissue un client JavaScript de toohello « jeton capacité ». Vous pouvez en savoir plus sur l’utilisation de VoIP avec node.js [sur le blog de développement hello Twilio][voipnode].

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a>Inscription à Twilio (remise Microsoft)
Avant d’utiliser les services Twilio, vous devez [vous inscrire pour obtenir un compte][signup]. Les clients de Microsoft Azure reçoivent une remise spéciale - [être toosign vraiment ici][signup]!

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a>Création et déploiement d'un site web Azure node.js
Ensuite, vous devez toocreate un site Web de node.js s’exécutant sur Azure. [documentation officielle de Hello pour cette opération se trouve ici][azure_new_site]. À un niveau élevé, vous allez effectuer suivant de hello :

* Création d'un compte Azure si vous n'en possédez pas déjà un
* À l’aide de hello Azure admin console toocreate un nouveau site Web
* Ajout d'une prise en charge du contrôle de code source (nous présumons que vous avez utilisé git)
* Création d’un fichier `server.js` avec une application web node.js simple
* Déploiement tooAzure de cette application simple

<a id="twiliomodule"/>

## <a name="configure-hello-twilio-module"></a>Configurer hello Twilio Module
Ensuite, nous allons commencer toowrite utilisent une application node.js simple, ce qui rend hello Twilio API. Avant de commencer, nous devons tooconfigure nos informations d’identification du compte Twilio.

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a>Configuration des informations d'identification Twilio dans des variables d'environnement système
Dans les requêtes de toomake authentifié ordre contre hello Twilio back-end, nous devons notre SID de compte et un jeton d’authentification, quelle est la fonction en tant que nom d’utilisateur hello et le mot de passe défini pour notre compte Twilio. tooconfigure de façon plus sécurisée Hello pour une utilisation avec le module de nœud hello dans Azure est via des variables d’environnement système, que vous pouvez définir directement dans la console d’administration Azure hello.

Sélectionnez votre site Web node.js et cliquez sur le lien « Configurer » de hello.  Si vous faites un peu défiler vers le bas, vous verrez une zone dans laquelle vous pouvez définir les propriétés de configuration de votre application.  Entrez vos informations d’identification du compte Twilio ([trouvé sur votre Twilio Console][twilio_console]) comme - Assurez-vous que tooname les `TWILIO_ACCOUNT_SID` et `TWILIO_AUTH_TOKEN`, respectivement :

![Console d'administration Azure][azure-admin-console]

Une fois que vous avez configuré ces variables, redémarrez votre application Bonjour console Azure.

### <a name="declaring-hello-twilio-module-in-packagejson"></a>Déclaration de module de Twilio hello dans package.json
Ensuite, nous devons toocreate un toomanage package.json notre dépendances de modules de nœud via [npm]. À hello de même niveau en tant que hello `server.js` fichier que vous avez créé dans hello *Azure/node.js* (didacticiel), créez un fichier nommé `package.json`.  À l’intérieur de ce fichier, placer les suivant hello :

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

Cela déclare module de twilio hello comme une dépendance, ainsi que les hello populaires [Express infrastructure web] [ express] et le moteur de modèle EJS hello.  Tout est maintenant prêt et nous pouvons passer à l'écriture du code.

<a id="makecall"/>

## <a name="make-an-outbound-call"></a>Exécution d'un appel téléphonique
Nous allons créer un formulaire simple qui place un nombre de tooa appel que vous choisissez. Ouvrez `server.js`, puis entrez hello suivant de code. Notez intitulée « CHANGE_ME » - y placées nom hello de votre site Web azure :

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

Ensuite, créez un répertoire appelé `views` - dans ce répertoire, créez un fichier nommé `index.ejs` avec hello suivant le contenu :

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

Maintenant, déployez votre site Web tooAzure et ouvrir votre domicile. Vous devez être en mesure de tooenter votre numéro de téléphone dans le champ de texte hello et recevoir un appel à partir de votre numéro de Twilio !

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a>Envoi d'un SMS
Maintenant, nous allons définir une interface utilisateur et le formulaire toosend de la logique de la gestion des messages texte. Ouvrez `server.js`et ajoutez hello suivant de code après le dernier appel de hello trop`app.post`:

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

Dans `views/index.ejs`, ajoutez une autre forme sous hello toosubmit tout d’abord un un nombre et un message texte :

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message toosend" name="message"/>
  <br/>
  <input type="submit" value="Send text toohello number above"/>
</form>
```

Redéployez tooAzure de votre application, et vous devez maintenant être en mesure de toosubmit qui écran et envoyer des messages texte vous-même (ou un de vos amis le plus proche) !

<a id="nextsteps"/>

## <a name="next-steps"></a>Étapes suivantes
Vous avez désormais appris les notions de base de hello d’à l’aide de node.js et Twilio toobuild applications qui communiquent. Mais ces exemples scratch à peine surface hello de ce qui est possible avec Twilio et node.js. Pour plus d’informations à l’aide de Twilio avec node.js, consultez hello suivant des ressources :

* [Documentations officielles sur le module][docs]
* [Didacticiel sur VoIP avec des applications node.js][voipnode]
* [Votr - application de vote par SMS en temps réel avec node.js et CouchDB (trois parties)][votr]
* [Programmation de paire dans le navigateur hello avec node.js][pair]

Nous espérons que vous aimerez travailler sur node.js et Twilio sur Azure !

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
