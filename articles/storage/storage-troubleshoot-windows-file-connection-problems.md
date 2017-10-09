---
title: "problèmes de stockage de fichier Azure aaaTroubleshoot dans Windows | Documents Microsoft"
description: "Résolution des problèmes liés au stockage Azure File dans Windows"
services: storage
documentationcenter: 
author: genlin
manager: willchen
editor: na
tags: storage
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: genli
ms.openlocfilehash: ba0315d1add76a27fec93a9aee3aa99ccb7fa164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a><span data-ttu-id="03592-103">Résoudre les problèmes liés au stockage Azure File dans Windows</span><span class="sxs-lookup"><span data-stu-id="03592-103">Troubleshoot Azure File storage problems in Windows</span></span>

<span data-ttu-id="03592-104">Cet article répertorie les problèmes courants qui sont associé tooMicrosoft de stockage de fichier Azure lorsque vous vous connectez à partir de clients Windows.</span><span class="sxs-lookup"><span data-stu-id="03592-104">This article lists common problems that are related tooMicrosoft Azure File storage when you connect from Windows clients.</span></span> <span data-ttu-id="03592-105">Il fournit également les causes possibles et les solutions de ces problèmes.</span><span class="sxs-lookup"><span data-stu-id="03592-105">It also provides possible causes and resolutions for these problems.</span></span> <span data-ttu-id="03592-106">En outre des étapes de résolution des problèmes de toohello dans cet article, vous pouvez également utiliser [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) pour vous assurer que Windows hello environnement client a des éléments de configuration.</span><span class="sxs-lookup"><span data-stu-id="03592-106">In addition toohello troubleshooting steps in this article, you can also use [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) to ensure that hello Windows client environment has correct prerequisites.</span></span> <span data-ttu-id="03592-107">AzFileDiagnostics automatise la détection de la plupart des symptômes hello citées dans cet article et permet d’ajouter des performances optimales de tooget votre environnement.</span><span class="sxs-lookup"><span data-stu-id="03592-107">AzFileDiagnostics automates detection of most of hello symptoms mentioned in this article and helps set up your environment tooget optimal performance.</span></span> <span data-ttu-id="03592-108">Vous pouvez également trouver ces informations dans hello [de résolution des problèmes de partages de fichiers de Azure](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) qui fournit les étapes tooassist des problèmes de partages de fichiers Azure de connexion de mappage/montage.</span><span class="sxs-lookup"><span data-stu-id="03592-108">You can also find this information in hello [Azure Files shares Troubleshooter](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) that provides steps tooassist you with problems connecting/mapping/mounting Azure Files shares.</span></span>


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a><span data-ttu-id="03592-109">Les messages « Erreur 53 », « Erreur 67 » ou « Erreur 87 » s’affichent lorsque vous montez ou démontez un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="03592-109">Error 53, Error 67, or Error 87 when you mount or unmount an Azure file share</span></span>

<span data-ttu-id="03592-110">Lorsque vous essayez de toomount un partage de fichiers en local ou à partir d’un autre centre de données, vous pouvez recevoir hello les erreurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="03592-110">When you try toomount a file share from on-premises or from a different datacenter, you might receive hello following errors:</span></span>

- <span data-ttu-id="03592-111">Erreur système 53.</span><span class="sxs-lookup"><span data-stu-id="03592-111">System error 53 has occurred.</span></span> <span data-ttu-id="03592-112">chemin d’accès réseau de Hello est introuvable.</span><span class="sxs-lookup"><span data-stu-id="03592-112">hello network path was not found.</span></span>
- <span data-ttu-id="03592-113">Erreur système 67.</span><span class="sxs-lookup"><span data-stu-id="03592-113">System error 67 has occurred.</span></span> <span data-ttu-id="03592-114">Impossible de trouver le nom de réseau Hello.</span><span class="sxs-lookup"><span data-stu-id="03592-114">hello network name cannot be found.</span></span>
- <span data-ttu-id="03592-115">Erreur système 87.</span><span class="sxs-lookup"><span data-stu-id="03592-115">System error 87 has occurred.</span></span> <span data-ttu-id="03592-116">le paramètre Hello est incorrect.</span><span class="sxs-lookup"><span data-stu-id="03592-116">hello parameter is incorrect.</span></span>

### <a name="cause-1-unencrypted-communication-channel"></a><span data-ttu-id="03592-117">Cause 1 : Canal de communication non chiffrée</span><span class="sxs-lookup"><span data-stu-id="03592-117">Cause 1: Unencrypted communication channel</span></span>

<span data-ttu-id="03592-118">Pour des raisons de sécurité, les partages de fichiers tooAzure sont bloquées si le canal de communication hello n’est pas chiffré, et si la tentative de connexion de hello n’est pas effectuée à partir de connexions hello même centre de données où résident les partages de fichiers Azure hello.</span><span class="sxs-lookup"><span data-stu-id="03592-118">For security reasons, connections tooAzure file shares are blocked if hello communication channel isn’t encrypted and if hello connection attempt isn't made from hello same datacenter where hello Azure file shares reside.</span></span> <span data-ttu-id="03592-119">Chiffrement de canal de communication est fourni uniquement si hello client de l’utilisateur du système d’exploitation prend en charge le chiffrement SMB.</span><span class="sxs-lookup"><span data-stu-id="03592-119">Communication channel encryption is provided only if hello user’s client OS supports SMB encryption.</span></span>

<span data-ttu-id="03592-120">Windows 8, Windows Server 2012 et les versions ultérieures de chaque demande de négociation système incluant SMB 3.0, prenant en charge le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="03592-120">Windows 8, Windows Server 2012, and later versions of each system negotiate requests that include SMB 3.0, which supports encryption.</span></span>

### <a name="solution-for-cause-1"></a><span data-ttu-id="03592-121">Solution pour la cause 1</span><span class="sxs-lookup"><span data-stu-id="03592-121">Solution for cause 1</span></span>

<span data-ttu-id="03592-122">Se connecter à partir d’un client qui effectue hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="03592-122">Connect from a client that does one of hello following:</span></span>

- <span data-ttu-id="03592-123">Répond aux exigences de hello de Windows 8 et Windows Server 2012 ou versions ultérieures</span><span class="sxs-lookup"><span data-stu-id="03592-123">Meets hello requirements of Windows 8 and Windows Server 2012 or later versions</span></span>
- <span data-ttu-id="03592-124">Se connecte à partir d’une machine virtuelle dans hello même centre de données comme compte de stockage Azure qui est utilisé pour le partage de fichiers Azure hello de hello</span><span class="sxs-lookup"><span data-stu-id="03592-124">Connects from a virtual machine in hello same datacenter as hello Azure storage account that is used for hello Azure file share</span></span>

### <a name="cause-2-port-445-is-blocked"></a><span data-ttu-id="03592-125">Cause 2 : Le Port 445 est bloqué</span><span class="sxs-lookup"><span data-stu-id="03592-125">Cause 2: Port 445 is blocked</span></span>

<span data-ttu-id="03592-126">Erreur système 53 ou l’erreur système 67 peut se produire si le port 445 les communications sortantes tooan fichier Azure stockage centre de données est bloquée.</span><span class="sxs-lookup"><span data-stu-id="03592-126">System error 53 or system error 67 can occur if port 445 outbound communication tooan Azure File storage datacenter is blocked.</span></span> <span data-ttu-id="03592-127">Résumé de hello toosee de fournisseurs de services Internet autoriser ou interdire l’accès à partir du port 445, accédez trop[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span><span class="sxs-lookup"><span data-stu-id="03592-127">toosee hello summary of ISPs that allow or disallow access from port 445, go too[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span></span>

<span data-ttu-id="03592-128">toounderstand s’il s’agit du message « Erreur système 53 » hello raison hello, vous pouvez utiliser le point de terminaison TCP:445 Portqry tooquery hello.</span><span class="sxs-lookup"><span data-stu-id="03592-128">toounderstand whether this is hello reason behind hello "System error 53" message, you can use Portqry tooquery hello TCP:445 endpoint.</span></span> <span data-ttu-id="03592-129">Si le point de terminaison TCP:445 hello est affiché comme filtrés, hello le port TCP est bloqué.</span><span class="sxs-lookup"><span data-stu-id="03592-129">If hello TCP:445 endpoint is displayed as filtered, hello TCP port is blocked.</span></span> <span data-ttu-id="03592-130">Voici un exemple de requête :</span><span class="sxs-lookup"><span data-stu-id="03592-130">Here is an example query:</span></span>

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

<span data-ttu-id="03592-131">Si le port TCP 445 est bloqué par une règle de chemin d’accès réseau de hello, vous verrez hello suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="03592-131">If TCP port 445 is blocked by a rule along hello network path, you will see hello following output:</span></span>

  `TCP port 445 (microsoft-ds service): FILTERED`

<span data-ttu-id="03592-132">Pour plus d’informations sur la façon toouse Portqry, consultez [Description de l’utilitaire de ligne de commande Portqry.exe hello](https://support.microsoft.com/help/310099).</span><span class="sxs-lookup"><span data-stu-id="03592-132">For more information about how toouse Portqry, see [Description of hello Portqry.exe command-line utility](https://support.microsoft.com/help/310099).</span></span>

### <a name="solution-for-cause-2"></a><span data-ttu-id="03592-133">Solution pour la cause 2</span><span class="sxs-lookup"><span data-stu-id="03592-133">Solution for cause 2</span></span>

<span data-ttu-id="03592-134">Fonctionne avec votre service informatique service tooopen le port 445 sortant trop[plages d’adresses IP de Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="03592-134">Work with your IT department tooopen port 445 outbound too[Azure IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="cause-3-ntlmv1-is-enabled"></a><span data-ttu-id="03592-135">Cause 3 : NTLMv1 est activé</span><span class="sxs-lookup"><span data-stu-id="03592-135">Cause 3: NTLMv1 is enabled</span></span>

<span data-ttu-id="03592-136">Erreur système 53 ou erreur 87 du système peut se produire si la communication NTLMv1 est activée sur le client de hello.</span><span class="sxs-lookup"><span data-stu-id="03592-136">System error 53 or system error 87 can occur if NTLMv1 communication is enabled on hello client.</span></span> <span data-ttu-id="03592-137">Le stockage Azure File prend uniquement en charge l’authentification NTLMv2.</span><span class="sxs-lookup"><span data-stu-id="03592-137">Azure File storage supports only NTLMv2 authentication.</span></span> <span data-ttu-id="03592-138">Le fait d’activer NTLMv1 crée un client moins sécurisé.</span><span class="sxs-lookup"><span data-stu-id="03592-138">Having NTLMv1 enabled creates a less-secure client.</span></span> <span data-ttu-id="03592-139">Par conséquent, les communications sont bloquées pour le stockage Azure File.</span><span class="sxs-lookup"><span data-stu-id="03592-139">Therefore, communication is blocked for Azure File storage.</span></span> 

<span data-ttu-id="03592-140">toodetermine s’il s’agit de cause hello d’erreur de hello, vérifiez que hello suivant la sous-clé de Registre est définie la valeur tooa 3 :</span><span class="sxs-lookup"><span data-stu-id="03592-140">toodetermine whether this is hello cause of hello error, verify that hello following registry subkey is set tooa value of 3:</span></span>

<span data-ttu-id="03592-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa &gt; LmCompatibilityLevel**</span><span class="sxs-lookup"><span data-stu-id="03592-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span></span>

<span data-ttu-id="03592-142">Pour plus d’informations, consultez hello [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) rubrique sur TechNet.</span><span class="sxs-lookup"><span data-stu-id="03592-142">For more information, see hello [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) topic on TechNet.</span></span>

### <a name="solution-for-cause-3"></a><span data-ttu-id="03592-143">Solution pour la cause 3</span><span class="sxs-lookup"><span data-stu-id="03592-143">Solution for cause 3</span></span>

<span data-ttu-id="03592-144">Rétablir hello **LmCompatibilityLevel** valeur par défaut toohello 3 Bonjour suivant la sous-clé de Registre :</span><span class="sxs-lookup"><span data-stu-id="03592-144">Revert hello **LmCompatibilityLevel** value toohello default value of 3 in hello following registry subkey:</span></span>

  <span data-ttu-id="03592-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span><span class="sxs-lookup"><span data-stu-id="03592-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span></span>

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-tooprocess-this-command-when-you-copy-tooan-azure-file-share"></a><span data-ttu-id="03592-146">Erreur 1816 « pas de suffisamment de quota est disponible tooprocess cette commande » lorsque vous copiez le partage de fichiers Azure tooan</span><span class="sxs-lookup"><span data-stu-id="03592-146">Error 1816 “Not enough quota is available tooprocess this command” when you copy tooan Azure file share</span></span>

### <a name="cause"></a><span data-ttu-id="03592-147">Cause :</span><span class="sxs-lookup"><span data-stu-id="03592-147">Cause</span></span>

<span data-ttu-id="03592-148">Erreur 1816 se produit lorsque vous atteignez la limite supérieure de hello de handles ouverts simultanées autorisées pour un fichier sur l’ordinateur de hello où le partage de fichiers hello est en cours monté.</span><span class="sxs-lookup"><span data-stu-id="03592-148">Error 1816 happens when you reach hello upper limit of concurrent open handles that are allowed for a file on hello computer where hello file share is being mounted.</span></span>

### <a name="solution"></a><span data-ttu-id="03592-149">Solution</span><span class="sxs-lookup"><span data-stu-id="03592-149">Solution</span></span>

<span data-ttu-id="03592-150">Réduire le nombre hello de handles ouverts simultanées en fermant certaines poignées, puis recommencez.</span><span class="sxs-lookup"><span data-stu-id="03592-150">Reduce hello number of concurrent open handles by closing some handles, and then retry.</span></span> <span data-ttu-id="03592-151">Pour plus d’informations, consultez [Liste de contrôle des performances et de l’extensibilité de Microsoft Azure Storage](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="03592-151">For more information, see [Microsoft Azure Storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-windows"></a><span data-ttu-id="03592-152">Fichier lente copie tooand à partir du stockage Windows Azure File</span><span class="sxs-lookup"><span data-stu-id="03592-152">Slow file copying tooand from Azure File storage in Windows</span></span>

<span data-ttu-id="03592-153">Vous pouvez voir le ralentissement des performances lorsque vous essayez de tootransfer toohello de fichiers Azure File service.</span><span class="sxs-lookup"><span data-stu-id="03592-153">You might see slow performance when you try tootransfer files toohello Azure File service.</span></span>

- <span data-ttu-id="03592-154">Si vous n’avez pas une exigence de taille d’e/s minimale spécifique, nous recommandons d’utiliser 1 Mo comme hello taille d’e/s pour des performances optimales.</span><span class="sxs-lookup"><span data-stu-id="03592-154">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as hello I/O size for optimal performance.</span></span>
-   <span data-ttu-id="03592-155">Si vous connaissez taille finale de hello d’un fichier que vous étendez avec écrit et votre logiciel n’a pas des problèmes de compatibilité lorsque hello non écrit la fin du fichier de hello contient des zéros non significatifs, puis ensemble hello taille de fichier à l’avance, au lieu d’effectuer chaque écriture une écriture d’extension.</span><span class="sxs-lookup"><span data-stu-id="03592-155">If you know hello final size of a file that you are extending with writes, and your software doesn’t have compatibility problems when hello unwritten tail on hello file contains zeros, then set hello file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="03592-156">Utilisez hello droite copy (méthode) :</span><span class="sxs-lookup"><span data-stu-id="03592-156">Use hello right copy method:</span></span>
    -   <span data-ttu-id="03592-157">Utilisez [AZCopy](storage-use-azcopy.md#file-copy) pour les transferts entre deux partages de fichiers.</span><span class="sxs-lookup"><span data-stu-id="03592-157">Use [AzCopy](storage-use-azcopy.md#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="03592-158">Utilisez [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) entre des partages de fichiers sur un ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="03592-158">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a><span data-ttu-id="03592-159">Informations pour Windows 8.1 ou Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="03592-159">Considerations for Windows 8.1 or Windows Server 2012 R2</span></span>

<span data-ttu-id="03592-160">Pour les clients qui exécutent Windows 8.1 ou Windows Server 2012 R2, assurez-vous que ce hello [KB3114025](https://support.microsoft.com/help/3114025) correctif logiciel est installé.</span><span class="sxs-lookup"><span data-stu-id="03592-160">For clients that are running Windows 8.1 or Windows Server 2012 R2, make sure that hello [KB3114025](https://support.microsoft.com/help/3114025) hotfix is installed.</span></span> <span data-ttu-id="03592-161">Ce correctif logiciel améliore les performances de hello de créer et fermer des descripteurs.</span><span class="sxs-lookup"><span data-stu-id="03592-161">This hotfix improves hello performance of create and close handles.</span></span>

<span data-ttu-id="03592-162">Vous pouvez exécuter hello suivant toocheck de script si hello correctif a été installé :</span><span class="sxs-lookup"><span data-stu-id="03592-162">You can run hello following script toocheck whether hello hotfix has been installed:</span></span>

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

<span data-ttu-id="03592-163">Si le correctif est installé, hello sortie suivante s’affiche :</span><span class="sxs-lookup"><span data-stu-id="03592-163">If hotfix is installed, hello following output is displayed:</span></span>

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> <span data-ttu-id="03592-164">Les images de Windows Server 2012 R2 dans Azure Marketplace ont le correctif logiciel KB3114025 installé par défaut à compter de décembre 2015.</span><span class="sxs-lookup"><span data-stu-id="03592-164">Windows Server 2012 R2 images in Azure Marketplace have hotfix KB3114025 installed by default, starting in December 2015.</span></span>

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a><span data-ttu-id="03592-165">Aucun dossier avec une lettre de lecteur dans **Poste de travail**</span><span class="sxs-lookup"><span data-stu-id="03592-165">No folder with a drive letter in **My Computer**</span></span>

<span data-ttu-id="03592-166">Si vous mappez un partage de fichiers Azure en tant qu’administrateur à l’aide de nette utilisation, le partage de hello apparaît toobe manquant.</span><span class="sxs-lookup"><span data-stu-id="03592-166">If you map an Azure file share as an administrator by using net use, hello share appears toobe missing.</span></span>

### <a name="cause"></a><span data-ttu-id="03592-167">Cause :</span><span class="sxs-lookup"><span data-stu-id="03592-167">Cause</span></span>

<span data-ttu-id="03592-168">Par défaut, l’Explorateur Windows ne s’exécute pas en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="03592-168">By default, Windows File Explorer does not run as an administrator.</span></span> <span data-ttu-id="03592-169">Si vous exécutez l’utilisation de nette à partir d’une invite de commandes d’administration, vous mappez un lecteur réseau hello en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="03592-169">If you run net use from an administrative command prompt, you map hello network drive as an administrator.</span></span> <span data-ttu-id="03592-170">Étant donné que les lecteurs mappés sont centrées sur l’utilisateur, compte d’utilisateur hello est enregistré dans n’affiche pas hello lecteurs s’ils sont montés sous un compte d’utilisateur différent.</span><span class="sxs-lookup"><span data-stu-id="03592-170">Because mapped drives are user-centric, hello user account that is logged in does not display hello drives if they are mounted under a different user account.</span></span>

### <a name="solution"></a><span data-ttu-id="03592-171">Solution</span><span class="sxs-lookup"><span data-stu-id="03592-171">Solution</span></span>
<span data-ttu-id="03592-172">Montez hello partage à partir d’une ligne de commande non administrateur.</span><span class="sxs-lookup"><span data-stu-id="03592-172">Mount hello share from a non-administrator command line.</span></span> <span data-ttu-id="03592-173">Vous pouvez également suivre [cette rubrique TechNet](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** valeur de Registre.</span><span class="sxs-lookup"><span data-stu-id="03592-173">Alternatively, you can follow [this TechNet topic](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** registry value.</span></span>

<a id="netuse"></a>
## <a name="net-use-command-fails-if-hello-storage-account-contains-a-forward-slash"></a><span data-ttu-id="03592-174">Commande net use échoue si le compte de stockage hello contient une barre oblique</span><span class="sxs-lookup"><span data-stu-id="03592-174">Net use command fails if hello storage account contains a forward slash</span></span>

### <a name="cause"></a><span data-ttu-id="03592-175">Cause :</span><span class="sxs-lookup"><span data-stu-id="03592-175">Cause</span></span>

<span data-ttu-id="03592-176">commande net use de Hello interprète une barre oblique (/) comme option de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="03592-176">hello net use command interprets a forward slash (/) as a command-line option.</span></span> <span data-ttu-id="03592-177">Si le nom de votre compte d’utilisateur commence par une barre oblique, mappage de lecteur hello échoue.</span><span class="sxs-lookup"><span data-stu-id="03592-177">If your user account name starts with a forward slash, hello drive mapping fails.</span></span>

### <a name="solution"></a><span data-ttu-id="03592-178">Solution</span><span class="sxs-lookup"><span data-stu-id="03592-178">Solution</span></span>

<span data-ttu-id="03592-179">Vous pouvez utiliser une des hello suivant toowork étapes contourner problème de hello :</span><span class="sxs-lookup"><span data-stu-id="03592-179">You can use either of hello following steps toowork around hello problem:</span></span>

- <span data-ttu-id="03592-180">Exécutez hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="03592-180">Run hello following PowerShell command:</span></span>

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  <span data-ttu-id="03592-181">À partir d’un fichier de commandes, vous pouvez exécuter commande hello de cette façon :</span><span class="sxs-lookup"><span data-stu-id="03592-181">From a batch file, you can run hello command this way:</span></span>

  `Echo new-smbMapping ... | powershell -command –`

- <span data-ttu-id="03592-182">Placez entre guillemets doubles hello de clé toowork résoudre ce problème, à moins que la barre oblique hello est le premier caractère de hello.</span><span class="sxs-lookup"><span data-stu-id="03592-182">Put double quotation marks around hello key toowork around this problem--unless hello forward slash is hello first character.</span></span> <span data-ttu-id="03592-183">S’il s’agit, utilisez le mode interactif hello et entrez votre mot de passe séparément ou régénérer vos clés de tooget une clé qui ne commence pas par une barre oblique.</span><span class="sxs-lookup"><span data-stu-id="03592-183">If it is, either use hello interactive mode and enter your password separately or regenerate your keys tooget a key that doesn't start with a forward slash.</span></span>

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a><span data-ttu-id="03592-184">L’application ou service ne peut pas accéder à un lecteur monté de stockage Azure File</span><span class="sxs-lookup"><span data-stu-id="03592-184">Application or service cannot access a mounted Azure File storage drive</span></span>

### <a name="cause"></a><span data-ttu-id="03592-185">Cause :</span><span class="sxs-lookup"><span data-stu-id="03592-185">Cause</span></span>

<span data-ttu-id="03592-186">Les lecteurs sont montés par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="03592-186">Drives are mounted per user.</span></span> <span data-ttu-id="03592-187">Si votre application ou service s’exécute sous un compte d’utilisateur différent hello qui hello lecteur monté, application hello ne verrez pas le lecteur de hello.</span><span class="sxs-lookup"><span data-stu-id="03592-187">If your application or service is running under a different user account than hello one that mounted hello drive, hello application will not see hello drive.</span></span>

### <a name="solution"></a><span data-ttu-id="03592-188">Solution</span><span class="sxs-lookup"><span data-stu-id="03592-188">Solution</span></span>

<span data-ttu-id="03592-189">Utilisez une des hello suivant solutions :</span><span class="sxs-lookup"><span data-stu-id="03592-189">Use one of hello following solutions:</span></span>

-   <span data-ttu-id="03592-190">Monter le lecteur de hello de hello même compte d’utilisateur qui contient l’application hello.</span><span class="sxs-lookup"><span data-stu-id="03592-190">Mount hello drive from hello same user account that contains hello application.</span></span> <span data-ttu-id="03592-191">Vous pouvez utiliser un outil tel que PsExec.</span><span class="sxs-lookup"><span data-stu-id="03592-191">You can use a tool such as PsExec.</span></span>
- <span data-ttu-id="03592-192">Passer le nom de compte de stockage hello et la clé des paramètres de nom et mot de passe d’utilisateur de la commande net use de hello hello.</span><span class="sxs-lookup"><span data-stu-id="03592-192">Pass hello storage account name and key in hello user name and password parameters of hello net use command.</span></span>

<span data-ttu-id="03592-193">Après avoir suivi ces instructions, vous pouvez recevoir hello message d’erreur suivant lorsque vous exécutez nette utilisation pour le compte de service réseau ou de systèmes hello : « erreur du système 1312 s’est produite.</span><span class="sxs-lookup"><span data-stu-id="03592-193">After you follow these instructions, you might receive hello following error message when you run net use for hello system/network service account: "System error 1312 has occurred.</span></span> <span data-ttu-id="03592-194">Une session ouverte spécifiée n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="03592-194">A specified logon session does not exist.</span></span> <span data-ttu-id="03592-195">Il se peut qu’elle ait été déjà fermée. »</span><span class="sxs-lookup"><span data-stu-id="03592-195">It may already have been terminated."</span></span> <span data-ttu-id="03592-196">Si cela se produit, assurez-vous que ce nom d’utilisateur de hello est passé toonet utilisation inclut des informations de domaine (par exemple : « [nom du compte de stockage]. file.core.windows .net »).</span><span class="sxs-lookup"><span data-stu-id="03592-196">If this occurs, make sure that hello username that is passed toonet use includes domain information (for example: "[storage account name].file.core.windows.net").</span></span>

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-tooa-destination-that-does-not-support-encryption"></a><span data-ttu-id="03592-197">Erreur « Vous copiez une destination de tooa de fichier qui ne prend pas en charge le chiffrement »</span><span class="sxs-lookup"><span data-stu-id="03592-197">Error "You are copying a file tooa destination that does not support encryption"</span></span>

<span data-ttu-id="03592-198">Lorsqu’un fichier est copié sur le réseau de hello, hello est déchiffrée sur ordinateur source de hello, transmis en texte brut, puis de nouveau chiffrée à la destination de hello.</span><span class="sxs-lookup"><span data-stu-id="03592-198">When a file is copied over hello network, hello file is decrypted on hello source computer, transmitted in plaintext, and re-encrypted at hello destination.</span></span> <span data-ttu-id="03592-199">Toutefois, vous pouvez voir l’erreur suivante lorsque vous essayez de toocopy un fichier chiffré de hello : «, vous copiez hello fichier tooa destination qui ne prend pas en charge le chiffrement. »</span><span class="sxs-lookup"><span data-stu-id="03592-199">However, you might see hello following error when you're trying toocopy an encrypted file: "You are copying hello file tooa destination that does not support encryption."</span></span>

### <a name="cause"></a><span data-ttu-id="03592-200">Cause :</span><span class="sxs-lookup"><span data-stu-id="03592-200">Cause</span></span>
<span data-ttu-id="03592-201">Ce problème peut se survenir si vous utilisez le système de fichiers EFS (Encrypting File System).</span><span class="sxs-lookup"><span data-stu-id="03592-201">This problem can occur if you are using Encrypting File System (EFS).</span></span> <span data-ttu-id="03592-202">Les fichiers chiffrés par BitLocker peuvent être copié tooAzure le stockage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="03592-202">BitLocker-encrypted files can be copied tooAzure File storage.</span></span> <span data-ttu-id="03592-203">Toutefois, le stockage Azure File ne prend pas en charge le système de fichiers EFS NTFS.</span><span class="sxs-lookup"><span data-stu-id="03592-203">However, Azure File storage does not support NTFS EFS.</span></span>

### <a name="workaround"></a><span data-ttu-id="03592-204">Solution de contournement</span><span class="sxs-lookup"><span data-stu-id="03592-204">Workaround</span></span>
<span data-ttu-id="03592-205">toocopy un fichier réseau hello, vous devez tout d’abord le déchiffrer.</span><span class="sxs-lookup"><span data-stu-id="03592-205">toocopy a file over hello network, you must first decrypt it.</span></span> <span data-ttu-id="03592-206">Utilisez une des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="03592-206">Use one of hello following methods:</span></span>

- <span data-ttu-id="03592-207">Hello d’utilisation **copier /d** commande.</span><span class="sxs-lookup"><span data-stu-id="03592-207">Use hello **copy /d** command.</span></span> <span data-ttu-id="03592-208">Il permet de hello chiffré fichiers toobe enregistré en tant que fichiers déchiffrés à la destination de hello.</span><span class="sxs-lookup"><span data-stu-id="03592-208">It allows hello encrypted files toobe saved as decrypted files at hello destination.</span></span>
- <span data-ttu-id="03592-209">Hello du jeu de clé de Registre suivante :</span><span class="sxs-lookup"><span data-stu-id="03592-209">Set hello following registry key:</span></span>
  - <span data-ttu-id="03592-210">Chemin d’accès = HKLM\Software\Policies\Microsoft\Windows\System</span><span class="sxs-lookup"><span data-stu-id="03592-210">Path = HKLM\Software\Policies\Microsoft\Windows\System</span></span>
  - <span data-ttu-id="03592-211">Type de valeur = DWORD</span><span class="sxs-lookup"><span data-stu-id="03592-211">Value type = DWORD</span></span>
  - <span data-ttu-id="03592-212">Nom = CopyFileAllowDecryptedRemoteDestination</span><span class="sxs-lookup"><span data-stu-id="03592-212">Name = CopyFileAllowDecryptedRemoteDestination</span></span>
  - <span data-ttu-id="03592-213">Valeur = 1</span><span class="sxs-lookup"><span data-stu-id="03592-213">Value = 1</span></span>

<span data-ttu-id="03592-214">N’oubliez pas de que clé de Registre paramètre hello affecte toutes les opérations de copie sont effectuées toonetwork partages.</span><span class="sxs-lookup"><span data-stu-id="03592-214">Be aware that setting hello registry key affects all copy operations that are made toonetwork shares.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="03592-215">Vous avez besoin d’aide ?</span><span class="sxs-lookup"><span data-stu-id="03592-215">Need help?</span></span> <span data-ttu-id="03592-216">Contactez le support technique.</span><span class="sxs-lookup"><span data-stu-id="03592-216">Contact support.</span></span>
<span data-ttu-id="03592-217">Si vous avez besoin d’aide, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget votre problème résolu rapidement.</span><span class="sxs-lookup"><span data-stu-id="03592-217">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your problem resolved quickly.</span></span>
