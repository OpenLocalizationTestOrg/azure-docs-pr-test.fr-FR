---
title: "aaaAzure résolution des problèmes de chiffrement de disque | Documents Microsoft"
description: "Cet article contient des conseils de dépannage concernant Microsoft Azure Disk Encryption pour les machines virtuelles IaaS Windows et Linux."
services: security
documentationcenter: na
author: deventiwari
manager: avibm
editor: yuridio
ms.assetid: ce0e23bd-07eb-43af-a56c-aa1a73bdb747
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: devtiw
ms.openlocfilehash: 2ecb8df1fb869e3bf8f3be4be4494e6485e75695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-troubleshooting-guide"></a>Guide de dépannage Azure Disk Encryption

Ce guide est aux professionnels informatiques (IT), informations d’aux analystes en sécurité et problèmes liés à des administrateurs de cloud dont l’organisation utilisent le chiffrement des disques Azure et avez besoin de conseils tootroubleshoot-chiffrement de disque.

## <a name="troubleshooting-linux-os-disk-encryption"></a>Résolution des problèmes de chiffrement de disque de système d’exploitation Linux

Chiffrement de disque du système d’exploitation Linux devez démonter toorunning préalable du lecteur hello du système d’exploitation via le processus de chiffrement de disque complet hello.   S’il ne peut pas, un message d’erreur « Échec toounmount après... » message d’erreur est probablement toooccur.

Cela se produit souvent lors d’une tentative de chiffrement de disque dans un environnement de machines virtuelles cible, quand l’image de ce dernier a été modifiée par rapport à celle de la galerie d’images stock (officielles) prises en charge.  Voici quelques exemples des écarts par rapport à partir de l’image hello pris en charge, ce qui peut interférer avec un lecteur de l’extension hello capacité toounmount hello du système d’exploitation :
- Images personnalisées qui ne correspondent plus au système de fichiers et/ou au schéma de partitionnement pris en charge.
- Images personnalisées avec des applications telles que les antivirus, Docker, SAP, MongoDB ou Cassandra Apache en cours d’exécution dans tooencryption préalable du système d’exploitation hello.  Ces applications sont tooterminate difficile, et lorsqu’ils conservent le lecteur de fichiers ouverts handles toohello du système d’exploitation, hello ne peut pas être démonté, à l’origine de la défaillance.
- Les scripts personnalisés qui s’exécutent dans fermant étape de chiffrement toohello de proximité permettre interférer et provoquer cette défaillance. Cela peut se produire lorsqu’un modèle de gestionnaire de ressources définit plusieurs extensions tooexecute simultanément, ou qu’une extension de script personnalisé ou une autre action s’exécute simultanément toodisk chiffrement.   Sérialisation et d’isoler ces étapes pour résoudre les problème de hello.
- Lorsque SELinux n’a pas été désactivé tooenabling préalable chiffrement, hello démontez étape échoue.  SELinux peut être réactivé à la fin du chiffrement.
- Lorsque hello du système d’exploitation disque utilise le schéma d’un gestionnaire de volume logique (bien que la prise en charge du disque de données Gestionnaire de volume logique limitée est disponible, disque de système d’exploitation du Gestionnaire de volume logique n’est pas)
- Lorsque les conditions requises en matière de capacité de mémoire minimale ne sont pas remplies (7 Go sont recommandés pour le chiffrement de disque de système d’exploitation).
- Lorsque les lecteurs de données ont été montés de manière récursive sous le répertoire /mnt/ou les uns sous les autres (par exemple /mnt/data1, /mnt/data2, /data3 + /data3/data4, etc.).
- Lorsque les autres [conditions préalables](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) pour l’utilisation d’Azure Disk Encryption pour Linux ne sont pas satisfaites.

## <a name="unable-tooencrypt"></a>Impossible de tooencrypt

Dans certains cas, le chiffrement de disque Linux hello apparaît toobe bloqué au niveau de « Chiffrement de disque du système d’exploitation a démarré » et SSH est désactivée. Ce processus peut prendre entre toocomplete 3-16 heures sur une image de la galerie de stock.  Si les disques de données de taille de multi-to sont ajoutés, les processus hello peuvent prendre des jours. Bonjour séquence de chiffrement de disque du système d’exploitation Linux démonte le lecteur de hello du système d’exploitation temporairement et effectue le chiffrement par bloc de hello totalité du système d’exploitation du disque, avant de remonter elle dans son état chiffré.   Contrairement au chiffrement de disque Azure sur Windows, chiffrement de disque Linux n’autorise pas l’utilisation simultanée de hello machine virtuelle pendant le chiffrement hello est en cours d’exécution.  caractéristiques de performances Hello Hello machine virtuelle, y compris la taille de hello de disque de hello et indique si le compte de stockage hello est sauvegardé par le stockage standard ou premium (SSD), peuvent influencer considérablement hello durée toocomplete chiffrement.

état de toocheck, champ ProgressMessage de hello retourné à partir de hello [Get-AzureRmVmDiskEncryptionStatus](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) commande peut être interrogée.   Alors que lecteur de hello du système d’exploitation est chiffrée, hello VM entre dans un état de maintenance et SSH est également désactivé tooprevent n’importe quel processus en cours de toohello interruption de service.  EncryptionInProgress sera signalé pour la majorité de hello des temps de hello pendant que le chiffrement est en cours, suivie de plusieurs heures plus tard avec un message VMRestartPending invitant toorestart hello machine virtuelle.  Par exemple :


```
PS > Get-AzureRmVMDiskEncryptionStatus -ResourceGroupName $resourceGroupName -VMName $vmName
OsVolumeEncrypted          : EncryptionInProgress
DataVolumesEncrypted       : EncryptionInProgress
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OS disk encryption started

PS > Get-AzureRmVMDiskEncryptionStatus -ResourceGroupName $resourceGroupName -VMName $vmName
OsVolumeEncrypted          : VMRestartPending
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OS disk successfully encrypted, please reboot hello VM
```

Une fois invité tooreboot hello machine virtuelle, et après le redémarrage de hello machine virtuelle et en donnant 2 à 3 minutes pour le redémarrage de hello et toobe dernières étapes effectuées sur la cible de hello, message d’état hello indique que le chiffrement est enfin terminée.   Une fois que ce message est disponible, lecteur de système d’exploitation hello chiffré n’est attendue toobe prêt pour une utilisation et pour toobe de machine virtuelle hello utilisable.

Dans les cas où cette séquence n’est pas visible, ou si les informations de démarrage, un message de progression ou autres indicateurs d’erreur signalent que le chiffrement du système d’exploitation a échoué au milieu de hello de ce processus (par exemple si hello « Échec de toounmount » message d’erreur décrit dans ce guide), Il est recommandé de capture instantanée de toorestore hello VM toohello précédent ou sauvegarde effectuée immédiatement préalable tooencryption.  Toohello préalable prochaine tentative, il est suggéré toore-évaluer les caractéristiques de hello Hello machine virtuelle et vous assurer que toutes les conditions préalables sont satisfaites.

## <a name="troubleshooting-azure-disk-encryption-behind-a-firewall"></a>Résolution des problèmes Azure Disk Encryption derrière un pare-feu
Lorsque connectivité est limitée par une capacité hello pare-feu, une exigence de proxy ou paramètres de groupe (NSG) de sécurité réseau, hello extension tooperform nécessitent tâches peut être interrompues.   Cela peut entraîner des messages d’état tels que « État de l’Extension non disponible sur la machine virtuelle de hello » dans des scénarios attendus échouent toofinish.  les sections Hello qui suivent a certains problèmes courants de pare-feu que vous pouvez examiner.

### <a name="network-security-groups"></a>groupes de sécurité réseau ;
Les paramètres appliqués du groupe de sécurité réseau doivent toujours autoriser la hello point de terminaison toomeet hello documentée réseau configuration [conditions préalables](https://docs.microsoft.com/azure/security/azure-security-disk-encryption#prerequisites) pour le chiffrement du disque.

### <a name="azure-keyvault-behind-firewall"></a>Azure Key Vault derrière un pare-feu
Hello machine virtuelle doit être en mesure de tooaccess coffre de clés. Consultez tooguidance lors d’une erreur de tookey accès derrière un pare-feu qui est géré par hello [le coffre de clés](https://docs.microsoft.com/azure/key-vault/key-vault-access-behind-firewall) équipe.

### <a name="linux-package-management-behind-firewall"></a>Gestion des packages Linux derrière un pare-feu
Au moment de l’exécution, le chiffrement de disque Azure pour Linux s’appuie sur package management tooinstall nécessité composants prérequis tooenabling préalable le chiffrement du système du hello cibler la distribution.  Si les paramètres de pare-feu empêchent d’hello machine virtuelle en mesure de toodownload et installent ces composants, les échecs suivants sont attendus.    tooconfigure d’étapes Hello que cela peut varier selon la distribution.  Sous Red Hat, lorsqu’un proxy est requis, vous devez absolument vous assurer que subscription-manager et yum sont configurés correctement.  Consultez [l’article](https://access.redhat.com/solutions/189533) de support Red Hat à ce propos.  

## <a name="troubleshooting-windows-server-2016-server-core"></a>Résolution des problèmes Windows Server 2016 Server Core

Sur Server Core de Windows Server 2016, composant de bdehdcfg hello n’est pas disponible par défaut. Ce composant est requis par Azure Disk Encryption.

tooworkaround ce problème, le hello copie suivant 4 fichiers depuis un dossier de c:\windows\system32 toohello machine virtuelle du centre de données de Windows Server 2016 d’image de Server Core hello :

```
bdehdcfg.exe
bdehdcfglib.dll
bdehdcfglib.dll.mui
bdehdcfg.exe.mui
```

Ensuite, exécutez hello de commande suivante :

```
bdehdcfg.exe -target default
```

Cette opération crée une partition de système de 550 Mo et puis après un redémarrage, vous pouvez utiliser des volumes de Diskpart toocheck hello et continuer.  

Par exemple :

```
DISKPART> list vol

  Volume ###  Ltr  Label        Fs     Type        Size     Status     Info
  ----------  ---  -----------  -----  ----------  -------  ---------  --------
  Volume 0     C                NTFS   Partition    126 GB  Healthy    Boot
  Volume 1                      NTFS   Partition    550 MB  Healthy    System
  Volume 2     D   Temporary S  NTFS   Partition     13 GB  Healthy    Pagefile
```
## <a name="see-also"></a>Voir aussi
Dans ce document, vous avez appris plus sur certains problèmes courants dans le chiffrement du disque Azure et comment tootroubleshoot. Pour plus d’informations sur ce service et ses fonctionnalités, consultez ces pages :

- [Appliquer le chiffrement de disque dans Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [Chiffrement d’une machine virtuelle Azure](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [Azure Data Encryption-at-Rest](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest) (Chiffrement des données Azure au repos)
