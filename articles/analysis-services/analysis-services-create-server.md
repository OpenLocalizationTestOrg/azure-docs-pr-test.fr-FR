---
title: "Création d’un serveur Analysis Services dans Azure | Microsoft Docs"
description: "Apprenez à créer une instance de serveur Analysis Services dans Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 7f560216-8a9a-4d06-852e-48cf24deab19
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 95b367e7cd74405088190c1fe19cf92990759d90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a><span data-ttu-id="7bb2a-103">Création d’un serveur Azure Analysis Services dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="7bb2a-103">Create an Azure Analysis Services server in Azure portal</span></span>
<span data-ttu-id="7bb2a-104">Cet article vous guide lors du processus de création d’une ressource de serveur Analysis Services dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="7bb2a-104">This article walks you through creating an Analysis Services server resource in your Azure subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7bb2a-105">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="7bb2a-105">Before you begin</span></span>
<span data-ttu-id="7bb2a-106">Pour effectuer ce démarrage rapide, les éléments suivants sont requis :</span><span class="sxs-lookup"><span data-stu-id="7bb2a-106">To complete this quickstart, you need:</span></span>

* <span data-ttu-id="7bb2a-107">**Abonnement Azure** : visitez [version d’évaluation gratuite d’Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) pour créer un compte.</span><span class="sxs-lookup"><span data-stu-id="7bb2a-107">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) to create an account.</span></span>
* <span data-ttu-id="7bb2a-108">**Azure Active Directory** : votre abonnement doit être associé à un locataire Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7bb2a-108">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant.</span></span> <span data-ttu-id="7bb2a-109">Vous devez également être connecté à Azure avec un compte dans cette instance d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7bb2a-109">And, you need to be signed in to Azure with an account in that Azure Active Directory.</span></span> <span data-ttu-id="7bb2a-110">Les comptes Microsoft ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7bb2a-110">Microsoft accounts are not supported.</span></span> <span data-ttu-id="7bb2a-111">Pour en savoir plus, consultez [Authentification et autorisations utilisateur](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="7bb2a-111">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>
* <span data-ttu-id="7bb2a-112">**Groupe de ressources** : utilisez un groupe de ressources existant ou [créez-en un](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7bb2a-112">**Resource group**: Use a resource group you already have or [create a new one](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7bb2a-113">La création d’un serveur peut donner lieu à un nouveau service facturable.</span><span class="sxs-lookup"><span data-stu-id="7bb2a-113">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="7bb2a-114">Pour en savoir plus, consultez [Tarification d’Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="7bb2a-114">To learn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
> 
> 

## <a name="to-create-a-server-in-azure-portal"></a><span data-ttu-id="7bb2a-115">Pour créer un serveur dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="7bb2a-115">To create a server in Azure portal</span></span>
1. <span data-ttu-id="7bb2a-116">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7bb2a-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="7bb2a-117">Cliquez sur **+ Nouveau** > **Données + analyse** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="7bb2a-117">Click **+ New** > **Data + analytics** > **Analysis Services**.</span></span>
3. <span data-ttu-id="7bb2a-118">Dans le panneau **Analysis Services**, renseignez les champs requis, puis appuyez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="7bb2a-118">In the **Analysis Services** blade, fill in the required fields, and then press **Create**.</span></span>
   
    ![Créer un serveur](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * <span data-ttu-id="7bb2a-120">**Nom du serveur** : tapez un nom unique utilisé pour se référencer au serveur.</span><span class="sxs-lookup"><span data-stu-id="7bb2a-120">**Server name**: Type a unique name used to reference the server.</span></span>
   * <span data-ttu-id="7bb2a-121">**Abonnement** : sélectionnez l’abonnement de facturation de ce serveur.</span><span class="sxs-lookup"><span data-stu-id="7bb2a-121">**Subscription**: Select the subscription this server bills to.</span></span>
   * <span data-ttu-id="7bb2a-122">**Groupe de ressources** : ces conteneurs sont conçus pour vous aider à gérer un ensemble de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="7bb2a-122">**Resource group**: These containers are designed to help you manage a collection of Azure resources.</span></span> <span data-ttu-id="7bb2a-123">Pour en savoir plus, consultez les [groupes de ressources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7bb2a-123">To learn more, see [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="7bb2a-124">**Emplacement** : cet emplacement du centre de données Azure héberge le serveur.</span><span class="sxs-lookup"><span data-stu-id="7bb2a-124">**Location**: This Azure datacenter location hosts the server.</span></span> <span data-ttu-id="7bb2a-125">Choisissez l’emplacement le plus proche de votre plus grande base d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="7bb2a-125">Choose a location nearest your largest user base.</span></span>
   * <span data-ttu-id="7bb2a-126">**Niveau de tarification** : sélectionnez un niveau de tarification.</span><span class="sxs-lookup"><span data-stu-id="7bb2a-126">**Pricing tier**: Select a pricing tier.</span></span> <span data-ttu-id="7bb2a-127">Les modèles tabulaires sont pris en charge jusqu’à 400 Go.</span><span class="sxs-lookup"><span data-stu-id="7bb2a-127">Tabular models up to 400 GB are supported.</span></span> <span data-ttu-id="7bb2a-128">Pour en savoir plus, voir [Tarification d’Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="7bb2a-128">To learn more, see [Azure Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
4. <span data-ttu-id="7bb2a-129">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="7bb2a-129">Click **Create**.</span></span>

<span data-ttu-id="7bb2a-130">La création prend généralement moins d’une minute, souvent quelques secondes seulement.</span><span class="sxs-lookup"><span data-stu-id="7bb2a-130">Create usually takes under a minute; often just a few seconds.</span></span> <span data-ttu-id="7bb2a-131">Si vous avez sélectionné **Add to Portal** (Ajouter au portail), accédez au portail pour voir votre nouveau serveur.</span><span class="sxs-lookup"><span data-stu-id="7bb2a-131">If you selected **Add to Portal**, navigate to your portal to see your new server.</span></span> <span data-ttu-id="7bb2a-132">Ou, accédez à **More services (Plus de services)** > **Analysis Services** pour voir si votre serveur est prêt.</span><span class="sxs-lookup"><span data-stu-id="7bb2a-132">Or, navigate to **More services** > **Analysis Services** to see if your server is ready.</span></span>

 ![Tableau de bord](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a><span data-ttu-id="7bb2a-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7bb2a-134">Next steps</span></span>
<span data-ttu-id="7bb2a-135">Une fois que vous avez créé votre serveur, vous pouvez y [déployer un modèle](analysis-services-deploy.md) via SSDT ou SSMS.</span><span class="sxs-lookup"><span data-stu-id="7bb2a-135">Once you've created your server, you can [deploy a model](analysis-services-deploy.md) to it by using SSDT or with SSMS.</span></span>

<span data-ttu-id="7bb2a-136">Si un modèle déployé sur votre serveur se connecte à des sources de données locales, vous devez installer une [passerelle de données locale](analysis-services-gateway.md) sur un ordinateur de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="7bb2a-136">If a model you deploy to your server connects to on-premises data sources, you need to install an [On-premises data gateway](analysis-services-gateway.md) on a computer in your network.</span></span>

