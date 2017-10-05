---
title: "Présentation de la sécurité d’Azure IoT Hub | Microsoft Docs"
description: "Guide du développeur : comment contrôler l’accès à IoT Hub pour les applications d’appareil et applications principales. Inclut des informations sur les jetons de sécurité et la prise en charge des certificats X.509."
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
ms.openlocfilehash: e4fe5400ffcf4446392015aada031dd4dfbf238a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="control-access-to-iot-hub"></a><span data-ttu-id="2e6b5-104">Contrôler l’accès à IoT Hub</span><span class="sxs-lookup"><span data-stu-id="2e6b5-104">Control access to IoT Hub</span></span>

<span data-ttu-id="2e6b5-105">Cet article décrit les options de sécurisation de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-105">This article describes the options for securing your IoT hub.</span></span> <span data-ttu-id="2e6b5-106">IoT Hub utilise des *autorisations* pour accorder l’accès à chaque point de terminaison IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-106">IoT Hub uses *permissions* to grant access to each IoT hub endpoint.</span></span> <span data-ttu-id="2e6b5-107">Les autorisations limitent l’accès à un hub IoT selon la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-107">Permissions limit the access to an IoT hub based on functionality.</span></span>

<span data-ttu-id="2e6b5-108">Cet article explique :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-108">This article describes:</span></span>

* <span data-ttu-id="2e6b5-109">Les différentes autorisations que vous pouvez accorder à une application d’appareil ou de serveur principal pour accéder à votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-109">The different permissions that you can grant to a device or back-end app to access your IoT hub.</span></span>
* <span data-ttu-id="2e6b5-110">Le processus d’authentification et les jetons qu’il utilise pour vérifier les autorisations.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-110">The authentication process and the tokens it uses to verify permissions.</span></span>
* <span data-ttu-id="2e6b5-111">Le mode de définition de l’étendue des informations d’identification pour limiter l’accès à des ressources spécifiques.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-111">How to scope credentials to limit access to specific resources.</span></span>
* <span data-ttu-id="2e6b5-112">La prise en charge par IoT Hub des certificats X.509.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-112">IoT Hub support for X.509 certificates.</span></span>
* <span data-ttu-id="2e6b5-113">Les mécanismes d’authentification d’appareil personnalisés qui utilisent des registres d’identités d’appareil ou des schémas d’authentification existants.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-113">Custom device authentication mechanisms that use existing device identity registries or authentication schemes.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="2e6b5-114">Quand utiliser</span><span class="sxs-lookup"><span data-stu-id="2e6b5-114">When to use</span></span>

<span data-ttu-id="2e6b5-115">Pour accéder à tout point de terminaison IoT Hub, vous devez disposer des autorisations appropriées.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-115">You must have appropriate permissions to access any of the IoT Hub endpoints.</span></span> <span data-ttu-id="2e6b5-116">Par exemple, un appareil doit inclure un jeton contenant des informations d’identification de sécurité dans chaque message envoyé à IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-116">For example, a device must include a token containing security credentials along with every message it sends to IoT Hub.</span></span>

## <a name="access-control-and-permissions"></a><span data-ttu-id="2e6b5-117">Contrôle d’accès et autorisations</span><span class="sxs-lookup"><span data-stu-id="2e6b5-117">Access control and permissions</span></span>

<span data-ttu-id="2e6b5-118">Vous pouvez accorder des [autorisations](#iot-hub-permissions) de différentes manières :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-118">You can grant [permissions](#iot-hub-permissions) in the following ways:</span></span>

* <span data-ttu-id="2e6b5-119">**Stratégies d’accès partagé au niveau d’IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-119">**IoT hub-level shared access policies**.</span></span> <span data-ttu-id="2e6b5-120">Les stratégies d’accès partagé peuvent accorder n’importe quelle combinaison d’[autorisations](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="2e6b5-120">Shared access policies can grant any combination of [permissions](#iot-hub-permissions).</span></span> <span data-ttu-id="2e6b5-121">Vous pouvez définir des stratégies dans le [Portail Azure][lnk-management-portal] ou par programmation à l’aide des [API REST de fournisseur de ressources IoT Hub][lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="2e6b5-121">You can define policies in the [Azure portal][lnk-management-portal], or programmatically by using the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="2e6b5-122">Un hub IoT qui vient d’être créé a les stratégies par défaut suivantes :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-122">A newly created IoT hub has the following default policies:</span></span>

  * <span data-ttu-id="2e6b5-123">**iothubowner**: stratégie jouissant de toutes les autorisations.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-123">**iothubowner**: Policy with all permissions.</span></span>
  * <span data-ttu-id="2e6b5-124">**service** : stratégie jouissant de l’autorisation **ServiceConnect**.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-124">**service**: Policy with **ServiceConnect** permission.</span></span>
  * <span data-ttu-id="2e6b5-125">**device** : stratégie jouissant de l’autorisation **DeviceConnect**.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-125">**device**: Policy with **DeviceConnect** permission.</span></span>
  * <span data-ttu-id="2e6b5-126">**registryRead** : stratégie jouissant de l’autorisation **RegistryRead**.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-126">**registryRead**: Policy with **RegistryRead** permission.</span></span>
  * <span data-ttu-id="2e6b5-127">**registryReadWrite** : stratégie jouissant des autorisations **RegistryRead** et RegistryWrite.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-127">**registryReadWrite**: Policy with **RegistryRead** and RegistryWrite permissions.</span></span>
  * <span data-ttu-id="2e6b5-128">**Informations d’identification de sécurité par appareil**.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-128">**Per-device security credentials**.</span></span> <span data-ttu-id="2e6b5-129">Chaque hub IoT contient un [registre des identités][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="2e6b5-129">Each IoT Hub contains an [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="2e6b5-130">Pour chaque appareil figurant dans ce registre des identités, vous pouvez configurer des informations d’identification de sécurité qui accordent des autorisations **DeviceConnect** incluses dans l’étendue des points de terminaison des appareils correspondants.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-130">For each device in this identity registry, you can configure security credentials that grant **DeviceConnect** permissions scoped to the corresponding device endpoints.</span></span>

<span data-ttu-id="2e6b5-131">Par exemple, dans une solution IoT classique :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-131">For example, in a typical IoT solution:</span></span>

* <span data-ttu-id="2e6b5-132">Le composant de gestion des appareils utilise la stratégie *registryReadWrite* .</span><span class="sxs-lookup"><span data-stu-id="2e6b5-132">The device management component uses the *registryReadWrite* policy.</span></span>
* <span data-ttu-id="2e6b5-133">Le composant de processeur d’événements utilise la stratégie *service* .</span><span class="sxs-lookup"><span data-stu-id="2e6b5-133">The event processor component uses the *service* policy.</span></span>
* <span data-ttu-id="2e6b5-134">Le composant de logique métier des appareils d’exécution utilise la stratégie *service*.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-134">The run-time device business logic component uses the *service* policy.</span></span>
* <span data-ttu-id="2e6b5-135">Les appareils individuels se connectent à l’aide d’informations d’identification stockées dans le registre des identités du hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-135">Individual devices connect using credentials stored in the IoT hub's identity registry.</span></span>

> [!NOTE]
> <span data-ttu-id="2e6b5-136">Pour plus d’informations, consultez la page [Autorisations](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="2e6b5-136">See [permissions](#iot-hub-permissions) for detailed information.</span></span>

## <a name="authentication"></a><span data-ttu-id="2e6b5-137">Authentification</span><span class="sxs-lookup"><span data-stu-id="2e6b5-137">Authentication</span></span>

<span data-ttu-id="2e6b5-138">Azure IoT Hub accorde l’accès aux points de terminaison en vérifiant un jeton par rapport aux stratégies d’accès partagé et aux informations d’identification de sécurité du registre des identités.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-138">Azure IoT Hub grants access to endpoints by verifying a token against the shared access policies and identity registry security credentials.</span></span>

<span data-ttu-id="2e6b5-139">Les informations d’identification de sécurité telles que les clés symétriques ne sont jamais envoyées sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-139">Security credentials, such as symmetric keys, are never sent over the wire.</span></span>

> [!NOTE]
> <span data-ttu-id="2e6b5-140">Le fournisseur de ressources Azure IoT Hub est sécurisé au moyen de votre abonnement Azure, à l’instar de tous les fournisseurs dans [Azure Resource Manager][lnk-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="2e6b5-140">The Azure IoT Hub resource provider is secured through your Azure subscription, as are all providers in the [Azure Resource Manager][lnk-azure-resource-manager].</span></span>

<span data-ttu-id="2e6b5-141">Pour plus d’informations sur la construction et l’utilisation des jetons de sécurité, consultez [Jetons de sécurité IoT Hub][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="2e6b5-141">For more information about how to construct and use security tokens, see [IoT Hub security tokens][lnk-sas-tokens].</span></span>

### <a name="protocol-specifics"></a><span data-ttu-id="2e6b5-142">Spécifications de protocole</span><span class="sxs-lookup"><span data-stu-id="2e6b5-142">Protocol specifics</span></span>

<span data-ttu-id="2e6b5-143">Chaque protocole pris en charge (par exemple, MQTT, AMQP et HTTP) transporte des jetons de différentes façons.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-143">Each supported protocol, such as MQTT, AMQP, and HTTP, transports tokens in different ways.</span></span>

<span data-ttu-id="2e6b5-144">Lorsque vous utilisez MQTT, le paquet CONNECT utilise deviceid en tant que ClientId, {iothubhostname}/{deviceId} dans le champ Nom d’utilisateur et un jeton SAP dans le champ Mot de passe.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-144">When using MQTT, the CONNECT packet has the deviceId as the ClientId, {iothubhostname}/{deviceId} in the Username field, and a SAS token in the Password field.</span></span> <span data-ttu-id="2e6b5-145">{iothubhostname} doit être le nom canonique (CNAME) complet d’IoT Hub (par exemple, contoso.azure-devices.net).</span><span class="sxs-lookup"><span data-stu-id="2e6b5-145">{iothubhostname} should be the full CName of the IoT hub (for example, contoso.azure-devices.net).</span></span>

<span data-ttu-id="2e6b5-146">Lorsque vous utilisez [AMQP][lnk-amqp], IoT Hub prend en charge [SASL PLAIN][lnk-sasl-plain] et la [sécurité basée sur des revendications AMQP][lnk-cbs].</span><span class="sxs-lookup"><span data-stu-id="2e6b5-146">When using [AMQP][lnk-amqp], IoT Hub supports [SASL PLAIN][lnk-sasl-plain] and [AMQP Claims-Based-Security][lnk-cbs].</span></span>

<span data-ttu-id="2e6b5-147">Si vous utilisez une sécurité basée sur des revendications AMQP, la norme indique comment transmettre les jetons répertoriés ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-147">If you use AMQP claims-based-security, the standard specifies how to transmit these tokens.</span></span>

<span data-ttu-id="2e6b5-148">Pour SASL PLAIN, le **nom d’utilisateur** peut être :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-148">For SASL PLAIN, the **username** can be:</span></span>

* <span data-ttu-id="2e6b5-149">`{policyName}@sas.root.{iothubName}` si vous utilisez des jetons au niveau du hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-149">`{policyName}@sas.root.{iothubName}` if using IoT hub-level tokens.</span></span>
* <span data-ttu-id="2e6b5-150">`{deviceId}@sas.{iothubname}` si vous utilisez des jetons à l’échelle de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-150">`{deviceId}@sas.{iothubname}` if using device-scoped tokens.</span></span>

<span data-ttu-id="2e6b5-151">Dans les deux cas, le champ de mot de passe contient le jeton, comme le décrit [Jetons de sécurité IoT Hub][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="2e6b5-151">In both cases, the password field contains the token, as described in [IoT Hub security tokens][lnk-sas-tokens].</span></span>

<span data-ttu-id="2e6b5-152">Le protocole HTTP implémente l’authentification en incluant un jeton valide dans l’en-tête de demande **Authorization** .</span><span class="sxs-lookup"><span data-stu-id="2e6b5-152">HTTP implements authentication by including a valid token in the **Authorization** request header.</span></span>

#### <a name="example"></a><span data-ttu-id="2e6b5-153">Exemple</span><span class="sxs-lookup"><span data-stu-id="2e6b5-153">Example</span></span>

<span data-ttu-id="2e6b5-154">Nom d’utilisateur (DeviceId respecte la casse) : `iothubname.azure-devices.net/DeviceId`</span><span class="sxs-lookup"><span data-stu-id="2e6b5-154">Username (DeviceId is case-sensitive): `iothubname.azure-devices.net/DeviceId`</span></span>

<span data-ttu-id="2e6b5-155">Mot de passe (générer le jeton SAP avec l’outil [Explorateur d’appareils][lnk-device-explorer]) : `SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span><span class="sxs-lookup"><span data-stu-id="2e6b5-155">Password (Generate SAS token with the [device explorer][lnk-device-explorer] tool): `SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span></span>

> [!NOTE]
> <span data-ttu-id="2e6b5-156">Les kits [Azure IoT SDK][lnk-sdks] génèrent automatiquement des jetons lors de la connexion au service.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-156">The [Azure IoT SDKs][lnk-sdks] automatically generate tokens when connecting to the service.</span></span> <span data-ttu-id="2e6b5-157">Dans certains cas, les kits Azure IoT SDK ne prennent pas en charge l’ensemble des protocoles ou méthodes d’authentification.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-157">In some cases, the Azure IoT SDKs do not support all the protocols or all the authentication methods.</span></span>

### <a name="special-considerations-for-sasl-plain"></a><span data-ttu-id="2e6b5-158">Considérations spécifiques concernant SASL PLAIN</span><span class="sxs-lookup"><span data-stu-id="2e6b5-158">Special considerations for SASL PLAIN</span></span>

<span data-ttu-id="2e6b5-159">Lorsque vous utilisez SASL PLAIN avec AMQP, un client qui se connecte à un IoT Hub peut utiliser un jeton unique pour chaque connexion TCP.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-159">When using SASL PLAIN with AMQP, a client connecting to an IoT hub can use a single token for each TCP connection.</span></span> <span data-ttu-id="2e6b5-160">Lorsque le jeton expire, la connexion TCP est déconnectée du service, ce qui déclenche une reconnexion.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-160">When the token expires, the TCP connection disconnects from the service and triggers a reconnect.</span></span> <span data-ttu-id="2e6b5-161">Bien que non problématique pour une application principale, ce comportement peut créer des dommages pour une application d’appareil pour les motifs suivants :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-161">This behavior, while not problematic for a back-end app, is damaging for a device app for the following reasons:</span></span>

* <span data-ttu-id="2e6b5-162">Les passerelles se connectent généralement au nom de nombreux appareils.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-162">Gateways usually connect on behalf of many devices.</span></span> <span data-ttu-id="2e6b5-163">Lorsque vous utilisez SASL PLAIN, elles doivent créer une connexion TCP distincte pour chaque appareil se connectant à un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-163">When using SASL PLAIN, they have to create a distinct TCP connection for each device connecting to an IoT hub.</span></span> <span data-ttu-id="2e6b5-164">Ce scénario augmente considérablement la consommation des ressources d’alimentation et de mise en réseau, ainsi que la latence de chaque connexion d’appareil.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-164">This scenario considerably increases the consumption of power and networking resources, and increases the latency of each device connection.</span></span>
* <span data-ttu-id="2e6b5-165">Les appareils avec des contraintes de ressources sont affectés par l’utilisation accrue des ressources pour se reconnecter après chaque expiration du jeton.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-165">Resource-constrained devices are adversely affected by the increased use of resources to reconnect after each token expiration.</span></span>

## <a name="scope-iot-hub-level-credentials"></a><span data-ttu-id="2e6b5-166">Étendue des informations d’identification au niveau du hub IoT</span><span class="sxs-lookup"><span data-stu-id="2e6b5-166">Scope IoT hub-level credentials</span></span>

<span data-ttu-id="2e6b5-167">Vous pouvez étendre les stratégies de sécurité au niveau du hub IoT en créant des jetons avec un URI de ressource restreint.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-167">You can scope IoT hub-level security policies by creating tokens with a restricted resource URI.</span></span> <span data-ttu-id="2e6b5-168">Par exemple, le point de terminaison pour l’envoi de messages appareil-à-cloud est **/devices/{deviceId}/messages/events**.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-168">For example, the endpoint to send device-to-cloud messages from a device is **/devices/{deviceId}/messages/events**.</span></span> <span data-ttu-id="2e6b5-169">Vous pouvez également utiliser une stratégie d’accès partagé au niveau du hub IoT avec des autorisations **DeviceConnect** pour signer un jeton dont l’URI de ressource est **/devices/{deviceId}**.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-169">You can also use an IoT hub-level shared access policy with **DeviceConnect** permissions to sign a token whose resourceURI is **/devices/{deviceId}**.</span></span> <span data-ttu-id="2e6b5-170">Cette approche crée un jeton utilisable uniquement pour envoyer des messages au nom de l’appareil **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-170">This approach creates a token that is only usable to send messages on behalf of device **deviceId**.</span></span>

<span data-ttu-id="2e6b5-171">Il s’agit d’un mécanisme semblable à la [Stratégie de publication d’Event Hubs][lnk-event-hubs-publisher-policy] qui vous permet d’implémenter des méthodes d’authentification personnalisées.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-171">This mechanism is similar to the [Event Hubs publisher policy][lnk-event-hubs-publisher-policy], and enables you to implement custom authentication methods.</span></span>

## <a name="security-tokens"></a><span data-ttu-id="2e6b5-172">Jetons de sécurité</span><span class="sxs-lookup"><span data-stu-id="2e6b5-172">Security tokens</span></span>

<span data-ttu-id="2e6b5-173">IoT Hub utilise des jetons de sécurité pour authentifier les appareils et les services afin d’éviter d’envoyer des clés sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-173">IoT Hub uses security tokens to authenticate devices and services to avoid sending keys on the wire.</span></span> <span data-ttu-id="2e6b5-174">En outre, la validité et la portée des jetons sont limitées dans le temps.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-174">Additionally, security tokens are limited in time validity and scope.</span></span> <span data-ttu-id="2e6b5-175">Les kits [Azure IoT SDK ][lnk-sdks] génèrent automatiquement les jetons sans configuration spéciale.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-175">[Azure IoT SDKs][lnk-sdks] automatically generate tokens without requiring any special configuration.</span></span> <span data-ttu-id="2e6b5-176">Certains scénarios nécessitent toutefois que vous génériez et utilisiez directement des jetons de sécurité.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-176">Some scenarios do require you to generate and use security tokens directly.</span></span> <span data-ttu-id="2e6b5-177">Il s’agit entre autres des scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-177">Such scenarios include:</span></span>

* <span data-ttu-id="2e6b5-178">Utilisation directe des surfaces MQTT, AMQP ou HTTP</span><span class="sxs-lookup"><span data-stu-id="2e6b5-178">The direct use of the MQTT, AMQP, or HTTP surfaces.</span></span>
* <span data-ttu-id="2e6b5-179">Implémentation du modèle de service de jeton, comme expliqué dans [Authentification d’appareil personnalisée][lnk-custom-auth].</span><span class="sxs-lookup"><span data-stu-id="2e6b5-179">The implementation of the token service pattern, as explained in [Custom device authentication][lnk-custom-auth].</span></span>

<span data-ttu-id="2e6b5-180">IoT Hub permet également aux appareils de s’authentifier avec IoT Hub à l’aide de [certificats X.509][lnk-x509].</span><span class="sxs-lookup"><span data-stu-id="2e6b5-180">IoT Hub also allows devices to authenticate with IoT Hub using [X.509 certificates][lnk-x509].</span></span>

### <a name="security-token-structure"></a><span data-ttu-id="2e6b5-181">Structure du jeton de sécurité</span><span class="sxs-lookup"><span data-stu-id="2e6b5-181">Security token structure</span></span>

<span data-ttu-id="2e6b5-182">Vous utilisez des jetons de sécurité pour accorder un accès limité dans le temps aux appareils et aux services à des fonctionnalités spécifiques dans IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-182">You use security tokens to grant time-bounded access to devices and services to specific functionality in IoT Hub.</span></span> <span data-ttu-id="2e6b5-183">Pour obtenir l’autorisation de se connecter à IoT Hub, les appareils et services doivent envoyer des jetons de sécurité signés avec une clé symétrique ou d’accès partagé.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-183">To get authorization to connect to IoT Hub, devices and services must send security tokens signed with either a shared access or symmetric key.</span></span> <span data-ttu-id="2e6b5-184">Ces clés sont stockées avec l’identité de l’appareil dans le registre de l’identité.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-184">These keys are stored with a device identity in the identity registry.</span></span>

<span data-ttu-id="2e6b5-185">Un jeton signé avec une clé d’accès partagé accorde un accès à toutes les fonctionnalités associées aux autorisations de stratégie d’accès partagé.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-185">A token signed with a shared access key grants access to all the functionality associated with the shared access policy permissions.</span></span> <span data-ttu-id="2e6b5-186">Un jeton signé avec la clé symétrique de l’identité de l’appareil accorde uniquement l’autorisation **DeviceConnect** à l’identité de l’appareil associée.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-186">A token signed with a device identity's symmetric key only grants the **DeviceConnect** permission for the associated device identity.</span></span>

<span data-ttu-id="2e6b5-187">Le jeton de sécurité présente le format suivant :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-187">The security token has the following format:</span></span>

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

<span data-ttu-id="2e6b5-188">Voici les valeurs attendues :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-188">Here are the expected values:</span></span>

| <span data-ttu-id="2e6b5-189">Valeur</span><span class="sxs-lookup"><span data-stu-id="2e6b5-189">Value</span></span> | <span data-ttu-id="2e6b5-190">Description</span><span class="sxs-lookup"><span data-stu-id="2e6b5-190">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2e6b5-191">{signature}</span><span class="sxs-lookup"><span data-stu-id="2e6b5-191">{signature}</span></span> |<span data-ttu-id="2e6b5-192">Une chaîne de signature HMAC-SHA256 sous la forme : `{URL-encoded-resourceURI} + "\n" + expiry`.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-192">An HMAC-SHA256 signature string of the form: `{URL-encoded-resourceURI} + "\n" + expiry`.</span></span> <span data-ttu-id="2e6b5-193">**Important**: la clé est décodée à partir de base64 et utilisée comme clé pour effectuer le calcul HMAC-SHA256.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-193">**Important**: The key is decoded from base64 and used as key to perform the HMAC-SHA256 computation.</span></span> |
| <span data-ttu-id="2e6b5-194">{resourceURI}</span><span class="sxs-lookup"><span data-stu-id="2e6b5-194">{resourceURI}</span></span> |<span data-ttu-id="2e6b5-195">Préfixe URI (par segment) des points de terminaison qui sont accessibles avec ce jeton, en commençant par le nom d’hôte IoT Hub (sans protocole).</span><span class="sxs-lookup"><span data-stu-id="2e6b5-195">URI prefix (by segment) of the endpoints that can be accessed with this token, starting with host name of the IoT hub (no protocol).</span></span> <span data-ttu-id="2e6b5-196">Par exemple, `myHub.azure-devices.net/devices/device1`</span><span class="sxs-lookup"><span data-stu-id="2e6b5-196">For example, `myHub.azure-devices.net/devices/device1`</span></span> |
| <span data-ttu-id="2e6b5-197">{expiry}</span><span class="sxs-lookup"><span data-stu-id="2e6b5-197">{expiry}</span></span> |<span data-ttu-id="2e6b5-198">Chaînes UTF8 pour le nombre de secondes depuis l’époque 00:00:00 UTC 1er janvier 1970.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-198">UTF8 strings for number of seconds since the epoch 00:00:00 UTC on 1 January 1970.</span></span> |
| <span data-ttu-id="2e6b5-199">{URL-encoded-resourceURI}</span><span class="sxs-lookup"><span data-stu-id="2e6b5-199">{URL-encoded-resourceURI}</span></span> |<span data-ttu-id="2e6b5-200">Encodage en URL minuscules de l’URI de ressource en minuscules</span><span class="sxs-lookup"><span data-stu-id="2e6b5-200">Lower case URL-encoding of the lower case resource URI</span></span> |
| <span data-ttu-id="2e6b5-201">{policyName}</span><span class="sxs-lookup"><span data-stu-id="2e6b5-201">{policyName}</span></span> |<span data-ttu-id="2e6b5-202">Le nom de la stratégie d’accès partagé à laquelle ce jeton fait référence.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-202">The name of the shared access policy to which this token refers.</span></span> <span data-ttu-id="2e6b5-203">Il n’y en a pas si le jeton fait référence aux informations d’identification de registre des appareils.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-203">Absent if the token refers to device-registry credentials.</span></span> |

<span data-ttu-id="2e6b5-204">**Remarque sur le préfixe**: le préfixe URI est calculé par segment et non par caractère.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-204">**Note on prefix**: The URI prefix is computed by segment and not by character.</span></span> <span data-ttu-id="2e6b5-205">Par exemple `/a/b` est un préfixe de `/a/b/c`, mais pas de `/a/bc`.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-205">For example `/a/b` is a prefix for `/a/b/c` but not for `/a/bc`.</span></span>

<span data-ttu-id="2e6b5-206">L’extrait de code Node.js suivant illustre une fonction appelée **generateSasToken** qui calcule le jeton à partir des entrées `resourceUri, signingKey, policyName, expiresInMins`.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-206">The following Node.js snippet shows a function called **generateSasToken** that computes the token from the inputs `resourceUri, signingKey, policyName, expiresInMins`.</span></span> <span data-ttu-id="2e6b5-207">Les sections suivantes décrivent en détail comment initialiser les différentes entrées pour les différents cas d’utilisation des jetons.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-207">The next sections detail how to initialize the different inputs for the different token use cases.</span></span>

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

<span data-ttu-id="2e6b5-208">À titre de comparaison, le code Python équivalent pour générer un jeton de sécurité est :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-208">As a comparison, the equivalent Python code to generate a security token is:</span></span>

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
> <span data-ttu-id="2e6b5-209">Étant donné que la validité du jeton est validée sur les ordinateurs IoT Hub, la dérive de l’horloge de l’ordinateur qui génère le jeton doit être minime.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-209">Since the time validity of the token is validated on IoT Hub machines, the drift on the clock of the machine that generates the token must be minimal.</span></span>

### <a name="use-sas-tokens-in-a-device-app"></a><span data-ttu-id="2e6b5-210">Utiliser des jetons SPA dans une application d’appareil</span><span class="sxs-lookup"><span data-stu-id="2e6b5-210">Use SAS tokens in a device app</span></span>

<span data-ttu-id="2e6b5-211">Il existe deux façons d’obtenir des autorisations **DeviceConnect** avec IoT Hub au moyen de jetons de sécurité : utiliser une [clé d’appareil symétrique extraite du registre des identités](#use-a-symmetric-key-in-the-identity-registry) ou une [clé d’accès partagé](#use-a-shared-access-policy).</span><span class="sxs-lookup"><span data-stu-id="2e6b5-211">There are two ways to obtain **DeviceConnect** permissions with IoT Hub with security tokens: use a [symmetric device key from the identity registry](#use-a-symmetric-key-in-the-identity-registry), or use a [shared access key](#use-a-shared-access-policy).</span></span>

<span data-ttu-id="2e6b5-212">N’oubliez pas que toutes les fonctionnalités accessibles à partir des appareils sont exposées par définition sur les points de terminaison avec le préfixe `/devices/{deviceId}`.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-212">Remember that all functionality accessible from devices is exposed by design on endpoints with prefix `/devices/{deviceId}`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e6b5-213">La seule façon dont IoT Hub authentifie un appareil est à l’aide de la clé symétrique d’identité de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-213">The only way that IoT Hub authenticates a specific device is using the device identity symmetric key.</span></span> <span data-ttu-id="2e6b5-214">Dans le cas où une stratégie d’accès partagé est utilisée pour accéder aux fonctionnalités de l’appareil, la solution doit prendre en compte le composant émettant le jeton de sécurité en tant que sous-composant approuvé.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-214">In cases when a shared access policy is used to access device functionality, the solution must consider the component issuing the security token as a trusted subcomponent.</span></span>

<span data-ttu-id="2e6b5-215">Les points de terminaison côté appareil sont (quel que soit le protocole) :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-215">The device-facing endpoints are (irrespective of the protocol):</span></span>

| <span data-ttu-id="2e6b5-216">Point de terminaison</span><span class="sxs-lookup"><span data-stu-id="2e6b5-216">Endpoint</span></span> | <span data-ttu-id="2e6b5-217">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="2e6b5-217">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |<span data-ttu-id="2e6b5-218">Envoyer des messages appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-218">Send device-to-cloud messages.</span></span> |
| `{iot hub host name}/devices/{deviceId}/devicebound` |<span data-ttu-id="2e6b5-219">Recevoir des messages cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-219">Receive cloud-to-device messages.</span></span> |

### <a name="use-a-symmetric-key-in-the-identity-registry"></a><span data-ttu-id="2e6b5-220">Utilisation d’une clé symétrique dans le registre d’identité</span><span class="sxs-lookup"><span data-stu-id="2e6b5-220">Use a symmetric key in the identity registry</span></span>

<span data-ttu-id="2e6b5-221">Lorsqu’une clé symétrique d’identité de l’appareil est utilisée pour générer un jeton, l’élément PolicyName (`skn`) du jeton est omis.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-221">When using a device identity's symmetric key to generate a token, the policyName (`skn`) element of the token is omitted.</span></span>

<span data-ttu-id="2e6b5-222">Par exemple, un jeton créé pour accéder à toutes les fonctionnalités de l’appareil doit avoir les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-222">For example, a token created to access all device functionality should have the following parameters:</span></span>

* <span data-ttu-id="2e6b5-223">URI de ressource : `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="2e6b5-223">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="2e6b5-224">clé de signature : n’importe quelle clé symétrique pour l’identité `{device id}` ,</span><span class="sxs-lookup"><span data-stu-id="2e6b5-224">signing key: any symmetric key for the `{device id}` identity,</span></span>
* <span data-ttu-id="2e6b5-225">pas de nom de stratégie,</span><span class="sxs-lookup"><span data-stu-id="2e6b5-225">no policy name,</span></span>
* <span data-ttu-id="2e6b5-226">n’importe quelle heure d’expiration.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-226">any expiration time.</span></span>

<span data-ttu-id="2e6b5-227">Un exemple d’utilisation de la fonction Node.js précédente serait :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-227">An example using the preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

<span data-ttu-id="2e6b5-228">Le résultat, qui accorde l’accès à toutes les fonctionnalités de device1, est alors :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-228">The result, which grants access to all functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> <span data-ttu-id="2e6b5-229">Il est possible de générer un jeton SAP à l’aide de l’outil [Explorateur d’appareils][lnk-device-explorer] .NET ou de l’utilitaire de ligne de commande multiplateforme et basé sur des nœuds [iothub-explorer][lnk-iothub-explorer].</span><span class="sxs-lookup"><span data-stu-id="2e6b5-229">It is possible to generate a SAS token using the .NET [device explorer][lnk-device-explorer] tool or the cross-platform, node-based [iothub-explorer][lnk-iothub-explorer] command-line utility.</span></span>

### <a name="use-a-shared-access-policy"></a><span data-ttu-id="2e6b5-230">Utilisation d’une stratégie d’accès partagé</span><span class="sxs-lookup"><span data-stu-id="2e6b5-230">Use a shared access policy</span></span>

<span data-ttu-id="2e6b5-231">Quand vous créez un jeton à partir d’une stratégie d’accès partagé, spécifiez le nom de la stratégie dans le champ `skn`.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-231">When you create a token from a shared access policy, set the `skn` field to the name of the policy.</span></span> <span data-ttu-id="2e6b5-232">Cette stratégie doit accorder l’autorisation **DeviceConnect**.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-232">This policy must grant the **DeviceConnect** permission.</span></span>

<span data-ttu-id="2e6b5-233">Les deux principaux scénarios pour l’utilisation de stratégies d’accès partagé pour accéder aux fonctionnalités de l’appareil sont :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-233">The two main scenarios for using shared access policies to access device functionality are:</span></span>

* <span data-ttu-id="2e6b5-234">[passerelles de protocole cloud][lnk-endpoints],</span><span class="sxs-lookup"><span data-stu-id="2e6b5-234">[cloud protocol gateways][lnk-endpoints],</span></span>
* <span data-ttu-id="2e6b5-235">[services de jeton][lnk-custom-auth] utilisés pour implémenter des schémas d’authentification personnalisés.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-235">[token services][lnk-custom-auth] used to implement custom authentication schemes.</span></span>

<span data-ttu-id="2e6b5-236">Étant donné que la stratégie d’accès partagé peut potentiellement accorder un accès pour se connecter comme n’importe quel appareil, il est important d’utiliser l’URI de ressource correct lors de la création de jetons de sécurité.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-236">Since the shared access policy can potentially grant access to connect as any device, it is important to use the correct resource URI when creating security tokens.</span></span> <span data-ttu-id="2e6b5-237">Ce paramètre est particulièrement important pour les services de jeton dont il faut définir l’étendue pour un appareil spécifique à l’aide de l’URI de ressource.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-237">This setting is especially important for token services, which have to scope the token to a specific device using the resource URI.</span></span> <span data-ttu-id="2e6b5-238">Ce point est moins important pour les passerelles de protocole, car elles interceptent déjà le trafic pour tous les appareils.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-238">This point is less relevant for protocol gateways as they are already mediating traffic for all devices.</span></span>

<span data-ttu-id="2e6b5-239">Par exemple, un service de jeton utilisant la stratégie d’accès partagé précréée appelée **device** crée un jeton avec les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-239">As an example, a token service using the pre-created shared access policy called **device** would create a token with the following parameters:</span></span>

* <span data-ttu-id="2e6b5-240">URI de ressource : `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="2e6b5-240">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="2e6b5-241">clé de signature : une des clés de la stratégie `device` ,</span><span class="sxs-lookup"><span data-stu-id="2e6b5-241">signing key: one of the keys of the `device` policy,</span></span>
* <span data-ttu-id="2e6b5-242">nom de la stratégie : `device`,</span><span class="sxs-lookup"><span data-stu-id="2e6b5-242">policy name: `device`,</span></span>
* <span data-ttu-id="2e6b5-243">n’importe quelle heure d’expiration.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-243">any expiration time.</span></span>

<span data-ttu-id="2e6b5-244">Un exemple d’utilisation de la fonction Node.js précédente serait :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-244">An example using the preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="2e6b5-245">Le résultat, qui accorde l’accès à toutes les fonctionnalités de device1, est alors :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-245">The result, which grants access to all functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

<span data-ttu-id="2e6b5-246">Une passerelle de protocole peut utiliser le même jeton pour tous les appareils en définissant simplement l’URI de ressource sur `myhub.azure-devices.net/devices`.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-246">A protocol gateway could use the same token for all devices simply setting the resource URI to `myhub.azure-devices.net/devices`.</span></span>

### <a name="use-security-tokens-from-service-components"></a><span data-ttu-id="2e6b5-247">Utilisation de jetons de sécurité de composants du service</span><span class="sxs-lookup"><span data-stu-id="2e6b5-247">Use security tokens from service components</span></span>

<span data-ttu-id="2e6b5-248">Les composants de service peuvent uniquement créer des jetons de sécurité utilisant des stratégies d’accès partagé pour accorder les autorisations adaptées, comme expliqué précédemment.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-248">Service components can only generate security tokens using shared access policies granting the appropriate permissions as explained previously.</span></span>

<span data-ttu-id="2e6b5-249">Voici les fonctions de service exposées sur les points de terminaison :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-249">Here is the service functions exposed on the endpoints:</span></span>

| <span data-ttu-id="2e6b5-250">Point de terminaison</span><span class="sxs-lookup"><span data-stu-id="2e6b5-250">Endpoint</span></span> | <span data-ttu-id="2e6b5-251">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="2e6b5-251">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices` |<span data-ttu-id="2e6b5-252">Créer, mettre à jour, récupérer et supprimer les identités des appareils.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-252">Create, update, retrieve, and delete device identities.</span></span> |
| `{iot hub host name}/messages/events` |<span data-ttu-id="2e6b5-253">Recevoir des messages appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-253">Receive device-to-cloud messages.</span></span> |
| `{iot hub host name}/servicebound/feedback` |<span data-ttu-id="2e6b5-254">Recevoir des commentaires pour les messages cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-254">Receive feedback for cloud-to-device messages.</span></span> |
| `{iot hub host name}/devicebound` |<span data-ttu-id="2e6b5-255">Envoyer des messages cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-255">Send cloud-to-device messages.</span></span> |

<span data-ttu-id="2e6b5-256">Par exemple, un service qui génère à l’aide de la stratégie d’accès partagé précréée appelée **registryRead** crée un jeton avec les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-256">As an example, a service generating using the pre-created shared access policy called **registryRead** would create a token with the following parameters:</span></span>

* <span data-ttu-id="2e6b5-257">URI de ressource : `{IoT hub name}.azure-devices.net/devices`,</span><span class="sxs-lookup"><span data-stu-id="2e6b5-257">resource URI: `{IoT hub name}.azure-devices.net/devices`,</span></span>
* <span data-ttu-id="2e6b5-258">clé de signature : une des clés de la stratégie `registryRead` ,</span><span class="sxs-lookup"><span data-stu-id="2e6b5-258">signing key: one of the keys of the `registryRead` policy,</span></span>
* <span data-ttu-id="2e6b5-259">nom de la stratégie : `registryRead`,</span><span class="sxs-lookup"><span data-stu-id="2e6b5-259">policy name: `registryRead`,</span></span>
* <span data-ttu-id="2e6b5-260">n’importe quelle heure d’expiration.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-260">any expiration time.</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="2e6b5-261">Le résultat, qui revient à accorder l’accès en lecture à toutes les identités des appareils, est alors :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-261">The result, which would grant access to read all device identities, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a><span data-ttu-id="2e6b5-262">Certificats X.509 pris en charge</span><span class="sxs-lookup"><span data-stu-id="2e6b5-262">Supported X.509 certificates</span></span>

<span data-ttu-id="2e6b5-263">Vous pouvez utiliser n’importe quel certificat X.509 pour authentifier un appareil sur IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-263">You can use any X.509 certificate to authenticate a device with IoT Hub.</span></span> <span data-ttu-id="2e6b5-264">Les certificats incluent :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-264">Certificates include:</span></span>

* <span data-ttu-id="2e6b5-265">**un certificat X.509 existant**.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-265">**An existing X.509 certificate**.</span></span> <span data-ttu-id="2e6b5-266">Un appareil peut être déjà associé à un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-266">A device may already have an X.509 certificate associated with it.</span></span> <span data-ttu-id="2e6b5-267">L’appareil peut utiliser ce certificat pour s’authentifier sur IoT Hub ;</span><span class="sxs-lookup"><span data-stu-id="2e6b5-267">The device can use this certificate to authenticate with IoT Hub.</span></span>
* <span data-ttu-id="2e6b5-268">**un certificat X-509 généré et signé automatiquement**.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-268">**A self-generated and self-signed X-509 certificate**.</span></span> <span data-ttu-id="2e6b5-269">Un fabricant d’appareils ou un technicien de déploiement en interne peut générer ces certificats et stocker la clé privée correspondante (ainsi que le certificat) sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-269">A device manufacturer or in-house deployer can generate these certificates and store the corresponding private key (and certificate) on the device.</span></span> <span data-ttu-id="2e6b5-270">Vous pouvez utiliser des outils tels que [OpenSSL][lnk-openssl] ou l’utilitaire [Windows SelfSignedCertificate][lnk-selfsigned] à cette fin ;</span><span class="sxs-lookup"><span data-stu-id="2e6b5-270">You can use tools such as [OpenSSL][lnk-openssl] and [Windows SelfSignedCertificate][lnk-selfsigned] utility for this purpose.</span></span>
* <span data-ttu-id="2e6b5-271">**un certificat X.509 signé par une autorité de certification**.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-271">**CA-signed X.509 certificate**.</span></span> <span data-ttu-id="2e6b5-272">Pour identifier un appareil et l’authentifier auprès de IoT Hub, vous pouvez utiliser un certificat X.509 généré et signé par une autorité de certification.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-272">To identify a device and authenticate it with IoT Hub, you can use an X.509 certificate generated and signed by a Certification Authority (CA).</span></span> <span data-ttu-id="2e6b5-273">IoT Hub vérifie seulement que l’empreinte présentée correspond à l’empreinte configurée.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-273">IoT Hub only verifies that the thumbprint presented matches the configured thumbprint.</span></span> <span data-ttu-id="2e6b5-274">Il valide ensuite la chaîne de certificats.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-274">IotHub does not validate the certificate chain.</span></span>

<span data-ttu-id="2e6b5-275">Un appareil peut utiliser un certificat X.509 ou un jeton de sécurité pour l’authentification, mais pas les deux.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-275">A device may either use an X.509 certificate or a security token for authentication, but not both.</span></span>

### <a name="register-an-x509-certificate-for-a-device"></a><span data-ttu-id="2e6b5-276">Inscrire un certificat X.509 pour un appareil</span><span class="sxs-lookup"><span data-stu-id="2e6b5-276">Register an X.509 certificate for a device</span></span>

<span data-ttu-id="2e6b5-277">[Azure IoT service SDK pour C#][lnk-service-sdk] (version 1.0.8+) prend en charge l’inscription d’un appareil qui utilise un certificat X.509 pour s’authentifier.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-277">The [Azure IoT Service SDK for C#][lnk-service-sdk] (version 1.0.8+) supports registering a device that uses an X.509 certificate for authentication.</span></span> <span data-ttu-id="2e6b5-278">D’autres API telles que l’importation/exportation d’appareils prennent également en charge les certificats X.509.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-278">Other APIs such as import/export of devices also support X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="2e6b5-279">Prise en charge de C\#</span><span class="sxs-lookup"><span data-stu-id="2e6b5-279">C\# Support</span></span>

<span data-ttu-id="2e6b5-280">La classe **RegistryManager** offre un moyen d’inscrire un appareil dans le cadre d’un programme.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-280">The **RegistryManager** class provides a programmatic way to register a device.</span></span> <span data-ttu-id="2e6b5-281">Les méthodes **AddDeviceAsync** et **UpdateDeviceAsync** vous permettent de vous inscrire et mettre à jour un appareil dans le registre des identités IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-281">In particular, the **AddDeviceAsync** and **UpdateDeviceAsync** methods enable you to register and update a device in the IoT Hub identity registry.</span></span> <span data-ttu-id="2e6b5-282">Ces deux méthodes utilisent une instance **Device** comme entrée.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-282">These two methods take a **Device** instance as input.</span></span> <span data-ttu-id="2e6b5-283">La classe **Device** inclut une propriété **Authentication** qui vous permet de spécifier les empreintes de certificats X.509 primaires et secondaires.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-283">The **Device** class includes an **Authentication** property that allows you to specify primary and secondary X.509 certificate thumbprints.</span></span> <span data-ttu-id="2e6b5-284">L’empreinte numérique représente un hachage SHA-1 du certificat X.509 (stocké à l’aide d’un codage DER binaire).</span><span class="sxs-lookup"><span data-stu-id="2e6b5-284">The thumbprint represents a SHA-1 hash of the X.509 certificate (stored using binary DER encoding).</span></span> <span data-ttu-id="2e6b5-285">Vous pouvez spécifier une empreinte numérique principale et/ou une empreinte numérique secondaire.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-285">You have the option of specifying a primary thumbprint or a secondary thumbprint or both.</span></span> <span data-ttu-id="2e6b5-286">Les empreintes numériques principales et secondaires sont prises en charge pour la gestion des scénarios de substitution de certificat.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-286">Primary and secondary thumbprints are supported to handle certificate rollover scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="2e6b5-287">IoT Hub ne requiert ni ne stocke le certificat X.509 dans son intégralité, mais uniquement l’empreinte numérique.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-287">IoT Hub does not require or store the entire X.509 certificate, only the thumbprint.</span></span>

<span data-ttu-id="2e6b5-288">Voici un exemple d’extrait de code C\# permettant d’inscrire un appareil à l’aide d’un certificat X.509 :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-288">Here is a sample C\# code snippet to register a device using an X.509 certificate:</span></span>

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

### <a name="use-an-x509-certificate-during-run-time-operations"></a><span data-ttu-id="2e6b5-289">Utiliser un certificat X.509 pendant les opérations d’exécution</span><span class="sxs-lookup"><span data-stu-id="2e6b5-289">Use an X.509 certificate during run-time operations</span></span>

<span data-ttu-id="2e6b5-290">[Azure IoT device SDK pour .NET][lnk-client-sdk] (version 1.0.11+) prend en charge l’utilisation de certificats X.509.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-290">The [Azure IoT device SDK for .NET][lnk-client-sdk] (version 1.0.11+) supports the use of X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="2e6b5-291">Prise en charge de C\#</span><span class="sxs-lookup"><span data-stu-id="2e6b5-291">C\# Support</span></span>

<span data-ttu-id="2e6b5-292">La classe **DeviceAuthenticationWithX509Certificate** prend en charge la création d’instances **DeviceClient** à l’aide d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-292">The class **DeviceAuthenticationWithX509Certificate** supports the creation of **DeviceClient** instances using an X.509 certificate.</span></span> <span data-ttu-id="2e6b5-293">Le certificat X.509 doit être au format PFX (également appelé PKCS #12) qui inclut la clé privée.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-293">The X.509 certificate must be in the PFX (also called PKCS #12) format that includes the private key.</span></span>

<span data-ttu-id="2e6b5-294">Voici un exemple d’extrait de code :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-294">Here is a sample code snippet:</span></span>

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a><span data-ttu-id="2e6b5-295">Authentification d'appareil personnalisée</span><span class="sxs-lookup"><span data-stu-id="2e6b5-295">Custom device authentication</span></span>

<span data-ttu-id="2e6b5-296">Vous pouvez utiliser le [registre des identités][lnk-identity-registry] IoT Hub pour configurer les informations d’identification de sécurité et le contrôle d’accès par appareil à l’aide de [jetons][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="2e6b5-296">You can use the IoT Hub [identity registry][lnk-identity-registry] to configure per-device security credentials and access control using [tokens][lnk-sas-tokens].</span></span> <span data-ttu-id="2e6b5-297">Si une solution IoT a déjà un registre des identités et/ou un schéma d’authentification personnalisé, vous pouvez créer un *service de jeton* pour intégrer cette infrastructure existante à IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-297">If an IoT solution already has a custom identity registry and/or authentication scheme, consider creating a *token service* to integrate this infrastructure with IoT Hub.</span></span> <span data-ttu-id="2e6b5-298">De cette façon, vous pouvez utiliser d'autres fonctionnalités IoT dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-298">In this way, you can use other IoT features in your solution.</span></span>

<span data-ttu-id="2e6b5-299">Un service de jeton est un service cloud personnalisé.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-299">A token service is a custom cloud service.</span></span> <span data-ttu-id="2e6b5-300">Il utilise une *stratégie d’accès partagé* IoT Hub avec des autorisations **DeviceConnect** pour créer des jetons *device-scoped*.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-300">It uses an IoT Hub *shared access policy* with **DeviceConnect** permissions to create *device-scoped* tokens.</span></span> <span data-ttu-id="2e6b5-301">Ces jetons permettent à un appareil de se connecter à votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-301">These tokens enable a device to connect to your IoT hub.</span></span>

![Étapes du modèle de service de jeton][img-tokenservice]

<span data-ttu-id="2e6b5-303">Voici les principales étapes du schéma de service de jeton :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-303">Here are the main steps of the token service pattern:</span></span>

1. <span data-ttu-id="2e6b5-304">Créez une stratégie d’accès partagé IoT Hub avec des autorisations **DeviceConnect** pour votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-304">Create an IoT Hub shared access policy with **DeviceConnect** permissions for your IoT hub.</span></span> <span data-ttu-id="2e6b5-305">Vous pouvez créer cette stratégie dans le [Portail Azure][lnk-management-portal] ou par programme.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-305">You can create this policy in the [Azure portal][lnk-management-portal] or programmatically.</span></span> <span data-ttu-id="2e6b5-306">Le service de jetons utilise cette stratégie pour signer les jetons qu'elle crée.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-306">The token service uses this policy to sign the tokens it creates.</span></span>
1. <span data-ttu-id="2e6b5-307">Lorsqu'un appareil doit accéder à votre hub IoT, il demande à votre service de jetons un jeton signé.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-307">When a device needs to access your IoT hub, it requests a signed token from your token service.</span></span> <span data-ttu-id="2e6b5-308">L’appareil peut s’authentifier avec votre registre des identités personnalisé/schéma d’authentification pour déterminer l’identité d’appareil que le service de jeton utilise pour créer le jeton.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-308">The device can authenticate with your custom identity registry/authentication scheme to determine the device identity that the token service uses to create the token.</span></span>
1. <span data-ttu-id="2e6b5-309">Le service de jeton renvoie un jeton.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-309">The token service returns a token.</span></span> <span data-ttu-id="2e6b5-310">Le jeton est créé en utilisant `/devices/{deviceId}` en tant qu’`resourceURI`, avec `deviceId` en tant qu’appareil en cours d’authentification.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-310">The token is created by using `/devices/{deviceId}` as `resourceURI`, with `deviceId` as the device being authenticated.</span></span> <span data-ttu-id="2e6b5-311">Le service de jeton utilise la stratégie d'accès partagé pour construire le jeton.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-311">The token service uses the shared access policy to construct the token.</span></span>
1. <span data-ttu-id="2e6b5-312">L’appareil utilise le jeton directement avec le hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-312">The device uses the token directly with the IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="2e6b5-313">Vous pouvez utiliser la classe .NET [SharedAccessSignatureBuilder][lnk-dotnet-sas] ou la classe Java [IotHubServiceSasToken][lnk-java-sas] pour créer un jeton dans votre service de jeton.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-313">You can use the .NET class [SharedAccessSignatureBuilder][lnk-dotnet-sas] or the Java class [IotHubServiceSasToken][lnk-java-sas] to create a token in your token service.</span></span>

<span data-ttu-id="2e6b5-314">Le service de jetons peut définir l’expiration du jeton comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-314">The token service can set the token expiration as desired.</span></span> <span data-ttu-id="2e6b5-315">Lorsque le jeton expire, le hub IoT interrompt la connexion.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-315">When the token expires, the IoT hub severs the device connection.</span></span> <span data-ttu-id="2e6b5-316">L’appareil doit ensuite demander un nouveau jeton au service de jeton.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-316">Then, the device must request a new token from the token service.</span></span> <span data-ttu-id="2e6b5-317">Un délai d'expiration court accroît la charge de l'appareil et du service de jeton.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-317">A short expiry time increases the load on both the device and the token service.</span></span>

<span data-ttu-id="2e6b5-318">Pour qu’un appareil se connecte à votre hub, vous devez l’ajouter au registre des identités IoT Hub, même si l’appareil utilise un jeton et non une clé d’appareil pour se connecter.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-318">For a device to connect to your hub, you must still add it to the IoT Hub identity registry — even though the device is using a token and not a device key to connect.</span></span> <span data-ttu-id="2e6b5-319">Ainsi, vous pouvez continuer à utiliser le contrôle d’accès par appareil en activant ou désactivant les identités des appareils dans le [Registre des identités][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="2e6b5-319">Therefore, you can continue to use per-device access control by enabling or disabling device identities in the [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="2e6b5-320">Cette approche réduit les risques liés à l'utilisation de jetons avec des délais d'expiration longs.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-320">This approach mitigates the risks of using tokens with long expiry times.</span></span>

### <a name="comparison-with-a-custom-gateway"></a><span data-ttu-id="2e6b5-321">Comparaison avec une passerelle personnalisée</span><span class="sxs-lookup"><span data-stu-id="2e6b5-321">Comparison with a custom gateway</span></span>

<span data-ttu-id="2e6b5-322">Le modèle de service de jeton est la méthode recommandée pour implémenter un schéma de registre d’identité/d’authentification avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-322">The token service pattern is the recommended way to implement a custom identity registry/authentication scheme with IoT Hub.</span></span> <span data-ttu-id="2e6b5-323">Ce modèle est recommandé car il laisse IoT Hub gérer la plupart du trafic de la solution.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-323">This pattern is recommended because IoT Hub continues to handle most of the solution traffic.</span></span> <span data-ttu-id="2e6b5-324">Toutefois, si l’entrelacement entre le schéma d’authentification personnalisé et le protocole SSL est conséquent, vous aurez peut-être besoin d’une *passerelle personnalisée* pour traiter tout le trafic.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-324">However, if the custom authentication scheme is so intertwined with the protocol, you may require a *custom gateway* to process all the traffic.</span></span> <span data-ttu-id="2e6b5-325">[Le protocole TLS (Transport Layer Security) et les clés prépartagées (PSK)][lnk-tls-psk] en sont un exemple.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-325">An example of such a scenario is using[Transport Layer Security (TLS) and pre-shared keys (PSKs)][lnk-tls-psk].</span></span> <span data-ttu-id="2e6b5-326">Pour plus d’informations, consultez la rubrique [Passerelle de protocole][lnk-protocols].</span><span class="sxs-lookup"><span data-stu-id="2e6b5-326">For more information, see the [protocol gateway][lnk-protocols] topic.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="2e6b5-327">Rubriques de référence :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-327">Reference topics:</span></span>

<span data-ttu-id="2e6b5-328">Les rubriques de référence suivantes vous fournissent des informations supplémentaires sur le contrôle de l’accès à votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-328">The following reference topics provide you with more information about controlling access to your IoT hub.</span></span>

## <a name="iot-hub-permissions"></a><span data-ttu-id="2e6b5-329">Autorisations IoT Hub</span><span class="sxs-lookup"><span data-stu-id="2e6b5-329">IoT Hub permissions</span></span>

<span data-ttu-id="2e6b5-330">Le tableau suivant répertorie les autorisations que vous pouvez utiliser pour contrôler l’accès à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-330">The following table lists the permissions you can use to control access to your IoT hub.</span></span>

| <span data-ttu-id="2e6b5-331">Autorisation</span><span class="sxs-lookup"><span data-stu-id="2e6b5-331">Permission</span></span> | <span data-ttu-id="2e6b5-332">Remarques</span><span class="sxs-lookup"><span data-stu-id="2e6b5-332">Notes</span></span> |
| --- | --- |
| <span data-ttu-id="2e6b5-333">**RegistryRead**.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-333">**RegistryRead**</span></span> |<span data-ttu-id="2e6b5-334">Accorde l’accès en lecture au registre des identités.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-334">Grants read access to the identity registry.</span></span> <span data-ttu-id="2e6b5-335">Pour plus d’informations, consultez [Registre des identités][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="2e6b5-335">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="2e6b5-336">Cette autorisation est utilisée par les services cloud principaux.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-336">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="2e6b5-337">**RegistryReadWrite**.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-337">**RegistryReadWrite**</span></span> |<span data-ttu-id="2e6b5-338">Accorde l’accès en lecture et en écriture au registre des identités.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-338">Grants read and write access to the identity registry.</span></span> <span data-ttu-id="2e6b5-339">Pour plus d’informations, consultez [Registre des identités][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="2e6b5-339">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="2e6b5-340">Cette autorisation est utilisée par les services cloud principaux.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-340">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="2e6b5-341">**ServiceConnect**.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-341">**ServiceConnect**</span></span> |<span data-ttu-id="2e6b5-342">Accorde l’accès à la communication de services cloud et à la surveillance des points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-342">Grants access to cloud service-facing communication and monitoring endpoints.</span></span> <br/><span data-ttu-id="2e6b5-343">Accorde l’autorisation de recevoir des messages appareil-à-cloud, d’envoyer des messages cloud-à-appareil et de récupérer les accusés de remise correspondants.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-343">Grants permission to receive device-to-cloud messages, send cloud-to-device messages, and retrieve the corresponding delivery acknowledgments.</span></span> <br/><span data-ttu-id="2e6b5-344">Accorde l’autorisation de récupérer les accusés de remise pour les chargements de fichiers.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-344">Grants permission to retrieve delivery acknowledgements for file uploads.</span></span> <br/><span data-ttu-id="2e6b5-345">Accorde l’autorisation d’accéder aux jumeaux d’appareil pour mettre à jour les balises et les propriétés voulues, de récupérer les propriétés signalées et d’exécuter des requêtes.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-345">Grants permission to access device twins to update tags and desired properties, retrieve reported properties, and run queries.</span></span> <br/><span data-ttu-id="2e6b5-346">Cette autorisation est utilisée par les services cloud principaux.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-346">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="2e6b5-347">**DeviceConnect**.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-347">**DeviceConnect**</span></span> |<span data-ttu-id="2e6b5-348">Accorde l’accès aux points de terminaison côté appareil.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-348">Grants access to device-facing endpoints.</span></span> <br/><span data-ttu-id="2e6b5-349">Accorde l’autorisation d’envoyer des messages appareil-à-cloud et de recevoir des messages cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-349">Grants permission to send device-to-cloud messages and receive cloud-to-device messages.</span></span> <br/><span data-ttu-id="2e6b5-350">Accorde l’autorisation d’effectuer un chargement de fichiers à partir d’un appareil.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-350">Grants permission to perform file upload from a device.</span></span> <br/><span data-ttu-id="2e6b5-351">Accorde l’autorisation de recevoir des notifications de propriétés voulues pour les jumeaux d’appareil et de mettre à jour les propriétés signalées pour les jumeaux d’appareil.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-351">Grants permission to receive device twin desired property notifications and update device twin reported properties.</span></span> <br/><span data-ttu-id="2e6b5-352">Accorde l’autorisation d’effectuer des chargements de fichiers.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-352">Grants permission to perform file uploads.</span></span> <br/><span data-ttu-id="2e6b5-353">Cette autorisation est utilisée par les appareils.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-353">This permission is used by devices.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="2e6b5-354">Matériel de référence supplémentaire</span><span class="sxs-lookup"><span data-stu-id="2e6b5-354">Additional reference material</span></span>

<span data-ttu-id="2e6b5-355">Les autres rubriques de référence dans le Guide du développeur IoT Hub comprennent :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-355">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="2e6b5-356">La rubrique [Points de terminaison IoT Hub][lnk-endpoints] décrit les différents points de terminaison que chaque IoT Hub expose pour les opérations d’exécution et de gestion.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-356">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="2e6b5-357">La rubrique [Référence - Quotas et limitation IoT Hub][lnk-quotas] décrit les quotas et le comportement de limitation qui s’appliquent au service IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-357">[Throttling and quotas][lnk-quotas] describes the quotas and throttling behaviors that apply to the IoT Hub service.</span></span>
* <span data-ttu-id="2e6b5-358">La section [Azure IoT device et service SDK][lnk-sdks] répertorie les Kits de développement logiciel (SDK) en différents langages que vous pouvez utiliser pour le développement d’applications d’appareil et de service qui interagissent avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-358">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="2e6b5-359">La rubrique [Référence - Langage de requête IoT Hub pour les jumeaux d’appareil, les travaux et le routage des messages][lnk-query] décrit le langage de requête permettant de récupérer à partir d’IoT Hub des informations sur des jumeaux d’appareil et des travaux.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-359">[IoT Hub query language][lnk-query] describes the query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="2e6b5-360">La rubrique [Prise en charge de MQTT au niveau d’IoT Hub][lnk-devguide-mqtt] fournit des informations supplémentaires sur la prise en charge du protocole MQTT par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2e6b5-360">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e6b5-361">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2e6b5-361">Next steps</span></span>

<span data-ttu-id="2e6b5-362">À présent que vous savez comment contrôler l’accès à IoT Hub, vous serez peut-être intéressé par les rubriques suivantes du Guide du développeur IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-362">Now you have learned how to control access IoT Hub, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="2e6b5-363">[Utiliser des jumeaux d’appareil pour synchroniser les données d’état et de configuration][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="2e6b5-363">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="2e6b5-364">[Appeler une méthode directe sur un appareil][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="2e6b5-364">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="2e6b5-365">[Planifier des travaux sur plusieurs appareils][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="2e6b5-365">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="2e6b5-366">Si vous souhaitez tenter de mettre en pratique certains des concepts décrits dans cet article, vous serez peut-être intéressé par les didacticiels IoT Hub suivants :</span><span class="sxs-lookup"><span data-stu-id="2e6b5-366">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorials:</span></span>

* <span data-ttu-id="2e6b5-367">[Mise en route d’Azure IoT Hub][lnk-getstarted-tutorial]</span><span class="sxs-lookup"><span data-stu-id="2e6b5-367">[Get started with Azure IoT Hub][lnk-getstarted-tutorial]</span></span>
* <span data-ttu-id="2e6b5-368">[Envoyer des messages cloud-à-appareil avec IoT Hub][lnk-c2d-tutorial]</span><span class="sxs-lookup"><span data-stu-id="2e6b5-368">[How to send cloud-to-device messages with IoT Hub][lnk-c2d-tutorial]</span></span>
* <span data-ttu-id="2e6b5-369">[Traiter les messages appareil-à-cloud IoT Hub][lnk-d2c-tutorial]</span><span class="sxs-lookup"><span data-stu-id="2e6b5-369">[How to process IoT Hub device-to-cloud messages][lnk-d2c-tutorial]</span></span>

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
