---
title: "aaaHow tooload équilibrer les ordinateurs virtuels Linux dans Azure | Documents Microsoft"
description: "Découvrez comment toouse hello Azure charge équilibrage toocreate une application hautement disponible et sécurisée entre trois machines virtuelles de Linux"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: f01752c3caec3489ee13e63000775769f3236e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-linux-virtual-machines-in-azure-toocreate-a-highly-available-application"></a>Comment tooload équilibrer les ordinateurs virtuels Linux dans Azure toocreate une application hautement disponible
L’équilibrage de charge offre un niveau plus élevé de disponibilité en répartissant les demandes entrantes sur plusieurs machines virtuelles. Dans ce didacticiel, vous découvrez hello différents composants d’équilibrage de charge Azure hello de distribuer le trafic et fournissant une haute disponibilité. Vous allez apprendre à effectuer les actions suivantes :

> [!div class="checklist"]
> * Crée un équilibrage de charge Azure
> * Créer une sonde d’intégrité d’équilibreur de charge
> * Créer des règles de trafic pour l’équilibrage de charge
> * Utiliser le nuage-init toocreate une application Node.js de base
> * Créer des ordinateurs virtuels et d’attachement d’équilibrage de charge tooa
> * Afficher un équilibrage de charge en action
> * Ajouter et supprimer des machines virtuelles d’un équilibreur de charge


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="azure-load-balancer-overview"></a>Vue d’ensemble de l’équilibreur de charge Azure
Un équilibreur de charge Azure est un équilibreur de charge de type Couche 4 (TCP, UDP) qui offre une haute disponibilité en répartissant le trafic entrant entre les machines virtuelles saines. Une sonde d’intégrité d’équilibrage de charge surveille un port donné sur chaque machine virtuelle et ne distribue le trafic tooan machine virtuelle opérationnelle.

Vous définissez une configuration IP frontale qui contient une ou plusieurs adresses IP publiques. Cette configuration IP frontale permet à votre toobe d’applications et d’équilibrage de charge accessible sur Internet de hello. 

Machines virtuelles se connecter tooa équilibrage de charge à l’aide de leur carte réseau virtuelle (NIC). toohello du trafic toodistribute machines virtuelles, un pool d’adresses de serveur principal contient des adresses IP de hello d’équilibrage de charge hello virtuelle (NIC) connectées toohello.

flux de hello toocontrol du trafic, vous définissez des règles d’équilibrage de charge pour les ports et protocoles qui mappent des machines virtuelles de tooyour spécifiques.

Si vous avez suivi les didacticiel précédent hello trop[créer un ensemble d’échelle de machine virtuelle](tutorial-create-vmss.md), un équilibreur de charge a été créé pour vous. Tous ces composants ont été configurées dans le cadre de l’ensemble d’échelle hello.


## <a name="create-azure-load-balancer"></a>Créer un équilibreur de charge Azure
Cette section décrit en détail comment vous pouvez créer et configurer chaque composant d’équilibrage de charge hello. Pour pouvoir créer votre équilibreur de charge, vous devez créer un groupe de ressources avec la commande [az group create](/cli/azure/group#create). Hello exemple suivant crée un groupe de ressources nommé *myResourceGroupLoadBalancer* Bonjour *eastus* emplacement :

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a>Créer une adresse IP publique
tooaccess votre application sur hello Internet, vous avez besoin d’une adresse IP publique pour l’équilibrage de charge hello. Créez une adresse IP publique avec la commande [az network public-ip create](/cli/azure/network/public-ip#create). Hello exemple suivant crée une adresse IP publique nommée *myPublicIP* Bonjour *myResourceGroupLoadBalancer* groupe de ressources :

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a>Créer un équilibrage de charge
Créez un équilibrage de charge avec la commande [az network lb create](/cli/azure/network/lb#create). Hello exemple suivant crée un équilibreur de charge nommé *myLoadBalancer* et assigne hello *myPublicIP* configuration IP frontale de l’adresse toohello :

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a>Créer une sonde d’intégrité
tooallow hello équilibrage toomonitor hello l’état de charge de votre application, vous utilisez une sonde d’intégrité. Sonde d’intégrité Hello dynamiquement ajoute ou supprime des machines virtuelles à partir de la rotation d’équilibrage de charge hello en fonction de leurs contrôles toohealth de réponse. Par défaut, un ordinateur virtuel est supprimé de la distribution d’équilibrage de charge hello après deux défaillances consécutives à des intervalles de 15 secondes. Vous créez une sonde d’intégrité selon un protocole ou une page de vérification d’intégrité spécifique pour votre application. 

Bonjour à l’exemple suivant crée une sonde TCP. Vous pouvez également créer des sondes HTTP personnalisées pour des contrôles d’intégrité plus affinés. Lorsque vous utilisez une sonde HTTP personnalisée, vous devez créer page vérifier l’intégrité hello, tel que *healthcheck.js*. Sonde de Hello doit retourner un **HTTP 200 OK** réponse pour hello charge équilibrage tookeep hello hôte en rotation.

toocreate une sonde d’intégrité TCP, vous utilisez [sonde d’équilibrage de charge réseau az créer](/cli/azure/network/lb/probe#create). Hello exemple suivant crée une sonde d’intégrité nommée *myHealthProbe*:

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a>Créer une règle d’équilibreur de charge
Une règle d’équilibreur de charge est utilisé toodefine comment le trafic est distribué toohello machines virtuelles. Vous définissez la configuration IP frontale de hello pour le trafic entrant de hello et hello principal pool tooreceive hello du trafic IP, ainsi que les sources requis hello et port de destination. toomake que seuls les ordinateurs virtuels sains recevoir du trafic, vous définissez également toouse de sonde d’intégrité hello.

Utilisez [az network lb rule create](/cli/azure/network/lb/rule#create) pour créer une règle d’équilibrage de charge. Hello exemple suivant crée une règle nommée *myLoadBalancerRule*, utilise hello *myHealthProbe* sonde d’intégrité et équilibre le trafic sur le port *80*:

```azurecli-interactive 
az network lb rule create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myLoadBalancerRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe
```


## <a name="configure-virtual-network"></a>Configurer un réseau virtuel
Avant de déployer des machines virtuelles et tester votre programme d’équilibrage, créer hello prenant en charge des ressources du réseau virtuel. Pour plus d’informations sur les réseaux virtuels, consultez hello [gérer les réseaux virtuels Azure](tutorial-virtual-network.md) didacticiel.

### <a name="create-network-resources"></a>Créer des ressources réseau
Créez un réseau virtuel avec la commande [az network vnet create](/cli/azure/network/vnet#create). Hello exemple suivant crée un réseau virtuel nommé *myVnet* avec un sous-réseau nommé *mySubnet*:

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

tooadd un groupe de sécurité réseau, vous utilisez [az réseau nsg créer](/cli/azure/network/nsg#create). Hello exemple suivant crée un groupe de sécurité réseau nommé *myNetworkSecurityGroup*:

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

Créez une règle de groupe de sécurité réseau avec la commande [az network nsg rule create](/cli/azure/network/nsg/rule#create). Hello exemple suivant crée une règle de groupe de sécurité réseau nommée *myNetworkSecurityGroupRule*:

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

Les cartes d’interface réseau virtuelles sont créées avec la commande [az network nic create](/cli/azure/network/nic#create). Hello exemple suivant crée trois cartes réseau virtuelles. (Une carte réseau virtuelle pour chaque ordinateur virtuel que vous créez pour votre application Bonjour suivant les étapes). Vous pouvez créer des cartes réseau virtuelles supplémentaires et des machines virtuelles à tout moment et ajoutez-les à équilibrage de charge toohello :

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupLoadBalancer \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --network-security-group myNetworkSecurityGroup \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-virtual-machines"></a>Créer des machines virtuelles

### <a name="create-cloud-init-config"></a>Créer une configuration cloud-init
Dans un didacticiel précédent sur [comment toocustomize une machine virtuelle de Linux au premier démarrage](tutorial-automate-vm-deployment.md), vous avez appris comment personnalisation tooautomate avec init-cloud. Vous pouvez utiliser hello même tooinstall fichier de configuration cloud-init NGINX et exécuter une application Node.js de « Hello World » simple.

Dans votre environnement actuel, créez un fichier nommé *cloud-init.txt* et coller hello de configuration suivante. Par exemple, créer le fichier de hello Bonjour Cloud Shell pas sur votre ordinateur local. Entrez `sensible-editor cloud-init.txt` toocreate hello fichier et afficher la liste des éditeurs disponibles. Assurez-vous que ce fichier d’ensemble cloud-init hello est copié correctement, en particulier hello première ligne :

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-virtual-machines"></a>Créer des machines virtuelles
tooimprove hello haute disponibilité de votre application, placez vos machines virtuelles dans un ensemble de disponibilité. Pour plus d’informations sur les groupes à haute disponibilité, consultez hello précédente [comment les ordinateurs virtuels hautement disponibles toocreate](tutorial-availability-sets.md) didacticiel.

Créez un groupe à haute disponibilité avec la commande [az vm availability-set create](/cli/azure/vm/availability-set#create). Hello exemple suivant crée un groupe à haute disponibilité nommée *myAvailabilitySet*:

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

Vous pouvez désormais créer VMs hello avec [az vm créer](/cli/azure/vm#create). Hello exemple suivant crée trois machines virtuelles et génère des clés SSH s’ils n’existent pas déjà :

```bash
for i in `seq 1 3`; do
    az vm create \
        --resource-group myResourceGroupLoadBalancer \
        --name myVM$i \
        --availability-set myAvailabilitySet \
        --nics myNic$i \
        --image UbuntuLTS \
        --admin-username azureuser \
        --generate-ssh-keys \
        --custom-data cloud-init.txt \
        --no-wait
done
```

Il existe des tâches en arrière-plan qui continuer toorun après que hello CLI d’Azure vous renvoie toohello invite. Hello `--no-wait` paramètre n’attend pas pour tous les hello toocomplete de tâches. Il peut être une ou deux minutes avant que vous pouvez accéder à application hello. Hello sonde d’intégrité d’équilibrage de charge détecte automatiquement lors de l’application hello est en cours d’exécution sur chaque machine virtuelle. Une fois que l’application hello est en cours d’exécution, règle d’équilibrage de charge hello démarre le trafic de toodistribute.


## <a name="test-load-balancer"></a>Tester l’équilibreur de charge
Obtenir hello une adresse IP publique de votre équilibreur de charge avec [az réseau public-ip afficher](/cli/azure/network/public-ip#show). exemple Hello obtient adresse IP hello *myPublicIP* créé précédemment :

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

Vous pouvez entrer ensuite des adresse IP publique de hello dans tooa navigateur. N’oubliez pas, il prend quelques minutes hello hello machines virtuelles toobe prêt avant le démarrage d’équilibrage de charge hello toodistribute trafic toothem. application Hello est affichée, notamment le nom d’hôte hello Hello VM cet équilibrage de charge hello distributed tooas trafic Bonjour l’exemple suivant :

![Exécution de l’application Node.js](./media/tutorial-load-balancer/running-nodejs-app.png)

équilibrage de charge toosee hello répartir le trafic entre tous les trois machines virtuelles exécutant votre application, vous pouvez forcer l’actualisation votre navigateur web.


## <a name="add-and-remove-vms"></a>Ajouter et supprimer des machines virtuelles
Vous devrez peut-être maintenance tooperform sur hello machines virtuelles exécutant votre application, telles que l’installation des mises à jour du système d’exploitation. toodeal avec une augmentation du trafic tooyour application, vous devrez peut-être tooadd des machines virtuelles supplémentaires. Cette section vous montre comment tooremove ou ajouter une machine virtuelle à partir de l’équilibrage de charge hello.

### <a name="remove-a-vm-from-hello-load-balancer"></a>Supprimer une machine virtuelle à partir de l’équilibrage de charge hello
Vous pouvez supprimer une machine virtuelle à partir du pool d’adresses principales hello avec [az carte réseau ip-config-pool d’adresses réseau supprimer](/cli/azure/network/nic/ip-config/address-pool#remove). Hello suivant supprime de l’exemple hello carte réseau virtuelle pour **myVM2** de *myLoadBalancer*:

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

équilibrage de charge toosee hello répartir le trafic entre hello deux autres machines virtuelles exécutant votre application vous pouvez forcer l’actualisation votre navigateur web. Vous pouvez désormais effectuer la maintenance sur hello machine virtuelle, tels que l’installation des mises à jour du système d’exploitation ou d’effectuer un redémarrage de l’ordinateur virtuel.

### <a name="add-a-vm-toohello-load-balancer"></a>Ajouter un équilibrage de charge de toohello de machine virtuelle
Après avoir effectué la maintenance de la machine virtuelle, ou si vous devez tooexpand capacité, vous pouvez ajouter un pool d’adresses principales toohello machine virtuelle avec [az carte réseau ip-config-pool d’adresses réseau ajouter](/cli/azure/network/nic/ip-config/address-pool#add). exemple Hello ajoute hello carte réseau virtuelle pour **myVM2** trop*myLoadBalancer*:

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous créé un équilibreur de charge et attaché tooit de machines virtuelles. Vous avez appris à effectuer les actions suivantes :

> [!div class="checklist"]
> * Crée un équilibrage de charge Azure
> * Créer une sonde d’intégrité d’équilibreur de charge
> * Créer des règles de trafic pour l’équilibrage de charge
> * Utiliser le nuage-init toocreate une application Node.js de base
> * Créer des ordinateurs virtuels et d’attachement d’équilibrage de charge tooa
> * Afficher un équilibrage de charge en action
> * Ajouter et supprimer des machines virtuelles d’un équilibreur de charge

Avance toolearn de didacticiel suivant toohello plus d’informations sur les composants de réseau virtuel Azure.

> [!div class="nextstepaction"]
> [Gérer les machines virtuelles et les réseaux virtuels](tutorial-virtual-network.md)
