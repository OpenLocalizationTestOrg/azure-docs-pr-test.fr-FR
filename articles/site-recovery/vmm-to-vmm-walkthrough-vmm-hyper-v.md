---
title: "aaaSet VMM et Hyper-V pour le site secondaire de réplication tooa avec Azure Site Recovery | Documents Microsoft"
description: "Décrit comment tooset les serveurs VMM System Center et les hôtes Hyper-V pour le site de réplication tooa secondaire VMM."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d0389e3b-3737-496c-bda6-77152264dd98
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 677bf6d38328ccc425e3b0f056d03159a52da428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-vmm-and-hyper-v-for-hyper-v-vm-replication-tooa-secondary-site"></a>Étape 4 : Configurer VMM et Hyper-V pour le site secondaire de machine virtuelle Hyper-V réplication tooa 

Une fois que vous avez préparé pour la mise en réseau, configurez les serveurs System Center Virtual Machine Manager (VMM) et les hôtes Hyper-V pour Hyper-V virtual machine (VM) réplication tooa site secondaire, à l’aide de [Azure Site Recovery](site-recovery-overview.md) Bonjour portail Azure. 

Après avoir lu cet article, validez les commentaires au bas de hello, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="prepare-vmm-servers"></a>Préparer les serveurs VMM 

tooprepare pour le déploiement :


1. Assurez-vous que les serveurs VMM conformes hello [prennent en charge les exigences](site-recovery-support-matrix-to-sec-site.md#on-premises-servers), et [conditions préalables au déploiement](vmm-to-vmm-walkthrough-prerequisites.md).
2. Assurez-vous que les serveurs VMM sont connecté toohello internet et avoir accès toothese URL.
    
    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
    - Si vous avez des règles de pare-feu basé sur l’adresse IP, assurez-vous qu’ils autorisent un tooAzure de communication.
    - Autoriser hello [plages d’adresses IP Azure Datacenter](https://www.microsoft.com/download/confirmation.aspx?id=41653)et hello port HTTPS (443).
    - Autoriser les plages d’adresses IP pour hello région Azure de votre abonnement et ouest des États-Unis (utilisé pour la gestion d’identité et contrôle d’accès).
3. Assurez-vous que le serveur VMM hello est [préparés pour le mappage réseau](vmm-to-vmm-walkthrough-network.md#prepare-for-network-mapping)


## <a name="prepare-hyper-v-hostsclusters"></a>Préparer les hôtes et clusters Hyper-V

1. Assurez-vous que les ordinateurs hôtes Hyper-V/clusters conformes hello [prennent en charge les exigences](site-recovery-support-matrix-to-sec-site.md#on-premises-servers), et [conditions préalables au déploiement](vmm-to-vmm-walkthrough-prerequisites.md).
2. Vérifiez la configuration requise de hello pour [des ordinateurs virtuels Hyper-V](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions)
3. Vérifiez les exigences du [réseau](site-recovery-support-matrix-to-sec-site.md#network-configuration) et du [stockage](site-recovery-support-matrix-to-sec-site.md#storage).
4. Assurez-vous que les ordinateurs hôtes Hyper-V sont connecté toohello internet et avoir accès toothese URL.
    
    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
    - Si vous avez des règles de pare-feu basé sur l’adresse IP, assurez-vous qu’ils autorisent un tooAzure de communication.
    - Autoriser hello [plages d’adresses IP Azure Datacenter](https://www.microsoft.com/download/confirmation.aspx?id=41653)et hello port HTTPS (443).
    - Autoriser les plages d’adresses IP pour hello région Azure de votre abonnement et ouest des États-Unis (utilisé pour la gestion d’identité et contrôle d’accès).

## <a name="prepare-for-single-server-deployment"></a>Préparation du déploiement d’un serveur unique


Si vous avez uniquement un seul serveur VMM, vous pouvez répliquer machines virtuelles dans les hôtes Hyper-V dans hello cloud VMM trop[Azure](hyper-v-site-walkthrough-overview.md) ou tooa secondaire cloud VMM, comme décrit dans ce document. Option de première hello est recommandée, car la réplication entre des clouds n’est pas transparente.

Si vous ne souhaitez pas tooreplicate entre des clouds, vous pouvez répliquer le serveur VMM autonome unique ou avec un seul serveur VMM déployé dans un cluster Windows étendu

### <a name="replicate-with-a-standalone-vmm-server"></a>Réplication avec un serveur VMM autonome

Dans ce scénario, vous déployez un seul serveur VMM de hello comme une machine virtuelle dans le site principal de hello et répliquez ce site secondaire de tooa de machine virtuelle à l’aide de la récupération de Site et le réplica Hyper-V.

1. **Configurez VMM sur une machine virtuelle Hyper-V**. Nous vous suggérons de que vous colocalisation d’instance de SQL Server hello utilisé par VMM sur hello même machine virtuelle. Ce gain de temps qu’une seule machine virtuelle a toobe créé. Si vous voulez toouse instance distante de SQL Server et si une panne se produit, vous devez toorecover cette instance avant de pouvoir récupérer VMM.
2. **Vérifiez le serveur VMM de hello a au moins deux clouds configurés**. Un cloud contiendra hello machines virtuelles vous le souhaitez tooreplicate et hello autres cloud servira d’emplacement secondaire de hello. Hello cloud qui contient hello machines virtuelles doivent satisfaire tooprotect [conditions préalables](#prerequisites).
3. Configurez Site Recovery comme le décrit cet article. Créer et inscrire le serveur VMM de hello dans un coffre, définir une stratégie de réplication et activer la réplication. noms VMM source et cible Hello sera hello à la même. Spécifiez que la réplication initiale a lieu sur le réseau de hello.
4. Lorsque vous configurez le mappage réseau vous mappez le réseau d’ordinateurs virtuels hello hello cloud principal toohello réseau de machines virtuelles pour le cloud secondaire de hello.
5. Dans la console Gestionnaire Hyper-V hello, activer la réplication Hyper-V sur l’ordinateur hôte Hyper-V hello contenant hello VMM VM et activer la réplication sur hello machine virtuelle. Assurez-vous que vous n’ajoutez pas tooclouds d’ordinateur virtuel VMM hello qui sont protégées par la récupération de Site, tooensure que les paramètres de réplication Hyper-V ne sont pas remplacés par la récupération de Site.
6. Si vous créez des plans de récupération pour le basculement, que vous utilisez hello même serveur VMM pour la source et cible.
7. Lors d’une panne complète, vous effectuez le basculement et la récupération comme suit :

   1. Dans la console du Gestionnaire Hyper-V hello dans un site secondaire hello, toofail sur le site secondaire hello principal VMM VM toohello, exécutez un basculement non planifié.
   2. Vérifiez que hello que VMM VM est activé et en cours d’exécution et dans le coffre de hello, exécuter un toofail basculement non planifié sur des machines virtuelles de hello de clouds spécifiques toosecondary principal. Valider le basculement de hello, puis sélectionnez un autre point de récupération si nécessaire.
   3. Une fois hello basculement non planifié est terminé, toutes les ressources accessibles à partir du site principal de hello à nouveau.
   4. Lorsque le site principal de hello est disponible, dans la console du Gestionnaire Hyper-V hello dans le site secondaire de hello, activez la réplication inverse pour hello VMM VM. Démarre la réplication pour hello machine virtuelle à partir de tooprimary secondaire.
   5. Dans la console du Gestionnaire Hyper-V hello dans un site secondaire hello, toofail sur le site principal de VMM VM toohello de hello, exécutez un basculement planifié. Valider le basculement de hello. Activez la réplication inverse, pour hello VMM VM est à nouveau réplication à partir de toosecondary principal.
   6. Dans le coffre Recovery Services hello, activez la réplication inverse pour les machines virtuelles, toostart répliquant tooprimary secondaire à partir de la charge de travail hello.
   7. Dans le coffre Recovery Services hello, exécuter un basculement planifié toofail hello précédent la charge de travail ordinateurs virtuels toohello site principal. Valider hello basculement toocomplete il. Ensuite, activez la réplication inverse toostart réplication hello charges de travail ordinateurs virtuels de toosecondary principal.

### <a name="replicate-with-a-stretched-vmm-cluster"></a>Réplication avec un cluster VMM étiré

Au lieu de déployer un serveur VMM autonome en tant qu’une machine virtuelle qui réplique le site secondaire de tooa, vous pouvez rendre VMM hautement disponible en la déployant comme une machine virtuelle dans un cluster de basculement Windows. pour fournir une résilience de la charge de travail et une protection contre les défaillances matérielles. toodeploy avec hello de récupération de Site VMM VM doit être déployé dans un cluster de stretch sur des sites géographiquement distincts. toodo cela :

1. Installez VMM sur un ordinateur virtuel dans un cluster de basculement Windows et sélectionnez hello option toorun hello serveur comme étant hautement disponible pendant l’installation.
2. instance de SQL Server Hello qui est utilisé par VMM doit être répliquée avec SQL Server AlwaysOn, afin qu’il existe un réplica de base de données hello dans le site secondaire de hello.
3. Suivez les instructions de hello dans cette toocreate article un coffre, inscrire hello serveur et configurer la protection. Vous devez tooregister chaque serveur VMM Bonjour cluster Bonjour de coffre Recovery Services. toodo, vous installez hello fournisseur sur un nœud actif et inscrire le serveur VMM de hello. Puis, vous installez hello fournisseur sur d’autres nœuds.
4. En cas de panne, hello VMM serveur et sa base de données SQL Server correspondante sont basculés et accessibles à partir du site secondaire de hello.



## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 5 : configurer un coffre](vmm-to-vmm-walkthrough-create-vault.md).
