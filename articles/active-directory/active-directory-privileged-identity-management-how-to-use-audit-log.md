---
title: "journal d’audit aaaHow toouse hello dans Azure AD Privileged Identity Management | Documents Microsoft"
description: "Découvrez comment du journal d’audit de toouse hello dans l’extension d’Azure Privileged Identity Management hello."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 5d13a6dd-1fcb-4e76-82fb-cb2f4f0e4357
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 36987eaab9fe02c5dd7b4f4705e487299430745d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-audit-log-in-pim"></a><span data-ttu-id="9e537-103">À l’aide du journal d’audit de hello dans PIM</span><span class="sxs-lookup"><span data-stu-id="9e537-103">Using hello audit log in PIM</span></span>
<span data-ttu-id="9e537-104">Vous pouvez utiliser toosee de journal d’audit hello Privileged Identity Management (PIM) toutes les affectations d’utilisateur de hello et des activations sur une période donnée.</span><span class="sxs-lookup"><span data-stu-id="9e537-104">You can use hello Privileged Identity Management (PIM) audit log toosee all hello user assignments and activations within a given time period.</span></span> <span data-ttu-id="9e537-105">Si vous souhaitez que l’historique d’audit de hello toosee d’activité de votre client, y compris l’administrateur, utilisateur final et l’activité de synchronisation, vous pouvez utiliser hello [rapports d’accès et d’utilisation de Azure Active Directory.](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="9e537-105">If you want toosee hello full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use hello [Azure Active Directory access and usage reports.](active-directory-view-access-usage-reports.md)</span></span>

## <a name="navigate-toohello-audit-log"></a><span data-ttu-id="9e537-106">Parcourir le journal d’audit de toohello</span><span class="sxs-lookup"><span data-stu-id="9e537-106">Navigate toohello audit log</span></span>
<span data-ttu-id="9e537-107">À partir de hello [portail Azure](https://portal.azure.com) tableau de bord, sélectionnez hello **Azure AD Privileged Identity Management** application.</span><span class="sxs-lookup"><span data-stu-id="9e537-107">From hello [Azure portal](https://portal.azure.com) dashboard, select hello **Azure AD Privileged Identity Management** app.</span></span> <span data-ttu-id="9e537-108">À partir de là, vous pouvez accéder au journal d’audit de hello en cliquant sur **gérer les rôles privilégiés** > **historique d’Audit** dans le tableau de bord hello PIM.</span><span class="sxs-lookup"><span data-stu-id="9e537-108">From there, access hello audit log by clicking **Manage privileged roles** > **Audit history** in hello PIM dashboard.</span></span>

## <a name="hello-audit-log-graph"></a><span data-ttu-id="9e537-109">graphique de journal d’audit Hello</span><span class="sxs-lookup"><span data-stu-id="9e537-109">hello audit log graph</span></span>
<span data-ttu-id="9e537-110">Vous pouvez utiliser des activations totales hello du tooview journal hello audit activations maximales par jour et des activations moyenne par jour dans un graphique linéaire.</span><span class="sxs-lookup"><span data-stu-id="9e537-110">You can use hello audit log tooview hello total activations, max activations per day, and average activations per day in a line graph.</span></span>  <span data-ttu-id="9e537-111">Vous pouvez également filtrer les données de salutation par rôle, s’il existe plusieurs rôles dans l’historique d’audit de hello.</span><span class="sxs-lookup"><span data-stu-id="9e537-111">You can also filter hello data by role if there is more than one role in hello audit history.</span></span>

<span data-ttu-id="9e537-112">Hello d’utilisation **temps**, **action**, et **rôle** boutons toosort hello journal.</span><span class="sxs-lookup"><span data-stu-id="9e537-112">Use hello **time**, **action**, and **role** buttons toosort hello log.</span></span>

## <a name="hello-audit-log-list"></a><span data-ttu-id="9e537-113">liste des journaux d’audit Hello</span><span class="sxs-lookup"><span data-stu-id="9e537-113">hello audit log list</span></span>
<span data-ttu-id="9e537-114">les colonnes dans la liste des journaux d’audit hello Hello sont :</span><span class="sxs-lookup"><span data-stu-id="9e537-114">hello columns in hello audit log list are:</span></span>

* <span data-ttu-id="9e537-115">**Demandeur** -utilisateur hello qui a demandé l’activation de rôles hello ou de modification.</span><span class="sxs-lookup"><span data-stu-id="9e537-115">**Requestor** - hello user who requested hello role activation or change.</span></span>  <span data-ttu-id="9e537-116">Si la valeur de hello est « Système Azure », consultez le journal d’audit Azure hello pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="9e537-116">If hello value is "Azure System", check hello Azure audit log for more information.</span></span>
* <span data-ttu-id="9e537-117">**Utilisateur** -utilisateur hello est activation ou tooa de rôle.</span><span class="sxs-lookup"><span data-stu-id="9e537-117">**User** - hello user who is activating or assigned tooa role.</span></span>
* <span data-ttu-id="9e537-118">**Rôle** -rôle de hello attribuée ou activée par l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="9e537-118">**Role** - hello role assigned or activated by hello user.</span></span>
* <span data-ttu-id="9e537-119">**Action** - actions hello pris par le demandeur de hello.</span><span class="sxs-lookup"><span data-stu-id="9e537-119">**Action** - hello actions taken by hello requestor.</span></span> <span data-ttu-id="9e537-120">Ceci peut inclure l'attribution, la non-attribution, l’activation ou la désactivation.</span><span class="sxs-lookup"><span data-stu-id="9e537-120">This can include assignment, unassignment, activation, or deactivation.</span></span>
* <span data-ttu-id="9e537-121">**Heure** : lors de l’action de hello s’est produite.</span><span class="sxs-lookup"><span data-stu-id="9e537-121">**Time** - when hello action occurred.</span></span>
* <span data-ttu-id="9e537-122">**Raisonnement** -si n’importe quel texte a été entré dans le champ reason du hello lors de l’activation, il s’affiche ici.</span><span class="sxs-lookup"><span data-stu-id="9e537-122">**Reasoning** - if any text was entered into hello reason field during activation, it will show up here.</span></span>
* <span data-ttu-id="9e537-123">**Expiration** : concerne uniquement l’activation de rôles.</span><span class="sxs-lookup"><span data-stu-id="9e537-123">**Expiration** - only relevant for activation of roles.</span></span>

## <a name="filter-hello-audit-log"></a><span data-ttu-id="9e537-124">Filtrer le journal d’audit hello</span><span class="sxs-lookup"><span data-stu-id="9e537-124">Filter hello audit log</span></span>
<span data-ttu-id="9e537-125">Vous pouvez filtrer les informations de hello qui s’affiche dans le journal d’audit de hello en cliquant sur hello **filtre** bouton.</span><span class="sxs-lookup"><span data-stu-id="9e537-125">You can filter hello information that shows up in hello audit log by clicking hello **Filter** button.</span></span>  <span data-ttu-id="9e537-126">Hello **Panneau de paramètres de mise à jour graphique** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="9e537-126">hello **Update chart parameters blade** will appear.</span></span>

<span data-ttu-id="9e537-127">Une fois que vous définissez des filtres de hello, cliquez sur **mise à jour** toofilter les données de salutation dans le journal de hello.</span><span class="sxs-lookup"><span data-stu-id="9e537-127">After you set hello filters, click **Update** toofilter hello data in hello log.</span></span>  <span data-ttu-id="9e537-128">Si les données de salutation n’apparaissent pas immédiatement, actualisez la page de hello.</span><span class="sxs-lookup"><span data-stu-id="9e537-128">If hello data doesn't appear right away, refresh hello page.</span></span>

### <a name="change-hello-date-range"></a><span data-ttu-id="9e537-129">Modifier la plage de dates hello</span><span class="sxs-lookup"><span data-stu-id="9e537-129">Change hello date range</span></span>
<span data-ttu-id="9e537-130">Hello d’utilisation **aujourd'hui**, **semaine**, **mois**, ou **personnalisé** boutons période toochange hello du journal d’audit de hello.</span><span class="sxs-lookup"><span data-stu-id="9e537-130">Use hello **Today**, **Past Week**, **Past Month**, or **Custom** buttons toochange hello time range of hello audit log.</span></span>

<span data-ttu-id="9e537-131">Lorsque vous choisissez hello **personnalisé** bouton, vous aurez un **de** champ date et un **à** date champ toospecify une plage de dates pour le journal de hello.</span><span class="sxs-lookup"><span data-stu-id="9e537-131">When you choose hello **Custom** button, you will be given a **From** date field and a **To** date field toospecify a range of dates for hello log.</span></span>  <span data-ttu-id="9e537-132">Vous pouvez entrer des dates de hello dans le format MM/JJ/AAAA ou cliquez sur hello **calendrier** icône et choisir la date de hello dans un calendrier.</span><span class="sxs-lookup"><span data-stu-id="9e537-132">You can either enter hello dates in MM/DD/YYYY format or click on hello **calendar** icon and choose hello date from a calendar.</span></span>

### <a name="change-hello-roles-included-in-hello-log"></a><span data-ttu-id="9e537-133">Modifier les rôles hello inclus dans le journal de hello</span><span class="sxs-lookup"><span data-stu-id="9e537-133">Change hello roles included in hello log</span></span>
<span data-ttu-id="9e537-134">Activez ou désactivez hello **rôle** tooinclude rôle tooeach suivant de case à cocher ou les exclure de hello ouvrir une session.</span><span class="sxs-lookup"><span data-stu-id="9e537-134">Check or uncheck hello **Role** checkbox next tooeach role tooinclude or exclude it from hello log.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="9e537-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9e537-135">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

