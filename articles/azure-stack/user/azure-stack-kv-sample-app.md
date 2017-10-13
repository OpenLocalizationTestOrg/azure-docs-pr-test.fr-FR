---
title: "Autoriser les applications à récupérer les secrets d’un coffre de clés dans Azure Stack | Microsoft Docs"
description: "Utiliser un exemple d’application à utiliser avec Azure Stack Key Vault"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 3748b719-e269-4b48-8d7d-d75a84b0e1e5
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/26/2017
ms.author: sngun
ms.openlocfilehash: 7cfb78cc5219d4adab5ceddc9d7eb8d1fc71b678
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2017
---
# <a name="sample-application-that-uses-keys-and-secrets-stored-in-a-key-vault"></a><span data-ttu-id="127fc-103">Exemple d’application qui utilise des clés et des secrets stockés dans un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="127fc-103">Sample application that uses keys and secrets stored in a key vault</span></span>

<span data-ttu-id="127fc-104">Dans cet article, vous découvrez comment exécuter un exemple d’application (HelloKeyVault) qui récupère les clés et les secrets d’un coffre de clés dans Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="127fc-104">In this article, we show you how to run a sample application (HelloKeyVault) that retrieves keys and secrets from a key vault in Azure Stack.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="127fc-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="127fc-105">Prerequisites</span></span> 

<span data-ttu-id="127fc-106">Effectuez les étapes prérequises suivantes à partir du [kit de développement](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop) ou à partir d’un client externe Windows si vous êtes [connecté via un VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) :</span><span class="sxs-lookup"><span data-stu-id="127fc-106">Run the following prerequisites either from the [Development Kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span>

* <span data-ttu-id="127fc-107">Installez les [modules Azure PowerShell compatibles avec Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="127fc-107">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
* <span data-ttu-id="127fc-108">Téléchargez les [outils nécessaires pour utiliser Azure Stack](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="127fc-108">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span> 

## <a name="create-and-get-the-key-vault-and-application-settings"></a><span data-ttu-id="127fc-109">Créer et obtenir les paramètres du coffre de clés et de l’application</span><span class="sxs-lookup"><span data-stu-id="127fc-109">Create and get the key vault and application settings</span></span>

<span data-ttu-id="127fc-110">Vous devez d’abord créer un coffre de clés dans Azure Stack et inscrire une application dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="127fc-110">First, you should create a key vault in Azure Stack, and register an application in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="127fc-111">Vous pouvez créer et inscrire les coffres de clés à l’aide du portail Azure ou de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="127fc-111">You can create and register the key vaults by using the Azure portal or PowerShell.</span></span> <span data-ttu-id="127fc-112">Cet article explique comment effectuer les tâches avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="127fc-112">This article shows you the PowerShell way to do the tasks.</span></span> <span data-ttu-id="127fc-113">Par défaut, ce script PowerShell crée une application dans Active Directory.</span><span class="sxs-lookup"><span data-stu-id="127fc-113">By default, this PowerShell script creates a new application in Active Directory.</span></span> <span data-ttu-id="127fc-114">Toutefois, vous pouvez également utiliser l’une de vos applications existantes.</span><span class="sxs-lookup"><span data-stu-id="127fc-114">However, you can also use one of your existing applications.</span></span> <span data-ttu-id="127fc-115">Veillez à fournir une valeur pour les variables `aadTenantName` et `applicationPassword`.</span><span class="sxs-lookup"><span data-stu-id="127fc-115">Make sure to provide a value for the `aadTenantName` and `applicationPassword` variables.</span></span> <span data-ttu-id="127fc-116">Si vous ne spécifiez pas de valeur pour la variable `applicationPassword`, ce script génère un mot de passe aléatoire.</span><span class="sxs-lookup"><span data-stu-id="127fc-116">If you don't specify a value for the `applicationPassword` variable, this script generates a random password.</span></span> 

```powershell
$vaultName           = 'myVault'
$resourceGroupName   = 'myResourceGroup'
$applicationName     = 'myApp'
$location            = 'local' 

# Password for the application. If not specified, this script will generate a random password during app creation.
$applicationPassword = '' 
                         
# Function to generate a random password for the application.
Function GenerateSymmetricKey()
{
    $key = New-Object byte[](32)
    $rng = [System.Security.Cryptography.RNGCryptoServiceProvider]::Create()
    $rng.GetBytes($key)
    return [System.Convert]::ToBase64String($key)
}

Write-Host 'Please log into your Azure Stack user environment' -foregroundcolor Green

$tenantARM = "https://management.local.azurestack.external"
$aadTenantName = "PLEASE FILL THIS IN WITH YOUR AAD TENANT NAME. FOR EXAMPLE: myazurestack.onmicrosoft.com"

# Configure the Azure Stack operator’s PowerShell environment.
Add-AzureRMEnvironment `
  -Name "AzureStackUser" `
  -ArmEndpoint $tenantARM

Set-AzureRmEnvironment `
  -Name "AzureStackAdmin" `
  -GraphAudience "https://graph.windows.net/"

$TenantID = Get-AzsDirectoryTenantId `
  -AADTenantName $aadTenantName `
  -EnvironmentName AzureStackUser

# Sign in to the user portal.
Login-AzureRmAccount `
  -EnvironmentName "AzureStackUser" `
  -TenantId $TenantID `
  
$now = [System.DateTime]::Now
$oneYearFromNow = $now.AddYears(1)

$applicationPassword = GenerateSymmetricKey
    
# Create a new Azure AD application.
$identifierUri = [string]::Format("http://localhost:8080/{0}",[Guid]::NewGuid().ToString("N"))
$homePage = "http://contoso.com"

Write-Host "Creating a new AAD Application"
$ADApp = New-AzureRmADApplication `
  -DisplayName $applicationName `
  -HomePage $homePage `
  -IdentifierUris $identifierUri `
  -StartDate $now `
  -EndDate $oneYearFromNow `
  -Password $applicationPassword

Write-Host "Creating a new AAD service principal"
$servicePrincipal = New-AzureRmADServicePrincipal `
  -ApplicationId $ADApp.ApplicationId

# Create a new resource group and a key vault within that resource group.
New-AzureRmResourceGroup `
  -Name $resourceGroupName `
  -Location $location   

Write-Host "Creating vault $vaultName"
$vault = New-AzureRmKeyVault -VaultName $vaultName `
  -ResourceGroupName $resourceGroupName `
  -Sku standard `
  -Location $location

# Specify full privileges to the vault for the application.
Write-Host "Setting access policy"
Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName `
  -ObjectId $servicePrincipal.Id `
  -PermissionsToKeys all `
  -PermissionsToSecrets all

Write-Host "Paste the following settings into the app.config file for the HelloKeyVault project:"
'<add key="VaultUrl" value="' + $vault.VaultUri + '"/>'
'<add key="AuthClientId" value="' + $servicePrincipal.ApplicationId + '"/>'
'<add key="AuthClientSecret" value="' + $applicationPassword + '"/>'
Write-Host

``` 

<span data-ttu-id="127fc-117">La capture d’écran suivante montre la sortie du script précédent :</span><span class="sxs-lookup"><span data-stu-id="127fc-117">The following screenshot shows the output of the previous script:</span></span>

![Configuration de l’application](media/azure-stack-kv-sample-app/settingsoutput.png)

<span data-ttu-id="127fc-119">Prenez note des valeurs de **VaultUrl**, **AuthClientId** et **AuthClientSecret** renvoyées par le script précédent.</span><span class="sxs-lookup"><span data-stu-id="127fc-119">Make a note of the **VaultUrl**, **AuthClientId**, and **AuthClientSecret** values returned by the previous script.</span></span> <span data-ttu-id="127fc-120">Vous utiliserez ces valeurs pour exécuter l’application HelloKeyVault.</span><span class="sxs-lookup"><span data-stu-id="127fc-120">You use these values to run the HelloKeyVault application.</span></span>

## <a name="download-and-run-the-sample-application"></a><span data-ttu-id="127fc-121">Télécharger et exécuter l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="127fc-121">Download and run the sample application</span></span>

<span data-ttu-id="127fc-122">Téléchargez l’exemple de coffre de clés à partir de la page [Azure Key Vault client samples](https://www.microsoft.com/en-us/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="127fc-122">Download the key vault sample from the Azure [Key Vault client samples](https://www.microsoft.com/en-us/download/details.aspx?id=45343) page.</span></span> <span data-ttu-id="127fc-123">Extrayez le contenu du fichier .zip sur votre station de travail de développement.</span><span class="sxs-lookup"><span data-stu-id="127fc-123">Extract the contents of the .zip file onto your development workstation.</span></span> <span data-ttu-id="127fc-124">Il existe deux exemples dans le dossier d’exemples.</span><span class="sxs-lookup"><span data-stu-id="127fc-124">There are two samples within the samples folder.</span></span> <span data-ttu-id="127fc-125">Nous utilisons l’exemple HelloKeyVault dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="127fc-125">We use the HellpKeyVault sample in this topic.</span></span> <span data-ttu-id="127fc-126">Accédez au dossier **Microsoft.Azure.KeyVault.Samples** > **samples** > **HelloKeyVault**, puis ouvrez l’application HelloKeyVault dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="127fc-126">Browse to the **Microsoft.Azure.KeyVault.Samples** > **samples** > **HelloKeyVault** folder and open the HelloKeyVault application in Visual Studio.</span></span> 

<span data-ttu-id="127fc-127">Ouvrez le fichier HelloKeyVault\App.config et remplacez les valeurs de l’élément <appSettings> par les valeurs de **VaultUrl**, **AuthClientId** et **AuthClientSecret** renvoyées par le script précédent.</span><span class="sxs-lookup"><span data-stu-id="127fc-127">Open the HelloKeyVault\App.config file and replace the values of the <appSettings> element with the **VaultUrl**, **AuthClientId**, and **AuthClientSecret** values returned by the previous script.</span></span> <span data-ttu-id="127fc-128">Notez que par défaut, le fichier App.config contient un espace réservé pour *AuthCertThumbprint*, mais utilisez *AuthClientSecret* à la place.</span><span class="sxs-lookup"><span data-stu-id="127fc-128">Note that by default the App.config contains a placeholder for *AuthCertThumbprint*, but use *AuthClientSecret* instead.</span></span> <span data-ttu-id="127fc-129">Après avoir remplacé les valeurs, regénérez la solution et démarrez l’application.</span><span class="sxs-lookup"><span data-stu-id="127fc-129">After you replace the settings, rebuild the solution and start the application.</span></span>

![Paramètres de l’application](media/azure-stack-kv-sample-app/appconfig.png)
 
<span data-ttu-id="127fc-131">L’application se connecte à Azure AD, puis utilise ce jeton pour s’authentifier auprès du coffre de clés dans Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="127fc-131">The application signs in to Azure AD, and then uses that token to authenticate to the key vault in Azure Stack.</span></span> <span data-ttu-id="127fc-132">L’application effectue des opérations comme créer, chiffrer, envelopper (wrap), supprimer, etc. sur les clés et les secrets du coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="127fc-132">The application performs operations like create, encrypt, wrap, and delete on the keys and secrets of the key vault.</span></span> <span data-ttu-id="127fc-133">Vous pouvez également transmettre des paramètres spécifiques, comme *encrypt* et *decrypt* à l’application, ce qui garantit que l’application exécute seulement ces opérations sur le coffre.</span><span class="sxs-lookup"><span data-stu-id="127fc-133">You can also pass specific parameters such as *encrypt* and *decrypt* to the application, which makes sure that the application executes only those operations against the vault.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="127fc-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="127fc-134">Next steps</span></span>
[<span data-ttu-id="127fc-135">Déployer une machine virtuelle avec un mot de passe Key Vault</span><span class="sxs-lookup"><span data-stu-id="127fc-135">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)

[<span data-ttu-id="127fc-136">Déployer une machine virtuelle avec un certificat Key Vault</span><span class="sxs-lookup"><span data-stu-id="127fc-136">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)



