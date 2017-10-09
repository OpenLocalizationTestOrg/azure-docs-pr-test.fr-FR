---
title: aaaAzure fournisseurs de ressources et les types de ressources | Documents Microsoft
description: "Décrit les fournisseurs de ressources hello qui prennent en charge le Gestionnaire de ressources, leurs schémas et les versions disponibles de l’API et les régions hello qui peuvent héberger des ressources de hello."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 3c7a6fe4-371a-40da-9ebe-b574f583305b
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 23db1d3808a20166f3b44ec801e1bcc46fbb9bd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-providers-and-types"></a>Fournisseurs et types de ressources

Lorsque vous déployez des ressources, vous devez fréquemment tooretrieve d’informations sur les types et les fournisseurs de ressources hello. Dans cet article, vous apprenez à :

* Afficher tous les fournisseurs de ressources dans Azure
* Vérifier l’état de l’inscription d’un fournisseur de ressources
* Inscrire un fournisseur de ressources
* Afficher les types de ressources pour un fournisseur de ressources
* Afficher les emplacements valides pour un type de ressource
* Afficher les versions d’API valides pour un type de ressource

Vous pouvez effectuer ces étapes via le portail de hello, PowerShell ou CLI d’Azure.

## <a name="powershell"></a>PowerShell

toosee tous les fournisseurs de ressources dans Azure et l’état de l’inscription de hello pour votre abonnement, utilisent :

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

Qui retourne des résultats semblables à :

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

L’inscription d’un fournisseur de ressources de configure toowork de votre abonnement avec le fournisseur de ressources hello. étendue Hello pour l’inscription est toujours hello abonnement. Par défaut, de nombreux fournisseurs de ressources sont enregistrés automatiquement. Toutefois, vous devrez peut-être toomanually inscrire des fournisseurs de ressources. tooregister un fournisseur de ressources, vous devez avoir hello de tooperform autorisation `/register/action` opération hello pour fournisseur de ressources. Cette opération est incluse dans hello collaborateurs et les rôles de propriétaire.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

Qui retourne des résultats semblables à :

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

Vous ne pouvez pas annuler l’inscription d’un fournisseur de ressources lorsque vous avez encore des types de ressources de ce fournisseur de ressources dans votre abonnement.

informations de toosee pour un fournisseur de ressources particulier, utilisez :

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

Qui retourne des résultats semblables à :

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

types de ressources toosee hello pour un fournisseur de ressources, utilisez :

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

Résultat :

```powershell
batchAccounts
operations
locations
locations/quotas
```

version de l’API Hello correspond version tooa d’opérations d’API REST publiées par le fournisseur de ressources hello. Comme un fournisseur de ressources permet de nouvelles fonctionnalités, il libère une nouvelle version de hello API REST. 

versions disponibles API tooget hello pour un type de ressource, utilisez :

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

Résultat :

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

Le Gestionnaire de ressources est pris en charge dans toutes les régions, mais les ressources hello que vous déployez ne peuvent pas être pris en charge dans toutes les régions. En outre, il peut être sur votre abonnement, les limitations qui vous empêchent d’utiliser certaines régions qui prennent en charge la ressource de hello. 

tooget les emplacements de hello pris en charge pour un type de ressource, utilisez.

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

Résultat :

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a>Interface de ligne de commande Azure
toosee tous les fournisseurs de ressources dans Azure et l’état de l’inscription de hello pour votre abonnement, utilisent :

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

Qui retourne des résultats semblables à :

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

L’inscription d’un fournisseur de ressources de configure toowork de votre abonnement avec le fournisseur de ressources hello. étendue Hello pour l’inscription est toujours hello abonnement. Par défaut, de nombreux fournisseurs de ressources sont enregistrés automatiquement. Toutefois, vous devrez peut-être toomanually inscrire des fournisseurs de ressources. tooregister un fournisseur de ressources, vous devez avoir hello de tooperform autorisation `/register/action` opération hello pour fournisseur de ressources. Cette opération est incluse dans hello collaborateurs et les rôles de propriétaire.

```azurecli
az provider register --namespace Microsoft.Batch
```

Qui retourne un message indiquant que l’inscription est en cours.

Vous ne pouvez pas annuler l’inscription d’un fournisseur de ressources lorsque vous avez encore des types de ressources de ce fournisseur de ressources dans votre abonnement.

informations de toosee pour un fournisseur de ressources particulier, utilisez :

```azurecli
az provider show --namespace Microsoft.Batch
```

Qui retourne des résultats semblables à :

```azurecli
{
    "id": "/subscriptions/####-####/providers/Microsoft.Batch",
    "namespace": "Microsoft.Batch",
    "registrationsState": "Registering",
    "resourceTypes:" [
        ...
    ]
}
```

types de ressources toosee hello pour un fournisseur de ressources, utilisez :

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

Résultat :

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

version de l’API Hello correspond version tooa d’opérations d’API REST publiées par le fournisseur de ressources hello. Comme un fournisseur de ressources permet de nouvelles fonctionnalités, il libère une nouvelle version de hello API REST. 

versions disponibles API tooget hello pour un type de ressource, utilisez :

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

Résultat :

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

Le Gestionnaire de ressources est pris en charge dans toutes les régions, mais les ressources hello que vous déployez ne peuvent pas être pris en charge dans toutes les régions. En outre, il peut être sur votre abonnement, les limitations qui vous empêchent d’utiliser certaines régions qui prennent en charge la ressource de hello. 

tooget les emplacements de hello pris en charge pour un type de ressource, utilisez.

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

Résultat :

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a>Portail

sélectionner de tous les fournisseurs de ressources dans Azure et l’état de l’inscription de hello pour votre abonnement, toosee **abonnements**.

![sélectionner les abonnements](./media/resource-manager-supported-services/select-subscriptions.png)

Choisissez hello abonnement tooview.

![spécifier l’abonnement](./media/resource-manager-supported-services/subscription.png)

Sélectionnez **fournisseurs de ressources** et afficher la liste des fournisseurs de ressources disponibles hello.

![afficher les fournisseurs de ressources](./media/resource-manager-supported-services/show-resource-providers.png)

L’inscription d’un fournisseur de ressources de configure toowork de votre abonnement avec le fournisseur de ressources hello. étendue Hello pour l’inscription est toujours hello abonnement. Par défaut, de nombreux fournisseurs de ressources sont enregistrés automatiquement. Toutefois, vous devrez peut-être toomanually inscrire des fournisseurs de ressources. tooregister un fournisseur de ressources, vous devez avoir hello de tooperform autorisation `/register/action` opération hello pour fournisseur de ressources. Cette opération est incluse dans hello collaborateurs et les rôles de propriétaire. tooregister un fournisseur de ressources, sélectionnez **inscrire**.

![inscrire un fournisseur de ressources](./media/resource-manager-supported-services/register-provider.png)

Vous ne pouvez pas annuler l’inscription d’un fournisseur de ressources lorsque vous avez encore des types de ressources de ce fournisseur de ressources dans votre abonnement.

informations toosee pour un fournisseur de ressources particulier, sélectionnez **davantage de services**.

![sélectionner d’autres services](./media/resource-manager-supported-services/more-services.png)

Recherchez **l’Explorateur de ressources** et sélectionnez-le dans les options disponibles hello.

![sélectionner l’Explorateur de ressources](./media/resource-manager-supported-services/select-resource-explorer.png)

Sélectionnez **Fournisseurs**.

![sélectionner les fournisseurs](./media/resource-manager-supported-services/select-providers.png)

Ressources et fournisseur de ressources hello sélectionnez le type que vous souhaitez tooview.

![sélectionner le type de ressource](./media/resource-manager-supported-services/select-resource-type.png)

Le Gestionnaire de ressources est pris en charge dans toutes les régions, mais les ressources hello que vous déployez ne peuvent pas être pris en charge dans toutes les régions. En outre, il peut être sur votre abonnement, les limitations qui vous empêchent d’utiliser certaines régions qui prennent en charge la ressource de hello. l’Explorateur de ressources Hello affiche des emplacements valides pour le type de ressource hello.

![afficher les emplacements](./media/resource-manager-supported-services/show-locations.png)

version de l’API Hello correspond version tooa d’opérations d’API REST publiées par le fournisseur de ressources hello. Comme un fournisseur de ressources permet de nouvelles fonctionnalités, il libère une nouvelle version de hello API REST. l’Explorateur de ressources Hello affiche les versions des API valides pour le type de ressource hello.

![afficher les versions d’API](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a>Étapes suivantes
* toolearn sur la création de modèles du Gestionnaire de ressources, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).
* toolearn sur le déploiement de ressources, consultez [déployer une application avec le modèle Azure Resource Manager](resource-group-template-deploy.md).
* opérations de hello tooview pour un fournisseur de ressources, consultez [API REST Azure](/rest/api/).

