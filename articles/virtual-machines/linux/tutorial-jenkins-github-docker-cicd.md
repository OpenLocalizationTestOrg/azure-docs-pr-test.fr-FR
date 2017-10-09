---
title: "aaaCreate un pipeline de développement dans Azure avec Jenkins | Documents Microsoft"
description: "Découvrez comment toocreate un Jenkins virtual machine dans Azure qu’extrait à partir de GitHub sur chaque code valider et génère une nouvelle Docker conteneur toorun votre application"
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
ms.date: 05/08/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c079e3c9186c9da0a3e51e1823215779c565e0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a>Comment toocreate une infrastructure de développement sur un VM Linux dans Azure avec Jenkins, GitHub et Docker
tooautomate hello build et tester la phase de développement d’applications, vous pouvez utiliser une intégration continue et le pipeline de déploiement de (l’élément de configuration/CD). Dans ce didacticiel, vous créez un pipeline CI/CD sur une machine virtuelle Azure et apprenez notamment comment :

> [!div class="checklist"]
> * Créer une machine virtuelle Jenkins
> * Installer et configurer Jenkins
> * Créer une intégration webhook entre GitHub et Jenkins
> * Créer et déclencher des tâches de génération Jenkins à partir de validations GitHub
> * Créer une image Docker pour votre application
> * Vérifier les validations GitHub, générer une nouvelle image Docker et mettre à jour l’application en cours d’exécution


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-jenkins-instance"></a>Création d’une instance Jenkins
Dans un didacticiel précédent sur [comment toocustomize une machine virtuelle de Linux au premier démarrage](tutorial-automate-vm-deployment.md), vous avez appris comment personnalisation tooautomate avec init-cloud. Ce didacticiel utilise un cloud-init fichier tooinstall Jenkins et le Docker sur un ordinateur virtuel. 

Dans votre environnement actuel, créez un fichier nommé *cloud-init.txt* et coller hello de configuration suivante. Par exemple, créer le fichier de hello Bonjour Cloud Shell pas sur votre ordinateur local. Entrez `sensible-editor cloud-init-jenkins.txt` toocreate hello fichier et afficher la liste des éditeurs disponibles. Assurez-vous que ce fichier d’ensemble cloud-init hello est copié correctement, en particulier hello première ligne :

```yaml
#cloud-config
package_upgrade: true
write_files:
  - path: /etc/systemd/system/docker.service.d/docker.conf
    content: |
      [Service]
        ExecStart=
        ExecStart=/usr/bin/dockerd
  - path: /etc/docker/daemon.json
    content: |
      {
        "hosts": ["fd://","tcp://127.0.0.1:2375"]
      }
runcmd:
  - wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
  - sh -c 'echo deb http://pkg.jenkins-ci.org/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
  - apt-get update && apt-get install jenkins -y
  - curl -sSL https://get.docker.com/ | sh
  - usermod -aG docker azureuser
  - usermod -aG docker jenkins
  - service jenkins restart
```

Pour pouvoir créer une machine virtuelle, vous devez créer un groupe de ressources avec la commande [az group create](/cli/azure/group#create). Hello exemple suivant crée un groupe de ressources nommé *myResourceGroupJenkins* Bonjour *eastus* emplacement :

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

Créez maintenant une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create). Hello d’utilisation `--custom-data` toopass de paramètre dans votre fichier de configuration cloud-init. Fournir le chemin d’accès complet de hello trop*cloud-init-jenkins.txt* si vous avez enregistré le fichier de hello en dehors de votre répertoire de travail actuelle.

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

Il prend quelques minutes pour hello toobe d’ordinateur virtuel créé et configuré.

tooallow web tooreach de trafic de votre machine virtuelle, utilisez [ouvrir un ordinateur virtuel az-port](/cli/azure/vm#open-port) tooopen port *8080* pour le trafic de Jenkins et le port *1337* pour application Node.js hello toorun utilisé un exemple d’application :

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a>Configurer Jenkins
tooaccess votre Jenkins d’une instance, obtenir hello une adresse IP publique de votre machine virtuelle :

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

Pour des raisons de sécurité, vous devez tooenter hello administration initiale mot de passe est stocké dans un fichier texte sur votre hello toostart de machine virtuelle que Jenkins installer. Utilisez l’adresse IP publique hello obtenu dans hello précédente étape tooSSH tooyour machine virtuelle :

```bash
ssh azureuser@<publicIps>
```

Hello de vue `initialAdminPassword` pour installer votre Jenkins et le copier :

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Si le fichier de hello n’est encore disponible, attendez quelques minutes pour cloud-init toocomplete hello Jenkins et installation de Docker.

Ouvrez un navigateur web et accédez trop`http://<publicIps>:8080`. Terminer la configuration initiale de Jenkins hello comme suit :

- Entrez hello *initialAdminPassword* obtenues à partir de hello machine virtuelle à l’étape précédente de hello.
- Cliquez sur **sélectionnez tooinstall de plug-ins**
- Recherchez *GitHub* dans la zone de texte hello haut hello, sélectionnez hello *plug-in GitHub*, puis cliquez sur **installer**
- toocreate un compte d’utilisateur Jenkins, complétez hello comme vous le souhaitez. Du point de vue de la sécurité, vous devez créer ce premier utilisateur Jenkins, plutôt que de se poursuivre en tant que compte d’administrateur par défaut hello.
- Une fois terminé, cliquez sur **Commencer à utiliser Jenkins**


## <a name="create-github-webhook"></a>Créer un webhook GitHub
intégration de hello tooconfigure à GitHub, ouvrez hello [Node.js Hello World, exemple d’application](https://github.com/Azure-Samples/nodejs-docs-hello-world) à partir du référentiel d’exemples Azure hello. toofork hello référentiel tooyour propre compte GitHub, cliquez sur hello **branchement** bouton dans le coin supérieur droit de hello.

Créer un webhook à l’intérieur de branchement hello vous avez créé :

- Cliquez sur **paramètres**, puis sélectionnez **intégrations & services** sur le côté gauche de hello.
- Cliquez sur **Ajouter un service**, puis entrez *Jenkins* dans la zone de filtre.
- Sélectionnez *Jenkins (plug-in GitHub)*
- Pourquoi **Jenkins raccorder URL**, entrez `http://<publicIps>:8080/github-webhook/`. Veillez à inclure à la fin hello /
- Cliquez sur **Ajouter un service**

![Ajoutez le référentiel GitHub de webhook tooyour dupliquée](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a>Créer une tâche Jenkins
toohave Jenkins tooan événement respond dans GitHub telles que la validation du code, créez un travail de Jenkins. 

Dans votre site Web de Jenkins, cliquez sur **créer de nouveaux travaux** à partir de la page d’accueil hello :

- Entrez *HelloWorld* comme nom de la tâche. Sélectionnez **Projet libre**, puis cliquez sur **OK**.
- Sous hello **général** section, sélectionnez **GitHub** de projet et entrez votre URL de référentiel RAMIFIÉ, tel que *https://github.com/iainfoulds/nodejs-docs-hello-world*
- Sous hello **de Source de la gestion du code** section, sélectionnez **Git**, entrez votre dépôt RAMIFIÉ *.git* URL, tel que *https://github.com/iainfoulds/nodejs-docs-hello-world.git*
- Sous hello **déclencheurs de Build** section, sélectionnez **déclencheur du hook GitHub pour l’interrogation de GITscm**.
- Sous hello **générer** , choisissez **étape de génération ajouter**. Sélectionnez **exécuter shell**, puis entrez `echo "Testing"` dans la fenêtre de toocommand.
- Cliquez sur **enregistrer** bas hello de la fenêtre des tâches hello.


## <a name="test-github-integration"></a>Test de l’intégration de GitHub
tootest hello intégration de GitHub à Jenkins, validez une modification dans votre branche. 

Dans GitHub de l’interface utilisateur web, sélectionnez votre dépôt RAMIFIÉ, puis cliquez sur hello **index.js** fichier. Cliquez sur hello crayon icône tooedit ce fichier afin que la ligne 6 affiche :

```nodejs
response.end("Hello World!");
```

toocommit vos modifications, cliquez sur hello **valider les modifications** bouton bas hello.

Dans Jenkins, une nouvelle build démarre sous hello **générer l’historique** section de hello en bas à gauche de la page de votre travail. Cliquez sur le lien du numéro de build hello et sélectionnez **sortie de Console** sur la taille de gauche hello. Vous pouvez afficher les étapes de hello Jenkins prend comme votre code est extraite à partir de GitHub et hello build action sorties message de type hello `Testing` toohello console. Chaque fois qu’une validation est effectuée dans GitHub, hello webhook contacte tooJenkins et déclencher une nouvelle build de cette façon.


## <a name="define-docker-build-image"></a>Définir l’image de génération Docker
toosee hello Node.js application est en cours d’exécution en fonction de vos validations GitHub, vous permet de générer une Docker image toorun hello application. image de Hello est construit à partir d’un fichier Dockerfile qui définit comment tooconfigure hello conteneur qui exécute l’application hello. 

À partir de tooyour de connexion SSH hello VM, basculez toohello Jenkins espace de travail nommé d’après la tâche hello que vous avez créé à l’étape précédente. Dans notre exemple, il était nommé *HelloWorld*.

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

Créer un fichier dans ce répertoire de l’espace de travail avec `sudo sensible-editor Dockerfile` et coller hello suivant le contenu. Vérifiez que hello que dockerfile entier est copié correctement, en particulier hello première ligne :

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

Ce fichier Dockerfile utilise image Node.js base hello utilisant Linux Alpine, port expose 1337 hello application Hello World s’exécute sur, puis copie les fichiers de l’application hello et l’initialise.


## <a name="create-jenkins-build-rules"></a>Créer des règles de génération Jenkins
À l’étape précédente, vous avez créé une règle de build Jenkins base une console toohello de message de sortie. Permet de créer hello build étape toouse notre fichier Dockerfile et exécuter l’application hello.

Dans votre instance de Jenkins, sélectionnez la tâche hello que vous avez créé à l’étape précédente. Cliquez sur **configurer** sur le côté gauche de hello et faites défiler toohello **générer** section :

- Supprimez votre étape de génération `echo "Test"` existante. Cliquez sur hello rouge croisée sur hello coin supérieur droit de zone étape build existante de hello.
- Cliquez sur **Ajouter une étape de génération**, puis sélectionnez **Exécuter l’interpréteur de commandes**
- Bonjour **commande** zone, entrez hello suivant des commandes Docker, puis sélectionnez **enregistrer**:

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

étapes de génération Docker Hello créent une image et une balise avec hello Jenkins numéro de build afin de l’historique des images. Tous les conteneurs existants en cours d’exécution application hello sont arrêtés et supprimés. Un conteneur est démarré à l’aide d’image de hello et exécute votre application Node.js selon les validations de dernière hello dans GitHub.


## <a name="test-your-pipeline"></a>Tester votre pipeline
pipeline de toute hello toosee dans action, modifier hello *index.js* dans votre référentiel GitHub RAMIFIÉ à nouveau, cliquez sur **de valider la modification**. Un nouveau travail démarre dans Jenkins selon hello webhook pour GitHub. Il prend quelques secondes image de Docker toocreate hello et que vous démarrez votre application dans un nouveau conteneur.

Si nécessaire, obtenir à nouveau hello adresse IP publique de votre machine virtuelle :

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

Ouvrez un navigateur web et entrez `http://<publicIps>:1337`. Votre application Node.js s’affiche et reflète les validations de dernière hello dans votre branche GitHub comme suit :

![Exécution de l’application Node.js](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

Maintenant faire une autre édition toohello *index.js* fichier changement de hello GitHub et la validation. Attendez quelques secondes pour toocomplete de travail hello dans Jenkins, puis actualiser votre version hello mis à jour toosee du navigateur web de votre application dans un nouveau conteneur comme suit :

![Exécution de l’application Node.js après une autre validation GitHub](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous configuré GitHub toorun un travail de build Jenkins lors de la validation de chaque code et ensuite déployez un tootest de conteneur Docker de votre application. Vous avez appris à effectuer les actions suivantes :

> [!div class="checklist"]
> * Créer une machine virtuelle Jenkins
> * Installer et configurer Jenkins
> * Créer une intégration webhook entre GitHub et Jenkins
> * Créer et déclencher des tâches de génération Jenkins à partir de validations GitHub
> * Créer une image Docker pour votre application
> * Vérifier les validations GitHub, générer une nouvelle image Docker et mettre à jour l’application en cours d’exécution

Avancer toolearn de didacticiel suivant toohello plus d’informations sur la façon toointegrate Jenkins avec Visual Studio Team Services.

> [!div class="nextstepaction"]
> [Déployer des applications avec Jenkins et Team Services](tutorial-build-deploy-jenkins.md)