---
title: "aaaCreate Azure Automation comme compte d’identification avec PowerShell | Documents Microsoft"
description: "Cet article décrit comment tooupgrade votre compte Automation avec hello de toocreate PowerShell exécuter en tant que comptes si vous n’avez pas effectué cette étape lors de la création initiale du portail de hello."
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
ms.date: 04/14/2017
ms.author: magoedte
ms.openlocfilehash: 1049601321d2bc1e5f9d982f622788f8e4e4d797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="update-automation-run-as-account-using-powershell"></a><span data-ttu-id="df956-103">Mise à jour d’un compte d’identification Automation à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="df956-103">Update Automation Run As account using PowerShell</span></span>
<span data-ttu-id="df956-104">Vous pouvez utiliser PowerShell tooupdate votre compte Automation existant si :</span><span class="sxs-lookup"><span data-stu-id="df956-104">You can use PowerShell tooupdate your existing Automation account if:</span></span>

* <span data-ttu-id="df956-105">Vous créez un compte Automation mais refusez toocreate hello exécuter en tant que compte.</span><span class="sxs-lookup"><span data-stu-id="df956-105">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="df956-106">Vous utilisez déjà une ressources de gestionnaire de ressources toomanage compte Automation et que vous souhaitez tooupdate hello tooinclude hello exécuter en tant que compte pour l’authentification de runbook.</span><span class="sxs-lookup"><span data-stu-id="df956-106">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="df956-107">Vous utilisez déjà une Automation compte toomanage les ressources classiques et tooupdate il toouse hello classique compte d’identification au lieu de créer un compte et la migration de votre tooit runbooks et ressources.</span><span class="sxs-lookup"><span data-stu-id="df956-107">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="df956-108">Vous souhaitez que toocreate une identification et classique compte d’identification à l’aide d’un certificat émis par votre autorité de certification d’entreprise (CA).</span><span class="sxs-lookup"><span data-stu-id="df956-108">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df956-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="df956-109">Prerequisites</span></span>

* <span data-ttu-id="df956-110">script de Hello peut exécuter uniquement sur Windows 10 et Windows Server 2016 avec des modules Azure Resource Manager 2.01 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="df956-110">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="df956-111">Il n’est pas pris en charge dans les versions antérieures de Windows.</span><span class="sxs-lookup"><span data-stu-id="df956-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="df956-112">Azure PowerShell 1.0 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="df956-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="df956-113">Pour plus d’informations sur la mise en production hello PowerShell 1.0, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="df956-113">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="df956-114">Un compte Automation, qui est référencé en tant que valeur hello pour hello *– AutomationAccountName* et *- ApplicationDisplayName* paramètres Bonjour suite du script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="df956-114">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="df956-115">les valeurs tooget hello pour *SubscriptionID*, *ResourceGroup*, et *AutomationAccountName*, qui sont des paramètres requis pour les scripts de hello, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="df956-115">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello scripts, do hello following:</span></span>
1. <span data-ttu-id="df956-116">Dans l’hello portail Azure, sélectionnez votre compte Automation sur hello **compte Automation** panneau, puis sélectionnez **tous les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="df956-116">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="df956-117">Sur hello **tous les paramètres** panneau, sous **les paramètres de compte**, sélectionnez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="df956-117">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="df956-118">Notez les valeurs hello sur hello **propriétés** panneau.</span><span class="sxs-lookup"><span data-stu-id="df956-118">Note hello values on hello **Properties** blade.</span></span>

![Panneau de Hello Automation compte « Propriétés »](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

## <a name="create-run-as-account-powershell-script"></a><span data-ttu-id="df956-120">Créer le script PowerShell d’un compte d’identification</span><span class="sxs-lookup"><span data-stu-id="df956-120">Create Run As Account PowerShell script</span></span>
<span data-ttu-id="df956-121">Ce script PowerShell prend en charge hello suivant configurations :</span><span class="sxs-lookup"><span data-stu-id="df956-121">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="df956-122">Créez un compte d’identification à l’aide d’un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="df956-122">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="df956-123">Créez un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="df956-123">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="df956-124">Créez un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="df956-124">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="df956-125">Créer un compte d’identification et classique compte d’identification à l’aide d’un certificat auto-signé Bonjour cloud d’Azure Government.</span><span class="sxs-lookup"><span data-stu-id="df956-125">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="df956-126">En fonction de l’option de configuration hello sélectionnée, le script de hello crée hello éléments suivants.</span><span class="sxs-lookup"><span data-stu-id="df956-126">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="df956-127">**Pour les comptes d’identification :**</span><span class="sxs-lookup"><span data-stu-id="df956-127">**For Run As accounts:**</span></span>

* <span data-ttu-id="df956-128">Crée un Azure AD application toobe exporté avec soit hello auto-signé ou clé publique du certificat enterprise, crée un compte de principal du service pour l’application hello dans Azure AD, et assigne hello compte hello dans votre rôle de collaborateur abonnement.</span><span class="sxs-lookup"><span data-stu-id="df956-128">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="df956-129">Vous pouvez modifier ce paramètre tooOwner ou tout autre rôle.</span><span class="sxs-lookup"><span data-stu-id="df956-129">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="df956-130">Pour plus d’informations, voir [Contrôle d’accès en fonction du rôle dans Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="df956-130">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="df956-131">Crée une ressource de certificat Automation nommée *AzureRunAsCertificate* Bonjour spécifié le compte Automation.</span><span class="sxs-lookup"><span data-stu-id="df956-131">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="df956-132">ressource de certificat Hello conserve la clé privée hello certificat utilisé par l’application hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df956-132">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="df956-133">Crée une ressource de connexion d’Automation nommée *AzureRunAsConnection* Bonjour spécifié le compte Automation.</span><span class="sxs-lookup"><span data-stu-id="df956-133">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="df956-134">ressource de connexion Hello conserve hello applicationId, tenantId, ID d’abonnement et l’empreinte numérique du certificat.</span><span class="sxs-lookup"><span data-stu-id="df956-134">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="df956-135">**Pour les comptes d’identification Classic :**</span><span class="sxs-lookup"><span data-stu-id="df956-135">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="df956-136">Crée une ressource de certificat Automation nommée *AzureClassicRunAsCertificate* Bonjour spécifié le compte Automation.</span><span class="sxs-lookup"><span data-stu-id="df956-136">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="df956-137">ressource de certificat Hello conserve la clé privée du certificat hello utilisé par le certificat de gestion hello.</span><span class="sxs-lookup"><span data-stu-id="df956-137">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="df956-138">Crée une ressource de connexion d’Automation nommée *AzureClassicRunAsConnection* Bonjour spécifié le compte Automation.</span><span class="sxs-lookup"><span data-stu-id="df956-138">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="df956-139">ressource de connexion Hello conserve hello abonnement nom, ID d’abonnement et nom de ressource de certificat.</span><span class="sxs-lookup"><span data-stu-id="df956-139">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="df956-140">Si vous sélectionnez l’option de création d’un compte classique exécuter en tant qu’après l’exécution de script de hello, téléchargement hello publique magasin de certificats de gestion de toohello (extension de nom de fichier .cer) pour l’abonnement de hello que hello compte Automation a été créé dans.</span><span class="sxs-lookup"><span data-stu-id="df956-140">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

1. <span data-ttu-id="df956-141">Enregistrez hello script suivant sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="df956-141">Save hello following script on your computer.</span></span> <span data-ttu-id="df956-142">Dans cet exemple, enregistrez-le sous le nom de fichier hello *New-RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="df956-142">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

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
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
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
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
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
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="df956-143">Sur votre ordinateur, démarrez **Windows PowerShell** de hello **Démarrer** écran avec des droits utilisateur élevés.</span><span class="sxs-lookup"><span data-stu-id="df956-143">On your computer, start **Windows PowerShell** from hello **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="df956-144">À partir de hello élevé interpréteur de commandes, accédez toohello dossier qui contient le script hello créé à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="df956-144">From hello elevated command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>  
4. <span data-ttu-id="df956-145">Exécuter le script de hello à l’aide des valeurs de paramètre hello pour configuration hello que vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="df956-145">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="df956-146">**Créer un compte d’identification à l’aide d’un certificat auto-signé**</span><span class="sxs-lookup"><span data-stu-id="df956-146">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="df956-147">**Créer un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat auto-signé**</span><span class="sxs-lookup"><span data-stu-id="df956-147">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="df956-148">**Créer un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat d’entreprise**</span><span class="sxs-lookup"><span data-stu-id="df956-148">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="df956-149">**Créer un compte d’identification et classique compte d’identification à l’aide d’un certificat auto-signé Bonjour cloud d’Azure Government**</span><span class="sxs-lookup"><span data-stu-id="df956-149">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="df956-150">Après l’exécution de script de hello, vous serez invité à tooauthenticate avec Azure.</span><span class="sxs-lookup"><span data-stu-id="df956-150">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="df956-151">Connectez-vous avec un compte qui est membre du rôle Administrateurs d’abonnement hello et coadministrateur de l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="df956-151">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="df956-152">Une fois le script de hello a été exécutée correctement, notez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="df956-152">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="df956-153">Si vous avez créé un classique compte d’identification avec un certificat auto-signé de public (fichier .cer), le script de hello crée et enregistre toohello dossier des fichiers temporaires sur votre ordinateur sous le profil utilisateur hello *%USERPROFILE%\AppData\Local\Temp*, que vous avez utilisé la session de PowerShell tooexecute hello.</span><span class="sxs-lookup"><span data-stu-id="df956-153">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="df956-154">Si vous avez créé un compte d’identification Classic avec un certificat public d’entreprise (fichier .cer), utilisez ce certificat.</span><span class="sxs-lookup"><span data-stu-id="df956-154">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="df956-155">Suivez les instructions de hello pour [téléchargement un toohello de certificat d’API de gestion portail Azure classic](../azure-api-management-certs.md), puis validez de configuration des informations d’identification hello avec des ressources de déploiement classique à l’aide de hello [exemple de code tooauthenticate avec des ressources de déploiement classique Azure](automation-verify-runas-authentication.md#classic-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="df956-155">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with classic deployment resources by using hello [sample code tooauthenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="df956-156">Si vous l’avez fait *pas* créer classique compte d’identification, de s’authentifier auprès des ressources du Gestionnaire de ressources et de valider la configuration des informations d’identification hello à l’aide de hello [exemple de code pour s’authentifier auprès de gestion des services ressources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="df956-156">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="df956-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="df956-157">Next steps</span></span>
* <span data-ttu-id="df956-158">Pour plus d’informations sur les principaux de Service, voir la rubrique trop[les objets de Principal du Service et Application](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="df956-158">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="df956-159">Pour plus d’informations sur les certificats et les services Azure, consultez trop[vue d’ensemble des certificats pour les Services de Cloud Azure](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="df956-159">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
