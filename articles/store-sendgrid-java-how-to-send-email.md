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
# <a name="how-toosend-email-using-sendgrid-from-java"></a><span data-ttu-id="b01d0-104">Comment tooSend par courrier électronique à l’aide de SendGrid depuis Java</span><span class="sxs-lookup"><span data-stu-id="b01d0-104">How tooSend Email Using SendGrid from Java</span></span>
<span data-ttu-id="b01d0-105">Ce guide montre comment tooperform des tâches de programmation courantes avec le SendGrid de messagerie service sur Azure.</span><span class="sxs-lookup"><span data-stu-id="b01d0-105">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="b01d0-106">exemples de Hello sont écrits en Java.</span><span class="sxs-lookup"><span data-stu-id="b01d0-106">hello samples are written in Java.</span></span> <span data-ttu-id="b01d0-107">Hello scénarios abordés incluent **construction de messagerie**, **envoi de courrier électronique**, **Ajout de pièces jointes**, **à l’aide de filtres**et **mise à jour des propriétés**.</span><span class="sxs-lookup"><span data-stu-id="b01d0-107">hello scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="b01d0-108">Pour plus d’informations sur SendGrid et envoi de courrier électronique, consultez hello [étapes](#next-steps) section.</span><span class="sxs-lookup"><span data-stu-id="b01d0-108">For more information on SendGrid and sending email, see hello [Next steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="b01d0-109">Qu’est hello SendGrid au Service de messagerie ?</span><span class="sxs-lookup"><span data-stu-id="b01d0-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="b01d0-110">SendGrid est un [service de messagerie dans le cloud] qui fournit des fonctionnalités fiables en matière de [remise de courrier électronique transactionnelle], d'extensibilité et d'analyse en temps réel, ainsi que des API flexibles qui facilitent l'intégration personnalisée.</span><span class="sxs-lookup"><span data-stu-id="b01d0-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="b01d0-111">Voici quelques scénarios courants en termes d'utilisation de SendGrid :</span><span class="sxs-lookup"><span data-stu-id="b01d0-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="b01d0-112">Envoyer automatiquement des accusés de réception toocustomers</span><span class="sxs-lookup"><span data-stu-id="b01d0-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="b01d0-113">Administration de listes de distribution pour un envoi mensuel de prospectus électroniques et d'offres spéciales aux clients</span><span class="sxs-lookup"><span data-stu-id="b01d0-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="b01d0-114">Collecte de mesures en temps réel concernant des éléments tels que les messages électroniques bloqués et la réactivité vis-à-vis des clients</span><span class="sxs-lookup"><span data-stu-id="b01d0-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="b01d0-115">Génération de rapports toohelp identifier les tendances</span><span class="sxs-lookup"><span data-stu-id="b01d0-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="b01d0-116">Transfert des demandes des clients</span><span class="sxs-lookup"><span data-stu-id="b01d0-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="b01d0-117">Notifications par courriers électroniques depuis votre application</span><span class="sxs-lookup"><span data-stu-id="b01d0-117">Email notifications from your application</span></span>

<span data-ttu-id="b01d0-118">Pour plus d'informations, consultez la page <http://sendgrid.com>.</span><span class="sxs-lookup"><span data-stu-id="b01d0-118">For more information, see <http://sendgrid.com>.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="b01d0-119">Création d'un compte SendGrid</span><span class="sxs-lookup"><span data-stu-id="b01d0-119">Create a SendGrid account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-hello-javaxmail-libraries"></a><span data-ttu-id="b01d0-120">Comment : utiliser les bibliothèques javax.mail hello</span><span class="sxs-lookup"><span data-stu-id="b01d0-120">How to: Use hello javax.mail libraries</span></span>
<span data-ttu-id="b01d0-121">Obtenir les bibliothèques javax.mail hello, par exemple à partir de <http://www.oracle.com/technetwork/java/javamail> et les importer dans votre code.</span><span class="sxs-lookup"><span data-stu-id="b01d0-121">Obtain hello javax.mail libraries, for example from <http://www.oracle.com/technetwork/java/javamail> and import them into your code.</span></span> <span data-ttu-id="b01d0-122">À un niveau élevé, hello processus pour l’utilisation de hello javax.mail bibliothèque toosend par courrier électronique à l’aide de SMTP est toodo hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b01d0-122">At a high-level, hello process for using hello javax.mail library toosend email using SMTP is toodo hello following:</span></span>

1. <span data-ttu-id="b01d0-123">Spécifier des valeurs de SMTP hello, y compris le serveur SMTP hello, c'est-à-dire pour SendGrid smtp.sendgrid.net.</span><span class="sxs-lookup"><span data-stu-id="b01d0-123">Specify hello SMTP values, including hello SMTP server, which for SendGrid is smtp.sendgrid.net.</span></span>

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

1. <span data-ttu-id="b01d0-124">Étendre hello *javax.mail.Authenticator* (classe) et dans votre implémentation de la *getPasswordAuthentication* (méthode), retourner votre nom d’utilisateur SendGrid et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="b01d0-124">Extend hello *javax.mail.Authenticator* class, and in your implementation of the *getPasswordAuthentication* method, return your SendGrid user name and password.</span></span>  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. <span data-ttu-id="b01d0-125">Créez une session de messagerie électronique authentifiée via un objet *javax.mail.Session* .</span><span class="sxs-lookup"><span data-stu-id="b01d0-125">Create an authenticated email session through a *javax.mail.Session* object.</span></span>  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. <span data-ttu-id="b01d0-126">Créez votre message et spécifiez des valeurs pour **À**, **De**, **Objet**.</span><span class="sxs-lookup"><span data-stu-id="b01d0-126">Create your message and assign **To**, **From**, **Subject** and content values.</span></span> <span data-ttu-id="b01d0-127">Cela est illustré par hello [comment faire : créer un message électronique](#how-to-create-an-email) section.</span><span class="sxs-lookup"><span data-stu-id="b01d0-127">This is shown in hello [How To: Create an Email](#how-to-create-an-email) section.</span></span>
4. <span data-ttu-id="b01d0-128">Envoyer le message de type hello via un *javax.mail.Transport* objet.</span><span class="sxs-lookup"><span data-stu-id="b01d0-128">Send hello message through a *javax.mail.Transport* object.</span></span> <span data-ttu-id="b01d0-129">Cela est illustré par hello [Comment : envoyer un courrier électronique] [Comment : envoyer un courrier électronique] section.</span><span class="sxs-lookup"><span data-stu-id="b01d0-129">This is shown in hello [How To: Send an Email][How to: Send an Email] section.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="b01d0-130">Création d'un message électronique</span><span class="sxs-lookup"><span data-stu-id="b01d0-130">How to: Create an email</span></span>
<span data-ttu-id="b01d0-131">Hello Voici comment toospecify les valeurs pour un message électronique.</span><span class="sxs-lookup"><span data-stu-id="b01d0-131">hello following shows how toospecify values for an email.</span></span>

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

## <a name="how-to-send-an-email"></a><span data-ttu-id="b01d0-132">Envoi d'un message électronique</span><span class="sxs-lookup"><span data-stu-id="b01d0-132">How to: Send an email</span></span>
<span data-ttu-id="b01d0-133">Hello ci-dessous illustre comment toosend un message électronique.</span><span class="sxs-lookup"><span data-stu-id="b01d0-133">hello following shows how toosend an email.</span></span>

    Transport transport = mailSession.getTransport();
    // Connect hello transport object.
    transport.connect();
    // Send hello message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close hello connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="b01d0-134">Ajout d'une pièce jointe</span><span class="sxs-lookup"><span data-stu-id="b01d0-134">How to: Add an attachment</span></span>
<span data-ttu-id="b01d0-135">Hello de code suivant vous montre comment tooadd une pièce jointe.</span><span class="sxs-lookup"><span data-stu-id="b01d0-135">hello following code shows you how tooadd an attachment.</span></span>

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

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="b01d0-136">Comment : utiliser les filtres analytique, suivi et les pieds de page tooenable</span><span class="sxs-lookup"><span data-stu-id="b01d0-136">How to: Use filters tooenable footers, tracking, and analytics</span></span>
<span data-ttu-id="b01d0-137">SendGrid fournit les fonctionnalités de messagerie supplémentaires via l’utilisation de hello de *filtres*.</span><span class="sxs-lookup"><span data-stu-id="b01d0-137">SendGrid provides additional email functionality through hello use of *filters*.</span></span> <span data-ttu-id="b01d0-138">Il s’agit des paramètres qui peuvent être ajoutées e-mail tooan pour activer des fonctionnalités spécifiques telles que l’activation de suivi des clics, Google analytique, abonnement suivi des modifications, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="b01d0-138">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="b01d0-139">Pour obtenir une liste exhaustive des filtres, consultez la page [Paramètres de filtre][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="b01d0-139">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

* <span data-ttu-id="b01d0-140">Hello Voici comment filtrer les tooinsert un pied de page qui génère du texte HTML qui apparaît au bas de hello de messagerie hello envoyé.</span><span class="sxs-lookup"><span data-stu-id="b01d0-140">hello following shows how tooinsert a footer filter that results in HTML text appearing at hello bottom of hello email being sent.</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* <span data-ttu-id="b01d0-141">Parmi les exemples de filtres, on peut également citer le suivi des clics.</span><span class="sxs-lookup"><span data-stu-id="b01d0-141">Another example of a filter is click tracking.</span></span> <span data-ttu-id="b01d0-142">Supposons que votre texte du courrier électronique contient un lien hypertexte, telles que hello suivant et que vous souhaitez tootrack hello cliquez sur taux :</span><span class="sxs-lookup"><span data-stu-id="b01d0-142">Let’s say that your email text contains a hyperlink, such as hello following, and you want tootrack hello click rate:</span></span>

      messagePart.setContent(
          "Hello,
          <p>This is hello body of hello message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* <span data-ttu-id="b01d0-143">tooenable hello sur le suivi des modifications, hello utilisation suivante du code :</span><span class="sxs-lookup"><span data-stu-id="b01d0-143">tooenable hello click tracking, use hello following code:</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a><span data-ttu-id="b01d0-144">Mise à jour des propriétés d'un message électronique</span><span class="sxs-lookup"><span data-stu-id="b01d0-144">How to: Update email properties</span></span>
<span data-ttu-id="b01d0-145">Certaines propriétés de messagerie peuvent être remplacées à l’aide de  **définir*propriété*** ou être ajoutées à l’aide de  **ajouter*propriété***.</span><span class="sxs-lookup"><span data-stu-id="b01d0-145">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span>

<span data-ttu-id="b01d0-146">Par exemple, toospecify **ReplyTo** adresses, utilisez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="b01d0-146">For example, toospecify **ReplyTo** addresses, use hello following:</span></span>

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

<span data-ttu-id="b01d0-147">tooadd un **Cc** suivant de hello destinataire, utilisez :</span><span class="sxs-lookup"><span data-stu-id="b01d0-147">tooadd a **Cc** recipient, use hello following:</span></span>

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="b01d0-148">Utilisation de services SendGrid supplémentaires</span><span class="sxs-lookup"><span data-stu-id="b01d0-148">How to: Use additional SendGrid services</span></span>
<span data-ttu-id="b01d0-149">SendGrid propose des API basées sur le web que vous pouvez utiliser les fonctionnalités de SendGrid tooleverage supplémentaires à partir de votre application Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="b01d0-149">SendGrid offers web-based APIs that you can use tooleverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="b01d0-150">Pour plus d’informations, consultez hello [documentation sur les API SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="b01d0-150">For full details, see hello [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="b01d0-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b01d0-151">Next steps</span></span>
<span data-ttu-id="b01d0-152">Maintenant que vous avez appris les notions de base de hello Hello au service de messagerie de SendGrid, suivez ces liens de toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="b01d0-152">Now that you’ve learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="b01d0-153">Exemple qui illustre l’utilisation de SendGrid dans un déploiement d’Azure : [comment toosend par courrier électronique à l’aide de SendGrid depuis Java dans un déploiement d’Azure](store-sendgrid-java-how-to-send-email-example.md)</span><span class="sxs-lookup"><span data-stu-id="b01d0-153">Sample that demonstrates using SendGrid in an Azure deployment: [How toosend email using SendGrid from Java in an Azure deployment](store-sendgrid-java-how-to-send-email-example.md)</span></span>
* <span data-ttu-id="b01d0-154">Kit de développement logiciel (SDK) SendGrid Java : <https://sendgrid.com/docs/Code_Examples/java.html></span><span class="sxs-lookup"><span data-stu-id="b01d0-154">SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html></span></span>
* <span data-ttu-id="b01d0-155">Documentation de l’API SendGrid : <https://sendgrid.com/docs/API_Reference/index.html></span><span class="sxs-lookup"><span data-stu-id="b01d0-155">SendGrid API documentation: <https://sendgrid.com/docs/API_Reference/index.html></span></span>
* <span data-ttu-id="b01d0-156">Offre spéciale SendGrid pour les clients Azure : <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="b01d0-156">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

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
