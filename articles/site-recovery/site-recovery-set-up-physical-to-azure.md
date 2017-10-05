---
title: "Configurer l’environnement source (serveurs physiques sur Azure) | Microsoft Docs"
description: "Cet article décrit comment configurer votre environnement local pour lancer la réplication des serveurs physiques exécutant Windows ou Linux dans Azure."
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
ms.openlocfilehash: 49b9d2e21dbcb612828a25f21ed4382327d6f64c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-the-source-environment-physical-server-to-azure"></a><span data-ttu-id="49b3f-103">Configurer l’environnement source (serveurs physiques sur Azure)</span><span class="sxs-lookup"><span data-stu-id="49b3f-103">Set up the source environment (physical server to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="49b3f-104">VMware vers Azure</span><span class="sxs-lookup"><span data-stu-id="49b3f-104">VMware to Azure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="49b3f-105">Physique vers Azure</span><span class="sxs-lookup"><span data-stu-id="49b3f-105">Physical to Azure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="49b3f-106">Cet article décrit comment configurer votre environnement local pour lancer la réplication des serveurs physiques exécutant Windows ou Linux dans Azure.</span><span class="sxs-lookup"><span data-stu-id="49b3f-106">This article describes how to set up your on-premises environment to start replicating physical servers running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49b3f-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="49b3f-107">Prerequisites</span></span>

<span data-ttu-id="49b3f-108">Cet article suppose que vous disposez déjà des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="49b3f-108">The article assumes that you already have:</span></span>
1. <span data-ttu-id="49b3f-109">Un coffre Recovery Services dans le [portail Azure](http://portal.azure.com "portail Azure").</span><span class="sxs-lookup"><span data-stu-id="49b3f-109">A Recovery Services vault in the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
3. <span data-ttu-id="49b3f-110">Un ordinateur physique sur lequel installer le serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="49b3f-110">A physical computer on which to install the configuration server.</span></span>

### <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="49b3f-111">Configuration minimale requise du serveur</span><span class="sxs-lookup"><span data-stu-id="49b3f-111">Configuration server minimum requirements</span></span>
<span data-ttu-id="49b3f-112">Le tableau suivant présente la configuration minimale requise pour le matériel, le logiciel et le réseau pour un serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="49b3f-112">The following table lists the minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="49b3f-113">Les serveurs proxy HTTPS ne sont pas pris en charge par le serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="49b3f-113">HTTPS-based proxy servers are not supported by the configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="49b3f-114">Sélectionner vos objectifs en matière de protection</span><span class="sxs-lookup"><span data-stu-id="49b3f-114">Choose your protection goals</span></span>

1. <span data-ttu-id="49b3f-115">Dans le portail Azure, accédez au panneau des coffres **Recovery Services**, puis sélectionnez votre coffre.</span><span class="sxs-lookup"><span data-stu-id="49b3f-115">In the Azure portal, go to the **Recovery Services** vaults blade and select your vault.</span></span>
2. <span data-ttu-id="49b3f-116">Dans le menu **Ressource** du coffre, cliquez sur **Prise en main** > **Site Recovery** > **Étape 1 : préparer l’infrastructure** > **Objectif de protection**.</span><span class="sxs-lookup"><span data-stu-id="49b3f-116">In the **Resource** menu of the vault, click **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Sélectionner des objectifs](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. <span data-ttu-id="49b3f-118">Dans la zone **Objectif de protection**, sélectionnez **To Azure** (Vers Azure) et **Non virtualisé/Autre**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="49b3f-118">In **Protection goal**, select **To Azure** and **Not virtualized/Other**, and then click **OK**.</span></span>

    ![Sélectionner des objectifs](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-the-source-environment"></a><span data-ttu-id="49b3f-120">Configurer l’environnement source</span><span class="sxs-lookup"><span data-stu-id="49b3f-120">Set up the source environment</span></span>

1. <span data-ttu-id="49b3f-121">Dans **Préparer la source**, si vous n’avez pas de serveur de configuration, cliquez sur **+Serveur de configuration** afin d’en ajouter un.</span><span class="sxs-lookup"><span data-stu-id="49b3f-121">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** to add one.</span></span>

  ![Configurer la source](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. <span data-ttu-id="49b3f-123">Dans le panneau **Ajouter un serveur**, vérifiez que **Serveur de configuration** s’affiche dans **Type de serveur**.</span><span class="sxs-lookup"><span data-stu-id="49b3f-123">In the **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="49b3f-124">Téléchargez le fichier d’installation unifiée de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="49b3f-124">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="49b3f-125">Téléchargez la clé d’inscription du coffre.</span><span class="sxs-lookup"><span data-stu-id="49b3f-125">Download the vault registration key.</span></span> <span data-ttu-id="49b3f-126">Vous avez besoin de la clé d’inscription lorsque vous exécutez le programme d’installation unifiée.</span><span class="sxs-lookup"><span data-stu-id="49b3f-126">You need the registration key when you run Unified Setup.</span></span> <span data-ttu-id="49b3f-127">Une fois générée, la clé reste valide pendant 5 jours.</span><span class="sxs-lookup"><span data-stu-id="49b3f-127">The key is valid for five days after you generate it.</span></span>

    ![Configurer la source](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. <span data-ttu-id="49b3f-129">Sur la machine qui vous sert de serveur de configuration, exécutez le **programme d’installation unifiée Azure Site Recovery** afin d’installer le serveur de configuration, le serveur de processus et le serveur cible maître.</span><span class="sxs-lookup"><span data-stu-id="49b3f-129">On the machine you’re using as the configuration server, run **Azure Site Recovery Unified Setup** to install the configuration server, the process server, and the master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="49b3f-130">Exécuter le programme d’installation unifiée Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="49b3f-130">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="49b3f-131">L’inscription du serveur de configuration échoue si l’horloge système de vos ordinateurs diffère de l’heure locale de plus de cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="49b3f-131">Configuration server registration fails if the time on your computer's system clock is more than five minutes off of local time.</span></span> <span data-ttu-id="49b3f-132">Synchronisez votre horloge système avec un [serveur de temps](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) avant de commencer l’installation.</span><span class="sxs-lookup"><span data-stu-id="49b3f-132">Synchronize your system clock with a [time server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting the installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="49b3f-133">Le serveur de configuration peut être installé via une ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="49b3f-133">The configuration server can be installed via a command line.</span></span> <span data-ttu-id="49b3f-134">Pour plus d’informations, consultez [Installation du serveur de configuration à l’aide des outils en ligne de commande](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="49b3f-134">For more information, see [Installing configuration server using command-line tools](http://aka.ms/installconfigsrv).</span></span>


## <a name="common-issues"></a><span data-ttu-id="49b3f-135">Problèmes courants</span><span class="sxs-lookup"><span data-stu-id="49b3f-135">Common issues</span></span>

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="49b3f-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="49b3f-136">Next steps</span></span>

<span data-ttu-id="49b3f-137">L’étape suivante consiste en la [configuration de votre environnement cible](./site-recovery-prepare-target-physical-to-azure.md) dans Azure.</span><span class="sxs-lookup"><span data-stu-id="49b3f-137">Next step involves [setting up your target environment](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span></span>
