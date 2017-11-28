---
title: "limitations de Cloud Shell (version préliminaire) aaaAzure | Documents Microsoft"
description: "Vue d’ensemble des limites d’Azure Cloud Shell"
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
ms.openlocfilehash: 8462b0b9850fcde790a386433009439bbab52c0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-cloud-shell"></a><span data-ttu-id="08534-103">Limitations d’Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="08534-103">Limitations of Azure Cloud Shell</span></span>
<span data-ttu-id="08534-104">Azure Cloud Shell a suivant hello restrictions connues :</span><span class="sxs-lookup"><span data-stu-id="08534-104">Azure Cloud Shell has hello following known limitations:</span></span>

## <a name="system-state-and-persistence"></a><span data-ttu-id="08534-105">État du système et persistance</span><span class="sxs-lookup"><span data-stu-id="08534-105">System state and persistence</span></span>
<span data-ttu-id="08534-106">ordinateur Hello qui fournit votre session d’interpréteur de commandes de Cloud est temporaire et il est recyclé une fois votre session est inactive pendant 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="08534-106">hello machine that provides your Cloud Shell session is temporary, and it is recycled after your session is inactive for 20 minutes.</span></span> <span data-ttu-id="08534-107">Cloud Shell nécessite une toobe de partage de fichiers monté.</span><span class="sxs-lookup"><span data-stu-id="08534-107">Cloud Shell requires a file share toobe mounted.</span></span> <span data-ttu-id="08534-108">Par conséquent, votre abonnement doit être en mesure de tooset des tooaccess de ressources de stockage Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="08534-108">As a result, your subscription must be able tooset up storage resources tooaccess Cloud Shell.</span></span> <span data-ttu-id="08534-109">Autres éléments à prendre en compte :</span><span class="sxs-lookup"><span data-stu-id="08534-109">Other considerations include:</span></span>
* <span data-ttu-id="08534-110">Avec le stockage monté, seules les modifications apportées à votre répertoire `$Home` ou `clouddrive` sont conservées.</span><span class="sxs-lookup"><span data-stu-id="08534-110">With mounted storage, only modifications within your `$Home` directory or `clouddrive` directory are persisted.</span></span>
* <span data-ttu-id="08534-111">Les partages de fichiers peuvent être montés uniquement depuis votre [région affectée](persisting-shell-storage.md#mount-a-new-clouddrive).</span><span class="sxs-lookup"><span data-stu-id="08534-111">File shares can be mounted only from within your [assigned region](persisting-shell-storage.md#mount-a-new-clouddrive).</span></span>
* <span data-ttu-id="08534-112">Azure Files prend uniquement en charge les comptes de stockage localement redondant et les comptes de stockage géoredondant.</span><span class="sxs-lookup"><span data-stu-id="08534-112">Azure Files supports only locally redundant storage and geo-redundant storage accounts.</span></span>

## <a name="user-permissions"></a><span data-ttu-id="08534-113">Autorisations utilisateur</span><span class="sxs-lookup"><span data-stu-id="08534-113">User permissions</span></span>
<span data-ttu-id="08534-114">Les autorisations sont définies en tant qu’utilisateurs standards sans accès sudo.</span><span class="sxs-lookup"><span data-stu-id="08534-114">Permissions are set as regular users without sudo access.</span></span> <span data-ttu-id="08534-115">Les installations en dehors du répertoire `$Home` ne sont pas conservées.</span><span class="sxs-lookup"><span data-stu-id="08534-115">Any installation outside your `$Home` directory will not persist.</span></span>
<span data-ttu-id="08534-116">Bien que certaines commandes de hello `clouddrive` répertoire comme `git clone`, n’ont pas les autorisations appropriées, votre `$Home` active dispose des autorisations appropriées.</span><span class="sxs-lookup"><span data-stu-id="08534-116">Although certain commands within hello `clouddrive` directory, such as `git clone`, do not have proper permissions, your `$Home` directory does have permissions.</span></span>

## <a name="browser-support"></a><span data-ttu-id="08534-117">Prise en charge des navigateurs</span><span class="sxs-lookup"><span data-stu-id="08534-117">Browser support</span></span>
<span data-ttu-id="08534-118">Cloud Shell prend en charge les versions les plus récentes de Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox et Apple Safari hello.</span><span class="sxs-lookup"><span data-stu-id="08534-118">Cloud Shell supports hello latest versions of Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox, and Apple Safari.</span></span> <span data-ttu-id="08534-119">Safari en mode privé n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="08534-119">Safari in private mode is not supported.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="08534-120">Copier et coller</span><span class="sxs-lookup"><span data-stu-id="08534-120">Copy and paste</span></span>
<span data-ttu-id="08534-121">CTRL + C et Ctrl + V ne fonctionnent pas comme copier/coller raccourcis dans le Cloud Shell sur des ordinateurs Windows, utilisez Ctrl + Inser et MAJ + INSER toocopy et collez respectivement.</span><span class="sxs-lookup"><span data-stu-id="08534-121">Ctrl+C and Ctrl+V do not function as copy/paste shortcuts in Cloud Shell on Windows machines, use Ctrl+Insert and Shift+Insert toocopy and paste respectively.</span></span>

<span data-ttu-id="08534-122">Avec le bouton Copier-coller options sont également disponibles, mais avec le bouton fonction est un accès au Presse-papiers de toobrowser spécifiques sujet.</span><span class="sxs-lookup"><span data-stu-id="08534-122">Right-click copy-and-paste options are also available, but right-click function is subject toobrowser-specific clipboard access.</span></span>

## <a name="editing-bashrc"></a><span data-ttu-id="08534-123">Modifier .bashrc</span><span class="sxs-lookup"><span data-stu-id="08534-123">Editing .bashrc</span></span>
<span data-ttu-id="08534-124">Faites attention lorsque vous modifiez .bashrc : cela peut entraîner des erreurs inattendues dans Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="08534-124">Take caution when editing .bashrc, doing so can cause unexpected errors in Cloud Shell.</span></span>

## <a name="bashhistory"></a><span data-ttu-id="08534-125">.bash_history</span><span class="sxs-lookup"><span data-stu-id="08534-125">.bash_history</span></span>
<span data-ttu-id="08534-126">Votre historique de commandes de l’interpréteur de commandes risque d’être incohérent en raison d’interruptions de sessions Cloud Shell ou de sessions simultanées.</span><span class="sxs-lookup"><span data-stu-id="08534-126">Your history of bash commands may be inconsistent because of Cloud Shell session disruption or concurrent sessions.</span></span>

## <a name="usage-limits"></a><span data-ttu-id="08534-127">Limites d’utilisation</span><span class="sxs-lookup"><span data-stu-id="08534-127">Usage limits</span></span>
<span data-ttu-id="08534-128">Cloud Shell est destiné aux cas d’usage interactif.</span><span class="sxs-lookup"><span data-stu-id="08534-128">Cloud Shell is intended for interactive use cases.</span></span> <span data-ttu-id="08534-129">De fait, les sessions non interactives longues se terminent sans avertissement.</span><span class="sxs-lookup"><span data-stu-id="08534-129">As a result, any long-running non-interactive sessions are ended without warning.</span></span>

## <a name="network-connectivity"></a><span data-ttu-id="08534-130">Connectivité réseau</span><span class="sxs-lookup"><span data-stu-id="08534-130">Network connectivity</span></span>
<span data-ttu-id="08534-131">Aucun temps d’attente dans un environnement de Cloud est connecté à internet toolocal sujet, Cloud Shell continue toocarry tooattempt les instructions envoyées.</span><span class="sxs-lookup"><span data-stu-id="08534-131">Any latency in Cloud Shell is subject toolocal internet connectivity, Cloud Shell continues tooattempt toocarry out any instructions sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08534-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="08534-132">Next steps</span></span>
[<span data-ttu-id="08534-133">Démarrage rapide de Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="08534-133">Cloud Shell Quickstart</span></span>](quickstart.md)
