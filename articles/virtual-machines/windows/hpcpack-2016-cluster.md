---
title: aaaHPC Pack 2016 de cluster dans Azure | Documents Microsoft
description: "Découvrez comment toodeploy une 2016 de Pack HPC cluster dans Azure"
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
ms.openlocfilehash: 9e21ec70c822a783474b96da77ce925940279abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a><span data-ttu-id="9c746-103">Déployer un cluster HPC Pack 2016 dans Azure</span><span class="sxs-lookup"><span data-stu-id="9c746-103">Deploy an HPC Pack 2016 cluster in Azure</span></span>

<span data-ttu-id="9c746-104">Suivez les étapes de hello dans cet article de toodeploy un [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster dans les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="9c746-104">Follow hello steps in this article toodeploy a [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster in Azure virtual machines.</span></span> <span data-ttu-id="9c746-105">HPC Pack est la solution HPC gratuite de Microsoft basée sur les technologies Microsoft Azure et Windows Server. Elle prend en charge un vaste éventail de charges de travail HPC.</span><span class="sxs-lookup"><span data-stu-id="9c746-105">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies and supports a wide range of HPC workloads.</span></span>

<span data-ttu-id="9c746-106">Utilisez une des hello [modèles Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) cluster hello HPC Pack 2016 de toodeploy.</span><span class="sxs-lookup"><span data-stu-id="9c746-106">Use one of hello [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 cluster.</span></span> <span data-ttu-id="9c746-107">Vous avez plusieurs options de topologie de cluster avec différents nombres de nœuds principaux de cluster et vous pouvez utiliser des nœuds de calcul Linux ou Windows.</span><span class="sxs-lookup"><span data-stu-id="9c746-107">You have several choices of cluster topology with different numbers of cluster head nodes, and with either Linux or Windows compute nodes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c746-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9c746-108">Prerequisites</span></span>

### <a name="pfx-certificate"></a><span data-ttu-id="9c746-109">Certificat PFX</span><span class="sxs-lookup"><span data-stu-id="9c746-109">PFX certificate</span></span>

<span data-ttu-id="9c746-110">Un cluster Microsoft HPC Pack 2016 nécessite une certificat Exchange d’informations personnelles (PFX) toosecure une communication hello entre les nœuds HPC hello.</span><span class="sxs-lookup"><span data-stu-id="9c746-110">A Microsoft HPC Pack 2016 cluster requires a Personal Information Exchange (PFX) certificate toosecure hello communication between hello HPC nodes.</span></span> <span data-ttu-id="9c746-111">certificat de Hello doit respecter hello suivant les exigences :</span><span class="sxs-lookup"><span data-stu-id="9c746-111">hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="9c746-112">Il doit avoir une clé privée capable d’échanger des clés.</span><span class="sxs-lookup"><span data-stu-id="9c746-112">It must have a private key capable of key exchange</span></span>
* <span data-ttu-id="9c746-113">L’utilisation de clés comprend la signature numérique et le chiffrage de clés.</span><span class="sxs-lookup"><span data-stu-id="9c746-113">Key usage includes Digital Signature and Key Encipherment</span></span>
* <span data-ttu-id="9c746-114">L’utilisation améliorée de la clé inclut l’authentification cliente et serveur.</span><span class="sxs-lookup"><span data-stu-id="9c746-114">Enhanced key usage includes Client Authentication and Server Authentication</span></span>

<span data-ttu-id="9c746-115">Si vous n’avez pas encore un certificat qui répond à ces exigences, vous pouvez demander le certificat de hello à partir d’une autorité de certification.</span><span class="sxs-lookup"><span data-stu-id="9c746-115">If you don’t already have a certificate that meets these requirements, you can request hello certificate from a certification authority.</span></span> <span data-ttu-id="9c746-116">Vous pouvez également utiliser hello suivant de commandes toogenerate hello un certificat auto-signé fonction hello système d’exploitation sur lequel vous exécutez la commande hello et exportez un certificat PFX format hello avec la clé privée.</span><span class="sxs-lookup"><span data-stu-id="9c746-116">Alternatively, you can use hello following commands toogenerate hello self-signed certificate based on hello operating system on which you run hello command, and export hello PFX format certificate with private key.</span></span>

* <span data-ttu-id="9c746-117">**Pour Windows 10 ou Windows Server 2016**, exécutez hello intégré **New-SelfSignedCertificate** applet de commande PowerShell comme suit :</span><span class="sxs-lookup"><span data-stu-id="9c746-117">**For Windows 10 or Windows Server 2016**, run hello built-in **New-SelfSignedCertificate** PowerShell cmdlet as follows:</span></span>

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* <span data-ttu-id="9c746-118">**Pour les systèmes d’exploitation antérieurs à Windows 10 ou Windows Server 2016**, télécharger hello [générateur du certificat auto-signé](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) de hello Microsoft Script Center.</span><span class="sxs-lookup"><span data-stu-id="9c746-118">**For operating systems earlier than Windows 10 or Windows Server 2016**, download hello [self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from hello Microsoft Script Center.</span></span> <span data-ttu-id="9c746-119">Extrayez son contenu, puis exécutez hello suivant les commandes à l’invite de PowerShell :</span><span class="sxs-lookup"><span data-stu-id="9c746-119">Extract its contents and run hello following commands at a PowerShell prompt:</span></span>

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-tooan-azure-key-vault"></a><span data-ttu-id="9c746-120">Télécharger le certificat tooan coffre de clés Azure</span><span class="sxs-lookup"><span data-stu-id="9c746-120">Upload certificate tooan Azure key vault</span></span>

<span data-ttu-id="9c746-121">Avant de déployer un cluster HPC de hello, télécharger hello certificat tooan [coffre de clés Azure](../../key-vault/index.md) comme un Bonjour secret et enregistrement suivant des informations pour une utilisation pendant le déploiement de hello : **nom du coffre**,  **Groupe de ressources de coffre**, **URL de certificat**, et **empreinte numérique du certificat**.</span><span class="sxs-lookup"><span data-stu-id="9c746-121">Before deploying hello HPC cluster, upload hello certificate tooan [Azure key vault](../../key-vault/index.md) as a secret, and record hello following information for use during hello deployment: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

<span data-ttu-id="9c746-122">Un certificat de hello exemple PowerShell script tooupload suit.</span><span class="sxs-lookup"><span data-stu-id="9c746-122">A sample PowerShell script tooupload hello certificate follows.</span></span> <span data-ttu-id="9c746-123">Pour plus d’informations sur le téléchargement d’un certificat de tooan coffre de clés Azure, consultez [prise en main d’Azure Key Vault](../../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9c746-123">For more information about uploading a certificate tooan Azure key vault, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md).</span></span>

```powershell
#Give hello following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate hello pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode hello JSON object
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
#Create an Azure key vault and upload hello certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"hello following Information will be used in hello deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a><span data-ttu-id="9c746-124">Topologies prises en charge</span><span class="sxs-lookup"><span data-stu-id="9c746-124">Supported topologies</span></span>

<span data-ttu-id="9c746-125">Choisissez une des hello [modèles Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) cluster hello HPC Pack 2016 de toodeploy.</span><span class="sxs-lookup"><span data-stu-id="9c746-125">Choose one of hello [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 cluster.</span></span> <span data-ttu-id="9c746-126">Voici les principales architectures des trois topologies de cluster prises en charge.</span><span class="sxs-lookup"><span data-stu-id="9c746-126">Following are high-level architectures of three supported cluster topologies.</span></span> <span data-ttu-id="9c746-127">Les topologies à haute disponibilité incluent plusieurs nœuds principaux de cluster.</span><span class="sxs-lookup"><span data-stu-id="9c746-127">High-availability topologies include multiple cluster head nodes.</span></span>

1. <span data-ttu-id="9c746-128">Cluster haute disponibilité avec un domaine Active Directory</span><span class="sxs-lookup"><span data-stu-id="9c746-128">High-availability cluster with Active Directory domain</span></span>

    ![Cluster haute disponibilité dans un domaine AD](./media/hpcpack-2016-cluster/haad.png)



2. <span data-ttu-id="9c746-130">Cluster haute disponibilité sans domaine Active Directory</span><span class="sxs-lookup"><span data-stu-id="9c746-130">High-availability cluster without Active Directory domain</span></span>

    ![Cluster haute disponibilité sans domaine AD](./media/hpcpack-2016-cluster/hanoad.png)

3. <span data-ttu-id="9c746-132">Cluster avec un seul nœud principal</span><span class="sxs-lookup"><span data-stu-id="9c746-132">Cluster with a single head node</span></span>

   ![Cluster avec un seul nœud principal](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a><span data-ttu-id="9c746-134">Déployer un cluster</span><span class="sxs-lookup"><span data-stu-id="9c746-134">Deploy a cluster</span></span>

<span data-ttu-id="9c746-135">cluster de hello toocreate, choisir un modèle et cliquez sur **déployer tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="9c746-135">toocreate hello cluster, choose a template and click **Deploy tooAzure**.</span></span> <span data-ttu-id="9c746-136">Bonjour [portail Azure](https://portal.azure.com), spécifiez des paramètres pour le modèle de hello comme décrit dans hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="9c746-136">In hello [Azure portal](https://portal.azure.com), specify parameters for hello template as described in hello following steps.</span></span> <span data-ttu-id="9c746-137">Chaque modèle crée toutes les ressources Azure requis pour l’infrastructure de cluster HPC hello.</span><span class="sxs-lookup"><span data-stu-id="9c746-137">Each template creates all Azure resources required for hello HPC cluster infrastructure.</span></span> <span data-ttu-id="9c746-138">Les ressources incluent un réseau virtuel Azure, une adresse IP publique, un équilibreur de charge (uniquement pour un cluster haute disponibilité), des interfaces réseau, des groupes à haute disponibilité, des comptes de stockage et des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="9c746-138">Resources include an Azure virtual network, public IP address, load balancer (only for a high-availability cluster), network interfaces, availability sets, storage accounts, and virtual machines.</span></span>

### <a name="step-1-select-hello-subscription-location-and-resource-group"></a><span data-ttu-id="9c746-139">Étape 1 : Sélectionnez l’abonnement de hello, l’emplacement et groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="9c746-139">Step 1: Select hello subscription, location, and resource group</span></span>

<span data-ttu-id="9c746-140">Hello **abonnement** et hello **emplacement** doit être le même que vous avez spécifié lorsque vous avez téléchargé votre certificat PFX (voir la configuration requise).</span><span class="sxs-lookup"><span data-stu-id="9c746-140">hello **Subscription** and hello **Location** must be same that you specified when you uploaded your PFX certificate (see Prerequisites).</span></span> <span data-ttu-id="9c746-141">Nous vous recommandons de créer un **groupe de ressources** pour le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="9c746-141">We recommend that you create a **Resource group** for hello deployment.</span></span>

### <a name="step-2-specify-hello-parameter-settings"></a><span data-ttu-id="9c746-142">Étape 2 : Spécifier les paramètres hello</span><span class="sxs-lookup"><span data-stu-id="9c746-142">Step 2: Specify hello parameter settings</span></span>

<span data-ttu-id="9c746-143">Entrez ou modifiez les valeurs des paramètres du modèle hello.</span><span class="sxs-lookup"><span data-stu-id="9c746-143">Enter or modify values for hello template parameters.</span></span> <span data-ttu-id="9c746-144">Cliquez sur le paramètre suivant tooeach hello icône pour les informations d’aide.</span><span class="sxs-lookup"><span data-stu-id="9c746-144">Click hello icon next tooeach parameter for help information.</span></span> <span data-ttu-id="9c746-145">Consultez également les conseils de hello pour [des tailles de machine virtuelle disponibles](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="9c746-145">Also see hello guidance for [available VM sizes](sizes.md).</span></span>

<span data-ttu-id="9c746-146">Spécifiez les valeurs hello enregistrés dans les conditions préalables de hello pour hello paramètres suivants : **nom du coffre**, **groupe de ressources de coffre**, **URL de certificat**et **Empreinte numérique du certificat**.</span><span class="sxs-lookup"><span data-stu-id="9c746-146">Specify hello values you recorded in hello Prerequisites for hello following parameters: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

### <a name="step-3-review-legal-terms-and-create"></a><span data-ttu-id="9c746-147">Étape 3.</span><span class="sxs-lookup"><span data-stu-id="9c746-147">Step 3.</span></span> <span data-ttu-id="9c746-148">Consulter les termes et conditions et créer</span><span class="sxs-lookup"><span data-stu-id="9c746-148">Review legal terms and create</span></span>
<span data-ttu-id="9c746-149">Cliquez sur **passez en revue les conditions juridiques** termes du contrat de tooreview hello.</span><span class="sxs-lookup"><span data-stu-id="9c746-149">Click **Review legal terms** tooreview hello terms.</span></span> <span data-ttu-id="9c746-150">Si vous acceptez, cliquez sur **achat**, puis cliquez sur **créer** déploiement de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="9c746-150">If you agree, click **Purchase**, and then click **Create** toostart hello deployment.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="9c746-151">Se connecter toohello cluster</span><span class="sxs-lookup"><span data-stu-id="9c746-151">Connect toohello cluster</span></span>
1. <span data-ttu-id="9c746-152">Après le déployée de cluster HPC Pack de hello, accédez à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9c746-152">After hello HPC Pack cluster is deployed, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9c746-153">Cliquez sur **groupes de ressources**et groupe de ressources hello rechercher dans le hello cluster a été déployée.</span><span class="sxs-lookup"><span data-stu-id="9c746-153">Click **Resource groups**, and find hello resource group in which hello cluster was deployed.</span></span> <span data-ttu-id="9c746-154">Machines virtuelles de nœud principal, vous pouvez trouver hello.</span><span class="sxs-lookup"><span data-stu-id="9c746-154">You can find hello head node virtual machines.</span></span>

    ![Nœuds de cluster principal dans le portail de hello](./media/hpcpack-2016-cluster/clusterhns.png)

2. <span data-ttu-id="9c746-156">Cliquez sur un seul nœud principal (dans un cluster de haute disponibilité, cliquez sur un des nœuds de tête hello).</span><span class="sxs-lookup"><span data-stu-id="9c746-156">Click one head node (in a high-availability cluster, click any of hello head nodes).</span></span> <span data-ttu-id="9c746-157">Dans **Essentials**, vous pouvez trouver d’adresse IP publique de hello ou le nom DNS complet du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="9c746-157">In **Essentials**, you can find hello public IP address or full DNS name of hello cluster.</span></span>

    ![Paramètres de connexion au cluster](./media/hpcpack-2016-cluster/clusterconnect.png)

3. <span data-ttu-id="9c746-159">Cliquez sur **Connect** toolog sur tooany de nœuds principaux d’hello avec votre nom d’utilisateur administrateur spécifié à l’aide de bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="9c746-159">Click **Connect** toolog on tooany of hello head nodes using Remote Desktop with your specified administrator user name.</span></span> <span data-ttu-id="9c746-160">Si le cluster hello vous avez déployée est dans un domaine Active Directory, le nom d’utilisateur de hello est sous forme de hello <privateDomainName> \<adminUsername > (par exemple, hpc.local\hpcadmin).</span><span class="sxs-lookup"><span data-stu-id="9c746-160">If hello cluster you deployed is in an Active Directory Domain, hello user name is of hello form <privateDomainName>\<adminUsername> (for example, hpc.local\hpcadmin).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c746-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9c746-161">Next steps</span></span>
* <span data-ttu-id="9c746-162">Soumettre le cluster tooyour de travaux.</span><span class="sxs-lookup"><span data-stu-id="9c746-162">Submit jobs tooyour cluster.</span></span> <span data-ttu-id="9c746-163">Consultez [envoyer des travaux tooHPC un cluster HPC Pack dans Azure](hpcpack-cluster-submit-jobs.md) et [gérer un cluster HPC Pack 2016 dans Azure à l’aide d’Azure Active Directory](hpcpack-cluster-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="9c746-163">See [Submit jobs tooHPC an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md) and [Manage an HPC Pack 2016 cluster in Azure using Azure Active Directory](hpcpack-cluster-active-directory.md).</span></span>

