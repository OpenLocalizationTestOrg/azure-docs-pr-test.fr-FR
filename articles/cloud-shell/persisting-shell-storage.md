---
title: "fichiers aaaPersist dans Azure Cloud Shell (version préliminaire) | Documents Microsoft"
description: "Procédure pas à pas de conservation des fichiers avec Azure Cloud Shell."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: b230453d5551c545553d63559741950206e4f1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a><span data-ttu-id="f476f-103">Conserver des fichiers dans Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="f476f-103">Persist files in Azure Cloud Shell</span></span>
<span data-ttu-id="f476f-104">Interpréteur de commandes de nuage tire parti Azure fichier toopersist des fichiers de stockage entre les sessions.</span><span class="sxs-lookup"><span data-stu-id="f476f-104">Cloud Shell takes advantage of Azure File storage toopersist files across sessions.</span></span>

## <a name="set-up-a-clouddrive-file-share"></a><span data-ttu-id="f476f-105">Créer un partage de fichiers `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="f476f-105">Set up a `clouddrive` file share</span></span>
<span data-ttu-id="f476f-106">Au démarrage initial, Cloud Shell vous invite tooassociate un fichier nouveau ou existant partager les fichiers toopersist sessions.</span><span class="sxs-lookup"><span data-stu-id="f476f-106">On initial start, Cloud Shell prompts you tooassociate a new or existing file share toopersist files across sessions.</span></span>

### <a name="create-new-storage"></a><span data-ttu-id="f476f-107">Créer un stockage</span><span class="sxs-lookup"><span data-stu-id="f476f-107">Create new storage</span></span>

<span data-ttu-id="f476f-108">Lorsque vous utilisez des paramètres de base et que vous sélectionnez qu’un abonnement, Shell de Cloud crée trois ressources de votre part dans la région de hello pris en charge est le plus proche tooyou :</span><span class="sxs-lookup"><span data-stu-id="f476f-108">When you use basic settings and select only a subscription, Cloud Shell creates three resources on your behalf in hello supported region that's nearest tooyou:</span></span>
* <span data-ttu-id="f476f-109">Groupe de ressources : `cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="f476f-109">Resource group: `cloud-shell-storage-<region>`</span></span>
* <span data-ttu-id="f476f-110">Compte de stockage : `cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="f476f-110">Storage account: `cs<uniqueGuid>`</span></span>
* <span data-ttu-id="f476f-111">Partage de fichiers : `cs-<user>-<domain>-com-<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="f476f-111">File share: `cs-<user>-<domain>-com-<uniqueGuid>`</span></span>

![paramètre d’abonnement Hello](media/basic-storage.png)

<span data-ttu-id="f476f-113">partage de fichiers Hello monte comme `clouddrive` dans votre `$Home` active.</span><span class="sxs-lookup"><span data-stu-id="f476f-113">hello file share mounts as `clouddrive` in your `$Home` directory.</span></span> <span data-ttu-id="f476f-114">Bonjour partage de fichiers est également utilisé toostore une image de 5 Go est créée automatiquement pour vous et qui met à jour et persiste votre `$Home` active.</span><span class="sxs-lookup"><span data-stu-id="f476f-114">hello file share is also used toostore a 5-GB image that's created for you and that automatically updates and persists your `$Home` directory.</span></span> <span data-ttu-id="f476f-115">Il s’agit d’une action unique, et partage de fichiers hello monte automatiquement dans les sessions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="f476f-115">This is a one-time action, and hello file share mounts automatically in subsequent sessions.</span></span>

### <a name="use-existing-resources"></a><span data-ttu-id="f476f-116">Utiliser les ressources existantes</span><span class="sxs-lookup"><span data-stu-id="f476f-116">Use existing resources</span></span>

<span data-ttu-id="f476f-117">À l’aide de hello option avancée, vous pouvez associer des ressources existantes.</span><span class="sxs-lookup"><span data-stu-id="f476f-117">By using hello advanced option, you can associate existing resources.</span></span> <span data-ttu-id="f476f-118">Invite de commandes d’installation de stockage hello, sélectionnez **afficher les paramètres avancés** tooview des options supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="f476f-118">When hello storage setup prompt appears, select **Show advanced settings** tooview additional options.</span></span> <span data-ttu-id="f476f-119">Les partages de fichiers existant recevoir un toopersist d’image utilisateur de 5 Go votre `$Home` active.</span><span class="sxs-lookup"><span data-stu-id="f476f-119">Existing file shares receive a 5-GB user image toopersist your `$Home` directory.</span></span> <span data-ttu-id="f476f-120">déroulants Hello sont filtrés pour votre région Cloud Shell et comptes de stockage redondant local & géo-redondant.</span><span class="sxs-lookup"><span data-stu-id="f476f-120">hello drop-down menus are filtered for your Cloud Shell region and for local-redundant & geo-redundant storage accounts.</span></span>

![paramètre de groupe de ressources Hello](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a><span data-ttu-id="f476f-122">Restreindre la création de ressources avec une stratégie de ressource Azure</span><span class="sxs-lookup"><span data-stu-id="f476f-122">Restrict resource creation with an Azure resource policy</span></span>
<span data-ttu-id="f476f-123">Les comptes de stockage que vous créez dans Cloud Shell sont identifiés à l’aide de la balise `ms-resource-usage:azure-cloud-shell`.</span><span class="sxs-lookup"><span data-stu-id="f476f-123">Storage accounts that you create in Cloud Shell are tagged with `ms-resource-usage:azure-cloud-shell`.</span></span> <span data-ttu-id="f476f-124">Si vous souhaitez toodisallow les utilisateurs de créer des comptes de stockage dans un environnement de Cloud, créez un [stratégie de ressources Azure pour les balises](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) qui sont déclenchés par cette balise spécifique.</span><span class="sxs-lookup"><span data-stu-id="f476f-124">If you want toodisallow users from creating storage accounts in Cloud Shell, create an [Azure resource policy for tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) that are triggered by this specific tag.</span></span>

## <a name="how-cloud-shell-works"></a><span data-ttu-id="f476f-125">Fonctionnement de Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="f476f-125">How Cloud Shell works</span></span>
<span data-ttu-id="f476f-126">Shell de cloud enregistre les fichiers à la fois de hello méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f476f-126">Cloud Shell persists files through both of hello following methods:</span></span>
* <span data-ttu-id="f476f-127">Création d’une image de disque de votre `$Home` toopersist Active tous les contenus dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="f476f-127">Creating a disk image of your `$Home` directory toopersist all contents within hello directory.</span></span> <span data-ttu-id="f476f-128">image de disque Hello est enregistré dans votre partage de fichier spécifié en tant que `acc_<User>.img` à `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, et il synchronise automatiquement les modifications.</span><span class="sxs-lookup"><span data-stu-id="f476f-128">hello disk image is saved in your specified file share as `acc_<User>.img` at `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, and it automatically syncs changes.</span></span>

* <span data-ttu-id="f476f-129">Montage du partage de fichiers spécifié en tant que `clouddrive` dans votre répertoire `$Home` pour l’interaction directe avec le partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="f476f-129">Mounting your specified file share as `clouddrive` in your `$Home` directory for direct file share interaction.</span></span> <span data-ttu-id="f476f-130">`/Home/<User>/clouddrive`est mappé trop`fileshare.storage.windows.net/fileshare`.</span><span class="sxs-lookup"><span data-stu-id="f476f-130">`/Home/<User>/clouddrive` is mapped too`fileshare.storage.windows.net/fileshare`.</span></span>
 
> [!NOTE]
> <span data-ttu-id="f476f-131">Tous les fichiers figurant dans votre répertoire `$Home`, tels que les clés SSH, sont conservés dans l’image disque utilisateur qui est stockée dans votre partage de fichiers monté.</span><span class="sxs-lookup"><span data-stu-id="f476f-131">All files in your `$Home` directory, such as SSH keys, are persisted in your user disk image, which is stored in your mounted file share.</span></span> <span data-ttu-id="f476f-132">Appliquez les bonnes pratiques lors de la conservation d’informations dans votre répertoire `$Home` et votre partage de fichiers monté.</span><span class="sxs-lookup"><span data-stu-id="f476f-132">Apply best practices when you persist information in your `$Home` directory and mounted file share.</span></span>

## <a name="use-hello-clouddrive-command"></a><span data-ttu-id="f476f-133">Hello d’utilisation `clouddrive` commande</span><span class="sxs-lookup"><span data-stu-id="f476f-133">Use hello `clouddrive` command</span></span>
<span data-ttu-id="f476f-134">Avec Cloud, vous pouvez exécuter une commande appelée `clouddrive`, qui permet de vous toomanually mise à jour hello de partage de fichiers tooCloud monté de Shell.</span><span class="sxs-lookup"><span data-stu-id="f476f-134">With Cloud Shell, you can run a command called `clouddrive`, which enables you toomanually update hello file share that's mounted tooCloud Shell.</span></span>
<span data-ttu-id="f476f-135">![Exécution de la commande « clouddrive » hello](media/clouddrive-h.png)</span><span class="sxs-lookup"><span data-stu-id="f476f-135">![Running hello "clouddrive" command](media/clouddrive-h.png)</span></span>

## <a name="mount-a-new-clouddrive"></a><span data-ttu-id="f476f-136">Monter un nouveau `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="f476f-136">Mount a new `clouddrive`</span></span>

### <a name="prerequisites-for-manual-mounting"></a><span data-ttu-id="f476f-137">Prérequis pour le montage manuel</span><span class="sxs-lookup"><span data-stu-id="f476f-137">Prerequisites for manual mounting</span></span>
<span data-ttu-id="f476f-138">Vous pouvez mettre à jour de partage de fichiers hello associé Cloud Shell à l’aide de hello `clouddrive mount` commande.</span><span class="sxs-lookup"><span data-stu-id="f476f-138">You can update hello file share that's associated with Cloud Shell by using hello `clouddrive mount` command.</span></span>

<span data-ttu-id="f476f-139">Si vous montez un partage de fichiers existant, les comptes de stockage hello doivent être :</span><span class="sxs-lookup"><span data-stu-id="f476f-139">If you mount an existing file share, hello storage accounts must be:</span></span>
* <span data-ttu-id="f476f-140">Stockage redondant en local ou partages de fichiers toosupport stockage géo-redondant.</span><span class="sxs-lookup"><span data-stu-id="f476f-140">Locally-redundant storage or geo-redundant storage toosupport file shares.</span></span>
* <span data-ttu-id="f476f-141">Situés dans votre région affectée.</span><span class="sxs-lookup"><span data-stu-id="f476f-141">Located in your assigned region.</span></span> <span data-ttu-id="f476f-142">Lorsque vous êtes l’intégration, région de hello vous sont assignés toois répertoriées dans le nom de groupe de ressources hello `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="f476f-142">When you are onboarding, hello region you are assigned toois listed in hello resource group name `cloud-shell-storage-<region>`.</span></span>

### <a name="supported-storage-regions"></a><span data-ttu-id="f476f-143">Régions de stockage prises en charge</span><span class="sxs-lookup"><span data-stu-id="f476f-143">Supported storage regions</span></span>
<span data-ttu-id="f476f-144">Bonjour Azure fichiers doivent résider dans hello même région que hello Cloud Shell ordinateur que vous êtes le montage de leur.</span><span class="sxs-lookup"><span data-stu-id="f476f-144">hello Azure files must reside in hello same region as hello Cloud Shell machine that you're mounting them to.</span></span> <span data-ttu-id="f476f-145">Clusters de Shell cloud existent actuellement dans hello suivant régions :</span><span class="sxs-lookup"><span data-stu-id="f476f-145">Cloud Shell clusters currently exist in hello following regions:</span></span>
|<span data-ttu-id="f476f-146">Domaine</span><span class="sxs-lookup"><span data-stu-id="f476f-146">Area</span></span>|<span data-ttu-id="f476f-147">Région</span><span class="sxs-lookup"><span data-stu-id="f476f-147">Region</span></span>|
|---|---|
|<span data-ttu-id="f476f-148">Amérique</span><span class="sxs-lookup"><span data-stu-id="f476f-148">Americas</span></span>|<span data-ttu-id="f476f-149">Est des États-Unis, Sud du centre des États-Unis, Ouest des États-Unis</span><span class="sxs-lookup"><span data-stu-id="f476f-149">East US, South Central US, West US</span></span>|
|<span data-ttu-id="f476f-150">Europe</span><span class="sxs-lookup"><span data-stu-id="f476f-150">Europe</span></span>|<span data-ttu-id="f476f-151">Europe du Nord, Europe de l’Ouest</span><span class="sxs-lookup"><span data-stu-id="f476f-151">North Europe, West Europe</span></span>|
|<span data-ttu-id="f476f-152">Asie-Pacifique</span><span class="sxs-lookup"><span data-stu-id="f476f-152">Asia Pacific</span></span>|<span data-ttu-id="f476f-153">Inde-Centre, Sud-Est asiatique</span><span class="sxs-lookup"><span data-stu-id="f476f-153">India Central, Southeast Asia</span></span>|

### <a name="hello-clouddrive-mount-command"></a><span data-ttu-id="f476f-154">Hello `clouddrive mount` commande</span><span class="sxs-lookup"><span data-stu-id="f476f-154">hello `clouddrive mount` command</span></span>

> [!NOTE]
> <span data-ttu-id="f476f-155">Si vous êtes le montage d’un partage de fichiers, une nouvelle image de l’utilisateur est créée pour votre `$Home` active, car votre précédente `$Home` image est conservée dans le partage de fichiers hello précédente.</span><span class="sxs-lookup"><span data-stu-id="f476f-155">If you're mounting a new file share, a new user image is created for your `$Home` directory, because your previous `$Home` image is kept in hello previous file share.</span></span>

<span data-ttu-id="f476f-156">Exécutez hello `clouddrive mount` avec hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="f476f-156">Run hello `clouddrive mount` command with hello following parameters:</span></span>

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

<span data-ttu-id="f476f-157">l’exécution de plus de détails, tooview `clouddrive mount -h`, comme illustré ici :</span><span class="sxs-lookup"><span data-stu-id="f476f-157">tooview more details, run `clouddrive mount -h`, as shown here:</span></span>

![En cours d’exécution hello ' clouddrive mount'command](media/mount-h.png)

## <a name="unmount-clouddrive"></a><span data-ttu-id="f476f-159">Démonter `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="f476f-159">Unmount `clouddrive`</span></span>
<span data-ttu-id="f476f-160">Vous pouvez démonter un partage de fichiers tooCloud monté de Shell à tout moment.</span><span class="sxs-lookup"><span data-stu-id="f476f-160">You can unmount a file share that's mounted tooCloud Shell at any time.</span></span> <span data-ttu-id="f476f-161">Une fois que le partage de fichiers est démonté, vous serez invité à toomount un tooyour préalable du partage de fichier nouveau session suivante.</span><span class="sxs-lookup"><span data-stu-id="f476f-161">Once your file share is unmounted, you will be prompted toomount a new file share prior tooyour next session.</span></span>

<span data-ttu-id="f476f-162">tooremove un fichier de partage à partir de l’interpréteur de commandes de Cloud :</span><span class="sxs-lookup"><span data-stu-id="f476f-162">tooremove a file share from Cloud Shell:</span></span>
1. <span data-ttu-id="f476f-163">Exécutez `clouddrive unmount`.</span><span class="sxs-lookup"><span data-stu-id="f476f-163">Run `clouddrive unmount`.</span></span>
2. <span data-ttu-id="f476f-164">Accuser réception et confirmez les invites de hello.</span><span class="sxs-lookup"><span data-stu-id="f476f-164">Acknowledge and confirm hello prompts.</span></span>

<span data-ttu-id="f476f-165">Le partage de fichiers continue tooexist, sauf si vous la supprimiez manuellement.</span><span class="sxs-lookup"><span data-stu-id="f476f-165">Your file share will continue tooexist unless you delete it manually.</span></span> <span data-ttu-id="f476f-166">Cloud Shell ne fera plus de recherche pour ce partage de fichiers lors des sessions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="f476f-166">Cloud Shell will no longer search for this file share on subsequent sessions.</span></span>

<span data-ttu-id="f476f-167">l’exécution de plus de détails, tooview `clouddrive unmount -h`, comme illustré ici :</span><span class="sxs-lookup"><span data-stu-id="f476f-167">tooview more details, run `clouddrive unmount -h`, as shown here:</span></span>

![En cours d’exécution hello ' clouddrive unmount'command](media/unmount-h.png)

> [!WARNING]
> <span data-ttu-id="f476f-169">L’exécution de cette commande ne supprime pas de ressources.</span><span class="sxs-lookup"><span data-stu-id="f476f-169">Running this command will not delete any resources.</span></span> <span data-ttu-id="f476f-170">Suppression manuelle d’un groupe de ressources, le compte de stockage ou le partage de fichiers qui est mappé à tooCloud Shell supprimera définitivement votre `$Home` image de répertoire et tous les autres fichiers dans le partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="f476f-170">Manually deleting a resource group, storage account, or file share that is mapped tooCloud Shell will permanently delete your `$Home` directory image and any other files in your file share.</span></span> <span data-ttu-id="f476f-171">Il est impossible d’annuler cette opération.</span><span class="sxs-lookup"><span data-stu-id="f476f-171">This action cannot be undone.</span></span>

## <a name="list-clouddrive-file-shares"></a><span data-ttu-id="f476f-172">Répertorier les partages de fichiers `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="f476f-172">List `clouddrive` file shares</span></span>
<span data-ttu-id="f476f-173">toodiscover le partage de fichiers est monté en tant que `clouddrive`, exécutez hello `df` commande.</span><span class="sxs-lookup"><span data-stu-id="f476f-173">toodiscover which file share is mounted as `clouddrive`, run hello following `df` command.</span></span> 

<span data-ttu-id="f476f-174">tooclouddrive de chemin d’accès de fichier Hello affiche que votre nom de compte de stockage et partage de fichiers dans l’URL de hello.</span><span class="sxs-lookup"><span data-stu-id="f476f-174">hello file path tooclouddrive shows your storage account name and file share in hello URL.</span></span> <span data-ttu-id="f476f-175">Par exemple, `//storageaccountname.file.core.windows.net/filesharename`</span><span class="sxs-lookup"><span data-stu-id="f476f-175">For example, `//storageaccountname.file.core.windows.net/filesharename`</span></span>

```
justin@Azure:~$ df
Filesystem                                               1K-blocks     Used Available Use% Mounted on
overlay                                                   30428648 15585636  14826628  52% /
tmpfs                                                       986704        0    986704   0% /dev
tmpfs                                                       986704        0    986704   0% /sys/fs/cgroup
/dev/sda1                                                 30428648 15585636  14826628  52% /etc/hosts
shm                                                          65536        0     65536   0% /dev/shm
//mystoragename.file.core.windows.net/fileshareName        6291456  5242944   1048512  84% /usr/justin/clouddrive
/dev/loop0                                                 5160576   601652   4296780  13% /home/justin
```

## <a name="transfer-local-files-toocloud-shell"></a><span data-ttu-id="f476f-176">Transfert de fichiers locaux tooCloud Shell</span><span class="sxs-lookup"><span data-stu-id="f476f-176">Transfer local files tooCloud Shell</span></span>
<span data-ttu-id="f476f-177">Hello `clouddrive` se synchronise de répertoire avec le panneau de stockage portail Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f476f-177">hello `clouddrive` directory syncs with hello Azure portal storage blade.</span></span> <span data-ttu-id="f476f-178">Utilisez cette tooor de fichiers locaux tootransfer panneau à partir de votre partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="f476f-178">Use this blade tootransfer local files tooor from your file share.</span></span> <span data-ttu-id="f476f-179">Mise à jour des fichiers à partir d’un environnement de Cloud est répercutée dans le stockage de fichier hello GUI lors de l’actualisation du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="f476f-179">Updating files from within Cloud Shell is reflected in hello file storage GUI when you refresh hello blade.</span></span>

### <a name="download-files"></a><span data-ttu-id="f476f-180">Téléchargement de fichiers</span><span class="sxs-lookup"><span data-stu-id="f476f-180">Download files</span></span>

![Liste de fichiers locaux](media/download.png)
1. <span data-ttu-id="f476f-182">Bonjour portail Azure, passez le partage de fichiers monté toohello.</span><span class="sxs-lookup"><span data-stu-id="f476f-182">In hello Azure portal, go toohello mounted file share.</span></span>
2. <span data-ttu-id="f476f-183">Sélectionnez le fichier cible de hello.</span><span class="sxs-lookup"><span data-stu-id="f476f-183">Select hello target file.</span></span>
3. <span data-ttu-id="f476f-184">Sélectionnez hello **télécharger** bouton.</span><span class="sxs-lookup"><span data-stu-id="f476f-184">Select hello **Download** button.</span></span>

### <a name="upload-files"></a><span data-ttu-id="f476f-185">Charger des fichiers</span><span class="sxs-lookup"><span data-stu-id="f476f-185">Upload files</span></span>

![Toobe fichiers locaux téléchargé](media/upload.png)
1. <span data-ttu-id="f476f-187">Passez le partage de fichiers monté tooyour.</span><span class="sxs-lookup"><span data-stu-id="f476f-187">Go tooyour mounted file share.</span></span>
2. <span data-ttu-id="f476f-188">Sélectionnez hello **télécharger** bouton.</span><span class="sxs-lookup"><span data-stu-id="f476f-188">Select hello **Upload** button.</span></span>
3. <span data-ttu-id="f476f-189">Sélectionnez hello ou les fichiers que vous souhaitez tooupload.</span><span class="sxs-lookup"><span data-stu-id="f476f-189">Select hello file or files that you want tooupload.</span></span>
4. <span data-ttu-id="f476f-190">Confirmer le téléchargement de hello.</span><span class="sxs-lookup"><span data-stu-id="f476f-190">Confirm hello upload.</span></span>

<span data-ttu-id="f476f-191">Vous devez maintenant voir les fichiers hello qui sont accessibles dans votre `clouddrive` répertoire dans un environnement de Cloud.</span><span class="sxs-lookup"><span data-stu-id="f476f-191">You should now see hello files that are accessible in your `clouddrive` directory in Cloud Shell.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f476f-192">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f476f-192">Next steps</span></span>
[<span data-ttu-id="f476f-193">Démarrage rapide de Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="f476f-193">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="f476f-194">
[En savoir plus sur Azure Stockage Fichier](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span><span class="sxs-lookup"><span data-stu-id="f476f-194">
[Learn about Azure File storage](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span></span> <br><span data-ttu-id="f476f-195">
[En savoir plus sur les balises de stockage](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span><span class="sxs-lookup"><span data-stu-id="f476f-195">
[Learn about storage tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span></span> <br>
