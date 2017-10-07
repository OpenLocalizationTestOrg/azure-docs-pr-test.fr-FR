---
title: aaaAzure Forum aux questions de sauvegarde | Documents Microsoft
description: "Réponses aux questions de toocommon sur : fonctionnalités de sauvegarde Azure, y compris les Services de récupération des coffres, qu’il peut sauvegarder, son fonctionnement, le chiffrement et limites. "
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "sauvegarde et récupération d’urgence ; service de sauvegarde"
ms.assetid: 1011bdd6-7a64-434f-abd7-2783436668d7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/21/2017
ms.author: markgal;arunak;trinadhk;
ms.openlocfilehash: 3338f7620bcc6ebf53c9c161191f2d8bca1a29da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-backup-service"></a>Questions sur hello service Azure Backup
Cet article contient des réponses toocommon questions toohelp vous comprenez rapidement les composants d’Azure Backup hello. Dans certaines des réponses de hello, sont des articles de toohello des liens qui ont des informations complètes. Vous pouvez poser des questions sur Azure Backup en cliquant sur **commentaires** (toohello à droite). Commentaires s’affichent en bas de hello de cet article. Un compte de Livefyre est toocomment requis. Vous pouvez également poser des questions sur hello service Azure Backup Bonjour [forum de discussion](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

sections de hello analyse tooquickly dans cet article, utilisez droite hello liens toohello sous **dans cet article**.


## <a name="recovery-services-vault"></a>Coffre Recovery Services

### <a name="is-there-any-limit-on-hello-number-of-vaults-that-can-be-created-in-each-azure-subscription-br"></a>Existe-t-il un nombre hello de coffres qui peuvent être créés dans chaque abonnement Azure ? <br/>
Oui. Depuis septembre 2016, vous pouvez créer 25 coffres Recovery Services ou de sauvegarde par abonnement. Vous pouvez créer des Services de récupération too25 coffres, par région prise en charge de la sauvegarde de Azure, par abonnement. Au-delà, créez un autre abonnement.

### <a name="are-there-limits-on-hello-number-of-serversmachines-that-can-be-registered-against-each-vault-br"></a>Existe-t-il des limites de nombre hello de serveurs/ordinateurs, ce qui peut être inscrit par rapport à chaque coffre ? <br/>
Oui, vous pouvez inscrire des ordinateurs too50 par coffre. Pour les machines virtuelles Azure IaaS, limite de hello est de 200 machines virtuelles par coffre. Si vous devez tooregister plusieurs ordinateurs, créez un autre coffre.

### <a name="if-my-organization-has-one-vault-how-can-i-isolate-one-servers-data-from-another-server-when-restoring-databr"></a>Si mon organisation possède un coffre, comment isoler les données d’un serveur de celles d’un autre serveur lors de la restauration des données ?<br/>
Tous les serveurs qui sont inscrit toohello même coffre peut récupérer hello données sauvegardées par d’autres serveurs *qui utilisent hello même phrase secrète*. Si vous avez des serveurs dont les données de sauvegarde souhaitée tooisolate à partir d’autres serveurs de votre organisation, utilisez un mot de passe désigné pour ces serveurs. Par exemple, les serveurs des ressources humaines peuvent utiliser une phrase secrète de chiffrement, les serveurs de comptabilité peuvent en utiliser une autre et les serveurs de stockage une troisième.

### <a name="can-i-migrate-my-backup-data-or-vault-between-subscriptions-br"></a>Puis-je « migrer » mon coffre ou mes données de sauvegarde entre des abonnements ? <br/>
Non. coffre de Hello est créé au niveau de l’abonnement et ne peut pas être réassigné tooanother abonnement qui a été créé.

### <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a>Les coffres Recovery Services sont basés sur Resource Manager. Les coffres Azure Backup (mode Classic) sont-ils toujours gérés ? <br/>
Tous les archivages de sauvegarde existants Bonjour [portail classique](https://manage.windowsazure.com) continuer toobe pris en charge. Toutefois, vous pouvez utiliser n’est plus les coffres de sauvegarde nouvelle hello toodeploy portail classique. Microsoft recommande d’utiliser les coffres des Services de récupération pour tous les déploiements, car les améliorations ultérieures s’appliquent tooRecovery les coffres des Services, uniquement. Si vous essayez de toocreate un coffre de sauvegarde dans le portail classique de hello, vous serez redirigé toohello [portail Azure](https://portal.azure.com).

### <a name="can-i-migrate-a-backup-vault-tooa-recovery-services-vault-br"></a>Puis-je migrer un coffre de sauvegarde coffre tooa Services de récupération ? <br/>
Malheureusement, non, ne peut pas migrer hello contenu d’un tooa de coffre de sauvegarde de coffre Recovery Services. Nous travaillons sur l’ajout de cette fonctionnalité, mais elle n’est pas disponible actuellement.

### <a name="i-backed-up-my-classic-vms-in-a-backup-vault-can-i-migrate-my-vms-from-classic-mode-tooresource-manager-mode-and-protect-them-in-a-recovery-services-vault"></a>J’ai sauvegardé mes machines virtuelles classiques dans un coffre de sauvegarde Azure. Puis-je migrer mes machines virtuelles à partir du mode de gestionnaire tooResource en mode classique et les protéger dans un coffre Recovery Services ?
Classiques points de récupération de machine virtuelle dans un coffre de sauvegarde ne faire migrer automatiquement le coffre Recovery Services tooa lorsque vous déplacez hello VM de tooResource classique en mode de gestionnaire. Suivez ces étapes tootransfer vos sauvegardes de machine virtuelle :

1. Dans le coffre de sauvegarde hello, accédez à toohello **éléments protégés** onglet et sélectionnez hello machine virtuelle. Cliquez sur [Arrêter la protection](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). Laissez l’option *Supprimer les données de sauvegarde associées***non cochée**.
2. Suppression de l’extension de sauvegarde/capture instantanée hello à partir de la machine virtuelle de hello.
3. Migrer hello virtual machine du mode de gestionnaire tooResource en mode classique. Assurez-vous que les informations réseau et de stockage hello machine virtuelle de toohello correspondante est également migrées dans le mode de gestionnaire tooResource.
4. Créer un coffre Recovery Services et configurer sauvegarde sur hello migrés à l’aide de l’ordinateur virtuel **sauvegarde** action au-dessus du tableau de bord coffre. Pour plus d’informations sur la sauvegarde d’une machine virtuelle tooa Recovery Services coffre, consultez l’article hello, [protéger des machines virtuelles Azure dans un coffre Recovery Services](backup-azure-vms-first-look-arm.md).

## <a name="azure-backup-agent"></a>Agent Azure Backup
Liste détaillée des questions présentes dans le [Forum aux questions sur la sauvegarde de fichiers-dossiers Azure](backup-azure-file-folder-backup-faq.md)

## <a name="azure-vm-backup"></a>Sauvegarde des machines virtuelles Azure
Liste détaillée des questions présentes dans le [Forum aux questions sur la sauvegarde des machines virtuelles Azure](backup-azure-vm-backup-faq.md)

## <a name="back-up-vmware-servers"></a>Sauvegarder des serveurs VMware

### <a name="can-i-back-up-vmware-vcenter-servers-tooazure"></a>Puis-je sauvegarder tooAzure de serveurs VMware vCenter ?

Oui. Vous pouvez utiliser tooback Azure Backup Server VMware vCenter et ESXi tooAzure. Pour plus d’informations sur la version de VMware hello pris en charge, consultez l’article hello, [matrice de protection d’Azure Backup Server](backup-mabs-protection-matrix.md). Pour obtenir des instructions, consultez [tooback utilisez Azure Backup Server d’un serveur VMware](backup-azure-backup-server-vmware.md).


## <a name="azure-backup-server-and-system-center-data-protection-manager"></a>Microsoft Azure Backup et System Center Data Protection Manager
### <a name="can-i-use-azure-backup-server-toocreate-a-bare-metal-recovery-bmr-backup-for-a-physical-server-br"></a>Puis-je utiliser Azure Backup Server toocreate une sauvegarde Bare Metal Recovery (BMR) pour un serveur physique ? <br/>
Oui.

### <a name="can-i-register-my-dpm-server-toomultiple-vaults-br"></a>Puis-je enregistrer mes coffres-forts toomultiple de serveur DPM ? <br/>
Non. Un serveur DPM ou MABS peut être tooonly inscrit un coffre.

### <a name="which-version-of-system-center-data-protection-manager-is-supported-br"></a>Quelle version de System Center Data Protection Manager est prise en charge ? <br/>
Nous vous recommandons d’installer hello [dernière](http://aka.ms/azurebackup_agent) Azure Backup agent hello dernier correctif cumulatif (UR) pour System Center Data Protection Manager (DPM). À partir d’août 2016, 11 de cumul de mettre à jour est la dernière mise à jour de hello.

### <a name="i-have-installed-azure-backup-agent-tooprotect-my-files-and-folders-can-i-now-install-system-center-dpm-toowork-with-azure-backup-agent-tooprotect-on-premises-applicationvm-workloads-tooazure-br"></a>J’ai installé Azure Backup agent tooprotect mes fichiers et des dossiers. Puis-je installer maintenant des toowork de System Center DPM avec Azure Backup agent tooprotect local application/des charges de travail tooAzure ? <br/>
toouse Azure Backup avec System Center Data Protection Manager (DPM), d’abord installer DPM, puis installez l’agent Azure Backup. Installation des composants de sauvegarde Azure hello dans cet ordre garantit l’agent de sauvegarde Azure hello fonctionne avec DPM. Lors de l’installation Bonjour Azure Backup agent avant l’installation de DPM n’est pas recommandé ou pris en charge.


## <a name="how-azure-backup-works"></a>Fonctionnement de la sauvegarde Azure
### <a name="if-i-cancel-a-backup-job-once-it-has-started-is-hello-transferred-backup-data-deleted-br"></a>Si vous annulez un travail de sauvegarde une fois qu’il a démarré, sont hello transféré les données de sauvegarde supprimées ? <br/>
Non. Toutes les données transférées dans le coffre de hello, avant l’annulation d’une tâche de sauvegarde hello, restent dans le coffre hello. Azure utilise sauvegarde un toooccasionally de mécanisme de point de contrôle ajouter des données de sauvegarde toohello des points de contrôle pendant hello sauvegarde. Étant donné que les points de contrôle dans les données de sauvegarde hello, processus de sauvegarde suivant hello peut valider l’intégrité de hello des fichiers de hello. travail de sauvegarde suivant Hello sera toohello incrémentielle les données précédemment sauvegardées. Les sauvegardes incrémentielles transfèrent uniquement les données nouvelles ou modifiées, ce qui équivaut toobetter taux d’utilisation de la bande passante.

Si vous annulez une tâche de sauvegarde pour une machine virtuelle Azure, toutes les données transférées sont ignorées. travail de sauvegarde suivant Hello transfère des données incrémentielles à partir de la dernière tâche réussie a sauvegarde hello.

### <a name="are-there-limits-on-when-or-how-many-times-a-backup-job-can-be-scheduledbr"></a>Existe-t-il des limites concernant le moment et le nombre de fois durant lesquels une opération de sauvegarde peut être planifiée chaque jour ?<br/>
Oui. Vous pouvez exécuter des travaux de sauvegarde sur Windows Server ou les stations de travail Windows des toothree heures / jour. Vous pouvez exécuter les travaux de sauvegarde sur System Center DPM tootwice quotidiennement. Vous pouvez exécuter une tâche de sauvegarde pour les machines virtuelles IaaS une fois par jour. Vous pouvez utiliser hello stratégie de planification pour Windows Server ou Windows workstation toospecify planifications quotidienne ou hebdomadaire. Avec System Center DPM, vous pouvez spécifier des planifications quotidiennes, hebdomadaires, mensuelles et annuelles.

### <a name="why-is-hello-size-of-hello-data-transferred-toohello-recovery-services-vault-smaller-than-hello-data-i-backed-upbr"></a>Pourquoi est-taille hello de toohello de données transférées hello de coffre de Services de récupération est plus petit que les données de salutation sauvegardées ?<br/>
 Toutes les données de hello sauvegardées à partir de l’Agent Azure Backup ou SCDPM ou serveur de sauvegarde Azure, sont compressées et chiffrées avant d’être transférées. Une fois que le chiffrement et la compression de hello est appliqué, données hello dans le coffre de sauvegarde hello sont inférieure à 30 à 40 %.

## <a name="what-can-i-back-up"></a>Que puis-je sauvegarder ?
### <a name="which-operating-systems-do-azure-backup-support-br"></a>Quels systèmes d’exploitation la sauvegarde Azure prend-elle en charge ? <br/>
Sauvegarde Azure prend en charge hello suivant de la liste des systèmes d’exploitation pour la sauvegarde : fichiers et dossiers et les applications de la charge de travail protégées à l’aide d’Azure Backup Server et System Center Data Protection Manager (DPM).

| Système d’exploitation | Plateforme | SKU |
|:--- | --- |:--- |
| Windows 8 et derniers Service Packs |64 bits |Entreprise, Professionnel |
| Windows 7 et derniers Service Packs |64 bits |Édition Intégrale, Entreprise, Professionnel, Édition Familiale Premium, Édition Familiale Basique, Édition Starter |
| Windows 8.1 et derniers Service Packs |64 bits |Entreprise, Professionnel |
| Windows 10 |64 bits |Entreprise, Professionnel, Familiale |
| Windows Server 2016 |64 bits |Standard, Datacenter, Essentials |
| Windows Server 2012 R2 et derniers Service Packs |64 bits |Standard, Datacenter, Foundation |
| Windows Server 2012 et derniers Service Packs |64 bits |Datacenter, Foundation, Standard |
| Windows Storage Server 2016 et derniers Service Packs |64 bits |Standard, Workgroup | 
| Windows Storage Server 2012 R2 et derniers Service Packs |64 bits |Standard, Workgroup |
| Windows Storage Server 2012 et derniers Service Packs |64 bits |Standard, Workgroup |
| Windows Server 2012 R2 et derniers Service Packs |64 bits |Essential |
| Windows Server 2008 R2 SP1 |64 bits |Standard, Entreprise, Datacenter, Foundation |
| Windows Server 2008 SP2 |64 bits |Standard, Entreprise, Datacenter, Foundation |

**Pour la sauvegarde de machines virtuelles Azure :**

* **Linux**: Azure Backup prend en charge [une liste de distributions approuvées par Azure](../virtual-machines/linux/endorsed-distros.md) , à l’exception de CoreOS Linux.  Autres Bring-Your-propriétaire-distributions Linux peuvent également fonctionner tant que l’agent de machine virtuelle hello est disponible sur l’ordinateur virtuel de hello et prise en charge de Python existe.
* **Windows Server** : les versions antérieures à Windows Server 2008 R2 ne sont pas prises en charge.


### <a name="is-there-a-limit-on-hello-size-of-each-data-source-being-backed-up-br"></a>Existe-t-il une limite de taille de hello de chaque source de données en cours de sauvegarde ? <br/>
Il n’existe aucune limite de quantité hello de données, que vous pouvez sauvegarder tooa coffre. Sauvegarde Azure limite la taille maximale de hello pour la source de données hello, toutefois, ces limites sont volumineuses. Depuis août 2015, taille maximale de hello pour une source de données pour les systèmes d’exploitation pris en charge de hello est :

| N° | Système d’exploitation | Taille maximale de la source de données |
|:---:|:--- |:--- |
| 1 |Windows Server 2012 ou version ultérieure |54 400 Go |
| 2 |Windows 8 ou version ultérieure |54 400 Go |
| 3 |Windows Server 2008, Windows Server 2008 R2 |1 700 Go |
| 4 |Windows 7 |1 700 Go |

Hello tableau suivant explique la manière dont la taille de chaque source de données est déterminé.

| Source de données | Détails |
|:---:|:--- |
| Volume |quantité de Hello de données sauvegardées à partir d’un volume unique d’un ordinateur client ou serveur |
| Machine virtuelle Hyper-V |Somme des données de tous les disques durs virtuels de hello de machine virtuelle de hello en cours de sauvegarde |
| Base de données Microsoft SQL Server |Taille d’une base de données SQL unique en cours de sauvegarde |
| Microsoft SharePoint |Somme des bases de données hello contenu et de configuration dans une batterie de serveurs SharePoint en cours de sauvegarde |
| Microsoft Exchange |Somme de toutes les bases de données Exchange sur un serveur Exchange en cours de sauvegarde |
| État système/récupération complète |Chaque copie individuelle de la récupération complète ou état du système d’ordinateur hello en cours de sauvegarde |

Pour la sauvegarde de la machine virtuelle Azure, chaque machine virtuelle peut avoir des disques de données too16 chaque disque de données étant de taille de 1 023 Go ou moins. 

## <a name="retention-policy-and-recovery-points"></a>Stratégie de rétention et points de récupération
### <a name="is-there-a-difference-between-hello-retention-policy-for-dpm-and-windows-serverclient-that-is-on-windows-server-without-dpmbr"></a>Y a-t-il une différence entre la stratégie de rétention de hello pour DPM et client Windows Server (autrement dit, sur Windows Server sans DPM) ?<br/>
Non, DPM et le serveur/client Windows Server répondent tous les deux à des stratégies quotidienne, hebdomadaire, mensuelle et annuelle de rétention.

### <a name="can-i-configure-my-retention-policies-selectively--ie-configure-weekly-and-daily-but-not-yearly-and-monthlybr"></a>Puis-je configurer mes stratégies de rétention de manière sélective (par exemple, configurer des stratégies hebdomadaires et quotidiennes, mais pas annuelles et mensuelles) ?<br/>
Oui, hello structure de rétention de sauvegarde Azure permet une souplesse totale de toohave dans la définition de stratégie de rétention hello conformément à vos besoins.

### <a name="can-i-schedule-a-backup-at-6pm-and-specify-retention-policies-at-a-different-timebr"></a>Puis-je « planifier une sauvegarde » à 18 h 00 et spécifier des stratégies de rétention à une autre heure ?<br/>
Non. Les stratégies de rétention ne peuvent être appliquées que sur les points de sauvegarde. Bonjour suivant image, stratégie de rétention hello est spécifié pour les sauvegardes effectuées à 0 h 00 et 18 h 00. <br/>

![Planification de sauvegarde et rétention](./media/backup-azure-backup-faq/Schedule.png)
<br/>

### <a name="if-a-backup-is-retained-for-a-long-duration-does-it-take-more-time-toorecover-an-older-data-point-br"></a>Si une sauvegarde est conservée pendant une longue durée, faut-il toorecover de temps plus d’un point de données plus anciens ? <br/>
Non – heure hello toorecover hello plus ancien ou hello plus récent point est hello même. Chaque point de récupération se comporte comme un point complet.

### <a name="if-each-recovery-point-is-like-a-full-point-does-it-impact-hello-total-billable-backup-storagebr"></a>Si chaque point de récupération est comme un point plein, est son impact sur stockage de sauvegarde facturables total hello ?<br/>
Les produits avec points de rétention à long terme stockent les données de sauvegarde en tant que points complets. points complète de Hello sont stockage *inefficace* , mais il est plus facile et plus rapide toorestore. Copies incrémentielles sont stockage *efficace* mais nécessitent que vous toorestore une chaîne de données, ce qui a un impact sur le temps de récupération. Azure propose sauvegarde de stockage architecture hello de meilleur des deux mondes par le stockage des données pour les restaurations rapides optimal et de subir des frais de stockage faible. Cette approche de stockage de données garantit que votre bande passante entrante et sortante est utilisée de façon efficace. La durée de hello hello et stockage de données nécessaires des données de salutation toorecover, est conservée tooa minimale. En savoir plus sur l’efficacité des [sauvegardes incrémentielles](https://azure.microsoft.com/blog/microsoft-azure-backup-save-on-long-term-storage/).

### <a name="is-there-a-limit-on-hello-number-of-recovery-points-that-can-be-createdbr"></a>Existe-t-il une limite du nombre de hello de points de récupération qui peut être créé ?<br/>
Vous pouvez créer des points de récupération too9999 par instance protégée. Une instance protégée est un ordinateur, serveur (physique ou virtuel) ou tooback de charge de travail configuré des données tooAzure. Pour plus d’informations, consultez explications hello [sauvegarde et rétention](./backup-introduction-to-azure-backup.md#backup-and-retention), et [ce qui est une instance protégée](./backup-introduction-to-azure-backup.md#what-is-a-protected-instance)?

### <a name="how-many-recoveries-can-i-perform-on-hello-data-that-is-backed-up-tooazurebr"></a>Récupérations combien puis-je effectuer sur les données hello sauvegardées tooAzure ?<br/>
Il n’existe aucune limite du nombre de hello de récupérations à partir d’Azure Backup.

### <a name="when-restoring-data-do-i-pay-for-hello-egress-traffic-from-azure-br"></a>Lors de la restauration des données, suis-je facturé pour le trafic sortant hello à partir d’Azure ? <br/>
Non. Votre récupérations sont gratuites et vous n’êtes pas facturé pour le trafic sortant hello.

## <a name="azure-backup-encryption"></a>Chiffrement de sauvegarde Azure
### <a name="is-hello-data-sent-tooazure-encrypted-br"></a>Sont-ce que les données hello envoyées tooAzure chiffré ? <br/>
Oui. Données sont chiffrées sur l’ordinateur de client/serveur/SCDPM hello local à l’aide de AES256 et les données hello sont envoyées via une connexion HTTPS sécurisée.

### <a name="is-hello-backup-data-on-azure-encrypted-as-wellbr"></a>Est des données de sauvegarde hello sur Azure chiffré également ?<br/>
Oui. envoyer des données de Hello tooAzure reste chiffrée (au repos). Microsoft ne déchiffre pas les données de sauvegarde hello à tout moment. Lorsque vous sauvegardez une machine virtuelle Azure, Azure Backup s’appuie sur le chiffrement de la machine virtuelle de hello. Par exemple, si votre machine virtuelle est chiffrée à l’aide du chiffrement de disque Azure, ou une autre technologie de chiffrement, Azure Backup utilise ce toosecure chiffrement vos données.

### <a name="what-is-hello-minimum-length-of-encryption-key-used-tooencrypt-backup-data-br"></a>Quelle est la longueur minimale de hello de clé de chiffrement utilisée tooencrypt les données de sauvegarde ? <br/>
clé de chiffrement Hello doit être au moins 16 caractères lorsque vous utilisez l’agent de sauvegarde Azure. Pour les machines virtuelles Azure, il n’existe aucun toolength limite de clés utilisées par Azure KeyVault. 

### <a name="what-happens-if-i-misplace-hello-encryption-key-can-i-recover-hello-data-or-can-microsoft-recover-hello-data-br"></a>Que se passe-t-il si j’ai égaré la clé de chiffrement hello ? Puis-je récupérer des données de hello (ou) Microsoft peut récupérer les données de hello ? <br/>
données de sauvegarde Hello clé tooencrypt utilisé hello sont présentes uniquement sur les locaux du client hello. Microsoft ne conserve pas une copie dans Azure et n’a pas de n’importe quelle touche de toohello d’accès. Si le client de hello égare clé de hello, Microsoft ne peut pas récupérer les données de sauvegarde hello.
