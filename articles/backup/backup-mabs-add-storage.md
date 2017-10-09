---
title: aaaUse le stockage de sauvegarde moderne avec Azure Backup Server v2 | Documents Microsoft
description: "En savoir plus sur les nouvelles fonctionnalités de hello dans Azure Backup Server v2. Cet article décrit comment tooupgrade votre installation du serveur de sauvegarde."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: b2a1ed27a6a682bd611fea1d2df9ef93314404e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-storage-tooazure-backup-server-v2"></a>Ajouter du stockage tooAzure v2 de sauvegarde du serveur

Le Serveur de sauvegarde Azure v2 est fourni avec le stockage de sauvegarde moderne du Data Protection Manager de System Center 2016. Le stockage de sauvegarde moderne offre des économies de stockage de 50 %, des sauvegardes trois fois plus rapides et un stockage plus efficace. Il s’agit également d’un stockage prenant en compte la charge de travail. 

> [!NOTE]
> toouse moderne le stockage de sauvegarde, vous devez exécuter v2 de sauvegarde du serveur sur Windows Server 2016. Si vous exécutez le Serveur de sauvegarde v2 sur une version antérieure de Windows Server, le Serveur de sauvegarde Azure ne peut pas tirer parti du stockage de sauvegarde moderne. Au lieu de cela, il protège les charges de travail comme il le fait avec le Serveur de sauvegarde v1. Pour plus d’informations, consultez la version du serveur de sauvegarde hello [matrice protection](backup-mabs-protection-matrix.md).

## <a name="volumes-in-backup-server-v2"></a>Volumes dans le Serveur de sauvegarde v2

Le Serveur de sauvegarde v2 accepte les volumes de stockage. Lorsque vous ajoutez un volume, serveur de sauvegarde met en forme hello volume tooResilient système de fichiers (ReFS), qui nécessite de stockage de sauvegarde moderne. tooadd un volume et tooexpand ultérieurement si vous le souhaitez, nous vous suggérons d’utiliser ce flux de travail :

1.  Configurez le Serveur de sauvegarde v2 sur une machine virtuelle.
2.  Créez un volume sur un disque virtuel dans un pool de stockage :
    1.  Ajouter un pool de stockage de disque tooa et créer un disque virtuel de la mise en page simple.
    2.  Ajouter des disques supplémentaires et d’étendre le disque virtuel de hello.
    3.  Créer des volumes sur le disque virtuel de hello.
3.  Ajoutez hello volumes tooBackup Server.
4.  Configurez un stockage prenant en compte la charge de travail.

## <a name="create-a-volume-for-modern-backup-storage"></a>Créer un volume pour le stockage de sauvegarde moderne

L’utilisation du Serveur de sauvegarde v2 avec des volumes tels qu’un stockage sur disque peut vous aider à contrôler le stockage. Un volume peut être un disque unique. Toutefois, si vous souhaitez stockage tooextend Bonjour future, créer un volume en dehors d’un disque créé à l’aide des espaces de stockage. Cela peut être utile si vous souhaitez le volume de hello tooexpand pour le stockage de sauvegarde. Cette section présente les meilleures pratiques en matière de création de volume avec ce programme d’installation.

1. Dans le Gestionnaire de serveur, sélectionnez **Services de fichiers et de stockage** > **Volumes** > **Pools de stockage**. Sous **Disques physiques**, sélectionnez **Nouveau pool de stockage**. 

    ![Créer un pool de stockage](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. Bonjour **tâches** zone de liste déroulante, sélectionnez **nouveau disque virtuel**.

    ![Ajouter un disque virtuel](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. Sélectionnez le pool de stockage hello et sélectionnez **ajouter un disque physique**.

    ![Ajouter un disque physique](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. Sélectionnez les disques physiques hello, puis **étendre un disque virtuel**.

    ![Étendre le disque virtuel de hello](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. Sélectionnez le disque virtuel de hello et sélectionnez **nouveau Volume**.

    ![Créer un volume](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. Bonjour **sélectionnez hello serveur et disque** boîte de dialogue, serveur de select hello et nouveau disque de hello. Ensuite, sélectionnez **Suivant**.

    ![Sélectionnez le disque et le serveur de hello](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-toobackup-server-disk-storage"></a>Ajouter du stockage sur disque des volumes tooBackup Server

tooadd un tooBackup volume Server, Bonjour **gestion** volet, effectuez une nouvelle analyse de stockage de hello, puis sélectionnez **ajouter**. Une liste de tous les hello volumes disponibles toobe ajouté pour le stockage de serveur de sauvegarde s’affiche. Une fois que les volumes disponibles sont ajoutés à la liste toohello des volumes sélectionnés, vous pouvez lui attribuer un toohelp nom convivial les gérer. tooformat tooReFS de ces volumes afin de la sauvegarde du serveur peuvent profiter des avantages de hello du stockage de sauvegarde moderne, sélectionnez **OK**.

![Ajouter des volumes disponibles](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a>Configurer un stockage prenant en compte la charge de travail

Avec un stockage prenant en charge les charges de travail, vous pouvez sélectionner les volumes hello préférence stocker certains types de charges de travail. Par exemple, vous pouvez définir des volumes coûteuses qui prennent en charge un grand nombre d’opérations d’entrée/sortie par seconde (IOPS) toostore uniquement hello les charges de travail qui nécessitent des sauvegardes fréquentes et élevées. Un exemple est SQL Server avec les journaux des transactions. Autres charges de travail qui sont sauvegardés moins fréquemment, telles que des machines virtuelles, peuvent être sauvegardées coût toolow volumes.

### <a name="update-dpmdiskstorage"></a>Update-DPMDiskStorage

Vous pouvez définir l’espace de stockage prenant en charge les charges de travail à l’aide d’applet de commande PowerShell hello DPMDiskStorage de la mise à jour, ce qui met à jour les propriétés de hello d’un volume dans le pool de stockage hello sur un serveur Data Protection Manager.

Syntaxe :

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
Hello capture d’écran suivante montre hello DPMDiskStorage de mise à jour applet de commande dans la fenêtre de PowerShell hello.

![Hello commande DPMDiskStorage de mise à jour dans la fenêtre de PowerShell hello](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

Hello apportée à l’aide de PowerShell est répercutées dans hello Console de l’administrateur du serveur de sauvegarde.

![Disques et volumes de hello Console Administrateur](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a>Étapes suivantes
Après avoir installé le serveur de sauvegarde, découvrez comment tooprepare votre serveur, ou pour commencer à protéger une charge de travail.

- [Préparer les charges de travail du serveur de sauvegarde](backup-azure-microsoft-azure-backup.md)
- [Utilisez tooback du serveur de sauvegarde d’un serveur VMware](backup-azure-backup-server-vmware.md)
- [Utilisez tooback de sauvegarde du serveur SQL Server](backup-azure-sql-mabs.md)

