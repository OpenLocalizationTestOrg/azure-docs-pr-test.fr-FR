---
title: "échelle de machines virtuelles aaaMake jeux disponible dans la pile de Azure"
description: "Découvrez comment un administrateur de cloud peut ajouter toohello de mise à l’échelle de machine virtuelle Azure Marketplace de pile"
services: azure-stack
author: anjayajodha
ms.service: azure-stack
ms.topic: article
ms.date: 8/4/2017
ms.author: anajod
keywords: 
ms.openlocfilehash: 14365d62ac2f2bc453c25ce4769464eb30180ea8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="make-virtual-machine-scale-sets-available-in-azure-stack"></a>Mettre les groupes de machines virtuelles identiques à disposition dans Azure Stack
Les groupes de machines virtuelles identiques constituent une ressource de calcul Azure Stack. Vous pouvez les utiliser toodeploy et gérer un ensemble de machines virtuelles identiques. Avec tous les ordinateurs virtuels configurés hello identiques, identiques ne nécessitent pas configuration anticipée des machines virtuelles. Il est plus facile toobuild à grande échelle des services qui ciblent des charges de travail big compute et données volumineuses.

Cette rubrique vous guide tout au long de l’échelle hello processus toomake jeux disponibles Bonjour Azure Marketplace de pile. Après avoir terminé cette procédure, vos utilisateurs peuvent ajouter, échelle de machines virtuelles définit tootheir abonnements.

Les groupes de machines virtuelles identiques sur Azure Stack suivent le même principe que sur Azure. Pour plus d’informations, consultez hello suivant vidéos :
* [Mark Russinovich parle des groupes identiques Azure](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/)
* [Jeux de mise à l’échelle de machine virtuelle, avec Guy Bowerman](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-191-Virtual-Machine-Scale-Sets-with-Guy-Bowerman)

Sur Azure Stack, les groupes de machines virtuelles identiques ne sont pas compatibles avec la mise à l’échelle automatique. Vous pouvez ajouter plusieurs instances tooa mise à l’échelle définie à l’aide du portail de pile de Azure hello, des modèles de gestionnaire de ressources ou PowerShell.

## <a name="prerequisites"></a>Composants requis
* **PowerShell et outils**

   Installer et PowerShell configuré pour la pile d’Azure et les outils de pile de Azure hello. Consultez la page [Devenir opérationnel avec PowerShell dans Azure Stack](azure-stack-powershell-configure-quickstart.md).

   Après avoir installé les outils de pile de Azure hello, assurez-vous d’importer hello suivant le module PowerShell (toohello relative du chemin d’accès. dossier \ComputeAdmin dans le dossier de hello AzureStack-outils-master) :

        Import-Module .\AzureStack.ComputeAdmin.psm1

* **Image du système d’exploitation**

   Si vous n’avez pas ajouté une tooyour d’image de système d’exploitation Azure Marketplace de pile, consultez [marketplace de la pile de Azure ajouter hello Windows Server 2016 VM image toohello](azure-stack-add-default-image.md).

   Pour la prise en charge de Linux, téléchargez Ubuntu Server 16.04 et l’ajouter à l’aide de ```Add-AzsVMImage``` avec les paramètres suivants de hello : ```-publisher "Canonical" -offer "UbuntuServer" -sku "16.04-LTS"```.

## <a name="add-hello-virtual-machine-scale-set"></a>Ajouter l’ensemble d’échelle de machine virtuelle hello

Modifier hello PowerShell suivantes pour votre environnement de script et exécutez-le tooadd un tooyour de jeu de mise à l’échelle machine virtuelle Azure Marketplace de pile. 

``$User``est un compte de hello que vous utilisez le portail d’administration tooconnect hello. Par exemple, serviceadmin@contoso.onmicrosoft.com.

```
$Arm = "https://adminmanagement.local.azurestack.external"
$Location = "local"

Add-AzureRMEnvironment -Name AzureStackAdmin -ArmEndpoint $Arm

$Password = ConvertTo-SecureString -AsPlainText -Force "<your Azure Stack administrator password>"

$User = "<your Azure Stack service administrator user name>"

$Creds =  New-Object System.Management.Automation.PSCredential $User, $Password

$AzsEnv = Get-AzureRmEnvironment AzureStackAdmin
$AzsEnvContext = Add-AzureRmAccount -Environment $AzsEnv -Credential $Creds
Select-AzureRmProfile -Profile $AzsEnvContext

Select-AzureRmSubscription -SubscriptionName "Default Provider Subscription"

Add-AzsVMSSGalleryItem -Location $Location
```

## <a name="remove-a-virtual-machine-scale-set"></a>Supprimer un groupe de machines virtuelles identiques

tooremove un élément de galerie de machine virtuelle mise à l’échelle ensemble, exécutez hello suivant de commande PowerShell :

    Remove-AzsVMSSGalleryItem

> [!NOTE]
> élément de la galerie Hello ne peut pas être supprimée immédiatement. Vous devrez peut-être portal de hello toorefresh plusieurs fois avant qu’il soit supprimé hello Marketplace.


## <a name="next-steps"></a>Étapes suivantes
[Forum aux questions sur Azure Stack](azure-stack-faq.md)

