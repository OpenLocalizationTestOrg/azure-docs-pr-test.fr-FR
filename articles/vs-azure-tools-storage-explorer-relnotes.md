---
title: "notes de version de l’Explorateur de stockage Azure (aperçu) aaaMicrosoft | Documents Microsoft"
description: "Notes de publication pour Microsoft Azure Storage Explorer (préversion)"
services: storage
documentationcenter: na
author: cawa
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.devlang: multiple
ms.topic: release-notes
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: cawa
ms.openlocfilehash: 44ff6dc8e2015f4eb71fa13098b832fbbf48ccac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a><span data-ttu-id="c4d0f-103">Notes de publication pour Microsoft Azure Storage Explorer (préversion)</span><span class="sxs-lookup"><span data-stu-id="c4d0f-103">Microsoft Azure Storage Explorer (Preview) release notes</span></span>

<span data-ttu-id="c4d0f-104">Cet article contient des notes pour Azure Storage Explorer 0.8.16 (version préliminaire) version, ainsi que les notes de publication pour les versions précédentes de la mise en production hello.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-104">This article contains hello release notes for Azure Storage Explorer 0.8.16 (Preview) release, as well as release notes for previous versions.</span></span>

<span data-ttu-id="c4d0f-105">[Explorateur de stockage Microsoft Azure (aperçu)](./vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome qui vous permet de travail tooeasily avec des données de stockage Azure sur Windows, Mac OS et Linux.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-105">[Microsoft Azure Storage Explorer (Preview)](./vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, macOS, and Linux.</span></span>

## <a name="version-0816-preview"></a><span data-ttu-id="c4d0f-106">Version 0.8.16 (préversion)</span><span class="sxs-lookup"><span data-stu-id="c4d0f-106">Version 0.8.16 (Preview)</span></span>
<span data-ttu-id="c4d0f-107">8/21/2017</span><span class="sxs-lookup"><span data-stu-id="c4d0f-107">8/21/2017</span></span>

### <a name="download-azure-storage-explorer-0816-preview"></a><span data-ttu-id="c4d0f-108">Télécharger l’explorateur de stockage Azure 0.8.16 (préversion)</span><span class="sxs-lookup"><span data-stu-id="c4d0f-108">Download Azure Storage Explorer 0.8.16 (Preview)</span></span>
- [<span data-ttu-id="c4d0f-109">Explorateur de stockage Azure 0.8.16 (préversion) pour Windows</span><span class="sxs-lookup"><span data-stu-id="c4d0f-109">Azure Storage Explorer 0.8.16 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=708343)
- [<span data-ttu-id="c4d0f-110">Explorateur de stockage Azure 0.8.16 (préversion) pour Mac</span><span class="sxs-lookup"><span data-stu-id="c4d0f-110">Azure Storage Explorer 0.8.16 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=708342)
- [<span data-ttu-id="c4d0f-111">Explorateur de stockage Azure 0.8.16 (préversion) pour Linux</span><span class="sxs-lookup"><span data-stu-id="c4d0f-111">Azure Storage Explorer 0.8.16 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a><span data-ttu-id="c4d0f-112">Nouveau</span><span class="sxs-lookup"><span data-stu-id="c4d0f-112">New</span></span>
* <span data-ttu-id="c4d0f-113">Lorsque vous ouvrez un objet blob, Explorateur de stockage vous demandera tooupload hello téléchargé fichier si une modification est détectée.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-113">When you open a blob, Storage Explorer will prompt you tooupload hello downloaded file if a change is detected</span></span>
* <span data-ttu-id="c4d0f-114">Expérience de connexion Azure Stack améliorée</span><span class="sxs-lookup"><span data-stu-id="c4d0f-114">Enhanced Azure Stack sign-in experience</span></span>
* <span data-ttu-id="c4d0f-115">Performances améliorées hello du téléchargement de nombreuses petits fichiers hello même temps</span><span class="sxs-lookup"><span data-stu-id="c4d0f-115">Improved hello performance of uploading/downloading many small files at hello same time</span></span>


### <a name="fixes"></a><span data-ttu-id="c4d0f-116">Correctifs</span><span class="sxs-lookup"><span data-stu-id="c4d0f-116">Fixes</span></span>
* <span data-ttu-id="c4d0f-117">Pour certains types d’objets blob, en choisissant trop « replace » pendant un conflit de téléchargement parfois entraînerait téléchargement hello en cours de redémarrage.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-117">For some blob types, choosing too"replace" during an upload conflict would sometimes result in hello upload being restarted.</span></span> 
* <span data-ttu-id="c4d0f-118">Dans la version 0.8.15, les chargements se bloquaient quelquefois à 99 %.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-118">In version 0.8.15, uploads would sometimes stall at 99%.</span></span>
* <span data-ttu-id="c4d0f-119">Lors du chargement de partage de fichiers tooa fichiers, si vous avez choisi le répertoire de tooa tooupload qui n’existe pas encore, le téléchargement échoue.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-119">When uploading files tooa file share, if you chose tooupload tooa directory which did not yet exist, your upload would fail.</span></span>
* <span data-ttu-id="c4d0f-120">L’explorateur de stockage créait de façon incorrecte des horodatages pour les requêtes de table et les signatures d’accès partagé.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-120">Storage Explorer was incorrectly generating time stamps for shared access signatures and table queries.</span></span>


<span data-ttu-id="c4d0f-121">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="c4d0f-121">Known Issues</span></span>
* <span data-ttu-id="c4d0f-122">Actuellement, l’utilisation d’une chaîne de connexion clé et nom ne fonctionne pas.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-122">Using a name and key connection string does not currently work.</span></span> <span data-ttu-id="c4d0f-123">Il sera résolu dans une prochaine version de hello.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-123">It will be fixed in hello next release.</span></span> <span data-ttu-id="c4d0f-124">En attendant, vous pouvez utiliser l’attachement avec le nom et la clé.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-124">Until then you can use attach with name and key.</span></span>
* <span data-ttu-id="c4d0f-125">Si vous essayez de tooopen un fichier avec un nom de fichier Windows non valide, le téléchargement de hello entraîne un erreur fichier non trouvé.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-125">If you try tooopen a file with an invalid Windows file name, hello download will result in a file not found error.</span></span>
* <span data-ttu-id="c4d0f-126">Après avoir cliqué sur « Annuler » sur une tâche, il peut prendre un certain temps pour toocancel de cette tâche.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-126">After clicking "Cancel" on a task, it may take a while for that task toocancel.</span></span> <span data-ttu-id="c4d0f-127">Il s’agit d’une limitation de la bibliothèque de nœud de stockage Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-127">This is a limitation of hello Azure Storage Node library.</span></span>
* <span data-ttu-id="c4d0f-128">Après avoir effectué un téléchargement de l’objet blob, onglet hello initiée par le téléchargement de hello est actualisé.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-128">After completing a blob upload, hello tab which initiated hello upload is refreshed.</span></span> <span data-ttu-id="c4d0f-129">Cela est une modification du comportement précédent et entraîne également vous toobe pris nouveau conteneur hello dans toohello racine.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-129">This is a change from previous behavior, and will also cause you toobe taken back toohello root of hello container you are in.</span></span>
* <span data-ttu-id="c4d0f-130">Si vous choisissez hello mauvais code confidentiel de carte à puce/certificat, vous devez toorestart dans l’ordre toohave Explorateur de stockage oubliez cette décision.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-130">If you choose hello wrong PIN/Smartcard certificate, then you will need toorestart in order toohave Storage Explorer forget that decision.</span></span>
* <span data-ttu-id="c4d0f-131">Panneau de paramètres de compte Hello peut indiquer que vous avez besoin d’abonnements de toofilter tooreenter informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-131">hello account settings panel may show that you need tooreenter credentials toofilter subscriptions.</span></span>
* <span data-ttu-id="c4d0f-132">Les captures instantanées ne sont pas conservées lorsque les blobs sont renommés (individuellement ou dans un conteneur d’objets blob renommé).</span><span class="sxs-lookup"><span data-stu-id="c4d0f-132">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="c4d0f-133">Lors d’un changement de nom, toutes les autres propriétés et métadonnées des objets blob, fichiers et entités sont conservées.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-133">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="c4d0f-134">Bien que Azure Stack ne prend actuellement pas en charge les partages de fichiers, un nœud de partages de fichiers apparaît toujours sous un compte de stockage d’Azure Stack joint.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-134">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span>
* <span data-ttu-id="c4d0f-135">Pour les utilisateurs sur Ubuntu 14.04, vous devez tooensure GCC est toodate - cela est possible en exécutant hello suivant de commandes, puis le redémarrage de votre ordinateur :</span><span class="sxs-lookup"><span data-stu-id="c4d0f-135">For users on Ubuntu 14.04, you will need tooensure GCC is up toodate - this can be done by running hello following commands, and then restarting your machine:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* <span data-ttu-id="c4d0f-136">Pour les utilisateurs sur Ubuntu 17.04, vous devez tooinstall GConf - cela hello suivant de commandes, puis le redémarrage de votre ordinateur en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="c4d0f-136">For users on Ubuntu 17.04, you will need tooinstall GConf - this can be done by running hello following commands, and then restarting your machine:</span></span>

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a><span data-ttu-id="c4d0f-137">Version 0.8.14 (aperçu)</span><span class="sxs-lookup"><span data-stu-id="c4d0f-137">Version 0.8.14 (Preview)</span></span>
<span data-ttu-id="c4d0f-138">06/22/2017</span><span class="sxs-lookup"><span data-stu-id="c4d0f-138">06/22/2017</span></span>

### <a name="download-azure-storage-explorer-0814-preview"></a><span data-ttu-id="c4d0f-139">Télécharger Azure Storage Explorer 0.8.14 (préversion)</span><span class="sxs-lookup"><span data-stu-id="c4d0f-139">Download Azure Storage Explorer 0.8.14 (Preview)</span></span>
* [<span data-ttu-id="c4d0f-140">Télécharger l’explorateur de stockage Azure 0.8.14 (aperçu) pour Windows</span><span class="sxs-lookup"><span data-stu-id="c4d0f-140">Download Azure Storage Explorer 0.8.14 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=809306)
* [<span data-ttu-id="c4d0f-141">Télécharger Azure Storage Explorer 0.8.14 (préversion) pour Mac</span><span class="sxs-lookup"><span data-stu-id="c4d0f-141">Download Azure Storage Explorer 0.8.14 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=809307)
* [<span data-ttu-id="c4d0f-142">Télécharger l’explorateur de stockage Azure 0.8.14 (aperçu) pour Linux</span><span class="sxs-lookup"><span data-stu-id="c4d0f-142">Download Azure Storage Explorer 0.8.14 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a><span data-ttu-id="c4d0f-143">Nouveau</span><span class="sxs-lookup"><span data-stu-id="c4d0f-143">New</span></span>

* <span data-ttu-id="c4d0f-144">Mise à jour too1.7.2 de version électronique dans parti de tootake d’ordre de plusieurs mises à jour critiques</span><span class="sxs-lookup"><span data-stu-id="c4d0f-144">Updated Electron version too1.7.2 in order tootake advantage of several critical security updates</span></span>
* <span data-ttu-id="c4d0f-145">Vous pouvez maintenant accéder rapidement aux guide de dépannage en ligne hello à partir du menu d’aide hello</span><span class="sxs-lookup"><span data-stu-id="c4d0f-145">You can now quickly access hello online troubleshooting guide from hello help menu</span></span>
* <span data-ttu-id="c4d0f-146">[Guide][2] de dépannage de Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="c4d0f-146">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="c4d0f-147">[Instructions] [ 3] sur la connexion d’abonnement de Azure pile tooan</span><span class="sxs-lookup"><span data-stu-id="c4d0f-147">[Instructions][3] on connecting tooan Azure Stack subscription</span></span>

### <a name="known-issues"></a><span data-ttu-id="c4d0f-148">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="c4d0f-148">Known Issues</span></span>

* <span data-ttu-id="c4d0f-149">Boutons de la boîte de dialogue de confirmation à dossier hello delete n’inscrivez pas avec les clics de souris hello sur Linux.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-149">Buttons on hello delete folder confirmation dialog don't register with hello mouse clicks on Linux.</span></span> <span data-ttu-id="c4d0f-150">Solution de contournement est la clé d’entrée toouse hello</span><span class="sxs-lookup"><span data-stu-id="c4d0f-150">Workaround is toouse hello Enter key</span></span>
* <span data-ttu-id="c4d0f-151">Si vous choisissez hello mauvais code confidentiel de carte à puce/certificat, vous devez toorestart dans l’ordre toohave Explorateur de stockage oublier la décision de hello</span><span class="sxs-lookup"><span data-stu-id="c4d0f-151">If you choose hello wrong PIN/Smartcard certificate then you will need toorestart in order toohave Storage Explorer forget hello decision</span></span>
* <span data-ttu-id="c4d0f-152">Plus de 3 groupes des objets BLOB ou des fichiers de téléchargement à hello même temps peut provoquer des erreurs</span><span class="sxs-lookup"><span data-stu-id="c4d0f-152">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="c4d0f-153">Panneau de paramètres de compte Hello peut indiquer que vous avez besoin d’informations d’identification tooreenter dans les abonnements toofilter de commande</span><span class="sxs-lookup"><span data-stu-id="c4d0f-153">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="c4d0f-154">Les captures instantanées ne sont pas conservées lorsque les blobs sont renommés (individuellement ou dans un conteneur d’objets blob renommé).</span><span class="sxs-lookup"><span data-stu-id="c4d0f-154">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="c4d0f-155">Lors d’un changement de nom, toutes les autres propriétés et métadonnées des objets blob, fichiers et entités sont conservées.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-155">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="c4d0f-156">Bien qu’Azure Stack ne prend actuellement pas en charge les partages de fichiers, un nœud de partages de fichiers apparaît toujours sous un compte de stockage d’Azure Stack joint.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-156">Although Azure Stack doesn't currently support File Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="c4d0f-157">Ubuntu 14.04 installation besoins gcc version mise à jour ou mise à niveau – tooupgrade d’étapes sont répertoriées ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c4d0f-157">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a><span data-ttu-id="c4d0f-158">Versions précédentes</span><span class="sxs-lookup"><span data-stu-id="c4d0f-158">Previous releases</span></span>

* [<span data-ttu-id="c4d0f-159">Version 0.8.13</span><span class="sxs-lookup"><span data-stu-id="c4d0f-159">Version 0.8.13</span></span>](#version-0813)
* [<span data-ttu-id="c4d0f-160">Version 0.8.12 / 0.8.11 / 0.8.10</span><span class="sxs-lookup"><span data-stu-id="c4d0f-160">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>](#version-0812--0811--0810)
* [<span data-ttu-id="c4d0f-161">Version 0.8.9 / 0.8.8</span><span class="sxs-lookup"><span data-stu-id="c4d0f-161">Version 0.8.9 / 0.8.8</span></span>](#version-089--088)
* [<span data-ttu-id="c4d0f-162">Version 0.8.7</span><span class="sxs-lookup"><span data-stu-id="c4d0f-162">Version 0.8.7</span></span>](#version-087)
* [<span data-ttu-id="c4d0f-163">Version 0.8.6</span><span class="sxs-lookup"><span data-stu-id="c4d0f-163">Version 0.8.6</span></span>](#version-086)
* [<span data-ttu-id="c4d0f-164">Version 0.8.5</span><span class="sxs-lookup"><span data-stu-id="c4d0f-164">Version 0.8.5</span></span>](#version-085)
* [<span data-ttu-id="c4d0f-165">Version 0.8.4</span><span class="sxs-lookup"><span data-stu-id="c4d0f-165">Version 0.8.4</span></span>](#version-084)
* [<span data-ttu-id="c4d0f-166">Version 0.8.3</span><span class="sxs-lookup"><span data-stu-id="c4d0f-166">Version 0.8.3</span></span>](#version-083)
* [<span data-ttu-id="c4d0f-167">Version 0.8.2</span><span class="sxs-lookup"><span data-stu-id="c4d0f-167">Version 0.8.2</span></span>](#version-082)
* [<span data-ttu-id="c4d0f-168">Version 0.8.0</span><span class="sxs-lookup"><span data-stu-id="c4d0f-168">Version 0.8.0</span></span>](#version-080)
* [<span data-ttu-id="c4d0f-169">Version 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="c4d0f-169">Version 0.7.20160509.0</span></span>](#version-07201605090)
* [<span data-ttu-id="c4d0f-170">Version 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="c4d0f-170">Version 0.7.20160325.0</span></span>](#version-07201603250)
* [<span data-ttu-id="c4d0f-171">Version 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="c4d0f-171">Version 0.7.20160129.1</span></span>](#version-07201601291)
* [<span data-ttu-id="c4d0f-172">Version 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="c4d0f-172">Version 0.7.20160105.0</span></span>](#version-07201601050)
* [<span data-ttu-id="c4d0f-173">Version 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="c4d0f-173">Version 0.7.20151116.0</span></span>](#version-07201511160)


### <a name="version-0813"></a><span data-ttu-id="c4d0f-174">Version 0.8.13</span><span class="sxs-lookup"><span data-stu-id="c4d0f-174">Version 0.8.13</span></span>
<span data-ttu-id="c4d0f-175">05/12/2017</span><span class="sxs-lookup"><span data-stu-id="c4d0f-175">05/12/2017</span></span>

#### <a name="new"></a><span data-ttu-id="c4d0f-176">Nouveau</span><span class="sxs-lookup"><span data-stu-id="c4d0f-176">New</span></span>

* <span data-ttu-id="c4d0f-177">[Guide][2] de dépannage de Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="c4d0f-177">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="c4d0f-178">[Instructions] [ 3] sur la connexion d’abonnement de Azure pile tooan</span><span class="sxs-lookup"><span data-stu-id="c4d0f-178">[Instructions][3] on connecting tooan Azure Stack subscription</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4d0f-179">Correctifs</span><span class="sxs-lookup"><span data-stu-id="c4d0f-179">Fixes</span></span>

* <span data-ttu-id="c4d0f-180">Problème résolu : le chargement du fichier peut provoquer très probablement une erreur de mémoire insuffisante</span><span class="sxs-lookup"><span data-stu-id="c4d0f-180">Fixed: File upload had a high chance of causing an out of memory error</span></span>
* <span data-ttu-id="c4d0f-181">Problème résolu : vous pouvez maintenant vous connecter avec le code PIN/carte à puce</span><span class="sxs-lookup"><span data-stu-id="c4d0f-181">Fixed: You can now sign in with PIN/Smartcard</span></span>
* <span data-ttu-id="c4d0f-182">Problème résolu : l’ouverture dans le portail fonctionne à présent avec Azure Chine, Azure Allemagne, Azure US Government et Azure Stack</span><span class="sxs-lookup"><span data-stu-id="c4d0f-182">Fixed: Open in Portal now works with Azure China, Azure Germany, Azure US Government, and Azure Stack</span></span>
* <span data-ttu-id="c4d0f-183">Problème résolu : Lors du téléchargement d’un conteneur d’objets blob tooa dossier, une erreur « Opération non conforme » se produisait parfois</span><span class="sxs-lookup"><span data-stu-id="c4d0f-183">Fixed: While uploading a folder tooa blob container, an "Illegal operation" error would sometimes occur</span></span>
* <span data-ttu-id="c4d0f-184">Problème résolu : sélectionner tout est désactivé lors de gestion des instantanés</span><span class="sxs-lookup"><span data-stu-id="c4d0f-184">Fixed: Select all was disabled while managing snapshots</span></span>
* <span data-ttu-id="c4d0f-185">Problème résolu : hello des métadonnées de l’objet blob de base hello risquent d’être écrasées après affichage des propriétés hello ses instantanés</span><span class="sxs-lookup"><span data-stu-id="c4d0f-185">Fixed: hello metadata of hello base blob might get overwritten after viewing hello properties of its snapshots</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c4d0f-186">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="c4d0f-186">Known Issues</span></span>

* <span data-ttu-id="c4d0f-187">Si vous choisissez hello mauvais code confidentiel de carte à puce/certificat, vous devez toorestart dans l’ordre toohave Explorateur de stockage oublier la décision de hello</span><span class="sxs-lookup"><span data-stu-id="c4d0f-187">If you choose hello wrong PIN/Smartcard certificate then you will need toorestart in order toohave Storage Explorer forget hello decision</span></span>
* <span data-ttu-id="c4d0f-188">Alors que le zoom avant ou arrière, niveau de zoom hello peut réinitialiser momentanément toohello au niveau de la valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="c4d0f-188">While zoomed in or out, hello zoom level may momentarily reset toohello default level</span></span>
* <span data-ttu-id="c4d0f-189">Plus de 3 groupes des objets BLOB ou des fichiers de téléchargement à hello même temps peut provoquer des erreurs</span><span class="sxs-lookup"><span data-stu-id="c4d0f-189">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="c4d0f-190">Panneau de paramètres de compte Hello peut indiquer que vous avez besoin d’informations d’identification tooreenter dans les abonnements toofilter de commande</span><span class="sxs-lookup"><span data-stu-id="c4d0f-190">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="c4d0f-191">Les captures instantanées ne sont pas conservées lorsque les blobs sont renommés (individuellement ou dans un conteneur d’objets blob renommé).</span><span class="sxs-lookup"><span data-stu-id="c4d0f-191">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="c4d0f-192">Lors d’un changement de nom, toutes les autres propriétés et métadonnées des objets blob, fichiers et entités sont conservées.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-192">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="c4d0f-193">Bien que Azure Stack ne prend actuellement pas en charge les partages de fichiers, un nœud de partages de fichiers apparaît toujours sous un compte de stockage d’Azure Stack joint.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-193">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="c4d0f-194">Ubuntu 14.04 installation besoins gcc version mise à jour ou mise à niveau – tooupgrade d’étapes sont répertoriées ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c4d0f-194">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a><span data-ttu-id="c4d0f-195">Version 0.8.12 / 0.8.11 / 0.8.10</span><span class="sxs-lookup"><span data-stu-id="c4d0f-195">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>
<span data-ttu-id="c4d0f-196">04/07/2017</span><span class="sxs-lookup"><span data-stu-id="c4d0f-196">04/07/2017</span></span>

#### <a name="new"></a><span data-ttu-id="c4d0f-197">Nouveau</span><span class="sxs-lookup"><span data-stu-id="c4d0f-197">New</span></span>

* <span data-ttu-id="c4d0f-198">Explorateur de stockage se ferme désormais automatiquement lorsque vous installez une mise à jour à partir de la notification de mise à jour hello</span><span class="sxs-lookup"><span data-stu-id="c4d0f-198">Storage Explorer will now automatically close when you install an update from hello update notification</span></span>
* <span data-ttu-id="c4d0f-199">L’accès rapide sur place fournit une expérience améliorée pour utiliser vos ressources fréquemment sollicitées</span><span class="sxs-lookup"><span data-stu-id="c4d0f-199">In-place quick access provides an enhanced experience for working with your frequently accessed resources</span></span>
* <span data-ttu-id="c4d0f-200">Dans l’éditeur de conteneur d’objets Blob hello, vous pouvez maintenant voir quel ordinateur virtuel auquel appartient un objet blob loué</span><span class="sxs-lookup"><span data-stu-id="c4d0f-200">In hello Blob Container editor, you can now see which virtual machine a leased blob belongs to</span></span>
* <span data-ttu-id="c4d0f-201">Vous pouvez désormais réduire le panneau de gauche de hello</span><span class="sxs-lookup"><span data-stu-id="c4d0f-201">You can now collapse hello left side panel</span></span>
* <span data-ttu-id="c4d0f-202">Découverte maintenant s’exécute sur hello même temps en tant que téléchargement</span><span class="sxs-lookup"><span data-stu-id="c4d0f-202">Discovery now runs at hello same time as download</span></span>
* <span data-ttu-id="c4d0f-203">Utilisation des statistiques Bonjour conteneur d’objets Blob, de partage de fichiers et de Table éditeurs toosee hello taille de votre ressource ou de la sélection</span><span class="sxs-lookup"><span data-stu-id="c4d0f-203">Use Statistics in hello Blob Container, File Share, and Table editors toosee hello size of your resource or selection</span></span>
* <span data-ttu-id="c4d0f-204">Vous pouvez maintenant tooAzure de connexion dans Active Directory (AAD) basée sur les comptes Azure pile.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-204">You can now sign-in tooAzure Active Directory (AAD) based Azure Stack accounts.</span></span> 
* <span data-ttu-id="c4d0f-205">Vous pouvez à présent les comptes de stockage de plus de 32 Mo tooPremium les fichiers d’archives de téléchargement</span><span class="sxs-lookup"><span data-stu-id="c4d0f-205">You can now upload archive files over 32MB tooPremium storage accounts</span></span>
* <span data-ttu-id="c4d0f-206">Prise en charge de l’accessibilité améliorée</span><span class="sxs-lookup"><span data-stu-id="c4d0f-206">Improved accessibility support</span></span>
* <span data-ttu-id="c4d0f-207">Vous pouvez maintenant ajouter approuvé Base-64 encodé de certificats X.509 SSL en accédant tooEdit -&gt; les certificats SSL -&gt; les certificats d’importation</span><span class="sxs-lookup"><span data-stu-id="c4d0f-207">You can now add trusted Base-64 encoded X.509 SSL certificates by going tooEdit -&gt; SSL Certificates -&gt; Import Certificates</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4d0f-208">Correctifs</span><span class="sxs-lookup"><span data-stu-id="c4d0f-208">Fixes</span></span>

* <span data-ttu-id="c4d0f-209">Problème résolu : après l’actualisation des informations d’identification d’un compte, arborescence hello est parfois pas actualiser automatiquement</span><span class="sxs-lookup"><span data-stu-id="c4d0f-209">Fixed: after refreshing an account's credentials, hello tree view would sometimes not automatically refresh</span></span>
* <span data-ttu-id="c4d0f-210">Problème résolu : générer une SAP pour les tables et les files d’attente de l’émulateur peut entraîner une URL non valide</span><span class="sxs-lookup"><span data-stu-id="c4d0f-210">Fixed: generating a SAS for emulator queues and tables would result in an invalid URL</span></span>
* <span data-ttu-id="c4d0f-211">Problème résolu : les comptes de stockage premium peuvent maintenant être développés lorsqu’un proxy est activé</span><span class="sxs-lookup"><span data-stu-id="c4d0f-211">Fixed: premium storage accounts can now be expanded while a proxy is enabled</span></span>
* <span data-ttu-id="c4d0f-212">Problème résolu : hello bouton Appliquer sur les comptes hello page de gestion ne fonctionnera pas si vous aviez 1 ou 0 comptes sélectionnés</span><span class="sxs-lookup"><span data-stu-id="c4d0f-212">Fixed: hello apply button on hello accounts management page would not work if you had 1 or 0 accounts selected</span></span>
* <span data-ttu-id="c4d0f-213">Problème résolu : le téléchargement d’objets blob qui nécessitent des résolutions de conflit peut échouer - résolu dans 0.8.11</span><span class="sxs-lookup"><span data-stu-id="c4d0f-213">Fixed: uploading blobs that require conflict resolutions may fail - fixed in 0.8.11</span></span> 
* <span data-ttu-id="c4d0f-214">Problème résolu : l’envoi de commentaires a été interrompu dans 0.8.11 - résolu dans 0.8.12</span><span class="sxs-lookup"><span data-stu-id="c4d0f-214">Fixed: sending feedback was broken in 0.8.11 - fixed in 0.8.12</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="c4d0f-215">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="c4d0f-215">Known Issues</span></span>

* <span data-ttu-id="c4d0f-216">Après la mise à niveau too0.8.10, vous devez toorefresh toutes vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-216">After upgrading too0.8.10, you will need toorefresh all of your credentials.</span></span>
* <span data-ttu-id="c4d0f-217">Alors que le zoom avant ou arrière, niveau de zoom hello peut réinitialiser momentanément toohello au niveau de la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-217">While zoomed in or out, hello zoom level may momentarily reset toohello default level.</span></span>
* <span data-ttu-id="c4d0f-218">Plus de 3 groupes des objets BLOB ou des fichiers de téléchargement à hello même temps peut provoquer des erreurs.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-218">Having more than 3 groups of blobs or files uploading at hello same time may cause errors.</span></span>
* <span data-ttu-id="c4d0f-219">Panneau de paramètres de compte Hello peut indiquer que vous avez besoin d’informations d’identification tooreenter dans les abonnements toofilter de commande.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-219">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions.</span></span>
* <span data-ttu-id="c4d0f-220">Les captures instantanées ne sont pas conservées lorsque les blobs sont renommés (individuellement ou dans un conteneur d’objets blob renommé).</span><span class="sxs-lookup"><span data-stu-id="c4d0f-220">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="c4d0f-221">Lors d’un changement de nom, toutes les autres propriétés et métadonnées des objets blob, fichiers et entités sont conservées.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-221">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="c4d0f-222">Bien que Azure Stack ne prend actuellement pas en charge les partages de fichiers, un nœud de partages de fichiers apparaît toujours sous un compte de stockage d’Azure Stack joint.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-222">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="c4d0f-223">Ubuntu 14.04 installation besoins gcc version mise à jour ou mise à niveau – tooupgrade d’étapes sont répertoriées ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c4d0f-223">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a><span data-ttu-id="c4d0f-224">Version 0.8.9 / 0.8.8</span><span class="sxs-lookup"><span data-stu-id="c4d0f-224">Version 0.8.9 / 0.8.8</span></span>
<span data-ttu-id="c4d0f-225">02/23/2017</span><span class="sxs-lookup"><span data-stu-id="c4d0f-225">02/23/2017</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="c4d0f-226">Nouveau</span><span class="sxs-lookup"><span data-stu-id="c4d0f-226">New</span></span>

* <span data-ttu-id="c4d0f-227">Explorateur de stockage 0.8.9 téléchargera automatiquement version la plus récente hello pour les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-227">Storage Explorer 0.8.9 will automatically download hello latest version for updates.</span></span>
* <span data-ttu-id="c4d0f-228">Correctif : à l’aide d’un portail généré tooattach URI SAS qu'un compte de stockage entraînerait une erreur.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-228">Hotfix: using a portal generated SAS URI tooattach a storage account would result in an error.</span></span>
* <span data-ttu-id="c4d0f-229">Vous pouvez désormais créer, gérer et promouvoir des instantanés d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-229">You can now create, manage, and promote blob snapshots.</span></span>
* <span data-ttu-id="c4d0f-230">Vous pouvez désormais vous connecter dans les comptes de tooAzure en Chine, Azure situés en Allemagne et Azure du gouvernement.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-230">You can now sign in tooAzure China, Azure Germany, and Azure US Government accounts.</span></span>
* <span data-ttu-id="c4d0f-231">Vous pouvez maintenant modifier le niveau de zoom hello.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-231">You can now change hello zoom level.</span></span> <span data-ttu-id="c4d0f-232">Utiliser les options de hello hello tooZoom de menu vue en Zoom arrière et réinitialiser le Zoom.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-232">Use hello options in hello View menu tooZoom In, Zoom Out, and Reset Zoom.</span></span>
* <span data-ttu-id="c4d0f-233">Les caractères Unicode sont désormais pris en charge dans les métadonnées de l’utilisateur pour les fichiers et les objets blob.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-233">Unicode characters are now supported in user metadata for blobs and files.</span></span>
* <span data-ttu-id="c4d0f-234">Améliorations de l’accessibilité.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-234">Accessibility improvements.</span></span>
* <span data-ttu-id="c4d0f-235">notes de publication de la version suivante Hello peuvent être affichés à partir de la notification de mise à jour hello.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-235">hello next version's release notes can be viewed from hello update notification.</span></span> <span data-ttu-id="c4d0f-236">Vous pouvez également afficher hello notes de publication à partir du menu d’aide hello.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-236">You can also view hello current release notes from hello Help menu.</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4d0f-237">Correctifs</span><span class="sxs-lookup"><span data-stu-id="c4d0f-237">Fixes</span></span>

* <span data-ttu-id="c4d0f-238">Problème résolu : numéro de version hello s’affiche désormais correctement dans le panneau de configuration sur Windows</span><span class="sxs-lookup"><span data-stu-id="c4d0f-238">Fixed: hello version number is now correctly displayed in Control Panel on Windows</span></span>
* <span data-ttu-id="c4d0f-239">Problème résolu : recherche n’est plus limitée too50, 000 nœuds</span><span class="sxs-lookup"><span data-stu-id="c4d0f-239">Fixed: search is no longer limited too50,000 nodes</span></span>
* <span data-ttu-id="c4d0f-240">Problème résolu : partage de fichiers de téléchargement tooa tourné indéfiniment si le répertoire de destination hello n’existait pas</span><span class="sxs-lookup"><span data-stu-id="c4d0f-240">Fixed: upload tooa file share spun forever if hello destination directory did not already exist</span></span>
* <span data-ttu-id="c4d0f-241">Problème résolu : stabilité améliorée pour de longs chargements et téléchargements</span><span class="sxs-lookup"><span data-stu-id="c4d0f-241">Fixed: improved stability for long uploads and downloads</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c4d0f-242">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="c4d0f-242">Known Issues</span></span>

* <span data-ttu-id="c4d0f-243">Alors que le zoom avant ou arrière, niveau de zoom hello peut réinitialiser momentanément toohello au niveau de la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-243">While zoomed in or out, hello zoom level may momentarily reset toohello default level.</span></span>
* <span data-ttu-id="c4d0f-244">L’Accès rapide fonctionne uniquement avec les éléments basés sur l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-244">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="c4d0f-245">Les ressources locales ou attachées par le biais d’une clé ou d’un jeton SAP ne sont pas prises en charge dans cette version.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-245">Local resources or resources attached via key or SAS token are not supported in this release.</span></span>
* <span data-ttu-id="c4d0f-246">Accès rapide peut prendre quelques secondes toonavigate toohello ressource cible, selon le nombre de ressources.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-246">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have.</span></span>
* <span data-ttu-id="c4d0f-247">Plus de 3 groupes des objets BLOB ou des fichiers de téléchargement à hello même temps peut provoquer des erreurs.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-247">Having more than 3 groups of blobs or files uploading at hello same time may cause errors.</span></span>

<span data-ttu-id="c4d0f-248">12/16/2016</span><span class="sxs-lookup"><span data-stu-id="c4d0f-248">12/16/2016</span></span>
### <a name="version-087"></a><span data-ttu-id="c4d0f-249">Version 0.8.7</span><span class="sxs-lookup"><span data-stu-id="c4d0f-249">Version 0.8.7</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="c4d0f-250">Nouveau</span><span class="sxs-lookup"><span data-stu-id="c4d0f-250">New</span></span>

* <span data-ttu-id="c4d0f-251">Vous pouvez choisir comment conflits tooresolve au début de hello d’une mise à jour, télécharger ou copier la session dans la fenêtre des activités hello</span><span class="sxs-lookup"><span data-stu-id="c4d0f-251">You can choose how tooresolve conflicts at hello beginning of an update, download or copy session in hello Activities window</span></span>
* <span data-ttu-id="c4d0f-252">Placez le curseur sur un onglet toosee hello chemin d’accès complet de la ressource de stockage hello</span><span class="sxs-lookup"><span data-stu-id="c4d0f-252">Hover over a tab toosee hello full path of hello storage resource</span></span>
* <span data-ttu-id="c4d0f-253">Lorsque vous cliquez sur un onglet, il se synchronise avec son emplacement dans le volet de navigation de gauche hello</span><span class="sxs-lookup"><span data-stu-id="c4d0f-253">When you click on a tab, it synchronizes with its location in hello left side navigation pane</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4d0f-254">Correctifs</span><span class="sxs-lookup"><span data-stu-id="c4d0f-254">Fixes</span></span>

* <span data-ttu-id="c4d0f-255">Problème résolu : Storage Explorer est désormais une application approuvée sur Mac</span><span class="sxs-lookup"><span data-stu-id="c4d0f-255">Fixed: Storage Explorer is now a trusted app on Mac</span></span>
* <span data-ttu-id="c4d0f-256">Problème résolu : Ubuntu 14.04 est de nouveau pris en charge</span><span class="sxs-lookup"><span data-stu-id="c4d0f-256">Fixed: Ubuntu 14.04 is again supported</span></span>
* <span data-ttu-id="c4d0f-257">Problème résolu : Parfois hello Ajouter compte UI clignote lors du chargement des abonnements</span><span class="sxs-lookup"><span data-stu-id="c4d0f-257">Fixed: Sometimes hello add account UI flashes when loading subscriptions</span></span>
* <span data-ttu-id="c4d0f-258">Problème résolu : Parfois pas toutes les ressources de stockage ont été répertoriés dans le volet de navigation de gauche hello</span><span class="sxs-lookup"><span data-stu-id="c4d0f-258">Fixed: Sometimes not all storage resources were listed in hello left side navigation pane</span></span>
* <span data-ttu-id="c4d0f-259">Problème résolu : hello volet Actions parfois affiche les actions vides</span><span class="sxs-lookup"><span data-stu-id="c4d0f-259">Fixed: hello action pane sometimes displayed empty actions</span></span>
* <span data-ttu-id="c4d0f-260">Problème résolu : la taille de la fenêtre de session de la dernière fermé de hello hello est maintenant conservé</span><span class="sxs-lookup"><span data-stu-id="c4d0f-260">Fixed: hello window size from hello last closed session is now retained</span></span>
* <span data-ttu-id="c4d0f-261">Résolution : Vous pouvez ouvrir plusieurs onglets pour hello même ressource à l’aide du menu contextuel de hello</span><span class="sxs-lookup"><span data-stu-id="c4d0f-261">Fixed: You can open multiple tabs for hello same resource using hello context menu</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c4d0f-262">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="c4d0f-262">Known Issues</span></span>

* <span data-ttu-id="c4d0f-263">L’Accès rapide fonctionne uniquement avec les éléments basés sur l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-263">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="c4d0f-264">Les ressources locales ou attachées par le biais d’une clé ou d’un jeton SAP ne sont pas prises en charge dans cette version</span><span class="sxs-lookup"><span data-stu-id="c4d0f-264">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="c4d0f-265">Accès rapide peut prendre quelques secondes toonavigate toohello ressource cible, selon le nombre de ressources</span><span class="sxs-lookup"><span data-stu-id="c4d0f-265">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="c4d0f-266">Plus de 3 groupes des objets BLOB ou des fichiers de téléchargement à hello même temps peut provoquer des erreurs</span><span class="sxs-lookup"><span data-stu-id="c4d0f-266">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="c4d0f-267">Les recherches peuvent porter sur 50 000 nœuds environ. Au-delà, elles affectent les performances ou peuvent entraîner des exceptions non prises en charge</span><span class="sxs-lookup"><span data-stu-id="c4d0f-267">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>
* <span data-ttu-id="c4d0f-268">Pourquoi première fois à l’aide de hello Explorateur de stockage sur macOS, vous pouvez voir plusieurs invites demandant trousseau de tooaccess d’autorisation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-268">For hello first time using hello Storage Explorer on macOS, you might see multiple prompts asking for user's permission tooaccess keychain.</span></span> <span data-ttu-id="c4d0f-269">Nous vous suggérons de que sélectionner toujours autoriser afin de l’invite de commandes hello ne s’afficheront à nouveau</span><span class="sxs-lookup"><span data-stu-id="c4d0f-269">We suggest you select Always Allow so hello prompt won't show up again</span></span>

<span data-ttu-id="c4d0f-270">11/18/2016</span><span class="sxs-lookup"><span data-stu-id="c4d0f-270">11/18/2016</span></span>
### <a name="version-086"></a><span data-ttu-id="c4d0f-271">Version 0.8.6</span><span class="sxs-lookup"><span data-stu-id="c4d0f-271">Version 0.8.6</span></span>

#### <a name="new"></a><span data-ttu-id="c4d0f-272">Nouveau</span><span class="sxs-lookup"><span data-stu-id="c4d0f-272">New</span></span>

* <span data-ttu-id="c4d0f-273">Vous pouvez maintenant le code confidentiel plus fréquemment utilisés services toohello accès rapide pour faciliter la navigation</span><span class="sxs-lookup"><span data-stu-id="c4d0f-273">You can now pin most frequently used services toohello Quick Access for easy navigation</span></span>
* <span data-ttu-id="c4d0f-274">Vous pouvez désormais ouvrir plusieurs éditeurs dans différents onglets.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-274">You can now open multiple editors in different tabs.</span></span> <span data-ttu-id="c4d0f-275">Tooopen un onglet temporaire ; par simple clic Double-cliquez sur tooopen un onglet permanent. Vous pouvez également cliquer sur hello onglet temporaire toomake il un onglet permanent</span><span class="sxs-lookup"><span data-stu-id="c4d0f-275">Single click tooopen a temporary tab; double click tooopen a permanent tab. You can also click on hello temporary tab toomake it a permanent tab</span></span>
* <span data-ttu-id="c4d0f-276">Des améliorations notables en termes de stabilité et de performances pour les chargements et téléchargements ont été réalisés, en particulier pour les fichiers volumineux sur des machines rapides</span><span class="sxs-lookup"><span data-stu-id="c4d0f-276">We have made noticeable performance and stability improvements for uploads and downloads, especially for large files on fast machines</span></span>
* <span data-ttu-id="c4d0f-277">Des dossiers « virtuels » vides peuvent maintenant être créés dans des conteneurs d’objets blob</span><span class="sxs-lookup"><span data-stu-id="c4d0f-277">Empty "virtual" folders can now be created in blob containers</span></span>
* <span data-ttu-id="c4d0f-278">Nous avons réintroduit une recherche étendue avec notre nouvelle recherche de sous-chaîne améliorée. Vous disposez désormais de deux options de recherche :</span><span class="sxs-lookup"><span data-stu-id="c4d0f-278">We have re-introduced scoped search with our new enhanced substring search, so you now have two options for searching:</span></span> 
    * <span data-ttu-id="c4d0f-279">Global recherche - simplement entrer un terme à rechercher dans la zone de texte Rechercher hello</span><span class="sxs-lookup"><span data-stu-id="c4d0f-279">Global search - just enter a search term into hello search textbox</span></span>
    * <span data-ttu-id="c4d0f-280">Recherche thématique - cliquez sur hello loupe icône tooa nœud suivant, ajouter une fin de toohello de terme de recherche du chemin de hello, ou avec le bouton droit et sélectionnez « Recherche d’ici »</span><span class="sxs-lookup"><span data-stu-id="c4d0f-280">Scoped search - click hello magnifying glass icon next tooa node, then add a search term toohello end of hello path, or right-click and select "Search from Here"</span></span>
* <span data-ttu-id="c4d0f-281">Nous avons ajouté différents thèmes : Clair (par défaut), Foncé, Contraste noir élevé et Contraste blanc élevé.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-281">We have added various themes: Light (default), Dark, High Contrast Black, and High Contrast White.</span></span> <span data-ttu-id="c4d0f-282">Accédez tooEdit -&gt; thèmes toochange votre préférence de thèmes</span><span class="sxs-lookup"><span data-stu-id="c4d0f-282">Go tooEdit -&gt; Themes toochange your theming preference</span></span>
* <span data-ttu-id="c4d0f-283">Vous pouvez modifier les propriétés des objets blob et des fichiers</span><span class="sxs-lookup"><span data-stu-id="c4d0f-283">You can modify Blob and file properties</span></span>
* <span data-ttu-id="c4d0f-284">Nous prenons désormais en charge les messages des files d’attente codés (base 64) et non codés</span><span class="sxs-lookup"><span data-stu-id="c4d0f-284">We now support encoded (base64) and unencoded queue messages</span></span>
* <span data-ttu-id="c4d0f-285">Sous Linux, un système d’exploitation 64 bits est désormais obligatoire.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-285">On Linux, a 64-bit OS is now required.</span></span> <span data-ttu-id="c4d0f-286">Pour cette version, nous ne prenons en charge que Ubuntu 16.04.1 LTS 64 bits</span><span class="sxs-lookup"><span data-stu-id="c4d0f-286">For this release we only support 64-bit Ubuntu 16.04.1 LTS</span></span>
* <span data-ttu-id="c4d0f-287">Nous avons mis à jour notre logo.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-287">We have updated our logo!</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4d0f-288">Correctifs</span><span class="sxs-lookup"><span data-stu-id="c4d0f-288">Fixes</span></span>

* <span data-ttu-id="c4d0f-289">Problème résolu : blocage de l’écran</span><span class="sxs-lookup"><span data-stu-id="c4d0f-289">Fixed: Screen freezing problems</span></span>
* <span data-ttu-id="c4d0f-290">Sécurité améliorée</span><span class="sxs-lookup"><span data-stu-id="c4d0f-290">Fixed: Enhanced security</span></span>
* <span data-ttu-id="c4d0f-291">Problème résolu : il peut arriver que des comptes joints en double s’affichent</span><span class="sxs-lookup"><span data-stu-id="c4d0f-291">Fixed: Sometimes duplicate attached accounts could appear</span></span>
* <span data-ttu-id="c4d0f-292">Problème résolu : un objet blob avec un type de contenu non défini peut générer une exception</span><span class="sxs-lookup"><span data-stu-id="c4d0f-292">Fixed: A blob with an undefined content type could generate an exception</span></span>
* <span data-ttu-id="c4d0f-293">Problème résolu : Hello lors de l’ouverture du Panneau de requête sur une table vide n’était pas possible</span><span class="sxs-lookup"><span data-stu-id="c4d0f-293">Fixed: Opening hello Query Panel on an empty table was not possible</span></span>
* <span data-ttu-id="c4d0f-294">Problème résolu : bogues différents dans la recherche</span><span class="sxs-lookup"><span data-stu-id="c4d0f-294">Fixed: Varies bugs in Search</span></span>
* <span data-ttu-id="c4d0f-295">Problème résolu : Augmenté nombre hello de ressources chargées à partir de 50 too100 lorsque vous cliquez sur « Charge plus »</span><span class="sxs-lookup"><span data-stu-id="c4d0f-295">Fixed: Increased hello number of resources loaded from 50 too100 when clicking "Load More"</span></span>
* <span data-ttu-id="c4d0f-296">Problème résolu : lors de la première exécution, si un compte est connecté, tous les abonnements sont sélectionnés pour ce compte par défaut</span><span class="sxs-lookup"><span data-stu-id="c4d0f-296">Fixed: On first run, if an account is signed into, we now select all subscriptions for that account by default</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="c4d0f-297">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="c4d0f-297">Known Issues</span></span>

* <span data-ttu-id="c4d0f-298">Cette version de hello Explorateur de stockage ne fonctionne pas sur Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="c4d0f-298">This release of hello Storage Explorer does not run on Ubuntu 14.04</span></span>
* <span data-ttu-id="c4d0f-299">tooopen plusieurs onglets pour hello même ressource, effectuez pas continuellement cliquez sur hello même ressource.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-299">tooopen multiple tabs for hello same resource, do not continuously click on hello same resource.</span></span> <span data-ttu-id="c4d0f-300">Cliquez sur une autre ressource, puis revenir en arrière, puis cliquez sur tooopen de ressource d’origine hello il à nouveau dans un autre onglet</span><span class="sxs-lookup"><span data-stu-id="c4d0f-300">Click on another resource and then go back and then click on hello original resource tooopen it again in another tab</span></span> 
* <span data-ttu-id="c4d0f-301">L’Accès rapide fonctionne uniquement avec les éléments basés sur l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-301">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="c4d0f-302">Les ressources locales ou attachées par le biais d’une clé ou d’un jeton SAP ne sont pas prises en charge dans cette version</span><span class="sxs-lookup"><span data-stu-id="c4d0f-302">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="c4d0f-303">Accès rapide peut prendre quelques secondes toonavigate toohello ressource cible, selon le nombre de ressources</span><span class="sxs-lookup"><span data-stu-id="c4d0f-303">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="c4d0f-304">Plus de 3 groupes des objets BLOB ou des fichiers de téléchargement à hello même temps peut provoquer des erreurs</span><span class="sxs-lookup"><span data-stu-id="c4d0f-304">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="c4d0f-305">Les recherches peuvent porter sur 50 000 nœuds environ. Au-delà, elles affectent les performances ou peuvent entraîner des exceptions non prises en charge</span><span class="sxs-lookup"><span data-stu-id="c4d0f-305">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>

<span data-ttu-id="c4d0f-306">10/03/2016</span><span class="sxs-lookup"><span data-stu-id="c4d0f-306">10/03/2016</span></span>
### <a name="version-085"></a><span data-ttu-id="c4d0f-307">Version 0.8.5</span><span class="sxs-lookup"><span data-stu-id="c4d0f-307">Version 0.8.5</span></span>

#### <a name="new"></a><span data-ttu-id="c4d0f-308">Nouveau</span><span class="sxs-lookup"><span data-stu-id="c4d0f-308">New</span></span>

* <span data-ttu-id="c4d0f-309">Peuvent désormais utiliser les associations de sécurité générés par le portail de clés tooattach tooStorage comptes et des ressources</span><span class="sxs-lookup"><span data-stu-id="c4d0f-309">Can now use Portal-generated SAS keys tooattach tooStorage Accounts and resources</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4d0f-310">Correctifs</span><span class="sxs-lookup"><span data-stu-id="c4d0f-310">Fixes</span></span>

* <span data-ttu-id="c4d0f-311">Problème résolu : condition de concurrence lors de la recherche parfois dû toobecome de nœuds non extensible</span><span class="sxs-lookup"><span data-stu-id="c4d0f-311">Fixed: race condition during search sometimes caused nodes toobecome non-expandable</span></span>
* <span data-ttu-id="c4d0f-312">Problème résolu : « Utiliser HTTP » ne fonctionne pas lors de la connexion des comptes tooStorage avec la clé et le nom du compte</span><span class="sxs-lookup"><span data-stu-id="c4d0f-312">Fixed: "Use HTTP" doesn't work when connecting tooStorage Accounts with account name and key</span></span>
* <span data-ttu-id="c4d0f-313">Problème résolu : les clés SAP (en particulier celles qui sont générées par le portail) renvoient une erreur « barre oblique »</span><span class="sxs-lookup"><span data-stu-id="c4d0f-313">Fixed: SAS keys (specially Portal-generated ones) return a "trailing slash" error</span></span>
* <span data-ttu-id="c4d0f-314">Problème résolu : problèmes d’importation de tables</span><span class="sxs-lookup"><span data-stu-id="c4d0f-314">Fixed: table import issues</span></span>
    * <span data-ttu-id="c4d0f-315">Parfois, la clé de partition et la clé de ligne ont été inversées</span><span class="sxs-lookup"><span data-stu-id="c4d0f-315">Sometimes partition key and row key were reversed</span></span>
    * <span data-ttu-id="c4d0f-316">Impossible de tooread « null » les clés de Partition</span><span class="sxs-lookup"><span data-stu-id="c4d0f-316">Unable tooread "null" Partition Keys</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c4d0f-317">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="c4d0f-317">Known Issues</span></span>

* <span data-ttu-id="c4d0f-318">Les recherches peuvent porter sur 50 000 nœuds environ. Au-delà, elles affectent les performances</span><span class="sxs-lookup"><span data-stu-id="c4d0f-318">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>
* <span data-ttu-id="c4d0f-319">Pile Azure ne prend actuellement en charge les fichiers, afin de la tentative de tooexpand fichiers affichera une erreur</span><span class="sxs-lookup"><span data-stu-id="c4d0f-319">Azure Stack doesn't currently support Files, so trying tooexpand Files will show an error</span></span>

<span data-ttu-id="c4d0f-320">09/12/2016</span><span class="sxs-lookup"><span data-stu-id="c4d0f-320">09/12/2016</span></span>
### <a name="version-084"></a><span data-ttu-id="c4d0f-321">Version 0.8.4</span><span class="sxs-lookup"><span data-stu-id="c4d0f-321">Version 0.8.4</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="c4d0f-322">Nouveau</span><span class="sxs-lookup"><span data-stu-id="c4d0f-322">New</span></span>

* <span data-ttu-id="c4d0f-323">Générer des comptes toostorage de liens directs, des conteneurs, des files d’attente, des tableaux ou des partages de fichiers simple pour le partage et accéder aux ressources de tooyour - Windows et prend en charge de Mac OS</span><span class="sxs-lookup"><span data-stu-id="c4d0f-323">Generate direct links toostorage accounts, containers, queues, tables, or file shares for sharing and easy access tooyour resources - Windows and Mac OS support</span></span>
* <span data-ttu-id="c4d0f-324">Rechercher vos conteneurs d’objets blob, les tables, les files d’attente, les partages de fichiers ou les comptes de stockage à partir de la zone de recherche hello</span><span class="sxs-lookup"><span data-stu-id="c4d0f-324">Search for your blob containers, tables, queues, file shares, or storage accounts from hello search box</span></span>
* <span data-ttu-id="c4d0f-325">Vous pouvez maintenant regrouper des clauses dans le Générateur de requêtes de table hello</span><span class="sxs-lookup"><span data-stu-id="c4d0f-325">You can now group clauses in hello table query builder</span></span>
* <span data-ttu-id="c4d0f-326">Renommer et copier/coller des conteneurs d’objets blob, des partages de fichiers, des tables, des objets blob, des dossiers d’objets blob, des fichiers et répertoires depuis des comptes et conteneurs joint par SAP</span><span class="sxs-lookup"><span data-stu-id="c4d0f-326">Rename and copy/paste blob containers, file shares, tables, blobs, blob folders, files and directories from within SAS-attached accounts and containers</span></span>
* <span data-ttu-id="c4d0f-327">Le changement de nom et la& copie des conteneurs d’objets blob et des partages de fichiers préservent désormais les métadonnées et propriétés</span><span class="sxs-lookup"><span data-stu-id="c4d0f-327">Renaming and copying blob containers and file shares now preserve properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4d0f-328">Correctifs</span><span class="sxs-lookup"><span data-stu-id="c4d0f-328">Fixes</span></span>

* <span data-ttu-id="c4d0f-329">Problème résolu : impossible de modifier des entités de tables si elles contiennent des propriétés booléennes ou binaires</span><span class="sxs-lookup"><span data-stu-id="c4d0f-329">Fixed: cannot edit table entities if they contain boolean or binary properties</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c4d0f-330">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="c4d0f-330">Known Issues</span></span>

* <span data-ttu-id="c4d0f-331">Les recherches peuvent porter sur 50 000 nœuds environ. Au-delà, elles affectent les performances</span><span class="sxs-lookup"><span data-stu-id="c4d0f-331">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>

<span data-ttu-id="c4d0f-332">08/03/2016</span><span class="sxs-lookup"><span data-stu-id="c4d0f-332">08/03/2016</span></span>
### <a name="version-083"></a><span data-ttu-id="c4d0f-333">Version 0.8.3</span><span class="sxs-lookup"><span data-stu-id="c4d0f-333">Version 0.8.3</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="c4d0f-334">Nouveau</span><span class="sxs-lookup"><span data-stu-id="c4d0f-334">New</span></span>

* <span data-ttu-id="c4d0f-335">Renommez des conteneurs, tables et partages de fichiers</span><span class="sxs-lookup"><span data-stu-id="c4d0f-335">Rename containers, tables, file shares</span></span>
* <span data-ttu-id="c4d0f-336">Meilleure expérience de générateur de requête</span><span class="sxs-lookup"><span data-stu-id="c4d0f-336">Improved Query builder experience</span></span>
* <span data-ttu-id="c4d0f-337">Capacité toosave et charge les requêtes</span><span class="sxs-lookup"><span data-stu-id="c4d0f-337">Ability toosave and load queries</span></span>
* <span data-ttu-id="c4d0f-338">Diriger les tables des comptes ou des conteneurs, les files d’attente, toostorage liens ou des partages pour le partage et facilement l’accès à vos ressources de fichiers (Windows uniquement - macOS prennent en charge sera bientôt disponible !)</span><span class="sxs-lookup"><span data-stu-id="c4d0f-338">Direct links toostorage accounts or containers, queues, tables, or file shares for sharing and easily accessing your resources (Windows-only - macOS support coming soon!)</span></span>
* <span data-ttu-id="c4d0f-339">Capacité toomanage et configurer les règles CORS</span><span class="sxs-lookup"><span data-stu-id="c4d0f-339">Ability toomanage and configure CORS rules</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4d0f-340">Correctifs</span><span class="sxs-lookup"><span data-stu-id="c4d0f-340">Fixes</span></span>

* <span data-ttu-id="c4d0f-341">Problème résolu : les comptes Microsoft nécessitent une nouvelle authentification toutes les 8 à 12 heures</span><span class="sxs-lookup"><span data-stu-id="c4d0f-341">Fixed: Microsoft Accounts require re-authentication every 8-12 hours</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c4d0f-342">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="c4d0f-342">Known Issues</span></span>

* <span data-ttu-id="c4d0f-343">Parfois hello l’interface utilisateur peut sembler bloquée - agrandissement de fenêtre hello permet de résoudre ce problème</span><span class="sxs-lookup"><span data-stu-id="c4d0f-343">Sometimes hello UI might appear frozen - maximizing hello window helps resolve this issue</span></span>
* <span data-ttu-id="c4d0f-344">L’installation de macOS peut nécessiter des autorisations élevées</span><span class="sxs-lookup"><span data-stu-id="c4d0f-344">macOS install may require elevated permissions</span></span>
* <span data-ttu-id="c4d0f-345">Panneau des paramètres de compte peut indiquer que vous avez besoin d’informations d’identification tooreenter dans les abonnements toofilter de commande</span><span class="sxs-lookup"><span data-stu-id="c4d0f-345">Account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="c4d0f-346">Changement de nom des partages de fichiers, les conteneurs d’objets blob et les tables ne conserve pas les métadonnées ou autres propriétés sur le conteneur de hello, telles que le quota du partage de fichiers, de niveau d’accès public ou de stratégies d’accès</span><span class="sxs-lookup"><span data-stu-id="c4d0f-346">Renaming file shares, blob containers, and tables does not preserve metadata or other properties on hello container, such as file share quota, public access level or access policies</span></span>
* <span data-ttu-id="c4d0f-347">Les captures instantanées ne sont pas conservées lorsque les blobs sont renommés (individuellement ou dans un conteneur d’objets blob renommé).</span><span class="sxs-lookup"><span data-stu-id="c4d0f-347">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="c4d0f-348">Lors d’un changement de nom, toutes les autres propriétés et métadonnées des objets blob, fichiers et entités sont conservées</span><span class="sxs-lookup"><span data-stu-id="c4d0f-348">All other properties and metadata for blobs, files and entities are preserved during a rename</span></span>
* <span data-ttu-id="c4d0f-349">Copier ou renommer des ressources ne fonctionne pas à l’intérieur des comptes joints par SAP</span><span class="sxs-lookup"><span data-stu-id="c4d0f-349">Copying or renaming resources does not work within SAS-attached accounts</span></span>

<span data-ttu-id="c4d0f-350">07/07/2016</span><span class="sxs-lookup"><span data-stu-id="c4d0f-350">07/07/2016</span></span>
### <a name="version-082"></a><span data-ttu-id="c4d0f-351">Version 0.8.2</span><span class="sxs-lookup"><span data-stu-id="c4d0f-351">Version 0.8.2</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="c4d0f-352">Nouveau</span><span class="sxs-lookup"><span data-stu-id="c4d0f-352">New</span></span>

* <span data-ttu-id="c4d0f-353">Les comptes de stockage sont regroupés par abonnements ; le stockage de développement et les ressources jointes via la clé ou SAP sont affichés sous le nœud (local et joint)</span><span class="sxs-lookup"><span data-stu-id="c4d0f-353">Storage Accounts are grouped by subscriptions; development storage and resources attached via key or SAS are shown under (Local and Attached) node</span></span>
* <span data-ttu-id="c4d0f-354">Se déconnecter depuis des comptes dans le panneau « Paramètres du compte Azure »</span><span class="sxs-lookup"><span data-stu-id="c4d0f-354">Sign off from accounts in "Azure Account Settings" panel</span></span>
* <span data-ttu-id="c4d0f-355">Configurer les tooenable des paramètres de proxy et gérer les connexion</span><span class="sxs-lookup"><span data-stu-id="c4d0f-355">Configure proxy settings tooenable and manage sign-in</span></span>
* <span data-ttu-id="c4d0f-356">Créer et annuler des baux d’objets blob</span><span class="sxs-lookup"><span data-stu-id="c4d0f-356">Create and break blob leases</span></span>
* <span data-ttu-id="c4d0f-357">Ouvrir des conteneurs d’objets blob, des files d’attente, des tables et des fichiers avec un simple clic</span><span class="sxs-lookup"><span data-stu-id="c4d0f-357">Open blob containers, queues, tables, and files with single-click</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4d0f-358">Correctifs</span><span class="sxs-lookup"><span data-stu-id="c4d0f-358">Fixes</span></span>

* <span data-ttu-id="c4d0f-359">Problème résolu : les messages de files d’attente insérés à l’aide des bibliothèques .NET ou Java ne sont pas correctement décodés depuis base64</span><span class="sxs-lookup"><span data-stu-id="c4d0f-359">Fixed: queue messages inserted with .NET or Java libraries are not properly decoded from base64</span></span>
* <span data-ttu-id="c4d0f-360">Problème résolu : les tables $metrics ne figurent pas pour les comptes de stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="c4d0f-360">Fixed: $metrics tables are not shown for Blob Storage accounts</span></span>
* <span data-ttu-id="c4d0f-361">Problème résolu : le nœud de la table ne fonctionne pas pour le stockage local (développement)</span><span class="sxs-lookup"><span data-stu-id="c4d0f-361">Fixed: tables node does not work for local (Development) storage</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c4d0f-362">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="c4d0f-362">Known Issues</span></span>

* <span data-ttu-id="c4d0f-363">L’installation de macOS peut nécessiter des autorisations élevées</span><span class="sxs-lookup"><span data-stu-id="c4d0f-363">macOS install may require elevated permissions</span></span>

<span data-ttu-id="c4d0f-364">06/15/2016</span><span class="sxs-lookup"><span data-stu-id="c4d0f-364">06/15/2016</span></span>
### <a name="version-080"></a><span data-ttu-id="c4d0f-365">Version 0.8.0</span><span class="sxs-lookup"><span data-stu-id="c4d0f-365">Version 0.8.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="c4d0f-366">Nouveau</span><span class="sxs-lookup"><span data-stu-id="c4d0f-366">New</span></span>

* <span data-ttu-id="c4d0f-367">Prise en charge du partage de fichiers : affichage, téléchargement, chargement, copie de fichiers et de répertoires, URI SAP (créer et connecter)</span><span class="sxs-lookup"><span data-stu-id="c4d0f-367">File share support: viewing, uploading, downloading, copying files and directories, SAS URIs (create and connect)</span></span>
* <span data-ttu-id="c4d0f-368">Amélioration de l’expérience utilisateur pour la connexion tooStorage avec SAS URI ou des clés de compte</span><span class="sxs-lookup"><span data-stu-id="c4d0f-368">Improved user experience for connecting tooStorage with SAS URIs or account keys</span></span>
* <span data-ttu-id="c4d0f-369">Exporter des résultats de requêtes de table</span><span class="sxs-lookup"><span data-stu-id="c4d0f-369">Export table query results</span></span>
* <span data-ttu-id="c4d0f-370">Réorganisation et personnalisation des colonnes de table</span><span class="sxs-lookup"><span data-stu-id="c4d0f-370">Table column reordering and customization</span></span>
* <span data-ttu-id="c4d0f-371">Affichage des conteneurs d’objets blob $logs et de tables $metrics pour les comptes de stockage avec les mesures activées</span><span class="sxs-lookup"><span data-stu-id="c4d0f-371">Viewing $logs blob containers and $metrics tables for Storage Accounts with enabled metrics</span></span>
* <span data-ttu-id="c4d0f-372">L’amélioration du comportement d’exportation et d’importation, inclut désormais le type de valeur de propriété</span><span class="sxs-lookup"><span data-stu-id="c4d0f-372">Improved export and import behavior, now includes property value type</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4d0f-373">Correctifs</span><span class="sxs-lookup"><span data-stu-id="c4d0f-373">Fixes</span></span>

* <span data-ttu-id="c4d0f-374">Problème résolu : le chargement ou le téléchargement d’objets blob volumineux peut entraîner des chargements/téléchargements incomplets</span><span class="sxs-lookup"><span data-stu-id="c4d0f-374">Fixed: uploading or downloading large blobs can result in incomplete uploads/downloads</span></span>
* <span data-ttu-id="c4d0f-375">Modification fixe :, l’ajout ou l’importation d’une entité avec une valeur de chaîne numérique (« 1 »), il sera converti toodouble</span><span class="sxs-lookup"><span data-stu-id="c4d0f-375">Fixed: editing, adding, or importing an entity with a numeric string value ("1") will convert it toodouble</span></span>
* <span data-ttu-id="c4d0f-376">Problème résolu : Nœud de table hello tooexpand impossible dans un environnement de développement local hello</span><span class="sxs-lookup"><span data-stu-id="c4d0f-376">Fixed: Unable tooexpand hello table node in hello local development environment</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c4d0f-377">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="c4d0f-377">Known Issues</span></span>

* <span data-ttu-id="c4d0f-378">Les tables $metrics ne figurent pas pour les comptes de stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="c4d0f-378">$metrics tables are not visible for Blob Storage accounts</span></span>
* <span data-ttu-id="c4d0f-379">File d’attente des messages ajoutés par programmation ne peuvent pas s’afficher correctement si les messages de type hello sont codés en Base64</span><span class="sxs-lookup"><span data-stu-id="c4d0f-379">Queue messages added programmatically may not be displayed correctly if hello messages are encoded using Base64 encoding</span></span>

<span data-ttu-id="c4d0f-380">05/17/2016</span><span class="sxs-lookup"><span data-stu-id="c4d0f-380">05/17/2016</span></span>
### <a name="version-07201605090"></a><span data-ttu-id="c4d0f-381">Version 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="c4d0f-381">Version 0.7.20160509.0</span></span>

#### <a name="new"></a><span data-ttu-id="c4d0f-382">Nouveau</span><span class="sxs-lookup"><span data-stu-id="c4d0f-382">New</span></span>

* <span data-ttu-id="c4d0f-383">Une meilleure gestion des erreurs pour les incidents d’applications</span><span class="sxs-lookup"><span data-stu-id="c4d0f-383">Better error handling for app crashes</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4d0f-384">Correctifs</span><span class="sxs-lookup"><span data-stu-id="c4d0f-384">Fixes</span></span>

* <span data-ttu-id="c4d0f-385">Bogue résolu dans lequel les messages de la barre d’informations parfois n’apparaissent pas lorsque les informations d’identification de connexion sont requises</span><span class="sxs-lookup"><span data-stu-id="c4d0f-385">Fixed bug where InfoBar messages sometimes don't show up when sign-in credentials were required</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c4d0f-386">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="c4d0f-386">Known Issues</span></span>

* <span data-ttu-id="c4d0f-387">Tables : Ajout, modification, ou l’importation d’une entité qui a une propriété avec une valeur numérique ambiguë, comme « 1 » ou « 1.0 », et hello utilisateur tentatives toosend comme un `Edm.String`, valeur de hello reviendra via le client hello API comme un Edm.Double</span><span class="sxs-lookup"><span data-stu-id="c4d0f-387">Tables: Adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and hello user tries toosend it as an `Edm.String`, hello value will come back through hello client API as an Edm.Double</span></span>

<span data-ttu-id="c4d0f-388">03/31/2016</span><span class="sxs-lookup"><span data-stu-id="c4d0f-388">03/31/2016</span></span>

### <a name="version-07201603250"></a><span data-ttu-id="c4d0f-389">Version 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="c4d0f-389">Version 0.7.20160325.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="c4d0f-390">Nouveau</span><span class="sxs-lookup"><span data-stu-id="c4d0f-390">New</span></span>

* <span data-ttu-id="c4d0f-391">Prise en charge de la table : opérations d’affichage, d’interrogation, d’exportation, d’importation et CRUD pour les entités</span><span class="sxs-lookup"><span data-stu-id="c4d0f-391">Table support: viewing, querying, export, import, and CRUD operations for entities</span></span>
* <span data-ttu-id="c4d0f-392">Prise en charge de la file d’attente : affichage, ajout, retrait de la file d’attente des messages</span><span class="sxs-lookup"><span data-stu-id="c4d0f-392">Queue support: viewing, adding, dequeueing messages</span></span>
* <span data-ttu-id="c4d0f-393">Génération d’URI SAP pour les comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="c4d0f-393">Generating SAS URIs for Storage Accounts</span></span>
* <span data-ttu-id="c4d0f-394">Connecter des comptes de tooStorage à des URI SAS</span><span class="sxs-lookup"><span data-stu-id="c4d0f-394">Connecting tooStorage Accounts with SAS URIs</span></span>
* <span data-ttu-id="c4d0f-395">Notifications de mise à jour pour les futures mises à jour tooStorage Explorer</span><span class="sxs-lookup"><span data-stu-id="c4d0f-395">Update notifications for future updates tooStorage Explorer</span></span>
* <span data-ttu-id="c4d0f-396">Apparence mise à jour</span><span class="sxs-lookup"><span data-stu-id="c4d0f-396">Updated look and feel</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4d0f-397">Correctifs</span><span class="sxs-lookup"><span data-stu-id="c4d0f-397">Fixes</span></span>

* <span data-ttu-id="c4d0f-398">Améliorations des performances et de la fiabilité</span><span class="sxs-lookup"><span data-stu-id="c4d0f-398">Performance and reliability improvements</span></span>

### <a name="known-issues-amp-mitigations"></a><span data-ttu-id="c4d0f-399">Problèmes connus &amp; atténuations des risques</span><span class="sxs-lookup"><span data-stu-id="c4d0f-399">Known Issues &amp; Mitigations</span></span>

* <span data-ttu-id="c4d0f-400">Le téléchargement de fichiers d’objets blob volumineux ne fonctionne pas correctement, nous vous recommandons d’utiliser AzCopy pendant que nous résolvons ce problème</span><span class="sxs-lookup"><span data-stu-id="c4d0f-400">Download of large blob files does not work correctly - we recommend using AzCopy while we address this issue</span></span> 
* <span data-ttu-id="c4d0f-401">Informations d’identification de compte ne seront pas récupérées ni mis en cache si le dossier de base hello est introuvable ou ne peut pas être écrit pour</span><span class="sxs-lookup"><span data-stu-id="c4d0f-401">Account credentials will not be retrieved nor cached if hello home folder cannot be found or cannot be written to</span></span>
* <span data-ttu-id="c4d0f-402">Si nous sommes Ajout, modification ou l’importation d’une entité qui a une propriété avec une valeur numérique ambiguë, comme « 1 » ou « 1.0 », et l’utilisateur de hello tente toosend comme un `Edm.String`, valeur de hello reviendra via le client hello API comme un Edm.Double</span><span class="sxs-lookup"><span data-stu-id="c4d0f-402">If we are adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and hello user tries toosend it as an `Edm.String`, hello value will come back through hello client API as an Edm.Double</span></span>
* <span data-ttu-id="c4d0f-403">Lors de l’importation de fichiers CSV avec des enregistrements multilignes, les données de salutation peuvent obtenir coupées ou brouillées</span><span class="sxs-lookup"><span data-stu-id="c4d0f-403">When importing CSV files with multiline records, hello data may get chopped or scrambled</span></span>

<span data-ttu-id="c4d0f-404">02/03/2016</span><span class="sxs-lookup"><span data-stu-id="c4d0f-404">02/03/2016</span></span>

### <a name="version-07201601291"></a><span data-ttu-id="c4d0f-405">Version 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="c4d0f-405">Version 0.7.20160129.1</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4d0f-406">Correctifs</span><span class="sxs-lookup"><span data-stu-id="c4d0f-406">Fixes</span></span>

* <span data-ttu-id="c4d0f-407">Amélioration des performances globales lors du chargement, du téléchargement et de la copie des objets blob</span><span class="sxs-lookup"><span data-stu-id="c4d0f-407">Improved overall performance when uploading, downloading and copying blobs</span></span>

<span data-ttu-id="c4d0f-408">01/14/2016</span><span class="sxs-lookup"><span data-stu-id="c4d0f-408">01/14/2016</span></span>

### <a name="version-07201601050"></a><span data-ttu-id="c4d0f-409">Version 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="c4d0f-409">Version 0.7.20160105.0</span></span>

#### <a name="new"></a><span data-ttu-id="c4d0f-410">Nouveau</span><span class="sxs-lookup"><span data-stu-id="c4d0f-410">New</span></span>

* <span data-ttu-id="c4d0f-411">Prise en charge de Linux (tooOSX de fonctionnalités de parité)</span><span class="sxs-lookup"><span data-stu-id="c4d0f-411">Linux support (parity features tooOSX)</span></span>
* <span data-ttu-id="c4d0f-412">Ajouter des conteneurs d’objets blob avec une clé Signatures d’accès partagé (SAP)</span><span class="sxs-lookup"><span data-stu-id="c4d0f-412">Add blob containers with Shared Access Signatures (SAS) key</span></span>
* <span data-ttu-id="c4d0f-413">Ajouter des comptes de stockage Azure Chine</span><span class="sxs-lookup"><span data-stu-id="c4d0f-413">Add Storage Accounts for Azure China</span></span>
* <span data-ttu-id="c4d0f-414">Ajouter des comptes de stockage avec des points de terminaison personnalisés</span><span class="sxs-lookup"><span data-stu-id="c4d0f-414">Add Storage Accounts with custom endpoints</span></span>
* <span data-ttu-id="c4d0f-415">Ouvrir et consulter les BLOB hello contenu texte et image</span><span class="sxs-lookup"><span data-stu-id="c4d0f-415">Open and view hello contents text and picture blobs</span></span>
* <span data-ttu-id="c4d0f-416">Affichez et modifiez les propriétés et métadonnées des blobs</span><span class="sxs-lookup"><span data-stu-id="c4d0f-416">View and edit blob properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4d0f-417">Correctifs</span><span class="sxs-lookup"><span data-stu-id="c4d0f-417">Fixes</span></span>

* <span data-ttu-id="c4d0f-418">Fixe : chargement ou téléchargement un grand nombre d’objets BLOB (500) peut parfois provoquer hello application toohave un écran blanc</span><span class="sxs-lookup"><span data-stu-id="c4d0f-418">Fixed: uploading or download a large number of blobs (500+) may sometimes cause hello app toohave a white screen</span></span> 
* <span data-ttu-id="c4d0f-419">Problème résolu : lors de la définition de niveau accès public du conteneur d’objets blob, nouvelle valeur de hello n'est pas mis à jour tant que vous définissez nouveau hello de se concentrer sur le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-419">Fixed: when setting blob container public access level, hello new value is not updated until you re-set hello focus on hello container.</span></span> <span data-ttu-id="c4d0f-420">En outre, boîte de dialogue hello toujours par défaut est trop « n’accès aucun public » et non hello actuelle de valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="c4d0f-420">Also, hello dialog always defaults too"No public access", and not hello actual current value.</span></span>
* <span data-ttu-id="c4d0f-421">Une meilleure prise en charge globale du clavier/accessibilité et de l’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="c4d0f-421">Better overall keyboard/accessibility and UI support</span></span>
* <span data-ttu-id="c4d0f-422">Le texte de l’historique des vues miniatures est encapsulé lorsqu’il est long avec un espace blanc</span><span class="sxs-lookup"><span data-stu-id="c4d0f-422">Breadcrumbs history text wraps when it's long with white space</span></span>
* <span data-ttu-id="c4d0f-423">La boîte de dialogue SAP prend en charge la validation d’entrée</span><span class="sxs-lookup"><span data-stu-id="c4d0f-423">SAS dialog supports input validation</span></span>
* <span data-ttu-id="c4d0f-424">Stockage local continue toobe disponible, même si les informations d’identification de l’utilisateur ont expiré</span><span class="sxs-lookup"><span data-stu-id="c4d0f-424">Local storage continues toobe available even if user credentials have expired</span></span>
* <span data-ttu-id="c4d0f-425">Lorsqu’un conteneur d’objets blob ouvert est supprimé, l’Explorateur d’objets blob hello sur droite hello est fermé</span><span class="sxs-lookup"><span data-stu-id="c4d0f-425">When an opened blob container is deleted, hello blob explorer on hello right side is closed</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c4d0f-426">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="c4d0f-426">Known Issues</span></span>

* <span data-ttu-id="c4d0f-427">Besoins d’installation Linux gcc version mise à jour ou mise à niveau – tooupgrade d’étapes sont répertoriées ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c4d0f-427">Linux install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span> 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

<span data-ttu-id="c4d0f-428">11/18/2015</span><span class="sxs-lookup"><span data-stu-id="c4d0f-428">11/18/2015</span></span>
### <a name="version-07201511160"></a><span data-ttu-id="c4d0f-429">Version 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="c4d0f-429">Version 0.7.20151116.0</span></span>

#### <a name="new"></a><span data-ttu-id="c4d0f-430">Nouveau</span><span class="sxs-lookup"><span data-stu-id="c4d0f-430">New</span></span>

* <span data-ttu-id="c4d0f-431">Versions macOS et Windows</span><span class="sxs-lookup"><span data-stu-id="c4d0f-431">macOS, and Windows versions</span></span>
* <span data-ttu-id="c4d0f-432">Connecter vos comptes de stockage tooview : utiliser votre compte professionnels Microsoft Account, 2FA, etc..</span><span class="sxs-lookup"><span data-stu-id="c4d0f-432">Sign in tooview your Storage Accounts – use your Org Account, Microsoft Account, 2FA, etc.</span></span>
* <span data-ttu-id="c4d0f-433">Stockage de développement local (utilisez l’émulateur de stockage, Windows uniquement)</span><span class="sxs-lookup"><span data-stu-id="c4d0f-433">Local development storage (use storage emulator, Windows-only)</span></span>
* <span data-ttu-id="c4d0f-434">Prise en charge d’Azure Resource Manager et des ressources classiques</span><span class="sxs-lookup"><span data-stu-id="c4d0f-434">Azure Resource Manager and Classic resource support</span></span>
* <span data-ttu-id="c4d0f-435">Créez et supprimez des objets blob, des files d’attente ou des tables</span><span class="sxs-lookup"><span data-stu-id="c4d0f-435">Create and delete blobs, queues, or tables</span></span>
* <span data-ttu-id="c4d0f-436">Recherchez des objets blob, des files d’attente ou des tables spécifiques</span><span class="sxs-lookup"><span data-stu-id="c4d0f-436">Search for specific blobs, queues, or tables</span></span>
* <span data-ttu-id="c4d0f-437">Explorer le contenu de hello de conteneurs d’objets blob</span><span class="sxs-lookup"><span data-stu-id="c4d0f-437">Explore hello contents of blob containers</span></span>
* <span data-ttu-id="c4d0f-438">Affichez et parcourez les répertoires</span><span class="sxs-lookup"><span data-stu-id="c4d0f-438">View and navigate through directories</span></span>
* <span data-ttu-id="c4d0f-439">Chargez, téléchargez et supprimez des objets blob et des dossiers</span><span class="sxs-lookup"><span data-stu-id="c4d0f-439">Upload, download, and delete blobs and folders</span></span>
* <span data-ttu-id="c4d0f-440">Affichez et modifiez les propriétés et métadonnées des blobs</span><span class="sxs-lookup"><span data-stu-id="c4d0f-440">View and edit blob properties and metadata</span></span>
* <span data-ttu-id="c4d0f-441">Générez des clés SAP</span><span class="sxs-lookup"><span data-stu-id="c4d0f-441">Generate SAS keys</span></span>
* <span data-ttu-id="c4d0f-442">Gérez et créez des stratégies d’accès stockés (SAS)</span><span class="sxs-lookup"><span data-stu-id="c4d0f-442">Manage and create Stored Access Policies (SAP)</span></span>
* <span data-ttu-id="c4d0f-443">Recherchez les blobs par préfixe</span><span class="sxs-lookup"><span data-stu-id="c4d0f-443">Search for blobs by prefix</span></span>
* <span data-ttu-id="c4d0f-444">Faites glisser et déplacer tooupload de fichiers ou de téléchargement</span><span class="sxs-lookup"><span data-stu-id="c4d0f-444">Drag 'n drop files tooupload or download</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c4d0f-445">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="c4d0f-445">Known Issues</span></span>

* <span data-ttu-id="c4d0f-446">Lorsque vous définissez le niveau accès public du conteneur d’objets blob, nouvelle valeur de hello n’est pas mis à jour tant que vous définissez nouveau hello de se concentrer sur le conteneur de hello</span><span class="sxs-lookup"><span data-stu-id="c4d0f-446">When setting blob container public access level, hello new value is not updated until you re-set hello focus on hello container</span></span>
* <span data-ttu-id="c4d0f-447">Lorsque vous ouvrez le niveau d’accès public hello dialogue tooset hello, il n’affiche toujours « Aucun accès public » comme valeur par défaut de hello et non hello actuelle de valeur réelle</span><span class="sxs-lookup"><span data-stu-id="c4d0f-447">When you open hello dialog tooset hello public access level, it always shows "No public access" as hello default, and not hello actual current value</span></span>
* <span data-ttu-id="c4d0f-448">Impossible de renommer des objets blob téléchargés</span><span class="sxs-lookup"><span data-stu-id="c4d0f-448">Cannot rename downloaded blobs</span></span>
* <span data-ttu-id="c4d0f-449">Entrées de journal d’activité est parfois « coincés » dans un en cours d’état lorsqu’une erreur se produit et hello erreur n’apparaît pas</span><span class="sxs-lookup"><span data-stu-id="c4d0f-449">Activity log entries will sometimes get "stuck" in an in progress state when an error occurs, and hello error is not displayed</span></span>
* <span data-ttu-id="c4d0f-450">Parfois les pannes ou désactive complètement blanc lors de la tentative de tooupload ou téléchargez un grand nombre d’objets BLOB</span><span class="sxs-lookup"><span data-stu-id="c4d0f-450">Sometimes crashes or turns completely white when trying tooupload or download a large number of blobs</span></span>
* <span data-ttu-id="c4d0f-451">Parfois, l’annulation d’une opération de copie ne fonctionne pas</span><span class="sxs-lookup"><span data-stu-id="c4d0f-451">Sometimes canceling a copy operation does not work</span></span>
* <span data-ttu-id="c4d0f-452">Au cours de la création d’un conteneur (table/file d’attente/blob), si vous entrez un nom non valide et que vous passez toocreate une autre sous un type de conteneur différents Impossible de définir le focus sur le nouveau type de hello</span><span class="sxs-lookup"><span data-stu-id="c4d0f-452">During creating a container (blob/queue/table), if you input an invalid name and proceed toocreate another under a different container type you cannot set focus on hello new type</span></span>
* <span data-ttu-id="c4d0f-453">Impossible de créer un nouveau dossier ou de renommer un dossier</span><span class="sxs-lookup"><span data-stu-id="c4d0f-453">Can't create new folder or rename folder</span></span>




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md