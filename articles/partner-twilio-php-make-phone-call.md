---
title: "aaaHow toomake un appel téléphonique à partir de Twilio (PHP) | Documents Microsoft"
description: "Découvrez comment toomake un appel téléphonique et envoyer un SMS de message avec le service de l’API de Twilio hello sur Azure. Les exemples concernent une applications PHP."
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 44e35adc-be06-4700-beee-8c9e2c20c540
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: e6fecc345bf9ae787d14d533bd8d96b175c2453b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-php-application-on-azure"></a>Comment tooMake un Twilio à l’aide d’un appel téléphonique dans une Application PHP sur Azure
Hello suivant montre comment vous pouvez utiliser Twilio toomake un appel à partir d’une page web PHP hébergé dans Azure. application qui en résulte Hello invite utilisateur hello pour les valeurs de l’appel téléphonique, comme indiqué dans hello suivant capture d’écran.

![Formulaire d'appel Azure avec Twilio et PHP][twilio_php]

Éléments dont vous aurez besoin toodo hello code hello de toouse dans cette rubrique :

1. Obtenir un compte Twilio et un jeton d’authentification auprès de la [console Twilio][twilio_console]. tooget main Twilio, évaluer la tarification au [http://www.twilio.com/pricing][twilio_pricing]. Vous pouvez vous inscrire pour obtenir un compte d’évaluation dans la page [https://www.twilio.com/try-twilio][try_twilio].
2. Obtenir hello [bibliothèque Twilio pour PHP](https://github.com/twilio/twilio-php) ou l’installer en tant que package poire. Pour plus d’informations, consultez hello [fichier Lisez-moi](https://github.com/twilio/twilio-php/blob/master/README.md).
3. Installer hello Azure SDK pour PHP. Pour une vue d’ensemble de hello SDK et obtenir des instructions sur l’installation, consultez [définir hello Azure SDK pour PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)

## <a name="create-a-web-form-for-making-a-call"></a>Création d'un formulaire web pour passer un appel
Hello suivant HTML de code montre comment toobuild une page web (**callform.html**) qui extrait des données de l’utilisateur d’un appel :

```html
<!DOCTYPE html>
<html>
<head>
  <title>Automated call form</title>
</head>
<body>
  <h1>Automated Call Form</h1>
  <p>Fill in all fields and click <b>Make this call</b>.</p>
  <form action="makecall.php" method="post">
    <table>
      <tr>
        <td>To:</td>
        <td><input name="callTo" size="50" type="text" value=""></td>
      </tr>
      <tr>
        <td>From:</td>
        <td><input name="callFrom" size="50" type="text" value=""></td>
      </tr>
      <tr>
        <td>Call message:</td>
        <td><input name="callText" size="100" type="text" value="Hello. This is hello call text. Good bye."></td>
      </tr>
      <tr>
        <td colspan="2"><input type="submit" value="Make this call"></td>
      </tr>
    </table>
  </form><br>
</body>
</html>
```

## <a name="create-hello-code-toomake-hello-call"></a>Créer l’appel de hello hello code toomake
Hello suivant de code montre comment toobuild **makecall.php**, qui est appelé quand l’utilisateur de hello soumet écran hello affiché par **callform.html**. code Hello ci-dessous crée le message d’appel hello et génère l’appel de hello. En outre, être toouse que votre compte Twilio et l’authentification de jeton à partir de hello [Twilio Console] [ twilio_console] au lieu de valeurs d’espace réservé hello affectés trop**$sid** et **$token** dans le code hello ci-dessous.

```html
<html>
<head><title>Making call...</title></head>
<body>
<p>Your call is being made.</p>

<?php
require_once 'path/to/vendor/autoload.php';

$sid   = "your_account_sid";
$token = "your_authentication_token";

$from_number = $_POST['callFrom']; // Calls must be made from a registered Twilio number.
$to_number   = $_POST['callTo'];
$message     = $_POST['callText'];

$client = new Twilio\Rest\Client($sid, $token);

$call = $client->calls->create(
            $to_number,
            $from_number,
            array('url' => http://twimlets.com/message?Message=' . urlencode($message))
        );

echo "Call status: " . $call->status . "<br />";
echo "URI resource: " . $call->uri . "<br />";
?>
</body>
</html>
```

En outre toomaking hello appel, **makecall.php** affiche des métadonnées de l’appel, comme illustré dans l’image hello ci-dessous. Pour plus d’informations sur les métadonnées de l’appel, consultez la page [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].

![Réponse d'appel Azure avec Twilio et PHP][twilio_php_response]

## <a name="run-hello-application"></a>Exécutez l’application hello
étape suivante de Hello est toodeploy votre tooAzure d’application des sites Web. Hello articles suivants contiennent des informations hello pour la création d’un site Web et le déploiement de votre code avec Git, FTP ou WebMatrix (bien que toutes les informations de chaque article sont applique) :

* [Création et déploiement d’un site web Azure PHP-MySQL avec Git](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [Création et déploiement d’un site web Azure PHP-MySQL avec FTP](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a>Étapes suivantes
Ce code a été fourni tooshow vous fonctionnalités de base à l’aide de Twilio dans PHP sur Azure. Avant de déployer tooAzure en production, vous souhaiterez tooadd plus de gestion des erreurs ou d’autres fonctionnalités. Par exemple :

* Au lieu d’utiliser un formulaire web, vous pourriez utiliser des objets BLOB de stockage Azure ou les numéros de téléphone toostore de base de données SQL et appeler le texte. Pour plus d’informations sur l’utilisation d’objets blob de stockage Azure dans PHP, consultez la page [Utilisation du stockage Azure dans les applications PHP][howto_blob_storage_php]. Pour plus d’informations sur l’utilisation de la base de données SQL dans PHP, consultez la page [Utilisation de la base de données SQL avec les applications PHP][howto_sql_azure_php].
* Hello **makecall.php** code utilise l’URL fournie par Twilio ([http://twimlets.com/message][twimlet_message_url]) tooprovide une réponse Twilio Markup Language (TwiML) expliquant comment Twilio tooproceed avec l’appel de hello. Par exemple, hello TwiML retourné peut contenir un `<Say>` verbe qui résulte dans le texte est prononcée toohello destinataire de l’appel. Au lieu d’utiliser l’URL fournie par Twilio de hello, vous pouvez générer demande de votre propre tooTwilio toorespond service ; Pour plus d’informations, consultez [comment tooUse Twilio pour la voix et de fonctionnalités SMS en PHP][howto_twilio_voice_sms_php]. Pour plus d’informations sur TwiML, consultez la page [http://www.twilio.com/docs/api/twiml][twiml], et pour plus d’informations sur `<Say>` et sur les autres verbes Twilio, consultez la page [http://www.twilio.com/docs/api/twiml/say][twilio_say].
* Lisez les consignes de sécurité hello Twilio à [https://www.twilio.com/docs/security][twilio_docs_security].

Pour plus d’informations sur Twilio, consultez la page [https://www.twilio.com/docs][twilio_docs].

## <a name="see-also"></a>Voir aussi
* [Comment tooUse Twilio pour les fonctionnalités de SMS en PHP et de la voix](partner-twilio-php-how-to-use-voice-sms.md)

[twilio_console]: https://www.twilio.com/console
[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/docs/api
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified
[twimlet_message_url]: http://twimlets.com/message
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api_service]: http://api.twilio.com
[build_php_azure_app]: http://azurephp.interoperabilitybridges.com/articles/build-and-deploy-a-windows-azure-php-application
[howto_twilio_voice_sms_php]: partner-twilio-php-how-to-use-voice-sms.md
[howto_blob_storage_php]: http://azure.microsoft.com/documentation/articles/storage-php-how-to-use-blobs/
[howto_sql_azure_php]: http://azure.microsoft.com/documentation/articles/sql-database-php-how-to-use/
[twilio_call_properties]: https://www.twilio.com/docs/api/rest/call#instance-properties
[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_php]: ./media/partner-twilio-php-make-phone-call/WA_TwilioPHPCallForm.jpg
[twilio_php_response]: ./media/partner-twilio-php-make-phone-call/WA_TwilioPHPMakeCall.jpg
[website-git]: ./web-sites/web-sites-php-mysql-deploy-use-git.md
[website-ftp]: ./web-sites/web-sites-php-mysql-deploy-use-ftp.md
[twilio_php_github]: https://github.com/twilio/twilio-php
