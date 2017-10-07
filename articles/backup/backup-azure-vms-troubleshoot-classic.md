---
title: aaaTroubleshoot Azure erreurs dans le portail classique de sauvegarde | Documents Microsoft
description: "Résoudre les problèmes de sauvegarde et restauration de machines virtuelles dans le portail classique de hello Azure."
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 117201fb-c0cd-4be4-b47f-abd88fe914cf
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: trinadhk;markgal;
ms.openlocfilehash: b9907f6fa57c631f5446c4d00f946a57c4efd72b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-virtual-machine-backup"></a>Dépannage de la sauvegarde de machine virtuelle Azure
> [!div class="op_single_selector"]
> * [Coffre Recovery Services](backup-azure-vms-troubleshoot.md)
> * [Archivage de sauvegarde](backup-azure-vms-troubleshoot-classic.md)
>
>

Vous pouvez résoudre les erreurs rencontrées lors de l’utilisation d’Azure Backup avec des informations répertoriées dans la table hello ci-dessous.

## <a name="discovery"></a>Découverte
| Opération de sauvegarde | Détails de l’erreur | Solution de contournement |
| --- | --- | --- |
| Découverte |Échec de toodiscover de nouveaux éléments - Microsoft Azure Backup a rencontré et une erreur interne. Attendez quelques minutes et recommencez l’opération hello. |Recommencer le processus de découverte de hello après 15 minutes. |
| Découverte |Échec de nouveaux éléments toodiscover – découverte une autre opération est déjà en cours d’exécution. Veuillez patienter jusqu'à ce que l’opération de découverte actuelle hello terminée. |Aucun |

## <a name="register"></a>S’inscrire
| Opération de sauvegarde | Détails de l’erreur | Solution de contournement |
| --- | --- | --- |
| S’inscrire |Nombre de disques de données attaché limite de hello pris en charge d’ordinateur virtuel a dépassé toohello - Veuillez détacher des disques de données sur cette opération hello machine virtuelle et réessayez. Azure prend en charge la sauvegarde des disques de données too16 jointe tooan machine virtuelle Azure pour la sauvegarde |Aucun |
| S’inscrire |Microsoft Azure Backup a rencontré une erreur interne - attendez quelques minutes et recommencez l’opération hello. Si hello problème persiste, contactez le Support Microsoft. |Vous pouvez obtenir cette erreur en raison de la configuration tooone de hello suivant non pris en charge de l’ordinateur virtuel sur le stockage LRS Premium. <br> Les machines virtuelles de stockage Premium peuvent être sauvegardées à l’aide du coffre Recovery Services. [En savoir plus](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup) |
| S’inscrire |Échec de l’inscription avec un délai d’expiration de l’opération Installer l’agent |Vérifiez si la version du système d’exploitation hello de machine virtuelle de hello est pris en charge. |
| S’inscrire |Échec de l’exécution de la commande - Une autre opération est en cours sur cet élément Veuillez patienter pendant que l’opération précédente de hello est terminée |Aucun |
| S’inscrire |Les machines virtuelles dotées de disques durs virtuels stockés sur le stockage Premium ne sont pas prises en charge par la sauvegarde |Aucun |
| S’inscrire |Agent de machine virtuelle n’est pas présent sur l’ordinateur virtuel de hello - installez hello préalable indispensable, agent de machine virtuelle et redémarrez l’opération de hello. |[En savoir plus](#vm-agent) concernant l’installation de l’agent de machine virtuelle et comment toovalidate hello installation de l’agent de machine virtuelle. |

## <a name="backup"></a>Sauvegarde
| Opération de sauvegarde | Détails de l’erreur | Solution de contournement |
| --- | --- | --- |
| Sauvegarde |N’a pas pu communiquer avec l’agent de machine virtuelle hello pour l’état de l’instantané. La sous-tâche de capture instantanée machine virtuelle a expiré. -Consultez Résolution des problèmes de hello guide sur la façon de tooresolve cela. |Cette erreur est levée si un problème avec l’Agent de machine virtuelle de hello ou toohello d’accès réseau infrastructure Azure est bloquée d’une certaine façon. En savoir plus sur le [débogage des problèmes d’instantanés de machines virtuelles](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md). <br> Si l’agent de machine virtuelle hello n’est pas dû à des problèmes, puis redémarrez hello machine virtuelle. Parfois un état incorrect de la machine virtuelle peut entraîner des problèmes et le redémarrage de machine virtuelle de hello réinitialise cet « état incorrect » |
| Sauvegarde |La sauvegarde a échoué avec une erreur interne, réessayez l’opération hello dans quelques minutes. Si hello problème persiste, contactez le Support Microsoft |Veuillez vérifier s’il existe un problème temporaire d’accès au stockage de la machine virtuelle. Veuillez vérifier [Azure Status](https://azure.microsoft.com/en-us/status/) toosee absence de tout problème connexe toocompute / / réseau de stockage dans la région de hello en cours. Veuillez réessayer hello post sauvegarde problème soit réduite. |
| Sauvegarde |N’a pas pu effectuer les opération hello comme machine virtuelle n’existe plus. |Sauvegarde ne peut pas être effectuée car hello configuré pour la sauvegarde de machine virtuelle a été supprimé. Arrêtez les autres sauvegardes en vue des éléments de tooProtected va, sélectionnez l’élément protégé et cliquez sur Arrêter la Protection. Vous pouvez conserver les données en sélectionnant l’option Conserver les données de sauvegarde. Vous pouvez réactiver ultérieurement la protection de cette machine virtuelle en cliquant sur Configurer la protection dans la vue des éléments protégés. |
| Sauvegarde |Échec tooinstall hello extension Azure Recovery Services sur un élément sélectionné de hello - Agent de machine virtuelle est requis pour l’Extension de Services de récupération Azure. Installez l’agent de machine virtuelle Azure hello et redémarrez l’opération d’inscription de hello |<ol> <li>Vérifiez si l’agent de machine virtuelle hello a été installé correctement. <li>Vérifiez que hello sur la configuration de machine virtuelle hello est défini correctement.</ol> [En savoir plus](#validating-vm-agent-installation) concernant l’installation de l’agent de machine virtuelle et comment toovalidate hello installation de l’agent de machine virtuelle. |
| Sauvegarde |Échec de l’exécution de la commande - Une autre opération est en cours sur cet élément. Veuillez patienter pendant que l’opération précédente de hello est terminée et recommencez |Un travail de sauvegarde ou de restauration existant pour hello machine virtuelle est en cours d’exécution, et un nouveau travail ne peut pas être démarré pendant l’exécution de travail existant de hello. |
| Sauvegarde |Installation de l’extension a échoué avec l’erreur de hello « COM + n’a pas pu tootalk toohello Microsoft Distributed Transaction Coordinator |Cela signifie généralement que service COM + hello n’est pas en cours d’exécution. Pour résoudre ce problème, contactez le support Microsoft. |
| Sauvegarde |Opération d’instantané a échoué avec hello erreur VSS de l’opération « ce lecteur est verrouillé par le chiffrement de lecteur BitLocker. Vous devez déverrouiller ce lecteur à partir du panneau de configuration. |Désactiver BitLocker pour tous les lecteurs de machine virtuelle de hello et observez si hello VSS est résolu |
| Sauvegarde |Les machines virtuelles dotées de disques durs virtuels stockés sur le stockage Premium ne sont pas prises en charge par la sauvegarde |Aucun |
| Sauvegarde |Machine virtuelle Azure introuvable |Cela se produit lorsque hello ordinateur virtuel principal est supprimé, mais continue de stratégie de sauvegarde hello toolook pour une sauvegarde de tooperform de machine virtuelle. toofix cette erreur : <ol><li>Recréer la machine virtuelle hello hello même nom et le même nom de groupe de ressources [nom du service cloud,] <br>(OU) <li> Désactivez la protection de cette machine virtuelle pour empêcher le déclenchement des autres sauvegardes. </ol> |
| Sauvegarde |Agent de machine virtuelle n’est pas présent sur l’ordinateur virtuel de hello - installez hello préalable indispensable, agent de machine virtuelle et redémarrez l’opération de hello. |[En savoir plus](#vm-agent) concernant l’installation de l’agent de machine virtuelle et comment toovalidate hello installation de l’agent de machine virtuelle. |

## <a name="jobs"></a>Tâches
| Opération | Détails de l’erreur | Solution de contournement |
| --- | --- | --- |
| Annuler le travail |L’annulation n’est pas prise en charge pour ce type de tâche : Veuillez patienter pendant que le travail de hello est terminé. |Aucun |
| Annuler le travail |tâche de Hello n’est pas dans un état annulable - Veuillez patienter pendant que le travail de hello est terminé. <br>OU<br> tâche sélectionnée de Hello n’est pas dans un état annulable - Veuillez attendre hello travail toocomplete. |Selon toute probabilité, la tâche de hello est presque terminé ; Veuillez attendre la fin de travail de hello |
| Annuler le travail |Impossible d’annuler la tâche de hello, car il n’est pas en cours d’exécution, l’annulation est uniquement pris en charge pour les travaux qui sont en cours d’exécution. Veuillez tenter l’annulation de la tâche en cours d’exécution. |Cela se produit en raison de l’état transitoire de tooa. Patientez une minute et réessayez l’opération d’annulation hello |
| Annuler le travail |Échec toocancel hello travail - Patientez jusqu'à ce que la tâche se termine. |Aucun |

## <a name="restore"></a>Restauration
| Opération | Détails de l’erreur | Solution de contournement |
| --- | --- | --- |
| Restauration |Échec de la restauration avec une erreur interne du cloud |<ol><li>Toowhich de service cloud vous essayez de toorestore est configuré avec les paramètres DNS. Vous pouvez vérifier  <br>$deployment = Get-AzureDeployment -ServiceName "ServiceName" -Slot "Production"     Get-AzureDns -DnsSettings $deployment.DnsSettings<br>Si une adresse est configurée, cela signifie que les paramètres DNS sont configurés.<br> <li>Essayez de cloud service toowhich tooyou toorestore est configurée avec l’adresse IP réservée et machines virtuelles existantes dans le service cloud sont dans l’état arrêté.<br>Vous pouvez vérifier qu’un service cloud a une adresse IP réservée à l’aide des applets de commande PowerShell suivantes :<br>$deployment = Get-AzureDeployment -ServiceName "servicename" -Slot "Production" $dep.ReservedIPName <br><li>Vous essayez de toorestore une machine virtuelle avec des configurations réseau spéciales suivantes dans le service cloud toosame. <br>- Machines virtuelles avec configuration d’un équilibreur de charge (interne et externe)<br>- Machines virtuelles avec plusieurs adresses IP réservées<br>- Machines virtuelles avec plusieurs NIC<br>Veuillez sélectionner un nouveau service cloud dans l’interface utilisateur de hello ou reportez-vous trop[restaurer considérations](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations) pour les machines virtuelles avec des configurations de réseau spéciales</ol> |
| Restauration |nom DNS de Hello sélectionné est déjà utilisé - Veuillez spécifier un nom DNS différent, puis réessayez. |Hello nom DNS fait référence toohello nom du service cloud (généralement se terminant par. cloudapp.net). Cela doit toobe unique. Si vous rencontrez cette erreur, vous devez toochoose un autre nom d’ordinateur virtuel pendant la restauration. <br><br> Cette erreur s’affiche uniquement les toousers Hello portail Azure. Hello restauration via PowerShell réussit car il permet simplement restaure les disques hello et ne crée pas de hello machine virtuelle. Erreur de Hello sera être confrontée hello machine virtuelle est explicitement créé par vous-même après l’opération de restauration du disque hello. |
| Restauration |configuration de réseau virtuel spécifié Hello n’est pas correcte - Veuillez spécifier une configuration de réseau virtuel, puis réessayez. |Aucun |
| Restauration |Hello spécifié utilise une adresse IP réservée, qui ne correspond à la configuration d’ordinateur virtuel de hello en cours de restauration de hello - spécifiez un autre service cloud qui n’utilise pas d’adresse IP réservée ou choisissez un autre toorestore de point de récupération à partir de service cloud. |Aucun |
| Restauration |Service cloud a atteint la limite du nombre de points de terminaison d’entrée - hello nouvelle tentative en spécifiant un autre service cloud ou à l’aide d’un point de terminaison existant. |Aucun |
| Restauration |Compte de stockage cible et de coffre de sauvegarde dans les deux régions différentes, assurez-vous que le compte de stockage hello spécifié dans l’opération de restauration est Bonjour même région Azure que le coffre de sauvegarde hello. |Aucun |
| Restauration |Compte de stockage spécifié pour l’opération de restauration hello n’est pas pris en charge - comptes de stockage de base/Standard uniquement avec localement redondante ou géo réplication redondante sont pris en charge. Veuillez sélectionner un compte de stockage pris en charge |Aucun |
| Restauration |Type de compte de stockage spécifié pour l’opération de restauration n’est pas en ligne -, assurez-vous que le compte de stockage hello spécifié dans l’opération de restauration est en ligne |Cela peut se produire en raison d’une erreur temporaire dans le stockage Azure ou en raison de la panne de tooan. Veuillez choisir un autre compte de stockage. |
| Restauration |Quota de groupe de ressources a été atteint - supprimez des groupes de ressources à partir du portail Azure ou contactez le support Azure tooincrease hello limites. |Aucun |
| Restauration |Le sous-réseau sélectionné n’existe pas. Veuillez sélectionner un sous-réseau qui existe |Aucun |

## <a name="policy"></a>Stratégie
| Opération | Détails de l’erreur | Solution de contournement |
| --- | --- | --- |
| Créer une stratégie |Échec de la stratégie de hello toocreate - Veuillez réduire toocontinue de choix de rétention hello avec la configuration de la stratégie. |Aucun |

## <a name="vm-agent"></a>Agent VM
### <a name="setting-up-hello-vm-agent"></a>Configuration de hello Agent de machine virtuelle
En règle générale, hello Agent de machine virtuelle est déjà présent dans les machines virtuelles qui sont créés à partir de la galerie Azure de hello. Toutefois, les ordinateurs virtuels qui sont migrés à partir de centres de données locale n’aurait pas hello Agent VM est installé. Pour ces ordinateurs virtuels, hello Agent de machine virtuelle doit toobe installé de manière explicite. En savoir plus sur [agent de machine virtuelle hello lors de l’installation sur un ordinateur virtuel existant](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).

Pour les machines virtuelles Windows :

* Téléchargez et installez hello [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Vous devrez l’installation de l’administrateur des privilèges toocomplete hello.
* [Mettre à jour la propriété de machine virtuelle hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate qui hello agent est installé.

Pour les machines virtuelles Linux :

* Installez l’ [agent Linux](https://github.com/Azure/WALinuxAgent) le plus récent à partir de github.
* [Mettre à jour la propriété de machine virtuelle hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate qui hello agent est installé.

### <a name="updating-hello-vm-agent"></a>Mise à jour hello Agent de machine virtuelle
Pour les machines virtuelles Windows :

* Hello mise à jour l’Agent de machine virtuelle est aussi simple que la réinstallation hello [binaires de l’Agent de machine virtuelle](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Toutefois, vous devez tooensure aucune opération de sauvegarde n’est en cours d’exécution lors de l’Agent de machine virtuelle est en cours de mise à jour de hello.

Pour les machines virtuelles Linux :

* Suivez les instructions de hello [mise à jour d’un Agent de machine virtuelle Linux](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="validating-vm-agent-installation"></a>Validation de l’installation de l’agent de machine virtuelle
Comment toocheck pour hello version de l’Agent de machine virtuelle sur les machines virtuelles Windows :

1. Ouvrez une session toohello machine virtuelle Azure et accédez toohello dossier *C:\WindowsAzure\Packages*. Vous devez rechercher la présence du fichier WaAppAgent.exe hello.
2. Cliquez sur le fichier de hello, accédez trop**propriétés**, puis sélectionnez hello **détails** onglet hello Version du produit doit être 2.6.1198.718 ou une version ultérieure
