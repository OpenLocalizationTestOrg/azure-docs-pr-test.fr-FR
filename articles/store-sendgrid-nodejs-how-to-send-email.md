---
title: aaaHow toouse hello SendGrid au service de messagerie (Node.js) | Documents Microsoft
description: "Découvrez comment envoyer un courrier électronique avec hello SendGrid au service de messagerie sur Azure. Exemples écrits à l’aide de hello Node.js API de code."
services: 
documentationcenter: nodejs
author: erikre
manager: wpickett
editor: 
ms.assetid: cac444b4-26b0-45ea-9c3d-eca28d57dacb
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 01/05/2016
ms.author: erikre
ms.openlocfilehash: fd617b6aaa656e7b5dd51c51ebb0db1e848450f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-nodejs"></a><span data-ttu-id="e26a9-104">Comment tooSend par courrier électronique à l’aide de SendGrid à partir de Node.js</span><span class="sxs-lookup"><span data-stu-id="e26a9-104">How tooSend Email Using SendGrid from Node.js</span></span>
<span data-ttu-id="e26a9-105">Ce guide montre comment tooperform des tâches de programmation courantes avec le SendGrid de messagerie service sur Azure.</span><span class="sxs-lookup"><span data-stu-id="e26a9-105">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="e26a9-106">exemples de Hello sont écrites à l’aide de hello Node.js API.</span><span class="sxs-lookup"><span data-stu-id="e26a9-106">hello samples are written using hello Node.js API.</span></span> <span data-ttu-id="e26a9-107">Hello scénarios abordés incluent **construction de messagerie**, **envoi de courrier électronique**, **Ajout de pièces jointes**, **à l’aide de filtres**et **mise à jour des propriétés**.</span><span class="sxs-lookup"><span data-stu-id="e26a9-107">hello scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="e26a9-108">Pour plus d’informations sur SendGrid et envoi de courrier électronique, consultez hello [étapes](#next-steps) section.</span><span class="sxs-lookup"><span data-stu-id="e26a9-108">For more information on SendGrid and sending email, see hello [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="e26a9-109">Qu’est hello SendGrid au Service de messagerie ?</span><span class="sxs-lookup"><span data-stu-id="e26a9-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="e26a9-110">SendGrid est un [service de messagerie dans le cloud] qui fournit des fonctionnalités fiables en matière de [remise de courrier électronique transactionnelle], d'extensibilité et d'analyse en temps réel, ainsi que des API flexibles qui facilitent l'intégration personnalisée.</span><span class="sxs-lookup"><span data-stu-id="e26a9-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="e26a9-111">Voici quelques scénarios courants en termes d'utilisation de SendGrid :</span><span class="sxs-lookup"><span data-stu-id="e26a9-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="e26a9-112">Envoyer automatiquement des accusés de réception toocustomers</span><span class="sxs-lookup"><span data-stu-id="e26a9-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="e26a9-113">Administration de listes de distribution pour un envoi mensuel de prospectus électroniques et d'offres spéciales aux clients</span><span class="sxs-lookup"><span data-stu-id="e26a9-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="e26a9-114">Collecte de mesures en temps réel concernant des éléments tels que les messages électroniques bloqués et la réactivité vis-à-vis des clients</span><span class="sxs-lookup"><span data-stu-id="e26a9-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="e26a9-115">Génération de rapports toohelp identifier les tendances</span><span class="sxs-lookup"><span data-stu-id="e26a9-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="e26a9-116">Transfert des demandes des clients</span><span class="sxs-lookup"><span data-stu-id="e26a9-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="e26a9-117">Notifications par courriers électroniques depuis votre application</span><span class="sxs-lookup"><span data-stu-id="e26a9-117">Email notifications from your application</span></span>

<span data-ttu-id="e26a9-118">Pour plus d'informations, consultez la page [https://sendgrid.com](https://sendgrid.com).</span><span class="sxs-lookup"><span data-stu-id="e26a9-118">For more information, see [https://sendgrid.com](https://sendgrid.com).</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="e26a9-119">Création d'un compte SendGrid</span><span class="sxs-lookup"><span data-stu-id="e26a9-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-nodejs-module"></a><span data-ttu-id="e26a9-120">Référence hello Module Node.js de SendGrid</span><span class="sxs-lookup"><span data-stu-id="e26a9-120">Reference hello SendGrid Node.js Module</span></span>
<span data-ttu-id="e26a9-121">module de SendGrid Hello pour Node.js peut être installé via le Gestionnaire de package de nœud hello (npm) à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e26a9-121">hello SendGrid module for Node.js can be installed through hello node package manager (npm) by using hello following command:</span></span>

    npm install sendgrid

<span data-ttu-id="e26a9-122">Après l’installation, vous pouvez exiger module de hello dans votre application à l’aide de hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="e26a9-122">After installation, you can require hello module in your application by using hello following code:</span></span>

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

<span data-ttu-id="e26a9-123">module de SendGrid Hello exporte hello **SendGrid** et **messagerie** fonctions.</span><span class="sxs-lookup"><span data-stu-id="e26a9-123">hello SendGrid module exports hello **SendGrid** and **Email** functions.</span></span>
<span data-ttu-id="e26a9-124">**SendGrid** est chargé d'envoyer l’e-mail par le biais de l'API Web, alors que **Email** permet d'encapsuler un e-mail.</span><span class="sxs-lookup"><span data-stu-id="e26a9-124">**SendGrid** is responsible for sending email through Web API, while **Email** encapsulates an email message.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="e26a9-125">Création d'un message électronique</span><span class="sxs-lookup"><span data-stu-id="e26a9-125">How to: Create an Email</span></span>
<span data-ttu-id="e26a9-126">Création d’un message électronique à l’aide du module de SendGrid hello implique la création d’abord un message électronique à l’aide de la fonction de messagerie hello, puis l’envoyer à l’aide de la fonction de SendGrid hello.</span><span class="sxs-lookup"><span data-stu-id="e26a9-126">Creating an email message using hello SendGrid module involves first creating an email message using hello Email function, and then sending it using hello SendGrid function.</span></span> <span data-ttu-id="e26a9-127">Hello Voici un exemple de création d’un nouveau message à l’aide de la fonction de messagerie hello :</span><span class="sxs-lookup"><span data-stu-id="e26a9-127">hello following is an example of creating a new message using hello Email function:</span></span>

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

<span data-ttu-id="e26a9-128">Vous pouvez également spécifier un message au format HTML pour les clients qui prennent en charge en définissant la propriété de html hello.</span><span class="sxs-lookup"><span data-stu-id="e26a9-128">You can also specify an HTML message for clients that support it by setting hello html property.</span></span> <span data-ttu-id="e26a9-129">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e26a9-129">For example:</span></span>

    html: This is a sample <b>HTML<b> email message.

<span data-ttu-id="e26a9-130">Définissant les propriétés de texte et html hello fournit des secours approprié au contenu de texte pour les clients qui ne peut pas prendre en charge les messages au format HTML.</span><span class="sxs-lookup"><span data-stu-id="e26a9-130">Setting both hello text and html properties provides graceful fallback to text content for clients that cannot support HTML messages.</span></span>

<span data-ttu-id="e26a9-131">Pour plus d’informations sur toutes les propriétés prises en charge par hello fonction de courrier électronique, consultez [sendgrid-nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="e26a9-131">For more information on all properties supported by hello Email function, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="e26a9-132">Envoi d'un message électronique</span><span class="sxs-lookup"><span data-stu-id="e26a9-132">How to: Send an Email</span></span>
<span data-ttu-id="e26a9-133">Après la création d’un message électronique à l’aide de hello fonction de courrier électronique, vous pouvez envoyer à l’aide de hello Web API fournie par SendGrid.</span><span class="sxs-lookup"><span data-stu-id="e26a9-133">After creating an email message using hello Email function, you can send it using hello Web API provided by SendGrid.</span></span> 

### <a name="web-api"></a><span data-ttu-id="e26a9-134">API Web</span><span class="sxs-lookup"><span data-stu-id="e26a9-134">Web API</span></span>
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> <span data-ttu-id="e26a9-135">Alors que hello exemples ci-dessus montrent le passage dans une fonction d’objet et de rappel par courrier électronique, vous pouvez également directement appeler fonction d’envoi hello en spécifiant directement les propriétés du courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="e26a9-135">While hello above examples show passing in an email object and callback function, you can also directly invoke hello send function by directly specifying email properties.</span></span> <span data-ttu-id="e26a9-136">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e26a9-136">For example:</span></span>  
> 
> `````
> sendgrid.send({
> to: 'john@contoso.com',
> from: 'anna@contoso.com',
> subject: 'test mail',
> text: 'This is a sample email message.'
> });
> `````
> 
> 

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="e26a9-137">Ajout d'une pièce jointe</span><span class="sxs-lookup"><span data-stu-id="e26a9-137">How to: Add an Attachment</span></span>
<span data-ttu-id="e26a9-138">Les pièces jointes peuvent être ajoutées tooa message en spécifiant les noms de fichiers hello et chemin d’accès au Bonjour **fichiers** propriété.</span><span class="sxs-lookup"><span data-stu-id="e26a9-138">Attachments can be added tooa message by specifying hello file name(s) and path(s) in hello **files** property.</span></span> <span data-ttu-id="e26a9-139">Bonjour à l’exemple suivant illustre l’envoi d’une pièce jointe :</span><span class="sxs-lookup"><span data-stu-id="e26a9-139">hello following example demonstrates sending an attachment:</span></span>

    sendgrid.send({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.',
        files: [
            {
                filename:     '',           // required only if file.content is used.
                contentType:  '',           // optional
                cid:          '',           // optional, used toospecify cid for inline content
                path:         '',           //
                url:          '',           // == One of these three options is required
                content:      ('' | Buffer) //
            }
        ],
    });

> [!NOTE]
> <span data-ttu-id="e26a9-140">Lorsque vous utilisez hello **fichiers** propriété, le fichier de hello doit être accessible via [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span><span class="sxs-lookup"><span data-stu-id="e26a9-140">When using hello **files** property, hello file must be accessible through [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span></span> <span data-ttu-id="e26a9-141">Si le fichier hello tooattach est hébergé dans le stockage Azure, par exemple dans un conteneur d’objets Blob, vous devez d’abord copier stockage toolocal hello ou tooan lecteur Azure avant d’être envoyé comme pièce jointe à l’aide de hello **fichiers** propriété.</span><span class="sxs-lookup"><span data-stu-id="e26a9-141">If hello file you wish tooattach is hosted in Azure Storage, such as in a Blob container, you must first copy hello file toolocal storage or tooan Azure drive before it can be sent as an attachment using hello **files** property.</span></span>
> 
> 

## <a name="how-to-use-filters-tooenable-footers-and-tracking"></a><span data-ttu-id="e26a9-142">Comment : utiliser des filtres tooEnable de pieds de page et de suivi</span><span class="sxs-lookup"><span data-stu-id="e26a9-142">How to: Use Filters tooEnable Footers and Tracking</span></span>
<span data-ttu-id="e26a9-143">SendGrid fournit les fonctionnalités de messagerie supplémentaires via l’utilisation de hello de filtres.</span><span class="sxs-lookup"><span data-stu-id="e26a9-143">SendGrid provides additional email functionality through hello use of filters.</span></span> <span data-ttu-id="e26a9-144">Il s’agit des paramètres qui peuvent être ajoutées e-mail tooan pour activer des fonctionnalités spécifiques telles que l’activation de suivi des clics, Google analytique, abonnement suivi des modifications, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="e26a9-144">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="e26a9-145">Pour obtenir une liste exhaustive des filtres, consultez la page [Paramètres de filtre][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="e26a9-145">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

<span data-ttu-id="e26a9-146">Les filtres peuvent être appliqués tooa message à l’aide de hello **filtres** propriété.</span><span class="sxs-lookup"><span data-stu-id="e26a9-146">Filters can be applied tooa message by using hello **filters** property.</span></span>
<span data-ttu-id="e26a9-147">Chaque filtre est spécifié par un hachage contenant des paramètres propres au filtre.</span><span class="sxs-lookup"><span data-stu-id="e26a9-147">Each filter is specified by a hash containing filter-specific settings.</span></span>
<span data-ttu-id="e26a9-148">Hello exemples suivants illustrent le pied de page hello et cliquez sur le suivi des filtres :</span><span class="sxs-lookup"><span data-stu-id="e26a9-148">hello following examples demonstrate hello footer and click tracking filters:</span></span>

### <a name="footer"></a><span data-ttu-id="e26a9-149">Pied de page</span><span class="sxs-lookup"><span data-stu-id="e26a9-149">Footer</span></span>
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'footer': {
            'settings': {
                'enable': 1,
                'text/plain': 'This is a text footer.'
            }
        }
    });

    sendgrid.send(email);

### <a name="click-tracking"></a><span data-ttu-id="e26a9-150">Suivi des clics</span><span class="sxs-lookup"><span data-stu-id="e26a9-150">Click Tracking</span></span>
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'clicktrack': {
            'settings': {
                'enable': 1
            }
        }
    });

    sendgrid.send(email);

## <a name="how-to-update-email-properties"></a><span data-ttu-id="e26a9-151">Mise à jour des propriétés de messagerie électronique</span><span class="sxs-lookup"><span data-stu-id="e26a9-151">How to: Update Email Properties</span></span>
<span data-ttu-id="e26a9-152">Certaines propriétés de messagerie peuvent être remplacées à l’aide de  **définir*propriété*** ou être ajoutées à l’aide de  **ajouter*propriété***.</span><span class="sxs-lookup"><span data-stu-id="e26a9-152">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span> <span data-ttu-id="e26a9-153">Par exemple, vous pouvez ajouter des destinataires supplémentaires en utilisant</span><span class="sxs-lookup"><span data-stu-id="e26a9-153">For example, you can add additional recipients by using</span></span>

    email.addTo('jeff@contoso.com');

<span data-ttu-id="e26a9-154">ou définir un filtre en utilisant</span><span class="sxs-lookup"><span data-stu-id="e26a9-154">or set a filter by using</span></span>

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

<span data-ttu-id="e26a9-155">Pour plus d’informations, consultez [sendgrid-nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="e26a9-155">For more information, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="e26a9-156">Utilisation de services SendGrid supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e26a9-156">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="e26a9-157">SendGrid propose des API basées sur le web que vous pouvez utiliser les fonctionnalités de SendGrid tooleverage supplémentaires à partir de votre application Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="e26a9-157">SendGrid offers web-based APIs that you can use tooleverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="e26a9-158">Pour plus d’informations, consultez hello [documentation sur les API SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="e26a9-158">For full details, see hello [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="e26a9-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e26a9-159">Next Steps</span></span>
<span data-ttu-id="e26a9-160">Maintenant que vous avez appris les notions de base de hello Hello au service de messagerie de SendGrid, suivez ces liens de toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="e26a9-160">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="e26a9-161">Référentiel de module SendGrid Node.js : [sendgrid-nodejs][sendgrid-nodejs]</span><span class="sxs-lookup"><span data-stu-id="e26a9-161">SendGrid Node.js module repository: [sendgrid-nodejs][sendgrid-nodejs]</span></span>
* <span data-ttu-id="e26a9-162">Documentation de l’API SendGrid : <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="e26a9-162">SendGrid API documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="e26a9-163">Offres spéciales SendGrid pour les clients Azure : [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span><span class="sxs-lookup"><span data-stu-id="e26a9-163">SendGrid special offer for Azure customers: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span></span>

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
[service de messagerie dans le cloud]: https://sendgrid.com/email-solutions
[remise de courrier électronique transactionnelle]: https://sendgrid.com/transactional-email
