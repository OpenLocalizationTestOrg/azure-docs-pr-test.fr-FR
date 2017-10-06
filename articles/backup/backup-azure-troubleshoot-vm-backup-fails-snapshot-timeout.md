---
title: "Résolution des échecs de sauvegarde Azure : état de l’agent invité non disponible | Microsoft Docs"
description: "Symptômes, les causes et résolutions de tooerror connexe des échecs de sauvegarde Azure : pas pu communiquer avec l’agent de machine virtuelle hello"
services: backup
documentationcenter: 
author: genlin
manager: cshepard
editor: 
keywords: "Sauvegarde Azure ; agent de machine virtuelle ; connectivité réseau ;"
ms.assetid: 4b02ffa4-c48e-45f6-8363-73d536be4639
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: genli;markgal;
ms.openlocfilehash: 724c61ba80d0a9ef91a5f8543ae72bb86968881b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-backup-failure-issues-with-agent-andor-extension"></a>Résoudre les problèmes de sauvegarde Microsoft Azure : problèmes liés à un agent et/ou une extension

Cet article fournit la résolution des problèmes toohelp étapes vous résolvez les échecs de sauvegarde associées tooproblems en communication avec l’agent de machine virtuelle et l’extension.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="vm-agent-unable-toocommunicate-with-azure-backup"></a>Toocommunicate Impossible d’Agent de machine virtuelle avec Azure Backup
Une fois que vous enregistrez, planifiez une machine virtuelle pour hello service Azure Backup, sauvegarde lance la tâche de hello en communiquant avec hello tootake de l’agent de machine virtuelle un instantané de point-à-temps. Une des conditions suivantes de hello peut empêcher la capture instantanée hello de déclenchement, qui à son tour peut provoquer une panne de tooBackup. Suivez les étapes de hello donné l’ordre de résolution des problèmes et recommencez l’opération.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Cause 1 : [hello machine virtuelle n’a pas accès Internet](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Cause 2 : [l’agent de hello est installé dans hello machine virtuelle, mais ne répond pas (pour les machines virtuelles Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Cause 3 : [agent hello installé Bonjour machine virtuelle est obsolète (pour les machines virtuelles Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Cause 4 : [Impossible de récupérer l’état d’instantané hello ou un instantané ne peut pas être effectuée.](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Cause 5 : [extension de sauvegarde hello échoue tooupdate ou la charge](#the-backup-extension-fails-to-update-or-load)

## <a name="snapshot-operation-failed-due-toono-network-connectivity-on-hello-virtual-machine"></a>Opération d’instantané a échoué en raison de la connectivité de réseau toono sur l’ordinateur virtuel de hello
Une fois que vous enregistrez, planifiez une machine virtuelle pour hello service Azure Backup, sauvegarde lance la tâche de hello en communiquant avec un instantané de tootake un point-à-temps hello VM extension de sauvegarde. Une des conditions suivantes de hello peut empêcher la capture instantanée hello de déclenchement, qui à son tour peut provoquer une panne de tooBackup. Suivez les étapes de hello donné l’ordre de résolution des problèmes et recommencez l’opération.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Cause 1 : [hello machine virtuelle n’a pas accès Internet](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Cause 2 : [Impossible de récupérer l’état d’instantané hello ou un instantané ne peut pas être effectuée.](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-3-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Cause 3 : [extension de sauvegarde hello échoue tooupdate ou la charge](#the-backup-extension-fails-to-update-or-load)

## <a name="vmsnapshot-extension-operation-failed"></a>Échec de l’opération d’extension VMSnapshot

Une fois que vous enregistrez, planifiez une machine virtuelle pour hello service Azure Backup, sauvegarde lance la tâche de hello en communiquant avec un instantané de tootake un point-à-temps hello VM extension de sauvegarde. Une des conditions suivantes de hello peut empêcher la capture instantanée hello de déclenchement, qui à son tour peut provoquer une panne de tooBackup. Suivez les étapes de hello donné l’ordre de résolution des problèmes et recommencez l’opération.
##### <a name="cause-1-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Cause 1 : [Impossible de récupérer l’état d’instantané hello ou un instantané ne peut pas être effectuée.](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-2-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Cause 2 : [extension de sauvegarde hello échoue tooupdate ou la charge](#the-backup-extension-fails-to-update-or-load)
##### <a name="cause-3-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Cause 3 : [hello machine virtuelle n’a pas accès Internet](#the-vm-has-no-internet-access)
##### <a name="cause-4-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Cause 4 : [agent de hello est installé dans hello machine virtuelle, mais ne répond pas (pour les machines virtuelles Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-5-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Cause 5 : [agent hello installé Bonjour machine virtuelle est obsolète (pour les machines virtuelles Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)

## <a name="unable-tooperform-hello-operation-as-hello-vm-agent-is-not-responsive"></a>Opération impossible tooperform hello hello Agent de machine virtuelle ne répond pas

Une fois que vous enregistrez, planifiez une machine virtuelle pour hello service Azure Backup, sauvegarde lance la tâche de hello en communiquant avec un instantané de tootake un point-à-temps hello VM extension de sauvegarde. Une des conditions suivantes de hello peut empêcher la capture instantanée hello de déclenchement, qui à son tour peut provoquer une panne de tooBackup. Suivez les étapes de hello donné l’ordre de résolution des problèmes et recommencez l’opération.
##### <a name="cause-1-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Cause 1 : [agent de hello est installé dans hello machine virtuelle, mais ne répond pas (pour les machines virtuelles Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-2-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Cause 2 : [agent hello installé Bonjour machine virtuelle est obsolète (pour les machines virtuelles Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-3-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Cause 3 : [hello machine virtuelle n’a pas accès Internet](#the-vm-has-no-internet-access)

## <a name="backup-failed-with-an-internal-error---please-retry-hello-operation-in-a-few-minutes"></a>La sauvegarde a échoué avec une erreur interne, réessayez l’opération hello dans quelques minutes

Une fois que vous enregistrez, planifiez une machine virtuelle pour hello service Azure Backup, sauvegarde lance la tâche de hello en communiquant avec un instantané de tootake un point-à-temps hello VM extension de sauvegarde. Une des conditions suivantes de hello peut empêcher la capture instantanée hello de déclenchement, qui à son tour peut provoquer une panne de tooBackup. Suivez les étapes de hello donné l’ordre de résolution des problèmes et recommencez l’opération.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Cause 1 : [hello machine virtuelle n’a pas accès Internet](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-agent-installed-in-hello-vm-but-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Cause 2 : [agent hello installé Bonjour machine virtuelle, mais ne répond pas (pour les machines virtuelles Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Cause 3 : [agent hello installé Bonjour machine virtuelle est obsolète (pour les machines virtuelles Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Cause 4 : [Impossible de récupérer l’état d’instantané hello ou un instantané ne peut pas être effectuée.](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Cause 5 : [extension de sauvegarde hello échoue tooupdate ou la charge](#the-backup-extension-fails-to-update-or-load)


## <a name="causes-and-solutions"></a>Causes et solutions

### <a name="hello-vm-has-no-internet-access"></a>Hello machine virtuelle n’a pas accès Internet
Par la spécification de déploiement hello hello machine virtuelle a sans accès à Internet, ou en place, les restrictions qui empêchent les accès toohello infrastructure Azure.

toofunction correctement, extension de sauvegarde hello nécessite des adresses IP public Azure toohello de connectivité. extension de Hello envoie des commandes tooan Azure Storage point de terminaison (URL HTTP) toomanage hello des instantanés de hello machine virtuelle. Si l’extension de hello ne possède aucun toohello accès Qu'internet public, par la suite de sauvegarde échoue.

####  <a name="solution"></a>Solution
problème de hello tooresolve, essayez l’une des méthodes hello répertoriées ici.
##### <a name="allow-access-toohello-azure-datacenter-ip-ranges"></a>Autoriser l’accès à des plages IP toohello centre de données Azure

1. Obtenir hello [la liste des adresses IP de centre de données Azure](https://www.microsoft.com/download/details.aspx?id=41653) accès tooallow à.
2. Débloquer hello IPs en exécutant hello **New-NetRoute** applet de commande Bonjour Azure VM dans une fenêtre PowerShell avec élévation de privilèges. Exécutez l’applet de commande hello en tant qu’administrateur.
3. tooallow accès toohello IPs, ajouter le groupe de sécurité de règles toohello réseau, si vous en avez.

##### <a name="create-a-path-for-http-traffic-tooflow"></a>Créer un chemin d’accès pour tooflow du trafic HTTP

1. Si vous avez des restrictions de réseau en place (par exemple, un groupe de sécurité réseau), déployez un serveur tooroute hello du trafic proxy HTTP.
2. tooallow accès toohello Internet à partir du serveur de proxy HTTP hello, ajouter le groupe de sécurité de règles toohello réseau, si vous en avez.

toolearn tooset d’un proxy HTTP pour les sauvegardes d’ordinateurs virtuels, voir [préparer votre tooback environnement des machines virtuelles](backup-azure-vms-prepare.md#using-an-http-proxy-for-vm-backups).

Si vous utilisez des disques gérés, vous devrez peut-être d’un port supplémentaire (8443) ouvrant sur les pare-feux hello.

### <a name="hello-agent-installed-in-hello-vm-but-unresponsive-for-windows-vms"></a>agent de Hello installé Bonjour machine virtuelle, mais ne répond pas (pour les machines virtuelles Windows)

#### <a name="solution"></a>Solution
Hello Agent de machine virtuelle peut être endommagé ou le service de hello a peut-être été arrêté. Réinstaller l’agent de machine virtuelle hello peut vous aider à obtenir la version la plus récente hello et redémarrer la communication de hello.

1. Vérifiez si le service de l’Agent invité de Windows en cours d’exécution dans les services (services.msc) de hello Machine virtuelle. Essayez de redémarrer le service de l’Agent invité de Windows hello et lancer hello sauvegarde<br>
2. S’il ne figure pas dans les services, vérifiez si le service d’agent invité Windows est installé sous Programmes et fonctionnalités.
4. Si vous êtes en mesure de tooview dans programmes et fonctionnalités hello de désinstaller l’Agent invité de Windows.
5. Téléchargez et installez hello [version la plus récente de l’agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Vous avez besoin d’installation de l’administrateur des privilèges toocomplete hello.
6. Ensuite, vous devez être en mesure de tooview des services de l’Agent invité de Windows dans les services
7. Essayez d’exécuter une sauvegarde adhoc / l’à la demande en cliquant sur « sauvegarde » dans le portail de hello.

Vérifiez également votre Machine virtuelle a  **[.NET 4.5 est installé dans le système de hello](https://docs.microsoft.com/en-us/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed)**. Il est requis pour toocommunicate de l’agent de machine virtuelle hello avec le service de hello

### <a name="hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vms"></a>agent Hello installé Bonjour machine virtuelle est obsolète (pour les machines virtuelles Linux)

#### <a name="solution"></a>Solution
La plupart des échecs des machines virtuelles Linux liés aux agents ou aux extensions sont causés par des problèmes qui affectent un agent obsolète de machine virtuelle. tootroubleshoot ce problème, suivez ces recommandations générales :

1. Suivez les instructions de hello pour [mise à jour de l’agent Linux VM de hello](../virtual-machines/linux/update-agent.md).

 >[!NOTE]
 >Nous *recommandons* que vous mettez à jour l’agent hello uniquement par le biais d’un référentiel de distribution. Il est déconseillé de téléchargement de code de l’agent hello directement à partir de GitHub et mettre à jour. Si l’agent plus récent hello n’est pas disponible pour votre distribution, contactez le support de distribution pour obtenir des instructions sur la façon de tooinstall il. toocheck pour hello plus récente de l’agent, accédez toohello [agent Windows Azure Linux](https://github.com/Azure/WALinuxAgent/releases) page dans le référentiel GitHub de hello.

2. Assurez-vous que l’agent Azure hello est en cours d’exécution sur hello machine virtuelle en exécutant hello de commande suivante :`ps -e`

 Si le processus de hello ne fonctionne pas, redémarrez-le à l’aide de hello suivant de commandes :

 * Pour Ubuntu : `service walinuxagent start`
 * Pour les autres distributions : `service waagent start`

3. [Configurer l’agent de redémarrage automatique hello](https://github.com/Azure/WALinuxAgent/wiki/Known-Issues#mitigate_agent_crash).
4. Exécutez une nouvelle sauvegarde de test. Si hello erreur persiste, veuillez collecter hello suivant des journaux à partir VM du client hello :

   * /var/lib/waagent/*.xml
   * /var/log/waagent.log
   * /var/log/azure/*

Si nous exigeons une journalisation détaillée pour waagent, procédez comme suit :

1. Dans le fichier de /etc/waagent.conf hello, recherchez hello ligne suivante : **activer la journalisation documentée (y | n)**
2. Hello de modification **Logs.Verbose** valeur  *n*  trop*y*.
3. Enregistrer les modifications de hello et redémarrez waagent en suivant les étapes précédentes de hello dans cette section.

### <a name="hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Impossible de récupérer l’état d’instantané Hello ou un instantané ne peut pas être effectuée.
sauvegarde de machine virtuelle Hello s’appuie sur l’émission d’un compte de stockage sous-jacent instantané commande toohello. Sauvegarde peut échouer car il ne dispose d’aucun compte de stockage toohello accès ou exécution hello de tâche d’instantané hello est retardée.

#### <a name="solution"></a>Solution
Hello conditions suivantes peut entraîner l’échec de la tâche instantané :

| Cause : | Solution |
| --- | --- |
| Hello machine virtuelle dispose d’une sauvegarde SQL Server configurée. | Par défaut, sauvegarde de machine virtuelle hello exécute une sauvegarde complète VSS sur les machines virtuelles Windows. Sur les machines virtuelles exécutant des serveurs basés sur SQL Server et sur lesquelles la sauvegarde SQL Server est configurée, des retards d’exécution des captures instantanées peuvent survenir.<br><br>Si vous rencontrez une défaillance de la sauvegarde en raison d’un problème de capture instantanée, définissez hello clé de Registre suivante :<br><br>**[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT] "USEVSSCOPYBACKUP"="TRUE"** |
| Hello, état de la machine virtuelle est signalée incorrectement car hello machine virtuelle est arrêté dans RDP. | Si vous arrêtez hello VM de protocole RDP (Remote Desktop), vérifiez les toodetermine portail hello si hello état de la machine virtuelle est correct. Si elle n’est pas correcte, arrêtez hello machine virtuelle dans le portail de hello à l’aide de hello **arrêt** option sur le tableau de bord hello VM. |
| Plusieurs machines virtuelles à partir de hello sont du même service cloud configuré tooback à hello même temps. | Il s’agit d’une meilleure toospread de pratique des planifications de sauvegarde hello pour les machines virtuelles à partir de hello même service cloud. |
| Hello machine virtuelle est en cours d’exécution à une utilisation élevée du processeur ou de la mémoire. | Si hello machine virtuelle est en cours d’exécution à l’utilisation du processeur élevée (plus de 90 pour cent) ou l’utilisation de mémoire haute, tâche d’instantané hello est en file d’attente retardée et qu’il n’expire par la suite. En pareille situation, essayez de procéder à une sauvegarde à la demande. |
| Hello machine virtuelle ne peut pas obtenir adresse d’hôte / l’ensemble fibre optique hello du serveur DHCP. | DHCP doit être activé dans invité hello pour hello toowork de sauvegarde IaaS VM.  Si hello machine virtuelle ne peut pas obtenir hello hôte / l’ensemble fibre optique adresse de réponse DHCP 245, il ne peut pas télécharger ou exécuter des extensions. Si vous avez besoin d’une adresse IP privée statique, vous devez le configurer via la plateforme de hello. Bonjour à l’option DHCP à l’intérieur de hello machine virtuelle doit rester activée. Pour en savoir plus, consultez la [définition d’une adresse IP privée interne statique](../virtual-network/virtual-networks-reserved-private-ip.md). |

### <a name="hello-backup-extension-fails-tooupdate-or-load"></a>Échec de l’extension de sauvegarde Hello tooupdate ou la charge
Si les extensions ne peuvent pas être chargées, la sauvegarde échoue en raison de l’impossibilité de capturer un instantané.

#### <a name="solution"></a>Solution

**Pour les invités Windows :** Vérifiez que le service d’iaasvmprovider hello est activé et a un type de démarrage *automatique*. Si le service de hello n’est pas configuré de cette façon, activez-la toodetermine si hello de sauvegarde suivant réussit.

**Pour les invités Linux sont disponibles :** Vérifiez hello dernière version de VMSnapshot pour Linux (extension hello utilisée par la sauvegarde) est 1.0.91.0.<br>


Si l’extension de sauvegarde hello échoue toujours tooupdate ou la charge, vous pouvez forcer hello VMSnapshot extension toobe rechargé en désinstallant l’extension de hello. tentative de sauvegarde suivant Hello recharge les extension hello.

toouninstall hello extension, hello suivant :

1. Accédez toohello [portail Azure](https://portal.azure.com/).
2. Recherchez hello machine virtuelle qui a des problèmes de sauvegarde.
3. Cliquez sur **Settings**.
4. Cliquez sur **Extensions**.
5. Cliquez sur **Extension Vmsnapshot**.
6. Cliquer sur **Désinstaller**.

Cette procédure entraîne toobe d’extension hello réinstallé lors de la sauvegarde suivante de hello.

