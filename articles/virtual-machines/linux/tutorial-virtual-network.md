---
title: "aaaAzure réseaux virtuels et des ordinateurs virtuels Linux | Documents Microsoft"
description: "Didacticiel - gérer les réseaux virtuels Azure et les ordinateurs virtuels Linux par hello CLI d’Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 57e6bd4de16f0e31d53dc67bf50dc5730d43712b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-hello-azure-cli"></a>Gérer les réseaux virtuels Azure et les ordinateurs virtuels Linux par hello CLI d’Azure

Les machines virtuelles Azure utilisent la gestion réseau Azure pour la communication réseau interne et externe. Ce didacticiel vous guide dans le déploiement de deux machines virtuelles et la configuration de la gestion réseau Azure pour celles-ci. exemples de Hello dans ce didacticiel partent du principe que les machines virtuelles de hello sont héberge une application web avec une base de données principale, toutefois, une application n’est pas déployée dans le didacticiel de hello. Ce didacticiel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Déployer un réseau virtuel
> * Créer un sous-réseau dans un réseau virtuel
> * Joindre des ordinateurs virtuels tooa sous-réseau
> * Gérer les adresses IP publiques des machines virtuelles
> * Sécuriser le trafic internet entrant
> * Sécuriser le trafic tooVM de machine virtuelle


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="vm-networking-overview"></a>Vue d’ensemble de la mise en réseau de machines virtuelles

Réseaux virtuels Azure activer des connexions réseau sécurisées entre les machines virtuelles, hello internet et autres services Azure comme base de données SQL Azure. Les réseaux virtuels sont divisés en segments logiques, appelés sous-réseaux. Sous-réseaux sont utilisés les flux de réseau toocontrol et comme une limite de sécurité. Lorsque vous déployez une machine virtuelle, il inclut généralement une interface de réseau virtuel, ce qui est attaché tooa sous-réseau.

## <a name="deploy-virtual-network"></a>Déployer un réseau virtuel

Pour ce didacticiel, un seul réseau virtuel est créé avec deux sous-réseaux. Un sous-réseau frontal pour l’hébergement d’une application web et un sous-réseau principal pour l’hébergement d’un serveur de base de données.

Avant de pouvoir créer un réseau virtuel, créez un groupe de ressources avec [az group create](/cli/azure/group#create). Hello exemple suivant crée un groupe de ressources nommé *myRGNetwork* dans l’emplacement d’eastus hello.

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a>Création d’un réseau virtuel

Nous hello [créer un réseau virtuel du réseau az](/cli/azure/network/vnet#create) commande toocreate un réseau virtuel. Dans cet exemple, le réseau de hello est nommé *mvVnet* et dispose d’un préfixe d’adresse *10.0.0.0/16*. Un sous-réseau est également créé avec le nom *mySubnetFrontEnd* et le préfixe d’adresse *10.0.1.0/24*. Plus loin dans ce didacticiel, une machine virtuelle frontale est connecté toothis sous-réseau. 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a>Créer un sous-réseau

Un nouveau sous-réseau est ajouté toohello de réseau virtuel à l’aide de hello [créer de sous-réseau de réseau virtuel az réseau](/cli/azure/network/vnet/subnet#create) commande. Dans cet exemple, le sous-réseau de hello est nommé *mySubnetBackEnd* et dispose d’un préfixe d’adresse *10.0.2.0/24*. Ce sous-réseau est utilisé avec tous les services principaux.

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

À ce stade, un réseau a été créé et segmenté en deux sous-réseaux, un pour les services frontaux et un autre pour les services principaux. Dans la section suivante de hello, les ordinateurs virtuels sont créés et toothese sous-réseaux connectés.

## <a name="understand-public-ip-address"></a>Présentation des adresses IP publiques

Une adresse IP publique permet de ressources Azure toobe accessible sur internet de hello. Dans cette section du didacticiel de hello, une machine virtuelle est créée toodemonstrate comment les adresses toowork avec l’adresse IP publique.

### <a name="allocation-method"></a>Méthode d’allocation

Une adresse IP publique peut être allouée comme adresse dynamique ou statique. Par défaut, une adresse IP publique est allouée dynamiquement. Les adresses IP dynamiques sont libérées quand une machine virtuelle est désallouée. Ce comportement provoque hello IP adresse toochange pendant toute opération qui inclut une désallocation de machine virtuelle.

méthode d’allocation de Hello peut être définie toostatic, ce qui garantit que les adresses IP de hello restent affectés tooa machine virtuelle, même pendant un état libéré. Lorsque vous utilisez une adresse IP allouée de manière statique, hello adresse IP ne peut pas être spécifié. Au lieu de cela, elle est allouée à partir d’un pool d’adresses disponibles.

### <a name="dynamic-allocation"></a>Allocation dynamique

Lors de la création d’une machine virtuelle avec hello [az vm créer](/cli/azure/vm#create) hello par défaut public d’allocation méthode d’adresse IP est dynamique de la commande. Bonjour l’exemple suivant, un ordinateur virtuel est créé avec une adresse IP dynamique. 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myFrontEndVM \
  --vnet-name myVnet \
  --subnet mySubnetFrontEnd \
  --nsg myNSGFrontEnd \
  --public-ip-address myFrontEndIP \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="static-allocation"></a>Allocation statique

Lors de la création d’un ordinateur virtuel à l’aide de hello [az vm créer](/cli/azure/vm#create) command, inclure hello `--public-ip-address-allocation static` argument tooassign une adresse IP publique statique. Cette opération n’est pas illustrée dans ce didacticiel, toutefois dans la section suivante de hello une adresse IP allouée dynamiquement est modifié tooa alloué statiquement adresse. 

### <a name="change-allocation-method"></a>Changer la méthode d’allocation

la méthode de l’allocation d’adresses IP Hello peut être modifiée à l’aide de hello [mise à jour de az réseau public-ip](/cli/azure/network/public-ip#update) commande. Dans cet exemple, hello méthode d’allocation d’adresse IP de hello frontal machine virtuelle est déplacée toostatic.

Tout d’abord, désallouer hello machine virtuelle.

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

Hello d’utilisation [mise à jour de az réseau public-ip](/cli/azure/network/public-ip#update) commande tooupdate hello d’allocation (méthode). Dans ce cas, hello `--allocation-method` est défini trop*statique*.

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

Démarrez hello machine virtuelle.

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a>Pas d’adresse IP publique

Souvent, une machine virtuelle n’a pas besoin toobe accessible sur internet de hello. toocreate une machine virtuelle sans une adresse IP publique, utilisez hello `--public-ip-address ""` argument avec un ensemble vide de guillemets doubles. Cette configuration est montrée plus loin dans ce didacticiel.

## <a name="secure-network-traffic"></a>sécurisent le trafic réseau

Un groupe de sécurité réseau (NSG) contient une liste de règles de sécurité qui autorisent ou refusent tooresources de trafic réseau connecté tooAzure de réseaux virtuels (VNet). Groupes de sécurité réseau peuvent être toosubnets associée ou interfaces réseau individuelles. Lorsqu’un groupe de sécurité réseau est associé à une interface réseau, il s’applique uniquement hello associé la machine virtuelle. Lorsqu’un groupe de sécurité réseau est associé tooa sous-réseau, les règles de hello s’appliquent tooall ressources toohello connecté sous-réseau. 

### <a name="network-security-group-rules"></a>Règles de groupe de sécurité réseau

Les règles de groupe de sécurité réseau définissent les ports réseau sur lesquels le trafic est autorisé ou refusé. règles de Hello peuvent inclure des plages d’adresses IP source et de destination afin que le trafic est contrôlé entre systèmes spécifiques ou des sous-réseaux. Les règles de groupe de sécurité réseau ont également une priorité (entre 1 et 4 096). Les règles sont évaluées dans l’ordre de hello de priorité. Une règle avec une priorité de 100 est évaluée avant une règle avec une priorité de 200.

Tous les groupes de ressources réseau contiennent un ensemble de règles par défaut. les règles par défaut Hello ne peut pas être supprimés, mais comme ils sont affectés de priorité la plus faible de hello, elles peuvent être remplacées par les règles hello que vous créez.

- **Réseau virtuel** : le trafic en provenance et à destination d’un réseau virtuel est autorisé à la fois dans les directions entrante et sortante.
- **Internet** : le trafic sortant est autorisé, mais le trafic entrant est bloqué.
- **L’équilibrage de charge** -charge équilibrage tooprobe hello l’intégrité autoriser Azure de vos machines virtuelles et les instances de rôle. Si vous n’utilisez pas un groupe à charge équilibrée, vous pouvez remplacer cette règle.

### <a name="create-network-security-groups"></a>Créer des groupes de sécurité réseau

Un groupe de sécurité réseau permettre être créé à hello même temps comme un ordinateur virtuel à l’aide de hello [az vm créer](/cli/azure/vm#create) commande. Lorsque vous procédez ainsi, hello NSG associée à interface réseau de machines virtuelles hello et une règle de groupe de sécurité réseau est créé automatiquement le trafic de tooallow sur le port *22* à partir de n’importe quelle source. Plus haut dans ce didacticiel, hello NSG frontal a été créée automatiquement avec hello frontal machine virtuelle. Une règle de groupe de sécurité réseau a également été créée automatiquement pour le port 22. 

Dans certains cas, il peut être utile toopre-créer un groupe de sécurité réseau, tels que lorsque les règles SSH par défaut ne doivent pas être créées, ou lorsque hello NSG doit être attaché tooa sous-réseau. 

Hello d’utilisation [az réseau nsg créer](/cli/azure/network/nsg#create) commande toocreate un groupe de sécurité réseau.

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

Au lieu de l’association d’interface réseau de hello NSG tooa, il est associé à un sous-réseau. Dans cette configuration, toutes les machines virtuelles qui sont attaché toohello sous-réseau hérite des règles du groupe de sécurité réseau hello.

Mise à jour hello de sous-réseau existant nommé *mySubnetBackEnd* avec hello du groupe de sécurité réseau.

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

Maintenant créer un ordinateur virtuel, qui est attaché toohello *mySubnetBackEnd*. Notez que hello `--nsg` argument a une valeur de guillemets doubles vides. Un groupe de sécurité réseau n’a pas besoin toobe créé par hello machine virtuelle. Hello machine virtuelle est sous-réseau principal toohello attachée, ce qui est protégé par hello principal groupe de sécurité réseau créé au préalable. Ce groupe de sécurité réseau s’applique toohello machine virtuelle. En outre, Notez ici que hello `--public-ip-address` argument a une valeur de guillemets doubles vides. Cette configuration crée une machine virtuelle sans adresse IP publique. 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myBackEndVM \
  --vnet-name myVnet \
  --subnet mySubnetBackEnd \
  --public-ip-address "" \
  --nsg "" \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="secure-incoming-traffic"></a>Sécuriser le trafic entrant

Lorsque hello frontal machine virtuelle a été créée, une règle de groupe de sécurité réseau a été créée tooallow du trafic entrant sur le port 22. Cette règle permet de toohello des connexions SSH machine virtuelle. Pour cet exemple, le trafic doit également être autorisé sur le port *80*. Cette configuration autorise une toobe d’application web accédé sur hello machine virtuelle.

Hello d’utilisation [créer de règle de groupe de sécurité réseau du réseau az](/cli/azure/network/nsg/rule#create) commande toocreate une règle pour le port *80*.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGFrontEnd \
  --name http \
  --access allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range 80
```

Hello frontal machine virtuelle est désormais uniquement accessible sur le port *22* et le port *80*. Tout le trafic entrant est bloqué au niveau de groupe de sécurité réseau hello. Il peut être utile de toovisualize configurations de la règle NSG hello. Configuration de la règle NSG hello retour avec hello [liste de règles de réseau az](/cli/azure/network/nsg/rule#list) commande. 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

Output:

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-toovm-traffic"></a>Sécuriser le trafic tooVM de machine virtuelle

Les règles de groupe de sécurité réseau peuvent également s’appliquer entre les machines virtuelles. Pour cet exemple, hello VM frontal doit toocommunicate avec hello VM principal sur le port *22* et *3306*. Cette configuration permet des connexions SSH hello frontal machine virtuelle et également autoriser une application sur hello frontal toocommunicate de machine virtuelle avec une base de données MySQL back-end. Tout autre trafic doit être bloqué entre hello frontaux et principaux virtuels.

Hello d’utilisation [créer de règle de groupe de sécurité réseau du réseau az](/cli/azure/network/nsg/rule#create) commande toocreate une règle pour le port 22. Notez que hello `--source-address-prefix` argument spécifie une valeur de *10.0.1.0/24*. Cette configuration garantit que seul le trafic de sous-réseau frontal de hello est autorisé via hello NSG.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name SSH \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 100 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "22"
```

Ajoutez maintenant une règle pour le trafic MySQL sur le port 3306.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name MySQL \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "3306"
```

Enfin, étant donné que les groupes de sécurité réseau ont une règle par défaut lui accordant tout le trafic entre les ordinateurs virtuels dans hello même réseau virtuel, une règle peut être créée pour hello principaux groupes de sécurité réseau tooblock tout le trafic. Notez ici que hello `--priority` reçoit la valeur de *300*, qui est plus faible que les deux hello des règles de groupe de sécurité réseau et de MySQL. Cette configuration garantit que le trafic SSH et MySQL est toujours autorisé via hello groupe de sécurité réseau.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name denyAll \
  --access Deny \
  --protocol Tcp \
  --direction Inbound \
  --priority 300 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "*"
```

Hello principal machine virtuelle est désormais uniquement accessible sur le port *22* et le port *3306* à partir du sous-réseau frontal de hello. Tout le trafic entrant est bloqué au niveau de groupe de sécurité réseau hello. Il peut être utile de toovisualize configurations de la règle NSG hello. Configuration de la règle NSG hello retour avec hello [liste de règles de réseau az](/cli/azure/network/nsg/rule#list) commande. 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

Output:

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous créé et sécurisé de réseaux Azure en tant que machines de toovirtual connexes. Vous avez appris à effectuer les actions suivantes :

> [!div class="checklist"]
> * Déployer un réseau virtuel
> * Créer un sous-réseau dans un réseau virtuel
> * Joindre des ordinateurs virtuels tooa sous-réseau
> * Gérer les adresses IP publiques des machines virtuelles
> * Sécuriser le trafic internet entrant
> * Sécuriser le trafic tooVM de machine virtuelle

Avance toohello toolearn de didacticiel suivant sur la sécurisation des données sur des machines virtuelles à l’aide de la sauvegarde Azure. 

> [!div class="nextstepaction"]
> [Sauvegarder des machines virtuelles Linux dans Azure](./tutorial-backup-vms.md)
