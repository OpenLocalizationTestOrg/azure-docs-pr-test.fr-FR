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
ms.openlocfilehash: 52591009ee7cb906402b8bca2ce63794ac7afcc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="eff80-103">Créer une infrastructure de base dans Azure à l’aide de Terraform</span><span class="sxs-lookup"><span data-stu-id="eff80-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="eff80-104">Cet article décrit les étapes de hello vous devez tootake tooprovision une machine virtuelle, ainsi que de l’infrastructure sous-jacente, dans Azure.</span><span class="sxs-lookup"><span data-stu-id="eff80-104">This article describes hello steps you need tootake tooprovision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="eff80-105">Vous allez apprendre comment toowrite Terraform scripts et comment toovisualize hello change avant de vous rendre dans votre infrastructure cloud.</span><span class="sxs-lookup"><span data-stu-id="eff80-105">You will learn how toowrite Terraform scripts and how toovisualize hello changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="eff80-106">Vous allez également apprendre comment infrastructure toocreate dans Azure à l’aide de Terraform.</span><span class="sxs-lookup"><span data-stu-id="eff80-106">You also will learn how toocreate infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="eff80-107">tooget démarré, créez un fichier appelé \terraform_azure101.tf dans votre éditeur de texte de choix (Visual Studio Code/Sublime/Vim/etc.).</span><span class="sxs-lookup"><span data-stu-id="eff80-107">tooget started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="eff80-108">nom exact de Hello du fichier de hello n’est pas important, car Terraform accepte le nom du dossier hello en tant que paramètre : tous les scripts dans le dossier de hello sont exécutées.</span><span class="sxs-lookup"><span data-stu-id="eff80-108">hello exact name of hello file isn't important because Terraform accepts hello folder name as a parameter: all scripts in hello folder get executed.</span></span> <span data-ttu-id="eff80-109">Collez hello suivant de code dans un fichier nouveau hello :</span><span class="sxs-lookup"><span data-stu-id="eff80-109">Paste hello following code in hello new file:</span></span>

~~~~
# Configure hello Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have tooinclude this block
provider "azurerm" {
  subscription_id = "your_subscription_id_from_script_execution"
  client_id       = "your_appId_from_script_execution"
  client_secret   = "your_password_from_script_execution"
  tenant_id       = "your_tenant_id_from_script_execution"
}

# create a resource group if it doesn't exist
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}
~~~~
<span data-ttu-id="eff80-110">Bonjour `provider` section Hello de script, vous indiquez à Terraform toouse une ressources tooprovision de fournisseur Azure dans le script de hello.</span><span class="sxs-lookup"><span data-stu-id="eff80-110">In hello `provider` section of hello script, you tell Terraform toouse an Azure provider tooprovision resources in hello script.</span></span> <span data-ttu-id="eff80-111">tooget valeurs ID_ABONNEMENT, appId, mot de passe et tenant_id, consultez hello [installer et configurer Terraform](terraform-install-configure.md) guide.</span><span class="sxs-lookup"><span data-stu-id="eff80-111">tooget values for subscription_id, appId, password, and tenant_id, see hello [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="eff80-112">Si vous avez créé des variables d’environnement pour les valeurs hello dans ce bloc, vous n’avez pas besoin de tooinclude il.</span><span class="sxs-lookup"><span data-stu-id="eff80-112">If you have created environment variables for hello values in this block, you don't need tooinclude it.</span></span> 

<span data-ttu-id="eff80-113">Hello `azurerm_resource_group` ressource indique Terraform toocreate un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="eff80-113">hello `azurerm_resource_group` resource instructs Terraform toocreate a new resource group.</span></span> <span data-ttu-id="eff80-114">Vous trouverez d’autres types de ressources disponibles dans Terraform plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="eff80-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-hello-script"></a><span data-ttu-id="eff80-115">Exécuter le script de hello</span><span class="sxs-lookup"><span data-stu-id="eff80-115">Execute hello script</span></span>
<span data-ttu-id="eff80-116">Après avoir enregistré le script de hello, quittez la ligne de commande de la console toohello et tapez Bonjour suivante :</span><span class="sxs-lookup"><span data-stu-id="eff80-116">After you save hello script, exit toohello console/command line, and type hello following:</span></span>
```
terraform init
```
 <span data-ttu-id="eff80-117">fournisseur de Terraform tooinitialize hello pour Azure.</span><span class="sxs-lookup"><span data-stu-id="eff80-117">tooinitialize hello Terraform provider for Azure.</span></span> <span data-ttu-id="eff80-118">Basculez ensuite hello trop**terraformscripts**, et hello du problème de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="eff80-118">Then change hello directory too**terraformscripts**, and issue hello following command:</span></span>
```
terraform plan
```
<span data-ttu-id="eff80-119">Nous avons utilisé hello `plan` commande Terraform, qui examine les ressources hello définies dans les scripts de hello.</span><span class="sxs-lookup"><span data-stu-id="eff80-119">We used hello `plan` Terraform command, which looks at hello resources defined in hello scripts.</span></span> <span data-ttu-id="eff80-120">Il compare les toohello les informations d’état enregistrées par Terraform et puis sorties hello planifié l’exécution _sans_ créez en fait des ressources dans Azure.</span><span class="sxs-lookup"><span data-stu-id="eff80-120">It compares them toohello state information saved by Terraform and then outputs hello planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="eff80-121">Une fois que vous exécutez la commande précédente hello, vous devez voir quelque chose comme hello suivant d’écran :</span><span class="sxs-lookup"><span data-stu-id="eff80-121">After you execute hello previous command, you should see something like hello following screen:</span></span>

![plan Terraform](./media/terraform/tf_plan2.png)

<span data-ttu-id="eff80-123">Si tout semble correct, configurez ce nouveau groupe de ressources dans Azure en exécutant hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="eff80-123">If everything looks correct, provision this new resource group in Azure by executing hello following:</span></span> 
```
terraform apply
```
<span data-ttu-id="eff80-124">Bonjour portail Azure, vous devez voir le nouveau groupe de ressources vide hello appelé `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="eff80-124">In hello Azure portal, you should see hello new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="eff80-125">Bonjour suivant la section, vous ajoutez qu'une machine virtuelle et tous les hello infrastructure de prise en charge pour ce groupe de ressources d’ordinateur virtuel toohello.</span><span class="sxs-lookup"><span data-stu-id="eff80-125">In hello following section, you add a virtual machine and all hello supporting infrastructure for that virtual machine toohello resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="eff80-126">Approvisionner une machine virtuelle Ubuntu avec Terraform</span><span class="sxs-lookup"><span data-stu-id="eff80-126">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="eff80-127">Nous allons étendre script de Terraform hello qu'avec les détails de hello tooprovision nécessaire, nous avons créé une machine virtuelle exécutant Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="eff80-127">Let's extend hello Terraform script we've created with hello details that are necessary tooprovision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="eff80-128">ressources Hello que vous préparez dans les sections suivantes de hello sont :</span><span class="sxs-lookup"><span data-stu-id="eff80-128">hello resources that you provision in hello following sections are:</span></span>

* <span data-ttu-id="eff80-129">Un réseau avec un sous-réseau unique</span><span class="sxs-lookup"><span data-stu-id="eff80-129">A network with a single subnet</span></span>
* <span data-ttu-id="eff80-130">Une carte d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="eff80-130">A network interface card</span></span> 
* <span data-ttu-id="eff80-131">Un compte de stockage pour les diagnostics de machine virtuelle hello</span><span class="sxs-lookup"><span data-stu-id="eff80-131">A storage account for hello virtual machine diagnostics</span></span>
* <span data-ttu-id="eff80-132">Une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="eff80-132">A public IP</span></span>
* <span data-ttu-id="eff80-133">Un ordinateur virtuel qui utilise toutes les ressources précédentes hello</span><span class="sxs-lookup"><span data-stu-id="eff80-133">A virtual machine that utilizes all hello previous resources</span></span> 

<span data-ttu-id="eff80-134">Pour obtenir une documentation complète pour chacune des ressources d’Azure Terraform hello, consultez hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="eff80-134">For thorough documentation for each of hello Azure Terraform resources, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="eff80-135">version complète de Hello Hello [script de configuration](#complete-terraform-script) est également fournie pour des raisons de commodité.</span><span class="sxs-lookup"><span data-stu-id="eff80-135">hello full version of hello [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-hello-terraform-script"></a><span data-ttu-id="eff80-136">Étendre le script de Terraform hello</span><span class="sxs-lookup"><span data-stu-id="eff80-136">Extend hello Terraform script</span></span>
<span data-ttu-id="eff80-137">Étendre le script hello qui a été créé avec hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="eff80-137">Extend hello script that was created with hello following resources:</span></span> 
~~~~
# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    tags {
        environment = "Terraform Demo"
    }
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}
~~~~
<span data-ttu-id="eff80-138">Hello le script précédent crée un réseau virtuel et un sous-réseau au sein de ce réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="eff80-138">hello previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="eff80-139">Notez le groupe de ressources hello référence toohello que vous avez déjà créé via « ${azurerm_resource_group.helloterraform.name} » dans le réseau virtuel de hello et définition de sous-réseau hello.</span><span class="sxs-lookup"><span data-stu-id="eff80-139">Note hello reference toohello resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both hello virtual network and hello subnet definition.</span></span>

~~~~
# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "Terraform Demo"
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

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
<span data-ttu-id="eff80-140">extraits de code de script précédent Hello créer une adresse IP publique et une interface réseau qui utilise des adresses IP publiques hello créé.</span><span class="sxs-lookup"><span data-stu-id="eff80-140">hello previous script snippets create a public IP and a network interface that makes use of hello public IP created.</span></span> <span data-ttu-id="eff80-141">Remarque hello références toosubnet_id et public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="eff80-141">Note hello references toosubnet_id and public_ip_address_id.</span></span> <span data-ttu-id="eff80-142">Terraform a intelligence intégrée toounderstand que hello interface réseau a une dépendance sur les ressources de hello que toobe besoin créé avant la création de l’interface de réseau hello hello.</span><span class="sxs-lookup"><span data-stu-id="eff80-142">Terraform has built-in intelligence toounderstand that hello network interface has a dependency on hello resources that need toobe created before hello creation of hello network interface.</span></span>

~~~~
# create a random id
resource "random_id" "randomId" {
  keepers = {
    # Generate a new id only when a new resource group is defined
    resource_group = "${azurerm_resource_group.helloterraform.name}"
  }

  byte_length = 8
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "diag${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "West US"
    account_type = "Standard_LRS"

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
<span data-ttu-id="eff80-143">Ici, vous avez créé un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="eff80-143">Here, you created a storage account.</span></span> <span data-ttu-id="eff80-144">Ce compte de stockage est où hello virtual machine stocke ses informations de diagnostics.</span><span class="sxs-lookup"><span data-stu-id="eff80-144">This storage account is where hello virtual machine will store its diagnostics details.</span></span>

~~~~
# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_DS1_v2"

    os_profile {
        computer_name = "hostname"
        admin_username = "azureuser"
        admin_password = ""
    }

    os_profile_linux_config {
        disable_password_authentication = true

        ssh_keys {
            path = "/home/azureuser/.ssh/authorized_keys"
            key_data = "... INSERT OPENSSH PUBLIC KEY HERE ..."
        }
    }

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "16.04.0-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        managed_disk_type = "Premium_LRS"
        create_option = "FromImage"
    } 

    boot_diagnostics {
        enabled = "true"
        storage_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
<span data-ttu-id="eff80-145">Enfin, extrait de code hello précédente crée un ordinateur virtuel qui utilise toutes les ressources hello configurés déjà.</span><span class="sxs-lookup"><span data-stu-id="eff80-145">Finally, hello previous snippet creates a virtual machine that utilizes all hello resources provisioned already.</span></span> <span data-ttu-id="eff80-146">Ils sont un compte de stockage pour les diagnostics de machine virtuelle hello, une interface réseau avec IP public et le sous-réseau spécifié et groupe de ressources hello déjà créé.</span><span class="sxs-lookup"><span data-stu-id="eff80-146">They are a storage account for hello virtual machine diagnostics, a network interface with public IP and subnet specified, and hello resource group you already created.</span></span> <span data-ttu-id="eff80-147">Notez la propriété de vm_size hello, où le script de hello spécifie une référence de DS1v2 Azure Standard.</span><span class="sxs-lookup"><span data-stu-id="eff80-147">Note hello vm_size property, where hello script specifies an Azure Standard DS1v2 SKU.</span></span>

<span data-ttu-id="eff80-148">Vous êtes toosupply requis une clé publique SSH.</span><span class="sxs-lookup"><span data-stu-id="eff80-148">You are required toosupply an SSH public key.</span></span> <span data-ttu-id="eff80-149">Placez la valeur de clé publique hello dans la section de hello **... INSERT OPENSSH PUBLIC KEY HERE ...** ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="eff80-149">Place hello public key value into hello section **... INSERT OPENSSH PUBLIC KEY HERE ...** above.</span></span> <span data-ttu-id="eff80-150">Vous pouvez utiliser un existant ssh paire de clés ou suivez hello [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) ou [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) paire de clés de documentation toogenerate hello.</span><span class="sxs-lookup"><span data-stu-id="eff80-150">You can use an existing ssh key pair or follow hello [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) or [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) documentation toogenerate hello key pair.</span></span>

### <a name="execute-hello-script"></a><span data-ttu-id="eff80-151">Exécuter le script de hello</span><span class="sxs-lookup"><span data-stu-id="eff80-151">Execute hello script</span></span>
<span data-ttu-id="eff80-152">Avec le script complet hello enregistré quitter la ligne de commande de la console toohello et tapez Bonjour suivant :</span><span class="sxs-lookup"><span data-stu-id="eff80-152">With hello full script saved, exit toohello console/command line and type hello following:</span></span>
```
terraform apply
```
<span data-ttu-id="eff80-153">Après un certain temps, hello ressources, y compris un ordinateur virtuel, s’affichent dans hello `terraformtest` groupe de ressources dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="eff80-153">After some time, hello resources, including a virtual machine, appear in hello `terraformtest` resource group in hello Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="eff80-154">Script Terraform complet</span><span class="sxs-lookup"><span data-stu-id="eff80-154">Complete Terraform script</span></span>

<span data-ttu-id="eff80-155">Pour votre commodité, voici complète du script Terraform hello qui configure de hello infrastructure abordé dans cet article.</span><span class="sxs-lookup"><span data-stu-id="eff80-155">For your convenience, below is hello complete Terraform script that provisions all of hello infrastructure discussed in this article.</span></span>

```
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

# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    tags {
        environment = "Terraform Demo"
    }
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}

# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "Terraform Demo"
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

    tags {
        environment = "Terraform Demo"
    }
}

# create a random id
resource "random_id" "randomId" {
  keepers = {
    # Generate a new id only when a new resource group is defined
    resource_group = "${azurerm_resource_group.helloterraform.name}"
  }

  byte_length = 8
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "diag${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "West US"
    account_type = "Standard_LRS"

    tags {
        environment = "Terraform Demo"
    }
}

# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_DS1_v2"

    os_profile {
        computer_name = "hostname"
        admin_username = "azureuser"
        admin_password = ""
    }

    os_profile_linux_config {
        disable_password_authentication = true

        ssh_keys {
            path = "/home/azureuser/.ssh/authorized_keys"
            key_data = "... INSERT OPENSSH PUBLIC KEY HERE ..."
        }
    }

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "16.04.0-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        managed_disk_type = "Premium_LRS"
        create_option = "FromImage"
    } 

    boot_diagnostics {
        enabled = "true"
        storage_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="eff80-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="eff80-156">Next steps</span></span>
<span data-ttu-id="eff80-157">Vous avez créé une infrastructure de base dans Azure à l’aide de Terraform.</span><span class="sxs-lookup"><span data-stu-id="eff80-157">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="eff80-158">Pour des scénarios plus complexes, y compris des exemples utilisant des équilibreurs de charge et des groupes de machines virtuelles identiques, consultez les nombreux [exemples Terraform pour Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="eff80-158">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="eff80-159">Pour obtenir une liste actualisée des fournisseurs Azure pris en charge, consultez hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="eff80-159">For an up-to-date list of supported Azure providers, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
