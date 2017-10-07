---
title: "Sauvegarde Azure : récupérer des fichiers et des dossiers à partir d’une sauvegarde de machine virtuelle Azure | Microsoft Docs"
description: "Récupérer des fichiers à partir d’un point de récupération de machine virtuelle Azure"
services: backup
documentationcenter: dev-center-name
author: pvrk
manager: shivamg
keywords: "récupération au niveau élément ; récupération de fichiers à partir d’une sauvegarde de machine virtuelle Azure ; restaurer des fichiers à partir d’une machine virtuelle Azure"
ms.assetid: f1c067a2-4826-4da4-b97a-c5fd6c189a77
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/20/2017
ms.author: pullabhk;markgal
ms.openlocfilehash: 1a62a0ed83d61272c032ac0377a54099ed118db4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="recover-files-from-azure-virtual-machine-backup"></a>Récupérer des fichiers à partir d’une sauvegarde de machine virtuelle Azure

Azure backup offre hello capacité toorestore [machines virtuelles Azure et les disques](./backup-azure-arm-restore-vms.md) à partir de sauvegardes de machine virtuelle Azure. Cet article explique comment récupérer des éléments tels que des fichiers et des dossiers à partir d’une sauvegarde de machine virtuelle Azure.

> [!Note]
> Cette fonctionnalité est disponible pour les machines virtuelles Azure déployé à l’aide du modèle de gestionnaire de ressources hello et protégé tooa coffre Recovery services.
> La récupération de fichiers à partir d’une sauvegarde de machine virtuelle chiffrée n’est pas prise en charge.
>

## <a name="mount-hello-volume-and-copy-files"></a>Monter hello volume et copier des fichiers

1. L’authentification à hello [portail Azure](http://portal.Azure.com). Recherchez coffre hello pertinentes Recovery services et sauvegarder l’élément hello requis.

2. Dans le panneau d’élément de sauvegarde hello, cliquez sur **récupération de fichier**

    ![Ouvrir l’élément de sauvegarde du coffre Recovery Services.](./media/backup-azure-restore-files-from-vm/open-vault-item.png)

    Hello **récupération de fichier** panneau s’ouvre.

    ![Panneau Récupération de fichier](./media/backup-azure-restore-files-from-vm/file-recovery-blade.png)

3. À partir de hello **sélectionner le point de récupération** menu déroulant, le point de récupération hello select qui contient les fichiers hello souhaité. Par défaut, dernier point de récupération hello est déjà sélectionné.

4. Cliquez sur **télécharger le fichier exécutable** (pour la machine virtuelle Windows Azure) ou **télécharger le Script** (pour Linux Azure VM) logiciels de hello toodownload que vous allez utiliser toocopy des fichiers de point de récupération hello.

  Hello exécutable/script crée une connexion entre l’ordinateur local de hello et hello spécifié point de récupération.

5. Vous avez besoin d’un mot de passe toorun hello téléchargé script/exécutable. Vous pouvez copier le mot de passe hello à partir du portail hello à l’aide du bouton en regard de mot de passe généré de hello hello

    ![Mot de passe généré](./media/backup-azure-restore-files-from-vm/generated-pswd.png)

6. Sur hello ordinateur sur lequel les fichiers hello toorecover, exécutez hello exécutable/script. Vous devez l’exécuter en tant qu’administrateur. Si vous exécutez le script de hello sur un ordinateur avec accès restreint, vérifiez l’accès à :

    - download.microsoft.com
    - points de terminaison Azure utilisés pour les sauvegardes de machines virtuelles Azure
    - port sortant 3260

   Pour Linux, script de hello nécessite les composants 'open-iscsi' et 'lshw' point de récupération tooconnect toohello. Si ceux n’existent pas sur l’ordinateur hello où elle est exécutée, elle demande composants concernés d’autorisation tooinstall hello et les installe sur son consentement.
   
   Entrez le mot de passe hello copié à partir du portail hello lorsque vous y êtes invité. Une fois que le mot de passe valide hello est entré les scripts hello établit une connexion point de récupération toohello.
      
    ![Panneau Récupération de fichier](./media/backup-azure-restore-files-from-vm/executable-output.png)
    
   
   Vous pouvez exécuter le script de hello sur les ordinateurs où le système d’exploitation de hello identiques (ou compatibles) comme hello sauvegardé machine virtuelle. Consultez hello [table du système d’exploitation Compatible](backup-azure-restore-files-from-vm.md#compatible-os) pour les systèmes d’exploitation compatibles. Si hello protégé Azure virtuel utilise machine des espaces de stockage de Windows (pour les machines virtuelles Windows Azure) ou le Gestionnaire de volume logique/RAID Arrays(for Linux VMs), puis vous ne pouvez pas exécuter hello exécutable/script sur hello même machine virtuelle. Au lieu de cela, exécutez-la sur n’importe quelle autre machine avec un système d’exploitation compatible.

### <a name="compatible-os"></a>Systèmes d’exploitation compatibles

#### <a name="for-windows"></a>Pour Windows

Hello suivant table affiche hello compatibilité entre les systèmes d’exploitation serveur et l’ordinateur. Lors de la récupération de fichiers, vous ne pouvez pas restaurer des fichiers entre des systèmes d’exploitation incompatibles.

|Système d’exploitation serveur | Système d’exploitation client compatible  |
| --------------- | ---- |
| Windows Server 2012 R2 | Windows 8.1 |
| Windows Server 2012    | Windows 8  |
| Windows Server 2008 R2 | Windows 7   |

#### <a name="for-linux"></a>Pour Linux

Sous Linux, condition fondamentale de hello est que hello du système d’exploitation de l’ordinateur hello où le script de hello est exécutée doit prendre en charge du système de fichiers hello Hello fichiers présents dans hello sauvegardéent Linux VM. Lors du choix d’un script de hello toorun machine, vérifiez que l’il possède des versions compatibles de système d’exploitation et hello hello comme indiqué dans le tableau hello ci-dessous.

|Système d’exploitation Linux | Versions  |
| --------------- | ---- |
| Ubuntu | 12.04 et versions ultérieures |
| CentOS | 6.5 et versions ultérieures  |
| RHEL | 6.7 et versions ultérieures |
| Debian | 7 et versions ultérieures |
| Oracle Linux | 6.4 et versions ultérieures |

script de Hello requiert aussi python et bash tooexecute de composants et vous connecter en toute sécurité point de récupération toohello.

|Composant | Version  |
| --------------- | ---- |
| bash | 4 et versions ultérieures |
| python | 2.6.6 et versions ultérieures  |


### <a name="identifying-volumes"></a>Identification des volumes

#### <a name="for-windows"></a>Pour Windows

Lorsque vous exécutez hello exécutable, système d’exploitation de hello monte les volumes nouvelle hello et attribue des lettres de lecteur. Vous pouvez utiliser l’Explorateur Windows ou l’Explorateur de fichiers toobrowse ces lecteurs. Hello lettres de lecteur affectées toohello volumes peut-être pas hello mêmes lettres que hello les ordinateur virtuel d’origine, toutefois, hello nom de volume sont conservé. Par exemple, si hello volume sur l’ordinateur virtuel d’origine de hello a été « disque de données (E:\)», que le volume peut être attaché en tant que « disque de données (« Aucune lettre de lecteur disponible » :\) sur l’ordinateur local de hello. Parcourir tous les volumes mentionnés dans la sortie du script hello jusqu'à ce que vous trouviez votre dossier de fichiers /.  
       
   ![Panneau Récupération de fichier](./media/backup-azure-restore-files-from-vm/volumes-attached.png)
           
#### <a name="for-linux"></a>Pour Linux

Sous Linux, volumes hello hello du point de récupération sont dossier monté toohello où le script de hello est exécutée. Hello attacher des disques, volumes et montage correspondante de hello chemins d’accès sont affichés en conséquence. Ces chemins d’accès de montage sont visibles toousers ayant un accès au niveau racine. Parcourir les volumes hello mentionnés dans la sortie du script hello.

  ![Panneau Récupération de fichier Linux](./media/backup-azure-restore-files-from-vm/linux-mount-paths.png)
  

## <a name="closing-hello-connection"></a>Fermeture de la connexion de hello

Après avoir identifié les fichiers de hello, les copier l’emplacement de stockage local tooa, supprimez (ou démonter) des lecteurs supplémentaires hello. lecteurs toounmount hello, hello **récupération de fichier** panneau Bonjour portail Azure, cliquez sur **démontage de disques**.

![Démonter les disques](./media/backup-azure-restore-files-from-vm/unmount-disks3.png)

Une fois que les disques hello ont été démontés, vous recevez un message vous informe qu’il a réussi. Il peut prendre quelques minutes pour hello connexion toorefresh afin que vous pouvez supprimer les disques hello.

Sous Linux, une fois le point de récupération toohello hello connexion est interrompue, hello du système d’exploitation ne supprime pas chemins d’accès de montage correspondants hello automatiquement. Ils se trouvent en tant que volumes de « orphelin » et ils sont visibles, mais génère une erreur lorsque vous les fichiers hello accès/écriture. Ils peuvent être supprimés manuellement. script Hello quand il est exécuté, identifie les volumes de ce type existant à partir des points de récupération précédent et nettoie les lors de son consentement.

## <a name="special-configurations"></a>Configurations spéciales

### <a name="dynamic-disks"></a>Disques dynamiques

Si hello machine virtuelle Azure qui a été sauvegardée comporte des volumes qui s’étendent sur plusieurs disques (volumes agrégés et) et/ou des volumes à tolérance de pannes (volumes en miroir ou RAID-5) sur les disques dynamiques, puis vous ne peut pas exécuter un script exécutable hello sur hello même machine virtuelle. Au lieu de cela, exécutez un script exécutable hello sur tout autre ordinateur avec un système d’exploitation compatible.

### <a name="windows-storage-spaces"></a>Espaces de stockage Windows

Espaces de stockage Windows est une technologie de stockage de Windows qui vous permet le stockage de toovirtualize. Avec les espaces de stockage Windows, vous pouvez regrouper des disques standard en pools de stockage et puis créer des disques virtuels, appelés espaces de stockage, à partir de l’espace disponible de hello dans les pools de stockage.

Si hello machine virtuelle Azure qui a été sauvegardée utilise des espaces de stockage Windows, puis vous ne peut pas exécuter un script exécutable hello sur hello même machine virtuelle. Au lieu de cela, exécutez un script exécutable hello sur tout autre ordinateur avec un système d’exploitation compatible.

### <a name="lvmraid-arrays"></a>Baies LVM/RAID

Dans Linux, le Gestionnaire de volume logique (LVM) et/ou du logiciel RAID tableaux sont des volumes logiques toomanage utilisé sur plusieurs disques. Si hello sauvegardée Linux VM utilise le Gestionnaire de volume logique et/ou des tableaux RAID, vous ne peut pas exécuter les script hello sur hello même machine virtuelle. Exécuter à la place de script de hello sur tout autre ordinateur avec le système d’exploitation compatible et qui prend en charge le système de fichiers de hello sauvegardé la machine virtuelle.

sortie du script Hello affiche hello Gestionnaire de volume logique et/ou les disques de tableaux RAID et les volumes de hello avec le type de partition hello comme indiqué ci-dessous

   ![Panneau de sortie de LVM Linux](./media/backup-azure-restore-files-from-vm/linux-LVMOutput.png)
   
les commandes Hello suivant besoin toobe exécutée par hello utilisateur toobring ces partitions en ligne. 

**Pour les partitions LVM**

```
$ pvs <volume name as shown above in hello script output> 
```
Répertorie les noms de groupe de volumes hello sous un volume physique.

```
$ lvdisplay <volume-group-name from hello pvs command’s results> 
```
Cela répertorie tous les volumes logiques, noms et chemins d’accès dans un groupe de volumes.

```
$ mount <LV path> </mountpath>
```
toomount hello des volumes logiques toohello chemin d’accès de votre choix.


**Pour les tableaux RAID**

```
$ mdadm –detail –scan
```
Cela affiche des détails sur tous les disques RAID. les disques RAID pertinentes Hello seront affichera en tant que`/dev/mdm/<RAID array name in hello backed up VM>`

Utilisez la commande de montage de hello si le disque RAID hello dispose de volumes physiques.
```
$ mount [RAID Disk Path] [/mounthpath]
```

Si ce disque RAID a un autre gestionnaire de volume logique configuré puis suivez hello même procédure, comme indiqué plus haut pour les partitions de gestionnaire de volume logique avec le nom de volume hello étant nom de disque RAID hello

## <a name="troubleshooting"></a>Résolution des problèmes

Si vous rencontrez des problèmes lors de la récupération de fichiers à partir d’ordinateurs virtuels de hello, vérifiez hello tableau pour plus d’informations.

| Message d’erreur/Scénario | Cause probable | Action recommandée |
| ------------------------ | -------------- | ------------------ |
| Sortie de l’exe : *connexion toohello cible (Exception)* |Script n’est pas un point de récupération tooaccess en mesure de hello | Vérifiez si les ordinateur hello satisfait les besoins de l’accès hello mentionnés ci-dessus|  
|   Sortie de l’exe : *hello cible a déjà été connectée via une session ISCSI.* |   script de Hello a déjà été exécuté sur hello même ordinateur et hello les lecteurs ont été attachées. |   volumes Hello hello du point de récupération ont déjà été attachés. Ils ne peuvent être montés par hello même des lettres de lecteur hello d’ordinateur virtuel d’origine. Parcourir tous les volumes disponibles hello dans l’Explorateur de fichiers hello pour votre fichier |
| Sortie de l’exe : *ce script n’est pas valide, car les disques hello ont été démontés via la limite de 12-hr hello de portail/dépassé. Téléchargez un nouveau script à partir du portail de hello.* |    les disques Hello ont été démontées du portail de hello ou de la limite de 12-hr hello dépassée |  Ce fichier exécutable en particulier n’est plus valide et ne peut pas être exécuté. Si vous souhaitez tooaccess hello des fichiers de cette récupération limitée dans le temps, visitez le portail de hello pour un nouvel exe|
| Sur l’ordinateur hello où hello exe est exécuté : nouveaux volumes de hello ne sont pas démontées après hello démontage du bouton |    initiateur ISCSI de Hello sur l’ordinateur de hello n’est pas de réponse/actualisation de sa cible de toohello de connexion et en conservant le cache de hello |    Attendez quelques minutes après que hello démontage bouton est enfoncé. Si de nouveaux volumes de hello sont toujours pas démontées, Veuillez parcourir tous les volumes hello. Cette force hello initiateur toorefresh hello connexion et hello volume est démonté avec un message d’erreur qui hello disque n’est pas disponible|
| Sortie de l’exe : Script est exécuté avec succès, mais « Nouveaux volumes attachés » ne sont pas affichés dans la sortie du script hello |   Il s’agit d’une erreur temporaire.   | les volumes Hello seraient ont été déjà attachés. Ouvrez l’Explorateur toobrowse. Si vous utilisez hello même de l’ordinateur pour exécuter des scripts à chaque fois, redémarrez l’ordinateur de hello et liste de hello doit être affiché dans les exécutions ultérieures exe hello. |
| Spécifique à Linux : tooview n’a pas pu hello souhaitée des volumes | Hello du système d’exploitation de l’ordinateur hello où le script de hello est exécutée peut ne pas reconnaît hello un système de fichiers sous-jacent de hello sauvegardé de machine virtuelle | Vérifiez si un point de récupération de hello est incident cohérent ou avec cohérence de fichiers. Si le script cohérent, exécutez hello du fichier sur un autre ordinateur dont système d’exploitation reconnaît hello sauvegardé de système de fichiers de la machine virtuelle |
| Spécifiques à Windows : tooview n’a pas pu hello souhaitée des volumes | les disques Hello ont été attachées, mais les volumes hello n’ont pas été configurées. | À partir de l’écran de gestion de disque hello, identifier le point de récupération de toohello connexes de disques supplémentaires hello. Si un de ces disques sont hors connexion état essayez en ligne en cliquant sur le disque de hello et cliquez sur « En ligne »|
