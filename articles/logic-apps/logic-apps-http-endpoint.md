---
title: "aaaCall, déclencheur, ou imbriquer des flux de travail avec des points de terminaison HTTP - Azure Logic Apps | Documents Microsoft"
description: "Configurer toocall de points de terminaison HTTP, le déclencheur ou imbriquer le flux de travail pour Azure Logic Apps"
services: logic-apps
keywords: workflows, points de terminaison HTTP
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 73ba2a70-03e9-4982-bfc8-ebfaad798bc2
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 03/31/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 072a314c3bff75ab7696f86bb063bb7c03c4ae89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a>Appeler, déclencher ou imbriquer des workflows via des points de terminaison HTTP dans des applications logiques

Vous pouvez exposer en mode natif les points de terminaison HTTP synchrones en tant que déclencheurs sur des applications logiques, afin que vous puissiez déclencher ou appeler vos applications logiques via une URL. Vous pouvez également imbriquer des workflows dans vos applications logiques à l’aide d’un modèle de points de terminaison pouvant être appelés.

points de terminaison HTTP toocreate, vous pouvez ajouter ces déclencheurs afin que vos applications logiques peuvent recevoir des demandes entrantes :

* [Requête](../connectors/connectors-native-reqres.md)

* [Déclencheur ApiConnectionWebhook](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [Déclencheur HTTPWebhook](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > Bien que nos exemples utilisent hello **demande** déclencheur, vous pouvez utiliser une des hello répertoriés déclencheurs HTTP, et tous les principes de façon identique s’appliquent toohello autres types de déclencheurs.

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a>Configurer un point de terminaison HTTP pour votre application logique

toocreate un point de terminaison HTTP, ajoutez un déclencheur qui peut recevoir des demandes entrantes.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com "portail Azure"). Accédez tooyour logique application et ouvrez le Concepteur de la logique d’application.

2. Ajoutez un déclencheur qui permet à votre application logique de recevoir des requêtes entrantes. Par exemple, ajouter hello **demande** application logique de tooyour déclencheur.

3.  Sous **demander un schéma JSON corps**, vous pouvez éventuellement entrer un schéma JSON pour la charge utile de la hello (données) que vous attendez hello déclencheur tooreceive.

    le Concepteur de Hello utilise ce schéma pour générer des jetons que votre application de la logique peut utiliser tooconsume, parse et passer les données à partir de déclencheur hello via votre flux de travail. 
    Cliquez sur le lien renvoyant à la section [Jetons générés à partir de schémas JSON pour votre application logique](#generated-tokens) pour en savoir plus.

    Pour cet exemple, entrez le schéma hello indiqué dans le Concepteur de hello :

    ```json
    {
      "type": "object",
      "properties": {
        "address": {
          "type": "string"
        }
      },
      "required": [
        "address"
      ]
    }
    ```

    ![Ajouter une action de demande hello][1]

    > [!TIP]
    > 
    > Vous pouvez générer un schéma pour une charge utile JSON d’exemple à partir d’un outil tel que [jsonschema.net](http://jsonschema.net/), ou Bonjour **demande** déclencheur en choisissant **utilisez exemple charge utile toogenerate de schéma**. 
    > Entrez votre exemple de charge utile et choisissez **Terminé**.

    Par exemple, cet exemple de charge utile :

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    génère ce schéma :

    ```json
    }
       "type": "object",
       "properties": {
          "address": {
             "type": "string" 
          }
       }
    }
    ```

4.  Enregistrez votre application logique. Sous **HTTP POST toothis URL**, vous devez maintenant rechercher une URL de rappel généré, comme dans cet exemple :

    ![URL de rappel générée pour le point de terminaison](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    Cette URL contient une clé de Signature d’accès partagé (SAS) dans les paramètres de requête hello qui sont utilisés pour l’authentification. 
    Vous pouvez également obtenir l’URL de point de terminaison HTTP hello à partir de votre présentation de l’application logique Bonjour portail Azure. Sous **Historique du déclencheur**, sélectionnez votre déclencheur :

    ![Obtenir l’URL de point de terminaison HTTP à partir du portail Azure][2]

    Ou vous pouvez obtenir les URL de hello par cet appel :

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-hello-http-method-for-your-trigger"></a>Modifier la méthode HTTP de hello pour votre déclencheur

Par défaut, hello **demande** déclencheur attend une demande HTTP POST, mais vous pouvez utiliser une méthode HTTP différente. 

> [!NOTE]
> Vous pouvez spécifier un seul type de méthode.

1. Sur votre déclencheur de **requête**, choisissez **Afficher les options avancées**.

2. Ouvrez hello **méthode** liste. Dans cet exemple, sélectionnez **GET** pour pouvoir tester ultérieurement l’URL de votre point de terminaison HTTP.

    > [!NOTE]
    > Vous pouvez sélectionner n’importe quelle autre méthode HTTP, ou spécifier une méthode personnalisée pour votre propre application logique.

    ![Changer de méthode HTTP](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a>Accepter les paramètres via votre URL de point de terminaison HTTP

Lorsque vous souhaitez que vos paramètres de tooaccept de URL de point de terminaison HTTP, personnaliser les chemin d’accès relatif de votre déclencheur.

1. Sur votre déclencheur de **requête**, choisissez **Afficher les options avancées**. 

2. Sous **méthode**, spécifiez la méthode hello HTTP que vous souhaitez toouse de votre demande. Dans cet exemple, sélectionnez hello **obtenir** méthode, si vous n’avez pas déjà fait, afin que vous puissiez tester URL du votre point de terminaison HTTP.

      > [!NOTE]
      > Lorsque vous spécifiez un chemin d’accès relatif pour votre déclencheur, vous devez également spécifier explicitement une méthode HTTP pour votre déclencheur.

3. Sous **chemin d’accès relatif**, spécifiez le chemin d’accès relatif de hello pour le paramètre hello que votre URL doit accepter, par exemple, `customers/{customerID}`.

    ![Spécifiez la méthode HTTP de hello et chemin d’accès relatif pour le paramètre](./media/logic-apps-http-endpoint/relativeurl.png)

4. toouse hello paramètre, ajoutez un **réponse** action tooyour logique application. (Sous votre déclencheur, choisissez **Nouvelle étape** > **Ajouter une action** > **Response**) 

5. Dans votre réponse **corps**, incluent le jeton hello pour le paramètre hello que vous avez spécifié dans le chemin d’accès relatif de votre déclencheur.

    Par exemple, tooreturn `Hello {customerID}`, mettre à jour de votre réponse **corps** avec `Hello {customerID token}`. 
    liste de contenu dynamique Hello doit apparaître et afficher hello `customerID` jeton pour vous tooselect.

    ![Ajoutez paramètre tooresponse corps](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    Votre valeur **Corps** doit ressembler à cet exemple :

    ![Corps de la réponse avec le paramètre](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. Enregistrez votre application logique. 

    Votre URL de point de terminaison HTTP inclut désormais les chemin d’accès relatif hello, par exemple : 

    https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...

7. tootest votre point de terminaison HTTP, copier- coller hello URL mise à jour dans une autre fenêtre de navigateur, mais remplacent `{customerID}` avec `123456`, puis appuyez sur ENTRÉE.

    Votre navigateur doit afficher le texte suivant : 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a>Jetons générés à partir de schémas JSON pour votre application logique

Lorsque vous fournissez un schéma JSON dans votre **demande** déclencher, hello Concepteur de logique d’application génère des jetons pour les propriétés de ce schéma. Vous pouvez ensuite utiliser ces jetons pour transmettre des données au workflow de votre application logique.

Pour cet exemple, si vous ajoutez hello `title` et `name` de schéma de propriété tooyour JSON, leurs jetons sont désormais disponible toouse dans les étapes ultérieures de flux de travail. 

Voici le schéma JSON hello complet :

```json
{
   "type": "object",
   "properties": {
      "address": {
         "type": "string"
      },
      "title": {
         "type": "string"
      },
      "name": {
         "type": "string"
      }
   },
   "required": [
      "address",
      "title",
      "name"
   ]
}
```

## <a name="create-nested-workflows-for-logic-apps"></a>Créer des workflows imbriqués pour les applications logiques

Vous pouvez imbriquer des workflows dans votre application logique en ajoutant d’autres applications logiques qui peuvent recevoir des requêtes. tooinclude ces applications logique, ajouter hello **Azure Logic Apps - choisissez un flux de travail Logic Apps** déclencheur tooyour d’action. Vous pouvez ensuite choisir entre des applications logiques éligibles.

![Ajouter une autre application logique](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a>Appeler ou déclencher des applications logiques via des points de terminaison HTTP

Après avoir créé votre point de terminaison HTTP, vous pouvez déclencher votre application logique via un `POST` méthode toohello une URL complète. Les applications logiques ont une prise en charge intégrée pour les points de terminaison à accès direct.

## <a name="reference-content-from-an-incoming-request"></a>Référencer le contenu à partir d’une requête entrante

Si le contenu de hello de type est `application/json`, vous pouvez référencer des propriétés à partir de la demande entrante de hello. Sinon, le contenu est traité comme une seule unité binaire que vous pouvez passer tooother API. tooreference ce contenu à l’intérieur du flux de travail hello, vous devez convertir ce contenu. Par exemple, si vous passez `application/xml` contenu, vous pouvez utiliser `@xpath()` pour l’extraction de XPath, ou `@json()` pour la conversion XML tooJSON. Découvrez plus en détail comment [utiliser les types de contenu](../logic-apps/logic-apps-content-type.md).

tooget hello la sortie à partir d’une demande entrante, vous pouvez utiliser hello `@triggerOutputs()` (fonction). sortie de Hello peut ressembler à cet exemple :

```json
{
    "headers": {
        "content-type" : "application/json"
    },
    "body": {
        "myProperty" : "property value"
    }
}
```

tooaccess hello `body` propriété en particulier, vous pouvez utiliser hello `@triggerBody()` contextuel. 

## <a name="respond-toorequests"></a>Répondre toorequests

Vous souhaiterez peut-être toorespond toocertain demandes qui démarre une application logique en retournant du contenu toohello appelant. code d’état tooconstruct hello, en-tête et corps de réponse, vous pouvez utiliser hello **réponse** action. Cette action peut apparaître n’importe où dans votre application logique, pas seulement à la fin de hello de votre flux de travail.

> [!NOTE] 
> Si votre application logique n’inclut pas un **réponse**, point de terminaison hello HTTP répond *immédiatement* avec un **202 accepté** état. En outre, pour hello d’origine demande tooget hello réponse, toutes les étapes nécessaires pour la réponse de hello doivent se terminer en hello [limite de délai d’attente de demandes](./logic-apps-limits-and-config.md) sauf si vous appelez workflow hello comme application logique imbriquées. Si aucune réponse se produit au sein de cette limite, la demande entrante de hello arrive à expiration et reçoit la réponse de hello HTTP **408 délai d’expiration du Client**. Pour les applications de la logique imbriquées, hello parent logique application continue toowait d’une réponse jusqu'à la fin, quel que soit le temps est nécessaire.

### <a name="construct-hello-response"></a>Construire la réponse de hello

Vous pouvez inclure plusieurs en-têtes et tout type de contenu dans le corps de la réponse hello. Dans notre exemple de réponse, l’en-tête de hello Spécifie que réponse de hello possède le type de contenu `application/json`. et hello corps contient `title` et `name`, basé sur un schéma JSON hello mis à jour pour hello **demande** déclencheur.

![Action HTTP Response][3]

Les réponses ont ces propriétés :

| Propriété | Description |
| --- | --- |
| statusCode |Spécifie le code d’état HTTP de hello pour la demande entrante si toohello ne répond. Ce code peut être tout code d’état valide commençant par 2xx, 4xx ou 5xx. Cependant, les codes d’état 3xx ne sont pas autorisés. |
| headers |Définit un nombre quelconque de tooinclude d’en-têtes dans la réponse de hello. |
| body |Indique un objet corps qui peut être une chaîne, un objet JSON ou même du contenu binaire référencé à partir d’une étape précédente. |

Voici le schéma JSON hello ressemble maintenant pour hello **réponse** action :

``` json
"Response": {
   "inputs": {
      "body": {
         "title": "@{triggerBody()?['title']}",
         "name": "@{triggerBody()?['name']}"
      },
      "headers": {
           "content-type": "application/json"
      },
      "statusCode": 200
   },
   "runAfter": {},
   "type": "Response"
}
```

> [!TIP]
> définition complète JSON tooview hello pour votre application logique, sur hello Concepteur de logique d’application, choisissez **mode Code**.

## <a name="q--a"></a>Questions et réponses

#### <a name="q-what-about-url-security"></a>Q : Qu’en est-il de la sécurité de l’URL ?

R : Les URL de rappel de l’application logique sont générées de façon sécurisée par Azure via une signature d’accès partagé (SAP). Cette signature est transmise directement comme paramètre de requête et doit être validée avant que votre application logique puisse être déclenchée. Azure génère la signature hello à l’aide d’une combinaison unique d’une clé secrète par application logique, le nom de déclencheur hello et opération hello qui est effectuée. Par conséquent, sauf si une personne a la clé d’application logique secrète accès toohello, ils ne peut pas générer une signature valide.

   > [!IMPORTANT]
   > Systèmes sécurisés et de production, il est fortement recommandé par rapport à l’appel de votre application logique directement à partir de navigateur de hello, car :
   > 
   > * clé d’accès partagé Hello s’affiche dans l’URL de hello.
   > * Vous ne peut pas gérer les stratégies de contenu sécurisées en raison des domaines tooshared entre les clients de l’application logique.

#### <a name="q-can-i-configure-http-endpoints-further"></a>Q : Puis-je configurer des points de terminaison HTTP de façon plus poussée ?

R : Oui, les points de terminaison HTTP prennent en charge une configuration plus avancée via [**Gestion des API**](../api-management/api-management-key-concepts.md). Ce service offre également la possibilité de hello pour tooconsistently vous gérez toutes les API, y compris les applications de la logique, paramétrer des noms de domaine personnalisé, utiliser plusieurs méthodes d’authentification et plus d’informations, par exemple :

* [Méthode de demande de modification hello](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [Modifier les segments d’URL hello de demande de hello](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* Configurer vos domaines de la gestion des API Bonjour [portail Azure](https://portal.azure.com/ "portail Azure")
* Configurer toocheck de stratégie pour l’authentification de base

#### <a name="q-what-changed-when-hello-schema-migrated-from-hello-december-1-2014-preview"></a>Q : qu’est changé lorsque le schéma de hello migré à partir de la version préliminaire du 1er décembre 2014 hello ?

R : Voici un résumé des modifications apportées :

| Version préliminaire du 1er décembre 2014 | 1er juin 2016 |
| --- | --- |
| Cliquez sur l’application API **Écouteur HTTP** |Cliquez sur **Déclenchement manuel** (aucune application API nécessaire) |
| Paramètre d’écouteur HTTP «*Envoie une réponse automatiquement*» |Soit inclure un **réponse** action ou pas dans la définition de workflow hello |
| Configurez l’authentification de base ou OAuth |via la gestion des API |
| Configurer la méthode HTTP |Sous **Afficher les options avancées**, choisissez une méthode HTTP |
| Configurer le chemin d’accès relatif |Sous **Afficher les options avancées**, ajoutez un chemin d’accès relatif |
| Corps d’entrants hello référence via`@triggerOutputs().body.Content` |Référencez via `@triggerOutputs().body` |
| **Envoyer la réponse HTTP** action sur hello écouteur HTTP |Cliquez sur **répondre tooHTTP demande** (aucune application API n’obligatoire) |

## <a name="get-help"></a>Obtenir de l’aide

tooask questions, répondre aux questions et savoir quels autres Azure Logic Apps font les utilisateurs, visitez hello [forum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp améliorer Azure Logic Apps et connecteurs, voter pour ou envoyer vos idées à hello [site de commentaires utilisateur Azure Logic Apps](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Étapes suivantes

* [Créer des définitions d’application logique](./logic-apps-author-definitions.md)
* [Gérer les erreurs et exceptions](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
