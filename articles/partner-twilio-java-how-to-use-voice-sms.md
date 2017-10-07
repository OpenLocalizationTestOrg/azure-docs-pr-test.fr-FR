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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-java"></a>Comment tooUse Twilio pour la voix et les fonctionnalités de SMS dans Java
Ce guide montre comment tooperform des tâches de programmation courantes avec hello Twilio API de service sur Azure. scénarios de Hello couvertes incluent un appel téléphonique et envoi d’un message de Service SMS (Short Message). Pour plus d’informations sur Twilio et à l’aide de la voix et SMS dans vos applications, consultez hello [étapes](#NextSteps) section.

## <a id="WhatIs"></a>Présentation de Twilio
Twilio est une API de service web de téléphonie qui vous permet d’utiliser votre langages web existants et les voix toobuild de compétences et les applications de SMS. Twilio est un service tiers, et non une fonctionnalité Azure ni un produit Microsoft.

**Twilio vocal** permet à votre toomake d’applications et de recevoir des appels téléphoniques. **Twilio SMS** permet à votre toomake d’applications et de recevoir des messages SMS. **Client twilio sur** tooenable la communication vocale via les connexions Internet, y compris les connexions mobiles permet à vos applications.

## <a id="Pricing"></a>Tarification de Twilio et offres spéciales
Des informations sur les prix de Twilio sont disponibles dans la page [Tarification de Twilio][twilio_pricing]. Les clients Azure reçoivent une [offre spéciale][special_offer] : un crédit gratuit de 1 000 SMS ou de 1 000 minutes d’appel en entrée. toosign pour cette offre ou obtenir plus d’informations, visitez [http://ahoy.twilio.com/azure][special_offer].

## <a id="Concepts"></a>Concepts
Hello Twilio API est une API RESTful qui fournit la voix et fonctionnalités SMS pour les applications. Les bibliothèques clientes sont disponibles dans plusieurs langues : pour en obtenir la liste, consultez la page [Bibliothèques de l’API Twilio][twilio_libraries].

Les principaux aspects du hello Twilio API sont Twilio verbes et Twilio Markup Language (TwiML).

### <a id="Verbs"></a>Verbes Twilio
Hello API se sert de Twilio verbes ; par exemple, hello  **&lt;prononcer&gt;**  verbe fait en sorte que Twilio tooaudibly remettre un message sur un appel.

Hello Voici une liste de verbes de Twilio.

* **&lt;Accès à distance&gt;**: se connecte phone de tooanother hello appelant.
* **&lt;Collecter des&gt;**: collecte les chiffres entrés sur le clavier de téléphone hello.
* **&lt;Hangup&gt;** : met fin à un appel.
* **&lt;Play&gt;** : lit un fichier audio.
* **&lt;File d’attente&gt;**: ajouter la file d’attente de tooa hello des appelants.
* **&lt;Pause&gt;** : patiente silencieusement pendant un nombre déterminé de secondes.
* **&lt;Enregistrement&gt;**: enregistre la voix de l’appelant hello et retourne une URL d’un fichier contenant un enregistrement de hello.
* **&lt;Rediriger&gt;**: transfère le contrôle d’un appel ou un SMS toohello TwiML à une autre URL.
* **&lt;Rejeter&gt;**: rejette un entrant appeler tooyour Twilio nombre sans vous de facturation.
* **&lt;Par exemple&gt;**: toospeech texte convertit effectuée sur un appel.
* **&lt;Sms&gt;** : envoie un SMS.

### <a id="TwiML"></a>TwiML
TwiML est un ensemble d’instructions basé sur XML en fonction de verbes Twilio hello qui informent Twilio de façon tooprocess un appel ou un SMS.

Par exemple, hello suivant TwiML permet de convertir le texte hello **Hello World !** toospeech.

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

Lorsque votre application appelle hello Twilio API, un des paramètres d’API hello est hello URL qui renvoie la réponse de TwiML hello. À des fins de développement, vous pouvez utiliser l’URL fournie par Twilio tooprovide hello TwiML les réponses employées par vos applications. Vous pourriez également héberger vos réponses de TwiML URL tooproduce hello et une autre option consiste à toouse hello **TwiMLResponse** objet.

Pour plus d’informations sur les verbes Twilio, leurs attributs et le langage TwiML, consultez la page [TwiML][twiml]. Pour plus d’informations sur hello Twilio API, consultez [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Créer un compte Twilio
Lorsque vous êtes prêt tooget un compte de Twilio, inscrivez-vous dans [essayez de Twilio][try_twilio]. Vous pouvez commencer avec un compte gratuit, avant de le mettre à niveau ultérieurement.

Lorsque vous créez un compte Twilio, vous recevez un ID de compte et un jeton d'authentification. Les deux seront les appels d’API de Twilio toomake nécessaires. tooprevent non autorisé à accéder à tooyour compte, de sécuriser votre jeton d’authentification. Votre ID de compte et l’authentification jeton peuvent être consultés à hello [Twilio Console][twilio_console], dans hello champs **SID de compte** et **dujetond’authentification**, respectivement.

## <a id="create_app"></a>Création d’une application Java
1. Obtenir hello Twilio JAR et l’ajouter tooyour chemin d’accès et votre assembly de déploiement WAR de build Java. À [https://github.com/twilio/twilio-java][twilio_java], vous pouvez télécharger hello GitHub sources et créer vos propres JAR ou télécharger le fichier JAR prédéfini (avec ou sans dépendances).
2. Assurez-vous de votre JDK **cacerts** keystore contient le certificat d’autorité de certification Equifax Secure hello avec 67:CB:9 d’empreinte digitale MD5 D : C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (numéro de série hello est 35:DE:F4:CF et hello SHA1 empreinte digitale est D2:32:09:AD:23:D3:14:23:21:74:E4:0 D : 7F:9 D : 62:13:97:86:63:3A). Il s’agit hello autorité de certification pour hello [https://api.twilio.com] [ twilio_api_service] service, qui est appelée lors de l’utilisation de Twilio APIs. Pour plus d’informations sur la capacité de votre JDK **cacerts** keystore contient le certificat d’autorité de certification approprié hello, consultez [Ajout d’un magasin de certificats d’autorité de certification Java de toohello certificat][add_ca_cert].

Obtenir des instructions détaillées pour l’utilisation de la bibliothèque cliente de Twilio hello pour Java sont disponibles sur [comment tooMake un Twilio à l’aide d’un appel téléphonique dans une Application Java sur Azure][howto_phonecall_java].

## <a id="configure_app"></a>Configurez des bibliothèques de votre Application tooUse Twilio
Dans votre code, vous pouvez ajouter **importer** instructions haut hello de vos fichiers sources pour hello Twilio packages ou des classes vous souhaitez toouse dans votre application.

Pour les fichiers sources Java :

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

Pour les fichiers sources JSP (Java Server Page) :

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
Selon les packages de Twilio ou les classes, vous souhaitez toouse, votre **importer** instructions peuvent être différents.

## <a id="howto_make_call"></a>Procédure : passer un appel sortant
Hello suivant montre comment toomake sortante appeler à l’aide de hello **appeler** classe. Ce code utilise également un Bonjour de tooreturn site fournie par Twilio réponse de Twilio Markup Language (TwiML). Remplacez par vos valeurs hello **de** et **à** les numéros de téléphone et assurez-vous que vous vérifiez hello **à partir de** numéro de téléphone de votre code hello de Twilio compte toorunning préalable.

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

Pour plus d’informations sur les paramètres de hello passés dans toohello **Call.creator** méthode, consultez [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].

Comme indiqué, ce code utilise un Bonjour de tooreturn TwiML réponse Twilio fournie par site. Vous pouvez utiliser votre propre hello tooprovide de site TwiML réponse ; Pour plus d’informations, consultez [comment tooProvide réponses TwiML dans une Application Java sur Azure](#howto_provide_twiml_responses).

## <a id="howto_send_sms"></a>Procédure : envoi d'un message SMS
Hello suivant montre comment un message SMS à l’aide de toosend hello **Message** classe. Hello **de** nombre, **4155992671**, est fournie par Twilio pour évaluation comptes toosend de SMS. Hello **à** nombre doit être vérifié pour votre code de hello Twilio compte toorunning préalable.

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

Pour plus d’informations sur les paramètres de hello passés dans toohello **Message.creator** méthode, consultez [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].

## <a id="howto_provide_twiml_responses"></a>Procédure : envoi de réponses TwiML depuis votre propre site web
Lorsque votre application démarre un toohello appel API de Twilio, par exemple via hello **CallCreator.create** méthode, Twilio enverra votre URL tooa demande tooreturn attendu une réponse TwiML. exemple Hello ci-dessus utilise les URL fournie par Twilio hello [http://twimlets.com/message][twimlet_message_url]. (TwiML est conçu pour une utilisation par les services Web, vous pouvez afficher hello TwiML dans votre navigateur. Par exemple, cliquez sur [http://twimlets.com/message] [ twimlet_message_url] toosee vide  **&lt;réponse&gt;**  élément ; un autre exemple, cliquez sur [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21] [ twimlet_message_url_hello_world] toosee un  **&lt;réponse&gt;**  élément contenant un  **&lt;prononcer &gt;**  élément.)

Au lieu d’utiliser les URL fournie par Twilio hello, vous pouvez créer votre propre site URL qui renvoie des réponses HTTP. Vous pouvez créer le site de hello dans n’importe quel langage qui retourne des réponses HTTP ; Cette rubrique suppose que vous allez héberger URL hello dans une page JSP.

Hello suivant page JSP qui en résulte dans une réponse TwiML indiquant que **Hello World !** appel de hello.

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

Bonjour suivant des résultats de la page JSP dans une réponse TwiML indiquant que du texte, a plusieurs pauses et affiche des informations sur la version de l’API de Twilio hello et le nom du rôle Azure hello.

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

Hello **ApiVersion** paramètre n’est disponible dans les demandes de voix Twilio (pas de demandes SMS). paramètres de demande disponible toosee hello pour Twilio vocal et les demandes SMS, consultez <https://www.twilio.com/docs/api/twiml/twilio_request> et <https://www.twilio.com/docs/api/twiml/sms/twilio_request >, respectivement. Hello **RoleName** variable d’environnement n’est disponible dans le cadre d’un déploiement d’Azure. (Si vous souhaitez que les variables d’environnement personnalisées tooadd afin qu’ils peut être récupérés à partir de **System.getenv**, consultez la section de variables d’environnement hello à [divers paramètres de Configuration de rôle] [misc_role_config_settings].)

Une fois que vous avez votre page JSP configurer tooprovide TwiML réponses, utilisez des URL de hello de page JSP hello comme hello URL passée hello **Call.creator** (méthode). Par exemple, si vous avez une application Web nommée MyTwiML déployé tooan Azure le service hébergé et nom hello de page JSP hello est mytwiml.jsp, hello URL peut être passé trop**Call.creator** comme indiqué dans les éléments suivants de hello :

```java
    // Declare tooand From numbers and hello URL of your JSP page
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

Une autre option pour répondre avec TwiML est via hello **VoiceResponse** (classe), qui est disponible dans hello **com.twilio.twiml** package.

Pour plus d’informations sur l’utilisation de Twilio dans Azure avec Java, consultez [comment tooMake un Twilio à l’aide d’un appel téléphonique dans une Application Java sur Azure][howto_phonecall_java].

## <a id="AdditionalServices"></a>Utilisation de services Twilio supplémentaires
En outre toohello les exemples indiqués ici, que twilio propose des API basées sur le web qui vous pouvez utiliser des fonctionnalités Twilio tooleverage supplémentaires à partir de votre application Windows Azure. Pour plus d’informations, consultez hello [documentation de l’API de Twilio][twilio_api_documentation].

## <a id="NextSteps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello Hello Twilio service, suivez ces liens de toolearn plus :

* [Conseils de sécurité Twilio][twilio_security_guidelines]
* [Procédures et exemples de code Twilio][twilio_howtos]
* [Didacticiels de démarrage rapide Twilio][twilio_quickstarts]
* [Twilio sur GitHub][twilio_on_github]
* [Communiquer avec tooTwilio prise en charge][twilio_support]

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
