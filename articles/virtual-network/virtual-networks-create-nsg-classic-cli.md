---
title: "aaaHow toocreate groupes de sécurité réseau à l’aide du mode classique hello CLI d’Azure | Documents Microsoft"
description: "Découvrez comment toocreate et déployer des groupes de sécurité réseau en mode classique, à l’aide de hello CLI d’Azure"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 17d98950-5fbb-4653-bef6-d822ab37541e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: eb78861e10a0dd950bb2c3783ee957d1cce55016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-nsgs-classic-in-hello-azure-cli"></a>Comment (classiques), de groupes de sécurité réseau toocreate hello CLI d’Azure
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Cet article décrit le modèle de déploiement classique hello. Vous pouvez également [créer des groupes de sécurité réseau dans le modèle de déploiement du Gestionnaire de ressources hello](virtual-networks-create-nsg-arm-cli.md).

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

commandes de CLI d’Azure Hello exemple ci-dessous s’attendre à un environnement simple déjà créé en fonction de scénario hello ci-dessus. Si vous souhaitez que les commandes de hello toorun car elles sont affichées dans ce document, tout d’abord créer d’environnement de test hello [créer un réseau virtuel](virtual-networks-create-vnet-classic-cli.md).

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a>Comment toocreate hello le groupe de sécurité réseau pour le sous-réseau frontal de hello
toocreate nommé d’un groupe de sécurité réseau nommé **NSG-FrontEnd** selon le scénario hello ci-dessus, suivez les étapes hello ci-dessous.

1. Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.
2. Exécutez hello  **`azure config mode`**  mode commande tooswitch tooclassic, comme indiqué ci-dessous.
   
        azure config mode asm
   
    Sortie attendue :
   
        info:    New mode is asm
3. Exécutez hello  **`azure network nsg create`**  commande toocreate un groupe de sécurité réseau.
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    Sortie attendue :
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : NSG-FrontEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    Paramètres :
   
   * **-l (ou --location)**. Région Azure où hello nouveau groupe de sécurité réseau doit être créé. Pour notre scénario, *westus*.
   * **-n (ou --name)**. Nom de hello nouveau groupe de sécurité réseau. Pour notre scénario, *NSG-FrontEnd*.
4. Exécutez hello  **`azure network nsg rule create`**  commande toocreate une règle qui autorise l’accès tooport 3389 (RDP) à partir de hello Internet.
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    Sortie attendue :
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : rdp-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 3389
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    Paramètres :
   
   * **-a (ou --nsg-name)**. Nom du NSG hello dans le hello règle sera créée. Pour notre scénario, *NSG-FrontEnd*.
   * **-n (ou --name)**. Nom de la nouvelle règle de hello. Pour notre scénario, *rdp-rule*.
   * **-c (ou--action)**. Niveau d’accès pour la règle hello (Deny ou autoriser).
   * **-p (ou --protocol)**. Protocole (Tcp, Udp ou *) pour la règle de hello.
   * **-r (ou --type)**. Direction de la connexion (Inbound ou Outbound).
   * **-y (ou --priority)**. Priorité de la règle de hello.
   * **-f (ou --source-address-prefix)**. Préfixe de l’adresse source dans CIDR ou à l’aide de balises par défaut.
   * **-o (ou --source-port-range)**. Port source ou plage de ports.
   * **-e (ou --destination-address-prefix)**. Préfixe de l’adresse de destination dans CIDR ou à l’aide de balises par défaut.
   * **-u (ou --destination-port-range)**. Port de destination ou plage de ports.
5. Exécutez hello  **`azure network nsg rule create`**  commande toocreate une règle qui autorise l’accès tooport 80 (HTTP) à partir de hello Internet.
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    Sortie attendue :
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. Exécutez hello  **`azure network nsg subnet add`**  sous-réseau frontal de commande toolink hello NSG toohello.
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    Sortie attendue :
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a>Comment mettre fin sous-réseau à toocreate hello NSG pour hello précédent
toocreate nommé d’un groupe de sécurité réseau nommé *principal de groupe de sécurité réseau* selon le scénario hello ci-dessus, suivez les étapes hello ci-dessous.

1. Exécutez hello  **`azure network nsg create`**  commande toocreate un groupe de sécurité réseau.
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    Sortie attendue :
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : NSG-BackEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    Paramètres :
   
   * **-l (ou --location)**. Région Azure où hello nouveau groupe de sécurité réseau doit être créé. Pour notre scénario, *westus*.
   * **-n (ou --name)**. Nom de hello nouveau groupe de sécurité réseau. Pour notre scénario, *NSG-FrontEnd*.
2. Exécutez hello  **`azure network nsg rule create`**  commande toocreate une règle qui autorise l’accès tooport 1433 (SQL) à partir du sous-réseau frontal de hello.
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    Sortie attendue :
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : sql-rule
        data:    Source address prefix           : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 1433
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. Exécutez hello  **`azure network nsg rule create`**  commande toocreate une règle qui refuse l’accès toohello Internet.
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    Sortie attendue :
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : *
        data:    Source Port                     : *
        data:    Destination address prefix      : INTERNET
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Outbound
        data:    Action                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. Exécutez hello  **`azure network nsg subnet add`**  toolink hello NSG toohello nouveau sous-réseau de fin de commande.
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    Sortie attendue :
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-BackEndX"
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

