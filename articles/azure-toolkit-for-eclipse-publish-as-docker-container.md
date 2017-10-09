---
title: "un conteneur Docker à l’aide d’aaaPublish hello boîte à outils Azure pour Eclipse | Documents Microsoft"
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
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 53ec3a7f7a171691024e03622fd48d6f1e257b50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a>Publier une application web comme un conteneur Docker à l’aide de hello boîte à outils Azure pour Eclipse

Les conteneurs Docker constituent une méthode largement utilisée pour déployer des applications web. À l’aide de conteneurs Docker, les développeurs peuvent consolider toutes leurs fichiers de projet et les dépendances dans un package unique pour le serveur de déploiement tooa. Hello boîte à outils Azure pour Eclipse simplifie ce processus pour les développeurs Java en ajoutant *publier en tant que conteneur Docker* fonctionnalités pour tooMicrosoft de déploiement Azure. Cet article vous guide toopublish requis des étapes de hello tooAzure de vos applications en tant que conteneurs Docker.

> [!NOTE]
> Plus d’informations sur Docker est disponible sur hello [site Web de Docker].
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Publier votre tooAzure d’application web à l’aide d’un conteneur Docker

1. Ouvrez votre projet d’application web dans Eclipse.

2. toostart hello **publier en tant que conteneur Docker** Assistant, effectuez une des manières suivantes les hello :

   * Bonjour **Navigator** afficher, avec le bouton droit de votre projet, cliquez sur **Azure**, puis cliquez sur **publier en tant que conteneur Docker**.

      ![Commande Publish as Docker Container (Publier en tant que conteneur Docker) de la vue Navigator (Navigateur)][PUB01]

   * Barre d’outils hello Eclipse, cliquez sur hello **publier** bouton, puis cliquez sur **publier en tant que conteneur Docker**.

      ![Commande Publier en tant que conteneur Docker de la barre d’outils Eclipse][PUB02]
      
    Hello **déployer le conteneur Docker sur Azure** Assistant s’ouvre.

    ![Hello conteneur Docker de déployer sur l’Assistant Azure][PUB03]

3. Bonjour **tapez un nom d’image, sélectionnez le chemin d’accès d’artefact hello et vérifier un toobe d’hôte Docker utilisé** fenêtre, hello suivant :

    a. Bonjour **nom de l’image Docker** , entrez un nom unique pour l’hôte Docker. (Assistant de hello crée automatiquement un nom, mais vous pouvez le modifier.)

    b. Hello **hôtes** zone affiche tous les ordinateurs hôtes Docker que vous avez déjà créé. Effectuez une des manières suivantes les hello :

    * Si vous avez un hôte Docker existant, vous pouvez déployer votre tooit d’application web.
    * toocreate un nouvel hôte Docker, cliquez sur **ajouter**.  
      
    Hello **créer un hôte Docker** boîte de dialogue s’ouvre.

    ![Assistant Deploy Docker Container on Azure (Déploiement d’un conteneur Docker sur Azure)][PUB04a]

4. Bonjour **configurer la machine virtuelle hello** fenêtre, spécifiez hello options pour l’hôte Docker suivantes. (Assistant de hello génère automatiquement la plupart des options hello pour vous, mais vous pouvez modifier un d'entre eux).

   a. **Nom**: entrez un nom unique pour l’hôte Docker de hello. (Il est ne pas hello identique hello du nom de l’image Docker que vous avez spécifié précédemment).

   b. **Abonnement**: entrez hello abonnement Azure que vous utilisez pour votre ordinateur hôte.

   c. **Région**: entrez hello la région géographique où se trouve votre hôte.

   d. Sur hello **système d’exploitation hôte et la taille** onglet :
     * **Héberger le système d’exploitation**: entrez le système d’exploitation de hello pour l’ordinateur virtuel hello qui contient votre hôte.
     * **Taille**: entrez la taille de machine virtuelle hello pour votre ordinateur hôte.

   e. Sur hello **groupe de ressources** onglet :
     * **New resource group** (Nouveau groupe de ressources) : créez un groupe de ressources pour votre hôte.
     * **Existing resource group** (Groupe de ressources existant) : entrez un groupe de ressources existant dans votre compte Azure.

   f. Sur hello **réseau** onglet :
     * **New virtual network** (Nouveau réseau virtuel) : créez un réseau virtuel pour votre hôte.
     * **Existing virtual network** (Réseau virtuel existant) : entrez un réseau virtuel existant dans votre compte Azure.

   g. Sur hello **stockage** onglet :
     * **New storage account** (Nouveau compte de stockage) : créez un compte de stockage pour votre hôte.
     * **Existing storage account** (Compte de stockage existant) : entrez un compte de stockage existant dans votre compte Azure.

5. Cliquez sur **Suivant**.

6. Bonjour **configurer le journal dans les informations d’identification et les paramètres de port** fenêtre, sélectionnez une des options suivantes de hello :

    * **Import credentials from Azure Key Vault** (Importer des informations d’identification depuis Azure Key Vault) : spécifie un ensemble d’informations d’identification précédemment enregistré et stocké dans votre abonnement Azure.

      >[!NOTE]
      >Un coffre de clés Azure qui est créé avec un compte spécifique ou un principal de service n’est pas automatiquement accessible par un autre compte ou principal de service qui partage un abonnement de hello. tooallow les toouse un autre compte ou un service principal hello coffre de clés, vous devez utiliser des hello compte de hello tooadd portail Azure ou principal du service.

    * **New log in credentials** (Nouvelles informations d’identification de connexion) : crée un nouvel ensemble d’informations d’identification de connexion. Si vous sélectionnez cette option, procédez comme hello suivant :
    
      * Sur hello **informations d’identification de l’ordinateur virtuel** , onglet de sélectionner les options pour les informations d’identification du compte de connexion à une machine virtuelle hello de l’hôte Docker de hello suivantes :

          * **Nom d’utilisateur**: entrez le nom d’utilisateur hello vos informations d’identification de connexion de machine virtuelle.
          * **Mot de passe** et **confirmer**: entrez le mot de passe hello vos informations d’identification de connexion de machine virtuelle.
          * **SSH**: entrez hello les paramètres de Secure Shell (SSH) pour l’hôte Docker. Vous pouvez choisir parmi hello options suivantes :
            * **None** (Aucun) : spécifie que votre machine virtuelle n’autorisera pas les connexions SSH.
            * **Générer automatiquement**: crée automatiquement les paramètres requis hello pour se connecter via une connexion SSH.
            * **Import from directory** (Importer à partir du répertoire) : spécifie un répertoire qui contient un jeu de paramètres SSH précédemment enregistrés. répertoire de Hello doit contenir hello deux fichiers suivants :
                * *id_rsa*: contient l’identification de RSA hello pour un utilisateur.
                * *id_rsa.pub*: contient la clé publique hello RSA qui est utilisé pour l’authentification.
        
        ![Créer un hôte Docker][PUB05]

      * Sur hello **informations d’identification du démon Docker** onglet, spécifiez hello options suivantes :

          * **Port du démon docker**: entrez le port TCP unique hello pour l’hôte Docker.
          * **Sécurité TLS**: entrez les paramètres de sécurité de la couche Transport hello pour l’hôte Docker. Vous pouvez choisir parmi hello options suivantes :
            * **None** (Aucun) : spécifie que votre machine virtuelle n’autorisera pas les connexions TLS.
            * **Générer automatiquement**: crée automatiquement les paramètres requis hello pour se connecter via le protocole TLS.
            * **Import from directory** (Importer à partir du répertoire) : spécifie un répertoire qui contient un jeu de paramètres TLS précédemment enregistrés. Plus spécifiquement, répertoire de hello doit contenir hello six fichiers suivants :
                * *CA.PEM* et *key.pem de l’autorité de certification*: contient le certificat de hello et la clé publique pour hello certificat TLS.
                * *CERT.PEM* et *key.pem*: contient le certificat de client hello et la clé publique qui est utilisée pour l’authentification TLS.
                * *Server.PEM* et *key.pem-server*: contient le certificat de serveur hello et la clé publique pour l’hôte de hello.

        ![Créer un hôte Docker][PUB06]

7. Après avoir entré toutes les informations précédentes de hello, cliquez sur **Terminer**.

8. Bonjour **déployer le conteneur Docker sur Azure** Assistant, cliquez sur **suivant**.

   ![Hello conteneur Docker de déployer sur l’Assistant Azure][PUB07]

9. Bonjour **configurer toobe de conteneur Docker hello créé** fenêtre, hello suivant :

   a. Bonjour **nom du conteneur Docker** , entrez un nom unique pour votre conteneur Docker.

   b. Choisissez une des hello suivant Docker images :
     * **Predefined Docker image** (Image Docker prédéfinie) : spécifie une image Docker préexistante dans Azure.

       >[!NOTE]
       >liste de Hello d’images Docker dans cette zone se compose de plusieurs images qui hello boîte à outils Azure a été configuré toopatch afin que votre objet est déployé automatiquement.

     * **Custom Dockerfile** (Fichier Dockerfile personnalisé) : spécifie un fichier Dockerfile précédemment enregistré sur votre ordinateur local.

       >[!NOTE]
       >Il s’agit d’une fonctionnalité avancée pour les développeurs qui veulent toodeploy leur propre fichier Dockerfile. Toutefois, c’est toodevelopers qui utilisent cette tooensure option leur Dockerfile générée correctement. Hello boîte à outils Azure ne valide pas le contenu de hello dans un fichier Dockerfile personnalisé, afin de hello déploiement risque d’échouer si hello Dockerfile présente des problèmes. En outre, hello boîte à outils Azure attend hello personnalisé Dockerfile toocontain un artefact d’application web, et il va tenter de tooopen une connexion HTTP. Si les développeurs publient un autre type d’artefact, ils peuvent recevoir des erreurs sans effet après le déploiement.

   c. **Paramètres de port**: entrez la liaison de port TCP unique hello pour votre conteneur Docker.

     ![fenêtre de Hello configurer hello Docker conteneur toobe créé][PUB08]

10. Une fois que vous avez effectué toutes les étapes précédentes de hello, cliquez sur **Terminer**.

Hello boîte à outils Azure commence à déployer votre tooAzure d’application web dans un conteneur Docker. 

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

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez [Centre de développement Java pour Azure] et [Outils Java pour Visual Studio Team Services].

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

[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/
[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/

[site Web de Docker]: https://www.docker.com/

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png