---
title: "Comment utiliser le journal d’audit dans Azure AD Privileged Identity Management | Microsoft Docs"
description: "Découvrez comment utiliser le journal d’audit dans l’extension Azure Privileged Identity Management."
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
ms.openlocfilehash: 7d9a5255a64d46c1388d328a606b3f297d61262b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-audit-log-in-pim"></a><span data-ttu-id="faf74-103">Utilisation du journal d’audit dans PIM</span><span class="sxs-lookup"><span data-stu-id="faf74-103">Using the audit log in PIM</span></span>
<span data-ttu-id="faf74-104">Vous pouvez utiliser le journal d’audit Privileged Identity Management (PIM) pour voir toutes les activations et affectations d’utilisateur dans un laps de temps donné.</span><span class="sxs-lookup"><span data-stu-id="faf74-104">You can use the Privileged Identity Management (PIM) audit log to see all the user assignments and activations within a given time period.</span></span> <span data-ttu-id="faf74-105">Si vous souhaitez consulter l’historique d’audit complet de l’activité dans votre client, notamment l’activité de l’administrateur, de l’utilisateur final et de la synchronisation, vous pouvez utiliser les [rapports d’accès et d’utilisation d’Azure Active Directory.](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="faf74-105">If you want to see the full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use the [Azure Active Directory access and usage reports.](active-directory-view-access-usage-reports.md)</span></span>

## <a name="navigate-to-the-audit-log"></a><span data-ttu-id="faf74-106">Accéder au journal d’audit</span><span class="sxs-lookup"><span data-stu-id="faf74-106">Navigate to the audit log</span></span>
<span data-ttu-id="faf74-107">À partir du [portail Azure](https://portal.azure.com) et du tableau de bord, sélectionnez l’application **Azure AD Privileged Identity Management** .</span><span class="sxs-lookup"><span data-stu-id="faf74-107">From the [Azure portal](https://portal.azure.com) dashboard, select the **Azure AD Privileged Identity Management** app.</span></span> <span data-ttu-id="faf74-108">À partir de là, accédez au journal d’audit en cliquant sur **Gérer les rôles privilégiés** > **Historique d’audit** dans le tableau de bord PIM.</span><span class="sxs-lookup"><span data-stu-id="faf74-108">From there, access the audit log by clicking **Manage privileged roles** > **Audit history** in the PIM dashboard.</span></span>

## <a name="the-audit-log-graph"></a><span data-ttu-id="faf74-109">Graphique du journal d’audit</span><span class="sxs-lookup"><span data-stu-id="faf74-109">The audit log graph</span></span>
<span data-ttu-id="faf74-110">Le journal d’audit indique le nombre total d’activations, le nombre maximal d’activations par jour et la moyenne d’activations par jour dans un graphique linéaire.</span><span class="sxs-lookup"><span data-stu-id="faf74-110">You can use the audit log to view the total activations, max activations per day, and average activations per day in a line graph.</span></span>  <span data-ttu-id="faf74-111">Vous pouvez également filtrer les données par rôle s’il existe plusieurs rôles dans l’historique d’audit.</span><span class="sxs-lookup"><span data-stu-id="faf74-111">You can also filter the data by role if there is more than one role in the audit history.</span></span>

<span data-ttu-id="faf74-112">Utilisez les boutons **temps**, **action** et **rôle** pour trier le journal.</span><span class="sxs-lookup"><span data-stu-id="faf74-112">Use the **time**, **action**, and **role** buttons to sort the log.</span></span>

## <a name="the-audit-log-list"></a><span data-ttu-id="faf74-113">Liste du journal d’audit</span><span class="sxs-lookup"><span data-stu-id="faf74-113">The audit log list</span></span>
<span data-ttu-id="faf74-114">Les colonnes dans la liste du journal d’audit sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="faf74-114">The columns in the audit log list are:</span></span>

* <span data-ttu-id="faf74-115">**Demandeur** : personne qui a demandé l’activation de rôle ou la modification.</span><span class="sxs-lookup"><span data-stu-id="faf74-115">**Requestor** - the user who requested the role activation or change.</span></span>  <span data-ttu-id="faf74-116">Si la valeur est « Système Azure », consultez le journal d'audit Azure pour plus d'informations.</span><span class="sxs-lookup"><span data-stu-id="faf74-116">If the value is "Azure System", check the Azure audit log for more information.</span></span>
* <span data-ttu-id="faf74-117">**Utilisateur** : l’utilisateur qui active un rôle ou y est affecté.</span><span class="sxs-lookup"><span data-stu-id="faf74-117">**User** - the user who is activating or assigned to a role.</span></span>
* <span data-ttu-id="faf74-118">**Rôle** : le rôle affecté ou activé par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="faf74-118">**Role** - the role assigned or activated by the user.</span></span>
* <span data-ttu-id="faf74-119">**Action** : les mesures prises par le demandeur.</span><span class="sxs-lookup"><span data-stu-id="faf74-119">**Action** - the actions taken by the requestor.</span></span> <span data-ttu-id="faf74-120">Ceci peut inclure l'attribution, la non-attribution, l’activation ou la désactivation.</span><span class="sxs-lookup"><span data-stu-id="faf74-120">This can include assignment, unassignment, activation, or deactivation.</span></span>
* <span data-ttu-id="faf74-121">**Heure** : heure à laquelle l’action s’est produite.</span><span class="sxs-lookup"><span data-stu-id="faf74-121">**Time** - when the action occurred.</span></span>
* <span data-ttu-id="faf74-122">**Motif** : tout texte éventuellement entré dans le champ de motif pendant l’activation.</span><span class="sxs-lookup"><span data-stu-id="faf74-122">**Reasoning** - if any text was entered into the reason field during activation, it will show up here.</span></span>
* <span data-ttu-id="faf74-123">**Expiration** : concerne uniquement l’activation de rôles.</span><span class="sxs-lookup"><span data-stu-id="faf74-123">**Expiration** - only relevant for activation of roles.</span></span>

## <a name="filter-the-audit-log"></a><span data-ttu-id="faf74-124">Filtrer le journal d’audit</span><span class="sxs-lookup"><span data-stu-id="faf74-124">Filter the audit log</span></span>
<span data-ttu-id="faf74-125">Vous pouvez filtrer les informations qui s’affichent dans le journal d’audit en cliquant sur le bouton **Filtre** .</span><span class="sxs-lookup"><span data-stu-id="faf74-125">You can filter the information that shows up in the audit log by clicking the **Filter** button.</span></span>  <span data-ttu-id="faf74-126">Le panneau **Mettre à jour les paramètres du graphique** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="faf74-126">The **Update chart parameters blade** will appear.</span></span>

<span data-ttu-id="faf74-127">Après avoir défini les filtres, cliquez sur **Mettre à jour** pour filtrer les données dans le journal.</span><span class="sxs-lookup"><span data-stu-id="faf74-127">After you set the filters, click **Update** to filter the data in the log.</span></span>  <span data-ttu-id="faf74-128">Si les données ne s’affichent pas immédiatement, actualisez la page.</span><span class="sxs-lookup"><span data-stu-id="faf74-128">If the data doesn't appear right away, refresh the page.</span></span>

### <a name="change-the-date-range"></a><span data-ttu-id="faf74-129">Modifier la plage de dates</span><span class="sxs-lookup"><span data-stu-id="faf74-129">Change the date range</span></span>
<span data-ttu-id="faf74-130">Utilisez les boutons **Aujourd’hui**, **Semaine passée**, **Mois Dernier** ou **Personnalisé**.</span><span class="sxs-lookup"><span data-stu-id="faf74-130">Use the **Today**, **Past Week**, **Past Month**, or **Custom** buttons to change the time range of the audit log.</span></span>

<span data-ttu-id="faf74-131">Si vous choisissez le bouton **Personnalisé**, les champs de date **De** et **À** s’affichent pour que vous puissiez spécifier une plage de dates pour le journal.</span><span class="sxs-lookup"><span data-stu-id="faf74-131">When you choose the **Custom** button, you will be given a **From** date field and a **To** date field to specify a range of dates for the log.</span></span>  <span data-ttu-id="faf74-132">Vous pouvez entrer les dates au format JJ/MM/AAAA ou cliquer sur l’icône de **calendrier** et sélectionner une date dans un calendrier.</span><span class="sxs-lookup"><span data-stu-id="faf74-132">You can either enter the dates in MM/DD/YYYY format or click on the **calendar** icon and choose the date from a calendar.</span></span>

### <a name="change-the-roles-included-in-the-log"></a><span data-ttu-id="faf74-133">Modifier les rôles inclus dans le journal</span><span class="sxs-lookup"><span data-stu-id="faf74-133">Change the roles included in the log</span></span>
<span data-ttu-id="faf74-134">Cochez (ou décochez) la case **Rôle** en regard de chaque rôle à inclure dans le journal (ou à exclure de ce dernier).</span><span class="sxs-lookup"><span data-stu-id="faf74-134">Check or uncheck the **Role** checkbox next to each role to include or exclude it from the log.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="faf74-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="faf74-135">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

