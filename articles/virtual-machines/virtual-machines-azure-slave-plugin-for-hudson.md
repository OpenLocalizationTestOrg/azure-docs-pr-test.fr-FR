---
title: "Utilisation du plug-in subordonné Azure avec la solution d’intégration continue Hudson | Microsoft Docs"
description: "Décrit l’utilisation du plug-in subordonné Azure avec la solution d'intégration continue Hudson"
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
ms.openlocfilehash: c11b59f8ea432075b147a391de4b7bd3331e639e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-azure-slave-plug-in-with-hudson-continuous-integration"></a><span data-ttu-id="52944-103">Utilisation du plug-in subordonné Azure avec la solution d'intégration continue Hudson</span><span class="sxs-lookup"><span data-stu-id="52944-103">How to use the Azure slave plug-in with Hudson Continuous Integration</span></span>
<span data-ttu-id="52944-104">Le plug-in subordonné Azure pour Hudson vous permet d’approvisionner des nœuds subordonnés sur Azure lors de l'exécution de builds distribués.</span><span class="sxs-lookup"><span data-stu-id="52944-104">The Azure slave plug-in for Hudson enables you to provision slave nodes on Azure when running distributed builds.</span></span>

## <a name="install-the-azure-slave-plug-in"></a><span data-ttu-id="52944-105">Installation du plug-in subordonné Azure</span><span class="sxs-lookup"><span data-stu-id="52944-105">Install the Azure Slave plug-in</span></span>
1. <span data-ttu-id="52944-106">Dans le tableau de bord Hudson, cliquez sur **Manage Hudson**(Gérer Hudson).</span><span class="sxs-lookup"><span data-stu-id="52944-106">In the Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="52944-107">Sur la page **Manage Hudson** (Gérer Hudson), cliquez sur **Manage Plugins** (Gérer les plug-ins).</span><span class="sxs-lookup"><span data-stu-id="52944-107">In the **Manage Hudson** page, click on **Manage Plugins**.</span></span>
3. <span data-ttu-id="52944-108">Cliquez sur l'onglet **Available** .</span><span class="sxs-lookup"><span data-stu-id="52944-108">Click the **Available** tab.</span></span>
4. <span data-ttu-id="52944-109">Cliquez sur **Search** (Rechercher) et tapez **Azure** pour limiter la liste aux plug-ins appropriés.</span><span class="sxs-lookup"><span data-stu-id="52944-109">Click **Search** and type **Azure** to limit the list to relevant plug-ins.</span></span>
   
    <span data-ttu-id="52944-110">Si vous choisissez de faire défiler la liste des plug-ins disponibles, vous trouverez le plug-in subordonné Azure sous la section **Cluster Management and Distributed Build** (Gestion du cluster et build distribué) dans l’onglet **Others** (Autres).</span><span class="sxs-lookup"><span data-stu-id="52944-110">If you opt to scroll through the list of available plug-ins, you will find the Azure slave plug-in under the **Cluster Management and Distributed Build** section in the **Others** tab.</span></span>
5. <span data-ttu-id="52944-111">Cochez la case **Azure Slave Plugin**(Plug-in esclave Azure).</span><span class="sxs-lookup"><span data-stu-id="52944-111">Select the checkbox for **Azure Slave Plugin**.</span></span>
6. <span data-ttu-id="52944-112">Cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="52944-112">Click **Install**.</span></span>
7. <span data-ttu-id="52944-113">Redémarrez Hudson.</span><span class="sxs-lookup"><span data-stu-id="52944-113">Restart Hudson.</span></span>

<span data-ttu-id="52944-114">Maintenant que le plug-in est installé, les étapes suivantes consistent à le configurer avec votre profil d'abonnement Azure et à créer un modèle qui sera utilisé lors de la création de la machine virtuelle pour le nœud subordonné.</span><span class="sxs-lookup"><span data-stu-id="52944-114">Now that the plug-in is installed, the next steps would be to configure the plug-in with your Azure subscription profile and to create a template that will be used in creating the VM for the slave node.</span></span>

## <a name="configure-the-azure-slave-plug-in-with-your-subscription-profile"></a><span data-ttu-id="52944-115">Configuration du plug-in subordonné Azure avec votre profil d’abonnement</span><span class="sxs-lookup"><span data-stu-id="52944-115">Configure the Azure Slave plug-in with your subscription profile</span></span>
<span data-ttu-id="52944-116">Un profil d'abonnement, également appelé paramètres de publication, est un fichier XML qui contient des informations d'identification sécurisées, ainsi que des informations supplémentaires, dont vous aurez besoin pour utiliser Azure dans votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="52944-116">A subscription profile, also referred to as publish settings, is an XML file that contains secure credentials and some additional information you'll need to work with Azure in your development environment.</span></span> <span data-ttu-id="52944-117">Pour configurer le plug-in subordonné Azure, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="52944-117">To configure the Azure slave plug-in, you need:</span></span>

* <span data-ttu-id="52944-118">Votre ID d’abonnement</span><span class="sxs-lookup"><span data-stu-id="52944-118">Your subscription id</span></span>
* <span data-ttu-id="52944-119">Un certificat de gestion pour votre abonnement</span><span class="sxs-lookup"><span data-stu-id="52944-119">A management certificate for your subscription</span></span>

<span data-ttu-id="52944-120">Vous les trouverez dans votre [profil d’abonnement].</span><span class="sxs-lookup"><span data-stu-id="52944-120">These can be found in your [subscription profile].</span></span> <span data-ttu-id="52944-121">Vous trouverez ci-dessous un exemple de profil d'abonnement.</span><span class="sxs-lookup"><span data-stu-id="52944-121">Below is an example of a subscription profile.</span></span>

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

<span data-ttu-id="52944-122">Une fois que vous avez votre profil d'abonnement, procédez comme suit pour configurer le plug-in subordonné Azure.</span><span class="sxs-lookup"><span data-stu-id="52944-122">Once you have your subscription profile, follow these steps to configure the Azure slave plug-in.</span></span>

1. <span data-ttu-id="52944-123">Dans le tableau de bord Hudson, cliquez sur **Manage Hudson**(Gérer Hudson).</span><span class="sxs-lookup"><span data-stu-id="52944-123">In the Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="52944-124">Cliquez sur **Configure System**(Configurer le système).</span><span class="sxs-lookup"><span data-stu-id="52944-124">Click **Configure System**.</span></span>
3. <span data-ttu-id="52944-125">Faites défiler la page vers le bas pour trouver la section **Cloud** .</span><span class="sxs-lookup"><span data-stu-id="52944-125">Scroll down the page to find the **Cloud** section.</span></span>
4. <span data-ttu-id="52944-126">Cliquez sur **Add new cloud > Microsoft Azure** (Ajouter un nouveau cloud > Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="52944-126">Click **Add new cloud > Microsoft Azure**.</span></span>
   
    ![ajouter un cloud][add new cloud]
   
    <span data-ttu-id="52944-128">Cette commande affiche les champs où vous devez entrer les détails de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="52944-128">This will show the fields where you need to enter your subscription details.</span></span>
   
    ![configurer le profil][configure profile]
5. <span data-ttu-id="52944-130">Copiez l'ID d'abonnement et le certificat de gestion de votre profil d'abonnement et collez-les dans les champs appropriés.</span><span class="sxs-lookup"><span data-stu-id="52944-130">Copy the subscription id and management certificate from your subscription profile and paste them in the appropriate fields.</span></span>
   
    <span data-ttu-id="52944-131">Lors de la copie de l'ID d'abonnement et du certificat de gestion, n'incluez **pas** les guillemets qui entourent les valeurs.</span><span class="sxs-lookup"><span data-stu-id="52944-131">When copying the subscription id and management certificate, **do not** include the quotes that enclose the values.</span></span>
6. <span data-ttu-id="52944-132">Cliquez sur **Verify configuration**(Vérifier la configuration).</span><span class="sxs-lookup"><span data-stu-id="52944-132">Click on **Verify configuration**.</span></span>
7. <span data-ttu-id="52944-133">Lorsque la configuration est vérifiée avec succès, cliquez sur **Save**(Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="52944-133">When the configuration is verified successfully, click **Save**.</span></span>

## <a name="set-up-a-virtual-machine-template-for-the-azure-slave-plug-in"></a><span data-ttu-id="52944-134">Configuration d’un modèle de machine virtuelle pour le plug-in subordonné Azure</span><span class="sxs-lookup"><span data-stu-id="52944-134">Set up a virtual machine template for the Azure Slave plug-in</span></span>
<span data-ttu-id="52944-135">Un modèle de machine virtuelle définit les paramètres qui seront utilisés par le plug-in pour créer un nœud subordonné dans Azure.</span><span class="sxs-lookup"><span data-stu-id="52944-135">A virtual machine template defines the parameters the plug-in will use to create a slave node on Azure.</span></span> <span data-ttu-id="52944-136">Dans les étapes suivantes, nous allons créer un modèle pour un ordinateur virtuel Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="52944-136">In the following steps we'll be creating template for an Ubuntu VM.</span></span>

1. <span data-ttu-id="52944-137">Dans le tableau de bord Hudson, cliquez sur **Manage Hudson**(Gérer Hudson).</span><span class="sxs-lookup"><span data-stu-id="52944-137">In the Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="52944-138">Cliquez sur **Configure System**(Configurer le système).</span><span class="sxs-lookup"><span data-stu-id="52944-138">Click on **Configure System**.</span></span>
3. <span data-ttu-id="52944-139">Faites défiler la page vers le bas pour trouver la section **Cloud** .</span><span class="sxs-lookup"><span data-stu-id="52944-139">Scroll down the page to find the **Cloud** section.</span></span>
4. <span data-ttu-id="52944-140">Dans la section **Cloud**, recherchez **Add Azure Virtual Machine Template** (Ajouter un modèle de machine virtuelle Azure) et cliquez sur le bouton **Add** (Ajouter).</span><span class="sxs-lookup"><span data-stu-id="52944-140">Within the **Cloud** section, find **Add Azure Virtual Machine Template** and click the **Add** button.</span></span>
   
    ![ajouter un modèle d'ordinateur virtuel][add vm template]
5. <span data-ttu-id="52944-142">Spécifiez un nom de service cloud dans le champ **Name** (Nom).</span><span class="sxs-lookup"><span data-stu-id="52944-142">Specify a cloud service name in the **Name** field.</span></span> <span data-ttu-id="52944-143">Si le nom spécifié fait référence à un service cloud existant, l'ordinateur virtuel sera déployé dans ce service.</span><span class="sxs-lookup"><span data-stu-id="52944-143">If the name you specify refers to an existing cloud service, the VM will be provisioned in that service.</span></span> <span data-ttu-id="52944-144">Dans le cas contraire, Azure en crée un nouveau.</span><span class="sxs-lookup"><span data-stu-id="52944-144">Otherwise, Azure will create a new one.</span></span>
6. <span data-ttu-id="52944-145">Dans le champ **Description** , entrez du texte qui décrit le modèle que vous créez.</span><span class="sxs-lookup"><span data-stu-id="52944-145">In the **Description** field, enter text that describes the template you are creating.</span></span> <span data-ttu-id="52944-146">Ces informations sont uniquement à des fins documentaires et ne sont pas utilisées dans la mise en service d'un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="52944-146">This information is only for documentary purposes and is not used in provisioning a VM.</span></span>
7. <span data-ttu-id="52944-147">Dans le champ **Labels** (Étiquettes), entrez **linux**.</span><span class="sxs-lookup"><span data-stu-id="52944-147">In the **Labels** field, enter **linux**.</span></span> <span data-ttu-id="52944-148">Cette étiquette est utilisée pour identifier le modèle que vous créez. Elle est ensuite utilisée pour référencer le modèle lors de la création d'un travail Hudson.</span><span class="sxs-lookup"><span data-stu-id="52944-148">This label is used to identify the template you are creating and is subsequently used to reference the template when creating a Hudson job.</span></span>
8. <span data-ttu-id="52944-149">Sélectionnez une région où l'ordinateur virtuel sera créé.</span><span class="sxs-lookup"><span data-stu-id="52944-149">Select a region where the VM will be created.</span></span>
9. <span data-ttu-id="52944-150">Sélectionnez la taille appropriée pour l'ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="52944-150">Select the appropriate VM size.</span></span>
10. <span data-ttu-id="52944-151">Spécifiez un compte de stockage dans lequel l'ordinateur virtuel sera créé.</span><span class="sxs-lookup"><span data-stu-id="52944-151">Specify a storage account where the VM will be created.</span></span> <span data-ttu-id="52944-152">Assurez-vous qu'il se trouve dans la même région que le service Cloud que vous allez utiliser.</span><span class="sxs-lookup"><span data-stu-id="52944-152">Make sure that it is in the same region as the cloud service you'll be using.</span></span> <span data-ttu-id="52944-153">Si vous souhaitez créer un nouveau stockage, vous pouvez laisser ce champ vide.</span><span class="sxs-lookup"><span data-stu-id="52944-153">If you want new storage to be created, you can leave this field blank.</span></span>
11. <span data-ttu-id="52944-154">La durée de conservation spécifie le nombre de minutes avant la suppression d'un esclave inactif par Hudson.</span><span class="sxs-lookup"><span data-stu-id="52944-154">Retention time specifies the number of minutes before Hudson deletes an idle slave.</span></span> <span data-ttu-id="52944-155">Conservez la valeur par défaut de 60.</span><span class="sxs-lookup"><span data-stu-id="52944-155">Leave this at the default value of 60.</span></span>
12. <span data-ttu-id="52944-156">Dans **Usage**(Utilisation), sélectionnez la condition appropriée lorsque ce nœud subordonné sera utilisé.</span><span class="sxs-lookup"><span data-stu-id="52944-156">In **Usage**, select the appropriate condition when this slave node will be used.</span></span> <span data-ttu-id="52944-157">Pour l'instant, sélectionnez **Utilize this node as much as possible**(Utiliser ce nœud autant que possible).</span><span class="sxs-lookup"><span data-stu-id="52944-157">For now, select **Utilize this node as much as possible**.</span></span>
    
     <span data-ttu-id="52944-158">À ce stade, votre formulaire doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="52944-158">At this point, your form would look somewhat similar to this:</span></span>
    
     ![configuration du modèle][template config]
13. <span data-ttu-id="52944-160">Dans **Image Family or Id** (Famille d'images ou ID), vous devez spécifier l'image système qui sera installée sur votre ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="52944-160">In **Image Family or Id** you have to specify what system image will be installed on your VM.</span></span> <span data-ttu-id="52944-161">Vous pouvez faire votre choix dans une liste de familles d'images ou spécifier une image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="52944-161">You can either select from a list of image families or specify a custom image.</span></span>
    
     <span data-ttu-id="52944-162">Si vous souhaitez faire votre choix dans une liste de familles d'images, entrez le premier caractère (respectez la casse) du nom de famille de l'image.</span><span class="sxs-lookup"><span data-stu-id="52944-162">If you want to select from a list of image families, enter the first character (case-sensitive) of the image family name.</span></span> <span data-ttu-id="52944-163">Par exemple, le fait de taper **U** affichera une liste des familles de serveurs Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="52944-163">For instance, typing **U** will bring up a list of Ubuntu Server families.</span></span> <span data-ttu-id="52944-164">Une fois que vous avez fait votre choix dans la liste, Hudson utilisera la version la plus récente de cette image système de cette famille lors de la mise en service de l'ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="52944-164">Once you select from the list, Jenkins will use the latest version of that system image from that family when provisioning your VM.</span></span>
    
     ![liste de famille de système d'exploitation][OS family list]
    
     <span data-ttu-id="52944-166">Si vous avez une image personnalisée que vous souhaitez utiliser à la place, entrez son nom.</span><span class="sxs-lookup"><span data-stu-id="52944-166">If you have a custom image that you want to use instead, enter the name of that custom image.</span></span> <span data-ttu-id="52944-167">Les noms des images personnalisées ne figurent pas dans une liste. Vous devez donc vous assurer que le nom est entré correctement.</span><span class="sxs-lookup"><span data-stu-id="52944-167">Custom image names are not shown in a list so you have to ensure that the name is entered correctly.</span></span>    
    
     <span data-ttu-id="52944-168">Pour ce didacticiel, tapez **U** pour afficher la liste des images Ubuntu et sélectionnez **Ubuntu Server 14.04 LTS**.</span><span class="sxs-lookup"><span data-stu-id="52944-168">For this tutorial, type **U** to bring up a list of Ubuntu images and select **Ubuntu Server 14.04 LTS**.</span></span>
14. <span data-ttu-id="52944-169">Pour la **méthode de lancement**, sélectionnez **SSH**.</span><span class="sxs-lookup"><span data-stu-id="52944-169">For **Launch method**, select **SSH**.</span></span>
15. <span data-ttu-id="52944-170">Copiez le script ci-dessous et collez-le dans le champ du **script init** .</span><span class="sxs-lookup"><span data-stu-id="52944-170">Copy the script below and paste in the **Init script** field.</span></span>
    
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
    
     <span data-ttu-id="52944-171">Le **script init** sera exécuté une fois l'ordinateur virtuel créé.</span><span class="sxs-lookup"><span data-stu-id="52944-171">The **Init script** will be executed after the VM is created.</span></span> <span data-ttu-id="52944-172">Dans cet exemple, le script installe Java, git et ant.</span><span class="sxs-lookup"><span data-stu-id="52944-172">In this example, the script installs Java, git, and ant.</span></span>
16. <span data-ttu-id="52944-173">Dans les champs **Username** (Nom d’utilisateur) et **Password** (Mot de passe), saisissez les valeurs de votre choix pour le compte administrateur qui sera créé sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="52944-173">In the **Username** and **Password** fields, enter your preferred values for the administrator account that will be created on your VM.</span></span>
17. <span data-ttu-id="52944-174">Cliquez sur **Verify Template** (Vérifier le modèle) pour vérifier si les paramètres spécifiés sont valides.</span><span class="sxs-lookup"><span data-stu-id="52944-174">Click on **Verify Template** to check if the parameters you specified are valid.</span></span>
18. <span data-ttu-id="52944-175">Cliquez sur **Save**(Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="52944-175">Click on **Save**.</span></span>

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a><span data-ttu-id="52944-176">Créer un travail Hudson qui s'exécute sur un nœud subordonné sur Azure</span><span class="sxs-lookup"><span data-stu-id="52944-176">Create a Hudson job that runs on a slave node on Azure</span></span>
<span data-ttu-id="52944-177">Dans cette section, vous allez créer un travail Hudson qui s'exécutera sur un nœud subordonné sur Azure.</span><span class="sxs-lookup"><span data-stu-id="52944-177">In this section, you'll be creating a Hudson task that will run on a slave node on Azure.</span></span>

1. <span data-ttu-id="52944-178">Dans le tableau de bord Hudson, cliquez sur **New Job**(Nouveau travail).</span><span class="sxs-lookup"><span data-stu-id="52944-178">In the Hudson dashboard, click **New Job**.</span></span>
2. <span data-ttu-id="52944-179">Entrez un nom pour le travail que vous créez.</span><span class="sxs-lookup"><span data-stu-id="52944-179">Enter a name for the job you are creating.</span></span>
3. <span data-ttu-id="52944-180">Pour le type de travail, sélectionnez **Build a free-style software job**(Générer un travail logiciel libre).</span><span class="sxs-lookup"><span data-stu-id="52944-180">For the job type, select **Build a free-style software job**.</span></span>
4. <span data-ttu-id="52944-181">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="52944-181">Click **OK**.</span></span>
5. <span data-ttu-id="52944-182">Dans la page de configuration du travail, sélectionnez **Restrict where this project can be run**(Limiter où ce projet peut être exécuté).</span><span class="sxs-lookup"><span data-stu-id="52944-182">In the job configuration page, select **Restrict where this project can be run**.</span></span>
6. <span data-ttu-id="52944-183">Sélectionnez **Node and label menu** (Menu nœud et étiquette) et sélectionnez **linux** (nous avons spécifié cette étiquette lors de la création du modèle de machine virtuelle dans la section précédente).</span><span class="sxs-lookup"><span data-stu-id="52944-183">Select **Node and label menu** and select **linux** (we specified this label when creating the virtual machine template in the previous section).</span></span>
7. <span data-ttu-id="52944-184">Dans la section **Build**, cliquez sur **Add build step** (Ajouter une étape de build) et sélectionnez **Execute shell** (Exécuter shell).</span><span class="sxs-lookup"><span data-stu-id="52944-184">In the **Build** section, click **Add build step** and select **Execute shell**.</span></span>
8. <span data-ttu-id="52944-185">Modifiez le script suivant, en remplaçant **{your github account name}**, **{your project name}** et **{your project directory}** par les valeurs appropriées et collez le script modifié dans la zone de texte qui s’affiche.</span><span class="sxs-lookup"><span data-stu-id="52944-185">Edit the following script, replacing **{your github account name}**, **{your project name}**, and **{your project directory}** with appropriate values, and paste the edited script in the text area that appears.</span></span>
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory to project
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. <span data-ttu-id="52944-186">Cliquez sur **Save**(Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="52944-186">Click on **Save**.</span></span>
10. <span data-ttu-id="52944-187">Dans le tableau de bord Hudson, recherchez le travail que vous venez de créer, puis cliquez sur l'icône **Schedule a build** (Planifier un build).</span><span class="sxs-lookup"><span data-stu-id="52944-187">In the Hudson dashboard, find the job you just created and click on the **Schedule a build** icon.</span></span>

<span data-ttu-id="52944-188">Hudson crée ensuite un nœud subordonné à l'aide du modèle créé dans la section précédente, puis il exécute le script que vous avez spécifié dans l'étape de build pour ce travail.</span><span class="sxs-lookup"><span data-stu-id="52944-188">Hudson will then create a slave node using the template created in the previous section and execute the script you specified in the build step for this task.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52944-189">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="52944-189">Next Steps</span></span>
<span data-ttu-id="52944-190">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez le [Centre de développement Java pour Azure].</span><span class="sxs-lookup"><span data-stu-id="52944-190">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="52944-191">[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="52944-191">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="52944-192">[profil d’abonnement]: http://go.microsoft.com/fwlink/?LinkID=396395</span><span class="sxs-lookup"><span data-stu-id="52944-192">[subscription profile]: http://go.microsoft.com/fwlink/?LinkID=396395</span></span>

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

