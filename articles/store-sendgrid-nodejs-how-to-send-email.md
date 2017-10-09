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
# <a name="how-toosend-email-using-sendgrid-from-nodejs"></a>Comment tooSend par courrier électronique à l’aide de SendGrid à partir de Node.js
Ce guide montre comment tooperform des tâches de programmation courantes avec le SendGrid de messagerie service sur Azure. exemples de Hello sont écrites à l’aide de hello Node.js API. Hello scénarios abordés incluent **construction de messagerie**, **envoi de courrier électronique**, **Ajout de pièces jointes**, **à l’aide de filtres**et **mise à jour des propriétés**. Pour plus d’informations sur SendGrid et envoi de courrier électronique, consultez hello [étapes](#next-steps) section.

## <a name="what-is-hello-sendgrid-email-service"></a>Qu’est hello SendGrid au Service de messagerie ?
SendGrid est un [service de messagerie dans le cloud] qui fournit des fonctionnalités fiables en matière de [remise de courrier électronique transactionnelle], d'extensibilité et d'analyse en temps réel, ainsi que des API flexibles qui facilitent l'intégration personnalisée. Voici quelques scénarios courants en termes d'utilisation de SendGrid :

* Envoyer automatiquement des accusés de réception toocustomers
* Administration de listes de distribution pour un envoi mensuel de prospectus électroniques et d'offres spéciales aux clients
* Collecte de mesures en temps réel concernant des éléments tels que les messages électroniques bloqués et la réactivité vis-à-vis des clients
* Génération de rapports toohelp identifier les tendances
* Transfert des demandes des clients
* Notifications par courriers électroniques depuis votre application

Pour plus d'informations, consultez la page [https://sendgrid.com](https://sendgrid.com).

## <a name="create-a-sendgrid-account"></a>Création d'un compte SendGrid
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-nodejs-module"></a>Référence hello Module Node.js de SendGrid
module de SendGrid Hello pour Node.js peut être installé via le Gestionnaire de package de nœud hello (npm) à l’aide de hello de commande suivante :

    npm install sendgrid

Après l’installation, vous pouvez exiger module de hello dans votre application à l’aide de hello suivant de code :

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

module de SendGrid Hello exporte hello **SendGrid** et **messagerie** fonctions.
**SendGrid** est chargé d'envoyer l’e-mail par le biais de l'API Web, alors que **Email** permet d'encapsuler un e-mail.

## <a name="how-to-create-an-email"></a>Création d'un message électronique
Création d’un message électronique à l’aide du module de SendGrid hello implique la création d’abord un message électronique à l’aide de la fonction de messagerie hello, puis l’envoyer à l’aide de la fonction de SendGrid hello. Hello Voici un exemple de création d’un nouveau message à l’aide de la fonction de messagerie hello :

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

Vous pouvez également spécifier un message au format HTML pour les clients qui prennent en charge en définissant la propriété de html hello. Par exemple :

    html: This is a sample <b>HTML<b> email message.

Définissant les propriétés de texte et html hello fournit des secours approprié au contenu de texte pour les clients qui ne peut pas prendre en charge les messages au format HTML.

Pour plus d’informations sur toutes les propriétés prises en charge par hello fonction de courrier électronique, consultez [sendgrid-nodejs][sendgrid-nodejs].

## <a name="how-to-send-an-email"></a>Envoi d'un message électronique
Après la création d’un message électronique à l’aide de hello fonction de courrier électronique, vous pouvez envoyer à l’aide de hello Web API fournie par SendGrid. 

### <a name="web-api"></a>API Web
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> Alors que hello exemples ci-dessus montrent le passage dans une fonction d’objet et de rappel par courrier électronique, vous pouvez également directement appeler fonction d’envoi hello en spécifiant directement les propriétés du courrier électronique. Par exemple :  
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

## <a name="how-to-add-an-attachment"></a>Ajout d'une pièce jointe
Les pièces jointes peuvent être ajoutées tooa message en spécifiant les noms de fichiers hello et chemin d’accès au Bonjour **fichiers** propriété. Bonjour à l’exemple suivant illustre l’envoi d’une pièce jointe :

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
> Lorsque vous utilisez hello **fichiers** propriété, le fichier de hello doit être accessible via [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile). Si le fichier hello tooattach est hébergé dans le stockage Azure, par exemple dans un conteneur d’objets Blob, vous devez d’abord copier stockage toolocal hello ou tooan lecteur Azure avant d’être envoyé comme pièce jointe à l’aide de hello **fichiers** propriété.
> 
> 

## <a name="how-to-use-filters-tooenable-footers-and-tracking"></a>Comment : utiliser des filtres tooEnable de pieds de page et de suivi
SendGrid fournit les fonctionnalités de messagerie supplémentaires via l’utilisation de hello de filtres. Il s’agit des paramètres qui peuvent être ajoutées e-mail tooan pour activer des fonctionnalités spécifiques telles que l’activation de suivi des clics, Google analytique, abonnement suivi des modifications, et ainsi de suite. Pour obtenir une liste exhaustive des filtres, consultez la page [Paramètres de filtre][Filter Settings].

Les filtres peuvent être appliqués tooa message à l’aide de hello **filtres** propriété.
Chaque filtre est spécifié par un hachage contenant des paramètres propres au filtre.
Hello exemples suivants illustrent le pied de page hello et cliquez sur le suivi des filtres :

### <a name="footer"></a>Pied de page
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

### <a name="click-tracking"></a>Suivi des clics
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

## <a name="how-to-update-email-properties"></a>Mise à jour des propriétés de messagerie électronique
Certaines propriétés de messagerie peuvent être remplacées à l’aide de  **définir*propriété*** ou être ajoutées à l’aide de  **ajouter*propriété***. Par exemple, vous pouvez ajouter des destinataires supplémentaires en utilisant

    email.addTo('jeff@contoso.com');

ou définir un filtre en utilisant

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

Pour plus d’informations, consultez [sendgrid-nodejs][sendgrid-nodejs].

## <a name="how-to-use-additional-sendgrid-services"></a>Utilisation de services SendGrid supplémentaires
SendGrid propose des API basées sur le web que vous pouvez utiliser les fonctionnalités de SendGrid tooleverage supplémentaires à partir de votre application Windows Azure. Pour plus d’informations, consultez hello [documentation sur les API SendGrid][SendGrid API documentation].

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello Hello au service de messagerie de SendGrid, suivez ces liens de toolearn plus.

* Référentiel de module SendGrid Node.js : [sendgrid-nodejs][sendgrid-nodejs]
* Documentation de l’API SendGrid : <https://sendgrid.com/docs>
* Offres spéciales SendGrid pour les clients Azure : [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
[service de messagerie dans le cloud]: https://sendgrid.com/email-solutions
[remise de courrier électronique transactionnelle]: https://sendgrid.com/transactional-email
