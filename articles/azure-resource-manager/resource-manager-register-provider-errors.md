---
title: "Erreurs d’inscription de fournisseurs de ressources Azure | Microsoft Docs"
description: "Décrit comment résoudre les erreurs d’inscription de fournisseurs de ressources Azure."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: support-article
ms.date: 09/13/2017
ms.author: tomfitz
ms.openlocfilehash: d6a99917e732a3439a31cafa5608348694014054
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="resolve-errors-for-resource-provider-registration"></a>Résoudre les erreurs d’inscription de fournisseurs de ressources

Cet article décrit les erreurs que vous pouvez rencontrer quand vous utilisez un fournisseur de ressources que vous n’avez pas jamais utilisé auparavant dans votre abonnement.

## <a name="symptom"></a>Symptôme

Lorsque vous déployez une ressource, vous pouvez recevoir le message et le code d’erreur suivants :

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

Vous pouvez sinon recevoir un message similaire indiquant :

```
Code: MissingSubscriptionRegistration
Message: The subscription is not registered to use namespace {resource-provider-namespace}
```

## <a name="cause"></a>Cause :

Ces erreurs apparaissent pour l’une des trois raisons suivantes :

1. Le fournisseur de ressources n’a pas été inscrit pour votre abonnement.
1. La version de l’API n’est pas prise en charge pour le type de ressource.
1. L’emplacement n’est pas pris en charge pour le type de ressource.

## <a name="solution"></a>Solution

Le message d’erreur doit fournir des suggestions pour les emplacements et les versions d’API pris en charge. Vous pouvez changer votre modèle en l’une des valeurs suggérées. La plupart des fournisseurs sont inscrits automatiquement par le portail Azure ou l’interface de ligne de commande que vous utilisez, mais pas tous. Si vous n’avez pas déjà utilisé un fournisseur de ressources spécifique, vous devrez peut-être inscrire ce dernier. Vous pouvez en savoir plus sur les fournisseurs de ressources via PowerShell ou l’interface de ligne de commande Azure.

### <a name="solution-1"></a>Solution 1

Pour PowerShell, utilisez **Get-AzureRmResourceProvider** pour afficher l’état de votre inscription.

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

Pour inscrire un fournisseur, utilisez **Register-AzureRmResourceProvider** et indiquez le nom du fournisseur de ressources que vous voulez inscrire.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

Pour obtenir les emplacements pris en charge d’un type particulier de ressource, utilisez la commande suivante :

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

Pour obtenir les versions d’API prises en charge d’un type particulier de ressource, utilisez la commande suivante :

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

### <a name="solution-2"></a>Solution 2

**Interface de ligne de commande Azure**

Pour voir si le fournisseur est inscrit, utilisez la commande `az provider list` .

```azurecli-interactive
az provider list
```

Pour inscrire un fournisseur de ressources, utilisez la commande `az provider register` et indiquez *l’espace de noms* à inscrire.

```azurecli-interactive
az provider register --namespace Microsoft.Cdn
```

Pour afficher les emplacements et les versions d’API pris en charge pour un type de ressources, utilisez la commande suivante :

```azurecli-interactive
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

### <a name="solution-3"></a>Solution 3

Vous pouvez voir l’état de l’inscription et inscrire un espace de noms de fournisseur de ressources par le biais du portail.

1. Sur votre abonnement, sélectionnez **Fournisseurs de ressources**.

   ![sélectionner Fournisseurs de ressources](./media/resource-manager-register-provider-errors/select-resource-provider.png)

1. Passez en revue la liste des fournisseurs de ressources et, si nécessaire, sélectionnez le lien **Inscrire** pour inscrire le fournisseur de ressources du type que vous voulez déployer.

   ![répertorier les fournisseurs de ressources](./media/resource-manager-register-provider-errors/list-resource-providers.png)
