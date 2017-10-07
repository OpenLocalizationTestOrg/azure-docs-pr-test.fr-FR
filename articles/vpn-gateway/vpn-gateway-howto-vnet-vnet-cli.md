---
title: "Connecter le réseau virtuel tooanother réseau virtuel : CLI d’Azure | Documents Microsoft"
description: "Cet article vous guide dans l’interconnexion de réseaux virtuels avec Azure Resource Manager et Azure CLI."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 70113914bcae03c80f9ad133ff081d1cf37fc309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a>Configurer une connexion de passerelle VPN de réseau virtuel à réseau virtuel à l’aide d’Azure CLI

Cet article vous montre comment toocreate une connexion de passerelle VPN entre les réseaux virtuels. Hello réseaux virtuels peuvent être hello identiques ou différentes régions, et à partir de hello identiques ou différents abonnements. Lors de la connexion des réseaux virtuels à partir de différents abonnements, les abonnements hello n’est pas nécessaire de toobe associé hello même client Active Directory. 

étapes de Hello dans cet article appliquent le modèle de déploiement du Gestionnaire de ressources toohello et utilisent CLI d’Azure. Vous pouvez également créer cette configuration à l’aide d’un outil de déploiement différentes ou d’un modèle de déploiement en sélectionnant une option différente de hello suivant liste :

> [!div class="op_single_selector"]
> * [Portail Azure](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Interface de ligne de commande Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Portail Azure (classique)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Connexions entre différents modèles de déploiement - Portail Azure](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Connexions entre différents modèles de déploiement - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

Connexion d’un réseau virtuel de réseau virtuel tooanother (au réseau) est tooconnecting comme emplacement d’un site réseau virtuel tooan local. Les deux types de connectivité utilisent un tooprovide de passerelle VPN un tunnel sécurisé utilisant IPsec/IKE. Si vos réseaux virtuels sont Bonjour même région, vous souhaiterez peut-être tooconsider les connectant à l’aide de l’homologation de réseau virtuel. L’homologation de réseaux virtuels (ou VNet Peering) n’utilise pas de passerelle VPN. Pour plus d’informations, consultez l’article [Homologation de réseaux virtuels](../virtual-network/virtual-network-peering-overview.md).

Vous pouvez combiner une communication de réseau virtuel à réseau virtuel avec des configurations multisites. Cela vous permet d’établir des topologies de réseau qui combinent une connectivité intersite de connectivité de réseau virtuel entre, comme indiqué dans hello suivant schéma :

![À propos des connexions](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <a name="why"></a>Pourquoi connecter des réseaux virtuels ?

Vous souhaiterez peut-être les réseaux virtuels tooconnect pour hello suivant raisons :

* **Géo-redondance et présence géographique dans plusieurs régions**

  * Vous pouvez configurer la géo-réplication ou la synchronisation avec une connectivité sécurisée sans passer par les points de terminaison accessibles sur Internet.
  * Avec Traffic Manager et l’équilibreur de charge Azure, vous pouvez configurer une charge de travail hautement disponible avec la géo-redondance dans plusieurs régions Azure. Par exemple important, tooset des SQL Always On avec des groupes de disponibilité répartis dans plusieurs régions Azure.
* **Applications multiniveaux régionales avec une limite d’isolement ou administrative**

  * Dans hello même région, vous pouvez définir des applications à plusieurs niveaux avec plusieurs réseaux virtuels interconnectés tooisolation ou exigences administratives.

Pour plus d’informations sur les connexions de réseau virtuel à réseau virtuel, consultez hello [FAQ sur le réseau à](#faq) à fin hello de cet article.

### <a name="which-set-of-steps-should-i-use"></a>Quelle procédure dois-je utiliser ?

Cet article inclut deux ensembles d’étapes distincts. Un ensemble d’étapes pour [qui résident dans des réseaux virtuels hello même abonnement](#samesub)et l’autre pour [des réseaux virtuels qui résident dans différents abonnements](#difsub).

## <a name="samesub"></a>Se connecter à des réseaux virtuels qui se trouvent dans hello même abonnement

![Diagramme v2v](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a>Avant de commencer

Avant de commencer, installez hello dernière version des commandes CLI de hello (version 2.0 ou version ultérieure). Pour plus d’informations sur l’installation des commandes CLI de hello, consultez [installer Azure CLI 2.0](/cli/azure/install-azure-cli).

### <a name="Plan"></a>Panifier vos plages d’adresses IP

Bonjour comme suit, nous créer deux réseaux virtuels, ainsi que leurs sous-réseaux de passerelle respectives et les configurations. Nous puis créez une connexion VPN entre hello deux réseaux virtuels. Il s’agit des plages d’adresses IP important tooplan hello pour votre configuration réseau. N’oubliez pas que vous devez vous assurer qu’aucune plage de réseaux virtuels ou de réseaux locaux ne se chevauche. Dans ces exemples, nous n’incluons pas de serveur DNS. Si vous souhaitez une résolution de noms pour vos réseaux virtuels, consultez la page [Résolution de noms](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

Nous utilisons hello valeurs dans les exemples hello suivantes :

**Valeurs pour TestVNet1 :**

* Nom du réseau virtuel : TestVNet1
* Groupe de ressources : TestRG1
* Emplacement : Est des États-Unis
* TestVNet1 : 10.11.0.0/16 et 10.12.0.0/16
* FrontEnd : 10.11.0.0/24
* BackEnd : 10.12.0.0/24
* GatewaySubnet : 10.12.255.0/27
* GatewayName : VNet1GW
* Adresse IP publique : VNet1GWIP
* Type de VPN : RouteBased
* Connection(1to4) : VNet1toVNet4
* Connection(1to5) : VNet1toVNet5
* Type de connexion : VNet2VNet

**Valeurs pour TestVNet4 :**

* Nom du réseau virtuel : TestVNet4
* TestVNet2 : 10.41.0.0/16 et 10.42.0.0/16
* Serveur frontal : 10.41.0.0/24
* Serveur principal : 10.42.0.0/24
* Sous-réseau de passerelle : 10.42.255.0/27
* Groupe de ressources : TestRG4
* Emplacement : États-Unis de l’Ouest
* Nom de la passerelle : VNet4GW
* Adresse IP publique : VNet4GWIP
* Type de VPN : RouteBased
* Connexion : VNet4toVNet1
* Type de connexion : VNet2VNet


### <a name="Connect"></a>Étape 1 : connecter tooyour abonnement

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <a name="TestVNet1"></a>Étape 2 : créez et configurez TestVNet1

1. Créez un groupe de ressources.

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. Créer des sous-réseaux TestVNet1 et hello pour TestVNet1. L’exemple suivant permet de créer un réseau virtuel nommé TestVNet1 et un sous-réseau nommé FrontEnd.

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. Créer un espace d’adressage supplémentaire pour le sous-réseau du serveur principal hello. Notez que dans cette étape, nous spécifier à la fois l’espace d’adressage hello que nous avons créés précédemment et hello espace d’adressage supplémentaire que nous souhaitons tooadd. C’est parce que hello [mise à jour du réseau virtuel az réseau](https://docs.microsoft.com/cli/azure/network/vnet#update) commande remplace les paramètres précédents hello. Assurez-vous que toospecify tous les préfixes d’adresse hello lors de l’utilisation de cette commande.

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. Créer un sous-réseau de back-end hello.
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. Créer un sous-réseau de passerelle hello. Notez que le sous-réseau passerelle hello est nommé « GatewaySubnet ». Ce nom est obligatoire. Dans cet exemple, sous-réseau de passerelle hello utilise un /27. Bien qu’il soit possible de toocreate un sous-réseau de passerelle aussi petit que /29, nous vous recommandons de créer un sous-réseau plus grand qui inclut plusieurs adresses en sélectionnant au moins /28 ou /27. Cette opération permettra suffisamment adresses tooaccommodate possibles des configurations supplémentaires que vous pouvez Bonjour futures.

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. Demander une passerelle publique de toohello alloué toobe adresse IP que vous allez créer pour votre réseau virtuel. Notez que hello AllocationMethod est dynamique. Vous ne pouvez pas spécifier hello adresse IP que vous toouse. Il est alloué dynamiquement tooyour passerelle.

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. Créer la passerelle de réseau virtuel hello pour TestVNet1. Les configurations de réseau virtuel à réseau virtuel requièrent un VPN de type RouteBased. Si vous exécutez cette commande à l’aide de hello '--aucune - attente' paramètre, vous ne voyez pas vos commentaires ou la sortie. Hello '--aucune - attente' paramètre permet de hello passerelle toocreate en arrière-plan de hello. Cela ne signifie pas le terme de la passerelle VPN hello création immédiatement. Création d’une passerelle peut souvent prendre entre 45 minutes ou plus, selon la passerelle de hello référence (SKU) que vous utilisez.

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="TestVNet4"></a>Étape 3 : créez et configurez TestVNet4

1. Créez un groupe de ressources.

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. Créez TestVNet4.

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. Créez des sous-réseaux supplémentaires pour TestVNet4.

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. Créer un sous-réseau de passerelle hello.

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. Demandez une adresse IP publique.

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. Créer la passerelle de réseau virtuel TestVNet4 hello.

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="createconnect"></a>Étape 4 : créer des connexions de hello

Vous avez maintenant deux réseaux virtuels avec des passerelles VPN. étape suivante de Hello est toocreate connexions de la passerelle VPN entre les passerelles de réseau virtuel hello. Si vous avez utilisé les exemples hello ci-dessus, vos passerelles de réseau virtuel sont dans différents groupes de ressources. Lorsque les passerelles se trouvent dans différents groupes de ressources, vous devez tooidentify et ID de ressource hello pour chaque passerelle lors de la connexion. Si vos réseaux virtuels sont Bonjour même groupe de ressources, vous pouvez utiliser hello [deuxième ensemble d’instructions](#samerg) , car vous n’avez pas besoin d’ID de ressource toospecify hello.

### <a name="diffrg"></a>tooconnect réseaux virtuels qui résident dans différents groupes de ressources

1. Obtenir hello ID de ressource de VNet1GW à partir de la sortie de hello Hello de commande suivante :

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  Dans la sortie de hello, recherchez hello » id : « ligne. les valeurs Hello entre guillemets de hello sont connexion de hello toocreate nécessaires dans la section suivante de hello. Copiez ces valeurs tooa éditeur de texte tel que le bloc-notes, afin que vous pouvez facilement collez-les lors de la création de votre connexion.

  Exemple de sortie :

  ```
  "activeActive": false, 
  "bgpSettings": { 
    "asn": 65515, 
    "bgpPeeringAddress": "10.12.255.30", 
    "peerWeight": 0 
   }, 
  "enableBgp": false, 
  "etag": "W/\"ecb42bc5-c176-44e1-802f-b0ce2962ac04\"", 
  "gatewayDefaultSite": null, 
  "gatewayType": "Vpn", 
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW", 
  "ipConfigurations":
  ```

  Copiez les valeurs hello après **« id » :** entre guillemets de hello.

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. Obtenir hello ID de ressource de VNet4GW et copie hello valeurs tooa éditeur de texte.

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. Créer hello TestVNet1 tooTestVNet4 connexion. Dans cette étape, vous créez des connexions de hello à partir de TestVNet1 tooTestVNet4. Il existe une clé partagée est référencée dans les exemples hello. Vous pouvez utiliser vos propres valeurs pour la clé partagée de hello. Hello important est que clé partagée hello doit correspondre pour les deux connexions. Création d’une connexion prend quelques instants toocomplete.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. Créer hello TestVNet4 tooTestVNet1 connexion. Cette étape est similaire toohello une version ultérieure, mais vous créez hello connexion à partir de TestVNet4 tooTestVNet1. Vérifiez que hello partagé clés correspondent. Il prend quelques minutes de connexion de hello tooestablish.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. Vérifiez vos connexions. Consultez [Vérifier votre connexion](#verify).

### <a name="samerg"></a>tooconnect réseaux virtuels qui résident dans hello même groupe de ressources

1. Créer hello TestVNet1 tooTestVNet4 connexion. Dans cette étape, vous créez des connexions de hello à partir de TestVNet1 tooTestVNet4. Groupes de ressources hello avis sont hello même dans les exemples hello. Vous voyez une clé partagée référencée dans les exemples hello. Vous pouvez utiliser vos propres valeurs pour la clé partagée de hello, toutefois, la clé partagée de hello doit correspondre pour les deux connexions. Création d’une connexion prend quelques instants toocomplete.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. Créer hello TestVNet4 tooTestVNet1 connexion. Cette étape est similaire toohello une version ultérieure, mais vous créez hello connexion à partir de TestVNet4 tooTestVNet1. Vérifiez que hello partagé clés correspondent. Il prend quelques minutes de connexion de hello tooestablish.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. Vérifiez vos connexions. Consultez [Vérifier votre connexion](#verify).

## <a name="difsub"></a>Connecter des réseaux virtuels situés dans différents abonnements

![Diagramme v2v](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

Dans ce scénario, nous connectons TestVNet1 et TestVNet5. Hello réseaux virtuels se trouvent à différents abonnements. les abonnements Hello n’est pas nécessaire de toobe associé hello même client Active Directory. étapes Hello pour cette configuration ajoutent une connexion au réseau supplémentaire dans l’ordre tooconnect TestVNet1 tooTestVNet5.

### <a name="TestVNet1diff"></a>Étape 5 : créez et configurez TestVNet1

Ces instructions continuent à partir des étapes hello Bonjour sections précédentes. Vous devez effectuer [étape 1](#Connect) et [étape 2](#TestVNet1) toocreate hello passerelle VPN pour TestVNet1 et configurer TestVNet1. Pour cette configuration, vous n’êtes pas requis toocreate TestVNet4 à partir de la section précédente de hello, bien que si vous créez il, il ne sera pas en conflit avec ces étapes. Une fois les étapes 1 et 2 effectuées, passez à l’étape 6 (ci-dessous).

### <a name="verifyranges"></a>Étape 6 : vérifier les plages d’adresses IP hello

Lorsque vous créez des connexions supplémentaires, il est important tooverify que l’espace d’adressage IP hello de réseau virtuel hello ne se chevauche pas avec les autres plages VNet ou de plages de passerelle de réseau local. Dans cet exercice, vous pouvez utiliser hello valeurs pour hello TestVNet5 suivantes :

**Valeurs pour TestVNet5 :**

* Nom du réseau virtuel : TestVNet5
* Groupe de ressources : TestRG5
* Emplacement : Japon de l’Est
* TestVNet5 : 10.51.0.0/16 et 10.52.0.0/16
* Serveur frontal : 10.51.0.0/24
* Serveur principal : 10.52.0.0/24
* Sous-réseau de passerelle : 10.52.255.0.0/27
* Nom de la passerelle : VNet5GW
* Adresse IP publique : VNet5GWIP
* Type de VPN : RouteBased
* Connexion : VNet5toVNet1
* Type de connexion : VNet2VNet

### <a name="TestVNet5"></a>Étape 7 : créez et configurez TestVNet5

Cette étape doit être effectuée dans le contexte de hello du nouvel abonnement hello, abonnement 5. Cette partie ne peut être effectuée par administrateur hello dans une autre organisation qui possède l’abonnement de hello. tooswitch entre l’utilisation d’abonnements ' liste des comptes az--tous les ' toolist hello compte tooyour disponible d’abonnements, puis utilisez ' az compte ensemble--abonnement <subscriptionID>' abonnement de toohello tooswitch que vous souhaitez toouse.

1. Assurez-vous que vous êtes connectée tooSubscription 5, puis que vous créez un groupe de ressources.

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. Créez TestVNet5.

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. Ajoutez des sous-réseaux.

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. Ajouter un sous-réseau de passerelle hello.

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. Demandez une adresse IP publique

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. Créer une passerelle de TestVNet5 hello

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="connections5"></a>Étape 8 - créer des connexions de hello

Fractionnées cette étape dans deux sessions CLI marqué comme **[1 abonnement]**, et **[abonnement 5]** , car les passerelles hello sont dans des abonnements différents hello. tooswitch entre l’utilisation d’abonnements ' liste des comptes az--tous les ' toolist hello compte tooyour disponible d’abonnements, puis utilisez ' az compte ensemble--abonnement <subscriptionID>' abonnement de toohello tooswitch que vous souhaitez toouse.

1. **[Abonnement 1]**  Se connecter et se connecter tooSubscription 1. Nom de hello tooget et l’ID de hello passerelle à partir de la sortie de hello de commandes suivante d’exécution hello :

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  Copier le résultat de hello pour « id : ». Envoi hello ID et nom de hello de hello réseau virtuel (VNet1GW) toohello administrateur de la passerelle de 5 d’abonnement par courrier électronique ou une autre méthode.

  Exemple de sortie :

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. **[Abonnement 5]**  Se connecter et se connecter tooSubscription 5. Nom de hello tooget et l’ID de hello passerelle à partir de la sortie de hello de commandes suivante d’exécution hello :

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  Copier le résultat de hello pour « id : ». Envoi hello ID et nom de hello de hello réseau virtuel (VNet5GW) toohello administrateur de la passerelle de 1 de l’abonnement par courrier électronique ou une autre méthode.

3. **[Abonnement 1]**  Dans cette étape, vous créez des connexion de hello à partir de TestVNet1 tooTestVNet5. Vous pouvez utiliser vos propres valeurs pour la clé partagée de hello, toutefois, la clé partagée de hello doit correspondre pour les deux connexions. Création d’une connexion peut prendre quelques instants toocomplete. Assurez-vous que vous vous connectez tooSubscription 1.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. **[Abonnement 5]**  Cette étape est similaire toohello une version ultérieure, mais vous créez hello connexion à partir de TestVNet5 tooTestVNet1. Assurez-vous que hello partagé clés correspondent et que vous vous connectez tooSubscription 5.

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <a name="verify"></a>Vérifiez les connexions hello
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <a name="faq"></a>Forum Aux Questions sur l’interconnexion de réseaux virtuels
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Étapes suivantes

* Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels. Pour plus d’informations, consultez hello [documentation de Machines virtuelles](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Pour plus d’informations sur BGP, consultez hello [vue d’ensemble du protocole BGP](vpn-gateway-bgp-overview.md) et [comment tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
