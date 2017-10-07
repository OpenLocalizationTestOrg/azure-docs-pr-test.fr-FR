---
title: "aaaMicrosoft outil de modélisation des menaces - Azure | Documents Microsoft"
description: "En savoir plus sur toutes les fonctionnalités de hello disponibles dans l’outil de modélisation des menaces de hello"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: f9ad5e623e7758063084cb7fc723c5735161a846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="threat-modeling-tool-feature-overview"></a><span data-ttu-id="6e5d5-103">Vue d’ensemble de la fonctionnalité Outil de modélisation des menaces</span><span class="sxs-lookup"><span data-stu-id="6e5d5-103">Threat Modeling Tool feature overview</span></span>

<span data-ttu-id="6e5d5-104">Nous sommes heureux que vous avez choisi toouse hello outil de modélisation des menaces pour vos besoins de modélisation des menaces !</span><span class="sxs-lookup"><span data-stu-id="6e5d5-104">We are glad you chose toouse hello Threat Modeling Tool for your threat modeling needs!</span></span> <span data-ttu-id="6e5d5-105">Si vous n’avez pas encore fait, visitez  **[prise en main de hello outil de modélisation des menaces](./azure-security-threat-modeling-tool-getting-started.md)**  notions de base toolearn hello.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-105">If you haven’t done so, visit **[Getting Started with hello Threat Modeling Tool](./azure-security-threat-modeling-tool-getting-started.md)** toolearn hello basics.</span></span>

> <span data-ttu-id="6e5d5-106">Notre outil est souvent mis à jour, reportez-vous à ce guide souvent toosee nos dernières fonctionnalités et améliorations.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-106">Our tool is updated often, so check this guide often toosee our latest features and improvements.</span></span>

<span data-ttu-id="6e5d5-107">En cliquant sur le bouton de « Création d’un modèle » hello ouvre une page de démarrage vierge, l’image toohello similaire ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="6e5d5-107">Clicking on hello "Create a New Model" button opens a blank start page, similar toohello image below:</span></span>

![Page de démarrage vierge](./media/azure-security-threat-modeling-tool/tmtstart.png)

<span data-ttu-id="6e5d5-109">À l’aide du modèle des menaces hello créées par notre équipe Bonjour  **[mise en route](./azure-security-threat-modeling-tool-getting-started.md)**  exemple, nous allons nous pencher toutes les fonctionnalités de hello disponibles dans l’outil de hello aujourd'hui.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-109">Using hello threat model created by our team in hello **[Getting Started](./azure-security-threat-modeling-tool-getting-started.md)** example, let’s check out all hello features available in hello tool today.</span></span>

![Modèle de menaces de base](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a><span data-ttu-id="6e5d5-111">Navigation</span><span class="sxs-lookup"><span data-stu-id="6e5d5-111">Navigation</span></span>

<span data-ttu-id="6e5d5-112">Avant de plonger dans les fonctionnalités intégrées hello, Attardons-nous sur hello principaux composants de hello outil</span><span class="sxs-lookup"><span data-stu-id="6e5d5-112">Before diving into hello built-in features, let’s go over hello main components found in hello tool</span></span>

### <a name="menu-items"></a><span data-ttu-id="6e5d5-113">Éléments de menu</span><span class="sxs-lookup"><span data-stu-id="6e5d5-113">Menu items</span></span>

<span data-ttu-id="6e5d5-114">expérience de Hello doit être d’autres produits Microsoft tooother similaires.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-114">hello experience should be similar tooother Microsoft products.</span></span> <span data-ttu-id="6e5d5-115">Commençons par l’intermédiaire des éléments de menu de niveau supérieur hello :</span><span class="sxs-lookup"><span data-stu-id="6e5d5-115">Let’s begin by going through hello top-level menu items:</span></span>

![Éléments de menu](./media/azure-security-threat-modeling-tool/menuitems.png)

| <span data-ttu-id="6e5d5-117">Étiquette</span><span class="sxs-lookup"><span data-stu-id="6e5d5-117">Label</span></span>                               | <span data-ttu-id="6e5d5-118">Détails</span><span class="sxs-lookup"><span data-stu-id="6e5d5-118">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="6e5d5-119">**File**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-119">**File**</span></span> | <ul><li><span data-ttu-id="6e5d5-120">Ouvrir, enregistrer et fermer des fichiers</span><span class="sxs-lookup"><span data-stu-id="6e5d5-120">Open, Save and Close Files</span></span></li><li><span data-ttu-id="6e5d5-121">Connexion et déconnexion aux comptes OneDrive</span><span class="sxs-lookup"><span data-stu-id="6e5d5-121">Sign In/Out of OneDrive accounts</span></span></li><li><span data-ttu-id="6e5d5-122">Partager des liens (Afficher + Modifier)</span><span class="sxs-lookup"><span data-stu-id="6e5d5-122">Share Links (View + Edit)</span></span></li><li><span data-ttu-id="6e5d5-123">Afficher les informations sur le fichier</span><span class="sxs-lookup"><span data-stu-id="6e5d5-123">View File Information</span></span></li><li><span data-ttu-id="6e5d5-124">Appliquer le nouveau modèle tooExisting modèles</span><span class="sxs-lookup"><span data-stu-id="6e5d5-124">Apply New Template tooExisting Models</span></span></li></ul> |
| <span data-ttu-id="6e5d5-125">**Modifier**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-125">**Edit**</span></span> | <span data-ttu-id="6e5d5-126">Annuler/rétablir des actions, ainsi que copier, coller et supprimer</span><span class="sxs-lookup"><span data-stu-id="6e5d5-126">Undo/redo actions, as well a copy, paste and delete</span></span> |
| <span data-ttu-id="6e5d5-127">**Afficher**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-127">**View**</span></span> | <ul><li><span data-ttu-id="6e5d5-128">Basculer entre les vues **Analyse** et **Conception**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-128">Switch between **Analysis** and **Design** views</span></span></li><li><span data-ttu-id="6e5d5-129">Ouvrir des fenêtres fermées (par ex. gabarits, propriétés des éléments et messages)</span><span class="sxs-lookup"><span data-stu-id="6e5d5-129">Open closed windows (e.g.stencils, element properties and messages)</span></span></li><li><span data-ttu-id="6e5d5-130">Réinitialiser les paramètres de disposition toodefault</span><span class="sxs-lookup"><span data-stu-id="6e5d5-130">Reset layout toodefault settings</span></span></li></ul> |
| <span data-ttu-id="6e5d5-131">**Diagramme**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-131">**Diagram**</span></span> | <span data-ttu-id="6e5d5-132">Ajouter/supprimer des diagrammes et naviguer dans les « onglets » des diagrammes</span><span class="sxs-lookup"><span data-stu-id="6e5d5-132">Add/Delete diagrams and navigate through “tabs” of diagrams</span></span> |
| <span data-ttu-id="6e5d5-133">**Rapports**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-133">**Reports**</span></span> | <span data-ttu-id="6e5d5-134">Créer des tooshare de rapports HTML avec d’autres utilisateurs</span><span class="sxs-lookup"><span data-stu-id="6e5d5-134">Create HTML reports tooshare with others</span></span> |
| <span data-ttu-id="6e5d5-135">**Aide**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-135">**Help**</span></span> | <span data-ttu-id="6e5d5-136">Guide toohelp que vous utilisez l’outil de hello</span><span class="sxs-lookup"><span data-stu-id="6e5d5-136">Guides toohelp you use hello tool</span></span> |

<span data-ttu-id="6e5d5-137">icônes de Hello sont des raccourcis pour les menus de niveau supérieur hello :</span><span class="sxs-lookup"><span data-stu-id="6e5d5-137">hello icons are shortcuts for hello top-level menus:</span></span>

| <span data-ttu-id="6e5d5-138">Icône</span><span class="sxs-lookup"><span data-stu-id="6e5d5-138">Icon</span></span>                               | <span data-ttu-id="6e5d5-139">Détails</span><span class="sxs-lookup"><span data-stu-id="6e5d5-139">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="6e5d5-140">**Ouvrir**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-140">**Open**</span></span> | <span data-ttu-id="6e5d5-141">Ouvre un nouveau fichier</span><span class="sxs-lookup"><span data-stu-id="6e5d5-141">Opens a new file</span></span> |
| <span data-ttu-id="6e5d5-142">**Save**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-142">**Save**</span></span> | <span data-ttu-id="6e5d5-143">Enregistre le fichier en cours</span><span class="sxs-lookup"><span data-stu-id="6e5d5-143">Saves current file</span></span> |
| <span data-ttu-id="6e5d5-144">**Conception**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-144">**Design**</span></span> | <span data-ttu-id="6e5d5-145">Accède au Mode création, où vous avez créé des modèles</span><span class="sxs-lookup"><span data-stu-id="6e5d5-145">Goes into design view, where you can create models</span></span> |
| <span data-ttu-id="6e5d5-146">**Analyser**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-146">**Analyze**</span></span> | <span data-ttu-id="6e5d5-147">Indique les menaces générées et leurs propriétés</span><span class="sxs-lookup"><span data-stu-id="6e5d5-147">Shows generated threats and their properties</span></span> |
| <span data-ttu-id="6e5d5-148">**Ajouter un diagramme**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-148">**Add Diagram**</span></span> | <span data-ttu-id="6e5d5-149">Ajoute un nouveau schéma (similaire toonew onglets dans Excel)</span><span class="sxs-lookup"><span data-stu-id="6e5d5-149">Adds new diagram (similar toonew tabs in Excel)</span></span> |
| <span data-ttu-id="6e5d5-150">**Supprimer un diagramme**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-150">**Delete Diagram**</span></span> | <span data-ttu-id="6e5d5-151">Supprime le diagramme actuel</span><span class="sxs-lookup"><span data-stu-id="6e5d5-151">Deletes current diagram</span></span> |
| <span data-ttu-id="6e5d5-152">**Copier/Couper/Coller**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-152">**Copy/Cut/Paste**</span></span> | <span data-ttu-id="6e5d5-153">Copie, coupe, colle des éléments</span><span class="sxs-lookup"><span data-stu-id="6e5d5-153">Copies/cuts/pastes elements</span></span> |
| <span data-ttu-id="6e5d5-154">**Annuler/Rétablir**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-154">**Undo/Redo**</span></span> | <span data-ttu-id="6e5d5-155">Annule/rétablit des actions</span><span class="sxs-lookup"><span data-stu-id="6e5d5-155">Undoes/redoes actions</span></span> |
| <span data-ttu-id="6e5d5-156">**Zoom avant / Zoom arrière**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-156">**Zoom In/Zoom Out**</span></span> | <span data-ttu-id="6e5d5-157">Effectue un zoom et diagramme hello pour une meilleure vue</span><span class="sxs-lookup"><span data-stu-id="6e5d5-157">Zooms in and out of hello diagram for a better view</span></span> |
| <span data-ttu-id="6e5d5-158">**Commentaires**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-158">**Feedback**</span></span> | <span data-ttu-id="6e5d5-159">Ouvre hello Forum MSDN</span><span class="sxs-lookup"><span data-stu-id="6e5d5-159">Opens hello MSDN Forum</span></span> |

### <a name="canvas"></a><span data-ttu-id="6e5d5-160">Canevas</span><span class="sxs-lookup"><span data-stu-id="6e5d5-160">Canvas</span></span>

<span data-ttu-id="6e5d5-161">espace de Hello où vous faites glisser et déposez les éléments dans.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-161">hello space where you drag and drop elements into.</span></span> <span data-ttu-id="6e5d5-162">Glisser -déplacer est hello plus rapide et des modèles de toobuild de façon plus efficaces.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-162">Drag and drop is hello quickest and most efficient way toobuild models.</span></span> <span data-ttu-id="6e5d5-163">Vous pouvez également cliquez droit et sélectionner à partir du menu hello, qui ajoute des versions génériques d’éléments hello que vous utilisez, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-163">You may also right click and select from hello menu, which adds generic versions of hello elements you’re using, as shown below.</span></span>

#### <a name="dropping-hello-stencil-on-hello-canvas"></a><span data-ttu-id="6e5d5-164">Suppression du stencil de hello sur la zone de dessin hello</span><span class="sxs-lookup"><span data-stu-id="6e5d5-164">Dropping hello stencil on hello canvas</span></span>

![Dépôt du canevas](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-hello-stencil"></a><span data-ttu-id="6e5d5-166">En cliquant sur un gabarit de hello</span><span class="sxs-lookup"><span data-stu-id="6e5d5-166">Clicking on hello stencil</span></span>

![Propriétés de l’élément](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a><span data-ttu-id="6e5d5-168">Gabarits</span><span class="sxs-lookup"><span data-stu-id="6e5d5-168">Stencils</span></span>

<span data-ttu-id="6e5d5-169">Où vous pouvez trouver tous les stencils toouse disponible en fonction de modèle hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-169">Where you can find all stencils available toouse based on hello template selected.</span></span> <span data-ttu-id="6e5d5-170">Si vous ne pouvez pas rechercher des éléments de droite hello, essayez d’utiliser un autre modèle ou modifiez un toofit vos besoins.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-170">If you can’t find hello right elements, try using another template, or modify one toofit your needs.</span></span> <span data-ttu-id="6e5d5-171">En règle générale, vous devez être en mesure de toofind une combinaison de catégories, telles que hello celles ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="6e5d5-171">Generally, you should be able toofind a combination of categories like hello ones below:</span></span>

| <span data-ttu-id="6e5d5-172">Nom du gabarit</span><span class="sxs-lookup"><span data-stu-id="6e5d5-172">Stencil Name</span></span>                               | <span data-ttu-id="6e5d5-173">Détails</span><span class="sxs-lookup"><span data-stu-id="6e5d5-173">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="6e5d5-174">**Processus**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-174">**Process**</span></span> | <span data-ttu-id="6e5d5-175">Applications, plug-ins de navigateur, menaces, machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="6e5d5-175">Applications, Browser Plugins, Threads, Virtual Machines</span></span> |
| <span data-ttu-id="6e5d5-176">**Interacteur externe**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-176">**External Interactor**</span></span> | <span data-ttu-id="6e5d5-177">Fournisseurs d’authentification, navigateurs, utilisateurs, applications Web</span><span class="sxs-lookup"><span data-stu-id="6e5d5-177">Authentication Providers, Browsers, Users, Web Applications</span></span> |
| <span data-ttu-id="6e5d5-178">**Banque de données**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-178">**Data Store**</span></span> | <span data-ttu-id="6e5d5-179">Cache, stockage, fichiers de configuration, bases de données, registre</span><span class="sxs-lookup"><span data-stu-id="6e5d5-179">Cache, Storage, Configuration Files, Databases, Registry</span></span> |
| <span data-ttu-id="6e5d5-180">**Flux de données**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-180">**Data Flow**</span></span> | <span data-ttu-id="6e5d5-181">Binaire, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, canal nommé, DCOM/RPC, SMB, UDP</span><span class="sxs-lookup"><span data-stu-id="6e5d5-181">Binary, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, Named Pipe, RPC/DCOM, SMB, UDP</span></span> |
| <span data-ttu-id="6e5d5-182">**Limites de bordure/ligne d’approbation**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-182">**Trust Line/Border Boundary**</span></span> | <span data-ttu-id="6e5d5-183">Réseaux d’entreprise, Internet, machine, Sandbox, mode utilisateur/noyau</span><span class="sxs-lookup"><span data-stu-id="6e5d5-183">Corporate Networks, Internet, Machine, Sandbox, User/Kernel Mode</span></span> |

### <a name="notesmessages"></a><span data-ttu-id="6e5d5-184">Remarques/messages</span><span class="sxs-lookup"><span data-stu-id="6e5d5-184">Notes/Messages</span></span>

| <span data-ttu-id="6e5d5-185">Composant</span><span class="sxs-lookup"><span data-stu-id="6e5d5-185">Component</span></span>                               | <span data-ttu-id="6e5d5-186">Détails</span><span class="sxs-lookup"><span data-stu-id="6e5d5-186">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="6e5d5-187">**Messages**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-187">**Messages**</span></span> | <span data-ttu-id="6e5d5-188">Logique d’outil interne qui avertit les utilisateurs chaque fois qu’il existe une erreur, telle qu’aucun flux de données entre des éléments</span><span class="sxs-lookup"><span data-stu-id="6e5d5-188">Internal tool logic that alerts users whenever there is an error, such as no data flows between elements</span></span> |
| <span data-ttu-id="6e5d5-189">**Remarques**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-189">**Notes**</span></span> | <span data-ttu-id="6e5d5-190">Notes manuelles fichier toohello ajoutés par les équipes d’ingénierie dans hello de conception et de révision</span><span class="sxs-lookup"><span data-stu-id="6e5d5-190">Manual notes added toohello file by engineering teams throughout hello design and review process</span></span> |

### <a name="element-properties"></a><span data-ttu-id="6e5d5-191">Propriétés de l’élément</span><span class="sxs-lookup"><span data-stu-id="6e5d5-191">Element properties</span></span>

<span data-ttu-id="6e5d5-192">Ceux-ci varient selon les éléments hello sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-192">These vary by hello elements selected.</span></span> <span data-ttu-id="6e5d5-193">En dehors des limites d’approbation, tous les autres éléments contiennent 3 sélections générales :</span><span class="sxs-lookup"><span data-stu-id="6e5d5-193">Apart from Trust Boundaries, all other elements contain 3 general selections:</span></span>

| <span data-ttu-id="6e5d5-194">Propriété d’élément</span><span class="sxs-lookup"><span data-stu-id="6e5d5-194">Element Property</span></span>                               | <span data-ttu-id="6e5d5-195">Détails</span><span class="sxs-lookup"><span data-stu-id="6e5d5-195">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="6e5d5-196">**Name**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-196">**Name**</span></span> | <span data-ttu-id="6e5d5-197">Utile pour nommer votre toobe de processus, magasins et les flux, INTERACTEURS facilement reconnu</span><span class="sxs-lookup"><span data-stu-id="6e5d5-197">Useful for naming your processes, stores, interactors and flows toobe easily recognized</span></span> |
| <span data-ttu-id="6e5d5-198">**Hors de portée**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-198">**Out of Scope**</span></span> | <span data-ttu-id="6e5d5-199">Si sélectionné, élément de hello est extraite de matrice de génération de menace hello (non recommandé)</span><span class="sxs-lookup"><span data-stu-id="6e5d5-199">If selected, hello element is taken out of hello threat generation matrix (not recommended)</span></span> |
| <span data-ttu-id="6e5d5-200">**Raison de l’hors de portée**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-200">**Reason for Out of Scope**</span></span> | <span data-ttu-id="6e5d5-201">Les utilisateurs de justification champ toolet savent pourquoi hors de portée a été sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-201">Justification field toolet users know why out of scope was selected</span></span> |

<span data-ttu-id="6e5d5-202">Les propriétés sont modifiées pour chaque catégorie d’élément.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-202">Properties are changed under each element category.</span></span> <span data-ttu-id="6e5d5-203">Cliquez sur chaque options disponibles d’élément tooinspect hello ou ouvrez toolearn de modèle hello plus.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-203">Click on each element tooinspect hello available options, or open hello template toolearn more.</span></span> <span data-ttu-id="6e5d5-204">Passons maintenant les fonctionnalités hello.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-204">Let’s get into hello features.</span></span>

## <a name="welcome-screen"></a><span data-ttu-id="6e5d5-205">Écran d’accueil</span><span class="sxs-lookup"><span data-stu-id="6e5d5-205">Welcome screen</span></span>

<span data-ttu-id="6e5d5-206">écran d’accueil Hello est hello première vue lorsque vous ouvrez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-206">hello welcome screen is hello first thing you see when you open hello app.</span></span>

### <a name="open-a-model"></a><span data-ttu-id="6e5d5-207">Ouvrir un modèle</span><span class="sxs-lookup"><span data-stu-id="6e5d5-207">Open A model</span></span>

<span data-ttu-id="6e5d5-208">Passez la souris sur le bouton « Ouvrir un modèle » pour afficher 2 options masquées : « Ouvrir depuis cet ordinateur » et « Ouvrir depuis OneDrive. »</span><span class="sxs-lookup"><span data-stu-id="6e5d5-208">Hovering over “Open a Model” button shows you 2 hidden options: “Open From this Computer” and “Open from OneDrive.”</span></span> <span data-ttu-id="6e5d5-209">Hello ouvre d’abord écran ouvrir le fichier de hello, tandis que hello ensuite vous accompagne tout processus de connexion hello pour OneDrive, autorisant les fichiers et dossiers de toopick après une authentification réussie.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-209">hello first opens hello File Open screen, while hello second takes you through hello sign in process for OneDrive, allowing you toopick folders and files after a successful authentication.</span></span>

![Ouvrir un modèle](./media/azure-security-threat-modeling-tool/openmodel.png)

![Ouvrir depuis l’ordinateur ou OneDrive](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a><span data-ttu-id="6e5d5-212">Commentaires, suggestions et problèmes</span><span class="sxs-lookup"><span data-stu-id="6e5d5-212">Feedback, suggestions and issues</span></span>

<span data-ttu-id="6e5d5-213">Cette option vous amènera toohello sur les Forums MSDN pour les outils de SDL.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-213">Selecting this option will take you toohello MSDN Forums for SDL Tools.</span></span> <span data-ttu-id="6e5d5-214">Il s’agit d’un toocheck excellent moyen des témoignages outil hello, y compris les solutions de contournement et de nouvelles idées sur les autres personnes.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-214">It’s a great way toocheck out what other people are saying about hello tool, including workarounds and new ideas.</span></span>

![Commentaires](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a><span data-ttu-id="6e5d5-216">Mode création</span><span class="sxs-lookup"><span data-stu-id="6e5d5-216">Design view</span></span>

<span data-ttu-id="6e5d5-217">Chaque fois que vous ouvrez ou créez un nouveau modèle, vous serez dirigé toohello en mode Création.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-217">Whenever you open or create a new model, you’ll be taken toohello design view.</span></span>

### <a name="adding-elements"></a><span data-ttu-id="6e5d5-218">Ajout d’éléments</span><span class="sxs-lookup"><span data-stu-id="6e5d5-218">Adding elements</span></span>

<span data-ttu-id="6e5d5-219">Il existe 2 méthodes tooadd éléments sur la grille de hello :</span><span class="sxs-lookup"><span data-stu-id="6e5d5-219">There are 2 ways tooadd elements on hello grid:</span></span>

- <span data-ttu-id="6e5d5-220">**Faites glisser et déposez** : faites glisser la grille de toohello hello élément souhaité, puis utilisez hello élément Propriétés tooprovide informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-220">**Drag and Drop** – drag hello desired element toohello grid, then use hello element properties tooprovide additional information.</span></span>
- <span data-ttu-id="6e5d5-221">**Bouton droit sur** : un clic droit n’importe où sur la grille de hello et sélectionnez dans la liste déroulante hello.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-221">**Right Click** – right click anywhere on hello grid and select from hello dropdown menu.</span></span> <span data-ttu-id="6e5d5-222">Une représentation générique de l’élément s’affiche sur l’écran hello.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-222">A generic representation of that element will appear on hello screen.</span></span>

### <a name="connecting-elements"></a><span data-ttu-id="6e5d5-223">Connexion des éléments</span><span class="sxs-lookup"><span data-stu-id="6e5d5-223">Connecting elements</span></span>

<span data-ttu-id="6e5d5-224">Il existe 2 méthodes tooconnect éléments dans l’outil de hello :</span><span class="sxs-lookup"><span data-stu-id="6e5d5-224">There are 2 ways tooconnect elements in hello tool:</span></span>

- <span data-ttu-id="6e5d5-225">**Faites glisser et déposez** : faites glisser la grille de toohello hello de flux de données souhaitée et connecter les deux extrémités toohello des éléments appropriés.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-225">**Drag and Drop** – drag hello desired dataflow toohello grid, and connect both ends toohello appropriate elements.</span></span>
- <span data-ttu-id="6e5d5-226">**Cliquez sur + MAJ** : cliquez sur l’élément de premier hello (envoi de données), appuyez sur et maintenez la touche MAJ de hello, puis sélectionnez hello deuxième élément (réception de données).</span><span class="sxs-lookup"><span data-stu-id="6e5d5-226">**Click + Shift** – click on hello first element (sending data), press and hold hello Shift key, then select hello second element (receiving data).</span></span> <span data-ttu-id="6e5d5-227">Cliquez avec le bouton droit, puis sélectionnez « Connecter ».</span><span class="sxs-lookup"><span data-stu-id="6e5d5-227">Right click, and select “Connect.”</span></span> <span data-ttu-id="6e5d5-228">Si vous utilisez un flux de données bidirectionnelle, l’ordre de hello n’est pas aussi important.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-228">If you’re using a bi-directional dataflow, hello order is not as important.</span></span>

### <a name="properties"></a><span data-ttu-id="6e5d5-229">Propriétés</span><span class="sxs-lookup"><span data-stu-id="6e5d5-229">Properties</span></span>

<span data-ttu-id="6e5d5-230">Affiche toutes les propriétés de hello qui peuvent être modifiées sur les gabarits hello placés dans le diagramme de hello.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-230">Shows all hello properties that can be modified on hello stencils placed in hello diagram.</span></span> <span data-ttu-id="6e5d5-231">propriétés de hello toosee, cliquez simplement sur gabarit de hello et informations de hello seront remplies en conséquence.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-231">toosee hello properties, just click on hello stencil and hello information will be populated accordingly.</span></span> <span data-ttu-id="6e5d5-232">exemple Hello ci-dessous montre avant et après un gabarit est déplacé vers le diagramme de hello « Database » :</span><span class="sxs-lookup"><span data-stu-id="6e5d5-232">hello example below shows before and after a "Database" stencil is dragged onto hello diagram:</span></span>

#### <a name="before"></a><span data-ttu-id="6e5d5-233">Avant</span><span class="sxs-lookup"><span data-stu-id="6e5d5-233">Before</span></span>

![Avant](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a><span data-ttu-id="6e5d5-235">Après</span><span class="sxs-lookup"><span data-stu-id="6e5d5-235">After</span></span>

![Après](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a><span data-ttu-id="6e5d5-237">Messages</span><span class="sxs-lookup"><span data-stu-id="6e5d5-237">Messages</span></span>

<span data-ttu-id="6e5d5-238">Si vous créez un modèle de menace et que vous oubliez tooelements de flux de données de tooconnect, fenêtre hello du message vous informe tooact.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-238">If you create a threat model and forget tooconnect data flows tooelements, hello message window notifies you tooact.</span></span> <span data-ttu-id="6e5d5-239">Vous pouvez choisir tooignore ou suivez hello problème de hello toofix obtenir des instructions.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-239">You can choose tooignore it or follow hello instructions toofix hello issue.</span></span> 

![Messages](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a><span data-ttu-id="6e5d5-241">Remarques</span><span class="sxs-lookup"><span data-stu-id="6e5d5-241">Notes</span></span>

<span data-ttu-id="6e5d5-242">Naviguez entre les onglets de Messages tooNotes permet de vous tooadd notes tooyour diagramme toocapture toutes vos idées</span><span class="sxs-lookup"><span data-stu-id="6e5d5-242">Switching tabs from Messages tooNotes allows you tooadd notes tooyour diagram toocapture all your thoughts</span></span>

## <a name="analysis-view"></a><span data-ttu-id="6e5d5-243">Vue d’analyse</span><span class="sxs-lookup"><span data-stu-id="6e5d5-243">Analysis view</span></span>

<span data-ttu-id="6e5d5-244">Une fois que vous avez terminé la création de votre diagramme basculer d’une tooanalysis vue en sélectionnant des sélections de menu du haut toohello et en choisissant la palette de peinture hello Loupe suivant toohello.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-244">Once you're done building your diagram, switch over tooanalysis view by going toohello top menu selections and choosing hello magnifying glass next toohello paint palette.</span></span>

![Vue d’analyse](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a><span data-ttu-id="6e5d5-246">Sélection de menaces générées</span><span class="sxs-lookup"><span data-stu-id="6e5d5-246">Generated threat selection</span></span>

<span data-ttu-id="6e5d5-247">Lorsque vous cliquez sur une menace, vous pouvez utiliser trois fonctions uniques :</span><span class="sxs-lookup"><span data-stu-id="6e5d5-247">When you click on a threat, you can leverage three unique functions:</span></span>

| <span data-ttu-id="6e5d5-248">Fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="6e5d5-248">Feature</span></span>                               | <span data-ttu-id="6e5d5-249">info</span><span class="sxs-lookup"><span data-stu-id="6e5d5-249">Info</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="6e5d5-250">**Indicateur de lecture**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-250">**Read Indicator**</span></span> | <p><span data-ttu-id="6e5d5-251">Menace est désormais marqué comme lu, ce qui peut facilement vous aider à effectuer le suivi des éléments de hello que vous avez déjà suivie</span><span class="sxs-lookup"><span data-stu-id="6e5d5-251">Threat is now marked as read, which can easily help you keep track of hello items you already went through</span></span></p><p>![Indicateur lu/non lu](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| <span data-ttu-id="6e5d5-253">**Focus d’interaction**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-253">**Interaction Focus**</span></span> | <p><span data-ttu-id="6e5d5-254">L’interaction dans le diagramme hello appartenant toothat menace est mis en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-254">Interaction in hello diagram belonging toothat threat is highlighted</span></span></p><p>![Focus d’interaction](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| <span data-ttu-id="6e5d5-256">**Propriétés de la menace**</span><span class="sxs-lookup"><span data-stu-id="6e5d5-256">**Threat Properties**</span></span> | <p><span data-ttu-id="6e5d5-257">Informations supplémentaires sur les menaces hello sont remplies dans la fenêtre Propriétés de menace hello</span><span class="sxs-lookup"><span data-stu-id="6e5d5-257">Additional information about hello threat is populated in hello threat properties window</span></span></p><p>![Propriétés de la menace](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a><span data-ttu-id="6e5d5-259">Modification de priorité</span><span class="sxs-lookup"><span data-stu-id="6e5d5-259">Priority change</span></span>

<span data-ttu-id="6e5d5-260">La modification du niveau de priorité hello de chaque menace généré change également leur toomake couleurs il tooidentify facilement les menaces de priorité haute, moyenne et basse.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-260">Changing hello priority level of each generated threat also changes their colors toomake it easy tooidentify high, medium and low priority threats.</span></span>

![Modification de priorité](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a><span data-ttu-id="6e5d5-262">Champs modifiables de propriétés de menaces</span><span class="sxs-lookup"><span data-stu-id="6e5d5-262">Threat properties editable fields</span></span>

<span data-ttu-id="6e5d5-263">Comme indiqué dans l’image hello ci-dessus, les utilisateurs peuvent modifier les informations de hello générées par l’outil de hello une également ajouter des champs de toocertain plus d’informations, telles que la justification.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-263">As seen in hello image above, users can change hello information generated by hello tool an also add information toocertain fields, such as justification.</span></span> <span data-ttu-id="6e5d5-264">Ces champs sont générés par le modèle de hello, donc si vous avez besoin de plus d’informations pour chaque menace, vous êtes invités toomake modifications.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-264">These fields are generated by hello template, so if you need more information for each threat, you're encouraged toomake modifications.</span></span>

![Propriétés de la menace](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a><span data-ttu-id="6e5d5-266">Rapports</span><span class="sxs-lookup"><span data-stu-id="6e5d5-266">Reports</span></span>

<span data-ttu-id="6e5d5-267">Une fois que vous avez terminé la modification des priorités et mise à jour hello état de chaque généré menace, vous pouvez enregistrer le fichier de hello ou imprimer un rapport en reçu trop « rapport » puis « Create rapport complet. »</span><span class="sxs-lookup"><span data-stu-id="6e5d5-267">Once you're done changing priorities and updating hello status of each generated threat, you can save hello file and/or print out a report by going too"Report" and then "Create Full Report."</span></span> <span data-ttu-id="6e5d5-268">Vous serez invité à indiquer rapport de hello tooname, et une fois que vous le faites, vous devez voir quelque chose de similaire image toohello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="6e5d5-268">You'll be asked tooname hello report, and once you do, you should see something similar toohello image below:</span></span>

![Rapport](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a><span data-ttu-id="6e5d5-270">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6e5d5-270">Next steps</span></span>

<span data-ttu-id="6e5d5-271">toocontribute un modèle pour la Communauté de hello, accédez à tooour  **[GitHub](https://github.com/Microsoft/threat-modeling-templates)**  page.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-271">toocontribute a template for hello community, please go tooour **[GitHub](https://github.com/Microsoft/threat-modeling-templates)** page.</span></span> <span data-ttu-id="6e5d5-272">**[Télécharger](https://aka.ms/tmtpreview)**  hello outil tooget dès aujourd'hui.</span><span class="sxs-lookup"><span data-stu-id="6e5d5-272">**[Download](https://aka.ms/tmtpreview)** hello tool tooget started today.</span></span>
