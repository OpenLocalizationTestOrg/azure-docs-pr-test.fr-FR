---
title: "un conteneur Docker à l’aide d’aaaPublish hello boîte à outils Azure pour IntelliJ | Documents Microsoft"
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
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: bee94cb269ea707ae7ad55232e23e915aec48c34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a>Publier une application web comme un conteneur Docker à l’aide de hello boîte à outils Azure pour IntelliJ

Les conteneurs Docker constituent une méthode largement utilisée pour déployer des applications web. À l’aide de conteneurs Docker, les développeurs peuvent consolider toutes leurs fichiers de projet et les dépendances dans un package unique pour le serveur de déploiement tooa. Bonjour Azure Toolkit pour IntelliJ simplifie ce processus pour les développeurs Java en ajoutant *publier en tant que conteneur Docker* fonctionnalités pour tooMicrosoft de déploiement Azure. Cet article vous guide toopublish requis des étapes de hello tooAzure de vos applications en tant que conteneurs Docker.

> [!NOTE]
>
> Plus d’informations sur Docker est disponible sur hello [site Web de Docker].
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Publier votre tooAzure d’application web à l’aide d’un conteneur Docker

> [!NOTE]
> * toopublish votre application web, vous devez créer un artefact prêts pour le déploiement. toolearn, voir hello [plus d’informations sur la création d’artefacts](#artifacts) section.
>
> * Une fois que vous avez terminé l’Assistant Déploiement hello au moins une fois, la plupart de vos paramètres est utilisée comme valeurs par défaut lorsque vous réexécutez hello.
>

1. Ouvrez votre projet d’application web dans IntelliJ.

2. toostart hello **publier en tant que conteneur Docker** Assistant, effectuez une des manières suivantes les hello :

   * Bonjour **projet** fenêtre de l’outil, avec le bouton droit de votre projet, cliquez sur **Azure**, puis cliquez sur **publier en tant que conteneur Docker**:

      ![Hello publier en tant que commande de conteneur Docker][PUB01]

   * Barre d’outils hello IntelliJ, cliquez sur hello **groupe publier** bouton, puis cliquez sur **publier en tant que conteneur Docker**:

      ![Hello publier en tant que commande de conteneur Docker][PUB02]  
    Hello **déployer le conteneur Docker sur Azure** Assistant s’ouvre.

   ![Hello conteneur Docker de déployer sur l’Assistant Azure][PUB03]

3. Bonjour **tapez un nom d’image, sélectionnez le chemin d’accès d’artefact hello et vérifier un toobe d’hôte Docker utilisé** fenêtre, hello suivant : 

   a. Bonjour **nom de l’image Docker** , entrez un nom unique pour l’hôte Docker. (Assistant de hello crée automatiquement un nom, mais vous pouvez le modifier.) 

   b. Hello **hôtes** zone affiche tous les ordinateurs hôtes Docker que vous avez déjà créé. Effectuez une des manières suivantes les hello : 
      * Si vous avez un hôte Docker existant, vous pouvez déployer votre tooit d’application web.
      * toocreate un hôte Docker, cliquez sur signe plus vert de hello (**+**).  
       Hello **créer un hôte Docker** boîte de dialogue s’ouvre. 

      ![Assistant Deploy Docker Container on Azure (Déploiement d’un conteneur Docker sur Azure)][PUB04a]

4. Bonjour **configurer la machine virtuelle hello** fenêtre, fournir hello suivant le plus d’informations sur l’hôte Docker. (Assistant de hello génère automatiquement la plupart des informations hello pour vous, mais vous pouvez modifier un d'entre eux). 

   a. Bonjour **nom** , entrez un nom unique pour l’hôte Docker de hello. (Il est ne pas hello identique hello du nom de l’image Docker que vous avez spécifié précédemment). 
    
   b. Bonjour **abonnement** , entrez hello abonnement Azure que vous utilisez pour votre ordinateur hôte. 
      
   c. Bonjour **région** , entrez la région géographique de hello où se trouve votre hôte.
      
   d. Sur hello **du système d’exploitation et la taille** onglet, procédez comme hello suivant :      
      * **Héberger le système d’exploitation**: entrez le système d’exploitation de hello pour l’ordinateur virtuel hello qui contient votre hôte. 
      * **Taille**: entrez la taille de machine virtuelle hello pour votre ordinateur hôte.   
       
   e. Sur hello **groupe de ressources** , sélectionnez de hello suivantes :      
      * **New resource group** (Nouveau groupe de ressources) : créez un groupe de ressources pour votre hôte.
      * **Existing resource group** (Groupe de ressources existant) : spécifiez un groupe de ressources existant dans votre compte Azure. 
       
   f. Sur hello **réseau** , sélectionnez de hello suivantes :      
      * **New virtual network** (Nouveau réseau virtuel) : créez un réseau virtuel pour votre hôte.
      * **Existing virtual network** (Réseau virtuel existant) : spécifiez un réseau virtuel existant dans votre compte Azure. 
       
   g. Sur hello **stockage** , sélectionnez de hello suivantes :      
      * **New storage account** (Nouveau compte de stockage) : créez un compte de stockage pour votre hôte.
      * **Compte de stockage existant** : spécifiez un compte de stockage existant dans votre compte Azure.
       
5. Cliquez sur **Suivant**.  
     Hello **configurer le journal dans les informations d’identification et les paramètres de port** fenêtre s’ouvre.

      ![journal de configuration Hello dans la fenêtre des paramètres de port et les informations d’identification][PUB05]

6. Sélectionnez une des options suivantes de hello :

      * **Import credentials from Azure Key Vault** (Importer des informations d’identification depuis Azure Key Vault) : spécifiez un ensemble d’informations d’identification précédemment enregistré et stocké dans votre abonnement Azure.

          > [!NOTE]
          > Un coffre de clés Azure qui est créé avec un compte spécifique ou un principal de service n’est pas automatiquement accessible par un autre compte ou principal de service qui partage un abonnement de hello. une autre clé hello toouse principal compte ou le service de coffre tooallow, vous devez utiliser hello compte de hello tooadd portail Azure ou principal du service.

      * **New log in credentials** (Nouvelles informations d’identification de connexion) : créez un nouvel ensemble d’informations d’identification de connexion. Si vous sélectionnez cette option, procédez comme hello suivant :

        a. Sur hello **informations d’identification de l’ordinateur virtuel** fournir hello suit les informations d’identification de connexion d’accès à une machine virtuelle hello de l’hôte Docker, onglet : * **nom d’utilisateur**: entrez les nom d’utilisateur hello de votre connexion à une machine virtuelle informations d’identification.
             * **Mot de passe** et **confirmer**: entrez le mot de passe de hello vos informations d’identification du compte de connexion à une machine virtuelle.
             * **SSH**: entrez hello les paramètres de Secure Shell (SSH) pour l’hôte Docker. Vous pouvez sélectionner une des options suivantes de hello : * **aucun**: Spécifie que votre ordinateur virtuel n’autorise pas les connexions SSH.
                * **Générer automatiquement**: crée automatiquement les paramètres requis hello pour se connecter via une connexion SSH.
                * **Importer à partir du répertoire**: vous permet de toospecify un répertoire qui contient un ensemble de paramètres SSH précédemment enregistrés. répertoire de Hello doit contenir hello deux fichiers suivants :
                
                  * *id_rsa*: Contains hello RSA identification for a user.
                  * *id_rsa.pub*: Contains hello RSA public key that is used for authentication.
            
        b. Sur hello **accès du démon Docker** , onglet de fournir hello informations suivantes :

          ![Créer un hôte Docker][PUB06]
    
             * **Docker Daemon port**: Enter hello unique TCP port for your Docker host.
             * **TLS Security**: Enter hello Transport Layer Security settings for your Docker host. You can choose from hello following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. hello directory must contain hello following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain hello client certificate and public key that is used for TLS authentication.

7. Après avoir entré les informations de hello requis, cliquez sur **Terminer**.  
    Hello **déployer le conteneur Docker sur Azure** Assistant s’affiche de nouveau.

   ![Assistant Deploy Docker Container on Azure (Déploiement d’un conteneur Docker sur Azure)][PUB07]

8. Cliquez sur **Suivant**.  
    Hello **configurer toobe de conteneur Docker hello créé** fenêtre s’ouvre.

   ![fenêtre de Hello configurer hello Docker conteneur toobe créé][PUB08]

9. Bonjour **configurer toobe de conteneur Docker hello créé** fenêtre, fournir hello informations suivantes : 

   a. Bonjour **nom du conteneur Docker** , entrez un nom unique pour votre conteneur Docker.

   b. Choisissez une des hello suivant Docker images : 

      * **Predefined Docker image** (Image Docker prédéfinie) : spécifiez une image Docker préexistante dans Azure. 

        > [!NOTE]
        > liste de Hello d’images Docker dans cette zone se compose de plusieurs images qui hello boîte à outils Azure a été configuré toopatch afin que votre objet est déployé automatiquement. 

      * **Custom Dockerfile** (Fichier Dockerfile personnalisé) : spécifiez un fichier Dockerfile précédemment enregistré sur votre ordinateur local.

        > [!NOTE]
        > Il s’agit d’une fonctionnalité avancée pour les développeurs qui veulent toodeploy leur propre fichier Dockerfile. Toutefois, c’est toodevelopers qui utilisent cette tooensure option leur Dockerfile générée correctement. Étant donné que hello boîte à outils Azure ne valide pas le contenu de hello dans un fichier Dockerfile personnalisé, déploiement de hello peut échouer si hello Dockerfile présente des problèmes. En outre, hello boîte à outils Azure escomptant hello personnalisé Dockerfile toocontain un artefact d’application web, il tente de tooopen une connexion HTTP. Si les développeurs publier un autre type d’artefact, ils peuvent recevoir des erreurs sans effet après le déploiement.

   c. Bonjour **paramètres de Port** , entrez la liaison de port TCP unique hello pour votre conteneur Docker. 

10. Après avoir terminé les étapes précédentes de hello, cliquez sur **Terminer**. 

Hello boîte à outils Azure commence à déployer votre tooAzure d’application web dans un conteneur Docker. Sauf si vous avez configuré toobe IntelliJ déployé dans l’arrière-plan de hello, un **déploiement tooAzure** barre de progression s’affiche. 

![barre de progression du déploiement Hello][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a>Informations supplémentaires sur la création d’artefacts

toocreate un artefact prêts pour le déploiement, procédez comme hello suivant :

1. Ouvrez votre projet d’application web dans IntelliJ.

2. Cliquez sur **File (Fichier)**, puis sur **Project Structure (Structure de projet)**.

   ![Hello commande de la Structure de projet][ART01]

3. tooadd un artefact, cliquez sur signe plus vert de hello (**+**), puis cliquez sur **Application Web : Archive**.

   ![Hello commande de « Application Web : Archive »][ART02]

4. Bonjour **nom** , entrez un nom pour votre artefact (n’incluez pas hello *.war* extension), puis cliquez sur **OK**.

   ![zone de nom d’artefact Hello][ART03]

Pour plus d’informations sur la création des artefacts dans IntelliJ, consultez [configurant des artefacts] sur le site Web de JetBrains hello.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur hello boîtes à outils Azure pour Java IDE, consultez hello suivant des ressources :

* [boîte à outils Azure pour Eclipse]
  * [Nouveautés de hello boîte à outils Azure pour Eclipse]
  * [Lors de l’installation hello boîte à outils Azure pour Eclipse]
  * [Instructions de connexion pour hello boîte à outils Azure pour Eclipse]
  * [Créer une application web Hello World pour Azure dans Eclipse]
* [Kit de ressources Azure pour IntelliJ]
  * [Quelles sont les nouveautés Bonjour Azure Toolkit pour IntelliJ]
  * [Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]
  * [Instructions d’authentification pour hello boîte à outils Azure pour IntelliJ]
  * [Créer une application web Hello World pour Azure dans IntelliJ]

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure] et hello [outils Java pour Visual Studio Team Services].

Pour obtenir des ressources supplémentaires pour Docker, consultez officielle de hello [site Web de Docker].

<!-- URL List -->

[boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij.md
[Créer une application web Hello World pour Azure dans Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Créer une application web Hello World pour Azure dans IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Lors de l’installation hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instructions de connexion pour hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Instructions d’authentification pour hello boîte à outils Azure pour IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Nouveautés de hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Quelles sont les nouveautés Bonjour Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[centre de développement Java Azure]: https://azure.microsoft.com/develop/java/
[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/

[site Web de Docker]: https://www.docker.com/
[configurant des artefacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
