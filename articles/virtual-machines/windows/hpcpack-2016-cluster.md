---
title: "Cluster HPC Pack 2016 dans Azure | Microsoft Docs"
description: "Découvrez comment déployer un cluster HPC Pack 2016 dans Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3dde6a68-e4a6-4054-8b67-d6a90fdc5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/15/2016
ms.author: danlep
ms.openlocfilehash: 88d1f4e29f38ba1a6bef57c2da43bee205575eee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a><span data-ttu-id="efef2-103">Déployer un cluster HPC Pack 2016 dans Azure</span><span class="sxs-lookup"><span data-stu-id="efef2-103">Deploy an HPC Pack 2016 cluster in Azure</span></span>

<span data-ttu-id="efef2-104">Suivez les étapes de cet article pour déployer un cluster [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) dans les machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="efef2-104">Follow the steps in this article to deploy a [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster in Azure virtual machines.</span></span> <span data-ttu-id="efef2-105">HPC Pack est la solution HPC gratuite de Microsoft basée sur les technologies Microsoft Azure et Windows Server. Elle prend en charge un vaste éventail de charges de travail HPC.</span><span class="sxs-lookup"><span data-stu-id="efef2-105">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies and supports a wide range of HPC workloads.</span></span>

<span data-ttu-id="efef2-106">Utilisez un des [modèles Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) pour déployer le cluster HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="efef2-106">Use one of the [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) to deploy the HPC Pack 2016 cluster.</span></span> <span data-ttu-id="efef2-107">Vous avez plusieurs options de topologie de cluster avec différents nombres de nœuds principaux de cluster et vous pouvez utiliser des nœuds de calcul Linux ou Windows.</span><span class="sxs-lookup"><span data-stu-id="efef2-107">You have several choices of cluster topology with different numbers of cluster head nodes, and with either Linux or Windows compute nodes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="efef2-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="efef2-108">Prerequisites</span></span>

### <a name="pfx-certificate"></a><span data-ttu-id="efef2-109">Certificat PFX</span><span class="sxs-lookup"><span data-stu-id="efef2-109">PFX certificate</span></span>

<span data-ttu-id="efef2-110">Un cluster Microsoft HPC Pack 2016 nécessite un certificat d’échange d’informations personnelles (PFX) pour sécuriser la communication entre les nœuds HPC.</span><span class="sxs-lookup"><span data-stu-id="efef2-110">A Microsoft HPC Pack 2016 cluster requires a Personal Information Exchange (PFX) certificate to secure the communication between the HPC nodes.</span></span> <span data-ttu-id="efef2-111">Le certificat doit répondre aux exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="efef2-111">The certificate must meet the following requirements:</span></span>

* <span data-ttu-id="efef2-112">Il doit avoir une clé privée capable d’échanger des clés.</span><span class="sxs-lookup"><span data-stu-id="efef2-112">It must have a private key capable of key exchange</span></span>
* <span data-ttu-id="efef2-113">L’utilisation de clés comprend la signature numérique et le chiffrage de clés.</span><span class="sxs-lookup"><span data-stu-id="efef2-113">Key usage includes Digital Signature and Key Encipherment</span></span>
* <span data-ttu-id="efef2-114">L’utilisation améliorée de la clé inclut l’authentification cliente et serveur.</span><span class="sxs-lookup"><span data-stu-id="efef2-114">Enhanced key usage includes Client Authentication and Server Authentication</span></span>

<span data-ttu-id="efef2-115">Si vous ne disposez pas d’un certificat conforme à ces exigences, vous pouvez demander le certificat auprès d’une autorité de certification.</span><span class="sxs-lookup"><span data-stu-id="efef2-115">If you don’t already have a certificate that meets these requirements, you can request the certificate from a certification authority.</span></span> <span data-ttu-id="efef2-116">Vous pouvez également utiliser les commandes suivantes pour générer le certificat auto-signé en fonction du système d’exploitation sur lequel vous exécutez la commande, et vous pouvez exporter le certificat au format PFX avec une clé privée.</span><span class="sxs-lookup"><span data-stu-id="efef2-116">Alternatively, you can use the following commands to generate the self-signed certificate based on the operating system on which you run the command, and export the PFX format certificate with private key.</span></span>

* <span data-ttu-id="efef2-117">**Pour Windows 10 ou Windows Server 2016**, exécutez l’applet de commande **New-SelfSignedCertificate** PowerShell intégrée comme suit :</span><span class="sxs-lookup"><span data-stu-id="efef2-117">**For Windows 10 or Windows Server 2016**, run the built-in **New-SelfSignedCertificate** PowerShell cmdlet as follows:</span></span>

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* <span data-ttu-id="efef2-118">**Pour les systèmes d’exploitation antérieurs à Windows 10 ou Windows Server 2016**, téléchargez le [générateur de certificat auto-signé](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) à partir du centre de scripts Microsoft.</span><span class="sxs-lookup"><span data-stu-id="efef2-118">**For operating systems earlier than Windows 10 or Windows Server 2016**, download the [self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from the Microsoft Script Center.</span></span> <span data-ttu-id="efef2-119">Extrayez son contenu et exécutez les commandes suivantes à l’invite de PowerShell :</span><span class="sxs-lookup"><span data-stu-id="efef2-119">Extract its contents and run the following commands at a PowerShell prompt:</span></span>

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-to-an-azure-key-vault"></a><span data-ttu-id="efef2-120">Chargement d’un certificat vers Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="efef2-120">Upload certificate to an Azure key vault</span></span>

<span data-ttu-id="efef2-121">Avant de déployer le cluster HPC, téléchargez le certificat vers un [coffre de clés Azure](../../key-vault/index.md) en tant que secret et enregistrez les informations suivantes pour une utilisation pendant le déploiement : **nom du coffre**, **groupe de ressources du coffre**, **URL du certificat** et **empreinte numérique du certificat**.</span><span class="sxs-lookup"><span data-stu-id="efef2-121">Before deploying the HPC cluster, upload the certificate to an [Azure key vault](../../key-vault/index.md) as a secret, and record the following information for use during the deployment: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

<span data-ttu-id="efef2-122">Un exemple de script Powershell pour charger le certificat est fourni ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="efef2-122">A sample PowerShell script to upload the certificate follows.</span></span> <span data-ttu-id="efef2-123">Pour en savoir plus sur le téléchargement d’un certificat dans Azure Key Vault, voir [Prise en main d’Azure Key Vault](../../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="efef2-123">For more information about uploading a certificate to an Azure key vault, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md).</span></span>

```powershell
#Give the following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate the pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode the JSON object
$pfxContentBytes = Get-Content $PfxFile -Encoding Byte
$pfxContentEncoded = [System.Convert]::ToBase64String($pfxContentBytes)
$jsonObject = @"
{
"data": "$pfxContentEncoded",
"dataType": "pfx",
"password": "$Password"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)
#Create an Azure key vault and upload the certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"The following Information will be used in the deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a><span data-ttu-id="efef2-124">Topologies prises en charge</span><span class="sxs-lookup"><span data-stu-id="efef2-124">Supported topologies</span></span>

<span data-ttu-id="efef2-125">Choisissez un des [modèles Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) pour déployer le cluster HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="efef2-125">Choose one of the [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) to deploy the HPC Pack 2016 cluster.</span></span> <span data-ttu-id="efef2-126">Voici les principales architectures des trois topologies de cluster prises en charge.</span><span class="sxs-lookup"><span data-stu-id="efef2-126">Following are high-level architectures of three supported cluster topologies.</span></span> <span data-ttu-id="efef2-127">Les topologies à haute disponibilité incluent plusieurs nœuds principaux de cluster.</span><span class="sxs-lookup"><span data-stu-id="efef2-127">High-availability topologies include multiple cluster head nodes.</span></span>

1. <span data-ttu-id="efef2-128">Cluster haute disponibilité avec un domaine Active Directory</span><span class="sxs-lookup"><span data-stu-id="efef2-128">High-availability cluster with Active Directory domain</span></span>

    ![Cluster haute disponibilité dans un domaine AD](./media/hpcpack-2016-cluster/haad.png)



2. <span data-ttu-id="efef2-130">Cluster haute disponibilité sans domaine Active Directory</span><span class="sxs-lookup"><span data-stu-id="efef2-130">High-availability cluster without Active Directory domain</span></span>

    ![Cluster haute disponibilité sans domaine AD](./media/hpcpack-2016-cluster/hanoad.png)

3. <span data-ttu-id="efef2-132">Cluster avec un seul nœud principal</span><span class="sxs-lookup"><span data-stu-id="efef2-132">Cluster with a single head node</span></span>

   ![Cluster avec un seul nœud principal](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a><span data-ttu-id="efef2-134">Déployer un cluster</span><span class="sxs-lookup"><span data-stu-id="efef2-134">Deploy a cluster</span></span>

<span data-ttu-id="efef2-135">Pour créer le cluster, choisissez un modèle et cliquez sur **Déployer sur Azure**.</span><span class="sxs-lookup"><span data-stu-id="efef2-135">To create the cluster, choose a template and click **Deploy to Azure**.</span></span> <span data-ttu-id="efef2-136">Dans le [portail Azure](https://portal.azure.com), spécifiez les paramètres du modèle comme décrit dans les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="efef2-136">In the [Azure portal](https://portal.azure.com), specify parameters for the template as described in the following steps.</span></span> <span data-ttu-id="efef2-137">Chaque modèle crée toutes les ressources Azure requises pour l’infrastructure de cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="efef2-137">Each template creates all Azure resources required for the HPC cluster infrastructure.</span></span> <span data-ttu-id="efef2-138">Les ressources incluent un réseau virtuel Azure, une adresse IP publique, un équilibreur de charge (uniquement pour un cluster haute disponibilité), des interfaces réseau, des groupes à haute disponibilité, des comptes de stockage et des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="efef2-138">Resources include an Azure virtual network, public IP address, load balancer (only for a high-availability cluster), network interfaces, availability sets, storage accounts, and virtual machines.</span></span>

### <a name="step-1-select-the-subscription-location-and-resource-group"></a><span data-ttu-id="efef2-139">Étape 1 : Sélectionner l’abonnement, l’emplacement et le groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="efef2-139">Step 1: Select the subscription, location, and resource group</span></span>

<span data-ttu-id="efef2-140">L’**abonnement** et l’**emplacement** doivent être les mêmes que ceux que vous avez spécifiés lorsque vous avez téléchargé votre certificat PFX (voir Configuration requise).</span><span class="sxs-lookup"><span data-stu-id="efef2-140">The **Subscription** and the **Location** must be same that you specified when you uploaded your PFX certificate (see Prerequisites).</span></span> <span data-ttu-id="efef2-141">Nous vous recommandons de créer un **groupe de ressources** pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="efef2-141">We recommend that you create a **Resource group** for the deployment.</span></span>

### <a name="step-2-specify-the-parameter-settings"></a><span data-ttu-id="efef2-142">Étape 2 : Spécifier les paramètres</span><span class="sxs-lookup"><span data-stu-id="efef2-142">Step 2: Specify the parameter settings</span></span>

<span data-ttu-id="efef2-143">Saisissez ou modifiez les valeurs des paramètres du modèle.</span><span class="sxs-lookup"><span data-stu-id="efef2-143">Enter or modify values for the template parameters.</span></span> <span data-ttu-id="efef2-144">Cliquez sur l’icône en regard de chaque paramètre pour obtenir de l’aide.</span><span class="sxs-lookup"><span data-stu-id="efef2-144">Click the icon next to each parameter for help information.</span></span> <span data-ttu-id="efef2-145">Voir aussi les conseils sur les [tailles de machines virtuelles disponibles](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="efef2-145">Also see the guidance for [available VM sizes](sizes.md).</span></span>

<span data-ttu-id="efef2-146">Spécifiez les valeurs que vous avez enregistrées dans les conditions préalables pour les paramètres suivants : **nom du coffre**, **groupe de ressources du coffre**, **URL du certificat** et **empreinte numérique du certificat**.</span><span class="sxs-lookup"><span data-stu-id="efef2-146">Specify the values you recorded in the Prerequisites for the following parameters: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

### <a name="step-3-review-legal-terms-and-create"></a><span data-ttu-id="efef2-147">Étape 3.</span><span class="sxs-lookup"><span data-stu-id="efef2-147">Step 3.</span></span> <span data-ttu-id="efef2-148">Consulter les termes et conditions et créer</span><span class="sxs-lookup"><span data-stu-id="efef2-148">Review legal terms and create</span></span>
<span data-ttu-id="efef2-149">Cliquez sur les **Mentions légales** pour les lire.</span><span class="sxs-lookup"><span data-stu-id="efef2-149">Click **Review legal terms** to review the terms.</span></span> <span data-ttu-id="efef2-150">Si vous les acceptez, cliquez sur **Acheter**, puis sur **Créer** pour commencer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="efef2-150">If you agree, click **Purchase**, and then click **Create** to start the deployment.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="efef2-151">Connexion au cluster</span><span class="sxs-lookup"><span data-stu-id="efef2-151">Connect to the cluster</span></span>
1. <span data-ttu-id="efef2-152">Une fois que le cluster HPC Pack est déployé, accédez au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="efef2-152">After the HPC Pack cluster is deployed, go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="efef2-153">Cliquez sur **Groupes de ressources**, puis recherchez le groupe de ressources dans lequel le cluster a été déployé.</span><span class="sxs-lookup"><span data-stu-id="efef2-153">Click **Resource groups**, and find the resource group in which the cluster was deployed.</span></span> <span data-ttu-id="efef2-154">Vous pouvez rechercher les machines virtuelles avec nœud principal.</span><span class="sxs-lookup"><span data-stu-id="efef2-154">You can find the head node virtual machines.</span></span>

    ![Nœuds principaux de cluster dans le portail](./media/hpcpack-2016-cluster/clusterhns.png)

2. <span data-ttu-id="efef2-156">Cliquez sur un nœud principal (dans un cluster haute disponibilité, cliquez sur l’un de ceux disponibles).</span><span class="sxs-lookup"><span data-stu-id="efef2-156">Click one head node (in a high-availability cluster, click any of the head nodes).</span></span> <span data-ttu-id="efef2-157">Dans **Bases**, vous pouvez trouver l’adresse IP publique ou le nom DNS complet du cluster.</span><span class="sxs-lookup"><span data-stu-id="efef2-157">In **Essentials**, you can find the public IP address or full DNS name of the cluster.</span></span>

    ![Paramètres de connexion au cluster](./media/hpcpack-2016-cluster/clusterconnect.png)

3. <span data-ttu-id="efef2-159">Cliquez sur **Se connecter** pour vous connecter aux nœuds principaux à l’aide du Bureau à distance avec votre nom d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="efef2-159">Click **Connect** to log on to any of the head nodes using Remote Desktop with your specified administrator user name.</span></span> <span data-ttu-id="efef2-160">Si le cluster que vous avez déployé est dans un domaine Active Directory, le nom d’utilisateur est au format <privateDomainName>\<adminUsername> (par exemple hpc.local\hpcadmin).</span><span class="sxs-lookup"><span data-stu-id="efef2-160">If the cluster you deployed is in an Active Directory Domain, the user name is of the form <privateDomainName>\<adminUsername> (for example, hpc.local\hpcadmin).</span></span>

## <a name="next-steps"></a><span data-ttu-id="efef2-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="efef2-161">Next steps</span></span>
* <span data-ttu-id="efef2-162">Envoyez des travaux au cluster.</span><span class="sxs-lookup"><span data-stu-id="efef2-162">Submit jobs to your cluster.</span></span> <span data-ttu-id="efef2-163">Voir [Envoyer des travaux à un cluster HPC Pack dans Azure](hpcpack-cluster-submit-jobs.md) et [Gérer un cluster HPC Pack 2016 dans Azure avec Azure Active Directory](hpcpack-cluster-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="efef2-163">See [Submit jobs to HPC an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md) and [Manage an HPC Pack 2016 cluster in Azure using Azure Active Directory](hpcpack-cluster-active-directory.md).</span></span>

