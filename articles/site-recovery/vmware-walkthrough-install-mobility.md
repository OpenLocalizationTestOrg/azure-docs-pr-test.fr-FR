---
title: "aaaInstall hello service mobilité pour la réplication VMware tooAzure | Documents Microsoft"
description: "Cet article décrit comment tooinstall hello agent du service mobilité pour la réplication tooAzure VMware avec le service d’Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: d3b7bc9c4d84d13317e0b0b47adcf38e8c41d0bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-install-hello-mobility-service"></a><span data-ttu-id="4ebc8-103">Étape 10 : Installer le service de mobilité hello</span><span class="sxs-lookup"><span data-stu-id="4ebc8-103">Step 10: Install hello Mobility service</span></span>


<span data-ttu-id="4ebc8-104">Cet article décrit comment tooconfigure les paramètres de source et cible lors de la réplication locale tooAzure d’ordinateurs virtuels VMware, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4ebc8-104">This article describes how tooconfigure source and target settings when replicating on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="4ebc8-105">Hello service mobilité capture les écritures de données sur un ordinateur et les transfère de serveur de processus toohello.</span><span class="sxs-lookup"><span data-stu-id="4ebc8-105">hello Mobility service captures data writes on a machine, and forwards them toohello process server.</span></span> <span data-ttu-id="4ebc8-106">Il doit être installé sur chaque ordinateur que vous souhaitez tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4ebc8-106">It should be installed on each machine that you want tooreplicate tooAzure.</span></span>

<span data-ttu-id="4ebc8-107">Vous pouvez installer manuel de service de mobilité hello, à l’aide d’une installation push du serveur de processus de récupération de Site hello lorsque la réplication est activée, ou utiliser un outil de System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="4ebc8-107">You can install hello Mobility service manual, using a push installation from hello Site Recovery process server when replication is enabled, or use a tool System Center Configuration Manager.</span></span> <span data-ttu-id="4ebc8-108">Si vous utilisez installation push, service de hello est installé sur hello machine virtuelle lorsque la réplication est activée.</span><span class="sxs-lookup"><span data-stu-id="4ebc8-108">If you use push installation, hello service is installed on hello VM when replication is enabled.</span></span>

<span data-ttu-id="4ebc8-109">Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="4ebc8-109">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="4ebc8-110">Installer manuellement</span><span class="sxs-lookup"><span data-stu-id="4ebc8-110">Install manually</span></span>

1. <span data-ttu-id="4ebc8-111">Vérifiez hello [conditions préalables](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) pour l’installation manuelle.</span><span class="sxs-lookup"><span data-stu-id="4ebc8-111">Check hello [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="4ebc8-112">Suivez [ces instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) pour l’installation manuelle à l’aide du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="4ebc8-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using hello portal.</span></span>
3. <span data-ttu-id="4ebc8-113">Si vous préférez tooinstall à partir de la ligne de commande hello, procédez comme [ces instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="4ebc8-113">If you prefer tooinstall from hello command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-hello-process-server"></a><span data-ttu-id="4ebc8-114">Installer hello serveur de processus</span><span class="sxs-lookup"><span data-stu-id="4ebc8-114">Install from hello process server</span></span>

<span data-ttu-id="4ebc8-115">Installation du service mobilité toopush hello hello du serveur de processus lorsque vous activez la réplication pour une machine virtuelle, vous devez un compte qui peut être utilisé par hello processus serveur tooaccess hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4ebc8-115">If you want toopush hello Mobility service installation from hello process server when you enable replication for a VM, you need an account that can be used by hello process server tooaccess hello VM.</span></span> <span data-ttu-id="4ebc8-116">Hello compte est uniquement utilisé pour l’installation push de hello.</span><span class="sxs-lookup"><span data-stu-id="4ebc8-116">hello account is only used for hello push installation.</span></span>

1. <span data-ttu-id="4ebc8-117">Vous devriez avoir [créé un compte](vmware-walkthrough-prepare-vmware.md) qui peut être utilisé pour l’installation push.</span><span class="sxs-lookup"><span data-stu-id="4ebc8-117">You should have [created an account](vmware-walkthrough-prepare-vmware.md) that can be used for push installation.</span></span> <span data-ttu-id="4ebc8-118">Puis, vous spécifiez hello compte toouse lorsque vous configurez des paramètres de la source pendant le déploiement de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="4ebc8-118">You then specify hello account you want toouse when you configure source settings during Site Recovery deployment.</span></span>
2. <span data-ttu-id="4ebc8-119">Suivez ensuite [ces instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) si vous souhaitez que le service de mobilité hello toopush sur des machines virtuelles exécutant Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="4ebc8-119">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want toopush hello Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-methods"></a><span data-ttu-id="4ebc8-120">Autres méthodes</span><span class="sxs-lookup"><span data-stu-id="4ebc8-120">Other methods</span></span>

<span data-ttu-id="4ebc8-121">En savoir plus sur [installation à l’aide du Gestionnaire de Configuration du service mobilité hello](site-recovery-install-mobility-service-using-sccm.md), ou à l’aide de [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="4ebc8-121">Learn more about [installing hello Mobility service using Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), or using [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ebc8-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4ebc8-122">Next steps</span></span>

<span data-ttu-id="4ebc8-123">Accédez trop[étape 11 : activer la réplication](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="4ebc8-123">Go too[Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>
