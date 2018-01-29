---
title: Utilisation des proxys dans Azure Functions | Microsoft Docs
description: "Présentation de l’utilisation de Azure Functions Proxies"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: cfowler
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/11/2017
ms.author: alkarche
ms.openlocfilehash: dd022b189783f2d8c6209a6cd656704ff144bfd6
ms.sourcegitcommit: 4256ebfe683b08fedd1a63937328931a5d35b157
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/23/2017
---
# <a name="work-with-azure-functions-proxies"></a>Utilisation d’Azure Functions Proxies

Cet article vous explique comment configurer et utiliser Azure Functions Proxies. Cette fonctionnalité vous permet de spécifier des points de terminaison sur votre Function App implémentés par une autre ressource. Vous pouvez utiliser ces proxys pour diviser une API de grande taille en plusieurs applications Function (comme dans une architecture microservice), tout en continuant à présenter une surface API unique aux clients.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE] 
> Une facturation standard s’applique à l’exécution des proxys. Pour plus d’informations, consultez [Tarification d’Azure Functions](https://azure.microsoft.com/pricing/details/functions/).

## <a name="create"></a>Création d’un proxy

Cette section vous explique comment créer un proxy dans le portail Functions.

1. Ouvrez le [portail Azure] et accédez à votre Function App.
2. Dans le volet gauche, sélectionnez **Nouveau proxy**.
3. Entrez un nom pour votre proxy.
4. Configurez le point de terminaison exposé sur cette Function App en spécifiant le **modèle de routage** et les **méthodes HTTP**. Ces paramètres se comportent selon les règles des [déclencheurs HTTP].
5. Définissez l’**URL principale** sur un autre point de terminaison. Il peut s’agir d’une fonction dans une autre Function App ou bien de n’importe quelle autre API. La valeur ne doit pas nécessairement être statique et peut faire référence aux [paramètres de l’application] et aux [paramètres de la demande client d’origine].
6. Cliquez sur **Créer**.

Votre proxy existe désormais sous la forme d’un nouveau point de terminaison de votre application de fonction. Du point de vue du client, cela équivaut à un HttpTrigger dans Azure Functions. Vous pouvez essayer votre nouveau proxy en copiant l’URL de proxy et en le testant avec le client HTTP de votre choix.

## <a name="modify-requests-responses"></a>Modification de demandes et de réponses

La fonctionnalité Azure Functions Proxies vous permet de modifier les demandes envoyées au backend et les réponses reçues de ce dernier. Ces transformations peuvent impliquer l’utilisation de variables, comme décrit dans la section [Utilisation de variables].

### <a name="modify-backend-request"></a>Modification de la demande du serveur principal

Par défaut, la demande du serveur principal est initialisée comme une copie de la demande d’origine. Outre la définition de l’URL du serveur principal, vous pouvez apporter des modifications à la méthode HTTP, aux en-têtes et aux paramètres de chaîne de requête. Les valeurs modifiées peuvent faire référence aux [paramètres de l’application] et aux [paramètres de la demande client d’origine].

Il n’est actuellement pas possible de modifier les demandes du serveur principal via un portail. Pour savoir comment appliquer cette fonctionnalité avec un fichier *proxies.json*, consultez la section [Définition d’un objet requestOverrides].

### <a name="modify-response"></a>Modification de la réponse

Par défaut, la réponse client est initialisée comme une copie de la réponse du serveur principal. Vous pouvez apporter des modifications au code d’état, au motif, aux en-têtes et au corps. Les valeurs modifiées peuvent faire référence aux [paramètres de l’application], aux [paramètres de la demande client d’origine] et aux [paramètres de la réponse du serveur principal].

Il n’est actuellement pas possible de modifier les réponses. Pour savoir comment appliquer cette fonctionnalité avec un fichier *proxies.json*, consultez la section [Définition d’un objet responseOverrides].

## <a name="using-variables"></a>Utilisation de variables

La configuration d’un proxy ne doit pas nécessairement être statique. Vous pouvez définir comme condition l’utilisation des variables de la demande client d’origine, de la réponse du backend ou des paramètres de l’application.

### <a name="request-parameters"></a>Référencement des paramètres de la demande

Les paramètres de la demande peuvent être entrés au niveau de la propriété d’URL du serveur principal ou peuvent être utilisés lors de la modification des demandes et des réponses. Certains paramètres peuvent être liés à partir du modèle de routage spécifié dans la configuration du proxy de base, alors que d’autres proviennent des propriétés de la demande entrante.

#### <a name="route-template-parameters"></a>Paramètres de modèle de routage
Les paramètres utilisés dans le modèle de routage peuvent être référencés par nom. Les noms des paramètres sont placés entre accolades ({}).

Par exemple, si un proxy dispose d’un modèle de routage du type `/pets/{petId}`, l’URL du serveur principal peut inclure la valeur de `{petId}`, comme dans `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`. Si le modèle de routage prend fin dans un caractère générique, tel que `/api/{*restOfPath}`, la valeur `{restOfPath}` est une chaîne représentant les autres segments de chemin d’accès de la demande entrante.

#### <a name="additional-request-parameters"></a>Paramètres de demande supplémentaires
Outre les paramètres de modèle de routage, les valeurs suivantes peuvent être utilisées dans les valeurs de configuration :

* **{request.method}** : méthode HTTP utilisée lors de la demande d’origine.
* **{request.headers.\<HeaderName\>}** : un en-tête qui peut être lu à partir de la demande d’origine. Remplacez *\<HeaderName\>* par le nom de l’en-tête que vous souhaitez lire. Si l’en-tête n’est pas inclus dans la demande, la valeur sera une chaîne vide.
* **{request.querystring.\<ParameterName\>}** : un paramètre de chaîne de requête qui peut être lu à partir de la demande d’origine. Remplacez *\<ParameterName\>* par le nom de l’en-tête que vous souhaitez lire. Si le paramètre n’est pas inclus dans la demande, la valeur sera une chaîne vide.

### <a name="response-parameters"></a>Référencement des paramètres de réponse du serveur principal

Les paramètres de réponse peuvent être utilisés lors de la modification de la réponse au client. Les valeurs suivantes peuvent être utilisées dans la configuration :

* **{backend.response.statusCode}** : code d’état HTTP renvoyé dans la réponse du serveur principal.
* **{backend.response.statusReason}** : motif HTTP renvoyé dans la réponse du serveur principal.
* **{backend.response.headers.\<HeaderName\>}** : en-tête pouvant être lu à partir de la réponse du serveur principal. Remplacez *\<HeaderName\>* par le nom de l’en-tête que vous souhaitez lire. Si l’en-tête n’est pas inclus dans la réponse, la valeur sera une chaîne vide.

### <a name="use-appsettings"></a>Référencement des paramètres de l’application

Vous pouvez également référencer les [paramètres de l’application définis pour la Function App](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) en mettant le nom du paramètre entre signes de pourcentage (%).

Par exemple, dans une URL de serveur principal de *https://%ORDER_PROCESSING_HOST%/api/orders*, %ORDER_PROCESSING_HOST% sera remplacé par la valeur du paramètre ORDER_PROCESSING_HOST.

> [!TIP] 
> Utilisez des paramètres d’application pour les hôtes de serveur principal lorsque vous avez plusieurs déploiements ou environnements de test. De cette façon, vous avez l’assurance de toujours parler au backend adapté à cet environnement.

## <a name="advanced-configuration"></a>Configuration avancée

Les serveurs proxy que vous configurez sont stockés dans un fichier *proxies.json* situé à la racine d’un répertoire de Function App. Vous pouvez modifier manuellement ce fichier et le déployer dans le cadre de votre application lors de l’utilisation de l’une des [méthodes de déploiement](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) prises en charge par Functions. La fonctionnalité Azure Functions Proxies doit être [activée](#enable) pour permettre le traitement du fichier. 

> [!TIP] 
> Si vous n’avez pas configuré l’une des méthodes de déploiement, vous pouvez également utiliser le fichier *proxies.json* dans le portail. Accédez à votre Function App et sélectionnez **Fonctionnalités de la plateforme**, puis **Éditeur App Service**. Cela vous permettra d’afficher l’ensemble de la structure de fichiers de votre Function App et d’y apporter des modifications.

*Proxies.json* est défini par un objet proxy, composé de proxys nommés et de leurs définitions. Vous pouvez éventuellement référencer un [schéma JSON](http://json.schemastore.org/proxies) de complétion de code si votre éditeur est compatible. Voici un exemple de fichier :

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

Chaque proxy a un nom convivial, tel que *proxy1* dans l’exemple ci-dessus. L’objet de définition de proxy correspondant est défini par les propriétés suivantes :

* **matchCondition** : Obligatoire - un objet définissant les demandes qui déclenchent l’exécution de ce proxy. Il contient deux propriétés partagées avec les [déclencheurs HTTP] :
    * _méthodes_ : un tableau des méthodes HTTP auxquelles le proxy répond. À défaut de spécification, le proxy répond à toutes les méthodes HTTP sur le routage.
    * _route_ : Obligatoire - définit le modèle de routage, en contrôlant les URL de demande auxquelles votre proxy répond. Contrairement aux déclencheurs HTTP, il n’y a pas de valeur par défaut.
* **backendUri** : l’URL de la ressource principale à laquelle la demande doit être transmise par proxy. Cette valeur peut faire référence aux paramètres de l’application et à ceux de la demande client d’origine. Si cette propriété n’est pas incluse, Azure Functions répond avec un message HTTP 200 OK.
* **requestOverrides** : un objet définissant les transformations apportées à la demande du serveur principal. Consultez la section [Définition d’un objet requestOverrides].
* **responseOverrides** : un objet définissant les transformations apportées à la réponse client. Consultez la section [Définition d’un objet responseOverrides].

> [!NOTE] 
> La propriété *route* dans Azure Functions Proxies n’honore pas la propriété *routePrefix* de la configuration d’hôte Function App. Si vous souhaitez inclure un préfixe tel que `/api`, il doit être inclus dans la propriété *route*.

### <a name="requestOverrides"></a>Définition d’un objet requestOverrides

L’objet requestOverrides définit les modifications apportées à la demande lors de l’appel de la ressource du serveur principal. L’objet est défini par les propriétés suivantes :

* **backend.request.method** : méthode HTTP utilisée pour appeler le backend.
* **backend.request.querystring.\<ParameterName\>** : paramètre de chaîne de requête pouvant être défini pour l’appel au backend. Remplacez *\<ParameterName\>* par le nom de l’en-tête que vous souhaitez définir. Si une chaîne vide est fournie, le paramètre n’est pas inclus dans la demande du serveur principal.
* **backend.request.headers.\<HeaderName\>** : en-tête qui peut être défini pour l’appel au backend. Remplacez *\<HeaderName\>* par le nom de l’en-tête que vous souhaitez définir. Si vous fournissez une chaîne vide, l’en-tête n’est pas inclus dans la demande du serveur principal.

Les valeurs peuvent faire référence aux paramètres de l’application et aux paramètres de la demande client d’origine.

Voici un exemple de configuration :

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

L’objet requestOverrides définit les modifications apportées à la réponse retransmise au client. L’objet est défini par les propriétés suivantes :

* **response.statusCode** : code d’état HTTP à renvoyer au client.
* **response.statusReason** : motif HTTP à renvoyer au client.
* **response.body** : la représentation sous forme de chaîne du corps à renvoyer au client.
* **response.headers.\<HeaderName\>** : un en-tête pouvant être défini pour la réponse au client. Remplacez *\<HeaderName\>* par le nom de l’en-tête que vous souhaitez définir. Si vous fournissez une chaîne vide, l’en-tête n’est pas inclus dans la réponse.

Les valeurs peuvent faire référence aux paramètres de l’application, aux paramètres de la demande client d’origine et aux paramètres de la réponse du serveur principal.

Voici un exemple de configuration :

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
> Dans cet exemple, le corps de la réponse est défini directement. Aucune propriété `backendUri` n’est nécessaire. Cet exemple illustre comment utiliser les Proxys Azure Functions pour simuler des API.

## <a name="enable"></a>Activation d’Azure Functions Proxies

Les proxys sont désormais activés par défaut ! Si vous utilisiez une ancienne version de la préversion des proxys, et des proxys désactivés, vous devez activer manuellement les proxys une fois dans l’ordre, pour qu’ils s’exécutent.

1. Ouvrez le [portail Azure] et accédez à votre Function App.
2. Sélectionnez **Paramètres Function App**.
3. Réglez **Activer les proxys Azure Functions (préversion)** sur **Activé**.

Vous pouvez également revenir ici pour mettre à jour le runtime proxy lorsque de nouvelles fonctionnalités sont disponibles.

[portail Azure]: https://portal.azure.com
[déclencheurs HTTP]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify the back-end request]: #modify-backend-request
[Modify the response]: #modify-response
[Définition d’un objet requestOverrides]: #requestOverrides
[Définition d’un objet responseOverrides]: #responseOverrides
[paramètres de l’application]: #use-appsettings
[Utilisation de variables]: #using-variables
[paramètres de la demande client d’origine]: #request-parameters
[paramètres de la réponse du serveur principal]: #response-parameters
