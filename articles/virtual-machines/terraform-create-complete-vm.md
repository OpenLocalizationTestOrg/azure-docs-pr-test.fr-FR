---
title: "infrastructure de base aaaCreate dans Azure à l’aide de Terraform | Documents Microsoft"
description: "Découvrez comment toocreate Azure ressources à l’aide de Terraform"
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
ms.openlocfilehash: 916a838c118f28b3fbd373188e0acb2afc655081
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="037c2-103">Créer une infrastructure de base dans Azure à l’aide de Terraform</span><span class="sxs-lookup"><span data-stu-id="037c2-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="037c2-104">Cet article décrit les étapes de hello vous devez tootake tooprovision une machine virtuelle, ainsi que de l’infrastructure sous-jacente, dans Azure.</span><span class="sxs-lookup"><span data-stu-id="037c2-104">This article describes hello steps you need tootake tooprovision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="037c2-105">Vous allez apprendre comment toowrite Terraform scripts et comment toovisualize hello change avant de vous rendre dans votre infrastructure cloud.</span><span class="sxs-lookup"><span data-stu-id="037c2-105">You will learn how toowrite Terraform scripts and how toovisualize hello changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="037c2-106">Vous allez également apprendre comment infrastructure toocreate dans Azure à l’aide de Terraform.</span><span class="sxs-lookup"><span data-stu-id="037c2-106">You also will learn how toocreate infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="037c2-107">tooget démarré, créez un fichier appelé \terraform_azure101.tf dans votre éditeur de texte de choix (Visual Studio Code/Sublime/Vim/etc.).</span><span class="sxs-lookup"><span data-stu-id="037c2-107">tooget started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="037c2-108">nom exact de Hello du fichier de hello n’est pas important, car Terraform accepte le nom du dossier hello en tant que paramètre : tous les scripts dans le dossier de hello sont exécutées.</span><span class="sxs-lookup"><span data-stu-id="037c2-108">hello exact name of hello file isn't important because Terraform accepts hello folder name as a parameter: all scripts in hello folder get executed.</span></span> <span data-ttu-id="037c2-109">Collez hello suivant de code dans un fichier nouveau hello :</span><span class="sxs-lookup"><span data-stu-id="037c2-109">Paste hello following code in hello new file:</span></span>

~~~~
# Configure hello Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have tooinclude this block
provider "azurerm" {
  subscription_id = "your_subscription_id_from_script_execution"
  client_id       = "your_appId_from_script_execution"
  client_secret   = "your_password_from_script_execution"
  tenant_id       = "your_tenant_id_from_script_execution"
}

# create a resource group 
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}
~~~~
<span data-ttu-id="037c2-110">Bonjour `provider` section Hello de script, vous indiquez à Terraform toouse une ressources tooprovision de fournisseur Azure dans le script de hello.</span><span class="sxs-lookup"><span data-stu-id="037c2-110">In hello `provider` section of hello script, you tell Terraform toouse an Azure provider tooprovision resources in hello script.</span></span> <span data-ttu-id="037c2-111">tooget valeurs ID_ABONNEMENT, appId, mot de passe et tenant_id, consultez hello [installer et configurer Terraform](terraform-install-configure.md) guide.</span><span class="sxs-lookup"><span data-stu-id="037c2-111">tooget values for subscription_id, appId, password, and tenant_id, see hello [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="037c2-112">Si vous avez créé des variables d’environnement pour les valeurs hello dans ce bloc, vous n’avez pas besoin de tooinclude il.</span><span class="sxs-lookup"><span data-stu-id="037c2-112">If you have created environment variables for hello values in this block, you don't need tooinclude it.</span></span> 

<span data-ttu-id="037c2-113">Hello `azurerm_resource_group` ressource indique Terraform toocreate un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="037c2-113">hello `azurerm_resource_group` resource instructs Terraform toocreate a new resource group.</span></span> <span data-ttu-id="037c2-114">Vous trouverez d’autres types de ressources disponibles dans Terraform plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="037c2-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-hello-script"></a><span data-ttu-id="037c2-115">Exécuter le script de hello</span><span class="sxs-lookup"><span data-stu-id="037c2-115">Execute hello script</span></span>
<span data-ttu-id="037c2-116">Après avoir enregistré le script de hello, quittez la ligne de commande de la console toohello et tapez Bonjour suivante :</span><span class="sxs-lookup"><span data-stu-id="037c2-116">After you save hello script, exit toohello console/command line, and type hello following:</span></span>
```
terraform init
```
<span data-ttu-id="037c2-117">fournisseur de Terraform tooinitialize pour Azure.</span><span class="sxs-lookup"><span data-stu-id="037c2-117">tooinitialize Terraform provider for Azure.</span></span> <span data-ttu-id="037c2-118">Puis tapez ce qui suit hello :</span><span class="sxs-lookup"><span data-stu-id="037c2-118">Then type hello following:</span></span>
```
terraform plan terraformscripts
```
<span data-ttu-id="037c2-119">Nous supposons que `terraformscripts` est le dossier hello où le script de hello a été enregistré.</span><span class="sxs-lookup"><span data-stu-id="037c2-119">We assume that `terraformscripts` is hello folder where hello script was saved.</span></span> <span data-ttu-id="037c2-120">Nous avons utilisé hello `plan` commande Terraform, qui examine les ressources hello définies dans les scripts de hello.</span><span class="sxs-lookup"><span data-stu-id="037c2-120">We used hello `plan` Terraform command, which looks at hello resources defined in hello scripts.</span></span> <span data-ttu-id="037c2-121">Il compare les toohello les informations d’état enregistrées par Terraform et puis sorties hello planifié l’exécution _sans_ créez en fait des ressources dans Azure.</span><span class="sxs-lookup"><span data-stu-id="037c2-121">It compares them toohello state information saved by Terraform and then outputs hello planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="037c2-122">Une fois que vous exécutez la commande précédente hello, vous devez voir quelque chose comme hello suivant d’écran :</span><span class="sxs-lookup"><span data-stu-id="037c2-122">After you execute hello previous command, you should see something like hello following screen:</span></span>

![plan Terraform](linux/media/terraform/tf_plan2.png)

<span data-ttu-id="037c2-124">Si tout semble correct, configurez ce nouveau groupe de ressources dans Azure en exécutant hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="037c2-124">If everything looks correct, provision this new resource group in Azure by executing hello following:</span></span> 
```
terraform apply terraformscripts
```
<span data-ttu-id="037c2-125">Bonjour portail Azure, vous devez voir le nouveau groupe de ressources vide hello appelé `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="037c2-125">In hello Azure portal, you should see hello new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="037c2-126">Bonjour suivant la section, vous ajoutez qu'une machine virtuelle et tous les hello infrastructure de prise en charge pour ce groupe de ressources d’ordinateur virtuel toohello.</span><span class="sxs-lookup"><span data-stu-id="037c2-126">In hello following section, you add a virtual machine and all hello supporting infrastructure for that virtual machine toohello resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="037c2-127">Approvisionner une machine virtuelle Ubuntu avec Terraform</span><span class="sxs-lookup"><span data-stu-id="037c2-127">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="037c2-128">Nous allons étendre script de Terraform hello qu'avec les détails de hello tooprovision nécessaire, nous avons créé une machine virtuelle exécutant Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="037c2-128">Let's extend hello Terraform script we've created with hello details that are necessary tooprovision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="037c2-129">ressources Hello que vous préparez dans les sections suivantes de hello sont :</span><span class="sxs-lookup"><span data-stu-id="037c2-129">hello resources that you provision in hello following sections are:</span></span>

* <span data-ttu-id="037c2-130">Un réseau avec un sous-réseau unique</span><span class="sxs-lookup"><span data-stu-id="037c2-130">A network with a single subnet</span></span>
* <span data-ttu-id="037c2-131">Une carte d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="037c2-131">A network interface card</span></span> 
* <span data-ttu-id="037c2-132">Un compte de stockage avec un conteneur de stockage</span><span class="sxs-lookup"><span data-stu-id="037c2-132">A storage account with a storage container</span></span>
* <span data-ttu-id="037c2-133">Une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="037c2-133">A public IP</span></span>
* <span data-ttu-id="037c2-134">Un ordinateur virtuel qui utilise toutes les ressources précédentes hello</span><span class="sxs-lookup"><span data-stu-id="037c2-134">A virtual machine that utilizes all hello previous resources</span></span> 

<span data-ttu-id="037c2-135">Pour obtenir une documentation complète pour chacune des ressources d’Azure Terraform hello, consultez hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="037c2-135">For thorough documentation for each of hello Azure Terraform resources, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="037c2-136">version complète de Hello Hello [script de configuration](#complete-terraform-script) est également fournie pour des raisons de commodité.</span><span class="sxs-lookup"><span data-stu-id="037c2-136">hello full version of hello [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-hello-terraform-script"></a><span data-ttu-id="037c2-137">Étendre le script de Terraform hello</span><span class="sxs-lookup"><span data-stu-id="037c2-137">Extend hello Terraform script</span></span>
<span data-ttu-id="037c2-138">Étendre le script hello qui a été créé avec hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="037c2-138">Extend hello script that was created with hello following resources:</span></span> 
~~~~
# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}
~~~~
<span data-ttu-id="037c2-139">Hello le script précédent crée un réseau virtuel et un sous-réseau au sein de ce réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="037c2-139">hello previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="037c2-140">Notez le groupe de ressources hello référence toohello que vous avez déjà créé via « ${azurerm_resource_group.helloterraform.name} » dans le réseau virtuel de hello et définition de sous-réseau hello.</span><span class="sxs-lookup"><span data-stu-id="037c2-140">Note hello reference toohello resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both hello virtual network and hello subnet definition.</span></span>

~~~~
# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "TerraformDemo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }
}
~~~~
<span data-ttu-id="037c2-141">extraits de code de script précédent Hello créer une adresse IP publique et une interface réseau qui utilise des adresses IP publiques hello créé.</span><span class="sxs-lookup"><span data-stu-id="037c2-141">hello previous script snippets create a public IP and a network interface that makes use of hello public IP created.</span></span> <span data-ttu-id="037c2-142">Remarque hello références toosubnet_id et public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="037c2-142">Note hello references toosubnet_id and public_ip_address_id.</span></span> <span data-ttu-id="037c2-143">Terraform a intelligence intégrée toounderstand que hello interface réseau a une dépendance sur les ressources de hello que toobe besoin créé avant la création de l’interface de réseau hello hello.</span><span class="sxs-lookup"><span data-stu-id="037c2-143">Terraform has built-in intelligence toounderstand that hello network interface has a dependency on hello resources that need toobe created before hello creation of hello network interface.</span></span>

~~~~
# create a random id
resource "random_id" "randomId" {
  byte_length = 4
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "tfstorage${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "westus"
    account_type = "Standard_LRS"

    tags {
        environment = "staging"
    }
}

# create storage container
resource "azurerm_storage_container" "helloterraformstoragestoragecontainer" {
    name = "vhd"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    storage_account_name = "${azurerm_storage_account.helloterraformstorage.name}"
    container_access_type = "private"
    depends_on = ["azurerm_storage_account.helloterraformstorage"]
}
~~~~
<span data-ttu-id="037c2-144">Ici, vous avez créé un compte de stockage et y avez défini un conteneur de stockage.</span><span class="sxs-lookup"><span data-stu-id="037c2-144">Here, you created a storage account and defined a storage container within that storage account.</span></span> <span data-ttu-id="037c2-145">Ce compte de stockage est où vous stockez des disques durs virtuels (VHD) pour la machine virtuelle de hello sur toobe créé.</span><span class="sxs-lookup"><span data-stu-id="037c2-145">This storage account is where you store virtual hard disks (VHDs) for hello virtual machine about toobe created.</span></span>

~~~~
# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_A0"

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "14.04.2-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        vhd_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}${azurerm_storage_container.helloterraformstoragestoragecontainer.name}/myosdisk.vhd"
        caching = "ReadWrite"
        create_option = "FromImage"
    }

    os_profile {
        computer_name = "hostname"
        admin_username = "testadmin"
        admin_password = "Password1234!"
    }

    os_profile_linux_config {
        disable_password_authentication = false
    }

    tags {
        environment = "staging"
    }
}
~~~~
<span data-ttu-id="037c2-146">Enfin, extrait de code hello précédente crée un ordinateur virtuel qui utilise toutes les ressources hello configurés déjà.</span><span class="sxs-lookup"><span data-stu-id="037c2-146">Finally, hello previous snippet creates a virtual machine that utilizes all hello resources provisioned already.</span></span> <span data-ttu-id="037c2-147">Ils sont un compte de stockage et un conteneur pour un disque dur virtuel, une interface réseau avec publique IP et le sous-réseau spécifié, et le groupe de ressources hello déjà créé.</span><span class="sxs-lookup"><span data-stu-id="037c2-147">They are a storage account and container for a VHD, a network interface with public IP and subnet specified, and hello resource group you already created.</span></span> <span data-ttu-id="037c2-148">Notez la propriété de vm_size hello, où le script de hello spécifie une référence (SKU) A0 de Azure.</span><span class="sxs-lookup"><span data-stu-id="037c2-148">Note hello vm_size property, where hello script specifies an Azure A0 SKU.</span></span>

### <a name="execute-hello-script"></a><span data-ttu-id="037c2-149">Exécuter le script de hello</span><span class="sxs-lookup"><span data-stu-id="037c2-149">Execute hello script</span></span>
<span data-ttu-id="037c2-150">Avec le script complet hello enregistré quitter la ligne de commande de la console toohello et tapez Bonjour suivant :</span><span class="sxs-lookup"><span data-stu-id="037c2-150">With hello full script saved, exit toohello console/command line and type hello following:</span></span>
```
terraform apply terraformscripts
```
<span data-ttu-id="037c2-151">Après un certain temps, hello ressources, y compris un ordinateur virtuel, s’affichent dans hello `terraformtest` groupe de ressources dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="037c2-151">After some time, hello resources, including a virtual machine, appear in hello `terraformtest` resource group in hello Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="037c2-152">Script Terraform complet</span><span class="sxs-lookup"><span data-stu-id="037c2-152">Complete Terraform script</span></span>

<span data-ttu-id="037c2-153">Pour votre commodité, voici complète du script Terraform hello qui configure de hello infrastructure abordé dans cet article.</span><span class="sxs-lookup"><span data-stu-id="037c2-153">For your convenience, below is hello complete Terraform script that provisions all of hello infrastructure discussed in this article.</span></span>

```
variable "resourcesname" {
  default = "helloterraform"
}

# Configure hello Microsoft Azure Provider
provider "azurerm" {
  subscription_id = "XXX"
  client_id       = "XXX"
  client_secret   = "XXX"
  tenant_id       = "XXX"
}

# create a resource group if it doesn't exist
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}

# create virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "tfvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "tfsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}


# create public IPs
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "TerraformDemo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }
}

# create a random id
resource "random_id" "randomId" {
  byte_length = 4
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "tfstorage${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "westus"
    account_type = "Standard_LRS"

    tags {
        environment = "staging"
    }
}

# create storage container
resource "azurerm_storage_container" "helloterraformstoragestoragecontainer" {
    name = "vhd"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    storage_account_name = "${azurerm_storage_account.helloterraformstorage.name}"
    container_access_type = "private"
    depends_on = ["azurerm_storage_account.helloterraformstorage"]
}

# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_A0"

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "14.04.2-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        vhd_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}${azurerm_storage_container.helloterraformstoragestoragecontainer.name}/myosdisk.vhd"
        caching = "ReadWrite"
        create_option = "FromImage"
    }

    os_profile {
        computer_name = "hostname"
        admin_username = "testadmin"
        admin_password = "Password1234!"
    }

    os_profile_linux_config {
        disable_password_authentication = false
    }

    tags {
        environment = "staging"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="037c2-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="037c2-154">Next steps</span></span>
<span data-ttu-id="037c2-155">Vous avez créé une infrastructure de base dans Azure à l’aide de Terraform.</span><span class="sxs-lookup"><span data-stu-id="037c2-155">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="037c2-156">Pour des scénarios plus complexes, y compris des exemples utilisant des équilibreurs de charge et des groupes de machines virtuelles identiques, consultez les nombreux [exemples Terraform pour Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="037c2-156">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="037c2-157">Pour obtenir une liste actualisée des fournisseurs Azure pris en charge, consultez hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="037c2-157">For an up-to-date list of supported Azure providers, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
