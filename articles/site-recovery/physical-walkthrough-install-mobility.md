---
title: "aaaInstall hello service mobilité pour la réplication de serveur physique tooAzure | Documents Microsoft"
description: "Cet article décrit comment tooinstall hello agent du service mobilité sur les serveurs physiques réplication tooAzure avec le service d’Azure Site Recovery hello."
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
ms.openlocfilehash: 48fd2c0ffe67875ed446c8167c2ae7f90d3f537c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-install-hello-mobility-service"></a><span data-ttu-id="45e85-103">Étape 9 : Installer le service de mobilité hello</span><span class="sxs-lookup"><span data-stu-id="45e85-103">Step 9: Install hello Mobility service</span></span>


<span data-ttu-id="45e85-104">Cet article décrit comment composant de service de mobilité tooinstall hello lors de la réplication locale tooAzure de serveurs physiques Windows/Linux, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="45e85-104">This article describes how tooinstall hello Mobility service component when replicating on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="45e85-105">Hello service mobilité capture les écritures de données sur un ordinateur et les transfère de serveur de processus toohello.</span><span class="sxs-lookup"><span data-stu-id="45e85-105">hello Mobility service captures data writes on a machine, and forwards them toohello process server.</span></span> <span data-ttu-id="45e85-106">Il doit être installé sur chaque serveur que vous souhaitez tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="45e85-106">It should be installed on each server that you want tooreplicate tooAzure.</span></span>

<span data-ttu-id="45e85-107">Vous pouvez installer le service de mobilité hello manuellement ou à l’aide d’une installation push de hello Site Recovery traiter serveur lors de la réplication est activée, ou à l’aide d’un outil tel que System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="45e85-107">You can install hello Mobility service manually, or using a push installation from hello Site Recovery process server when replication is enabled, or using a tool such as System Center Configuration Manager.</span></span> <span data-ttu-id="45e85-108">Si vous utilisez installation push, service de hello est installé sur le serveur de hello lorsque vous activez la réplication.</span><span class="sxs-lookup"><span data-stu-id="45e85-108">If you use push installation, hello service is installed on hello server when you enable replication.</span></span>

<span data-ttu-id="45e85-109">Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="45e85-109">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="45e85-110">Installer manuellement</span><span class="sxs-lookup"><span data-stu-id="45e85-110">Install manually</span></span>

1. <span data-ttu-id="45e85-111">Vérifiez hello [conditions préalables](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) pour l’installation manuelle.</span><span class="sxs-lookup"><span data-stu-id="45e85-111">Check hello [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="45e85-112">Suivez [ces instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) pour l’installation manuelle à l’aide du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="45e85-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using hello portal.</span></span>
3. <span data-ttu-id="45e85-113">Si vous préférez tooinstall à partir de la ligne de commande hello, procédez comme [ces instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="45e85-113">If you prefer tooinstall from hello command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-hello-process-server"></a><span data-ttu-id="45e85-114">Installer hello serveur de processus</span><span class="sxs-lookup"><span data-stu-id="45e85-114">Install from hello process server</span></span>

<span data-ttu-id="45e85-115">Si vous souhaitez toopush hello installation du service mobilité hello du serveur de processus lorsque vous activez la réplication pour un ordinateur, vous avez besoin d’un compte peut être utilisé par hello processus tooaccess hello du serveur.</span><span class="sxs-lookup"><span data-stu-id="45e85-115">If you want toopush hello Mobility service installation from hello process server when you enable replication for a machine, you need an account that can be used by hello process server tooaccess hello machine.</span></span> <span data-ttu-id="45e85-116">Hello compte est uniquement utilisé pour l’installation push de hello.</span><span class="sxs-lookup"><span data-stu-id="45e85-116">hello account is only used for hello push installation.</span></span>

1. <span data-ttu-id="45e85-117">Si vous n’avez pas créé de compte, faites-le à l’aide de ces instructions :</span><span class="sxs-lookup"><span data-stu-id="45e85-117">If you haven't created an account, do so using these guidelines:</span></span>

    - <span data-ttu-id="45e85-118">Vous pouvez utiliser un compte local ou de domaine</span><span class="sxs-lookup"><span data-stu-id="45e85-118">You can use a domain or local account</span></span>
    - <span data-ttu-id="45e85-119">Pour Windows, si vous n’utilisez pas un compte de domaine, vous devez toodisable contrôle des accès utilisateur à distance sur l’ordinateur local de hello.</span><span class="sxs-lookup"><span data-stu-id="45e85-119">For Windows, if you're not using a domain account, you need toodisable Remote User Access control on hello local machine.</span></span> <span data-ttu-id="45e85-120">toodo, Bonjour Enregistrer sous **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, ajouter l’entrée DWORD de hello **LocalAccountTokenFilterPolicy**, avec la valeur 1.</span><span class="sxs-lookup"><span data-stu-id="45e85-120">toodo this, in hello register under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, add hello DWORD entry **LocalAccountTokenFilterPolicy**, with a value of 1.</span></span>
    - <span data-ttu-id="45e85-121">Si vous souhaitez l’entrée de Registre tooadd hello pour Windows à partir d’une interface CLI, tapez :</span><span class="sxs-lookup"><span data-stu-id="45e85-121">If you want tooadd hello registry entry for Windows from a CLI, type:</span></span>

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - <span data-ttu-id="45e85-122">Pour Linux, hello doit être racine sur le serveur de Linux hello source.</span><span class="sxs-lookup"><span data-stu-id="45e85-122">For Linux, hello account should be root on hello source Linux server.</span></span>

2. <span data-ttu-id="45e85-123">Suivez ensuite [ces instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) si vous souhaitez que le service de mobilité hello toopush sur des machines virtuelles exécutant Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="45e85-123">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want toopush hello Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-installation-methods"></a><span data-ttu-id="45e85-124">Autres méthodes d’installation</span><span class="sxs-lookup"><span data-stu-id="45e85-124">Other installation methods</span></span>

- <span data-ttu-id="45e85-125">[En savoir plus sur](site-recovery-install-mobility-service-using-sccm.md) installation à l’aide du Gestionnaire de Configuration du service mobilité hello</span><span class="sxs-lookup"><span data-stu-id="45e85-125">[Learn about](site-recovery-install-mobility-service-using-sccm.md) installing hello Mobility service using Configuration Manager</span></span>
- <span data-ttu-id="45e85-126">[En savoir plus sur](site-recovery-automate-mobility-service-install.md) l’installation avec Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="45e85-126">[Learn about](site-recovery-automate-mobility-service-install.md) installing with Azure Automation DSC.</span></span>


## <a name="next-steps"></a><span data-ttu-id="45e85-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="45e85-127">Next steps</span></span>

<span data-ttu-id="45e85-128">Accédez trop[étape 10 : activer la réplication](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="45e85-128">Go too[Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>
