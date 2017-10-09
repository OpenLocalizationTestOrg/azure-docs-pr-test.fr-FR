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
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="b2959-103">Publier une application web comme un conteneur Docker à l’aide de hello boîte à outils Azure pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="b2959-103">Publish a web app as a Docker container by using hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="b2959-104">Les conteneurs Docker constituent une méthode largement utilisée pour déployer des applications web.</span><span class="sxs-lookup"><span data-stu-id="b2959-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="b2959-105">À l’aide de conteneurs Docker, les développeurs peuvent consolider toutes leurs fichiers de projet et les dépendances dans un package unique pour le serveur de déploiement tooa.</span><span class="sxs-lookup"><span data-stu-id="b2959-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment tooa server.</span></span> <span data-ttu-id="b2959-106">Hello boîte à outils Azure pour Eclipse simplifie ce processus pour les développeurs Java en ajoutant *publier en tant que conteneur Docker* fonctionnalités pour tooMicrosoft de déploiement Azure.</span><span class="sxs-lookup"><span data-stu-id="b2959-106">hello Azure Toolkit for Eclipse simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment tooMicrosoft Azure.</span></span> <span data-ttu-id="b2959-107">Cet article vous guide toopublish requis des étapes de hello tooAzure de vos applications en tant que conteneurs Docker.</span><span class="sxs-lookup"><span data-stu-id="b2959-107">This article walks you through hello steps required toopublish your applications tooAzure as Docker containers.</span></span>

> [!NOTE]
> <span data-ttu-id="b2959-108">Plus d’informations sur Docker est disponible sur hello [site Web de Docker].</span><span class="sxs-lookup"><span data-stu-id="b2959-108">More information about Docker is available on hello [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="b2959-109">Publier votre tooAzure d’application web à l’aide d’un conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="b2959-109">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="b2959-110">Ouvrez votre projet d’application web dans Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b2959-110">Open your web app project in Eclipse.</span></span>

2. <span data-ttu-id="b2959-111">toostart hello **publier en tant que conteneur Docker** Assistant, effectuez une des manières suivantes les hello :</span><span class="sxs-lookup"><span data-stu-id="b2959-111">toostart hello **Publish as Docker Container** wizard, do either of hello following:</span></span>

   * <span data-ttu-id="b2959-112">Bonjour **Navigator** afficher, avec le bouton droit de votre projet, cliquez sur **Azure**, puis cliquez sur **publier en tant que conteneur Docker**.</span><span class="sxs-lookup"><span data-stu-id="b2959-112">In hello **Navigator** view, right-click your project, click **Azure**, and then click **Publish as Docker Container**.</span></span>

      ![Commande Publish as Docker Container (Publier en tant que conteneur Docker) de la vue Navigator (Navigateur)][PUB01]

   * <span data-ttu-id="b2959-114">Barre d’outils hello Eclipse, cliquez sur hello **publier** bouton, puis cliquez sur **publier en tant que conteneur Docker**.</span><span class="sxs-lookup"><span data-stu-id="b2959-114">On hello Eclipse toolbar, click hello **Publish** button, and then click **Publish as Docker Container**.</span></span>

      ![Commande Publier en tant que conteneur Docker de la barre d’outils Eclipse][PUB02]
      
    <span data-ttu-id="b2959-116">Hello **déployer le conteneur Docker sur Azure** Assistant s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="b2959-116">hello **Deploy Docker Container on Azure** wizard opens.</span></span>

    ![Hello conteneur Docker de déployer sur l’Assistant Azure][PUB03]

3. <span data-ttu-id="b2959-118">Bonjour **tapez un nom d’image, sélectionnez le chemin d’accès d’artefact hello et vérifier un toobe d’hôte Docker utilisé** fenêtre, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b2959-118">In hello **Type an image name, select hello artifact's path and check a Docker host toobe used** window, do hello following:</span></span>

    <span data-ttu-id="b2959-119">a.</span><span class="sxs-lookup"><span data-stu-id="b2959-119">a.</span></span> <span data-ttu-id="b2959-120">Bonjour **nom de l’image Docker** , entrez un nom unique pour l’hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="b2959-120">In hello **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="b2959-121">(Assistant de hello crée automatiquement un nom, mais vous pouvez le modifier.)</span><span class="sxs-lookup"><span data-stu-id="b2959-121">(hello wizard automatically creates a name, but you can modify it.)</span></span>

    <span data-ttu-id="b2959-122">b.</span><span class="sxs-lookup"><span data-stu-id="b2959-122">b.</span></span> <span data-ttu-id="b2959-123">Hello **hôtes** zone affiche tous les ordinateurs hôtes Docker que vous avez déjà créé.</span><span class="sxs-lookup"><span data-stu-id="b2959-123">hello **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="b2959-124">Effectuez une des manières suivantes les hello :</span><span class="sxs-lookup"><span data-stu-id="b2959-124">Do either of hello following:</span></span>

    * <span data-ttu-id="b2959-125">Si vous avez un hôte Docker existant, vous pouvez déployer votre tooit d’application web.</span><span class="sxs-lookup"><span data-stu-id="b2959-125">If you have an existing Docker host, you can deploy your web app tooit.</span></span>
    * <span data-ttu-id="b2959-126">toocreate un nouvel hôte Docker, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b2959-126">toocreate a new Docker host, click **Add**.</span></span>  
      
    <span data-ttu-id="b2959-127">Hello **créer un hôte Docker** boîte de dialogue s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="b2959-127">hello **Create Docker Host** dialog box opens.</span></span>

    ![Assistant Deploy Docker Container on Azure (Déploiement d’un conteneur Docker sur Azure)][PUB04a]

4. <span data-ttu-id="b2959-129">Bonjour **configurer la machine virtuelle hello** fenêtre, spécifiez hello options pour l’hôte Docker suivantes.</span><span class="sxs-lookup"><span data-stu-id="b2959-129">In hello **Configure hello new virtual machine** window, specify hello following options for your Docker host.</span></span> <span data-ttu-id="b2959-130">(Assistant de hello génère automatiquement la plupart des options hello pour vous, mais vous pouvez modifier un d'entre eux).</span><span class="sxs-lookup"><span data-stu-id="b2959-130">(hello wizard automatically generates most of hello options for you, but you can modify any of them.)</span></span>

   <span data-ttu-id="b2959-131">a.</span><span class="sxs-lookup"><span data-stu-id="b2959-131">a.</span></span> <span data-ttu-id="b2959-132">**Nom**: entrez un nom unique pour l’hôte Docker de hello.</span><span class="sxs-lookup"><span data-stu-id="b2959-132">**Name**: Enter a unique name for hello Docker host.</span></span> <span data-ttu-id="b2959-133">(Il est ne pas hello identique hello du nom de l’image Docker que vous avez spécifié précédemment).</span><span class="sxs-lookup"><span data-stu-id="b2959-133">(It is not hello same as hello Docker image name that you specified earlier.)</span></span>

   <span data-ttu-id="b2959-134">b.</span><span class="sxs-lookup"><span data-stu-id="b2959-134">b.</span></span> <span data-ttu-id="b2959-135">**Abonnement**: entrez hello abonnement Azure que vous utilisez pour votre ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="b2959-135">**Subscription**: Enter hello Azure subscription that you use for your host.</span></span>

   <span data-ttu-id="b2959-136">c.</span><span class="sxs-lookup"><span data-stu-id="b2959-136">c.</span></span> <span data-ttu-id="b2959-137">**Région**: entrez hello la région géographique où se trouve votre hôte.</span><span class="sxs-lookup"><span data-stu-id="b2959-137">**Region**: Enter hello geographical region where your host is located.</span></span>

   <span data-ttu-id="b2959-138">d.</span><span class="sxs-lookup"><span data-stu-id="b2959-138">d.</span></span> <span data-ttu-id="b2959-139">Sur hello **système d’exploitation hôte et la taille** onglet :</span><span class="sxs-lookup"><span data-stu-id="b2959-139">On hello **Host OS and Size** tab:</span></span>
     * <span data-ttu-id="b2959-140">**Héberger le système d’exploitation**: entrez le système d’exploitation de hello pour l’ordinateur virtuel hello qui contient votre hôte.</span><span class="sxs-lookup"><span data-stu-id="b2959-140">**Host OS**: Enter hello operating system for hello virtual machine that contains your host.</span></span>
     * <span data-ttu-id="b2959-141">**Taille**: entrez la taille de machine virtuelle hello pour votre ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="b2959-141">**Size**: Enter hello virtual-machine size for your host.</span></span>

   <span data-ttu-id="b2959-142">e.</span><span class="sxs-lookup"><span data-stu-id="b2959-142">e.</span></span> <span data-ttu-id="b2959-143">Sur hello **groupe de ressources** onglet :</span><span class="sxs-lookup"><span data-stu-id="b2959-143">On hello **Resource Group** tab:</span></span>
     * <span data-ttu-id="b2959-144">**New resource group** (Nouveau groupe de ressources) : créez un groupe de ressources pour votre hôte.</span><span class="sxs-lookup"><span data-stu-id="b2959-144">**New resource group**: Create a new resource group for your host.</span></span>
     * <span data-ttu-id="b2959-145">**Existing resource group** (Groupe de ressources existant) : entrez un groupe de ressources existant dans votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="b2959-145">**Existing resource group**: Enter an existing resource group from your Azure account.</span></span>

   <span data-ttu-id="b2959-146">f.</span><span class="sxs-lookup"><span data-stu-id="b2959-146">f.</span></span> <span data-ttu-id="b2959-147">Sur hello **réseau** onglet :</span><span class="sxs-lookup"><span data-stu-id="b2959-147">On hello **Network** tab:</span></span>
     * <span data-ttu-id="b2959-148">**New virtual network** (Nouveau réseau virtuel) : créez un réseau virtuel pour votre hôte.</span><span class="sxs-lookup"><span data-stu-id="b2959-148">**New virtual network**: Create a new virtual network for your host.</span></span>
     * <span data-ttu-id="b2959-149">**Existing virtual network** (Réseau virtuel existant) : entrez un réseau virtuel existant dans votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="b2959-149">**Existing virtual network**: Enter an existing virtual network from your Azure account.</span></span>

   <span data-ttu-id="b2959-150">g.</span><span class="sxs-lookup"><span data-stu-id="b2959-150">g.</span></span> <span data-ttu-id="b2959-151">Sur hello **stockage** onglet :</span><span class="sxs-lookup"><span data-stu-id="b2959-151">On hello **Storage** tab:</span></span>
     * <span data-ttu-id="b2959-152">**New storage account** (Nouveau compte de stockage) : créez un compte de stockage pour votre hôte.</span><span class="sxs-lookup"><span data-stu-id="b2959-152">**New storage account**: Create a new storage account for your host.</span></span>
     * <span data-ttu-id="b2959-153">**Existing storage account** (Compte de stockage existant) : entrez un compte de stockage existant dans votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="b2959-153">**Existing storage account**: Enter an existing storage account from your Azure account.</span></span>

5. <span data-ttu-id="b2959-154">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="b2959-154">Click **Next**.</span></span>

6. <span data-ttu-id="b2959-155">Bonjour **configurer le journal dans les informations d’identification et les paramètres de port** fenêtre, sélectionnez une des options suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="b2959-155">In hello **Configure log in credentials and port settings** window, select one of hello following options:</span></span>

    * <span data-ttu-id="b2959-156">**Import credentials from Azure Key Vault** (Importer des informations d’identification depuis Azure Key Vault) : spécifie un ensemble d’informations d’identification précédemment enregistré et stocké dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="b2959-156">**Import credentials from Azure Key Vault**: Specifies a previously saved set of credentials that are stored in your Azure subscription.</span></span>

      >[!NOTE]
      ><span data-ttu-id="b2959-157">Un coffre de clés Azure qui est créé avec un compte spécifique ou un principal de service n’est pas automatiquement accessible par un autre compte ou principal de service qui partage un abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="b2959-157">An Azure Key Vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares hello subscription.</span></span> <span data-ttu-id="b2959-158">tooallow les toouse un autre compte ou un service principal hello coffre de clés, vous devez utiliser des hello compte de hello tooadd portail Azure ou principal du service.</span><span class="sxs-lookup"><span data-stu-id="b2959-158">tooallow another account or service principal toouse hello Key Vault, you must use hello Azure portal tooadd hello account or service principal.</span></span>

    * <span data-ttu-id="b2959-159">**New log in credentials** (Nouvelles informations d’identification de connexion) : crée un nouvel ensemble d’informations d’identification de connexion.</span><span class="sxs-lookup"><span data-stu-id="b2959-159">**New log in credentials**: Creates a new set of login credentials.</span></span> <span data-ttu-id="b2959-160">Si vous sélectionnez cette option, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b2959-160">If you select this option, do hello following:</span></span>
    
      * <span data-ttu-id="b2959-161">Sur hello **informations d’identification de l’ordinateur virtuel** , onglet de sélectionner les options pour les informations d’identification du compte de connexion à une machine virtuelle hello de l’hôte Docker de hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="b2959-161">On hello **VM Credentials** tab, choose one of hello following options for hello virtual-machine login credentials of your Docker host:</span></span>

          * <span data-ttu-id="b2959-162">**Nom d’utilisateur**: entrez le nom d’utilisateur hello vos informations d’identification de connexion de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b2959-162">**Username**: Enter hello username for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="b2959-163">**Mot de passe** et **confirmer**: entrez le mot de passe hello vos informations d’identification de connexion de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b2959-163">**Password** and **Confirm**: Enter hello password for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="b2959-164">**SSH**: entrez hello les paramètres de Secure Shell (SSH) pour l’hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="b2959-164">**SSH**: Enter hello Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="b2959-165">Vous pouvez choisir parmi hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="b2959-165">You can choose from hello following options:</span></span>
            * <span data-ttu-id="b2959-166">**None** (Aucun) : spécifie que votre machine virtuelle n’autorisera pas les connexions SSH.</span><span class="sxs-lookup"><span data-stu-id="b2959-166">**None**: Specifies that your virtual machine will not allow SSH connections.</span></span>
            * <span data-ttu-id="b2959-167">**Générer automatiquement**: crée automatiquement les paramètres requis hello pour se connecter via une connexion SSH.</span><span class="sxs-lookup"><span data-stu-id="b2959-167">**Auto-generate**: Automatically creates hello requisite settings for connecting via SSH.</span></span>
            * <span data-ttu-id="b2959-168">**Import from directory** (Importer à partir du répertoire) : spécifie un répertoire qui contient un jeu de paramètres SSH précédemment enregistrés.</span><span class="sxs-lookup"><span data-stu-id="b2959-168">**Import from directory**: Specifies a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="b2959-169">répertoire de Hello doit contenir hello deux fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="b2959-169">hello directory must contain hello following two files:</span></span>
                * <span data-ttu-id="b2959-170">*id_rsa*: contient l’identification de RSA hello pour un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b2959-170">*id_rsa*: Contains hello RSA identification for a user.</span></span>
                * <span data-ttu-id="b2959-171">*id_rsa.pub*: contient la clé publique hello RSA qui est utilisé pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="b2959-171">*id_rsa.pub*: Contains hello RSA public key that is used for authentication.</span></span>
        
        ![Créer un hôte Docker][PUB05]

      * <span data-ttu-id="b2959-173">Sur hello **informations d’identification du démon Docker** onglet, spécifiez hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="b2959-173">On hello **Docker Daemon Credentials** tab, specify hello following options:</span></span>

          * <span data-ttu-id="b2959-174">**Port du démon docker**: entrez le port TCP unique hello pour l’hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="b2959-174">**Docker Daemon port**: Enter hello unique TCP port for your Docker host.</span></span>
          * <span data-ttu-id="b2959-175">**Sécurité TLS**: entrez les paramètres de sécurité de la couche Transport hello pour l’hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="b2959-175">**TLS Security**: Enter hello Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="b2959-176">Vous pouvez choisir parmi hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="b2959-176">You can choose from hello following options:</span></span>
            * <span data-ttu-id="b2959-177">**None** (Aucun) : spécifie que votre machine virtuelle n’autorisera pas les connexions TLS.</span><span class="sxs-lookup"><span data-stu-id="b2959-177">**None**: Specifies that your virtual machine will not allow TLS connections.</span></span>
            * <span data-ttu-id="b2959-178">**Générer automatiquement**: crée automatiquement les paramètres requis hello pour se connecter via le protocole TLS.</span><span class="sxs-lookup"><span data-stu-id="b2959-178">**Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.</span></span>
            * <span data-ttu-id="b2959-179">**Import from directory** (Importer à partir du répertoire) : spécifie un répertoire qui contient un jeu de paramètres TLS précédemment enregistrés.</span><span class="sxs-lookup"><span data-stu-id="b2959-179">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="b2959-180">Plus spécifiquement, répertoire de hello doit contenir hello six fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="b2959-180">More specifically, hello directory must contain hello following six files:</span></span>
                * <span data-ttu-id="b2959-181">*CA.PEM* et *key.pem de l’autorité de certification*: contient le certificat de hello et la clé publique pour hello certificat TLS.</span><span class="sxs-lookup"><span data-stu-id="b2959-181">*ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.</span></span>
                * <span data-ttu-id="b2959-182">*CERT.PEM* et *key.pem*: contient le certificat de client hello et la clé publique qui est utilisée pour l’authentification TLS.</span><span class="sxs-lookup"><span data-stu-id="b2959-182">*cert.pem* and *key.pem*: Contain hello client certificate and public key that is used for TLS authentication.</span></span>
                * <span data-ttu-id="b2959-183">*Server.PEM* et *key.pem-server*: contient le certificat de serveur hello et la clé publique pour l’hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="b2959-183">*server.pem* and *server-key.pem*: Contain hello server certificate and public key for hello host.</span></span>

        ![Créer un hôte Docker][PUB06]

7. <span data-ttu-id="b2959-185">Après avoir entré toutes les informations précédentes de hello, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="b2959-185">After you have entered all of hello preceding information, click **Finish**.</span></span>

8. <span data-ttu-id="b2959-186">Bonjour **déployer le conteneur Docker sur Azure** Assistant, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="b2959-186">In hello **Deploy Docker Container on Azure** wizard, click **Next**.</span></span>

   ![Hello conteneur Docker de déployer sur l’Assistant Azure][PUB07]

9. <span data-ttu-id="b2959-188">Bonjour **configurer toobe de conteneur Docker hello créé** fenêtre, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b2959-188">In hello **Configure hello Docker container toobe created** window, do hello following:</span></span>

   <span data-ttu-id="b2959-189">a.</span><span class="sxs-lookup"><span data-stu-id="b2959-189">a.</span></span> <span data-ttu-id="b2959-190">Bonjour **nom du conteneur Docker** , entrez un nom unique pour votre conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="b2959-190">In hello **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="b2959-191">b.</span><span class="sxs-lookup"><span data-stu-id="b2959-191">b.</span></span> <span data-ttu-id="b2959-192">Choisissez une des hello suivant Docker images :</span><span class="sxs-lookup"><span data-stu-id="b2959-192">Choose one of hello following Docker images:</span></span>
     * <span data-ttu-id="b2959-193">**Predefined Docker image** (Image Docker prédéfinie) : spécifie une image Docker préexistante dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b2959-193">**Predefined Docker image**: Specifies a pre-existing Docker image from Azure.</span></span>

       >[!NOTE]
       ><span data-ttu-id="b2959-194">liste de Hello d’images Docker dans cette zone se compose de plusieurs images qui hello boîte à outils Azure a été configuré toopatch afin que votre objet est déployé automatiquement.</span><span class="sxs-lookup"><span data-stu-id="b2959-194">hello list of Docker images in this box consists of several images that hello Azure Toolkit has been configured toopatch so that your artifact is deployed automatically.</span></span>

     * <span data-ttu-id="b2959-195">**Custom Dockerfile** (Fichier Dockerfile personnalisé) : spécifie un fichier Dockerfile précédemment enregistré sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="b2959-195">**Custom Dockerfile**: Specifies a previously saved Dockerfile from your local computer.</span></span>

       >[!NOTE]
       ><span data-ttu-id="b2959-196">Il s’agit d’une fonctionnalité avancée pour les développeurs qui veulent toodeploy leur propre fichier Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="b2959-196">This is a more advanced feature for developers who want toodeploy their own Dockerfile.</span></span> <span data-ttu-id="b2959-197">Toutefois, c’est toodevelopers qui utilisent cette tooensure option leur Dockerfile générée correctement.</span><span class="sxs-lookup"><span data-stu-id="b2959-197">However, it is up toodevelopers who use this option tooensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="b2959-198">Hello boîte à outils Azure ne valide pas le contenu de hello dans un fichier Dockerfile personnalisé, afin de hello déploiement risque d’échouer si hello Dockerfile présente des problèmes.</span><span class="sxs-lookup"><span data-stu-id="b2959-198">hello Azure Toolkit does not validate hello content in a custom Dockerfile, so hello deployment might fail if hello Dockerfile has issues.</span></span> <span data-ttu-id="b2959-199">En outre, hello boîte à outils Azure attend hello personnalisé Dockerfile toocontain un artefact d’application web, et il va tenter de tooopen une connexion HTTP.</span><span class="sxs-lookup"><span data-stu-id="b2959-199">In addition, hello Azure Toolkit expects hello custom Dockerfile toocontain a web app artifact, and it will attempt tooopen an HTTP connection.</span></span> <span data-ttu-id="b2959-200">Si les développeurs publient un autre type d’artefact, ils peuvent recevoir des erreurs sans effet après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="b2959-200">If developers publish a different type of artifact, they may receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="b2959-201">c.</span><span class="sxs-lookup"><span data-stu-id="b2959-201">c.</span></span> <span data-ttu-id="b2959-202">**Paramètres de port**: entrez la liaison de port TCP unique hello pour votre conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="b2959-202">**Port settings**: Enter hello unique TCP port binding for your Docker container.</span></span>

     ![fenêtre de Hello configurer hello Docker conteneur toobe créé][PUB08]

10. <span data-ttu-id="b2959-204">Une fois que vous avez effectué toutes les étapes précédentes de hello, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="b2959-204">After you have completed all of hello preceding steps, click **Finish**.</span></span>

<span data-ttu-id="b2959-205">Hello boîte à outils Azure commence à déployer votre tooAzure d’application web dans un conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="b2959-205">hello Azure Toolkit begins deploying your web app tooAzure in a Docker container.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b2959-206">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b2959-206">Next steps</span></span>
<span data-ttu-id="b2959-207">Pour plus d’informations sur hello boîtes à outils Azure pour Java IDE, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="b2959-207">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="b2959-208">[boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b2959-208">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b2959-209">[Nouveautés de hello boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b2959-209">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b2959-210">[Lors de l’installation hello boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b2959-210">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b2959-211">[Instructions de connexion pour hello boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b2959-211">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b2959-212">[Créer une application web Hello World pour Azure dans Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b2959-212">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="b2959-213">[Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b2959-213">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b2959-214">[Quelles sont les nouveautés Bonjour Azure Toolkit pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b2959-214">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b2959-215">[Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b2959-215">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b2959-216">[Instructions d’authentification pour hello boîte à outils Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b2959-216">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b2959-217">[Créer une application web Hello World pour Azure dans IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b2959-217">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="b2959-218">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez [Centre de développement Java pour Azure] et [Outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="b2959-218">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="b2959-219">Pour obtenir des ressources supplémentaires pour Docker, consultez officielle de hello [site Web de Docker].</span><span class="sxs-lookup"><span data-stu-id="b2959-219">For additional resources for Docker, see hello official [Docker website].</span></span>

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