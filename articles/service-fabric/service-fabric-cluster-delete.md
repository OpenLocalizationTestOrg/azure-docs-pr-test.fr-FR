---
title: Supprimer un cluster Azure et ses ressources | Microsoft Docs
description: "Découvrez comment supprimer complètement un cluster Service Fabric en supprimant le groupe de ressources dans lequel il se trouve ou en supprimant les ressources individuellement."
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
ms.openlocfilehash: 7672aa12421fbe4ad86e7315d6a7a06c2ff5124d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-the-resources-it-uses"></a><span data-ttu-id="c0ec6-103">Supprimer un cluster Service Fabric sur Azure et les ressources qu’il utilise</span><span class="sxs-lookup"><span data-stu-id="c0ec6-103">Delete a Service Fabric cluster on Azure and the resources it uses</span></span>
<span data-ttu-id="c0ec6-104">Un cluster Service Fabric est composé de nombreuses ressources Azure en plus de la ressource de cluster elle-même.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-104">A Service Fabric cluster is made up of many other Azure resources in addition to the cluster resource itself.</span></span> <span data-ttu-id="c0ec6-105">Pour supprimer complètement un cluster Service Fabric, vous devez également supprimer toutes les ressources qui le composent.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-105">So to completely delete a Service Fabric cluster you also need to delete all the resources it is made of.</span></span>
<span data-ttu-id="c0ec6-106">Vous pouvez procéder de deux façons : vous pouvez supprimer le groupe de ressources dans lequel est situé le cluster (ce qui supprime la ressource de cluster et toutes les autres ressources du groupe de ressources) ou supprimer spécifiquement la ressource de cluster et les ressources associées (mais pas d’autres ressources du groupe de ressources).</span><span class="sxs-lookup"><span data-stu-id="c0ec6-106">You have two options: Either delete the resource group that the cluster is in (which deletes the cluster resource and any other resources in the resource group) or specifically delete the cluster resource and it's associated resources (but not other resources in the resource group).</span></span>

> [!NOTE]
> <span data-ttu-id="c0ec6-107">La suppression de la ressource de cluster n’entraîne **pas** celle de toutes les autres ressources composant votre cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-107">Deleting the cluster resource **does not** delete all the other resources that your Service Fabric cluster is composed of.</span></span>
> 
> 

## <a name="delete-the-entire-resource-group-rg-that-the-service-fabric-cluster-is-in"></a><span data-ttu-id="c0ec6-108">Supprimer l’ensemble du groupe de ressources dans lequel se trouve le cluster Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c0ec6-108">Delete the entire resource group (RG) that the Service Fabric cluster is in</span></span>
<span data-ttu-id="c0ec6-109">Il s’agit du moyen le plus simple pour vous assurer de supprimer toutes les ressources associées à votre cluster, y compris le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-109">This is the easiest way to ensure that you delete all the resources associated with your cluster, including the resource group.</span></span> <span data-ttu-id="c0ec6-110">Vous pouvez supprimer le groupe de ressources à l’aide de PowerShell ou du Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-110">You can delete the resource group using PowerShell or through the Azure portal.</span></span> <span data-ttu-id="c0ec6-111">Si votre groupe de ressources comporte des ressources qui ne sont pas liées au cluster Service Fabric, vous pouvez supprimer des ressources spécifiques.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-111">If your resource group has resources that are not related to Service fabric cluster, then you can delete specific resources.</span></span>

### <a name="delete-the-resource-group-using-azure-powershell"></a><span data-ttu-id="c0ec6-112">Supprimer le groupe de ressources à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0ec6-112">Delete the resource group using Azure PowerShell</span></span>
<span data-ttu-id="c0ec6-113">Vous pouvez également supprimer le groupe de ressources en exécutant les applets de commande Azure PowerShell suivantes.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-113">You can also delete the resource group by running the following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="c0ec6-114">Vérifiez qu’Azure PowerShell 1.0 ou une version ultérieure est installé sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-114">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="c0ec6-115">Si ce n’est déjà fait, suivez les étapes décrites dans [Installation et configuration d’Azure PowerShell](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="c0ec6-115">If you have not done this before, follow the steps outlined in [How to install and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="c0ec6-116">Ouvrez une fenêtre PowerShell et exécutez les applets de commande PS suivantes :</span><span class="sxs-lookup"><span data-stu-id="c0ec6-116">Open a PowerShell window and run the following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

<span data-ttu-id="c0ec6-117">Vous êtes invité à confirmer la suppression si vous n’avez pas utilisé l’option *-Force* .</span><span class="sxs-lookup"><span data-stu-id="c0ec6-117">You will get a prompt to confirm the deletion if you did not use the *-Force* option.</span></span> <span data-ttu-id="c0ec6-118">Après confirmation, le groupe de ressources et toutes les ressources qu’il contient sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-118">On confirmation the RG and all the resources it contains are deleted.</span></span>

### <a name="delete-a-resource-group-in-the-azure-portal"></a><span data-ttu-id="c0ec6-119">Supprimer un groupe de ressources dans le Portail Azure</span><span class="sxs-lookup"><span data-stu-id="c0ec6-119">Delete a resource group in the Azure portal</span></span>
1. <span data-ttu-id="c0ec6-120">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c0ec6-120">Login to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c0ec6-121">Accédez au cluster Service Fabric que vous souhaitez supprimer.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-121">Navigate to the Service Fabric cluster you want to delete.</span></span>
3. <span data-ttu-id="c0ec6-122">Cliquez sur le nom du groupe de ressources sur la page des éléments essentiels du cluster.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-122">Click on the Resource Group name on the cluster essentials page.</span></span>
4. <span data-ttu-id="c0ec6-123">Cela fait apparaître la page **Essentials du groupe de ressources** .</span><span class="sxs-lookup"><span data-stu-id="c0ec6-123">This brings up the **Resource Group Essentials** page.</span></span>
5. <span data-ttu-id="c0ec6-124">Cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-124">Click **Delete**.</span></span>
6. <span data-ttu-id="c0ec6-125">Suivez les instructions de cette page pour procéder à la suppression du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-125">Follow the instructions on that page to complete the deletion of the resource group.</span></span>

![Supprimer un groupe de ressources][ResourceGroupDelete]

## <a name="delete-the-cluster-resource-and-the-resources-it-uses-but-not-other-resources-in-the-resource-group"></a><span data-ttu-id="c0ec6-127">Supprimer la ressource de cluster et les ressources associées, mais pas d’autres ressources du groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="c0ec6-127">Delete the cluster resource and the resources it uses, but not other resources in the resource group</span></span>
<span data-ttu-id="c0ec6-128">Si votre groupe de ressources comporte uniquement des ressources qui sont liées au cluster Service Fabric à supprimer, il est plus facile de supprimer l’ensemble du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-128">If your resource group has only resources that are related to the Service Fabric cluster you want to delete, then it is easier to delete the entire resource group.</span></span> <span data-ttu-id="c0ec6-129">Si vous souhaitez supprimer certaines ressources de votre groupe de ressources individuellement, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-129">If you want to selectively delete the resources one-by-one in your resource group, then follow these steps.</span></span>

<span data-ttu-id="c0ec6-130">Si vous avez déployé votre cluster à l’aide du portail ou de l’un des modèles Resource Manager Service Fabric de la galerie de modèles, toutes les ressources utilisées par le cluster sont balisées avec les deux balises suivantes.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-130">If you deployed your cluster using the portal or using one of the Service Fabric Resource Manager templates from the template gallery, then all the resources that the cluster uses are tagged with the following two tags.</span></span> <span data-ttu-id="c0ec6-131">Vous pouvez les utiliser pour décider des ressources à supprimer.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-131">You can use them to decide which resources you want to delete.</span></span>

<span data-ttu-id="c0ec6-132">***Balise 1 :*** Clé = clusterName, Valeur = « nom du cluster »</span><span class="sxs-lookup"><span data-stu-id="c0ec6-132">***Tag#1:*** Key = clusterName, Value = 'name of the cluster'</span></span>

<span data-ttu-id="c0ec6-133">***Balise 2 :*** Clé = resourceName, Valeur = ServiceFabric</span><span class="sxs-lookup"><span data-stu-id="c0ec6-133">***Tag#2:*** Key = resourceName, Value = ServiceFabric</span></span>

### <a name="delete-specific-resources-in-the-azure-portal"></a><span data-ttu-id="c0ec6-134">Supprimer des ressources spécifiques dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="c0ec6-134">Delete specific resources in the Azure portal</span></span>
1. <span data-ttu-id="c0ec6-135">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c0ec6-135">Login to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c0ec6-136">Accédez au cluster Service Fabric que vous souhaitez supprimer.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-136">Navigate to the Service Fabric cluster you want to delete.</span></span>
3. <span data-ttu-id="c0ec6-137">Sélectionnez **Tous les paramètres** dans le panneau des éléments essentiels.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-137">Go to **All settings** on the essentials blade.</span></span>
4. <span data-ttu-id="c0ec6-138">Cliquez sur **Balises** sous **Gestion des ressources** dans le panneau des paramètres.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-138">Click on **Tags** under **Resource Management** in the settings blade.</span></span>
5. <span data-ttu-id="c0ec6-139">Cliquez sur l’une des **balises** dans le panneau des balises pour obtenir une liste de toutes les ressources associées à cette balise.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-139">Click on one of the **Tags** in the tags blade to get a list of all the resources with that tag.</span></span>
   
    ![Balises de ressource][ResourceTags]
6. <span data-ttu-id="c0ec6-141">Une fois affichée la liste des ressources balisées, cliquez sur chacune des ressources et supprimez-les.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-141">Once you have the list of tagged resources, click on each of the resources and delete them.</span></span>
   
    ![Ressources balisées][TaggedResources]

### <a name="delete-the-resources-using-azure-powershell"></a><span data-ttu-id="c0ec6-143">Supprimer les ressources à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0ec6-143">Delete the resources using Azure PowerShell</span></span>
<span data-ttu-id="c0ec6-144">Vous pouvez supprimer les ressources individuellement en exécutant les applets de commande Azure PowerShell suivantes.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-144">You can delete the resources one-by-one by running the following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="c0ec6-145">Vérifiez qu’Azure PowerShell 1.0 ou une version ultérieure est installé sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c0ec6-145">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="c0ec6-146">Si ce n’est déjà fait, suivez les étapes décrites dans [Installation et configuration d’Azure PowerShell](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="c0ec6-146">If you have not done this before, follow the steps outlined in [How to install and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="c0ec6-147">Ouvrez une fenêtre PowerShell et exécutez les applets de commande PS suivantes :</span><span class="sxs-lookup"><span data-stu-id="c0ec6-147">Open a PowerShell window and run the following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="c0ec6-148">Pour chacune des ressources à supprimer, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c0ec6-148">For each of the resources you want to delete, run the following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of the Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of the resource group>" -Force
```

<span data-ttu-id="c0ec6-149">Pour supprimer la ressource de cluster, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c0ec6-149">To delete the cluster resource, run the following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of the Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of the resource group>" -Force
```

## <a name="next-steps"></a><span data-ttu-id="c0ec6-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c0ec6-150">Next steps</span></span>
<span data-ttu-id="c0ec6-151">Lisez les documents suivants pour en savoir plus sur la mise à niveau d’un cluster et le partitionnement des services :</span><span class="sxs-lookup"><span data-stu-id="c0ec6-151">Read the following to also learn about upgrading a cluster and partitioning services:</span></span>

* [<span data-ttu-id="c0ec6-152">En savoir plus sur les mises à niveau de cluster</span><span class="sxs-lookup"><span data-stu-id="c0ec6-152">Learn about cluster upgrades</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="c0ec6-153">En savoir plus sur le partitionnement de services avec état pour une mise à l’échelle maximale</span><span class="sxs-lookup"><span data-stu-id="c0ec6-153">Learn about partitioning stateful services for maximum scale</span></span>](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
