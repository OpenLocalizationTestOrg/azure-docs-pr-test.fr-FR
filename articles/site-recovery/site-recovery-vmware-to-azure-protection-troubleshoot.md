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
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a><span data-ttu-id="3f81e-103">Résoudre les problèmes locaux de réplication VMware/du serveur physique</span><span class="sxs-lookup"><span data-stu-id="3f81e-103">Troubleshoot on-premises VMware/Physical server replication issues</span></span>
<span data-ttu-id="3f81e-104">Vous pouvez recevoir un message d’erreur spécifique lorsque vous protégez vos machines virtuelles VMware ou les serveurs physiques à l’aide d’Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="3f81e-104">You may receive a specific error message when protecting your VMware virtual machines or physical servers using Azure Site Recovery.</span></span> <span data-ttu-id="3f81e-105">Cet article explique certaines des hello rencontrés avec tooresolve d’étapes de résolution des problèmes des messages d’erreur courants les.</span><span class="sxs-lookup"><span data-stu-id="3f81e-105">This article details some of hello more common error messages encountered, along with troubleshooting steps tooresolve them.</span></span>


## <a name="initial-replication-is-stuck-at-0"></a><span data-ttu-id="3f81e-106">La réplication initiale est bloquée à 0 %</span><span class="sxs-lookup"><span data-stu-id="3f81e-106">Initial replication is stuck at 0%</span></span>
<span data-ttu-id="3f81e-107">La plupart des échecs de réplication initiale hello que nous rencontrer sur le support technique sont en raison de problèmes tooconnectivity entre le serveur de processus-serveur source ou processus de serveur à Azure.</span><span class="sxs-lookup"><span data-stu-id="3f81e-107">Most of hello initial replication failures that we encounter at support are due tooconnectivity issues between source server-to-process server or process server-to-Azure.</span></span>
<span data-ttu-id="3f81e-108">La plupart des cas, vous pouvez self résoudre ces problèmes en suivant les étapes de hello répertoriées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3f81e-108">For most cases, you can self troubleshoot these issues by following hello steps listed below.</span></span>

###<a name="check-hello-following-on-source-machine"></a><span data-ttu-id="3f81e-109">Vérifiez suivantes hello sur l’ordinateur SOURCE</span><span class="sxs-lookup"><span data-stu-id="3f81e-109">Check hello following on SOURCE MACHINE</span></span>
* <span data-ttu-id="3f81e-110">À partir de la ligne de commande d’ordinateur serveur Source, utilisez Telnet tooping hello serveur de processus avec le port https (par défaut 9443) comme indiqué ci-dessous toosee si des problèmes de connectivité réseau ou des problèmes de blocage de port de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="3f81e-110">From Source Server machine command line, use Telnet tooping hello Process Server with https port (default 9443) as shown below toosee if there are any network connectivity issues or firewall port blocking issues.</span></span>
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > <span data-ttu-id="3f81e-111">Utilisation de Telnet, ne pas utiliser une connexion de tootest PING.</span><span class="sxs-lookup"><span data-stu-id="3f81e-111">Use Telnet, don’t use PING tootest connectivity.</span></span>  <span data-ttu-id="3f81e-112">Si Telnet n’est pas installé, suivez la liste des étapes hello [ici](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="3f81e-112">If Telnet is not installed, follow hello steps list [here](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span></span>

<span data-ttu-id="3f81e-113">Impossible de tooconnect, autoriser le port entrant 9443 sur hello serveur de processus et vérifiez si hello problème toujours s’exécute.</span><span class="sxs-lookup"><span data-stu-id="3f81e-113">If unable tooconnect, allow inbound port 9443 on hello Process Server and check if hello problem still exits.</span></span> <span data-ttu-id="3f81e-114">Dans certains cas, le serveur de traitement se trouvait derrière une zone DMZ, ce qui était à l’origine de ce problème.</span><span class="sxs-lookup"><span data-stu-id="3f81e-114">There has been some cases where process server was behind DMZ, which was causing this problem.</span></span>

* <span data-ttu-id="3f81e-115">Vérifier l’état de hello du service `InMage Scout VX Agent – Sentinel/OutpostStart` si elle n’est pas en cours d’exécution et vérifiez si le problème de hello existe toujours.</span><span class="sxs-lookup"><span data-stu-id="3f81e-115">Check hello status of service `InMage Scout VX Agent – Sentinel/OutpostStart` if it is not running and check if hello problem still exists.</span></span>   
 
###<a name="check-hello-following-on-process-server"></a><span data-ttu-id="3f81e-116">Vérifiez suivantes hello sur le serveur de processus</span><span class="sxs-lookup"><span data-stu-id="3f81e-116">Check hello following on PROCESS SERVER</span></span>

* <span data-ttu-id="3f81e-117">**Vérifiez si le serveur de processus repousse activement tooAzure de données**</span><span class="sxs-lookup"><span data-stu-id="3f81e-117">**Check if process server is actively pushing data tooAzure**</span></span> 

<span data-ttu-id="3f81e-118">À partir de l’ordinateur du serveur de processus, ouvrez hello Gestionnaire des tâches (appuyez sur Ctrl-Maj-Échap).</span><span class="sxs-lookup"><span data-stu-id="3f81e-118">From Process Server machine, open hello Task Manager (press Ctrl-Shift-Esc ).</span></span> <span data-ttu-id="3f81e-119">Onglet de performances toohello, cliquez sur le lien de 'Ouvrir Moniteur de ressource'.</span><span class="sxs-lookup"><span data-stu-id="3f81e-119">Go toohello Performance tab and click ‘Open Resource Monitor’ link.</span></span> <span data-ttu-id="3f81e-120">Dans le Gestionnaire de ressources, accédez à tooNetwork onglet. Vérifiez si cbengine.exe dans « Processes with Network Activity » (Processus avec activité réseau) envoie activement de gros volume de données (en Mo).</span><span class="sxs-lookup"><span data-stu-id="3f81e-120">From Resource Manager, go tooNetwork tab. Check if cbengine.exe in ‘Processes with Network Activity’ is actively sending large volume (in Mbs) of data.</span></span>

![Activer la réplication](./media/site-recovery-protection-common-errors/cbengine.png)

<span data-ttu-id="3f81e-122">Si ce n’est pas hello les étapes répertoriées ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3f81e-122">If not follow hello steps listed below:</span></span>

* <span data-ttu-id="3f81e-123">**Vérifiez si le serveur de processus est en mesure de tooconnect objets Blob Azure**: sélectionnez et vérifiez cbengine.exe tooview hello 'Connexions TCP' toosee s’il existe une connectivité à partir de l’URL de processus serveur tooAzure stockage blob.</span><span class="sxs-lookup"><span data-stu-id="3f81e-123">**Check if Process server is able tooconnect Azure Blob**: Select and check cbengine.exe tooview hello ‘TCP Connections’ toosee if there is connectivity from Process server tooAzure Storage blob URL.</span></span>

![Activer la réplication](./media/site-recovery-protection-common-errors/rmonitor.png)

<span data-ttu-id="3f81e-125">Dans le cas contraire, allez tooControl Panneau de configuration > Services, vérifiez si hello suivant services est en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="3f81e-125">If not then go tooControl Panel > Services, check if hello following services are up and running:</span></span>

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
<span data-ttu-id="3f81e-126">(Re) Démarrer un service qui n’est pas en cours d’exécution et vérifiez si le problème de hello existe toujours.</span><span class="sxs-lookup"><span data-stu-id="3f81e-126">(Re)Start any service which is not running and check if hello problem still exists.</span></span>

* <span data-ttu-id="3f81e-127">**Vérifiez si le serveur de processus est adresse IP publique de tooconnect en mesure de tooAzure via le port 443**</span><span class="sxs-lookup"><span data-stu-id="3f81e-127">**Check if Process server is able tooconnect tooAzure Public IP address using port 443**</span></span>

<span data-ttu-id="3f81e-128">Ouvrez hello CBEngineCurr.errlog plus récentes à partir de `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` et recherchez : 443 et connexion tentative a échoué.</span><span class="sxs-lookup"><span data-stu-id="3f81e-128">Open hello latest CBEngineCurr.errlog from `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` and search for :443  and connection attempt failed.</span></span>

![Activer la réplication](./media/site-recovery-protection-common-errors/logdetails1.png)

<span data-ttu-id="3f81e-130">Si des problèmes, puis à partir de la ligne de commande du serveur de processus, utilisez telnet tooping votre adresse IP publique Azure (masquée dans ci-dessus image) trouvé dans hello CBEngineCurr.currLog via le port 443.</span><span class="sxs-lookup"><span data-stu-id="3f81e-130">If there are issues, then from Process Server command line, use telnet tooping your Azure Public IP address (masked in above image) found in hello CBEngineCurr.currLog using port 443.</span></span>

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
<span data-ttu-id="3f81e-131">Si vous êtes tooconnect impossible, puis vérifiez si le problème d’accès hello est toofirewall ou Proxy, comme décrit dans l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="3f81e-131">If you are unable tooconnect, then check if hello access issue is due toofirewall or Proxy as described in next step.</span></span>


* <span data-ttu-id="3f81e-132">**Vérifiez si le pare-feu basé sur l’adresse IP sur le serveur de processus ne bloque l’accès**: Si vous utilisez une de règles de pare-feu basé sur l’adresse IP sur le serveur de hello, puis télécharger la liste complète des plages d’IP centre de données Microsoft Azure à partir de hello [ici ](https://www.microsoft.com/download/details.aspx?id=41653) et ajoutez-les tooensure de configuration de pare-feu tooyour qu’elles autorisent tooAzure de communication (et hello port HTTPS (443)).</span><span class="sxs-lookup"><span data-stu-id="3f81e-132">**Check if IP address-based firewall on Process server are not blocking access**: If you are using an IP address-based firewall rules on hello server, then download hello complete list of Microsoft Azure Datacenter IP Ranges from [here](https://www.microsoft.com/download/details.aspx?id=41653) and add them tooyour firewall configuration tooensure they allow communication tooAzure (and hello HTTPS (443) port).</span></span>  <span data-ttu-id="3f81e-133">Autoriser les plages d’adresses IP pour hello région Azure de votre abonnement et ouest des États-Unis (utilisé pour la gestion d’identité et contrôle d’accès).</span><span class="sxs-lookup"><span data-stu-id="3f81e-133">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

* <span data-ttu-id="3f81e-134">**Vérifiez si basée sur URL le pare-feu sur le serveur de processus ne bloque pas les accès**: Si vous utilisez des règles de pare-feu une URL basée sur le serveur de hello, assurez-vous de hello URL suivantes est ajoutée toofirewall configuration.</span><span class="sxs-lookup"><span data-stu-id="3f81e-134">**Check if URL-based firewall on Process server is not blocking access**:  If you are using a URL based firewall rules on hello server, ensure hello following URLs are added toofirewall configuration.</span></span> 
     
  <span data-ttu-id="3f81e-135">`*.accesscontrol.windows.net:` : élément utilisé pour la gestion des identités et le contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="3f81e-135">`*.accesscontrol.windows.net:` Used for access control and identity management</span></span>

  <span data-ttu-id="3f81e-136">`*.backup.windowsazure.com:` : élément utilisé pour l’orchestration et le transfert des données de réplication.</span><span class="sxs-lookup"><span data-stu-id="3f81e-136">`*.backup.windowsazure.com:` Used for replication data transfer and orchestration</span></span>

  <span data-ttu-id="3f81e-137">`*.blob.core.windows.net:`Utilisé pour l’accès toohello compte de stockage qui stocke des données répliquées</span><span class="sxs-lookup"><span data-stu-id="3f81e-137">`*.blob.core.windows.net:` Used for access toohello storage account that stores replicated data</span></span>

  <span data-ttu-id="3f81e-138">`*.hypervrecoverymanager.windowsazure.com:` : élément utilisé pour l’orchestration et l’administration des opérations de gestion de la réplication.</span><span class="sxs-lookup"><span data-stu-id="3f81e-138">`*.hypervrecoverymanager.windowsazure.com:` Used for replication management operations and orchestration</span></span>

  <span data-ttu-id="3f81e-139">`time.nist.gov`et `time.windows.com`: utilisé toocheck synchronisation date / heure entre le système et l’heure globale.</span><span class="sxs-lookup"><span data-stu-id="3f81e-139">`time.nist.gov` and `time.windows.com`: Used toocheck time synchronization between system and global time.</span></span>

<span data-ttu-id="3f81e-140">URL du **cloud Azure Government** :</span><span class="sxs-lookup"><span data-stu-id="3f81e-140">URLs for **Azure Government Cloud**:</span></span>

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* <span data-ttu-id="3f81e-141">**Vérifiez si les paramètres de proxy sur le serveur de traitement ne bloque pas l’accès**.</span><span class="sxs-lookup"><span data-stu-id="3f81e-141">**Check if Proxy Settings on Process server are not blocking access**.</span></span>  <span data-ttu-id="3f81e-142">Si vous utilisez un serveur Proxy, vérifiez que la résolution de nom du serveur proxy hello par le serveur DNS hello.</span><span class="sxs-lookup"><span data-stu-id="3f81e-142">If you are using a Proxy Server, ensure hello proxy server name is resolving by hello DNS server.</span></span>
<span data-ttu-id="3f81e-143">toocheck vous avez fourni au moment de hello du programme d’installation du serveur de Configuration.</span><span class="sxs-lookup"><span data-stu-id="3f81e-143">toocheck what you have provided at hello time of Configuration Server setup.</span></span> <span data-ttu-id="3f81e-144">Accédez tooregistry clé</span><span class="sxs-lookup"><span data-stu-id="3f81e-144">Go tooregistry key</span></span>

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

<span data-ttu-id="3f81e-145">Maintenant, assurez-vous que hello mêmes paramètres sont utilisés par les données de toosend de l’agent Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="3f81e-145">Now ensure that hello same settings are being used by Azure Site Recovery agent toosend data.</span></span>
<span data-ttu-id="3f81e-146">Rechercher dans la sauvegarde Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="3f81e-146">Search Microsoft Azure  Backup</span></span> 

![Activer la réplication](./media/site-recovery-protection-common-errors/mab.png)

<span data-ttu-id="3f81e-148">Ouvrez-la et cliquez sur Action > Modifier les propriétés.</span><span class="sxs-lookup"><span data-stu-id="3f81e-148">Open it and click on Action > Change Properties.</span></span> <span data-ttu-id="3f81e-149">Sous l’onglet Configuration de Proxy, vous devez voir l’adresse proxy hello, qui doit être identique, comme indiqué par les paramètres de Registre hello.</span><span class="sxs-lookup"><span data-stu-id="3f81e-149">Under Proxy Configuration tab, you should see hello proxy address, which should be same as shown by hello registry settings.</span></span> <span data-ttu-id="3f81e-150">Dans le cas contraire, veuillez modifier toohello même adresse.</span><span class="sxs-lookup"><span data-stu-id="3f81e-150">If not, please change it toohello same address.</span></span>

![Activer la réplication](./media/site-recovery-protection-common-errors/mabproxy.png)

* <span data-ttu-id="3f81e-152">**Vérifiez si la bande passante de la limitation de bande passante n’est pas limitée sur le serveur de processus**: augmenter la bande passante hello et vérifiez si le problème de hello existe toujours.</span><span class="sxs-lookup"><span data-stu-id="3f81e-152">**Check if Throttle bandwidth is not constrained on Process server**:  Increase hello bandwidth  and check if hello problem still exists.</span></span>

##<a name="next-steps"></a><span data-ttu-id="3f81e-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3f81e-153">Next steps</span></span>
<span data-ttu-id="3f81e-154">Si vous avez besoin d’aide, puis de valider votre requête trop[Forum sur la récupération automatique du système](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="3f81e-154">If you need more help, then post your query too[ASR forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span></span> <span data-ttu-id="3f81e-155">Nous avons une communauté active et un de nos ingénieurs sera tooassist en mesure de vous.</span><span class="sxs-lookup"><span data-stu-id="3f81e-155">We have an active community and one of our engineers will be able tooassist you.</span></span>
