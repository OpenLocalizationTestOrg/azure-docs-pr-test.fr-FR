---
title: "aaaConfigure SSL décharger la passerelle d’Application Azure - - CLI Azure 2.0 | Documents Microsoft"
description: "Cette page fournit des instructions toocreate une passerelle d’application avec SSL décharger par Azure CLI 2.0"
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
ms.openlocfilehash: f8d50e0c6ffef17c807938d816410e6d85321c9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-cli-20"></a>Configurer une passerelle d’application pour le déchargement SSL en utilisant Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Portail Azure](application-gateway-ssl-portal.md)
> * [Commandes PowerShell pour Azure Resource Manager](application-gateway-ssl-arm.md)
> * [Azure Classic PowerShell](application-gateway-ssl.md)
> * [Azure CLI 2.0](application-gateway-ssl-cli.md)

Passerelle d’Application Azure peut être configuré tooterminate hello Secure Sockets Layer (SSL) session à hello passerelle tooavoid coûteux SSL déchiffrement tâches toohappen au niveau de la batterie de serveurs web hello. Déchargement SSL simplifie également la gestion des certificats sur le serveur frontal de hello.

## <a name="prerequisite-install-hello-azure-cli-20"></a>Condition préalable : Installez hello Azure CLI 2.0

les étapes tooperform hello dans cet article, vous devez trop[installer hello Interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="required-components"></a>Composants requis

* **Pool de serveur principal :** liste hello des adresses IP des serveurs principaux de hello. adresses IP de Hello répertoriés doivent appartenir soit de sous-réseau de réseau virtuel toohello ou doivent être une adresse IP/VIP publique.
* **Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies. Ces paramètres sont lié tooa pool et sont des serveurs tooall appliqué dans le pool de hello.
* **Port frontal :** ce port est le port public hello qui est ouvert sur la passerelle d’application hello. Le trafic atteint ce port et obtient redirigés tooone de hello sur les serveurs principaux.
* **Écouteur :** hello port d’écoute utilise un port frontal, un protocole (Http ou Https, ces paramètres respectent la casse) et le nom du certificat SSL hello (si le déchargement de la configuration de SSL).
* **La règle :** règle de hello lie le port d’écoute hello et pool de serveur principal hello et définit le trafic de hello de pool de serveur principal doit être dirigée toowhen il atteint un écouteur particulier. Actuellement, seuls hello *base* règle est pris en charge. Hello *base* règle est la distribution de la charge de tourniquet.

**Notes de configuration supplémentaires :**

Pour configurer des certificats SSL, hello protocole dans **HttpListener** doit également modifier*Https* (sensible à la casse). Hello **certificat SSL** l’élément est ajouté trop**HttpListener** avec la valeur de la variable hello configuré pour le certificat SSL de hello. le port frontal Hello doit être too443 mis à jour.

**affinité basé sur cookie de tooenable**: une passerelle d’application peut être configurée tooensure qu’une demande à partir d’une session cliente est toujours dirigée toohello même machine virtuelle dans la batterie de serveurs web hello. Ce scénario est effectué par injection d’un cookie de session qui autorise le trafic toodirect de passerelle de hello de manière appropriée. l’affinité basé sur cookie tooenable, définie **CookieBasedAffinity** trop*activé* Bonjour **paramètres** élément.

## <a name="configure-ssl-offload-on-an-existing-application-gateway"></a>Configurer le déchargement SSL sur une passerelle d’application existante

```azurecli-interactive
#!/bin/bash

# Create a new front end port toobe used for SSL
az network application-gateway frontend-port create \
  --name sslport \
  --port 443 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Upload hello .pfx certificate for SSL offload
az network application-gateway ssl-cert create \
  --name "newcert" \
  --cert-file /home/azureuser/self-signed/AdatumAppGatewayCert.pfx \
  --cert-password P@ssw0rd \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new listener referencing hello port and certificate created earlier
az network application-gateway http-listener create \
  --frontend-ip "appGatewayFrontendIP" \
  --frontend-port sslport  \
  --name sslListener \
  --ssl-cert newcert \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new back-end pool toobe used
az network application-gateway address-pool create \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG" \
  --name "appGatewayBackendPool2" \
  --servers 10.0.0.7 10.0.0.8

# Create a new back-end HTTP settings using hello new probe
az network application-gateway http-settings create \
  --name "settings2" \
  --port 80 \
  --cookie-based-affinity Enabled \
  --protocol "Http" \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new rule linking hello listener toohello back-end pool
az network application-gateway rule create \
  --name "rule2" \
  --rule-type Basic \
  --http-settings settings2 \
  --http-listener ssllistener \
  --address-pool temp1 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

```

## <a name="create-an-application-gateway-with-ssl-offload"></a>Créer une passerelle d’application avec déchargement SSL

Hello suivant l’exemple crée une passerelle d’application avec déchargement SSL.  certificat de Hello et mot de passe de certificat doivent être mis à jour tooa clé privée valide.

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

## <a name="get-application-gateway-dns-name"></a>Obtenir le nom DNS d’une passerelle Application Gateway

Après la création de la passerelle de hello, hello prochaine étape consiste tooconfigure hello frontal pour la communication. Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial. les utilisateurs finaux de tooensure pouvez atteindre la passerelle d’application hello, un enregistrement CNAME peut être le point de terminaison utilisé toopoint toohello public de la passerelle d’application hello. [Configuration d’un nom de domaine personnalisé pour Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure un alias, de récupérer les détails de la passerelle d’application hello et son nom IP/DNS associé à l’aide de la passerelle d’application hello PublicIPAddress élément attaché toohello. nom DNS de la passerelle d’application Hello doit être utilisé toocreate un enregistrement CNAME, le nom DNS de points hello deux web applications toothis. les utilisation de Hello d’enregistrements d’un n’est pas recommandée étant donné que l’adresse IP virtuelle hello peut changer lors du redémarrage de la passerelle d’application.


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

## <a name="next-steps"></a>Étapes suivantes

Si vous souhaitez tooconfigure un toouse de passerelle d’application avec un équilibreur de charge interne (ILB), consultez [créer une passerelle d’application avec un équilibreur de charge interne (ILB)](application-gateway-ilb.md).

Si vous souhaitez plus d'informations sur les options d'équilibrage de charge en général, consultez :

* [Équilibrage de charge Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)
