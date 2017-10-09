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
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a><span data-ttu-id="dda12-103">Créer un groupe de machines virtuelles identiques et déployer une application hautement disponible sur Linux</span><span class="sxs-lookup"><span data-stu-id="dda12-103">Create a Virtual Machine Scale Set and deploy a highly available app on Linux</span></span>
<span data-ttu-id="dda12-104">Un ensemble d’échelle de machine virtuelle vous permet de toodeploy et gérer un ensemble de machines virtuelles identiques et la mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="dda12-104">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="dda12-105">Vous pouvez mettre à l’échelle nombre hello d’ordinateurs virtuels dans un ensemble d’échelle hello manuellement ou définir tooautoscale règles en fonction de l’utilisation du processeur, la demande de mémoire ou le trafic réseau.</span><span class="sxs-lookup"><span data-stu-id="dda12-105">You can scale hello number of VMs in hello scale set manually, or define rules tooautoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="dda12-106">Ce didacticiel explique comment déployer un groupe de machines virtuelles identiques dans Azure.</span><span class="sxs-lookup"><span data-stu-id="dda12-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="dda12-107">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="dda12-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dda12-108">Utiliser le nuage-init toocreate un tooscale d’application</span><span class="sxs-lookup"><span data-stu-id="dda12-108">Use cloud-init toocreate an app tooscale</span></span>
> * <span data-ttu-id="dda12-109">Créer un groupe de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="dda12-109">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="dda12-110">Augmentez ou diminuez le nombre de hello d’instances dans un ensemble d’échelle</span><span class="sxs-lookup"><span data-stu-id="dda12-110">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="dda12-111">Afficher les informations de connexion pour les instances de groupe identique</span><span class="sxs-lookup"><span data-stu-id="dda12-111">View connection info for scale set instances</span></span>
> * <span data-ttu-id="dda12-112">Utiliser des disques de données dans un groupe identique</span><span class="sxs-lookup"><span data-stu-id="dda12-112">Use data disks in a scale set</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="dda12-113">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="dda12-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="dda12-114">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="dda12-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="dda12-115">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dda12-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="scale-set-overview"></a><span data-ttu-id="dda12-116">Vue d’ensemble des groupes identiques</span><span class="sxs-lookup"><span data-stu-id="dda12-116">Scale Set overview</span></span>
<span data-ttu-id="dda12-117">Un ensemble d’échelle de machine virtuelle vous permet de toodeploy et gérer un ensemble de machines virtuelles identiques et la mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="dda12-117">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="dda12-118">Échelle définit utilisez hello mêmes composants que vous avez appris dans le cadre du didacticiel précédent hello trop[créer des ordinateurs virtuels à haute disponibilités](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="dda12-118">Scale sets use hello same components as you learned about in hello previous tutorial too[Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="dda12-119">Les machines virtuelles d’un groupe identique sont créées dans un groupe de disponibilité et réparties entre les domaines d’erreur logique et de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="dda12-119">VMs in a scale set are created in an availability set and distributed across logic fault and update domains.</span></span>

<span data-ttu-id="dda12-120">Les machines virtuelles sont créées en fonction des besoins dans un groupe identique.</span><span class="sxs-lookup"><span data-stu-id="dda12-120">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="dda12-121">Vous définissez toocontrol de règles de mise à l’échelle quand et comment les machines virtuelles sont ajoutés ou supprimés à partir d’un ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="dda12-121">You define autoscale rules toocontrol how and when VMs are added or removed from hello scale set.</span></span> <span data-ttu-id="dda12-122">Ces règles peuvent se déclencher en fonction de mesures telles que la charge du processeur, l’utilisation de la mémoire ou le trafic réseau.</span><span class="sxs-lookup"><span data-stu-id="dda12-122">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="dda12-123">Échelle définit la prise en charge des too1, 000 des machines virtuelles lorsque vous utilisez une image de plateforme Azure.</span><span class="sxs-lookup"><span data-stu-id="dda12-123">Scale sets support up too1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="dda12-124">Pour les charges de production, vous souhaiterez peut-être trop[créer une image de machine virtuelle personnalisée](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="dda12-124">For production workloads, you may wish too[Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="dda12-125">Vous pouvez créer des machines virtuelles de too100 dans une échelle définie lors de l’utilisation d’une image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="dda12-125">You can create up too100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-tooscale"></a><span data-ttu-id="dda12-126">Créer une application tooscale</span><span class="sxs-lookup"><span data-stu-id="dda12-126">Create an app tooscale</span></span>
<span data-ttu-id="dda12-127">À des fins de production, vous souhaiterez peut-être trop[créer une image de machine virtuelle personnalisée](tutorial-custom-images.md) qui inclut votre application installée et configurée.</span><span class="sxs-lookup"><span data-stu-id="dda12-127">For production use, you may wish too[Create a custom VM image](tutorial-custom-images.md) that includes your application installed and configured.</span></span> <span data-ttu-id="dda12-128">Pour ce didacticiel, permet de personnaliser les hello que machines virtuelles sur le premier démarrage tooquickly voir une échelle définie dans l’action.</span><span class="sxs-lookup"><span data-stu-id="dda12-128">For this tutorial, lets customize hello VMs on first boot tooquickly see a scale set in action.</span></span>

<span data-ttu-id="dda12-129">Dans un didacticiel précédent, vous avez appris [comment toocustomize une machine virtuelle de Linux au premier démarrage](tutorial-automate-vm-deployment.md) avec init-cloud.</span><span class="sxs-lookup"><span data-stu-id="dda12-129">In a previous tutorial, you learned [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md) with cloud-init.</span></span> <span data-ttu-id="dda12-130">Vous pouvez utiliser hello même tooinstall fichier de configuration cloud-init NGINX et exécuter une application Node.js de « Hello World » simple.</span><span class="sxs-lookup"><span data-stu-id="dda12-130">You can use hello same cloud-init configuration file tooinstall NGINX and run a simple 'Hello World' Node.js app.</span></span> 

<span data-ttu-id="dda12-131">Dans votre environnement actuel, créez un fichier nommé *cloud-init.txt* et coller hello de configuration suivante.</span><span class="sxs-lookup"><span data-stu-id="dda12-131">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="dda12-132">Par exemple, créer le fichier de hello Bonjour Cloud Shell pas sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="dda12-132">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="dda12-133">Entrez `sensible-editor cloud-init.txt` toocreate hello fichier et afficher la liste des éditeurs disponibles.</span><span class="sxs-lookup"><span data-stu-id="dda12-133">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="dda12-134">Assurez-vous que ce fichier d’ensemble cloud-init hello est copié correctement, en particulier hello première ligne :</span><span class="sxs-lookup"><span data-stu-id="dda12-134">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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


## <a name="create-a-scale-set"></a><span data-ttu-id="dda12-135">Créer un groupe identique</span><span class="sxs-lookup"><span data-stu-id="dda12-135">Create a scale set</span></span>
<span data-ttu-id="dda12-136">Pour pouvoir créer un groupe identique, vous devez créer un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="dda12-136">Before you can create a scale set, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="dda12-137">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroupScaleSet* Bonjour *eastus* emplacement :</span><span class="sxs-lookup"><span data-stu-id="dda12-137">hello following example creates a resource group named *myResourceGroupScaleSet* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

<span data-ttu-id="dda12-138">Créez à présent un groupe de machines virtuelles identiques avec [az vmss create](/cli/azure/vmss#create).</span><span class="sxs-lookup"><span data-stu-id="dda12-138">Now create a virtual machine scale set with [az vmss create](/cli/azure/vmss#create).</span></span> <span data-ttu-id="dda12-139">Hello exemple suivant crée une échelle définie nommée *myScaleSet*, utilise Bonjour cloud-init fichier toocustomize Bonjour VM et génère des clés SSH s’ils n’existent pas :</span><span class="sxs-lookup"><span data-stu-id="dda12-139">hello following example creates a scale set named *myScaleSet*, uses hello cloud-init file toocustomize hello VM, and generates SSH keys if they do not exist:</span></span>

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

<span data-ttu-id="dda12-140">Il prend quelques minutes toocreate et que vous configurez toutes les ressources de jeu de mise à l’échelle hello et machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="dda12-140">It takes a few minutes toocreate and configure all hello scale set resources and VMs.</span></span> <span data-ttu-id="dda12-141">Il existe des tâches en arrière-plan qui continuer toorun après que hello CLI d’Azure vous renvoie toohello invite.</span><span class="sxs-lookup"><span data-stu-id="dda12-141">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="dda12-142">Il peut être une ou deux minutes avant que vous pouvez accéder à application hello.</span><span class="sxs-lookup"><span data-stu-id="dda12-142">It may be another couple of minutes before you can access hello app.</span></span>


## <a name="allow-web-traffic"></a><span data-ttu-id="dda12-143">Autoriser le trafic web</span><span class="sxs-lookup"><span data-stu-id="dda12-143">Allow web traffic</span></span>
<span data-ttu-id="dda12-144">Un équilibreur de charge a été créé automatiquement dans le cadre de l’ensemble d’échelle de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="dda12-144">A load balancer was created automatically as part of hello virtual machine scale set.</span></span> <span data-ttu-id="dda12-145">équilibrage de charge Hello répartit le trafic sur un ensemble de VM défini à l’aide de règles d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="dda12-145">hello load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="dda12-146">Plus d’informations sur les concepts d’équilibrage de charge et de configuration dans le didacticiel suivant de hello, [comment tooload équilibrer les machines virtuelles dans Azure](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="dda12-146">You can learn more about load balancer concepts and configuration in hello next tutorial, [How tooload balance virtual machines in Azure](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="dda12-147">tooallow trafic tooreach hello web app, créez une règle avec [créer de règle d’équilibrage de charge réseau az](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="dda12-147">tooallow traffic tooreach hello web app, create a rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="dda12-148">Hello exemple suivant crée une règle nommée *myLoadBalancerRuleWeb*:</span><span class="sxs-lookup"><span data-stu-id="dda12-148">hello following example creates a rule named *myLoadBalancerRuleWeb*:</span></span>

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

## <a name="test-your-app"></a><span data-ttu-id="dda12-149">Test de l'application</span><span class="sxs-lookup"><span data-stu-id="dda12-149">Test your app</span></span>
<span data-ttu-id="dda12-150">toosee votre application Node.js sur le web de hello, obtenir hello adresse IP publique de votre équilibreur de charge avec [az réseau public-ip afficher](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="dda12-150">toosee your Node.js app on hello web, obtain hello public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="dda12-151">exemple Hello obtient adresse IP hello *myScaleSetLBPublicIP* créé comme faisant partie d’un ensemble d’échelle hello :</span><span class="sxs-lookup"><span data-stu-id="dda12-151">hello following example obtains hello IP address for *myScaleSetLBPublicIP* created as part of hello scale set:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="dda12-152">Entrez l’adresse IP publique de hello dans le navigateur web de tooa.</span><span class="sxs-lookup"><span data-stu-id="dda12-152">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="dda12-153">application Hello s’affiche, y compris le nom d’hôte hello Hello VM que hello la charge du trafic d’équilibrage distribué à :</span><span class="sxs-lookup"><span data-stu-id="dda12-153">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic to:</span></span>

![Exécution de l’application Node.js](./media/tutorial-create-vmss/running-nodejs-app.png)

<span data-ttu-id="dda12-155">toosee hello en puissance en action, vous pouvez forcer l’actualisation de le de votre charge web browser toosee hello équilibrage répartir le trafic entre tous les ordinateurs virtuels de hello votre application en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="dda12-155">toosee hello scale set in action, you can force-refresh your web browser toosee hello load balancer distribute traffic across all hello VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="dda12-156">Tâches de gestion</span><span class="sxs-lookup"><span data-stu-id="dda12-156">Management tasks</span></span>
<span data-ttu-id="dda12-157">Tout au long du cycle de vie hello de hello ensemble d’échelle, vous devrez peut-être toorun une ou plusieurs tâches de gestion.</span><span class="sxs-lookup"><span data-stu-id="dda12-157">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="dda12-158">En outre, vous souhaiterez toocreate les scripts qui automatisent différentes pour les tâches de cycle de vie.</span><span class="sxs-lookup"><span data-stu-id="dda12-158">Additionally, you may want toocreate scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="dda12-159">Bonjour Azure CLI 2.0 fournit un moyen rapide de toodo ces tâches.</span><span class="sxs-lookup"><span data-stu-id="dda12-159">hello Azure CLI 2.0 provides a quick way toodo those tasks.</span></span> <span data-ttu-id="dda12-160">Voici quelques tâches courantes.</span><span class="sxs-lookup"><span data-stu-id="dda12-160">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="dda12-161">Afficher les machines virtuelles d’un groupe identique</span><span class="sxs-lookup"><span data-stu-id="dda12-161">View VMs in a scale set</span></span>
<span data-ttu-id="dda12-162">une liste d’ordinateurs virtuels en cours d’exécution dans l’échelle de votre jeu de tooview, utilisez [az mise-instances de listes](/cli/azure/vmss#list-instances) comme suit :</span><span class="sxs-lookup"><span data-stu-id="dda12-162">tooview a list of VMs running in your scale set, use [az vmss list-instances](/cli/azure/vmss#list-instances) as follows:</span></span>

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

<span data-ttu-id="dda12-163">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="dda12-163">hello output is similar toohello following example:</span></span>

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="dda12-164">Augmenter ou diminuer les instances de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="dda12-164">Increase or decrease VM instances</span></span>
<span data-ttu-id="dda12-165">nombre de hello toosee d’instances actuellement dans une échelle paramétrées, utilisez [afficher mise de az](/cli/azure/vmss#show) et des requêtes sur *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="dda12-165">toosee hello number of instances you currently have in a scale set, use [az vmss show](/cli/azure/vmss#show) and query on *sku.capacity*:</span></span>

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

<span data-ttu-id="dda12-166">Vous pouvez puis manuellement augmenter ou réduire le nombre hello d’ordinateurs virtuels dans l’échelle de hello avec [mise à l’échelle de az mise](/cli/azure/vmss#scale).</span><span class="sxs-lookup"><span data-stu-id="dda12-166">You can then manually increase or decrease hello number of virtual machines in hello scale set with [az vmss scale](/cli/azure/vmss#scale).</span></span> <span data-ttu-id="dda12-167">Hello exemple suivant définit hello nombre de machines virtuelles dans votre échelle définie trop*5*:</span><span class="sxs-lookup"><span data-stu-id="dda12-167">hello following example sets hello number of VMs in your scale set too*5*:</span></span>

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

<span data-ttu-id="dda12-168">Les règles de mise à l’échelle vous permettent de définir comment tooscale monter ou descendre le nombre de hello d’ordinateurs virtuels dans votre échelle définies dans toodemand réponse telles que le trafic réseau ou de l’utilisation du processeur.</span><span class="sxs-lookup"><span data-stu-id="dda12-168">Autoscale rules let you define how tooscale up or down hello number of VMs in your scale set in response toodemand such as network traffic or CPU usage.</span></span> <span data-ttu-id="dda12-169">Actuellement, ces règles ne peuvent pas être définies dans Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="dda12-169">Currently, these rules cannot be set in Azure CLI 2.0.</span></span> <span data-ttu-id="dda12-170">Hello d’utilisation [portail Azure](https://portal.azure.com) tooconfigure mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="dda12-170">Use hello [Azure portal](https://portal.azure.com) tooconfigure autoscale.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="dda12-171">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="dda12-171">Get connection info</span></span>
<span data-ttu-id="dda12-172">les informations de connexion tooobtain sur hello des machines virtuelles dans vos jeux de mise à l’échelle, utilisez [az mise liste-instance-connexion-info](/cli/azure/vmss#list-instance-connection-info).</span><span class="sxs-lookup"><span data-stu-id="dda12-172">tooobtain connection information about hello VMs in your scale sets, use [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span></span> <span data-ttu-id="dda12-173">Cette commande génère une adresse IP publique de hello et le port pour chaque machine virtuelle qui vous permet de tooconnect avec SSH :</span><span class="sxs-lookup"><span data-stu-id="dda12-173">This command outputs hello public IP address and port for each VM that allows you tooconnect with SSH:</span></span>

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a><span data-ttu-id="dda12-174">Utiliser des disques de données avec des groupes identiques</span><span class="sxs-lookup"><span data-stu-id="dda12-174">Use data disks with scale sets</span></span>
<span data-ttu-id="dda12-175">Vous pouvez créer et utiliser des disques de données avec des groupes identiques.</span><span class="sxs-lookup"><span data-stu-id="dda12-175">You can create and use data disks with scale sets.</span></span> <span data-ttu-id="dda12-176">Dans un didacticiel précédent, vous avez appris comment trop[disques Azure de gérer](tutorial-manage-disks.md) que contours hello meilleures pratiques et les améliorations des performances pour la création d’applications sur des disques de données plutôt que sur le disque de hello du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="dda12-176">In a previous tutorial, you learned how too[Manage Azure disks](tutorial-manage-disks.md) that outlines hello best practices and performance improvements for building apps on data disks rather than hello OS disk.</span></span>

### <a name="create-scale-set-with-data-disks"></a><span data-ttu-id="dda12-177">Créer un groupe identique avec des disques de données</span><span class="sxs-lookup"><span data-stu-id="dda12-177">Create scale set with data disks</span></span>
<span data-ttu-id="dda12-178">toocreate une échelle définie et attacher des disques de données, ajouter hello `--data-disk-sizes-gb` paramètre toohello [az mise créer](/cli/azure/vmss#create) commande.</span><span class="sxs-lookup"><span data-stu-id="dda12-178">toocreate a scale set and attach data disks, add hello `--data-disk-sizes-gb` parameter toohello [az vmss create](/cli/azure/vmss#create) command.</span></span> <span data-ttu-id="dda12-179">Hello exemple suivant crée une échelle avec *50*Go des disques de données attaché tooeach instance :</span><span class="sxs-lookup"><span data-stu-id="dda12-179">hello following example creates a scale set with *50*Gb data disks attached tooeach instance:</span></span>

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

<span data-ttu-id="dda12-180">Lorsque les instances sont supprimées d’un groupe identique, les disques de données associés sont également supprimés.</span><span class="sxs-lookup"><span data-stu-id="dda12-180">When instances are removed from a scale set, any attached data disks are also removed.</span></span>

### <a name="add-data-disks"></a><span data-ttu-id="dda12-181">Ajouter des disques de données</span><span class="sxs-lookup"><span data-stu-id="dda12-181">Add data disks</span></span>
<span data-ttu-id="dda12-182">définir de tooadd un tooinstances de disque de données dans votre échelle, utilisez [attacher de disque de mise az](/cli/azure/vmss/disk#attach).</span><span class="sxs-lookup"><span data-stu-id="dda12-182">tooadd a data disk tooinstances in your scale set, use [az vmss disk attach](/cli/azure/vmss/disk#attach).</span></span> <span data-ttu-id="dda12-183">Hello exemple suivant ajoute un *50*instance de tooeach Go disque :</span><span class="sxs-lookup"><span data-stu-id="dda12-183">hello following example adds a *50*Gb disk tooeach instance:</span></span>

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a><span data-ttu-id="dda12-184">Détacher des disques de données</span><span class="sxs-lookup"><span data-stu-id="dda12-184">Detach data disks</span></span>
<span data-ttu-id="dda12-185">définir de tooremove un tooinstances de disque de données dans votre échelle, utilisez [détachement du disque de mise az](/cli/azure/vmss/disk#detach).</span><span class="sxs-lookup"><span data-stu-id="dda12-185">tooremove a data disk tooinstances in your scale set, use [az vmss disk detach](/cli/azure/vmss/disk#detach).</span></span> <span data-ttu-id="dda12-186">Hello exemple suivant supprime le disque de données hello au numéro d’unité logique *2* de chaque instance de :</span><span class="sxs-lookup"><span data-stu-id="dda12-186">hello following example removes hello data disk at LUN *2* from each instance:</span></span>

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a><span data-ttu-id="dda12-187">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dda12-187">Next steps</span></span>
<span data-ttu-id="dda12-188">Ce didacticiel vous a montré comment créer un groupe de machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="dda12-188">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="dda12-189">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="dda12-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dda12-190">Utiliser le nuage-init toocreate un tooscale d’application</span><span class="sxs-lookup"><span data-stu-id="dda12-190">Use cloud-init toocreate an app tooscale</span></span>
> * <span data-ttu-id="dda12-191">Créer un groupe de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="dda12-191">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="dda12-192">Augmentez ou diminuez le nombre de hello d’instances dans un ensemble d’échelle</span><span class="sxs-lookup"><span data-stu-id="dda12-192">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="dda12-193">Afficher les informations de connexion pour les instances de groupe identique</span><span class="sxs-lookup"><span data-stu-id="dda12-193">View connection info for scale set instances</span></span>
> * <span data-ttu-id="dda12-194">Utiliser des disques de données dans un groupe identique</span><span class="sxs-lookup"><span data-stu-id="dda12-194">Use data disks in a scale set</span></span>

<span data-ttu-id="dda12-195">Avance toolearn de didacticiel suivant toohello plus d’informations sur les concepts de machines virtuelles d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="dda12-195">Advance toohello next tutorial toolearn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dda12-196">Équilibrage de charge des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="dda12-196">Load balance virtual machines</span></span>](tutorial-load-balancer.md)