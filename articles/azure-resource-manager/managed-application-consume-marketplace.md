---
title: "Utilisation des applications gérées de la Place de marché Azure | Microsoft Docs"
description: "Explique comment créer une application gérée Azure disponible via la Place de marché."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/11/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: baf456740bddd562391ed64d707f990c8921d710
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="consume-azure-managed-applications-in-the-marketplace"></a><span data-ttu-id="7d7b7-103">Utilisation des applications gérées de la Place de marché Azure</span><span class="sxs-lookup"><span data-stu-id="7d7b7-103">Consume Azure managed applications in the Marketplace</span></span>

<span data-ttu-id="7d7b7-104">Comme décrit dans l’article [Vue d’ensemble des applications gérées Azure](managed-application-overview.md), il existe deux scénarios dans l’expérience de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-104">As discussed in the [Managed Application overview](managed-application-overview.md) article, there are two scenarios in the end to end experience.</span></span> <span data-ttu-id="7d7b7-105">D’un côté, il y a l’éditeur ou le fournisseur désireux de créer une application gérée destinée à être utilisée par les clients.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-105">One is the publisher or vendor who wants to create a managed application for use by customers.</span></span> <span data-ttu-id="7d7b7-106">De l’autre, le client final ou l’utilisateur de l’application gérée.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-106">The second is the end customer or the consumer of the managed application.</span></span> <span data-ttu-id="7d7b7-107">Cet article concerne le second scénario.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-107">This article covers the second scenario.</span></span> <span data-ttu-id="7d7b7-108">Il décrit comment vous pouvez déployer une application gérée à partir de la Place de marché Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-108">It describes how you can deploy a managed application from the Microsoft Azure Marketplace.</span></span>

## <a name="create-from-the-marketplace"></a><span data-ttu-id="7d7b7-109">Créer une application à partir de la Place de marché</span><span class="sxs-lookup"><span data-stu-id="7d7b7-109">Create from the Marketplace</span></span>

<span data-ttu-id="7d7b7-110">Le déploiement d’une application gérée à partir de la Place de marché est similaire au déploiement de n’importe quel type de ressources de ce Marketplace.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-110">Deploying a managed application from the Marketplace is similar to deploying any type of resources from the Marketplace.</span></span> 

<span data-ttu-id="7d7b7-111">Dans le portail, sélectionnez **+ Nouveau** et recherchez le type de solution à déployer.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-111">In the portal, select **+ New** and search for the type of solution to deploy.</span></span> <span data-ttu-id="7d7b7-112">Parmi les options disponibles, sélectionnez celle dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-112">From the available options, select the one you need.</span></span>

![rechercher des solutions](./media/managed-application-consume-marketplace/search-apps.png)

<span data-ttu-id="7d7b7-114">Passez en revue le résumé de l’application, puis sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-114">Review the summary of the application, and select **Create**.</span></span>

![créer une application gérée](./media/managed-application-consume-marketplace/create-marketplace-managed-app.png)

<span data-ttu-id="7d7b7-116">Comme avec toute autre solution, vous devez définir les valeurs de certains champs.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-116">Like any other solution, you are presented with fields to provide values for.</span></span> <span data-ttu-id="7d7b7-117">Ces champs varient selon le type d’application gérée que vous créez.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-117">These fields vary by the type of managed application you create.</span></span> 

## <a name="view-support-information"></a><span data-ttu-id="7d7b7-118">Afficher les informations de support</span><span class="sxs-lookup"><span data-stu-id="7d7b7-118">View support information</span></span>

<span data-ttu-id="7d7b7-119">Après le déploiement de votre application gérée, affichez les informations de support associées.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-119">After your managed application has deployed, view the support information for the application.</span></span> <span data-ttu-id="7d7b7-120">Ces informations s’affichent dans le panneau de l’application gérée.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-120">In the managed application blade, the support information is listed.</span></span>

![support](./media/managed-application-consume-marketplace/support.png)

## <a name="view-publisher-permissions"></a><span data-ttu-id="7d7b7-122">Afficher les autorisations d’éditeur</span><span class="sxs-lookup"><span data-stu-id="7d7b7-122">View publisher permissions</span></span>

<span data-ttu-id="7d7b7-123">Le fournisseur qui gère votre application a accès à vos ressources.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-123">The vendor that manages your application is granted access to your resources.</span></span> <span data-ttu-id="7d7b7-124">Pour afficher ces autorisations, sélectionnez **Autorisations**.</span><span class="sxs-lookup"><span data-stu-id="7d7b7-124">To see those permissions, select **Authorizations**.</span></span>

![autorisations](./media/managed-application-consume-marketplace/authorizations.png)

## <a name="next-steps"></a><span data-ttu-id="7d7b7-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7d7b7-126">Next steps</span></span>

* <span data-ttu-id="7d7b7-127">Pour plus d’informations sur la publication d’une application gérée sur la Place de marché, consultez l’article [Applications gérées sur la Place de marché Azure](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="7d7b7-127">For information about publishing a managed application in the Marketplace, see [Azure Managed Applications in Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="7d7b7-128">Pour publier des applications gérées uniquement disponibles pour les utilisateurs de votre organisation, consultez la page [Créer et publier une application gérée de catalogue de services](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="7d7b7-128">To publish managed applications that are only available to users in your organization, see [Create and publish Service Catalog Managed Application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="7d7b7-129">Pour utiliser des applications gérées uniquement disponibles pour les utilisateurs de votre organisation, consultez la page [Utiliser une application gérée du catalogue de services](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="7d7b7-129">To consume managed applications that are only available to users in your organization, see [Consume a Service Catalog Managed Application](managed-application-consumption.md).</span></span>