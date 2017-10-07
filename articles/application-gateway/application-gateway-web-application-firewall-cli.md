---
title: "pare-feu d’applications web aaaConfigure - passerelle d’Application Azure | Documents Microsoft"
description: "Cet article fournit des conseils sur comment toostart à l’aide de web des pare-feu d’applications sur une passerelle d’application existant ou nouveau."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: gwallace
ms.openlocfilehash: d5354984760ceab12ed49efa9e18836e9f1d3c96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a>Configurer un pare-feu d’application web sur une passerelle Application Gateway nouvelle ou existante avec Azure CLI

> [!div class="op_single_selector"]
> * [Portail Azure](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Interface de ligne de commande Azure](application-gateway-web-application-firewall-cli.md)

Découvrez comment toocreate un pare-feu d’applications web activé la passerelle d’application ou ajouter web application pare-feu tooan existant passerelle d’application.

pare-feu d’applications Hello web (WAF) dans la passerelle d’Application Azure protège les applications web à partir des attaques courantes basée sur le web telles que l’injection SQL, les attaques de script entre sites et des détournements de session.

La passerelle Azure Application Gateway est un équilibreur de charge de couche 7. Il fournit un basculement, routage des performances des requêtes HTTP entre différents serveurs, qu’ils soient sur le cloud de hello ou localement. La passerelle d’application offre de nombreuses fonctionnalités du contrôleur de livraison d’applications (ADC) : équilibrage de charge HTTP, affinité de session basée sur les cookies, déchargement de protocole SSL, sondes d’intégrité personnalisées, prise en charge multisite, etc. toofind une liste complète des fonctionnalités prises en charge, visitez : [vue d’ensemble de la passerelle d’Application](application-gateway-introduction.md).

Hello ci-dessous montre comment trop[ajouter web application pare-feu tooan existant application passerelle](#add-web-application-firewall-to-an-existing-application-gateway) et [créer une passerelle d’application qui utilise le pare-feu d’applications web](#create-an-application-gateway-with-web-application-firewall).

![image du scénario][scenario]

## <a name="prerequisite-install-hello-azure-cli-20"></a>Condition préalable : Installez hello Azure CLI 2.0

les étapes tooperform hello dans cet article, vous devez trop[installer hello Interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="waf-configuration-differences"></a>Différences de configuration WAF

Si vous avez lu [créer une passerelle d’Application avec Azure CLI](application-gateway-create-gateway-cli.md), vous comprenez tooconfigure de paramètres de référence (SKU) hello lors de la création d’une passerelle d’application. WAF fournit des paramètres supplémentaires toodefine lors de la configuration de référence (SKU) de hello sur une passerelle d’application. Il n’y a aucune modification supplémentaire que vous apportez sur la passerelle d’application hello lui-même.

| **Paramètre** | **Détails**
|---|---|
|**Référence (SKU)** |Une passerelle d’application normale sans WAF prend en charge les tailles **Standard\_Small**, **Standard\_Medium** et **Standard\_Large**. Avec l’introduction de hello de WAF, il existe deux références supplémentaires, **WAF\_support** et **WAF\_grande**. WAF n’est pas pris en charge sur les petites passerelles d’application.|
|**Mode** | Ce paramètre est le mode de WAF hello. Les valeurs autorisées sont **Détection** et **Prévention**. Lorsque WAF est configuré en mode de détection, toutes les menaces sont stockées dans un fichier journal. En mode de prévention, les événements sont toujours enregistrés, mais les intrus hello reçoive une réponse non autorisé 403 passerelle d’application hello.|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a>Ajouter web application pare-feu tooan existant passerelle d’application

Hello suivre les modifications de commande une passerelle d’application activé de tooa WAF de passerelle standard d’application existant.

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

Cette commande met à jour la passerelle d’application hello avec pare-feu d’applications web. Visitez [Application Diagnostics de passerelle](application-gateway-diagnostics.md) toounderstand comment tooview se connecte pour la passerelle de votre application. En raison de la nature de sécurité toohello de WAF, journaux besoin toobe révisé régulièrement posture de sécurité hello toounderstand de vos applications web.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Créer une passerelle Application Gateway avec le pare-feu d’applications web

Hello commande suivante crée une passerelle d’Application avec le pare-feu d’applications web.

```azurecli-interactive
#!/bin/bash

az network application-gateway create \
  --name "AdatumAppGateway2" \
  --location "eastus" \
  --resource-group "AdatumAppGatewayRG" \
  --vnet-name "AdatumAppGatewayVNET2" \
  --vnet-address-prefix "10.0.0.0/16" \
  --subnet "Appgatewaysubnet2" \
  --subnet-address-prefix "10.0.0.0/28" \
 --servers "10.0.0.5 10.0.0.4" \
  --capacity 2 
  --sku "WAF_Medium" \
  --http-settings-cookie-based-affinity "Enabled" \
  --http-settings-protocol "Http" \
  --frontend-port "80" \
  --routing-rule-type "Basic" \
  --http-settings-port "80" \
  --public-ip-address "pip2" \
  --public-ip-address-allocation "dynamic" \
  --tags "cli[2] owner[administrator]"
```

> [!NOTE]
> Passerelles d’application créés avec la configuration du pare-feu application hello web de base sont configurés avec CRS 3.0 pour les protections.

## <a name="get-application-gateway-dns-name"></a>Obtenir le nom DNS d’une passerelle Application Gateway

Après la création de la passerelle de hello, hello prochaine étape consiste tooconfigure hello frontal pour la communication. Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial. les utilisateurs finaux de tooensure pouvez atteindre la passerelle d’application hello, un enregistrement CNAME peut être le point de terminaison utilisé toopoint toohello public de la passerelle d’application hello. [Configuration d’un nom de domaine personnalisé pour Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure un enregistrement CNAME, récupérer les détails de la passerelle d’application hello et son nom IP/DNS associé à l’aide de la passerelle d’application hello PublicIPAddress élément attaché toohello. nom DNS de la passerelle d’application Hello doit être utilisé toocreate un enregistrement CNAME, le nom DNS de points hello deux web applications toothis. les utilisation de Hello d’enregistrements d’un n’est pas recommandée étant donné que l’adresse IP virtuelle hello peut changer lors du redémarrage de la passerelle d’application.

```azurecli-interactive
#!/bin/bash

az network public-ip show \
  --name pip2 \
  --resource-group "AdatumAppGatewayRG"
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

Découvrez le fonctionnement des règles de toocustomize WAF en visitant : [personnaliser les règles de pare-feu d’applications web via hello Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
