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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-from-azure"></a>Comment toouse Twilio pour la voix et les fonctionnalités SMS à partir de Azure
Ce guide montre comment tooperform des tâches de programmation courantes avec hello Twilio API de service sur Azure. scénarios de Hello couvertes incluent un appel téléphonique et envoi d’un message de Service SMS (Short Message). Pour plus d’informations sur Twilio et à l’aide de la voix et SMS dans vos applications, consultez hello [étapes](#NextSteps) section.

## <a id="WhatIs"></a>Présentation de Twilio
Twilio est futures hello de communications professionnelles de mise sous tension, l’activation de voix de tooembed les développeurs, VoIP et dans les applications de messagerie. La virtualisation toute infrastructure nécessaires dans un environnement en nuage, global, exposant via la plateforme de hello Twilio communications API. Les applications sont toobuild simple et évolutive. Tirez parti de la souplesse du paiement à l’utilisation et de la fiabilité du cloud.

**Twilio vocal** permet à votre toomake d’applications et de recevoir des appels téléphoniques. **Twilio SMS** Active toosend de vos applications et de recevoir des messages SMS. **Client twilio sur** vous permet d’appels de VoIP toomake à partir de n’importe quel téléphone, tablette ou un navigateur et prend en charge WebRTC.

## <a id="Pricing"></a>Tarification de Twilio et offres spéciales
Les clients Azure reçoivent une [offre spéciale](http://www.twilio.com/azure)de 10 $ en crédit Twilio lorsqu'ils mettent à niveau leur compte Twilio. Ce Twilio crédit peut être appliqué tooany l’utilisation de Twilio (10 $ crédit équivalent toosending jusqu'à 1 000 messages SMS et la réception des too1000 entrants voix minutes, selon emplacement hello de votre destination de nombre et de message ou d’appel téléphonique). Profitez de ce crédit Twilio et démarrez en consultant la page [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).

Twilio est un service de paiement à l'utilisation. Il n’y a pas de frais d’entrée et vous pouvez fermer votre compte quand vous le souhaitez. Pour plus d'informations, consultez la page [Tarification de Twilio](http://www.twilio.com/voice/pricing).

## <a id="Concepts"></a>Concepts
Hello Twilio API est une API RESTful qui fournit la voix et fonctionnalités SMS pour les applications. Les bibliothèques clientes sont disponibles dans plusieurs langues : pour en obtenir la liste, consultez la page [Bibliothèques de l’API Twilio][twilio_libraries].

Les principaux aspects du hello Twilio API sont Twilio verbes et Twilio Markup Language (TwiML).

### <a id="Verbs"></a>Verbes Twilio
Hello API se sert de Twilio verbes ; par exemple, hello  **&lt;prononcer&gt;**  verbe fait en sorte que Twilio tooaudibly remettre un message sur un appel.

Hello Voici une liste de verbes de Twilio.  En savoir plus sur hello autres verbes et les fonctionnalités via [documentation de langage de balisage Twilio](http://www.twilio.com/docs/api/twiml).

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

### <a id="TwiML"></a>TwiML
TwiML est un ensemble d’instructions basé sur XML en fonction de verbes Twilio hello qui informent Twilio de façon tooprocess un appel ou un SMS.

Par exemple, hello suivant TwiML permet de convertir le texte hello **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

Lorsque votre application appelle hello Twilio API, un des paramètres d’API hello est hello URL qui renvoie la réponse de TwiML hello. À des fins de développement, vous pouvez utiliser l’URL fournie par Twilio tooprovide hello TwiML les réponses employées par vos applications. Vous pourriez également héberger vos réponses de TwiML URL tooproduce hello et une autre option consiste à toouse hello **TwiMLResponse** objet.

Pour plus d’informations sur les verbes Twilio, leurs attributs et le langage TwiML, consultez la page [TwiML][twiml]. Pour plus d’informations sur hello Twilio API, consultez [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Créer un compte Twilio
Lorsque vous êtes prêt tooget un compte de Twilio, inscrivez-vous dans [essayez de Twilio][try_twilio]. Vous pouvez commencer avec un compte gratuit, avant de le mettre à niveau ultérieurement.

Lorsque vous créez un compte Twilio, vous recevez un ID de compte et un jeton d'authentification. Les deux seront les appels d’API de Twilio toomake nécessaires. tooprevent non autorisé à accéder à tooyour compte, de sécuriser votre jeton d’authentification. Votre ID de compte et l’authentification jeton peuvent être consultés à hello [page de compte Twilio][twilio_account], dans hello champs **SID de compte** et **dujetond’authentification**, respectivement.

## <a id="create_app"></a>Créer une application Microsoft Azure
Une application Azure qui héberge une application Twilio n'est pas différente d'une autre application Azure. Ajout d’une bibliothèque de Twilio .NET hello et de configurer hello rôle toouse hello Twilio les bibliothèques .NET.
Pour plus d’informations sur la création d’un projet Azure initial, consultez la page [Création d’un projet Azure avec Visual Studio][vs_project].

## <a id="configure_app"></a>Configurez des bibliothèques de votre Application toouse Twilio
Twilio fournit un ensemble de bibliothèques .NET d’assistance qui encapsulent les divers aspects de Twilio tooprovide facilement et simple toointeract avec hello API REST de Twilio et Twilio Client toogenerate TwiML réponses.

Twilio offre cinq bibliothèques destinées aux développeurs .NET :
Bibliothèque|Description
---|---
Twilio.API|Hello Twilio bibliothèque principale qui encapsule hello API REST de Twilio dans une bibliothèque .NET conviviale. Cette bibliothèque est disponible pour .NET, Silverlight et Windows Phone 7.
Twilio.TwiML|Fournit un balisage de TwiML toogenerate .NET manière conviviale.
Twilio.MVC|Pour les développeurs utilisant ASP.NET MVC, cette bibliothèque inclut TwilioController, TwiML ActionResult et un attribut de validation de demande.
Twilio.WebMatrix|Pour les développeurs utilisant l'outil de développement WebMatrix gratuit de Microsoft, cette bibliothèque contient les aides à la syntaxe Razor pour différentes actions Twilio.
Twilio.Client.Capability|Contient le Générateur de jetons de capacité hello pour une utilisation avec hello Twilio Client JavaScript SDK.

Notez que toutes les bibliothèques nécessitent .NET 3.5, Silverlight 4 ou Windows Phone 7 ou version ultérieure.

les exemples de Hello fournies dans ce guide utilisent la bibliothèque de Twilio.API hello.

Hello bibliothèques peuvent être [installé à l’aide d’extension hello du Gestionnaire de package NuGet](http://www.twilio.com/docs/csharp/install) too2015 disponibles pour Visual Studio 2010.  code source Hello est hébergé sur [GitHub][twilio_github_repo], qui inclut un site Wiki qui contient une documentation complète pour l’utilisation de bibliothèques de hello.

Par défaut, Microsoft Visual Studio 2010 installe la version 1.2 de NuGet. L’installation des bibliothèques de Twilio hello requiert la version 1.6 de NuGet ou une version ultérieure. Pour plus d’informations sur l’installation ou la mise à jour de NuGet, consultez le site [http://nuget.org/][nuget].

> [!NOTE]
> version la plus récente hello tooinstall de NuGet, vous devez d’abord désinstaller hello de version chargée à l’aide de hello Gestionnaire d’extensions Visual Studio. toodo par conséquent, vous devez exécuter Visual Studio en tant qu’administrateur. Sinon, le bouton de désinstaller hello est désactivée.
>
>

### <a id="use_nuget"></a>tooadd hello Twilio bibliothèques tooyour Visual Studio un projet :
1. Ouvrez votre solution dans Visual Studio.
2. Cliquez avec le bouton droit sur **Références**.
3. Cliquez sur **Gérer les packages NuGet...**
4. Cliquez sur **En ligne**.
5. Dans la zone en ligne de recherche hello, tapez *twilio*.
6. Cliquez sur **installer** sur le package de Twilio hello.

## <a id="howto_make_call"></a>Procédure : passer un appel sortant
Hello suivant montre comment toomake sortante appeler à l’aide de hello **CallResource** classe. Ce code utilise également un Bonjour de tooreturn site fournie par Twilio réponse de Twilio Markup Language (TwiML). Remplacez par vos valeurs hello **à** et **de** les numéros de téléphone et assurez-vous que vous vérifiez hello **de** numéro de téléphone de votre compte Twilio avant d’exécuter le code de hello.

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

Pour plus d’informations sur les paramètres de hello passés dans toohello **CallResource.Create** méthode, consultez [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].

Comme indiqué, ce code utilise un Bonjour de tooreturn TwiML réponse Twilio fournie par site. Vous pouvez utiliser votre propre hello tooprovide de site TwiML réponse. Pour plus d’informations, consultez [Envoi de réponses TwiML à partir de votre propre site web](#howto_provide_twiml_responses).

## <a id="howto_send_sms"></a>Procédure : envoi d'un message SMS
Hello capture d’écran suivante montre comment un message SMS à l’aide de toosend hello **MessageResource** classe. Hello **de** numéro est fourni par Twilio pour évaluation comptes toosend de SMS. Hello **à** nombre doit être vérifié pour votre compte Twilio avant d’exécuter le code de hello.

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

## <a id="howto_provide_twiml_responses"></a>Procédure : envoi de réponses TwiML depuis votre propre site Web
Lorsque votre application démarre, par exemple, un toohello d’appels API de Twilio - via hello **CallResource.Create** méthode - Twilio votre URL tooan demande tooreturn attendu envoie une réponse TwiML. exemple Hello dans [Comment : effectuer un appel sortant](#howto_make_call) utilise hello URL fournie par Twilio [http://twimlets.com/message] [ twimlet_message_url] réponse de hello tooreturn.

> [!NOTE]
> TwiML est conçu pour une utilisation par les services web, vous pouvez afficher hello TwiML dans votre navigateur. Par exemple, cliquez sur [http://twimlets.com/message] [ twimlet_message_url] toosee vide &lt;réponse&gt; élément ; un autre exemple, cliquez sur [http://twimlets.com/message ? Message % 5B0 %5, D = Hello % 20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee un &lt;réponse&gt; élément contenant un &lt;prononcer&gt; élément.
>
>

Au lieu d’utiliser les URL fournie par Twilio hello, vous pouvez créer votre propre site URL qui renvoie des réponses HTTP. Vous pouvez créer le site de hello dans n’importe quel langage qui renvoie des réponses HTTP. Cette rubrique suppose que vous allez héberger URL hello à partir d’un gestionnaire générique ASP.NET.

Hello suivant gestionnaire ASP.NET développe une réponse TwiML indiquant que **Hello World** sur l’appel de hello.

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
    
Comme vous pouvez le voir à partir de l’exemple hello ci-dessus, hello TwiML réponse est simplement un document XML. bibliothèque de Twilio.TwiML Hello contient des classes qui génèrent TwiML pour vous. Hello exemple ci-dessous génère réponse équivalent de hello comme indiqué ci-dessus, mais utilise hello **VoiceResponse** classe.

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

Pour plus d'informations sur TwiML, consultez la page [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).

Une fois que vous avez configuré une réponse de TwiML tooprovide moyen, vous pouvez passer ce toohello URL **CallResource.Create** (méthode). Par exemple, si vous disposez d’une application web nommée MyTwiML déployé tooan service cloud Azure, et hello le nom de votre gestionnaire d’ASP.NET est mytwiml.ashx, hello URL peut être transmise trop**CallResource.Create** comme indiqué dans hello suivant de code exemple :

    // This sample uses hello sandbox number provided by Twilio toomake hello call.
    // Place hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

Pour plus d’informations sur l’utilisation de Twilio sur Azure avec ASP.NET, consultez [comment toomake un appel téléphonique dans un rôle web sur Azure à l’aide de Twilio][howto_phonecall_dotnet].

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
