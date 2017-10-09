---
title: "aaaUsing SQL des bases de données sur la pile de Azure | Documents Microsoft"
description: "Découvrez comment vous pouvez déployer des bases de données SQL en tant que service sur la pile d’Azure et adaptateur fournisseur de ressources hello étapes rapides toodeploy hello SQL Server"
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
ms.openlocfilehash: 01418ce7cd708ca8f9e302d6bcd2a43ad33df93f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-databases-on-microsoft-azure-stack"></a><span data-ttu-id="06534-103">Utiliser des bases de données SQL sur Microsoft Azure Stack</span><span class="sxs-lookup"><span data-stu-id="06534-103">Use SQL databases on Microsoft Azure Stack</span></span>


<span data-ttu-id="06534-104">Utilisez hello SQL Server resource fournisseur adaptateur tooexpose bases de données SQL en tant que service de pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="06534-104">Use hello SQL Server resource provider adapter tooexpose SQL databases as a service of Azure Stack.</span></span> <span data-ttu-id="06534-105">Une fois que vous installez le fournisseur de ressources hello et connectez tooone ou autres instances de SQL Server, vous et vos utilisateurs peuvent créer des bases de données pour les applications cloud en mode natif, les sites Web basés sur SQL et les charges de travail qui sont basés sur SQL sans avoir tooprovision une machine virtuelle machine (VM) qui héberge SQL Server chaque fois.</span><span class="sxs-lookup"><span data-stu-id="06534-105">After you install hello resource provider and connect it tooone or more SQL Server instances, you and your users can create databases for cloud-native apps, websites that are based on SQL, and workloads that are based on SQL without having tooprovision a virtual machine (VM) that hosts SQL Server each time.</span></span>

<span data-ttu-id="06534-106">fournisseur de ressources Hello ne prend pas en charge toutes les fonctionnalités de gestion de la base de données hello de [base de données SQL Azure](https://azure.microsoft.com/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="06534-106">hello resource provider does not support all hello database management capabilities of [Azure SQL Database](https://azure.microsoft.com/services/sql-database/).</span></span> <span data-ttu-id="06534-107">Par exemple, les pools de bases de données élastiques et performances de base de données tooscale hello capacité ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="06534-107">For example, elastic database pools and hello ability tooscale database performance aren't supported.</span></span> <span data-ttu-id="06534-108">Hello API n’est pas compatible avec la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="06534-108">hello API is not compatible with SQL DB.</span></span>


## <a name="sql-server-resource-provider-adapter-architecture"></a><span data-ttu-id="06534-109">Architecture de l’adaptateur de fournisseur de ressource SQL Server</span><span class="sxs-lookup"><span data-stu-id="06534-109">SQL Server Resource Provider Adapter architecture</span></span>
<span data-ttu-id="06534-110">fournisseur de ressources Hello n’est pas basé sur, ni offre toutes les fonctionnalités de gestion de la base de données hello de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="06534-110">hello resource provider is not based on, nor does it offer all hello database management capabilities of Azure SQL Database.</span></span> <span data-ttu-id="06534-111">Par exemple, les pools de bases de données élastiques et performances de base de données toodial hello capacité haut et bas automatiquement ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="06534-111">For example, elastic database pools and hello ability toodial database performance up and down automatically aren't available.</span></span> <span data-ttu-id="06534-112">Toutefois, hello ressource fournisseur prend en charge similaire créer, lire, mettre à jour et supprimer (CRUD) des opérations.</span><span class="sxs-lookup"><span data-stu-id="06534-112">However, hello resource provider does support similar create, read, update, and delete (CRUD) operations.</span></span>

<span data-ttu-id="06534-113">fournisseur de ressources Hello est constitué de trois composants :</span><span class="sxs-lookup"><span data-stu-id="06534-113">hello resource provider is made up of three components:</span></span>

- <span data-ttu-id="06534-114">**adaptateur de fournisseur Hello SQL ressource VM**, qui est un ordinateur virtuel de Windows exécutant les services de fournisseur hello.</span><span class="sxs-lookup"><span data-stu-id="06534-114">**hello SQL resource provider adapter VM**, which is a Windows virtual machine running hello provider services.</span></span>
- <span data-ttu-id="06534-115">**fournisseur de ressources Hello lui-même**, qui traite les demandes d’approvisionnement et expose les ressources de base de données.</span><span class="sxs-lookup"><span data-stu-id="06534-115">**hello resource provider itself**, which processes provisioning requests and exposes database resources.</span></span>
- <span data-ttu-id="06534-116">**Les serveurs qui hébergent SQL Server**, qui offrent de la capacité pour les bases de données, et qui sont appelés « serveurs d’hébergement ».</span><span class="sxs-lookup"><span data-stu-id="06534-116">**Servers that host SQL Server**, which provide capacity for databases, called Hosting Servers.</span></span> 

<span data-ttu-id="06534-117">Cette version ne crée plus d’instance SQL.</span><span class="sxs-lookup"><span data-stu-id="06534-117">This release no longer creates a SQL instance.</span></span> <span data-ttu-id="06534-118">Vous devez créer un (ou plusieurs) ou fournir un accès tooexternal les instances de SQL.</span><span class="sxs-lookup"><span data-stu-id="06534-118">You must create one (or more) and/or provide access tooexternal SQL instances.</span></span> <span data-ttu-id="06534-119">Il existe un nombre d’options de tooyou disponibles, y compris les modèles Bonjour [galerie de démarrage rapide Azure pile](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) et d’éléments du Marketplace.</span><span class="sxs-lookup"><span data-stu-id="06534-119">There are a number of options available tooyou including templates in hello [Azure Stack Quickstart Gallery](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) and Marketplace items.</span></span> 

>[!NOTE]
<span data-ttu-id="06534-120">Si vous avez téléchargé tous les éléments SQL Marketplace, assurez-vous que vous téléchargez également hello IaaS Extension de SQL ou ces ne déploiement pas.</span><span class="sxs-lookup"><span data-stu-id="06534-120">If you have downloaded any SQL Marketplace items, make sure you also download hello SQL IaaS Extension or these will not deploy.</span></span>


## <a name="deploy-hello-resource-provider"></a><span data-ttu-id="06534-121">Déployer le fournisseur de ressources hello</span><span class="sxs-lookup"><span data-stu-id="06534-121">Deploy hello resource provider</span></span>

1. <span data-ttu-id="06534-122">Si vous ne le n'avez pas déjà fait, inscrire votre kit de développement et de télécharger une image de Windows Server 2016 EVAL hello téléchargeable via la gestion du Marketplace.</span><span class="sxs-lookup"><span data-stu-id="06534-122">If you have not already done so, register your development kit and download hello Windows Server 2016 EVAL image downloadable through Marketplace Management.</span></span> <span data-ttu-id="06534-123">Vous pouvez également utiliser un script toocreate un [image de Windows Server 2016](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).</span><span class="sxs-lookup"><span data-stu-id="06534-123">You can also use a script toocreate a [Windows Server 2016 image](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).</span></span> <span data-ttu-id="06534-124">exécution de Hello .NET 3.5 n’est plus nécessaire.</span><span class="sxs-lookup"><span data-stu-id="06534-124">hello .NET 3.5 runtime is no longer required.</span></span>

2. <span data-ttu-id="06534-125">[Télécharger le fichier de fichiers binaires du fournisseur de ressources hello SQL](https://aka.ms/azurestacksqlrp) et extrayez-le sur l’hôte de kit de développement hello.</span><span class="sxs-lookup"><span data-stu-id="06534-125">[Download hello SQL resource provider binaries file](https://aka.ms/azurestacksqlrp) and extract it on hello development kit host.</span></span>

3. <span data-ttu-id="06534-126">Connectez-vous à hôte de kit de développement toohello et extraire hello répertoire temporaire de tooa de fichiers de programme d’installation de SQL RP.</span><span class="sxs-lookup"><span data-stu-id="06534-126">Sign in toohello development kit host and extract hello SQL RP installer file tooa temporary directory.</span></span>

4. <span data-ttu-id="06534-127">certificat racine de pile de Azure Hello est récupérée et un certificat auto-signé est créé dans le cadre de ce processus.</span><span class="sxs-lookup"><span data-stu-id="06534-127">hello Azure Stack root certificate is retrieved and a self-signed certificate is created as part of this process.</span></span> 

    <span data-ttu-id="06534-128">__Facultatif :__ si vous avez besoin de tooprovide votre propre, préparer les certificats hello et tooa répertoire local si vous le souhaitez toocustomize les certificats hello (script d’installation toohello passé).</span><span class="sxs-lookup"><span data-stu-id="06534-128">__Optional:__ If you need tooprovide your own, prepare hello certificates and copy tooa local directory if you wish toocustomize hello certificates (passed toohello installation script).</span></span> <span data-ttu-id="06534-129">Vous devez hello certificats suivants :</span><span class="sxs-lookup"><span data-stu-id="06534-129">You need hello following certificates:</span></span>

    <span data-ttu-id="06534-130">a.</span><span class="sxs-lookup"><span data-stu-id="06534-130">a.</span></span> <span data-ttu-id="06534-131">Un certificat générique pour *.dbadapter.\<région\>.\<fqdn_externe\>.</span><span class="sxs-lookup"><span data-stu-id="06534-131">A wildcard certificate for *.dbadapter.\<region\>.\<external fqdn\>.</span></span> <span data-ttu-id="06534-132">Ce certificat doit être approuvé, tel qu’est émise par une autorité de certification (autrement dit, chaîne hello d’approbation doit exister sans exiger de certificats intermédiaires). (Un certificat de site unique utilisable avec nom VM explicite de hello, que vous fournissez lors de l’installation.)</span><span class="sxs-lookup"><span data-stu-id="06534-132">This certificate must be trusted, such as would be issued by a certificate authority (that is, hello chain of trust must exist without requiring intermediate certificates.) (A single site certificate can be used with hello explicit VM name you provide during install.)</span></span>

    <span data-ttu-id="06534-133">b.</span><span class="sxs-lookup"><span data-stu-id="06534-133">b.</span></span> <span data-ttu-id="06534-134">Hello certificat utilisé par hello Azure Resource Manager pour votre instance de la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="06534-134">hello root certificate used by hello Azure Resource Manager for your instance of Azure Stack.</span></span> <span data-ttu-id="06534-135">S’il n’est pas trouvé, certificat hello est récupérée.</span><span class="sxs-lookup"><span data-stu-id="06534-135">If it is not found, hello root certificate will be retrieved.</span></span>


5. <span data-ttu-id="06534-136">Ouvrir un **nouvelle** élevé PowerShell console et de modifier le répertoire toohello où vous avez extrait les fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="06534-136">Open a **new** elevated PowerShell console and change toohello directory where you extracted hello files.</span></span> <span data-ttu-id="06534-137">Utilisez une nouvelle fenêtre tooavoid les problèmes qui peuvent survenir à partir des modules PowerShell incorrects déjà chargés sur le système de hello.</span><span class="sxs-lookup"><span data-stu-id="06534-137">Use a new window tooavoid problems that may arise from incorrect PowerShell modules already loaded on hello system.</span></span>

6. <span data-ttu-id="06534-138">Si vous avez installé des versions des modules AzureStack PowerShell autres que 1.2.9 ou 1.2.10 hello Azure Resource Manager, vous serez invité à tooremove les ou hello installation ne sera pas effectuée.</span><span class="sxs-lookup"><span data-stu-id="06534-138">If you have installed any versions of hello AzureRm or AzureStack PowerShell modules other than 1.2.9 or 1.2.10, you will be prompted tooremove them or hello install will not proceed.</span></span> <span data-ttu-id="06534-139">Cela inclut les versions 1.3 ou ultérieures.</span><span class="sxs-lookup"><span data-stu-id="06534-139">This includes versions 1.3 or greater.</span></span>

7. <span data-ttu-id="06534-140">Exécutez hello DeploySqlProvider.ps1 script avec des paramètres de hello répertoriée ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="06534-140">Run hello DeploySqlProvider.ps1 script with hello parameters listed below.</span></span>

<span data-ttu-id="06534-141">script de Hello procède comme suit :</span><span class="sxs-lookup"><span data-stu-id="06534-141">hello script performs these steps:</span></span>

* <span data-ttu-id="06534-142">Si nécessaire, téléchargement d’une version compatible d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06534-142">If necessary, download a compatible version of Azure PowerShell.</span></span>
* <span data-ttu-id="06534-143">Télécharger les certificats hello et autres comptes de stockage tooa artefacts sur votre pile Azure.</span><span class="sxs-lookup"><span data-stu-id="06534-143">Upload hello certificates and other artifacts tooa storage account on your Azure Stack.</span></span>
* <span data-ttu-id="06534-144">Publier des packages de la galerie afin que vous pouvez déployer des bases de données SQL via la galerie de hello.</span><span class="sxs-lookup"><span data-stu-id="06534-144">Publish gallery packages so that you can deploy SQL databases through hello gallery.</span></span>
* <span data-ttu-id="06534-145">Déployer un ordinateur virtuel à l’aide d’image hello Windows Server 2016 créé à l’étape 1 et installer le fournisseur de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="06534-145">Deploy a VM using hello Windows Server 2016 image created in step 1 and install hello resource provider.</span></span>
* <span data-ttu-id="06534-146">Inscrire un enregistrement DNS local qui mappe le fournisseur de ressources tooyour machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="06534-146">Register a local DNS record that maps tooyour resource provider VM.</span></span>
* <span data-ttu-id="06534-147">Inscrire votre fournisseur de ressources par hello local Azure Resource Manager (client et administrateur).</span><span class="sxs-lookup"><span data-stu-id="06534-147">Register your resource provider with hello local Azure Resource Manager (Tenant and Admin).</span></span>

> [!NOTE]
> <span data-ttu-id="06534-148">Si l’installation de hello prend plus de 90 minutes, il risque d’échouer et vous voyez un message d’erreur sur l’écran hello et dans le fichier journal de hello, mais déploiement de hello est retentée à partir de hello échouent étape.</span><span class="sxs-lookup"><span data-stu-id="06534-148">If hello installation takes more than 90 minutes, it may fail and you see a failure message on hello screen and in hello log file, but hello deployment is retried from hello failing step.</span></span> <span data-ttu-id="06534-149">Les systèmes qui ne respectent pas hello mémoire recommandée et les spécifications principales peuvent ne pas être en mesure de toodeploy hello SQL RP.</span><span class="sxs-lookup"><span data-stu-id="06534-149">Systems that do not meet hello recommended memory and core specifications may not be able toodeploy hello SQL RP.</span></span>
>

<span data-ttu-id="06534-150">Voici un exemple, vous pouvez exécuter à partir de hello PowerShell invite (mais modifier des points de terminaison hello compte des informations et du portail si nécessaire) :</span><span class="sxs-lookup"><span data-stu-id="06534-150">Here's an example you can run from hello PowerShell prompt (but change hello account information and portal endpoints as needed):</span></span>

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
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("sqlrpadmin", $vmLocalAdminPass)

$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AdminPass)

# change this as appropriate
$PfxPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force

# Change directory toohello folder where you extracted hello installation files 
# and adjust hello endpoints
<extracted file directory>\DeploySQLProvider.ps1 -DirectoryTenantID $tenantID -AzCredential $AdminCreds -VMLocalCredential $vmLocalAdminCreds -ResourceGroupName "SqlRPRG" -VmName "SqlVM" -ArmEndpoint "https://adminmanagement.local.azurestack.external" -TenantArmEndpoint "https://management.local.azurestack.external" -DefaultSSLCertificatePassword $PfxPass
 ```

### <a name="deploysqlproviderps1-parameters"></a><span data-ttu-id="06534-151">Paramètres de DeploySqlProvider.ps1</span><span class="sxs-lookup"><span data-stu-id="06534-151">DeploySqlProvider.ps1 parameters</span></span>
<span data-ttu-id="06534-152">Vous pouvez spécifier ces paramètres dans la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="06534-152">You can specify these parameters in hello command line.</span></span> <span data-ttu-id="06534-153">Si vous n’effectuez pas ou n’importe quel paramètre validation échoue, vous êtes invité tooprovide hello requis ceux.</span><span class="sxs-lookup"><span data-stu-id="06534-153">If you do not, or any parameter validation fails, you are prompted tooprovide hello required ones.</span></span>

| <span data-ttu-id="06534-154">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="06534-154">Parameter Name</span></span> | <span data-ttu-id="06534-155">Description</span><span class="sxs-lookup"><span data-stu-id="06534-155">Description</span></span> | <span data-ttu-id="06534-156">Commentaire ou valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="06534-156">Comment or Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="06534-157">**DirectoryTenantID**</span><span class="sxs-lookup"><span data-stu-id="06534-157">**DirectoryTenantID**</span></span> | <span data-ttu-id="06534-158">Bonjour Azure ou ID de répertoire AD FS (guid).</span><span class="sxs-lookup"><span data-stu-id="06534-158">hello Azure or ADFS Directory ID (guid).</span></span> | <span data-ttu-id="06534-159">_obligatoire_</span><span class="sxs-lookup"><span data-stu-id="06534-159">_required_</span></span> |
| <span data-ttu-id="06534-160">**AzCredential**</span><span class="sxs-lookup"><span data-stu-id="06534-160">**AzCredential**</span></span> | <span data-ttu-id="06534-161">Fournir des informations d’identification de hello pour hello compte d’administrateur de Service de pile Azure.</span><span class="sxs-lookup"><span data-stu-id="06534-161">Provide hello credentials for hello Azure Stack Service Admin account.</span></span> <span data-ttu-id="06534-162">Vous devez utiliser hello même les informations d’identification que vous avez utilisé pour le déploiement d’Azure pile).</span><span class="sxs-lookup"><span data-stu-id="06534-162">You must use hello same credentials as you used for deploying Azure Stack).</span></span> | <span data-ttu-id="06534-163">_obligatoire_</span><span class="sxs-lookup"><span data-stu-id="06534-163">_required_</span></span> |
| <span data-ttu-id="06534-164">**VMLocalCredential**</span><span class="sxs-lookup"><span data-stu-id="06534-164">**VMLocalCredential**</span></span> | <span data-ttu-id="06534-165">Définir les informations d’identification de hello pour le compte d’administrateur local hello de fournisseur de ressources SQL hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="06534-165">Define hello credentials for hello local administrator account of hello SQL resource provider VM.</span></span> <span data-ttu-id="06534-166">Ce mot de passe est également utilisé pour hello SQL **sa** compte.</span><span class="sxs-lookup"><span data-stu-id="06534-166">This password is also used for hello SQL **sa** account.</span></span> | <span data-ttu-id="06534-167">_obligatoire_</span><span class="sxs-lookup"><span data-stu-id="06534-167">_required_</span></span> |
| <span data-ttu-id="06534-168">**ResourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="06534-168">**ResourceGroupName**</span></span> | <span data-ttu-id="06534-169">Définissez un nom pour un groupe de ressources dans lequel les éléments créés par ce script seront stockés.</span><span class="sxs-lookup"><span data-stu-id="06534-169">Define a name for a Resource Group in which items created by this script will be stored.</span></span> <span data-ttu-id="06534-170">Par exemple, *SqlRPRG*.</span><span class="sxs-lookup"><span data-stu-id="06534-170">For example, *SqlRPRG*.</span></span> |  <span data-ttu-id="06534-171">_obligatoire_</span><span class="sxs-lookup"><span data-stu-id="06534-171">_required_</span></span> |
| <span data-ttu-id="06534-172">**VmName**</span><span class="sxs-lookup"><span data-stu-id="06534-172">**VmName**</span></span> | <span data-ttu-id="06534-173">Définir le nom hello de machine virtuelle de hello sur le fournisseur de ressources tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="06534-173">Define hello name of hello virtual machine on which tooinstall hello resource provider.</span></span> <span data-ttu-id="06534-174">Par exemple, *SqlVM*.</span><span class="sxs-lookup"><span data-stu-id="06534-174">For example, *SqlVM*.</span></span> |  <span data-ttu-id="06534-175">_obligatoire_</span><span class="sxs-lookup"><span data-stu-id="06534-175">_required_</span></span> |
| <span data-ttu-id="06534-176">**DependencyFilesLocalPath**</span><span class="sxs-lookup"><span data-stu-id="06534-176">**DependencyFilesLocalPath**</span></span> | <span data-ttu-id="06534-177">Vos fichiers de certificats doivent également être placés dans ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="06534-177">Your certificate files must be placed in this directory as well.</span></span> | <span data-ttu-id="06534-178">_facultatif_</span><span class="sxs-lookup"><span data-stu-id="06534-178">_optional_</span></span> |
| <span data-ttu-id="06534-179">**DefaultSSLCertificatePassword**</span><span class="sxs-lookup"><span data-stu-id="06534-179">**DefaultSSLCertificatePassword**</span></span> | <span data-ttu-id="06534-180">mot de passe Hello certificat .pfx de hello</span><span class="sxs-lookup"><span data-stu-id="06534-180">hello password for hello .pfx certificate</span></span> | <span data-ttu-id="06534-181">_obligatoire_</span><span class="sxs-lookup"><span data-stu-id="06534-181">_required_</span></span> |
| <span data-ttu-id="06534-182">**MaxRetryCount**</span><span class="sxs-lookup"><span data-stu-id="06534-182">**MaxRetryCount**</span></span> | <span data-ttu-id="06534-183">Définir le nombre de fois où vous voulez que tooretry chaque opération s’il existe un échec.</span><span class="sxs-lookup"><span data-stu-id="06534-183">Define how many times you want tooretry each operation if there is a failure.</span></span>| <span data-ttu-id="06534-184">2</span><span class="sxs-lookup"><span data-stu-id="06534-184">2</span></span> |
| <span data-ttu-id="06534-185">**RetryDuration**</span><span class="sxs-lookup"><span data-stu-id="06534-185">**RetryDuration**</span></span> | <span data-ttu-id="06534-186">Définir le délai d’attente hello entre les nouvelles tentatives, en secondes.</span><span class="sxs-lookup"><span data-stu-id="06534-186">Define hello timeout between retries, in seconds.</span></span> | <span data-ttu-id="06534-187">120</span><span class="sxs-lookup"><span data-stu-id="06534-187">120</span></span> |
| <span data-ttu-id="06534-188">**Désinstaller**</span><span class="sxs-lookup"><span data-stu-id="06534-188">**Uninstall**</span></span> | <span data-ttu-id="06534-189">Supprimer le fournisseur de ressources hello et toutes les ressources associées (voir les remarques ci-dessous)</span><span class="sxs-lookup"><span data-stu-id="06534-189">Remove hello resource provider and all associated resources (see notes below)</span></span> | <span data-ttu-id="06534-190">Non</span><span class="sxs-lookup"><span data-stu-id="06534-190">No</span></span> |
| <span data-ttu-id="06534-191">**DebugMode**</span><span class="sxs-lookup"><span data-stu-id="06534-191">**DebugMode**</span></span> | <span data-ttu-id="06534-192">Empêche le nettoyage automatique en cas d’échec.</span><span class="sxs-lookup"><span data-stu-id="06534-192">Prevents automatic cleanup on failure</span></span> | <span data-ttu-id="06534-193">Non</span><span class="sxs-lookup"><span data-stu-id="06534-193">No</span></span> |


## <a name="verify-hello-deployment-using-hello-azure-stack-portal"></a><span data-ttu-id="06534-194">Vérifier le déploiement hello à l’aide de hello Azure pile portail</span><span class="sxs-lookup"><span data-stu-id="06534-194">Verify hello deployment using hello Azure Stack Portal</span></span>

> [!NOTE]
>  <span data-ttu-id="06534-195">Après l’achèvement du script d’installation hello, vous devez le panneau admin hello toorefresh hello toosee portail.</span><span class="sxs-lookup"><span data-stu-id="06534-195">After hello installation script completes, you will need toorefresh hello portal toosee hello admin blade.</span></span>


1. <span data-ttu-id="06534-196">Sur le bureau de machine virtuelle de Console hello, cliquez sur **Microsoft Azure pile Portal** et connectez-vous au portail toohello en tant qu’administrateur de service hello.</span><span class="sxs-lookup"><span data-stu-id="06534-196">On hello Console VM desktop, click **Microsoft Azure Stack Portal** and sign in toohello portal as hello service administrator.</span></span>

2. <span data-ttu-id="06534-197">Vérifiez que le déploiement de hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="06534-197">Verify that hello deployment succeeded.</span></span> <span data-ttu-id="06534-198">Cliquez sur **groupes de ressources** &gt; cliquez sur le groupe de ressources hello utilisé et assurez-vous que cette partie d’essentials hello de lectures de panneau (moitié supérieure) hello  **_date_ (réussite)**.</span><span class="sxs-lookup"><span data-stu-id="06534-198">Click **Resource Groups** &gt; click hello resource group you used and then make sure that hello essentials part of hello blade (upper half) reads **_date_ (Succeeded)**.</span></span>

      ![Vérifier le déploiement de hello SQL RP](./media/azure-stack-sql-rp-deploy/sqlrp-verify.png)


## <a name="provide-capacity-by-connecting-tooa-hosting-sql-server"></a><span data-ttu-id="06534-200">Fournir une capacité en vous connectant tooa hébergeant SQL server</span><span class="sxs-lookup"><span data-stu-id="06534-200">Provide capacity by connecting tooa hosting SQL server</span></span>

1. <span data-ttu-id="06534-201">Connectez-vous toohello de portail d’administration Azure pile en tant qu’un administrateur de service</span><span class="sxs-lookup"><span data-stu-id="06534-201">Sign in toohello Azure Stack admin portal as a service admin</span></span>

2. <span data-ttu-id="06534-202">Créez une machine virtuelle SQL, sauf si vous en avez déjà une disponible.</span><span class="sxs-lookup"><span data-stu-id="06534-202">Create a SQL virtual machine, unless you have one already available.</span></span> <span data-ttu-id="06534-203">La Gestion de la Place de marché offre certaines options pour le déploiement de machines virtuelles SQL.</span><span class="sxs-lookup"><span data-stu-id="06534-203">Marketplace Management offers some options for deploying SQL VMs.</span></span>

3. <span data-ttu-id="06534-204">Cliquez sur **Fournisseurs de ressources** &gt; **SQLAdapter** &gt; **Serveurs d’hébergement** &gt; **+Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="06534-204">Click **Resource Providers** &gt; **SQLAdapter** &gt; **Hosting Servers** &gt; **+Add**.</span></span>

    <span data-ttu-id="06534-205">Hello **serveurs d’hébergement SQL** lame est où vous pouvez vous connecter hello fournisseur de ressources SQL Server tooactual instances de SQL Server qui servent de hello back-end du fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="06534-205">hello **SQL Hosting Servers** blade is where you can connect hello SQL Server Resource Provider tooactual instances of SQL Server that serve as hello resource provider’s backend.</span></span>

    ![Serveurs d’hébergement](./media/azure-stack-sql-rp-deploy/sqlrp-hostingserver.PNG)

4. <span data-ttu-id="06534-207">Remplir le formulaire de hello avec les détails de la connexion hello de votre instance de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="06534-207">Fill hello form with hello connection details of your SQL Server instance.</span></span>

    ![Nouveau serveur d’hébergement](./media/azure-stack-sql-rp-deploy/sqlrp-newhostingserver.PNG)

    > [!NOTE]
    > <span data-ttu-id="06534-209">Tant que l’instance SQL hello est accessible par le locataire de hello et administrateur Azure Resource Manager, il peut être placé sous contrôle de fournisseur de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="06534-209">As long as hello SQL instance can be accessed by hello tenant and admin Azure Resource Manager, it can be placed under control of hello resource provider.</span></span> <span data-ttu-id="06534-210">l’instance SQL Hello __doit__ être allouées exclusivement toohello RP.</span><span class="sxs-lookup"><span data-stu-id="06534-210">hello SQL instance __must__ be allocated exclusively toohello RP.</span></span>

5. <span data-ttu-id="06534-211">Lorsque vous ajoutez des serveurs, vous devez les affecter tooa nouveau ou existants SKU toodifferentiate offres de service.</span><span class="sxs-lookup"><span data-stu-id="06534-211">As you add servers, you must assign them tooa new or existing SKU toodifferentiate service offerings.</span></span> <span data-ttu-id="06534-212">Par exemple, vous peut avoir qu’une instance de SQL Enterprise en fournissant la capacité de la base de données et la sauvegarde automatique, réserver serveurs hautes performances pour les services, nom de référence (SKU) etc. hello doit refléter les propriétés hello afin que les clients peuvent placer leurs bases de données en conséquence et tous les serveurs d’hébergement dans une référence (SKU) doivent avoir hello les mêmes fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="06534-212">For example, you could have a SQL Enterprise instance providing database capacity and automatic backup, reserve high-performance servers for individual departments, etc. hello SKU name should reflect hello properties so that tenants can place their databases appropriately and all hosting servers in a SKU should have hello same capabilities.</span></span>

    <span data-ttu-id="06534-213">Exemple :</span><span class="sxs-lookup"><span data-stu-id="06534-213">An example:</span></span>

    ![Références (SKU)](./media/azure-stack-sql-rp-deploy/sqlrp-newsku.png)

>[!NOTE]
<span data-ttu-id="06534-215">Références (SKU) peut prendre jusqu'à toobe d’heure tooan visible dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="06534-215">SKUs can take up tooan hour toobe visible in hello portal.</span></span> <span data-ttu-id="06534-216">Impossible de créer une base de données jusqu'à ce que hello que référence (SKU) est créé.</span><span class="sxs-lookup"><span data-stu-id="06534-216">You cannot create a database until hello SKU is created.</span></span>


## <a name="create-your-first-sql-database-tootest-your-deployment"></a><span data-ttu-id="06534-217">Créer votre première tootest de base de données SQL de votre déploiement</span><span class="sxs-lookup"><span data-stu-id="06534-217">Create your first SQL database tootest your deployment</span></span>

1. <span data-ttu-id="06534-218">Se connecter toohello portail d’administration Azure pile en tant qu’administrateur de service.</span><span class="sxs-lookup"><span data-stu-id="06534-218">Sign in toohello Azure Stack admin portal as service admin.</span></span>

2. <span data-ttu-id="06534-219">Cliquez sur **+ Nouveau** &gt; **Données + stockage** &gt; **Base de données SQL Server (préversion)** &gt; **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="06534-219">Click **+ New** &gt;**Data + Storage"** &gt; **SQL Server Database (preview)** &gt; **Add**.</span></span>

3. <span data-ttu-id="06534-220">Renseignez le formulaire hello avec les détails de la base de données, y compris un **nom de la base de données**, **taille maximale**, et la modification hello autres paramètres si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="06534-220">Fill in hello form with database details, including a **Database Name**, **Maximum Size**, and change hello other parameters as necessary.</span></span> <span data-ttu-id="06534-221">Vous êtes invité à toopick une référence (SKU) pour votre base de données.</span><span class="sxs-lookup"><span data-stu-id="06534-221">You are asked toopick a SKU for your database.</span></span> <span data-ttu-id="06534-222">Lorsque les serveurs d’hébergement sont ajoutés, ils sont attribués à une référence (SKU) et bases de données sont créés dans ce pool de serveurs qui composent hello SKU d’hébergement.</span><span class="sxs-lookup"><span data-stu-id="06534-222">As hosting servers are added, they are assigned a SKU and databases are created in that pool of hosting servers that make up hello SKU.</span></span>

    ![Nouvelle base de données](./media/azure-stack-sql-rp-deploy/newsqldb.png)


4. <span data-ttu-id="06534-224">Renseignez hello paramètres de connexion : **connexion de base de données**, et **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="06534-224">Fill in hello Login Settings: **Database login**, and **Password**.</span></span> <span data-ttu-id="06534-225">Il s’agit d’une information d’identification de l’authentification SQL est créée pour votre accès toothis base de données uniquement.</span><span class="sxs-lookup"><span data-stu-id="06534-225">This is a SQL Authentication credential that is created for your access toothis database only.</span></span> <span data-ttu-id="06534-226">nom d’utilisateur Hello doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="06534-226">hello login user name must be globally unique.</span></span> <span data-ttu-id="06534-227">Créez un paramètre de connexion ou sélectionnez-en un qui existe déjà.</span><span class="sxs-lookup"><span data-stu-id="06534-227">Either create a new login setting or select an existing one.</span></span> <span data-ttu-id="06534-228">Vous pouvez réutiliser les paramètres de connexion pour les autres bases de données à l’aide de hello même référence SKU.</span><span class="sxs-lookup"><span data-stu-id="06534-228">You can reuse login settings for other databases using hello same SKU.</span></span>

    ![Créer une connexion de base de données](./media/azure-stack-sql-rp-deploy/create-new-login.png)


5. <span data-ttu-id="06534-230">Soumettre le formulaire de hello et attendez hello déploiement toocomplete.</span><span class="sxs-lookup"><span data-stu-id="06534-230">Submit hello form and wait for hello deployment toocomplete.</span></span>

    <span data-ttu-id="06534-231">Dans le panneau résultant de hello, notez le champ de « Chaîne de connexion » hello.</span><span class="sxs-lookup"><span data-stu-id="06534-231">In hello resulting blade, notice hello “Connection string” field.</span></span> <span data-ttu-id="06534-232">Vous pouvez utiliser cette chaîne dans toute application qui nécessite un accès à SQL Server (par exemple, une application web) dans Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="06534-232">You can use that string in any application that requires SQL Server access (for example, a web app) in your Azure Stack.</span></span>

    ![Récupérer la chaîne de connexion hello](./media/azure-stack-sql-rp-deploy/sql-db-settings.png)

## <a name="add-capacity"></a><span data-ttu-id="06534-234">Ajouter de la capacité</span><span class="sxs-lookup"><span data-stu-id="06534-234">Add capacity</span></span>

<span data-ttu-id="06534-235">Augmenter la capacité en ajoutant des hôtes SQL supplémentaires dans le portail d’Azure pile hello et les associer à une référence (SKU) approprié.</span><span class="sxs-lookup"><span data-stu-id="06534-235">Add capacity by adding additional SQL hosts in hello Azure Stack portal and associate them with an appropriate SKU.</span></span> <span data-ttu-id="06534-236">Si vous le souhaitez toouse une autre instance de SQL au lieu de hello celle installée sur le fournisseur hello machine virtuelle, cliquez sur **fournisseurs de ressources** &gt; **SQLAdapter** &gt; **SQL d’hébergement Serveurs** &gt; **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="06534-236">If you wish toouse another instance of SQL instead of hello one installed on hello provider VM, click **Resource Providers** &gt; **SQLAdapter** &gt; **SQL Hosting Servers** &gt; **+Add**.</span></span>

## <a name="making-sql-databases-available-tootenants"></a><span data-ttu-id="06534-237">Rendre les bases de données SQL tootenants disponibles</span><span class="sxs-lookup"><span data-stu-id="06534-237">Making SQL databases available tootenants</span></span>

<span data-ttu-id="06534-238">Créer des plans et des offres toomake bases de données SQL disponibles pour les locataires.</span><span class="sxs-lookup"><span data-stu-id="06534-238">Create plans and offers toomake SQL databases available for tenants.</span></span> <span data-ttu-id="06534-239">Vous devez créer un plan, ajouter hello Microsoft.SqlAdapter service toohello plan et ajouter un Quota existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="06534-239">You must create a plan, add hello Microsoft.SqlAdapter service toohello plan, and add an existing Quota, or create a new one.</span></span> <span data-ttu-id="06534-240">Si vous créez un quota, vous pouvez spécifier le locataire de hello capacité tooallow hello.</span><span class="sxs-lookup"><span data-stu-id="06534-240">If you create a quota, you can specify hello capacity tooallow hello tenant.</span></span>
    <span data-ttu-id="06534-241">![Créer des plans et des offres tooinclude bases de données](./media/azure-stack-sql-rp-deploy/sqlrp-newplan.png)</span><span class="sxs-lookup"><span data-stu-id="06534-241">![Create plans and offers tooinclude databases](./media/azure-stack-sql-rp-deploy/sqlrp-newplan.png)</span></span>

## <a name="tenant-usage-of-hello-resource-provider"></a><span data-ttu-id="06534-242">Utilisation de clients de hello fournisseur de ressources</span><span class="sxs-lookup"><span data-stu-id="06534-242">Tenant usage of hello Resource Provider</span></span>

<span data-ttu-id="06534-243">Libre service les bases de données sont fournies via l’utilisation du portail locataire hello.</span><span class="sxs-lookup"><span data-stu-id="06534-243">Self-service databases are provided through hello tenant portal experience.</span></span>

## <a name="removing-hello-sql-adapter-resource-provider"></a><span data-ttu-id="06534-244">Suppression de hello fournisseur de ressources de l’adaptateur SQL</span><span class="sxs-lookup"><span data-stu-id="06534-244">Removing hello SQL Adapter Resource Provider</span></span>

<span data-ttu-id="06534-245">Dans le fournisseur de ressources tooremove hello ordre, il est essentiel toofirst supprimer toutes les dépendances.</span><span class="sxs-lookup"><span data-stu-id="06534-245">In order tooremove hello resource provider, it is essential toofirst remove any dependencies.</span></span>

1. <span data-ttu-id="06534-246">Assurez-vous de qu'avoir hello d’origine package de déploiement que vous avez téléchargé pour cette version du fournisseur de ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="06534-246">Ensure you have hello original deployment package that you downloaded for this version of hello Resource Provider.</span></span>

2. <span data-ttu-id="06534-247">Toutes les bases de données client doivent être supprimés à partir du fournisseur de ressources hello (cela ne supprimera pas les données de salutation).</span><span class="sxs-lookup"><span data-stu-id="06534-247">All tenant databases must be deleted from hello resource provider (this will not delete hello data).</span></span> <span data-ttu-id="06534-248">Doit être effectué par les locataires hello eux-mêmes.</span><span class="sxs-lookup"><span data-stu-id="06534-248">This should be performed by hello tenants themselves.</span></span>

3. <span data-ttu-id="06534-249">Administrateur doit supprimer hello hébergeant des serveurs à partir de hello adaptateur SQL</span><span class="sxs-lookup"><span data-stu-id="06534-249">Administrator must delete hello hosting servers from hello SQL Adapter</span></span>

4. <span data-ttu-id="06534-250">Administrateur doit supprimer tous les plans qui font référence à hello adaptateur SQL.</span><span class="sxs-lookup"><span data-stu-id="06534-250">Administrator must delete any plans that reference hello SQL Adapter.</span></span>

5. <span data-ttu-id="06534-251">Administrateur doit supprimer toutes les références (SKU) et les quotas associés toohello adaptateur SQL.</span><span class="sxs-lookup"><span data-stu-id="06534-251">Administrator must delete any SKUs and quotas associated toohello SQL Adapter.</span></span>

6. <span data-ttu-id="06534-252">Réexécutez le script de déploiement hello dans hello - désinstallation de paramètre, les points de terminaison Azure Resource Manager, les DirectoryTenantID et les informations d’identification pour le compte d’administrateur de service de hello.</span><span class="sxs-lookup"><span data-stu-id="06534-252">Rerun hello deployment script with hello -Uninstall parameter, Azure Resource Manager endpoints, DirectoryTenantID, and credentials for hello service administrator account.</span></span>



## <a name="next-steps"></a><span data-ttu-id="06534-253">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="06534-253">Next steps</span></span>


<span data-ttu-id="06534-254">Essayez d’autres [services PaaS](azure-stack-tools-paas-services.md) comme hello [fournisseur de ressources MySQL Server](azure-stack-mysql-resource-provider-deploy.md) et hello [fournisseur de ressources des Services d’application](azure-stack-app-service-overview.md).</span><span class="sxs-lookup"><span data-stu-id="06534-254">Try other [PaaS services](azure-stack-tools-paas-services.md) like hello [MySQL Server resource provider](azure-stack-mysql-resource-provider-deploy.md) and hello [App Services resource provider](azure-stack-app-service-overview.md).</span></span>
