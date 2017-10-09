---
title: "modèles Azure Resource Manager d’aaaUse dans la pile de Azure | Documents Microsoft"
description: "Découvrez comment les modèles Azure Resource Manager toouse dans les ressources Azure pile tooprovision."
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
ms.openlocfilehash: bcc73756fa712ecff9791301d43d227112be8362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-resource-manager-templates-in-azure-stack"></a><span data-ttu-id="b5e4b-103">Utiliser les modèles Azure Resource Manager dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b5e4b-103">Use Azure Resource Manager templates in Azure Stack</span></span>
<span data-ttu-id="b5e4b-104">Les modèles de gestionnaire de ressources Azure déploiement et approvisionnement des toutes les ressources hello pour votre application dans une opération unique et coordonnée.</span><span class="sxs-lookup"><span data-stu-id="b5e4b-104">Azure Resource Manager templates deploy and provision all hello resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="b5e4b-105">Vous pouvez également redéployer modèles toomake modifications toohello ressources hello groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b5e4b-105">You can also redeploy templates toomake changes toohello resources in hello resource group.</span></span>

<span data-ttu-id="b5e4b-106">Ces modèles peuvent être déployés avec le portail de Microsoft Azure pile hello, PowerShell, ligne de commande hello et Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b5e4b-106">These templates can be deployed with hello Microsoft Azure Stack portal, PowerShell, hello command line, and Visual Studio.</span></span>

<span data-ttu-id="b5e4b-107">Hello suivant des modèles de démarrage rapide est disponible sur [GitHub](http://aka.ms/azurestackgithub):</span><span class="sxs-lookup"><span data-stu-id="b5e4b-107">hello following quickstart templates are available on [GitHub](http://aka.ms/azurestackgithub):</span></span>

## <a name="deploy-sharepoint-non-high-availability"></a><span data-ttu-id="b5e4b-108">Déploiement de SharePoint (sans haute disponibilité)</span><span class="sxs-lookup"><span data-stu-id="b5e4b-108">Deploy SharePoint (non-high availability)</span></span>
<span data-ttu-id="b5e4b-109">Utiliser hello DSC PowerShell extension toocreate un SharePoint 2013 batterie de serveurs comprenant hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="b5e4b-109">Use hello PowerShell DSC extension toocreate a SharePoint 2013 farm that includes hello following resources:</span></span>

* <span data-ttu-id="b5e4b-110">Un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="b5e4b-110">A virtual network</span></span>
* <span data-ttu-id="b5e4b-111">Trois comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="b5e4b-111">Three storage accounts</span></span>
* <span data-ttu-id="b5e4b-112">Deux équilibreurs de charge externes</span><span class="sxs-lookup"><span data-stu-id="b5e4b-112">Two external load balancers</span></span>
* <span data-ttu-id="b5e4b-113">Une machine virtuelle configurée en tant que contrôleur de domaine dans une nouvelle forêt avec un domaine unique</span><span class="sxs-lookup"><span data-stu-id="b5e4b-113">One VM configured as a domain controller for a new forest with a single domain</span></span>
* <span data-ttu-id="b5e4b-114">Une machine virtuelle configurée sous la forme d’un serveur autonome SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="b5e4b-114">One VM configured as a SQL Server 2014 stand-alone server</span></span>
* <span data-ttu-id="b5e4b-115">Une machine virtuelle configurée comme une batterie de serveurs SharePoint 2013 composée d’un seul ordinateur</span><span class="sxs-lookup"><span data-stu-id="b5e4b-115">One VM configured as a one machine SharePoint 2013 farm</span></span>

## <a name="deploy-ad-non-high-availability"></a><span data-ttu-id="b5e4b-116">Déployer AD (sans haute disponibilité)</span><span class="sxs-lookup"><span data-stu-id="b5e4b-116">Deploy AD (non-high availability)</span></span>
<span data-ttu-id="b5e4b-117">Utilisez hello DSC PowerShell extension toocreate un serveur de contrôleur de domaine Active Directory qui inclut hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="b5e4b-117">Use hello PowerShell DSC extension toocreate an AD domain controller server that includes hello following resources:</span></span>

* <span data-ttu-id="b5e4b-118">Un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="b5e4b-118">A virtual network</span></span>
* <span data-ttu-id="b5e4b-119">Un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="b5e4b-119">One storage account</span></span>
* <span data-ttu-id="b5e4b-120">Un équilibreur de charge externe</span><span class="sxs-lookup"><span data-stu-id="b5e4b-120">One external load balancer</span></span>
* <span data-ttu-id="b5e4b-121">Une machine virtuelle configurée en tant que contrôleur de domaine dans une nouvelle forêt avec un domaine unique</span><span class="sxs-lookup"><span data-stu-id="b5e4b-121">One VM configured as a domain controller for a new forest with a single domain</span></span>

## <a name="deploy-adsql-non-high-availability"></a><span data-ttu-id="b5e4b-122">Déploiement d’AD/SQL (sans haute disponibilité)</span><span class="sxs-lookup"><span data-stu-id="b5e4b-122">Deploy AD/SQL (non-high availability)</span></span>
<span data-ttu-id="b5e4b-123">Utiliser hello DSC PowerShell extension toocreate un SQL Server 2014 serveur autonome qui inclut hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="b5e4b-123">Use hello PowerShell DSC extension toocreate a SQL Server 2014 stand-alone server that includes hello following resources:</span></span>

* <span data-ttu-id="b5e4b-124">Un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="b5e4b-124">A virtual network</span></span>
* <span data-ttu-id="b5e4b-125">deux comptes de stockage ;</span><span class="sxs-lookup"><span data-stu-id="b5e4b-125">Two storage accounts</span></span>
* <span data-ttu-id="b5e4b-126">Un équilibreur de charge externe</span><span class="sxs-lookup"><span data-stu-id="b5e4b-126">One external load balancer</span></span>
* <span data-ttu-id="b5e4b-127">Une machine virtuelle configurée en tant que contrôleur de domaine dans une nouvelle forêt avec un domaine unique</span><span class="sxs-lookup"><span data-stu-id="b5e4b-127">One VM configured as a domain controller for a new forest with a single domain</span></span>
* <span data-ttu-id="b5e4b-128">Une machine virtuelle configurée sous la forme d’un serveur autonome SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="b5e4b-128">One VM configured as a SQL Server 2014 stand-alone server</span></span>

## <a name="vm-dsc-extension-azure-automation-pull-server"></a><span data-ttu-id="b5e4b-129">VM-DSC-Extension-Azure-Automation-Pull-Server</span><span class="sxs-lookup"><span data-stu-id="b5e4b-129">VM-DSC-Extension-Azure-Automation-Pull-Server</span></span>
<span data-ttu-id="b5e4b-130">Utilisez hello DSC PowerShell extension tooconfigure un ordinateur virtuel existant de Configuration Manager (local) et l’inscrire tooan serveur collecteur Azure Automation compte DSC.</span><span class="sxs-lookup"><span data-stu-id="b5e4b-130">Use hello PowerShell DSC extension tooconfigure an existing virtual machine Local Configuration Manager (LCM) and register it tooan Azure Automation Account DSC Pull Server.</span></span>

## <a name="create-a-virtual-machine-from-a-user-image"></a><span data-ttu-id="b5e4b-131">Création d’une machine virtuelle à partir d’une image utilisateur</span><span class="sxs-lookup"><span data-stu-id="b5e4b-131">Create a virtual machine from a user image</span></span>
<span data-ttu-id="b5e4b-132">Créez une machine virtuelle à partir d’une image utilisateur personnalisée.</span><span class="sxs-lookup"><span data-stu-id="b5e4b-132">Create a virtual machine from a custom user image.</span></span> <span data-ttu-id="b5e4b-133">Ce modèle déploie également un réseau virtuel (avec DNS), une adresse IP publique et une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="b5e4b-133">This template also deploys a virtual network (with DNS), public IP address, and a network interface.</span></span>

## <a name="simple-vm"></a><span data-ttu-id="b5e4b-134">Machine virtuelle simple</span><span class="sxs-lookup"><span data-stu-id="b5e4b-134">Simple VM</span></span>
<span data-ttu-id="b5e4b-135">Déployez une machine virtuelle Windows comprenant un réseau virtuel (avec DNS), une adresse IP publique et une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="b5e4b-135">Deploy a Windows VM that includes a virtual network (with DNS), public IP address, and a network interface.</span></span>

## <a name="cancel-a-running-template-deployment"></a><span data-ttu-id="b5e4b-136">Annuler le déploiement d’un modèle en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="b5e4b-136">Cancel a running template deployment</span></span>
<span data-ttu-id="b5e4b-137">toocancel un déploiement de modèle en cours d’exécution, utilisez hello `Stop-AzureRmResourceGroupDeployment` applet de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5e4b-137">toocancel a running template deployment, use hello `Stop-AzureRmResourceGroupDeployment` PowerShell cmdlet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5e4b-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b5e4b-138">Next steps</span></span>
[<span data-ttu-id="b5e4b-139">Déployer des modèles de portail de hello</span><span class="sxs-lookup"><span data-stu-id="b5e4b-139">Deploy templates with hello portal</span></span>](azure-stack-deploy-template-portal.md)

[<span data-ttu-id="b5e4b-140">Présentation d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b5e4b-140">Azure Resource Manager overview</span></span>](../azure-resource-manager/resource-group-overview.md)

