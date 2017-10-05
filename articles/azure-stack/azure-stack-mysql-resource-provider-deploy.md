---
title: "Utiliser des bases de données MySQL en tant que PaaS sur Azure Stack | Microsoft Docs"
description: "Découvrez comment déployer le fournisseur de ressources MySQL et fournir des bases de données MySQL en tant que service sur Azure Stack."
services: azure-stack
documentationCenter: 
author: JeffGoldner
manager: bradleyb
editor: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: JeffGo
ms.openlocfilehash: 4e9da524ef9dfa2d5b7150bc6a888536a1435dfd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-mysql-databases-on-microsoft-azure-stack"></a><span data-ttu-id="bf511-103">Utiliser des bases de données MySQL sur Microsoft Azure Stack</span><span class="sxs-lookup"><span data-stu-id="bf511-103">Use MySQL databases on Microsoft Azure Stack</span></span>


<span data-ttu-id="bf511-104">Vous pouvez déployer un fournisseur de ressources MySQL sur Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="bf511-104">You can deploy a MySQL resource provider on Azure Stack.</span></span> <span data-ttu-id="bf511-105">Après avoir déployé le fournisseur de ressources, vous pouvez créer des serveurs et des bases de données MySQL avec des modèles de déploiement Azure Resource Manager et fournir des bases de données MySQL en tant que service.</span><span class="sxs-lookup"><span data-stu-id="bf511-105">After you deploy the resource provider, you can create MySQL servers and databases through Azure Resource Manager deployment templates and provide MySQL databases as a service.</span></span> <span data-ttu-id="bf511-106">Les bases de données MySQL, qui sont courantes sur les sites web, prennent en charge de nombreuses plateformes de site web.</span><span class="sxs-lookup"><span data-stu-id="bf511-106">MySQL databases, which are common on web sites, support many website platforms.</span></span> <span data-ttu-id="bf511-107">Par exemple, après avoir déployé le fournisseur de ressources, vous pouvez créer des sites web WordPress à partir du module complémentaire PaaS (Platform as a Service) Azure Web Apps pour Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="bf511-107">As an example, after you deploy the resource provider, you can create WordPress websites from the Azure Web Apps platform as a service (PaaS) add-on for Azure Stack.</span></span>

<span data-ttu-id="bf511-108">Pour déployer le fournisseur MySQL sur un système qui n’a pas accès à Internet, vous pouvez copier le fichier [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Download/sConnector-Net/mysql-connector-net-6.9.9.msi) sur un partage local et fournir ce nom de partage quand vous y êtes invité (voir ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="bf511-108">To deploy the MySQL provider on a system that does not have internet access, you can copy the file [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Download/sConnector-Net/mysql-connector-net-6.9.9.msi) to a local share and provide that share name when prompted (see below).</span></span> <span data-ttu-id="bf511-109">Vous devez également installer les modules PowerShell Azure et Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="bf511-109">You must also install the Azure and Azure Stack PowerShell modules.</span></span>


## <a name="mysql-server-resource-provider-adapter-architecture"></a><span data-ttu-id="bf511-110">Architecture de l’adaptateur de fournisseur de ressources MySQL Server</span><span class="sxs-lookup"><span data-stu-id="bf511-110">MySQL Server Resource Provider Adapter architecture</span></span>

<span data-ttu-id="bf511-111">Le fournisseur de ressources est constitué de trois composants :</span><span class="sxs-lookup"><span data-stu-id="bf511-111">The resource provider is made up of three components:</span></span>

- <span data-ttu-id="bf511-112">**La machine virtuelle d’adaptateur de fournisseur de ressources MySQL**, qui est une machine virtuelle Windows exécutant les services de fournisseur.</span><span class="sxs-lookup"><span data-stu-id="bf511-112">**The MySQL resource provider adapter VM**, which is a Windows virtual machine running the provider services.</span></span>
- <span data-ttu-id="bf511-113">**Le fournisseur de ressources proprement dit**, qui traite les demandes d’approvisionnement et expose les ressources de base de données.</span><span class="sxs-lookup"><span data-stu-id="bf511-113">**The resource provider itself**, which processes provisioning requests and exposes database resources.</span></span>
- <span data-ttu-id="bf511-114">**Les serveurs qui hébergent MySQL Server**, qui fournissent de la capacité pour les bases de données, appelés serveurs d’hébergement.</span><span class="sxs-lookup"><span data-stu-id="bf511-114">**Servers that host MySQL Server**, which provide capacity for databases, called Hosting Servers.</span></span> 

<span data-ttu-id="bf511-115">Cette version ne crée plus d’instance de MySQL.</span><span class="sxs-lookup"><span data-stu-id="bf511-115">This release no longer creates a MySQL instance.</span></span> <span data-ttu-id="bf511-116">Vous devez les créer et/ou fournir un accès à des instances SQL externes.</span><span class="sxs-lookup"><span data-stu-id="bf511-116">You must create them and/or provide access to external SQL instances.</span></span> <span data-ttu-id="bf511-117">Vous pouvez accéder à la [galerie de démarrage rapide Azure Stack](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) pour obtenir un exemple de modèle capable de créer un serveur MySQL pour vous, ou télécharger et déployer un serveur MySQL à partir de la Place de marché.</span><span class="sxs-lookup"><span data-stu-id="bf511-117">You can visit the [Azure Stack Quickstart Gallery](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) for an example template that can create a MySQL server for you or download and deploy a MySQL Server from the Marketplace.</span></span>

## <a name="deploy-the-resource-provider"></a><span data-ttu-id="bf511-118">Déployer le fournisseur de ressources</span><span class="sxs-lookup"><span data-stu-id="bf511-118">Deploy the resource provider</span></span>

1. <span data-ttu-id="bf511-119">Si ce n’est déjà fait, inscrivez votre Kit de développement et téléchargez l’image Windows Server 2016 Datacenter - Eval à partir de Gestion dans la Place de marché.</span><span class="sxs-lookup"><span data-stu-id="bf511-119">If you have not already done so, register your development kit and download the Windows Server 2016 Datacenter - Eval image downloadable through Marketplace Management.</span></span> <span data-ttu-id="bf511-120">Vous pouvez également utiliser un script pour créer une [image de Windows Server 2016](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).</span><span class="sxs-lookup"><span data-stu-id="bf511-120">You can also use a script to create a [Windows Server 2016 image](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).</span></span>

2. <span data-ttu-id="bf511-121">[Téléchargez le fichier binaire du fournisseur de ressources MySQL](https://aka.ms/azurestackmysqlrp) et extrayez-le sur l’hôte du Kit de développement.</span><span class="sxs-lookup"><span data-stu-id="bf511-121">[Download the MySQL resource provider binaries file](https://aka.ms/azurestackmysqlrp) and extract it on the development kit host.</span></span>

3. <span data-ttu-id="bf511-122">Connectez-vous à l’hôte du Kit de développement et extrayez le fichier du programme d’installation du fournisseur de ressources MySQL dans un répertoire temporaire.</span><span class="sxs-lookup"><span data-stu-id="bf511-122">Sign in to the development kit host, and extract the MySQL RP installer file to a temporary directory.</span></span>

4. <span data-ttu-id="bf511-123">Le certificat racine Azure Stack est récupéré et un certificat auto-signé est créé dans le cadre de ce processus.</span><span class="sxs-lookup"><span data-stu-id="bf511-123">The Azure Stack root certificate is retrieved and a self-signed certificate is created as part of this process.</span></span> 

    <span data-ttu-id="bf511-124">__Facultatif :__ Si vous devez fournir vos propres certificats, préparez-les et copiez-les dans un répertoire local si vous souhaitez personnaliser les certificats (passés au script d’installation).</span><span class="sxs-lookup"><span data-stu-id="bf511-124">__Optional:__ If you need to provide your own, prepare the certificates and copy to a local directory if you wish to customize the certificates (passed to the installation script).</span></span> <span data-ttu-id="bf511-125">Vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="bf511-125">You need the following:</span></span>

    <span data-ttu-id="bf511-126">a.</span><span class="sxs-lookup"><span data-stu-id="bf511-126">a.</span></span> <span data-ttu-id="bf511-127">Un certificat générique pour *.dbadapter.\<région\>.\<fqdn_externe\>.</span><span class="sxs-lookup"><span data-stu-id="bf511-127">A wildcard certificate for *.dbadapter.\<region\>.\<external fqdn\>.</span></span> <span data-ttu-id="bf511-128">Ce certificat doit être approuvé, par exemple émis par une autorité de certification (autrement dit, la chaîne d’approbation doit exister sans qu’aucun certificat intermédiaire ne soit nécessaire). (Vous pouvez utiliser un certificat de site unique avec le nom de machine virtuelle explicite que vous fournissez lors de l’installation.)</span><span class="sxs-lookup"><span data-stu-id="bf511-128">This certificate must be trusted, such as would be issued by a certificate authority (that is, the chain of trust must exist without requiring intermediate certificates.) (A single site certificate can be used with the explicit VM name you provide during install.)</span></span>

    <span data-ttu-id="bf511-129">b.</span><span class="sxs-lookup"><span data-stu-id="bf511-129">b.</span></span> <span data-ttu-id="bf511-130">Le certificat racine utilisé par Azure Resource Manager pour votre instance d’Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="bf511-130">The root certificate used by the Azure Resource Manager for your instance of Azure Stack.</span></span> <span data-ttu-id="bf511-131">S’il est introuvable, le certificat racine est récupéré.</span><span class="sxs-lookup"><span data-stu-id="bf511-131">If it is not found, the root certificate will be retrieved.</span></span>

5. <span data-ttu-id="bf511-132">Ouvrez une **nouvelle** console PowerShell avec élévation de privilèges et basculez vers le répertoire où vous avez extrait les fichiers.</span><span class="sxs-lookup"><span data-stu-id="bf511-132">Open a **new** elevated PowerShell console and change to the directory where you extracted the files.</span></span> <span data-ttu-id="bf511-133">Utilisez une nouvelle fenêtre pour éviter les problèmes qui peuvent se produire à cause des modules PowerShell incorrects déjà chargés sur le système.</span><span class="sxs-lookup"><span data-stu-id="bf511-133">Use a new window to avoid problems that may arise from incorrect PowerShell modules already loaded on the system.</span></span>

6. <span data-ttu-id="bf511-134">Si vous avez installé des versions des modules PowerShell AzureRm ou AzureStack autres que 1.2.9 ou 1.2.10, vous devrez les supprimer ou l’installation ne sera pas effectuée.</span><span class="sxs-lookup"><span data-stu-id="bf511-134">If you have installed any versions of the AzureRm or AzureStack PowerShell modules other than 1.2.9 or 1.2.10, you will be prompted to remove them or the install will not proceed.</span></span> <span data-ttu-id="bf511-135">Cela inclut les versions 1.3 ou ultérieures.</span><span class="sxs-lookup"><span data-stu-id="bf511-135">This includes versions 1.3 or greater.</span></span>

7. <span data-ttu-id="bf511-136">Exécutez DeployMySqlProvider.ps1.</span><span class="sxs-lookup"><span data-stu-id="bf511-136">Run DeployMySqlProvider.ps1.</span></span>

<span data-ttu-id="bf511-137">Ce script effectue les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="bf511-137">This script performs these steps:</span></span>

* <span data-ttu-id="bf511-138">Si nécessaire, téléchargement d’une version compatible d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bf511-138">If necessary, download a compatible version of Azure PowerShell.</span></span>
* <span data-ttu-id="bf511-139">Téléchargement du fichier binaire de connecteur MySQL (peut être fourni en mode hors connexion).</span><span class="sxs-lookup"><span data-stu-id="bf511-139">Download the MySQL connector binary (this can be provided offline).</span></span>
* <span data-ttu-id="bf511-140">Chargement du certificat et de tous les autres artefacts sur un compte de stockage Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="bf511-140">Upload the certificate and all other artifacts to an Azure Stack storage account.</span></span>
* <span data-ttu-id="bf511-141">Publication des packages de la galerie afin que vous puissiez déployer des bases de données MySQL par le biais de la galerie.</span><span class="sxs-lookup"><span data-stu-id="bf511-141">Publish gallery packages so that you can deploy MySQL databases through the gallery.</span></span>
* <span data-ttu-id="bf511-142">Déploiement d’une machine virtuelle qui héberge votre fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="bf511-142">Deploy a virtual machine (VM) that hosts your resource provider.</span></span>
* <span data-ttu-id="bf511-143">Inscription d’un enregistrement DNS local mappé à votre machine virtuelle de fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="bf511-143">Register a local DNS record that maps to your resource provider VM.</span></span>
* <span data-ttu-id="bf511-144">Inscription de votre fournisseur de ressources auprès de l’instance Azure Resource Manager locale.</span><span class="sxs-lookup"><span data-stu-id="bf511-144">Register your resource provider with the local Azure Resource Manager.</span></span>

<span data-ttu-id="bf511-145">Spécifiez au moins les paramètres obligatoires sur la ligne de commande ou, si vous exécutez sans paramètres, vous êtes invité à les entrer.</span><span class="sxs-lookup"><span data-stu-id="bf511-145">Either specify at least the required parameters on the command line, or, if you run without any parameters, you are prompted to enter them.</span></span> 

<span data-ttu-id="bf511-146">Voici un exemple que vous pouvez exécuter à partir de l’invite PowerShell (mais changez les points de terminaison du portail et les informations du compte si nécessaire) :</span><span class="sxs-lookup"><span data-stu-id="bf511-146">Here's an example you can run from the PowerShell prompt (but change the account information and portal endpoints as needed):</span></span>


```
# Install the AzureRM.Bootstrapper module
Install-Module -Name AzureRm.BootStrapper -Force

# Installs and imports the API Version Profile required by Azure Stack into the current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile
Install-Module -Name AzureStack -RequiredVersion 1.2.10 -Force

# Download the Azure Stack Tools from GitHub and set the environment
cd c:\
Invoke-Webrequest https://github.com/Azure/AzureStack-Tools/archive/master.zip -OutFile master.zip
Expand-Archive master.zip -DestinationPath . -Force

# This endpoint may be different for your installation
Import-Module C:\AzureStack-Tools-master\Connect\AzureStack.Connect.psm1
Add-AzureRmEnvironment -Name AzureStackAdmin -ArmEndpoint "https://adminmanagement.local.azurestack.external" 

# For AAD, use the following
$tenantID = Get-AzsDirectoryTenantID -AADTenantName "<your directory name>" -EnvironmentName AzureStackAdmin

# For ADFS, replace the previous line with
# $tenantID = Get-AzsDirectoryTenantID -ADFS -EnvironmentName AzureStackAdmin

$vmLocalAdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("mysqlrpadmin", $vmLocalAdminPass)

$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AdminPass)

# change this as appropriate
$PfxPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force

# Change directory to the folder where you extracted the installation files 
# and adjust the endpoints
<extracted file directory>\DeployMySQLProvider.ps1 -DirectoryTenantID $tenantID -AzCredential $AdminCreds -VMLocalCredential $vmLocalAdminCreds -ResourceGroupName "MySqlRG" -VmName "MySQLRP" -ArmEndpoint "https://adminmanagement.local.azurestack.external" -TenantArmEndpoint "https://management.local.azurestack.external" -DefaultSSLCertificatePassword $PfxPass -DependencyFilesLocalPath
 ```

### <a name="deploymysqlproviderps1-parameters"></a><span data-ttu-id="bf511-147">Paramètres de DeployMySqlProvider.ps1</span><span class="sxs-lookup"><span data-stu-id="bf511-147">DeployMySqlProvider.ps1 parameters</span></span>

<span data-ttu-id="bf511-148">Vous pouvez spécifier ces paramètres sur la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="bf511-148">You can specify these parameters in the command line.</span></span> <span data-ttu-id="bf511-149">Si vous ne le faites pas, ou si la validation des paramètres échoue, vous êtes invité à fournir les paramètres obligatoires.</span><span class="sxs-lookup"><span data-stu-id="bf511-149">If you do not, or any parameter validation fails, you are prompted to provide the required ones.</span></span>

| <span data-ttu-id="bf511-150">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="bf511-150">Parameter Name</span></span> | <span data-ttu-id="bf511-151">Description</span><span class="sxs-lookup"><span data-stu-id="bf511-151">Description</span></span> | <span data-ttu-id="bf511-152">Commentaire ou valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="bf511-152">Comment or Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bf511-153">**DirectoryTenantID**</span><span class="sxs-lookup"><span data-stu-id="bf511-153">**DirectoryTenantID**</span></span> | <span data-ttu-id="bf511-154">ID de répertoire AD FS ou Azure (guid)</span><span class="sxs-lookup"><span data-stu-id="bf511-154">The Azure or ADFS Directory ID (guid)</span></span> | <span data-ttu-id="bf511-155">_obligatoire_</span><span class="sxs-lookup"><span data-stu-id="bf511-155">_required_</span></span> |
| <span data-ttu-id="bf511-156">**ArmEndpoint**</span><span class="sxs-lookup"><span data-stu-id="bf511-156">**ArmEndpoint**</span></span> | <span data-ttu-id="bf511-157">Point de terminaison Azure Resource Manager d’administration Azure Stack</span><span class="sxs-lookup"><span data-stu-id="bf511-157">The Azure Stack Administrative Azure Resource Manager Endpoint</span></span> | <span data-ttu-id="bf511-158">_obligatoire_</span><span class="sxs-lookup"><span data-stu-id="bf511-158">_required_</span></span> |
| <span data-ttu-id="bf511-159">**TenantArmEndpoint**</span><span class="sxs-lookup"><span data-stu-id="bf511-159">**TenantArmEndpoint**</span></span> | <span data-ttu-id="bf511-160">Point de terminaison Azure Resource Manager de locataire Azure Stack</span><span class="sxs-lookup"><span data-stu-id="bf511-160">The Azure Stack Tenant Azure Resource Manager Endpoint</span></span> | <span data-ttu-id="bf511-161">_obligatoire_</span><span class="sxs-lookup"><span data-stu-id="bf511-161">_required_</span></span> |
| <span data-ttu-id="bf511-162">**AzCredential**</span><span class="sxs-lookup"><span data-stu-id="bf511-162">**AzCredential**</span></span> | <span data-ttu-id="bf511-163">Informations d’identification du compte d’administration de service Azure Stack (utilisez le même compte que celui utilisé pour le déploiement d’Azure Stack)</span><span class="sxs-lookup"><span data-stu-id="bf511-163">Azure Stack Service Admin account credential (use the same account as you used for deploying Azure Stack)</span></span> | <span data-ttu-id="bf511-164">_obligatoire_</span><span class="sxs-lookup"><span data-stu-id="bf511-164">_required_</span></span> |
| <span data-ttu-id="bf511-165">**VMLocalCredential**</span><span class="sxs-lookup"><span data-stu-id="bf511-165">**VMLocalCredential**</span></span> | <span data-ttu-id="bf511-166">Compte d’administrateur local de la machine virtuelle du fournisseur de ressources MySQL</span><span class="sxs-lookup"><span data-stu-id="bf511-166">The local administrator account of the MySQL resource provider VM</span></span> | <span data-ttu-id="bf511-167">_obligatoire_</span><span class="sxs-lookup"><span data-stu-id="bf511-167">_required_</span></span> |
| <span data-ttu-id="bf511-168">**ResourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="bf511-168">**ResourceGroupName**</span></span> | <span data-ttu-id="bf511-169">Groupe de ressources pour les éléments créés par ce script</span><span class="sxs-lookup"><span data-stu-id="bf511-169">Resource Group for the items created by this script</span></span> |  <span data-ttu-id="bf511-170">_obligatoire_</span><span class="sxs-lookup"><span data-stu-id="bf511-170">_required_</span></span> |
| <span data-ttu-id="bf511-171">**VmName**</span><span class="sxs-lookup"><span data-stu-id="bf511-171">**VmName**</span></span> | <span data-ttu-id="bf511-172">Nom de la machine virtuelle contenant le fournisseur de ressources</span><span class="sxs-lookup"><span data-stu-id="bf511-172">Name of the VM holding the resource provider</span></span> |  <span data-ttu-id="bf511-173">_obligatoire_</span><span class="sxs-lookup"><span data-stu-id="bf511-173">_required_</span></span> |
| <span data-ttu-id="bf511-174">**AcceptLicense**</span><span class="sxs-lookup"><span data-stu-id="bf511-174">**AcceptLicense**</span></span> | <span data-ttu-id="bf511-175">Ignore l’invite demandant d’accepter la licence GPL (http://www.gnu.org/licenses/old-licenses/gpl-2.0.html)</span><span class="sxs-lookup"><span data-stu-id="bf511-175">Skips the prompt to accept the GPL License  (http://www.gnu.org/licenses/old-licenses/gpl-2.0.html)</span></span> | |
| <span data-ttu-id="bf511-176">**DependencyFilesLocalPath**</span><span class="sxs-lookup"><span data-stu-id="bf511-176">**DependencyFilesLocalPath**</span></span> | <span data-ttu-id="bf511-177">Chemin vers un partage local contenant [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Downloads/Connector-Net/mysql-connector-net-6.9.9.msi).</span><span class="sxs-lookup"><span data-stu-id="bf511-177">Path to a local share containing [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Downloads/Connector-Net/mysql-connector-net-6.9.9.msi).</span></span> <span data-ttu-id="bf511-178">Si vous les fournissez, les fichiers de certificats doivent être placés dans ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="bf511-178">If you provide them, certificate files must be placed in this directory as well.</span></span> | <span data-ttu-id="bf511-179">_facultatif_</span><span class="sxs-lookup"><span data-stu-id="bf511-179">_optional_</span></span> |
| <span data-ttu-id="bf511-180">**DefaultSSLCertificatePassword**</span><span class="sxs-lookup"><span data-stu-id="bf511-180">**DefaultSSLCertificatePassword**</span></span> | <span data-ttu-id="bf511-181">Mot de passe pour le certificat .pfx.</span><span class="sxs-lookup"><span data-stu-id="bf511-181">The password for the .pfx certificate</span></span> | <span data-ttu-id="bf511-182">_obligatoire_</span><span class="sxs-lookup"><span data-stu-id="bf511-182">_required_</span></span> |
| <span data-ttu-id="bf511-183">**MaxRetryCount**</span><span class="sxs-lookup"><span data-stu-id="bf511-183">**MaxRetryCount**</span></span> | <span data-ttu-id="bf511-184">Chaque opération est retentée en cas d’échec</span><span class="sxs-lookup"><span data-stu-id="bf511-184">Each operation is retried if there is a failure</span></span> | <span data-ttu-id="bf511-185">2</span><span class="sxs-lookup"><span data-stu-id="bf511-185">2</span></span> |
| <span data-ttu-id="bf511-186">**RetryDuration**</span><span class="sxs-lookup"><span data-stu-id="bf511-186">**RetryDuration**</span></span> | <span data-ttu-id="bf511-187">Délai d’attente entre les tentatives, en secondes</span><span class="sxs-lookup"><span data-stu-id="bf511-187">Timeout between retries, in seconds</span></span> | <span data-ttu-id="bf511-188">120</span><span class="sxs-lookup"><span data-stu-id="bf511-188">120</span></span> |
| <span data-ttu-id="bf511-189">**Désinstaller**</span><span class="sxs-lookup"><span data-stu-id="bf511-189">**Uninstall**</span></span> | <span data-ttu-id="bf511-190">Supprimer le fournisseur de ressources</span><span class="sxs-lookup"><span data-stu-id="bf511-190">Remove the resource provider</span></span> | <span data-ttu-id="bf511-191">Non</span><span class="sxs-lookup"><span data-stu-id="bf511-191">No</span></span> |
| <span data-ttu-id="bf511-192">**DebugMode**</span><span class="sxs-lookup"><span data-stu-id="bf511-192">**DebugMode**</span></span> | <span data-ttu-id="bf511-193">Empêche le nettoyage automatique en cas d’échec.</span><span class="sxs-lookup"><span data-stu-id="bf511-193">Prevents automatic cleanup on failure</span></span> | <span data-ttu-id="bf511-194">Non</span><span class="sxs-lookup"><span data-stu-id="bf511-194">No</span></span> |


<span data-ttu-id="bf511-195">En fonction de la vitesse de téléchargement et des performances système, l’installation peut durer entre 20 minutes et plusieurs heures.</span><span class="sxs-lookup"><span data-stu-id="bf511-195">Depending on the system performance and download speeds, installation may take as little as 20 minutes or as long as several hours.</span></span> <span data-ttu-id="bf511-196">Vous devez actualiser le portail d’administration si le panneau MySQLAdapter n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="bf511-196">You must refresh the admin portal if the MySQLAdapter blade is not available.</span></span>

> [!NOTE]
> <span data-ttu-id="bf511-197">Si l’installation prend plus de 90 minutes, elle risque d’échouer et vous verrez un message d’erreur à l’écran et dans le fichier journal.</span><span class="sxs-lookup"><span data-stu-id="bf511-197">If the installation takes more than 90 minutes, it may fail and you will see a failure message on the screen and in the log file.</span></span> <span data-ttu-id="bf511-198">Une nouvelle tentative de déploiement est effectuée à partir de l’étape ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="bf511-198">The deployment is retried from the failing step.</span></span> <span data-ttu-id="bf511-199">Les systèmes qui ne répondent pas aux spécifications recommandées en matière de mémoire et de noyau risquent de ne pas pouvoir déployer le fournisseur de ressources MySQL.</span><span class="sxs-lookup"><span data-stu-id="bf511-199">Systems that do not meet the recommended memory and core specifications may not be able to deploy the MySQL RP.</span></span>


## <a name="provide-capacity-by-connecting-to-a-mysql-hosting-server"></a><span data-ttu-id="bf511-200">Fournir de la capacité en se connectant à un serveur d’hébergement MySQL</span><span class="sxs-lookup"><span data-stu-id="bf511-200">Provide capacity by connecting to a MySQL hosting server</span></span>

1. <span data-ttu-id="bf511-201">Connectez-vous au portail Azure Stack en tant qu’administrateur de service.</span><span class="sxs-lookup"><span data-stu-id="bf511-201">Sign in to the Azure Stack portal as a service admin.</span></span>

2. <span data-ttu-id="bf511-202">Cliquez sur **Fournisseurs de ressources** &gt; **MySQLAdapter** &gt; **Serveurs d’hébergement** &gt; **+ Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bf511-202">Click **Resource Providers** &gt; **MySQLAdapter** &gt; **Hosting Servers** &gt; **+Add**.</span></span>

    <span data-ttu-id="bf511-203">Dans le panneau **Serveurs d’hébergement MySQL**, vous pouvez connecter le fournisseur de ressources MySQL Server à des instances réelles de MySQL Server qui font office de backend du fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="bf511-203">The **MySQL Hosting Servers** blade is where you can connect the MySQL Server Resource Provider to actual instances of MySQL Server that serve as the resource provider’s backend.</span></span>

    ![Serveurs d’hébergement](./media/azure-stack-mysql-rp-deploy/mysql-add-hosting-server-2.png)

3. <span data-ttu-id="bf511-205">Remplissez le formulaire avec les détails de connexion de votre instance de MySQL Server.</span><span class="sxs-lookup"><span data-stu-id="bf511-205">Fill the form with the connection details of your MySQL Server instance.</span></span> <span data-ttu-id="bf511-206">Fournissez le nom de domaine complet (FQDN) ou une adresse IPv4 valide, et pas le nom court de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bf511-206">Provide the fully qualified domain name (FQDN) or a valid IPv4 address, and not the short VM name.</span></span> <span data-ttu-id="bf511-207">Cette installation ne fournit plus d’instance de MySQL par défaut.</span><span class="sxs-lookup"><span data-stu-id="bf511-207">This installation no longer provides a default MySQL instance.</span></span> <span data-ttu-id="bf511-208">La taille fournie aide le fournisseur de ressources à gérer la capacité de la base de données.</span><span class="sxs-lookup"><span data-stu-id="bf511-208">The size provided helps the resource provider manage the database capacity.</span></span> <span data-ttu-id="bf511-209">Elle doit être proche de la capacité physique du serveur de base de données.</span><span class="sxs-lookup"><span data-stu-id="bf511-209">It should be close to the physical capacity of the database server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bf511-210">Tant que l’instance MySQL est accessible par le locataire et l’administrateur Azure Resource Manager, elle peut être placée sous contrôle du fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="bf511-210">As long as the MySQL instance can be accessed by the tenant and admin Azure Resource Manager, it can be placed under control of the resource provider.</span></span> <span data-ttu-id="bf511-211">L’instance de MySQL __doit__ être allouée exclusivement au fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="bf511-211">The MySQL instance __must__ be allocated exclusively to the RP.</span></span>

4. <span data-ttu-id="bf511-212">À mesure que vous ajoutez des serveurs, vous devez les affecter à une référence (SKU) nouvelle ou existante pour pouvoir différencier les offres de service.</span><span class="sxs-lookup"><span data-stu-id="bf511-212">As you add servers, you must assign them to a new or existing SKU to allow differentiation of service offerings.</span></span> <span data-ttu-id="bf511-213">Par exemple, vous pouvez avoir une instance d’entreprise qui fournit la capacité de base de données et la sauvegarde automatique, réserver les serveurs hautes performances pour les différents services, et ainsi de suite. Le nom de la référence doit refléter les propriétés afin que les locataires puissent placer correctement leurs bases de données, et tous les serveurs d’hébergement d’une référence doivent avoir les mêmes fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="bf511-213">For example, you could have an enterprise instance providing database capacity and automatic backup, reserve high-performance servers for individual departments, etc. The SKU name should reflect the properties so that tenants can place their databases appropriately and all hosting servers in a SKU should have the same capabilities.</span></span>

    ![Créer une référence (SKU) MySQL](./media/azure-stack-mysql-rp-deploy/mysql-new-sku.png)


>[!NOTE]
<span data-ttu-id="bf511-215">Une heure entière peut être nécessaire avant que les références n’apparaissent dans le portail.</span><span class="sxs-lookup"><span data-stu-id="bf511-215">SKUs can take up to an hour to be visible in the portal.</span></span> <span data-ttu-id="bf511-216">Vous ne pouvez pas créer une base de données tant que la référence n’a pas été créée.</span><span class="sxs-lookup"><span data-stu-id="bf511-216">You cannot create a database until the SKU is created.</span></span>


## <a name="create-your-first-mysql-database-to-test-your-deployment"></a><span data-ttu-id="bf511-217">Créer votre première base de données MySQL pour tester votre déploiement</span><span class="sxs-lookup"><span data-stu-id="bf511-217">Create your first MySQL database to test your deployment</span></span>


1. <span data-ttu-id="bf511-218">Connectez-vous au portail Azure Stack en tant qu’administrateur de service.</span><span class="sxs-lookup"><span data-stu-id="bf511-218">Sign in to the Azure Stack portal as service admin.</span></span>

2. <span data-ttu-id="bf511-219">Cliquez sur le bouton **+ Nouveau** &gt; **Données + stockage** &gt; **Base de données MySQL (préversion)**.</span><span class="sxs-lookup"><span data-stu-id="bf511-219">Click the **+ New** button &gt; **Data + Storage** &gt; **MySQL Database (preview)**.</span></span>

3. <span data-ttu-id="bf511-220">Remplissez le formulaire avec les détails de la base de données.</span><span class="sxs-lookup"><span data-stu-id="bf511-220">Fill in the form with the database details.</span></span>

    ![Créer une base de données MySQL test](./media/azure-stack-mysql-rp-deploy/mysql-create-db.png)

4. <span data-ttu-id="bf511-222">Sélectionnez une référence (SKU).</span><span class="sxs-lookup"><span data-stu-id="bf511-222">Select a SKU.</span></span>

    ![Sélectionner une référence](./media/azure-stack-mysql-rp-deploy/mysql-select-a-sku.png)

5. <span data-ttu-id="bf511-224">Créez un paramètre de connexion.</span><span class="sxs-lookup"><span data-stu-id="bf511-224">Create a login setting.</span></span> <span data-ttu-id="bf511-225">Vous pouvez réutiliser un paramètre de connexion ou en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="bf511-225">The login setting can be reused or a new one created.</span></span> <span data-ttu-id="bf511-226">Ce paramètre contient le nom d’utilisateur et le mot de passe de la base de données.</span><span class="sxs-lookup"><span data-stu-id="bf511-226">This contains the user name and password for the database.</span></span>

    ![Créer une connexion de base de données](./media/azure-stack-mysql-rp-deploy/create-new-login.png)

    <span data-ttu-id="bf511-228">La chaîne de connexion inclut le nom réel du serveur de base de données.</span><span class="sxs-lookup"><span data-stu-id="bf511-228">The connections string includes the real database server name.</span></span> <span data-ttu-id="bf511-229">Copiez-le à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="bf511-229">Copy it from the portal.</span></span>

    ![Obtenir la chaîne de connexion pour la base de données MySQL](./media/azure-stack-mysql-rp-deploy/mysql-db-created.png)

> [!NOTE]
> <span data-ttu-id="bf511-231">La longueur des noms d’utilisateurs ne doit pas dépasser 32 caractères avec MySQL 5.7, ou 16 caractères dans les éditions antérieures.</span><span class="sxs-lookup"><span data-stu-id="bf511-231">The length of the user names cannot exceed 32 characters with MySQL 5.7 or 16 characters in earlier editions.</span></span> <span data-ttu-id="bf511-232">Il s’agit d’une limitation des implémentations de MySQL.</span><span class="sxs-lookup"><span data-stu-id="bf511-232">This is a limitation of the MySQL implementations.</span></span>


## <a name="add-capacity"></a><span data-ttu-id="bf511-233">Ajouter de la capacité</span><span class="sxs-lookup"><span data-stu-id="bf511-233">Add capacity</span></span>

<span data-ttu-id="bf511-234">Augmentez la capacité en ajoutant des serveurs MySQL dans le portail Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="bf511-234">Add capacity by adding additional MySQL servers in the Azure Stack portal.</span></span> <span data-ttu-id="bf511-235">Si vous souhaitez utiliser une autre instance de MySQL, cliquez sur **Fournisseurs de ressources** &gt; **MySQLAdapter** &gt; **Serveurs d’hébergement MySQL** &gt; **+Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bf511-235">If you wish to use another instance of MySQL, click **Resource Providers** &gt; **MySQLAdapter** &gt; **MySQL Hosting Servers** &gt; **+Add**.</span></span>


## <a name="making-mysql-databases-available-to-tenants"></a><span data-ttu-id="bf511-236">Mise à disposition des bases de données MySQL pour les locataires</span><span class="sxs-lookup"><span data-stu-id="bf511-236">Making MySQL databases available to tenants</span></span>
<span data-ttu-id="bf511-237">Créez des plans et des offres pour mettre les bases de données MySQL à disposition des locataires.</span><span class="sxs-lookup"><span data-stu-id="bf511-237">Create plans and offers to make MySQL databases available for tenants.</span></span> <span data-ttu-id="bf511-238">Ajoutez le service Microsoft.MySqlAdapter, ajoutez un quota, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="bf511-238">Add the Microsoft.MySqlAdapter service, add a quota, etc.</span></span>

![Créer des plans et des offres pour inclure des bases de données](./media/azure-stack-mysql-rp-deploy/mysql-new-plan.png)

## <a name="removing-the-mysql-adapter-resource-provider"></a><span data-ttu-id="bf511-240">Suppression du fournisseur de ressources de l’adaptateur MySQL</span><span class="sxs-lookup"><span data-stu-id="bf511-240">Removing the MySQL Adapter Resource Provider</span></span>

<span data-ttu-id="bf511-241">Pour supprimer le fournisseur de ressources, il est essentiel de supprimer d’abord toutes les dépendances.</span><span class="sxs-lookup"><span data-stu-id="bf511-241">To remove the resource provider, it is essential to first remove any dependencies.</span></span>

1. <span data-ttu-id="bf511-242">Vérifiez que vous avez le package de déploiement d’origine que vous avez téléchargé pour cette version du fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="bf511-242">Ensure you have the original deployment package that you downloaded for this version of the Resource Provider.</span></span>

2. <span data-ttu-id="bf511-243">Toutes les bases de données de locataire doivent être supprimées du fournisseur de ressources (cela ne supprime pas les données).</span><span class="sxs-lookup"><span data-stu-id="bf511-243">All tenant databases must be deleted from the resource provider (this will not delete the data).</span></span> <span data-ttu-id="bf511-244">Cette opération doit être effectuée par les locataires eux-mêmes.</span><span class="sxs-lookup"><span data-stu-id="bf511-244">This should be performed by the tenants themselves.</span></span>

3. <span data-ttu-id="bf511-245">Les locataires doivent annuler l’inscription à partir de l’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="bf511-245">Tenants must unregister from the namespace.</span></span>

4. <span data-ttu-id="bf511-246">L’administrateur doit supprimer les serveurs d’hébergement de l’adaptateur MySQL</span><span class="sxs-lookup"><span data-stu-id="bf511-246">Administrator must delete the hosting servers from the MySQL Adapter</span></span>

5. <span data-ttu-id="bf511-247">L’administrateur doit supprimer tous les plans qui référencent l’adaptateur MySQL.</span><span class="sxs-lookup"><span data-stu-id="bf511-247">Administrator must delete any plans that reference the MySQL Adapter.</span></span>

6. <span data-ttu-id="bf511-248">L’administrateur doit supprimer tous les quotas associés à l’adaptateur MySQL.</span><span class="sxs-lookup"><span data-stu-id="bf511-248">Administrator must delete any quotas associated to the MySQL Adapter.</span></span>

7. <span data-ttu-id="bf511-249">Réexécutez le script de déploiement avec le paramètre -Uninstall, les points de terminaison Azure Resource Manager, DirectoryTenantID et les informations d’identification du compte d’administrateur de service.</span><span class="sxs-lookup"><span data-stu-id="bf511-249">Rerun the deployment script with the -Uninstall parameter, Azure Resource Manager endpoints, DirectoryTenantID, and credentials for the service administrator account.</span></span>




## <a name="next-steps"></a><span data-ttu-id="bf511-250">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bf511-250">Next steps</span></span>


<span data-ttu-id="bf511-251">Essayez d’autres [services PaaS](azure-stack-tools-paas-services.md) comme le [fournisseur de ressources SQL Server](azure-stack-sql-resource-provider-deploy.md) et le [fournisseur de ressources App Services](azure-stack-app-service-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bf511-251">Try other [PaaS services](azure-stack-tools-paas-services.md) like the [SQL Server resource provider](azure-stack-sql-resource-provider-deploy.md) and the [App Services resource provider](azure-stack-app-service-overview.md).</span></span>
