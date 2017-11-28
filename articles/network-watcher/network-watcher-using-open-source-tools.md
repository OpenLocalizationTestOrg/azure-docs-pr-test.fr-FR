---
title: "Visualiser les modèles de trafic réseau à l’aide d’Azure Network Watcher et d’outils open source | Microsoft Docs"
description: "Cette page explique comment utiliser la capture de paquets Network Watcher avec Capanalysis pour visualiser les modèles de trafic depuis et vers les machines virtuelles."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 936d881b-49f9-4798-8e45-d7185ec9fe89
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: e27bb694d0cbcf1ff7c9d8ca4682a79c8b5c5cb1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-network-traffic-patterns-to-and-from-your-vms-using-open-source-tools"></a><span data-ttu-id="b10d6-103">Visualiser les modèles de trafic réseau depuis et vers les machines virtuelles à l’aide d’outils open source</span><span class="sxs-lookup"><span data-stu-id="b10d6-103">Visualize network traffic patterns to and from your VMs using open source tools</span></span>

<span data-ttu-id="b10d6-104">Les captures de paquets contiennent des données réseau qui vous permettent d’effectuer des analyses réseau et une inspection approfondie des paquets.</span><span class="sxs-lookup"><span data-stu-id="b10d6-104">Packet captures contain network data that allow you to perform network forensics and deep packet inspection.</span></span> <span data-ttu-id="b10d6-105">Il existe de nombreux outils open source que vous pouvez utiliser pour analyser des captures de paquets et obtenir des informations sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="b10d6-105">There are many opens source tools you can use to analyze packet captures to gain insights about your network.</span></span> <span data-ttu-id="b10d6-106">L’un de ces outils est CapAnalysis, un outil de visualisation de capture de paquets open source.</span><span class="sxs-lookup"><span data-stu-id="b10d6-106">One such tool is CapAnalysis, an open source packet capture visualization tool.</span></span> <span data-ttu-id="b10d6-107">La visualisation des données de capture de paquets est un moyen efficace de trouver des informations sur les modèles et anomalies au sein de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="b10d6-107">Visualizing packet capture data is a valuable way to quickly derive insights on patterns and anomalies within your network.</span></span> <span data-ttu-id="b10d6-108">Les visualisations fournissent également un moyen de partager ces informations d’une manière facilement consommable.</span><span class="sxs-lookup"><span data-stu-id="b10d6-108">Visualizations also provide a means of sharing such insights in an easily consumable manner.</span></span>

<span data-ttu-id="b10d6-109">Network Watcher d’Azure vous donne les moyens de capturer ces données précieuses en vous permettant d’effectuer des captures de paquets sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="b10d6-109">Azure’s Network Watcher provides you the ability to capture this valuable data by allowing you to perform packet captures on your network.</span></span> <span data-ttu-id="b10d6-110">Dans cet article, nous vous indiquons la procédure pour visualiser et exploiter les informations issues des captures de paquets en utilisant CapAnalysis avec Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="b10d6-110">In this article, we provide a walkthrough of how to visualize and gain insights from packet captures using CapAnalysis with Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="b10d6-111">Scénario</span><span class="sxs-lookup"><span data-stu-id="b10d6-111">Scenario</span></span>

<span data-ttu-id="b10d6-112">Vous disposez d’une application web simple déployée sur une machine virtuelle dans Azure et vous voulez utiliser les outils open source pour visualiser son trafic réseau et identifier rapidement les modèles de flux et les anomalies potentielles.</span><span class="sxs-lookup"><span data-stu-id="b10d6-112">You have a simple web application deployed on a VM in Azure want to use open source tools to visualize its network traffic to quickly identify flow patterns and any possible anomalies.</span></span> <span data-ttu-id="b10d6-113">Avec Network Watcher, vous pouvez obtenir une capture de paquets de votre environnement réseau et la stocker directement dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="b10d6-113">With Network Watcher, you can obtain a packet capture of your network environment and directly store it on your storage account.</span></span> <span data-ttu-id="b10d6-114">CapAnalysis peut ensuite ingérer la capture de paquets directement à partir de l’objet blob de stockage, puis visualiser son contenu.</span><span class="sxs-lookup"><span data-stu-id="b10d6-114">CapAnalysis can then ingest the packet capture directly from the storage blob and visualize its contents.</span></span>

![scénario][1]

## <a name="steps"></a><span data-ttu-id="b10d6-116">Étapes</span><span class="sxs-lookup"><span data-stu-id="b10d6-116">Steps</span></span>

### <a name="install-capanalysis"></a><span data-ttu-id="b10d6-117">Installation de CapAnalysis</span><span class="sxs-lookup"><span data-stu-id="b10d6-117">Install CapAnalysis</span></span>

<span data-ttu-id="b10d6-118">Pour installer CapAnalysis sur une machine virtuelle, vous pouvez consulter les instructions officielles ici https://www.capanalysis.net/ca/how-to-install-capanalysis.</span><span class="sxs-lookup"><span data-stu-id="b10d6-118">To install CapAnalysis on a virtual machine, you can refer to the official instructions here https://www.capanalysis.net/ca/how-to-install-capanalysis.</span></span>
<span data-ttu-id="b10d6-119">Pour accéder à CapAnalysis à distance, nous devons ouvrir le port 9877 sur votre machine virtuelle en ajoutant une nouvelle règle de sécurité entrante.</span><span class="sxs-lookup"><span data-stu-id="b10d6-119">In order access CapAnalysis remotely, we need to open port 9877 on your VM by adding a new inbound security rule.</span></span> <span data-ttu-id="b10d6-120">Pour plus d’informations sur la création de règles dans les groupes de sécurité réseau, reportez-vous à [Création de règles dans un NSG existant](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span><span class="sxs-lookup"><span data-stu-id="b10d6-120">For more about creating rules in Network Security Groups, refer to [Create rules in an existing NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span></span> <span data-ttu-id="b10d6-121">Une fois la règle correctement ajoutée, vous devez pouvoir accéder à CapAnalysis à partir de `http://<PublicIP>:9877`</span><span class="sxs-lookup"><span data-stu-id="b10d6-121">Once the rule has been successfully added, you should be able to access CapAnalysis from `http://<PublicIP>:9877`</span></span>

### <a name="use-azure-network-watcher-to-start-a-packet-capture-session"></a><span data-ttu-id="b10d6-122">Utilisation d’Azure Network Watcher pour démarrer une session de capture de paquets</span><span class="sxs-lookup"><span data-stu-id="b10d6-122">Use Azure Network Watcher to start a packet capture session</span></span>

<span data-ttu-id="b10d6-123">Network Watcher vous permet de capturer les paquets pour suivre le trafic entrant et sortant d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b10d6-123">Network Watcher allows you to capture packets to track traffic in and out of a virtual machine.</span></span> <span data-ttu-id="b10d6-124">Vous pouvez vous reporter aux instructions de l’article [Manage packet captures with Network Watcher](network-watcher-packet-capture-manage-portal.md) (Gérer les captures de paquets avec Network Watcher) pour démarrer une session de capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="b10d6-124">You can refer to the instructions at [Manage packet captures with Network Watcher](network-watcher-packet-capture-manage-portal.md) to start a packet capture session.</span></span> <span data-ttu-id="b10d6-125">Cette capture de paquets peut être stockée dans un objet blob de stockage accessible par CapAnalysis.</span><span class="sxs-lookup"><span data-stu-id="b10d6-125">This packet capture can be stored in a storage blob to be accessed by CapAnalysis.</span></span>

### <a name="upload-a-packet-capture-to-capanalysis"></a><span data-ttu-id="b10d6-126">Chargement d’une capture de paquets vers CapAnalysis</span><span class="sxs-lookup"><span data-stu-id="b10d6-126">Upload a packet capture to CapAnalysis</span></span>
<span data-ttu-id="b10d6-127">Vous pouvez directement charger une capture de paquets effectuée par Network Watcher à l’aide de l’onglet « Importer à partir d’une URL » en fournissant un lien vers l’objet blob de stockage contenant la capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="b10d6-127">You can directly upload a packet capture taken by network watcher using the “Import from URL” tab and providing a link to the storage blob where the packet capture is stored.</span></span>

<span data-ttu-id="b10d6-128">Lorsque vous fournissez un lien vers CapAnalysis, veillez à ajouter un jeton SAP à l’URL de l’objet blob de stockage.</span><span class="sxs-lookup"><span data-stu-id="b10d6-128">When providing a link to CapAnalysis, make sure to append a SAS token to the storage blob URL.</span></span>  <span data-ttu-id="b10d6-129">Pour ce faire, accédez à la signature d’accès partagé à partir du compte de stockage, désignez les autorisations accordées et appuyez sur le bouton Générer une signature d’accès partagé pour créer un jeton.</span><span class="sxs-lookup"><span data-stu-id="b10d6-129">To do this, navigate to Shared access signature from the storage account, designate the allowed permissions, and press the Generate SAS button to create a token.</span></span> <span data-ttu-id="b10d6-130">Vous pouvez ensuite ajouter ce jeton SAP à l’URL de l’objet blob de stockage de la capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="b10d6-130">You can then append this SAS token to the packet capture storage blob URL.</span></span>

<span data-ttu-id="b10d6-131">L’URL doit ressembler à ceci : http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span><span class="sxs-lookup"><span data-stu-id="b10d6-131">The resulting URL will look something like this: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span></span>


### <a name="analyzing-packet-captures"></a><span data-ttu-id="b10d6-132">Analyse des captures de paquets</span><span class="sxs-lookup"><span data-stu-id="b10d6-132">Analyzing packet captures</span></span>

<span data-ttu-id="b10d6-133">CapAnalysis propose différentes options pour visualiser la capture de paquets. Chacune fournit une analyse sous un angle différent.</span><span class="sxs-lookup"><span data-stu-id="b10d6-133">CapAnalysis offers various options to visualize your packet capture, each providing analysis from a different perspective.</span></span> <span data-ttu-id="b10d6-134">Ces synthèses visuelles vous permettent de comprendre les tendances du trafic réseau et d’identifier rapidement les activités inhabituelles.</span><span class="sxs-lookup"><span data-stu-id="b10d6-134">With these visual summaries, you can understand your network traffic trends and quickly spot any unusual activity.</span></span> <span data-ttu-id="b10d6-135">La liste suivante montre quelques-unes de ces fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="b10d6-135">A few of these features are shown in the following list:</span></span>

1. <span data-ttu-id="b10d6-136">Tables des flux</span><span class="sxs-lookup"><span data-stu-id="b10d6-136">Flow Tables</span></span>

    <span data-ttu-id="b10d6-137">Cette table fournit la liste des flux dans les données du paquet, l’horodatage associé aux flux et les différents protocoles associés à chaque flux, ainsi que les IP source et de destination.</span><span class="sxs-lookup"><span data-stu-id="b10d6-137">This table gives you the list of flows in the packet data, the time stamp associated with the flows and the various protocols associated with the flow, as well as source and destination IP.</span></span>

    ![page de flux capanalysis][5]

1. <span data-ttu-id="b10d6-139">Vue d’ensemble du protocole</span><span class="sxs-lookup"><span data-stu-id="b10d6-139">Protocol Overview</span></span>

    <span data-ttu-id="b10d6-140">Ce volet vous permet de visualiser rapidement la répartition du trafic réseau sur les différents protocoles et zones géographiques.</span><span class="sxs-lookup"><span data-stu-id="b10d6-140">This pane allows you to quickly see the distribution of network traffic over the various protocols and geographies.</span></span>

    ![vue d’ensemble du protocole capanalysis][6]

1. <span data-ttu-id="b10d6-142">Statistiques</span><span class="sxs-lookup"><span data-stu-id="b10d6-142">Statistics</span></span>

    <span data-ttu-id="b10d6-143">Ce volet vous permet de consulter les statistiques du trafic réseau : octets envoyés et reçus à partir des IP source et de destination, flux de chaque IP source et de destination, protocole utilisé pour les différents flux et durée des flux.</span><span class="sxs-lookup"><span data-stu-id="b10d6-143">This pane allows you to view network traffic statistics – bytes sent and received from source and destination IPs, flows for each of the source and destination IPs, protocol used for various flows, and the duration of flows.</span></span>

    ![statistiques de capanalysis][7]

1. <span data-ttu-id="b10d6-145">Carte des zones géographiques</span><span class="sxs-lookup"><span data-stu-id="b10d6-145">Geomap</span></span>

    <span data-ttu-id="b10d6-146">Ce volet vous fournit une vue cartographique de votre trafic réseau, avec des couleurs correspondant au volume de trafic de chaque pays.</span><span class="sxs-lookup"><span data-stu-id="b10d6-146">This pane provides you with a map view of your network traffic, with colors scaling to the volume of traffic from each country.</span></span> <span data-ttu-id="b10d6-147">Vous pouvez sélectionner les pays en surbrillance pour afficher des statistiques de flux supplémentaires, telles que la proportion de données envoyées et reçues à partir des IP dans ce pays.</span><span class="sxs-lookup"><span data-stu-id="b10d6-147">You can select highlighted countries to view additional flow statistics such as the proportion of data sent and received from IPs in that country.</span></span>

    ![carte des zones géographiques][8]

1. <span data-ttu-id="b10d6-149">Filtres</span><span class="sxs-lookup"><span data-stu-id="b10d6-149">Filters</span></span>

    <span data-ttu-id="b10d6-150">CapAnalysis fournit un ensemble de filtres pour l’analyse rapide de paquets spécifiques.</span><span class="sxs-lookup"><span data-stu-id="b10d6-150">CapAnalysis provides a set of filters for quick analysis of specific packets.</span></span> <span data-ttu-id="b10d6-151">Vous pouvez par exemple choisir de filtrer les données par protocole pour obtenir des informations spécifiques sur ce sous-ensemble de trafic.</span><span class="sxs-lookup"><span data-stu-id="b10d6-151">For example, you can choose to filter the data by protocol to gain specific insights on that subset of traffic.</span></span>

    ![filtres][11]

    <span data-ttu-id="b10d6-153">Visitez [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) pour en savoir plus sur l’ensemble des fonctionnalités de CapAnalysis.</span><span class="sxs-lookup"><span data-stu-id="b10d6-153">Visit [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) to learn more about all CapAnalysis' capabilities.</span></span>

## <a name="conclusion"></a><span data-ttu-id="b10d6-154">Conclusion</span><span class="sxs-lookup"><span data-stu-id="b10d6-154">Conclusion</span></span>

<span data-ttu-id="b10d6-155">La fonctionnalité de capture de paquets de Network Watcher vous permet de capturer les données nécessaires pour effectuer des analyses réseau et mieux comprendre le trafic réseau.</span><span class="sxs-lookup"><span data-stu-id="b10d6-155">Network Watcher’s packet capture feature allows you to capture the data necessary to perform network forensics and better understand your network traffic.</span></span> <span data-ttu-id="b10d6-156">Dans ce scénario, nous vous avons montré comment intégrer facilement les captures de paquets de Network Watcher avec des outils de visualisation open source.</span><span class="sxs-lookup"><span data-stu-id="b10d6-156">In this scenario, we showed how packet captures from Network Watcher can easily be integrated with open source visualization tools.</span></span> <span data-ttu-id="b10d6-157">À l’aide d’outils open source permettant de visualiser les captures de paquets comme CapAnalysis, vous pouvez effectuer une analyse approfondie des paquets et identifier rapidement les tendances de votre trafic réseau.</span><span class="sxs-lookup"><span data-stu-id="b10d6-157">By using open source tools such as CapAnalysis to visualize packets captures, you can perform deep packet inspection and quickly identify trends within your network traffic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b10d6-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b10d6-158">Next steps</span></span>

<span data-ttu-id="b10d6-159">Pour en savoir plus sur les journaux de flux NSG, consultez l’article sur les [journaux de flux NSG](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b10d6-159">To learn more about NSG flow logs, visit [NSG Flow logs](network-watcher-nsg-flow-logging-overview.md)</span></span>

<span data-ttu-id="b10d6-160">Découvrez comment visualiser vos journaux de flux de groupe de sécurité réseau avec Power BI en consultant la page [Visualizing Network Security Group flow logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md) (Visualisation des journaux de flux de groupe de sécurité réseau avec Power BI).</span><span class="sxs-lookup"><span data-stu-id="b10d6-160">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>
<!--Image references-->

[1]: ./media/network-watcher-using-open-source-tools/figure1.png
[2]: ./media/network-watcher-using-open-source-tools/figure2.png
[3]: ./media/network-watcher-using-open-source-tools/figure3.png
[4]: ./media/network-watcher-using-open-source-tools/figure4.png
[5]: ./media/network-watcher-using-open-source-tools/figure5.png
[6]: ./media/network-watcher-using-open-source-tools/figure6.png
[7]: ./media/network-watcher-using-open-source-tools/figure7.png
[8]: ./media/network-watcher-using-open-source-tools/figure8.png
[9]: ./media/network-watcher-using-open-source-tools/figure9.png
[10]: ./media/network-watcher-using-open-source-tools/figure10.png
[11]: ./media/network-watcher-using-open-source-tools/figure11.png
