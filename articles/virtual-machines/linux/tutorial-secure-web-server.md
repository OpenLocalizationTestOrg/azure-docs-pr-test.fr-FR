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
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a>Sécuriser un serveur web à l’aide de certificats SSL sur une machine virtuelle Linux dans Azure
les serveurs web toosecure, un certificat ultérieurement SSL (Secure Sockets) peut être utilisé tooencrypt le trafic web. Ces certificats SSL peuvent être stockées dans le coffre de clés Azure et autoriser des déploiements sécurisés de certificats tooLinux virtual machines virtuelles dans Azure. Ce didacticiel vous explique comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Créer un Azure Key Vault
> * Générer ou télécharger un certificat de toohello le coffre de clés
> * Créer une machine virtuelle et installer le serveur web hello NGINX
> * Injecter du certificat de hello dans hello machine virtuelle et configurer NGINX avec une liaison SSL

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).  


## <a name="overview"></a>Vue d'ensemble
Azure Key Vault protège les clés de chiffrement et les secrets, tels que les certificats ou les mots de passe. Coffre de clés permet de rationaliser le processus de gestion des certificats hello et vous permet de contrôler toomaintain clés qui accèdent à ces certificats. Vous pouvez créer un certificat auto-signé à l’intérieur de Key Vault ou charger un certificat approuvé existant que vous avez déjà.

Au lieu d’utiliser une image de machine virtuelle personnalisée qui inclut des certificats intégrés, vous injectez des certificats dans une machine virtuelle en cours d’exécution. Ce processus garantit que les certificats hello plus récentes sont installés sur un serveur web pendant le déploiement. Si vous renouvelez ou remplacez un certificat, vous ne pouvez toocreate une nouvelle image de machine virtuelle personnalisée. certificats de dernière Hello sont automatiquement injectés que vous créez des machines virtuelles supplémentaires. Au cours de l’ensemble du processus hello, certificats hello jamais laisser hello plateforme Azure ou sont exposées dans un script, un historique de ligne de commande ou un modèle.


## <a name="create-an-azure-key-vault"></a>Créer un Azure Key Vault
Avant de créer un coffre de clés et des certificats, créez un groupe de ressources avec [az group create](/cli/azure/group#create). Hello exemple suivant crée un groupe de ressources nommé *myResourceGroupSecureWeb* Bonjour *eastus* emplacement :

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

Ensuite, créez un coffre de clés avec la commande [az keyvault create](/cli/azure/keyvault#create) et activez son utilisation lors du déploiement d’une machine virtuelle. Chaque Key Vault requiert un nom unique en minuscules. Remplacez  *<mykeyvault>*  Bonjour votre propre nom de coffre de clés unique de l’exemple suivant :

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a>Générer un certificat et le stocker dans Key Vault
Dans un environnement de production, vous devez importer un certificat valide signé par un fournisseur approuvé à l’aide de la commande [az keyvault certificate import](/cli/azure/certificate#import). Pour ce didacticiel, hello suivant montre comment vous pouvez générer un certificat auto-signé avec [création de certificat de keyvault az](/cli/azure/certificate#create) qui utilise la stratégie de certificat par défaut hello :

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a>Préparer un certificat en vue de son utilisation avec une machine virtuelle
certificat de hello de toouse pendant hello VM créer un processus, obtenir l’ID hello de votre certificat avec [az keyvault secrète liste versions](/cli/azure/keyvault/secret#list-versions). Convertir le certificat hello avec [az vm format-secret](/cli/azure/vm#format-secret). Hello, l’exemple suivant attribue à sortie hello de toovariables de ces commandes pour faciliter l’utilisation Bonjour étapes suivantes :

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-toosecure-nginx"></a>Créer un toosecure de configuration cloud-init NGINX
[Init-cloud](https://cloudinit.readthedocs.io) est un toocustomize approche largement utilisée une VM Linux au démarrage pour hello première fois. Vous pouvez utiliser des packages tooinstall init de cloud et écrire des fichiers, ou de tooconfigure utilisateurs et de sécurité. Comme le cloud-init s’exécute pendant le processus de démarrage initial hello, il n’existe aucune étape supplémentaire ou agents tooapply votre configuration.

Lorsque vous créez une machine virtuelle, les certificats et clés sont stockées dans hello protégé */var/lib/waagent/* active. l’ajout de tooautomate hello certificat toohello VM et configuration de serveur web de hello, utilisez init-cloud. Dans cet exemple, nous installer et configurer le serveur de web NGINX hello. Vous pouvez utiliser hello même processus tooinstall et que vous configurez Apache. 

Créez un fichier nommé *cloud-init-web-server.txt* et coller hello de configuration suivante :

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

### <a name="create-a-secure-vm"></a>Créer une machine virtuelle sécurisée
Créez maintenant une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create). les données de certificat Hello sont injectées dans le coffre de clés avec hello `--secrets` paramètre. Vous passez dans la configuration du cloud-init hello avec hello `--custom-data` paramètre :

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

Il prend quelques minutes pour hello toobe de machine virtuelle créée, hello packages tooinstall et toostart d’application hello. Lorsque hello machine virtuelle a été créé, prenez note de hello `publicIpAddress` affiché par hello CLI d’Azure. Cette adresse est utilisée tooaccess votre site dans un navigateur web.

tooallow sécurisé tooreach du trafic web de votre machine virtuelle, ouvrir le port 443 à partir de hello Internet avec [ouvrir un ordinateur virtuel az-port](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-hello-secure-web-app"></a>Application de test hello web sécurisé
Vous pouvez désormais ouvrir un navigateur web et entrez *https://<publicIpAddress>*  dans la barre d’adresses hello. Fournissez vos propres adresse IP à partir de la machine virtuelle de hello créer le processus. Acceptez l’avertissement de sécurité hello si vous avez utilisé un certificat auto-signé :

![Accepter l’avertissement de sécurité du navigateur web](./media/tutorial-secure-web-server/browser-warning.png)

Votre site NGINX sécurisé est ensuite affichée comme hello l’exemple suivant :

![Afficher le site NGINX sécurisé en cours d’exécution](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez sécurisé un serveur web NGINX à l’aide d’un certificat SSL stocké dans Azure Key Vault. Vous avez appris à effectuer les actions suivantes :

> [!div class="checklist"]
> * Créer un Azure Key Vault
> * Générer ou télécharger un certificat de toohello le coffre de clés
> * Créer une machine virtuelle et installer le serveur web hello NGINX
> * Injecter du certificat de hello dans hello machine virtuelle et configurer NGINX avec une liaison SSL

Suivez cette toosee lien intégrées dans les exemples de scripts de machine virtuelle.

> [!div class="nextstepaction"]
> [Exemples de scripts de machine virtuelle Windows](./cli-samples.md)