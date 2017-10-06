---
title: aaaOverview des archivages de Recovery Services | Documents Microsoft
description: "Vue d’ensemble et comparaison entre les coffres Recovery Services et les coffres de sauvegarde Azure."
services: backup
documentationcenter: " "
author: markgalioto
manager: carmonm
ms.assetid: 38d4078b-ebc8-41ff-9bc8-47acf256dc80
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/15/2017
ms.author: markgal;arunak
ms.openlocfilehash: 77dd9ece7fe86429cc6f9a47a68b5150a1f4af71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="recovery-services-vaults-overview"></a>Vue d’ensemble des coffres Recovery Services

Cet article décrit les fonctionnalités de hello d’un coffre Recovery Services. Un coffre Recovery Services est une entité de stockage dans Azure qui héberge des données. les données de salutation sont généralement des copies de données ou des informations de configuration pour les machines virtuelles (VM), les charges de travail, serveurs ou stations de travail. Un coffre Recovery Services est la version du Gestionnaire de ressources hello d’un coffre de sauvegarde. Microsoft vous encourage les coffres des Services de récupération toouse et tooconvert les coffres des Services de tooRecovery les coffres de n’importe quelle sauvegarde.

## <a name="what-is-a-recovery-services-vault"></a>Présentation d’un coffre Recovery Services

Un coffre Recovery Services est qu'une entité de stockage en ligne dans Azure utilisé toohold des données telles que des copies de sauvegarde, les points de récupération et les stratégies de sauvegarde. Vous pouvez utiliser les Services de récupération des coffres toohold les données de sauvegarde pour différents services Azure tels que les machines virtuelles IaaS de (Windows ou Linux) et les bases de données SQL Azure. Les coffres Recovery Services prennent en charge System Center DPM, Windows Server, le serveur de sauvegarde Azure et bien plus. Archivages de Recovery Services rendent facile tooorganize vos données de sauvegarde, tout en réduisant les frais de gestion.

Dans un abonnement Azure, vous pouvez créer autant de coffres Recovery Services que vous le souhaitez.

## <a name="comparing-recovery-services-vaults-and-backup-vaults"></a>Comparaison entre les coffres Recovery Services et les coffres de sauvegarde

Les coffres des Services de récupération sont basées sur le modèle du Gestionnaire de ressources Azure hello d’Azure, tandis que les coffres de sauvegarde sont basées sur le modèle de Service Manager de Azure hello. Lorsque vous mettez à niveau un coffre de sauvegarde coffre tooa Services de récupération, les données de sauvegarde hello restent intactes, pendant et après la mise à niveau de hello. Les coffres Recovery Services fournissent des fonctionnalités non disponibles pour les coffres de sauvegarde, telles que :

- **Des données de sauvegarde sécurisé de fonctionnalités toohelp améliorées**: les coffres de With Recovery Services, Azure Backup sécurise les sauvegardes en cloud tooprotect fonctionnalités. Ces fonctionnalités de sécurité vous garantissent de pouvoir sécuriser vos sauvegardes, et récupérer en toute sécurité des données à partir de sauvegardes cloud, même si des serveurs de production et de sauvegarde sont compromis. [En savoir plus](backup-azure-security-feature.md)

- **Surveillance centrale de votre environnement informatique hybride** : avec les coffres Recovery Services, vous pouvez surveiller non seulement vos [machines virtuelles IaaS Azure](backup-azure-manage-vms.md), mais aussi votre [ressources locales](backup-azure-manage-windows-server.md#manage-backup-items) à partir d’un portail centralisé. [En savoir plus](http://azure.microsoft.com/blog/alerting-and-monitoring-for-azure-backup)

- **Contrôle d’accès en fonction du rôle (RBAC)** : le RBAC offre un contrôle précis de la gestion des accès dans Azure. [Azure fournit plusieurs rôles intégrés](../active-directory/role-based-access-built-in-roles.md), et Azure Backup a trois [points de récupération de rôles intégrés toomanage](backup-rbac-rs-vault.md). Les coffres des Services de récupération sont compatibles avec RBAC, ce qui limite la sauvegarde et restaurer l’accès toohello défini des rôles d’utilisateur. [En savoir plus](backup-rbac-rs-vault.md)

- **Protéger toutes les configurations des machines virtuelles Azure** : les coffres Recovery Services protègent les machines virtuelles basées sur Resource Manager, notamment les disques Premium, les disques gérés et les machines virtuelles chiffrées. Un tooa de coffre de sauvegarde de la mise à niveau des Services de récupération de coffre permet de vous hello opportunité tooupgrade votre tooResource Service Manager sur des ordinateurs virtuels en fonction de gestionnaire de machines virtuelles. Lors de la mise à niveau de coffre de hello, vous pouvez conserver vos points de récupération d’ordinateurs virtuels Service Manager et configurer la protection pour hello mis à niveau (Gestionnaire de ressources-activé) de machines virtuelles. [En savoir plus](http://azure.microsoft.com/blog/azure-backup-recovery-services-vault-ga)

- **Restauration de machines virtuelles IaaS**: les coffres d’à l’aide des Services de récupération, vous pouvez restaurer les fichiers et dossiers à partir d’un IaaS VM sans restauration hello machine virtuelle entière, ce qui permet des temps de restauration plus rapides. La restauration instantanée de machines virtuelles IaaS est disponible pour les machines virtuelles Windows et Linux. [En savoir plus](http://azure.microsoft.com/blog/instant-file-recovery-from-azure-linux-vm-backup-using-azure-backup-preview)

## <a name="managing-your-recovery-services-vaults-in-hello-portal"></a>Gestion des coffres de vos Services de récupération dans le portail de hello
Il est facile de création et la gestion des archivages de Recovery Services Bonjour Azure portal car hello service de sauvegarde est intégré dans le panneau des paramètres Azure hello. Cette intégration signifie que vous pouvez créer ou gérer un coffre Recovery Services *dans le contexte de hello du service cible de hello*. Par exemple, des points de récupération de hello tooview pour une machine virtuelle, sélectionnez-le, puis cliquez sur **sauvegarde** dans le panneau des paramètres hello. toothat spécifique de Hello informations de sauvegarde la machine virtuelle s’affiche. Bonjour, l’exemple suivant **ContosoVM** est le nom hello de machine virtuelle de hello. **ContosoVM-demovault** hello désigne hello de coffre Recovery Services. Vous n’avez pas besoin nom de hello tooremember du coffre Recovery Services hello qui stocke les points de récupération hello, vous pouvez accéder à ces informations à partir de l’ordinateur virtuel de hello.  

![coffre recovery services, détails, machine virtuelle](./media/backup-azure-recovery-services-vault-overview/rs-vault-in-context.png)

Si plusieurs serveurs sont protégés à l’aide de hello coffre des mêmes Services de récupération, il se peut toolook plus logique à hello de coffre Recovery Services. Vous pouvez rechercher tous les archivages de Recovery Services dans l’abonnement de hello et choisissez une à partir de la liste de hello.

Hello sections suivantes contiennent des liens tooarticles qui expliquent comment toouse un Recovery Services coffre dans chaque type d’activité.

### <a name="back-up-data"></a>Sauvegarder des données
- [Sauvegarder une machine virtuelle Azure](backup-azure-vms-first-look-arm.md)
- [Sauvegarder des stations de travail Windows Server ou Windows](backup-try-azure-backup-in-10-mins.md)
- [Sauvegarder tooAzure de charges de travail DPM](backup-azure-dpm-introduction.md)
- [Préparer tooback des charges de travail à l’aide d’Azure Backup Server](backup-azure-microsoft-azure-backup.md)

### <a name="manage-recovery-points"></a>Gérer les points de récupération
- [Gérer les sauvegardes de machines virtuelles Azure](backup-azure-manage-vms.md)
- [Gestion des fichiers et dossiers](backup-azure-manage-windows-server.md)

### <a name="restore-data-from-hello-vault"></a>Restaurer les données d’archivage de hello
- [Récupérer des fichiers individuels d’une machine virtuelle Azure](backup-azure-restore-files-from-vm.md)
- [Restaurer une machine virtuelle Azure](backup-azure-arm-restore-vms.md)

### <a name="secure-hello-vault"></a>Coffre de hello sécurisé
- [Sécurisation des données de sauvegarde cloud dans des coffres Recovery Services](backup-azure-security-feature.md)



## <a name="next-steps"></a>Étapes suivantes
Utilisez hello article pour suivant :</br>
[Sauvegarder une machine virtuelle IaaS](backup-azure-arm-vms-prepare.md)</br>
[Sauvegarder un serveur de sauvegarde Azure](backup-azure-microsoft-azure-backup.md)</br>
[Sauvegarder un serveur Windows Server](backup-configure-vault.md)
