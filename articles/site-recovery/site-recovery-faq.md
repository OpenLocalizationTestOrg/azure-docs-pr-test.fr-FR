---
title: "Azure Site Recovery : Forum Aux Questions | Microsoft Docs"
description: "Cet article traite des questions fréquemment posées sur Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5cdc4bcd-b4fe-48c7-8be1-1db39bd9c078
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/22/2017
ms.author: raynew
ms.openlocfilehash: 6d0bd2475466e5745e1f084bd2267d954d624ebd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-frequently-asked-questions-faq"></a>Azure Site Recovery : Forum Aux Questions (FAQ)
Cet article contient les questions fréquemment posées sur Microsoft Azure Site Recovery. Si vous avez des questions après avoir lu cet article, faites-nous part hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).

## <a name="general"></a>Généralités
### <a name="what-does-site-recovery-do"></a>À quoi sert Site Recovery ?
Récupération de site contribue tooyour continuité des activités et la stratégie de récupération d’urgence, par l’orchestration et l’automatisation de la réplication de machines virtuelles Azure entre les régions, les ordinateurs virtuels locaux et tooAzure des serveurs physiques et tooa d’ordinateurs locaux Centre de données secondaire. [En savoir plus](site-recovery-overview.md).

### <a name="what-can-site-recovery-protect"></a>Que peut protéger Site Recovery ?
* **Machines virtuelles Azure** : Site Recovery permet de répliquer n’importe quelle charge de travail exécutée sur une machine virtuelle Azure prise en charge
* **Machines virtuelles Hyper-V**: Site Recovery peut protéger toute charge de travail en cours d’exécution sur une machine virtuelle Hyper-V.
* **Serveurs physiques**: Site Recovery peut protéger les serveurs physiques exécutant Windows ou Linux.
* **Machines virtuelles VMware**: Site Recovery peut protéger toute charge de travail en cours d’exécution dans une machine virtuelle VMware.

### <a name="does-site-recovery-support-hello-azure-resource-manager-model"></a>Récupération de Site prend-elle en charge le modèle du Gestionnaire de ressources Azure hello ?
Récupération de site est disponible dans hello portail Azure avec prise en charge pour le Gestionnaire de ressources. Récupération de site prend en charge les déploiements hérités Bonjour portail Azure classic. Impossible de créer des coffres dans le portail classique de hello et nouvelles fonctionnalités ne sont pas pris en charge.

### <a name="can-i-replicate-azure-vms"></a>Puis-je répliquer des machines virtuelles Azure ?
Oui, vous pouvez répliquer des machines virtuelles Azure prises en charge entre des régions Azure. [En savoir plus](site-recovery-azure-to-azure.md).

### <a name="what-do-i-need-in-hyper-v-tooorchestrate-replication-with-site-recovery"></a>De quoi ai-je besoin dans la réplication Hyper-V tooorchestrate avec récupération de Site ?
Pour le serveur hôte de Hyper-V hello ce dont vous avez besoin dépend de scénario de déploiement hello. Découvrez hello des conditions préalables de Hyper-V dans :

* [Réplication des ordinateurs virtuels Hyper-V (sans VMM) tooAzure](site-recovery-hyper-v-site-to-azure.md)
* [Réplication des ordinateurs virtuels Hyper-V (avec VMM) tooAzure](site-recovery-vmm-to-azure.md)
* [Réplication des ordinateurs virtuels Hyper-V tooa centre de données secondaire](site-recovery-vmm-to-vmm.md)
* Si vous effectuez une réplication tooa secondaire centre de données en savoir plus sur [prise en charge des systèmes d’exploitation invités pour les ordinateurs virtuels Hyper-V](https://technet.microsoft.com/library/mt126277.aspx).
* Si vous effectuez une réplication tooAzure, récupération de Site prend en charge tous les systèmes d’exploitation invités hello qui sont [pris en charge par Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx).

### <a name="can-i-protect-vms-when-hyper-v-is-running-on-a-client-operating-system"></a>Puis-je protéger des machines virtuelles lorsque Hyper-V est en cours d’exécution sur un système d’exploitation client ?
Non, les machines virtuelles doivent se trouver sur un serveur hôte Hyper-V s’exécutant sur une machine serveur Windows prise en charge. Si vous avez besoin de tooprotect un ordinateur client vous pourriez répliquer en tant qu’un ordinateur physique trop[Azure](site-recovery-vmware-to-azure.md) ou un [centre de données secondaire](site-recovery-vmware-to-vmware.md).

### <a name="what-workloads-can-i-protect-with-site-recovery"></a>Quelles charges de travail puis-je protéger avec Site Recovery ?
La plupart des charges de travail en cours d’exécution sur un serveur physique ou un ordinateur virtuel pris en charge, vous pouvez utiliser tooprotect de récupération de Site. Récupération de site prend en charge pour la réplication d’application, afin que les applications puissent être récupérées état intelligent de tooan. Site Recovery s’intègre aux applications Microsoft, notamment à SharePoint, Exchange, Dynamics, SQL Server et Active Directory, et fonctionne en étroite collaboration avec les principaux fournisseurs, notamment Oracle, SAP, IBM et Red Hat. [En savoir plus](site-recovery-workload.md) sur la protection des charges de travail.

### <a name="do-hyper-v-hosts-need-toobe-in-vmm-clouds"></a>Ordinateurs hôtes Hyper-V doivent-elles toobe dans les clouds VMM ?
Si vous souhaitez que le centre de données secondaire tooreplicate tooa, puis les ordinateurs virtuels Hyper-V doivent se trouver sur Hyper-V héberge les serveurs situés dans un cloud VMM. Si vous souhaitez tooreplicate tooAzure, vous pouvez répliquer des machines virtuelles sur des serveurs d’hôtes Hyper-V avec ou sans les clouds VMM. [En savoir plus](site-recovery-hyper-v-site-to-azure.md).

### <a name="can-i-deploy-site-recovery-with-vmm-if-i-only-have-one-vmm-server"></a>Puis-je déployer Site Recovery avec VMM si je ne dispose que d’un seul serveur VMM ?

Oui. Vous pouvez soit répliquer des machines virtuelles dans les serveurs Hyper-V dans hello VMM cloud tooAzure, ou vous pouvez répliquer entre des clouds VMM sur hello même serveur. Pour la réplication locale tooon local, nous vous recommandons que vous avez un serveur VMM dans les deux sites principaux et secondaires de hello.  

### <a name="what-physical-servers-can-i-protect"></a>Quels serveurs physiques puis-je protéger ?
Vous pouvez répliquer les serveurs physiques exécutant Windows et Linux tooAzure ou tooa secondaire du site. [Découvrez](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) la configuration requise du système d’exploitation.  Hello mêmes exigences s’appliquent si vous effectuez une réplication tooAzure des serveurs physiques, ou tooa un site secondaire.


Notez que les serveurs physiques seront exécutés en tant que machines virtuelles dans Azure si votre serveur local tombe en panne. La restauration automatique tooan local serveur physique n’est pas pris en charge actuellement. Pour un ordinateur protégé en tant que physique, vous pouvez uniquement la restauration automatique tooa VMware virtual machine.

### <a name="what-vmware-vms-can-i-protect"></a>Quelles machines virtuelles VMware puis-je protéger ?

tooprotect les ordinateurs virtuels VMware vous aurez besoin d’un hyperviseur vSphere et les machines virtuelles exécutant les outils VMware. Nous vous recommandons également d’avoir un les toomanage hello hyperviseurs VMware vCenter server. [En savoir plus](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) sur des spécifications exactes pour la réplication de site secondaire de tooa et tooAzure de machines virtuelles ou des serveurs VMware.


### <a name="can-i-manage-disaster-recovery-for-my-branch-offices-with-site-recovery"></a>Puis-je gérer la récupération d’urgence pour mes succursales avec Site Recovery ?
Oui. Lorsque vous utilisez la réplication tooorchestrate de récupération de Site et de basculement dans vos filiales, vous obtenez une orchestration unifiée et l’affichage de toutes les charges de travail votre office branche dans un emplacement central. Vous pouvez facilement effectuer des basculements et administrer la récupération d’urgence de toutes les branches à partir de votre siège social, sans visiter les branches hello.

## <a name="pricing"></a>Tarification

### <a name="what-charges-do-i-incur-while-using-azure-site-recovery"></a>Quels frais sont facturés lors de l’utilisation d’Azure Site Recovery ?
Lorsque vous utilisez la récupération de Site, peut occasionner des frais de licences de Site Recovery hello, le stockage Azure, les transactions de stockage et transfert de données sortantes. [En savoir plus](https://azure.microsoft.com/pricing/details/site-recovery).

licence de Site Recovery Hello est par instance protégée, où une instance est un ordinateur virtuel ou un serveur physique.

- Si un disque de machine virtuelle réplique le compte de stockage standard tooa, hello frais de stockage Azure est pour la consommation du stockage hello. Par exemple, si la taille du disque source hello est 1 To et 400 Go est utilisé, Site Recovery crée un disque dur virtuel de 1 To dans Azure, mais stockage hello facturé est 400 Go (plus de quantité hello d’espace de stockage utilisé pour les journaux de réplication).
- Si un disque de machine virtuelle est répliquée tooa compte de stockage premium, hello frais de stockage Azure est de taille de stockage hello configuré, arrondi à pour hello plus proche de l’option de disque de stockage premium. Par exemple, si la taille du disque source hello est 50 Go, Site Recovery crée un disque de 50 Go dans Azure et Azure mappe cette toohello le plus proche du disque de stockage premium (P10).  Les coûts sont calculés sur P10 et non sur la taille du disque hello 50 Go.  [En savoir plus](https://aka.ms/premium-storage-pricing).  Si vous utilisez le stockage premium, un compte de stockage standard pour la connexion de réplication est également requis, et quantité hello standard d’espace de stockage utilisé pour ces journaux est également facturée.
- Aucun disque n’est créé tant qu’un test de basculement ou un basculement n’a pas eu lieu. État de réplication hello, stockage frais sous la catégorie hello de « objet blob de pages et de disque » conformément à hello [calculateur de coût de stockage](https://azure.microsoft.com/en-in/pricing/calculator/) sont soumises. Ces frais sont basés sur le type de stockage hello de redondance de données premium et standard et hello - LRS, GRS, etc. de RA-GRS de type.
- Si hello option toouse des disques gérés sur un basculement est sélectionné, [frais de disques gérés](https://azure.microsoft.com/en-in/pricing/details/managed-disks/) s’appliquent après un basculement et de test de basculement. Les frais de disques managés ne s’appliquent pas pendant la réplication.
- Si l’option hello toouse géré des disques sur un basculement n’est pas sélectionnée, stockage frais sous la catégorie hello de « objet blob de pages et de disque » conformément à hello [calculateur de coût de stockage](https://azure.microsoft.com/en-in/pricing/calculator/) sont effectuées après le basculement. Ces frais sont basés sur le type de stockage hello de redondance de données premium et standard et hello - LRS, GRS, etc. de RA-GRS de type.
- Des transactions de stockage sont facturées pendant la réplication à l’état stationnaire et pour les opérations régulières de machine virtuelle après un basculement/test de basculement. Mais ces coûts sont négligeables.

Sont également coûts pendant le basculement de test, où les coûts de transactions de machine virtuelle, de stockage, de sortie et de stockage hello seront appliquées.



## <a name="security"></a>Sécurité
### <a name="is-replication-data-sent-toohello-site-recovery-service"></a>Sont-ce que les données de réplication envoyées toohello le service de récupération de Site ?
Non, Site Recovery n’intercepte pas les données répliquées et n’a pas d’informations sur les éléments exécutés sur vos machines virtuelles ou serveurs physiques.
Les données de réplication sont échangées entre des hôtes Hyper-V, des hyperviseurs VMware ou des serveurs physiques locaux et le stockage Azure ou votre site secondaire. Site Recovery ne dispose d’aucune toointercept possibilité que les données. Uniquement les métadonnées de hello nécessaires tooorchestrate réplication et basculement est envoyé toohello le service de récupération de Site.  

Récupération de site est ISO 27001 : 2013, 27018, HIPAA, DPA certifié et est en cours de hello des évaluations SOC2 et FedRAMP JAB.

### <a name="for-compliance-reasons-even-our-on-premises-metadata-must-remain-within-hello-same-geographic-region-can-site-recovery-help-us"></a>Pour des raisons de conformité, même nos métadonnées local doivent rester dans hello même région géographique. Site Recovery peut-il nous aider ?
Oui. Lorsque vous créez un coffre Site Recovery dans une région, nous nous assurons que qui toutes les métadonnées que nous devez tooenable et orchestrer la réplication et le basculement reste dans cette région de géographique limite.

### <a name="does-site-recovery-encrypt-replication"></a>Site Recovery chiffre-t-il la réplication ?
Pour la réplication de machines virtuelles et de serveurs physiques entre des sites locaux, le chiffrement en transit est pris en charge. Pour les ordinateurs virtuels et des serveurs physiques réplication tooAzure, à la fois le chiffrement en transit et [chiffrement au repos (dans Azure)](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) sont pris en charge.

## <a name="replication"></a>Réplication

### <a name="can-i-replicate-over-a-site-to-site-vpn-tooazure"></a>Puis-je répliquer via un tooAzure VPN de site à site ?
Azure Site Recovery réplique le compte de stockage Azure tooan données sur un point de terminaison public. La réplication ne s’effectue pas via un réseau VPN de site à site. Vous pouvez créer un réseau VPN de site à site, avec un réseau virtuel Azure. Cela n’interfère pas avec la réplication Site Recovery.

### <a name="can-i-use-expressroute-tooreplicate-virtual-machines-tooazure"></a>Puis-je utiliser ExpressRoute tooreplicate virtuels tooAzure ?
Oui, ExpressRoute peut être utilisé tooreplicate virtuels tooAzure. Azure Site Recovery réplique les données tooan compte de stockage Azure via un point de terminaison public. Vous avez besoin tooset [l’homologation publique](../expressroute/expressroute-circuit-peerings.md#public-peering) toouse ExpressRoute pour la réplication de la récupération de Site. Après l’échec d’ordinateurs virtuels hello sur tooan réseau virtuel Azure vous pouvez y accéder à l’aide de hello [homologation privée](../expressroute/expressroute-circuit-peerings.md#private-peering) le programme d’installation avec hello réseau virtuel Azure.

### <a name="are-there-any-prerequisites-for-replicating-virtual-machines-tooazure"></a>Existe-t-il des conditions requises pour la réplication des machines virtuelles tooAzure ?
Machines virtuelles tooreplicate tooAzure doit se conformer [conditions requises pour Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

Votre compte d’utilisateur Azure doit toohave certaines [autorisations](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la réplication d’un nouveau tooAzure d’ordinateur virtuel.

### <a name="can-i-replicate-hyper-v-generation-2-virtual-machines-tooazure"></a>Puis-je répliquer tooAzure de 2 machines virtuelles de génération de Hyper-V ?
Oui. Récupération de site convertit à partir de la génération 2 toogeneration 1 pendant le basculement. À la restauration automatique machine de hello est toogeneration arrière convertie 2. [En savoir plus](http://azure.microsoft.com/blog/2015/04/28/disaster-recovery-to-azure-enhanced-and-were-listening/).

### <a name="if-i-replicate-tooazure-how-do-i-pay-for-azure-vms"></a>Si répliquer tooAzure comment pour payer pour les machines virtuelles Azure ?
Lors de la réplication normale, les données sont répliquées de stockage Azure toogeo redondante et vous n’avez pas besoin toopay tous les frais de machine virtuelle Azure IaaS, en fournissant un avantage significatif. Lorsque vous exécutez un tooAzure de basculement, récupération de Site automatiquement crée des machines virtuelles Azure IaaS, et une fois que vous serez facturé pour les ressources de calcul hello vous consommez dans Azure.

### <a name="can-i-automate-site-recovery-scenarios-with-an-sdk"></a>Puis-je automatiser des scénarios Site Recovery avec un kit SDK ?
Oui. Vous pouvez automatiser les workflows de récupération de Site à l’aide de hello API Rest, PowerShell ou hello Azure SDK. Scénarios actuellement pris en charge pour le déploiement de Site Recovery à l’aide de PowerShell :

* [Répliquer des ordinateurs virtuels Hyper-V dans VMM de nuages tooAzure Gestionnaire de ressources de PowerShell](site-recovery-vmm-to-azure-powershell-resource-manager.md)
* [Répliquer des ordinateurs virtuels Hyper-V sans VMM tooAzure Gestionnaire de ressources de PowerShell](site-recovery-deploy-with-powershell-resource-manager.md)

### <a name="if-i-replicate-tooazure-what-kind-of-storage-account-do-i-need"></a>Si vous répliquez tooAzure quel type de compte de stockage dois-je ?
* **Portail Azure classic**: Si vous déployez le Site Recovery Bonjour portail Azure classic, vous devez un [compte de stockage géo-redondant standard](../storage/common/storage-redundancy.md#geo-redundant-storage). Stockage Premium n’est pas pris en charge pour le moment. compte de Hello doit être Bonjour même région que le coffre Site Recovery hello.
* **Portail Azure**: Si vous déployez dans hello portail Azure Site Recovery, vous devez avoir un compte de stockage LRS ou GRS. Nous vous recommandons de GRS afin que les données ne doit pas être si une panne régionale se produit, ou si la région primaire hello ne peut pas être récupérée. compte de Hello doit être Bonjour Services de récupération de la même région que hello coffre. Stockage Premium est maintenant pris en charge pour VMware VM, un ordinateur virtuel Hyper-V et la réplication du serveur physique, lorsque vous déployez le Site Recovery Bonjour portail Azure.

### <a name="how-often-can-i-replicate-data"></a>À quelle fréquence puis-je répliquer les données ?
* **Hyper-V :** les machines virtuelles Hyper-V peuvent être répliquées toutes les 30 secondes (sauf pour le Stockage Premium), 5 minutes ou 15 minutes. Si vous avez configuré une réplication SAN, la réplication est alors synchrone.
* **Serveurs VMware et physiques :** une fréquence de réplication n’est pas pertinente ici. La réplication est continue.

### <a name="can-i-extend-replication-from-existing-recovery-site-tooanother-tertiary-site"></a>Puis-je étendre réplication à partir de la récupération site tooanother tertiaire site existant ?
La réplication étendue ou chaînée n’est pas prise en charge. Demandez cette fonctionnalité dans le [forum de commentaires](http://feedback.azure.com/forums/256299-site-recovery/suggestions/6097959-support-for-exisiting-extended-replication).

### <a name="can-i-do-an-offline-replication-hello-first-time-i-replicate-tooazure"></a>Puis-je faire une hello réplication hors connexion de première que répliquer tooAzure ?
Ceci n’est pas pris en charge. Demander cette fonctionnalité Bonjour [forum de commentaires](http://feedback.azure.com/forums/256299-site-recovery/suggestions/6227386-support-for-offline-replication-data-transfer-from).

### <a name="can-i-exclude-specific-disks-from-replication"></a>Puis-je exclure des disques spécifiques de la réplication ?
Cela est pris en charge lorsque vous êtes [répliquer des ordinateurs virtuels Hyper-V et les ordinateurs virtuels VMware](site-recovery-exclude-disk.md) tooAzure, à l’aide de hello portail Azure.

### <a name="can-i-replicate-virtual-machines-with-dynamic-disks"></a>Puis-je répliquer des machines virtuelles avec des disques dynamiques ?
Les disques dynamiques sont pris en charge lors de la réplication de machines virtuelles Hyper-V. Elles sont également prises en charge lors de la réplication des ordinateurs virtuels VMware et les machines physiques tooAzure. disque de système d’exploitation Hello doit être un disque de base.

### <a name="can-i-add-a-new-machine-tooan-existing-replication-group"></a>Puis-je ajouter un nouveau groupe de réplication existant machine tooan ?
Ajout de nouveaux groupes de réplication tooexisting machines est pris en charge. toodo, sélectionnez le groupe de réplication hello (à partir de 'Éléments répliqué' lame) et un menu contextuel/sélectionner cliquez droit sur le groupe de réplication hello et sélectionnez l’option appropriée de hello.

![Ajouter un groupe tooreplication](./media/site-recovery-faq/add-server-replication-group.png)

### <a name="can-i-throttle-bandwidth-allotted-for-hyper-v-replication-traffic"></a>Puis-je limiter la bande passante allouée pour le trafic de réplication Hyper-V ?
Oui. Vous pouvez en savoir plus sur la limitation de bande passante dans les articles de déploiement hello :

* [Planification de la capacité pour la réplication de machines virtuelles VMware et de serveurs physiques](site-recovery-plan-capacity-vmware.md)
* [Planification de la capacité pour la réplication de machines virtuelles Hyper-V dans des clouds VMM](site-recovery-vmm-to-azure.md#capacity-planning)
* [Planification de la capacité pour la réplication de machines virtuelles Hyper-V sans VMM](site-recovery-hyper-v-site-to-azure.md)

## <a name="failover"></a>Basculement
### <a name="if-im-failing-over-tooazure-how-do-i-access-hello-azure-virtual-machines-after-failover"></a>Si je suis basculement tooAzure, comment accéder hello Azure machines virtuelles après le basculement ?
Vous pouvez accéder à hello machines virtuelles Azure via une connexion Internet sécurisée, via une connexion VPN de site à site ou sur Azure ExpressRoute. Vous devez tooprepare un nombre d’éléments dans l’ordre tooconnect. [En savoir plus](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)


### <a name="if-i-fail-over-tooazure-how-does-azure-make-sure-my-data-is-resilient"></a>Si je basculez tooAzure comment Azure assurer mes données sont résilientes ?
Azure est conçu pour la résilience. Récupération de site est déjà conçue pour basculement tooa Azure centre de données secondaire, conformément aux hello SLA Azure si vous avez besoin de hello survient. Si cela se produit, nous assurer que vos métadonnées et les coffres restent dans hello même région géographique que vous avez choisie pour votre archivage.  

### <a name="if-im-replicating-between-two-datacenters-what-happens-if-my-primary-datacenter-experiences-an-unexpected-outage"></a>Si j’effectue une réplication entre deux centres de données, que se passe-t-il si mon centre de données principal connaît une panne inattendue ?
Vous pouvez déclencher un basculement non planifié à partir du site secondaire de hello. Récupération de site n’a pas besoin de connectivité à partir de basculement de hello tooperform hello site principal.

### <a name="is-failover-automatic"></a>Le basculement est-il automatique ?
Le basculement n’est pas automatique. Lancer de basculements avec un seul clic dans le portail de hello, ou vous pouvez utiliser [PowerShell de récupération de Site](/powershell/module/azurerm.siterecovery) tootrigger un basculement. Échec de retour est une action simple dans le portail Site Recovery hello.

tooautomate, que vous pouvez utiliser localement Orchestrator ou Operations Manager toodetect une défaillance de l’ordinateur virtuel, et puis déclencheur hello basculement à l’aide de hello SDK.

* [Découvrez plus d’informations](site-recovery-create-recovery-plans.md) sur les plans de récupération.
* [En savoir plus](site-recovery-failover.md) sur le basculement.
* [En savoir plus](site-recovery-failback-azure-to-vmware.md) sur la restauration automatique de serveurs physiques et de machines virtuelles VMware

### <a name="if-my-on-premises-host-is-not-responding-or-crashed-can-i-failover-back-tooa-different-host"></a>Si mon hôte local n’est pas répondre ou en panne, puis-je basculement tooa arrière autre ordinateur hôte ?
Oui, vous pouvez utiliser hello autre emplacement toofailback tooa autre ordinateur hôte de récupération à partir d’Azure. En savoir plus sur les options de hello Bonjour liens ci-dessous pour les machines virtuelles VMware et Hyper-v.

* [Pour les machines virtuelles VMware](site-recovery-how-to-failback-azure-to-vmware.md#fail-back-to-the-original-or-alternate-location)
* [Pour les machines virtuelles Hyper-V](site-recovery-failback-from-azure-to-hyper-v.md#failback-to-an-alternate-location)

## <a name="service-providers"></a>Fournisseurs de services
### <a name="im-a-service-provider-does-site-recovery-work-for-dedicated-and-shared-infrastructure-models"></a>Je suis un fournisseur de services. Site Recovery fonctionne-t-il pour les modèles d’infrastructure dédiée ou partagée ?
Oui, Site Recovery prend en charge les modèles d’infrastructure dédiée et partagée.

### <a name="for-a-service-provider-is-hello-identity-of-my-tenant-shared-with-hello-site-recovery-service"></a>Pour un fournisseur de services, est l’identité hello de mon client partagé avec le service de récupération de Site hello ?
Non. L’identité du locataire reste anonyme. Portail de Site Recovery accès toohello n’avez pas besoin vos clients. Seul l’administrateur de fournisseur hello service interagit avec le portail de hello.

### <a name="will-tenant-application-data-ever-go-tooazure"></a>Données d’application client ira jamais tooAzure ?
Lors de la réplication entre les sites appartenant à un fournisseur de service, les données d’application va jamais tooAzure. Données sont chiffrées en transit et répliquées directement entre les sites de fournisseur de service hello.

Si vous effectuez une réplication tooAzure, les données d’application sont envoyées tooAzure stockage mais pas toohello service Site Recovery. Les données sont chiffrées en transit et restent chiffrées dans Azure.

### <a name="will-my-tenants-receive-a-bill-for-any-azure-services"></a>Mes clients recevront-ils une facture pour les services Azure ?
Non. Relation de facturation d’Azure est directement avec le fournisseur de services hello. Les fournisseurs de services sont responsables de la création de factures spécifiques pour leurs locataires.

### <a name="if-im-replicating-tooazure-do-we-need-toorun-virtual-machines-in-azure-at-all-times"></a>Si je suis réplication tooAzure, devons-nous toorun machines virtuelles Azure en permanence ?
Non, les données sont répliquée tooan compte de stockage Azure dans votre abonnement. Lorsque vous effectuez un basculement de test (test de récupération d’urgence) ou un basculement réel, Site Recovery crée automatiquement les machines virtuelles dans votre abonnement.

### <a name="do-you-ensure-tenant-level-isolation-when-i-replicate-tooazure"></a>Assurez-vous d’isolation au niveau du client lorsque tooAzure répliquer ?
Oui.

### <a name="what-platforms-do-you-currently-support"></a>Quelles plates-formes prenez-vous en charge, actuellement ?
Nous prenons en charge Azure Pack et le système Cloud Platform, ainsi que les déploiements basés sur System Center (2012 et versions supérieures). [En savoir plus](https://technet.microsoft.com/library/dn850370.aspx) sur l’intégration d’Azure Pack et de Site Recovery.

### <a name="do-you-support-single-azure-pack-and-single-vmm-server-deployments"></a>Prenez-vous en charge les déploiements uniques de serveurs VMM et Azure Pack ?
Oui, vous pouvez répliquer tooAzure d’ordinateurs virtuels Hyper-V, ou entre les sites de fournisseur de service.  Notez que si vous répliquez entre des sites du fournisseur de services, l’intégration de runbooks Azure n’est pas disponible.

## <a name="next-steps"></a>Étapes suivantes
* Hello de lecture [vue d’ensemble de la récupération de Site](site-recovery-overview.md)
* En savoir plus sur l’ [architecture de Site Recovery](site-recovery-components.md)  
