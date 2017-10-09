---
title: aaaSecure un serveur web avec SSL des certificats dans Azure | Documents Microsoft
description: "Découvrez comment les certificats serveur de web NGINX toosecure hello avec SSL sur un VM Linux dans Azure"
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
ms.openlocfilehash: d3a62d77ac05c9aa2a44356b7c8e44cb485b81aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="f2607-103">Sécuriser un serveur web à l’aide de certificats SSL sur une machine virtuelle Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="f2607-103">Secure a web server with SSL certificates on a Linux virtual machine in Azure</span></span>
<span data-ttu-id="f2607-104">les serveurs web toosecure, un certificat ultérieurement SSL (Secure Sockets) peut être utilisé tooencrypt le trafic web.</span><span class="sxs-lookup"><span data-stu-id="f2607-104">toosecure web servers, a Secure Sockets Later (SSL) certificate can be used tooencrypt web traffic.</span></span> <span data-ttu-id="f2607-105">Ces certificats SSL peuvent être stockées dans le coffre de clés Azure et autoriser des déploiements sécurisés de certificats tooLinux virtual machines virtuelles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f2607-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates tooLinux virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="f2607-106">Ce didacticiel vous explique comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="f2607-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f2607-107">Créer un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="f2607-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="f2607-108">Générer ou télécharger un certificat de toohello le coffre de clés</span><span class="sxs-lookup"><span data-stu-id="f2607-108">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="f2607-109">Créer une machine virtuelle et installer le serveur web hello NGINX</span><span class="sxs-lookup"><span data-stu-id="f2607-109">Create a VM and install hello NGINX web server</span></span>
> * <span data-ttu-id="f2607-110">Injecter du certificat de hello dans hello machine virtuelle et configurer NGINX avec une liaison SSL</span><span class="sxs-lookup"><span data-stu-id="f2607-110">Inject hello certificate into hello VM and configure NGINX with an SSL binding</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f2607-111">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="f2607-111">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="f2607-112">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="f2607-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f2607-113">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f2607-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  


## <a name="overview"></a><span data-ttu-id="f2607-114">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f2607-114">Overview</span></span>
<span data-ttu-id="f2607-115">Azure Key Vault protège les clés de chiffrement et les secrets, tels que les certificats ou les mots de passe.</span><span class="sxs-lookup"><span data-stu-id="f2607-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="f2607-116">Coffre de clés permet de rationaliser le processus de gestion des certificats hello et vous permet de contrôler toomaintain clés qui accèdent à ces certificats.</span><span class="sxs-lookup"><span data-stu-id="f2607-116">Key Vault helps streamline hello certificate management process and enables you toomaintain control of keys that access those certificates.</span></span> <span data-ttu-id="f2607-117">Vous pouvez créer un certificat auto-signé à l’intérieur de Key Vault ou charger un certificat approuvé existant que vous avez déjà.</span><span class="sxs-lookup"><span data-stu-id="f2607-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="f2607-118">Au lieu d’utiliser une image de machine virtuelle personnalisée qui inclut des certificats intégrés, vous injectez des certificats dans une machine virtuelle en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f2607-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="f2607-119">Ce processus garantit que les certificats hello plus récentes sont installés sur un serveur web pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="f2607-119">This process ensures that hello most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="f2607-120">Si vous renouvelez ou remplacez un certificat, vous ne pouvez toocreate une nouvelle image de machine virtuelle personnalisée.</span><span class="sxs-lookup"><span data-stu-id="f2607-120">If you renew or replace a certificate, you don't also have toocreate a new custom VM image.</span></span> <span data-ttu-id="f2607-121">certificats de dernière Hello sont automatiquement injectés que vous créez des machines virtuelles supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="f2607-121">hello latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="f2607-122">Au cours de l’ensemble du processus hello, certificats hello jamais laisser hello plateforme Azure ou sont exposées dans un script, un historique de ligne de commande ou un modèle.</span><span class="sxs-lookup"><span data-stu-id="f2607-122">During hello whole process, hello certificates never leave hello Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="f2607-123">Créer un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="f2607-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="f2607-124">Avant de créer un coffre de clés et des certificats, créez un groupe de ressources avec [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f2607-124">Before you can create a Key Vault and certificates, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f2607-125">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroupSecureWeb* Bonjour *eastus* emplacement :</span><span class="sxs-lookup"><span data-stu-id="f2607-125">hello following example creates a resource group named *myResourceGroupSecureWeb* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

<span data-ttu-id="f2607-126">Ensuite, créez un coffre de clés avec la commande [az keyvault create](/cli/azure/keyvault#create) et activez son utilisation lors du déploiement d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2607-126">Next, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="f2607-127">Chaque Key Vault requiert un nom unique en minuscules.</span><span class="sxs-lookup"><span data-stu-id="f2607-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="f2607-128">Remplacez  *<mykeyvault>*  Bonjour votre propre nom de coffre de clés unique de l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="f2607-128">Replace *<mykeyvault>* in hello following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="f2607-129">Générer un certificat et le stocker dans Key Vault</span><span class="sxs-lookup"><span data-stu-id="f2607-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="f2607-130">Dans un environnement de production, vous devez importer un certificat valide signé par un fournisseur approuvé à l’aide de la commande [az keyvault certificate import](/cli/azure/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="f2607-130">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/certificate#import).</span></span> <span data-ttu-id="f2607-131">Pour ce didacticiel, hello suivant montre comment vous pouvez générer un certificat auto-signé avec [création de certificat de keyvault az](/cli/azure/certificate#create) qui utilise la stratégie de certificat par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="f2607-131">For this tutorial, hello following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/certificate#create) that uses hello default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a><span data-ttu-id="f2607-132">Préparer un certificat en vue de son utilisation avec une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f2607-132">Prepare a certificate for use with a VM</span></span>
<span data-ttu-id="f2607-133">certificat de hello de toouse pendant hello VM créer un processus, obtenir l’ID hello de votre certificat avec [az keyvault secrète liste versions](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="f2607-133">toouse hello certificate during hello VM create process, obtain hello ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="f2607-134">Convertir le certificat hello avec [az vm format-secret](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="f2607-134">Convert hello certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="f2607-135">Hello, l’exemple suivant attribue à sortie hello de toovariables de ces commandes pour faciliter l’utilisation Bonjour étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f2607-135">hello following example assigns hello output of these commands toovariables for ease of use in hello next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-toosecure-nginx"></a><span data-ttu-id="f2607-136">Créer un toosecure de configuration cloud-init NGINX</span><span class="sxs-lookup"><span data-stu-id="f2607-136">Create a cloud-init config toosecure NGINX</span></span>
<span data-ttu-id="f2607-137">[Init-cloud](https://cloudinit.readthedocs.io) est un toocustomize approche largement utilisée une VM Linux au démarrage pour hello première fois.</span><span class="sxs-lookup"><span data-stu-id="f2607-137">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach toocustomize a Linux VM as it boots for hello first time.</span></span> <span data-ttu-id="f2607-138">Vous pouvez utiliser des packages tooinstall init de cloud et écrire des fichiers, ou de tooconfigure utilisateurs et de sécurité.</span><span class="sxs-lookup"><span data-stu-id="f2607-138">You can use cloud-init tooinstall packages and write files, or tooconfigure users and security.</span></span> <span data-ttu-id="f2607-139">Comme le cloud-init s’exécute pendant le processus de démarrage initial hello, il n’existe aucune étape supplémentaire ou agents tooapply votre configuration.</span><span class="sxs-lookup"><span data-stu-id="f2607-139">As cloud-init runs during hello initial boot process, there are no additional steps or required agents tooapply your configuration.</span></span>

<span data-ttu-id="f2607-140">Lorsque vous créez une machine virtuelle, les certificats et clés sont stockées dans hello protégé */var/lib/waagent/* active.</span><span class="sxs-lookup"><span data-stu-id="f2607-140">When you create a VM, certificates and keys are stored in hello protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="f2607-141">l’ajout de tooautomate hello certificat toohello VM et configuration de serveur web de hello, utilisez init-cloud.</span><span class="sxs-lookup"><span data-stu-id="f2607-141">tooautomate adding hello certificate toohello VM and configuring hello web server, use cloud-init.</span></span> <span data-ttu-id="f2607-142">Dans cet exemple, nous installer et configurer le serveur de web NGINX hello.</span><span class="sxs-lookup"><span data-stu-id="f2607-142">In this example, we install and configure hello NGINX web server.</span></span> <span data-ttu-id="f2607-143">Vous pouvez utiliser hello même processus tooinstall et que vous configurez Apache.</span><span class="sxs-lookup"><span data-stu-id="f2607-143">You can use hello same process tooinstall and configure Apache.</span></span> 

<span data-ttu-id="f2607-144">Créez un fichier nommé *cloud-init-web-server.txt* et coller hello de configuration suivante :</span><span class="sxs-lookup"><span data-stu-id="f2607-144">Create a file named *cloud-init-web-server.txt* and paste hello following configuration:</span></span>

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

### <a name="create-a-secure-vm"></a><span data-ttu-id="f2607-145">Créer une machine virtuelle sécurisée</span><span class="sxs-lookup"><span data-stu-id="f2607-145">Create a secure VM</span></span>
<span data-ttu-id="f2607-146">Créez maintenant une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="f2607-146">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="f2607-147">les données de certificat Hello sont injectées dans le coffre de clés avec hello `--secrets` paramètre.</span><span class="sxs-lookup"><span data-stu-id="f2607-147">hello certificate data is injected from Key Vault with hello `--secrets` parameter.</span></span> <span data-ttu-id="f2607-148">Vous passez dans la configuration du cloud-init hello avec hello `--custom-data` paramètre :</span><span class="sxs-lookup"><span data-stu-id="f2607-148">You pass in hello cloud-init config with hello `--custom-data` parameter:</span></span>

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

<span data-ttu-id="f2607-149">Il prend quelques minutes pour hello toobe de machine virtuelle créée, hello packages tooinstall et toostart d’application hello.</span><span class="sxs-lookup"><span data-stu-id="f2607-149">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="f2607-150">Lorsque hello machine virtuelle a été créé, prenez note de hello `publicIpAddress` affiché par hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="f2607-150">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="f2607-151">Cette adresse est utilisée tooaccess votre site dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="f2607-151">This address is used tooaccess your site in a web browser.</span></span>

<span data-ttu-id="f2607-152">tooallow sécurisé tooreach du trafic web de votre machine virtuelle, ouvrir le port 443 à partir de hello Internet avec [ouvrir un ordinateur virtuel az-port](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="f2607-152">tooallow secure web traffic tooreach your VM, open port 443 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-hello-secure-web-app"></a><span data-ttu-id="f2607-153">Application de test hello web sécurisé</span><span class="sxs-lookup"><span data-stu-id="f2607-153">Test hello secure web app</span></span>
<span data-ttu-id="f2607-154">Vous pouvez désormais ouvrir un navigateur web et entrez *https://<publicIpAddress>*  dans la barre d’adresses hello.</span><span class="sxs-lookup"><span data-stu-id="f2607-154">Now you can open a web browser and enter *https://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="f2607-155">Fournissez vos propres adresse IP à partir de la machine virtuelle de hello créer le processus.</span><span class="sxs-lookup"><span data-stu-id="f2607-155">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="f2607-156">Acceptez l’avertissement de sécurité hello si vous avez utilisé un certificat auto-signé :</span><span class="sxs-lookup"><span data-stu-id="f2607-156">Accept hello security warning if you used a self-signed certificate:</span></span>

![Accepter l’avertissement de sécurité du navigateur web](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="f2607-158">Votre site NGINX sécurisé est ensuite affichée comme hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="f2607-158">Your secured NGINX site is then displayed as in hello following example:</span></span>

![Afficher le site NGINX sécurisé en cours d’exécution](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="f2607-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f2607-160">Next steps</span></span>

<span data-ttu-id="f2607-161">Dans ce didacticiel, vous avez sécurisé un serveur web NGINX à l’aide d’un certificat SSL stocké dans Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="f2607-161">In this tutorial, you secured an NGINX web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="f2607-162">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="f2607-162">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f2607-163">Créer un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="f2607-163">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="f2607-164">Générer ou télécharger un certificat de toohello le coffre de clés</span><span class="sxs-lookup"><span data-stu-id="f2607-164">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="f2607-165">Créer une machine virtuelle et installer le serveur web hello NGINX</span><span class="sxs-lookup"><span data-stu-id="f2607-165">Create a VM and install hello NGINX web server</span></span>
> * <span data-ttu-id="f2607-166">Injecter du certificat de hello dans hello machine virtuelle et configurer NGINX avec une liaison SSL</span><span class="sxs-lookup"><span data-stu-id="f2607-166">Inject hello certificate into hello VM and configure NGINX with an SSL binding</span></span>

<span data-ttu-id="f2607-167">Suivez cette toosee lien intégrées dans les exemples de scripts de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2607-167">Follow this link toosee pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f2607-168">Exemples de scripts de machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="f2607-168">Windows virtual machine script samples</span></span>](./cli-samples.md)