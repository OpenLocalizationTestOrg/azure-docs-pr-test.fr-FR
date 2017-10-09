---
title: "fenêtre d’interpréteur de commandes de cloud computing Azure (aperçu) aaaUsing hello | Documents Microsoft"
description: "Fenêtre d’interpréteur de commandes Azure Cloud procédure pas à pas hello."
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
ms.date: 07/13/2017
ms.author: juluk
ms.openlocfilehash: 571db3c8e177799a9e05f38a7cf8d2a4d5f8c8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cloud-shell-window"></a><span data-ttu-id="7ab3b-103">À l’aide de la fenêtre d’interpréteur de commandes Azure Cloud hello</span><span class="sxs-lookup"><span data-stu-id="7ab3b-103">Using hello Azure Cloud Shell window</span></span>

<span data-ttu-id="7ab3b-104">Ce document explique comment toouse hello fenêtre Shell de Cloud.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-104">This document explains how toouse hello Cloud Shell window.</span></span>

## <a name="concurrent-sessions"></a><span data-ttu-id="7ab3b-105">Sessions simultanées</span><span class="sxs-lookup"><span data-stu-id="7ab3b-105">Concurrent sessions</span></span>
<span data-ttu-id="7ab3b-106">Cloud Shell permet à plusieurs sessions simultanées entre les onglets de navigateur en permettant à chaque tooexist de session en tant que processus séparé Bash.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-106">Cloud Shell enables multiple concurrent sessions across browser tabs by allowing each session tooexist as a separate Bash process.</span></span>
<span data-ttu-id="7ab3b-107">Si quitter une session, assurez-vous que chaque processus s’exécute indépendamment bien qu’elles s’exécutent sur tooexit à partir de chaque fenêtre de session hello même ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-107">If exiting a session, be sure tooexit from each session window as each process runs independently although they run on hello same machine.</span></span>

## <a name="restart-cloud-shell"></a><span data-ttu-id="7ab3b-108">Redémarrer Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="7ab3b-108">Restart Cloud Shell</span></span>
![](media/recycle.png)
> [!WARNING]
> <span data-ttu-id="7ab3b-109">Le redémarrage de Cloud Shell réinitialise l’état de la machine et tous les fichiers non conservés par votre partage de fichiers sont perdus.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-109">Restarting Cloud Shell will reset machine state and any files not persisted by your file share will be lost.</span></span>

* <span data-ttu-id="7ab3b-110">Cliquez sur icône du redémarrage hello sur la barre d’outils de hello tooreceive un nouvel environnement de Shell du Cloud.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-110">Click hello restart icon on hello toolbar tooreceive a new Cloud Shell environment.</span></span>

## <a name="minimize--maximize-cloud-shell-window"></a><span data-ttu-id="7ab3b-111">Réduire et agrandir la fenêtre Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="7ab3b-111">Minimize & maximize Cloud Shell window</span></span>
![](media/minmax.png)
* <span data-ttu-id="7ab3b-112">Cliquez sur hello réduire sur hello icône haut à droite de hello fenêtre toohide il.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-112">Click hello minimize icon on hello top right of hello window toohide it.</span></span> <span data-ttu-id="7ab3b-113">Recliquez sur hello icône Cloud Shell toounhide.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-113">Click hello Cloud Shell icon again toounhide.</span></span>
* <span data-ttu-id="7ab3b-114">Cliquez sur hello optimiser la hauteur de toomax icône tooset fenêtre.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-114">Click hello maximize icon tooset window toomax height.</span></span> <span data-ttu-id="7ab3b-115">toorestore fenêtre tooprevious taille, cliquez sur Restaurer.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-115">toorestore window tooprevious size, click restore.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="7ab3b-116">Copier et coller</span><span class="sxs-lookup"><span data-stu-id="7ab3b-116">Copy and paste</span></span>
* <span data-ttu-id="7ab3b-117">Windows : `Ctrl-insert` toocopy et `Shift-insert` toopaste.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-117">Windows: `Ctrl-insert` toocopy and `Shift-insert` toopaste.</span></span> <span data-ttu-id="7ab3b-118">Le menu déroulant accessible par un clic droit permet également de copier/coller.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-118">Right-click dropdown can also enable copy/paste.</span></span>
  * <span data-ttu-id="7ab3b-119">FireFox/IE peuvent ne pas prendre en charge correctement les autorisations de Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-119">FireFox/IE may not support clipboard permissions properly.</span></span>
* <span data-ttu-id="7ab3b-120">Mac OS : `Cmd-c` toocopy et `Cmd-v` toopaste.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-120">Mac OS: `Cmd-c` toocopy and `Cmd-v` toopaste.</span></span> <span data-ttu-id="7ab3b-121">Le menu déroulant accessible par un clic droit permet également de copier/coller.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-121">Right-click dropdown can also enable copy/paste.</span></span>

## <a name="resize-cloud-shell-window"></a><span data-ttu-id="7ab3b-122">Redimensionner la fenêtre Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="7ab3b-122">Resize Cloud Shell window</span></span>
* <span data-ttu-id="7ab3b-123">Cliquez et faites glisser de bord supérieur de hello de barre d’outils hello haut ou le bas de la fenêtre de l’interface de Cloud tooresize hello.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-123">Click and drag hello top edge of hello toolbar up or down tooresize hello Cloud Shell window.</span></span>

## <a name="scrolling-text-display"></a><span data-ttu-id="7ab3b-124">Défilement du texte</span><span class="sxs-lookup"><span data-stu-id="7ab3b-124">Scrolling text display</span></span>
* <span data-ttu-id="7ab3b-125">Défile avec le texte de terminal toomove tactile ou de la souris.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-125">Scroll with your mouse or touchpad toomove terminal text.</span></span>

## <a name="exit-command"></a><span data-ttu-id="7ab3b-126">Commande Quitter</span><span class="sxs-lookup"><span data-stu-id="7ab3b-126">Exit command</span></span>
<span data-ttu-id="7ab3b-127">En cours d’exécution `exit` met fin à la session active de hello.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-127">Running `exit` terminates hello active session.</span></span> <span data-ttu-id="7ab3b-128">Ce comportement se produit par défaut au bout de 20 minutes en l’absence d’interaction.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-128">This behavior occurs by default after 20 minutes without interaction.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ab3b-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7ab3b-129">Next steps</span></span>
[<span data-ttu-id="7ab3b-130">Démarrage rapide de Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="7ab3b-130">Cloud Shell Quickstart</span></span>](quickstart.md)
