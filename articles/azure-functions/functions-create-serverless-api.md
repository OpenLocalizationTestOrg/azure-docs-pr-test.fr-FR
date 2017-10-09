---
title: "aaaCreate une API sans serveur à l’aide des fonctions de Azure | Documents Microsoft"
description: "Comment toocreate une API sans serveur à l’aide des fonctions d’Azure"
services: functions
author: mattchenderson
manager: erikre
ms.service: functions
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: mahender
ms.custom: mvc
ms.openlocfilehash: 877e3b229d5477fc5fec594ccd284fb55d7f3c07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a>Créer une API sans serveur à l’aide d’Azure Functions

Dans ce didacticiel, vous allez apprendre comment les fonctions Azure vous permet de toobuild des API hautement évolutives. Fonctions Azure est fourni avec une collection intégrée HTTP et les liaisons qui rendent tooauthor facile à un point de terminaison dans une variété de langues, y compris Node.JS, c# et bien plus encore. Dans ce didacticiel, vous allez personnaliser un HTTP déclencheur toohandle des actions spécifiques dans votre conception de l’API. Vous allez également préparer le développement de votre API, l’intégration avec Proxys Azure Functions et la configuration d’API factices. Tout ceci s’effectue sur hello fonctions sans environnement de calcul, donc vous n’avez pas tooworry sur la mise à l’échelle des ressources, vous pouvez vous concentrer uniquement sur votre logique de l’API.

## <a name="prerequisites"></a>Composants requis 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

fonction qui en résulte Hello servira pour reste hello de ce didacticiel.

### <a name="sign-in-tooazure"></a>Connectez-vous à tooAzure

Ouvrez hello portail Azure. toodo, connectez-vous trop[https://portal.azure.com](https://portal.azure.com) avec votre compte Azure.

## <a name="customize-your-http-function"></a>Personnaliser une fonction HTTP

Par défaut, votre fonction a déclenché l’HTTP est configuré tooaccept n’importe quelle méthode HTTP. Il existe également une URL par défaut sous forme de hello `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`. Si vous avez suivi hello quickstart, puis `<funcname>` probablement similaire à « HttpTriggerJS1 ». Dans cette section, vous allez modifier les demandes de tooGET uniquement hello fonction toorespond sur `/api/hello` Router à la place. 

Accédez à fonction tooyour Bonjour portail Azure. Sélectionnez **intégrer** Bonjour barre de navigation gauche.

![Personnalisation d’une fonction HTTP](./media/functions-create-serverless-api/customizing-http.png)

Utilisez les paramètres de déclencheur HTTP tel que spécifié dans la table de hello.

| Champ | Exemple de valeur | Description |
|---|---|---|
| Méthodes HTTP autorisées | Méthodes sélectionnées | Détermine quelles méthodes HTTP peuvent être utilisé tooinvoke cette fonction |
| Méthodes HTTP sélectionnées | GET | Autorise uniquement sélectionné toobe de méthodes HTTP utilisées tooinvoke cette fonction |
| Modèle d’itinéraire | /hello | Détermine l’itinéraire est tooinvoke utilisé cette fonction |

Notez que vous n’avez pas inclus hello `/api` baser le préfixe de chemin d’accès dans le modèle d’itinéraire hello, comme cela est géré par un paramètre global.

Cliquez sur **Enregistrer**.

Pour plus d’informations sur la personnalisation des fonctions HTTP, consultez la page [Liaisons HTTP et de webhooks d’Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).

### <a name="test-your-api"></a>Tester l’API

Ensuite, testez votre toosee fonction qu’il fonctionne avec la surface de l’API nouvelle hello.

Accédez de page de développement toohello arrière en cliquant sur le nom de la fonction hello Bonjour barre de navigation gauche.

Cliquez sur **obtenir l’URL de la fonction** et copier l’URL de hello. Vous devez voir qu’il utilise hello `/api/hello` Router maintenant.

Copier l’URL hello dans un nouvel onglet de navigateur ou de votre client REST préféré. Les navigateurs utilisent GET par défaut.

Exécuter la fonction hello et vérifiez qu’il fonctionne. Vous devrez peut-être le paramètre « name » de hello tooprovide comme un code de démarrage rapide de requête chaîne toosatisfy hello.

Vous pouvez aussi essayer d’appeler le point de terminaison hello avec tooconfirm de méthode HTTP autre que la fonction hello n’est pas exécutée. Pour ce faire, vous devez toouse un client REST, telles que cURL, Postman ou Fiddler.

## <a name="proxies-overview"></a>Vue d’ensemble des proxys

Dans la section suivante de hello, vous affichera votre API via un proxy. Les proxys de fonctions Azure est une fonctionnalité d’aperçu qui vous permet de tooforward demande tooother des ressources. Vous définissez comme un point de terminaison HTTP avec le déclencheur d’HTTP, mais au lieu d’écrire le code tooexecute lorsque ce point de terminaison est appelée, vous fournissez une implémentation à distance de tooa URL. Cela vous permet de toocompose API plusieurs sources en une seule API qui est facile pour les clients tooconsume. Cela est particulièrement utile si vous souhaitez que votre API en tant que microservices toobuild.

Un proxy peut pointer tooany HTTP ressources, telles que :
- Azure Functions 
- Applications API dans [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)
- Conteneurs Docker dans [App Service sur Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)
- Toute autre API hébergée

toolearn en savoir plus sur les serveurs proxy, consultez [utilisation de proxys de fonctions Azure (aperçu)].

## <a name="create-your-first-proxy"></a>Créer un premier proxy

Dans cette section, vous allez créer un nouveau proxy qui sert comme un serveur frontal tooyour API globale. 

### <a name="setting-up-hello-frontend-environment"></a>Création d’un environnement de serveur frontal hello

Répétez les étapes de hello trop[créer une application de la fonction](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate une nouvelle application de la fonction dans laquelle vous allez créer votre proxy. Cette nouvelle application servira de serveur frontal de hello pour notre API et application de fonction hello que vous modifiiez précédemment servira d’un serveur principal.

Accédez tooyour nouvelle application frontale fonction dans le portail de hello.

Sélectionnez **Paramètres**. Puis basculer **activer des proxys de fonctions Azure (aperçu)** trop « sur ».

Sélectionnez **Paramètres de la plateforme** et choisissez **Paramètres de l’application**.

Faites défiler la liste trop**paramètres de l’application** et créer un nouveau paramètre avec la clé « HELLO_HOST ». Définir son hôte toohello de valeur de votre application de la fonction principale, telles que `<YourApp>.azurewebsites.net`. Il s’agit de partie de hello URL que vous avez copiée précédemment lorsque vous testez votre fonction HTTP. Vous devez faire référence à ce paramètre dans la configuration de hello plus tard.

> [!NOTE] 
> Paramètres de l’application sont recommandées pour hello hôte configuration tooprevent une dépendance codée en dur l’environnement pour le proxy de hello. À l’aide des paramètres de l’application signifie que vous pouvez déplacer la configuration du proxy hello entre les environnements et paramètres d’application propres à l’environnement hello seront appliqués.

Cliquez sur **Enregistrer**.

### <a name="creating-a-proxy-on-hello-frontend"></a>Création d’un proxy sur le serveur frontal de hello

Accédez tooyour arrière frontal fonction application dans le portail de hello.

Dans la navigation de gauche hello, cliquez sur hello signe plus le suivant '+' trop « Proxy (version préliminaire) ».

![Création d’un proxy](./media/functions-create-serverless-api/creating-proxy.png)

Utiliser les paramètres de proxy tel que spécifié dans la table de hello.

| Champ | Exemple de valeur | Description |
|---|---|---|
| Nom | HelloProxy | Nom convivial utilisé uniquement à des fins de gestion. |
| Modèle d’itinéraire | /api/hello | Détermine l’itinéraire est tooinvoke utilisé ce proxy |
| URL principale | https://%HELLO_HOST%/api/hello | Spécifie la demande de hello toowhich hello point de terminaison doit être utilisé comme proxy |

Notez que les serveurs proxy ne fournit pas de hello `/api` préfixe de chemin d’accès de base et ce doit être inclus dans le modèle d’itinéraire hello.

Hello `%HELLO_HOST%` syntaxe fait référence le paramètre d’application hello vous avez créé précédemment. Hello résolu QU'URL pointe tooyour (fonction) d’origine.

Cliquez sur **Créer**.

Vous pouvez essayer votre nouveau proxy par copie hello URL de Proxy et de le tester dans le navigateur de hello ou avec votre client HTTP favori.

## <a name="create-a-mock-api"></a>Créer une API factice

Ensuite, vous allez utiliser un toocreate proxy une API fictive pour votre solution. Cela permet le développement client tooprogress, sans avoir besoin de back-end hello entièrement implémentée. Dans le développement, créez une nouvelle application de fonction qui prend en charge cette logique et rediriger votre tooit proxy.

toocreate cette simulation d’API, nous allons créer un nouveau proxy, cette fois à l’aide de hello [éditeur de Service d’applications](https://github.com/projectkudu/kudu/wiki/App-Service-Editor). tooget démarré, accédez à application de fonction tooyour dans le portail de hello. Sélectionnez **Fonctionnalités de la plateforme** et **Éditeur App Service**. Cliquer sur ce bouton, hello App Service éditeur s’ouvre dans un nouvel onglet.

Sélectionnez `proxies.json` Bonjour barre de navigation gauche. Il s’agit de fichier hello qui stocke la configuration hello pour tous les proxys. Si vous utilisez une des hello [fonctions des méthodes de déploiement](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), c’est le fichier hello que vous voulez gérer dans le contrôle de code source. toolearn en savoir plus sur ce fichier, consultez [configuration avancée de proxys](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).

Si vous avez suivi jusqu'à présent, votre proxies.json doit ressembler à hello suivantes :

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        }
    }
}
```

Vous allez maintenant ajouter votre API factice. Remplacez votre fichier proxies.json par hello qui suit :

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        },
        "GetUserByName" : {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/users/{username}"
            },
            "responseOverrides": {
                "response.statusCode": "200",
                "response.headers.Content-Type" : "application/json",
                "response.body": {
                    "name": "{username}",
                    "description": "Awesome developer and master of serverless APIs",
                    "skills": [
                        "Serverless",
                        "APIs",
                        "Azure",
                        "Cloud"
                    ]
                }
            }
        }
    }
}
```

Cela ajoute un nouveau proxy, « GetUserByName », sans propriété de backendUri hello. Au lieu d’appeler une autre ressource, il modifie la réponse par défaut hello proxys à l’aide d’une substitution de la réponse. Les substitutions de demandes et de réponses peuvent également être utilisées en association avec une URL principale. Cela est particulièrement utile lorsque le système hérité proxy tooa, où vous devrez peut-être toomodify en-têtes, les paramètres de requête, etc. toolearn plus d’informations sur les remplacements de demande et de réponse, consultez [modification des demandes et réponses de proxys](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).

Tester votre API fictive en appelant hello `/api/users/{username}` point de terminaison à l’aide d’un navigateur ou votre client REST favori. Être vraiment tooreplace _{username}_ avec une valeur de chaîne représentant un nom d’utilisateur.

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris comment toobuild et personnaliser une API sur les fonctions d’Azure. Vous avez également appris comment toobring plusieurs API, y compris mocks, ensemble comme une surface API unifiée. Vous pouvez utiliser ces toobuild techniques des API complexes, tout en s’exécutant sur hello sans modèle fourni par les fonctions Azure de calcul.

Hello références suivantes peuvent être utiles lorsque vous développez votre API supplémentaire :

- [Liaisons HTTP et webhook Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- [utilisation de proxys de fonctions Azure (aperçu)]
- [Documenter une API Azure Functions (préversion)](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[utilisation de proxys de fonctions Azure (aperçu)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
