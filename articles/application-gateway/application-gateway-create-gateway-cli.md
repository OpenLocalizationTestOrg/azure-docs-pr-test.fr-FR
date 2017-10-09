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
# <a name="create-an-application-gateway-by-using-hello-azure-cli-20"></a>Créer une passerelle d’application à l’aide de hello Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Portail Azure](application-gateway-create-gateway-portal.md)
> * [Commandes PowerShell pour Azure Resource Manager](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Modèle Azure Resource Manager](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI 1.0](application-gateway-create-gateway-cli.md)
> * [Azure CLI 2.0](application-gateway-create-gateway-cli.md)

Application Gateway est une appliance virtuelle dédiée qui intègre Application Delivery Controller (ADC) en tant que service, offrant diverses fonctionnalités d’équilibrage de charge de couche 7 pour votre application.

## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete

Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

* [Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) -notre CLI pour les modèles de déploiement gestion classique et les ressources des hello.
* [Azure CLI 2.0](application-gateway-create-gateway-cli.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello

## <a name="prerequisite-install-hello-azure-cli-20"></a>Condition préalable : Installez hello Azure CLI 2.0

les étapes tooperform hello dans cet article, vous devez trop[installer hello Interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

> [!NOTE]
> Si vous n’avez pas de compte Azure, vous devez vous en procurer un. Inscrivez-vous à un [essai gratuit ici](../active-directory/sign-up-organization.md).

## <a name="scenario"></a>Scénario

Dans ce scénario, vous découvrez comment une passerelle d’application à l’aide de toocreate hello portail Azure.

Ce scénario va :

* créer une passerelle Application Gateway moyenne avec deux instances ;
* créer un réseau virtuel nommé AdatumAppGatewayVNET avec un bloc CIDR réservé de 10.0.0.0/16 ;
* créer un sous-réseau appelé Appgatewaysubnet qui utilise 10.0.0.0/28 comme bloc CIDR ;

> [!NOTE]
> Les tests de configuration supplémentaires de la passerelle d’application hello, y compris l’intégrité personnalisée, les adresses du pool principal et des règles supplémentaires sont configurés après la configuration de la passerelle d’application hello et non pendant le déploiement initial.

## <a name="before-you-begin"></a>Avant de commencer

La passerelle Application Gateway Azure requiert son propre sous-réseau. Lorsque vous créez un réseau virtuel, assurez-vous que vous laissez suffisamment toohave d’espace adresse plusieurs sous-réseaux. Une fois que vous déployez un tooa de sous-réseau de la passerelle d’application, passerelles d’application uniquement supplémentaires peuvent être ajoutées toohello sous-réseau.

## <a name="log-in-tooazure"></a>Connectez-vous à tooAzure

Ouvrez hello **invite de commandes Microsoft Azure**et les journaux. 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> Vous pouvez également utiliser `az login` sans commutateur hello pour la connexion de périphérique qui requiert la saisie d’un code à aka.ms/devicelogin.

Une fois que vous tapez hello précédent exemple, un code est fourni. Accédez toohttps://aka.ms/devicelogin dans un processus de connexion de navigateur toocontinue hello.

![Invite de commande affichant le code de l’appareil][1]

Dans le navigateur de hello, entrez le code hello que vous avez reçu. Vous êtes redirigé tooa-page de connexion.

![code de tooenter du navigateur][2]

Une fois que le code de hello a été entré. vous êtes connecté, fermer hello navigateur toocontinue avec le scénario hello.

![Connexion réussie][3]

## <a name="create-hello-resource-group"></a>Créer le groupe de ressources hello

Avant de créer la passerelle d’application hello, un groupe de ressources est créé de passerelle d’application toocontain hello. Hello Voici commande hello.

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-hello-application-gateway"></a>Créer une passerelle d’application hello

Hello IP adresses utilisées pour hello principal sont hello pour votre serveur principal. Ces valeurs peuvent être des deux adresses IP privées dans le réseau virtuel de hello, des adresses IP publiques ou des noms de domaine complet pour vos serveurs principaux. Hello exemple suivant crée une passerelle d’application avec les paramètres de configuration supplémentaires pour les paramètres http, les ports et les règles.

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

Hello exemple précédent montre plusieurs propriétés qui ne sont pas requises lors de la création de hello d’une passerelle d’application. Hello, exemple de code suivant crée une passerelle d’application avec les informations de hello requis.

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
> Pour obtenir la liste de paramètres qui peuvent être fournies au cours de hello création exécuter commande suivante : `az network application-gateway create --help`.

Cet exemple crée une passerelle d’application de base avec les paramètres par défaut pour l’écouteur de hello, pool principal, paramètres http du serveur principal et les règles. Vous pouvez modifier ces paramètres toosuit votre déploiement une fois l’approvisionnement de hello réussie.
Si vous avez déjà votre application web définie avec le pool principal d’hello Bonjour précédentes étapes, une fois créés, l’équilibrage de charge démarre.

## <a name="get-application-gateway-dns-name"></a>Obtenir le nom DNS d’une passerelle Application Gateway

Après la création de la passerelle de hello, hello prochaine étape consiste tooconfigure hello frontal pour la communication. Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial. les utilisateurs finaux de tooensure pouvez atteindre la passerelle d’application hello, un enregistrement CNAME peut être le point de terminaison utilisé toopoint toohello public de la passerelle d’application hello. [Configuration d’un nom de domaine personnalisé pour Azure](../dns/dns-custom-domain.md). tooconfigure un alias, de récupérer les détails de la passerelle d’application hello et son nom IP/DNS associé à l’aide de la passerelle d’application hello PublicIPAddress élément attaché toohello. nom DNS de la passerelle d’application Hello doit être utilisé toocreate un enregistrement CNAME, le nom DNS de points hello deux web applications toothis. les utilisation de Hello d’enregistrements d’un n’est pas recommandée étant donné que l’adresse IP virtuelle hello peut changer lors du redémarrage de la passerelle d’application.


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

## <a name="delete-all-resources"></a>Supprimer toutes les ressources

toodelete toutes les ressources créées dans cet article, hello complète comme suit :

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a>Étapes suivantes

Découvrez comment des sondes toocreate d’état personnalisé en vous rendant sur [créer une sonde d’intégrité personnalisé](application-gateway-create-probe-portal.md)

Découvrez comment tooconfigure déchargement SSL et le déchiffrement SSL coûteux take hello désactivé vos serveurs web en vous rendant sur [configurer le déchargement SSL](application-gateway-ssl-arm.md)

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
