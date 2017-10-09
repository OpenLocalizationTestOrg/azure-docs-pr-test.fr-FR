---
title: aaaHow toouse SendGrid dans les fonctions de Azure | Documents Microsoft
description: "Montre comment toouse SendGrid dans les fonctions d’Azure"
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/31/2017
ms.author: rachelap
ms.openlocfilehash: a0ffdae04e5924c773d2d26427626fc1f570f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-sendgrid-in-azure-functions"></a>Comment toouse SendGrid dans les fonctions d’Azure

## <a name="sendgrid-overview"></a>Présentation de SendGrid

Prend en charge des fonctions Azure SendGrid sortie liaisons tooenable vos messages de messagerie fonctions toosend avec quelques lignes de code et un compte SendGrid.

toouse hello des API SendGrid dans une fonction d’Azure, vous devez avoir un [compte SendGrid](http://SendGrid.com). En outre, vous devez disposer d’une clé d’API SendGrid. Connectez-vous à tooyour compte SendGrid, puis cliquez sur **paramètres** puis **clé API** toogenerate une API clé. Gardez cette clé sous la main, car vous l’utiliserez dans une étape à venir.

Vous êtes maintenant prêt toocreate une application de la fonction d’Azure.

## <a name="create-an-azure-function-app"></a>Création d’une application Azure Function 

Les applications Azure Function sont des conteneurs pour une ou plusieurs fonctions Azure. Les fonctions Azure sont exactement cela : des fonctions. Chaque fonction Azure est liée tooone déclencheur, qui est un événement qui provoque hello fonction toorun.
Chaque fonction peut contenir un nombre quelconque de liaisons d’entrée ou de sortie. Les liaisons sont des services que vous pouvez utiliser dans une fonction. SendGrid est une sortie liaison vous pouvez utiliser toosend e-mail. 

1. Connectez-vous à toohello portail Azure et [créer une application de la fonction Azure](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) ou ouvrir une application existante de la fonction. 
2. Créez une fonction Azure. tookeep il simple, choisissez un déclencheur manuel et c#. 

 ![Création d’une fonction Azure](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a>Configuration de SendGrid pour une utilisation dans une application Azure Function

Vous devez stocker votre clé d’API SendGrid comme un toouse de paramètre d’application dans une fonction. champ de ApiKey Hello n’est pas votre clé API SendGrid réel, mais une application de paramètre, vous définissez et qui représente votre clé API réel. Votre clé est stockée de cette façon à des fins de sécurité, car elle est séparée de tout code et tous fichiers qui peuvent être consultés avec le contrôle de code source.

- Créez une clé **AppSettings** dans les **Paramètres de l’application** de votre application de fonction.

 ![Création d’une fonction Azure](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a>Configuration des liaisons de sortie SendGrid

SendGrid est disponible en tant que liaison de sortie de fonction Azure. liaison de sortie toocreate un SendGrid :

1. Accédez toohello **intégrer** onglet de la fonction hello Bonjour portail Azure.
2. Cliquez sur **nouvelle sortie** toocreate un SendGrid liaison de sortie.
3. Renseignez hello **clé API** et **nom de paramètre de Message** propriétés. Si vous le souhaitez, vous pouvez entrer hello maintenant les autres propriétés, ou à la place de leur code. Ces paramètres peuvent être utilisés comme valeurs par défaut.

 ![Configuration des liaisons de sortie SendGrid](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

Ajout d’une fonction de tooa liaison crée un fichier appelé **function.json** dans le dossier de votre fonction. Ce fichier contient tous les hello les mêmes informations que vous voyez dans hello la fonction Azure **intégrer** onglet, mais dans Json de format. Hello du paramètre **ApiKey**, **message**, et **de** champs créent hello suivant entrées Bonjour **function.json** fichier : 

```json
{
  "bindings": [    
    {
      "type": "sendGrid",
      "name": "message",
      "apiKey": "SendGridKey",
      "direction": "out",
      "from": "azure@contoso.com"
    }
  ],
  "disabled": false
}
```

Si vous préférez, vous pouvez modifier ce fichier vous-même directement.

Maintenant que vous avez créé et configuré les hello application de la fonction et la fonction, vous pouvez écrire un message électronique toosend de code hello.

## <a name="write-code-that-creates-and-sends-email"></a>Écriture du code qui crée et envoie un message électronique

Hello API SendGrid contient toutes les commandes de hello vous devez toocreate et envoyez un courrier électronique.  

- Remplacez le code hello fonction hello avec hello suivant de code :

```cs
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static void Run(TraceWriter log, string input, out Mail message)
{
    message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    // change tooemail of recipient
    personalization.AddTo(new Email("MoreEmailPlease@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

Avis hello première ligne contient hello ```#r``` directive qui référence l’assembly SendGrid de hello. Après cela, vous pouvez utiliser un ```using``` instruction toomore accéder facilement aux objets hello dans cet espace de noms. Dans le code hello, créer des instances de ```Mail```, ```Personalization```, et ```Content``` objets hello API SendGrid à partir de rédiger un message électronique de hello. Lorsque vous renvoyez le message de type hello, SendGrid effectue sa remise. 

Hello signature de la fonction contient également un supplémentaire, le paramètre de type out ```Mail``` nommé ```message```. Les liaisons d’entrée et de sortie s’expriment elles-mêmes en tant que paramètres de fonction dans le code. 

2. Testez votre code en cliquant sur **Test** et en entrant un message en hello **corps de la demande** champ, puis en cliquant sur hello **exécuter** bouton.

 ![Test de votre code](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. Vérifiez tooverify par courrier électronique que SendGrid envoyées par courrier électronique hello. Il doit atteindre l’adresse toohello dans le code hello à l’étape 1 et contient le message de type hello de hello **corps de la demande**.

## <a name="next-steps"></a>Étapes suivantes
Cet article a montré comment toouse hello SendGrid service toocreate et envoyer un courrier électronique. toolearn savoir plus sur l’utilisation de fonctions de Azure dans vos applications, consultez hello rubriques suivantes : 

- [Meilleures pratiques pour les fonctions Azure](functions-best-practices.md) répertorie certains meilleures toouse de pratiques lors de la création de fonctions d’Azure.

- [Référence du développeur Azure Functions](functions-reference.md) Référence du programmeur pour le codage de fonctions et la définition de déclencheurs et de liaisons.

- Le didacticiel [Test d’Azure Functions](functions-test-a-function.md) décrit plusieurs outils et techniques permettant de tester vos fonctions.