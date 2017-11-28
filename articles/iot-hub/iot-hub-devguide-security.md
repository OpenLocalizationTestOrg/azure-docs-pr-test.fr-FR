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
# <a name="control-access-tooiot-hub"></a><span data-ttu-id="0f166-104">Contrôle l’accès tooIoT Hub</span><span class="sxs-lookup"><span data-stu-id="0f166-104">Control access tooIoT Hub</span></span>

<span data-ttu-id="0f166-105">Cet article décrit les options de hello pour sécuriser votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0f166-105">This article describes hello options for securing your IoT hub.</span></span> <span data-ttu-id="0f166-106">IoT Hub utilise *autorisations* point de terminaison toogrant accès tooeach IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0f166-106">IoT Hub uses *permissions* toogrant access tooeach IoT hub endpoint.</span></span> <span data-ttu-id="0f166-107">Autorisations limitent hub IoT hello accès tooan sont basée sur fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="0f166-107">Permissions limit hello access tooan IoT hub based on functionality.</span></span>

<span data-ttu-id="0f166-108">Cet article explique :</span><span class="sxs-lookup"><span data-stu-id="0f166-108">This article describes:</span></span>

* <span data-ttu-id="0f166-109">Hello différentes autorisations que vous pouvez accorder tooa appareil ou applications principal tooaccess votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0f166-109">hello different permissions that you can grant tooa device or back-end app tooaccess your IoT hub.</span></span>
* <span data-ttu-id="0f166-110">Bonjour processus et hello les jetons d’authentification qu’il utilise des autorisations de tooverify.</span><span class="sxs-lookup"><span data-stu-id="0f166-110">hello authentication process and hello tokens it uses tooverify permissions.</span></span>
* <span data-ttu-id="0f166-111">Comment tooscope les informations d’identification de toospecific toolimit accéder aux ressources.</span><span class="sxs-lookup"><span data-stu-id="0f166-111">How tooscope credentials toolimit access toospecific resources.</span></span>
* <span data-ttu-id="0f166-112">La prise en charge par IoT Hub des certificats X.509.</span><span class="sxs-lookup"><span data-stu-id="0f166-112">IoT Hub support for X.509 certificates.</span></span>
* <span data-ttu-id="0f166-113">Les mécanismes d’authentification d’appareil personnalisés qui utilisent des registres d’identités d’appareil ou des schémas d’authentification existants.</span><span class="sxs-lookup"><span data-stu-id="0f166-113">Custom device authentication mechanisms that use existing device identity registries or authentication schemes.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="0f166-114">Lorsque toouse</span><span class="sxs-lookup"><span data-stu-id="0f166-114">When toouse</span></span>

<span data-ttu-id="0f166-115">Vous devez disposer des autorisations appropriées tooaccess un des points de terminaison IoT Hub hello.</span><span class="sxs-lookup"><span data-stu-id="0f166-115">You must have appropriate permissions tooaccess any of hello IoT Hub endpoints.</span></span> <span data-ttu-id="0f166-116">Par exemple, un appareil doit inclure un jeton contenant des informations d’identification de sécurité, ainsi que tous les messages qu’il envoie tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0f166-116">For example, a device must include a token containing security credentials along with every message it sends tooIoT Hub.</span></span>

## <a name="access-control-and-permissions"></a><span data-ttu-id="0f166-117">Contrôle d’accès et autorisations</span><span class="sxs-lookup"><span data-stu-id="0f166-117">Access control and permissions</span></span>

<span data-ttu-id="0f166-118">Vous pouvez accorder [autorisations](#iot-hub-permissions) Bonjour suivant façons :</span><span class="sxs-lookup"><span data-stu-id="0f166-118">You can grant [permissions](#iot-hub-permissions) in hello following ways:</span></span>

* <span data-ttu-id="0f166-119">**Stratégies d’accès partagé au niveau d’IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="0f166-119">**IoT hub-level shared access policies**.</span></span> <span data-ttu-id="0f166-120">Les stratégies d’accès partagé peuvent accorder n’importe quelle combinaison d’[autorisations](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="0f166-120">Shared access policies can grant any combination of [permissions](#iot-hub-permissions).</span></span> <span data-ttu-id="0f166-121">Vous pouvez définir des stratégies dans hello [portail Azure][lnk-management-portal], ou par programme à l’aide de hello [fournisseur de ressources IoT Hub API REST][lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="0f166-121">You can define policies in hello [Azure portal][lnk-management-portal], or programmatically by using hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="0f166-122">Un hub IoT nouvellement créé a hello suivant des stratégies par défaut :</span><span class="sxs-lookup"><span data-stu-id="0f166-122">A newly created IoT hub has hello following default policies:</span></span>

  * <span data-ttu-id="0f166-123">**iothubowner**: stratégie jouissant de toutes les autorisations.</span><span class="sxs-lookup"><span data-stu-id="0f166-123">**iothubowner**: Policy with all permissions.</span></span>
  * <span data-ttu-id="0f166-124">**service** : stratégie jouissant de l’autorisation **ServiceConnect**.</span><span class="sxs-lookup"><span data-stu-id="0f166-124">**service**: Policy with **ServiceConnect** permission.</span></span>
  * <span data-ttu-id="0f166-125">**device** : stratégie jouissant de l’autorisation **DeviceConnect**.</span><span class="sxs-lookup"><span data-stu-id="0f166-125">**device**: Policy with **DeviceConnect** permission.</span></span>
  * <span data-ttu-id="0f166-126">**registryRead** : stratégie jouissant de l’autorisation **RegistryRead**.</span><span class="sxs-lookup"><span data-stu-id="0f166-126">**registryRead**: Policy with **RegistryRead** permission.</span></span>
  * <span data-ttu-id="0f166-127">**registryReadWrite** : stratégie jouissant des autorisations **RegistryRead** et RegistryWrite.</span><span class="sxs-lookup"><span data-stu-id="0f166-127">**registryReadWrite**: Policy with **RegistryRead** and RegistryWrite permissions.</span></span>
  * <span data-ttu-id="0f166-128">**Informations d’identification de sécurité par appareil**.</span><span class="sxs-lookup"><span data-stu-id="0f166-128">**Per-device security credentials**.</span></span> <span data-ttu-id="0f166-129">Chaque hub IoT contient un [registre des identités][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="0f166-129">Each IoT Hub contains an [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="0f166-130">Pour chaque périphérique dans le Registre des identités, vous pouvez configurer les informations d’identification de sécurité qui accorde **DeviceConnect** autorisations étendue des points de terminaison de périphérique correspondant toohello.</span><span class="sxs-lookup"><span data-stu-id="0f166-130">For each device in this identity registry, you can configure security credentials that grant **DeviceConnect** permissions scoped toohello corresponding device endpoints.</span></span>

<span data-ttu-id="0f166-131">Par exemple, dans une solution IoT classique :</span><span class="sxs-lookup"><span data-stu-id="0f166-131">For example, in a typical IoT solution:</span></span>

* <span data-ttu-id="0f166-132">composant de gestion de périphérique Hello utilise hello *registryReadWrite* stratégie.</span><span class="sxs-lookup"><span data-stu-id="0f166-132">hello device management component uses hello *registryReadWrite* policy.</span></span>
* <span data-ttu-id="0f166-133">composant processeur d’événements Hello utilise hello *service* stratégie.</span><span class="sxs-lookup"><span data-stu-id="0f166-133">hello event processor component uses hello *service* policy.</span></span>
* <span data-ttu-id="0f166-134">composant de la logique d’entreprise Hello appareil de l’exécution utilise hello *service* stratégie.</span><span class="sxs-lookup"><span data-stu-id="0f166-134">hello run-time device business logic component uses hello *service* policy.</span></span>
* <span data-ttu-id="0f166-135">Périphériques individuels se connectent à l’aide des informations d’identification stockées dans le Registre des identités de concentrateur hello IoT.</span><span class="sxs-lookup"><span data-stu-id="0f166-135">Individual devices connect using credentials stored in hello IoT hub's identity registry.</span></span>

> [!NOTE]
> <span data-ttu-id="0f166-136">Pour plus d’informations, consultez la page [Autorisations](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="0f166-136">See [permissions](#iot-hub-permissions) for detailed information.</span></span>

## <a name="authentication"></a><span data-ttu-id="0f166-137">Authentification</span><span class="sxs-lookup"><span data-stu-id="0f166-137">Authentication</span></span>

<span data-ttu-id="0f166-138">IoT Hub Azure accorde l’accès tooendpoints en vérifiant un jeton par rapport aux stratégies d’accès partagé de hello et identification de sécurité du Registre.</span><span class="sxs-lookup"><span data-stu-id="0f166-138">Azure IoT Hub grants access tooendpoints by verifying a token against hello shared access policies and identity registry security credentials.</span></span>

<span data-ttu-id="0f166-139">Informations d’identification de sécurité, telles que des clés symétriques, ne sont jamais envoyées acheminement hello.</span><span class="sxs-lookup"><span data-stu-id="0f166-139">Security credentials, such as symmetric keys, are never sent over hello wire.</span></span>

> [!NOTE]
> <span data-ttu-id="0f166-140">Hello fournisseur de ressources Azure IoT Hub est sécurisé via votre abonnement Azure, sont tous les fournisseurs hello [Azure Resource Manager][lnk-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="0f166-140">hello Azure IoT Hub resource provider is secured through your Azure subscription, as are all providers in hello [Azure Resource Manager][lnk-azure-resource-manager].</span></span>

<span data-ttu-id="0f166-141">Pour plus d’informations sur la façon tooconstruct et l’utilisation des jetons de sécurité, consultez [des jetons de sécurité IoT Hub][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="0f166-141">For more information about how tooconstruct and use security tokens, see [IoT Hub security tokens][lnk-sas-tokens].</span></span>

### <a name="protocol-specifics"></a><span data-ttu-id="0f166-142">Spécifications de protocole</span><span class="sxs-lookup"><span data-stu-id="0f166-142">Protocol specifics</span></span>

<span data-ttu-id="0f166-143">Chaque protocole pris en charge (par exemple, MQTT, AMQP et HTTP) transporte des jetons de différentes façons.</span><span class="sxs-lookup"><span data-stu-id="0f166-143">Each supported protocol, such as MQTT, AMQP, and HTTP, transports tokens in different ways.</span></span>

<span data-ttu-id="0f166-144">Lorsque vous utilisez MQTT, paquet de connexion hello a hello deviceId comme hello ClientId, {iothubhostname} / {deviceId} dans le champ de nom d’utilisateur hello et un jeton SAS dans le champ de mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="0f166-144">When using MQTT, hello CONNECT packet has hello deviceId as hello ClientId, {iothubhostname}/{deviceId} in hello Username field, and a SAS token in hello Password field.</span></span> <span data-ttu-id="0f166-145">{iothubhostname} doit être hello complète CName hello IoT hub (par exemple, contoso.azure devices.net).</span><span class="sxs-lookup"><span data-stu-id="0f166-145">{iothubhostname} should be hello full CName of hello IoT hub (for example, contoso.azure-devices.net).</span></span>

<span data-ttu-id="0f166-146">Lorsque vous utilisez [AMQP][lnk-amqp], IoT Hub prend en charge [SASL PLAIN][lnk-sasl-plain] et la [sécurité basée sur des revendications AMQP][lnk-cbs].</span><span class="sxs-lookup"><span data-stu-id="0f166-146">When using [AMQP][lnk-amqp], IoT Hub supports [SASL PLAIN][lnk-sasl-plain] and [AMQP Claims-Based-Security][lnk-cbs].</span></span>

<span data-ttu-id="0f166-147">Spécifie de hello standard si vous utilisez AMQP revendications--sécurité, comment tootransmit ces jetons.</span><span class="sxs-lookup"><span data-stu-id="0f166-147">If you use AMQP claims-based-security, hello standard specifies how tootransmit these tokens.</span></span>

<span data-ttu-id="0f166-148">Pour SASL brut, hello **nom d’utilisateur** peut être :</span><span class="sxs-lookup"><span data-stu-id="0f166-148">For SASL PLAIN, hello **username** can be:</span></span>

* <span data-ttu-id="0f166-149">`{policyName}@sas.root.{iothubName}` si vous utilisez des jetons au niveau du hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0f166-149">`{policyName}@sas.root.{iothubName}` if using IoT hub-level tokens.</span></span>
* <span data-ttu-id="0f166-150">`{deviceId}@sas.{iothubname}` si vous utilisez des jetons à l’échelle de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="0f166-150">`{deviceId}@sas.{iothubname}` if using device-scoped tokens.</span></span>

<span data-ttu-id="0f166-151">Dans les deux cas, les champs de mot de passe hello contient le jeton de hello, comme décrit dans [des jetons de sécurité IoT Hub][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="0f166-151">In both cases, hello password field contains hello token, as described in [IoT Hub security tokens][lnk-sas-tokens].</span></span>

<span data-ttu-id="0f166-152">HTTP implémente l’authentification en incluant un jeton valide Bonjour **autorisation** en-tête de demande.</span><span class="sxs-lookup"><span data-stu-id="0f166-152">HTTP implements authentication by including a valid token in hello **Authorization** request header.</span></span>

#### <a name="example"></a><span data-ttu-id="0f166-153">Exemple</span><span class="sxs-lookup"><span data-stu-id="0f166-153">Example</span></span>

<span data-ttu-id="0f166-154">Nom d’utilisateur (DeviceId respecte la casse) : `iothubname.azure-devices.net/DeviceId`</span><span class="sxs-lookup"><span data-stu-id="0f166-154">Username (DeviceId is case-sensitive): `iothubname.azure-devices.net/DeviceId`</span></span>

<span data-ttu-id="0f166-155">Mot de passe (jeton SAS de générer avec hello [Explorateur de périphérique] [ lnk-device-explorer] outil) :`SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span><span class="sxs-lookup"><span data-stu-id="0f166-155">Password (Generate SAS token with hello [device explorer][lnk-device-explorer] tool): `SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span></span>

> [!NOTE]
> <span data-ttu-id="0f166-156">Hello [kits de développement logiciel Azure IoT] [ lnk-sdks] générer automatiquement des jetons lors de la connexion toohello service.</span><span class="sxs-lookup"><span data-stu-id="0f166-156">hello [Azure IoT SDKs][lnk-sdks] automatically generate tokens when connecting toohello service.</span></span> <span data-ttu-id="0f166-157">Dans certains cas, hello kits de développement logiciel Azure IoT ne gèrent pas tous les protocoles hello ou toutes les méthodes d’authentification hello.</span><span class="sxs-lookup"><span data-stu-id="0f166-157">In some cases, hello Azure IoT SDKs do not support all hello protocols or all hello authentication methods.</span></span>

### <a name="special-considerations-for-sasl-plain"></a><span data-ttu-id="0f166-158">Considérations spécifiques concernant SASL PLAIN</span><span class="sxs-lookup"><span data-stu-id="0f166-158">Special considerations for SASL PLAIN</span></span>

<span data-ttu-id="0f166-159">Lorsque vous utilisez SASL brut avec AMQP, un client se connectant tooan IoT hub peut utiliser un jeton unique pour chaque connexion TCP.</span><span class="sxs-lookup"><span data-stu-id="0f166-159">When using SASL PLAIN with AMQP, a client connecting tooan IoT hub can use a single token for each TCP connection.</span></span> <span data-ttu-id="0f166-160">Lors de l’expiration du jeton de hello, hello connexion TCP se déconnecte de service de hello et déclenche une reconnexion.</span><span class="sxs-lookup"><span data-stu-id="0f166-160">When hello token expires, hello TCP connection disconnects from hello service and triggers a reconnect.</span></span> <span data-ttu-id="0f166-161">Ce comportement, pendant pas problématique pour une application back-end, endommager pour une application de périphérique pour hello suivant raisons :</span><span class="sxs-lookup"><span data-stu-id="0f166-161">This behavior, while not problematic for a back-end app, is damaging for a device app for hello following reasons:</span></span>

* <span data-ttu-id="0f166-162">Les passerelles se connectent généralement au nom de nombreux appareils.</span><span class="sxs-lookup"><span data-stu-id="0f166-162">Gateways usually connect on behalf of many devices.</span></span> <span data-ttu-id="0f166-163">Lorsque vous utilisez SASL brut, ils ont toocreate une connexion TCP distincte pour chaque périphérique se connectant tooan IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0f166-163">When using SASL PLAIN, they have toocreate a distinct TCP connection for each device connecting tooan IoT hub.</span></span> <span data-ttu-id="0f166-164">Ce scénario considérablement augmente la consommation de puissance et de ressources réseau hello et augmente la latence hello de chaque connexion de périphérique.</span><span class="sxs-lookup"><span data-stu-id="0f166-164">This scenario considerably increases hello consumption of power and networking resources, and increases hello latency of each device connection.</span></span>
* <span data-ttu-id="0f166-165">Périphériques ressources limitées sont affectées à l’aide de hello augmentée de ressources tooreconnect après chaque d’expiration du jeton.</span><span class="sxs-lookup"><span data-stu-id="0f166-165">Resource-constrained devices are adversely affected by hello increased use of resources tooreconnect after each token expiration.</span></span>

## <a name="scope-iot-hub-level-credentials"></a><span data-ttu-id="0f166-166">Étendue des informations d’identification au niveau du hub IoT</span><span class="sxs-lookup"><span data-stu-id="0f166-166">Scope IoT hub-level credentials</span></span>

<span data-ttu-id="0f166-167">Vous pouvez étendre les stratégies de sécurité au niveau du hub IoT en créant des jetons avec un URI de ressource restreint.</span><span class="sxs-lookup"><span data-stu-id="0f166-167">You can scope IoT hub-level security policies by creating tokens with a restricted resource URI.</span></span> <span data-ttu-id="0f166-168">Par exemple, les messages appareil-à-cloud toosend du point de terminaison hello à partir d’un appareil est **/devices/ {deviceId} / messages/événements**.</span><span class="sxs-lookup"><span data-stu-id="0f166-168">For example, hello endpoint toosend device-to-cloud messages from a device is **/devices/{deviceId}/messages/events**.</span></span> <span data-ttu-id="0f166-169">Vous pouvez également utiliser une stratégie d’un accès partagé au niveau du hub IoT avec **DeviceConnect** toosign d’autorisations dont resourceURI est un jeton de **/devices/ {deviceId}**.</span><span class="sxs-lookup"><span data-stu-id="0f166-169">You can also use an IoT hub-level shared access policy with **DeviceConnect** permissions toosign a token whose resourceURI is **/devices/{deviceId}**.</span></span> <span data-ttu-id="0f166-170">Cette approche crée un jeton qui est uniquement des messages toosend utilisable pour le compte d’appareil **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="0f166-170">This approach creates a token that is only usable toosend messages on behalf of device **deviceId**.</span></span>

<span data-ttu-id="0f166-171">Ce mécanisme est semblable toohello [stratégie d’éditeur de concentrateurs d’événements][lnk-event-hubs-publisher-policy]et vous permet de méthodes d’authentification personnalisée tooimplement.</span><span class="sxs-lookup"><span data-stu-id="0f166-171">This mechanism is similar toohello [Event Hubs publisher policy][lnk-event-hubs-publisher-policy], and enables you tooimplement custom authentication methods.</span></span>

## <a name="security-tokens"></a><span data-ttu-id="0f166-172">Jetons de sécurité</span><span class="sxs-lookup"><span data-stu-id="0f166-172">Security tokens</span></span>

<span data-ttu-id="0f166-173">IoT Hub utilise la sécurité jetons tooauthenticate appareils et services tooavoid envoi de clés sur le câble de hello.</span><span class="sxs-lookup"><span data-stu-id="0f166-173">IoT Hub uses security tokens tooauthenticate devices and services tooavoid sending keys on hello wire.</span></span> <span data-ttu-id="0f166-174">En outre, la validité et la portée des jetons sont limitées dans le temps.</span><span class="sxs-lookup"><span data-stu-id="0f166-174">Additionally, security tokens are limited in time validity and scope.</span></span> <span data-ttu-id="0f166-175">Les kits [Azure IoT SDK ][lnk-sdks] génèrent automatiquement les jetons sans configuration spéciale.</span><span class="sxs-lookup"><span data-stu-id="0f166-175">[Azure IoT SDKs][lnk-sdks] automatically generate tokens without requiring any special configuration.</span></span> <span data-ttu-id="0f166-176">Certains scénarios nécessitent toogenerate et utiliser directement les jetons de sécurité.</span><span class="sxs-lookup"><span data-stu-id="0f166-176">Some scenarios do require you toogenerate and use security tokens directly.</span></span> <span data-ttu-id="0f166-177">Il s’agit entre autres des scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="0f166-177">Such scenarios include:</span></span>

* <span data-ttu-id="0f166-178">utilisation directe de Hello des surfaces MQTT, AMQP ou HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="0f166-178">hello direct use of hello MQTT, AMQP, or HTTP surfaces.</span></span>
* <span data-ttu-id="0f166-179">Hello d’implémentation du modèle de service de jeton de hello, comme expliqué dans [l’authentification des appareils personnalisé][lnk-custom-auth].</span><span class="sxs-lookup"><span data-stu-id="0f166-179">hello implementation of hello token service pattern, as explained in [Custom device authentication][lnk-custom-auth].</span></span>

<span data-ttu-id="0f166-180">IoT Hub autorise également les périphériques tooauthenticate avec IoT Hub à l’aide de [certificats X.509][lnk-x509].</span><span class="sxs-lookup"><span data-stu-id="0f166-180">IoT Hub also allows devices tooauthenticate with IoT Hub using [X.509 certificates][lnk-x509].</span></span>

### <a name="security-token-structure"></a><span data-ttu-id="0f166-181">Structure du jeton de sécurité</span><span class="sxs-lookup"><span data-stu-id="0f166-181">Security token structure</span></span>

<span data-ttu-id="0f166-182">Vous utilisez sécurité jetons toogrant limités toodevices et services toospecific fonctionnalité d’accès dans IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0f166-182">You use security tokens toogrant time-bounded access toodevices and services toospecific functionality in IoT Hub.</span></span> <span data-ttu-id="0f166-183">tooget d’autorisation tooconnect tooIoT Hub, appareils et services doivent envoyer des jetons de sécurité signés avec un accès partagé ou une clé symétrique.</span><span class="sxs-lookup"><span data-stu-id="0f166-183">tooget authorization tooconnect tooIoT Hub, devices and services must send security tokens signed with either a shared access or symmetric key.</span></span> <span data-ttu-id="0f166-184">Ces clés sont stockées avec une identité d’appareil dans le Registre des identités hello.</span><span class="sxs-lookup"><span data-stu-id="0f166-184">These keys are stored with a device identity in hello identity registry.</span></span>

<span data-ttu-id="0f166-185">Un jeton signé avec une accès partagé accorde clé tooall hello fonctionnalité d’accès associée aux autorisations de stratégie d’accès hello partagé.</span><span class="sxs-lookup"><span data-stu-id="0f166-185">A token signed with a shared access key grants access tooall hello functionality associated with hello shared access policy permissions.</span></span> <span data-ttu-id="0f166-186">Un jeton signé avec hello d’accorde uniquement à clé symétrique d’une identité d’appareil **DeviceConnect** autorisation pour hello associé d’identité de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="0f166-186">A token signed with a device identity's symmetric key only grants hello **DeviceConnect** permission for hello associated device identity.</span></span>

<span data-ttu-id="0f166-187">jeton de sécurité Hello a hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="0f166-187">hello security token has hello following format:</span></span>

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

<span data-ttu-id="0f166-188">Voici les valeurs attendues hello :</span><span class="sxs-lookup"><span data-stu-id="0f166-188">Here are hello expected values:</span></span>

| <span data-ttu-id="0f166-189">Valeur</span><span class="sxs-lookup"><span data-stu-id="0f166-189">Value</span></span> | <span data-ttu-id="0f166-190">Description</span><span class="sxs-lookup"><span data-stu-id="0f166-190">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0f166-191">{signature}</span><span class="sxs-lookup"><span data-stu-id="0f166-191">{signature}</span></span> |<span data-ttu-id="0f166-192">Une chaîne de signature de code HMAC-SHA256 sous forme de hello : `{URL-encoded-resourceURI} + "\n" + expiry`.</span><span class="sxs-lookup"><span data-stu-id="0f166-192">An HMAC-SHA256 signature string of hello form: `{URL-encoded-resourceURI} + "\n" + expiry`.</span></span> <span data-ttu-id="0f166-193">**Important**: hello clé est décodée à partir de base64 et utilisée en tant que clé tooperform le calcul hello HMAC-SHA256.</span><span class="sxs-lookup"><span data-stu-id="0f166-193">**Important**: hello key is decoded from base64 and used as key tooperform hello HMAC-SHA256 computation.</span></span> |
| <span data-ttu-id="0f166-194">{resourceURI}</span><span class="sxs-lookup"><span data-stu-id="0f166-194">{resourceURI}</span></span> |<span data-ttu-id="0f166-195">Préfixe URI (par segment) des points de terminaison hello qui sont accessibles par ce jeton, en commençant par le nom d’hôte de hello IoT hub (aucun protocole).</span><span class="sxs-lookup"><span data-stu-id="0f166-195">URI prefix (by segment) of hello endpoints that can be accessed with this token, starting with host name of hello IoT hub (no protocol).</span></span> <span data-ttu-id="0f166-196">Par exemple, `myHub.azure-devices.net/devices/device1`</span><span class="sxs-lookup"><span data-stu-id="0f166-196">For example, `myHub.azure-devices.net/devices/device1`</span></span> |
| <span data-ttu-id="0f166-197">{expiry}</span><span class="sxs-lookup"><span data-stu-id="0f166-197">{expiry}</span></span> |<span data-ttu-id="0f166-198">Chaînes UTF-8 pour le nombre de secondes écoulées depuis le 1er janvier 1970 hello époque 00:00:00 UTC.</span><span class="sxs-lookup"><span data-stu-id="0f166-198">UTF8 strings for number of seconds since hello epoch 00:00:00 UTC on 1 January 1970.</span></span> |
| <span data-ttu-id="0f166-199">{URL-encoded-resourceURI}</span><span class="sxs-lookup"><span data-stu-id="0f166-199">{URL-encoded-resourceURI}</span></span> |<span data-ttu-id="0f166-200">Faible cas encodage d’URL de l’URI de ressource hello minuscules</span><span class="sxs-lookup"><span data-stu-id="0f166-200">Lower case URL-encoding of hello lower case resource URI</span></span> |
| <span data-ttu-id="0f166-201">{policyName}</span><span class="sxs-lookup"><span data-stu-id="0f166-201">{policyName}</span></span> |<span data-ttu-id="0f166-202">nom de Hello Hello partagé toowhich de stratégie d’accès que fait référence de ce jeton.</span><span class="sxs-lookup"><span data-stu-id="0f166-202">hello name of hello shared access policy toowhich this token refers.</span></span> <span data-ttu-id="0f166-203">Absent si le jeton de hello fait référence les informations d’identification de toodevice du Registre.</span><span class="sxs-lookup"><span data-stu-id="0f166-203">Absent if hello token refers toodevice-registry credentials.</span></span> |

<span data-ttu-id="0f166-204">**Remarque sur le préfixe**: préfixe URI de hello est calculé par segment et non par caractère.</span><span class="sxs-lookup"><span data-stu-id="0f166-204">**Note on prefix**: hello URI prefix is computed by segment and not by character.</span></span> <span data-ttu-id="0f166-205">Par exemple `/a/b` est un préfixe de `/a/b/c`, mais pas de `/a/bc`.</span><span class="sxs-lookup"><span data-stu-id="0f166-205">For example `/a/b` is a prefix for `/a/b/c` but not for `/a/bc`.</span></span>

<span data-ttu-id="0f166-206">Hello Node.js extrait de code suivant illustre une fonction appelée **generateSasToken** que calcule hello jeton à partir des entrées de hello `resourceUri, signingKey, policyName, expiresInMins`.</span><span class="sxs-lookup"><span data-stu-id="0f166-206">hello following Node.js snippet shows a function called **generateSasToken** that computes hello token from hello inputs `resourceUri, signingKey, policyName, expiresInMins`.</span></span> <span data-ttu-id="0f166-207">les sections suivantes Hello décrit en détail comment tooinitialize hello différentes entrées pour le jeton différent de hello cas d’usage.</span><span class="sxs-lookup"><span data-stu-id="0f166-207">hello next sections detail how tooinitialize hello different inputs for hello different token use cases.</span></span>

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

<span data-ttu-id="0f166-208">En comparaison, hello toogenerate de code Python équivalent qu'est d’un jeton de sécurité :</span><span class="sxs-lookup"><span data-stu-id="0f166-208">As a comparison, hello equivalent Python code toogenerate a security token is:</span></span>

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
> <span data-ttu-id="0f166-209">Étant donné que la validité du jeton de hello hello est validée sur les ordinateurs de IoT Hub, écarts hello horloge hello d’ordinateur hello qui génère les jetons hello doit être minime.</span><span class="sxs-lookup"><span data-stu-id="0f166-209">Since hello time validity of hello token is validated on IoT Hub machines, hello drift on hello clock of hello machine that generates hello token must be minimal.</span></span>

### <a name="use-sas-tokens-in-a-device-app"></a><span data-ttu-id="0f166-210">Utiliser des jetons SPA dans une application d’appareil</span><span class="sxs-lookup"><span data-stu-id="0f166-210">Use SAS tokens in a device app</span></span>

<span data-ttu-id="0f166-211">Il existe deux façons tooobtain **DeviceConnect** autorisations avec IoT Hub avec des jetons de sécurité : utilisez un [clé symétrique de périphérique à partir du Registre des identités hello](#use-a-symmetric-key-in-the-identity-registry), ou utilisez un [cléd’accèspartagé](#use-a-shared-access-policy).</span><span class="sxs-lookup"><span data-stu-id="0f166-211">There are two ways tooobtain **DeviceConnect** permissions with IoT Hub with security tokens: use a [symmetric device key from hello identity registry](#use-a-symmetric-key-in-the-identity-registry), or use a [shared access key](#use-a-shared-access-policy).</span></span>

<span data-ttu-id="0f166-212">N’oubliez pas que toutes les fonctionnalités accessibles à partir des appareils sont exposées par définition sur les points de terminaison avec le préfixe `/devices/{deviceId}`.</span><span class="sxs-lookup"><span data-stu-id="0f166-212">Remember that all functionality accessible from devices is exposed by design on endpoints with prefix `/devices/{deviceId}`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0f166-213">Hello seule façon que IoT Hub s’authentifie à un périphérique spécifique à l’aide de clé symétrique d’identité appareil hello.</span><span class="sxs-lookup"><span data-stu-id="0f166-213">hello only way that IoT Hub authenticates a specific device is using hello device identity symmetric key.</span></span> <span data-ttu-id="0f166-214">Dans le cas lorsqu’une stratégie d’accès partagé est une fonctionnalité d’appareil tooaccess utilisé, les solutions hello doivent prendre en compte composant hello émission de jeton de sécurité hello comme un sous-composant approuvé.</span><span class="sxs-lookup"><span data-stu-id="0f166-214">In cases when a shared access policy is used tooaccess device functionality, hello solution must consider hello component issuing hello security token as a trusted subcomponent.</span></span>

<span data-ttu-id="0f166-215">points de terminaison de périphérique Hello sont (quel que soit le protocole de hello) :</span><span class="sxs-lookup"><span data-stu-id="0f166-215">hello device-facing endpoints are (irrespective of hello protocol):</span></span>

| <span data-ttu-id="0f166-216">Point de terminaison</span><span class="sxs-lookup"><span data-stu-id="0f166-216">Endpoint</span></span> | <span data-ttu-id="0f166-217">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="0f166-217">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |<span data-ttu-id="0f166-218">Envoyer des messages appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="0f166-218">Send device-to-cloud messages.</span></span> |
| `{iot hub host name}/devices/{deviceId}/devicebound` |<span data-ttu-id="0f166-219">Recevoir des messages cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="0f166-219">Receive cloud-to-device messages.</span></span> |

### <a name="use-a-symmetric-key-in-hello-identity-registry"></a><span data-ttu-id="0f166-220">Utiliser une clé symétrique dans le Registre des identités hello</span><span class="sxs-lookup"><span data-stu-id="0f166-220">Use a symmetric key in hello identity registry</span></span>

<span data-ttu-id="0f166-221">Lorsque vous utilisez toogenerate clé symétrique un jeton d’identité d’un appareil, hello stratégie (`skn`) élément de jeton de hello est omis.</span><span class="sxs-lookup"><span data-stu-id="0f166-221">When using a device identity's symmetric key toogenerate a token, hello policyName (`skn`) element of hello token is omitted.</span></span>

<span data-ttu-id="0f166-222">Par exemple, un jeton créé tooaccess toutes les fonctionnalités de l’appareil doit avoir hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="0f166-222">For example, a token created tooaccess all device functionality should have hello following parameters:</span></span>

* <span data-ttu-id="0f166-223">URI de ressource : `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="0f166-223">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="0f166-224">clé de signature : une clé symétrique pour hello `{device id}` identité,</span><span class="sxs-lookup"><span data-stu-id="0f166-224">signing key: any symmetric key for hello `{device id}` identity,</span></span>
* <span data-ttu-id="0f166-225">pas de nom de stratégie,</span><span class="sxs-lookup"><span data-stu-id="0f166-225">no policy name,</span></span>
* <span data-ttu-id="0f166-226">n’importe quelle heure d’expiration.</span><span class="sxs-lookup"><span data-stu-id="0f166-226">any expiration time.</span></span>

<span data-ttu-id="0f166-227">Un exemple d’utilisation hello précédant Node.js fonction serait :</span><span class="sxs-lookup"><span data-stu-id="0f166-227">An example using hello preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

<span data-ttu-id="0f166-228">résultat de Hello, qui accorde l’accès des fonctionnalités tooall pour appareil1, serait :</span><span class="sxs-lookup"><span data-stu-id="0f166-228">hello result, which grants access tooall functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> <span data-ttu-id="0f166-229">Il est possible de toogenerate un jeton SAP à l’aide de hello .NET [Explorateur de périphérique] [ lnk-device-explorer] outil ou hello inter-plateformes, basée sur le nœud [iothub-explorer] [ lnk-iothub-explorer] utilitaire de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="0f166-229">It is possible toogenerate a SAS token using hello .NET [device explorer][lnk-device-explorer] tool or hello cross-platform, node-based [iothub-explorer][lnk-iothub-explorer] command-line utility.</span></span>

### <a name="use-a-shared-access-policy"></a><span data-ttu-id="0f166-230">Utilisation d’une stratégie d’accès partagé</span><span class="sxs-lookup"><span data-stu-id="0f166-230">Use a shared access policy</span></span>

<span data-ttu-id="0f166-231">Lorsque vous créez un jeton à partir d’une stratégie d’accès partagé, définissez hello `skn` toohello nom du champ de la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="0f166-231">When you create a token from a shared access policy, set hello `skn` field toohello name of hello policy.</span></span> <span data-ttu-id="0f166-232">Cette stratégie doit accorder hello **DeviceConnect** autorisation.</span><span class="sxs-lookup"><span data-stu-id="0f166-232">This policy must grant hello **DeviceConnect** permission.</span></span>

<span data-ttu-id="0f166-233">Hello deux principaux scénarios pour l’utilisation de fonctionnalités du périphérique tooaccess accès partagé stratégies sont :</span><span class="sxs-lookup"><span data-stu-id="0f166-233">hello two main scenarios for using shared access policies tooaccess device functionality are:</span></span>

* <span data-ttu-id="0f166-234">[passerelles de protocole cloud][lnk-endpoints],</span><span class="sxs-lookup"><span data-stu-id="0f166-234">[cloud protocol gateways][lnk-endpoints],</span></span>
* <span data-ttu-id="0f166-235">[services de jeton] [ lnk-custom-auth] utilisé tooimplement des schémas d’authentification personnalisés.</span><span class="sxs-lookup"><span data-stu-id="0f166-235">[token services][lnk-custom-auth] used tooimplement custom authentication schemes.</span></span>

<span data-ttu-id="0f166-236">Depuis hello stratégie d’accès partagé peut potentiellement accorder l’accès tooconnect n’importe quel appareil, qu'il s’agit des URI de ressource correct hello toouse important lors de la création de jetons de sécurité.</span><span class="sxs-lookup"><span data-stu-id="0f166-236">Since hello shared access policy can potentially grant access tooconnect as any device, it is important toouse hello correct resource URI when creating security tokens.</span></span> <span data-ttu-id="0f166-237">Ce paramètre est particulièrement important pour les services de jeton, qui présentent le périphérique spécifique tooscope hello tooa jeton à l’aide d’URI de ressource hello.</span><span class="sxs-lookup"><span data-stu-id="0f166-237">This setting is especially important for token services, which have tooscope hello token tooa specific device using hello resource URI.</span></span> <span data-ttu-id="0f166-238">Ce point est moins important pour les passerelles de protocole, car elles interceptent déjà le trafic pour tous les appareils.</span><span class="sxs-lookup"><span data-stu-id="0f166-238">This point is less relevant for protocol gateways as they are already mediating traffic for all devices.</span></span>

<span data-ttu-id="0f166-239">Par exemple, un service de jeton à l’aide de hello créé au préalable partagé appelée stratégie d’accès **périphérique** créerait un jeton avec hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="0f166-239">As an example, a token service using hello pre-created shared access policy called **device** would create a token with hello following parameters:</span></span>

* <span data-ttu-id="0f166-240">URI de ressource : `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="0f166-240">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="0f166-241">clé de signature : une des clés de hello Hello `device` stratégie,</span><span class="sxs-lookup"><span data-stu-id="0f166-241">signing key: one of hello keys of hello `device` policy,</span></span>
* <span data-ttu-id="0f166-242">nom de la stratégie : `device`,</span><span class="sxs-lookup"><span data-stu-id="0f166-242">policy name: `device`,</span></span>
* <span data-ttu-id="0f166-243">n’importe quelle heure d’expiration.</span><span class="sxs-lookup"><span data-stu-id="0f166-243">any expiration time.</span></span>

<span data-ttu-id="0f166-244">Un exemple d’utilisation hello précédant Node.js fonction serait :</span><span class="sxs-lookup"><span data-stu-id="0f166-244">An example using hello preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="0f166-245">résultat de Hello, qui accorde l’accès des fonctionnalités tooall pour appareil1, serait :</span><span class="sxs-lookup"><span data-stu-id="0f166-245">hello result, which grants access tooall functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

<span data-ttu-id="0f166-246">Une passerelle de protocole peut utiliser hello même jeton pour tous les appareils définissant simplement hello URI de ressource trop`myhub.azure-devices.net/devices`.</span><span class="sxs-lookup"><span data-stu-id="0f166-246">A protocol gateway could use hello same token for all devices simply setting hello resource URI too`myhub.azure-devices.net/devices`.</span></span>

### <a name="use-security-tokens-from-service-components"></a><span data-ttu-id="0f166-247">Utilisation de jetons de sécurité de composants du service</span><span class="sxs-lookup"><span data-stu-id="0f166-247">Use security tokens from service components</span></span>

<span data-ttu-id="0f166-248">Composants de service peuvent uniquement générer des jetons de sécurité à l’aide de stratégies d’accès partagé accorde hello approprié comme expliqué précédemment.</span><span class="sxs-lookup"><span data-stu-id="0f166-248">Service components can only generate security tokens using shared access policies granting hello appropriate permissions as explained previously.</span></span>

<span data-ttu-id="0f166-249">Voici les fonctions de service hello exposées sur les points de terminaison hello :</span><span class="sxs-lookup"><span data-stu-id="0f166-249">Here is hello service functions exposed on hello endpoints:</span></span>

| <span data-ttu-id="0f166-250">Point de terminaison</span><span class="sxs-lookup"><span data-stu-id="0f166-250">Endpoint</span></span> | <span data-ttu-id="0f166-251">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="0f166-251">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices` |<span data-ttu-id="0f166-252">Créer, mettre à jour, récupérer et supprimer les identités des appareils.</span><span class="sxs-lookup"><span data-stu-id="0f166-252">Create, update, retrieve, and delete device identities.</span></span> |
| `{iot hub host name}/messages/events` |<span data-ttu-id="0f166-253">Recevoir des messages appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="0f166-253">Receive device-to-cloud messages.</span></span> |
| `{iot hub host name}/servicebound/feedback` |<span data-ttu-id="0f166-254">Recevoir des commentaires pour les messages cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="0f166-254">Receive feedback for cloud-to-device messages.</span></span> |
| `{iot hub host name}/devicebound` |<span data-ttu-id="0f166-255">Envoyer des messages cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="0f166-255">Send cloud-to-device messages.</span></span> |

<span data-ttu-id="0f166-256">Par exemple, un service de génération à l’aide de hello créé au préalable partagé appelée stratégie d’accès **registryRead** créerait un jeton avec hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="0f166-256">As an example, a service generating using hello pre-created shared access policy called **registryRead** would create a token with hello following parameters:</span></span>

* <span data-ttu-id="0f166-257">URI de ressource : `{IoT hub name}.azure-devices.net/devices`,</span><span class="sxs-lookup"><span data-stu-id="0f166-257">resource URI: `{IoT hub name}.azure-devices.net/devices`,</span></span>
* <span data-ttu-id="0f166-258">clé de signature : une des clés de hello Hello `registryRead` stratégie,</span><span class="sxs-lookup"><span data-stu-id="0f166-258">signing key: one of hello keys of hello `registryRead` policy,</span></span>
* <span data-ttu-id="0f166-259">nom de la stratégie : `registryRead`,</span><span class="sxs-lookup"><span data-stu-id="0f166-259">policy name: `registryRead`,</span></span>
* <span data-ttu-id="0f166-260">n’importe quelle heure d’expiration.</span><span class="sxs-lookup"><span data-stu-id="0f166-260">any expiration time.</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="0f166-261">résultat de Hello, qui vous accordez l’accès tooread toutes les identités d’appareil, serait :</span><span class="sxs-lookup"><span data-stu-id="0f166-261">hello result, which would grant access tooread all device identities, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a><span data-ttu-id="0f166-262">Certificats X.509 pris en charge</span><span class="sxs-lookup"><span data-stu-id="0f166-262">Supported X.509 certificates</span></span>

<span data-ttu-id="0f166-263">Vous pouvez utiliser n’importe quel tooauthenticate de certificat X.509 un périphérique avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0f166-263">You can use any X.509 certificate tooauthenticate a device with IoT Hub.</span></span> <span data-ttu-id="0f166-264">Les certificats incluent :</span><span class="sxs-lookup"><span data-stu-id="0f166-264">Certificates include:</span></span>

* <span data-ttu-id="0f166-265">**un certificat X.509 existant**.</span><span class="sxs-lookup"><span data-stu-id="0f166-265">**An existing X.509 certificate**.</span></span> <span data-ttu-id="0f166-266">Un appareil peut être déjà associé à un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="0f166-266">A device may already have an X.509 certificate associated with it.</span></span> <span data-ttu-id="0f166-267">Appareil de Hello peut utiliser des tooauthenticate de ce certificat avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0f166-267">hello device can use this certificate tooauthenticate with IoT Hub.</span></span>
* <span data-ttu-id="0f166-268">**un certificat X-509 généré et signé automatiquement**.</span><span class="sxs-lookup"><span data-stu-id="0f166-268">**A self-generated and self-signed X-509 certificate**.</span></span> <span data-ttu-id="0f166-269">Un fabricant ou le responsable du déploiement en interne peut générer ces certificats et stocker la clé privée hello (et les certificats) sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="0f166-269">A device manufacturer or in-house deployer can generate these certificates and store hello corresponding private key (and certificate) on hello device.</span></span> <span data-ttu-id="0f166-270">Vous pouvez utiliser des outils tels que [OpenSSL][lnk-openssl] ou l’utilitaire [Windows SelfSignedCertificate][lnk-selfsigned] à cette fin ;</span><span class="sxs-lookup"><span data-stu-id="0f166-270">You can use tools such as [OpenSSL][lnk-openssl] and [Windows SelfSignedCertificate][lnk-selfsigned] utility for this purpose.</span></span>
* <span data-ttu-id="0f166-271">**un certificat X.509 signé par une autorité de certification**.</span><span class="sxs-lookup"><span data-stu-id="0f166-271">**CA-signed X.509 certificate**.</span></span> <span data-ttu-id="0f166-272">tooidentify un appareil et de son authentification avec IoT Hub, vous pouvez utiliser un certificat X.509 généré et signé par une autorité de Certification (CA).</span><span class="sxs-lookup"><span data-stu-id="0f166-272">tooidentify a device and authenticate it with IoT Hub, you can use an X.509 certificate generated and signed by a Certification Authority (CA).</span></span> <span data-ttu-id="0f166-273">IoT Hub vérifie uniquement que l’empreinte numérique hello présentée correspond à l’empreinte numérique hello configuré.</span><span class="sxs-lookup"><span data-stu-id="0f166-273">IoT Hub only verifies that hello thumbprint presented matches hello configured thumbprint.</span></span> <span data-ttu-id="0f166-274">IotHub ne valide pas la chaîne de certificats hello.</span><span class="sxs-lookup"><span data-stu-id="0f166-274">IotHub does not validate hello certificate chain.</span></span>

<span data-ttu-id="0f166-275">Un appareil peut utiliser un certificat X.509 ou un jeton de sécurité pour l’authentification, mais pas les deux.</span><span class="sxs-lookup"><span data-stu-id="0f166-275">A device may either use an X.509 certificate or a security token for authentication, but not both.</span></span>

### <a name="register-an-x509-certificate-for-a-device"></a><span data-ttu-id="0f166-276">Inscrire un certificat X.509 pour un appareil</span><span class="sxs-lookup"><span data-stu-id="0f166-276">Register an X.509 certificate for a device</span></span>

<span data-ttu-id="0f166-277">Hello [Azure IoT Service SDK pour c#] [ lnk-service-sdk] (version 1.0.8+) prend en charge l’inscription d’un périphérique qui utilise un certificat X.509 pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="0f166-277">hello [Azure IoT Service SDK for C#][lnk-service-sdk] (version 1.0.8+) supports registering a device that uses an X.509 certificate for authentication.</span></span> <span data-ttu-id="0f166-278">D’autres API telles que l’importation/exportation d’appareils prennent également en charge les certificats X.509.</span><span class="sxs-lookup"><span data-stu-id="0f166-278">Other APIs such as import/export of devices also support X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="0f166-279">Prise en charge de C\#</span><span class="sxs-lookup"><span data-stu-id="0f166-279">C\# Support</span></span>

<span data-ttu-id="0f166-280">Hello **RegistryManager** classe fournit un tooregister par programme un appareil.</span><span class="sxs-lookup"><span data-stu-id="0f166-280">hello **RegistryManager** class provides a programmatic way tooregister a device.</span></span> <span data-ttu-id="0f166-281">En particulier, hello **AddDeviceAsync** et **UpdateDeviceAsync** méthodes vous tooregister et mettre à jour un appareil Bonjour Registre des identités IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0f166-281">In particular, hello **AddDeviceAsync** and **UpdateDeviceAsync** methods enable you tooregister and update a device in hello IoT Hub identity registry.</span></span> <span data-ttu-id="0f166-282">Ces deux méthodes utilisent une instance **Device** comme entrée.</span><span class="sxs-lookup"><span data-stu-id="0f166-282">These two methods take a **Device** instance as input.</span></span> <span data-ttu-id="0f166-283">Hello **périphérique** classe inclut une **authentification** propriété qui vous permet de toospecify principaux et secondaires X.509 empreintes numériques de certificat.</span><span class="sxs-lookup"><span data-stu-id="0f166-283">hello **Device** class includes an **Authentication** property that allows you toospecify primary and secondary X.509 certificate thumbprints.</span></span> <span data-ttu-id="0f166-284">l’empreinte numérique Hello représente un hachage SHA-1 du certificat X.509 de hello (stockée à l’aide du codage de DER binaire).</span><span class="sxs-lookup"><span data-stu-id="0f166-284">hello thumbprint represents a SHA-1 hash of hello X.509 certificate (stored using binary DER encoding).</span></span> <span data-ttu-id="0f166-285">Vous pouvez hello en spécifiant une empreinte numérique du principal ou une empreinte numérique secondaire ou les deux.</span><span class="sxs-lookup"><span data-stu-id="0f166-285">You have hello option of specifying a primary thumbprint or a secondary thumbprint or both.</span></span> <span data-ttu-id="0f166-286">Empreintes numériques de principales et secondaires sont toohandle pris en charge les scénarios de substitution de certificat.</span><span class="sxs-lookup"><span data-stu-id="0f166-286">Primary and secondary thumbprints are supported toohandle certificate rollover scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="0f166-287">IoT Hub ne requiert pas ou ne sont pas stocker le certificat X.509 hello entière, l’empreinte numérique hello uniquement.</span><span class="sxs-lookup"><span data-stu-id="0f166-287">IoT Hub does not require or store hello entire X.509 certificate, only hello thumbprint.</span></span>

<span data-ttu-id="0f166-288">Voici un exemple C\# tooregister d’extrait de code un périphérique à l’aide d’un certificat X.509 :</span><span class="sxs-lookup"><span data-stu-id="0f166-288">Here is a sample C\# code snippet tooregister a device using an X.509 certificate:</span></span>

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

### <a name="use-an-x509-certificate-during-run-time-operations"></a><span data-ttu-id="0f166-289">Utiliser un certificat X.509 pendant les opérations d’exécution</span><span class="sxs-lookup"><span data-stu-id="0f166-289">Use an X.509 certificate during run-time operations</span></span>

<span data-ttu-id="0f166-290">Hello [appareil Azure IoT SDK pour .NET] [ lnk-client-sdk] (version 1.0.11+) prend en charge hello de certificats X.509.</span><span class="sxs-lookup"><span data-stu-id="0f166-290">hello [Azure IoT device SDK for .NET][lnk-client-sdk] (version 1.0.11+) supports hello use of X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="0f166-291">Prise en charge de C\#</span><span class="sxs-lookup"><span data-stu-id="0f166-291">C\# Support</span></span>

<span data-ttu-id="0f166-292">Hello classe **DeviceAuthenticationWithX509Certificate** prend en charge hello la création de **DeviceClient** instances à l’aide d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="0f166-292">hello class **DeviceAuthenticationWithX509Certificate** supports hello creation of **DeviceClient** instances using an X.509 certificate.</span></span> <span data-ttu-id="0f166-293">certificat X.509 de Hello doit être au format PFX (également appelé PKCS #12) hello qui inclut la clé privée de hello.</span><span class="sxs-lookup"><span data-stu-id="0f166-293">hello X.509 certificate must be in hello PFX (also called PKCS #12) format that includes hello private key.</span></span>

<span data-ttu-id="0f166-294">Voici un exemple d’extrait de code :</span><span class="sxs-lookup"><span data-stu-id="0f166-294">Here is a sample code snippet:</span></span>

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a><span data-ttu-id="0f166-295">Authentification d'appareil personnalisée</span><span class="sxs-lookup"><span data-stu-id="0f166-295">Custom device authentication</span></span>

<span data-ttu-id="0f166-296">Vous pouvez utiliser hello IoT Hub [Registre des identités] [ lnk-identity-registry] informations d’identification de sécurité de chaque appareil tooconfigure et contrôle d’accès à l’aide de [jetons] [ lnk-sas-tokens] .</span><span class="sxs-lookup"><span data-stu-id="0f166-296">You can use hello IoT Hub [identity registry][lnk-identity-registry] tooconfigure per-device security credentials and access control using [tokens][lnk-sas-tokens].</span></span> <span data-ttu-id="0f166-297">Si une solution IoT a déjà un schéma de Registre et/ou l’authentification d’identité personnalisée, envisagez de créer un *service de jeton* toointegrate cette infrastructure avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0f166-297">If an IoT solution already has a custom identity registry and/or authentication scheme, consider creating a *token service* toointegrate this infrastructure with IoT Hub.</span></span> <span data-ttu-id="0f166-298">De cette façon, vous pouvez utiliser d'autres fonctionnalités IoT dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="0f166-298">In this way, you can use other IoT features in your solution.</span></span>

<span data-ttu-id="0f166-299">Un service de jeton est un service cloud personnalisé.</span><span class="sxs-lookup"><span data-stu-id="0f166-299">A token service is a custom cloud service.</span></span> <span data-ttu-id="0f166-300">Il utilise un IoT Hub *stratégie d’accès partagé* avec **DeviceConnect** autorisations toocreate *étendue de périphérique* jetons.</span><span class="sxs-lookup"><span data-stu-id="0f166-300">It uses an IoT Hub *shared access policy* with **DeviceConnect** permissions toocreate *device-scoped* tokens.</span></span> <span data-ttu-id="0f166-301">Ces jetons activer un hub IoT de périphérique tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="0f166-301">These tokens enable a device tooconnect tooyour IoT hub.</span></span>

![Étapes du modèle de service de jeton de hello][img-tokenservice]

<span data-ttu-id="0f166-303">Les étapes principales hello hello jeton du modèle de service sont :</span><span class="sxs-lookup"><span data-stu-id="0f166-303">Here are hello main steps of hello token service pattern:</span></span>

1. <span data-ttu-id="0f166-304">Créez une stratégie d’accès partagé IoT Hub avec des autorisations **DeviceConnect** pour votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0f166-304">Create an IoT Hub shared access policy with **DeviceConnect** permissions for your IoT hub.</span></span> <span data-ttu-id="0f166-305">Vous pouvez créer cette stratégie Bonjour [portail Azure] [ lnk-management-portal] ou par programme.</span><span class="sxs-lookup"><span data-stu-id="0f166-305">You can create this policy in hello [Azure portal][lnk-management-portal] or programmatically.</span></span> <span data-ttu-id="0f166-306">service de jeton de Hello utilise cette stratégie toosign hello les jetons qu’il crée.</span><span class="sxs-lookup"><span data-stu-id="0f166-306">hello token service uses this policy toosign hello tokens it creates.</span></span>
1. <span data-ttu-id="0f166-307">Quand un appareil doit tooaccess votre IoT hub, il demande un jeton signé à partir de votre service de jeton.</span><span class="sxs-lookup"><span data-stu-id="0f166-307">When a device needs tooaccess your IoT hub, it requests a signed token from your token service.</span></span> <span data-ttu-id="0f166-308">Appareil de Hello avec peut s’authentifier votre identité d’appareil identité personnalisée Registre/authentification schéma toodetermine hello que service de jeton de hello utilise le jeton de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="0f166-308">hello device can authenticate with your custom identity registry/authentication scheme toodetermine hello device identity that hello token service uses toocreate hello token.</span></span>
1. <span data-ttu-id="0f166-309">service de jeton de Hello retourne un jeton.</span><span class="sxs-lookup"><span data-stu-id="0f166-309">hello token service returns a token.</span></span> <span data-ttu-id="0f166-310">jeton Hello est créé à l’aide de `/devices/{deviceId}` en tant que `resourceURI`, avec `deviceId` en tant que périphérique hello en cours d’authentification.</span><span class="sxs-lookup"><span data-stu-id="0f166-310">hello token is created by using `/devices/{deviceId}` as `resourceURI`, with `deviceId` as hello device being authenticated.</span></span> <span data-ttu-id="0f166-311">service de jeton de Hello utilise le jeton hello tooconstruct hello accès partagé stratégie.</span><span class="sxs-lookup"><span data-stu-id="0f166-311">hello token service uses hello shared access policy tooconstruct hello token.</span></span>
1. <span data-ttu-id="0f166-312">Appareil de Hello utilise le jeton de hello directement avec hello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0f166-312">hello device uses hello token directly with hello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="0f166-313">Vous pouvez utiliser la classe .NET de hello [SharedAccessSignatureBuilder] [ lnk-dotnet-sas] ou hello classe Java [IotHubServiceSasToken] [ lnk-java-sas] toocreate un jeton dans votre service d’émission de jeton.</span><span class="sxs-lookup"><span data-stu-id="0f166-313">You can use hello .NET class [SharedAccessSignatureBuilder][lnk-dotnet-sas] or hello Java class [IotHubServiceSasToken][lnk-java-sas] toocreate a token in your token service.</span></span>

<span data-ttu-id="0f166-314">service de jeton de Hello peut définir l’expiration de jeton hello comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="0f166-314">hello token service can set hello token expiration as desired.</span></span> <span data-ttu-id="0f166-315">Lors de l’expiration du jeton de hello, hub IoT de hello interrompt la connexion de périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="0f166-315">When hello token expires, hello IoT hub severs hello device connection.</span></span> <span data-ttu-id="0f166-316">Ensuite, les appareils hello doivent demander un nouveau jeton à partir du service de jeton de hello.</span><span class="sxs-lookup"><span data-stu-id="0f166-316">Then, hello device must request a new token from hello token service.</span></span> <span data-ttu-id="0f166-317">Un délai d’expiration court augmente la charge hello sur le périphérique de hello et service de jeton de hello.</span><span class="sxs-lookup"><span data-stu-id="0f166-317">A short expiry time increases hello load on both hello device and hello token service.</span></span>

<span data-ttu-id="0f166-318">Pour un concentrateur de tooyour tooconnect du périphérique, vous devez toujours l’ajouter toohello Registre des identités IoT Hub, même si hello appareil utilise un jeton et pas une clé tooconnect de périphérique.</span><span class="sxs-lookup"><span data-stu-id="0f166-318">For a device tooconnect tooyour hub, you must still add it toohello IoT Hub identity registry — even though hello device is using a token and not a device key tooconnect.</span></span> <span data-ttu-id="0f166-319">Par conséquent, vous pouvez continuer le contrôle d’accès par périphérique toouse en activant ou désactivant les identités d’appareil Bonjour [Registre des identités][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="0f166-319">Therefore, you can continue toouse per-device access control by enabling or disabling device identities in hello [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="0f166-320">Cette approche réduit les risques de hello de l’utilisation de jetons avec délais d’expiration longs.</span><span class="sxs-lookup"><span data-stu-id="0f166-320">This approach mitigates hello risks of using tokens with long expiry times.</span></span>

### <a name="comparison-with-a-custom-gateway"></a><span data-ttu-id="0f166-321">Comparaison avec une passerelle personnalisée</span><span class="sxs-lookup"><span data-stu-id="0f166-321">Comparison with a custom gateway</span></span>

<span data-ttu-id="0f166-322">modèle de service de jeton Hello est hello recommandé tooimplement de façon un schéma de Registre / d’authentification d’identité personnalisé avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0f166-322">hello token service pattern is hello recommended way tooimplement a custom identity registry/authentication scheme with IoT Hub.</span></span> <span data-ttu-id="0f166-323">Ce modèle est recommandé, car l’IoT Hub continue toohandle la plupart du trafic de solution hello.</span><span class="sxs-lookup"><span data-stu-id="0f166-323">This pattern is recommended because IoT Hub continues toohandle most of hello solution traffic.</span></span> <span data-ttu-id="0f166-324">Toutefois, si le schéma d’authentification personnalisé hello est donc étroitement avec le protocole de hello, vous pouvez avoir besoin une *passerelle personnalisé* tooprocess tous hello du trafic.</span><span class="sxs-lookup"><span data-stu-id="0f166-324">However, if hello custom authentication scheme is so intertwined with hello protocol, you may require a *custom gateway* tooprocess all hello traffic.</span></span> <span data-ttu-id="0f166-325">[Le protocole TLS (Transport Layer Security) et les clés prépartagées (PSK)][lnk-tls-psk] en sont un exemple.</span><span class="sxs-lookup"><span data-stu-id="0f166-325">An example of such a scenario is using[Transport Layer Security (TLS) and pre-shared keys (PSKs)][lnk-tls-psk].</span></span> <span data-ttu-id="0f166-326">Pour plus d’informations, consultez hello [passerelle de protocole] [ lnk-protocols] rubrique.</span><span class="sxs-lookup"><span data-stu-id="0f166-326">For more information, see hello [protocol gateway][lnk-protocols] topic.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="0f166-327">Rubriques de référence :</span><span class="sxs-lookup"><span data-stu-id="0f166-327">Reference topics:</span></span>

<span data-ttu-id="0f166-328">Hello rubriques de référence suivantes vous fournissent plus d’informations sur tooyour IoT hub de contrôler l’accès.</span><span class="sxs-lookup"><span data-stu-id="0f166-328">hello following reference topics provide you with more information about controlling access tooyour IoT hub.</span></span>

## <a name="iot-hub-permissions"></a><span data-ttu-id="0f166-329">Autorisations IoT Hub</span><span class="sxs-lookup"><span data-stu-id="0f166-329">IoT Hub permissions</span></span>

<span data-ttu-id="0f166-330">Hello tableau suivant répertorie les autorisations hello vous pouvez utiliser toocontrol accès tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0f166-330">hello following table lists hello permissions you can use toocontrol access tooyour IoT hub.</span></span>

| <span data-ttu-id="0f166-331">Autorisation</span><span class="sxs-lookup"><span data-stu-id="0f166-331">Permission</span></span> | <span data-ttu-id="0f166-332">Remarques</span><span class="sxs-lookup"><span data-stu-id="0f166-332">Notes</span></span> |
| --- | --- |
| <span data-ttu-id="0f166-333">**RegistryRead**.</span><span class="sxs-lookup"><span data-stu-id="0f166-333">**RegistryRead**</span></span> |<span data-ttu-id="0f166-334">Registre des identités toohello accorde un accès en lecture.</span><span class="sxs-lookup"><span data-stu-id="0f166-334">Grants read access toohello identity registry.</span></span> <span data-ttu-id="0f166-335">Pour plus d’informations, consultez [Registre des identités][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="0f166-335">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="0f166-336">Cette autorisation est utilisée par les services cloud principaux.</span><span class="sxs-lookup"><span data-stu-id="0f166-336">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="0f166-337">**RegistryReadWrite**.</span><span class="sxs-lookup"><span data-stu-id="0f166-337">**RegistryReadWrite**</span></span> |<span data-ttu-id="0f166-338">Octroie accès en lecture et écriture toohello Registre des identités.</span><span class="sxs-lookup"><span data-stu-id="0f166-338">Grants read and write access toohello identity registry.</span></span> <span data-ttu-id="0f166-339">Pour plus d’informations, consultez [Registre des identités][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="0f166-339">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="0f166-340">Cette autorisation est utilisée par les services cloud principaux.</span><span class="sxs-lookup"><span data-stu-id="0f166-340">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="0f166-341">**ServiceConnect**.</span><span class="sxs-lookup"><span data-stu-id="0f166-341">**ServiceConnect**</span></span> |<span data-ttu-id="0f166-342">Octroie accéder toocloud service orientées communication et la surveillance des points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="0f166-342">Grants access toocloud service-facing communication and monitoring endpoints.</span></span> <br/><span data-ttu-id="0f166-343">Octroie autorisation tooreceive les messages appareil-à-cloud, envoyer des messages cloud-à-appareil et hello récupérer correspondant des accusés de réception de remise.</span><span class="sxs-lookup"><span data-stu-id="0f166-343">Grants permission tooreceive device-to-cloud messages, send cloud-to-device messages, and retrieve hello corresponding delivery acknowledgments.</span></span> <br/><span data-ttu-id="0f166-344">Les téléchargements accorde autorisation tooretrieve remise les accusés de réception pour le fichier.</span><span class="sxs-lookup"><span data-stu-id="0f166-344">Grants permission tooretrieve delivery acknowledgements for file uploads.</span></span> <br/><span data-ttu-id="0f166-345">Octroie autorisation tooaccess appareil jumeaux tooupdate balises et les propriétés souhaitées, récupérer les propriétés déclarées et exécuter des requêtes.</span><span class="sxs-lookup"><span data-stu-id="0f166-345">Grants permission tooaccess device twins tooupdate tags and desired properties, retrieve reported properties, and run queries.</span></span> <br/><span data-ttu-id="0f166-346">Cette autorisation est utilisée par les services cloud principaux.</span><span class="sxs-lookup"><span data-stu-id="0f166-346">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="0f166-347">**DeviceConnect**.</span><span class="sxs-lookup"><span data-stu-id="0f166-347">**DeviceConnect**</span></span> |<span data-ttu-id="0f166-348">Octroie accéder aux points de terminaison toodevice accessibles.</span><span class="sxs-lookup"><span data-stu-id="0f166-348">Grants access toodevice-facing endpoints.</span></span> <br/><span data-ttu-id="0f166-349">Octroie autorisation toosend appareil-à-cloud messages et recevoir des messages cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="0f166-349">Grants permission toosend device-to-cloud messages and receive cloud-to-device messages.</span></span> <br/><span data-ttu-id="0f166-350">Téléchargement du fichier tooperform accorde autorisation à partir d’un appareil.</span><span class="sxs-lookup"><span data-stu-id="0f166-350">Grants permission tooperform file upload from a device.</span></span> <br/><span data-ttu-id="0f166-351">Notifications de la propriété accorde autorisation tooreceive appareil double souhaité et de périphérique de mise à jour à deux propriétés déclarées.</span><span class="sxs-lookup"><span data-stu-id="0f166-351">Grants permission tooreceive device twin desired property notifications and update device twin reported properties.</span></span> <br/><span data-ttu-id="0f166-352">Fichier de tooperform d’autorisations accorde télécharge.</span><span class="sxs-lookup"><span data-stu-id="0f166-352">Grants permission tooperform file uploads.</span></span> <br/><span data-ttu-id="0f166-353">Cette autorisation est utilisée par les appareils.</span><span class="sxs-lookup"><span data-stu-id="0f166-353">This permission is used by devices.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="0f166-354">Matériel de référence supplémentaire</span><span class="sxs-lookup"><span data-stu-id="0f166-354">Additional reference material</span></span>

<span data-ttu-id="0f166-355">Les autres rubriques de référence de hello guide du développeur IoT Hub sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="0f166-355">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="0f166-356">[Points de terminaison IoT Hub] [ lnk-endpoints] décrit hello différents points de terminaison qui expose de chaque IoT hub pour les opérations de gestion et d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0f166-356">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="0f166-357">[Limitation et les quotas] [ lnk-quotas] décrit les quotas hello et la limitation des comportements qui s’appliquent toohello IoT Hub service.</span><span class="sxs-lookup"><span data-stu-id="0f166-357">[Throttling and quotas][lnk-quotas] describes hello quotas and throttling behaviors that apply toohello IoT Hub service.</span></span>
* <span data-ttu-id="0f166-358">[Azure IoT périphérique et service kits de développement logiciel] [ lnk-sdks] listes hello langue différents kits de développement logiciel vous pouvez utiliser lorsque vous développez des applications de périphérique et le service qui interagissent avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0f166-358">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="0f166-359">[Langage de requête IoT Hub] [ lnk-query] décrit le langage de requête hello vous pouvez utiliser les informations de tooretrieve à partir de IoT Hub sur votre jumeaux de périphérique et les travaux.</span><span class="sxs-lookup"><span data-stu-id="0f166-359">[IoT Hub query language][lnk-query] describes hello query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="0f166-360">[Prise en charge IoT Hub MQTT] [ lnk-devguide-mqtt] fournit plus d’informations sur la prise en charge IoT Hub pour le protocole MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="0f166-360">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f166-361">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0f166-361">Next steps</span></span>

<span data-ttu-id="0f166-362">Maintenant vous avez appris comment toocontrol aux IoT Hub, peut vous intéresser hello IoT Hub développeur guide rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="0f166-362">Now you have learned how toocontrol access IoT Hub, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="0f166-363">[Utiliser les configurations et état du périphérique jumeaux toosynchronize][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="0f166-363">[Use device twins toosynchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="0f166-364">[Appeler une méthode directe sur un appareil][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="0f166-364">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="0f166-365">[Planifier des travaux sur plusieurs appareils][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="0f166-365">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="0f166-366">Si vous souhaitez que tootry certains des concepts hello décrits dans cet article, peut vous intéresser hello suivant les didacticiels IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="0f166-366">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorials:</span></span>

* <span data-ttu-id="0f166-367">[Mise en route d’Azure IoT Hub][lnk-getstarted-tutorial]</span><span class="sxs-lookup"><span data-stu-id="0f166-367">[Get started with Azure IoT Hub][lnk-getstarted-tutorial]</span></span>
* <span data-ttu-id="0f166-368">[Comment les messages toosend cloud-à-appareil avec IoT Hub][lnk-c2d-tutorial]</span><span class="sxs-lookup"><span data-stu-id="0f166-368">[How toosend cloud-to-device messages with IoT Hub][lnk-c2d-tutorial]</span></span>
* <span data-ttu-id="0f166-369">[Comment tooprocess les messages appareil-à-cloud IoT Hub][lnk-d2c-tutorial]</span><span class="sxs-lookup"><span data-stu-id="0f166-369">[How tooprocess IoT Hub device-to-cloud messages][lnk-d2c-tutorial]</span></span>

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
