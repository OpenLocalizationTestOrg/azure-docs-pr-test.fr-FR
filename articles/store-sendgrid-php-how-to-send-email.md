---
title: aaaHow toouse hello SendGrid au service de messagerie (PHP) | Documents Microsoft
description: "Découvrez comment envoyer un courrier électronique avec hello SendGrid au service de messagerie sur Azure. Exemples de code écrits en PHP."
documentationcenter: php
services: 
manager: sendgrid
editor: mollybos
author: thinkingserious
ms.assetid: 51a9928a-4c9e-4b0a-aca8-9a408aeb6f47
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 10/30/2014
ms.author: elmer.thomas@sendgrid.com; erika.berkland@sendgrid.com; vibhork; matt.bernier@sendgrid.com
ms.openlocfilehash: 0076e56dc185cb8f52e629395e7d2c143cb5cfa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-sendgrid-email-service-from-php"></a>Comment tooUse hello SendGrid Service de messagerie à partir de PHP
Ce guide montre comment tooperform des tâches de programmation courantes avec hello SendGrid envoyer par courrier électronique service sur Azure. exemples de Hello sont écrits en PHP.
Hello scénarios abordés incluent **construction de messagerie**, **envoi de courrier électronique**, et **Ajout de pièces jointes**. Pour plus d’informations sur SendGrid et envoi de courrier électronique, consultez hello [étapes](#next-steps) section.

## <a name="what-is-hello-sendgrid-email-service"></a>Qu’est hello SendGrid au Service de messagerie ?
SendGrid est un [service de messagerie dans le cloud] qui fournit des fonctionnalités fiables en matière de [remise de courrier électronique transactionnelle], d'extensibilité et d'analyse en temps réel, ainsi que des API flexibles qui facilitent l'intégration personnalisée. Voici quelques scénarios courants en termes d'utilisation de SendGrid :

* Envoyer automatiquement des accusés de réception toocustomers
* Administration de listes de distribution pour un envoi mensuel de prospectus électroniques et d'offres spéciales aux clients
* Collecte de mesures en temps réel concernant des éléments tels que les messages électroniques bloqués et la réactivité vis-à-vis des clients
* Génération de rapports toohelp identifier les tendances
* Transfert des demandes des clients
* Notifications par courriers électroniques depuis votre application

Pour plus d’informations, consultez la page [https://sendgrid.com][https://sendgrid.com].

## <a name="create-a-sendgrid-account"></a>Création d'un compte SendGrid
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="using-sendgrid-from-your-php-application"></a>Utilisation de SendGrid à partir de votre application PHP
L'utilisation de SendGrid dans une application Azure PHP ne nécessite ni configuration spéciale, ni codage particulier. SendGrid étant un service, il est accessible dans hello exactement identique à partir d’une application cloud tel qu’il peut à partir d’une application sur site.

## <a name="how-to-send-an-email"></a>Envoi d'un message électronique
Vous pouvez envoyer par courrier électronique à l’aide de SMTP ou hello Web API fournie par SendGrid.

### <a name="smtp-api"></a>API SMTP
messagerie de toosend à l’aide de hello SendGrid SMTP API, utilisez *Swift Mailer*, une bibliothèque de base de composants pour l’envoi des messages électroniques à partir d’applications PHP. Vous pouvez télécharger hello *Swift Mailer* bibliothèque à partir de [http://swiftmailer.org/download] [ http://swiftmailer.org/download] v5.3.0 (utilisez [Composer] tooinstall Distribution rapide). Envoi de courrier électronique avec la bibliothèque de hello implique la création d’instances de la <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_Mailer</span>, et <span class="auto-style2">Swift\_Message </span> classes, en définissant les propriétés appropriées et en appelant le <span class="auto-style2">Swift\_Mailer::send</span> (méthode).

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create hello body of hello message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of hello email
      * If hello receiver is able tooview html emails then only hello html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
     $html = "<html>
           <head></head>
           <body>
               <p>Hi!<br>
                   How are you?<br>
               </p>
           </body>
           </html>";
     // This is your From email address
     $from = array('someone@example.com' => 'Name tooAppear');
     // Email recipients
     $too= array(
           'john@contoso.com'=>'Destination 1 Name',
           'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach hello body of hello email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
         // This will let us know how many users received this message
         echo 'Message sent out too'.$recipients.' users';
     }
     // something went wrong =(
     else
     {
         echo "Something went wrong - ";
         print_r($failures);
     }

### <a name="web-api"></a>API Web
Utilisation de PHP [curl fonction] [ curl function] toosend à l’aide de messagerie hello SendGrid Web API.

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $params = array(
          'api_user' => $user,
          'api_key' => $pass,
          'to' => 'john@contoso.com',
          'subject' => 'testing from curl',
          'html' => 'testing body',
          'text' => 'testing body',
          'from' => 'anna@contoso.com',
       );

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl toouse HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is hello body of hello POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not tooreturn headers, but do return hello response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

Web API de SendGrid est très similaire tooa API REST, s’il n’est pas réellement une API RESTful, car, dans la plupart des appels, à la fois obtenir et les verbes POST peuvent être utilisées indifféremment.

## <a name="how-to-add-an-attachment"></a>Ajout d'une pièce jointe
### <a name="smtp-api"></a>API SMTP
Envoi d’une pièce jointe à l’aide de hello SMTP API implique une ligne de code toohello exemple de script pour envoyer un courrier électronique avec Swift Mailer.

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create hello body of hello message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of hello email
      * If hello reciever is able tooview html emails then only hello html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
      $html = "<html>
          <head></head>
          <body>
             <p>Hi!<br>
                How are you?<br>
             </p>
          </body>
          </html>";

     // This is your From email address
     $from = array('someone@example.com' => 'Name tooAppear');

     // Email recipients
     $too= array(
          'john@contoso.com'=>'Destination 1 Name',
          'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach hello body of hello email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');
     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName("file_name"));

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
          // This will let us know how many users received this message
          echo 'Message sent out too'.$recipients.' users';
     }
     // something went wrong =(
     else
     {
          echo "Something went wrong - ";
          print_r($failures);
     }

la ligne de code supplémentaire Hello est comme suit :

     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName('file_name'));

Cette ligne de code appelle hello attach (méthode) sur le <span class="auto-style2">Swift\_Message</span> de l’objet et utilise la méthode statique <span class="auto-style2">fromPath</span> sur la <span class="auto-style2">Swift\_pièce jointe</span>tooget de classe et de joindre un message tooa de fichier.

### <a name="web-api"></a>API Web
Envoi d’une pièce jointe à l’aide des API Web de hello est très similaire toosending un courrier électronique à l’aide de hello API Web. Toutefois, notez que dans l’exemple hello qui suit, tableau de paramètres hello doit contenir cet élément :

    'files['.$fileName.']' => '@'.$filePath.'/'.$fileName

Exemple :

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $fileName = 'myfile';
     $filePath = dirname(__FILE__);

     $params = array(
         'api_user' => $user,
         'api_key' => $pass,
         'to' =>'john@contoso.com',
         'subject' => 'test of file sends',
         'html' => '<p> hello HTML </p>',
         'text' => 'hello plain text',
         'from' => 'anna@contoso.com',
         'files['.$fileName.']' => '@'.$filePath.'/'.$fileName
     );

     print_r($params);

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl toouse HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is hello body of hello POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not tooreturn headers, but do return hello response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a>Comment : utiliser des filtres Analytique, suivi et les pieds de page tooEnable
SendGrid fournit les fonctionnalités de messagerie supplémentaires via l’utilisation de hello de « filtres ». Il s’agit des paramètres qui peuvent être ajoutées e-mail tooan pour activer des fonctionnalités spécifiques telles que l’activation de suivi des clics, Google analytique, abonnement suivi des modifications, et ainsi de suite.

Filtres peuvent être appliqués tooa message en utilisant la propriété de filtres hello. Chaque filtre est spécifié par un hachage contenant des paramètres propres au filtre. L’exemple suivant active le filtre de pied de page hello et spécifie un message texte qui sera ajouté bas toohello d’e-mail hello.
Pour cet exemple, nous utiliserons la bibliothèque [sendgrid-php].
Utilisez [Composer] tooinstall bibliothèque :

    php composer.phar require sendgrid/sendgrid 2.1.1

Exemple :    

    <?php
     /*
      * This example is used for sendgrid-php V2.1.1 (https://github.com/sendgrid/sendgrid-php/tree/v2.1.1)
      */
     include "vendor/autoload.php";

     $email = new SendGrid\Email();
     // hello list of addresses this message will be sent to
     // [This list is used for sending multiple emails using just ONE request tooSendGrid]
     $toList = array('john@contoso.com', 'anna@contoso.com');

     // Specify hello names of hello recipients
     $nameList = array('Name 1', 'Name 2');

     // Used as an example of variable substitution
     $timeList = array('4 PM', '5 PM');

     // Set all of hello above variables
     $email->setTos($toList);
     $email->addSubstitution('-name-', $nameList);
     $email->addSubstitution('-time-', $timeList);

     // Specify that this is an initial contact message
     $email->addCategory("initial");

     // You can optionally setup individual filters here, in this example, we have
     // enabled hello footer filter
     $email->addFilter('footer', 'enable', 1);
     $email->addFilter('footer', "text/plain", "Thank you for your business");
     $email->addFilter('footer', "text/html", "Thank you for your business");

     // hello subject of your email
     $subject = 'Example SendGrid Email';

     // Where is this message coming from. For example, this message can be from
     // support@yourcompany.com, info@yourcompany.com
     $from = 'someone@example.com';

     // If you do not specify a sender list above, you can specifiy hello user here. If
     // a sender list IS specified above, this email address becomes irrelevant.
     $too= 'john@contoso.com';

     # Create hello body of hello message (a plain-text and an HTML version).
     # text is your plain-text email
     # html is your html version of hello email
     # if hello receiver is able tooview html emails then only hello html
     # email will be displayed

     /*
      * Note hello variable substitution here =)
      */
     $text = "
     Hello -name-,
     Thank you for your interest in our products. We have set up an appointment toocall you at -time- EST toodiscuss your needs in more detail.
     Regards,
     Fred";

     $html = "
     <html>
     <head></head>
     <body>
     <p>Hello -name-,<br>
     Thank you for your interest in our products. We have set up an appointment
     toocall you at -time- EST toodiscuss your needs in more detail.

     Regards,

     Fred<br>
     </p>
     </body>
     </html>";

     // set subject
     $email->setSubject($subject);

     // attach hello body of hello email
     $email->setFrom($from);
     $email->setHtml($html);
     $email->addTo($to);
     $email->setText($text);

     // Your SendGrid account credentials
     $username = 'sendgridusername@yourdomain.com';
     $password = 'example';

     // Create SendGrid object
     $sendgrid = new SendGrid($username, $password);

     // send message
     $response = $sendgrid->send($email);

     print_r($response);

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello Hello au service de messagerie de SendGrid, suivez ces liens de toolearn plus.

* Documentation de SendGrid : <https://sendgrid.com/docs>
* Bibliothèque PHP de SendGrid : <https://github.com/sendgrid/sendgrid-php>
* Offre spéciale SendGrid pour les clients Azure : <https://sendgrid.com/windowsazure.html>

Pour plus d’informations, consultez également hello [centre de développement PHP](/develop/php/).

[https://sendgrid.com]: https://sendgrid.com
[https://sendgrid.com/transactional-email/pricing]: https://sendgrid.com/transactional-email/pricing
[special offer]: https://www.sendgrid.com/windowsazure.html
[Packaging and Deploying PHP Applications for Azure]: http://msdn.microsoft.com/library/windowsazure/hh674499(v=VS.103).aspx
[http://swiftmailer.org/download]: http://swiftmailer.org/download
[curl function]: http://php.net/curl
[service de messagerie dans le cloud]: https://sendgrid.com/email-solutions
[remise de courrier électronique transactionnelle]: https://sendgrid.com/transactional-email
[sendgrid-php]: https://github.com/sendgrid/sendgrid-php/tree/v2.1.1
[Composer]: https://getcomposer.org/download/
