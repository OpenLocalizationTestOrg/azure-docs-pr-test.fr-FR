---
title: aaaHow toouse hello SendGrid au service de messagerie (.NET) | Documents Microsoft
description: "Découvrez comment envoyer un courrier électronique avec hello SendGrid au service de messagerie sur Azure. Exemples de code écrits en c# et utilisez hello API .NET."
services: app-service-web
documentationcenter: .net
author: thinkingserious
manager: erikre
editor: 
ms.assetid: 21bf4028-9046-476b-9799-3d3082a0f84c
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/15/2017
ms.author: dx@sendgrid.com
ms.openlocfilehash: b3d77bb67898b991c7293e6b9086b263f6bcb755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-with-azure"></a><span data-ttu-id="92681-104">Comment tooSend par courrier électronique à l’aide de SendGrid avec Azure</span><span class="sxs-lookup"><span data-stu-id="92681-104">How tooSend Email Using SendGrid with Azure</span></span>
## <a name="overview"></a><span data-ttu-id="92681-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="92681-105">Overview</span></span>
<span data-ttu-id="92681-106">Ce guide montre comment tooperform des tâches de programmation courantes avec le SendGrid de messagerie service sur Azure.</span><span class="sxs-lookup"><span data-stu-id="92681-106">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="92681-107">exemples de Hello sont écrits en C\# et prend en charge .NET Standard 1.3.</span><span class="sxs-lookup"><span data-stu-id="92681-107">hello samples are written in C\# and supports .NET Standard 1.3.</span></span> <span data-ttu-id="92681-108">scénarios de Hello couvertes incluent construction par courrier électronique, envoi de courrier électronique, ajout de pièces jointes, activer la messagerie de différentes et des paramètres de suivi.</span><span class="sxs-lookup"><span data-stu-id="92681-108">hello scenarios covered include constructing email, sending email, adding attachments, and enabling various mail and tracking settings.</span></span> <span data-ttu-id="92681-109">Pour plus d’informations sur SendGrid et envoi de courrier électronique, consultez hello [étapes] [ Next steps] section.</span><span class="sxs-lookup"><span data-stu-id="92681-109">For more information on SendGrid and sending email, see hello [Next steps][Next steps] section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="92681-110">Qu’est hello SendGrid au Service de messagerie ?</span><span class="sxs-lookup"><span data-stu-id="92681-110">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="92681-111">SendGrid est un [service de messagerie dans le cloud] qui fournit des fonctionnalités fiables en matière de [remise de courrier électronique transactionnelle], d'extensibilité et d'analyse en temps réel, ainsi que des API flexibles qui facilitent l'intégration personnalisée.</span><span class="sxs-lookup"><span data-stu-id="92681-111">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="92681-112">Voici quelques cas d’utilisation courants de SendGrid :</span><span class="sxs-lookup"><span data-stu-id="92681-112">Common SendGrid use cases include:</span></span>

* <span data-ttu-id="92681-113">Envoyer automatiquement des accusés de réception ou toocustomers de confirmations d’achat.</span><span class="sxs-lookup"><span data-stu-id="92681-113">Automatically sending receipts or purchase confirmations toocustomers.</span></span>
* <span data-ttu-id="92681-114">Gestion de listes de distribution pour l’envoi mensuel de brochures et de promotions aux clients</span><span class="sxs-lookup"><span data-stu-id="92681-114">Administering distribution lists for sending customers monthly fliers and promotions.</span></span>
* <span data-ttu-id="92681-115">Collecte de mesures en temps réel, notamment en ce qui concerne les e-mails bloqués et l’engagement des clients</span><span class="sxs-lookup"><span data-stu-id="92681-115">Collecting real-time metrics for things like blocked email and customer engagement.</span></span>
* <span data-ttu-id="92681-116">transfert des demandes de renseignements des clients.</span><span class="sxs-lookup"><span data-stu-id="92681-116">Forwarding customer inquiries.</span></span>
* <span data-ttu-id="92681-117">traitement des messages électroniques entrants.</span><span class="sxs-lookup"><span data-stu-id="92681-117">Processing incoming emails.</span></span>

<span data-ttu-id="92681-118">Pour plus d’informations, consultez le site [https://sendgrid.com](https://sendgrid.com) ou la [bibliothèque C#][sendgrid-csharp] de SendGrid dans le dépôt GitHub.</span><span class="sxs-lookup"><span data-stu-id="92681-118">For more information, visit [https://sendgrid.com](https://sendgrid.com) or SendGrid's [C# library][sendgrid-csharp] GitHub repo.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="92681-119">Création d'un compte SendGrid</span><span class="sxs-lookup"><span data-stu-id="92681-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-net-class-library"></a><span data-ttu-id="92681-120">Référence hello SendGrid bibliothèque de classes .NET</span><span class="sxs-lookup"><span data-stu-id="92681-120">Reference hello SendGrid .NET Class Library</span></span>
<span data-ttu-id="92681-121">Hello [package SendGrid NuGet](https://www.nuget.org/packages/Sendgrid) est hello de tooget de façon plus simple hello API SendGrid et tooconfigure votre application avec toutes les dépendances.</span><span class="sxs-lookup"><span data-stu-id="92681-121">hello [SendGrid NuGet package](https://www.nuget.org/packages/Sendgrid) is hello easiest way tooget hello SendGrid API and tooconfigure your application with all dependencies.</span></span> <span data-ttu-id="92681-122">NuGet est un extension incluse avec Microsoft Visual Studio 2015 et supérieur à celui rend facile bibliothèques de tooinstall et de mise à jour et les outils de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="92681-122">NuGet is a Visual Studio extension included with Microsoft Visual Studio 2015 and above that makes it easy tooinstall and update libraries and tools.</span></span>

> [!NOTE]
> <span data-ttu-id="92681-123">tooinstall NuGet si vous exécutez une version de Visual Studio antérieures à Visual Studio 2015, visitez [http://www.nuget.org](http://www.nuget.org), puis cliquez sur hello **installer NuGet** bouton.</span><span class="sxs-lookup"><span data-stu-id="92681-123">tooinstall NuGet if you are running a version of Visual Studio earlier than Visual Studio 2015, visit [http://www.nuget.org](http://www.nuget.org), and click hello **Install NuGet** button.</span></span>
>
>

<span data-ttu-id="92681-124">tooinstall hello package SendGrid NuGet dans votre application, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="92681-124">tooinstall hello SendGrid NuGet package in your application, do hello following:</span></span>

1. <span data-ttu-id="92681-125">Cliquez sur **Nouveau projet**, puis sélectionnez un **Modèle**.</span><span class="sxs-lookup"><span data-stu-id="92681-125">Click on **New Project** and select a **Template**.</span></span>

   ![Création d'un projet][create-new-project]
2. <span data-ttu-id="92681-127">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur **References**, puis cliquez sur **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="92681-127">In **Solution Explorer**, right-click **References**, then click **Manage NuGet Packages**.</span></span>

   ![package NuGet SendGrid][SendGrid-NuGet-package]
3. <span data-ttu-id="92681-129">Recherchez **SendGrid** et sélectionnez hello **SendGrid** élément dans la liste des résultats.</span><span class="sxs-lookup"><span data-stu-id="92681-129">Search for **SendGrid** and select hello **SendGrid** item in the results list.</span></span>
4. <span data-ttu-id="92681-130">Sélectionnez hello dernière version stable du package Nuget de hello dans hello version déroulante toobe en mesure de toowork avec le modèle d’objet hello et API présentés dans cet article.</span><span class="sxs-lookup"><span data-stu-id="92681-130">Select hello latest stable version of hello Nuget package from hello version dropdown toobe able toowork with hello object model and APIs demonstrated in this article.</span></span>

   ![Package SendGrid][sendgrid-package]
5. <span data-ttu-id="92681-132">Cliquez sur **installer** toocomplete hello installation, puis fermez cette boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="92681-132">Click **Install** toocomplete hello installation, and then close this dialog.</span></span>

<span data-ttu-id="92681-133">La bibliothèque de classes .NET de SendGrid est appelée **SendGrid**.</span><span class="sxs-lookup"><span data-stu-id="92681-133">SendGrid's .NET class library is called **SendGrid**.</span></span> <span data-ttu-id="92681-134">Il contient hello suivant des espaces de noms :</span><span class="sxs-lookup"><span data-stu-id="92681-134">It contains hello following namespaces:</span></span>

* <span data-ttu-id="92681-135">**SendGrid** pour la communication avec l’API de SendGrid</span><span class="sxs-lookup"><span data-stu-id="92681-135">**SendGrid** for communicating with SendGrid’s API.</span></span>
* <span data-ttu-id="92681-136">**SendGrid.Helpers.Mail** d’assistance pour les méthodes tooeasily créer des objets SendGridMessage qui spécifient comment toosend envoie par courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="92681-136">**SendGrid.Helpers.Mail** for helper methods tooeasily create SendGridMessage objects that specify how toosend emails.</span></span>

<span data-ttu-id="92681-137">Ajoutez hello suivant code espace de noms déclarations toohello en haut de tous les fichiers c# dans lequel vous voulez que le service messagerie SendGrid tooprogrammatically accès hello.</span><span class="sxs-lookup"><span data-stu-id="92681-137">Add hello following code namespace declarations toohello top of any C# file in which you want tooprogrammatically access hello SendGrid email service.</span></span>

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a><span data-ttu-id="92681-138">Création d'un message électronique</span><span class="sxs-lookup"><span data-stu-id="92681-138">How to: Create an Email</span></span>
<span data-ttu-id="92681-139">Hello d’utilisation **SendGridMessage** toocreate un message électronique de l’objet.</span><span class="sxs-lookup"><span data-stu-id="92681-139">Use hello **SendGridMessage** object toocreate an email message.</span></span> <span data-ttu-id="92681-140">Une fois que l’objet de message hello est créé, vous pouvez définir des propriétés et méthodes, y compris l’expéditeur du courrier électronique hello, destinataire du courrier électronique hello et objet de hello et le corps des messages électroniques de hello.</span><span class="sxs-lookup"><span data-stu-id="92681-140">Once hello message object is created, you can set properties and methods, including hello email sender, hello email recipient, and hello subject and body of hello email.</span></span>

<span data-ttu-id="92681-141">Hello exemple suivant montre comment toocreate un objet de messagerie entièrement remplie :</span><span class="sxs-lookup"><span data-stu-id="92681-141">hello following example demonstrates how toocreate a fully populated email object:</span></span>

    var msg = new SendGridMessage();

    msg.SetFrom(new EmailAddress("dx@example.com", "SendGrid DX Team"));

    var recipients = new List<EmailAddress>
    {
        new EmailAddress("jeff@example.com", "Jeff Smith"),
        new EmailAddress("anna@example.com", "Anna Lidman"),
        new EmailAddress("peter@example.com", "Peter Saddow")
    };
    msg.AddTos(recipients);

    msg.SetSubject("Testing hello SendGrid C# Library");

    msg.AddContent(MimeType.Text, "Hello World plain text!");
    msg.AddContent(MimeType.Html, "<p>Hello World!</p>");

<span data-ttu-id="92681-142">Pour plus d’informations sur toutes les propriétés et méthodes prises en charge par le type **SendGrid**, consultez la page [sendgrid-csharp][sendgrid-csharp] sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="92681-142">For more information on all properties and methods supported by the **SendGrid** type, see [sendgrid-csharp][sendgrid-csharp] on GitHub.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="92681-143">Envoi d'un message électronique</span><span class="sxs-lookup"><span data-stu-id="92681-143">How to: Send an Email</span></span>
<span data-ttu-id="92681-144">Après avoir créé un e-mail, vous pouvez l’envoyer à l’aide de l’API de SendGrid.</span><span class="sxs-lookup"><span data-stu-id="92681-144">After creating an email message, you can send it using SendGrid's API.</span></span> <span data-ttu-id="92681-145">Une autre possibilité consiste à utiliser la [bibliothèque intégrée de .NET][NET-library].</span><span class="sxs-lookup"><span data-stu-id="92681-145">Alternatively, you may use [.NET's built in library][NET-library].</span></span>

<span data-ttu-id="92681-146">Pour envoyer des e-mails, vous devez fournir votre clé API SendGrid.</span><span class="sxs-lookup"><span data-stu-id="92681-146">Sending email requires that you supply your SendGrid API Key.</span></span> <span data-ttu-id="92681-147">Si vous avez besoin de plus d’informations sur la façon tooconfigure clés API, visitez le site API clés de SendGrid [documentation][documentation].</span><span class="sxs-lookup"><span data-stu-id="92681-147">If you need details about how tooconfigure API Keys, please visit SendGrid's API Keys [documentation][documentation].</span></span>

<span data-ttu-id="92681-148">Vous pouvez stocker ces informations d’identification via votre portail Azure en cliquant sur paramètres de l’Application et ajout paires clé/valeur de hello sous les paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="92681-148">You may store these credentials via your Azure Portal by clicking Application settings and adding hello key/value pairs under App settings.</span></span>

 ![Paramètres de l’application Azure][azure_app_settings]

 <span data-ttu-id="92681-150">Vous pouvez ensuite y accéder comme suit :</span><span class="sxs-lookup"><span data-stu-id="92681-150">Then, you may access them as follows:</span></span>

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

<span data-ttu-id="92681-151">Hello suivant exemples montrent comment un message à l’aide de toosend hello API Web.</span><span class="sxs-lookup"><span data-stu-id="92681-151">hello following examples show how toosend a message using hello Web API.</span></span>

    using System;
    using System.Threading.Tasks;
    using SendGrid;
    using SendGrid.Helpers.Mail;

    namespace Example
    {
        internal class Example
        {
            private static void Main()
            {
                Execute().Wait();
            }

            static async Task Execute()
            {
                var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
                var client = new SendGridClient(apiKey);
                var msg = new SendGridMessage()
                {
                    From = new EmailAddress("test@example.com", "DX Team"),
                    Subject = "Hello World from hello SendGrid CSharp SDK!",
                    PlainTextContent = "Hello, Email!",
                    HtmlContent = "<strong>Hello, Email!</strong>"
                };
                msg.AddTo(new EmailAddress("test@example.com", "Test User"));
                var response = await client.SendEmailAsync(msg);
            }
        }
    }

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="92681-152">Ajout d'une pièce jointe</span><span class="sxs-lookup"><span data-stu-id="92681-152">How to: Add an attachment</span></span>
<span data-ttu-id="92681-153">Les pièces jointes peuvent être ajoutées à tooa message en appelant hello **AddAttachment** méthode et en spécifiant au minimum le nom de fichier hello et encodé en base 64 de contenu vous souhaitez tooattach.</span><span class="sxs-lookup"><span data-stu-id="92681-153">Attachments can be added tooa message by calling hello **AddAttachment** method and minimally specifying hello file name and Base64 encoded content you want tooattach.</span></span> <span data-ttu-id="92681-154">Vous pouvez inclure plusieurs pièces jointes en appelant cette méthode une fois pour chaque fichier, vous souhaitez tooattach ou à l’aide de hello **AddAttachments** (méthode).</span><span class="sxs-lookup"><span data-stu-id="92681-154">You can include multiple attachments by calling this method once for each file you wish tooattach or by using hello **AddAttachments** method.</span></span> <span data-ttu-id="92681-155">Bonjour à l’exemple suivant illustre l’ajout d’un message tooa de pièce jointe :</span><span class="sxs-lookup"><span data-stu-id="92681-155">hello following example demonstrates adding an attachment tooa message:</span></span>

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="92681-156">Comment : utiliser tooenable les pieds de page Paramètres du courrier, le suivi et analytique</span><span class="sxs-lookup"><span data-stu-id="92681-156">How to: Use mail settings tooenable footers, tracking, and analytics</span></span>
<span data-ttu-id="92681-157">SendGrid fournit les fonctionnalités de messagerie supplémentaires via l’utilisation de hello de paramètres de courrier électronique et les paramètres de suivi.</span><span class="sxs-lookup"><span data-stu-id="92681-157">SendGrid provides additional email functionality through hello use of mail settings and tracking settings.</span></span> <span data-ttu-id="92681-158">Ces paramètres peuvent être ajoutés tooan message tooenable des fonctionnalités de messagerie telles que le suivi des clics, Google analytique, suivi des abonnements et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="92681-158">These settings can be added tooan email message tooenable specific functionality such as click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="92681-159">Pour obtenir une liste complète des applications, consultez hello [paramètres Documentation][settings-documentation].</span><span class="sxs-lookup"><span data-stu-id="92681-159">For a full list of apps, see hello [Settings Documentation][settings-documentation].</span></span>

<span data-ttu-id="92681-160">Les applications peuvent être appliquées trop**SendGrid** e-mails à l’aide des méthodes implémentées dans le cadre de hello **SendGridMessage** classe.</span><span class="sxs-lookup"><span data-stu-id="92681-160">Apps can be applied too**SendGrid** email messages using methods implemented as part of hello **SendGridMessage** class.</span></span> <span data-ttu-id="92681-161">Hello exemples suivants illustrent le pied de page hello et cliquez sur le suivi des filtres :</span><span class="sxs-lookup"><span data-stu-id="92681-161">hello following examples demonstrate hello footer and click tracking filters:</span></span>

<span data-ttu-id="92681-162">Hello exemples suivants illustrent le pied de page hello et cliquez sur le suivi des filtres :</span><span class="sxs-lookup"><span data-stu-id="92681-162">hello following examples demonstrate hello footer and click tracking filters:</span></span>

### <a name="footer-settings"></a><span data-ttu-id="92681-163">Paramètres de pied de page</span><span class="sxs-lookup"><span data-stu-id="92681-163">Footer settings</span></span>
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a><span data-ttu-id="92681-164">Suivi des clics</span><span class="sxs-lookup"><span data-stu-id="92681-164">Click tracking</span></span>
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="92681-165">Utilisation de services SendGrid supplémentaires</span><span class="sxs-lookup"><span data-stu-id="92681-165">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="92681-166">SendGrid offre plusieurs API et webhooks que vous pouvez utiliser des fonctionnalités supplémentaires tooleverage au sein de votre application Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="92681-166">SendGrid offers several APIs and webhooks that you can use tooleverage additional functionality within your Azure application.</span></span> <span data-ttu-id="92681-167">Pour plus d’informations, consultez hello [référence des API SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="92681-167">For more details, see hello [SendGrid API Reference][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="92681-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="92681-168">Next steps</span></span>
<span data-ttu-id="92681-169">Maintenant que vous avez appris les notions de base de hello Hello au service de messagerie de SendGrid, suivez ces liens de toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="92681-169">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="92681-170">Référentiel de la bibliothèque C\# de SendGrid : [sendgrid-csharp][sendgrid-csharp]</span><span class="sxs-lookup"><span data-stu-id="92681-170">SendGrid C\# library repo: [sendgrid-csharp][sendgrid-csharp]</span></span>
* <span data-ttu-id="92681-171">Documentation de l’API SendGrid : <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="92681-171">SendGrid API documentation: <https://sendgrid.com/docs></span></span>

[Next steps]: #next-steps
[What is hello SendGrid Email Service?]: #whatis
[Create a SendGrid Account]: #createaccount
[Reference hello SendGrid .NET Class Library]: #reference
[How to: Create an Email]: #createemail
[How to: Send an Email]: #sendemail
[How to: Add an Attachment]: #addattachment
[How to: Use Filters tooEnable Footers, Tracking, and Analytics]: #usefilters
[How to: Use Additional SendGrid Services]: #useservices

[create-new-project]: ./media/sendgrid-dotnet-how-to-send-email/new-project.png
[SendGrid-NuGet-package]: ./media/sendgrid-dotnet-how-to-send-email/reference.png
[sendgrid-package]: ./media/sendgrid-dotnet-how-to-send-email/sendgrid-package.png
[azure_app_settings]: ./media/sendgrid-dotnet-how-to-send-email/azure-app-settings.png
[sendgrid-csharp]: https://github.com/sendgrid/sendgrid-csharp
[SMTP vs. Web API]: https://sendgrid.com/docs/Integrate/index.html
[App Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/api_v3.html
[NET-library]: https://sendgrid.com/docs/Integrate/Code_Examples/v2_Mail/csharp.html#-Using-NETs-Builtin-SMTP-Library
[documentation]: https://sendgrid.com/docs/Classroom/Send/api_keys.html
[settings-documentation]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html

[service de messagerie dans le cloud]: https://sendgrid.com/solutions
[remise de courrier électronique transactionnelle]: https://sendgrid.com/use-cases/transactional-email

