---
title: "aaaUnderstand sécurité d’Azure IoT Hub | Documents Microsoft"
description: "Guide de développeur - comment toocontrol aux tooIoT Hub pour les applications de périphérique et les applications de back-end. Inclut des informations sur les jetons de sécurité et la prise en charge des certificats X.509."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 45631e70-865b-4e06-bb1d-aae1175a52ba
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 717726328a6bb5c5c334a123d0abfed711b2c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="control-access-tooiot-hub"></a>Contrôle l’accès tooIoT Hub

Cet article décrit les options de hello pour sécuriser votre hub IoT. IoT Hub utilise *autorisations* point de terminaison toogrant accès tooeach IoT hub. Autorisations limitent hub IoT hello accès tooan sont basée sur fonctionnalité.

Cet article explique :

* Hello différentes autorisations que vous pouvez accorder tooa appareil ou applications principal tooaccess votre hub IoT.
* Bonjour processus et hello les jetons d’authentification qu’il utilise des autorisations de tooverify.
* Comment tooscope les informations d’identification de toospecific toolimit accéder aux ressources.
* La prise en charge par IoT Hub des certificats X.509.
* Les mécanismes d’authentification d’appareil personnalisés qui utilisent des registres d’identités d’appareil ou des schémas d’authentification existants.

### <a name="when-toouse"></a>Lorsque toouse

Vous devez disposer des autorisations appropriées tooaccess un des points de terminaison IoT Hub hello. Par exemple, un appareil doit inclure un jeton contenant des informations d’identification de sécurité, ainsi que tous les messages qu’il envoie tooIoT Hub.

## <a name="access-control-and-permissions"></a>Contrôle d’accès et autorisations

Vous pouvez accorder [autorisations](#iot-hub-permissions) Bonjour suivant façons :

* **Stratégies d’accès partagé au niveau d’IoT Hub**. Les stratégies d’accès partagé peuvent accorder n’importe quelle combinaison d’[autorisations](#iot-hub-permissions). Vous pouvez définir des stratégies dans hello [portail Azure][lnk-management-portal], ou par programme à l’aide de hello [fournisseur de ressources IoT Hub API REST][lnk-resource-provider-apis]. Un hub IoT nouvellement créé a hello suivant des stratégies par défaut :

  * **iothubowner**: stratégie jouissant de toutes les autorisations.
  * **service** : stratégie jouissant de l’autorisation **ServiceConnect**.
  * **device** : stratégie jouissant de l’autorisation **DeviceConnect**.
  * **registryRead** : stratégie jouissant de l’autorisation **RegistryRead**.
  * **registryReadWrite** : stratégie jouissant des autorisations **RegistryRead** et RegistryWrite.
  * **Informations d’identification de sécurité par appareil**. Chaque hub IoT contient un [registre des identités][lnk-identity-registry]. Pour chaque périphérique dans le Registre des identités, vous pouvez configurer les informations d’identification de sécurité qui accorde **DeviceConnect** autorisations étendue des points de terminaison de périphérique correspondant toohello.

Par exemple, dans une solution IoT classique :

* composant de gestion de périphérique Hello utilise hello *registryReadWrite* stratégie.
* composant processeur d’événements Hello utilise hello *service* stratégie.
* composant de la logique d’entreprise Hello appareil de l’exécution utilise hello *service* stratégie.
* Périphériques individuels se connectent à l’aide des informations d’identification stockées dans le Registre des identités de concentrateur hello IoT.

> [!NOTE]
> Pour plus d’informations, consultez la page [Autorisations](#iot-hub-permissions).

## <a name="authentication"></a>Authentification

IoT Hub Azure accorde l’accès tooendpoints en vérifiant un jeton par rapport aux stratégies d’accès partagé de hello et identification de sécurité du Registre.

Informations d’identification de sécurité, telles que des clés symétriques, ne sont jamais envoyées acheminement hello.

> [!NOTE]
> Hello fournisseur de ressources Azure IoT Hub est sécurisé via votre abonnement Azure, sont tous les fournisseurs hello [Azure Resource Manager][lnk-azure-resource-manager].

Pour plus d’informations sur la façon tooconstruct et l’utilisation des jetons de sécurité, consultez [des jetons de sécurité IoT Hub][lnk-sas-tokens].

### <a name="protocol-specifics"></a>Spécifications de protocole

Chaque protocole pris en charge (par exemple, MQTT, AMQP et HTTP) transporte des jetons de différentes façons.

Lorsque vous utilisez MQTT, paquet de connexion hello a hello deviceId comme hello ClientId, {iothubhostname} / {deviceId} dans le champ de nom d’utilisateur hello et un jeton SAS dans le champ de mot de passe hello. {iothubhostname} doit être hello complète CName hello IoT hub (par exemple, contoso.azure devices.net).

Lorsque vous utilisez [AMQP][lnk-amqp], IoT Hub prend en charge [SASL PLAIN][lnk-sasl-plain] et la [sécurité basée sur des revendications AMQP][lnk-cbs].

Spécifie de hello standard si vous utilisez AMQP revendications--sécurité, comment tootransmit ces jetons.

Pour SASL brut, hello **nom d’utilisateur** peut être :

* `{policyName}@sas.root.{iothubName}` si vous utilisez des jetons au niveau du hub IoT.
* `{deviceId}@sas.{iothubname}` si vous utilisez des jetons à l’échelle de l’appareil.

Dans les deux cas, les champs de mot de passe hello contient le jeton de hello, comme décrit dans [des jetons de sécurité IoT Hub][lnk-sas-tokens].

HTTP implémente l’authentification en incluant un jeton valide Bonjour **autorisation** en-tête de demande.

#### <a name="example"></a>Exemple

Nom d’utilisateur (DeviceId respecte la casse) : `iothubname.azure-devices.net/DeviceId`

Mot de passe (jeton SAS de générer avec hello [Explorateur de périphérique] [ lnk-device-explorer] outil) :`SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`

> [!NOTE]
> Hello [kits de développement logiciel Azure IoT] [ lnk-sdks] générer automatiquement des jetons lors de la connexion toohello service. Dans certains cas, hello kits de développement logiciel Azure IoT ne gèrent pas tous les protocoles hello ou toutes les méthodes d’authentification hello.

### <a name="special-considerations-for-sasl-plain"></a>Considérations spécifiques concernant SASL PLAIN

Lorsque vous utilisez SASL brut avec AMQP, un client se connectant tooan IoT hub peut utiliser un jeton unique pour chaque connexion TCP. Lors de l’expiration du jeton de hello, hello connexion TCP se déconnecte de service de hello et déclenche une reconnexion. Ce comportement, pendant pas problématique pour une application back-end, endommager pour une application de périphérique pour hello suivant raisons :

* Les passerelles se connectent généralement au nom de nombreux appareils. Lorsque vous utilisez SASL brut, ils ont toocreate une connexion TCP distincte pour chaque périphérique se connectant tooan IoT hub. Ce scénario considérablement augmente la consommation de puissance et de ressources réseau hello et augmente la latence hello de chaque connexion de périphérique.
* Périphériques ressources limitées sont affectées à l’aide de hello augmentée de ressources tooreconnect après chaque d’expiration du jeton.

## <a name="scope-iot-hub-level-credentials"></a>Étendue des informations d’identification au niveau du hub IoT

Vous pouvez étendre les stratégies de sécurité au niveau du hub IoT en créant des jetons avec un URI de ressource restreint. Par exemple, les messages appareil-à-cloud toosend du point de terminaison hello à partir d’un appareil est **/devices/ {deviceId} / messages/événements**. Vous pouvez également utiliser une stratégie d’un accès partagé au niveau du hub IoT avec **DeviceConnect** toosign d’autorisations dont resourceURI est un jeton de **/devices/ {deviceId}**. Cette approche crée un jeton qui est uniquement des messages toosend utilisable pour le compte d’appareil **deviceId**.

Ce mécanisme est semblable toohello [stratégie d’éditeur de concentrateurs d’événements][lnk-event-hubs-publisher-policy]et vous permet de méthodes d’authentification personnalisée tooimplement.

## <a name="security-tokens"></a>Jetons de sécurité

IoT Hub utilise la sécurité jetons tooauthenticate appareils et services tooavoid envoi de clés sur le câble de hello. En outre, la validité et la portée des jetons sont limitées dans le temps. Les kits [Azure IoT SDK ][lnk-sdks] génèrent automatiquement les jetons sans configuration spéciale. Certains scénarios nécessitent toogenerate et utiliser directement les jetons de sécurité. Il s’agit entre autres des scénarios suivants :

* utilisation directe de Hello des surfaces MQTT, AMQP ou HTTP hello.
* Hello d’implémentation du modèle de service de jeton de hello, comme expliqué dans [l’authentification des appareils personnalisé][lnk-custom-auth].

IoT Hub autorise également les périphériques tooauthenticate avec IoT Hub à l’aide de [certificats X.509][lnk-x509].

### <a name="security-token-structure"></a>Structure du jeton de sécurité

Vous utilisez sécurité jetons toogrant limités toodevices et services toospecific fonctionnalité d’accès dans IoT Hub. tooget d’autorisation tooconnect tooIoT Hub, appareils et services doivent envoyer des jetons de sécurité signés avec un accès partagé ou une clé symétrique. Ces clés sont stockées avec une identité d’appareil dans le Registre des identités hello.

Un jeton signé avec une accès partagé accorde clé tooall hello fonctionnalité d’accès associée aux autorisations de stratégie d’accès hello partagé. Un jeton signé avec hello d’accorde uniquement à clé symétrique d’une identité d’appareil **DeviceConnect** autorisation pour hello associé d’identité de l’appareil.

jeton de sécurité Hello a hello suivant le format :

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

Voici les valeurs attendues hello :

| Valeur | Description |
| --- | --- |
| {signature} |Une chaîne de signature de code HMAC-SHA256 sous forme de hello : `{URL-encoded-resourceURI} + "\n" + expiry`. **Important**: hello clé est décodée à partir de base64 et utilisée en tant que clé tooperform le calcul hello HMAC-SHA256. |
| {resourceURI} |Préfixe URI (par segment) des points de terminaison hello qui sont accessibles par ce jeton, en commençant par le nom d’hôte de hello IoT hub (aucun protocole). Par exemple, `myHub.azure-devices.net/devices/device1` |
| {expiry} |Chaînes UTF-8 pour le nombre de secondes écoulées depuis le 1er janvier 1970 hello époque 00:00:00 UTC. |
| {URL-encoded-resourceURI} |Faible cas encodage d’URL de l’URI de ressource hello minuscules |
| {policyName} |nom de Hello Hello partagé toowhich de stratégie d’accès que fait référence de ce jeton. Absent si le jeton de hello fait référence les informations d’identification de toodevice du Registre. |

**Remarque sur le préfixe**: préfixe URI de hello est calculé par segment et non par caractère. Par exemple `/a/b` est un préfixe de `/a/b/c`, mais pas de `/a/bc`.

Hello Node.js extrait de code suivant illustre une fonction appelée **generateSasToken** que calcule hello jeton à partir des entrées de hello `resourceUri, signingKey, policyName, expiresInMins`. les sections suivantes Hello décrit en détail comment tooinitialize hello différentes entrées pour le jeton différent de hello cas d’usage.

```nodejs
var generateSasToken = function(resourceUri, signingKey, policyName, expiresInMins) {
    resourceUri = encodeURIComponent(resourceUri);

    // Set expiration in seconds
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    expires = Math.ceil(expires);
    var toSign = resourceUri + '\n' + expires;

    // Use crypto
    var hmac = crypto.createHmac('sha256', new Buffer(signingKey, 'base64'));
    hmac.update(toSign);
    var base64UriEncoded = encodeURIComponent(hmac.digest('base64'));

    // Construct autorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
};
```

En comparaison, hello toogenerate de code Python équivalent qu'est d’un jeton de sécurité :

```python
from base64 import b64encode, b64decode
from hashlib import sha256
from time import time
from urllib import quote_plus, urlencode
from hmac import HMAC

def generate_sas_token(uri, key, policy_name, expiry=3600):
    ttl = time() + expiry
    sign_key = "%s\n%d" % ((quote_plus(uri)), int(ttl))
    print sign_key
    signature = b64encode(HMAC(b64decode(key), sign_key, sha256).digest())

    rawtoken = {
        'sr' :  uri,
        'sig': signature,
        'se' : str(int(ttl))
    }

    if policy_name is not None:
        rawtoken['skn'] = policy_name

    return 'SharedAccessSignature ' + urlencode(rawtoken)
```

> [!NOTE]
> Étant donné que la validité du jeton de hello hello est validée sur les ordinateurs de IoT Hub, écarts hello horloge hello d’ordinateur hello qui génère les jetons hello doit être minime.

### <a name="use-sas-tokens-in-a-device-app"></a>Utiliser des jetons SPA dans une application d’appareil

Il existe deux façons tooobtain **DeviceConnect** autorisations avec IoT Hub avec des jetons de sécurité : utilisez un [clé symétrique de périphérique à partir du Registre des identités hello](#use-a-symmetric-key-in-the-identity-registry), ou utilisez un [cléd’accèspartagé](#use-a-shared-access-policy).

N’oubliez pas que toutes les fonctionnalités accessibles à partir des appareils sont exposées par définition sur les points de terminaison avec le préfixe `/devices/{deviceId}`.

> [!IMPORTANT]
> Hello seule façon que IoT Hub s’authentifie à un périphérique spécifique à l’aide de clé symétrique d’identité appareil hello. Dans le cas lorsqu’une stratégie d’accès partagé est une fonctionnalité d’appareil tooaccess utilisé, les solutions hello doivent prendre en compte composant hello émission de jeton de sécurité hello comme un sous-composant approuvé.

points de terminaison de périphérique Hello sont (quel que soit le protocole de hello) :

| Point de terminaison | Fonctionnalités |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |Envoyer des messages appareil-à-cloud. |
| `{iot hub host name}/devices/{deviceId}/devicebound` |Recevoir des messages cloud-à-appareil. |

### <a name="use-a-symmetric-key-in-hello-identity-registry"></a>Utiliser une clé symétrique dans le Registre des identités hello

Lorsque vous utilisez toogenerate clé symétrique un jeton d’identité d’un appareil, hello stratégie (`skn`) élément de jeton de hello est omis.

Par exemple, un jeton créé tooaccess toutes les fonctionnalités de l’appareil doit avoir hello paramètres suivants :

* URI de ressource : `{IoT hub name}.azure-devices.net/devices/{device id}`,
* clé de signature : une clé symétrique pour hello `{device id}` identité,
* pas de nom de stratégie,
* n’importe quelle heure d’expiration.

Un exemple d’utilisation hello précédant Node.js fonction serait :

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

résultat de Hello, qui accorde l’accès des fonctionnalités tooall pour appareil1, serait :

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> Il est possible de toogenerate un jeton SAP à l’aide de hello .NET [Explorateur de périphérique] [ lnk-device-explorer] outil ou hello inter-plateformes, basée sur le nœud [iothub-explorer] [ lnk-iothub-explorer] utilitaire de ligne de commande.

### <a name="use-a-shared-access-policy"></a>Utilisation d’une stratégie d’accès partagé

Lorsque vous créez un jeton à partir d’une stratégie d’accès partagé, définissez hello `skn` toohello nom du champ de la stratégie de hello. Cette stratégie doit accorder hello **DeviceConnect** autorisation.

Hello deux principaux scénarios pour l’utilisation de fonctionnalités du périphérique tooaccess accès partagé stratégies sont :

* [passerelles de protocole cloud][lnk-endpoints],
* [services de jeton] [ lnk-custom-auth] utilisé tooimplement des schémas d’authentification personnalisés.

Depuis hello stratégie d’accès partagé peut potentiellement accorder l’accès tooconnect n’importe quel appareil, qu'il s’agit des URI de ressource correct hello toouse important lors de la création de jetons de sécurité. Ce paramètre est particulièrement important pour les services de jeton, qui présentent le périphérique spécifique tooscope hello tooa jeton à l’aide d’URI de ressource hello. Ce point est moins important pour les passerelles de protocole, car elles interceptent déjà le trafic pour tous les appareils.

Par exemple, un service de jeton à l’aide de hello créé au préalable partagé appelée stratégie d’accès **périphérique** créerait un jeton avec hello paramètres suivants :

* URI de ressource : `{IoT hub name}.azure-devices.net/devices/{device id}`,
* clé de signature : une des clés de hello Hello `device` stratégie,
* nom de la stratégie : `device`,
* n’importe quelle heure d’expiration.

Un exemple d’utilisation hello précédant Node.js fonction serait :

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

résultat de Hello, qui accorde l’accès des fonctionnalités tooall pour appareil1, serait :

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

Une passerelle de protocole peut utiliser hello même jeton pour tous les appareils définissant simplement hello URI de ressource trop`myhub.azure-devices.net/devices`.

### <a name="use-security-tokens-from-service-components"></a>Utilisation de jetons de sécurité de composants du service

Composants de service peuvent uniquement générer des jetons de sécurité à l’aide de stratégies d’accès partagé accorde hello approprié comme expliqué précédemment.

Voici les fonctions de service hello exposées sur les points de terminaison hello :

| Point de terminaison | Fonctionnalités |
| --- | --- |
| `{iot hub host name}/devices` |Créer, mettre à jour, récupérer et supprimer les identités des appareils. |
| `{iot hub host name}/messages/events` |Recevoir des messages appareil-à-cloud. |
| `{iot hub host name}/servicebound/feedback` |Recevoir des commentaires pour les messages cloud-à-appareil. |
| `{iot hub host name}/devicebound` |Envoyer des messages cloud-à-appareil. |

Par exemple, un service de génération à l’aide de hello créé au préalable partagé appelée stratégie d’accès **registryRead** créerait un jeton avec hello paramètres suivants :

* URI de ressource : `{IoT hub name}.azure-devices.net/devices`,
* clé de signature : une des clés de hello Hello `registryRead` stratégie,
* nom de la stratégie : `registryRead`,
* n’importe quelle heure d’expiration.

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

résultat de Hello, qui vous accordez l’accès tooread toutes les identités d’appareil, serait :

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a>Certificats X.509 pris en charge

Vous pouvez utiliser n’importe quel tooauthenticate de certificat X.509 un périphérique avec IoT Hub. Les certificats incluent :

* **un certificat X.509 existant**. Un appareil peut être déjà associé à un certificat X.509. Appareil de Hello peut utiliser des tooauthenticate de ce certificat avec IoT Hub.
* **un certificat X-509 généré et signé automatiquement**. Un fabricant ou le responsable du déploiement en interne peut générer ces certificats et stocker la clé privée hello (et les certificats) sur l’appareil de hello. Vous pouvez utiliser des outils tels que [OpenSSL][lnk-openssl] ou l’utilitaire [Windows SelfSignedCertificate][lnk-selfsigned] à cette fin ;
* **un certificat X.509 signé par une autorité de certification**. tooidentify un appareil et de son authentification avec IoT Hub, vous pouvez utiliser un certificat X.509 généré et signé par une autorité de Certification (CA). IoT Hub vérifie uniquement que l’empreinte numérique hello présentée correspond à l’empreinte numérique hello configuré. IotHub ne valide pas la chaîne de certificats hello.

Un appareil peut utiliser un certificat X.509 ou un jeton de sécurité pour l’authentification, mais pas les deux.

### <a name="register-an-x509-certificate-for-a-device"></a>Inscrire un certificat X.509 pour un appareil

Hello [Azure IoT Service SDK pour c#] [ lnk-service-sdk] (version 1.0.8+) prend en charge l’inscription d’un périphérique qui utilise un certificat X.509 pour l’authentification. D’autres API telles que l’importation/exportation d’appareils prennent également en charge les certificats X.509.

### <a name="c-support"></a>Prise en charge de C\#

Hello **RegistryManager** classe fournit un tooregister par programme un appareil. En particulier, hello **AddDeviceAsync** et **UpdateDeviceAsync** méthodes vous tooregister et mettre à jour un appareil Bonjour Registre des identités IoT Hub. Ces deux méthodes utilisent une instance **Device** comme entrée. Hello **périphérique** classe inclut une **authentification** propriété qui vous permet de toospecify principaux et secondaires X.509 empreintes numériques de certificat. l’empreinte numérique Hello représente un hachage SHA-1 du certificat X.509 de hello (stockée à l’aide du codage de DER binaire). Vous pouvez hello en spécifiant une empreinte numérique du principal ou une empreinte numérique secondaire ou les deux. Empreintes numériques de principales et secondaires sont toohandle pris en charge les scénarios de substitution de certificat.

> [!NOTE]
> IoT Hub ne requiert pas ou ne sont pas stocker le certificat X.509 hello entière, l’empreinte numérique hello uniquement.

Voici un exemple C\# tooregister d’extrait de code un périphérique à l’aide d’un certificat X.509 :

```csharp
var device = new Device(deviceId)
{
  Authentication = new AuthenticationMechanism()
  {
    X509Thumbprint = new X509Thumbprint()
    {
      PrimaryThumbprint = "921BC9694ADEB8929D4F7FE4B9A3A6DE58B0790B"
    }
  }
};
RegistryManager registryManager = RegistryManager.CreateFromConnectionString(deviceGatewayConnectionString);
await registryManager.AddDeviceAsync(device);
```

### <a name="use-an-x509-certificate-during-run-time-operations"></a>Utiliser un certificat X.509 pendant les opérations d’exécution

Hello [appareil Azure IoT SDK pour .NET] [ lnk-client-sdk] (version 1.0.11+) prend en charge hello de certificats X.509.

### <a name="c-support"></a>Prise en charge de C\#

Hello classe **DeviceAuthenticationWithX509Certificate** prend en charge hello la création de **DeviceClient** instances à l’aide d’un certificat X.509. certificat X.509 de Hello doit être au format PFX (également appelé PKCS #12) hello qui inclut la clé privée de hello.

Voici un exemple d’extrait de code :

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a>Authentification d'appareil personnalisée

Vous pouvez utiliser hello IoT Hub [Registre des identités] [ lnk-identity-registry] informations d’identification de sécurité de chaque appareil tooconfigure et contrôle d’accès à l’aide de [jetons] [ lnk-sas-tokens] . Si une solution IoT a déjà un schéma de Registre et/ou l’authentification d’identité personnalisée, envisagez de créer un *service de jeton* toointegrate cette infrastructure avec IoT Hub. De cette façon, vous pouvez utiliser d'autres fonctionnalités IoT dans votre solution.

Un service de jeton est un service cloud personnalisé. Il utilise un IoT Hub *stratégie d’accès partagé* avec **DeviceConnect** autorisations toocreate *étendue de périphérique* jetons. Ces jetons activer un hub IoT de périphérique tooconnect tooyour.

![Étapes du modèle de service de jeton de hello][img-tokenservice]

Les étapes principales hello hello jeton du modèle de service sont :

1. Créez une stratégie d’accès partagé IoT Hub avec des autorisations **DeviceConnect** pour votre hub IoT. Vous pouvez créer cette stratégie Bonjour [portail Azure] [ lnk-management-portal] ou par programme. service de jeton de Hello utilise cette stratégie toosign hello les jetons qu’il crée.
1. Quand un appareil doit tooaccess votre IoT hub, il demande un jeton signé à partir de votre service de jeton. Appareil de Hello avec peut s’authentifier votre identité d’appareil identité personnalisée Registre/authentification schéma toodetermine hello que service de jeton de hello utilise le jeton de hello toocreate.
1. service de jeton de Hello retourne un jeton. jeton Hello est créé à l’aide de `/devices/{deviceId}` en tant que `resourceURI`, avec `deviceId` en tant que périphérique hello en cours d’authentification. service de jeton de Hello utilise le jeton hello tooconstruct hello accès partagé stratégie.
1. Appareil de Hello utilise le jeton de hello directement avec hello IoT hub.

> [!NOTE]
> Vous pouvez utiliser la classe .NET de hello [SharedAccessSignatureBuilder] [ lnk-dotnet-sas] ou hello classe Java [IotHubServiceSasToken] [ lnk-java-sas] toocreate un jeton dans votre service d’émission de jeton.

service de jeton de Hello peut définir l’expiration de jeton hello comme vous le souhaitez. Lors de l’expiration du jeton de hello, hub IoT de hello interrompt la connexion de périphérique de hello. Ensuite, les appareils hello doivent demander un nouveau jeton à partir du service de jeton de hello. Un délai d’expiration court augmente la charge hello sur le périphérique de hello et service de jeton de hello.

Pour un concentrateur de tooyour tooconnect du périphérique, vous devez toujours l’ajouter toohello Registre des identités IoT Hub, même si hello appareil utilise un jeton et pas une clé tooconnect de périphérique. Par conséquent, vous pouvez continuer le contrôle d’accès par périphérique toouse en activant ou désactivant les identités d’appareil Bonjour [Registre des identités][lnk-identity-registry]. Cette approche réduit les risques de hello de l’utilisation de jetons avec délais d’expiration longs.

### <a name="comparison-with-a-custom-gateway"></a>Comparaison avec une passerelle personnalisée

modèle de service de jeton Hello est hello recommandé tooimplement de façon un schéma de Registre / d’authentification d’identité personnalisé avec IoT Hub. Ce modèle est recommandé, car l’IoT Hub continue toohandle la plupart du trafic de solution hello. Toutefois, si le schéma d’authentification personnalisé hello est donc étroitement avec le protocole de hello, vous pouvez avoir besoin une *passerelle personnalisé* tooprocess tous hello du trafic. [Le protocole TLS (Transport Layer Security) et les clés prépartagées (PSK)][lnk-tls-psk] en sont un exemple. Pour plus d’informations, consultez hello [passerelle de protocole] [ lnk-protocols] rubrique.

## <a name="reference-topics"></a>Rubriques de référence :

Hello rubriques de référence suivantes vous fournissent plus d’informations sur tooyour IoT hub de contrôler l’accès.

## <a name="iot-hub-permissions"></a>Autorisations IoT Hub

Hello tableau suivant répertorie les autorisations hello vous pouvez utiliser toocontrol accès tooyour IoT hub.

| Autorisation | Remarques |
| --- | --- |
| **RegistryRead**. |Registre des identités toohello accorde un accès en lecture. Pour plus d’informations, consultez [Registre des identités][lnk-identity-registry]. <br/>Cette autorisation est utilisée par les services cloud principaux. |
| **RegistryReadWrite**. |Octroie accès en lecture et écriture toohello Registre des identités. Pour plus d’informations, consultez [Registre des identités][lnk-identity-registry]. <br/>Cette autorisation est utilisée par les services cloud principaux. |
| **ServiceConnect**. |Octroie accéder toocloud service orientées communication et la surveillance des points de terminaison. <br/>Octroie autorisation tooreceive les messages appareil-à-cloud, envoyer des messages cloud-à-appareil et hello récupérer correspondant des accusés de réception de remise. <br/>Les téléchargements accorde autorisation tooretrieve remise les accusés de réception pour le fichier. <br/>Octroie autorisation tooaccess appareil jumeaux tooupdate balises et les propriétés souhaitées, récupérer les propriétés déclarées et exécuter des requêtes. <br/>Cette autorisation est utilisée par les services cloud principaux. |
| **DeviceConnect**. |Octroie accéder aux points de terminaison toodevice accessibles. <br/>Octroie autorisation toosend appareil-à-cloud messages et recevoir des messages cloud-à-appareil. <br/>Téléchargement du fichier tooperform accorde autorisation à partir d’un appareil. <br/>Notifications de la propriété accorde autorisation tooreceive appareil double souhaité et de périphérique de mise à jour à deux propriétés déclarées. <br/>Fichier de tooperform d’autorisations accorde télécharge. <br/>Cette autorisation est utilisée par les appareils. |

## <a name="additional-reference-material"></a>Matériel de référence supplémentaire

Les autres rubriques de référence de hello guide du développeur IoT Hub sont les suivantes :

* [Points de terminaison IoT Hub] [ lnk-endpoints] décrit hello différents points de terminaison qui expose de chaque IoT hub pour les opérations de gestion et d’exécution.
* [Limitation et les quotas] [ lnk-quotas] décrit les quotas hello et la limitation des comportements qui s’appliquent toohello IoT Hub service.
* [Azure IoT périphérique et service kits de développement logiciel] [ lnk-sdks] listes hello langue différents kits de développement logiciel vous pouvez utiliser lorsque vous développez des applications de périphérique et le service qui interagissent avec IoT Hub.
* [Langage de requête IoT Hub] [ lnk-query] décrit le langage de requête hello vous pouvez utiliser les informations de tooretrieve à partir de IoT Hub sur votre jumeaux de périphérique et les travaux.
* [Prise en charge IoT Hub MQTT] [ lnk-devguide-mqtt] fournit plus d’informations sur la prise en charge IoT Hub pour le protocole MQTT hello.

## <a name="next-steps"></a>Étapes suivantes

Maintenant vous avez appris comment toocontrol aux IoT Hub, peut vous intéresser hello IoT Hub développeur guide rubriques suivantes :

* [Utiliser les configurations et état du périphérique jumeaux toosynchronize][lnk-devguide-device-twins]
* [Appeler une méthode directe sur un appareil][lnk-devguide-directmethods]
* [Planifier des travaux sur plusieurs appareils][lnk-devguide-jobs]

Si vous souhaitez que tootry certains des concepts hello décrits dans cet article, peut vous intéresser hello suivant les didacticiels IoT Hub :

* [Mise en route d’Azure IoT Hub][lnk-getstarted-tutorial]
* [Comment les messages toosend cloud-à-appareil avec IoT Hub][lnk-c2d-tutorial]
* [Comment tooprocess les messages appareil-à-cloud IoT Hub][lnk-d2c-tutorial]

<!-- links and images -->

[img-tokenservice]: ./media/iot-hub-devguide-security/tokenservice.png
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-openssl]: https://www.openssl.org/
[lnk-selfsigned]: https://technet.microsoft.com/library/hh848633

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-sas-tokens]: iot-hub-devguide-security.md#security-tokens
[lnk-amqp]: https://www.amqp.org/
[lnk-azure-resource-manager]: ../azure-resource-manager/resource-group-overview.md
[lnk-cbs]: https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc
[lnk-event-hubs-publisher-policy]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab
[lnk-management-portal]: https://portal.azure.com
[lnk-sasl-plain]: http://tools.ietf.org/html/rfc4616
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-dotnet-sas]: https://msdn.microsoft.com/library/microsoft.azure.devices.common.security.sharedaccesssignaturebuilder.aspx
[lnk-java-sas]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth._iot_hub_service_sas_token
[lnk-tls-psk]: https://tools.ietf.org/html/rfc4279
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-custom-auth]: iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: iot-hub-devguide-security.md#supported-x509-certificates
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-client-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
