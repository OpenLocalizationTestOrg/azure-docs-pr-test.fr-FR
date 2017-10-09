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
# <a name="connected-factory-preconfigured-solution-walkthrough"></a>Procédure pas à pas de la solution préconfigurée d’usine connectée

Hello IoT Suite connecté fabrique [solution préconfigurée] [ lnk-preconfigured-solutions] est une implémentation d’une solution de bout en bout industrielle qui :

* Se connecte les appareils industriels tooboth simulée exécutant des serveurs OPC UA des lignes de production simulé fabrique et des appareils de serveur réels OPC UA. Pour plus d’informations sur OPC UA, consultez hello [connecté fabrique FAQ](iot-suite-faq-cf.md).
* Affiche les indicateurs de performance clé (KPI) opérationnels et les OEE de ces appareils et des lignes de production.
* Montre comment une application basée sur le cloud peut être toointeract utilisé avec les systèmes de serveur OPC UA.
* Permet de vous tooconnect les appareils de votre propre serveur OPC UA.
* Vous permet de toobrowse et modifier hello données OPC UA du serveur.
* S’intègre avec hello Azure temps série Insights (STI) service tooprovide des vues personnalisées de données hello à partir de vos serveurs OPC UA.

Vous pouvez utiliser la solution de hello comme point de départ pour votre propre implémentation et [personnaliser] [ lnk-customize] il toomeet vos propres besoins professionnels spécifiques.

Cet article vous guide certains éléments clés hello hello connecté fabrique solution tooenable toounderstand son fonctionnement. Ces connaissances vous aident à :

* Résoudre les problèmes dans les solutions hello.
* Planifier comment toocustomize toohello solution toomeet vos besoins spécifiques.
* Concevoir votre propre solution IoT utilisant des services Azure.

Pour plus d’informations, consultez hello [connecté fabrique FAQ](iot-suite-faq-cf.md).

## <a name="logical-architecture"></a>Architecture logique

Hello suivant schéma présente des composants logiques de hello de solution de hello préconfiguré :

![Architecture logique d’usine connectée][connected-factory-logical]

## <a name="communication-patterns"></a>Modèles de communication

solution de Hello utilise hello [les spécification OPC UA Pub/Sub](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend OPC UA télémétrie données tooIoT Hub au format JSON. solution de Hello utilise hello [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) module IoT Edge à cet effet.

solution de Hello possède également un client OPC UA intégré dans une application web qui peut établir des connexions avec des serveurs locaux OPC UA. Hello client utilise un [proxy inversé](https://wikipedia.org/wiki/Reverse_proxy) et reçoit les aide à partir de la connexion de IoT Hub toomake hello sans devoir ouvrir les ports dans le pare-feu local hello. Ce modèle de communication est appelé [communication assistée par le service](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/). solution de Hello utilise hello [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) module IoT Edge à cet effet.


## <a name="simulation"></a>Simulation

Hello simulés stations et production hello simulée systèmes (MES) constituent une ligne en usine. Hello simulations de périphériques et hello OPC Publisher Module sont basés sur hello [OPC UA .NET Standard] [ lnk-OPC-UA-NET-Standard] publié par hello OPC Foundation.

Hello OPC Proxy et le serveur de publication OPC sont implémentés en tant que modules basés sur [Azure IoT bord][lnk-Azure-IoT-Gateway]. Chaque ligne de production simulée dispose d’une passerelle désignée associée.

Tous les composants de simulation sont exécutés dans des conteneurs Docker hébergés dans une machine virtuelle Linux Azure. simulation de Hello est configuré toorun huit lignes production simulé par défaut.

## <a name="simulated-production-line"></a>Ligne de production simulée

Une ligne de production fabrique des parties. Elle est composée de différents postes : un poste d’assembly, un poste de test et un poste de packaging.

simulation de Hello s’exécute et met à jour les données hello qui sont exposées via des nœuds OPC UA hello. Toutes les stations line simulé de production sont orchestrées par hello MES via OPC UA.

## <a name="simulated-manufacturing-execution-system"></a>Simulation de système d’exécution de fabrication

Hello MES analyse chaque station dans la ligne de production hello à travers les modifications d’état OPC UA toodetect station. Il appelle OPC UA stations de méthodes toocontrol hello et transmet ensuite un produit à partir d’une station toohello qu’elle soit terminée.

## <a name="gateway-opc-publisher-module"></a>Module Éditeur d’OPC de la passerelle

Module de serveur de publication OPC connecte toohello station OPC UA serveurs et s’abonne toohello OPC nœuds toobe publié. module de Hello convertit les données du nœud hello en format JSON, chiffre et envoie tooIoT Hub en tant que messages de OPC UA Pub/Sub.

module de serveur de publication OPC Hello nécessite un port sortant https (443) uniquement et permettre travailler avec l’infrastructure d’entreprise existante.

## <a name="gateway-opc-proxy-module"></a>Module proxy OPC de la passerelle

Hello passerelle OPC UA Proxy Module utilise des messages de contrôle et commande OPC UA binaires et seulement nécessite un port sortant https (443). Il est compatible avec l’infrastructure d’entreprise existante, y compris les proxys Web.

Il utilise un appareil de Hub IoT méthodes tootransfer en paquets TCP/IP données au niveau de la couche d’application hello et garantit ainsi la confiance de point de terminaison, le chiffrement des données et d’intégrité à l’aide de SSL/TLS.

Hello protocole binaire de OPC UA relayée via proxy hello lui-même utilise le chiffrement et authentification de l’agent utilisateur.

## <a name="azure-time-series-insights"></a>Azure Time Series Insights

Hello passerelle OPC Publisher Module s’abonne modifications tooOPC UA server nœuds toodetect hello valeurs de données. Si une modification de données est détectée dans un des nœuds de hello, ce module envoie ensuite les messages tooAzure IoT Hub.

IoT Hub fournit un tooAzure de source d’événement STI. STI stocke les données pendant 30 jours en fonction des horodatages attaché toohello messages. Ces données incluent :

* OPC UA ApplicationUri
* OPC UA NodeId
* Valeur du nœud de hello
* Source timestamp
* OPC UA DisplayName

Actuellement, STI n’autorise pas les clients toocustomize combien ils veulent tookeep données hello.

Requêtes de STI sur les données de nœud à l’aide d’un SearchSpan (Time.From, Time.To) et des agrégats par OPC UA ApplicationUri ou OPC UA NodeId ou OPC UA DisplayName.

tooretrieve les données de hello pour les jauges OEE et l’indicateur de performance clé hello et graphiques de série de temps hello, les données sont agrégées par nombre d’événements, Sum, Avg, Min et Max.

MTS Hello sont créées à l’aide d’un autre processus. OEE et indicateurs de performance clés sont calculées à partir des données de base station et propagés pour topologie hello (lignes de production, fabriques, entreprise) dans une application hello.

En outre, série chronologique pour topologie OEE et l’indicateur de performance clé est calculée dans une application hello, chaque fois qu’un intervalle de temps affiché est prêt. Par exemple, affichage du jour hello est mise à jour chaque heure complète.

la vue de données du nœud de série au moment Hello proviennent directement de STI à l’aide d’une agrégation pour l’intervalle de temps.

## <a name="iot-hub"></a>IoT Hub
Hello [IoT hub] [ lnk-IoT Hub] reçoit les données envoyées de hello OPC Publisher Module dans le cloud de hello et rend le service de Azure STI toohello disponibles. 

Hello IoT Hub dans les solutions hello également :
- Gère un registre des identités qui stocke les identificateurs hello pour tout Module de serveur de publication OPC et tous les Modules de Proxy OPC.
- Est utilisé en tant que canal de transport pour la communication bidirectionnelle de hello OPC Proxy Module.

## <a name="azure-storage"></a>Azure Storage
solution de Hello utilise le stockage d’objets blob Azure en tant que stockage de disque pour les données de déploiement de machine virtuelle et toostore hello.

## <a name="web-app"></a>Application web
application Hello web déployée comme partie de hello préconfiguré solution se compose d’un client OPC UA intégré, le traitement des alertes et visualisation des données de télémétrie.

## <a name="next-steps"></a>Étapes suivantes

Vous pouvez continuer la mise en route avec IoT Suite en lisant hello suivant des articles :

* [Autorisations sur le site de azureiotsuite.com hello][lnk-permissions]
* [Déployer une passerelle sur Windows ou Linux pour la solution de fabrique préconfiguré hello connecté](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
