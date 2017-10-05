---
title: Liaisons SendGrid dans Azure Functions | Microsoft Docs
description: "Informations de référence sur les liaisons SendGrid dans Azure Functions"
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/16/2017
ms.author: rachelap
ms.openlocfilehash: 445a40a884e648cdb2a57f8ef43bed4f8a3efcf2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-sendgrid-bindings"></a><span data-ttu-id="4be49-103">Liaisons SendGrid dans Azure Functions</span><span class="sxs-lookup"><span data-stu-id="4be49-103">Azure Functions SendGrid bindings</span></span>

<span data-ttu-id="4be49-104">Cet article explique comment configurer et utiliser des liaisons SendGrid dans Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="4be49-104">This article explains how to configure and work with SendGrid bindings in Azure Functions.</span></span> <span data-ttu-id="4be49-105">Avec SendGrid, vous pouvez utiliser Azure Functions pour envoyer un e-mail personnalisé par programmation.</span><span class="sxs-lookup"><span data-stu-id="4be49-105">With SendGrid, you can use Azure Functions to send customized email programmatically.</span></span>

<span data-ttu-id="4be49-106">Cet article fournit des informations de référence pour les développeurs Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="4be49-106">This article is reference information for Azure Functions developers.</span></span> <span data-ttu-id="4be49-107">Si vous ne connaissez pas bien Azure Functions, commencez par consulter les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="4be49-107">If you're new to Azure Functions, start with the following resources:</span></span>

<span data-ttu-id="4be49-108">[Créer votre première fonction Azure](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="4be49-108">[Create your first Azure Function](functions-create-first-azure-function.md).</span></span> 
<span data-ttu-id="4be49-109">Références pour les développeurs [C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md) ou [Node](functions-reference-node.md).</span><span class="sxs-lookup"><span data-stu-id="4be49-109">[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md), or [Node](functions-reference-node.md) developer references.</span></span>

## <a name="functionjson-for-sendgrid-bindings"></a><span data-ttu-id="4be49-110">function.json pour les liaisons SendGrid</span><span class="sxs-lookup"><span data-stu-id="4be49-110">function.json for SendGrid bindings</span></span>

<span data-ttu-id="4be49-111">Azure Functions fournit une liaison de sortie pour SendGrid.</span><span class="sxs-lookup"><span data-stu-id="4be49-111">Azure Functions provides an output binding for SendGrid.</span></span> <span data-ttu-id="4be49-112">La liaison de sortie SendGrid vous permet de créer et d’envoyer un e-mail par programmation.</span><span class="sxs-lookup"><span data-stu-id="4be49-112">The SendGrid output binding enables you to create and send email programmatically.</span></span> 

<span data-ttu-id="4be49-113">La liaison SendGrid prend en charge les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="4be49-113">The SendGrid binding supports the following properties:</span></span>

- <span data-ttu-id="4be49-114">`name` : obligatoire - nom de variable utilisé dans le code de la fonction pour la demande ou dans le corps de la demande.</span><span class="sxs-lookup"><span data-stu-id="4be49-114">`name` : Required - the variable name used in function code for the request or request body.</span></span> <span data-ttu-id="4be49-115">Cette valeur est ```$return``` lorsqu’il n’existe qu’une valeur de retour.</span><span class="sxs-lookup"><span data-stu-id="4be49-115">This value is ```$return``` when there is only one return value.</span></span> 
- <span data-ttu-id="4be49-116">`type` : obligatoire - doit être « SendGrid ».</span><span class="sxs-lookup"><span data-stu-id="4be49-116">`type` : Required - must be set to "sendGrid."</span></span>
- <span data-ttu-id="4be49-117">`direction` : obligatoire - doit être « out ».</span><span class="sxs-lookup"><span data-stu-id="4be49-117">`direction` : Required - must be set to "out."</span></span>
- <span data-ttu-id="4be49-118">`apiKey` :obligatoire - doit correspondre au nom de votre clé API stockée dans les paramètres d’application de Function App.</span><span class="sxs-lookup"><span data-stu-id="4be49-118">`apiKey` : Required - must be set to the name of your API key stored in the Function App's app settings.</span></span>
- <span data-ttu-id="4be49-119">`to` : adresse e-mail du destinataire.</span><span class="sxs-lookup"><span data-stu-id="4be49-119">`to` : the recipient's email address.</span></span>
- <span data-ttu-id="4be49-120">`from` : adresse e-mail de l’expéditeur.</span><span class="sxs-lookup"><span data-stu-id="4be49-120">`from` : the sender's email address.</span></span>
- <span data-ttu-id="4be49-121">`subject` : objet de l’e-mail.</span><span class="sxs-lookup"><span data-stu-id="4be49-121">`subject` : the subject of the email.</span></span>
- <span data-ttu-id="4be49-122">`text` : contenu de l’e-mail.</span><span class="sxs-lookup"><span data-stu-id="4be49-122">`text` : the email content.</span></span>

<span data-ttu-id="4be49-123">Exemple de code **function.json** :</span><span class="sxs-lookup"><span data-stu-id="4be49-123">Example of **function.json**:</span></span>

```json 
{
    "bindings": [
        {
            "name": "$return",
            "type": "sendGrid",
            "direction": "out",
            "apiKey" : "MySendGridKey",
            "to": "{ToEmail}",
            "from": "{FromEmail}",
            "subject": "SendGrid output bindings"
        }
    ]
}
```

> [!NOTE]
> <span data-ttu-id="4be49-124">Azure Functions stocke vos informations de connexion et les clés API en tant que paramètres d’application, de sorte qu’elles ne soient pas vérifiées dans votre référentiel de contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="4be49-124">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="4be49-125">Ceci protège vos informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="4be49-125">This action safeguards your sensitive information.</span></span>
>
>

## <a name="c-example-of-the-sendgrid-output-binding"></a><span data-ttu-id="4be49-126">Exemple de liaison de sortie SendGrid en C#</span><span class="sxs-lookup"><span data-stu-id="4be49-126">C# example of the SendGrid output binding</span></span>

```csharp
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static Mail Run(TraceWriter log, string input, out Mail message)
{
     message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    personalization.AddTo(new Email("recipient@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

## <a name="node-example-of-the-sendgrid-output-binding"></a><span data-ttu-id="4be49-127">Exemple de liaison de sortie SendGrid en Node</span><span class="sxs-lookup"><span data-stu-id="4be49-127">Node example of the SendGrid output binding</span></span>

```javascript
module.exports = function (context, input) {    
    var message = {
         "personalizations": [ { "to": [ { "email": "sample@sample.com" } ] } ],
        from: "sender@contoso.com",        
        subject: "Azure news",
        content: [{
            type: 'text/plain',
            value: input
        }]
    };

    context.done(null, message);
};

```

## <a name="next-steps"></a><span data-ttu-id="4be49-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4be49-128">Next steps</span></span>
<span data-ttu-id="4be49-129">Pour obtenir des informations sur les autres liaisons et déclencheurs pour Azure Functions, consultez :</span><span class="sxs-lookup"><span data-stu-id="4be49-129">For information about other bindings and triggers for Azure Functions, see</span></span> 
- [<span data-ttu-id="4be49-130">Informations de référence pour les développeurs sur les déclencheurs et liaisons Azure Functions</span><span class="sxs-lookup"><span data-stu-id="4be49-130">Azure Functions triggers and bindings developer reference</span></span>](functions-triggers-bindings.md)

- <span data-ttu-id="4be49-131">[Meilleures pratiques pour Azure Functions](functions-best-practices.md) répertorie les meilleures pratiques à utiliser lors de la création de fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="4be49-131">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices to use when creating Azure Functions.</span></span>

- <span data-ttu-id="4be49-132">[Référence du développeur Azure Functions](functions-reference.md) Référence du programmeur pour le codage de fonctions et la définition de déclencheurs et de liaisons.</span><span class="sxs-lookup"><span data-stu-id="4be49-132">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>
