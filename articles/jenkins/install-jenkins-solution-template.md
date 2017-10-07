---
title: aaaCreate un serveur Jenkins sur Azure
description: "Installer Jenkins sur une machine virtuelle de Azure Linux à partir du modèle de solution Jenkins hello et générer un exemple d’application Java."
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 82ab2ac52594acba131414b449b608978591d4b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-hello-azure-portal"></a><span data-ttu-id="07627-103">Créer un serveur Jenkins sur une machine virtuelle Linux de Azure à partir de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="07627-103">Create a Jenkins server on an Azure Linux VM from hello Azure portal</span></span>

<span data-ttu-id="07627-104">Ce démarrage rapide montre comment tooinstall [Jenkins](https://jenkins.io) sur une machine virtuelle Ubuntu Linux avec les outils de hello et de plug-ins configurés toowork avec Azure.</span><span class="sxs-lookup"><span data-stu-id="07627-104">This quickstart shows how tooinstall [Jenkins](https://jenkins.io) on an Ubuntu Linux VM with hello tools and plug-ins configured toowork with Azure.</span></span> <span data-ttu-id="07627-105">Lorsque vous avez terminé, vous disposez d’un serveur de Jenkins s’exécutant dans Azure qui génère un exemple d’application Java à partir de [Github](https://github.com).</span><span class="sxs-lookup"><span data-stu-id="07627-105">When you're finished, you have a Jenkins server running in Azure building a sample Java app from [GitHub](https://github.com).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07627-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="07627-106">Prerequisites</span></span>

* <span data-ttu-id="07627-107">Un abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="07627-107">An Azure subscription</span></span>
* <span data-ttu-id="07627-108">TooSSH d’accès sur la ligne de commande de votre ordinateur (par exemple hello Bash shell ou [PuTTY](http://www.putty.org/))</span><span class="sxs-lookup"><span data-stu-id="07627-108">Access tooSSH on your computer's command line (such as hello Bash shell or [PuTTY](http://www.putty.org/))</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-jenkins-vm-from-hello-solution-template"></a><span data-ttu-id="07627-109">Créer hello Jenkins VM à partir du modèle de solution hello</span><span class="sxs-lookup"><span data-stu-id="07627-109">Create hello Jenkins VM from hello solution template</span></span>

<span data-ttu-id="07627-110">Ouvrez hello [une image marketplace pour Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) dans votre navigateur web, puis sélectionnez **GET IT maintenant** à partir de la partie gauche de la page de hello hello.</span><span class="sxs-lookup"><span data-stu-id="07627-110">Open hello [marketplace image for Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) in your web browser and select  **GET IT NOW** from hello left-hand side of hello page.</span></span> <span data-ttu-id="07627-111">Hello révision prix et sélectionnez **continuer**, puis sélectionnez **créer** serveur Jenkins tooconfigure hello hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="07627-111">Review hello pricing details and select **Continue**, then select **Create** tooconfigure hello Jenkins server in hello Azure portal.</span></span> 
   
![Boîte de dialogue du Portail Azure](./media/install-jenkins-solution-template/ap-create.png)

<span data-ttu-id="07627-113">Bonjour **configurer les paramètres de base** onglet, renseignez hello champs qui suivent :</span><span class="sxs-lookup"><span data-stu-id="07627-113">In hello **Configure basic settings** tab, fill in hello following fields:</span></span>

![Configurer les paramètres de base](./media/install-jenkins-solution-template/ap-basic.png)

* <span data-ttu-id="07627-115">Utilisez **Jenkins** comme **Nom**.</span><span class="sxs-lookup"><span data-stu-id="07627-115">Use **Jenkins** for **Name**.</span></span>
* <span data-ttu-id="07627-116">Entrez un **Nom d’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="07627-116">Enter a **User name**.</span></span> <span data-ttu-id="07627-117">nom d’utilisateur Hello doit répondre aux [aux exigences](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="07627-117">hello user name must meet [specific requirements](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span></span>
* <span data-ttu-id="07627-118">Sélectionnez **mot de passe** comme hello **type d’authentification** et entrez un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="07627-118">Select **Password** as hello **Authentication type** and enter a password.</span></span> <span data-ttu-id="07627-119">Hello le mot de passe doit contenir une lettre majuscule, un nombre et un caractère spécial.</span><span class="sxs-lookup"><span data-stu-id="07627-119">hello password must have an upper case character, a number, and one special character.</span></span>
* <span data-ttu-id="07627-120">Utilisez **myJenkinsResourceGroup** pour hello **groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="07627-120">Use **myJenkinsResourceGroup** for hello **Resource Group**.</span></span>
* <span data-ttu-id="07627-121">Choisissez hello **États-Unis** [région Azure](https://azure.microsoft.com/regions/) de hello **emplacement** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="07627-121">Choose hello **East US** [Azure region](https://azure.microsoft.com/regions/) from hello **Location** drop-down.</span></span>

<span data-ttu-id="07627-122">Sélectionnez **OK** tooproceed toohello **configurer des options supplémentaires** onglet. Entrez un nom unique de domaine nom tooidentify hello Jenkins et sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="07627-122">Select **OK** tooproceed toohello **Configure additional options** tab. Enter a unique domain name tooidentify hello Jenkins server and select **OK**.</span></span>

![Configurer des options supplémentaires](./media/install-jenkins-solution-template/ap-addtional.png)  

 <span data-ttu-id="07627-124">Une fois la validation réussit, sélectionnez **OK** à partir de hello **Résumé** onglet. Enfin, sélectionnez **achat** toocreate hello Jenkins VM.</span><span class="sxs-lookup"><span data-stu-id="07627-124">Once validation passes, select **OK** again from hello **Summary** tab. Finally, select **Purchase** toocreate hello Jenkins VM.</span></span> <span data-ttu-id="07627-125">Lorsque votre serveur est prêt, vous recevez une notification Bonjour portail Azure :</span><span class="sxs-lookup"><span data-stu-id="07627-125">When your server is ready, you get a notification in hello Azure portal:</span></span>   

![Notification Jenkins est prêt](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-toojenkins"></a><span data-ttu-id="07627-127">Se connecter tooJenkins</span><span class="sxs-lookup"><span data-stu-id="07627-127">Connect tooJenkins</span></span>

<span data-ttu-id="07627-128">Accédez tooyour virtual machine (par exemple, http://jenkins2517454.eastus.cloudapp.azure.com/) dans votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="07627-128">Navigate tooyour virtual machine (for example, http://jenkins2517454.eastus.cloudapp.azure.com/) in  your web browser.</span></span> <span data-ttu-id="07627-129">console de Jenkins Hello n’est pas accessible via le protocole HTTP non sécurisé afin de vous trouverez des instructions sur la console de Jenkins hello page tooaccess hello en toute sécurité à partir de votre ordinateur à l’aide d’un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="07627-129">hello Jenkins console is inaccessible through unsecured HTTP so instructions are provided on hello page tooaccess hello Jenkins console securely from your computer using an SSH tunnel.</span></span>

![Déverrouiller Jenkins](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

<span data-ttu-id="07627-131">Configurer tunnel hello à l’aide de hello `ssh` commande page hello à partir de la ligne de commande hello, en remplaçant `username` avec le nom d’utilisateur d’administrateur de machine virtuelle hello choisi précédemment lors de la configuration d’ordinateur virtuel de hello à partir de modèle de solution hello de hello.</span><span class="sxs-lookup"><span data-stu-id="07627-131">Set up hello tunnel using hello `ssh` command on hello page from hello command line, replacing `username` with hello name of hello virtual machine admin user chosen earlier when setting up hello virtual machine from hello solution template.</span></span>

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

<span data-ttu-id="07627-132">Une fois que vous avez démarré le tunnel de hello, accédez toohttp://localhost:8080 / sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="07627-132">After you have started hello tunnel, navigate toohttp://localhost:8080/ on your local machine.</span></span> 

<span data-ttu-id="07627-133">Obtenir le mot de passe initial de hello en exécutant hello commande dans la ligne de commande hello tout en étant connecté via SSH toohello Jenkins VM suivante.</span><span class="sxs-lookup"><span data-stu-id="07627-133">Get hello initial password by running hello following command in hello command line while connected through SSH toohello Jenkins VM.</span></span>

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

<span data-ttu-id="07627-134">Déverrouillage du tableau de bord Jenkins hello pour hello première fois à l’aide de ce mot de passe initial.</span><span class="sxs-lookup"><span data-stu-id="07627-134">Unlock hello Jenkins dashboard for hello first time using this initial password.</span></span>

![Déverrouiller Jenkins](./media/install-jenkins-solution-template/jenkins-unlock.png)

<span data-ttu-id="07627-136">Sélectionnez **installer le plug-ins suggérées** sur hello page suivante, puis créez un Jenkins administrateur de l’utilisateur utilisées tooaccess hello Jenkins du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="07627-136">Select **Install suggested plugins** on hello next page and then create a Jenkins admin user used tooaccess hello Jenkins dashboard.</span></span>

![Jenkins est prêt à l’emploi](./media/install-jenkins-solution-template/jenkins-welcome.png)

<span data-ttu-id="07627-138">Hello Jenkins serveur est maintenant prêt toobuild code.</span><span class="sxs-lookup"><span data-stu-id="07627-138">hello Jenkins server is now ready toobuild code.</span></span>

## <a name="create-your-first-job"></a><span data-ttu-id="07627-139">Créer votre premier travail</span><span class="sxs-lookup"><span data-stu-id="07627-139">Create your first job</span></span>

<span data-ttu-id="07627-140">Sélectionnez **créer de nouveaux travaux** à partir de la console de Jenkins hello, puis nommez-le **mySampleApp** et sélectionnez **projet Freestyle**, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="07627-140">Select **Create new jobs** from hello Jenkins console, then name it **mySampleApp** and select **Freestyle project**, then select **OK**.</span></span>

![Créer un travail](./media/install-jenkins-solution-template/jenkins-new-job.png) 

<span data-ttu-id="07627-142">Sélectionnez hello **gestion du Code Source** onglet, activez **Git**, puis entrez hello suivant des URL dans **URL du référentiel** champ :`https://github.com/spring-guides/gs-spring-boot.git`</span><span class="sxs-lookup"><span data-stu-id="07627-142">Select hello **Source Code Management** tab, enable **Git**, and enter hello following URL in **Repository URL**  field: `https://github.com/spring-guides/gs-spring-boot.git`</span></span>

![Définir le référentiel Git de hello](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

<span data-ttu-id="07627-144">Sélectionnez hello **générer** , puis sélectionnez **étape de génération ajouter**, **Gradle d’appel de script**.</span><span class="sxs-lookup"><span data-stu-id="07627-144">Select hello **Build** tab, then select **Add build step**, **Invoke Gradle script**.</span></span> <span data-ttu-id="07627-145">Sélectionnez **Utiliser Gradle Wrapper**, puis entrez `complete` dans l’**emplacement de Wrapper** et `build` pour **Tâches**.</span><span class="sxs-lookup"><span data-stu-id="07627-145">Select **Use Gradle Wrapper**, then enter `complete` in **Wrapper location** and `build` for **Tasks**.</span></span>

![Utilisez hello Gradle wrapper toobuild](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

<span data-ttu-id="07627-147">Sélectionnez **Avancé..**</span><span class="sxs-lookup"><span data-stu-id="07627-147">Select **Advanced..**</span></span> <span data-ttu-id="07627-148">puis entrez `complete` Bonjour **racine générer un script** champ.</span><span class="sxs-lookup"><span data-stu-id="07627-148">and then enter `complete` in hello **Root Build script** field.</span></span> <span data-ttu-id="07627-149">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="07627-149">Select **Save**.</span></span>

![Définir les paramètres avancés dans l’étape de génération de wrapper Gradle hello](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-hello-code"></a><span data-ttu-id="07627-151">Générer du code de hello</span><span class="sxs-lookup"><span data-stu-id="07627-151">Build hello code</span></span>

<span data-ttu-id="07627-152">Sélectionnez **générer maintenant** toocompile hello code et le package hello exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="07627-152">Select **Build Now** toocompile hello code and package hello sample app.</span></span> <span data-ttu-id="07627-153">Lorsque votre build est terminée, sélectionnez hello **espace de travail** lien pour le projet de hello.</span><span class="sxs-lookup"><span data-stu-id="07627-153">When your build completes, select hello **Workspace** link for hello project.</span></span>

![Parcourir le fichier toohello espace de travail tooget hello JAR à partir de la génération de hello](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

<span data-ttu-id="07627-155">Accédez trop`complete/build/libs` et vérifiez que hello `gs-spring-boot-0.1.0.jar` existe-t-il tooverify que votre build a réussi.</span><span class="sxs-lookup"><span data-stu-id="07627-155">Navigate too`complete/build/libs` and ensure hello `gs-spring-boot-0.1.0.jar` is there tooverify that your build was successful.</span></span> <span data-ttu-id="07627-156">Votre Jenkins serveur est maintenant prêt à toobuild vos projets dans Azure.</span><span class="sxs-lookup"><span data-stu-id="07627-156">Your Jenkins server is now ready toobuild your own projects in Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07627-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="07627-157">Next Steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="07627-158">Ajouter des machines virtuelles Azure en tant qu’agents Jenkins</span><span class="sxs-lookup"><span data-stu-id="07627-158">Add Azure VMs as Jenkins agents</span></span>](jenkins-azure-vm-agents.md)
