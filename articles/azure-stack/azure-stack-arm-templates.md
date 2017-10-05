---
title: "Utiliser les modèles Azure Resource Manager dans Azure Stack | Microsoft Docs"
description: "Découvrez comment utiliser les modèles Azure Resource Manager dans Azure Stack pour approvisionner des ressources."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 2022dbe5-47fd-457d-9af3-6c01688171d7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 228e641afefd16edc7b405a2fc1d60184ce41e96
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-azure-resource-manager-templates-in-azure-stack"></a><span data-ttu-id="e6319-103">Utiliser les modèles Azure Resource Manager dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="e6319-103">Use Azure Resource Manager templates in Azure Stack</span></span>
<span data-ttu-id="e6319-104">Les modèles Azure Resource Manager déploient et approvisionnent toutes les ressources de l’application en une seule opération coordonnée.</span><span class="sxs-lookup"><span data-stu-id="e6319-104">Azure Resource Manager templates deploy and provision all the resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="e6319-105">Vous pouvez également redéployer des modèles pour apporter des modifications aux ressources dans le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e6319-105">You can also redeploy templates to make changes to the resources in the resource group.</span></span>

<span data-ttu-id="e6319-106">Ces modèles peuvent être déployés à l’aide du portail Microsoft Azure Stack, de PowerShell, de l’interface de ligne de commande et de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e6319-106">These templates can be deployed with the Microsoft Azure Stack portal, PowerShell, the command line, and Visual Studio.</span></span>

<span data-ttu-id="e6319-107">Les modèles de démarrage rapide suivants sont disponibles sur [GitHub](http://aka.ms/azurestackgithub) :</span><span class="sxs-lookup"><span data-stu-id="e6319-107">The following quickstart templates are available on [GitHub](http://aka.ms/azurestackgithub):</span></span>

## <a name="deploy-sharepoint-non-high-availability"></a><span data-ttu-id="e6319-108">Déploiement de SharePoint (sans haute disponibilité)</span><span class="sxs-lookup"><span data-stu-id="e6319-108">Deploy SharePoint (non-high availability)</span></span>
<span data-ttu-id="e6319-109">Utilisez l’extension PowerShell DSC pour créer une batterie de serveurs SharePoint 2013 comprenant les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="e6319-109">Use the PowerShell DSC extension to create a SharePoint 2013 farm that includes the following resources:</span></span>

* <span data-ttu-id="e6319-110">Un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="e6319-110">A virtual network</span></span>
* <span data-ttu-id="e6319-111">Trois comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="e6319-111">Three storage accounts</span></span>
* <span data-ttu-id="e6319-112">Deux équilibreurs de charge externes</span><span class="sxs-lookup"><span data-stu-id="e6319-112">Two external load balancers</span></span>
* <span data-ttu-id="e6319-113">Une machine virtuelle configurée en tant que contrôleur de domaine dans une nouvelle forêt avec un domaine unique</span><span class="sxs-lookup"><span data-stu-id="e6319-113">One VM configured as a domain controller for a new forest with a single domain</span></span>
* <span data-ttu-id="e6319-114">Une machine virtuelle configurée sous la forme d’un serveur autonome SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="e6319-114">One VM configured as a SQL Server 2014 stand-alone server</span></span>
* <span data-ttu-id="e6319-115">Une machine virtuelle configurée comme une batterie de serveurs SharePoint 2013 composée d’un seul ordinateur</span><span class="sxs-lookup"><span data-stu-id="e6319-115">One VM configured as a one machine SharePoint 2013 farm</span></span>

## <a name="deploy-ad-non-high-availability"></a><span data-ttu-id="e6319-116">Déployer AD (sans haute disponibilité)</span><span class="sxs-lookup"><span data-stu-id="e6319-116">Deploy AD (non-high availability)</span></span>
<span data-ttu-id="e6319-117">Utilisez l’extension PowerShell DSC pour créer un serveur de contrôleurs de domaine AD comprenant les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="e6319-117">Use the PowerShell DSC extension to create an AD domain controller server that includes the following resources:</span></span>

* <span data-ttu-id="e6319-118">Un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="e6319-118">A virtual network</span></span>
* <span data-ttu-id="e6319-119">Un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="e6319-119">One storage account</span></span>
* <span data-ttu-id="e6319-120">Un équilibreur de charge externe</span><span class="sxs-lookup"><span data-stu-id="e6319-120">One external load balancer</span></span>
* <span data-ttu-id="e6319-121">Une machine virtuelle configurée en tant que contrôleur de domaine dans une nouvelle forêt avec un domaine unique</span><span class="sxs-lookup"><span data-stu-id="e6319-121">One VM configured as a domain controller for a new forest with a single domain</span></span>

## <a name="deploy-adsql-non-high-availability"></a><span data-ttu-id="e6319-122">Déploiement d’AD/SQL (sans haute disponibilité)</span><span class="sxs-lookup"><span data-stu-id="e6319-122">Deploy AD/SQL (non-high availability)</span></span>
<span data-ttu-id="e6319-123">Utilisez l’extension PowerShell DSC pour créer un serveur autonome SQL Server 2014 comprenant les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="e6319-123">Use the PowerShell DSC extension to create a SQL Server 2014 stand-alone server that includes the following resources:</span></span>

* <span data-ttu-id="e6319-124">Un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="e6319-124">A virtual network</span></span>
* <span data-ttu-id="e6319-125">deux comptes de stockage ;</span><span class="sxs-lookup"><span data-stu-id="e6319-125">Two storage accounts</span></span>
* <span data-ttu-id="e6319-126">Un équilibreur de charge externe</span><span class="sxs-lookup"><span data-stu-id="e6319-126">One external load balancer</span></span>
* <span data-ttu-id="e6319-127">Une machine virtuelle configurée en tant que contrôleur de domaine dans une nouvelle forêt avec un domaine unique</span><span class="sxs-lookup"><span data-stu-id="e6319-127">One VM configured as a domain controller for a new forest with a single domain</span></span>
* <span data-ttu-id="e6319-128">Une machine virtuelle configurée sous la forme d’un serveur autonome SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="e6319-128">One VM configured as a SQL Server 2014 stand-alone server</span></span>

## <a name="vm-dsc-extension-azure-automation-pull-server"></a><span data-ttu-id="e6319-129">VM-DSC-Extension-Azure-Automation-Pull-Server</span><span class="sxs-lookup"><span data-stu-id="e6319-129">VM-DSC-Extension-Azure-Automation-Pull-Server</span></span>
<span data-ttu-id="e6319-130">Utilisez l’extension PowerShell DSC pour configurer un gestionnaire local de configuration (LCM) de machines virtuelles existant et enregistrez-le dans un serveur Pull DSC de compte Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="e6319-130">Use the PowerShell DSC extension to configure an existing virtual machine Local Configuration Manager (LCM) and register it to an Azure Automation Account DSC Pull Server.</span></span>

## <a name="create-a-virtual-machine-from-a-user-image"></a><span data-ttu-id="e6319-131">Création d’une machine virtuelle à partir d’une image utilisateur</span><span class="sxs-lookup"><span data-stu-id="e6319-131">Create a virtual machine from a user image</span></span>
<span data-ttu-id="e6319-132">Créez une machine virtuelle à partir d’une image utilisateur personnalisée.</span><span class="sxs-lookup"><span data-stu-id="e6319-132">Create a virtual machine from a custom user image.</span></span> <span data-ttu-id="e6319-133">Ce modèle déploie également un réseau virtuel (avec DNS), une adresse IP publique et une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="e6319-133">This template also deploys a virtual network (with DNS), public IP address, and a network interface.</span></span>

## <a name="simple-vm"></a><span data-ttu-id="e6319-134">Machine virtuelle simple</span><span class="sxs-lookup"><span data-stu-id="e6319-134">Simple VM</span></span>
<span data-ttu-id="e6319-135">Déployez une machine virtuelle Windows comprenant un réseau virtuel (avec DNS), une adresse IP publique et une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="e6319-135">Deploy a Windows VM that includes a virtual network (with DNS), public IP address, and a network interface.</span></span>

## <a name="cancel-a-running-template-deployment"></a><span data-ttu-id="e6319-136">Annuler le déploiement d’un modèle en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="e6319-136">Cancel a running template deployment</span></span>
<span data-ttu-id="e6319-137">Pour annuler le déploiement d’un modèle en cours d’exécution, utilisez la cmdlet PowerShell `Stop-AzureRmResourceGroupDeployment`.</span><span class="sxs-lookup"><span data-stu-id="e6319-137">To cancel a running template deployment, use the `Stop-AzureRmResourceGroupDeployment` PowerShell cmdlet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6319-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e6319-138">Next steps</span></span>
[<span data-ttu-id="e6319-139">Déployer des modèles avec le portail</span><span class="sxs-lookup"><span data-stu-id="e6319-139">Deploy templates with the portal</span></span>](azure-stack-deploy-template-portal.md)

[<span data-ttu-id="e6319-140">Présentation d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e6319-140">Azure Resource Manager overview</span></span>](../azure-resource-manager/resource-group-overview.md)

