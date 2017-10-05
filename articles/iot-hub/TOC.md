# Vue d'ensemble
## [Azure et IoT](iot-hub-what-is-azure-iot.md)
## [Qu’est-ce qu’Azure IoT Hub ?](iot-hub-what-is-iot-hub.md)
## [Présentation de la gestion des appareils](iot-hub-device-management-overview.md)

# [Prise en main](iot-hub-get-started.md)

## Configurer votre appareil
### [Simuler un appareil sur votre ordinateur](iot-hub-get-started-simulated.md)
#### [.NET](iot-hub-csharp-csharp-getstarted.md)
#### [Java](iot-hub-java-java-getstarted.md)
#### [Node.JS](iot-hub-node-node-getstarted.md)
#### [Python](iot-hub-python-getstarted.md)

### [Utiliser un simulateur en ligne](iot-hub-raspberry-pi-web-simulator-get-started.md)

### [Utiliser un appareil physique](iot-hub-get-started-physical.md)
#### [Raspberry Pi avec Python](iot-hub-raspberry-pi-kit-python-get-started.md)
#### [Raspberry Pi avec Node.js](iot-hub-raspberry-pi-kit-node-get-started.md)
#### [Raspberry Pi avec C](iot-hub-raspberry-pi-kit-c-get-started.md)

#### [MXChip IoT DevKit avec Arduino](iot-hub-arduino-iot-devkit-az3166-get-started.md)

#### [Intel Edison avec Node.js](iot-hub-intel-edison-kit-node-get-started.md)
#### [Intel Edison avec C](iot-hub-intel-edison-kit-c-get-started.md)

#### [Adafruit Feather HUZZAH ESP8266 avec Arduino IDE](iot-hub-arduino-huzzah-esp8266-get-started.md)
#### [Sparkfun ESP8266 Thing Dev avec Arduino IDE](iot-hub-sparkfun-esp8266-thing-dev-get-started.md)
#### [Adafruit Feather M0 avec Arduino IDE](iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md)

#### Utiliser le Kit de démarrage de la passerelle IoT
##### [Configurer Intel NUC comme une passerelle](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
##### [Connecter la passerelle à IoT Hub](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
##### [Utiliser la passerelle pour la conversion de données](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)

## Scénarios IoT étendus
### [Gérer la messagerie de périphérique cloud avec iothub-explorer](iot-hub-explorer-cloud-device-messaging.md)
### [Enregistrer les messages IoT Hub dans le stockage de données Azure](iot-hub-store-data-in-azure-table-storage.md)
### [Visualisation des données dans Power BI](iot-hub-live-data-visualization-in-power-bi.md)
### [Visualisation des données avec des applications web](iot-hub-live-data-visualization-in-web-apps.md)
### [Prévisions météo avec Azure Machine Learning](iot-hub-weather-forecast-machine-learning.md)
### [Gestion des appareils avec iothub-explorer](iot-hub-device-management-iothub-explorer.md)
### [Surveillance à distance et notifications avec Logic Apps](iot-hub-monitoring-notifications-with-azure-logic-apps.md)

# Procédure
## Planification
### [Comparaison entre IoT Hub et Event Hubs](iot-hub-compare-event-hubs.md)
### [Mettre à l’échelle votre solution](iot-hub-scaling.md)
### [Haute disponibilité et récupération d’urgence](iot-hub-ha-dr.md)
### [Protocoles supplémentaires pris en charge](iot-hub-protocol-gateway.md)
## [Développement](iot-hub-how-to.md)
### [Guide du développeur](iot-hub-devguide.md)
#### [Guide des fonctionnalités appareil-à-cloud](iot-hub-devguide-d2c-guidance.md)
#### [Guide des fonctionnalités cloud-à-appareil](iot-hub-devguide-c2d-guidance.md)
#### [Envoyer et recevoir des messages](iot-hub-devguide-messaging.md)
##### [Envoyer des messages appareil-à-cloud sur IoT Hub](iot-hub-devguide-messages-d2c.md)
##### [Lire des messages appareil-à-cloud à partir du point de terminaison intégré](iot-hub-devguide-messages-read-builtin.md)
##### [Utiliser des points de terminaison et des règles de routage personnalisés pour les messages appareil-à-cloud](iot-hub-devguide-messages-read-custom.md)
##### [Envoyer des messages cloud-à-appareil à partir d’IoT Hub](iot-hub-devguide-messages-c2d.md)
##### [Créer et lire des messages IoT Hub](iot-hub-devguide-messages-construct.md)
##### [Choisir un protocole de communication](iot-hub-devguide-protocols.md)
#### [Charger des fichiers à partir d’un appareil](iot-hub-devguide-file-upload.md)
#### [Gérer les identités des appareils](iot-hub-devguide-identity-registry.md)
#### [Contrôler l’accès à IoT Hub](iot-hub-devguide-security.md)
#### [Comprendre les représentations d’appareils](iot-hub-devguide-device-twins.md)
#### [Appeler des méthodes directes sur un appareil](iot-hub-devguide-direct-methods.md)
#### [Planifier des travaux sur plusieurs appareils](iot-hub-devguide-jobs.md)
#### [Points de terminaison IoT Hub](iot-hub-devguide-endpoints.md)
#### [Langage de requête](iot-hub-devguide-query-language.md)
#### [Quotas et limitation](iot-hub-devguide-quotas-throttling.md)
#### [Exemples de tarification](iot-hub-devguide-pricing.md)
#### [Kits de développement logiciel (SDK) de services et d’appareils](iot-hub-devguide-sdks.md)
#### [Support MQTT](iot-hub-mqtt-support.md)
#### [Glossaire](iot-hub-devguide-glossary.md)
### [Utiliser le Kit de développement logiciel (SDK) Azure IoT device pour C](iot-hub-device-sdk-c-intro.md)
#### [Utiliser IoTHubClient](iot-hub-device-sdk-c-iothubclient.md)
#### [Utiliser le sérialiseur](iot-hub-device-sdk-c-serializer.md)
### Traitement des messages appareil-à-cloud
#### [.NET](iot-hub-csharp-csharp-process-d2c.md)
#### [Java](iot-hub-java-java-process-d2c.md)
### Envoi de messages cloud vers appareil
#### [.NET](iot-hub-csharp-csharp-c2d.md)
#### [Java](iot-hub-java-java-c2d.md)
#### [Node.JS](iot-hub-node-node-c2d.md)
### [Charger des fichiers à partir d’appareils](iot-hub-csharp-csharp-file-upload.md)
### Prise en main des représentations d’appareils
#### [Serveur principal Node.js/appareil Node.js](iot-hub-node-node-twin-getstarted.md)
#### [Serveur principal .NET/appareil Node.js](iot-hub-csharp-node-twin-getstarted.md)
#### [Appareil back end/.NET de .NET](iot-hub-csharp-csharp-twin-getstarted.md)
#### [Serveur principal Java/appareil Java](iot-hub-java-java-twin-getstarted.md)
### Utiliser des méthodes directes
#### [Serveur principal Node.js/appareil Node.js](iot-hub-node-node-direct-methods.md)
#### [Serveur principal .NET/appareil Node.js](iot-hub-csharp-node-direct-methods.md)
#### [Appareil back end/.NET de .NET](iot-hub-csharp-csharp-direct-methods.md)
#### [Serveur principal Java/appareil Java](iot-hub-java-java-direct-methods.md)
### Prise en main de la gestion d’appareils
#### [Serveur principal Node.js/appareil Node.js](iot-hub-node-node-device-management-get-started.md)
#### [Serveur principal .NET/appareil Node.js](iot-hub-csharp-node-device-management-get-started.md)
#### [Serveur principal Java/appareil Java](iot-hub-java-java-device-management-getstarted.md)
### Utilisation des propriétés des représentations
#### [Serveur principal Node.js/appareil Node.js](iot-hub-node-node-twin-how-to-configure.md)
#### [Serveur principal .NET/appareil Node.js](iot-hub-csharp-node-twin-how-to-configure.md)
#### [Appareil back end/.NET de .NET](iot-hub-csharp-csharp-twin-how-to-configure.md)
### Utiliser des travaux d’appareils pour mettre à jour le microprogramme des appareils
#### [Serveur principal Node/appareil Node](iot-hub-node-node-firmware-update.md)
#### [Serveur principal .NET/appareil Node.js](iot-hub-csharp-node-firmware-update.md)
### Planifier et diffuser des travaux
#### [Serveur principal Node.js/appareil Node.js](iot-hub-node-node-schedule-jobs.md)
#### [Serveur principal .NET/appareil Node.js](iot-hub-csharp-node-schedule-jobs.md)
#### [Java](iot-hub-java-java-schedule-jobs.md)
## Gérer
### Créer un hub IoT 
#### [Utiliser le portail](iot-hub-create-through-portal.md)
#### [Utiliser PowerShell](iot-hub-create-using-powershell.md)
#### [Utiliser l’interface de ligne de commande 2.0](iot-hub-create-using-cli.md)
#### [Utiliser l’interface de ligne de commande](iot-hub-create-using-cli-nodejs.md)
#### [Utiliser l’API REST](iot-hub-rm-rest.md)
#### [Utiliser un modèle à partir de PowerShell](iot-hub-rm-template-powershell.md)
#### [Utiliser un modèle à partir de .NET](iot-hub-rm-template.md)
### Configurer le chargement de fichiers
#### [Utiliser le portail](iot-hub-configure-file-upload.md)
#### [Utiliser PowerShell](iot-hub-configure-file-upload-powershell.md)
#### [Utiliser l’interface de ligne de commande 2.0](iot-hub-configure-file-upload-cli.md)
### [Gestion en bloc des appareils IoT](iot-hub-bulk-identity-mgmt.md)
### [Mesures d’utilisation](iot-hub-metrics.md)
### [Surveillance des opérations](iot-hub-operations-monitoring.md)
### [Configurer le filtrage d’adresse IP](iot-hub-ip-filtering.md)
## Sécuriser
### [Tout savoir sur la sécurité](iot-hub-security-ground-up.md)
### [Meilleures pratiques en matière de sécurité](iot-hub-security-best-practices.md)
### [Architecture de la sécurité](iot-hub-security-architecture.md)
### [Sécuriser votre déploiement IoT](iot-hub-security-deployment.md)
## Azure IoT Edge
### [Vue d'ensemble](iot-hub-iot-edge-overview.md)
### Prise en main
#### [Linux](iot-hub-linux-iot-edge-get-started.md)
#### [Windows](iot-hub-windows-iot-edge-get-started.md)
### Simuler un appareil
#### [Linux](iot-hub-linux-iot-edge-simulated-device.md)
#### [Windows](iot-hub-windows-iot-edge-simulated-device.md)
### [Utiliser un appareil réel](iot-hub-iot-edge-physical-device.md)
### Création d’un module
#### [Java](iot-hub-iot-edge-create-module-java.md)
#### [.NET Framework](https://github.com/Azure-Samples/iot-edge-samples#how-to-run-the-net-module-sample-windows-10)
#### [.NET Standard](iot-hub-iot-edge-create-module-dotnet-core.md)
#### [Node.JS](iot-hub-iot-edge-create-module-js.md)
### Créer
#### [.NET Framework](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample)
#### [Module .NET Core](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_core_module_sample)
#### [Passerelle gérée .NET Core](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_core_managed_gateway)
#### [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample)
#### [Node.JS](https://github.com/Azure/iot-edge/tree/master/samples/nodejs_simple_sample)
#### [Ajouter le module de manière dynamique](https://github.com/Azure/iot-edge/tree/master/samples/dynamically_add_module_sample)
#### [Module proxy hors processus](https://github.com/Azure/iot-edge/tree/master/samples/proxy_sample)
#### [Hôte de module natif](https://github.com/Azure/iot-edge/tree/master/samples/native_module_host_sample)

# Référence
## [Exemples de code](https://azure.microsoft.com/en-us/resources/samples/?service=iot-hub)
## [Interface de ligne de commande Azure](/cli/azure/iot)
## [.NET (service)](/dotnet/api/microsoft.azure.devices)
## [.NET (appareils)](/dotnet/api/microsoft.azure.devices.client)
## [Java (service)](/java/api/com.microsoft.azure.sdk.iot.service)
## [Java (appareils)](/java/api/com.microsoft.azure.sdk.iot.device)
## [Kits de développement logiciel (SDK) Node.js](http://azure.github.io/azure-iot-sdk-node/)
## [SDK d’appareils C](https://azure.github.io/azure-iot-sdk-c/index.html)
## [Azure IoT Edge](http://azure.github.io/iot-edge/)
## [REST (fournisseur de ressources)](https://docs.microsoft.com/rest/api/iothub/iothubresource)
## [REST (identités des appareils)](https://docs.microsoft.com/rest/api/iothub/deviceapi)
## [Représentations d’appareil physique](https://docs.microsoft.com/rest/api/iothub/devicetwinapi)
## [REST (messagerie des appareils)](https://docs.microsoft.com/rest/api/iothub/httpruntime)
## [REST (tâches)](https://docs.microsoft.com/rest/api/iothub/jobapi)

# Rubriques connexes
## [Azure IoT Suite](https://azure.microsoft.com/documentation/suites/iot-suite/)
## [Azure Event Hubs](https://azure.microsoft.com/documentation/services/event-hubs/)
## [Stream Analytics](https://azure.microsoft.com/documentation/services/stream-analytics/)
## [Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/)

# Ressources
## [Catalogue d’appareils certifiés Azure pour l’IoT](https://catalog.azureiotsuite.com/)
## [Centre de développement Azure IoT](https://azure.microsoft.com/develop/iot/)
## [Feuille de route Azure](https://azure.microsoft.com/roadmap/?category=internet-of-things)
## [Outil DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)
## [Outil iothub-diagnostics](https://github.com/Azure/iothub-diagnostics)
## [Outil iothub-explorer](https://github.com/Azure/iothub-explorer)
## [Parcours d’apprentissage](https://azure.microsoft.com/documentation/learning-paths/iot-hub/)
## [Forum MSDN](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azureiothub)
## [Tarification](https://azure.microsoft.com/pricing/details/iot-hub/)
## [Calculatrice de prix](https://azure.microsoft.com/pricing/calculator/)
## [Mises à jour de service](https://azure.microsoft.com/updates/?product=iot-hub)
## [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-iot-hub)
## [Études de cas techniques](https://microsoft.github.io/techcasestudies/#technology=IoT&sortBy=featured)
## [Vidéos](https://azure.microsoft.com/documentation/videos/index/?services=iot-hub)
