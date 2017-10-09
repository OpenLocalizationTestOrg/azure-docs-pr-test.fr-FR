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
# <a name="how-toosend-email-using-sendgrid-from-java-in-an-azure-deployment"></a><span data-ttu-id="153c9-103">Comment tooSend par courrier électronique à l’aide de SendGrid à partir de Java dans un déploiement d’Azure</span><span class="sxs-lookup"><span data-stu-id="153c9-103">How tooSend Email Using SendGrid from Java in an Azure Deployment</span></span>
<span data-ttu-id="153c9-104">Hello suivant montre comment vous pouvez utiliser des messages électroniques de toosend SendGrid à partir d’une page web hébergée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="153c9-104">hello following example shows you how you can use SendGrid toosend emails from a web page hosted in Azure.</span></span> <span data-ttu-id="153c9-105">application qui en résulte Hello invite utilisateur hello pour les valeurs de la messagerie, comme indiqué dans hello suivant capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="153c9-105">hello resulting application will prompt hello user for email values, as shown in hello following screen shot.</span></span>

![Formulaire de courrier électronique][emailform]

<span data-ttu-id="153c9-107">Hello obtenu par courrier électronique ressemblera toohello similaire après la capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="153c9-107">hello resulting email will look similar toohello following screen shot.</span></span>

![Message électronique][emailsent]

<span data-ttu-id="153c9-109">Éléments dont vous aurez besoin toodo hello code hello de toouse dans cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="153c9-109">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="153c9-110">Obtenir hello javax.mail fichiers JAR, par exemple à partir de <http://www.oracle.com/technetwork/java/javamail/index.html>.</span><span class="sxs-lookup"><span data-stu-id="153c9-110">Obtain hello javax.mail JARs, for example from <http://www.oracle.com/technetwork/java/javamail/index.html>.</span></span>
2. <span data-ttu-id="153c9-111">Ajoutez tooyour de fichiers JAR hello chemin d’accès de build Java.</span><span class="sxs-lookup"><span data-stu-id="153c9-111">Add hello JARs tooyour Java build path.</span></span>
3. <span data-ttu-id="153c9-112">Si vous utilisez Eclipse toocreate cette application Java, vous pouvez inclure des bibliothèques de SendGrid hello dans votre fichier de déploiement de l’application (WAR) à l’aide de la fonction d’assemblage déploiement d’Eclipse.</span><span class="sxs-lookup"><span data-stu-id="153c9-112">If you are using Eclipse toocreate this Java application, you can include hello SendGrid libraries in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="153c9-113">Si vous n’utilisez pas Eclipse toocreate cette application Java, vérifiez les bibliothèques hello sont inclus dans hello même rôle Azure comme chemin de classe Java toohello application et ajout de votre application.</span><span class="sxs-lookup"><span data-stu-id="153c9-113">If you are not using Eclipse toocreate this Java application, ensure hello libraries are included within hello same Azure role as your Java application, and added toohello class path of your application.</span></span>

<span data-ttu-id="153c9-114">Vous devez également votre propre nom d’utilisateur SendGrid et le mot de passe, la messagerie de hello toobe toosend en mesure de.</span><span class="sxs-lookup"><span data-stu-id="153c9-114">You must also have your own SendGrid username and password, toobe able toosend hello email.</span></span> <span data-ttu-id="153c9-115">tooget main SendGrid, consultez [comment toosend par courrier électronique à l’aide de SendGrid depuis Java](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="153c9-115">tooget started with SendGrid, see [How toosend email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

<span data-ttu-id="153c9-116">En outre, vous êtes familiarisé avec les informations de hello au [création d’une Application Hello World pour Azure dans Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), ou à d’autres techniques pour l’hébergement d’applications Java dans Azure si vous n’utilisez pas d’Eclipse, est fortement recommandé.</span><span class="sxs-lookup"><span data-stu-id="153c9-116">Additionally, familiarity with hello information at [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-sending-email"></a><span data-ttu-id="153c9-117">Création d'un formulaire Web pour l'envoi de courriers électroniques</span><span class="sxs-lookup"><span data-stu-id="153c9-117">Create a web form for sending email</span></span>
<span data-ttu-id="153c9-118">Hello suivant de code montre comment les données d’utilisateur de tooretrieve pour l’envoi de courrier électronique du formulaire toocreate un site web.</span><span class="sxs-lookup"><span data-stu-id="153c9-118">hello following code shows how toocreate a web form tooretrieve user data for sending email.</span></span> <span data-ttu-id="153c9-119">Pour des raisons de ce contenu, un fichier JSP hello est nommé **emailform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="153c9-119">For purposes of this content, hello JSP file is named **emailform.jsp**.</span></span>

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

## <a name="create-hello-code-toosend-hello-email"></a><span data-ttu-id="153c9-120">Créer hello code toosend hello e-mail</span><span class="sxs-lookup"><span data-stu-id="153c9-120">Create hello code toosend hello email</span></span>
<span data-ttu-id="153c9-121">Hello code suivant, qui est appelée lorsque vous complétez le formulaire de hello dans emailform.jsp, crée le message électronique de hello et l’envoie.</span><span class="sxs-lookup"><span data-stu-id="153c9-121">hello following code, which is called when you complete hello form in emailform.jsp, creates hello email message and sends it.</span></span> <span data-ttu-id="153c9-122">Pour des raisons de ce contenu, un fichier JSP hello est nommé **sendemail.jsp**.</span><span class="sxs-lookup"><span data-stu-id="153c9-122">For purposes of this content, hello JSP file is named **sendemail.jsp**.</span></span>

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

<span data-ttu-id="153c9-123">En outre toosending hello message électronique, emailform.jsp fournit un résultat pour l’utilisateur de hello ; par exemple, hello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="153c9-123">In addition toosending hello email, emailform.jsp provides a result for hello user; an example is hello following screen shot:</span></span>

![Résultat de l'envoi d'un courrier électronique][emailresult]

## <a name="next-steps"></a><span data-ttu-id="153c9-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="153c9-125">Next steps</span></span>
<span data-ttu-id="153c9-126">Déployer votre émulateur de calcul toohello application et dans un navigateur, exécutez emailform.jsp, entrez les valeurs sous forme de hello, cliquez sur **envoyer ce message électronique**, puis consultez les résultats dans sendemail.jsp.</span><span class="sxs-lookup"><span data-stu-id="153c9-126">Deploy your application toohello compute emulator and within a browser run emailform.jsp, enter values in hello form, click **Send this email**, and then see results in sendemail.jsp.</span></span>

<span data-ttu-id="153c9-127">Ce code a été fourni tooshow vous comment toouse SendGrid dans Java sur Azure.</span><span class="sxs-lookup"><span data-stu-id="153c9-127">This code was provided tooshow you how toouse SendGrid in Java on Azure.</span></span> <span data-ttu-id="153c9-128">Avant de déployer tooAzure en production, vous souhaiterez tooadd plus de gestion des erreurs ou d’autres fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="153c9-128">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="153c9-129">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="153c9-129">For example:</span></span> 

* <span data-ttu-id="153c9-130">Vous pouvez utiliser des objets BLOB de stockage Azure ou les adresses de messagerie de base de données SQL toostore et les messages électroniques, au lieu d’utiliser un formulaire web.</span><span class="sxs-lookup"><span data-stu-id="153c9-130">You could use Azure storage blobs or SQL Database toostore email addresses and email messages, instead of using a web form.</span></span> <span data-ttu-id="153c9-131">Pour plus d’informations sur l’utilisation d’objets BLOB de stockage Azure dans Java, consultez [comment tooUse hello Service de stockage d’objets Blob à partir de Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span><span class="sxs-lookup"><span data-stu-id="153c9-131">For information about using Azure storage blobs in Java, see [How tooUse hello Blob Storage Service from Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span></span> <span data-ttu-id="153c9-132">Pour plus d'informations sur l'utilisation de la base de données SQL dans Java, consultez la page [Utilisation de bases de données SQL dans Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span><span class="sxs-lookup"><span data-stu-id="153c9-132">For information about using SQL Database in Java, see [Using SQL Database in Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span></span>
* <span data-ttu-id="153c9-133">Vous pouvez utiliser `RoleEnvironment.getConfigurationSettings` le nom d’utilisateur SendGrid tooretrieve hello et un mot de passe à partir des paramètres de configuration de votre déploiement, au lieu d’utiliser hello web form tooretrieve ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="153c9-133">You could use `RoleEnvironment.getConfigurationSettings` tooretrieve hello SendGrid username and password from your deployment's configuration settings, instead of using hello web form tooretrieve those values.</span></span> <span data-ttu-id="153c9-134">Pour plus d’informations sur hello `RoleEnvironment` de classe, consultez [Using hello bibliothèque Runtime du Service Azure dans JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) et la documentation de package de Runtime du Service Azure hello à <http://dl.windowsazure.com/javadoc>.</span><span class="sxs-lookup"><span data-stu-id="153c9-134">For information about hello `RoleEnvironment` class, see [Using hello Azure Service Runtime Library in JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) and hello Azure Service Runtime package documentation at <http://dl.windowsazure.com/javadoc>.</span></span>
* <span data-ttu-id="153c9-135">Pour plus d’informations sur l’utilisation de SendGrid dans Java, consultez [comment toosend par courrier électronique à l’aide de SendGrid depuis Java](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="153c9-135">For more information about using SendGrid in Java, see [How toosend email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
