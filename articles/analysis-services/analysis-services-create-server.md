---
title: aaaCreate un serveur Analysis Services dans Azure | Documents Microsoft
description: "Découvrez comment toocreate un serveur Analysis Services instance dans Azure."
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
ms.openlocfilehash: 3668f659039f79f3dd71498d1066e8682bf33228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a><span data-ttu-id="9c5f0-103">Création d’un serveur Azure Analysis Services dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="9c5f0-103">Create an Azure Analysis Services server in Azure portal</span></span>
<span data-ttu-id="9c5f0-104">Cet article vous guide lors du processus de création d’une ressource de serveur Analysis Services dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="9c5f0-104">This article walks you through creating an Analysis Services server resource in your Azure subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9c5f0-105">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="9c5f0-105">Before you begin</span></span>
<span data-ttu-id="9c5f0-106">toocomplete ce démarrage rapide, vous devez :</span><span class="sxs-lookup"><span data-stu-id="9c5f0-106">toocomplete this quickstart, you need:</span></span>

* <span data-ttu-id="9c5f0-107">**Abonnement Azure**: visitez [d’évaluation gratuite Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate un compte.</span><span class="sxs-lookup"><span data-stu-id="9c5f0-107">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate an account.</span></span>
* <span data-ttu-id="9c5f0-108">**Azure Active Directory** : votre abonnement doit être associé à un locataire Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9c5f0-108">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant.</span></span> <span data-ttu-id="9c5f0-109">Et bien, vous devez toobe tooAzure connecté avec un compte dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9c5f0-109">And, you need toobe signed in tooAzure with an account in that Azure Active Directory.</span></span> <span data-ttu-id="9c5f0-110">Les comptes Microsoft ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="9c5f0-110">Microsoft accounts are not supported.</span></span> <span data-ttu-id="9c5f0-111">toolearn, voir [d’authentification et les autorisations utilisateur](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="9c5f0-111">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>
* <span data-ttu-id="9c5f0-112">**Groupe de ressources** : utilisez un groupe de ressources existant ou [créez-en un](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9c5f0-112">**Resource group**: Use a resource group you already have or [create a new one](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9c5f0-113">La création d’un serveur peut donner lieu à un nouveau service facturable.</span><span class="sxs-lookup"><span data-stu-id="9c5f0-113">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="9c5f0-114">toolearn, voir [Analysis Services tarification](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="9c5f0-114">toolearn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
> 
> 

## <a name="toocreate-a-server-in-azure-portal"></a><span data-ttu-id="9c5f0-115">toocreate un serveur dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="9c5f0-115">toocreate a server in Azure portal</span></span>
1. <span data-ttu-id="9c5f0-116">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9c5f0-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="9c5f0-117">Cliquez sur **+ Nouveau** > **Données + analyse** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="9c5f0-117">Click **+ New** > **Data + analytics** > **Analysis Services**.</span></span>
3. <span data-ttu-id="9c5f0-118">Bonjour **Analysis Services** panneau, renseignez les champs hello requis, puis appuyez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="9c5f0-118">In hello **Analysis Services** blade, fill in hello required fields, and then press **Create**.</span></span>
   
    ![Créer un serveur](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * <span data-ttu-id="9c5f0-120">**Nom du serveur**: Type d’un serveur de hello tooreference nom unique utilisé.</span><span class="sxs-lookup"><span data-stu-id="9c5f0-120">**Server name**: Type a unique name used tooreference hello server.</span></span>
   * <span data-ttu-id="9c5f0-121">**Abonnement**: sélectionnez l’abonnement hello facture de ce serveur à.</span><span class="sxs-lookup"><span data-stu-id="9c5f0-121">**Subscription**: Select hello subscription this server bills to.</span></span>
   * <span data-ttu-id="9c5f0-122">**Groupe de ressources**: ces conteneurs sont conçu toohelp vous gérez une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="9c5f0-122">**Resource group**: These containers are designed toohelp you manage a collection of Azure resources.</span></span> <span data-ttu-id="9c5f0-123">toolearn, voir [groupes de ressources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9c5f0-123">toolearn more, see [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="9c5f0-124">**Emplacement**: ordinateurs hôtes emplacement de centre de données Azure ce hello serveur.</span><span class="sxs-lookup"><span data-stu-id="9c5f0-124">**Location**: This Azure datacenter location hosts hello server.</span></span> <span data-ttu-id="9c5f0-125">Choisissez l’emplacement le plus proche de votre plus grande base d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9c5f0-125">Choose a location nearest your largest user base.</span></span>
   * <span data-ttu-id="9c5f0-126">**Niveau de tarification** : sélectionnez un niveau de tarification.</span><span class="sxs-lookup"><span data-stu-id="9c5f0-126">**Pricing tier**: Select a pricing tier.</span></span> <span data-ttu-id="9c5f0-127">Les modèles tabulaires des too400 Go sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="9c5f0-127">Tabular models up too400 GB are supported.</span></span> <span data-ttu-id="9c5f0-128">toolearn, voir [tarification Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="9c5f0-128">toolearn more, see [Azure Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
4. <span data-ttu-id="9c5f0-129">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="9c5f0-129">Click **Create**.</span></span>

<span data-ttu-id="9c5f0-130">La création prend généralement moins d’une minute, souvent quelques secondes seulement.</span><span class="sxs-lookup"><span data-stu-id="9c5f0-130">Create usually takes under a minute; often just a few seconds.</span></span> <span data-ttu-id="9c5f0-131">Si vous avez sélectionné **ajouter tooPortal**, accédez à toosee de portail tooyour votre nouveau serveur.</span><span class="sxs-lookup"><span data-stu-id="9c5f0-131">If you selected **Add tooPortal**, navigate tooyour portal toosee your new server.</span></span> <span data-ttu-id="9c5f0-132">Naviguer trop**davantage de services** > **Analysis Services** toosee si votre serveur est prêt.</span><span class="sxs-lookup"><span data-stu-id="9c5f0-132">Or, navigate too**More services** > **Analysis Services** toosee if your server is ready.</span></span>

 ![tableau de bord](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a><span data-ttu-id="9c5f0-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9c5f0-134">Next steps</span></span>
<span data-ttu-id="9c5f0-135">Une fois que vous avez créé votre serveur, vous pouvez [déployer un modèle](analysis-services-deploy.md) tooit à l’aide de SSDT ou SSMS.</span><span class="sxs-lookup"><span data-stu-id="9c5f0-135">Once you've created your server, you can [deploy a model](analysis-services-deploy.md) tooit by using SSDT or with SSMS.</span></span>

<span data-ttu-id="9c5f0-136">Si un modèle de déploiement tooyour serveur connecte à des sources de données tooon local, vous devez tooinstall une [passerelle de données locale](analysis-services-gateway.md) sur un ordinateur de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="9c5f0-136">If a model you deploy tooyour server connects tooon-premises data sources, you need tooinstall an [On-premises data gateway](analysis-services-gateway.md) on a computer in your network.</span></span>

