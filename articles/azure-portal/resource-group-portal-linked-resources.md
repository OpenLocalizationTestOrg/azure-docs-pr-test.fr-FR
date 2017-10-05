---
title: "Ressources associées et liées dans la Galerie de vignettes"
description: "Apprenez en quoi consistent les ressources associées et liées qui sont affichées dans la Galerie de vignettes du portail Azure en version préliminaire."
services: azure-portal
documentationcenter: 
author: adamabdelhamed
manager: wpickett
editor: 
ms.assetid: dba96d29-f518-49c8-bfd2-f14cecb44cbf
ms.service: azure-portal
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2015
ms.author: adamab
ms.openlocfilehash: efa7bce26c2c4c153b083e0e34d689a11d27dd16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="related-and-linked-resources-in-the-tile-gallery"></a><span data-ttu-id="7163a-103">Ressources associées et liées dans la Galerie de vignettes</span><span class="sxs-lookup"><span data-stu-id="7163a-103">Related and linked resources in the tile gallery</span></span>
<span data-ttu-id="7163a-104">La Galerie de vignettes vous permet de rechercher des vignettes pour une ressource spécifique et de les faire glisser jusqu’à votre panneau actif.</span><span class="sxs-lookup"><span data-stu-id="7163a-104">The tile gallery enables you to find tiles for a particular resource and drag them onto your current blade.</span></span> <span data-ttu-id="7163a-105">À l’aide de la Galerie de vignettes, vous pouvez créer des vues de gestion portant sur les ressources.</span><span class="sxs-lookup"><span data-stu-id="7163a-105">Using the tile gallery, you can create management views that span resources.</span></span> <span data-ttu-id="7163a-106">Pour n’importe quelle ressource donnée, les ressources associées englobent toutes les ressources de son groupe de ressources, ainsi que toutes les ressources qui établissent des liens à destination ou en provenance de la ressource.</span><span class="sxs-lookup"><span data-stu-id="7163a-106">For any specified resource, the related resources include all the resources in its resource group, and any resources that link to or from the resource.</span></span>

## <a name="linked-resources-in-resource-manager"></a><span data-ttu-id="7163a-107">Ressources liées dans Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7163a-107">Linked resources in Resource Manager</span></span>
<span data-ttu-id="7163a-108">La liaison est une fonctionnalité de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7163a-108">Linking is a feature of the Resource Manager.</span></span>  <span data-ttu-id="7163a-109">Elle vous permet de déclarer des relations entre les ressources, même si ces dernières n’appartiennent pas au même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="7163a-109">It enables you to declare relationships between resources even if they do not reside in the same resource group.</span></span> <span data-ttu-id="7163a-110">La liaison n’a aucun impact sur le moment de l’exécution de vos ressources, sur la facturation, ni sur l’accès en fonction du rôle.</span><span class="sxs-lookup"><span data-stu-id="7163a-110">Linking has no impact on the runtime of your resources, no impact on billing, and no impact on role-based access.</span></span>  <span data-ttu-id="7163a-111">Il s’agit simplement d’un mécanisme qui vous permet de représenter les relations afin que les outils comme la Galerie de vignettes puissent offrir une expérience de gestion enrichie.</span><span class="sxs-lookup"><span data-stu-id="7163a-111">It's simply a mechanism you can use to represent relationships so that tools like the tile gallery can provide a rich management experience.</span></span>  <span data-ttu-id="7163a-112">Vos outils peuvent inspecter les liens à l’aide de l’API de liens et fournir également des expériences de gestion des relations personnalisées.</span><span class="sxs-lookup"><span data-stu-id="7163a-112">Your tools can inspect the links using the links API and provide custom relationship management experiences as well.</span></span> 

## <a name="how-do-i-link-my-resources"></a><span data-ttu-id="7163a-113">Comment lier mes ressources ?</span><span class="sxs-lookup"><span data-stu-id="7163a-113">How do I link my resources?</span></span>
<span data-ttu-id="7163a-114">Lorsque vous créez des ressources par le biais du portail ou en déployant un modèle par l’intermédiaire d’Azure PowerShell ou de l’interface de ligne de commande Azure, des liens sont automatiquement créés pour certaines ressources dépendantes.</span><span class="sxs-lookup"><span data-stu-id="7163a-114">When you create resources through the portal or by deploying a template through Azure PowerShell or Azure CLI, links are automatically created for some dependent resources.</span></span> <span data-ttu-id="7163a-115">Vous pouvez également lier des ressources par programme à l’aide de [l’API REST Ressources liées](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="7163a-115">You can also programmatically link resources by using the [Linked Resources REST API](/rest/api/resources/resourcelinks).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7163a-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7163a-116">Next steps</span></span>
* <span data-ttu-id="7163a-117">Pour plus d’informations sur l’écriture de modèles Resource Manager, consultez la page [Création de modèles](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7163a-117">If you need an introduction to writing Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="7163a-118">Pour plus d’informations sur l’utilisation des groupes de ressources par le biais du portail, consultez la page [Utiliser le Portail Azure pour gérer vos ressources Azure](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7163a-118">To understand more about working with resource groups through the portal, see [Using the Azure portal to manage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span></span>

