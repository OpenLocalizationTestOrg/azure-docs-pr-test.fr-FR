---
title: aaaWork avec les serveurs proxy dans les fonctions de Azure | Documents Microsoft
description: "Vue d’ensemble de la procédure toouse Proxies de fonctions Azure"
services: functions
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/11/2017
ms.author: mahender
ms.openlocfilehash: 4d94c89e8f8f2d2c771b01bae142bf9a4f3b7f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a>Utilisation de Azure Functions Proxies (version préliminaire)

> [!NOTE] 
> Azure Functions Proxies est actuellement disponible en version préliminaire. C’est gratuit tandis que dans l’aperçu, mais les fonctions standard facturation applique tooproxy exécutions. Pour plus d’informations, consultez [Tarification d’Azure Functions](https://azure.microsoft.com/pricing/details/functions/).

Cet article explique comment tooconfigure et fonctionnent avec les proxys de fonctions Azure. Cette fonctionnalité vous permet de spécifier des points de terminaison sur votre Function App implémentés par une autre ressource. Vous pouvez utiliser ces toobreak proxys une API volumineuse dans plusieurs applications de fonction (par exemple, une architecture de microservice), tout en présentant une surface API unique pour les clients.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <a name="enable"></a>Activation d’Azure Functions Proxies

Les proxies ne sont pas activés par défaut. Vous pouvez créer des proxys lors de la fonctionnalité de hello est désactivée, mais ils ne seront exécute pas. les proxys tooenable, hello suivant :

1. Ouvrez hello [portail Azure], puis passez tooyour fonction app.
2. Sélectionnez **Paramètres Function App**.
3. Commutateur **activer des proxys de fonctions Azure (aperçu)** trop**sur**.

Vous pouvez également revenir ici tooupdate hello proxy runtime que de nouvelles fonctionnalités sont disponibles.


## <a name="create"></a>Création d’un proxy

Cette section vous montre comment toocreate un proxy dans hello portal de fonctions.

1. Ouvrez hello [portail Azure], puis passez tooyour fonction app.
2. Dans le volet gauche de hello, sélectionnez **nouveau proxy**.
3. Entrez un nom pour votre proxy.
4. Configurer des hello de point de terminaison qui est exposé sur cette application de la fonction en spécifiant hello **modèle d’itinéraire** et **méthodes HTTP**. Ces paramètres comportent en fonction des règles de toohello pour [HTTP déclencheurs].
5. Ensemble hello **URL principal** tooanother le point de terminaison. Il peut s’agir d’une fonction dans une autre Function App ou bien de n’importe quelle autre API. Hello valeur ne doit pas toobe statique, et il peut référencer [paramètres de l’application] et [paramètres à partir de la demande du client d’origine hello].
6. Cliquez sur **Créer**.

Votre proxy existe désormais sous la forme d’un nouveau point de terminaison de votre application de fonction. À partir d’un point de vue du client, il est équivalent tooan HttpTrigger dans les fonctions d’Azure. Vous pouvez essayer votre nouveau proxy en copiant hello URL de Proxy et de test avec votre client HTTP favori.

## <a name="modify-requests-responses"></a>Modification de demandes et de réponses

Avec les serveurs proxy de fonctions Azure, vous pouvez modifier les requêtes tooand réponses de back-end hello. Ces transformations peuvent impliquer l’utilisation de variables, comme décrit dans la section [Utilisation de variables].

### <a name="modify-backend-request"></a>Modifier hello principal demande

Par défaut, demande de back-end hello est initialisée comme une copie de la demande d’origine de hello. En outre vous toosetting hello principal URL, vous pouvez apporter modifications toohello HTTP méthode, les en-têtes et les paramètres de chaîne de requête. Hello valeurs modifiées peuvent référencer [paramètres de l’application] et [paramètres à partir de la demande du client d’origine hello].

Il n’est actuellement pas possible de modifier les demandes du serveur principal via un portail. toolearn tooapply cette fonctionnalité à partir de proxies.json, voir [définir un objet requestOverrides].

### <a name="modify-response"></a>Modifier la réponse de hello

Par défaut, la réponse hello du client est initialisé comme une copie de la réponse du serveur principal hello. Vous pouvez apporter de code d’état de la réponse de modifications toohello, phrase de motif, en-têtes et corps. Hello valeurs modifiées peuvent référencer [paramètres de l’application], [paramètres à partir de la demande du client d’origine hello], et [paramètres de réponse du serveur principal hello].

Il n’est actuellement pas possible de modifier les réponses. toolearn tooapply cette fonctionnalité à partir de proxies.json, voir [définir un objet responseOverrides].

## <a name="using-variables"></a>Utilisation de variables

configuration Hello pour un serveur proxy n’a pas besoin toobe statique. Vous pouvez que celle-ci variables toouse à partir de la demande d’origine de hello, réponse de back-end hello ou paramètres de l’application.

### <a name="request-parameters"></a>Référencement des paramètres de la demande

Vous pouvez utiliser les paramètres de la demande comme entrées de propriété de l’URL principale toohello ou dans le cadre de la modification des demandes et réponses. Certains paramètres peuvent être liés à partir du modèle d’itinéraire hello qui est spécifié dans la configuration du proxy base hello et d’autres peuvent provenir de propriétés de la demande entrante de hello.

#### <a name="route-template-parameters"></a>Paramètres de modèle de routage
Paramètres qui sont utilisés dans le modèle d’itinéraire hello sont disponible toobe référencée par son nom. les noms de paramètre Hello sont placés entre accolades ({}).

Par exemple, si un proxy dispose d’un modèle d’itinéraire, tel que `/pets/{petId}`, hello principal URL peut inclure la valeur hello `{petId}`, comme dans `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`. Si modèle d’itinéraire hello se termine dans un caractère générique, tel que `/api/{*restOfPath}`, hello valeur `{restOfPath}` est une représentation de chaîne de hello restant de segments de chemin d’accès à partir de la demande entrante de hello.

#### <a name="additional-request-parameters"></a>Paramètres de demande supplémentaires
En outre toohello les paramètres de modèle d’itinéraire, hello valeurs suivantes peut être utilisée dans les valeurs de configuration :

* **{request.method}** : hello méthode HTTP qui est utilisé à la demande d’origine de hello.
* **{request.headers. \<HeaderName\>}**: un en-tête qui peut être lu à partir de la demande d’origine de hello. Remplacez  *\<HeaderName\>*  avec nom hello d’en-tête hello que vous souhaitez tooread. Si l’en-tête de hello n’est pas inclus dans la demande de hello, valeur de hello sera une chaîne vide hello.
* **{request.querystring. \<Nom_paramètre\>}**: un paramètre de chaîne de requête permettre être lus à partir de la demande d’origine de hello. Remplacez  *\<nom_paramètre\>*  avec nom hello du paramètre hello que vous souhaitez tooread. Si le paramètre hello n’est pas inclus dans la demande de hello, valeur de hello sera une chaîne vide hello.

### <a name="response-parameters"></a>Référencement des paramètres de réponse du serveur principal

Paramètres de réponse peuvent être utilisés dans le cadre de la modification de client de toohello réponse hello. Hello valeurs suivantes sont utilisables dans les valeurs de configuration :

* **{backend.response.statusCode}** : hello le code d’état HTTP retourné de réponse du serveur principal hello.
* **{backend.response.statusReason}** : phrase de motif hello HTTP qui est renvoyée en cas de réponse du serveur principal hello.
* **{backend.response.headers. \<HeaderName\>}**: un en-tête qui peut être lu à partir de la réponse du serveur principal hello. Remplacez  *\<HeaderName\>*  avec nom hello d’en-tête de hello souhaité tooread. Si l’en-tête de hello n’est pas inclus dans la demande de hello, valeur de hello sera une chaîne vide hello.

### <a name="use-appsettings"></a>Référencement des paramètres de l’application

Vous pouvez également référencer [paramètres d’application définis pour l’application de fonction hello](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) en entourant le nom du paramètre hello avec des signes de pourcentage (%).

Par exemple, une URL principale *https://%ORDER_PROCESSING_HOST%/api/orders* aurait « ORDER_PROCESSING_HOST % » remplacé par la valeur hello du paramètre de ORDER_PROCESSING_HOST hello.

> [!TIP] 
> Utilisez des paramètres d’application pour les hôtes de serveur principal lorsque vous avez plusieurs déploiements ou environnements de test. De cette façon, vous pouvez vous assurer que vous vous entretenez toujours toohello immédiatement fin pour cet environnement.

## <a name="advanced-configuration"></a>Configuration avancée

les proxys Hello que vous configurez sont stockés dans un fichier proxies.json, qui se trouve dans un répertoire d’application de fonction racine hello. Vous pouvez manuellement modifier ce fichier et le déployer dans le cadre de votre application quand vous utilisez une des hello [méthodes de déploiement](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) qui prend en charge des fonctions. fonctionnalité de Hello doit être [activé](#enable) pour toobe de fichier hello traité. 

> [!TIP] 
> Si vous n’avez pas défini un hello des méthodes de déploiement, vous pouvez également travailler avec fichier de proxies.json hello dans le portail de hello. Application de fonction tooyour accédez, sélectionnez **fonctionnalités de plateforme**, puis sélectionnez **éditeur de Service d’applications**. En procédant ainsi, vous pouvez afficher la structure de fichiers complète hello de votre application de la fonction et apporter des modifications.

Proxies.json est défini par un objet proxy, composé de proxys nommés et de leurs définitions. Vous pouvez éventuellement référencer un [schéma JSON](http://json.schemastore.org/proxies) de complétion de code si votre éditeur est compatible. Un exemple de fichier peut se présenter comme hello suivantes :

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>"
        }
    }
}
```

Chaque proxy a un nom convivial, tel que *proxy1* Bonjour précédent exemple. objet de définition de proxy Hello correspondant est défini par hello propriétés suivantes :

* **matchCondition**: obligatoire : un objet définissant les demandes hello qui déclenchent l’exécution de hello du proxy. Il contient deux propriétés partagées avec les [HTTP déclencheurs] :
    * _méthodes_: un tableau de méthodes hello HTTP qui hello proxy répond à. S’il n’est pas spécifié, le proxy de hello répond tooall les méthodes HTTP sur l’itinéraire de hello.
    * _itinéraire_: obligatoire : définit le modèle d’itinéraire hello, contrôle qui demande les URL de votre proxy répond à. Contrairement aux déclencheurs HTTP, il n’y a pas de valeur par défaut.
* **backendUri**: URL hello hello principal toowhich hello de demande de ressource doit être traitée. Cette valeur peut référencer des paramètres d’application et les paramètres à partir de la demande du client d’origine hello. Si cette propriété n’est pas incluse, Azure Functions répond avec un message HTTP 200 OK.
* **requestOverrides**: un objet qui définit la demande de transformations toohello back-end. Consultez la section [définir un objet requestOverrides].
* **responseOverrides**: un objet qui définit la réponse de transformations toohello client. Consultez la section [définir un objet responseOverrides].

> [!NOTE] 
> propriété d’itinéraire Hello Proxies de fonctions Azure ne respecte pas la propriété de préfixe d’itinéraire hello de configuration de l’hôte fonctions hello. Si vous voulez tooinclude un préfixe tel que/API, il doit être inclus dans la propriété d’itinéraire hello.

### <a name="requestOverrides"></a>Définition d’un objet requestOverrides

objet de requestOverrides Hello définit les modifications apportées toohello demande lors de la ressource principale de hello est appelée. objet de Hello est défini par hello propriétés suivantes :

* **backend.Request.Method**: hello méthode HTTP qui a utilisé le principal hello toocall.
* **backend.Request.QueryString. \<Nom_paramètre\>**: un paramètre de chaîne de requête qui peut être défini pour hello appel toohello back-end. Remplacez  *\<nom_paramètre\>*  avec nom hello du paramètre hello que vous souhaitez tooset. Si une chaîne vide hello est fournie, le paramètre hello n’est pas inclus à la demande de back-end hello.
* **backend.Request.Headers. \<HeaderName\>**: un en-tête qui peut être défini pour hello appel toohello back-end. Remplacez  *\<HeaderName\>*  avec nom hello d’en-tête hello que vous souhaitez tooset. Si vous fournissez une chaîne vide hello, en-tête de hello n’est pas inclus à la demande de back-end hello.

Valeurs peuvent référencer des paramètres d’application et de paramètres à partir de la demande du client d’origine hello.

Un exemple de configuration peut se présenter comme hello suivantes :

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>",
            "requestOverrides": {
                "backend.request.headers.Accept": "application/xml",
                "backend.request.headers.x-functions-key": "%ANOTHERAPP_API_KEY%"
            }
        }
    }
}
```

### <a name="responseOverrides"></a>Définition d’un objet responseOverrides

objet de requestOverrides Hello définit les modifications apportées à réponse toohello qui a passé arrière toohello client. objet de Hello est défini par hello propriétés suivantes :

* **response.statusCode**: toobe de code d’état HTTP de hello retourné toohello client.
* **response.statusReason**: toobe de phrase de motif hello HTTP retourné toohello client.
* **Response.Body**: représentation sous forme de chaîne hello de hello corps toobe retourné toohello client.
* **Response.Headers. \<HeaderName\>**: un en-tête qui peut être défini pour le client de toohello réponse hello. Remplacez  *\<HeaderName\>*  avec nom hello d’en-tête hello que vous souhaitez tooset. Si vous fournissez une chaîne vide hello, en-tête de hello n’est pas inclus dans la réponse de hello.

Valeurs peuvent référencer des paramètres d’application, les paramètres de demande du client d’origine hello et les paramètres de réponse du serveur principal hello.

Un exemple de configuration peut se présenter comme hello suivantes :

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "responseOverrides": {
                "response.body": "Hello, {test}",
                "response.headers.Content-Type": "text/plain"
            }
        }
    }
}
```
> [!NOTE] 
> Dans cet exemple, corps de hello est définie directement, etc. `backendUri` propriété est nécessaire. Hello montre comment vous pouvez utiliser des proxys de fonctions Azure pour la simulation d’API.

[portail Azure]: https://portal.azure.com
[HTTP déclencheurs]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify hello back-end request]: #modify-backend-request
[Modify hello response]: #modify-response
[définir un objet requestOverrides]: #requestOverrides
[définir un objet responseOverrides]: #responseOverrides
[paramètres de l’application]: #use-appsettings
[Utilisation de variables]: #using-variables
[paramètres à partir de la demande du client d’origine hello]: #request-parameters
[paramètres de réponse du serveur principal hello]: #response-parameters
