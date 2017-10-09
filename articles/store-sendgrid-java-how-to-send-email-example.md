---
title: aaastore-sendgrid-Java-How-to-Send-email-example
description: "Comment toosend par courrier électronique à l’aide de SendGrid depuis Java dans un déploiement d’Azure"
services: 
documentationcenter: java
author: thinkingserious
manager: sendgrid
editor: mollybos
ms.assetid: af096a73-6985-4350-92e4-ce1722c8d72f
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 10/30/2014
ms.author: vibhork;dominic.may@sendgrid.com;elmer.thomas@sendgrid.com
ms.openlocfilehash: 51fde1fc71467f8252532b30d2f87856ec25067b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-java-in-an-azure-deployment"></a>Comment tooSend par courrier électronique à l’aide de SendGrid à partir de Java dans un déploiement d’Azure
Hello suivant montre comment vous pouvez utiliser des messages électroniques de toosend SendGrid à partir d’une page web hébergée dans Azure. application qui en résulte Hello invite utilisateur hello pour les valeurs de la messagerie, comme indiqué dans hello suivant capture d’écran.

![Formulaire de courrier électronique][emailform]

Hello obtenu par courrier électronique ressemblera toohello similaire après la capture d’écran.

![Message électronique][emailsent]

Éléments dont vous aurez besoin toodo hello code hello de toouse dans cette rubrique :

1. Obtenir hello javax.mail fichiers JAR, par exemple à partir de <http://www.oracle.com/technetwork/java/javamail/index.html>.
2. Ajoutez tooyour de fichiers JAR hello chemin d’accès de build Java.
3. Si vous utilisez Eclipse toocreate cette application Java, vous pouvez inclure des bibliothèques de SendGrid hello dans votre fichier de déploiement de l’application (WAR) à l’aide de la fonction d’assemblage déploiement d’Eclipse. Si vous n’utilisez pas Eclipse toocreate cette application Java, vérifiez les bibliothèques hello sont inclus dans hello même rôle Azure comme chemin de classe Java toohello application et ajout de votre application.

Vous devez également votre propre nom d’utilisateur SendGrid et le mot de passe, la messagerie de hello toobe toosend en mesure de. tooget main SendGrid, consultez [comment toosend par courrier électronique à l’aide de SendGrid depuis Java](store-sendgrid-java-how-to-send-email.md).

En outre, vous êtes familiarisé avec les informations de hello au [création d’une Application Hello World pour Azure dans Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), ou à d’autres techniques pour l’hébergement d’applications Java dans Azure si vous n’utilisez pas d’Eclipse, est fortement recommandé.

## <a name="create-a-web-form-for-sending-email"></a>Création d'un formulaire Web pour l'envoi de courriers électroniques
Hello suivant de code montre comment les données d’utilisateur de tooretrieve pour l’envoi de courrier électronique du formulaire toocreate un site web. Pour des raisons de ce contenu, un fichier JSP hello est nommé **emailform.jsp**.

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Email form</title>
    </head>
    <body>
     <p>Fill in all fields and click <b>Send this email</b>.</p>
     <br/>
      <form action="sendemail.jsp" method="post">
       <table>
         <tr>
           <td>To:</td>
           <td><input type="text" size=50 name="emailTo">
           </td>
         </tr>
         <tr>
           <td>From:</td>
           <td><input type="text" size=50 name="emailFrom">
           </td>
         </tr>
         <tr>
           <td>Subject:</td>
           <td><input type="text" size=100 name="emailSubject" value="My email subject">
           </td>
         </tr>
         <tr>
           <td>Text:</td>
           <td><input type="text" size=400 name="emailText" value="Hello,<p>This is my message.</p>Thank you." />
           </td>
         </tr>
         <tr>
           <td>SendGrid user name:</td>
           <td><input type="text" name="sendGridUser">
           </td>
         </tr>
         <tr>
           <td>SendGrid password:</td>
           <td><input type="password" name="sendGridPassword">
           </td>
         </tr>
         <tr>
           <td colspan=2><input type="submit" value="Send this email">
           </td>
         </tr>
       </table>
     </form>
     <br/>
    </body>
    </html>

## <a name="create-hello-code-toosend-hello-email"></a>Créer hello code toosend hello e-mail
Hello code suivant, qui est appelée lorsque vous complétez le formulaire de hello dans emailform.jsp, crée le message électronique de hello et l’envoie. Pour des raisons de ce contenu, un fichier JSP hello est nommé **sendemail.jsp**.

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" import="javax.activation.*, javax.mail.*, javax.mail.internet.*, java.util.Date, java.util.Properties" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Email processing happens here</title>
    </head>
    <body>
        <b>This is my send mail page.</b><p/>
     <%

     final String sendGridUser = request.getParameter("sendGridUser");
     final String sendGridPassword = request.getParameter("sendGridPassword");

     class SMTPAuthenticator extends Authenticator
     {
       public PasswordAuthentication getPasswordAuthentication()
       {
            String username = sendGridUser;
            String password = sendGridPassword;

            return new PasswordAuthentication(username, password);   
       }
     }
     try
     {

         // hello SendGrid SMTP server.
         String SMTP_HOST_NAME = "smtp.sendgrid.net";

         Properties properties;

         properties = new Properties();

         // Specify SMTP values.
         properties.put("mail.transport.protocol", "smtp");
         properties.put("mail.smtp.host", SMTP_HOST_NAME);
         properties.put("mail.smtp.port", 587);
         properties.put("mail.smtp.auth", "true");

         // Display hello email fields entered by hello user. 
         out.println("Value entered for email Subject: " + request.getParameter("emailSubject") + "<br/>");        
         out.println("Value entered for email      To: " + request.getParameter("emailTo") + "<br/>");
         out.println("Value entered for email    From: " + request.getParameter("emailFrom") + "<br/>");
         out.println("Value entered for email    Text: " + "<br/>" + request.getParameter("emailText") + "<br/>");

         // Create hello authenticator object.
         Authenticator authenticator = new SMTPAuthenticator();

         // Create hello mail session object.
         Session mailSession;
         mailSession = Session.getDefaultInstance(properties, authenticator);

         // Display debug information toostdout, useful when using the
         // compute emulator during development.
         mailSession.setDebug(true);

         // Create hello message and message part objects.
         MimeMessage message;
         Multipart multipart;
         MimeBodyPart messagePart; 

         message = new MimeMessage(mailSession);

         multipart = new MimeMultipart("alternative");
         messagePart = new MimeBodyPart();
         messagePart.setContent(request.getParameter("emailText"), "text/html");
         multipart.addBodyPart(messagePart);            

         // Specify hello email To, From, Subject and Content. 
         message.setFrom(new InternetAddress(request.getParameter("emailFrom")));
         message.addRecipient(Message.RecipientType.TO, new InternetAddress(request.getParameter("emailTo")));
         message.setSubject(request.getParameter("emailSubject")); 
         message.setContent(multipart);

         // Uncomment hello following if you want tooadd a footer.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"footer\": {\"settings\": {\"enable\":1,\"text/html\": \"<html>This is my <b>email footer</b>.</html>\"}}}}");

         // Uncomment hello following if you want tooenable click tracking.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"clicktrack\": {\"settings\": {\"enable\":1}}}}");

         Transport transport;
         transport = mailSession.getTransport();
         // Connect hello transport object.
         transport.connect();
         // Send hello message.
         transport.sendMessage(message,  message.getRecipients(Message.RecipientType.TO));
         // Close hello connection.
         transport.close();

        out.println("<p>Email processing completed.</p>");

     }
     catch (Exception e)
     {
         out.println("<p>Exception encountered: " + 
                            e.getMessage()     +
                            "</p>");   
     }
    %>

    </body>
    </html>

En outre toosending hello message électronique, emailform.jsp fournit un résultat pour l’utilisateur de hello ; par exemple, hello suivant capture d’écran :

![Résultat de l'envoi d'un courrier électronique][emailresult]

## <a name="next-steps"></a>Étapes suivantes
Déployer votre émulateur de calcul toohello application et dans un navigateur, exécutez emailform.jsp, entrez les valeurs sous forme de hello, cliquez sur **envoyer ce message électronique**, puis consultez les résultats dans sendemail.jsp.

Ce code a été fourni tooshow vous comment toouse SendGrid dans Java sur Azure. Avant de déployer tooAzure en production, vous souhaiterez tooadd plus de gestion des erreurs ou d’autres fonctionnalités. Par exemple : 

* Vous pouvez utiliser des objets BLOB de stockage Azure ou les adresses de messagerie de base de données SQL toostore et les messages électroniques, au lieu d’utiliser un formulaire web. Pour plus d’informations sur l’utilisation d’objets BLOB de stockage Azure dans Java, consultez [comment tooUse hello Service de stockage d’objets Blob à partir de Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/). Pour plus d'informations sur l'utilisation de la base de données SQL dans Java, consultez la page [Utilisation de bases de données SQL dans Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).
* Vous pouvez utiliser `RoleEnvironment.getConfigurationSettings` le nom d’utilisateur SendGrid tooretrieve hello et un mot de passe à partir des paramètres de configuration de votre déploiement, au lieu d’utiliser hello web form tooretrieve ces valeurs. Pour plus d’informations sur hello `RoleEnvironment` de classe, consultez [Using hello bibliothèque Runtime du Service Azure dans JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) et la documentation de package de Runtime du Service Azure hello à <http://dl.windowsazure.com/javadoc>.
* Pour plus d’informations sur l’utilisation de SendGrid dans Java, consultez [comment toosend par courrier électronique à l’aide de SendGrid depuis Java](store-sendgrid-java-how-to-send-email.md).

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
