---
title: "aaaTroubleshoot protection échecs VMware/physiques tooAzure | Documents Microsoft"
description: "Cet article décrit les échecs de réplication d’ordinateur VMware hello courants et comment tootroubleshoot les"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/26/2017
ms.author: asgang
ms.openlocfilehash: b821e9aa2610482ba1900645fb75e75744dc442f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a>Résoudre les problèmes locaux de réplication VMware/du serveur physique
Vous pouvez recevoir un message d’erreur spécifique lorsque vous protégez vos machines virtuelles VMware ou les serveurs physiques à l’aide d’Azure Site Recovery. Cet article explique certaines des hello rencontrés avec tooresolve d’étapes de résolution des problèmes des messages d’erreur courants les.


## <a name="initial-replication-is-stuck-at-0"></a>La réplication initiale est bloquée à 0 %
La plupart des échecs de réplication initiale hello que nous rencontrer sur le support technique sont en raison de problèmes tooconnectivity entre le serveur de processus-serveur source ou processus de serveur à Azure.
La plupart des cas, vous pouvez self résoudre ces problèmes en suivant les étapes de hello répertoriées ci-dessous.

###<a name="check-hello-following-on-source-machine"></a>Vérifiez suivantes hello sur l’ordinateur SOURCE
* À partir de la ligne de commande d’ordinateur serveur Source, utilisez Telnet tooping hello serveur de processus avec le port https (par défaut 9443) comme indiqué ci-dessous toosee si des problèmes de connectivité réseau ou des problèmes de blocage de port de pare-feu.
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > Utilisation de Telnet, ne pas utiliser une connexion de tootest PING.  Si Telnet n’est pas installé, suivez la liste des étapes hello [ici](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)

Impossible de tooconnect, autoriser le port entrant 9443 sur hello serveur de processus et vérifiez si hello problème toujours s’exécute. Dans certains cas, le serveur de traitement se trouvait derrière une zone DMZ, ce qui était à l’origine de ce problème.

* Vérifier l’état de hello du service `InMage Scout VX Agent – Sentinel/OutpostStart` si elle n’est pas en cours d’exécution et vérifiez si le problème de hello existe toujours.   
 
###<a name="check-hello-following-on-process-server"></a>Vérifiez suivantes hello sur le serveur de processus

* **Vérifiez si le serveur de processus repousse activement tooAzure de données** 

À partir de l’ordinateur du serveur de processus, ouvrez hello Gestionnaire des tâches (appuyez sur Ctrl-Maj-Échap). Onglet de performances toohello, cliquez sur le lien de 'Ouvrir Moniteur de ressource'. Dans le Gestionnaire de ressources, accédez à tooNetwork onglet. Vérifiez si cbengine.exe dans « Processes with Network Activity » (Processus avec activité réseau) envoie activement de gros volume de données (en Mo).

![Activer la réplication](./media/site-recovery-protection-common-errors/cbengine.png)

Si ce n’est pas hello les étapes répertoriées ci-dessous :

* **Vérifiez si le serveur de processus est en mesure de tooconnect objets Blob Azure**: sélectionnez et vérifiez cbengine.exe tooview hello 'Connexions TCP' toosee s’il existe une connectivité à partir de l’URL de processus serveur tooAzure stockage blob.

![Activer la réplication](./media/site-recovery-protection-common-errors/rmonitor.png)

Dans le cas contraire, allez tooControl Panneau de configuration > Services, vérifiez si hello suivant services est en cours d’exécution :

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
(Re) Démarrer un service qui n’est pas en cours d’exécution et vérifiez si le problème de hello existe toujours.

* **Vérifiez si le serveur de processus est adresse IP publique de tooconnect en mesure de tooAzure via le port 443**

Ouvrez hello CBEngineCurr.errlog plus récentes à partir de `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` et recherchez : 443 et connexion tentative a échoué.

![Activer la réplication](./media/site-recovery-protection-common-errors/logdetails1.png)

Si des problèmes, puis à partir de la ligne de commande du serveur de processus, utilisez telnet tooping votre adresse IP publique Azure (masquée dans ci-dessus image) trouvé dans hello CBEngineCurr.currLog via le port 443.

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
Si vous êtes tooconnect impossible, puis vérifiez si le problème d’accès hello est toofirewall ou Proxy, comme décrit dans l’étape suivante.


* **Vérifiez si le pare-feu basé sur l’adresse IP sur le serveur de processus ne bloque l’accès**: Si vous utilisez une de règles de pare-feu basé sur l’adresse IP sur le serveur de hello, puis télécharger la liste complète des plages d’IP centre de données Microsoft Azure à partir de hello [ici ](https://www.microsoft.com/download/details.aspx?id=41653) et ajoutez-les tooensure de configuration de pare-feu tooyour qu’elles autorisent tooAzure de communication (et hello port HTTPS (443)).  Autoriser les plages d’adresses IP pour hello région Azure de votre abonnement et ouest des États-Unis (utilisé pour la gestion d’identité et contrôle d’accès).

* **Vérifiez si basée sur URL le pare-feu sur le serveur de processus ne bloque pas les accès**: Si vous utilisez des règles de pare-feu une URL basée sur le serveur de hello, assurez-vous de hello URL suivantes est ajoutée toofirewall configuration. 
     
  `*.accesscontrol.windows.net:` : élément utilisé pour la gestion des identités et le contrôle d’accès.

  `*.backup.windowsazure.com:` : élément utilisé pour l’orchestration et le transfert des données de réplication.

  `*.blob.core.windows.net:`Utilisé pour l’accès toohello compte de stockage qui stocke des données répliquées

  `*.hypervrecoverymanager.windowsazure.com:` : élément utilisé pour l’orchestration et l’administration des opérations de gestion de la réplication.

  `time.nist.gov`et `time.windows.com`: utilisé toocheck synchronisation date / heure entre le système et l’heure globale.

URL du **cloud Azure Government** :

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* **Vérifiez si les paramètres de proxy sur le serveur de traitement ne bloque pas l’accès**.  Si vous utilisez un serveur Proxy, vérifiez que la résolution de nom du serveur proxy hello par le serveur DNS hello.
toocheck vous avez fourni au moment de hello du programme d’installation du serveur de Configuration. Accédez tooregistry clé

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

Maintenant, assurez-vous que hello mêmes paramètres sont utilisés par les données de toosend de l’agent Azure Site Recovery.
Rechercher dans la sauvegarde Microsoft Azure 

![Activer la réplication](./media/site-recovery-protection-common-errors/mab.png)

Ouvrez-la et cliquez sur Action > Modifier les propriétés. Sous l’onglet Configuration de Proxy, vous devez voir l’adresse proxy hello, qui doit être identique, comme indiqué par les paramètres de Registre hello. Dans le cas contraire, veuillez modifier toohello même adresse.

![Activer la réplication](./media/site-recovery-protection-common-errors/mabproxy.png)

* **Vérifiez si la bande passante de la limitation de bande passante n’est pas limitée sur le serveur de processus**: augmenter la bande passante hello et vérifiez si le problème de hello existe toujours.

##<a name="next-steps"></a>Étapes suivantes
Si vous avez besoin d’aide, puis de valider votre requête trop[Forum sur la récupération automatique du système](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr). Nous avons une communauté active et un de nos ingénieurs sera tooassist en mesure de vous.
