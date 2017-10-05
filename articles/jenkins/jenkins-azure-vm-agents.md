---
title: "Utilisez des agents de machine virtuelle Azure pour l’intégration continue avec Jenkins."
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
ms.openlocfilehash: 0b22a559fbc03158a6d4398603d1a7d2874d7b67
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a><span data-ttu-id="775e8-103">Utilisez des agents de machine virtuelle Azure pour l’intégration continue avec Jenkins.</span><span class="sxs-lookup"><span data-stu-id="775e8-103">Use Azure VM agents for continuous integration with Jenkins.</span></span>

<span data-ttu-id="775e8-104">Ce guide de démarrage rapide montre comment utiliser le plug-in d’agents de machine virtuelle Azure Jenkins pour créer un agent Linux (Ubuntu) à la demande dans Azure.</span><span class="sxs-lookup"><span data-stu-id="775e8-104">This quickstart shows how to use the Jenkins Azure VM Agents plugin to create an on-demand Linux (Ubuntu) agent in Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="775e8-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="775e8-105">Prerequisites</span></span>

<span data-ttu-id="775e8-106">Pour effectuer ce démarrage rapide :</span><span class="sxs-lookup"><span data-stu-id="775e8-106">To complete this quickstart:</span></span>

* <span data-ttu-id="775e8-107">Si vous n’avez pas encore de maître Jenkins, vous pouvez démarrer avec le [modèle de solution](install-jenkins-solution-template.md).</span><span class="sxs-lookup"><span data-stu-id="775e8-107">If you do not already have a Jenkins master, you can start with the [Solution Template](install-jenkins-solution-template.md)</span></span> 
* <span data-ttu-id="775e8-108">Reportez-vous à [Créer un principal du service Azure avec Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) si vous n’avez pas encore de principal de service Azure.</span><span class="sxs-lookup"><span data-stu-id="775e8-108">Refer to [Create an Azure Service principal with Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) if you do not already have an Azure service principal.</span></span>

## <a name="install-azure-vm-agents-plugin"></a><span data-ttu-id="775e8-109">Installer le plug-in Agents de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="775e8-109">Install Azure VM Agents plugin</span></span>

<span data-ttu-id="775e8-110">Si vous démarrez à partir du [modèle de solution](install-jenkins-solution-template.md), le plug-in Agents de machine virtuelle Azure est installé dans le maître Jenkins.</span><span class="sxs-lookup"><span data-stu-id="775e8-110">If you start from the [Solution Template](install-jenkins-solution-template.md), the Azure VM Agent plugin is installed in the Jenkins master.</span></span>

<span data-ttu-id="775e8-111">Sinon, installez le plug-in **Agents de machine virtuelle Azure** à partir du tableau de bord Jenkins.</span><span class="sxs-lookup"><span data-stu-id="775e8-111">Otherwise, install the **Azure VM Agents** plugin from within the Jenkins dashboard.</span></span>

## <a name="configure-the-plugin"></a><span data-ttu-id="775e8-112">Configurer le plug-in</span><span class="sxs-lookup"><span data-stu-id="775e8-112">Configure the plugin</span></span>

* <span data-ttu-id="775e8-113">Dans le tableau de bord Jenkins, cliquez sur **Manage Jenkins (Gérer Jenkins) -> Configure System (Configurer le système) ->**.</span><span class="sxs-lookup"><span data-stu-id="775e8-113">Within the Jenkins dashboard, click **Manage Jenkins -> Configure System ->**.</span></span> <span data-ttu-id="775e8-114">Faites défiler vers le bas de la page et recherchez la section avec la liste déroulante **Add new cloud (Ajouter un nouveau cloud)**.</span><span class="sxs-lookup"><span data-stu-id="775e8-114">Scroll to the bottom of the page and find the section with the dropdown **Add new cloud**.</span></span> <span data-ttu-id="775e8-115">Dans le menu, sélectionnez **Microsoft Azure VM Agents (Agents de machine virtuelle Microsoft Azure)**.</span><span class="sxs-lookup"><span data-stu-id="775e8-115">From the menu, select **Microsoft Azure VM Agents**</span></span>
* <span data-ttu-id="775e8-116">Sélectionnez un compte existant dans la liste déroulante Azure Credentials (Informations d’identification Azure).</span><span class="sxs-lookup"><span data-stu-id="775e8-116">Select an existing account from the Azure Credentials dropdown.</span></span>  <span data-ttu-id="775e8-117">Pour ajouter un nouveau **principal du service Microsoft Azure**, entrez les valeurs suivantes : ID d’abonnement, ID de client, clé secrète client et point de terminaison de jeton OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="775e8-117">To add a new **Microsoft Azure Service Principal,** enter the following values: Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span>

![Informations d’identification Azure](./media/jenkins-azure-vm-agents/service-principal.png)

* <span data-ttu-id="775e8-119">Cliquez sur **Verify configuration (Vérifier la configuration)** pour vous assurer que la configuration du profil est correcte.</span><span class="sxs-lookup"><span data-stu-id="775e8-119">Click **Verify configuration** to make sure that the profile configuration is correct.</span></span>
* <span data-ttu-id="775e8-120">Enregistrez la configuration et passez à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="775e8-120">Save the configuration, and continue to the next step.</span></span>

## <a name="template-configuration"></a><span data-ttu-id="775e8-121">Configuration du modèle</span><span class="sxs-lookup"><span data-stu-id="775e8-121">Template configuration</span></span>

### <a name="general-configuration"></a><span data-ttu-id="775e8-122">Configuration générale</span><span class="sxs-lookup"><span data-stu-id="775e8-122">General configuration</span></span>
<span data-ttu-id="775e8-123">Ensuite, configurez un modèle qui servira à définir un agent de machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="775e8-123">Next, configure a template for use to define an Azure VM agent.</span></span> 

* <span data-ttu-id="775e8-124">Cliquez sur **Add (Ajouter)** pour ajouter un modèle.</span><span class="sxs-lookup"><span data-stu-id="775e8-124">Click **Add** to add a template.</span></span> 
* <span data-ttu-id="775e8-125">Entrez un nom pour votre nouveau modèle.</span><span class="sxs-lookup"><span data-stu-id="775e8-125">Provide a name for your new template.</span></span> 
* <span data-ttu-id="775e8-126">Pour l’étiquette, entrez « ubuntu ».</span><span class="sxs-lookup"><span data-stu-id="775e8-126">For the label, enter  "ubuntu."</span></span> <span data-ttu-id="775e8-127">Cette étiquette est utilisée lors de la configuration du travail.</span><span class="sxs-lookup"><span data-stu-id="775e8-127">This label is used during the job configuration.</span></span>
* <span data-ttu-id="775e8-128">Dans la zone de liste modifiable, sélectionnez la région souhaitée.</span><span class="sxs-lookup"><span data-stu-id="775e8-128">Select the desired region from the combo box.</span></span>
* <span data-ttu-id="775e8-129">Sélectionnez la taille de machine virtuelle qui vous intéresse.</span><span class="sxs-lookup"><span data-stu-id="775e8-129">Select the desired VM size.</span></span>
* <span data-ttu-id="775e8-130">Spécifiez le nom de compte de stockage Azure ou laissez le champ vide pour utiliser le nom par défaut « jenkinsarmst ».</span><span class="sxs-lookup"><span data-stu-id="775e8-130">Specify the Azure Storage account name or leave it blank to use the default name "jenkinsarmst."</span></span>
* <span data-ttu-id="775e8-131">Spécifiez la durée de rétention en minutes.</span><span class="sxs-lookup"><span data-stu-id="775e8-131">Specify the retention time in minutes.</span></span> <span data-ttu-id="775e8-132">Ce paramètre définit le nombre de minutes que Jenkins peut attendre avant de supprimer automatiquement un agent inactif.</span><span class="sxs-lookup"><span data-stu-id="775e8-132">This setting defines the number of minutes Jenkins can wait before automatically deleting an idle agent.</span></span> <span data-ttu-id="775e8-133">Spécifiez 0 si vous ne souhaitez pas que les agents inactifs soient supprimés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="775e8-133">Specify 0 if you do not want idle agents to be deleted automatically.</span></span>

![Configuration générale](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a><span data-ttu-id="775e8-135">Configuration d’une image</span><span class="sxs-lookup"><span data-stu-id="775e8-135">Image configuration</span></span>

<span data-ttu-id="775e8-136">Pour créer un agent Linux (Ubuntu), sélectionnez **Image reference (Référence d’image)** et utilisez la configuration suivante comme exemple.</span><span class="sxs-lookup"><span data-stu-id="775e8-136">To create a Linux (Ubuntu) agent, select **Image reference** and use the following configuration as an example.</span></span> <span data-ttu-id="775e8-137">Consultez la [place de marché Microsoft Azure](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) pour obtenir les dernières images Azure prises en charge.</span><span class="sxs-lookup"><span data-stu-id="775e8-137">Refer to [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) for the latest Azure supported images.</span></span>

* <span data-ttu-id="775e8-138">Éditeur d’images : Canonical</span><span class="sxs-lookup"><span data-stu-id="775e8-138">Image Publisher: Canonical</span></span>
* <span data-ttu-id="775e8-139">Offre de l’image : UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="775e8-139">Image Offer: UbuntuServer</span></span>
* <span data-ttu-id="775e8-140">Référence SKU de l’image : 14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="775e8-140">Image Sku: 14.04.5-LTS</span></span>
* <span data-ttu-id="775e8-141">Version de l’image : la plus récente</span><span class="sxs-lookup"><span data-stu-id="775e8-141">Image version: latest</span></span>
* <span data-ttu-id="775e8-142">Type de système d’exploitation : Linux</span><span class="sxs-lookup"><span data-stu-id="775e8-142">OS Type: Linux</span></span>
* <span data-ttu-id="775e8-143">Méthode de lancement : SSH</span><span class="sxs-lookup"><span data-stu-id="775e8-143">Launch method: SSH</span></span>
* <span data-ttu-id="775e8-144">Fournir des informations d’identification d’administrateur</span><span class="sxs-lookup"><span data-stu-id="775e8-144">Provide an admin credentials</span></span>
* <span data-ttu-id="775e8-145">Pour le script d’initialisation de machine virtuelle, entrez :</span><span class="sxs-lookup"><span data-stu-id="775e8-145">For VM initialization script, enter:</span></span>
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![Configuration d’une image](./media/jenkins-azure-vm-agents/image-config.png)

* <span data-ttu-id="775e8-147">Cliquez sur **Verify Template (Vérifier le modèle)** pour vérifier la configuration.</span><span class="sxs-lookup"><span data-stu-id="775e8-147">Click **Verify Template** to verify the configuration.</span></span>
* <span data-ttu-id="775e8-148">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="775e8-148">Click **Save**.</span></span>

## <a name="create-a-job-in-jenkins"></a><span data-ttu-id="775e8-149">Créer un travail dans Jenkins</span><span class="sxs-lookup"><span data-stu-id="775e8-149">Create a job in Jenkins</span></span>

* <span data-ttu-id="775e8-150">Dans le tableau de bord Jenkins, cliquez sur **Nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="775e8-150">Within the Jenkins dashboard, click **New Item**.</span></span> 
* <span data-ttu-id="775e8-151">Entrez un nom, sélectionnez **Freestyle project (Projet libre)** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="775e8-151">Enter a name and select **Freestyle project** and click **OK**.</span></span>
* <span data-ttu-id="775e8-152">Dans l’onglet **General (Général)**, sélectionnez l’option « Restrict where project can be run » (Restreindre les emplacements d’exécution du projet) et saisissez « ubuntu » dans le champ Label Expression (Expression d’étiquette).</span><span class="sxs-lookup"><span data-stu-id="775e8-152">In the **General** tab, select "Restrict where project can be run" and type "ubuntu" in Label Expression.</span></span> <span data-ttu-id="775e8-153">Vous voyez maintenant « ubuntu » dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="775e8-153">You now see "ubuntu" in the dropdown.</span></span>
* <span data-ttu-id="775e8-154">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="775e8-154">Click **Save**.</span></span>

![Configurer un travail](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a><span data-ttu-id="775e8-156">Générer votre nouveau projet</span><span class="sxs-lookup"><span data-stu-id="775e8-156">Build your new project</span></span>

* <span data-ttu-id="775e8-157">Revenez au tableau de bord Jenkins.</span><span class="sxs-lookup"><span data-stu-id="775e8-157">Go back to the Jenkins dashboard.</span></span>
* <span data-ttu-id="775e8-158">Cliquez avec le bouton droit de la souris sur le travail que vous venez de créer, puis choisissez l’option **Build now (Générer maintenant)**.</span><span class="sxs-lookup"><span data-stu-id="775e8-158">Right-click the new job you created, then click **Build now**.</span></span> <span data-ttu-id="775e8-159">Une génération est lancée.</span><span class="sxs-lookup"><span data-stu-id="775e8-159">A build is kicked off.</span></span> 
* <span data-ttu-id="775e8-160">Une fois la génération terminée, accédez à la **sortie de la console**.</span><span class="sxs-lookup"><span data-stu-id="775e8-160">Once the build is complete, go to **Console output**.</span></span> <span data-ttu-id="775e8-161">Vous voyez que la génération a été effectuée à distance sur Azure.</span><span class="sxs-lookup"><span data-stu-id="775e8-161">You see that the build was performed remotely on Azure.</span></span>

![Sortie de la console](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a><span data-ttu-id="775e8-163">Référence</span><span class="sxs-lookup"><span data-stu-id="775e8-163">Reference</span></span>

* <span data-ttu-id="775e8-164">Vidéo Azure Friday : [intégration continue avec Jenkins à l’aide d’agents de machine virtuelle Azure](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span><span class="sxs-lookup"><span data-stu-id="775e8-164">Azure Friday video: [Continuous Integration with Jenkins using Azure VM agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span></span>
* <span data-ttu-id="775e8-165">Informations de prise en charge et options de configuration : [wiki du plug-in Jenkins pour agents de machine virtuelle Azure](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span><span class="sxs-lookup"><span data-stu-id="775e8-165">Support information and configuration options:  [Azure VM Agent Jenkins Plugin Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span></span> 

