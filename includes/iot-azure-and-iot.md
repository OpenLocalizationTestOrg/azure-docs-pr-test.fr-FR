
# <a name="azure-and-internet-of-things"></a>Azure et IoT

Bienvenue dans tooMicrosoft Azure et hello Internet of Things (IoT). Cet article présente une architecture de solution IoT qui décrit des caractéristiques communes hello d’une solution IoT que vous pouvez déployer à l’aide des services Azure. IoT solutions nécessitent sécuriser, communication bidirectionnelle entre les appareils, éventuellement numérotation hello millions et un principal de la solution. Par exemple, un principal de la solution peut utiliser des analytique automatisés, prédictive toouncover insights de votre flux d’événements de l’appareil-à-cloud.

Azure IoT Hub est la clé de voûte de l’implémentation de cette architecture de solution IoT au moyen de services Azure. IoT Suite assure des implémentations complètes de bout en bout de cette architecture pour des scénarios IoT spécifiques. Par exemple :

* Hello *surveillance à distance* solution permet d’état de hello toomonitor des périphériques tels que des distributeurs automatiques.
* Hello *maintenance prédictive* solution vous aide à tooanticipate les besoins de gestion des périphériques tels que des pompes de stations pompage à distance et les temps d’arrêt non planifié de tooavoid.
* Hello *fabrique connecté* solution vous aide à tooconnect et surveillez vos appareils industriels.

## <a name="iot-solution-architecture"></a>Architecture de solution IoT

Hello suivant schéma montre une architecture de solution IoT standard. diagramme de Hello n’inclut pas les noms de hello des services Azure spécifiques, mais décrit hello des éléments clés dans une architecture de solution IoT générique. Dans cette architecture, appareils IoT collectant les données qu’ils envoient tooa la passerelle de cloud. passerelle de cloud Hello rend les données hello disponibles pour le traitement par d’autres services principaux à partir d’où les données sont fournies les applications métier-tooother ou opérateurs toohuman via un tableau de bord ou un autre périphérique de présentation.

![Architecture de solution IoT][img-solution-architecture]

> [!NOTE]
> Pour une discussion détaillée de l’architecture de IoT, consultez hello [Architecture de référence de Microsoft Azure IoT][lnk-refarch].

### <a name="device-connectivity"></a>Connectivité des appareils

Dans cette architecture de solution IoT, appareils envoient la télémétrie, tels que les lectures des capteurs à partir d’une station pompage, le point de terminaison tooa cloud pour le stockage et le traitement. Dans un scénario de maintenance prédictive hello solution back-end peut-être utiliser des flux de hello de toodetermine de données de capteur lorsqu’une pompe spécifique requiert une maintenance. Appareils peuvent également recevoir et répondre messages toocloud-à-appareil par la lecture de messages à partir d’un point de terminaison du cloud. Par exemple, dans la solution de hello du scénario de maintenance prédictive hello back-end peut envoyer des messages tooother pompes Bonjour pompage toobegin station du réacheminement de flux juste avant l’échéance maintenance toostart. Cette procédure Assurez-vous ingénieur de maintenance hello pourrait commencer dès qu’elle arrive.

Un des hello plus grands défis pour les projets IoT est comment tooreliably et connectez-vous en toute sécurité des appareils toohello solution back-end. Appareils IoT ont des caractéristiques différentes en tant que clients comparés tooother tels que des navigateurs et des applications mobiles. Les appareils IoT :

* sont souvent des systèmes intégrés, qui ne font appel à aucun opérateur humain ;
* peuvent être déployés sur des sites distants avec un accès physique coûteux ;
* Peut être uniquement accessible via une hello solution back-end. Il n’existe aucune autre toointeract façon avec les appareils hello.
* peuvent avoir des performances et/ou des ressources de traitement limitées ;
* peuvent avoir une connectivité réseau intermittente, lente ou coûteuse ;
* Protocoles d’application propriétaire, personnalisées ou spécifiques au secteur toouse peut-être.
* peuvent être créés à l’aide d’un large éventail de plateformes matérielles et logicielles populaires.

En outre toohello les spécifications ci-dessus, n’importe quelle solution IoT doit également fournir l’échelle, la sécurité et fiabilité. Bonjour ensemble d’exigences de connectivité résultant est tooimplement et complexe à l’aide de technologies traditionnelles telles que les conteneurs de web et courtiers de messagerie. Azure IoT Hub et hello kits de développement logiciel Azure IoT périphérique rendent plus faciles solutions tooimplement qui répondent à ces exigences.

Un périphérique peut communiquer directement avec un point de terminaison de passerelle de cloud, ou si l’appareil de hello ne peut pas utiliser un des protocoles de communication hello hello prend en charge de passerelle de cloud, il peut se connecter via une passerelle intermédiaire. Par exemple, hello [passerelle de protocole Azure IoT] [ lnk-protocol-gateway] peut effectuer traduction de protocole si les périphériques ne peut pas utiliser un des protocoles hello IoT Hub prend en charge.

### <a name="data-processing-and-analytics"></a>Traitement et analyse des données

Dans le cloud de hello, un principal de solution IoT constitue la plupart hello du traitement des données, telles que le filtrage et l’agrégation de télémétrie et de leur routage tooother services. Hello principal IoT solution :

* Reçoit les données de télémétrie à grande échelle à partir de vos appareils et détermine comment tooprocess et stocker ces données. 
* Peut vous permettre de commandes toosend hello cloud toospecific appareil.
* Fournit des fonctionnalités de l’inscription des appareils qui vous tooprovision périphériques et toocontrol les appareils qui sont autorisés à tooconnect tooyour infrastructure.
* Permet de vous tootrack hello l’état de vos appareils et contrôler leurs activités.

Dans le scénario de maintenance prédictive hello, hello solution back-end stocke les données de télémétrie historiques. Hello solution back-end permet cette données toouse tooidentify des modèles qui indiquent la maintenance est due à une pompe spécifique.

Les solutions IoT peuvent inclure des boucles de rétroaction automatique. Par exemple, un module d’analytique dans hello solution back-end peut identifier à partir de la télémétrie température hello d’un périphérique spécifique est supérieure à des niveaux de fonctionnement normales. solution de Hello peut alors envoyer un périphérique toohello de commande, lui indiquant une action corrective tootake.

### <a name="presentation-and-business-connectivity"></a>Présentation et connectivité d’entreprise

couche de connectivité de présentation et entreprise Hello permet aux utilisateurs finaux toointeract avec hello solution IoT et les appareils hello. Il permet aux utilisateurs tooview et analyser les données hello collectées à partir de leurs appareils. Ces vues peuvent prendre la forme hello de tableaux de bord ou rapports BI qui peuvent afficher des données historiques ou à proximité des données en temps réel. Par exemple, un opérateur peut vérifier état hello de station de pompage particulier et voir les alertes déclenchées par le système de hello. Cette couche permet également une intégration de hello IoT solution principale avec des tootie line-of-business applications existantes dans le processus d’entreprise ou des flux de travail. Par exemple, hello maintenance prédictive solution peut s’intégrer avec un système de planification que la documentation un toovisit ingénieur une station pompage lors de la solution de hello identifie une pompe ayant besoin de maintenance.

![Tableau de bord de solution IoT][img-dashboard]

[img-solution-architecture]: ./media/iot-azure-and-iot/iot-reference-architecture.png
[img-dashboard]: ./media/iot-azure-and-iot/iot-suite.png

[lnk-machinelearning]: http://azure.microsoft.com/documentation/services/machine-learning/
[Azure IoT Suite]: http://azure.microsoft.com/solutions/iot
[lnk-protocol-gateway]:  ../articles/iot-hub/iot-hub-protocol-gateway.md
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
