---
title: " Gérer un serveur de processus en cours d’exécution dans Azure (Resource Manager) | Microsoft Docs"
description: "Cet article décrit comment tooset d’une restauration automatique processus serveur (Resource Manager) dans Azure."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 70426b96095cc42befff6c4114fb56536284a667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a><span data-ttu-id="8e979-103">Gérer un serveur de processus en cours d’exécution dans Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="8e979-103">Manage a process server running in Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8e979-104">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="8e979-104">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [<span data-ttu-id="8e979-105">Classic </span><span class="sxs-lookup"><span data-stu-id="8e979-105">Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)

<span data-ttu-id="8e979-106">Lors de la restauration automatique, il est recommandé de serveur de processus toodeploy dans Azure s’il existe une latence élevée entre hello réseau virtuel Azure et votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="8e979-106">During failback, it is recommended toodeploy process server in Azure if there is high latency between hello Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="8e979-107">Cet article décrit comment vous pouvez définir, configurer et gérer des serveurs de traitement hello s’exécutant dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8e979-107">This article describes how you can set up, configure, and manage hello process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="8e979-108">Cet article est utilisé si vous avez utilisé des toobe **le Gestionnaire de ressources** en tant que modèle de déploiement hello pour les ordinateurs virtuels de hello pendant le basculement.</span><span class="sxs-lookup"><span data-stu-id="8e979-108">This article is toobe used if you used **Resource Manager** as hello deployment model for hello virtual machines during failover.</span></span> <span data-ttu-id="8e979-109">Si vous avez utilisé **classique** en tant que modèle de déploiement hello, suivez les étapes de hello dans [comment tooset & Mettre à configurer un serveur de processus de restauration automatique (classique)](./site-recovery-vmware-setup-azure-ps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="8e979-109">If you used **Classic** as hello deployment model, follow hello steps in [How tooset up & configure a Failback process server (Classic)](./site-recovery-vmware-setup-azure-ps-classic.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e979-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8e979-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="8e979-111">Déployer un serveur de processus dans Azure</span><span class="sxs-lookup"><span data-stu-id="8e979-111">Deploy a process server on Azure</span></span>
1. <span data-ttu-id="8e979-112">Bonjour coffre > **Infrastructure Site Recovery** (sous le titre de « Gérer » hello) > **serveurs de Configuration** (titre « Pour VMware et les Machines physiques »), sélectionnez le serveur de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="8e979-112">In hello Vault > **Site Recovery Infrastructure** (under hello "Manage" heading) > **Configuration Servers** (under "For VMware and Physical Machines" heading), select hello configuration server.</span></span>
2. <span data-ttu-id="8e979-113">Dans la page de détails de Configuration serveur hello qui s’ouvre, cliquez sur « + serveur de traitement »</span><span class="sxs-lookup"><span data-stu-id="8e979-113">In hello Configuration Server details page that opens click "+ Process server"</span></span>

  ![Galerie Ajouter un serveur de processus](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  <span data-ttu-id="8e979-115">Sur hello **ajouter un serveur de processus** page, sélectionnez hello valeurs suivantes</span><span class="sxs-lookup"><span data-stu-id="8e979-115">On hello **Add process server** page, select hello following values</span></span>

  ![Élément de la galerie Ajouter un serveur de processus](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|<span data-ttu-id="8e979-117">**Nom du champ**</span><span class="sxs-lookup"><span data-stu-id="8e979-117">**Field Name**</span></span>|<span data-ttu-id="8e979-118">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="8e979-118">**Value**</span></span>|
|-|-|
|<span data-ttu-id="8e979-119">Choisissez où vous souhaitez toodeploy votre serveur de processus</span><span class="sxs-lookup"><span data-stu-id="8e979-119">Choose where you want toodeploy your process server</span></span>|<span data-ttu-id="8e979-120">Sélectionnez la valeur de hello **déployer un serveur de processus de restauration dans Azure**</span><span class="sxs-lookup"><span data-stu-id="8e979-120">Select hello value **Deploy a failback process server in Azure**</span></span> |
|<span data-ttu-id="8e979-121">Abonnement</span><span class="sxs-lookup"><span data-stu-id="8e979-121">Subscription</span></span>|<span data-ttu-id="8e979-122">Sélectionnez hello abonnement Azure où vous hello machines virtuelles ayant basculé</span><span class="sxs-lookup"><span data-stu-id="8e979-122">Select hello Azure Subscription where you failed over hello virtual machines</span></span>|
|<span data-ttu-id="8e979-123">Groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="8e979-123">Resource Group</span></span>|<span data-ttu-id="8e979-124">Vous pouvez créer un groupe de ressources de toodeploy ce serveur de processus ou choisissez un serveur de processus toodeploy hello dans un groupe de ressources existant</span><span class="sxs-lookup"><span data-stu-id="8e979-124">You can create a Resource Group toodeploy this process server or choose toodeploy hello process server in an existing Resource Group</span></span>|
|<span data-ttu-id="8e979-125">Lieu</span><span class="sxs-lookup"><span data-stu-id="8e979-125">Location</span></span>|<span data-ttu-id="8e979-126">Sélectionnez le centre de données Azure hello dans laquelle les ordinateurs virtuels hello où basculé dans</span><span class="sxs-lookup"><span data-stu-id="8e979-126">Select hello Azure Data Center into which hello virtual machines where failed over into</span></span>|
|<span data-ttu-id="8e979-127">Réseau Azure</span><span class="sxs-lookup"><span data-stu-id="8e979-127">Azure Network</span></span>|<span data-ttu-id="8e979-128">Sélectionnez hello Network(VNet) virtuel Azure qui hello des machines virtuelles où basculé dans.</span><span class="sxs-lookup"><span data-stu-id="8e979-128">Select hello Azure Virtual Network(VNet) that hello virtual machines where failed over into.</span></span> <span data-ttu-id="8e979-129">Si vous avez basculé des machines virtuelles dans plusieurs réseaux virtuels Azure, vous devez déployer un serveur de processus pour chaque réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="8e979-129">If you failed over virtual machines into multiple Azure VNets, then you need a process server deployed per VNet</span></span>|

4. <span data-ttu-id="8e979-130">Renseignez hello autres propriétés hello pour serveur de processus hello</span><span class="sxs-lookup"><span data-stu-id="8e979-130">Fill in hello rest of hello properties for hello process server</span></span>

  ![Récapitulatif Ajouter un serveur de processus](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|<span data-ttu-id="8e979-132">**Nom du champ**</span><span class="sxs-lookup"><span data-stu-id="8e979-132">**Field Name**</span></span>|<span data-ttu-id="8e979-133">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="8e979-133">**Value**</span></span>|
|-|-|
|<span data-ttu-id="8e979-134">Nom du serveur</span><span class="sxs-lookup"><span data-stu-id="8e979-134">Server Name</span></span>|<span data-ttu-id="8e979-135">Nom d’affichage et nom d’hôte de la machine virtuelle de votre serveur processus</span><span class="sxs-lookup"><span data-stu-id="8e979-135">Display name & Host name for your process server virtual machine</span></span>|
| <span data-ttu-id="8e979-136">User Name</span><span class="sxs-lookup"><span data-stu-id="8e979-136">User Name</span></span>|<span data-ttu-id="8e979-137">Nom d’utilisateur qui devient un administrateur sur cette machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="8e979-137">A user name that becomes an Administrator on that virtual machine</span></span>|
|<span data-ttu-id="8e979-138">Compte de stockage</span><span class="sxs-lookup"><span data-stu-id="8e979-138">Storage Account</span></span>|<span data-ttu-id="8e979-139">Nom de compte de stockage où est placé les du disque virtuel hello machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="8e979-139">Name of hello Storage Account where hello virtual machine's virtual disk's are placed</span></span>|
|<span data-ttu-id="8e979-140">Sous-réseau</span><span class="sxs-lookup"><span data-stu-id="8e979-140">Subnet</span></span>|<span data-ttu-id="8e979-141">sous-réseau Hello de machine virtuelle de hello réseau virtuel Azure toowhich hello est connecté.</span><span class="sxs-lookup"><span data-stu-id="8e979-141">hello subnet of hello Azure VNet toowhich hello virtual machine is connected</span></span>|
| <span data-ttu-id="8e979-142">Adresse IP</span><span class="sxs-lookup"><span data-stu-id="8e979-142">IP Address</span></span>|<span data-ttu-id="8e979-143">Adresse IP que vous aimeriez hello processus serveur tooassume une fois qu’il démarre</span><span class="sxs-lookup"><span data-stu-id="8e979-143">IP Address that you would like hello process server tooassume once it boots up</span></span>|
5. <span data-ttu-id="8e979-144">Cliquez sur toostart de bouton OK hello déploiement d’ordinateur virtuel de hello processus serveur.</span><span class="sxs-lookup"><span data-stu-id="8e979-144">Click hello OK button toostart deploying hello process server virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="8e979-145">toouse en mesure de toobe ce serveur de processus pour la restauration automatique, vous devez tooregister avec le serveur de configuration local hello.</span><span class="sxs-lookup"><span data-stu-id="8e979-145">toobe able toouse this process server for failback, you need tooregister it with hello on-premises configuration server.</span></span>

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a><span data-ttu-id="8e979-146">L’inscription hello processus serveur (en cours d’exécution dans Azure) tooa Configuration serveur (local)</span><span class="sxs-lookup"><span data-stu-id="8e979-146">Registering hello process server (running in Azure) tooa Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a><span data-ttu-id="8e979-147">La mise à niveau hello processus toolatest version du serveur.</span><span class="sxs-lookup"><span data-stu-id="8e979-147">Upgrading hello process server toolatest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="8e979-148">Annuler l’inscription du serveur de processus hello (en cours d’exécution dans Azure) à partir d’un serveur de Configuration (en cours d’exécution locale)</span><span class="sxs-lookup"><span data-stu-id="8e979-148">Unregistering hello process server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
