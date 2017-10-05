---
title: "Corriger les défauts de protection VMware/physiques dans Azure | Microsoft Docs"
description: "Cet article décrit les échecs de réplication d’ordinateur VMware courants et comment les résoudre"
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
ms.openlocfilehash: 6ebec2e06566b1e2d6834fdd81c0d8b2801b80b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a><span data-ttu-id="07c12-103">Résoudre les problèmes locaux de réplication VMware/du serveur physique</span><span class="sxs-lookup"><span data-stu-id="07c12-103">Troubleshoot on-premises VMware/Physical server replication issues</span></span>
<span data-ttu-id="07c12-104">Vous pouvez recevoir un message d’erreur spécifique lorsque vous protégez vos machines virtuelles VMware ou les serveurs physiques à l’aide d’Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="07c12-104">You may receive a specific error message when protecting your VMware virtual machines or physical servers using Azure Site Recovery.</span></span> <span data-ttu-id="07c12-105">Cet article décrit en détail certains des messages d’erreur les plus couramment rencontrés, ainsi que les étapes de dépannage à suivre pour les résoudre.</span><span class="sxs-lookup"><span data-stu-id="07c12-105">This article details some of the more common error messages encountered, along with troubleshooting steps to resolve them.</span></span>


## <a name="initial-replication-is-stuck-at-0"></a><span data-ttu-id="07c12-106">La réplication initiale est bloquée à 0 %</span><span class="sxs-lookup"><span data-stu-id="07c12-106">Initial replication is stuck at 0%</span></span>
<span data-ttu-id="07c12-107">La plupart des échecs de réplication initiale que nous rencontrons au niveau du support sont dus à des problèmes de connectivité entre le serveur source et le serveur de traitement ou le serveur de traitement et Azure.</span><span class="sxs-lookup"><span data-stu-id="07c12-107">Most of the initial replication failures that we encounter at support are due to connectivity issues between source server-to-process server or process server-to-Azure.</span></span>
<span data-ttu-id="07c12-108">Dans la plupart des cas, vous pouvez résoudre vous-même ces problèmes en suivant les étapes indiquées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="07c12-108">For most cases, you can self troubleshoot these issues by following the steps listed below.</span></span>

###<a name="check-the-following-on-source-machine"></a><span data-ttu-id="07c12-109">Vérifiez les points suivants sur la MACHINE SOURCE</span><span class="sxs-lookup"><span data-stu-id="07c12-109">Check the following on SOURCE MACHINE</span></span>
* <span data-ttu-id="07c12-110">À partir de la ligne de commande du serveur source, utilisez Telnet pour effectuer un test Ping sur le serveur de traitement avec le port https (par défaut 9443) comme indiqué ci-dessous. Cela vous indiquera s’il existe des problèmes de connectivité réseau ou des problèmes de blocage de port par le pare-feu.</span><span class="sxs-lookup"><span data-stu-id="07c12-110">From Source Server machine command line, use Telnet to ping the Process Server with https port (default 9443) as shown below to see if there are any network connectivity issues or firewall port blocking issues.</span></span>
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > <span data-ttu-id="07c12-111">Utilisez Telnet et non PING pour tester la connectivité.</span><span class="sxs-lookup"><span data-stu-id="07c12-111">Use Telnet, don’t use PING to test connectivity.</span></span>  <span data-ttu-id="07c12-112">Si Telnet n’est pas installé, suivez les étapes présentées [ici](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="07c12-112">If Telnet is not installed, follow the steps list [here](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span></span>

<span data-ttu-id="07c12-113">Si vous ne parvenez pas à vous connecter, autorisez le port entrant 9443 sur le serveur de traitement et vérifiez si le problème persiste.</span><span class="sxs-lookup"><span data-stu-id="07c12-113">If unable to connect, allow inbound port 9443 on the Process Server and check if the problem still exits.</span></span> <span data-ttu-id="07c12-114">Dans certains cas, le serveur de traitement se trouvait derrière une zone DMZ, ce qui était à l’origine de ce problème.</span><span class="sxs-lookup"><span data-stu-id="07c12-114">There has been some cases where process server was behind DMZ, which was causing this problem.</span></span>

* <span data-ttu-id="07c12-115">Vérifiez l’état du service `InMage Scout VX Agent – Sentinel/OutpostStart` s’il n’est pas en cours d’exécution et vérifiez si le problème persiste.</span><span class="sxs-lookup"><span data-stu-id="07c12-115">Check the status of service `InMage Scout VX Agent – Sentinel/OutpostStart` if it is not running and check if the problem still exists.</span></span>   
 
###<a name="check-the-following-on-process-server"></a><span data-ttu-id="07c12-116">Vérifiez les éléments suivants sur le SERVEUR DE TRAITEMENT</span><span class="sxs-lookup"><span data-stu-id="07c12-116">Check the following on PROCESS SERVER</span></span>

* <span data-ttu-id="07c12-117">**Vérifiez si le serveur de traitement transmet activement des données à Azure**</span><span class="sxs-lookup"><span data-stu-id="07c12-117">**Check if process server is actively pushing data to Azure**</span></span> 

<span data-ttu-id="07c12-118">Sur le serveur de traitement, ouvrez le Gestionnaire des tâches (Ctrl-Maj-Échap).</span><span class="sxs-lookup"><span data-stu-id="07c12-118">From Process Server machine, open the Task Manager (press Ctrl-Shift-Esc ).</span></span> <span data-ttu-id="07c12-119">Accédez à l’onglet Performances, puis cliquez sur le lien « Open Resource Monitor » (Ouvrir le moniteur de ressource).</span><span class="sxs-lookup"><span data-stu-id="07c12-119">Go to the Performance tab and click ‘Open Resource Monitor’ link.</span></span> <span data-ttu-id="07c12-120">Dans le Gestionnaire des ressources, accédez à l’onglet Réseau.</span><span class="sxs-lookup"><span data-stu-id="07c12-120">From Resource Manager, go to Network tab.</span></span> <span data-ttu-id="07c12-121">Vérifiez si cbengine.exe dans « Processes with Network Activity » (Processus avec activité réseau) envoie activement de gros volume de données (en Mo).</span><span class="sxs-lookup"><span data-stu-id="07c12-121">Check if cbengine.exe in ‘Processes with Network Activity’ is actively sending large volume (in Mbs) of data.</span></span>

![Activer la réplication](./media/site-recovery-protection-common-errors/cbengine.png)

<span data-ttu-id="07c12-123">Si ce n’est pas le cas, suivez les étapes détaillées ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="07c12-123">If not follow the steps listed below:</span></span>

* <span data-ttu-id="07c12-124">**Vérifiez si le serveur de traitement est en mesure de se connecter à Azure Blob** : sélectionnez et vérifiez cbengine.exe pour afficher les connexions TCP et voir s’il existe une connectivité du serveur de traitement à l’URL d’objet blob Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="07c12-124">**Check if Process server is able to connect Azure Blob**: Select and check cbengine.exe to view the ‘TCP Connections’ to see if there is connectivity from Process server to Azure Storage blob URL.</span></span>

![Activer la réplication](./media/site-recovery-protection-common-errors/rmonitor.png)

<span data-ttu-id="07c12-126">Si ce n’est pas le cas, accédez au Panneau de configuration > Services et vérifiez si les services suivants sont en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="07c12-126">If not then go to Control Panel > Services, check if the following services are up and running:</span></span>

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
<span data-ttu-id="07c12-127">(Re)démarrez les services qui ne sont pas en cours d’exécution et vérifiez si le problème persiste.</span><span class="sxs-lookup"><span data-stu-id="07c12-127">(Re)Start any service which is not running and check if the problem still exists.</span></span>

* <span data-ttu-id="07c12-128">**Vérifiez si le serveur de traitement est en mesure de se connecter à l’adresse IP publique Azure via le port 443**</span><span class="sxs-lookup"><span data-stu-id="07c12-128">**Check if Process server is able to connect to Azure Public IP address using port 443**</span></span>

<span data-ttu-id="07c12-129">Ouvrez le dernier fichier CBEngineCurr.errlog sous `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` et recherchez « :443 » et « connection attempt failed ».</span><span class="sxs-lookup"><span data-stu-id="07c12-129">Open the latest CBEngineCurr.errlog from `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` and search for :443  and connection attempt failed.</span></span>

![Activer la réplication](./media/site-recovery-protection-common-errors/logdetails1.png)

<span data-ttu-id="07c12-131">Si vous rencontrez des problèmes, dans la ligne de commande du serveur de traitement, utilisez telnet pour effectuer un test ping avec votre adresse IP publique Azure (masquée dans l’image ci-dessus) trouvée dans le fichier CBEngineCurr.currLog via le port 443.</span><span class="sxs-lookup"><span data-stu-id="07c12-131">If there are issues, then from Process Server command line, use telnet to ping your Azure Public IP address (masked in above image) found in the CBEngineCurr.currLog using port 443.</span></span>

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
<span data-ttu-id="07c12-132">Si vous ne parvenez pas à vous connecter, vérifiez si le problème d’accès est dû au pare-feu ou au proxy, comme décrit dans l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="07c12-132">If you are unable to connect, then check if the access issue is due to firewall or Proxy as described in next step.</span></span>


* <span data-ttu-id="07c12-133">**Vérifiez si le pare-feu basé sur l’adresse IP du serveur de traitement ne bloque pas l’accès** : si vous utilisez des règles de pare-feu basées sur l’adresse IP sur le serveur, téléchargez la liste complète des plages d’IP du centre de données Microsoft Azure [ici](https://www.microsoft.com/download/details.aspx?id=41653) et ajoutez-les à la configuration de votre pare-feu pour vous assurer que la communication avec Azure (et le port HTTPS (443)) est autorisée.</span><span class="sxs-lookup"><span data-stu-id="07c12-133">**Check if IP address-based firewall on Process server are not blocking access**: If you are using an IP address-based firewall rules on the server, then download the complete list of Microsoft Azure Datacenter IP Ranges from [here](https://www.microsoft.com/download/details.aspx?id=41653) and add them to your firewall configuration to ensure they allow communication to Azure (and the HTTPS (443) port).</span></span>  <span data-ttu-id="07c12-134">Autorisez les plages d’adresses IP relatives à la région de votre abonnement Azure et à la région des États-Unis de l’Ouest (utilisées pour la gestion du contrôle d’accès et des identités).</span><span class="sxs-lookup"><span data-stu-id="07c12-134">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

* <span data-ttu-id="07c12-135">**Vérifiez si le pare-feu basé sur l’URL du serveur de traitement ne bloque pas l’accès** : si vous utilisez des règles de pare-feu basées sur l’URL sur le serveur, vérifiez que les URL suivantes figurent dans la configuration du pare-feu.</span><span class="sxs-lookup"><span data-stu-id="07c12-135">**Check if URL-based firewall on Process server is not blocking access**:  If you are using a URL based firewall rules on the server, ensure the following URLs are added to firewall configuration.</span></span> 
     
  <span data-ttu-id="07c12-136">`*.accesscontrol.windows.net:` : élément utilisé pour la gestion des identités et le contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="07c12-136">`*.accesscontrol.windows.net:` Used for access control and identity management</span></span>

  <span data-ttu-id="07c12-137">`*.backup.windowsazure.com:` : élément utilisé pour l’orchestration et le transfert des données de réplication.</span><span class="sxs-lookup"><span data-stu-id="07c12-137">`*.backup.windowsazure.com:` Used for replication data transfer and orchestration</span></span>

  <span data-ttu-id="07c12-138">`*.blob.core.windows.net:` : élément utilisé pour l’accès au compte de stockage qui stocke les données répliquées</span><span class="sxs-lookup"><span data-stu-id="07c12-138">`*.blob.core.windows.net:` Used for access to the storage account that stores replicated data</span></span>

  <span data-ttu-id="07c12-139">`*.hypervrecoverymanager.windowsazure.com:` : élément utilisé pour l’orchestration et l’administration des opérations de gestion de la réplication.</span><span class="sxs-lookup"><span data-stu-id="07c12-139">`*.hypervrecoverymanager.windowsazure.com:` Used for replication management operations and orchestration</span></span>

  <span data-ttu-id="07c12-140">`time.nist.gov` et `time.windows.com` : éléments utilisés pour vérifier la synchronisation horaire entre l’horloge système et l’heure globale.</span><span class="sxs-lookup"><span data-stu-id="07c12-140">`time.nist.gov` and `time.windows.com`: Used to check time synchronization between system and global time.</span></span>

<span data-ttu-id="07c12-141">URL du **cloud Azure Government** :</span><span class="sxs-lookup"><span data-stu-id="07c12-141">URLs for **Azure Government Cloud**:</span></span>

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* <span data-ttu-id="07c12-142">**Vérifiez si les paramètres de proxy sur le serveur de traitement ne bloque pas l’accès**.</span><span class="sxs-lookup"><span data-stu-id="07c12-142">**Check if Proxy Settings on Process server are not blocking access**.</span></span>  <span data-ttu-id="07c12-143">Si vous utilisez un serveur proxy, vérifiez que le nom du serveur proxy résout le nom du serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="07c12-143">If you are using a Proxy Server, ensure the proxy server name is resolving by the DNS server.</span></span>
<span data-ttu-id="07c12-144">Pour vérifier les informations que vous avez fournies au moment de la configuration du serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="07c12-144">To check what you have provided at the time of Configuration Server setup.</span></span> <span data-ttu-id="07c12-145">Accédez à la clé de Registre</span><span class="sxs-lookup"><span data-stu-id="07c12-145">Go to registry key</span></span>

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

<span data-ttu-id="07c12-146">Assurez-vous maintenant que les mêmes paramètres sont utilisés par l’agent Azure Site Recovery pour envoyer des données.</span><span class="sxs-lookup"><span data-stu-id="07c12-146">Now ensure that the same settings are being used by Azure Site Recovery agent to send data.</span></span>
<span data-ttu-id="07c12-147">Rechercher dans la sauvegarde Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="07c12-147">Search Microsoft Azure  Backup</span></span> 

![Activer la réplication](./media/site-recovery-protection-common-errors/mab.png)

<span data-ttu-id="07c12-149">Ouvrez-la et cliquez sur Action > Modifier les propriétés.</span><span class="sxs-lookup"><span data-stu-id="07c12-149">Open it and click on Action > Change Properties.</span></span> <span data-ttu-id="07c12-150">Sous l’onglet Configuration du proxy, vous devez voir l’adresse du proxy, qui doit être la même que celle figurant dans les paramètres du Registre.</span><span class="sxs-lookup"><span data-stu-id="07c12-150">Under Proxy Configuration tab, you should see the proxy address, which should be same as shown by the registry settings.</span></span> <span data-ttu-id="07c12-151">Si ce n’est pas le cas, remplacez-la par la même adresse.</span><span class="sxs-lookup"><span data-stu-id="07c12-151">If not, please change it to the same address.</span></span>

![Activer la réplication](./media/site-recovery-protection-common-errors/mabproxy.png)

* <span data-ttu-id="07c12-153">**Vérifiez si la bande passante de limitation n’est pas limitée sur le serveur de traitement** : augmentez la bande passante et vérifiez si le problème persiste.</span><span class="sxs-lookup"><span data-stu-id="07c12-153">**Check if Throttle bandwidth is not constrained on Process server**:  Increase the bandwidth  and check if the problem still exists.</span></span>

##<a name="next-steps"></a><span data-ttu-id="07c12-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="07c12-154">Next steps</span></span>
<span data-ttu-id="07c12-155">Si vous avez besoin d’aide, posez votre question sur le [forum ASR](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="07c12-155">If you need more help, then post your query to [ASR forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span></span> <span data-ttu-id="07c12-156">Nous avons une communauté active et un de nos ingénieurs pourra vous aider.</span><span class="sxs-lookup"><span data-stu-id="07c12-156">We have an active community and one of our engineers will be able to assist you.</span></span>