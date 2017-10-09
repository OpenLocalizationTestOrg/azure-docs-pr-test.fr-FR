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
# <a name="azure-functions-sendgrid-bindings"></a>Liaisons SendGrid dans Azure Functions

Cet article explique comment tooconfigure et de travailler avec des liaisons de SendGrid dans les fonctions d’Azure. Avec SendGrid, vous pouvez utiliser les fonctions Azure toosend personnalisé messagerie par programmation.

Cet article fournit des informations de référence pour les développeurs Azure Functions. Si vous êtes nouvelles fonctions tooAzure, commencer par hello suivant des ressources :

[Créer votre première fonction Azure](functions-create-first-azure-function.md). 
Références pour les développeurs [C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md) ou [Node](functions-reference-node.md).

## <a name="functionjson-for-sendgrid-bindings"></a>function.json pour les liaisons SendGrid

Azure Functions fournit une liaison de sortie pour SendGrid. Hello SendGrid sortie liaison vous permet de toocreate et envoyer un courrier électronique par programmation. 

liaison de SendGrid Hello prend en charge hello propriétés suivantes :

- `name`: Obligatoire - Nom de la variable hello utilisée dans le code de fonction de requête de hello ou de corps de la demande. Cette valeur est ```$return``` lorsqu’il n’existe qu’une valeur de retour. 
- `type`: Obligatoire - doit être défini trop « sendGrid ».
- `direction`: Obligatoire - doit être défini trop « sortie ».
- `apiKey`: Obligatoire - doit être toohello nom de votre clé API stockée dans les paramètres de l’application de l’application hello (fonction).
- `to`: hello adresse de messagerie du destinataire.
- `from`: hello adresse de messagerie de l’expéditeur.
- `subject`: objet hello de courrier électronique de hello.
- `text`: hello du contenu des e-mails.

Exemple de code **function.json** :

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
> Azure Functions stocke vos informations de connexion et les clés API en tant que paramètres d’application, de sorte qu’elles ne soient pas vérifiées dans votre référentiel de contrôle de code source. Ceci protège vos informations sensibles.
>
>

## <a name="c-example-of-hello-sendgrid-output-binding"></a>Liaison de sortie exemple c# de hello SendGrid

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

## <a name="node-example-of-hello-sendgrid-output-binding"></a>Exemple de nœud de hello SendGrid de sortie de liaison

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

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des informations sur les autres liaisons et déclencheurs pour Azure Functions, consultez : 
- [Informations de référence pour les développeurs sur les déclencheurs et liaisons Azure Functions](functions-triggers-bindings.md)

- [Meilleures pratiques pour les fonctions Azure](functions-best-practices.md) répertorie certains meilleures toouse de pratiques lors de la création de fonctions d’Azure.

- [Référence du développeur Azure Functions](functions-reference.md) Référence du programmeur pour le codage de fonctions et la définition de déclencheurs et de liaisons.
