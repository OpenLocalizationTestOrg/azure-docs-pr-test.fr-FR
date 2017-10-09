---
title: "Forum aux questions de coffre de Services d’aaaRecovery | Documents Microsoft"
description: "Cette version de hello FAQ prend en charge la version préliminaire publique de hello Hello service Azure Backup. Elles en sonttrop de réponses aux questions sur l’agent de sauvegarde hello, sauvegarde et de rétention, récupération, sécurité et autres questions courantes sur hello solution de sauvegarde Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "solution de sauvegarde ; service de sauvegarde"
ms.assetid: 5f55b500-1ee9-4f64-9306-02d6f7a8eded
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/21/2016
ms.author: markgal;trinadhk;
ms.openlocfilehash: 882b2e67ed424dc9f3681a8870e6b4c7b4cdcaec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="recovery-services-vault---faq"></a>FAQ du coffre Recovery Services
Cet article fournit le coffre de Services spécifiques tooRecovery informations et il complète hello [Forum aux questions de sauvegarde Azure](backup-azure-backup-faq.md). Hello Forum aux questions de sauvegarde Azure fournit ensemble complet de hello de questions et réponses sur hello service Azure Backup.  

Vous pouvez poser des questions sur Azure Backup Bonjour section Disqus de cet article ou d’un article. Vous pouvez également poser des questions sur hello service Azure Backup Bonjour [forum de discussion](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a>Les coffres Recovery Services sont basés sur Resource Manager. Les coffres Azure Backup (mode Classic) sont-ils toujours gérés ? <br/>
Oui, les coffres Azure Backup sont toujours pris en charge. Créer des coffres de sauvegarde Bonjour [portal de classique](https://manage.windowsazure.com). Créer les coffres des Services de récupération Bonjour [portail Azure](https://portal.azure.com). Nous recommandons vivement de vous toocreate coffre recovery services en tant que toutes les futures améliorations sera toutefois disponible uniquement dans le coffre Recovery Services.

## <a name="can-i-migrate-a-backup-vault-tooa-recovery-services-vault-br"></a>Puis-je migrer un coffre de sauvegarde coffre tooa Services de récupération ? <br/>
Malheureusement, non, à ce stade ne peut pas migrer hello contenu d’un tooa de coffre de sauvegarde de coffre Recovery Services. Nous travaillons sur l’ajout de cette fonctionnalité, mais elle n’est pas disponible dans la version préliminaire publique.

## <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>Les coffres Recovery Services prennent-ils en charge les machines virtuelles Azure Classic ou Resource Manager ? <br/>
Les coffres Recovery Services prennent en charge les deux modèles.  Vous pouvez sauvegarder un ordinateur virtuel créé dans le portail classique de hello (qui sont des ordinateurs virtuels du mode classique), ou une machine virtuelle créée dans hello portail Azure (qui sont en fonction de gestionnaire de ressources) des Services de récupération tooa de coffre.

## <a name="i-have-backed-up-my-classic-vms-in-backup-vault-now-i-want-toomigrate-my-vms-from-classic-mode-tooresource-manager-mode--how-can-i-backup-them-in-recovery-services-vault"></a>J’ai sauvegardé mes machines virtuelles en mode Classic dans le coffre Azure Backup. Je souhaite maintenant toomigrate mes machines virtuelles à partir du mode de gestionnaire tooResource en mode classique.  Comment faire pour les sauvegarder dans le coffre Recovery Services ?
Sauvegardes de machines virtuelles de classiques dans le coffre de sauvegarde ne sera pas migrer automatiquement toorecovery services coffre lorsque vous migrez hello machines virtuelles de tooResource classique en mode de gestionnaire. Pour migrer des sauvegardes de machines virtuelles, procédez comme suit :

1. Dans le coffre de sauvegarde, accédez trop**éléments protégés** onglet et sélectionnez hello machine virtuelle. Cliquez sur [Arrêter la protection](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). Laissez l’option *Supprimer les données de sauvegarde associées***non cochée**.
2. Bonjour [portail Azure](https://portal.azure.com), accédez toohello **Extensions** menu hello VM et désinstaller hello **VMSnapshot/VMSnapshotLinux** extension.
3. Migrer hello virtual machine du mode de gestionnaire tooResource en mode classique. Assurez-vous que correspondant toovirtual machine de réseau et de stockage sont également migrés tooResource Manager mode.
4. Créer un coffre recovery services et configurer sauvegarde sur hello migrés à l’aide de l’ordinateur virtuel **sauvegarde** action au-dessus du tableau de bord coffre. En savoir plus sur la façon de trop[activer la sauvegarde dans le coffre recovery services](backup-azure-vms-first-look-arm.md)
