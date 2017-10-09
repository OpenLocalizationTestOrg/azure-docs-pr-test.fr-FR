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
# <a name="install-and-configure-terraform-tooprovision-vms-and-other-infrastructure-into-azure"></a>Installer et configurer des machines virtuelles de tooprovision Terraform et une autre infrastructure dans Azure 
Cet article décrit les hello étapes nécessaires tooinstall et configurer les ressources de tooprovision Terraform tels que des machines virtuelles dans Azure. Vous allez apprendre comment toocreate et utilisez Azure les informations d’identification tooenable Terraform tooprovision des ressources de cloud de manière sécurisée.

HashiCorp Terraform fournit un moyen simple de toodefine et déployer l’infrastructure cloud à l’aide d’un langage de création de modèles personnalisé appelé langage de configuration HashiCorp (HCL). Ce langage personnalisé est [toowrite simple et facile toounderstand](terraform-create-complete-vm.md). En outre, à l’aide de hello `terraform plan` de commande, vous pouvez visualiser les infrastructures de tooyour hello modifications avant de les valider. Suivez ces toostart étapes à l’aide de Terraform avec Azure.

## <a name="install-terraform"></a>Installer Terraform
tooinstall Terraform, [télécharger](https://www.terraform.io/downloads.html) package hello appropriée pour votre système d’exploitation dans un répertoire d’installation distincts. Hello contient un seul fichier exécutable pour lequel vous devez également définir un chemin d’accès globale. Pour obtenir des instructions sur la façon dont tooset hello chemin d’accès sur Linux et Mac, accédez trop[cette page Web](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux). Pour obtenir des instructions sur comment tooset hello chemin d’accès sur Windows, accédez trop[cette page Web](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows). tooverify votre installation, exécutez hello `terraform` commande. Une liste des options Terraform disponibles devrait s’afficher en sortie.

Ensuite, vous devez tooallow Terraform accès tooyour abonnement Azure tooperform infrastructure de configuration.

## <a name="set-up-terraform-access-tooazure"></a>Configurer Terraform accès tooAzure
tooenable Terraform tooprovision des ressources dans Azure, vous devez toocreate deux entités dans Azure Active Directory (Azure AD) : une application Azure AD et un principal du service Azure AD. Utilisez ensuite les identificateurs de ces entités dans vos scripts Terraform. Le principal de service est une instance locale d’application Azure AD globale. Un principal de service permet de ressources de tooglobal contrôle granulaire de l’accès local.

Il existe plusieurs façons toocreate une application Azure AD et un principal du service Azure AD. Hello plus facile et plus rapide est façon aujourd'hui toouse Azure CLI 2.0, lequel [vous pouvez télécharger et installer sur un Mac, Linux ou Windows](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli). Vous pouvez également utiliser l’infrastructure de sécurité nécessaires de hello toocreate PowerShell ou CLI Azure version 1.0. Hello les instructions qui suivent montrent comment tooconfigure Terraform pour Azure à l’aide de toutes ces approches.

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a>Utiliser Azure CLI 2.0 (pour les utilisateurs Windows, Linux ou Mac) 
Une fois que vous téléchargez et installez hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), connectez-vous tooadminister votre abonnement Azure en émettant hello de commande suivante :

```
az login
```

>[!NOTE]
>Si vous utilisez hello Chine, Azure situés en Allemagne ou les clouds Azure Government, vous devez toofirst configurer hello CLI d’Azure toowork avec ce cloud. Pour cela, vous pouvez exécutant hello suivante :

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

Si vous avez plusieurs abonnements Azure, leurs détails sont retournés par hello `az login` commande. Ensemble hello `SUBSCRIPTION_ID` environnement hello toohold variable la valeur hello retournée `id` champ d’abonnement de hello souhaité toouse. 

Définir l’abonnement hello que vous souhaitez toouse pour cette session.

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

ID d’abonnement hello hello compte tooget de requête et valeurs d’ID de client.

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

Créez ensuite des informations d’identification distinctes pour Terraform.

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

Les valeurs appId, password, sp_name et tenant sont renvoyées. Prenez note de hello appId et le mot de passe.

tooconfirm vos informations d’identification (principal du service), ouvrez un nouvel interpréteur de commandes et exécutez hello suivant les commandes. Hello substitut retourné valeurs sp_name, mot de passe et client :

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a>Utiliser PowerShell (pour les utilisateurs Windows) 
toouse Windows toowrite de l’ordinateur et exécuter votre Terraform scripts et toouse PowerShell pour les tâches de configuration, configurer votre ordinateur avec les outils PowerShell hello. 

1. Installer les outils PowerShell en suivant les étapes de hello dans [installer et configurer Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps). 

2. Télécharger et exécuter hello [azure-setup.ps1 script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) à partir de la console PowerShell de hello.

3. script d’azure-setup.ps1 toorun hello, télécharger et exécuter hello `./azure-setup.ps1 setup` commande à partir de la console PowerShell de hello. Connectez-vous ensuite tooyour abonnement Azure avec des privilèges d’administrateur.

4. Indiquez un nom d’application (chaîne arbitraire, requis) lorsque vous y êtes invité. À l’invite, vous pouvez également indiquer un mot de passe sécurisé. Si vous ne fournissez pas de mot de passe, le mot de passe sécurisé est automatiquement généré à l’aide des bibliothèques de sécurité .NET.

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a>Utiliser Azure CLI 1.0 (pour les utilisateurs Linux ou Mac)
tooget main Terraform sur les ordinateurs Linux ou Mac avec Azure CLI 1.0, installer les bibliothèques hello approprié sur votre ordinateur.  

1. Installer les outils CLI xPlat Azure en suivant les étapes de hello dans [installer Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli). 

2. Téléchargez et installez un processeur JSON en suivant les instructions de hello dans [télécharger jq](https://stedolan.github.io/jq/download/).

3. Télécharger et exécuter hello [azure-setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script à partir de la console de hello.

4. script d’azure-setup.sh toorun hello, télécharger et exécuter hello `./azure-setup setup` commande à partir de la console de hello. Connectez-vous ensuite tooyour abonnement Azure avec des privilèges d’administrateur.
 
5. Indiquez un nom d’application (chaîne arbitraire, requis) lorsque vous y êtes invité. À l’invite, vous pouvez également indiquer un mot de passe sécurisé. Si vous ne fournissez pas de mot de passe, le mot de passe sécurisé est automatiquement généré à l’aide des bibliothèques de sécurité .NET.

Tous les scripts précédents hello créent une application Azure AD et le service principal. principal du service Hello obtienne un contributeur ou l’accès au niveau du propriétaire d’abonnement de hello. En raison de hello haut niveau d’accès accordé, vous devez toujours protéger les informations de sécurité hello générées par ces scripts. Prenez note des quatre éléments d’informations de sécurité fournis par ces scripts : appId, password, subscription_id et tenant_id.

## <a name="set-environment-variables"></a>Définition des variables d'environnement
Une fois que vous créez et configurez un principal du service Azure AD, vous devez toolet Terraform connaître hello client ID, ID d’abonnement, ID de client et toouse secrète du client. Vous pouvez le faire en incorporant ces valeurs dans vos scripts Terraform (comme décrit dans l’article [Créer une infrastructure de base dans Azure à l’aide de Terraform](terraform-create-complete-vm.md). Ou bien, vous pouvez définir hello suivant des variables d’environnement (et par conséquent éviter accidentellement archivage ou le partage de vos informations d’identification) :

- ARM_SUBSCRIPTION_ID
- ARM_CLIENT_ID
- ARM_CLIENT_SECRET
- ARM_TENANT_ID

Ces variables, vous pouvez utiliser cette tooset de script de shell exemple :

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

En outre, si vous utilisez Terraform avec Azure en Chine ou soit Azure Government ou Allemagne d’Azure, vous devez correctement variable d’environnement tooset hello.

## <a name="next-steps"></a>Étapes suivantes
Vous avez installé Terraform et configuré les informations d’identification Azure pour pouvoir démarrer le déploiement d’infrastructure dans votre abonnement Azure. Ensuite, découvrez comment trop[créer l’infrastructure avec Terraform](terraform-create-complete-vm.md).
