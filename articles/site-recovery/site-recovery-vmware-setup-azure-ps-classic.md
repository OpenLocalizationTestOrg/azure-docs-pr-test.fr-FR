---
title: " Gérer un serveur de processus en cours d’exécution dans Azure (Classic) | Microsoft Docs"
description: "Cet article décrit comment tooset d’une restauration automatique du processus Server(Classic) dans Azure."
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
ms.openlocfilehash: eadcc0236c77c9ebbbc885c4a7ee81098f1f4e72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a><span data-ttu-id="ed594-103">Gérer un serveur de processus en cours d’exécution dans Azure (Classic)</span><span class="sxs-lookup"><span data-stu-id="ed594-103">Manage a Process Server running in Azure (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ed594-104">Azure Classic </span><span class="sxs-lookup"><span data-stu-id="ed594-104">Azure Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [<span data-ttu-id="ed594-105">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="ed594-105">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

<span data-ttu-id="ed594-106">Lors de la restauration automatique, il est recommandé de toodeploy serveur de traitement dans Azure s’il existe une latence élevée entre hello réseau virtuel Azure et votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="ed594-106">During failback, it is recommended toodeploy Process Server in Azure if there is high latency between hello Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="ed594-107">Cet article décrit comment vous pouvez définir, configurer et gérer des serveurs de traitement hello s’exécutant dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ed594-107">This article describes how you can set up, configure, and manage hello process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="ed594-108">Cet article est toobe utilisé si vous avez utilisé classique en tant que modèle de déploiement hello pour les ordinateurs virtuels de hello pendant le basculement.</span><span class="sxs-lookup"><span data-stu-id="ed594-108">This article is toobe used if you used Classic as hello deployment model for hello virtual machines during failover.</span></span> <span data-ttu-id="ed594-109">Si vous avez utilisé le Gestionnaire de ressources comme hello des étapes de déploiement modèle suivent hello dans [comment tooset & Mettre à configurer un serveur de processus de restauration automatique (Resource Manager).](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="ed594-109">If you used Resource Manager as hello deployment model follow hello steps in [How tooset up & configure a Failback Process Server (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed594-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ed594-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="ed594-111">Déployer un serveur de processus dans Azure</span><span class="sxs-lookup"><span data-stu-id="ed594-111">Deploy a Process Server on Azure</span></span>

1. <span data-ttu-id="ed594-112">Dans Azure Marketplace, créez un ordinateur virtuel à l’aide de hello **processus serveur V2 de Microsoft Azure Site Recovery**</span><span class="sxs-lookup"><span data-stu-id="ed594-112">In Azure Marketplace, create a virtual machine using hello **Microsoft Azure Site Recovery Process Server V2**</span></span> </br>
    <span data-ttu-id="ed594-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span><span class="sxs-lookup"><span data-stu-id="ed594-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span></span>
2. <span data-ttu-id="ed594-114">Vérifiez que vous sélectionnez le modèle de déploiement hello en tant que **classique**</span><span class="sxs-lookup"><span data-stu-id="ed594-114">Ensure that you select hello deployment model as **Classic**</span></span> </br><span data-ttu-id="ed594-115">
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span><span class="sxs-lookup"><span data-stu-id="ed594-115">
![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span></span>
3. <span data-ttu-id="ed594-116">Dans l’Assistant de création de machine virtuelle hello > Paramètres de base, veillez à sélectionner toowhere d’abonnement et l’emplacement hello vous hello machines virtuelles ayant basculé.</span><span class="sxs-lookup"><span data-stu-id="ed594-116">In hello Create virtual machine wizard > Basic Settings, ensure you select hello Subscription and Location toowhere you failed over hello virtual machines.</span></span></br><span data-ttu-id="ed594-117">
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span><span class="sxs-lookup"><span data-stu-id="ed594-117">
![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span></span>
4. <span data-ttu-id="ed594-118">Vérifiez que l’ordinateur virtuel hello est connecté hello de toowhich toohello réseau virtuel Azure a échoué sur l’ordinateur virtuel est connecté.</span><span class="sxs-lookup"><span data-stu-id="ed594-118">Ensure that hello virtual machine is connected toohello Azure Virtual Network toowhich hello failed over virtual machine is connected.</span></span></br><span data-ttu-id="ed594-119">
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span><span class="sxs-lookup"><span data-stu-id="ed594-119">
![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span></span>
5. <span data-ttu-id="ed594-120">Une fois que la machine virtuelle de processus serveur hello est configuré, vous devez toolog dans et l’inscrivez auprès de hello serveur de Configuration.</span><span class="sxs-lookup"><span data-stu-id="ed594-120">Once hello Process Server virtual machine is provisioned, you need toolog in and register it with hello Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="ed594-121">toouse en mesure de toobe ce serveur de processus pour la restauration automatique, vous devez tooregister avec le serveur de configuration local hello.</span><span class="sxs-lookup"><span data-stu-id="ed594-121">toobe able toouse this Process Server for failback, you need tooregister it with hello on-premises configuration server.</span></span>

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a><span data-ttu-id="ed594-122">L’inscription de serveur de processus (en cours d’exécution dans Azure) de hello tooa Configuration serveur (local)</span><span class="sxs-lookup"><span data-stu-id="ed594-122">Registering hello Process Server (running in Azure) tooa Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a><span data-ttu-id="ed594-123">La mise à niveau de version de toolatest hello serveur de processus.</span><span class="sxs-lookup"><span data-stu-id="ed594-123">Upgrading hello Process Server toolatest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="ed594-124">Hello Désinscription du serveur de processus (en cours d’exécution dans Azure) à partir d’un serveur de Configuration (en cours d’exécution locale)</span><span class="sxs-lookup"><span data-stu-id="ed594-124">Unregistering hello Process Server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
