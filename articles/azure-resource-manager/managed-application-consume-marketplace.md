---
title: "aaaConsume Azure des applications gérés dans marketplace | Documents Microsoft"
description: "Explique toocreate une Application Azure géré qui est disponible via hello Marketplace."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/11/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 9ae6e11a3f63eb58a9f3199364b5606a7afe5618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-azure-managed-applications-in-hello-marketplace"></a><span data-ttu-id="bd535-103">Utiliser Azure géré applications Bonjour Marketplace</span><span class="sxs-lookup"><span data-stu-id="bd535-103">Consume Azure managed applications in hello Marketplace</span></span>

<span data-ttu-id="bd535-104">Comme indiqué dans hello [vue d’ensemble de l’Application managée](managed-application-overview.md) l’article, il existe deux scénarios dans expérience tooend hello.</span><span class="sxs-lookup"><span data-stu-id="bd535-104">As discussed in hello [Managed Application overview](managed-application-overview.md) article, there are two scenarios in hello end tooend experience.</span></span> <span data-ttu-id="bd535-105">Un est serveur de publication hello ou un fournisseur qui souhaite toocreate une application managée pour une utilisation par les clients.</span><span class="sxs-lookup"><span data-stu-id="bd535-105">One is hello publisher or vendor who wants toocreate a managed application for use by customers.</span></span> <span data-ttu-id="bd535-106">Hello est ensuite client final de hello ou consommateur hello de l’application hello géré.</span><span class="sxs-lookup"><span data-stu-id="bd535-106">hello second is hello end customer or hello consumer of hello managed application.</span></span> <span data-ttu-id="bd535-107">Cet article décrit le deuxième scénario de hello.</span><span class="sxs-lookup"><span data-stu-id="bd535-107">This article covers hello second scenario.</span></span> <span data-ttu-id="bd535-108">Il décrit comment vous pouvez déployer une application managée à partir de hello Microsoft Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="bd535-108">It describes how you can deploy a managed application from hello Microsoft Azure Marketplace.</span></span>

## <a name="create-from-hello-marketplace"></a><span data-ttu-id="bd535-109">Créer à partir de hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="bd535-109">Create from hello Marketplace</span></span>

<span data-ttu-id="bd535-110">Le déploiement d’une application managée à partir de hello Marketplace est similaire toodeploying tous les types de ressources à partir de hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="bd535-110">Deploying a managed application from hello Marketplace is similar toodeploying any type of resources from hello Marketplace.</span></span> 

<span data-ttu-id="bd535-111">Dans le portail de hello, sélectionnez **+ nouveau** et recherche de type hello de solution toodeploy.</span><span class="sxs-lookup"><span data-stu-id="bd535-111">In hello portal, select **+ New** and search for hello type of solution toodeploy.</span></span> <span data-ttu-id="bd535-112">Parmi les options disponibles hello, sélectionnez hello, vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="bd535-112">From hello available options, select hello one you need.</span></span>

![rechercher des solutions](./media/managed-application-consume-marketplace/search-apps.png)

<span data-ttu-id="bd535-114">Passez en revue le résumé hello de l’application hello, puis sélectionnez **créer**.</span><span class="sxs-lookup"><span data-stu-id="bd535-114">Review hello summary of hello application, and select **Create**.</span></span>

![créer une application gérée](./media/managed-application-consume-marketplace/create-marketplace-managed-app.png)

<span data-ttu-id="bd535-116">Comme toute autre solution, vous sont présentés avec les valeurs des champs tooprovide pour.</span><span class="sxs-lookup"><span data-stu-id="bd535-116">Like any other solution, you are presented with fields tooprovide values for.</span></span> <span data-ttu-id="bd535-117">Ces champs varient selon le type de hello d’application managée que vous créez.</span><span class="sxs-lookup"><span data-stu-id="bd535-117">These fields vary by hello type of managed application you create.</span></span> 

## <a name="view-support-information"></a><span data-ttu-id="bd535-118">Afficher les informations de support</span><span class="sxs-lookup"><span data-stu-id="bd535-118">View support information</span></span>

<span data-ttu-id="bd535-119">Une fois que votre application managée a été déployé, afficher des informations de prise en charge de hello pour une application hello.</span><span class="sxs-lookup"><span data-stu-id="bd535-119">After your managed application has deployed, view hello support information for hello application.</span></span> <span data-ttu-id="bd535-120">Dans le panneau des applications gérés hello, informations de prise en charge hello sont répertoriées.</span><span class="sxs-lookup"><span data-stu-id="bd535-120">In hello managed application blade, hello support information is listed.</span></span>

![support](./media/managed-application-consume-marketplace/support.png)

## <a name="view-publisher-permissions"></a><span data-ttu-id="bd535-122">Afficher les autorisations d’éditeur</span><span class="sxs-lookup"><span data-stu-id="bd535-122">View publisher permissions</span></span>

<span data-ttu-id="bd535-123">fournisseur Hello qui gère votre application est accordé tooyour d’accéder aux ressources.</span><span class="sxs-lookup"><span data-stu-id="bd535-123">hello vendor that manages your application is granted access tooyour resources.</span></span> <span data-ttu-id="bd535-124">toosee ces autorisations, sélectionnez **autorisations**.</span><span class="sxs-lookup"><span data-stu-id="bd535-124">toosee those permissions, select **Authorizations**.</span></span>

![autorisations](./media/managed-application-consume-marketplace/authorizations.png)

## <a name="next-steps"></a><span data-ttu-id="bd535-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bd535-126">Next steps</span></span>

* <span data-ttu-id="bd535-127">Pour plus d’informations sur la publication d’une application managée dans hello Marketplace, consultez [Azure des Applications gérées dans Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="bd535-127">For information about publishing a managed application in hello Marketplace, see [Azure Managed Applications in Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="bd535-128">toopublish applications managées qui sont uniquement disponibles toousers dans votre organisation, consultez [créer et publier l’Application de Service de catalogue gérée](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="bd535-128">toopublish managed applications that are only available toousers in your organization, see [Create and publish Service Catalog Managed Application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="bd535-129">tooconsume applications managées qui sont uniquement disponibles toousers dans votre organisation, consultez [consommer une Application managée de catalogue Service](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="bd535-129">tooconsume managed applications that are only available toousers in your organization, see [Consume a Service Catalog Managed Application](managed-application-consumption.md).</span></span>
