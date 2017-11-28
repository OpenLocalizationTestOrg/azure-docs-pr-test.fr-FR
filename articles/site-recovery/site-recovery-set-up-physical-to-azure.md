---
title: "Configurer l’environnement source hello (tooAzure serveurs physiques) | Documents Microsoft"
description: "Cet article décrit comment tooset de votre toostart d’environnement local réplication des serveurs physiques exécutant Windows ou Linux dans Azure."
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
ms.openlocfilehash: d4702265bf36910015685d2bba99d6e577531bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-physical-server-tooazure"></a><span data-ttu-id="f485f-103">Configurer l’environnement source hello (serveur physique tooAzure)</span><span class="sxs-lookup"><span data-stu-id="f485f-103">Set up hello source environment (physical server tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f485f-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="f485f-104">VMware tooAzure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="f485f-105">TooAzure physique</span><span class="sxs-lookup"><span data-stu-id="f485f-105">Physical tooAzure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="f485f-106">Cet article décrit comment tooset de votre toostart d’environnement local réplication des serveurs physiques exécutant Windows ou Linux dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f485f-106">This article describes how tooset up your on-premises environment toostart replicating physical servers running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f485f-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f485f-107">Prerequisites</span></span>

<span data-ttu-id="f485f-108">article de Hello suppose que vous avez déjà :</span><span class="sxs-lookup"><span data-stu-id="f485f-108">hello article assumes that you already have:</span></span>
1. <span data-ttu-id="f485f-109">Un coffre Recovery Services Bonjour [portail Azure](http://portal.azure.com "portail Azure").</span><span class="sxs-lookup"><span data-stu-id="f485f-109">A Recovery Services vault in hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
3. <span data-ttu-id="f485f-110">Un ordinateur physique sur le serveur de configuration tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="f485f-110">A physical computer on which tooinstall hello configuration server.</span></span>

### <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="f485f-111">Configuration minimale requise du serveur</span><span class="sxs-lookup"><span data-stu-id="f485f-111">Configuration server minimum requirements</span></span>
<span data-ttu-id="f485f-112">Hello tableau suivant répertorie la configuration matérielle minimale hello, de logiciels et de configuration réseau requise pour un serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="f485f-112">hello following table lists hello minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="f485f-113">Serveurs proxy de basée sur HTTPS ne sont pas pris en charge par le serveur de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="f485f-113">HTTPS-based proxy servers are not supported by hello configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="f485f-114">Sélectionner vos objectifs en matière de protection</span><span class="sxs-lookup"><span data-stu-id="f485f-114">Choose your protection goals</span></span>

1. <span data-ttu-id="f485f-115">Bonjour portail Azure, accédez à toohello **Services de récupération** panneau les coffres et sélectionnez votre archivage.</span><span class="sxs-lookup"><span data-stu-id="f485f-115">In hello Azure portal, go toohello **Recovery Services** vaults blade and select your vault.</span></span>
2. <span data-ttu-id="f485f-116">Bonjour **ressource** menu du coffre de hello, cliquez sur **mise en route** > **Site Recovery** > **étape 1 : préparer Infrastructure** > **objectif de Protection**.</span><span class="sxs-lookup"><span data-stu-id="f485f-116">In hello **Resource** menu of hello vault, click **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Sélectionner des objectifs](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. <span data-ttu-id="f485f-118">Dans **objectif de Protection**, sélectionnez **tooAzure** et **non virtualisé,**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f485f-118">In **Protection goal**, select **tooAzure** and **Not virtualized/Other**, and then click **OK**.</span></span>

    ![Sélectionner des objectifs](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="f485f-120">Configurer l’environnement source hello</span><span class="sxs-lookup"><span data-stu-id="f485f-120">Set up hello source environment</span></span>

1. <span data-ttu-id="f485f-121">Dans **Prepare source**, si vous n’avez pas un serveur de configuration, cliquez sur **+ serveur de Configuration** tooadd une.</span><span class="sxs-lookup"><span data-stu-id="f485f-121">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** tooadd one.</span></span>

  ![Configurer la source](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. <span data-ttu-id="f485f-123">Bonjour **ajouter un serveur** panneau, vérifiez que **serveur de Configuration** s’affiche dans **type de serveur**.</span><span class="sxs-lookup"><span data-stu-id="f485f-123">In hello **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="f485f-124">Télécharger le fichier d’installation le programme d’installation de Site Recovery unifiée hello.</span><span class="sxs-lookup"><span data-stu-id="f485f-124">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="f485f-125">Télécharger la clé d’inscription du coffre hello.</span><span class="sxs-lookup"><span data-stu-id="f485f-125">Download hello vault registration key.</span></span> <span data-ttu-id="f485f-126">Vous devez la clé d’inscription de hello lorsque vous exécutez le programme d’installation unifiée.</span><span class="sxs-lookup"><span data-stu-id="f485f-126">You need hello registration key when you run Unified Setup.</span></span> <span data-ttu-id="f485f-127">clé de Hello est valide pendant cinq jours après que l’avoir généré.</span><span class="sxs-lookup"><span data-stu-id="f485f-127">hello key is valid for five days after you generate it.</span></span>

    ![Configurer la source](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. <span data-ttu-id="f485f-129">Sur la machine hello vous utilisez en tant que serveur de configuration hello, exécutez **installation unifiée d’Azure Site Recovery** serveur de configuration tooinstall hello, serveur de processus hello et maître de hello de serveur ciblent.</span><span class="sxs-lookup"><span data-stu-id="f485f-129">On hello machine you’re using as hello configuration server, run **Azure Site Recovery Unified Setup** tooinstall hello configuration server, hello process server, and hello master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="f485f-130">Exécuter le programme d’installation unifiée Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="f485f-130">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="f485f-131">L’inscription du serveur de configuration échoue si les temps de hello sur l’horloge système de votre ordinateur est plus de cinq minutes sur une heure locale.</span><span class="sxs-lookup"><span data-stu-id="f485f-131">Configuration server registration fails if hello time on your computer's system clock is more than five minutes off of local time.</span></span> <span data-ttu-id="f485f-132">Synchroniser l’horloge de votre système avec un [serveur de temps](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) avant de commencer l’installation de hello.</span><span class="sxs-lookup"><span data-stu-id="f485f-132">Synchronize your system clock with a [time server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting hello installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="f485f-133">serveur de configuration Hello peut être installé via une ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="f485f-133">hello configuration server can be installed via a command line.</span></span> <span data-ttu-id="f485f-134">Pour plus d’informations, consultez [Installation du serveur de configuration à l’aide des outils en ligne de commande](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="f485f-134">For more information, see [Installing configuration server using command-line tools](http://aka.ms/installconfigsrv).</span></span>


## <a name="common-issues"></a><span data-ttu-id="f485f-135">Problèmes courants</span><span class="sxs-lookup"><span data-stu-id="f485f-135">Common issues</span></span>

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="f485f-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f485f-136">Next steps</span></span>

<span data-ttu-id="f485f-137">L’étape suivante consiste en la [configuration de votre environnement cible](./site-recovery-prepare-target-physical-to-azure.md) dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f485f-137">Next step involves [setting up your target environment](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span></span>
