---
title: "Personnaliser une machine virtuelle Linux au premier démarrage dans Azure | Microsoft Docs"
description: "Découvrez comment utiliser cloud-init et Key Vault pour personnaliser les machines virtuelles lors de leur premier démarrage dans Azure"
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
ms.openlocfilehash: 6adf4e43aa80c28c6f5f8d8a071966323ba85723
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-customize-a-linux-virtual-machine-on-first-boot"></a><span data-ttu-id="9a0ab-103">Comment personnaliser une machine virtuelle Linux au premier démarrage</span><span class="sxs-lookup"><span data-stu-id="9a0ab-103">How to customize a Linux virtual machine on first boot</span></span>
<span data-ttu-id="9a0ab-104">Dans un didacticiel précédent, vous avez appris comment établir une connexion SSH à une machine virtuelle et installer NGINX manuellement.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-104">In a previous tutorial, you learned how to SSH to a virtual machine (VM) and manually install NGINX.</span></span> <span data-ttu-id="9a0ab-105">Pour créer des machines virtuelles de façon rapide et cohérente, une certaine forme d’automatisation est généralement souhaitable.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-105">To create VMs in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="9a0ab-106">Pour personnaliser une machine virtuelle au premier démarrage, l’approche la plus courante consiste à utiliser [cloud-init](https://cloudinit.readthedocs.io).</span><span class="sxs-lookup"><span data-stu-id="9a0ab-106">A common approach to customize a VM on first boot is to use [cloud-init](https://cloudinit.readthedocs.io).</span></span> <span data-ttu-id="9a0ab-107">Ce tutoriel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="9a0ab-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9a0ab-108">Créer un fichier de configuration cloud-init</span><span class="sxs-lookup"><span data-stu-id="9a0ab-108">Create a cloud-init config file</span></span>
> * <span data-ttu-id="9a0ab-109">Créer une machine virtuelle utilisant un fichier cloud-init</span><span class="sxs-lookup"><span data-stu-id="9a0ab-109">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="9a0ab-110">Afficher une application Node.js en cours d’exécution une fois la machine virtuelle est créée</span><span class="sxs-lookup"><span data-stu-id="9a0ab-110">View a running Node.js app after the VM is created</span></span>
> * <span data-ttu-id="9a0ab-111">Utiliser un Key Vault pour stocker des certificats en toute sécurité</span><span class="sxs-lookup"><span data-stu-id="9a0ab-111">Use Key Vault to securely store certificates</span></span>
> * <span data-ttu-id="9a0ab-112">Automatiser des déploiements sécurisés de NGINX avec cloud-init</span><span class="sxs-lookup"><span data-stu-id="9a0ab-112">Automate secure deployments of NGINX with cloud-init</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9a0ab-113">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0.4 ou une version ultérieure pour poursuivre la procédure décrite dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9a0ab-114">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="9a0ab-115">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9a0ab-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  



## <a name="cloud-init-overview"></a><span data-ttu-id="9a0ab-116">Présentation de cloud-init</span><span class="sxs-lookup"><span data-stu-id="9a0ab-116">Cloud-init overview</span></span>
<span data-ttu-id="9a0ab-117">[Cloud-init](https://cloudinit.readthedocs.io) est une méthode largement utilisée pour personnaliser une machine virtuelle Linux lors de son premier démarrage.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-117">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach to customize a Linux VM as it boots for the first time.</span></span> <span data-ttu-id="9a0ab-118">Vous pouvez utiliser cloud-init pour installer des packages et écrire des fichiers, ou encore pour configurer des utilisateurs ou des paramètres de sécurité.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-118">You can use cloud-init to install packages and write files, or to configure users and security.</span></span> <span data-ttu-id="9a0ab-119">Comme cloud-init s’exécute pendant le processus de démarrage initial, aucune autre étape ni aucun agent ne sont nécessaires pour appliquer votre configuration.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-119">As cloud-init runs during the initial boot process, there are no additional steps or required agents to apply your configuration.</span></span>

<span data-ttu-id="9a0ab-120">Cloud-init fonctionne aussi sur les différentes distributions.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-120">Cloud-init also works across distributions.</span></span> <span data-ttu-id="9a0ab-121">Par exemple, vous n’utilisez pas **apt-get install** ou **yum install** pour installer un package.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-121">For example, you don't use **apt-get install** or **yum install** to install a package.</span></span> <span data-ttu-id="9a0ab-122">Au lieu de cela, vous pouvez définir une liste des packages à installer,</span><span class="sxs-lookup"><span data-stu-id="9a0ab-122">Instead you can define a list of packages to install.</span></span> <span data-ttu-id="9a0ab-123">après quoi cloud-init se charge d’utiliser automatiquement l’outil de gestion de package natif correspondant à la distribution que vous sélectionnez.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-123">Cloud-init automatically uses the native package management tool for the distro you select.</span></span>

<span data-ttu-id="9a0ab-124">Nous collaborons avec nos partenaires pour que cloud-init soit inclus et fonctionne dans les images qu’ils fournissent à Azure.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-124">We are working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span> <span data-ttu-id="9a0ab-125">Le tableau suivant présente la disponibilité actuelle de cloud-init sur les images de plateforme Azure :</span><span class="sxs-lookup"><span data-stu-id="9a0ab-125">The following table outlines the current cloud-init availability on Azure platform images:</span></span>

| <span data-ttu-id="9a0ab-126">Alias</span><span class="sxs-lookup"><span data-stu-id="9a0ab-126">Alias</span></span> | <span data-ttu-id="9a0ab-127">Éditeur</span><span class="sxs-lookup"><span data-stu-id="9a0ab-127">Publisher</span></span> | <span data-ttu-id="9a0ab-128">Offer</span><span class="sxs-lookup"><span data-stu-id="9a0ab-128">Offer</span></span> | <span data-ttu-id="9a0ab-129">SKU</span><span class="sxs-lookup"><span data-stu-id="9a0ab-129">SKU</span></span> | <span data-ttu-id="9a0ab-130">Version</span><span class="sxs-lookup"><span data-stu-id="9a0ab-130">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="9a0ab-131">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="9a0ab-131">UbuntuLTS</span></span> |<span data-ttu-id="9a0ab-132">Canonical</span><span class="sxs-lookup"><span data-stu-id="9a0ab-132">Canonical</span></span> |<span data-ttu-id="9a0ab-133">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="9a0ab-133">UbuntuServer</span></span> |<span data-ttu-id="9a0ab-134">16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="9a0ab-134">16.04-LTS</span></span> |<span data-ttu-id="9a0ab-135">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9a0ab-135">latest</span></span> |
| <span data-ttu-id="9a0ab-136">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="9a0ab-136">UbuntuLTS</span></span> |<span data-ttu-id="9a0ab-137">Canonical</span><span class="sxs-lookup"><span data-stu-id="9a0ab-137">Canonical</span></span> |<span data-ttu-id="9a0ab-138">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="9a0ab-138">UbuntuServer</span></span> |<span data-ttu-id="9a0ab-139">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="9a0ab-139">14.04.5-LTS</span></span> |<span data-ttu-id="9a0ab-140">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9a0ab-140">latest</span></span> |
| <span data-ttu-id="9a0ab-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="9a0ab-141">CoreOS</span></span> |<span data-ttu-id="9a0ab-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="9a0ab-142">CoreOS</span></span> |<span data-ttu-id="9a0ab-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="9a0ab-143">CoreOS</span></span> |<span data-ttu-id="9a0ab-144">Stable</span><span class="sxs-lookup"><span data-stu-id="9a0ab-144">Stable</span></span> |<span data-ttu-id="9a0ab-145">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9a0ab-145">latest</span></span> |


## <a name="create-cloud-init-config-file"></a><span data-ttu-id="9a0ab-146">Créer un fichier de configuration cloud-init</span><span class="sxs-lookup"><span data-stu-id="9a0ab-146">Create cloud-init config file</span></span>
<span data-ttu-id="9a0ab-147">Pour voir le cloud-init en action, créez une machine virtuelle qui installe NGINX et exécute une simple application « Hello World » Node.js.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-147">To see cloud-init in action, create a VM that installs NGINX and runs a simple 'Hello World' Node.js app.</span></span> <span data-ttu-id="9a0ab-148">La configuration cloud-init suivante installe les packages, crée une application Node.js, puis initialise et démarre l’application.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-148">The following cloud-init configuration installs the required packages, creates a Node.js app, then initialize and starts the app.</span></span>

<span data-ttu-id="9a0ab-149">Dans l’interpréteur de commandes actuel, créez un fichier nommé *cloud-init.txt* et collez la configuration suivante.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-149">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="9a0ab-150">Par exemple, créez le fichier dans l’interpréteur de commandes Cloud et non sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-150">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="9a0ab-151">Vous pouvez utiliser l’éditeur de votre choix.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-151">You can use any editor you wish.</span></span> <span data-ttu-id="9a0ab-152">Entrez `sensible-editor cloud-init.txt` pour créer le fichier et afficher la liste des éditeurs disponibles.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-152">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="9a0ab-153">Vérifiez que l’intégralité du fichier cloud-init est copiée, en particulier la première ligne :</span><span class="sxs-lookup"><span data-stu-id="9a0ab-153">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

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

<span data-ttu-id="9a0ab-154">Pour plus d’informations sur les options de configuration de cloud-init, consultez les [exemples de configuration cloud-init](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span><span class="sxs-lookup"><span data-stu-id="9a0ab-154">For more information about cloud-init configuration options, see [cloud-init config examples](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="9a0ab-155">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="9a0ab-155">Create virtual machine</span></span>
<span data-ttu-id="9a0ab-156">Pour pouvoir créer une machine virtuelle, vous devez créer un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="9a0ab-156">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="9a0ab-157">L’exemple suivant crée un groupe de ressources nommé *myResourceGroupAutomate* dans l’emplacement *westus*:</span><span class="sxs-lookup"><span data-stu-id="9a0ab-157">The following example creates a resource group named *myResourceGroupAutomate* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

<span data-ttu-id="9a0ab-158">Créez maintenant une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="9a0ab-158">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="9a0ab-159">Utilisez le paramètre `--custom-data` à transmettre dans votre fichier de configuration cloud-init.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-159">Use the `--custom-data` parameter to pass in your cloud-init config file.</span></span> <span data-ttu-id="9a0ab-160">Indiquez le chemin complet vers la configuration *cloud-init.txt* si vous avez enregistré le fichier en dehors de votre répertoire de travail actuel.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-160">Provide the full path to the *cloud-init.txt* config if you saved the file outside of your present working directory.</span></span> <span data-ttu-id="9a0ab-161">L’exemple suivant permet de créer une machine virtuelle nommée *myAutomatedVM* :</span><span class="sxs-lookup"><span data-stu-id="9a0ab-161">The following example creates a VM named *myAutomatedVM*:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="9a0ab-162">Vous devez patienter quelques minutes le temps que la machine virtuelle soit créée, que les packages soient installés et que l’application démarre.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-162">It takes a few minutes for the VM to be created, the packages to install, and the app to start.</span></span> <span data-ttu-id="9a0ab-163">Certaines tâches en arrière-plan continuent à s’exécuter une fois que l’interface CLI Azure vous renvoie à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-163">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="9a0ab-164">Un délai de quelques minutes peut être nécessaire avant que vous puissiez accéder à l’application.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-164">It may be another couple of minutes before you can access the app.</span></span> <span data-ttu-id="9a0ab-165">Une fois la machine virtuelle créée, notez la valeur de `publicIpAddress` qui s’affiche dans l’interface Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-165">When the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="9a0ab-166">Cette adresse est utilisée pour accéder à l’application Node.js via un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-166">This address is used to access the Node.js app via a web browser.</span></span>

<span data-ttu-id="9a0ab-167">Pour autoriser le trafic web à accéder à votre machine virtuelle, ouvrez le port 80 à partir d’Internet à l’aide de la commande [az vm open-port](/cli/azure/vm#open-port) :</span><span class="sxs-lookup"><span data-stu-id="9a0ab-167">To allow web traffic to reach your VM, open port 80 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a><span data-ttu-id="9a0ab-168">Tester l’application web</span><span class="sxs-lookup"><span data-stu-id="9a0ab-168">Test web app</span></span>
<span data-ttu-id="9a0ab-169">Vous pouvez maintenant ouvrir un navigateur web et entrer *http://<publicIpAddress>* dans la barre d’adresse.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-169">Now you can open a web browser and enter *http://<publicIpAddress>* in the address bar.</span></span> <span data-ttu-id="9a0ab-170">Indiquez votre propre adresse IP publique à partir du processus de création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-170">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="9a0ab-171">Votre application Node.js apparaît telle que dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="9a0ab-171">Your Node.js app is displayed as in the following example:</span></span>

![Afficher le site NGINX en cours d’exécution](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a><span data-ttu-id="9a0ab-173">Injecter des certificats à partir de Key Vault</span><span class="sxs-lookup"><span data-stu-id="9a0ab-173">Inject certificates from Key Vault</span></span>
<span data-ttu-id="9a0ab-174">Cette section montre comment stocker des certificats en toute sécurité dans Azure Key Vault et comment les injecter lors du déploiement de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-174">This optional section shows how you can securely store certificates in Azure Key Vault and inject them during the VM deployment.</span></span> <span data-ttu-id="9a0ab-175">Au lieu d’utiliser une image personnalisée qui inclut les certificats intégrés, ce processus permet d’injecter les certificats les plus récents dans une machine virtuelle dès le premier démarrage.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-175">Rather than using a custom image that includes the certificates baked-in, this process ensures that the most up-to-date certificates are injected to a VM on first boot.</span></span> <span data-ttu-id="9a0ab-176">Pendant le processus, le certificat ne quitte jamais la plateforme Azure ; il est exposé dans un script, un historique de ligne de commande ou un modèle.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-176">During the process, the certificate never leaves the Azure platform or is exposed in a script, command-line history, or template.</span></span>

<span data-ttu-id="9a0ab-177">Azure Key Vault protège les clés de chiffrement et les secrets, tels que les certificats ou les mots de passe.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-177">Azure Key Vault safeguards cryptographic keys and secrets, such as certificates or passwords.</span></span> <span data-ttu-id="9a0ab-178">Key Vault rationalise le processus de gestion de clés et vous permet de garder le contrôle des clés qui accèdent à vos données et les chiffrent.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-178">Key Vault helps streamline the key management process and enables you to maintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="9a0ab-179">Ce scénario présente quelques concepts de Key Vault permettant de créer et utiliser un certificat ; il ne prétend pas détailler de manière exhaustive l’utilisation de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-179">This scenario introduces some Key Vault concepts to create and use a certificate, though is not an exhaustive overview on how to use Key Vault.</span></span>

<span data-ttu-id="9a0ab-180">Les étapes suivantes vous expliquent comment :</span><span class="sxs-lookup"><span data-stu-id="9a0ab-180">The following steps show how you can:</span></span>

- <span data-ttu-id="9a0ab-181">Créer un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="9a0ab-181">Create an Azure Key Vault</span></span>
- <span data-ttu-id="9a0ab-182">Générer ou télécharger un certificat dans Key Vault</span><span class="sxs-lookup"><span data-stu-id="9a0ab-182">Generate or upload a certificate to the Key Vault</span></span>
- <span data-ttu-id="9a0ab-183">Créer un secret à partir du certificat pour l’injecter dans une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="9a0ab-183">Create a secret from the certificate to inject in to a VM</span></span>
- <span data-ttu-id="9a0ab-184">Créer une machine virtuelle et injecter le certificat</span><span class="sxs-lookup"><span data-stu-id="9a0ab-184">Create a VM and inject the certificate</span></span>

### <a name="create-an-azure-key-vault"></a><span data-ttu-id="9a0ab-185">Créer un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="9a0ab-185">Create an Azure Key Vault</span></span>
<span data-ttu-id="9a0ab-186">Commencez par créer un Key Vault avec la commande [az keyvault create](/cli/azure/keyvault#create) et activez son utilisation lors du déploiement d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-186">First, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="9a0ab-187">Chaque Key Vault requiert un nom unique en minuscules.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-187">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="9a0ab-188">Remplacez *mykeyvault* dans l’exemple suivant par le nom unique de votre propre Key Vault :</span><span class="sxs-lookup"><span data-stu-id="9a0ab-188">Replace *mykeyvault* in the following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a><span data-ttu-id="9a0ab-189">Générer le certificat et le stocker dans Key Vault</span><span class="sxs-lookup"><span data-stu-id="9a0ab-189">Generate certificate and store in Key Vault</span></span>
<span data-ttu-id="9a0ab-190">Dans un environnement de production, vous devez importer un certificat valide signé par un fournisseur approuvé à l’aide de la commande [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="9a0ab-190">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span></span> <span data-ttu-id="9a0ab-191">Pour ce didacticiel, l’exemple suivant vous montre comment générer un certificat auto-signé avec la commande [az keyvault certificate create](/cli/azure/keyvault/certificate#create) qui utilise la stratégie de certificat par défaut :</span><span class="sxs-lookup"><span data-stu-id="9a0ab-191">For this tutorial, the following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/keyvault/certificate#create) that uses the default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a><span data-ttu-id="9a0ab-192">Préparer le certificat en vue de son utilisation avec la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="9a0ab-192">Prepare certificate for use with VM</span></span>
<span data-ttu-id="9a0ab-193">Pour utiliser le certificat au cours du processus de création de la machine virtuelle, récupérez l’ID de votre certificat à l’aide de la commande [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="9a0ab-193">To use the certificate during the VM create process, obtain the ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="9a0ab-194">Le certificat doit respecter un certain format pour être injecté au démarrage du système par la machine virtuelle. Par conséquent, convertissez le certificat avec [az vm format-secret](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="9a0ab-194">The VM needs the certificate in a certain format to inject it on boot, so convert the certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="9a0ab-195">L’exemple suivant affecte la sortie de ces commandes à des variables, afin de simplifier la procédure dans les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="9a0ab-195">The following example assigns the output of these commands to variables for ease of use in the next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-to-secure-nginx"></a><span data-ttu-id="9a0ab-196">Créer la configuration cloud-init pour sécuriser NGINX</span><span class="sxs-lookup"><span data-stu-id="9a0ab-196">Create cloud-init config to secure NGINX</span></span>
<span data-ttu-id="9a0ab-197">Lorsque vous créez une machine virtuelle, les certificats et les clés sont stockés dans le répertoire */var/lib/waagent/* protégé.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-197">When you create a VM, certificates and keys are stored in the protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="9a0ab-198">Pour ajouter le certificat à la machine virtuelle et configurer NGINX de façon automatique, vous pouvez utiliser une configuration cloud-init mise à jour par rapport à l’exemple précédent.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-198">To automate adding the certificate to the VM and configuring NGINX, you can use an updated cloud-init config from the previous example.</span></span>

<span data-ttu-id="9a0ab-199">Créez un fichier nommé *cloud-init-secured.txt* et collez la configuration suivante.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-199">Create a file named *cloud-init-secured.txt* and paste the following configuration.</span></span> <span data-ttu-id="9a0ab-200">Là encore, si vous utilisez Cloud Shell, vous devez créer le fichier de configuration cloud-init ici et non sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-200">Again, if you use the Cloud Shell, create the cloud-init config file there and not on your local machine.</span></span> <span data-ttu-id="9a0ab-201">Utilisez `sensible-editor cloud-init-secured.txt` pour créer le fichier et afficher la liste des éditeurs disponibles.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-201">Use `sensible-editor cloud-init-secured.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="9a0ab-202">Vérifiez que l’intégralité du fichier cloud-init est copiée, en particulier la première ligne :</span><span class="sxs-lookup"><span data-stu-id="9a0ab-202">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

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

### <a name="create-secure-vm"></a><span data-ttu-id="9a0ab-203">Créer une machine virtuelle sécurisée</span><span class="sxs-lookup"><span data-stu-id="9a0ab-203">Create secure VM</span></span>
<span data-ttu-id="9a0ab-204">Créez maintenant une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="9a0ab-204">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="9a0ab-205">Les données de certificat sont injectées à partir de Key Vault avec le paramètre `--secrets`.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-205">The certificate data is injected from Key Vault with the `--secrets` parameter.</span></span> <span data-ttu-id="9a0ab-206">Comme dans l’exemple précédent, vous allez également transmettre la configuration de cloud-init avec le paramètre `--custom-data` :</span><span class="sxs-lookup"><span data-stu-id="9a0ab-206">As in the previous example, you also pass in the cloud-init config with the `--custom-data` parameter:</span></span>

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

<span data-ttu-id="9a0ab-207">Vous devez patienter quelques minutes le temps que la machine virtuelle soit créée, que les packages soient installés et que l’application démarre.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-207">It takes a few minutes for the VM to be created, the packages to install, and the app to start.</span></span> <span data-ttu-id="9a0ab-208">Certaines tâches en arrière-plan continuent à s’exécuter une fois que l’interface CLI Azure vous renvoie à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-208">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="9a0ab-209">Un délai de quelques minutes peut être nécessaire avant que vous puissiez accéder à l’application.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-209">It may be another couple of minutes before you can access the app.</span></span> <span data-ttu-id="9a0ab-210">Une fois la machine virtuelle créée, notez la valeur de `publicIpAddress` qui s’affiche dans l’interface Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-210">When the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="9a0ab-211">Cette adresse est utilisée pour accéder à l’application Node.js via un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-211">This address is used to access the Node.js app via a web browser.</span></span>

<span data-ttu-id="9a0ab-212">Pour autoriser le trafic web sécurisé à accéder à votre machine virtuelle, ouvrez le port 443 à partir d’Internet à l’aide de la commande [az vm open-port](/cli/azure/vm#open-port) :</span><span class="sxs-lookup"><span data-stu-id="9a0ab-212">To allow secure web traffic to reach your VM, open port 443 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a><span data-ttu-id="9a0ab-213">Tester l’application web sécurisée</span><span class="sxs-lookup"><span data-stu-id="9a0ab-213">Test secure web app</span></span>
<span data-ttu-id="9a0ab-214">Vous pouvez maintenant ouvrir un navigateur web et entrer *https://<publicIpAddress>* dans la barre d’adresse.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-214">Now you can open a web browser and enter *https://<publicIpAddress>* in the address bar.</span></span> <span data-ttu-id="9a0ab-215">Indiquez votre propre adresse IP publique à partir du processus de création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-215">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="9a0ab-216">Acceptez l’avertissement de sécurité si vous avez utilisé un certificat auto-signé :</span><span class="sxs-lookup"><span data-stu-id="9a0ab-216">Accept the security warning if you used a self-signed certificate:</span></span>

![Accepter l’avertissement de sécurité du navigateur web](./media/tutorial-automate-vm-deployment/browser-warning.png)

<span data-ttu-id="9a0ab-218">Votre site NGINX sécurisé et votre application Node.js apparaissent maintenant dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="9a0ab-218">Your secured NGINX site and Node.js app is then displayed as in the following example:</span></span>

![Afficher le site NGINX sécurisé en cours d’exécution](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="9a0ab-220">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9a0ab-220">Next steps</span></span>
<span data-ttu-id="9a0ab-221">Ce didacticiel vous a montré comment configurer des machines virtuelles au premier démarrage avec cloud-init.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-221">In this tutorial, you configured VMs on first boot with cloud-init.</span></span> <span data-ttu-id="9a0ab-222">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="9a0ab-222">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9a0ab-223">Créer un fichier de configuration cloud-init</span><span class="sxs-lookup"><span data-stu-id="9a0ab-223">Create a cloud-init config file</span></span>
> * <span data-ttu-id="9a0ab-224">Créer une machine virtuelle utilisant un fichier cloud-init</span><span class="sxs-lookup"><span data-stu-id="9a0ab-224">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="9a0ab-225">Afficher une application Node.js en cours d’exécution une fois la machine virtuelle est créée</span><span class="sxs-lookup"><span data-stu-id="9a0ab-225">View a running Node.js app after the VM is created</span></span>
> * <span data-ttu-id="9a0ab-226">Utiliser un Key Vault pour stocker des certificats en toute sécurité</span><span class="sxs-lookup"><span data-stu-id="9a0ab-226">Use Key Vault to securely store certificates</span></span>
> * <span data-ttu-id="9a0ab-227">Automatiser des déploiements sécurisés de NGINX avec cloud-init</span><span class="sxs-lookup"><span data-stu-id="9a0ab-227">Automate secure deployments of NGINX with cloud-init</span></span>

<span data-ttu-id="9a0ab-228">Passez au didacticiel suivant pour découvrir comment créer des images de machine virtuelle personnalisées.</span><span class="sxs-lookup"><span data-stu-id="9a0ab-228">Advance to the next tutorial to learn how to create custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9a0ab-229">Créer des images de machine virtuelle personnalisées</span><span class="sxs-lookup"><span data-stu-id="9a0ab-229">Create custom VM images</span></span>](./tutorial-custom-images.md)
