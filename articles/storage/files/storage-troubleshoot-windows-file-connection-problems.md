---
title: "Résoudre les problèmes liés au stockage Azure File dans Windows | Microsoft Docs"
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
ms.openlocfilehash: daaf7d0589f5e2d82b43dad879bffd23370a2c81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a><span data-ttu-id="6b60a-103">Résoudre les problèmes liés au stockage Azure File dans Windows</span><span class="sxs-lookup"><span data-stu-id="6b60a-103">Troubleshoot Azure File storage problems in Windows</span></span>

<span data-ttu-id="6b60a-104">Cet article répertorie les problèmes courants liés au stockage Microsoft Azure File lorsque vous vous connectez à partir des clients Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="6b60a-104">This article lists common problems that are related to Microsoft Azure File storage when you connect from Windows clients.</span></span> <span data-ttu-id="6b60a-105">Il fournit également les causes possibles et les solutions de ces problèmes.</span><span class="sxs-lookup"><span data-stu-id="6b60a-105">It also provides possible causes and resolutions for these problems.</span></span> <span data-ttu-id="6b60a-106">En plus des étapes de résolutions présentées dans cet article, vous pouvez aussi utiliser [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) pour être sûr que l’environnement du client Windows est configuré correctement.</span><span class="sxs-lookup"><span data-stu-id="6b60a-106">In addition to the troubleshooting steps in this article, you can also use [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) to ensure that the Windows client environment has correct prerequisites.</span></span> <span data-ttu-id="6b60a-107">AzFileDiagnostics détecte automatiquement la plupart des problèmes mentionnés dans cet article et vous aide à configurer votre environnement pour que les performances soient optimales.</span><span class="sxs-lookup"><span data-stu-id="6b60a-107">AzFileDiagnostics automates detection of most of the symptoms mentioned in this article and helps set up your environment to get optimal performance.</span></span> <span data-ttu-id="6b60a-108">Vous pouvez également trouver ces informations dans [l’utilitaire de résolution des problèmes de partages Azure Files](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares), qui indique la procédure à suivre pour vous aider en cas de problèmes de connexion/mappage/montage de partages Azure Files.</span><span class="sxs-lookup"><span data-stu-id="6b60a-108">You can also find this information in the [Azure Files shares Troubleshooter](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) that provides steps to assist you with problems connecting/mapping/mounting Azure Files shares.</span></span>


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a><span data-ttu-id="6b60a-109">Les messages « Erreur 53 », « Erreur 67 » ou « Erreur 87 » s’affichent lorsque vous montez ou démontez un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="6b60a-109">Error 53, Error 67, or Error 87 when you mount or unmount an Azure file share</span></span>

<span data-ttu-id="6b60a-110">Lorsque vous essayez de monter un partage de fichiers depuis un centre de données local ou un centre de données différent, les erreurs suivantes pourraient survenir :</span><span class="sxs-lookup"><span data-stu-id="6b60a-110">When you try to mount a file share from on-premises or from a different datacenter, you might receive the following errors:</span></span>

- <span data-ttu-id="6b60a-111">Erreur système 53.</span><span class="sxs-lookup"><span data-stu-id="6b60a-111">System error 53 has occurred.</span></span> <span data-ttu-id="6b60a-112">Le chemin d’accès réseau est introuvable.</span><span class="sxs-lookup"><span data-stu-id="6b60a-112">The network path was not found.</span></span>
- <span data-ttu-id="6b60a-113">Erreur système 67.</span><span class="sxs-lookup"><span data-stu-id="6b60a-113">System error 67 has occurred.</span></span> <span data-ttu-id="6b60a-114">Le nom du réseau est introuvable.</span><span class="sxs-lookup"><span data-stu-id="6b60a-114">The network name cannot be found.</span></span>
- <span data-ttu-id="6b60a-115">Erreur système 87.</span><span class="sxs-lookup"><span data-stu-id="6b60a-115">System error 87 has occurred.</span></span> <span data-ttu-id="6b60a-116">Le paramètre est incorrect.</span><span class="sxs-lookup"><span data-stu-id="6b60a-116">The parameter is incorrect.</span></span>

### <a name="cause-1-unencrypted-communication-channel"></a><span data-ttu-id="6b60a-117">Cause 1 : Canal de communication non chiffrée</span><span class="sxs-lookup"><span data-stu-id="6b60a-117">Cause 1: Unencrypted communication channel</span></span>

<span data-ttu-id="6b60a-118">Pour des raisons de sécurité, les connexions aux partages de fichiers Azure sont bloquées si le canal de communication n’est pas chiffré et si la tentative de connexion n’est pas effectuée depuis le centre de données sur lequel résident les partages de fichiers Azure.</span><span class="sxs-lookup"><span data-stu-id="6b60a-118">For security reasons, connections to Azure file shares are blocked if the communication channel isn’t encrypted and if the connection attempt isn't made from the same datacenter where the Azure file shares reside.</span></span> <span data-ttu-id="6b60a-119">Le chiffrement du canal de communication n’est fourni que si le système d’exploitation client de l’utilisateur prend en charge le chiffrement SMB.</span><span class="sxs-lookup"><span data-stu-id="6b60a-119">Communication channel encryption is provided only if the user’s client OS supports SMB encryption.</span></span>

<span data-ttu-id="6b60a-120">Windows 8, Windows Server 2012 et les versions ultérieures de chaque demande de négociation système incluant SMB 3.0, prenant en charge le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="6b60a-120">Windows 8, Windows Server 2012, and later versions of each system negotiate requests that include SMB 3.0, which supports encryption.</span></span>

### <a name="solution-for-cause-1"></a><span data-ttu-id="6b60a-121">Solution pour la cause 1</span><span class="sxs-lookup"><span data-stu-id="6b60a-121">Solution for cause 1</span></span>

<span data-ttu-id="6b60a-122">Connectez-vous depuis un client qui :</span><span class="sxs-lookup"><span data-stu-id="6b60a-122">Connect from a client that does one of the following:</span></span>

- <span data-ttu-id="6b60a-123">Dispose de la configuration requise de Windows 8 et Windows Server 2012 ou versions ultérieures</span><span class="sxs-lookup"><span data-stu-id="6b60a-123">Meets the requirements of Windows 8 and Windows Server 2012 or later versions</span></span>
- <span data-ttu-id="6b60a-124">Se connecte depuis une machine virtuelle située dans le même centre de données que le compte de stockage Azure utilisé pour le partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="6b60a-124">Connects from a virtual machine in the same datacenter as the Azure storage account that is used for the Azure file share</span></span>

### <a name="cause-2-port-445-is-blocked"></a><span data-ttu-id="6b60a-125">Cause 2 : Le Port 445 est bloqué</span><span class="sxs-lookup"><span data-stu-id="6b60a-125">Cause 2: Port 445 is blocked</span></span>

<span data-ttu-id="6b60a-126">Les messages Erreur système 53 ou Erreur système 67 peuvent s’afficher si la communication sortante du port 445 vers le centre de données du stockage Azure File est bloquée.</span><span class="sxs-lookup"><span data-stu-id="6b60a-126">System error 53 or system error 67 can occur if port 445 outbound communication to an Azure File storage datacenter is blocked.</span></span> <span data-ttu-id="6b60a-127">Pour afficher le récapitulatif des FAI qui autorisent ou interdisent l’accès depuis le port 445, consultez [TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span><span class="sxs-lookup"><span data-stu-id="6b60a-127">To see the summary of ISPs that allow or disallow access from port 445, go to [TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span></span>

<span data-ttu-id="6b60a-128">Pour comprendre s’il s’agit de la raison pour laquelle le message « Erreur système 53 » s’affiche, vous pouvez utiliser Portqry pour interroger le point de terminaison TCP:445.</span><span class="sxs-lookup"><span data-stu-id="6b60a-128">To understand whether this is the reason behind the "System error 53" message, you can use Portqry to query the TCP:445 endpoint.</span></span> <span data-ttu-id="6b60a-129">Si le point de terminaison TCP:445 est affiché comme filtré, le port TCP est bloqué.</span><span class="sxs-lookup"><span data-stu-id="6b60a-129">If the TCP:445 endpoint is displayed as filtered, the TCP port is blocked.</span></span> <span data-ttu-id="6b60a-130">Voici un exemple de requête :</span><span class="sxs-lookup"><span data-stu-id="6b60a-130">Here is an example query:</span></span>

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

<span data-ttu-id="6b60a-131">Si le port TCP 445 est bloqué par une règle sur le chemin d’accès réseau, vous verrez la sortie suivante :</span><span class="sxs-lookup"><span data-stu-id="6b60a-131">If TCP port 445 is blocked by a rule along the network path, you will see the following output:</span></span>

  `TCP port 445 (microsoft-ds service): FILTERED`

<span data-ttu-id="6b60a-132">Pour plus d’informations sur l’utilisation de Portqry, consultez [Description de l’utilitaire de ligne de commande Portqry.exe](https://support.microsoft.com/help/310099).</span><span class="sxs-lookup"><span data-stu-id="6b60a-132">For more information about how to use Portqry, see [Description of the Portqry.exe command-line utility](https://support.microsoft.com/help/310099).</span></span>

### <a name="solution-for-cause-2"></a><span data-ttu-id="6b60a-133">Solution pour la cause 2</span><span class="sxs-lookup"><span data-stu-id="6b60a-133">Solution for cause 2</span></span>

<span data-ttu-id="6b60a-134">Contactez votre service informatique pour ouvrir le port 445 sortant aux [plages IP Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="6b60a-134">Work with your IT department to open port 445 outbound to [Azure IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="cause-3-ntlmv1-is-enabled"></a><span data-ttu-id="6b60a-135">Cause 3 : NTLMv1 est activé</span><span class="sxs-lookup"><span data-stu-id="6b60a-135">Cause 3: NTLMv1 is enabled</span></span>

<span data-ttu-id="6b60a-136">Les messages Erreur système 53 ou Erreur système 87 peuvent également s’afficher si la communication NTLMv1 est activée sur le client.</span><span class="sxs-lookup"><span data-stu-id="6b60a-136">System error 53 or system error 87 can occur if NTLMv1 communication is enabled on the client.</span></span> <span data-ttu-id="6b60a-137">Le stockage Azure File prend uniquement en charge l’authentification NTLMv2.</span><span class="sxs-lookup"><span data-stu-id="6b60a-137">Azure File storage supports only NTLMv2 authentication.</span></span> <span data-ttu-id="6b60a-138">Le fait d’activer NTLMv1 crée un client moins sécurisé.</span><span class="sxs-lookup"><span data-stu-id="6b60a-138">Having NTLMv1 enabled creates a less-secure client.</span></span> <span data-ttu-id="6b60a-139">Par conséquent, les communications sont bloquées pour le stockage Azure File.</span><span class="sxs-lookup"><span data-stu-id="6b60a-139">Therefore, communication is blocked for Azure File storage.</span></span> 

<span data-ttu-id="6b60a-140">Pour déterminer s’il s’agit de la cause de l’erreur, vérifiez que la sous-clé de Registre suivante est définie sur une valeur de 3 :</span><span class="sxs-lookup"><span data-stu-id="6b60a-140">To determine whether this is the cause of the error, verify that the following registry subkey is set to a value of 3:</span></span>

<span data-ttu-id="6b60a-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span><span class="sxs-lookup"><span data-stu-id="6b60a-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span></span>

<span data-ttu-id="6b60a-142">Pour plus d’informations, consultez la rubrique [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) sur TechNet.</span><span class="sxs-lookup"><span data-stu-id="6b60a-142">For more information, see the [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) topic on TechNet.</span></span>

### <a name="solution-for-cause-3"></a><span data-ttu-id="6b60a-143">Solution pour la cause 3</span><span class="sxs-lookup"><span data-stu-id="6b60a-143">Solution for cause 3</span></span>

<span data-ttu-id="6b60a-144">Rétablissez la valeur **LmCompatibilityLevel** à la valeur par défaut 3 dans la sous-clé de Registre suivante :</span><span class="sxs-lookup"><span data-stu-id="6b60a-144">Revert the **LmCompatibilityLevel** value to the default value of 3 in the following registry subkey:</span></span>

  <span data-ttu-id="6b60a-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span><span class="sxs-lookup"><span data-stu-id="6b60a-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span></span>

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-to-process-this-command-when-you-copy-to-an-azure-file-share"></a><span data-ttu-id="6b60a-146">Le message Erreur 1816 « Quota disponible insuffisant pour effectuer cette commande » s’affiche lorsque vous copiez vers un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="6b60a-146">Error 1816 “Not enough quota is available to process this command” when you copy to an Azure file share</span></span>

### <a name="cause"></a><span data-ttu-id="6b60a-147">Cause :</span><span class="sxs-lookup"><span data-stu-id="6b60a-147">Cause</span></span>

<span data-ttu-id="6b60a-148">L’erreur 1816 se produit lorsque vous atteignez la limite autorisée de descripteurs ouverts simultanément pour un fichier sur l’ordinateur où le partage de fichiers est monté.</span><span class="sxs-lookup"><span data-stu-id="6b60a-148">Error 1816 happens when you reach the upper limit of concurrent open handles that are allowed for a file on the computer where the file share is being mounted.</span></span>

### <a name="solution"></a><span data-ttu-id="6b60a-149">Solution</span><span class="sxs-lookup"><span data-stu-id="6b60a-149">Solution</span></span>

<span data-ttu-id="6b60a-150">Réduisez le nombre de handles ouverts simultanément en fermant certains d’entre eux, puis réessayez.</span><span class="sxs-lookup"><span data-stu-id="6b60a-150">Reduce the number of concurrent open handles by closing some handles, and then retry.</span></span> <span data-ttu-id="6b60a-151">Pour plus d’informations, consultez [Liste de contrôle des performances et de l’extensibilité de Microsoft Azure Storage](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6b60a-151">For more information, see [Microsoft Azure Storage performance and scalability checklist](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-to-and-from-azure-file-storage-in-windows"></a><span data-ttu-id="6b60a-152">Ralentissement des copies de fichiers vers et depuis le stockage Azure File dans Windows</span><span class="sxs-lookup"><span data-stu-id="6b60a-152">Slow file copying to and from Azure File storage in Windows</span></span>

<span data-ttu-id="6b60a-153">Les performances peuvent être ralenties lorsque vous essayez de transférer des fichiers vers le service Azure File.</span><span class="sxs-lookup"><span data-stu-id="6b60a-153">You might see slow performance when you try to transfer files to the Azure File service.</span></span>

- <span data-ttu-id="6b60a-154">Si vous n’avez pas d’exigence de taille d’E/S minimum spécifique, nous vous recommandons d’utiliser une taille d’E/S de 1 Mo pour des performances optimales.</span><span class="sxs-lookup"><span data-stu-id="6b60a-154">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as the I/O size for optimal performance.</span></span>
-   <span data-ttu-id="6b60a-155">Si vous connaissez la taille finale d’un fichier que vous étendez avec des écritures, et si votre logiciel ne présente aucun problème de compatibilité lorsque la fin non écrite du fichier contient des zéros, définissez la taille du fichier à l’avance au lieu que chaque écriture soit une écriture d’extension.</span><span class="sxs-lookup"><span data-stu-id="6b60a-155">If you know the final size of a file that you are extending with writes, and your software doesn’t have compatibility problems when the unwritten tail on the file contains zeros, then set the file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="6b60a-156">Utilisez la méthode de copie appropriée :</span><span class="sxs-lookup"><span data-stu-id="6b60a-156">Use the right copy method:</span></span>
    -   <span data-ttu-id="6b60a-157">Utilisez [AZCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) pour les transferts entre deux partages de fichiers.</span><span class="sxs-lookup"><span data-stu-id="6b60a-157">Use [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="6b60a-158">Utilisez [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) entre des partages de fichiers sur un ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="6b60a-158">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a><span data-ttu-id="6b60a-159">Informations pour Windows 8.1 ou Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="6b60a-159">Considerations for Windows 8.1 or Windows Server 2012 R2</span></span>

<span data-ttu-id="6b60a-160">Pour les clients qui exécutent Windows 8.1 ou Windows Server 2012 R2, assurez-vous que le correctif logiciel [KB3114025](https://support.microsoft.com/help/3114025) est installé.</span><span class="sxs-lookup"><span data-stu-id="6b60a-160">For clients that are running Windows 8.1 or Windows Server 2012 R2, make sure that the [KB3114025](https://support.microsoft.com/help/3114025) hotfix is installed.</span></span> <span data-ttu-id="6b60a-161">Ce correctif logiciel améliore les performances de création et d’ouverture des handles.</span><span class="sxs-lookup"><span data-stu-id="6b60a-161">This hotfix improves the performance of create and close handles.</span></span>

<span data-ttu-id="6b60a-162">Vous pouvez exécuter le script suivant pour vérifier si le correctif logiciel a été installé :</span><span class="sxs-lookup"><span data-stu-id="6b60a-162">You can run the following script to check whether the hotfix has been installed:</span></span>

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

<span data-ttu-id="6b60a-163">Si le correctif logiciel est installé, la sortie suivante s’affiche :</span><span class="sxs-lookup"><span data-stu-id="6b60a-163">If hotfix is installed, the following output is displayed:</span></span>

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> <span data-ttu-id="6b60a-164">Les images de Windows Server 2012 R2 dans Azure Marketplace ont le correctif logiciel KB3114025 installé par défaut à compter de décembre 2015.</span><span class="sxs-lookup"><span data-stu-id="6b60a-164">Windows Server 2012 R2 images in Azure Marketplace have hotfix KB3114025 installed by default, starting in December 2015.</span></span>

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a><span data-ttu-id="6b60a-165">Aucun dossier avec une lettre de lecteur dans **Poste de travail**</span><span class="sxs-lookup"><span data-stu-id="6b60a-165">No folder with a drive letter in **My Computer**</span></span>

<span data-ttu-id="6b60a-166">Si vous mappez un partage de fichiers Azure en tant qu’administrateur via Net use, le partage n’apparaît pas.</span><span class="sxs-lookup"><span data-stu-id="6b60a-166">If you map an Azure file share as an administrator by using net use, the share appears to be missing.</span></span>

### <a name="cause"></a><span data-ttu-id="6b60a-167">Cause :</span><span class="sxs-lookup"><span data-stu-id="6b60a-167">Cause</span></span>

<span data-ttu-id="6b60a-168">Par défaut, l’Explorateur Windows ne s’exécute pas en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="6b60a-168">By default, Windows File Explorer does not run as an administrator.</span></span> <span data-ttu-id="6b60a-169">Si vous exécutez Net use depuis une invite de commandes administrateur, vous mappez le lecteur réseau en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="6b60a-169">If you run net use from an administrative command prompt, you map the network drive as an administrator.</span></span> <span data-ttu-id="6b60a-170">Étant donné que les lecteurs mappés sont centrés sur l’utilisateur, le compte d’utilisateur qui est connecté n’affiche pas les lecteurs s’ils sont montés sous un compte d’utilisateur différent.</span><span class="sxs-lookup"><span data-stu-id="6b60a-170">Because mapped drives are user-centric, the user account that is logged in does not display the drives if they are mounted under a different user account.</span></span>

### <a name="solution"></a><span data-ttu-id="6b60a-171">Solution</span><span class="sxs-lookup"><span data-stu-id="6b60a-171">Solution</span></span>
<span data-ttu-id="6b60a-172">Montez le partage à partir d’une ligne de commande non administrateur.</span><span class="sxs-lookup"><span data-stu-id="6b60a-172">Mount the share from a non-administrator command line.</span></span> <span data-ttu-id="6b60a-173">Vous pouvez également suivre [cette rubrique TechNet](https://technet.microsoft.com/library/ee844140.aspx) pour configurer la valeur de Registre **EnableLinkedConnections**.</span><span class="sxs-lookup"><span data-stu-id="6b60a-173">Alternatively, you can follow [this TechNet topic](https://technet.microsoft.com/library/ee844140.aspx) to configure the **EnableLinkedConnections** registry value.</span></span>

<a id="netuse"></a>
## <a name="net-use-command-fails-if-the-storage-account-contains-a-forward-slash"></a><span data-ttu-id="6b60a-174">La commande Net use échoue si le compte de stockage contient une barre oblique</span><span class="sxs-lookup"><span data-stu-id="6b60a-174">Net use command fails if the storage account contains a forward slash</span></span>

### <a name="cause"></a><span data-ttu-id="6b60a-175">Cause :</span><span class="sxs-lookup"><span data-stu-id="6b60a-175">Cause</span></span>

<span data-ttu-id="6b60a-176">La commande Net use interprète une barre oblique (/) comme une option de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="6b60a-176">The net use command interprets a forward slash (/) as a command-line option.</span></span> <span data-ttu-id="6b60a-177">Si le nom de votre compte utilisateur commence par une barre oblique, le mappage du lecteur échoue.</span><span class="sxs-lookup"><span data-stu-id="6b60a-177">If your user account name starts with a forward slash, the drive mapping fails.</span></span>

### <a name="solution"></a><span data-ttu-id="6b60a-178">Solution</span><span class="sxs-lookup"><span data-stu-id="6b60a-178">Solution</span></span>

<span data-ttu-id="6b60a-179">Vous pouvez utiliser l’une des étapes suivantes pour contourner le problème :</span><span class="sxs-lookup"><span data-stu-id="6b60a-179">You can use either of the following steps to work around the problem:</span></span>

- <span data-ttu-id="6b60a-180">Exécutez la commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="6b60a-180">Run the following PowerShell command:</span></span>

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  <span data-ttu-id="6b60a-181">Depuis un fichier de commandes, vous pouvez exécuter la commande de cette façon :</span><span class="sxs-lookup"><span data-stu-id="6b60a-181">From a batch file, you can run the command this way:</span></span>

  `Echo new-smbMapping ... | powershell -command –`

- <span data-ttu-id="6b60a-182">Placez des guillemets doubles autour de la clé pour résoudre ce problème, sauf si la barre oblique est le premier caractère.</span><span class="sxs-lookup"><span data-stu-id="6b60a-182">Put double quotation marks around the key to work around this problem--unless the forward slash is the first character.</span></span> <span data-ttu-id="6b60a-183">Si c’est le cas, utilisez le mode interactif et entrez votre mot de passe séparément, ou régénérez vos clés pour obtenir une clé qui ne commence pas par une barre oblique.</span><span class="sxs-lookup"><span data-stu-id="6b60a-183">If it is, either use the interactive mode and enter your password separately or regenerate your keys to get a key that doesn't start with a forward slash.</span></span>

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a><span data-ttu-id="6b60a-184">L’application ou service ne peut pas accéder à un lecteur monté de stockage Azure File</span><span class="sxs-lookup"><span data-stu-id="6b60a-184">Application or service cannot access a mounted Azure File storage drive</span></span>

### <a name="cause"></a><span data-ttu-id="6b60a-185">Cause :</span><span class="sxs-lookup"><span data-stu-id="6b60a-185">Cause</span></span>

<span data-ttu-id="6b60a-186">Les lecteurs sont montés par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6b60a-186">Drives are mounted per user.</span></span> <span data-ttu-id="6b60a-187">Si vous n’exécutez pas l’application ou service depuis le compte utilisateur ayant monté le lecteur, l’application ou service ne verra pas le lecteur.</span><span class="sxs-lookup"><span data-stu-id="6b60a-187">If your application or service is running under a different user account than the one that mounted the drive, the application will not see the drive.</span></span>

### <a name="solution"></a><span data-ttu-id="6b60a-188">Solution</span><span class="sxs-lookup"><span data-stu-id="6b60a-188">Solution</span></span>

<span data-ttu-id="6b60a-189">Utilisez l'une des solutions suivantes :</span><span class="sxs-lookup"><span data-stu-id="6b60a-189">Use one of the following solutions:</span></span>

-   <span data-ttu-id="6b60a-190">Montez le lecteur depuis le compte utilisateur qui dispose de l’application.</span><span class="sxs-lookup"><span data-stu-id="6b60a-190">Mount the drive from the same user account that contains the application.</span></span> <span data-ttu-id="6b60a-191">Vous pouvez utiliser un outil tel que PsExec.</span><span class="sxs-lookup"><span data-stu-id="6b60a-191">You can use a tool such as PsExec.</span></span>
- <span data-ttu-id="6b60a-192">Transmettez le nom et la clé du compte de stockage dans les paramètres de nom d’utilisateur et de mot de passe de la commande Net use.</span><span class="sxs-lookup"><span data-stu-id="6b60a-192">Pass the storage account name and key in the user name and password parameters of the net use command.</span></span>

<span data-ttu-id="6b60a-193">Après avoir suivi ces instructions, vous pourriez recevoir le message d’erreur suivant en exécutant Net use sur le compte de service réseau ou système : « Erreur système 1312.</span><span class="sxs-lookup"><span data-stu-id="6b60a-193">After you follow these instructions, you might receive the following error message when you run net use for the system/network service account: "System error 1312 has occurred.</span></span> <span data-ttu-id="6b60a-194">Une session ouverte spécifiée n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="6b60a-194">A specified logon session does not exist.</span></span> <span data-ttu-id="6b60a-195">Il se peut qu’elle ait été déjà fermée. »</span><span class="sxs-lookup"><span data-stu-id="6b60a-195">It may already have been terminated."</span></span> <span data-ttu-id="6b60a-196">Si cela se produit, vérifiez que le nom d’utilisateur transmis à Net use inclut des informations de domaine (par exemple : « [nom du compte de stockage].file.core.windows.net »).</span><span class="sxs-lookup"><span data-stu-id="6b60a-196">If this occurs, make sure that the username that is passed to net use includes domain information (for example: "[storage account name].file.core.windows.net").</span></span>

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-to-a-destination-that-does-not-support-encryption"></a><span data-ttu-id="6b60a-197">Erreur « Vous copiez un fichier vers une destination qui ne prend pas en charge le chiffrement »</span><span class="sxs-lookup"><span data-stu-id="6b60a-197">Error "You are copying a file to a destination that does not support encryption"</span></span>

<span data-ttu-id="6b60a-198">Lorsqu’un fichier est copié sur le réseau, le fichier est déchiffré sur l’ordinateur source, transmis en clair, puis de nouveau chiffré une fois à destination.</span><span class="sxs-lookup"><span data-stu-id="6b60a-198">When a file is copied over the network, the file is decrypted on the source computer, transmitted in plaintext, and re-encrypted at the destination.</span></span> <span data-ttu-id="6b60a-199">Toutefois, vous pourriez rencontrer l’erreur suivante en essayant de copier un fichier chiffré : « Vous copiez le fichier vers une destination qui ne prend pas en charge le chiffrement. »</span><span class="sxs-lookup"><span data-stu-id="6b60a-199">However, you might see the following error when you're trying to copy an encrypted file: "You are copying the file to a destination that does not support encryption."</span></span>

### <a name="cause"></a><span data-ttu-id="6b60a-200">Cause :</span><span class="sxs-lookup"><span data-stu-id="6b60a-200">Cause</span></span>
<span data-ttu-id="6b60a-201">Ce problème peut se survenir si vous utilisez le système de fichiers EFS (Encrypting File System).</span><span class="sxs-lookup"><span data-stu-id="6b60a-201">This problem can occur if you are using Encrypting File System (EFS).</span></span> <span data-ttu-id="6b60a-202">Les fichiers chiffrés par BitLocker peuvent être copiés vers le stockage Azure Files.</span><span class="sxs-lookup"><span data-stu-id="6b60a-202">BitLocker-encrypted files can be copied to Azure File storage.</span></span> <span data-ttu-id="6b60a-203">Toutefois, le stockage Azure File ne prend pas en charge le système de fichiers EFS NTFS.</span><span class="sxs-lookup"><span data-stu-id="6b60a-203">However, Azure File storage does not support NTFS EFS.</span></span>

### <a name="workaround"></a><span data-ttu-id="6b60a-204">Solution de contournement</span><span class="sxs-lookup"><span data-stu-id="6b60a-204">Workaround</span></span>
<span data-ttu-id="6b60a-205">Pour copier un fichier sur le réseau, vous devez d’abord le déchiffrer.</span><span class="sxs-lookup"><span data-stu-id="6b60a-205">To copy a file over the network, you must first decrypt it.</span></span> <span data-ttu-id="6b60a-206">Utilisez l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="6b60a-206">Use one of the following methods:</span></span>

- <span data-ttu-id="6b60a-207">Utilisez la commande **copy /d**.</span><span class="sxs-lookup"><span data-stu-id="6b60a-207">Use the **copy /d** command.</span></span> <span data-ttu-id="6b60a-208">Les fichiers chiffrés peuvent ainsi être enregistrés comme fichiers déchiffrés une fois à destination.</span><span class="sxs-lookup"><span data-stu-id="6b60a-208">It allows the encrypted files to be saved as decrypted files at the destination.</span></span>
- <span data-ttu-id="6b60a-209">Définissez la clé de Registre suivante :</span><span class="sxs-lookup"><span data-stu-id="6b60a-209">Set the following registry key:</span></span>
  - <span data-ttu-id="6b60a-210">Chemin d’accès = HKLM\Software\Policies\Microsoft\Windows\System</span><span class="sxs-lookup"><span data-stu-id="6b60a-210">Path = HKLM\Software\Policies\Microsoft\Windows\System</span></span>
  - <span data-ttu-id="6b60a-211">Type de valeur = DWORD</span><span class="sxs-lookup"><span data-stu-id="6b60a-211">Value type = DWORD</span></span>
  - <span data-ttu-id="6b60a-212">Nom = CopyFileAllowDecryptedRemoteDestination</span><span class="sxs-lookup"><span data-stu-id="6b60a-212">Name = CopyFileAllowDecryptedRemoteDestination</span></span>
  - <span data-ttu-id="6b60a-213">Valeur = 1</span><span class="sxs-lookup"><span data-stu-id="6b60a-213">Value = 1</span></span>

<span data-ttu-id="6b60a-214">Notez bien que la définition de la clé de Registre affecte toutes les opérations de copie sur les partages réseau.</span><span class="sxs-lookup"><span data-stu-id="6b60a-214">Be aware that setting the registry key affects all copy operations that are made to network shares.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="6b60a-215">Vous avez besoin d’aide ?</span><span class="sxs-lookup"><span data-stu-id="6b60a-215">Need help?</span></span> <span data-ttu-id="6b60a-216">Contactez le support technique.</span><span class="sxs-lookup"><span data-stu-id="6b60a-216">Contact support.</span></span>
<span data-ttu-id="6b60a-217">Si vous avez encore besoin d’aide, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) pour résoudre rapidement votre problème.</span><span class="sxs-lookup"><span data-stu-id="6b60a-217">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your problem resolved quickly.</span></span>
