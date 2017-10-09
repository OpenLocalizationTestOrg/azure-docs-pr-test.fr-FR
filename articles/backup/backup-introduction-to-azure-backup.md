---
title: "aaaWhat est Azure Backup ? | Microsoft Docs"
description: "Utilisez Azure Backup tooback et restaurer des données et les charges de travail à partir de serveurs Windows, les stations de travail Windows, les serveurs System Center DPM et les machines virtuelles."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "sauvegarde et restauration ; services de restauration ; solutions de sauvegarde"
ms.assetid: 0d2a7f08-8ade-443a-93af-440cbf7c36c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/11/2017
ms.author: markgal;trinadhk;anuragm
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 953a19600f67a6b7451f71b1e3234d913816d18c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-features-in-azure-backup"></a>Vue d’ensemble des fonctionnalités de hello dans Azure Backup
Azure Backup est service basé sur Azure hello vous pouvez utiliser un tooback (ou protéger) et restaurer vos données Bonjour cloud de Microsoft. Azure Backup remplace votre solution de sauvegarde locale ou hors site par une solution basée dans le cloud à la fois fiable, sécurisée et économique. Sauvegarde Azure offre plusieurs composants que vous téléchargez et déployez sur les ordinateurs appropriés hello, server, ou dans le cloud de hello. composant de Hello, ou un agent, que vous déployez dépend de ce que vous souhaitez tooprotect. Tous les composants d’Azure Backup (quel que soit le si vous protégez des données en local ou dans le cloud de hello) peuvent être utilisé tooback configuration coffre de Services de récupération des données tooa dans Azure. Consultez hello [table des composants Azure Backup](backup-introduction-to-azure-backup.md#which-azure-backup-components-should-i-use) (plus loin dans cet article) pour plus d’informations sur les données de composant toouse tooprotect spécifiques, des applications ou charges de travail.

[Regarder une vidéo de présentation d’Azure Backup](https://azure.microsoft.com/documentation/videos/what-is-azure-backup/)

## <a name="why-use-azure-backup"></a>Pourquoi utiliser Azure Backup ?
Solutions de sauvegarde traditionnelles ont évolué cloud de hello tootreat comme un point de terminaison, ou la destination de stockage statique, toodisks similaire ou une bande. Cette approche est simple, il est limitée et ne tire pas parti complète d’une plateforme cloud sous-jacente, qui se traduit par la solution de coûteux, inefficace tooan. Autres solutions sont coûteux, car vous vous retrouvez payer pour un type incorrect hello de stockage, ou de stockage que vous n’avez pas besoin. Autres solutions sont souvent inefficaces, car ils ne vous offrent les type hello ou la quantité de stockage dont vous avez besoin, ou des tâches d’administration nécessitent trop de temps. Par opposition, Azure Backup offre les principaux avantages suivants :

**Gestion du stockage automatique** - environnements hybrides nécessitent souvent stockage hétérogène : certains sur site et certains se trouvent dans hello cloud. Avec Azure Backup, l’utilisation d’appareils de stockage locaux ne génère aucun coût. Azure Backup alloue et gère automatiquement le stockage de sauvegarde sur la base d’un modèle de paiement à l’utilisation. Payer en tant que-vous à l’emploi signifie que vous ne payez que pour le stockage de hello vous consommez. Pour plus d’informations, consultez hello [Azure tarification article](https://azure.microsoft.com/pricing/details/backup).

**Mise à l’échelle illimitées** - Azure Backup utilise hello sous-jacent power et un nombre illimité d’échelle de hello Azure cloud toodeliver haute disponibilité - avec aucune maintenance ou de la surcharge d’analyse. Vous pouvez définir des informations sur les alertes tooprovide sur les événements, mais vous n’avez pas besoin tooworry sur la haute disponibilité pour vos données dans le cloud de hello.

**Diverses options de stockage** : la réplication du stockage est l’un des facteurs de haute disponibilité. La solution Sauvegarde Azure propose deux types de réplications : le [stockage localement redondant](../storage/common/storage-redundancy.md#locally-redundant-storage) et le [stockage géoredondant](../storage/common/storage-redundancy.md#geo-redundant-storage). Choisissez l’option de stockage de sauvegarde hello en fonction des besoins :

* Stockage localement redondant (LRS) réplique vos données trois fois (il crée trois copies de vos données) dans un centre de données apparié hello même région. Le stockage LRS est une option à faible coût qui protège vos données contre les défaillances matérielles locales.

* Stockage géo-redondant (GRS) réplique vos données tooa secondaire la région (des centaines de miles en dehors de l’emplacement principal de hello de source de données hello). Le stockage GRS est plus onéreux que le stockage LRS, mais il offre une durabilité des données supérieure, même en cas de panne au niveau régional.

**Transfert de données illimité** - Azure Backup ne limite pas la quantité de hello de trafic entrant ou sortantes vous de transfert de données. Également, la sauvegarde Azure ne facture pas pour les données hello sont transférées. Toutefois, si vous utilisez hello Azure Import/Export service tooimport grandes quantités de données, a un coût associé à des données entrantes. Pour plus d’informations sur ce coût, consultez [Flux de travail de la sauvegarde hors connexion dans Azure Backup](backup-azure-backup-import-export.md). Données sortantes fait référence toodata transféré à partir d’un coffre de Services de récupération pendant une opération de restauration.

**Le chiffrement des données** -chiffrement des données permet de sécuriser la transmission et le stockage de vos données dans un cloud public hello. Vous stockez la phrase secrète de chiffrement hello localement, et il n’est jamais transmise ou stockée dans Azure. S’il s’agit de tout état nécessaire toorestore de données de hello, seulement vous avez phrase secrète de chiffrement ou de clé.

**Sauvegarde avec cohérence d’application** -si vous sauvegardez un serveur de fichiers, un ordinateur virtuel ou une base de données SQL, vous devez tooknow qu’un point de récupération possède toutes les requis de copie de sauvegarde de données toorestore hello. Azure Backup offre des sauvegardes cohérentes avec les applications qui garantissait des correctifs supplémentaires ne sont pas les données de salutation toorestore nécessaires. Restauration de données cohérent d’application réduit les temps de restauration hello, ce qui vous tooa de retour tooquickly état en cours d’exécution.

**Rétention à long terme** -au lieu de passer des copies de sauvegarde de disque tootape et déplacement hello bande tooan hors site, vous pouvez utiliser Azure pour la rétention à court terme et à long terme. Azure ne limite pas durée hello de données restent dans un coffre de sauvegarde ou de Services de récupération. Vous pouvez conserver des données dans un coffre aussi longtemps que vous le souhaitez. Azure Backup est limité à 9 999 points de récupération par instance protégée. Consultez hello [sauvegarde et rétention](backup-introduction-to-azure-backup.md#backup-and-retention) dans cet article pour une explication de la manière dont cette limite peut affecter vos besoins de sauvegarde.  

## <a name="which-azure-backup-components-should-i-use"></a>Quels composants Azure Backup dois-je utiliser ?
Si vous ne savez pas quel composant de sauvegarde Azure fonctionne pour vos besoins, consultez hello tableau pour plus d’informations sur ce que vous pouvez protéger chaque composant suivant. Hello portail Azure fournit un Assistant, ce qui est intégré à un portail hello, tooguide vous en choisissant hello toodownload de composant et que vous déployez. Assistant Hello, qui fait partie de la création du coffre Recovery Services de hello, vous guide tout au long des étapes de hello pour le choix d’un objectif de sauvegarde et en choisissant tooprotect de données ou d’une application hello.

| Composant | Avantages | limites | Qu’est-ce qui est protégé ? | Où sont stockées les sauvegardes ? |
| --- | --- | --- | --- | --- |
| Agent Azure Backup (MARS) |<li>Sauvegarde des fichiers et des dossiers sur un système d’exploitation Windows physique ou virtuel (les machines virtuelles peuvent être locales ou dans Azure)<li>Aucun serveur de sauvegarde distinct n’est requis. |<li>Sauvegarde 3 fois par jour <li>Ne tient pas compte des applications ; restauration au niveau du fichier, du dossier et du volume seulement, <li>  Linux non pris en charge. |<li>Fichiers, <li>Dossiers |Coffre Recovery Services |
| System Center DPM |<li>Instantanés tenant compte des applications (VSS)<li>Total de flexibilité pour le tootake des sauvegardes<li>Granularité de récupération (tout)<li>Possibilité d’utiliser un coffre Recovery Services<li>Prise en charge de Linux sur machines virtuelles Hyper-V et VMware <li>Sauvegarder et restaurer des machines virtuelles VMware à l’aide de DPM 2012 R2 |Impossible de sauvegarder des charges de travail Oracle.|<li>Fichiers, <li>Dossiers,<li> Volumes, <li>Machines virtuelles,<li> Applications,<li> Charges de travail |<li>Coffre Recovery Services,<li> Disque connecté localement,<li>  Bande (locale uniquement) |
| Azure Backup Server |<li>Instantanés tenant compte des applications (VSS)<li>Total de flexibilité pour le tootake des sauvegardes<li>Granularité de récupération (tout)<li>Possibilité d’utiliser un coffre Recovery Services<li>Prise en charge de Linux sur machines virtuelles Hyper-V et VMware<li>Sauvegarder et restaurer des machines virtuelles VMWare <li>Ne nécessite pas de licence System Center |<li>Impossible de sauvegarder des charges de travail Oracle.<li>Requiert toujours un abonnement Azure en direct<li>Aucune prise en charge de la sauvegarde sur bande |<li>Fichiers, <li>Dossiers,<li> Volumes, <li>Machines virtuelles,<li> Applications,<li> Charges de travail |<li>Coffre Recovery Services,<li> Disque connecté localement |
| Sauvegarde des machines virtuelles IaaS Azure |<li>Sauvegardes natives pour Windows/Linux<li>Aucune installation spécifique d’agent n’est requise<li>Sauvegarde au niveau structure sans nécessiter d’infrastructure de sauvegarde |<li>Sauvegarde des machines virtuelles une fois par jour <li>Restauration des machines virtuelles uniquement au niveau du disque<li>Impossible d’effectuer une sauvegarde en local |<li>Machines virtuelles, <li>Tous les disques (à l’aide de PowerShell) |<p>Coffre Recovery Services</p> |

## <a name="what-are-hello-deployment-scenarios-for-each-component"></a>Quels sont les scénarios de déploiement hello pour chaque composant ?
| Composant | Déploiement possible dans Azure ? | Déploiement possible localement ? | Stockage cible pris en charge |
| --- | --- | --- | --- |
| Agent Azure Backup (MARS) |<p>**Oui**</p> <p>Hello Azure Backup agent peut être déployé sur n’importe quel ordinateur Windows Server qui s’exécute dans Azure.</p> |<p>**Oui**</p> <p>l’agent de sauvegarde Hello peut être déployé sur tout ordinateur virtuel Windows Server ou d’un ordinateur physique.</p> |<p>Coffre Recovery Services</p> |
| System Center DPM |<p>**Oui**</p><p>En savoir plus sur [comment tooprotect les charges de travail dans Azure à l’aide de System Center DPM](backup-azure-dpm-introduction.md).</p> |<p>**Oui**</p> <p>En savoir plus sur [comment tooprotect les charges de travail et machines virtuelles dans votre centre de données](https://technet.microsoft.com/system-center-docs/dpm/data-protection-manager).</p> |<p>Disque connecté localement,</p> <p>Coffre Recovery Services,</p> <p>Bande (locale uniquement)</p> |
| Azure Backup Server |<p>**Oui**</p><p>En savoir plus sur [comment tooprotect les charges de travail dans Azure à l’aide d’Azure Backup Server](backup-azure-microsoft-azure-backup.md).</p> |<p>**Oui**</p> <p>En savoir plus sur [comment tooprotect les charges de travail dans Azure à l’aide d’Azure Backup Server](backup-azure-microsoft-azure-backup.md).</p> |<p>Disque connecté localement,</p> <p>Coffre Recovery Services</p> |
| Sauvegarde des machines virtuelles IaaS Azure |<p>**Oui**</p><p>Partie de la structure Azure</p><p>Spécialisé dans la [sauvegarde des machines virtuelles Azure IaaS (infrastructure en tant que service)](backup-azure-vms-introduction.md).</p> |<p>**Non**</p> <p>Utilisez tooback System Center DPM les machines virtuelles dans votre centre de données.</p> |<p>Coffre Recovery Services</p> |

## <a name="which-applications-and-workloads-can-be-backed-up"></a>Quelles applications et charges de travail est-il possible de sauvegarder ?
Hello tableau suivant fournit une matrice de données de hello et de charges de travail qui peuvent être protégés à l’aide d’Azure Backup. colonne de solution de sauvegarde Azure Hello a la documentation relative au déploiement des liens toohello pour cette solution. Chaque composant Azure Backup peut être déployé dans un environnement de modèle de déploiement Classic ou Resource Manager.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

| Données ou charge de travail | Environnement source | Solution Azure Backup |
| --- | --- | --- |
| Fichiers et dossiers |Windows Server |<p>[Agent Azure Backup](backup-configure-vault.md),</p> <p>[System Center DPM](backup-azure-dpm-introduction.md) (+ hello Azure Backup agent)</p> <p>[Serveur de sauvegarde Azure](backup-azure-microsoft-azure-backup.md) (y compris hello Azure Backup agent)</p> |
| Fichiers et dossiers |Ordinateur Windows |<p>[Agent Azure Backup](backup-configure-vault.md),</p> <p>[System Center DPM](backup-azure-dpm-introduction.md) (+ hello Azure Backup agent)</p> <p>[Serveur de sauvegarde Azure](backup-azure-microsoft-azure-backup.md) (y compris hello Azure Backup agent)</p> |
| Machine virtuelle Hyper-V (Windows) |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure Backup agent)</p> <p>[Serveur de sauvegarde Azure](backup-azure-microsoft-azure-backup.md) (y compris hello Azure Backup agent)</p> |
| Machine virtuelle Hyper-V (Linux) |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure Backup agent)</p> <p>[Serveur de sauvegarde Azure](backup-azure-microsoft-azure-backup.md) (y compris hello Azure Backup agent)</p> |
| Microsoft SQL Server |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure Backup agent)</p> <p>[Serveur de sauvegarde Azure](backup-azure-microsoft-azure-backup.md) (y compris hello Azure Backup agent)</p> |
| Microsoft SharePoint |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure Backup agent)</p> <p>[Serveur de sauvegarde Azure](backup-azure-microsoft-azure-backup.md) (y compris hello Azure Backup agent)</p> |
| Microsoft Exchange |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure Backup agent)</p> <p>[Serveur de sauvegarde Azure](backup-azure-microsoft-azure-backup.md) (y compris hello Azure Backup agent)</p> |
| Machines virtuelles IaaS Azure (Windows) |exécution dans Azure |[Azure Backup (extension de machine virtuelle)](backup-azure-vms-introduction.md) |
| Machines virtuelles IaaS Azure (Linux) |exécution dans Azure |[Azure Backup (extension de machine virtuelle)](backup-azure-vms-introduction.md) |

## <a name="linux-support"></a>Prise en charge de Linux
Hello tableau suivant montre les composants de sauvegarde Azure hello qui prennent en charge Linux.  

| Composant | Prise en charge Linux (approuvée par Azure) |
| --- | --- |
| Agent Azure Backup (MARS) |Aucun (agent uniquement sur Windows) |
| System Center DPM |<li> Sauvegarde cohérente au niveau fichier de machines virtuelles invitées Linux sur Hyper-V et VMware<br/> <li> Restauration de machines virtuelles invitées Linux Hyper-V et VMware </br> </br>  *Sauvegarde cohérente des fichiers non disponible pour la machine virtuelle Azure* <br/> |
| Azure Backup Server |<li>Sauvegarde cohérente au niveau fichier de machines virtuelles invitées Linux sur Hyper-V et VMware<br/> <li> Restauration de machines virtuelles invitées Linux Hyper-V et VMware </br></br> *Sauvegarde cohérente des fichiers non disponible pour la machine virtuelle Azure*  |
| Sauvegarde des machines virtuelles IaaS Azure |Sauvegarde cohérente au niveau application à l’aide de [l’infrastructure pré et post-script](backup-azure-linux-app-consistent.md)<br/> [Récupération de fichiers granulaire](backup-azure-restore-files-from-vm.md)<br/> [Restaurer tous les disques de machines virtuelles](backup-azure-arm-restore-vms.md#restore-backed-up-disks)<br/> [Restauration de machines virtuelles](backup-azure-arm-restore-vms.md#create-a-new-vm-from-restore-point) |

## <a name="using-premium-storage-vms-with-azure-backup"></a>Utilisation des machines virtuelles Premium Storage avec Azure Backup
Azure Backup protège les machines virtuelles Premium Storage. Stockage Azure Premium est un disque SSD (SSD)-les charges de travail de stockage conçu toosupport e/S intensives. Stockage Premium est intéressant pour les charges de travail des machines virtuelles. Pour plus d’informations sur le stockage Premium, consultez l’article hello, [stockage Premium : stockage hautes performances pour les charges de travail de Machine virtuelle Azure](../storage/common/storage-premium-storage.md).

### <a name="back-up-premium-storage-vms"></a>Sauvegarder des machines virtuelles Premium Storage
Lors de la sauvegarde des ordinateurs virtuels de stockage Premium, service de sauvegarde hello crée un emplacement temporaire, nommé « AzureBackup- », dans le compte de stockage Premium hello. Hello hello emplacement intermédiaire est égal toohello taille d’instantané de point de récupération hello. Veillez à hello compte de stockage Premium a suffisamment d’espace disponible tooaccommodate hello intermédiaire un emplacement temporaire. Pour plus d’informations, consultez l’article hello, [limitations de stockage premium](../storage/common/storage-premium-storage.md#scalability-and-performance-targets). Une fois que la fin du travail de sauvegarde hello, hello emplacement intermédiaire est supprimé. Hello prix du stockage utilisé pour hello emplacement intermédiaire est cohérent avec toutes les [tarification du stockage Premium](../storage/common/storage-premium-storage.md#pricing-and-billing).

> [!NOTE]
> Ne modifiez pas ou ne modifier hello emplacement intermédiaire.
>
>

### <a name="restore-premium-storage-vms"></a>Restaurer des machines virtuelles Premium Storage
Machines virtuelles de stockage Premium peut être restaurée tooeither stockage Premium ou toonormal. Restauration d’un tooPremium arrière du point de récupération VM de stockage Premium stockage consiste à hello classique de restauration. Toutefois, il peut être rentable toorestore un point toostandard de stockage de récupération d’ordinateur virtuel de stockage Premium. Ce type de restauration peut être utilisé si vous avez besoin d’un sous-ensemble de fichiers à partir de la machine virtuelle de hello.

## <a name="using-managed-disk-vms-with-azure-backup"></a>Utilisation des machines virtuelles de disque géré avec Azure Backup
Azure Backup protège les machines virtuelles de disque géré. Les disques gérés vous libèrent de la gestion des comptes de stockage des machines virtuelles et simplifient considérablement l’approvisionnement des machines virtuelles.

### <a name="back-up-managed-disk-vms"></a>Sauvegarder des machines virtuelles de disque géré
La sauvegarde des machines virtuelles sur des disques gérés est identique à la sauvegarde des machines virtuelles de Resource Manager. Bonjour portail Azure, vous pouvez configurer la tâche de sauvegarde hello directement à partir de hello, vue de l’ordinateur virtuel ou à partir des Services de récupération hello de coffre de vue. Vous pouvez sauvegarder des machines virtuelles sur des disques gérés par le biais des collections RestorePoint basées sur des disques gérés. Azure Backup prend également en charge la sauvegarde des machines virtuelles de disque géré chiffrées avec Azure Disk Encryption (ADE).

### <a name="restore-managed-disk-vms"></a>Restaurer des machines virtuelles de disque géré
Azure Backup permet de toorestore une VM terminée avec des disques gérés, ou restauration gérés compte de stockage tooa de disques. Azure gère les disques hello géré pendant le processus de restauration hello. Vous (client hello) gérez le compte de stockage hello créé dans le cadre du processus de restauration hello. Lors de la restauration géré chiffrée de machines virtuelles, hello clés et les secrets de l’ordinateur virtuel doivent exister dans l’opération de restauration hello hello coffre de clés toostarting préalable.

## <a name="what-are-hello-features-of-each-backup-component"></a>Quelles sont les fonctions hello de chaque composant de sauvegarde ?
Hello les sections suivantes fournit des tables qui résument la disponibilité de hello ou prise en charge de diverses fonctionnalités dans chaque composant de sauvegarde Azure. Consultez les informations de hello suivant chaque table prise en charge supplémentaire pour des détails.

### <a name="storage"></a>Storage
| Fonctionnalité | Agent Azure Backup | System Center DPM | Azure Backup Server | Sauvegarde des machines virtuelles IaaS Azure |
| --- | --- | --- | --- | --- |
| Coffre Recovery Services |![Oui][green] |![Oui][green] |![Oui][green] |![Oui][green] |
| Stockage sur disque | |![Oui][green] |![Oui][green] | |
| Stockage sur bande | |![Oui][green] | | |
| Compression <br/>(dans un coffre Recovery Services) |![Oui][green] |![Oui][green] |![Oui][green] | |
| Sauvegarde incrémentielle |![Oui][green] |![Oui][green] |![Oui][green] |![Oui][green] |
| Déduplication de disque | |![Partiellement][yellow] |![Partiellement][yellow] | | |

![clé de table](./media/backup-introduction-to-azure-backup/table-key.png)

le coffre Recovery Services Hello est la cible de stockage par défaut de hello sur tous les composants. System Center DPM et Azure Backup Server fournissent également hello option toohave une copie du disque local. Toutefois, System Center DPM fournit hello option toowrite tooa bande dispositif de stockage.

#### <a name="compression"></a>Compression
Les sauvegardes sont compressées tooreduce hello requise d’espace de stockage. Hello seul composant qui n’utilise pas la compression est l’extension de machine virtuelle hello. copies d’extension de machine virtuelle Hello toutes les données de sauvegarde à partir de votre toohello de compte de stockage des Services de récupération de coffre dans hello même région. Aucune compression est utilisée lors du transfert de données de salutation. Transfert de données hello sans compression légèrement augmente le stockage hello utilisé. Toutefois, stockez les données de hello sans la compression permet de restauration plus rapide, si vous avez besoin ce point de récupération.


#### <a name="disk-deduplication"></a>Déduplication de disque
Vous pouvez tirer parti de la déduplication lorsque vous déployez System Center DPM ou le serveur de sauvegarde Azure [sur une machine virtuelle Hyper-V](http://blogs.technet.com/b/dpm/archive/2015/01/06/deduplication-of-dpm-storage-reduce-dpm-storage-consumption.aspx). Windows Server effectue la déduplication des données (au niveau de l’hôte hello) sur les disques durs virtuels (VHD) qui sont attachés toohello l’ordinateur virtuel en tant que stockage de sauvegarde.

> [!NOTE]
> La déduplication n’est pas disponible dans Azure pour aucun des composants Azure Backup. Lorsque System Center DPM et le serveur de sauvegarde sont déployés dans Azure, les disques de stockage hello attaché toohello que machine virtuelle ne peut pas être dédupliqué.
>
>

### <a name="incremental-backup-explained"></a>Explication de la sauvegarde incrémentielle
Chaque composant de sauvegarde Azure prend en charge la sauvegarde incrémentielle, quelle que soit le stockage de cible hello (disque, bande, coffre Recovery Services). Sauvegarde incrémentielle garantit que les sauvegardes sont stockées et temps efficace, en transférant uniquement les modifications apportées depuis la dernière sauvegarde de hello.

#### <a name="comparing-full-differential-and-incremental-backup"></a>Comparaison entre la sauvegarde complète, différentielle et incrémentielle

La consommation du stockage, l’objectif de délai de récupération (RTO) et la consommation réseau varient pour chaque type de méthode de sauvegarde. tookeep hello sauvegarde coût total de possession (TCO) vers le bas, vous devez toounderstand la solution de sauvegarde meilleures toochoose hello. Hello suivant image compare la sauvegarde complète et une sauvegarde différentielle sauvegarde incrémentielle. Dans l’image de hello, source de données Qu'a est composé de stockage 10 bloque A1-A10, qui sont sauvegardé mensuelle. Blocs A2, A3, A4, A9 modifier Bonjour premier mois et bloquer les modifications de A5 Bonjour mois suivant.

![illustration montrant la comparaison des méthodes de sauvegarde](./media/backup-introduction-to-azure-backup/backup-method-comparison.png)

Avec **sauvegarde complète**, chaque copie de sauvegarde contienne hello toute source de données. La sauvegarde complète consomme une grande quantité de bande passante réseau et de stockage, à chaque fois qu’une copie de sauvegarde est transférée.

**Sauvegarde différentielle** stocke uniquement hello bloque changé depuis hello sauvegarde initiale complète, ce qui entraîne une plus petite quantité de la consommation de stockage et de réseau. Les sauvegardes différentielles ne conservent pas de copies redondantes des données inchangées. Toutefois, étant donné que les blocs de données hello restent inchangées entre les sauvegardes ultérieures sont transférées et stockées, les sauvegardes différentielles sont inefficaces. Bonjour deuxième mois, les blocs modifiés A2, A3, A4 et A9 sont sauvegardées. Bonjour troisième mois, ces blocs mêmes sont sauvegardées, ainsi que le bloc modifié A5. Hello blocs modifié continuer toobe de sauvegarde jusqu'à la sauvegarde complète de hello suivant se produit.

**Sauvegarde incrémentielle** parvient à haute efficacité de stockage et de réseau en stockant des blocs hello uniquement des données modifiées depuis la sauvegarde précédente de hello. Avec une sauvegarde incrémentielle, il n’est aucun nécessaire tootake des sauvegardes régulières complète. Dans l’exemple de hello, après que hello sauvegarde complète est effectuée pour hello premier mois, les blocs modifiés A2, A3, A4 et A9 sont marqués comme modifiés et transférées pour hello deuxième mois. Bonjour troisième mois, modifié uniquement un bloc A5 est marqué et transféré. Le fait de déplacer moins de données permet d’économiser des ressources de réseau et de stockage, ce qui réduit le coût total de possession.   

### <a name="security"></a>Sécurité
| Fonctionnalité | Agent Azure Backup | System Center DPM | Azure Backup Server | Sauvegarde des machines virtuelles IaaS Azure |
| --- | --- | --- | --- | --- |
| Sécurité du réseau<br/> (tooAzure) |![Oui][green] |![Oui][green] |![Oui][green] |![Partiellement][yellow] |
| Sécurité des données<br/> (dans Azure) |![Oui][green] |![Oui][green] |![Oui][green] |![Partiellement][yellow] |

![clé de table](./media/backup-introduction-to-azure-backup/table-key.png)

#### <a name="network-security"></a>Sécurité du réseau
Tout le trafic de sauvegarde à partir de votre toohello de serveurs de coffre Recovery Services est chiffré à l’aide de 256 Standard de chiffrement avancé. les données de sauvegarde Hello sont envoyées via une connexion HTTPS sécurisée. les données de sauvegarde Hello sont également stockées dans le coffre Recovery Services hello sous forme chiffrée. Uniquement, hello client Azure, avoir hello phrase secrète toounlock ces données. Microsoft ne peut pas déchiffrer les données de sauvegarde hello à tout moment.

> [!WARNING]
> Une fois que vous établissez le coffre Recovery Services hello, vous suffit de clé de chiffrement toohello accès. Microsoft jamais conserve une copie de votre clé de chiffrement et n’a pas de clé d’accès toohello. Si la clé de hello est mal placé, Microsoft ne peut pas récupérer les données de sauvegarde hello.
>
>

#### <a name="data-security"></a>Sécurité des données
Sauvegarde des machines virtuelles Azure nécessite de configuration du chiffrement *dans* hello virtual machine. Utilisez BitLocker sur les machines virtuelles Windows et **dm-crypt** sur les machines virtuelles Linux. Azure Backup ne chiffre pas automatiquement les données de sauvegarde en provenance de ce chemin d’accès.

### <a name="network"></a>Réseau
| Fonctionnalité | Agent Azure Backup | System Center DPM | Azure Backup Server | Sauvegarde des machines virtuelles IaaS Azure |
| --- | --- | --- | --- | --- |
| Compression réseau <br/>(trop**sauvegarde du serveur**) | |![Oui][green] |![Oui][green] | |
| Compression réseau <br/>(trop**de coffre Recovery Services**) |![Oui][green] |![Oui][green] |![Oui][green] | |
| Protocole réseau <br/>(trop**sauvegarde du serveur**) | |TCP |TCP | |
| Protocole réseau <br/>(trop**de coffre Recovery Services**) |HTTPS |HTTPS |HTTPS |HTTPS |

![clé de table](./media/backup-introduction-to-azure-backup/table-key-2.png)

Hello extension de machine virtuelle (sur hello IaaS VM) lit les hello données directement à partir de hello compte de stockage Azure via le réseau de stockage hello, il n’est pas nécessaire toocompress ce trafic.

Si vous utilisez un serveur de System Center DPM ou d’un serveur de sauvegarde Azure en tant qu’un sauvegarde du serveur secondaire, compresser les données de hello allant hello principal toohello sauvegarde du serveur. La compression des données avant la sauvegarde tooDPM ou Azure Backup Server, enregistre la bande passante.

#### <a name="network-throttling"></a>Limitation du réseau
agent de sauvegarde Azure Hello offre limitation du réseau, qui vous permet de toocontrol utilisation de la bande passante réseau lors du transfert de données. La limitation peut être utile si vous devez tooback des données pendant les heures de travail mais que vous ne souhaitez pas que toointerfere du processus de sauvegarde hello avec tout autre trafic internet. La limitation pour les données de transfert s’applique tooback des activités et de restauration.

## <a name="backup-and-retention"></a>Sauvegarde et rétention

La solution Sauvegarde Azure présente une limite de 9 999 points de récupération, également appelés copies ou instantanés de sauvegarde, par *instance protégée*. Une instance protégée est un ordinateur, serveur (physique ou virtuel) ou tooback de charge de travail configuré des données tooAzure. Pour plus d’informations, consultez la section de hello, [ce qui est une instance protégée](backup-introduction-to-azure-backup.md#what-is-a-protected-instance). Une instance est protégée une fois qu’une copie de sauvegarde des données a été enregistrée. copie de sauvegarde Hello de données est une protection hello. Si la source de données hello a été perdue ou a été endommagé, copie de sauvegarde hello peut restaurer des données de source de hello. Hello tableau suivant montre fréquence de sauvegarde maximale hello pour chaque composant. Configuration de votre stratégie de sauvegarde détermine la rapidité d’utilisation de points de récupération hello. Par exemple, si vous créez un point de récupération chaque jour, vous pouvez conserver les points de récupération pendant 27 ans avant d’en manquer. Si vous prenez un point de récupération tous les mois, vous pouvez conserver les points de récupération pour 833 années avant d’exécuter. Hello service de sauvegarde ne définit pas un délai d’expiration sur un point de récupération.

|  | Agent Azure Backup | System Center DPM | Azure Backup Server | Sauvegarde des machines virtuelles IaaS Azure |
| --- | --- | --- | --- | --- |
| Fréquence de sauvegarde<br/> (coffre tooRecovery Services) |Trois sauvegardes par jour |Deux sauvegardes par jour |Deux sauvegardes par jour |Une sauvegarde par jour |
| Fréquence de sauvegarde<br/> (toodisk) |Non applicable |<li>Toutes les 15 minutes pour SQL Server <li>Toutes les heures pour les autres charges de travail |<li>Toutes les 15 minutes pour SQL Server <li>Toutes les heures pour les autres charges de travail</p> |Non applicable |
| Options de rétention |Quotidienne, hebdomadaire, mensuelle, annuelle |Quotidienne, hebdomadaire, mensuelle, annuelle |Quotidienne, hebdomadaire, mensuelle, annuelle |Quotidienne, hebdomadaire, mensuelle, annuelle |
| Nombre maximal de points de récupération par instance protégée |9 999|9 999|9 999|9 999|
| Période de rétention maximale |Dépend de la fréquence de sauvegarde |Dépend de la fréquence de sauvegarde |Dépend de la fréquence de sauvegarde |Dépend de la fréquence de sauvegarde |
| Points de récupération sur le disque local |Non applicable |<li>64 pour les serveurs de fichiers,<li>448 pour les serveurs d’applications |<li>64 pour les serveurs de fichiers,<li>448 pour les serveurs d’applications |Non applicable |
| Points de récupération sur bande |Non applicable |Illimité |Non applicable |Non applicable |

## <a name="what-is-a-protected-instance"></a>Qu’est-ce qu’une instance protégée ?
Une instance protégée est un ordinateur Windows de tooa référence générique, un serveur (physique ou virtuel) ou une base de données SQL qui a été configuré tooback des tooAzure. Une instance est protégée une fois que vous configurez une stratégie de sauvegarde pour l’ordinateur de hello, serveur ou base de données, créez une copie de sauvegarde de données de hello. Les copies suivantes hello des données de sauvegarde pour cette instance protégée (qui sont appelés des points de récupération), augmentez hello de stockage consommé. Vous pouvez créer des points de récupération too9999 pour une instance protégée. Si vous supprimez un point de récupération à partir du stockage, il ne compte pas sur le total de points de récupération 9999 hello.
Des exemples courants d’instances protégées sont des ordinateurs virtuels, les serveurs d’applications, les bases de données et les ordinateurs personnels exécutant le système d’exploitation de Windows hello. Par exemple :

* Un ordinateur virtuel en cours d’exécution l’ensemble fibre optique hyperviseur hello Hyper-V ou IaaS Azure. les systèmes d’exploitation invités Hello pour la machine virtuelle de hello peut être Windows Server ou Linux.
* Un serveur d’applications : serveur d’applications hello peut être un ordinateur physique ou virtuel exécutant Windows Server et les charges de travail avec des données qui doit toobe sauvegardé. Microsoft SQL Server, Microsoft Exchange server, Microsoft SharePoint server et rôle de serveur de fichiers hello sur Windows Server sont des charges de travail courantes. tooback de ces charges de travail, vous devez System Center Data Protection Manager (DPM) ou le serveur de sauvegarde Azure.
* Un ordinateur personnel, une station de travail ou un ordinateur portable exécutant le système d’exploitation de Windows hello.


## <a name="what-is-a-recovery-services-vault"></a>Présentation d’un coffre Recovery Services
Un coffre Recovery Services est qu'une entité de stockage en ligne dans Azure utilisé toohold des données telles que des copies de sauvegarde, les points de récupération et les stratégies de sauvegarde. Vous pouvez utiliser les Services de récupération des coffres toohold les données de sauvegarde pour les stations de travail et des serveurs locaux et des services Windows Azure. Archivages de Recovery Services rendent facile tooorganize vos données de sauvegarde, tout en réduisant les frais de gestion. Vous pouvez créer autant de coffres Recovery Services que vous le souhaitez au sein d’un abonnement.

Coffres de sauvegarde, qui sont basés sur le Gestionnaire des services Azure, ont été hello première version de coffre de hello. Coffres des Services de récupération, qui ajoutent des fonctionnalités de modèle Azure Resource Manager hello, sont hello deuxième version du coffre de hello. Consultez hello [article de vue d’ensemble du coffre Recovery Services](backup-azure-recovery-services-vault-overview.md) pour obtenir une description complète des différences de fonctionnalités hello. Vous ne pouvez plus créer toocreate de portail utilisez hello coffres de sauvegarde, mais les coffres de sauvegarde sont toujours gérées.

> [!IMPORTANT]
> Vous pouvez maintenant mettre à niveau vos archivages de sauvegarde coffres tooRecovery Services. Pour plus d’informations, voir l’article hello [mise à niveau d’un tooa de coffre de sauvegarde de coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft vous encourage tooupgrade coffres des Services tooRecovery les coffres de votre sauvegarde.<br/> **Le 15 octobre 2017**, vous ne pourra plus être coffres de sauvegarde toocreate toouse en mesure de PowerShell. <br/> **D’ici au 1er novembre 2017** :
>- Les coffres de sauvegarde restants seront les coffres des Services de tooRecovery automatiquement mis à niveau.
>- Vous ne pourra plus être en mesure de tooaccess vos données de sauvegarde dans le portail classique de hello. Au lieu de cela, utilisez hello tooaccess portail Azure vos données de sauvegarde dans les coffres des Services de récupération.
>

## <a name="how-does-azure-backup-differ-from-azure-site-recovery"></a>Quelle est la différence entre Azure Backup et Azure Site Recovery ?
La sauvegarde Azure Backup et Azure Site Recovery sont liés dans la mesure où les deux services sauvegardent les données et peuvent les restaurer. Toutefois, ces services ont des objectifs différents en assurant la continuité d’activité et la récupération d’urgence dans votre entreprise. Utiliser Azure Backup tooprotect et restaurer des données à un niveau plus granulaire. Par exemple, si une présentation sur un ordinateur portable a été endommagée, vous utiliseriez présentation de Azure Backup toorestore hello. Si vous souhaitiez tooreplicate hello données de configuration et sur une machine virtuelle dans un autre centre de données, utilisez Azure Site Recovery.

Sauvegarde Azure protège les données en local et dans le cloud de hello. Azure Site Recovery coordonne la réplication, le basculement et la restauration automatique des machines virtuelles et des serveurs physiques. Les deux services sont importantes, car votre solution de récupération d’urgence doit tookeep vos données sûre et récupérables (sauvegarde) *et* conserver vos charges de travail disponibles (récupération de Site), cas de panne.

Hello suivant concepts peut vous aider à prendre des décisions importantes autour de sauvegarde et récupération d’urgence.

| Concept | Détails | Sauvegarde | Récupération d’urgence |
| --- | --- | --- | --- |
| Objectif de point de récupération (RPO) |quantité Hello acceptable de perte de données si une récupération doit toobe terminé. |Les solutions de sauvegarde offrent des RPO extrêmement variables. Les sauvegardes de machines virtuelles ont généralement un RPO d’un jour, contre seulement 15 minutes pour les sauvegardes de base de données. |Les solutions de récupération d’urgence ont un RPO faible. Hello copie de la récupération d’urgence peut être derrière en quelques secondes à quelques minutes. |
| Objectif de délai de récupération (RTO) |Hello durée nécessaire toocomplete une récupération ou restauration. |En raison de hello RPO plus grande quantité hello de données qu’une solution de sauvegarde doit tooprocess est généralement beaucoup plus important, ce qui aboutit toolonger RTO. Par exemple, il peut prendre des jours toorestore des données à partir de bandes, en fonction de hello temps bande de hello tootransport à partir d’un emplacement hors site. |Solutions de récupération d’urgence ont RTO plus petites, car ils ne sont plus synchronisés avec la source de hello. Moins de modifications doivent toobe traité. |
| Rétention |La durée pendant laquelle les données doivent toobe stockée |Pour les scénarios qui exigent une reprise des opérations (altération des données, suppression accidentelle de fichiers, défaillances du système d’exploitation), les données de sauvegarde sont généralement conservées pendant 30 jours au maximum.<br>Du point de vue de la conformité, toobe stockée pour les mois, voire des années est nécessaire aux données. Dans ce cas, les données de sauvegarde sont parfaitement adaptées aux besoins d’archivage. |Récupération d’urgence doit uniquement les données de récupération opérationnelle, qui prend généralement quelques heures ou des jours de tooa. En raison de la capture de données affinées hello utilisée dans les solutions de récupération d’urgence à l’aide des données de récupération d’urgence pour une rétention à long terme n’est pas recommandé. |

## <a name="next-steps"></a>Étapes suivantes
Utilisez une des hello suivant des didacticiels pour obtenir des instructions pas à pas, pour la protection des données sur Windows Server, ou la protection d’un ordinateur virtuel (VM) dans Azure :

* [Sauvegarde des fichiers et dossiers](backup-try-azure-backup-in-10-mins.md)
* [Sauvegarde des machines virtuelles Azure](backup-azure-vms-first-look-arm.md)

Pour plus d’informations sur la protection des autres charges de travail, consultez l’un des articles suivants :

* [Sauvegarder Windows Server](backup-configure-vault.md)
* [Sauvegarder les charges de travail des applications](backup-azure-microsoft-azure-backup.md)
* [Sauvegarde des machines virtuelles IaaS Azure](backup-azure-vms-prepare.md)

[green]: ./media/backup-introduction-to-azure-backup/green.png
[yellow]: ./media/backup-introduction-to-azure-backup/yellow.png
[red]: ./media/backup-introduction-to-azure-backup/red.png
