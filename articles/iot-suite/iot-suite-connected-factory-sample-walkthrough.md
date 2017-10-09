---
title: "procédure pas à pas d’aaaConnected fabrique Azure IoT Suite solution | Documents Microsoft"
description: "Obtenir une description de hello Azure IoT préconfiguré solution connecté fabrique et son architecture."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 7fd55c51351659401349cfde91a20fce1045b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a><span data-ttu-id="ed8b4-103">Procédure pas à pas de la solution préconfigurée d’usine connectée</span><span class="sxs-lookup"><span data-stu-id="ed8b4-103">Connected factory preconfigured solution walkthrough</span></span>

<span data-ttu-id="ed8b4-104">Hello IoT Suite connecté fabrique [solution préconfigurée] [ lnk-preconfigured-solutions] est une implémentation d’une solution de bout en bout industrielle qui :</span><span class="sxs-lookup"><span data-stu-id="ed8b4-104">hello IoT Suite connected factory [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end industrial solution that:</span></span>

* <span data-ttu-id="ed8b4-105">Se connecte les appareils industriels tooboth simulée exécutant des serveurs OPC UA des lignes de production simulé fabrique et des appareils de serveur réels OPC UA.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-105">Connects tooboth simulated industrial devices running OPC UA servers in simulated factory production lines, and real OPC UA server devices.</span></span> <span data-ttu-id="ed8b4-106">Pour plus d’informations sur OPC UA, consultez hello [connecté fabrique FAQ](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="ed8b4-106">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="ed8b4-107">Affiche les indicateurs de performance clé (KPI) opérationnels et les OEE de ces appareils et des lignes de production.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-107">Shows operational KPIs and OEE of those devices and production lines.</span></span>
* <span data-ttu-id="ed8b4-108">Montre comment une application basée sur le cloud peut être toointeract utilisé avec les systèmes de serveur OPC UA.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-108">Demonstrates how a cloud-based application could be used toointeract with OPC UA server systems.</span></span>
* <span data-ttu-id="ed8b4-109">Permet de vous tooconnect les appareils de votre propre serveur OPC UA.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-109">Enables you tooconnect your own OPC UA server devices.</span></span>
* <span data-ttu-id="ed8b4-110">Vous permet de toobrowse et modifier hello données OPC UA du serveur.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-110">Enables you toobrowse and modify hello OPC UA server data.</span></span>
* <span data-ttu-id="ed8b4-111">S’intègre avec hello Azure temps série Insights (STI) service tooprovide des vues personnalisées de données hello à partir de vos serveurs OPC UA.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-111">Integrates with hello Azure Time Series Insights (TSI) service tooprovide customized views of hello data from your OPC UA servers.</span></span>

<span data-ttu-id="ed8b4-112">Vous pouvez utiliser la solution de hello comme point de départ pour votre propre implémentation et [personnaliser] [ lnk-customize] il toomeet vos propres besoins professionnels spécifiques.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-112">You can use hello solution as a starting point for your own implementation and [customize][lnk-customize] it toomeet your own specific business requirements.</span></span>

<span data-ttu-id="ed8b4-113">Cet article vous guide certains éléments clés hello hello connecté fabrique solution tooenable toounderstand son fonctionnement.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-113">This article walks you through some of hello key elements of hello connected factory solution tooenable you toounderstand how it works.</span></span> <span data-ttu-id="ed8b4-114">Ces connaissances vous aident à :</span><span class="sxs-lookup"><span data-stu-id="ed8b4-114">This knowledge helps you to:</span></span>

* <span data-ttu-id="ed8b4-115">Résoudre les problèmes dans les solutions hello.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-115">Troubleshoot issues in hello solution.</span></span>
* <span data-ttu-id="ed8b4-116">Planifier comment toocustomize toohello solution toomeet vos besoins spécifiques.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-116">Plan how toocustomize toohello solution toomeet your own specific requirements.</span></span>
* <span data-ttu-id="ed8b4-117">Concevoir votre propre solution IoT utilisant des services Azure.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-117">Design your own IoT solution that uses Azure services.</span></span>

<span data-ttu-id="ed8b4-118">Pour plus d’informations, consultez hello [connecté fabrique FAQ](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="ed8b4-118">For more information, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="ed8b4-119">Architecture logique</span><span class="sxs-lookup"><span data-stu-id="ed8b4-119">Logical architecture</span></span>

<span data-ttu-id="ed8b4-120">Hello suivant schéma présente des composants logiques de hello de solution de hello préconfiguré :</span><span class="sxs-lookup"><span data-stu-id="ed8b4-120">hello following diagram outlines hello logical components of hello preconfigured solution:</span></span>

![Architecture logique d’usine connectée][connected-factory-logical]

## <a name="communication-patterns"></a><span data-ttu-id="ed8b4-122">Modèles de communication</span><span class="sxs-lookup"><span data-stu-id="ed8b4-122">Communication patterns</span></span>

<span data-ttu-id="ed8b4-123">solution de Hello utilise hello [les spécification OPC UA Pub/Sub](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend OPC UA télémétrie données tooIoT Hub au format JSON.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-123">hello solution uses hello [OPC UA Pub/Sub specification](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend OPC UA telemetry data tooIoT Hub in JSON format.</span></span> <span data-ttu-id="ed8b4-124">solution de Hello utilise hello [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) module IoT Edge à cet effet.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-124">hello solution uses hello [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) IoT Edge module for this purpose.</span></span>

<span data-ttu-id="ed8b4-125">solution de Hello possède également un client OPC UA intégré dans une application web qui peut établir des connexions avec des serveurs locaux OPC UA.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-125">hello solution also has an OPC UA client integrated into a web application that can establish connections with on-premises OPC UA servers.</span></span> <span data-ttu-id="ed8b4-126">Hello client utilise un [proxy inversé](https://wikipedia.org/wiki/Reverse_proxy) et reçoit les aide à partir de la connexion de IoT Hub toomake hello sans devoir ouvrir les ports dans le pare-feu local hello.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-126">hello client uses a [reverse-proxy](https://wikipedia.org/wiki/Reverse_proxy) and receives help from IoT Hub toomake hello connection without requiring open ports in hello on-premises firewall.</span></span> <span data-ttu-id="ed8b4-127">Ce modèle de communication est appelé [communication assistée par le service](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span><span class="sxs-lookup"><span data-stu-id="ed8b4-127">This communication pattern is called [service-assisted communication](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span></span> <span data-ttu-id="ed8b4-128">solution de Hello utilise hello [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) module IoT Edge à cet effet.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-128">hello solution uses hello [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) IoT Edge module for this purpose.</span></span>


## <a name="simulation"></a><span data-ttu-id="ed8b4-129">Simulation</span><span class="sxs-lookup"><span data-stu-id="ed8b4-129">Simulation</span></span>

<span data-ttu-id="ed8b4-130">Hello simulés stations et production hello simulée systèmes (MES) constituent une ligne en usine.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-130">hello simulated stations and hello simulated manufacturing execution systems (MES) make up a factory production line.</span></span> <span data-ttu-id="ed8b4-131">Hello simulations de périphériques et hello OPC Publisher Module sont basés sur hello [OPC UA .NET Standard] [ lnk-OPC-UA-NET-Standard] publié par hello OPC Foundation.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-131">hello simulated devices and hello OPC Publisher Module are based on hello [OPC UA .NET Standard][lnk-OPC-UA-NET-Standard] published by hello OPC Foundation.</span></span>

<span data-ttu-id="ed8b4-132">Hello OPC Proxy et le serveur de publication OPC sont implémentés en tant que modules basés sur [Azure IoT bord][lnk-Azure-IoT-Gateway].</span><span class="sxs-lookup"><span data-stu-id="ed8b4-132">hello OPC Proxy and OPC Publisher are implemented as modules based on [Azure IoT Edge][lnk-Azure-IoT-Gateway].</span></span> <span data-ttu-id="ed8b4-133">Chaque ligne de production simulée dispose d’une passerelle désignée associée.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-133">Each simulated production line has a designated gateway attached.</span></span>

<span data-ttu-id="ed8b4-134">Tous les composants de simulation sont exécutés dans des conteneurs Docker hébergés dans une machine virtuelle Linux Azure.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-134">All simulation components run in Docker containers  hosted in an Azure Linux VM.</span></span> <span data-ttu-id="ed8b4-135">simulation de Hello est configuré toorun huit lignes production simulé par défaut.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-135">hello simulation is configured toorun eight simulated production lines by default.</span></span>

## <a name="simulated-production-line"></a><span data-ttu-id="ed8b4-136">Ligne de production simulée</span><span class="sxs-lookup"><span data-stu-id="ed8b4-136">Simulated production line</span></span>

<span data-ttu-id="ed8b4-137">Une ligne de production fabrique des parties.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-137">A production line manufactures parts.</span></span> <span data-ttu-id="ed8b4-138">Elle est composée de différents postes : un poste d’assembly, un poste de test et un poste de packaging.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-138">It is composed of different stations: an assembly station, a test station, and a packaging station.</span></span>

<span data-ttu-id="ed8b4-139">simulation de Hello s’exécute et met à jour les données hello qui sont exposées via des nœuds OPC UA hello.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-139">hello simulation runs and updates hello data that is exposed through hello OPC UA nodes.</span></span> <span data-ttu-id="ed8b4-140">Toutes les stations line simulé de production sont orchestrées par hello MES via OPC UA.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-140">All simulated production line stations are orchestrated by hello MES through OPC UA.</span></span>

## <a name="simulated-manufacturing-execution-system"></a><span data-ttu-id="ed8b4-141">Simulation de système d’exécution de fabrication</span><span class="sxs-lookup"><span data-stu-id="ed8b4-141">Simulated manufacturing execution system</span></span>

<span data-ttu-id="ed8b4-142">Hello MES analyse chaque station dans la ligne de production hello à travers les modifications d’état OPC UA toodetect station.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-142">hello MES monitors each station in hello production line through OPC UA toodetect station status changes.</span></span> <span data-ttu-id="ed8b4-143">Il appelle OPC UA stations de méthodes toocontrol hello et transmet ensuite un produit à partir d’une station toohello qu’elle soit terminée.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-143">It calls OPC UA methods toocontrol hello stations and passes a product from one station toohello next until it is complete.</span></span>

## <a name="gateway-opc-publisher-module"></a><span data-ttu-id="ed8b4-144">Module Éditeur d’OPC de la passerelle</span><span class="sxs-lookup"><span data-stu-id="ed8b4-144">Gateway OPC publisher module</span></span>

<span data-ttu-id="ed8b4-145">Module de serveur de publication OPC connecte toohello station OPC UA serveurs et s’abonne toohello OPC nœuds toobe publié.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-145">OPC Publisher Module connects toohello station OPC UA servers and subscribes toohello OPC nodes toobe published.</span></span> <span data-ttu-id="ed8b4-146">module de Hello convertit les données du nœud hello en format JSON, chiffre et envoie tooIoT Hub en tant que messages de OPC UA Pub/Sub.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-146">hello module converts hello node data into JSON format, encrypts it, and sends it tooIoT Hub as OPC UA Pub/Sub messages.</span></span>

<span data-ttu-id="ed8b4-147">module de serveur de publication OPC Hello nécessite un port sortant https (443) uniquement et permettre travailler avec l’infrastructure d’entreprise existante.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-147">hello OPC Publisher module only requires an outbound https port (443) and can work with existing enterprise infrastructure.</span></span>

## <a name="gateway-opc-proxy-module"></a><span data-ttu-id="ed8b4-148">Module proxy OPC de la passerelle</span><span class="sxs-lookup"><span data-stu-id="ed8b4-148">Gateway OPC proxy module</span></span>

<span data-ttu-id="ed8b4-149">Hello passerelle OPC UA Proxy Module utilise des messages de contrôle et commande OPC UA binaires et seulement nécessite un port sortant https (443).</span><span class="sxs-lookup"><span data-stu-id="ed8b4-149">hello Gateway OPC UA Proxy Module tunnels binary OPC UA command and control messages and only requires an outbound https port (443).</span></span> <span data-ttu-id="ed8b4-150">Il est compatible avec l’infrastructure d’entreprise existante, y compris les proxys Web.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-150">It can work with existing enterprise infrastructure, including Web Proxies.</span></span>

<span data-ttu-id="ed8b4-151">Il utilise un appareil de Hub IoT méthodes tootransfer en paquets TCP/IP données au niveau de la couche d’application hello et garantit ainsi la confiance de point de terminaison, le chiffrement des données et d’intégrité à l’aide de SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-151">It uses IoT Hub Device methods tootransfer packetized TCP/IP data at hello application layer and thus ensures endpoint trust, data encryption, and integrity using SSL/TLS.</span></span>

<span data-ttu-id="ed8b4-152">Hello protocole binaire de OPC UA relayée via proxy hello lui-même utilise le chiffrement et authentification de l’agent utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-152">hello OPC UA binary protocol relayed through hello proxy itself uses UA authentication and encryption.</span></span>

## <a name="azure-time-series-insights"></a><span data-ttu-id="ed8b4-153">Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="ed8b4-153">Azure Time Series Insights</span></span>

<span data-ttu-id="ed8b4-154">Hello passerelle OPC Publisher Module s’abonne modifications tooOPC UA server nœuds toodetect hello valeurs de données.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-154">hello Gateway OPC Publisher Module subscribes tooOPC UA server nodes toodetect change in hello data values.</span></span> <span data-ttu-id="ed8b4-155">Si une modification de données est détectée dans un des nœuds de hello, ce module envoie ensuite les messages tooAzure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-155">If a data change is detected in one of hello nodes, this module then sends messages tooAzure IoT Hub.</span></span>

<span data-ttu-id="ed8b4-156">IoT Hub fournit un tooAzure de source d’événement STI.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-156">IoT Hub provides an event source tooAzure TSI.</span></span> <span data-ttu-id="ed8b4-157">STI stocke les données pendant 30 jours en fonction des horodatages attaché toohello messages.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-157">TSI stores data for 30 days based on timestamps attached toohello messages.</span></span> <span data-ttu-id="ed8b4-158">Ces données incluent :</span><span class="sxs-lookup"><span data-stu-id="ed8b4-158">This data includes:</span></span>

* <span data-ttu-id="ed8b4-159">OPC UA ApplicationUri</span><span class="sxs-lookup"><span data-stu-id="ed8b4-159">OPC UA ApplicationUri</span></span>
* <span data-ttu-id="ed8b4-160">OPC UA NodeId</span><span class="sxs-lookup"><span data-stu-id="ed8b4-160">OPC UA NodeId</span></span>
* <span data-ttu-id="ed8b4-161">Valeur du nœud de hello</span><span class="sxs-lookup"><span data-stu-id="ed8b4-161">Value of hello node</span></span>
* <span data-ttu-id="ed8b4-162">Source timestamp</span><span class="sxs-lookup"><span data-stu-id="ed8b4-162">Source timestamp</span></span>
* <span data-ttu-id="ed8b4-163">OPC UA DisplayName</span><span class="sxs-lookup"><span data-stu-id="ed8b4-163">OPC UA DisplayName</span></span>

<span data-ttu-id="ed8b4-164">Actuellement, STI n’autorise pas les clients toocustomize combien ils veulent tookeep données hello.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-164">Currently, TSI does not allow customers toocustomize how long they wish tookeep hello data for.</span></span>

<span data-ttu-id="ed8b4-165">Requêtes de STI sur les données de nœud à l’aide d’un SearchSpan (Time.From, Time.To) et des agrégats par OPC UA ApplicationUri ou OPC UA NodeId ou OPC UA DisplayName.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-165">TSI queries against node data using a SearchSpan (Time.From, Time.To) and aggregates by OPC UA ApplicationUri or OPC UA NodeId or OPC UA DisplayName.</span></span>

<span data-ttu-id="ed8b4-166">tooretrieve les données de hello pour les jauges OEE et l’indicateur de performance clé hello et graphiques de série de temps hello, les données sont agrégées par nombre d’événements, Sum, Avg, Min et Max.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-166">tooretrieve hello data for hello OEE and KPI gauges, and hello time series charts, data is aggregated by count of events, Sum, Avg, Min, and Max.</span></span>

<span data-ttu-id="ed8b4-167">MTS Hello sont créées à l’aide d’un autre processus.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-167">hello time series are built using a different process.</span></span> <span data-ttu-id="ed8b4-168">OEE et indicateurs de performance clés sont calculées à partir des données de base station et propagés pour topologie hello (lignes de production, fabriques, entreprise) dans une application hello.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-168">OEE and KPIs are calculated from station base data and bubbled up for hello topology (production lines, factories, enterprise) in hello application.</span></span>

<span data-ttu-id="ed8b4-169">En outre, série chronologique pour topologie OEE et l’indicateur de performance clé est calculée dans une application hello, chaque fois qu’un intervalle de temps affiché est prêt.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-169">Additionally, time series for OEE and KPI topology is calculated in hello app, whenever a displayed timespan is ready.</span></span> <span data-ttu-id="ed8b4-170">Par exemple, affichage du jour hello est mise à jour chaque heure complète.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-170">For example, hello day view is updated every full hour.</span></span>

<span data-ttu-id="ed8b4-171">la vue de données du nœud de série au moment Hello proviennent directement de STI à l’aide d’une agrégation pour l’intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-171">hello time series view of node data comes directly from TSI using an aggregation for timespan.</span></span>

## <a name="iot-hub"></a><span data-ttu-id="ed8b4-172">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="ed8b4-172">IoT Hub</span></span>
<span data-ttu-id="ed8b4-173">Hello [IoT hub] [ lnk-IoT Hub] reçoit les données envoyées de hello OPC Publisher Module dans le cloud de hello et rend le service de Azure STI toohello disponibles.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-173">hello [IoT hub][lnk-IoT Hub] receives data sent from hello OPC Publisher Module into hello cloud and makes it available toohello Azure TSI service.</span></span> 

<span data-ttu-id="ed8b4-174">Hello IoT Hub dans les solutions hello également :</span><span class="sxs-lookup"><span data-stu-id="ed8b4-174">hello IoT Hub in hello solution also:</span></span>
- <span data-ttu-id="ed8b4-175">Gère un registre des identités qui stocke les identificateurs hello pour tout Module de serveur de publication OPC et tous les Modules de Proxy OPC.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-175">Maintains an identity registry that stores hello IDs for all OPC Publisher Module and all OPC Proxy Modules.</span></span>
- <span data-ttu-id="ed8b4-176">Est utilisé en tant que canal de transport pour la communication bidirectionnelle de hello OPC Proxy Module.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-176">Is used as transport channel for bidirectional communication of hello OPC Proxy Module.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="ed8b4-177">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="ed8b4-177">Azure Storage</span></span>
<span data-ttu-id="ed8b4-178">solution de Hello utilise le stockage d’objets blob Azure en tant que stockage de disque pour les données de déploiement de machine virtuelle et toostore hello.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-178">hello solution uses Azure blob storage as disk storage for hello VM and toostore deployment data.</span></span>

## <a name="web-app"></a><span data-ttu-id="ed8b4-179">Application web</span><span class="sxs-lookup"><span data-stu-id="ed8b4-179">Web app</span></span>
<span data-ttu-id="ed8b4-180">application Hello web déployée comme partie de hello préconfiguré solution se compose d’un client OPC UA intégré, le traitement des alertes et visualisation des données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="ed8b4-180">hello web app deployed as part of hello preconfigured solution comprises of an integrated OPC UA client, alerts processing and telemetry visualization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed8b4-181">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ed8b4-181">Next steps</span></span>

<span data-ttu-id="ed8b4-182">Vous pouvez continuer la mise en route avec IoT Suite en lisant hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="ed8b4-182">You can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="ed8b4-183">[Autorisations sur le site de azureiotsuite.com hello][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="ed8b4-183">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="ed8b4-184">Déployer une passerelle sur Windows ou Linux pour la solution de fabrique préconfiguré hello connecté</span><span class="sxs-lookup"><span data-stu-id="ed8b4-184">Deploy a gateway on Windows or Linux for hello connected factory preconfigured solution</span></span>](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
