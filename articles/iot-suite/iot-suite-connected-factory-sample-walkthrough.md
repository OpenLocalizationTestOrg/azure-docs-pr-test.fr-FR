---
title: "Procédure pas à pas pour la solution d’usine connectée Azure IoT Suite | Microsoft Docs"
description: "Description de la solution préconfigurée d’usine connectée Azure IoT et de son architecture."
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
ms.openlocfilehash: 517e908a744734139ed0aeee314a4f3b9eda86cc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a><span data-ttu-id="0de53-103">Procédure pas à pas de la solution préconfigurée d’usine connectée</span><span class="sxs-lookup"><span data-stu-id="0de53-103">Connected factory preconfigured solution walkthrough</span></span>

<span data-ttu-id="0de53-104">La [solution préconfigurée][lnk-preconfigured-solutions] d’usine connectée IoT Suite est une implémentation d’une solution industrielle de bout en bout qui :</span><span class="sxs-lookup"><span data-stu-id="0de53-104">The IoT Suite connected factory [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end industrial solution that:</span></span>

* <span data-ttu-id="0de53-105">Se connecte à la fois aux appareils industriels simulés fonctionnant sur des serveurs OPC UA dans des lignes de production simulées et aux appareils fonctionnant sur des serveurs OPC UA réels.</span><span class="sxs-lookup"><span data-stu-id="0de53-105">Connects to both simulated industrial devices running OPC UA servers in simulated factory production lines, and real OPC UA server devices.</span></span> <span data-ttu-id="0de53-106">Pour plus d’informations sur OPC UA, consultez les [questions fréquentes (FAQ) sur l’usine connectée](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="0de53-106">For more information about OPC UA, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="0de53-107">Affiche les indicateurs de performance clé (KPI) opérationnels et les OEE de ces appareils et des lignes de production.</span><span class="sxs-lookup"><span data-stu-id="0de53-107">Shows operational KPIs and OEE of those devices and production lines.</span></span>
* <span data-ttu-id="0de53-108">Montre comment une application basée sur le cloud peut être utilisée pour interagir avec les systèmes de serveur OPC UA.</span><span class="sxs-lookup"><span data-stu-id="0de53-108">Demonstrates how a cloud-based application could be used to interact with OPC UA server systems.</span></span>
* <span data-ttu-id="0de53-109">Vous permet de connecter vos propres appareils de serveur OPC UA.</span><span class="sxs-lookup"><span data-stu-id="0de53-109">Enables you to connect your own OPC UA server devices.</span></span>
* <span data-ttu-id="0de53-110">Vous permet de parcourir et de modifier les données de serveur OPC UA.</span><span class="sxs-lookup"><span data-stu-id="0de53-110">Enables you to browse and modify the OPC UA server data.</span></span>
* <span data-ttu-id="0de53-111">S’intègre avec le service Azure Time Series Insights (TSI) pour fournir des vues personnalisées des données à partir de vos serveurs OPC UA.</span><span class="sxs-lookup"><span data-stu-id="0de53-111">Integrates with the Azure Time Series Insights (TSI) service to provide customized views of the data from your OPC UA servers.</span></span>

<span data-ttu-id="0de53-112">Vous pouvez utiliser la solution comme point de départ pour votre propre implémentation et la [personnaliser][lnk-customize] pour répondre à vos propres exigences professionnelles.</span><span class="sxs-lookup"><span data-stu-id="0de53-112">You can use the solution as a starting point for your own implementation and [customize][lnk-customize] it to meet your own specific business requirements.</span></span>

<span data-ttu-id="0de53-113">Cet article vous familiarise avec les éléments clés de la solution d’usine connectée pour vous permettre de comprendre son fonctionnement.</span><span class="sxs-lookup"><span data-stu-id="0de53-113">This article walks you through some of the key elements of the connected factory solution to enable you to understand how it works.</span></span> <span data-ttu-id="0de53-114">Ces connaissances vous aident à :</span><span class="sxs-lookup"><span data-stu-id="0de53-114">This knowledge helps you to:</span></span>

* <span data-ttu-id="0de53-115">Résoudre les problèmes dans la solution.</span><span class="sxs-lookup"><span data-stu-id="0de53-115">Troubleshoot issues in the solution.</span></span>
* <span data-ttu-id="0de53-116">Adapter la solution à vos besoins professionnels.</span><span class="sxs-lookup"><span data-stu-id="0de53-116">Plan how to customize to the solution to meet your own specific requirements.</span></span>
* <span data-ttu-id="0de53-117">Concevoir votre propre solution IoT utilisant des services Azure.</span><span class="sxs-lookup"><span data-stu-id="0de53-117">Design your own IoT solution that uses Azure services.</span></span>

<span data-ttu-id="0de53-118">Pour plus d’informations, consultez le [FAQ sur l’usine connectée](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="0de53-118">For more information, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="0de53-119">Architecture logique</span><span class="sxs-lookup"><span data-stu-id="0de53-119">Logical architecture</span></span>

<span data-ttu-id="0de53-120">Le schéma suivant décrit les composants logiques de la solution préconfigurée :</span><span class="sxs-lookup"><span data-stu-id="0de53-120">The following diagram outlines the logical components of the preconfigured solution:</span></span>

![Architecture logique d’usine connectée][connected-factory-logical]

## <a name="communication-patterns"></a><span data-ttu-id="0de53-122">Modèles de communication</span><span class="sxs-lookup"><span data-stu-id="0de53-122">Communication patterns</span></span>

<span data-ttu-id="0de53-123">La solution utilise la [spécification Pub/Sub OPC UA](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) pour envoyer des données de télémétrie OPC UA à IoT Hub au format JSON.</span><span class="sxs-lookup"><span data-stu-id="0de53-123">The solution uses the [OPC UA Pub/Sub specification](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) to send OPC UA telemetry data to IoT Hub in JSON format.</span></span> <span data-ttu-id="0de53-124">Pour ce faire, la solution utilise le module IoT Edge de [l’éditeur d’OPC](https://github.com/Azure/iot-edge-opc-publisher).</span><span class="sxs-lookup"><span data-stu-id="0de53-124">The solution uses the [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) IoT Edge module for this purpose.</span></span>

<span data-ttu-id="0de53-125">La solution dispose également d’un client OPC UA intégré à une application web qui peut établir des connexions avec des serveurs locaux OPC UA.</span><span class="sxs-lookup"><span data-stu-id="0de53-125">The solution also has an OPC UA client integrated into a web application that can establish connections with on-premises OPC UA servers.</span></span> <span data-ttu-id="0de53-126">Le client utilise un [proxy inversé](https://wikipedia.org/wiki/Reverse_proxy) et reçoit de l’aide d’IoT Hub pour établir la connexion sans demander de ports ouverts dans le pare-feu local.</span><span class="sxs-lookup"><span data-stu-id="0de53-126">The client uses a [reverse-proxy](https://wikipedia.org/wiki/Reverse_proxy) and receives help from IoT Hub to make the connection without requiring open ports in the on-premises firewall.</span></span> <span data-ttu-id="0de53-127">Ce modèle de communication est appelé [communication assistée par le service](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span><span class="sxs-lookup"><span data-stu-id="0de53-127">This communication pattern is called [service-assisted communication](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span></span> <span data-ttu-id="0de53-128">Pour ce faire, la solution utilise le module IoT Edge de [proxy OPC](https://github.com/Azure/iot-edge-opc-proxy/).</span><span class="sxs-lookup"><span data-stu-id="0de53-128">The solution uses the [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) IoT Edge module for this purpose.</span></span>


## <a name="simulation"></a><span data-ttu-id="0de53-129">Simulation</span><span class="sxs-lookup"><span data-stu-id="0de53-129">Simulation</span></span>

<span data-ttu-id="0de53-130">Les postes et les systèmes d'exécution de la fabrication (MES) simulés constituent une chaîne de fabrication d’usine.</span><span class="sxs-lookup"><span data-stu-id="0de53-130">The simulated stations and the simulated manufacturing execution systems (MES) make up a factory production line.</span></span> <span data-ttu-id="0de53-131">Les appareils simulés et le module Éditeur d’OPC sont basés sur le [Standard OPC UA .NET][lnk-OPC-UA-NET-Standard] publié par la Fondation OPC.</span><span class="sxs-lookup"><span data-stu-id="0de53-131">The simulated devices and the OPC Publisher Module are based on the [OPC UA .NET Standard][lnk-OPC-UA-NET-Standard] published by the OPC Foundation.</span></span>

<span data-ttu-id="0de53-132">Le Proxy OPC et le module Éditeur d’OPC sont implémentés en tant que modules basés sur [Azure IoT Edge][lnk-Azure-IoT-Gateway].</span><span class="sxs-lookup"><span data-stu-id="0de53-132">The OPC Proxy and OPC Publisher are implemented as modules based on [Azure IoT Edge][lnk-Azure-IoT-Gateway].</span></span> <span data-ttu-id="0de53-133">Chaque ligne de production simulée dispose d’une passerelle désignée associée.</span><span class="sxs-lookup"><span data-stu-id="0de53-133">Each simulated production line has a designated gateway attached.</span></span>

<span data-ttu-id="0de53-134">Tous les composants de simulation sont exécutés dans des conteneurs Docker hébergés dans une machine virtuelle Linux Azure.</span><span class="sxs-lookup"><span data-stu-id="0de53-134">All simulation components run in Docker containers  hosted in an Azure Linux VM.</span></span> <span data-ttu-id="0de53-135">La simulation est configurée pour exécuter huit lignes de production simulées par défaut.</span><span class="sxs-lookup"><span data-stu-id="0de53-135">The simulation is configured to run eight simulated production lines by default.</span></span>

## <a name="simulated-production-line"></a><span data-ttu-id="0de53-136">Ligne de production simulée</span><span class="sxs-lookup"><span data-stu-id="0de53-136">Simulated production line</span></span>

<span data-ttu-id="0de53-137">Une ligne de production fabrique des parties.</span><span class="sxs-lookup"><span data-stu-id="0de53-137">A production line manufactures parts.</span></span> <span data-ttu-id="0de53-138">Elle est composée de différents postes : un poste d’assembly, un poste de test et un poste de packaging.</span><span class="sxs-lookup"><span data-stu-id="0de53-138">It is composed of different stations: an assembly station, a test station, and a packaging station.</span></span>

<span data-ttu-id="0de53-139">La simulation s’exécute et met à jour les données exposées via les nœuds OPC UA.</span><span class="sxs-lookup"><span data-stu-id="0de53-139">The simulation runs and updates the data that is exposed through the OPC UA nodes.</span></span> <span data-ttu-id="0de53-140">Toutes les stations de ligne de production simulées sont orchestrées par le MES via OPC UA.</span><span class="sxs-lookup"><span data-stu-id="0de53-140">All simulated production line stations are orchestrated by the MES through OPC UA.</span></span>

## <a name="simulated-manufacturing-execution-system"></a><span data-ttu-id="0de53-141">Simulation de système d’exécution de fabrication</span><span class="sxs-lookup"><span data-stu-id="0de53-141">Simulated manufacturing execution system</span></span>

<span data-ttu-id="0de53-142">Le MES analyse chaque poste dans la ligne de production via OPC UA pour détecter les modifications d’état des postes.</span><span class="sxs-lookup"><span data-stu-id="0de53-142">The MES monitors each station in the production line through OPC UA to detect station status changes.</span></span> <span data-ttu-id="0de53-143">Il appelle des méthodes OPC UA pour contrôler les stations et transmet les produits d’un poste à l’autre jusqu'à la fin de l’opération.</span><span class="sxs-lookup"><span data-stu-id="0de53-143">It calls OPC UA methods to control the stations and passes a product from one station to the next until it is complete.</span></span>

## <a name="gateway-opc-publisher-module"></a><span data-ttu-id="0de53-144">Module Éditeur d’OPC de la passerelle</span><span class="sxs-lookup"><span data-stu-id="0de53-144">Gateway OPC publisher module</span></span>

<span data-ttu-id="0de53-145">Le module Éditeur d’OPC se connecte aux serveurs de poste OPC UA et s’abonne aux nœuds OPC à publier.</span><span class="sxs-lookup"><span data-stu-id="0de53-145">OPC Publisher Module connects to the station OPC UA servers and subscribes to the OPC nodes to be published.</span></span> <span data-ttu-id="0de53-146">Le module convertit les données de nœud au format JSON, les chiffre et les envoie au IoT Hub sous forme de messages OPC UA Pub/Sub.</span><span class="sxs-lookup"><span data-stu-id="0de53-146">The module converts the node data into JSON format, encrypts it, and sends it to IoT Hub as OPC UA Pub/Sub messages.</span></span>

<span data-ttu-id="0de53-147">Le module Éditeur d’OPC nécessite un port sortant https (443) uniquement et fonctionne avec l’infrastructure d’entreprise existante.</span><span class="sxs-lookup"><span data-stu-id="0de53-147">The OPC Publisher module only requires an outbound https port (443) and can work with existing enterprise infrastructure.</span></span>

## <a name="gateway-opc-proxy-module"></a><span data-ttu-id="0de53-148">Module proxy OPC de la passerelle</span><span class="sxs-lookup"><span data-stu-id="0de53-148">Gateway OPC proxy module</span></span>

<span data-ttu-id="0de53-149">Le module proxy OPC UA de la passerelle « tunnele » les messages OPC UA binaires de commande et de contrôle et nécessite seulement un port sortant https (443).</span><span class="sxs-lookup"><span data-stu-id="0de53-149">The Gateway OPC UA Proxy Module tunnels binary OPC UA command and control messages and only requires an outbound https port (443).</span></span> <span data-ttu-id="0de53-150">Il est compatible avec l’infrastructure d’entreprise existante, y compris les proxys Web.</span><span class="sxs-lookup"><span data-stu-id="0de53-150">It can work with existing enterprise infrastructure, including Web Proxies.</span></span>

<span data-ttu-id="0de53-151">Il utilise des méthodes d’appareil IoT Hub pour transférer des données TCP/IP en paquets à la couche d’application et garantit ainsi l’approbation du point de terminaison, le chiffrement des données et l’intégrité à l’aide de SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="0de53-151">It uses IoT Hub Device methods to transfer packetized TCP/IP data at the application layer and thus ensures endpoint trust, data encryption, and integrity using SSL/TLS.</span></span>

<span data-ttu-id="0de53-152">Le protocole binaire OPC UA relayé via le proxy utilise le chiffrement et l’authentification UA.</span><span class="sxs-lookup"><span data-stu-id="0de53-152">The OPC UA binary protocol relayed through the proxy itself uses UA authentication and encryption.</span></span>

## <a name="azure-time-series-insights"></a><span data-ttu-id="0de53-153">Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="0de53-153">Azure Time Series Insights</span></span>

<span data-ttu-id="0de53-154">Le module Éditeur d’OPC de la passerelle s’abonne à des nœuds de serveur OPC UA pour détecter des modifications dans les valeurs de données.</span><span class="sxs-lookup"><span data-stu-id="0de53-154">The Gateway OPC Publisher Module subscribes to OPC UA server nodes to detect change in the data values.</span></span> <span data-ttu-id="0de53-155">Si une modification de données est détectée dans un des nœuds, ce module envoie des messages à Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0de53-155">If a data change is detected in one of the nodes, this module then sends messages to Azure IoT Hub.</span></span>

<span data-ttu-id="0de53-156">IoT Hub fournit une source d’événements à Azure STI.</span><span class="sxs-lookup"><span data-stu-id="0de53-156">IoT Hub provides an event source to Azure TSI.</span></span> <span data-ttu-id="0de53-157">STI stocke les données durant 30 jours en fonction des horodatages associés messages.</span><span class="sxs-lookup"><span data-stu-id="0de53-157">TSI stores data for 30 days based on timestamps attached to the messages.</span></span> <span data-ttu-id="0de53-158">Ces données incluent :</span><span class="sxs-lookup"><span data-stu-id="0de53-158">This data includes:</span></span>

* <span data-ttu-id="0de53-159">OPC UA ApplicationUri</span><span class="sxs-lookup"><span data-stu-id="0de53-159">OPC UA ApplicationUri</span></span>
* <span data-ttu-id="0de53-160">OPC UA NodeId</span><span class="sxs-lookup"><span data-stu-id="0de53-160">OPC UA NodeId</span></span>
* <span data-ttu-id="0de53-161">Valeur du nœud</span><span class="sxs-lookup"><span data-stu-id="0de53-161">Value of the node</span></span>
* <span data-ttu-id="0de53-162">Source timestamp</span><span class="sxs-lookup"><span data-stu-id="0de53-162">Source timestamp</span></span>
* <span data-ttu-id="0de53-163">OPC UA DisplayName</span><span class="sxs-lookup"><span data-stu-id="0de53-163">OPC UA DisplayName</span></span>

<span data-ttu-id="0de53-164">Actuellement, STI n’autorise pas les clients à personnaliser la durée pendant laquelle ils souhaitent conserver les données.</span><span class="sxs-lookup"><span data-stu-id="0de53-164">Currently, TSI does not allow customers to customize how long they wish to keep the data for.</span></span>

<span data-ttu-id="0de53-165">Requêtes de STI sur les données de nœud à l’aide d’un SearchSpan (Time.From, Time.To) et des agrégats par OPC UA ApplicationUri ou OPC UA NodeId ou OPC UA DisplayName.</span><span class="sxs-lookup"><span data-stu-id="0de53-165">TSI queries against node data using a SearchSpan (Time.From, Time.To) and aggregates by OPC UA ApplicationUri or OPC UA NodeId or OPC UA DisplayName.</span></span>

<span data-ttu-id="0de53-166">Pour récupérer les données pour les jauges OEE et KPI et les graphiques de séries chronologiques, les données sont agrégées par nombre d’événements, Sum, Avg, Min et Max.</span><span class="sxs-lookup"><span data-stu-id="0de53-166">To retrieve the data for the OEE and KPI gauges, and the time series charts, data is aggregated by count of events, Sum, Avg, Min, and Max.</span></span>

<span data-ttu-id="0de53-167">Les séries chronologiques sont créées à l’aide d’un processus différent.</span><span class="sxs-lookup"><span data-stu-id="0de53-167">The time series are built using a different process.</span></span> <span data-ttu-id="0de53-168">Les OOE et les KPI sont calculées à partir des données de base des postes et propagées pour la topologie (lignes de production, usines, entreprise) dans l’application.</span><span class="sxs-lookup"><span data-stu-id="0de53-168">OEE and KPIs are calculated from station base data and bubbled up for the topology (production lines, factories, enterprise) in the application.</span></span>

<span data-ttu-id="0de53-169">En outre, les séries chronologiques pour la topologie OEE et KPI sont calculées dans l’application, chaque fois qu’un intervalle de temps affiché est prêt.</span><span class="sxs-lookup"><span data-stu-id="0de53-169">Additionally, time series for OEE and KPI topology is calculated in the app, whenever a displayed timespan is ready.</span></span> <span data-ttu-id="0de53-170">Par exemple, l’affichage quotidien est mis à jour chaque heure complète.</span><span class="sxs-lookup"><span data-stu-id="0de53-170">For example, the day view is updated every full hour.</span></span>

<span data-ttu-id="0de53-171">L’affichage de séries chronologiques des données de nœud provient directement de STI à l’aide d’une agrégation pour l’intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="0de53-171">The time series view of node data comes directly from TSI using an aggregation for timespan.</span></span>

## <a name="iot-hub"></a><span data-ttu-id="0de53-172">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="0de53-172">IoT Hub</span></span>
<span data-ttu-id="0de53-173">[IoT Hub][lnk-IoT Hub] reçoit les données envoyées par le module Éditeur d’OPC au cloud et les rend disponibles au service Azure TSI.</span><span class="sxs-lookup"><span data-stu-id="0de53-173">The [IoT hub][lnk-IoT Hub] receives data sent from the OPC Publisher Module into the cloud and makes it available to the Azure TSI service.</span></span> 

<span data-ttu-id="0de53-174">L’instance IoT Hub de la solution effectue également ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="0de53-174">The IoT Hub in the solution also:</span></span>
- <span data-ttu-id="0de53-175">Gère un registre d’identité qui stocke les ID des modules Éditeur d’OPC et de tous les modules de Proxy OPC.</span><span class="sxs-lookup"><span data-stu-id="0de53-175">Maintains an identity registry that stores the IDs for all OPC Publisher Module and all OPC Proxy Modules.</span></span>
- <span data-ttu-id="0de53-176">Est utilisé en tant que canal de transport pour la communication bidirectionnelle du module Proxy OPC.</span><span class="sxs-lookup"><span data-stu-id="0de53-176">Is used as transport channel for bidirectional communication of the OPC Proxy Module.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="0de53-177">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0de53-177">Azure Storage</span></span>
<span data-ttu-id="0de53-178">La solution utilise le stockage d’objets blob Azure comme stockage sur disque pour la machine virtuelle et pour stocker les données de déploiement.</span><span class="sxs-lookup"><span data-stu-id="0de53-178">The solution uses Azure blob storage as disk storage for the VM and to store deployment data.</span></span>

## <a name="web-app"></a><span data-ttu-id="0de53-179">Application web</span><span class="sxs-lookup"><span data-stu-id="0de53-179">Web app</span></span>
<span data-ttu-id="0de53-180">L’application web déployée dans le cadre de la solution préconfigurée comprend un client OPC UA intégré, un système de traitement des alertes et de visualisation de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="0de53-180">The web app deployed as part of the preconfigured solution comprises of an integrated OPC UA client, alerts processing and telemetry visualization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0de53-181">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0de53-181">Next steps</span></span>

<span data-ttu-id="0de53-182">Vous pouvez poursuivre la prise en main d’IoT Suite en lisant les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="0de53-182">You can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="0de53-183">[Autorisations sur le site azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="0de53-183">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="0de53-184">Déployer une passerelle sur Windows ou Linux pour la solution préconfigurée d’usine connectée</span><span class="sxs-lookup"><span data-stu-id="0de53-184">Deploy a gateway on Windows or Linux for the connected factory preconfigured solution</span></span>](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
