---
title: "Déployer un service web dans plusieurs régions | Microsoft Docs"
description: "Étapes pour déployer (copier) un nouveau service web dans d’autres régions."
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
ms.openlocfilehash: 3895537bbca72e687838ff5013c291dfee3be707
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-web-service-to-multiple-regions"></a><span data-ttu-id="3ecb7-103">Comment déployer un service web dans plusieurs régions</span><span class="sxs-lookup"><span data-stu-id="3ecb7-103">How to deploy a Web Service to multiple regions</span></span>
<span data-ttu-id="3ecb7-104">Les nouveaux services web Azure vous permettent de déployer facilement un service web dans plusieurs régions, sans avoir besoin de plusieurs abonnements ou espaces de travail.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-104">The New Azure Web Services allow you to easily deploy a web service to multiple regions without needing multiple subscriptions or workspaces.</span></span> 

<span data-ttu-id="3ecb7-105">Le tarif est spécifique à chaque région et vous devez donc définir un profil de facturation pour chaque région dans laquelle vous allez déployer le service web.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-105">Pricing is region specific, therefore you must define a billing plan for each region in which you will deploy the web service.</span></span>

## <a name="to-create-a-plan-in-another-region"></a><span data-ttu-id="3ecb7-106">Pour créer un profil dans une autre région</span><span class="sxs-lookup"><span data-stu-id="3ecb7-106">To create a plan in another region</span></span>
1. <span data-ttu-id="3ecb7-107">Connectez-vous aux [services web Microsoft Azure Machine Learning](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="3ecb7-107">Sign into [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).</span></span>
2. <span data-ttu-id="3ecb7-108">Cliquez sur l’option de menu **Abonnements** .</span><span class="sxs-lookup"><span data-stu-id="3ecb7-108">Click the **Plans** menu option.</span></span>
3. <span data-ttu-id="3ecb7-109">Sur la page de présentation des abonnements, cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-109">On the Plans over view page, click **New**.</span></span>
4. <span data-ttu-id="3ecb7-110">Dans la liste déroulante **Abonnement** , sélectionnez l’abonnement dans lequel résidera le nouveau plan.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-110">From the **Subscription** dropdown, select the subscription in which the new plan will reside.</span></span>
5. <span data-ttu-id="3ecb7-111">Dans la liste déroulante **Région** , sélectionnez une région pour le nouveau plan.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-111">From the **Region** dropdown, select a region for the new plan.</span></span> <span data-ttu-id="3ecb7-112">Les options du plan de la région sélectionnée apparaissent dans la section **Plan Options** (Option du plan) de la page.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-112">The Plan Options for the selected region will display in the **Plan Options** section of the page.</span></span>
6. <span data-ttu-id="3ecb7-113">Dans la liste déroulante **Groupe de ressources** , sélectionnez un groupe de ressources pour le plan.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-113">From the **Resource Group** dropdown, select a resource group for the plan.</span></span> <span data-ttu-id="3ecb7-114">Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3ecb7-114">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
7. <span data-ttu-id="3ecb7-115">Dans **Plan Name** (Nom du plan), tapez le nom du plan.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-115">In **Plan Name** type the name of the plan.</span></span>
8. <span data-ttu-id="3ecb7-116">Sous **Plan Options**(Options du plan), cliquez sur le niveau de facturation du nouveau plan.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-116">Under **Plan Options**, click the billing level for the new plan.</span></span>
9. <span data-ttu-id="3ecb7-117">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-117">Click **Create**.</span></span>

## <a name="deploying-the-web-service-to-another-region"></a><span data-ttu-id="3ecb7-118">Déploiement du service web dans une autre région</span><span class="sxs-lookup"><span data-stu-id="3ecb7-118">Deploying the web service to another region</span></span>
1. <span data-ttu-id="3ecb7-119">Cliquez sur l’option de menu **Services web** .</span><span class="sxs-lookup"><span data-stu-id="3ecb7-119">Click the **Web Services** menu option.</span></span>
2. <span data-ttu-id="3ecb7-120">Sélectionnez le service web que vous déployez dans une nouvelle région.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-120">Select the Web Service you are deploying to a new region.</span></span>
3. <span data-ttu-id="3ecb7-121">Cliquez sur **Copy**.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-121">Click **Copy**.</span></span>
4. <span data-ttu-id="3ecb7-122">Dans **Nom du service web**, tapez le nouveau nom du service web.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-122">In **Web Service Name**, type a new name for the web service.</span></span>
5. <span data-ttu-id="3ecb7-123">Dans **Description du service web**, tapez une description du service web.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-123">In **Web service description**, type a description for the web service.</span></span>
6. <span data-ttu-id="3ecb7-124">Dans la liste déroulante **Abonnement** , sélectionnez l’abonnement dans lequel résidera le nouveau service web.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-124">From the **Subscription** dropdown, select the subscription in which the new web service will reside.</span></span>
7. <span data-ttu-id="3ecb7-125">Dans la liste déroulante **Groupe de ressources** , sélectionnez un groupe de ressources pour le service web.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-125">From the **Resource Group** dropdown, select a resource group for the web service.</span></span> <span data-ttu-id="3ecb7-126">Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3ecb7-126">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="3ecb7-127">Dans la liste déroulante **Région** , sélectionnez la région dans laquelle vous voulez déployer le service web.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-127">From the **Region** dropdown, select the region in which to deploy the web service.</span></span>
9. <span data-ttu-id="3ecb7-128">Dans la liste déroulante **Compte de stockage** , sélectionnez un compte de stockage où stocker le service web.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-128">From the **Storage account** dropdown, select a storage account in which to store the web service.</span></span>
10. <span data-ttu-id="3ecb7-129">Dans la liste déroulante **Plan de tarification** , sélectionnez un plan dans la région que vous avez sélectionnée à l’étape 8.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-129">From the **Price Plan** dropdown, select a plan in the region you selected in step 8.</span></span>
11. <span data-ttu-id="3ecb7-130">Cliquez sur **Copy**.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-130">Click **Copy**.</span></span>

