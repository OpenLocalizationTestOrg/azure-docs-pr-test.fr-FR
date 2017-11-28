---
title: "aaaRelated et les ressources liées Bonjour vignette de la galerie"
description: "En savoir plus sur les ressources associées et liés sont affichent dans la galerie de vignette hello du portail Azure en version préliminaire de hello."
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
ms.openlocfilehash: c8f99be8e23dc9641ec3cd3169604b33a4b049f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="related-and-linked-resources-in-hello-tile-gallery"></a><span data-ttu-id="ff078-103">Ressources connexes et liés dans la galerie de vignette hello</span><span class="sxs-lookup"><span data-stu-id="ff078-103">Related and linked resources in hello tile gallery</span></span>
<span data-ttu-id="ff078-104">Galerie de vignette Hello vous permet de vignettes toofind pour une ressource particulière et faites-les glisser vers votre panneau actuel.</span><span class="sxs-lookup"><span data-stu-id="ff078-104">hello tile gallery enables you toofind tiles for a particular resource and drag them onto your current blade.</span></span> <span data-ttu-id="ff078-105">À l’aide de la galerie de vignette hello, vous pouvez créer des vues de gestion qui s’étendent sur des ressources.</span><span class="sxs-lookup"><span data-stu-id="ff078-105">Using hello tile gallery, you can create management views that span resources.</span></span> <span data-ttu-id="ff078-106">Pour n’importe quelle ressource spécifiée, hello liée ressources incluent toutes les ressources de hello dans son groupe de ressources et toutes les ressources qui sont liées tooor à partir de la ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="ff078-106">For any specified resource, hello related resources include all hello resources in its resource group, and any resources that link tooor from hello resource.</span></span>

## <a name="linked-resources-in-resource-manager"></a><span data-ttu-id="ff078-107">Ressources liées dans Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ff078-107">Linked resources in Resource Manager</span></span>
<span data-ttu-id="ff078-108">La liaison est une fonctionnalité du Gestionnaire de ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="ff078-108">Linking is a feature of hello Resource Manager.</span></span>  <span data-ttu-id="ff078-109">Il vous permet de toodeclare les relations entre les ressources même si elles ne trouvent pas dans hello même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="ff078-109">It enables you toodeclare relationships between resources even if they do not reside in hello same resource group.</span></span> <span data-ttu-id="ff078-110">Liaison n’a aucun impact sur le runtime hello de vos ressources, aucun impact sur la facturation et aucun impact sur l’accès en fonction du rôle.</span><span class="sxs-lookup"><span data-stu-id="ff078-110">Linking has no impact on hello runtime of your resources, no impact on billing, and no impact on role-based access.</span></span>  <span data-ttu-id="ff078-111">Il est simplement un mécanisme que vous pouvez utiliser les relations toorepresent afin que les outils tels que la galerie de vignette hello peut fournir une gestion riche expérience.</span><span class="sxs-lookup"><span data-stu-id="ff078-111">It's simply a mechanism you can use toorepresent relationships so that tools like hello tile gallery can provide a rich management experience.</span></span>  <span data-ttu-id="ff078-112">Vos outils peuvent inspecter les liens de hello à l’aide de liens de hello API et fournissent également des expériences de gestion des relations personnalisées.</span><span class="sxs-lookup"><span data-stu-id="ff078-112">Your tools can inspect hello links using hello links API and provide custom relationship management experiences as well.</span></span> 

## <a name="how-do-i-link-my-resources"></a><span data-ttu-id="ff078-113">Comment lier mes ressources ?</span><span class="sxs-lookup"><span data-stu-id="ff078-113">How do I link my resources?</span></span>
<span data-ttu-id="ff078-114">Lorsque vous créez des ressources hello portal ou en déployant un modèle via Azure PowerShell ou CLI d’Azure, des liens sont créés automatiquement pour certaines des ressources dépendantes.</span><span class="sxs-lookup"><span data-stu-id="ff078-114">When you create resources through hello portal or by deploying a template through Azure PowerShell or Azure CLI, links are automatically created for some dependent resources.</span></span> <span data-ttu-id="ff078-115">Vous pouvez également programmer lier des ressources à l’aide de hello [lié API REST de ressources](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="ff078-115">You can also programmatically link resources by using hello [Linked Resources REST API](/rest/api/resources/resourcelinks).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff078-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ff078-116">Next steps</span></span>
* <span data-ttu-id="ff078-117">Si vous avez besoin d’une présentation toowriting Gestionnaire de ressources des modèles, consultez [création de modèles](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ff078-117">If you need an introduction toowriting Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="ff078-118">toounderstand en savoir plus sur l’utilisation des groupes de ressources via le portail de hello, consultez [Using hello toomanage portail Azure vos ressources Azure](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ff078-118">toounderstand more about working with resource groups through hello portal, see [Using hello Azure portal toomanage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span></span>

