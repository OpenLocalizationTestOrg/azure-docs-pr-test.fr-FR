---
title: Ressources de certificats dans Azure Automation | Microsoft Docs
description: "Les certificats peuvent être stockés en toute sécurité dans Azure Automation afin d’y accéder par des Runbooks ou configurations DSC pour s’authentifier auprès des ressources Azure et tierces.  Cet article présente les certificats et leur utilisation dans la création textuelle et graphique."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: ac9c22ae-501f-42b9-9543-ac841cf2cc36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/19/2016
ms.author: magoedte;bwren
ms.openlocfilehash: fd1737a420c132dace9307436bfea98a9bde94a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="certificate-assets-in-azure-automation"></a><span data-ttu-id="4771e-104">Ressources de certificats dans Azure Automation</span><span class="sxs-lookup"><span data-stu-id="4771e-104">Certificate assets in Azure Automation</span></span>

<span data-ttu-id="4771e-105">Les certificats peuvent être stockés en toute sécurité dans Azure Automation afin d’être accessibles par des Runbooks ou des configurations DSC à l’aide de l’activité **Get-AzureRmAutomationRmCertificate** pour les ressoures Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4771e-105">Certificates can be stored securely in Azure Automation so they can be accessed by runbooks or DSC configurations using the **Get-AzureRmAutomationRmCertificate** activity for Azure Resource Manager resources.</span></span> <span data-ttu-id="4771e-106">Cette méthode vous permet de créer des Runbooks et des configurations DSC qui utilisent des certificats pour l’authentification ou les ajoute aux ressources Azure ou tierces.</span><span class="sxs-lookup"><span data-stu-id="4771e-106">This allows you to create runbooks and DSC configurations that use certificates for authentication or adds them to Azure or third party resources.</span></span>

> [!NOTE] 
> <span data-ttu-id="4771e-107">Les ressources sécurisées dans Azure Automation incluent les informations d'identification, les certificats, les connexions et les variables chiffrées.</span><span class="sxs-lookup"><span data-stu-id="4771e-107">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="4771e-108">Ces ressources sont chiffrées et stockées dans Azure Automation à l'aide d'une clé unique, générée pour chaque compte Automation.</span><span class="sxs-lookup"><span data-stu-id="4771e-108">These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="4771e-109">Cette clé est chiffrée par un certificat principal et stockée dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="4771e-109">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="4771e-110">Avant de stocker une ressource sécurisée, la clé pour le compte Automation est déchiffrée à l’aide du certificat principal, puis utilisée pour chiffrer la ressource.</span><span class="sxs-lookup"><span data-stu-id="4771e-110">Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.</span></span>
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="4771e-111">Applets de commande Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="4771e-111">Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="4771e-112">Les applets de commande du tableau suivant sont utilisées pour créer et gérer les ressources de certificats Automation avec Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4771e-112">The cmdlets in the following table are used to create and manage automation certificate assets with Windows PowerShell.</span></span> <span data-ttu-id="4771e-113">Elles sont fournies dans le cadre du [module Azure PowerShell](../powershell-install-configure.md) , utilisable dans les Runbooks Automation et les configurations DSC.</span><span class="sxs-lookup"><span data-stu-id="4771e-113">They ship as part of the [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configurations.</span></span>

|<span data-ttu-id="4771e-114">Applets de commande</span><span class="sxs-lookup"><span data-stu-id="4771e-114">Cmdlets</span></span>|<span data-ttu-id="4771e-115">Description</span><span class="sxs-lookup"><span data-stu-id="4771e-115">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="4771e-116">Get-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="4771e-116">Get-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603765.aspx)|<span data-ttu-id="4771e-117">Récupère des informations sur un certificat à utiliser dans un Runbook ou dans une configuration DSC.</span><span class="sxs-lookup"><span data-stu-id="4771e-117">Retrieves information about a certificate to use in a runbook or DSC configuration.</span></span> <span data-ttu-id="4771e-118">Vous pouvez uniquement récupérer le certificat lui-même à partir de l’activité Get-AutomationCertificate.</span><span class="sxs-lookup"><span data-stu-id="4771e-118">You can only retrieve the certificate itself from Get-AutomationCertificate activity.</span></span>|
|[<span data-ttu-id="4771e-119">New-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="4771e-119">New-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603604.aspx)|<span data-ttu-id="4771e-120">Crée un nouveau certificat dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="4771e-120">Creates a new certificate into Azure Automation.</span></span>|
[<span data-ttu-id="4771e-121">Remove-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="4771e-121">Remove-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603529.aspx)|<span data-ttu-id="4771e-122">Supprime un certificat dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="4771e-122">Removes a certificate from Azure Automation.</span></span>|<span data-ttu-id="4771e-123">Crée un nouveau certificat dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="4771e-123">Creates a new certificate into Azure Automation.</span></span>
|[<span data-ttu-id="4771e-124">Set-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="4771e-124">Set-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603760.aspx)|<span data-ttu-id="4771e-125">Définit les propriétés d’un certificat existant, y compris le téléchargement du fichier de certificat et le mot de passe d’un fichier .pfx.</span><span class="sxs-lookup"><span data-stu-id="4771e-125">Sets the properties for an existing certificate including uploading the certificate file and setting the password for a .pfx.</span></span>|
|[<span data-ttu-id="4771e-126">Add-AzureCertificate</span><span class="sxs-lookup"><span data-stu-id="4771e-126">Add-AzureCertificate</span></span>](https://msdn.microsoft.com/library/azure/dn495214.aspx)|<span data-ttu-id="4771e-127">Charge un certificat de service pour le service cloud spécifié.</span><span class="sxs-lookup"><span data-stu-id="4771e-127">Uploads a service certificate for the specified cloud service.</span></span>|


## <a name="creating-a-new-certificate"></a><span data-ttu-id="4771e-128">Création d’un certificat</span><span class="sxs-lookup"><span data-stu-id="4771e-128">Creating a new certificate</span></span>

<span data-ttu-id="4771e-129">Lorsque vous créez un certificat, vous téléchargez un fichier .cer ou .pfx dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="4771e-129">When you create a new certificate, you upload a .cer or .pfx file to Azure Automation.</span></span> <span data-ttu-id="4771e-130">Si vous marquez le certificat comme exportable, vous pouvez également le transférer du magasin de certificats Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="4771e-130">If you mark the certificate as exportable, then you can transfer it out of the Azure Automation certificate store.</span></span> <span data-ttu-id="4771e-131">S’il n’est pas exportable, il peut uniquement être utilisé pour la signature dans le Runbook ou la configuration DSC.</span><span class="sxs-lookup"><span data-stu-id="4771e-131">If it is not exportable, then it can only be used for signing within the runbook or DSC configuration.</span></span>


### <a name="to-create-a-new-certificate-with-the-azure-portal"></a><span data-ttu-id="4771e-132">Pour créer un certificat avec le portail Azure</span><span class="sxs-lookup"><span data-stu-id="4771e-132">To create a new certificate with the Azure portal</span></span>

1. <span data-ttu-id="4771e-133">À partir de votre compte Automation, cliquez sur le panneau **Ressources** afin d’ouvrir le panneau **Ressources**.</span><span class="sxs-lookup"><span data-stu-id="4771e-133">From your Automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
1. <span data-ttu-id="4771e-134">Cliquez sur le panneau **Certificats** pour ouvrir le panneau **Certificats**.</span><span class="sxs-lookup"><span data-stu-id="4771e-134">Click the **Certificates** tile to open the **Certificates** blade.</span></span>
1. <span data-ttu-id="4771e-135">Cliquez sur **Ajouter un certificat** en haut du panneau.</span><span class="sxs-lookup"><span data-stu-id="4771e-135">Click **Add a certificate** at the top of the blade.</span></span>
2. <span data-ttu-id="4771e-136">Tapez un nom pour le certificat dans la zone **Nom** .</span><span class="sxs-lookup"><span data-stu-id="4771e-136">Type a name for the certificate in the **Name** box.</span></span>
2. <span data-ttu-id="4771e-137">Cliquez sur **Sélectionner un fichier** sous **Charger un fichier de certificat** pour rechercher un fichier .cer ou .pfx.</span><span class="sxs-lookup"><span data-stu-id="4771e-137">Click **Select a file** under **Upload a certificate file** to browse for a .cer or .pfx file.</span></span>  <span data-ttu-id="4771e-138">Si vous sélectionnez un fichier .pfx, spécifiez un mot de passe et s’il est autorisé à être exporté.</span><span class="sxs-lookup"><span data-stu-id="4771e-138">If you select a .pfx file, specify a password and whether it should be allowed to be exported.</span></span>
1. <span data-ttu-id="4771e-139">Cliquez sur **Créer** pour enregistrer la nouvelle ressource de certificat.</span><span class="sxs-lookup"><span data-stu-id="4771e-139">Click **Create** to save the new certificate asset.</span></span>


### <a name="to-create-a-new-certificate-with-windows-powershell"></a><span data-ttu-id="4771e-140">Pour créer un certificat avec Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="4771e-140">To create a new certificate with Windows PowerShell</span></span>

<span data-ttu-id="4771e-141">L’exemple suivant démontre la création d’un certificat Automation et sont marquage comme exportable.</span><span class="sxs-lookup"><span data-stu-id="4771e-141">The following example demonstrates how to create a new Automation certificate and mark it exportable.</span></span> <span data-ttu-id="4771e-142">Cette opération importe un fichier pfx existant.</span><span class="sxs-lookup"><span data-stu-id="4771e-142">This imports an existing .pfx file.</span></span>

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a><span data-ttu-id="4771e-143">Utilisation d’un certificat</span><span class="sxs-lookup"><span data-stu-id="4771e-143">Using a certificate</span></span>

<span data-ttu-id="4771e-144">Vous devez utiliser l’activité **Get-AutomationCertificate** pour utiliser un certificat.</span><span class="sxs-lookup"><span data-stu-id="4771e-144">You must use the **Get-AutomationCertificate** activity to use a certificate.</span></span> <span data-ttu-id="4771e-145">Vous ne pouvez pas utiliser l’applet de commande [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) dans la mesure où elle retourne des informations sur la ressource de certificat, mais pas le certificat lui-même.</span><span class="sxs-lookup"><span data-stu-id="4771e-145">You cannot use the [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet since it returns information about the certificate asset but not the certificate itself.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="4771e-146">Exemple de Runbook textuel</span><span class="sxs-lookup"><span data-stu-id="4771e-146">Textual runbook sample</span></span>

<span data-ttu-id="4771e-147">L’exemple de code suivant montre comment ajouter un certificat à un service cloud dans un Runbook.</span><span class="sxs-lookup"><span data-stu-id="4771e-147">The following sample code shows how to add a certificate to a cloud service in a runbook.</span></span> <span data-ttu-id="4771e-148">Dans cet exemple, le mot de passe est récupéré à partir d’une variable Automation chiffrée.</span><span class="sxs-lookup"><span data-stu-id="4771e-148">In this sample, the password is retrieved from an encrypted automation variable.</span></span>

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a><span data-ttu-id="4771e-149">Exemple de Runbook graphique</span><span class="sxs-lookup"><span data-stu-id="4771e-149">Graphical runbook sample</span></span>

<span data-ttu-id="4771e-150">Pour ajouter une commande **Get-AutomationCerticificate** à un Runbook graphique, vous devez cliquer avec le bouton droit sur le certificat dans le volet Bibliothèque de l’éditeur graphique et sélectionner l’option **Ajouter à la zone de dessin**.</span><span class="sxs-lookup"><span data-stu-id="4771e-150">You add a **Get-AutomationCertificate** to a graphical runbook by right-clicking on the certificate in the Library pane of the graphical editor and selecting **Add to canvas**.</span></span>

![Ajouter un certificat à la zone de dessin](media/automation-certificates/automation-certificate-add-to-canvas.png)

<span data-ttu-id="4771e-152">L’image suivante montre un exemple d’utilisation d’un certificat dans un Runbook graphique.</span><span class="sxs-lookup"><span data-stu-id="4771e-152">The following image shows an example of using a certificate in a graphical runbook.</span></span>  <span data-ttu-id="4771e-153">Il s’agit du même exemple que celui affiché plus haut pour ajouter un certificat à un service cloud à partir d’un Runbook textuel.</span><span class="sxs-lookup"><span data-stu-id="4771e-153">This is the same example shown above for adding a certificate to a cloud service from a textual runbook.</span></span>

![<span data-ttu-id="4771e-154">Exemple de création graphique</span><span class="sxs-lookup"><span data-stu-id="4771e-154">Example Graphical Authoring</span></span> ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a><span data-ttu-id="4771e-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4771e-155">Next steps</span></span>

- <span data-ttu-id="4771e-156">Pour en savoir plus sur l’utilisation des liens pour contrôler le flux logique d’activités que votre runbook est conçu pour effectuer, consultez [Liens de création graphique](automation-graphical-authoring-intro.md#links-and-workflow).</span><span class="sxs-lookup"><span data-stu-id="4771e-156">To learn more about working with links to control the logical flow of activities your runbook is designed to perform, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow).</span></span> 
