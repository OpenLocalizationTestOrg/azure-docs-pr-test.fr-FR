---
title: "aaaVisualizing flux du groupe de sécurité réseau Azure se connecte à Power BI | Documents Microsoft"
description: "Cette page décrit le mode de journalisation des flux de groupe de sécurité réseau toovisualize avec Power BI."
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
ms.openlocfilehash: d9adcf256df8fed68c39be1a026ca64cc6b5c6d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a><span data-ttu-id="37fbb-103">Visualisation des journaux de flux des groupes de sécurité réseau Azure avec Power BI</span><span class="sxs-lookup"><span data-stu-id="37fbb-103">Visualizing Network Security Group flow logs with Power BI</span></span>

<span data-ttu-id="37fbb-104">Journaux de flux de groupe de sécurité réseau permettent de tooview informations du trafic IP entrant et sortant sur les groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="37fbb-104">Network Security Group flow logs allow you tooview information about ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="37fbb-105">Ces journaux flux affiche sortant et les flux entrants sur une base par la règle, hello flux hello de carte réseau s’applique, 5-tuple d’informations sur les flux de hello (Source/Destination IP, Port de la Source et de Destination, protocole), et si le trafic de hello a été autorisé ou refusé.</span><span class="sxs-lookup"><span data-stu-id="37fbb-105">These flow logs show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="37fbb-106">Il peut être difficile toogain connaître de flux de journalisation des données en recherchant manuellement les fichiers journaux de hello.</span><span class="sxs-lookup"><span data-stu-id="37fbb-106">It can be difficult toogain insights into flow logging data by manually searching hello log files.</span></span> <span data-ttu-id="37fbb-107">Dans cet article, nous fournissons un toovisualize solution votre flux plus récent consigne et en savoir plus sur le trafic sur votre réseau.</span><span class="sxs-lookup"><span data-stu-id="37fbb-107">In this article, we provide a solution toovisualize your most recent flow logs and learn about traffic on your network.</span></span>

## <a name="scenario"></a><span data-ttu-id="37fbb-108">Scénario</span><span class="sxs-lookup"><span data-stu-id="37fbb-108">Scenario</span></span>

<span data-ttu-id="37fbb-109">Bonjour scénario, nous connecter compte de stockage de bureau toohello Power BI que nous avons configurés en tant que récepteur d’hello pour notre groupe de sécurité réseau de flux de données.</span><span class="sxs-lookup"><span data-stu-id="37fbb-109">In hello following scenario, we connect Power BI desktop toohello storage account we have configured as hello sink for our NSG Flow Logging data.</span></span> <span data-ttu-id="37fbb-110">Une fois que nous avons connecté compte de stockage tooour, Power BI télécharge et analyse hello journaux tooprovide une représentation visuelle du trafic hello enregistrées par les groupes de sécurité du réseau.</span><span class="sxs-lookup"><span data-stu-id="37fbb-110">After we connect tooour storage account, Power BI downloads and parses hello logs tooprovide a visual representation of hello traffic that is logged by Network Security groups.</span></span>

<span data-ttu-id="37fbb-111">À l’aide d’éléments visuels de hello fournis dans le modèle hello que vous pouvez examiner :</span><span class="sxs-lookup"><span data-stu-id="37fbb-111">Using hello visuals supplied in hello template you can examine:</span></span>

* <span data-ttu-id="37fbb-112">Principaux consommateurs</span><span class="sxs-lookup"><span data-stu-id="37fbb-112">Top Talkers</span></span>
* <span data-ttu-id="37fbb-113">Données de flux chronologiques par direction et par règle de décision</span><span class="sxs-lookup"><span data-stu-id="37fbb-113">Time Series Flow Data by direction and rule decision</span></span>
* <span data-ttu-id="37fbb-114">Flux par adresse MAC d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="37fbb-114">Flows by Network Interface MAC address</span></span>
* <span data-ttu-id="37fbb-115">Flux par groupe de sécurité réseau et par règle</span><span class="sxs-lookup"><span data-stu-id="37fbb-115">Flows by NSG and Rule</span></span>
* <span data-ttu-id="37fbb-116">Flux par port de destination</span><span class="sxs-lookup"><span data-stu-id="37fbb-116">Flows by Destination Port</span></span>

<span data-ttu-id="37fbb-117">modèle Hello fourni est modifiable afin d’en modifier tooadd nouvelles données, des éléments visuels, ou modifier des requêtes toosuit vos besoins.</span><span class="sxs-lookup"><span data-stu-id="37fbb-117">hello template provided is editable so you can modify it tooadd new data, visuals, or edit queries toosuit your needs.</span></span>

## <a name="setup"></a><span data-ttu-id="37fbb-118">Paramétrage</span><span class="sxs-lookup"><span data-stu-id="37fbb-118">Setup</span></span>

<span data-ttu-id="37fbb-119">Avant de commencer, la journalisation des flux de groupe de sécurité réseau doit être activée sur un ou plusieurs groupes de sécurité réseau de votre compte.</span><span class="sxs-lookup"><span data-stu-id="37fbb-119">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="37fbb-120">Pour obtenir des instructions sur l’activation de la sécurité du réseau de flux de journaux, consultez l’article suivant de toohello : [journalisation tooflow de présentation pour les groupes de sécurité réseau](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="37fbb-120">For instructions on enabling Network Security flow logs, refer toohello following article: [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="37fbb-121">Vous client devez également être hello Power BI Desktop installé sur votre ordinateur et suffisamment d’espace libre sur votre ordinateur toodownload et charge hello journal des données qui existent dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="37fbb-121">You must also have hello Power BI Desktop client installed on your machine, and enough free space on your machine toodownload and load hello log data that exists in your storage account.</span></span>

![Diagramme Visio][1]

### <a name="steps"></a><span data-ttu-id="37fbb-123">Étapes</span><span class="sxs-lookup"><span data-stu-id="37fbb-123">Steps</span></span>

1. <span data-ttu-id="37fbb-124">Téléchargez et ouvrez hello suivant le modèle de Power BI Bonjour Power BI Desktop Application [Power BI de l’Observateur réseau flux enregistre le modèle](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span><span class="sxs-lookup"><span data-stu-id="37fbb-124">Download and open hello following Power BI template in hello Power BI Desktop Application [Network Watcher PowerBI flow logs template](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span></span>
1. <span data-ttu-id="37fbb-125">Entrez les paramètres de requête hello requis</span><span class="sxs-lookup"><span data-stu-id="37fbb-125">Enter hello required Query parameters</span></span>
    1. <span data-ttu-id="37fbb-126">**StorageAccountName** – Spécifie le nom de compte de stockage hello flux de groupe de sécurité réseau hello contenant les journaux que vous avez toohello serait tels que tooload et visualiser.</span><span class="sxs-lookup"><span data-stu-id="37fbb-126">**StorageAccountName** – Specifies toohello name of hello storage account containing hello NSG flow logs that you would like tooload and visualize.</span></span>
    1. <span data-ttu-id="37fbb-127">**NumberOfLogFiles** – Spécifie le nombre de hello de fichiers journaux que vous souhaitez toodownload et visualiser dans Power BI.</span><span class="sxs-lookup"><span data-stu-id="37fbb-127">**NumberOfLogFiles** – Specifies hello number of log files that you would like toodownload and visualize in Power BI.</span></span> <span data-ttu-id="37fbb-128">Par exemple, si 50 est spécifié, hello 50 fichiers journaux plus récents.</span><span class="sxs-lookup"><span data-stu-id="37fbb-128">For example, if 50 is specified, hello 50 latest log files.</span></span> <span data-ttu-id="37fbb-129">FF que nous avons 2 groupes de sécurité réseau activé et configuré de compte de toothis toosend NSG de journaux, puis hello dernières heures 25 des journaux peuvent être affichés.</span><span class="sxs-lookup"><span data-stu-id="37fbb-129">Ff we have 2 NSGs enabled and configured toosend NSG flow logs toothis account, then hello past 25 hours of logs can be viewed.</span></span>

    ![page d’accueil Power BI][2]

1. <span data-ttu-id="37fbb-131">Entrez hello clé d’accès pour votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="37fbb-131">Enter hello Access Key for your storage account.</span></span> <span data-ttu-id="37fbb-132">Vous pouvez trouver les clés d’accès valide en naviguant dans le compte de stockage tooyour Bonjour Azure portail et en sélectionnant **clés d’accès** à partir du menu Paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="37fbb-132">You can find valid access keys by navigating tooyour storage account in hello Azure portal and selecting **Access Keys** from hello Settings menu.</span></span> <span data-ttu-id="37fbb-133">Cliquez sur **Connecter**, puis appliquez les modifications.</span><span class="sxs-lookup"><span data-stu-id="37fbb-133">Click **Connect** then apply changes.</span></span>

    ![clés d'accès][3]

    ![clé d’accès 2][4]

4.  <span data-ttu-id="37fbb-136">Les journaux sont télécharger analysé et vous pouvez désormais utiliser des éléments visuels créés au préalable hello.</span><span class="sxs-lookup"><span data-stu-id="37fbb-136">Your logs are download and parsed and you can now utilize hello pre-created visuals.</span></span>

## <a name="understanding-hello-visuals"></a><span data-ttu-id="37fbb-137">Présentation des éléments visuels de hello</span><span class="sxs-lookup"><span data-stu-id="37fbb-137">Understanding hello visuals</span></span>

<span data-ttu-id="37fbb-138">Condition Bonjour modèle sont un ensemble d’éléments visuels qui aident à faciliter le décryptage hello données du journal de flux de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="37fbb-138">Provided in hello template are a set of visuals that help make sense of hello NSG Flow Log data.</span></span> <span data-ttu-id="37fbb-139">Hello images suivantes montrent un exemple de quel tableau de bord hello ressemble lorsque rempli avec les données.</span><span class="sxs-lookup"><span data-stu-id="37fbb-139">hello following images show a sample of what hello dashboard looks like when populated with data.</span></span> <span data-ttu-id="37fbb-140">Nous allons examiner ci-dessous en détail chaque représentation visuelle</span><span class="sxs-lookup"><span data-stu-id="37fbb-140">Below we examine each visual in greater detail</span></span> 

![powerbi][5]
 
<span data-ttu-id="37fbb-142">Haut Hello consommateurs montre visual hello des adresses IP que vous avez lancé hello la plupart des connexions sur hello période spécifiée.</span><span class="sxs-lookup"><span data-stu-id="37fbb-142">hello Top Talkers visual shows hello IPs that have initiated hello most connections over hello period specified.</span></span> <span data-ttu-id="37fbb-143">taille de Hello de zones de hello correspond toohello le nombre relatif de connexions.</span><span class="sxs-lookup"><span data-stu-id="37fbb-143">hello size of hello boxes corresponds toohello relative number of connections.</span></span> 

![toptalkers][6]

<span data-ttu-id="37fbb-145">Hello graphiques de série de temps suivants montrent nombre hello de flux période hello.</span><span class="sxs-lookup"><span data-stu-id="37fbb-145">hello following time series graphs show hello number of flows over hello period.</span></span> <span data-ttu-id="37fbb-146">graphique de supérieur Hello est segmentée en direction du flux hello et hello inférieur est segmentée en hello décision (autorisation ou refus).</span><span class="sxs-lookup"><span data-stu-id="37fbb-146">hello upper graph is segmented by hello flow direction, and hello lower is segmented by hello decision made (allow or deny).</span></span> <span data-ttu-id="37fbb-147">Avec cet élément visuel, vous pouvez examiner les tendances du trafic au fil du temps et repérer les pics ou baisses d’activité anormaux au niveau du trafic ou de la segmentation du trafic.</span><span class="sxs-lookup"><span data-stu-id="37fbb-147">With this visual, you can examine your traffic trends over time, and spot any abnormal spikes or decline in traffic or traffic segmentation.</span></span>

![flowsoverperiod][7]

<span data-ttu-id="37fbb-149">Hello graphiques suivants montrent les flux hello par interface réseau, avec hello supérieur segmentées par la direction du flux et hello inférieur segmentées par une décision de.</span><span class="sxs-lookup"><span data-stu-id="37fbb-149">hello following graphs show hello flows per Network interface, with hello upper segmented by flow direction and hello lower segmented by decision made.</span></span> <span data-ttu-id="37fbb-150">Avec ces informations, vous pouvez obtenir de vos machines virtuelles communiqués hello la plupart des tooothers relatif, et si le trafic tooa machine virtuelle spécifique est en cours d’autorisée ou refusée.</span><span class="sxs-lookup"><span data-stu-id="37fbb-150">With this information, you can gain insights into which of your VMs communicated hello most relative tooothers, and if traffic tooa specific VM is being allowed or denied.</span></span>

![flowspernic][8]

<span data-ttu-id="37fbb-152">Hello suivant graphique roue montre une répartition de flux par le Port de Destination.</span><span class="sxs-lookup"><span data-stu-id="37fbb-152">hello following donut wheel chart shows a breakdown of Flows by Destination Port.</span></span> <span data-ttu-id="37fbb-153">Avec ces informations, vous pouvez afficher les ports de destination de hello les plus courants utilisés dans hello spécifié période.</span><span class="sxs-lookup"><span data-stu-id="37fbb-153">With this information, you can view hello most commonly used destination ports used within hello specified period.</span></span>

![donut][9]

<span data-ttu-id="37fbb-155">Hello graphique à barres suivant montre hello flux par groupe de sécurité réseau et de la règle.</span><span class="sxs-lookup"><span data-stu-id="37fbb-155">hello following bar chart shows hello Flow by NSG and Rule.</span></span> <span data-ttu-id="37fbb-156">Avec ces informations, vous pouvez voir hello NSG responsable hello la plupart des trafic et répartition hello du trafic sur un groupe de sécurité réseau par règle.</span><span class="sxs-lookup"><span data-stu-id="37fbb-156">With this information, you can see hello NSGs responsible for hello most traffic, and hello breakdown of traffic on an NSG by rule.</span></span>

![barchart][10]
 
<span data-ttu-id="37fbb-158">Hello suivantes affichent des informations graphiques d’information sur les groupes de sécurité réseau hello présents dans les journaux de hello, hello nombre de flux capturées sur la période de hello et date hello de hello plus ancien journal est capturé.</span><span class="sxs-lookup"><span data-stu-id="37fbb-158">hello following informational charts display information about hello NSGs present in hello logs, hello number of Flows captured over hello period, and hello date of hello earliest log captured.</span></span> <span data-ttu-id="37fbb-159">Ces informations vous donnent une idée de quels groupes de sécurité réseau sont enregistrés et hello la plage de dates de flux.</span><span class="sxs-lookup"><span data-stu-id="37fbb-159">This information gives you an idea of what NSGs are being logged and hello date range of flows.</span></span>

![infochart1][11]

![infochart2][12]

<span data-ttu-id="37fbb-162">Ce modèle inclut hello suivants des segments tooallow vous tooview uniquement les données de salutation vous intéressez le plus.</span><span class="sxs-lookup"><span data-stu-id="37fbb-162">This template includes hello following slicers tooallow you tooview only hello data you are most interested in.</span></span> <span data-ttu-id="37fbb-163">Vous pouvez appliquer un filtre sur vos groupes de ressources, sur les groupes de sécurité réseau et sur les règles.</span><span class="sxs-lookup"><span data-stu-id="37fbb-163">You can filter on your resource groups, NSGs, and rules.</span></span> <span data-ttu-id="37fbb-164">Vous pouvez également filtrer sur les informations de 5 tuples, la décision et temps de hello journal de hello a été écrit.</span><span class="sxs-lookup"><span data-stu-id="37fbb-164">You can also filter on 5-tuple information, decision, and hello time hello log was written.</span></span>

![slicers][13]

## <a name="conclusion"></a><span data-ttu-id="37fbb-166">Conclusion</span><span class="sxs-lookup"><span data-stu-id="37fbb-166">Conclusion</span></span>

<span data-ttu-id="37fbb-167">Nous vous avons montré dans ce scénario qu’en utilisant les journaux de flux de groupe de sécurité réseau fournis par l’Observateur réseau et Power BI, nous sont en mesure de toovisualize et comprendre le trafic de hello.</span><span class="sxs-lookup"><span data-stu-id="37fbb-167">We showed in this scenario that by using Network Security Group Flow logs provided by Network Watcher and Power BI, we are able toovisualize and understand hello traffic.</span></span> <span data-ttu-id="37fbb-168">À l’aide du modèle de hello fourni, Power BI télécharge les journaux de hello directement à partir du stockage et les traite localement.</span><span class="sxs-lookup"><span data-stu-id="37fbb-168">Using hello provided template, Power BI downloads hello logs directly from storage and processes them locally.</span></span> <span data-ttu-id="37fbb-169">Modèle de hello tooload durée varie selon le nombre hello de fichiers requis et la taille totale des fichiers téléchargés.</span><span class="sxs-lookup"><span data-stu-id="37fbb-169">Time taken tooload hello template varies depending on hello number of files requested and total size of files downloaded.</span></span>

<span data-ttu-id="37fbb-170">Vous pouvez toocustomize libre ce modèle pour vos besoins.</span><span class="sxs-lookup"><span data-stu-id="37fbb-170">Feel free toocustomize this template for your needs.</span></span> <span data-ttu-id="37fbb-171">Il existe de nombreuses manières d’utiliser Power BI avec les journaux de flux des groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="37fbb-171">There are many numerous ways that you can use Power BI with Network Security Group Flow Logs.</span></span> 

## <a name="notes"></a><span data-ttu-id="37fbb-172">Remarques</span><span class="sxs-lookup"><span data-stu-id="37fbb-172">Notes</span></span>

* <span data-ttu-id="37fbb-173">Par défaut, les journaux sont stockés dans `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span><span class="sxs-lookup"><span data-stu-id="37fbb-173">Logs by default are stored in `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span></span>

    * <span data-ttu-id="37fbb-174">Si d’autres données existent dans un autre répertoire ils hello toopull de requêtes et traiter les données hello doivent être modifiées.</span><span class="sxs-lookup"><span data-stu-id="37fbb-174">If other data exists in another directory they hello queries toopull and process hello data must be modified.</span></span>

* <span data-ttu-id="37fbb-175">modèle de Hello fourni n’est pas recommandée pour une utilisation avec plus de 1 Go de journaux.</span><span class="sxs-lookup"><span data-stu-id="37fbb-175">hello provided template is not recommended for use with more than 1 GB of logs.</span></span>

* <span data-ttu-id="37fbb-176">Si vous disposez d’une grande quantité de journaux, nous vous recommandons de rechercher une solution à l’aide d’un autre magasin de données tel que Data Lake ou SQL Server.</span><span class="sxs-lookup"><span data-stu-id="37fbb-176">If you have a large amount of logs, we recommend that you investigate a solution using another data store like Data Lake or SQL server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37fbb-177">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="37fbb-177">Next Steps</span></span>

<span data-ttu-id="37fbb-178">Découvrez comment toovisualize votre flux de groupe de sécurité réseau consigne avec hello Elastick pile en vous rendant sur [visualiser tooand de modèles de trafic réseau à partir de vos machines virtuelles à l’aide d’outils open source](network-watcher-using-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="37fbb-178">Learn how toovisualize your NSG flow logs with hello Elastick Stack by visiting [Visualize network traffic patterns tooand from your VMs using open source tools](network-watcher-using-open-source-tools.md)</span></span>

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
