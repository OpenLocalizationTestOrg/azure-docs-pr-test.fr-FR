---
title: "aaaAzure résolution des problèmes de récupération de Site pour les erreurs et les problèmes de réplication Azure sur Azure | Documents Microsoft"
description: "Dépannage des erreurs et des problèmes lors de la réplication de machines virtuelles Azure pour la récupération d’urgence"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/10/2017
ms.author: sujayt
ms.openlocfilehash: bca957dd0f40e6b16e68913caf522f3431c55bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-to-azure-vm-replication-issues"></a>Résoudre les problèmes de réplication de machine virtuelle Azure vers Azure

Cet article décrit les problèmes courants hello dans Azure Site Recovery lors de la réplication et la récupération des machines virtuelles à partir de la région de tooanother une région et explique comment tootroubleshoot les. Pour plus d’informations sur les configurations prises en charge, consultez hello [matrice de prise en charge pour la réplication des machines virtuelles Azure](site-recovery-support-matrix-azure-to-azure.md).

## <a name="azure-resource-quota-issues-error-code-150097"></a>Problèmes liés aux quotas de ressources Azure (code d’erreur 150097)
Votre abonnement doit être activé toocreate machines virtuelles de Azure dans la région cible hello que vous envisagez de toouse votre région de récupération d’urgence. En outre, votre abonnement doit avoir suffisamment avec quota toocreate machines virtuelles de taille spécifique. Par défaut, les sélections de récupération de Site hello même taille pour la cible de hello machine virtuelle comme hello d’ordinateur virtuel source. Si la taille de correspondance hello n’est pas disponible, taille de la plus proche possible hello est choisie automatiquement. S’il n’existe pas de taille correspondante qui prend en charge la configuration de la machine virtuelle source, ce message d’erreur s’affiche :

**Code d’erreur** | **Causes possibles** | **Recommandation**
--- | --- | ---
150097<br></br>**Message**: la réplication n’a pas pu être activée pour la machine virtuelle de hello VmName. | -Votre abonnement QU'ID ne peut pas être activé toocreate de machines virtuelles dans un emplacement de la région cible hello.</br></br>-Votre ID d’abonnement ne peut pas être activé ou n’a pas suffisamment quota toocreate VM des tailles spécifiques dans l’emplacement de la région cible hello.</br></br>-Une taille de machine virtuelle cible appropriée qui correspond à la source de hello nombre de VM NIC (2) est introuvables pour l’ID d’abonnement hello dans l’emplacement de la région cible hello.| Contact [support de facturation Azure](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) tooenable création d’ordinateurs virtuels pour hello requis des tailles de machine virtuelle dans l’emplacement cible de hello pour votre abonnement. Une fois qu’il est activé, nouvelle tentative hello Échec de l’opération.

### <a name="fix-hello-problem"></a>Résoudre les problème de hello
Vous pouvez contacter [support de facturation Azure](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) tooenable votre toocreate abonnement machines virtuelles de tailles requis dans l’emplacement cible de hello.

Si l’emplacement cible de hello possède une contrainte de capacité, désactivez la réplication et activer tooa autre emplacement où votre abonnement a toocreate quota suffisant machines virtuelles de tailles de hello requis.

## <a name="trusted-root-certificates-error-code-151066"></a>Certificats racines approuvés (code d’erreur 151066)

Si tous les certificats racines de confiance de la dernière hello ne sont pas présents sur hello machine virtuelle, votre travail « activer la réplication » risque d’échouer. Sans les certificats hello, authentification de hello et l’autorisation du service de récupération de Site, les appels à partir de la machine virtuelle de hello échouent. message d’erreur Hello hello échoué « activer la réplication » Site travail de récupération s’affiche :

**Code d’erreur** | **Cause possible** | **Recommandations**
--- | --- | ---
151066<br></br>**Message** : Échec de la configuration de Site Recovery. | Hello requise des certificats racines de confiance utilisées pour l’autorisation et l’authentification ne sont pas présents sur l’ordinateur de hello. | -Pour une machine virtuelle exécutant le système d’exploitation de Windows hello, vérifiez que hello approuvées de certificats racine sont présents sur l’ordinateur de hello. Pour plus d’informations, consultez [Configurer des racines de confiance et des certificats non autorisés](https://technet.microsoft.com/library/dn265983.aspx).<br></br>-Pour une machine virtuelle exécutant le système d’exploitation de Linux hello, suivez les instructions de hello pour les certificats racines de confiance publiées par le distributeur de version de système d’exploitation de Linux hello.

### <a name="fix-hello-problem"></a>Résoudre les problème de hello
**Windows**

Installez tous les hello dernières mises à jour Windows sur hello VM afin que tous les certificats racine de hello approuvé sont présents sur l’ordinateur de hello. Si vous êtes dans un environnement déconnecté, suivez le processus de mise à jour de Windows standard hello dans vos certificats de hello tooget organisation. Hello besoin de certificats ne sont pas présents sur hello VM, hello appels toohello service de récupération de Site échoue pour des raisons de sécurité.

Suivez hello gestion de mise à jour Windows standard ou des processus de gestion de mise à jour de certificat dans votre tooget organisation tous les certificats racines de la dernière hello et la révocation de certificats hello mis à jour de liste de hello machines virtuelles.

tooverify qui hello le problème est résolu, passez toologin.microsoftonline.com à partir d’un navigateur dans votre machine virtuelle.

**Linux**

Suivez les instructions de hello fournie par votre liste de révocation de certificats plus récente hello sur hello machine virtuelle Linux distributeur tooget hello plus récente des certificats racine approuvés.

SuSE Linux utilisant des liens symboliques toomaintain une liste de certificats, procédez comme suit :

1.  Connectez-vous en tant qu’utilisateur racine.

2.  Exécutez cette commande :

      ``# cd /etc/ssl/certs``

3.  toosee si le certificat d’autorité de certification hello Symantec racine est présent ou non, exécutez cette commande :

      ``# ls VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem``

4.  Si le fichier de hello n’est pas disponible, exécutez ces commandes :

      ``# wget https://www.symantec.com/content/dam/symantec/docs/other-resources/verisign-class-3-public-primary-certification-authority-g5-en.pem -O VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem``

      ``# c_rehash``

5.  toocreate un lien symbolique avec b204d74a.0 -> VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem, exécutez la commande suivante :

      ``# ln -s  VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem b204d74a.0``

6.  Vérifiez toosee si cette commande a hello suivant de sortie. Si ce n’est pas le cas, vous avez un lien symbolique toocreate :

      ``# ls -l | grep Baltimore
      -rw-r--r-- 1 root root   1303 Apr  7  2016 Baltimore_CyberTrust_Root.pem
      lrwxrwxrwx 1 root root     29 May 30 04:47 3ad48a91.0 -> Baltimore_CyberTrust_Root.pem
      lrwxrwxrwx 1 root root     29 May 30 05:01 653b494a.0 -> Baltimore_CyberTrust_Root.pem``

7. Si le lien symbolique 653b494a.0 n’est pas présent, utilisez ce toocreate commande un lien symbolique :

      ``# ln -s Baltimore_CyberTrust_Root.pem 653b494a.0``


## <a name="outbound-connectivity-for-site-recovery-urls-or-ip-ranges-error-code-151037-or-151072"></a>Connectivité sortante pour les plages d’adresses IP ou les URL Site Recovery (code d’erreur 151037 ou 151072)

Pour toowork de réplication de Site Recovery, toospecific connectivité sortante URL ou plages IP est requise à partir de la machine virtuelle de hello. Si votre machine virtuelle se trouve derrière un pare-feu ou utilisations réseau connectivité sortante de sécurité (groupe) règles toocontrol, vous pouvez voir un de ces messages d’erreur :

**Codes d’erreur** | **Causes possibles** | **Recommandations**
--- | --- | ---
151037<br></br>**Message**: Échec de tooregister machine virtuelle Azure Site Recovery. | -Vous utilisez un accès sortant NSG toocontrol sur la machine virtuelle de hello et hello requis IP plages ne sont pas dans la liste approuvée pour l’accès sortant.</br></br>-Vous utilisez des outils de pare-feu tiers et hello requis de plages IP URL ne sont pas autorisés.</br>| -Si vous utilisez des pare-feu proxy toocontrol réseau sortant connectivité sur hello machine virtuelle, vérifiez que hello URL requis ou plages d’adresses IP de centre de données sont autorisés. Pour plus d’informations, consultez ces [instructions relatives aux proxy de pare-feu](https://aka.ms/a2a-firewall-proxy-guidance).</br></br>-Si vous utilisez la connectivité de réseau sortant NSG règles toocontrol sur hello machine virtuelle, assurez-vous que les plages d’adresses IP de centre de données requis de hello sont autorisés. Pour plus d’informations, consultez ces [instructions relatives aux groupes de sécurité réseau](https://aka.ms/a2a-nsg-guidance).
151072<br></br>**Message** : Échec de la configuration de Site Recovery. | Connexion ne peut pas être des points de terminaison de service tooSite établie récupération. | -Si vous utilisez des pare-feu proxy toocontrol réseau sortant connectivité sur hello machine virtuelle, vérifiez que hello URL requis ou plages d’adresses IP de centre de données sont autorisés. Pour plus d’informations, consultez ces [instructions relatives aux proxy de pare-feu](https://aka.ms/a2a-firewall-proxy-guidance).</br></br>-Si vous utilisez la connectivité de réseau sortant NSG règles toocontrol sur hello machine virtuelle, assurez-vous que les plages d’adresses IP de centre de données requis de hello sont autorisés. Pour plus d’informations, consultez ces [instructions relatives aux groupes de sécurité réseau](https://aka.ms/a2a-nsg-guidance).

### <a name="fix-hello-problem"></a>Résoudre les problème de hello
toowhitelist [hello requis URL](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-urls) ou hello [requis de plages d’adresses IP](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-ip-ranges), suivez les étapes de hello Bonjour [document du Guide de mise en réseau](site-recovery-azure-to-azure-networking-guidance.md).

## <a name="disk-not-found-in-hello-machine-error-code-150039"></a>Disque introuvable dans l’ordinateur hello (code d’erreur 150039)

Un nouveau disque attaché toohello que machine virtuelle doit être initialisé.

**Code d’erreur** | **Causes possibles** | **Recommandations**
--- | --- | ---
150039<br></br>**Message**: le disque de données Azure (DiskName) (DiskURI) avec le numéro d’unité logique (LUN) (LUNValue) n’était pas mappé tooa disque signalé au cours à partir de hello machine virtuelle qui a hello même valeur de numéro d’unité logique. | -Un nouveau disque de données a été attachée toohello machine virtuelle, mais elle n’a pas été initialisée.</br></br>-le disque de données hello à l’intérieur de hello VM ne signale pas correctement de valeur de numéro d’unité logique hello à quels hello disque a été attaché toohello machine virtuelle.| Assurez-vous que les disques de données hello sont initialisés et puis recommencez hello.</br></br>Pour Windows : [Attacher et initialiser un nouveau disque](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk).</br></br>Pour Linux : [Initialiser un nouveau disque de données sous Linux](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux).

### <a name="fix-hello-problem"></a>Résoudre les problème de hello
Vérifiez que les disques de données hello aient été initialisés et recommencez hello opération :

- Pour Windows : [Attacher et initialiser un nouveau disque](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk).
- Pour Linux : [Initialiser un nouveau disque de données sous Linux](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux).

Si hello problème persiste, contactez le support technique.


## <a name="unable-toosee-hello-azure-vm-for-selection-in-enable-replication"></a>Impossible de toosee hello machine virtuelle Azure pour la sélection dans « activer la réplication »

Votre machine virtuelle peut ne pas figurer dans la liste dans [Activer la réplication : Étape 2](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines). Ce problème peut être dû à configuration de la récupération de Site toostale restant sur hello machine virtuelle Azure. configuration d’obsolètes Hello pourrait rester sur une machine virtuelle de Azure Bonjour suivant cas :

- Vous activé la réplication pour hello machine virtuelle Azure à l’aide de récupération de Site et supprimé le coffre Site Recovery hello sans explicitement la désactivation de la réplication sur hello machine virtuelle.
- Vous activé la réplication pour hello machine virtuelle Azure à l’aide de récupération de Site et ensuite supprimé le groupe de ressources hello contenant le coffre Site Recovery hello sans explicitement la désactivation de la réplication sur hello machine virtuelle.

### <a name="fix-hello-problem"></a>Résoudre les problème de hello

Vous pouvez utiliser [supprimer un script de configuration automatique du obsolète](https://gallery.technet.microsoft.com/Azure-Recovery-ASR-script-3a93f412) et supprimer hello obsolète configuration de Site Recovery sur hello machine virtuelle Azure. Vous devez voir hello machine virtuelle dans [activer la réplication : étape 2](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines) après suppression de la configuration d’obsolètes hello.


## <a name="next-steps"></a>Étapes suivantes
[Répliquer des machines virtuelles Azure](site-recovery-replicate-azure-to-azure.md)
