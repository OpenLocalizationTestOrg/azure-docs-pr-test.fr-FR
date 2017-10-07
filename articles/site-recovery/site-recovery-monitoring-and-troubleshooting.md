---
title: "aaaMonitor et résoudre les problèmes de protection pour les serveurs physiques et virtuels | Documents Microsoft"
description: "Azure Site Recovery coordonne la réplication hello, le basculement et récupération des machines virtuelles situées sur tooAzure des serveurs locaux ou d’un centre de données secondaire. Utilisez cette toomonitor article et résoudre les problèmes de protection de site de Virtual Machine Manager ou Hyper-V."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 0fc8e368-0c0e-4bb1-9d50-cffd5ad0853f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: d790375db5f30e98f009c8d8272558188c51934c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-troubleshoot-protection-for-virtual-machines-and-physical-servers"></a>Surveiller et résoudre les problèmes de protection pour les machines virtuelles et les serveurs physiques
Cette analyse et la résolution des problèmes du guide vous aide à vous apprendre comment tootrack intégrité de la réplication et résoudre les problèmes techniques pour Azure Site Recovery.

## <a name="understand-hello-components"></a>Comprendre les composants hello
### <a name="vmware-virtual-machine-or-physical-server-site-deployment-for-replication-between-on-premises-and-azure"></a>Déploiement d’une machine virtuelle VMware ou d’un serveur physique à répliquer entre un site local et Azure
tooset la récupération de la base de données entre un ordinateur virtuel VMware sur local, ou de serveur physique et de Azure, vous devez tooset des serveur de configuration hello, serveur cible maître et des composants de serveur de processus sur votre ordinateur virtuel ou le serveur. Lorsque vous activez la protection pour le serveur de source de hello, Azure Site Recovery installe hello applications mobiles de Microsoft Azure App Service. Après une panne sur site et après hello source server tooAzure bascule, les clients doivent tooset d’un serveur de traitement dans Azure et un serveur cible maître sur un serveur local toorebuild hello source local.

![Déploiement d’un site VMware/physique à répliquer entre un site local et Azure](media/site-recovery-monitoring-and-troubleshooting/image18.png)

### <a name="virtual-machine-manager-site-deployment-for-replication-between-on-premises-sites"></a>Déploiement d’un site VMM (Virtual Machine Manager) à répliquer entre des sites locaux
tooset la récupération de la base de données entre deux emplacements sur site, vous avez besoin du fournisseur Azure Site Recovery de hello toodownload et installez sur le serveur Virtual Machine Manager de hello. fournisseur de Hello doit tooensure de connectivité Internet que local tooon traduites opérations d’obtention de toutes les opérations de hello qui sont déclenchées à partir de hello portail Azure.

![Déploiement d’un site VMM (Virtual Machine Manager) à répliquer entre des sites locaux](media/site-recovery-monitoring-and-troubleshooting/image1.png)

### <a name="virtual-machine-manager-site-deployment-for-replication-between-on-premises-locations-and-azure"></a>Déploiement d’un site VMM (Virtual Machine Manager) à répliquer entre des sites locaux et Azure
Lorsque vous définissez la récupération de la base de données entre les emplacements sur site et Azure, vous devez fournisseur Azure Site Recovery de hello toodownload et l’installer sur le serveur Virtual Machine Manager de hello. Vous devez également tooinstall hello Azure Recovery Services Agent, qui doit toobe installé sur chaque hôte Hyper-V. [Cliquez ici](site-recovery-hyper-v-azure-architecture.md) pour plus d’informations.

![Déploiement d’un site VMM (Virtual Machine Manager) à répliquer entre des sites locaux et Azure](media/site-recovery-monitoring-and-troubleshooting/image2.png)

### <a name="hyper-v-site-deployment-for-replication-between-on-premises-locations-and-azure"></a>Déploiement d’un site Hyper-V à répliquer entre des sites locaux et Azure
Ce processus est le déploiement de Machine Manager tooVirtual similaires. Bonjour seule différence est que le fournisseur Azure Site Recovery hello et Azure Recovery Services Agent installé sur l’hôte Hyper-V de hello lui-même. [En savoir plus](site-recovery-hyper-v-azure-architecture.md). .

## <a name="monitor-configuration-protection-and-recovery-operations"></a>Surveillance des opérations de configuration, de protection et de récupération
Chaque opération dans Azure Site Recovery est auditée et suivie sous hello **travaux** onglet. Pour toute configuration, la protection ou erreur de récupération, accédez à toohello **travaux** onglet et recherchez des pannes.

![filtre d’échec Hello sous l’onglet tâches de hello](media/site-recovery-monitoring-and-troubleshooting/image3.png)

Si vous trouvez des erreurs sous hello **travaux** onglet, cliquez sur la tâche hello et cliquez sur **détails de l’erreur** de ce travail.

![bouton des détails de l’erreur Hello](media/site-recovery-monitoring-and-troubleshooting/image4.png)

Détails de l’erreur Hello vous aidera à identifier la cause et la recommandation pour le problème de hello.

![Boîte de dialogue affichant les détails de l’erreur d’une tâche spécifique](media/site-recovery-monitoring-and-troubleshooting/image5.png)

Dans l’exemple précédent de hello, une autre opération est en cours d’exécution peut paraître toobe à l’origine de toofail de configuration de protection hello. Résoudre les problème de hello selon la recommandation de hello, puis cliquez sur **redémarrez votre** opération hello tooinitiate.

![bouton de redémarrage Hello sous l’onglet tâches de hello](media/site-recovery-monitoring-and-troubleshooting/image6.png)

Hello **redémarrer** option n’est pas disponible pour toutes les opérations. Si une opération n’a pas hello **redémarrer** option, de revenir en arrière toohello objet et de restauration par progression opération hello. Vous pouvez annuler un travail qui est en cours d’exécution à l’aide de hello **Annuler** bouton.

![bouton d’annulation Hello](media/site-recovery-monitoring-and-troubleshooting/image7.png)

## <a name="monitor-replication-health-for-virtual-machines"></a>Surveillance de l’intégrité de la réplication des machines virtuelles
Vous pouvez utiliser les fournisseurs d’Azure Site Recovery moniteur hello tooremotely portail Azure pour chacune des entités de hello protégé. Cliquez sur **ÉLÉMENTS PROTÉGÉS**, puis sur **CLOUDS VMM** ou **GROUPES DE PROTECTION**. Hello **CLOUDS VMM** onglet n’est disponible pour les déploiements qui sont basées sur Virtual Machine Manager. Pour d’autres scénarios, les entités hello protégé sont sous hello **groupes de PROTECTION** onglet.

![options de Clouds VMM et des groupes de PROTECTION de Hello](media/site-recovery-monitoring-and-troubleshooting/image8.png)

Cliquez sur une entité protégée sous hello respectifs cloud ou protection groupe toosee que toutes les opérations disponibles sont affichées dans le volet du bas hello.

![Options disponibles pour une entité protégée sélectionnée](media/site-recovery-monitoring-and-troubleshooting/image9.png)

Comme indiqué dans la capture d’écran précédente hello, contrôle d’intégrité de la machine virtuelle hello est **critique**. Vous pouvez cliquer sur hello **détails de l’erreur** bouton en cas d’erreur de hello toosee hello bas. En fonction de hello **les causes possibles** et **recommandation**, résoudre le problème de hello.

![bouton des détails de l’erreur Hello](media/site-recovery-monitoring-and-troubleshooting/image10.png)

![Erreurs et les recommandations contenues dans la boîte de dialogue Détails de l’erreur hello](media/site-recovery-monitoring-and-troubleshooting/image11.png)

> [!NOTE]
> Si toutes les opérations actives en cours d’exécution ou a échoué, accédez à toohello **travaux** vue comme mentionné erreur hello tooview antérieure d’un travail spécifique.
>
>

## <a name="troubleshoot-on-premises-hyper-v-issues"></a>Résolution des problèmes Hyper-V locaux
Connecter la console du Gestionnaire Hyper-V toohello local, sélectionnez hello virtual machine et voir l’intégrité de la réplication hello.

![Intégrité de la réplication tooview option dans la console du Gestionnaire Hyper-V de hello](media/site-recovery-monitoring-and-troubleshooting/image12.png)

En l’occurrence, l’**intégrité de la réplication** est **Critique**. Machine virtuelle de hello d’avec le bouton droit, puis cliquez sur **réplication** > **afficher l’intégrité de la réplication** détails de hello toosee.

![Intégrité de la réplication d’une machine virtuelle](media/site-recovery-monitoring-and-troubleshooting/image13.png)

Si la réplication est suspendue pour la machine virtuelle de hello, avec le bouton droit hello virtual machine, puis cliquez sur **réplication** > **reprendre la réplication**.

![Option de réplication dans la console du Gestionnaire Hyper-V de hello tooresume](media/site-recovery-monitoring-and-troubleshooting/image19.png)

Si un ordinateur virtuel migre un nouvel hôte Hyper-V qui se trouve dans un cluster de hello ou un ordinateur autonome et l’ordinateur hôte Hyper-V de hello a été configuré via Azure Site Recovery, réplication pour la machine virtuelle de hello ne pourraient être touchée. Vérifiez que hôte Hyper-V de nouveau hello répond à toutes les conditions préalables de hello et qu’il est configuré à l’aide d’Azure Site Recovery.

### <a name="event-log"></a>Journal des événements
| Sources d’événement | Détails |
| --- |:--- |
| **Journaux des applications et des services/Microsoft/VirtualMachineManager/Server/Admin** (serveur Virtual Machine Manager) |Fournit des tootroubleshoot de journalisation utile de nombreux autres facteurs de Virtual Machine Manager. |
| **Journaux des applications et des services/MicrosoftAzureRecoveryServices/Replication** (hôte Hyper-V) |Fournit des nombreux problèmes de Microsoft Azure Recovery Services Agent tootroubleshoot de journalisation utile. <br/> ![Emplacement de la source d’événements de réplication de l’hôte Hyper-V](media/site-recovery-monitoring-and-troubleshooting/eventviewer03.png) |
| **Journaux des applications et des services/Microsoft/Azure Site Recovery/Provider/Operational** (hôte Hyper-V) |Fournit des nombreux problèmes de Service Microsoft Azure Site Recovery tootroubleshoot de journalisation utile. <br/> ![Emplacement de la source d’événements opérationnels de l’hôte Hyper-V](media/site-recovery-monitoring-and-troubleshooting/eventviewer02.png) |
| **Journaux des applications et des services/Microsoft/Windows/Hyper-V-VMMS/Admin** (hôte Hyper-V) |Fournit journalisation utile tootroubleshoot de nombreux problèmes de gestion d’ordinateur virtuel Hyper-V. <br/> ![Emplacement de la source d’événements Virtual Machine Manager de l’hôte Hyper-V](media/site-recovery-monitoring-and-troubleshooting/eventviewer01.png) |

### <a name="hyper-v-replication-logging-options"></a>Options de journalisation de réplication Hyper-V
Tous les événements qui se rapportent à la réplication tooHyper-V sont enregistrés Bonjour Hyper-V-VMMS\\Admin journal situé sous journaux des Applications et Services\\Microsoft\\Windows. En outre, vous pouvez activer un journal d’analyse pour hello Service de gestion d’ordinateur virtuel Hyper-V. tooenable ce journal, effectuez d’abord hello analyse, de journaux de débogage peut être affiché dans l’Observateur d’événements de hello. Ouvrez l’Observateur d’événements, puis cliquez sur **Affichage** > **Afficher les journaux d’analyse et de débogage**.

![Hello option Afficher les journaux d’analyse et de débogage](media/site-recovery-monitoring-and-troubleshooting/image14.png)

Un journal d’analyse s’affiche sous **Hyper-V-VMMS**.

![Ouvrez une session dans l’arborescence de l’Observateur d’événements hello Hello analyse](media/site-recovery-monitoring-and-troubleshooting/image15.png)

Bonjour **Actions** volet, cliquez sur **activer le journal**. Une fois activé, il apparaît dans **Analyseur de performances** comme une **Session de suivi d’événements** située sous **Ensembles de collecteurs de données**.

![Sessions de suivi d’événements dans l’arborescence de l’Analyseur de performances hello](media/site-recovery-monitoring-and-troubleshooting/image16.png)

tooview hello les informations collectées, arrêtez d’abord session de suivi hello en désactivant le journal de hello. Enregistrer le journal de hello et ouvrez de nouveau dans l’Observateur d’événements ou utiliser d’autres outils tooconvert il comme vous le souhaitez.

## <a name="reach-out-for-microsoft-support"></a>Contacter le support Microsoft
### <a name="log-collection"></a>Collection de journaux
Pour la protection de site de Virtual Machine Manager, consultez trop[collecte des journaux Azure Site Recovery à l’aide de la prise en charge des Diagnostics plate-forme (SDP) outil](http://social.technet.microsoft.com/wiki/contents/articles/28198.asr-data-collection-and-analysis-using-the-vmm-support-diagnostics-platform-sdp-tool.aspx) toocollect hello requis des journaux.

Pour la protection de site Hyper-V, vous devez télécharger le [outil](https://dcupload.microsoft.com/tools/win7files/DIAG_ASRHyperV_global.DiagCab) et exécutez-le sur les journaux de hello toocollect hello Hyper-V hôte.

Pour les scénarios de serveurs VMware/physiques, voir la rubrique trop[collecte de journaux d’Azure Site Recovery pour VMware et la protection de site physique](http://social.technet.microsoft.com/wiki/contents/articles/30677.azure-site-recovery-log-collection-for-vmware-and-physical-site-protection.aspx) toocollect hello requis des journaux.

outil de Hello collecte des journaux de hello localement dans un sous-dossier nommé de façon aléatoire sous % LocalAppData%\ElevatedDiagnostics.

![Exemples d’étapes provenant de la protection du site Hyper-V.](media/site-recovery-monitoring-and-troubleshooting/animate01.gif)

### <a name="open-a-support-ticket"></a>Ouverture d’un ticket de support
tooraise un ticket de support pour Azure Site Recovery, atteindre tooAzure prise en charge à l’aide de l’URL à <http://aka.ms/getazuresupport>.

## <a name="kb-articles"></a>Articles de la Base de connaissances
* [Comment toopreserve lettre de lecteur hello pour protégés des ordinateurs virtuels qui sont basculés ou migré tooAzure](http://support.microsoft.com/kb/3031135)
* [Comment toomanage local tooAzure protection de bande passante](https://support.microsoft.com/kb/3056159)
* [Erreur d’Azure Site Recovery : « ressource de cluster hello introuvable » lorsque vous essayez de protection tooenable pour un ordinateur virtuel](http://support.microsoft.com/kb/3010979)
* [Guide de présentation et de résolution des problèmes relatifs à la réplication Hyper-V](http://social.technet.microsoft.com/wiki/contents/articles/21948.hyper-v-replica-troubleshooting-guide.aspx)

## <a name="common-azure-site-recovery-errors-and-their-resolutions"></a>Erreurs liées à Azure Site Recovery et résolution
Les erreurs suivantes et leurs résolutions sont courantes. Chaque erreur est documentée dans une page WIKI dédiée.

### <a name="general"></a>Généralités
* <span style="color:green;">NOUVEAU</span>[Échec de travaux avec l’erreur « Une opération est en cours ». Erreur 505, 514, 532.](http://social.technet.microsoft.com/wiki/contents/articles/32190.azure-site-recovery-jobs-failing-with-error-an-operation-is-in-progress-error-505-514-532.aspx)
* <span style="color:green;">NOUVELLE</span> [tâches ont échoué avec l’erreur « Le serveur n’est pas connecté toohello Internet ». Erreur 25018.](http://social.technet.microsoft.com/wiki/contents/articles/32192.azure-site-recovery-jobs-failing-with-error-server-isn-t-connected-to-the-internet-error-25018.aspx)

### <a name="setup"></a>Paramétrage
* [serveur Virtual Machine Manager de Hello ne peut pas être inscrit en raison de l’erreur interne de tooan. Consultez Vue tâches toohello portail de Site Recovery hello pour plus d’informations sur l’erreur de hello. Exécutez le programme d’installation à nouveau le serveur de hello tooregister.](http://social.technet.microsoft.com/wiki/contents/articles/25570.the-vmm-server-cannot-be-registered-due-to-an-internal-error-please-refer-to-the-jobs-view-in-the-site-recovery-portal-for-more-details-on-the-error-run-setup-again-to-register-the-server.aspx)
* [Une connexion ne peut pas être établie toohello le coffre Hyper-V Recovery Manager. Vérifiez les paramètres de proxy hello ou réessayez plus tard.](http://social.technet.microsoft.com/wiki/contents/articles/25571.a-connection-cant-be-established-to-the-hyper-v-recovery-manager-vault-verify-the-proxy-settings-or-try-again-later.aspx)

### <a name="configuration"></a>Configuration
* [Impossible de toocreate groupe de Protection : une erreur s’est produite lors de la récupération hello serveurs.](http://blogs.technet.com/b/somaning/archive/2015/08/12/unable-to-create-the-protection-group-in-azure-site-recovery-portal.aspx)
* [Cluster hôte Hyper-V contient au moins une carte réseau statique, ou aucune carte connectée n’est toouse configuré DHCP.](http://social.technet.microsoft.com/wiki/contents/articles/25498.hyper-v-host-cluster-contains-at-least-one-static-network-adapter-or-no-connected-adapters-are-configured-to-use-dhcp.aspx)
* [Virtual Machine Manager n’a pas d’autorisations toocomplete une action.](http://social.technet.microsoft.com/wiki/contents/articles/31110.vmm-does-not-have-permissions-to-complete-an-action.aspx)
* [Impossible de sélectionner le compte de stockage hello au sein de l’abonnement hello lors de la configuration de la protection.](http://social.technet.microsoft.com/wiki/contents/articles/32027.can-t-select-the-storage-account-within-the-subscription-while-configuring-protection.aspx)

### <a name="protection"></a>Protection
* <span style="color:green;">NOUVELLE</span> [activer la Protection échoue avec l’erreur « Protection n’a pas pu être configurée pour l’ordinateur virtuel de hello ». Erreur 60007, 40003.](http://social.technet.microsoft.com/wiki/contents/articles/32194.azure-site-recovery-enable-protection-failing-with-error-protection-couldn-t-be-configured-for-the-virtual-machine-error-60007-40003.aspx)
* <span style="color:green;">NOUVELLE</span> [activer la Protection échoue avec l’erreur « Impossible d’activer la Protection pour la machine virtuelle de hello. » Erreur 70094.](http://social.technet.microsoft.com/wiki/contents/articles/32195.azure-site-recovery-enable-protection-failing-with-error-protection-couldn-t-be-enabled-for-the-virtual-machine-error-70094.aspx)
* <span style="color:green;">NOUVELLE</span> [toobe déplacé à l’aide du type Live est en train de migration dynamique erreur 23848 - machine virtuelle de hello. Cela peut endommager l’état de protection de récupération de hello de machine virtuelle de hello.](http://social.technet.microsoft.com/wiki/contents/articles/32021.live-migration-error-23848-the-virtual-machine-is-going-to-be-moved-using-type-live-this-could-break-the-recovery-protection-status-of-the-virtual-machine.aspx)
* [Échec de l’activation de la protection, car l’agent n’est pas installé sur la machine hôte.](http://social.technet.microsoft.com/wiki/contents/articles/31105.enable-protection-failed-since-agent-not-installed-on-host-machine.aspx)
* [Impossible de trouver un hôte approprié pour l’ordinateur virtuel de réplication hello - en raison de ressources de calcul toolow.](http://social.technet.microsoft.com/wiki/contents/articles/25501.a-suitable-host-for-the-replica-virtual-machine-can-t-be-found-due-to-low-compute-resources.aspx)
* [Impossible de trouver un hôte approprié pour l’ordinateur virtuel de réplication hello - échéance toono attachés au réseau logique.](http://social.technet.microsoft.com/wiki/contents/articles/25502.a-suitable-host-for-the-replica-virtual-machine-can-t-be-found-due-to-no-logical-network-attached.aspx)
* [Impossible de se connecter ordinateur hôte de réplica toohello - connexion n’a pas pu être établie.](http://social.technet.microsoft.com/wiki/contents/articles/31106.cannot-connect-to-the-replica-host-machine-connection-could-not-be-established.aspx)

### <a name="recovery"></a>Récupérer
* Virtual Machine Manager ne peut pas effectuer l’opération hôte hello :
  * [Basculer le point de récupération toohello sélectionné pour la machine virtuelle : erreur accès général refusé.](http://social.technet.microsoft.com/wiki/contents/articles/25504.fail-over-to-the-selected-recovery-point-for-virtual-machine-general-access-denied-error.aspx)
  * [Toofail ayant échoué d’Hyper-V sur toohello sélectionné de point de récupération pour la machine virtuelle : opération abandonnée.  Essayez avec un point de récupération plus récent. (0x80004004).](http://social.technet.microsoft.com/wiki/contents/articles/25503.hyper-v-failed-to-fail-over-to-the-selected-recovery-point-for-virtual-machine-operation-aborted-try-a-more-recent-recovery-point-0x80004004.aspx)
  * Une connexion avec hello serveur n’a pas pu être établie (0x00002EFD).
    * [Échec de la tooenable la réplication inverse pour l’ordinateur virtuel Hyper-V.](http://social.technet.microsoft.com/wiki/contents/articles/25505.a-connection-with-the-server-could-not-be-established-0x00002efd-hyper-v-failed-to-enable-reverse-replication-for-virtual-machine.aspx)
    * [Échec de la réplication tooenable pour l’ordinateur virtuel de machine virtuelle Hyper-V.](http://social.technet.microsoft.com/wiki/contents/articles/25506.a-connection-with-the-server-could-not-be-established-0x00002efd-hyper-v-failed-to-enable-replication-for-virtual-machine-virtual-machine.aspx)
  * [Impossible de valider le basculement de la machine virtuelle.](http://social.technet.microsoft.com/wiki/contents/articles/25508.could-not-commit-failover-for-virtual-machine.aspx)
* [plan de récupération Hello contient des ordinateurs virtuels qui ne sont pas prêtes pour le basculement planifié.](http://social.technet.microsoft.com/wiki/contents/articles/25509.the-recovery-plan-contains-virtual-machines-which-are-not-ready-for-planned-failover.aspx)
* [machine virtuelle de Hello n’est pas prêt pour le basculement planifié.](http://social.technet.microsoft.com/wiki/contents/articles/25507.the-virtual-machine-isn-t-ready-for-planned-failover.aspx)
* [La machine virtuelle n’est pas en cours d’exécution et n’est pas hors tension.](http://social.technet.microsoft.com/wiki/contents/articles/25510.virtual-machine-is-not-running-and-is-not-powered-off.aspx)
* [Une opération hors bande s’est produite sur une machine virtuelle et la validation du basculement a échoué.](http://social.technet.microsoft.com/wiki/contents/articles/25507.the-virtual-machine-isn-t-ready-for-planned-failover.aspx)
* Test de basculement
  * [Impossible de lancer le basculement, car le test de basculement en cours.](http://social.technet.microsoft.com/wiki/contents/articles/31111.failover-could-not-be-initiated-since-test-failover-is-in-progress.aspx)
* <span style="color:green;">NOUVELLE</span> basculement expire et 'task PreFailoverWorkflow WaitForScriptExecutionTaskTimeout' en raison des paramètres de configuration toohello sur hello groupe de sécurité réseau associé hello Machine virtuelle ou machine de hello hello sous-réseau toowhich auquel appartient. Consultez trop['task PreFailoverWorkflow WaitForScriptExecutionTaskTimeout'](https://aka.ms/troubleshoot-nsg-issue-azure-site-recovery) pour plus d’informations.

### <a name="configuration-server-process-server-master-target"></a>Serveur de configuration, serveur de processus, serveur maître
* [hôte ESXi Hello sur quel hello PS/CS est hébergé comme une machine virtuelle échoue avec un écran violet de mort.](http://social.technet.microsoft.com/wiki/contents/articles/31107.vmware-esxi-host-experiences-a-purple-screen-of-death.aspx)

### <a name="remote-desktop-troubleshooting-after-failover"></a>Résolution des problèmes après un basculement de bureau à distance
* De nombreux clients ont dû faire face toohello tooconnect de problèmes a échoué sur une machine virtuelle dans Azure. [Hello utilisez dépannage tooRDP de document dans la machine virtuelle de hello](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

#### <a name="adding-a-public-ip-on-a-resource-manager-virtual-machine"></a>Ajout d’une adresse IP publique sur une machine virtuelle du Gestionnaire des ressources
Si hello **Connect** dans le portail de hello est grisé et que vous n’êtes pas connecté tooAzure via une connexion VPN Express Route ou de Site à Site, vous devez toocreate et que vous attribuez à votre machine virtuelle une adresse IP publique avant de pouvoir utiliser à distance Interface de bureau/partagé. Vous pouvez ensuite ajouter une adresse IP publique sur l’interface de réseau hello de machine virtuelle de hello.  

![Échec de l’ajout d’une adresse IP publique sur l’interface de réseau hello de sur l’ordinateur virtuel](media/site-recovery-monitoring-and-troubleshooting/createpublicip.gif)
