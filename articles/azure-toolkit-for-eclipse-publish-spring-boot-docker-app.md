---
title: "une application de démarrage du ressort comme un conteneur Docker à l’aide d’aaaPublish hello boîte à outils Azure pour Eclipse | Documents Microsoft"
description: "Découvrez comment toopublish un tooMicrosoft d’application web Azure comme un conteneur Docker à l’aide de hello boîte à outils Azure pour Eclipse."
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
ms.openlocfilehash: 29390c49c339a1ebb87cb3951b21cea01c0da15f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a>Publier une application de démarrage du ressort comme un conteneur Docker à l’aide de hello boîte à outils Azure pour Eclipse

Hello [Spring Framework] est une solution open source qui permet aux développeurs Java de créer des applications d’entreprise. Un des projets plus-populaires hello qui est créé de plateforme est [ressort démarrage], qui fournit une approche simplifiée pour la création d’applications Java autonome.

[Docker] est une solution open source qui permet aux développeurs d’automatiser hello déploiement, mise à l’échelle et la gestion de leurs applications qui s’exécutent dans des conteneurs.

Ce didacticiel vous guide hello étapes toodeploy une application de démarrage du ressort comme un tooMicrosoft du conteneur Docker Azure à l’aide de hello boîte à outils Azure pour Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repository"></a>Cloner le référentiel de Docker de démarrage ressort hello par défaut

### <a name="import-hello-public-repository"></a>Importer un référentiel public hello

Hello étapes suivantes vous guident le clonage d’ordinateur local de hello ressort démarrage Docker référentiel tooyour à l’aide de IntelliJ. Si vous souhaitez toouse une ligne de commande, consultez [déployer une application de démarrage du ressort sur Linux dans le Service de conteneur Azure][Deploy Spring Boot on Linux in ACS].

1. Ouvrez Eclipse.

1. Cliquez sur **Fichier** > **Importer**.

   ![Menu Importer fichier][CL01]

1. Hello lorsque **importation** ouvre la boîte de dialogue :

   a. Développez **Git**.

   b. Sélectionnez **Projets de Git**.
   
   c. Cliquez sur **Suivant**.

   ![Boîte de dialogue Importer][CL02]

1. Sur hello **sélectionner une Source de référentiel** page :

   a. Sélectionnez **Cloner l’URI**.
   
   b. Cliquez sur **Suivant**.

   ![Sélectionner la page source du référentiel][CL03]

1. Sur hello **référentiel de code Source Git** page :

   a. Pour **URI**, entrez `https://github.com/spring-guides/gs-spring-boot-docker.git`. Cette étape doit remplir automatiquement hello **hôte** et **chemin d’accès du référentiel** champs avec hello corriger les valeurs.
   
   b. référentiel de démarrage du ressort Hello est publique, donc vous ne devez pas tooenter votre nom d’utilisateur Git et le mot de passe.
   
   c. Cliquez sur **Suivant**.

   ![Page du référentiel Git source][CL04]

1. Sur hello **sélection de la branche** , cliquez sur **suivant**.

   ![Page Sélection de la branche][CL05]

1. Sur hello **Local de Destination** page :

   a. Spécifiez hello de dossier local où vous souhaitez que votre référentiel local.
   
   b. Cliquez sur **Suivant**.

   ![Page Destination locale][CL06]

1. Sur hello **sélectionner un toouse de l’Assistant pour importer des projets** page :

   a. Sélectionnez **Importer en tant que projet général**.
   
   b. Cliquez sur **Suivant**.

   ![Page « Sélectionner un toouse de l’Assistant pour importer des projets »][CL07]

1. Sur hello **importation projets** page :

   a. Spécifiez le nom de votre projet.
   
   b. Cliquez sur **Terminer**.

   ![Page Importer des projets][CL08]

1. Lorsque le référentiel de hello est cloné avec succès, vous voyez tous les fichiers hello répertoriés dans Eclipse.

   ![Référentiel local][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a>Créer un projet Maven à partir de votre référentiel local

référentiel du ressort démarrage Docker Hello contient un projet de Maven terminé, vous allez utiliser pour ce didacticiel. 

1. Cliquez sur **Fichier** > **Importer**.

   ![Importer la commande de menu de fichier hello][CL01]

1. Hello lorsque **importation** ouvre la boîte de dialogue :

   a. Développez **Maven**.
   
   b. Sélectionnez **Projets Maven existants**.
   
   c. Cliquez sur **Suivant**.

   ![Boîte de dialogue Importer][MV01]

1. Sur hello **projets Maven** page :

   a. Pour **répertoire racine**, spécifiez hello **complète** dossier dans votre référentiel local.
   
   b. Développez hello **avancé** section et entrez un nom personnalisé pour **modèle de nom**.
   
   c. Boîte de sélection hello hello **pom.xml** fichier de projet de hello.
   
   d. Cliquez sur **Terminer**.

   ![Page Projets Maven][MV02]

1. Lorsque le projet de Maven hello est ouvert avec succès, vous consultez un deuxième projet répertorié dans Eclipse.

   ![Projet Maven local][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a>Générer votre application Spring Boot à l’aide de Maven

1. Bonjour Explorateur de projets Eclipse, sélectionnez projet de Maven hello.

1. Cliquez sur **Exécuter** > **Exécuter en tant que** > **build Maven**.

   ![Toorun de commandes en tant que build Maven][BU01]

1. Lorsque votre application est générée avec succès, fenêtre de console hello affiche état de hello.

   ![Build Maven réussie][BU02]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Publier votre tooAzure d’application web à l’aide d’un conteneur Docker

1. Bonjour Explorateur de projets Eclipse, sélectionnez projet de Maven hello.

1. Cliquez sur hello Azure **publier** menu, puis sur **publier en tant que conteneur Docker**.

   ![Commande Publier en tant que conteneur Docker][PU01]

1. Hello lorsque **déploiement de conteneur Docker sur Azure** boîte de dialogue s’affiche :

   a. Entrez un nom d’image Docker personnalisé.
   
   b. Pour **artefact toodeploy**, spécifiez hello chemin d’accès toohello **0.1.0.jar du docker démarrage gs ressort** fichier que vous venez de créer.

   ![Spécifiez les options Docker][PU02]

   Tous les hôtes Docker existants s’affichent. 

1. Si vous choisissez d’hôte de toodeploy tooan existant, vous pouvez ignorer toostep 5. Sinon, utilisez hello suivant les étapes toocreate un ordinateur hôte :

   a. Cliquez sur **Add**.

      ![Ajouter un nouvel hôte Docker][PU03]

   b. Hello lorsque **créer un hôte Docker** boîte de dialogue s’affiche, vous pouvez choisir les valeurs par défaut de tooaccept hello, ou vous pouvez spécifier tous les paramètres personnalisés pour votre nouvel hôte Docker. (Pour une description détaillée de hello divers paramètres, consultez [publier une application web comme un conteneur Docker à l’aide de hello boîte à outils Azure pour IntelliJ][Publish Container with Azure Toolkit].) Cliquez sur **suivant** lorsque vous avez spécifié le paramètres toouse.

      ![Spécifier les options de l’hôte Docker][PU04]

   c. Vous pouvez choisir les informations d’identification de connexion existantes toouse dans un coffre de clés Azure, ou vous pouvez choisir de tooenter de nouvelles informations d’identification de connexion Docker. Cliquez sur **Finish** une fois que vous avez spécifié vos options.

      ![Spécifier les identifiants de connexion à l’hôte Docker][PU05]

1. Sélectionnez votre hôte Docker, puis cliquez sur **Suivant**.

   ![Sélectionnez toouse d’hôte Docker][PU06]

1. Sur la dernière page de hello Hello **déploiement de conteneur Docker sur Azure** boîte de dialogue, spécifiez hello options suivantes :

   a. Vous pouvez choisir toospecify un nom personnalisé pour le conteneur hello qui hébergera votre conteneur Docker, ou vous pouvez accepter la valeur par défaut hello.

   b. Entrez les ports TCP hello pour l’hôte docker à l’aide de la syntaxe de hello : *[port externe]*:*[port interne]*. Par exemple, **80:8080** spécifie un port externe 80 et le port interne ressort démarrage hello par défaut 8080.
   
      Si vous avez personnalisé votre port interne (par exemple, en modifiant le fichier de application.yml hello), vous devez numéro de port toospecify hello pour hello toooccur de routage correct dans Azure.

   c. Après avoir configuré ces options, cliquez sur **Terminer**.

   ![Déployer un conteneur Docker dans Azure][PU07]

1. Une fois hello boîte à outils Azure publication, hello affiche du journal des activités Azure **publié** pour l’état de hello.

   ![Déploiement réussi de l’hôte Docker][PU08]

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[ressort démarrage]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
