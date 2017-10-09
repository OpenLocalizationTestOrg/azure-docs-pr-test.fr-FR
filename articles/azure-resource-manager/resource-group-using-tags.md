---
title: "aaaTag Azure ressources pour l’organisation logique | Documents Microsoft"
description: Montre comment les balises tooapply tooorganize Azure ressources de facturation et de gestion.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 003a78e5-2ff8-4685-93b4-e94d6fb8ed5b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: AzurePortal
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tomfitz
ms.openlocfilehash: e07470463d160f8cefe5c80bc91e66a96af6ca45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-tags-tooorganize-your-azure-resources"></a>Utiliser des balises tooorganize vos ressources Azure
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> Vous pouvez appliquer des balises tooresources uniquement qui prennent en charge les opérations d’Azure Resource Manager. Si vous avez créé un ordinateur virtuel, un réseau virtuel ou un compte de stockage via le modèle de déploiement classique hello (telles que via hello portail Azure classic), vous ne pouvez pas appliquer une ressource de toothat de balise. toosupport étiquetage, redéployez ces ressources via le Gestionnaire de ressources. Toutes les autres ressources prennent en charge le balisage.
> 
> 

## <a name="policies-for-tag-consistency"></a>Stratégies pour la cohérence des balises

Vous pouvez utiliser des règles standard toocreate de stratégies de ressources pour votre organisation. Vous pouvez créer des stratégies qui garantissent que les ressources sont balisés avec des valeurs appropriées de hello. Pour plus d’informations, consultez [Appliquer des stratégies de ressources pour les balises](resource-manager-policy-tags.md).

## <a name="powershell"></a>PowerShell
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a>Interface de ligne de commande Azure

toosee hello balises existantes pour un *groupe de ressources*, utilisez :

```azurecli
az group show -n examplegroup --query tags
```

Ce script renvoie hello suivant le format :

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

toosee hello balises existantes pour un *ressource qui comporte un ID de ressource spécifié*, utilisez :

```azurecli
az resource show --id {resource-id} --query tags
```

Ou, toosee hello balises existantes pour un *ressource qui comporte un groupe spécifié de nom, type et des ressources*, utilisez :

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

les groupes de ressources tooget qui ont une balise spécifique, utilisez `az group list`:

```azurecli
az group list --tag Dept=IT
```

l’utilisation de toutes les ressources hello qui ont une balise spécifique et une valeur, tooget `az resource list`:

```azurecli
az resource list --tag Dept=Finance
```

Chaque fois que vous appliquez des balises tooa ressource ou un groupe de ressources, vous remplacez les balises existantes hello sur cette ressource ou un groupe de ressources. Par conséquent, vous devez utiliser une approche différente selon que hello ressource ou un groupe de ressources a des balises existantes. 

tooadd balises tooa *groupe de ressources sans balises existantes*, utilisez :

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

tooadd balises tooa *ressource sans balises existantes*, utilisez :

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

tooadd balises tooa ressource qui a déjà des balises, récupérer les balises existantes hello, reformater cette valeur et réappliquer les balises existantes et nouvelles hello : 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

tooapply toutes les balises à partir d’un groupe tooits ressources, et *ne conserve pas les balises existantes sur des ressources hello*, utilisez hello script suivant :

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    az resource tag --tags $t --id $resid
  done 
done
```

tooapply toutes les balises à partir d’un groupe tooits ressources, et *conserver les balises existantes sur les ressources*, utilisez hello script suivant :

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    jsonrtag=$(az resource show --id $resid --query tags)
    rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
    az resource tag --tags $t$rt --id $resid
  done 
done
```


## <a name="templates"></a>Modèles

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a>Portail
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a>API REST
Hello portail Azure et PowerShell utilisent hello [REST API du Gestionnaire de ressources](https://docs.microsoft.com/rest/api/resources/) coulisses hello. Si vous devez toointegrate le balisage dans un autre environnement, vous pouvez obtenir les balises à l’aide de **obtenir** sur hello ressource ID de mise à jour hello ensemble de balises à l’aide un **correctif** appeler.

## <a name="tags-and-billing"></a>Balises et facturation
Vous pouvez utiliser des balises toogroup vos données de facturation. Par exemple, si vous exécutez plusieurs ordinateurs virtuels pour différentes organisations, vous pouvez utiliser hello balises toogroup utilisation par centre de coûts. Vous pouvez également utiliser des balises toocategorize coûts par l’environnement d’exécution, notamment l’utilisation de facturation hello pour les machines virtuelles en cours d’exécution dans un environnement de production hello.


Vous pouvez récupérer des informations sur les balises via hello [l’utilisation des ressources Azure et RateCard APIs](../billing/billing-usage-rate-card-overview.md) ou un fichier de valeurs séparées par des virgules (CSV) de l’utilisation de hello. Vous téléchargez le fichier de l’utilisation de hello de hello [portail du compte Azure](https://account.windowsazure.com/) ou [portal d’EA](https://ea.azure.com). Pour plus d’informations sur les informations de toobilling l’accès par programme, consultez [obtenir votre consommation de ressources Microsoft Azure](../billing/billing-usage-rate-card-overview.md). Pour plus d’informations sur les opérations de l’API REST, consultez [Informations de référence sur l’API REST Azure Billing](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).


Lorsque vous téléchargez l’utilisation de hello volume partagé de cluster pour les services qui prennent en charge les balises de facturation, hello apparaissent Bonjour **balises** colonne. Pour plus d’informations, consultez [Comprendre votre facture Microsoft Azure](../billing/billing-understand-your-bill.md).

![Voir les balises dans la facturation](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a>Étapes suivantes
* Vous pouvez appliquer des restrictions et des conventions sur votre abonnement avec des stratégies personnalisées. La stratégie que vous définissez peut exiger que toutes les ressources aient une valeur pour une balise en particulier. Pour plus d’informations, consultez [toomanage les stratégies exploitent et contrôler l’accès](resource-manager-policy.md).
* Pour une présentation de toousing Azure PowerShell lorsque vous déployez des ressources, consultez [à l’aide de Azure PowerShell avec Azure Resource Manager](powershell-azure-resource-manager.md).
* Pour un hello de toousing introduction CLI d’Azure lorsque vous déployez des ressources, consultez [Using hello CLI d’Azure pour Mac, Linux et Windows avec Azure Resource Manager](xplat-cli-azure-resource-manager.md).
* Pour un portail de hello toousing de présentation, consultez [Using hello toomanage portail Azure vos ressources Azure](resource-group-portal.md).  
* Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).

