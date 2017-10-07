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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-python"></a>Comment tooUse Twilio pour la voix et les fonctionnalités de SMS dans Python
Ce guide montre comment tooperform des tâches de programmation courantes avec hello Twilio API de service sur Azure. scénarios de Hello couvertes incluent un appel téléphonique et envoi d’un message de Service SMS (Short Message). Pour plus d’informations sur Twilio et à l’aide de la voix et SMS dans vos applications, consultez hello [étapes](#NextSteps) section.

## <a id="WhatIs"></a>Présentation de Twilio
Twilio est futures hello de communications professionnelles de mise sous tension, l’activation de voix de tooembed les développeurs, VoIP et dans les applications de messagerie. La virtualisation toute infrastructure nécessaires dans un environnement en nuage, global, exposant via la plateforme de hello Twilio communications API. Les applications sont toobuild simple et évolutive. Tirez parti de la souplesse du paiement à l'utilisation et de la fiabilité du cloud.

**Twilio vocal** permet à votre toomake d’applications et de recevoir des appels téléphoniques.
**Twilio SMS** Active toosend de votre application et de recevoir des messages texte.
**Client twilio sur** vous permet d’appels de VoIP toomake à partir de n’importe quel téléphone, tablette ou un navigateur et prend en charge WebRTC.

## <a id="Pricing"></a>Tarification de Twilio et offres spéciales
Les clients Azure reçoivent une [offre spéciale][special_offer] de 10 $ en crédit Twilio quand ils mettent à niveau leur compte Twilio. Ce Twilio crédit peut être appliqué tooany l’utilisation de Twilio (10 $ crédit équivalent toosending jusqu'à 1 000 messages SMS et la réception des too1000 entrants voix minutes, selon emplacement hello de votre destination de nombre et de message ou d’appel téléphonique). Profitez de ce [crédit Twilio][special_offer] et lancez-vous.

Twilio est un service de paiement à l'utilisation. Il n'existe pas de frais d'entrée et vous pouvez fermer votre compte quand vous le souhaitez. Pour plus d’informations, consultez la page [Tarification de Twilio][twilio_pricing].

## <a id="Concepts"></a>Concepts
Hello Twilio API est une API RESTful qui fournit la voix et fonctionnalités SMS pour les applications. Les bibliothèques clientes sont disponibles dans plusieurs langues : pour en obtenir la liste, consultez la page [Bibliothèques de l’API Twilio][twilio_libraries].

Les principaux aspects du hello Twilio API sont Twilio verbes et Twilio Markup Language (TwiML).

### <a id="Verbs"></a>Verbes Twilio
Hello API se sert de Twilio verbes ; par exemple, hello  **&lt;prononcer&gt;**  verbe fait en sorte que Twilio tooaudibly remettre un message sur un appel.

Hello Voici une liste de verbes de Twilio. En savoir plus sur hello autres verbes et les fonctionnalités via [documentation de langage de balisage Twilio][twiml].

* **&lt;Accès à distance&gt;**: se connecte phone de tooanother hello appelant.
* **&lt;Collecter des&gt;**: collecte les chiffres entrés sur le clavier de téléphone hello.
* **&lt;Hangup&gt;** : met fin à un appel.
* **&lt;Pause&gt;** : patiente silencieusement pendant un nombre déterminé de secondes.
* **&lt;Play&gt;** : lit un fichier audio.
* **&lt;File d’attente&gt;**: ajouter la file d’attente de tooa hello des appelants.
* **&lt;Enregistrement&gt;**: enregistre les voix hello de l’appelant de hello et retourne une URL d’un fichier contenant un enregistrement de hello.
* **&lt;Rediriger&gt;**: transfère le contrôle d’un appel ou un SMS toohello TwiML à une autre URL.
* **&lt;Rejeter&gt;**: rejette un entrant appeler tooyour Twilio nombre sans vous de facturation.
* **&lt;Par exemple&gt;**: toospeech texte convertit effectuée sur un appel.
* **&lt;Sms&gt;** : envoie un SMS.

### <a id="TwiML"></a>TwiML
TwiML est un ensemble d’instructions basé sur XML en fonction de verbes Twilio hello qui informent Twilio de façon tooprocess un appel ou un SMS.

Par exemple, hello suivant TwiML permet de convertir le texte hello **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

Lorsque votre application appelle hello Twilio API, un des paramètres d’API hello est hello URL qui renvoie la réponse de TwiML hello. À des fins de développement, vous pouvez utiliser l’URL fournie par Twilio tooprovide hello TwiML les réponses employées par vos applications. Vous pourriez également héberger vos réponses de TwiML URL tooproduce hello et une autre option consiste à toouse hello `TwiMLResponse` objet.

Pour plus d’informations sur les verbes Twilio, leurs attributs et le langage TwiML, consultez la page [TwiML][twiml]. Pour plus d’informations sur hello Twilio API, consultez [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Créer un compte Twilio
Lorsque vous êtes prêt tooget un compte de Twilio, inscrivez-vous dans [essayez de Twilio][try_twilio]. Vous pouvez commencer avec un compte gratuit, avant de le mettre à niveau ultérieurement.

Quand vous vous inscrivez pour obtenir un compte Twilio, vous recevez un SID de compte et un jeton d’authentification. Les deux seront les appels d’API de Twilio toomake nécessaires. tooprevent non autorisé à accéder à tooyour compte, de sécuriser votre jeton d’authentification. Votre compte SID et le jeton d’authentification peuvent être consultés dans hello [Twilio Console][twilio_console], dans hello champs **SID de compte** et **dujetond’authentification**, respectivement.

## <a id="create_app"></a>Créer une application Python
Une application de Python qui utilise le service de Twilio hello et s’exécute dans Azure n’est pas différente de toute autre application Python qui utilise le service de Twilio hello. Twilio services sont basés sur REST et peuvent être appelées à partir de Python de plusieurs façons, cet article se concentrera sur le fonctionnement des services avec toouse Twilio [bibliothèque Twilio pour Python à partir de GitHub][twilio_python]. Pour plus d’informations sur l’utilisation de la bibliothèque de Twilio hello pour Python, consultez [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].

Première, [configurer un nouvel ordinateur virtuel Azure Linux] tooact [azure_vm_setup] en tant qu’hôte pour votre nouvelle application web de Python. Une fois que hello ordinateur virtuel est en cours d’exécution, vous devez tooexpose votre application sur un port public comme décrit ci-dessous.

### <a name="add-an-incoming-rule"></a>Ajouter une règle entrante
  1. Accédez toohello [groupe de sécurité réseau] [azure_nsg] page.
  2. Sélectionnez hello réseau de groupe de sécurité qui correspond à votre Machine virtuelle.
  3. Ajoutez une **règle sortante** pour le **port 80**. Être tooallow vraiment entrante à partir de n’importe quelle adresse.

### <a name="set-hello-dns-name-label"></a>Ensemble hello étiquette de nom DNS
  1. Accédez toohello [hello des Adresses IP publiques] [azure_ips] page.
  2. Sélectionnez hello adresse IP publique que correspends avec votre Machine virtuelle.
  3. Ensemble hello **étiquette de nom DNS** Bonjour **Configuration** section. Dans les cas de hello de cet exemple montre comment il ressemble à ceci *votre nom de domaine*. centralus.cloudapp.azure.com

Une fois que vous êtes en mesure de tooconnect via SSH toohello Machine virtuelle que vous pouvez installer hello infrastructure Web de votre choix (hello plus connus dans Python étant deux [ballon](http://flask.pocoo.org/) et [Django](https://www.djangoproject.com)). Vous pouvez installer un d’eux simplement en exécutant hello `pip install` commande.

Gardez à l’esprit que nous avons configuré tooallow le trafic de la Machine virtuelle hello uniquement sur le port 80. Par conséquent, assurez-vous que tooconfigure hello application toouse ce port.

## <a id="configure_app"></a>Configurez des bibliothèques de votre Application tooUse Twilio
Vous pouvez configurer votre bibliothèque de Twilio application toouse hello pour Python de deux manières :

* Installer la bibliothèque de Twilio hello pour Python en tant que package Pip. Il peut être installé avec hello suivant de commandes :
   
        $ pip install twilio

    OU

* Télécharger la bibliothèque de Twilio hello pour Python à partir de GitHub ([https://github.com/twilio/twilio-python][twilio_python]) et l’installer comme suit :

        $ python setup.py install

Une fois que vous avez installé la bibliothèque de Twilio hello pour Python, vous pouvez ensuite `import` dans vos fichiers Python :

        import twilio

Pour plus d’informations, consultez [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].

## <a id="howto_make_call"></a>Procédure : passer un appel sortant
Hello suivant montre comment appeler le toomake sortante. Ce code utilise également un Bonjour de tooreturn site fournie par Twilio réponse de Twilio Markup Language (TwiML). Remplacez par vos valeurs hello **from_number** et **to_number** les numéros de téléphone et assurez-vous que vous avez vérifié hello **from_number** numéro de téléphone de votre compte Twilio avant d’exécuter un code hello.

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

Comme indiqué, ce code utilise un Bonjour de tooreturn TwiML réponse Twilio fournie par site. Vous pouvez utiliser votre propre hello tooprovide de site TwiML réponse ; Pour plus d’informations, consultez [comment tooProvide TwiML les réponses à partir de votre propre Site Web](#howto_provide_twiml_responses).

## <a id="howto_send_sms"></a>Procédure : envoi d'un message SMS
Hello suivant montre comment un message SMS à l’aide de toosend hello `TwilioRestClient` classe. Hello **from_number** numéro est fourni par Twilio pour évaluation comptes toosend de SMS. Hello **to_number** nombre doit être vérifié pour votre compte Twilio avant d’exécuter le code de hello.

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

## <a id="howto_provide_twiml_responses"></a>Procédure : envoi de réponses TwiML depuis votre propre site web
Lorsque votre application lance un appel de toohello Twilio API, Twilio enverra votre URL tooa demande attendu tooreturn une réponse TwiML. exemple Hello ci-dessus utilise les URL fournie par Twilio hello [http://twimlets.com/message][twimlet_message_url]. Comme TwiML est conçu pour être utilisé par Twilio, vous pouvez l’afficher dans votre navigateur. Par exemple, cliquez sur [http://twimlets.com/message] [ twimlet_message_url] toosee vide `<Response>` élément ; un autre exemple, cliquez sur [http://twimlets.com/message? Message % 5B0 %5, D = Hello % 20World] [ twimlet_message_url_hello_world] toosee un `<Response>` élément contenant un `<Say>` élément.)

Au lieu d’utiliser les URL fournie par Twilio hello, vous pouvez créer votre propre site qui renvoie des réponses HTTP. Vous pouvez créer le site de hello dans n’importe quel langage qui retourne les réponses XML ; Cette rubrique suppose que vous utiliserez hello toocreate de Python TwiML.

Hello exemples suivants produira une réponse TwiML indiquant que **Hello World** sur l’appel de hello.

Avec Flask :

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

Avec Django :

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

Comme vous pouvez le voir à partir de l’exemple hello ci-dessus, hello TwiML réponse est simplement un document XML. bibliothèque de Twilio Hello pour Python contient des classes qui génèrent TwiML pour vous. Hello exemple ci-dessous génère réponse équivalent de hello comme indiqué ci-dessus, mais utilise hello `twiml` module dans la bibliothèque de Twilio hello pour Python :

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

Pour plus d’informations sur TwiML, consultez la page [https://www.twilio.com/docs/api/twiml][twiml_reference].

Une fois que votre application Python configurer tooprovide TwiML réponses, utilisez hello les URL de l’application hello comme hello URL passée hello `client.calls.create` (méthode). Par exemple, si vous avez une application Web nommée **MyTwiML** tooan déployé Azure le service hébergé, vous pouvez utiliser des son url en tant que webhook, comme indiqué dans hello l’exemple suivant :

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

## <a id="AdditionalServices"></a>Utilisation de services Twilio supplémentaires
En outre toohello les exemples indiqués ici, que twilio propose des API basées sur le web qui vous pouvez utiliser des fonctionnalités Twilio tooleverage supplémentaires à partir de votre application Windows Azure. Pour plus d’informations, consultez hello [documentation de l’API de Twilio][twilio_api].

## <a id="NextSteps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello Hello Twilio service, suivez ces liens de toolearn plus :

* [Conseils de sécurité Twilio][twilio_security_guidelines]
* [Procédures et exemples de code Twilio][twilio_howtos]
* [Didacticiels de démarrage rapide Twilio][twilio_quickstarts]
* [Twilio sur GitHub][twilio_on_github]
* [Communiquer avec tooTwilio prise en charge][twilio_support]

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
