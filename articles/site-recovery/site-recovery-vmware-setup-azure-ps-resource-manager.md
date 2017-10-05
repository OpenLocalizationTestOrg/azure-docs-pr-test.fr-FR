---
title: " Gérer un serveur de processus en cours d’exécution dans Azure (Resource Manager) | Microsoft Docs"
description: Cet article explique comment configurer un serveur de processus de restauration automatique (Resource Manager) dans Azure.
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
ms.openlocfilehash: 2b9b31abd5d11d02935a74e47d26be9803cdc920
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a><span data-ttu-id="0c548-103">Gérer un serveur de processus en cours d’exécution dans Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="0c548-103">Manage a process server running in Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0c548-104">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="0c548-104">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [<span data-ttu-id="0c548-105">Classic </span><span class="sxs-lookup"><span data-stu-id="0c548-105">Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)

<span data-ttu-id="0c548-106">Lors de la restauration automatique, il est recommandé de déployer le serveur de processus dans Azure s’il existe une latence élevée entre le réseau virtuel Azure et votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="0c548-106">During failback, it is recommended to deploy process server in Azure if there is high latency between the Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="0c548-107">Cet article explique comment installer, configurer et gérer les serveurs de processus en cours d’exécution dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0c548-107">This article describes how you can set up, configure, and manage the process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="0c548-108">Consultez cet article si vous avez utilisé **Resource Manager** comme modèle de déploiement pour les machines virtuelles lors du basculement.</span><span class="sxs-lookup"><span data-stu-id="0c548-108">This article is to be used if you used **Resource Manager** as the deployment model for the virtual machines during failover.</span></span> <span data-ttu-id="0c548-109">Si vous avez utilisé le modèle de déploiement **Classic**, suivez les étapes de la rubrique [Guide pratique pour installer et configurer un serveur de processus de restauration automatique (Classic)](./site-recovery-vmware-setup-azure-ps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="0c548-109">If you used **Classic** as the deployment model, follow the steps in [How to set up & configure a Failback process server (Classic)](./site-recovery-vmware-setup-azure-ps-classic.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c548-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0c548-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="0c548-111">Déployer un serveur de processus dans Azure</span><span class="sxs-lookup"><span data-stu-id="0c548-111">Deploy a process server on Azure</span></span>
1. <span data-ttu-id="0c548-112">Sous Coffre > **Infrastructure Site Recovery** (sous le titre « Gérer ») > **Serveurs de configuration** (sous le titre « Pour VMware et les machines physiques »), sélectionnez le serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="0c548-112">In the Vault > **Site Recovery Infrastructure** (under the "Manage" heading) > **Configuration Servers** (under "For VMware and Physical Machines" heading), select the configuration server.</span></span>
2. <span data-ttu-id="0c548-113">Dans la page des détails du serveur de configuration qui s’ouvre, cliquez sur « +Serveur de processus »</span><span class="sxs-lookup"><span data-stu-id="0c548-113">In the Configuration Server details page that opens click "+ Process server"</span></span>

  ![Galerie Ajouter un serveur de processus](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  <span data-ttu-id="0c548-115">Sur la page **Ajouter un serveur de processus**, sélectionnez les valeurs suivantes</span><span class="sxs-lookup"><span data-stu-id="0c548-115">On the **Add process server** page, select the following values</span></span>

  ![Élément de la galerie Ajouter un serveur de processus](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|<span data-ttu-id="0c548-117">**Nom du champ**</span><span class="sxs-lookup"><span data-stu-id="0c548-117">**Field Name**</span></span>|<span data-ttu-id="0c548-118">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="0c548-118">**Value**</span></span>|
|-|-|
|<span data-ttu-id="0c548-119">Indique où vous souhaitez déployer votre serveur de processus</span><span class="sxs-lookup"><span data-stu-id="0c548-119">Choose where you want to deploy your process server</span></span>|<span data-ttu-id="0c548-120">Sélectionnez la valeur **Déployer un serveur de processus de restauration automatique dans Azure**</span><span class="sxs-lookup"><span data-stu-id="0c548-120">Select the value **Deploy a failback process server in Azure**</span></span> |
|<span data-ttu-id="0c548-121">Abonnement</span><span class="sxs-lookup"><span data-stu-id="0c548-121">Subscription</span></span>|<span data-ttu-id="0c548-122">Sélectionnez l’abonnement Azure dans lequel vous avez basculé les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="0c548-122">Select the Azure Subscription where you failed over the virtual machines</span></span>|
|<span data-ttu-id="0c548-123">Groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="0c548-123">Resource Group</span></span>|<span data-ttu-id="0c548-124">Vous pouvez créer un groupe de ressources afin d’y déployer ce serveur de processus, ou choisir de déployer le serveur de processus dans un groupe de ressources existant</span><span class="sxs-lookup"><span data-stu-id="0c548-124">You can create a Resource Group to deploy this process server or choose to deploy the process server in an existing Resource Group</span></span>|
|<span data-ttu-id="0c548-125">Lieu</span><span class="sxs-lookup"><span data-stu-id="0c548-125">Location</span></span>|<span data-ttu-id="0c548-126">Sélectionnez le centre de données Azure dans lequel les machines virtuelles ont été basculées</span><span class="sxs-lookup"><span data-stu-id="0c548-126">Select the Azure Data Center into which the virtual machines where failed over into</span></span>|
|<span data-ttu-id="0c548-127">Réseau Azure</span><span class="sxs-lookup"><span data-stu-id="0c548-127">Azure Network</span></span>|<span data-ttu-id="0c548-128">Sélectionnez le réseau virtuel Azure (VNet) dans lequel les machines virtuelles ont été basculées.</span><span class="sxs-lookup"><span data-stu-id="0c548-128">Select the Azure Virtual Network(VNet) that the virtual machines where failed over into.</span></span> <span data-ttu-id="0c548-129">Si vous avez basculé des machines virtuelles dans plusieurs réseaux virtuels Azure, vous devez déployer un serveur de processus pour chaque réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="0c548-129">If you failed over virtual machines into multiple Azure VNets, then you need a process server deployed per VNet</span></span>|

4. <span data-ttu-id="0c548-130">Spécifiez les autres propriétés du serveur de processus</span><span class="sxs-lookup"><span data-stu-id="0c548-130">Fill in the rest of the properties for the process server</span></span>

  ![Récapitulatif Ajouter un serveur de processus](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|<span data-ttu-id="0c548-132">**Nom du champ**</span><span class="sxs-lookup"><span data-stu-id="0c548-132">**Field Name**</span></span>|<span data-ttu-id="0c548-133">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="0c548-133">**Value**</span></span>|
|-|-|
|<span data-ttu-id="0c548-134">Nom du serveur</span><span class="sxs-lookup"><span data-stu-id="0c548-134">Server Name</span></span>|<span data-ttu-id="0c548-135">Nom d’affichage et nom d’hôte de la machine virtuelle de votre serveur processus</span><span class="sxs-lookup"><span data-stu-id="0c548-135">Display name & Host name for your process server virtual machine</span></span>|
| <span data-ttu-id="0c548-136">User Name</span><span class="sxs-lookup"><span data-stu-id="0c548-136">User Name</span></span>|<span data-ttu-id="0c548-137">Nom d’utilisateur qui devient un administrateur sur cette machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="0c548-137">A user name that becomes an Administrator on that virtual machine</span></span>|
|<span data-ttu-id="0c548-138">Compte de stockage</span><span class="sxs-lookup"><span data-stu-id="0c548-138">Storage Account</span></span>|<span data-ttu-id="0c548-139">Nom du compte de stockage où est placé le disque virtuel de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="0c548-139">Name of the Storage Account where the virtual machine's virtual disk's are placed</span></span>|
|<span data-ttu-id="0c548-140">Sous-réseau</span><span class="sxs-lookup"><span data-stu-id="0c548-140">Subnet</span></span>|<span data-ttu-id="0c548-141">Sous-réseau du réseau virtuel Azure auquel les machines virtuelles sont connectées</span><span class="sxs-lookup"><span data-stu-id="0c548-141">The subnet of the Azure VNet to which the virtual machine is connected</span></span>|
| <span data-ttu-id="0c548-142">Adresse IP</span><span class="sxs-lookup"><span data-stu-id="0c548-142">IP Address</span></span>|<span data-ttu-id="0c548-143">Adresse IP que le serveur de processus est supposé utiliser au démarrage</span><span class="sxs-lookup"><span data-stu-id="0c548-143">IP Address that you would like the process server to assume once it boots up</span></span>|
5. <span data-ttu-id="0c548-144">Cliquez sur le bouton OK pour commencer le déploiement de la machine virtuelle du serveur de processus.</span><span class="sxs-lookup"><span data-stu-id="0c548-144">Click the OK button to start deploying the process server virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="0c548-145">Pour pouvoir utiliser ce serveur de processus pour la restauration automatique, vous devez l’inscrire auprès du serveur de configuration local.</span><span class="sxs-lookup"><span data-stu-id="0c548-145">To be able to use this process server for failback, you need to register it with the on-premises configuration server.</span></span>

## <a name="registering-the-process-server-running-in-azure-to-a-configuration-server-running-on-premises"></a><span data-ttu-id="0c548-146">Inscription du serveur de processus (en cours d’exécution dans Azure) auprès d’un serveur de Configuration (en cours d’exécution en local)</span><span class="sxs-lookup"><span data-stu-id="0c548-146">Registering the process server (running in Azure) to a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-the-process-server-to-latest-version"></a><span data-ttu-id="0c548-147">Mise à niveau du serveur de processus avec la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="0c548-147">Upgrading the process server to latest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-the-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="0c548-148">Désinscription du serveur de processus (en cours d’exécution dans Azure) d’un serveur de Configuration (en cours d’exécution en local)</span><span class="sxs-lookup"><span data-stu-id="0c548-148">Unregistering the process server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
