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
# <a name="use-tags-tooorganize-your-azure-resources"></a><span data-ttu-id="b57d9-103">Utiliser des balises tooorganize vos ressources Azure</span><span class="sxs-lookup"><span data-stu-id="b57d9-103">Use tags tooorganize your Azure resources</span></span>
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> <span data-ttu-id="b57d9-104">Vous pouvez appliquer des balises tooresources uniquement qui prennent en charge les opérations d’Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b57d9-104">You can apply tags only tooresources that support Azure Resource Manager operations.</span></span> <span data-ttu-id="b57d9-105">Si vous avez créé un ordinateur virtuel, un réseau virtuel ou un compte de stockage via le modèle de déploiement classique hello (telles que via hello portail Azure classic), vous ne pouvez pas appliquer une ressource de toothat de balise.</span><span class="sxs-lookup"><span data-stu-id="b57d9-105">If you created a virtual machine, virtual network, or storage account through hello classic deployment model (such as through hello Azure classic portal), you cannot apply a tag toothat resource.</span></span> <span data-ttu-id="b57d9-106">toosupport étiquetage, redéployez ces ressources via le Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="b57d9-106">toosupport tagging, redeploy these resources through Resource Manager.</span></span> <span data-ttu-id="b57d9-107">Toutes les autres ressources prennent en charge le balisage.</span><span class="sxs-lookup"><span data-stu-id="b57d9-107">All other resources support tagging.</span></span>
> 
> 

## <a name="policies-for-tag-consistency"></a><span data-ttu-id="b57d9-108">Stratégies pour la cohérence des balises</span><span class="sxs-lookup"><span data-stu-id="b57d9-108">Policies for tag consistency</span></span>

<span data-ttu-id="b57d9-109">Vous pouvez utiliser des règles standard toocreate de stratégies de ressources pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="b57d9-109">You can use resource policies toocreate standard rules for your organization.</span></span> <span data-ttu-id="b57d9-110">Vous pouvez créer des stratégies qui garantissent que les ressources sont balisés avec des valeurs appropriées de hello.</span><span class="sxs-lookup"><span data-stu-id="b57d9-110">You can create policies that ensure resources are tagged with hello appropriate values.</span></span> <span data-ttu-id="b57d9-111">Pour plus d’informations, consultez [Appliquer des stratégies de ressources pour les balises](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="b57d9-111">For more information, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="b57d9-112">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b57d9-112">PowerShell</span></span>
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a><span data-ttu-id="b57d9-113">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="b57d9-113">Azure CLI</span></span>

<span data-ttu-id="b57d9-114">toosee hello balises existantes pour un *groupe de ressources*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="b57d9-114">toosee hello existing tags for a *resource group*, use:</span></span>

```azurecli
az group show -n examplegroup --query tags
```

<span data-ttu-id="b57d9-115">Ce script renvoie hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="b57d9-115">That script returns hello following format:</span></span>

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

<span data-ttu-id="b57d9-116">toosee hello balises existantes pour un *ressource qui comporte un ID de ressource spécifié*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="b57d9-116">toosee hello existing tags for a *resource that has a specified resource ID*, use:</span></span>

```azurecli
az resource show --id {resource-id} --query tags
```

<span data-ttu-id="b57d9-117">Ou, toosee hello balises existantes pour un *ressource qui comporte un groupe spécifié de nom, type et des ressources*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="b57d9-117">Or, toosee hello existing tags for a *resource that has a specified name, type, and resource group*, use:</span></span>

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

<span data-ttu-id="b57d9-118">les groupes de ressources tooget qui ont une balise spécifique, utilisez `az group list`:</span><span class="sxs-lookup"><span data-stu-id="b57d9-118">tooget resource groups that have a specific tag, use `az group list`:</span></span>

```azurecli
az group list --tag Dept=IT
```

<span data-ttu-id="b57d9-119">l’utilisation de toutes les ressources hello qui ont une balise spécifique et une valeur, tooget `az resource list`:</span><span class="sxs-lookup"><span data-stu-id="b57d9-119">tooget all hello resources that have a particular tag and value, use `az resource list`:</span></span>

```azurecli
az resource list --tag Dept=Finance
```

<span data-ttu-id="b57d9-120">Chaque fois que vous appliquez des balises tooa ressource ou un groupe de ressources, vous remplacez les balises existantes hello sur cette ressource ou un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b57d9-120">Every time you apply tags tooa resource or a resource group, you overwrite hello existing tags on that resource or resource group.</span></span> <span data-ttu-id="b57d9-121">Par conséquent, vous devez utiliser une approche différente selon que hello ressource ou un groupe de ressources a des balises existantes.</span><span class="sxs-lookup"><span data-stu-id="b57d9-121">Therefore, you must use a different approach based on whether hello resource or resource group has existing tags.</span></span> 

<span data-ttu-id="b57d9-122">tooadd balises tooa *groupe de ressources sans balises existantes*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="b57d9-122">tooadd tags tooa *resource group without existing tags*, use:</span></span>

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

<span data-ttu-id="b57d9-123">tooadd balises tooa *ressource sans balises existantes*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="b57d9-123">tooadd tags tooa *resource without existing tags*, use:</span></span>

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

<span data-ttu-id="b57d9-124">tooadd balises tooa ressource qui a déjà des balises, récupérer les balises existantes hello, reformater cette valeur et réappliquer les balises existantes et nouvelles hello :</span><span class="sxs-lookup"><span data-stu-id="b57d9-124">tooadd tags tooa resource that already has tags, retrieve hello existing tags, reformat that value, and reapply hello existing and new tags:</span></span> 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

<span data-ttu-id="b57d9-125">tooapply toutes les balises à partir d’un groupe tooits ressources, et *ne conserve pas les balises existantes sur des ressources hello*, utilisez hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="b57d9-125">tooapply all tags from a resource group tooits resources, and *not retain existing tags on hello resources*, use hello following script:</span></span>

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

<span data-ttu-id="b57d9-126">tooapply toutes les balises à partir d’un groupe tooits ressources, et *conserver les balises existantes sur les ressources*, utilisez hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="b57d9-126">tooapply all tags from a resource group tooits resources, and *retain existing tags on resources*, use hello following script:</span></span>

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


## <a name="templates"></a><span data-ttu-id="b57d9-127">Modèles</span><span class="sxs-lookup"><span data-stu-id="b57d9-127">Templates</span></span>

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a><span data-ttu-id="b57d9-128">Portail</span><span class="sxs-lookup"><span data-stu-id="b57d9-128">Portal</span></span>
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a><span data-ttu-id="b57d9-129">API REST</span><span class="sxs-lookup"><span data-stu-id="b57d9-129">REST API</span></span>
<span data-ttu-id="b57d9-130">Hello portail Azure et PowerShell utilisent hello [REST API du Gestionnaire de ressources](https://docs.microsoft.com/rest/api/resources/) coulisses hello.</span><span class="sxs-lookup"><span data-stu-id="b57d9-130">hello Azure portal and PowerShell both use hello [Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) behind hello scenes.</span></span> <span data-ttu-id="b57d9-131">Si vous devez toointegrate le balisage dans un autre environnement, vous pouvez obtenir les balises à l’aide de **obtenir** sur hello ressource ID de mise à jour hello ensemble de balises à l’aide un **correctif** appeler.</span><span class="sxs-lookup"><span data-stu-id="b57d9-131">If you need toointegrate tagging into another environment, you can get tags by using **GET** on hello resource ID and update hello set of tags by using a **PATCH** call.</span></span>

## <a name="tags-and-billing"></a><span data-ttu-id="b57d9-132">Balises et facturation</span><span class="sxs-lookup"><span data-stu-id="b57d9-132">Tags and billing</span></span>
<span data-ttu-id="b57d9-133">Vous pouvez utiliser des balises toogroup vos données de facturation.</span><span class="sxs-lookup"><span data-stu-id="b57d9-133">You can use tags toogroup your billing data.</span></span> <span data-ttu-id="b57d9-134">Par exemple, si vous exécutez plusieurs ordinateurs virtuels pour différentes organisations, vous pouvez utiliser hello balises toogroup utilisation par centre de coûts.</span><span class="sxs-lookup"><span data-stu-id="b57d9-134">For example, if you are running multiple VMs for different organizations, use hello tags toogroup usage by cost center.</span></span> <span data-ttu-id="b57d9-135">Vous pouvez également utiliser des balises toocategorize coûts par l’environnement d’exécution, notamment l’utilisation de facturation hello pour les machines virtuelles en cours d’exécution dans un environnement de production hello.</span><span class="sxs-lookup"><span data-stu-id="b57d9-135">You can also use tags toocategorize costs by runtime environment, such as hello billing usage for VMs running in hello production environment.</span></span>


<span data-ttu-id="b57d9-136">Vous pouvez récupérer des informations sur les balises via hello [l’utilisation des ressources Azure et RateCard APIs](../billing/billing-usage-rate-card-overview.md) ou un fichier de valeurs séparées par des virgules (CSV) de l’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="b57d9-136">You can retrieve information about tags through hello [Azure Resource Usage and RateCard APIs](../billing/billing-usage-rate-card-overview.md) or hello usage comma-separated values (CSV) file.</span></span> <span data-ttu-id="b57d9-137">Vous téléchargez le fichier de l’utilisation de hello de hello [portail du compte Azure](https://account.windowsazure.com/) ou [portal d’EA](https://ea.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b57d9-137">You download hello usage file from hello [Azure account portal](https://account.windowsazure.com/) or [EA portal](https://ea.azure.com).</span></span> <span data-ttu-id="b57d9-138">Pour plus d’informations sur les informations de toobilling l’accès par programme, consultez [obtenir votre consommation de ressources Microsoft Azure](../billing/billing-usage-rate-card-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b57d9-138">For more information about programmatic access toobilling information, see [Gain insights into your Microsoft Azure resource consumption](../billing/billing-usage-rate-card-overview.md).</span></span> <span data-ttu-id="b57d9-139">Pour plus d’informations sur les opérations de l’API REST, consultez [Informations de référence sur l’API REST Azure Billing](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span><span class="sxs-lookup"><span data-stu-id="b57d9-139">For REST API operations, see [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span></span>


<span data-ttu-id="b57d9-140">Lorsque vous téléchargez l’utilisation de hello volume partagé de cluster pour les services qui prennent en charge les balises de facturation, hello apparaissent Bonjour **balises** colonne.</span><span class="sxs-lookup"><span data-stu-id="b57d9-140">When you download hello usage CSV for services that support tags with billing, hello tags appear in hello **Tags** column.</span></span> <span data-ttu-id="b57d9-141">Pour plus d’informations, consultez [Comprendre votre facture Microsoft Azure](../billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="b57d9-141">For more information, see [Understand your bill for Microsoft Azure](../billing/billing-understand-your-bill.md).</span></span>

![Voir les balises dans la facturation](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a><span data-ttu-id="b57d9-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b57d9-143">Next steps</span></span>
* <span data-ttu-id="b57d9-144">Vous pouvez appliquer des restrictions et des conventions sur votre abonnement avec des stratégies personnalisées.</span><span class="sxs-lookup"><span data-stu-id="b57d9-144">You can apply restrictions and conventions across your subscription by using customized policies.</span></span> <span data-ttu-id="b57d9-145">La stratégie que vous définissez peut exiger que toutes les ressources aient une valeur pour une balise en particulier.</span><span class="sxs-lookup"><span data-stu-id="b57d9-145">A policy that you define might require that all resources have a value for a particular tag.</span></span> <span data-ttu-id="b57d9-146">Pour plus d’informations, consultez [toomanage les stratégies exploitent et contrôler l’accès](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="b57d9-146">For more information, see [Use policies toomanage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="b57d9-147">Pour une présentation de toousing Azure PowerShell lorsque vous déployez des ressources, consultez [à l’aide de Azure PowerShell avec Azure Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b57d9-147">For an introduction toousing Azure PowerShell when you're deploying resources, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="b57d9-148">Pour un hello de toousing introduction CLI d’Azure lorsque vous déployez des ressources, consultez [Using hello CLI d’Azure pour Mac, Linux et Windows avec Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b57d9-148">For an introduction toousing hello Azure CLI when you're deploying resources, see [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="b57d9-149">Pour un portail de hello toousing de présentation, consultez [Using hello toomanage portail Azure vos ressources Azure](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b57d9-149">For an introduction toousing hello portal, see [Using hello Azure portal toomanage your Azure resources](resource-group-portal.md).</span></span>  
* <span data-ttu-id="b57d9-150">Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="b57d9-150">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

