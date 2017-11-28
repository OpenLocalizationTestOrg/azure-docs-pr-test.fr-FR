---
title: "Résolution des problèmes et surveillance de SAP HANA sur Azure (grandes instances) | Microsoft Docs"
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
ms.openlocfilehash: ee5be707b443cbe42bf4a492d79390e534d4b91f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-troubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a><span data-ttu-id="cf978-103">Guide pratique de résolution des problèmes et de surveillance de SAP HANA (grandes instances) sur Azure</span><span class="sxs-lookup"><span data-stu-id="cf978-103">How to troubleshoot and monitor SAP HANA (large instances) on Azure</span></span>


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a><span data-ttu-id="cf978-104">Surveillance de SAP HANA sur Azure (grandes instances)</span><span class="sxs-lookup"><span data-stu-id="cf978-104">Monitoring in SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="cf978-105">SAP HANA sur Azure (grandes instances) est semblable aux autres déploiements IaaS, dans le sens où vous devez surveiller les actions du système d’exploitation et de l’application, et comment ils consomment les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="cf978-105">SAP HANA on Azure (Large Instances) is no different from any other IaaS deployment — you need to monitor what the OS and the application is doing and how these consume the following resources:</span></span>

- <span data-ttu-id="cf978-106">UC</span><span class="sxs-lookup"><span data-stu-id="cf978-106">CPU</span></span>
- <span data-ttu-id="cf978-107">Mémoire</span><span class="sxs-lookup"><span data-stu-id="cf978-107">Memory</span></span>
- <span data-ttu-id="cf978-108">Bande passante réseau</span><span class="sxs-lookup"><span data-stu-id="cf978-108">Network bandwidth</span></span>
- <span data-ttu-id="cf978-109">Espace disque</span><span class="sxs-lookup"><span data-stu-id="cf978-109">Disk space</span></span>

<span data-ttu-id="cf978-110">Comme avec les machines virtuelles Azure, vous devez déterminer si les classes de ressources ci-dessus sont suffisantes, ou si elles vont se retrouver épuisées.</span><span class="sxs-lookup"><span data-stu-id="cf978-110">As with Azure Virtual Machines you need to figure out whether the resource classes named above are sufficient, or whether these get depleted.</span></span> <span data-ttu-id="cf978-111">Voici plus de détails sur chacune des classes :</span><span class="sxs-lookup"><span data-stu-id="cf978-111">Here is more detail on each of the different classes:</span></span>

<span data-ttu-id="cf978-112">**Consommation des ressources du processeur :** le ratio défini par SAP pour certaines charges de travail sur HANA est appliqué pour vous assurer que les ressources du processeur disponibles sont suffisantes pour travailler avec les données stockées en mémoire.</span><span class="sxs-lookup"><span data-stu-id="cf978-112">**CPU resource consumption:** The ratio that SAP defined for certain workload against HANA is enforced to make sure that there should be enough CPU resources available to work through the data that is stored in memory.</span></span> <span data-ttu-id="cf978-113">Toutefois, il peut arriver que HANA consomme un grand nombre de requêtes d’exécution du processeur en raison d’index manquants ou de problèmes similaires.</span><span class="sxs-lookup"><span data-stu-id="cf978-113">Nevertheless, there might be cases where HANA consumes a lot of CPU executing queries due to missing indexes or similar issues.</span></span> <span data-ttu-id="cf978-114">Cela signifie que vous devez surveiller la consommation des ressources du processeur de l’unité de grande instance HANA, ainsi que les ressources du processeur consommées par les services HANA spécifiques.</span><span class="sxs-lookup"><span data-stu-id="cf978-114">This means you should monitor CPU resource consumption of the HANA large instance unit as well as CPU resources consumed by the specific HANA services.</span></span>

<span data-ttu-id="cf978-115">**Consommation de mémoire :** sa surveillance est importante dans HANA, ainsi qu’en dehors de HANA sur l’unité.</span><span class="sxs-lookup"><span data-stu-id="cf978-115">**Memory consumption:** Is important to monitor from within HANA, as well as outside of HANA on the unit.</span></span> <span data-ttu-id="cf978-116">Dans HANA, surveillez comment les données consomment la mémoire allouée à HANA, afin de respecter les instructions de dimensionnement de SAP.</span><span class="sxs-lookup"><span data-stu-id="cf978-116">Within HANA, monitor how the data is consuming HANA allocated memory in order to stay within the required sizing guidelines of SAP.</span></span> <span data-ttu-id="cf978-117">Vous devez également surveiller la consommation de mémoire au niveau de la grande instance afin de vous assurer que les logiciels supplémentaires non HANA installés ne consomment pas trop de mémoire, et ne concurrencent donc pas HANA en termes de mémoire.</span><span class="sxs-lookup"><span data-stu-id="cf978-117">You also want to monitor memory consumption on the Large Instance level to make sure that additional installed non-HANA software does not consume too much memory, and therefore compete with HANA for memory.</span></span>

<span data-ttu-id="cf978-118">**Bande passante réseau :** la passerelle de réseau virtuel Azure est limitée en bande passante pour le déplacement des données dans le réseau virtuel Azure. Il est donc utile de surveiller les données reçues par toutes les machines virtuelles Azure au sein d’un réseau virtuel pour déterminer s’il vous reste de la marge par rapport aux limites définies par la référence SKU de la passerelle Azure choisie.</span><span class="sxs-lookup"><span data-stu-id="cf978-118">**Network bandwidth:** The Azure VNet gateway is limited in bandwidth of data moving into the Azure VNet, so it is helpful to monitor the data received by all the Azure VMs within a VNet to figure out how close you are to the limits of the Azure gateway SKU you selected.</span></span> <span data-ttu-id="cf978-119">Sur l’unité de grande instance HANA, il est pertinent de surveiller également le trafic réseau entrant et sortant, et de suivre les volumes qui sont gérés au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="cf978-119">On the HANA Large Instance unit, it does make sense to monitor incoming and outgoing network traffic as well, and to keep track of the volumes that are handled over time.</span></span>

<span data-ttu-id="cf978-120">**Espace disque :** la consommation d’espace disque augmente généralement au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="cf978-120">**Disk space:** Disk space consumption usually increases over time.</span></span> <span data-ttu-id="cf978-121">Il existe plusieurs raisons à cela, les principales étant les suivantes : augmentation du volume de données, exécution de sauvegardes des journaux de transaction, stockage des fichiers de trace et création d’instantanés du stockage.</span><span class="sxs-lookup"><span data-stu-id="cf978-121">There are many reasons for this, but most of all are: data volume increases, execution of transaction log backups, storing trace files, and performing storage snapshots.</span></span> <span data-ttu-id="cf978-122">Par conséquent, il est important de surveiller l’espace disque et de gérer l’espace disque associé à l’unité de grande instance HANA.</span><span class="sxs-lookup"><span data-stu-id="cf978-122">Therefore, it is important to monitor disk space usage and manage the disk space associated with the HANA Large Instance unit.</span></span>

## <a name="monitoring-and-troubleshooting-from-hana-side"></a><span data-ttu-id="cf978-123">Surveillance et dépannage à partir de HANA</span><span class="sxs-lookup"><span data-stu-id="cf978-123">Monitoring and troubleshooting from HANA side</span></span>

<span data-ttu-id="cf978-124">Pour analyser efficacement les problèmes liés à SAP HANA sur Azure (grandes instances), il est utile d’identifier la cause principale d’un problème.</span><span class="sxs-lookup"><span data-stu-id="cf978-124">In order to effectively analyze problems related to SAP HANA on Azure (Large Instances), it is useful to narrow down the root cause of a problem.</span></span> <span data-ttu-id="cf978-125">SAP a publié de nombreux documents pour vous aider.</span><span class="sxs-lookup"><span data-stu-id="cf978-125">SAP has published a large amount of documentation to help you.</span></span>

<span data-ttu-id="cf978-126">Des FAQ pertinentes liées aux performances de SAP HANA se trouvent dans les Notes SAP suivantes :</span><span class="sxs-lookup"><span data-stu-id="cf978-126">Applicable FAQs related to SAP HANA performance can be found in the following SAP Notes:</span></span>

- [<span data-ttu-id="cf978-127">Note SAP #2222200 – FAQ : réseau SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cf978-127">SAP Note #2222200 – FAQ: SAP HANA Network</span></span>](https://launchpad.support.sap.com/#/notes/2222200)
- [<span data-ttu-id="cf978-128">Note SAP #2100040 – FAQ : processeur SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cf978-128">SAP Note #2100040 – FAQ: SAP HANA CPU</span></span>](https://launchpad.support.sap.com/#/notes/0002100040)
- [<span data-ttu-id="cf978-129">Note SAP #199997 – FAQ : mémoire SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cf978-129">SAP Note #199997 – FAQ: SAP HANA Memory</span></span>](https://launchpad.support.sap.com/#/notes/2177064)
- [<span data-ttu-id="cf978-130">Note SAP #200000 – FAQ : optimisation des performances de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cf978-130">SAP Note #200000 – FAQ: SAP HANA Performance Optimization</span></span>](https://launchpad.support.sap.com/#/notes/2000000)
- [<span data-ttu-id="cf978-131">Note SAP #199930 – FAQ : analyse d’E/S SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cf978-131">SAP Note #199930 – FAQ: SAP HANA I/O Analysis</span></span>](https://launchpad.support.sap.com/#/notes/1999930)
- [<span data-ttu-id="cf978-132">Note SAP #2177064 – FAQ : incidents et redémarrage du service SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cf978-132">SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes</span></span>](https://launchpad.support.sap.com/#/notes/2177064)

<span data-ttu-id="cf978-133">**Alertes SAP HANA**</span><span class="sxs-lookup"><span data-stu-id="cf978-133">**SAP HANA Alerts**</span></span>

<span data-ttu-id="cf978-134">Dans un premier temps, vérifiez les journaux d’alerte SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="cf978-134">As a first step, check the current SAP HANA alert logs.</span></span> <span data-ttu-id="cf978-135">Dans SAP HANA Studio, accédez à **Console d’administration: Alertes: Afficher: Toutes les alertes**.</span><span class="sxs-lookup"><span data-stu-id="cf978-135">In SAP HANA Studio, go to **Administration Console: Alerts: Show: all alerts**.</span></span> <span data-ttu-id="cf978-136">Cet onglet affiche toutes les alertes SAP HANA ayant des valeurs spécifiques (mémoire physique disponible, utilisation du processeur, etc.) qui se situent en dehors des seuils minimum et maximum définis.</span><span class="sxs-lookup"><span data-stu-id="cf978-136">This tab will show all SAP HANA alerts for specific values (free physical memory, CPU utilization, etc.) that fall outside of the set minimum and maximum thresholds.</span></span> <span data-ttu-id="cf978-137">Par défaut, les vérifications sont effectuées automatiquement toutes les 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="cf978-137">By default, checks are auto-refreshed every 15 minutes.</span></span>

![Dans SAP HANA Studio, accédez à Console d’administration: Alertes: Afficher: Toutes les alertes](./media/troubleshooting-monitoring/image1-show-alerts.png)

<span data-ttu-id="cf978-139">**UC**</span><span class="sxs-lookup"><span data-stu-id="cf978-139">**CPU**</span></span>

<span data-ttu-id="cf978-140">Pour résoudre une alerte déclenchée en raison d’un paramètre hors du seuil, vous pouvez rétablir la valeur par défaut ou définir une valeur de seuil plus raisonnable.</span><span class="sxs-lookup"><span data-stu-id="cf978-140">For an alert triggered due to improper threshold setting, a resolution is to reset to the default value or a more reasonable threshold value.</span></span>

![Rétablir la valeur par défaut ou définir une valeur de seuil plus raisonnable](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

<span data-ttu-id="cf978-142">Les alertes suivantes peuvent également indiquer des problèmes de ressources de processeur :</span><span class="sxs-lookup"><span data-stu-id="cf978-142">The following alerts may indicate CPU resource problems:</span></span>

- <span data-ttu-id="cf978-143">Utilisation du processeur hôte (alerte 5)</span><span class="sxs-lookup"><span data-stu-id="cf978-143">Host CPU Usage (Alert 5)</span></span>
- <span data-ttu-id="cf978-144">Dernière opération de point de sauvegarde (alerte 28)</span><span class="sxs-lookup"><span data-stu-id="cf978-144">Most recent savepoint operation (Alert 28)</span></span>
- <span data-ttu-id="cf978-145">Durée du point de sauvegarde (alerte 54)</span><span class="sxs-lookup"><span data-stu-id="cf978-145">Savepoint duration (Alert 54)</span></span>

<span data-ttu-id="cf978-146">Les éléments suivants peuvent vous aider à identifier une consommation de processeur élevée sur votre base de données SAP HANA :</span><span class="sxs-lookup"><span data-stu-id="cf978-146">You may notice high CPU consumption on your SAP HANA database from one of the following:</span></span>

- <span data-ttu-id="cf978-147">L’alerte 5 (Utilisation du processeur hôte) est déclenchée pour l’utilisation actuelle ou passée du processeur</span><span class="sxs-lookup"><span data-stu-id="cf978-147">Alert 5 (Host CPU usage) is raised for current or past CPU usage</span></span>
- <span data-ttu-id="cf978-148">L’utilisation du processeur affichée sur l’écran Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="cf978-148">The displayed CPU usage on the overview screen</span></span>

![Utilisation du processeur affichée sur l’écran Vue d’ensemble](./media/troubleshooting-monitoring/image3-cpu-usage.png)

<span data-ttu-id="cf978-150">Le graphique de charge peut indiquer une consommation du processeur élevée, ou une consommation élevée par le passé :</span><span class="sxs-lookup"><span data-stu-id="cf978-150">The Load graph might show high CPU consumption, or high consumption in the past:</span></span>

![Le graphique de charge peut indiquer une consommation du processeur élevée, ou une consommation élevée par le passé](./media/troubleshooting-monitoring/image4-load-graph.png)

<span data-ttu-id="cf978-152">Une alerte déclenchée en raison d’une utilisation élevée du processeur peut être due à plusieurs raisons, y compris, sans toutefois s’y limiter : l’exécution de certaines transactions, le chargement de données, la mise en attente de tâches, les instructions SQL de longue durée et des performances de requête incorrectes (par exemple, avec BW sur des cubes HANA).</span><span class="sxs-lookup"><span data-stu-id="cf978-152">An alert triggered due to high CPU utilization could be caused by several reasons, including, but not limited to: execution of certain transactions, data loading, hanging of jobs, long running SQL statements, and bad query performance (for example, with BW on HANA cubes).</span></span>

<span data-ttu-id="cf978-153">Reportez-vous au site [Dépannage SAP HANA : causes et solutions liées au processeur](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) pour obtenir des étapes de dépannage détaillées.</span><span class="sxs-lookup"><span data-stu-id="cf978-153">Refer to the [SAP HANA Troubleshooting: CPU Related Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="cf978-154">**Système d’exploitation**</span><span class="sxs-lookup"><span data-stu-id="cf978-154">**Operating System**</span></span>

<span data-ttu-id="cf978-155">L’une des principales vérifications à effectuer pour SAP HANA sur Linux est de s’assurer que les THP (Transparent Huge Pages) sont désactivées. Consultez la [Note SAP #2131662 – THP (Transparent Huge Pages) sur les serveurs SAP HANA](https://launchpad.support.sap.com/#/notes/2131662).</span><span class="sxs-lookup"><span data-stu-id="cf978-155">One of the most important checks for SAP HANA on Linux is to make sure that Transparent Huge Pages are disabled, see [SAP Note #2131662 – Transparent Huge Pages (THP) on SAP HANA Servers](https://launchpad.support.sap.com/#/notes/2131662).</span></span>

- <span data-ttu-id="cf978-156">Vous pouvez vérifier si les Transparent Huge Pages sont activées via la commande Linux suivante : **cat /sys/kernel/mm/transparent\_hugepage/enabled**</span><span class="sxs-lookup"><span data-stu-id="cf978-156">You can check if Transparent Huge Pages are enabled through the following Linux command: **cat /sys/kernel/mm/transparent\_hugepage/enabled**</span></span>
- <span data-ttu-id="cf978-157">Si _always_ apparaît entre crochets, comme ci-dessous, cela signifie que les THP sont activées : [always] madvise never ; si _never_ est placé entre crochets, comme ci-dessous, cela signifie que les THP sont désactivées : always madvise [never]</span><span class="sxs-lookup"><span data-stu-id="cf978-157">If _always_ is enclosed in brackets as below, it means that the Transparent Huge Pages are enabled: [always] madvise never; if _never_ is enclosed in brackets as below, it means that the Transparent Huge Pages are disabled: always madvise [never]</span></span>

<span data-ttu-id="cf978-158">La commande Linux suivante ne doit renvoyer aucun résultat : **rpm -qa | grep ulimit.**</span><span class="sxs-lookup"><span data-stu-id="cf978-158">The following Linux command should return nothing: **rpm -qa | grep ulimit.**</span></span> <span data-ttu-id="cf978-159">Si _ulimit_ est installé, désinstallez-le immédiatement.</span><span class="sxs-lookup"><span data-stu-id="cf978-159">If it appears _ulimit_ is installed, uninstall it immediately.</span></span>

<span data-ttu-id="cf978-160">**Mémoire**</span><span class="sxs-lookup"><span data-stu-id="cf978-160">**Memory**</span></span>

<span data-ttu-id="cf978-161">Vous pouvez voir que la quantité de mémoire allouée par la base de données SAP HANA est plus élevée que prévu.</span><span class="sxs-lookup"><span data-stu-id="cf978-161">You may observe that the amount of memory allocated by the SAP HANA database is higher than expected.</span></span> <span data-ttu-id="cf978-162">Les alertes suivantes indiquent des problèmes liés à une utilisation élevée de la mémoire :</span><span class="sxs-lookup"><span data-stu-id="cf978-162">The following alerts indicate issues with high memory usage:</span></span>

- <span data-ttu-id="cf978-163">Utilisation de la mémoire physique de l’hôte (alerte 1)</span><span class="sxs-lookup"><span data-stu-id="cf978-163">Host physical memory usage (Alert 1)</span></span>
- <span data-ttu-id="cf978-164">Utilisation de la mémoire du serveur de noms (alerte 12)</span><span class="sxs-lookup"><span data-stu-id="cf978-164">Memory usage of name server (Alert 12)</span></span>
- <span data-ttu-id="cf978-165">Utilisation totale de la mémoire des tables de la banque des colonnes (alerte 40)</span><span class="sxs-lookup"><span data-stu-id="cf978-165">Total memory usage of Column Store tables (Alert 40)</span></span>
- <span data-ttu-id="cf978-166">Utilisation de la mémoire des services (alerte 43)</span><span class="sxs-lookup"><span data-stu-id="cf978-166">Memory usage of services (Alert 43)</span></span>
- <span data-ttu-id="cf978-167">Utilisation de la mémoire du stockage principal des tables de la banque des colonnes (alerte 45)</span><span class="sxs-lookup"><span data-stu-id="cf978-167">Memory usage of main storage of Column Store tables (Alert 45)</span></span>
- <span data-ttu-id="cf978-168">Fichiers de vidage runtime (alerte 46)</span><span class="sxs-lookup"><span data-stu-id="cf978-168">Runtime dump files (Alert 46)</span></span>

<span data-ttu-id="cf978-169">Reportez-vous au site [Dépannage SAP HANA : problèmes de mémoire](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) pour obtenir des étapes de dépannage détaillées.</span><span class="sxs-lookup"><span data-stu-id="cf978-169">Refer to the [SAP HANA Troubleshooting: Memory Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="cf978-170">**Réseau**</span><span class="sxs-lookup"><span data-stu-id="cf978-170">**Network**</span></span>

<span data-ttu-id="cf978-171">Reportez-vous à la [Note SAP #2081065 – Résolution des problèmes de réseau SAP HANA](https://launchpad.support.sap.com/#/notes/2081065) et suivez les étapes de dépannage réseau qui y sont décrites.</span><span class="sxs-lookup"><span data-stu-id="cf978-171">Refer to [SAP Note #2081065 – Troubleshooting SAP HANA Network](https://launchpad.support.sap.com/#/notes/2081065) and perform the network troubleshooting steps in this SAP Note.</span></span>

1. <span data-ttu-id="cf978-172">Analyse des temps d’aller-retour entre le client et le serveur.</span><span class="sxs-lookup"><span data-stu-id="cf978-172">Analyzing round-trip time between server and client.</span></span>
  <span data-ttu-id="cf978-173">A.</span><span class="sxs-lookup"><span data-stu-id="cf978-173">A.</span></span> <span data-ttu-id="cf978-174">Exécutez le script SQL [_HANA\_Réseau\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="cf978-174">Run the SQL script [_HANA\_Network\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>
  
2. <span data-ttu-id="cf978-175">Analysez la communication entre les nœuds.</span><span class="sxs-lookup"><span data-stu-id="cf978-175">Analyze internode communication.</span></span>
  <span data-ttu-id="cf978-176">A.</span><span class="sxs-lookup"><span data-stu-id="cf978-176">A.</span></span> <span data-ttu-id="cf978-177">Exécutez le script SQL [_HANA\_Réseau\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="cf978-177">Run SQL script [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>

3. <span data-ttu-id="cf978-178">Exécutez la commande Linux **ifconfig** (la sortie indique si des pertes de paquets se produisent).</span><span class="sxs-lookup"><span data-stu-id="cf978-178">Run Linux command **ifconfig** (the output shows if any packet losses are occurring).</span></span>
4. <span data-ttu-id="cf978-179">Exécutez la commande Linux **tcpdump**.</span><span class="sxs-lookup"><span data-stu-id="cf978-179">Run Linux command **tcpdump**.</span></span>

<span data-ttu-id="cf978-180">Utilisez également l’outil open source [IPERF](https://iperf.fr/) (ou tout outil similaire) pour mesurer les véritables performances du réseau d’application.</span><span class="sxs-lookup"><span data-stu-id="cf978-180">Also, use the open source [IPERF](https://iperf.fr/) tool (or similar) to measure real application network performance.</span></span>

<span data-ttu-id="cf978-181">Reportez-vous au site [Dépannage SAP HANA : problèmes de connectivité et de performances réseau](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) pour obtenir des étapes de dépannage détaillées.</span><span class="sxs-lookup"><span data-stu-id="cf978-181">Refer to the [SAP HANA Troubleshooting: Networking Performance and Connectivity Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="cf978-182">**Stockage**</span><span class="sxs-lookup"><span data-stu-id="cf978-182">**Storage**</span></span>

<span data-ttu-id="cf978-183">Du point de vue de l’utilisateur final, une application (ou l’ensemble du système) s’exécute lentement, ne répond pas ou peut même sembler cesser de répondre en cas de problèmes de performances d’E/S.</span><span class="sxs-lookup"><span data-stu-id="cf978-183">From an end-user perspective, an application (or the system as a whole) runs sluggishly, is unresponsive, or can even seem to hang if there are issues with I/O performance.</span></span> <span data-ttu-id="cf978-184">L’onglet **Volumes** de SAP HANA Studio répertorie les volumes associés et les volumes utilisés par chaque service.</span><span class="sxs-lookup"><span data-stu-id="cf978-184">In the **Volumes** tab in SAP HANA Studio, you can see the attached volumes, and what volumes are used by each service.</span></span>

![L’onglet Volumes de SAP HANA Studio répertorie les volumes associés et les volumes utilisés par chaque service](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

<span data-ttu-id="cf978-186">Pour les volumes associés figurant dans la partie inférieure de l’écran, vous pouvez voir les détails des volumes, par exemple les fichiers et les statistiques d’E/S.</span><span class="sxs-lookup"><span data-stu-id="cf978-186">Attached volumes in the lower part of the screen you can see details of the volumes, such as files and I/O statistics.</span></span>

![Pour les volumes associés figurant dans la partie inférieure de l’écran, vous pouvez voir les détails des volumes, par exemple les fichiers et les statistiques d’E/S](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

<span data-ttu-id="cf978-188">Reportez-vous aux sites [Dépannage SAP HANA : causes principales liées à l’E/S et solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) et [Dépannage SAP HANA : causes principales liées au disque et solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) pour obtenir des étapes de dépannage détaillées.</span><span class="sxs-lookup"><span data-stu-id="cf978-188">Refer to the [SAP HANA Troubleshooting: I/O Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) and [SAP HANA Troubleshooting: Disk Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="cf978-189">**Outils de diagnostic**</span><span class="sxs-lookup"><span data-stu-id="cf978-189">**Diagnostic Tools**</span></span>

<span data-ttu-id="cf978-190">Effectuez une vérification d’intégrité de SAP HANA via HANA\_Configuration\_Minichecks.</span><span class="sxs-lookup"><span data-stu-id="cf978-190">Perform an SAP HANA Health Check through HANA\_Configuration\_Minichecks.</span></span> <span data-ttu-id="cf978-191">Cet outil signale les problèmes techniques critiques potentiels qui devraient déjà avoir déclenché une alerte dans SAP HANA Studio.</span><span class="sxs-lookup"><span data-stu-id="cf978-191">This tool returns potentially critical technical issues that should have already been raised as alerts in SAP HANA Studio.</span></span>

<span data-ttu-id="cf978-192">Reportez-vous à la [Note SAP #1969700 – collection d’instructions SQL pour SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) et téléchargez le fichier SQL Statements.zip associé à cette note.</span><span class="sxs-lookup"><span data-stu-id="cf978-192">Refer to [SAP Note #1969700 – SQL statement collection for SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) and download the SQL Statements.zip file attached to that note.</span></span> <span data-ttu-id="cf978-193">Enregistrez ce fichier .zip sur le disque dur local.</span><span class="sxs-lookup"><span data-stu-id="cf978-193">Store this .zip file on the local hard drive.</span></span>

<span data-ttu-id="cf978-194">Dans SAP HANA Studio, dans l’onglet **System Information** (Informations système), cliquez avec le bouton droit de la souris dans la colonne **Name** (Nom) et sélectionnez **Import SQL Statements** (Importer des instructions SQL).</span><span class="sxs-lookup"><span data-stu-id="cf978-194">In SAP HANA Studio, on the **System Information** tab, right-click in the **Name** column and select **Import SQL Statements**.</span></span>

![Dans SAP HANA Studio, dans l’onglet System Information (Informations système), cliquez avec le bouton droit de la souris dans la colonne Name (Nom) et sélectionnez Import SQL Statements (Importer des instructions SQL)](./media/troubleshooting-monitoring/image7-import-statements-a.png)

<span data-ttu-id="cf978-196">Sélectionnez le fichier SQL Statements.zip enregistré sur votre ordinateur pour qu’un dossier contenant les instructions SQL correspondantes soit importé.</span><span class="sxs-lookup"><span data-stu-id="cf978-196">Select the SQL Statements.zip file stored locally, and a folder with the corresponding SQL statements will be imported.</span></span> <span data-ttu-id="cf978-197">À ce stade, plusieurs vérifications de diagnostics peuvent être effectuées avec ces instructions SQL.</span><span class="sxs-lookup"><span data-stu-id="cf978-197">At this point, the many different diagnostic checks can be run with these SQL statements.</span></span>

<span data-ttu-id="cf978-198">Par exemple, pour tester les besoins en bande passante pour la réplication du système SAP HANA, cliquez avec le bouton droit de la souris sur l’instruction **Bandwidth** (Bande passante) sous **Replication: Bandwidth** (Réplication : bande passante) et sélectionnez **Open** (Ouvrir) dans la console SQL.</span><span class="sxs-lookup"><span data-stu-id="cf978-198">For example, to test SAP HANA System Replication bandwidth requirements, right-click the **Bandwidth** statement under **Replication: Bandwidth** and select **Open** in SQL Console.</span></span>

<span data-ttu-id="cf978-199">L’instruction SQL s’ouvre. Vous pouvez alors modifier puis exécuter les paramètres d’entrée (section Modification).</span><span class="sxs-lookup"><span data-stu-id="cf978-199">The complete SQL statement opens allowing input parameters (modification section) to be changed and then executed.</span></span>

![L’instruction SQL s’ouvre. Vous pouvez alors modifier puis exécuter les paramètres d’entrée (section Modification)](./media/troubleshooting-monitoring/image8-import-statements-b.png)

<span data-ttu-id="cf978-201">Autre exemple : cliquez avec le bouton droit de la souris sur les instructions sous **Replication: Overview** (Réplication : vue d’ensemble).</span><span class="sxs-lookup"><span data-stu-id="cf978-201">Another example is right-clicking on the statements under **Replication: Overview**.</span></span> <span data-ttu-id="cf978-202">Sélectionnez **Execute** (Exécuter) dans le menu contextuel :</span><span class="sxs-lookup"><span data-stu-id="cf978-202">Select **Execute** from the context menu:</span></span>

![Autre exemple : cliquez avec le bouton droit de la souris sur les instructions sous Replication: Overview (Réplication : vue d’ensemble).](./media/troubleshooting-monitoring/image9-import-statements-c.png)

<span data-ttu-id="cf978-205">Vous obtenez ainsi des informations qui vous aident à résoudre le problème :</span><span class="sxs-lookup"><span data-stu-id="cf978-205">This results in information that helps with troubleshooting:</span></span>

![Vous obtenez ainsi des informations qui vous aident à résoudre le problème](./media/troubleshooting-monitoring/image10-import-statements-d.png)

<span data-ttu-id="cf978-207">Faites de même pour HANA\_Configuration\_Minichecks et vérifiez les marques _X_ dans la colonne _C_ (Critique).</span><span class="sxs-lookup"><span data-stu-id="cf978-207">Do the same for HANA\_Configuration\_Minichecks and check for any _X_ marks in the _C_ (Critical) column.</span></span>

<span data-ttu-id="cf978-208">Exemples de sortie :</span><span class="sxs-lookup"><span data-stu-id="cf978-208">Sample outputs:</span></span>

<span data-ttu-id="cf978-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** pour les vérifications SAP HANA générales.</span><span class="sxs-lookup"><span data-stu-id="cf978-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** for general SAP HANA checks.</span></span>

![HANA\_Configuration\_MiniChecks\_Rev102.01+1 pour les vérifications SAP HANA générales](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

<span data-ttu-id="cf978-211">**HANA\_Services\_Overview** pour une vue d’ensemble des exécutions actuelles des services SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="cf978-211">**HANA\_Services\_Overview** for an overview of what SAP HANA services are currently running.</span></span>

![HANA\_Services\_Overview pour une vue d’ensemble des exécutions actuelles des services SAP HANA](./media/troubleshooting-monitoring/image12-services-overview.png)

<span data-ttu-id="cf978-213">**HANA\_Services\_Statistics** pour les informations de service SAP HANA (processeur, mémoire, etc.).</span><span class="sxs-lookup"><span data-stu-id="cf978-213">**HANA\_Services\_Statistics** for SAP HANA service information (CPU, memory, etc.).</span></span>

![<span data-ttu-id="cf978-214">HANA\_Services\_Statistics pour les informations de service SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cf978-214">HANA\_Services\_Statistics for SAP HANA service information</span></span> ](./media/troubleshooting-monitoring/image13-services-statistics.png)

<span data-ttu-id="cf978-215">**HANA\_Configuration\_Overview\_Rev110 +** pour des informations générales sur l’instance SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="cf978-215">**HANA\_Configuration\_Overview\_Rev110+** for general information on the SAP HANA instance.</span></span>

![HANA\_Configuration\_Overview\_Rev110 + pour des informations générales sur l’instance SAP HANA](./media/troubleshooting-monitoring/image14-configuration-overview.png)

<span data-ttu-id="cf978-217">**HANA\_Configuration\_Parameters\_Rev70+** pour vérifier les paramètres de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="cf978-217">**HANA\_Configuration\_Parameters\_Rev70+** to check SAP HANA parameters.</span></span>

![HANA\_Configuration\_Parameters\_Rev70+ pour vérifier les paramètres de SAP HANA](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

