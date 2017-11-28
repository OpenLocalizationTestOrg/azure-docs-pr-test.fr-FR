---
title: store-sendgrid-java-how-to-send-email-example
description: "Envoi de courriers électroniques à l'aide de SendGrid à partir de Java dans un déploiement Azure"
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
ms.openlocfilehash: d80d7d9c54bad12a4d26d8623eeccdf9bc2a743a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-send-email-using-sendgrid-from-java-in-an-azure-deployment"></a><span data-ttu-id="b3f05-103">Envoi de courriers électroniques à l'aide de SendGrid à partir de Java dans un déploiement Azure</span><span class="sxs-lookup"><span data-stu-id="b3f05-103">How to Send Email Using SendGrid from Java in an Azure Deployment</span></span>
<span data-ttu-id="b3f05-104">L'exemple qui suit montre comment vous pouvez utiliser SendGrid pour envoyer des courriers électroniques depuis une page Web hébergée sur Azure.</span><span class="sxs-lookup"><span data-stu-id="b3f05-104">The following example shows you how you can use SendGrid to send emails from a web page hosted in Azure.</span></span> <span data-ttu-id="b3f05-105">L'application finale demande à l'utilisateur les valeurs du courrier électronique, comme illustré dans la capture d'écran qui suit.</span><span class="sxs-lookup"><span data-stu-id="b3f05-105">The resulting application will prompt the user for email values, as shown in the following screen shot.</span></span>

![Formulaire de courrier électronique][emailform]

<span data-ttu-id="b3f05-107">Le courrier électronique obtenu est semblable à la capture d'écran suivante.</span><span class="sxs-lookup"><span data-stu-id="b3f05-107">The resulting email will look similar to the following screen shot.</span></span>

![Message électronique][emailsent]

<span data-ttu-id="b3f05-109">Pour utiliser le code de cette rubrique, vous devrez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b3f05-109">You'll need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="b3f05-110">Obtenez les JAR javax.mail, par exemple depuis <http://www.oracle.com/technetwork/java/javamail/index.html>.</span><span class="sxs-lookup"><span data-stu-id="b3f05-110">Obtain the javax.mail JARs, for example from <http://www.oracle.com/technetwork/java/javamail/index.html>.</span></span>
2. <span data-ttu-id="b3f05-111">Ajoutez les JAR à votre chemin de build Java.</span><span class="sxs-lookup"><span data-stu-id="b3f05-111">Add the JARs to your Java build path.</span></span>
3. <span data-ttu-id="b3f05-112">Si vous utilisez Eclipse pour créer cette application Java, vous pouvez ajouter les bibliothèques SendGrid à votre fichier WAR de déploiement d'application à l'aide de la fonction d'assembly de déploiement d'Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b3f05-112">If you are using Eclipse to create this Java application, you can include the SendGrid libraries in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="b3f05-113">Si vous n'utilisez pas Eclipse pour créer cette application Java, assurez-vous que les bibliothèques sont incluses dans le même rôle Azure que votre application Java et qu'elles sont ajoutées au chemin de classe de votre application.</span><span class="sxs-lookup"><span data-stu-id="b3f05-113">If you are not using Eclipse to create this Java application, ensure the libraries are included within the same Azure role as your Java application, and added to the class path of your application.</span></span>

<span data-ttu-id="b3f05-114">Vous devez également avoir vos propres nom d'utilisateur et mot de passe SendGrid pour pouvoir envoyer le courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="b3f05-114">You must also have your own SendGrid username and password, to be able to send the email.</span></span> <span data-ttu-id="b3f05-115">Pour vos premiers pas avec SendGrid, consultez la page [Envoi de courriers électroniques à l'aide de SendGrid depuis Java](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="b3f05-115">To get started with SendGrid, see [How to send email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

<span data-ttu-id="b3f05-116">En outre, il est recommandé de bien connaître les informations de la page [Création d'une application Hello World pour Azure dans Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944)ou bien d'autres techniques d'hébergement pour les applications Java dans Azure si vous n'utilisez pas Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b3f05-116">Additionally, familiarity with the information at [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-sending-email"></a><span data-ttu-id="b3f05-117">Création d'un formulaire Web pour l'envoi de courriers électroniques</span><span class="sxs-lookup"><span data-stu-id="b3f05-117">Create a web form for sending email</span></span>
<span data-ttu-id="b3f05-118">Le code qui suit présente la conception d'un formulaire Web qui extrait les données des utilisateurs pour envoyer des courriers électroniques.</span><span class="sxs-lookup"><span data-stu-id="b3f05-118">The following code shows how to create a web form to retrieve user data for sending email.</span></span> <span data-ttu-id="b3f05-119">Dans le cadre du présent contenu, le fichier JSP est nommé **emailform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="b3f05-119">For purposes of this content, the JSP file is named **emailform.jsp**.</span></span>

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

## <a name="create-the-code-to-send-the-email"></a><span data-ttu-id="b3f05-120">Création du code pour envoyer le courrier électronique</span><span class="sxs-lookup"><span data-stu-id="b3f05-120">Create the code to send the email</span></span>
<span data-ttu-id="b3f05-121">Le code suivant, qui est appelé lorsque vous remplissez le formulaire dans emailform.jsp, crée le courrier électronique et l'envoie.</span><span class="sxs-lookup"><span data-stu-id="b3f05-121">The following code, which is called when you complete the form in emailform.jsp, creates the email message and sends it.</span></span> <span data-ttu-id="b3f05-122">Dans le cadre du présent contenu, le fichier JSP est nommé **sendemail.jsp**.</span><span class="sxs-lookup"><span data-stu-id="b3f05-122">For purposes of this content, the JSP file is named **sendemail.jsp**.</span></span>

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

         // The SendGrid SMTP server.
         String SMTP_HOST_NAME = "smtp.sendgrid.net";

         Properties properties;

         properties = new Properties();

         // Specify SMTP values.
         properties.put("mail.transport.protocol", "smtp");
         properties.put("mail.smtp.host", SMTP_HOST_NAME);
         properties.put("mail.smtp.port", 587);
         properties.put("mail.smtp.auth", "true");

         // Display the email fields entered by the user. 
         out.println("Value entered for email Subject: " + request.getParameter("emailSubject") + "<br/>");        
         out.println("Value entered for email      To: " + request.getParameter("emailTo") + "<br/>");
         out.println("Value entered for email    From: " + request.getParameter("emailFrom") + "<br/>");
         out.println("Value entered for email    Text: " + "<br/>" + request.getParameter("emailText") + "<br/>");

         // Create the authenticator object.
         Authenticator authenticator = new SMTPAuthenticator();

         // Create the mail session object.
         Session mailSession;
         mailSession = Session.getDefaultInstance(properties, authenticator);

         // Display debug information to stdout, useful when using the
         // compute emulator during development.
         mailSession.setDebug(true);

         // Create the message and message part objects.
         MimeMessage message;
         Multipart multipart;
         MimeBodyPart messagePart; 

         message = new MimeMessage(mailSession);

         multipart = new MimeMultipart("alternative");
         messagePart = new MimeBodyPart();
         messagePart.setContent(request.getParameter("emailText"), "text/html");
         multipart.addBodyPart(messagePart);            

         // Specify the email To, From, Subject and Content. 
         message.setFrom(new InternetAddress(request.getParameter("emailFrom")));
         message.addRecipient(Message.RecipientType.TO, new InternetAddress(request.getParameter("emailTo")));
         message.setSubject(request.getParameter("emailSubject")); 
         message.setContent(multipart);

         // Uncomment the following if you want to add a footer.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"footer\": {\"settings\": {\"enable\":1,\"text/html\": \"<html>This is my <b>email footer</b>.</html>\"}}}}");

         // Uncomment the following if you want to enable click tracking.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"clicktrack\": {\"settings\": {\"enable\":1}}}}");

         Transport transport;
         transport = mailSession.getTransport();
         // Connect the transport object.
         transport.connect();
         // Send the message.
         transport.sendMessage(message,  message.getRecipients(Message.RecipientType.TO));
         // Close the connection.
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

<span data-ttu-id="b3f05-123">En plus d'envoyer le courrier électronique, emailform.jsp fournit un résultat à l'utilisateur. La capture d'écran suivante présente un exemple :</span><span class="sxs-lookup"><span data-stu-id="b3f05-123">In addition to sending the email, emailform.jsp provides a result for the user; an example is the following screen shot:</span></span>

![Résultat de l'envoi d'un courrier électronique][emailresult]

## <a name="next-steps"></a><span data-ttu-id="b3f05-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b3f05-125">Next steps</span></span>
<span data-ttu-id="b3f05-126">Déployez votre application sur l'émulateur de calcul, puis dans un navigateur, exécutez emailform.jsp, entrez les valeurs dans le formulaire, cliquez sur **Send this email**, puis consultez les résultats dans sendemail.jsp.</span><span class="sxs-lookup"><span data-stu-id="b3f05-126">Deploy your application to the compute emulator and within a browser run emailform.jsp, enter values in the form, click **Send this email**, and then see results in sendemail.jsp.</span></span>

<span data-ttu-id="b3f05-127">Ce code vous est fourni afin de vous montrer comment utiliser SendGrid dans Java sur Azure.</span><span class="sxs-lookup"><span data-stu-id="b3f05-127">This code was provided to show you how to use SendGrid in Java on Azure.</span></span> <span data-ttu-id="b3f05-128">Avant d'effectuer le déploiement de production sur Azure, vous pouvez ajouter d'autres fonctionnalités telles que la gestion des erreurs.</span><span class="sxs-lookup"><span data-stu-id="b3f05-128">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="b3f05-129">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b3f05-129">For example:</span></span> 

* <span data-ttu-id="b3f05-130">Vous pouvez utiliser des objets blob de stockage Azure ou une base de données SQL pour stocker les adresses de messagerie et les courriers électroniques, plutôt que d'utiliser un formulaire Web.</span><span class="sxs-lookup"><span data-stu-id="b3f05-130">You could use Azure storage blobs or SQL Database to store email addresses and email messages, instead of using a web form.</span></span> <span data-ttu-id="b3f05-131">Pour plus d'informations sur l'utilisation d'objets blob de stockage Azure dans Java, consultez la page [Utilisation du service de stockage d'objets blob de Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span><span class="sxs-lookup"><span data-stu-id="b3f05-131">For information about using Azure storage blobs in Java, see [How to Use the Blob Storage Service from Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span></span> <span data-ttu-id="b3f05-132">Pour plus d'informations sur l'utilisation de la base de données SQL dans Java, consultez la page [Utilisation de bases de données SQL dans Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span><span class="sxs-lookup"><span data-stu-id="b3f05-132">For information about using SQL Database in Java, see [Using SQL Database in Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span></span>
* <span data-ttu-id="b3f05-133">Vous pouvez utiliser `RoleEnvironment.getConfigurationSettings` pour extraire le nom d'utilisateur et le mot de passe SendGrid à partir des paramètres de configuration de votre déploiement, au lieu d'utiliser un formulaire Web.</span><span class="sxs-lookup"><span data-stu-id="b3f05-133">You could use `RoleEnvironment.getConfigurationSettings` to retrieve the SendGrid username and password from your deployment's configuration settings, instead of using the web form to retrieve those values.</span></span> <span data-ttu-id="b3f05-134">Pour en savoir plus sur la classe `RoleEnvironment`, consultez la rubrique [Utilisation de la bibliothèque Azure Service Runtime en JSP](http://msdn.microsoft.com/library/windowsazure/hh690948), ainsi que la documentation du package Azure Service Runtime sur <http://dl.windowsazure.com/javadoc>.</span><span class="sxs-lookup"><span data-stu-id="b3f05-134">For information about the `RoleEnvironment` class, see [Using the Azure Service Runtime Library in JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) and the Azure Service Runtime package documentation at <http://dl.windowsazure.com/javadoc>.</span></span>
* <span data-ttu-id="b3f05-135">Pour plus d'informations sur l'utilisation de SendGrid dans Java, consultez la page [Envoi de courriers électroniques à l'aide de SendGrid depuis Java](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="b3f05-135">For more information about using SendGrid in Java, see [How to send email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
