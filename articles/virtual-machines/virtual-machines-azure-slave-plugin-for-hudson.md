---
title: "aaaHow toouse hello Azure esclave plug-in avec une intégration continue Hudson | Documents Microsoft"
description: "Décrit comment toouse hello Azure esclave plug-in avec une intégration continue Hudson."
services: virtual-machines-linux
documentationcenter: 
author: rmcmurray
manager: wpickett
editor: 
ms.assetid: b2083d1c-4de8-4a19-a615-ccc9d9b6e1d9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cd6e67ad71c208aa56746aa8b70ba507da20bee9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-slave-plug-in-with-hudson-continuous-integration"></a><span data-ttu-id="017be-103">Comment toouse hello Azure esclave plug-in avec une intégration continue Hudson</span><span class="sxs-lookup"><span data-stu-id="017be-103">How toouse hello Azure slave plug-in with Hudson Continuous Integration</span></span>
<span data-ttu-id="017be-104">Hello Azure esclave Hudson plug-in vous permet de nœuds d’esclave tooprovision sur Azure lorsque les builds en cours d’exécution distribuée.</span><span class="sxs-lookup"><span data-stu-id="017be-104">hello Azure slave plug-in for Hudson enables you tooprovision slave nodes on Azure when running distributed builds.</span></span>

## <a name="install-hello-azure-slave-plug-in"></a><span data-ttu-id="017be-105">Installer hello esclave Azure plug-in</span><span class="sxs-lookup"><span data-stu-id="017be-105">Install hello Azure Slave plug-in</span></span>
1. <span data-ttu-id="017be-106">Dans le tableau de bord Hudson de hello, cliquez sur **gérer les Hudson**.</span><span class="sxs-lookup"><span data-stu-id="017be-106">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="017be-107">Bonjour **gérer les Hudson** page, cliquez sur **gérer les plug-ins**.</span><span class="sxs-lookup"><span data-stu-id="017be-107">In hello **Manage Hudson** page, click on **Manage Plugins**.</span></span>
3. <span data-ttu-id="017be-108">Cliquez sur hello **disponible** onglet.</span><span class="sxs-lookup"><span data-stu-id="017be-108">Click hello **Available** tab.</span></span>
4. <span data-ttu-id="017be-109">Cliquez sur **recherche** et type **Azure** toolimit hello liste toorelevant plug-ins.</span><span class="sxs-lookup"><span data-stu-id="017be-109">Click **Search** and type **Azure** toolimit hello list toorelevant plug-ins.</span></span>
   
    <span data-ttu-id="017be-110">Si vous choisissez tooscroll liste hello de plug-ins disponibles, vous trouverez hello esclave Azure plug-in sous hello **gestion du Cluster et distribués générer** section Bonjour **d’autres** onglet.</span><span class="sxs-lookup"><span data-stu-id="017be-110">If you opt tooscroll through hello list of available plug-ins, you will find hello Azure slave plug-in under hello **Cluster Management and Distributed Build** section in hello **Others** tab.</span></span>
5. <span data-ttu-id="017be-111">Sélectionnez la case à cocher hello **plug-in de Azure esclave**.</span><span class="sxs-lookup"><span data-stu-id="017be-111">Select hello checkbox for **Azure Slave Plugin**.</span></span>
6. <span data-ttu-id="017be-112">Cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="017be-112">Click **Install**.</span></span>
7. <span data-ttu-id="017be-113">Redémarrez Hudson.</span><span class="sxs-lookup"><span data-stu-id="017be-113">Restart Hudson.</span></span>

<span data-ttu-id="017be-114">Maintenant que hello plug-in est installé, les étapes suivantes hello serait hello tooconfigure plug-in avec votre toocreate un modèle qui sera utilisé pour la création d’hello machine virtuelle pour le noeud esclave hello et un profil de l’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="017be-114">Now that hello plug-in is installed, hello next steps would be tooconfigure hello plug-in with your Azure subscription profile and toocreate a template that will be used in creating hello VM for hello slave node.</span></span>

## <a name="configure-hello-azure-slave-plug-in-with-your-subscription-profile"></a><span data-ttu-id="017be-115">Configurer hello esclave Azure plug-in avec le profil de votre abonnement</span><span class="sxs-lookup"><span data-stu-id="017be-115">Configure hello Azure Slave plug-in with your subscription profile</span></span>
<span data-ttu-id="017be-116">Un profil d’abonnement, également désignées tooas paramètres de publication, est un fichier XML qui contient les informations d’identification sécurisées ainsi que certaines informations supplémentaires, vous aurez besoin de toowork avec Azure dans votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="017be-116">A subscription profile, also referred tooas publish settings, is an XML file that contains secure credentials and some additional information you'll need toowork with Azure in your development environment.</span></span> <span data-ttu-id="017be-117">tooconfigure hello Azure esclave plug-in, vous devez :</span><span class="sxs-lookup"><span data-stu-id="017be-117">tooconfigure hello Azure slave plug-in, you need:</span></span>

* <span data-ttu-id="017be-118">Votre ID d’abonnement</span><span class="sxs-lookup"><span data-stu-id="017be-118">Your subscription id</span></span>
* <span data-ttu-id="017be-119">Un certificat de gestion pour votre abonnement</span><span class="sxs-lookup"><span data-stu-id="017be-119">A management certificate for your subscription</span></span>

<span data-ttu-id="017be-120">Vous les trouverez dans votre [profil d’abonnement].</span><span class="sxs-lookup"><span data-stu-id="017be-120">These can be found in your [subscription profile].</span></span> <span data-ttu-id="017be-121">Vous trouverez ci-dessous un exemple de profil d'abonnement.</span><span class="sxs-lookup"><span data-stu-id="017be-121">Below is an example of a subscription profile.</span></span>

    <?xml version="1.0" encoding="utf-8"?>

        <PublishData>

          <PublishProfile SchemaVersion="2.0" PublishMethod="AzureServiceManagementAPI">

        <Subscription

              ServiceManagementUrl="https://management.core.windows.net"

              Id="<Subscription ID>"

              Name="Pay-As-You-Go"
            ManagementCertificate="<Management certificate value>" />

          </PublishProfile>

    </PublishData>

<span data-ttu-id="017be-122">Une fois que vous avez votre profil d’abonnement, suivez ces hello de tooconfigure étapes subordonnées Azure plug-in.</span><span class="sxs-lookup"><span data-stu-id="017be-122">Once you have your subscription profile, follow these steps tooconfigure hello Azure slave plug-in.</span></span>

1. <span data-ttu-id="017be-123">Dans le tableau de bord Hudson de hello, cliquez sur **gérer les Hudson**.</span><span class="sxs-lookup"><span data-stu-id="017be-123">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="017be-124">Cliquez sur **Configure System**(Configurer le système).</span><span class="sxs-lookup"><span data-stu-id="017be-124">Click **Configure System**.</span></span>
3. <span data-ttu-id="017be-125">Défiler hello de hello page toofind **Cloud** section.</span><span class="sxs-lookup"><span data-stu-id="017be-125">Scroll down hello page toofind hello **Cloud** section.</span></span>
4. <span data-ttu-id="017be-126">Cliquez sur **Add new cloud > Microsoft Azure** (Ajouter un nouveau cloud > Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="017be-126">Click **Add new cloud > Microsoft Azure**.</span></span>
   
    ![ajouter un cloud][add new cloud]
   
    <span data-ttu-id="017be-128">Cette opération affiche les champs hello où vous avez besoin de tooenter détails de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="017be-128">This will show hello fields where you need tooenter your subscription details.</span></span>
   
    ![configurer le profil][configure profile]
5. <span data-ttu-id="017be-130">Copiez le certificat de gestion et l’id d’abonnement hello à partir de votre profil d’abonnement et les coller dans les champs appropriés hello.</span><span class="sxs-lookup"><span data-stu-id="017be-130">Copy hello subscription id and management certificate from your subscription profile and paste them in hello appropriate fields.</span></span>
   
    <span data-ttu-id="017be-131">Lors de la copie du certificat gestion et l’id d’abonnement hello, **pas** inclure les guillemets hello qui entourent les valeurs hello.</span><span class="sxs-lookup"><span data-stu-id="017be-131">When copying hello subscription id and management certificate, **do not** include hello quotes that enclose hello values.</span></span>
6. <span data-ttu-id="017be-132">Cliquez sur **Verify configuration**(Vérifier la configuration).</span><span class="sxs-lookup"><span data-stu-id="017be-132">Click on **Verify configuration**.</span></span>
7. <span data-ttu-id="017be-133">Lors de la configuration de hello est vérifiée avec succès, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="017be-133">When hello configuration is verified successfully, click **Save**.</span></span>

## <a name="set-up-a-virtual-machine-template-for-hello-azure-slave-plug-in"></a><span data-ttu-id="017be-134">Définir un modèle d’ordinateur virtuel pour hello Azure esclave plug-in</span><span class="sxs-lookup"><span data-stu-id="017be-134">Set up a virtual machine template for hello Azure Slave plug-in</span></span>
<span data-ttu-id="017be-135">Un modèle d’ordinateur virtuel définit les paramètres de hello hello plug-in utilise toocreate un nœud subordonné sur Azure.</span><span class="sxs-lookup"><span data-stu-id="017be-135">A virtual machine template defines hello parameters hello plug-in will use toocreate a slave node on Azure.</span></span> <span data-ttu-id="017be-136">Bonjour suit nous allons créer le modèle pour un VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="017be-136">In hello following steps we'll be creating template for an Ubuntu VM.</span></span>

1. <span data-ttu-id="017be-137">Dans le tableau de bord Hudson de hello, cliquez sur **gérer les Hudson**.</span><span class="sxs-lookup"><span data-stu-id="017be-137">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="017be-138">Cliquez sur **Configure System**(Configurer le système).</span><span class="sxs-lookup"><span data-stu-id="017be-138">Click on **Configure System**.</span></span>
3. <span data-ttu-id="017be-139">Défiler hello de hello page toofind **Cloud** section.</span><span class="sxs-lookup"><span data-stu-id="017be-139">Scroll down hello page toofind hello **Cloud** section.</span></span>
4. <span data-ttu-id="017be-140">Au sein de hello **Cloud** section, recherchez **ajouter un modèle de Machine virtuelle Azure** et cliquez sur hello **ajouter** bouton.</span><span class="sxs-lookup"><span data-stu-id="017be-140">Within hello **Cloud** section, find **Add Azure Virtual Machine Template** and click hello **Add** button.</span></span>
   
    ![ajouter un modèle d'ordinateur virtuel][add vm template]
5. <span data-ttu-id="017be-142">Spécifiez un nom de service cloud dans hello **nom** champ.</span><span class="sxs-lookup"><span data-stu-id="017be-142">Specify a cloud service name in hello **Name** field.</span></span> <span data-ttu-id="017be-143">Si nom hello que vous spécifiez fait référence tooan existant du service cloud, hello machine virtuelle est approvisionné dans ce service.</span><span class="sxs-lookup"><span data-stu-id="017be-143">If hello name you specify refers tooan existing cloud service, hello VM will be provisioned in that service.</span></span> <span data-ttu-id="017be-144">Dans le cas contraire, Azure en crée un nouveau.</span><span class="sxs-lookup"><span data-stu-id="017be-144">Otherwise, Azure will create a new one.</span></span>
6. <span data-ttu-id="017be-145">Bonjour **Description** , entrez le texte qui décrit le modèle hello que vous créez.</span><span class="sxs-lookup"><span data-stu-id="017be-145">In hello **Description** field, enter text that describes hello template you are creating.</span></span> <span data-ttu-id="017be-146">Ces informations sont uniquement à des fins documentaires et ne sont pas utilisées dans la mise en service d'un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="017be-146">This information is only for documentary purposes and is not used in provisioning a VM.</span></span>
7. <span data-ttu-id="017be-147">Bonjour **étiquettes** , entrez **linux**.</span><span class="sxs-lookup"><span data-stu-id="017be-147">In hello **Labels** field, enter **linux**.</span></span> <span data-ttu-id="017be-148">Cette étiquette est modèle hello tooidentify utilisé que vous créez et modèle de hello tooreference utilisé par la suite lors de la création d’un travail Hudson.</span><span class="sxs-lookup"><span data-stu-id="017be-148">This label is used tooidentify hello template you are creating and is subsequently used tooreference hello template when creating a Hudson job.</span></span>
8. <span data-ttu-id="017be-149">Sélectionnez une région où hello machine virtuelle doit être créé.</span><span class="sxs-lookup"><span data-stu-id="017be-149">Select a region where hello VM will be created.</span></span>
9. <span data-ttu-id="017be-150">Sélectionnez la taille de machine virtuelle appropriée hello.</span><span class="sxs-lookup"><span data-stu-id="017be-150">Select hello appropriate VM size.</span></span>
10. <span data-ttu-id="017be-151">Spécifiez un compte de stockage où hello machine virtuelle doit être créé.</span><span class="sxs-lookup"><span data-stu-id="017be-151">Specify a storage account where hello VM will be created.</span></span> <span data-ttu-id="017be-152">Assurez-vous qu’il s’agit de hello même région que le service de cloud computing hello vous allez utiliser.</span><span class="sxs-lookup"><span data-stu-id="017be-152">Make sure that it is in hello same region as hello cloud service you'll be using.</span></span> <span data-ttu-id="017be-153">Si vous souhaitez que le nouveau stockage toobe créé, vous pouvez laisser ce champ vide.</span><span class="sxs-lookup"><span data-stu-id="017be-153">If you want new storage toobe created, you can leave this field blank.</span></span>
11. <span data-ttu-id="017be-154">Durée de rétention spécifie le nombre hello de minutes avant la suppression d’une inactivité esclave Hudson.</span><span class="sxs-lookup"><span data-stu-id="017be-154">Retention time specifies hello number of minutes before Hudson deletes an idle slave.</span></span> <span data-ttu-id="017be-155">Laissez cette valeur par défaut 60 hello.</span><span class="sxs-lookup"><span data-stu-id="017be-155">Leave this at hello default value of 60.</span></span>
12. <span data-ttu-id="017be-156">Dans **utilisation**, sélectionnez hello condition appropriée lorsque ce nœud subordonné sera utilisé.</span><span class="sxs-lookup"><span data-stu-id="017be-156">In **Usage**, select hello appropriate condition when this slave node will be used.</span></span> <span data-ttu-id="017be-157">Pour l'instant, sélectionnez **Utilize this node as much as possible**(Utiliser ce nœud autant que possible).</span><span class="sxs-lookup"><span data-stu-id="017be-157">For now, select **Utilize this node as much as possible**.</span></span>
    
     <span data-ttu-id="017be-158">À ce stade, votre écran ressemble toothis quelque peu similaires :</span><span class="sxs-lookup"><span data-stu-id="017be-158">At this point, your form would look somewhat similar toothis:</span></span>
    
     ![configuration du modèle][template config]
13. <span data-ttu-id="017be-160">Dans **Id de famille de l’Image ou de** vous avez toospecify quelle image système sera installé sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="017be-160">In **Image Family or Id** you have toospecify what system image will be installed on your VM.</span></span> <span data-ttu-id="017be-161">Vous pouvez faire votre choix dans une liste de familles d'images ou spécifier une image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="017be-161">You can either select from a list of image families or specify a custom image.</span></span>
    
     <span data-ttu-id="017be-162">Si vous souhaitez tooselect dans la liste des familles de l’image, entrez hello premier caractère (respecte la casse) du nom de famille d’image hello.</span><span class="sxs-lookup"><span data-stu-id="017be-162">If you want tooselect from a list of image families, enter hello first character (case-sensitive) of hello image family name.</span></span> <span data-ttu-id="017be-163">Par exemple, le fait de taper **U** affichera une liste des familles de serveurs Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="017be-163">For instance, typing **U** will bring up a list of Ubuntu Server families.</span></span> <span data-ttu-id="017be-164">Une fois que vous sélectionnez dans la liste de hello, Jenkins utilisera version la plus récente de cette image du système à partir de cette famille hello lors de la configuration de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="017be-164">Once you select from hello list, Jenkins will use hello latest version of that system image from that family when provisioning your VM.</span></span>
    
     ![liste de famille de système d'exploitation][OS family list]
    
     <span data-ttu-id="017be-166">Si vous disposez d’une image personnalisée que vous souhaitez toouse au lieu de cela, entrez le nom hello de cette image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="017be-166">If you have a custom image that you want toouse instead, enter hello name of that custom image.</span></span> <span data-ttu-id="017be-167">Noms d’images personnalisées ne figurent pas dans une liste afin que vous ayez tooensure qui hello nom a été saisi correctement.</span><span class="sxs-lookup"><span data-stu-id="017be-167">Custom image names are not shown in a list so you have tooensure that hello name is entered correctly.</span></span>    
    
     <span data-ttu-id="017be-168">Pour ce didacticiel, tapez **U** toobring la liste des images d’Ubuntu et sélectionnez **Ubuntu Server 14.04 LTS**.</span><span class="sxs-lookup"><span data-stu-id="017be-168">For this tutorial, type **U** toobring up a list of Ubuntu images and select **Ubuntu Server 14.04 LTS**.</span></span>
14. <span data-ttu-id="017be-169">Pour la **méthode de lancement**, sélectionnez **SSH**.</span><span class="sxs-lookup"><span data-stu-id="017be-169">For **Launch method**, select **SSH**.</span></span>
15. <span data-ttu-id="017be-170">Copiez le script ci-dessous hello et collez Bonjour **script d’initialisation** champ.</span><span class="sxs-lookup"><span data-stu-id="017be-170">Copy hello script below and paste in hello **Init script** field.</span></span>
    
         # Install Java
    
         sudo apt-get -y update
    
         sudo apt-get install -y openjdk-7-jdk
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y openjdk-7-jdk
    
         # Install git
    
         sudo apt-get install -y git
    
         #Install ant
    
         sudo apt-get install -y ant
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y ant
    
     <span data-ttu-id="017be-171">Hello **script d’initialisation** sera exécuté après hello machine virtuelle est créée.</span><span class="sxs-lookup"><span data-stu-id="017be-171">hello **Init script** will be executed after hello VM is created.</span></span> <span data-ttu-id="017be-172">Dans cet exemple, le script de hello installe Java, git et ant.</span><span class="sxs-lookup"><span data-stu-id="017be-172">In this example, hello script installs Java, git, and ant.</span></span>
16. <span data-ttu-id="017be-173">Bonjour **nom d’utilisateur** et **mot de passe** , saisissez les valeurs par défaut pour le compte d’administrateur hello qui sera créé sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="017be-173">In hello **Username** and **Password** fields, enter your preferred values for hello administrator account that will be created on your VM.</span></span>
17. <span data-ttu-id="017be-174">Cliquez sur **vérifier le modèle** toocheck si paramètres hello spécifiés sont valides.</span><span class="sxs-lookup"><span data-stu-id="017be-174">Click on **Verify Template** toocheck if hello parameters you specified are valid.</span></span>
18. <span data-ttu-id="017be-175">Cliquez sur **Save**(Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="017be-175">Click on **Save**.</span></span>

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a><span data-ttu-id="017be-176">Créer un travail Hudson qui s'exécute sur un nœud subordonné sur Azure</span><span class="sxs-lookup"><span data-stu-id="017be-176">Create a Hudson job that runs on a slave node on Azure</span></span>
<span data-ttu-id="017be-177">Dans cette section, vous allez créer un travail Hudson qui s'exécutera sur un nœud subordonné sur Azure.</span><span class="sxs-lookup"><span data-stu-id="017be-177">In this section, you'll be creating a Hudson task that will run on a slave node on Azure.</span></span>

1. <span data-ttu-id="017be-178">Dans le tableau de bord Hudson de hello, cliquez sur **nouveau travail**.</span><span class="sxs-lookup"><span data-stu-id="017be-178">In hello Hudson dashboard, click **New Job**.</span></span>
2. <span data-ttu-id="017be-179">Entrez un nom pour la tâche hello que vous créez.</span><span class="sxs-lookup"><span data-stu-id="017be-179">Enter a name for hello job you are creating.</span></span>
3. <span data-ttu-id="017be-180">Pour le type de tâche hello, sélectionnez **créer un travail de style libre logiciel**.</span><span class="sxs-lookup"><span data-stu-id="017be-180">For hello job type, select **Build a free-style software job**.</span></span>
4. <span data-ttu-id="017be-181">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="017be-181">Click **OK**.</span></span>
5. <span data-ttu-id="017be-182">Dans la page de configuration du travail hello, sélectionnez **Restrict où ce projet peut être exécuté**.</span><span class="sxs-lookup"><span data-stu-id="017be-182">In hello job configuration page, select **Restrict where this project can be run**.</span></span>
6. <span data-ttu-id="017be-183">Sélectionnez **nœud et étiquette de menu** et sélectionnez **linux** (que nous avons spécifié cette étiquette lors de la création du modèle d’ordinateur virtuel hello dans la section précédente de hello).</span><span class="sxs-lookup"><span data-stu-id="017be-183">Select **Node and label menu** and select **linux** (we specified this label when creating hello virtual machine template in hello previous section).</span></span>
7. <span data-ttu-id="017be-184">Bonjour **générer** , cliquez sur **étape de génération ajouter** et sélectionnez **exécuter shell**.</span><span class="sxs-lookup"><span data-stu-id="017be-184">In hello **Build** section, click **Add build step** and select **Execute shell**.</span></span>
8. <span data-ttu-id="017be-185">Modifier hello script suivant, en remplaçant **{nom de votre compte github}**, **{nom de votre projet}**, et **{votre répertoire de projet}** avec les valeurs appropriées et collez hello modifier le script dans la zone de texte hello qui s’affiche.</span><span class="sxs-lookup"><span data-stu-id="017be-185">Edit hello following script, replacing **{your github account name}**, **{your project name}**, and **{your project directory}** with appropriate values, and paste hello edited script in hello text area that appears.</span></span>
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory tooproject
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. <span data-ttu-id="017be-186">Cliquez sur **Save**(Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="017be-186">Click on **Save**.</span></span>
10. <span data-ttu-id="017be-187">Hello du tableau de bord Hudson, recherchez les tâches hello vous venez de créer et cliquez sur hello **planifier une build** icône.</span><span class="sxs-lookup"><span data-stu-id="017be-187">In hello Hudson dashboard, find hello job you just created and click on hello **Schedule a build** icon.</span></span>

<span data-ttu-id="017be-188">Hudson ensuite créer un nœud subordonné à l’aide du modèle de hello créé dans la section précédente de hello et exécuter le script hello spécifié à l’étape de génération hello pour cette tâche.</span><span class="sxs-lookup"><span data-stu-id="017be-188">Hudson will then create a slave node using hello template created in hello previous section and execute hello script you specified in hello build step for this task.</span></span>

## <a name="next-steps"></a><span data-ttu-id="017be-189">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="017be-189">Next Steps</span></span>
<span data-ttu-id="017be-190">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure].</span><span class="sxs-lookup"><span data-stu-id="017be-190">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<!-- URL List -->

[centre de développement Java Azure]: https://azure.microsoft.com/develop/java/
[profil d’abonnement]: http://go.microsoft.com/fwlink/?LinkID=396395

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

