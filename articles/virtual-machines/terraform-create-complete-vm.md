---
title: "Créer une infrastructure de base dans Azure à l’aide de Terraform | Microsoft Docs"
description: "Découvrez comment créer des ressources Azure à l’aide de Terraform"
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
ms.openlocfilehash: 9660a95b440c2e4311829979e270d9f10099f624
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="295cc-103">Créer une infrastructure de base dans Azure à l’aide de Terraform</span><span class="sxs-lookup"><span data-stu-id="295cc-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="295cc-104">Cet article décrit les étapes nécessaires pour configurer une machine virtuelle, ainsi que l’infrastructure sous-jacente, dans Azure.</span><span class="sxs-lookup"><span data-stu-id="295cc-104">This article describes the steps you need to take to provision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="295cc-105">Vous allez apprendre à rédiger des scripts Terraform et à visualiser les modifications avant de les ajouter à votre infrastructure cloud.</span><span class="sxs-lookup"><span data-stu-id="295cc-105">You will learn how to write Terraform scripts and how to visualize the changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="295cc-106">Vous allez également apprendre à créer une infrastructure dans Azure à l’aide de Terraform.</span><span class="sxs-lookup"><span data-stu-id="295cc-106">You also will learn how to create infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="295cc-107">Pour commencer, créez un fichier appelé \terraform_azure101.tf dans l’éditeur de texte de votre choix (Visual Studio Code/Sublime/Vim/etc.).</span><span class="sxs-lookup"><span data-stu-id="295cc-107">To get started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="295cc-108">Le nom exact du fichier n’est pas important, étant donné que Terraform accepte le nom du dossier en tant que paramètre : tous les scripts contenus dans le dossier sont exécutés.</span><span class="sxs-lookup"><span data-stu-id="295cc-108">The exact name of the file isn't important because Terraform accepts the folder name as a parameter: all scripts in the folder get executed.</span></span> <span data-ttu-id="295cc-109">Collez le code suivant dans le nouveau fichier :</span><span class="sxs-lookup"><span data-stu-id="295cc-109">Paste the following code in the new file:</span></span>

~~~~
# Configure the Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have to include this block
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
<span data-ttu-id="295cc-110">Dans la section `provider` du script, vous devez demander à Terraform d’utiliser un fournisseur Azure pour approvisionner les ressources dans le script.</span><span class="sxs-lookup"><span data-stu-id="295cc-110">In the `provider` section of the script, you tell Terraform to use an Azure provider to provision resources in the script.</span></span> <span data-ttu-id="295cc-111">Pour obtenir les valeurs de subscription_id, appId, password et tenant_id, reportez-vous au guide [d’installation et de configuration de Terraform](terraform-install-configure.md).</span><span class="sxs-lookup"><span data-stu-id="295cc-111">To get values for subscription_id, appId, password, and tenant_id, see the [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="295cc-112">Si vous avez créé des variables d’environnement pour les valeurs de ce bloc, vous n’avez pas besoin de l’inclure.</span><span class="sxs-lookup"><span data-stu-id="295cc-112">If you have created environment variables for the values in this block, you don't need to include it.</span></span> 

<span data-ttu-id="295cc-113">La ressource `azurerm_resource_group` demande à Terraform de créer un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="295cc-113">The `azurerm_resource_group` resource instructs Terraform to create a new resource group.</span></span> <span data-ttu-id="295cc-114">Vous trouverez d’autres types de ressources disponibles dans Terraform plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="295cc-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-the-script"></a><span data-ttu-id="295cc-115">Exécuter le script</span><span class="sxs-lookup"><span data-stu-id="295cc-115">Execute the script</span></span>
<span data-ttu-id="295cc-116">Une fois le script enregistré, quittez l’écran pour revenir à la console/ligne de commande et saisissez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="295cc-116">After you save the script, exit to the console/command line, and type the following:</span></span>
```
terraform init
```
<span data-ttu-id="295cc-117">pour initialiser le fournisseur Terraform pour Azure.</span><span class="sxs-lookup"><span data-stu-id="295cc-117">to initialize Terraform provider for Azure.</span></span> <span data-ttu-id="295cc-118">Tapez ensuite la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="295cc-118">Then type the following:</span></span>
```
terraform plan terraformscripts
```
<span data-ttu-id="295cc-119">Nous supposons que `terraformscripts` est le dossier dans lequel le script a été enregistré.</span><span class="sxs-lookup"><span data-stu-id="295cc-119">We assume that `terraformscripts` is the folder where the script was saved.</span></span> <span data-ttu-id="295cc-120">Nous avons utilisé la commande Terraform `plan`, qui examine les ressources définies dans les scripts.</span><span class="sxs-lookup"><span data-stu-id="295cc-120">We used the `plan` Terraform command, which looks at the resources defined in the scripts.</span></span> <span data-ttu-id="295cc-121">Elle les compare aux informations d’état enregistrées par Terraform et génère ensuite l’exécution planifiée _sans_ créer réellement de ressources dans Azure.</span><span class="sxs-lookup"><span data-stu-id="295cc-121">It compares them to the state information saved by Terraform and then outputs the planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="295cc-122">Après l’exécution de la commande précédente, vous devriez voir un écran similaire au suivant :</span><span class="sxs-lookup"><span data-stu-id="295cc-122">After you execute the previous command, you should see something like the following screen:</span></span>

![plan Terraform](linux/media/terraform/tf_plan2.png)

<span data-ttu-id="295cc-124">Si tout semble correct, approvisionnez ce nouveau groupe de ressources dans Azure en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="295cc-124">If everything looks correct, provision this new resource group in Azure by executing the following:</span></span> 
```
terraform apply terraformscripts
```
<span data-ttu-id="295cc-125">Dans le portail Azure, vous devez voir le nouveau groupe de ressources vide appelé `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="295cc-125">In the Azure portal, you should see the new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="295cc-126">Dans la section suivante, vous allez ajouter une machine virtuelle et toute l’infrastructure de prise en charge pour cette dernière dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="295cc-126">In the following section, you add a virtual machine and all the supporting infrastructure for that virtual machine to the resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="295cc-127">Approvisionner une machine virtuelle Ubuntu avec Terraform</span><span class="sxs-lookup"><span data-stu-id="295cc-127">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="295cc-128">Nous allons étendre le script Terraform créé avec les détails nécessaires à l’approvisionnement d’une machine virtuelle exécutant Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="295cc-128">Let's extend the Terraform script we've created with the details that are necessary to provision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="295cc-129">Voici les ressources approvisionnées dans les sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="295cc-129">The resources that you provision in the following sections are:</span></span>

* <span data-ttu-id="295cc-130">Un réseau avec un sous-réseau unique</span><span class="sxs-lookup"><span data-stu-id="295cc-130">A network with a single subnet</span></span>
* <span data-ttu-id="295cc-131">Une carte d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="295cc-131">A network interface card</span></span> 
* <span data-ttu-id="295cc-132">Un compte de stockage avec un conteneur de stockage</span><span class="sxs-lookup"><span data-stu-id="295cc-132">A storage account with a storage container</span></span>
* <span data-ttu-id="295cc-133">Une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="295cc-133">A public IP</span></span>
* <span data-ttu-id="295cc-134">Une machine virtuelle qui utilise toutes les ressources précédentes</span><span class="sxs-lookup"><span data-stu-id="295cc-134">A virtual machine that utilizes all the previous resources</span></span> 

<span data-ttu-id="295cc-135">Pour obtenir une documentation complète de chacune des ressources Azure Terraform, consultez la [documentation Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="295cc-135">For thorough documentation for each of the Azure Terraform resources, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="295cc-136">La version complète du [script d’approvisionnement](#complete-terraform-script) est également fournie pour des raisons de commodité.</span><span class="sxs-lookup"><span data-stu-id="295cc-136">The full version of the [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-the-terraform-script"></a><span data-ttu-id="295cc-137">Étendre le script Terraform</span><span class="sxs-lookup"><span data-stu-id="295cc-137">Extend the Terraform script</span></span>
<span data-ttu-id="295cc-138">Étendez le script créé avec les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="295cc-138">Extend the script that was created with the following resources:</span></span> 
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
<span data-ttu-id="295cc-139">Le script précédent crée un réseau virtuel et un sous-réseau au sein de ce réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="295cc-139">The previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="295cc-140">Prenez note de la référence au groupe de ressources que vous avez déjà créé par le biais de « ${azurerm_resource_group.helloterraform.name} » dans le réseau virtuel et la définition de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="295cc-140">Note the reference to the resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both the virtual network and the subnet definition.</span></span>

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
<span data-ttu-id="295cc-141">Les extraits de code de script précédents permettent de créer une adresse IP publique et une interface réseau qui utilise l’adresse IP publique créée.</span><span class="sxs-lookup"><span data-stu-id="295cc-141">The previous script snippets create a public IP and a network interface that makes use of the public IP created.</span></span> <span data-ttu-id="295cc-142">Prenez note des références à subnet_id et public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="295cc-142">Note the references to subnet_id and public_ip_address_id.</span></span> <span data-ttu-id="295cc-143">Terraform dispose d’une intelligence intégrée et comprend ainsi que cette interface réseau a une dépendance vis-à-vis des ressources qui doivent être créées avant l’interface réseau.</span><span class="sxs-lookup"><span data-stu-id="295cc-143">Terraform has built-in intelligence to understand that the network interface has a dependency on the resources that need to be created before the creation of the network interface.</span></span>

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
<span data-ttu-id="295cc-144">Ici, vous avez créé un compte de stockage et y avez défini un conteneur de stockage.</span><span class="sxs-lookup"><span data-stu-id="295cc-144">Here, you created a storage account and defined a storage container within that storage account.</span></span> <span data-ttu-id="295cc-145">C’est dans ce compte de stockage que sont stockés les disques durs virtuels (VHD) de la machine virtuelle que vous êtes sur le point de créer.</span><span class="sxs-lookup"><span data-stu-id="295cc-145">This storage account is where you store virtual hard disks (VHDs) for the virtual machine about to be created.</span></span>

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
<span data-ttu-id="295cc-146">Enfin, l’extrait de code précédent crée une machine virtuelle qui utilise toutes les ressources déjà approvisionnées.</span><span class="sxs-lookup"><span data-stu-id="295cc-146">Finally, the previous snippet creates a virtual machine that utilizes all the resources provisioned already.</span></span> <span data-ttu-id="295cc-147">Il s’agit du compte et du conteneur de stockage pour disque dur virtuel, de l’interface réseau avec adresse IP publique et du sous-réseau spécifié, et du groupe de ressources déjà créé.</span><span class="sxs-lookup"><span data-stu-id="295cc-147">They are a storage account and container for a VHD, a network interface with public IP and subnet specified, and the resource group you already created.</span></span> <span data-ttu-id="295cc-148">Prenez note de la propriété vm_size, où le script spécifie une référence SKU Azure A0.</span><span class="sxs-lookup"><span data-stu-id="295cc-148">Note the vm_size property, where the script specifies an Azure A0 SKU.</span></span>

### <a name="execute-the-script"></a><span data-ttu-id="295cc-149">Exécuter le script</span><span class="sxs-lookup"><span data-stu-id="295cc-149">Execute the script</span></span>
<span data-ttu-id="295cc-150">Une fois le script complet enregistré, quittez la console/ligne de commande et saisissez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="295cc-150">With the full script saved, exit to the console/command line and type the following:</span></span>
```
terraform apply terraformscripts
```
<span data-ttu-id="295cc-151">Après quelques instants, les ressources (y compris une machine virtuelle) s’affichent dans le groupe de ressources `terraformtest` sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="295cc-151">After some time, the resources, including a virtual machine, appear in the `terraformtest` resource group in the Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="295cc-152">Script Terraform complet</span><span class="sxs-lookup"><span data-stu-id="295cc-152">Complete Terraform script</span></span>

<span data-ttu-id="295cc-153">Pour faciliter votre travail, voici l’intégralité du script Terraform qui configure l’ensemble de l’infrastructure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="295cc-153">For your convenience, below is the complete Terraform script that provisions all of the infrastructure discussed in this article.</span></span>

```
variable "resourcesname" {
  default = "helloterraform"
}

# Configure the Microsoft Azure Provider
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

## <a name="next-steps"></a><span data-ttu-id="295cc-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="295cc-154">Next steps</span></span>
<span data-ttu-id="295cc-155">Vous avez créé une infrastructure de base dans Azure à l’aide de Terraform.</span><span class="sxs-lookup"><span data-stu-id="295cc-155">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="295cc-156">Pour des scénarios plus complexes, y compris des exemples utilisant des équilibreurs de charge et des groupes de machines virtuelles identiques, consultez les nombreux [exemples Terraform pour Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="295cc-156">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="295cc-157">Pour obtenir une liste actualisée et complète des fournisseurs Azure pris en charge, consultez la [documentation Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="295cc-157">For an up-to-date list of supported Azure providers, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
