---
title: "aaaPrerequisites pour tooAzure de réplication à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "En savoir plus sur la configuration requise de hello pour répliquer les machines virtuelles et des machines physiques tooAzure à l’aide du service d’Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: jwhit
editor: tysonn
ms.assetid: e24eea6c-50a7-4cd5-aab4-2c5c4d72ee2d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: rajanaki
ms.openlocfilehash: 0e32ab7cd7c65a3f67ffa2f2c15af189c15b6f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
#  <a name="prerequisites-for-replication-from-on-premises-tooazure-by-using-site-recovery"></a>Conditions préalables pour la réplication à partir de tooAzure local à l’aide de récupération de Site

> [!div class="op_single_selector"]
> * [Répliquer à partir d’Azure tooAzure](site-recovery-azure-to-azure-prereq.md)
> * [Répliquer à partir de local tooAzure](site-recovery-prereq.md)

Azure Site Recovery peut vous aider à prendre en charge votre stratégie de récupération d’urgence et de continuité d’activité entreprise en coordonnant la réplication d’une machine virtuelle Azure (VM) de tooanother région Azure. Récupération de site est également répliqué serveurs physiques locaux et les machines virtuelles toohello cloud (Azure) ou tooa de centre de données secondaire. Si une panne se produit sur votre site principal, vous pouvez basculer tooa emplacement secondaire tookeep applications et charges de travail disponibles. Vous pouvez échouer emplacement principal de tooyour arrière lorsque l’emplacement principal de hello retourne les opérations de toonormal. Pour plus d’informations sur Site Recovery, consultez la page [Qu’est-ce que Site Recovery ?](site-recovery-overview.md)

Dans cet article, nous résument les conditions préalables de hello pour le début de la réplication de récupération de Site à partir d’un tooAzure d’ordinateur local.

Vous pouvez valider les commentaires en bas de hello d’article de hello. Vous pouvez également poser des questions techniques dans hello [forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="azure-requirements"></a>Conditions requises pour Azure

**Prérequis** | **Détails**
--- | ---
**Compte Azure** | Un [compte Microsoft Azure](http://azure.microsoft.com/). Vous pouvez commencer par une version d’ [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).
**Service Site Recovery** | Pour plus d’informations sur la tarification pour hello service Azure Site Recovery, consultez [tarification de la récupération de Site](https://azure.microsoft.com/pricing/details/site-recovery/). |
**Azure Storage** | Vous avez besoin d’un stockage Azure compte toostore répliquée de données. compte de stockage Hello doit être Bonjour Azure Recovery Services de la même région que hello coffre. Des machines virtuelles Azure sont créées en cas de basculement.<br/><br/> Selon le modèle de ressource hello souhaitée toouse pour le basculement de la machine virtuelle Azure, vous pouvez configurer un compte à l’aide de hello [modèle de déploiement Azure Resource Manager](../storage/common/storage-create-storage-account.md) ou hello [modèle de déploiement classique](../storage/common/storage-create-storage-account.md).<br/><br/>Vous pouvez utiliser le [stockage géoredondant](../storage/common/storage-redundancy.md#geo-redundant-storage) ou le stockage localement redondant. Nous vous recommandons d’utiliser le stockage géo-redondant. Avec un stockage géo-redondant, les données sont résilientes si une panne régionale se produit, ou si la région primaire hello ne peut pas être récupérée.<br/><br/> Vous pouvez utiliser un compte de stockage Azure standard ou Azure Premium. Le [stockage Premium](https://docs.microsoft.com/azure/storage/storage-premium-storage) est généralement utilisé pour les machines virtuelles nécessitant des performances d’E/S élevées et une faible latence. Avec le stockage Premium, une machine virtuelle peut héberger des charges de travail nécessitant beaucoup d’E/S. Si vous utilisez un stockage Premium pour les données répliquées, il vous faut également un compte de stockage standard. Un compte de stockage standard stocke les journaux de réplication qui capturent des données de site tooon les changements en cours.<br/><br/>
**Limites de stockage** | Vous ne peut pas déplacer les comptes de stockage que vous utilisez dans le groupe de ressources différent de tooa de récupération de Site ou déplacer utilisez tooor avec un autre abonnement.<br/><br/> Actuellement, toopremium des comptes de stockage dans le centre de l’Inde et de l’Inde du Sud de réplication n’est pas disponible.
**Réseau Azure** | Vous avez besoin d’un réseau Azure, connecter des machines virtuelles Azure de toowhich après le basculement. réseau Azure Hello doit être Bonjour Services de récupération de la même région que hello coffre.<br/><br/> Bonjour portail Azure, vous pouvez créer un réseau Azure à l’aide de hello [modèle de déploiement Resource Manager](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) ou hello [modèle de déploiement classique](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).<br/><br/> Si vous répliquez à partir de System Center Virtual Machine Manager (VMM) tooAzure, vous devez configurer le mappage réseau entre les réseaux VMM VM et Azure. Cela garantit que les machines virtuelles Azure connecter tooappropriate réseaux après le basculement.
**Limitations du réseau** | Vous ne peut pas déplacer les comptes de réseau que vous utilisez dans le groupe de ressources différent de tooa de récupération de Site ou déplacer utilisez tooor avec un autre abonnement.
**Mappage réseau** | Si vous répliquez des machines virtuelles Microsoft Hyper-V dans des clouds VMM, vous devez configurer le mappage réseau. Cela garantit que les machines virtuelles Azure se connecter tooappropriate réseaux lorsqu’ils sont créés après le basculement.

> [!NOTE]
> Hello sections suivantes décrivent des conditions préalables de hello pour les différents composants de l’environnement client hello. Pour plus d’informations sur la prise en charge des configurations spécifiques, consultez hello [matrice de prise en charge](site-recovery-support-matrix.md).
>

## <a name="disaster-recovery-of-vmware-vms-or-physical-windows-or-linux-servers-tooazure"></a>Récupération d’urgence des ordinateurs virtuels VMware ou tooAzure de serveurs physique Windows ou Linux
Hello suivant des composants est requis pour la récupération d’urgence des ordinateurs virtuels VMware ou serveurs physiques de Windows ou Linux. En outre, il s’agit toohello celles décrites dans [conditions requises pour Azure](#azure-requirements).


### <a name="configuration-server-or-additional-process-server"></a>Serveur de configuration ou serveur de traitement supplémentaire

Configurer un ordinateur local comme hello configuration serveur tooorchestrate entre deux sites locaux hello et Azure. ordinateur local, Hello gère également la réplication des données. <br/></br>

*   **Conditions préalables pour l’hôte VMware vCenter ou vSphere**

    | **Composant** | **Configuration requise** |
    | --- | --- |
    | **vSphere** | Vous avez besoin d’un ou de plusieurs hyperviseurs VMware vSphere.<br/><br/>Hyperviseurs doivent être en cours d’exécution vSphere version 5.1, 5.5 ou 6.0 avec hello dernières mises à jour.<br/><br/>Nous recommandons que vSphere hôtes et serveurs vCenter que tous deux être Bonjour même réseau que le serveur de processus hello. Sauf si vous avez configuré un serveur dédié, il s’agit de réseau hello où se trouve le serveur de configuration hello. |
    | **vCenter** | Nous vous recommandons de déployer un toomanage de serveur VMware vCenter vos hôtes vSphere. Il doit être exécuté vCenter version 6.0 ou 5.5, avec les dernières mises à jour de hello.<br/><br/>**Limitation** : Site Recovery ne prend pas en charge la réplication entre des instances de vCenter vMotion. Storage DRS et Storage vMotion ne sont pas non plus pris en charge sur une machine virtuelle cible maître après une opération de reprotection.||

* **Configuration requise pour les machines répliquées**

    | **Composant** | **Configuration requise** |
    | --- | --- |
    | **Machines locales** (machines virtuelles VMware) | Les outils VMware doivent être installés et en cours d’exécution sur les machines virtuelles répliquées.<br/><br/> Les machines virtuelles doivent répondre aux [conditions préalables Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) pour la création d’une machine virtuelle Azure.<br/><br/>La capacité du disque sur chaque ordinateur protégé ne peut pas être supérieure à 1 023 Go. <br/><br/>2 Go d’espace disponible sur le lecteur d’installation hello minimale est requise pour l’installation du composant.<br/><br/>Si vous souhaitez que la cohérence multimachine virtuelle de tooenable, port 20004 doit être ouvert sur le pare-feu local de machine virtuelle hello.<br/><br/>Le nom des machines doit contenir entre 1 et 63 caractères (lettres, chiffres et tirets). Hello doit commencer par une lettre ou un chiffre et se terminer par une lettre ou un chiffre. <br/><br/>Une fois que vous avez activé la réplication pour un ordinateur, vous pouvez modifier hello nom Azure.<br/><br/> |
    | **Ordinateurs Windows** (serveur physique ou VMware) | Hello ordinateur doit être en cours d’exécution suivantes hello pris en charge les systèmes d’exploitation 64 bits : <br/>- Windows Server 2012 R2<br/>- Windows Server 2012<br/>-Windows Server 2008 R2 avec SP1 ou version ultérieure<br/><br/> Hello système d’exploitation doit être installé sur le lecteur C. le disque hello du système d’exploitation doit être un disque de base de Windows et non dynamique. disque de données Hello peut être dynamique.<br/><br/>|
    | **Ordinateurs Linux** (serveur physique ou VMware) | Hello ordinateur doit être en cours d’exécution suivantes hello pris en charge les systèmes d’exploitation 64 bits : <br/>- Red Hat Enterprise Linux 7.2, 7.1, 6.8 ou 6.7<br/>- Centos 7.2, 7.1, 7.0, 6.8, 6.7, 6.6 ou 6.5<br/>- Serveur Ubuntu 14.04 LTS (pour obtenir la liste des versions de noyau prises en charge pour Ubuntu, voir les [systèmes d’exploitation pris en charge](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions))<br/>-Noyau de compatible Hat Enterprise Linux version 6.5 ou 6.4, en cours d’exécution soit hello rouge oracle ou insécable Enterprise noyau version 3 (UEK3)<br/>-SUSE Linux Enterprise Server 11 SP4 ou SUSE Linux Enterprise Server 11 SP3<br/><br/>Vos fichiers/etc/hosts sur les ordinateurs protégés doivent disposer d’entrées qui mappent des adresses de tooIP du nom d’hôte local hello associés à toutes les cartes réseau.<br/><br/>Après un basculement, si vous souhaitez tooconnect tooan machine virtuelle Azure exécutant Linux à l’aide d’un client Secure Shell (SSH), assurez-vous que le service SSH hello sur l’ordinateur de hello protégé est défini toostart automatiquement au démarrage du système. Assurez-vous également que les règles de pare-feu autorisent une machine toohello protégé de connexion SSH.<br/><br/>nom d’hôte Hello, des points de montage, noms de périphériques et chemins d’accès de système de Linux et les noms de fichiers (par exemple, trouver et /usr) doivent être en anglais uniquement.<br/><br/>Hello suivants répertoires (si configuré en tant que partitions distinctes ou des systèmes de fichiers) doit être sur hello même disque (disque hello du système d’exploitation) sur le serveur de source de hello :<br/>- / (racine)<br/>- /boot<br/>- /usr<br/>- /usr/local<br/>- /var<br/>- /etc<br/><br/>Actuellement, les fonctionnalités XFS v5, telles que les sommes de contrôle de métadonnées, ne sont pas prises en charge par Site Recovery sur les systèmes de fichiers XFS. Assurez-vous que vos systèmes de fichiers XFS n’utilisent pas de fonctionnalités v5. Vous pouvez utiliser superbloc XFS de hello xfs_info utilitaire toocheck hello pour la partition de hello. Si **ftype** est défini trop**1**, XFS v5 fonctionnalités sont utilisées.<br/><br/>Sur les serveurs Red Hat Enterprise Linux 7 et CentOS 7, utilitaire de lsof hello doit être installé et disponible.<br/><br/>


## <a name="disaster-recovery-of-hyper-v-vms-tooazure-no-vmm"></a>Récupération d’urgence des ordinateurs virtuels Hyper-V tooAzure (sans VMM)

Hello suivant des composants est requis pour la récupération d’urgence de machines virtuelles de Hyper-V dans les clouds VMM. En outre, il s’agit toohello celles décrites dans [conditions requises pour Azure](#azure-requirements).

| **Configuration requise** | **Détails** |
| --- | --- |
| **Hôte Hyper-V** |Un ou plusieurs serveurs sur site doivent exécuter Windows Server 2012 R2 avec les dernières mises à jour de hello et rôle hello Hyper-V est activé ou Microsoft Hyper-V Server 2012 R2.<br/><br/>Les serveurs Hyper-V doivent avoir une ou plusieurs machines virtuelles.<br/><br/>Serveurs Hyper-V doivent être connecté toohello Internet, directement ou via un proxy.<br/><br/>Serveurs Hyper-V doivent avoir des correctifs hello décrites dans l’article de Base de connaissances hello [2961977](https://support.microsoft.com/kb/2961977) installé.
|**Fournisseur et agent**| Pendant le déploiement de la récupération de Site, vous installez le fournisseur Azure Site Recovery hello. installation du fournisseur Hello installe également hello Azure Recovery Services agent sur chaque serveur Hyper-V qui exécute des machines virtuelles, vous souhaitez tooprotect. <br/><br/>Tous les serveurs Hyper-V dans le coffre doit avoir une récupération de Site hello les mêmes versions de fournisseur de hello et l’agent de hello.<br/><br/>fournisseur de Hello doit tooconnect tooSite récupération sur hello Internet. Le trafic peut être envoyé directement ou via un proxy. Le protocole HTTPS basé sur proxy n’est pas pris en charge. Hello proxy doit permettre le toohello accès aux URL suivantes :<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/>Si vous avez des règles de pare-feu basé sur l’adresse IP sur le serveur de hello, assurez-vous que les règles de hello autorisent tooAzure de communication.<br/><br/> Autoriser hello [plages d’adresses IP de centre de données Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)et HTTPS (port 443).<br/><br/> Autoriser les plages d’adresses IP pour hello région Azure de votre abonnement et pourquoi l’ouest des États-Unis (utilisé pour la gestion de contrôle et l’identité de l’accès).


## <a name="disaster-recovery-of-hyper-v-vms-in-vmm-clouds-tooazure"></a>TooAzure des clouds de récupération d’urgence des ordinateurs virtuels Hyper-V dans VMM

Hello suivant des composants est requis pour la récupération d’urgence de machines virtuelles de Hyper-V dans les clouds VMM. En outre, il s’agit toohello celles décrites dans [conditions requises pour Azure](#azure-requirements).

| **Configuration requise** | **Détails** |
| --- | --- |
| **Virtual Machine Manager** |Vous devez avoir un ou plusieurs serveurs VMM s’exécutant sous System Center 2012 R2 ou une version ultérieure. Chaque serveur VMM doit être associé à un ou plusieurs clouds configurés. <br/><br/>Un cloud doit avoir :<br/>- Un ou plusieurs groupes hôtes VMM.<br/>- Un ou plusieurs serveurs hôtes Hyper-V ou clusters dans chaque groupe hôte.<br/><br/>Pour plus d’informations sur la configuration des clouds VMM, consultez [comment toocreate un cloud dans Virtual Machine Manager 2012](http://social.technet.microsoft.com/wiki/contents/articles/2729.how-to-create-a-cloud-in-vmm-2012.aspx). |
| **Hyper-V** |Serveurs de l’hôte Hyper-V doivent exécuter au moins Windows Server 2012 R2 avec le rôle hello Hyper-V activé ou Microsoft Hyper-V Server 2012 R2. dernières mises à jour de Hello doivent être installés.<br/><br/> Un serveur Hyper-V doivent avoir une ou plusieurs machines virtuelles.<br/><br/> Un serveur hôte Hyper-V ou un cluster qui inclut les machines virtuelles que vous souhaitez tooreplicate doit être géré dans un cloud VMM.<br/><br/>Serveurs Hyper-V doivent être connecté toohello Internet, directement ou via un proxy.<br/><br/>Serveurs Hyper-V doivent avoir des correctifs hello décrites dans l’article de Base de connaissances hello [2961977](https://support.microsoft.com/kb/2961977) installé.<br/><br/>Les serveurs hôte Hyper-V doivent accéder à Internet pour tooAzure de réplication de données. |
| **Fournisseur et agent** |Pendant le déploiement d’Azure Site Recovery, installez le fournisseur Azure Site Recovery sur le serveur VMM de hello. Installez l’agent Recovery Services sur des hôtes Hyper-V. l’agent et le fournisseur de hello doivent tooconnect tooAzure directement hello Internet ou via un proxy. Les proxies basés sur HTTPS ne sont pas pris en charge. serveur de proxy Hello sur le serveur VMM de hello et hôtes Hyper-V doit autoriser l’accès à : <br/><br/>[!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)] <br/><br/>Si vous avez des règles de pare-feu basé sur l’adresse IP sur le serveur VMM de hello, assurez-vous que les règles de hello autorisent tooAzure de communication.<br/><br/> Autoriser hello [plages d’adresses IP de centre de données Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) et HTTPS (port 443).<br/><br/>Autoriser les plages d’adresses IP pour hello région Azure pour votre abonnement et hello ouest des États-Unis (utilisé pour la gestion de contrôle et l’identité de l’accès).<br/><br/> |

### <a name="replicated-machine-prerequisites"></a>Configuration requise pour les machines répliquées

| **Composant** | **Détails** |
| --- | --- |
| **Machines virtuelles protégées** | Site Recovery fonctionne sur tous les systèmes d’exploitation pris en charge par [Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx).<br/><br/>Machines virtuelles doivent respecter hello [conditions préalables Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) pour la création d’une machine virtuelle Azure. Le nom des machines doit contenir entre 1 et 63 caractères (lettres, chiffres et tirets). Hello doit commencer par une lettre ou un chiffre et se terminer par une lettre ou un chiffre. <br/><br/>Vous pouvez modifier le nom d’ordinateur virtuel hello une fois que vous avez activé la réplication pour hello machine virtuelle. <br/><br/> La capacité du disque pour chaque ordinateur protégé ne peut pas être supérieure à 1 023 Go. Une machine virtuelle peut avoir des disques too16 (haut too16 to).<br/><br/>


## <a name="disaster-recovery-of-hyper-v-vms-in-vmm-clouds-tooa-customer-owned-site"></a>Récupération d’urgence des ordinateurs virtuels Hyper-V dans VMM des clouds de site appartenant à un client de tooa

Hello suivant des composants est requis pour la récupération d’urgence de site appartenant à un client VMM clouds tooa machines virtuelles Hyper-V. En outre, il s’agit toohello celles décrites dans [conditions requises pour Azure](#azure-requirements).

| **Composant** | **Détails** |
| --- | --- |
| **Virtual Machine Manager** |  Nous vous recommandons de déployer un serveur VMM sur le site principal de hello et site secondaire de hello.<br/><br/> Vous pouvez [effectuer la réplication entre des clouds sur un seul serveur VMM](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment). tooreplicate entre des clouds sur un seul serveur VMM, vous devez au moins deux clouds configurés sur le serveur VMM de hello.<br/><br/> Serveurs VMM doivent exécuter au moins System Center 2012 SP1, avec les dernières mises à jour de hello.<br/><br/> Chaque serveur VMM doit disposer d’un ou de plusieurs clouds. Tous les clouds doivent avoir hello qu'ensemble de profils de capacité Hyper-V. <br/><br/>Les clouds doivent contenir un ou plusieurs groupes hôtes VMM. Pour plus d’informations sur la configuration des clouds VMM, voir [Préparer le déploiement d’Azure Site Recovery](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric). |
| **Hyper-V** | Serveurs Hyper-V doivent être en cours d’exécution au moins Windows Server 2012 avec un rôle de hello Hyper-V activé et avoir hello les dernières mises à jour installées.<br/><br/> Un serveur Hyper-V doivent avoir une ou plusieurs machines virtuelles.<br/><br/>  Les serveurs hôte Hyper-V doivent se trouver dans des groupes hôtes dans des clouds VMM principaux et secondaires hello.<br/><br/> Si vous exécutez Hyper-V dans un cluster Windows Server 2012 R2, nous vous recommandons d’installer décrite dans l’article de la Base de connaissances de la mise à jour hello [2961977](https://support.microsoft.com/kb/2961977).<br/><br/> Si vous exécutez Hyper-V dans un cluster sous Windows Server 2012, notez que le répartiteur de clusters n’est pas créé automatiquement si vous avez un cluster basé sur des adresses IP statiques. Vous devez configurer manuellement le service broker de cluster hello. Pour plus d’informations sur le service broker de cluster hello, consultez [rôle du service broker du réplica hello configurer pour la réplication de cluster à cluster](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx). |
| **Fournisseur** | Pendant le déploiement de la récupération de Site, installez le fournisseur Azure Site Recovery hello sur les serveurs VMM. fournisseur de Hello communique avec Site Recovery sur la réplication tooorchestrate HTTPS (port 443). Réplication de données se produit entre hello serveurs principaux et secondaires Hyper-V hello LAN ou via une connexion VPN.<br/><br/> fournisseur Hello qui s’exécute sur le serveur VMM de hello a besoin d’accéder à toohello URL suivantes :<br/><br/>[!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)] <br/><br/>le fournisseur Site Recovery Hello doit autoriser la communication de pare-feu de hello VMM serveurs toohello [plages d’adresses IP de centre de données Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)et autoriser le protocole HTTPS (port 443) de hello. |


## <a name="url-access"></a>Accès URL
Ces URL doivent être disponibles depuis VMware, VMM et les serveurs hôtes Hyper-V :

|**URL** | **VMM tooVMM** | **VMM tooAzure** | **Hyper-V tooAzure** | **VMware tooAzure** |
|--- | --- | --- | --- | --- |
|``*.accesscontrol.windows.net`` | AUTORISER | Autoriser | Autoriser | Autoriser |
|``*.backup.windowsazure.com`` | Non requis | Autoriser | Autoriser | Autoriser |
|``*.hypervrecoverymanager.windowsazure.com`` | Autoriser | Autoriser | Autoriser | Autoriser |
|``*.store.core.windows.net`` | Autoriser | Autoriser | Autoriser | Autoriser |
|``*.blob.core.windows.net`` | Non requis | Autoriser | Autoriser | Autoriser |
|``https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi`` | Non requis | Non requis | Non requis | Autoriser le téléchargement SQL |
|``time.windows.com`` | AUTORISER | Autoriser | Autoriser | Autoriser|
|``time.nist.gov`` | Autoriser | Autoriser | Autoriser | AUTORISER |
