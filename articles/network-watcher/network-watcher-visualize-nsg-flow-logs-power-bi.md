---
title: "Visualiser les journaux de flux des groupes de sécurité réseau Azure avec Power BI | Microsoft Docs"
description: Cette page explique comment utiliser Power BI pour visualiser les journaux de flux NSG.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 1e4f95fa-f5f0-4e03-bc25-008fbfc4934c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d8c61ca2a3bd5affe02e8f9500655db6699a245f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a><span data-ttu-id="04dd5-103">Visualisation des journaux de flux des groupes de sécurité réseau Azure avec Power BI</span><span class="sxs-lookup"><span data-stu-id="04dd5-103">Visualizing Network Security Group flow logs with Power BI</span></span>

<span data-ttu-id="04dd5-104">Les journaux de flux des groupes de sécurité réseau (NSG) vous permettent d’afficher des informations relatives au trafic IP entrant et sortant sur les groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="04dd5-104">Network Security Group flow logs allow you to view information about ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="04dd5-105">Ces journaux de flux affichent les flux entrants et sortants en fonction de la règle, de la carte réseau à laquelle le flux s’applique, des informations à 5 tuples sur le flux (adresse IP source/de destination, port source/de destination, protocole), et de l’autorisation ou du refus du trafic.</span><span class="sxs-lookup"><span data-stu-id="04dd5-105">These flow logs show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="04dd5-106">Il peut être difficile de comprendre les données de journalisation des flux en effectuant une simple recherche manuelle dans les fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="04dd5-106">It can be difficult to gain insights into flow logging data by manually searching the log files.</span></span> <span data-ttu-id="04dd5-107">Dans cet article, nous vous proposons une solution permettant de visualiser vos flux de journaux les plus récents et d’en savoir plus sur le trafic de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="04dd5-107">In this article, we provide a solution to visualize your most recent flow logs and learn about traffic on your network.</span></span>

## <a name="scenario"></a><span data-ttu-id="04dd5-108">Scénario</span><span class="sxs-lookup"><span data-stu-id="04dd5-108">Scenario</span></span>

<span data-ttu-id="04dd5-109">Dans le scénario suivant, nous connectons Power BI Desktop au compte de stockage que nous avons configuré comme récepteur pour nos données de consignation de flux NSG.</span><span class="sxs-lookup"><span data-stu-id="04dd5-109">In the following scenario, we connect Power BI desktop to the storage account we have configured as the sink for our NSG Flow Logging data.</span></span> <span data-ttu-id="04dd5-110">Une fois connecté à notre compte de stockage, Power BI télécharge et analyse les journaux pour fournir une représentation visuelle du trafic consigné par les groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="04dd5-110">After we connect to our storage account, Power BI downloads and parses the logs to provide a visual representation of the traffic that is logged by Network Security groups.</span></span>

<span data-ttu-id="04dd5-111">Grâce aux représentations visuelles fournies dans le modèle, vous pouvez examiner les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="04dd5-111">Using the visuals supplied in the template you can examine:</span></span>

* <span data-ttu-id="04dd5-112">Principaux consommateurs</span><span class="sxs-lookup"><span data-stu-id="04dd5-112">Top Talkers</span></span>
* <span data-ttu-id="04dd5-113">Données de flux chronologiques par direction et par règle de décision</span><span class="sxs-lookup"><span data-stu-id="04dd5-113">Time Series Flow Data by direction and rule decision</span></span>
* <span data-ttu-id="04dd5-114">Flux par adresse MAC d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="04dd5-114">Flows by Network Interface MAC address</span></span>
* <span data-ttu-id="04dd5-115">Flux par groupe de sécurité réseau et par règle</span><span class="sxs-lookup"><span data-stu-id="04dd5-115">Flows by NSG and Rule</span></span>
* <span data-ttu-id="04dd5-116">Flux par port de destination</span><span class="sxs-lookup"><span data-stu-id="04dd5-116">Flows by Destination Port</span></span>

<span data-ttu-id="04dd5-117">Le modèle fourni est modifiable afin de vous permettre d’ajouter de nouvelles données ou de nouveaux graphiques, ou encore d’adapter vos requêtes à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="04dd5-117">The template provided is editable so you can modify it to add new data, visuals, or edit queries to suit your needs.</span></span>

## <a name="setup"></a><span data-ttu-id="04dd5-118">Paramétrage</span><span class="sxs-lookup"><span data-stu-id="04dd5-118">Setup</span></span>

<span data-ttu-id="04dd5-119">Avant de commencer, la journalisation des flux de groupe de sécurité réseau doit être activée sur un ou plusieurs groupes de sécurité réseau de votre compte.</span><span class="sxs-lookup"><span data-stu-id="04dd5-119">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="04dd5-120">Pour obtenir des instructions sur l’activation des journaux de flux de sécurité réseau, consultez l’article suivant [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md) (Introduction à la journalisation des flux pour les groupes de sécurité réseau).</span><span class="sxs-lookup"><span data-stu-id="04dd5-120">For instructions on enabling Network Security flow logs, refer to the following article: [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="04dd5-121">Le client Power BI Desktop doit également être installé sur votre ordinateur, lequel doit posséder suffisamment d’espace libre pour pouvoir télécharger et charger les données de journaux existant dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="04dd5-121">You must also have the Power BI Desktop client installed on your machine, and enough free space on your machine to download and load the log data that exists in your storage account.</span></span>

![Diagramme Visio][1]

### <a name="steps"></a><span data-ttu-id="04dd5-123">Étapes</span><span class="sxs-lookup"><span data-stu-id="04dd5-123">Steps</span></span>

1. <span data-ttu-id="04dd5-124">Téléchargez et ouvrez le modèle Power BI suivant dans l’application Power BI Desktop : [Modèle de journaux de flux Network Watcher PowerBI](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span><span class="sxs-lookup"><span data-stu-id="04dd5-124">Download and open the following Power BI template in the Power BI Desktop Application [Network Watcher PowerBI flow logs template](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span></span>
1. <span data-ttu-id="04dd5-125">Entrez les paramètres de requête obligatoires</span><span class="sxs-lookup"><span data-stu-id="04dd5-125">Enter the required Query parameters</span></span>
    1. <span data-ttu-id="04dd5-126">**StorageAccountName** : spécifie le nom du compte de stockage contenant les journaux de flux NSG que vous souhaitez charger et visualiser.</span><span class="sxs-lookup"><span data-stu-id="04dd5-126">**StorageAccountName** – Specifies to the name of the storage account containing the NSG flow logs that you would like to load and visualize.</span></span>
    1. <span data-ttu-id="04dd5-127">**NumberOfLogFiles** : spécifie le nombre de fichiers journaux que vous souhaitez télécharger et visualiser dans Power BI.</span><span class="sxs-lookup"><span data-stu-id="04dd5-127">**NumberOfLogFiles** – Specifies the number of log files that you would like to download and visualize in Power BI.</span></span> <span data-ttu-id="04dd5-128">Par exemple, si vous spécifiez 50, il s’agit des 50 derniers fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="04dd5-128">For example, if 50 is specified, the 50 latest log files.</span></span> <span data-ttu-id="04dd5-129">Si vous avez activé 2 groupes de sécurité réseau et que vous les avez configurés pour envoyer des journaux de flux NSG sur ce compte, vous pourrez visualiser les 25 dernières heures de journaux.</span><span class="sxs-lookup"><span data-stu-id="04dd5-129">Ff we have 2 NSGs enabled and configured to send NSG flow logs to this account, then the past 25 hours of logs can be viewed.</span></span>

    ![page d’accueil Power BI][2]

1. <span data-ttu-id="04dd5-131">Entrez la clé d'accès de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="04dd5-131">Enter the Access Key for your storage account.</span></span> <span data-ttu-id="04dd5-132">Pour trouver les clés d’accès valides, accédez à votre compte de stockage dans le portail Azure et sélectionnez **Clés d’accès** dans le menu Paramètres.</span><span class="sxs-lookup"><span data-stu-id="04dd5-132">You can find valid access keys by navigating to your storage account in the Azure portal and selecting **Access Keys** from the Settings menu.</span></span> <span data-ttu-id="04dd5-133">Cliquez sur **Connecter**, puis appliquez les modifications.</span><span class="sxs-lookup"><span data-stu-id="04dd5-133">Click **Connect** then apply changes.</span></span>

    ![clés d'accès][3]

    ![clé d’accès 2][4]

4.  <span data-ttu-id="04dd5-136">Vos journaux sont téléchargés et analysés. Vous pouvez maintenant utiliser les éléments visuels créés au préalable.</span><span class="sxs-lookup"><span data-stu-id="04dd5-136">Your logs are download and parsed and you can now utilize the pre-created visuals.</span></span>

## <a name="understanding-the-visuals"></a><span data-ttu-id="04dd5-137">Vue d’ensemble des éléments visuels</span><span class="sxs-lookup"><span data-stu-id="04dd5-137">Understanding the visuals</span></span>

<span data-ttu-id="04dd5-138">Le modèle contient un ensemble d’éléments visuels qui permettent de mieux comprendre les données des journaux de flux NSG.</span><span class="sxs-lookup"><span data-stu-id="04dd5-138">Provided in the template are a set of visuals that help make sense of the NSG Flow Log data.</span></span> <span data-ttu-id="04dd5-139">Les illustrations suivantes montrent un exemple du tableau de bord complété par des données.</span><span class="sxs-lookup"><span data-stu-id="04dd5-139">The following images show a sample of what the dashboard looks like when populated with data.</span></span> <span data-ttu-id="04dd5-140">Nous allons examiner ci-dessous en détail chaque représentation visuelle</span><span class="sxs-lookup"><span data-stu-id="04dd5-140">Below we examine each visual in greater detail</span></span> 

![powerbi][5]
 
<span data-ttu-id="04dd5-142">Le graphique Top Talkers (Principaux consommateurs) présente les adresses IP qui ont initié le plus de connexions sur la période spécifiée.</span><span class="sxs-lookup"><span data-stu-id="04dd5-142">The Top Talkers visual shows the IPs that have initiated the most connections over the period specified.</span></span> <span data-ttu-id="04dd5-143">La taille des zones correspond au nombre relatif de connexions.</span><span class="sxs-lookup"><span data-stu-id="04dd5-143">The size of the boxes corresponds to the relative number of connections.</span></span> 

![toptalkers][6]

<span data-ttu-id="04dd5-145">Les graphiques chronologiques suivants indiquent le nombre de flux sur la période.</span><span class="sxs-lookup"><span data-stu-id="04dd5-145">The following time series graphs show the number of flows over the period.</span></span> <span data-ttu-id="04dd5-146">Le graphique supérieur est segmenté en fonction de la direction du flux, et le graphique inférieur est segmenté en fonction de la décision prise (autorisation ou refus).</span><span class="sxs-lookup"><span data-stu-id="04dd5-146">The upper graph is segmented by the flow direction, and the lower is segmented by the decision made (allow or deny).</span></span> <span data-ttu-id="04dd5-147">Avec cet élément visuel, vous pouvez examiner les tendances du trafic au fil du temps et repérer les pics ou baisses d’activité anormaux au niveau du trafic ou de la segmentation du trafic.</span><span class="sxs-lookup"><span data-stu-id="04dd5-147">With this visual, you can examine your traffic trends over time, and spot any abnormal spikes or decline in traffic or traffic segmentation.</span></span>

![flowsoverperiod][7]

<span data-ttu-id="04dd5-149">Les graphiques suivants décrivent les flux par interface réseau, le graphique supérieur étant segmenté en fonction de la direction du flux et le graphique inférieur en fonction de la décision prise.</span><span class="sxs-lookup"><span data-stu-id="04dd5-149">The following graphs show the flows per Network interface, with the upper segmented by flow direction and the lower segmented by decision made.</span></span> <span data-ttu-id="04dd5-150">Avec ces informations, vous pouvez identifier parmi vos machines virtuelles celles qui ont le plus communiqué par rapport aux autres et déterminer si le trafic vers une machine virtuelle spécifique est autorisé ou refusé.</span><span class="sxs-lookup"><span data-stu-id="04dd5-150">With this information, you can gain insights into which of your VMs communicated the most relative to others, and if traffic to a specific VM is being allowed or denied.</span></span>

![flowspernic][8]

<span data-ttu-id="04dd5-152">Le graphique circulaire ci-dessous montre une répartition des flux par port de destination.</span><span class="sxs-lookup"><span data-stu-id="04dd5-152">The following donut wheel chart shows a breakdown of Flows by Destination Port.</span></span> <span data-ttu-id="04dd5-153">Avec ces informations, vous pouvez afficher les ports de destination les plus fréquemment utilisés pendant la période spécifiée.</span><span class="sxs-lookup"><span data-stu-id="04dd5-153">With this information, you can view the most commonly used destination ports used within the specified period.</span></span>

![donut][9]

<span data-ttu-id="04dd5-155">Le diagramme ci-dessous illustre le flux par groupe de sécurité réseau et par règle.</span><span class="sxs-lookup"><span data-stu-id="04dd5-155">The following bar chart shows the Flow by NSG and Rule.</span></span> <span data-ttu-id="04dd5-156">Ces informations vous permettent d’identifier les groupes de sécurité associés au trafic le plus important et de voir la répartition du trafic sur un groupe de sécurité réseau par règle.</span><span class="sxs-lookup"><span data-stu-id="04dd5-156">With this information, you can see the NSGs responsible for the most traffic, and the breakdown of traffic on an NSG by rule.</span></span>

![barchart][10]
 
<span data-ttu-id="04dd5-158">Les graphiques d’informations suivants affichent des informations sur les groupes de sécurité réseau présents dans les journaux, le nombre de flux capturés au cours de la période et la date du premier journal capturé.</span><span class="sxs-lookup"><span data-stu-id="04dd5-158">The following informational charts display information about the NSGs present in the logs, the number of Flows captured over the period, and the date of the earliest log captured.</span></span> <span data-ttu-id="04dd5-159">Ces informations vous donnent une idée des groupes de sécurité réseau consignés ainsi que de la plage de dates des flux.</span><span class="sxs-lookup"><span data-stu-id="04dd5-159">This information gives you an idea of what NSGs are being logged and the date range of flows.</span></span>

![infochart1][11]

![infochart2][12]

<span data-ttu-id="04dd5-162">Ce modèle inclut les segments suivants afin que vous puissiez afficher uniquement les données qui vous intéressent le plus.</span><span class="sxs-lookup"><span data-stu-id="04dd5-162">This template includes the following slicers to allow you to view only the data you are most interested in.</span></span> <span data-ttu-id="04dd5-163">Vous pouvez appliquer un filtre sur vos groupes de ressources, sur les groupes de sécurité réseau et sur les règles.</span><span class="sxs-lookup"><span data-stu-id="04dd5-163">You can filter on your resource groups, NSGs, and rules.</span></span> <span data-ttu-id="04dd5-164">Vous pouvez également filtrer sur les informations à 5 tuples, sur la décision et sur l’heure à laquelle des données ont été écrites dans le journal.</span><span class="sxs-lookup"><span data-stu-id="04dd5-164">You can also filter on 5-tuple information, decision, and the time the log was written.</span></span>

![slicers][13]

## <a name="conclusion"></a><span data-ttu-id="04dd5-166">Conclusion</span><span class="sxs-lookup"><span data-stu-id="04dd5-166">Conclusion</span></span>

<span data-ttu-id="04dd5-167">Dans ce scénario, nous vous avons montré comment visualiser et comprendre le trafic à l’aide des journaux de flux des groupes de sécurité réseau fournis par Network Watcher et par Power BI.</span><span class="sxs-lookup"><span data-stu-id="04dd5-167">We showed in this scenario that by using Network Security Group Flow logs provided by Network Watcher and Power BI, we are able to visualize and understand the traffic.</span></span> <span data-ttu-id="04dd5-168">À l’aide du modèle fourni, Power BI télécharge les journaux directement à partir du stockage et les traite en local.</span><span class="sxs-lookup"><span data-stu-id="04dd5-168">Using the provided template, Power BI downloads the logs directly from storage and processes them locally.</span></span> <span data-ttu-id="04dd5-169">Le temps nécessaire au chargement du modèle varie en fonction du nombre de fichiers requis et de la taille totale des fichiers téléchargés.</span><span class="sxs-lookup"><span data-stu-id="04dd5-169">Time taken to load the template varies depending on the number of files requested and total size of files downloaded.</span></span>

<span data-ttu-id="04dd5-170">N’hésitez pas à personnaliser ce modèle selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="04dd5-170">Feel free to customize this template for your needs.</span></span> <span data-ttu-id="04dd5-171">Il existe de nombreuses manières d’utiliser Power BI avec les journaux de flux des groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="04dd5-171">There are many numerous ways that you can use Power BI with Network Security Group Flow Logs.</span></span> 

## <a name="notes"></a><span data-ttu-id="04dd5-172">Remarques</span><span class="sxs-lookup"><span data-stu-id="04dd5-172">Notes</span></span>

* <span data-ttu-id="04dd5-173">Par défaut, les journaux sont stockés dans `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span><span class="sxs-lookup"><span data-stu-id="04dd5-173">Logs by default are stored in `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span></span>

    * <span data-ttu-id="04dd5-174">S’il existe d’autres données dans un autre répertoire, vous devez modifier les requêtes permettant d’extraire et traiter les données.</span><span class="sxs-lookup"><span data-stu-id="04dd5-174">If other data exists in another directory they the queries to pull and process the data must be modified.</span></span>

* <span data-ttu-id="04dd5-175">Le modèle fourni n’est pas recommandé pour des journaux d’une taille supérieure à 1 Go.</span><span class="sxs-lookup"><span data-stu-id="04dd5-175">The provided template is not recommended for use with more than 1 GB of logs.</span></span>

* <span data-ttu-id="04dd5-176">Si vous disposez d’une grande quantité de journaux, nous vous recommandons de rechercher une solution à l’aide d’un autre magasin de données tel que Data Lake ou SQL Server.</span><span class="sxs-lookup"><span data-stu-id="04dd5-176">If you have a large amount of logs, we recommend that you investigate a solution using another data store like Data Lake or SQL server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04dd5-177">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="04dd5-177">Next Steps</span></span>

<span data-ttu-id="04dd5-178">Consultez l’article [Visualize network traffic patterns to and from your VMs using open source tools](network-watcher-using-open-source-tools.md) (Visualiser les modèles de trafic réseau vers et depuis vos machines virtuelles à l’aide d’outils open source) pour apprendre à visualiser vos journaux de flux NSG avec la pile Elastick</span><span class="sxs-lookup"><span data-stu-id="04dd5-178">Learn how to visualize your NSG flow logs with the Elastick Stack by visiting [Visualize network traffic patterns to and from your VMs using open source tools](network-watcher-using-open-source-tools.md)</span></span>

[1]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure7.png
[8]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure8.png
[9]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure9.png
[10]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure10.png
[11]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure11.png
[12]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure12.png
[13]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure13.png
