---
title: "aaaUse MySQL de bases de données en tant que PaaS dans Azure pile | Documents Microsoft"
description: "Découvrez comment vous pouvez déployer hello fournisseur de ressources MySQL et fournissent des bases de données MySQL en tant que service sur la pile de Azure"
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
ms.openlocfilehash: 634e408eae9f3d8257a8610c60def0978ce333c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mysql-databases-on-microsoft-azure-stack"></a><span data-ttu-id="b77a7-103">Utiliser des bases de données MySQL sur Microsoft Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b77a7-103">Use MySQL databases on Microsoft Azure Stack</span></span>


<span data-ttu-id="b77a7-104">Vous pouvez déployer un fournisseur de ressources MySQL sur Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b77a7-104">You can deploy a MySQL resource provider on Azure Stack.</span></span> <span data-ttu-id="b77a7-105">Après avoir déployé le fournisseur de ressources hello, vous pouvez créer des bases de données via des modèles de déploiement Azure Resource Manager et des serveurs MySQL et fournir des bases de données MySQL en tant que service.</span><span class="sxs-lookup"><span data-stu-id="b77a7-105">After you deploy hello resource provider, you can create MySQL servers and databases through Azure Resource Manager deployment templates and provide MySQL databases as a service.</span></span> <span data-ttu-id="b77a7-106">Les bases de données MySQL, qui sont courantes sur les sites web, prennent en charge de nombreuses plateformes de site web.</span><span class="sxs-lookup"><span data-stu-id="b77a7-106">MySQL databases, which are common on web sites, support many website platforms.</span></span> <span data-ttu-id="b77a7-107">Par exemple, après avoir déployé le fournisseur de ressources hello, vous pouvez créer des sites Web WordPress à partir de la plateforme d’applications Web Azure hello comme un module complémentaire de service (PaaS) pour la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="b77a7-107">As an example, after you deploy hello resource provider, you can create WordPress websites from hello Azure Web Apps platform as a service (PaaS) add-on for Azure Stack.</span></span>

<span data-ttu-id="b77a7-108">le fournisseur de MySQL toodeploy hello sur un système qui n’a pas accès à internet, vous pouvez copier les fichiers hello [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Download/sConnector-Net/mysql-connector-net-6.9.9.msi) tooa local partager et fournir ce nom de partage lorsque vous y êtes invité (voir ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="b77a7-108">toodeploy hello MySQL provider on a system that does not have internet access, you can copy hello file [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Download/sConnector-Net/mysql-connector-net-6.9.9.msi) tooa local share and provide that share name when prompted (see below).</span></span> <span data-ttu-id="b77a7-109">Vous devez également installer les modules Azure et Azure pile PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="b77a7-109">You must also install hello Azure and Azure Stack PowerShell modules.</span></span>


## <a name="mysql-server-resource-provider-adapter-architecture"></a><span data-ttu-id="b77a7-110">Architecture de l’adaptateur de fournisseur de ressources MySQL Server</span><span class="sxs-lookup"><span data-stu-id="b77a7-110">MySQL Server Resource Provider Adapter architecture</span></span>

<span data-ttu-id="b77a7-111">fournisseur de ressources Hello est constitué de trois composants :</span><span class="sxs-lookup"><span data-stu-id="b77a7-111">hello resource provider is made up of three components:</span></span>

- <span data-ttu-id="b77a7-112">**adaptateur de fournisseur ressources Hello MySQL VM**, qui est un ordinateur virtuel de Windows exécutant les services de fournisseur hello.</span><span class="sxs-lookup"><span data-stu-id="b77a7-112">**hello MySQL resource provider adapter VM**, which is a Windows virtual machine running hello provider services.</span></span>
- <span data-ttu-id="b77a7-113">**fournisseur de ressources Hello lui-même**, qui traite les demandes d’approvisionnement et expose les ressources de base de données.</span><span class="sxs-lookup"><span data-stu-id="b77a7-113">**hello resource provider itself**, which processes provisioning requests and exposes database resources.</span></span>
- <span data-ttu-id="b77a7-114">**Les serveurs qui hébergent MySQL Server**, qui fournissent de la capacité pour les bases de données, appelés serveurs d’hébergement.</span><span class="sxs-lookup"><span data-stu-id="b77a7-114">**Servers that host MySQL Server**, which provide capacity for databases, called Hosting Servers.</span></span> 

<span data-ttu-id="b77a7-115">Cette version ne crée plus d’instance de MySQL.</span><span class="sxs-lookup"><span data-stu-id="b77a7-115">This release no longer creates a MySQL instance.</span></span> <span data-ttu-id="b77a7-116">Vous devez les créer ou fournir un accès tooexternal les instances de SQL.</span><span class="sxs-lookup"><span data-stu-id="b77a7-116">You must create them and/or provide access tooexternal SQL instances.</span></span> <span data-ttu-id="b77a7-117">Vous pouvez visiter hello [galerie de démarrage rapide Azure pile](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) pour un exemple de modèle que vous pouvez créer un serveur MySQL pour vous ou télécharger et déployer un serveur MySQL de hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b77a7-117">You can visit hello [Azure Stack Quickstart Gallery](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) for an example template that can create a MySQL server for you or download and deploy a MySQL Server from hello Marketplace.</span></span>

## <a name="deploy-hello-resource-provider"></a><span data-ttu-id="b77a7-118">Déployer le fournisseur de ressources hello</span><span class="sxs-lookup"><span data-stu-id="b77a7-118">Deploy hello resource provider</span></span>

1. <span data-ttu-id="b77a7-119">Si vous ne le n'avez pas déjà fait, inscrire votre kit de développement et télécharger hello Windows Server Datacenter 2016 - Eval image téléchargeable via la gestion du Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b77a7-119">If you have not already done so, register your development kit and download hello Windows Server 2016 Datacenter - Eval image downloadable through Marketplace Management.</span></span> <span data-ttu-id="b77a7-120">Vous pouvez également utiliser un script toocreate un [image de Windows Server 2016](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).</span><span class="sxs-lookup"><span data-stu-id="b77a7-120">You can also use a script toocreate a [Windows Server 2016 image](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).</span></span>

2. <span data-ttu-id="b77a7-121">[Télécharger le fichier de fichiers binaires du fournisseur de ressources hello MySQL](https://aka.ms/azurestackmysqlrp) et extrayez-le sur l’hôte de kit de développement hello.</span><span class="sxs-lookup"><span data-stu-id="b77a7-121">[Download hello MySQL resource provider binaries file](https://aka.ms/azurestackmysqlrp) and extract it on hello development kit host.</span></span>

3. <span data-ttu-id="b77a7-122">Connectez-vous à hôte de kit de développement toohello, puis extraire hello répertoire temporaire de tooa de fichiers de programme d’installation de MySQL RP.</span><span class="sxs-lookup"><span data-stu-id="b77a7-122">Sign in toohello development kit host, and extract hello MySQL RP installer file tooa temporary directory.</span></span>

4. <span data-ttu-id="b77a7-123">certificat racine de pile de Azure Hello est récupérée et un certificat auto-signé est créé dans le cadre de ce processus.</span><span class="sxs-lookup"><span data-stu-id="b77a7-123">hello Azure Stack root certificate is retrieved and a self-signed certificate is created as part of this process.</span></span> 

    <span data-ttu-id="b77a7-124">__Facultatif :__ si vous avez besoin de tooprovide votre propre, préparer les certificats hello et tooa répertoire local si vous le souhaitez toocustomize les certificats hello (script d’installation toohello passé).</span><span class="sxs-lookup"><span data-stu-id="b77a7-124">__Optional:__ If you need tooprovide your own, prepare hello certificates and copy tooa local directory if you wish toocustomize hello certificates (passed toohello installation script).</span></span> <span data-ttu-id="b77a7-125">Éléments de hello suivants sont nécessaires :</span><span class="sxs-lookup"><span data-stu-id="b77a7-125">You need hello following:</span></span>

    <span data-ttu-id="b77a7-126">a.</span><span class="sxs-lookup"><span data-stu-id="b77a7-126">a.</span></span> <span data-ttu-id="b77a7-127">Un certificat générique pour *.dbadapter.\<région\>.\<fqdn_externe\>.</span><span class="sxs-lookup"><span data-stu-id="b77a7-127">A wildcard certificate for *.dbadapter.\<region\>.\<external fqdn\>.</span></span> <span data-ttu-id="b77a7-128">Ce certificat doit être approuvé, tel qu’est émise par une autorité de certification (autrement dit, chaîne hello d’approbation doit exister sans exiger de certificats intermédiaires). (Un certificat de site unique utilisable avec nom VM explicite de hello, que vous fournissez lors de l’installation.)</span><span class="sxs-lookup"><span data-stu-id="b77a7-128">This certificate must be trusted, such as would be issued by a certificate authority (that is, hello chain of trust must exist without requiring intermediate certificates.) (A single site certificate can be used with hello explicit VM name you provide during install.)</span></span>

    <span data-ttu-id="b77a7-129">b.</span><span class="sxs-lookup"><span data-stu-id="b77a7-129">b.</span></span> <span data-ttu-id="b77a7-130">Hello certificat utilisé par hello Azure Resource Manager pour votre instance de la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="b77a7-130">hello root certificate used by hello Azure Resource Manager for your instance of Azure Stack.</span></span> <span data-ttu-id="b77a7-131">S’il n’est pas trouvé, certificat hello est récupérée.</span><span class="sxs-lookup"><span data-stu-id="b77a7-131">If it is not found, hello root certificate will be retrieved.</span></span>

5. <span data-ttu-id="b77a7-132">Ouvrir un **nouvelle** élevé PowerShell console et de modifier le répertoire toohello où vous avez extrait les fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="b77a7-132">Open a **new** elevated PowerShell console and change toohello directory where you extracted hello files.</span></span> <span data-ttu-id="b77a7-133">Utilisez une nouvelle fenêtre tooavoid les problèmes qui peuvent survenir à partir des modules PowerShell incorrects déjà chargés sur le système de hello.</span><span class="sxs-lookup"><span data-stu-id="b77a7-133">Use a new window tooavoid problems that may arise from incorrect PowerShell modules already loaded on hello system.</span></span>

6. <span data-ttu-id="b77a7-134">Si vous avez installé des versions des modules AzureStack PowerShell autres que 1.2.9 ou 1.2.10 hello Azure Resource Manager, vous serez invité à tooremove les ou hello installation ne sera pas effectuée.</span><span class="sxs-lookup"><span data-stu-id="b77a7-134">If you have installed any versions of hello AzureRm or AzureStack PowerShell modules other than 1.2.9 or 1.2.10, you will be prompted tooremove them or hello install will not proceed.</span></span> <span data-ttu-id="b77a7-135">Cela inclut les versions 1.3 ou ultérieures.</span><span class="sxs-lookup"><span data-stu-id="b77a7-135">This includes versions 1.3 or greater.</span></span>

7. <span data-ttu-id="b77a7-136">Exécutez DeployMySqlProvider.ps1.</span><span class="sxs-lookup"><span data-stu-id="b77a7-136">Run DeployMySqlProvider.ps1.</span></span>

<span data-ttu-id="b77a7-137">Ce script effectue les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="b77a7-137">This script performs these steps:</span></span>

* <span data-ttu-id="b77a7-138">Si nécessaire, téléchargement d’une version compatible d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b77a7-138">If necessary, download a compatible version of Azure PowerShell.</span></span>
* <span data-ttu-id="b77a7-139">Téléchargez hello connecteur MySQL binaire (Cela peut être fourni en mode hors connexion).</span><span class="sxs-lookup"><span data-stu-id="b77a7-139">Download hello MySQL connector binary (this can be provided offline).</span></span>
* <span data-ttu-id="b77a7-140">Télécharger le certificat de hello et tous les autres tooan artefacts compte de stockage Azure pile.</span><span class="sxs-lookup"><span data-stu-id="b77a7-140">Upload hello certificate and all other artifacts tooan Azure Stack storage account.</span></span>
* <span data-ttu-id="b77a7-141">Publier des packages de la galerie afin que vous pouvez déployer des bases de données MySQL via la galerie de hello.</span><span class="sxs-lookup"><span data-stu-id="b77a7-141">Publish gallery packages so that you can deploy MySQL databases through hello gallery.</span></span>
* <span data-ttu-id="b77a7-142">Déploiement d’une machine virtuelle qui héberge votre fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="b77a7-142">Deploy a virtual machine (VM) that hosts your resource provider.</span></span>
* <span data-ttu-id="b77a7-143">Inscrire un enregistrement DNS local qui mappe le fournisseur de ressources tooyour machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b77a7-143">Register a local DNS record that maps tooyour resource provider VM.</span></span>
* <span data-ttu-id="b77a7-144">Inscrire votre fournisseur de ressources par hello local Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b77a7-144">Register your resource provider with hello local Azure Resource Manager.</span></span>

<span data-ttu-id="b77a7-145">Spécifiez au moins hello paramètres requis sur la ligne de commande hello ou, si vous exécutez sans paramètres, vous êtes invité à tooenter les.</span><span class="sxs-lookup"><span data-stu-id="b77a7-145">Either specify at least hello required parameters on hello command line, or, if you run without any parameters, you are prompted tooenter them.</span></span> 

<span data-ttu-id="b77a7-146">Voici un exemple, vous pouvez exécuter à partir de hello PowerShell invite (mais modifier des points de terminaison hello compte des informations et du portail si nécessaire) :</span><span class="sxs-lookup"><span data-stu-id="b77a7-146">Here's an example you can run from hello PowerShell prompt (but change hello account information and portal endpoints as needed):</span></span>


```
# Install hello AzureRM.Bootstrapper module
Install-Module -Name AzureRm.BootStrapper -Force

# Installs and imports hello API Version Profile required by Azure Stack into hello current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile
Install-Module -Name AzureStack -RequiredVersion 1.2.10 -Force

# Download hello Azure Stack Tools from GitHub and set hello environment
cd c:\
Invoke-Webrequest https://github.com/Azure/AzureStack-Tools/archive/master.zip -OutFile master.zip
Expand-Archive master.zip -DestinationPath . -Force

# This endpoint may be different for your installation
Import-Module C:\AzureStack-Tools-master\Connect\AzureStack.Connect.psm1
Add-AzureRmEnvironment -Name AzureStackAdmin -ArmEndpoint "https://adminmanagement.local.azurestack.external" 

# For AAD, use hello following
$tenantID = Get-AzsDirectoryTenantID -AADTenantName "<your directory name>" -EnvironmentName AzureStackAdmin

# For ADFS, replace hello previous line with
# $tenantID = Get-AzsDirectoryTenantID -ADFS -EnvironmentName AzureStackAdmin

$vmLocalAdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("mysqlrpadmin", $vmLocalAdminPass)

$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AdminPass)

# change this as appropriate
$PfxPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force

# Change directory toohello folder where you extracted hello installation files 
# and adjust hello endpoints
<extracted file directory>\DeployMySQLProvider.ps1 -DirectoryTenantID $tenantID -AzCredential $AdminCreds -VMLocalCredential $vmLocalAdminCreds -ResourceGroupName "MySqlRG" -VmName "MySQLRP" -ArmEndpoint "https://adminmanagement.local.azurestack.external" -TenantArmEndpoint "https://management.local.azurestack.external" -DefaultSSLCertificatePassword $PfxPass -DependencyFilesLocalPath
 ```

### <a name="deploymysqlproviderps1-parameters"></a><span data-ttu-id="b77a7-147">Paramètres de DeployMySqlProvider.ps1</span><span class="sxs-lookup"><span data-stu-id="b77a7-147">DeployMySqlProvider.ps1 parameters</span></span>

<span data-ttu-id="b77a7-148">Vous pouvez spécifier ces paramètres dans la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="b77a7-148">You can specify these parameters in hello command line.</span></span> <span data-ttu-id="b77a7-149">Si vous n’effectuez pas ou n’importe quel paramètre validation échoue, vous êtes invité tooprovide hello requis ceux.</span><span class="sxs-lookup"><span data-stu-id="b77a7-149">If you do not, or any parameter validation fails, you are prompted tooprovide hello required ones.</span></span>

| <span data-ttu-id="b77a7-150">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="b77a7-150">Parameter Name</span></span> | <span data-ttu-id="b77a7-151">Description</span><span class="sxs-lookup"><span data-stu-id="b77a7-151">Description</span></span> | <span data-ttu-id="b77a7-152">Commentaire ou valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="b77a7-152">Comment or Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b77a7-153">**DirectoryTenantID**</span><span class="sxs-lookup"><span data-stu-id="b77a7-153">**DirectoryTenantID**</span></span> | <span data-ttu-id="b77a7-154">Bonjour Azure ou ID de répertoire AD FS (guid)</span><span class="sxs-lookup"><span data-stu-id="b77a7-154">hello Azure or ADFS Directory ID (guid)</span></span> | <span data-ttu-id="b77a7-155">_obligatoire_</span><span class="sxs-lookup"><span data-stu-id="b77a7-155">_required_</span></span> |
| <span data-ttu-id="b77a7-156">**ArmEndpoint**</span><span class="sxs-lookup"><span data-stu-id="b77a7-156">**ArmEndpoint**</span></span> | <span data-ttu-id="b77a7-157">Bonjour Azure pile d’administration Gestionnaire de ressources du point de terminaison Azure</span><span class="sxs-lookup"><span data-stu-id="b77a7-157">hello Azure Stack Administrative Azure Resource Manager Endpoint</span></span> | <span data-ttu-id="b77a7-158">_obligatoire_</span><span class="sxs-lookup"><span data-stu-id="b77a7-158">_required_</span></span> |
| <span data-ttu-id="b77a7-159">**TenantArmEndpoint**</span><span class="sxs-lookup"><span data-stu-id="b77a7-159">**TenantArmEndpoint**</span></span> | <span data-ttu-id="b77a7-160">Bonjour Azure pile client Gestionnaire de ressources du point de terminaison Azure</span><span class="sxs-lookup"><span data-stu-id="b77a7-160">hello Azure Stack Tenant Azure Resource Manager Endpoint</span></span> | <span data-ttu-id="b77a7-161">_obligatoire_</span><span class="sxs-lookup"><span data-stu-id="b77a7-161">_required_</span></span> |
| <span data-ttu-id="b77a7-162">**AzCredential**</span><span class="sxs-lookup"><span data-stu-id="b77a7-162">**AzCredential**</span></span> | <span data-ttu-id="b77a7-163">Références du compte administrateur de Service de pile Azure (hello utilisez même compte que vous avez utilisé pour le déploiement d’Azure pile)</span><span class="sxs-lookup"><span data-stu-id="b77a7-163">Azure Stack Service Admin account credential (use hello same account as you used for deploying Azure Stack)</span></span> | <span data-ttu-id="b77a7-164">_obligatoire_</span><span class="sxs-lookup"><span data-stu-id="b77a7-164">_required_</span></span> |
| <span data-ttu-id="b77a7-165">**VMLocalCredential**</span><span class="sxs-lookup"><span data-stu-id="b77a7-165">**VMLocalCredential**</span></span> | <span data-ttu-id="b77a7-166">compte d’administrateur local Hello de fournisseur de ressources MySQL hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="b77a7-166">hello local administrator account of hello MySQL resource provider VM</span></span> | <span data-ttu-id="b77a7-167">_obligatoire_</span><span class="sxs-lookup"><span data-stu-id="b77a7-167">_required_</span></span> |
| <span data-ttu-id="b77a7-168">**ResourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="b77a7-168">**ResourceGroupName**</span></span> | <span data-ttu-id="b77a7-169">Groupe de ressources pour les éléments hello créés par ce script</span><span class="sxs-lookup"><span data-stu-id="b77a7-169">Resource Group for hello items created by this script</span></span> |  <span data-ttu-id="b77a7-170">_obligatoire_</span><span class="sxs-lookup"><span data-stu-id="b77a7-170">_required_</span></span> |
| <span data-ttu-id="b77a7-171">**VmName**</span><span class="sxs-lookup"><span data-stu-id="b77a7-171">**VmName**</span></span> | <span data-ttu-id="b77a7-172">Nom de l’exploitation de machine virtuelle hello fournisseur de ressources hello</span><span class="sxs-lookup"><span data-stu-id="b77a7-172">Name of hello VM holding hello resource provider</span></span> |  <span data-ttu-id="b77a7-173">_obligatoire_</span><span class="sxs-lookup"><span data-stu-id="b77a7-173">_required_</span></span> |
| <span data-ttu-id="b77a7-174">**AcceptLicense**</span><span class="sxs-lookup"><span data-stu-id="b77a7-174">**AcceptLicense**</span></span> | <span data-ttu-id="b77a7-175">Ignore Bonjour tooaccept invite Bonjour le licence GPL (http://www.gnu.org/licenses/old-licenses/gpl-2.0.html)</span><span class="sxs-lookup"><span data-stu-id="b77a7-175">Skips hello prompt tooaccept hello GPL License  (http://www.gnu.org/licenses/old-licenses/gpl-2.0.html)</span></span> | |
| <span data-ttu-id="b77a7-176">**DependencyFilesLocalPath**</span><span class="sxs-lookup"><span data-stu-id="b77a7-176">**DependencyFilesLocalPath**</span></span> | <span data-ttu-id="b77a7-177">Chemin d’accès tooa partage local contenant [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Downloads/Connector-Net/mysql-connector-net-6.9.9.msi).</span><span class="sxs-lookup"><span data-stu-id="b77a7-177">Path tooa local share containing [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Downloads/Connector-Net/mysql-connector-net-6.9.9.msi).</span></span> <span data-ttu-id="b77a7-178">Si vous les fournissez, les fichiers de certificats doivent être placés dans ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="b77a7-178">If you provide them, certificate files must be placed in this directory as well.</span></span> | <span data-ttu-id="b77a7-179">_facultatif_</span><span class="sxs-lookup"><span data-stu-id="b77a7-179">_optional_</span></span> |
| <span data-ttu-id="b77a7-180">**DefaultSSLCertificatePassword**</span><span class="sxs-lookup"><span data-stu-id="b77a7-180">**DefaultSSLCertificatePassword**</span></span> | <span data-ttu-id="b77a7-181">mot de passe Hello certificat .pfx de hello</span><span class="sxs-lookup"><span data-stu-id="b77a7-181">hello password for hello .pfx certificate</span></span> | <span data-ttu-id="b77a7-182">_obligatoire_</span><span class="sxs-lookup"><span data-stu-id="b77a7-182">_required_</span></span> |
| <span data-ttu-id="b77a7-183">**MaxRetryCount**</span><span class="sxs-lookup"><span data-stu-id="b77a7-183">**MaxRetryCount**</span></span> | <span data-ttu-id="b77a7-184">Chaque opération est retentée en cas d’échec</span><span class="sxs-lookup"><span data-stu-id="b77a7-184">Each operation is retried if there is a failure</span></span> | <span data-ttu-id="b77a7-185">2</span><span class="sxs-lookup"><span data-stu-id="b77a7-185">2</span></span> |
| <span data-ttu-id="b77a7-186">**RetryDuration**</span><span class="sxs-lookup"><span data-stu-id="b77a7-186">**RetryDuration**</span></span> | <span data-ttu-id="b77a7-187">Délai d’attente entre les tentatives, en secondes</span><span class="sxs-lookup"><span data-stu-id="b77a7-187">Timeout between retries, in seconds</span></span> | <span data-ttu-id="b77a7-188">120</span><span class="sxs-lookup"><span data-stu-id="b77a7-188">120</span></span> |
| <span data-ttu-id="b77a7-189">**Désinstaller**</span><span class="sxs-lookup"><span data-stu-id="b77a7-189">**Uninstall**</span></span> | <span data-ttu-id="b77a7-190">Supprimer le fournisseur de ressources hello</span><span class="sxs-lookup"><span data-stu-id="b77a7-190">Remove hello resource provider</span></span> | <span data-ttu-id="b77a7-191">Non</span><span class="sxs-lookup"><span data-stu-id="b77a7-191">No</span></span> |
| <span data-ttu-id="b77a7-192">**DebugMode**</span><span class="sxs-lookup"><span data-stu-id="b77a7-192">**DebugMode**</span></span> | <span data-ttu-id="b77a7-193">Empêche le nettoyage automatique en cas d’échec.</span><span class="sxs-lookup"><span data-stu-id="b77a7-193">Prevents automatic cleanup on failure</span></span> | <span data-ttu-id="b77a7-194">Non</span><span class="sxs-lookup"><span data-stu-id="b77a7-194">No</span></span> |


<span data-ttu-id="b77a7-195">En fonction des vitesses téléchargement et les performances du système hello, installation peut prendre en l’espace de 20 minutes ou en tant que long en plusieurs heures.</span><span class="sxs-lookup"><span data-stu-id="b77a7-195">Depending on hello system performance and download speeds, installation may take as little as 20 minutes or as long as several hours.</span></span> <span data-ttu-id="b77a7-196">Vous devez actualiser le portail d’administration hello si le panneau de MySQLAdapter hello n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="b77a7-196">You must refresh hello admin portal if hello MySQLAdapter blade is not available.</span></span>

> [!NOTE]
> <span data-ttu-id="b77a7-197">Si l’installation de hello prend plus de 90 minutes, elle peut échouer et vous verrez un message d’erreur sur l’écran hello et dans le fichier journal de hello.</span><span class="sxs-lookup"><span data-stu-id="b77a7-197">If hello installation takes more than 90 minutes, it may fail and you will see a failure message on hello screen and in hello log file.</span></span> <span data-ttu-id="b77a7-198">déploiement de Hello est retentée à partir de hello échouent étape.</span><span class="sxs-lookup"><span data-stu-id="b77a7-198">hello deployment is retried from hello failing step.</span></span> <span data-ttu-id="b77a7-199">Les systèmes qui ne respectent pas hello mémoire recommandée et les spécifications principales peuvent ne pas être en mesure de toodeploy hello MySQL RP.</span><span class="sxs-lookup"><span data-stu-id="b77a7-199">Systems that do not meet hello recommended memory and core specifications may not be able toodeploy hello MySQL RP.</span></span>


## <a name="provide-capacity-by-connecting-tooa-mysql-hosting-server"></a><span data-ttu-id="b77a7-200">Fournir une capacité en vous connectant tooa serveur d’hébergement MySQL</span><span class="sxs-lookup"><span data-stu-id="b77a7-200">Provide capacity by connecting tooa MySQL hosting server</span></span>

1. <span data-ttu-id="b77a7-201">Connectez-vous toohello de portail de la pile de Azure en tant qu’un administrateur de service.</span><span class="sxs-lookup"><span data-stu-id="b77a7-201">Sign in toohello Azure Stack portal as a service admin.</span></span>

2. <span data-ttu-id="b77a7-202">Cliquez sur **Fournisseurs de ressources** &gt; **MySQLAdapter** &gt; **Serveurs d’hébergement** &gt; **+ Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b77a7-202">Click **Resource Providers** &gt; **MySQLAdapter** &gt; **Hosting Servers** &gt; **+Add**.</span></span>

    <span data-ttu-id="b77a7-203">Hello **serveurs d’hébergement MySQL** lame est où vous pouvez vous connecter hello fournisseur de ressources MySQL Server tooactual instances de MySQL Server qui servent de hello back-end du fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="b77a7-203">hello **MySQL Hosting Servers** blade is where you can connect hello MySQL Server Resource Provider tooactual instances of MySQL Server that serve as hello resource provider’s backend.</span></span>

    ![Serveurs d’hébergement](./media/azure-stack-mysql-rp-deploy/mysql-add-hosting-server-2.png)

3. <span data-ttu-id="b77a7-205">Remplir le formulaire de hello avec les détails de la connexion de votre instance de serveur MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="b77a7-205">Fill hello form with hello connection details of your MySQL Server instance.</span></span> <span data-ttu-id="b77a7-206">Fournir le nom de domaine complet hello (FQDN) ou une adresse IPv4 valide et pas hello VM nom court.</span><span class="sxs-lookup"><span data-stu-id="b77a7-206">Provide hello fully qualified domain name (FQDN) or a valid IPv4 address, and not hello short VM name.</span></span> <span data-ttu-id="b77a7-207">Cette installation ne fournit plus d’instance de MySQL par défaut.</span><span class="sxs-lookup"><span data-stu-id="b77a7-207">This installation no longer provides a default MySQL instance.</span></span> <span data-ttu-id="b77a7-208">Hello taille fournie permet de gérer la capacité de base de données hello fournisseur de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="b77a7-208">hello size provided helps hello resource provider manage hello database capacity.</span></span> <span data-ttu-id="b77a7-209">Il doit être toohello fermer la capacité physique du serveur de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="b77a7-209">It should be close toohello physical capacity of hello database server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b77a7-210">Tant qu’instance de MySQL hello est accessible par le locataire de hello et administrateur Azure Resource Manager, il peut être placé sous contrôle de fournisseur de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="b77a7-210">As long as hello MySQL instance can be accessed by hello tenant and admin Azure Resource Manager, it can be placed under control of hello resource provider.</span></span> <span data-ttu-id="b77a7-211">instance de MySQL Hello __doit__ être allouées exclusivement toohello RP.</span><span class="sxs-lookup"><span data-stu-id="b77a7-211">hello MySQL instance __must__ be allocated exclusively toohello RP.</span></span>

4. <span data-ttu-id="b77a7-212">Lorsque vous ajoutez des serveurs, vous devez les affecter tooa nouveau ou existante SKU tooallow différentiation entre des offres de service.</span><span class="sxs-lookup"><span data-stu-id="b77a7-212">As you add servers, you must assign them tooa new or existing SKU tooallow differentiation of service offerings.</span></span> <span data-ttu-id="b77a7-213">Par exemple, Impossible de dispose d’une instance de l’entreprise en fournissant la capacité de la base de données et la sauvegarde automatique, de réserver les serveurs hautes performances pour les services, nom de référence (SKU) etc. hello doit refléter les propriétés hello afin que les clients peuvent placer leurs bases de données en conséquence et tous les serveurs d’hébergement dans une référence (SKU) doivent avoir hello les mêmes fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="b77a7-213">For example, you could have an enterprise instance providing database capacity and automatic backup, reserve high-performance servers for individual departments, etc. hello SKU name should reflect hello properties so that tenants can place their databases appropriately and all hosting servers in a SKU should have hello same capabilities.</span></span>

    ![Créer une référence (SKU) MySQL](./media/azure-stack-mysql-rp-deploy/mysql-new-sku.png)


>[!NOTE]
<span data-ttu-id="b77a7-215">Références (SKU) peut prendre jusqu'à toobe d’heure tooan visible dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="b77a7-215">SKUs can take up tooan hour toobe visible in hello portal.</span></span> <span data-ttu-id="b77a7-216">Impossible de créer une base de données jusqu'à ce que hello que référence (SKU) est créé.</span><span class="sxs-lookup"><span data-stu-id="b77a7-216">You cannot create a database until hello SKU is created.</span></span>


## <a name="create-your-first-mysql-database-tootest-your-deployment"></a><span data-ttu-id="b77a7-217">Créer votre première tootest de base de données MySQL à votre déploiement</span><span class="sxs-lookup"><span data-stu-id="b77a7-217">Create your first MySQL database tootest your deployment</span></span>


1. <span data-ttu-id="b77a7-218">Se connecter toohello portail de la pile de Azure en tant qu’administrateur de service.</span><span class="sxs-lookup"><span data-stu-id="b77a7-218">Sign in toohello Azure Stack portal as service admin.</span></span>

2. <span data-ttu-id="b77a7-219">Cliquez sur hello **+ nouveau** bouton &gt; **données + stockage** &gt; **base de données MySQL (version préliminaire)**.</span><span class="sxs-lookup"><span data-stu-id="b77a7-219">Click hello **+ New** button &gt; **Data + Storage** &gt; **MySQL Database (preview)**.</span></span>

3. <span data-ttu-id="b77a7-220">Renseignez le formulaire hello avec les détails de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="b77a7-220">Fill in hello form with hello database details.</span></span>

    ![Créer une base de données MySQL test](./media/azure-stack-mysql-rp-deploy/mysql-create-db.png)

4. <span data-ttu-id="b77a7-222">Sélectionnez une référence (SKU).</span><span class="sxs-lookup"><span data-stu-id="b77a7-222">Select a SKU.</span></span>

    ![Sélectionner une référence](./media/azure-stack-mysql-rp-deploy/mysql-select-a-sku.png)

5. <span data-ttu-id="b77a7-224">Créez un paramètre de connexion.</span><span class="sxs-lookup"><span data-stu-id="b77a7-224">Create a login setting.</span></span> <span data-ttu-id="b77a7-225">paramètre de connexion Hello peut être réutilisé ou créer une nouvelle.</span><span class="sxs-lookup"><span data-stu-id="b77a7-225">hello login setting can be reused or a new one created.</span></span> <span data-ttu-id="b77a7-226">Nom d’utilisateur hello et le mot de passe pour la base de données hello contient.</span><span class="sxs-lookup"><span data-stu-id="b77a7-226">This contains hello user name and password for hello database.</span></span>

    ![Créer une connexion de base de données](./media/azure-stack-mysql-rp-deploy/create-new-login.png)

    <span data-ttu-id="b77a7-228">chaîne de connexion Hello inclut le nom de serveur de base de données réels hello.</span><span class="sxs-lookup"><span data-stu-id="b77a7-228">hello connections string includes hello real database server name.</span></span> <span data-ttu-id="b77a7-229">Copier à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="b77a7-229">Copy it from hello portal.</span></span>

    ![Obtenir la chaîne de connexion hello pour la base de données MySQL hello](./media/azure-stack-mysql-rp-deploy/mysql-db-created.png)

> [!NOTE]
> <span data-ttu-id="b77a7-231">Hello hello des noms d’utilisateur ne peut pas dépasser 32 caractères avec MySQL 5.7 ou 16 caractères dans les éditions antérieures.</span><span class="sxs-lookup"><span data-stu-id="b77a7-231">hello length of hello user names cannot exceed 32 characters with MySQL 5.7 or 16 characters in earlier editions.</span></span> <span data-ttu-id="b77a7-232">Il s’agit d’une limitation des implémentations de MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="b77a7-232">This is a limitation of hello MySQL implementations.</span></span>


## <a name="add-capacity"></a><span data-ttu-id="b77a7-233">Ajouter de la capacité</span><span class="sxs-lookup"><span data-stu-id="b77a7-233">Add capacity</span></span>

<span data-ttu-id="b77a7-234">Augmenter la capacité en ajoutant des serveurs MySQL dans le portail d’Azure pile hello.</span><span class="sxs-lookup"><span data-stu-id="b77a7-234">Add capacity by adding additional MySQL servers in hello Azure Stack portal.</span></span> <span data-ttu-id="b77a7-235">Si vous le souhaitez toouse une autre instance de MySQL, cliquez sur **fournisseurs de ressources** &gt; **MySQLAdapter** &gt; **serveurs d’hébergement MySQL** &gt; **+ Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b77a7-235">If you wish toouse another instance of MySQL, click **Resource Providers** &gt; **MySQLAdapter** &gt; **MySQL Hosting Servers** &gt; **+Add**.</span></span>


## <a name="making-mysql-databases-available-tootenants"></a><span data-ttu-id="b77a7-236">Rendre les bases de données MySQL tootenants disponibles</span><span class="sxs-lookup"><span data-stu-id="b77a7-236">Making MySQL databases available tootenants</span></span>
<span data-ttu-id="b77a7-237">Créer des plans et des offres toomake MySQL de bases de données disponibles pour les locataires.</span><span class="sxs-lookup"><span data-stu-id="b77a7-237">Create plans and offers toomake MySQL databases available for tenants.</span></span> <span data-ttu-id="b77a7-238">Ajouter un service de Microsoft.MySqlAdapter hello, ajouter un quota, un etc..</span><span class="sxs-lookup"><span data-stu-id="b77a7-238">Add hello Microsoft.MySqlAdapter service, add a quota, etc.</span></span>

![Créer des plans et des offres tooinclude bases de données](./media/azure-stack-mysql-rp-deploy/mysql-new-plan.png)

## <a name="removing-hello-mysql-adapter-resource-provider"></a><span data-ttu-id="b77a7-240">Suppression de hello fournisseur de ressources MySQL adaptateur</span><span class="sxs-lookup"><span data-stu-id="b77a7-240">Removing hello MySQL Adapter Resource Provider</span></span>

<span data-ttu-id="b77a7-241">fournisseur de ressources tooremove hello, il est essentiel toofirst supprimer toutes les dépendances.</span><span class="sxs-lookup"><span data-stu-id="b77a7-241">tooremove hello resource provider, it is essential toofirst remove any dependencies.</span></span>

1. <span data-ttu-id="b77a7-242">Assurez-vous de qu'avoir hello d’origine package de déploiement que vous avez téléchargé pour cette version du fournisseur de ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="b77a7-242">Ensure you have hello original deployment package that you downloaded for this version of hello Resource Provider.</span></span>

2. <span data-ttu-id="b77a7-243">Toutes les bases de données client doivent être supprimés à partir du fournisseur de ressources hello (cela ne supprimera pas les données de salutation).</span><span class="sxs-lookup"><span data-stu-id="b77a7-243">All tenant databases must be deleted from hello resource provider (this will not delete hello data).</span></span> <span data-ttu-id="b77a7-244">Doit être effectué par les locataires hello eux-mêmes.</span><span class="sxs-lookup"><span data-stu-id="b77a7-244">This should be performed by hello tenants themselves.</span></span>

3. <span data-ttu-id="b77a7-245">Les locataires doivent annuler l’inscription à partir de l’espace de noms hello.</span><span class="sxs-lookup"><span data-stu-id="b77a7-245">Tenants must unregister from hello namespace.</span></span>

4. <span data-ttu-id="b77a7-246">Administrateur doit supprimer hello hébergeant des serveurs à partir de hello MySQL adaptateur</span><span class="sxs-lookup"><span data-stu-id="b77a7-246">Administrator must delete hello hosting servers from hello MySQL Adapter</span></span>

5. <span data-ttu-id="b77a7-247">Administrateur doit supprimer tous les plans qui font référence à hello MySQL adaptateur.</span><span class="sxs-lookup"><span data-stu-id="b77a7-247">Administrator must delete any plans that reference hello MySQL Adapter.</span></span>

6. <span data-ttu-id="b77a7-248">Administrateur doit supprimer n’importe quel toohello associé de quotas MySQL adaptateur.</span><span class="sxs-lookup"><span data-stu-id="b77a7-248">Administrator must delete any quotas associated toohello MySQL Adapter.</span></span>

7. <span data-ttu-id="b77a7-249">Réexécutez le script de déploiement hello dans hello - désinstallation de paramètre, les points de terminaison Azure Resource Manager, les DirectoryTenantID et les informations d’identification pour le compte d’administrateur de service de hello.</span><span class="sxs-lookup"><span data-stu-id="b77a7-249">Rerun hello deployment script with hello -Uninstall parameter, Azure Resource Manager endpoints, DirectoryTenantID, and credentials for hello service administrator account.</span></span>




## <a name="next-steps"></a><span data-ttu-id="b77a7-250">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b77a7-250">Next steps</span></span>


<span data-ttu-id="b77a7-251">Essayez d’autres [services PaaS](azure-stack-tools-paas-services.md) comme hello [fournisseur de ressources SQL Server](azure-stack-sql-resource-provider-deploy.md) et hello [fournisseur de ressources des Services d’application](azure-stack-app-service-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b77a7-251">Try other [PaaS services](azure-stack-tools-paas-services.md) like hello [SQL Server resource provider](azure-stack-sql-resource-provider-deploy.md) and hello [App Services resource provider](azure-stack-app-service-overview.md).</span></span>
