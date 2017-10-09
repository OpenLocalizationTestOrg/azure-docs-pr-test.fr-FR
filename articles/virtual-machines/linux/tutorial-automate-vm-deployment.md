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
# <a name="how-toocustomize-a-linux-virtual-machine-on-first-boot"></a>Comment toocustomize une machine virtuelle de Linux au premier démarrage
Dans un didacticiel précédent, vous avez appris comment tooSSH tooa virtual machine (VM) et installer manuellement les NGINX. toocreate machines virtuelles de manière rapide et cohérente, une forme d’automatisation est généralement souhaité. Un toocustomize approche commune une machine virtuelle au premier démarrage est toouse [cloud-init](https://cloudinit.readthedocs.io). Ce didacticiel vous explique comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Créer un fichier de configuration cloud-init
> * Créer une machine virtuelle utilisant un fichier cloud-init
> * Afficher une application en cours d’exécution de Node.js après hello que machine virtuelle est créée.
> * Utiliser des certificats de coffre de clés toosecurely magasin
> * Automatiser des déploiements sécurisés de NGINX avec cloud-init


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).  



## <a name="cloud-init-overview"></a>Présentation de cloud-init
[Init-cloud](https://cloudinit.readthedocs.io) est un toocustomize approche largement utilisée une VM Linux au démarrage pour hello première fois. Vous pouvez utiliser des packages tooinstall init de cloud et écrire des fichiers, ou de tooconfigure utilisateurs et de sécurité. Comme le cloud-init s’exécute pendant le processus de démarrage initial hello, il n’existe aucune étape supplémentaire ou agents tooapply votre configuration.

Cloud-init fonctionne aussi sur les différentes distributions. Par exemple, vous n’utilisez pas **apt-get install** ou **yum installer** tooinstall un package. Au lieu de cela, vous pouvez définir une liste de packages tooinstall. Init-cloud utilise automatiquement l’outil de gestion de package native de hello pour distribution hello que vous sélectionnez.

Nous sommes utilisation de nos partenaires tooget cloud-init inclus et utilisation dans des images hello qu’ils fournissent des tooAzure. Hello tableau suivant souligne hello actuel cloud-init disponibilité sur les images de plateforme Azure :

| Alias | Éditeur | Offer | SKU | Version |
|:--- |:--- |:--- |:--- |:--- |:--- |
| UbuntuLTS |Canonical |UbuntuServer |16.04-LTS |le plus récent |
| UbuntuLTS |Canonical |UbuntuServer |14.04.5-LTS |le plus récent |
| CoreOS |CoreOS |CoreOS |Stable |le plus récent |


## <a name="create-cloud-init-config-file"></a>Créer un fichier de configuration cloud-init
toosee cloud-init dans action, créez une machine virtuelle qui installe NGINX et exécute une application Node.js de « Hello World » simple. Hello configuration du cloud-init suivante installe les packages hello requis, crée une application Node.js, puis initialisez et démarre l’application hello.

Dans votre environnement actuel, créez un fichier nommé *cloud-init.txt* et coller hello de configuration suivante. Par exemple, créer le fichier de hello Bonjour Cloud Shell pas sur votre ordinateur local. Vous pouvez utiliser l’éditeur de votre choix. Entrez `sensible-editor cloud-init.txt` toocreate hello fichier et afficher la liste des éditeurs disponibles. Assurez-vous que ce fichier d’ensemble cloud-init hello est copié correctement, en particulier hello première ligne :

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

Pour plus d’informations sur les options de configuration de cloud-init, consultez les [exemples de configuration cloud-init](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).

## <a name="create-virtual-machine"></a>Create virtual machine
Pour pouvoir créer une machine virtuelle, vous devez créer un groupe de ressources avec la commande [az group create](/cli/azure/group#create). Hello exemple suivant crée un groupe de ressources nommé *myResourceGroupAutomate* Bonjour *eastus* emplacement :

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

Créez maintenant une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create). Hello d’utilisation `--custom-data` toopass de paramètre dans votre fichier de configuration cloud-init. Fournir hello chemin d’accès complet toohello *init.txt de cloud* configuration si vous avez enregistré le fichier de hello en dehors de votre répertoire de travail actuelle. Hello exemple suivant crée un ordinateur virtuel nommé *myAutomatedVM*:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

Il prend quelques minutes pour hello toobe de machine virtuelle créée, hello packages tooinstall et toostart d’application hello. Il existe des tâches en arrière-plan qui continuer toorun après que hello CLI d’Azure vous renvoie toohello invite. Il peut être une ou deux minutes avant que vous pouvez accéder à application hello. Lorsque hello machine virtuelle a été créé, prenez note de hello `publicIpAddress` affiché par hello CLI d’Azure. Cette adresse est utilisée tooaccess hello Node.js application via un navigateur web.

tooallow web tooreach de trafic de votre machine virtuelle, ouvrez port 80 du hello Internet avec [ouvrir un ordinateur virtuel az-port](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a>Tester l’application web
Vous pouvez désormais ouvrir un navigateur web et entrez *http://<publicIpAddress>*  dans la barre d’adresses hello. Fournissez vos propres adresse IP à partir de la machine virtuelle de hello créer le processus. Votre application Node.js s’affiche comme dans hello l’exemple suivant :

![Afficher le site NGINX en cours d’exécution](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a>Injecter des certificats à partir de Key Vault
Cette section montre comment vous pouvez stocker des certificats dans le coffre de clés Azure en toute sécurité et les injecter pendant hello déploiement des ordinateurs virtuels. Au lieu d’utiliser une image personnalisée qui inclut les certificats de hello cuit-in, ce processus garantit que les certificats hello plus récentes sont injectées tooa VM au premier démarrage. Pendant le processus de hello, certificat hello jamais laisse hello plateforme Azure ou est exposée dans un script, un historique de ligne de commande ou un modèle.

Azure Key Vault protège les clés de chiffrement et les secrets, tels que les certificats ou les mots de passe. Coffre de clés permet de rationaliser le processus de gestion de clés hello et vous permet de contrôler toomaintain clés d’accès et de chiffrer vos données. Ce scénario présente certains toocreate des concepts de coffre de clés et les utiliser un certificat, bien que n’est pas une vue d’ensemble exhaustive sur la façon de toouse le coffre de clés.

comment vous pouvez affiche les Hello comme suit :

- Créer un Azure Key Vault
- Générer ou télécharger un certificat de toohello le coffre de clés
- Créer une clé secrète à partir de tooinject de certificat hello dans tooa machine virtuelle
- Créer une machine virtuelle et injecter du certificat de hello

### <a name="create-an-azure-key-vault"></a>Créer un Azure Key Vault
Commencez par créer un Key Vault avec la commande [az keyvault create](/cli/azure/keyvault#create) et activez son utilisation lors du déploiement d’une machine virtuelle. Chaque Key Vault requiert un nom unique en minuscules. Remplacez *mykeyvault* Bonjour votre propre nom de coffre de clés unique de l’exemple suivant :

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a>Générer le certificat et le stocker dans Key Vault
Dans un environnement de production, vous devez importer un certificat valide signé par un fournisseur approuvé à l’aide de la commande [az keyvault certificate import](/cli/azure/keyvault/certificate#import). Pour ce didacticiel, hello suivant montre comment vous pouvez générer un certificat auto-signé avec [création de certificat de keyvault az](/cli/azure/keyvault/certificate#create) qui utilise la stratégie de certificat par défaut hello :

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a>Préparer le certificat en vue de son utilisation avec la machine virtuelle
certificat de hello de toouse pendant hello VM créer un processus, obtenir l’ID hello de votre certificat avec [az keyvault secrète liste versions](/cli/azure/keyvault/secret#list-versions). Hello machine virtuelle a besoin de certificat de hello dans une certaine tooinject format il au démarrage du système, par conséquent, convertir certificat hello avec [az vm format-secret](/cli/azure/vm#format-secret). Hello, l’exemple suivant attribue à sortie hello de toovariables de ces commandes pour faciliter l’utilisation Bonjour étapes suivantes :

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-toosecure-nginx"></a>Créer le nuage-init config toosecure NGINX
Lorsque vous créez une machine virtuelle, les certificats et clés sont stockées dans hello protégé */var/lib/waagent/* active. tooautomate Ajout hello certificat toohello machine virtuelle et la configuration NGINX, vous pouvez utiliser une configuration cloud-init mis à jour à partir de l’exemple précédent de hello.

Créez un fichier nommé *cloud-init-secured.txt* et coller hello de configuration suivante. Là encore, si vous utilisez hello Shell de cloud computing, vous devez créer le fichier de configuration cloud-init hello ici et pas sur votre ordinateur local. Utilisez `sensible-editor cloud-init-secured.txt` toocreate hello fichier et afficher la liste des éditeurs disponibles. Assurez-vous que ce fichier d’ensemble cloud-init hello est copié correctement, en particulier hello première ligne :

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

### <a name="create-secure-vm"></a>Créer une machine virtuelle sécurisée
Créez maintenant une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create). les données de certificat Hello sont injectées dans le coffre de clés avec hello `--secrets` paramètre. Comme exemple précédent de hello, vous passez également dans la configuration du cloud-init hello avec hello `--custom-data` paramètre :

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

Il prend quelques minutes pour hello toobe de machine virtuelle créée, hello packages tooinstall et toostart d’application hello. Il existe des tâches en arrière-plan qui continuer toorun après que hello CLI d’Azure vous renvoie toohello invite. Il peut être une ou deux minutes avant que vous pouvez accéder à application hello. Lorsque hello machine virtuelle a été créé, prenez note de hello `publicIpAddress` affiché par hello CLI d’Azure. Cette adresse est utilisée tooaccess hello Node.js application via un navigateur web.

tooallow sécurisé tooreach du trafic web de votre machine virtuelle, ouvrir le port 443 à partir de hello Internet avec [ouvrir un ordinateur virtuel az-port](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a>Tester l’application web sécurisée
Vous pouvez désormais ouvrir un navigateur web et entrez *https://<publicIpAddress>*  dans la barre d’adresses hello. Fournissez vos propres adresse IP à partir de la machine virtuelle de hello créer le processus. Acceptez l’avertissement de sécurité hello si vous avez utilisé un certificat auto-signé :

![Accepter l’avertissement de sécurité du navigateur web](./media/tutorial-automate-vm-deployment/browser-warning.png)

Votre site NGINX sécurisés et les Node.js application est ensuite affichée comme hello l’exemple suivant :

![Afficher le site NGINX sécurisé en cours d’exécution](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a>Étapes suivantes
Ce didacticiel vous a montré comment configurer des machines virtuelles au premier démarrage avec cloud-init. Vous avez appris à effectuer les actions suivantes :

> [!div class="checklist"]
> * Créer un fichier de configuration cloud-init
> * Créer une machine virtuelle utilisant un fichier cloud-init
> * Afficher une application en cours d’exécution de Node.js après hello que machine virtuelle est créée.
> * Utiliser des certificats de coffre de clés toosecurely magasin
> * Automatiser des déploiements sécurisés de NGINX avec cloud-init

Avancer toolearn de didacticiel suivant toohello comment toocreate les images de machine virtuelle personnalisées.

> [!div class="nextstepaction"]
> [Créer des images de machine virtuelle personnalisées](./tutorial-custom-images.md)
