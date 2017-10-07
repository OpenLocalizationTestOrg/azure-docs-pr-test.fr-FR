---
title: "aaaAzure IoT préconfiguré solutions | Documents Microsoft"
description: "Obtenir une description de hello Azure IoT préconfiguré solutions ainsi que leur architecture avec des ressources tooadditional des liens."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 59009f37-9ba0-4e17-a189-7ea354a858a2
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: bd059d08ab458fdb0b6f49b3ac469db930dab09e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-hello-azure-iot-suite-preconfigured-solutions"></a>Quelles sont les solutions Azure IoT Suite préconfiguré hello ?

Bonjour Azure IoT préconfiguré suites sont des implémentations de modèles de solution IoT courants que vous pouvez déployer tooAzure à l’aide de votre abonnement. Vous pouvez utiliser des solutions de hello préconfiguré :

* Comme point de départ de vos propres solutions IoT.
* toolearn sur des modèles courants dans le développement et de conception de la solution IoT.

Chaque solution préconfigurée est une implémentation complète, de bout en bout qu’utilise simulées télémétrie toogenerate de périphériques.

Vous pouvez télécharger toocustomize de code source complet hello et étendre hello solution toomeet vos exigences IoT spécifiques.

> [!NOTE]
> toodeploy une Hello préconfiguré solutions, visitez le site [Microsoft Azure IoT Suite][lnk-azureiotsuite]. article de Hello [prise en main des solutions IoT préconfiguré hello] [ lnk-getstarted-preconfigured] fournit plus d’informations sur comment toodeploy et une exécution de hello solutions.

Hello tableau suivant montre comment les solutions hello mappent toospecific IoT fonctionnalités :

| Solution | Ingestion de données | Identité d’appareil | Gestion des appareils | Commande et contrôle | Règles et actions | Analyse prédictive |
| --- | --- | --- | --- | --- | --- | --- |
| [Surveillance à distance][lnk-getstarted-preconfigured] |Oui |Oui |Oui |Oui |Oui |- |
| [Maintenance prédictive][lnk-predictive-maintenance] |Oui |Oui |- |Oui |Oui |Oui |
| [Fabrique connectée][lnk-getstarted-factory] |Oui |Oui |Oui |Oui |Oui |- |

* *Intégrer les données*: entrée de données au cloud toohello de mise à l’échelle.
* *Identité de l’appareil*: appareil accès toohello solution de contrôle et de gérer les identités d’appareil unique.
* *Gestion des appareils* : gérez les métadonnées de l’appareil et effectuez des opérations comme le redémarrage d’appareils et la mise à jour du microprogramme.
* *Contrôle et commande*: toocause hello appareil tootake une action, envoyer des messages de périphérique de tooa du cloud de hello.
* *Les règles et les actions*: tooact sur des données spécifiques appareil-à-cloud, hello solution back-end utilise des règles.
* *Analytique prédictive*: hello solution back-end analyse toopredict de données de l’appareil-à-cloud lorsque des actions spécifiques doivent avoir lieu. Par exemple, analyser avion moteur télémétrie toodetermine lors de la maintenance du moteur est due.

## <a name="remote-monitoring-preconfigured-solution-overview"></a>Présentation de la solution préconfigurée de surveillance à distance

Nous avons choisi toodiscuss hello solution préconfigurée de contrôle à distance dans cet article, car il illustre de nombreux éléments de conception communs qui hello autre partage de solutions.

Hello diagramme suivant illustre hello principaux éléments de solution de surveillance à distance de hello. Hello sections suivantes fournissent plus d’informations sur ces éléments.

![Architecture de la solution préconfigurée Surveillance à distance][img-remote-monitoring-arch]

## <a name="devices"></a>Appareils

Lorsque vous déployez hello solution préconfigurée de surveillance à distance, quatre périphériques simulées sont préconfigurés dans solution hello qui simulent un périphérique de refroidissement. Ces appareils de simulation intègrent un modèle de température et d’humidité qui génère des données de télémétrie. Ces appareils simulés sont inclus pour :

- Illustrer le flux de bout en bout de hello des données dans les solutions hello.
- Fournir une source de données de télémétrie pratique.
- Fournissent une cible pour les méthodes ou les commandes si vous êtes un développeur de back-end à l’aide des solutions de hello comme point de départ pour une implémentation personnalisée.

appareils Hello simulé dans la solution de hello peuvent répondre toohello suivant les communications du cloud sur l’appareil :

- *Méthodes ([direct de méthodes][lnk-direct-methods])*: une méthode de communication bidirectionnelle où un périphérique connecté est attendu toorespond immédiatement.
- *Commandes (messages cloud-à-appareil)*: une méthode de communication unidirectionnelle où un périphérique récupère commande hello à partir d’une file d’attente durable.

Pour une comparaison de ces différentes approches, consultez [Conseils pour les communications cloud-à-appareil][lnk-c2d-guidance].

Lorsqu’un périphérique connecte tooIoT Hub dans les solutions hello préconfiguré d’abord, il envoie un concentrateur de toohello du message d’informations de périphérique. Ce message énumère les méthodes hello appareil de hello peut répondre à. Bonjour solution préconfigurée de surveillance à distance, simulations de périphériques prennent en charge ces méthodes :

* *Lancer la mise à jour de microprogramme*: cette méthode démarre une tâche asynchrone sur hello appareil tooperform une mise à jour du microprogramme. tâche asynchrone Hello utilise les propriétés déclarées toodeliver état des mises à jour toohello solution du tableau de bord.
* *Redémarrez*: cette méthode provoque hello simulée périphérique tooreboot.
* *FactoryReset*: cette méthode déclenche usine sur l’appareil simulé de hello.

Lorsqu’un périphérique connecte tooIoT Hub dans les solutions hello préconfiguré d’abord, il envoie un concentrateur de toohello du message d’informations de périphérique. Ce message énumère les commandes hello appareil de hello peut répondre à. Bonjour solution préconfigurée de surveillance à distance, simulations de périphériques prennent en charge ces commandes :

* *Appareil de ping*: hello répond commande toothis avec un accusé de réception. Cette commande est utile pour la vérification de que ce périphérique hello est toujours active et à l’écoute.
* *Démarrer la télémétrie*: fait en sorte que toostart de périphérique hello envoi de données de télémétrie.
* *Arrêter la télémétrie*: fait en sorte que toostop de périphérique hello envoi de données de télémétrie.
* *Modifier la température de définir le Point*: contrôles hello température simulé télémétrie valeurs hello appareil envoie. Cette commande est utile dans le cadre de tests de logique Back-end.
* *Télémétrie de diagnostic*: contrôle si l’appareil de hello doit envoyer les températures externes hello en tant que données de télémétrie.
* *Changement d’état périphérique*: définit hello appareil état métadonnées propriété hello des rapports de l’appareil. Cette commande est utile dans le cadre de tests de logique Back-end.

Vous pouvez ajouter plusieurs simulations de périphériques toohello solution qui émettent hello télémétrie même et y répondre toohello même des méthodes et des commandes.

En outre tooresponding toocommands et les méthodes, les solutions hello utilisent [jumeaux de périphérique][lnk-device-twin]. Les périphériques utilisent un appareil jumeaux tooreport propriété valeurs toohello solution back-end. tableau de bord de solution Hello utilise les valeurs de propriété appareil jumeaux tooset toonew souhaitée sur les appareils. Par exemple, au cours des rapports d’appareils hello simulée hello microprogramme mise à jour de processus hello état Hello mis à jour à l’aide des propriétés déclarées.

## <a name="iot-hub"></a>IoT Hub

Dans cette solution préconfigurée, hello IoT Hub correspond instance toohello *passerelle de Cloud* courant [architecture de solution IoT][lnk-what-is-azure-iot].

Un hub IoT reçoit la télémétrie à partir d’appareils hello à un seul point de terminaison. Un hub IoT conserve également des points de terminaison spécifique à l’appareil où chaque périphérique peut récupérer les commandes hello envoyés tooit.

IoT hub de Hello rend les données de télémétrie hello reçu disponibles via la télémétrie du côté service hello lire le point de terminaison.

fonctionnalité de gestion de périphérique de Hello de IoT Hub permet de vous toomanage vos propriétés de l’appareil à partir des travaux de planification et de portail de solution hello qui effectuent des opérations telles que :

- Redémarrage des appareils
- Changement d’état d’appareil
- Mises à jour de microprogramme

## <a name="azure-stream-analytics"></a>Azure Stream Analytics

Hello solution préconfigurée utilise trois [Analytique de flux de données Azure] [ lnk-asa] (ASA) travaux toofilter hello télémétrie des flux de données à partir d’appareils de hello :

* *DeviceInfo travail* -concentrateur d’événements sorties données tooan qui achemine le Registre des appareils appareil messages spécifiques d’inscription toohello solution. Le registre d’appareils correspond à une base de données Azure Cosmos DB. Ces messages sont envoyés lorsqu’un périphérique se connecte d’abord ou dans la réponse tooa **modifier l’état de l’appareil** commande.
* *Travail de télémétrie* - envoie tout le stockage blob brutes de télémesure de tooAzure pour le stockage à froid et calculant des agrégations de données de télémétrie qui s’affichent dans le tableau de bord de solution hello.
* *Travail de règles* - filtres hello des flux de données de télémétrie pour les valeurs qui dépassent les seuils de règle et sorties hello concentrateur d’événements de tooan de données. Lorsqu’une règle se déclenche, vue de tableau de bord de portail hello solutions affiche cet événement comme une nouvelle ligne dans la table d’historique alarme hello. Ces règles peuvent également déclencher une action basée sur les paramètres de hello définis sur hello **règles** et **Actions** vues dans le portail de solution hello.

Dans cette solution préconfigurée, hello ASA travaux font partie de toohello **principal solution IoT** courant [architecture de solution IoT][lnk-what-is-azure-iot].

## <a name="event-processor"></a>Processeur d’événements

Dans cette solution préconfigurée, processeur d’événements hello constitue une partie de hello **principal solution IoT** courant [architecture de solution IoT][lnk-what-is-azure-iot].

Hello **DeviceInfo** et **règles** les travaux ASA envoyer leurs concentrateurs tooEvent de sortie pour la remise tooother les services principaux. Hello solution utilise une [EventProcessorHost] [ lnk-event-processor] instance, en cours d’exécution un [WebJob][lnk-web-job], messages de type hello tooread à partir de ces concentrateurs d’événements. Hello **EventProcessorHost** utilise :
- Hello **DeviceInfo** tooupdate hello unité de données dans la base de données de la base de données Cosmos hello.
- Hello **règles** tooinvoke hello logique application et mise à jour hello alertes de données affichent dans le portail de solution hello.

## <a name="device-identity-registry-device-twin-and-cosmos-db"></a>Registre d’identité des appareils, jumeau d’appareil et Cosmos DB

Chaque IoT hub inclut un [registre d’identité des appareils][lnk-identity-registry] qui stocke des clés d’appareils. IoT Hub utilise ces informations authentifier les appareils : un périphérique doit être enregistré et disposer d’une clé valide avant de se connecter toohello hub.

A [double de l’appareil] [ lnk-device-twin] est un document JSON géré par hello IoT Hub. Une représentation d’appareil contient :

- Propriétés signalées envoyées par le concentrateur de toohello périphérique hello. Vous pouvez afficher ces propriétés dans le portail de solution hello.
- Propriétés souhaitées que vous souhaitez toosend toohello appareil. Vous pouvez définir ces propriétés dans le portail de solution hello.
- Balises qui existent uniquement en double d’appareil hello et non sur le périphérique de hello. Vous pouvez utiliser ces listes toofilter de balises de périphériques dans le portail de solution hello.

Cette solution utilise des métadonnées de périphérique jumeaux toomanage appareil. solution de Hello utilise également un Cosmos DB de base de données toostore appareil spécifiques à des solutions supplémentaires de données telles que les commandes hello pris en charge par chaque périphérique et hello historique des commandes.

solution de Hello doit également conserver les informations de hello dans Registre des identités hello périphérique synchronisé avec le contenu de hello de base de données de la base de données Cosmos hello. Hello **EventProcessorHost** utilise hello des données à partir de **DeviceInfo** analytique de flux de données de synchronisation de hello toomanage la tâche.

## <a name="solution-portal"></a>Portail de la solution

![portail de la solution][img-dashboard]

portail de solution Hello est une interface utilisateur web qui est déployé toohello cloud dans le cadre de la solution de hello préconfiguré. Il vous permet d’effectuer les opérations suivantes :

* Afficher l’historique de télémétrie et d’alertes dans un tableau de bord.
* Approvisionner de nouveaux appareils.
* Gérer et surveiller des appareils.
* Envoyer des commandes toospecific périphériques.
* Des méthodes d’appel sur des appareils spécifiques.
* Gérer les règles et les actions.
* Planifier toorun travaux sur un ou plusieurs périphériques.

Dans cette solution préconfigurée, portail de solution hello constitue une partie de hello **principal solution IoT** et fait partie intégrante hello **connectivité de traitement et d’entreprise** Bonjour classique [solution IoT architecture][lnk-what-is-azure-iot].

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les architectures de solution IoT, consultez le document [Microsoft Azure IoT services: Reference Architecture][lnk-refarch].

Maintenant, vous savez quelle une solution préconfigurée est, vous pouvez commencer en déployant hello *surveillance à distance* solution préconfigurée : [prise en main des solutions hello préconfiguré] [ lnk-getstarted-preconfigured].

[img-remote-monitoring-arch]: ./media/iot-suite-what-are-preconfigured-solutions/remote-monitoring-arch1.png
[img-dashboard]: ./media/iot-suite-what-are-preconfigured-solutions/dashboard.png
[lnk-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-event-processor]: ../event-hubs/event-hubs-programming-guide.md#event-processor-host
[lnk-web-job]: ../app-service-web/web-sites-create-web-jobs.md
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-predictive-maintenance]: iot-suite-predictive-overview.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
[lnk-getstarted-preconfigured]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-getstarted-factory]: iot-suite-connected-factory-overview.md
