# <a name="secure-your-iot-deployment"></a>Sécuriser votre déploiement IoT
Cet article fournit un niveau de détail suivant de hello pour la sécurisation de l’infrastructure de base Azure IoT Internet of Things (IoT) hello. Elle lie les détails de niveau tooimplementation pour la configuration et de déploiement de chaque composant. Il fournit également des comparaisons et des choix entre les différentes méthodes.

Sécurisation du déploiement d’Azure IoT hello peut être divisé en hello suivant trois zones de sécurité :

* **Sécurité des appareils**: hello IoT DISPOSITIF pendant qu’il est déployé dans hello générique.
* **Sécurité de connexion**: toutes les données transmises entre les appareils IoT de hello et IoT Hub est confidentiel et de toute falsification.
* **Sécurité de cloud computing**: en fournissant un moyen toosecure données pendant parcourt, puis il est stocké dans le cloud de hello.

![Trois zones de sécurité][img-overview]

## <a name="secure-device-provisioning-and-authentication"></a>Approvisionnement et authentification sécurisés des appareils
Bonjour Azure IoT Suite sécurise les appareils IoT par hello deux méthodes suivantes :

* En fournissant une clé d’identité unique (les jetons de sécurité) pour chaque périphérique, qui peut être utilisé par toocommunicate de périphérique hello avec hello IoT Hub.
* À l’aide d’un appareil [certificat X.509] [ lnk-x509] et la clé privée comme un toohello de périphérique signifie tooauthenticate hello IoT Hub. Cette méthode d’authentification permet de s’assurer que hello clé privée sur l’appareil de hello ne connaît pas en dehors de l’appareil de hello à tout moment, en fournissant un niveau de sécurité plus élevé.

méthode de jeton de sécurité Hello fournit l’authentification pour chaque appel effectué par hello appareil tooIoT Hub en associant l’appel de tooeach clé symétrique hello. L’authentification basée sur X.509 permet l’authentification d’une unité IoT au niveau de la couche physique de hello dans le cadre de l’établissement d’une connexion TLS hello. méthode de base de jetons de sécurité de Hello peut être utilisée sans l’authentification hello X.509 qui est un modèle moins sécurisé. Hello choix entre les méthodes hello deux est principalement dictée par hello sécurisé a besoin de l’authentification des appareils toobe et la disponibilité de stockage sécurisé sur l’appareil de hello (toostore hello en toute sécurité une clé privée).

## <a name="iot-hub-security-tokens"></a>Jetons de sécurité IoT Hub
IoT Hub utilise la sécurité des jetons tooauthenticate appareils et services tooavoid envoi de clés sur le réseau de hello. En outre, la validité et la portée des jetons sont limitées dans le temps. Les Kits de développement logiciel (SDK) Azure IoT Hub génèrent automatiquement les jetons sans configuration spéciale. Certains scénarios, cependant, nécessitent hello utilisateur toogenerate et utilisent directement les jetons de sécurité. Citons notamment une utilisation directe des surfaces MQTT, AMQP ou HTTP hello hello ou implémentation hello hello jeton du modèle de service.

Vous trouverez plus d’informations sur la structure de hello du jeton de sécurité hello et son utilisation dans hello suivant des articles :

* [Structure du jeton de sécurité][lnk-security-tokens]
* [Utilisation de jetons SAP comme appareil][lnk-sas-tokens]

Chaque IoT Hub a un [Registre des identités] [ lnk-identity-registry] qui peut être utilisé toocreate par périphérique ressources hello service, comme une file d’attente qui contient des messages cloud-à-appareil et en vol et tooallow accès toohello points de terminaison de périphérique. Hello Registre des identités IoT Hub fournit le stockage sécurisé des identités des appareils et des clés de sécurité pour une solution. Individuelles ou des groupes d’identités d’appareil peuvent être ajoutés tooan autorise la liste ou une liste de blocs, l’activation du contrôle total sur l’accès à l’appareil. Hello articles suivants fournissent plus de détails sur la structure de hello du Registre des identités hello et opérations prises en charge.

[IoT Hub prend en charge les protocoles tels que MQTT, AMQP, and HTTP][lnk-protocols]. Chacun de ces protocoles utilisent des jetons de sécurité à partir de tooIoT de périphérique hello IoT Hub différemment :

* AMQP : SASL simple et basée sur les revendications AMQP la sécurité ({stratégie}@sas.root. {} iothubName} dans les cas de hello de jetons d’au niveau du hub IoT ; {deviceId} en cas de l’appareil de portée des jetons).
* MQTT : Connecter des utilisations de paquet {deviceId} comme hello {ClientId}, {IoThubhostname} / {deviceId} Bonjour **nom d’utilisateur** champ et une SAP de jeton Bonjour **mot de passe** champ.
* HTTP : Jeton valide est dans l’en-tête de demande d’autorisation hello.

Registre des identités IoT Hub peut être des informations d’identification de sécurité tooconfigure utilisé par périphérique et le contrôle d’accès. Cependant, si une solution IoT représente déjà un investissement significatif dans un [registre d’identité des appareils personnalisé et/ou un schéma d’authentification][lnk-custom-auth], vous pouvez intégrer cette infrastructure existante à IoT Hub en créant un service de jeton.

### <a name="x509-certificate-based-device-authentication"></a>Authentification des appareils basée sur un certificat X.509
Hello d’utilisation d’un [basée sur l’appareil un certificat X.509] [ lnk-use-x509] et sa paire de clés privée et publique associée permet une authentification supplémentaire au niveau de la couche physique de hello. clé privée de Hello est stocké en toute sécurité dans le dispositif de hello et n’est pas détectable en dehors de l’appareil de hello. certificat X.509 de Hello contient plus d’informations sur l’appareil hello, telles que les ID de périphérique et d’autres détails d’organisation. Une signature de certificat de hello est générée à l’aide de clé privée de hello.

Flux d’approvisionnement des appareils de haut niveau :

* Associer un identificateur tooa périphérique physique : identité de l’appareil et/ou par appareil de toohello associé de certificat X.509 au cours de l’unité de fabrication ou de mise en service.
* Créer une entrée d’identité correspondante dans IoT Hub – identité de l’appareil et les informations de périphérique associé Bonjour Registre des identités IoT Hub.
* Stocker en toute sécurité l’empreinte numérique du certificat X.509 dans le Registre d’identité IoT Hub.

### <a name="root-certificate-on-device"></a>Certificat racine sur un appareil
Lors de l’établissement d’une connexion TLS sécurisée avec IoT Hub, appareils IoT de hello authentifie IoT Hub à l’aide d’un certificat racine qui fait partie de l’appareil hello SDK. Pour que le client hello C SDK hello est situé sous le dossier de hello »\\c\\certificats » sous la racine hello de dépôt de hello. Bien que ces certificats racine soient de longue durée, ils peuvent malgré tout expirer ou être révoqués. S’il n’existe aucun moyen de mise à jour hello certificat sur l’appareil de hello, hello périphérique ne peut pas être en mesure de toosubsequently connecter toohello IoT Hub (ou tout autre service cloud). Avoir un certificat racine de moyens tooupdate hello une fois déployé appareils IoT de hello réduire de manière efficace ce risque.

## <a name="securing-hello-connection"></a>Sécurisation de connexion de hello
Connexion Internet entre appareils IoT de hello et IoT Hub est sécurisée à l’aide de la norme de sécurité TLS (Transport Layer) hello. Azure IoT prend en charge [TLS 1.2][lnk-tls12], TLS 1.1 et TLS 1.0, dans cet ordre. La prise en charge de TLS 1.0 est fournie uniquement à des fins de compatibilité descendante. Il est recommandé de toouse TLS 1.2 puisqu’il fournit hello plus de sécurité.

Azure IoT Suite prend en charge hello suivant des Suites de chiffrement, dans cet ordre.

| Suite de chiffrement | Longueur |
| --- | --- |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA384 (0xc028) ECDH secp384r1 (eq. 7680 bits RSA) FS |256 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0xc027) ECDH secp256r1 (eq. 3072 bits RSA) FS |128 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA (0xc014) ECDH secp384r1 (eq. 7680 bits RSA) FS |256 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA (0xc013) ECDH secp256r1 (eq. 3072 bits RSA) FS |128 |
| TLS\_RSA\_WITH\_AES\_256\_GCM\_SHA384 (0x9d) |256 |
| TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256 (0x9c) |128 |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA256 (0x3d) |256 |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0x3c) |128 |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA (0x35) |256 |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA (0x2f) |128 |
| TLS\_RSA\_WITH\_3DES\_EDE\_CBC\_SHA (0xa) |112 |

## <a name="securing-hello-cloud"></a>Sécurisation de cloud de hello
Azure IoT Hub permet la définition de [stratégies de contrôle d’accès][lnk-protocols] pour chaque clé de sécurité. Il utilise hello ensemble suivant d’autorisations toogrant accès tooeach de points de terminaison de IoT Hub. Autorisations limitent tooan d’accès hello Qu'iot Hub basé sur la fonctionnalité.

* **RegistryRead**. Registre des identités toohello accorde un accès en lecture. Pour plus d’informations, consultez la rubrique dédiée au [registre des identités][lnk-identity-registry].
* **RegistryReadWrite**. Octroie accès en lecture et écriture toohello Registre des identités. Pour plus d’informations, consultez la rubrique dédiée au [registre des identités][lnk-identity-registry].
* **ServiceConnect**. Octroie accéder toocloud service orientées communication et la surveillance des points de terminaison. Par exemple, il accorde hello récupérer correspondant des accusés de réception de remise des messages appareil-à-cloud autorisation tooback-fin cloud services tooreceive et envoyer des messages cloud-à-appareil.
* **DeviceConnect**. Octroie accéder aux points de terminaison toodevice accessibles. Par exemple, il accorde l’autorisation des messages appareil-à-cloud toosend et recevoir des messages cloud-à-appareil. Cette autorisation est utilisée par les appareils.

Il existe deux façons tooobtain **DeviceConnect** autorisations avec IoT Hub avec [les jetons de sécurité][lnk-sas-tokens]: à l’aide d’une clé d’identité de périphérique, ou une clé d’accès partagé. En outre, il est important toonote toutes les fonctionnalités accessibles à partir d’appareils exposé par la conception sur les points de terminaison avec le préfixe `/devices/{deviceId}`.

[Composants de service peuvent uniquement créer des jetons de sécurité] [ lnk-service-tokens] à l’aide des stratégies d’accès l’octroi d’autorisations approprié de hello partagé.

IoT Hub Azure et autres services qui peuvent faire partie d’une solution de hello autoriser la gestion des utilisateurs à l’aide de hello Azure Active Directory.

Les données reçues par Azure IoT Hub peuvent être utilisées par une variété de services comme Azure Stream Analytics et le stockage d’objets blob. Ces services permettent un accès en gestion. En savoir plus sur ces services et les options disponibles ci-dessous :

* [Azure DocumentDB][lnk-docdb]: un service de base de données évolutives et entièrement indexés pour des données semi-structurées qui gère les métadonnées pour les appareils hello vous configurez, telles que des attributs, la configuration et les propriétés de sécurité. DocumentDB assure un traitement hautes performances et à débit élevé, ainsi qu’une indexation des données indépendante du schéma. Ce service offre également une interface de requête SQL enrichie.
* [Analytique de flux de données Azure][lnk-asa]: flux en temps réel de traitement dans le cloud hello toorapidly vous permet de développer et déployer un informations économiques analytique solution toouncover en temps réel à partir d’appareils, capteurs, infrastructure et les applications. les données de salutation à partir de ce service entièrement géré peuvent évoluer tooany volume tout en atteignant un débit élevé, une latence faible et résilience.
* [Services d’application Azure][lnk-appservices]: un cloud platform toobuild puissantes applications web et mobiles qui se connectent toodata n’importe où ; dans le cloud de hello ou localement. Créez des applications mobiles attrayantes pour iOS, Android et Windows. Intégrer avec votre logiciel comme un Service (SaaS) et d’entreprise des applications avec toodozens out of box connectivité des services basés sur le cloud et applications d’entreprise. Le code dans votre langage favori et l’IDE et les applications web toobuild (.NET, Node.js, PHP, Python ou Java) et API plus rapidement qu’auparavant.
* [Logique d’applications][lnk-logicapps]: fonctionnalité de Logic Apps hello du Service d’applications Azure permet d’intégrer vos systèmes métier-IoT solution tooyour existants et d’automatiser les processus de flux de travail. Logique d’applications permet aux développeurs toodesign des flux de travail qui démarrent à partir d’un déclencheur, puis exécutent une série d’étapes, les règles et les actions qui utilisent des connecteurs puissant toointegrate avec vos processus d’entreprise. Logique d’applications offre d’emploi connectivité tooa vaste écosystème de SaaS, basé sur le cloud et des applications sur site.
* [Stockage d’objets blob Azure][lnk-blob]: stockage cloud fiable et économique pour les données hello que vos appareils envoient toohello cloud.

## <a name="conclusion"></a>Conclusion
Cet article fournit une vue d’ensemble des détails au niveau de l’implémentation pour concevoir et déployer une infrastructure IoT à l’aide d’Azure IoT. Configuration de chaque composant toobe sécurisée est la clé pour la sécurisation de hello infrastructure IoT globale. le choix de conception Hello disponible dans Azure IoT permettent un certain degré de souplesse et de choix ; Toutefois, chaque choix peut avoir des implications de sécurité. Nous vous recommandons d’évaluer chacun de ces choix à l’aide d’une évaluation des risques et du coût.

[img-overview]: media/iot-secure-your-deployment/overview.png

[lnk-security-tokens]: ../articles/iot-hub/iot-hub-devguide-security.md#security-token-structure
[lnk-sas-tokens]: ../articles/iot-hub/iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-identity-registry]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-protocols]: ../articles/iot-hub/iot-hub-devguide-security.md
[lnk-custom-auth]: ../articles/iot-hub/iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: http://www.itu.int/rec/T-REC-X.509-201210-I/en
[lnk-use-x509]: ../articles/iot-hub/iot-hub-devguide-security.md
[lnk-tls12]: https://tools.ietf.org/html/rfc5246
[lnk-service-tokens]: ../articles/iot-hub/iot-hub-devguide-security.md#use-security-tokens-from-service-components
[lnk-docdb]: https://azure.microsoft.com/services/documentdb/
[lnk-asa]: https://azure.microsoft.com/services/stream-analytics/
[lnk-appservices]: https://azure.microsoft.com/services/app-service/
[lnk-logicapps]: https://azure.microsoft.com/services/app-service/logic/
[lnk-blob]: https://azure.microsoft.com/services/storage/
