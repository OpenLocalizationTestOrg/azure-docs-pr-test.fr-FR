---
title: "Configuration d'Apache Tomcat sur une machine virtuelle Linux | Microsoft Docs"
description: "Apprenez à configurer Apache Tomcat7 avec une machine virtuelle Azure exécutant Linux."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 45ecc89c-1cb0-4e80-8944-bd0d0bbedfdc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: ningk
ms.openlocfilehash: fa30c78a5a5d458ba8845c3c10b87538427786c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a><span data-ttu-id="f119b-103">Configurer Tomcat7 sur une machine virtuelle Linux avec Azure</span><span class="sxs-lookup"><span data-stu-id="f119b-103">Set up Tomcat7 on a Linux virtual machine with Azure</span></span>
<span data-ttu-id="f119b-104">Apache Tomcat (ou simplement Tomcat, également appelé Jakarta Tomcat précédemment) est un serveur web open source et un conteneur de servlet développé par Apache Software Foundation (ASF).</span><span class="sxs-lookup"><span data-stu-id="f119b-104">Apache Tomcat (or simply Tomcat, also formerly called Jakarta Tomcat) is an open source web server and servlet container developed by the Apache Software Foundation (ASF).</span></span> <span data-ttu-id="f119b-105">Tomcat implémente le servlet Java et les spécifications Java Server Pages (JSP) de Sun Microsystems.</span><span class="sxs-lookup"><span data-stu-id="f119b-105">Tomcat implements the Java Servlet and the JavaServer Pages (JSP) specifications from Sun Microsystems.</span></span> <span data-ttu-id="f119b-106">Tomcat fournit un environnement de serveur web HTTP Java pur dans lequel exécuter le code Java.</span><span class="sxs-lookup"><span data-stu-id="f119b-106">Tomcat provides a pure Java HTTP web server environment in which to run Java code.</span></span> <span data-ttu-id="f119b-107">Dans la configuration la plus simple, Tomcat s’exécute dans un processus de système d’exploitation unique.</span><span class="sxs-lookup"><span data-stu-id="f119b-107">In the simplest configuration, Tomcat runs in a single operating system process.</span></span> <span data-ttu-id="f119b-108">Ce processus exécute une machine virtuelle Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="f119b-108">This process runs a Java virtual machine (JVM).</span></span> <span data-ttu-id="f119b-109">Chaque requête HTTP d’un navigateur vers Tomcat est traitée comme un thread séparé dans le processus de Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f119b-109">Every HTTP request from a browser to Tomcat is processed as a separate thread in the Tomcat process.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="f119b-110">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Azure Resource Manager et classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f119b-110">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f119b-111">Cet article explique comment utiliser le modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="f119b-111">This article covers how to use the classic deployment model.</span></span> <span data-ttu-id="f119b-112">Pour la plupart des nouveaux déploiements, nous recommandons d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f119b-112">We recommend that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="f119b-113">Pour utiliser un modèle Resource Manager afin de déployer une machine virtuelle Ubuntu avec Open JDK et Tomcat, lisez [cet article](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span><span class="sxs-lookup"><span data-stu-id="f119b-113">To use a Resource Manager template to deploy an Ubuntu VM with Open JDK and Tomcat, see [this article](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span></span>

<span data-ttu-id="f119b-114">Dans cet article, vous installerez Tomcat7 sur une image Linux et le déploierez dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f119b-114">In this article, you will install Tomcat7 on a Linux image and deploy it in Azure.</span></span>  

<span data-ttu-id="f119b-115">Vous apprendrez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="f119b-115">You will learn:</span></span>  

* <span data-ttu-id="f119b-116">Création d’une machine virtuelle dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f119b-116">How to create a virtual machine in Azure.</span></span>
* <span data-ttu-id="f119b-117">Préparation de la machine virtuelle pour Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="f119b-117">How to prepare the virtual machine for Tomcat7.</span></span>
* <span data-ttu-id="f119b-118">Installation de Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="f119b-118">How to install Tomcat7.</span></span>

<span data-ttu-id="f119b-119">Nous partons du principe que vous possédez déjà un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f119b-119">It is assumed that you already have an Azure subscription.</span></span>  <span data-ttu-id="f119b-120">Si ce n’est pas le cas, vous pouvez vous inscrire sur [le site web Azure](https://azure.microsoft.com/) pour obtenir une évaluation gratuite.</span><span class="sxs-lookup"><span data-stu-id="f119b-120">If not, you can sign up for a free trial at [the Azure website](https://azure.microsoft.com/).</span></span> <span data-ttu-id="f119b-121">Si vous disposez d’un abonnement MSDN, consultez la page présentant les [tarifs préférentiels Microsoft Azure : avantages MSDN, MPN et BizSpark](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span><span class="sxs-lookup"><span data-stu-id="f119b-121">If you have an MSDN subscription, see [Microsoft Azure Special Pricing: MSDN, MPN, and BizSpark Benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span></span> <span data-ttu-id="f119b-122">Pour en savoir plus sur Azure, consultez [Présentation d’Azure](https://azure.microsoft.com/overview/what-is-azure/).</span><span class="sxs-lookup"><span data-stu-id="f119b-122">To learn more about Azure, see [What is Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span></span>

<span data-ttu-id="f119b-123">Cet article suppose que vous avez des connaissances de base relatives à Tomcat et Linux.</span><span class="sxs-lookup"><span data-stu-id="f119b-123">This article assumes that you have a basic working knowledge of Tomcat and Linux.</span></span>  

## <a name="phase-1-create-an-image"></a><span data-ttu-id="f119b-124">Phase 1 : Création d’une image</span><span class="sxs-lookup"><span data-stu-id="f119b-124">Phase 1: Create an image</span></span>
<span data-ttu-id="f119b-125">Lors de cette phase, vous allez créer une machine virtuelle à l’aide d’une image Linux dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f119b-125">In this phase, you will create a virtual machine by using a Linux image in Azure.</span></span>  

### <a name="step-1-generate-an-ssh-authentication-key"></a><span data-ttu-id="f119b-126">Étape 1 : Générer une clé d’authentification SSH</span><span class="sxs-lookup"><span data-stu-id="f119b-126">Step 1: Generate an SSH authentication key</span></span>
<span data-ttu-id="f119b-127">SSH est un outil important pour les administrateurs système.</span><span class="sxs-lookup"><span data-stu-id="f119b-127">SSH is an important tool for system administrators.</span></span> <span data-ttu-id="f119b-128">Toutefois, une configuration de la sécurité d’accès basée sur un mot de passe déterminé par l’homme n’est pas recommandée.</span><span class="sxs-lookup"><span data-stu-id="f119b-128">However, configuring access security based on a human-determined password is not recommended.</span></span> <span data-ttu-id="f119b-129">Les utilisateurs malveillants peuvent s’introduire dans votre système si vous disposez d’un nom d’utilisateur et d’un mot de passe faibles.</span><span class="sxs-lookup"><span data-stu-id="f119b-129">Malicious users can break into your system based on a username and a weak password.</span></span>

<span data-ttu-id="f119b-130">Toutefois, il existe un moyen de laisser l’accès à distance ouvert. Vous n’aurez donc pas à vous soucier des mots de passe.</span><span class="sxs-lookup"><span data-stu-id="f119b-130">The good news is that there is a way to leave remote access open and not worry about passwords.</span></span> <span data-ttu-id="f119b-131">Cette méthode se compose d’une authentification avec chiffrement asymétrique.</span><span class="sxs-lookup"><span data-stu-id="f119b-131">This method consists of authentication with asymmetric cryptography.</span></span> <span data-ttu-id="f119b-132">La clé privée de l’utilisateur est celle qui accorde l’authentification.</span><span class="sxs-lookup"><span data-stu-id="f119b-132">The user’s private key is the one that grants the authentication.</span></span> <span data-ttu-id="f119b-133">Vous pouvez même verrouiller le compte de l’utilisateur pour interdire l’authentification par mot de passe.</span><span class="sxs-lookup"><span data-stu-id="f119b-133">You can even lock the user’s account to not allow password authentication.</span></span>

<span data-ttu-id="f119b-134">Un autre avantage de cette méthode est que vous n’avez pas besoin de mots de passe différents pour vous connecter à des serveurs différents.</span><span class="sxs-lookup"><span data-stu-id="f119b-134">Another advantage of this method is that you do not need different passwords to sign in to different servers.</span></span> <span data-ttu-id="f119b-135">Vous pouvez vous authentifier à l’aide de la clé privée personnelle sur tous les serveurs, ce qui vous évite d’avoir à mémoriser plusieurs mots de passe.</span><span class="sxs-lookup"><span data-stu-id="f119b-135">You can authenticate by using the personal private key on all servers, which prevents you from having to remember several passwords.</span></span>



<span data-ttu-id="f119b-136">Pour générer la clé d’authentification SSH, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="f119b-136">Follow these steps to generate the SSH authentication key.</span></span>

1. <span data-ttu-id="f119b-137">Téléchargez et installez PuTTYgen à partir de l’emplacement suivant : [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="f119b-137">Download and install PuTTYgen from the following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
2. <span data-ttu-id="f119b-138">Exécutez Puttygen.exe.</span><span class="sxs-lookup"><span data-stu-id="f119b-138">Run Puttygen.exe.</span></span>
3. <span data-ttu-id="f119b-139">Cliquez sur **Generate** pour générer les clés.</span><span class="sxs-lookup"><span data-stu-id="f119b-139">Click **Generate** to generate the keys.</span></span> <span data-ttu-id="f119b-140">Dans le processus, vous pouvez augmenter le caractère aléatoire en déplaçant la souris sur la zone vide dans la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="f119b-140">In the process, you can increase randomness by moving the mouse over the blank area in the window.</span></span>  
   <span data-ttu-id="f119b-141">![Capture d’écran du générateur de clé puTTY montrant le bouton permettant de générer une nouvelle clé][1]</span><span class="sxs-lookup"><span data-stu-id="f119b-141">![PuTTY Key Generator screenshot that shows the generate new key button][1]</span></span>
4. <span data-ttu-id="f119b-142">Après le processus de génération, Puttygen.exe affiche votre nouvelle clé publique.</span><span class="sxs-lookup"><span data-stu-id="f119b-142">After the generate process, Puttygen.exe will show your new public key.</span></span>  
   ![Capture d’écran du générateur de clé puTTY montrant la nouvelle clé publique et le bouton permettant d'enregistrer une clé privée][2]
5. <span data-ttu-id="f119b-144">Sélectionnez et copiez la clé publique et enregistrez-la dans un fichier nommé publicKey.pem.</span><span class="sxs-lookup"><span data-stu-id="f119b-144">Select and copy the public key, and save it in a file named publicKey.pem.</span></span> <span data-ttu-id="f119b-145">Ne cliquez pas sur **Save public key**, car le format de fichier de la clé publique enregistrée est différent de la clé publique que nous voulons.</span><span class="sxs-lookup"><span data-stu-id="f119b-145">Don’t click **Save public key**, because the saved public key’s file format is different from the public key we want.</span></span>
6. <span data-ttu-id="f119b-146">Cliquez sur **Save private key** et enregistrez-la dans un fichier nommé privateKey.ppk.</span><span class="sxs-lookup"><span data-stu-id="f119b-146">Click **Save private key**, and save it in a file named privateKey.ppk.</span></span>

### <a name="step-2-create-the-image-in-the-azure-portal"></a><span data-ttu-id="f119b-147">Étape 2 : Créer l’image dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="f119b-147">Step 2: Create the image in the Azure portal</span></span>
1. <span data-ttu-id="f119b-148">Dans le [portail](https://portal.azure.com/), cliquez sur **Nouveau** dans la barre des tâches pour créer une image.</span><span class="sxs-lookup"><span data-stu-id="f119b-148">In the [portal](https://portal.azure.com/), click **New** in the task bar to create an image.</span></span> <span data-ttu-id="f119b-149">Choisissez ensuite l’image Linux selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="f119b-149">Then choose the Linux image that is based on your needs.</span></span> <span data-ttu-id="f119b-150">L’exemple suivant utilise l’image Ubuntu 14.04.</span><span class="sxs-lookup"><span data-stu-id="f119b-150">The following example uses the Ubuntu 14.04 image.</span></span>
<span data-ttu-id="f119b-151">![Capture d’écran du portail montrant le bouton Nouveau][3]</span><span class="sxs-lookup"><span data-stu-id="f119b-151">![Screenshot of the portal that shows the New button][3]</span></span>

2. <span data-ttu-id="f119b-152">Pour **Nom d’hôte** spécifiez le nom de l’URL que les clients Internet utiliseront pour accéder à cette machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f119b-152">For **Host Name**, specify the name for the URL that you and Internet clients will use to access this virtual machine.</span></span> <span data-ttu-id="f119b-153">Définissez la dernière partie du nom DNS, par exemple, tomcatdemo.</span><span class="sxs-lookup"><span data-stu-id="f119b-153">Define the last part of the DNS name, for example, tomcatdemo.</span></span> <span data-ttu-id="f119b-154">Azure génère alors l’URL sous la forme tomcatdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="f119b-154">Azure will then generate the URL as tomcatdemo.cloudapp.net.</span></span>  

3. <span data-ttu-id="f119b-155">Pour **Clé d’authentification SSH**, copiez la valeur de clé à partir du fichier publicKey.pem qui contient la clé publique générée par PuTTYgen.</span><span class="sxs-lookup"><span data-stu-id="f119b-155">For **SSH Authentication Key**, copy the key value from the publicKey.pem file, which contains the public key generated by PuTTYgen.</span></span>  
<span data-ttu-id="f119b-156">![Zone de la clé d’authentification SSH dans le portail][4]</span><span class="sxs-lookup"><span data-stu-id="f119b-156">![SSH Authentication Key box in the portal][4]</span></span>

4. <span data-ttu-id="f119b-157">Configurez d’autres paramètres selon les besoins, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f119b-157">Configure other settings as needed, and then click **Create**.</span></span>  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a><span data-ttu-id="f119b-158">Phase 2 : Préparation de la machine virtuelle pour Tomcat7</span><span class="sxs-lookup"><span data-stu-id="f119b-158">Phase 2: Prepare your virtual machine for Tomcat7</span></span>
<span data-ttu-id="f119b-159">Lors de cette phase, vous allez configurer un point de terminaison pour le trafic Tomcat, puis vous connecter à votre nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f119b-159">In this phase, you will configure an endpoint for Tomcat traffic, and then connect to your new virtual machine.</span></span>

### <a name="step-1-open-the-http-port-to-allow-web-access"></a><span data-ttu-id="f119b-160">Étape 2 : Ouverture du port HTTP pour autoriser l’accès web</span><span class="sxs-lookup"><span data-stu-id="f119b-160">Step 1: Open the HTTP port to allow web access</span></span>
<span data-ttu-id="f119b-161">Les points de terminaison dans Azure se composent d’un protocole TCP ou UDP et d’un port public et privé.</span><span class="sxs-lookup"><span data-stu-id="f119b-161">Endpoints in Azure consist of a TCP or UDP protocol, along with a public and private port.</span></span> <span data-ttu-id="f119b-162">Le port privé est celui que le service écoute sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f119b-162">The private port is the port that the service is listening to on the virtual machine.</span></span> <span data-ttu-id="f119b-163">Le port public est celui que le service cloud Azure écoute en externe pour le trafic Internet entrant.</span><span class="sxs-lookup"><span data-stu-id="f119b-163">The public port is the port that the Azure cloud service listens to externally for incoming, Internet-based traffic.</span></span>  

<span data-ttu-id="f119b-164">Le port TCP 8080 est le numéro de port par défaut sur lequel Tomcat écoute.</span><span class="sxs-lookup"><span data-stu-id="f119b-164">TCP port 8080 is the default port number that Tomcat uses to listen.</span></span> <span data-ttu-id="f119b-165">Si ce port est ouvert avec un point de terminaison Azure, vous pouvez (vous et d’autres clients Internet) accéder aux pages Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f119b-165">If this port is opened with an Azure endpoint, you and other Internet clients can access Tomcat pages.</span></span>  

1. <span data-ttu-id="f119b-166">Dans le portail, cliquez sur **Parcourir** > **Machines virtuelles**, puis cliquez sur la machine virtuelle que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="f119b-166">In the portal, click **Browse** > **Virtual machines**, and then click the virtual machine that you created.</span></span>  
   <span data-ttu-id="f119b-167">![Capture d’écran de l’annuaire des machines virtuelles][5]</span><span class="sxs-lookup"><span data-stu-id="f119b-167">![Screenshot of the Virtual machines directory][5]</span></span>
2. <span data-ttu-id="f119b-168">Pour ajouter un point de terminaison à votre machine virtuelle, cliquez sur la zone **Points de terminaison** .</span><span class="sxs-lookup"><span data-stu-id="f119b-168">To add an endpoint to your virtual machine, click the **Endpoints** box.</span></span>
   <span data-ttu-id="f119b-169">![Capture d’écran montrant la zone Points de terminaison][6]</span><span class="sxs-lookup"><span data-stu-id="f119b-169">![Screenshot that shows the Endpoints box][6]</span></span>
3. <span data-ttu-id="f119b-170">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="f119b-170">Click **Add**.</span></span>  

   1. <span data-ttu-id="f119b-171">Entrez un nom pour le point de terminaison dans **Point de terminaison**, puis tapez 80 dans **Port public**.</span><span class="sxs-lookup"><span data-stu-id="f119b-171">For the endpoint, enter a name for the endpoint in **Endpoint**, and then enter 80 in **Public Port**.</span></span>  

      <span data-ttu-id="f119b-172">Si vous affectez le port 80, vous n’avez pas besoin d’inclure le numéro de port dans l’URL utilisée pour accéder à Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f119b-172">If you set it to 80, you don’t need to include the port number in the URL that is used to access Tomcat.</span></span> <span data-ttu-id="f119b-173">Par exemple, http://tomcatdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="f119b-173">For example, http://tomcatdemo.cloudapp.net.</span></span>    

      <span data-ttu-id="f119b-174">Si vous affectez une autre valeur pour le port, par exemple 81, vous devez ajouter le numéro de port à l’URL pour accéder à Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f119b-174">If you set it to another value, such as 81, you need to add the port number to the URL to access Tomcat.</span></span> <span data-ttu-id="f119b-175">Par exemple, http://tomcatdemo.cloudapp.net:81/.</span><span class="sxs-lookup"><span data-stu-id="f119b-175">For example,  http://tomcatdemo.cloudapp.net:81/.</span></span>
   2. <span data-ttu-id="f119b-176">Tapez 8080 dans **Port privé**.</span><span class="sxs-lookup"><span data-stu-id="f119b-176">Enter 8080 in **Private Port**.</span></span> <span data-ttu-id="f119b-177">Par défaut, Tomcat écoute sur le port TCP 8080.</span><span class="sxs-lookup"><span data-stu-id="f119b-177">By default, Tomcat listens on TCP port 8080.</span></span> <span data-ttu-id="f119b-178">Si vous avez modifié le port d’écoute par défaut de Tomcat, vous devez mettre à jour **Port privé** pour qu’il s’agisse du même que le port d’écoute Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f119b-178">If you changed the default listen port of Tomcat, you should update **Private Port** to be the same as the Tomcat listen port.</span></span>  
      <span data-ttu-id="f119b-179">![Capture d’écran de l’interface utilisateur montrant la commande Ajouter, Port public et Port privé][7]</span><span class="sxs-lookup"><span data-stu-id="f119b-179">![Screenshot of UI that shows Add command, Public Port, and Private Port][7]</span></span>
4. <span data-ttu-id="f119b-180">Cliquez sur **OK** pour ajouter le point de terminaison à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f119b-180">Click **OK** to add the endpoint to your virtual machine.</span></span>

### <a name="step-2-connect-to-the-image-you-created"></a><span data-ttu-id="f119b-181">Étape 2 : Connexion à l’image que vous avez créée</span><span class="sxs-lookup"><span data-stu-id="f119b-181">Step 2: Connect to the image you created</span></span>
<span data-ttu-id="f119b-182">Vous pouvez choisir n’importe quel outil SSH pour vous connecter à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f119b-182">You can choose any SSH tool to connect to your virtual machine.</span></span> <span data-ttu-id="f119b-183">Dans cet exemple, nous utilisons PuTTY.</span><span class="sxs-lookup"><span data-stu-id="f119b-183">In this example, we use PuTTY.</span></span>  

1. <span data-ttu-id="f119b-184">Obtenez le nom DNS de votre machine virtuelle à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="f119b-184">Get the DNS name of your virtual machine from the portal.</span></span>
    1. <span data-ttu-id="f119b-185">Cliquez sur **Parcourir** > **Machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="f119b-185">Click **Browse** > **Virtual machines**.</span></span>
    2. <span data-ttu-id="f119b-186">Sélectionnez le nom de votre machine virtuelle, puis cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="f119b-186">Select the name of your virtual machine, and then click **Properties**.</span></span>
    3. <span data-ttu-id="f119b-187">Dans la mosaïque **Propriétés**, consultez la zone **Nom de domaine** pour obtenir le nom DNS.</span><span class="sxs-lookup"><span data-stu-id="f119b-187">In the **Properties** tile, look in the **Domain Name** box to get the DNS name.</span></span>  

2. <span data-ttu-id="f119b-188">Obtenez le numéro de port pour les connexions SSH à partir de la zone **SSH**.</span><span class="sxs-lookup"><span data-stu-id="f119b-188">Get the port number for SSH connections from the **SSH** box.</span></span>  
<span data-ttu-id="f119b-189">![Capture d’écran montrant le numéro de port de connexion SSH][8]</span><span class="sxs-lookup"><span data-stu-id="f119b-189">![Screenshot that shows the SSH connection port number][8]</span></span>

3. <span data-ttu-id="f119b-190">Téléchargez [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="f119b-190">Download [PuTTY](http://www.putty.org/).</span></span>  

4. <span data-ttu-id="f119b-191">Après le téléchargement, cliquez sur le fichier exécutable Putty.exe.</span><span class="sxs-lookup"><span data-stu-id="f119b-191">After downloading, click the executable file Putty.exe.</span></span> <span data-ttu-id="f119b-192">Dans la configuration PuTTY, configurez les options de base avec le nom d’hôte et le numéro de port obtenus à partir des propriétés de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f119b-192">In PuTTY configuration, configure the basic options with the host name and port number that is obtained from the properties of your virtual machine.</span></span>   
![Capture d’écran montrant les options de nom d'hôte et de port de la configuration PuTTY][9]

5. <span data-ttu-id="f119b-194">Dans le volet gauche, cliquez sur **Connexion** > **SSH** > **Auth**, puis cliquez sur **Parcourir** pour spécifier l’emplacement du fichier privateKey.ppk.</span><span class="sxs-lookup"><span data-stu-id="f119b-194">In the left pane, click **Connection** > **SSH** > **Auth**, and then click **Browse** to specify the location of the privateKey.ppk file.</span></span> <span data-ttu-id="f119b-195">Le fichier privateKey.ppk contient la clé privée générée précédemment par PuTTYgen dans la section « Phase 1 : Création d'une image » de cet article.</span><span class="sxs-lookup"><span data-stu-id="f119b-195">The privateKey.ppk file contains the private key that is generated by PuTTYgen earlier in the "Phase 1: Create an image" section of this article.</span></span>  
<span data-ttu-id="f119b-196">![Capture d’écran montrant la hiérarchie du répertoire Connexion et un bouton Parcourir][10]</span><span class="sxs-lookup"><span data-stu-id="f119b-196">![Screenshot that shows the Connection directory hierarchy and Browse button][10]</span></span>

6. <span data-ttu-id="f119b-197">Cliquez sur **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="f119b-197">Click **Open**.</span></span> <span data-ttu-id="f119b-198">Une boîte de message peut s’afficher.</span><span class="sxs-lookup"><span data-stu-id="f119b-198">You might be alerted by a message box.</span></span> <span data-ttu-id="f119b-199">Si vous avez configuré le nom DNS et le numéro de port correctement, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="f119b-199">If you have configured the DNS name and port number correctly, click **Yes**.</span></span>
<span data-ttu-id="f119b-200">![Capture d’écran montrant la notification][11]</span><span class="sxs-lookup"><span data-stu-id="f119b-200">![Screenshot that shows the notification][11]</span></span>

7. <span data-ttu-id="f119b-201">Vous êtes invité à saisir votre nom d'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f119b-201">You are prompted to enter your username.</span></span>  
![Capture d’écran montrant où entrer le nom d’utilisateur][12]

8. <span data-ttu-id="f119b-203">Entrez le nom d’utilisateur que vous avez utilisé pour créer la machine virtuelle dans la section « Phase 1 : Création d'une image » plus haut dans cet article.</span><span class="sxs-lookup"><span data-stu-id="f119b-203">Enter the username that you used to create the virtual machine in the "Phase 1: Create an image" section earlier in this article.</span></span> <span data-ttu-id="f119b-204">Vous verrez quelque chose comme suit : </span><span class="sxs-lookup"><span data-stu-id="f119b-204">You will see something like the following:</span></span>  
![Capture d’écran montrant la confirmation de l’authentification][13]

## <a name="phase-3-install-software"></a><span data-ttu-id="f119b-206">Phase 3 : Installation du logiciel</span><span class="sxs-lookup"><span data-stu-id="f119b-206">Phase 3: Install software</span></span>
<span data-ttu-id="f119b-207">Dans cette phase, vous installez l’environnement d’exécution Java, Tomcat7 et d’autres composants de Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="f119b-207">In this phase, you install the Java runtime environment, Tomcat7, and other Tomcat7 components.</span></span>  

### <a name="java-runtime-environment"></a><span data-ttu-id="f119b-208">Environnement d’exécution Java</span><span class="sxs-lookup"><span data-stu-id="f119b-208">Java runtime environment</span></span>
<span data-ttu-id="f119b-209">Tomcat est écrit en Java.</span><span class="sxs-lookup"><span data-stu-id="f119b-209">Tomcat is written in Java.</span></span> <span data-ttu-id="f119b-210">Il existe deux types de Kits de développement Java (JDK), OpenJDK et JDK Oracle.</span><span class="sxs-lookup"><span data-stu-id="f119b-210">There are two kinds of Java Development Kits (JDKs), OpenJDK and Oracle JDK.</span></span> <span data-ttu-id="f119b-211">Vous pouvez choisir celui qui vous intéresse.</span><span class="sxs-lookup"><span data-stu-id="f119b-211">You can choose the one you want.</span></span>  

> [!NOTE]
> <span data-ttu-id="f119b-212">Les deux JDK ont pratiquement le même code pour les classes dans l’API Java, mais le code de la machine virtuelle est différent.</span><span class="sxs-lookup"><span data-stu-id="f119b-212">Both JDKs have almost the same code for the classes in the Java API, but the code for the virtual machine is different.</span></span> <span data-ttu-id="f119b-213">OpenJDK utilise généralement des bibliothèques libres tandis que celles de JDK Oracle sont fermées.</span><span class="sxs-lookup"><span data-stu-id="f119b-213">OpenJDK tends to use open libraries, while Oracle JDK tends to use closed ones.</span></span> <span data-ttu-id="f119b-214">Le JDK Oracle a plus de classes et quelques correctifs et il est plus stable qu’OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="f119b-214">Oracle JDK has more classes and some fixed bugs, and Oracle JDK is more stable than OpenJDK.</span></span>

#### <a name="install-openjdk"></a><span data-ttu-id="f119b-215">Installer OpenJDK</span><span class="sxs-lookup"><span data-stu-id="f119b-215">Install OpenJDK</span></span>  

<span data-ttu-id="f119b-216">Utilisez la commande suivante pour télécharger OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="f119b-216">Use the following command to download OpenJDK.</span></span>   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* <span data-ttu-id="f119b-217">Pour créer un répertoire contenant les fichiers JDK :</span><span class="sxs-lookup"><span data-stu-id="f119b-217">To create a directory to contain the JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="f119b-218">Pour extraire les fichiers JDK dans le répertoire /usr/lib/jvm :</span><span class="sxs-lookup"><span data-stu-id="f119b-218">To extract the JDK files into the /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a><span data-ttu-id="f119b-219">Installer JDK Oracle</span><span class="sxs-lookup"><span data-stu-id="f119b-219">Install Oracle JDK</span></span>


<span data-ttu-id="f119b-220">Utilisez la commande suivante pour télécharger JDK Oracle à partir du site Web d’Oracle.</span><span class="sxs-lookup"><span data-stu-id="f119b-220">Use the following command to download Oracle JDK from the Oracle website.</span></span>  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* <span data-ttu-id="f119b-221">Pour créer un répertoire contenant les fichiers JDK :</span><span class="sxs-lookup"><span data-stu-id="f119b-221">To create a directory to contain the JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="f119b-222">Pour extraire les fichiers JDK dans le répertoire /usr/lib/jvm :</span><span class="sxs-lookup"><span data-stu-id="f119b-222">To extract the JDK files into the /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* <span data-ttu-id="f119b-223">Pour définir le JDK Oracle comme machine virtuelle Java par défaut :</span><span class="sxs-lookup"><span data-stu-id="f119b-223">To set Oracle JDK as the default Java virtual machine:</span></span>  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a><span data-ttu-id="f119b-224">Confirmer que l’installation de Java a réussi</span><span class="sxs-lookup"><span data-stu-id="f119b-224">Confirm that Java installation is successful</span></span>
<span data-ttu-id="f119b-225">Vous pouvez utiliser une commande semblable à la suivante pour vérifier si l’environnement d’exécution Java est correctement installé :</span><span class="sxs-lookup"><span data-stu-id="f119b-225">You can use a command like the following to test if the Java runtime environment is installed correctly:</span></span>  

    java -version  

<span data-ttu-id="f119b-226">Si vous avez installé OpenJDK, vous devez voir un message similaire au suivant : ![Successful OpenJDK installation message][14] (Message d'installation réussie d'OpenJDK)</span><span class="sxs-lookup"><span data-stu-id="f119b-226">If you installed OpenJDK, you should see a message like the following: ![Successful OpenJDK installation message][14]</span></span>

<span data-ttu-id="f119b-227">Si vous avez installé JDK Oracle, vous devez voir un message similaire au suivant : ![Successful Oracle JDK installation message][15] (Message d'installation réussie de JDK Oracle)</span><span class="sxs-lookup"><span data-stu-id="f119b-227">If you installed Oracle JDK, you should see a message like the following: ![Successful Oracle JDK installation message][15]</span></span>

### <a name="install-tomcat7"></a><span data-ttu-id="f119b-228">Installer Tomcat7</span><span class="sxs-lookup"><span data-stu-id="f119b-228">Install Tomcat7</span></span>
<span data-ttu-id="f119b-229">Utilisez la commande suivante pour installer Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="f119b-229">Use the following command to install Tomcat7.</span></span>  

    sudo apt-get install tomcat7  

<span data-ttu-id="f119b-230">Si vous n’utilisez pas Tomcat7, utilisez la variation appropriée de cette commande.</span><span class="sxs-lookup"><span data-stu-id="f119b-230">If you are not using Tomcat7, use the appropriate variation of this command.</span></span>  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a><span data-ttu-id="f119b-231">Confirmer que l’installation de Tomcat7 a réussi</span><span class="sxs-lookup"><span data-stu-id="f119b-231">Confirm that Tomcat7 installation is successful</span></span>
<span data-ttu-id="f119b-232">Pour vérifier que Tomcat7 est correctement installé, recherchez le nom DNS de votre serveur Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f119b-232">To check if Tomcat7 is successfully installed, browse to your Tomcat server’s DNS name.</span></span> <span data-ttu-id="f119b-233">Dans cet article, l’exemple d'URL est http://tomcatexample.cloudapp.net/.</span><span class="sxs-lookup"><span data-stu-id="f119b-233">In this article, the example URL is http://tomcatexample.cloudapp.net/.</span></span> <span data-ttu-id="f119b-234">Si vous voyez un message similaire à celui-ci, Tomcat7 est correctement installé.</span><span class="sxs-lookup"><span data-stu-id="f119b-234">If you see a message like the following, Tomcat7 is installed correctly.</span></span>
<span data-ttu-id="f119b-235">![Message d’installation réussie de Tomcat7][16]</span><span class="sxs-lookup"><span data-stu-id="f119b-235">![Successful Tomcat7 installation message][16]</span></span>

### <a name="install-other-tomcat7-components"></a><span data-ttu-id="f119b-236">Installer d’autres composants de Tomcat7</span><span class="sxs-lookup"><span data-stu-id="f119b-236">Install other Tomcat7 components</span></span>
<span data-ttu-id="f119b-237">Il existe d’autres composants facultatifs de Tomcat que vous pouvez installer.</span><span class="sxs-lookup"><span data-stu-id="f119b-237">There are other optional Tomcat components that you can install.</span></span>  

<span data-ttu-id="f119b-238">Utilisez la commande **sudo apt-cache search tomcat7** pour afficher tous les composants disponibles.</span><span class="sxs-lookup"><span data-stu-id="f119b-238">Use the **sudo apt-cache search tomcat7** command to see all of the available components.</span></span> <span data-ttu-id="f119b-239">Utilisez les commandes suivantes pour installer certains composants utiles.</span><span class="sxs-lookup"><span data-stu-id="f119b-239">Use the following commands to install some useful components.</span></span>  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools to create user instances  

## <a name="phase-4-configure-tomcat7"></a><span data-ttu-id="f119b-240">Phase 4 : Configuration de Tomcat7</span><span class="sxs-lookup"><span data-stu-id="f119b-240">Phase 4: Configure Tomcat7</span></span>
<span data-ttu-id="f119b-241">Dans cette phase, vous administrez Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f119b-241">In this phase, you administer Tomcat.</span></span>

### <a name="start-and-stop-tomcat7"></a><span data-ttu-id="f119b-242">Démarrage et arrêt de Tomcat7</span><span class="sxs-lookup"><span data-stu-id="f119b-242">Start and stop Tomcat7</span></span>
<span data-ttu-id="f119b-243">Le serveur de Tomcat7 démarre automatiquement lorsque vous l’installez.</span><span class="sxs-lookup"><span data-stu-id="f119b-243">The Tomcat7 server automatically starts when you install it.</span></span> <span data-ttu-id="f119b-244">Vous pouvez également le lancer avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f119b-244">You can also start it with the following command:</span></span>   

    sudo /etc/init.d/tomcat7 start

<span data-ttu-id="f119b-245">Pour arrêter Tomcat7 :</span><span class="sxs-lookup"><span data-stu-id="f119b-245">To stop Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 stop

<span data-ttu-id="f119b-246">Pour afficher l’état de Tomcat7 :</span><span class="sxs-lookup"><span data-stu-id="f119b-246">To view the status of Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 status

<span data-ttu-id="f119b-247">Pour redémarrer les services de Tomcat :</span><span class="sxs-lookup"><span data-stu-id="f119b-247">To restart Tomcat services:</span></span> 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a><span data-ttu-id="f119b-248">Administration de Tomcat7</span><span class="sxs-lookup"><span data-stu-id="f119b-248">Tomcat7 administration</span></span>
<span data-ttu-id="f119b-249">Vous pouvez modifier le fichier de configuration utilisateur de Tomcat pour configurer vos informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="f119b-249">You can edit the Tomcat user configuration file to set up your admin credentials.</span></span> <span data-ttu-id="f119b-250">Utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f119b-250">Use the following command:</span></span>  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

<span data-ttu-id="f119b-251">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="f119b-251">Here is an example:</span></span>  
![Capture d’écran montrant la sortie de la commande sudo vi][17]  

> [!NOTE]
> <span data-ttu-id="f119b-253">Créez un mot de passe fort pour le nom d’utilisateur admin.</span><span class="sxs-lookup"><span data-stu-id="f119b-253">Create a strong password for the admin username.</span></span>  

<span data-ttu-id="f119b-254">Après avoir modifié ce fichier, vous devez redémarrer les services Tomcat7 avec la commande suivante pour vous assurer que les modifications prennent effet :</span><span class="sxs-lookup"><span data-stu-id="f119b-254">After editing this file, you should restart Tomcat7 services with the following command to ensure that the changes take effect:</span></span>  

    sudo /etc/init.d/tomcat7 restart  

<span data-ttu-id="f119b-255">Ouvrez votre navigateur et entrez l’URL **http://<your tomcat server DNS name>/manager/html**.</span><span class="sxs-lookup"><span data-stu-id="f119b-255">Open your browser, and enter **http://<your tomcat server DNS name>/manager/html** as the URL.</span></span> <span data-ttu-id="f119b-256">Pour l’exemple de cet article, l’URL est http://tomcatexample.cloudapp.net/manager/html.</span><span class="sxs-lookup"><span data-stu-id="f119b-256">For the example in this article, the URL is http://tomcatexample.cloudapp.net/manager/html.</span></span>  

<span data-ttu-id="f119b-257">Une fois connecté, vous devez voir quelque chose de similaire à ce qui suit : </span><span class="sxs-lookup"><span data-stu-id="f119b-257">After connecting, you should see something similar to the following:</span></span>  
![Capture d’écran de Tomcat Web Application Manager][18]

## <a name="common-issues"></a><span data-ttu-id="f119b-259">Problèmes courants</span><span class="sxs-lookup"><span data-stu-id="f119b-259">Common issues</span></span>
### <a name="cant-access-the-virtual-machine-with-tomcat-and-moodle-from-the-internet"></a><span data-ttu-id="f119b-260">Impossible d’accéder à une machine virtuelle avec Tomcat et Moodle à partir d’Internet</span><span class="sxs-lookup"><span data-stu-id="f119b-260">Can't access the virtual machine with Tomcat and Moodle from the Internet</span></span>
#### <a name="symptom"></a><span data-ttu-id="f119b-261">Symptôme</span><span class="sxs-lookup"><span data-stu-id="f119b-261">Symptom</span></span>  
  <span data-ttu-id="f119b-262">Tomcat est en cours d’exécution, mais vous ne voyez pas la page par défaut Tomcat avec votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="f119b-262">Tomcat is running but you can’t see the Tomcat default page with your browser.</span></span>
#### <a name="possible-root-cause"></a><span data-ttu-id="f119b-263">Cause principale possible</span><span class="sxs-lookup"><span data-stu-id="f119b-263">Possible root cause</span></span>   

  * <span data-ttu-id="f119b-264">Le port d’écoute Tomcat n’est pas identique au port privé du point de terminaison de votre machine virtuelle pour le trafic Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f119b-264">The Tomcat listen port is not the same as the private port of your virtual machine's endpoint for Tomcat traffic.</span></span>  

     <span data-ttu-id="f119b-265">Vérifiez vos paramètres de points de terminaison de port public et de port privé et assurez-vous que le port privé est identique au port d’écoute Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f119b-265">Check your public port and private port endpoint settings and make sure the private port is the same as the Tomcat listen port.</span></span> <span data-ttu-id="f119b-266">Consultez la section « Phase 1 : Création d’une image » de cet article pour obtenir des instructions sur la configuration des points de terminaison pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f119b-266">See "Phase 1: Create an image" section of this article for instructions on configuring endpoints for your virtual machine.</span></span>  

     <span data-ttu-id="f119b-267">Pour déterminer le port d’écoute de Tomcat, ouvrez /etc/httpd/conf/httpd.conf (version Red Hat) ou /etc/tomcat7/server.xml (version Debian).</span><span class="sxs-lookup"><span data-stu-id="f119b-267">To determine the Tomcat listen port, open /etc/httpd/conf/httpd.conf (Red Hat release), or /etc/tomcat7/server.xml (Debian release).</span></span> <span data-ttu-id="f119b-268">Par défaut, le port d’écoute de Tomcat est 8080.</span><span class="sxs-lookup"><span data-stu-id="f119b-268">By default, the Tomcat listen port is 8080.</span></span> <span data-ttu-id="f119b-269">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="f119b-269">Here is an example:</span></span>  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     <span data-ttu-id="f119b-270">Si vous utilisez un ordinateur virtuel comme Debian ou Ubuntu et que vous souhaitez modifier la valeur par défaut de port d’écoute de Tomcat (par exemple 8081), vous devez également ouvrir le port pour le système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="f119b-270">If you are using a virtual machine like Debian or Ubuntu and you want to change the default port of Tomcat Listen (for example 8081), you should also open the port for the operating system.</span></span> <span data-ttu-id="f119b-271">Tout d’abord, ouvrez le profil :</span><span class="sxs-lookup"><span data-stu-id="f119b-271">First, open the profile:</span></span>  

        sudo vi /etc/default/tomcat7  

     <span data-ttu-id="f119b-272">Supprimez ensuite le commentaire de la dernière ligne, puis remplacez « non » par « oui ».</span><span class="sxs-lookup"><span data-stu-id="f119b-272">Then uncomment the last line and change “no” to “yes”.</span></span>  

        AUTHBIND=yes
  2. <span data-ttu-id="f119b-273">Le pare-feu a désactivé le port d’écoute Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f119b-273">The firewall has disabled the listen port of Tomcat.</span></span>

     <span data-ttu-id="f119b-274">Vous pouvez uniquement afficher la page Tomcat par défaut à partir de l’hôte local.</span><span class="sxs-lookup"><span data-stu-id="f119b-274">You can only see the Tomcat default page from the local host.</span></span> <span data-ttu-id="f119b-275">Le problème est probablement dû au fait que le port écouté par Tomcat est bloqué par le pare-feu.</span><span class="sxs-lookup"><span data-stu-id="f119b-275">The problem is most likely that the port, which is listened to by Tomcat, is blocked by the firewall.</span></span> <span data-ttu-id="f119b-276">Vous pouvez utiliser l’outil w3m pour parcourir la page web.</span><span class="sxs-lookup"><span data-stu-id="f119b-276">You can use the w3m tool to browse the webpage.</span></span> <span data-ttu-id="f119b-277">Les commandes suivantes installent w3m et accèdent à la page par défaut Tomcat :</span><span class="sxs-lookup"><span data-stu-id="f119b-277">The following commands install w3m and browse to the Tomcat default page:</span></span>  


        <span data-ttu-id="f119b-278">sudo yum  install w3m w3m-img</span><span class="sxs-lookup"><span data-stu-id="f119b-278">sudo yum  install w3m w3m-img</span></span>


        <span data-ttu-id="f119b-279">w3m http://localhost:8080</span><span class="sxs-lookup"><span data-stu-id="f119b-279">w3m http://localhost:8080</span></span>  
#### <a name="solution"></a><span data-ttu-id="f119b-280">Solution</span><span class="sxs-lookup"><span data-stu-id="f119b-280">Solution</span></span>

  * <span data-ttu-id="f119b-281">Si le port d’écoute Tomcat n’est pas identique au port privé du point de terminaison pour le trafic sur la machine virtuelle, vous devez modifier le port privé pour qu’il soit identique au port d’écoute de Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f119b-281">If the Tomcat listen port is not the same as the private port of the endpoint for traffic to the virtual machine, you need change the private port to be the same as the Tomcat listen port.</span></span>   
  2. <span data-ttu-id="f119b-282">Si le problème est dû à firewall/iptables, ajoutez les lignes suivantes à /etc/sysconfig/iptables.</span><span class="sxs-lookup"><span data-stu-id="f119b-282">If the issue is caused by firewall/iptables, add the following lines to /etc/sysconfig/iptables.</span></span> <span data-ttu-id="f119b-283">La deuxième ligne est nécessaire uniquement pour le trafic https :</span><span class="sxs-lookup"><span data-stu-id="f119b-283">The second line is only needed for https traffic:</span></span>  

      <span data-ttu-id="f119b-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="f119b-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span></span>

      <span data-ttu-id="f119b-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="f119b-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span></span>  

     > [!IMPORTANT]
     > <span data-ttu-id="f119b-286">Assurez-vous que les lignes précédentes sont positionnées au-dessus de toutes les lignes qui limiteraient globalement l’accès, par exemple : -A INPUT -j REJECT --reject-with icmp-host-prohibited</span><span class="sxs-lookup"><span data-stu-id="f119b-286">Make sure the previous lines are positioned above any lines that would globally restrict access, such as the following: -A INPUT -j REJECT --reject-with icmp-host-prohibited</span></span>



<span data-ttu-id="f119b-287">Pour recharger les iptables, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f119b-287">To reload the iptables, run the following command:</span></span>

    service iptables restart

<span data-ttu-id="f119b-288">Cela a été testé sur CentOS 6.3.</span><span class="sxs-lookup"><span data-stu-id="f119b-288">This has been tested on CentOS 6.3.</span></span>

### <a name="permission-denied-when-you-upload-project-files-to-varlibtomcat7webapps"></a><span data-ttu-id="f119b-289">Autorisation refusée quand vous chargez des fichiers de projet vers /var/lib/tomcat7/webapps/</span><span class="sxs-lookup"><span data-stu-id="f119b-289">Permission denied when you upload project files to /var/lib/tomcat7/webapps/</span></span>
#### <a name="symptom"></a><span data-ttu-id="f119b-290">Symptôme</span><span class="sxs-lookup"><span data-stu-id="f119b-290">Symptom</span></span>
  <span data-ttu-id="f119b-291">Quand vous utilisez un client SFTP (par exemple, FileZilla) pour vous connecter à votre machine virtuelle et que vous accédez à /var/lib/tomcat7/webapps/ pour publier votre site, un message d’erreur semblable au suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="f119b-291">When you use an SFTP client (such as FileZilla) to connect to your virtual machine and navigate to /var/lib/tomcat7/webapps/ to publish your site, you get an error message similar to the following:</span></span>  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a><span data-ttu-id="f119b-292">Cause principale possible</span><span class="sxs-lookup"><span data-stu-id="f119b-292">Possible root cause</span></span>
  <span data-ttu-id="f119b-293">Vous n’êtes pas autorisé à accéder au dossier /var/lib/tomcat7/webapps.</span><span class="sxs-lookup"><span data-stu-id="f119b-293">You have no permissions to access the /var/lib/tomcat7/webapps folder.</span></span>  
#### <a name="solution"></a><span data-ttu-id="f119b-294">Solution</span><span class="sxs-lookup"><span data-stu-id="f119b-294">Solution</span></span>  
  <span data-ttu-id="f119b-295">Vous devez obtenir l’autorisation à partir du compte racine.</span><span class="sxs-lookup"><span data-stu-id="f119b-295">You need to get permission from the root account.</span></span> <span data-ttu-id="f119b-296">Vous pouvez modifier le propriétaire par défaut de ce dossier (la racine) et choisir le nom d’utilisateur que vous avez utilisé lors de l’approvisionnement de la machine.</span><span class="sxs-lookup"><span data-stu-id="f119b-296">You can change the ownership of that folder from root to the username you used when you provisioned the machine.</span></span> <span data-ttu-id="f119b-297">Voici un exemple avec le nom de compte azureuser :</span><span class="sxs-lookup"><span data-stu-id="f119b-297">Here is an example with the azureuser account name:</span></span>  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  <span data-ttu-id="f119b-298">Utilisez l’option -R pour appliquer aussi les autorisations pour tous les fichiers contenus dans un répertoire.</span><span class="sxs-lookup"><span data-stu-id="f119b-298">Use the -R option to apply the permissions for all files inside of a directory too.</span></span>  

  <span data-ttu-id="f119b-299">Cette commande fonctionne également pour les répertoires.</span><span class="sxs-lookup"><span data-stu-id="f119b-299">This command also works for directories.</span></span> <span data-ttu-id="f119b-300">L’option -R modifie les autorisations pour tous les fichiers et répertoires contenus dans le répertoire.</span><span class="sxs-lookup"><span data-stu-id="f119b-300">The -R option changes the permissions for all files and directories inside the directory.</span></span> <span data-ttu-id="f119b-301">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="f119b-301">Here is an example:</span></span>  

     sudo chown -R username:group directory  

  <span data-ttu-id="f119b-302">Cette commande modifie le propriétaire (utilisateur et groupe) pour tous les fichiers et répertoires contenus dans le répertoire.</span><span class="sxs-lookup"><span data-stu-id="f119b-302">This command changes ownership (both user and group) for all files and directories that are inside the directory.</span></span>  

  <span data-ttu-id="f119b-303">La commande suivante modifie uniquement l’autorisation du répertoire.</span><span class="sxs-lookup"><span data-stu-id="f119b-303">The following command only changes the permission of the folder directory.</span></span> <span data-ttu-id="f119b-304">Les fichiers et dossiers dans le répertoire restent intacts.</span><span class="sxs-lookup"><span data-stu-id="f119b-304">The files and folders inside the directory are not changed.</span></span>  

     sudo chown username:group directory

[1]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-01.png
[2]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-02.png
[3]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-03.png
[4]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-04.png
[5]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-05.png
[6]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-06.png
[7]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-07.png
[8]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-08.png
[9]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-09.png
[10]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-10.png
[11]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-11.png
[12]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-12.png
[13]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-13.png
[14]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-14.png
[15]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-15.png
[16]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-16.png
[17]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-17.png
[18]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-18.png
