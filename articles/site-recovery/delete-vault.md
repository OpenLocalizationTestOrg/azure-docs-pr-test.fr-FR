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
# <a name="delete-a-site-recovery-vault"></a>Supprimer un archivage Site Recovery
Des dépendances peuvent vous empêcher de supprimer un archivage Azure Site Recovery. Hello actions que vous tootake dépend de scénario de récupération de Site hello : VMware tooAzure, tooAzure de Hyper-V (avec et sans System Center Virtual Machine Manager) et Azure Backup. toodelete un coffre utilisé pour la sauvegarde Azure, consultez [supprimer un coffre de sauvegarde dans Azure](../backup/backup-azure-delete-vault.md).

>[!Important]
>Si vous testez le produit de hello et que vous n’êtes pas inquiet de la perte de données, utilisez hello force delete méthode toorapidly supprimer le coffre hello et toutes ses dépendances.

> Hello commande PowerShell supprime tout le contenu de l’archivage de hello hello et n’est pas réversible.

## <a name="use-powershell-tooforce-delete-hello-vault"></a>Utilisez PowerShell tooforce de supprimer l’archivage de hello 

hello toodelete de coffre de récupération de Site même s’il existe des éléments protégés, utilisez les commandes suivantes :

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a>Supprimer un archivage Site Recovery 
coffre de hello toodelete, hello suivez étapes pour votre scénario recommandée.

### <a name="vmware-vms-tooazure"></a>Les ordinateurs virtuels VMware tooAzure

1. Supprimer tous les protégées des machines virtuelles en suivant les étapes de hello dans [désactiver la protection pour VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Supprimer toutes les stratégies de réplication en suivant les étapes de hello dans [supprimer une stratégie de réplication](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3. Supprimer les références toovCenter par hello suivant les étapes dans [supprimer un vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).

4. Supprimer le serveur de configuration hello en suivant les étapes de hello dans [désaffecter un serveur de configuration](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).

5. Supprimer l’archivage de hello.


### <a name="hyper-v-vms-with-virtual-machine-manager-tooazure"></a>Des ordinateurs virtuels Hyper-V (avec Virtual Machine Manager) tooAzure
1. Supprimer tous les protégées des machines virtuelles en suivant les étapes de hello dans [désactiver la protection pour un serveur physique ou le VMware VM](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Supprimer toutes les stratégies de réplication en suivant les étapes de hello dans [supprimer une stratégie de réplication](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3.  Delete fait référence à des serveurs de tooVirtual Machine Manager en suivant les étapes de hello dans [annuler l’inscription d’un serveur VMM connecté](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).

4.  Supprimer l’archivage de hello.

### <a name="hyper-v-vms-without-virtual-machine-manager-tooazure"></a>Machines virtuelles de Hyper-V (sans Virtual Machine Manager) tooAzure
1. Supprimer tous les protégées des machines virtuelles en suivant les étapes de hello dans [désactiver la protection pour un serveur physique ou le VMware VM](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Supprimer toutes les stratégies de réplication en suivant les étapes de hello dans [supprimer une stratégie de réplication](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3. Delete fait référence à des serveurs tooHyper-V en suivant les étapes de hello dans [annuler l’inscription d’un ordinateur hôte Hyper-V](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).

4. Supprimer le site de hello Hyper-V.

5. Supprimer l’archivage de hello.
