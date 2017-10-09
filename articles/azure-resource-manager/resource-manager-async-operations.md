---
title: "les opérations asynchrones aaaAzure | Documents Microsoft"
description: "Décrit comment tootrack des opérations asynchrones dans Azure."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: b81254196013adf87998eff11a50993efa52d40d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="track-asynchronous-azure-operations"></a>Suivre les opérations asynchrones Azure
Certaines opérations REST de Azure exécutent de façon asynchrone car hello opération impossible rapidement. Cette rubrique décrit comment état de hello tootrack d’opérations asynchrones via les valeurs retournées dans la réponse de hello.  

## <a name="status-codes-for-asynchronous-operations"></a>Codes d’état pour les opérations asynchrones
Initialement, une opération asynchrone retourne un code d’état HTTP de type :

* 201 (créé)
* 202 (accepté) 

Lors de l’opération de hello terminée avec succès, il renvoie :

* 200 (OK)
* 204 (Pas de contenu) 

Consultez toohello [documentation de l’API REST](/rest/api/) toosee les réponses hello pour l’opération hello vous en cours d’exécution. 

## <a name="monitor-status-of-operation"></a>Surveiller l’état de l'opération
Hello asynchrone reste opérations retour valeurs d’en-tête, que vous pouvez utiliser l’état de hello toodetermine de hello l’opération. Il existe potentiellement en-tête trois valeurs tooexamine :

* `Azure-AsyncOperation`-URL de vérification de l’état en cours de hello d’opération de hello. Si votre opération renvoie cette valeur, utilisez toujours le statut de hello tootrack informatique (au lieu d’emplacement) de l’opération de hello.
* `Location`- URL pour déterminer si une opération est terminée. Utilisez cette valeur uniquement lorsque la valeur Azure-AsyncOperation n’est pas retournée.
* `Retry-After`-hello du nombre de secondes toowait avant de vérifier l’état de hello d’opération asynchrone de hello.

Toutefois, certaines opérations asynchrones ne retournent pas toutes ces valeurs. Par exemple, vous devrez peut-être valeur d’en-tête tooevaluate hello AsyncOperation de Azure pour une opération et la valeur de l’en-tête emplacement hello pour une autre opération. 

Pour récupérer des valeurs d’en-tête hello comme vous permet de récupérer n’importe quel valeur d’en-tête pour une demande. Par exemple, en c#, extraire hello en-tête comprise entre un `HttpWebResponse` objet nommé `response` avec hello suivant de code :

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a>Demande et réponse Azure-AsyncOperation

état de hello tooget d’opération asynchrone de hello, envoyer une URL toohello de demande GET dans la valeur d’en-tête AsyncOperation de Azure.

corps Hello de réponse hello à partir de cette opération contient des informations sur les opération hello. Hello suivant montre les valeurs possibles de hello retournés à partir de l’opération de hello :

```json
{
    "id": "{resource path from GET operation}",
    "name": "{operation-id}", 
    "status" : "Succeeded | Failed | Canceled | {resource provider values}", 
    "startTime": "2017-01-06T20:56:36.002812+00:00",
    "endTime": "2017-01-06T20:56:56.002812+00:00",
    "percentComplete": {double between 0 and 100 },
    "properties": {
        /* Specific resource provider values for successful operations */
    },
    "error" : { 
        "code": "{error code}",  
        "message": "{error description}" 
    }
}
```

Seule la valeur `status` est renvoyée pour toutes les réponses. Hello erreur est retourné lorsque l’état de hello est Échec ou annulé. Toutes les autres valeurs sont facultatives ; Par conséquent, la réponse hello que vous recevez peut ressembler différente de celle hello exemple.

## <a name="provisioningstate-values"></a>Valeurs provisioningState

Les opérations qui créent, mettent à jour ou suppriment (PUT, PATCH, DELETE) une ressource retournent généralement une valeur `provisioningState`. Lorsqu’une opération est terminée, une des trois valeurs suivantes est retournée : 

* Réussi
* Échec
* Canceled

Toutes les autres valeurs indiquent l’opération de hello est en cours d’exécution. fournisseur de ressources Hello peut retourner une valeur personnalisée qui indique son état. Par exemple, vous pouvez recevoir **accepté** lorsque la demande de hello est reçu et en cours d’exécution.

## <a name="example-requests-and-responses"></a>Exemples de demandes et de réponses

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a>Démarrez la machine virtuelle (202 avec Azure-AsyncOperation)
Cet exemple montre comment toodetermine hello état de **Démarrer** opération pour les ordinateurs virtuels. demande initiale de Hello est Bonjour suivant le format :

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

Renvoie le code d’état 202. Parmi les valeurs d’en-tête hello, vous voyez :

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

état de hello toocheck d’opération asynchrone hello, envoyer une autre demande toothat URL.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

corps de réponse Hello contient l’état hello d’opération de hello :

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a>Déployer des ressources (201 avec Azure-AsyncOperation)

Cet exemple montre comment toodetermine hello état de **déploiements** opération pour le déploiement de ressources tooAzure. demande initiale de Hello est Bonjour suivant le format :

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

Il renvoie le code d’état 201. Hello de corps de réponse de hello inclut :

```json
"provisioningState":"Accepted",
```

Parmi les valeurs d’en-tête hello, vous voyez :

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

état de hello toocheck d’opération asynchrone hello, envoyer une autre demande toothat URL.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

corps de réponse Hello contient l’état hello d’opération de hello :

```json
{"status":"Running"}
```

Lorsque le déploiement de hello est terminé, la réponse de hello contient :

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a>Créer le compte de stockage (202 avec Location et Retry-After)

Cet exemple montre comment toodetermine hello état Hello **créer** opération pour les comptes de stockage. demande initiale de Hello est Bonjour suivant le format :

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

Et le corps de la demande hello contient les propriétés de compte de stockage hello :

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

Renvoie le code d’état 202. Parmi les valeurs d’en-tête hello, vous voyez hello deux valeurs suivantes :

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

Après avoir attendu pour le nombre de secondes spécifié dans Retry-After, vérifiez l’état hello d’opération asynchrone de hello en envoyant une autre demande toothat URL.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

Si la demande de hello est en cours d’exécution, vous recevez un code d’état 202. Si la demande de hello est terminée, votre recevoir un code d’état 200 et corps hello de réponse de hello contient des propriétés de hello hello du compte de stockage qui a été créé.

## <a name="next-steps"></a>Étapes suivantes

* Pour plus d'informations sur chaque opération REST, consultez la [documentation de l'API REST](/rest/api/).
* Pour plus d’informations sur la gestion des ressources via hello REST API du Gestionnaire de ressources, consultez [Using hello REST API du Gestionnaire de ressources](resource-manager-rest-api.md).
* Pour plus d’informations sur le déploiement de modèles via hello REST API du Gestionnaire de ressources, consultez [déployer des ressources avec des modèles de gestionnaire de ressources et les REST API du Gestionnaire de ressources](resource-group-template-deploy-rest.md).
