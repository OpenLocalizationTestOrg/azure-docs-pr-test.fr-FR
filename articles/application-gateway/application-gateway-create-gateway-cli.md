---
title: "aaaCreate une passerelle d’Application Azure - Azure CLI 2.0 | Documents Microsoft"
description: "Découvrez comment toocreate une passerelle d’Application à l’aide de hello Azure CLI 2.0 dans le Gestionnaire de ressources"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 952065586cd87d253882438bb779b768d9fd59fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli-20"></a><span data-ttu-id="dedff-103">Créer une passerelle d’application à l’aide de hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="dedff-103">Create an application gateway by using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="dedff-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="dedff-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="dedff-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dedff-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="dedff-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="dedff-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="dedff-107">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dedff-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="dedff-108">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="dedff-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="dedff-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="dedff-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="dedff-110">Application Gateway est une appliance virtuelle dédiée qui intègre Application Delivery Controller (ADC) en tant que service, offrant diverses fonctionnalités d’équilibrage de charge de couche 7 pour votre application.</span><span class="sxs-lookup"><span data-stu-id="dedff-110">Application Gateway is a dedicated virtual appliance that provides application delivery controller (ADC) as a service, offering various layer 7 load balancing capabilities for your application.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="dedff-111">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="dedff-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="dedff-112">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="dedff-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="dedff-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) -notre CLI pour les modèles de déploiement gestion classique et les ressources des hello.</span><span class="sxs-lookup"><span data-stu-id="dedff-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="dedff-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="dedff-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="dedff-115">Condition préalable : Installez hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="dedff-115">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="dedff-116">les étapes tooperform hello dans cet article, vous devez trop[installer hello Interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="dedff-116">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

> [!NOTE]
> <span data-ttu-id="dedff-117">Si vous n’avez pas de compte Azure, vous devez vous en procurer un.</span><span class="sxs-lookup"><span data-stu-id="dedff-117">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="dedff-118">Inscrivez-vous à un [essai gratuit ici](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="dedff-118">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="dedff-119">Scénario</span><span class="sxs-lookup"><span data-stu-id="dedff-119">Scenario</span></span>

<span data-ttu-id="dedff-120">Dans ce scénario, vous découvrez comment une passerelle d’application à l’aide de toocreate hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dedff-120">In this scenario, you learn how toocreate an application gateway using hello Azure portal.</span></span>

<span data-ttu-id="dedff-121">Ce scénario va :</span><span class="sxs-lookup"><span data-stu-id="dedff-121">This scenario will:</span></span>

* <span data-ttu-id="dedff-122">créer une passerelle Application Gateway moyenne avec deux instances ;</span><span class="sxs-lookup"><span data-stu-id="dedff-122">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="dedff-123">créer un réseau virtuel nommé AdatumAppGatewayVNET avec un bloc CIDR réservé de 10.0.0.0/16 ;</span><span class="sxs-lookup"><span data-stu-id="dedff-123">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="dedff-124">créer un sous-réseau appelé Appgatewaysubnet qui utilise 10.0.0.0/28 comme bloc CIDR ;</span><span class="sxs-lookup"><span data-stu-id="dedff-124">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="dedff-125">Les tests de configuration supplémentaires de la passerelle d’application hello, y compris l’intégrité personnalisée, les adresses du pool principal et des règles supplémentaires sont configurés après la configuration de la passerelle d’application hello et non pendant le déploiement initial.</span><span class="sxs-lookup"><span data-stu-id="dedff-125">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dedff-126">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="dedff-126">Before you begin</span></span>

<span data-ttu-id="dedff-127">La passerelle Application Gateway Azure requiert son propre sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="dedff-127">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="dedff-128">Lorsque vous créez un réseau virtuel, assurez-vous que vous laissez suffisamment toohave d’espace adresse plusieurs sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="dedff-128">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="dedff-129">Une fois que vous déployez un tooa de sous-réseau de la passerelle d’application, passerelles d’application uniquement supplémentaires peuvent être ajoutées toohello sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="dedff-129">Once you deploy an application gateway tooa subnet, only additional application gateways can be added toohello subnet.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="dedff-130">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="dedff-130">Log in tooAzure</span></span>

<span data-ttu-id="dedff-131">Ouvrez hello **invite de commandes Microsoft Azure**et les journaux.</span><span class="sxs-lookup"><span data-stu-id="dedff-131">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="dedff-132">Vous pouvez également utiliser `az login` sans commutateur hello pour la connexion de périphérique qui requiert la saisie d’un code à aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="dedff-132">You can also use `az login` without hello switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="dedff-133">Une fois que vous tapez hello précédent exemple, un code est fourni.</span><span class="sxs-lookup"><span data-stu-id="dedff-133">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="dedff-134">Accédez toohttps://aka.ms/devicelogin dans un processus de connexion de navigateur toocontinue hello.</span><span class="sxs-lookup"><span data-stu-id="dedff-134">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![Invite de commande affichant le code de l’appareil][1]

<span data-ttu-id="dedff-136">Dans le navigateur de hello, entrez le code hello que vous avez reçu.</span><span class="sxs-lookup"><span data-stu-id="dedff-136">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="dedff-137">Vous êtes redirigé tooa-page de connexion.</span><span class="sxs-lookup"><span data-stu-id="dedff-137">You are redirected tooa sign-in page.</span></span>

![code de tooenter du navigateur][2]

<span data-ttu-id="dedff-139">Une fois que le code de hello a été entré. vous êtes connecté, fermer hello navigateur toocontinue avec le scénario hello.</span><span class="sxs-lookup"><span data-stu-id="dedff-139">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![Connexion réussie][3]

## <a name="create-hello-resource-group"></a><span data-ttu-id="dedff-141">Créer le groupe de ressources hello</span><span class="sxs-lookup"><span data-stu-id="dedff-141">Create hello resource group</span></span>

<span data-ttu-id="dedff-142">Avant de créer la passerelle d’application hello, un groupe de ressources est créé de passerelle d’application toocontain hello.</span><span class="sxs-lookup"><span data-stu-id="dedff-142">Before creating hello application gateway, a resource group is created toocontain hello application gateway.</span></span> <span data-ttu-id="dedff-143">Hello Voici commande hello.</span><span class="sxs-lookup"><span data-stu-id="dedff-143">hello following shows hello command.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="dedff-144">Créer une passerelle d’application hello</span><span class="sxs-lookup"><span data-stu-id="dedff-144">Create hello application gateway</span></span>

<span data-ttu-id="dedff-145">Hello IP adresses utilisées pour hello principal sont hello pour votre serveur principal.</span><span class="sxs-lookup"><span data-stu-id="dedff-145">hello IP addresses used for hello backend are hello IP addresses for your backend server.</span></span> <span data-ttu-id="dedff-146">Ces valeurs peuvent être des deux adresses IP privées dans le réseau virtuel de hello, des adresses IP publiques ou des noms de domaine complet pour vos serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="dedff-146">These values can be either private IPs in hello virtual network, public ips, or fully qualified domain names for your backend servers.</span></span> <span data-ttu-id="dedff-147">Hello exemple suivant crée une passerelle d’application avec les paramètres de configuration supplémentaires pour les paramètres http, les ports et les règles.</span><span class="sxs-lookup"><span data-stu-id="dedff-147">hello following example creates an application gateway with additional configuration settings for http settings, ports, and rules.</span></span>

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet" \
--subnet-address-prefix "10.0.0.0/28" \
--servers 10.0.0.4 10.0.0.5 \
--capacity 2 \
--sku Standard_Small \
--http-settings-cookie-based-affinity Enabled \
--http-settings-protocol Http \
--frontend-port 80 \
--routing-rule-type Basic \
--http-settings-port 80 \
--public-ip-address "pip2" \
--public-ip-address-allocation "dynamic" \

```

<span data-ttu-id="dedff-148">Hello exemple précédent montre plusieurs propriétés qui ne sont pas requises lors de la création de hello d’une passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="dedff-148">hello preceding example shows many properties that are not required during hello creation of an application gateway.</span></span> <span data-ttu-id="dedff-149">Hello, exemple de code suivant crée une passerelle d’application avec les informations de hello requis.</span><span class="sxs-lookup"><span data-stu-id="dedff-149">hello following code example creates an application gateway with hello required information.</span></span>

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet \
--subnet-address-prefix "10.0.0.0/28" \
--servers "10.0.0.5"  \
--public-ip-address pip
```
 
> [!NOTE]
> <span data-ttu-id="dedff-150">Pour obtenir la liste de paramètres qui peuvent être fournies au cours de hello création exécuter commande suivante : `az network application-gateway create --help`.</span><span class="sxs-lookup"><span data-stu-id="dedff-150">For a list of parameters that can be provided during creation run hello following command: `az network application-gateway create --help`.</span></span>

<span data-ttu-id="dedff-151">Cet exemple crée une passerelle d’application de base avec les paramètres par défaut pour l’écouteur de hello, pool principal, paramètres http du serveur principal et les règles.</span><span class="sxs-lookup"><span data-stu-id="dedff-151">This example creates a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="dedff-152">Vous pouvez modifier ces paramètres toosuit votre déploiement une fois l’approvisionnement de hello réussie.</span><span class="sxs-lookup"><span data-stu-id="dedff-152">You can modify these settings toosuit your deployment once hello provisioning is successful.</span></span>
<span data-ttu-id="dedff-153">Si vous avez déjà votre application web définie avec le pool principal d’hello Bonjour précédentes étapes, une fois créés, l’équilibrage de charge démarre.</span><span class="sxs-lookup"><span data-stu-id="dedff-153">If you already have your web application defined with hello backend pool in hello preceding steps, once created, load balancing begins.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="dedff-154">Obtenir le nom DNS d’une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="dedff-154">Get application gateway DNS name</span></span>

<span data-ttu-id="dedff-155">Après la création de la passerelle de hello, hello prochaine étape consiste tooconfigure hello frontal pour la communication.</span><span class="sxs-lookup"><span data-stu-id="dedff-155">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="dedff-156">Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial.</span><span class="sxs-lookup"><span data-stu-id="dedff-156">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="dedff-157">les utilisateurs finaux de tooensure pouvez atteindre la passerelle d’application hello, un enregistrement CNAME peut être le point de terminaison utilisé toopoint toohello public de la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="dedff-157">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="dedff-158">[Configuration d’un nom de domaine personnalisé pour Azure](../dns/dns-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="dedff-158">[Configuring a custom domain name for in Azure](../dns/dns-custom-domain.md).</span></span> <span data-ttu-id="dedff-159">tooconfigure un alias, de récupérer les détails de la passerelle d’application hello et son nom IP/DNS associé à l’aide de la passerelle d’application hello PublicIPAddress élément attaché toohello.</span><span class="sxs-lookup"><span data-stu-id="dedff-159">tooconfigure an alias, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="dedff-160">nom DNS de la passerelle d’application Hello doit être utilisé toocreate un enregistrement CNAME, le nom DNS de points hello deux web applications toothis.</span><span class="sxs-lookup"><span data-stu-id="dedff-160">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="dedff-161">les utilisation de Hello d’enregistrements d’un n’est pas recommandée étant donné que l’adresse IP virtuelle hello peut changer lors du redémarrage de la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="dedff-161">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


```azurecli-interactive
az network public-ip show --name "pip" --resource-group "AdatumAppGatewayRG"
```

```
{
  "dnsSettings": {
    "domainNameLabel": null,
    "fqdn": "8c786058-96d4-4f3e-bb41-660860ceae4c.cloudapp.net",
    "reverseFqdn": null
  },
  "etag": "W/\"3b0ac031-01f0-4860-b572-e3c25e0c57ad\"",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/publicIPAddresses/pip2",
  "idleTimeoutInMinutes": 4,
  "ipAddress": "40.121.167.250",
  "ipConfiguration": {
    "etag": null,
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/applicationGateways/AdatumAppGateway2/frontendIPConfigurations/appGatewayFrontendIP",
    "name": null,
    "privateIpAddress": null,
    "privateIpAllocationMethod": null,
    "provisioningState": null,
    "publicIpAddress": null,
    "resourceGroup": "AdatumAppGatewayRG",
    "subnet": null
  },
  "location": "eastus",
  "name": "pip2",
  "provisioningState": "Succeeded",
  "publicIpAddressVersion": "IPv4",
  "publicIpAllocationMethod": "Dynamic",
  "resourceGroup": "AdatumAppGatewayRG",
  "resourceGuid": "3c30d310-c543-4e9d-9c72-bbacd7fe9b05",
  "tags": {
    "cli[2] owner[administrator]": ""
  },
  "type": "Microsoft.Network/publicIPAddresses"
}
```

## <a name="delete-all-resources"></a><span data-ttu-id="dedff-162">Supprimer toutes les ressources</span><span class="sxs-lookup"><span data-stu-id="dedff-162">Delete all resources</span></span>

<span data-ttu-id="dedff-163">toodelete toutes les ressources créées dans cet article, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="dedff-163">toodelete all resources created in this article, complete hello following steps:</span></span>

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a><span data-ttu-id="dedff-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dedff-164">Next steps</span></span>

<span data-ttu-id="dedff-165">Découvrez comment des sondes toocreate d’état personnalisé en vous rendant sur [créer une sonde d’intégrité personnalisé](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="dedff-165">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="dedff-166">Découvrez comment tooconfigure déchargement SSL et le déchiffrement SSL coûteux take hello désactivé vos serveurs web en vous rendant sur [configurer le déchargement SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="dedff-166">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
