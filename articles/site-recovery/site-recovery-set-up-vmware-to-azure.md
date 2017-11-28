---
title: "Configurer l’environnement source (VMware vers Azure) | Microsoft Docs"
description: "Cet article décrit la procédure de configuration de votre environnement local de manière à lancer la réplication de machines virtuelles VMware dans Azure."
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
ms.openlocfilehash: a2fabc56463c8cbf0b8a76b7a84369ed8e535486
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-the-source-environment-vmware-to-azure"></a><span data-ttu-id="54da9-103">Configurer l’environnement source (VMware vers Azure)</span><span class="sxs-lookup"><span data-stu-id="54da9-103">Set up the source environment (VMware to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="54da9-104">VMware vers Azure</span><span class="sxs-lookup"><span data-stu-id="54da9-104">VMware to Azure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="54da9-105">Physique vers Azure</span><span class="sxs-lookup"><span data-stu-id="54da9-105">Physical to Azure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="54da9-106">Cet article décrit la procédure de configuration de votre environnement local de manière à lancer la réplication de machines virtuelles exécutées sur VMware dans Azure.</span><span class="sxs-lookup"><span data-stu-id="54da9-106">This article describes how to set up your on-premises environment to start replicating virtual machines running on VMware to Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54da9-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="54da9-107">Prerequisites</span></span>

<span data-ttu-id="54da9-108">Cet article suppose que vous avez déjà créé les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="54da9-108">The article assumes that you have already created:</span></span>
- <span data-ttu-id="54da9-109">Un coffre Recovery Services dans le [portail Azure](http://portal.azure.com "portail Azure").</span><span class="sxs-lookup"><span data-stu-id="54da9-109">A Recovery Services Vault in the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="54da9-110">Un compte dédié dans votre serveur VMware vCenter qui peut être utilisé pour la [découverte automatique](./site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="54da9-110">A dedicated account in your VMware vCenter that can be used for [automatic discovery](./site-recovery-vmware-to-azure.md).</span></span>
- <span data-ttu-id="54da9-111">Une machine virtuelle sur laquelle installer le serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="54da9-111">A virtual machine on which to install the configuration server.</span></span>

## <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="54da9-112">Configuration minimale requise du serveur</span><span class="sxs-lookup"><span data-stu-id="54da9-112">Configuration server minimum requirements</span></span>
<span data-ttu-id="54da9-113">Le logiciel du serveur de configuration doit être déployé sur une machine virtuelle VMware à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="54da9-113">The configuration server software should be deployed on a highly available VMware virtual machine.</span></span> <span data-ttu-id="54da9-114">Le tableau suivant présente la configuration minimale requise pour le matériel, le logiciel et le réseau pour un serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="54da9-114">The following table lists the minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="54da9-115">Les serveurs proxy HTTPS ne sont pas pris en charge par le serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="54da9-115">HTTPS-based proxy servers are not supported by the configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="54da9-116">Sélectionner vos objectifs en matière de protection</span><span class="sxs-lookup"><span data-stu-id="54da9-116">Choose your protection goals</span></span>

1. <span data-ttu-id="54da9-117">Dans le portail Azure, accédez au panneau des coffres **Recovery Services**, puis sélectionnez votre coffre.</span><span class="sxs-lookup"><span data-stu-id="54da9-117">In the Azure portal, go to the **Recovery Services** vault blade and select your vault.</span></span>
2. <span data-ttu-id="54da9-118">Dans le menu Ressource du coffre, sélectionnez **Prise en main** > **Site Recovery** > **Étape 1 : préparer l’infrastructure** > **Objectif de protection**.</span><span class="sxs-lookup"><span data-stu-id="54da9-118">On the resource menu of the vault, go to **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Sélectionner des objectifs](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. <span data-ttu-id="54da9-120">Dans **Objectif de la protection**, sélectionnez **Vers Azure** puis choisissez **Oui, avec hyperviseur vSphere VMware**.</span><span class="sxs-lookup"><span data-stu-id="54da9-120">In **Protection goal**, select **To Azure**, and choose **Yes, with VMware vSphere Hypervisor**.</span></span> <span data-ttu-id="54da9-121">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="54da9-121">Then click **OK**.</span></span>

    ![Sélectionner des objectifs](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-the-source-environment"></a><span data-ttu-id="54da9-123">Configurer l’environnement source</span><span class="sxs-lookup"><span data-stu-id="54da9-123">Set up the source environment</span></span>
<span data-ttu-id="54da9-124">La configuration de l’environnement implique deux activités principales :</span><span class="sxs-lookup"><span data-stu-id="54da9-124">Setting up the source environment involves two main activities:</span></span>

- <span data-ttu-id="54da9-125">Installer et inscrire un serveur de configuration avec Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="54da9-125">Install and register a configuration server with Site Recovery.</span></span>
- <span data-ttu-id="54da9-126">Découvrir vos machines virtuelles locales par la connexion de Site Recovery à vos hôtes VMware vCenter ou vSphere EXSi locaux.</span><span class="sxs-lookup"><span data-stu-id="54da9-126">Discover your on-premises virtual machines by connecting Site Recovery to your on-premises VMware vCenter or vSphere EXSi hosts.</span></span>

### <a name="step-1-install-and-register-a-configuration-server"></a><span data-ttu-id="54da9-127">Étape 1 : Installer et inscrire un serveur de configuration</span><span class="sxs-lookup"><span data-stu-id="54da9-127">Step 1: Install and register a configuration server</span></span>

1. <span data-ttu-id="54da9-128">Cliquez sur **Étape 1 : Préparer l’infrastructure** > **Source**.</span><span class="sxs-lookup"><span data-stu-id="54da9-128">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span> <span data-ttu-id="54da9-129">Dans **Préparer la source**, si vous n’avez pas de serveur de configuration, cliquez sur **+Serveur de configuration** afin d’en ajouter un.</span><span class="sxs-lookup"><span data-stu-id="54da9-129">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** to add one.</span></span>

    ![Configurer la source](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. <span data-ttu-id="54da9-131">Dans le panneau **Ajouter un serveur**, vérifiez que **Serveur de configuration** s’affiche dans **Type de serveur**.</span><span class="sxs-lookup"><span data-stu-id="54da9-131">On the **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="54da9-132">Téléchargez le fichier d’installation unifiée de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="54da9-132">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="54da9-133">Téléchargez la clé d’inscription du coffre.</span><span class="sxs-lookup"><span data-stu-id="54da9-133">Download the vault registration key.</span></span> <span data-ttu-id="54da9-134">Vous avez besoin de la clé d’inscription lorsque vous exécutez le programme d’installation unifiée.</span><span class="sxs-lookup"><span data-stu-id="54da9-134">You need the registration key when you run Unified Setup.</span></span> <span data-ttu-id="54da9-135">Une fois générée, la clé reste valide pendant 5 jours.</span><span class="sxs-lookup"><span data-stu-id="54da9-135">The key is valid for five days after you generate it.</span></span>

    ![Configurer la source](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. <span data-ttu-id="54da9-137">Sur la machine qui vous sert de serveur de configuration, exécutez le **programme d’installation unifiée Azure Site Recovery** afin d’installer le serveur de configuration, le serveur de processus et le serveur cible maître.</span><span class="sxs-lookup"><span data-stu-id="54da9-137">On the machine you’re using as the configuration server, run **Azure Site Recovery Unified Setup** to install the configuration server, the process server, and the master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="54da9-138">Exécuter le programme d’installation unifiée Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="54da9-138">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="54da9-139">L’inscription du serveur de configuration échoue si l’horloge système de vos ordinateurs diffère de l’heure locale de plus de cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="54da9-139">Configuration server registration fails if the time on your computer's system clock differs from local time by more than five minutes.</span></span> <span data-ttu-id="54da9-140">Synchronisez votre horloge système avec un [serveur de temps](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) avant de commencer l’installation.</span><span class="sxs-lookup"><span data-stu-id="54da9-140">Synchronize your system clock with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting the installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="54da9-141">Le serveur de configuration peut être installé via la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="54da9-141">The configuration server can be installed via command line.</span></span> <span data-ttu-id="54da9-142">Pour plus d’informations, consultez [Installation du serveur de configuration à l’aide des outils en ligne de commande](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="54da9-142">For more information, see [Installing the configuration server using Command-line tools](http://aka.ms/installconfigsrv).</span></span>

#### <a name="add-the-vmware-account-for-automatic-discovery"></a><span data-ttu-id="54da9-143">Ajouter le compte VMware pour la découverte automatique</span><span class="sxs-lookup"><span data-stu-id="54da9-143">Add the VMware account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a><span data-ttu-id="54da9-144">Étape 2 : Ajouter un serveur vCenter</span><span class="sxs-lookup"><span data-stu-id="54da9-144">Step 2: Add a vCenter</span></span>
<span data-ttu-id="54da9-145">Pour permettre à Azure Site Recovery de détecter les machines virtuelles en cours d’exécution dans votre environnement local, vous devez connecter votre serveur VMware vCenter ou vos hôtes ESXi vSphere à Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="54da9-145">To allow Azure Site Recovery to discover virtual machines running in your on-premises environment, you need to connect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span>

<span data-ttu-id="54da9-146">Sélectionnez **+vCenter** pour connecter un serveur VMware vCenter ou un ordinateur hôte VMware vSphere ESXi.</span><span class="sxs-lookup"><span data-stu-id="54da9-146">Select **+vCenter** to start connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a><span data-ttu-id="54da9-147">Problèmes courants</span><span class="sxs-lookup"><span data-stu-id="54da9-147">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="54da9-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="54da9-148">Next steps</span></span>
<span data-ttu-id="54da9-149">[Configurez votre environnement cible](./site-recovery-prepare-target-vmware-to-azure.md) dans Azure.</span><span class="sxs-lookup"><span data-stu-id="54da9-149">[Set up your target environment](./site-recovery-prepare-target-vmware-to-azure.md) in Azure.</span></span>
