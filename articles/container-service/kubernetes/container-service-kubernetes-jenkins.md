---
title: aaaJenkins CI/CD avec Kubernetes dans le Service de conteneur Azure | Documents Microsoft
description: "Comment tooautomate un élément de configuration/CD traiter avec Jenkins toodeploy et mettre à niveau une application en conteneur sur Kubernetes dans le Service de conteneur Azure"
services: container-service
documentationcenter: 
author: chzbrgr71
manager: johny
editor: 
tags: acs, azure-container-service, jenkins
keywords: Docker, conteneurs, Kubernetes, Azure, Jenkins
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: briar
ms.custom: mvc
ms.openlocfilehash: e00e13bf06619bed73e82878777e55458ea3dd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a><span data-ttu-id="30145-104">Intégration Jenkins avec Azure Container Service et Kubernetes</span><span class="sxs-lookup"><span data-stu-id="30145-104">Jenkins integration with Azure Container Service and Kubernetes</span></span> 
<span data-ttu-id="30145-105">Dans ce didacticiel, nous guider tooset de processus hello d’intégration continue d’une application conteneur multiples dans Azure conteneur Service Kubernetes à l’aide de la plateforme de Jenkins hello.</span><span class="sxs-lookup"><span data-stu-id="30145-105">In this tutorial, we walk through hello process tooset up continuous integration of a multi-container application into Azure Container Service Kubernetes using hello Jenkins platform.</span></span> <span data-ttu-id="30145-106">flux de travail Hello met à jour d’image de conteneur hello dans le Hub d’ancrage et POD de Kubernetes hello à l’aide d’un déploiement de mises à niveau.</span><span class="sxs-lookup"><span data-stu-id="30145-106">hello workflow updates hello container image in Docker Hub and upgrades hello Kubernetes pods using a deployment rollout.</span></span> 

## <a name="high-level-process"></a><span data-ttu-id="30145-107">Processus de niveau supérieur</span><span class="sxs-lookup"><span data-stu-id="30145-107">High level process</span></span>
<span data-ttu-id="30145-108">les étapes de base Hello détaillées dans cet article sont :</span><span class="sxs-lookup"><span data-stu-id="30145-108">hello basic steps detailed in this article are:</span></span> 
- <span data-ttu-id="30145-109">Installation d’un cluster Kubernetes dans Container Service</span><span class="sxs-lookup"><span data-stu-id="30145-109">Install a Kubernetes cluster in Container Service</span></span>
- <span data-ttu-id="30145-110">Configurer Jenkins et accès tooContainer Service</span><span class="sxs-lookup"><span data-stu-id="30145-110">Set up Jenkins and configure access tooContainer Service</span></span>
- <span data-ttu-id="30145-111">Création d’un flux de travail Jenkins</span><span class="sxs-lookup"><span data-stu-id="30145-111">Create a Jenkins workflow</span></span>
- <span data-ttu-id="30145-112">Test hello CI/CD processus fin tooend</span><span class="sxs-lookup"><span data-stu-id="30145-112">Test hello CI/CD process end tooend</span></span>

## <a name="install-a-kubernetes-cluster"></a><span data-ttu-id="30145-113">Installation d’un cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="30145-113">Install a Kubernetes cluster</span></span>
    
<span data-ttu-id="30145-114">Déployer un cluster de Kubernetes hello dans le conteneur de Service Azure à l’aide de hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="30145-114">Deploy hello Kubernetes cluster in Azure Container Service using hello following steps.</span></span> <span data-ttu-id="30145-115">Une documentation complète est disponible [ici](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="30145-115">Full documentation is located [here](container-service-kubernetes-walkthrough.md).</span></span>

### <a name="step-1-create-a-resource-group"></a><span data-ttu-id="30145-116">Étape 1 : création d’un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="30145-116">Step 1: Create a resource group</span></span>
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-hello-cluster"></a><span data-ttu-id="30145-117">Étape 2 : Déployer le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="30145-117">Step 2: Deploy hello cluster</span></span>
> [!NOTE]
> <span data-ttu-id="30145-118">Hello étapes suivantes requièrent une clé publique SSH locale stockée dans le dossier de ~/.ssh hello.</span><span class="sxs-lookup"><span data-stu-id="30145-118">hello following steps require a local SSH public key stored in hello ~/.ssh folder.</span></span>
>

```azurecli
RESOURCE_GROUP=my-resource-group
DNS_PREFIX=some-unique-value
CLUSTER_NAME=any-acs-cluster-name

az acs create \
--orchestrator-type=kubernetes \
--resource-group $RESOURCE_GROUP \
--name=$CLUSTER_NAME \
--dns-prefix=$DNS_PREFIX \
--ssh-key-value ~/.ssh/id_rsa.pub \
--admin-username=azureuser \
--master-count=1 \
--agent-count=5 \
--agent-vm-size=Standard_D1_v2
```

## <a name="set-up-jenkins-and-configure-access-toocontainer-service"></a><span data-ttu-id="30145-119">Configurer Jenkins et accès tooContainer Service</span><span class="sxs-lookup"><span data-stu-id="30145-119">Set up Jenkins and configure access tooContainer Service</span></span>

### <a name="step-1-install-jenkins"></a><span data-ttu-id="30145-120">Étape 1 : Installer Jenkins</span><span class="sxs-lookup"><span data-stu-id="30145-120">Step 1: Install Jenkins</span></span>
1. <span data-ttu-id="30145-121">Créez une machine virtuelle Azure avec Ubuntu 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="30145-121">Create an Azure VM with Ubuntu 16.04 LTS.</span></span>  <span data-ttu-id="30145-122">Étant donné que les étapes ultérieures Bonjour sera peut-être tooconnect toothis machine virtuelle en utilisant bash sur votre ordinateur local, la clé publique d’ensemble hello 'Type d’authentification' too'SSH' et la coller hello clé publique SSH qui est stockée localement dans votre dossier ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="30145-122">Since later in hello steps you will need tooconnect toothis VM using bash on your local machine, set hello 'Authentication type' too'SSH public key' and paste hello SSH public key that is stored locally in your ~/.ssh folder.</span></span>  <span data-ttu-id="30145-123">En outre, notez que vous spécifiez, car ce nom d’utilisateur sera Jenkins tableau de bord hello tooview nécessaire et pour la connexion toohello Jenkins VM dans les étapes ultérieures de hello 'Nom_utilisateur'.</span><span class="sxs-lookup"><span data-stu-id="30145-123">Also, take note of hello 'User name' that you specify since this user name will be needed tooview hello Jenkins dashboard and for connecting toohello Jenkins VM in later steps.</span></span>
2. <span data-ttu-id="30145-124">Installez Jenkins en suivant ces [instructions](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="30145-124">Install Jenkins via these [instructions](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span></span> <span data-ttu-id="30145-125">Un didacticiel plus détaillé est disponible sur [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span><span class="sxs-lookup"><span data-stu-id="30145-125">A more detailed tutorial is at [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span></span>
3. <span data-ttu-id="30145-126">tooview hello Jenkins du tableau de bord sur votre ordinateur local, mettre à jour le port tooallow de groupe de sécurité réseau Azure hello 8080 en ajoutant une règle de trafic entrant qui autorise l’accès tooport 8080.</span><span class="sxs-lookup"><span data-stu-id="30145-126">tooview hello Jenkins dashboard on your local machine, update hello Azure network security group tooallow port 8080 by adding an inbound rule that allows access tooport 8080.</span></span>  <span data-ttu-id="30145-127">Vous pouvez également configurer un réacheminement de port en exécutant la commande suivante : `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`.</span><span class="sxs-lookup"><span data-stu-id="30145-127">Alternatively, you may setup port forwarding by running this command: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span></span>
4. <span data-ttu-id="30145-128">Connexion serveur Jenkins de tooyour à l’aide du navigateur de hello en accédant d’adresse IP publique toohello (http:// < your_jenkins_public_ip > : 8080) et de déverrouillage du tableau de bord Jenkins hello pour hello première fois avec un mot de passe administrateur initial hello.</span><span class="sxs-lookup"><span data-stu-id="30145-128">Connect tooyour Jenkins server using hello browser by navigating toohello public IP (http://<your_jenkins_public_ip>:8080) and unlock hello Jenkins dashboard for hello first time with hello initial admin password.</span></span>  <span data-ttu-id="30145-129">mot de passe administrateur Hello est stocké à /var/lib/jenkins/secrets/initialAdminPassword sur hello Jenkins VM.</span><span class="sxs-lookup"><span data-stu-id="30145-129">hello admin password is stored at /var/lib/jenkins/secrets/initialAdminPassword on hello Jenkins VM.</span></span>  <span data-ttu-id="30145-130">Un tooget facilement ce mot de passe est tooSSH dans hello Jenkins VM : `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="30145-130">An easy way tooget this password is tooSSH into hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="30145-131">Ensuite, exécutez la commande suivante : `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span><span class="sxs-lookup"><span data-stu-id="30145-131">Next, run: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span></span>
5. <span data-ttu-id="30145-132">Installer Docker sur l’ordinateur de Jenkins hello via ces [instructions](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span><span class="sxs-lookup"><span data-stu-id="30145-132">Install Docker on hello Jenkins machine via these [instructions](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span></span> <span data-ttu-id="30145-133">Ainsi, Docker toobe de commandes s’exécutent dans les travaux de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="30145-133">This allows for Docker commands toobe run in Jenkins jobs.</span></span>
6. <span data-ttu-id="30145-134">Configurer Docker autorisations tooallow Jenkins tooaccess hello Docker point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="30145-134">Configure Docker permissions tooallow Jenkins tooaccess hello Docker endpoint.</span></span>

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. <span data-ttu-id="30145-135">Installez la CLI `kubectl` sur Jenkins.</span><span class="sxs-lookup"><span data-stu-id="30145-135">Install `kubectl` CLI on Jenkins.</span></span> <span data-ttu-id="30145-136">Des informations supplémentaires sont disponibles dans l’article [Installation et configuration de kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span><span class="sxs-lookup"><span data-stu-id="30145-136">More details are at [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>  <span data-ttu-id="30145-137">Travaux de Jenkins utilise 'kubectl' toomanage et déployer toohello Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="30145-137">Jenkins jobs will use 'kubectl' toomanage and deploy toohello Kubernetes cluster.</span></span>

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-toohello-kubernetes-cluster"></a><span data-ttu-id="30145-138">Étape 2 : Configurer le cluster d’accès toohello Kubernetes</span><span class="sxs-lookup"><span data-stu-id="30145-138">Step 2: Set up access toohello Kubernetes cluster</span></span>

> [!NOTE]
> <span data-ttu-id="30145-139">Il existe plusieurs hello de tooaccomplishing approches comme suit.</span><span class="sxs-lookup"><span data-stu-id="30145-139">There are multiple approaches tooaccomplishing hello following steps.</span></span> <span data-ttu-id="30145-140">Utiliser hello approche est plus facile pour vous.</span><span class="sxs-lookup"><span data-stu-id="30145-140">Use hello approach that is easiest for you.</span></span>
>

1. <span data-ttu-id="30145-141">Hello de copie `kubectl` toohello du fichier config Jenkins de l’ordinateur afin que les travaux de Jenkins ont cluster d’accès toohello Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="30145-141">Copy hello `kubectl` config file toohello Jenkins machine so that Jenkins jobs have access toohello Kubernetes cluster.</span></span> <span data-ttu-id="30145-142">Ces instructions supposent que vous utilisez un interpréteur de commandes à partir d’un autre ordinateur que hello Jenkins VM et qu’une clé publique SSH locale est stockée dans le dossier ~/.ssh de l’ordinateur hello.</span><span class="sxs-lookup"><span data-stu-id="30145-142">These instructions assume that you are using bash from a different machine than hello Jenkins VM and that a local SSH public key is stored in hello machine's ~/.ssh folder.</span></span>

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. <span data-ttu-id="30145-143">Valider de Jenkins que hello Kubernetes cluster est accessible.</span><span class="sxs-lookup"><span data-stu-id="30145-143">Validate from Jenkins that hello Kubernetes cluster is accessible.</span></span>  <span data-ttu-id="30145-144">toodo, SSH dans hello Jenkins VM : `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="30145-144">toodo this, SSH into hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="30145-145">Ensuite, vérifiez Jenkins connexion tooyour cluster : `kubectl cluster-info`.</span><span class="sxs-lookup"><span data-stu-id="30145-145">Next, verify Jenkins can successfully connect tooyour cluster: `kubectl cluster-info`.</span></span>
    

## <a name="create-a-jenkins-workflow"></a><span data-ttu-id="30145-146">Création d’un flux de travail Jenkins</span><span class="sxs-lookup"><span data-stu-id="30145-146">Create a Jenkins workflow</span></span>

### <a name="prerequisites"></a><span data-ttu-id="30145-147">Composants requis</span><span class="sxs-lookup"><span data-stu-id="30145-147">Prerequisites</span></span>

- <span data-ttu-id="30145-148">Compte GitHub pour le référentiel de code.</span><span class="sxs-lookup"><span data-stu-id="30145-148">GitHub account for code repo.</span></span>
- <span data-ttu-id="30145-149">Docker Hub compte toostore et mise à jour les images.</span><span class="sxs-lookup"><span data-stu-id="30145-149">Docker Hub account toostore and update images.</span></span>
- <span data-ttu-id="30145-150">Applications en conteneur pouvant être reconstruites et mises à jour.</span><span class="sxs-lookup"><span data-stu-id="30145-150">Containerized application that can be rebuilt and updated.</span></span> <span data-ttu-id="30145-151">Vous pouvez utiliser cet exemple d’application de conteneur écrite en Golang : https://github.com/chzbrgr71/go-web</span><span class="sxs-lookup"><span data-stu-id="30145-151">You can use this sample container app written in Golang: https://github.com/chzbrgr71/go-web</span></span> 

> [!NOTE]
> <span data-ttu-id="30145-152">Hello étapes suivantes doivent être effectuées dans votre propre compte GitHub.</span><span class="sxs-lookup"><span data-stu-id="30145-152">hello following steps must be performed in your own GitHub account.</span></span> <span data-ttu-id="30145-153">Pensez hello tooclone libre au-dessus de dépôt, mais vous devez utiliser votre propre webhooks de hello tooconfigure compte et Jenkins accéder.</span><span class="sxs-lookup"><span data-stu-id="30145-153">Feel free tooclone hello above repo, but you must use your own account tooconfigure hello webhooks and Jenkins access.</span></span>
>

### <a name="step-1-deploy-initial-v1-of-application"></a><span data-ttu-id="30145-154">Étape 1 : Déployer la v1 initiale de l’application</span><span class="sxs-lookup"><span data-stu-id="30145-154">Step 1: Deploy initial v1 of application</span></span>
1. <span data-ttu-id="30145-155">Build application hello à partir de l’ordinateur de développeur hello avec hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="30145-155">Build hello app from hello developer machine with hello following commands.</span></span> <span data-ttu-id="30145-156">Remplacez `myrepo` par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="30145-156">Replace `myrepo` with your own.</span></span>
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. <span data-ttu-id="30145-157">Push image tooDocker Hub.</span><span class="sxs-lookup"><span data-stu-id="30145-157">Push image tooDocker Hub.</span></span>

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. <span data-ttu-id="30145-158">Déployer un cluster de Kubernetes toohello.</span><span class="sxs-lookup"><span data-stu-id="30145-158">Deploy toohello Kubernetes cluster.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="30145-159">Modifier hello `go-web.yaml` fichier tooupdate votre image de conteneur et du référentiel.</span><span class="sxs-lookup"><span data-stu-id="30145-159">Edit hello `go-web.yaml` file tooupdate your container image and repo.</span></span>
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a><span data-ttu-id="30145-160">Étape 2 : Configurer le système de Jenkins</span><span class="sxs-lookup"><span data-stu-id="30145-160">Step 2: Configure Jenkins system</span></span>
1. <span data-ttu-id="30145-161">Cliquez sur **Gérer Jenkins** > **Configurer le système**.</span><span class="sxs-lookup"><span data-stu-id="30145-161">Click **Manage Jenkins** > **Configure System**.</span></span>
2. <span data-ttu-id="30145-162">Sous **GitHub**, sélectionnez **Ajouter un serveur GitHub**.</span><span class="sxs-lookup"><span data-stu-id="30145-162">Under **GitHub**, select **Add GitHub Server**.</span></span>
3. <span data-ttu-id="30145-163">Laissez **URL d’API** comme valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="30145-163">Leave **API URL** as default.</span></span>
4. <span data-ttu-id="30145-164">Sous **Informations d’identification**, ajoutez des informations d’identification Jenkins à l’aide d’un **Texte secret**.</span><span class="sxs-lookup"><span data-stu-id="30145-164">Under **Credentials**, add a Jenkins credential using **Secret text**.</span></span> <span data-ttu-id="30145-165">Nous recommandons l’utilisation de jetons d’accès personnels GitHub, qui sont configurés dans vos paramètres de compte d’utilisateur GitHub.</span><span class="sxs-lookup"><span data-stu-id="30145-165">We recommend using GitHub personal access tokens, which are configured in your GitHub user account settings.</span></span> <span data-ttu-id="30145-166">Plus d’informations, rendez-vous [ici](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/).</span><span class="sxs-lookup"><span data-stu-id="30145-166">More details on this [here.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span></span>
5. <span data-ttu-id="30145-167">Cliquez sur **tester la connexion** tooensure est configuré correctement.</span><span class="sxs-lookup"><span data-stu-id="30145-167">Click **Test connection** tooensure this is configured correctly.</span></span>
6. <span data-ttu-id="30145-168">Sous **Propriétés globales**, ajoutez une variable d’environnement `DOCKER_HUB` et fournissez votre mot de passe Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="30145-168">Under **Global Properties**, add an environment variable `DOCKER_HUB` and provide your Docker Hub password.</span></span> <span data-ttu-id="30145-169">(Ceci est utile dans cette démonstration, mais un scénario de production nécessite une approche plus sécurisée.)</span><span class="sxs-lookup"><span data-stu-id="30145-169">(This is useful in this demo, but a production scenario would require a more secure approach.)</span></span>
7. <span data-ttu-id="30145-170">Enregistrez.</span><span class="sxs-lookup"><span data-stu-id="30145-170">Save.</span></span>

![Accès de Jenkins à GitHub](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-hello-jenkins-workflow"></a><span data-ttu-id="30145-172">Étape 3 : Créer des flux de travail hello Jenkins</span><span class="sxs-lookup"><span data-stu-id="30145-172">Step 3: Create hello Jenkins workflow</span></span>
1. <span data-ttu-id="30145-173">Créez un élément Jenkins.</span><span class="sxs-lookup"><span data-stu-id="30145-173">Create a Jenkins item.</span></span>
2. <span data-ttu-id="30145-174">Fournissez un nom (par exemple, « go-web ») et sélectionnez **Freestyle Project**.</span><span class="sxs-lookup"><span data-stu-id="30145-174">Provide a name (for example, "go-web") and select **Freestyle Project**.</span></span> 
3. <span data-ttu-id="30145-175">Vérifiez **GitHub projet** et fournir le référentiel GitHub de hello URL tooyour.</span><span class="sxs-lookup"><span data-stu-id="30145-175">Check **GitHub project** and provide hello URL tooyour GitHub repo.</span></span>
4. <span data-ttu-id="30145-176">Dans **gestion du Code Source**, fournissez les informations d’identification et les URL de référentiel GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="30145-176">In **Source Code Management**, provide hello GitHub repo URL and credentials.</span></span> 
5. <span data-ttu-id="30145-177">Ajouter un **étape de génération** de type **exécuter shell** et utilisez hello après le texte :</span><span class="sxs-lookup"><span data-stu-id="30145-177">Add a **Build Step** of type **Execute shell** and use hello following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. <span data-ttu-id="30145-178">Ajoutez un autre **étape de génération** de type **exécuter shell** et utilisez hello après le texte :</span><span class="sxs-lookup"><span data-stu-id="30145-178">Add another **Build Step** of type **Execute shell** and use hello following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Étapes de génération Jenkins](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. <span data-ttu-id="30145-180">Enregistrer l’élément de Jenkins hello et tester avec **générer maintenant**.</span><span class="sxs-lookup"><span data-stu-id="30145-180">Save hello Jenkins item and test with **Build Now**.</span></span>

### <a name="step-4-connect-github-webhook"></a><span data-ttu-id="30145-181">Étape 4 : Se connecter au webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="30145-181">Step 4: Connect GitHub webhook</span></span>
1. <span data-ttu-id="30145-182">Dans l’élément de Jenkins hello vous avez créé, cliquez sur **configurer**.</span><span class="sxs-lookup"><span data-stu-id="30145-182">In hello Jenkins item you created, click **Configure**.</span></span>
2. <span data-ttu-id="30145-183">Sous **Déclencheurs de génération**, sélectionnez **Déclencher un hook GitHub pour l’interrogation GITScm**, puis **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="30145-183">Under **Build Triggers**, select **GitHub hook trigger for GITScm polling** and **Save**.</span></span> <span data-ttu-id="30145-184">Cela configure automatiquement hello GitHub webhook.</span><span class="sxs-lookup"><span data-stu-id="30145-184">This automatically configures hello GitHub webhook.</span></span>
3. <span data-ttu-id="30145-185">Dans votre référentiel GitHub pour « go-web », cliquez sur **Paramètres > Webhooks**.</span><span class="sxs-lookup"><span data-stu-id="30145-185">In your GitHub repo for go-web, click **Settings > Webhooks**.</span></span>
4. <span data-ttu-id="30145-186">Vérifiez que hello webhook Jenkins URL a été ajouté avec succès.</span><span class="sxs-lookup"><span data-stu-id="30145-186">Verify that hello Jenkins webhook URL was added successfully.</span></span> <span data-ttu-id="30145-187">URL de Hello doit se terminer par « github-webhook ».</span><span class="sxs-lookup"><span data-stu-id="30145-187">hello URL should end in "github-webhook".</span></span>

![Configuration du webhook Jenkins](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-hello-cicd-process-end-tooend"></a><span data-ttu-id="30145-189">Test hello CI/CD processus fin tooend</span><span class="sxs-lookup"><span data-stu-id="30145-189">Test hello CI/CD process end tooend</span></span>

1. <span data-ttu-id="30145-190">Mettre à jour le code pour le dépôt de hello et push/synch avec le référentiel GitHub de hello.</span><span class="sxs-lookup"><span data-stu-id="30145-190">Update code for hello repo and push/synch with hello GitHub repository.</span></span>
2. <span data-ttu-id="30145-191">À partir de la console de Jenkins hello, activez hello **générer un historique** et valider ce hello travail a été exécuté.</span><span class="sxs-lookup"><span data-stu-id="30145-191">From hello Jenkins console, check hello **Build History** and validate that hello job has run.</span></span> <span data-ttu-id="30145-192">Afficher les détails de toosee sortie console.</span><span class="sxs-lookup"><span data-stu-id="30145-192">View console output toosee details.</span></span>
3. <span data-ttu-id="30145-193">À partir de Kubernetes, afficher les détails de hello mis à niveau le déploiement :</span><span class="sxs-lookup"><span data-stu-id="30145-193">From Kubernetes, view details of hello upgraded deployment:</span></span>

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a><span data-ttu-id="30145-194">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="30145-194">Next steps</span></span>

- <span data-ttu-id="30145-195">Déployez le registre de conteneurs Azure et stockez des images dans un référentiel sécurisé.</span><span class="sxs-lookup"><span data-stu-id="30145-195">Deploy Azure Container Registry and store images in a secure repository.</span></span> <span data-ttu-id="30145-196">Consultez les [documents du Registre de conteneurs Azure](https://docs.microsoft.com/azure/container-registry).</span><span class="sxs-lookup"><span data-stu-id="30145-196">See [Azure Container Registry docs](https://docs.microsoft.com/azure/container-registry).</span></span>
- <span data-ttu-id="30145-197">Créez un flux de travail plus complexe qui inclut les déploiements côte à côte et les tests automatisés dans Jenkins.</span><span class="sxs-lookup"><span data-stu-id="30145-197">Build a more complex workflow that includes side-by-side deployment and automated tests in Jenkins.</span></span>
- <span data-ttu-id="30145-198">Pour plus d’informations sur l’élément de configuration/CD avec Jenkins et Kubernetes, consultez hello [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span><span class="sxs-lookup"><span data-stu-id="30145-198">For more information about CI/CD with Jenkins and Kubernetes, see hello [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span></span>
