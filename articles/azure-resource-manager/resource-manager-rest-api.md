---
title: "API REST du Gestionnaire d’aaaResource | Documents Microsoft"
description: "Une vue d’ensemble de hello authentification de l’API REST du Gestionnaire de ressources et des exemples d’utilisation"
services: azure-resource-manager
documentationcenter: na
author: navalev
manager: timlt
editor: 
ms.assetid: e8d7a1d2-1e82-4212-8288-8697341408c5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/13/2017
ms.author: navale;tomfitz;
ms.openlocfilehash: 3ccc3575c5e06c41f2fdc5317711980fc6a2f649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-manager-rest-apis"></a>API REST Resource Manager
> [!div class="op_single_selector"]
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [Interface de ligne de commande Azure](xplat-cli-azure-resource-manager.md)
> * [Portail](resource-group-portal.md) 
> * [API REST](resource-manager-rest-api.md)
> 
> 

Derrière chaque tooAzure d’appel de gestionnaire de ressources derrière chaque modèle déployé, derrière chaque compte de stockage configurés sont les API RESTful un ou plusieurs appels toohello Azure du Gestionnaire de ressources. Cette rubrique est consacrée toothose API et comment vous pouvez les appeler sans utiliser un kit de développement logiciel du tout. Cette approche est utile si vous souhaitez que le contrôle total de demandes tooAzure ou si hello Kit de développement logiciel pour votre langue par défaut n’est pas disponible ou ne prend pas en charge les opérations que vous devez hello.

Cet article ne passe pas par le biais des API qui sont exposée dans Azure, mais qu’il utilise certaines opérations sont des exemples de la façon dont vous vous connectez toothem. Une fois que vous comprenez les notions de base hello, vous pouvez lire hello [référence d’API REST Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) toofind des informations détaillées sur comment reste hello toouse hello API.

## <a name="authentication"></a>Authentification
L’authentification pour Resource Manager est gérée par Azure Active Directory (AD). tooconnect tooany API, vous devez tout d’abord tooauthenticate avec Azure AD tooreceive un jeton d’authentification que vous pouvez passer à la demande de tooevery. Comme nous décrivons un appel pur directement toohello API REST, nous partons du principe que vous ne souhaitez pas tooauthenticate à être invité à entrer un nom d’utilisateur et un mot de passe. Nous supposons également que vous n’utilisez pas les mécanismes d’authentification à deux facteurs. Par conséquent, nous créons ce que l'on appelle une Application Azure AD et un principal de service qui sont utilisé toolog dans. Mais rappelez-vous que Azure AD prend en charge plusieurs procédures d’authentification et tous les peut être utilisé tooretrieve ce jeton d’authentification nécessaire pour les demandes API suivantes.
Pour connaître la procédure détaillée, suivez les instructions figurant dans [Créer une application Azure AD et un principal du service](resource-group-create-service-principal-portal.md).

### <a name="generating-an-access-token"></a>Génération d’un jeton d’accès
L’authentification auprès d’Azure AD est effectuée en appelant tooAzure AD, situé à login.microsoftonline.com. tooauthenticate, vous devez hello toohave informations suivantes :

* ID de locataire Azure AD (hello nom de qu’Azure AD à l’aide de toolog dans, souvent hello identique à votre entreprise mais n’est pas nécessaire)
* ID d’application (effectuée au cours de l’étape de la création de l’application hello Azure AD)
* Mot de passe (que vous avez sélectionné lors de la création de hello Application Azure AD)

Bonjour suivant la requête HTTP, assurez-vous que tooreplace « ID de locataire Azure AD, » « ID d’Application » et « Password » avec les valeurs correctes hello.

**Requête HTTP générique :**

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

... va (si l’authentification réussit) entraîne un toohello similaire de réponse suivant la réponse :

```json
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1448199959",
  "not_before": "1448196059",
  "resource": "https://management.core.windows.net/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhb...86U3JI_0InPUk_lZqWvKiEWsayA"
}
```
(access_token hello Bonjour précédant la réponse ont été raccourcie tooincrease lisibilité)

**Génération du jeton d’accès à l’aide d’un interpréteur de commandes (Bash) :**

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

**Génération du jeton d’accès à l’aide de PowerShell :**

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

Hello réponse contient un jeton d’accès, d’informations sur la durée pendant laquelle ce jeton est valide et plus d’informations sur la ressource que vous pouvez utiliser ce jeton pour.
jeton d’accès Hello que vous avez reçu dans l’appel HTTP de la précédente hello doit être transmise pour toohello demande toutes les API du Gestionnaire de ressources. Passez-le en tant qu’une valeur d’en-tête nommée « Authorization » avec la valeur de hello « Support YOUR_ACCESS_TOKEN ». Notez l’espace hello entre « Support » et votre jeton d’accès.

Comme vous pouvez voir à partir de hello ci-dessus HTTP, jeton de hello est valide pour une période spécifique au cours de laquelle vous devez mettre en cache et réutiliser ce même jeton. Même s’il est possible tooauthenticate auprès d’Azure AD pour chaque appel d’API, il est peu efficace.

## <a name="calling-resource-manager-rest-apis"></a>Appel d'API REST Resource Manager
Cette rubrique utilise uniquement quelques API tooexplain hello l’utilisation de base des opérations REST de hello. Pour plus d’informations sur toutes les opérations de hello, consultez [API REST de Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).

### <a name="list-all-subscriptions"></a>Répertorier tous les abonnements
Une des opérations de la plus simple de hello que faire est toolist hello disponibles les abonnements auxquels vous pouvez accéder. Bonjour demande, vous consultez Comment jeton d’accès hello est passée comme un en-tête de :

(Remplacez YOUR_ACCESS_TOKEN par votre véritable jeton d’accès.)

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

... et par conséquent, vous obtenez une liste des abonnements que ce principal du service est autorisé tooaccess

(Les ID d’abonnement ont été raccourcis pour une meilleure lisibilité)

```json
{
  "value": [
    {
      "id": "/subscriptions/3a8555...555995",
      "subscriptionId": "3a8555...555995",
      "displayName": "Azure Subscription",
      "state": "Enabled",
      "subscriptionPolicies": {
        "locationPlacementId": "Internal_2014-09-01",
        "quotaId": "Internal_2014-09-01"
      }
    }
  ]
}
```

### <a name="list-all-resource-groups-in-a-specific-subscription"></a>Répertorier tous les groupes de ressources dans un abonnement spécifique
Toutes les ressources disponibles avec les API du Gestionnaire de ressources de hello sont imbriqués à l’intérieur d’un groupe de ressources. Vous pouvez interroger le Gestionnaire de ressources pour les groupes de ressources existants dans votre abonnement à l’aide de hello suivant demande HTTP GET. Notez comment hello ID d’abonnement est passé en tant que partie de l’URL de hello instant.

(Remplacez YOUR_ACCESS_TOKEN et SUBSCRIPTION_ID par vos véritables jetons d’accès et ID d’abonnement)

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

Hello réponse varie selon que vous disposez d’aucun groupe de ressources défini et si tel est le cas, combien.

(Les ID d’abonnement ont été raccourcis pour une meilleure lisibilité)

```json
{
    "value": [
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/myfirstresourcegroup",
            "name": "myfirstresourcegroup",
            "location": "eastus",
            "properties": {
                "provisioningState": "Succeeded"
            }
        },
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/mysecondresourcegroup",
            "name": "mysecondresourcegroup",
            "location": "northeurope",
            "tags": {
                "tagname1": "My first tag"
            },
            "properties": {
                "provisioningState": "Succeeded"
            }
        }
    ]
}
```

### <a name="create-a-resource-group"></a>Créer un groupe de ressources
Jusqu'à présent, nous avons été interrogeant uniquement hello API du Gestionnaire de ressources pour plus d’informations. Il est temps de créer des ressources et nous commençons par hello plus simple d'entre eux tous, un groupe de ressources. Hello requête HTTP suivante crée un groupe de ressources dans une région de votre choix et ajoute un tooit de balise.

(Remplacez YOUR_ACCESS_TOKEN, ID_ABONNEMENT, nom_groupe_ressource avec votre réel jeton d’accès, ID d’abonnement et le nom de groupe de ressources que vous voulez toocreate de hello)

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  }
}
```

En cas de réussite, vous obtenez une réponse similaire toohello suivant la réponse :

```json
{
  "id": "/subscriptions/3a8555...555995/resourceGroups/RESOURCE_GROUP_NAME",
  "name": "RESOURCE_GROUP_NAME",
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  },
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

Vous avez créé un groupe de ressources dans Azure ! Félicitations !

### <a name="deploy-resources-tooa-resource-group-using-a-resource-manager-template"></a>Déployer le groupe de ressources tooa de ressources à l’aide d’un modèle de gestionnaire de ressources
Avec Resource Manager, vous pouvez déployer vos ressources à l’aide de modèles. Un modèle définit plusieurs ressources et leurs dépendances. Dans cette section, nous supposons que vous êtes familiarisé avec les modèles de gestionnaire de ressources, et nous vous montrer comment toomake hello API appeler toostart déploiement. Pour en savoir plus sur la création de modèles, voir [Création de modèles Azure Resource Manager](resource-group-authoring-templates.md).

Déploiement d’un modèle ne diffère beaucoup toohow vous appelez d’autres API. Un aspect important est le fait que le déploiement d’un modèle peut prendre beaucoup de temps. appel d’API de Hello retourne simplement et c’est tooyou comme tooquery de développeur pour l’état de toofind de déploiement hello out fois hello déploiement terminé. Pour plus d’informations, consultez la rubrique [Suivre les opérations asynchrones Azure](resource-manager-async-operations.md).

Pour cet exemple, nous utilisons un modèle exposé publiquement disponible sur [GitHub](https://github.com/Azure/azure-quickstart-templates). modèle Hello que nous utilisons déploie une région ouest des États-Unis de toohello Linux VM. Bien que cet exemple utilise un modèle disponible dans un référentiel public comme GitHub, vous pouvez passer à la place les modèle complet de hello dans le cadre de la demande de hello. Notez que nous fournissons des valeurs de paramètre dans la demande de hello qui servent à l’intérieur de hello déployé le modèle.

(Remplacez toovalues ID_ABONNEMENT, nom_groupe_ressource, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD et DNS_NAME_FOR_PUBLIC_IP appropriés pour votre demande)

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME/providers/microsoft.resources/deployments/DEPLOYMENT_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "properties": {
    "templateLink": {
      "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json",
      "contentVersion": "1.0.0.0",
    },
    "mode": "Incremental",
    "parameters": {
        "newStorageAccountName": {
          "value": "GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME"
        },
        "adminUsername": {
          "value": "ADMIN_USER_NAME"
        },
        "adminPassword": {
          "value": "ADMIN_PASSWORD"
        },
        "dnsNameForPublicIP": {
          "value": "DNS_NAME_FOR_PUBLIC_IP"
        },
        "ubuntuOSVersion": {
          "value": "15.04"
        }
    }
  }
}
```

Hello temps de réponse JSON pour cette demande a été lisibilité tooimprove omis de cette documentation. réponse de Hello contient des informations sur le déploiement basé sur un modèle hello que vous avez créé.

## <a name="next-steps"></a>Étapes suivantes

- toolearn sur la gestion des opérations asynchrones de REST, consultez [le suivi des opérations asynchrones Azure](resource-manager-async-operations.md).
