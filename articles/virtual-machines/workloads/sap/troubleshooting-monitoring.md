---
title: aaaTroubleshooting et surveillance de HANA SAP sur Azure (Instances de grande taille) | Documents Microsoft
description: "Résolvez les problèmes et surveillez SAP HANA sur Azure (grandes instances)."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1f1cd35820e227fd99af495431cd4b826aa53600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a><span data-ttu-id="f22e1-103">Comment tootroubleshoot et analyse SAP HANA (instances de grande taille) sur Azure</span><span class="sxs-lookup"><span data-stu-id="f22e1-103">How tootroubleshoot and monitor SAP HANA (large instances) on Azure</span></span>


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a><span data-ttu-id="f22e1-104">Surveillance de SAP HANA sur Azure (grandes instances)</span><span class="sxs-lookup"><span data-stu-id="f22e1-104">Monitoring in SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="f22e1-105">SAP HANA sur Azure (Instances de grande taille) n’est pas différente de n’importe quel autre déploiement IaaS, vous devez toomonitor que hello du système d’exploitation et application hello cela et comment ces consomment hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="f22e1-105">SAP HANA on Azure (Large Instances) is no different from any other IaaS deployment — you need toomonitor what hello OS and hello application is doing and how these consume hello following resources:</span></span>

- <span data-ttu-id="f22e1-106">UC</span><span class="sxs-lookup"><span data-stu-id="f22e1-106">CPU</span></span>
- <span data-ttu-id="f22e1-107">Mémoire</span><span class="sxs-lookup"><span data-stu-id="f22e1-107">Memory</span></span>
- <span data-ttu-id="f22e1-108">Bande passante réseau</span><span class="sxs-lookup"><span data-stu-id="f22e1-108">Network bandwidth</span></span>
- <span data-ttu-id="f22e1-109">Espace disque</span><span class="sxs-lookup"><span data-stu-id="f22e1-109">Disk space</span></span>

<span data-ttu-id="f22e1-110">Comme avec les Machines virtuelles Azure, vous devez toofigure indique si les classes de ressources hello susmentionnées sont suffisants, ou si ces obtient épuisées.</span><span class="sxs-lookup"><span data-stu-id="f22e1-110">As with Azure Virtual Machines you need toofigure out whether hello resource classes named above are sufficient, or whether these get depleted.</span></span> <span data-ttu-id="f22e1-111">Voici plus de détails sur chacune des différentes classes de hello :</span><span class="sxs-lookup"><span data-stu-id="f22e1-111">Here is more detail on each of hello different classes:</span></span>

<span data-ttu-id="f22e1-112">**La consommation des ressources du processeur :** ratio de hello SAP définie pour certaines charges de travail par rapport à HANA est appliquée toomake sûr qu’il doit y avoir suffisamment toowork disponible de ressources du processeur par le biais des données hello qui sont stockées en mémoire.</span><span class="sxs-lookup"><span data-stu-id="f22e1-112">**CPU resource consumption:** hello ratio that SAP defined for certain workload against HANA is enforced toomake sure that there should be enough CPU resources available toowork through hello data that is stored in memory.</span></span> <span data-ttu-id="f22e1-113">Néanmoins, il peut arriver où HANA consomme beaucoup d’UC à exécuter des requêtes d’échéance toomissing index ou des problèmes similaires.</span><span class="sxs-lookup"><span data-stu-id="f22e1-113">Nevertheless, there might be cases where HANA consumes a lot of CPU executing queries due toomissing indexes or similar issues.</span></span> <span data-ttu-id="f22e1-114">Cela signifie que vous devez surveiller la consommation des ressources du processeur de l’unité de grande instance HANA hello, ainsi que des ressources UC utilisée par les services HANA hello spécifiques.</span><span class="sxs-lookup"><span data-stu-id="f22e1-114">This means you should monitor CPU resource consumption of hello HANA large instance unit as well as CPU resources consumed by hello specific HANA services.</span></span>

<span data-ttu-id="f22e1-115">**La consommation de mémoire :** est important toomonitor à partir de HANA, ainsi qu’en dehors de HANA sur l’unité de hello.</span><span class="sxs-lookup"><span data-stu-id="f22e1-115">**Memory consumption:** Is important toomonitor from within HANA, as well as outside of HANA on hello unit.</span></span> <span data-ttu-id="f22e1-116">Dans HANA, surveiller la façon dont les données de salutation consomme HANA alloué de la mémoire dans toostay order dans hello requis d’instructions de SAP de dimensionnement.</span><span class="sxs-lookup"><span data-stu-id="f22e1-116">Within HANA, monitor how hello data is consuming HANA allocated memory in order toostay within hello required sizing guidelines of SAP.</span></span> <span data-ttu-id="f22e1-117">Vous souhaitez également la consommation de mémoire de toomonitor hello grande Instance niveau toomake assurer que les logiciels supplémentaires HANA-non installé ne consomment trop de mémoire et par conséquent sont en concurrence avec HANA pour la mémoire.</span><span class="sxs-lookup"><span data-stu-id="f22e1-117">You also want toomonitor memory consumption on hello Large Instance level toomake sure that additional installed non-HANA software does not consume too much memory, and therefore compete with HANA for memory.</span></span>

<span data-ttu-id="f22e1-118">**La bande passante réseau :** passerelle de réseau virtuel Azure hello est limitée de la bande passante des données en transit dans hello réseau virtuel Azure, il est donc utile toomonitor les données de salutation reçues par tous les hello machines virtuelles de Azure dans un toofigure de réseau virtuel comment fermer vous sont les limites de toohello de hello Azure référence (SKU), vous avez sélectionné la passerelle.</span><span class="sxs-lookup"><span data-stu-id="f22e1-118">**Network bandwidth:** hello Azure VNet gateway is limited in bandwidth of data moving into hello Azure VNet, so it is helpful toomonitor hello data received by all hello Azure VMs within a VNet toofigure out how close you are toohello limits of hello Azure gateway SKU you selected.</span></span> <span data-ttu-id="f22e1-119">Sur l’unité d’Instance est importante HANA hello, il fait sens toomonitor entrants et sortants le trafic réseau également et suivre tookeep de volumes hello qui sont gérés au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="f22e1-119">On hello HANA Large Instance unit, it does make sense toomonitor incoming and outgoing network traffic as well, and tookeep track of hello volumes that are handled over time.</span></span>

<span data-ttu-id="f22e1-120">**Espace disque :** la consommation d’espace disque augmente généralement au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="f22e1-120">**Disk space:** Disk space consumption usually increases over time.</span></span> <span data-ttu-id="f22e1-121">Il existe plusieurs raisons à cela, les principales étant les suivantes : augmentation du volume de données, exécution de sauvegardes des journaux de transaction, stockage des fichiers de trace et création d’instantanés du stockage.</span><span class="sxs-lookup"><span data-stu-id="f22e1-121">There are many reasons for this, but most of all are: data volume increases, execution of transaction log backups, storing trace files, and performing storage snapshots.</span></span> <span data-ttu-id="f22e1-122">Par conséquent, il est l’utilisation d’espace disque important toomonitor et gérer l’espace disque hello associé hello HANA grande Instance unité.</span><span class="sxs-lookup"><span data-stu-id="f22e1-122">Therefore, it is important toomonitor disk space usage and manage hello disk space associated with hello HANA Large Instance unit.</span></span>

## <a name="monitoring-and-troubleshooting-from-hana-side"></a><span data-ttu-id="f22e1-123">Surveillance et dépannage à partir de HANA</span><span class="sxs-lookup"><span data-stu-id="f22e1-123">Monitoring and troubleshooting from HANA side</span></span>

<span data-ttu-id="f22e1-124">Dans l’ordre tooeffectively analyser tooSAP de problèmes connexes HANA sur Azure (Instances de grande taille), il est utile toonarrow vers le bas hello cause d’un problème.</span><span class="sxs-lookup"><span data-stu-id="f22e1-124">In order tooeffectively analyze problems related tooSAP HANA on Azure (Large Instances), it is useful toonarrow down hello root cause of a problem.</span></span> <span data-ttu-id="f22e1-125">SAP a publié une grande quantité de documentation toohelp vous.</span><span class="sxs-lookup"><span data-stu-id="f22e1-125">SAP has published a large amount of documentation toohelp you.</span></span>

<span data-ttu-id="f22e1-126">Vous trouverez applicable FAQ tooSAP connexes HANA performances Bonjour suit les Notes SAP :</span><span class="sxs-lookup"><span data-stu-id="f22e1-126">Applicable FAQs related tooSAP HANA performance can be found in hello following SAP Notes:</span></span>

- [<span data-ttu-id="f22e1-127">Note SAP #2222200 – FAQ : réseau SAP HANA</span><span class="sxs-lookup"><span data-stu-id="f22e1-127">SAP Note #2222200 – FAQ: SAP HANA Network</span></span>](https://launchpad.support.sap.com/#/notes/2222200)
- [<span data-ttu-id="f22e1-128">Note SAP #2100040 – FAQ : processeur SAP HANA</span><span class="sxs-lookup"><span data-stu-id="f22e1-128">SAP Note #2100040 – FAQ: SAP HANA CPU</span></span>](https://launchpad.support.sap.com/#/notes/0002100040)
- [<span data-ttu-id="f22e1-129">Note SAP #199997 – FAQ : mémoire SAP HANA</span><span class="sxs-lookup"><span data-stu-id="f22e1-129">SAP Note #199997 – FAQ: SAP HANA Memory</span></span>](https://launchpad.support.sap.com/#/notes/2177064)
- [<span data-ttu-id="f22e1-130">Note SAP #200000 – FAQ : optimisation des performances de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="f22e1-130">SAP Note #200000 – FAQ: SAP HANA Performance Optimization</span></span>](https://launchpad.support.sap.com/#/notes/2000000)
- [<span data-ttu-id="f22e1-131">Note SAP #199930 – FAQ : analyse d’E/S SAP HANA</span><span class="sxs-lookup"><span data-stu-id="f22e1-131">SAP Note #199930 – FAQ: SAP HANA I/O Analysis</span></span>](https://launchpad.support.sap.com/#/notes/1999930)
- [<span data-ttu-id="f22e1-132">Note SAP #2177064 – FAQ : incidents et redémarrage du service SAP HANA</span><span class="sxs-lookup"><span data-stu-id="f22e1-132">SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes</span></span>](https://launchpad.support.sap.com/#/notes/2177064)

<span data-ttu-id="f22e1-133">**Alertes SAP HANA**</span><span class="sxs-lookup"><span data-stu-id="f22e1-133">**SAP HANA Alerts**</span></span>

<span data-ttu-id="f22e1-134">Dans un premier temps, vérifiez hello SAP HANA alerte le journal actuel.</span><span class="sxs-lookup"><span data-stu-id="f22e1-134">As a first step, check hello current SAP HANA alert logs.</span></span> <span data-ttu-id="f22e1-135">Dans SAP HANA Studio, accédez trop**Console d’Administration : alertes : afficher : toutes les alertes**.</span><span class="sxs-lookup"><span data-stu-id="f22e1-135">In SAP HANA Studio, go too**Administration Console: Alerts: Show: all alerts**.</span></span> <span data-ttu-id="f22e1-136">Cet onglet affiche toutes les alertes de SAP HANA pour valeurs spécifiques (mémoire physique disponible, l’utilisation du processeur, etc.) qui se trouvent en dehors de hello valeur minimale et maximales seuils.</span><span class="sxs-lookup"><span data-stu-id="f22e1-136">This tab will show all SAP HANA alerts for specific values (free physical memory, CPU utilization, etc.) that fall outside of hello set minimum and maximum thresholds.</span></span> <span data-ttu-id="f22e1-137">Par défaut, les vérifications sont effectuées automatiquement toutes les 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="f22e1-137">By default, checks are auto-refreshed every 15 minutes.</span></span>

![Dans SAP HANA Studio, accédez à tooAdministration Console : alertes : afficher : toutes les alertes](./media/troubleshooting-monitoring/image1-show-alerts.png)

<span data-ttu-id="f22e1-139">**UC**</span><span class="sxs-lookup"><span data-stu-id="f22e1-139">**CPU**</span></span>

<span data-ttu-id="f22e1-140">Pour une alerte déclenchée en raison du paramètre de seuil tooimproper, une résolution est tooreset toohello par défaut ou une valeur de seuil plus raisonnable.</span><span class="sxs-lookup"><span data-stu-id="f22e1-140">For an alert triggered due tooimproper threshold setting, a resolution is tooreset toohello default value or a more reasonable threshold value.</span></span>

![Réinitialiser la valeur par défaut de toohello ou une valeur de seuil plus raisonnable](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

<span data-ttu-id="f22e1-142">Hello suivant alertes peut-être indiquer des problèmes de ressources de processeur :</span><span class="sxs-lookup"><span data-stu-id="f22e1-142">hello following alerts may indicate CPU resource problems:</span></span>

- <span data-ttu-id="f22e1-143">Utilisation du processeur hôte (alerte 5)</span><span class="sxs-lookup"><span data-stu-id="f22e1-143">Host CPU Usage (Alert 5)</span></span>
- <span data-ttu-id="f22e1-144">Dernière opération de point de sauvegarde (alerte 28)</span><span class="sxs-lookup"><span data-stu-id="f22e1-144">Most recent savepoint operation (Alert 28)</span></span>
- <span data-ttu-id="f22e1-145">Durée du point de sauvegarde (alerte 54)</span><span class="sxs-lookup"><span data-stu-id="f22e1-145">Savepoint duration (Alert 54)</span></span>

<span data-ttu-id="f22e1-146">Vous pouvez remarquer la consommation élevée de processeur sur votre base de données SAP HANA à partir de hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="f22e1-146">You may notice high CPU consumption on your SAP HANA database from one of hello following:</span></span>

- <span data-ttu-id="f22e1-147">L’alerte 5 (Utilisation du processeur hôte) est déclenchée pour l’utilisation actuelle ou passée du processeur</span><span class="sxs-lookup"><span data-stu-id="f22e1-147">Alert 5 (Host CPU usage) is raised for current or past CPU usage</span></span>
- <span data-ttu-id="f22e1-148">Hello affiche l’utilisation du processeur sur l’écran de présentation hello</span><span class="sxs-lookup"><span data-stu-id="f22e1-148">hello displayed CPU usage on hello overview screen</span></span>

![Affiche l’utilisation du processeur sur l’écran de présentation hello](./media/troubleshooting-monitoring/image3-cpu-usage.png)

<span data-ttu-id="f22e1-150">graphique de charge Hello peut afficher la consommation élevée de l’UC, ou une consommation élevée Bonjour dernières :</span><span class="sxs-lookup"><span data-stu-id="f22e1-150">hello Load graph might show high CPU consumption, or high consumption in hello past:</span></span>

![graphique de charge Hello peut afficher consommation élevée de l’UC, ou une consommation élevée Bonjour précédentes](./media/troubleshooting-monitoring/image4-load-graph.png)

<span data-ttu-id="f22e1-152">Une alerte déclenchée en raison de l’utilisation du processeur de toohigh peut être dû à plusieurs raisons, y compris, mais non limité à : l’exécution de certaines transactions, le chargement de données en retrait des tâches longues instructions SQL et les performances de requête non optimaux (par exemple, avec BW sur HANA cubes).</span><span class="sxs-lookup"><span data-stu-id="f22e1-152">An alert triggered due toohigh CPU utilization could be caused by several reasons, including, but not limited to: execution of certain transactions, data loading, hanging of jobs, long running SQL statements, and bad query performance (for example, with BW on HANA cubes).</span></span>

<span data-ttu-id="f22e1-153">Consultez toohello [dépannage de SAP HANA : provoque connexes du processeur et les Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) de site pour les étapes de dépannage détaillées.</span><span class="sxs-lookup"><span data-stu-id="f22e1-153">Refer toohello [SAP HANA Troubleshooting: CPU Related Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="f22e1-154">**Système d’exploitation**</span><span class="sxs-lookup"><span data-stu-id="f22e1-154">**Operating System**</span></span>

<span data-ttu-id="f22e1-155">Une des plus importantes de hello vérifie pour SAP HANA sur Linux est toomake assurer que les Pages de grande Transparent sont désactivées, consultez [2131662 de # de la Note SAP – Transparent énorme Pages (THP) sur les serveurs SAP HANA](https://launchpad.support.sap.com/#/notes/2131662).</span><span class="sxs-lookup"><span data-stu-id="f22e1-155">One of hello most important checks for SAP HANA on Linux is toomake sure that Transparent Huge Pages are disabled, see [SAP Note #2131662 – Transparent Huge Pages (THP) on SAP HANA Servers](https://launchpad.support.sap.com/#/notes/2131662).</span></span>

- <span data-ttu-id="f22e1-156">Vous pouvez vérifier si les Pages énorme Transparent sont activés via hello Linux commande suivante : **cat /sys/kernel/mm/transparent\_hugepage/activé**</span><span class="sxs-lookup"><span data-stu-id="f22e1-156">You can check if Transparent Huge Pages are enabled through hello following Linux command: **cat /sys/kernel/mm/transparent\_hugepage/enabled**</span></span>
- <span data-ttu-id="f22e1-157">Si _toujours_ est placé entre crochets, comme indiqué ci-dessous, cela signifie que les Pages de grande Transparent hello sont activés : madvise [toujours] jamais ; si _jamais_ est placé entre crochets, comme indiqué ci-dessous, cela signifie que hello Transparent Pages énormes sont désactivées : madvise toujours [jamais]</span><span class="sxs-lookup"><span data-stu-id="f22e1-157">If _always_ is enclosed in brackets as below, it means that hello Transparent Huge Pages are enabled: [always] madvise never; if _never_ is enclosed in brackets as below, it means that hello Transparent Huge Pages are disabled: always madvise [never]</span></span>

<span data-ttu-id="f22e1-158">Hello après la commande Linux doit retourner la valeur nothing : **rpm - qa | grep ulimit.**</span><span class="sxs-lookup"><span data-stu-id="f22e1-158">hello following Linux command should return nothing: **rpm -qa | grep ulimit.**</span></span> <span data-ttu-id="f22e1-159">Si _ulimit_ est installé, désinstallez-le immédiatement.</span><span class="sxs-lookup"><span data-stu-id="f22e1-159">If it appears _ulimit_ is installed, uninstall it immediately.</span></span>

<span data-ttu-id="f22e1-160">**Mémoire**</span><span class="sxs-lookup"><span data-stu-id="f22e1-160">**Memory**</span></span>

<span data-ttu-id="f22e1-161">Vous pouvez observer ce montant hello de mémoire allouée par hello SAP HANA, base de données est plus élevée que prévu.</span><span class="sxs-lookup"><span data-stu-id="f22e1-161">You may observe that hello amount of memory allocated by hello SAP HANA database is higher than expected.</span></span> <span data-ttu-id="f22e1-162">Hello suivant les alertes indique des problèmes de mémoire :</span><span class="sxs-lookup"><span data-stu-id="f22e1-162">hello following alerts indicate issues with high memory usage:</span></span>

- <span data-ttu-id="f22e1-163">Utilisation de la mémoire physique de l’hôte (alerte 1)</span><span class="sxs-lookup"><span data-stu-id="f22e1-163">Host physical memory usage (Alert 1)</span></span>
- <span data-ttu-id="f22e1-164">Utilisation de la mémoire du serveur de noms (alerte 12)</span><span class="sxs-lookup"><span data-stu-id="f22e1-164">Memory usage of name server (Alert 12)</span></span>
- <span data-ttu-id="f22e1-165">Utilisation totale de la mémoire des tables de la banque des colonnes (alerte 40)</span><span class="sxs-lookup"><span data-stu-id="f22e1-165">Total memory usage of Column Store tables (Alert 40)</span></span>
- <span data-ttu-id="f22e1-166">Utilisation de la mémoire des services (alerte 43)</span><span class="sxs-lookup"><span data-stu-id="f22e1-166">Memory usage of services (Alert 43)</span></span>
- <span data-ttu-id="f22e1-167">Utilisation de la mémoire du stockage principal des tables de la banque des colonnes (alerte 45)</span><span class="sxs-lookup"><span data-stu-id="f22e1-167">Memory usage of main storage of Column Store tables (Alert 45)</span></span>
- <span data-ttu-id="f22e1-168">Fichiers de vidage runtime (alerte 46)</span><span class="sxs-lookup"><span data-stu-id="f22e1-168">Runtime dump files (Alert 46)</span></span>

<span data-ttu-id="f22e1-169">Consultez toohello [dépannage de SAP HANA : problèmes de mémoire](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) de site pour les étapes de dépannage détaillées.</span><span class="sxs-lookup"><span data-stu-id="f22e1-169">Refer toohello [SAP HANA Troubleshooting: Memory Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="f22e1-170">**Réseau**</span><span class="sxs-lookup"><span data-stu-id="f22e1-170">**Network**</span></span>

<span data-ttu-id="f22e1-171">Consultez trop[2081065 de # SAP Remarque : résolution des problèmes de réseau de HANA SAP](https://launchpad.support.sap.com/#/notes/2081065) et effectuer des étapes dans cette Note SAP de dépannage du réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="f22e1-171">Refer too[SAP Note #2081065 – Troubleshooting SAP HANA Network](https://launchpad.support.sap.com/#/notes/2081065) and perform hello network troubleshooting steps in this SAP Note.</span></span>

1. <span data-ttu-id="f22e1-172">Analyse des temps d’aller-retour entre le client et le serveur.</span><span class="sxs-lookup"><span data-stu-id="f22e1-172">Analyzing round-trip time between server and client.</span></span>
  <span data-ttu-id="f22e1-173">R :</span><span class="sxs-lookup"><span data-stu-id="f22e1-173">A.</span></span> <span data-ttu-id="f22e1-174">Exécuter le script SQL de hello [ _HANA\_réseau\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="f22e1-174">Run hello SQL script [_HANA\_Network\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>
  
2. <span data-ttu-id="f22e1-175">Analysez la communication entre les nœuds.</span><span class="sxs-lookup"><span data-stu-id="f22e1-175">Analyze internode communication.</span></span>
  <span data-ttu-id="f22e1-176">A.</span><span class="sxs-lookup"><span data-stu-id="f22e1-176">A.</span></span> <span data-ttu-id="f22e1-177">Exécutez le script SQL [_HANA\_Réseau\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="f22e1-177">Run SQL script [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>

3. <span data-ttu-id="f22e1-178">Exécutez la commande Linux **ifconfig** (sortie de hello indique si les pertes de paquets sont produisent).</span><span class="sxs-lookup"><span data-stu-id="f22e1-178">Run Linux command **ifconfig** (hello output shows if any packet losses are occurring).</span></span>
4. <span data-ttu-id="f22e1-179">Exécutez la commande Linux **tcpdump**.</span><span class="sxs-lookup"><span data-stu-id="f22e1-179">Run Linux command **tcpdump**.</span></span>

<span data-ttu-id="f22e1-180">En outre, utilisez ouvrir la source de hello [IPERF](https://iperf.fr/) outil (ou similaire) toomeasure des performances de réseau véritable application.</span><span class="sxs-lookup"><span data-stu-id="f22e1-180">Also, use hello open source [IPERF](https://iperf.fr/) tool (or similar) toomeasure real application network performance.</span></span>

<span data-ttu-id="f22e1-181">Consultez toohello [dépannage de SAP HANA : mise en réseau des performances et des problèmes de connectivité](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) de site pour les étapes de dépannage détaillées.</span><span class="sxs-lookup"><span data-stu-id="f22e1-181">Refer toohello [SAP HANA Troubleshooting: Networking Performance and Connectivity Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="f22e1-182">**Stockage**</span><span class="sxs-lookup"><span data-stu-id="f22e1-182">**Storage**</span></span>

<span data-ttu-id="f22e1-183">À partir d’un point de vue de l’utilisateur final, une application (ou système hello dans son ensemble) s’exécute lentement, ne répond pas ou peut sembler même toohang si des problèmes avec les performances d’e/s.</span><span class="sxs-lookup"><span data-stu-id="f22e1-183">From an end-user perspective, an application (or hello system as a whole) runs sluggishly, is unresponsive, or can even seem toohang if there are issues with I/O performance.</span></span> <span data-ttu-id="f22e1-184">Bonjour **Volumes** onglet dans SAP HANA Studio, vous pouvez voir hello attaché volumes et les volumes sont utilisés par chaque service.</span><span class="sxs-lookup"><span data-stu-id="f22e1-184">In hello **Volumes** tab in SAP HANA Studio, you can see hello attached volumes, and what volumes are used by each service.</span></span>

![Dans l’onglet de Volumes hello dans SAP HANA Studio, vous pouvez voir hello attaché volumes et les volumes sont utilisés par chaque service](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

<span data-ttu-id="f22e1-186">Les volumes associés dans la partie inférieure de hello d’écran hello de que vous pouvez voir les détails hello volumes, tels que les fichiers et les statistiques d’e/s.</span><span class="sxs-lookup"><span data-stu-id="f22e1-186">Attached volumes in hello lower part of hello screen you can see details of hello volumes, such as files and I/O statistics.</span></span>

![Les volumes associés dans la partie inférieure de hello d’écran hello de que vous pouvez voir les détails hello volumes, tels que les fichiers et les statistiques d’e/s](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

<span data-ttu-id="f22e1-188">Consultez toohello [dépannage de SAP HANA : e/s associées Causes principales et les Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) et [dépannage de SAP HANA : disque connexes Causes principales et les Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) de site pour les étapes de dépannage détaillées.</span><span class="sxs-lookup"><span data-stu-id="f22e1-188">Refer toohello [SAP HANA Troubleshooting: I/O Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) and [SAP HANA Troubleshooting: Disk Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="f22e1-189">**Outils de diagnostic**</span><span class="sxs-lookup"><span data-stu-id="f22e1-189">**Diagnostic Tools**</span></span>

<span data-ttu-id="f22e1-190">Effectuez une vérification d’intégrité de SAP HANA via HANA\_Configuration\_Minichecks.</span><span class="sxs-lookup"><span data-stu-id="f22e1-190">Perform an SAP HANA Health Check through HANA\_Configuration\_Minichecks.</span></span> <span data-ttu-id="f22e1-191">Cet outil signale les problèmes techniques critiques potentiels qui devraient déjà avoir déclenché une alerte dans SAP HANA Studio.</span><span class="sxs-lookup"><span data-stu-id="f22e1-191">This tool returns potentially critical technical issues that should have already been raised as alerts in SAP HANA Studio.</span></span>

<span data-ttu-id="f22e1-192">Consultez trop[1969700 de # SAP Remarque : collection d’instructions SQL pour SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) et téléchargez hello SQL Statements.zip fichier joint toothat Remarque.</span><span class="sxs-lookup"><span data-stu-id="f22e1-192">Refer too[SAP Note #1969700 – SQL statement collection for SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) and download hello SQL Statements.zip file attached toothat note.</span></span> <span data-ttu-id="f22e1-193">Stockez ce fichier .zip sur le disque dur local hello.</span><span class="sxs-lookup"><span data-stu-id="f22e1-193">Store this .zip file on hello local hard drive.</span></span>

<span data-ttu-id="f22e1-194">Dans Studio SAP HANA, hello **informations système** droit Bonjour **nom** colonne et sélectionnez **instructions d’importation SQL**.</span><span class="sxs-lookup"><span data-stu-id="f22e1-194">In SAP HANA Studio, on hello **System Information** tab, right-click in hello **Name** column and select **Import SQL Statements**.</span></span>

![Dans SAP HANA Studio, sur l’onglet informations de système de hello, avec le bouton droit dans la colonne de nom hello et sélectionnez Importer des instructions SQL](./media/troubleshooting-monitoring/image7-import-statements-a.png)

<span data-ttu-id="f22e1-196">Sélectionnez hello SQL Statements.zip fichier stocké localement, et un dossier avec des instructions SQL correspondantes hello est importé.</span><span class="sxs-lookup"><span data-stu-id="f22e1-196">Select hello SQL Statements.zip file stored locally, and a folder with hello corresponding SQL statements will be imported.</span></span> <span data-ttu-id="f22e1-197">À ce stade, hello que nombreux différents contrôles de diagnostic peuvent être exécutés avec les instructions SQL.</span><span class="sxs-lookup"><span data-stu-id="f22e1-197">At this point, hello many different diagnostic checks can be run with these SQL statements.</span></span>

<span data-ttu-id="f22e1-198">Par exemple, les besoins en bande passante de réplication du système SAP HANA tootest, droit hello **la bande passante** instruction sous **réplication : la bande passante** et sélectionnez **ouvrir** dans la Console SQL.</span><span class="sxs-lookup"><span data-stu-id="f22e1-198">For example, tootest SAP HANA System Replication bandwidth requirements, right-click hello **Bandwidth** statement under **Replication: Bandwidth** and select **Open** in SQL Console.</span></span>

<span data-ttu-id="f22e1-199">instruction SQL complète de Hello ouvre permettant toobe de paramètres d’entrée (section modification) modifié et exécutées.</span><span class="sxs-lookup"><span data-stu-id="f22e1-199">hello complete SQL statement opens allowing input parameters (modification section) toobe changed and then executed.</span></span>

![instruction SQL complète de Hello ouvre permettant toobe de paramètres d’entrée (section modification) modifié et exécutée](./media/troubleshooting-monitoring/image8-import-statements-b.png)

<span data-ttu-id="f22e1-201">Un autre exemple est avec le bouton droit sur les instructions hello sous **réplication : vue d’ensemble**.</span><span class="sxs-lookup"><span data-stu-id="f22e1-201">Another example is right-clicking on hello statements under **Replication: Overview**.</span></span> <span data-ttu-id="f22e1-202">Sélectionnez **Execute** à partir du menu contextuel de hello :</span><span class="sxs-lookup"><span data-stu-id="f22e1-202">Select **Execute** from hello context menu:</span></span>

![Un autre exemple est avec le bouton droit sur les instructions hello sous réplication : vue d’ensemble.](./media/troubleshooting-monitoring/image9-import-statements-c.png)

<span data-ttu-id="f22e1-205">Vous obtenez ainsi des informations qui vous aident à résoudre le problème :</span><span class="sxs-lookup"><span data-stu-id="f22e1-205">This results in information that helps with troubleshooting:</span></span>

![Vous obtenez ainsi des informations qui vous aident à résoudre le problème](./media/troubleshooting-monitoring/image10-import-statements-d.png)

<span data-ttu-id="f22e1-207">De même hello pour HANA\_Configuration\_Minichecks et recherchez les _X_ marques Bonjour _C_ (critique) colonne.</span><span class="sxs-lookup"><span data-stu-id="f22e1-207">Do hello same for HANA\_Configuration\_Minichecks and check for any _X_ marks in hello _C_ (Critical) column.</span></span>

<span data-ttu-id="f22e1-208">Exemples de sortie :</span><span class="sxs-lookup"><span data-stu-id="f22e1-208">Sample outputs:</span></span>

<span data-ttu-id="f22e1-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** pour les vérifications SAP HANA générales.</span><span class="sxs-lookup"><span data-stu-id="f22e1-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** for general SAP HANA checks.</span></span>

![HANA\_Configuration\_MiniChecks\_Rev102.01+1 pour les vérifications SAP HANA générales](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

<span data-ttu-id="f22e1-211">**HANA\_Services\_Overview** pour une vue d’ensemble des exécutions actuelles des services SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="f22e1-211">**HANA\_Services\_Overview** for an overview of what SAP HANA services are currently running.</span></span>

![HANA\_Services\_Overview pour une vue d’ensemble des exécutions actuelles des services SAP HANA](./media/troubleshooting-monitoring/image12-services-overview.png)

<span data-ttu-id="f22e1-213">**HANA\_Services\_Statistics** pour les informations de service SAP HANA (processeur, mémoire, etc.).</span><span class="sxs-lookup"><span data-stu-id="f22e1-213">**HANA\_Services\_Statistics** for SAP HANA service information (CPU, memory, etc.).</span></span>

![<span data-ttu-id="f22e1-214">HANA\_Services\_Statistics pour les informations de service SAP HANA</span><span class="sxs-lookup"><span data-stu-id="f22e1-214">HANA\_Services\_Statistics for SAP HANA service information</span></span> ](./media/troubleshooting-monitoring/image13-services-statistics.png)

<span data-ttu-id="f22e1-215">**HANA\_Configuration\_vue d’ensemble\_Rev110 +** pour des informations générales sur l’instance de SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="f22e1-215">**HANA\_Configuration\_Overview\_Rev110+** for general information on hello SAP HANA instance.</span></span>

![HANA\_Configuration\_vue d’ensemble\_Rev110 + pour des informations générales sur l’instance de SAP HANA hello](./media/troubleshooting-monitoring/image14-configuration-overview.png)

<span data-ttu-id="f22e1-217">**HANA\_Configuration\_paramètres\_Rev70 +** toocheck les paramètres de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="f22e1-217">**HANA\_Configuration\_Parameters\_Rev70+** toocheck SAP HANA parameters.</span></span>

![HANA\_Configuration\_paramètres\_toocheck Rev70 +, paramètres de SAP HANA](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

