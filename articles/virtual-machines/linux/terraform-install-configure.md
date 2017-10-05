---
title: "Installer et configurer Terraform pour approvisionner les machines virtuelles et d’autres infrastructures dans Azure | Microsoft Docs"
description: "Découvrez comment installer et configurer Terraform pour créer des ressources Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: da567097be38ac649c6bf1de1508de24d21cb877
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="install-and-configure-terraform-to-provision-vms-and-other-infrastructure-into-azure"></a><span data-ttu-id="8561f-103">Installer et configurer Terraform pour approvisionner les machines virtuelles et d’autres infrastructures dans Azure</span><span class="sxs-lookup"><span data-stu-id="8561f-103">Install and configure Terraform to provision VMs and other infrastructure into Azure</span></span> 
<span data-ttu-id="8561f-104">Cet article décrit les étapes nécessaires à l’installation et la configuration de Terraform afin d’approvisionner des ressources telles que des machines virtuelles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8561f-104">This article describes the necessary steps to install and configure Terraform to provision resources such as virtual machines into Azure.</span></span> <span data-ttu-id="8561f-105">Vous allez apprendre à créer et utiliser des informations d’identification Azure pour permettre à Terraform d’approvisionner des ressources cloud de manière sécurisée.</span><span class="sxs-lookup"><span data-stu-id="8561f-105">You will learn how to create and use Azure credentials to enable Terraform to provision cloud resources in a secure manner.</span></span>

<span data-ttu-id="8561f-106">HashiCorp Terraform fournit un moyen simple de définir et déployer l’infrastructure cloud à l’aide d’un langage de création de modèles personnalisé appelé HCL (HashiCorp Configuration Language).</span><span class="sxs-lookup"><span data-stu-id="8561f-106">HashiCorp Terraform provides an easy way to define and deploy cloud infrastructure by using a custom templating language called HashiCorp configuration language (HCL).</span></span> <span data-ttu-id="8561f-107">Ce langage personnalisé est [facile à écrire et facile à comprendre](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="8561f-107">This custom language is [easy to write and easy to understand](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="8561f-108">En outre, à l’aide de la commande `terraform plan`, vous pouvez visualiser les modifications apportées à votre infrastructure avant de les valider.</span><span class="sxs-lookup"><span data-stu-id="8561f-108">Additionally, by using the `terraform plan` command, you can visualize the changes to your infrastructure before you commit them.</span></span> <span data-ttu-id="8561f-109">Suivez ces étapes pour commencer à utiliser Terraform avec Azure.</span><span class="sxs-lookup"><span data-stu-id="8561f-109">Follow these steps to start using Terraform with Azure.</span></span>

## <a name="install-terraform"></a><span data-ttu-id="8561f-110">Installer Terraform</span><span class="sxs-lookup"><span data-stu-id="8561f-110">Install Terraform</span></span>
<span data-ttu-id="8561f-111">Pour installer Terraform, [téléchargez](https://www.terraform.io/downloads.html) le package correspondant à votre système d’exploitation dans un répertoire d’installation distinct.</span><span class="sxs-lookup"><span data-stu-id="8561f-111">To install Terraform, [download](https://www.terraform.io/downloads.html) the package appropriate for your operating system into a separate install directory.</span></span> <span data-ttu-id="8561f-112">Le téléchargement contient un seul fichier exécutable, pour lequel vous devez également définir un chemin d’accès global.</span><span class="sxs-lookup"><span data-stu-id="8561f-112">The download contains a single executable file, for which you should also define a global path.</span></span> <span data-ttu-id="8561f-113">Pour obtenir des instructions sur la définition du chemin d’accès sous Linux et Mac, consultez [cette page web](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span><span class="sxs-lookup"><span data-stu-id="8561f-113">For instructions on how to set the path on Linux and Mac, go to [this webpage](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span></span> <span data-ttu-id="8561f-114">Pour obtenir des instructions sur la définition du chemin d’accès sous Windows, consultez [cette page web](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span><span class="sxs-lookup"><span data-stu-id="8561f-114">For instructions on how to set the path on Windows, go to [this webpage](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span></span> <span data-ttu-id="8561f-115">Pour vérifier votre installation, exécutez la commande `terraform`.</span><span class="sxs-lookup"><span data-stu-id="8561f-115">To verify your installation, run the `terraform` command.</span></span> <span data-ttu-id="8561f-116">Une liste des options Terraform disponibles devrait s’afficher en sortie.</span><span class="sxs-lookup"><span data-stu-id="8561f-116">You should see a list of available Terraform options as output.</span></span>

<span data-ttu-id="8561f-117">Ensuite, vous devez autoriser Terraform à accéder à votre abonnement Azure pour effectuer l’approvisionnement de l’infrastructure.</span><span class="sxs-lookup"><span data-stu-id="8561f-117">Next, you need to allow Terraform access to your Azure subscription to perform infrastructure provisioning.</span></span>

## <a name="set-up-terraform-access-to-azure"></a><span data-ttu-id="8561f-118">Configurer l’accès Terraform à Azure</span><span class="sxs-lookup"><span data-stu-id="8561f-118">Set up Terraform access to Azure</span></span>
<span data-ttu-id="8561f-119">Pour permettre à Terraform d’approvisionner des ressources dans Azure, vous devez créer deux entités dans Azure Active Directory (Azure AD) : une application Azure AD et un principal de service Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8561f-119">To enable Terraform to provision resources into Azure, you need to create two entities in Azure Active Directory (Azure AD): an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="8561f-120">Utilisez ensuite les identificateurs de ces entités dans vos scripts Terraform.</span><span class="sxs-lookup"><span data-stu-id="8561f-120">Then, you use these entities' identifiers in your Terraform scripts.</span></span> <span data-ttu-id="8561f-121">Le principal de service est une instance locale d’application Azure AD globale.</span><span class="sxs-lookup"><span data-stu-id="8561f-121">A service principal is a local instance of a global Azure AD application.</span></span> <span data-ttu-id="8561f-122">Un principal de service permet un contrôle granulaire de l’accès local aux ressources globales.</span><span class="sxs-lookup"><span data-stu-id="8561f-122">A service principal allows granular local access control to global resources.</span></span>

<span data-ttu-id="8561f-123">Il existe plusieurs façons de créer une application Azure AD et un principal de service Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8561f-123">There are several ways to create an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="8561f-124">À l’heure actuelle, le moyen le plus simple et le plus rapide consiste à utiliser Azure CLI 2.0, que [vous pouvez télécharger et installer sur Windows, Linux ou un Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8561f-124">The easiest and fastest way today is to use Azure CLI 2.0, which [you can download and install on Windows, Linux, or a Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="8561f-125">Vous pouvez également utiliser PowerShell ou Azure CLI 1.0 pour créer l’infrastructure de sécurité nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8561f-125">You also can use PowerShell or Azure CLI 1.0 to create the necessary security infrastructure.</span></span> <span data-ttu-id="8561f-126">Les instructions ci-dessous vous montrent comment configurer Terraform pour Azure selon toutes ces approches.</span><span class="sxs-lookup"><span data-stu-id="8561f-126">The instructions that follow show you how to configure Terraform for Azure by using all of these approaches.</span></span>

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a><span data-ttu-id="8561f-127">Utiliser Azure CLI 2.0 (pour les utilisateurs Windows, Linux ou Mac)</span><span class="sxs-lookup"><span data-stu-id="8561f-127">Use Azure CLI 2.0 (for Windows, Linux, or Mac users)</span></span> 
<span data-ttu-id="8561f-128">Après avoir téléchargé et installé [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), connectez-vous afin de gérer votre abonnement Azure en émettant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8561f-128">After you download and install the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), sign in to administer your Azure subscription by issuing the following command:</span></span>

```
az login
```

>[!NOTE]
><span data-ttu-id="8561f-129">Si vous utilisez les clouds Azure Government, Azure - Allemagne ou Azure - Chine, vous devez d’abord configurer Azure CLI pour qu’elle fonctionne avec ce cloud.</span><span class="sxs-lookup"><span data-stu-id="8561f-129">If you use the China, Azure Germany, or Azure Government clouds, you need to first configure the Azure CLI to work with that cloud.</span></span> <span data-ttu-id="8561f-130">Pour ce faire, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8561f-130">You can do this by running the following:</span></span>

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

<span data-ttu-id="8561f-131">Si vous avez plusieurs abonnements Azure, leurs détails sont retournés par la commande `az login`.</span><span class="sxs-lookup"><span data-stu-id="8561f-131">If you have multiple Azure subscriptions, their details are returned by the `az login` command.</span></span> <span data-ttu-id="8561f-132">Définissez la variable d’environnement `SUBSCRIPTION_ID` pour qu’elle contienne la valeur du champ `id` retourné à partir de l’abonnement que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="8561f-132">Set the `SUBSCRIPTION_ID` environment variable to hold the value of the returned `id` field from the subscription you want to use.</span></span> 

<span data-ttu-id="8561f-133">Sélectionnez l’abonnement à utiliser pour cette session.</span><span class="sxs-lookup"><span data-stu-id="8561f-133">Set the subscription that you want to use for this session.</span></span>

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

<span data-ttu-id="8561f-134">Interrogez le compte pour obtenir les valeurs ID d’abonnement et ID locataire.</span><span class="sxs-lookup"><span data-stu-id="8561f-134">Query the account to get the subscription ID and tenant ID values.</span></span>

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

<span data-ttu-id="8561f-135">Créez ensuite des informations d’identification distinctes pour Terraform.</span><span class="sxs-lookup"><span data-stu-id="8561f-135">Next, create separate credentials for Terraform.</span></span>

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

<span data-ttu-id="8561f-136">Les valeurs appId, password, sp_name et tenant sont renvoyées.</span><span class="sxs-lookup"><span data-stu-id="8561f-136">Your appId, password, sp_name, and tenant are returned.</span></span> <span data-ttu-id="8561f-137">Prenez note des valeurs appId et password.</span><span class="sxs-lookup"><span data-stu-id="8561f-137">Make a note of the appId and password.</span></span>

<span data-ttu-id="8561f-138">Pour confirmer vos informations d’identification (principal du service), ouvrez un nouveau shell et exécutez les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="8561f-138">To confirm your credentials (service principal), open a new shell and run the following commands.</span></span> <span data-ttu-id="8561f-139">Remplacez les valeurs renvoyées pour sp_name, password et tenant :</span><span class="sxs-lookup"><span data-stu-id="8561f-139">Substitute the returned values for sp_name, password, and tenant:</span></span>

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a><span data-ttu-id="8561f-140">Utiliser PowerShell (pour les utilisateurs Windows)</span><span class="sxs-lookup"><span data-stu-id="8561f-140">Use PowerShell (for Windows users)</span></span> 
<span data-ttu-id="8561f-141">Pour utiliser un ordinateur Windows pour écrire et exécuter vos scripts Terraform et effectuer les tâches de configuration dans PowerShell, configurez votre machine avec les outils PowerShell appropriés.</span><span class="sxs-lookup"><span data-stu-id="8561f-141">To use a Windows machine to write and execute your Terraform scripts and to use PowerShell for configuration tasks, configure your machine with the right PowerShell tools.</span></span> 

1. <span data-ttu-id="8561f-142">Installez les outils PowerShell en suivant les étapes décrites dans l’article [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps) (Installer et configurer Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="8561f-142">Install PowerShell tools by following the steps in [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> 

2. <span data-ttu-id="8561f-143">Téléchargez et exécutez le script [azure-setup.ps1 script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) à partir de la console PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8561f-143">Download and execute the [azure-setup.ps1 script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) from the PowerShell console.</span></span>

3. <span data-ttu-id="8561f-144">Pour exécuter le script azure-setup.ps1, téléchargez-le et exécutez la commande `./azure-setup.ps1 setup` à partir de la console PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8561f-144">To run the azure-setup.ps1 script, download it and execute the `./azure-setup.ps1 setup` command from the PowerShell console.</span></span> <span data-ttu-id="8561f-145">Connectez-vous ensuite à votre abonnement Azure avec des privilèges Administrateur.</span><span class="sxs-lookup"><span data-stu-id="8561f-145">Then sign in to your Azure subscription with administrative privileges.</span></span>

4. <span data-ttu-id="8561f-146">Indiquez un nom d’application (chaîne arbitraire, requis) lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="8561f-146">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="8561f-147">À l’invite, vous pouvez également indiquer un mot de passe sécurisé.</span><span class="sxs-lookup"><span data-stu-id="8561f-147">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="8561f-148">Si vous ne fournissez pas de mot de passe, le mot de passe sécurisé est automatiquement généré à l’aide des bibliothèques de sécurité .NET.</span><span class="sxs-lookup"><span data-stu-id="8561f-148">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a><span data-ttu-id="8561f-149">Utiliser Azure CLI 1.0 (pour les utilisateurs Linux ou Mac)</span><span class="sxs-lookup"><span data-stu-id="8561f-149">Use Azure CLI 1.0 (for Linux or Mac users)</span></span>
<span data-ttu-id="8561f-150">Pour commencer à utiliser Terraform sur les machines Linux ou Mac avec Azure CLI 1.0, installez les bibliothèques appropriées sur votre machine.</span><span class="sxs-lookup"><span data-stu-id="8561f-150">To get started with Terraform on Linux machines or Macs with Azure CLI 1.0, install the proper libraries on your machine.</span></span>  

1. <span data-ttu-id="8561f-151">Installez les outils d’interface de ligne de commande interplateforme Azure en suivant les étapes décrites dans l’article [Installer Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8561f-151">Install Azure xPlat CLI tools by following the steps in [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

2. <span data-ttu-id="8561f-152">Téléchargez et installez un processeur JSON en suivant les instructions de la page [Download jq](https://stedolan.github.io/jq/download/) (Télécharger jq).</span><span class="sxs-lookup"><span data-stu-id="8561f-152">Download and install a JSON processor by following the instructions in [Download jq](https://stedolan.github.io/jq/download/).</span></span>

3. <span data-ttu-id="8561f-153">Téléchargez et exécutez le script bash [azure-setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) à partir de la console.</span><span class="sxs-lookup"><span data-stu-id="8561f-153">Download and execute the [azure-setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script from the console.</span></span>

4. <span data-ttu-id="8561f-154">Pour exécuter le script azure-setup.sh, téléchargez-le et exécutez la commande `./azure-setup setup` à partir de la console.</span><span class="sxs-lookup"><span data-stu-id="8561f-154">To run the azure-setup.sh script, download it and execute the `./azure-setup setup` command from the console.</span></span> <span data-ttu-id="8561f-155">Connectez-vous ensuite à votre abonnement Azure avec des privilèges Administrateur.</span><span class="sxs-lookup"><span data-stu-id="8561f-155">Then sign in to your Azure subscription with administrative privileges.</span></span>
 
5. <span data-ttu-id="8561f-156">Indiquez un nom d’application (chaîne arbitraire, requis) lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="8561f-156">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="8561f-157">À l’invite, vous pouvez également indiquer un mot de passe sécurisé.</span><span class="sxs-lookup"><span data-stu-id="8561f-157">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="8561f-158">Si vous ne fournissez pas de mot de passe, le mot de passe sécurisé est automatiquement généré à l’aide des bibliothèques de sécurité .NET.</span><span class="sxs-lookup"><span data-stu-id="8561f-158">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

<span data-ttu-id="8561f-159">Tous les scripts précédents créent une application Azure AD et le principal du service.</span><span class="sxs-lookup"><span data-stu-id="8561f-159">All the previous scripts create an Azure AD application and service principal.</span></span> <span data-ttu-id="8561f-160">Le principal du service obtient un accès contributeur ou propriétaire à l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="8561f-160">The service principal gets a contributor or owner-level access on the subscription.</span></span> <span data-ttu-id="8561f-161">En raison du niveau élevé d’accès octroyé, vous devez toujours protéger les informations de sécurité générées par ces scripts.</span><span class="sxs-lookup"><span data-stu-id="8561f-161">Because of the high level of access granted, you should always protect the security information generated by those scripts.</span></span> <span data-ttu-id="8561f-162">Prenez note des quatre éléments d’informations de sécurité fournis par ces scripts : appId, password, subscription_id et tenant_id.</span><span class="sxs-lookup"><span data-stu-id="8561f-162">Make a note of all four pieces of security information provided by those scripts: appId, password, subscription_id, and tenant_id.</span></span>

## <a name="set-environment-variables"></a><span data-ttu-id="8561f-163">Définition des variables d'environnement</span><span class="sxs-lookup"><span data-stu-id="8561f-163">Set environment variables</span></span>
<span data-ttu-id="8561f-164">Après avoir créé et configuré le principal de service Azure AD, vous devez communiquer à Terraform l’ID locataire, l’ID d’abonnement, l’ID client et la clé secrète client à utiliser.</span><span class="sxs-lookup"><span data-stu-id="8561f-164">After you create and configure an Azure AD service principal, you need to let Terraform know the tenant ID, subscription ID, client ID, and client secret to use.</span></span> <span data-ttu-id="8561f-165">Vous pouvez le faire en incorporant ces valeurs dans vos scripts Terraform (comme décrit dans l’article [Créer une infrastructure de base dans Azure à l’aide de Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="8561f-165">You can do it by embedding those values in your Terraform scripts, as described in [Create basic infrastructure by using Terraform](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="8561f-166">Vous pouvez également définir les variables d’environnement suivantes (et ainsi éviter d’archiver ou de partager accidentellement vos informations d’identification) :</span><span class="sxs-lookup"><span data-stu-id="8561f-166">Alternately, you can set the following environment variables (and thus avoid accidentally checking in or sharing your credentials):</span></span>

- <span data-ttu-id="8561f-167">ARM_SUBSCRIPTION_ID</span><span class="sxs-lookup"><span data-stu-id="8561f-167">ARM_SUBSCRIPTION_ID</span></span>
- <span data-ttu-id="8561f-168">ARM_CLIENT_ID</span><span class="sxs-lookup"><span data-stu-id="8561f-168">ARM_CLIENT_ID</span></span>
- <span data-ttu-id="8561f-169">ARM_CLIENT_SECRET</span><span class="sxs-lookup"><span data-stu-id="8561f-169">ARM_CLIENT_SECRET</span></span>
- <span data-ttu-id="8561f-170">ARM_TENANT_ID</span><span class="sxs-lookup"><span data-stu-id="8561f-170">ARM_TENANT_ID</span></span>

<span data-ttu-id="8561f-171">Vous pouvez utiliser cet exemple de script shell pour définir ces variables :</span><span class="sxs-lookup"><span data-stu-id="8561f-171">You can use this sample shell script to set those variables:</span></span>

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

<span data-ttu-id="8561f-172">En outre, si vous utilisez Terraform avec Azure - Chine, Azure Government ou Azure - Allemagne, vous devez définir la variable ENVIRONMENT de façon appropriée.</span><span class="sxs-lookup"><span data-stu-id="8561f-172">Additionally, if you use Terraform with Azure in China or either Azure Government or Azure Germany, you need to set the ENVIRONMENT variable appropriately.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8561f-173">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8561f-173">Next steps</span></span>
<span data-ttu-id="8561f-174">Vous avez installé Terraform et configuré les informations d’identification Azure pour pouvoir démarrer le déploiement d’infrastructure dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="8561f-174">You have now installed Terraform and configured Azure credentials so that you can start deploying infrastructure into your Azure subscription.</span></span> <span data-ttu-id="8561f-175">À présent, découvrez comment [créer une infrastructure avec Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="8561f-175">Next, learn how to [create infrastructure with Terraform](terraform-create-complete-vm.md).</span></span>
