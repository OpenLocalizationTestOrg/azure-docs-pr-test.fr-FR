---
title: "aaaContinuous build et l’intégration de votre application Azure Service Fabric Linux Java à l’aide de Jenkins | Documents Microsoft"
description: "Génération et intégration en continu pour votre application Linux Java à l’aide de Jenkins"
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: 15da2cb8c759233219369ea889550da93748129f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-jenkins-toobuild-and-deploy-your-linux-java-application"></a>Utilisez Jenkins toobuild et déployer votre application Java de Linux
Jenkins est un outil populaire pour l’intégration et le déploiement en continu de vos applications. Voici comment toobuild et déployer votre application Azure Service Fabric à l’aide de Jenkins.

## <a name="general-prerequisites"></a>Conditions préalables
- Git doit être installé en local. Vous pouvez installer hello une version Git appropriée à partir de [page de téléchargements hello Git](https://git-scm.com/downloads), en fonction de votre système d’exploitation. Si vous êtes tooGit nouveau, plus d’informations à partir de hello [Git documentation](https://git-scm.com/docs).
- Avoir hello Jenkins de l’infrastructure du Service plug-in pratique. Vous pouvez le télécharger à partir des [téléchargements Service Fabric](https://servicefabricdownloads.blob.core.windows.net/jenkins/serviceFabric.hpi).

## <a name="set-up-jenkins-inside-a-service-fabric-cluster"></a>Configurer Jenkins à l’intérieur d’un cluster Service Fabric

Vous pouvez configurer Jenkins à l’intérieur ou en dehors d’un cluster Service Fabric. afficher les sections suivantes de Hello comment tooset, configurez-le à l’intérieur d’un cluster lors de l’utilisation d’un stockage Azure compte état de hello toosave de l’instance de conteneur hello.

### <a name="prerequisites"></a>Composants requis
1. Avoir un cluster Linux Service Fabric de prêt. Un cluster Service Fabric déjà créé à partir de hello portail Azure a Docker installé. Si vous exécutez localement cluster de hello, vérifiez si Docker est installé à l’aide de commande hello ``docker info``. S’il n’est pas installé, installez-le en conséquence à l’aide de hello commandes suivantes :

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```
2. Disposer d’application de conteneur de Service Fabric hello déployée sur un cluster de hello, à l’aide de hello comme suit :

  ```sh
git clone https://github.com/Azure-Samples/service-fabric-java-getting-started.git
cd service-fabric-java-getting-started/Services/JenkinsDocker/
```

3. Vous devez hello connecter des informations sur l’option de stockage Azure-partage de fichiers, de hello où vous souhaitez que l’état de hello de toopersist de l’instance de conteneur hello Jenkins. Si vous utilisez le portail de Microsoft Azure hello pour hello identiques, suivez les étapes de hello Veuillez - créer un compte de stockage Azure, par exemple ``sfjenkinsstorage1``. Créez un **partage de fichiers** sous ce compte de stockage, par exemple ``sfjenkins``. Cliquez sur **Connect** pour Bonjour Bonjour de partage de fichiers et notez les valeurs s’affichent sous **connexion à partir de Linux**, supposons que cela ressemble à :
```sh
sudo mount -t cifs //sfjenkinsstorage1.file.core.windows.net/sfjenkins [mount point] -o vers=3.0,username=sfjenkinsstorage1,password=<storage_key>,dir_mode=0777,file_mode=0777
```

4. Mettre à jour les valeurs d’espace réservé hello hello ```setupentrypoint.sh``` script avec les détails correspondants de stockage azure.
```sh
vi JenkinsSF/JenkinsOnSF/Code/setupentrypoint.sh
```
Remplacez ``[REMOTE_FILE_SHARE_LOCATION]`` avec la valeur de hello ``//sfjenkinsstorage1.file.core.windows.net/sfjenkins`` à partir de la sortie de hello Hello se connecter au point 3.
Remplacez ``[FILE_SHARE_CONNECT_OPTIONS_STRING]`` avec la valeur de hello ``vers=3.0,username=sfjenkinsstorage1,password=GB2NPUCQY9LDGeG9Bci5dJV91T6SrA7OxrYBUsFHyueR62viMrC6NIzyQLCKNz0o7pepGfGY+vTa9gxzEtfZHw==,dir_mode=0777,file_mode=0777`` à partir du point 3 ci-dessus.

5. Se connecter toohello cluster et installer l’application de conteneur hello.
```azurecli
sfctl cluster select --endpoint http://PublicIPorFQDN:19080   # cluster connect command
bash Scripts/install.sh
```
Cela installe un conteneur Jenkins sur le cluster de hello et peut être analysé à l’aide de hello Service Fabric Explorer.

### <a name="steps"></a>Étapes
1. À partir de votre navigateur, accédez trop``http://PublicIPorFQDN:8081``. Il fournit le chemin d’accès de hello de toosign de mot de passe d’administration initiale hello dans. Vous pouvez continuer toouse Jenkins en tant qu’administrateur. Ou vous pouvez créer et changer de hello, une fois que vous vous connectez avec un compte d’administration initiale hello.

   > [!NOTE]
   > Assurez-vous que le port 8081 de hello est spécifié en tant que port de point de terminaison d’application hello lors de la création d’un cluster de hello.
   >

2. Obtenir l’ID d’instance hello conteneur à l’aide de ``docker ps -a``.
3. Secure Shell (SSH) de connexion toohello conteneur et collez le chemin d’accès hello que vous ont été affichées sur le portail Jenkins hello. Par exemple, si dans le portail de hello il affiche le chemin d’accès hello `PATH_TO_INITIAL_ADMIN_PASSWORD`, exécutez hello suivante :

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash   # This takes you inside Docker shell
  cat PATH_TO_INITIAL_ADMIN_PASSWORD
  ```

4. Configurer toowork GitHub avec Jenkins, à l’aide des étapes hello indiquées dans [générer une nouvelle clé SSH et ajout de l’agent SSH toohello](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).
    * Utilisez les instructions hello fournies par la clé SSH de GitHub toogenerate hello et toohello clé tooadd hello SSH compte GitHub qui héberge votre référentiel.
    * Exécutez les commandes hello mentionnés dans hello précédant lien Bonjour shell de Jenkins Docker (et non sur votre ordinateur hôte).
    * toosign dans toohello shell Jenkins à partir de votre ordinateur hôte, hello utilisez commande suivante :

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
  ```

## <a name="set-up-jenkins-outside-a-service-fabric-cluster"></a>Configurer Jenkins en dehors d’un cluster Service Fabric

Vous pouvez configurer Jenkins à l’intérieur ou en dehors d’un cluster Service Fabric. Hello suivant sections indiquent comment tooset, configurez-le en dehors d’un cluster.

### <a name="prerequisites"></a>Composants requis
Vous devez toohave Docker installé. Hello suivant les commandes peut être utilisé tooinstall Docker à partir de hello Terminal Server :

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```

Désormais, lorsque vous exécutez ``docker info`` Bonjour Terminal Server, vous devriez voir dans la sortie de hello que hello Docker service est en cours d’exécution.

### <a name="steps"></a>Étapes
  1. Extraire l’image de conteneur de Service Fabric Jenkins hello :``docker pull raunakpandya/jenkins:v1``
  2. Exécutez l’image de conteneur hello :``docker run -itd -p 8080:8080 raunakpandya/jenkins:v1``
  3. Obtenir les ID de hello d’instance d’image de conteneur de hello. Vous pouvez répertorier tous les conteneurs de Docker hello avec la commande hello``docker ps –a``
  4. La connexion toohello Jenkins portail à l’aide de hello comme suit :

    * ```sh
    docker exec [first-four-digits-of-container-ID] cat /var/jenkins_home/secrets/initialAdminPassword
    ```
    Si l’ID du conteneur est 2d24a73b5964, utilisez 2d24.
    * Ce mot de passe est requis pour la signature dans le tableau de bord toohello Jenkins à partir du portail, ce qui est``http://<HOST-IP>:8080``
    * Après que vous être connecté pour hello première fois, vous pouvez créer votre propre compte d’utilisateur et l’utiliser pour les besoins futurs, ou vous pouvez continuer de compte d’administrateur toouse hello. Après avoir créé un utilisateur, vous devez toocontinue avec qui.
  5. Configurer toowork GitHub avec Jenkins, à l’aide des étapes hello indiquées dans [générer une nouvelle clé SSH et ajout de l’agent SSH toohello](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).
        * Utilisez les instructions hello fournies par la clé SSH de GitHub toogenerate hello et toohello clé tooadd hello SSH compte GitHub qui héberge le référentiel de hello.
        * Exécutez les commandes hello mentionnés dans hello précédant lien Bonjour shell de Jenkins Docker (et non sur votre ordinateur hôte).
      * toosign dans toohello shell Jenkins à partir de votre hôte, hello utilisation suivant de commandes :

      ```sh
      docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
      ```

Assurez-vous que le cluster de hello ou d’un ordinateur où hello image de conteneur Jenkins est hébergé a une adresse IP publique. Ainsi, les notifications de tooreceive hello Jenkins instance à partir de GitHub.

## <a name="install-hello-service-fabric-jenkins-plug-in-from-hello-portal"></a>Installer hello Jenkins de l’infrastructure du Service plug-in du portail de hello

1. Accédez trop``http://PublicIPorFQDN:8081``
2. Dans le tableau de bord hello Jenkins, sélectionnez **gérer les Jenkins** > **gérer les plug-ins** > **avancé**.
Ici, vous pouvez charger un plug-in. Sélectionnez **choisir un fichier**, puis sélectionnez hello **serviceFabric.hpi** fichier que vous avez téléchargé sous les conditions préalables. Lorsque vous sélectionnez **télécharger**, Jenkins installe automatiquement hello plug-in. Autorisez un redémarrage si nécessaire.

## <a name="create-and-configure-a-jenkins-job"></a>Créer et configurer un travail Jenkins

1. Créez un **élément** à partir du tableau de bord.
2. Entrez un nom d’élément (par exemple, **MyJob**). Sélectionnez **free-style project** (projet libre), puis cliquez sur **OK**.
3. Atteindre la page hello du travail, puis cliquez sur **configurer**.

   a. Dans la section Général de hello, sous **GitHub projet**, spécifiez l’URL de votre projet de GitHub. Cette URL hôtes hello Service Fabric application Java que vous souhaitez toointegrate avec hello intégration continue Jenkins, flux de déploiement continu (CI/CD) (par exemple, ``https://github.com/sayantancs/SFJenkins``).

   b. Sous hello **gestion du Code Source** section, sélectionnez **Git**. Spécifiez l’URL du référentiel hello qui héberge l’application de Service Fabric Java hello que vous souhaitez toointegrate avec hello Jenkins CI/CD flux (par exemple, ``https://github.com/sayantancs/SFJenkins.git``). Vous pouvez également spécifier ici le toobuild branche (par exemple, **/maître**).
4. Configurer votre *GitHub* (qui héberge hello référentiel) afin qu’il soit en mesure de tootalk tooJenkins. Utilisez hello comme suit :

   a. Atteindre la page de référentiel GitHub tooyour. Accédez trop**paramètres** > **intégrations et Services**.

   b. Sélectionnez **ajouter un Service**, type **Jenkins**et sélectionnez hello **plug-in Jenkins-GitHub**.

   c. Entrez votre URL du webhook Jenkins (par défaut, il doit être ``http://<PublicIPorFQDN>:8081/github-webhook/``). Cliquez sur **Add/Update service** (Ajouter/Mettre à jour le service).

   d. Un événement de test est envoyé tooyour Jenkins instance. Vous devez voir une coche verte en webhook hello dans GitHub, et que votre projet est généré.

   e. Sous hello **déclencheurs de Build** , sélectionnez l’option souhaitée de build. Pour cet exemple, vous souhaitez tootrigger une build chaque fois que certaines référentiel de toohello par émission de données se produit. Vous sélectionnez donc **GitHub hook trigger for GITScm polling** (Déclencher un hook GitHub pour l’interrogation GITScm). (Cette option a été appelée précédemment, **générer lorsqu’une modification est envoyée tooGitHub**.)

   f. Sous hello **section de**, dans hello de liste déroulante **étape de génération ajouter**, sélectionnez l’option de hello **appeler le Gradle Script**. Dans widget hello fourni, spécifiez le chemin d’accès de hello trop**racine générer le script** pour votre application. Il récupère build.gradle de chemin d’accès hello spécifié et fonctionne en conséquence. Si vous créez un projet nommé ``MyActor`` (à l’aide de générateur de plug-in ou Yeoman hello Eclipse), du script de compilation hello racine doit contenir ``${WORKSPACE}/MyActor``. Consultez hello suivant capture d’écran pour obtenir un exemple de quoi cela ressemble :

    ![Action de génération Jenkins de Service Fabric][build-step]

   g. À partir de hello **post-Build Actions** liste déroulante, sélectionnez **déployer un projet de l’infrastructure de Service**. Ici, vous devez cluster tooprovide détails où hello Jenkins compilé application Service Fabric sont déployées. Vous pouvez également fournir les détails supplémentaires de l’application utilisée application hello de toodeploy. Consultez hello suivant capture d’écran pour obtenir un exemple de quoi cela ressemble :

    ![Action de génération Jenkins de Service Fabric][post-build-step]

   > [!NOTE]
   > cluster Hello ici peut être identique à Bonjour Bonjour hébergement une application conteneur de Jenkins, au cas où vous utilisez une image de conteneur de Service Fabric toodeploy hello Jenkins.
   >

## <a name="next-steps"></a>Étapes suivantes
GitHub et Jenkins sont maintenant configurés. Envisagez de rendre certains exemples de modification dans votre ``MyActor`` projet dans l’exemple de référentiel hello, https://github.com/sayantancs/SFJenkins. Push votre tooa modifications distant ``master`` branche (ou n’importe quelle branche que vous avez configuré toowork avec). Cela déclenche la tâche de Jenkins hello, ``MyJob``, que vous avez configuré. Il extrait les modifications hello à partir de GitHub, les génère et déploie hello application toohello cluster point de terminaison spécifié dans les actions de post-build.  

  <!-- Images -->
  [build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/build-step.png
  [post-build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/post-build-step.png
