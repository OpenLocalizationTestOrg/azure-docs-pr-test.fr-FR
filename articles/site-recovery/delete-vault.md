---
title: "aaaDelete un coffre de récupération de Site"
description: "Découvrez comment toodelete un coffre Azure Site Recovery, basé sur un scénario de récupération de Site hello."
service: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: 36db202d8b790bb5d31d1348fb72f51acb5d559c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="3b9a5-103">Supprimer un archivage Site Recovery</span><span class="sxs-lookup"><span data-stu-id="3b9a5-103">Delete a Site Recovery vault</span></span>
<span data-ttu-id="3b9a5-104">Des dépendances peuvent vous empêcher de supprimer un archivage Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-104">Dependencies can prevent you from deleting an Azure Site Recovery vault.</span></span> <span data-ttu-id="3b9a5-105">Hello actions que vous tootake dépend de scénario de récupération de Site hello : VMware tooAzure, tooAzure de Hyper-V (avec et sans System Center Virtual Machine Manager) et Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-105">hello actions you need tootake vary based on hello Site Recovery scenario: VMware tooAzure, Hyper-V (with and without System Center Virtual Machine Manager) tooAzure, and Azure Backup.</span></span> <span data-ttu-id="3b9a5-106">toodelete un coffre utilisé pour la sauvegarde Azure, consultez [supprimer un coffre de sauvegarde dans Azure](../backup/backup-azure-delete-vault.md).</span><span class="sxs-lookup"><span data-stu-id="3b9a5-106">toodelete a vault used in Azure Backup, see [Delete a Backup vault in Azure](../backup/backup-azure-delete-vault.md).</span></span>

>[!Important]
><span data-ttu-id="3b9a5-107">Si vous testez le produit de hello et que vous n’êtes pas inquiet de la perte de données, utilisez hello force delete méthode toorapidly supprimer le coffre hello et toutes ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-107">If you're testing hello product and aren't concerned about data loss, use hello force delete method toorapidly remove hello vault and all its dependencies.</span></span>

> <span data-ttu-id="3b9a5-108">Hello commande PowerShell supprime tout le contenu de l’archivage de hello hello et n’est pas réversible.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-108">hello PowerShell command deletes all hello contents of hello vault and is not reversible.</span></span>

## <a name="use-powershell-tooforce-delete-hello-vault"></a><span data-ttu-id="3b9a5-109">Utilisez PowerShell tooforce de supprimer l’archivage de hello</span><span class="sxs-lookup"><span data-stu-id="3b9a5-109">Use PowerShell tooforce delete hello vault</span></span> 

<span data-ttu-id="3b9a5-110">hello toodelete de coffre de récupération de Site même s’il existe des éléments protégés, utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="3b9a5-110">toodelete hello Site Recovery vault even if there are protected items, use these commands:</span></span>

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="3b9a5-111">Supprimer un archivage Site Recovery</span><span class="sxs-lookup"><span data-stu-id="3b9a5-111">Delete a Site Recovery vault</span></span> 
<span data-ttu-id="3b9a5-112">coffre de hello toodelete, hello suivez étapes pour votre scénario recommandée.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-112">toodelete hello vault, follow hello recommended steps for your scenario.</span></span>

### <a name="vmware-vms-tooazure"></a><span data-ttu-id="3b9a5-113">Les ordinateurs virtuels VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="3b9a5-113">VMware VMs tooAzure</span></span>

1. <span data-ttu-id="3b9a5-114">Supprimer tous les protégées des machines virtuelles en suivant les étapes de hello dans [désactiver la protection pour VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="3b9a5-114">Delete all protected VMs by following hello steps in [Disable protection for a VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="3b9a5-115">Supprimer toutes les stratégies de réplication en suivant les étapes de hello dans [supprimer une stratégie de réplication](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="3b9a5-115">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="3b9a5-116">Supprimer les références toovCenter par hello suivant les étapes dans [supprimer un vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span><span class="sxs-lookup"><span data-stu-id="3b9a5-116">Delete references toovCenter by following hello steps in [Delete a vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span></span>

4. <span data-ttu-id="3b9a5-117">Supprimer le serveur de configuration hello en suivant les étapes de hello dans [désaffecter un serveur de configuration](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="3b9a5-117">Delete hello configuration server by following hello steps in [Decommission a configuration server](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span></span>

5. <span data-ttu-id="3b9a5-118">Supprimer l’archivage de hello.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-118">Delete hello vault.</span></span>


### <a name="hyper-v-vms-with-virtual-machine-manager-tooazure"></a><span data-ttu-id="3b9a5-119">Des ordinateurs virtuels Hyper-V (avec Virtual Machine Manager) tooAzure</span><span class="sxs-lookup"><span data-stu-id="3b9a5-119">Hyper-V VMs (with Virtual Machine Manager) tooAzure</span></span>
1. <span data-ttu-id="3b9a5-120">Supprimer tous les protégées des machines virtuelles en suivant les étapes de hello dans [désactiver la protection pour un serveur physique ou le VMware VM](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="3b9a5-120">Delete all protected VMs by following hello steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="3b9a5-121">Supprimer toutes les stratégies de réplication en suivant les étapes de hello dans [supprimer une stratégie de réplication](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="3b9a5-121">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3.  <span data-ttu-id="3b9a5-122">Delete fait référence à des serveurs de tooVirtual Machine Manager en suivant les étapes de hello dans [annuler l’inscription d’un serveur VMM connecté](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span><span class="sxs-lookup"><span data-stu-id="3b9a5-122">Delete references tooVirtual Machine Manager servers by following hello steps in [Unregister a connected VMM server](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span></span>

4.  <span data-ttu-id="3b9a5-123">Supprimer l’archivage de hello.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-123">Delete hello vault.</span></span>

### <a name="hyper-v-vms-without-virtual-machine-manager-tooazure"></a><span data-ttu-id="3b9a5-124">Machines virtuelles de Hyper-V (sans Virtual Machine Manager) tooAzure</span><span class="sxs-lookup"><span data-stu-id="3b9a5-124">Hyper-V VMs (without Virtual Machine Manager) tooAzure</span></span>
1. <span data-ttu-id="3b9a5-125">Supprimer tous les protégées des machines virtuelles en suivant les étapes de hello dans [désactiver la protection pour un serveur physique ou le VMware VM](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="3b9a5-125">Delete all protected VMs by following hello steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="3b9a5-126">Supprimer toutes les stratégies de réplication en suivant les étapes de hello dans [supprimer une stratégie de réplication](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="3b9a5-126">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="3b9a5-127">Delete fait référence à des serveurs tooHyper-V en suivant les étapes de hello dans [annuler l’inscription d’un ordinateur hôte Hyper-V](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span><span class="sxs-lookup"><span data-stu-id="3b9a5-127">Delete references tooHyper-V servers by following hello steps in [Unregister a Hyper-V host](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span></span>

4. <span data-ttu-id="3b9a5-128">Supprimer le site de hello Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-128">Delete hello Hyper-V site.</span></span>

5. <span data-ttu-id="3b9a5-129">Supprimer l’archivage de hello.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-129">Delete hello vault.</span></span>
