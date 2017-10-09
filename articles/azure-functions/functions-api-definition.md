---
title: "métadonnées aaaOpenAPI dans les fonctions de Azure | Documents Microsoft"
description: "Vue d’ensemble de la prise en charge d’OpenAPI dans les fonctions Azure"
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
ms.openlocfilehash: fff8f14110469a002a6c9dca03f641672003a3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="openapi-20-metadata-support-in-azure-functions-preview"></a>Prise en charge des métadonnées OpenAPI 2.0 dans Azure Functions (préversion)
OpenAPI 2.0 (anciennement Swagger) prise en charge des métadonnées dans les fonctions de Azure est une fonctionnalité d’aperçu que vous pouvez utiliser la définition de toowrite un 2.0 OpenAPI à l’intérieur d’une application de la fonction. Vous pouvez ensuite héberger ce fichier à l’aide d’application de fonction hello.

[Les métadonnées OpenAPI](http://swagger.io/) permet à une fonction qui héberge un toobe de l’API REST utilisée par un grand nombre d’autres logiciels. Ce logiciel inclut des offres Microsoft telles que PowerApps et hello [fonctionnalité applications API de Service d’applications Azure](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), comme les outils de développement de tiers [Postman](https://www.getpostman.com/docs/importing_swagger), et [de nombreux packages plus](http://swagger.io/tools/).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

>[!TIP]
>Nous vous recommandons de commencer par hello [didacticiel de mise en route](./functions-api-definition-getting-started.md) , puis de retourner toothis document toolearn plus d’informations sur les fonctionnalités spécifiques.

## <a name="enable"></a>Activer la prise en charge de la définition OpenAPI
Vous pouvez configurer tous les paramètres OpenAPI sur hello **définition d’API** page dans votre application de fonction **fonctionnalités de plateforme**.

génération de hello tooenable d’une définition de OpenAPI hébergée et une définition de démarrage rapide, définissez **source de définition d’API** trop**(fonction) (version préliminaire)**. **URL externe** permet à une définition de OpenAPI qui a hébergé ailleurs toouse de votre fonction.

## <a name="generate-definition"></a>Générer une structure Swagger à partir des métadonnées de votre fonction
Un modèle peut vous aider à commencer à écrire votre première définition OpenAPI. fonctionnalité de définition de modèle Hello crée une définition de OpenAPI partiellement allouée à l’aide de toutes les métadonnées hello dans le fichier de function.json hello pour chacun de vos fonctions de déclencheur HTTP. Vous devez toofill dans plus d’informations sur votre API à partir de hello [OpenAPI spécification](http://swagger.io/specification/), tels que les modèles de demande et de réponse.

Pour obtenir des instructions, consultez hello [didacticiel de mise en route](./functions-api-definition-getting-started.md).

### <a name="templates"></a>Modèles disponibles

|Nom| Description |
|:-----|:-----|
|Définition générée|Une définition d’OpenAPI hello quantité d’informations maximale qui peuvent être déduites à partir des métadonnées existantes de la fonction hello.|

### <a name="quickstart-details"></a>Métadonnées incluses dans la définition de hello généré

Hello suivant représente hello paramètres du portail Azure et les données correspondantes dans function.json car il est mappé toohello généré Swagger squelette.

|Swagger.json|Interface utilisateur du portail|Function.json|
|:----|:-----|:-----|
|[Hôte](http://swagger.io/specification/#fixed-fields-15)|**Paramètres de l’application de fonctions** > **Paramètres App Service** > **Vue d’ensemble** > **URL**|*Non présent*
|[Chemins d’accès](http://swagger.io/specification/#paths-object-29)|**Intégrer** > **Méthodes HTTP sélectionnées**|Liaisons : itinéraire
|[Élément du chemin d’accès](http://swagger.io/specification/#path-item-object-32)|**Intégrer** > **Modèle de routage**|Liaisons : méthodes
|[Sécurité](http://swagger.io/specification/#security-scheme-object-112)|**Clés**|*Non présent*|
|operationID*|**Itinéraire + verbes autorisés**|Itinéraire + verbes autorisés|

\*ID d’opération Hello est requis uniquement pour l’intégration avec PowerApps et le flux.
> [!NOTE]
> extension de x-ms-résumé Hello fournit un nom complet dans le flux Logic Apps et PowerApps.
>
> toolearn, voir [personnaliser votre définition Swagger pour PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/).

## <a name="CICD"></a>Utilisez l’élément de configuration/CD tooset une API définition

 Vous devez activer l’API définition hébergement dans le portail de hello avant d’activer la source contrôle toomodify votre définition de l’API de contrôle de code source. Suivez ces instructions :

1. Parcourir trop**définition d’API (version préliminaire)** dans vos paramètres d’application de fonction.
  1. Définissez **source de définition d’API** trop**fonction**.
  1. Cliquez sur **modèle de définition de générer des API** , puis **enregistrer** toocreate une définition de modèle pour le modifier ultérieurement.
  1. Notez votre URL de définition d’API et votre clé.
1. [Configurez l’intégration continue/le déploiement continu (CI/CD)](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment#continuous-deployment-requirements).
2. Modifiez swagger.json dans le contrôle de code source à l’adresse \site\wwwroot\.azurefunctions\swagger\swagger.json.

Maintenant, les modifications tooswagger.json dans votre espace de stockage sont hébergées par votre application de fonction au niveau de l’URL de la définition hello API et la clé que vous avez noté à l’étape 1.

## <a name="next-steps"></a>Étapes suivantes
* [Didacticiel de prise en main](functions-api-definition-getting-started.md). Essayez notre toosee de procédure pas à pas une définition de OpenAPI en action.
* [Référentiel GitHub Azure Functions](https://github.com/Azure/Azure-Functions/). Consultez hello fonctions référentiel toogive nous des commentaires sur la version préliminaire de hello API définition prise en charge. Créer un problème GitHub pour tout ce que vous voulez toosee mis à jour.
* [Référence du développeur Azure Functions](functions-reference.md). Apprenez-en davantage sur le codage de fonctions et la définition de déclencheurs et de liaisons.
