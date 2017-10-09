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
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a>Intégration Jenkins avec Azure Container Service et Kubernetes 
Dans ce didacticiel, nous guider tooset de processus hello d’intégration continue d’une application conteneur multiples dans Azure conteneur Service Kubernetes à l’aide de la plateforme de Jenkins hello. flux de travail Hello met à jour d’image de conteneur hello dans le Hub d’ancrage et POD de Kubernetes hello à l’aide d’un déploiement de mises à niveau. 

## <a name="high-level-process"></a>Processus de niveau supérieur
les étapes de base Hello détaillées dans cet article sont : 
- Installation d’un cluster Kubernetes dans Container Service
- Configurer Jenkins et accès tooContainer Service
- Création d’un flux de travail Jenkins
- Test hello CI/CD processus fin tooend

## <a name="install-a-kubernetes-cluster"></a>Installation d’un cluster Kubernetes
    
Déployer un cluster de Kubernetes hello dans le conteneur de Service Azure à l’aide de hello comme suit. Une documentation complète est disponible [ici](container-service-kubernetes-walkthrough.md).

### <a name="step-1-create-a-resource-group"></a>Étape 1 : création d’un groupe de ressources
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-hello-cluster"></a>Étape 2 : Déployer le cluster de hello
> [!NOTE]
> Hello étapes suivantes requièrent une clé publique SSH locale stockée dans le dossier de ~/.ssh hello.
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

## <a name="set-up-jenkins-and-configure-access-toocontainer-service"></a>Configurer Jenkins et accès tooContainer Service

### <a name="step-1-install-jenkins"></a>Étape 1 : Installer Jenkins
1. Créez une machine virtuelle Azure avec Ubuntu 16.04 LTS.  Étant donné que les étapes ultérieures Bonjour sera peut-être tooconnect toothis machine virtuelle en utilisant bash sur votre ordinateur local, la clé publique d’ensemble hello 'Type d’authentification' too'SSH' et la coller hello clé publique SSH qui est stockée localement dans votre dossier ~/.ssh.  En outre, notez que vous spécifiez, car ce nom d’utilisateur sera Jenkins tableau de bord hello tooview nécessaire et pour la connexion toohello Jenkins VM dans les étapes ultérieures de hello 'Nom_utilisateur'.
2. Installez Jenkins en suivant ces [instructions](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu). Un didacticiel plus détaillé est disponible sur [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).
3. tooview hello Jenkins du tableau de bord sur votre ordinateur local, mettre à jour le port tooallow de groupe de sécurité réseau Azure hello 8080 en ajoutant une règle de trafic entrant qui autorise l’accès tooport 8080.  Vous pouvez également configurer un réacheminement de port en exécutant la commande suivante : `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`.
4. Connexion serveur Jenkins de tooyour à l’aide du navigateur de hello en accédant d’adresse IP publique toohello (http:// < your_jenkins_public_ip > : 8080) et de déverrouillage du tableau de bord Jenkins hello pour hello première fois avec un mot de passe administrateur initial hello.  mot de passe administrateur Hello est stocké à /var/lib/jenkins/secrets/initialAdminPassword sur hello Jenkins VM.  Un tooget facilement ce mot de passe est tooSSH dans hello Jenkins VM : `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.  Ensuite, exécutez la commande suivante : `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
5. Installer Docker sur l’ordinateur de Jenkins hello via ces [instructions](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts). Ainsi, Docker toobe de commandes s’exécutent dans les travaux de Jenkins.
6. Configurer Docker autorisations tooallow Jenkins tooaccess hello Docker point de terminaison.

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. Installez la CLI `kubectl` sur Jenkins. Des informations supplémentaires sont disponibles dans l’article [Installation et configuration de kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).  Travaux de Jenkins utilise 'kubectl' toomanage et déployer toohello Kubernetes cluster.

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-toohello-kubernetes-cluster"></a>Étape 2 : Configurer le cluster d’accès toohello Kubernetes

> [!NOTE]
> Il existe plusieurs hello de tooaccomplishing approches comme suit. Utiliser hello approche est plus facile pour vous.
>

1. Hello de copie `kubectl` toohello du fichier config Jenkins de l’ordinateur afin que les travaux de Jenkins ont cluster d’accès toohello Kubernetes. Ces instructions supposent que vous utilisez un interpréteur de commandes à partir d’un autre ordinateur que hello Jenkins VM et qu’une clé publique SSH locale est stockée dans le dossier ~/.ssh de l’ordinateur hello.

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. Valider de Jenkins que hello Kubernetes cluster est accessible.  toodo, SSH dans hello Jenkins VM : `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.  Ensuite, vérifiez Jenkins connexion tooyour cluster : `kubectl cluster-info`.
    

## <a name="create-a-jenkins-workflow"></a>Création d’un flux de travail Jenkins

### <a name="prerequisites"></a>Composants requis

- Compte GitHub pour le référentiel de code.
- Docker Hub compte toostore et mise à jour les images.
- Applications en conteneur pouvant être reconstruites et mises à jour. Vous pouvez utiliser cet exemple d’application de conteneur écrite en Golang : https://github.com/chzbrgr71/go-web 

> [!NOTE]
> Hello étapes suivantes doivent être effectuées dans votre propre compte GitHub. Pensez hello tooclone libre au-dessus de dépôt, mais vous devez utiliser votre propre webhooks de hello tooconfigure compte et Jenkins accéder.
>

### <a name="step-1-deploy-initial-v1-of-application"></a>Étape 1 : Déployer la v1 initiale de l’application
1. Build application hello à partir de l’ordinateur de développeur hello avec hello suivant les commandes. Remplacez `myrepo` par les vôtres.
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. Push image tooDocker Hub.

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. Déployer un cluster de Kubernetes toohello.
    
    > [!NOTE] 
    > Modifier hello `go-web.yaml` fichier tooupdate votre image de conteneur et du référentiel.
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a>Étape 2 : Configurer le système de Jenkins
1. Cliquez sur **Gérer Jenkins** > **Configurer le système**.
2. Sous **GitHub**, sélectionnez **Ajouter un serveur GitHub**.
3. Laissez **URL d’API** comme valeur par défaut.
4. Sous **Informations d’identification**, ajoutez des informations d’identification Jenkins à l’aide d’un **Texte secret**. Nous recommandons l’utilisation de jetons d’accès personnels GitHub, qui sont configurés dans vos paramètres de compte d’utilisateur GitHub. Plus d’informations, rendez-vous [ici](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/).
5. Cliquez sur **tester la connexion** tooensure est configuré correctement.
6. Sous **Propriétés globales**, ajoutez une variable d’environnement `DOCKER_HUB` et fournissez votre mot de passe Docker Hub. (Ceci est utile dans cette démonstration, mais un scénario de production nécessite une approche plus sécurisée.)
7. Enregistrez.

![Accès de Jenkins à GitHub](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-hello-jenkins-workflow"></a>Étape 3 : Créer des flux de travail hello Jenkins
1. Créez un élément Jenkins.
2. Fournissez un nom (par exemple, « go-web ») et sélectionnez **Freestyle Project**. 
3. Vérifiez **GitHub projet** et fournir le référentiel GitHub de hello URL tooyour.
4. Dans **gestion du Code Source**, fournissez les informations d’identification et les URL de référentiel GitHub hello. 
5. Ajouter un **étape de génération** de type **exécuter shell** et utilisez hello après le texte :

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. Ajoutez un autre **étape de génération** de type **exécuter shell** et utilisez hello après le texte :

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Étapes de génération Jenkins](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. Enregistrer l’élément de Jenkins hello et tester avec **générer maintenant**.

### <a name="step-4-connect-github-webhook"></a>Étape 4 : Se connecter au webhook GitHub
1. Dans l’élément de Jenkins hello vous avez créé, cliquez sur **configurer**.
2. Sous **Déclencheurs de génération**, sélectionnez **Déclencher un hook GitHub pour l’interrogation GITScm**, puis **Enregistrer**. Cela configure automatiquement hello GitHub webhook.
3. Dans votre référentiel GitHub pour « go-web », cliquez sur **Paramètres > Webhooks**.
4. Vérifiez que hello webhook Jenkins URL a été ajouté avec succès. URL de Hello doit se terminer par « github-webhook ».

![Configuration du webhook Jenkins](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-hello-cicd-process-end-tooend"></a>Test hello CI/CD processus fin tooend

1. Mettre à jour le code pour le dépôt de hello et push/synch avec le référentiel GitHub de hello.
2. À partir de la console de Jenkins hello, activez hello **générer un historique** et valider ce hello travail a été exécuté. Afficher les détails de toosee sortie console.
3. À partir de Kubernetes, afficher les détails de hello mis à niveau le déploiement :

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a>Étapes suivantes

- Déployez le registre de conteneurs Azure et stockez des images dans un référentiel sécurisé. Consultez les [documents du Registre de conteneurs Azure](https://docs.microsoft.com/azure/container-registry).
- Créez un flux de travail plus complexe qui inclut les déploiements côte à côte et les tests automatisés dans Jenkins.
- Pour plus d’informations sur l’élément de configuration/CD avec Jenkins et Kubernetes, consultez hello [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).
