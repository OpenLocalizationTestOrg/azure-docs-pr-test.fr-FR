---
title: "problèmes d’activation aaaTroubleshoot Windows machine virtuelle dans Azure | Documents Microsoft"
description: "Fournit des hello résoudre les étapes de résolution des problèmes d’activation de machine virtuelle Windows dans Azure"
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
ms.openlocfilehash: 4ebdac66166e80dcd68cd9e2931b30a29ac01eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a><span data-ttu-id="1e049-103">Résoudre des problèmes liés à l’activation de machines virtuelles Windows Azure</span><span class="sxs-lookup"><span data-stu-id="1e049-103">Troubleshoot Azure Windows virtual machine activation problems</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="1e049-104">Si vous rencontrez des problèmes lors de l’activation d’Azure Windows virtual machine (VM) qui est créé à partir d’une image personnalisée, vous pouvez utiliser les informations de hello fournies dans ce problème de hello tootroubleshoot document.</span><span class="sxs-lookup"><span data-stu-id="1e049-104">If you have trouble when activating Azure Windows virtual machine (VM) that is created from a custom image, you can use hello information provided in this document tootroubleshoot hello issue.</span></span> 

## <a name="symptom"></a><span data-ttu-id="1e049-105">Symptôme</span><span class="sxs-lookup"><span data-stu-id="1e049-105">Symptom</span></span>

<span data-ttu-id="1e049-106">Lorsque vous essayez de tooactivate une machine virtuelle de Windows Azure, vous recevez une erreur hello suivant l’exemple est semblable à :</span><span class="sxs-lookup"><span data-stu-id="1e049-106">When you try tooactivate an Azure Windows VM, you receive an error message resembles hello following sample:</span></span>

<span data-ttu-id="1e049-107">**Erreur : 0xC004F074 hello LicensingService de logiciels a signalé que cet ordinateur hello n’a pas pu être activé. Aucun service de gestion des clés (KMS) n’a pu être contacté. Consultez hello journal des événements pour plus d’informations.**</span><span class="sxs-lookup"><span data-stu-id="1e049-107">**Error: 0xC004F074 hello Software LicensingService reported that hello computer could not be activated. No Key ManagementService (KMS) could be contacted. Please see hello Application Event Log for additional information.**</span></span>

## <a name="cause"></a><span data-ttu-id="1e049-108">Cause :</span><span class="sxs-lookup"><span data-stu-id="1e049-108">Cause</span></span>
<span data-ttu-id="1e049-109">En général, Azure VM activation rencontrer des problèmes si hello machine virtuelle Windows n’est pas configurée par à l’aide de hello clé KMS client le programme d’installation ou hello machine virtuelle Windows possède un toohello de problème de connectivité service Azure KMS (kms.core.windows.net, port 1668).</span><span class="sxs-lookup"><span data-stu-id="1e049-109">Generally, Azure VM activation issues occur if hello Windows VM is not configured by using hello appropriate KMS client setup key, or hello Windows VM has a connectivity problem toohello Azure KMS service (kms.core.windows.net, port 1668).</span></span> 

## <a name="solution"></a><span data-ttu-id="1e049-110">Solution</span><span class="sxs-lookup"><span data-stu-id="1e049-110">Solution</span></span>

>[!NOTE]
><span data-ttu-id="1e049-111">Si vous utilisez un VPN de site à site et forcé de tunneling, consultez [utilisez Azure personnalisée achemine l’activation KMS tooenable avec le tunneling forcé](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e049-111">If you are using a site-to-site VPN and forced tunneling, see [Use Azure custom routes tooenable KMS activation with forced tunneling](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span></span> 
>
><span data-ttu-id="1e049-112">Si vous utilisez ExpressRoute et que vous avez publiée d’un itinéraire par défaut, consultez [machine virtuelle Azure peut basculer tooactivate ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e049-112">If you are using ExpressRoute and you have a default route published, see [Azure VM may fail tooactivate over ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span></span>

### <a name="step-1-configure-hello-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a><span data-ttu-id="1e049-113">Étape 1 configurer hello client le programme d’installation clé KMS (pour Windows Server 2016 et Windows Server 2012 R2)</span><span class="sxs-lookup"><span data-stu-id="1e049-113">Step 1 Configure hello appropriate KMS client setup key (for Windows Server 2016 and Windows Server 2012 R2)</span></span>

<span data-ttu-id="1e049-114">Pour hello machine virtuelle qui est créé à partir d’une image personnalisée de Windows Server 2016 ou Windows Server 2012 R2, vous devez configurer hello client le programme d’installation clé KMS pour hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1e049-114">For hello VM that is created from a custom image of Windows Server 2016 or Windows Server 2012 R2, you must configure hello appropriate KMS client setup key for hello VM.</span></span>

<span data-ttu-id="1e049-115">Cette étape ne s’applique pas tooWindows 2012 ou Windows 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="1e049-115">This step does not apply tooWindows 2012 or Windows 2008 R2.</span></span> <span data-ttu-id="1e049-116">Il utilise la fonctionnalité de l’Activation d’ordinateur virtuel (AVMA) Automation hello, qui est pris en charge uniquement par Windows Server 2016 et Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="1e049-116">It uses hello Automation Virtual Machine Activation (AVMA) feature, which is supported only by Windows Server 2016 and Windows Server 2012 R2.</span></span>

1. <span data-ttu-id="1e049-117">Exécutez **slmgr.vbs /dlv** dans une invite de commandes avec élévation de privilèges.</span><span class="sxs-lookup"><span data-stu-id="1e049-117">Run **slmgr.vbs /dlv** at an elevated command prompt.</span></span> <span data-ttu-id="1e049-118">Vérifiez hello valeur de Description dans la sortie de hello et déterminer si elle a été créée à partir de la vente au détail (canal de vente au détail) ou le support de licence en volume (VOLUME_KMSCLIENT) :</span><span class="sxs-lookup"><span data-stu-id="1e049-118">Check hello Description value in hello output, and then determine whether it was created from retail (RETAIL channel) or volume (VOLUME_KMSCLIENT) license media:</span></span>
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. <span data-ttu-id="1e049-119">Si **slmgr.vbs /dlv** montre le canal de vente au détail, exécutez hello suivant hello tooset de commandes [clé le programme d’installation du client KMS](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) utilisée pour la version de hello de Windows Server et forcer l’activation de tooretry :</span><span class="sxs-lookup"><span data-stu-id="1e049-119">If **slmgr.vbs /dlv** shows RETAIL channel, run hello following commands tooset hello [KMS client setup key](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) for hello version of Windows Server being used, and force it tooretry activation:</span></span> 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    <span data-ttu-id="1e049-120">Par exemple, pour Windows Server Datacenter 2016, vous exécuteriez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1e049-120">For example, for Windows Server 2016 Datacenter, you would run hello following command:</span></span>

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-hello-connectivity-between-hello-vm-and-azure-kms-service"></a><span data-ttu-id="1e049-121">Étape 2 hello Vérifiez la connectivité entre hello machine virtuelle et le service KMS de Azure</span><span class="sxs-lookup"><span data-stu-id="1e049-121">Step 2 Verify hello connectivity between hello VM and Azure KMS service</span></span>

1. <span data-ttu-id="1e049-122">Téléchargez et extrayez hello [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) dossier local de tooa outil Bonjour machine virtuelle qui n’est pas activé.</span><span class="sxs-lookup"><span data-stu-id="1e049-122">Download and extract hello [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) tool tooa local folder in hello VM that does not activate.</span></span> 

2. <span data-ttu-id="1e049-123">Accédez tooStart, effectuez une recherche sur Windows PowerShell, avec le bouton droit de Windows PowerShell, puis sélectionnez Exécuter en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="1e049-123">Go tooStart, search on Windows PowerShell, right-click Windows PowerShell, and then select Run as administrator.</span></span>

3. <span data-ttu-id="1e049-124">Assurez-vous que ce hello que machine virtuelle est configurée toouse hello correcte Azure KMS du serveur.</span><span class="sxs-lookup"><span data-stu-id="1e049-124">Make sure that hello VM is configured toouse hello correct Azure KMS server.</span></span> <span data-ttu-id="1e049-125">toodo cela, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1e049-125">toodo this, run the following command:</span></span>
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    <span data-ttu-id="1e049-126">commande Hello doit retourner : nom d’ordinateur de Service de gestion de clés défini tookms.core.windows.net:1688 avec succès.</span><span class="sxs-lookup"><span data-stu-id="1e049-126">hello command should return: Key Management Service machine name set tookms.core.windows.net:1688 successfully.</span></span>

4. <span data-ttu-id="1e049-127">Vérifier à l’aide de Psping que vous avez connectivité toohello KMS serveur.</span><span class="sxs-lookup"><span data-stu-id="1e049-127">Verify by using Psping that you have connectivity toohello KMS server.</span></span> <span data-ttu-id="1e049-128">Basculez le dossier toohello où vous avez extrait le téléchargement de Pstools.zip hello et puis exécutez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="1e049-128">Switch toohello folder where you extracted hello Pstools.zip download, and then run hello following:</span></span>
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  <span data-ttu-id="1e049-129">Dans la ligne de la dernière seconde hello de sortie de hello, assurez-vous que vous voyez : envoyés = 4, reçus = 4, perdus = 0 (perte 0 %).</span><span class="sxs-lookup"><span data-stu-id="1e049-129">In hello second-to-last line of hello output, make sure that you see: Sent = 4, Received = 4, Lost = 0 (0% loss).</span></span>

  <span data-ttu-id="1e049-130">Si la perte est supérieure à 0 (zéro), hello machine virtuelle n’a pas de serveur de connectivité toohello KMS.</span><span class="sxs-lookup"><span data-stu-id="1e049-130">If Lost is greater than 0 (zero), hello VM does not have connectivity toohello KMS server.</span></span> <span data-ttu-id="1e049-131">Dans ce cas, si hello machine virtuelle est dans un réseau virtuel et spécifié a un serveur DNS personnalisé, vous devez vous assurer que serveur DNS est en mesure de tooresolve kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="1e049-131">In this situation, if hello VM is in a virtual network and has a custom DNS server specified, you must make sure that DNS server is able tooresolve kms.core.windows.net.</span></span> <span data-ttu-id="1e049-132">Ou bien, modifiez hello DNS server tooone qui se résout kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="1e049-132">Or, change hello DNS server tooone that does resolve kms.core.windows.net.</span></span>

  <span data-ttu-id="1e049-133">Notez que si vous supprimez l’ensemble des serveurs DNS du réseau virtuel, les machines virtuelles utiliseront le service DNS interne d’Azure.</span><span class="sxs-lookup"><span data-stu-id="1e049-133">Notice that if you remove all DNS servers from a virtual network, VMs use Azure’s internal DNS service.</span></span> <span data-ttu-id="1e049-134">Ce service peut résoudre kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="1e049-134">This service can resolve kms.core.windows.net.</span></span>
  
<span data-ttu-id="1e049-135">Vérifiez également que le pare-feu hello invité n’a pas été configuré de manière susceptibles de bloquer les tentatives d’activation.</span><span class="sxs-lookup"><span data-stu-id="1e049-135">Also verify that hello guest firewall has not been configured in a manner that would block activation attempts.</span></span>

5. <span data-ttu-id="1e049-136">Après avoir vérifié tookms.core.windows.net de connectivité, exécutez hello suivant de commande à l’invite Windows PowerShell avec élévation de privilèges.</span><span class="sxs-lookup"><span data-stu-id="1e049-136">After you verify successful connectivity tookms.core.windows.net, run hello following command at that elevated Windows PowerShell prompt.</span></span> <span data-ttu-id="1e049-137">Cette commande tente plusieurs fois l’activation.</span><span class="sxs-lookup"><span data-stu-id="1e049-137">This command tries activation multiple times.</span></span>

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

<span data-ttu-id="1e049-138">Une activation réussie retourne des informations semblables hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="1e049-138">A successful activation returns information that resembles hello following:</span></span>

<span data-ttu-id="1e049-139">**Activation de Windows(R), édition ServerDatacenter (12345678-1234-1234-1234-12345678)... Le produit a été activé.**</span><span class="sxs-lookup"><span data-stu-id="1e049-139">**Activating Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) … Product activated successfully.**</span></span>

## <a name="faq"></a><span data-ttu-id="1e049-140">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="1e049-140">FAQ</span></span> 

### <a name="i-created-hello-windows-server-2016-from-azure-marketplace-do-i-need-tooconfigure-kms-key-for-activating-hello-windows-server-2016"></a><span data-ttu-id="1e049-141">J’ai créé hello Windows Server 2016 à partir d’Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1e049-141">I created hello Windows Server 2016 from Azure Marketplace.</span></span> <span data-ttu-id="1e049-142">Dois-je tooconfigure clés d’activation hello Windows Server 2016 ?</span><span class="sxs-lookup"><span data-stu-id="1e049-142">Do I need tooconfigure KMS key for activating hello Windows Server 2016?</span></span> 
 
<span data-ttu-id="1e049-143">Non.</span><span class="sxs-lookup"><span data-stu-id="1e049-143">No.</span></span> <span data-ttu-id="1e049-144">image Hello dans Azure Marketplace a hello client le programme d’installation clé KMS déjà configuré.</span><span class="sxs-lookup"><span data-stu-id="1e049-144">hello image in Azure Marketplace has hello appropriate KMS client setup key already configured.</span></span> 

### <a name="does-windows-activation-work-hello-same-way-regardless-if-hello-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a><span data-ttu-id="1e049-145">Travail d’activation de Windows hello même façon quel que soit si hello machine virtuelle utilise Azure hybride utilisez avantage (HUB) ou non ?</span><span class="sxs-lookup"><span data-stu-id="1e049-145">Does Windows activation work hello same way regardless if hello VM is using Azure Hybrid Use Benefit (HUB) or not?</span></span> 
 
<span data-ttu-id="1e049-146">Oui.</span><span class="sxs-lookup"><span data-stu-id="1e049-146">Yes.</span></span> 
 
### <a name="what-happens-if-windows-activation-period-expires"></a><span data-ttu-id="1e049-147">Que se passe-t-il en cas d’expiration de la période d’activation de Windows ?</span><span class="sxs-lookup"><span data-stu-id="1e049-147">What happens if Windows activation period expires?</span></span> 
 
<span data-ttu-id="1e049-148">Lorsque hello la période de grâce a expiré et si Windows n’est pas encore activé, Windows Server 2008 R2 et versions ultérieures de Windows affichera des notifications supplémentaires sur l’activation.</span><span class="sxs-lookup"><span data-stu-id="1e049-148">When hello grace period has expired and Windows is still not activated, Windows Server 2008 R2 and later versions of Windows will show additional notifications about activating.</span></span> <span data-ttu-id="1e049-149">peint Hello reste noir et mise à jour Windows installera la sécurité et des mises à jour critiques uniquement, mais pas facultatifs mises à jour.</span><span class="sxs-lookup"><span data-stu-id="1e049-149">hello desktop wallpaper remains black, and Windows Update will install security and critical updates only, but not optional updates.</span></span> <span data-ttu-id="1e049-150">Consultez les Notifications de hello section bas hello hello [Conditions de licence](http://technet.microsoft.com/en-us/library/ff793403.aspx) page.</span><span class="sxs-lookup"><span data-stu-id="1e049-150">See  hello Notifications section at hello bottom of hello [Licensing Conditions](http://technet.microsoft.com/en-us/library/ff793403.aspx) page.</span></span>   

## <a name="need-help-contact-support"></a><span data-ttu-id="1e049-151">Vous avez besoin d’aide ?</span><span class="sxs-lookup"><span data-stu-id="1e049-151">Need help?</span></span> <span data-ttu-id="1e049-152">Contactez le support technique.</span><span class="sxs-lookup"><span data-stu-id="1e049-152">Contact support.</span></span>
<span data-ttu-id="1e049-153">Si vous avez besoin d’aide, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget votre problème résolu rapidement.</span><span class="sxs-lookup"><span data-stu-id="1e049-153">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
