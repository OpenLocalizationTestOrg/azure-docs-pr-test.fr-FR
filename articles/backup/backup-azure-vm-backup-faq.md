---
title: aaaAzure Forum aux questions de sauvegarde de machine virtuelle | Documents Microsoft
description: "Réponses aux questions de toocommon sur : comment les travaux de sauvegarde de machine virtuelle Azure, limitations et ce qui se produit lorsque toopolicy des modifications se produisent"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "sauvegarde de la machine virtuelle azure, restauration de la machine virtuelle azure, stratégie de sauvegarde"
ms.assetid: c4cd7ff6-8206-45a3-adf5-787f64dbd7e1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: a1ad2cb3a379577a8c4258c8207ce75809e11a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-vm-backup-service"></a>Questions sur hello service de sauvegarde de machine virtuelle Azure
Cet article contient des réponses toocommon questions toohelp vous comprenez rapidement les composants de sauvegarde de machine virtuelle Azure hello. Dans certaines des réponses de hello, sont des articles de toohello des liens qui ont des informations complètes. Vous pouvez également poser des questions sur hello service Azure Backup Bonjour [forum de discussion](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="configure-backup"></a>Configurer une sauvegarde
### <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>Les coffres Recovery Services prennent-ils en charge les machines virtuelles Azure Classic ou Resource Manager ? <br/>
Les coffres Recovery Services prennent en charge les deux modèles.  Vous pouvez sauvegarder une VM classique (créé dans le portail classique de hello) ou un tooa VM Gestionnaire de ressources (créé dans hello portail Azure) de coffre Recovery Services.

### <a name="what-configurations-are-not-supported-by-azure-vm-backup-"></a>Quelles configurations ne sont pas prises en charge par la sauvegarde de machine virtuelle Azure ?
Consultez [Systèmes d’exploitation pris en charge](backup-azure-arm-vms-prepare.md#supported-operating-system-for-backup) et [Limitations des sauvegardes de machine virtuelle](backup-azure-arm-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)

### <a name="why-cant-i-see-my-vm-in-configure-backup-wizard"></a>Pourquoi je ne peux pas voir ma machine virtuelle dans l’assistant de configuration de la sauvegarde ?
Dans l’assistant de configuration de la sauvegarde, Azure Backup répertorie uniquement les machines virtuelles qui sont :
* Pas encore protégé - vous pouvez vérifier état hello de la sauvegarde d’une machine virtuelle en sélectionnant tooVM lame et de vérification sur l’état de la sauvegarde à partir du Menu Paramètres du Panneau de hello. En savoir plus sur la façon de trop[vérifier l’état de la sauvegarde d’une machine virtuelle](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-vm-management-blade)
* Appartient toosame région en tant que machine virtuelle

## <a name="backup"></a>Sauvegarde
### <a name="will-on-demand-backup-job-follow-same-retention-schedule-as-scheduled-backups"></a>Est-ce qu’un travail de sauvegarde à la demande suit le même planning de rétention que les autres sauvegardes planifiées ?
Non. Vous avez besoin de durée de rétention toospecify hello pour une opération de sauvegarde à la demande. Par défaut, il sera conservé pendant 30 jours s’il a été déclenché à partir du portail. 

### <a name="i-recently-enabled-azure-disk-encryption-on-some-vms-will-my-backups-continue-toowork"></a>J’ai récemment activé Azure Disk Encryption sur certaines machines virtuelles. Mes sauvegardes continueront toowork ?
Vous devez disposer des autorisations de toogive pour Azure Backup service tooaccess le coffre de clés. Vous pouvez fournir ces autorisations dans PowerShell à l’aide des étapes présentées dans la section *Sauvegarde des machines virtuelles Azure* de la documentation [PowerShell](backup-azure-vms-automation.md).

### <a name="i-migrated-disks-of-a-vm-toomanaged-disks-will-my-backups-continue-toowork"></a>Migration des disques des disques d’un ordinateur virtuel toomanaged. Mes sauvegardes continueront toowork ?
Oui, les sauvegardes fonctionnent de façon transparente et sans nécessité toore-configurer la sauvegarde. 

## <a name="restore"></a>Restauration
### <a name="how-do-i-decide-between-restoring-disks-versus-full-vm-restore"></a>Comment choisir entre la restauration des disques et la restauration complète de la machine virtuelle ?
Vous devez considérer la restauration complète de la machine virtuelle Azure comme une manière rapide de créer une option pour la machine virtuelle restaurée. Restaurer la machine virtuelle option modifie les noms de disques hello, conteneurs utilisés par les disques, les adresses IP publiques, interface réseau noms pour l’unicité de ressources créé dans le cadre de la création d’ordinateurs virtuels. Il ajoutera également pas hello VM tooavailability ensemble. 

Utilisez des disques de restauration pour :
* Personnaliser hello machine virtuelle qui est créée à partir du point de configuration du temps comme la modification de la taille de hello à partir de la configuration de la sauvegarde
* Ajouter des configurations qui ne sont pas présentes au moment de hello de sauvegarde 
* Contrôle hello de convention d’affectation de noms de ressources créé
* Ajouter la machine virtuelle tooavailability ensemble
* Vous disposez de n’importe quelle configuration pouvant être obtenue uniquement à l’aide de PowerShell/d’une définition de modèle déclaratif

## <a name="manage-vm-backups"></a>Gérer les sauvegardes de machine virtuelle
### <a name="what-happens-when-i-change-a-backup-policy-on-vms"></a>Que se passe-t-il lorsque je modifie une stratégie de sauvegarde sur des machines virtuelles ?
Lorsqu’une nouvelle stratégie est appliquée sur les machines virtuelles, planification et rétention de la stratégie de nouvelle hello de suivi. Si la rétention est étendue, les points de récupération existants seront marquées tookeep leur en fonction de la nouvelle stratégie. Si la rétention est réduite, ils sont marqués pour le nettoyage de la prochaine tâche de nettoyage hello et seront supprimés. 
