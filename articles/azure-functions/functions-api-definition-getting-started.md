---
title: "aaaGetting démarré avec OpenAPI Metadata dans les fonctions Azure | Documents Microsoft"
description: "Prise en main de la prise en charge d’OpenAPI dans Azure Functions"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/23/2017
ms.author: alkarche
ms.openlocfilehash: fee3464c9a0a11b6d3891ccd0e9c5343d6bedcad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a>Création de métadonnées OpenAPI 2.0 (Swagger) pour une Function App (version préliminaire)

Ce document vous guide tout au long des processus d’étape par étape de hello de création d’une définition de OpenAPI pour une API simple hébergée sur les fonctions d’Azure.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a>Qu’est-ce qu’OpenAPI (Swagger) ?
[Métadonnées de swagger](http://swagger.io/) est un fichier qui définit les fonctionnalités de hello et modes de votre API de fonctionnement et permet à une fonction qui héberge un toobe de l’API REST utilisée par un grand nombre d’autres logiciels. Offres Microsoft telles que PowerApps et [applications API](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), ainsi que de 3 développeur tiers tels que des outils [Postman](https://www.getpostman.com/docs/importing_swagger) et [de nombreux packages plus](http://swagger.io/tools/) tous les autoriser votre toobe API consommée avec un Définition swagger.

## <a name="prepare-function"></a>Création d’une fonction avec une API simple
  toocreate une définition OpenAPI, nous devons tout d’abord toocreate une fonction avec une API simple. Si vous avez déjà une API hébergée sur une application de la fonction, vous pouvez ignorer la section suivante de droite toohello
1. Créez une nouvelle Function App.
    1. [Portail Azure](https://portal.azure.com) > `+ New` &gt; Recherchez « Function App »
1. Créer une nouvelle fonction de déclencheur HTTP à l’intérieur de votre nouvelle Function App
    1. Votre fonction est préremplie avec du code définissant une API REST très simple.
    1. N’importe quelle chaîne passée toohello fonction comme paramètre de requête ou dans le corps de hello est retourné en tant que « Hello {entrée} »
1. Accédez toohello `Integrate` onglet de votre nouvelle fonction de déclencheur de HTTP
    1. Activer/désactiver `Allowed HTTP methods` trop`Selected methods`
    1. Dans `Selected HTTP methods`, désactivez chaque verbe sauf POST.
    ![Méthodes HTTP sélectionnées](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)
    1. Cette étape simplifiera votre définition d’API.

## <a name="enable"></a>Activation de la prise en charge de la définition d’API
1. Accédez trop`your function name` > `Platform Features` > `API Definition`
![onglet Définition](./media/functions-api-definition-getting-started/definitiontab.png)
1. Définissez `API Definition Source` trop`Function (preview)`
    1. Cette étape permet à une suite d’options OpenAPI pour votre application de la fonction, y compris un point de terminaison de toohost un fichier OpenAPI à partir du domaine de votre application de fonction, une copie de la ligne de hello [OpenAPI éditeur](http://editor.swagger.io)et un générateur de définition de démarrage rapide.
![Définition activée](./media/functions-api-definition-getting-started/enabledefinition.png)

## <a name="create-definition"></a>Création de votre définition d’API à partir d’un modèle
1. Cliquez sur `Generate API Definition template`
    1. Cette étape analyse votre application de la fonction pour les fonctions de déclencheur de HTTP et utilise les informations de hello dans functions.json toogenerate un document OpenAPI.
1. Ajouter un objet de l’opération trop`paths: /api/yourfunctionroute post:`
    1. document de OpenAPI de démarrage rapide de Hello est un plan d’un document OpenAPI complète. Il requiert plusieurs métadonnées toobe une définition complète de OpenAPI, tels que les objets d’opération et les modèles de réponse.
    1. objet d’opération exemple Hello ci-dessous est remplie produit/consomme une section, un objet de paramètre et un objet de réponse.
    
    ```yaml
      post:
        operationId: /api/yourfunctionroute/post
        consumes: [application/json]
        produces: [application/json]
        parameters:
          - name: name
            in: body
            description: Your name
            x-ms-summary: Your name
            required: true
            schema:
              type: object
              properties:
                name:
                  type: string
        description: >-
          Replace with Operation Object
          #http://swagger.io/specification/#operationObject
        responses:
          '200':
            description: A Greeting
            x-ms-summary: Your name
            schema:
              type: string
        security:
          - apikeyQuery: []
    ```
    
    > [!NOTE]
    >  x-ms-summary fournit un nom d’affichage dans Logic Apps, Flow et PowerApps.
    >
    > Extraire [personnaliser votre définition Swagger pour PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn plus.

1. Cliquez sur `save` toosave vos modifications ![Ajout d’une définition de modèle](./media/functions-api-definition-getting-started/addingtemplate.png)

## <a name="use-definition"></a>Utilisation de votre définition d’API
1. Copiez votre `API definition URL` et collez-le dans un nouveau tooview d’onglet navigateur votre document OpenAPI brut.
1. Vous pouvez importer votre numéro tooany OpenAPI des outils de test et l’intégration à l’aide de cette URL.
    1. Nombre de ressources Azure est tooautomatically en mesure des importer à l’aide de votre document OpenAPI hello URL de définition d’API qui est enregistré dans les paramètres de votre application (fonction). Dans le cadre de hello `Function` source de définition d’API, nous mettre à jour cette url pour vous.


## <a name="test-definition"></a>À l’aide de tootest de l’interface utilisateur de Swagger hello votre définition de l’API
Testez outils intégrés dans la vue de l’interface utilisateur toohello de l’éditeur de définition d’API hello incorporé. Ajoutez votre clé API et l’utiliser hello `Try this operation` sous chaque méthode. Hello outil utilise vos demandes de hello tooformat définition d’API et des réponses réussies indique que votre définition est correcte.

### <a name="steps"></a>Étapes :

1. Copier votre clé d’API de fonction
    1. Hello API clé se trouve dans votre fonction de déclenchement HTTP sous `function name` > `Keys` > `Function Keys` 
   ![touche de fonction](./media/functions-api-definition-getting-started/functionkey.png)
1. Accédez toohello `API Definition` page.
    1. Cliquez sur `Authenticate` et ajoutez votre objet de sécurité clé toohello fonction API haut hello.
  ![Clé OpenAPI](./media/functions-api-definition-getting-started/definitionTest auth.png)
1. sélectionnez `/api/yourfunctionroute` > `POST`
1. Cliquez sur `Try it out` et entrez un nom tootest
1. Vous devriez voir un résultat RÉUSSITE sous `Pretty`
![Test de définition d’API](./media/functions-api-definition-getting-started/definitionTest.png)

## <a name="next-steps"></a>Étapes suivantes
* [Définition OpenAPI dans Vue d’ensemble de Functions](functions-api-definition.md)
  * Lire la documentation complète de hello pour plus d’informations sur la prise en charge OpenAPI.
* [Référence du développeur Azure Functions](functions-reference.md)  
  * Référence du programmeur pour le codage de fonctions et la définition de déclencheurs et de liaisons.
* [Référentiel GitHub Azure Functions](https://github.com/Azure/Azure-Functions/)
  * Découvrez hello fonctions GitHub toogive nous des commentaires sur la version préliminaire de hello API définition prise en charge. Créer un problème GitHub pour ce que vous voulez toosee mis à jour.
