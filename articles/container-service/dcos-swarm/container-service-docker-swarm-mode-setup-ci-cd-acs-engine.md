---
title: "aaaCI/CD avec moteur du Service de conteneur d’Azure et de Swarm | Documents Microsoft"
description: Utiliser le moteur du Service de conteneur Azure avec le Mode de Docker Swarm un Registre de conteneur Azure et Visual Studio Team Services toodeliver en permanence une application de .NET Core conteneur multi
services: container-service
documentationcenter: " "
author: diegomrtnzg
manager: esterdnb
tags: acs, azure-container-service, acs-engine
keywords: Docker, conteneurs, micro-services, Swarm, Azure, Visual Studio Team Services, DevOps, moteur ACS
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/27/2017
ms.author: diegomrtnzg
ms.custom: mvc
ms.openlocfilehash: 040522c452f7ea0ce3c92f2fe57b1c141b97e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a>L’élément de configuration complet/CD pipeline toodeploy une application conteneur multiples sur un Service de conteneur Azure avec le moteur d’ACS et le Mode Docker Swarm à l’aide de Visual Studio Team Services

*Cet article est basé sur [/CD complète de l’élément de configuration de pipeline toodeploy une application conteneur multi Azure Service de conteneur avec Docker Swarm à l’aide de Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentation*

Aujourd'hui, un des hello plus grands défis lors de développement d’applications modernes pour le cloud de hello toodeliver en mesure de ces applications en continu. Dans cet article, vous découvrez comment tooimplement une intégration complète continue et déploiement (élément de configuration/CD) pipeline à l’aide de : 
* Moteur Azure Container Service avec le mode Docker Swarm
* Azure Container Registry
* Visual Studio Team Services

Cet article est basé sur une application simple, disponible sur [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), développée avec ASP.NET Core. application Hello est composée de quatre services différents : trois web API et un site web frontal :

![Exemple d’application MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

objectif de Hello est toodeliver cette application en continu dans un cluster de Mode de Docker Swarm, à l’aide de Visual Studio Team Services. la figure suivant de Hello détails ce pipeline de livraison continue :

![Exemple d’application MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

Voici une brève explication des étapes de hello :

1. Modifications du code sont validées toohello référentiel de code source (ici, GitHub) 
2. GitHub déclenche une build dans Visual Studio Team Services. 
3. Obtient la version la plus récente de sources de hello hello de Visual Studio Team Services et génère toutes les images hello qui composent l’application hello 
4. Visual Studio Team Services transmet chaque registre Docker de tooa image créé à l’aide du service de Registre de conteneur Azure hello 
5. Visual Studio Team Services déclenche une nouvelle mise en production. 
6. version de Hello exécute des commandes à l’aide de SSH sur le nœud principal du cluster service conteneur Azure hello 
7. Docker Swarm Mode sur le cluster de hello extrait la version la plus récente des images de hello hello 
8. Hello nouvelle version d’application hello est déployée à l’aide de la pile de Docker 

## <a name="prerequisites"></a>Composants requis

Avant de commencer ce didacticiel, vous devez hello toocomplete tâches suivantes :

- [Création d’un cluster du Mode Swarm dans Azure Container Service avec le moteur ACS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [Se connecter à un cluster d’essaim hello dans le conteneur de Service Azure](../container-service-connect.md)
- [Utilisation d’un Registre de conteneurs Azure](../../container-registry/container-registry-get-started-portal.md)
- [Création d’un compte et d’un projet d’équipe Visual Studio Team Services](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [Effectuer un branchement tooyour de référentiel GitHub hello compte GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> orchestrator de Docker Swarm Hello dans le Service de conteneur Azure utilise autonome hérité essaim. Actuellement, hello intégré [essaim mode](https://docs.docker.com/engine/swarm/) (dans Docker 1.12 et versions ultérieures) n’est pas un orchestrateur de prise en charge dans le Service de conteneur Azure. Pour cette raison, nous utilisons [ACS moteur](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), une communauté [modèle de démarrage rapide](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), ou une solution de Docker Bonjour [Azure Marketplace](https://azuremarketplace.microsoft.com).
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a>Étape 1 : configuration de votre compte Visual Studio Team Services 

Dans cette section, vous allez configurer votre compte Visual Studio Team Services. points de terminaison des Services de VSTS de tooconfigure, dans votre projet Visual Studio Team Services, cliquez sur hello **paramètres** icône dans la barre d’outils hello, puis sélectionnez **Services**.

![Ouvrez Point de terminaison de services](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a>Connectez Visual Studio Team Services avec votre compte Azure

Configurez une connexion entre votre projet VSTS et votre compte Azure.

1. Sur hello gauche, cliquez sur **nouveau point de terminaison de Service** > **Azure Resource Manager**.
2. toowork VSTS tooauthorize avec votre compte Azure, sélectionnez votre **abonnement** et cliquez sur **OK**.

    ![Visual Studio Team Services - Autoriser Azure](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a>Connexion entre Visual Studio Team Services et GitHub

Configurez une connexion entre votre projet VSTS et votre compte GitHub.

1. Sur hello gauche, cliquez sur **nouveau point de terminaison de Service** > **GitHub**.
2. toowork VSTS tooauthorize avec votre compte GitHub, cliquez sur **Authorize** et suivez la procédure hello dans la fenêtre hello qui s’ouvre.

    ![Visual Studio Team Services - Autoriser GitHub](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-tooyour-azure-container-service-cluster"></a>Connecter le cluster de Service de conteneur Azure tooyour VSTS

dernières étapes de Hello avant d’entrer dans le pipeline de l’élément de configuration/CD hello sont tooconfigure connexions externes tooyour Docker Swarm un cluster dans Azure. 

1. Pour le cluster de Docker Swarm hello, ajoutez un point de terminaison de type **SSH**. Puis entrez les informations de connexion SSH hello de votre cluster essaim (nœud principal).

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

La configuration hello est effectuée maintenant. Dans les étapes suivantes hello, créer pipeline de l’élément de configuration/CD hello qui génère et déploie hello application toohello Docker Swarm cluster. 

## <a name="step-2-create-hello-build-definition"></a>Étape 2 : Créer la définition de build hello

Dans cette étape, vous configurez une définition de build pour votre projet VSTS et définissez le flux de travail de build hello pour vos images de conteneur

### <a name="initial-definition-setup"></a>Configuration de la définition initiale

1. toocreate une définition de build, connecter tooyour Visual Studio Team Services projet, puis cliquez sur **générer & version**. Bonjour **des définitions de Build** , cliquez sur **+ nouveau**. 

    ![Visual Studio Team Services - Nouvelle définition de build](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. Sélectionnez hello **processus vide**.

    ![Visual Studio Team Services - Nouvelle définition de build vide](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. Ensuite, cliquez sur hello **Variables** onglet et créez deux nouvelles variables : **RegistryURL** et **AgentURL**. Collez les valeurs hello de votre Registre et le Cluster Agents DNS.

    ![Visual Studio Team Services - Configuration des variables de la build](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. Sur hello **définitions de Build** page, ouvrez hello **déclencheurs** onglet et configurer l’intégration continue hello build toouse avec branchement hello du projet MyShop hello que vous avez créé dans les conditions préalables de hello. Sélectionnez ensuite **Modifications de lot**. Assurez-vous que vous sélectionnez *docker-linux* comme hello **branche spécification**.

    ![Visual Studio Team Services - Configuration du référentiel de la build](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. Enfin, cliquez sur hello **Options** onglet et configurer trop de file d’attente de l’agent de valeur par défaut hello**aperçu de Linux hébergés**.

    ![Visual Studio Team Services - Configuration de l’agent hébergé](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-hello-build-workflow"></a>Définir le flux de travail de build hello
les étapes suivantes Hello définissent des flux de travail de build hello. Tout d’abord, vous devez source hello tooconfigure code de hello. toodo il, sélectionnez **GitHub** et votre **référentiel** et **branche** (docker linux).

![Visual Studio Team Services - Configurer la source du code](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

Il existe cinq toobuild d’images de conteneur pour hello *MyShop* application. Chaque image est générée à l’aide de hello que dockerfile situé dans des dossiers du projet hello :

* ProductsApi
* Proxy
* RatingsApi
* RecommandationsApi
* ShopFront

Vous avez besoin de deux étapes de Docker pour chaque image, une image de hello toobuild et une image de hello toopush dans le Registre de conteneur Azure hello. 

1. tooadd une étape dans le flux de travail hello, cliquez sur **+ ajouter une étape build** et sélectionnez **Docker**.

    ![Visual Studio Team Services - Ajout d’étapes de build](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. Pour chaque image, configurez une seule étape qui utilise hello `docker build` commande.

    ![Visual Studio Team Services - Build Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    Opération de génération pour hello, sélectionnez votre Registre de conteneur Azure, hello **générer une image** action et hello Dockerfile qui définit chaque image. Ensemble hello **du répertoire de travail** dans le répertoire racine du fichier Dockerfile hello, définir hello **nom de l’Image**, puis sélectionnez **inclure une balise Latest**.
    
    Hello, nom de l’Image a toobe dans ce format : ```$(RegistryURL)/[NAME]:$(Build.BuildId)```. Remplacez **[nom]** avec le nom de l’image hello :
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. Pour chaque image, configurer une deuxième étape qui utilise hello `docker push` commande.

    ![Visual Studio Team Services - Envoi du fichier Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    Pour une opération de diffusion hello, sélectionnez votre Registre conteneur Azure, hello **de pousser une image** action, entrez hello **nom de l’Image** qui est intégré dans l’étape précédente de hello et sélectionnez **inclure une balise Latest** .

4. Après avoir configuré la génération de hello et distribuer les étapes pour chacune des images de cinq hello, ajouter que trois étapes plus Bonjour générer des flux de travail.

   ![Visual Studio Team Services - Ajout d’une tâche de ligne de commande](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. Une tâche de ligne de commande qui utilise un Bonjour tooreplace du script bash *RegistryURL* occurrence dans le fichier de docker-compose.yml hello avec la variable de RegistryURL hello. 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio Team Services - Mise à jour du fichier Compose avec l’URL du Registre](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. Une tâche de ligne de commande qui utilise un Bonjour tooreplace du script bash *AgentURL* occurrence dans le fichier de docker-compose.yml hello avec la variable de AgentURL hello.
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. Une tâche qui supprime hello mis à jour le fichier de message en tant qu’un artefact de build il peut être utilisé dans la version de hello. Hello suivant l’écran pour plus d’informations, consultez.

         ![Visual Studio Team Services - Publication de l’artefact](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Visual Studio Team Services - Publication du fichier Compose](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. Cliquez sur **enregistrer et de file d’attente** tootest votre définition de build.

   ![Visual Studio Team Services - Enregistrer et mettre en file d’attente](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio Team Services - Nouvelle file d’attente](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. Si hello **générer** est correct, vous avez toosee cet écran :

  ![Visual Studio Team Services - Build réussie](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-hello-release-definition"></a>Étape 3 : Créer la définition de la version hello

Visual Studio Team Services vous permet de trop[gérer les versions dans des environnements](https://www.visualstudio.com/team-services/release-management/). Vous pouvez activer toomake déploiement continu sûr que votre application est déployée sur vos environnements différents (par exemple, le développement, test, préproduction et production) de façon fluide. Vous pouvez créer un environnement qui représente votre cluster Docker Swarm Azure Container Service.

![Visual Studio Team Services - version tooACS](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a>Configuration de la mise en production initiale

1. toocreate une définition de la mise en production, cliquez sur **versions** > **+ Release**

2. source d’artefact tooconfigure hello, cliquez sur **artefacts** > **lier une source d’artefact**. Ici, lier cette nouvelle définition toohello version Release que vous avez définie à l’étape précédente de hello. Après cela, le fichier de docker-compose.yml de hello est disponible dans le processus de mise en production hello.

    ![Visual Studio Team Services - Artefacts de mise en production](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. déclencheur hello tooconfigure, cliquez sur **déclencheurs** et sélectionnez **déploiement continu**. Définir un déclencheur hello sur hello même source d’artefact. Ce paramètre s’assure qu’une nouvelle version démarre lorsque hello build s’effectue correctement.

    ![Visual Studio Team Services - Déclencheurs de mise en production](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. Cliquez sur les variables de version tooconfigure hello, **Variables** et sélectionnez **+ Variable** toocreate trois nouvelles variables avec des informations du Registre de hello hello : **docker.username**, **docker.password**, et **docker.registry**. Collez les valeurs hello de votre Registre et le Cluster Agents DNS.

    ![Visual Studio Team Services - Configuration du référentiel de la build](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > Comme indiqué à l’écran précédent de hello, cliquez sur hello **verrou** case à cocher dans docker.password. Ce paramètre est un mot de passe hello toorestrict important.
    >

### <a name="define-hello-release-workflow"></a>Définir le flux de travail de mise en production hello

flux de travail de mise en production Hello est composé de deux tâches que vous ajoutez.

1. Configurer un Bonjour de copie toosecurely tâche composer fichier tooa *déployer* dossier hello Docker Swarm nœud maître, à l’aide de la connexion SSH hello configurées précédemment. Hello suivant l’écran pour plus d’informations, consultez.
    
    Dossier source : ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```

    ![Visual Studio Team Services - SCP mise en production](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. Configurer une deuxième tooexecute de tâche un toorun de commande d’interpréteur de commandes `docker` et `docker stack deploy` commandes sur le nœud principal de hello. Hello suivant l’écran pour plus d’informations, consultez.

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio Team Services - Bash mise en production](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    commande Hello exécutée sur le contrôleur de hello utilise hello Docker CLI et hello de toodo CLI de Docker Compose hello tâches suivantes :

    - Ouvrez une session dans le Registre de conteneur Azure toohello (il utilise trois variables de génération qui sont définis dans hello **Variables** onglet)
    - Définir hello **DOCKER_HOST** toowork variable avec le point de terminaison hello essaim ( : 2375)
    - Accédez toohello *déployer* dossier qui a été créé par hello précédant la tâche de copie sécurisée et qui contient le fichier de docker-compose.yml hello 
    - Exécutez `docker stack deploy` commandes qui extrait les nouvelles images de hello et créer des conteneurs de hello.

    >[!IMPORTANT]
    > Comme indiqué à l’écran précédent de hello, laissez hello **échouer dans STDERR** case à cocher est désactivée. Ce paramètre permet de processus de mise en production toocomplete hello échéance trop`docker-compose` imprime plusieurs messages de diagnostic, tels que les conteneurs sont en cours de suppression sur la sortie d’erreur standard hello ou d’arrêt. Si vous activez la case à cocher hello, Visual Studio Team Services signale que les erreurs se sont produites au cours de la version de hello, même si tout se passe bien.
    >
3. Enregistrez cette nouvelle définition de mise en production.

## <a name="step-4-test-hello-cicd-pipeline"></a>Étape 4 : Tester le pipeline de l’élément de configuration/CD hello

Maintenant que vous avez terminé avec la configuration de hello, il est temps tootest de ce nouveau pipeline de l’élément de configuration/CD. tootest moyen plus simple de Hello, il est tooupdate Bonjour source code puis de valider Bonjour change dans votre référentiel GitHub. Quelques secondes après le push de code de hello, vous verrez une nouvelle build en cours d’exécution dans Visual Studio Team Services. Une fois terminé, une nouvelle version est déclenchée et déployé hello nouvelle version d’application hello sur le cluster du Service de conteneur Azure hello.

## <a name="next-steps"></a>Étapes suivantes

* Pour plus d’informations sur l’élément de configuration/CD avec Visual Studio Team Services, consultez hello [VSTS générer une vue d’ensemble](https://www.visualstudio.com/docs/build/overview).
* Pour plus d’informations sur le moteur d’ACS, consultez hello [référentiel GitHub de moteur ACS](https://github.com/Azure/acs-engine).
* Pour plus d’informations sur le mode de Docker Swarm, consultez hello [Docker Swarm une vue d’ensemble du mode](https://docs.docker.com/engine/swarm/).
