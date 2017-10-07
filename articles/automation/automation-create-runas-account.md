---
title: "aaaCreate Azure Automation exécuter en tant que comptes | Documents Microsoft"
description: "Cet article décrit comment tooupdate votre automatisation compte et créez des comptes d’identification avec PowerShell ou depuis le portail de hello."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: 94eb54fa0b518056a726d17146c63411e248273b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a>Mettre à jour l’authentification de votre compte Automation avec des comptes d’identification 
Vous pouvez mettre à jour de votre compte Automation existant à partir du portail de hello ou utilisation de PowerShell si :

* Vous créez un compte Automation mais refusez toocreate hello exécuter en tant que compte.
* Vous utilisez déjà une ressources de gestionnaire de ressources toomanage compte Automation et que vous souhaitez tooupdate hello tooinclude hello exécuter en tant que compte pour l’authentification de runbook.
* Vous utilisez déjà une Automation compte toomanage les ressources classiques et tooupdate il toouse hello classique compte d’identification au lieu de créer un compte et la migration de votre tooit runbooks et ressources.   
* Vous souhaitez que toocreate une identification et classique compte d’identification à l’aide d’un certificat émis par votre autorité de certification d’entreprise (CA).

## <a name="prerequisites"></a>Composants requis

* script de Hello peut être exécutée que sur Windows 10 et Windows Server 2016 avec des modules Azure Resource Manager 3.0.0 et versions ultérieures. Il n’est pas pris en charge dans les versions antérieures de Windows.
* Azure PowerShell 1.0 et versions ultérieures. Pour plus d’informations sur la mise en production hello PowerShell 1.0, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs).
* Un compte Automation, qui est référencé en tant que valeur hello pour hello *– AutomationAccountName* et *- ApplicationDisplayName* paramètres Bonjour suite du script PowerShell.

les valeurs tooget hello pour *SubscriptionID*, *ResourceGroup*, et *AutomationAccountName*, qui sont des paramètres requis pour le script de hello, procédez comme hello suivant :

1. Dans l’hello portail Azure, sélectionnez votre compte Automation sur hello **compte Automation** panneau, puis sélectionnez **tous les paramètres**.  
2. Sur hello **tous les paramètres** panneau, sous **les paramètres de compte**, sélectionnez **propriétés**. 
3. Notez les valeurs hello sur hello **propriétés** panneau.<br><br> ![Panneau de Hello Automation compte « Propriétés »](media/automation-create-runas-account/automation-account-properties.png)  

### <a name="required-permissions-tooupdate-your-automation-account"></a>Requis tooupdate d’autorisations de votre compte Automation
tooupdate un compte Automation, vous devez avoir hello suivant des privilèges spécifiques et des autorisations requises toocomplete de cette rubrique.   
 
* Votre compte d’utilisateur Active Directory doit être rôle tooa ajouté de toobe avec le rôle de collaborateur équivalent toohello autorisations pour les ressources Microsoft.Automation comme indiqué dans l’article [contrôle d’accès basé sur un rôle dans Azure Automation](automation-role-based-access-control.md#contributor-role-permissions).  
* Les utilisateurs non administrateurs dans votre locataire Azure AD peuvent [inscrire des applications AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) si les inscriptions d’application hello paramètre est défini trop**Oui**.  Si les inscriptions d’application hello paramètre est défini trop**non**, utilisateur hello effectuer cette action doit être un administrateur global dans Azure AD. 

Si vous n’êtes pas un membre d’instance d’Active Directory de l’abonnement hello avant que vous êtes ajouté toohello global administrateur ou le co-administrateur rôle d’abonnement de hello, vous êtes ajouté tooActive active en tant qu’invité. Dans ce cas, vous recevez un « vous n’avez pas toocreate autorisations... » avertissement sur hello **ajouter un compte Automation** panneau. Les utilisateurs qui ont été ajoutées toohello global administrateur ou le co-administrateur rôle tout d’abord peut être supprimé de l’instance d’Active Directory de l’abonnement hello et rajouté toomake les un utilisateur complète dans Active Directory. tooverify cette situation, hello **Azure Active Directory** volet Bonjour portail Azure, sélectionnez **utilisateurs et groupes**, sélectionnez **tous les utilisateurs** et, après avoir sélectionné hello utilisateur spécifique, sélectionnez **profil**. Hello valeur Hello **type utilisateur** attribut sous le profil de l’utilisateur hello doit être **invité**.

## <a name="create-run-as-account-from-hello-portal"></a>Créer un compte d’identification à partir du portail de hello
Dans cette section, effectuez hello suivant les étapes tooupdate votre compte Azure Automation hello portail Azure.  Vous créez des comptes d’identification et Classic exécuter en tant que hello individuellement, et si vous n’avez pas besoin des ressources de toomanage dans le portail Azure classic de hello, vous pouvez simplement créer un compte d’identification Azure hello.  

processus de Hello crée hello éléments ci-après dans votre compte Automation.

**Pour les comptes d’identification :**

* Crée une application Azure AD avec un certificat auto-signé, crée un compte de principal du service pour l’application hello dans Azure AD et attribue le rôle de collaborateur hello compte hello dans votre abonnement actuel. Vous pouvez modifier ce paramètre tooOwner ou tout autre rôle. Pour plus d’informations, voir [Contrôle d’accès en fonction du rôle dans Azure Automation](automation-role-based-access-control.md).
* Crée une ressource de certificat Automation nommée *AzureRunAsCertificate* Bonjour spécifié le compte Automation. ressource de certificat Hello conserve la clé privée hello certificat utilisé par l’application hello Azure AD.
* Crée une ressource de connexion d’Automation nommée *AzureRunAsConnection* Bonjour spécifié le compte Automation. ressource de connexion Hello conserve hello applicationId, tenantId, ID d’abonnement et l’empreinte numérique du certificat.

**Pour les comptes d’identification Classic :**

* Crée une ressource de certificat Automation nommée *AzureClassicRunAsCertificate* Bonjour spécifié le compte Automation. ressource de certificat Hello conserve la clé privée du certificat hello utilisé par le certificat de gestion hello.
* Crée une ressource de connexion d’Automation nommée *AzureClassicRunAsConnection* Bonjour spécifié le compte Automation. ressource de connexion Hello conserve hello abonnement nom, ID d’abonnement et nom de ressource de certificat.

1. Se connecter toohello portail Azure avec un compte qui est membre du rôle des administrateurs d’abonnements hello et coadministrateur de l’abonnement de hello.
2. Dans le panneau de compte Automation hello, sélectionnez **comptes d’identification** section hello **les paramètres de compte**.  
3. Selon le compte dont vous avez besoin, sélectionnez **Compte d’identification Azure** ou **Compte d’identification Azure Classic**.  Après avoir sélectionné soit hello **ajouter Azure exécuter en tant que** ou **ajouter Azure Classic compte d’identification** panneau s’affiche et après avoir examiné les informations de vue d’ensemble de hello, cliquez sur **créer** tooproceed avec exécuter en tant que la création du compte.  
4. Alors que Azure crée le compte d’identification hello, vous pouvez suivre la progression de hello sous **Notifications** de hello menu et une bannière s’affiche indiquant hello compte doit être créé.  Ce processus peut prendre quelques minutes toocomplete.  

## <a name="create-run-as-account-using-powershell-script"></a>Créer un compte d’identification à l’aide d’un script PowerShell
Ce script PowerShell prend en charge hello suivant configurations :

* Créez un compte d’identification à l’aide d’un certificat auto-signé.
* Créez un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat auto-signé.
* Créez un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat d’entreprise.
* Créer un compte d’identification et classique compte d’identification à l’aide d’un certificat auto-signé Bonjour cloud d’Azure Government.

En fonction de l’option de configuration hello sélectionnée, le script de hello crée hello éléments suivants.

**Pour les comptes d’identification :**

* Crée un Azure AD application toobe exporté avec soit hello auto-signé ou clé publique du certificat enterprise, crée un compte de principal du service pour l’application hello dans Azure AD, et assigne hello compte hello dans votre rôle de collaborateur abonnement. Vous pouvez modifier ce paramètre tooOwner ou tout autre rôle. Pour plus d’informations, voir [Contrôle d’accès en fonction du rôle dans Azure Automation](automation-role-based-access-control.md).
* Crée une ressource de certificat Automation nommée *AzureRunAsCertificate* Bonjour spécifié le compte Automation. ressource de certificat Hello conserve la clé privée hello certificat utilisé par l’application hello Azure AD.
* Crée une ressource de connexion d’Automation nommée *AzureRunAsConnection* Bonjour spécifié le compte Automation. ressource de connexion Hello conserve hello applicationId, tenantId, ID d’abonnement et l’empreinte numérique du certificat.

**Pour les comptes d’identification Classic :**

* Crée une ressource de certificat Automation nommée *AzureClassicRunAsCertificate* Bonjour spécifié le compte Automation. ressource de certificat Hello conserve la clé privée du certificat hello utilisé par le certificat de gestion hello.
* Crée une ressource de connexion d’Automation nommée *AzureClassicRunAsConnection* Bonjour spécifié le compte Automation. ressource de connexion Hello conserve hello abonnement nom, ID d’abonnement et nom de ressource de certificat.

>[!NOTE]
> Si vous sélectionnez l’option de création d’un compte classique exécuter en tant qu’après l’exécution de script de hello, téléchargement hello publique magasin de certificats de gestion de toohello (extension de nom de fichier .cer) pour l’abonnement de hello que hello compte Automation a été créé dans.
> 

1. Enregistrez hello script suivant sur votre ordinateur. Dans cet exemple, enregistrez-le sous le nom de fichier hello *New-RunAsAccount.ps1*.

        #Requires -RunAsAdministrator
        Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                       [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
            -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
            -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate = Get-Date $PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
            Sleep -s 10
            New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
            $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
            $Retries++;
        }
            return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 3 -and $AzureRMProfileVersion.Minor -ge 0) -or ($AzureRMProfileVersion.Major -gt 3)))
        {
            Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
            return
        }

        Login-AzureRmAccount -Environment $EnvironmentName 
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
           $CertificateName = $AutomationAccountName+$CertifcateAssetName
           $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
           $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
           $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
           CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
             # Create a Run As account by using a service principal
             $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
             $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
             $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
             $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                     "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                     "Then click Upload and upload hello .cer format of #CERT#"

              if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
              $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
              $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
              $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
              $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
              $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
              $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
              $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
              $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
              CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.Name
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. Sur votre ordinateur, démarrez **Windows PowerShell** de hello **Démarrer** écran avec des droits utilisateur élevés.
3. À partir de hello élevé interpréteur de commandes, accédez toohello dossier qui contient le script hello créé à l’étape 1.  
4. Exécuter le script de hello à l’aide des valeurs de paramètre hello pour configuration hello que vous avez besoin.

    **Créer un compte d’identification à l’aide d’un certificat auto-signé**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    **Créer un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat auto-signé**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    **Créer un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat d’entreprise**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    **Créer un compte d’identification et classique compte d’identification à l’aide d’un certificat auto-signé Bonjour cloud d’Azure Government**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > Après l’exécution de script de hello, vous serez invité à tooauthenticate avec Azure. Connectez-vous avec un compte qui est membre du rôle Administrateurs d’abonnement hello et coadministrateur de l’abonnement de hello.
    >
    >

Une fois le script de hello a été exécutée correctement, notez hello qui suit :
* Si vous avez créé un classique compte d’identification avec un certificat auto-signé de public (fichier .cer), le script de hello crée et enregistre toohello dossier des fichiers temporaires sur votre ordinateur sous le profil utilisateur hello *%USERPROFILE%\AppData\Local\Temp*, que vous avez utilisé la session de PowerShell tooexecute hello.
* Si vous avez créé un compte d’identification Classic avec un certificat public d’entreprise (fichier .cer), utilisez ce certificat. Suivez les instructions de hello pour [téléchargement un toohello de certificat d’API de gestion portail Azure classic](../azure-api-management-certs.md), puis validez de configuration des informations d’identification hello avec des ressources de déploiement classique à l’aide de hello [exemple de code tooauthenticate avec des ressources de déploiement classique Azure](automation-verify-runas-authentication.md#classic-run-as-authentication). 
* Si vous l’avez fait *pas* créer classique compte d’identification, de s’authentifier auprès des ressources du Gestionnaire de ressources et de valider la configuration des informations d’identification hello à l’aide de hello [exemple de code pour s’authentifier auprès de gestion des services ressources](automation-verify-runas-authentication.md#automation-run-as-authentication).

## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur les principaux de Service, voir la rubrique trop[les objets de Principal du Service et Application](../active-directory/active-directory-application-objects.md).
* Pour plus d’informations sur les certificats et les services Azure, consultez trop[vue d’ensemble des certificats pour les Services de Cloud Azure](../cloud-services/cloud-services-certs-create.md).
