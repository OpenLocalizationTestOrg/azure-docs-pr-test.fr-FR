---
title: "Installer le service Mobilité pour un serveur physique en vue d’une réplication sur Azure | Microsoft Docs"
description: "Cet article explique comment installer l’agent du service Mobilité sur des serveurs physiques en vue d’une réplication sur Azure à l’aide du service Azure Site Recovery."
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
ms.openlocfilehash: d73267d7a64221a3138af19e9a2d5dd15809b927
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="step-9-install-the-mobility-service"></a><span data-ttu-id="80267-103">Étape 9 : Installer le service Mobilité</span><span class="sxs-lookup"><span data-stu-id="80267-103">Step 9: Install the Mobility service</span></span>


<span data-ttu-id="80267-104">Cet article décrit comment installer le composant du service Mobilité lors de la réplication des serveurs physiques Windows/Linux sur Azure, à l’aide du service [Azure Site Recovery](site-recovery-overview.md) dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="80267-104">This article describes how to install the Mobility service component when replicating on-premises Windows/Linux physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="80267-105">Le service Mobilité enregistre les écritures de données sur une machine et les transmet au serveur de traitement.</span><span class="sxs-lookup"><span data-stu-id="80267-105">The Mobility service captures data writes on a machine, and forwards them to the process server.</span></span> <span data-ttu-id="80267-106">Ce service doit être installé sur chaque serveur que vous souhaitez répliquer sur Azure.</span><span class="sxs-lookup"><span data-stu-id="80267-106">It should be installed on each server that you want to replicate to Azure.</span></span>

<span data-ttu-id="80267-107">Vous pouvez installer le service Mobilité manuellement ou à l’aide d’une installation push à partir du serveur de traitement de Site Recovery lorsque la réplication est activée, ou à l’aide d’un outil tel que System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="80267-107">You can install the Mobility service manually, or using a push installation from the Site Recovery process server when replication is enabled, or using a tool such as System Center Configuration Manager.</span></span> <span data-ttu-id="80267-108">Si vous utilisez l’installation push, le service est installé sur le serveur lorsque vous activez la réplication.</span><span class="sxs-lookup"><span data-stu-id="80267-108">If you use push installation, the service is installed on the server when you enable replication.</span></span>

<span data-ttu-id="80267-109">Publiez des commentaires et des questions au bas de cet article, ou sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="80267-109">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="80267-110">Installer manuellement</span><span class="sxs-lookup"><span data-stu-id="80267-110">Install manually</span></span>

1. <span data-ttu-id="80267-111">Vérifiez les [prérequis](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) pour l’installation manuelle.</span><span class="sxs-lookup"><span data-stu-id="80267-111">Check the [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="80267-112">Suivez [ces instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) pour l’installation manuelle à l’aide du portail.</span><span class="sxs-lookup"><span data-stu-id="80267-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using the portal.</span></span>
3. <span data-ttu-id="80267-113">Si vous préférez installer à partir de la ligne de commande, suivez [ces instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="80267-113">If you prefer to install from the command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-the-process-server"></a><span data-ttu-id="80267-114">Installer à partir du serveur de traitement</span><span class="sxs-lookup"><span data-stu-id="80267-114">Install from the process server</span></span>

<span data-ttu-id="80267-115">Si vous voulez effectuer une installation push du service Mobilité à partir du serveur de processus lorsque vous activez la réplication pour une machine, vous devez disposer d’un compte pouvant être utilisé par le serveur de traitement pour accéder à la machine.</span><span class="sxs-lookup"><span data-stu-id="80267-115">If you want to push the Mobility service installation from the process server when you enable replication for a machine, you need an account that can be used by the process server to access the machine.</span></span> <span data-ttu-id="80267-116">Le compte est utilisé uniquement pour l’installation Push.</span><span class="sxs-lookup"><span data-stu-id="80267-116">The account is only used for the push installation.</span></span>

1. <span data-ttu-id="80267-117">Si vous n’avez pas créé de compte, faites-le à l’aide de ces instructions :</span><span class="sxs-lookup"><span data-stu-id="80267-117">If you haven't created an account, do so using these guidelines:</span></span>

    - <span data-ttu-id="80267-118">Vous pouvez utiliser un compte local ou de domaine</span><span class="sxs-lookup"><span data-stu-id="80267-118">You can use a domain or local account</span></span>
    - <span data-ttu-id="80267-119">Pour Windows, si vous n’utilisez pas un compte de domaine, vous devez désactiver le contrôle d’accès utilisateur distant sur la machine locale.</span><span class="sxs-lookup"><span data-stu-id="80267-119">For Windows, if you're not using a domain account, you need to disable Remote User Access control on the local machine.</span></span> <span data-ttu-id="80267-120">Pour cela, dans le registre situé sous **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, ajoutez l’entrée DWORD **LocalAccountTokenFilterPolicy** avec une valeur de 1.</span><span class="sxs-lookup"><span data-stu-id="80267-120">To do this, in the register under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, add the DWORD entry **LocalAccountTokenFilterPolicy**, with a value of 1.</span></span>
    - <span data-ttu-id="80267-121">Si vous souhaitez ajouter l’entrée de registre pour Windows à partir d’une interface CLI, tapez :</span><span class="sxs-lookup"><span data-stu-id="80267-121">If you want to add the registry entry for Windows from a CLI, type:</span></span>

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - <span data-ttu-id="80267-122">Pour Linux, le compte doit être un utilisateur racine sur le serveur Linux source.</span><span class="sxs-lookup"><span data-stu-id="80267-122">For Linux, the account should be root on the source Linux server.</span></span>

2. <span data-ttu-id="80267-123">Suivez ensuite [ces instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) si vous souhaitez effectuer une transmission push du service Mobilité sur les machines virtuelles exécutant Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="80267-123">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want to push the Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-installation-methods"></a><span data-ttu-id="80267-124">Autres méthodes d’installation</span><span class="sxs-lookup"><span data-stu-id="80267-124">Other installation methods</span></span>

- <span data-ttu-id="80267-125">[En savoir plus](site-recovery-install-mobility-service-using-sccm.md) sur l’installation du service Mobilité à l’aide de Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="80267-125">[Learn about](site-recovery-install-mobility-service-using-sccm.md) installing the Mobility service using Configuration Manager</span></span>
- <span data-ttu-id="80267-126">[En savoir plus sur](site-recovery-automate-mobility-service-install.md) l’installation avec Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="80267-126">[Learn about](site-recovery-automate-mobility-service-install.md) installing with Azure Automation DSC.</span></span>


## <a name="next-steps"></a><span data-ttu-id="80267-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="80267-127">Next steps</span></span>

<span data-ttu-id="80267-128">Aller à [Étape 10 : activer la réplication](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="80267-128">Go to [Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>
