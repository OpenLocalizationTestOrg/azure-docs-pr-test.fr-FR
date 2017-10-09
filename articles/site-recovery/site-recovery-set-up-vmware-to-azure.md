---
title: "Configurer l’environnement source hello (tooAzure VMware) | Documents Microsoft"
description: "Cet article décrit comment tooset de votre toostart d’environnement local Réplication VMware virtual machines tooAzure."
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
ms.openlocfilehash: cbeeffc1061b11223e12ff3e237fa7e55b999aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-vmware-tooazure"></a><span data-ttu-id="439b8-103">Configurer l’environnement source hello (tooAzure VMware)</span><span class="sxs-lookup"><span data-stu-id="439b8-103">Set up hello source environment (VMware tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="439b8-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="439b8-104">VMware tooAzure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="439b8-105">TooAzure physique</span><span class="sxs-lookup"><span data-stu-id="439b8-105">Physical tooAzure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="439b8-106">Cet article décrit comment tooset de votre toostart d’environnement local réplication virtual machines en cours d’exécution sur VMware tooAzure.</span><span class="sxs-lookup"><span data-stu-id="439b8-106">This article describes how tooset up your on-premises environment toostart replicating virtual machines running on VMware tooAzure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="439b8-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="439b8-107">Prerequisites</span></span>

<span data-ttu-id="439b8-108">article de Hello part du principe que vous avez déjà créé :</span><span class="sxs-lookup"><span data-stu-id="439b8-108">hello article assumes that you have already created:</span></span>
- <span data-ttu-id="439b8-109">Un coffre Recovery Services Bonjour [portail Azure](http://portal.azure.com "portail Azure").</span><span class="sxs-lookup"><span data-stu-id="439b8-109">A Recovery Services Vault in hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="439b8-110">Un compte dédié dans votre serveur VMware vCenter qui peut être utilisé pour la [découverte automatique](./site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="439b8-110">A dedicated account in your VMware vCenter that can be used for [automatic discovery](./site-recovery-vmware-to-azure.md).</span></span>
- <span data-ttu-id="439b8-111">Un ordinateur virtuel sur le serveur de configuration tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="439b8-111">A virtual machine on which tooinstall hello configuration server.</span></span>

## <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="439b8-112">Configuration minimale requise du serveur</span><span class="sxs-lookup"><span data-stu-id="439b8-112">Configuration server minimum requirements</span></span>
<span data-ttu-id="439b8-113">logiciel de serveur de configuration Hello doit être déployé sur un ordinateur virtuel de VMware hautement disponible.</span><span class="sxs-lookup"><span data-stu-id="439b8-113">hello configuration server software should be deployed on a highly available VMware virtual machine.</span></span> <span data-ttu-id="439b8-114">Hello tableau suivant répertorie la configuration matérielle minimale hello, de logiciels et de configuration réseau requise pour un serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="439b8-114">hello following table lists hello minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="439b8-115">Serveurs proxy de basée sur HTTPS ne sont pas pris en charge par le serveur de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="439b8-115">HTTPS-based proxy servers are not supported by hello configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="439b8-116">Sélectionner vos objectifs en matière de protection</span><span class="sxs-lookup"><span data-stu-id="439b8-116">Choose your protection goals</span></span>

1. <span data-ttu-id="439b8-117">Bonjour portail Azure, accédez à toohello **Services de récupération** Panneau de coffre et sélectionnez votre archivage.</span><span class="sxs-lookup"><span data-stu-id="439b8-117">In hello Azure portal, go toohello **Recovery Services** vault blade and select your vault.</span></span>
2. <span data-ttu-id="439b8-118">Sur le menu de ressource hello de coffre de hello, accédez trop**mise en route** > **Site Recovery** > **étape 1 : préparer l’Infrastructure**  >  **Objectif de protection**.</span><span class="sxs-lookup"><span data-stu-id="439b8-118">On hello resource menu of hello vault, go too**Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Sélectionner des objectifs](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. <span data-ttu-id="439b8-120">Dans **objectif de Protection**, sélectionnez **tooAzure**, puis choisissez **Oui, avec l’hyperviseur VMware vSphere**.</span><span class="sxs-lookup"><span data-stu-id="439b8-120">In **Protection goal**, select **tooAzure**, and choose **Yes, with VMware vSphere Hypervisor**.</span></span> <span data-ttu-id="439b8-121">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="439b8-121">Then click **OK**.</span></span>

    ![Sélectionner des objectifs](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="439b8-123">Configurer l’environnement source hello</span><span class="sxs-lookup"><span data-stu-id="439b8-123">Set up hello source environment</span></span>
<span data-ttu-id="439b8-124">Configuration de l’environnement source hello implique deux activités principales :</span><span class="sxs-lookup"><span data-stu-id="439b8-124">Setting up hello source environment involves two main activities:</span></span>

- <span data-ttu-id="439b8-125">Installer et inscrire un serveur de configuration avec Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="439b8-125">Install and register a configuration server with Site Recovery.</span></span>
- <span data-ttu-id="439b8-126">Découvrir vos machines virtuelles de local en vous connectant le Site Recovery tooyour local VMware vCenter ou vSphere EXSi hôtes.</span><span class="sxs-lookup"><span data-stu-id="439b8-126">Discover your on-premises virtual machines by connecting Site Recovery tooyour on-premises VMware vCenter or vSphere EXSi hosts.</span></span>

### <a name="step-1-install-and-register-a-configuration-server"></a><span data-ttu-id="439b8-127">Étape 1 : Installer et inscrire un serveur de configuration</span><span class="sxs-lookup"><span data-stu-id="439b8-127">Step 1: Install and register a configuration server</span></span>

1. <span data-ttu-id="439b8-128">Cliquez sur **Étape 1 : Préparer l’infrastructure** > **Source**.</span><span class="sxs-lookup"><span data-stu-id="439b8-128">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span> <span data-ttu-id="439b8-129">Dans **Prepare source**, si vous n’avez pas un serveur de configuration, cliquez sur **+ serveur de Configuration** tooadd une.</span><span class="sxs-lookup"><span data-stu-id="439b8-129">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** tooadd one.</span></span>

    ![Configurer la source](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. <span data-ttu-id="439b8-131">Sur hello **ajouter un serveur** panneau, vérifiez que **serveur de Configuration** s’affiche dans **type de serveur**.</span><span class="sxs-lookup"><span data-stu-id="439b8-131">On hello **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="439b8-132">Télécharger le fichier d’installation le programme d’installation de Site Recovery unifiée hello.</span><span class="sxs-lookup"><span data-stu-id="439b8-132">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="439b8-133">Télécharger la clé d’inscription du coffre hello.</span><span class="sxs-lookup"><span data-stu-id="439b8-133">Download hello vault registration key.</span></span> <span data-ttu-id="439b8-134">Vous devez la clé d’inscription de hello lorsque vous exécutez le programme d’installation unifiée.</span><span class="sxs-lookup"><span data-stu-id="439b8-134">You need hello registration key when you run Unified Setup.</span></span> <span data-ttu-id="439b8-135">clé de Hello est valide pendant cinq jours après que l’avoir généré.</span><span class="sxs-lookup"><span data-stu-id="439b8-135">hello key is valid for five days after you generate it.</span></span>

    ![Configurer la source](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. <span data-ttu-id="439b8-137">Sur la machine hello vous utilisez en tant que serveur de configuration hello, exécutez **installation unifiée d’Azure Site Recovery** serveur de configuration tooinstall hello, serveur de processus hello et maître de hello de serveur ciblent.</span><span class="sxs-lookup"><span data-stu-id="439b8-137">On hello machine you’re using as hello configuration server, run **Azure Site Recovery Unified Setup** tooinstall hello configuration server, hello process server, and hello master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="439b8-138">Exécuter le programme d’installation unifiée Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="439b8-138">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="439b8-139">L’inscription du serveur de configuration échoue si le temps hello sur l’horloge système de votre ordinateur diffère de l’heure locale de plus de cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="439b8-139">Configuration server registration fails if hello time on your computer's system clock differs from local time by more than five minutes.</span></span> <span data-ttu-id="439b8-140">Synchroniser l’horloge de votre système avec un [serveur de temps](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) avant de commencer l’installation de hello.</span><span class="sxs-lookup"><span data-stu-id="439b8-140">Synchronize your system clock with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting hello installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="439b8-141">serveur de configuration Hello peut être installé via la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="439b8-141">hello configuration server can be installed via command line.</span></span> <span data-ttu-id="439b8-142">Pour plus d’informations, consultez [installation à l’aide des outils de ligne de commande de server configuration hello](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="439b8-142">For more information, see [Installing hello configuration server using Command-line tools](http://aka.ms/installconfigsrv).</span></span>

#### <a name="add-hello-vmware-account-for-automatic-discovery"></a><span data-ttu-id="439b8-143">Ajouter compte de VMware hello pour la découverte automatique</span><span class="sxs-lookup"><span data-stu-id="439b8-143">Add hello VMware account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a><span data-ttu-id="439b8-144">Étape 2 : Ajouter un serveur vCenter</span><span class="sxs-lookup"><span data-stu-id="439b8-144">Step 2: Add a vCenter</span></span>
<span data-ttu-id="439b8-145">tooallow Azure Site Recovery toodiscover machines virtuelles en cours d’exécution dans votre environnement local, vous devez tooconnect votre serveur VMware vCenter ou les ordinateurs hôtes ESXi vSphere avec Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="439b8-145">tooallow Azure Site Recovery toodiscover virtual machines running in your on-premises environment, you need tooconnect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span>

<span data-ttu-id="439b8-146">Sélectionnez **+ vCenter** toostart connecter un serveur VMware vCenter ou un hôte VMware vSphere ESXi.</span><span class="sxs-lookup"><span data-stu-id="439b8-146">Select **+vCenter** toostart connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a><span data-ttu-id="439b8-147">Problèmes courants</span><span class="sxs-lookup"><span data-stu-id="439b8-147">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="439b8-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="439b8-148">Next steps</span></span>
<span data-ttu-id="439b8-149">[Configurez votre environnement cible](./site-recovery-prepare-target-vmware-to-azure.md) dans Azure.</span><span class="sxs-lookup"><span data-stu-id="439b8-149">[Set up your target environment](./site-recovery-prepare-target-vmware-to-azure.md) in Azure.</span></span>
