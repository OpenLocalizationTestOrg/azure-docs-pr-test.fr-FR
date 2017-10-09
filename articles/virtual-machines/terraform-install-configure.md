---
title: aaaInstall et configurer des machines virtuelles de tooprovision Terraform et une autre infrastructure dans Azure | Documents Microsoft
description: "Découvrez comment tooinstall et configurer Terraform toocreate Azure ressources"
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
ms.openlocfilehash: 803f51a6f5357417b96264ba713791408f9935b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-terraform-tooprovision-vms-and-other-infrastructure-into-azure"></a><span data-ttu-id="f4219-103">Installer et configurer des machines virtuelles de tooprovision Terraform et une autre infrastructure dans Azure</span><span class="sxs-lookup"><span data-stu-id="f4219-103">Install and configure Terraform tooprovision VMs and other infrastructure into Azure</span></span> 
<span data-ttu-id="f4219-104">Cet article décrit les hello étapes nécessaires tooinstall et configurer les ressources de tooprovision Terraform tels que des machines virtuelles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f4219-104">This article describes hello necessary steps tooinstall and configure Terraform tooprovision resources such as virtual machines into Azure.</span></span> <span data-ttu-id="f4219-105">Vous allez apprendre comment toocreate et utilisez Azure les informations d’identification tooenable Terraform tooprovision des ressources de cloud de manière sécurisée.</span><span class="sxs-lookup"><span data-stu-id="f4219-105">You will learn how toocreate and use Azure credentials tooenable Terraform tooprovision cloud resources in a secure manner.</span></span>

<span data-ttu-id="f4219-106">HashiCorp Terraform fournit un moyen simple de toodefine et déployer l’infrastructure cloud à l’aide d’un langage de création de modèles personnalisé appelé langage de configuration HashiCorp (HCL).</span><span class="sxs-lookup"><span data-stu-id="f4219-106">HashiCorp Terraform provides an easy way toodefine and deploy cloud infrastructure by using a custom templating language called HashiCorp configuration language (HCL).</span></span> <span data-ttu-id="f4219-107">Ce langage personnalisé est [toowrite simple et facile toounderstand](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="f4219-107">This custom language is [easy toowrite and easy toounderstand](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="f4219-108">En outre, à l’aide de hello `terraform plan` de commande, vous pouvez visualiser les infrastructures de tooyour hello modifications avant de les valider.</span><span class="sxs-lookup"><span data-stu-id="f4219-108">Additionally, by using hello `terraform plan` command, you can visualize hello changes tooyour infrastructure before you commit them.</span></span> <span data-ttu-id="f4219-109">Suivez ces toostart étapes à l’aide de Terraform avec Azure.</span><span class="sxs-lookup"><span data-stu-id="f4219-109">Follow these steps toostart using Terraform with Azure.</span></span>

## <a name="install-terraform"></a><span data-ttu-id="f4219-110">Installer Terraform</span><span class="sxs-lookup"><span data-stu-id="f4219-110">Install Terraform</span></span>
<span data-ttu-id="f4219-111">tooinstall Terraform, [télécharger](https://www.terraform.io/downloads.html) package hello appropriée pour votre système d’exploitation dans un répertoire d’installation distincts.</span><span class="sxs-lookup"><span data-stu-id="f4219-111">tooinstall Terraform, [download](https://www.terraform.io/downloads.html) hello package appropriate for your operating system into a separate install directory.</span></span> <span data-ttu-id="f4219-112">Hello contient un seul fichier exécutable pour lequel vous devez également définir un chemin d’accès globale.</span><span class="sxs-lookup"><span data-stu-id="f4219-112">hello download contains a single executable file, for which you should also define a global path.</span></span> <span data-ttu-id="f4219-113">Pour obtenir des instructions sur la façon dont tooset hello chemin d’accès sur Linux et Mac, accédez trop[cette page Web](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span><span class="sxs-lookup"><span data-stu-id="f4219-113">For instructions on how tooset hello path on Linux and Mac, go too[this webpage](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span></span> <span data-ttu-id="f4219-114">Pour obtenir des instructions sur comment tooset hello chemin d’accès sur Windows, accédez trop[cette page Web](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span><span class="sxs-lookup"><span data-stu-id="f4219-114">For instructions on how tooset hello path on Windows, go too[this webpage](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span></span> <span data-ttu-id="f4219-115">tooverify votre installation, exécutez hello `terraform` commande.</span><span class="sxs-lookup"><span data-stu-id="f4219-115">tooverify your installation, run hello `terraform` command.</span></span> <span data-ttu-id="f4219-116">Une liste des options Terraform disponibles devrait s’afficher en sortie.</span><span class="sxs-lookup"><span data-stu-id="f4219-116">You should see a list of available Terraform options as output.</span></span>

<span data-ttu-id="f4219-117">Ensuite, vous devez tooallow Terraform accès tooyour abonnement Azure tooperform infrastructure de configuration.</span><span class="sxs-lookup"><span data-stu-id="f4219-117">Next, you need tooallow Terraform access tooyour Azure subscription tooperform infrastructure provisioning.</span></span>

## <a name="set-up-terraform-access-tooazure"></a><span data-ttu-id="f4219-118">Configurer Terraform accès tooAzure</span><span class="sxs-lookup"><span data-stu-id="f4219-118">Set up Terraform access tooAzure</span></span>
<span data-ttu-id="f4219-119">tooenable Terraform tooprovision des ressources dans Azure, vous devez toocreate deux entités dans Azure Active Directory (Azure AD) : une application Azure AD et un principal du service Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4219-119">tooenable Terraform tooprovision resources into Azure, you need toocreate two entities in Azure Active Directory (Azure AD): an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="f4219-120">Utilisez ensuite les identificateurs de ces entités dans vos scripts Terraform.</span><span class="sxs-lookup"><span data-stu-id="f4219-120">Then, you use these entities' identifiers in your Terraform scripts.</span></span> <span data-ttu-id="f4219-121">Le principal de service est une instance locale d’application Azure AD globale.</span><span class="sxs-lookup"><span data-stu-id="f4219-121">A service principal is a local instance of a global Azure AD application.</span></span> <span data-ttu-id="f4219-122">Un principal de service permet de ressources de tooglobal contrôle granulaire de l’accès local.</span><span class="sxs-lookup"><span data-stu-id="f4219-122">A service principal allows granular local access control tooglobal resources.</span></span>

<span data-ttu-id="f4219-123">Il existe plusieurs façons toocreate une application Azure AD et un principal du service Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4219-123">There are several ways toocreate an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="f4219-124">Hello plus facile et plus rapide est façon aujourd'hui toouse Azure CLI 2.0, lequel [vous pouvez télécharger et installer sur un Mac, Linux ou Windows](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f4219-124">hello easiest and fastest way today is toouse Azure CLI 2.0, which [you can download and install on Windows, Linux, or a Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="f4219-125">Vous pouvez également utiliser l’infrastructure de sécurité nécessaires de hello toocreate PowerShell ou CLI Azure version 1.0.</span><span class="sxs-lookup"><span data-stu-id="f4219-125">You also can use PowerShell or Azure CLI 1.0 toocreate hello necessary security infrastructure.</span></span> <span data-ttu-id="f4219-126">Hello les instructions qui suivent montrent comment tooconfigure Terraform pour Azure à l’aide de toutes ces approches.</span><span class="sxs-lookup"><span data-stu-id="f4219-126">hello instructions that follow show you how tooconfigure Terraform for Azure by using all of these approaches.</span></span>

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a><span data-ttu-id="f4219-127">Utiliser Azure CLI 2.0 (pour les utilisateurs Windows, Linux ou Mac)</span><span class="sxs-lookup"><span data-stu-id="f4219-127">Use Azure CLI 2.0 (for Windows, Linux, or Mac users)</span></span> 
<span data-ttu-id="f4219-128">Une fois que vous téléchargez et installez hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), connectez-vous tooadminister votre abonnement Azure en émettant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f4219-128">After you download and install hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), sign in tooadminister your Azure subscription by issuing hello following command:</span></span>

```
az login
```

>[!NOTE]
><span data-ttu-id="f4219-129">Si vous utilisez hello Chine, Azure situés en Allemagne ou les clouds Azure Government, vous devez toofirst configurer hello CLI d’Azure toowork avec ce cloud.</span><span class="sxs-lookup"><span data-stu-id="f4219-129">If you use hello China, Azure Germany, or Azure Government clouds, you need toofirst configure hello Azure CLI toowork with that cloud.</span></span> <span data-ttu-id="f4219-130">Pour cela, vous pouvez exécutant hello suivante :</span><span class="sxs-lookup"><span data-stu-id="f4219-130">You can do this by running hello following:</span></span>

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

<span data-ttu-id="f4219-131">Si vous avez plusieurs abonnements Azure, leurs détails sont retournés par hello `az login` commande.</span><span class="sxs-lookup"><span data-stu-id="f4219-131">If you have multiple Azure subscriptions, their details are returned by hello `az login` command.</span></span> <span data-ttu-id="f4219-132">Ensemble hello `SUBSCRIPTION_ID` environnement hello toohold variable la valeur hello retournée `id` champ d’abonnement de hello souhaité toouse.</span><span class="sxs-lookup"><span data-stu-id="f4219-132">Set hello `SUBSCRIPTION_ID` environment variable toohold hello value of hello returned `id` field from hello subscription you want toouse.</span></span> 

<span data-ttu-id="f4219-133">Définir l’abonnement hello que vous souhaitez toouse pour cette session.</span><span class="sxs-lookup"><span data-stu-id="f4219-133">Set hello subscription that you want toouse for this session.</span></span>

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

<span data-ttu-id="f4219-134">ID d’abonnement hello hello compte tooget de requête et valeurs d’ID de client.</span><span class="sxs-lookup"><span data-stu-id="f4219-134">Query hello account tooget hello subscription ID and tenant ID values.</span></span>

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

<span data-ttu-id="f4219-135">Créez ensuite des informations d’identification distinctes pour Terraform.</span><span class="sxs-lookup"><span data-stu-id="f4219-135">Next, create separate credentials for Terraform.</span></span>

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

<span data-ttu-id="f4219-136">Les valeurs appId, password, sp_name et tenant sont renvoyées.</span><span class="sxs-lookup"><span data-stu-id="f4219-136">Your appId, password, sp_name, and tenant are returned.</span></span> <span data-ttu-id="f4219-137">Prenez note de hello appId et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="f4219-137">Make a note of hello appId and password.</span></span>

<span data-ttu-id="f4219-138">tooconfirm vos informations d’identification (principal du service), ouvrez un nouvel interpréteur de commandes et exécutez hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="f4219-138">tooconfirm your credentials (service principal), open a new shell and run hello following commands.</span></span> <span data-ttu-id="f4219-139">Hello substitut retourné valeurs sp_name, mot de passe et client :</span><span class="sxs-lookup"><span data-stu-id="f4219-139">Substitute hello returned values for sp_name, password, and tenant:</span></span>

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a><span data-ttu-id="f4219-140">Utiliser PowerShell (pour les utilisateurs Windows)</span><span class="sxs-lookup"><span data-stu-id="f4219-140">Use PowerShell (for Windows users)</span></span> 
<span data-ttu-id="f4219-141">toouse Windows toowrite de l’ordinateur et exécuter votre Terraform scripts et toouse PowerShell pour les tâches de configuration, configurer votre ordinateur avec les outils PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="f4219-141">toouse a Windows machine toowrite and execute your Terraform scripts and toouse PowerShell for configuration tasks, configure your machine with hello right PowerShell tools.</span></span> 

1. <span data-ttu-id="f4219-142">Installer les outils PowerShell en suivant les étapes de hello dans [installer et configurer Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="f4219-142">Install PowerShell tools by following hello steps in [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> 

2. <span data-ttu-id="f4219-143">Télécharger et exécuter hello [azure-setup.ps1 script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) à partir de la console PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="f4219-143">Download and execute hello [azure-setup.ps1 script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) from hello PowerShell console.</span></span>

3. <span data-ttu-id="f4219-144">script d’azure-setup.ps1 toorun hello, télécharger et exécuter hello `./azure-setup.ps1 setup` commande à partir de la console PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="f4219-144">toorun hello azure-setup.ps1 script, download it and execute hello `./azure-setup.ps1 setup` command from hello PowerShell console.</span></span> <span data-ttu-id="f4219-145">Connectez-vous ensuite tooyour abonnement Azure avec des privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f4219-145">Then sign in tooyour Azure subscription with administrative privileges.</span></span>

4. <span data-ttu-id="f4219-146">Indiquez un nom d’application (chaîne arbitraire, requis) lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="f4219-146">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="f4219-147">À l’invite, vous pouvez également indiquer un mot de passe sécurisé.</span><span class="sxs-lookup"><span data-stu-id="f4219-147">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="f4219-148">Si vous ne fournissez pas de mot de passe, le mot de passe sécurisé est automatiquement généré à l’aide des bibliothèques de sécurité .NET.</span><span class="sxs-lookup"><span data-stu-id="f4219-148">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a><span data-ttu-id="f4219-149">Utiliser Azure CLI 1.0 (pour les utilisateurs Linux ou Mac)</span><span class="sxs-lookup"><span data-stu-id="f4219-149">Use Azure CLI 1.0 (for Linux or Mac users)</span></span>
<span data-ttu-id="f4219-150">tooget main Terraform sur les ordinateurs Linux ou Mac avec Azure CLI 1.0, installer les bibliothèques hello approprié sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f4219-150">tooget started with Terraform on Linux machines or Macs with Azure CLI 1.0, install hello proper libraries on your machine.</span></span>  

1. <span data-ttu-id="f4219-151">Installer les outils CLI xPlat Azure en suivant les étapes de hello dans [installer Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f4219-151">Install Azure xPlat CLI tools by following hello steps in [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

2. <span data-ttu-id="f4219-152">Téléchargez et installez un processeur JSON en suivant les instructions de hello dans [télécharger jq](https://stedolan.github.io/jq/download/).</span><span class="sxs-lookup"><span data-stu-id="f4219-152">Download and install a JSON processor by following hello instructions in [Download jq](https://stedolan.github.io/jq/download/).</span></span>

3. <span data-ttu-id="f4219-153">Télécharger et exécuter hello [azure-setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script à partir de la console de hello.</span><span class="sxs-lookup"><span data-stu-id="f4219-153">Download and execute hello [azure-setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script from hello console.</span></span>

4. <span data-ttu-id="f4219-154">script d’azure-setup.sh toorun hello, télécharger et exécuter hello `./azure-setup setup` commande à partir de la console de hello.</span><span class="sxs-lookup"><span data-stu-id="f4219-154">toorun hello azure-setup.sh script, download it and execute hello `./azure-setup setup` command from hello console.</span></span> <span data-ttu-id="f4219-155">Connectez-vous ensuite tooyour abonnement Azure avec des privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f4219-155">Then sign in tooyour Azure subscription with administrative privileges.</span></span>
 
5. <span data-ttu-id="f4219-156">Indiquez un nom d’application (chaîne arbitraire, requis) lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="f4219-156">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="f4219-157">À l’invite, vous pouvez également indiquer un mot de passe sécurisé.</span><span class="sxs-lookup"><span data-stu-id="f4219-157">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="f4219-158">Si vous ne fournissez pas de mot de passe, le mot de passe sécurisé est automatiquement généré à l’aide des bibliothèques de sécurité .NET.</span><span class="sxs-lookup"><span data-stu-id="f4219-158">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

<span data-ttu-id="f4219-159">Tous les scripts précédents hello créent une application Azure AD et le service principal.</span><span class="sxs-lookup"><span data-stu-id="f4219-159">All hello previous scripts create an Azure AD application and service principal.</span></span> <span data-ttu-id="f4219-160">principal du service Hello obtienne un contributeur ou l’accès au niveau du propriétaire d’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="f4219-160">hello service principal gets a contributor or owner-level access on hello subscription.</span></span> <span data-ttu-id="f4219-161">En raison de hello haut niveau d’accès accordé, vous devez toujours protéger les informations de sécurité hello générées par ces scripts.</span><span class="sxs-lookup"><span data-stu-id="f4219-161">Because of hello high level of access granted, you should always protect hello security information generated by those scripts.</span></span> <span data-ttu-id="f4219-162">Prenez note des quatre éléments d’informations de sécurité fournis par ces scripts : appId, password, subscription_id et tenant_id.</span><span class="sxs-lookup"><span data-stu-id="f4219-162">Make a note of all four pieces of security information provided by those scripts: appId, password, subscription_id, and tenant_id.</span></span>

## <a name="set-environment-variables"></a><span data-ttu-id="f4219-163">Définition des variables d'environnement</span><span class="sxs-lookup"><span data-stu-id="f4219-163">Set environment variables</span></span>
<span data-ttu-id="f4219-164">Une fois que vous créez et configurez un principal du service Azure AD, vous devez toolet Terraform connaître hello client ID, ID d’abonnement, ID de client et toouse secrète du client.</span><span class="sxs-lookup"><span data-stu-id="f4219-164">After you create and configure an Azure AD service principal, you need toolet Terraform know hello tenant ID, subscription ID, client ID, and client secret toouse.</span></span> <span data-ttu-id="f4219-165">Vous pouvez le faire en incorporant ces valeurs dans vos scripts Terraform (comme décrit dans l’article [Créer une infrastructure de base dans Azure à l’aide de Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="f4219-165">You can do it by embedding those values in your Terraform scripts, as described in [Create basic infrastructure by using Terraform](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="f4219-166">Ou bien, vous pouvez définir hello suivant des variables d’environnement (et par conséquent éviter accidentellement archivage ou le partage de vos informations d’identification) :</span><span class="sxs-lookup"><span data-stu-id="f4219-166">Alternately, you can set hello following environment variables (and thus avoid accidentally checking in or sharing your credentials):</span></span>

- <span data-ttu-id="f4219-167">ARM_SUBSCRIPTION_ID</span><span class="sxs-lookup"><span data-stu-id="f4219-167">ARM_SUBSCRIPTION_ID</span></span>
- <span data-ttu-id="f4219-168">ARM_CLIENT_ID</span><span class="sxs-lookup"><span data-stu-id="f4219-168">ARM_CLIENT_ID</span></span>
- <span data-ttu-id="f4219-169">ARM_CLIENT_SECRET</span><span class="sxs-lookup"><span data-stu-id="f4219-169">ARM_CLIENT_SECRET</span></span>
- <span data-ttu-id="f4219-170">ARM_TENANT_ID</span><span class="sxs-lookup"><span data-stu-id="f4219-170">ARM_TENANT_ID</span></span>

<span data-ttu-id="f4219-171">Ces variables, vous pouvez utiliser cette tooset de script de shell exemple :</span><span class="sxs-lookup"><span data-stu-id="f4219-171">You can use this sample shell script tooset those variables:</span></span>

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

<span data-ttu-id="f4219-172">En outre, si vous utilisez Terraform avec Azure en Chine ou soit Azure Government ou Allemagne d’Azure, vous devez correctement variable d’environnement tooset hello.</span><span class="sxs-lookup"><span data-stu-id="f4219-172">Additionally, if you use Terraform with Azure in China or either Azure Government or Azure Germany, you need tooset hello environment variable appropriately.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4219-173">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f4219-173">Next steps</span></span>
<span data-ttu-id="f4219-174">Vous avez installé Terraform et configuré les informations d’identification Azure pour pouvoir démarrer le déploiement d’infrastructure dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f4219-174">You have now installed Terraform and configured Azure credentials so that you can start deploying infrastructure into your Azure subscription.</span></span> <span data-ttu-id="f4219-175">Ensuite, découvrez comment trop[créer l’infrastructure avec Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="f4219-175">Next, learn how too[create infrastructure with Terraform](terraform-create-complete-vm.md).</span></span>
