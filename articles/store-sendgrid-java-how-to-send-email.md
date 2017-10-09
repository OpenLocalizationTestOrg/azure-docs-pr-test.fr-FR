---
title: aaaHow toouse hello SendGrid au service de messagerie (Java) | Documents Microsoft
description: "Découvrez comment envoyer un courrier électronique avec hello SendGrid au service de messagerie sur Azure. Exemples de code écrits en Java."
services: 
documentationcenter: java
author: thinkingserious
manager: sendgrid
editor: mollybos
ms.assetid: cc75c43e-ede9-492b-98c2-9147fcb92c21
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 10/30/2014
ms.author: elmer.thomas@sendgrid.com; erika.berkland@sendgrid.com; vibhork
ms.openlocfilehash: 542ce0003e94fc8f5551487d5a3cd6f75d27e8cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-java"></a>Comment tooSend par courrier électronique à l’aide de SendGrid depuis Java
Ce guide montre comment tooperform des tâches de programmation courantes avec le SendGrid de messagerie service sur Azure. exemples de Hello sont écrits en Java. Hello scénarios abordés incluent **construction de messagerie**, **envoi de courrier électronique**, **Ajout de pièces jointes**, **à l’aide de filtres**et **mise à jour des propriétés**. Pour plus d’informations sur SendGrid et envoi de courrier électronique, consultez hello [étapes](#next-steps) section.

## <a name="what-is-hello-sendgrid-email-service"></a>Qu’est hello SendGrid au Service de messagerie ?
SendGrid est un [service de messagerie dans le cloud] qui fournit des fonctionnalités fiables en matière de [remise de courrier électronique transactionnelle], d'extensibilité et d'analyse en temps réel, ainsi que des API flexibles qui facilitent l'intégration personnalisée. Voici quelques scénarios courants en termes d'utilisation de SendGrid :

* Envoyer automatiquement des accusés de réception toocustomers
* Administration de listes de distribution pour un envoi mensuel de prospectus électroniques et d'offres spéciales aux clients
* Collecte de mesures en temps réel concernant des éléments tels que les messages électroniques bloqués et la réactivité vis-à-vis des clients
* Génération de rapports toohelp identifier les tendances
* Transfert des demandes des clients
* Notifications par courriers électroniques depuis votre application

Pour plus d'informations, consultez la page <http://sendgrid.com>.

## <a name="create-a-sendgrid-account"></a>Création d'un compte SendGrid
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-hello-javaxmail-libraries"></a>Comment : utiliser les bibliothèques javax.mail hello
Obtenir les bibliothèques javax.mail hello, par exemple à partir de <http://www.oracle.com/technetwork/java/javamail> et les importer dans votre code. À un niveau élevé, hello processus pour l’utilisation de hello javax.mail bibliothèque toosend par courrier électronique à l’aide de SMTP est toodo hello suivant :

1. Spécifier des valeurs de SMTP hello, y compris le serveur SMTP hello, c'est-à-dire pour SendGrid smtp.sendgrid.net.

```
        import java.util.Properties;
        import javax.activation.*;
        import javax.mail.*;
        import javax.mail.internet.*;

        public class MyEmailer {
           private static final String SMTP_HOST_NAME = "smtp.sendgrid.net";
           private static final String SMTP_AUTH_USER = "your_sendgrid_username";
           private static final String SMTP_AUTH_PWD = "your_sendgrid_password";

           public static void main(String[] args) throws Exception{
               new MyEmailer().SendMail();
           }

           public void SendMail() throws Exception
           {
              Properties properties = new Properties();
                 properties.put("mail.transport.protocol", "smtp");
                 properties.put("mail.smtp.host", SMTP_HOST_NAME);
                 properties.put("mail.smtp.port", 587);
                 properties.put("mail.smtp.auth", "true");
                 // …
```

1. Étendre hello *javax.mail.Authenticator* (classe) et dans votre implémentation de la *getPasswordAuthentication* (méthode), retourner votre nom d’utilisateur SendGrid et le mot de passe.  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. Créez une session de messagerie électronique authentifiée via un objet *javax.mail.Session* .  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. Créez votre message et spécifiez des valeurs pour **À**, **De**, **Objet**. Cela est illustré par hello [comment faire : créer un message électronique](#how-to-create-an-email) section.
4. Envoyer le message de type hello via un *javax.mail.Transport* objet. Cela est illustré par hello [Comment : envoyer un courrier électronique] [Comment : envoyer un courrier électronique] section.

## <a name="how-to-create-an-email"></a>Création d'un message électronique
Hello Voici comment toospecify les valeurs pour un message électronique.

    MimeMessage message = new MimeMessage(mailSession);
    Multipart multipart = new MimeMultipart("alternative");
    BodyPart part1 = new MimeBodyPart();
    part1.setText("Hello, Your Contoso order has shipped. Thank you, John");
    BodyPart part2 = new MimeBodyPart();
    part2.setContent(
        "<p>Hello,</p>
        <p>Your Contoso order has <b>shipped</b>.</p>
        <p>Thank you,<br>John</br></p>",
        "text/html");
    multipart.addBodyPart(part1);
    multipart.addBodyPart(part2);
    message.setFrom(new InternetAddress("john@contoso.com"));
    message.addRecipient(Message.RecipientType.TO,
       new InternetAddress("someone@example.com"));
    message.setSubject("Your recent order");
    message.setContent(multipart);

## <a name="how-to-send-an-email"></a>Envoi d'un message électronique
Hello ci-dessous illustre comment toosend un message électronique.

    Transport transport = mailSession.getTransport();
    // Connect hello transport object.
    transport.connect();
    // Send hello message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close hello connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a>Ajout d'une pièce jointe
Hello de code suivant vous montre comment tooadd une pièce jointe.

    // Local file name and path.
    String attachmentName = "myfile.zip";
    String attachmentPath = "c:\\myfiles\\";
    MimeBodyPart attachmentPart = new MimeBodyPart();
    // Specify hello local file tooattach.
    DataSource source = new FileDataSource(attachmentPath + attachmentName);
    attachmentPart.setDataHandler(new DataHandler(source));
    // This example uses hello local file name as hello attachment name.
    // They could be different if you prefer.
    attachmentPart.setFileName(attachmentName);
    multipart.addBodyPart(attachmentPart);

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a>Comment : utiliser les filtres analytique, suivi et les pieds de page tooenable
SendGrid fournit les fonctionnalités de messagerie supplémentaires via l’utilisation de hello de *filtres*. Il s’agit des paramètres qui peuvent être ajoutées e-mail tooan pour activer des fonctionnalités spécifiques telles que l’activation de suivi des clics, Google analytique, abonnement suivi des modifications, et ainsi de suite. Pour obtenir une liste exhaustive des filtres, consultez la page [Paramètres de filtre][Filter Settings].

* Hello Voici comment filtrer les tooinsert un pied de page qui génère du texte HTML qui apparaît au bas de hello de messagerie hello envoyé.

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* Parmi les exemples de filtres, on peut également citer le suivi des clics. Supposons que votre texte du courrier électronique contient un lien hypertexte, telles que hello suivant et que vous souhaitez tootrack hello cliquez sur taux :

      messagePart.setContent(
          "Hello,
          <p>This is hello body of hello message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* tooenable hello sur le suivi des modifications, hello utilisation suivante du code :

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a>Mise à jour des propriétés d'un message électronique
Certaines propriétés de messagerie peuvent être remplacées à l’aide de  **définir*propriété*** ou être ajoutées à l’aide de  **ajouter*propriété***.

Par exemple, toospecify **ReplyTo** adresses, utilisez hello qui suit :

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

tooadd un **Cc** suivant de hello destinataire, utilisez :

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a>Utilisation de services SendGrid supplémentaires
SendGrid propose des API basées sur le web que vous pouvez utiliser les fonctionnalités de SendGrid tooleverage supplémentaires à partir de votre application Windows Azure. Pour plus d’informations, consultez hello [documentation sur les API SendGrid][SendGrid API documentation].

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello Hello au service de messagerie de SendGrid, suivez ces liens de toolearn plus.

* Exemple qui illustre l’utilisation de SendGrid dans un déploiement d’Azure : [comment toosend par courrier électronique à l’aide de SendGrid depuis Java dans un déploiement d’Azure](store-sendgrid-java-how-to-send-email-example.md)
* Kit de développement logiciel (SDK) SendGrid Java : <https://sendgrid.com/docs/Code_Examples/java.html>
* Documentation de l’API SendGrid : <https://sendgrid.com/docs/API_Reference/index.html>
* Offre spéciale SendGrid pour les clients Azure : <https://sendgrid.com/windowsazure.html>

[http://sendgrid.com]: https://sendgrid.com
[http://sendgrid.com/pricing.html]: http://sendgrid.com/pricing.html
[http://www.sendgrid.com/azure.html]: https://www.sendgrid.com/windowsazure.html
[http://sendgrid.com/features]: https://sendgrid.com/features
[http://www.oracle.com/technetwork/java/javamail]: http://www.oracle.com/technetwork/java/javamail/index.html
[Filter Settings]: https://sendgrid.com/docs/API_Reference/Web_API/filter_settings.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/index.html
[http://sendgrid.com/azure.html]: https://sendgrid.com/windowsazure.html
[service de messagerie dans le cloud]: https://sendgrid.com/email-solutions
[remise de courrier électronique transactionnelle]: https://sendgrid.com/transactional-email
