---
title: "conditions préalables de hello aaaReview pour Hyper-V réplication tooa site VMM secondaire avec Azure Site Recovery | Documents Microsoft"
description: "Décrit les conditions préalables de hello pour répliquer des ordinateurs virtuels Hyper-V tooa site VMM secondaire avec Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 21ff0545-8be5-4495-9804-78ab6e24add6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 1bd945fdda36c3cce5d159209abbd3c98a7e3682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-and-limitations-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a>Étape 2 : Passez en revue les conditions préalables de hello et limitations pour le site VMM secondaire de machine virtuelle Hyper-V réplication tooa


Une fois que vous avez consulté hello [architecture du scénario](vmm-to-vmm-walkthrough-architecture.md), lisez cette toomake article que vous comprenez les conditions préalables au déploiement hello, lors de la réplication des machines virtuelles locales Hyper-V (VM) gérés dans System Center Virtual Machine Manager (VMM) des clouds, tooa secondaire du site à l’aide de [Azure Site Recovery](site-recovery-overview.md) Bonjour portail Azure.

Après avoir lu cet article, validez les commentaires au bas de hello, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites-and-limitations"></a>Conditions préalables et limitations

**Prérequis** | **Détails**
--- | ---
**Microsoft Azure** | Un abonnement [Microsoft Azure](http://azure.microsoft.com/).<br/><br/> Vous pouvez commencer par une version d’ [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).<br/><br/> [En savoir plus](https://azure.microsoft.com/pricing/details/site-recovery/) sur la tarification Site Recovery.<br/><br/> Vérifiez les régions hello pris en charge pour la récupération de Site, sous géographique disponibilité dans [détails de la tarification de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
**Serveurs VMM** | Nous vous recommandons de qu'avoir deux serveurs VMM, un site principal de hello et un Bonjour secondaire.<br/><br/> La réplication entre des clouds sur un seul serveur VMM est prise en charge.<br/><br/> Serveurs VMM doivent exécuter au moins System Center 2012 SP1 avec les dernières mises à jour de hello.<br/><br/> Les serveurs VMM doivent avoir accès à Internet.
**Clouds VMM** | Chaque serveur VMM doit avoir à un ou plusieurs clouds et tous les clouds doivent avoir le profil de capacité de Hyper-V hello. <br/><br/>Les clouds doivent contenir un ou plusieurs groupes hôtes VMM.<br/><br/> Si vous avez uniquement un seul serveur VMM, il doit au moins deux clouds, tooact comme principale et secondaire.
**Hyper-V** | Serveurs Hyper-V doivent être en cours d’exécution au moins Windows Server 2012 avec le rôle de hello Hyper-V, et avoir hello les dernières mises à jour installées.<br/><br/> Un serveur Hyper-V doit contenir au moins une machine virtuelle.<br/><br/>  Les serveurs hôte Hyper-V doivent se trouver dans des groupes hôtes dans des clouds VMM principaux et secondaires hello.<br/><br/> Si vous exécutez Hyper-V dans un cluster sur Windows Server 2012 R2, installez la [mise à jour 2961977](https://support.microsoft.com/kb/2961977).<br/><br/> Si vous exécutez Hyper-V dans un cluster sous Windows Server 2012, notez que le répartiteur de clusters n’est pas créé automatiquement si vous avez un cluster basé sur des adresses IP statiques. Configurer le service broker de cluster hello manuellement. [En savoir plus](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).<br/><br/> Les serveurs Hyper-V doivent disposer d’un accès Internet.




## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 3 : planifier la mise en réseau](vmm-to-vmm-walkthrough-network.md).
