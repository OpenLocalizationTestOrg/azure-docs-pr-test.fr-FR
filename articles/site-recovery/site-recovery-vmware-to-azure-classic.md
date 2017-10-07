---
title: les ordinateurs virtuels VMware aaaReplicate et tooAzure des serveurs physiques dans hello portail classique | Documents Microsoft
description: "Cet article décrit comment la réplication tooorchestrate toodeploy Azure Site Recovery, le basculement et récupération de locaux des ordinateurs virtuels VMware et tooAzure des serveurs physiques Windows/Linux."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: a9022c1f-43c1-4d38-841f-52540025fb46
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-vmware-to-azure
ms.openlocfilehash: f85e4139ad45552ce963072e14d71d279bb7dac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-and-physical-servers-tooazure-with-azure-site-recovery"></a>Répliquer des machines virtuelles VMware et tooAzure des serveurs physiques avec Azure Site Recovery
> [!div class="op_single_selector"]
> * [Hello portail Azure](site-recovery-vmware-to-azure.md)
> * [portail classique de Hello](site-recovery-vmware-to-azure-classic.md)
> * [portail classique de Hello (hérité)](site-recovery-vmware-to-azure-classic-legacy.md)
>
>

Hello service Azure Site Recovery contribue tooyour continuité des activités et la stratégie de récupération d’urgence en coordonnant la réplication, le basculement et récupération des ordinateurs virtuels et des serveurs physiques. Machines peuvent être répliquée tooAzure ou centre de données secondaire locale tooa. Pour une présentation rapide de ce service, consultez l’article [Qu’est-ce qu’Azure Site Recovery ?](site-recovery-overview.md).

## <a name="overview"></a>Vue d’ensemble
Cet article explique comment :

* **Répliquer tooAzure de machines virtuelles VMware**: réplication toocoordinate de déployer la récupération de Site, le basculement et récupération d’un stockage tooAzure machines virtuelles VMware local.
* **Répliquer les serveurs physiques tooAzure**: la réplication toocoordinate déployer Azure Site Recovery, le basculement et récupération de local physiques Windows et Linux serveurs tooAzure.

> [!NOTE]
> Cet article décrit comment tooreplicate tooAzure. Si vous souhaitez tooreplicate les ordinateurs virtuels VMware ou Windows/Linux serveurs physiques tooa centre de données secondaire, consultez [VMware de récupération de Site tooVMware](site-recovery-vmware-to-vmware.md).
>
>

Valider des commentaires ou des questions bas hello de cet article ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="enhanced-deployment"></a>Déploiement amélioré
Cet article contient des instructions pour un déploiement améliorée Bonjour portail Azure classic. Nous vous conseillons d’utiliser cette version pour tous les nouveaux déploiements. Si vous avez déjà déployé par à l’aide de hello hérité antérieure, nous vous recommandons de migrer toohello nouvelle version. Pour plus d’informations sur la migration, consultez [classique de tooAzure VMware de récupération de Site hérité](site-recovery-vmware-to-azure-classic-legacy.md#migrate-to-the-enhanced-deployment).

déploiement de Hello amélioré est une mise à jour majeure. Voici un récapitulatif des améliorations hello que nous avons fait :

* **Aucune infrastructure de machines virtuelles dans Azure**: les données sont répliquées directement compte de stockage Azure tooan. En outre, n’a aucune tooset besoin de toutes les machines virtuelles d’infrastructure (comme serveur de configuration ou le serveur cible maître) pour la réplication et de basculement était nécessaire dans un déploiement hérité de hello.  
* **Installation unifiée**: une seule installation offre une configuration simple et l’extensibilité des composants locaux.
* **Déploiement sécurisé** : l’ensemble du trafic est chiffré et les communications de gestion de la réplication sont envoyées par le biais du port HTTPS 443.
* **Points de récupération** : prise en charge des points de récupération après incident cohérents avec les applications pour les environnements Windows et Linux, et prise en charge des configurations avec machine virtuelle unique et machines virtuelles multiples.
* **Test de basculement**: prise en charge de tooAzure de basculement de test sans interruption de service sans affecter la production ou la suspension de la réplication.
* **Basculement non planifié**: prise en charge de tooAzure basculement non planifié avec une tooautomatically une meilleure option Arrêter les ordinateurs virtuels avant le basculement.
* **La restauration automatique**: la restauration automatique intégrée qui réplique uniquement les modifications de delta dans toohello site local.
* **vSphere 6.0** : prise en charge limitée des déploiements VMware vSphere 6.0.

## <a name="how-does-site-recovery-help-protect-virtual-machines-and-physical-servers"></a>Comment Site Recovery permet-il de protéger des serveurs physiques et virtuels ?
* Les administrateurs de VMware peuvent configurer des dispositifs de protection hors site tooprotect Azure à partir de charges de travail métier et les applications qui s’exécutent sur des ordinateurs virtuels VMware. Gestionnaires de serveur peuvent répliquer tooAzure de serveurs Windows et Linux physique local.
* console de récupération de Site Azure Hello fournit un emplacement unique pour le programme d’installation simple et gestion des processus de récupération, le basculement et la réplication.
* Si vous répliquez des machines virtuelles VMware gérées par un serveur vCenter, Site Recovery peut automatiquement détecter ces machines virtuelles. Si les ordinateurs se trouvent sur un ordinateur hôte ESXi, Site Recovery détecte les ordinateurs virtuels sur l’ordinateur hôte de hello.
* Si vous exécutez des basculements facile à partir de votre tooAzure d’infrastructure sur site, vous pouvez ne sauvegarder (restauration) à partir de serveurs de machine virtuelle Azure tooVMware dans le site local de hello.
* Vous pouvez configurer les plans de récupération qui regroupent des charges de travail d’application hiérarchisées sur plusieurs machines. Si vous basculez de ces plans, Site Recovery cohérence multimachine virtuelle afin que les machines en cours d’exécution hello mêmes charges de travail peuvent être récupérées ensemble point de cohérence des données tooa.

## <a name="supported-operating-systems"></a>Systèmes d’exploitation pris en charge
### <a name="windows-64-bit-only"></a>Windows (64 bits uniquement)
* Windows Server 2008 R2 SP1+
* Windows Server 2012
* Windows Server 2012 R2

### <a name="linux-64-bit-only"></a>Linux (64 bits uniquement)
* Red Hat Enterprise Linux 6.7, 7.1 et 7.2
* CentOS 6.5, 6.6, 6.7, 7.0, 7.1 et 7.2
* Noyau de Oracle Enterprise Linux 6.4 et 6.5 en cours d’exécution soit hello Red Hat compatible ou insécable Enterprise noyau version 3 (UEK3)
* SUSE Linux Enterprise Server 11 SP3

## <a name="scenario-architecture"></a>Architecture du scénario
Composants du scénario :

* **Un serveur d’administration local**: serveur d’administration hello exécute les composants de Site Recovery :
  * **Serveur de configuration** : coordonne la communication et gère les processus de réplication et de récupération des données.
  * **Serveur de traitement** : fait office de passerelle de réplication. Il reçoit des données à partir d’ordinateurs de la source protégée ; Il optimise avec la mise en cache, la compression et le chiffrement ; envoie la réplication tooAzure stockage des données et. Il gère l’installation push du ordinateurs tooprotected du service mobilité et effectue la détection automatique des ordinateurs virtuels VMware.
  * **Serveur cible maître**: gère les données de réplication pendant la restauration automatique à partir d’Azure.
    Vous pouvez également déployer un serveur d’administration qui agit uniquement comme un tooscale de serveur de processus de votre déploiement.
* **Hello service mobilité**: ce composant est déployé sur chaque ordinateur que vous souhaitez tooreplicate tooAzure (VMware VM ou serveur physique). Il capture les écritures de données sur l’ordinateur de hello et les transfère un serveur de processus toohello.
* **Azure**: vous n’avez pas besoin toocreate toutes les machines virtuelles Azure toohandle réplication et le basculement. Hello service Site Recovery gère la gestion des données et les données sont répliquées directement tooAzure stockage. Machines virtuelles répliquées de Azure sont lancés automatiquement uniquement en cas de basculement tooAzure. Toutefois, si vous souhaitez toofail depuis Azure toohello sur site local, vous devez tooset des tooact d’une machine virtuelle Azure en tant que processus serveur.

Hello graphique (créée par Henry Robalino) suivant montre comment ces composants interagissent :

![Architecture des composants](./media/site-recovery-vmware-to-azure/v2a-architecture-henry.png)

## <a name="capacity-planning"></a>Planification de la capacité
Lorsque vous planifiez la capacité, voici ce que vous devez toothink sur :

* **l’environnement source Hello**: capacité planification ou hello VMware infrastructure et la source de configuration requise.
* **serveur d’administration Hello**: la planification de hello local serveurs d’administration qui exécutent les composants de Site Recovery.
* **La bande passante réseau à partir de la source tootarget**: planification de la bande passante requise pour la réplication entre la source de hello et Azure.

### <a name="source-environment-considerations"></a>Considérations relatives à l’environnement source
* **Taux de modification quotidien maximum** : une machine protégée ne peut utiliser qu’un serveur de traitement. Un serveur de processus unique peut gérer des too2 to de données modifier par jour. 2 To est donc maximale des données quotidiennes hello modifier taux est prise en charge pour un ordinateur protégé.
* **Débit maximal**: un ordinateur répliqué peut appartenir tooone compte de stockage dans Azure. Un compte de stockage standard peut gérer un maximum de 20 000 demandes par seconde, et nous vous recommandons de conserver nombre hello d’IOPS sur un too20 machine source, 000. Par exemple, si vous disposez d’un ordinateur source avec 5 disques, et chaque disque génère 120 e/s (taille de 8 Ko) sur la source de hello, il sera dans hello Azure limite des e/s de disque de 500 par. Hello du nombre de comptes de stockage requise = source total IOPs/20 000.

### <a name="management-server-considerations"></a>Considérations relatives aux serveurs d’administration
serveur d’administration Hello exécute les composants de Site Recovery qui gèrent l’optimisation des données, réplication et gestion. Il doit être en mesure de toohandle hello quotidienne modification capacité dans toutes les charges de travail en cours d’exécution sur les ordinateurs protégés, et il a suffisamment de bande passante toocontinuously répliquer tooAzure le stockage de données. Plus précisément :

* serveur de processus Hello reçoit des données de réplication à partir des ordinateurs protégés et optimise les demandes avec la mise en cache, la compression et le chiffrement avant de l’envoyer tooAzure. serveur d’administration Hello doit avoir suffisamment tooperform de ressources, ces tâches.
* serveur de processus Hello utilise le cache disque. Nous vous recommandons d’un disque distinct du cache de 600 Go ou plus de modifications données toohandle stockées dans l’événement hello de goulot d’étranglement du réseau ou d’une panne. Au cours du déploiement, vous pouvez configurer le cache de hello sur n’importe quel lecteur qui a au moins 5 Go de stockage disponible, mais 600 Go est recommandation minimale de hello.
* Comme meilleure pratique, nous vous recommandons de ce serveur d’administration hello se trouve sur hello même réseau et le segment de réseau local en tant que machines que vous voulez tooprotect de hello. Il peut se trouver sur un autre réseau, mais que vous souhaitez tooprotect doit avoir tooit de visibilité réseau L3 de machines.

Recommandations de taille pour le serveur d’administration hello sont résumées dans hello tableau suivant :

| **Unité centrale de serveur d’administration** | **Mémoire** | **Taille du disque cache** | **Taux de modification des données** | **Machines protégées** |
| --- | --- | --- | --- | --- |
| 8 processeurs virtuels (2 sockets * 4 cœurs à 2,5 GHz) |16 Go |300 Go |500 Go ou moins |Déployer un serveur d’administration avec ces paramètres de tooreplicate moins de 100 ordinateurs. |
| 12 processeurs virtuels (2 sockets * 6 cœurs à 2,5 GHz) |18 Go |600 Go |500 Go too1 to |Déployer un serveur d’administration avec ces ordinateurs de 100 à 150 tooreplicate paramètres. |
| 16 processeurs virtuels (2 sockets * 8 cœurs à 2,5 GHz) |32 Go |1 To |1 to too2 to |Déployer un serveur d’administration avec ces ordinateurs de 150 et 200 tooreplicate paramètres. |
| Déployer un autre serveur de traitement | | |> 2 To |Déployer des serveurs de traitement supplémentaires si vous effectuez une réplication plus de 200 ordinateurs, ou si des modifications des données quotidiennes de hello taux dépasse 2 To. |

Où :

* Chaque ordinateur source est configuré avec 3 disques de 100 Go chacune.
* Nous avons utilisé le stockage de référence de 8 disques SAS de 10 000 tr/min avec RAID 10 pour les mesures de disque cache.

### <a name="network-bandwidth-from-source-tootarget"></a>Bande passante réseau à partir de la source tootarget
Assurez-vous que vous calculez la bande passante hello qui subordonnée nécessaire pour la réplication initiale et la réplication delta à l’aide de hello [outil capacity planner](site-recovery-capacity-planner.md).

#### <a name="throttling-bandwidth-used-for-replication"></a>Limitation de la bande passante utilisée pour la réplication
VMware le trafic de réplication tooAzure passe par un serveur de processus spécifique. Vous pouvez limiter la bande passante hello qui est disponible pour la réplication de Site Recovery sur ce serveur comme suit :

1. Ouvrez hello le composant logiciel enfichable MMC Microsoft Azure Backup sur le serveur d’administration principal de hello ou sur un serveur d’administration en cours d’exécution supplémentaires mis en service des serveurs de traitement. Par défaut, un raccourci pour Microsoft Azure Backup est créé sur le bureau de hello. Vous le trouverez également sous C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Dans le composant logiciel enfichable hello, cliquez sur **modifier les propriétés**.

    ![Modifier les propriétés de limitation de la bande passante](./media/site-recovery-vmware-to-azure-classic/throttle1.png)
3. Sur hello **limitation** onglet, spécifiez la bande passante hello qui peut être utilisée pour la réplication de Site Recovery et hello planification applicable.

    ![Limiter la bande passante utilisée pour la réplication](./media/site-recovery-vmware-to-azure-classic/throttle2.png)

Vous pouvez également définir une limitation à l’aide de PowerShell. Voici un exemple :

    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth (512*1024) -NonWorkHourBandwidth (2048*1024)

#### <a name="maximizing-bandwidth-usage"></a>Optimisation de l’utilisation de la bande passante
tooincrease hello la bande passante utilisée pour la réplication par Azure Site Recovery, vous devez toochange une clé de Registre.

Hello contrôles clés suivants hello nombre de threads par réplication de disque qui sont utilisés lors de la réplication :

    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication\UploadThreadsPerVM

 Dans un réseau surapprovisionnée, cette clé de Registre doit toobe modifié à partir de ses valeurs par défaut. Nous prenons en charge un maximum de 32 threads.  

Pour plus d’informations sur la planification détaillée de la capacité, consultez [Site Recovery Capacity Planner](site-recovery-capacity-planner.md).

### <a name="additional-process-servers"></a>Serveurs de traitement supplémentaires
Si vous avez besoin de tooprotect plus de 200 ordinateurs ou votre taux de modification quotidien est supérieure à 2 To, vous pouvez ajouter des serveurs supplémentaires toohandle hello charge. tooscale out, vous pouvez :

* Augmentez le nombre hello des serveurs d’administration. Par exemple, vous pouvez protéger les machines too400 avec deux serveurs d’administration.
* Ajouter des serveurs de traitement supplémentaires et utiliser ces serveur d’administration hello toohandle le trafic au lieu de (ou en plus).

Ce tableau décrit un scénario dans lequel :

* Permet de paramétrer hello toouse du serveur management d’origine en tant qu’un seul serveur de configuration.
* Vous pouvez configurer un serveur de traitement supplémentaire.
* Vous configurez des ordinateurs virtuels protégés toouse hello supplémentaires de processus serveur.
* Chaque ordinateur source protégé est configuré avec trois disques de 100 Go chacun.

| **Serveur d’administration d’origine**<br/><br/>(serveur de configuration) | **Serveur de traitement supplémentaire** | **Taille du disque cache** | **Taux de modification des données** | **Machines protégées** |
| --- | --- | --- | --- | --- |
| 8 processeurs virtuels (2 sockets * 4 cœurs à 2,5 GHz), 16 Go de RAM |4 processeurs virtuels (2 sockets * 2 cœurs à 2,5 GHz), 8 Go de RAM |300 Go |250 Go ou moins |Vous pouvez répliquer 85 machines ou moins. |
| 8 processeurs virtuels (2 sockets * 4 cœurs à 2,5 GHz), 16 Go de RAM |8 processeurs virtuels (2 sockets * 4 cœurs à 2,5 GHz), 12 Go de RAM |600 Go |250 Go too1 to |Vous pouvez répliquer de 85 à 150 machines. |
| 12 processeurs virtuels (2 sockets * 6 cœurs à 2,5 GHz), 18 Go de RAM |12 processeurs virtuels (2 sockets * 6 cœurs à 2,5 GHz), 24 Go de RAM |1 To |1 to too2 to |Vous pouvez répliquer de 150 à 225 machines. |

Le mode de mise à l’échelle de vos serveurs dépend de votre préférence pour un modèle de montée en puissance ou de montée en charge. La montée en puissance consiste à déployer quelques serveurs de gestion et de processus haut de gamme, tandis que la montée en charge implique le déploiement d’un plus grand nombre de serveurs avec moins de ressources. Par exemple : Si vous avez besoin de machines de 220 tooprotect, vous pouvez procéder de hello suivantes :

* Configurer le serveur d’administration d’origine hello avec 12 processeurs virtuels et 18 Go de RAM. Configurer un serveur de traitement supplémentaire avec 12 processeurs virtuels et 24 Go de RAM. Configurer des ordinateurs protégés toouse uniquement hello supplémentaires de processus serveur.
* Configurer deux serveurs d’administration (2 x 8 processeurs virtuels, 16 Go de RAM) et deux serveurs de processus supplémentaire (1 x 8 processeurs virtuels et 4vCPUs x des ordinateurs (220) toohandle 135 + 85 1). Configurez les serveurs de processus supplémentaire machines protégées toouse uniquement hello.

Suivez les instructions de hello dans [déployer des serveurs de traitement supplémentaires](#deploy-additional-process-servers) tooset d’un serveur de processus supplémentaires.

## <a name="before-you-start-deployment"></a>Avant de lancer le déploiement
Hello tableaux suivants résument les conditions préalables de hello pour le déploiement de ce scénario.

### <a name="azure-prerequisites"></a>Conditions préalables pour Azure
| **Configuration requise** | **Détails** |
| --- | --- |
| **Compte Azure** |Vous avez besoin d’un compte [Microsoft Azure](https://azure.microsoft.com/) . Vous pouvez commencer par une version d’ [essai gratuit](https://azure.microsoft.com/pricing/free-trial/). Pour plus d’informations sur la tarification de Site Recovery, consultez la page [Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/). |
| **Stockage Azure** |Vous avez besoin d’un stockage Azure compte toostore répliquée de données. Les données répliquées sont stockées dans le stockage Azure et les machines virtuelles Azure sont lancées au moment du basculement. <br/><br/>Vous avez besoin d’un [compte de stockage géoredondant standard](../storage/storage-redundancy.md#geo-redundant-storage). Hello compte doit se trouver dans hello même région que hello service Site Recovery et être associé à hello même abonnement. Comptes de stockage toopremium de réplication n’est pas actuellement pris en charge et ne doivent pas être utilisées.<br/><br/>Nous ne prennent pas en charge Mobile comptes de stockage créés à l’aide de hello [portail Azure](../storage/storage-create-storage-account.md) plusieurs groupes de ressources. Pour plus d’informations, consultez [Introduction tooMicrosoft Azure Storage](../storage/storage-introduction.md).<br/><br/> |
| **Réseau Azure** |Vous avez besoin d’un réseau virtuel Azure qui se connectera machines virtuelles Azure toowhen basculement se produit. réseau virtuel Azure Hello doit être Bonjour même région que le coffre Site Recovery hello.<br/><br/>toofail après le basculement tooAzure, vous avez besoin d’un VPN de connexion (ou Azure ExpressRoute) configurer à partir du site de hello réseau Azure toohello local. |

### <a name="on-premises-prerequisites"></a>Conditions préalables locales
| **Configuration requise** | **Détails** |
| --- | --- |
| **Serveur d’administration** |Vous avez besoin d’un serveur Windows 2012 R2 local s’exécutant sur une machine virtuelle ou un serveur physique. Tous les composants de Site Recovery hello sur site sont installés sur ce serveur d’administration.<br/><br/> Nous vous recommandons de que déployer serveur hello comme un VM VMware hautement disponible. La restauration automatique toohello sur site local à partir de Azure est toujours VMs tooVMware indépendamment de si vous effectuez le basculement des machines virtuelles ou des serveurs physiques. Si vous ne configurez le serveur d’administration hello comme un VM VMware, vous devez tooset d’un serveur cible maître distinct comme un trafic de la restauration automatique tooreceive VMware VM.<br/><br/>serveur de Hello ne doit pas être un contrôleur de domaine.<br/><br/>serveur de Hello doit avoir une adresse IP statique.<br/><br/>nom d’hôte Hello du serveur de hello doit être de 15 caractères ou moins.<br/><br/>paramètres régionaux du système d’exploitation Hello doivent être en anglais uniquement.<br/><br/>serveur d’administration Hello requiert un accès Internet.<br/><br/>Vous devez accéder à partir du serveur de hello comme suit : un accès temporaire sur HTTP 80 pendant l’installation des composants de Site Recovery hello (toodownload MySQL) ; accès sortant en cours sur le port HTTPS 443 pour la gestion de la réplication ; accès sortant en cours sur HTTPS 9443 le trafic de réplication (ce port peut être modifié).<br/><br/> Assurez-vous que ces URL est accessibles à partir du serveur d’administration hello : <br/>- \*.hypervrecoverymanager.windowsazure.com<br/>- \*.accesscontrol.windows.net<br/>- \*.backup.windowsazure.com<br/>- \*.blob.core.windows.net<br/>- \*.store.core.windows.net<br/>- https://www.msftncsi.com/ncsi.txt<br/>- [https://dev.MySQL.com/Get/archives/MySQL-5.5/MySQL-5.5.37-Win32.msi] (https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi")<br/><br/>Si vous avez des règles de pare-feu basé sur l’adresse IP sur le serveur de hello, vérifiez que les règles de hello autorisent tooAzure de communication. Vous devez tooallow hello [plages d’adresses IP Azure Datacenter](https://www.microsoft.com/download/details.aspx?id=41653) et hello port HTTPS (443). Vous devez également les plages d’adresses IP toowhitelist hello région Azure de votre abonnement et ouest des États-Unis. URL de Hello [https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi] (https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi") est pour télécharger MySQL. |
| **Hôte VMware ESXi/vCenter** |Vous devez au moins un vSphere ESX/ESXi les hyperviseurs VMware gérer vos ordinateurs virtuels VMware, en cours d’exécution ESX/ESXi version 5.1, 5.5 ou 6.0 avec les dernières mises à jour de hello.<br/><br/> Nous vous recommandons de déployer un toomanage de serveur VMware vCenter vos hôtes ESXi. Il doit exécuter vCenter version 6.0 ou 5.5 avec les dernières mises à jour de hello.<br/><br/>Notez que Site Recovery ne prend pas en charge les nouvelles fonctionnalités de vCenter et vSphere 6.0, telles que Cross vCenter vMotion, les volumes virtuels et Storage DRS. Prise en charge de récupération de site est limitée toofeatures qui étaient également disponibles dans la version 5.5. |
| **Machines protégées** |**Microsoft Azure**<br/><br/>Ordinateurs que vous souhaitez que doivent respecter les tooprotect [conditions préalables Azure](site-recovery-prereq.md) pour la création de machines virtuelles Azure.<br><br/>Si vous souhaitez tooconnect toohello machines virtuelles Azure après le basculement, vous devez tooenable les connexions Bureau à distance sur les pare-feu local hello.<br/><br/>Sur les machines protégées, la capacité d’un disque ne doit pas dépasser 1023 Go. Une machine virtuelle peut avoir des disques too64 (et donc des too64 to). Si la taille de vos disques est supérieure à 1 To, vous pouvez utiliser la réplication de base de données offerte par des fonctionnalités telles que SQL Server AlwaysOn ou Oracle Data Guard.<br/><br/>2 Go minimum d’espace disponible sur le lecteur d’installation hello pour l’installation du composant.<br/><br/>Les clusters invités dont le disque est partagé ne sont pas pris en charge. Si vous disposez d’un déploiement en cluster, vous pouvez utiliser la réplication de base de données offerte par des fonctionnalités telles que SQL Server AlwaysOn ou Oracle Data Guard.<br/><br/>L’amorçage UEFI (Unified Extensible Firmware Interface) / EFI (Extensible Firmware Interface) n’est pas pris en charge.<br/><br/>Le nom des machines doit contenir entre 1 et 63 caractères (lettres, chiffres et tirets). Hello doit commencer par une lettre ou un chiffre et se terminer par une lettre ou un chiffre. Une fois qu’un ordinateur est protégé, vous pouvez modifier hello nom Azure.<br/><br/>**Machines virtuelles VMware**<br/><br>Vous devez tooinstall VMware vSphere PowerCLI 6.0. sur le serveur d’administration hello (serveur de configuration).<br/><br/>Ordinateurs virtuels VMware souhaité tooprotect doit avoir les outils VMware installé et en cours d’exécution.<br/><br/>Si l’ordinateur virtuel source de hello a association de cartes réseau, il est converti tooa une seule carte réseau après le basculement tooAzure.<br/><br/>Si les ordinateurs virtuels protégés ont un disque iSCSI, Site Recovery convertit hello protégé disque iSCSI de machine virtuelle dans un fichier de disque dur virtuel lorsque hello machine virtuelle bascule tooAzure. Si la cible iSCSI peut être atteint par hello machine virtuelle Azure, il se connecter tooiSCSI cible et consultez essentiellement de deux disques : disque VHD hello hello machine virtuelle Azure et hello source le disque iSCSI. Dans ce cas, vous devez toodisconnect cible iSCSI hello qui apparaît sur hello basculé machine virtuelle Azure.<br/><br/>Pour plus d’informations sur les autorisations des utilisateurs VMware hello doit que Site de récupération, consultez [VMware des autorisations pour l’accès de vCenter](#vmware-permissions-for-vcenter-access).<br/><br/> **Ordinateurs Windows Server (sur des machines virtuelles VMware ou un serveur physique)**<br/><br/>serveur de Hello doit exécuter un système d’exploitation de 64 bits pris en charge : Windows Server 2012 R2, Windows Server 2012 ou Windows Server 2008 R2 avec au moins SP1.<br/><br/>système d’exploitation de Hello doit être installé sur le lecteur C, et disque de système d’exploitation hello doit être un disque de base Windows. (hello du système d’exploitation ne doit pas être installé sur un disque dynamique de Windows).<br/><br/>Pour les ordinateurs Windows Server 2008 R2, vous devez toohave .NET Framework 3.5.1 installé.<br/><br/>Vous avez besoin d’un compte d’administrateur de tooprovide (doit être d’un administrateur local sur l’ordinateur de Windows hello) pour Bonjour Bonjour d’installation poussée du Service mobilité sur les serveurs Windows. Si hello fourni de compte est un compte de domaine, vous devez toodisable contrôle des accès utilisateur à distance sur l’ordinateur local de hello. Pour plus d’informations, consultez [installer le service de mobilité hello en mode installation push](#install-the-mobility-service-with-push-installation).<br/><br/>Site Recovery prend en charge les machines virtuelles équipées d’un disque RDM. Lors du retour arrière, Site Recovery réutilise le disque RDM hello si la source d’origine de hello machine virtuelle et le disque RDM sont disponibles. Si ce n’est pas le cas, Site Recovery crée un fichier VMDK pour chaque disque.<br/><br/>**Ordinateurs Linux**<br/><br/>Vous avez besoin d’un système d’exploitation de 64 bits pris en charge : Red Hat Enterprise Linux 6.7 ; CentOS 6.5, 6.6 ou 6.7 ; Oracle Enterprise Linux version 6.4 ou 6.5 exécutant noyau compatible de Red Hat hello ou insécable Enterprise noyau version 3 (UEK3) ; SUSE Linux Enterprise Server 11 SP3.<br/><br/>les fichiers / etc/hosts sur les ordinateurs protégés doivent contenir des entrées qui mappent des adresses de tooIP du nom d’hôte local hello associés à toutes les cartes réseau. <br/><br/>Si vous souhaitez tooconnect tooan machine virtuelle Azure exécutant Linux après le basculement à l’aide d’un Secure Shell client (ssh), vérifiez que service de Secure Shell hello sur l’ordinateur de hello protégé est toostart automatiquement au démarrage du système, et que les règles de pare-feu autorisent un ssh tooit de connexion.<br/><br/>Protection ne peut être activée que pour les ordinateurs Linux avec hello après stockage : fichiers système (EXT3, ETX4, ReiserFS, XFS) ; Périphérique logiciel MPIO Mappeur (MPIO) ; Gestionnaire de volume (LVM2). Les serveurs physiques avec stockage de contrôleur HP CCISS ne sont pas pris en charge. système de fichiers ReiserFS Hello est pris en charge uniquement sur SUSE Linux Enterprise Server 11 SP3.<br/><br/>Site Recovery prend en charge les machines virtuelles équipées d’un disque RDM. Lors de la restauration automatique de Linux, Site Recovery ne réutiliser le disque RDM hello. Il crée à la place un fichier VMDK pour chaque disque RDM correspondant. |

Uniquement pour un VM Linux : vous assurer que les paramètre de disk.enableUUID=true hello Bonjour Hello VM dans VMware, les paramètres de configuration. Si cette ligne n’existe pas, ajoutez-la. Il s’agit de tooprovide requis un toohello UUID cohérent VMDK afin qu’il monte correctement. Sans ce paramètre, la restauration automatique entraîne un téléchargement complet même si hello machine virtuelle est disponible localement. L’ajout de ce paramètre garantit que seules les modifications d’ordre différentiel sont retransférées pendant la restauration automatique.

## <a name="step-1-create-a-vault"></a>Étape 1 : Créer un coffre
1. Connectez-vous à toohello [portail Azure](https://manage.windowsazure.com/).
2. Développez **Data Services** > **Recovery Services**, puis cliquez sur **Coffre Site Recovery**.
3. Cliquez sur **Créer nouveau** > **Création rapide**.
4. Dans **nom**, entrez un coffre de hello tooidentify nom convivial.
5. Dans **région**, sélectionnez hello région géographique pour le coffre hello. les régions toocheck pris en charge, consultez [détails de la tarification Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Cliquez sur **Create vault**.
    ![Création d’un coffre](./media/site-recovery-vmware-to-azure-classic/quick-start-create-vault.png)

Vérifiez tooconfirm de barre d’état hello qui hello coffre a été créé avec succès. Hello est répertorié en tant que **Active** sur hello principal **Services de récupération** page.

## <a name="step-2-set-up-an-azure-network"></a>Étape 2 : Configurer un réseau Azure
Configurer un réseau Azure afin que les machines virtuelles Azure sera connecté tooa réseau après le basculement, et afin que la restauration automatique toohello local site peut fonctionner comme prévu.

1. Bonjour portail Azure, sélectionnez **créer un réseau virtuel** et spécifiez le nom de réseau hello, plage d’adresses IP et nom du sous-réseau.
2. Si vous avez besoin de la restauration automatique toodo, ajouter des VPN/ExpressRoute toohello réseau. Toohello réseau peuvent être ajouté à VPN/ExpressRoute, même après le basculement.

Pour plus d’informations sur les réseaux virtuels, consultez la [vue d’ensemble des réseaux virtuels](../virtual-network/virtual-networks-overview.md).

> [!NOTE]
> [Migration des réseaux](../azure-resource-manager/resource-group-move-resources.md) entre les ressources groupes dans hello même abonnement ou entre abonnements n’est pas prise en charge pour les réseaux utilisés pour le déploiement de Site Recovery.
>
>

## <a name="step-3-install-hello-vmware-components"></a>Étape 3 : Installer les composants VMware hello
Si vous souhaitez que les ordinateurs virtuels VMware tooreplicate, procédez comme suit sur le serveur d’administration hello :

1. [Téléchargez](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1) et installez VMware vSphere PowerCLI 6.0.
2. Redémarrez le serveur de hello.

## <a name="step-4-download-a-vault-registration-key"></a>Étape 4 : Générer une clé d’inscription du coffre
1. À partir du serveur d’administration hello, ouvrez la console de récupération de Site hello dans Azure. Sur hello **Services de récupération** , cliquez sur hello de hello coffre tooopen **Quick Start** page. Vous pouvez également ouvrir hello **Quick Start** page à tout moment en cliquant sur hello icône.

    ![Icône Démarrage rapide](./media/site-recovery-vmware-to-azure-classic/quick-start-icon.png)
2. Sur hello **Quick Start** , cliquez sur **préparer les ressources cibles** > **télécharger une clé d’inscription**. un fichier d’inscription Hello est généré automatiquement. Il est valide pendant cinq jours après sa création.

## <a name="step-5-install-hello-management-server"></a>Étape 5 : Installer le serveur d’administration hello
> [!TIP]
> Assurez-vous que ces URL est accessibles à partir du serveur d’administration hello :
>
> * *.hypervrecoverymanager.windowsazure.com
> * *.accesscontrol.windows.net
> * *.backup.windowsazure.com
> * *.blob.core.windows.net
> * *.store.core.windows.net
> * https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi
> * https://www.msftncsi.com/ncsi.txt
>
>



>[!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Setup-Registration/player]



1. Sur hello **Quick Start** page, téléchargez hello installation unifiée fichier toohello server.
2. Exécutez le programme d’installation toostart de fichier d’installation Bonjour Bonjour **le programme d’installation de Site Recovery unifiée** Assistant.
3. Dans **avant de commencer**, sélectionnez **installer le serveur de configuration hello et serveur de processus**.

   ![Avant de commencer](./media/site-recovery-vmware-to-azure-classic/combined-wiz1.png)
4. Dans **licence de logiciel tiers**, cliquez sur **J’accepte** toodownload et installer MySQL.

    ![Logiciels tiers](./media/site-recovery-vmware-to-azure-classic/combined-wiz105.PNG)
5. Dans **inscription**, recherchez et sélectionnez la clé d’inscription hello que vous avez téléchargé à partir du coffre de hello.

    ![Inscription](./media/site-recovery-vmware-to-azure-classic/combined-wiz3.png)
6. Dans **paramètres Internet**, spécifiez comment le fournisseur hello en cours d’exécution sur le serveur de configuration hello vont se connecter tooAzure Site Recovery sur hello Internet.

   * Si vous souhaitez tooconnect avec proxy hello est actuellement configuré sur l’ordinateur de hello, sélectionnez **se connecter avec des paramètres proxy existants**.
   * Si vous souhaitez hello fournisseur tooconnect directement, sélectionnez **se connecter directement sans proxy**.
   * Si le proxy existant de hello requiert une authentification, ou si vous souhaitez toouse un proxy personnalisé pour la connexion du fournisseur hello, sélectionnez **se connecter avec les paramètres de proxy personnalisés**.
     * Si vous utilisez un proxy personnalisé, vous aurez besoin des informations d’identification, le port et adresse de hello toospecify.
     * Si vous utilisez un proxy, il convient que vous avez déjà autorisé hello URL suivantes :
       * *.hypervrecoverymanager.windowsazure.com    
       * *.accesscontrol.windows.net
       * *.backup.windowsazure.com
       * *.blob.core.windows.net
       * *.store.core.windows.net

    ![Pare-feu](./media/site-recovery-vmware-to-azure-classic/combined-wiz4.png)

1. Dans **vérification**, le programme d’installation exécute une vérification toomake assurer que l’installation de hello peut exécuter.

    ![Composants requis](./media/site-recovery-vmware-to-azure-classic/combined-wiz5.png)

     Si un avertissement s’affiche sur hello **vérification de la synchronisation temporelle globale**, vérifiez cette heure hello sur l’horloge système hello (**Date et heure** paramètres) est identique à hello en tant que le fuseau horaire de hello.

     ![Problème de synchronisation de l’heure](./media/site-recovery-vmware-to-azure-classic/time-sync-issue.png)

1. Dans **MySQL Configuration**, créer des informations d’identification pour la signature dans l’instance de serveur MySQL toohello qui est installée.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz6.png)
2. Dans **détails de l’environnement**, indiquez si vous souhaitez tooreplicate les ordinateurs virtuels VMware. Si c’est le cas, le programme d’installation vérifie que PowerCLI 6.0 est installé.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz7.png)
3. Dans **l’emplacement d’installation**, sélectionnez où vous souhaitez que les fichiers binaires de tooinstall hello et stockez le cache de hello. Vous pouvez sélectionner un lecteur qui dispose d’au moins 5 Go d’espace disque disponible. Toutefois, nous vous recommandons d’utiliser un lecteur de cache présentant au moins 600 Go d’espace disque disponible.

   ![Emplacement d’installation](./media/site-recovery-vmware-to-azure-classic/combined-wiz8.png)
4. Dans **sélection du réseau**, spécifiez l’écouteur hello (carte réseau et port SSL) sur le hello serveur de configuration envoient et reçoivent des données de réplication. Vous pouvez modifier la valeur par défaut hello port (9443). Dans le port toothis d’ajout, le port 443 utilisera un serveur web qui orchestre les opérations de réplication. N’utilisez pas le port 443 pour la réception du trafic de réplication.

    ![Sélection du réseau](./media/site-recovery-vmware-to-azure-classic/combined-wiz9.png)



1. Dans **Résumé**, passez en revue les informations hello et cliquez sur **installer**. Une fois l’installation terminée, une phrase secrète est générée. Vous en aurez besoin pour l’activation de la réplication. Par conséquent, copiez-la et conservez-la en lieu sûr.

   ![Résumé](./media/site-recovery-vmware-to-azure-classic/combined-wiz10.png)


> [!WARNING]
> Hello proxy de Microsoft Azure Recovery services Agent doit être configuré.
> Une fois l’installation de hello terminée, démarrez hello Microsoft Azure Recovery Services Shell à partir du menu de démarrage de Windows hello. Dans la fenêtre de commande hello qui s’ouvre, exécutez hello ensemble suivant de tooset de commandes des paramètres du serveur proxy hello.
>
>
    $pwd = ConvertTo-SecureString -String ProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumb – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
>


### <a name="run-setup-from-hello-command-line"></a>Exécutez le programme d’installation à partir de la ligne de commande hello
Vous pouvez également exécuter des Assistant unifiée de hello à partir de la ligne de commande hello, comme suit :

    UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]

Où :

* /ServerMode : Obligatoire. Spécifie si l’installation de hello doit installer hello configuration et des processus de serveurs ou hello processus uniquement (serveurs de processus supplémentaire tooinstall utilisé). Valeurs d’entrée : CS, PS.
* InstallDrive : Obligatoire. Spécifie le dossier hello dans lequel sont installés les composants de hello.
* /MySQLCredFilePath. Obligatoire. Spécifie le fichier de tooa de chemin d’accès de hello où sont stockées les informations d’identification de hello MySQL server. Obtenir le fichier de hello modèle toocreate hello.
* /VaultCredFilePath. Obligatoire. Emplacement du fichier d’informations d’identification de coffre hello.
* / EnvType. Obligatoire. Type d’installation. Valeurs : VMware, NonVMware.
* / PSIP et /CSIP. Obligatoire. Adresse IP du serveur de processus hello et serveur de configuration.
* /PassphraseFilePath. Obligatoire. Emplacement du fichier de mot de passe hello.
* /ByPassProxy. facultatif. Spécifie le serveur d’administration hello qui se connecte tooAzure sans proxy.
* /ProxySettingsFilePath. facultatif. Spécifie les paramètres pour un proxy personnalisé (proxy par défaut sur le serveur hello qui nécessite une authentification), ou proxy personnalisé.

## <a name="step-6-set-up-credentials-for-hello-vcenter-server"></a>Étape 6 : Configurer des informations d’identification pour le serveur vCenter hello
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Discovery/player]
>
>

serveur de processus Hello peut détecter automatiquement les ordinateurs virtuels VMware qui sont gérés par un serveur vCenter. Pour la détection automatique, récupération de Site a besoin d’un compte et les informations d’identification qui peuvent accéder au serveur vCenter de hello. Ce n’est pas le cas si vous répliquez uniquement des serveurs physiques.

compte de hello tooset et les informations d’identification :

1. Sur le serveur vCenter hello, créez un rôle (**Azure_Site_Recovery**) au niveau de vCenter hello avec hello [autorisations requises](#vmware-permissions-for-vcenter-access).
2. Affecter hello **Azure_Site_Recovery** utilisateur de rôle tooa vCenter.

   > [!NOTE]
   > Un compte d’utilisateur vCenter ayant le rôle en lecture seule de hello peut exécuter le basculement sans arrêter les ordinateurs de la source protégée. Si vous souhaitez tooshut vers le bas de ces ordinateurs, vous devez hello Azure_Site_Recovery rôle. Si vous migrez uniquement des machines virtuelles à partir de VMware tooAzure et que vous n’avez pas besoin de toofail précédent, rôle en lecture seule de hello est suffisante.
   >
   >
3. compte de tooadd hello, ouvrez **cspsconfigtool**. Il est disponible comme un raccourci sur le bureau de hello et situé dans le dossier de \home\svsystems\bin hello [emplacement d’installation].
4. Sur hello **gérer les comptes** , cliquez sur **ajouter un compte**.

    ![Ajouter un compte](./media/site-recovery-vmware-to-azure-classic/credentials1.png)
5. Dans **détails du compte**, ajouter des informations d’identification qui peuvent être utilisés tooaccess hello serveur vCenter. Il peut prendre plus de 15 minutes pour tooappear de nom de compte hello dans le portail de hello. tooupdate immédiatement, cliquez sur **Actualiser** sur hello **serveurs de Configuration** onglet.

    ![Détails](./media/site-recovery-vmware-to-azure-classic/credentials2.png)

## <a name="step-7-add-vcenter-servers-and-esxi-hosts"></a>Étape 7 : Ajouter des serveurs vCenter ou des hôtes ESXi
Si vous répliquez des ordinateurs virtuels VMware, vous devez tooadd un serveur vCenter (ou hôte ESXi).

1. Sur hello **serveurs** > **serveurs de Configuration** onglet, sélectionnez **ajouter un serveur vCenter**.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter1.png)
2. Ajoutez le serveur vCenter hello ou les détails de l’hôte ESXi, nom hello du compte hello que vous avez spécifié tooaccess hello serveur vCenter à l’étape précédente de hello et serveur de processus hello qui sera utilisé toodiscover les ordinateurs virtuels VMware qui sont gérés par le serveur vCenter hello. le serveur vCenter Hello ou hôte ESXi doit se trouver dans hello même réseau en tant que serveur hello quels hello processus serveur est installé.

   > [!NOTE]
   > Si vous ajoutez le serveur vCenter hello ou hôte ESXi avec un compte qui ne dispose pas des privilèges d’administrateur sur hello vCenter ou serveur hôte, vérifiez que hello vCenter ou ESXi comptes posséder les privilèges activés : centre de données, magasin de données, dossier, Jost, réseau, Ressources, ordinateur virtuel et vSphere Distributed Switch. le serveur vCenter Hello a besoin d’affichages de stockage de hello privilège activé.
   >
   >

    ![Ajouter un serveur vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter2.png)
3. Une fois la détection terminée, le serveur vCenter hello s’afficheront sur hello **serveurs de Configuration** onglet.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter3.png)

## <a name="step-8-create-a-protection-group"></a>Étape 8 : Créer un groupe de protection
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Protection/player]
>
>

Groupes de protection sont des groupements logiques d’ordinateurs virtuels ou de serveurs physiques que vous souhaitez tooprotect à l’aide de bienvenue des mêmes paramètres de protection. Vous appliquez le groupe de protection de tooa de paramètres de protection, et ces paramètres sont appliqués tooall ordinateurs (virtuels ou physiques) que vous ajoutez toohello groupe.

1. Accédez trop**éléments protégés** > **groupe de Protection** sur l’icône de hello tooadd un groupe de protection.

    ![Créer un groupe de protection](./media/site-recovery-vmware-to-azure-classic/protection-groups1.png)
2. Sur hello **spécifier les paramètres de groupe de Protection** , spécifiez un nom pour le groupe de hello. Bonjour **de** liste déroulante, le serveur de configuration sélectionnez hello sur lequel vous souhaitez que toocreate hello groupe. La **cible**  est Microsoft Azure.

    ![Paramètres du groupe de protection](./media/site-recovery-vmware-to-azure-classic/protection-groups2.png)
3. Sur hello **spécifier les paramètres de réplication** page, configurez les paramètres de réplication hello qui seront utilisés pour toutes les machines hello dans le groupe de hello.

    ![Réplication du groupe de protection](./media/site-recovery-vmware-to-azure-classic/protection-groups3.png)

   * **Cohérence de multiples VM**: Si vous activez ce, il crée des points de récupération cohérents avec les applications partagées sur plusieurs ordinateurs hello dans le groupe de protection hello. Ce paramètre est particulièrement importante lorsque tous les ordinateurs dans le groupe de protection hello exécutent hello la même charge de travail. Tous les ordinateurs seront récupérée toohello même point de données. Il est disponible que vous répliquiez des machines virtuelles VMware ou des serveurs physiques (Windows ou Linux).
   * **Seuil RPO**: jeux hello RPO. Alertes sont générées lors de la réplication de protection continue des données hello dépasse la valeur de seuil RPO hello configuré.
   * **Rétention du point de récupération**: Spécifie la période de conservation hello. Les ordinateurs protégés peuvent être récupérées point tooany dans cette fenêtre.
   * **Fréquence des instantanés cohérents au niveau des applications** : spécifie la fréquence de création des points de récupération contenant des instantanés cohérents au niveau des applications.

Lorsque vous sélectionnez la case à cocher hello, un groupe de protection est créé avec le nom hello spécifié. En outre, un deuxième groupe de protection est créé avec le nom de hello *nom du groupe de protection*- la restauration automatique. Ce groupe de protection est utilisé si vous ne le site local de toohello précédent après basculement tooAzure. Vous pouvez surveiller les groupes de protection hello comme elles sont créées sur hello **éléments protégés** page.

## <a name="step-9-install-hello-mobility-service"></a>Étape 9 : Installer le service de mobilité hello
Hello première étape de la protection des ordinateurs virtuels et des serveurs physiques est un service de mobilité tooinstall hello. Il existe deux méthodes pour le faire :

* Push et d’installer automatiquement le service de hello sur chaque ordinateur hello du serveur de processus. Lorsque vous ajoutez le groupe de protection de machines tooa et ils exécutez déjà une version appropriée du service mobilité de hello, poussée ne se produise. Vous pouvez également automatiquement installer le service de hello à l’aide de votre méthode de push enterprise, comme WSUS ou System Center Configuration Manager. Assurez-vous que vous avez configuré serveur d’administration hello avant de le faire.
* Installer le service de hello manuellement sur chaque ordinateur que vous souhaitez tooprotect. Assurez-vous que vous avez configuré serveur d’administration hello avant de le faire.

### <a name="install-hello-mobility-service-with-push-installation"></a>Installer le service de mobilité hello en mode installation push
Lorsque vous ajoutez le groupe de protection de machines tooa, hello service mobilité est automatiquement envoyée et installé sur chaque ordinateur par le serveur de processus hello.

#### <a name="prepare-for-automatic-push-on-windows-machines"></a>Préparez une opération Push automatique sur les machines Windows
tooprepare afin que hello service mobilité des ordinateurs Windows peuvent être installés automatiquement par le serveur de processus hello :

1. Créez un compte de que ce serveur de processus hello utilisez tooaccess hello machine. compte de Hello doit disposer des privilèges d’administrateur (local ou domaine). Ces informations d’identification sont utilisées uniquement pour l’installation push du service mobilité de hello.

   > [!NOTE]
   > Si vous n’utilisez pas un compte de domaine, vous devez toodisable contrôle des accès utilisateur à distance sur l’ordinateur local de hello. toodo, dans le Registre hello sous HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System, ajouter l’hello entrée DWORD LocalAccountTokenFilterPolicy avec une valeur de 1 sous. entrée de Registre tooadd hello à partir d’une interface de ligne commande Ouvrir ou à l’aide de PowerShell, entrez  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** .
   >
   >
2. Pour le pare-feu Windows sur l’ordinateur hello que vous souhaitez tooprotect, sélectionnez **autoriser une application ou une fonctionnalité via le pare-feu**et activer **partage de fichiers et imprimantes** et **gestion de Windows Instrumentation**. Pour les ordinateurs qui appartiennent tooa domaine, vous pouvez configurer la stratégie de pare-feu hello avec un objet de stratégie de groupe.

   ![Paramètres du pare-feu](./media/site-recovery-vmware-to-azure-classic/mobility1.png)
3. Ajoutez le compte hello que vous avez créé :

   * Ouvrez **cspsconfigtool**. Il est disponible comme un raccourci sur le bureau de hello et situé dans le dossier de \home\svsystems\bin hello [emplacement d’installation].
   * Sur hello **gérer les comptes** , cliquez sur **ajouter un compte**.
   * Ajoutez le compte hello que vous avez créé. Après avoir ajouté le compte de hello, vous aurez besoin des informations d’identification de tooprovide hello lorsque vous ajoutez un groupe de protection de machine tooa.

#### <a name="prepare-for-automatic-push-on-linux-servers"></a>Préparez une opération Push automatique sur les serveurs Linux
1. Assurez-vous que cet ordinateur de Linux hello souhaité tooprotect est pris en charge comme décrit dans [conditions préalables local](#on-premises-prerequisites). Vérifiez qu’il existe une connectivité réseau entre l’ordinateur de hello souhaité tooprotect et hello serveur d’administration qui exécute le serveur de processus hello.
2. Créez un compte de que ce serveur de processus hello utilisez tooaccess hello machine. compte de Hello doit être un utilisateur racine sur le serveur de Linux hello source. Ces informations d’identification sont utilisées uniquement pour l’installation push du service mobilité de hello.

   * Ouvrez **cspsconfigtool**. Il est disponible comme un raccourci sur le bureau de hello et situé dans le dossier de \home\svsystems\bin hello [emplacement d’installation].
   * Sur hello **gérer les comptes** , cliquez sur **ajouter un compte**.
   * Ajoutez le compte hello que vous avez créé. Après avoir ajouté le compte de hello, vous aurez besoin des informations d’identification de tooprovide hello lorsque vous ajoutez un groupe de protection de machine tooa.
3. Vérifiez le fichier/etc/hosts hello sur la source de hello Linux server contient des entrées qui mappent des adresses de tooIP hello nom d’hôte local associés à toutes les cartes réseau.
4. Installer hello dernière openssh openssh-serveur openssl les packages et sur l’ordinateur hello que vous souhaitez tooprotect.
5. Vérifiez que le protocole SSH est activé et exécuté sur le port 22.
6. Activer l’authentification dans le fichier de sshd_config hello SFTP sous-système et le mot de passe comme suit :

   * Connectez-vous en tant qu’utilisateur racine.
   * Dans le fichier de /etc/ssh/sshd_config hello, rechercher la ligne hello qui commence par PasswordAuthentication.
   * Supprimez les commentaires de la ligne de hello et remplacez valeur hello **aucun** trop**Oui**.
   * Ligne hello rechercher qui commence par **sous-système** et supprimez les commentaires de la ligne de hello.

     ![Remplacement de l’absence de sous-système par défaut dans Linux](./media/site-recovery-vmware-to-azure-classic/mobility2.png)

### <a name="install-hello-mobility-service-manually"></a>Installer manuellement le service de mobilité de hello
programmes d’installation Hello sont disponibles dans C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository.

| Système d’exploitation source | Fichier d’installation du service Mobilité |
| --- | --- |
| Windows Server (64 bits uniquement) |Microsoft-ASR_UA_9.*.0.0_Windows_* release.exe |
| CentOS 6.4, 6.5, 6.6 (64 bits uniquement) |Microsoft-ASR_UA_9.*.0.0_RHEL6-64_*release.tar.gz |
| SUSE Linux Enterprise Server 11 SP3 (64 bits uniquement) |Microsoft-ASR_UA_9.*.0.0_SLES11-SP3-64_*release.tar.gz |
| Oracle Enterprise Linux 6.4, 6.5 (64 bits uniquement) |Microsoft-ASR_UA_9.*.0.0_OL6-64_*release.tar.gz |

#### <a name="install-hello-mobility-service-manually-on-a-windows-server"></a>Installer manuellement le service de mobilité de hello sur un serveur Windows
1. Téléchargez et exécutez le programme d’installation approprié de hello.
2. Dans **Avant de commencer**, sélectionnez **Service Mobilité**.

    ![Installation du service Mobilité](./media/site-recovery-vmware-to-azure-classic/mobility3.png)
3. Dans **détails du serveur Configuration**hello phrase secrète qui a été générée lors de l’installation des composants de serveur de gestion hello et spécifiez l’adresse IP de hello hello du serveur d’administration. Vous pouvez récupérer la phrase secrète de hello en exécutant  **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** sur le serveur d’administration hello.

    ![Service Mobilité](./media/site-recovery-vmware-to-azure-classic/mobility6.png)
4. Dans **l’emplacement d’installation**, conserver l’emplacement par défaut de hello et cliquez sur **suivant** toobegin installation.
5. Dans **progression de l’Installation**, vérifiez l’installation et redémarrer l’ordinateur de hello si vous y êtes invité.

Vous pouvez également installer en entrant hello suivant la ligne de commande de texte hello :

    UnifiedAgent.exe [/Role <Agent/MasterTarget>] [/InstallLocation <Installation Directory>] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>] [/LogFilePath <Log File Path>]

Bonjour précédant la commande :

* /Role : Obligatoire Spécifie si le service mobilité de hello doit être installé.
* /InstallLocation : Obligatoire. Spécifie où tooinstall hello service.
* / PassphraseFilePath : Obligatoire. Spécifie le mot de passe serveur hello configuration.
* /LogFilePath : Obligatoire. Spécifie l’emplacement du fichier hello journal d’installation.

#### <a name="uninstall-hello-mobility-service-manually"></a>Désinstaller le service de mobilité hello manuellement
Vous pouvez désinstaller le service de mobilité hello à l’aide de **désinstaller ou modifier un programme** dans le panneau de configuration ou en utilisant la ligne de commande hello.

Hello commande toouninstall service mobilité à l’aide de ligne de commande hello est la suivante :

    MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1}

#### <a name="change-hello-ip-address-of-hello-management-server"></a>Modifier l’adresse IP de hello hello du serveur d’administration
Une fois que vous exécutez hello Assistant, vous pouvez modifier les adresse IP de hello hello du serveur d’administration comme suit :

1. Ouvrez hello fichier hostconfig.exe (situé sur le bureau de hello).
2. Sur hello **Global** , modifiez l’adresse IP de hello hello du serveur d’administration.

   > [!NOTE]
   > Modifier uniquement les adresses IP hello hello du serveur d’administration. numéro de port Hello pour les communications de serveur d’administration doit être 443, et **utiliser HTTPS** gauche doit être activé. Ne modifiez pas le mot de passe hello.
   >
   >

    ![Adresse IP du serveur d’administration](./media/site-recovery-vmware-to-azure-classic/host-config.png)

#### <a name="install-hello-mobility-service-manually-on-a-linux-server"></a>Installer manuellement le service de mobilité de hello sur un serveur Linux
1. Copier la machine hello tar approprié archiver toohello Linux que vous souhaitez tooprotect. Consultez la table hello sous [installer manuellement le service de mobilité de hello](#install-the-mobility-service-manually) toodetermine archiver le tar doit utiliser.
2. Ouvrir un programme de l’interpréteur de commandes et extrayez hello archive tar archive tooa chemin d’accès local en exécutant :`tar -xvzf Microsoft-ASR_UA_8.5.0.0*`
3. Créez un fichier nommé passphrase.txt dans toowhich de répertoire local hello vous avez extrait le contenu hello d’archive tar de hello. toodo, copie hello phrase secrète à partir de C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase sur le serveur d’administration hello et enregistrez-le dans passphrase.txt en exécutant  *`echo <passphrase> >passphrase.txt`*  dans le shell hello.
4. Installer le service de mobilité hello en hello de commande suivante :*`sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i <IP address> -p <port> -s y -c https -P passphrase.txt`*
5. Spécifier l’adresse IP interne de hello hello du serveur d’administration et assurez-vous que le port 443 est sélectionné.

#### <a name="install-hello-mobility-service-from-hello-command-line"></a>Installer le service de mobilité hello à partir de la ligne de commande hello

Copier les hello le mot de passe à partir de \InMage Systems\private\connection C:\Program Files (x86) sur le serveur d’administration hello et l’enregistrer en tant que « passphrase.txt » sur le serveur d’administration hello. Puis exécutez hello suivant les commandes. Dans notre exemple, adresse IP hello du serveur de gestion est 104.40.75.37 et hello port HTTPS est 443 :

tooinstall sur un serveur de production :

    ./install -t both -a host -R Agent -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt

tooinstall sur le serveur cible maître de hello :

    ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt


## <a name="step-10-enable-protection-for-a-machine"></a>Étape 10 : activation de la protection d’une machine
protection de tooenable, ajoutez le groupe de protection tooa serveurs physiques et virtuels. Avant de commencer, notez les suivant hello si vous protégez des ordinateurs virtuels VMware :

* Les ordinateurs virtuels VMware sont découverts toutes les 15 minutes, et il peut prendre plus de 15 minutes pour les tooappear dans le portail Site Recovery hello après la découverte.
* Modifications de l’environnement sur l’ordinateur virtuel de hello (par exemple, l’installation des outils VMware) peuvent également prendre plus de toobe 15 minutes mis à jour en mode de récupération de Site.
* Vous pouvez vérifier hello découverts dernière heure pour les ordinateurs virtuels VMware Bonjour **dernier Contact à** field pour un hôte de serveur/ESXi vCenter hello sur hello **serveurs de Configuration** onglet.
* Si vous ajoutez un serveur vCenter ou l’hôte ESXi après la création d’un groupe de protection, il peut prendre plus de 15 minutes pour toorefresh de portail Azure Site Recovery hello et toobe d’ordinateurs virtuels répertoriés dans hello **groupe de protection ajouter machines tooa**boîte de dialogue.
* Si vous souhaitez tooproceed immédiatement et que vous ajoutez le groupe de protection de machines tooa sans attendre la détection planifiée de hello, mettez en surbrillance le serveur de configuration hello (ne cliquez pas dessus) et cliquez sur **Actualiser**.

Par ailleurs :

* Nous vous recommandons de structurer vos groupes de protection afin qu’ils reflètent vos charges de travail. Par exemple, ajouter des ordinateurs qui exécutent une application spécifique de toohello même groupe.
* Lorsque vous ajoutez le groupe de protection de machines tooa, serveur de processus hello transmet automatiquement et installe le service de mobilité hello s’il n’est pas déjà installé. Vous devez le mécanisme de diffusion toohave hello préparé comme indiqué dans l’étape précédente de hello.

### <a name="add-machines-tooa-protection-group"></a>Ajouter le groupe de protection de machines tooa

1. Accédez trop**éléments protégés** > **groupe de Protection** > **Machines** > **ajouter des ordinateurs** .
2. Si vous protégez des machines virtuelles VMware dans **sélectionner des Machines virtuelles**, sélectionnez un serveur vCenter qui gère vos machines virtuelles (ou l’hôte de EXSi hello sur lequel ils s’exécutent), puis sélectionnez les ordinateurs hello.

    ![activation de la protection pour les machines virtuelles](./media/site-recovery-vmware-to-azure-classic/enable-protection2.png)
3. Si vous protégez des serveurs physiques, dans **sélectionner des Machines virtuelles**, ouvrez hello **ajouter des Machines physiques** Assistant et fournir l’adresse IP de hello et nom convivial. Sélectionnez ensuite la famille du système d’exploitation hello.

   ![Activer la protection de serveurs physiques](./media/site-recovery-vmware-to-azure-classic/enable-protection1.png)
4. Dans **spécifier les ressources cible**, sélectionnez le compte de stockage hello que vous utilisez pour la réplication et indiquez si les paramètres de hello doivent être utilisés pour toutes les charges de travail. Les comptes de stockage Premium ne sont pas pris en charge pour le moment.

   > [!NOTE]
   > Nous ne prennent pas en charge Mobile comptes de stockage créés à l’aide de hello [portail Azure](../storage/storage-create-storage-account.md) plusieurs groupes de ressources.                           
   > [Migration de comptes de stockage](../azure-resource-manager/resource-group-move-resources.md) entre les ressources groupes dans hello même abonnement ou entre abonnements n’est pas prise en charge pour les comptes de stockage utilisés pour le déploiement de Site Recovery.
   >
   >

    ![Configurer les paramètres cibles](./media/site-recovery-vmware-to-azure-classic/enable-protection3.png)
5. Dans **spécifier les comptes**, sélectionnez hello compte que vous avez [configurer](#install-the-mobility-service-with-push-installation) toouse pour l’installation automatique du service mobilité de hello.

    ![Spécifier les comptes](./media/site-recovery-vmware-to-azure-classic/enable-protection4.png)
6. Cliquez sur toofinish de case à cocher hello Ajout d’ordinateurs toohello protection toostart et groupe de réplication initiale pour chaque ordinateur.

   > [!NOTE]
   > Si l’installation push a été préparée, hello service mobilité est installé automatiquement sur les ordinateurs qui n’est pas installé comme elles sont ajoutées à groupe de protection toohello. Une fois que le service de hello est installé, une tâche de protection démarre et échoue. Après échec de hello, vous devez redémarrer toomanually chaque ordinateur qui a été hello service mobilité est installé. Après le redémarrage de hello, une tâche de protection hello commence à nouveau et la réplication initiale se produit.
   >
   >

Vous pouvez surveiller l’état sur hello **travaux** page.

![Surveiller l’état sur la page des travaux hello](./media/site-recovery-vmware-to-azure-classic/enable-protection5.png)

Vous pouvez aussi contrôler l’état de la protection dans **Éléments protégés** > *Nom du groupe de protection* > **Machines virtuelles**. Une fois la réplication initiale est terminée et les données sont synchronisées, trop de changements d’état l’ordinateur**protégé**.

![Surveiller l’état dans Éléments protégés](./media/site-recovery-vmware-to-azure-classic/enable-protection6.png)

## <a name="step-11-set-protected-machine-properties"></a>Étape 11 Définir les propriétés de l’ordinateur protégé
1. Dès qu’une machine présente l’état **Protégé**, vous pouvez configurer ses propriétés de basculement. Dans les détails du groupe de protection de hello, sélectionnez hello hello ordinateur et ouvrir **configurer** onglet.
2. Récupération de site propose des propriétés pour hello Azure VM automatiquement et détecte hello localement les paramètres réseau.

    ![Définir les propriétés des machines virtuelles](./media/site-recovery-vmware-to-azure-classic/vm-properties1.png)
3. Vous pouvez modifier les paramètres suivants :

   * **Nom de la machine virtuelle Azure**: il s’agit nom hello donné toohello machine dans Azure après le basculement. nom de Hello doit être conforme aux exigences d’Azure.
   * **Taille de machine virtuelle Azure**: nombre de hello de cartes réseau est dicté par taille de hello que vous spécifiez pour la machine virtuelle cible hello. Pour plus d’informations sur les tailles et les adaptateurs, consultez hello [la taille des tables](../virtual-machines/linux/sizes.md). Notez les points suivants :

     * Lorsque vous modifiez taille hello d’un ordinateur virtuel et enregistrez les paramètres de hello, nombre hello de cartes réseau change lorsque vous ouvrez hello **configurer** hello d’onglet prochaine. nombre minimal de Hello de cartes réseau de machines virtuelles cible est égal toohello le nombre minimal de cartes réseau sur une machine virtuelle source. nombre maximal de Hello de cartes réseau est déterminé par la taille de hello de machine virtuelle de hello.
       * Si nombre hello de cartes réseau sur l’ordinateur source de hello est inférieur ou égal toohello le nombre de cartes autorisé pour la taille de la machine cible hello, cible de hello aura hello même nombre de cartes en tant que source de hello.
       * Si le nombre de hello de cartes pour l’ordinateur virtuel de hello source dépasse hello autorisé pour la taille cible hello, taille maximale de la cible hello servira.
        Par exemple, si un ordinateur source possède deux cartes réseau et la taille de la machine cible hello prend en charge quatre, l’ordinateur cible hello aura deux cartes. Si ordinateur source de hello possède deux cartes, mais prend en charge la taille de la cible hello pris en charge qu’un seul, de l’ordinateur cible hello aura qu’une seule carte.
     * Si l’ordinateur virtuel de hello possède plusieurs cartes réseau, toutes les cartes doivent être connectée toohello même réseau Azure.
   * **Réseau Azure**: vous devez spécifier un réseau Azure que les machines virtuelles Azure sera connecté tooafter basculement. Si vous ne précisez aucun, hello machines virtuelles Azure ne pourra plus être connecté tooany réseau. En outre, vous devez toospecify un réseau Azure si vous souhaitez toofailback à partir du site local de Azure toohello. La restauration automatique exige une connexion VPN entre un réseau Azure et un réseau local.
   * **Azure/sous-réseau d’adresse IP**: pour chaque carte réseau, sélectionnez hello de toowhich hello sous-réseau Azure VM doit se connecter. Notez que si la carte de réseau hello de l’ordinateur source de hello est toouse configuré une adresse IP statique, vous pouvez spécifier une adresse IP statique pour hello machine virtuelle Azure. Si vous ne fournissez pas d’adresse IP statique, n’importe quelle adresse IP disponible sera allouée. Si l’adresse IP de hello cible est spécifié, mais il est déjà en cours d’utilisation par une autre machine virtuelle dans Azure, le basculement échoue. Si la carte réseau de hello de l’ordinateur source de hello est configuré toouse DHCP, vous avez DHCP en tant que paramètre hello pour Azure.      

## <a name="step-12-create-a-recovery-plan-and-run-a-failover"></a>Étape 12 : Créer un plan de récupération et exécuter le basculement.
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Failover/player]
>
>

Vous pouvez exécuter un basculement pour un seul ordinateur, ou vous pouvez basculer à plusieurs ordinateurs virtuels qui exécutent hello même de tâches ou que vous exécutez hello même charge de travail. toofail sur plusieurs ordinateurs à hello même temps, vous les ajoutez le plan de récupération tooa.

toocreate un plan de récupération :

1. Sur hello **les Plans de récupération** , cliquez sur **ajouter un Plan de récupération** et ajouter un plan de récupération. Spécifier les détails pour le plan de hello et sélectionnez **Azure** comme cible de hello.

 ![Configurer le plan de récupération](./media/site-recovery-vmware-to-azure-classic/recovery-plan1.png)
2. Dans **sélectionner l’ordinateur virtuel**, sélectionnez un groupe de protection, puis sélectionnez les ordinateurs dans le plan de récupération hello groupe tooadd toohello.

 ![Ajouter des machines virtuelles](./media/site-recovery-vmware-to-azure-classic/recovery-plan2.png)

Vous pouvez personnaliser les groupes de toocreate hello plan et ordre de tri hello dans lequel les ordinateurs dans le plan de récupération hello sont basculés. Vous pouvez également ajouter des scripts et des invites pour des actions manuelles. Vous pouvez créer des scripts manuellement ou à l’aide de [runbooks Azure Automation](site-recovery-runbook-automation.md). Pour plus d’informations sur la personnalisation des plans de récupération, consultez [Créer des plans de récupération](site-recovery-create-recovery-plans.md).

## <a name="run-a-failover"></a>Exécuter un basculement
Avant d’exécuter un basculement :

* Assurez-vous que ce serveur d’administration hello est en cours d’exécution et disponible. Si ce n’est pas le cas, le basculement échouera.
* Si vous exécutez un basculement non planifié :

  * Il est préférable d’arrêter les machines principales avant d’exécuter un basculement non planifié lorsque c’est possible. Cela garantit que vous n’avez pas les deux ordinateurs source et réplica hello en hello même temps. Si vous répliquez des ordinateurs virtuels VMware lorsque vous exécutez un basculement non planifié, vous pouvez spécifier que Site Recovery doit essayer de tooshut vers le bas les ordinateurs source hello. En fonction de l’état de hello du site principal de hello, cela peut ou peut ne pas fonctionne. Si vous répliquez des serveurs physiques, Site Recovery ne propose pas cette option.
  * Un basculement non planifié met un terme à la réplication des données à partir des machines principales. Par conséquent, les différences dans les données ne seront pas transférées une fois qu’un basculement non planifié a commencé.
  * Si vous souhaitez tooconnect toohello ordinateur virtuel dans Azure après le basculement, activer la connexion Bureau à distance sur l’ordinateur source de hello avant d’exécuter le basculement de hello. Puis autoriser des connexions RDP via le pare-feu hello. Vous devez également tooallow RDP sur le point de terminaison public hello Hello machine virtuelle Azure après le basculement. Suivez [meilleures pratiques](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) tooensure RDP fonctionne après un basculement.

> [!NOTE]
> tooget hello meilleures performances lorsque vous effectuez un basculement tooAzure, assurez-vous que vous avez installé hello Azure Agent sur l’ordinateur de hello protégé. Cela permet de démarrage de la machine hello plus rapidement et vous aide à diagnostiquer les problèmes. Bonjour Azure Agent n’est disponible pour [Linux](https://github.com/Azure/WALinuxAgent) et [Windows](http://go.microsoft.com/fwlink/?LinkID=394789).
>
>

### <a name="run-a-test-failover"></a>Exécution d’un test de basculement
Exécuter un toosimulate de basculement de test le basculement et les processus de récupération dans un réseau isolé qui n’affecte pas votre environnement de production et de la réplication normale permet de se poursuivre. Test de basculement est initiatd sur la source de hello, et vous pouvez l’exécuter de deux façons :

* **Ne spécifiez pas un réseau Azure**: Si vous exécutez un test de basculement sans réseau, test de hello vérifie que les machines virtuelles démarrer et s’affichent correctement dans Azure. Machines virtuelles n’est connecté tooan réseau Azure après le basculement.
* **Spécifiez un réseau Azure**: ce type de basculement vérifie qu’environnement de réplication dans son intégralité hello s’affiche comme prévu et que les machines virtuelles sont connectée toohello réseau spécifié.

toorun un test de basculement :

1. Sur hello **les Plans de récupération** , sélectionnez le plan de hello et cliquez sur **Test de basculement**.

 ![Sélectionnez le plan de hello](./media/site-recovery-vmware-to-azure-classic/test-failover1.png)
2. Dans **confirmer le Test de basculement**, sélectionnez **aucun** tooindicate que vous ne souhaitez pas toouse un réseau Azure pour hello test de basculement ou test de hello toowhich hello sélectionnez réseau de machines virtuelles est connectée après le basculement. Cliquez sur le basculement de hello toostart hello case à cocher.

 ![Effectuer une sélection](./media/site-recovery-vmware-to-azure-classic/test-failover2.png)
3. Surveiller la progression du basculement sur hello **travaux** onglet.

 ![Surveiller la progression](./media/site-recovery-vmware-to-azure-classic/test-failover3.png)
4. Une fois hello basculement terminé, vous devez également être en mesure de réplica de hello toosee machine Azure s’affichent dans **virtuels** Bonjour portail Azure. Si vous voulez tooinitiate un toohello de connexion RDP machine virtuelle Azure, vous devez le port 3389 tooopen sur le point de terminaison de machine virtuelle hello.
5. Une fois que vous avez terminé, quand basculement atteint hello **Complete** test phase, cliquez sur **effectuer le Test** toofinish. Dans **Notes**, enregistrer et enregistrer toutes les observations associées au basculement de test hello.
6. Cliquez sur **hello test de basculement est terminé** tooautomatically nettoyer l’environnement de test hello. Une fois cette opération est effectuée, test de basculement hello présentent un **Complete** état. Tous les éléments ou machines virtuelles créés automatiquement lors du test de basculement hello sont supprimés. Si un test de basculement continue de plus de deux semaines, il devient toofinish.

### <a name="run-an-unplanned-failover"></a>Exécuter un basculement non planifié
Basculement non planifié est lancé à partir d’Azure et peut être effectué même si le site principal de hello n’est pas disponible.

1. Sur hello **les Plans de récupération** , sélectionnez le plan de hello et cliquez sur **basculement** > **basculement non planifié**.

 ![Sélectionnez le plan de hello](./media/site-recovery-vmware-to-azure-classic/unplanned-failover1.png)
2. Si vous répliquez des machines virtuelles VMware, vous pouvez essayer tooshut machines virtuelles du local vers le bas. Il s’agit d’une action de meilleur effort et continue de basculement si les efforts hello réussit ou non. S’il ne réussit pas, les détails de l’erreur apparaîtra sur hello **travaux** onglet sous **les tâches de basculement non planifié**.

 ![Option d’arrêt des machines virtuelles locales](./media/site-recovery-vmware-to-azure-classic/unplanned-failover2.png)

 > [!NOTE]
 > Cette option n’est pas disponible si vous répliquez des serveurs physiques. Vous devez tootry tooshut celles bas manuellement si possible.
 >
 >

3. Dans **confirmer le basculement**, vérifiez le sens du basculement hello (tooAzure) et sélectionnez hello point de récupération que vous souhaitez toouse pour le basculement hello. Si vous avez activé multi-VM lorsque vous avez configuré les propriétés de réplication, vous pouvez récupérer toohello dernier application cohérentes en cas d’incident ou de point de récupération. Vous pouvez également sélectionner **point de récupération personnalisée** toorecover tooan précédemment point dans le temps. Cliquez sur le basculement de hello toostart hello case à cocher.

 ![Confirmer le sens du basculement](./media/site-recovery-vmware-to-azure-classic/unplanned-failover3.png)
4. Attendez que hello toofinish de travail de basculement non planifié. Vous pouvez surveiller la progression du basculement sur hello **travaux** onglet. Même si des erreurs se produisent pendant le basculement non planifié, le plan de récupération hello s’exécute jusqu'à ce qu’elle est terminée. Vous devez également être en mesure de réplica de hello toosee machine Azure s’affichent dans **virtuels** Bonjour portail Azure.

### <a name="connect-tooreplicated-azure-virtual-machines-after-failover"></a>Se connecter tooreplicated Azure machines virtuelles après basculement
tooconnect tooreplicated virtuels dans Azure après le basculement, vous devez :

- Une connexion Bureau à distance est activée sur l’ordinateur principal hello.
- Le pare-feu Windows sur l’ordinateur principal hello définir tooallow RDP.
- RDP ajouté toohello un point de terminaison public pour hello machine virtuelle Azure.

Pour plus d’informations sur la configuration de ces éléments, consultez [Troubleshooting remote desktop connection after failover using ASR](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) (Résolution des problèmes de connexion Bureau à distance après un basculement à l’aide d’ASR).

## <a name="deploy-additional-process-servers"></a>Déployer d’autres serveurs de traitement
Si vous devez faire évoluer votre déploiement au-delà de 200 machines sources, ou si votre taux d’évolution du quotidien total est supérieure à 2 To, vous devez le volume de trafic de processus supplémentaire serveurs toohandle hello. tooset d’un serveur de processus supplémentaire, vérification des exigences de hello dans [serveurs de traitement supplémentaires](#additional-process-servers), et puis configurer le serveur de processus hello selon toohello suivant les instructions fournies. Après avoir configuré le serveur de hello, vous pouvez configurer la source machines toouse il.

### <a name="set-up-an-additional-process-server"></a>Configurer un serveur de traitement supplémentaire
Pour configurer un serveur de traitement supplémentaire, procédez comme suit :

* Exécutez hello unifiée Assistant tooconfigure un serveur d’administration en tant que processus serveur uniquement.
* Si vous souhaitez que la réplication des données toomanage à l’aide uniquement hello nouveau serveur de processus, vous devez toomigrate vos ordinateurs protégés.

### <a name="install-hello-process-server"></a>Installer le serveur de processus hello
1. Sur hello **Quick Start** page, téléchargez le fichier d’installation unifiée hello pour hello installation des composants de Site Recovery. Exécutez le programme d’installation.
2. Dans **avant de commencer**, sélectionnez **ajouter tooscale de serveurs de processus supplémentaire déploiement**.

 ![Ajouter un serveur de traitement](./media/site-recovery-vmware-to-azure-classic/add-ps1.png)
3. Assistant hello comme vous le faisiez quand vous [configurer](#step-5-install-the-management-server) premier serveur d’administration hello.
4. Dans **détails de Configuration serveur**, entrez l’adresse IP de hello hello d’origine du serveur d’administration sur lequel vous avez installé le serveur de configuration hello, puis entrez la phrase secrète de hello. Si vous n’avez pas de mot de passe hello, exécutez  **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** sur hello d’origine management server tooretrieve il.

 ![Détails du serveur de configuration](./media/site-recovery-vmware-to-azure-classic/add-ps2.png)

### <a name="migrate-machines-toouse-hello-new-process-server"></a>Migrer des machines toouse hello nouveau serveur de processus
1. Ouvrez **serveurs de Configuration** > **Server** > *nom du serveur d’administration d’origine hello*  >   **Détails du serveur**.

 ![Détails du serveur](./media/site-recovery-vmware-to-azure-classic/update-process-server1.png)
2. Bonjour **serveurs de processus** liste, sélectionnez **modifier le processus serveur** serveur toohello suivant que vous souhaitez toochange.

 ![Serveur de processus de mise à jour hello](./media/site-recovery-vmware-to-azure-classic/update-process-server2.png)
3. Sélectionnez **modifier le serveur de processus**, sélectionnez **serveur de processus cible**, et puis sélectionnez hello nouveau serveur d’administration. Machines virtuelles hello sélectionnez hello nouveau serveur de processus gérera. Cliquez sur hello icône tooget d’informations sur le serveur de hello. espace moyen Hello tooreplicate chaque ordinateur virtuel sélectionné toohello nouveau serveur de processus est affichée toohelp vous que la charge des décisions que nécessaire. Cliquez sur toostart de case à cocher hello toohello nouveau serveur de processus de réplication.

 ![Changer de serveur de processus hello](./media/site-recovery-vmware-to-azure-classic/update-process-server3.png)

## <a name="vmware-permissions-for-vcenter-access"></a>Autorisations VMware pour l’accès au vCenter
serveur de processus Hello peut détecter automatiquement les ordinateurs virtuels sur un serveur vCenter. tooperform la détection automatique, vous devez toodefine un rôle (Azure_Site_Recovery) sur le serveur vCenter de hello vCenter tooallow au niveau Site Recovery tooaccess hello. Si uniquement, vous devez toomigrate VMware machines tooAzure et que vous n’avez pas besoin de toofailback à partir d’Azure, vous pouvez définir un rôle en lecture seule qui est suffisant. Définir des autorisations de hello, comme décrit dans [étape 6 : configurer les informations d’identification pour le serveur vCenter hello](#step-6-set-up-credentials-for-the-vcenter-server). autorisations de rôle Hello sont résumées dans hello tableau suivant :

| **Rôle** | **Détails** | **Autorisations** |
| --- | --- | --- |
| Rôle Azure_Site_Recovery |Détection de machine virtuelle VMware |Attribuer ces privilèges pour le serveur de v-Center hello :<br/><br/>Banque de données : Allouer de l’espace, Parcourir la banque de données, Opérations de fichier de bas niveau, Supprimer le fichier, Mettre à jour les fichiers de machine virtuelle<br/><br/>Réseau : Attribution de réseau<br/><br/>Ressources : Affecter pool de machines virtuelles tooresource, migrer hors tension l’ordinateur virtuel, migrer sous tension l’ordinateur virtuel<br/><br/>Tâches : Créer une tâche, Mettre à jour une tâche<br/><br/>Machine virtuelle > Configuration<br/><br/>Machine virtuelle > Interagir > Répondre à la question, Connexion d’appareil, Configurer un support de CD, Configurer une disquette, Mettre hors tension, Mettre sous tension, Installation des outils VMware<br/><br/>Machine virtuelle > Stock > Créer, Inscrire, Désinscrire<br/><br/>Machine virtuelle > Approvisionnement > Autoriser le téléchargement de machines virtuelles, Autoriser le chargement de fichiers de machine virtuelle<br/><br/>Machine virtuelle > Instantanés > Supprimer les instantanés |
| Rôle d’utilisateur vCenter |Découverte/Basculement de machine virtuelle VMware sans arrêt de la machine virtuelle source |Attribuer ces privilèges pour le serveur de v-Center hello :<br/><br/>Objet de centre de données > propager tooChild objet, rôle = lecture seule <br/><br/>utilisateur de Hello est assignée au niveau du centre de données hello et par conséquent, a accès tooall hello objets dans le centre de données hello. Si vous souhaitez accéder de hello toorestrict, affecter hello **aucun accès** rôle avec hello **propager toochild** toohello (ordinateurs hôtes ESX, magasins de données, machines virtuelles et réseaux) des objets enfants de l’objet. |
| Rôle d’utilisateur vCenter |Basculement et restauration automatique |Attribuer ces privilèges pour le serveur de v-Center hello :<br/><br/>Objet de centre de données – propager toochild objet, rôle = Azure_Site_Recovery<br/><br/>utilisateur de Hello est assignée au niveau du centre de données et par conséquent, a accès tooall hello objets dans le centre de données hello.  Si vous souhaitez accéder de hello toorestrict, affecter hello ** aucun accès ** rôle avec hello **propager toochild objet** objet enfant qui toohello (ordinateurs hôtes ESX, magasins de données, machines virtuelles et réseaux). |

## <a name="third-party-software-notices-and-information"></a>Informations et remarques relatives aux logiciels tiers
<!--Do Not Translate or Localize-->

logiciels de Hello et de microprogramme en cours d’exécution hello produit Microsoft ou service repose sur ou inclut, du contenu à partir de hello projets répertoriés ci-dessous (collectivement, « Code tiers »).  Microsoft est hello pas auteur de hello Code de tiers.  mention de copyright d’origine Hello et de licence, dans lesquelles Microsoft a reçu ce Code tiers, sont définies ci-dessous.

informations Hello dans la Section A concerne un Code de tiers des composants à partir de projets de hello répertoriées ci-dessous. Such licenses and information are provided for informational purposes only.  Ce Code de tiers est en cours tooyou relicensed par Microsoft hello produit ou service Microsoft termes du contrat de licence des logiciels de Microsoft.  

informations Hello dans la Section B concernant les composants de Code de tiers qui sont établies tooyou disponible par Microsoft sous les termes du contrat de licence d’origine hello.

fichier dans son intégralité Hello se trouve sur hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel or otherwise.

## <a name="next-steps"></a>Étapes suivantes
[En savoir plus sur la restauration automatique](site-recovery-failback-azure-to-vmware-classic.md) toobring vos machines ayant basculé en cours d’exécution dans Azure sauvegarder l’environnement local de tooyour.
