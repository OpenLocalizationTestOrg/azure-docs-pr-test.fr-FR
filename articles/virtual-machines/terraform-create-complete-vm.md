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
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a>Créer une infrastructure de base dans Azure à l’aide de Terraform
Cet article décrit les étapes de hello vous devez tootake tooprovision une machine virtuelle, ainsi que de l’infrastructure sous-jacente, dans Azure. Vous allez apprendre comment toowrite Terraform scripts et comment toovisualize hello change avant de vous rendre dans votre infrastructure cloud. Vous allez également apprendre comment infrastructure toocreate dans Azure à l’aide de Terraform.

tooget démarré, créez un fichier appelé \terraform_azure101.tf dans votre éditeur de texte de choix (Visual Studio Code/Sublime/Vim/etc.). nom exact de Hello du fichier de hello n’est pas important, car Terraform accepte le nom du dossier hello en tant que paramètre : tous les scripts dans le dossier de hello sont exécutées. Collez hello suivant de code dans un fichier nouveau hello :

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
Bonjour `provider` section Hello de script, vous indiquez à Terraform toouse une ressources tooprovision de fournisseur Azure dans le script de hello. tooget valeurs ID_ABONNEMENT, appId, mot de passe et tenant_id, consultez hello [installer et configurer Terraform](terraform-install-configure.md) guide. Si vous avez créé des variables d’environnement pour les valeurs hello dans ce bloc, vous n’avez pas besoin de tooinclude il. 

Hello `azurerm_resource_group` ressource indique Terraform toocreate un groupe de ressources. Vous trouverez d’autres types de ressources disponibles dans Terraform plus loin dans cet article.

## <a name="execute-hello-script"></a>Exécuter le script de hello
Après avoir enregistré le script de hello, quittez la ligne de commande de la console toohello et tapez Bonjour suivante :
```
terraform init
```
fournisseur de Terraform tooinitialize pour Azure. Puis tapez ce qui suit hello :
```
terraform plan terraformscripts
```
Nous supposons que `terraformscripts` est le dossier hello où le script de hello a été enregistré. Nous avons utilisé hello `plan` commande Terraform, qui examine les ressources hello définies dans les scripts de hello. Il compare les toohello les informations d’état enregistrées par Terraform et puis sorties hello planifié l’exécution _sans_ créez en fait des ressources dans Azure. 

Une fois que vous exécutez la commande précédente hello, vous devez voir quelque chose comme hello suivant d’écran :

![plan Terraform](linux/media/terraform/tf_plan2.png)

Si tout semble correct, configurez ce nouveau groupe de ressources dans Azure en exécutant hello qui suit : 
```
terraform apply terraformscripts
```
Bonjour portail Azure, vous devez voir le nouveau groupe de ressources vide hello appelé `terraformtest`. Bonjour suivant la section, vous ajoutez qu'une machine virtuelle et tous les hello infrastructure de prise en charge pour ce groupe de ressources d’ordinateur virtuel toohello.

## <a name="provision-an-ubuntu-vm-with-terraform"></a>Approvisionner une machine virtuelle Ubuntu avec Terraform
Nous allons étendre script de Terraform hello qu'avec les détails de hello tooprovision nécessaire, nous avons créé une machine virtuelle exécutant Ubuntu. ressources Hello que vous préparez dans les sections suivantes de hello sont :

* Un réseau avec un sous-réseau unique
* Une carte d’interface réseau 
* Un compte de stockage avec un conteneur de stockage
* Une adresse IP publique
* Un ordinateur virtuel qui utilise toutes les ressources précédentes hello 

Pour obtenir une documentation complète pour chacune des ressources d’Azure Terraform hello, consultez hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).

version complète de Hello Hello [script de configuration](#complete-terraform-script) est également fournie pour des raisons de commodité.

### <a name="extend-hello-terraform-script"></a>Étendre le script de Terraform hello
Étendre le script hello qui a été créé avec hello suivant des ressources : 
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
Hello le script précédent crée un réseau virtuel et un sous-réseau au sein de ce réseau virtuel. Notez le groupe de ressources hello référence toohello que vous avez déjà créé via « ${azurerm_resource_group.helloterraform.name} » dans le réseau virtuel de hello et définition de sous-réseau hello.

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
extraits de code de script précédent Hello créer une adresse IP publique et une interface réseau qui utilise des adresses IP publiques hello créé. Remarque hello références toosubnet_id et public_ip_address_id. Terraform a intelligence intégrée toounderstand que hello interface réseau a une dépendance sur les ressources de hello que toobe besoin créé avant la création de l’interface de réseau hello hello.

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
Ici, vous avez créé un compte de stockage et y avez défini un conteneur de stockage. Ce compte de stockage est où vous stockez des disques durs virtuels (VHD) pour la machine virtuelle de hello sur toobe créé.

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
Enfin, extrait de code hello précédente crée un ordinateur virtuel qui utilise toutes les ressources hello configurés déjà. Ils sont un compte de stockage et un conteneur pour un disque dur virtuel, une interface réseau avec publique IP et le sous-réseau spécifié, et le groupe de ressources hello déjà créé. Notez la propriété de vm_size hello, où le script de hello spécifie une référence (SKU) A0 de Azure.

### <a name="execute-hello-script"></a>Exécuter le script de hello
Avec le script complet hello enregistré quitter la ligne de commande de la console toohello et tapez Bonjour suivant :
```
terraform apply terraformscripts
```
Après un certain temps, hello ressources, y compris un ordinateur virtuel, s’affichent dans hello `terraformtest` groupe de ressources dans hello portail Azure.

## <a name="complete-terraform-script"></a>Script Terraform complet

Pour votre commodité, voici complète du script Terraform hello qui configure de hello infrastructure abordé dans cet article.

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

## <a name="next-steps"></a>Étapes suivantes
Vous avez créé une infrastructure de base dans Azure à l’aide de Terraform. Pour des scénarios plus complexes, y compris des exemples utilisant des équilibreurs de charge et des groupes de machines virtuelles identiques, consultez les nombreux [exemples Terraform pour Azure](https://github.com/hashicorp/terraform/tree/master/examples). Pour obtenir une liste actualisée des fournisseurs Azure pris en charge, consultez hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).
