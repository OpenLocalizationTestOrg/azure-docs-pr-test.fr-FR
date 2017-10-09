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

# create a resource group if it doesn't exist
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
 fournisseur de Terraform tooinitialize hello pour Azure. Basculez ensuite hello trop**terraformscripts**, et hello du problème de commande suivante :
```
terraform plan
```
Nous avons utilisé hello `plan` commande Terraform, qui examine les ressources hello définies dans les scripts de hello. Il compare les toohello les informations d’état enregistrées par Terraform et puis sorties hello planifié l’exécution _sans_ créez en fait des ressources dans Azure. 

Une fois que vous exécutez la commande précédente hello, vous devez voir quelque chose comme hello suivant d’écran :

![plan Terraform](./media/terraform/tf_plan2.png)

Si tout semble correct, configurez ce nouveau groupe de ressources dans Azure en exécutant hello qui suit : 
```
terraform apply
```
Bonjour portail Azure, vous devez voir le nouveau groupe de ressources vide hello appelé `terraformtest`. Bonjour suivant la section, vous ajoutez qu'une machine virtuelle et tous les hello infrastructure de prise en charge pour ce groupe de ressources d’ordinateur virtuel toohello.

## <a name="provision-an-ubuntu-vm-with-terraform"></a>Approvisionner une machine virtuelle Ubuntu avec Terraform
Nous allons étendre script de Terraform hello qu'avec les détails de hello tooprovision nécessaire, nous avons créé une machine virtuelle exécutant Ubuntu. ressources Hello que vous préparez dans les sections suivantes de hello sont :

* Un réseau avec un sous-réseau unique
* Une carte d’interface réseau 
* Un compte de stockage pour les diagnostics de machine virtuelle hello
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
Hello le script précédent crée un réseau virtuel et un sous-réseau au sein de ce réseau virtuel. Notez le groupe de ressources hello référence toohello que vous avez déjà créé via « ${azurerm_resource_group.helloterraform.name} » dans le réseau virtuel de hello et définition de sous-réseau hello.

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
extraits de code de script précédent Hello créer une adresse IP publique et une interface réseau qui utilise des adresses IP publiques hello créé. Remarque hello références toosubnet_id et public_ip_address_id. Terraform a intelligence intégrée toounderstand que hello interface réseau a une dépendance sur les ressources de hello que toobe besoin créé avant la création de l’interface de réseau hello hello.

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
Ici, vous avez créé un compte de stockage. Ce compte de stockage est où hello virtual machine stocke ses informations de diagnostics.

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
Enfin, extrait de code hello précédente crée un ordinateur virtuel qui utilise toutes les ressources hello configurés déjà. Ils sont un compte de stockage pour les diagnostics de machine virtuelle hello, une interface réseau avec IP public et le sous-réseau spécifié et groupe de ressources hello déjà créé. Notez la propriété de vm_size hello, où le script de hello spécifie une référence de DS1v2 Azure Standard.

Vous êtes toosupply requis une clé publique SSH. Placez la valeur de clé publique hello dans la section de hello **... INSERT OPENSSH PUBLIC KEY HERE ...** ci-dessus. Vous pouvez utiliser un existant ssh paire de clés ou suivez hello [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) ou [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) paire de clés de documentation toogenerate hello.

### <a name="execute-hello-script"></a>Exécuter le script de hello
Avec le script complet hello enregistré quitter la ligne de commande de la console toohello et tapez Bonjour suivant :
```
terraform apply
```
Après un certain temps, hello ressources, y compris un ordinateur virtuel, s’affichent dans hello `terraformtest` groupe de ressources dans hello portail Azure.

## <a name="complete-terraform-script"></a>Script Terraform complet

Pour votre commodité, voici complète du script Terraform hello qui configure de hello infrastructure abordé dans cet article.

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

## <a name="next-steps"></a>Étapes suivantes
Vous avez créé une infrastructure de base dans Azure à l’aide de Terraform. Pour des scénarios plus complexes, y compris des exemples utilisant des équilibreurs de charge et des groupes de machines virtuelles identiques, consultez les nombreux [exemples Terraform pour Azure](https://github.com/hashicorp/terraform/tree/master/examples). Pour obtenir une liste actualisée des fournisseurs Azure pris en charge, consultez hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).
