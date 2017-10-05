---
title: "Configurer le déchargement SSL - Passerelle Azure Application Gateway - Azure CLI 2.0 | Microsoft Docs"
description: "Cette page fournit des instructions pour la création d’une passerelle d’application avec déchargement SSL à l’aide d’Azure CLI 2.0"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: e8c1ba09daef09ef5002e33345905772961c1d93
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-cli-20"></a><span data-ttu-id="4fc4e-103">Configurer une passerelle d’application pour le déchargement SSL en utilisant Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4fc4e-103">Configure an application gateway for SSL offload by using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4fc4e-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="4fc4e-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="4fc4e-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4fc4e-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="4fc4e-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="4fc4e-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="4fc4e-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4fc4e-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="4fc4e-108">Il est possible de configurer Azure Application Gateway de façon à mettre fin à la session SSL (Secure Sockets Layer) sur la passerelle pour éviter les tâches de déchiffrement SSL coûteuses au niveau de la batterie de serveurs web.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="4fc4e-109">Le déchargement SSL simplifie également la gestion des certificats sur le serveur frontal.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-109">SSL offload also simplifies certificate management at the front-end server.</span></span>

## <a name="prerequisite-install-the-azure-cli-20"></a><span data-ttu-id="4fc4e-110">Condition préalable : installer Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4fc4e-110">Prerequisite: Install the Azure CLI 2.0</span></span>

<span data-ttu-id="4fc4e-111">Pour exécuter la procédure indiquée dans cet article, vous devez [installer l’interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="4fc4e-111">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="required-components"></a><span data-ttu-id="4fc4e-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4fc4e-112">Required components</span></span>

* <span data-ttu-id="4fc4e-113">**Pool de serveurs principaux :** liste des adresses IP des serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-113">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="4fc4e-114">Les adresses IP répertoriées doivent appartenir au sous-réseau de réseau virtuel ou doivent correspondre à une adresse IP/VIP publique.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-114">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="4fc4e-115">**Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-115">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="4fc4e-116">Ces paramètres sont liés à un pool et sont appliqués à tous les serveurs du pool.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-116">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="4fc4e-117">**Port frontal :** il s’agit du port public ouvert sur la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-117">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="4fc4e-118">Le trafic atteint ce port, puis il est redirigé vers l’un des serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-118">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="4fc4e-119">**Écouteur :** l’écouteur a un port frontal, un protocole (Http ou Https, avec respect de la casse) et le nom du certificat SSL (en cas de configuration du déchargement SSL).</span><span class="sxs-lookup"><span data-stu-id="4fc4e-119">**Listener:** The listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="4fc4e-120">**Règle :** la règle lie l’écouteur et le pool de serveurs principaux et définit vers quel pool de serveurs principaux le trafic doit être dirigé quand il atteint un écouteur spécifique.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-120">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="4fc4e-121">Actuellement, seule la règle *de base* est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-121">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="4fc4e-122">La règle de *base* est la distribution de charge par tourniquet.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-122">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="4fc4e-123">**Notes de configuration supplémentaires :**</span><span class="sxs-lookup"><span data-stu-id="4fc4e-123">**Additional configuration notes**</span></span>

<span data-ttu-id="4fc4e-124">Pour configurer des certificats SSL, le protocole dans **HttpListener** doit passer à *Https* (sensible à la casse).</span><span class="sxs-lookup"><span data-stu-id="4fc4e-124">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="4fc4e-125">L’élément **SslCertificate** doit être ajouté à **HttpListener** avec la valeur de variable configurée pour le certificat SSL.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-125">The **SslCertificate** element is added to **HttpListener** with the variable value configured for the SSL certificate.</span></span> <span data-ttu-id="4fc4e-126">Le port du serveur frontal doit être mis à jour sur 443.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-126">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="4fc4e-127">**Pour activer l’affinité basée sur les cookies**: une passerelle Application Gateway peut être configurée pour garantir qu’une requête d’une session client est toujours dirigée vers la même machine virtuelle dans la batterie de serveurs web.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-127">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="4fc4e-128">Ce scénario est réalisé par l’injection d’un cookie de session, qui permet à la passerelle de diriger le trafic de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-128">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="4fc4e-129">Pour activer l’affinité basée sur les cookies, définissez **CookieBasedAffinity** sur *Activé* dans l’élément **BackendHttpSettings**.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-129">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

## <a name="configure-ssl-offload-on-an-existing-application-gateway"></a><span data-ttu-id="4fc4e-130">Configurer le déchargement SSL sur une passerelle d’application existante</span><span class="sxs-lookup"><span data-stu-id="4fc4e-130">Configure SSL offload on an existing application gateway</span></span>

```azurecli-interactive
#!/bin/bash

# Create a new front end port to be used for SSL
az network application-gateway frontend-port create \
  --name sslport \
  --port 443 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Upload the .pfx certificate for SSL offload
az network application-gateway ssl-cert create \
  --name "newcert" \
  --cert-file /home/azureuser/self-signed/AdatumAppGatewayCert.pfx \
  --cert-password P@ssw0rd \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new listener referencing the port and certificate created earlier
az network application-gateway http-listener create \
  --frontend-ip "appGatewayFrontendIP" \
  --frontend-port sslport  \
  --name sslListener \
  --ssl-cert newcert \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new back-end pool to be used
az network application-gateway address-pool create \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG" \
  --name "appGatewayBackendPool2" \
  --servers 10.0.0.7 10.0.0.8

# Create a new back-end HTTP settings using the new probe
az network application-gateway http-settings create \
  --name "settings2" \
  --port 80 \
  --cookie-based-affinity Enabled \
  --protocol "Http" \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new rule linking the listener to the back-end pool
az network application-gateway rule create \
  --name "rule2" \
  --rule-type Basic \
  --http-settings settings2 \
  --http-listener ssllistener \
  --address-pool temp1 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

```

## <a name="create-an-application-gateway-with-ssl-offload"></a><span data-ttu-id="4fc4e-131">Créer une passerelle d’application avec déchargement SSL</span><span class="sxs-lookup"><span data-stu-id="4fc4e-131">Create an application gateway with SSL Offload</span></span>

<span data-ttu-id="4fc4e-132">L’exemple suivant permet de créer une passerelle d’application avec déchargement SSL.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-132">The following sample creates an application gateway with SSL offload.</span></span>  <span data-ttu-id="4fc4e-133">Le certificat et le mot de passe de certificat doivent être mis à jour avec une clé privée valide.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-133">The certificate and certificate password must be updated to a valid private key.</span></span>

```azurecli-interactive
#!/bin/bash

# Creates an application gateway with SSL offload
az network application-gateway create \
  --name "AdatumAppGateway3" \
  --location "eastus" \
  --resource-group "AdatumAppGatewayRG2" \
  --vnet-name "AdatumAppGatewayVNET2" \
  --cert-file /home/azureuser/self-signed/AdatumAppGatewayCert.pfx \
  --cert-password P@ssw0rd \
  --vnet-address-prefix "10.0.0.0/16" \
  --subnet "Appgatewaysubnet" \
  --subnet-address-prefix "10.0.0.0/28" \
  --frontend-port 443 \
  --servers "10.0.0.5 10.0.0.4" \
  --capacity 2 \
  --sku "Standard_Small" \
  --http-settings-cookie-based-affinity "Enabled" \
  --http-settings-protocol "Http" \
  --frontend-port "80" \
  --routing-rule-type "Basic" \
  --http-settings-port "80" \
  --public-ip-address "pip" \
  --public-ip-address-allocation "dynamic"
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="4fc4e-134">Obtenir le nom DNS d’une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="4fc4e-134">Get application gateway DNS name</span></span>

<span data-ttu-id="4fc4e-135">Une fois la passerelle créée, l’étape suivante consiste à configurer le serveur frontal pour la communication.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-135">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="4fc4e-136">Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-136">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="4fc4e-137">Pour s’assurer que les utilisateurs finaux peuvent atteindre la passerelle d’application, un enregistrement CNAME peut être utilisé pour pointer vers le point de terminaison public de la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-137">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="4fc4e-138">[Configuration d’un nom de domaine personnalisé pour Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4fc4e-138">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="4fc4e-139">Pour configurer un alias, récupérez les détails de la passerelle d’application et de son nom IP/DNS associé à l’aide de l’élément PublicIPAddress attaché à la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-139">To configure an alias, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="4fc4e-140">Le nom DNS de la passerelle Application Gateway doit être utilisé pour créer un enregistrement CNAME qui pointe les deux applications web sur ce nom DNS.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-140">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="4fc4e-141">L’utilisation de A-records n’est pas recommandée étant donné que l’adresse IP virtuelle peut changer lors du redémarrage de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="4fc4e-141">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="4fc4e-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4fc4e-142">Next steps</span></span>

<span data-ttu-id="4fc4e-143">Si vous souhaitez configurer une passerelle Application Gateway à utiliser avec l’équilibreur de charge interne (ILB), consultez [Création d’une passerelle Application Gateway avec un équilibrage de charge interne (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="4fc4e-143">If you want to configure an application gateway to use with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="4fc4e-144">Si vous souhaitez plus d'informations sur les options d'équilibrage de charge en général, consultez :</span><span class="sxs-lookup"><span data-stu-id="4fc4e-144">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="4fc4e-145">Équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="4fc4e-145">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="4fc4e-146">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="4fc4e-146">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
