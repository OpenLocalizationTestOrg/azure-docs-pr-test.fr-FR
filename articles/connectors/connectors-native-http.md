---
title: "aaaCommunicate avec n’importe quel point de terminaison via HTTP - Azure Logic Apps | Documents Microsoft"
description: "Créer des applications logiques qui peuvent communiquer avec n’importe quel point de terminaison via HTTP"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: e11c6b4d-65a5-4d2d-8e13-38150db09c0b
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: 9793601839437a2b880bdb81e15881270cacc963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http-action"></a>Prise en main hello action HTTP

Avec hello action HTTP, vous pouvez étendre le flux de travail pour votre organisation et communiquer un point de terminaison tooany via HTTP.

Vous pouvez :

* Créez des workflows d’application logique qui s’activent (se déclenchent) lors d’une défaillance d’un site Web que vous gérez.
* Communiquent tooany le point de terminaison via HTTP tooextend votre flux de travail à d’autres services.

tooget démarré à l’aide d’action de hello HTTP dans une application logique, consultez [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-http-trigger"></a>Utilisez le déclencheur de hello HTTP
Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail qui est défini dans une application logique. [En savoir plus sur les déclencheurs](connectors-overview.md).

Voici un exemple de séquence de comment déclencher des tooset des hello HTTP Bonjour Concepteur de logique d’application.

1. Ajouter le déclencheur HTTP hello dans votre application logique.
2. Renseignez les paramètres pour le point de terminaison hello HTTP que vous souhaitez toopoll hello.
3. Modifier l’intervalle de périodicité hello sur la fréquence à laquelle il doit interroger.

   application de la logique de Hello déclenche maintenant dont le contenu est renvoyée lors de chaque vérification.

   ![Déclencheur HTTP](./media/connectors-native-http/using-trigger.png)

### <a name="how-hello-http-trigger-works"></a>Fonctionne de déclencheur HTTP hello

déclencheur HTTP Hello envoie un point de terminaison tooHTTP appel sur un intervalle périodique. Par défaut, tout code de réponse HTTP qui est inférieur à 300 entraîne un toorun d’application logique. toospecify si l’application logique de hello doit être activé, vous pouvez modifier l’application de la logique de hello en mode code et ajouter une condition qui prend la valeur hello après l’appel HTTP. Voici un exemple d’un déclencheur HTTP qui se déclenche lorsque hello retourné le code d’état est supérieur ou égal à trop`400`.

```javascript
"Http":
{
    "conditions": [
        {
            "expression": "@greaterOrEquals(triggerOutputs()['statusCode'], 400)"
        }
    ],
    "inputs": {
        "method": "GET",
        "uri": "https://blogs.msdn.microsoft.com/logicapps/",
        "headers": {
            "accept-language": "en"
        }
    },
    "recurrence": {
        "frequency": "Second",
        "interval": 15
    },
    "type": "Http"
}
```

En savoir plus sur les paramètres de déclencheur hello HTTP sont disponibles sur [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).

## <a name="use-hello-http-action"></a>Utilisez l’action de hello HTTP

Une action est une opération est effectuée par le flux de travail hello défini dans une application logique. 
[En savoir plus sur les actions](connectors-overview.md).

1. Choisissez **Nouvelle étape** > **Ajouter une action**.
3. Dans la zone de recherche action hello, tapez **http** actions de hello HTTP toolist.
   
    ![Sélectionnez l’action de hello HTTP](./media/connectors-native-http/using-action-1.png)

4. Ajoutez tous les paramètres requis pour l’appel de hello HTTP.
   
    ![Hello complète action HTTP](./media/connectors-native-http/using-action-2.png)

5. Dans la barre d’outils Concepteur hello, cliquez sur **enregistrer**. Votre application logique est enregistrée et publiée (activée) à hello même temps.

## <a name="http-trigger"></a>Déclencheur HTTP
Voici les détails de hello pour déclencheur hello qui prend en charge par ce connecteur. connecteur HTTP Hello a un déclencheur.

| Déclencheur | Description |
| --- | --- |
| HTTP |Effectue un appel HTTP et retourne le contenu de la réponse hello. |

## <a name="http-action"></a>Action HTTP
Voici les détails de hello pour action hello qui prend en charge par ce connecteur. connecteur de Hello HTTP a une seule action possible.

| Action | Description |
| --- | --- |
| HTTP |Effectue un appel HTTP et retourne le contenu de la réponse hello. |

## <a name="http-details"></a>Détails HTTP
Hello tableaux suivants décrivent hello requis et les champs d’entrée facultatifs pour action de hello et détails sortie correspondants hello qui sont associés à l’aide d’action de hello.

#### <a name="http-request"></a>Demande HTTP
Hello Voici les champs d’entrée pour l’action hello, qui effectue une requête de sortie HTTP.
Le symbole * désigne est un champ obligatoire.

| Nom complet | Nom de la propriété | Description |
| --- | --- | --- |
| Method (Méthode)* |method |Hello HTTP verbe toouse |
| URI* |URI |Hello URI de demande de hello HTTP |
| headers |headers |Un objet JSON de tooinclude des en-têtes HTTP |
| Corps |body |Hello corps de la demande HTTP |
| Authentification |authentication |Détails Bonjour [authentification](#authentication) section |

<br>

#### <a name="output-details"></a>Détails des résultats
Hello Voici les détails de sortie de réponse HTTP de hello.

| Nom de la propriété | Type de données | Description |
| --- | --- | --- |
| headers |objet |En-têtes de réponse |
| Corps |objet |Objet Réponse |
| Code d’état |int |Code d'état HTTP |

## <a name="authentication"></a>Authentification
fonctionnalité de Logic Apps Hello permet toouse différents types d’authentification par rapport aux points de terminaison HTTP. Vous pouvez utiliser cette authentification avec hello **HTTP**,  **[HTTP + Swagger](connectors-native-http-swagger.md)**, et  **[HTTP Webhook](connectors-native-webhook.md)**  connecteurs. Hello, les types d’authentification suivants est configurable :

* [Authentification de base](#basic-authentication)
* [Authentification par certificat client](#client-certificate-authentication)
* [Authentification OAuth Azure Active Directory (Azure AD)](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a>Authentification de base

Hello suivant l’objet d’authentification est nécessaire pour l’authentification de base.
Le symbole * désigne est un champ obligatoire.

| Nom de la propriété | Type de données | Description |
| --- | --- | --- |
| Entrez* |type |Type d’authentification (doit être `Basic` dans le cas d’une authentification de base) |
| Nom d’utilisateur* |username |Tooauthenticate de nom d’utilisateur |
| Mot de passe* |password |Mot de passe tooauthenticate |

> [!TIP]
> Si vous souhaitez toouse un mot de passe ne peut pas être récupérée à partir de la définition de hello, utilisez un `securestring` paramètre et hello `@parameters()`  
>  [fonction de définition de flux de travail](http://aka.ms/logicappdocs).

Par exemple :

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a>Authentification par certificat client

Hello objet suivant de l’authentification est nécessaire pour l’authentification par certificat client. Le symbole * désigne est un champ obligatoire.

| Nom de la propriété | Type de données | Description |
| --- | --- | --- |
| Entrez* |type |type d’authentification de Hello (doit être `ClientCertificate` pour les certificats clients SSL) |
| PFX* |pfx |contenu de codée en Base64 Hello du fichier d’informations Exchange PFX (Personal) hello |
| Mot de passe* |password |tooaccess de mot de passe Hello hello fichier PFX |

> [!TIP]
> toouse un paramètre qui ne sont pas lisible dans la définition de hello après avoir enregistré l’application logique de hello, vous pouvez utiliser un `securestring` paramètre et hello `@parameters()`  
>  [fonction de définition de flux de travail](http://aka.ms/logicappdocs).

Par exemple :

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a>Authentification OAuth Azure AD
Hello suivant l’objet d’authentification est nécessaire pour l’authentification Azure AD OAuth. Le symbole * désigne est un champ obligatoire.

| Nom de la propriété | Type de données | Description |
| --- | --- | --- |
| Entrez* |type |type d’authentification de Hello (doit être `ActiveDirectoryOAuth` pour Azure AD OAuth) |
| Locataire* |locataire |Identificateur du locataire Hello pour le client de hello Azure AD |
| Public ciblé* |audience |ressource Hello vous demande d’autorisation toouse. Par exemple : `https://management.core.windows.net/` |
| ID de client* |clientId |Hello d’identificateur de client pour l’application hello Azure AD |
| Secret* |secret |secret Hello du client hello qui demande hello jeton |

> [!TIP]
> Vous pouvez utiliser un `securestring` paramètre et hello `@parameters()` [fonction de définition de workflow](http://aka.ms/logicappdocs) toouse un paramètre qui ne sont pas lisible dans la définition de hello après l’enregistrement.
> 
> 

Par exemple :

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a>Étapes suivantes
Maintenant, essayez de plate-forme de hello et [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md). Vous pouvez Explorer hello tous les autres connecteurs disponibles dans les applications de la logique en consultant notre [liste des API](apis-list.md).

