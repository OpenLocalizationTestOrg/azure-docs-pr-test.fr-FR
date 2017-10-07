---
title: "aaaHow toodeploy un Service Web toomultiple régions | Documents Microsoft"
description: "Étapes toodeploy (copier) un régions tooother de nouveau Service Web."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: cgronlun
ms.assetid: 36c60411-f2db-4ee2-9b66-b1f1d77a8f44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 21fcdb96f118c60ed98b60b1b2df833766c7c8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-web-service-toomultiple-regions"></a><span data-ttu-id="0929c-103">Comment toodeploy un Service Web toomultiple régions</span><span class="sxs-lookup"><span data-stu-id="0929c-103">How toodeploy a Web Service toomultiple regions</span></span>
<span data-ttu-id="0929c-104">Hello nouveaux Services Web de Azure permettent tooeasily déployer un régions toomultiple du service web sans avoir besoin de plusieurs abonnements ou les espaces de travail.</span><span class="sxs-lookup"><span data-stu-id="0929c-104">hello New Azure Web Services allow you tooeasily deploy a web service toomultiple regions without needing multiple subscriptions or workspaces.</span></span> 

<span data-ttu-id="0929c-105">La tarification est région spécifique, que vous devez donc définir un plan de facturation pour chaque région dans laquelle vous allez déployer le service web de hello.</span><span class="sxs-lookup"><span data-stu-id="0929c-105">Pricing is region specific, therefore you must define a billing plan for each region in which you will deploy hello web service.</span></span>

## <a name="toocreate-a-plan-in-another-region"></a><span data-ttu-id="0929c-106">toocreate un plan dans une autre région</span><span class="sxs-lookup"><span data-stu-id="0929c-106">toocreate a plan in another region</span></span>
1. <span data-ttu-id="0929c-107">Connectez-vous aux [services web Microsoft Azure Machine Learning](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="0929c-107">Sign into [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).</span></span>
2. <span data-ttu-id="0929c-108">Cliquez sur hello **Plans** option de menu.</span><span class="sxs-lookup"><span data-stu-id="0929c-108">Click hello **Plans** menu option.</span></span>
3. <span data-ttu-id="0929c-109">Dans les Plans de hello sur la page de vue, cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="0929c-109">On hello Plans over view page, click **New**.</span></span>
4. <span data-ttu-id="0929c-110">À partir de hello **abonnement** liste déroulante, abonnement hello sélectionnez réside dans le hello nouveau plan.</span><span class="sxs-lookup"><span data-stu-id="0929c-110">From hello **Subscription** dropdown, select hello subscription in which hello new plan will reside.</span></span>
5. <span data-ttu-id="0929c-111">À partir de hello **région** liste déroulante, sélectionnez une région pour le nouveau plan de hello.</span><span class="sxs-lookup"><span data-stu-id="0929c-111">From hello **Region** dropdown, select a region for hello new plan.</span></span> <span data-ttu-id="0929c-112">Hello Options du Plan pour la région sélectionnée hello affichera Bonjour **Options du Plan** section de la page de hello.</span><span class="sxs-lookup"><span data-stu-id="0929c-112">hello Plan Options for hello selected region will display in hello **Plan Options** section of hello page.</span></span>
6. <span data-ttu-id="0929c-113">À partir de hello **groupe de ressources** liste déroulante, sélectionnez une ressource de groupe pour le plan de hello.</span><span class="sxs-lookup"><span data-stu-id="0929c-113">From hello **Resource Group** dropdown, select a resource group for hello plan.</span></span> <span data-ttu-id="0929c-114">Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0929c-114">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
7. <span data-ttu-id="0929c-115">Dans **le nom du Plan** nom hello du type de plan de hello.</span><span class="sxs-lookup"><span data-stu-id="0929c-115">In **Plan Name** type hello name of hello plan.</span></span>
8. <span data-ttu-id="0929c-116">Sous **des Options Plan**, cliquez sur le niveau facturation hello pour le nouveau plan de hello.</span><span class="sxs-lookup"><span data-stu-id="0929c-116">Under **Plan Options**, click hello billing level for hello new plan.</span></span>
9. <span data-ttu-id="0929c-117">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="0929c-117">Click **Create**.</span></span>

## <a name="deploying-hello-web-service-tooanother-region"></a><span data-ttu-id="0929c-118">Déploiement de service tooanother région hello web</span><span class="sxs-lookup"><span data-stu-id="0929c-118">Deploying hello web service tooanother region</span></span>
1. <span data-ttu-id="0929c-119">Cliquez sur hello **Services Web** option de menu.</span><span class="sxs-lookup"><span data-stu-id="0929c-119">Click hello **Web Services** menu option.</span></span>
2. <span data-ttu-id="0929c-120">Sélectionnez Service Web que vous déployez tooa nouvelle région de hello.</span><span class="sxs-lookup"><span data-stu-id="0929c-120">Select hello Web Service you are deploying tooa new region.</span></span>
3. <span data-ttu-id="0929c-121">Cliquez sur **Copy**.</span><span class="sxs-lookup"><span data-stu-id="0929c-121">Click **Copy**.</span></span>
4. <span data-ttu-id="0929c-122">Dans **nom du Service Web**, tapez un nouveau nom pour le service web de hello.</span><span class="sxs-lookup"><span data-stu-id="0929c-122">In **Web Service Name**, type a new name for hello web service.</span></span>
5. <span data-ttu-id="0929c-123">Dans **description du service Web**, tapez une description de service web de hello.</span><span class="sxs-lookup"><span data-stu-id="0929c-123">In **Web service description**, type a description for hello web service.</span></span>
6. <span data-ttu-id="0929c-124">À partir de hello **abonnement** liste déroulante, abonnement hello sélectionnez réside dans le hello nouveau service web.</span><span class="sxs-lookup"><span data-stu-id="0929c-124">From hello **Subscription** dropdown, select hello subscription in which hello new web service will reside.</span></span>
7. <span data-ttu-id="0929c-125">À partir de hello **groupe de ressources** liste déroulante, sélectionnez une ressource de groupe pour le service web de hello.</span><span class="sxs-lookup"><span data-stu-id="0929c-125">From hello **Resource Group** dropdown, select a resource group for hello web service.</span></span> <span data-ttu-id="0929c-126">Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0929c-126">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="0929c-127">À partir de hello **région** liste déroulante, la région de hello select dans le service web qui toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="0929c-127">From hello **Region** dropdown, select hello region in which toodeploy hello web service.</span></span>
9. <span data-ttu-id="0929c-128">À partir de hello **compte de stockage** liste déroulante, sélectionnez un compte de stockage dans le hello toostore de service web.</span><span class="sxs-lookup"><span data-stu-id="0929c-128">From hello **Storage account** dropdown, select a storage account in which toostore hello web service.</span></span>
10. <span data-ttu-id="0929c-129">À partir de hello **Plan tarifaire** liste déroulante, sélectionnez un plan dans la région de hello sélectionnée à l’étape 8.</span><span class="sxs-lookup"><span data-stu-id="0929c-129">From hello **Price Plan** dropdown, select a plan in hello region you selected in step 8.</span></span>
11. <span data-ttu-id="0929c-130">Cliquez sur **Copy**.</span><span class="sxs-lookup"><span data-stu-id="0929c-130">Click **Copy**.</span></span>

