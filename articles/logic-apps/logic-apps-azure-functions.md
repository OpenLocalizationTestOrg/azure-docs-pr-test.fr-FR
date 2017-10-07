---
title: code aaaCustom pour Azure Logic Apps avec des fonctions de Azure | Documents Microsoft
description: "Création et exécution d’un code personnalisé pour Azure Logic Apps avec Azure Functions"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 18b3821ed7e434feb568b9b96e9a5a2189dba3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a>Ajout et exécution d’un code personnalisé pour des applications logiques avec Azure Functions

extraits de code personnalisés toorun de c# ou node.js dans les applications de la logique, vous pouvez créer des fonctions personnalisées au moyen de fonctions de Azure. 
[Azure Functions](../azure-functions/functions-overview.md) assure le calcul sans serveur dans Microsoft Azure, et est utile pour effectuer ces tâches :

* Mise en forme avancée ou calcul de champs dans les applications logiques
* Effectuez les calculs dans un workflow.
* Étendre les fonctionnalités de l’application hello logique avec des fonctions qui sont prises en charge en c# ou node.js

## <a name="create-custom-functions-for-your-logic-apps"></a>Création de fonctions personnalisées pour vos applications logiques

Nous vous recommandons de créer une fonction dans le portail Azure fonctions hello, à partir de hello **Webhook générique - nœud** ou **Webhook - générique c#** modèles. résultat de Hello crée un rempli automatiquement un modèle qui accepte `application/json` à partir d’une application logique. Les fonctions que vous créez à partir de ces modèles sont détectées automatiquement et s’affichent dans hello de concepteur d’application logique sous **fonctions Azure dans ma région.**

Bonjour portail Azure, sur hello **intégrer** volet de votre fonction, votre modèle doit montrer que **Mode** défini trop**Webhook** et **Webhook type** est défini trop**JSON générique**. 

Les fonctions de Webhook accepter une demande et passez-la dans la méthode hello via un `data` variable. Vous pouvez accéder à des propriétés de hello de votre charge utile à l’aide de notation par points comme `data.function-name`. Par exemple, une fonction JavaScript simple qui convertit une valeur DateTime en une chaîne de date se présente comme hello l’exemple suivant :

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a>Appeler Azure Functions à partir d’applications logiques

conteneurs de hello toolist dans votre abonnement et la fonction hello select que vous souhaitez toocall, dans le Concepteur d’application logique, cliquez sur hello **Actions** , puis sélectionnez à partir de **fonctions Azure dans ma région**.

Après avoir sélectionné la fonction hello, vous êtes invité toospecify un objet de la charge utile d’entrée. Cet objet est un message de type hello hello logique application envoie toohello fonction et doit être un objet JSON. Par exemple, si vous souhaitez toopass Bonjour **de dernière modification** date à partir d’un déclencheur de Salesforce, charge utile de fonction hello peut se présenter à l’exemple suivant :

![Date de dernière modification][1]

## <a name="trigger-logic-apps-from-a-function"></a>Déclencher des applications logiques à partir d’une fonction

Vous pouvez déclencher une application logique dans une fonction. Consultez [Applications logiques en tant que points de terminaison pouvant être appelés](logic-apps-http-endpoint.md). Créer une application de la logique qui comporte un déclencheur manuel, puis à partir de votre fonction, générer une URL de déclenchement manuel toohello HTTP POST avec une charge utile hello qui que vous souhaitez envoyer toohello logique application.

### <a name="create-a-function-from-logic-app-designer"></a>Création d’une fonction à partir du concepteur d’applications logiques

Vous pouvez également créer une fonction de webhook node.js à partir du concepteur hello. Tout d’abord, sélectionnez **Azure Functions in my Region** (Azure Functions dans ma région) et choisissez un conteneur pour votre fonction. Si vous n’avez pas encore un conteneur, vous devez toocreate une à partir de hello [portal de fonctions d’Azure](https://functions.azure.com/signin). Sélectionnez ensuite **Créer**.  

toogenerate un modèle basé sur les données de salutation que vous souhaitez toocompute, spécifiez l’objet de contexte hello que vous envisagez de toopass dans une fonction. Cet objet doit être un objet JSON. Par exemple, si vous passez dans le contenu du fichier hello à partir d’une action de FTP, charge utile de contexte hello ressemble à l’exemple suivant :

![Charge utile de contexte][2]

> [!NOTE]
> Étant donné que cet objet n’a pas été converti en une chaîne, le contenu hello est ajouté directement charge utile JSON de toohello. Toutefois, une erreur se produit si l’objet de hello n’est pas un jeton JSON (autrement dit, une chaîne ou JSON/tableau d’objets). objet de hello toocast sous forme de chaîne, ajouter des guillemets comme indiqué dans la première illustration de hello dans cet article.
> 

le Concepteur de Hello génère ensuite un modèle de fonction que vous pouvez créer en ligne. Les variables sont créés au préalable en fonction de contexte hello que vous envisagez de toopass dans la fonction hello.

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
