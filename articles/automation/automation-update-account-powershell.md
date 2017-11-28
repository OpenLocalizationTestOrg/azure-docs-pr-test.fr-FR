---
title: "Création d’un compte d’identification Azure Automation avec PowerShell | Microsoft Docs"
description: "Cet article décrit comment mettre à niveau votre compte Automation avec PowerShell pour créer des comptes d’identification si vous n’avez pas effectué cette étape lors de la création initiale à partir du portail."
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
ms.openlocfilehash: a41a57ee3815a815c23e9bbe2dd0309e6c61c8f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="update-automation-run-as-account-using-powershell"></a><span data-ttu-id="c9afe-103">Mise à jour d’un compte d’identification Automation à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9afe-103">Update Automation Run As account using PowerShell</span></span>
<span data-ttu-id="c9afe-104">Vous pouvez utiliser PowerShell pour mettre à jour votre compte Automation existant si :</span><span class="sxs-lookup"><span data-stu-id="c9afe-104">You can use PowerShell to update your existing Automation account if:</span></span>

* <span data-ttu-id="c9afe-105">Vous créez un compte Automation sans compte d’identification.</span><span class="sxs-lookup"><span data-stu-id="c9afe-105">You create an Automation account but decline to create the Run As account.</span></span>
* <span data-ttu-id="c9afe-106">Vous possédez déjà un compte Automation pour gérer les ressources Resource Manager et vous voulez le mettre à jour pour inclure le compte d’identification pour l’authentification du Runbook.</span><span class="sxs-lookup"><span data-stu-id="c9afe-106">You already use an Automation account to manage Resource Manager resources and you want to update the account to include the Run As account for runbook authentication.</span></span>
* <span data-ttu-id="c9afe-107">Vous possédez déjà un compte Automation pour gérer les ressources classiques et souhaitez le mettre à jour pour utiliser le compte d’identification Classic au lieu de créer un compte et d’y migrer vos Runbooks et ressources.</span><span class="sxs-lookup"><span data-stu-id="c9afe-107">You already use an Automation account to manage classic resources and you want to update it to use the Classic Run As account instead of creating a new account and migrating your runbooks and assets to it.</span></span>   
* <span data-ttu-id="c9afe-108">Vous souhaitez créer un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat émis par votre AC d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="c9afe-108">You want to create a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9afe-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c9afe-109">Prerequisites</span></span>

* <span data-ttu-id="c9afe-110">Ce script peut uniquement être exécuté sur Windows 10 et sur Windows Server 2016 avec les modules Azure Resource Manager 2.01 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="c9afe-110">The script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="c9afe-111">Il n’est pas pris en charge dans les versions antérieures de Windows.</span><span class="sxs-lookup"><span data-stu-id="c9afe-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="c9afe-112">Azure PowerShell 1.0 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="c9afe-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="c9afe-113">Pour plus d’informations sur la version PowerShell 1.0, voir [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c9afe-113">For information about the PowerShell 1.0 release, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="c9afe-114">Un compte Automation, référencé en tant que valeur des paramètres *–AutomationAccountName* et *-ApplicationDisplayName* dans le script PowerShell suivant.</span><span class="sxs-lookup"><span data-stu-id="c9afe-114">An Automation account, which is referenced as the value for the *–AutomationAccountName* and *-ApplicationDisplayName* parameters in the following PowerShell script.</span></span>

<span data-ttu-id="c9afe-115">Pour obtenir les valeurs des paramètres *SubscriptionID*, *ResourceGroup* et *AutomationAccountName*, qui sont des paramètres requis pour les scripts, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c9afe-115">To get the values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for the scripts, do the following:</span></span>
1. <span data-ttu-id="c9afe-116">Sélectionnez votre compte Automation à partir du panneau **Compte Automation** du portail Azure, puis sélectionnez **Tous les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="c9afe-116">In the Azure portal, select your Automation account on the **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="c9afe-117">Dans le panneau **Tous les paramètres**, sous **Paramètres du compte**, sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="c9afe-117">On the **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="c9afe-118">Notez les valeurs dans le panneau **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="c9afe-118">Note the values on the **Properties** blade.</span></span>

![Panneau Propriétés du compte Automation](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

## <a name="create-run-as-account-powershell-script"></a><span data-ttu-id="c9afe-120">Créer le script PowerShell d’un compte d’identification</span><span class="sxs-lookup"><span data-stu-id="c9afe-120">Create Run As Account PowerShell script</span></span>
<span data-ttu-id="c9afe-121">Ce script PowerShell prend en charge les configurations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c9afe-121">This PowerShell script includes support for the following configurations:</span></span>

* <span data-ttu-id="c9afe-122">Créez un compte d’identification à l’aide d’un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="c9afe-122">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="c9afe-123">Créez un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="c9afe-123">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="c9afe-124">Créez un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="c9afe-124">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="c9afe-125">Créez un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat auto-signé dans le cloud Azure Government.</span><span class="sxs-lookup"><span data-stu-id="c9afe-125">Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud.</span></span>

<span data-ttu-id="c9afe-126">Selon l’option de configuration que vous sélectionnez, le script crée les éléments suivants.</span><span class="sxs-lookup"><span data-stu-id="c9afe-126">Depending on the configuration option you select, the script creates the following items.</span></span>

<span data-ttu-id="c9afe-127">**Pour les comptes d’identification :**</span><span class="sxs-lookup"><span data-stu-id="c9afe-127">**For Run As accounts:**</span></span>

* <span data-ttu-id="c9afe-128">Crée une application Azure AD qui sera exportée avec la clé publique du certificat auto-signé ou du certificat d’entreprise, crée un compte de principal de service pour cette application dans Azure AD et affecte le rôle Collaborateur pour le compte dans votre abonnement actuel.</span><span class="sxs-lookup"><span data-stu-id="c9afe-128">Creates an Azure AD application to be exported with either the self-signed or enterprise certificate public key, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="c9afe-129">Vous pouvez remplacer ce paramètre par un rôle de propriétaire ou par tout autre rôle.</span><span class="sxs-lookup"><span data-stu-id="c9afe-129">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="c9afe-130">Pour plus d’informations, voir [Contrôle d’accès en fonction du rôle dans Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="c9afe-130">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="c9afe-131">Crée une ressource de certificat Automation nommée *AzureRunAsCertificate* dans le compte Automation spécifié.</span><span class="sxs-lookup"><span data-stu-id="c9afe-131">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="c9afe-132">La ressource de certificat conserve la clé privée du certificat utilisée par l’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9afe-132">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="c9afe-133">Crée une ressource de connexion Automation nommée *AzureRunAsConnection* dans le compte Automation spécifié.</span><span class="sxs-lookup"><span data-stu-id="c9afe-133">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="c9afe-134">La ressource de connexion conserve les ID applicationId, tenantId et subscriptionId, et l’empreinte de certificat.</span><span class="sxs-lookup"><span data-stu-id="c9afe-134">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="c9afe-135">**Pour les comptes d’identification Classic :**</span><span class="sxs-lookup"><span data-stu-id="c9afe-135">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="c9afe-136">Crée une ressource de certificat Automation nommée *AzureClassicRunAsCertificate*dans le compte Automation spécifié.</span><span class="sxs-lookup"><span data-stu-id="c9afe-136">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="c9afe-137">La ressource de certificat conserve la clé privée du certificat utilisée par le certificat de gestion.</span><span class="sxs-lookup"><span data-stu-id="c9afe-137">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="c9afe-138">Crée une ressource de connexion Automation nommée *AzureClassicRunAsConnection* dans le compte Automation spécifié.</span><span class="sxs-lookup"><span data-stu-id="c9afe-138">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="c9afe-139">La ressource de connexion conserve le nom de l’abonnement, l’ID subscriptionId et le nom de ressource de certificat.</span><span class="sxs-lookup"><span data-stu-id="c9afe-139">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="c9afe-140">Si vous sélectionnez l’option permettant de créer un compte d’identification Classic, après l’exécution du script, vous devez charger le certificat public (extension de nom de fichier .cer) dans le magasin de gestion de l’abonnement dans lequel le compte Automation a été créé.</span><span class="sxs-lookup"><span data-stu-id="c9afe-140">If you select either option for creating a Classic Run As account, after the script is executed, upload the public certificate (.cer file name extension) to the management store for the subscription that the Automation account was created in.</span></span>
> 

1. <span data-ttu-id="c9afe-141">Enregistrez le script suivant sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c9afe-141">Save the following script on your computer.</span></span> <span data-ttu-id="c9afe-142">Dans cet exemple, enregistrez-le sous le nom de fichier *New-RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="c9afe-142">In this example, save it with the filename *New-RunAsAccount.ps1*.</span></span>

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

        # Sleep here for a few seconds to allow the service principal application to become active (ordinarily takes a few seconds)
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
           Write-Error -Message "Please install the latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate the ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload the .cer format of #CERT# to the Management store by following the steps below." + [Environment]::NewLine +
                    "Log in to the Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload the .cer format of #CERT#"

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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate the ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="c9afe-143">Sur votre ordinateur, démarrez **Windows PowerShell** dans l’écran **Démarrer** avec des droits de l’utilisateur élevés.</span><span class="sxs-lookup"><span data-stu-id="c9afe-143">On your computer, start **Windows PowerShell** from the **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="c9afe-144">À partir de l’interface de ligne de commande avec élévation de privilèges, accédez au dossier contenant le script que vous avez créé à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="c9afe-144">From the elevated command-line shell, go to the folder that contains the script you created in step 1.</span></span>  
4. <span data-ttu-id="c9afe-145">Exécutez le script en utilisant les valeurs de paramètre pour la configuration dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="c9afe-145">Execute the script by using the parameter values for the configuration you require.</span></span>

    <span data-ttu-id="c9afe-146">**Créer un compte d’identification à l’aide d’un certificat auto-signé**</span><span class="sxs-lookup"><span data-stu-id="c9afe-146">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="c9afe-147">**Créer un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat auto-signé**</span><span class="sxs-lookup"><span data-stu-id="c9afe-147">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="c9afe-148">**Créer un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat d’entreprise**</span><span class="sxs-lookup"><span data-stu-id="c9afe-148">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="c9afe-149">**Créer un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat auto-signé dans le cloud Azure Government**</span><span class="sxs-lookup"><span data-stu-id="c9afe-149">**Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="c9afe-150">Une fois le script exécuté, vous êtes invité à vous authentifier auprès d’Azure.</span><span class="sxs-lookup"><span data-stu-id="c9afe-150">After the script has executed, you will be prompted to authenticate with Azure.</span></span> <span data-ttu-id="c9afe-151">Connectez-vous avec un compte membre du rôle Administrateurs des abonnements et coadministrateur de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="c9afe-151">Sign in with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>
    >
    >

<span data-ttu-id="c9afe-152">Une fois le script exécuté, notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="c9afe-152">After the script has executed successfully, note the following:</span></span>
* <span data-ttu-id="c9afe-153">Si vous avez créé un compte d’identification Classic avec un certificat public auto-signé (fichier .cer), le script le crée et l’enregistre dans le dossier de fichiers temporaires sur votre ordinateur, sous le profil d’utilisateur *%USERPROFILE%\AppData\Local\Temp* utilisé pour exécuter la session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c9afe-153">If you created a Classic Run As account with a self-signed public certificate (.cer file), the script creates and saves it to the temporary files folder on your computer under the user profile *%USERPROFILE%\AppData\Local\Temp*, which you used to execute the PowerShell session.</span></span>
* <span data-ttu-id="c9afe-154">Si vous avez créé un compte d’identification Classic avec un certificat public d’entreprise (fichier .cer), utilisez ce certificat.</span><span class="sxs-lookup"><span data-stu-id="c9afe-154">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="c9afe-155">Suivez les instructions pour [charger un certificat d’API de gestion vers le portail Azure Classic](../azure-api-management-certs.md), puis validez la configuration des informations d’identification avec les ressources de déploiement classique à l’aide de [l’exemple de code pour l’authentification avec les ressources de déploiement Azure Classic](automation-verify-runas-authentication.md#classic-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="c9afe-155">Follow the instructions for [uploading a management API certificate to the Azure classic portal](../azure-api-management-certs.md), and then validate the credential configuration with classic deployment resources by using the [sample code to authenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="c9afe-156">Si vous n’avez *pas* créé de compte d’identification Classic, authentifiez-vous avec des ressources Resource Manager et validez la configuration des informations d’identification à l’aide [l’exemple de code pour l’authentification avec les ressources de gestion des services](automation-verify-runas-authentication.md#automation-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="c9afe-156">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate the credential configuration by using the [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9afe-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c9afe-157">Next steps</span></span>
* <span data-ttu-id="c9afe-158">Pour plus d’informations sur les principaux de service, consultez l’article [Objets Principal du service et Application](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="c9afe-158">For more information about Service Principals, refer to [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="c9afe-159">Pour plus d’informations sur les certificats et les services Azure, consultez la page [Vue d’ensemble des certificats pour Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="c9afe-159">For more information about certificates and Azure services, refer to [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
