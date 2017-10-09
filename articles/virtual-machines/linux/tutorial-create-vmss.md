---
title: aaaCreate un machines virtuelles identiques pour Linux dans Azure | Documents Microsoft
description: "Créez et déployez une application hautement disponible sur des machines virtuelles Linux à l’aide d’un groupe de machines virtuelles identiques"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.openlocfilehash: 00dd81043f9be46ef2dc6dfe97eefdb20944ee13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a>Créer un groupe de machines virtuelles identiques et déployer une application hautement disponible sur Linux
Un ensemble d’échelle de machine virtuelle vous permet de toodeploy et gérer un ensemble de machines virtuelles identiques et la mise à l’échelle automatique. Vous pouvez mettre à l’échelle nombre hello d’ordinateurs virtuels dans un ensemble d’échelle hello manuellement ou définir tooautoscale règles en fonction de l’utilisation du processeur, la demande de mémoire ou le trafic réseau. Ce didacticiel explique comment déployer un groupe de machines virtuelles identiques dans Azure. Vous allez apprendre à effectuer les actions suivantes :

> [!div class="checklist"]
> * Utiliser le nuage-init toocreate un tooscale d’application
> * Créer un groupe de machines virtuelles identiques
> * Augmentez ou diminuez le nombre de hello d’instances dans un ensemble d’échelle
> * Afficher les informations de connexion pour les instances de groupe identique
> * Utiliser des disques de données dans un groupe identique


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="scale-set-overview"></a>Vue d’ensemble des groupes identiques
Un ensemble d’échelle de machine virtuelle vous permet de toodeploy et gérer un ensemble de machines virtuelles identiques et la mise à l’échelle automatique. Échelle définit utilisez hello mêmes composants que vous avez appris dans le cadre du didacticiel précédent hello trop[créer des ordinateurs virtuels à haute disponibilités](tutorial-availability-sets.md). Les machines virtuelles d’un groupe identique sont créées dans un groupe de disponibilité et réparties entre les domaines d’erreur logique et de mise à jour.

Les machines virtuelles sont créées en fonction des besoins dans un groupe identique. Vous définissez toocontrol de règles de mise à l’échelle quand et comment les machines virtuelles sont ajoutés ou supprimés à partir d’un ensemble d’échelle hello. Ces règles peuvent se déclencher en fonction de mesures telles que la charge du processeur, l’utilisation de la mémoire ou le trafic réseau.

Échelle définit la prise en charge des too1, 000 des machines virtuelles lorsque vous utilisez une image de plateforme Azure. Pour les charges de production, vous souhaiterez peut-être trop[créer une image de machine virtuelle personnalisée](tutorial-custom-images.md). Vous pouvez créer des machines virtuelles de too100 dans une échelle définie lors de l’utilisation d’une image personnalisée.


## <a name="create-an-app-tooscale"></a>Créer une application tooscale
À des fins de production, vous souhaiterez peut-être trop[créer une image de machine virtuelle personnalisée](tutorial-custom-images.md) qui inclut votre application installée et configurée. Pour ce didacticiel, permet de personnaliser les hello que machines virtuelles sur le premier démarrage tooquickly voir une échelle définie dans l’action.

Dans un didacticiel précédent, vous avez appris [comment toocustomize une machine virtuelle de Linux au premier démarrage](tutorial-automate-vm-deployment.md) avec init-cloud. Vous pouvez utiliser hello même tooinstall fichier de configuration cloud-init NGINX et exécuter une application Node.js de « Hello World » simple. 

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


## <a name="create-a-scale-set"></a>Créer un groupe identique
Pour pouvoir créer un groupe identique, vous devez créer un groupe de ressources avec la commande [az group create](/cli/azure/group#create). Hello exemple suivant crée un groupe de ressources nommé *myResourceGroupScaleSet* Bonjour *eastus* emplacement :

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

Créez à présent un groupe de machines virtuelles identiques avec [az vmss create](/cli/azure/vmss#create). Hello exemple suivant crée une échelle définie nommée *myScaleSet*, utilise Bonjour cloud-init fichier toocustomize Bonjour VM et génère des clés SSH s’ils n’existent pas :

```azurecli-interactive 
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image UbuntuLTS \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

Il prend quelques minutes toocreate et que vous configurez toutes les ressources de jeu de mise à l’échelle hello et machines virtuelles. Il existe des tâches en arrière-plan qui continuer toorun après que hello CLI d’Azure vous renvoie toohello invite. Il peut être une ou deux minutes avant que vous pouvez accéder à application hello.


## <a name="allow-web-traffic"></a>Autoriser le trafic web
Un équilibreur de charge a été créé automatiquement dans le cadre de l’ensemble d’échelle de machine virtuelle hello. équilibrage de charge Hello répartit le trafic sur un ensemble de VM défini à l’aide de règles d’équilibrage de charge. Plus d’informations sur les concepts d’équilibrage de charge et de configuration dans le didacticiel suivant de hello, [comment tooload équilibrer les machines virtuelles dans Azure](tutorial-load-balancer.md).

tooallow trafic tooreach hello web app, créez une règle avec [créer de règle d’équilibrage de charge réseau az](/cli/azure/network/lb/rule#create). Hello exemple suivant crée une règle nommée *myLoadBalancerRuleWeb*:

```azurecli-interactive 
az network lb rule create \
  --resource-group myResourceGroupScaleSet \
  --name myLoadBalancerRuleWeb \
  --lb-name myScaleSetLB \
  --backend-pool-name myScaleSetLBBEPool \
  --backend-port 80 \
  --frontend-ip-name loadBalancerFrontEnd \
  --frontend-port 80 \
  --protocol tcp
```

## <a name="test-your-app"></a>Test de l'application
toosee votre application Node.js sur le web de hello, obtenir hello adresse IP publique de votre équilibreur de charge avec [az réseau public-ip afficher](/cli/azure/network/public-ip#show). exemple Hello obtient adresse IP hello *myScaleSetLBPublicIP* créé comme faisant partie d’un ensemble d’échelle hello :

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

Entrez l’adresse IP publique de hello dans le navigateur web de tooa. application Hello s’affiche, y compris le nom d’hôte hello Hello VM que hello la charge du trafic d’équilibrage distribué à :

![Exécution de l’application Node.js](./media/tutorial-create-vmss/running-nodejs-app.png)

toosee hello en puissance en action, vous pouvez forcer l’actualisation de le de votre charge web browser toosee hello équilibrage répartir le trafic entre tous les ordinateurs virtuels de hello votre application en cours d’exécution.


## <a name="management-tasks"></a>Tâches de gestion
Tout au long du cycle de vie hello de hello ensemble d’échelle, vous devrez peut-être toorun une ou plusieurs tâches de gestion. En outre, vous souhaiterez toocreate les scripts qui automatisent différentes pour les tâches de cycle de vie. Bonjour Azure CLI 2.0 fournit un moyen rapide de toodo ces tâches. Voici quelques tâches courantes.

### <a name="view-vms-in-a-scale-set"></a>Afficher les machines virtuelles d’un groupe identique
une liste d’ordinateurs virtuels en cours d’exécution dans l’échelle de votre jeu de tooview, utilisez [az mise-instances de listes](/cli/azure/vmss#list-instances) comme suit :

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

Hello la sortie est similaire toohello l’exemple suivant :

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a>Augmenter ou diminuer les instances de machines virtuelles
nombre de hello toosee d’instances actuellement dans une échelle paramétrées, utilisez [afficher mise de az](/cli/azure/vmss#show) et des requêtes sur *sku.capacity*:

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

Vous pouvez puis manuellement augmenter ou réduire le nombre hello d’ordinateurs virtuels dans l’échelle de hello avec [mise à l’échelle de az mise](/cli/azure/vmss#scale). Hello exemple suivant définit hello nombre de machines virtuelles dans votre échelle définie trop*5*:

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

Les règles de mise à l’échelle vous permettent de définir comment tooscale monter ou descendre le nombre de hello d’ordinateurs virtuels dans votre échelle définies dans toodemand réponse telles que le trafic réseau ou de l’utilisation du processeur. Actuellement, ces règles ne peuvent pas être définies dans Azure CLI 2.0. Hello d’utilisation [portail Azure](https://portal.azure.com) tooconfigure mise à l’échelle.

### <a name="get-connection-info"></a>Obtenir des informations de connexion
les informations de connexion tooobtain sur hello des machines virtuelles dans vos jeux de mise à l’échelle, utilisez [az mise liste-instance-connexion-info](/cli/azure/vmss#list-instance-connection-info). Cette commande génère une adresse IP publique de hello et le port pour chaque machine virtuelle qui vous permet de tooconnect avec SSH :

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a>Utiliser des disques de données avec des groupes identiques
Vous pouvez créer et utiliser des disques de données avec des groupes identiques. Dans un didacticiel précédent, vous avez appris comment trop[disques Azure de gérer](tutorial-manage-disks.md) que contours hello meilleures pratiques et les améliorations des performances pour la création d’applications sur des disques de données plutôt que sur le disque de hello du système d’exploitation.

### <a name="create-scale-set-with-data-disks"></a>Créer un groupe identique avec des disques de données
toocreate une échelle définie et attacher des disques de données, ajouter hello `--data-disk-sizes-gb` paramètre toohello [az mise créer](/cli/azure/vmss#create) commande. Hello exemple suivant crée une échelle avec *50*Go des disques de données attaché tooeach instance :

```azurecli-interactive 
az vmss create \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetDisks \
    --image UbuntuLTS \
    --upgrade-policy-mode automatic \
    --custom-data cloud-init.txt \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50
```

Lorsque les instances sont supprimées d’un groupe identique, les disques de données associés sont également supprimés.

### <a name="add-data-disks"></a>Ajouter des disques de données
définir de tooadd un tooinstances de disque de données dans votre échelle, utilisez [attacher de disque de mise az](/cli/azure/vmss/disk#attach). Hello exemple suivant ajoute un *50*instance de tooeach Go disque :

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a>Détacher des disques de données
définir de tooremove un tooinstances de disque de données dans votre échelle, utilisez [détachement du disque de mise az](/cli/azure/vmss/disk#detach). Hello exemple suivant supprime le disque de données hello au numéro d’unité logique *2* de chaque instance de :

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a>Étapes suivantes
Ce didacticiel vous a montré comment créer un groupe de machines virtuelles identiques. Vous avez appris à effectuer les actions suivantes :

> [!div class="checklist"]
> * Utiliser le nuage-init toocreate un tooscale d’application
> * Créer un groupe de machines virtuelles identiques
> * Augmentez ou diminuez le nombre de hello d’instances dans un ensemble d’échelle
> * Afficher les informations de connexion pour les instances de groupe identique
> * Utiliser des disques de données dans un groupe identique

Avance toolearn de didacticiel suivant toohello plus d’informations sur les concepts de machines virtuelles d’équilibrage de charge.

> [!div class="nextstepaction"]
> [Équilibrage de charge des machines virtuelles](tutorial-load-balancer.md)