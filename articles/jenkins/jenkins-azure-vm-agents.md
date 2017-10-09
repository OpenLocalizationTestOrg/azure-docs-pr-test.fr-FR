---
title: "agents de machine virtuelle Azure aaaUse pour l’intégration continue avec Jenkins."
description: "Agents de machine virtuelle Azure en tant que subordonnés de Jenkins."
services: multiple
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 2388e6919d0280372166fbd325d80dafb00d7550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a><span data-ttu-id="d03d6-103">Utilisez des agents de machine virtuelle Azure pour l’intégration continue avec Jenkins.</span><span class="sxs-lookup"><span data-stu-id="d03d6-103">Use Azure VM agents for continuous integration with Jenkins.</span></span>

<span data-ttu-id="d03d6-104">Ce démarrage rapide montre comment toouse hello toocreate de plug-in d’Agents de machine virtuelle Azure Jenkins un agent de Linux (Ubuntu) à la demande dans Azure.</span><span class="sxs-lookup"><span data-stu-id="d03d6-104">This quickstart shows how toouse hello Jenkins Azure VM Agents plugin toocreate an on-demand Linux (Ubuntu) agent in Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d03d6-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d03d6-105">Prerequisites</span></span>

<span data-ttu-id="d03d6-106">toocomplete ce démarrage rapide :</span><span class="sxs-lookup"><span data-stu-id="d03d6-106">toocomplete this quickstart:</span></span>

* <span data-ttu-id="d03d6-107">Si vous n’avez pas déjà un maître de Jenkins, vous pouvez démarrer avec hello [modèle de Solution](install-jenkins-solution-template.md)</span><span class="sxs-lookup"><span data-stu-id="d03d6-107">If you do not already have a Jenkins master, you can start with hello [Solution Template](install-jenkins-solution-template.md)</span></span> 
* <span data-ttu-id="d03d6-108">Consultez trop[créer un principal de Service Azure avec Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) si vous n’avez pas déjà un principal du service Azure.</span><span class="sxs-lookup"><span data-stu-id="d03d6-108">Refer too[Create an Azure Service principal with Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) if you do not already have an Azure service principal.</span></span>

## <a name="install-azure-vm-agents-plugin"></a><span data-ttu-id="d03d6-109">Installer le plug-in Agents de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="d03d6-109">Install Azure VM Agents plugin</span></span>

<span data-ttu-id="d03d6-110">Si vous démarrez à partir de hello [modèle de Solution](install-jenkins-solution-template.md), plug-in de l’Agent de machine virtuelle Azure hello est installé dans le masque de Jenkins hello.</span><span class="sxs-lookup"><span data-stu-id="d03d6-110">If you start from hello [Solution Template](install-jenkins-solution-template.md), hello Azure VM Agent plugin is installed in hello Jenkins master.</span></span>

<span data-ttu-id="d03d6-111">Sinon, installer hello **Agents de machine virtuelle Azure** plug-in à partir du tableau de bord hello Jenkins.</span><span class="sxs-lookup"><span data-stu-id="d03d6-111">Otherwise, install hello **Azure VM Agents** plugin from within hello Jenkins dashboard.</span></span>

## <a name="configure-hello-plugin"></a><span data-ttu-id="d03d6-112">Configurer le plug-in hello</span><span class="sxs-lookup"><span data-stu-id="d03d6-112">Configure hello plugin</span></span>

* <span data-ttu-id="d03d6-113">Dans le tableau de bord hello Jenkins, cliquez sur **Jenkins de gérer -> configuration du système ->**.</span><span class="sxs-lookup"><span data-stu-id="d03d6-113">Within hello Jenkins dashboard, click **Manage Jenkins -> Configure System ->**.</span></span> <span data-ttu-id="d03d6-114">Faites défiler bas toohello de page de hello et rechercher la section hello avec hello déroulant **Ajouter nouveau cloud**.</span><span class="sxs-lookup"><span data-stu-id="d03d6-114">Scroll toohello bottom of hello page and find hello section with hello dropdown **Add new cloud**.</span></span> <span data-ttu-id="d03d6-115">Dans le menu de hello, sélectionnez **Agents de machine virtuelle Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="d03d6-115">From hello menu, select **Microsoft Azure VM Agents**</span></span>
* <span data-ttu-id="d03d6-116">Sélectionnez un compte existant à partir de la liste déroulante de hello informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="d03d6-116">Select an existing account from hello Azure Credentials dropdown.</span></span>  <span data-ttu-id="d03d6-117">tooadd un nouveau **Principal du Service Microsoft Azure,** entrez hello valeurs suivantes : ID d’abonnement, ID de Client, question secrète du Client et OAuth 2.0 Token Endpoint.</span><span class="sxs-lookup"><span data-stu-id="d03d6-117">tooadd a new **Microsoft Azure Service Principal,** enter hello following values: Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span>

![Informations d’identification Azure](./media/jenkins-azure-vm-agents/service-principal.png)

* <span data-ttu-id="d03d6-119">Cliquez sur **Vérifiez configuration** toomake que cette configuration de profil hello est correcte.</span><span class="sxs-lookup"><span data-stu-id="d03d6-119">Click **Verify configuration** toomake sure that hello profile configuration is correct.</span></span>
* <span data-ttu-id="d03d6-120">Enregistrer la configuration de hello et continuer toohello prochaine étape.</span><span class="sxs-lookup"><span data-stu-id="d03d6-120">Save hello configuration, and continue toohello next step.</span></span>

## <a name="template-configuration"></a><span data-ttu-id="d03d6-121">Configuration du modèle</span><span class="sxs-lookup"><span data-stu-id="d03d6-121">Template configuration</span></span>

### <a name="general-configuration"></a><span data-ttu-id="d03d6-122">Configuration générale</span><span class="sxs-lookup"><span data-stu-id="d03d6-122">General configuration</span></span>
<span data-ttu-id="d03d6-123">Ensuite, configurez un modèle pour utilisation toodefine un agent de machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="d03d6-123">Next, configure a template for use toodefine an Azure VM agent.</span></span> 

* <span data-ttu-id="d03d6-124">Cliquez sur **ajouter** tooadd un modèle.</span><span class="sxs-lookup"><span data-stu-id="d03d6-124">Click **Add** tooadd a template.</span></span> 
* <span data-ttu-id="d03d6-125">Entrez un nom pour votre nouveau modèle.</span><span class="sxs-lookup"><span data-stu-id="d03d6-125">Provide a name for your new template.</span></span> 
* <span data-ttu-id="d03d6-126">Pour l’étiquette de hello, entrez « ubuntu. »</span><span class="sxs-lookup"><span data-stu-id="d03d6-126">For hello label, enter  "ubuntu."</span></span> <span data-ttu-id="d03d6-127">Cette étiquette est utilisée lors de la configuration de tâche hello.</span><span class="sxs-lookup"><span data-stu-id="d03d6-127">This label is used during hello job configuration.</span></span>
* <span data-ttu-id="d03d6-128">Sélectionnez la région souhaités hello à partir de la zone de liste déroulante hello.</span><span class="sxs-lookup"><span data-stu-id="d03d6-128">Select hello desired region from hello combo box.</span></span>
* <span data-ttu-id="d03d6-129">Sélectionnez hello souhaité de taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d03d6-129">Select hello desired VM size.</span></span>
* <span data-ttu-id="d03d6-130">Spécifiez le nom de compte de stockage Azure hello ou laisser le nom par défaut de hello toouse vide « jenkinsarmst ».</span><span class="sxs-lookup"><span data-stu-id="d03d6-130">Specify hello Azure Storage account name or leave it blank toouse hello default name "jenkinsarmst."</span></span>
* <span data-ttu-id="d03d6-131">Spécifiez la durée de rétention hello en minutes.</span><span class="sxs-lookup"><span data-stu-id="d03d6-131">Specify hello retention time in minutes.</span></span> <span data-ttu-id="d03d6-132">Ce paramètre définit le nombre de hello de minutes que Jenkins peut attendre avant de supprimer automatiquement un agent inactif.</span><span class="sxs-lookup"><span data-stu-id="d03d6-132">This setting defines hello number of minutes Jenkins can wait before automatically deleting an idle agent.</span></span> <span data-ttu-id="d03d6-133">Spécifiez 0 si vous ne souhaitez pas toobe agents inactifs supprimé automatiquement.</span><span class="sxs-lookup"><span data-stu-id="d03d6-133">Specify 0 if you do not want idle agents toobe deleted automatically.</span></span>

![Configuration générale](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a><span data-ttu-id="d03d6-135">Configuration d’une image</span><span class="sxs-lookup"><span data-stu-id="d03d6-135">Image configuration</span></span>

<span data-ttu-id="d03d6-136">toocreate un agent Linux (Ubuntu), sélectionnez **référence d’Image** et utilisez hello suivant la configuration, par exemple.</span><span class="sxs-lookup"><span data-stu-id="d03d6-136">toocreate a Linux (Ubuntu) agent, select **Image reference** and use hello following configuration as an example.</span></span> <span data-ttu-id="d03d6-137">Consultez trop[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) hello Azure plus récente prises en charge les images.</span><span class="sxs-lookup"><span data-stu-id="d03d6-137">Refer too[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) for hello latest Azure supported images.</span></span>

* <span data-ttu-id="d03d6-138">Éditeur d’images : Canonical</span><span class="sxs-lookup"><span data-stu-id="d03d6-138">Image Publisher: Canonical</span></span>
* <span data-ttu-id="d03d6-139">Offre de l’image : UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="d03d6-139">Image Offer: UbuntuServer</span></span>
* <span data-ttu-id="d03d6-140">Référence SKU de l’image : 14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="d03d6-140">Image Sku: 14.04.5-LTS</span></span>
* <span data-ttu-id="d03d6-141">Version de l’image : la plus récente</span><span class="sxs-lookup"><span data-stu-id="d03d6-141">Image version: latest</span></span>
* <span data-ttu-id="d03d6-142">Type de système d’exploitation : Linux</span><span class="sxs-lookup"><span data-stu-id="d03d6-142">OS Type: Linux</span></span>
* <span data-ttu-id="d03d6-143">Méthode de lancement : SSH</span><span class="sxs-lookup"><span data-stu-id="d03d6-143">Launch method: SSH</span></span>
* <span data-ttu-id="d03d6-144">Fournir des informations d’identification d’administrateur</span><span class="sxs-lookup"><span data-stu-id="d03d6-144">Provide an admin credentials</span></span>
* <span data-ttu-id="d03d6-145">Pour le script d’initialisation de machine virtuelle, entrez :</span><span class="sxs-lookup"><span data-stu-id="d03d6-145">For VM initialization script, enter:</span></span>
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![Configuration d’une image](./media/jenkins-azure-vm-agents/image-config.png)

* <span data-ttu-id="d03d6-147">Cliquez sur **vérifier le modèle** configuration de hello tooverify.</span><span class="sxs-lookup"><span data-stu-id="d03d6-147">Click **Verify Template** tooverify hello configuration.</span></span>
* <span data-ttu-id="d03d6-148">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d03d6-148">Click **Save**.</span></span>

## <a name="create-a-job-in-jenkins"></a><span data-ttu-id="d03d6-149">Créer un travail dans Jenkins</span><span class="sxs-lookup"><span data-stu-id="d03d6-149">Create a job in Jenkins</span></span>

* <span data-ttu-id="d03d6-150">Dans le tableau de bord hello Jenkins, cliquez sur **un nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="d03d6-150">Within hello Jenkins dashboard, click **New Item**.</span></span> 
* <span data-ttu-id="d03d6-151">Entrez un nom, sélectionnez **Freestyle project (Projet libre)** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d03d6-151">Enter a name and select **Freestyle project** and click **OK**.</span></span>
* <span data-ttu-id="d03d6-152">Bonjour **général** onglet, sélectionnez « Restreindre où le projet peut être exécuté » et le type « ubuntu » dans l’Expression de l’étiquette.</span><span class="sxs-lookup"><span data-stu-id="d03d6-152">In hello **General** tab, select "Restrict where project can be run" and type "ubuntu" in Label Expression.</span></span> <span data-ttu-id="d03d6-153">Vous voyez maintenant « ubuntu » dans la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="d03d6-153">You now see "ubuntu" in hello dropdown.</span></span>
* <span data-ttu-id="d03d6-154">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d03d6-154">Click **Save**.</span></span>

![Configurer un travail](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a><span data-ttu-id="d03d6-156">Générer votre nouveau projet</span><span class="sxs-lookup"><span data-stu-id="d03d6-156">Build your new project</span></span>

* <span data-ttu-id="d03d6-157">Retournez dans le tableau de bord toohello Jenkins.</span><span class="sxs-lookup"><span data-stu-id="d03d6-157">Go back toohello Jenkins dashboard.</span></span>
* <span data-ttu-id="d03d6-158">Nouvelle tâche de hello avec le bouton que vous avez créé, puis cliquez sur **créer maintenant**.</span><span class="sxs-lookup"><span data-stu-id="d03d6-158">Right-click hello new job you created, then click **Build now**.</span></span> <span data-ttu-id="d03d6-159">Une génération est lancée.</span><span class="sxs-lookup"><span data-stu-id="d03d6-159">A build is kicked off.</span></span> 
* <span data-ttu-id="d03d6-160">Une fois la génération de hello est terminée, accédez trop**sortie de Console**.</span><span class="sxs-lookup"><span data-stu-id="d03d6-160">Once hello build is complete, go too**Console output**.</span></span> <span data-ttu-id="d03d6-161">Vous voyez que build de hello a été effectuée à distance sur Azure.</span><span class="sxs-lookup"><span data-stu-id="d03d6-161">You see that hello build was performed remotely on Azure.</span></span>

![Sortie de la console](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a><span data-ttu-id="d03d6-163">Référence</span><span class="sxs-lookup"><span data-stu-id="d03d6-163">Reference</span></span>

* <span data-ttu-id="d03d6-164">Vidéo Azure Friday : [intégration continue avec Jenkins à l’aide d’agents de machine virtuelle Azure](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span><span class="sxs-lookup"><span data-stu-id="d03d6-164">Azure Friday video: [Continuous Integration with Jenkins using Azure VM agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span></span>
* <span data-ttu-id="d03d6-165">Informations de prise en charge et options de configuration : [wiki du plug-in Jenkins pour agents de machine virtuelle Azure](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span><span class="sxs-lookup"><span data-stu-id="d03d6-165">Support information and configuration options:  [Azure VM Agent Jenkins Plugin Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span></span> 

