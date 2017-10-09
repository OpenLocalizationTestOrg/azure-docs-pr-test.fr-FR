---
title: "authentification et sécurité de grille d’événement aaaAzure"
description: "Détaille Azure Event Grid et ses concepts."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: 74f692c7e3a30856c3a80cbbfe82a26bf4c1c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-security-and-authentication"></a>Sécurité et authentification Azure Event Grid 

Azure Event Grid dispose de trois types d’authentification :

* Abonnements à des événements
* Publication d’événement
* Remise d’événement WebHook

## <a name="webhook-event-delivery"></a>Remise d’événement WebHook

Webhooks sont un des nombreux événements tooreceive de manières en temps réel à partir de la grille d’événement Azure.

Chaque fois qu’il existe un nouveau toobe de prêt événement remis, grille d’événement envoie une requête HTTP avec tooyour WebHook avec les événements hello dans le corps de hello.

Lorsque vous inscrivez votre propre point de terminaison WebHook avec grille d’événement, il vous envoie une requête POST avec un code de validation simple dans la propriété de commande tooprove point de terminaison. Votre application doit toorespond en affichant le code de validation hello précédent. Grille d’événement renverra pas d’événements tooWebHook des points de terminaison qui n’ont pas réussi la validation hello.
 
### <a name="validation-details"></a>Détails de validation :

* Au moment de hello d’événement abonnement création/mise à jour, grille d’événement valide un point de terminaison cible de toohello événements « SubscriptionValidationEvent ».
* événement de Hello contient une valeur d’en-tête « Validation de : Type d’événement ».
* corps de l’événement Hello a hello même schéma que d’autres événements de la grille d’événement.
* données d’événement Hello incluent une propriété « ValidationCode » avec une chaîne générée de façon aléatoire, par exemple « ValidationCode : acb13... ».

Dans la propriété de commande tooprove point de terminaison, par exemple, de code de validation hello arrière d’écho « ValidationResponse : acb13... ».

Enfin, il est important toonote que grille d’événement Azure prend en charge les points de terminaison HTTPS webhook.
## <a name="event-subscription"></a>Abonnement à un événement

événement de tooan toosubscribe, vous devez disposer hello **Microsoft.EventGrid/EventSubscriptions/Write** ressource nécessite une autorisation sur hello. Vous avez besoin de cette autorisation, car l’écriture d’un nouvel abonnement à la portée de hello de ressource de hello. Hello requis ressources différent selon que vous vous abonnez tooa système rubrique ou personnalisé. Les deux types sont décrits dans cette section.

### <a name="system-topics-azure-service-publishers"></a>Rubriques du système (éditeurs du service Azure)

Les rubriques du système, vous avez besoin d’autorisation toowrite un nouvel abonnement des événements au niveau de portée de hello d’événement de hello publication hello ressource. format Hello de ressource de hello est :`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`

Par exemple, les événements tooan toosubscribe sur un compte de stockage nommé **MONCOMPTE**, vous devez avoir l’autorisation de Microsoft.EventGrid/EventSubscriptions/Write de hello sur :`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`

### <a name="custom-topics"></a>Rubriques personnalisées

Les rubriques personnalisés, vous devez autorisation toowrite un nouvel abonnement des événements au niveau de portée de hello de rubrique de grille d’événement hello. format Hello de ressource de hello est :`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`

Par exemple, toosubscribe tooa rubrique personnalisée nommée **mytopic**, vous devez avoir l’autorisation de Microsoft.EventGrid/EventSubscriptions/Write de hello sur :`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`

## <a name="topic-publishing"></a>Publication d’une rubrique

Les rubriques utilisent une Signature d’accès partagé (SAP) ou une authentification par clé. Nous vous recommandons la SAP, mais l’authentification par clé propose une programmation simple et est compatible avec de nombreux éditeurs de webhook existants. 

Vous incluez la valeur d’authentification hello dans l’en-tête HTTP de hello. Pour les associations de sécurité, utilisez **jeton de sas, AEG,** pour la valeur d’en-tête hello. Pour l’authentification par clé, utilisez **clé de sas, AEG,** pour la valeur d’en-tête hello.

### <a name="key-authentication"></a>Authentification par clé

Authentification de la clé est la forme la plus simple de hello d’authentification. Utilisez le format hello :`aeg-sas-key: <your key>`

Par exemple, vous transmettez une clé avec : 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a>Jetons SAS

Jetons SAP pour la grille d’événement incluent hello ressource, un délai d’expiration et une signature. Bonjour format du jeton SAS de hello est : `r={resource}&e={expiration}&s={signature}`.

chemin d’accès hello est Hello ressource pour hello rubrique toowhich vous envoyez des événements. Par exemple, un chemin d’accès de ressource valide est :`https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`

Pour générer des signatures de hello à partir d’une clé.

Par exemple, une valeur **aeg-sas-token** valide est :

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

Hello, l’exemple suivant crée un jeton SAP pour une utilisation avec la grille d’événement :

```cs
static string BuildSharedAccessSignature(string resource, DateTime expirationUtc, string key)
{
    const char Resource = 'r';
    const char Expiration = 'e';
    const char Signature = 's';

    string encodedResource = HttpUtility.UrlEncode(resource);
    string encodedExpirationUtc = HttpUtility.UrlEncode(expirationUtc.ToString());

    string unsignedSas = $"{Resource}={encodedResource}&{Expiration}={encodedExpirationUtc}";
    using (var hmac = new HMACSHA256(Convert.FromBase64String(key)))
    {
        string signature = Convert.ToBase64String(hmac.ComputeHash(Encoding.UTF8.GetBytes(unsignedSas)));
        string encodedSignature = HttpUtility.UrlEncode(signature);
        string signedSas = $"{unsignedSas}&{Signature}={encodedSignature}";

        return signedSas;
    }
}
```

## <a name="management-access-control"></a>Contrôle d’accès à la gestion

Grille d’événement Azure permet de vous toocontrol hello au niveau d’accès donné toodifferent utilisateurs toodo plusieurs opérations de gestion telles que les abonnements d’événement de liste, créer de nouveaux et générer des clés. Pour cela, Event Grid utilise la vérification d’accès par rôle (RBAC).

### <a name="operation-types"></a>Types d’opération

Grille d’événement Azure prend en charge hello suivant des actions :

* Microsoft.EventGrid/*/read 
* Microsoft.EventGrid/*/write 
* Microsoft.EventGrid/*/delete 
* Microsoft.EventGrid/eventSubscriptions/getFullUrl/action 
* Microsoft.EventGrid/topics/listKeys/action 
* Microsoft.EventGrid/topics/regenerateKey/action

Bonjour les trois dernières opérations retournent potentiellement secret des informations qui obtient filtrage dans les opérations de lecture normales. Il est recommandé pour vous, les opérations de toothese toorestrict accès. Des rôles personnalisés peuvent être créés à l’aide de [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure Interface de ligne de commande (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md)et hello [API REST](../active-directory/role-based-access-control-manage-access-rest.md).

### <a name="enforcing-role-based-access-check-rbac"></a>Application de la vérification d’accès par rôle (RBAC)

Hello suivant les étapes tooenforce RBAC pour différents utilisateurs, utilisez :

#### <a name="create-a-custom-role-definition-file-json"></a>Créer un fichier de définition de rôle personnalisé (.json)

Hello Voici des exemples de définitions de rôle grille d’événement qui permettent aux utilisateurs tooperform différents ensembles d’actions.

**EventGridReadOnlyRole.json** : pour autoriser uniquement les opérations en lecture seule.
```json
{ 
  "Name": "Event grid read only role", 
  "Id": "7C0B6B59-A278-4B62-BA19-411B70753856", 
  "IsCustom": true, 
  "Description": "Event grid read only role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/read" 
  ], 
  "NotActions": [ 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription Id>" 
  ] 
}
```

**EventGridNoDeleteListKeysRole.json** : pour autoriser des actions de publication limitées, et interdire les actions de suppression.
```json
{ 
  "Name": "Event grid No Delete Listkeys role", 
  "Id": "B9170838-5F9D-4103-A1DE-60496F7C9174", 
  "IsCustom": true, 
  "Description": "Event grid No Delete Listkeys role", 
  "Actions": [     
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action" 
  ], 
  "NotActions": [ 
    "Microsoft.EventGrid/*/delete" 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription id>" 
  ] 
}
```
 
**EventGridContributorRole.json**: pour autoriser toutes les actions dans Event Grid.  
```json
{ 
  "Name": "Event grid contributor role", 
  "Id": "4BA6FB33-2955-491B-A74F-53C9126C9514", 
  "IsCustom": true, 
  "Description": "Event grid contributor role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/*/delete", 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
  ], 
  "NotActions": [], 
  "AssignableScopes": [ 
    "/subscriptions/d48566a8-2428-4a6c-8347-9675d09fb851" 
  ] 
} 
```

#### <a name="install-and-login-tooazure-cli"></a>Installation et ouverture de session tooAzure CLI

* Azure CLI version 0.8.8 ou ultérieure. version la plus récente tooinstall hello et à associer à votre abonnement Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md).
* Azure Resource Manager dans l’interface de ligne de commande Azure. Accédez trop[Using hello CLI d’Azure avec hello Gestionnaire de ressources](../xplat-cli-azure-resource-manager.md) pour plus d’informations.

#### <a name="create-a-custom-role"></a>Créer un rôle personnalisé

toocreate un rôle personnalisé, utilisez :

    azure role create --inputfile <file path>

#### <a name="assign-hello-role-tooa-user"></a>Affecter hello rôle tooa utilisateur


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a>Étapes suivantes

* Pour une introduction tooEvent grille, consultez [sur la grille d’événement](overview.md)
