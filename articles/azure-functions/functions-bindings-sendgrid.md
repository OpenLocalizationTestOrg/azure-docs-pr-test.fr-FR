---
title: liaisons de fonctions SendGrid aaaAzure | Documents Microsoft
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
ms.openlocfilehash: 10a3837875eb6ae18e6c789bcf64cc401cf5f26a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-sendgrid-bindings"></a><span data-ttu-id="058e7-103">Liaisons SendGrid dans Azure Functions</span><span class="sxs-lookup"><span data-stu-id="058e7-103">Azure Functions SendGrid bindings</span></span>

<span data-ttu-id="058e7-104">Cet article explique comment tooconfigure et de travailler avec des liaisons de SendGrid dans les fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="058e7-104">This article explains how tooconfigure and work with SendGrid bindings in Azure Functions.</span></span> <span data-ttu-id="058e7-105">Avec SendGrid, vous pouvez utiliser les fonctions Azure toosend personnalisé messagerie par programmation.</span><span class="sxs-lookup"><span data-stu-id="058e7-105">With SendGrid, you can use Azure Functions toosend customized email programmatically.</span></span>

<span data-ttu-id="058e7-106">Cet article fournit des informations de référence pour les développeurs Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="058e7-106">This article is reference information for Azure Functions developers.</span></span> <span data-ttu-id="058e7-107">Si vous êtes nouvelles fonctions tooAzure, commencer par hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="058e7-107">If you're new tooAzure Functions, start with hello following resources:</span></span>

<span data-ttu-id="058e7-108">[Créer votre première fonction Azure](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="058e7-108">[Create your first Azure Function](functions-create-first-azure-function.md).</span></span> 
<span data-ttu-id="058e7-109">Références pour les développeurs [C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md) ou [Node](functions-reference-node.md).</span><span class="sxs-lookup"><span data-stu-id="058e7-109">[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md), or [Node](functions-reference-node.md) developer references.</span></span>

## <a name="functionjson-for-sendgrid-bindings"></a><span data-ttu-id="058e7-110">function.json pour les liaisons SendGrid</span><span class="sxs-lookup"><span data-stu-id="058e7-110">function.json for SendGrid bindings</span></span>

<span data-ttu-id="058e7-111">Azure Functions fournit une liaison de sortie pour SendGrid.</span><span class="sxs-lookup"><span data-stu-id="058e7-111">Azure Functions provides an output binding for SendGrid.</span></span> <span data-ttu-id="058e7-112">Hello SendGrid sortie liaison vous permet de toocreate et envoyer un courrier électronique par programmation.</span><span class="sxs-lookup"><span data-stu-id="058e7-112">hello SendGrid output binding enables you toocreate and send email programmatically.</span></span> 

<span data-ttu-id="058e7-113">liaison de SendGrid Hello prend en charge hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="058e7-113">hello SendGrid binding supports hello following properties:</span></span>

- <span data-ttu-id="058e7-114">`name`: Obligatoire - Nom de la variable hello utilisée dans le code de fonction de requête de hello ou de corps de la demande.</span><span class="sxs-lookup"><span data-stu-id="058e7-114">`name` : Required - hello variable name used in function code for hello request or request body.</span></span> <span data-ttu-id="058e7-115">Cette valeur est ```$return``` lorsqu’il n’existe qu’une valeur de retour.</span><span class="sxs-lookup"><span data-stu-id="058e7-115">This value is ```$return``` when there is only one return value.</span></span> 
- <span data-ttu-id="058e7-116">`type`: Obligatoire - doit être défini trop « sendGrid ».</span><span class="sxs-lookup"><span data-stu-id="058e7-116">`type` : Required - must be set too"sendGrid."</span></span>
- <span data-ttu-id="058e7-117">`direction`: Obligatoire - doit être défini trop « sortie ».</span><span class="sxs-lookup"><span data-stu-id="058e7-117">`direction` : Required - must be set too"out."</span></span>
- <span data-ttu-id="058e7-118">`apiKey`: Obligatoire - doit être toohello nom de votre clé API stockée dans les paramètres de l’application de l’application hello (fonction).</span><span class="sxs-lookup"><span data-stu-id="058e7-118">`apiKey` : Required - must be set toohello name of your API key stored in hello Function App's app settings.</span></span>
- <span data-ttu-id="058e7-119">`to`: hello adresse de messagerie du destinataire.</span><span class="sxs-lookup"><span data-stu-id="058e7-119">`to` : hello recipient's email address.</span></span>
- <span data-ttu-id="058e7-120">`from`: hello adresse de messagerie de l’expéditeur.</span><span class="sxs-lookup"><span data-stu-id="058e7-120">`from` : hello sender's email address.</span></span>
- <span data-ttu-id="058e7-121">`subject`: objet hello de courrier électronique de hello.</span><span class="sxs-lookup"><span data-stu-id="058e7-121">`subject` : hello subject of hello email.</span></span>
- <span data-ttu-id="058e7-122">`text`: hello du contenu des e-mails.</span><span class="sxs-lookup"><span data-stu-id="058e7-122">`text` : hello email content.</span></span>

<span data-ttu-id="058e7-123">Exemple de code **function.json** :</span><span class="sxs-lookup"><span data-stu-id="058e7-123">Example of **function.json**:</span></span>

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
> <span data-ttu-id="058e7-124">Azure Functions stocke vos informations de connexion et les clés API en tant que paramètres d’application, de sorte qu’elles ne soient pas vérifiées dans votre référentiel de contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="058e7-124">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="058e7-125">Ceci protège vos informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="058e7-125">This action safeguards your sensitive information.</span></span>
>
>

## <a name="c-example-of-hello-sendgrid-output-binding"></a><span data-ttu-id="058e7-126">Liaison de sortie exemple c# de hello SendGrid</span><span class="sxs-lookup"><span data-stu-id="058e7-126">C# example of hello SendGrid output binding</span></span>

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

## <a name="node-example-of-hello-sendgrid-output-binding"></a><span data-ttu-id="058e7-127">Exemple de nœud de hello SendGrid de sortie de liaison</span><span class="sxs-lookup"><span data-stu-id="058e7-127">Node example of hello SendGrid output binding</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="058e7-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="058e7-128">Next steps</span></span>
<span data-ttu-id="058e7-129">Pour obtenir des informations sur les autres liaisons et déclencheurs pour Azure Functions, consultez :</span><span class="sxs-lookup"><span data-stu-id="058e7-129">For information about other bindings and triggers for Azure Functions, see</span></span> 
- [<span data-ttu-id="058e7-130">Informations de référence pour les développeurs sur les déclencheurs et liaisons Azure Functions</span><span class="sxs-lookup"><span data-stu-id="058e7-130">Azure Functions triggers and bindings developer reference</span></span>](functions-triggers-bindings.md)

- <span data-ttu-id="058e7-131">[Meilleures pratiques pour les fonctions Azure](functions-best-practices.md) répertorie certains meilleures toouse de pratiques lors de la création de fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="058e7-131">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices toouse when creating Azure Functions.</span></span>

- <span data-ttu-id="058e7-132">[Référence du développeur Azure Functions](functions-reference.md) Référence du programmeur pour le codage de fonctions et la définition de déclencheurs et de liaisons.</span><span class="sxs-lookup"><span data-stu-id="058e7-132">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>
