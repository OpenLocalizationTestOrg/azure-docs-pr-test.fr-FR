---
title: "une application de démarrage du ressort comme un conteneur Docker à l’aide d’aaaPublish hello boîte à outils Azure pour IntelliJ | Documents Microsoft"
description: "Découvrez comment toopublish un tooMicrosoft d’application web Azure comme un conteneur Docker à l’aide de hello boîte à outils Azure pour IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/21/2017
ms.author: robmcm
ms.openlocfilehash: 8964cb33fd8f61a39f091633ae9074d9658232fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a>Publier une application de démarrage du ressort comme un conteneur Docker à l’aide de hello boîte à outils Azure pour IntelliJ

Hello [Spring Framework] est une solution open source qui permet aux développeurs Java de créer des applications d’entreprise. Un des projets plus-populaires hello qui est créé de plateforme est [ressort démarrage], qui fournit une approche simplifiée pour la création d’applications Java autonome.

[Docker] est une solution open source qui permet aux développeurs d’automatiser hello déploiement, mise à l’échelle et la gestion de leurs applications qui s’exécutent dans des conteneurs.

Ce didacticiel vous guide hello étapes toodeploy une application de démarrage du ressort comme un tooMicrosoft du conteneur Docker Azure à l’aide de hello boîte à outils Azure pour IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repo"></a>Cloner hello par défaut ressort démarrage Docker référentiel

Hello étapes suivantes vous guident le clonage du référentiel du ressort démarrage Docker hello à l’aide de IntelliJ. Si vous souhaitez toouse une ligne de commande, consultez [déployer une application de démarrage du ressort sur Linux dans le Service de conteneur Azure][Deploy Spring Boot on Linux in ACS].

1. Ouvrez IntelliJ.

1. Sur l’écran d’accueil hello, sélectionnez hello **GitHub** option Bonjour **extraire du contrôle de Version** liste.

   ![Option GitHub pour le contrôle de version][CL01]

1. Entrez vos informations d’identification si vous êtes invité à toolog dans.

   * Si vous utilisez un nom d’utilisateur/mot de passe toolog dans tooGitHub :

      ![Boîte de dialogue pour la saisie du nom d’utilisateur et du mot de passe GitHub][CL02a]

   * Si vous utilisez un jeton toolog dans tooGitHub :

      ![Boîte de dialogue pour la saisie d’un jeton GitHub][CL02b]

1. Entrez **https://github.com/spring-guides/gs-spring-boot-docker.git** pour l’URL de référentiel hello, spécifiez le chemin d’accès local et les informations de dossier, puis cliquez sur **Clone**.

   ![Boîte de dialogue Cloner le référentiel][CL03]

1. Lorsque vous êtes invité à entrer toocreate un projet IntelliJ, sélectionnez **non**.

   ![Refus toocreate un projet IntelliJ][CL04]

1. Dans la page d’accueil hello, cliquez sur **projet d’importation**.

   ![Choix d’importer un projet][CL05]

1. Localiser hello le chemin où vous avez cloné le dépôt de démarrage du ressort hello, sélectionnez hello **complète** dossier sous la racine de hello, puis cliquez sur **OK**.

   ![Sélectionner un dossier pour l’importation][CL06]

1. Lorsque vous y êtes invité, sélectionnez **Create project from existing sources** (Créer un projet à partir de sources existantes).

   ![Option toocreate un projet à partir de sources existantes][CL07]

1. Spécifiez le nom de votre projet ou accepter la valeur par défaut de hello, vérifiez toohello de chemin d’accès correct hello **complète** dossier, puis cliquez sur **suivant**.

   ![Spécifiez le nom du projet hello][CL08]

1. Personnalisez les répertoires pour l’importation, puis cliquez sur **Next**.

   ![Choisir des répertoires][CL09]

1. Passez en revue les hello bibliothèques tooimport, puis cliquez sur **suivant**.

   ![Passer en revue les bibliothèques de projet][CL10]

1. Passez en revue la structure de module hello, puis cliquez sur **suivant**.

   ![Passer en revue la structure des modules][CL11]

1. Spécifiez votre JDK, puis cliquez sur **Next**.

   ![Spécifier un JDK][CL12]

1. Cliquez sur **Terminer**.

   ![Bouton Terminer][CL13]

IntelliJ importe l’application de démarrage du ressort hello en tant que projet et affiche la structure de hello lors de l’importation du hello est terminée.

![Application Spring Boot dans IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a>Générer votre application Spring Boot

### <a name="build-hello-app-by-using-hello-maven-pom"></a>Générer l’application hello à l’aide de hello POM Maven

1. Ouvrez la fenêtre d’outil hello Maven s’il n’est pas déjà ouvert. Cliquez sur **View (Affichage)** > **Tool Windows (Fenêtre Outil)** > **Maven Projects (Projets Maven)**.

   ![Commandes Fenêtres Outil et Projets Maven][BU01]

1. Dans la fenêtre outil de Maven hello, cliquez sur **package** et sélectionnez **exécuter la Build Maven**. (Si votre projet Maven ne s’affiche pas automatiquement, cliquez sur hello **réimporter** icône sur la barre d’outils de Maven hello.)

   ![Commande Run Maven Build][BU02]

1. Une fois votre application Spring Boot créée, IntelliJ doit afficher le message **BUILD SUCCESS** (GÉNÉRATION RÉUSSIE).

   ![Message BUILD SUCCESS][BU03]

### <a name="create-a-deployment-ready-artifact"></a>Créer un artefact prêt pour le déploiement

toopublish votre application de démarrage du ressort, vous devez toocreate un artefact prêts pour le déploiement. Utilisez hello comme suit :

1. Ouvrez votre projet d’application web dans IntelliJ.

1. Cliquez sur **File (Fichier)**, puis sur **Project Structure (Structure de projet)**.

   ![Commande Project Structure][ART01]

1. Cliquez sur hello vert plus (**+**) tooadd un artefact de symboles, cliquez sur **JAR**, puis cliquez sur **vide**.

   ![Ajouter un artefact][ART02]

1. Nommez votre artefact en veillant pas tooadd hello extension « .jar », puis spécifiez le dossier cible hello hello Maven de sortie.

   ![Spécifier les propriétés de l’artefact][ART03]

1. Créez un manifeste pour votre artefact (facultatif) :

   a. Cliquez sur **Create Manifest** (Créer un manifeste).

      ![Cliquez sur le bouton de créer un manifeste de hello][ART04a]

   b. Choisissez le chemin d’accès par défaut de hello pour l’artefact de hello, puis cliquez sur **OK**.

      ![Spécifier le chemin de l’artefact][ART04b]

   c. Cliquez sur les points de suspension hello (**...** ) classe principale de toolocate hello.

      ![Localiser la classe principale][ART04c]

   d. Choisissez votre classe principale, puis cliquez sur **OK**.

      ![Spécifier la classe principale][ART04d]

1. Cliquez sur **OK**.

   ![Fermez la boîte de dialogue de Structure de projet hello][ART05]

> [!NOTE]
> Pour plus d’informations sur la création des artefacts dans IntelliJ, consultez [configuration des artefacts] sur le site Web de JetBrains hello.
>

### <a name="build-hello-artifact-for-deployment"></a>Artefact hello pour le déploiement de build

1. Cliquez sur **Build** (Générer), puis sur **Artifacts** (Artefacts).

   ![Commande Build Artifacts][BU04]

1. Hello lorsque **générer un artefact** menu contextuel s’affiche, cliquez sur **Build**.

   ![Menu contextuel Build Artifact][BU05]

IntelliJ doit s’afficher artefact hello terminée pour votre application de démarrage du ressort dans la fenêtre outil du projet hello.

   ![Artefact créé][BU06]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Publier votre tooAzure d’application web à l’aide d’un conteneur Docker

1. Si vous n’êtes pas inscrit dans tooyour compte Azure, suivez les étapes de hello dans [instructions d’authentification pour hello boîte à outils Azure pour IntelliJ][Azure Sign In for IntelliJ].

1. Dans la fenêtre outil de l’Explorateur de projets hello, cliquez sur le projet de hello et sélectionnez **Azure** > **publier en tant que conteneur Docker**.

   ![Commande Publier en tant que conteneur Docker][PU01]

1. Hello lorsque **déployer le conteneur Docker sur Azure** boîte de dialogue s’affiche, tous les hôtes Docker existantes sont affichées. Si vous choisissez d’hôte de toodeploy tooan existant, vous pouvez ignorer toostep 4. Sinon, utilisez hello suivant les étapes toocreate un ordinateur hôte :

   a. Cliquez sur hello vert plus (**+**) symbole.

      ![Ajouter un nouvel hôte Docker][PU02]

   b. Hello lorsque **créer un hôte Docker** boîte de dialogue s’affiche, vous pouvez choisir les valeurs par défaut de tooaccept hello, ou vous pouvez spécifier tous les paramètres personnalisés pour votre nouvel hôte Docker. (Pour une description détaillée de hello divers paramètres, consultez [publier une application web comme un conteneur Docker à l’aide de hello boîte à outils Azure pour IntelliJ][Publish Container with Azure Toolkit].) Cliquez sur **suivant** lorsque vous avez spécifié le paramètres toouse.

      ![Spécifier les options de l’hôte Docker][PU03a]

   c. Vous pouvez choisir les informations d’identification de connexion existantes toouse dans un coffre de clés Azure, ou vous pouvez choisir de tooenter de nouvelles informations d’identification de connexion Docker. Cliquez sur **Finish** une fois que vous avez spécifié vos options.

      ![Spécifier les identifiants de connexion à l’hôte Docker][PU03b]

1. Sélectionnez votre hôte Docker, puis cliquez sur **Suivant**.

   ![Sélectionnez hello Docker hôte toouse][PU04]

1. Sur la dernière page de hello Hello **déployer le conteneur Docker sur Azure** boîte de dialogue, spécifiez hello options suivantes :

   a. Vous pouvez choisir toospecify un nom personnalisé pour le conteneur hello qui hébergera votre conteneur Docker, ou vous pouvez accepter la valeur par défaut hello.

   b. Entrez les ports TCP hello pour l’hôte docker à l’aide de la syntaxe de hello : *[port externe]*:*[port interne]*. Par exemple, **80:8080** spécifie un port externe 80 et le port interne ressort démarrage hello par défaut 8080.
   
      Si vous avez personnalisé votre port interne (par exemple, en modifiant le fichier de application.yml hello), vous devez numéro de port toospecify hello pour hello toooccur de routage correct dans Azure.

   c. Après avoir configuré ces options, cliquez sur **Terminer**.

   ![Déployer un conteneur Docker dans Azure][PU05]

1. Une fois hello boîte à outils Azure publication, hello affiche du journal des activités Azure **publié** pour l’état de hello.

   ![Déploiement réussi de l’hôte Docker][PU06]

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

toolearn des méthodes supplémentaires pour la création d’applications de démarrage du ressort à l’aide de IntelliJ, consultez [création de projets de démarrage ressort](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) sur le site Web de JetBrains hello.

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[configuration des artefacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html (Configuration des artefacts)
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[ressort démarrage]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
