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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-php-application-on-azure"></a><span data-ttu-id="dbf81-104">Comment tooMake un Twilio à l’aide d’un appel téléphonique dans une Application PHP sur Azure</span><span class="sxs-lookup"><span data-stu-id="dbf81-104">How tooMake a Phone Call Using Twilio in a PHP Application on Azure</span></span>
<span data-ttu-id="dbf81-105">Hello suivant montre comment vous pouvez utiliser Twilio toomake un appel à partir d’une page web PHP hébergé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="dbf81-105">hello following example shows you how you can use Twilio toomake a call from a PHP web page hosted in Azure.</span></span> <span data-ttu-id="dbf81-106">application qui en résulte Hello invite utilisateur hello pour les valeurs de l’appel téléphonique, comme indiqué dans hello suivant capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="dbf81-106">hello resulting application will prompt hello user for phone call values, as shown in hello following screen shot.</span></span>

![Formulaire d'appel Azure avec Twilio et PHP][twilio_php]

<span data-ttu-id="dbf81-108">Éléments dont vous aurez besoin toodo hello code hello de toouse dans cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="dbf81-108">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="dbf81-109">Obtenir un compte Twilio et un jeton d’authentification auprès de la [console Twilio][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="dbf81-109">Acquire a Twilio account and authentication token from your [Twilio Console][twilio_console].</span></span> <span data-ttu-id="dbf81-110">tooget main Twilio, évaluer la tarification au [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="dbf81-110">tooget started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="dbf81-111">Vous pouvez vous inscrire pour obtenir un compte d’évaluation dans la page [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="dbf81-111">You can sign up for a trial account at [https://www.twilio.com/try-twilio][try_twilio].</span></span>
2. <span data-ttu-id="dbf81-112">Obtenir hello [bibliothèque Twilio pour PHP](https://github.com/twilio/twilio-php) ou l’installer en tant que package poire.</span><span class="sxs-lookup"><span data-stu-id="dbf81-112">Obtain hello [Twilio library for PHP](https://github.com/twilio/twilio-php) or install it as a PEAR package.</span></span> <span data-ttu-id="dbf81-113">Pour plus d’informations, consultez hello [fichier Lisez-moi](https://github.com/twilio/twilio-php/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="dbf81-113">For more information, see hello [readme file](https://github.com/twilio/twilio-php/blob/master/README.md).</span></span>
3. <span data-ttu-id="dbf81-114">Installer hello Azure SDK pour PHP.</span><span class="sxs-lookup"><span data-stu-id="dbf81-114">Install hello Azure SDK for PHP.</span></span> <span data-ttu-id="dbf81-115">Pour une vue d’ensemble de hello SDK et obtenir des instructions sur l’installation, consultez [définir hello Azure SDK pour PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span><span class="sxs-lookup"><span data-stu-id="dbf81-115">For an overview of hello SDK and instructions on installing it, see [Set up hello Azure SDK for PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="dbf81-116">Création d'un formulaire web pour passer un appel</span><span class="sxs-lookup"><span data-stu-id="dbf81-116">Create a web form for making a call</span></span>
<span data-ttu-id="dbf81-117">Hello suivant HTML de code montre comment toobuild une page web (**callform.html**) qui extrait des données de l’utilisateur d’un appel :</span><span class="sxs-lookup"><span data-stu-id="dbf81-117">hello following HTML code shows how toobuild a web page (**callform.html**) that retrieves user data for making a call:</span></span>

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

## <a name="create-hello-code-toomake-hello-call"></a><span data-ttu-id="dbf81-118">Créer l’appel de hello hello code toomake</span><span class="sxs-lookup"><span data-stu-id="dbf81-118">Create hello code toomake hello call</span></span>
<span data-ttu-id="dbf81-119">Hello suivant de code montre comment toobuild **makecall.php**, qui est appelé quand l’utilisateur de hello soumet écran hello affiché par **callform.html**.</span><span class="sxs-lookup"><span data-stu-id="dbf81-119">hello following code shows how toobuild **makecall.php**, which is called when hello user submits hello form displayed by **callform.html**.</span></span> <span data-ttu-id="dbf81-120">code Hello ci-dessous crée le message d’appel hello et génère l’appel de hello.</span><span class="sxs-lookup"><span data-stu-id="dbf81-120">hello code shown below creates hello call message and generates hello call.</span></span> <span data-ttu-id="dbf81-121">En outre, être toouse que votre compte Twilio et l’authentification de jeton à partir de hello [Twilio Console] [ twilio_console] au lieu de valeurs d’espace réservé hello affectés trop**$sid** et **$token** dans le code hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="dbf81-121">Also, be sure toouse your Twilio account and authentication token from hello [Twilio Console][twilio_console] instead of hello placeholder values assigned too**$sid** and **$token** in hello code below.</span></span>

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

<span data-ttu-id="dbf81-122">En outre toomaking hello appel, **makecall.php** affiche des métadonnées de l’appel, comme illustré dans l’image hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="dbf81-122">In addition toomaking hello call, **makecall.php** displays some call metadata, as is shown in hello image below.</span></span> <span data-ttu-id="dbf81-123">Pour plus d’informations sur les métadonnées de l’appel, consultez la page [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span><span class="sxs-lookup"><span data-stu-id="dbf81-123">For more information about call metadata, see [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span></span>

![Réponse d'appel Azure avec Twilio et PHP][twilio_php_response]

## <a name="run-hello-application"></a><span data-ttu-id="dbf81-125">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="dbf81-125">Run hello application</span></span>
<span data-ttu-id="dbf81-126">étape suivante de Hello est toodeploy votre tooAzure d’application des sites Web.</span><span class="sxs-lookup"><span data-stu-id="dbf81-126">hello next step is toodeploy your application tooAzure Websites.</span></span> <span data-ttu-id="dbf81-127">Hello articles suivants contiennent des informations hello pour la création d’un site Web et le déploiement de votre code avec Git, FTP ou WebMatrix (bien que toutes les informations de chaque article sont applique) :</span><span class="sxs-lookup"><span data-stu-id="dbf81-127">hello following articles contain hello information for creating a website and deploying your code with Git, FTP, or WebMatrix (though not all information in each article is relevant):</span></span>

* [<span data-ttu-id="dbf81-128">Création et déploiement d’un site web Azure PHP-MySQL avec Git</span><span class="sxs-lookup"><span data-stu-id="dbf81-128">Create a PHP-MySQL Azure Web Site and deploy using Git</span></span>](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [<span data-ttu-id="dbf81-129">Création et déploiement d’un site web Azure PHP-MySQL avec FTP</span><span class="sxs-lookup"><span data-stu-id="dbf81-129">Create a PHP-MySQL Azure Web Site and Deploy Using FTP</span></span>](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a><span data-ttu-id="dbf81-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dbf81-130">Next steps</span></span>
<span data-ttu-id="dbf81-131">Ce code a été fourni tooshow vous fonctionnalités de base à l’aide de Twilio dans PHP sur Azure.</span><span class="sxs-lookup"><span data-stu-id="dbf81-131">This code was provided tooshow you basic functionality using Twilio in PHP on Azure.</span></span> <span data-ttu-id="dbf81-132">Avant de déployer tooAzure en production, vous souhaiterez tooadd plus de gestion des erreurs ou d’autres fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="dbf81-132">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="dbf81-133">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="dbf81-133">For example:</span></span>

* <span data-ttu-id="dbf81-134">Au lieu d’utiliser un formulaire web, vous pourriez utiliser des objets BLOB de stockage Azure ou les numéros de téléphone toostore de base de données SQL et appeler le texte.</span><span class="sxs-lookup"><span data-stu-id="dbf81-134">Instead of using a web form, you could use Azure storage blobs or SQL Database toostore phone numbers and call text.</span></span> <span data-ttu-id="dbf81-135">Pour plus d’informations sur l’utilisation d’objets blob de stockage Azure dans PHP, consultez la page [Utilisation du stockage Azure dans les applications PHP][howto_blob_storage_php].</span><span class="sxs-lookup"><span data-stu-id="dbf81-135">For information about using Azure storage blobs in PHP, see [Using Azure Storage with PHP Applications][howto_blob_storage_php].</span></span> <span data-ttu-id="dbf81-136">Pour plus d’informations sur l’utilisation de la base de données SQL dans PHP, consultez la page [Utilisation de la base de données SQL avec les applications PHP][howto_sql_azure_php].</span><span class="sxs-lookup"><span data-stu-id="dbf81-136">For information about using SQL Database in PHP, see [Using SQL Database with PHP Applications][howto_sql_azure_php].</span></span>
* <span data-ttu-id="dbf81-137">Hello **makecall.php** code utilise l’URL fournie par Twilio ([http://twimlets.com/message][twimlet_message_url]) tooprovide une réponse Twilio Markup Language (TwiML) expliquant comment Twilio tooproceed avec l’appel de hello.</span><span class="sxs-lookup"><span data-stu-id="dbf81-137">hello **makecall.php** code uses Twilio-provided URL ([http://twimlets.com/message][twimlet_message_url]) tooprovide a Twilio Markup Language (TwiML) response that informs Twilio how tooproceed with hello call.</span></span> <span data-ttu-id="dbf81-138">Par exemple, hello TwiML retourné peut contenir un `<Say>` verbe qui résulte dans le texte est prononcée toohello destinataire de l’appel.</span><span class="sxs-lookup"><span data-stu-id="dbf81-138">For example, hello TwiML that is returned can contain a `<Say>` verb that results in text being spoken toohello call recipient.</span></span> <span data-ttu-id="dbf81-139">Au lieu d’utiliser l’URL fournie par Twilio de hello, vous pouvez générer demande de votre propre tooTwilio toorespond service ; Pour plus d’informations, consultez [comment tooUse Twilio pour la voix et de fonctionnalités SMS en PHP][howto_twilio_voice_sms_php].</span><span class="sxs-lookup"><span data-stu-id="dbf81-139">Instead of using hello Twilio-provided URL, you could build your own service toorespond tooTwilio's request; for more information, see [How tooUse Twilio for Voice and SMS Capabilities in PHP][howto_twilio_voice_sms_php].</span></span> <span data-ttu-id="dbf81-140">Pour plus d’informations sur TwiML, consultez la page [http://www.twilio.com/docs/api/twiml][twiml], et pour plus d’informations sur `<Say>` et sur les autres verbes Twilio, consultez la page [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="dbf81-140">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about `<Say>` and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="dbf81-141">Lisez les consignes de sécurité hello Twilio à [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="dbf81-141">Read hello Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="dbf81-142">Pour plus d’informations sur Twilio, consultez la page [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="dbf81-142">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="dbf81-143">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="dbf81-143">See Also</span></span>
* [<span data-ttu-id="dbf81-144">Comment tooUse Twilio pour les fonctionnalités de SMS en PHP et de la voix</span><span class="sxs-lookup"><span data-stu-id="dbf81-144">How tooUse Twilio for Voice and SMS Capabilities in PHP</span></span>](partner-twilio-php-how-to-use-voice-sms.md)

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
