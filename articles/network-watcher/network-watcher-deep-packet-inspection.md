---
title: "inspection d’aaaPacket avec l’Observateur de réseau Azure | Documents Microsoft"
description: "Cet article décrit la façon dont les toouse inspection approfondie des paquets de tooperform Observateur réseau collectées à partir d’une machine virtuelle"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b907d00-9c35-40f5-a61e-beb7b782276f
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4aeddcd482edc4df3d63e87b5c4b0788c540850b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="packet-inspection-with-azure-network-watcher"></a><span data-ttu-id="029aa-103">Inspection de paquets avec Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="029aa-103">Packet inspection with Azure Network Watcher</span></span>

<span data-ttu-id="029aa-104">À l’aide de la fonctionnalité de capture de paquets hello de l’Observateur réseau, vous pouvez lancer et gérer les sessions de capture sur vos machines virtuelles Azure, à partir du portail de hello, PowerShell CLI et par programme via le Kit de développement logiciel de hello et l’API REST.</span><span class="sxs-lookup"><span data-stu-id="029aa-104">Using hello packet capture feature of Network Watcher, you can initiate and manage captures sessions on your Azure VMs from hello portal, PowerShell, CLI, and programmatically through hello SDK and REST API.</span></span> <span data-ttu-id="029aa-105">Capture des paquets vous permet de tooaddress les scénarios qui requièrent des données au niveau du paquet en fournissant des informations hello dans un format facilement utilisable.</span><span class="sxs-lookup"><span data-stu-id="029aa-105">Packet capture allows you tooaddress scenarios that require packet level data by providing hello information in a readily usable format.</span></span> <span data-ttu-id="029aa-106">Tirant parti de données de salutation tooinspect d’outils, vous pouvez examiner les communications envoyées tooand à partir de vos machines virtuelles et obtenir des informations détaillées sur votre trafic réseau.</span><span class="sxs-lookup"><span data-stu-id="029aa-106">Leveraging freely available tools tooinspect hello data, you can examine communications sent tooand from your VMs and gain insights into your network traffic.</span></span> <span data-ttu-id="029aa-107">Exemples d’utilisation des données de capture de paquets : étude des problèmes de réseau ou d’application, détection des tentatives d’utilisation abusive et d’intrusion sur le réseau ou maintien de la conformité aux réglementations.</span><span class="sxs-lookup"><span data-stu-id="029aa-107">Some example uses of packet capture data include: investigating network or application issues, detecting network misuse and intrusion attempts, or maintaining regulatory compliance.</span></span> <span data-ttu-id="029aa-108">Dans cet article, nous montrons comment tooopen un fichier de capture de paquet fourni par l’Observateur réseau à l’aide d’un outil open source populaires.</span><span class="sxs-lookup"><span data-stu-id="029aa-108">In this article, we show how tooopen a packet capture file provided by Network Watcher using a popular open source tool.</span></span> <span data-ttu-id="029aa-109">Elle fournit également des exemples montrant comment identifier le trafic anormal toocalculate une latence de la connexion et examiner les statistiques de mise en réseau.</span><span class="sxs-lookup"><span data-stu-id="029aa-109">We will also provide examples showing how toocalculate a connection latency, identify abnormal traffic, and examine networking statistics.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="029aa-110">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="029aa-110">Before you begin</span></span>

<span data-ttu-id="029aa-111">Cet article aborde certains scénarios préconfigurés dans une capture de paquets exécutée précédemment.</span><span class="sxs-lookup"><span data-stu-id="029aa-111">This article goes through some pre-configured scenarios on a packet capture that was run previously.</span></span> <span data-ttu-id="029aa-112">Ces scénarios illustrent les fonctionnalités qui sont accessibles en consultant une capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="029aa-112">These scenarios illustrate capabilities that can be accessed by reviewing a packet capture.</span></span> <span data-ttu-id="029aa-113">Ce scénario utilise [WireShark](https://www.wireshark.org/) tooinspect capture des paquets hello.</span><span class="sxs-lookup"><span data-stu-id="029aa-113">This scenario uses [WireShark](https://www.wireshark.org/) tooinspect hello packet capture.</span></span>

<span data-ttu-id="029aa-114">Ce scénario part du principe que vous avez déjà exécuté une capture de paquets sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="029aa-114">This scenario assumes you already ran a packet capture on a virtual machine.</span></span> <span data-ttu-id="029aa-115">toolearn comment toocreate une capture de paquets visitez [capture des paquets de gérer avec le portail de hello](network-watcher-packet-capture-manage-portal.md) ou reste en vous rendant sur [la gestion des Captures de paquets d’API REST](network-watcher-packet-capture-manage-rest.md).</span><span class="sxs-lookup"><span data-stu-id="029aa-115">toolearn how toocreate a packet capture visit [Manage packet captures with hello portal](network-watcher-packet-capture-manage-portal.md) or with REST by visiting [Managing Packet Captures with REST API](network-watcher-packet-capture-manage-rest.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="029aa-116">Scénario</span><span class="sxs-lookup"><span data-stu-id="029aa-116">Scenario</span></span>

<span data-ttu-id="029aa-117">Dans ce scénario, vous allez :</span><span class="sxs-lookup"><span data-stu-id="029aa-117">In this scenario, you:</span></span>

* <span data-ttu-id="029aa-118">Examiner une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="029aa-118">Review a packet capture</span></span>

## <a name="calculate-network-latency"></a><span data-ttu-id="029aa-119">Calculer la latence du réseau</span><span class="sxs-lookup"><span data-stu-id="029aa-119">Calculate network latency</span></span>

<span data-ttu-id="029aa-120">Dans ce scénario, nous montrons comment tooview hello heure aller-retour initiale (RTT) d’une conversation de protocole TCP (Transmission Control) qui se produit entre deux points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="029aa-120">In this scenario, we show how tooview hello initial Round Trip Time (RTT) of a Transmission Control Protocol (TCP) conversation occurring between two endpoints.</span></span>

<span data-ttu-id="029aa-121">Lorsqu’une connexion TCP est établie, hello trois premiers paquets envoyés dans la connexion de hello suivent un modèle communément tooas hello tridirectionnel.</span><span class="sxs-lookup"><span data-stu-id="029aa-121">When a TCP connection is established, hello first three packets sent in hello connection follow a pattern commonly referred tooas hello three-way handshake.</span></span> <span data-ttu-id="029aa-122">En examinant les paquets hello deux premières envoyés dans ce protocole de transfert, une demande initiale à partir du client de hello et une réponse du serveur de hello, nous permet de calculer la latence hello lorsque cette connexion a été établie.</span><span class="sxs-lookup"><span data-stu-id="029aa-122">By examining hello first two packets sent in this handshake, an initial request from hello client and a response from hello server, we can calculate hello latency when this connection was established.</span></span> <span data-ttu-id="029aa-123">Cette latence soit référencé tooas hello temps d’aller-retour (RTT).</span><span class="sxs-lookup"><span data-stu-id="029aa-123">This latency is referred tooas hello Round Trip Time (RTT).</span></span> <span data-ttu-id="029aa-124">Pour plus d’informations sur le protocole TCP hello et tridirectionnel hello reportez-vous toohello suivant des ressources.</span><span class="sxs-lookup"><span data-stu-id="029aa-124">For more information on hello TCP protocol and hello three-way handshake refer toohello following resource.</span></span> <span data-ttu-id="029aa-125">https://support.microsoft.com/fr-fr/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span><span class="sxs-lookup"><span data-stu-id="029aa-125">https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span></span>

### <a name="step-1"></a><span data-ttu-id="029aa-126">Étape 1 :</span><span class="sxs-lookup"><span data-stu-id="029aa-126">Step 1</span></span>

<span data-ttu-id="029aa-127">Lancez WireShark.</span><span class="sxs-lookup"><span data-stu-id="029aa-127">Launch WireShark</span></span>

### <a name="step-2"></a><span data-ttu-id="029aa-128">Étape 2</span><span class="sxs-lookup"><span data-stu-id="029aa-128">Step 2</span></span>

<span data-ttu-id="029aa-129">Hello de charge **.cap** fichier à partir de la capture des paquets.</span><span class="sxs-lookup"><span data-stu-id="029aa-129">Load hello **.cap** file from your packet capture.</span></span> <span data-ttu-id="029aa-130">Ce fichier se trouve dans l’objet blob de hello il a été enregistré dans notre machine virtuelle hello localement sur, en fonction de leur configuration.</span><span class="sxs-lookup"><span data-stu-id="029aa-130">This file can be found in hello blob it was saved in our locally on hello virtual machine, depending on how you configured it.</span></span>

### <a name="step-3"></a><span data-ttu-id="029aa-131">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="029aa-131">Step 3</span></span>

<span data-ttu-id="029aa-132">tooview hello heure aller-retour initiale (RTT) dans les conversations TCP, nous sera être examine uniquement les deux premières paquets hello impliquées dans la négociation TCP hello.</span><span class="sxs-lookup"><span data-stu-id="029aa-132">tooview hello initial Round Trip Time (RTT) in TCP conversations, we will only be looking at hello first two packets involved in hello TCP handshake.</span></span> <span data-ttu-id="029aa-133">Nous allons utiliser des deux premières les paquets hello dans hello tridirectionnel, qui sont hello [SYN], [SYN, ACK] paquets.</span><span class="sxs-lookup"><span data-stu-id="029aa-133">We will be using hello first two packets in hello three-way handshake, which are hello [SYN], [SYN, ACK] packets.</span></span> <span data-ttu-id="029aa-134">Ils sont nommés pour les indicateurs définis dans l’en-tête TCP hello.</span><span class="sxs-lookup"><span data-stu-id="029aa-134">They are named for flags set in hello TCP header.</span></span> <span data-ttu-id="029aa-135">Hello dernier paquet dans la négociation hello, les paquets hello [l’accusé de réception], servira pas dans ce scénario.</span><span class="sxs-lookup"><span data-stu-id="029aa-135">hello last packet in hello handshake, hello [ACK] packet, will not be used in this scenario.</span></span> <span data-ttu-id="029aa-136">les paquets Hello [SYN] sont envoyé par le client de hello.</span><span class="sxs-lookup"><span data-stu-id="029aa-136">hello [SYN] packet is sent by hello client.</span></span> <span data-ttu-id="029aa-137">Après sa réception server de hello envoie les paquets hello [ACK] sous la forme d’un accusé de réception hello SYN à partir du client de hello.</span><span class="sxs-lookup"><span data-stu-id="029aa-137">Once it is received hello server sends hello [ACK] packet as an acknowledgement of receiving hello SYN from hello client.</span></span> <span data-ttu-id="029aa-138">Grâce à des faits hello que réponse du serveur hello nécessite très peu de surcharge, nous calculons hello RTT en soustrayant l’heure hello les paquets hello [SYN, ACK] a été reçu par le client de hello par paquet de temps [SYN] hello a été envoyé par le client de hello.</span><span class="sxs-lookup"><span data-stu-id="029aa-138">Leveraging hello fact that hello server’s response requires very little overhead, we calculate hello RTT by subtracting hello time hello [SYN, ACK] packet was received by hello client by hello time [SYN] packet was sent by hello client.</span></span>

<span data-ttu-id="029aa-139">Si vous utilisez WireShark, cette valeur est calculée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="029aa-139">Using WireShark this value is calculated for us.</span></span>

<span data-ttu-id="029aa-140">toomore afficher facilement les deux premières les paquets hello dans hello TCP tridirectionnel, nous allons utiliser hello fonctionnalité fournie par WireShark de filtrage.</span><span class="sxs-lookup"><span data-stu-id="029aa-140">toomore easily view hello first two packets in hello TCP three-way handshake, we will utilize hello filtering capability provided by WireShark.</span></span>

<span data-ttu-id="029aa-141">filtre de hello tooapply dans WireShark, développez hello Segment « Transmission Control Protocol » d’un paquet [SYN] dans la capture et examiner les indicateurs hello définies dans l’en-tête TCP hello.</span><span class="sxs-lookup"><span data-stu-id="029aa-141">tooapply hello filter in WireShark, expand hello “Transmission Control Protocol” Segment of a [SYN] packet in your capture and examine hello flags set in hello TCP header.</span></span>

<span data-ttu-id="029aa-142">Étant donné que nous recherchons toofilter sur tous les [SYN] et [SYN, ACK] cofirm de paquets, sous indicateurs que hello Syn bit a la valeur too1, puis cliquez à droite sur les bits de Syn hello -> appliquer comme filtre -> sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="029aa-142">Since we are looking toofilter on all [SYN] and [SYN, ACK] packets, under flags cofirm that hello Syn bit is set too1, then right click on hello Syn bit -> Apply as Filter -> Selected.</span></span>

![figure 7][7]

### <a name="step-4"></a><span data-ttu-id="029aa-144">Étape 4</span><span class="sxs-lookup"><span data-stu-id="029aa-144">Step 4</span></span>

<span data-ttu-id="029aa-145">Maintenant que vous avez filtré les paquets de voir hello fenêtre tooonly avec hello [SYN] bit défini, vous pouvez facilement sélectionner conversations vous intéressez tooview hello RTT initial.</span><span class="sxs-lookup"><span data-stu-id="029aa-145">Now that you have filtered hello window tooonly see packets with hello [SYN] bit set, you can easily select conversations you are interested in tooview hello initial RTT.</span></span> <span data-ttu-id="029aa-146">Un Bonjour de tooview facilement RTT dans WireShark cliquez simplement sur déroulante hello marqué l’analyse de « SEQ / l’accusé de réception ».</span><span class="sxs-lookup"><span data-stu-id="029aa-146">A simple way tooview hello RTT in WireShark simply click hello dropdown marked “SEQ/ACK” analysis.</span></span> <span data-ttu-id="029aa-147">Vous verrez ensuite hello que RTT affiché.</span><span class="sxs-lookup"><span data-stu-id="029aa-147">You will then see hello RTT displayed.</span></span> <span data-ttu-id="029aa-148">Dans ce cas, hello RTT a été 0.0022114 secondes ou 2.211 ms.</span><span class="sxs-lookup"><span data-stu-id="029aa-148">In this case, hello RTT was 0.0022114 seconds, or 2.211 ms.</span></span>

![figure 8][8]

## <a name="unwanted-protocols"></a><span data-ttu-id="029aa-150">Protocoles indésirables</span><span class="sxs-lookup"><span data-stu-id="029aa-150">Unwanted protocols</span></span>

<span data-ttu-id="029aa-151">De nombreuses applications peuvent être exécutées sur une instance de machine virtuelle que vous avez déployée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="029aa-151">You can have many applications running on a virtual machine instance you have deployed in Azure.</span></span> <span data-ttu-id="029aa-152">Plusieurs de ces applications communiquent via le réseau de hello, éventuellement sans votre autorisation explicite.</span><span class="sxs-lookup"><span data-stu-id="029aa-152">Many of these applications communicate over hello network, perhaps without your explicit permission.</span></span> <span data-ttu-id="029aa-153">À l’aide de la communication réseau de paquet capture toostore, nous pouvons étudier comment application s’adressent sur le réseau de hello et recherchez les problèmes.</span><span class="sxs-lookup"><span data-stu-id="029aa-153">Using packet capture toostore network communication, we can investigate how application are talking on hello network and look for any issues.</span></span>

<span data-ttu-id="029aa-154">Dans cet exemple, nous allons examiner une capture de paquets précédemment exécutée afin d’identifier les protocoles indésirables susceptibles d’indiquer une communication non autorisée à partir d’une application en cours d’exécution sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="029aa-154">In this example, we review a previous ran packet capture for unwanted protocols that may indicate unauthorized communication from an application running on your machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="029aa-155">Étape 1</span><span class="sxs-lookup"><span data-stu-id="029aa-155">Step 1</span></span>

<span data-ttu-id="029aa-156">À l’aide de hello même capture dans hello précédente scénario, cliquez sur **statistiques** > **hiérarchie de protocole**</span><span class="sxs-lookup"><span data-stu-id="029aa-156">Using hello same capture in hello previous scenario click **Statistics** > **Protocol Hierarchy**</span></span>

![menu Hiérarchie des protocoles][2]

<span data-ttu-id="029aa-158">fenêtre hiérarchie de protocole Hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="029aa-158">hello protocol hierarchy window appears.</span></span> <span data-ttu-id="029aa-159">Cette vue fournit une liste de tous les protocoles hello qui étaient en cours d’utilisation pendant la session de capture hello et nombre de hello de paquets transmis et reçus à l’aide de protocoles de hello.</span><span class="sxs-lookup"><span data-stu-id="029aa-159">This view provides a list of all hello protocols that were in use during hello capture session and hello number of packets transmitted and received using hello protocols.</span></span> <span data-ttu-id="029aa-160">Cette vue peut être utile pour détecter le trafic réseau indésirable sur vos machines virtuelles ou sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="029aa-160">This view can be useful for finding unwanted network traffic on your virtual machines or network.</span></span>

![hiérarchie des protocoles développée][3]

<span data-ttu-id="029aa-162">Comme vous pouvez le voir dans hello suivant capture d’écran, il a été le trafic à l’aide du protocole BitTorrent hello, qui est utilisé pour le partage de fichiers homologue toopeer.</span><span class="sxs-lookup"><span data-stu-id="029aa-162">As you can see in hello following screen capture, there was traffic using hello BitTorrent protocol, which is used for peer toopeer file sharing.</span></span> <span data-ttu-id="029aa-163">En tant qu’administrateur, vous ne prévoyez pas le trafic de BitTorrent toosee sur cet notamment les ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="029aa-163">As an administrator you do not expect toosee BitTorrent traffic on this particular virtual machines.</span></span> <span data-ttu-id="029aa-164">Maintenant vous prenant en charge de ce trafic, vous pouvez supprimer hello homologue toopeer logiciel installés sur cet ordinateur virtuel, ou hello du bloc à l’aide d’un pare-feu ou des groupes de sécurité réseau du trafic.</span><span class="sxs-lookup"><span data-stu-id="029aa-164">Now you aware of this traffic, you can remove hello peer toopeer software that installed on this virtual machine, or block hello traffic using Network Security Groups or a Firewall.</span></span> <span data-ttu-id="029aa-165">En outre, vous pouvez choisir les captures de paquets toorun selon une planification, afin que vous pouvez vérifier régulièrement utilisation du protocole hello sur vos ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="029aa-165">Additionally, you may elect toorun packet captures on a schedule, so you can review hello protocol use on your virtual machines regularly.</span></span> <span data-ttu-id="029aa-166">Pour obtenir un exemple sur des tâches de tooautomate réseau dans azure visite [surveiller les ressources réseau avec azure automation](network-watcher-monitor-with-azure-automation.md)</span><span class="sxs-lookup"><span data-stu-id="029aa-166">For an example on how tooautomate network tasks in azure visit [Monitor network resources with azure automation](network-watcher-monitor-with-azure-automation.md)</span></span>

## <a name="finding-top-destinations-and-ports"></a><span data-ttu-id="029aa-167">Identification des principaux ports et destinations</span><span class="sxs-lookup"><span data-stu-id="029aa-167">Finding top destinations and ports</span></span>

<span data-ttu-id="029aa-168">Présentation des types de trafic hello, hello des points de terminaison et ports hello communiquées via est un important lors de l’analyse ou la résolution des problèmes des applications et des ressources sur votre réseau.</span><span class="sxs-lookup"><span data-stu-id="029aa-168">Understanding hello types of traffic, hello endpoints, and hello ports communicated over is an important when monitoring or troubleshooting applications and resources on your network.</span></span> <span data-ttu-id="029aa-169">En utilisant un fichier de capture de paquet ci-dessus, nous pouvons apprendre rapidement hello premières destinations notre machine virtuelle avec lequel communique et hello ports utilisés.</span><span class="sxs-lookup"><span data-stu-id="029aa-169">Utilizing a packet capture file from above, we can quickly learn hello top destinations our VM is communicating with and hello ports being utilized.</span></span>

### <a name="step-1"></a><span data-ttu-id="029aa-170">Étape 1</span><span class="sxs-lookup"><span data-stu-id="029aa-170">Step 1</span></span>

<span data-ttu-id="029aa-171">À l’aide de hello même capture dans hello précédente scénario, cliquez sur **statistiques** > **statistiques IPv4** > **Destinations et les Ports**</span><span class="sxs-lookup"><span data-stu-id="029aa-171">Using hello same capture in hello previous scenario click **Statistics** > **IPv4 Statistics** > **Destinations and Ports**</span></span>

![fenêtre de capture de paquets][4]

### <a name="step-2"></a><span data-ttu-id="029aa-173">Étape 2</span><span class="sxs-lookup"><span data-stu-id="029aa-173">Step 2</span></span>

<span data-ttu-id="029aa-174">Comme nous Examinez les résultats de hello est une ligne, a été plusieurs connexions sur le port 111.</span><span class="sxs-lookup"><span data-stu-id="029aa-174">As we look through hello results a line stands out, there were multiple connections on port 111.</span></span> <span data-ttu-id="029aa-175">port de Hello plus utilisé a été 3389, qui est le Bureau à distance et hello restants sont des ports dynamiques RPC.</span><span class="sxs-lookup"><span data-stu-id="029aa-175">hello most used port was 3389, which is remote desktop, and hello remaining are RPC dynamic ports.</span></span>

<span data-ttu-id="029aa-176">Alors que ce trafic peut signifier nothing, il s’agit d’un port qui a été utilisé pour un grand nombre de connexions et est inconnu toohello administrateur.</span><span class="sxs-lookup"><span data-stu-id="029aa-176">While this traffic may mean nothing, it is a port that was used for many connections and is unknown toohello administrator.</span></span>

![figure 5][5]

### <a name="step-3"></a><span data-ttu-id="029aa-178">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="029aa-178">Step 3</span></span>

<span data-ttu-id="029aa-179">Maintenant que nous avons déterminé une hors du port de la place, nous pouvons filtrer notre capture basée sur le port hello.</span><span class="sxs-lookup"><span data-stu-id="029aa-179">Now that we have determined an out of place port we can filter our capture based on hello port.</span></span>

<span data-ttu-id="029aa-180">filtre Hello dans ce scénario serait :</span><span class="sxs-lookup"><span data-stu-id="029aa-180">hello filter in this scenario would be:</span></span>

```
tcp.port == 111
```

<span data-ttu-id="029aa-181">Nous permet d’entrer le texte du filtre hello ci-dessus dans la zone de texte de filtre hello et appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="029aa-181">We enter hello filter text from above in hello filter textbox and hit enter.</span></span>

![figure 6][6]

<span data-ttu-id="029aa-183">À partir des résultats de hello, nous pouvons voir tout le trafic de hello provient d’un ordinateur virtuel local sur hello même sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="029aa-183">From hello results, we can see all hello traffic is coming from a local virtual machine on hello same subnet.</span></span> <span data-ttu-id="029aa-184">Si nous ne pas toujours comprendre pourquoi ce trafic se produit, nous pouvons examiner plus toodetermine de paquets hello pourquoi il effectue ces appels sur le port 111.</span><span class="sxs-lookup"><span data-stu-id="029aa-184">If we still don’t understand why this traffic is occurring, we can further inspect hello packets toodetermine why it is making these calls on port 111.</span></span> <span data-ttu-id="029aa-185">Avec ces informations nous pouvons effectuer l’action appropriée de hello.</span><span class="sxs-lookup"><span data-stu-id="029aa-185">With this information we can take hello appropriate action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="029aa-186">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="029aa-186">Next steps</span></span>

<span data-ttu-id="029aa-187">En savoir plus sur hello autres fonctionnalités de diagnostic de l’Observateur réseau en vous rendant sur [réseau Azure la présentation des moniteurs](network-watcher-monitoring-overview.md)</span><span class="sxs-lookup"><span data-stu-id="029aa-187">Learn about hello other diagnostic features of Network Watcher by visiting [Azure network monitoring overview](network-watcher-monitoring-overview.md)</span></span>

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













