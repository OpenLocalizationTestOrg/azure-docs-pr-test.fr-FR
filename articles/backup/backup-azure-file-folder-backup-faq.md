---
title: "l’agent de sauvegarde aaaAzure FAQ | Documents Microsoft"
description: "Réponses aux questions de toocommon sur : comment hello limites works, de sauvegarde et de rétention de l’agent de sauvegarde Azure."
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "sauvegarde et récupération d’urgence ; service de sauvegarde"
ms.assetid: 778c6ccf-3e57-4103-a022-367cc60c411a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: bdefb4efb39301f38cdf692bdc93c841a2bbb441
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-backup-agent"></a>Questions sur l’agent de sauvegarde Azure hello
Cet article contient des réponses toocommon questions toohelp vous comprenez rapidement les composants de l’agent de sauvegarde Azure hello. Dans certaines des réponses de hello, sont des articles de toohello des liens qui ont des informations complètes. Vous pouvez également poser des questions sur hello service Azure Backup Bonjour [forum de discussion](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="configure-backup"></a>Configurer une sauvegarde
### <a name="where-can-i-download-hello-latest-azure-backup-agent-br"></a>Où puis-je télécharger hello dernière Azure Backup agent ? <br/>
Vous pouvez télécharger l’agent hello plus récent pour la sauvegarde de Windows Server, System Center DPM ou du client Windows, à partir de [ici](http://aka.ms/azurebackup_agent). Si vous souhaitez tooback une machine virtuelle, utilisez hello Agent de machine virtuelle (qui installe automatiquement l’extension appropriée de hello). Hello Agent de machine virtuelle est déjà présent sur les ordinateurs virtuels créés à partir de hello la galerie Azure.

### <a name="when-configuring-hello-azure-backup-agent-i-am-prompted-tooenter-hello-vault-credentials-do-vault-credentials-expire"></a>Lorsque vous configurez l’agent de sauvegarde Azure hello, je suis informations d’identification de coffre de hello tooenter demandées. Les informations d’identification de coffre expirent-elles ?
Oui, les informations d’identification de coffre hello expirent au bout de 48 heures. Si le fichier de hello expire, dans toohello Azure portal et téléchargement hello coffre informations d’identification des fichiers journaux à partir de votre coffre.

### <a name="what-types-of-drives-can-i-back-up-files-and-folders-from-br"></a>À partir de quels types de lecteurs puis-je sauvegarder des fichiers et des dossiers ? <br/>
Vous ne pouvez pas sauvegarder hello suivant des lecteurs/volumes :

* Média amovible : toutes les sources d’éléments de sauvegarde l’élément doivent être déclarées fixes.
* Les Volumes en lecture seule : hello doit être accessible en écriture pour hello volume shadow copy service (VSS) toofunction.
* Les Volumes hors connexion : le volume de hello doit être en ligne pour toofunction VSS.
* Partage réseau : hello doit être toobe de serveur local toohello sauvegardé à l’aide de la sauvegarde en ligne.
* Les volumes protégés par BitLocker : hello doit être déverrouillé avant hello sauvegarde peut être effectuée.
* Identification de système de fichiers : NTFS est hello uniquement pris en charge.

### <a name="what-file-and-folder-types-can-i-back-up-from-my-serverbr"></a>Quels types de fichier et dossier puis-je sauvegarder à partir de mon serveur ?<br/>
Hello les types suivants est pris en charge :

* Chiffré
* Compressé
* Partiellement alloué
* Compressé + partiellement alloué
* Liens physiques : non pris en charge, ignorés
* Point d’analyse : non pris en charge, ignoré
* Chiffré + partiellement alloué : non pris en charge, ignoré
* Flux compressé : non pris en charge, ignoré
* Flux partiellement alloué : non pris en charge, ignoré

### <a name="can-i-install-hello-azure-backup-agent-on-an-azure-vm-already-backed-by-hello-azure-backup-service-using-hello-vm-extension-br"></a>Puis-je installer hello Azure Backup agent sur une machine virtuelle de Azure déjà sauvegardé par le service de sauvegarde Azure hello à l’aide de hello extension de machine virtuelle ? <br/>
Absolument. Azure Backup offre une sauvegarde au niveau de la machine virtuelle pour les machines virtuelles Azure à l’aide d’extension de machine virtuelle hello. tooprotect fichiers et dossiers sur l’invité hello Windows du système d’exploitation, installer hello Azure Backup agent sur l’invité hello du système d’exploitation Windows.

### <a name="can-i-install-hello-azure-backup-agent-on-an-azure-vm-tooback-up-files-and-folders-present-on-temporary-storage-provided-by-hello-azure-vm-br"></a>Puis-je installer hello Azure Backup agent sur un tooback de machine virtuelle Azure des fichiers et dossiers présents sur le stockage temporaire fourni par hello Azure VM ? <br/>
Oui. Installer l’agent de sauvegarde Azure hello sur l’invité hello du système d’exploitation Windows et sauvegarder des fichiers et dossiers de stockage de tootemporary. Les opérations de sauvegarde échouent une fois les données du stockage temporaire effacées. En outre, si les données de stockage temporaire salutation a été supprimées, vous pouvez uniquement restaurer le stockage volatile toonon.

### <a name="whats-hello-minimum-size-requirement-for-hello-cache-folder-br"></a>Qu’est hello taille minimale requise pour le dossier de cache hello ? <br/>
taille de Hello hello du dossier de cache détermine hello de données que vous sauvegardez. Votre dossier de cache doit être de 5 % d’espace hello requis pour le stockage de données.

### <a name="how-do-i-register-my-server-tooanother-datacenterbr"></a>Comment inscrire mon centre de données tooanother server ?<br/>
Données de sauvegarde sont envoyées à centre de données toohello de toowhich de coffre hello qu’il est inscrit. Hello plus simple moyen toochange hello centre de données est l’agent de hello toouninstall et réinstaller l’agent de hello et inscrire tooa nouveau coffre auquel appartient le centre de données toodesired.

### <a name="does-hello-azure-backup-agent-work-on-a-server-that-uses-windows-server-2012-deduplication-br"></a>Est hello Azure Backup agent fonctionne sur un serveur qui utilise la déduplication de Windows Server 2012 ? <br/>
Oui. service de l’agent Hello convertit hello dédupliqué données toonormal lorsqu’il prépare l’opération de sauvegarde hello. Puis optimise les données hello pour la sauvegarde, chiffre les données hello et envoie ensuite le service sauvegarde en ligne de données toohello hello chiffré.

## <a name="backup"></a>Sauvegarde
### <a name="how-do-i-change-hello-cache-location-specified-for-hello-azure-backup-agentbr"></a>Évolution de l’emplacement du cache de hello spécifié pour l’agent de sauvegarde Azure hello<br/>
Utilisez hello suivant l’emplacement du cache de liste toochange hello.

1. Arrêter le moteur de sauvegarde hello en exécutant hello suivant de commande dans une invite de commandes avec élévation de privilèges :

    ```PS C:\> Net stop obengine``` 
  
2. Ne déplacez pas les fichiers hello. Au lieu de cela, copiez hello cache espace dossier tooa lecteur disposant de suffisamment d’espace. espace de cache Hello d’origine peut être supprimé après avoir confirmé hello sauvegardes fonctionnent avec le nouvel espace de cache hello.
3. Mettre à jour hello suivant des entrées de Registre avec le dossier d’espace cache nouvelle hello chemin d’accès toohello.<br/>

    | Chemin d’accès au Registre | Clé de Registre | Valeur |
    | --- | --- | --- |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config` |ScratchLocation |*Emplacement du nouveau dossier de cache* |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider` |ScratchLocation |*Emplacement du nouveau dossier de cache* |

4. Redémarrez le moteur de sauvegarde hello en exécutant hello suivant de commande dans une invite de commandes avec élévation de privilèges :

    ```PS C:\> Net start obengine```

Une fois la création de la sauvegarde hello est terminée dans le nouvel emplacement de cache hello, vous pouvez supprimer le dossier de cache hello d’origine.


### <a name="where-can-i-put-hello-cache-folder-for-hello-azure-backup-agent-toowork-as-expectedbr"></a>Où puis-je placer le dossier de cache hello pour hello Azure Backup Agent toowork comme prévu ?<br/>
Hello emplacements suivants pour le dossier de cache hello ne sont pas recommandés :

* Réseau du partage ou un support amovible : dossier de cache hello doit être le serveur local toohello nécessitant une sauvegarde à l’aide de la sauvegarde en ligne. Les emplacements réseau ou les médias amovibles (tels que les lecteurs USB) ne sont pas pris en charge.
* Volumes hors connexion : le dossier de cache hello doit être en ligne pour la sauvegarde attendu à l’aide de l’Agent Azure Backup.

### <a name="are-there-any-attributes-of-hello-cache-folder-that-are-not-supportedbr"></a>Y a-t-il des attributs du dossier de cache hello qui ne sont pas pris en charge ?<br/>
Hello attributs suivants ou leurs combinaisons ne sont pas pris en charge pour le dossier de cache hello :

* Chiffré
* Dédupliqué
* Compressé
* Partiellement alloué
* Point d’analyse

dossier de cache Hello et hello métadonnées VHD inutile attributs nécessaires de hello pour hello Azure Backup agent.

### <a name="is-there-a-way-tooadjust-hello-amount-of-bandwidth-used-by-hello-backup-servicebr"></a>Existe-t-il une quantité de hello tooadjust moyen de la bande passante utilisée par le service de sauvegarde hello ?<br/>
  Oui, utiliser hello **modifier les propriétés** option de la bande passante de tooadjust hello l’Agent de sauvegarde. Vous pouvez ajuster hello fois hello et la bande passante lorsque vous utilisez que la bande passante. Pour obtenir des instructions détaillées, consultez **[Activation de la limitation du réseau](backup-configure-vault.md#enable-network-throttling)**.

## <a name="manage-backups"></a>Gestion des sauvegardes
### <a name="what-happens-if-i-rename-a-windows-server-that-is-backing-up-data-tooazurebr"></a>Que se passe-t-il si vous renommez un serveur Windows qui sauvegarde les données tooAzure ?<br/>
Lorsque vous renommez un serveur, toutes les sauvegardes actuellement configurées sont arrêtées.
Hello nouveau nom du serveur de hello auprès de coffre de sauvegarde hello. Lorsque vous enregistrez un nouveau nom de hello avec le coffre de hello, la première opération de sauvegarde hello est un *complète* sauvegarde. Si vous avez besoin des données toorecover sauvegardées coffre toohello avec l’ancien nom du serveur hello, utilisez hello [ **un autre serveur** ](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) option Bonjour **récupérer les données** Assistant.

### <a name="what-is-hello-maximum-file-path-length-that-can-be-specified-in-backup-policy-using-azure-backup-agent-br"></a>Quelle est la longueur de chemin d’accès de fichier maximale hello qui peut être spécifiée dans la stratégie de sauvegarde à l’aide de l’agent Azure Backup ? <br/>
L’agent Azure Backup utilise le format NTFS. Hello [spécification de longueur de chemin d’accès est limitée par hello API Windows](https://msdn.microsoft.com/library/aa365247.aspx#fully_qualified_vs._relative_paths). Si les fichiers hello tooprotect ont une longueur de chemin d’accès plus longue que ce qui est autorisé par hello API Windows, sauvegardez hello parent dossier ou un lecteur de disque hello.  

### <a name="what-characters-are-allowed-in-file-path-of-azure-backup-policy-using-azure-backup-agent-br"></a>Quels sont les caractères autorisés dans le chemin d’accès du fichier de stratégie Azure Backup à l’aide de l’agent Azure Backup ? <br>
 L’agent Azure Backup utilise le format NTFS. Elle active les [caractères NTFS pris en charge](https://msdn.microsoft.com/library/aa365247.aspx#naming_conventions) dans le cadre de la spécification de fichier. 
 
### <a name="i-receive-hello-warning-azure-backups-have-not-been-configured-for-this-server-even-though-i-configured-a-backup-policy-br"></a>Je reçois hello avertissement, « Sauvegardes Azure n'ont pas été configurées pour ce serveur » bien que j’ai configuré une stratégie de sauvegarde <br/>
Cet avertissement se produit lorsque les paramètres de planification de sauvegarde hello stockés sur le serveur local de hello ne sont pas hello identique hello paramètres stockés dans le coffre de sauvegarde hello. Lorsque le serveur de hello ou de paramètres de hello ont été récupéré tooa bonne configuration connue, les planifications de sauvegarde hello peuvent perdre la synchronisation. Si vous recevez cet avertissement, [reconfigurer la stratégie de sauvegarde hello](backup-azure-manage-windows-server.md) , puis **exécuter une sauvegarde immédiate** serveur local de hello tooresynchronize avec Azure.
