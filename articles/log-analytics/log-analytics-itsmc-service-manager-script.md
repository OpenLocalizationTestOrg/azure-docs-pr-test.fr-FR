---
title: "Script automatisé permettant de créer l’application web Service Manager pour se connecter au connecteur de gestion des services informatiques dans OMS | Microsoft Docs"
description: "Créez une application web Service Manager à l’aide d’un script automatisé pour vous connecter au connecteur de gestion des services informatiques dans OMS, et pour surveiller et gérer centralement les éléments de travail ITSM."
services: log-analytics
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 879e819f-d880-41c8-9775-a30907e42059
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: v-jysur
ms.openlocfilehash: ad69d82e57be8bfd9ba40dd88cbc0a979c9e1722
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-service-manager-web-app-using-the-automated-script-preview"></a><span data-ttu-id="1cfba-103">Créer l’application web Service Manager en utilisant le script automatisé (préversion)</span><span class="sxs-lookup"><span data-stu-id="1cfba-103">Create Service Manager Web app using the automated script (Preview)</span></span>

<span data-ttu-id="1cfba-104">Utilisez le script suivant pour créer l’application web pour votre instance Service Manager.</span><span class="sxs-lookup"><span data-stu-id="1cfba-104">Use the following script to create the Web app for your Service Manager instance.</span></span> <span data-ttu-id="1cfba-105">Informations supplémentaires sur la connexion à Service Manager : [application web Service Manager](log-analytics-itsmc-connections.md#create-and-deploy-service-manager-web-app-service)</span><span class="sxs-lookup"><span data-stu-id="1cfba-105">More information about Service Manager connection is here: [Service Manager Web app](log-analytics-itsmc-connections.md#create-and-deploy-service-manager-web-app-service)</span></span>

<span data-ttu-id="1cfba-106">Exécutez le script en fournissant les informations obligatoires suivantes :</span><span class="sxs-lookup"><span data-stu-id="1cfba-106">Run the script by providing the following required details:</span></span>

- <span data-ttu-id="1cfba-107">Détails de l’abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="1cfba-107">Azure subscription details</span></span>
- <span data-ttu-id="1cfba-108">Nom de groupe ressources</span><span class="sxs-lookup"><span data-stu-id="1cfba-108">Resource group name</span></span>
- <span data-ttu-id="1cfba-109">Emplacement</span><span class="sxs-lookup"><span data-stu-id="1cfba-109">Location</span></span>
- <span data-ttu-id="1cfba-110">Détails du serveur Service Manager (nom du serveur, domaine, nom d’utilisateur et mot de passe)</span><span class="sxs-lookup"><span data-stu-id="1cfba-110">Service Manager server details (server name,    domain, username and password)</span></span>
- <span data-ttu-id="1cfba-111">Préfixe de nom de site pour votre application Web</span><span class="sxs-lookup"><span data-stu-id="1cfba-111">Site name prefix for your Web app</span></span>
- <span data-ttu-id="1cfba-112">Espace de noms ServiceBus.</span><span class="sxs-lookup"><span data-stu-id="1cfba-112">ServiceBus Namespace.</span></span>

<span data-ttu-id="1cfba-113">Le script va créer l’application web en utilisant le nom que vous avez spécifié (avec quelques chaînes supplémentaires pour le rendre unique).</span><span class="sxs-lookup"><span data-stu-id="1cfba-113">The script will create the Web app using the name that you specified (along with few additional strings to make it unique).</span></span> <span data-ttu-id="1cfba-114">Il génère **l’URL de l’application web**, **l’ID client** et la **clé secrète client**.</span><span class="sxs-lookup"><span data-stu-id="1cfba-114">It generates the **Web app URL**, **client ID** and **client secret**.</span></span>

<span data-ttu-id="1cfba-115">Enregistrez ces valeurs. Vous en aurez besoin lorsque vous créez une connexion avec le connecteur de gestion des services informatiques.</span><span class="sxs-lookup"><span data-stu-id="1cfba-115">Save these values, you will need these when you create a connection with IT Service Management Connector.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1cfba-116">Prérequis</span><span class="sxs-lookup"><span data-stu-id="1cfba-116">Prerequisites</span></span>

 <span data-ttu-id="1cfba-117">Windows Management Framework 5.0 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1cfba-117">Windows Management Framework 5.0 or above.</span></span>
<span data-ttu-id="1cfba-118">Par défaut, Windows 10 a la version 5.1.</span><span class="sxs-lookup"><span data-stu-id="1cfba-118">Windows 10 has 5.1 by default.</span></span> <span data-ttu-id="1cfba-119">Vous pouvez télécharger l’infrastructure [ici](https://www.microsoft.com/download/details.aspx?id=53347) :</span><span class="sxs-lookup"><span data-stu-id="1cfba-119">You can download the framework from [here](https://www.microsoft.com/download/details.aspx?id=53347):</span></span>

<span data-ttu-id="1cfba-120">Utilisez le script suivant :</span><span class="sxs-lookup"><span data-stu-id="1cfba-120">Use the following script:</span></span>

```
####################################
# User Configuration Section Begins
####################################

# Subscription name in Azure account. Check in Azure Portal.
$azureSubscriptionName = ""

# Resource group name for resource deployment. Could be an existing resource group or a new one to be created.
$resourceGroupName = ""

# Location for existing resource group or new resource group deployment
################################### List of available regions #################################################
# centralus,eastasia,southeastasia,eastus,eastus2,westus,westus2,northcentralus,southcentralus,westcentralus,
# northeurope,westeurope,japaneast,japanwest,brazilsouth,australiasoutheast,australiaeast,westindia,southindia,
# centralindia,canadacentral,canadaeast,uksouth,ukwest.
###############################################################################################################
$location = ""

# Service Manager Authentication Settings
$serverName = ""
$domain = ""
$username = ""
$password = ""


# Azure site Name Prefix. Default is "smoc". It can be configured to any desired value.
$siteNamePrefix = ""

# Service Bus namespace. Please provide an already existing service bus namespace.
# If it doesn't exist, a new one will be created with name $siteName + "sbn" which can also be later reused for any other hybrid connections.
$serviceName = ""

##################################
# User Configuration Section Ends
##################################

################
# Installations
################

# Allowing the execution of the script for current user.  
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser -Force

Write-Host "Checking for required modules..."
if(!(Get-PackageProvider -Name NuGet))
{
   Write-Host "Installing NuGet Package Provider..."
   Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Scope CurrentUser -Force -WarningAction SilentlyContinue
}
$module = Get-Module -ListAvailable -Name AzureRM

if(!$module -or ($module[0].Version.Major -lt 4))
{
    Write-Host "Installing AzureRm Module..."  
    try
    {
        # In case of Win 10 Anniversary update
        Install-Module AzureRM -MinimumVersion 4.1.0 -Scope CurrentUser -Force -WarningAction SilentlyContinue -AllowClobber
    }
    catch
    {
        Install-Module AzureRM -MinimumVersion 4.1.0 -Scope CurrentUser -Force -WarningAction SilentlyContinue
    }

}

Write-Host "Requirement check complete!!"

#############
# Parameters
#############

$errorActionPreference = "Stop"

$templateUri = "https://raw.githubusercontent.com/SystemCenterServiceManager/SMOMSConnector/master/azuredeploy.json"

if(!$siteNamePrefix)
{
    $siteNamePrefix = "smoc"
}

Add-AzureRmAccount

$context = Set-AzureRmContext -SubscriptionName $azureSubscriptionName -WarningAction SilentlyContinue

$resourceProvider = Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web

if(!$resourceProvider -or $resourceProvider[0].RegistrationState -ne "Registered")
{
    try
    {
        Write-Host "Registering Microsoft.Web Resource Provider"
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Web
    }
    catch
    {
        Write-Host "Failed to Register Microsoft.Web Resource Provider. Please register it in Azure Portal."
        exit
    }   
}
do
{
    $rand = Get-Random -Maximum 32000

    $siteName = $siteNamePrefix + $rand

    $resource = Find-AzureRmResource -ResourceNameContains $siteName -ResourceType Microsoft.Web/sites

}while($resource)

$azureSite = "https://"+$siteName+".azurewebsites.net"

##############
# MAIN Begins
##############

# Web App Deployment
####################

$tenant = $context.Tenant.Id
if(!$tenant)
{
    #For backward compatibility with older versions
    $tenant = $context.Tenant.TenantId
}
try
{
    Get-AzureRmResourceGroup -Name $resourceGroupName
}
catch
{
    New-AzureRmResourceGroup -Location $location -Name $resourceGroupName
}

Write-Output "Web App Deployment in progress...."

New-AzureRmResourceGroupDeployment -TemplateUri $templateUri -siteName $siteName -ResourceGroupName $resourceGroupName

Write-Output "Web App Deployed successfully!!"

# AAD Authentication
####################

Add-Type -AssemblyName System.Web

$clientSecret = [System.Web.Security.Membership]::GeneratePassword(30,2).ToString()

try
{

    Write-Host "Creating AzureAD application..."

    $adApp = New-AzureRmADApplication -DisplayName $siteName -HomePage $azureSite -IdentifierUris $azureSite -Password $clientSecret

    Write-Host "AzureAD application created succesfully!!"
}
catch
{
    # Delete the deployed web app if Azure AD application fails
    Remove-AzureRmResource -ResourceGroupName $resourceGroupName -ResourceName $siteName -ResourceType Microsoft.Web/sites -Force

    Write-Host "Faiure occured in Azure AD application....Try again!!"

    exit

}

$clientId = $adApp.ApplicationId

$servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $clientId

# Web App Configuration
#######################
try
{

    Write-Host "Configuring deployed Web-App..."
    $webApp = Get-AzureRMWebAppSlot -ResourceGroupName $resourceGroupName -Name $siteName -Slot production -WarningAction SilentlyContinue

    $appSettingList = $webApp.SiteConfig.AppSettings

    $appSettings = @{}
    ForEach ($item in $appSettingList) {
        $appSettings[$item.Name] = $item.Value
    }
    $appSettings['ida:Tenant'] = $tenant
    $appSettings['ida:Audience'] = $azureSite
    $appSettings['ida:ServerName'] = $serverName
    $appSettings['ida:Domain'] = $domain
    $appSettings['ida:Username'] = $userName

    $connStrings = @{}
    $kvp = @{"Type"="Custom"; "Value"=$password}
    $connStrings['ida:Password'] = $kvp

    Set-AzureRMWebAppSlot -ResourceGroupName $resourceGroupName -Name $siteName -AppSettings $appSettings -ConnectionStrings $connStrings -Slot production -WarningAction SilentlyContinue

}
catch
{
    Write-Host "Web App configuration failed. Please ensure all values are provided in Service Manager Authentication Settings in User Configuration Section"

    # Delete the AzureRm AD Application if confiuration fails
    Remove-AzureRmADApplication -ObjectId $adApp.ObjectId -Force

    # Delete the deployed web app if configuration fails
    Remove-AzureRmResource -ResourceGroupName $resourceGroupName -ResourceName $siteName -ResourceType Microsoft.Web/sites -Force

    exit
}


# Relay Namespace
###################

if(!$serviceName)
{
    $serviceName = $siteName + "sbn"
}

$resourceProvider = Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Relay

if(!$resourceProvider -or $resourceProvider[0].RegistrationState -ne "Registered")
{
    try
    {
        Write-Host "Registering Microsoft.Relay Resource Provider"
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Relay
    }
    catch
    {
        Write-Host "Failed to Register Microsoft.Relay Resource Provider. Please register it in Azure Portal."
    }   
}

$resource = Find-AzureRmResource -ResourceNameContains $serviceName -ResourceType Microsoft.Relay/namespaces

if(!$resource)
{
    $serviceName = $siteName + "sbn"
    $properties = @{
        "sku" = @{
            "name"= "Standard"
            "tier"= "Standard"
            "capacity"= 1
         }
    }
    try
    {
        Write-Host "Creating Service Bus namespace..."
        New-AzureRmResource -ResourceName $serviceName -Location $location -PropertyObject $properties -ResourceGroupName $resourceGroupName -ResourceType Microsoft.Relay/namespaces -ApiVersion 2016-07-01 -Force
    }
    catch
    {
        $err = $TRUE
        Write-Host "Creation of Service Bus Namespace failed...Please create it manually from Azure Portal.`n"
    }

}

Write-Host "Note: Please Configure Hybrid connection in the Networking section of the web application in Azure Portal to link to the on-premises system.`n"
Write-Host "App Details"
Write-Host "============"
Write-Host "App Name:"  $siteName
Write-Host "Client Id:"  $clientId
Write-Host "Client Secret:"  $clientSecret
Write-Host "URI:"  $azureSite
if(!$err)
{
    Write-Host "ServiceBus Namespace:"  $serviceName  
}

```
## <a name="next-steps"></a><span data-ttu-id="1cfba-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1cfba-121">Next steps</span></span>
<span data-ttu-id="1cfba-122">[Configurez la connexion hybride](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="1cfba-122">[Configure the Hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>