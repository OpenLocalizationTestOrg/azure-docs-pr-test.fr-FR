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
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="84344-103">Publier une application web comme un conteneur Docker à l’aide de hello boîte à outils Azure pour IntelliJ</span><span class="sxs-lookup"><span data-stu-id="84344-103">Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="84344-104">Les conteneurs Docker constituent une méthode largement utilisée pour déployer des applications web.</span><span class="sxs-lookup"><span data-stu-id="84344-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="84344-105">À l’aide de conteneurs Docker, les développeurs peuvent consolider toutes leurs fichiers de projet et les dépendances dans un package unique pour le serveur de déploiement tooa.</span><span class="sxs-lookup"><span data-stu-id="84344-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment tooa server.</span></span> <span data-ttu-id="84344-106">Bonjour Azure Toolkit pour IntelliJ simplifie ce processus pour les développeurs Java en ajoutant *publier en tant que conteneur Docker* fonctionnalités pour tooMicrosoft de déploiement Azure.</span><span class="sxs-lookup"><span data-stu-id="84344-106">hello Azure Toolkit for IntelliJ simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment tooMicrosoft Azure.</span></span> <span data-ttu-id="84344-107">Cet article vous guide toopublish requis des étapes de hello tooAzure de vos applications en tant que conteneurs Docker.</span><span class="sxs-lookup"><span data-stu-id="84344-107">This article walks you through hello steps required toopublish your applications tooAzure as Docker containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="84344-108">Plus d’informations sur Docker est disponible sur hello [site Web de Docker].</span><span class="sxs-lookup"><span data-stu-id="84344-108">More information about Docker is available on hello [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="84344-109">Publier votre tooAzure d’application web à l’aide d’un conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="84344-109">Publish your web app tooAzure by using a Docker container</span></span>

> [!NOTE]
> * <span data-ttu-id="84344-110">toopublish votre application web, vous devez créer un artefact prêts pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="84344-110">toopublish your web app, you must create a deployment-ready artifact.</span></span> <span data-ttu-id="84344-111">toolearn, voir hello [plus d’informations sur la création d’artefacts](#artifacts) section.</span><span class="sxs-lookup"><span data-stu-id="84344-111">toolearn more, see hello [Additional information about creating artifacts](#artifacts) section.</span></span>
>
> * <span data-ttu-id="84344-112">Une fois que vous avez terminé l’Assistant Déploiement hello au moins une fois, la plupart de vos paramètres est utilisée comme valeurs par défaut lorsque vous réexécutez hello.</span><span class="sxs-lookup"><span data-stu-id="84344-112">After you have completed hello deployment wizard at least once, most of your settings are used as defaults when you run hello wizard again.</span></span>
>

1. <span data-ttu-id="84344-113">Ouvrez votre projet d’application web dans IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="84344-113">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="84344-114">toostart hello **publier en tant que conteneur Docker** Assistant, effectuez une des manières suivantes les hello :</span><span class="sxs-lookup"><span data-stu-id="84344-114">toostart hello **Publish as Docker Container** wizard, do either of hello following:</span></span>

   * <span data-ttu-id="84344-115">Bonjour **projet** fenêtre de l’outil, avec le bouton droit de votre projet, cliquez sur **Azure**, puis cliquez sur **publier en tant que conteneur Docker**:</span><span class="sxs-lookup"><span data-stu-id="84344-115">In hello **Project** tool window, right-click your project, click **Azure**, and then click **Publish as Docker Container**:</span></span>

      ![Hello publier en tant que commande de conteneur Docker][PUB01]

   * <span data-ttu-id="84344-117">Barre d’outils hello IntelliJ, cliquez sur hello **groupe publier** bouton, puis cliquez sur **publier en tant que conteneur Docker**:</span><span class="sxs-lookup"><span data-stu-id="84344-117">On hello IntelliJ toolbar, click hello **Publish Group** button, and then click **Publish as Docker Container**:</span></span>

      <span data-ttu-id="84344-118">![Hello publier en tant que commande de conteneur Docker][PUB02]</span><span class="sxs-lookup"><span data-stu-id="84344-118">![hello Publish as Docker Container command][PUB02]</span></span>  
    <span data-ttu-id="84344-119">Hello **déployer le conteneur Docker sur Azure** Assistant s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="84344-119">hello **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![Hello conteneur Docker de déployer sur l’Assistant Azure][PUB03]

3. <span data-ttu-id="84344-121">Bonjour **tapez un nom d’image, sélectionnez le chemin d’accès d’artefact hello et vérifier un toobe d’hôte Docker utilisé** fenêtre, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="84344-121">In hello **Type an image name, select hello artifact's path and check a Docker host toobe used** window, do hello following:</span></span> 

   <span data-ttu-id="84344-122">a.</span><span class="sxs-lookup"><span data-stu-id="84344-122">a.</span></span> <span data-ttu-id="84344-123">Bonjour **nom de l’image Docker** , entrez un nom unique pour l’hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="84344-123">In hello **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="84344-124">(Assistant de hello crée automatiquement un nom, mais vous pouvez le modifier.)</span><span class="sxs-lookup"><span data-stu-id="84344-124">(hello wizard automatically creates a name, but you can modify it.)</span></span> 

   <span data-ttu-id="84344-125">b.</span><span class="sxs-lookup"><span data-stu-id="84344-125">b.</span></span> <span data-ttu-id="84344-126">Hello **hôtes** zone affiche tous les ordinateurs hôtes Docker que vous avez déjà créé.</span><span class="sxs-lookup"><span data-stu-id="84344-126">hello **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="84344-127">Effectuez une des manières suivantes les hello :</span><span class="sxs-lookup"><span data-stu-id="84344-127">Do either of hello following:</span></span> 
      * <span data-ttu-id="84344-128">Si vous avez un hôte Docker existant, vous pouvez déployer votre tooit d’application web.</span><span class="sxs-lookup"><span data-stu-id="84344-128">If you have an existing Docker host, you can deploy your web app tooit.</span></span>
      * <span data-ttu-id="84344-129">toocreate un hôte Docker, cliquez sur signe plus vert de hello (**+**).</span><span class="sxs-lookup"><span data-stu-id="84344-129">toocreate a Docker host, click hello green plus sign (**+**).</span></span>  
       <span data-ttu-id="84344-130">Hello **créer un hôte Docker** boîte de dialogue s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="84344-130">hello **Create Docker Host** dialog box opens.</span></span> 

      ![Assistant Deploy Docker Container on Azure (Déploiement d’un conteneur Docker sur Azure)][PUB04a]

4. <span data-ttu-id="84344-132">Bonjour **configurer la machine virtuelle hello** fenêtre, fournir hello suivant le plus d’informations sur l’hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="84344-132">In hello **Configure hello new virtual machine** window, provide hello following information about your Docker host.</span></span> <span data-ttu-id="84344-133">(Assistant de hello génère automatiquement la plupart des informations hello pour vous, mais vous pouvez modifier un d'entre eux).</span><span class="sxs-lookup"><span data-stu-id="84344-133">(hello wizard automatically generates most of hello information for you, but you can modify any of them.)</span></span> 

   <span data-ttu-id="84344-134">a.</span><span class="sxs-lookup"><span data-stu-id="84344-134">a.</span></span> <span data-ttu-id="84344-135">Bonjour **nom** , entrez un nom unique pour l’hôte Docker de hello.</span><span class="sxs-lookup"><span data-stu-id="84344-135">In hello **Name** box, enter a unique name for hello Docker host.</span></span> <span data-ttu-id="84344-136">(Il est ne pas hello identique hello du nom de l’image Docker que vous avez spécifié précédemment).</span><span class="sxs-lookup"><span data-stu-id="84344-136">(It is not hello same as hello Docker image name that you specified earlier.)</span></span> 
    
   <span data-ttu-id="84344-137">b.</span><span class="sxs-lookup"><span data-stu-id="84344-137">b.</span></span> <span data-ttu-id="84344-138">Bonjour **abonnement** , entrez hello abonnement Azure que vous utilisez pour votre ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="84344-138">In hello **Subscription** box, enter hello Azure subscription that you use for your host.</span></span> 
      
   <span data-ttu-id="84344-139">c.</span><span class="sxs-lookup"><span data-stu-id="84344-139">c.</span></span> <span data-ttu-id="84344-140">Bonjour **région** , entrez la région géographique de hello où se trouve votre hôte.</span><span class="sxs-lookup"><span data-stu-id="84344-140">In hello **Region** box, enter hello geographical region where your host is located.</span></span>
      
   <span data-ttu-id="84344-141">d.</span><span class="sxs-lookup"><span data-stu-id="84344-141">d.</span></span> <span data-ttu-id="84344-142">Sur hello **du système d’exploitation et la taille** onglet, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="84344-142">On hello **OS and Size** tab, do hello following:</span></span>      
      * <span data-ttu-id="84344-143">**Héberger le système d’exploitation**: entrez le système d’exploitation de hello pour l’ordinateur virtuel hello qui contient votre hôte.</span><span class="sxs-lookup"><span data-stu-id="84344-143">**Host OS**: Enter hello operating system for hello virtual machine that contains your host.</span></span> 
      * <span data-ttu-id="84344-144">**Taille**: entrez la taille de machine virtuelle hello pour votre ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="84344-144">**Size**: Enter hello virtual-machine size for your host.</span></span>   
       
   <span data-ttu-id="84344-145">e.</span><span class="sxs-lookup"><span data-stu-id="84344-145">e.</span></span> <span data-ttu-id="84344-146">Sur hello **groupe de ressources** , sélectionnez de hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="84344-146">On hello **Resource Group** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="84344-147">**New resource group** (Nouveau groupe de ressources) : créez un groupe de ressources pour votre hôte.</span><span class="sxs-lookup"><span data-stu-id="84344-147">**New resource group**: Create a resource group for your host.</span></span>
      * <span data-ttu-id="84344-148">**Existing resource group** (Groupe de ressources existant) : spécifiez un groupe de ressources existant dans votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="84344-148">**Existing resource group**: Specify an existing resource group from your Azure account.</span></span> 
       
   <span data-ttu-id="84344-149">f.</span><span class="sxs-lookup"><span data-stu-id="84344-149">f.</span></span> <span data-ttu-id="84344-150">Sur hello **réseau** , sélectionnez de hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="84344-150">On hello **Network** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="84344-151">**New virtual network** (Nouveau réseau virtuel) : créez un réseau virtuel pour votre hôte.</span><span class="sxs-lookup"><span data-stu-id="84344-151">**New virtual network**: Create a virtual network for your host.</span></span>
      * <span data-ttu-id="84344-152">**Existing virtual network** (Réseau virtuel existant) : spécifiez un réseau virtuel existant dans votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="84344-152">**Existing virtual network**: Specify an existing virtual network from your Azure account.</span></span> 
       
   <span data-ttu-id="84344-153">g.</span><span class="sxs-lookup"><span data-stu-id="84344-153">g.</span></span> <span data-ttu-id="84344-154">Sur hello **stockage** , sélectionnez de hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="84344-154">On hello **Storage** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="84344-155">**New storage account** (Nouveau compte de stockage) : créez un compte de stockage pour votre hôte.</span><span class="sxs-lookup"><span data-stu-id="84344-155">**New storage account**: Create a storage account for your host.</span></span>
      * <span data-ttu-id="84344-156">**Compte de stockage existant** : spécifiez un compte de stockage existant dans votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="84344-156">**Existing storage account**: Specify an existing storage account from your Azure account.</span></span>
       
5. <span data-ttu-id="84344-157">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="84344-157">Click **Next**.</span></span>  
     <span data-ttu-id="84344-158">Hello **configurer le journal dans les informations d’identification et les paramètres de port** fenêtre s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="84344-158">hello **Configure log in credentials and port settings** window opens.</span></span>

      ![journal de configuration Hello dans la fenêtre des paramètres de port et les informations d’identification][PUB05]

6. <span data-ttu-id="84344-160">Sélectionnez une des options suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="84344-160">Select one of hello following options:</span></span>

      * <span data-ttu-id="84344-161">**Import credentials from Azure Key Vault** (Importer des informations d’identification depuis Azure Key Vault) : spécifiez un ensemble d’informations d’identification précédemment enregistré et stocké dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="84344-161">**Import credentials from Azure Key Vault**: Specify a previously saved set of credentials that are stored in your Azure subscription.</span></span>

          > [!NOTE]
          > <span data-ttu-id="84344-162">Un coffre de clés Azure qui est créé avec un compte spécifique ou un principal de service n’est pas automatiquement accessible par un autre compte ou principal de service qui partage un abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="84344-162">An Azure key vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares hello subscription.</span></span> <span data-ttu-id="84344-163">une autre clé hello toouse principal compte ou le service de coffre tooallow, vous devez utiliser hello compte de hello tooadd portail Azure ou principal du service.</span><span class="sxs-lookup"><span data-stu-id="84344-163">tooallow another account or service principal toouse hello key vault, you must use hello Azure portal tooadd hello account or service principal.</span></span>

      * <span data-ttu-id="84344-164">**New log in credentials** (Nouvelles informations d’identification de connexion) : créez un nouvel ensemble d’informations d’identification de connexion.</span><span class="sxs-lookup"><span data-stu-id="84344-164">**New log in credentials**: Create a new set of login credentials.</span></span> <span data-ttu-id="84344-165">Si vous sélectionnez cette option, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="84344-165">If you select this option, do hello following:</span></span>

        <span data-ttu-id="84344-166">a.</span><span class="sxs-lookup"><span data-stu-id="84344-166">a.</span></span> <span data-ttu-id="84344-167">Sur hello **informations d’identification de l’ordinateur virtuel** fournir hello suit les informations d’identification de connexion d’accès à une machine virtuelle hello de l’hôte Docker, onglet : * **nom d’utilisateur**: entrez les nom d’utilisateur hello de votre connexion à une machine virtuelle informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="84344-167">On hello **VM Credentials** tab, provide hello following information for hello virtual-machine login credentials of your Docker host: * **Username**: Enter hello username for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="84344-168">* **Mot de passe** et **confirmer**: entrez le mot de passe de hello vos informations d’identification du compte de connexion à une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="84344-168">* **Password** and **Confirm**: Enter hello password for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="84344-169">* **SSH**: entrez hello les paramètres de Secure Shell (SSH) pour l’hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="84344-169">* **SSH**: Enter hello Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="84344-170">Vous pouvez sélectionner une des options suivantes de hello : * **aucun**: Spécifie que votre ordinateur virtuel n’autorise pas les connexions SSH.</span><span class="sxs-lookup"><span data-stu-id="84344-170">You can select one of hello following options: * **None**: Specifies that your virtual machine does not allow SSH connections.</span></span>
                <span data-ttu-id="84344-171">* **Générer automatiquement**: crée automatiquement les paramètres requis hello pour se connecter via une connexion SSH.</span><span class="sxs-lookup"><span data-stu-id="84344-171">* **Auto-generate**: Automatically creates hello requisite settings for connecting via SSH.</span></span>
                <span data-ttu-id="84344-172">* **Importer à partir du répertoire**: vous permet de toospecify un répertoire qui contient un ensemble de paramètres SSH précédemment enregistrés.</span><span class="sxs-lookup"><span data-stu-id="84344-172">* **Import from directory**: Allows you toospecify a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="84344-173">répertoire de Hello doit contenir hello deux fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="84344-173">hello directory must contain hello following two files:</span></span>
                
                  * *id_rsa*: Contains hello RSA identification for a user.
                  * *id_rsa.pub*: Contains hello RSA public key that is used for authentication.
            
        <span data-ttu-id="84344-174">b.</span><span class="sxs-lookup"><span data-stu-id="84344-174">b.</span></span> <span data-ttu-id="84344-175">Sur hello **accès du démon Docker** , onglet de fournir hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="84344-175">On hello **Docker Daemon Access** tab, provide hello following information:</span></span>

          ![Créer un hôte Docker][PUB06]
    
             * **Docker Daemon port**: Enter hello unique TCP port for your Docker host.
             * **TLS Security**: Enter hello Transport Layer Security settings for your Docker host. You can choose from hello following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. hello directory must contain hello following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain hello client certificate and public key that is used for TLS authentication.

7. <span data-ttu-id="84344-177">Après avoir entré les informations de hello requis, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="84344-177">After you have entered hello required information, click **Finish**.</span></span>  
    <span data-ttu-id="84344-178">Hello **déployer le conteneur Docker sur Azure** Assistant s’affiche de nouveau.</span><span class="sxs-lookup"><span data-stu-id="84344-178">hello **Deploy Docker Container on Azure** wizard reappears.</span></span>

   ![Assistant Deploy Docker Container on Azure (Déploiement d’un conteneur Docker sur Azure)][PUB07]

8. <span data-ttu-id="84344-180">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="84344-180">Click **Next**.</span></span>  
    <span data-ttu-id="84344-181">Hello **configurer toobe de conteneur Docker hello créé** fenêtre s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="84344-181">hello **Configure hello Docker container toobe created** window opens.</span></span>

   ![fenêtre de Hello configurer hello Docker conteneur toobe créé][PUB08]

9. <span data-ttu-id="84344-183">Bonjour **configurer toobe de conteneur Docker hello créé** fenêtre, fournir hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="84344-183">In hello **Configure hello Docker container toobe created** window, provide hello following information:</span></span> 

   <span data-ttu-id="84344-184">a.</span><span class="sxs-lookup"><span data-stu-id="84344-184">a.</span></span> <span data-ttu-id="84344-185">Bonjour **nom du conteneur Docker** , entrez un nom unique pour votre conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="84344-185">In hello **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="84344-186">b.</span><span class="sxs-lookup"><span data-stu-id="84344-186">b.</span></span> <span data-ttu-id="84344-187">Choisissez une des hello suivant Docker images :</span><span class="sxs-lookup"><span data-stu-id="84344-187">Choose one of hello following Docker images:</span></span> 

      * <span data-ttu-id="84344-188">**Predefined Docker image** (Image Docker prédéfinie) : spécifiez une image Docker préexistante dans Azure.</span><span class="sxs-lookup"><span data-stu-id="84344-188">**Predefined Docker image**: Specify a pre-existing Docker image from Azure.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="84344-189">liste de Hello d’images Docker dans cette zone se compose de plusieurs images qui hello boîte à outils Azure a été configuré toopatch afin que votre objet est déployé automatiquement.</span><span class="sxs-lookup"><span data-stu-id="84344-189">hello list of Docker images in this box consists of several images that hello Azure Toolkit has been configured toopatch so that your artifact is deployed automatically.</span></span> 

      * <span data-ttu-id="84344-190">**Custom Dockerfile** (Fichier Dockerfile personnalisé) : spécifiez un fichier Dockerfile précédemment enregistré sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="84344-190">**Custom Dockerfile**: Specify a previously saved Dockerfile from your local computer.</span></span>

        > [!NOTE]
        > <span data-ttu-id="84344-191">Il s’agit d’une fonctionnalité avancée pour les développeurs qui veulent toodeploy leur propre fichier Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="84344-191">This is a more advanced feature for developers who want toodeploy their own Dockerfile.</span></span> <span data-ttu-id="84344-192">Toutefois, c’est toodevelopers qui utilisent cette tooensure option leur Dockerfile générée correctement.</span><span class="sxs-lookup"><span data-stu-id="84344-192">However, it is up toodevelopers who use this option tooensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="84344-193">Étant donné que hello boîte à outils Azure ne valide pas le contenu de hello dans un fichier Dockerfile personnalisé, déploiement de hello peut échouer si hello Dockerfile présente des problèmes.</span><span class="sxs-lookup"><span data-stu-id="84344-193">Because hello Azure Toolkit does not validate hello content in a custom Dockerfile, hello deployment might fail if hello Dockerfile has issues.</span></span> <span data-ttu-id="84344-194">En outre, hello boîte à outils Azure escomptant hello personnalisé Dockerfile toocontain un artefact d’application web, il tente de tooopen une connexion HTTP.</span><span class="sxs-lookup"><span data-stu-id="84344-194">In addition, because hello Azure Toolkit expects hello custom Dockerfile toocontain a web app artifact, it attempts tooopen an HTTP connection.</span></span> <span data-ttu-id="84344-195">Si les développeurs publier un autre type d’artefact, ils peuvent recevoir des erreurs sans effet après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="84344-195">If developers publish a different type of artifact, they might receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="84344-196">c.</span><span class="sxs-lookup"><span data-stu-id="84344-196">c.</span></span> <span data-ttu-id="84344-197">Bonjour **paramètres de Port** , entrez la liaison de port TCP unique hello pour votre conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="84344-197">In hello **Port settings** box, enter hello unique TCP port binding for your Docker container.</span></span> 

10. <span data-ttu-id="84344-198">Après avoir terminé les étapes précédentes de hello, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="84344-198">After you have completed hello preceding steps, click **Finish**.</span></span> 

<span data-ttu-id="84344-199">Hello boîte à outils Azure commence à déployer votre tooAzure d’application web dans un conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="84344-199">hello Azure Toolkit begins deploying your web app tooAzure in a Docker container.</span></span> <span data-ttu-id="84344-200">Sauf si vous avez configuré toobe IntelliJ déployé dans l’arrière-plan de hello, un **déploiement tooAzure** barre de progression s’affiche.</span><span class="sxs-lookup"><span data-stu-id="84344-200">Unless you have configured IntelliJ toobe deployed in hello background, a **Deploying tooAzure** progress bar appears.</span></span> 

![barre de progression du déploiement Hello][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a><span data-ttu-id="84344-202">Informations supplémentaires sur la création d’artefacts</span><span class="sxs-lookup"><span data-stu-id="84344-202">Additional information about creating artifacts</span></span>

<span data-ttu-id="84344-203">toocreate un artefact prêts pour le déploiement, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="84344-203">toocreate a deployment-ready artifact, do hello following:</span></span>

1. <span data-ttu-id="84344-204">Ouvrez votre projet d’application web dans IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="84344-204">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="84344-205">Cliquez sur **File (Fichier)**, puis sur **Project Structure (Structure de projet)**.</span><span class="sxs-lookup"><span data-stu-id="84344-205">Click **File**, and then click **Project Structure**.</span></span>

   ![Hello commande de la Structure de projet][ART01]

3. <span data-ttu-id="84344-207">tooadd un artefact, cliquez sur signe plus vert de hello (**+**), puis cliquez sur **Application Web : Archive**.</span><span class="sxs-lookup"><span data-stu-id="84344-207">tooadd an artifact, click hello green plus sign (**+**), and then click **Web Application: Archive**.</span></span>

   ![Hello commande de « Application Web : Archive »][ART02]

4. <span data-ttu-id="84344-209">Bonjour **nom** , entrez un nom pour votre artefact (n’incluez pas hello *.war* extension), puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="84344-209">In hello **Name** box, enter a name for your artifact (do not include hello *.war* extension), and then click **OK**.</span></span>

   ![zone de nom d’artefact Hello][ART03]

<span data-ttu-id="84344-211">Pour plus d’informations sur la création des artefacts dans IntelliJ, consultez [configurant des artefacts] sur le site Web de JetBrains hello.</span><span class="sxs-lookup"><span data-stu-id="84344-211">For more information about creating artifacts in IntelliJ, see [Configuring artifacts] on hello JetBrains website.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84344-212">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="84344-212">Next steps</span></span>
<span data-ttu-id="84344-213">Pour plus d’informations sur hello boîtes à outils Azure pour Java IDE, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="84344-213">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="84344-214">[boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="84344-214">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="84344-215">[Nouveautés de hello boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="84344-215">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="84344-216">[Lors de l’installation hello boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="84344-216">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="84344-217">[Instructions de connexion pour hello boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="84344-217">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="84344-218">[Créer une application web Hello World pour Azure dans Eclipse]</span><span class="sxs-lookup"><span data-stu-id="84344-218">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="84344-219">[Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="84344-219">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="84344-220">[Quelles sont les nouveautés Bonjour Azure Toolkit pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="84344-220">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="84344-221">[Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="84344-221">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="84344-222">[Instructions d’authentification pour hello boîte à outils Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="84344-222">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="84344-223">[Créer une application web Hello World pour Azure dans IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="84344-223">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="84344-224">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure] et hello [outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="84344-224">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="84344-225">Pour obtenir des ressources supplémentaires pour Docker, consultez officielle de hello [site Web de Docker].</span><span class="sxs-lookup"><span data-stu-id="84344-225">For additional resources for Docker, see hello official [Docker website].</span></span>

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
