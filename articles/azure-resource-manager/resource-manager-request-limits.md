---
title: les limites des demandes Gestionnaire de ressources aaaAzure | Documents Microsoft
description: "Décrit comment les demandes toouse limitation avec Azure Resource Manager lorsque les limites de l’abonnement ont été atteintes."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: e1047233-b8e4-4232-8919-3268d93a3824
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: ea274f3145af36aac753730e1f280d8a8b59c3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-resource-manager-requests"></a>Limitation des requêtes de Resource Manager
Pour chaque abonnement et le client, les limites de gestionnaire de ressources too15 de demandes, 000 par heure et écrira les demandes too1, 200 par heure. Ces limites s’appliquent d’instance d’Azure Resource Manager tooeach ; Il existe plusieurs instances dans chaque région Azure et Azure Resource Manager est déployé tooall Azure régions.  Par conséquent, dans la pratique, les limites sont effectivement beaucoup plus importantes que celles répertoriées ci-dessus, car les requêtes utilisateur sont généralement prises en charge par de nombreuses instances différentes.

Si votre application ou le script atteint ces limites, vous devez toothrottle vos demandes. Cette rubrique vous montre comment hello toodetermine restant demande que vous avez avant d’atteindre la limite de hello et toorespond lorsque vous avez atteint la limite de hello.

Lorsque vous atteignez la limite de hello, vous recevez le code d’état HTTP de hello **429 trop grand nombre de demandes**.

nombre de demandes de Hello est étendue tooeither votre abonnement ou votre client. Si vous avez plusieurs, applications simultanées qui effectue des demandes dans votre abonnement, hello requêtes à partir de ces applications sont ajoutées ensemble toodetermine hello quantité, pour les requêtes restantes.

Demandes d’abonnement d’une étendue sont celles hello impliquent le passage de votre id d’abonnement, telles que la récupération des groupes de ressources hello dans votre abonnement. Les requêtes étendues au locataire n’incluent pas votre ID d’abonnement, notamment pour la récupération des emplacements Azure valides.

## <a name="remaining-requests"></a>Requêtes restantes
Vous pouvez déterminer le nombre de hello d’autres demandes en examinant les en-têtes de réponse. Chaque demande inclut des valeurs pour le nombre de hello de restant en lecture et les demandes d’écriture. Hello tableau suivant décrit les en-têtes de réponse hello que vous pouvez examiner ces valeurs :

| En-tête de réponse | Description |
| --- | --- |
| x-ms-ratelimit-remaining-subscription-reads |Requêtes de lecture restantes étendues à l’abonnement |
| x-ms-ratelimit-remaining-subscription-writes |Requêtes d’écriture restantes étendues à l’abonnement |
| x-ms-ratelimit-remaining-tenant-reads |Requêtes de lecture restantes étendues au locataire |
| x-ms-ratelimit-remaining-tenant-writes |Requêtes d’écriture restantes étendues au locataire |
| x-ms-ratelimit-remaining-subscription-resource-requests |Requêtes de type de ressource restantes étendues à l’abonnement.<br /><br />Cette valeur d’en-tête est uniquement retournée si un service a remplacé la limite par défaut hello. Le Gestionnaire de ressources ajoute cette valeur au lieu de hello abonnement lectures ou écritures. |
| x-ms-ratelimit-remaining-subscription-resource-entities-read |Requêtes de collecte de type de ressource restantes étendues à l’abonnement.<br /><br />Cette valeur d’en-tête est uniquement retournée si un service a remplacé la limite par défaut hello. Cette valeur fournit un nombre de hello d’autres demandes de collecte (ressources de la liste). |
| x-ms-ratelimit-remaining-tenant-resource-requests |Requêtes de type de ressource restantes étendues au locataire.<br /><br />Cet en-tête est ajouté uniquement pour les demandes au niveau du client, et uniquement si un service a remplacé la limite par défaut hello. Le Gestionnaire de ressources ajoute cette valeur au lieu de hello client lectures ou écritures. |
| x-ms-ratelimit-remaining-tenant-resource-entities-read |Requêtes de collecte de type de ressource restantes étendues au locataire.<br /><br />Cet en-tête est ajouté uniquement pour les demandes au niveau du client, et uniquement si un service a remplacé la limite par défaut hello. |

## <a name="retrieving-hello-header-values"></a>La récupération des valeurs d’en-tête hello
La récupération de ces valeurs d’en-tête dans votre code ou script est similaire à la récupération de n’importe quelle valeur d’en-tête. 

Par exemple, dans **c#**, vous récupérez la valeur à partir de l’en-tête hello un **HttpWebResponse** objet nommé **réponse** avec hello suivant de code :

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

Dans **PowerShell**, vous récupériez la valeur d’en-tête hello à partir d’une opération Invoke-WebRequest.

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

Ou, si voulez restant de hello toosee des demandes pour le débogage, vous pouvez fournir hello **-déboguer** paramètre sur votre **PowerShell** applet de commande.

```powershell
Get-AzureRmResourceGroup -Debug
```

Qui retourne le nombre de valeurs, y compris hello suivant la valeur de la réponse :

```powershell
...
DEBUG: ============================ HTTP RESPONSE ============================

Status Code:
OK

Headers:
Pragma                        : no-cache
x-ms-ratelimit-remaining-subscription-reads: 14999
...
```

Dans **CLI d’Azure**, vous récupérer la valeur d’en-tête hello à l’aide de hello option plus détaillée.

```azurecli
azure group list -vv --json
```

Qui retourne le nombre de valeurs, y compris hello objet :

```azurecli
...
silly: returnObject
{
  "statusCode": 200,
  "header": {
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "x-ms-ratelimit-remaining-subscription-reads": "14998",
    ...
```

## <a name="waiting-before-sending-next-request"></a>Attente avant l’envoi de la requête suivante
Lorsque vous atteignez la limite de demandes hello, Gestionnaire de ressources renvoie hello **429** code d’état HTTP et un **Retry-After** valeur dans l’en-tête de hello. Hello **Retry-After** valeur spécifie le nombre de hello de secondes pendant lesquelles votre application doit attendre (ou en veille) avant d’envoyer la demande suivante de hello. Si vous envoyez une demande avant de la valeur de nouvelle tentative hello s’est écoulé, votre demande n’est pas traitée et une nouvelle valeur de nouvelle tentative est retournée.

## <a name="next-steps"></a>Étapes suivantes

* Pour plus d’informations sur les limites et les quotas, consultez [Abonnement Azure et limites, quotas et contraintes du service](../azure-subscription-service-limits.md).
* toolearn sur la gestion des demandes asynchrones de REST, consultez [le suivi des opérations asynchrones Azure](resource-manager-async-operations.md).
