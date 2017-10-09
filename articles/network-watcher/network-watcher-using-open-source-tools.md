---
title: "modèles de trafic réseau aaaVisualize avec l’Observateur de réseau Azure et d’outils open source | Documents Microsoft"
description: "Cette page décrit comment la capture de paquet de l’Observateur réseau toouse avec tooand de modèles Capanalysis toovisualize le trafic à partir de vos machines virtuelles."
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
ms.openlocfilehash: fca9a226729162cd90d412c7b699ac54d2257a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-network-traffic-patterns-tooand-from-your-vms-using-open-source-tools"></a><span data-ttu-id="beadd-103">Visualiser tooand de modèles de trafic réseau à partir de vos machines virtuelles à l’aide d’outils open source</span><span class="sxs-lookup"><span data-stu-id="beadd-103">Visualize network traffic patterns tooand from your VMs using open source tools</span></span>

<span data-ttu-id="beadd-104">Les captures de paquets contiennent des données de réseau qui permettent une analyse de réseau tooperform, l’inspection approfondie des paquets.</span><span class="sxs-lookup"><span data-stu-id="beadd-104">Packet captures contain network data that allow you tooperform network forensics and deep packet inspection.</span></span> <span data-ttu-id="beadd-105">Il existe s’affiche de nombreux outils source vous pouvez utiliser tooanalyze paquet captures toogain insights sur votre réseau.</span><span class="sxs-lookup"><span data-stu-id="beadd-105">There are many opens source tools you can use tooanalyze packet captures toogain insights about your network.</span></span> <span data-ttu-id="beadd-106">L’un de ces outils est CapAnalysis, un outil de visualisation de capture de paquets open source.</span><span class="sxs-lookup"><span data-stu-id="beadd-106">One such tool is CapAnalysis, an open source packet capture visualization tool.</span></span> <span data-ttu-id="beadd-107">Visualisation des données de capture de paquet est un moyen très utile tooquickly tirer des leçons sur les modèles et les anomalies dans votre réseau.</span><span class="sxs-lookup"><span data-stu-id="beadd-107">Visualizing packet capture data is a valuable way tooquickly derive insights on patterns and anomalies within your network.</span></span> <span data-ttu-id="beadd-108">Les visualisations fournissent également un moyen de partager ces informations d’une manière facilement consommable.</span><span class="sxs-lookup"><span data-stu-id="beadd-108">Visualizations also provide a means of sharing such insights in an easily consumable manner.</span></span>

<span data-ttu-id="beadd-109">Observateur de réseau de Azure fournit que vous hello toocapture possibilité capture de ces données précieuses en vous tooperform paquet sur votre réseau.</span><span class="sxs-lookup"><span data-stu-id="beadd-109">Azure’s Network Watcher provides you hello ability toocapture this valuable data by allowing you tooperform packet captures on your network.</span></span> <span data-ttu-id="beadd-110">Dans cet article, nous fournissons une procédure pas à pas comment insights toovisualize et d’accéder à partir du paquet capture à l’aide de CapAnalysis avec l’Observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="beadd-110">In this article, we provide a walkthrough of how toovisualize and gain insights from packet captures using CapAnalysis with Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="beadd-111">Scénario</span><span class="sxs-lookup"><span data-stu-id="beadd-111">Scenario</span></span>

<span data-ttu-id="beadd-112">Vous avez une application web simple déployée sur une machine virtuelle dans Azure que vous souhaitez toouse open source outils toovisualize son tooquickly de trafic réseau identifier toute anomalie possibles et les modèles de flux.</span><span class="sxs-lookup"><span data-stu-id="beadd-112">You have a simple web application deployed on a VM in Azure want toouse open source tools toovisualize its network traffic tooquickly identify flow patterns and any possible anomalies.</span></span> <span data-ttu-id="beadd-113">Avec Network Watcher, vous pouvez obtenir une capture de paquets de votre environnement réseau et la stocker directement dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="beadd-113">With Network Watcher, you can obtain a packet capture of your network environment and directly store it on your storage account.</span></span> <span data-ttu-id="beadd-114">CapAnalysis ensuite réception hello capture des paquets directement à partir de l’objet blob de stockage hello et visualiser son contenu.</span><span class="sxs-lookup"><span data-stu-id="beadd-114">CapAnalysis can then ingest hello packet capture directly from hello storage blob and visualize its contents.</span></span>

![scénario][1]

## <a name="steps"></a><span data-ttu-id="beadd-116">Étapes</span><span class="sxs-lookup"><span data-stu-id="beadd-116">Steps</span></span>

### <a name="install-capanalysis"></a><span data-ttu-id="beadd-117">Installation de CapAnalysis</span><span class="sxs-lookup"><span data-stu-id="beadd-117">Install CapAnalysis</span></span>

<span data-ttu-id="beadd-118">tooinstall CapAnalysis sur un ordinateur virtuel, vous pouvez faire référence les instructions officiel toohello https://www.capanalysis.net/ca/how-to-install-capanalysis ici.</span><span class="sxs-lookup"><span data-stu-id="beadd-118">tooinstall CapAnalysis on a virtual machine, you can refer toohello official instructions here https://www.capanalysis.net/ca/how-to-install-capanalysis.</span></span>
<span data-ttu-id="beadd-119">Accès CapAnalysis à distance, nous devons tooopen port 9877 sur votre machine virtuelle en ajoutant une nouvelle règle de sécurité de trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="beadd-119">In order access CapAnalysis remotely, we need tooopen port 9877 on your VM by adding a new inbound security rule.</span></span> <span data-ttu-id="beadd-120">Pour plus d’informations sur la création de règles dans les groupes de sécurité réseau, consultez trop[créer des règles dans un groupe de sécurité réseau existant](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span><span class="sxs-lookup"><span data-stu-id="beadd-120">For more about creating rules in Network Security Groups, refer too[Create rules in an existing NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span></span> <span data-ttu-id="beadd-121">Une fois que la règle de hello a été ajouté avec succès, vous devez être en mesure de tooaccess CapAnalysis à partir de`http://<PublicIP>:9877`</span><span class="sxs-lookup"><span data-stu-id="beadd-121">Once hello rule has been successfully added, you should be able tooaccess CapAnalysis from `http://<PublicIP>:9877`</span></span>

### <a name="use-azure-network-watcher-toostart-a-packet-capture-session"></a><span data-ttu-id="beadd-122">Utilisez toostart l’Observateur réseau Azure un paquet de capture de session</span><span class="sxs-lookup"><span data-stu-id="beadd-122">Use Azure Network Watcher toostart a packet capture session</span></span>

<span data-ttu-id="beadd-123">Observateur réseau vous permet de trafic de tootrack toocapture paquets vers et depuis un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="beadd-123">Network Watcher allows you toocapture packets tootrack traffic in and out of a virtual machine.</span></span> <span data-ttu-id="beadd-124">Vous pouvez faire référence à des instructions de toohello à [captures de paquets de gérer d’observateur réseau](network-watcher-packet-capture-manage-portal.md) toostart une session de capture de paquet.</span><span class="sxs-lookup"><span data-stu-id="beadd-124">You can refer toohello instructions at [Manage packet captures with Network Watcher](network-watcher-packet-capture-manage-portal.md) toostart a packet capture session.</span></span> <span data-ttu-id="beadd-125">Cette capture des paquets peut être stockée dans un toobe d’objet blob de stockage accédé par CapAnalysis.</span><span class="sxs-lookup"><span data-stu-id="beadd-125">This packet capture can be stored in a storage blob toobe accessed by CapAnalysis.</span></span>

### <a name="upload-a-packet-capture-toocapanalysis"></a><span data-ttu-id="beadd-126">Télécharger un tooCapAnalysis de capture de paquet</span><span class="sxs-lookup"><span data-stu-id="beadd-126">Upload a packet capture tooCapAnalysis</span></span>
<span data-ttu-id="beadd-127">Vous pouvez télécharger directement d’une capture de paquets prise par l’Observateur réseau à l’aide d’onglet de « Importation à partir de l’URL » hello et en fournissant un objet blob de lien toohello stockage où la capture des paquets hello est stockée.</span><span class="sxs-lookup"><span data-stu-id="beadd-127">You can directly upload a packet capture taken by network watcher using hello “Import from URL” tab and providing a link toohello storage blob where hello packet capture is stored.</span></span>

<span data-ttu-id="beadd-128">Lorsque vous fournissez un lien de tooCapAnalysis, assurez-vous que tooappend une URL de blob de stockage toohello jeton SAS.</span><span class="sxs-lookup"><span data-stu-id="beadd-128">When providing a link tooCapAnalysis, make sure tooappend a SAS token toohello storage blob URL.</span></span>  <span data-ttu-id="beadd-129">toodo, accédez tooShared signature d’accès de compte de stockage hello, désignez hello les autorisations accordée, appuyez sur toocreate de bouton hello SAS de générer un jeton.</span><span class="sxs-lookup"><span data-stu-id="beadd-129">toodo this, navigate tooShared access signature from hello storage account, designate hello allowed permissions, and press hello Generate SAS button toocreate a token.</span></span> <span data-ttu-id="beadd-130">Vous pouvez ensuite ajouter cette URL de blob de stockage SAS toohello jeton paquet capture.</span><span class="sxs-lookup"><span data-stu-id="beadd-130">You can then append this SAS token toohello packet capture storage blob URL.</span></span>

<span data-ttu-id="beadd-131">Hello URL résultante ressemble à ceci : http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span><span class="sxs-lookup"><span data-stu-id="beadd-131">hello resulting URL will look something like this: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span></span>


### <a name="analyzing-packet-captures"></a><span data-ttu-id="beadd-132">Analyse des captures de paquets</span><span class="sxs-lookup"><span data-stu-id="beadd-132">Analyzing packet captures</span></span>

<span data-ttu-id="beadd-133">CapAnalysis offre différentes options toovisualize la capture des paquets, chaque ainsi que l’analyse à partir d’une perspective différente.</span><span class="sxs-lookup"><span data-stu-id="beadd-133">CapAnalysis offers various options toovisualize your packet capture, each providing analysis from a different perspective.</span></span> <span data-ttu-id="beadd-134">Ces synthèses visuelles vous permettent de comprendre les tendances du trafic réseau et d’identifier rapidement les activités inhabituelles.</span><span class="sxs-lookup"><span data-stu-id="beadd-134">With these visual summaries, you can understand your network traffic trends and quickly spot any unusual activity.</span></span> <span data-ttu-id="beadd-135">Certaines de ces fonctionnalités sont répertoriées dans hello suivant liste :</span><span class="sxs-lookup"><span data-stu-id="beadd-135">A few of these features are shown in hello following list:</span></span>

1. <span data-ttu-id="beadd-136">Tables des flux</span><span class="sxs-lookup"><span data-stu-id="beadd-136">Flow Tables</span></span>

    <span data-ttu-id="beadd-137">Ce tableau vous propose vous hello liste de flux de données de paquets hello, hello horodatage associé au flux de hello et hello différents protocoles associés aux flux de hello, ainsi que les IP source et de destination.</span><span class="sxs-lookup"><span data-stu-id="beadd-137">This table gives you hello list of flows in hello packet data, hello time stamp associated with hello flows and hello various protocols associated with hello flow, as well as source and destination IP.</span></span>

    ![page de flux capanalysis][5]

1. <span data-ttu-id="beadd-139">Vue d’ensemble du protocole</span><span class="sxs-lookup"><span data-stu-id="beadd-139">Protocol Overview</span></span>

    <span data-ttu-id="beadd-140">Ce volet vous permet de tooquickly consultez distribution hello du trafic réseau via hello différents protocoles et des zones géographiques différentes.</span><span class="sxs-lookup"><span data-stu-id="beadd-140">This pane allows you tooquickly see hello distribution of network traffic over hello various protocols and geographies.</span></span>

    ![vue d’ensemble du protocole capanalysis][6]

1. <span data-ttu-id="beadd-142">Statistiques</span><span class="sxs-lookup"><span data-stu-id="beadd-142">Statistics</span></span>

    <span data-ttu-id="beadd-143">Ce volet permet de vous tooview statistiques de trafic réseau-octets envoyés et reçus à partir de la source et les adresses IP, les flux pour chaque source de hello et de destination, des adresses IP de destination de protocole utilisé pour différents flux et la durée de hello de flux.</span><span class="sxs-lookup"><span data-stu-id="beadd-143">This pane allows you tooview network traffic statistics – bytes sent and received from source and destination IPs, flows for each of hello source and destination IPs, protocol used for various flows, and hello duration of flows.</span></span>

    ![statistiques de capanalysis][7]

1. <span data-ttu-id="beadd-145">Carte des zones géographiques</span><span class="sxs-lookup"><span data-stu-id="beadd-145">Geomap</span></span>

    <span data-ttu-id="beadd-146">Ce volet vous offre une vue de mappage de votre trafic réseau, volume toohello du trafic de chaque pays de mise à l’échelle de couleurs.</span><span class="sxs-lookup"><span data-stu-id="beadd-146">This pane provides you with a map view of your network traffic, with colors scaling toohello volume of traffic from each country.</span></span> <span data-ttu-id="beadd-147">Vous pouvez sélectionner le pays en surbrillance tooview flux supplémentaires des statistiques telles que proportion hello de données envoyés et reçus à partir d’adresses IP dans ce pays.</span><span class="sxs-lookup"><span data-stu-id="beadd-147">You can select highlighted countries tooview additional flow statistics such as hello proportion of data sent and received from IPs in that country.</span></span>

    ![carte des zones géographiques][8]

1. <span data-ttu-id="beadd-149">Filtres</span><span class="sxs-lookup"><span data-stu-id="beadd-149">Filters</span></span>

    <span data-ttu-id="beadd-150">CapAnalysis fournit un ensemble de filtres pour l’analyse rapide de paquets spécifiques.</span><span class="sxs-lookup"><span data-stu-id="beadd-150">CapAnalysis provides a set of filters for quick analysis of specific packets.</span></span> <span data-ttu-id="beadd-151">Par exemple, vous pouvez choisir les données de salutation toofilter par protocole toogain spécifiques des informations sur ce sous-ensemble de trafic.</span><span class="sxs-lookup"><span data-stu-id="beadd-151">For example, you can choose toofilter hello data by protocol toogain specific insights on that subset of traffic.</span></span>

    ![filtres][11]

    <span data-ttu-id="beadd-153">Visitez [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn plus d’informations sur les fonctionnalités des tous les CapAnalysis.</span><span class="sxs-lookup"><span data-stu-id="beadd-153">Visit [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn more about all CapAnalysis' capabilities.</span></span>

## <a name="conclusion"></a><span data-ttu-id="beadd-154">Conclusion</span><span class="sxs-lookup"><span data-stu-id="beadd-154">Conclusion</span></span>

<span data-ttu-id="beadd-155">Fonctionnalité de capture de paquet de l’Observateur réseau vous permet de post-mortem de données nécessaires tooperform réseau toocapture hello et mieux comprendre votre trafic réseau.</span><span class="sxs-lookup"><span data-stu-id="beadd-155">Network Watcher’s packet capture feature allows you toocapture hello data necessary tooperform network forensics and better understand your network traffic.</span></span> <span data-ttu-id="beadd-156">Dans ce scénario, nous vous avons montré comment intégrer facilement les captures de paquets de Network Watcher avec des outils de visualisation open source.</span><span class="sxs-lookup"><span data-stu-id="beadd-156">In this scenario, we showed how packet captures from Network Watcher can easily be integrated with open source visualization tools.</span></span> <span data-ttu-id="beadd-157">À l’aide des outils open source tels que les paquets toovisualize CapAnalysis capture, vous pouvez effectuer une inspection approfondie des paquets et identifier rapidement les tendances au sein de votre trafic réseau.</span><span class="sxs-lookup"><span data-stu-id="beadd-157">By using open source tools such as CapAnalysis toovisualize packets captures, you can perform deep packet inspection and quickly identify trends within your network traffic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="beadd-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="beadd-158">Next steps</span></span>

<span data-ttu-id="beadd-159">toolearn en savoir plus sur les journaux de flux de groupe de sécurité réseau, visitez [consigne des flux de groupe de sécurité réseau](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="beadd-159">toolearn more about NSG flow logs, visit [NSG Flow logs](network-watcher-nsg-flow-logging-overview.md)</span></span>

<span data-ttu-id="beadd-160">Découvrez comment toovisualize votre flux de groupe de sécurité réseau se connecte à Power BI en vous rendant sur [NSG de visualiser les flux de journaux avec Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="beadd-160">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>
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
