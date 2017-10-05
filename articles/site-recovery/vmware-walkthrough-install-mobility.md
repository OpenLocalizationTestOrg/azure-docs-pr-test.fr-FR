---
title: "Installer le service Mobilité pour VMware en vue d’une réplication sur Azure | Microsoft Docs"
description: "Cet article explique comment installer l’agent du service Mobilité pour VMware en vue d’une réplication sur Azure à l’aide du service Azure Site Recovery."
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
ms.openlocfilehash: bc520bd2ea54208889861a7a3b275e3008a05d53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="step-10-install-the-mobility-service"></a><span data-ttu-id="424cf-103">Étape 10 : installer le service Mobilité</span><span class="sxs-lookup"><span data-stu-id="424cf-103">Step 10: Install the Mobility service</span></span>


<span data-ttu-id="424cf-104">Cet article explique comment configurer des paramètres source et cible lors de la réplication de machines virtuelles VMware locales sur Azure à l’aide du service [Azure Site Recovery](site-recovery-overview.md) dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="424cf-104">This article describes how to configure source and target settings when replicating on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="424cf-105">Le service Mobilité enregistre les écritures de données sur une machine et les transmet au serveur de traitement.</span><span class="sxs-lookup"><span data-stu-id="424cf-105">The Mobility service captures data writes on a machine, and forwards them to the process server.</span></span> <span data-ttu-id="424cf-106">Ce service devrait être installé sur chaque machine que vous souhaitez répliquer sur Azure.</span><span class="sxs-lookup"><span data-stu-id="424cf-106">It should be installed on each machine that you want to replicate to Azure.</span></span>

<span data-ttu-id="424cf-107">Vous pouvez installer le manuel du service Mobilité, à l’aide d’une installation push à partir du serveur de traitement de Site Recovery lorsque la réplication est activée, ou utiliser un outil de System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="424cf-107">You can install the Mobility service manual, using a push installation from the Site Recovery process server when replication is enabled, or use a tool System Center Configuration Manager.</span></span> <span data-ttu-id="424cf-108">Si vous utilisez l’installation push, le service est installé sur la machine virtuelle lorsque la réplication est activée.</span><span class="sxs-lookup"><span data-stu-id="424cf-108">If you use push installation, the service is installed on the VM when replication is enabled.</span></span>

<span data-ttu-id="424cf-109">Publiez des commentaires et des questions au bas de cet article, ou sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="424cf-109">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="424cf-110">Installer manuellement</span><span class="sxs-lookup"><span data-stu-id="424cf-110">Install manually</span></span>

1. <span data-ttu-id="424cf-111">Vérifiez les [prérequis](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) pour l’installation manuelle.</span><span class="sxs-lookup"><span data-stu-id="424cf-111">Check the [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="424cf-112">Suivez [ces instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) pour l’installation manuelle à l’aide du portail.</span><span class="sxs-lookup"><span data-stu-id="424cf-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using the portal.</span></span>
3. <span data-ttu-id="424cf-113">Si vous préférez installer à partir de la ligne de commande, suivez [ces instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="424cf-113">If you prefer to install from the command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-the-process-server"></a><span data-ttu-id="424cf-114">Installer à partir du serveur de processus</span><span class="sxs-lookup"><span data-stu-id="424cf-114">Install from the process server</span></span>

<span data-ttu-id="424cf-115">Si vous voulez effectuer une installation push du service Mobilité à partir du serveur de processus lorsque la réplication est activée, vous devez disposer d’un compte pouvant être utilisé par le serveur de processus pour accéder à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="424cf-115">If you want to push the Mobility service installation from the process server when you enable replication for a VM, you need an account that can be used by the process server to access the VM.</span></span> <span data-ttu-id="424cf-116">Le compte est utilisé uniquement pour l’installation Push.</span><span class="sxs-lookup"><span data-stu-id="424cf-116">The account is only used for the push installation.</span></span>

1. <span data-ttu-id="424cf-117">Vous devriez avoir [créé un compte](vmware-walkthrough-prepare-vmware.md) qui peut être utilisé pour l’installation push.</span><span class="sxs-lookup"><span data-stu-id="424cf-117">You should have [created an account](vmware-walkthrough-prepare-vmware.md) that can be used for push installation.</span></span> <span data-ttu-id="424cf-118">Vous pouvez ensuite spécifier le compte que vous souhaitez utiliser lors de la configuration des paramètres source pendant le déploiement de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="424cf-118">You then specify the account you want to use when you configure source settings during Site Recovery deployment.</span></span>
2. <span data-ttu-id="424cf-119">Suivez ensuite [ces instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) si vous souhaitez effectuer une transmission push du service Mobilité sur les machines virtuelles exécutant Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="424cf-119">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want to push the Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-methods"></a><span data-ttu-id="424cf-120">Autres méthodes</span><span class="sxs-lookup"><span data-stu-id="424cf-120">Other methods</span></span>

<span data-ttu-id="424cf-121">En savoir plus sur comment [installer le service Mobilité à l’aide du Gestionnaire de configuration](site-recovery-install-mobility-service-using-sccm.md), ou à l’aide [d’Azure Automation DSC](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="424cf-121">Learn more about [installing the Mobility service using Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), or using [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="424cf-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="424cf-122">Next steps</span></span>

<span data-ttu-id="424cf-123">Aller à [Étape 11 : activer la réplication](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="424cf-123">Go to [Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>
