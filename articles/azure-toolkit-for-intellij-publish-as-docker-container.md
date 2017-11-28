---
title: Publier un conteneur Docker avec le kit de ressources Azure pour IntelliJ | Microsoft Docs
description: "Découvrez comment publier une application web sur Microsoft Azure en tant que conteneur Docker à l’aide du kit de ressources Azure pour IntelliJ."
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
ms.openlocfilehash: 96680319a6c4c0f0a4673cd6303a5b172f428797
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="cbcd2-103">Publier une application web en tant que conteneur Docker à l’aide du kit de ressources Azure pour IntelliJ</span><span class="sxs-lookup"><span data-stu-id="cbcd2-103">Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="cbcd2-104">Les conteneurs Docker constituent une méthode largement utilisée pour déployer des applications web.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="cbcd2-105">En utilisant des conteneurs Docker, les développeurs peuvent regrouper tous les fichiers et dépendances de leur projet en un même package pour un déploiement sur un serveur.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="cbcd2-106">Le kit de ressources Azure pour IntelliJ simplifie ce processus pour les développeurs Java en ajoutant des fonctionnalités pour *publier en tant que conteneur Docker* permettant le déploiement sur Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-106">The Azure Toolkit for IntelliJ simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment to Microsoft Azure.</span></span> <span data-ttu-id="cbcd2-107">Cet article vous guide à travers les étapes nécessaires à la publication de vos applications sur Azure en tant que conteneurs Docker.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-107">This article walks you through the steps required to publish your applications to Azure as Docker containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="cbcd2-108">Vous pouvez trouver plus d’informations sur Docker sur le [site web de Docker].</span><span class="sxs-lookup"><span data-stu-id="cbcd2-108">More information about Docker is available on the [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="cbcd2-109">Publier votre application web sur Azure en utilisant un conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="cbcd2-109">Publish your web app to Azure by using a Docker container</span></span>

> [!NOTE]
> * <span data-ttu-id="cbcd2-110">Pour publier votre application web, vous devrez créer un artefact prêt pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-110">To publish your web app, you must create a deployment-ready artifact.</span></span> <span data-ttu-id="cbcd2-111">Pour plus d’informations, consultez la section [Informations supplémentaires sur la création d’artefacts](#artifacts).</span><span class="sxs-lookup"><span data-stu-id="cbcd2-111">To learn more, see the [Additional information about creating artifacts](#artifacts) section.</span></span>
>
> * <span data-ttu-id="cbcd2-112">Une fois que vous avez utilisé l’Assistant de déploiement au moins une fois, la plupart de vos paramètres sont utilisés comme valeurs par défaut quand vous réexécutez l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-112">After you have completed the deployment wizard at least once, most of your settings are used as defaults when you run the wizard again.</span></span>
>

1. <span data-ttu-id="cbcd2-113">Ouvrez votre projet d’application web dans IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-113">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="cbcd2-114">Pour démarrer l’Assistant **Publish as Docker Container** (Publication en tant que conteneur Docker), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="cbcd2-114">To start the **Publish as Docker Container** wizard, do either of the following:</span></span>

   * <span data-ttu-id="cbcd2-115">Dans la fenêtre de l’outil **Project** (Projet), cliquez avec le bouton droit sur votre projet, cliquez sur **Azure** puis sur **Publish as Docker Container** (Publier en tant que conteneur Docker) :</span><span class="sxs-lookup"><span data-stu-id="cbcd2-115">In the **Project** tool window, right-click your project, click **Azure**, and then click **Publish as Docker Container**:</span></span>

      ![Commande Publish as Docker Container (Publier en tant que conteneur Docker)][PUB01]

   * <span data-ttu-id="cbcd2-117">Dans la barre d’outils IntelliJ, cliquez sur le bouton **Publish Group** (Publier le groupe) puis cliquez sur **Publish as Docker Container** (Publier en tant que conteneur Docker) :</span><span class="sxs-lookup"><span data-stu-id="cbcd2-117">On the IntelliJ toolbar, click the **Publish Group** button, and then click **Publish as Docker Container**:</span></span>

      <span data-ttu-id="cbcd2-118">![Commande Publish as Docker Container (Publier en tant que conteneur Docker)][PUB02]</span><span class="sxs-lookup"><span data-stu-id="cbcd2-118">![The Publish as Docker Container command][PUB02]</span></span>  
    <span data-ttu-id="cbcd2-119">L’Assistant **Deploy Docker Container on Azure** (Déploiement d’un conteneur Docker sur Azure) s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-119">The **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![Assistant Deploy Docker Container on Azure (Déploiement d’un conteneur Docker sur Azure)][PUB03]

3. <span data-ttu-id="cbcd2-121">Dans la fenêtre **Type an image name, select the artifact’s path and check a Docker host to be used** (Tapez un nom d’image, sélectionnez le chemin de l’artefact et indiquez un hôte Docker à utiliser), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="cbcd2-121">In the **Type an image name, select the artifact's path and check a Docker host to be used** window, do the following:</span></span> 

   <span data-ttu-id="cbcd2-122">a.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-122">a.</span></span> <span data-ttu-id="cbcd2-123">Dans la zone **Docker image name** (Nom de l’image Docker), entrez un nom unique pour votre hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-123">In the **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="cbcd2-124">(L’Assistant crée automatiquement un nom, mais vous pouvez le modifier.)</span><span class="sxs-lookup"><span data-stu-id="cbcd2-124">(The wizard automatically creates a name, but you can modify it.)</span></span> 

   <span data-ttu-id="cbcd2-125">b.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-125">b.</span></span> <span data-ttu-id="cbcd2-126">La zone **Hosts** (Hôtes) affiche tous les hôtes Docker que vous avez déjà créés.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-126">The **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="cbcd2-127">Effectuez l’une des actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="cbcd2-127">Do either of the following:</span></span> 
      * <span data-ttu-id="cbcd2-128">Si vous avez un hôte Docker existant, vous pouvez déployer votre application web sur celui-ci.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-128">If you have an existing Docker host, you can deploy your web app to it.</span></span>
      * <span data-ttu-id="cbcd2-129">Pour créer un hôte Docker, cliquez sur le signe plus de couleur verte (**+**).</span><span class="sxs-lookup"><span data-stu-id="cbcd2-129">To create a Docker host, click the green plus sign (**+**).</span></span>  
       <span data-ttu-id="cbcd2-130">La boîte de dialogue **Create Docker Host** (Créer un hôte Docker) s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-130">The **Create Docker Host** dialog box opens.</span></span> 

      ![Assistant Deploy Docker Container on Azure (Déploiement d’un conteneur Docker sur Azure)][PUB04a]

4. <span data-ttu-id="cbcd2-132">Dans la fenêtre **Configure the new virtual machine** (Configurer la nouvelle machine virtuelle), fournissez les informations suivantes sur votre hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-132">In the **Configure the new virtual machine** window, provide the following information about your Docker host.</span></span> <span data-ttu-id="cbcd2-133">(L’Assistant génère automatiquement la plupart des informations pour vous, mais vous pouvez les modifier.)</span><span class="sxs-lookup"><span data-stu-id="cbcd2-133">(The wizard automatically generates most of the information for you, but you can modify any of them.)</span></span> 

   <span data-ttu-id="cbcd2-134">a.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-134">a.</span></span> <span data-ttu-id="cbcd2-135">Dans la zone **Name** (Nom), entrez un nom unique pour votre hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-135">In the **Name** box, enter a unique name for the Docker host.</span></span> <span data-ttu-id="cbcd2-136">(Ce n’est pas le même que le nom de l’image Docker que vous avez spécifié précédemment.)</span><span class="sxs-lookup"><span data-stu-id="cbcd2-136">(It is not the same as the Docker image name that you specified earlier.)</span></span> 
    
   <span data-ttu-id="cbcd2-137">b.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-137">b.</span></span> <span data-ttu-id="cbcd2-138">Dans la zone **Subscription** (Abonnement), entrez l’abonnement Azure que vous utilisez pour votre hôte.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-138">In the **Subscription** box, enter the Azure subscription that you use for your host.</span></span> 
      
   <span data-ttu-id="cbcd2-139">c.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-139">c.</span></span> <span data-ttu-id="cbcd2-140">Dans la zone **Region** (Région), entrez la région géographique où se trouve votre hôte.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-140">In the **Region** box, enter the geographical region where your host is located.</span></span>
      
   <span data-ttu-id="cbcd2-141">d.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-141">d.</span></span> <span data-ttu-id="cbcd2-142">Sous l’onglet **OS and Size** (Système d’exploitation et taille), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="cbcd2-142">On the **OS and Size** tab, do the following:</span></span>      
      * <span data-ttu-id="cbcd2-143">**Host OS** (Système d’exploitation de l’hôte) : entrez le système d’exploitation de la machine virtuelle qui contient votre hôte.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-143">**Host OS**: Enter the operating system for the virtual machine that contains your host.</span></span> 
      * <span data-ttu-id="cbcd2-144">**Size** (Taille) : entrez la taille de la machine virtuelle de votre hôte.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-144">**Size**: Enter the virtual-machine size for your host.</span></span>   
       
   <span data-ttu-id="cbcd2-145">e.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-145">e.</span></span> <span data-ttu-id="cbcd2-146">Sous l’onglet **Resource Group** (Groupe de ressources), sélectionnez une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="cbcd2-146">On the **Resource Group** tab, select either of the following:</span></span>      
      * <span data-ttu-id="cbcd2-147">**New resource group** (Nouveau groupe de ressources) : créez un groupe de ressources pour votre hôte.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-147">**New resource group**: Create a resource group for your host.</span></span>
      * <span data-ttu-id="cbcd2-148">**Existing resource group** (Groupe de ressources existant) : spécifiez un groupe de ressources existant dans votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-148">**Existing resource group**: Specify an existing resource group from your Azure account.</span></span> 
       
   <span data-ttu-id="cbcd2-149">f.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-149">f.</span></span> <span data-ttu-id="cbcd2-150">Sous l’onglet **Network** (Réseau), sélectionnez une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="cbcd2-150">On the **Network** tab, select either of the following:</span></span>      
      * <span data-ttu-id="cbcd2-151">**New virtual network** (Nouveau réseau virtuel) : créez un réseau virtuel pour votre hôte.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-151">**New virtual network**: Create a virtual network for your host.</span></span>
      * <span data-ttu-id="cbcd2-152">**Existing virtual network** (Réseau virtuel existant) : spécifiez un réseau virtuel existant dans votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-152">**Existing virtual network**: Specify an existing virtual network from your Azure account.</span></span> 
       
   <span data-ttu-id="cbcd2-153">g.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-153">g.</span></span> <span data-ttu-id="cbcd2-154">Sous l’onglet **Storage** (Stockage), sélectionnez une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="cbcd2-154">On the **Storage** tab, select either of the following:</span></span>      
      * <span data-ttu-id="cbcd2-155">**New storage account** (Nouveau compte de stockage) : créez un compte de stockage pour votre hôte.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-155">**New storage account**: Create a storage account for your host.</span></span>
      * <span data-ttu-id="cbcd2-156">**Compte de stockage existant** : spécifiez un compte de stockage existant dans votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-156">**Existing storage account**: Specify an existing storage account from your Azure account.</span></span>
       
5. <span data-ttu-id="cbcd2-157">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-157">Click **Next**.</span></span>  
     <span data-ttu-id="cbcd2-158">La fenêtre **Configure log in credentials and port settings** (Configurer les informations d’identification de connexion et les paramètres de port) s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-158">The **Configure log in credentials and port settings** window opens.</span></span>

      ![La fenêtre Configure log in credentials and port settings (Configurer les informations d’identification de connexion et les paramètres de port)][PUB05]

6. <span data-ttu-id="cbcd2-160">Sélectionnez l’une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="cbcd2-160">Select one of the following options:</span></span>

      * <span data-ttu-id="cbcd2-161">**Import credentials from Azure Key Vault** (Importer des informations d’identification depuis Azure Key Vault) : spécifiez un ensemble d’informations d’identification précédemment enregistré et stocké dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-161">**Import credentials from Azure Key Vault**: Specify a previously saved set of credentials that are stored in your Azure subscription.</span></span>

          > [!NOTE]
          > <span data-ttu-id="cbcd2-162">Un coffre de clés Azure créé avec un compte ou un principal de service spécifique n’est pas automatiquement accessible par un autre compte ou principal de service qui partage l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-162">An Azure key vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares the subscription.</span></span> <span data-ttu-id="cbcd2-163">Pour permettre à un autre compte ou principal de service d’utiliser le coffre de clés, vous devez utiliser le portail Azure pour ajouter le compte ou le principal de service.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-163">To allow another account or service principal to use the key vault, you must use the Azure portal to add the account or service principal.</span></span>

      * <span data-ttu-id="cbcd2-164">**New log in credentials** (Nouvelles informations d’identification de connexion) : créez un nouvel ensemble d’informations d’identification de connexion.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-164">**New log in credentials**: Create a new set of login credentials.</span></span> <span data-ttu-id="cbcd2-165">Si vous sélectionnez cette option, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="cbcd2-165">If you select this option, do the following:</span></span>

        <span data-ttu-id="cbcd2-166">a.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-166">a.</span></span> <span data-ttu-id="cbcd2-167">Sous l’onglet **Informations d’identification de la machine virtuelle**, renseignez les informations suivantes pour les informations d’identification de connexion de la machine virtuelle de votre hôte Docker : * **Nom d’utilisateur** : entrez le nom d’utilisateur pour les informations d’identification de connexion de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-167">On the **VM Credentials** tab, provide the following information for the virtual-machine login credentials of your Docker host: * **Username**: Enter the username for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="cbcd2-168">* **Password** (Mot de passe) et **Confirm** (Confirmer) : entrez le mot de passe pour les informations d’identification de connexion de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-168">* **Password** and **Confirm**: Enter the password for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="cbcd2-169">* **SSH** : entrez les paramètres SSH (Secure Shell) pour votre hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-169">* **SSH**: Enter the Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="cbcd2-170">Vous pouvez sélectionner une des options suivantes : * **Aucun** : spécifie que votre machine virtuelle n’autorise pas les connexions SSH.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-170">You can select one of the following options: * **None**: Specifies that your virtual machine does not allow SSH connections.</span></span>
                <span data-ttu-id="cbcd2-171">* **Auto-generate** (Générer automatiquement) : crée automatiquement les paramètres nécessaires pour la connexion via SSH.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-171">* **Auto-generate**: Automatically creates the requisite settings for connecting via SSH.</span></span>
                <span data-ttu-id="cbcd2-172">* **Import from directory** (Importer à partir du répertoire) : vous permet de spécifier un répertoire qui contient un jeu de paramètres SSH précédemment enregistrés.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-172">* **Import from directory**: Allows you to specify a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="cbcd2-173">Le répertoire doit contenir les deux fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="cbcd2-173">The directory must contain the following two files:</span></span>
                
                  * *id_rsa*: Contains the RSA identification for a user.
                  * *id_rsa.pub*: Contains the RSA public key that is used for authentication.
            
        <span data-ttu-id="cbcd2-174">b.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-174">b.</span></span> <span data-ttu-id="cbcd2-175">Sous l’onglet **Docker Daemon Access** (Accès au démon Docker), fournissez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="cbcd2-175">On the **Docker Daemon Access** tab, provide the following information:</span></span>

          ![Créer un hôte Docker][PUB06]
    
             * **Docker Daemon port**: Enter the unique TCP port for your Docker host.
             * **TLS Security**: Enter the Transport Layer Security settings for your Docker host. You can choose from the following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates the requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. The directory must contain the following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain the client certificate and public key that is used for TLS authentication.

7. <span data-ttu-id="cbcd2-177">Après avoir entré les informations nécessaires, cliquez sur **Finish** (Terminer).</span><span class="sxs-lookup"><span data-stu-id="cbcd2-177">After you have entered the required information, click **Finish**.</span></span>  
    <span data-ttu-id="cbcd2-178">L’Assistant **Deploy Docker Container on Azure** (Déploiement d’un conteneur Docker sur Azure) réapparaît.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-178">The **Deploy Docker Container on Azure** wizard reappears.</span></span>

   ![Assistant Deploy Docker Container on Azure (Déploiement d’un conteneur Docker sur Azure)][PUB07]

8. <span data-ttu-id="cbcd2-180">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-180">Click **Next**.</span></span>  
    <span data-ttu-id="cbcd2-181">La fenêtre **Configure the Docker container to be created** (Configurer le conteneur Docker à créer) s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-181">The **Configure the Docker container to be created** window opens.</span></span>

   ![La fenêtre Configure the Docker container to be created (Configurer le conteneur Docker à créer)][PUB08]

9. <span data-ttu-id="cbcd2-183">Dans la fenêtre **Configure the Docker container to be created** (Configurer le conteneur Docker à créer), fournissez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="cbcd2-183">In the **Configure the Docker container to be created** window, provide the following information:</span></span> 

   <span data-ttu-id="cbcd2-184">a.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-184">a.</span></span> <span data-ttu-id="cbcd2-185">Dans la zone **Docker container name** (Nom du conteneur Docker), entrez un nom unique pour votre conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-185">In the **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="cbcd2-186">b.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-186">b.</span></span> <span data-ttu-id="cbcd2-187">Choisissez l’une des images Docker suivantes :</span><span class="sxs-lookup"><span data-stu-id="cbcd2-187">Choose one of the following Docker images:</span></span> 

      * <span data-ttu-id="cbcd2-188">**Predefined Docker image** (Image Docker prédéfinie) : spécifiez une image Docker préexistante dans Azure.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-188">**Predefined Docker image**: Specify a pre-existing Docker image from Azure.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="cbcd2-189">La liste des images Docker dans cette zone est constituée de plusieurs images configurées pour application d’un correctif par le kit de ressources Azure afin que votre artefact soit déployé automatiquement.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-189">The list of Docker images in this box consists of several images that the Azure Toolkit has been configured to patch so that your artifact is deployed automatically.</span></span> 

      * <span data-ttu-id="cbcd2-190">**Custom Dockerfile** (Fichier Dockerfile personnalisé) : spécifiez un fichier Dockerfile précédemment enregistré sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-190">**Custom Dockerfile**: Specify a previously saved Dockerfile from your local computer.</span></span>

        > [!NOTE]
        > <span data-ttu-id="cbcd2-191">Il s’agit d’une fonctionnalité plus avancée destinée aux développeurs qui veulent déployer leur propre fichier Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-191">This is a more advanced feature for developers who want to deploy their own Dockerfile.</span></span> <span data-ttu-id="cbcd2-192">Toutefois, les développeurs qui utilisent cette option doivent s’assurer que leur fichier Docker est construit correctement.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-192">However, it is up to developers who use this option to ensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="cbcd2-193">Comme le kit de ressources Azure ne valide pas le contenu d’un fichier Dockerfile personnalisé, le déploiement peut échouer si le fichier Dockerfile présente des problèmes.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-193">Because the Azure Toolkit does not validate the content in a custom Dockerfile, the deployment might fail if the Dockerfile has issues.</span></span> <span data-ttu-id="cbcd2-194">En outre, comme la boîte à outils Azure attend que le fichier Dockerfile personnalisé contienne un artefact d’application web, il tente d’ouvrir une connexion HTTP.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-194">In addition, because the Azure Toolkit expects the custom Dockerfile to contain a web app artifact, it attempts to open an HTTP connection.</span></span> <span data-ttu-id="cbcd2-195">Si les développeurs publier un autre type d’artefact, ils peuvent recevoir des erreurs sans effet après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-195">If developers publish a different type of artifact, they might receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="cbcd2-196">c.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-196">c.</span></span> <span data-ttu-id="cbcd2-197">Dans la zone **Port settings** (Paramètres de port), entrez la liaison de port TCP unique pour votre conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-197">In the **Port settings** box, enter the unique TCP port binding for your Docker container.</span></span> 

10. <span data-ttu-id="cbcd2-198">Après avoir terminé les étapes précédentes, cliquez sur **Finish** (Terminer).</span><span class="sxs-lookup"><span data-stu-id="cbcd2-198">After you have completed the preceding steps, click **Finish**.</span></span> 

<span data-ttu-id="cbcd2-199">Le kit de ressources Azure commence le déploiement de votre application web sur Azure dans un conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-199">The Azure Toolkit begins deploying your web app to Azure in a Docker container.</span></span> <span data-ttu-id="cbcd2-200">Sauf si vous avez configuré le déploiement d’IntelliJ en arrière-plan, une barre de progression **Deploying to Azure** (Déploiement sur Azure) s’affiche.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-200">Unless you have configured IntelliJ to be deployed in the background, a **Deploying to Azure** progress bar appears.</span></span> 

![La barre de progression du déploiement][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a><span data-ttu-id="cbcd2-202">Informations supplémentaires sur la création d’artefacts</span><span class="sxs-lookup"><span data-stu-id="cbcd2-202">Additional information about creating artifacts</span></span>

<span data-ttu-id="cbcd2-203">Pour créer un artefact prêt pour le déploiement, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="cbcd2-203">To create a deployment-ready artifact, do the following:</span></span>

1. <span data-ttu-id="cbcd2-204">Ouvrez votre projet d’application web dans IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-204">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="cbcd2-205">Cliquez sur **Fichier**, puis sur **Structure de projet**.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-205">Click **File**, and then click **Project Structure**.</span></span>

   ![La commande Structure de projet][ART01]

3. <span data-ttu-id="cbcd2-207">Pour ajouter un artefact, cliquez sur le signe plus de couleur verte (**+**) puis cliquez sur **Web Application: Archive** (Application web : Archive).</span><span class="sxs-lookup"><span data-stu-id="cbcd2-207">To add an artifact, click the green plus sign (**+**), and then click **Web Application: Archive**.</span></span>

   ![La commande Web Application: Archive (Application web : Archive)][ART02]

4. <span data-ttu-id="cbcd2-209">Dans la zone **Name** (Nom), entrez un nom pour votre artefact (n’incluez pas l’extension *.war*) puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-209">In the **Name** box, enter a name for your artifact (do not include the *.war* extension), and then click **OK**.</span></span>

   ![La zone Name (Nom) de l’artefact][ART03]

<span data-ttu-id="cbcd2-211">Pour plus d’informations sur la création d’artefacts dans IntelliJ, consultez [Configuring artifacts] sur le site web de JetBrains.</span><span class="sxs-lookup"><span data-stu-id="cbcd2-211">For more information about creating artifacts in IntelliJ, see [Configuring artifacts] on the JetBrains website.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbcd2-212">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cbcd2-212">Next steps</span></span>
<span data-ttu-id="cbcd2-213">Pour plus d’informations sur les kits d’outils Azure pour les environnements de développement Java, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="cbcd2-213">For more information about the Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="cbcd2-214">[Kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="cbcd2-214">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="cbcd2-215">[Nouveautés du Kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="cbcd2-215">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="cbcd2-216">[Installation du kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="cbcd2-216">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="cbcd2-217">[Instructions de connexion pour le Kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="cbcd2-217">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="cbcd2-218">[Créer une application web Hello World pour Azure dans Eclipse]</span><span class="sxs-lookup"><span data-stu-id="cbcd2-218">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="cbcd2-219">[Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="cbcd2-219">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="cbcd2-220">[Nouveautés du Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="cbcd2-220">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="cbcd2-221">[Installation du kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="cbcd2-221">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="cbcd2-222">[Instructions de connexion pour le Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="cbcd2-222">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="cbcd2-223">[Créer une application web Hello World pour Azure dans IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="cbcd2-223">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="cbcd2-224">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez le [Centre de développement Java pour Azure] et les [outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="cbcd2-224">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="cbcd2-225">Pour obtenir des ressources supplémentaires pour Docker, consultez le [site web de Docker].</span><span class="sxs-lookup"><span data-stu-id="cbcd2-225">For additional resources for Docker, see the official [Docker website].</span></span>

<!-- URL List -->

<span data-ttu-id="cbcd2-226">[Kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="cbcd2-226">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="cbcd2-227">[Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="cbcd2-227">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="cbcd2-228">[Créer une application web Hello World pour Azure dans Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="cbcd2-228">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="cbcd2-229">[Créer une application web Hello World pour Azure dans IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="cbcd2-229">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="cbcd2-230">[Installation du kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="cbcd2-230">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="cbcd2-231">[Installation du kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="cbcd2-231">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="cbcd2-232">[Instructions de connexion pour le Kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="cbcd2-232">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="cbcd2-233">[Instructions de connexion pour le Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="cbcd2-233">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="cbcd2-234">[Nouveautés du Kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="cbcd2-234">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="cbcd2-235">[Nouveautés du Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="cbcd2-235">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="cbcd2-236">[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="cbcd2-236">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="cbcd2-237">[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="cbcd2-237">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="cbcd2-238">[site web de Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="cbcd2-238">[Docker website]: https://www.docker.com/</span></span>
<span data-ttu-id="cbcd2-239">[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html</span><span class="sxs-lookup"><span data-stu-id="cbcd2-239">[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html</span></span>

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
