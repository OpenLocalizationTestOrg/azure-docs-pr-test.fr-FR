---
title: "aaaDownload pile d’Azure tools à partir de GitHub | Documents Microsoft"
description: "Découvrez comment les outils toodownload requis toowork avec la pile de Azure."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: a88c97b0ef1dd70e63771f0607cc07ec7a00b533
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="download-azure-stack-tools-from-github"></a>Télécharger les outils Azure Stack à partir de GitHub

AzureStack-Tools est un référentiel GitHub qui héberge des modules PowerShell que vous pouvez utiliser toomanage et déployer des ressources tooAzure pile. Vous pouvez télécharger et utiliser ces PowerShell modules toohello Kit de développement Azure pile ou tooa basé sur windows externe client si vous envisagez de connectivité VPN de tooestablish. tooobtain ces outils, cloner le référentiel GitHub de hello ou hello AzureStack-outils dossier de téléchargement. 

référentiel de hello tooclone, téléchargez [Git](https://git-scm.com/download/win) pour Windows, ouvrez une fenêtre d’invite de commandes et exécutez hello script suivant :

```PowerShell
# Change directory toohello root directory 
cd \

# clone hello repository
git clone https://github.com/Azure/AzureStack-Tools.git --recursive

# Change toohello tools directory
cd AzureStack-Tools
```

dossier d’outils hello toodownload, exécutez hello script suivant :

```PowerShell
# Change directory toohello root directory 
cd \

# Download hello tools archive
invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

# Expand hello downloaded files
expand-archive master.zip `
  -DestinationPath . `
  -Force

# Change toohello tools directory
cd AzureStack-Tools-master

```

## <a name="functionalities-provided-by-hello-modules"></a>Fonctionnalités fournies par les modules de hello

référentiel de Hello AzureStack-Tools contient des modules PowerShell qui prennent en charge hello suivant de fonctionnalités pour la pile de Azure :  

| Fonctionnalités | Description | Qui peut utiliser ce module ? |
| --- | --- | --- |
| [Fonctionnalités de cloud](azure-stack-validate-templates.md) | Utilisez cette fonctionnalités de cloud de module tooget hello d’un cloud. Par exemple, vous pouvez obtenir les capacités du cloud hello telles que la version de l’API, les ressources d’Azure Resource Manager, les extensions de machine virtuelle etc. pour la pile d’Azure et Azure cloud à l’aide de ce module. | Les administrateurs et les utilisateurs de cloud |
| [Administration de calcul Azure Stack](azure-stack-add-vm-image.md) | Utilisez cette tooadd module ou supprimer une image de machine virtuelle à partir du marketplace d’Azure pile hello. | Administrateurs de cloud. |
| [Administration de l’infrastructure Azure Stack](https://github.com/Azure/AzureStack-Tools/blob/master/Infrastructure/README.md) | Utilisez cette infrastructure de pile de Azure module toomanage machines virtuelles, des alertes, etc. les mises à jour. |  Administrateurs de cloud.|
| [Stratégie Resource Manager pour Azure Stack](azure-stack-policy-module.md) | Utiliser ce module de tooconfigure un abonnement Azure ou une ressource Azure de groupe avec hello même le contrôle de version et le service de disponibilité en tant que pile d’Azure. | Les administrateurs et les utilisateurs de cloud |
| [Inscription auprès d’Azure](azure-stack-register.md) | Utilisez cette tooregister module votre instance de kit de développement avec Azure. Une fois inscrit, vous pouvez télécharger des éléments du marketplace hello à partir d’Azure et les utiliser dans la pile de Azure. | Administrateurs de cloud |
| [Déploiement Azure Stack](azure-stack-run-powershell-script.md) | Utilisez cet ordinateur toodeploy de module tooprepare hello Azure pile hôte et redéployer l’aide de l’image de Disk(VHD) de disque dur virtuel de la pile Azure hello. | Administrateurs de cloud. |
| [Connexion tooAzure pile](azure-stack-connect-powershell.md) | Utilisez cette instance d’Azure pile module tooconnect tooan via PowerShell et tooconfigure tooAzure de connectivité VPN pile. | Les administrateurs et les utilisateurs de cloud |
| [Administration des services Azure Stack](azure-stack-create-offer.md) | Azure pile les administrateurs peuvent utiliser cette toocreate module offrent d’un client par défaut avec un quota illimité dans les services de calcul, stockage, réseau et le coffre de clés.   | Administrateurs de cloud.|
| [Validateur de modèle](azure-stack-validate-templates.md) | Utilisez cette tooverify module si un existant ou un nouveau modèle peut être déployé tooAzure pile. | Les administrateurs et les utilisateurs de cloud |


## <a name="next-steps"></a>Étapes suivantes
* [Configurer l’environnement de l’utilisateur hello pile d’Azure PowerShell](azure-stack-powershell-configure-user.md)   
* [Se connecter tooAzure Kit de développement de pile sur un réseau privé virtuel](azure-stack-connect-azure-stack.md)  
