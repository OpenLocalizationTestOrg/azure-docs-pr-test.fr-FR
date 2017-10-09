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
# <a name="how-toocreate-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a><span data-ttu-id="62933-103">Comment toocreate une infrastructure de développement sur un VM Linux dans Azure avec Jenkins, GitHub et Docker</span><span class="sxs-lookup"><span data-stu-id="62933-103">How toocreate a development infrastructure on a Linux VM in Azure with Jenkins, GitHub, and Docker</span></span>
<span data-ttu-id="62933-104">tooautomate hello build et tester la phase de développement d’applications, vous pouvez utiliser une intégration continue et le pipeline de déploiement de (l’élément de configuration/CD).</span><span class="sxs-lookup"><span data-stu-id="62933-104">tooautomate hello build and test phase of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="62933-105">Dans ce didacticiel, vous créez un pipeline CI/CD sur une machine virtuelle Azure et apprenez notamment comment :</span><span class="sxs-lookup"><span data-stu-id="62933-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="62933-106">Créer une machine virtuelle Jenkins</span><span class="sxs-lookup"><span data-stu-id="62933-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="62933-107">Installer et configurer Jenkins</span><span class="sxs-lookup"><span data-stu-id="62933-107">Install and configure Jenkins</span></span>
> * <span data-ttu-id="62933-108">Créer une intégration webhook entre GitHub et Jenkins</span><span class="sxs-lookup"><span data-stu-id="62933-108">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="62933-109">Créer et déclencher des tâches de génération Jenkins à partir de validations GitHub</span><span class="sxs-lookup"><span data-stu-id="62933-109">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="62933-110">Créer une image Docker pour votre application</span><span class="sxs-lookup"><span data-stu-id="62933-110">Create a Docker image for your app</span></span>
> * <span data-ttu-id="62933-111">Vérifier les validations GitHub, générer une nouvelle image Docker et mettre à jour l’application en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="62933-111">Verify GitHub commits build new Docker image and updates running app</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="62933-112">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="62933-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="62933-113">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="62933-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="62933-114">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="62933-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-jenkins-instance"></a><span data-ttu-id="62933-115">Création d’une instance Jenkins</span><span class="sxs-lookup"><span data-stu-id="62933-115">Create Jenkins instance</span></span>
<span data-ttu-id="62933-116">Dans un didacticiel précédent sur [comment toocustomize une machine virtuelle de Linux au premier démarrage](tutorial-automate-vm-deployment.md), vous avez appris comment personnalisation tooautomate avec init-cloud.</span><span class="sxs-lookup"><span data-stu-id="62933-116">In a previous tutorial on [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with cloud-init.</span></span> <span data-ttu-id="62933-117">Ce didacticiel utilise un cloud-init fichier tooinstall Jenkins et le Docker sur un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="62933-117">This tutorial uses a cloud-init file tooinstall Jenkins and Docker on a VM.</span></span> 

<span data-ttu-id="62933-118">Dans votre environnement actuel, créez un fichier nommé *cloud-init.txt* et coller hello de configuration suivante.</span><span class="sxs-lookup"><span data-stu-id="62933-118">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="62933-119">Par exemple, créer le fichier de hello Bonjour Cloud Shell pas sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="62933-119">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="62933-120">Entrez `sensible-editor cloud-init-jenkins.txt` toocreate hello fichier et afficher la liste des éditeurs disponibles.</span><span class="sxs-lookup"><span data-stu-id="62933-120">Enter `sensible-editor cloud-init-jenkins.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="62933-121">Assurez-vous que ce fichier d’ensemble cloud-init hello est copié correctement, en particulier hello première ligne :</span><span class="sxs-lookup"><span data-stu-id="62933-121">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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

<span data-ttu-id="62933-122">Pour pouvoir créer une machine virtuelle, vous devez créer un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="62933-122">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="62933-123">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroupJenkins* Bonjour *eastus* emplacement :</span><span class="sxs-lookup"><span data-stu-id="62933-123">hello following example creates a resource group named *myResourceGroupJenkins* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

<span data-ttu-id="62933-124">Créez maintenant une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="62933-124">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="62933-125">Hello d’utilisation `--custom-data` toopass de paramètre dans votre fichier de configuration cloud-init.</span><span class="sxs-lookup"><span data-stu-id="62933-125">Use hello `--custom-data` parameter toopass in your cloud-init config file.</span></span> <span data-ttu-id="62933-126">Fournir le chemin d’accès complet de hello trop*cloud-init-jenkins.txt* si vous avez enregistré le fichier de hello en dehors de votre répertoire de travail actuelle.</span><span class="sxs-lookup"><span data-stu-id="62933-126">Provide hello full path too*cloud-init-jenkins.txt* if you saved hello file outside of your present working directory.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

<span data-ttu-id="62933-127">Il prend quelques minutes pour hello toobe d’ordinateur virtuel créé et configuré.</span><span class="sxs-lookup"><span data-stu-id="62933-127">It takes a few minutes for hello VM toobe created and configured.</span></span>

<span data-ttu-id="62933-128">tooallow web tooreach de trafic de votre machine virtuelle, utilisez [ouvrir un ordinateur virtuel az-port](/cli/azure/vm#open-port) tooopen port *8080* pour le trafic de Jenkins et le port *1337* pour application Node.js hello toorun utilisé un exemple d’application :</span><span class="sxs-lookup"><span data-stu-id="62933-128">tooallow web traffic tooreach your VM, use [az vm open-port](/cli/azure/vm#open-port) tooopen port *8080* for Jenkins traffic and port *1337* for hello Node.js app that is used toorun a sample app:</span></span>

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a><span data-ttu-id="62933-129">Configurer Jenkins</span><span class="sxs-lookup"><span data-stu-id="62933-129">Configure Jenkins</span></span>
<span data-ttu-id="62933-130">tooaccess votre Jenkins d’une instance, obtenir hello une adresse IP publique de votre machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="62933-130">tooaccess your Jenkins instance, obtain hello public IP address of your VM:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="62933-131">Pour des raisons de sécurité, vous devez tooenter hello administration initiale mot de passe est stocké dans un fichier texte sur votre hello toostart de machine virtuelle que Jenkins installer.</span><span class="sxs-lookup"><span data-stu-id="62933-131">For security purposes, you need tooenter hello initial admin password that is stored in a text file on your VM toostart hello Jenkins install.</span></span> <span data-ttu-id="62933-132">Utilisez l’adresse IP publique hello obtenu dans hello précédente étape tooSSH tooyour machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="62933-132">Use hello public IP address obtained in hello previous step tooSSH tooyour VM:</span></span>

```bash
ssh azureuser@<publicIps>
```

<span data-ttu-id="62933-133">Hello de vue `initialAdminPassword` pour installer votre Jenkins et le copier :</span><span class="sxs-lookup"><span data-stu-id="62933-133">View hello `initialAdminPassword` for your Jenkins install and copy it:</span></span>

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

<span data-ttu-id="62933-134">Si le fichier de hello n’est encore disponible, attendez quelques minutes pour cloud-init toocomplete hello Jenkins et installation de Docker.</span><span class="sxs-lookup"><span data-stu-id="62933-134">If hello file isn't available yet, wait a couple more minutes for cloud-init toocomplete hello Jenkins and Docker install.</span></span>

<span data-ttu-id="62933-135">Ouvrez un navigateur web et accédez trop`http://<publicIps>:8080`.</span><span class="sxs-lookup"><span data-stu-id="62933-135">Now open a web browser and go too`http://<publicIps>:8080`.</span></span> <span data-ttu-id="62933-136">Terminer la configuration initiale de Jenkins hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="62933-136">Complete hello initial Jenkins setup as follows:</span></span>

- <span data-ttu-id="62933-137">Entrez hello *initialAdminPassword* obtenues à partir de hello machine virtuelle à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="62933-137">Enter hello *initialAdminPassword* obtained from hello VM in hello previous step.</span></span>
- <span data-ttu-id="62933-138">Cliquez sur **sélectionnez tooinstall de plug-ins**</span><span class="sxs-lookup"><span data-stu-id="62933-138">Click **Select plugins tooinstall**</span></span>
- <span data-ttu-id="62933-139">Recherchez *GitHub* dans la zone de texte hello haut hello, sélectionnez hello *plug-in GitHub*, puis cliquez sur **installer**</span><span class="sxs-lookup"><span data-stu-id="62933-139">Search for *GitHub* in hello text box across hello top, select hello *GitHub plugin*, then click **Install**</span></span>
- <span data-ttu-id="62933-140">toocreate un compte d’utilisateur Jenkins, complétez hello comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="62933-140">toocreate a Jenkins user account, fill out hello form as desired.</span></span> <span data-ttu-id="62933-141">Du point de vue de la sécurité, vous devez créer ce premier utilisateur Jenkins, plutôt que de se poursuivre en tant que compte d’administrateur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="62933-141">From a security perspective, you should create this first Jenkins user rather than continuing as hello default admin account.</span></span>
- <span data-ttu-id="62933-142">Une fois terminé, cliquez sur **Commencer à utiliser Jenkins**</span><span class="sxs-lookup"><span data-stu-id="62933-142">When finished, click **Start using Jenkins**</span></span>


## <a name="create-github-webhook"></a><span data-ttu-id="62933-143">Créer un webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="62933-143">Create GitHub webhook</span></span>
<span data-ttu-id="62933-144">intégration de hello tooconfigure à GitHub, ouvrez hello [Node.js Hello World, exemple d’application](https://github.com/Azure-Samples/nodejs-docs-hello-world) à partir du référentiel d’exemples Azure hello.</span><span class="sxs-lookup"><span data-stu-id="62933-144">tooconfigure hello integration with GitHub, open hello [Node.js Hello World sample app](https://github.com/Azure-Samples/nodejs-docs-hello-world) from hello Azure samples repo.</span></span> <span data-ttu-id="62933-145">toofork hello référentiel tooyour propre compte GitHub, cliquez sur hello **branchement** bouton dans le coin supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="62933-145">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>

<span data-ttu-id="62933-146">Créer un webhook à l’intérieur de branchement hello vous avez créé :</span><span class="sxs-lookup"><span data-stu-id="62933-146">Create a webhook inside hello fork you created:</span></span>

- <span data-ttu-id="62933-147">Cliquez sur **paramètres**, puis sélectionnez **intégrations & services** sur le côté gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="62933-147">Click **Settings**, then select **Integrations & services** on hello left-hand side.</span></span>
- <span data-ttu-id="62933-148">Cliquez sur **Ajouter un service**, puis entrez *Jenkins* dans la zone de filtre.</span><span class="sxs-lookup"><span data-stu-id="62933-148">Click **Add service**, then enter *Jenkins* in filter box.</span></span>
- <span data-ttu-id="62933-149">Sélectionnez *Jenkins (plug-in GitHub)*</span><span class="sxs-lookup"><span data-stu-id="62933-149">Select *Jenkins (GitHub plugin)*</span></span>
- <span data-ttu-id="62933-150">Pourquoi **Jenkins raccorder URL**, entrez `http://<publicIps>:8080/github-webhook/`.</span><span class="sxs-lookup"><span data-stu-id="62933-150">For hello **Jenkins hook URL**, enter `http://<publicIps>:8080/github-webhook/`.</span></span> <span data-ttu-id="62933-151">Veillez à inclure à la fin hello /</span><span class="sxs-lookup"><span data-stu-id="62933-151">Make sure you include hello trailing /</span></span>
- <span data-ttu-id="62933-152">Cliquez sur **Ajouter un service**</span><span class="sxs-lookup"><span data-stu-id="62933-152">Click **Add service**</span></span>

![Ajoutez le référentiel GitHub de webhook tooyour dupliquée](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a><span data-ttu-id="62933-154">Créer une tâche Jenkins</span><span class="sxs-lookup"><span data-stu-id="62933-154">Create Jenkins job</span></span>
<span data-ttu-id="62933-155">toohave Jenkins tooan événement respond dans GitHub telles que la validation du code, créez un travail de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="62933-155">toohave Jenkins respond tooan event in GitHub such as committing code, create a Jenkins job.</span></span> 

<span data-ttu-id="62933-156">Dans votre site Web de Jenkins, cliquez sur **créer de nouveaux travaux** à partir de la page d’accueil hello :</span><span class="sxs-lookup"><span data-stu-id="62933-156">In your Jenkins website, click **Create new jobs** from hello home page:</span></span>

- <span data-ttu-id="62933-157">Entrez *HelloWorld* comme nom de la tâche.</span><span class="sxs-lookup"><span data-stu-id="62933-157">Enter *HelloWorld* as job name.</span></span> <span data-ttu-id="62933-158">Sélectionnez **Projet libre**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="62933-158">Choose **Freestyle project**, then select **OK**.</span></span>
- <span data-ttu-id="62933-159">Sous hello **général** section, sélectionnez **GitHub** de projet et entrez votre URL de référentiel RAMIFIÉ, tel que *https://github.com/iainfoulds/nodejs-docs-hello-world*</span><span class="sxs-lookup"><span data-stu-id="62933-159">Under hello **General** section, select **GitHub** project and enter your forked repo URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world*</span></span>
- <span data-ttu-id="62933-160">Sous hello **de Source de la gestion du code** section, sélectionnez **Git**, entrez votre dépôt RAMIFIÉ *.git* URL, tel que *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span><span class="sxs-lookup"><span data-stu-id="62933-160">Under hello **Source code management** section, select **Git**, enter your forked repo *.git* URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span></span>
- <span data-ttu-id="62933-161">Sous hello **déclencheurs de Build** section, sélectionnez **déclencheur du hook GitHub pour l’interrogation de GITscm**.</span><span class="sxs-lookup"><span data-stu-id="62933-161">Under hello **Build Triggers** section, select **GitHub hook trigger for GITscm polling**.</span></span>
- <span data-ttu-id="62933-162">Sous hello **générer** , choisissez **étape de génération ajouter**.</span><span class="sxs-lookup"><span data-stu-id="62933-162">Under hello **Build** section, choose **Add build step**.</span></span> <span data-ttu-id="62933-163">Sélectionnez **exécuter shell**, puis entrez `echo "Testing"` dans la fenêtre de toocommand.</span><span class="sxs-lookup"><span data-stu-id="62933-163">Select **Execute shell**, then enter `echo "Testing"` in toocommand window.</span></span>
- <span data-ttu-id="62933-164">Cliquez sur **enregistrer** bas hello de la fenêtre des tâches hello.</span><span class="sxs-lookup"><span data-stu-id="62933-164">Click **Save** at hello bottom of hello jobs window.</span></span>


## <a name="test-github-integration"></a><span data-ttu-id="62933-165">Test de l’intégration de GitHub</span><span class="sxs-lookup"><span data-stu-id="62933-165">Test GitHub integration</span></span>
<span data-ttu-id="62933-166">tootest hello intégration de GitHub à Jenkins, validez une modification dans votre branche.</span><span class="sxs-lookup"><span data-stu-id="62933-166">tootest hello GitHub integration with Jenkins, commit a change in your fork.</span></span> 

<span data-ttu-id="62933-167">Dans GitHub de l’interface utilisateur web, sélectionnez votre dépôt RAMIFIÉ, puis cliquez sur hello **index.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="62933-167">Back in GitHub web UI, select your forked repo, and then click hello **index.js** file.</span></span> <span data-ttu-id="62933-168">Cliquez sur hello crayon icône tooedit ce fichier afin que la ligne 6 affiche :</span><span class="sxs-lookup"><span data-stu-id="62933-168">Click hello pencil icon tooedit this file so line 6 reads:</span></span>

```nodejs
response.end("Hello World!");
```

<span data-ttu-id="62933-169">toocommit vos modifications, cliquez sur hello **valider les modifications** bouton bas hello.</span><span class="sxs-lookup"><span data-stu-id="62933-169">toocommit your changes, click hello **Commit changes** button at hello bottom.</span></span>

<span data-ttu-id="62933-170">Dans Jenkins, une nouvelle build démarre sous hello **générer l’historique** section de hello en bas à gauche de la page de votre travail.</span><span class="sxs-lookup"><span data-stu-id="62933-170">In Jenkins, a new build starts under hello **Build history** section of hello bottom left-hand corner of your job page.</span></span> <span data-ttu-id="62933-171">Cliquez sur le lien du numéro de build hello et sélectionnez **sortie de Console** sur la taille de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="62933-171">Click hello build number link and select **Console output** on hello left-hand size.</span></span> <span data-ttu-id="62933-172">Vous pouvez afficher les étapes de hello Jenkins prend comme votre code est extraite à partir de GitHub et hello build action sorties message de type hello `Testing` toohello console.</span><span class="sxs-lookup"><span data-stu-id="62933-172">You can view hello steps Jenkins takes as your code is pulled from GitHub and hello build action outputs hello message `Testing` toohello console.</span></span> <span data-ttu-id="62933-173">Chaque fois qu’une validation est effectuée dans GitHub, hello webhook contacte tooJenkins et déclencher une nouvelle build de cette façon.</span><span class="sxs-lookup"><span data-stu-id="62933-173">Each time a commit is made in GitHub, hello webhook reaches out tooJenkins and trigger a new build in this way.</span></span>


## <a name="define-docker-build-image"></a><span data-ttu-id="62933-174">Définir l’image de génération Docker</span><span class="sxs-lookup"><span data-stu-id="62933-174">Define Docker build image</span></span>
<span data-ttu-id="62933-175">toosee hello Node.js application est en cours d’exécution en fonction de vos validations GitHub, vous permet de générer une Docker image toorun hello application.</span><span class="sxs-lookup"><span data-stu-id="62933-175">toosee hello Node.js app running based on your GitHub commits, lets build a Docker image toorun hello app.</span></span> <span data-ttu-id="62933-176">image de Hello est construit à partir d’un fichier Dockerfile qui définit comment tooconfigure hello conteneur qui exécute l’application hello.</span><span class="sxs-lookup"><span data-stu-id="62933-176">hello image is built from a Dockerfile that defines how tooconfigure hello container that runs hello app.</span></span> 

<span data-ttu-id="62933-177">À partir de tooyour de connexion SSH hello VM, basculez toohello Jenkins espace de travail nommé d’après la tâche hello que vous avez créé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="62933-177">From hello SSH connection tooyour VM, change toohello Jenkins workspace directory named after hello job you created in a previous step.</span></span> <span data-ttu-id="62933-178">Dans notre exemple, il était nommé *HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="62933-178">In our example, that was named *HelloWorld*.</span></span>

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

<span data-ttu-id="62933-179">Créer un fichier dans ce répertoire de l’espace de travail avec `sudo sensible-editor Dockerfile` et coller hello suivant le contenu.</span><span class="sxs-lookup"><span data-stu-id="62933-179">Create a file with in this workspace directory with `sudo sensible-editor Dockerfile` and paste hello following contents.</span></span> <span data-ttu-id="62933-180">Vérifiez que hello que dockerfile entier est copié correctement, en particulier hello première ligne :</span><span class="sxs-lookup"><span data-stu-id="62933-180">Make sure that hello whole Dockerfile is copied correctly, especially hello first line:</span></span>

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

<span data-ttu-id="62933-181">Ce fichier Dockerfile utilise image Node.js base hello utilisant Linux Alpine, port expose 1337 hello application Hello World s’exécute sur, puis copie les fichiers de l’application hello et l’initialise.</span><span class="sxs-lookup"><span data-stu-id="62933-181">This Dockerfile uses hello base Node.js image using Alpine Linux, exposes port 1337 that hello Hello World app runs on, then copies hello app files and initializes it.</span></span>


## <a name="create-jenkins-build-rules"></a><span data-ttu-id="62933-182">Créer des règles de génération Jenkins</span><span class="sxs-lookup"><span data-stu-id="62933-182">Create Jenkins build rules</span></span>
<span data-ttu-id="62933-183">À l’étape précédente, vous avez créé une règle de build Jenkins base une console toohello de message de sortie.</span><span class="sxs-lookup"><span data-stu-id="62933-183">In a previous step, you created a basic Jenkins build rule that output a message toohello console.</span></span> <span data-ttu-id="62933-184">Permet de créer hello build étape toouse notre fichier Dockerfile et exécuter l’application hello.</span><span class="sxs-lookup"><span data-stu-id="62933-184">Lets create hello build step toouse our Dockerfile and run hello app.</span></span>

<span data-ttu-id="62933-185">Dans votre instance de Jenkins, sélectionnez la tâche hello que vous avez créé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="62933-185">Back in your Jenkins instance, select hello job you created in a previous step.</span></span> <span data-ttu-id="62933-186">Cliquez sur **configurer** sur le côté gauche de hello et faites défiler toohello **générer** section :</span><span class="sxs-lookup"><span data-stu-id="62933-186">Click **Configure** on hello left-hand side and scroll down toohello **Build** section:</span></span>

- <span data-ttu-id="62933-187">Supprimez votre étape de génération `echo "Test"` existante.</span><span class="sxs-lookup"><span data-stu-id="62933-187">Remove your existing `echo "Test"` build step.</span></span> <span data-ttu-id="62933-188">Cliquez sur hello rouge croisée sur hello coin supérieur droit de zone étape build existante de hello.</span><span class="sxs-lookup"><span data-stu-id="62933-188">Click hello red cross on hello top right-hand corner of hello existing build step box.</span></span>
- <span data-ttu-id="62933-189">Cliquez sur **Ajouter une étape de génération**, puis sélectionnez **Exécuter l’interpréteur de commandes**</span><span class="sxs-lookup"><span data-stu-id="62933-189">Click **Add build step**, then select **Execute shell**</span></span>
- <span data-ttu-id="62933-190">Bonjour **commande** zone, entrez hello suivant des commandes Docker, puis sélectionnez **enregistrer**:</span><span class="sxs-lookup"><span data-stu-id="62933-190">In hello **Command** box, enter hello following Docker commands, then select **Save**:</span></span>

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

<span data-ttu-id="62933-191">étapes de génération Docker Hello créent une image et une balise avec hello Jenkins numéro de build afin de l’historique des images.</span><span class="sxs-lookup"><span data-stu-id="62933-191">hello Docker build steps create an image and tag it with hello Jenkins build number so you can maintain a history of images.</span></span> <span data-ttu-id="62933-192">Tous les conteneurs existants en cours d’exécution application hello sont arrêtés et supprimés.</span><span class="sxs-lookup"><span data-stu-id="62933-192">Any existing containers running hello app are stopped and then removed.</span></span> <span data-ttu-id="62933-193">Un conteneur est démarré à l’aide d’image de hello et exécute votre application Node.js selon les validations de dernière hello dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="62933-193">A new container is then started using hello image and runs your Node.js app based on hello latest commits in GitHub.</span></span>


## <a name="test-your-pipeline"></a><span data-ttu-id="62933-194">Tester votre pipeline</span><span class="sxs-lookup"><span data-stu-id="62933-194">Test your pipeline</span></span>
<span data-ttu-id="62933-195">pipeline de toute hello toosee dans action, modifier hello *index.js* dans votre référentiel GitHub RAMIFIÉ à nouveau, cliquez sur **de valider la modification**.</span><span class="sxs-lookup"><span data-stu-id="62933-195">toosee hello whole pipeline in action, edit hello *index.js* file in your forked GitHub repo again and click **Commit change**.</span></span> <span data-ttu-id="62933-196">Un nouveau travail démarre dans Jenkins selon hello webhook pour GitHub.</span><span class="sxs-lookup"><span data-stu-id="62933-196">A new job starts in Jenkins based on hello webhook for GitHub.</span></span> <span data-ttu-id="62933-197">Il prend quelques secondes image de Docker toocreate hello et que vous démarrez votre application dans un nouveau conteneur.</span><span class="sxs-lookup"><span data-stu-id="62933-197">It takes a few seconds toocreate hello Docker image and start your app in a new container.</span></span>

<span data-ttu-id="62933-198">Si nécessaire, obtenir à nouveau hello adresse IP publique de votre machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="62933-198">If needed, obtain hello public IP address of your VM again:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="62933-199">Ouvrez un navigateur web et entrez `http://<publicIps>:1337`.</span><span class="sxs-lookup"><span data-stu-id="62933-199">Open a web browser and enter `http://<publicIps>:1337`.</span></span> <span data-ttu-id="62933-200">Votre application Node.js s’affiche et reflète les validations de dernière hello dans votre branche GitHub comme suit :</span><span class="sxs-lookup"><span data-stu-id="62933-200">Your Node.js app is displayed and reflects hello latest commits in your GitHub fork as follows:</span></span>

![Exécution de l’application Node.js](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

<span data-ttu-id="62933-202">Maintenant faire une autre édition toohello *index.js* fichier changement de hello GitHub et la validation.</span><span class="sxs-lookup"><span data-stu-id="62933-202">Now make another edit toohello *index.js* file in GitHub and commit hello change.</span></span> <span data-ttu-id="62933-203">Attendez quelques secondes pour toocomplete de travail hello dans Jenkins, puis actualiser votre version hello mis à jour toosee du navigateur web de votre application dans un nouveau conteneur comme suit :</span><span class="sxs-lookup"><span data-stu-id="62933-203">Wait a few seconds for hello job toocomplete in Jenkins, then refresh your web browser toosee hello updated version of your app running in a new container as follows:</span></span>

![Exécution de l’application Node.js après une autre validation GitHub](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a><span data-ttu-id="62933-205">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="62933-205">Next steps</span></span>
<span data-ttu-id="62933-206">Dans ce didacticiel, vous configuré GitHub toorun un travail de build Jenkins lors de la validation de chaque code et ensuite déployez un tootest de conteneur Docker de votre application.</span><span class="sxs-lookup"><span data-stu-id="62933-206">In this tutorial, you configured GitHub toorun a Jenkins build job on each code commit and then deploy a Docker container tootest your app.</span></span> <span data-ttu-id="62933-207">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="62933-207">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="62933-208">Créer une machine virtuelle Jenkins</span><span class="sxs-lookup"><span data-stu-id="62933-208">Create a Jenkins VM</span></span>
> * <span data-ttu-id="62933-209">Installer et configurer Jenkins</span><span class="sxs-lookup"><span data-stu-id="62933-209">Install and configure Jenkins</span></span>
> * <span data-ttu-id="62933-210">Créer une intégration webhook entre GitHub et Jenkins</span><span class="sxs-lookup"><span data-stu-id="62933-210">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="62933-211">Créer et déclencher des tâches de génération Jenkins à partir de validations GitHub</span><span class="sxs-lookup"><span data-stu-id="62933-211">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="62933-212">Créer une image Docker pour votre application</span><span class="sxs-lookup"><span data-stu-id="62933-212">Create a Docker image for your app</span></span>
> * <span data-ttu-id="62933-213">Vérifier les validations GitHub, générer une nouvelle image Docker et mettre à jour l’application en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="62933-213">Verify GitHub commits build new Docker image and updates running app</span></span>

<span data-ttu-id="62933-214">Avancer toolearn de didacticiel suivant toohello plus d’informations sur la façon toointegrate Jenkins avec Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="62933-214">Advance toohello next tutorial toolearn more about how toointegrate Jenkins with Visual Studio Team Services.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="62933-215">Déployer des applications avec Jenkins et Team Services</span><span class="sxs-lookup"><span data-stu-id="62933-215">Deploy apps with Jenkins and Team Services</span></span>](tutorial-build-deploy-jenkins.md)