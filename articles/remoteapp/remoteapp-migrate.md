---
title: "données d’utilisateur aaaMigrate à partir d’Azure RemoteApp | Documents Microsoft"
description: "Découvrez comment toomigrate vos données utilisateur vers et depuis Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d7e4fbf1-cb42-4430-94a0-ed6d4676fc86
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aefc6ccc2c6173754acf6cad06102f27c8cb1d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-data-into-and-out-of-azure-remoteapp"></a><span data-ttu-id="06f1b-103">Comment toomigrate des données dans et hors d’Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="06f1b-103">How toomigrate data into and out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="06f1b-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="06f1b-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="06f1b-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="06f1b-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="06f1b-106">Vous pouvez utiliser de nombreux différents outils et méthodes tootransfer [données utilisateur](remoteapp-upd.md) dans et hors d’Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="06f1b-106">You can use many different tools and methods tootransfer [user data](remoteapp-upd.md) into and out of Azure RemoteApp.</span></span> <span data-ttu-id="06f1b-107">Voici quelques méthodes :</span><span class="sxs-lookup"><span data-stu-id="06f1b-107">Here are a few methods:</span></span>

* <span data-ttu-id="06f1b-108">Copier et coller en utilisant le partage du Presse-papiers</span><span class="sxs-lookup"><span data-stu-id="06f1b-108">Copy and paste using clipboard sharing</span></span>
* <span data-ttu-id="06f1b-109">Copiez les fichiers et les données de serveur de fichiers tooa</span><span class="sxs-lookup"><span data-stu-id="06f1b-109">Copy files and data tooa file server</span></span>
* <span data-ttu-id="06f1b-110">Copiez les fichiers tooOneDrive for Business via un navigateur</span><span class="sxs-lookup"><span data-stu-id="06f1b-110">Copy files tooOneDrive for Business through a browser</span></span>
* <span data-ttu-id="06f1b-111">Copier des fichiers à l’aide de la redirection</span><span class="sxs-lookup"><span data-stu-id="06f1b-111">Copy files using redirection</span></span>

> [!NOTE]
> <span data-ttu-id="06f1b-112">Vous ne pouvez pas activer hello OneDrive pour les agents de synchronisation professionnels et particuliers - ils [ne sont pas pris en charge](remoteapp-onedrive.md) dans Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="06f1b-112">You cannot enable hello OneDrive for Business or Consumer sync agents - they [are not supported](remoteapp-onedrive.md) in Azure RemoteApp.</span></span>
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a><span data-ttu-id="06f1b-113">Utiliser le copier-coller dans l’Explorateur de fichiers</span><span class="sxs-lookup"><span data-stu-id="06f1b-113">Use copy and paste in File Explorer</span></span>
<span data-ttu-id="06f1b-114">Copier et coller à l’aide de Presse-papiers de hello est activé dans les déploiements de RemoteApp [par défaut](remoteapp-redirection.md).</span><span class="sxs-lookup"><span data-stu-id="06f1b-114">Copy and paste using hello clipboard is enabled in RemoteApp deployments [by default](remoteapp-redirection.md).</span></span> <span data-ttu-id="06f1b-115">Cela permet aux utilisateurs de copier des fichiers entre leur ordinateur local et les applications RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="06f1b-115">This lets users copy files between their local PC and RemoteApp apps.</span></span> <span data-ttu-id="06f1b-116">Souvent, via hello normales à l’aide d’applications dans RemoteApp, les utilisateurs ont enregistré les fichiers des tootheir - déplacement que les données de RemoteApp sont faciles :</span><span class="sxs-lookup"><span data-stu-id="06f1b-116">Often, through hello normal course of using apps in RemoteApp, users have saved files tootheir UPDs - moving that data out of RemoteApp is easy:</span></span>

1. <span data-ttu-id="06f1b-117">[Publiez l’Explorateur de fichiers en tant qu’application](remoteapp-publish.md) dans une collection RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="06f1b-117">[Publish File Explorer as an app](remoteapp-publish.md) in a RemoteApp collection.</span></span> <span data-ttu-id="06f1b-118">(Notez qu’il s’agit d’une tâche administrative.)</span><span class="sxs-lookup"><span data-stu-id="06f1b-118">(Note that this is an administrative task.)</span></span>
2. <span data-ttu-id="06f1b-119">Directement votre application de l’Explorateur de fichiers utilisateurs toolaunch hello que vous avez publié et toouse qui toocopy et coller les fichiers dans leur UPD et de sortie.</span><span class="sxs-lookup"><span data-stu-id="06f1b-119">Direct your users toolaunch hello File Explorer app you published and toouse that toocopy and paste files both into their UPD and out of it.</span></span>

## <a name="upload-files-and-data-tooa-file-server-by-using-standard-network-file-copy"></a><span data-ttu-id="06f1b-120">Télécharger les fichiers et serveur de fichiers de données tooa à l’aide de la copie de fichiers réseau standard</span><span class="sxs-lookup"><span data-stu-id="06f1b-120">Upload files and data tooa file server by using standard network file copy</span></span>
<span data-ttu-id="06f1b-121">Souvent, les organisations utilisent le fichier serveurs toostore général des données.</span><span class="sxs-lookup"><span data-stu-id="06f1b-121">Often organizations use file servers toostore general data.</span></span> <span data-ttu-id="06f1b-122">Si vous connaissez le nom du serveur hello ou un emplacement, vos utilisateurs peuvent parcourir hello de réseau local pour le serveur de hello et copier puis leurs fichiers, comme c’était le cas ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="06f1b-122">If you know hello server name or location, your users can browse hello local network for hello server and then copy their files there, much like they did above.</span></span> <span data-ttu-id="06f1b-123">Nouveau vous souhaitez tooRemoteApp de l’Explorateur de fichiers toopublish et puis de le partager avec vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="06f1b-123">Again you'll want toopublish File Explorer tooRemoteApp and then share it with your users.</span></span>

> [!NOTE]
> <span data-ttu-id="06f1b-124">serveur de fichiers Hello doit être sur un réseau routable hello RemoteApp a été déployé dans.</span><span class="sxs-lookup"><span data-stu-id="06f1b-124">hello file server must be on hello routable network that RemoteApp was deployed into.</span></span>
> 
> 

## <a name="copy-files-tooonedrive-for-business"></a><span data-ttu-id="06f1b-125">Copier les fichiers tooOneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="06f1b-125">Copy files tooOneDrive for Business</span></span>
<span data-ttu-id="06f1b-126">Bien que vous ne pouvez pas activer hello OneDrive pour l’agent de synchronisation d’entreprise dans RemoteApp, vous pouvez toujours copier les fichiers à partir de votre tooOneDrive UPD for Business via un navigateur.</span><span class="sxs-lookup"><span data-stu-id="06f1b-126">Although you cannot enable hello OneDrive for Business sync agent in RemoteApp, you can still copy files from your UPD tooOneDrive for Business through a browser.</span></span> 

1. <span data-ttu-id="06f1b-127">Publication tooRemoteApp de l’Explorateur de fichiers et ensuite d’indiquer aux utilisateurs tooaccess hello fichiers grâce à cette application.</span><span class="sxs-lookup"><span data-stu-id="06f1b-127">Publish File Explorer tooRemoteApp and then tell users tooaccess hello files through that app.</span></span> 
2. <span data-ttu-id="06f1b-128">Il est plus simple tootransfer fichiers si elles sont compressées, donc les utilisateurs doivent créer un fichier .zip qui contienne tous les hello fichiers toomove tooOneDrive de l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="06f1b-128">It's easiest tootransfer files if they are compressed, so users should create a .zip file that contains all of hello files toomove tooOneDrive for Business.</span></span>
3. <span data-ttu-id="06f1b-129">Demander le portail d’utilisateurs toogo toohello Office 365, puis passez tooOneDrive et téléchargez le fichier .zip de hello.</span><span class="sxs-lookup"><span data-stu-id="06f1b-129">Ask users toogo toohello Office 365 portal, and then go tooOneDrive and upload hello .zip file.</span></span>

## <a name="copy-files-by-using-drive-redirection"></a><span data-ttu-id="06f1b-130">Copier des fichiers à l’aide de la redirection de lecteur</span><span class="sxs-lookup"><span data-stu-id="06f1b-130">Copy files by using drive redirection</span></span>
<span data-ttu-id="06f1b-131">Si vous avez activé [la redirection de lecteur](remoteapp-redirection.md), vous avez déjà créé un lecteur mappé pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="06f1b-131">If you have enabled [drive redirection](remoteapp-redirection.md), you have already created a mapped drive for your users.</span></span> <span data-ttu-id="06f1b-132">Dans ce cas, ils peuvent leurs fichiers sur le lecteur de hello redirigé zip et enregistrez-les tootheir PC local.</span><span class="sxs-lookup"><span data-stu-id="06f1b-132">In this case, they can zip their files on hello redirected drive and then save them tootheir local PC.</span></span>

## <a name="how-administrators-can-export-data"></a><span data-ttu-id="06f1b-133">Comment les administrateurs peuvent exporter des données</span><span class="sxs-lookup"><span data-stu-id="06f1b-133">How administrators can export data</span></span>

<span data-ttu-id="06f1b-134">Administre pour Azure RemoteApp peut exporter tous les disques de profil utilisateur (UPD) pour toutes les collections dans un stockage à l’aide d’Azure PowerShell de tooAzure abonnement applet de commande Export-AzureRemoteAppUserDisk.</span><span class="sxs-lookup"><span data-stu-id="06f1b-134">Administers for Azure RemoteApp can export all user profile disks (UPD) for all collections within a subscription tooAzure Storage using Azure PowerShell cmdlet, Export-AzureRemoteAppUserDisk.</span></span>  <span data-ttu-id="06f1b-135">Il n’existe aucune possibilité tooselect individuels UPD.</span><span class="sxs-lookup"><span data-stu-id="06f1b-135">There is no ability tooselect individual UPD's.</span></span>  <span data-ttu-id="06f1b-136">Lors de l’exécution de commande PowerShell de hello, chaque disque de l’utilisateur sera un 50 Go de taille de disque fixe et être exporté tooAzure stockage.</span><span class="sxs-lookup"><span data-stu-id="06f1b-136">When hello PowerShell command is executed, each user disk will be a 50gb in fixed disk size and be exported tooAzure storage.</span></span>  <span data-ttu-id="06f1b-137">Les coûts de stockage Azure sont immédiatement exposés pour ce stockage.</span><span class="sxs-lookup"><span data-stu-id="06f1b-137">Costs of Azure storage will incur immediately for this storage.</span></span>  <span data-ttu-id="06f1b-138">Lors de l’exécution de cette commande garantit il n’y a aucune session sinon hello exportation échoue.</span><span class="sxs-lookup"><span data-stu-id="06f1b-138">When running this command ensure there are no sessions otherwise hello export will fail.</span></span>

<span data-ttu-id="06f1b-139">Les disques de profil utilisateur pour les déploiements Azure RemoteApp joints à un domaine peuvent être réutilisés uniquement dans un déploiement de services Bureau à distance, et les déploiements non-joints à un domaine ne peuvent pas être utilisés.</span><span class="sxs-lookup"><span data-stu-id="06f1b-139">UPD's for domain joined Azure RemoteApp deployments can only be used again in an RDS deployment, non-domain joined deployments cannot be used.</span></span>  <span data-ttu-id="06f1b-140">Si ces disques seront utilisés dans un déploiement services Bureau à distance nous vous recommandons de toouse notre [scripts automatisés](https://github.com/arcadiahlyy/aramigration) qui sera exporter, de convertir et importer hello d’UPD un déploiement services Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="06f1b-140">If these disks will be used in an RDS deployment we recommend toouse our [automated scripts](https://github.com/arcadiahlyy/aramigration) that will export, convert, and import hello UPD's into an RDS deployment.</span></span>

