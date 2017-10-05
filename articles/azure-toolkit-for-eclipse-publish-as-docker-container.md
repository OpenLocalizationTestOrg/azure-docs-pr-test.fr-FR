---
title: Publier un conteneur Docker avec le kit de ressources Azure pour Eclipse | Microsoft Docs
description: "Découvrez comment publier une application web sur Microsoft Azure en tant que conteneur Docker à l’aide du kit de ressources Azure pour Eclipse."
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
ms.openlocfilehash: 746bb0a073396b84fa8592adda6748a2a5692ee8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="1b99f-103">Publier une application web en tant que conteneur Docker à l’aide du kit de ressources Azure pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="1b99f-103">Publish a web app as a Docker container by using the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="1b99f-104">Les conteneurs Docker constituent une méthode largement utilisée pour déployer des applications web.</span><span class="sxs-lookup"><span data-stu-id="1b99f-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="1b99f-105">En utilisant des conteneurs Docker, les développeurs peuvent regrouper tous les fichiers et dépendances de leur projet en un même package pour un déploiement sur un serveur.</span><span class="sxs-lookup"><span data-stu-id="1b99f-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="1b99f-106">Le kit de ressources Azure pour Eclipse simplifie ce processus pour les développeurs Java en ajoutant des fonctionnalités pour *publier en tant que conteneur Docker* permettant le déploiement sur Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1b99f-106">The Azure Toolkit for Eclipse simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment to Microsoft Azure.</span></span> <span data-ttu-id="1b99f-107">Cet article vous guide à travers les étapes nécessaires à la publication de vos applications sur Azure en tant que conteneurs Docker.</span><span class="sxs-lookup"><span data-stu-id="1b99f-107">This article walks you through the steps required to publish your applications to Azure as Docker containers.</span></span>

> [!NOTE]
> <span data-ttu-id="1b99f-108">Vous pouvez trouver plus d’informations sur Docker sur le [site web de Docker].</span><span class="sxs-lookup"><span data-stu-id="1b99f-108">More information about Docker is available on the [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="1b99f-109">Publier votre application web sur Azure en utilisant un conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="1b99f-109">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="1b99f-110">Ouvrez votre projet d’application web dans Eclipse.</span><span class="sxs-lookup"><span data-stu-id="1b99f-110">Open your web app project in Eclipse.</span></span>

2. <span data-ttu-id="1b99f-111">Pour démarrer l’Assistant **Publish as Docker Container** (Publication en tant que conteneur Docker), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1b99f-111">To start the **Publish as Docker Container** wizard, do either of the following:</span></span>

   * <span data-ttu-id="1b99f-112">Dans la vue **Navigator** (Navigateur), cliquez avec le bouton droit sur votre projet, cliquez sur **Azure** puis sur **Publish as Docker Container** (Publier en tant que conteneur Docker).</span><span class="sxs-lookup"><span data-stu-id="1b99f-112">In the **Navigator** view, right-click your project, click **Azure**, and then click **Publish as Docker Container**.</span></span>

      ![Commande Publish as Docker Container (Publier en tant que conteneur Docker) de la vue Navigator (Navigateur)][PUB01]

   * <span data-ttu-id="1b99f-114">Dans la barre d’outils Eclipse, cliquez sur le bouton **Publish** (Publier) puis cliquez sur **Publish as Docker Container** (Publier en tant que conteneur Docker).</span><span class="sxs-lookup"><span data-stu-id="1b99f-114">On the Eclipse toolbar, click the **Publish** button, and then click **Publish as Docker Container**.</span></span>

      ![Commande Publier en tant que conteneur Docker de la barre d’outils Eclipse][PUB02]
      
    <span data-ttu-id="1b99f-116">L’Assistant **Deploy Docker Container on Azure** (Déploiement d’un conteneur Docker sur Azure) s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="1b99f-116">The **Deploy Docker Container on Azure** wizard opens.</span></span>

    ![Assistant Deploy Docker Container on Azure (Déploiement d’un conteneur Docker sur Azure)][PUB03]

3. <span data-ttu-id="1b99f-118">Dans la fenêtre **Type an image name, select the artifact’s path and check a Docker host to be used** (Tapez un nom d’image, sélectionnez le chemin de l’artefact et indiquez un hôte Docker à utiliser), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1b99f-118">In the **Type an image name, select the artifact's path and check a Docker host to be used** window, do the following:</span></span>

    <span data-ttu-id="1b99f-119">a.</span><span class="sxs-lookup"><span data-stu-id="1b99f-119">a.</span></span> <span data-ttu-id="1b99f-120">Dans la zone **Docker image name** (Nom de l’image Docker), entrez un nom unique pour votre hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="1b99f-120">In the **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="1b99f-121">(L’Assistant crée automatiquement un nom, mais vous pouvez le modifier.)</span><span class="sxs-lookup"><span data-stu-id="1b99f-121">(The wizard automatically creates a name, but you can modify it.)</span></span>

    <span data-ttu-id="1b99f-122">b.</span><span class="sxs-lookup"><span data-stu-id="1b99f-122">b.</span></span> <span data-ttu-id="1b99f-123">La zone **Hosts** (Hôtes) affiche tous les hôtes Docker que vous avez déjà créés.</span><span class="sxs-lookup"><span data-stu-id="1b99f-123">The **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="1b99f-124">Effectuez l’une des actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b99f-124">Do either of the following:</span></span>

    * <span data-ttu-id="1b99f-125">Si vous avez un hôte Docker existant, vous pouvez déployer votre application web sur celui-ci.</span><span class="sxs-lookup"><span data-stu-id="1b99f-125">If you have an existing Docker host, you can deploy your web app to it.</span></span>
    * <span data-ttu-id="1b99f-126">Pour créer un hôte Docker, cliquez sur **Add** (Ajouter).</span><span class="sxs-lookup"><span data-stu-id="1b99f-126">To create a new Docker host, click **Add**.</span></span>  
      
    <span data-ttu-id="1b99f-127">La boîte de dialogue **Create Docker Host** (Créer un hôte Docker) s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="1b99f-127">The **Create Docker Host** dialog box opens.</span></span>

    ![Assistant Deploy Docker Container on Azure (Déployer un conteneur Docker dans Azure)][PUB04a]

4. <span data-ttu-id="1b99f-129">Dans la fenêtre **Configure the new virtual machine** (Configurer la nouvelle machine virtuelle), spécifiez les options suivantes pour votre hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="1b99f-129">In the **Configure the new virtual machine** window, specify the following options for your Docker host.</span></span> <span data-ttu-id="1b99f-130">(L’Assistant génère automatiquement la plupart des options pour vous, mais vous pouvez les modifier.)</span><span class="sxs-lookup"><span data-stu-id="1b99f-130">(The wizard automatically generates most of the options for you, but you can modify any of them.)</span></span>

   <span data-ttu-id="1b99f-131">a.</span><span class="sxs-lookup"><span data-stu-id="1b99f-131">a.</span></span> <span data-ttu-id="1b99f-132">**Name** (Nom) : entrez un nom unique pour l’hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="1b99f-132">**Name**: Enter a unique name for the Docker host.</span></span> <span data-ttu-id="1b99f-133">(Ce n’est pas le même que le nom de l’image Docker que vous avez spécifié précédemment.)</span><span class="sxs-lookup"><span data-stu-id="1b99f-133">(It is not the same as the Docker image name that you specified earlier.)</span></span>

   <span data-ttu-id="1b99f-134">b.</span><span class="sxs-lookup"><span data-stu-id="1b99f-134">b.</span></span> <span data-ttu-id="1b99f-135">**Subscription** (Abonnement) : entrez l’abonnement Azure que vous utilisez pour votre hôte.</span><span class="sxs-lookup"><span data-stu-id="1b99f-135">**Subscription**: Enter the Azure subscription that you use for your host.</span></span>

   <span data-ttu-id="1b99f-136">c.</span><span class="sxs-lookup"><span data-stu-id="1b99f-136">c.</span></span> <span data-ttu-id="1b99f-137">**Region** (Région) : entrez la région géographique où se trouve votre hôte.</span><span class="sxs-lookup"><span data-stu-id="1b99f-137">**Region**: Enter the geographical region where your host is located.</span></span>

   <span data-ttu-id="1b99f-138">d.</span><span class="sxs-lookup"><span data-stu-id="1b99f-138">d.</span></span> <span data-ttu-id="1b99f-139">Dans l’onglet **Host OS and Size** (Système d’exploitation et taille de l’hôte) :</span><span class="sxs-lookup"><span data-stu-id="1b99f-139">On the **Host OS and Size** tab:</span></span>
     * <span data-ttu-id="1b99f-140">**Host OS** (Système d’exploitation de l’hôte) : entrez le système d’exploitation de la machine virtuelle qui contient votre hôte.</span><span class="sxs-lookup"><span data-stu-id="1b99f-140">**Host OS**: Enter the operating system for the virtual machine that contains your host.</span></span>
     * <span data-ttu-id="1b99f-141">**Size** (Taille) : entrez la taille de la machine virtuelle de votre hôte.</span><span class="sxs-lookup"><span data-stu-id="1b99f-141">**Size**: Enter the virtual-machine size for your host.</span></span>

   <span data-ttu-id="1b99f-142">e.</span><span class="sxs-lookup"><span data-stu-id="1b99f-142">e.</span></span> <span data-ttu-id="1b99f-143">Dans l’onglet **Groupe de ressources** :</span><span class="sxs-lookup"><span data-stu-id="1b99f-143">On the **Resource Group** tab:</span></span>
     * <span data-ttu-id="1b99f-144">**New resource group** (Nouveau groupe de ressources) : créez un groupe de ressources pour votre hôte.</span><span class="sxs-lookup"><span data-stu-id="1b99f-144">**New resource group**: Create a new resource group for your host.</span></span>
     * <span data-ttu-id="1b99f-145">**Existing resource group** (Groupe de ressources existant) : entrez un groupe de ressources existant dans votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="1b99f-145">**Existing resource group**: Enter an existing resource group from your Azure account.</span></span>

   <span data-ttu-id="1b99f-146">f.</span><span class="sxs-lookup"><span data-stu-id="1b99f-146">f.</span></span> <span data-ttu-id="1b99f-147">Dans l’onglet **Réseau** :</span><span class="sxs-lookup"><span data-stu-id="1b99f-147">On the **Network** tab:</span></span>
     * <span data-ttu-id="1b99f-148">**New virtual network** (Nouveau réseau virtuel) : créez un réseau virtuel pour votre hôte.</span><span class="sxs-lookup"><span data-stu-id="1b99f-148">**New virtual network**: Create a new virtual network for your host.</span></span>
     * <span data-ttu-id="1b99f-149">**Existing virtual network** (Réseau virtuel existant) : entrez un réseau virtuel existant dans votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="1b99f-149">**Existing virtual network**: Enter an existing virtual network from your Azure account.</span></span>

   <span data-ttu-id="1b99f-150">g.</span><span class="sxs-lookup"><span data-stu-id="1b99f-150">g.</span></span> <span data-ttu-id="1b99f-151">Dans l’onglet **Stockage** :</span><span class="sxs-lookup"><span data-stu-id="1b99f-151">On the **Storage** tab:</span></span>
     * <span data-ttu-id="1b99f-152">**New storage account** (Nouveau compte de stockage) : créez un compte de stockage pour votre hôte.</span><span class="sxs-lookup"><span data-stu-id="1b99f-152">**New storage account**: Create a new storage account for your host.</span></span>
     * <span data-ttu-id="1b99f-153">**Existing storage account** (Compte de stockage existant) : entrez un compte de stockage existant dans votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="1b99f-153">**Existing storage account**: Enter an existing storage account from your Azure account.</span></span>

5. <span data-ttu-id="1b99f-154">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="1b99f-154">Click **Next**.</span></span>

6. <span data-ttu-id="1b99f-155">Dans la fenêtre **Configure log in credentials and port settings** (Configurer les informations d’identification de connexion et les paramètres de port), sélectionnez une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b99f-155">In the **Configure log in credentials and port settings** window, select one of the following options:</span></span>

    * <span data-ttu-id="1b99f-156">**Import credentials from Azure Key Vault** (Importer des informations d’identification depuis Azure Key Vault) : spécifie un ensemble d’informations d’identification précédemment enregistré et stocké dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="1b99f-156">**Import credentials from Azure Key Vault**: Specifies a previously saved set of credentials that are stored in your Azure subscription.</span></span>

      >[!NOTE]
      ><span data-ttu-id="1b99f-157">Un coffre de clés Azure créé avec un compte ou un principal de service spécifique n’est pas automatiquement accessible par un autre compte ou principal de service qui partage l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="1b99f-157">An Azure Key Vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares the subscription.</span></span> <span data-ttu-id="1b99f-158">Pour permettre à un autre compte ou principal de service d’utiliser le coffre de clés, vous devez utiliser le portail Azure pour ajouter le compte ou le principal de service.</span><span class="sxs-lookup"><span data-stu-id="1b99f-158">To allow another account or service principal to use the Key Vault, you must use the Azure portal to add the account or service principal.</span></span>

    * <span data-ttu-id="1b99f-159">**New log in credentials** (Nouvelles informations d’identification de connexion) : crée un nouvel ensemble d’informations d’identification de connexion.</span><span class="sxs-lookup"><span data-stu-id="1b99f-159">**New log in credentials**: Creates a new set of login credentials.</span></span> <span data-ttu-id="1b99f-160">Si vous sélectionnez cette option, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1b99f-160">If you select this option, do the following:</span></span>
    
      * <span data-ttu-id="1b99f-161">Sous l’onglet **VM Credentials** (Informations d’identification de la machine virtuelle), choisissez une des options suivantes pour les informations d’identification de connexion de la machine virtuelle de votre hôte Docker :</span><span class="sxs-lookup"><span data-stu-id="1b99f-161">On the **VM Credentials** tab, choose one of the following options for the virtual-machine login credentials of your Docker host:</span></span>

          * <span data-ttu-id="1b99f-162">**Username** (Nom d’utilisateur) : entrez le nom d’utilisateur des informations d’identification de connexion de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1b99f-162">**Username**: Enter the username for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="1b99f-163">**Password** (Mot de passe) et **Confirm** (Confirmer) : entrez le mot de passe pour les informations d’identification de connexion de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1b99f-163">**Password** and **Confirm**: Enter the password for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="1b99f-164">**SSH** : entrez les paramètres SSH (Secure Shell) pour votre hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="1b99f-164">**SSH**: Enter the Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="1b99f-165">Vous pouvez choisir parmi les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b99f-165">You can choose from the following options:</span></span>
            * <span data-ttu-id="1b99f-166">**None** (Aucun) : spécifie que votre machine virtuelle n’autorisera pas les connexions SSH.</span><span class="sxs-lookup"><span data-stu-id="1b99f-166">**None**: Specifies that your virtual machine will not allow SSH connections.</span></span>
            * <span data-ttu-id="1b99f-167">**Auto-generate** (Générer automatiquement) : crée automatiquement les paramètres nécessaire pour la connexion via SSH.</span><span class="sxs-lookup"><span data-stu-id="1b99f-167">**Auto-generate**: Automatically creates the requisite settings for connecting via SSH.</span></span>
            * <span data-ttu-id="1b99f-168">**Import from directory** (Importer à partir du répertoire) : spécifie un répertoire qui contient un jeu de paramètres SSH précédemment enregistrés.</span><span class="sxs-lookup"><span data-stu-id="1b99f-168">**Import from directory**: Specifies a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="1b99f-169">Le répertoire doit contenir les deux fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="1b99f-169">The directory must contain the following two files:</span></span>
                * <span data-ttu-id="1b99f-170">*id_rsa* : contient l’identification RSA d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1b99f-170">*id_rsa*: Contains the RSA identification for a user.</span></span>
                * <span data-ttu-id="1b99f-171">*id_rsa.pub* : contient la clé publique RSA qui est utilisée pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="1b99f-171">*id_rsa.pub*: Contains the RSA public key that is used for authentication.</span></span>
        
        ![Créer un hôte Docker][PUB05]

      * <span data-ttu-id="1b99f-173">Sous l’onglet **Docker Daemon Credentials** (Informations d’identification du démon Docker), spécifiez les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b99f-173">On the **Docker Daemon Credentials** tab, specify the following options:</span></span>

          * <span data-ttu-id="1b99f-174">**Docker Daemon port** (Port du démon Docker) : entrez le port TCP unique pour votre hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="1b99f-174">**Docker Daemon port**: Enter the unique TCP port for your Docker host.</span></span>
          * <span data-ttu-id="1b99f-175">**TLS Security** (Sécurité TLS) : entrez les paramètres TLS (Transport Layer Security) pour votre hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="1b99f-175">**TLS Security**: Enter the Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="1b99f-176">Vous pouvez choisir parmi les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b99f-176">You can choose from the following options:</span></span>
            * <span data-ttu-id="1b99f-177">**None** (Aucun) : spécifie que votre machine virtuelle n’autorisera pas les connexions TLS.</span><span class="sxs-lookup"><span data-stu-id="1b99f-177">**None**: Specifies that your virtual machine will not allow TLS connections.</span></span>
            * <span data-ttu-id="1b99f-178">**Auto-generate** (Générer automatiquement) : crée automatiquement les paramètres nécessaire pour la connexion via TLS.</span><span class="sxs-lookup"><span data-stu-id="1b99f-178">**Auto-generate**: Automatically creates the requisite settings for connecting via TLS.</span></span>
            * <span data-ttu-id="1b99f-179">**Import from directory** (Importer à partir du répertoire) : spécifie un répertoire qui contient un jeu de paramètres TLS précédemment enregistrés.</span><span class="sxs-lookup"><span data-stu-id="1b99f-179">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="1b99f-180">Plus précisément, le répertoire doit contenir les six fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="1b99f-180">More specifically, the directory must contain the following six files:</span></span>
                * <span data-ttu-id="1b99f-181">*ca.pem* et *ca-key.pem* : contiennent le certificat et la clé publique de l’autorité de certification TLS.</span><span class="sxs-lookup"><span data-stu-id="1b99f-181">*ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.</span></span>
                * <span data-ttu-id="1b99f-182">*cert.pem* et *key.pem*: contiennent le certificat client et la clé publique qui est utilisée pour l’authentification TLS.</span><span class="sxs-lookup"><span data-stu-id="1b99f-182">*cert.pem* and *key.pem*: Contain the client certificate and public key that is used for TLS authentication.</span></span>
                * <span data-ttu-id="1b99f-183">*server.pem* et *server-key.pem* : contiennent la clé publique et le certificat de serveur pour l’hôte.</span><span class="sxs-lookup"><span data-stu-id="1b99f-183">*server.pem* and *server-key.pem*: Contain the server certificate and public key for the host.</span></span>

        ![Créer un hôte Docker][PUB06]

7. <span data-ttu-id="1b99f-185">Après avoir entré toutes les informations précédentes, cliquez sur **Finish** (Terminer).</span><span class="sxs-lookup"><span data-stu-id="1b99f-185">After you have entered all of the preceding information, click **Finish**.</span></span>

8. <span data-ttu-id="1b99f-186">Dans l’Assistant **Deploy Docker Container on Azure** (Déploiement d’un conteneur Docker dans Azure), cliquez sur **Next** (Suivant).</span><span class="sxs-lookup"><span data-stu-id="1b99f-186">In the **Deploy Docker Container on Azure** wizard, click **Next**.</span></span>

   ![Assistant Deploy Docker Container on Azure (Déploiement d’un conteneur Docker sur Azure)][PUB07]

9. <span data-ttu-id="1b99f-188">Dans la fenêtre **Configure the Docker container to be created** (Configurer le conteneur Docker à créer), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1b99f-188">In the **Configure the Docker container to be created** window, do the following:</span></span>

   <span data-ttu-id="1b99f-189">a.</span><span class="sxs-lookup"><span data-stu-id="1b99f-189">a.</span></span> <span data-ttu-id="1b99f-190">Dans la zone **Docker container name** (Nom du conteneur Docker), entrez un nom unique pour votre conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="1b99f-190">In the **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="1b99f-191">b.</span><span class="sxs-lookup"><span data-stu-id="1b99f-191">b.</span></span> <span data-ttu-id="1b99f-192">Choisissez l’une des images Docker suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b99f-192">Choose one of the following Docker images:</span></span>
     * <span data-ttu-id="1b99f-193">**Predefined Docker image** (Image Docker prédéfinie) : spécifie une image Docker préexistante dans Azure.</span><span class="sxs-lookup"><span data-stu-id="1b99f-193">**Predefined Docker image**: Specifies a pre-existing Docker image from Azure.</span></span>

       >[!NOTE]
       ><span data-ttu-id="1b99f-194">La liste des images Docker dans cette zone est constituée de plusieurs images configurées pour application d’un correctif par le kit de ressources Azure afin que votre artefact soit déployé automatiquement.</span><span class="sxs-lookup"><span data-stu-id="1b99f-194">The list of Docker images in this box consists of several images that the Azure Toolkit has been configured to patch so that your artifact is deployed automatically.</span></span>

     * <span data-ttu-id="1b99f-195">**Custom Dockerfile** (Fichier Dockerfile personnalisé) : spécifie un fichier Dockerfile précédemment enregistré sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="1b99f-195">**Custom Dockerfile**: Specifies a previously saved Dockerfile from your local computer.</span></span>

       >[!NOTE]
       ><span data-ttu-id="1b99f-196">Il s’agit d’une fonctionnalité plus avancée destinée aux développeurs qui souhaitent déployer leur propre fichier Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="1b99f-196">This is a more advanced feature for developers who want to deploy their own Dockerfile.</span></span> <span data-ttu-id="1b99f-197">Toutefois, les développeurs qui utilisent cette option doivent s’assurer que leur fichier Docker est construit correctement.</span><span class="sxs-lookup"><span data-stu-id="1b99f-197">However, it is up to developers who use this option to ensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="1b99f-198">Comme le kit de ressources Azure ne valide pas le contenu d’un fichier Dockerfile personnalisé, le déploiement peut échouer si le fichier Dockerfile présente des problèmes.</span><span class="sxs-lookup"><span data-stu-id="1b99f-198">The Azure Toolkit does not validate the content in a custom Dockerfile, so the deployment might fail if the Dockerfile has issues.</span></span> <span data-ttu-id="1b99f-199">En outre, comme le kit de ressources Azure attend que le fichier Dockerfile personnalisé contienne un artefact d’application web, il tente d’ouvrir une connexion HTTP.</span><span class="sxs-lookup"><span data-stu-id="1b99f-199">In addition, the Azure Toolkit expects the custom Dockerfile to contain a web app artifact, and it will attempt to open an HTTP connection.</span></span> <span data-ttu-id="1b99f-200">Si les développeurs publient un autre type d’artefact, ils peuvent recevoir des erreurs sans effet après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="1b99f-200">If developers publish a different type of artifact, they may receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="1b99f-201">c.</span><span class="sxs-lookup"><span data-stu-id="1b99f-201">c.</span></span> <span data-ttu-id="1b99f-202">**Port settings** (Paramètres de port), entrez la liaison de port TCP unique pour votre conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="1b99f-202">**Port settings**: Enter the unique TCP port binding for your Docker container.</span></span>

     ![La fenêtre Configure the Docker container to be created (Configurer le conteneur Docker à créer)][PUB08]

10. <span data-ttu-id="1b99f-204">Après avoir terminé toutes les étapes précédentes, cliquez sur **Finish** (Terminer).</span><span class="sxs-lookup"><span data-stu-id="1b99f-204">After you have completed all of the preceding steps, click **Finish**.</span></span>

<span data-ttu-id="1b99f-205">Le kit de ressources Azure commence le déploiement de votre application web sur Azure dans un conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="1b99f-205">The Azure Toolkit begins deploying your web app to Azure in a Docker container.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1b99f-206">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1b99f-206">Next steps</span></span>
<span data-ttu-id="1b99f-207">Pour plus d’informations sur les kits d’outils Azure pour les environnements de développement Java, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b99f-207">For more information about the Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="1b99f-208">[Kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="1b99f-208">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="1b99f-209">[Nouveautés du Kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="1b99f-209">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="1b99f-210">[Installation du kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="1b99f-210">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="1b99f-211">[Instructions de connexion pour le Kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="1b99f-211">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="1b99f-212">[Créer une application web Hello World pour Azure dans Eclipse]</span><span class="sxs-lookup"><span data-stu-id="1b99f-212">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="1b99f-213">[Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="1b99f-213">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="1b99f-214">[Nouveautés du Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="1b99f-214">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="1b99f-215">[Installation du kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="1b99f-215">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="1b99f-216">[Instructions de connexion pour le Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="1b99f-216">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="1b99f-217">[Créer une application web Hello World pour Azure dans IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="1b99f-217">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="1b99f-218">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez [Centre de développement Java pour Azure] et [Outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="1b99f-218">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="1b99f-219">Pour obtenir des ressources supplémentaires pour Docker, consultez le [site web de Docker].</span><span class="sxs-lookup"><span data-stu-id="1b99f-219">For additional resources for Docker, see the official [Docker website].</span></span>

<!-- URL List -->

<span data-ttu-id="1b99f-220">[Kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="1b99f-220">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="1b99f-221">[Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="1b99f-221">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="1b99f-222">[Créer une application web Hello World pour Azure dans Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="1b99f-222">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="1b99f-223">[Créer une application web Hello World pour Azure dans IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="1b99f-223">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="1b99f-224">[Installation du kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="1b99f-224">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="1b99f-225">[Installation du kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="1b99f-225">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="1b99f-226">[Instructions de connexion pour le Kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="1b99f-226">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="1b99f-227">[Instructions de connexion pour le Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="1b99f-227">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="1b99f-228">[Nouveautés du Kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="1b99f-228">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="1b99f-229">[Nouveautés du Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="1b99f-229">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="1b99f-230">[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="1b99f-230">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="1b99f-231">[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="1b99f-231">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="1b99f-232">[site web de Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="1b99f-232">[Docker website]: https://www.docker.com/</span></span>

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