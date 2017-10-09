---
title: "aaaCustomize un VM Linux au premier démarrage dans Azure | Documents Microsoft"
description: "Découvrez comment toouse cloud-init et hello de machines virtuelles Linux coffre de clés toocustomze première fois que les serveurs démarrent dans Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 280189723ac0205226f9c0068bd605da13249ace
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-linux-virtual-machine-on-first-boot"></a><span data-ttu-id="e6a95-103">Comment toocustomize une machine virtuelle de Linux au premier démarrage</span><span class="sxs-lookup"><span data-stu-id="e6a95-103">How toocustomize a Linux virtual machine on first boot</span></span>
<span data-ttu-id="e6a95-104">Dans un didacticiel précédent, vous avez appris comment tooSSH tooa virtual machine (VM) et installer manuellement les NGINX.</span><span class="sxs-lookup"><span data-stu-id="e6a95-104">In a previous tutorial, you learned how tooSSH tooa virtual machine (VM) and manually install NGINX.</span></span> <span data-ttu-id="e6a95-105">toocreate machines virtuelles de manière rapide et cohérente, une forme d’automatisation est généralement souhaité.</span><span class="sxs-lookup"><span data-stu-id="e6a95-105">toocreate VMs in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="e6a95-106">Un toocustomize approche commune une machine virtuelle au premier démarrage est toouse [cloud-init](https://cloudinit.readthedocs.io).</span><span class="sxs-lookup"><span data-stu-id="e6a95-106">A common approach toocustomize a VM on first boot is toouse [cloud-init](https://cloudinit.readthedocs.io).</span></span> <span data-ttu-id="e6a95-107">Ce didacticiel vous explique comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e6a95-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e6a95-108">Créer un fichier de configuration cloud-init</span><span class="sxs-lookup"><span data-stu-id="e6a95-108">Create a cloud-init config file</span></span>
> * <span data-ttu-id="e6a95-109">Créer une machine virtuelle utilisant un fichier cloud-init</span><span class="sxs-lookup"><span data-stu-id="e6a95-109">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="e6a95-110">Afficher une application en cours d’exécution de Node.js après hello que machine virtuelle est créée.</span><span class="sxs-lookup"><span data-stu-id="e6a95-110">View a running Node.js app after hello VM is created</span></span>
> * <span data-ttu-id="e6a95-111">Utiliser des certificats de coffre de clés toosecurely magasin</span><span class="sxs-lookup"><span data-stu-id="e6a95-111">Use Key Vault toosecurely store certificates</span></span>
> * <span data-ttu-id="e6a95-112">Automatiser des déploiements sécurisés de NGINX avec cloud-init</span><span class="sxs-lookup"><span data-stu-id="e6a95-112">Automate secure deployments of NGINX with cloud-init</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e6a95-113">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="e6a95-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="e6a95-114">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="e6a95-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e6a95-115">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e6a95-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  



## <a name="cloud-init-overview"></a><span data-ttu-id="e6a95-116">Présentation de cloud-init</span><span class="sxs-lookup"><span data-stu-id="e6a95-116">Cloud-init overview</span></span>
<span data-ttu-id="e6a95-117">[Init-cloud](https://cloudinit.readthedocs.io) est un toocustomize approche largement utilisée une VM Linux au démarrage pour hello première fois.</span><span class="sxs-lookup"><span data-stu-id="e6a95-117">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach toocustomize a Linux VM as it boots for hello first time.</span></span> <span data-ttu-id="e6a95-118">Vous pouvez utiliser des packages tooinstall init de cloud et écrire des fichiers, ou de tooconfigure utilisateurs et de sécurité.</span><span class="sxs-lookup"><span data-stu-id="e6a95-118">You can use cloud-init tooinstall packages and write files, or tooconfigure users and security.</span></span> <span data-ttu-id="e6a95-119">Comme le cloud-init s’exécute pendant le processus de démarrage initial hello, il n’existe aucune étape supplémentaire ou agents tooapply votre configuration.</span><span class="sxs-lookup"><span data-stu-id="e6a95-119">As cloud-init runs during hello initial boot process, there are no additional steps or required agents tooapply your configuration.</span></span>

<span data-ttu-id="e6a95-120">Cloud-init fonctionne aussi sur les différentes distributions.</span><span class="sxs-lookup"><span data-stu-id="e6a95-120">Cloud-init also works across distributions.</span></span> <span data-ttu-id="e6a95-121">Par exemple, vous n’utilisez pas **apt-get install** ou **yum installer** tooinstall un package.</span><span class="sxs-lookup"><span data-stu-id="e6a95-121">For example, you don't use **apt-get install** or **yum install** tooinstall a package.</span></span> <span data-ttu-id="e6a95-122">Au lieu de cela, vous pouvez définir une liste de packages tooinstall.</span><span class="sxs-lookup"><span data-stu-id="e6a95-122">Instead you can define a list of packages tooinstall.</span></span> <span data-ttu-id="e6a95-123">Init-cloud utilise automatiquement l’outil de gestion de package native de hello pour distribution hello que vous sélectionnez.</span><span class="sxs-lookup"><span data-stu-id="e6a95-123">Cloud-init automatically uses hello native package management tool for hello distro you select.</span></span>

<span data-ttu-id="e6a95-124">Nous sommes utilisation de nos partenaires tooget cloud-init inclus et utilisation dans des images hello qu’ils fournissent des tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e6a95-124">We are working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span> <span data-ttu-id="e6a95-125">Hello tableau suivant souligne hello actuel cloud-init disponibilité sur les images de plateforme Azure :</span><span class="sxs-lookup"><span data-stu-id="e6a95-125">hello following table outlines hello current cloud-init availability on Azure platform images:</span></span>

| <span data-ttu-id="e6a95-126">Alias</span><span class="sxs-lookup"><span data-stu-id="e6a95-126">Alias</span></span> | <span data-ttu-id="e6a95-127">Éditeur</span><span class="sxs-lookup"><span data-stu-id="e6a95-127">Publisher</span></span> | <span data-ttu-id="e6a95-128">Offer</span><span class="sxs-lookup"><span data-stu-id="e6a95-128">Offer</span></span> | <span data-ttu-id="e6a95-129">SKU</span><span class="sxs-lookup"><span data-stu-id="e6a95-129">SKU</span></span> | <span data-ttu-id="e6a95-130">Version</span><span class="sxs-lookup"><span data-stu-id="e6a95-130">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="e6a95-131">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="e6a95-131">UbuntuLTS</span></span> |<span data-ttu-id="e6a95-132">Canonical</span><span class="sxs-lookup"><span data-stu-id="e6a95-132">Canonical</span></span> |<span data-ttu-id="e6a95-133">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="e6a95-133">UbuntuServer</span></span> |<span data-ttu-id="e6a95-134">16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="e6a95-134">16.04-LTS</span></span> |<span data-ttu-id="e6a95-135">le plus récent</span><span class="sxs-lookup"><span data-stu-id="e6a95-135">latest</span></span> |
| <span data-ttu-id="e6a95-136">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="e6a95-136">UbuntuLTS</span></span> |<span data-ttu-id="e6a95-137">Canonical</span><span class="sxs-lookup"><span data-stu-id="e6a95-137">Canonical</span></span> |<span data-ttu-id="e6a95-138">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="e6a95-138">UbuntuServer</span></span> |<span data-ttu-id="e6a95-139">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="e6a95-139">14.04.5-LTS</span></span> |<span data-ttu-id="e6a95-140">le plus récent</span><span class="sxs-lookup"><span data-stu-id="e6a95-140">latest</span></span> |
| <span data-ttu-id="e6a95-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="e6a95-141">CoreOS</span></span> |<span data-ttu-id="e6a95-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="e6a95-142">CoreOS</span></span> |<span data-ttu-id="e6a95-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="e6a95-143">CoreOS</span></span> |<span data-ttu-id="e6a95-144">Stable</span><span class="sxs-lookup"><span data-stu-id="e6a95-144">Stable</span></span> |<span data-ttu-id="e6a95-145">le plus récent</span><span class="sxs-lookup"><span data-stu-id="e6a95-145">latest</span></span> |


## <a name="create-cloud-init-config-file"></a><span data-ttu-id="e6a95-146">Créer un fichier de configuration cloud-init</span><span class="sxs-lookup"><span data-stu-id="e6a95-146">Create cloud-init config file</span></span>
<span data-ttu-id="e6a95-147">toosee cloud-init dans action, créez une machine virtuelle qui installe NGINX et exécute une application Node.js de « Hello World » simple.</span><span class="sxs-lookup"><span data-stu-id="e6a95-147">toosee cloud-init in action, create a VM that installs NGINX and runs a simple 'Hello World' Node.js app.</span></span> <span data-ttu-id="e6a95-148">Hello configuration du cloud-init suivante installe les packages hello requis, crée une application Node.js, puis initialisez et démarre l’application hello.</span><span class="sxs-lookup"><span data-stu-id="e6a95-148">hello following cloud-init configuration installs hello required packages, creates a Node.js app, then initialize and starts hello app.</span></span>

<span data-ttu-id="e6a95-149">Dans votre environnement actuel, créez un fichier nommé *cloud-init.txt* et coller hello de configuration suivante.</span><span class="sxs-lookup"><span data-stu-id="e6a95-149">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="e6a95-150">Par exemple, créer le fichier de hello Bonjour Cloud Shell pas sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="e6a95-150">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="e6a95-151">Vous pouvez utiliser l’éditeur de votre choix.</span><span class="sxs-lookup"><span data-stu-id="e6a95-151">You can use any editor you wish.</span></span> <span data-ttu-id="e6a95-152">Entrez `sensible-editor cloud-init.txt` toocreate hello fichier et afficher la liste des éditeurs disponibles.</span><span class="sxs-lookup"><span data-stu-id="e6a95-152">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="e6a95-153">Assurez-vous que ce fichier d’ensemble cloud-init hello est copié correctement, en particulier hello première ligne :</span><span class="sxs-lookup"><span data-stu-id="e6a95-153">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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

<span data-ttu-id="e6a95-154">Pour plus d’informations sur les options de configuration de cloud-init, consultez les [exemples de configuration cloud-init](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span><span class="sxs-lookup"><span data-stu-id="e6a95-154">For more information about cloud-init configuration options, see [cloud-init config examples](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="e6a95-155">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="e6a95-155">Create virtual machine</span></span>
<span data-ttu-id="e6a95-156">Pour pouvoir créer une machine virtuelle, vous devez créer un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e6a95-156">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="e6a95-157">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroupAutomate* Bonjour *eastus* emplacement :</span><span class="sxs-lookup"><span data-stu-id="e6a95-157">hello following example creates a resource group named *myResourceGroupAutomate* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

<span data-ttu-id="e6a95-158">Créez maintenant une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="e6a95-158">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="e6a95-159">Hello d’utilisation `--custom-data` toopass de paramètre dans votre fichier de configuration cloud-init.</span><span class="sxs-lookup"><span data-stu-id="e6a95-159">Use hello `--custom-data` parameter toopass in your cloud-init config file.</span></span> <span data-ttu-id="e6a95-160">Fournir hello chemin d’accès complet toohello *init.txt de cloud* configuration si vous avez enregistré le fichier de hello en dehors de votre répertoire de travail actuelle.</span><span class="sxs-lookup"><span data-stu-id="e6a95-160">Provide hello full path toohello *cloud-init.txt* config if you saved hello file outside of your present working directory.</span></span> <span data-ttu-id="e6a95-161">Hello exemple suivant crée un ordinateur virtuel nommé *myAutomatedVM*:</span><span class="sxs-lookup"><span data-stu-id="e6a95-161">hello following example creates a VM named *myAutomatedVM*:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="e6a95-162">Il prend quelques minutes pour hello toobe de machine virtuelle créée, hello packages tooinstall et toostart d’application hello.</span><span class="sxs-lookup"><span data-stu-id="e6a95-162">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="e6a95-163">Il existe des tâches en arrière-plan qui continuer toorun après que hello CLI d’Azure vous renvoie toohello invite.</span><span class="sxs-lookup"><span data-stu-id="e6a95-163">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="e6a95-164">Il peut être une ou deux minutes avant que vous pouvez accéder à application hello.</span><span class="sxs-lookup"><span data-stu-id="e6a95-164">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="e6a95-165">Lorsque hello machine virtuelle a été créé, prenez note de hello `publicIpAddress` affiché par hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="e6a95-165">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="e6a95-166">Cette adresse est utilisée tooaccess hello Node.js application via un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="e6a95-166">This address is used tooaccess hello Node.js app via a web browser.</span></span>

<span data-ttu-id="e6a95-167">tooallow web tooreach de trafic de votre machine virtuelle, ouvrez port 80 du hello Internet avec [ouvrir un ordinateur virtuel az-port](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="e6a95-167">tooallow web traffic tooreach your VM, open port 80 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a><span data-ttu-id="e6a95-168">Tester l’application web</span><span class="sxs-lookup"><span data-stu-id="e6a95-168">Test web app</span></span>
<span data-ttu-id="e6a95-169">Vous pouvez désormais ouvrir un navigateur web et entrez *http://<publicIpAddress>*  dans la barre d’adresses hello.</span><span class="sxs-lookup"><span data-stu-id="e6a95-169">Now you can open a web browser and enter *http://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="e6a95-170">Fournissez vos propres adresse IP à partir de la machine virtuelle de hello créer le processus.</span><span class="sxs-lookup"><span data-stu-id="e6a95-170">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="e6a95-171">Votre application Node.js s’affiche comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="e6a95-171">Your Node.js app is displayed as in hello following example:</span></span>

![Afficher le site NGINX en cours d’exécution](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a><span data-ttu-id="e6a95-173">Injecter des certificats à partir de Key Vault</span><span class="sxs-lookup"><span data-stu-id="e6a95-173">Inject certificates from Key Vault</span></span>
<span data-ttu-id="e6a95-174">Cette section montre comment vous pouvez stocker des certificats dans le coffre de clés Azure en toute sécurité et les injecter pendant hello déploiement des ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="e6a95-174">This optional section shows how you can securely store certificates in Azure Key Vault and inject them during hello VM deployment.</span></span> <span data-ttu-id="e6a95-175">Au lieu d’utiliser une image personnalisée qui inclut les certificats de hello cuit-in, ce processus garantit que les certificats hello plus récentes sont injectées tooa VM au premier démarrage.</span><span class="sxs-lookup"><span data-stu-id="e6a95-175">Rather than using a custom image that includes hello certificates baked-in, this process ensures that hello most up-to-date certificates are injected tooa VM on first boot.</span></span> <span data-ttu-id="e6a95-176">Pendant le processus de hello, certificat hello jamais laisse hello plateforme Azure ou est exposée dans un script, un historique de ligne de commande ou un modèle.</span><span class="sxs-lookup"><span data-stu-id="e6a95-176">During hello process, hello certificate never leaves hello Azure platform or is exposed in a script, command-line history, or template.</span></span>

<span data-ttu-id="e6a95-177">Azure Key Vault protège les clés de chiffrement et les secrets, tels que les certificats ou les mots de passe.</span><span class="sxs-lookup"><span data-stu-id="e6a95-177">Azure Key Vault safeguards cryptographic keys and secrets, such as certificates or passwords.</span></span> <span data-ttu-id="e6a95-178">Coffre de clés permet de rationaliser le processus de gestion de clés hello et vous permet de contrôler toomaintain clés d’accès et de chiffrer vos données.</span><span class="sxs-lookup"><span data-stu-id="e6a95-178">Key Vault helps streamline hello key management process and enables you toomaintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="e6a95-179">Ce scénario présente certains toocreate des concepts de coffre de clés et les utiliser un certificat, bien que n’est pas une vue d’ensemble exhaustive sur la façon de toouse le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="e6a95-179">This scenario introduces some Key Vault concepts toocreate and use a certificate, though is not an exhaustive overview on how toouse Key Vault.</span></span>

<span data-ttu-id="e6a95-180">comment vous pouvez affiche les Hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e6a95-180">hello following steps show how you can:</span></span>

- <span data-ttu-id="e6a95-181">Créer un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="e6a95-181">Create an Azure Key Vault</span></span>
- <span data-ttu-id="e6a95-182">Générer ou télécharger un certificat de toohello le coffre de clés</span><span class="sxs-lookup"><span data-stu-id="e6a95-182">Generate or upload a certificate toohello Key Vault</span></span>
- <span data-ttu-id="e6a95-183">Créer une clé secrète à partir de tooinject de certificat hello dans tooa machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e6a95-183">Create a secret from hello certificate tooinject in tooa VM</span></span>
- <span data-ttu-id="e6a95-184">Créer une machine virtuelle et injecter du certificat de hello</span><span class="sxs-lookup"><span data-stu-id="e6a95-184">Create a VM and inject hello certificate</span></span>

### <a name="create-an-azure-key-vault"></a><span data-ttu-id="e6a95-185">Créer un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="e6a95-185">Create an Azure Key Vault</span></span>
<span data-ttu-id="e6a95-186">Commencez par créer un Key Vault avec la commande [az keyvault create](/cli/azure/keyvault#create) et activez son utilisation lors du déploiement d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e6a95-186">First, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="e6a95-187">Chaque Key Vault requiert un nom unique en minuscules.</span><span class="sxs-lookup"><span data-stu-id="e6a95-187">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="e6a95-188">Remplacez *mykeyvault* Bonjour votre propre nom de coffre de clés unique de l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="e6a95-188">Replace *mykeyvault* in hello following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a><span data-ttu-id="e6a95-189">Générer le certificat et le stocker dans Key Vault</span><span class="sxs-lookup"><span data-stu-id="e6a95-189">Generate certificate and store in Key Vault</span></span>
<span data-ttu-id="e6a95-190">Dans un environnement de production, vous devez importer un certificat valide signé par un fournisseur approuvé à l’aide de la commande [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="e6a95-190">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span></span> <span data-ttu-id="e6a95-191">Pour ce didacticiel, hello suivant montre comment vous pouvez générer un certificat auto-signé avec [création de certificat de keyvault az](/cli/azure/keyvault/certificate#create) qui utilise la stratégie de certificat par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="e6a95-191">For this tutorial, hello following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/keyvault/certificate#create) that uses hello default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a><span data-ttu-id="e6a95-192">Préparer le certificat en vue de son utilisation avec la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e6a95-192">Prepare certificate for use with VM</span></span>
<span data-ttu-id="e6a95-193">certificat de hello de toouse pendant hello VM créer un processus, obtenir l’ID hello de votre certificat avec [az keyvault secrète liste versions](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="e6a95-193">toouse hello certificate during hello VM create process, obtain hello ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="e6a95-194">Hello machine virtuelle a besoin de certificat de hello dans une certaine tooinject format il au démarrage du système, par conséquent, convertir certificat hello avec [az vm format-secret](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="e6a95-194">hello VM needs hello certificate in a certain format tooinject it on boot, so convert hello certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="e6a95-195">Hello, l’exemple suivant attribue à sortie hello de toovariables de ces commandes pour faciliter l’utilisation Bonjour étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e6a95-195">hello following example assigns hello output of these commands toovariables for ease of use in hello next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-toosecure-nginx"></a><span data-ttu-id="e6a95-196">Créer le nuage-init config toosecure NGINX</span><span class="sxs-lookup"><span data-stu-id="e6a95-196">Create cloud-init config toosecure NGINX</span></span>
<span data-ttu-id="e6a95-197">Lorsque vous créez une machine virtuelle, les certificats et clés sont stockées dans hello protégé */var/lib/waagent/* active.</span><span class="sxs-lookup"><span data-stu-id="e6a95-197">When you create a VM, certificates and keys are stored in hello protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="e6a95-198">tooautomate Ajout hello certificat toohello machine virtuelle et la configuration NGINX, vous pouvez utiliser une configuration cloud-init mis à jour à partir de l’exemple précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="e6a95-198">tooautomate adding hello certificate toohello VM and configuring NGINX, you can use an updated cloud-init config from hello previous example.</span></span>

<span data-ttu-id="e6a95-199">Créez un fichier nommé *cloud-init-secured.txt* et coller hello de configuration suivante.</span><span class="sxs-lookup"><span data-stu-id="e6a95-199">Create a file named *cloud-init-secured.txt* and paste hello following configuration.</span></span> <span data-ttu-id="e6a95-200">Là encore, si vous utilisez hello Shell de cloud computing, vous devez créer le fichier de configuration cloud-init hello ici et pas sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="e6a95-200">Again, if you use hello Cloud Shell, create hello cloud-init config file there and not on your local machine.</span></span> <span data-ttu-id="e6a95-201">Utilisez `sensible-editor cloud-init-secured.txt` toocreate hello fichier et afficher la liste des éditeurs disponibles.</span><span class="sxs-lookup"><span data-stu-id="e6a95-201">Use `sensible-editor cloud-init-secured.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="e6a95-202">Assurez-vous que ce fichier d’ensemble cloud-init hello est copié correctement, en particulier hello première ligne :</span><span class="sxs-lookup"><span data-stu-id="e6a95-202">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
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
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-secure-vm"></a><span data-ttu-id="e6a95-203">Créer une machine virtuelle sécurisée</span><span class="sxs-lookup"><span data-stu-id="e6a95-203">Create secure VM</span></span>
<span data-ttu-id="e6a95-204">Créez maintenant une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="e6a95-204">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="e6a95-205">les données de certificat Hello sont injectées dans le coffre de clés avec hello `--secrets` paramètre.</span><span class="sxs-lookup"><span data-stu-id="e6a95-205">hello certificate data is injected from Key Vault with hello `--secrets` parameter.</span></span> <span data-ttu-id="e6a95-206">Comme exemple précédent de hello, vous passez également dans la configuration du cloud-init hello avec hello `--custom-data` paramètre :</span><span class="sxs-lookup"><span data-stu-id="e6a95-206">As in hello previous example, you also pass in hello cloud-init config with hello `--custom-data` parameter:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-secured.txt \
    --secrets "$vm_secret"
```

<span data-ttu-id="e6a95-207">Il prend quelques minutes pour hello toobe de machine virtuelle créée, hello packages tooinstall et toostart d’application hello.</span><span class="sxs-lookup"><span data-stu-id="e6a95-207">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="e6a95-208">Il existe des tâches en arrière-plan qui continuer toorun après que hello CLI d’Azure vous renvoie toohello invite.</span><span class="sxs-lookup"><span data-stu-id="e6a95-208">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="e6a95-209">Il peut être une ou deux minutes avant que vous pouvez accéder à application hello.</span><span class="sxs-lookup"><span data-stu-id="e6a95-209">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="e6a95-210">Lorsque hello machine virtuelle a été créé, prenez note de hello `publicIpAddress` affiché par hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="e6a95-210">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="e6a95-211">Cette adresse est utilisée tooaccess hello Node.js application via un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="e6a95-211">This address is used tooaccess hello Node.js app via a web browser.</span></span>

<span data-ttu-id="e6a95-212">tooallow sécurisé tooreach du trafic web de votre machine virtuelle, ouvrir le port 443 à partir de hello Internet avec [ouvrir un ordinateur virtuel az-port](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="e6a95-212">tooallow secure web traffic tooreach your VM, open port 443 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a><span data-ttu-id="e6a95-213">Tester l’application web sécurisée</span><span class="sxs-lookup"><span data-stu-id="e6a95-213">Test secure web app</span></span>
<span data-ttu-id="e6a95-214">Vous pouvez désormais ouvrir un navigateur web et entrez *https://<publicIpAddress>*  dans la barre d’adresses hello.</span><span class="sxs-lookup"><span data-stu-id="e6a95-214">Now you can open a web browser and enter *https://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="e6a95-215">Fournissez vos propres adresse IP à partir de la machine virtuelle de hello créer le processus.</span><span class="sxs-lookup"><span data-stu-id="e6a95-215">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="e6a95-216">Acceptez l’avertissement de sécurité hello si vous avez utilisé un certificat auto-signé :</span><span class="sxs-lookup"><span data-stu-id="e6a95-216">Accept hello security warning if you used a self-signed certificate:</span></span>

![Accepter l’avertissement de sécurité du navigateur web](./media/tutorial-automate-vm-deployment/browser-warning.png)

<span data-ttu-id="e6a95-218">Votre site NGINX sécurisés et les Node.js application est ensuite affichée comme hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="e6a95-218">Your secured NGINX site and Node.js app is then displayed as in hello following example:</span></span>

![Afficher le site NGINX sécurisé en cours d’exécution](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="e6a95-220">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e6a95-220">Next steps</span></span>
<span data-ttu-id="e6a95-221">Ce didacticiel vous a montré comment configurer des machines virtuelles au premier démarrage avec cloud-init.</span><span class="sxs-lookup"><span data-stu-id="e6a95-221">In this tutorial, you configured VMs on first boot with cloud-init.</span></span> <span data-ttu-id="e6a95-222">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="e6a95-222">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e6a95-223">Créer un fichier de configuration cloud-init</span><span class="sxs-lookup"><span data-stu-id="e6a95-223">Create a cloud-init config file</span></span>
> * <span data-ttu-id="e6a95-224">Créer une machine virtuelle utilisant un fichier cloud-init</span><span class="sxs-lookup"><span data-stu-id="e6a95-224">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="e6a95-225">Afficher une application en cours d’exécution de Node.js après hello que machine virtuelle est créée.</span><span class="sxs-lookup"><span data-stu-id="e6a95-225">View a running Node.js app after hello VM is created</span></span>
> * <span data-ttu-id="e6a95-226">Utiliser des certificats de coffre de clés toosecurely magasin</span><span class="sxs-lookup"><span data-stu-id="e6a95-226">Use Key Vault toosecurely store certificates</span></span>
> * <span data-ttu-id="e6a95-227">Automatiser des déploiements sécurisés de NGINX avec cloud-init</span><span class="sxs-lookup"><span data-stu-id="e6a95-227">Automate secure deployments of NGINX with cloud-init</span></span>

<span data-ttu-id="e6a95-228">Avancer toolearn de didacticiel suivant toohello comment toocreate les images de machine virtuelle personnalisées.</span><span class="sxs-lookup"><span data-stu-id="e6a95-228">Advance toohello next tutorial toolearn how toocreate custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e6a95-229">Créer des images de machine virtuelle personnalisées</span><span class="sxs-lookup"><span data-stu-id="e6a95-229">Create custom VM images</span></span>](./tutorial-custom-images.md)
