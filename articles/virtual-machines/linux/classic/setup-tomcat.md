---
title: "aaaSet d’Apache Tomcat sur une machine virtuelle Linux | Documents Microsoft"
description: "Découvrez comment tooset d’Apache Tomcat7 à l’aide de Machines virtuelles Azure exécutant Linux."
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
ms.openlocfilehash: b837a73e91fcb25d5459d993a0e93ceef1a1fc8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a><span data-ttu-id="ec0ec-103">Configurer Tomcat7 sur une machine virtuelle Linux avec Azure</span><span class="sxs-lookup"><span data-stu-id="ec0ec-103">Set up Tomcat7 on a Linux virtual machine with Azure</span></span>
<span data-ttu-id="ec0ec-104">Apache Tomcat (ou simplement Tomcat, également anciennement appelé Jakarta Tomcat) est un serveur web open source et un conteneur de servlet développé par hello Apache Software Foundation ASF ().</span><span class="sxs-lookup"><span data-stu-id="ec0ec-104">Apache Tomcat (or simply Tomcat, also formerly called Jakarta Tomcat) is an open source web server and servlet container developed by hello Apache Software Foundation (ASF).</span></span> <span data-ttu-id="ec0ec-105">Tomcat implémente hello Servlet Java et les spécifications de Java Server Pages (JSP) hello de Sun Microsystems.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-105">Tomcat implements hello Java Servlet and hello JavaServer Pages (JSP) specifications from Sun Microsystems.</span></span> <span data-ttu-id="ec0ec-106">Tomcat fournit un environnement de serveur web HTTP de Java pur dans le code Java toorun.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-106">Tomcat provides a pure Java HTTP web server environment in which toorun Java code.</span></span> <span data-ttu-id="ec0ec-107">Dans la configuration la plus simple de hello, Tomcat s’exécute dans un processus de système d’exploitation unique.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-107">In hello simplest configuration, Tomcat runs in a single operating system process.</span></span> <span data-ttu-id="ec0ec-108">Ce processus exécute une machine virtuelle Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="ec0ec-108">This process runs a Java virtual machine (JVM).</span></span> <span data-ttu-id="ec0ec-109">Toutes les demandes HTTP à partir d’un navigateur de tooTomcat sont traité comme un thread distinct dans le processus de Tomcat hello.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-109">Every HTTP request from a browser tooTomcat is processed as a separate thread in hello Tomcat process.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="ec0ec-110">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Azure Resource Manager et classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ec0ec-110">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ec0ec-111">Cet article décrit comment toouse hello modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-111">This article covers how toouse hello classic deployment model.</span></span> <span data-ttu-id="ec0ec-112">Nous recommandons que la plupart des nouveaux déploiements utilisent le modèle de gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-112">We recommend that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="ec0ec-113">toouse un toodeploy de modèle de gestionnaire de ressources une VM Ubuntu avec Open JDK et Tomcat, consultez [cet article](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span><span class="sxs-lookup"><span data-stu-id="ec0ec-113">toouse a Resource Manager template toodeploy an Ubuntu VM with Open JDK and Tomcat, see [this article](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span></span>

<span data-ttu-id="ec0ec-114">Dans cet article, vous installerez Tomcat7 sur une image Linux et le déploierez dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-114">In this article, you will install Tomcat7 on a Linux image and deploy it in Azure.</span></span>  

<span data-ttu-id="ec0ec-115">Vous apprendrez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-115">You will learn:</span></span>  

* <span data-ttu-id="ec0ec-116">Comment toocreate une machine virtuelle dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-116">How toocreate a virtual machine in Azure.</span></span>
* <span data-ttu-id="ec0ec-117">Comment tooprepare hello machine virtuelle pour Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-117">How tooprepare hello virtual machine for Tomcat7.</span></span>
* <span data-ttu-id="ec0ec-118">Comment tooinstall Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-118">How tooinstall Tomcat7.</span></span>

<span data-ttu-id="ec0ec-119">Nous partons du principe que vous possédez déjà un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-119">It is assumed that you already have an Azure subscription.</span></span>  <span data-ttu-id="ec0ec-120">Si non, vous pouvez vous inscrire pour une évaluation gratuite à [hello site Web Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="ec0ec-120">If not, you can sign up for a free trial at [hello Azure website](https://azure.microsoft.com/).</span></span> <span data-ttu-id="ec0ec-121">Si vous disposez d’un abonnement MSDN, consultez la page présentant les [tarifs préférentiels Microsoft Azure : avantages MSDN, MPN et BizSpark](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span><span class="sxs-lookup"><span data-stu-id="ec0ec-121">If you have an MSDN subscription, see [Microsoft Azure Special Pricing: MSDN, MPN, and BizSpark Benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span></span> <span data-ttu-id="ec0ec-122">toolearn en savoir plus sur Azure, consultez [Nouveautés Azure ?](https://azure.microsoft.com/overview/what-is-azure/).</span><span class="sxs-lookup"><span data-stu-id="ec0ec-122">toolearn more about Azure, see [What is Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span></span>

<span data-ttu-id="ec0ec-123">Cet article suppose que vous avez des connaissances de base relatives à Tomcat et Linux.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-123">This article assumes that you have a basic working knowledge of Tomcat and Linux.</span></span>  

## <a name="phase-1-create-an-image"></a><span data-ttu-id="ec0ec-124">Phase 1 : Création d’une image</span><span class="sxs-lookup"><span data-stu-id="ec0ec-124">Phase 1: Create an image</span></span>
<span data-ttu-id="ec0ec-125">Lors de cette phase, vous allez créer une machine virtuelle à l’aide d’une image Linux dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-125">In this phase, you will create a virtual machine by using a Linux image in Azure.</span></span>  

### <a name="step-1-generate-an-ssh-authentication-key"></a><span data-ttu-id="ec0ec-126">Étape 1 : Générer une clé d’authentification SSH</span><span class="sxs-lookup"><span data-stu-id="ec0ec-126">Step 1: Generate an SSH authentication key</span></span>
<span data-ttu-id="ec0ec-127">SSH est un outil important pour les administrateurs système.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-127">SSH is an important tool for system administrators.</span></span> <span data-ttu-id="ec0ec-128">Toutefois, une configuration de la sécurité d’accès basée sur un mot de passe déterminé par l’homme n’est pas recommandée.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-128">However, configuring access security based on a human-determined password is not recommended.</span></span> <span data-ttu-id="ec0ec-129">Les utilisateurs malveillants peuvent s’introduire dans votre système si vous disposez d’un nom d’utilisateur et d’un mot de passe faibles.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-129">Malicious users can break into your system based on a username and a weak password.</span></span>

<span data-ttu-id="ec0ec-130">excellente Hello est qu’il existe un moyen de l’accès à distance tooleave ouvrir et ne vous inquiétez pas sur les mots de passe.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-130">hello good news is that there is a way tooleave remote access open and not worry about passwords.</span></span> <span data-ttu-id="ec0ec-131">Cette méthode se compose d’une authentification avec chiffrement asymétrique.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-131">This method consists of authentication with asymmetric cryptography.</span></span> <span data-ttu-id="ec0ec-132">Hello clé privée de l’utilisateur est hello qui accorde l’authentification hello.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-132">hello user’s private key is hello one that grants hello authentication.</span></span> <span data-ttu-id="ec0ec-133">Vous pouvez verrouiller même compte d’utilisateur hello toonot autoriser l’authentification du mot de passe.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-133">You can even lock hello user’s account toonot allow password authentication.</span></span>

<span data-ttu-id="ec0ec-134">Un autre avantage de cette méthode est que vous n’avez pas besoin de toosign de mots de passe différents dans les serveurs toodifferent.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-134">Another advantage of this method is that you do not need different passwords toosign in toodifferent servers.</span></span> <span data-ttu-id="ec0ec-135">Vous pouvez vous authentifier à l’aide de clé privée personnelle de hello sur tous les serveurs, ce qui vous évite d’avoir tooremember plusieurs mots de passe.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-135">You can authenticate by using hello personal private key on all servers, which prevents you from having tooremember several passwords.</span></span>



<span data-ttu-id="ec0ec-136">Suivez ces étapes toogenerate hello authentification code SSH.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-136">Follow these steps toogenerate hello SSH authentication key.</span></span>

1. <span data-ttu-id="ec0ec-137">Téléchargez et installez PuTTYgen hello l’emplacement suivant : [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="ec0ec-137">Download and install PuTTYgen from hello following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
2. <span data-ttu-id="ec0ec-138">Exécutez Puttygen.exe.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-138">Run Puttygen.exe.</span></span>
3. <span data-ttu-id="ec0ec-139">Cliquez sur **générer** toogenerate les clés hello.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-139">Click **Generate** toogenerate hello keys.</span></span> <span data-ttu-id="ec0ec-140">Dans le processus de hello, vous pouvez augmenter le caractère aléatoire par déplacement de la souris hello sur une zone vide de hello dans la fenêtre hello.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-140">In hello process, you can increase randomness by moving hello mouse over hello blank area in hello window.</span></span>  
   <span data-ttu-id="ec0ec-141">![PuTTY Générateur de clés capture d’écran hello générer de nouveau bouton clé][1]</span><span class="sxs-lookup"><span data-stu-id="ec0ec-141">![PuTTY Key Generator screenshot that shows hello generate new key button][1]</span></span>
4. <span data-ttu-id="ec0ec-142">Une fois hello générer un processus, Puttygen.exe présentent votre nouvelle clé publique.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-142">After hello generate process, Puttygen.exe will show your new public key.</span></span>  
   ![Capture d’écran Générateur de clé puTTY qui affiche la clé publique hello et hello enregistrer bouton clé privée][2]
5. <span data-ttu-id="ec0ec-144">Sélectionnez et copiez la clé publique de hello et enregistrez-le dans un fichier nommé publicKey.pem.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-144">Select and copy hello public key, and save it in a file named publicKey.pem.</span></span> <span data-ttu-id="ec0ec-145">Ne cliquez pas sur **clé publique d’enregistrement**, car hello enregistré le format de fichier de la clé publique est différent de la clé publique hello nous voulons.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-145">Don’t click **Save public key**, because hello saved public key’s file format is different from hello public key we want.</span></span>
6. <span data-ttu-id="ec0ec-146">Cliquez sur **Save private key** et enregistrez-la dans un fichier nommé privateKey.ppk.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-146">Click **Save private key**, and save it in a file named privateKey.ppk.</span></span>

### <a name="step-2-create-hello-image-in-hello-azure-portal"></a><span data-ttu-id="ec0ec-147">Étape 2 : Créer l’image de hello Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="ec0ec-147">Step 2: Create hello image in hello Azure portal</span></span>
1. <span data-ttu-id="ec0ec-148">Bonjour [portal](https://portal.azure.com/), cliquez sur **nouveau** Bonjour barre des tâches toocreate une image.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-148">In hello [portal](https://portal.azure.com/), click **New** in hello task bar toocreate an image.</span></span> <span data-ttu-id="ec0ec-149">Choisissez ensuite l’image Linux hello selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-149">Then choose hello Linux image that is based on your needs.</span></span> <span data-ttu-id="ec0ec-150">Hello exemple suivant utilise hello Ubuntu 14.04 image.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-150">hello following example uses hello Ubuntu 14.04 image.</span></span>
<span data-ttu-id="ec0ec-151">![Capture d’écran du portail hello qui montre le bouton nouvelle de hello][3]</span><span class="sxs-lookup"><span data-stu-id="ec0ec-151">![Screenshot of hello portal that shows hello New button][3]</span></span>

2. <span data-ttu-id="ec0ec-152">Pour **nom d’hôte**, spécifiez nom hello pour hello les URL que vous et les clients Internet utilisera tooaccess cet ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-152">For **Host Name**, specify hello name for hello URL that you and Internet clients will use tooaccess this virtual machine.</span></span> <span data-ttu-id="ec0ec-153">Définissez hello dernière partie du nom DNS de hello, par exemple, tomcatdemo.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-153">Define hello last part of hello DNS name, for example, tomcatdemo.</span></span> <span data-ttu-id="ec0ec-154">Azure génèrera hello URL en tant que tomcatdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-154">Azure will then generate hello URL as tomcatdemo.cloudapp.net.</span></span>  

3. <span data-ttu-id="ec0ec-155">Pour **clé d’authentification SSH**, copiez la valeur de clé de hello à partir du fichier hello publicKey.pem, qui contient la clé publique de hello généré par PuTTYgen.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-155">For **SSH Authentication Key**, copy hello key value from hello publicKey.pem file, which contains hello public key generated by PuTTYgen.</span></span>  
<span data-ttu-id="ec0ec-156">![Clé d’authentification SSH zone dans le portail de hello][4]</span><span class="sxs-lookup"><span data-stu-id="ec0ec-156">![SSH Authentication Key box in hello portal][4]</span></span>

4. <span data-ttu-id="ec0ec-157">Configurez d’autres paramètres selon les besoins, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-157">Configure other settings as needed, and then click **Create**.</span></span>  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a><span data-ttu-id="ec0ec-158">Phase 2 : Préparation de la machine virtuelle pour Tomcat7</span><span class="sxs-lookup"><span data-stu-id="ec0ec-158">Phase 2: Prepare your virtual machine for Tomcat7</span></span>
<span data-ttu-id="ec0ec-159">Dans cette phase, vous configurerez un point de terminaison pour le trafic de Tomcat et puis connectez-vous tooyour machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-159">In this phase, you will configure an endpoint for Tomcat traffic, and then connect tooyour new virtual machine.</span></span>

### <a name="step-1-open-hello-http-port-tooallow-web-access"></a><span data-ttu-id="ec0ec-160">Étape 1 : Ouvrir l’accès web hello HTTP port tooallow</span><span class="sxs-lookup"><span data-stu-id="ec0ec-160">Step 1: Open hello HTTP port tooallow web access</span></span>
<span data-ttu-id="ec0ec-161">Les points de terminaison dans Azure se composent d’un protocole TCP ou UDP et d’un port public et privé.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-161">Endpoints in Azure consist of a TCP or UDP protocol, along with a public and private port.</span></span> <span data-ttu-id="ec0ec-162">Hello privé hello port est que hello écoutent tooon hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-162">hello private port is hello port that hello service is listening tooon hello virtual machine.</span></span> <span data-ttu-id="ec0ec-163">port public de Hello est le port hello hello service cloud Azure écoute tooexternally pour le trafic entrant, basés sur Internet.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-163">hello public port is hello port that hello Azure cloud service listens tooexternally for incoming, Internet-based traffic.</span></span>  

<span data-ttu-id="ec0ec-164">Le port TCP 8080 est le numéro de port par défaut hello que Tomcat utilise toolisten.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-164">TCP port 8080 is hello default port number that Tomcat uses toolisten.</span></span> <span data-ttu-id="ec0ec-165">Si ce port est ouvert avec un point de terminaison Azure, vous pouvez (vous et d’autres clients Internet) accéder aux pages Tomcat.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-165">If this port is opened with an Azure endpoint, you and other Internet clients can access Tomcat pages.</span></span>  

1. <span data-ttu-id="ec0ec-166">Dans le portail de hello, cliquez sur **Parcourir** > **virtuels**, puis cliquez sur la machine virtuelle hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-166">In hello portal, click **Browse** > **Virtual machines**, and then click hello virtual machine that you created.</span></span>  
   <span data-ttu-id="ec0ec-167">![Capture d’écran du répertoire des ordinateurs virtuels hello][5]</span><span class="sxs-lookup"><span data-stu-id="ec0ec-167">![Screenshot of hello Virtual machines directory][5]</span></span>
2. <span data-ttu-id="ec0ec-168">tooadd une machine virtuelle de tooyour de point de terminaison, cliquez sur hello **points de terminaison** boîte.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-168">tooadd an endpoint tooyour virtual machine, click hello **Endpoints** box.</span></span>
   <span data-ttu-id="ec0ec-169">![Capture d’écran qui affiche la boîte de points de terminaison hello][6]</span><span class="sxs-lookup"><span data-stu-id="ec0ec-169">![Screenshot that shows hello Endpoints box][6]</span></span>
3. <span data-ttu-id="ec0ec-170">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-170">Click **Add**.</span></span>  

   1. <span data-ttu-id="ec0ec-171">Pour le point de terminaison hello, entrez un nom pour le point de terminaison hello dans **point de terminaison**, puis entrez 80 dans **Port Public**.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-171">For hello endpoint, enter a name for hello endpoint in **Endpoint**, and then enter 80 in **Public Port**.</span></span>  

      <span data-ttu-id="ec0ec-172">Si vous lui affectez too80, vous n’avez pas besoin numéro de port tooinclude hello dans URL hello utilisé tooaccess Tomcat.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-172">If you set it too80, you don’t need tooinclude hello port number in hello URL that is used tooaccess Tomcat.</span></span> <span data-ttu-id="ec0ec-173">Par exemple, http://tomcatdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-173">For example, http://tomcatdemo.cloudapp.net.</span></span>    

      <span data-ttu-id="ec0ec-174">Si vous lui affectez la valeur tooanother, telles que 81, vous devez tooadd hello port numéro toohello URL tooaccess Tomcat.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-174">If you set it tooanother value, such as 81, you need tooadd hello port number toohello URL tooaccess Tomcat.</span></span> <span data-ttu-id="ec0ec-175">Par exemple, http://tomcatdemo.cloudapp.net:81/.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-175">For example,  http://tomcatdemo.cloudapp.net:81/.</span></span>
   2. <span data-ttu-id="ec0ec-176">Tapez 8080 dans **Port privé**.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-176">Enter 8080 in **Private Port**.</span></span> <span data-ttu-id="ec0ec-177">Par défaut, Tomcat écoute sur le port TCP 8080.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-177">By default, Tomcat listens on TCP port 8080.</span></span> <span data-ttu-id="ec0ec-178">Si vous avez modifié le port hello par défaut d’écoute de Tomcat, vous devez mettre à jour **Port privé** toobe hello identique hello du port d’écoute de Tomcat.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-178">If you changed hello default listen port of Tomcat, you should update **Private Port** toobe hello same as hello Tomcat listen port.</span></span>  
      <span data-ttu-id="ec0ec-179">![Capture d’écran de l’interface utilisateur montrant la commande Ajouter, Port public et Port privé][7]</span><span class="sxs-lookup"><span data-stu-id="ec0ec-179">![Screenshot of UI that shows Add command, Public Port, and Private Port][7]</span></span>
4. <span data-ttu-id="ec0ec-180">Cliquez sur **OK** tooadd hello point de terminaison tooyour virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-180">Click **OK** tooadd hello endpoint tooyour virtual machine.</span></span>

### <a name="step-2-connect-toohello-image-you-created"></a><span data-ttu-id="ec0ec-181">Étape 2 : Connexion image toohello que vous avez créé</span><span class="sxs-lookup"><span data-stu-id="ec0ec-181">Step 2: Connect toohello image you created</span></span>
<span data-ttu-id="ec0ec-182">Vous pouvez choisir n’importe quel ordinateur virtuel SSH outil tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-182">You can choose any SSH tool tooconnect tooyour virtual machine.</span></span> <span data-ttu-id="ec0ec-183">Dans cet exemple, nous utilisons PuTTY.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-183">In this example, we use PuTTY.</span></span>  

1. <span data-ttu-id="ec0ec-184">Obtenir le nom DNS de hello de votre machine virtuelle à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-184">Get hello DNS name of your virtual machine from hello portal.</span></span>
    1. <span data-ttu-id="ec0ec-185">Cliquez sur **Parcourir** > **Machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-185">Click **Browse** > **Virtual machines**.</span></span>
    2. <span data-ttu-id="ec0ec-186">Sélectionnez le nom hello de votre machine virtuelle, puis cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-186">Select hello name of your virtual machine, and then click **Properties**.</span></span>
    3. <span data-ttu-id="ec0ec-187">Bonjour **propriétés** vignette, regardez dans hello **nom de domaine** nom DNS de boîte tooget hello.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-187">In hello **Properties** tile, look in hello **Domain Name** box tooget hello DNS name.</span></span>  

2. <span data-ttu-id="ec0ec-188">Obtenir le numéro de port hello pour les connexions SSH à partir de hello **SSH** boîte.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-188">Get hello port number for SSH connections from hello **SSH** box.</span></span>  
<span data-ttu-id="ec0ec-189">![Capture d’écran qui affiche le numéro de port de connexion SSH hello][8]</span><span class="sxs-lookup"><span data-stu-id="ec0ec-189">![Screenshot that shows hello SSH connection port number][8]</span></span>

3. <span data-ttu-id="ec0ec-190">Téléchargez [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="ec0ec-190">Download [PuTTY](http://www.putty.org/).</span></span>  

4. <span data-ttu-id="ec0ec-191">Après avoir téléchargé, cliquez sur le fichier exécutable de hello Putty.exe.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-191">After downloading, click hello executable file Putty.exe.</span></span> <span data-ttu-id="ec0ec-192">Dans la configuration de PuTTY, configurer les options de base hello avec le nom d’hôte hello et le port de nombre est obtenu à partir des propriétés hello de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-192">In PuTTY configuration, configure hello basic options with hello host name and port number that is obtained from hello properties of your virtual machine.</span></span>   
![Capture d’écran qui affiche des options de nom et le ports hôte configuration PuTTY de hello][9]

5. <span data-ttu-id="ec0ec-194">Dans le volet gauche de hello, cliquez sur **connexion** > **SSH** > **Auth**, puis cliquez sur **Parcourir** toospecify emplacement Hello du fichier de privateKey.ppk hello.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-194">In hello left pane, click **Connection** > **SSH** > **Auth**, and then click **Browse** toospecify hello location of hello privateKey.ppk file.</span></span> <span data-ttu-id="ec0ec-195">fichier de privateKey.ppk de Hello contient la clé privée hello qui est généré par PuTTYgen plus haut dans hello « Phase 1 : créer une image « section de cet article.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-195">hello privateKey.ppk file contains hello private key that is generated by PuTTYgen earlier in hello "Phase 1: Create an image" section of this article.</span></span>  
<span data-ttu-id="ec0ec-196">![Capture d’écran qui affiche la hiérarchie de répertoires de connexion hello et le bouton Parcourir][10]</span><span class="sxs-lookup"><span data-stu-id="ec0ec-196">![Screenshot that shows hello Connection directory hierarchy and Browse button][10]</span></span>

6. <span data-ttu-id="ec0ec-197">Cliquez sur **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-197">Click **Open**.</span></span> <span data-ttu-id="ec0ec-198">Une boîte de message peut s’afficher.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-198">You might be alerted by a message box.</span></span> <span data-ttu-id="ec0ec-199">Si vous avez configuré nom DNS de hello et numéro de port correctement, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-199">If you have configured hello DNS name and port number correctly, click **Yes**.</span></span>
<span data-ttu-id="ec0ec-200">![Capture d’écran qui affiche la notification de hello][11]</span><span class="sxs-lookup"><span data-stu-id="ec0ec-200">![Screenshot that shows hello notification][11]</span></span>

7. <span data-ttu-id="ec0ec-201">Vous est demandée tooenter votre nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-201">You are prompted tooenter your username.</span></span>  
![Capture d’écran de qui indique où le nom d’utilisateur tooenter][12]

8. <span data-ttu-id="ec0ec-203">Entrez le nom d’utilisateur hello que vous avez utilisé un ordinateur virtuel de hello toocreate Bonjour « Phase 1 : créer une image » plus haut dans cet article.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-203">Enter hello username that you used toocreate hello virtual machine in hello "Phase 1: Create an image" section earlier in this article.</span></span> <span data-ttu-id="ec0ec-204">Vous verrez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-204">You will see something like hello following:</span></span>  
![Capture d’écran qui affiche la confirmation de l’authentification de hello][13]

## <a name="phase-3-install-software"></a><span data-ttu-id="ec0ec-206">Phase 3 : Installation du logiciel</span><span class="sxs-lookup"><span data-stu-id="ec0ec-206">Phase 3: Install software</span></span>
<span data-ttu-id="ec0ec-207">Dans cette phase, vous installez hello Java runtime environment, Tomcat7 et autres composants Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-207">In this phase, you install hello Java runtime environment, Tomcat7, and other Tomcat7 components.</span></span>  

### <a name="java-runtime-environment"></a><span data-ttu-id="ec0ec-208">Environnement d’exécution Java</span><span class="sxs-lookup"><span data-stu-id="ec0ec-208">Java runtime environment</span></span>
<span data-ttu-id="ec0ec-209">Tomcat est écrit en Java.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-209">Tomcat is written in Java.</span></span> <span data-ttu-id="ec0ec-210">Il existe deux types de Kits de développement Java (JDK), OpenJDK et JDK Oracle.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-210">There are two kinds of Java Development Kits (JDKs), OpenJDK and Oracle JDK.</span></span> <span data-ttu-id="ec0ec-211">Vous pouvez choisir hello celui que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-211">You can choose hello one you want.</span></span>  

> [!NOTE]
> <span data-ttu-id="ec0ec-212">À la fois JDK ont pratiquement les hello même code pour les classes hello Bonjour API Java, mais le code hello pour la machine virtuelle de hello est différent.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-212">Both JDKs have almost hello same code for hello classes in hello Java API, but hello code for hello virtual machine is different.</span></span> <span data-ttu-id="ec0ec-213">OpenJDK a tendance à toouse les bibliothèques open, tandis que le JDK Oracle tend toouse fermé celles.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-213">OpenJDK tends toouse open libraries, while Oracle JDK tends toouse closed ones.</span></span> <span data-ttu-id="ec0ec-214">Le JDK Oracle a plus de classes et quelques correctifs et il est plus stable qu’OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-214">Oracle JDK has more classes and some fixed bugs, and Oracle JDK is more stable than OpenJDK.</span></span>

#### <a name="install-openjdk"></a><span data-ttu-id="ec0ec-215">Installer OpenJDK</span><span class="sxs-lookup"><span data-stu-id="ec0ec-215">Install OpenJDK</span></span>  

<span data-ttu-id="ec0ec-216">Utilisez hello suivant toodownload de commande OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-216">Use hello following command toodownload OpenJDK.</span></span>   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* <span data-ttu-id="ec0ec-217">toocreate un toocontain directory hello des fichiers JDK :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-217">toocreate a directory toocontain hello JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="ec0ec-218">fichiers de JDK tooextract hello dans le répertoire/usr/lib/jvm/hello :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-218">tooextract hello JDK files into hello /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a><span data-ttu-id="ec0ec-219">Installer JDK Oracle</span><span class="sxs-lookup"><span data-stu-id="ec0ec-219">Install Oracle JDK</span></span>


<span data-ttu-id="ec0ec-220">Utilisez hello suivant toodownload de commande JDK Oracle à partir du site Web de Oracle hello.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-220">Use hello following command toodownload Oracle JDK from hello Oracle website.</span></span>  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* <span data-ttu-id="ec0ec-221">toocreate un toocontain directory hello des fichiers JDK :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-221">toocreate a directory toocontain hello JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="ec0ec-222">fichiers de JDK tooextract hello dans le répertoire/usr/lib/jvm/hello :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-222">tooextract hello JDK files into hello /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* <span data-ttu-id="ec0ec-223">tooset JDK Oracle comme hello par défaut machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-223">tooset Oracle JDK as hello default Java virtual machine:</span></span>  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a><span data-ttu-id="ec0ec-224">Confirmer que l’installation de Java a réussi</span><span class="sxs-lookup"><span data-stu-id="ec0ec-224">Confirm that Java installation is successful</span></span>
<span data-ttu-id="ec0ec-225">Vous pouvez utiliser une commande telle que hello suivant tootest si l’environnement d’exécution Java hello est correctement installé :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-225">You can use a command like hello following tootest if hello Java runtime environment is installed correctly:</span></span>  

    java -version  

<span data-ttu-id="ec0ec-226">Si vous avez installé OpenJDK, vous devez voir un message hello suivante : ![message OpenJDK réussie de l’installation][14]</span><span class="sxs-lookup"><span data-stu-id="ec0ec-226">If you installed OpenJDK, you should see a message like hello following: ![Successful OpenJDK installation message][14]</span></span>

<span data-ttu-id="ec0ec-227">Si vous avez installé le JDK Oracle, vous devez voir un message hello suivante : ![message d’installation réussie JDK Oracle][15]</span><span class="sxs-lookup"><span data-stu-id="ec0ec-227">If you installed Oracle JDK, you should see a message like hello following: ![Successful Oracle JDK installation message][15]</span></span>

### <a name="install-tomcat7"></a><span data-ttu-id="ec0ec-228">Installer Tomcat7</span><span class="sxs-lookup"><span data-stu-id="ec0ec-228">Install Tomcat7</span></span>
<span data-ttu-id="ec0ec-229">Utilisez hello suivant commande tooinstall Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-229">Use hello following command tooinstall Tomcat7.</span></span>  

    sudo apt-get install tomcat7  

<span data-ttu-id="ec0ec-230">Si vous n’utilisez pas Tomcat7, conservez hello approprié de cette commande.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-230">If you are not using Tomcat7, use hello appropriate variation of this command.</span></span>  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a><span data-ttu-id="ec0ec-231">Confirmer que l’installation de Tomcat7 a réussi</span><span class="sxs-lookup"><span data-stu-id="ec0ec-231">Confirm that Tomcat7 installation is successful</span></span>
<span data-ttu-id="ec0ec-232">toocheck si Tomcat7 est installé avec succès, parcourir le nom DNS du serveur tooyour Tomcat.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-232">toocheck if Tomcat7 is successfully installed, browse tooyour Tomcat server’s DNS name.</span></span> <span data-ttu-id="ec0ec-233">Dans cet article, exemple d’URL hello est http://tomcatexample.cloudapp.net/.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-233">In this article, hello example URL is http://tomcatexample.cloudapp.net/.</span></span> <span data-ttu-id="ec0ec-234">Si vous voyez un message comme hello suivant, Tomcat7 est correctement installé.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-234">If you see a message like hello following, Tomcat7 is installed correctly.</span></span>
<span data-ttu-id="ec0ec-235">![Message d’installation réussie de Tomcat7][16]</span><span class="sxs-lookup"><span data-stu-id="ec0ec-235">![Successful Tomcat7 installation message][16]</span></span>

### <a name="install-other-tomcat7-components"></a><span data-ttu-id="ec0ec-236">Installer d’autres composants de Tomcat7</span><span class="sxs-lookup"><span data-stu-id="ec0ec-236">Install other Tomcat7 components</span></span>
<span data-ttu-id="ec0ec-237">Il existe d’autres composants facultatifs de Tomcat que vous pouvez installer.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-237">There are other optional Tomcat components that you can install.</span></span>  

<span data-ttu-id="ec0ec-238">Hello d’utilisation **sudo apt-cache recherche tomcat7** commande toosee tous les composants disponibles hello.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-238">Use hello **sudo apt-cache search tomcat7** command toosee all of hello available components.</span></span> <span data-ttu-id="ec0ec-239">Utilisez hello suivant de commandes tooinstall certains composants utiles.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-239">Use hello following commands tooinstall some useful components.</span></span>  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools toocreate user instances  

## <a name="phase-4-configure-tomcat7"></a><span data-ttu-id="ec0ec-240">Phase 4 : Configuration de Tomcat7</span><span class="sxs-lookup"><span data-stu-id="ec0ec-240">Phase 4: Configure Tomcat7</span></span>
<span data-ttu-id="ec0ec-241">Dans cette phase, vous administrez Tomcat.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-241">In this phase, you administer Tomcat.</span></span>

### <a name="start-and-stop-tomcat7"></a><span data-ttu-id="ec0ec-242">Démarrage et arrêt de Tomcat7</span><span class="sxs-lookup"><span data-stu-id="ec0ec-242">Start and stop Tomcat7</span></span>
<span data-ttu-id="ec0ec-243">serveur de Tomcat7 Hello démarre automatiquement lorsque vous l’installez.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-243">hello Tomcat7 server automatically starts when you install it.</span></span> <span data-ttu-id="ec0ec-244">Vous pouvez également le démarrer avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-244">You can also start it with hello following command:</span></span>   

    sudo /etc/init.d/tomcat7 start

<span data-ttu-id="ec0ec-245">toostop Tomcat7 :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-245">toostop Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 stop

<span data-ttu-id="ec0ec-246">état de hello tooview de Tomcat7 :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-246">tooview hello status of Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 status

<span data-ttu-id="ec0ec-247">services de Tomcat toorestart :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-247">toorestart Tomcat services:</span></span> 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a><span data-ttu-id="ec0ec-248">Administration de Tomcat7</span><span class="sxs-lookup"><span data-stu-id="ec0ec-248">Tomcat7 administration</span></span>
<span data-ttu-id="ec0ec-249">Vous pouvez modifier hello Tomcat utilisateur configuration fichier tooset de vos informations d’identification d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-249">You can edit hello Tomcat user configuration file tooset up your admin credentials.</span></span> <span data-ttu-id="ec0ec-250">Utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-250">Use hello following command:</span></span>  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

<span data-ttu-id="ec0ec-251">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-251">Here is an example:</span></span>  
![Capture d’écran qui affiche la sortie de la commande hello sudo vi][17]  

> [!NOTE]
> <span data-ttu-id="ec0ec-253">Créer un mot de passe fort pour le nom d’utilisateur administrateur de hello.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-253">Create a strong password for hello admin username.</span></span>  

<span data-ttu-id="ec0ec-254">Après avoir modifié ce fichier, vous devez redémarrer les services Tomcat7 par hello suivant tooensure commande que hello modifications prennent effet :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-254">After editing this file, you should restart Tomcat7 services with hello following command tooensure that hello changes take effect:</span></span>  

    sudo /etc/init.d/tomcat7 restart  

<span data-ttu-id="ec0ec-255">Ouvrez votre navigateur et entrez **http://<your tomcat server DNS name>/manager/html** comme hello URL.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-255">Open your browser, and enter **http://<your tomcat server DNS name>/manager/html** as hello URL.</span></span> <span data-ttu-id="ec0ec-256">Par exemple hello dans cet article, les URL de hello est http://tomcatexample.cloudapp.net/manager/html.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-256">For hello example in this article, hello URL is http://tomcatexample.cloudapp.net/manager/html.</span></span>  

<span data-ttu-id="ec0ec-257">Une fois connecté, vous devez voir s’afficher quelque chose de similaire toohello :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-257">After connecting, you should see something similar toohello following:</span></span>  
![Capture d’écran de hello Gestionnaire d’applications Web Tomcat][18]

## <a name="common-issues"></a><span data-ttu-id="ec0ec-259">Problèmes courants</span><span class="sxs-lookup"><span data-stu-id="ec0ec-259">Common issues</span></span>
### <a name="cant-access-hello-virtual-machine-with-tomcat-and-moodle-from-hello-internet"></a><span data-ttu-id="ec0ec-260">Impossible d’accéder à machine virtuelle hello Tomcat et Moodle de hello Internet</span><span class="sxs-lookup"><span data-stu-id="ec0ec-260">Can't access hello virtual machine with Tomcat and Moodle from hello Internet</span></span>
#### <a name="symptom"></a><span data-ttu-id="ec0ec-261">Symptôme</span><span class="sxs-lookup"><span data-stu-id="ec0ec-261">Symptom</span></span>  
  <span data-ttu-id="ec0ec-262">Tomcat est en cours d’exécution, mais vous ne voyez pas la page par défaut hello Tomcat avec votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-262">Tomcat is running but you can’t see hello Tomcat default page with your browser.</span></span>
#### <a name="possible-root-cause"></a><span data-ttu-id="ec0ec-263">Cause principale possible</span><span class="sxs-lookup"><span data-stu-id="ec0ec-263">Possible root cause</span></span>   

  * <span data-ttu-id="ec0ec-264">port d’écoute Tomcat Hello n’est pas hello identique au port privé de hello du point de terminaison de votre machine virtuelle pour le trafic de Tomcat.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-264">hello Tomcat listen port is not hello same as hello private port of your virtual machine's endpoint for Tomcat traffic.</span></span>  

     <span data-ttu-id="ec0ec-265">Vérifiez votre port public et la privée des paramètres de point de terminaison de port, assurez-vous que le port privé de hello est hello identique hello Tomcat port d’écoute.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-265">Check your public port and private port endpoint settings and make sure hello private port is hello same as hello Tomcat listen port.</span></span> <span data-ttu-id="ec0ec-266">Consultez la section « Phase 1 : Création d’une image » de cet article pour obtenir des instructions sur la configuration des points de terminaison pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-266">See "Phase 1: Create an image" section of this article for instructions on configuring endpoints for your virtual machine.</span></span>  

     <span data-ttu-id="ec0ec-267">toodetermine hello Tomcat port d’écoute, ouvrez /etc/httpd/conf/httpd.conf (version Red Hat) ou /etc/tomcat7/server.xml (version Debian).</span><span class="sxs-lookup"><span data-stu-id="ec0ec-267">toodetermine hello Tomcat listen port, open /etc/httpd/conf/httpd.conf (Red Hat release), or /etc/tomcat7/server.xml (Debian release).</span></span> <span data-ttu-id="ec0ec-268">Par défaut, hello port d’écoute de Tomcat est 8080.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-268">By default, hello Tomcat listen port is 8080.</span></span> <span data-ttu-id="ec0ec-269">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-269">Here is an example:</span></span>  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     <span data-ttu-id="ec0ec-270">Si vous utilisez un ordinateur virtuel comme Debian ou Ubuntu et que vous souhaitez toochange hello par défaut port de Tomcat écouter (par exemple 8081), vous devez également ouvrir le port hello hello système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-270">If you are using a virtual machine like Debian or Ubuntu and you want toochange hello default port of Tomcat Listen (for example 8081), you should also open hello port for hello operating system.</span></span> <span data-ttu-id="ec0ec-271">Tout d’abord, ouvrez le profil de hello :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-271">First, open hello profile:</span></span>  

        sudo vi /etc/default/tomcat7  

     <span data-ttu-id="ec0ec-272">Puis supprimez les commentaires de la dernière ligne de hello et modifiez « non » trop « Oui ».</span><span class="sxs-lookup"><span data-stu-id="ec0ec-272">Then uncomment hello last line and change “no” too“yes”.</span></span>  

        AUTHBIND=yes
  2. <span data-ttu-id="ec0ec-273">les pare-feu Hello a désactivé hello port d’écoute de Tomcat.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-273">hello firewall has disabled hello listen port of Tomcat.</span></span>

     <span data-ttu-id="ec0ec-274">Vous pouvez page ne s’affiche hello Tomcat par défaut à partir de l’hôte local de hello.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-274">You can only see hello Tomcat default page from hello local host.</span></span> <span data-ttu-id="ec0ec-275">problème de Hello est très probable que le port hello, qui est la bonne tooby Tomcat, est bloqué par le pare-feu hello.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-275">hello problem is most likely that hello port, which is listened tooby Tomcat, is blocked by hello firewall.</span></span> <span data-ttu-id="ec0ec-276">Vous pouvez utiliser la page Web de hello w3m outil toobrowse hello.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-276">You can use hello w3m tool toobrowse hello webpage.</span></span> <span data-ttu-id="ec0ec-277">Hello commandes suivantes installer w3m et parcourir la page par défaut de Tomcat toohello :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-277">hello following commands install w3m and browse toohello Tomcat default page:</span></span>  


        <span data-ttu-id="ec0ec-278">sudo yum  install w3m w3m-img</span><span class="sxs-lookup"><span data-stu-id="ec0ec-278">sudo yum  install w3m w3m-img</span></span>


        <span data-ttu-id="ec0ec-279">w3m http://localhost:8080</span><span class="sxs-lookup"><span data-stu-id="ec0ec-279">w3m http://localhost:8080</span></span>  
#### <a name="solution"></a><span data-ttu-id="ec0ec-280">Solution</span><span class="sxs-lookup"><span data-stu-id="ec0ec-280">Solution</span></span>

  * <span data-ttu-id="ec0ec-281">Si hello port d’écoute de Tomcat est même hello pas en tant que port privé de hello du point de terminaison hello pour la machine virtuelle de toohello le trafic, vous devez modifier un port privé hello toobe hello identique hello du port d’écoute de Tomcat.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-281">If hello Tomcat listen port is not hello same as hello private port of hello endpoint for traffic toohello virtual machine, you need change hello private port toobe hello same as hello Tomcat listen port.</span></span>   
  2. <span data-ttu-id="ec0ec-282">Si le problème de hello est provoqué par un pare-feu/iptables, ajoutez hello suivant lignes trop/etc/sysconfig/iptables.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-282">If hello issue is caused by firewall/iptables, add hello following lines too/etc/sysconfig/iptables.</span></span> <span data-ttu-id="ec0ec-283">deuxième ligne de Hello est nécessaire uniquement pour le trafic https :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-283">hello second line is only needed for https traffic:</span></span>  

      <span data-ttu-id="ec0ec-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="ec0ec-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span></span>

      <span data-ttu-id="ec0ec-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="ec0ec-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span></span>  

     > [!IMPORTANT]
     > <span data-ttu-id="ec0ec-286">Assurez-vous que les lignes précédentes hello sont positionnées au-dessus de toutes les lignes qui seraient globalement restreindre l’accès, telles que les éléments suivants de hello : - A -j rejeter--rejeter avec icmp-hôte-interdit d’entrée</span><span class="sxs-lookup"><span data-stu-id="ec0ec-286">Make sure hello previous lines are positioned above any lines that would globally restrict access, such as hello following: -A INPUT -j REJECT --reject-with icmp-host-prohibited</span></span>



<span data-ttu-id="ec0ec-287">tooreload hello iptables, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-287">tooreload hello iptables, run hello following command:</span></span>

    service iptables restart

<span data-ttu-id="ec0ec-288">Cela a été testé sur CentOS 6.3.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-288">This has been tested on CentOS 6.3.</span></span>

### <a name="permission-denied-when-you-upload-project-files-toovarlibtomcat7webapps"></a><span data-ttu-id="ec0ec-289">Autorisation refusée lorsque vous téléchargez le projet fichiers trop/var/lib/tomcat7/WebApp /</span><span class="sxs-lookup"><span data-stu-id="ec0ec-289">Permission denied when you upload project files too/var/lib/tomcat7/webapps/</span></span>
#### <a name="symptom"></a><span data-ttu-id="ec0ec-290">Symptôme</span><span class="sxs-lookup"><span data-stu-id="ec0ec-290">Symptom</span></span>
  <span data-ttu-id="ec0ec-291">Lorsque vous utilisez un ordinateur virtuel SFTP client (par exemple, FileZilla) tooconnect tooyour et accédez trop/var/lib/tomcat7/WebApp/toopublish votre site, vous obtenez un suivant de toohello erreur message similaire :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-291">When you use an SFTP client (such as FileZilla) tooconnect tooyour virtual machine and navigate too/var/lib/tomcat7/webapps/ toopublish your site, you get an error message similar toohello following:</span></span>  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a><span data-ttu-id="ec0ec-292">Cause principale possible</span><span class="sxs-lookup"><span data-stu-id="ec0ec-292">Possible root cause</span></span>
  <span data-ttu-id="ec0ec-293">Vous ne disposez d’aucun dossier de /var/lib/tomcat7/webapps autorisations tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-293">You have no permissions tooaccess hello /var/lib/tomcat7/webapps folder.</span></span>  
#### <a name="solution"></a><span data-ttu-id="ec0ec-294">Solution</span><span class="sxs-lookup"><span data-stu-id="ec0ec-294">Solution</span></span>  
  <span data-ttu-id="ec0ec-295">Vous devez avoir l’autorisation de tooget à partir du compte root hello.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-295">You need tooget permission from hello root account.</span></span> <span data-ttu-id="ec0ec-296">Vous pouvez modifier la propriété de hello de ce dossier à partir du nom d’utilisateur du toohello racine que vous avez utilisé lorsque vous avez configuré l’ordinateur de hello.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-296">You can change hello ownership of that folder from root toohello username you used when you provisioned hello machine.</span></span> <span data-ttu-id="ec0ec-297">Voici un exemple avec le nom du compte azureuser hello :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-297">Here is an example with hello azureuser account name:</span></span>  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  <span data-ttu-id="ec0ec-298">Utiliser des autorisations hello tooapply hello -R option pour tous les fichiers à l’intérieur d’un répertoire.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-298">Use hello -R option tooapply hello permissions for all files inside of a directory too.</span></span>  

  <span data-ttu-id="ec0ec-299">Cette commande fonctionne également pour les répertoires.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-299">This command also works for directories.</span></span> <span data-ttu-id="ec0ec-300">modifications de l’option -R Hello hello des autorisations pour tous les fichiers et répertoires à l’intérieur du répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-300">hello -R option changes hello permissions for all files and directories inside hello directory.</span></span> <span data-ttu-id="ec0ec-301">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="ec0ec-301">Here is an example:</span></span>  

     sudo chown -R username:group directory  

  <span data-ttu-id="ec0ec-302">Cette commande modifie la propriété (utilisateur et groupe) pour tous les fichiers et répertoires à l’intérieur des hello active.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-302">This command changes ownership (both user and group) for all files and directories that are inside hello directory.</span></span>  

  <span data-ttu-id="ec0ec-303">Hello commande suivante modifie uniquement autorisation hello du répertoire du dossier hello.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-303">hello following command only changes hello permission of hello folder directory.</span></span> <span data-ttu-id="ec0ec-304">les fichiers Hello et dossiers contenus dans le répertoire de hello ne sont pas modifiés.</span><span class="sxs-lookup"><span data-stu-id="ec0ec-304">hello files and folders inside hello directory are not changed.</span></span>  

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
