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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-ruby"></a>Comment tooUse Twilio pour la voix et les fonctionnalités de SMS dans Ruby
Ce guide montre comment tooperform des tâches de programmation courantes avec hello Twilio API de service sur Azure. scénarios de Hello couvertes incluent un appel téléphonique et envoi d’un message de Service SMS (Short Message). Pour plus d’informations sur Twilio et à l’aide de la voix et SMS dans vos applications, consultez hello [étapes](#NextSteps) section.

## <a id="WhatIs"></a>Présentation de Twilio
Twilio est une API de service web de téléphonie qui vous permet d’utiliser votre langages web existants et les voix toobuild de compétences et les applications de SMS. Twilio est un service tiers, et non une fonctionnalité Azure ni un produit Microsoft.

**Twilio vocal** permet à votre toomake d’applications et de recevoir des appels téléphoniques. **Twilio SMS** permet à votre toomake d’applications et de recevoir des messages SMS. **Client twilio sur** tooenable la communication vocale via les connexions Internet, y compris les connexions mobiles permet à vos applications.

## <a id="Pricing"></a>Tarification de Twilio et offres spéciales
Des informations sur les prix de Twilio sont disponibles dans la page [Tarification de Twilio][twilio_pricing]. Les clients Azure reçoivent une [offre spéciale][special_offer] : un crédit gratuit de 1 000 SMS ou de 1 000 minutes d’appel en entrée. toosign pour cette offre ou obtenir plus d’informations, visitez [http://ahoy.twilio.com/azure][special_offer].  

## <a id="Concepts"></a>Concepts
Hello Twilio API est une API RESTful qui fournit la voix et fonctionnalités SMS pour les applications. Les bibliothèques clientes sont disponibles dans plusieurs langues : pour en obtenir la liste, consultez la page [Bibliothèques de l’API Twilio][twilio_libraries].

### <a id="TwiML"></a>TwiML
TwiML est un ensemble d’instructions basé sur XML qui informent Twilio de façon tooprocess un appel ou un SMS.

Par exemple, hello suivant TwiML permet de convertir le texte hello **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

Tous les documents TwiML ont un élément racine `<Response>` . À partir de là, vous utilisez comportement de hello toodefine Twilio verbes de votre application.

### <a id="Verbs"></a>Verbes TwiML
Les verbes de Twilio sont des balises XML qui indiquent à Twilio que trop**faire**. Par exemple, hello  **&lt;prononcer&gt;**  verbe fait en sorte que Twilio tooaudibly remettre un message sur un appel. 

Hello Voici une liste de verbes de Twilio.

* **&lt;Accès à distance&gt;**: se connecte phone de tooanother hello appelant.
* **&lt;Collecter des&gt;**: collecte les chiffres entrés sur le clavier de téléphone hello.
* **&lt;Hangup&gt;** : met fin à un appel.
* **&lt;Play&gt;** : lit un fichier audio.
* **&lt;Pause&gt;** : patiente silencieusement pendant un nombre déterminé de secondes.
* **&lt;Enregistrement&gt;**: enregistre la voix de l’appelant hello et retourne une URL d’un fichier contenant un enregistrement de hello.
* **&lt;Rediriger&gt;**: transfère le contrôle d’un appel ou un SMS toohello TwiML à une autre URL.
* **&lt;Rejeter&gt;**: rejette un entrant appeler tooyour Twilio nombre sans vous de facturation
* **&lt;Par exemple&gt;**: toospeech texte convertit effectuée sur un appel.
* **&lt;Sms&gt;** : envoie un SMS.

Pour plus d’informations sur les verbes Twilio, leurs attributs et le langage TwiML, consultez la page [TwiML][twiml]. Pour plus d’informations sur hello Twilio API, consultez [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Créer un compte Twilio
Lorsque vous êtes prêt tooget un compte de Twilio, inscrivez-vous dans [essayez de Twilio][try_twilio]. Vous pouvez commencer avec un compte gratuit, avant de le mettre à niveau ultérieurement.

Lors de la création d'un compte Twilio, vous obtenez un numéro de téléphone gratuit pour votre application. Vous recevez également un SID de compte et un jeton d'authentification. Les deux seront les appels d’API de Twilio toomake nécessaires. tooprevent non autorisé à accéder à tooyour compte, de sécuriser votre jeton d’authentification. Votre compte SID et le jeton d’authentification peuvent être consultés à hello [page de compte Twilio][twilio_account], dans hello champs **SID de compte** et **le jeton d’authentification** , respectivement.

### <a id="VerifyPhoneNumbers"></a>Vérifier les numéros de téléphone
Nombre de toohello plus que vous donne Twilio, vous pouvez également vérifier les nombres que vous contrôlez (autrement dit, votre téléphone portable ou accueil numéro de téléphone) pour une utilisation dans vos applications. 

Pour plus d’informations sur la façon de tooverify un numéro de téléphone, consultez [gérer les nombres][verify_phone].

## <a id="create_app"></a>Créer une application Ruby
Une application Ruby qui utilise le service de Twilio hello et s’exécute dans Azure n’est pas différente de toute autre application Ruby qui utilise le service de Twilio hello. Tandis que Twilio services sont RESTful qui peuvent être appelés depuis Ruby de plusieurs façons, cet article se concentrera sur le fonctionnement des services avec toouse Twilio [bibliothèque d’assistance de Twilio pour Ruby][twilio_ruby].

Tout d’abord, [configurer un nouvel ordinateur virtuel Azure Linux] [ azure_vm_setup] tooact en tant qu’hôte pour votre nouvelle application web Ruby. Ignorez les étapes hello impliquant la création d’une application de quadrillage, simplement hello de configuration VM hello. Veillez à créer un point de terminaison avec un port externe défini sur 80 et un port interne défini sur 5000.

Dans les exemples de hello ci-dessous, nous allons utiliser [Sinatra][sinatra], une infrastructure web très simple pour Ruby. Mais vous pouvez certainement utiliser bibliothèque d’assistance de Twilio hello pour Ruby avec n’importe quel autre infrastructure web, y compris Ruby on Rails.

Utilisez SSH dans votre nouvelle machine virtuelle et créez un répertoire pour votre nouvelle application. À l’intérieur de ce répertoire, créez un fichier appelé Gemfile et copie hello après le code dans celui-ci :

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

Sur la ligne de commande hello exécuter `bundle install`. Dépendances de hello ci-dessus seront installés. Ensuite, créez un fichier appelé `web.rb`. Il s’agit de résidence de code hello pour votre application web. Collez hello après le code dans celui-ci :

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

À ce stade, vous devez être commande hello de hello en mesure de s’exécuter `ruby web.rb -p 5000`. Ceci met en place un petit serveur web sur le port 5000. Vous devez être en mesure de toobrowse toothis application dans votre navigateur en visitant l’URL de hello vous configuration pour votre machine virtuelle Azure. Une fois que vous pouvez atteindre votre application web dans le navigateur de hello, vous êtes prêt toostart création d’une application Twilio.

## <a id="configure_app"></a>Configurer votre Application tooUse Twilio
Vous pouvez configurer votre bibliothèque de Twilio web application toouse hello en mettant à jour votre `Gemfile` tooinclude cette ligne :

    gem 'twilio-ruby'

Sur la ligne de commande hello, exécutez `bundle install`. Ouvrez maintenant `web.rb` et incluant cette ligne en haut de hello :

    require 'twilio-ruby'

Vous êtes maintenant toutes définies bibliothèque d’assistance de toouse hello Twilio pour Ruby dans votre application web.

## <a id="howto_make_call"></a>Procédure : passer un appel sortant
Hello suivant montre comment appeler le toomake sortante. Concepts clés incluent à l’aide de la bibliothèque d’assistance de Twilio hello pour Ruby toomake qu'appelle des API REST et TwiML de rendu. Remplacez par vos valeurs hello **de** et **à** les numéros de téléphone et assurez-vous que vous vérifiez hello **à partir de** numéro de téléphone de votre code hello de Twilio compte toorunning préalable.

Ajouter cette fonction trop`web.md`:

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

Si l’ouverture des `http://yourdomain.cloudapp.net/make_call` dans un navigateur, qui déclenchera un appel téléphonique de hello appel toohello Twilio API toomake hello. Hello des deux premiers paramètres dans `client.account.calls.create` sont suffisamment explicites : hello numéro hello appel est `from` et appel de hello numéro hello est `to`. 

Hello troisième paramètre (`url`) est l’URL de hello que Twilio demande tooget des instructions sur le toodo une fois que l’appel hello est connecté. Dans ce cas nous configurer une URL (`http://yourdomain.cloudapp.net`) qui retourne un document TwiML simple et utilise hello `<Say>` toodo verbe certains synthèse vocale, puis prononcez « Hello le » toohello destinataire hello appeler.

## <a id="howto_recieve_sms"></a>Réception d’un SMS
Dans l’exemple précédent de hello, nous avons lancé une **sortants** appel téléphonique. Cette fois, nous allons utiliser le numéro de téléphone hello Twilio nous a donné au cours de l’inscription tooprocess un **entrant** message SMS.

Tout d’abord, ouverture de session de tooyour [tableau de bord Twilio][twilio_account]. Cliquez sur « Numéros » de navigation supérieure de hello, puis cliquez sur hello le nombre de Twilio que vous ont été fournis. Deux URL sont disponibles pour configuration : une URL de requête vocale et une URL de requête SMS. Il s’agit des URL de hello Twilio appelle chaque fois qu’un appel téléphonique est effectuée ou un SMS envoyé tooyour nombre. URL de Hello sont également définis en tant que « web hooks ».

Nous aimerions tooprocess les messages SMS entrants, par conséquent, nous allons mettre à jour des URL de hello trop`http://yourdomain.cloudapp.net/sms_url`. Pour commencer, cliquez sur Enregistrer les changements au bas de hello de page de hello. Maintenant, de retour dans `web.rb` programme nous allons notre toohandle application cela :

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for hello ping! Twilio and Azure rock!</Message>
       </Response>"
    end

Après avoir apporté la modification de hello, assurez-vous que toore-démarrer votre application web. Ensuite, retirez votre téléphone et envoyer un SMS de tooyour Twilio nombre. Vous devez obtenir rapidement une réponse SMS indiquant que « Hey, Merci de ping de hello ! Twilio et Azure sont les meilleurs ! »

## <a id="additional_services"></a>Utilisation de services Twilio supplémentaires
En outre toohello les exemples indiqués ici, que twilio propose des API basées sur le web qui vous pouvez utiliser des fonctionnalités Twilio tooleverage supplémentaires à partir de votre application Windows Azure. Pour plus d’informations, consultez hello [documentation de l’API de Twilio][twilio_api_documentation].

### <a id="NextSteps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello Hello Twilio service, suivez ces liens de toolearn plus :

* [Conseils de sécurité Twilio][twilio_security_guidelines]
* [Procédures et exemples de code Twilio][twilio_howtos]
* [Didacticiels de démarrage rapide Twilio][twilio_quickstarts] 
* [Twilio sur GitHub][twilio_on_github]
* [Communiquer avec tooTwilio prise en charge][twilio_support]

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
