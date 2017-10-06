---
title: points de terminaison REST aaaCall avec HTTP + Swagger connecteur pour Azure Logic Apps | Documents Microsoft
description: "Connecter les points de terminaison tooREST à partir d’applications logique via Swagger hello HTTP + Swagger connecteur"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: eccfd87c-c5fe-4cf7-b564-9752775fd667
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: baaa57689ff41fcd052f9d86086e36619ddec46e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http--swagger-action"></a>Prise en main Bonjour HTTP + Swagger action

Vous pouvez créer un point de terminaison REST de tooany connecteur de première classe via un [Swagger document](https://swagger.io) lorsque vous utilisez Bonjour HTTP + Swagger action dans votre workflow d’application logique. Vous pouvez également étendre logique applications toocall n’importe quel point de terminaison REST avec une expérience de concepteur d’application logique de première classe.

toolearn toocreate des applications de logique avec les connecteurs, voir [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a>Utiliser HTTP + Swagger comme un déclencheur ou d’une action

Bonjour HTTP + travail trigger et action de Swagger hello même hello [action HTTP](connectors-native-http.md) mais aussi fournir une meilleure expérience dans le Concepteur d’application logique en exposant la structure de hello API et les sorties de hello [Swagger métadonnées](https://swagger.io) . Vous pouvez également utiliser Bonjour HTTP + Swagger connecteur comme un déclencheur. Si vous voulez tooimplement un déclencheur d’interrogation, procèdent d’interrogation de hello qui est décrit dans [créer personnalisé API toocall autres API, les services et les systèmes à partir d’applications de logique](../logic-apps/logic-apps-create-api-app.md#polling-triggers).

En savoir plus sur les [déclencheurs et actions de l’application logique](connectors-overview.md).

Voici un exemple de comment toouse hello HTTP + Swagger opération en tant qu’action dans un flux de travail dans une application logique.

1. Sélectionnez hello **nouvelle étape** bouton.
2. Sélectionnez **Ajouter une action**.
3. Dans la zone de recherche action hello, tapez **swagger** hello de toolist HTTP + Swagger action.
   
    ![Sélectionnez une action HTTP + Swagger](./media/connectors-native-http-swagger/using-action-1.png)
4. Tapez l’URL hello pour un document de Swagger :
   
   * toowork de hello Concepteur d’application logique, hello URL doit être un point de terminaison HTTPS et disposer CORS.
   * Si le document de Swagger hello ne répond pas à cette exigence, vous pouvez utiliser [le stockage Azure avec CORS activé](#hosting-swagger-from-storage) document de hello toostore.
5. Cliquez sur **suivant** tooread et rendu à partir de Swagger document hello.
6. Ajoutez tous les paramètres qui sont requis pour l’appel de hello HTTP.
   
    ![Exécuter l’action HTTP](./media/connectors-native-http-swagger/using-action-2.png)
7. toosave et publier votre application logique, cliquez sur **enregistrer** sur la barre d’outils.

### <a name="host-swagger-from-azure-storage"></a>Héberger un document Swagger à partir d'Azure Storage
Vous souhaiterez peut-être tooreference un document de Swagger qui n’est pas hébergé, ou qui ne répond pas aux exigences de sécurité et de cross-origin de hello pour le concepteur hello. tooresolve ce problème, vous pouvez stocker des documents de Swagger hello dans le stockage Azure et activer CORS tooreference hello document.  

Voici hello étapes toocreate, configurer et stocker les documents de Swagger dans le stockage Azure :

1. [Créez un compte de stockage Azure avec un stockage d'objets blob Azure](../storage/common/storage-create-storage-account.md). tooperform cette étape, définir des autorisations trop**accès Public**.

2. Activer l’objet blob de hello CORS. 

   tooautomatically configurer ce paramètre, vous pouvez utiliser [ce script PowerShell](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).

3. Télécharger l’objet blob de hello Swagger fichier toohello. 

   Vous pouvez effectuer cette étape à partir de hello [portail Azure](https://portal.azure.com) ou à partir d’un outil tel que [Azure Storage Explorer](http://storageexplorer.com/).

4. Faire référence à un document de toohello lien HTTPS dans le stockage d’objets Blob Azure. 

   lien de Hello utilise ce format :

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a>Détails techniques
Voici les détails de hello pour hello déclencheurs et les actions que cette HTTP + Swagger connecteur prend en charge.

## <a name="http--swagger-triggers"></a>Déclencheurs HTTP + Swagger
Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail qui est défini dans une application logique. [En savoir plus sur les déclencheurs.](connectors-overview.md) Hello HTTP + Swagger connecteur a un déclencheur.

| Déclencheur | Description |
| --- | --- |
| HTTP + Swagger |Effectuer un appel HTTP et retournent le contenu de la réponse hello |

## <a name="http--swagger-actions"></a>Actions HTTP + Swagger
Une action est une opération est effectuée par le flux de travail hello défini dans une application logique. [En savoir plus sur les actions.](connectors-overview.md) Hello HTTP + Swagger connecteur a une seule action possible.

| Action | Description |
| --- | --- |
| HTTP + Swagger |Effectuer un appel HTTP et retournent le contenu de la réponse hello |

### <a name="action-details"></a>Détails de l’action
Hello HTTP + Swagger connecteur est fourni avec une seule action possible. Voici quelques informations sur chacune des actions de hello, des champs d’entrée obligatoires et facultatifs et hello correspondant détails de sortie qui sont associés à leur utilisation.

#### <a name="http--swagger"></a>HTTP + Swagger
Faites une demande HTTP sortante avec assistance des métadonnées Swagger.
Un astérisque (*) signifie un champ obligatoire.

| Nom complet | Nom de la propriété | Description |
| --- | --- | --- |
| Method (Méthode)* |method |Toouse du verbe HTTP. |
| URI* |URI |URI de demande de hello HTTP. |
| headers |headers |Un objet JSON de tooinclude des en-têtes HTTP. |
| Corps |body |Hello corps de la demande HTTP. |
| Authentification |authentication |Toouse d’authentification pour la demande. Pour plus d’informations, consultez hello [connecteur HTTP](connectors-native-http.md#authentication). |

**Détails des résultats**

Réponse HTTP

| Nom de la propriété | Type de données | Description |
| --- | --- | --- |
| headers |objet |En-têtes de réponse |
| Corps |objet |Objet Réponse |
| Code d’état |int |Code d'état HTTP |

### <a name="http-responses"></a>Réponses HTTP
Lorsque vous élaborez des appels toovarious actions, vous pouvez obtenir certaines réponses. La table ci-dessous indique les réponses correspondantes et leurs descriptions.

| Name | Description |
| --- | --- |
| 200 |OK |
| 202 |Acceptée |
| 400 |Demande incorrecte |
| 401 |Non autorisé |
| 403 |Interdit |
| 404 |Introuvable |
| 500 |Erreur interne du serveur. Une erreur inconnue s’est produite. |

- - -
## <a name="next-steps"></a>Étapes suivantes

* [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md)
* [Rechercher d’autres connecteurs](apis-list.md)