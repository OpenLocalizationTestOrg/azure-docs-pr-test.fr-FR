---
title: ressources aaaCertificate dans Azure Automation | Documents Microsoft
description: "Les certificats peuvent être stockées en toute sécurité dans Azure Automation afin qu’ils sont accessibles par les procédures opérationnelles ou tooauthenticate des configurations DSC sur Azure et les ressources tierces.  Cet article explique les détails de hello des certificats et comment toowork avec eux dans textuels et graphiques de création."
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
ms.openlocfilehash: 2c25bee937890438ea9022669be2c24c77a110b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-assets-in-azure-automation"></a><span data-ttu-id="01353-104">Ressources de certificats dans Azure Automation</span><span class="sxs-lookup"><span data-stu-id="01353-104">Certificate assets in Azure Automation</span></span>

<span data-ttu-id="01353-105">Les certificats peuvent être stockés en toute sécurité dans Azure Automation afin qu’ils sont accessibles par les procédures opérationnelles ou les configurations DSC à l’aide de hello **Get-AzureRmAutomationRmCertificate** activité pour les ressources Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="01353-105">Certificates can be stored securely in Azure Automation so they can be accessed by runbooks or DSC configurations using hello **Get-AzureRmAutomationRmCertificate** activity for Azure Resource Manager resources.</span></span> <span data-ttu-id="01353-106">Cela vous permet de toocreate runbooks et les configurations DSC qui utilisent des certificats pour l’authentification ou ajoute les ressources tooAzure ou tiers.</span><span class="sxs-lookup"><span data-stu-id="01353-106">This allows you toocreate runbooks and DSC configurations that use certificates for authentication or adds them tooAzure or third party resources.</span></span>

> [!NOTE] 
> <span data-ttu-id="01353-107">Les ressources sécurisées dans Azure Automation incluent les informations d'identification, les certificats, les connexions et les variables chiffrées.</span><span class="sxs-lookup"><span data-stu-id="01353-107">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="01353-108">Ces ressources sont chiffrées et stockées Bonjour Azure Automation à l’aide d’une clé unique qui est générée pour chaque compte automation.</span><span class="sxs-lookup"><span data-stu-id="01353-108">These assets are encrypted and stored in hello Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="01353-109">Cette clé est chiffrée par un certificat principal et stockée dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="01353-109">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="01353-110">Avant de stocker une ressource sécurisée, clé hello pour le compte d’automatisation hello est déchiffré à l’aide du certificat master de hello, puis utilisé asset de hello tooencrypt.</span><span class="sxs-lookup"><span data-stu-id="01353-110">Before storing a secure asset, hello key for hello automation account is decrypted using hello master certificate and then used tooencrypt hello asset.</span></span>
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="01353-111">Applets de commande Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="01353-111">Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="01353-112">applets de commande Hello Bonjour tableau suivant sont utilisée toocreate et gérer des ressources de certificat automation avec Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="01353-112">hello cmdlets in hello following table are used toocreate and manage automation certificate assets with Windows PowerShell.</span></span> <span data-ttu-id="01353-113">Elles font partie de hello [module Azure PowerShell](../powershell-install-configure.md) qui est disponible pour une utilisation dans les runbooks Automation et les configurations DSC.</span><span class="sxs-lookup"><span data-stu-id="01353-113">They ship as part of hello [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configurations.</span></span>

|<span data-ttu-id="01353-114">Applets de commande</span><span class="sxs-lookup"><span data-stu-id="01353-114">Cmdlets</span></span>|<span data-ttu-id="01353-115">Description</span><span class="sxs-lookup"><span data-stu-id="01353-115">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="01353-116">Get-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="01353-116">Get-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603765.aspx)|<span data-ttu-id="01353-117">Récupère des informations sur un toouse de certificat dans un runbook ou la configuration DSC.</span><span class="sxs-lookup"><span data-stu-id="01353-117">Retrieves information about a certificate toouse in a runbook or DSC configuration.</span></span> <span data-ttu-id="01353-118">Vous pouvez uniquement récupérer le certificat hello lui-même à partir de l’activité de Get-AutomationCertificate.</span><span class="sxs-lookup"><span data-stu-id="01353-118">You can only retrieve hello certificate itself from Get-AutomationCertificate activity.</span></span>|
|[<span data-ttu-id="01353-119">New-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="01353-119">New-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603604.aspx)|<span data-ttu-id="01353-120">Crée un nouveau certificat dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="01353-120">Creates a new certificate into Azure Automation.</span></span>|
[<span data-ttu-id="01353-121">Remove-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="01353-121">Remove-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603529.aspx)|<span data-ttu-id="01353-122">Supprime un certificat dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="01353-122">Removes a certificate from Azure Automation.</span></span>|<span data-ttu-id="01353-123">Crée un nouveau certificat dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="01353-123">Creates a new certificate into Azure Automation.</span></span>
|[<span data-ttu-id="01353-124">Set-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="01353-124">Set-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603760.aspx)|<span data-ttu-id="01353-125">Définit les propriétés hello pour un certificat existant, notamment le téléchargement du fichier de certificat hello et un mot de passe hello paramètre d’un fichier .pfx.</span><span class="sxs-lookup"><span data-stu-id="01353-125">Sets hello properties for an existing certificate including uploading hello certificate file and setting hello password for a .pfx.</span></span>|
|[<span data-ttu-id="01353-126">Add-AzureCertificate</span><span class="sxs-lookup"><span data-stu-id="01353-126">Add-AzureCertificate</span></span>](https://msdn.microsoft.com/library/azure/dn495214.aspx)|<span data-ttu-id="01353-127">Téléchargements d’un service de certificats pour hello spécifié service cloud.</span><span class="sxs-lookup"><span data-stu-id="01353-127">Uploads a service certificate for hello specified cloud service.</span></span>|


## <a name="creating-a-new-certificate"></a><span data-ttu-id="01353-128">Création d’un certificat</span><span class="sxs-lookup"><span data-stu-id="01353-128">Creating a new certificate</span></span>

<span data-ttu-id="01353-129">Lorsque vous créez un nouveau certificat, vous téléchargez un fichier .cer ou .pfx tooAzure Automation.</span><span class="sxs-lookup"><span data-stu-id="01353-129">When you create a new certificate, you upload a .cer or .pfx file tooAzure Automation.</span></span> <span data-ttu-id="01353-130">Si vous marquez le certificat hello comme exportable, vous pouvez également le transférer hors de magasin de certificats Azure Automation hello.</span><span class="sxs-lookup"><span data-stu-id="01353-130">If you mark hello certificate as exportable, then you can transfer it out of hello Azure Automation certificate store.</span></span> <span data-ttu-id="01353-131">Si elle n’est pas exportable, puis il peut uniquement être utilisé pour la signature dans hello runbook ou la configuration DSC.</span><span class="sxs-lookup"><span data-stu-id="01353-131">If it is not exportable, then it can only be used for signing within hello runbook or DSC configuration.</span></span>


### <a name="toocreate-a-new-certificate-with-hello-azure-portal"></a><span data-ttu-id="01353-132">toocreate un nouveau certificat avec hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="01353-132">toocreate a new certificate with hello Azure portal</span></span>

1. <span data-ttu-id="01353-133">À partir de votre compte Automation, cliquez sur hello **actifs** vignette tooopen hello **actifs** panneau.</span><span class="sxs-lookup"><span data-stu-id="01353-133">From your Automation account, click hello **Assets** tile tooopen hello **Assets** blade.</span></span>
1. <span data-ttu-id="01353-134">Cliquez sur hello **certificats** vignette tooopen hello **certificats** panneau.</span><span class="sxs-lookup"><span data-stu-id="01353-134">Click hello **Certificates** tile tooopen hello **Certificates** blade.</span></span>
1. <span data-ttu-id="01353-135">Cliquez sur **ajouter un certificat** haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="01353-135">Click **Add a certificate** at hello top of hello blade.</span></span>
2. <span data-ttu-id="01353-136">Tapez un nom pour le certificat de hello Bonjour **nom** boîte.</span><span class="sxs-lookup"><span data-stu-id="01353-136">Type a name for hello certificate in hello **Name** box.</span></span>
2. <span data-ttu-id="01353-137">Cliquez sur **sélectionner un fichier** sous **télécharger un fichier de certificat** toobrowse pour un fichier .cer ou .pfx.</span><span class="sxs-lookup"><span data-stu-id="01353-137">Click **Select a file** under **Upload a certificate file** toobrowse for a .cer or .pfx file.</span></span>  <span data-ttu-id="01353-138">Si vous sélectionnez un fichier .pfx, spécifiez un mot de passe et si elle doit être autorisée toobe exporté.</span><span class="sxs-lookup"><span data-stu-id="01353-138">If you select a .pfx file, specify a password and whether it should be allowed toobe exported.</span></span>
1. <span data-ttu-id="01353-139">Cliquez sur **créer** toosave hello nouveau certificat bien.</span><span class="sxs-lookup"><span data-stu-id="01353-139">Click **Create** toosave hello new certificate asset.</span></span>


### <a name="toocreate-a-new-certificate-with-windows-powershell"></a><span data-ttu-id="01353-140">toocreate un nouveau certificat avec Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="01353-140">toocreate a new certificate with Windows PowerShell</span></span>

<span data-ttu-id="01353-141">Hello exemple suivant montre comment toocreate une Automation de nouveau certificat et marquer exportable.</span><span class="sxs-lookup"><span data-stu-id="01353-141">hello following example demonstrates how toocreate a new Automation certificate and mark it exportable.</span></span> <span data-ttu-id="01353-142">Cette opération importe un fichier pfx existant.</span><span class="sxs-lookup"><span data-stu-id="01353-142">This imports an existing .pfx file.</span></span>

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a><span data-ttu-id="01353-143">Utilisation d’un certificat</span><span class="sxs-lookup"><span data-stu-id="01353-143">Using a certificate</span></span>

<span data-ttu-id="01353-144">Vous devez utiliser hello **Get-AutomationCertificate** activité toouse un certificat.</span><span class="sxs-lookup"><span data-stu-id="01353-144">You must use hello **Get-AutomationCertificate** activity toouse a certificate.</span></span> <span data-ttu-id="01353-145">Vous ne pouvez pas utiliser hello [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) applet de commande, car elle retourne des informations sur la ressource de certificat hello mais pas les certificats hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="01353-145">You cannot use hello [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet since it returns information about hello certificate asset but not hello certificate itself.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="01353-146">Exemple de Runbook textuel</span><span class="sxs-lookup"><span data-stu-id="01353-146">Textual runbook sample</span></span>

<span data-ttu-id="01353-147">Hello suivant l’exemple de code montre comment tooadd un tooa certificat service de cloud computing dans un runbook.</span><span class="sxs-lookup"><span data-stu-id="01353-147">hello following sample code shows how tooadd a certificate tooa cloud service in a runbook.</span></span> <span data-ttu-id="01353-148">Dans cet exemple, un mot de passe hello est récupérée à partir d’une variable automation chiffrée.</span><span class="sxs-lookup"><span data-stu-id="01353-148">In this sample, hello password is retrieved from an encrypted automation variable.</span></span>

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a><span data-ttu-id="01353-149">Exemple de Runbook graphique</span><span class="sxs-lookup"><span data-stu-id="01353-149">Graphical runbook sample</span></span>

<span data-ttu-id="01353-150">Vous ajoutez un **Get-AutomationCertificate** tooa des runbook graphique en cliquant sur le certificat hello dans le volet Bibliothèque de hello de l’éditeur graphique de hello et en sélectionnant **ajouter toocanvas**.</span><span class="sxs-lookup"><span data-stu-id="01353-150">You add a **Get-AutomationCertificate** tooa graphical runbook by right-clicking on hello certificate in hello Library pane of hello graphical editor and selecting **Add toocanvas**.</span></span>

![Ajouter la zone de dessin toohello certificat](media/automation-certificates/automation-certificate-add-to-canvas.png)

<span data-ttu-id="01353-152">Hello image suivante montre un exemple d’utilisation d’un certificat dans un runbook graphique.</span><span class="sxs-lookup"><span data-stu-id="01353-152">hello following image shows an example of using a certificate in a graphical runbook.</span></span>  <span data-ttu-id="01353-153">Il s’agit de hello même exemple ci-dessus pour l’ajout d’un service de cloud de tooa de certificat à partir d’un runbook textuels.</span><span class="sxs-lookup"><span data-stu-id="01353-153">This is hello same example shown above for adding a certificate tooa cloud service from a textual runbook.</span></span>

![<span data-ttu-id="01353-154">Exemple de création graphique</span><span class="sxs-lookup"><span data-stu-id="01353-154">Example Graphical Authoring</span></span> ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a><span data-ttu-id="01353-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="01353-155">Next steps</span></span>

- <span data-ttu-id="01353-156">toolearn plus sur l’utilisation avec des liens toocontrol hello logique un flux d’activités de votre runbook est conçu tooperform, consultez [liens de création graphique](automation-graphical-authoring-intro.md#links-and-workflow).</span><span class="sxs-lookup"><span data-stu-id="01353-156">toolearn more about working with links toocontrol hello logical flow of activities your runbook is designed tooperform, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow).</span></span> 
