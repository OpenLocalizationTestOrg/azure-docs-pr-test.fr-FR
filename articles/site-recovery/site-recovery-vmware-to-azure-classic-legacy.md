---
title: "aaaReplicate les ordinateurs virtuels VMware et des serveurs physiques tooAzure (classique hérité) | Documents Microsoft"
description: "Décrit comment tooreplicate local machines virtuelles et tooAzure de serveurs physiques Windows/Linux à l’aide d’Azure Site Recovery dans un déploiement hérité dans le portail classique de hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: f980fb52-8ec2-4dd9-85e2-8e52e449f1ba
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: raynew
ms.openlocfilehash: 64c6d906d54426fdd2b884350542a4562bb12528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-and-physical-servers-tooazure-with-azure-site-recovery-using-hello-classic-portal-legacy"></a>Répliquer les machines virtuelles VMware et des serveurs physiques tooAzure avec Azure Site Recovery à l’aide du portail classique de hello (hérité)
> [!div class="op_single_selector"]
> * [portail Azure](site-recovery-vmware-to-azure.md)
> * [Portail Classic](site-recovery-vmware-to-azure-classic.md)
> * [Portail Classic (version héritée)](site-recovery-vmware-to-azure-classic-legacy.md)
>
>

Récupération de Site de tooAzure Bienvenue ! Cet article décrit un déploiement hérité pour répliquer des ordinateurs virtuels VMware localement ou tooAzure de serveurs physiques Windows/Linux à l’aide d’Azure Site Recovery dans le portail classique de hello.

## <a name="overview"></a>Vue d'ensemble
Les organisations besoin d’une stratégie BCDR qui détermine comment les charges de travail, les applications et données restent en cours d’exécution et disponibles pendant le temps d’arrêt planifiés et non planifiés et récupérer les conditions de travail toonormal dès que possible. Votre stratégie BCDR doit assurer la sécurisation et la récupération des données d’entreprise, ainsi que la disponibilité continue des charges de travail suite à un sinistre.

Récupération de site est un service Azure qui contribue de stratégie BCDR tooyour en orchestrant ces opérations de réplication de serveurs physiques locaux et les machines virtuelles toohello cloud (Azure) ou tooa de centre de données secondaire. En cas de pannes dans votre emplacement principal, vous basculez toohello emplacement secondaire tookeep applications et charges de travail disponibles. Vous ne parvenez pas emplacement principal d’arrière tooyour lorsqu’elle retourne les opérations de toonormal. Pour plus d’informations, consultez [Qu’est-ce que le service Azure Site Recovery ?](site-recovery-overview.md)

> [!WARNING]
> Cet article contient des **instructions héritées**. Il ne concerne pas les nouveaux déploiements. Au lieu de cela, [suivez ces instructions](site-recovery-vmware-to-azure.md) toodeploy Site Recovery Bonjour portail Azure, ou [Utilisez ces instructions](site-recovery-vmware-to-azure-classic.md) tooconfigure hello amélioré de déploiement dans le portail classique de hello. Si vous avez déjà déployé à l’aide de la méthode hello décrit dans cet article, nous vous recommandons de migrer déploiement toohello améliorée dans le portail classique de hello.
>
>

## <a name="migrate-toohello-enhanced-deployment"></a>Migrer les déploiement toohello améliorée
Cette section est uniquement pertinente si vous avez déjà déployé la récupération de Site à l’aide des instructions de hello dans cet article.

toomigrate votre déploiement existant, vous devez :

1. Déployez de nouveaux composants Site Recovery sur votre site local.
2. Configurer les informations d’identification pour la détection automatique des ordinateurs virtuels VMware sur le nouveau serveur de configuration hello.
3. Découvrir les serveurs de VMware hello avec le nouveau serveur de configuration hello.
4. Créer un nouveau groupe de protection avec le nouveau serveur de configuration hello.

Avant de commencer :

* Nous vous recommandons de définir une fenêtre de maintenance pour la migration.
* Hello **migrer les ordinateurs** option est disponible uniquement si vous avez des groupes de protection existants qui ont été créés lors d’un déploiement hérité.
* Après avoir terminé les étapes de migration hello peut prendre 15 minutes ou informations d’identification de plus de temps toorefresh hello et machines virtuelles toodiscover et actualisation afin que vous pouvez les ajouter groupe de protection tooa. Vous pouvez procéder à une actualisation manuelle au lieu d’attendre.

Exécutez la migration comme suit :

1. En savoir plus sur [améliorée du déploiement dans le portail classique de hello](site-recovery-vmware-to-azure-classic.md). Hello révision améliorée [architecture](site-recovery-vmware-to-azure-classic.md), et [conditions préalables](site-recovery-vmware-to-azure-classic.md).
2. Désinstaller le service de mobilité hello à partir d’ordinateurs que vous effectuez une réplication actuellement. Une nouvelle version du service de hello sera être installée sur les ordinateurs hello lorsque vous les ajoutez toohello nouveau groupe de protection.
3. Télécharger un [clé d’inscription du coffre](site-recovery-vmware-to-azure-classic.md) et [exécuter l’Assistant d’installation unifiée hello](site-recovery-vmware-to-azure-classic.md) master, serveur de processus et serveur de configuration tooinstall hello ciblent des composants serveur. Apprenez-en plus sur la [planification de la capacité](site-recovery-vmware-to-azure-classic.md).
4. [Configurer les informations d’identification](site-recovery-vmware-to-azure-classic.md) que Site de récupération peuvent utiliser tooaccess VMware server tooautomatically découvrir les ordinateurs virtuels VMware. Découvrez les [autorisations requises](site-recovery-vmware-to-azure-classic.md).
5. Ajoutez des [serveurs vCenter ou des hôtes vSphere](site-recovery-vmware-to-azure-classic.md). Il peut prendre 15 minutes pour plus d’informations pour les serveurs tooappear dans le portail Site Recovery hello.
6. Créez un [groupe de protection](site-recovery-vmware-to-azure-classic.md). Afin que les ordinateurs virtuels hello sont découverts et peut prendre jusqu'à minutes too15 toorefresh de portail hello. Si vous ne souhaitez pas toowait vous pouvez mettre en surbrillance le nom du serveur gestion hello (ne cliquez pas dessus) > **Actualiser**.
7. Nouveau groupe de protection hello sur **migrer les ordinateurs**.

    ![Ajouter un compte](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration1.png)
8. Dans **sélectionner des ordinateurs** hello sélectionnez protection groupe souhaité toomigrate à partir de, hello machines que vous souhaitez toomigrate.

    ![Ajouter un compte](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration2.png)
9. Dans **configurer les paramètres de cible** spécifier si vous souhaitez toouse hello les mêmes paramètres pour tous les ordinateurs et serveur de processus sélectionnez hello et compte de stockage Azure. Si vous n’avez pas un serveur de processus séparé, il s’agit adresse hello hello hello server du serveur de configuration.

    ![Ajouter un compte](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration3.png)

    > [AZURE.NOTE] [Migration de comptes de stockage](../resource-group-move-resources.md) entre les ressources groupes dans hello même abonnement ou entre abonnements n’est pas prise en charge pour les comptes de stockage utilisés pour le déploiement de Site Recovery.

1. Dans **spécifier les comptes**, sélectionnez le compte hello vous avez créé pour hello processus serveur tooaccess hello la nouvelle version de hello de toopush d’ordinateur du service de mobilité hello.

   ![Ajouter un compte](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration4.png)
2. Récupération de site migrerez votre compte de stockage Azure toohello les données répliquées que vous avez fourni. Si vous le souhaitez, vous pouvez réutiliser compte de stockage hello que vous avez utilisé dans un déploiement hérité de hello.
3. Tâche de hello machines virtuelles de fin se synchronise automatiquement. Une fois la synchronisation terminée, vous pouvez supprimer virtuels hello hello hérité du groupe de protection.
4. Une fois que tous les ordinateurs ont été migrés vous pouvez supprimer le groupe de protection héritée hello.
5. N’oubliez pas de propriétés de basculement toospecify hello pour les ordinateurs et hello paramètres réseau Azure après que la synchronisation est terminée.
6. Si vous avez des plans de récupération existants, vous pouvez migrer les déploiement toohello améliorée avec hello **migrer le Plan de récupération** option. Vous ne devez faire cela que lorsque toutes les machines protégées ont été migrées.

   ![Ajouter un compte](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration5.png)

> [!NOTE]
> Une fois que vous avez terminé la migration poursuivre hello [article améliorée](site-recovery-vmware-to-azure-classic.md). rest Hello de cet article hérité ne seront plus pertinentes et vous n’avez pas besoin toofollow tout plus hello les étapes décrites dans l’informatique **.
>
>

## <a name="what-do-i-need"></a>De quoi ai-je besoin ?
Ce diagramme illustre les composants de déploiement hello.

![Nouveau coffre](./media/site-recovery-vmware-to-azure-classic-legacy/architecture.png)

Voici ce dont vous aurez besoin :

| **Composant** | **Déploiement** | **Détails** |
| --- | --- | --- |
| **Serveur de configuration** |Une machine virtuelle A3 standard Azure Bonjour même abonnement que la récupération de Site. |serveur de configuration Hello coordonne les communications entre les ordinateurs protégés, serveur de processus hello et serveurs cible maître dans Azure. Il configure la réplication et coordonne la récupération dans Azure lors du basculement. |
| **Serveur cible maître** |Une machine virtuelle Azure, un serveur Windows basé sur une image de la galerie Windows Server 2012 R2 (ordinateurs de Windows tooprotect) ou comme un serveur Linux basée sur une image de la galerie d’OpenLogic CentOS 6.6 (tooprotect les ordinateurs Linux).<br/><br/> Trois options de dimensionnement sont disponibles : A4 standard, D14 standard et DS4 standard.<br/><br/> serveur Hello est connecté toohello même réseau Azure en tant que serveur de configuration hello.<br/><br/> Vous avez configuré dans le portail Site Recovery hello |Il reçoit et stocke les données répliquées à partir de vos machines protégées à l’aide de disques durs virtuels attachés créés sur le stockage d’objets blob dans votre compte Azure Storage.<br/><br/> Sélectionnez DS4 standard pour configurer la protection des charges de travail nécessitant des performances élevées et cohérentes ainsi qu’une faible latence à l’aide d’un compte Premium Storage. |
| **Serveur de traitement** |Un serveur virtuel ou physique local exécutant Windows Server 2012 R2<br/><br/> Nous vous recommandons d’elle a placé sur hello même réseau et le segment de réseau local en tant qu’ordinateurs hello que vous le souhaitez tooprotect, mais il peut s’exécuter sur un autre réseau tant que machines protégées ont L3 tooit de visibilité du réseau.<br/><br/> Configurer et de serveur de configuration toohello l’enregistrer dans le portail Site Recovery hello. |Serveur de processus de réplication données toohello local d’envoi des ordinateurs protégés. Il possède une cache disque toocache la réplication de données qu’il reçoit. Il exécute un certain nombre d’actions sur les données.<br/><br/> Cela permet d’optimiser les données par la mise en cache, la compression et le chiffrant avant de l’envoyer sur le serveur cible maître de toohello.<br/><br/> Gestion de l’installation push du Service mobilité de hello.<br/><br/> Il procède à la découverte automatisée des machines virtuelles VMWare. |
| **Ordinateurs locaux** |Machines virtuelles VMware locales ou serveurs physiques exécutant Windows ou Linux. |Vous configurez les paramètres de réplication qui s’appliquent à une ou plusieurs machines. Vous pouvez basculer une machine individuelle ou, plus fréquemment, plusieurs machines virtuelles rassemblées dans un plan de récupération. |
| **Service de mobilité** |Installé sur chaque ordinateur virtuel ou d’un serveur physique, vous souhaitez tooprotect<br/><br/> Peut être installé manuellement ou envoyées et installé automatiquement par le serveur de processus hello lorsque vous activez la réplication pour un ordinateur. |Hello service mobilité envoie le serveur de traitement de données toohello lors de la réplication initiale (resync). Une fois l’ordinateur de hello dans un état de protection (une fois la resynchronisation terminée) hello service mobilité capture toodisk écritures en mémoire et les envoie de serveur de processus toohello. Le service VSS apporte la cohérence des applications pour les serveurs Windows. |
| **Coffre Azure Site Recovery** |Vous créez un coffre de récupération de Site avec un abonnement Azure et inscrivez les serveurs dans le coffre hello. |coffre de Hello coordonne et orchestre la réplication des données, le basculement et la récupération entre votre site local et le Azure. |
| **Mécanisme de réplication** |**Sur hello Internet**: communique et réplique les données à partir de tooAzure de serveurs de site protégé à l’aide d’un canal sécurisé SSL/TLS sur hello internet. Il s’agit d’option par défaut de hello.<br/><br/> **VPN/ExpressRoute**: communique et réplique les données entre les serveurs locaux et Azure par le biais d’une connexion VPN. Vous devez tooset un VPN de site à site ou d’une connexion ExpressRoute entre votre site local et le réseau Azure.<br/><br/> Vous devez sélectionner la façon dont vous souhaitez tooreplicate durant le déploiement de la récupération de Site. Vous ne pouvez pas modifier le mécanisme de hello après que qu’il est configuré sans impact sur la réplication des ordinateurs existants. |Aucune de ces options requiert vous tooopen tous les ports réseau entrant sur les ordinateurs protégés. Toutes les communications réseau sont lancée à partir du site local de hello. |

## <a name="capacity-planning"></a>Planification de la capacité
Hello les domaines, vous devez tooconsider :

* **Environnement source**: hello infrastructure VMware, les paramètres de l’ordinateur source et les exigences.
* **Composants serveur**: hello du serveur de traitement, de serveur de configuration et de serveur cible maître

### <a name="considerations-for-hello-source-environment"></a>Considérations pour l’environnement source hello
* **Taille maximale de disque**: hello actuel taille maximale de disque hello qui peut être attachés tooa virtual machine est de 1 To. Par conséquent, hello taille maximale d’un disque source qui peut être répliqué est également limité too1 to.
* **Taille maximale par source**: hello de taille maximale d’un ordinateur source unique est de 31 To (avec 31 disques) et avec une instance D14 configurés pour le serveur cible maître de hello.
* **Nombre de sources par serveur cible maître**: plusieurs ordinateurs source peuvent être protégés avec un seul serveur cible maître. Toutefois, un ordinateur source unique ne peut pas protéger sur plusieurs serveurs cible maître, car comme répliquent les disques, un disque dur virtuel qui reflète la taille de hello du disque de hello est créé sur le stockage d’objets blob Azure et attaché en tant que données disque toohello cible maître serveur.  
* **Taux de modification quotidien maximale par source**: il existe trois facteurs qui doivent toobe considéré comme lorsque vous envisagez de hello recommandé de modification taux par source. Pour des considérations relatives à la cible en fonction hello deux IOPS sont requis sur le disque cible de hello pour chaque opération de source de hello. Il s’agit, car une lecture d’anciennes données et une écriture de nouvelles données de hello aura lieu sur le disque cible de hello.
  * **Modifier tous les jours des taux de prise en charge par le serveur de processus hello**: un ordinateur source ne peut pas s’étendre sur plusieurs serveurs de traitement. Un serveur de processus unique peut prendre en charge jusqu'à to too1 du taux de modification quotidien. Par conséquent 1 To est pris en charge pour un ordinateur source des taux de modification de données quotidiens de hello maximale.
  * **Débit maximal pris en charge par le disque de cible hello**: évolution maximale par disque source ne peut pas être plus de 144 Go/jour (avec une taille d’écriture de 8 Ko). Consultez hello de section de serveur cible maître hello pour un débit hello et les e/s de cible hello pour différentes tailles d’écriture. Étant donné que chaque source IOP génère 2 e/s sur le disque cible de hello, ce nombre doit être divisé par deux. En savoir plus sur [des cibles de performances et évolutivité Azure](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) lors de la configuration cible hello pour les comptes de stockage premium.
  * **Débit maximal pris en charge par le compte de stockage hello**: une source ne peut pas couvrir plusieurs comptes de stockage. Étant donné qu’un compte de stockage prend un maximum de 20 000 demandes par seconde et que chaque source IOP génère des 2 IOPS sur le serveur cible maître de hello, nous recommandons de que conserver de nombre hello d’IOPS sur hello source too10, 000. En savoir plus sur [des cibles de performances et évolutivité Azure](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) lors de la configuration de source de hello pour les comptes de stockage premium.

### <a name="considerations-for-component-servers"></a>Considérations relatives aux serveurs de composants
Le tableau 1 récapitule les tailles de machine virtuelle hello pour la configuration de hello et serveurs cibles maîtres.

| **Composant** | **Instances Azure déployées** | **Cœurs** | **Mémoire** | **Disques max** | **Taille du disque** |
| --- | --- | --- | --- | --- | --- |
| Serveur de configuration |A3 standard |4 |7 Go |8 |1 023 Go |
| Serveur cible maître |A4 standard |8 |14 Go |16 |1 023 Go |
| D14 standard |16 |112 Go |32 |1 023 Go | |
| DS4 standard |8 |28 Go |16 |1 023 Go | |

**Tableau 1**

#### <a name="process-server-considerations"></a>Considérations relatives aux serveurs de traitement
Dimensionnement du serveur dépend généralement les taux de modification quotidien hello dans toutes les charges de travail protégées.

* Vous devez les tâches de tooperform suffisante calcul telles que la compression en ligne et le chiffrement.
* serveur de processus Hello utilise le cache disque. Vérifiez que hello recommandé d’espace dans le cache et débit de disque est stockées dans l’événement hello de goulot d’étranglement du réseau ou d’une panne les modifications de données disponible toofacilitate hello.
* Vérifiez la bande passante suffisante afin que hello serveur de processus peut télécharger protection continue des données tooprovide de la cible maître toohello hello données serveur.

Tableau 2 fournit un résumé des recommandations de serveur de processus hello.

| **Taux de modification des données** | **UC** | **Mémoire** | **Taille du disque cache** | **Débit du disque cache** | **Bande passante en entrée/sortie** |
| --- | --- | --- | --- | --- | --- |
| < 300 Go |4 processeurs virtuels (2 sockets * 2 cœurs à 2,5 GHz) |4 Go |600 Go |too10 7 des Mo par seconde |30 Mbits/s / 21 Mbits/s |
| too600 300 Go |8 processeurs virtuels (2 sockets * 4 cœurs à 2,5 GHz) |6 Go |600 Go |Mo too15 11 par seconde |60 Mbits/s / 42 Mbits/s |
| 600 Go too1 to |12 processeurs virtuels (2 sockets * 6 cœurs à 2,5 GHz) |8 Go |600 Go |Mo too20 16 par seconde |100 Mbits/s / 70 Mbits/s |
| > 1 To |Déployer un autre serveur de traitement | | | | |

**Tableau 2**

Où :

* Entrée est la bande passante de téléchargement (intranet entre le serveur source et le processus hello).
* En sortie est la bande passante de téléchargement (internet entre le serveur de processus hello et le serveur cible maître). Les nombres concernant la sortie supposent une compression de serveur de traitement moyenne de 30 %.
* Pour le disque cache, un disque de système d'exploitation distinct de 128 Go minimum est recommandé pour tous les serveurs de traitement.
* Pourquoi de débit du cache disque suivant de stockage a été utilisé pour des tests de performances : 8 disques SAS de 10 K TPM avec une configuration RAID 10.

#### <a name="configuration-server-considerations"></a>Considérations relatives aux serveurs de configuration
Chaque serveur de configuration peut prendre en charge des machines de sources too100 avec des volumes de 3 et 4. Si votre déploiement est plus étendu, nous vous recommandons de déployer un autre serveur de configuration. Voir le tableau 1 pour les propriétés d’ordinateur virtuel par défaut hello hello du serveur de configuration.

#### <a name="master-target-server-and-storage-account-considerations"></a>Considérations relatives aux comptes de stockage et serveurs cibles maîtres
stockage Hello pour chaque serveur cible maître inclut un disque de système d’exploitation, d’un volume de rétention et de disques de données. lecteur de rétention Hello conserve un journal hello des modifications de disque pour la durée de conservation hello définie dans le portail Site Recovery hello hello.  Pour les propriétés d’ordinateur virtuel hello du serveur cible maître de hello, voir tooTable 1. Le tableau 3 illustre l’utilisation des disques hello a4.

| **Instance** | **Disque de système d’exploitation** | **Rétention** | **Disques de données** |
| --- | --- | --- | --- |
| **Rétention** |**Disques de données** | | |
| A4 standard |1 disque (1 * 1 023 Go) |1 disque (1 * 1 023 Go) |15 disques (15 * 1 023 Go) |
| D14 standard |1 disque (1 * 1 023 Go) |1 disque (1 * 1 023 Go) |31 disques (15 * 1 023 Go) |
| DS4 standard |1 disque (1 * 1 023 Go) |1 disque (1 * 1 023 Go) |15 disques (15 * 1 023 Go) |

**Tableau 3**

Dépend de la planification de capacité pour le serveur cible maître de hello :

* Limitations et performances de stockage Azure
  * nombre maximal de Hello d’utilisation des disques pour un niveau Standard pour machine virtuelle hautement, est d’environ 40 (20 000/500 IOPS par disque) dans un seul compte de stockage. Pour en savoir plus, consultez [Objectifs d’évolutivité pour les comptes de stockage standard](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) et [Objectifs d’évolutivité pour les comptes de stockage premium](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).
* Taux de modification quotidien
* Stockage de volume de rétention.

Notez les points suivants :

* Une seule source ne peut pas couvrir plusieurs comptes de stockage. Disque de données toohello qui vont toohello les comptes de stockage sélectionnés lorsque vous configurez la protection s’applique. disques de rétention de système d’exploitation et hello Hello accédez généralement toohello déployé automatiquement le compte de stockage.
* volume de stockage de rétention Hello requis dépend du taux de modification quotidien hello et hello de jours de rétention. stockage de rétention requise par le serveur cible maître de Hello = évolution totale du code à partir de la source par jour * nombre de jours de rétention.
* Chaque serveur cible maître n'a qu'un seul volume de rétention. volume de rétention Hello est partagé entre le serveur cible maître de hello disques toohello attaché. Par exemple :
  * S’il existe un ordinateur source avec 5 disques, et chaque disque génère 120 e/s (taille de 8 Ko) sur la source de hello, cela traduit too240 d’IOPS par disque (2 opérations sur le disque cible de hello par source d’e/s). 240 IOPS se trouve dans hello Azure limite des e/s de disque de 500 par.
  * Sur le volume de rétention hello, cela devient 120 * 5 = 600 e/s et cela peuvent devenir un goulot d’eau. Dans ce scénario, une bonne stratégie serait être tooadd volume de rétention plus disques toohello et span transmettons, comme une configuration de bandes RAID. Cela améliore les performances car hello IOPS sont distribués sur plusieurs lecteurs. nombre de Hello de lecteurs toobe ajouté volume de rétention toohello seront comme suit :
    * Nombre total d'IOPS à partir de l'environnement source / 500
    * Attrition totale par jour à partir de l'environnement source (non compressé) / 287 Go. 287 Go est le débit maximal de hello pris en charge par un disque cible par jour. Cette mesure varient en fonction de la taille d’écriture hello avec un facteur de 8 Ko, car dans ce cas 8K est trois pris par défaut de la taille de l’écriture. Par exemple, si la taille d’écriture hello est 4K débit sera 287/2. Et si la taille d’écriture hello est de 16 Ko débit sera 287 * 2.
* Hello du nombre de comptes de stockage requise = source total IOPs/10000.

## <a name="before-you-start"></a>Avant de commencer
| **Composant** | **Configuration requise** | **Détails** |
| --- | --- | --- |
| **Compte Azure** |Vous aurez besoin d’un compte [Microsoft Azure](https://azure.microsoft.com/) . Vous pouvez commencer avec une [version d'évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/). | |
| **Stockage Azure** |Vous aurez besoin d’un stockage Azure compte toostore répliquée de données<br/><br/> Des comptes hello doivent être un [Standard compte de stockage géo-redondant](../storage/common/storage-redundancy.md#geo-redundant-storage) ou [compte de stockage Premium](../storage/common/storage-premium-storage.md).<br/><br/> Il doit en hello même région que hello service Azure Site Recovery et être associé à hello même abonnement. Nous ne prennent pas en charge déplacement hello de comptes de stockage créé à l’aide de hello [nouveau portail Azure](../storage/common/storage-create-storage-account.md) plusieurs groupes de ressources.<br/><br/> toolearn plus lire [Introduction tooMicrosoft stockage Azure](../storage/common/storage-introduction.md) | |
| **Réseau virtuel Azure** |Vous aurez besoin d’un réseau virtuel Azure sur le hello serveur de configuration et le serveur cible maître seront déployés. Elle doit être hello même abonnement et région que le coffre Azure Site Recovery hello. Si vous souhaitez que les données tooreplicate sur un hello de connexion Azure ExpressRoute ou VPN virtuel réseau doit être de réseau local de tooyour connecté via une connexion ExpressRoute ou d’un VPN de Site à Site. | |
| **Ressources Azure** |Assurez-vous que vous avez suffisamment toodeploy de ressources Azure, tous les composants. En savoir plus sur les [limites d’abonnement Azure](../azure-subscription-service-limits.md). | |
| **Machines virtuelles Azure** |Machines virtuelles tooprotect doivent respecter les [conditions préalables Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).<br/><br/> **Nombre de disques** : un serveur protégé peut prendre en charge jusqu’à 31 disques.<br/><br/> **Taille des disques** : la capacité d’un disque ne doit pas dépasser 1023 Go.<br/><br/> **Clustering** : les serveurs en cluster ne sont pas pris en charge.<br/><br/> **Démarrage** : le démarrage UEFI (Unified Extensible Firmware Interface)/EFI (Extensible Firmware Interface) n’est pas pris en charge.<br/><br/> **Volumes** : les volumes chiffrés par Bitlocker ne sont pas pris en charge.<br/><br/> **Noms des serveurs**: les noms doivent contenir entre 1 et 63 caractères (lettres, chiffres et traits d’union). Hello doit commencer par une lettre ou un chiffre et se terminer par une lettre ou un chiffre. Une fois qu’un ordinateur est protégé, vous pouvez modifier hello nom Azure. | |
| **Serveur de configuration** |Ordinateur de virtuel A3 standard basé sur une image de la galerie Azure Site Recovery Windows Server 2012 R2 sera créé dans votre abonnement pour le serveur de configuration hello. Il est créé en tant que hello première instance d’un nouveau service cloud. Si vous sélectionnez Internet Public comme type de connectivité hello pour le service cloud hello hello configuration serveur sera créé avec une adresse IP publique réservée.<br/><br/> chemin d’installation de Hello doit être uniquement des caractères anglais. | |
| **Serveur cible maître** |Machine virtuelle Azure, A4 standard, D14 standard ou DS4 standard.<br/><br/> chemin d’installation de Hello doit être uniquement des caractères anglais. Par exemple le chemin d’accès hello doit être **/usr/local/ASR** pour un serveur cible maître Linux en cours d’exécution. | |
| **Serveur de traitement** |Vous pouvez déployer le serveur de processus hello sur l’ordinateur physique ou virtuel exécutant Windows Server 2012 R2 avec les dernières mises à jour de hello. Installez-le sur C:/.<br/><br/> Nous vous recommandons de placer de serveur de hello sur hello même réseau et sous-réseau que hello machines que vous souhaitez tooprotect.<br/><br/> Installez VMware vSphere CLI 5.5.0 sur le serveur de processus hello. composant de Hello VMware vSphere CLI est requis sur le serveur de traitement hello ordre toodiscover virtuels gérés par un serveur vCenter ou machines virtuelles s’exécutant sur un ordinateur hôte ESXi.<br/><br/> chemin d’installation de Hello doit être uniquement des caractères anglais.<br/><br/> Le système de fichiers ReFS n’est pas pris en charge. | |
| **VMware** |Un serveur VMware vCenter qui gère vos hyperviseurs VMware vSphere. Il doit exécuter vCenter version 5.1 ou 5.5 avec les dernières mises à jour de hello.<br/><br/> Un ou plusieurs hyperviseurs vSphere contenant des ordinateurs virtuels VMware que vous souhaitiez tooprotect. Hello hyperviseur doit être en cours d’exécution ESX/ESXi version 5.1 ou 5.5 avec les dernières mises à jour de hello.<br/><br/> Les outils VMware doivent être installés et en cours d’exécution sur les machines virtuelles VMware. | |
| **Ordinateurs Windows** |Les serveurs physiques ou les machines virtuelles VMware protégés exécutant Windows sont associés à un certain nombre de prérequis.<br/><br/> Système d’exploitation 64 bits pris en charge : **Windows Server 2012 R2**, **Windows Server 2012** ou **Windows Server 2008 R2 avec au moins SP1**.<br/><br/> Hello nom d’hôte, des points de montage, les noms des périphériques, chemin d’accès de système de Windows (par exemple : C:\Windows) doit être en anglais uniquement.<br/><br/> système d’exploitation de Hello doit être installé sur le lecteur C:\.<br/><br/> Seuls les disques de base sont pris en charge. Les disques dynamiques ne sont pas pris en charge.<br/><br/> Règles de pare-feu sur les ordinateurs protégés doivent autoriser les serveurs cibles tooreach hello configuration et le maître dans Azure.p ><p>Vous aurez besoin d’un compte d’administrateur de tooprovide (doit être d’un administrateur local sur l’ordinateur de Windows hello) toopush installer hello Service mobilité sur les serveurs Windows. Si le compte de hello fourni est un compte de domaine, vous devez toodisable contrôle des accès utilisateur à distance sur l’ordinateur local de hello. toodo cette entrée de Registre LocalAccountTokenFilterPolicy DWORD avec une valeur de 1 sous HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System de hello ajouter. entrée de Registre tooadd hello à partir d’une interface CLI ouvrez cmd ou powershell, puis entrez  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** . [En savoir plus](https://msdn.microsoft.com/library/aa826699.aspx) sur le contrôle d’accès.<br/><br/> Après un basculement, si vous voulez vous connecter des machines virtuelles tooWindows Azure avec le Bureau à distance Assurez-vous que le Bureau à distance est activé pour l’ordinateur local, hello. Si vous vous connectez pas via le VPN, les règles de pare-feu doivent autoriser les connexions Bureau à distance sur hello internet. | |
| **Ordinateurs Linux** |Un système d’exploitation pris en charge 64 bits : **Centos 6.4, 6.5, 6.6**; **Oracle Enterprise Linux versions 6.4 et 6.5 exécutant noyau compatible de Red Hat hello ou insécable Enterprise noyau version 3 (UEK3)**, **SUSE Linux Enterprise Server 11 SP3**.<br/><br/> Règles de pare-feu sur les ordinateurs protégés doivent permettre leur configuration de hello tooreach et serveurs cibles maîtres dans Azure.<br/><br/> fichiers/etc/hosts sur les ordinateurs protégés doivent contenir des entrées qui mappent des adresses de tooIP du nom d’hôte local hello associés à toutes les cartes réseau <br/><br/> Si vous souhaitez tooconnect tooan Azure virtual machine Linux en cours d’exécution après basculement à l’aide d’un Secure Shell client (ssh), vérifiez que hello service Secure Shell sur hello protégé machine est toostart automatiquement au démarrage du système et qui permettent de règles de pare-feu une ssh tooit de connexion.<br/><br/> nom d’hôte Hello, des points de montage, noms de périphériques et chemins d’accès de système de Linux et les noms de fichiers (par exemple, / etc / ; /usr) doivent être en anglais uniquement.<br/><br/> Protection peut être activée pour les machines locales avec hello après stockage :-<br>Système de fichiers : EXT3, ETX4, ReiserFS, XFS<br>Logiciel multichemin : Device Mapper (multichemin)<br>Gestionnaire de volume : LVM2<br>Les serveurs physiques avec stockage de contrôleur HP CCISS ne sont pas pris en charge. | |
| **Tiers** |Certains composants de déploiement dans ce scénario dépendent des logiciels tiers toofunction correctement. Pour obtenir la liste complète, consultez la rubrique [Informations et remarques relatives aux logiciels tiers](#third-party) | |

### <a name="network-connectivity"></a>Connectivité réseau
Vous avez deux options lors de la configuration de la connectivité réseau entre votre site local et hello réseau virtuel Azure sur le hello les composants d’infrastructure (serveur de configuration, les serveurs cibles maîtres) sont déployés. Vous devez toodecide le toouse d’option de connectivité réseau avant que vous pouvez déployer votre serveur de configuration. Vous devez toochoose ce paramètre au moment de hello du déploiement. Ce ne sera pas possible ultérieurement.

**Internet :** Communication et la réplication des données entre hello sur des serveurs locaux (serveur de processus, des ordinateurs protégés) et les serveurs (serveur de configuration, un serveur cible maître) de composants d’infrastructure Azure hello se produit sur une sécurisé SSL / Connexion TLS à partir de points de terminaison locaux toohello publics sur les serveurs de cibles de configuration et le maître hello. (la seule exception de hello est connexion hello entre le serveur de processus hello et le serveur cible maître de hello sur le port TCP 9080 n’est pas chiffré. Les informations de contrôle uniquement relatives toohello protocole pour la configuration de réplication est échangée sur cette connexion.)

![Diagramme de déploiement Internet](./media/site-recovery-vmware-to-azure-classic-legacy/internet-deployment.png)

**VPN**: Communication et la réplication des données entre hello sur des serveurs locaux (serveur de processus, des ordinateurs protégés) et les serveurs (serveur de configuration, un serveur cible maître) de composants d’infrastructure Azure hello se produit sur une connexion VPN entre votre réseau local et le hello Azure réseau virtuel sur le hello serveur de configuration et serveurs cibles maîtres sont déployés. Assurez-vous que votre réseau local est connecté toohello réseau virtuel Azure par une connexion ExpressRoute ou d’une connexion VPN site à site.

![Diagramme de déploiement VPN](./media/site-recovery-vmware-to-azure-classic-legacy/vpn-deployment.png)

## <a name="step-1-create-a-vault"></a>Étape 1 : Créer un coffre
1. Connectez-vous à toohello [portail de gestion](https://portal.azure.com).
2. Développez **Data Services** > **Recovery Services**, puis cliquez sur **Coffre Site Recovery**.
3. Cliquez sur **Créer nouveau** > **Création rapide**.
4. Dans **nom**, entrez un coffre de hello tooidentify nom convivial.
5. Dans **région**, sélectionnez hello région géographique pour le coffre hello. les régions toocheck pris en charge consultez disponibilité géographique dans [détails de la tarification de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)
6. Cliquez sur **Create vault**.

    ![Nouveau coffre](./media/site-recovery-vmware-to-azure-classic-legacy/quick-start-create-vault.png)

Vérifiez tooconfirm de barre d’état hello qui hello coffre a été créé avec succès. Hello est répertorié en tant que **Active** sur hello principal **Services de récupération** page.

## <a name="step-2-deploy-a-configuration-server"></a>Étape 2 : déployer un serveur de configuration
### <a name="configure-server-settings"></a>Configurez les paramètres du serveur
1. Bonjour **Services de récupération** , cliquez sur la page de démarrage rapide de hello coffre tooopen hello. Démarrage rapide peut également être ouvert à tout moment à l’aide d’icône de hello.

    ![Icône Quick Start](./media/site-recovery-vmware-to-azure-classic-legacy/quick-start-icon.png)
2. Dans la liste déroulante de hello, sélectionnez **entre un site local avec des serveurs VMware/physiques et Azure**.
3. Dans **Préparer les ressources (Azure) cibles**, cliquez sur **Déployer un serveur de configuration**.

    ![Déployer un serveur de configuration](./media/site-recovery-vmware-to-azure-classic-legacy/deploy-cs2.png)
4. Dans **Détails du nouveau serveur de configuration** , spécifiez :

   * Nom de tooit tooconnect hello configuration serveur et les informations d’identification.
   * Dans le type de connectivité réseau hello liste déroulante Sélectionnez **Internet Public** ou **VPN**. Vous ne pouvez pas modifier ce paramètre une fois qu’il est appliqué.
   * Sélectionnez hello réseau Azure sur le hello server doit être situé. Si vous utilisez VPN Assurez-vous que hello réseau Azure n’est connecté tooyour sur réseau local comme prévu.
   * Spécifiez l’adresse IP interne hello et un sous-réseau qui sera assigné toohello server. Notez que les quatre premières adresses IP dans n’importe quel sous-réseau de hello sont réservés pour un usage interne Azure. Utilisez une autre adresse IP disponible.

     ![Déployer un serveur de configuration](./media/site-recovery-vmware-to-azure-classic-legacy/cs-details.png)
5. Lorsque vous cliquez sur **OK** un ordinateur de virtuel A3 standard basé sur une image de la galerie Azure Site Recovery Windows Server 2012 R2 sera créé dans votre abonnement pour le serveur de configuration de hello. Il est créé en tant que hello première instance d’un nouveau service cloud. Si vous avez sélectionné tooconnect sur le service de cloud hello hello internet est créé avec une adresse IP publique réservée. Vous pouvez surveiller la progression dans hello **travaux** onglet.

    ![Surveiller la progression](./media/site-recovery-vmware-to-azure-classic-legacy/monitor-cs.png)
6. Si vous vous connectez sur hello internet, une fois serveur de configuration hello Remarque déployé hello publique IP adresse affectée tooit sur hello **virtuels** page Bonjour portail Azure. Puis sur hello **points de terminaison** onglet Remarque hello publiques HTTPS port mappé tooprivate le port 443. Vous aurez besoin ultérieurement lorsque vous inscrivez le serveur cible maître hello et serveurs de processus avec le serveur de configuration hello. serveur de configuration Hello est déployé avec ces points de terminaison :

   * HTTPS : Un port public est utilisé toocoordinate la communication entre les serveurs des composants et Azure via hello internet. Port privé 443 est toocoordinate utilisé la communication entre les serveurs des composants et Azure via le VPN.
   * Custom : Un port public est utilisé pour la communication d’outil de la restauration automatique sur hello internet. Le port privé 9443 est utilisé pour la communication des outils de restauration automatique via VPN.
   * PowerShell : port privé 5986
   * Bureau à distance : port privé 3389

   ![Points de terminaison de MV](./media/site-recovery-vmware-to-azure-classic-legacy/vm-endpoints.png)

   > [!WARNING]
   > Ne pas supprimer ou modifier le numéro de port public ou privé hello des points de terminaison créé au cours du déploiement de serveur de configuration.
   >
   >

serveur de configuration Hello est déployé dans un service cloud Azure créé automatiquement avec une adresse IP réservée. adresse réservée Hello est tooensure nécessaire qui hello l’adresse IP du service cloud configuration serveur reste hello même entre les redémarrages de hello virtuels (y compris le serveur de configuration hello) sur le service de cloud computing hello. Hello des adresses IP publiques réservées devez toobe manuellement sans réservation lorsque serveur de configuration hello est désactivé ou il allez restent réservé. Il existe une limite par défaut de 20 adresses IP publiques réservées par abonnement. [En savoir plus](../virtual-network/virtual-networks-reserved-private-ip.md) sur les adresses IP réservées.

### <a name="register-hello-configuration-server-in-hello-vault"></a>Inscrire le serveur de configuration hello dans le coffre de hello
1. Bonjour **Quick Start** page, cliquez sur **préparer les ressources cibles** > **télécharger une clé d’inscription**. fichier de clé Hello est généré automatiquement. Il est valide pendant cinq jours après sa création. Copier le serveur de configuration toohello.
2. Dans **virtuels** serveur de configuration hello select à partir de la liste des ordinateurs virtuels hello. Ouvrez hello **tableau de bord** onglet et cliquez sur **connexion**. **Ouvrez** hello téléchargé toolog du fichier RDP sur le serveur de configuration hello à l’aide du Bureau à distance. Si vous utilisez un VPN, utilisez hello interne adresse IP (hello vous avez spécifié lorsque vous avez déployé le serveur de configuration hello) pour une connexion Bureau à distance à partir du site local de hello. Hello Assistant Installation de Azure Site Recovery Configuration serveur s’exécute automatiquement lorsque vous connectez pour hello première fois.

    ![Inscription](./media/site-recovery-vmware-to-azure-classic-legacy/splash.png)
3. Dans **Installation de logiciels tiers** cliquez sur **J’accepte** toodownload et installer MySQL.

    ![Installation de MySQL](./media/site-recovery-vmware-to-azure-classic-legacy/sql-eula.png)
4. Dans **détails du serveur MySQL** créer toolog des informations d’identification sur l’instance de serveur MySQL hello.

    ![Informations d'identification de MySQL](./media/site-recovery-vmware-to-azure-classic-legacy/sql-password.png)
5. Dans **paramètres Internet** spécifiez comment le serveur de configuration hello vont se connecter toohello internet. Notez les points suivants :

   * Si vous voulez toouse un proxy personnalisé vous devez installez-le avant d’installer le fournisseur de hello.
   * Lorsque vous cliquez sur **suivant** un test s’exécutera la connexion au proxy toocheck hello.
   * Si vous utilisez un proxy personnalisé, ou votre proxy par défaut nécessite une authentification, vous devez tooenter hello proxy plus d’informations, y compris les informations d’identification, le port et adresse de hello.
   * Hello URL suivantes doit être accessible via le proxy hello :
     * *.hypervrecoverymanager.windowsazure.com
     * *.accesscontrol.windows.net
     * *.backup.windowsazure.com
     * *.blob.core.windows.net
     * *.store.core.windows.net
   * Si vous avez basé sur l’adresse IP des règles de pare-feu s’assurer que les règles de hello sont définies communication tooallow à partir d’adresses IP hello configuration serveur toohello décrites dans [plages d’adresses IP Azure Datacenter](https://msdn.microsoft.com/library/azure/dn175718.aspx) et le protocole HTTPS (443). Vous devriez toowhite-liste des plages IP de hello région Azure que vous envisagez de toouse et l’ouest des États-Unis.

     ![Inscription de proxy](./media/site-recovery-vmware-to-azure-classic-legacy/register-proxy.png)
6. Dans **paramètres de localisation de Message d’erreur fournisseur** spécifier la langue dans laquelle vous souhaitez tooappear de messages d’erreur.

    ![Inscription de message d’erreur](./media/site-recovery-vmware-to-azure-classic-legacy/register-locale.png)
7. Dans **Azure Site Recovery inscription** Parcourir et fichier de clé de hello sélectionnez vous avez copié toohello server.

    ![Inscription de fichier de clé](./media/site-recovery-vmware-to-azure-classic-legacy/register-vault.png)
8. À la fin de hello page d’Assistant de hello sélectionner ces options :

   * Sélectionnez **lancer de boîte de dialogue compte de gestion** toospecify qui hello boîte de dialogue Gérer les comptes doit ouvrir une fois que vous avez terminé l’Assistant de hello.
   * Sélectionnez **créer une icône de bureau pour Cspsconfigtool** tooadd un raccourci du bureau sur le serveur de configuration hello afin que vous puissiez ouvrir hello **gérer les comptes** boîte de dialogue à tout moment sans avoir besoin de toorerun hello Assistant.

     ![Terminer l’inscription](./media/site-recovery-vmware-to-azure-classic-legacy/register-final.png)
9. Cliquez sur **Terminer** Assistant de hello toocomplete. Une phrase secrète est générée. Copier tooa les emplacement sécurisé. Vous avez besoin de tooauthenticate et inscrire les processus hello et serveurs cibles maîtres avec le serveur de configuration hello. Il a également utilisé l’intégrité du canal tooensure dans les communications de serveur de configuration. Vous pouvez régénérer hello le mot de passe, mais vous devez serveur cible maître dans le Registre toore hello et serveurs de processus à l’aide de hello nouvelle phrase secrète.

    ![Phrase secrète](./media/site-recovery-vmware-to-azure-classic-legacy/passphrase.png)

Après l’inscription, serveur de configuration hello s’afficheront sur hello **serveurs de Configuration** page dans le coffre hello.

### <a name="set-up-and-manage-accounts"></a>Configurer et gérer des comptes
Au cours du déploiement récupération de Site demande les informations d’identification pour hello suivant des actions :

* Un compte VMware afin que Site Recovery puisse découvrir automatiquement les machines virtuelles sur les serveurs vCenter ou les hôtes vSphere.
* Lorsque vous ajoutez des ordinateurs pour la protection, afin que la récupération de Site peut installer le service de mobilité hello sur ces derniers.

Une fois que vous avez enregistré le serveur de configuration hello, vous pouvez ouvrir hello **gérer les comptes** tooadd de la boîte de dialogue et gérer les comptes qui doivent être utilisées pour ces actions. Il existe deux façons toodo cela :

* Ouvrez le raccourci hello vous avez choisi toocreated boîte de dialogue hello sur hello dernière page du programme d’installation pour le serveur de configuration hello (cspsconfigtool).
* Boîte de dialogue Ouvrir hello sur fin du programme d’installation du serveur de configuration.

1. Sous **Gérer les comptes** click **Ajouter un compte**. Vous pouvez également modifier et supprimer des comptes existants.

    ![Gérer les comptes](./media/site-recovery-vmware-to-azure-classic-legacy/manage-account.png)
2. Dans **détails du compte** spécifier une toouse de nom de compte dans Azure et les informations d’identification (domaine/nom d’utilisateur).

    ![Gérer les comptes](./media/site-recovery-vmware-to-azure-classic-legacy/account-details.png)

### <a name="connect-toohello-configuration-server"></a>Connecter le serveur de configuration toohello
Il n’y a deux façons tooconnect toohello configuration serveur :

* Via une connexion VPN de site à site ou ExpressRoute
* Sur hello internet

Notez les points suivants :

* Une connexion internet utilise des points de terminaison hello de machine virtuelle de hello en conjonction avec hello adresse IP virtuelle publique du serveur de hello.
* Une connexion VPN utilise hello adresse IP interne du serveur de hello ainsi que des ports privés du point de terminaison hello.
* Il est une décision unique de toodecide si tooconnect (contrôle et la réplication de données) à partir de votre toohello de serveurs locaux divers composants serveur (serveur de configuration, un serveur cible maître) s’exécutant dans Azure via une connexion VPN ou hello internet. Vous ne pouvez pas modifier ce paramètre par la suite. Si vous le faites vous aurez besoin tooredeploy hello scénario et rétablissez vos ordinateurs.  

## <a name="step-3-deploy-hello-master-target-server"></a>Étape 3 : Déployer le serveur cible maître de hello
1. Cliquez sur **Préparer des ressources cibles (Azure)** > **Déployer le serveur cible maître**.
2. Spécifiez les informations d’identification et les détails du serveur cible maître hello. serveur de Hello sera déployé dans hello même réseau Azure en tant que serveur de configuration hello. Lorsque vous cliquez sur toocomplete une machine virtuelle Azure sera créée avec une image de la galerie Windows ou Linux.

    ![Paramètres du serveur cible](./media/site-recovery-vmware-to-azure-classic-legacy/target-details.png)

Notez que les quatre premières adresses IP dans n’importe quel sous-réseau de hello sont réservés pour un usage interne Azure. Indiquez une autre adresse IP disponible.

> [!NOTE]
> Sélectionnez DS4 Standard lors de la configuration de protection pour les charges de travail nécessitant de hautes performances d’e/s et une faible latence dans l’ordre toohost d’e/s intensives les charges de travail à l’aide de [compte de stockage Premium](../storage/common/storage-premium-storage.md).
>
>

1. Une machine virtuelle de serveur cible maître Windows est créée avec les points de terminaison suivants : Notez que les points de terminaison publics sont créées uniquement si votre connexion via hello internet.

   * Personnalisé : De port Public utilisé par les données de réplication hello processus serveur toosend sur hello internet. Port privé 9443 est utilisé par serveur cible maître de toohello données réplication hello processus serveur toosend via le VPN.
   * Custom1 : Port Public utilisé par les métadonnées toosend du serveur de processus hello sur hello internet. Port privé 9080 est utilisé par le serveur cible maître de hello processus serveur toosend métadonnées toohello via le VPN.
   * PowerShell : port privé 5986
   * Bureau à distance : port privé 3389
2. Une machine virtuelle de serveur cible maître Linux est créée avec les points de terminaison suivants. Notez que les points de terminaison publics sont créées uniquement si vous vous connectez sur hello internet.

   * Personnalisé : De port Public utilisé par les données de réplication de processus serveur toosend sur hello internet. Port privé 9443 est utilisé par serveur cible maître de toohello données réplication hello processus serveur toosend via le VPN.
   * Custom1 : Port Public est utilisé par les métadonnées toosend du serveur de processus hello sur hello internet. Port privé 9080 est utilisé par le serveur cible maître de hello processus serveur toosend métadonnées toohello via le VPN
   * SSH : port privé 22

     > [!WARNING]
     > Ne pas supprimer ou modifier le numéro de port public ou privé hello d’un des points de terminaison hello créés au cours du déploiement de serveur cible maître hello.
     >
     >
3. Dans **virtuels** attendre toostart de machine virtuelle hello.

   * S’il s’agit d’une note de serveur Windows vers le bas des détails du Bureau à distance hello.
   * S’il s’agit d’un serveur Linux, et vous vous connectez via VPN Remarque hello adresse IP interne de l’ordinateur virtuel de hello. Si vous vous connectez sur hello internet Remarque hello adresse IP publique.
4. Ouvrez une session sur l’installation du serveur de toocomplete hello et l’inscrire avec le serveur de configuration hello.
5. Si vous exécutez Windows :

   1. Lancer une machine virtuelle de toohello connexion Bureau à distance. Hello première fois que vous ouvrez une session sur un script s’exécute dans une fenêtre PowerShell. Ne la fermez pas. Quand il termine outil de configuration de l’Agent hôte hello s’ouvre automatiquement serveur hello de tooregister.
   2. Dans **Config de l’Agent hôte** spécifier hello adresse IP interne du serveur de configuration hello et le port 443. Vous pouvez utiliser l’adresse interne hello et port privé 443 même si vous vous connectez pas via le VPN étant hello virtual machine toohello attaché même réseau Azure en tant que serveur de configuration hello. Laissez l'option **Utiliser HTTPS** activée. Entrez la phrase secrète de hello pour le serveur de configuration hello que vous avez notée précédemment. Cliquez sur **OK** serveur hello de tooregister. Vous pouvez ignorer les options de NAT hello. Elles ne sont pas utilisées.
   3. Si vos besoins de lecteur de rétention estimé est plus de 1 To, vous pouvez configurer volume de rétention hello (r) à l’aide d’un disque virtuel et [des espaces de stockage](http://blogs.technet.com/b/askpfeplat/archive/2013/10/21/storage-spaces-how-to-configure-storage-tiers-with-windows-server-2012-r2.aspx)

   ![Serveur cible maître Windows](./media/site-recovery-vmware-to-azure-classic-legacy/target-register.png)
6. Si vous exécutez Linux :

   1. Assurez-vous que vous avez installé hello derniers Services d’intégration Linux (LIS) installé avant d’installer le serveur cible maître de hello. Vous trouverez la version la plus récente hello de LIS ainsi que les instructions sur la façon de tooinstall [ici](https://www.microsoft.com/download/details.aspx?id=46842). Redémarrez l’ordinateur de hello après hello LIS installé.
   2. Dans **Préparer des ressources cibles (Azure)**, cliquez sur **Télécharger et installer un logiciel supplémentaire (uniquement pour le serveur cible maître Linux)**. Hello de copie téléchargé tar fichier toohello virtual machine à l’aide d’un client sftp. Ou bien vous pouvez ouvrir une session sur le serveur cible maître de linux déployés toohello et utiliser *wget http://go.microsoft.com/fwlink/?LinkID=529757&clcid=0x409* fichier de hello toodownload hello.
   3. Ouvrez une session sur le serveur toohello à l’aide d’un client Secure Shell. Si vous êtes connecté toohello réseau Azure via le VPN utiliser l’adresse IP interne hello. Sinon, utiliser une adresse IP externe hello et le point de terminaison public hello SSH.
   4. Extraire des fichiers de hello du programme d’installation de gzippé hello en exécutant : **tar – xvzf Microsoft-ASR_UA_8.4.0.0_RHEL6-64***
      ![serveur cible maître de Linux](./media/site-recovery-vmware-to-azure-classic-legacy/linux-tar.png)
   5. Vérifiez que vous êtes dans hello Active toowhich vous avez extrait le contenu hello du fichier d’archive tar hello.
   6. Copie hello configuration serveur phrase secrète tooa fichier local à l’aide de la commande hello **echo  *`<passphrase>`*  > passphrase.txt**
   7. Exécuter la commande hello »**sudo. /Install t - les deux - a -R héberger MasterTarget des /usr/local/ASR -d -i  *`<Configuration server internal IP address>`*  -p 443 s - y - c https -P passphrase.txt**».

      ![Inscrire un serveur cible](./media/site-recovery-vmware-to-azure-classic-legacy/linux-mt-install.png)
7. Attendez quelques minutes (10-15) et sur la vérification de page hello que le serveur cible maître hello est répertorié comme enregistré dans **serveurs** > **serveurs de Configuration** **Détailsduserveur** onglet. Si vous exécutez Linux, et il n’a pas inscrit exécuter hello hôte outil de configuration à nouveau à partir de /usr/local/ASR/Vx/bin/hostconfigcli. Vous aurez besoin des autorisations d’accès tooset en exécutant chmod en tant que racine.

    ![Vérifier le serveur cible](./media/site-recovery-vmware-to-azure-classic-legacy/target-server-list.png)

> [!NOTE]
> Elle peut prendre too15 minutes après que l’inscription est terminée pour toobe de serveur cible maître hello répertorié dans le portail de hello. tooupdate immédiatement, cliquez sur **Actualiser** sur hello **serveurs de Configuration** page.
>
>

## <a name="step-4-deploy-hello-on-premises-process-server"></a>Étape 4 : Déployer le serveur de traitement local hello
Avant de commencer, nous vous recommandons de configurer une adresse IP statique sur le serveur de processus hello afin qu’il est garanti toobe persistant redémarre à travers.

1. Cliquez sur démarrage rapide > **installer un serveur de traitement local** > **télécharger et installer le serveur de processus hello**.

    ![Installer un serveur de traitement](./media/site-recovery-vmware-to-azure-classic-legacy/ps-deploy.png)
2. Hello de copie téléchargé le serveur de toohello de fichiers zip sur lequel vous allez le serveur de processus tooinstall hello. fichier zip de Hello contient deux fichiers d’installation :

   * Microsoft-ASR_CX_TP_8.4.0.0_Windows*
   * Microsoft-ASR_CX_8.4.0.0_Windows*
3. Décompressez hello archive et copie hello fichiers tooa emplacement d’installation sur le serveur de hello.
4. Exécutez hello **Microsoft-ASR_CX_TP_8.4.0.0_Windows*** fichier d’installation et suivez hello instructions. Cette commande installe les composants tiers nécessaires pour le déploiement de hello.
5. Puis exécutez **Microsoft-ASR_CX_8.4.0.0_Windows***.
6. Sur hello **Mode serveur** page Sélectionnez **serveur de processus**.
7. Sur hello **détails de l’environnement** page hello suivant :

    - Si vous souhaitez que le clic de machines virtuelles VMware tooprotect **Oui**
    - Si vous souhaitez uniquement les serveurs physiques de tooprotect et que vous ne devez donc vCLI VMware installé sur le serveur de processus hello. Cliquez sur **Non** et continuez.

1. Notez les points suivants de hello lors de l’installation vCLI de VMware :

   * **Seule la version VMware vSphere CLI 5.5.0 est prise en charge**. serveur de processus Hello ne fonctionne pas avec d’autres versions ou les mises à jour de vSphere CLI.
   * Téléchargez vSphere CLI 5.5.0 [ici.](https://my.vmware.com/web/vmware/details?downloadGroup=VCLI550&productId=352)
   * Si vous avez installé vSphere CLI juste avant que vous avez démarré l’installation du serveur de processus hello et il ne détecte pas le programme d’installation, attendre des toofive minutes avant d’essayer à nouveau le programme d’installation. Cela garantit que toutes les variables d’environnement hello nécessitent pour la détection de vSphere CLI ont été correctement initialisées.
2. Dans **sélection de carte réseau pour le serveur de processus** carte réseau de hello Sélectionnez ce serveur de processus hello doit utiliser.

   ![Sélectionner une carte](./media/site-recovery-vmware-to-azure-classic-legacy/ps-nic.png)
3. Dans **Détails du serveur de configuration**:

   * Pour l’adresse IP de hello et le port, si vous vous connectez via le VPN spécifiez hello adresse IP interne du serveur de configuration hello et 443 pour le port de hello. Sinon, spécifier l’adresse IP virtuelle publique hello et mappé point de terminaison HTTP public.
   * Tapez la phrase secrète de hello hello du serveur de configuration.
   * Désactivez **signature de logiciel de service de mobilité de vérifier** si vous souhaitez toodisable vérification lorsque vous utilisez le service de push automatique tooinstall hello. Vérification de la signature a besoin de connectivité internet hello du serveur de processus.
   * Cliquez sur **Suivant**.

   ![Inscrire un serveur de configuration](./media/site-recovery-vmware-to-azure-classic-legacy/ps-cs.png)
4. Dans **Sélectionner le lecteur d'Installation** , sélectionnez un lecteur de cache. serveur de processus Hello a besoin d’un lecteur de cache au moins 600 Go d’espace libre. Cliquez ensuite sur **Installer**.

   ![Inscrire un serveur de configuration](./media/site-recovery-vmware-to-azure-classic-legacy/ps-cache.png)
5. Notez que vous devrez peut-être l’installation hello toocomplete toorestart hello server. Dans **serveur de Configuration** > **détails du serveur** vérifier ce serveur de processus hello apparaît et est enregistré avec succès dans le coffre hello.

> [!NOTE]
> Il peut prendre jusqu'à too15 minutes après que l’inscription est terminée pour hello processus serveur tooappear sous le serveur de configuration hello. tooupdate actualiser immédiatement, le serveur de configuration hello en cliquant sur le bouton d’actualisation hello bas hello page hello du serveur de configuration
>
>

![Valider un serveur de traitement](./media/site-recovery-vmware-to-azure-classic-legacy/ps-register.png)

Si vous n’avez pas désactiver la vérification de signature pour service de mobilité hello lorsque vous avez inscrit le serveur de processus hello vous pouvez le faire ultérieurement comme suit :

1. Ouvrez une session sur le serveur de processus hello en tant qu’administrateur, puis ouvrez le fichier de hello C:\pushinstallsvc\pushinstaller.conf pour la modification. Section hello **[PushInstaller.transport]** ajoutez cette ligne : **SignatureVerificationChecks = « 0 »**. Enregistrez et fermez le fichier de hello.
2. Redémarrez hello InMage PushInstall service.

## <a name="step-5-update-site-recovery-components"></a>Étape 5 : Mettre à jour les composants de Site Recovery
Les composants de récupération de site sont mis à jour à partir de tootime de temps. Lorsque de nouvelles mises à jour sont disponibles, vous devez les installer dans hello suivant l’ordre :

1. Serveur de configuration
2. Serveur de traitement
3. Serveur cible maître
4. Outil de restauration automatique (vContinuum)

### <a name="obtain-and-install-hello-updates"></a>Obtenir et installer les mises à jour hello
1. Vous pouvez obtenir les mises à jour pour la configuration de hello, les processus et les serveurs cibles maîtres de hello Site Recovery **tableau de bord**. Pour l’installation de Linux extraire les fichiers de hello du programme d’installation de gzippé hello et exécuter la commande hello « sudo. / installer des « mise à jour de tooinstall hello.
2. [Télécharger](http://go.microsoft.com/fwlink/?LinkID=533813) hello dernière mise à jour tool(vContinuum) de la restauration automatique hello.
3. Si vous exécutez des ordinateurs virtuels ou des serveurs physiques qui déjà hello mobilité service sont installé, vous pouvez obtenir les mises à jour pour le service de hello comme suit :

   * **Option 1**: télécharger les mises à jour :
     * [Windows Server (64 bits uniquement)](http://download.microsoft.com/download/8/4/8/8487F25A-E7D9-4810-99E4-6C18DF13A6D3/Microsoft-ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe)
     * [CentOS 6.4,6.5,6.6 (64 bits uniquement)](http://download.microsoft.com/download/7/E/D/7ED50614-1FE1-41F8-B4D2-25D73F623E9B/Microsoft-ASR_UA_8.4.0.0_RHEL6-64_GA_28Jul2015_release.tar.gz)
     * [Oracle Enterprise Linux 6.4,6.5 (64 bits uniquement)](http://download.microsoft.com/download/5/2/6/526AFE4B-7280-4DC6-B10B-BA3FD18B8091/Microsoft-ASR_UA_8.4.0.0_OL6-64_GA_28Jul2015_release.tar.gz)
     * [SUSE Linux Enterprise Server SP3 (64 bits uniquement)](http://download.microsoft.com/download/B/4/2/B4229162-C25C-4DB2-AD40-D0AE90F92305/Microsoft-ASR_UA_8.4.0.0_SLES11-SP3-64_GA_28Jul2015_release.tar.gz)
     * Après la mise à jour des messages hello du processus serveur hello version mise à jour du service mobilité de hello sera disponible dans dossier de C:\pushinstallsvc\repository hello sur le serveur de processus hello.
   * **Option 2**: Si vous avez un ordinateur avec une version antérieure de hello service mobilité est installé, vous pouvez automatiquement mettre à niveau service de mobilité hello sur l’ordinateur de hello à partir du portail de gestion hello.

     1. Assurez-vous que ce serveur de processus hello est mise à jour.
     2. Assurez-vous que l’ordinateur protégé hello est conforme à hello [conditions préalables](#install-the-mobility-service-automatically) pour diffuser automatiquement le service de mobilité hello, afin que la mise à jour hello fonctionne comme prévu.
     3. Groupe de protection de hello SELECT, mettez en surbrillance hello protégé machine, puis cliquez sur **service mobilité de la mise à jour**. Ce bouton est disponible uniquement si une version plus récente de hello service mobilité.

         ![Sélectionnez un serveur vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/update-mobility.png)

Dans Sélectionnez les comptes spécifier hello administrateur compte toobe utilisé tooupdate hello mobilité service sur le serveur de hello protégé. Cliquez sur OK et attendre hello déclenchée travail toocomplete.

## <a name="step-6-add-vcenter-servers-or-vsphere-hosts"></a>Étape 6 : Ajouter des serveurs vCenter ou des hôtes vSphere
1. Cliquez sur **serveurs** > **serveurs de Configuration** > serveur de configuration >**ajouter le serveur vCenter** tooadd un hôte de serveur ou vSphere vCenter.

    ![Sélectionnez un serveur vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter.png)
2. Spécifier les détails de hello serveur ou ordinateur hôte et sélectionnez hello processus qui sera utilisé toodiscover il.

   * Si le serveur vCenter hello n’est pas en cours d’exécution sur le port 443 par défaut de hello spécifier le numéro de port de hello sur quel hello serveur vCenter est en cours d’exécution.
   * serveur de processus Hello doit être sur hello même réseau que hello vCenter serveur/hôte vSphere et doit avoir un VMware vSphere CLI 5.5.0 installé.

     ![Paramètres du serveur vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter4.png)
3. Après que la découverte se termine le serveur vCenter hello est répertorié sous Détails hello du serveur de configuration.

    ![Paramètres du serveur vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter2.png)
4. Si vous utilisez un ordinateur hôte ou le serveur de compte non administrateur tooadd hello, vérifiez que le compte de hello comporte hello suivant des privilèges :

   * Les privilèges Centre de données, Magasin de données, Dossier, Hôte, Réseau, Ressource, Stockage, Ordinateur virtuel et vSphere Distributed Switch doivent être activés pour les comptes vCenter.
   * comptes d’ordinateur hôte vSphere doivent avoir hello Datacenter, la banque de données, dossier, hôte, réseau, ressources, machine virtuelle et les privilèges de commutateur de Distributed vSphere activés

## <a name="step-7-create-a-protection-group"></a>Étape 7 : créer un groupe de protection
1. Ouvrez **Éléments protégés** > **Groupe de protection** > **Créer un groupe de protection**.

    ![Créer un groupe de protection](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg1.png)
2. Sur hello **spécifier les paramètres de groupe de Protection** page spécifier un nom pour le groupe de hello et le serveur de configuration de sélection hello sur lequel vous souhaitez que toocreate hello groupe.

    ![Paramètres du groupe de protection](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg2.png)
3. Sur hello **spécifier les paramètres de réplication** page Configurer les paramètres de réplication hello qui seront utilisés pour toutes les machines hello dans le groupe de hello.

    ![Réplication du groupe de protection](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg3.png)
4. Paramètres :

   * **Cohérence de multiples VM**: Si vous activez cette option sur elle crée des points de récupération cohérents avec les applications partagées sur plusieurs ordinateurs hello dans le groupe de protection hello. Ce paramètre est particulièrement importante lorsque toutes les machines de hello du groupe de protection hello exécutent hello la même charge de travail. Tous les ordinateurs seront récupérée toohello même point de données. Disponible uniquement pour les serveurs Windows.
   * **Seuil RPO**: alerte ne sera générée lors de la réplication de protection continue des données hello RPO dépasse la valeur de seuil RPO hello configuré.
   * **Rétention du point de récupération**: Spécifie la période de conservation hello. Les ordinateurs protégés peuvent être récupérées point tooany dans cette fenêtre.
   * **Fréquence des instantanés cohérents au niveau des applications**: spécifie la fréquence de création des points de récupération contenant des instantanés cohérents au niveau des applications.

Vous pouvez surveiller le groupe de protection hello comme elles sont créées sur hello **éléments protégés** page.

## <a name="step-8-set-up-machines-you-want-tooprotect"></a>Étape 8 : Configurer des ordinateurs vous voulez tooprotect
Vous devez tooinstall hello service mobilité sur les ordinateurs virtuels et les serveurs physiques que vous souhaitez tooprotect. Il existe deux méthodes pour le faire :

* Push et d’installer automatiquement le service de hello sur chaque ordinateur hello du serveur de processus.
* Installer manuellement le service de hello.

### <a name="install-hello-mobility-service-automatically"></a>Installer automatiquement le service de mobilité de hello
Lorsque vous ajoutez des machines tooa protection groupe hello service mobilité est automatiquement envoyée et installé sur chaque ordinateur par le serveur de processus hello.

**Automatiquement push installer le service de mobilité de hello sur les serveurs Windows :**

1. Installez hello plus récentes des mises à jour pour le serveur de processus hello comme décrit dans [étape 5 : installer les dernières mises à jour](#step-5-install-latest-updates)et assurez-vous que ce serveur de processus hello est disponible.
2. Vérifiez la connectivité réseau est entre l’ordinateur source de hello et hello serveur de traitement et cet ordinateur de source hello est accessible à partir du serveur de processus hello.  
3. Configurer tooallow de pare-feu Windows hello **partage de fichiers et imprimantes** et **Windows Management Instrumentation**. Sous paramètres du pare-feu Windows, sélectionnez l’option de hello « Autoriser une application ou une fonctionnalité via le pare-feu », puis sélectionnez les applications hello comme indiqué dans l’image hello ci-dessous. Pour les ordinateurs qui font partie du domaine tooa vous pouvez configurer la stratégie de pare-feu hello avec un objet de stratégie de groupe.

    ![Paramètres du pare-feu](./media/site-recovery-vmware-to-azure-classic-legacy/push-firewall.png)
4. Hello compte utilisé tooperform hello poussée doit être dans le groupe d’administrateurs hello sur l’ordinateur de hello souhaité tooprotect. Ces informations d’identification sont utilisées uniquement pour l’installation push du service mobilité de hello et vous devez lui fournir lorsque vous ajoutez un groupe de protection de machine tooa.
5. Si hello fourni de compte n’est pas un compte de domaine, vous devez toodisable contrôle des accès utilisateur à distance sur l’ordinateur local de hello. toodo cette entrée de Registre LocalAccountTokenFilterPolicy DWORD avec une valeur de 1 sous HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System de hello ajouter. entrée de Registre tooadd hello à partir d’une interface CLI ouvrez cmd ou powershell, puis entrez  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** .

**Automatiquement push installer le service de mobilité de hello sur des serveurs Linux :**

1. Installez hello plus récentes des mises à jour pour le serveur de processus hello comme décrit dans [étape 5 : installer les dernières mises à jour](#step-5-install-latest-updates)et assurez-vous que ce serveur de processus hello est disponible.
2. Vérifiez la connectivité réseau est entre l’ordinateur source de hello et hello serveur de traitement et cet ordinateur de source hello est accessible à partir du serveur de processus hello.  
3. Assurez-vous que le compte de hello est un utilisateur racine sur le serveur de Linux hello source.
4. Vérifiez que ce fichier/etc/hosts de hello sur la source de hello Linux server contient des entrées qui mappent des adresses de tooIP du nom d’hôte local hello associés à toutes les cartes réseau.
5. Installer openssh plus récente de hello, openssh-serveur, les packages openssl sur l’ordinateur de hello souhaité tooprotect.
6. Vérifiez que SSH est activé et exécuté sur le port 22.
7. Activer l’authentification dans le fichier de sshd_config hello SFTP sous-système et le mot de passe comme suit :

   * a) Connectez-vous en tant qu’utilisateur racine.
   * (b) dans hello fichier/etc/ssh/fichier sshd_config, rechercher la ligne hello qui commence par **PasswordAuthentication**.
   * c) supprimer les commentaires de ligne de hello et modifiez les valeur hello à partir de « non » trop « Oui ».

       ![Mobilité Linux](./media/site-recovery-vmware-to-azure-classic-legacy/linux-push.png)
   * d) recherche ligne hello qui commence par le sous-système et supprimez les commentaires de la ligne de hello.

       ![Mobilité push de Linux](./media/site-recovery-vmware-to-azure-classic-legacy/linux-push2.png)    
8. Vérifiez le type variant de hello source ordinateur Linux est prise en charge.

### <a name="install-hello-mobility-service-manually"></a>Installer manuellement le service de mobilité de hello
packages de logiciels Hello utilisé tooinstall hello mobilité service se trouvent sur le serveur de traitement hello C:\pushinstallsvc\repository. Ouvrez une session sur le serveur de processus hello et copie hello installation approprié package toohello machine source en fonction de la table hello ci-dessous :-

| Système d’exploitation source | Package de service de mobilité sur le serveur de traitement |
| --- | --- |
| Windows Server (64 bits uniquement) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe` |
| CentOS 6.4, 6.5, 6.6 (64 bits uniquement) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_RHEL6-64_GA_28Jul2015_release.tar.gz` |
| SUSE Linux Enterprise Server 11 SP3 (64 bits uniquement) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_SLES11-SP3-64_GA_28Jul2015_release.tar.gz` |
| Oracle Enterprise Linux 6.4, 6.5 (64 bits uniquement) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_OL6-64_GA_28Jul2015_release.tar.gz` |

**tooinstall hello service mobilité manuellement sur un serveur Windows**, hello suivant :

1. Hello de copie **Microsoft-ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe** package à partir du chemin d’accès du répertoire hello processus serveur répertorié dans la table hello ci-dessus ordinateur de source toohello.
2. Installer le service de mobilité de hello en hello exécutable en cours d’exécution sur l’ordinateur source de hello.
3. Suivez les instructions du programme d’installation hello.
4. Sélectionnez **service mobilité** en tant que rôle de hello et cliquez sur **suivant**.

    ![Installer le service de mobilité](./media/site-recovery-vmware-to-azure-classic-legacy/ms-install.png)
5. Laissez le répertoire d’installation hello en tant que chemin d’installation de hello par défaut et cliquez sur **installer**.
6. Dans **Config de l’Agent hôte** spécifier l’adresse IP de hello et le port HTTPS hello du serveur de configuration.

   * Si vous vous connectez sur hello internet spécifier hello adresse IP virtuelle publique et le point de terminaison HTTPS public en tant que port de hello.
   * Si vous vous connectez via le VPN spécifier l’adresse IP interne hello et 443 pour le port de hello. Laissez l’option **Utiliser HTTPS** cochée.

     ![Installer le service de mobilité](./media/site-recovery-vmware-to-azure-classic-legacy/ms-install2.png)
7. Spécifiez la phrase secrète de hello configuration serveur, cliquez sur **OK** tooregister hello service mobilité avec le serveur de configuration hello.

**toorun à partir de la ligne de commande hello :**

1. Copiez hello le mot de passe à partir hello CX toohello « C:\connection.passphrase » sur le serveur de hello et exécuter cette commande. Dans notre exemple CX i 104.40.75.37 et hello port HTTPS est 62519 :

    `C:\Microsoft-ASR_UA_8.2.0.0_Windows_PREVIEW_20Mar2015_Release.exe" -ip 104.40.75.37 -port 62519 -mode UA /LOG="C:\stdout.txt" /DIR="C:\Program Files (x86)\Microsoft Azure Site Recovery" /VERYSILENT  /SUPPRESSMSGBOXES /norestart  -usesysvolumes  /CommunicationMode https /PassphrasePath "C:\connection.passphrase"`

**Installer manuellement le service de mobilité de hello sur un serveur Linux**:

1. Copiez l’archive tar approprié de hello basé sur la table hello ci-dessus, à partir de l’ordinateur source de hello processus serveur toohello.
2. Ouvrir un programme de l’interpréteur de commandes et extraire hello archive tar archive tooa chemin d’accès local en exécutant`tar -xvzf Microsoft-ASR_UA_8.2.0.0*`
3. Créer un fichier passphrase.txt dans toowhich de répertoire local hello vous avez extrait le contenu hello d’archive tar de hello en entrant  *`echo <passphrase> >passphrase.txt`*  à partir de l’interpréteur de commandes.
4. Installer le service de mobilité hello en entrant  *`sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i <IP address> -p <port> -s y -c https -P passphrase.txt`* .
5. Spécifiez le port et adresse IP de hello :

   * Si vous vous connectez le serveur de configuration toohello sur hello internet spécifier hello configuration serveur virtuel adresse IP publique et point de terminaison HTTPS public dans `<IP address>` et `<port>`.
   * Si vous vous connectez via une connexion VPN spécifiez 443 et l’adresse IP interne de hello.

**toorun à partir de la ligne de commande hello**:

1. Copiez hello le mot de passe à partir hello CX toohello « passphrase.txt » sur le serveur de hello et exécuter cette commande. Dans notre exemple CX i 104.40.75.37 et hello port HTTPS est 62519 :

tooinstall sur un serveur de production :

    ./install -t both -a host -R Agent -d /usr/local/ASR -i 104.40.75.37 -p 62519 -s y -c https -P passphrase.txt

tooinstall sur le serveur cible de hello :

    ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 62519 -s y -c https -P passphrase.txt

> [!NOTE]
> Lorsque vous ajoutez le groupe de protection tooa ordinateurs qui exécutent déjà une version appropriée du service mobilité de hello puis poussée hello est ignorée.
>
>

## <a name="step-9-enable-protection"></a>Étape 9 : activer la protection
protection tooenable vous ajoutez le groupe de protection tooa serveurs physiques et virtuels. Avant de commencer, notez les points suivants :

* Machines virtuelles sont découverts toutes les 15 minutes et peut prendre jusqu'à minutes too15 leur tooappear dans Azure Site Recovery après la découverte.
* Modifications de l’environnement sur l’ordinateur virtuel de hello (par exemple, l’installation des outils VMware) peuvent également prendre too15 minutes toobe est mis à jour en mode de récupération de Site.
* Vous pouvez vérifier hello découverts dernière heure Bonjour **dernier CONTACT à** field pour un hôte de serveur/ESXi vCenter hello sur hello **serveurs de Configuration** page.
* Si vous avez déjà créé un groupe de protection et que vous ajoutez un hôte de serveur ou ESXi vCenter après cela, il prend les quinze minutes pour toorefresh de portail Azure Site Recovery hello et toobe d’ordinateurs virtuels répertoriés dans hello **groupe de protection tooa ajouter les ordinateurs**  boîte de dialogue.
* Si vous souhaitez que tooproceed immédiatement avec l’ajout du groupe de machines tooprotection sans attendre la détection planifiée de hello, mettez en surbrillance le serveur de configuration hello (ne cliquez pas dessus) et cliquez sur hello **Actualiser** bouton.
* Lorsque vous ajoutez des ordinateurs virtuels ou groupe de protection de machines physiques tooa, serveur de processus hello transmet automatiquement et installe le service de mobilité hello sur le serveur de source de hello si hello il n’est pas déjà installé.
* Mécanisme de transmission automatique hello toowork Assurez-vous que vous avez configuré vos ordinateurs protégés comme décrit dans l’étape précédente de hello.

Ajoutez des ordinateurs comme suit :

1. Cliquez sur **Éléments protégés** > **Groupe de protection** > **Machines** > **Ajouter des machines**. Comme meilleure pratique, nous recommandons que les groupes de protection doivent refléter vos charges de travail afin que vous ajoutez des ordinateurs exécutant une application spécifique de toohello même groupe.
2. Dans **sélectionner des Machines virtuelles** si vous protégez des serveurs physiques, Bonjour **ajouter des Machines physiques** Assistant fournir l’adresse IP de hello et le nom convivial. Sélectionnez ensuite la famille du système d’exploitation hello.

    ![Ajouter un serveur V-Center](./media/site-recovery-vmware-to-azure-classic-legacy/physical-protect.png)
3. Dans **sélectionner des Machines virtuelles** si vous protégez des ordinateurs virtuels VMware, sélectionnez un serveur vCenter qui gère vos machines virtuelles (ou l’hôte de EXSi hello sur lequel ils s’exécutent), puis les machines hello.

    ![Ajouter un serveur V-Center](./media/site-recovery-vmware-to-azure-classic-legacy/select-vms.png)    
4. Dans **spécifier les ressources cible** sélectionner les serveurs cible maître hello et toouse de stockage pour la réplication et indiquez si les paramètres de hello doivent être utilisés pour toutes les charges de travail. Sélectionnez [compte de stockage Premium](../storage/common/storage-premium-storage.md) lors de la configuration de la protection pour les charges de travail nécessitant de hautes performances d’e/s et une latence faible dans l’ordre toohost e/s intensives les charges de travail. Si vous voulez toouse un compte de stockage Premium pour les disques de votre charge de travail, vous devez toouse hello cible principale de la série DS. Vous ne pouvez pas utiliser de disques de stockage Premium avec une cible maître qui n’est pas de série DS.

   > [!NOTE]
   > Nous ne prennent pas en charge déplacement hello de comptes de stockage créé à l’aide de hello [nouveau portail Azure](../storage/common/storage-create-storage-account.md) plusieurs groupes de ressources.
   >
   >

    ![Serveur vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/machine-resources.png)
5. Dans **spécifier les comptes** sélectionnez hello compte toouse pour l’installation de service de mobilité hello sur les ordinateurs protégés. informations d’identification du compte de Hello sont nécessaires pour l’installation automatique du service mobilité de hello. Si vous ne pouvez pas sélectionner un compte, assurez-vous que vous en avez établi un comme décrit à l'étape 2. Notez que ce compte ne peut pas être accédé par Azure. Pour Windows, compte hello du serveur doit avoir des privilèges d’administrateur sur le serveur de source de hello. Pour Linux, compte de hello doit être racine.

    ![Informations d’identification Linux](./media/site-recovery-vmware-to-azure-classic-legacy/mobility-account.png)
6. Cliquez sur toofinish de case à cocher hello Ajout d’ordinateurs toohello protection toostart et groupe de réplication initiale pour chaque ordinateur. Vous pouvez surveiller l’état sur hello **travaux** page.

    ![Ajouter un serveur V-Center](./media/site-recovery-vmware-to-azure-classic-legacy/pg-jobs2.png)
7. En outre, vous pouvez surveiller l’état de protection en cliquant sur **Éléments protégés** > nom du groupe de protection > **Machines virtuelles**. Une fois la réplication initiale est terminée et les machines hello synchronisent les données qu’ils présentent **protégé** état.

    ![Tâches relatives aux ordinateurs virtuels](./media/site-recovery-vmware-to-azure-classic-legacy/pg-jobs.png)

### <a name="set-protected-machine-properties"></a>définir les propriétés de l'ordinateur protégé
1. Dès qu’un ordinateur est à l’état **Protégé** , vous pouvez configurer ses propriétés de basculement. Dans les détails du groupe de protection hello sélectionnez hello hello ordinateur et ouvrir **configurer** onglet.
2. Vous pouvez modifier le nom hello donné toohello machine dans Azure après le basculement et hello taille de machine virtuelle Azure. Vous pouvez également sélectionner machine de hello toowhich hello réseau Azure est connectée après le basculement.

   > [!NOTE]
   > [Migration des réseaux](../resource-group-move-resources.md) entre les ressources groupes dans hello même abonnement ou entre abonnements n’est pas prise en charge pour les réseaux utilisés pour le déploiement de Site Recovery.
   >
   >

    ![Définir les propriétés des machines virtuelles](./media/site-recovery-vmware-to-azure-classic-legacy/vm-props.png)

Notez les points suivants :

* nom Hello Hello machine Azure doit être conforme aux exigences d’Azure.
* Par défaut des machines virtuelles répliquées dans Azure ne sont pas connecté tooan réseau Azure. Si vous souhaitez que les machines virtuelles répliquées toocommunicate Assurez-vous tooset hello même réseau Azure pour eux.
* Si vous redimensionnez un volume sur un serveur physique ou un ordinateur virtuel VMware, il passe dans un état critique. Si vous avez besoin de taille de hello toomodify, hello suivant :

  * un) modifiez le paramètre de taille hello.
  * (b) dans hello **virtuels** , sélectionnez l’ordinateur virtuel de hello et cliquez sur **supprimer**.
  * c) dans **supprimer un ordinateur virtuel** l’option hello **désactiver la protection (utiliser l’extraction pour la récupération et redimensionnement de volume)**. Cette option désactive la protection, mais conserve les points de récupération hello dans Azure.

      ![Définir les propriétés des machines virtuelles](./media/site-recovery-vmware-to-azure-classic-legacy/remove-vm.png)
  * d) réactiver la protection des machines virtuelles de hello. Lorsque vous réactivez la protection des données hello pour le volume de hello redimensionné seront transférée tooAzure.

## <a name="step-10-run-a-failover"></a>Étape 10 : exécuter un basculement
Actuellement, vous ne pouvez exécuter que des basculements non planifiés pour les serveurs physiques et les ordinateurs virtuels VMware protégés. Notez hello suivantes :

* Avant d’initier un basculement, vérifiez que hello configuration principale cible des serveurs et sont en cours d’exécution et sain. Le basculement échouera dans le cas contraire.
* Les ordinateurs sources ne sont pas arrêtés dans le cadre d'un basculement non planifié. Effectuer un basculement non planifié, réplication des données pour les serveurs de hello protégé s’arrête. Vous aurez besoin de machines de hello toodelete hello du groupe de protection et les ajouter à nouveau dans l’ordre les toostart protection des ordinateurs une fois terminée hello basculement non planifié.
* Si vous souhaitez toofail par sans perdre de données, assurez-vous que les ordinateurs virtuels hello site principal sont mis hors tension avant de lancer le basculement de hello.

1. Sur hello **les Plans de récupération** page et ajouter un plan de récupération. Spécifier les détails pour le plan de hello et sélectionnez **Azure** comme cible de hello.

    ![Configurer le plan de récupération](./media/site-recovery-vmware-to-azure-classic-legacy/rplan1.png)
2. Dans **sélectionner l’ordinateur virtuel** sélectionner un groupe de protection, puis sélectionnez les ordinateurs dans le plan de récupération hello groupe tooadd toohello. [Découvrez plus d’informations](site-recovery-create-recovery-plans.md) sur les plans de récupération.

    ![Ajouter des machines virtuelles](./media/site-recovery-vmware-to-azure-classic-legacy/rplan2.png)
3. Si nécessaire vous pouvez personnaliser les groupes toocreate hello plan et ordre de tri hello dans les ordinateurs en mode de récupération hello plan est basculé. Vous pouvez également ajouter des invites pour des actions manuelles et des scripts. Hello scripts lors de la récupération de tooAzure peut être ajouté à l’aide de [Runbooks d’automatisation Azure](site-recovery-runbook-automation.md).
4. Bonjour **les Plans de récupération** page plan de hello sélectionnez et cliquez sur **basculement non planifié**.
5. Dans **confirmer le basculement** Vérifiez le sens du basculement hello (tooAzure) et sélectionnez toofail de point de récupération hello supérieur à.
6. Attendez que toocomplete de travail de basculement hello, puis vérifiez que hello basculement fonctionné comme prévu et que hello répliquées démarrer des machines virtuelles dans Azure.

## <a name="step-11-fail-back-failed-over-machines-from-azure"></a>Étape 11 : restaurer automatiquement les ordinateurs basculés depuis Azure
[En savoir plus](site-recovery-failback-azure-to-vmware-classic-legacy.md) sur la toobring votre ayant échoué sur les ordinateurs s’exécutant dans Azure précédent environnement local de tooyour.

## <a name="manage-your-process-servers"></a>Gérer vos serveurs de traitement
serveur de processus Hello envoie le serveur cible maître de réplication données toohello dans Azure et détecte le nouveau serveur de vCenter tooa ajouté les ordinateurs virtuels VMware. Dans hello suivant circonstances, vous souhaiterez serveur de processus toochange hello dans votre déploiement :

* Si le serveur de processus en cours hello tombe en panne
* Si le point de récupération du objectif (RPO) augmente tooan de niveau inacceptable pour votre organisation.

Si nécessaire que vous pouvez déplacer la réplication hello de tout ou partie de votre local VMware virtual machines et tooa de serveurs physiques différents processus. Par exemple :

* **Échec de**: si un serveur de processus échoue ou qu’il n’est pas disponible si vous pouvez déplacer le serveur de processus tooanother ordinateur protégé par la réplication. Métadonnées de l’ordinateur source de hello et machine de réplication seront déplacés toohello nouveau serveur de processus et de données sont resynchronisées. nouveau serveur de processus Hello se connecte automatiquement à la découverte automatique toohello vCenter server tooperform. Vous pouvez surveiller l’état de hello de serveurs de traitement sur le tableau de bord hello Site Recovery.
* **Équilibrage tooadjust RPO**— pour l’équilibrage amélioré vous pouvez sélectionner un autre serveur de processus dans le portail Site Recovery hello et déplace la réplication d’un ou plusieurs tooit machines pour l’équilibrage de charge manuelle. Dans ce cas, les métadonnées de la source sélectionnée de hello et les ordinateurs de réplication sont déplacé toohello nouveau serveur de processus. serveur de processus Hello d’origine reste connecté toohello vCenter server.

### <a name="monitor-hello-process-server"></a>Serveur de processus Moniteur hello
Si un serveur de processus est dans un état critique un avertissement d’état s’affichera sur hello récupération de Site du tableau de bord. Vous pouvez cliquer sur l’onglet événements de hello état tooopen hello et puis Explorer les travaux toospecific sur l’onglet tâches de hello.

### <a name="modify-hello-process-server-used-for-replication"></a>Modifier le serveur de processus hello utilisée pour la réplication
1. Cliquez sur **Serveurs** > **Serveurs de configuration** > serveur de configuration > **Détails du serveur**.
2. Cliquez sur **serveurs de processus** > **modifier le serveur de processus** suivant toohello serveur toomodify.

    ![Modifier le serveur de traitement 1](./media/site-recovery-vmware-to-azure-classic-legacy/change-ps1.png)
3. Dans **modifier le serveur de processus** > **serveur de processus cible** sélectionnez hello nouveau serveur souhaité toouse puis sélectionnez hello ordinateurs virtuels que vous souhaitez tooreplicate toohello nouveau serveur. Cliquez sur hello icône suivant toohello nom de serveur pour plus d’informations d’espace libre et de la mémoire utilisée. espace moyen Hello sera tooreplicate requis, chaque ordinateur virtuel sélectionné toohello nouveau serveur de processus est affichée toohelp vous que la charge des décisions.

    ![Modifier le serveur de traitement 2](./media/site-recovery-vmware-to-azure-classic-legacy/change-ps2.png)
4. Cliquez sur toobegin de case à cocher hello toohello nouveau serveur de processus de réplication. Notez que si vous supprimez toutes les machines virtuelles à partir d’un serveur de processus qui a été critiques qu’il doit n’est plus affiche un avertissement critique dans le tableau de bord hello.

## <a name="third-party-software-notices-and-information"></a>Informations et remarques relatives aux logiciels tiers
Do Not Translate or Localize

logiciels de Hello et de microprogramme en cours d’exécution hello produit Microsoft ou service repose sur ou inclut, du contenu à partir de hello projets répertoriés ci-dessous (collectivement, « Code tiers »).  Microsoft est hello pas auteur de hello Code de tiers.  mention de copyright d’origine Hello et de licence, dans lesquelles Microsoft a reçu ce Code tiers, sont définies ci-dessous.

informations Hello dans la Section A concerne un Code de tiers des composants à partir de projets de hello répertoriées ci-dessous. Such licenses and information are provided for informational purposes only.  Ce Code de tiers est en cours tooyou relicensed par Microsoft hello produit ou service Microsoft termes du contrat de licence des logiciels de Microsoft.  

informations Hello dans la Section B concernant les composants de Code de tiers qui sont établies tooyou disponible par Microsoft sous les termes du contrat de licence d’origine hello.

fichier dans son intégralité Hello se trouve sur hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel or otherwise.
