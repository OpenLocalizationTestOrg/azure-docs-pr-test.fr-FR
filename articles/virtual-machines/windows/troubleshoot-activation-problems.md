---
title: "Résoudre des problèmes liés à l’activation de machines virtuelles Windows dans Azure | Microsoft Docs"
description: "Indique les étapes de résolution des problèmes relatifs à l’activation de machines virtuelles Windows dans Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 77ef396e0bf75fab56bda2e76516b481d018c5b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a><span data-ttu-id="9b3bb-103">Résoudre des problèmes liés à l’activation de machines virtuelles Windows Azure</span><span class="sxs-lookup"><span data-stu-id="9b3bb-103">Troubleshoot Azure Windows virtual machine activation problems</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="9b3bb-104">Si vous rencontrez des problèmes lors de l’activation de machines virtuelles Windows Azure créées à partir d’une image personnalisée, vous pouvez utiliser les informations disponibles de ce document pour résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-104">If you have trouble when activating Azure Windows virtual machine (VM) that is created from a custom image, you can use the information provided in this document to troubleshoot the issue.</span></span> 

## <a name="symptom"></a><span data-ttu-id="9b3bb-105">Symptôme</span><span class="sxs-lookup"><span data-stu-id="9b3bb-105">Symptom</span></span>

<span data-ttu-id="9b3bb-106">Lorsque vous essayez d’activer une machine virtuelle Windows Azure, vous recevez un message d’erreur semblable à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="9b3bb-106">When you try to activate an Azure Windows VM, you receive an error message resembles the following sample:</span></span>

<span data-ttu-id="9b3bb-107">**Erreur 0xC004F074  : le logiciel LicensingService a signalé que l’ordinateur n’a pas pu être activé. Aucun service de gestion des clés (KMS) n’a pu être contacté. Pour obtenir plus d’informations, veuillez consulter le Journal des événements de l’application.**</span><span class="sxs-lookup"><span data-stu-id="9b3bb-107">**Error: 0xC004F074 The Software LicensingService reported that the computer could not be activated. No Key ManagementService (KMS) could be contacted. Please see the Application Event Log for additional information.**</span></span>

## <a name="cause"></a><span data-ttu-id="9b3bb-108">Cause :</span><span class="sxs-lookup"><span data-stu-id="9b3bb-108">Cause</span></span>
<span data-ttu-id="9b3bb-109">En règle générale, les problèmes d’activation de machines virtuelles Azure se produisent si la machine virtuelle Windows n’est pas configurée à l’aide de la bonne clé d’installation client KMS. Ces problèmes peuvent également survenir si la machine virtuelle Windows rencontre un problème de connectivité au service Azure KMS (kms.core.windows.net, port 1668).</span><span class="sxs-lookup"><span data-stu-id="9b3bb-109">Generally, Azure VM activation issues occur if the Windows VM is not configured by using the appropriate KMS client setup key, or the Windows VM has a connectivity problem to the Azure KMS service (kms.core.windows.net, port 1668).</span></span> 

## <a name="solution"></a><span data-ttu-id="9b3bb-110">Solution</span><span class="sxs-lookup"><span data-stu-id="9b3bb-110">Solution</span></span>

>[!NOTE]
><span data-ttu-id="9b3bb-111">Si vous utilisez un réseau privé virtuel de site à site et un tunneling forcé, consultez l’article [Use Azure custom routes to enable KMS activation with forced tunneling](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx) (Utiliser les itinéraires personnalisés Azure pour permettre l’activation du service de gestion de clés avec un tunneling forcé).</span><span class="sxs-lookup"><span data-stu-id="9b3bb-111">If you are using a site-to-site VPN and forced tunneling, see [Use Azure custom routes to enable KMS activation with forced tunneling](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span></span> 
>
><span data-ttu-id="9b3bb-112">Si vous utilisez le service ExpressRoute et possédez un itinéraire publié par défaut, consultez l’article [Azure VM may fail to activate over ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx) (Une machine virtuelle Azure peut être incapable d’activer ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="9b3bb-112">If you are using ExpressRoute and you have a default route published, see [Azure VM may fail to activate over ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span></span>

### <a name="step-1-configure-the-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a><span data-ttu-id="9b3bb-113">Étape 1 : Configurer la bonne clé d’installation client KMS (pour Windows Server 2016 et Windows Server 2012 R2)</span><span class="sxs-lookup"><span data-stu-id="9b3bb-113">Step 1 Configure the appropriate KMS client setup key (for Windows Server 2016 and Windows Server 2012 R2)</span></span>

<span data-ttu-id="9b3bb-114">Pour la machine virtuelle créée à partir d’une image personnalisée de Windows Server 2016 ou Windows Server 2012 R2, vous devez configurer la clé d’installation client KMS adéquate pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-114">For the VM that is created from a custom image of Windows Server 2016 or Windows Server 2012 R2, you must configure the appropriate KMS client setup key for the VM.</span></span>

<span data-ttu-id="9b3bb-115">Cette étape ne s’applique pas pour Windows 2012 ou Windows 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-115">This step does not apply to Windows 2012 or Windows 2008 R2.</span></span> <span data-ttu-id="9b3bb-116">Elle utilise la fonctionnalité d’activation automatique de machine virtuelle (AVMA). Cette dernière est uniquement prise en charge par Windows Server 2016 et Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-116">It uses the Automation Virtual Machine Activation (AVMA) feature, which is supported only by Windows Server 2016 and Windows Server 2012 R2.</span></span>

1. <span data-ttu-id="9b3bb-117">Exécutez **slmgr.vbs /dlv** dans une invite de commandes avec élévation de privilèges.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-117">Run **slmgr.vbs /dlv** at an elevated command prompt.</span></span> <span data-ttu-id="9b3bb-118">Dans la sortie, vérifiez la valeur Description. Ensuite, déterminez si cette valeur a été créée à partir de la vente au détail (Canal de vente au détail) ou d’un support de licence en volume (VOLUME_KMSCLIENT) :</span><span class="sxs-lookup"><span data-stu-id="9b3bb-118">Check the Description value in the output, and then determine whether it was created from retail (RETAIL channel) or volume (VOLUME_KMSCLIENT) license media:</span></span>
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. <span data-ttu-id="9b3bb-119">Si **slmgr.vbs /dlv**affiche le canal de vente au détail, exécutez les commandes suivantes afin de définir la [clé d’installation client KMS](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) de la version de Windows Server utilisée. Forcez ensuite la tentative d’activation :</span><span class="sxs-lookup"><span data-stu-id="9b3bb-119">If **slmgr.vbs /dlv** shows RETAIL channel, run the following commands to set the [KMS client setup key](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) for the version of Windows Server being used, and force it to retry activation:</span></span> 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    <span data-ttu-id="9b3bb-120">Par exemple, pour Windows Server 2016 Datacenter, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9b3bb-120">For example, for Windows Server 2016 Datacenter, you would run the following command:</span></span>

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-the-connectivity-between-the-vm-and-azure-kms-service"></a><span data-ttu-id="9b3bb-121">Étape 2 : Vérifier la connectivité entre la machine virtuelle et le service Azure KMS</span><span class="sxs-lookup"><span data-stu-id="9b3bb-121">Step 2 Verify the connectivity between the VM and Azure KMS service</span></span>

1. <span data-ttu-id="9b3bb-122">Téléchargez et extrayez l’outil [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) dans un dossier local sur la machine virtuelle qui ne s’active pas.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-122">Download and extract the [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) tool to a local folder in the VM that does not activate.</span></span> 

2. <span data-ttu-id="9b3bb-123">Accédez au menu Démarrer, effectuez une recherche pour Windows PowerShell, cliquez avec le bouton droit sur Windows PowerShell, puis sélectionnez l’option Exécuter en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-123">Go to Start, search on Windows PowerShell, right-click Windows PowerShell, and then select Run as administrator.</span></span>

3. <span data-ttu-id="9b3bb-124">Assurez-vous que la machine virtuelle est configurée pour utiliser le bon serveur Azure KMS.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-124">Make sure that the VM is configured to use the correct Azure KMS server.</span></span> <span data-ttu-id="9b3bb-125">Pour ce faire, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9b3bb-125">To do this, run the following command:</span></span>
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    <span data-ttu-id="9b3bb-126">La commande doit renvoyer le message suivant : le nom de machine de KMS a été configuré sur kms.core.windows.net:1688 avec succès.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-126">The command should return: Key Management Service machine name set to kms.core.windows.net:1688 successfully.</span></span>

4. <span data-ttu-id="9b3bb-127">Vérifiez à l’aide de Psping que vous avez une connexion au serveur KMS.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-127">Verify by using Psping that you have connectivity to the KMS server.</span></span> <span data-ttu-id="9b3bb-128">Basculez vers le dossier où vous avez extrait le téléchargement Pstools.zip, puis exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9b3bb-128">Switch to the folder where you extracted the Pstools.zip download, and then run the following:</span></span>
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  <span data-ttu-id="9b3bb-129">Dans l’avant-dernière ligne de la sortie, assurez-vous que les informations suivantes s’affichent : Envoyé = 4, Reçu = 4, Perdu = 0 (0 % de perte).</span><span class="sxs-lookup"><span data-stu-id="9b3bb-129">In the second-to-last line of the output, make sure that you see: Sent = 4, Received = 4, Lost = 0 (0% loss).</span></span>

  <span data-ttu-id="9b3bb-130">Si la perte est supérieure à 0 (zéro), la machine virtuelle n’a pas de connectivité au serveur KMS.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-130">If Lost is greater than 0 (zero), the VM does not have connectivity to the KMS server.</span></span> <span data-ttu-id="9b3bb-131">Dans ce cas, si la machine virtuelle se trouve au sein d’un réseau virtuel et a spécifié un serveur DNS personnalisé, vérifiez que le serveur DNS est capable de résoudre kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-131">In this situation, if the VM is in a virtual network and has a custom DNS server specified, you must make sure that DNS server is able to resolve kms.core.windows.net.</span></span> <span data-ttu-id="9b3bb-132">Sinon, passez à un serveur DNS capable de résoudre kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-132">Or, change the DNS server to one that does resolve kms.core.windows.net.</span></span>

  <span data-ttu-id="9b3bb-133">Notez que si vous supprimez l’ensemble des serveurs DNS du réseau virtuel, les machines virtuelles utiliseront le service DNS interne d’Azure.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-133">Notice that if you remove all DNS servers from a virtual network, VMs use Azure’s internal DNS service.</span></span> <span data-ttu-id="9b3bb-134">Ce service peut résoudre kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-134">This service can resolve kms.core.windows.net.</span></span>
  
<span data-ttu-id="9b3bb-135">Vérifiez également que le pare-feu invité n’a pas été configuré de manière à bloquer les tentatives d’activation.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-135">Also verify that the guest firewall has not been configured in a manner that would block activation attempts.</span></span>

5. <span data-ttu-id="9b3bb-136">Après avoir vérifié que la connectivité à kms.core.windows.net fonctionne, exécutez la commande suivante dans l’invite Windows PowerShell avec élévation de privilèges.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-136">After you verify successful connectivity to kms.core.windows.net, run the following command at that elevated Windows PowerShell prompt.</span></span> <span data-ttu-id="9b3bb-137">Cette commande tente plusieurs fois l’activation.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-137">This command tries activation multiple times.</span></span>

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

<span data-ttu-id="9b3bb-138">Une activation réussie renvoie des informations qui ressemblent à ceci :</span><span class="sxs-lookup"><span data-stu-id="9b3bb-138">A successful activation returns information that resembles the following:</span></span>

<span data-ttu-id="9b3bb-139">**Activation de Windows(R), édition ServerDatacenter (12345678-1234-1234-1234-12345678)... Le produit a été activé.**</span><span class="sxs-lookup"><span data-stu-id="9b3bb-139">**Activating Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) … Product activated successfully.**</span></span>

## <a name="faq"></a><span data-ttu-id="9b3bb-140">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="9b3bb-140">FAQ</span></span> 

### <a name="i-created-the-windows-server-2016-from-azure-marketplace-do-i-need-to-configure-kms-key-for-activating-the-windows-server-2016"></a><span data-ttu-id="9b3bb-141">J’ai créé l’image Windows Server 2016 à partir de la Place de marché Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-141">I created the Windows Server 2016 from Azure Marketplace.</span></span> <span data-ttu-id="9b3bb-142">Ai-je besoin de configurer la clé KMS pour l’activation de Windows Server 2016 ?</span><span class="sxs-lookup"><span data-stu-id="9b3bb-142">Do I need to configure KMS key for activating the Windows Server 2016?</span></span> 
 
<span data-ttu-id="9b3bb-143">Non.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-143">No.</span></span> <span data-ttu-id="9b3bb-144">Dans la Place de marché Microsoft Azure, l’image contient la bonne clé d’installation client KMS déjà configurée.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-144">The image in Azure Marketplace has the appropriate KMS client setup key already configured.</span></span> 

### <a name="does-windows-activation-work-the-same-way-regardless-if-the-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a><span data-ttu-id="9b3bb-145">L’activation de Windows fonctionne-t-elle de la même façon, peu importe si la machine virtuelle utilise ou non Azure Hybrid Use Benefit (HUB) ?</span><span class="sxs-lookup"><span data-stu-id="9b3bb-145">Does Windows activation work the same way regardless if the VM is using Azure Hybrid Use Benefit (HUB) or not?</span></span> 
 
<span data-ttu-id="9b3bb-146">Oui.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-146">Yes.</span></span> 
 
### <a name="what-happens-if-windows-activation-period-expires"></a><span data-ttu-id="9b3bb-147">Que se passe-t-il en cas d’expiration de la période d’activation de Windows ?</span><span class="sxs-lookup"><span data-stu-id="9b3bb-147">What happens if Windows activation period expires?</span></span> 
 
<span data-ttu-id="9b3bb-148">Lorsque la période de grâce a expiré et si Windows n’est pas encore activé, Windows Server 2008 R2 et versions ultérieures de Windows affichera des notifications supplémentaires sur l’activation.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-148">When the grace period has expired and Windows is still not activated, Windows Server 2008 R2 and later versions of Windows will show additional notifications about activating.</span></span> <span data-ttu-id="9b3bb-149">Le fond d’écran du Bureau reste noir, et Windows Update installera uniquement les mises à jour essentielles et de sécurité. Les mises à jour facultatives ne seront pas installées par Windows Update.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-149">The desktop wallpaper remains black, and Windows Update will install security and critical updates only, but not optional updates.</span></span> <span data-ttu-id="9b3bb-150">Consultez la section Notifications au bas de la page [Licensing Conditions](http://technet.microsoft.com/en-us/library/ff793403.aspx) (Conditions d’obtention de licence).</span><span class="sxs-lookup"><span data-stu-id="9b3bb-150">See  the Notifications section at the bottom of the [Licensing Conditions](http://technet.microsoft.com/en-us/library/ff793403.aspx) page.</span></span>   

## <a name="need-help-contact-support"></a><span data-ttu-id="9b3bb-151">Vous avez besoin d’aide ?</span><span class="sxs-lookup"><span data-stu-id="9b3bb-151">Need help?</span></span> <span data-ttu-id="9b3bb-152">Contactez le support technique.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-152">Contact support.</span></span>
<span data-ttu-id="9b3bb-153">Si vous avez besoin d’aide, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) pour obtenir une prise en charge rapide de votre problème.</span><span class="sxs-lookup"><span data-stu-id="9b3bb-153">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>