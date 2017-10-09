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
# <a name="how-toosend-email-using-sendgrid-with-azure"></a>Comment tooSend par courrier électronique à l’aide de SendGrid avec Azure
## <a name="overview"></a>Vue d'ensemble
Ce guide montre comment tooperform des tâches de programmation courantes avec le SendGrid de messagerie service sur Azure. exemples de Hello sont écrits en C\# et prend en charge .NET Standard 1.3. scénarios de Hello couvertes incluent construction par courrier électronique, envoi de courrier électronique, ajout de pièces jointes, activer la messagerie de différentes et des paramètres de suivi. Pour plus d’informations sur SendGrid et envoi de courrier électronique, consultez hello [étapes] [ Next steps] section.

## <a name="what-is-hello-sendgrid-email-service"></a>Qu’est hello SendGrid au Service de messagerie ?
SendGrid est un [service de messagerie dans le cloud] qui fournit des fonctionnalités fiables en matière de [remise de courrier électronique transactionnelle], d'extensibilité et d'analyse en temps réel, ainsi que des API flexibles qui facilitent l'intégration personnalisée. Voici quelques cas d’utilisation courants de SendGrid :

* Envoyer automatiquement des accusés de réception ou toocustomers de confirmations d’achat.
* Gestion de listes de distribution pour l’envoi mensuel de brochures et de promotions aux clients
* Collecte de mesures en temps réel, notamment en ce qui concerne les e-mails bloqués et l’engagement des clients
* transfert des demandes de renseignements des clients.
* traitement des messages électroniques entrants.

Pour plus d’informations, consultez le site [https://sendgrid.com](https://sendgrid.com) ou la [bibliothèque C#][sendgrid-csharp] de SendGrid dans le dépôt GitHub.

## <a name="create-a-sendgrid-account"></a>Création d'un compte SendGrid
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-net-class-library"></a>Référence hello SendGrid bibliothèque de classes .NET
Hello [package SendGrid NuGet](https://www.nuget.org/packages/Sendgrid) est hello de tooget de façon plus simple hello API SendGrid et tooconfigure votre application avec toutes les dépendances. NuGet est un extension incluse avec Microsoft Visual Studio 2015 et supérieur à celui rend facile bibliothèques de tooinstall et de mise à jour et les outils de Visual Studio.

> [!NOTE]
> tooinstall NuGet si vous exécutez une version de Visual Studio antérieures à Visual Studio 2015, visitez [http://www.nuget.org](http://www.nuget.org), puis cliquez sur hello **installer NuGet** bouton.
>
>

tooinstall hello package SendGrid NuGet dans votre application, procédez comme hello suivant :

1. Cliquez sur **Nouveau projet**, puis sélectionnez un **Modèle**.

   ![Création d'un projet][create-new-project]
2. Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur **References**, puis cliquez sur **Manage NuGet Packages**.

   ![package NuGet SendGrid][SendGrid-NuGet-package]
3. Recherchez **SendGrid** et sélectionnez hello **SendGrid** élément dans la liste des résultats.
4. Sélectionnez hello dernière version stable du package Nuget de hello dans hello version déroulante toobe en mesure de toowork avec le modèle d’objet hello et API présentés dans cet article.

   ![Package SendGrid][sendgrid-package]
5. Cliquez sur **installer** toocomplete hello installation, puis fermez cette boîte de dialogue.

La bibliothèque de classes .NET de SendGrid est appelée **SendGrid**. Il contient hello suivant des espaces de noms :

* **SendGrid** pour la communication avec l’API de SendGrid
* **SendGrid.Helpers.Mail** d’assistance pour les méthodes tooeasily créer des objets SendGridMessage qui spécifient comment toosend envoie par courrier électronique.

Ajoutez hello suivant code espace de noms déclarations toohello en haut de tous les fichiers c# dans lequel vous voulez que le service messagerie SendGrid tooprogrammatically accès hello.

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a>Création d'un message électronique
Hello d’utilisation **SendGridMessage** toocreate un message électronique de l’objet. Une fois que l’objet de message hello est créé, vous pouvez définir des propriétés et méthodes, y compris l’expéditeur du courrier électronique hello, destinataire du courrier électronique hello et objet de hello et le corps des messages électroniques de hello.

Hello exemple suivant montre comment toocreate un objet de messagerie entièrement remplie :

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

Pour plus d’informations sur toutes les propriétés et méthodes prises en charge par le type **SendGrid**, consultez la page [sendgrid-csharp][sendgrid-csharp] sur GitHub.

## <a name="how-to-send-an-email"></a>Envoi d'un message électronique
Après avoir créé un e-mail, vous pouvez l’envoyer à l’aide de l’API de SendGrid. Une autre possibilité consiste à utiliser la [bibliothèque intégrée de .NET][NET-library].

Pour envoyer des e-mails, vous devez fournir votre clé API SendGrid. Si vous avez besoin de plus d’informations sur la façon tooconfigure clés API, visitez le site API clés de SendGrid [documentation][documentation].

Vous pouvez stocker ces informations d’identification via votre portail Azure en cliquant sur paramètres de l’Application et ajout paires clé/valeur de hello sous les paramètres de l’application.

 ![Paramètres de l’application Azure][azure_app_settings]

 Vous pouvez ensuite y accéder comme suit :

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

Hello suivant exemples montrent comment un message à l’aide de toosend hello API Web.

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

## <a name="how-to-add-an-attachment"></a>Ajout d'une pièce jointe
Les pièces jointes peuvent être ajoutées à tooa message en appelant hello **AddAttachment** méthode et en spécifiant au minimum le nom de fichier hello et encodé en base 64 de contenu vous souhaitez tooattach. Vous pouvez inclure plusieurs pièces jointes en appelant cette méthode une fois pour chaque fichier, vous souhaitez tooattach ou à l’aide de hello **AddAttachments** (méthode). Bonjour à l’exemple suivant illustre l’ajout d’un message tooa de pièce jointe :

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-tooenable-footers-tracking-and-analytics"></a>Comment : utiliser tooenable les pieds de page Paramètres du courrier, le suivi et analytique
SendGrid fournit les fonctionnalités de messagerie supplémentaires via l’utilisation de hello de paramètres de courrier électronique et les paramètres de suivi. Ces paramètres peuvent être ajoutés tooan message tooenable des fonctionnalités de messagerie telles que le suivi des clics, Google analytique, suivi des abonnements et ainsi de suite. Pour obtenir une liste complète des applications, consultez hello [paramètres Documentation][settings-documentation].

Les applications peuvent être appliquées trop**SendGrid** e-mails à l’aide des méthodes implémentées dans le cadre de hello **SendGridMessage** classe. Hello exemples suivants illustrent le pied de page hello et cliquez sur le suivi des filtres :

Hello exemples suivants illustrent le pied de page hello et cliquez sur le suivi des filtres :

### <a name="footer-settings"></a>Paramètres de pied de page
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a>Suivi des clics
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a>Utilisation de services SendGrid supplémentaires
SendGrid offre plusieurs API et webhooks que vous pouvez utiliser des fonctionnalités supplémentaires tooleverage au sein de votre application Windows Azure. Pour plus d’informations, consultez hello [référence des API SendGrid][SendGrid API documentation].

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello Hello au service de messagerie de SendGrid, suivez ces liens de toolearn plus.

* Référentiel de la bibliothèque C\# de SendGrid : [sendgrid-csharp][sendgrid-csharp]
* Documentation de l’API SendGrid : <https://sendgrid.com/docs>

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

