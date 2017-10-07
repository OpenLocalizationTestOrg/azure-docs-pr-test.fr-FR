---
title: aaaCI/CD avec le Service de conteneur Azure et essaim | Documents Microsoft
description: Utiliser le Service de conteneur Azure avec Docker Swarm un Registre de conteneur Azure et Visual Studio Team Services toodeliver en permanence une application de .NET Core multi conteneur
services: container-service
documentationcenter: " "
author: jcorioland
manager: pierlag
tags: acs, azure-container-service
keywords: Docker, conteneurs, micro-services, Swarm, Azure, Visual Studio Team Services, DevOps
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/08/2016
ms.author: jucoriol
ms.custom: mvc
ms.openlocfilehash: 35348800aa620469fb62ab3e5a02b33834359446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a>/ CD complète de l’élément de configuration de pipeline toodeploy une application conteneur multi Azure Service de conteneur avec Docker Swarm à l’aide de Visual Studio Team Services

Un des hello plus grands défis lors de développement d’applications modernes pour le cloud de hello toodeliver en mesure de ces applications en continu. Dans cet article, vous découvrez comment tooimplement une intégration complète continue et le pipeline de déploiement (élément de configuration/CD) à l’aide du Service de conteneur Azure avec Docker Swarm, Registre de conteneur Azure et Visual Studio Team Services de génération et gestion des versions.

Cet article est basé sur une application simple, disponible sur [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), développée avec ASP.NET Core. application Hello est composée de quatre services différents : trois web API et un site web frontal :

![Exemple d’application MyShop](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

objectif de Hello est toodeliver cette application en continu dans un cluster de Docker Swarm, à l’aide de Visual Studio Team Services. la figure suivant de Hello détails ce pipeline de livraison continue :

![Exemple d’application MyShop](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

Voici une brève explication des étapes de hello :

1. Modifications du code sont validées toohello référentiel de code source (ici, GitHub) 
2. GitHub déclenche une build dans Visual Studio Team Services. 
3. Obtient la version la plus récente de sources de hello hello de Visual Studio Team Services et génère toutes les images hello qui composent l’application hello 
4. Visual Studio Team Services transmet chaque registre Docker de tooa image créé à l’aide du service de Registre de conteneur Azure hello 
5. Visual Studio Team Services déclenche une nouvelle mise en production. 
6. version de Hello exécute des commandes à l’aide de SSH sur le nœud principal du cluster service conteneur Azure hello 
7. Essaim docker sur hello cluster extrait hello version la plus récente des images de hello 
8. Hello nouvelle version d’application hello est déployée à l’aide de Docker Compose 

## <a name="prerequisites"></a>Composants requis

Avant de commencer ce didacticiel, vous devez hello toocomplete tâches suivantes :

- [Création d’un cluster Swarm dans Azure Container Service](container-service-deployment.md)
- [Se connecter à un cluster d’essaim hello dans le conteneur de Service Azure](../container-service-connect.md)
- [Utilisation d’un Registre de conteneurs Azure](../../container-registry/container-registry-get-started-portal.md)
- [Création d’un compte et d’un projet d’équipe Visual Studio Team Services](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [Effectuer un branchement tooyour de référentiel GitHub hello compte GitHub](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

Vous devez également posséder un ordinateur Ubuntu (14.04 ou 16.04) avec Docker installé. Cet ordinateur est utilisé par Visual Studio Team Services pendant hello générer et lancer le processus. Une façon toocreate cet ordinateur est l’image de hello toouse disponible dans hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/). 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a>Étape 1 : configuration de votre compte Visual Studio Team Services 

Dans cette section, vous allez configurer votre compte Visual Studio Team Services.

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a>Configuration d’un agent de build Linux Visual Studio Team Services

toocreate Docker images et push que générer de ces images dans un Registre de conteneur Azure à partir d’un Visual Studio Team Services, vous devez tooregister un agent Linux. Vous avez le choix entre les options d’installation suivantes :

* [Déploiement d’un agent sur Linux](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [Utilisez l’agent de Docker toorun hello VSTS](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-hello-docker-integration-vsts-extension"></a>Installation de l’extension de Docker intégration VSTS hello

Microsoft fournit une extension VSTS toowork avec Docker dans la build et libérer des processus. Cette extension est disponible dans hello [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker). Cliquez sur **installer** tooadd ce compte VSTS tooyour extension :

![Installer hello intégration de Docker](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

Vous êtes invité compte VSTS tooyour tooconnect à l’aide de vos informations d’identification. 

### <a name="connect-visual-studio-team-services-and-github"></a>Connexion entre Visual Studio Team Services et GitHub

Configurez une connexion entre votre projet VSTS et votre compte GitHub.

1. Dans votre projet Visual Studio Team Services, cliquez sur hello **paramètres** icône dans la barre d’outils hello, puis sélectionnez **Services**.

    ![Visual Studio Team Services - Connexion externe](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. Sur hello gauche, cliquez sur **nouveau point de terminaison de Service** > **GitHub**.

    ![Visual Studio Team Services - GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. toowork VSTS tooauthorize avec votre compte GitHub, cliquez sur **Authorize** et suivez la procédure hello dans la fenêtre hello qui s’ouvre.

    ![Visual Studio Team Services - Autoriser GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-tooyour-azure-container-registry-and-azure-container-service-cluster"></a>Se connecter du Registre de conteneur Azure VSTS tooyour et cluster du Service de conteneur Azure

dernières étapes de Hello avant d’entrer dans le pipeline de l’élément de configuration/CD hello sont Registre de conteneur tooyour tooconfigure connexions externes et de votre cluster Docker Swarm dans Azure. 

1. Bonjour **Services** paramètres de votre projet Visual Studio Team Services, ajouter un point de terminaison de type **Docker Registre**. 

2. Dans le menu contextuel hello qui s’ouvre, entrez l’URL de la hello et les informations d’identification hello du Registre de votre conteneur Azure.

    ![Visual Studio Team Services - Registre Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. Pour le cluster de Docker Swarm hello, ajoutez un point de terminaison de type **SSH**. Puis entrez les informations de connexion SSH hello de votre cluster essaim.

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

La configuration hello est effectuée maintenant. Dans les étapes suivantes hello, créer pipeline de l’élément de configuration/CD hello qui génère et déploie hello application toohello Docker Swarm cluster. 

## <a name="step-2-create-hello-build-definition"></a>Étape 2 : Créer la définition de build hello

Dans cette étape, vous configurer un definitionfor de génération de votre projet VSTS et définissez le flux de travail de build hello pour vos images de conteneur

### <a name="initial-definition-setup"></a>Configuration de la définition initiale

1. toocreate une définition de build, connecter tooyour Visual Studio Team Services projet, puis cliquez sur **générer & version**. 

2. Bonjour **des définitions de Build** , cliquez sur **+ nouveau**. Sélectionnez hello **vide** modèle.

    ![Visual Studio Team Services - Nouvelle définition de build](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. Configurer la nouvelle version de hello avec une source de référentiel GitHub, vérification **intégration continue**et la file d’attente de l’agent hello sélectionnez où vous avez inscrit votre agent Linux. Cliquez sur **créer** toocreate hello la définition de build.

    ![Visual Studio Team Services - Création de la définition de build](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. Sur hello **définitions de Build** page, ouvrez d’abord hello **référentiel** onglet et configurer le branchement de hello toouse hello build de projet MyShop hello que vous avez créé dans les conditions préalables de hello. Assurez-vous que vous sélectionnez *acs-documents* comme hello **branche par défaut**.

    ![Visual Studio Team Services - Configuration du référentiel de la build](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. Sur hello **déclencheurs** , onglet de la configurer hello build toobe est déclenchée après chaque validation. Sélectionnez **Intégration continue** et **Modifications par lots**.

    ![Visual Studio Team Services - Configuration du déclencheur de la build](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-hello-build-workflow"></a>Définir le flux de travail de build hello
les étapes suivantes Hello définissent des flux de travail de build hello. Il existe cinq toobuild d’images de conteneur pour hello *MyShop* application. Chaque image est générée à l’aide de hello que dockerfile situé dans des dossiers du projet hello :

* ProductsApi
* Proxy
* RatingsApi
* RecommandationsApi
* ShopFront

Vous devez tooadd deux étapes de Docker pour chaque image, une image de hello toobuild et une image de hello toopush dans le Registre de conteneur Azure hello. 

1. tooadd une étape dans le flux de travail hello, cliquez sur **+ ajouter une étape build** et sélectionnez **Docker**.

    ![Visual Studio Team Services - Ajout d’étapes de build](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. Pour chaque image, configurez une seule étape qui utilise hello `docker build` commande.

    ![Visual Studio Team Services - Build Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    Opération de génération pour hello, sélectionnez votre Registre conteneur Azure, hello **générer une image** action et hello Dockerfile qui définit chaque image. Ensemble hello **contexte de génération** comme hello Dockerfile répertoire racine et définir hello **nom de l’Image**. 
    
    Comme indiqué dans le hello précédant l’écran, démarrez nom de l’image hello avec hello URI de votre Registre de conteneur Azure. (Vous pouvez également utiliser une balise de hello tooparameterize variable génération d’image hello, comme l’identificateur de build hello dans cet exemple).

3. Pour chaque image, configurer une deuxième étape qui utilise hello `docker push` commande.

    ![Visual Studio Team Services - Envoi du fichier Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    Pour une opération de diffusion hello, sélectionnez votre Registre conteneur Azure, hello **de pousser une image** action, puis entrez hello **nom de l’Image** qui est généré à l’étape précédente de hello.

4. Après avoir configuré la génération de hello et distribuer les étapes pour chacune des images de cinq hello, ajoutez que deux étapes plus Bonjour générer des flux de travail.

    a. Une tâche de ligne de commande qui utilise un Bonjour tooreplace du script bash *BuildNumber* occurrence dans le fichier docker-compose.yml hello hello actuel générer ID. Hello suivant l’écran pour plus d’informations, consultez.

    ![Visual Studio Team Services - Mise à jour du fichier Compose](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    b. Une tâche qui supprime hello mis à jour le fichier de message en tant qu’un artefact de build il peut être utilisé dans la version de hello. Hello suivant l’écran pour plus d’informations, consultez.

    ![Visual Studio Team Services - Publication du fichier Compose](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. Cliquez sur **Enregistrer** et affectez un nom à votre définition de build.

## <a name="step-3-create-hello-release-definition"></a>Étape 3 : Créer la définition de la version hello

Visual Studio Team Services vous permet de trop[gérer les versions dans des environnements](https://www.visualstudio.com/team-services/release-management/). Vous pouvez activer toomake déploiement continu sûr que votre application est déployée sur vos environnements différents (par exemple, le développement, test, préproduction et production) de façon fluide. Vous pouvez créer un nouvel environnement qui représente votre cluster Docker Swarm Azure Container Service.

![Visual Studio Team Services - version tooACS](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a>Configuration de la mise en production initiale

1. toocreate une définition de la mise en production, cliquez sur **versions** > **+ Release**

2. source d’artefact tooconfigure hello, cliquez sur **artefacts** > **lier une source d’artefact**. Ici, lier cette nouvelle définition toohello version Release que vous avez définie à l’étape précédente de hello. Ce faisant, fichier de docker-compose.yml hello est disponible dans le processus de mise en production hello.

    ![Visual Studio Team Services - Artefacts de mise en production](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. déclencheur hello tooconfigure, cliquez sur **déclencheurs** et sélectionnez **déploiement continu**. Définir un déclencheur hello sur hello même source d’artefact. Ce paramètre s’assure qu’une nouvelle version démarre dès qu’hello build s’effectue correctement.

    ![Visual Studio Team Services - Déclencheurs de mise en production](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-hello-release-workflow"></a>Définir le flux de travail de mise en production hello

flux de travail de mise en production Hello est composé de deux tâches que vous ajoutez.

1. Configurer un Bonjour de copie toosecurely tâche composer fichier tooa *déployer* dossier hello Docker Swarm nœud maître, à l’aide de la connexion SSH hello configurées précédemment. Hello suivant l’écran pour plus d’informations, consultez.

    ![Visual Studio Team Services - SCP mise en production](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. Configurer une deuxième tooexecute de tâche un toorun de commande d’interpréteur de commandes `docker` et `docker-compose` commandes sur le nœud principal de hello. Hello suivant l’écran pour plus d’informations, consultez.

    ![Visual Studio Team Services - Bash mise en production](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    commande Hello exécutée sur Bonjour utilisez master Bonjour Docker CLI et hello de toodo CLI de Docker Compose hello tâches suivantes :

    - Registre de conteneur Azure connexion toohello (il utilise trois variab'les de génération qui sont définis dans hello **Variables** onglet)
    - Définir hello **DOCKER_HOST** toowork variable avec le point de terminaison hello essaim ( : 2375)
    - Accédez toohello *déployer* dossier qui a été créé par hello précédant la tâche de copie sécurisée et qui contient le fichier de docker-compose.yml hello 
    - Exécutez `docker-compose` commandes qui extrait les nouvelles images de hello, arrêter les services de hello, supprimez les services hello et créer des conteneurs de hello.

    >[!IMPORTANT]
    > Comme indiqué dans le hello précédant l’écran, laissez hello **échouer dans STDERR** case à cocher est désactivée. Ceci est un paramètre important, car `docker-compose` imprime plusieurs messages de diagnostic, tels que les conteneurs sont en cours de suppression sur la sortie d’erreur standard hello ou d’arrêt. Si vous activez la case à cocher hello, Visual Studio Team Services signale que les erreurs se sont produites au cours de la version de hello, même si tout se passe bien.
    >
3. Enregistrez cette nouvelle définition de mise en production.


>[!NOTE]
>Ce déploiement inclut un temps d’arrêt, car nous sommes l’arrêt des services d’ancien hello et en cours d’exécution hello nouveau. Il est possible de tooavoid cela en effectuant un déploiement bleu-vert.
>

## <a name="step-4-test-hello-cicd-pipeline"></a>Étape 4. Tester le pipeline de l’élément de configuration/CD hello

Maintenant que vous avez terminé avec la configuration de hello, il est temps tootest de ce nouveau pipeline de l’élément de configuration/CD. tootest moyen plus simple de Hello, il est tooupdate Bonjour source code puis de valider Bonjour change dans votre référentiel GitHub. Quelques secondes après le push de code de hello, vous verrez une nouvelle build en cours d’exécution dans Visual Studio Team Services. Une fois terminé, une nouvelle version est déclenchée et déploiera hello nouvelle version d’application hello sur le cluster du Service de conteneur Azure hello.

## <a name="next-steps"></a>Étapes suivantes

* Pour plus d’informations sur l’élément de configuration/CD avec Visual Studio Team Services, consultez hello [VSTS générer une vue d’ensemble](https://www.visualstudio.com/docs/build/overview).
