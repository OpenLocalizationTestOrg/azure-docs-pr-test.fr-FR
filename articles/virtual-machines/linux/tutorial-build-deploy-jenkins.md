---
title: aaaCI/CD de Jenkins tooAzure machines virtuelles avec Team Services | Documents Microsoft
description: "Configurer l’intégration continue (CI) et le déploiement continu (CD) d’une application Node.js à l’aide de machines virtuelles de tooAzure Jenkins à partir de la gestion des versions dans Visual Studio Team Services (VSTS) ou Microsoft Team Foundation Server (TFS)"
author: ahomer
manager: douge
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/15/2017
ms.author: ahomer
ms.custom: mvc
ms.openlocfilehash: 400ae34cbdf45da65351811c0ff6ff5d61ef862c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-toolinux-vms-using-jenkins-and-team-services"></a>Déployer votre application de tooLinux machines virtuelles à l’aide de Jenkins et Team Services

L’intégration continue (CI) et le déploiement continu (CD) constituent un pipeline via lequel vous pouvez générer, mettre en production et déployer votre code. Team Services fournit un ensemble de CD de l’élément de configuration/Outils d’automatisation complète et complet pour tooAzure de déploiement. Jenkins est un outil serveur CI/CD tiers populaire qui propose également l’automatisation CI/CD. Vous pouvez utiliser les deux ensemble toocustomize comment livrer votre application cloud ou le service.

Dans ce didacticiel, vous utilisez Jenkins toobuild un **application web Node.js**et Visual Studio Team Services toodeploy il tooa [groupe de déploiement](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) contenant des ordinateurs virtuels Linux.

Vous allez :

> [!div class="checklist"]
> * Générer votre application dans Jenkins
> * Configurer Jenkins pour l’intégration Team Services
> * Créer un groupe de déploiement hello pour les machines virtuelles
> * Créer une définition de mise en production qui configure les ordinateurs virtuels de hello et déploie l’application hello

## <a name="before-you-begin"></a>Avant de commencer

* Vous devez le compte d’accès tooa Jenkins. Si vous n’avez pas encore créé de serveur Jenkins, consultez la [documentation Jenkins](https://jenkins.io/doc/). 

* Connectez-vous à tooyour compte Team Services (`https://{youraccount}.visualstudio.com`). 
  Vous pouvez obtenir un [compte Team Services gratuit](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).

  > [!NOTE]
  > Pour plus d’informations, consultez [connecter les Services de tooTeam](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).

* Créez un jeton d’accès personnel (PAT) dans votre compte Team Services si vous n’en avez pas encore. Jenkins requiert cette tooaccess informations de votre compte Team Services.
  Lecture [comment créer un jeton d’accès personnel pour Team Services et TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn comment toogenerate une.

## <a name="get-hello-sample-app"></a>Obtenir l’exemple d’application hello

Vous avez besoin d’un toodeploy d’application stocké dans un référentiel Git.
Pour ce didacticiel, nous vous recommandons d’utiliser [cet exemple d’application disponible sur GitHub](https://github.com/azooinmyluggage/fabrikam-node).

1. Créer une branche de cette application et notez hello emplacement (URL) pour une utilisation dans les étapes ultérieures de ce didacticiel.

1. Vérifiez le branchement de hello **public** toosimplify vous tooGitHub plus tard.

> [!NOTE]
> Pour plus d’informations, consultez [Fork A Repo](https://help.github.com/articles/fork-a-repo/) (Dupliquer un référentiel)et [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/) (Rendre public un référentiel privé).

> [!NOTE]
> application Hello a été générée à l’aide de [Yeoman](http://yeoman.io/learning/index.html); elle utilise **Express**, **bower**, et **grunt**; et qu’il a certaines **npm**packages en tant que dépendances.
> Hello, exemple d’application contient un ensemble de [modèles Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) que sont toodynamically utilisé créer des machines virtuelles de hello pour le déploiement sur Azure. Ces modèles sont utilisés par des tâches de hello [Team Services version définition](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).
> les modèles principal Hello crée un groupe de sécurité réseau, un ordinateur virtuel et un réseau virtuel. Il attribue une adresse IP publique et ouvre le port 80 entrant. Il ajoute également une balise qui est utilisée par hello groupe hello trop sélectionnez machines tooreceive hello un déploiement.
>
> exemple Hello contient également un script qui configure Nginx et déploie l’application hello. Il est exécuté sur chacun des ordinateurs virtuels hello. Plus précisément, le script de hello installe nœud Nginx et PM2 ; Configure Nginx et PM2 ; démarre ensuite l’application de nœud hello.

## <a name="configure-jenkins-plugins"></a>Configurer les plug-ins Jenkins

Tout d’abord, vous devez configurer deux plug-ins Jenkins pour **NodeJS** et **l’intégration avec Team Services**.

1. Ouvrez votre compte Jenkins et choisissez **Manage Jenkins** (Gérer Jenkins).

1. Bonjour **gérer les Jenkins** choisissez **gérer les plug-ins**.

1. Filtre Bonjour liste toolocate Bonjour **NodeJS** plug-in et l’installer sans redémarrage.

   ![Ajout de hello NodeJS plug-in tooJenkins](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. Filtre Bonjour liste toofind Bonjour **Team Foundation Server** plug-in et l’installer. (Ce plug-in fonctionne pour Team Services et Team Foundation Server.) Le redémarrage de Jenkins n’est pas nécessaire.

## <a name="configure-jenkins-build-for-nodejs"></a>Configurer la génération Jenkins pour Node.js

Dans Jenkins, créez un projet de génération et configurez-le comme suit :

1. Bonjour **général** , entrez un nom pour votre projet de build.

1. Bonjour **gestion du Code Source** onglet, sélectionnez **Git** et entrez les détails de hello du référentiel de hello et de branche hello contenant le code de votre application.

   ![Ajouter une build tooyour de référentiel](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > Si votre référentiel n’est pas public, choisissez **ajouter** et fournir des informations d’identification tooconnect tooit.

1. Bonjour **déclencheurs de Build** onglet, sélectionnez **interrogation SCM** et entrez la planification de hello `H/03 * * * *` référentiel Git toopoll hello modifications toutes les trois minutes. 

1. Bonjour **environnement Build** onglet, sélectionnez **fournissent un nœud &amp; npm bin / chemin d’accès de dossier** et entrez `NodeJS` pour hello valeur du nœud JS Installation. Laissez **npmrc file** (fichier npmrc) défini sur « utiliser les valeurs par défaut du système ».

1. Bonjour **générer** , entrez la commande hello `npm install` tooensure toutes les dépendances sont mises à jour.

## <a name="configure-jenkins-for-team-services-integration"></a>Configurer Jenkins pour l’intégration Team Services

1. Bonjour **post-build Actions** onglet, pour **tooarchive de fichiers**, entrez `**/*` tooinclude tous les fichiers.

1. Pour **déclencher la mise en production dans TFS/Team Services**, entrer une URL complète de votre compte hello (tel que `https://your-account-name.visualstudio.com`), hello nom du projet, un nom pour la définition de la version hello (créé ultérieurement), et hello des informations d’identification tooconnect tooyour compte.
   Vous avez besoin de votre nom d’utilisateur et le hello PAT que vous avez créé précédemment. 

   ![Configuration des actions post-génération Jenkins](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. Enregistrez le projet de build hello.

## <a name="create-a-jenkins-service-endpoint"></a>Créer un point de terminaison de service Jenkins

Un point de terminaison de service permet de tooJenkins de tooconnect Team Services.

1. Ouvrez hello **Services** page Team Services, ouvrez hello **nouveau point de terminaison de Service** liste, puis choisissez **Jenkins**.

   ![Ajouter un point de terminaison Jenkins](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. Entrez un nom que vous utiliserez toorefer toothis connexion.

1. Entrez l’URL de hello de votre serveur Jenkins et graduations hello **accepter les certificats SSL non fiables** option.

1. Entrez le nom d’utilisateur hello et le mot de passe pour votre compte Jenkins.

1. Choisissez **vérifier connexion** toocheck qui hello informations est correct.

1. Choisissez **OK** point de terminaison de service toocreate hello.

## <a name="create-a-deployment-group"></a>Créer un groupe de déploiement

Vous avez besoin une [groupe de déploiement](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) contiennent trop de machines virtuelles de hello.

1. Ouvrez hello **versions** onglet Hello **générer &amp; version** concentrateur, puis ouvrez hello **groupes de déploiement** onglet, puis choisissez **+ nouveau**.

1. Entrez un nom pour le groupe de déploiement hello et une description facultative.
   Sélectionnez ensuite **Créer**.

tâche de déploiement de groupe de ressources Azure Hello crée et enregistre les machines virtuelles de hello lorsqu’elle s’exécute à l’aide du modèle de gestionnaire de ressources Azure hello.
Vous ne devez toocreate et inscrire des machines virtuelles de hello vous-même.

## <a name="create-a-release-definition"></a>Création d’une définition de version

Une définition de mise en production Spécifie le processus hello Team Services exécutera toodeploy hello application.
définition de mise en production toocreate hello dans Team Services :

1. Ouvrez hello **versions** onglet Hello **générer &amp; Release** hub, ouvrez hello  **+**  liste déroulante dans la liste hello des définitions de version, puis choisissez Hello **définition de créer la version**. 

1. Sélectionnez hello **vide** modèle et choisissez **suivant**.

1. Bonjour **artefacts** section, cliquez sur **lier un artefact** et choisissez **Jenkins**. Sélectionnez votre connexion de point de terminaison de service Jenkins. Sélectionnez le projet source de Jenkins hello ensuite et choisissez **créer**. 

1. Bonjour nouvelles release définition, choisissez **+ ajouter des tâches** et ajoutez un **déploiement de groupe de ressources Azure** toohello de l’environnement par défaut de tâche.

1. Choisissez hello déroulante toohello suivant de flèche **+ ajouter des tâches** lier et ajoutez une définition de déploiement groupe phase toohello.

   ![Ajout d’une phase de groupe de déploiement](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. Dans le catalogue de tâche hello, ouvrez hello **utilitaire** section et ajoutez une instance de hello **Script Shell** tâche.

1. modèle de paramètres de Hello utilisé dans la tâche de déploiement de groupe de ressources Azure hello définit hello admin avec le mot de passe utilisé tooconnect toohello machines virtuelles.
   Vous fournissez ce mot de passe avec la variable de hello **$(adminpassword)**:
   
   - Ouvrez hello **Variables** onglet et hello **Variables** section, entrez le nom de hello `adminpassword`.

   - Entrez le mot de passe administrateur hello.

   - Choisissez hello cadenas » en » icône suivant toohello valeur textbox tooprotect hello mot de passe. 

## <a name="configure-hello-azure-resource-group-deployment-task"></a>Configurer la tâche de déploiement de groupe de ressources Azure hello

Hello **déploiement de groupe de ressources Azure** tâche est le groupe de déploiement hello toocreate utilisé. Configurez-le comme suit :

* **Abonnement Azure :** sélectionner une connexion à partir de la liste de hello sous **des connexions de Service Azure disponibles**. 
  Si aucune connexion n’apparaît, choisissez **gérer**, sélectionnez **nouveau point de terminaison de Service** puis **Azure Resource Manager**et suivez les invites hello.
  Retourner tooyour hello d’actualisation, définition de la version **AzureRM abonnement** liste et la connexion hello sélectionnez vous avez créé.

* **Groupe de ressources**: entrez un nom de groupe de ressources hello vous avez créé précédemment.

* **Emplacement**: sélectionnez une région pour le déploiement de hello.

  ![Création d’un groupe de ressources](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* **Emplacement du modèle** : `URL of hello file`

* **Lien du modèle** : `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`

* **Lien des paramètres de modèle** : `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`

* **Remplacer les paramètres de modèle**: une liste de hello remplacer des valeurs, par exemple : `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.<br />Insérez vos propres valeurs spécifiques pour hello {des espaces réservés}. 

* **Activer les prérequis** : `Configure with Deployment Group agent`

* **Point de terminaison TFS/VSTS**: choisissez **ajouter** et, dans le dialogue de « Ajouter la nouvelle connexion de Services de serveur/équipe Team Foundation » hello, sélectionnez **authentification jeton**. Entrez un nom de connexion de hello et URL hello de votre projet d’équipe. Générer, puis entrez un [personnel Access jeton (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) projet d’équipe tooyour tooauthenticate hello connexion.

  ![Créer un jeton d’accès personnel](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* **Projet d’équipe** : sélectionnez votre projet actuel.

* **Groupe de déploiement**: entrez hello le même nom de groupe de déploiement que vous avez utilisé pour hello **groupe de ressources** paramètre.

paramètres par défaut de Hello pour la tâche de déploiement de groupe de ressources Azure hello sont toocreate ou mise à jour d’une ressource et toodo donc incrémentielle. tâche Hello crée hello de machines virtuelles hello première fois qu’elle s’exécute, les mettre à jour par la suite uniquement.

## <a name="configure-hello-shell-script-task"></a>Configurer la tâche de Script Shell hello

Hello **Script Shell** tâche est configuration de hello tooprovide utilisés pour un toorun de script sur chaque serveur tooinstall Node.js et démarrer hello d’application. Configurez-le comme suit :

* **Chemin d’accès au script** : `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`

* **Spécifier le répertoire de travail** : `Checked`

* **Répertoire de travail** : `$(System.DefaultWorkingDirectory)/Fabrikam-Node`
   
## <a name="rename-and-save-hello-release-definition"></a>Renommer et enregistrer la définition de la version hello

1. Modifier le nom hello hello version de définition de toohello vous avez spécifié dans le **post-build Actions** onglet de build Jenkins hello. Jenkins requiert cette tootrigger en mesure de nom toobe une nouvelle version mise à jour des artefacts de code source hello.

1. Modifiez éventuellement le nom hello d’environnement de hello en cliquant sur le nom de hello. 

1. Choisissez **Enregistrer**, puis **OK**.

## <a name="start-a-manual-deployment"></a>Démarrer un déploiement manuel

1. Choisissez **+ Mise en production** et sélectionnez **Créer une mise en production**.

1. Sélectionnez la build hello vous terminé dans la liste déroulante de la mise en surbrillance hello et choisissez **créer**.

1. Choisissez le lien de mise en production de hello dans un message contextuel hello. Par exemple : « Mise en production **Mise en production-1** a été créé. ».

1. Ouvrez hello **journaux** onglet sortie de la console toowatch hello mise en production.

1. Dans votre navigateur, ouvrez hello URL de l’un des serveurs de hello, vous avez ajouté le groupe de déploiement tooyour. Par exemple, entrez `http://{your-server-ip-address}`.

## <a name="start-a-cicd-deployment"></a>Démarrer un déploiement CI/CD

1. Bonjour, lancez définition, décochez la case hello **activé** case à cocher Bonjour **contrôler les Options de** section des paramètres de hello pour la tâche de déploiement de groupe de ressources Azure hello.
   Pour les déploiements futurs toohello déploiement groupe existant, vous n’avez pas besoin de toore-exécuter cette tâche.

1. Référentiel Git de source toohello et modifiez le contenu de hello Hello **h1** en-tête dans le fichier de hello [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).

1. Validez votre modification.

1. Après quelques minutes, vous verrez une nouvelle version créée Bonjour **versions** page des Services d’équipe TFS. Ouvrez hello toosee hello déploiement se produisent. Félicitations !

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez automatisé déploiement hello d’un tooAzure d’application à l’aide de la build Jenkins et Team Services pour cette version. Vous avez appris à effectuer les actions suivantes :

> [!div class="checklist"]
> * Générer votre application dans Jenkins
> * Configurer Jenkins pour l’intégration Team Services
> * Créer un groupe de déploiement hello pour les machines virtuelles
> * Créer une définition de mise en production qui configure les ordinateurs virtuels de hello et déploie l’application hello

Avance toolearn de didacticiel suivant toohello plus d’informations sur la façon dont la pile toodeploy un feu (Linux, Apache, MySQL et PHP).

> [!div class="nextstepaction"]
> [Déploiement d’une pile LAMP dans Azure](tutorial-lamp-stack.md)