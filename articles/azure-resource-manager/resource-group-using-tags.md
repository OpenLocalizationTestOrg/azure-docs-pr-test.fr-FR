---
title: "Organisation logique des ressources Azure à l’aide de balises | Microsoft Docs"
description: "Indique comment appliquer des balises afin d’organiser des ressources Azure dédiées à la facturation et à la gestion."
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
ms.openlocfilehash: 4f52c30614ad39da8a34ff6ecfb707b75400517f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-tags-to-organize-your-azure-resources"></a><span data-ttu-id="febbc-103">Organisation des ressources Azure à l’aide de balises</span><span class="sxs-lookup"><span data-stu-id="febbc-103">Use tags to organize your Azure resources</span></span>
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> <span data-ttu-id="febbc-104">Vous ne pouvez appliquer des balises qu’à des ressources qui prennent en charge les opérations Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="febbc-104">You can apply tags only to resources that support Azure Resource Manager operations.</span></span> <span data-ttu-id="febbc-105">Si vous avez créé une machine virtuelle, un réseau virtuel ou un compte de stockage par le biais du modèle de déploiement classique (tel que via le portail Azure classique), vous ne pouvez pas appliquer de balise à cette ressource.</span><span class="sxs-lookup"><span data-stu-id="febbc-105">If you created a virtual machine, virtual network, or storage account through the classic deployment model (such as through the Azure classic portal), you cannot apply a tag to that resource.</span></span> <span data-ttu-id="febbc-106">Pour prendre en charge le balisage, redéployez ces ressources via Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="febbc-106">To support tagging, redeploy these resources through Resource Manager.</span></span> <span data-ttu-id="febbc-107">Toutes les autres ressources prennent en charge le balisage.</span><span class="sxs-lookup"><span data-stu-id="febbc-107">All other resources support tagging.</span></span>
> 
> 

## <a name="policies-for-tag-consistency"></a><span data-ttu-id="febbc-108">Stratégies pour la cohérence des balises</span><span class="sxs-lookup"><span data-stu-id="febbc-108">Policies for tag consistency</span></span>

<span data-ttu-id="febbc-109">Les stratégies de ressources vous permettent de créer des règles standard pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="febbc-109">You can use resource policies to create standard rules for your organization.</span></span> <span data-ttu-id="febbc-110">Vous pouvez créer des stratégies qui garantissent que les ressources sont balisées avec les valeurs appropriées.</span><span class="sxs-lookup"><span data-stu-id="febbc-110">You can create policies that ensure resources are tagged with the appropriate values.</span></span> <span data-ttu-id="febbc-111">Pour plus d’informations, consultez [Appliquer des stratégies de ressources pour les balises](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="febbc-111">For more information, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="febbc-112">PowerShell</span><span class="sxs-lookup"><span data-stu-id="febbc-112">PowerShell</span></span>
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a><span data-ttu-id="febbc-113">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="febbc-113">Azure CLI</span></span>

<span data-ttu-id="febbc-114">Pour afficher les balises existantes pour un *groupe de ressources*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="febbc-114">To see the existing tags for a *resource group*, use:</span></span>

```azurecli
az group show -n examplegroup --query tags
```

<span data-ttu-id="febbc-115">Le script retourne les informations au format suivant :</span><span class="sxs-lookup"><span data-stu-id="febbc-115">That script returns the following format:</span></span>

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

<span data-ttu-id="febbc-116">Pour afficher les balises existantes pour une *ressource dont l’ID de ressource est spécifié*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="febbc-116">To see the existing tags for a *resource that has a specified resource ID*, use:</span></span>

```azurecli
az resource show --id {resource-id} --query tags
```

<span data-ttu-id="febbc-117">Alternativement, pour afficher les balises existantes pour une *ressource dont le nom, le type et le groupe sont spécifiés*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="febbc-117">Or, to see the existing tags for a *resource that has a specified name, type, and resource group*, use:</span></span>

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

<span data-ttu-id="febbc-118">Pour obtenir des groupes de ressources contenant une balise spécifique, utilisez `az group list` :</span><span class="sxs-lookup"><span data-stu-id="febbc-118">To get resource groups that have a specific tag, use `az group list`:</span></span>

```azurecli
az group list --tag Dept=IT
```

<span data-ttu-id="febbc-119">Pour obtenir toutes les ressources contenant une balise et une valeur spécifiques, utilisez `az resource list` :</span><span class="sxs-lookup"><span data-stu-id="febbc-119">To get all the resources that have a particular tag and value, use `az resource list`:</span></span>

```azurecli
az resource list --tag Dept=Finance
```

<span data-ttu-id="febbc-120">Chaque fois que vous appliquez des balises à une ressource ou un groupe de ressources, vous remplacez les balises existantes de cette ressource ou de ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="febbc-120">Every time you apply tags to a resource or a resource group, you overwrite the existing tags on that resource or resource group.</span></span> <span data-ttu-id="febbc-121">Par conséquent, vous devez utiliser une approche différente selon que la ressource ou le groupe de ressources a des balises existantes.</span><span class="sxs-lookup"><span data-stu-id="febbc-121">Therefore, you must use a different approach based on whether the resource or resource group has existing tags.</span></span> 

<span data-ttu-id="febbc-122">Pour ajouter des balises à un *groupe de ressources ne contenant pas de balises existantes*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="febbc-122">To add tags to a *resource group without existing tags*, use:</span></span>

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

<span data-ttu-id="febbc-123">Pour ajouter des balises à une *ressource ne contenant pas de balises existantes*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="febbc-123">To add tags to a *resource without existing tags*, use:</span></span>

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

<span data-ttu-id="febbc-124">Pour ajouter des balises à une ressource qui comporte déjà les balises, récupérez les balises existantes et reformatez cette valeur, puis réappliquez les balises nouvelles et existantes :</span><span class="sxs-lookup"><span data-stu-id="febbc-124">To add tags to a resource that already has tags, retrieve the existing tags, reformat that value, and reapply the existing and new tags:</span></span> 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

<span data-ttu-id="febbc-125">Pour appliquer toutes les balises d’un groupe de ressources à ses ressources *sans conserver les balises existantes*, utilisez le script suivant :</span><span class="sxs-lookup"><span data-stu-id="febbc-125">To apply all tags from a resource group to its resources, and *not retain existing tags on the resources*, use the following script:</span></span>

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

<span data-ttu-id="febbc-126">Pour appliquer toutes les balises d’un groupe de ressources à ses ressources *en conservant les balises existantes*, utilisez le script suivant :</span><span class="sxs-lookup"><span data-stu-id="febbc-126">To apply all tags from a resource group to its resources, and *retain existing tags on resources*, use the following script:</span></span>

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


## <a name="templates"></a><span data-ttu-id="febbc-127">Modèles</span><span class="sxs-lookup"><span data-stu-id="febbc-127">Templates</span></span>

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a><span data-ttu-id="febbc-128">Portail</span><span class="sxs-lookup"><span data-stu-id="febbc-128">Portal</span></span>
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a><span data-ttu-id="febbc-129">API REST</span><span class="sxs-lookup"><span data-stu-id="febbc-129">REST API</span></span>
<span data-ttu-id="febbc-130">Le portail Azure et PowerShell utilisent tous deux [l’API REST du Gestionnaire de ressources](https://docs.microsoft.com/rest/api/resources/) en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="febbc-130">The Azure portal and PowerShell both use the [Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) behind the scenes.</span></span> <span data-ttu-id="febbc-131">Si vous avez besoin d’intégrer le balisage dans un autre environnement, vous pouvez récupérer des balises en utilisant **GET** sur l’ID de ressource et mettre à jour le jeu de balises en utilisant un appel **PATCH**.</span><span class="sxs-lookup"><span data-stu-id="febbc-131">If you need to integrate tagging into another environment, you can get tags by using **GET** on the resource ID and update the set of tags by using a **PATCH** call.</span></span>

## <a name="tags-and-billing"></a><span data-ttu-id="febbc-132">Balises et facturation</span><span class="sxs-lookup"><span data-stu-id="febbc-132">Tags and billing</span></span>
<span data-ttu-id="febbc-133">Vous pouvez utiliser des balises pour regrouper vos données de facturation.</span><span class="sxs-lookup"><span data-stu-id="febbc-133">You can use tags to group your billing data.</span></span> <span data-ttu-id="febbc-134">Par exemple, si vous exécutez plusieurs machines virtuelles pour différentes organisations, vous pouvez recourir aux balises pour regrouper l’utilisation par centre de coûts.</span><span class="sxs-lookup"><span data-stu-id="febbc-134">For example, if you are running multiple VMs for different organizations, use the tags to group usage by cost center.</span></span> <span data-ttu-id="febbc-135">Vous pouvez également utiliser des balises pour catégoriser les coûts par environnement d’exécution ; par exemple, l’utilisation de la facturation pour les machines virtuelles en cours d’exécution dans l’environnement de production.</span><span class="sxs-lookup"><span data-stu-id="febbc-135">You can also use tags to categorize costs by runtime environment, such as the billing usage for VMs running in the production environment.</span></span>


<span data-ttu-id="febbc-136">Vous pouvez récupérer des informations sur les balises par le biais des [API Resource Usage et RateCard](../billing/billing-usage-rate-card-overview.md) ou du fichier de valeurs séparées par des virgules (CSV).</span><span class="sxs-lookup"><span data-stu-id="febbc-136">You can retrieve information about tags through the [Azure Resource Usage and RateCard APIs](../billing/billing-usage-rate-card-overview.md) or the usage comma-separated values (CSV) file.</span></span> <span data-ttu-id="febbc-137">Téléchargez le fichier d’utilisation depuis le [portail des comptes Azure](https://account.windowsazure.com/) ou depuis le [portail EA](https://ea.azure.com).</span><span class="sxs-lookup"><span data-stu-id="febbc-137">You download the usage file from the [Azure account portal](https://account.windowsazure.com/) or [EA portal](https://ea.azure.com).</span></span> <span data-ttu-id="febbc-138">Pour plus d’informations sur l’accès par programme aux informations de facturation, consultez [Obtenir une vue d’ensemble de votre consommation des ressources Microsoft Azure](../billing/billing-usage-rate-card-overview.md).</span><span class="sxs-lookup"><span data-stu-id="febbc-138">For more information about programmatic access to billing information, see [Gain insights into your Microsoft Azure resource consumption](../billing/billing-usage-rate-card-overview.md).</span></span> <span data-ttu-id="febbc-139">Pour plus d’informations sur les opérations de l’API REST, consultez [Informations de référence sur l’API REST Azure Billing](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span><span class="sxs-lookup"><span data-stu-id="febbc-139">For REST API operations, see [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span></span>


<span data-ttu-id="febbc-140">Lorsque vous téléchargez le fichier CSV d’utilisation pour les services qui prennent en charge les balises avec la facturation, les balises s’affichent dans la colonne **Balises** .</span><span class="sxs-lookup"><span data-stu-id="febbc-140">When you download the usage CSV for services that support tags with billing, the tags appear in the **Tags** column.</span></span> <span data-ttu-id="febbc-141">Pour plus d’informations, consultez [Comprendre votre facture Microsoft Azure](../billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="febbc-141">For more information, see [Understand your bill for Microsoft Azure](../billing/billing-understand-your-bill.md).</span></span>

![Voir les balises dans la facturation](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a><span data-ttu-id="febbc-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="febbc-143">Next steps</span></span>
* <span data-ttu-id="febbc-144">Vous pouvez appliquer des restrictions et des conventions sur votre abonnement avec des stratégies personnalisées.</span><span class="sxs-lookup"><span data-stu-id="febbc-144">You can apply restrictions and conventions across your subscription by using customized policies.</span></span> <span data-ttu-id="febbc-145">La stratégie que vous définissez peut exiger que toutes les ressources aient une valeur pour une balise en particulier.</span><span class="sxs-lookup"><span data-stu-id="febbc-145">A policy that you define might require that all resources have a value for a particular tag.</span></span> <span data-ttu-id="febbc-146">Pour plus d'informations, consultez [Utiliser les stratégies pour gérer les ressources et contrôler l'accès](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="febbc-146">For more information, see [Use policies to manage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="febbc-147">Pour plus d’informations sur l’utilisation d’Azure PowerShell lors du déploiement de ressources, consultez [Utilisation d’Azure PowerShell avec Azure Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="febbc-147">For an introduction to using Azure PowerShell when you're deploying resources, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="febbc-148">Si vous n’avez jamais utilisé l’interface CLI Azure pour le déploiement de ressources, consultez [Utiliser l’interface CLI Azure pour Mac, Linux et Windows avec Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="febbc-148">For an introduction to using the Azure CLI when you're deploying resources, see [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="febbc-149">Pour plus d’informations sur l’utilisation du portail, consultez [Utilisation du portail Azure pour gérer vos ressources Azure](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="febbc-149">For an introduction to using the portal, see [Using the Azure portal to manage your Azure resources](resource-group-portal.md).</span></span>  
* <span data-ttu-id="febbc-150">Pour obtenir des conseils sur l’utilisation de Resource Manager par les entreprises pour gérer efficacement les abonnements, voir [Structure d’Azure Enterprise - Gouvernance normative de l’abonnement](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="febbc-150">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

