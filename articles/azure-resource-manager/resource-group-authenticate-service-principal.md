---
title: "identité aaaCreate pour une application Azure avec PowerShell | Documents Microsoft"
description: "Décrit comment contrôlent les toouse Azure PowerShell toocreate une application Azure Active Directory et principal du service et accordez il accéder tooresources via l’accès en fonction du rôle. Il montre comment application tooauthenticate avec un mot de passe ou un certificat."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: d2caf121-9fbe-4f00-bf9d-8f3d1f00a6ff
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: c534360799b590054a051e4426e5e27dccb559b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toocreate-a-service-principal-tooaccess-resources"></a><span data-ttu-id="05bc0-104">Utiliser Azure PowerShell toocreate une ressources tooaccess principal du service</span><span class="sxs-lookup"><span data-stu-id="05bc0-104">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>

<span data-ttu-id="05bc0-105">Lorsque vous avez une application ou un script nécessitant des ressources de tooaccess, vous pouvez configurer une identité pour l’application hello et authentifier l’application hello avec ses propres informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="05bc0-105">When you have an app or script that needs tooaccess resources, you can set up an identity for hello app and authenticate hello app with its own credentials.</span></span> <span data-ttu-id="05bc0-106">Cette identité est connue en tant que principal de service.</span><span class="sxs-lookup"><span data-stu-id="05bc0-106">This identity is known as a service principal.</span></span> <span data-ttu-id="05bc0-107">Cette approche vous permet d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="05bc0-107">This approach enables you to:</span></span>

* <span data-ttu-id="05bc0-108">Affecter des autorisations identité d’application toohello différents de vos propres autorisations.</span><span class="sxs-lookup"><span data-stu-id="05bc0-108">Assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="05bc0-109">En règle générale, ces autorisations sont limitée tooexactly quelle application hello doit toodo.</span><span class="sxs-lookup"><span data-stu-id="05bc0-109">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="05bc0-110">Utilisez un certificat pour l’authentification lors de l’exécution d’un script sans assistance.</span><span class="sxs-lookup"><span data-stu-id="05bc0-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="05bc0-111">Cette rubrique vous montre comment toouse [Azure PowerShell](/powershell/azure/overview) tooset installé tout ce dont vous avez besoin pour une toorun application sous ses propres informations d’identification et l’identité.</span><span class="sxs-lookup"><span data-stu-id="05bc0-111">This topic shows you how toouse [Azure PowerShell](/powershell/azure/overview) tooset up everything you need for an application toorun under its own credentials and identity.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="05bc0-112">Autorisations requises</span><span class="sxs-lookup"><span data-stu-id="05bc0-112">Required permissions</span></span>
<span data-ttu-id="05bc0-113">toocomplete cette rubrique, vous devez disposer des autorisations suffisantes dans Azure Active Directory et votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="05bc0-113">toocomplete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="05bc0-114">Plus précisément, vous devez être en mesure de toocreate une application Bonjour Azure Active Directory et affecter des rôle tooa principal du service hello.</span><span class="sxs-lookup"><span data-stu-id="05bc0-114">Specifically, you must be able toocreate an app in hello Azure Active Directory, and assign hello service principal tooa role.</span></span> 

<span data-ttu-id="05bc0-115">Hello toocheck de façon plus simple si votre compte dispose des autorisations adéquates est via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="05bc0-115">hello easiest way toocheck whether your account has adequate permissions is through hello portal.</span></span> <span data-ttu-id="05bc0-116">Consultez [Vérifier l’autorisation requise](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="05bc0-116">See [Check required permission](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="05bc0-117">Maintenant, section tooa pour l’authentification avec :</span><span class="sxs-lookup"><span data-stu-id="05bc0-117">Now, proceed tooa section for authenticating with:</span></span>

* [<span data-ttu-id="05bc0-118">mot de passe</span><span class="sxs-lookup"><span data-stu-id="05bc0-118">password</span></span>](#create-service-principal-with-password)
* [<span data-ttu-id="05bc0-119">certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="05bc0-119">self-signed certificate</span></span>](#create-service-principal-with-self-signed-certificate)
* [<span data-ttu-id="05bc0-120">certificat délivré par une autorité de certification</span><span class="sxs-lookup"><span data-stu-id="05bc0-120">certificate from Certificate Authority</span></span>](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a><span data-ttu-id="05bc0-121">Commandes PowerShell</span><span class="sxs-lookup"><span data-stu-id="05bc0-121">PowerShell commands</span></span>

<span data-ttu-id="05bc0-122">tooset d’un service principal, utilisez :</span><span class="sxs-lookup"><span data-stu-id="05bc0-122">tooset up a service principal, you use:</span></span>

| <span data-ttu-id="05bc0-123">Commande</span><span class="sxs-lookup"><span data-stu-id="05bc0-123">Command</span></span> | <span data-ttu-id="05bc0-124">Description</span><span class="sxs-lookup"><span data-stu-id="05bc0-124">Description</span></span> |
| ------- | ----------- | 
| [<span data-ttu-id="05bc0-125">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="05bc0-125">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="05bc0-126">Crée un principal de service Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05bc0-126">Creates an Azure Active Directory service principal</span></span> |
| [<span data-ttu-id="05bc0-127">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="05bc0-127">New-AzureRmRoleAssignment</span></span>](/powershell/module/azurerm.resources/new-azurermroleassignment) | <span data-ttu-id="05bc0-128">Assigne hello spécifiées RBAC rôle toohello spécifié principal, au hello étendue.</span><span class="sxs-lookup"><span data-stu-id="05bc0-128">Assigns hello specified RBAC role toohello specified principal, at hello specified scope.</span></span> |


## <a name="create-service-principal-with-password"></a><span data-ttu-id="05bc0-129">Créer un principal du service avec un mot de passe</span><span class="sxs-lookup"><span data-stu-id="05bc0-129">Create service principal with password</span></span>

<span data-ttu-id="05bc0-130">toocreate un principal de service avec le rôle de collaborateur hello pour votre abonnement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="05bc0-130">toocreate a service principal with hello Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="05bc0-131">exemple de Hello mise en veille tooallow de 20 secondes du temps pour hello de nouveau service principal toopropagate dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="05bc0-131">hello example sleeps for 20 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="05bc0-132">Si votre script n’attend pas suffisamment longtemps, vous voyez une erreur indiquant : « PrincipalNotFound : Principal {id} n’existe pas dans le répertoire de hello. »</span><span class="sxs-lookup"><span data-stu-id="05bc0-132">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>

<span data-ttu-id="05bc0-133">Hello script suivant vous permet de toospecify une portée différente d’abonnement par défaut de hello et nouvelles tentatives hello attribution de rôle si une erreur se produit :</span><span class="sxs-lookup"><span data-stu-id="05bc0-133">hello following script enables you toospecify a scope other than hello default subscription, and retries hello role assignment if an error occurs:</span></span>

```powershell
Param (

 # Use tooset scope tooresource group. If no value is provided, scope is set toosubscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use tooset subscription. If no value is provided, default subscription is used. 
 [Parameter(Mandatory=$false)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName,

 [Parameter(Mandatory=$true)]
 [String] $Password
)

 Login-AzureRmAccount
 Import-Module AzureRM.Resources

 if ($SubscriptionId -eq "") 
 {
    $SubscriptionId = (Get-AzureRmContext).Subscription.Id
 }
 else
 {
    Set-AzureRmContext -SubscriptionId $SubscriptionId
 }

 if ($ResourceGroup -eq "")
 {
    $Scope = "/subscriptions/" + $SubscriptionId
 }
 else
 {
    $Scope = (Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop).ResourceId
 }

 
 # Create Service Principal for hello AD app
 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

<span data-ttu-id="05bc0-134">Quelques éléments toonote, sur le script de hello :</span><span class="sxs-lookup"><span data-stu-id="05bc0-134">A few items toonote about hello script:</span></span>

* <span data-ttu-id="05bc0-135">toogrant hello identité accès toohello abonnement par défaut vous n’avez pas besoin tooprovide les paramètres de groupe de ressources ou d’ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="05bc0-135">toogrant hello identity access toohello default subscription, you do not need tooprovide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="05bc0-136">Spécifiez le paramètre de groupe de ressources hello uniquement lorsque vous souhaitez étendue de hello toolimit hello rôle affectation tooa du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="05bc0-136">Specify hello ResourceGroup parameter only when you want toolimit hello scope of hello role assignment tooa resource group.</span></span>
*  <span data-ttu-id="05bc0-137">Dans cet exemple, vous ajoutez rôle de collaborateur hello service toohello principal.</span><span class="sxs-lookup"><span data-stu-id="05bc0-137">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="05bc0-138">Pour les autres rôles, voir [RBAC : rôles intégrés](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="05bc0-138">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="05bc0-139">script de Hello mise en veille tooallow de 15 secondes du temps pour hello de nouveau service principal toopropagate dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="05bc0-139">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="05bc0-140">Si votre script n’attend pas suffisamment longtemps, vous voyez une erreur indiquant : « PrincipalNotFound : Principal {id} n’existe pas dans le répertoire de hello. »</span><span class="sxs-lookup"><span data-stu-id="05bc0-140">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="05bc0-141">Si vous avez besoin d’abonnements de toomore toogrant hello service principal l’accès ou les groupes de ressources, exécutez hello `New-AzureRMRoleAssignment` applet de commande avec des portées différentes.</span><span class="sxs-lookup"><span data-stu-id="05bc0-141">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>


### <a name="provide-credentials-through-powershell"></a><span data-ttu-id="05bc0-142">Fournir des informations d’identification via PowerShell</span><span class="sxs-lookup"><span data-stu-id="05bc0-142">Provide credentials through PowerShell</span></span>
<span data-ttu-id="05bc0-143">Maintenant, vous devez toolog dans en tant qu’opérations de tooperform application hello.</span><span class="sxs-lookup"><span data-stu-id="05bc0-143">Now, you need toolog in as hello application tooperform operations.</span></span> <span data-ttu-id="05bc0-144">Pour nom d’utilisateur hello, utilisez hello `ApplicationId` que vous avez créé pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="05bc0-144">For hello user name, use hello `ApplicationId` that you created for hello application.</span></span> <span data-ttu-id="05bc0-145">Mot de passe hello, utilisez hello une que vous avez spécifié lors de la création du compte de hello.</span><span class="sxs-lookup"><span data-stu-id="05bc0-145">For hello password, use hello one you specified when creating hello account.</span></span> 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

<span data-ttu-id="05bc0-146">ID de client Hello n’est pas sensible, vous pouvez l’incorporer directement dans votre script.</span><span class="sxs-lookup"><span data-stu-id="05bc0-146">hello tenant ID is not sensitive, so you can embed it directly in your script.</span></span> <span data-ttu-id="05bc0-147">Si vous avez besoin d’ID de client hello tooretrieve, utilisez :</span><span class="sxs-lookup"><span data-stu-id="05bc0-147">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a><span data-ttu-id="05bc0-148">Créer un principal du service avec un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="05bc0-148">Create service principal with self-signed certificate</span></span>

<span data-ttu-id="05bc0-149">toocreate un principal de service avec un certificat auto-signé et le rôle de collaborateur hello pour votre abonnement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="05bc0-149">toocreate a service principal with a self-signed certificate and hello Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="05bc0-150">exemple de Hello mise en veille tooallow de 20 secondes du temps pour hello de nouveau service principal toopropagate dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="05bc0-150">hello example sleeps for 20 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="05bc0-151">Si votre script n’attend pas suffisamment longtemps, vous voyez une erreur indiquant : « PrincipalNotFound : Principal {id} n’existe pas dans le répertoire de hello. »</span><span class="sxs-lookup"><span data-stu-id="05bc0-151">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>

<span data-ttu-id="05bc0-152">Hello script suivant vous permet de toospecify une portée différente d’abonnement par défaut de hello et nouvelles tentatives hello attribution de rôle si une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="05bc0-152">hello following script enables you toospecify a scope other than hello default subscription, and retries hello role assignment if an error occurs.</span></span> <span data-ttu-id="05bc0-153">Vous devez disposer d’Azure PowerShell 2.0 sur Windows 10 ou Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="05bc0-153">You must have Azure PowerShell 2.0 on Windows 10 or Windows Server 2016.</span></span>

```powershell
Param (

 # Use tooset scope tooresource group. If no value is provided, scope is set toosubscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use tooset subscription. If no value is provided, default subscription is used. 
 [Parameter(Mandatory=$false)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName
 )

 Login-AzureRmAccount
 Import-Module AzureRM.Resources

 if ($SubscriptionId -eq "") 
 {
    $SubscriptionId = (Get-AzureRmContext).Subscription.Id
 }
 else
 {
    Set-AzureRmContext -SubscriptionId $SubscriptionId
 }

 if ($ResourceGroup -eq "")
 {
    $Scope = "/subscriptions/" + $SubscriptionId
 }
 else
 {
    $Scope = (Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop).ResourceId
 }

 $cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
 $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

<span data-ttu-id="05bc0-154">Quelques éléments toonote, sur le script de hello :</span><span class="sxs-lookup"><span data-stu-id="05bc0-154">A few items toonote about hello script:</span></span>

* <span data-ttu-id="05bc0-155">toogrant hello identité accès toohello abonnement par défaut vous n’avez pas besoin tooprovide les paramètres de groupe de ressources ou d’ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="05bc0-155">toogrant hello identity access toohello default subscription, you do not need tooprovide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="05bc0-156">Spécifiez le paramètre de groupe de ressources hello uniquement lorsque vous souhaitez étendue de hello toolimit hello rôle affectation tooa du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="05bc0-156">Specify hello ResourceGroup parameter only when you want toolimit hello scope of hello role assignment tooa resource group.</span></span>
* <span data-ttu-id="05bc0-157">Dans cet exemple, vous ajoutez rôle de collaborateur hello service toohello principal.</span><span class="sxs-lookup"><span data-stu-id="05bc0-157">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="05bc0-158">Pour les autres rôles, voir [RBAC : rôles intégrés](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="05bc0-158">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="05bc0-159">script de Hello mise en veille tooallow de 15 secondes du temps pour hello de nouveau service principal toopropagate dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="05bc0-159">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="05bc0-160">Si votre script n’attend pas suffisamment longtemps, vous voyez une erreur indiquant : « PrincipalNotFound : Principal {id} n’existe pas dans le répertoire de hello. »</span><span class="sxs-lookup"><span data-stu-id="05bc0-160">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="05bc0-161">Si vous avez besoin d’abonnements de toomore toogrant hello service principal l’accès ou les groupes de ressources, exécutez hello `New-AzureRMRoleAssignment` applet de commande avec des portées différentes.</span><span class="sxs-lookup"><span data-stu-id="05bc0-161">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

<span data-ttu-id="05bc0-162">Si vous **n’ont pas Windows 10 ou Windows Server 2016 Technical Preview**, vous devez les hello toodownload [générateur du certificat auto-signé](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) à partir de Microsoft Script Center.</span><span class="sxs-lookup"><span data-stu-id="05bc0-162">If you **do not have Windows 10 or Windows Server 2016 Technical Preview**, you need toodownload hello [Self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from Microsoft Script Center.</span></span> <span data-ttu-id="05bc0-163">Extrayez son contenu et importer l’applet de commande hello que vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="05bc0-163">Extract its contents and import hello cmdlet you need.</span></span>

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
<span data-ttu-id="05bc0-164">Dans le script de hello, remplacer hello suivant certificat hello de toogenerate deux lignes.</span><span class="sxs-lookup"><span data-stu-id="05bc0-164">In hello script, substitute hello following two lines toogenerate hello certificate.</span></span>
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="05bc0-165">Fournir un certificat via un script PowerShell automatisé</span><span class="sxs-lookup"><span data-stu-id="05bc0-165">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="05bc0-166">Chaque fois que vous êtes connecté en tant que service principal, vous avez besoin d’id de client hello tooprovide du répertoire de hello pour votre application AD.</span><span class="sxs-lookup"><span data-stu-id="05bc0-166">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="05bc0-167">Un locataire est une instance d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="05bc0-167">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="05bc0-168">Si vous disposez d’un seul abonnement, vous pouvez utiliser :</span><span class="sxs-lookup"><span data-stu-id="05bc0-168">If you only have one subscription, you can use:</span></span>

```powershell
Param (
 
 [Parameter(Mandatory=$true)]
 [String] $CertSubject,
 
 [Parameter(Mandatory=$true)]
 [String] $ApplicationId,

 [Parameter(Mandatory=$true)]
 [String] $TenantId
 )

 $Thumbprint = (Get-ChildItem cert:\CurrentUser\My\ | Where-Object {$_.Subject -match $CertSubject }).Thumbprint
 Login-AzureRmAccount -ServicePrincipal -CertificateThumbprint $Thumbprint -ApplicationId $ApplicationId -TenantId $TenantId
```

<span data-ttu-id="05bc0-169">application Hello ID et l’ID de client n’étant pas sensibles, vous pouvez les incorporer directement dans votre script.</span><span class="sxs-lookup"><span data-stu-id="05bc0-169">hello application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="05bc0-170">Si vous avez besoin d’ID de client hello tooretrieve, utilisez :</span><span class="sxs-lookup"><span data-stu-id="05bc0-170">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="05bc0-171">Si vous avez besoin d’ID de l’application hello tooretrieve, utilisez :</span><span class="sxs-lookup"><span data-stu-id="05bc0-171">If you need tooretrieve hello application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a><span data-ttu-id="05bc0-172">Créer un principal du service avec un certificat à partir de l’autorité de certification</span><span class="sxs-lookup"><span data-stu-id="05bc0-172">Create service principal with certificate from Certificate Authority</span></span>
<span data-ttu-id="05bc0-173">toouse un certificat émis par un principal de service Autorité de certification toocreate, hello utilisez script suivant :</span><span class="sxs-lookup"><span data-stu-id="05bc0-173">toouse a certificate issued from a Certificate Authority toocreate service principal, use hello following script:</span></span>

```powershell
Param (
 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName,

 [Parameter(Mandatory=$true)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $CertPath,

 [Parameter(Mandatory=$true)]
 [String] $CertPlainPassword
 )

 Login-AzureRmAccount
 Import-Module AzureRM.Resources
 Set-AzureRmContext -SubscriptionId $SubscriptionId

 $KeyId = (New-Guid).Guid
 $CertPassword = ConvertTo-SecureString $CertPlainPassword -AsPlainText -Force

 $PFXCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($CertPath, $CertPassword)
 $KeyValue = [System.Convert]::ToBase64String($PFXCert.GetRawCertData())

 $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
 $KeyCredential.StartDate = $PFXCert.NotBefore
 $KeyCredential.EndDate= $PFXCert.NotAfter
 $KeyCredential.KeyId = $KeyId
 $KeyCredential.CertValue = $KeyValue

 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -KeyCredentials $keyCredential
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
 
 $NewRole
```

<span data-ttu-id="05bc0-174">Quelques éléments toonote, sur le script de hello :</span><span class="sxs-lookup"><span data-stu-id="05bc0-174">A few items toonote about hello script:</span></span>

* <span data-ttu-id="05bc0-175">L’accès est étendue toohello abonnement.</span><span class="sxs-lookup"><span data-stu-id="05bc0-175">Access is scoped toohello subscription.</span></span>
* <span data-ttu-id="05bc0-176">Dans cet exemple, vous ajoutez rôle de collaborateur hello service toohello principal.</span><span class="sxs-lookup"><span data-stu-id="05bc0-176">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="05bc0-177">Pour les autres rôles, voir [RBAC : rôles intégrés](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="05bc0-177">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="05bc0-178">script de Hello mise en veille tooallow de 15 secondes du temps pour hello de nouveau service principal toopropagate dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="05bc0-178">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="05bc0-179">Si votre script n’attend pas suffisamment longtemps, vous voyez une erreur indiquant : « PrincipalNotFound : Principal {id} n’existe pas dans le répertoire de hello. »</span><span class="sxs-lookup"><span data-stu-id="05bc0-179">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="05bc0-180">Si vous avez besoin d’abonnements de toomore toogrant hello service principal l’accès ou les groupes de ressources, exécutez hello `New-AzureRMRoleAssignment` applet de commande avec des portées différentes.</span><span class="sxs-lookup"><span data-stu-id="05bc0-180">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="05bc0-181">Fournir un certificat via un script PowerShell automatisé</span><span class="sxs-lookup"><span data-stu-id="05bc0-181">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="05bc0-182">Chaque fois que vous êtes connecté en tant que service principal, vous avez besoin d’id de client hello tooprovide du répertoire de hello pour votre application AD.</span><span class="sxs-lookup"><span data-stu-id="05bc0-182">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="05bc0-183">Un locataire est une instance d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="05bc0-183">A tenant is an instance of Azure Active Directory.</span></span>

```powershell
Param (
 
 [Parameter(Mandatory=$true)]
 [String] $CertPath,

 [Parameter(Mandatory=$true)]
 [String] $CertPlainPassword,
 
 [Parameter(Mandatory=$true)]
 [String] $ApplicationId,

 [Parameter(Mandatory=$true)]
 [String] $TenantId
 )

 $CertPassword = ConvertTo-SecureString $CertPlainPassword -AsPlainText -Force
 $PFXCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($CertPath, $CertPassword)
 $Thumbprint = $PFXCert.Thumbprint

 Login-AzureRmAccount -ServicePrincipal -CertificateThumbprint $Thumbprint -ApplicationId $ApplicationId -TenantId $TenantId
```

<span data-ttu-id="05bc0-184">application Hello ID et l’ID de client n’étant pas sensibles, vous pouvez les incorporer directement dans votre script.</span><span class="sxs-lookup"><span data-stu-id="05bc0-184">hello application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="05bc0-185">Si vous avez besoin d’ID de client hello tooretrieve, utilisez :</span><span class="sxs-lookup"><span data-stu-id="05bc0-185">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="05bc0-186">Si vous avez besoin d’ID de l’application hello tooretrieve, utilisez :</span><span class="sxs-lookup"><span data-stu-id="05bc0-186">If you need tooretrieve hello application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a><span data-ttu-id="05bc0-187">Modifier les informations d’identification</span><span class="sxs-lookup"><span data-stu-id="05bc0-187">Change credentials</span></span>

<span data-ttu-id="05bc0-188">informations d’identification de hello toochange pour une application AD, soit en raison d’une compromission de la sécurité ou une date d’expiration des informations d’identification, utilisent hello [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) et [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) applets de commande.</span><span class="sxs-lookup"><span data-stu-id="05bc0-188">toochange hello credentials for an AD app, either because of a security compromise or a credential expiration, use hello [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) and [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlets.</span></span>

<span data-ttu-id="05bc0-189">tooremove toutes les informations d’identification de hello pour une application, utilisez :</span><span class="sxs-lookup"><span data-stu-id="05bc0-189">tooremove all hello credentials for an application, use:</span></span>

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

<span data-ttu-id="05bc0-190">tooadd un mot de passe, utilisez :</span><span class="sxs-lookup"><span data-stu-id="05bc0-190">tooadd a password, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

<span data-ttu-id="05bc0-191">tooadd une valeur de certificat, créez un certificat auto-signé, comme indiqué dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="05bc0-191">tooadd a certificate value, create a self-signed certificate as shown in this topic.</span></span> <span data-ttu-id="05bc0-192">Ensuite, utilisez :</span><span class="sxs-lookup"><span data-stu-id="05bc0-192">Then, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-toosimplify-log-in"></a><span data-ttu-id="05bc0-193">Enregistrer les accès toosimplify jeton connectez-vous</span><span class="sxs-lookup"><span data-stu-id="05bc0-193">Save access token toosimplify log in</span></span>
<span data-ttu-id="05bc0-194">tooavoid fournissant hello service principal informations d’identification chaque fois qu’il doit toolog dans, vous pouvez enregistrer le jeton d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="05bc0-194">tooavoid providing hello service principal credentials every time it needs toolog in, you can save hello access token.</span></span>

<span data-ttu-id="05bc0-195">toouse hello jeton d’accès actuel dans une session ultérieure, enregistrez le profil de hello.</span><span class="sxs-lookup"><span data-stu-id="05bc0-195">toouse hello current access token in a later session, save hello profile.</span></span>
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
<span data-ttu-id="05bc0-196">Ouvrir le profil de hello et examiner son contenu.</span><span class="sxs-lookup"><span data-stu-id="05bc0-196">Open hello profile and examine its contents.</span></span> <span data-ttu-id="05bc0-197">Notez qu’il contient un jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="05bc0-197">Notice that it contains an access token.</span></span> <span data-ttu-id="05bc0-198">Au lieu de manuellement une nouvelle connexion, il suffit de recharger profil de hello.</span><span class="sxs-lookup"><span data-stu-id="05bc0-198">Instead of manually logging in again, simply load hello profile.</span></span>
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> <span data-ttu-id="05bc0-199">jeton d’accès Hello expire, donc à l’aide d’un profil enregistré fonctionne uniquement pour tant que hello du jeton est valide.</span><span class="sxs-lookup"><span data-stu-id="05bc0-199">hello access token expires, so using a saved profile only works for as long as hello token is valid.</span></span>
>  

<span data-ttu-id="05bc0-200">Ou bien, vous pouvez appeler des opérations REST à partir de toolog PowerShell dans.</span><span class="sxs-lookup"><span data-stu-id="05bc0-200">Alternatively, you can invoke REST operations from PowerShell toolog in.</span></span> <span data-ttu-id="05bc0-201">À partir de la réponse d’authentification hello, vous pouvez récupérer le jeton d’accès hello pour une utilisation avec d’autres opérations.</span><span class="sxs-lookup"><span data-stu-id="05bc0-201">From hello authentication response, you can retrieve hello access token for use with other operations.</span></span> <span data-ttu-id="05bc0-202">Pour obtenir un exemple de la récupération du jeton d’accès hello en appelant les opérations REST, consultez [générer un jeton d’accès](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="05bc0-202">For an example of retrieving hello access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="debug"></a><span data-ttu-id="05bc0-203">Déboguer</span><span class="sxs-lookup"><span data-stu-id="05bc0-203">Debug</span></span>

<span data-ttu-id="05bc0-204">Vous pouvez rencontrer les erreurs suivantes lors de la création d’un principal de service de hello :</span><span class="sxs-lookup"><span data-stu-id="05bc0-204">You may encounter hello following errors when creating a service principal:</span></span>

* <span data-ttu-id="05bc0-205">**« Authentication_Unauthorized »** ou **« aucun abonnement ne trouvé dans le contexte de hello. »**</span><span class="sxs-lookup"><span data-stu-id="05bc0-205">**"Authentication_Unauthorized"** or **"No subscription found in hello context."**</span></span> <span data-ttu-id="05bc0-206">-Vous recevez cette erreur lorsque votre compte ne dispose pas de hello [autorisations requises](#required-permissions) sur hello Azure Active Directory tooregister une application.</span><span class="sxs-lookup"><span data-stu-id="05bc0-206">- You see this error when your account does not have hello [required permissions](#required-permissions) on hello Azure Active Directory tooregister an app.</span></span> <span data-ttu-id="05bc0-207">En règle générale, vous obtenez cette erreur lorsque seuls des utilisateurs administrateurs dans votre annuaire Azure Active Directory peuvent inscrire des applications et que votre compte n’est pas un compte d’administrateur. Demandez à votre tooeither administrateur affecter le rôle administrateur tooan ou tooenable utilisateurs tooregister applications.</span><span class="sxs-lookup"><span data-stu-id="05bc0-207">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin. Ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

* <span data-ttu-id="05bc0-208">Votre compte **« n’a pas action de tooperform d’autorisation 'Microsoft.Authorization/roleAssignments/write' sur l’étendue '/ subscriptions / {guid}'. »**  -Vous recevez cette erreur lorsque votre compte n’a pas suffisamment autorisations tooassign une identité tooan du rôle.</span><span class="sxs-lookup"><span data-stu-id="05bc0-208">Your account **"does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions tooassign a role tooan identity.</span></span> <span data-ttu-id="05bc0-209">Demandez à votre tooadd d’administrateur abonnement rôle administrateur de l’accès tooUser.</span><span class="sxs-lookup"><span data-stu-id="05bc0-209">Ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="05bc0-210">Exemples d'applications</span><span class="sxs-lookup"><span data-stu-id="05bc0-210">Sample applications</span></span>
<span data-ttu-id="05bc0-211">Pour plus d’informations sur la connexion en tant qu’application hello via différentes plateformes, consultez :</span><span class="sxs-lookup"><span data-stu-id="05bc0-211">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="05bc0-212">.NET</span><span class="sxs-lookup"><span data-stu-id="05bc0-212">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="05bc0-213">Java</span><span class="sxs-lookup"><span data-stu-id="05bc0-213">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="05bc0-214">Node.JS</span><span class="sxs-lookup"><span data-stu-id="05bc0-214">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="05bc0-215">Python</span><span class="sxs-lookup"><span data-stu-id="05bc0-215">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="05bc0-216">Ruby</span><span class="sxs-lookup"><span data-stu-id="05bc0-216">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="05bc0-217">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="05bc0-217">Next steps</span></span>
* <span data-ttu-id="05bc0-218">Pour obtenir des instructions détaillées sur l’intégration d’une application dans Azure pour la gestion des ressources, consultez [tooauthorization du guide du développeur avec hello API Azure Resource Manager](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="05bc0-218">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="05bc0-219">Pour obtenir une explication plus détaillée des applications et des principaux du service, consultez la rubrique [Objets principal du service et application](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="05bc0-219">For a more detailed explanation of applications and service principals, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span> 
* <span data-ttu-id="05bc0-220">Pour plus d’informations sur l’authentification Azure Active Directory, consultez la rubrique [Scénarios d’authentification pour Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="05bc0-220">For more information about Azure Active Directory authentication, see [Authentication Scenarios for Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span></span>
* <span data-ttu-id="05bc0-221">Pour obtenir la liste des actions disponibles qui peuvent être accordées ou refusées toousers, consultez [opérations du fournisseur de ressources Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="05bc0-221">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>

