---
title: "aaaPublish un élément de marketplace personnalisé dans la pile de Azure (opérateur de cloud) | Documents Microsoft"
description: "Comme un opérateur cloud, découvrez comment toopublish un marketplace personnalisé d’élément dans la pile de Azure."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 60871cbb-eed2-433c-a76d-d605c7aec06c
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: erikje
ms.openlocfilehash: e33e1c6574d43ada1c1c85bf77df7d0d191116aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-azure-stack-marketplace-overview"></a><span data-ttu-id="9fb5b-103">vue d’ensemble de la pile de Azure Marketplace Hello</span><span class="sxs-lookup"><span data-stu-id="9fb5b-103">hello Azure Stack Marketplace overview</span></span>
<span data-ttu-id="9fb5b-104">Hello Marketplace est une collection de services, applications et ressources personnalisés pour la pile de Azure, telles que les réseaux, les ordinateurs virtuels, stockage et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="9fb5b-104">hello Marketplace is a collection of services, applications, and resources customized for Azure Stack, like networks, virtual machines, storage, and so on.</span></span> <span data-ttu-id="9fb5b-105">Les utilisateurs reviennent ici toocreate nouvelles ressources et déploiement de nouvelles applications.</span><span class="sxs-lookup"><span data-stu-id="9fb5b-105">Users come here toocreate new resources and deploy new applications.</span></span> <span data-ttu-id="9fb5b-106">Considérez-le comme un catalogue d’achat où les utilisateurs peuvent parcourir et choisissez hello ils les éléments que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="9fb5b-106">Think of it as a shopping catalog where users can browse and choose hello items they want toouse.</span></span> <span data-ttu-id="9fb5b-107">toouse un élément de Marketplace, les utilisateurs doivent s’abonner offre tooan qui accorde l’élément toohello d’accès.</span><span class="sxs-lookup"><span data-stu-id="9fb5b-107">toouse a Marketplace item, users must subscribe tooan offer that grants them access toohello item.</span></span>

<span data-ttu-id="9fb5b-108">Comme un opérateur cloud, vous décidez quels tooadd éléments (publier) toohello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="9fb5b-108">As a cloud operator, you decide which items tooadd (publish) toohello Marketplace.</span></span> <span data-ttu-id="9fb5b-109">Vous pouvez publier des éléments tels que des bases de données, App Services, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="9fb5b-109">You can publish things like databases, App Services, and so on.</span></span> <span data-ttu-id="9fb5b-110">Cela les rend visible tooall vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9fb5b-110">This makes them visible tooall your users.</span></span> <span data-ttu-id="9fb5b-111">Vous pouvez publier des éléments personnalisés que vous créez.</span><span class="sxs-lookup"><span data-stu-id="9fb5b-111">You can publish custom items that you create.</span></span> <span data-ttu-id="9fb5b-112">Vous pouvez également publier des éléments à partir d’une [liste croissante d’éléments de Place de Marché Azure](azure-stack-marketplace-azure-items.md).</span><span class="sxs-lookup"><span data-stu-id="9fb5b-112">You can also publish items from a growing [list of Azure Marketplace items](azure-stack-marketplace-azure-items.md).</span></span> <span data-ttu-id="9fb5b-113">Lorsque vous publiez un toohello élément Marketplace, les utilisateurs peuvent le voir dans les cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="9fb5b-113">When you publish an item toohello Marketplace, users can see it within five minutes.</span></span>

<span data-ttu-id="9fb5b-114">tooopen hello Marketplace, cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="9fb5b-114">tooopen hello Marketplace, click **New**.</span></span>

![](media/azure-stack-publish-custom-marketplace-item/image1.png)

## <a name="marketplace-items"></a><span data-ttu-id="9fb5b-115">Éléments du Marketplace</span><span class="sxs-lookup"><span data-stu-id="9fb5b-115">Marketplace items</span></span>
<span data-ttu-id="9fb5b-116">Un élément Place de Marché Azure Stack est un service, une application ou une ressource que vos utilisateurs peuvent télécharger et utiliser.</span><span class="sxs-lookup"><span data-stu-id="9fb5b-116">An Azure Stack Marketplace item is a service, application, or resource that your users can download and use.</span></span> <span data-ttu-id="9fb5b-117">Tous les éléments d’Azure Marketplace de pile est visible tooall vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9fb5b-117">All Azure Stack Marketplace items are visible tooall your users.</span></span>

<span data-ttu-id="9fb5b-118">Chaque élément du Marketplace comporte :</span><span class="sxs-lookup"><span data-stu-id="9fb5b-118">Every Marketplace item has:</span></span>

* <span data-ttu-id="9fb5b-119">Modèle Azure Resource Manager pour l’approvisionnement de la ressource</span><span class="sxs-lookup"><span data-stu-id="9fb5b-119">An Azure Resource Manager template for resource provisioning</span></span>
* <span data-ttu-id="9fb5b-120">Les métadonnées telles que les chaînes, les icônes et autres supports marketing</span><span class="sxs-lookup"><span data-stu-id="9fb5b-120">Metadata, like strings, icons, and other marketing collateral</span></span>
* <span data-ttu-id="9fb5b-121">Mise en forme élément hello toodisplay d’informations dans le portail de hello</span><span class="sxs-lookup"><span data-stu-id="9fb5b-121">Formatting information toodisplay hello item in hello portal</span></span>

<span data-ttu-id="9fb5b-122">Chaque élément publié toohello Marketplace utilise un Package de la galerie Azure (azpkg) du format appelée hello.</span><span class="sxs-lookup"><span data-stu-id="9fb5b-122">Every item published toohello Marketplace uses a format called hello Azure Gallery Package (azpkg).</span></span> <span data-ttu-id="9fb5b-123">Ajouter des ressources de déploiement ou d’exécution (par exemple, du code, les fichiers zip avec des logiciels ou images de machine virtuelle) tooAzure de pile séparément, pas dans le cadre de hello élément du Marketplace.</span><span class="sxs-lookup"><span data-stu-id="9fb5b-123">Add deployment or runtime resources (like code, zip files with software, or virtual machine images) tooAzure Stack separately, not as part of hello Marketplace Item.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9fb5b-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9fb5b-124">Next steps</span></span>
[<span data-ttu-id="9fb5b-125">Créer et publier un élément de Place de Marché</span><span class="sxs-lookup"><span data-stu-id="9fb5b-125">Create and publish a marketplace item</span></span>](azure-stack-create-and-publish-marketplace-item.md)

