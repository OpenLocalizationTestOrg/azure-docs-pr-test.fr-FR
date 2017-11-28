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
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="6540e-103">Activer une connexion Bureau à distance pour un rôle dans Azure Cloud Services avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="6540e-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6540e-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="6540e-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="6540e-105">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="6540e-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="6540e-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6540e-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="6540e-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6540e-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="6540e-108">Bureau à distance vous permet de bureau de hello tooaccess d’un rôle en cours d’exécution dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6540e-108">Remote Desktop enables you tooaccess hello desktop of a role running in Azure.</span></span> <span data-ttu-id="6540e-109">Vous pouvez utiliser un tootroubleshoot de connexion Bureau à distance et diagnostiquer les problèmes avec votre application pendant son exécution.</span><span class="sxs-lookup"><span data-stu-id="6540e-109">You can use a Remote Desktop connection tootroubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="6540e-110">Cet article décrit comment tooenable le Bureau à distance sur les rôles de votre Service Cloud à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6540e-110">This article describes how tooenable remote desktop on your Cloud Service Roles using PowerShell.</span></span> <span data-ttu-id="6540e-111">Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour hello requis pour cet article.</span><span class="sxs-lookup"><span data-stu-id="6540e-111">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span> <span data-ttu-id="6540e-112">PowerShell utilise hello Extension Bureau à distance afin d’après que l’application hello est déployée, vous pouvez activer Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="6540e-112">PowerShell utilizes hello Remote Desktop Extension so you can enable Remote Desktop after hello application is deployed.</span></span>

## <a name="configure-remote-desktop-from-powershell"></a><span data-ttu-id="6540e-113">Configurer le Bureau à distance à partir de PowerShell</span><span class="sxs-lookup"><span data-stu-id="6540e-113">Configure Remote Desktop from PowerShell</span></span>
<span data-ttu-id="6540e-114">Hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) applet de commande vous permet de tooenable Bureau à distance sur tous les rôles de votre déploiement de service cloud ou de rôles spécifiés.</span><span class="sxs-lookup"><span data-stu-id="6540e-114">hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet allows you tooenable Remote Desktop on specified roles or all roles of your cloud service deployment.</span></span> <span data-ttu-id="6540e-115">applet de commande Hello vous permet de spécifier hello nom d’utilisateur et mot de passe pour l’utilisateur du Bureau à distance hello via hello *informations d’identification* paramètre qui accepte un objet PSCredential.</span><span class="sxs-lookup"><span data-stu-id="6540e-115">hello cmdlet lets you specify hello Username and Password for hello remote desktop user through hello *Credential* parameter that accepts a PSCredential object.</span></span>

<span data-ttu-id="6540e-116">Si vous utilisez PowerShell de manière interactive, vous pouvez facilement définir objet PSCredential de hello en appelant hello [Get-informations d’identification](https://technet.microsoft.com/library/hh849815.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="6540e-116">If you are using PowerShell interactively, you can easily set hello PSCredential object by calling hello [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

```
$remoteusercredentials = Get-Credential
```

<span data-ttu-id="6540e-117">Cette commande affiche une boîte de dialogue permettant d’username hello tooenter et le mot de passe pour l’utilisateur distant de hello de manière sécurisée.</span><span class="sxs-lookup"><span data-stu-id="6540e-117">This command displays a dialog box allowing you tooenter hello username and password for hello remote user in a secure manner.</span></span>

<span data-ttu-id="6540e-118">Étant donné que l’aide de PowerShell dans les scénarios d’automatisation, vous pouvez également configurer hello **PSCredential** objet d’une manière qui ne nécessite l’intervention de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6540e-118">Since PowerShell helps in automation scenarios, you can also set up hello **PSCredential** object in a way that doesn't require user interaction.</span></span> <span data-ttu-id="6540e-119">Tout d’abord, vous devez tooset un mot de passe sécurisé.</span><span class="sxs-lookup"><span data-stu-id="6540e-119">First, you need tooset up a secure password.</span></span> <span data-ttu-id="6540e-120">Commencer avec la spécification d’un mot de passe en texte brut le convertir en chaîne sécurisée de tooa à l’aide de [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="6540e-120">You begin with specifying a plain text password convert it tooa secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span> <span data-ttu-id="6540e-121">Ensuite, vous devez tooconvert cette chaîne sécurisée dans une chaîne chiffrée standard à l’aide de [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span><span class="sxs-lookup"><span data-stu-id="6540e-121">Next you need tooconvert this secure string into an encrypted standard string using [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span></span> <span data-ttu-id="6540e-122">Vous pouvez maintenant enregistrer ce fichier tooa chaîne standard chiffrée à l’aide [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span><span class="sxs-lookup"><span data-stu-id="6540e-122">Now you can save this encrypted standard string tooa file using [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span></span>

<span data-ttu-id="6540e-123">Vous pouvez également créer un fichier de mot de passe sécurisé afin que vous n’avez pas tootype mot de passe hello chaque fois.</span><span class="sxs-lookup"><span data-stu-id="6540e-123">You can also create a secure password file so that you don't have tootype in hello password every time.</span></span> <span data-ttu-id="6540e-124">En outre, un fichier de mot de passe sécurisé est préférable à un fichier texte brut.</span><span class="sxs-lookup"><span data-stu-id="6540e-124">Also, a secure password file is better than a plain text file.</span></span> <span data-ttu-id="6540e-125">Utilisez hello suivant PowerShell toocreate un fichier de mot de passe sécurisé :</span><span class="sxs-lookup"><span data-stu-id="6540e-125">Use hello following PowerShell toocreate a secure password file:</span></span>

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> <span data-ttu-id="6540e-126">Lorsque vous définissez un mot de passe hello, assurez-vous que vous remplissez hello [exigences de complexité](https://technet.microsoft.com/library/cc786468.aspx).</span><span class="sxs-lookup"><span data-stu-id="6540e-126">When setting hello password, make sure that you meet hello [complexity requirements](https://technet.microsoft.com/library/cc786468.aspx).</span></span>
>
>

<span data-ttu-id="6540e-127">objet d’informations d’identification du hello toocreate à partir du fichier de mot de passe sécurisé hello, vous devez lire le contenu du fichier hello et convertissez-les tooa arrière sécuriser à l’aide de la chaîne [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="6540e-127">toocreate hello credential object from hello secure password file, you must read hello file contents and convert them back tooa secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span>

<span data-ttu-id="6540e-128">Hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) applet de commande accepte également une *Expiration* paramètre qui spécifie un **DateTime** utilisateur hello compte expire.</span><span class="sxs-lookup"><span data-stu-id="6540e-128">hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet also accepts an *Expiration* parameter, which specifies a **DateTime** at which hello user account expires.</span></span> <span data-ttu-id="6540e-129">Par exemple, vous pouvez définir hello compte tooexpire quelques jours à partir de hello date et heure actuelles.</span><span class="sxs-lookup"><span data-stu-id="6540e-129">For example, you could set hello account tooexpire a few days from hello current date and time.</span></span>

<span data-ttu-id="6540e-130">Cet exemple PowerShell vous montre comment tooset hello Extension Bureau à distance sur un service cloud :</span><span class="sxs-lookup"><span data-stu-id="6540e-130">This PowerShell example shows you how tooset hello Remote Desktop Extension on a cloud service:</span></span>

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
<span data-ttu-id="6540e-131">Vous pouvez spécifier emplacement de déploiement hello et les rôles que vous voulez le Bureau à distance de tooenable sur.</span><span class="sxs-lookup"><span data-stu-id="6540e-131">You can also optionally specify hello deployment slot and roles that you want tooenable remote desktop on.</span></span> <span data-ttu-id="6540e-132">Si ces paramètres ne sont pas spécifiés, hello permet d’activer Bureau à distance sur tous les rôles de hello **Production** emplacement de déploiement.</span><span class="sxs-lookup"><span data-stu-id="6540e-132">If these parameters are not specified, hello cmdlet enables remote desktop on all roles in hello **Production** deployment slot.</span></span>

<span data-ttu-id="6540e-133">Hello extension du Bureau à distance est associé à un déploiement.</span><span class="sxs-lookup"><span data-stu-id="6540e-133">hello Remote Desktop extension is associated with a deployment.</span></span> <span data-ttu-id="6540e-134">Si vous créez un nouveau déploiement de service de hello, vous disposez Bureau à distance de tooenable sur ce déploiement.</span><span class="sxs-lookup"><span data-stu-id="6540e-134">If you create a new deployment for hello service, you have tooenable remote desktop on that deployment.</span></span> <span data-ttu-id="6540e-135">Si vous souhaitez toujours toohave Bureau à distance est activé, vous devez envisager l’intégration de scripts PowerShell de hello dans votre flux de travail de déploiement.</span><span class="sxs-lookup"><span data-stu-id="6540e-135">If you always want toohave remote desktop enabled, then you should consider integrating hello PowerShell scripts into your deployment workflow.</span></span>

## <a name="remote-desktop-into-a-role-instance"></a><span data-ttu-id="6540e-136">Bureau à distance dans une instance de rôle</span><span class="sxs-lookup"><span data-stu-id="6540e-136">Remote Desktop into a role instance</span></span>
<span data-ttu-id="6540e-137">Hello [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) applet de commande est bureau tooremote utilisé dans une instance de rôle spécifique de votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="6540e-137">hello [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet is used tooremote desktop into a specific role instance of your cloud service.</span></span> <span data-ttu-id="6540e-138">Vous pouvez utiliser hello *LocalPath* hello toodownload de paramètre RDP fichier localement.</span><span class="sxs-lookup"><span data-stu-id="6540e-138">You can use hello *LocalPath* parameter toodownload hello RDP file locally.</span></span> <span data-ttu-id="6540e-139">Vous pouvez également utiliser hello *lancer* tooaccess de la boîte de dialogue paramètre toodirectly lancement hello connexion Bureau à distance hello instance de rôle de service cloud.</span><span class="sxs-lookup"><span data-stu-id="6540e-139">Or you can use hello *Launch* parameter toodirectly launch hello Remote Desktop Connection dialog tooaccess hello cloud service role instance.</span></span>

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a><span data-ttu-id="6540e-140">Vérifiez si l’extension des services de Bureau à distance est activée sur un service</span><span class="sxs-lookup"><span data-stu-id="6540e-140">Check if Remote Desktop extension is enabled on a service</span></span>
<span data-ttu-id="6540e-141">Hello [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) affiche des applets de commande Bureau à distance est activé ou désactivé sur un déploiement de service.</span><span class="sxs-lookup"><span data-stu-id="6540e-141">hello [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet displays that remote desktop is enabled or disabled on a service deployment.</span></span> <span data-ttu-id="6540e-142">applet de commande Hello retourne hello les nom d’utilisateur pour l’utilisateur hello de bureau à distance et les rôles de hello prenant en charge l’extension hello de bureau à distance pour.</span><span class="sxs-lookup"><span data-stu-id="6540e-142">hello cmdlet returns hello username for hello remote desktop user and hello roles that hello remote desktop extension is enabled for.</span></span> <span data-ttu-id="6540e-143">Par défaut, cela se produit sur l’emplacement de déploiement hello et vous pouvez choisir hello toouse staging emplacement à la place.</span><span class="sxs-lookup"><span data-stu-id="6540e-143">By default, this happens on hello deployment slot and you can choose toouse hello staging slot instead.</span></span>

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a><span data-ttu-id="6540e-144">Supprimer l’extension de bureau distant d’un service</span><span class="sxs-lookup"><span data-stu-id="6540e-144">Remove Remote Desktop extension from a service</span></span>
<span data-ttu-id="6540e-145">Si vous avez déjà activé extension de bureau à distance hello sur un déploiement, et devez tooupdate hello paramètres Bureau à distance, tout d’abord supprimer les extension hello.</span><span class="sxs-lookup"><span data-stu-id="6540e-145">If you have already enabled hello remote desktop extension on a deployment, and need tooupdate hello remote desktop settings, first remove hello extension.</span></span> <span data-ttu-id="6540e-146">Et activez de nouveau avec les nouveaux paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="6540e-146">And enable it again with hello new settings.</span></span> <span data-ttu-id="6540e-147">Par exemple, si vous voulez tooset un nouveau mot de passe pour le compte d’utilisateur distant hello ou hello compte a expiré.</span><span class="sxs-lookup"><span data-stu-id="6540e-147">For example, if you want tooset a new password for hello remote user account, or hello account expired.</span></span> <span data-ttu-id="6540e-148">Cette opération est requise sur les déploiements existants qui ont l’extension Bureau à distance hello activée.</span><span class="sxs-lookup"><span data-stu-id="6540e-148">Doing this is required on existing deployments that have hello remote desktop extension enabled.</span></span> <span data-ttu-id="6540e-149">Pour les nouveaux déploiements, vous pouvez simplement appliquer hello extension directement.</span><span class="sxs-lookup"><span data-stu-id="6540e-149">For new deployments, you can simply apply hello extension directly.</span></span>

<span data-ttu-id="6540e-150">tooremove hello bureau extension distant du déploiement de hello, vous pouvez utiliser hello [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="6540e-150">tooremove hello remote desktop extension from hello deployment, you can use hello [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="6540e-151">Vous pouvez éventuellement spécifier d’emplacement de déploiement hello et le rôle à partir de laquelle vous souhaitez l’extension tooremove hello de bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="6540e-151">You can also optionally specify hello deployment slot and role from which you want tooremove hello remote desktop extension.</span></span>

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> <span data-ttu-id="6540e-152">configuration d’extension hello toocompletely supprimer, vous devez appeler hello *supprimer* applet de commande avec hello **UninstallConfiguration** paramètre.</span><span class="sxs-lookup"><span data-stu-id="6540e-152">toocompletely remove hello extension configuration, you should call hello *remove* cmdlet with hello **UninstallConfiguration** parameter.</span></span>
>
> <span data-ttu-id="6540e-153">Hello **UninstallConfiguration** paramètre désinstalle toute configuration de l’extension qui est appliqué toohello service.</span><span class="sxs-lookup"><span data-stu-id="6540e-153">hello **UninstallConfiguration** parameter uninstalls any extension configuration that is applied toohello service.</span></span> <span data-ttu-id="6540e-154">Chaque configuration de l’extension est associée à la configuration du service hello.</span><span class="sxs-lookup"><span data-stu-id="6540e-154">Every extension configuration is associated with hello service configuration.</span></span> <span data-ttu-id="6540e-155">Appel hello *supprimer* applet de commande sans **UninstallConfiguration** dissocie hello <mark>déploiement</mark> à partir de la configuration de l’extension hello, donc supprimer efficacement extension de Hello.</span><span class="sxs-lookup"><span data-stu-id="6540e-155">Calling hello *remove* cmdlet without **UninstallConfiguration** disassociates hello <mark>deployment</mark> from hello extension configuration, thus effectively removing hello extension.</span></span> <span data-ttu-id="6540e-156">Toutefois, la configuration de l’extension hello reste associée au service de hello.</span><span class="sxs-lookup"><span data-stu-id="6540e-156">However, hello extension configuration remains associated with hello service.</span></span>
>
>

## <a name="additional-resources"></a><span data-ttu-id="6540e-157">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="6540e-157">Additional resources</span></span>

<span data-ttu-id="6540e-158">[Comment tooConfigure Services de cloud computing](cloud-services-how-to-configure.md)
[Cloud FAQ - des services Bureau à distance](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="6540e-158">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
