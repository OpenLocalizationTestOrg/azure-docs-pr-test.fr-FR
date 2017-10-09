---
title: profils de version aaaUsing API dans la pile de Azure | Documents Microsoft
description: "En savoir plus sur les profils de version des API dans Azure Stack."
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
ms.date: 03/21/2017
ms.author: sngun
ms.openlocfilehash: cb54a683054f08fd123bcb6245d88aaa30c29882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-api-version-profiles-in-azure-stack"></a>Gérer les profils de version des API dans Azure Stack

Profils de version d’API fournissent une toomanage de façon les différences de version entre Azure et de la pile de Azure. Un profil de version d’API est un ensemble de modules PowerShell AzureRM avec des versions d’API spécifiques. Chaque plateforme cloud a un ensemble de profils de version d’API pris en charge. Par exemple, Azure pile prend en charge une version de profil ayant une date spécifique tel que **2017-03-09-profil**et prend en charge Azure hello **dernière** profil de version d’API. Lorsque vous installez un profil, hello modules AzureRM PowerShell qui correspondent toohello spécifié profil sont installés.

## <a name="install-hello-powershell-module-required-toouse-api-version-profiles"></a>Installer des profils de version hello PowerShell module requis toouse API

Hello **AzureRM.Bootstrapper** module qui est disponible via hello PowerShell Gallery fournit les applets de commande PowerShell qui sont requis toowork avec des profils de version d’API. Utilisez hello suivant du module de AzureRM.Bootstrapper hello applet de commande tooinstall :

```PowerShell
Install-Module -Name AzureRm.BootStrapper
```
module de AzureRM.Bootstrapper Hello est en version préliminaire ; détails et les fonctionnalités sont toochange de sujet. toodownload et installez hello version la plus récente de ce module de hello PowerShell Gallery, exécutez hello suivant l’applet de commande :

```PowerShell
Update-Module -Name "AzureRm.BootStrapper"
```

## <a name="install-a-profile"></a>Installer un profil

Hello d’utilisation **Install-AzureRmProfile** applet de commande avec hello **2017-03-09-profil** API version profil tooinstall hello Azure Resource Manager modules requis par la pile de Azure. Notez que les modules hello Azure pile cloud administrateur ne sont pas installés avec ce profil de la version API, et ils doivent être installés séparément comme spécifié dans hello étape 3 de hello [installer PowerShell pour Azure pile](azure-stack-powershell-install.md) l’article.

```PowerShell 
Install-AzureRMProfile -Profile 2017-03-09-profile
```
## <a name="install-and-import-modules-in-a-profile"></a>Installer et importer des modules dans un profil

Hello d’utilisation **AzureRmProfile-utilisez** applet de commande tooinstall et importer les modules qui sont associés à un profil de la version API. Vous pouvez importer un seul profil de version d’API dans une session PowerShell. profil de version tooimport une autre API, vous devez ouvrir une nouvelle session PowerShell. applet de commande Hello utilisation-AzureRMProfile exécute hello tâches suivantes :  
1. Vérifie si les modules PowerShell hello associés hello spécifié le profil de version d’API est installés dans l’étendue actuelle de hello.  
2. Télécharge et installe les modules hello s’ils ne sont pas déjà installés.   
3. Importations hello modules dans la session PowerShell en cours de hello. 

```PowerShell
# Installs and imports hello specified API version profile into hello current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser

# Installs and imports hello specified API version profile into hello current PowerShell session without any prompts
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser -Force
```

tooinstall et importation sélectionné les modules Azure Resource Manager à partir d’un profil de version d’API, exécuter l’applet de commande hello AzureRMProfile à l’utilisation par hello **Module** paramètre :

```PowerShell
# Installs and imports hello compute, Storage and Network modules from hello specified API version profile into your current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Module AzureRM.Compute, AzureRM.Storage, AzureRM.Network
```

## <a name="get-hello-installed-profiles"></a>Obtenir les profils de hello installé

Hello d’utilisation **Get-AzureRmProfile** applet de commande tooget hello liste API version profils disponibles : 

```PowerShell
# lists all API version profiles provided by hello AzureRM.BootStrapper module.
Get-AzureRmProfile -ListAvailable 

# lists hello API version profiles which are installed on your machine
Get-AzureRmProfile
```
## <a name="update-profiles"></a>Mettre à jour des profils

Hello d’utilisation **AzureRmProfile de mise à jour** modules de hello tooupdate applet de commande dans une version profil toohello dernière version de l’API des modules qui sont disponibles dans hello PSGallery. Il est recommandé de tooalways exécuter hello **AzureRmProfile de mise à jour** applet de commande dans une nouvelle tooavoid de session PowerShell est en conflit lors de l’importation de modules. applet de commande Hello AzureRmProfile de mise à jour s’exécute hello tâches suivantes :

1. Vérifie si hello dernières versions des modules sont installées dans hello donnée de profil de version d’API pour l’étendue actuelle de hello.  
2. Vous invite tooinstall s’ils ne sont pas déjà installés.  
3. Installe et importe les modules de hello mis à jour dans la session PowerShell en cours de hello.  

```PowerShell
Update-AzureRmProfile -Profile 2017-03-09-profile
```

tooremove les versions hello précédemment installé des modules hello avant la mise à jour toohello version la plus récente, utiliser l’applet de commande hello AzureRmProfile de mise à jour en même temps que hello **- RemovePreviousVersions** paramètre :

```PowerShell 
Update-AzureRmProfile -Profile 2017-03-09-profile -RemovePreviousVersions
```

Cette applet de commande exécute hello tâches suivantes :  

1. Vérifie si hello dernières versions des modules sont installées dans hello donnée de profil de version d’API pour l’étendue actuelle de hello.  
2. Supprime hello anciennes versions de modules à partir du profil de version API hello actuel et dans la session PowerShell en cours de hello.  
4. vous demande la version la plus récente tooinstall hello.  
5. Installe et importe les modules de hello mis à jour dans la session PowerShell en cours de hello.  
 
## <a name="uninstall-profiles"></a>Désinstaller des profils

Hello d’utilisation **AzureRmProfile de désinstallation** applet de commande toouninstall hello spécifié le profil de version d’API.

```PowerShell 
Uninstall-AzureRmProfile -Profile 2017-03-09-profile
```

## <a name="next-steps"></a>Étapes suivantes
* [Installer PowerShell pour Azure Stack](azure-stack-powershell-install.md)
* [Configurer l’environnement de l’utilisateur hello pile d’Azure PowerShell](azure-stack-powershell-configure-user.md)  
