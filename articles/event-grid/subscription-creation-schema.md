---
title: "schéma d’abonnement aaaAzure grille d’événement"
description: "Décrit les propriétés de hello d’abonnement de l’événement tooan avec grille d’événement Azure."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/17/2017
ms.author: babanisa
ms.openlocfilehash: 6a96d67975a5a733c5ea3c56ea54501f94ea4cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-subscription-schema"></a>Schéma d’abonnement à Event Grid

toocreate un abonnement de la grille d’événement, vous envoyez une demande de toohello opération d’abonnement Create Event. Utilisez hello suivant le format :

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

Par exemple, toocreate un abonnement aux événements pour un compte de stockage nommé `examplestorage` dans un groupe de ressources nommé `examplegroup`, format utilisez hello suivant :

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

Hello décrit les propriétés hello et schéma de corps hello de demande de hello.
 
## <a name="event-subscription-properties"></a>Propriétés de l’abonnement aux événements

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| destination | objet | objet Hello qui définit le point de terminaison hello. |
| filter | objet | Un champ facultatif pour le filtrage de types hello d’événements. |

### <a name="destination-object"></a>objet de destination

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| endpointType | string | type Hello du point de terminaison pour l’abonnement hello (webhook/HTTP, concentrateur d’événements ou file d’attente). | 
| endpointUrl | string |  | 

### <a name="filter-object"></a>objet de filtre

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| includedEventTypes | array | Mettre en correspondance lorsque le type d’événement hello dans le message d’événement hello est un tooone de correspondance exacte de ces noms de type d’événement. Génère une erreur lorsque le nom de l’événement ne correspond pas à hello inscrit des noms de type d’événements pour la source d’événement hello. Génère une correspondance pour tous les types d’événements. |
| subjectBeginsWith | string | Un préfixe filtre toohello objet champ de correspondance dans le message d’événement hello. valeur par défaut Hello ou chaîne vide correspond à tous. | 
| subjectEndsWith | string | Un suffixe filtre toohello objet champ de correspondance dans le message d’événement hello. valeur par défaut Hello ou chaîne vide correspond à tous. |
| subjectIsCaseSensitive | string | Contrôle la correspondance sensible à la casse pour les filtres. |


## <a name="example-subscription-schema"></a>Exemple de schéma d’abonnement

```json
{
  "properties": {
    "destination": {
      "endpointType": "webhook",
      "properties": {
          "endpointUrl": "https://example.azurewebsites.net/api/HttpTriggerCSharp1?code=VXbGWce53l48Mt8wuotr0GPmyJ/nDT4hgdFj9DpBiRt38qqnnm5OFg=="
      }
    },
    "filter": {
      "includedEventTypes": [ "blobCreated", "blobDeleted" ],
      "subjectBeginsWith": "blobServices/default/containers/mycontainer/log",
      "subjectEndsWith": ".jpg",
      "subjectIsCaseSensitive": "true"
    }
  }
}
```

## <a name="next-steps"></a>Étapes suivantes

* Pour une introduction tooEvent grille, consultez [quelle est la grille d’événement ?](overview.md)
