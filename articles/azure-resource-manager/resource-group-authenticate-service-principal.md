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
# <a name="use-azure-powershell-toocreate-a-service-principal-tooaccess-resources"></a>Utiliser Azure PowerShell toocreate une ressources tooaccess principal du service

Lorsque vous avez une application ou un script nécessitant des ressources de tooaccess, vous pouvez configurer une identité pour l’application hello et authentifier l’application hello avec ses propres informations d’identification. Cette identité est connue en tant que principal de service. Cette approche vous permet d’effectuer les opérations suivantes :

* Affecter des autorisations identité d’application toohello différents de vos propres autorisations. En règle générale, ces autorisations sont limitée tooexactly quelle application hello doit toodo.
* Utilisez un certificat pour l’authentification lors de l’exécution d’un script sans assistance.

Cette rubrique vous montre comment toouse [Azure PowerShell](/powershell/azure/overview) tooset installé tout ce dont vous avez besoin pour une toorun application sous ses propres informations d’identification et l’identité.

## <a name="required-permissions"></a>Autorisations requises
toocomplete cette rubrique, vous devez disposer des autorisations suffisantes dans Azure Active Directory et votre abonnement Azure. Plus précisément, vous devez être en mesure de toocreate une application Bonjour Azure Active Directory et affecter des rôle tooa principal du service hello. 

Hello toocheck de façon plus simple si votre compte dispose des autorisations adéquates est via le portail de hello. Consultez [Vérifier l’autorisation requise](resource-group-create-service-principal-portal.md#required-permissions).

Maintenant, section tooa pour l’authentification avec :

* [mot de passe](#create-service-principal-with-password)
* [certificat auto-signé](#create-service-principal-with-self-signed-certificate)
* [certificat délivré par une autorité de certification](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a>Commandes PowerShell

tooset d’un service principal, utilisez :

| Commande | Description |
| ------- | ----------- | 
| [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | Crée un principal de service Azure Active Directory |
| [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment) | Assigne hello spécifiées RBAC rôle toohello spécifié principal, au hello étendue. |


## <a name="create-service-principal-with-password"></a>Créer un principal du service avec un mot de passe

toocreate un principal de service avec le rôle de collaborateur hello pour votre abonnement, utilisez : 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

exemple de Hello mise en veille tooallow de 20 secondes du temps pour hello de nouveau service principal toopropagate dans Azure Active Directory. Si votre script n’attend pas suffisamment longtemps, vous voyez une erreur indiquant : « PrincipalNotFound : Principal {id} n’existe pas dans le répertoire de hello. »

Hello script suivant vous permet de toospecify une portée différente d’abonnement par défaut de hello et nouvelles tentatives hello attribution de rôle si une erreur se produit :

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

Quelques éléments toonote, sur le script de hello :

* toogrant hello identité accès toohello abonnement par défaut vous n’avez pas besoin tooprovide les paramètres de groupe de ressources ou d’ID d’abonnement.
* Spécifiez le paramètre de groupe de ressources hello uniquement lorsque vous souhaitez étendue de hello toolimit hello rôle affectation tooa du groupe de ressources.
*  Dans cet exemple, vous ajoutez rôle de collaborateur hello service toohello principal. Pour les autres rôles, voir [RBAC : rôles intégrés](../active-directory/role-based-access-built-in-roles.md).
* script de Hello mise en veille tooallow de 15 secondes du temps pour hello de nouveau service principal toopropagate dans Azure Active Directory. Si votre script n’attend pas suffisamment longtemps, vous voyez une erreur indiquant : « PrincipalNotFound : Principal {id} n’existe pas dans le répertoire de hello. »
* Si vous avez besoin d’abonnements de toomore toogrant hello service principal l’accès ou les groupes de ressources, exécutez hello `New-AzureRMRoleAssignment` applet de commande avec des portées différentes.


### <a name="provide-credentials-through-powershell"></a>Fournir des informations d’identification via PowerShell
Maintenant, vous devez toolog dans en tant qu’opérations de tooperform application hello. Pour nom d’utilisateur hello, utilisez hello `ApplicationId` que vous avez créé pour l’application hello. Mot de passe hello, utilisez hello une que vous avez spécifié lors de la création du compte de hello. 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

ID de client Hello n’est pas sensible, vous pouvez l’incorporer directement dans votre script. Si vous avez besoin d’ID de client hello tooretrieve, utilisez :

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a>Créer un principal du service avec un certificat auto-signé

toocreate un principal de service avec un certificat auto-signé et le rôle de collaborateur hello pour votre abonnement, utilisez : 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

exemple de Hello mise en veille tooallow de 20 secondes du temps pour hello de nouveau service principal toopropagate dans Azure Active Directory. Si votre script n’attend pas suffisamment longtemps, vous voyez une erreur indiquant : « PrincipalNotFound : Principal {id} n’existe pas dans le répertoire de hello. »

Hello script suivant vous permet de toospecify une portée différente d’abonnement par défaut de hello et nouvelles tentatives hello attribution de rôle si une erreur se produit. Vous devez disposer d’Azure PowerShell 2.0 sur Windows 10 ou Windows Server 2016.

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

Quelques éléments toonote, sur le script de hello :

* toogrant hello identité accès toohello abonnement par défaut vous n’avez pas besoin tooprovide les paramètres de groupe de ressources ou d’ID d’abonnement.
* Spécifiez le paramètre de groupe de ressources hello uniquement lorsque vous souhaitez étendue de hello toolimit hello rôle affectation tooa du groupe de ressources.
* Dans cet exemple, vous ajoutez rôle de collaborateur hello service toohello principal. Pour les autres rôles, voir [RBAC : rôles intégrés](../active-directory/role-based-access-built-in-roles.md).
* script de Hello mise en veille tooallow de 15 secondes du temps pour hello de nouveau service principal toopropagate dans Azure Active Directory. Si votre script n’attend pas suffisamment longtemps, vous voyez une erreur indiquant : « PrincipalNotFound : Principal {id} n’existe pas dans le répertoire de hello. »
* Si vous avez besoin d’abonnements de toomore toogrant hello service principal l’accès ou les groupes de ressources, exécutez hello `New-AzureRMRoleAssignment` applet de commande avec des portées différentes.

Si vous **n’ont pas Windows 10 ou Windows Server 2016 Technical Preview**, vous devez les hello toodownload [générateur du certificat auto-signé](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) à partir de Microsoft Script Center. Extrayez son contenu et importer l’applet de commande hello que vous avez besoin.

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
Dans le script de hello, remplacer hello suivant certificat hello de toogenerate deux lignes.
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a>Fournir un certificat via un script PowerShell automatisé
Chaque fois que vous êtes connecté en tant que service principal, vous avez besoin d’id de client hello tooprovide du répertoire de hello pour votre application AD. Un locataire est une instance d’Azure Active Directory. Si vous disposez d’un seul abonnement, vous pouvez utiliser :

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

application Hello ID et l’ID de client n’étant pas sensibles, vous pouvez les incorporer directement dans votre script. Si vous avez besoin d’ID de client hello tooretrieve, utilisez :

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

Si vous avez besoin d’ID de l’application hello tooretrieve, utilisez :

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a>Créer un principal du service avec un certificat à partir de l’autorité de certification
toouse un certificat émis par un principal de service Autorité de certification toocreate, hello utilisez script suivant :

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

Quelques éléments toonote, sur le script de hello :

* L’accès est étendue toohello abonnement.
* Dans cet exemple, vous ajoutez rôle de collaborateur hello service toohello principal. Pour les autres rôles, voir [RBAC : rôles intégrés](../active-directory/role-based-access-built-in-roles.md).
* script de Hello mise en veille tooallow de 15 secondes du temps pour hello de nouveau service principal toopropagate dans Azure Active Directory. Si votre script n’attend pas suffisamment longtemps, vous voyez une erreur indiquant : « PrincipalNotFound : Principal {id} n’existe pas dans le répertoire de hello. »
* Si vous avez besoin d’abonnements de toomore toogrant hello service principal l’accès ou les groupes de ressources, exécutez hello `New-AzureRMRoleAssignment` applet de commande avec des portées différentes.

### <a name="provide-certificate-through-automated-powershell-script"></a>Fournir un certificat via un script PowerShell automatisé
Chaque fois que vous êtes connecté en tant que service principal, vous avez besoin d’id de client hello tooprovide du répertoire de hello pour votre application AD. Un locataire est une instance d’Azure Active Directory.

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

application Hello ID et l’ID de client n’étant pas sensibles, vous pouvez les incorporer directement dans votre script. Si vous avez besoin d’ID de client hello tooretrieve, utilisez :

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

Si vous avez besoin d’ID de l’application hello tooretrieve, utilisez :

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a>Modifier les informations d’identification

informations d’identification de hello toochange pour une application AD, soit en raison d’une compromission de la sécurité ou une date d’expiration des informations d’identification, utilisent hello [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) et [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) applets de commande.

tooremove toutes les informations d’identification de hello pour une application, utilisez :

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

tooadd un mot de passe, utilisez :

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

tooadd une valeur de certificat, créez un certificat auto-signé, comme indiqué dans cette rubrique. Ensuite, utilisez :

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-toosimplify-log-in"></a>Enregistrer les accès toosimplify jeton connectez-vous
tooavoid fournissant hello service principal informations d’identification chaque fois qu’il doit toolog dans, vous pouvez enregistrer le jeton d’accès hello.

toouse hello jeton d’accès actuel dans une session ultérieure, enregistrez le profil de hello.
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
Ouvrir le profil de hello et examiner son contenu. Notez qu’il contient un jeton d’accès. Au lieu de manuellement une nouvelle connexion, il suffit de recharger profil de hello.
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> jeton d’accès Hello expire, donc à l’aide d’un profil enregistré fonctionne uniquement pour tant que hello du jeton est valide.
>  

Ou bien, vous pouvez appeler des opérations REST à partir de toolog PowerShell dans. À partir de la réponse d’authentification hello, vous pouvez récupérer le jeton d’accès hello pour une utilisation avec d’autres opérations. Pour obtenir un exemple de la récupération du jeton d’accès hello en appelant les opérations REST, consultez [générer un jeton d’accès](resource-manager-rest-api.md#generating-an-access-token).

## <a name="debug"></a>Déboguer

Vous pouvez rencontrer les erreurs suivantes lors de la création d’un principal de service de hello :

* **« Authentication_Unauthorized »** ou **« aucun abonnement ne trouvé dans le contexte de hello. »** -Vous recevez cette erreur lorsque votre compte ne dispose pas de hello [autorisations requises](#required-permissions) sur hello Azure Active Directory tooregister une application. En règle générale, vous obtenez cette erreur lorsque seuls des utilisateurs administrateurs dans votre annuaire Azure Active Directory peuvent inscrire des applications et que votre compte n’est pas un compte d’administrateur. Demandez à votre tooeither administrateur affecter le rôle administrateur tooan ou tooenable utilisateurs tooregister applications.

* Votre compte **« n’a pas action de tooperform d’autorisation 'Microsoft.Authorization/roleAssignments/write' sur l’étendue '/ subscriptions / {guid}'. »**  -Vous recevez cette erreur lorsque votre compte n’a pas suffisamment autorisations tooassign une identité tooan du rôle. Demandez à votre tooadd d’administrateur abonnement rôle administrateur de l’accès tooUser.

## <a name="sample-applications"></a>Exemples d'applications
Pour plus d’informations sur la connexion en tant qu’application hello via différentes plateformes, consultez :

* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.JS](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a>Étapes suivantes
* Pour obtenir des instructions détaillées sur l’intégration d’une application dans Azure pour la gestion des ressources, consultez [tooauthorization du guide du développeur avec hello API Azure Resource Manager](resource-manager-api-authentication.md).
* Pour obtenir une explication plus détaillée des applications et des principaux du service, consultez la rubrique [Objets principal du service et application](../active-directory/active-directory-application-objects.md). 
* Pour plus d’informations sur l’authentification Azure Active Directory, consultez la rubrique [Scénarios d’authentification pour Azure AD](../active-directory/active-directory-authentication-scenarios.md).
* Pour obtenir la liste des actions disponibles qui peuvent être accordées ou refusées toousers, consultez [opérations du fournisseur de ressources Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).

