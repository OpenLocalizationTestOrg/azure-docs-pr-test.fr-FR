---
title: " Gérer un serveur de processus en cours d’exécution dans Azure (Classic) | Microsoft Docs"
description: Cet article explique comment configurer un serveur de processus de restauration automatique dans Azure (Classic).
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
ms.openlocfilehash: 479bbd207bcf715138c340f9e4d2634120bab85c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a><span data-ttu-id="e0f70-103">Gérer un serveur de processus en cours d’exécution dans Azure (Classic)</span><span class="sxs-lookup"><span data-stu-id="e0f70-103">Manage a Process Server running in Azure (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e0f70-104">Azure Classic </span><span class="sxs-lookup"><span data-stu-id="e0f70-104">Azure Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [<span data-ttu-id="e0f70-105">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="e0f70-105">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

<span data-ttu-id="e0f70-106">Lors de la restauration automatique, il est recommandé de déployer le serveur de processus dans Azure s’il existe une latence élevée entre le réseau virtuel Azure et votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="e0f70-106">During failback, it is recommended to deploy Process Server in Azure if there is high latency between the Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="e0f70-107">Cet article explique comment installer, configurer et gérer les serveurs de processus en cours d’exécution dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e0f70-107">This article describes how you can set up, configure, and manage the process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="e0f70-108">Consultez cet article si vous avez utilisé le déploiement Classic comme modèle de déploiement pour les machines virtuelles lors du basculement.</span><span class="sxs-lookup"><span data-stu-id="e0f70-108">This article is to be used if you used Classic as the deployment model for the virtual machines during failover.</span></span> <span data-ttu-id="e0f70-109">Si vous avez utilisé le modèle de déploiement Resource Manager, suivez les étapes de la rubrique [Guide pratique pour installer et configurer un serveur de processus de restauration automatique (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e0f70-109">If you used Resource Manager as the deployment model follow the steps in [How to set up & configure a Failback Process Server (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0f70-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e0f70-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="e0f70-111">Déployer un serveur de processus dans Azure</span><span class="sxs-lookup"><span data-stu-id="e0f70-111">Deploy a Process Server on Azure</span></span>

1. <span data-ttu-id="e0f70-112">Dans Azure Marketplace, créez une machine virtuelle à l’aide du **serveur de processus Microsoft Azure Site Recovery V2**</span><span class="sxs-lookup"><span data-stu-id="e0f70-112">In Azure Marketplace, create a virtual machine using the **Microsoft Azure Site Recovery Process Server V2**</span></span> </br>
    <span data-ttu-id="e0f70-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span><span class="sxs-lookup"><span data-stu-id="e0f70-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span></span>
2. <span data-ttu-id="e0f70-114">Veillez à sélectionner le modèle de déploiement **Classic**</span><span class="sxs-lookup"><span data-stu-id="e0f70-114">Ensure that you select the deployment model as **Classic**</span></span> </br><span data-ttu-id="e0f70-115">
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span><span class="sxs-lookup"><span data-stu-id="e0f70-115">
![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span></span>
3. <span data-ttu-id="e0f70-116">Dans l’Assistant Créer une machine virtuelle > Paramètres de base, veillez à sélectionner l’abonnement et l’emplacement où vous avez basculé les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="e0f70-116">In the Create virtual machine wizard > Basic Settings, ensure you select the Subscription and Location to where you failed over the virtual machines.</span></span></br><span data-ttu-id="e0f70-117">
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span><span class="sxs-lookup"><span data-stu-id="e0f70-117">
![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span></span>
4. <span data-ttu-id="e0f70-118">Assurez-vous que la machine virtuelle est connectée au réseau virtuel Azure auquel la machine virtuelle basculée est connectée.</span><span class="sxs-lookup"><span data-stu-id="e0f70-118">Ensure that the virtual machine is connected to the Azure Virtual Network to which the failed over virtual machine is connected.</span></span></br><span data-ttu-id="e0f70-119">
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span><span class="sxs-lookup"><span data-stu-id="e0f70-119">
![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span></span>
5. <span data-ttu-id="e0f70-120">Une fois la machine virtuelle du serveur de processus configurée, vous devez vous connecter et inscrire cette machine auprès du serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="e0f70-120">Once the Process Server virtual machine is provisioned, you need to log in and register it with the Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="e0f70-121">Pour pouvoir utiliser ce serveur de processus pour la restauration automatique, vous devez l’inscrire auprès du serveur de configuration local.</span><span class="sxs-lookup"><span data-stu-id="e0f70-121">To be able to use this Process Server for failback, you need to register it with the on-premises configuration server.</span></span>

## <a name="registering-the-process-server-running-in-azure-to-a-configuration-server-running-on-premises"></a><span data-ttu-id="e0f70-122">Inscription du serveur de processus (en cours d’exécution dans Azure) auprès d’un serveur de Configuration (en cours d’exécution en local)</span><span class="sxs-lookup"><span data-stu-id="e0f70-122">Registering the Process Server (running in Azure) to a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-the-process-server-to-latest-version"></a><span data-ttu-id="e0f70-123">Mise à niveau du serveur de processus avec la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="e0f70-123">Upgrading the Process Server to latest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-the-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="e0f70-124">Désinscription du serveur de processus (en cours d’exécution dans Azure) d’un serveur de Configuration (en cours d’exécution en local)</span><span class="sxs-lookup"><span data-stu-id="e0f70-124">Unregistering the Process Server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
