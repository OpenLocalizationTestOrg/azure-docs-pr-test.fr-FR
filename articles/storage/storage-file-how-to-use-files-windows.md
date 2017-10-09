---
title: "aaaMount un partage de fichiers d’Azure et hello d’accès de partage dans Windows | Documents Microsoft"
description: "Montez un partage de fichiers d’Azure et un partage de hello d’accès dans Windows."
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 15ac468d9d7b8e0a195b024926ed4dd9790360d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-an-azure-file-share-and-access-hello-share-in-windows"></a><span data-ttu-id="0780f-103">Monter d’un partage de fichiers d’Azure et un partage de hello d’accès dans Windows</span><span class="sxs-lookup"><span data-stu-id="0780f-103">Mount an Azure File share and access hello share in Windows</span></span>
<span data-ttu-id="0780f-104">[Stockage de fichier Azure](storage-dotnet-how-to-use-files.md) est le système de fichiers de cloud de Microsoft toouse facile.</span><span class="sxs-lookup"><span data-stu-id="0780f-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy toouse cloud file system.</span></span> <span data-ttu-id="0780f-105">Les partages de fichiers Azure peuvent être montés dans Windows et Windows Server.</span><span class="sxs-lookup"><span data-stu-id="0780f-105">Azure File shares can be mounted in Windows and Windows Server.</span></span> <span data-ttu-id="0780f-106">Cet article décrit trois façons différentes toomount un partage de fichiers de Azure sur Windows : avec hello fichier Explorateur de l’interface utilisateur, via PowerShell ou hello invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="0780f-106">This article shows three different ways toomount an Azure File share on Windows: with hello File Explorer UI, via PowerShell, and via hello Command Prompt.</span></span> 

<span data-ttu-id="0780f-107">Dans l’ordre les toomount un fichier Azure partager en dehors de hello région Azure, il est hébergé dans, telles que localement ou dans une région différente, hello du système d’exploitation doit prendre en charge SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="0780f-107">In order toomount an Azure File share outside of hello Azure region it is hosted in, such as on-premises or in a different Azure region, hello OS must support SMB 3.0.</span></span> 

<span data-ttu-id="0780f-108">Le partage de fichier Azure peut être monté sur une machine Azure. Le montage est réalisé en local ou sur une machine virtuelle Azure en fonction de la version du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="0780f-108">Azure File share can be mounted on Windows machine either on-premises or in Azure VM depending on OS version.</span></span> <span data-ttu-id="0780f-109">Tableau ci-dessous illustre hello</span><span class="sxs-lookup"><span data-stu-id="0780f-109">Below table illustrates hello</span></span> 

| <span data-ttu-id="0780f-110">Version de Windows</span><span class="sxs-lookup"><span data-stu-id="0780f-110">Windows Version</span></span>        | <span data-ttu-id="0780f-111">Version SMB</span><span class="sxs-lookup"><span data-stu-id="0780f-111">SMB Version</span></span> |<span data-ttu-id="0780f-112">Version montable sur une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="0780f-112">Mountable On Azure VM</span></span>|<span data-ttu-id="0780f-113">Version montable en local</span><span class="sxs-lookup"><span data-stu-id="0780f-113">Mountable On-Premise</span></span>|
|------------------------|-------------|---------------------|---------------------|
| <span data-ttu-id="0780f-114">Windows 7</span><span class="sxs-lookup"><span data-stu-id="0780f-114">Windows 7</span></span>              | <span data-ttu-id="0780f-115">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="0780f-115">SMB 2.1</span></span>     | <span data-ttu-id="0780f-116">Oui</span><span class="sxs-lookup"><span data-stu-id="0780f-116">Yes</span></span>                 | <span data-ttu-id="0780f-117">Non</span><span class="sxs-lookup"><span data-stu-id="0780f-117">No</span></span>                  |
| <span data-ttu-id="0780f-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="0780f-118">Windows Server 2008 R2</span></span> | <span data-ttu-id="0780f-119">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="0780f-119">SMB 2.1</span></span>     | <span data-ttu-id="0780f-120">Oui</span><span class="sxs-lookup"><span data-stu-id="0780f-120">Yes</span></span>                 | <span data-ttu-id="0780f-121">Non</span><span class="sxs-lookup"><span data-stu-id="0780f-121">No</span></span>                  |
| <span data-ttu-id="0780f-122">Windows 8</span><span class="sxs-lookup"><span data-stu-id="0780f-122">Windows 8</span></span>              | <span data-ttu-id="0780f-123">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="0780f-123">SMB 3.0</span></span>     | <span data-ttu-id="0780f-124">Oui</span><span class="sxs-lookup"><span data-stu-id="0780f-124">Yes</span></span>                 | <span data-ttu-id="0780f-125">Oui</span><span class="sxs-lookup"><span data-stu-id="0780f-125">Yes</span></span>                 |
| <span data-ttu-id="0780f-126">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="0780f-126">Windows Server 2012</span></span>    | <span data-ttu-id="0780f-127">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="0780f-127">SMB 3.0</span></span>     | <span data-ttu-id="0780f-128">Oui</span><span class="sxs-lookup"><span data-stu-id="0780f-128">Yes</span></span>                 | <span data-ttu-id="0780f-129">Oui</span><span class="sxs-lookup"><span data-stu-id="0780f-129">Yes</span></span>                 |
| <span data-ttu-id="0780f-130">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="0780f-130">Windows Server 2012 R2</span></span> | <span data-ttu-id="0780f-131">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="0780f-131">SMB 3.0</span></span>     | <span data-ttu-id="0780f-132">Oui</span><span class="sxs-lookup"><span data-stu-id="0780f-132">Yes</span></span>                 | <span data-ttu-id="0780f-133">Oui</span><span class="sxs-lookup"><span data-stu-id="0780f-133">Yes</span></span>                 |
| <span data-ttu-id="0780f-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="0780f-134">Windows 10</span></span>             | <span data-ttu-id="0780f-135">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="0780f-135">SMB 3.0</span></span>     | <span data-ttu-id="0780f-136">Oui</span><span class="sxs-lookup"><span data-stu-id="0780f-136">Yes</span></span>                 | <span data-ttu-id="0780f-137">Oui</span><span class="sxs-lookup"><span data-stu-id="0780f-137">Yes</span></span>                 |

> [!Note]  
> <span data-ttu-id="0780f-138">Nous vous recommandons de prendre hello Ko la plus récente pour votre version de Windows.</span><span class="sxs-lookup"><span data-stu-id="0780f-138">We always recommend taking hello most recent KB for your version of Windows.</span></span>

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a><span data-ttu-id="0780f-139"></a>Conditions préalables pour le montage d’un partage de fichiers Azure avec Windows</span><span class="sxs-lookup"><span data-stu-id="0780f-139"></a>Prerequisites for Mounting Azure File Share with Windows</span></span> 
* <span data-ttu-id="0780f-140">**Nom de compte de stockage**: partage d’un fichier Azure toomount, vous devez serez hello nom hello du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0780f-140">**Storage Account Name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="0780f-141">**Clé de compte de stockage**: partage d’un fichier Azure toomount, vous devez serez hello la clé primaire (ou secondaire).</span><span class="sxs-lookup"><span data-stu-id="0780f-141">**Storage Account Key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="0780f-142">Actuellement, les clés SAS ne sont pas prises en charge pour le montage.</span><span class="sxs-lookup"><span data-stu-id="0780f-142">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="0780f-143">**Assurez-vous que le port 445 est ouvert** : le Stockage Fichier Azure utilise le protocole SMB.</span><span class="sxs-lookup"><span data-stu-id="0780f-143">**Ensure port 445 is open**: Azure File storage uses SMB protocol.</span></span> <span data-ttu-id="0780f-144">SMB communique via le port TCP 445 - Vérifiez les toosee si votre pare-feu ne bloque pas les ports TCP 445 à partir de l’ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="0780f-144">SMB communicates over TCP port 445 - check toosee if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-hello-azure-file-share-with-file-explorer"></a><span data-ttu-id="0780f-145">Monter le partage de fichiers Azure hello avec l’Explorateur de fichiers</span><span class="sxs-lookup"><span data-stu-id="0780f-145">Mount hello Azure File share with File Explorer</span></span>
> [!Note]  
> <span data-ttu-id="0780f-146">Notez que hello suivant les instructions affichées sur Windows 10 et peuvent différer légèrement sur les versions plus anciennes.</span><span class="sxs-lookup"><span data-stu-id="0780f-146">Note that hello following instructions are shown on Windows 10 and may differ slightly on older releases.</span></span> 

1. <span data-ttu-id="0780f-147">**Ouvrez l’Explorateur de fichiers**: cela est possible en l’ouvrant à partir du Menu Démarrer de hello, ou en appuyant sur le raccourci de Win + E.</span><span class="sxs-lookup"><span data-stu-id="0780f-147">**Open File Explorer**: This can be done by opening from hello Start Menu, or by pressing Win+E shortcut.</span></span>

2. <span data-ttu-id="0780f-148">**Accédez toohello élément de « Ce PC » sur le côté gauche de hello de fenêtre hello. Cela modifie les menus hello disponibles dans le ruban de hello. Sous le menu d’ordinateur hello, sélectionnez « Connecter un lecteur réseau »**.</span><span class="sxs-lookup"><span data-stu-id="0780f-148">**Navigate toohello "This PC" item on hello left-hand side of hello window. This will change hello menus available in hello ribbon. Under hello Computer menu, select "Map Network Drive"**.</span></span>
    
    ![Menu déroulant de capture d’écran de hello « Connecter un lecteur réseau »](media/storage-file-how-to-use-files-windows/1_MountOnWindows10.png)

3. <span data-ttu-id="0780f-150">**Chemin d’accès de copie hello UNC du volet de « Se connecter » hello Bonjour Azure portal**: une description détaillée de toofind ces informations peuvent être trouvées comment [ici](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span><span class="sxs-lookup"><span data-stu-id="0780f-150">**Copy hello UNC path from hello "Connect" pane in hello Azure portal**: A detailed description of how toofind this information can be found [here](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span></span>

    ![chemin d’accès UNC de Hello à partir du volet de connexion de stockage de fichier Azure hello](media/storage-file-how-to-use-files-windows/portal_netuse_connect.png)

4. <span data-ttu-id="0780f-152">**Sélectionnez la lettre de lecteur hello et entrez le chemin d’accès UNC de hello.**</span><span class="sxs-lookup"><span data-stu-id="0780f-152">**Select hello Drive letter and enter hello UNC path.**</span></span> 
    
    ![Une capture d’écran de boîte de dialogue « Connecter un lecteur réseau » hello](media/storage-file-how-to-use-files-windows/2_MountOnWindows10.png)

5. <span data-ttu-id="0780f-154">**Hello d’utilisation avec préfixe de nom de compte de stockage `Azure\` en tant que nom d’utilisateur hello et une clé de compte de stockage en tant que mot de passe hello.**</span><span class="sxs-lookup"><span data-stu-id="0780f-154">**Use hello Storage Account Name prepended with `Azure\` as hello username and a Storage Account Key as hello password.**</span></span>
    
    ![Une capture d’écran de la boîte de dialogue informations d’identification de réseau hello](media/storage-file-how-to-use-files-windows/3_MountOnWindows10.png)

6. <span data-ttu-id="0780f-156">**Utilisez le partage de fichiers Azure à votre guise**.</span><span class="sxs-lookup"><span data-stu-id="0780f-156">**Use Azure File share as desired**.</span></span>
    
    ![Le partage de fichiers Azure est désormais monté.](media/storage-file-how-to-use-files-windows/4_MountOnWindows10.png)

7. <span data-ttu-id="0780f-158">**Lorsque vous toodismount prêt (ou déconnectez) partage de fichiers Azure hello, vous pouvez le faire par le bouton droit sur l’entrée hello pour partage hello sous hello « emplacements réseau » dans l’Explorateur de fichiers et en sélectionnant « Déconnecter »**.</span><span class="sxs-lookup"><span data-stu-id="0780f-158">**When you are ready toodismount (or disconnect) hello Azure File share, you can do so by right clicking on hello entry for hello share under hello "Network locations" in File Explorer and selecting "Disconnect"**.</span></span>

## <a name="mount-hello-azure-file-share-with-powershell"></a><span data-ttu-id="0780f-159">Monter le partage de fichiers Azure hello avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="0780f-159">Mount hello Azure File share with PowerShell</span></span>
1. <span data-ttu-id="0780f-160">**Partage de fichiers Azure hello toomount de commande suivant de hello utilisation**: n’oubliez pas de tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` avec des informations correctes hello.</span><span class="sxs-lookup"><span data-stu-id="0780f-160">**Use hello following command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with hello proper information.</span></span>

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. <span data-ttu-id="0780f-161">**Partage de fichiers Azure hello utilisation comme vous le souhaitez**.</span><span class="sxs-lookup"><span data-stu-id="0780f-161">**Use hello Azure File share as desired**.</span></span>

3. <span data-ttu-id="0780f-162">**Lorsque vous avez terminé, démontez le partage de fichiers Azure hello hello de commande suivante à l’aide de**.</span><span class="sxs-lookup"><span data-stu-id="0780f-162">**When you are finished, dismount hello Azure File share using hello following command**.</span></span>

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> <span data-ttu-id="0780f-163">Vous pouvez utiliser hello `-Persist` paramètre sur `New-PSDrive` toomake hello reste visible toohello hello du système d’exploitation pendant le montage de fichiers Azure partage.</span><span class="sxs-lookup"><span data-stu-id="0780f-163">You may use hello `-Persist` parameter on `New-PSDrive` toomake hello Azure File share visible toohello rest of hello OS while mounted.</span></span>

## <a name="mount-hello-azure-file-share-with-command-prompt"></a><span data-ttu-id="0780f-164">Monter le partage de fichiers Azure hello invite de commandes</span><span class="sxs-lookup"><span data-stu-id="0780f-164">Mount hello Azure File share with Command Prompt</span></span>
1. <span data-ttu-id="0780f-165">**Partage de fichiers Azure hello toomount de commande suivant de hello utilisation**: n’oubliez pas de tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` avec des informations correctes hello.</span><span class="sxs-lookup"><span data-stu-id="0780f-165">**Use hello following command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with hello proper information.</span></span>

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. <span data-ttu-id="0780f-166">**Partage de fichiers Azure hello utilisation comme vous le souhaitez**.</span><span class="sxs-lookup"><span data-stu-id="0780f-166">**Use hello Azure File share as desired**.</span></span>

3. <span data-ttu-id="0780f-167">**Lorsque vous avez terminé, démontez le partage de fichiers Azure hello hello de commande suivante à l’aide de**.</span><span class="sxs-lookup"><span data-stu-id="0780f-167">**When you are finished, dismount hello Azure File share using hello following command**.</span></span>

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> <span data-ttu-id="0780f-168">Vous pouvez configurer hello fichier Azure partage tooautomatically se reconnecter au redémarrage par les informations d’identification hello persistantes dans Windows.</span><span class="sxs-lookup"><span data-stu-id="0780f-168">You can configure hello Azure File share tooautomatically reconnect on reboot by persisting hello credentials in Windows.</span></span> <span data-ttu-id="0780f-169">Hello commande suivante rendront les informations d’identification hello :</span><span class="sxs-lookup"><span data-stu-id="0780f-169">hello following command will persist hello credentials:</span></span>
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a><span data-ttu-id="0780f-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0780f-170">Next steps</span></span>
<span data-ttu-id="0780f-171">Pour plus d’informations sur le stockage de fichiers Azure, consultez ces liens.</span><span class="sxs-lookup"><span data-stu-id="0780f-171">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="0780f-172">FAQ</span><span class="sxs-lookup"><span data-stu-id="0780f-172">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="0780f-173">Dépannage</span><span class="sxs-lookup"><span data-stu-id="0780f-173">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="0780f-174">Vidéos et articles conceptuels</span><span class="sxs-lookup"><span data-stu-id="0780f-174">Conceptual articles and videos</span></span>
* [<span data-ttu-id="0780f-175">Stockage Fichier Azure : un système de fichiers SMB dans le cloud sans friction pour Windows et Linux</span><span class="sxs-lookup"><span data-stu-id="0780f-175">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="0780f-176">Comment toouse stockage Azure files avec Linux</span><span class="sxs-lookup"><span data-stu-id="0780f-176">How toouse Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a><span data-ttu-id="0780f-177">Outils pour le Stockage Fichier Azure</span><span class="sxs-lookup"><span data-stu-id="0780f-177">Tooling support for Azure File storage</span></span>
* [<span data-ttu-id="0780f-178">Utilisation d'Azure PowerShell avec Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0780f-178">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="0780f-179">Comment toouse AzCopy avec Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0780f-179">How toouse AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="0780f-180">À l’aide de hello CLI d’Azure avec le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="0780f-180">Using hello Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="0780f-181">Résolution des problèmes de stockage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="0780f-181">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="blog-posts"></a><span data-ttu-id="0780f-182">Billets de blog :</span><span class="sxs-lookup"><span data-stu-id="0780f-182">Blog posts</span></span>
* [<span data-ttu-id="0780f-183">Le stockage de fichiers Azure est désormais mis à la disposition générale</span><span class="sxs-lookup"><span data-stu-id="0780f-183">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="0780f-184">Dans le Stockage Fichier Azure</span><span class="sxs-lookup"><span data-stu-id="0780f-184">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="0780f-185">Présentation de Microsoft Azure File Service</span><span class="sxs-lookup"><span data-stu-id="0780f-185">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="0780f-186">Migration tooAzure de données fichier</span><span class="sxs-lookup"><span data-stu-id="0780f-186">Migrating data tooAzure File </span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="0780f-187">Référence</span><span class="sxs-lookup"><span data-stu-id="0780f-187">Reference</span></span>
* [<span data-ttu-id="0780f-188">Référence de la bibliothèque cliente de stockage pour .NET</span><span class="sxs-lookup"><span data-stu-id="0780f-188">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="0780f-189">Référence de l’API REST du service de fichiers</span><span class="sxs-lookup"><span data-stu-id="0780f-189">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
