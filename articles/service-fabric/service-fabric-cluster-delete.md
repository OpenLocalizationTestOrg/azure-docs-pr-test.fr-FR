---
title: aaaDelete Azure cluster et ses ressources | Documents Microsoft
description: "Découvrez comment toocompletely supprimer une structure de Service de cluster un groupe de ressources hello suppression contenant hello cluster ou en supprimant sélectivement des ressources."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: de422950-2d22-4ddb-ac47-dd663a946a7e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/24/2017
ms.author: chackdan
ms.openlocfilehash: 5c15a4184644da715cd69397f2150de86ab433ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-hello-resources-it-uses"></a><span data-ttu-id="cdef7-103">Supprimer un cluster Service Fabric sur les ressources Azure et hello qu’il utilise</span><span class="sxs-lookup"><span data-stu-id="cdef7-103">Delete a Service Fabric cluster on Azure and hello resources it uses</span></span>
<span data-ttu-id="cdef7-104">Un cluster Service Fabric est composé de nombreuses autres ressources Windows Azure en outre toohello du cluster lui-même.</span><span class="sxs-lookup"><span data-stu-id="cdef7-104">A Service Fabric cluster is made up of many other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="cdef7-105">Toocompletely supprimer un cluster Service Fabric, vous devez également toodelete que tous hello il est constitué de ressources.</span><span class="sxs-lookup"><span data-stu-id="cdef7-105">So toocompletely delete a Service Fabric cluster you also need toodelete all hello resources it is made of.</span></span>
<span data-ttu-id="cdef7-106">Vous avez deux options : un groupe de ressources hello delete hello cluster est dans (ce qui supprime la ressource de cluster hello et d’autres ressources dans le groupe de ressources hello) ou spécifiquement supprimer la ressource de cluster de hello et il est associé à des ressources (mais pas d’autres ressources de groupe de ressources hello).</span><span class="sxs-lookup"><span data-stu-id="cdef7-106">You have two options: Either delete hello resource group that hello cluster is in (which deletes hello cluster resource and any other resources in hello resource group) or specifically delete hello cluster resource and it's associated resources (but not other resources in hello resource group).</span></span>

> [!NOTE]
> <span data-ttu-id="cdef7-107">Suppression de ressource de cluster hello **pas** supprimer tous les hello d’autres ressources de votre cluster Service Fabric est composé de.</span><span class="sxs-lookup"><span data-stu-id="cdef7-107">Deleting hello cluster resource **does not** delete all hello other resources that your Service Fabric cluster is composed of.</span></span>
> 
> 

## <a name="delete-hello-entire-resource-group-rg-that-hello-service-fabric-cluster-is-in"></a><span data-ttu-id="cdef7-108">Supprimer le groupe de ressources entière hello (RG) qui hello Service Fabric cluster se trouve dans</span><span class="sxs-lookup"><span data-stu-id="cdef7-108">Delete hello entire resource group (RG) that hello Service Fabric cluster is in</span></span>
<span data-ttu-id="cdef7-109">Il s’agit de hello tooensure de façon plus simple que vous supprimez toutes les ressources de hello associées à votre cluster, y compris le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="cdef7-109">This is hello easiest way tooensure that you delete all hello resources associated with your cluster, including hello resource group.</span></span> <span data-ttu-id="cdef7-110">Vous pouvez supprimer le groupe de ressources hello à l’aide de PowerShell ou via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cdef7-110">You can delete hello resource group using PowerShell or through hello Azure portal.</span></span> <span data-ttu-id="cdef7-111">Si votre groupe de ressources comporte des ressources qui ne sont pas en cluster de l’ensemble fibre optique tooService connexes, vous pouvez supprimer des ressources spécifiques.</span><span class="sxs-lookup"><span data-stu-id="cdef7-111">If your resource group has resources that are not related tooService fabric cluster, then you can delete specific resources.</span></span>

### <a name="delete-hello-resource-group-using-azure-powershell"></a><span data-ttu-id="cdef7-112">Supprimer le groupe de ressources hello à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cdef7-112">Delete hello resource group using Azure PowerShell</span></span>
<span data-ttu-id="cdef7-113">Vous pouvez également supprimer le groupe de ressources hello en hello suivant d’applets de commande Azure PowerShell en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="cdef7-113">You can also delete hello resource group by running hello following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="cdef7-114">Vérifiez qu’Azure PowerShell 1.0 ou une version ultérieure est installé sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="cdef7-114">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="cdef7-115">Si vous n’avez pas fait avant, suivez les étapes de hello décrites dans [comment tooinstall et configurer Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="cdef7-115">If you have not done this before, follow hello steps outlined in [How tooinstall and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="cdef7-116">Ouvrez une fenêtre PowerShell et exécutez hello suivant d’applets de commande PS :</span><span class="sxs-lookup"><span data-stu-id="cdef7-116">Open a PowerShell window and run hello following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

<span data-ttu-id="cdef7-117">Vous obtiendrez une suppression de hello tooconfirm invite si vous n’utilisez pas hello *-Force* option.</span><span class="sxs-lookup"><span data-stu-id="cdef7-117">You will get a prompt tooconfirm hello deletion if you did not use hello *-Force* option.</span></span> <span data-ttu-id="cdef7-118">Confirmation de hello RG et toutes les ressources hello qu’il contient sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="cdef7-118">On confirmation hello RG and all hello resources it contains are deleted.</span></span>

### <a name="delete-a-resource-group-in-hello-azure-portal"></a><span data-ttu-id="cdef7-119">Supprimer un groupe de ressources Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="cdef7-119">Delete a resource group in hello Azure portal</span></span>
1. <span data-ttu-id="cdef7-120">Connexion toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cdef7-120">Login toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cdef7-121">Accédez à cluster Service Fabric de toohello vous souhaitez toodelete.</span><span class="sxs-lookup"><span data-stu-id="cdef7-121">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
3. <span data-ttu-id="cdef7-122">Cliquez sur hello le nom du groupe de ressources sur la page d’essentials hello cluster.</span><span class="sxs-lookup"><span data-stu-id="cdef7-122">Click on hello Resource Group name on hello cluster essentials page.</span></span>
4. <span data-ttu-id="cdef7-123">Ceci fait apparaître hello **Essentials du groupe de ressources** page.</span><span class="sxs-lookup"><span data-stu-id="cdef7-123">This brings up hello **Resource Group Essentials** page.</span></span>
5. <span data-ttu-id="cdef7-124">Cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="cdef7-124">Click **Delete**.</span></span>
6. <span data-ttu-id="cdef7-125">Suivez les instructions de hello sur cette page toocomplete hello la suppression du groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="cdef7-125">Follow hello instructions on that page toocomplete hello deletion of hello resource group.</span></span>

![Supprimer un groupe de ressources][ResourceGroupDelete]

## <a name="delete-hello-cluster-resource-and-hello-resources-it-uses-but-not-other-resources-in-hello-resource-group"></a><span data-ttu-id="cdef7-127">Supprimer la ressource de cluster hello et ressources hello qu’il utilise, mais pas d’autres ressources dans le groupe de ressources hello</span><span class="sxs-lookup"><span data-stu-id="cdef7-127">Delete hello cluster resource and hello resources it uses, but not other resources in hello resource group</span></span>
<span data-ttu-id="cdef7-128">Si votre groupe de ressources a uniquement les ressources qui sont le cluster Service Fabric de toohello connexes souhaité toodelete, il est plus facile groupe de ressource entier toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="cdef7-128">If your resource group has only resources that are related toohello Service Fabric cluster you want toodelete, then it is easier toodelete hello entire resource group.</span></span> <span data-ttu-id="cdef7-129">Si vous souhaitez que les ressources de hello tooselectively supprimer un par un dans votre groupe de ressources, puis procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="cdef7-129">If you want tooselectively delete hello resources one-by-one in your resource group, then follow these steps.</span></span>

<span data-ttu-id="cdef7-130">Si vous avez déployé votre cluster à l’aide du portail de hello ou à l’aide d’un des modèles du Gestionnaire de ressources de l’infrastructure de Service hello à partir de la galerie de modèles de hello, toutes les ressources hello hello de cluster utilise sont balisés avec hello suivant deux balises.</span><span class="sxs-lookup"><span data-stu-id="cdef7-130">If you deployed your cluster using hello portal or using one of hello Service Fabric Resource Manager templates from hello template gallery, then all hello resources that hello cluster uses are tagged with hello following two tags.</span></span> <span data-ttu-id="cdef7-131">Vous pouvez les utiliser toodecide les ressources que vous souhaitez toodelete.</span><span class="sxs-lookup"><span data-stu-id="cdef7-131">You can use them toodecide which resources you want toodelete.</span></span>

<span data-ttu-id="cdef7-132">***Balise n° 1 :*** clé = clusterName, valeur = « nom du cluster de hello »</span><span class="sxs-lookup"><span data-stu-id="cdef7-132">***Tag#1:*** Key = clusterName, Value = 'name of hello cluster'</span></span>

<span data-ttu-id="cdef7-133">***Balise 2 :*** Clé = resourceName, Valeur = ServiceFabric</span><span class="sxs-lookup"><span data-stu-id="cdef7-133">***Tag#2:*** Key = resourceName, Value = ServiceFabric</span></span>

### <a name="delete-specific-resources-in-hello-azure-portal"></a><span data-ttu-id="cdef7-134">Supprimer des ressources spécifiques dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="cdef7-134">Delete specific resources in hello Azure portal</span></span>
1. <span data-ttu-id="cdef7-135">Connexion toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cdef7-135">Login toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cdef7-136">Accédez à cluster Service Fabric de toohello vous souhaitez toodelete.</span><span class="sxs-lookup"><span data-stu-id="cdef7-136">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
3. <span data-ttu-id="cdef7-137">Accédez trop**tous les paramètres** sur le panneau d’essentials hello.</span><span class="sxs-lookup"><span data-stu-id="cdef7-137">Go too**All settings** on hello essentials blade.</span></span>
4. <span data-ttu-id="cdef7-138">Cliquez sur **balises** sous **gestion des ressources** dans le panneau des paramètres hello.</span><span class="sxs-lookup"><span data-stu-id="cdef7-138">Click on **Tags** under **Resource Management** in hello settings blade.</span></span>
5. <span data-ttu-id="cdef7-139">Cliquez sur un des hello **balises** dans tooget Panneau de balises hello une liste de toutes les ressources hello avec cette balise.</span><span class="sxs-lookup"><span data-stu-id="cdef7-139">Click on one of hello **Tags** in hello tags blade tooget a list of all hello resources with that tag.</span></span>
   
    ![Balises de ressource][ResourceTags]
6. <span data-ttu-id="cdef7-141">Une fois que vous avez liste hello de ressources avec balises, cliquez sur chacune des ressources de hello et les supprimer.</span><span class="sxs-lookup"><span data-stu-id="cdef7-141">Once you have hello list of tagged resources, click on each of hello resources and delete them.</span></span>
   
    ![Ressources balisées][TaggedResources]

### <a name="delete-hello-resources-using-azure-powershell"></a><span data-ttu-id="cdef7-143">Supprimer des ressources hello à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cdef7-143">Delete hello resources using Azure PowerShell</span></span>
<span data-ttu-id="cdef7-144">Vous pouvez supprimer des ressources de hello un-à-un en exécutant hello suivant d’applets de commande PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="cdef7-144">You can delete hello resources one-by-one by running hello following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="cdef7-145">Vérifiez qu’Azure PowerShell 1.0 ou une version ultérieure est installé sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="cdef7-145">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="cdef7-146">Si vous n’avez pas fait avant, suivez les étapes de hello décrites dans [comment tooinstall et configurer Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="cdef7-146">If you have not done this before, follow hello steps outlined in [How tooinstall and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="cdef7-147">Ouvrez une fenêtre PowerShell et exécutez hello suivant d’applets de commande PS :</span><span class="sxs-lookup"><span data-stu-id="cdef7-147">Open a PowerShell window and run hello following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="cdef7-148">Pour chacune des ressources de hello, vous souhaitez que toodelete, exécutez hello suivante :</span><span class="sxs-lookup"><span data-stu-id="cdef7-148">For each of hello resources you want toodelete, run hello following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of hello resource group>" -Force
```

<span data-ttu-id="cdef7-149">ressource de cluster hello toodelete, exécutez hello suivante :</span><span class="sxs-lookup"><span data-stu-id="cdef7-149">toodelete hello cluster resource, run hello following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of hello resource group>" -Force
```

## <a name="next-steps"></a><span data-ttu-id="cdef7-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cdef7-150">Next steps</span></span>
<span data-ttu-id="cdef7-151">Hello en lecture suivant tooalso en savoir plus sur la mise à niveau un cluster et le partitionnement des services :</span><span class="sxs-lookup"><span data-stu-id="cdef7-151">Read hello following tooalso learn about upgrading a cluster and partitioning services:</span></span>

* [<span data-ttu-id="cdef7-152">En savoir plus sur les mises à niveau de cluster</span><span class="sxs-lookup"><span data-stu-id="cdef7-152">Learn about cluster upgrades</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="cdef7-153">En savoir plus sur le partitionnement de services avec état pour une mise à l’échelle maximale</span><span class="sxs-lookup"><span data-stu-id="cdef7-153">Learn about partitioning stateful services for maximum scale</span></span>](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
