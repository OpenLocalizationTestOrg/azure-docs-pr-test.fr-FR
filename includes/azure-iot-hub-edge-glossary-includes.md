## <a name="iot-edge"></a>IoT Edge
Azure IoT Edge permet d’effectuer un déploiement basé sur le cloud de services Azure et de code spécifique de solution sur des appareils locaux. Les appareils IoT Edge peuvent agréger des données d’autres appareils afin d’effectuer un calcul et une analyse avant d’envoyer les données vers le cloud. Pour plus d’informations, consultez [Azure IoT Edge](https://docs.microsoft.com/azure/iot-edge/).

## <a name="iot-edge-agent"></a>Agent IoT Edge
Partie du runtime IoT Edge responsable des modules de déploiement et de surveillance.

## <a name="iot-edge-device"></a>Appareil IoT Edge
Un runtime IoT Edge doit être installé sur les appareils IoT Edge et ces derniers doivent être marqués comme « Appareil IoT Edge » dans les détails de l’appareil. En savoir plus sur [Déployer Azure IoT Edge sur un appareil simulé dans Linux - préversion](https://docs.microsoft.com/azure/iot-edge/tutorial-simulate-device-linux).

## <a name="iot-edge-deployment"></a>Déploiement IoT Edge
Un déploiement IoT Edge configure un ensemble cible d’appareils IoT Edge pour exécuter un ensemble de modules IoT Edge. Chaque déploiement s’assure en permanence que tous les appareils qui correspondent à la condition cible exécutent l’ensemble spécifié de modules, même lorsque de nouveaux appareils sont créés ou modifiées pour correspondre à la condition cible. Chaque appareil IoT Edge ne reçoit que le déploiement de priorité la plus élevée pour lequel il répond à la condition cible. Pour en savoir plus sur le [Déploiement IoT Edge](https://docs.microsoft.com/azure/iot-edge/module-deployment-monitoring).

## <a name="iot-edge-deployment-manifest"></a>Manifeste de déploiement IoT Edge
Document JSON contenant les informations à copier dans une ou plusieurs représentations de modules d’appareils IoT Edge pour déployer un ensemble de modules, itinéraires et propriétés souhaitées de module associé.

## <a name="iot-edge-gateway-device"></a>Appareil de passerelle IoT Edge
Appareil IoT Edge avec appareil en aval. L’appareil en aval peut être un appareil IoT Edge ou non IoT Edge.

## <a name="iot-edge-hub"></a>Hub IoT Edge
Partie du runtime IoT Edge responsable des communications entre modules, des communications en amont (vers IoT Hub) et en aval (depuis IoT Hub). 

## <a name="iot-edge-leaf-device"></a>Appareil de nœud terminal IoT Edge
Appareil IoT Edge avec aucun appareil en aval. 

## <a name="iot-edge-module"></a>Module IoT Edge
Un module IoT Edge est un conteneur Docker que vous pouvez déployer sur des appareils IoT Edge. Il effectue une tâche spécifique, comme l’ingestion de messages provenant d’appareils, la transformation de messages ou l’envoi de messages à un IoT Hub. Il communique avec d’autres modules et envoie des données au runtime IoT Edge. [Comprendre les exigences et outils de développement de modules IoT Edge](https://docs.microsoft.com/azure/iot-edge/module-development).

## <a name="iot-edge-module-identity"></a>Identité de module IoT Edge
Enregistrement dans le registre d’identités de module IoT Hub détaillant les informations d’identification d’existence et de sécurité utilisées par un module pour s’authentifier à Edge Hub ou un IoT Hub.

## <a name="iot-edge-module-image"></a>Image de module IoT Edge
Image Docker utilisée par le runtime IoT Edge pour instancier des instances de module.

## <a name="iot-edge-module-twin"></a>Représentation de module IoT Edge
Document JSON permanent dans l’IoT Hub qui stocke les informations d’état d’une instance de module.

## <a name="iot-edge-priority"></a>Priorité des déploiements IoT Edge
Lorsque deux déploiements IoT Edge ciblent le même appareil, le déploiement avec la priorité plus élevée est appliqué. Si les deux déploiements ont la même priorité, le déploiement avec la date de création la plus tardive est appliqué. En savoir plus sur la [priorité](https://docs.microsoft.com/azure/iot-edge/module-deployment-monitoring#priority).

## <a name="iot-edge-runtime"></a>Runtime IoT Edge
Le runtime IoT Edge inclut tout ce que Microsoft distribue pour l’installation sur un appareil IoT Edge. Il inclut l’agent Edge, Edge Hub et l’outil Edge CTL.

## <a name="iot-edge-set-modules-to-a-single-device"></a>Modules d’ensemble IoT Edge sur un seul appareil
Opération qui copie le contenu d’un manifeste IoT Edge sur une représentation de module d’appareil. L’API sous-jacente est de type « appliquer la configuration » générique, qui utilise simplement un manifeste IoT Edge en tant qu’entrée.

## <a name="iot-edge-target-condition"></a>Condition cible IoT Edge
Dans un déploiement IoT Edge, la condition cible est une condition booléenne sur les balises des représentations d’appareil afin de sélectionner les appareils cibles du déploiement, par exemple, « tag.environment = prod ». La condition cible est évaluée en permanence pour inclure les nouveaux appareils qui répondent aux exigences ou pour supprimer les appareils qui n’y répondent plus. En savoir plus sur la [condition cible](https://docs.microsoft.com/azure/iot-edge/module-deployment-monitoring#target-condition)