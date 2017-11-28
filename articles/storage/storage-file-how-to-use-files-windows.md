---
title: "Montage d’un partage de fichiers Azure et accès au partage dans Windows | Microsoft Docs"
description: "Montage d’un partage de fichiers Azure et accès au partage dans Windows."
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
ms.openlocfilehash: e911e787cd1e29b2bbeaa648869c50245f2dd9ba
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="mount-an-azure-file-share-and-access-the-share-in-windows"></a><span data-ttu-id="1bd30-103">Montage d’un partage de fichiers Azure et accès au partage dans Windows</span><span class="sxs-lookup"><span data-stu-id="1bd30-103">Mount an Azure File share and access the share in Windows</span></span>
<span data-ttu-id="1bd30-104">Le [Stockage Fichier Azure](storage-dotnet-how-to-use-files.md) est le système de fichiers dans le cloud, facile à utiliser, de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1bd30-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy to use cloud file system.</span></span> <span data-ttu-id="1bd30-105">Les partages de fichiers Azure peuvent être montés dans Windows et Windows Server.</span><span class="sxs-lookup"><span data-stu-id="1bd30-105">Azure File shares can be mounted in Windows and Windows Server.</span></span> <span data-ttu-id="1bd30-106">Cet article présente trois méthodes différentes de montage d’un partage de fichiers Azure sur Windows : avec l’interface utilisateur de l’Explorateur de fichiers, via PowerShell ou via l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="1bd30-106">This article shows three different ways to mount an Azure File share on Windows: with the File Explorer UI, via PowerShell, and via the Command Prompt.</span></span> 

<span data-ttu-id="1bd30-107">Pour monter un partage de fichiers Azure en dehors de la région Azure sur laquelle il est hébergé, par exemple localement ou dans une région Azure différente, le système d’exploitation doit prendre en charge SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="1bd30-107">In order to mount an Azure File share outside of the Azure region it is hosted in, such as on-premises or in a different Azure region, the OS must support SMB 3.0.</span></span> 

<span data-ttu-id="1bd30-108">Le partage de fichier Azure peut être monté sur une machine Azure. Le montage est réalisé en local ou sur une machine virtuelle Azure en fonction de la version du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="1bd30-108">Azure File share can be mounted on Windows machine either on-premises or in Azure VM depending on OS version.</span></span> <span data-ttu-id="1bd30-109">Le tableau ci-dessous illustre la :</span><span class="sxs-lookup"><span data-stu-id="1bd30-109">Below table illustrates the</span></span> 

| <span data-ttu-id="1bd30-110">Version de Windows</span><span class="sxs-lookup"><span data-stu-id="1bd30-110">Windows Version</span></span>        | <span data-ttu-id="1bd30-111">Version SMB</span><span class="sxs-lookup"><span data-stu-id="1bd30-111">SMB Version</span></span> |<span data-ttu-id="1bd30-112">Version montable sur une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="1bd30-112">Mountable On Azure VM</span></span>|<span data-ttu-id="1bd30-113">Version montable en local</span><span class="sxs-lookup"><span data-stu-id="1bd30-113">Mountable On-Premise</span></span>|
|------------------------|-------------|---------------------|---------------------|
| <span data-ttu-id="1bd30-114">Windows 7</span><span class="sxs-lookup"><span data-stu-id="1bd30-114">Windows 7</span></span>              | <span data-ttu-id="1bd30-115">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="1bd30-115">SMB 2.1</span></span>     | <span data-ttu-id="1bd30-116">Oui</span><span class="sxs-lookup"><span data-stu-id="1bd30-116">Yes</span></span>                 | <span data-ttu-id="1bd30-117">Non</span><span class="sxs-lookup"><span data-stu-id="1bd30-117">No</span></span>                  |
| <span data-ttu-id="1bd30-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="1bd30-118">Windows Server 2008 R2</span></span> | <span data-ttu-id="1bd30-119">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="1bd30-119">SMB 2.1</span></span>     | <span data-ttu-id="1bd30-120">Oui</span><span class="sxs-lookup"><span data-stu-id="1bd30-120">Yes</span></span>                 | <span data-ttu-id="1bd30-121">Non</span><span class="sxs-lookup"><span data-stu-id="1bd30-121">No</span></span>                  |
| <span data-ttu-id="1bd30-122">Windows 8</span><span class="sxs-lookup"><span data-stu-id="1bd30-122">Windows 8</span></span>              | <span data-ttu-id="1bd30-123">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="1bd30-123">SMB 3.0</span></span>     | <span data-ttu-id="1bd30-124">Oui</span><span class="sxs-lookup"><span data-stu-id="1bd30-124">Yes</span></span>                 | <span data-ttu-id="1bd30-125">Oui</span><span class="sxs-lookup"><span data-stu-id="1bd30-125">Yes</span></span>                 |
| <span data-ttu-id="1bd30-126">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="1bd30-126">Windows Server 2012</span></span>    | <span data-ttu-id="1bd30-127">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="1bd30-127">SMB 3.0</span></span>     | <span data-ttu-id="1bd30-128">Oui</span><span class="sxs-lookup"><span data-stu-id="1bd30-128">Yes</span></span>                 | <span data-ttu-id="1bd30-129">Oui</span><span class="sxs-lookup"><span data-stu-id="1bd30-129">Yes</span></span>                 |
| <span data-ttu-id="1bd30-130">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="1bd30-130">Windows Server 2012 R2</span></span> | <span data-ttu-id="1bd30-131">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="1bd30-131">SMB 3.0</span></span>     | <span data-ttu-id="1bd30-132">Oui</span><span class="sxs-lookup"><span data-stu-id="1bd30-132">Yes</span></span>                 | <span data-ttu-id="1bd30-133">Oui</span><span class="sxs-lookup"><span data-stu-id="1bd30-133">Yes</span></span>                 |
| <span data-ttu-id="1bd30-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="1bd30-134">Windows 10</span></span>             | <span data-ttu-id="1bd30-135">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="1bd30-135">SMB 3.0</span></span>     | <span data-ttu-id="1bd30-136">Oui</span><span class="sxs-lookup"><span data-stu-id="1bd30-136">Yes</span></span>                 | <span data-ttu-id="1bd30-137">Oui</span><span class="sxs-lookup"><span data-stu-id="1bd30-137">Yes</span></span>                 |

> [!Note]  
> <span data-ttu-id="1bd30-138">Nous vous conseillons de prendre la base de connaissances la plus récente pour votre version de Windows.</span><span class="sxs-lookup"><span data-stu-id="1bd30-138">We always recommend taking the most recent KB for your version of Windows.</span></span>

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a><span data-ttu-id="1bd30-139"></a>Conditions préalables pour le montage d’un partage de fichiers Azure avec Windows</span><span class="sxs-lookup"><span data-stu-id="1bd30-139"></a>Prerequisites for Mounting Azure File Share with Windows</span></span> 
* <span data-ttu-id="1bd30-140">**Nom de compte de stockage** : pour monter un partage de fichiers Azure, vous avez besoin du nom du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="1bd30-140">**Storage Account Name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="1bd30-141">**Clé du compte de stockage** : pour monter un partage de fichiers Azure, vous avez besoin de la clé de stockage primaire (ou secondaire).</span><span class="sxs-lookup"><span data-stu-id="1bd30-141">**Storage Account Key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="1bd30-142">Actuellement, les clés SAS ne sont pas prises en charge pour le montage.</span><span class="sxs-lookup"><span data-stu-id="1bd30-142">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="1bd30-143">**Assurez-vous que le port 445 est ouvert** : le Stockage Fichier Azure utilise le protocole SMB.</span><span class="sxs-lookup"><span data-stu-id="1bd30-143">**Ensure port 445 is open**: Azure File storage uses SMB protocol.</span></span> <span data-ttu-id="1bd30-144">SMB communique via le port TCP 445. Assurez-vous que votre pare-feu ne bloque pas les ports TCP 445 à partir de la machine cliente.</span><span class="sxs-lookup"><span data-stu-id="1bd30-144">SMB communicates over TCP port 445 - check to see if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-the-azure-file-share-with-file-explorer"></a><span data-ttu-id="1bd30-145">Montage du partage de fichiers Azure avec l’Explorateur de fichiers</span><span class="sxs-lookup"><span data-stu-id="1bd30-145">Mount the Azure File share with File Explorer</span></span>
> [!Note]  
> <span data-ttu-id="1bd30-146">Notez que les instructions ci-après sont affichées sur Windows 10 et peuvent différer légèrement sur les versions plus anciennes.</span><span class="sxs-lookup"><span data-stu-id="1bd30-146">Note that the following instructions are shown on Windows 10 and may differ slightly on older releases.</span></span> 

1. <span data-ttu-id="1bd30-147">**Ouvrez l’Explorateur de fichiers** : pour cela, accédez au menu Démarrer ou appuyez sur les touches Win+E.</span><span class="sxs-lookup"><span data-stu-id="1bd30-147">**Open File Explorer**: This can be done by opening from the Start Menu, or by pressing Win+E shortcut.</span></span>

2. <span data-ttu-id="1bd30-148">**Accédez à l’élément « Ce PC » sur la gauche de la fenêtre. Cela modifie les menus disponibles dans le ruban. Dans le menu Ordinateur, sélectionnez « Connecter un lecteur réseau »**.</span><span class="sxs-lookup"><span data-stu-id="1bd30-148">**Navigate to the "This PC" item on the left-hand side of the window. This will change the menus available in the ribbon. Under the Computer menu, select "Map Network Drive"**.</span></span>
    
    ![Une capture d’écran du menu déroulant « Connecter un lecteur réseau »](media/storage-file-how-to-use-files-windows/1_MountOnWindows10.png)

3. <span data-ttu-id="1bd30-150">**Copiez le chemin d’accès UNC depuis le volet « Connexion » dans le portail Azure** : découvrez en détail comment trouver ces informations, en cliquant [ici](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span><span class="sxs-lookup"><span data-stu-id="1bd30-150">**Copy the UNC path from the "Connect" pane in the Azure portal**: A detailed description of how to find this information can be found [here](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span></span>

    ![Le chemin d’accès UNC dans le volet de connexion Stockage Fichier Azure](media/storage-file-how-to-use-files-windows/portal_netuse_connect.png)

4. <span data-ttu-id="1bd30-152">**Sélectionnez la lettre de lecteur et entrez le chemin d’accès UNC.**</span><span class="sxs-lookup"><span data-stu-id="1bd30-152">**Select the Drive letter and enter the UNC path.**</span></span> 
    
    ![Une capture d’écran de la boîte de dialogue « Connecter un lecteur réseau »](media/storage-file-how-to-use-files-windows/2_MountOnWindows10.png)

5. <span data-ttu-id="1bd30-154">**Utilisez le nom du compte de stockage avec le préfixe `Azure\` comme nom d’utilisateur et une clé de compte de stockage comme mot de passe.**</span><span class="sxs-lookup"><span data-stu-id="1bd30-154">**Use the Storage Account Name prepended with `Azure\` as the username and a Storage Account Key as the password.**</span></span>
    
    ![Une capture d’écran de la boîte de dialogue des identifiants réseau](media/storage-file-how-to-use-files-windows/3_MountOnWindows10.png)

6. <span data-ttu-id="1bd30-156">**Utilisez le partage de fichiers Azure à votre guise**.</span><span class="sxs-lookup"><span data-stu-id="1bd30-156">**Use Azure File share as desired**.</span></span>
    
    ![Le partage de fichiers Azure est désormais monté.](media/storage-file-how-to-use-files-windows/4_MountOnWindows10.png)

7. <span data-ttu-id="1bd30-158">**Lorsque vous êtes prêt à démonter (ou déconnecter) le partage de fichiers Azure, il vous suffit de cliquer avec le bouton droit de la souris sur l’entrée du partage, sous « Emplacements réseau », dans l’Explorateur de fichiers et de sélectionner « Déconnecter »**.</span><span class="sxs-lookup"><span data-stu-id="1bd30-158">**When you are ready to dismount (or disconnect) the Azure File share, you can do so by right clicking on the entry for the share under the "Network locations" in File Explorer and selecting "Disconnect"**.</span></span>

## <a name="mount-the-azure-file-share-with-powershell"></a><span data-ttu-id="1bd30-159">Montage du partage de fichiers Azure avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="1bd30-159">Mount the Azure File share with PowerShell</span></span>
1. <span data-ttu-id="1bd30-160">**Utilisez la commande suivante pour monter le partage de fichiers Azure** : n’oubliez pas de remplacer `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` par les informations appropriées.</span><span class="sxs-lookup"><span data-stu-id="1bd30-160">**Use the following command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with the proper information.</span></span>

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. <span data-ttu-id="1bd30-161">**Utilisez le partage de fichiers Azure à votre guise**.</span><span class="sxs-lookup"><span data-stu-id="1bd30-161">**Use the Azure File share as desired**.</span></span>

3. <span data-ttu-id="1bd30-162">**Lorsque vous avez terminé, démontez le partage de fichiers Azure à l’aide de la commande suivante**.</span><span class="sxs-lookup"><span data-stu-id="1bd30-162">**When you are finished, dismount the Azure File share using the following command**.</span></span>

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> <span data-ttu-id="1bd30-163">Vous pouvez utiliser le paramètre `-Persist` sur `New-PSDrive` pour que le partage de fichiers Azure soit visible pour le reste du système d’exploitation lorsqu’il est monté.</span><span class="sxs-lookup"><span data-stu-id="1bd30-163">You may use the `-Persist` parameter on `New-PSDrive` to make the Azure File share visible to the rest of the OS while mounted.</span></span>

## <a name="mount-the-azure-file-share-with-command-prompt"></a><span data-ttu-id="1bd30-164">Montage du partage de fichiers Azure avec l’invite de commandes</span><span class="sxs-lookup"><span data-stu-id="1bd30-164">Mount the Azure File share with Command Prompt</span></span>
1. <span data-ttu-id="1bd30-165">**Utilisez la commande suivante pour monter le partage de fichiers Azure** : n’oubliez pas de remplacer `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` par les informations appropriées.</span><span class="sxs-lookup"><span data-stu-id="1bd30-165">**Use the following command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with the proper information.</span></span>

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. <span data-ttu-id="1bd30-166">**Utilisez le partage de fichiers Azure à votre guise**.</span><span class="sxs-lookup"><span data-stu-id="1bd30-166">**Use the Azure File share as desired**.</span></span>

3. <span data-ttu-id="1bd30-167">**Lorsque vous avez terminé, démontez le partage de fichiers Azure à l’aide de la commande suivante**.</span><span class="sxs-lookup"><span data-stu-id="1bd30-167">**When you are finished, dismount the Azure File share using the following command**.</span></span>

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> <span data-ttu-id="1bd30-168">Vous pouvez configurer le partage de fichiers Azure de manière à ce qu’il se reconnecte automatiquement au redémarrage grâce aux identifiants persistants dans Windows.</span><span class="sxs-lookup"><span data-stu-id="1bd30-168">You can configure the Azure File share to automatically reconnect on reboot by persisting the credentials in Windows.</span></span> <span data-ttu-id="1bd30-169">La commande suivante permet de conserver les informations d’identification :</span><span class="sxs-lookup"><span data-stu-id="1bd30-169">The following command will persist the credentials:</span></span>
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a><span data-ttu-id="1bd30-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1bd30-170">Next steps</span></span>
<span data-ttu-id="1bd30-171">Pour plus d’informations sur le stockage de fichiers Azure, consultez ces liens.</span><span class="sxs-lookup"><span data-stu-id="1bd30-171">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="1bd30-172">FAQ</span><span class="sxs-lookup"><span data-stu-id="1bd30-172">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="1bd30-173">Dépannage</span><span class="sxs-lookup"><span data-stu-id="1bd30-173">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="1bd30-174">Vidéos et articles conceptuels</span><span class="sxs-lookup"><span data-stu-id="1bd30-174">Conceptual articles and videos</span></span>
* [<span data-ttu-id="1bd30-175">Stockage Fichier Azure : un système de fichiers SMB dans le cloud sans friction pour Windows et Linux</span><span class="sxs-lookup"><span data-stu-id="1bd30-175">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="1bd30-176">Utilisation de Stockage Fichier Azure avec Linux</span><span class="sxs-lookup"><span data-stu-id="1bd30-176">How to use Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a><span data-ttu-id="1bd30-177">Outils pour le Stockage Fichier Azure</span><span class="sxs-lookup"><span data-stu-id="1bd30-177">Tooling support for Azure File storage</span></span>
* [<span data-ttu-id="1bd30-178">Utilisation d'Azure PowerShell avec Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1bd30-178">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="1bd30-179">Utilisation de AzCopy avec Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1bd30-179">How to use AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="1bd30-180">Utilisation de la CLI Microsoft Azure avec Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1bd30-180">Using the Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="1bd30-181">Résolution des problèmes de stockage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="1bd30-181">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="blog-posts"></a><span data-ttu-id="1bd30-182">Billets de blog :</span><span class="sxs-lookup"><span data-stu-id="1bd30-182">Blog posts</span></span>
* [<span data-ttu-id="1bd30-183">Le stockage de fichiers Azure est désormais mis à la disposition générale</span><span class="sxs-lookup"><span data-stu-id="1bd30-183">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="1bd30-184">Dans le Stockage Fichier Azure</span><span class="sxs-lookup"><span data-stu-id="1bd30-184">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="1bd30-185">Présentation de Microsoft Azure File Service</span><span class="sxs-lookup"><span data-stu-id="1bd30-185">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="1bd30-186">Migration de données vers le fichier Azure</span><span class="sxs-lookup"><span data-stu-id="1bd30-186">Migrating data to Azure File </span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="1bd30-187">Référence</span><span class="sxs-lookup"><span data-stu-id="1bd30-187">Reference</span></span>
* [<span data-ttu-id="1bd30-188">Référence de la bibliothèque cliente de stockage pour .NET</span><span class="sxs-lookup"><span data-stu-id="1bd30-188">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="1bd30-189">Référence de l’API REST du service de fichiers</span><span class="sxs-lookup"><span data-stu-id="1bd30-189">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
