---
title: "Sécuriser un serveur web à l’aide de certificats SSL dans Azure | Microsoft Docs"
description: "Découvrez comment sécuriser le serveur web NGINX à l’aide de certificats SSL sur une machine virtuelle Linux dans Azure"
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
ms.date: 07/17/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 181be35aeb61020db3abaeba22aa882848923c31
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="59b25-103">Sécuriser un serveur web à l’aide de certificats SSL sur une machine virtuelle Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="59b25-103">Secure a web server with SSL certificates on a Linux virtual machine in Azure</span></span>
<span data-ttu-id="59b25-104">Pour sécuriser les serveurs web, vous pouvez utiliser un certificat SSL (Secure Sockets Layer) et chiffrer ainsi le trafic web.</span><span class="sxs-lookup"><span data-stu-id="59b25-104">To secure web servers, a Secure Sockets Later (SSL) certificate can be used to encrypt web traffic.</span></span> <span data-ttu-id="59b25-105">Ces certificats SSL peuvent être stockés dans Azure Key Vault et autoriser des déploiements sécurisés de certificats sur des machines virtuelles Linux dans Azure.</span><span class="sxs-lookup"><span data-stu-id="59b25-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates to Linux virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="59b25-106">Ce didacticiel vous explique comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="59b25-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="59b25-107">Créer un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="59b25-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="59b25-108">Générer ou télécharger un certificat dans Key Vault</span><span class="sxs-lookup"><span data-stu-id="59b25-108">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="59b25-109">Créer une machine virtuelle et installer le serveur web NGINX</span><span class="sxs-lookup"><span data-stu-id="59b25-109">Create a VM and install the NGINX web server</span></span>
> * <span data-ttu-id="59b25-110">Injecter le certificat dans la machine virtuelle et configurer NGINX à l’aide d’une liaison SSL</span><span class="sxs-lookup"><span data-stu-id="59b25-110">Inject the certificate into the VM and configure NGINX with an SSL binding</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="59b25-111">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0.4 ou une version ultérieure pour poursuivre la procédure décrite dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="59b25-111">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="59b25-112">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="59b25-112">Run `az --version` to find the version.</span></span> <span data-ttu-id="59b25-113">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="59b25-113">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  


## <a name="overview"></a><span data-ttu-id="59b25-114">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="59b25-114">Overview</span></span>
<span data-ttu-id="59b25-115">Azure Key Vault protège les clés de chiffrement et les secrets, tels que les certificats ou les mots de passe.</span><span class="sxs-lookup"><span data-stu-id="59b25-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="59b25-116">Key Vault rationalise le processus de gestion de certificats et vous permet de garder le contrôle sur les clés d’accès à ces certificats.</span><span class="sxs-lookup"><span data-stu-id="59b25-116">Key Vault helps streamline the certificate management process and enables you to maintain control of keys that access those certificates.</span></span> <span data-ttu-id="59b25-117">Vous pouvez créer un certificat auto-signé à l’intérieur de Key Vault ou charger un certificat approuvé existant que vous avez déjà.</span><span class="sxs-lookup"><span data-stu-id="59b25-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="59b25-118">Au lieu d’utiliser une image de machine virtuelle personnalisée qui inclut des certificats intégrés, vous injectez des certificats dans une machine virtuelle en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="59b25-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="59b25-119">Ce processus garantit que les certificats les plus récents sont installés sur un serveur web pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="59b25-119">This process ensures that the most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="59b25-120">Si vous renouvelez ou remplacez un certificat, vous n’êtes pas non plus obligé de créer une image de machine virtuelle personnalisée.</span><span class="sxs-lookup"><span data-stu-id="59b25-120">If you renew or replace a certificate, you don't also have to create a new custom VM image.</span></span> <span data-ttu-id="59b25-121">Les certificats les plus récents sont automatiquement injectés à la création des machines virtuelles supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="59b25-121">The latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="59b25-122">Pendant tout le processus, les certificats ne quittent jamais la plateforme Azure, ni ne sont exposés dans un script, un historique de ligne de commande ou un modèle.</span><span class="sxs-lookup"><span data-stu-id="59b25-122">During the whole process, the certificates never leave the Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="59b25-123">Créer un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="59b25-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="59b25-124">Avant de créer un coffre de clés et des certificats, créez un groupe de ressources avec [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="59b25-124">Before you can create a Key Vault and certificates, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="59b25-125">L’exemple suivant crée un groupe de ressources nommé *myResourceGroupSecureWeb* à l’emplacement *eastus* :</span><span class="sxs-lookup"><span data-stu-id="59b25-125">The following example creates a resource group named *myResourceGroupSecureWeb* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

<span data-ttu-id="59b25-126">Ensuite, créez un coffre de clés avec la commande [az keyvault create](/cli/azure/keyvault#create) et activez son utilisation lors du déploiement d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="59b25-126">Next, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="59b25-127">Chaque Key Vault requiert un nom unique en minuscules.</span><span class="sxs-lookup"><span data-stu-id="59b25-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="59b25-128">Remplacez *<mykeyvault>* dans l’exemple suivant par le nom unique de votre propre Key Vault :</span><span class="sxs-lookup"><span data-stu-id="59b25-128">Replace *<mykeyvault>* in the following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="59b25-129">Générer un certificat et le stocker dans Key Vault</span><span class="sxs-lookup"><span data-stu-id="59b25-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="59b25-130">Dans un environnement de production, vous devez importer un certificat valide signé par un fournisseur approuvé à l’aide de la commande [az keyvault certificate import](/cli/azure/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="59b25-130">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/certificate#import).</span></span> <span data-ttu-id="59b25-131">Pour ce didacticiel, l’exemple suivant vous montre comment générer un certificat auto-signé avec la commande [az keyvault certificate create](/cli/azure/certificate#create) qui utilise la stratégie de certificat par défaut :</span><span class="sxs-lookup"><span data-stu-id="59b25-131">For this tutorial, the following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/certificate#create) that uses the default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a><span data-ttu-id="59b25-132">Préparer un certificat en vue de son utilisation avec une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="59b25-132">Prepare a certificate for use with a VM</span></span>
<span data-ttu-id="59b25-133">Pour utiliser le certificat au cours du processus de création de la machine virtuelle, récupérez l’ID de votre certificat à l’aide de la commande [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="59b25-133">To use the certificate during the VM create process, obtain the ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="59b25-134">Utilisez la commande [az vm format-secret](/cli/azure/vm#format-secret) pour convertir le certificat.</span><span class="sxs-lookup"><span data-stu-id="59b25-134">Convert the certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="59b25-135">L’exemple suivant affecte la sortie de ces commandes à des variables, afin de simplifier la procédure dans les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="59b25-135">The following example assigns the output of these commands to variables for ease of use in the next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-to-secure-nginx"></a><span data-ttu-id="59b25-136">Créer une configuration cloud-init pour sécuriser NGINX</span><span class="sxs-lookup"><span data-stu-id="59b25-136">Create a cloud-init config to secure NGINX</span></span>
<span data-ttu-id="59b25-137">[Cloud-init](https://cloudinit.readthedocs.io) est une méthode largement utilisée pour personnaliser une machine virtuelle Linux lors de son premier démarrage.</span><span class="sxs-lookup"><span data-stu-id="59b25-137">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach to customize a Linux VM as it boots for the first time.</span></span> <span data-ttu-id="59b25-138">Vous pouvez utiliser cloud-init pour installer des packages et écrire des fichiers, ou encore pour configurer des utilisateurs ou des paramètres de sécurité.</span><span class="sxs-lookup"><span data-stu-id="59b25-138">You can use cloud-init to install packages and write files, or to configure users and security.</span></span> <span data-ttu-id="59b25-139">Comme cloud-init s’exécute pendant le processus de démarrage initial, aucune autre étape ni aucun agent ne sont nécessaires pour appliquer votre configuration.</span><span class="sxs-lookup"><span data-stu-id="59b25-139">As cloud-init runs during the initial boot process, there are no additional steps or required agents to apply your configuration.</span></span>

<span data-ttu-id="59b25-140">Lorsque vous créez une machine virtuelle, les certificats et les clés sont stockés dans le répertoire */var/lib/waagent/* protégé.</span><span class="sxs-lookup"><span data-stu-id="59b25-140">When you create a VM, certificates and keys are stored in the protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="59b25-141">Pour automatiser l’ajout du certificat à la machine virtuelle et la configuration du serveur web, utilisez cloud-init.</span><span class="sxs-lookup"><span data-stu-id="59b25-141">To automate adding the certificate to the VM and configuring the web server, use cloud-init.</span></span> <span data-ttu-id="59b25-142">Dans cet exemple, nous installons et configurons le serveur web NGINX.</span><span class="sxs-lookup"><span data-stu-id="59b25-142">In this example, we install and configure the NGINX web server.</span></span> <span data-ttu-id="59b25-143">Vous pouvez utiliser le même processus pour installer et configurer Apache.</span><span class="sxs-lookup"><span data-stu-id="59b25-143">You can use the same process to install and configure Apache.</span></span> 

<span data-ttu-id="59b25-144">Créez un fichier nommé *cloud-init-web-server.txt* et collez la configuration suivante :</span><span class="sxs-lookup"><span data-stu-id="59b25-144">Create a file named *cloud-init-web-server.txt* and paste the following configuration:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
      }
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
```

### <a name="create-a-secure-vm"></a><span data-ttu-id="59b25-145">Créer une machine virtuelle sécurisée</span><span class="sxs-lookup"><span data-stu-id="59b25-145">Create a secure VM</span></span>
<span data-ttu-id="59b25-146">Créez maintenant une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="59b25-146">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="59b25-147">Les données de certificat sont injectées à partir de Key Vault avec le paramètre `--secrets`.</span><span class="sxs-lookup"><span data-stu-id="59b25-147">The certificate data is injected from Key Vault with the `--secrets` parameter.</span></span> <span data-ttu-id="59b25-148">Vous transmettez la configuration cloud-init à l’aide du paramètre `--custom-data` :</span><span class="sxs-lookup"><span data-stu-id="59b25-148">You pass in the cloud-init config with the `--custom-data` parameter:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-web-server.txt \
    --secrets "$vm_secret"
```

<span data-ttu-id="59b25-149">Vous devez patienter quelques minutes le temps que la machine virtuelle soit créée, que les packages soient installés et que l’application démarre.</span><span class="sxs-lookup"><span data-stu-id="59b25-149">It takes a few minutes for the VM to be created, the packages to install, and the app to start.</span></span> <span data-ttu-id="59b25-150">Une fois la machine virtuelle créée, notez la valeur de `publicIpAddress` qui s’affiche dans l’interface Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="59b25-150">When the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="59b25-151">Cette adresse est utilisée pour accéder à votre site à l’aide d’un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="59b25-151">This address is used to access your site in a web browser.</span></span>

<span data-ttu-id="59b25-152">Pour autoriser le trafic web sécurisé à accéder à votre machine virtuelle, ouvrez le port 443 à partir d’Internet à l’aide de la commande [az vm open-port](/cli/azure/vm#open-port) :</span><span class="sxs-lookup"><span data-stu-id="59b25-152">To allow secure web traffic to reach your VM, open port 443 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-the-secure-web-app"></a><span data-ttu-id="59b25-153">Tester l’application web sécurisée</span><span class="sxs-lookup"><span data-stu-id="59b25-153">Test the secure web app</span></span>
<span data-ttu-id="59b25-154">Vous pouvez maintenant ouvrir un navigateur web et entrer *https://<publicIpAddress>* dans la barre d’adresse.</span><span class="sxs-lookup"><span data-stu-id="59b25-154">Now you can open a web browser and enter *https://<publicIpAddress>* in the address bar.</span></span> <span data-ttu-id="59b25-155">Indiquez votre propre adresse IP publique à partir du processus de création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="59b25-155">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="59b25-156">Acceptez l’avertissement de sécurité si vous avez utilisé un certificat auto-signé :</span><span class="sxs-lookup"><span data-stu-id="59b25-156">Accept the security warning if you used a self-signed certificate:</span></span>

![Accepter l’avertissement de sécurité du navigateur web](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="59b25-158">Votre site NGINX sécurisé apparaît maintenant comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="59b25-158">Your secured NGINX site is then displayed as in the following example:</span></span>

![Afficher le site NGINX sécurisé en cours d’exécution](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="59b25-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="59b25-160">Next steps</span></span>

<span data-ttu-id="59b25-161">Dans ce didacticiel, vous avez sécurisé un serveur web NGINX à l’aide d’un certificat SSL stocké dans Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="59b25-161">In this tutorial, you secured an NGINX web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="59b25-162">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="59b25-162">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="59b25-163">Créer un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="59b25-163">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="59b25-164">Générer ou télécharger un certificat dans Key Vault</span><span class="sxs-lookup"><span data-stu-id="59b25-164">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="59b25-165">Créer une machine virtuelle et installer le serveur web NGINX</span><span class="sxs-lookup"><span data-stu-id="59b25-165">Create a VM and install the NGINX web server</span></span>
> * <span data-ttu-id="59b25-166">Injecter le certificat dans la machine virtuelle et configurer NGINX à l’aide d’une liaison SSL</span><span class="sxs-lookup"><span data-stu-id="59b25-166">Inject the certificate into the VM and configure NGINX with an SSL binding</span></span>

<span data-ttu-id="59b25-167">Suivez ce lien pour consulter des exemples de scripts de machine virtuelle prédéfinis.</span><span class="sxs-lookup"><span data-stu-id="59b25-167">Follow this link to see pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="59b25-168">Exemples de scripts de machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="59b25-168">Windows virtual machine script samples</span></span>](./cli-samples.md)