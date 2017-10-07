---
title: "aaaEnable connexion Bureau à distance pour un rôle dans Azure Cloud Services à l’aide de PowerShell"
description: "Tooconfigure votre azure cloud application de service à l’aide de PowerShell tooallow les connexions Bureau à distance"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: bf2f70a4-20dc-4302-a91a-38cd7a2baa62
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 3f46b014f29f1c0be0e1b485d2f0152424162bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a>Activer une connexion Bureau à distance pour un rôle dans Azure Cloud Services avec PowerShell
> [!div class="op_single_selector"]
> * [Portail Azure](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Portail Azure Classic](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)
>
>

Bureau à distance vous permet de bureau de hello tooaccess d’un rôle en cours d’exécution dans Azure. Vous pouvez utiliser un tootroubleshoot de connexion Bureau à distance et diagnostiquer les problèmes avec votre application pendant son exécution.

Cet article décrit comment tooenable le Bureau à distance sur les rôles de votre Service Cloud à l’aide de PowerShell. Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour hello requis pour cet article. PowerShell utilise hello Extension Bureau à distance afin d’après que l’application hello est déployée, vous pouvez activer Bureau à distance.

## <a name="configure-remote-desktop-from-powershell"></a>Configurer le Bureau à distance à partir de PowerShell
Hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) applet de commande vous permet de tooenable Bureau à distance sur tous les rôles de votre déploiement de service cloud ou de rôles spécifiés. applet de commande Hello vous permet de spécifier hello nom d’utilisateur et mot de passe pour l’utilisateur du Bureau à distance hello via hello *informations d’identification* paramètre qui accepte un objet PSCredential.

Si vous utilisez PowerShell de manière interactive, vous pouvez facilement définir objet PSCredential de hello en appelant hello [Get-informations d’identification](https://technet.microsoft.com/library/hh849815.aspx) applet de commande.

```
$remoteusercredentials = Get-Credential
```

Cette commande affiche une boîte de dialogue permettant d’username hello tooenter et le mot de passe pour l’utilisateur distant de hello de manière sécurisée.

Étant donné que l’aide de PowerShell dans les scénarios d’automatisation, vous pouvez également configurer hello **PSCredential** objet d’une manière qui ne nécessite l’intervention de l’utilisateur. Tout d’abord, vous devez tooset un mot de passe sécurisé. Commencer avec la spécification d’un mot de passe en texte brut le convertir en chaîne sécurisée de tooa à l’aide de [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx). Ensuite, vous devez tooconvert cette chaîne sécurisée dans une chaîne chiffrée standard à l’aide de [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx). Vous pouvez maintenant enregistrer ce fichier tooa chaîne standard chiffrée à l’aide [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).

Vous pouvez également créer un fichier de mot de passe sécurisé afin que vous n’avez pas tootype mot de passe hello chaque fois. En outre, un fichier de mot de passe sécurisé est préférable à un fichier texte brut. Utilisez hello suivant PowerShell toocreate un fichier de mot de passe sécurisé :

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> Lorsque vous définissez un mot de passe hello, assurez-vous que vous remplissez hello [exigences de complexité](https://technet.microsoft.com/library/cc786468.aspx).
>
>

objet d’informations d’identification du hello toocreate à partir du fichier de mot de passe sécurisé hello, vous devez lire le contenu du fichier hello et convertissez-les tooa arrière sécuriser à l’aide de la chaîne [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).

Hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) applet de commande accepte également une *Expiration* paramètre qui spécifie un **DateTime** utilisateur hello compte expire. Par exemple, vous pouvez définir hello compte tooexpire quelques jours à partir de hello date et heure actuelles.

Cet exemple PowerShell vous montre comment tooset hello Extension Bureau à distance sur un service cloud :

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
Vous pouvez spécifier emplacement de déploiement hello et les rôles que vous voulez le Bureau à distance de tooenable sur. Si ces paramètres ne sont pas spécifiés, hello permet d’activer Bureau à distance sur tous les rôles de hello **Production** emplacement de déploiement.

Hello extension du Bureau à distance est associé à un déploiement. Si vous créez un nouveau déploiement de service de hello, vous disposez Bureau à distance de tooenable sur ce déploiement. Si vous souhaitez toujours toohave Bureau à distance est activé, vous devez envisager l’intégration de scripts PowerShell de hello dans votre flux de travail de déploiement.

## <a name="remote-desktop-into-a-role-instance"></a>Bureau à distance dans une instance de rôle
Hello [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) applet de commande est bureau tooremote utilisé dans une instance de rôle spécifique de votre service cloud. Vous pouvez utiliser hello *LocalPath* hello toodownload de paramètre RDP fichier localement. Vous pouvez également utiliser hello *lancer* tooaccess de la boîte de dialogue paramètre toodirectly lancement hello connexion Bureau à distance hello instance de rôle de service cloud.

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a>Vérifiez si l’extension des services de Bureau à distance est activée sur un service
Hello [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) affiche des applets de commande Bureau à distance est activé ou désactivé sur un déploiement de service. applet de commande Hello retourne hello les nom d’utilisateur pour l’utilisateur hello de bureau à distance et les rôles de hello prenant en charge l’extension hello de bureau à distance pour. Par défaut, cela se produit sur l’emplacement de déploiement hello et vous pouvez choisir hello toouse staging emplacement à la place.

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a>Supprimer l’extension de bureau distant d’un service
Si vous avez déjà activé extension de bureau à distance hello sur un déploiement, et devez tooupdate hello paramètres Bureau à distance, tout d’abord supprimer les extension hello. Et activez de nouveau avec les nouveaux paramètres de hello. Par exemple, si vous voulez tooset un nouveau mot de passe pour le compte d’utilisateur distant hello ou hello compte a expiré. Cette opération est requise sur les déploiements existants qui ont l’extension Bureau à distance hello activée. Pour les nouveaux déploiements, vous pouvez simplement appliquer hello extension directement.

tooremove hello bureau extension distant du déploiement de hello, vous pouvez utiliser hello [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) applet de commande. Vous pouvez éventuellement spécifier d’emplacement de déploiement hello et le rôle à partir de laquelle vous souhaitez l’extension tooremove hello de bureau à distance.

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> configuration d’extension hello toocompletely supprimer, vous devez appeler hello *supprimer* applet de commande avec hello **UninstallConfiguration** paramètre.
>
> Hello **UninstallConfiguration** paramètre désinstalle toute configuration de l’extension qui est appliqué toohello service. Chaque configuration de l’extension est associée à la configuration du service hello. Appel hello *supprimer* applet de commande sans **UninstallConfiguration** dissocie hello <mark>déploiement</mark> à partir de la configuration de l’extension hello, donc supprimer efficacement extension de Hello. Toutefois, la configuration de l’extension hello reste associée au service de hello.
>
>

## <a name="additional-resources"></a>Ressources supplémentaires

[Comment tooConfigure Services de cloud computing](cloud-services-how-to-configure.md)
[Cloud FAQ - des services Bureau à distance](cloud-services-faq.md)
