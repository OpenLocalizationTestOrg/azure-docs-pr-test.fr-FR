---
title: "stratégies de rétention de rapport Active Directory aaaAzure | Documents Microsoft"
description: "Stratégies de rétention des données de rapport dans Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c46a68198cb34e9c92662b2f8461010745392c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-report-retention-policies"></a><span data-ttu-id="dd450-103">Stratégies de rétention des rapports Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd450-103">Azure Active Directory report retention policies</span></span>


<span data-ttu-id="dd450-104">Cette rubrique fournit des réponses toohello des questions courantes conjointement avec conservation des données hello pour les rapports d’activité différente hello dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dd450-104">This topic provides you with answers toohello most common questions in conjunction with hello data retention for hello different activity reports in Azure Active Directory.</span></span> 

<span data-ttu-id="dd450-105">**Q : comment obtenir collection hello de données d’activité a démarré ?**</span><span class="sxs-lookup"><span data-stu-id="dd450-105">**Q: How can you get hello collection of activity data started?**</span></span>

<span data-ttu-id="dd450-106">**R :**</span><span class="sxs-lookup"><span data-stu-id="dd450-106">**A:**</span></span>

| <span data-ttu-id="dd450-107">Édition d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd450-107">Azure AD Edition</span></span> | <span data-ttu-id="dd450-108">Début de la collection</span><span class="sxs-lookup"><span data-stu-id="dd450-108">Collection Start</span></span> |
| :--              | :--   |
| <span data-ttu-id="dd450-109">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="dd450-109">Azure AD Premium P1</span></span> <br /> <span data-ttu-id="dd450-110">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="dd450-110">Azure AD Premium P2</span></span> | <span data-ttu-id="dd450-111">Lorsque vous vous inscrivez pour un abonnement</span><span class="sxs-lookup"><span data-stu-id="dd450-111">When you sign-up for a subscription</span></span> |
| <span data-ttu-id="dd450-112">Azure AD Gratuit</span><span class="sxs-lookup"><span data-stu-id="dd450-112">Azure AD Free</span></span> | <span data-ttu-id="dd450-113">Hello la première fois que vous ouvrez hello [panneau d’Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) ou utilisez hello [API de création de rapports](https://aka.ms/aadreports)</span><span class="sxs-lookup"><span data-stu-id="dd450-113">hello first time you open hello [Azure Active Directory blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) or use hello [reporting APIs](https://aka.ms/aadreports)</span></span>  |

---
<span data-ttu-id="dd450-114">**Q : quand vos données d’activité est disponible dans hello portail Azure ?**</span><span class="sxs-lookup"><span data-stu-id="dd450-114">**Q: When is your activity data available in hello Azure portal?**</span></span>

<span data-ttu-id="dd450-115">**R :**</span><span class="sxs-lookup"><span data-stu-id="dd450-115">**A:**</span></span>

- <span data-ttu-id="dd450-116">**Immédiatement** : Si vous avez déjà travaillé avec des rapports Bonjour portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="dd450-116">**Immediately** - If you have already been working with reports in hello Azure classic portal</span></span>
- <span data-ttu-id="dd450-117">**Dans les 2 heures** : Si vous n’avez pas activé la création de rapports Bonjour portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="dd450-117">**Within 2 hours** - If you haven’t turned reporting on  in hello Azure classic portal</span></span>

---
<span data-ttu-id="dd450-118">**Q : comment obtenir collection hello de signaux de sécurité a démarré ?**</span><span class="sxs-lookup"><span data-stu-id="dd450-118">**Q: How can you get hello collection of security signals started?**</span></span>  

<span data-ttu-id="dd450-119">**R :** pour les signaux de sécurité, le processus de collecte hello démarre lorsque vous choisissez de participer toouse hello identité Protection Center.</span><span class="sxs-lookup"><span data-stu-id="dd450-119">**A:** For security signals, hello collection process starts when you opt-in toouse hello Identity Protection Center.</span></span> 


---
<span data-ttu-id="dd450-120">**Q : combien de temps est hello stockées les données collectées ?**</span><span class="sxs-lookup"><span data-stu-id="dd450-120">**Q: For how long is hello collected data stored?**</span></span>

<span data-ttu-id="dd450-121">**R :**</span><span class="sxs-lookup"><span data-stu-id="dd450-121">**A:**</span></span>

<span data-ttu-id="dd450-122">**Rapports d’activité**</span><span class="sxs-lookup"><span data-stu-id="dd450-122">**Activity reports**</span></span>    

| <span data-ttu-id="dd450-123">Rapport</span><span class="sxs-lookup"><span data-stu-id="dd450-123">Report</span></span>                 | <span data-ttu-id="dd450-124">Azure AD Gratuit</span><span class="sxs-lookup"><span data-stu-id="dd450-124">Azure AD Free</span></span> | <span data-ttu-id="dd450-125">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="dd450-125">Azure AD Premium P1</span></span> | <span data-ttu-id="dd450-126">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="dd450-126">Azure AD Premium P2</span></span> |
| :--                    | :--           | :--                 | :--                 |
| <span data-ttu-id="dd450-127">Audit de répertoire</span><span class="sxs-lookup"><span data-stu-id="dd450-127">Directory Audit</span></span>        | <span data-ttu-id="dd450-128">7 jours</span><span class="sxs-lookup"><span data-stu-id="dd450-128">7 days</span></span>        | <span data-ttu-id="dd450-129">30 jours</span><span class="sxs-lookup"><span data-stu-id="dd450-129">30 days</span></span>             | <span data-ttu-id="dd450-130">30 jours</span><span class="sxs-lookup"><span data-stu-id="dd450-130">30 days</span></span>             |
| <span data-ttu-id="dd450-131">Activité de connexion</span><span class="sxs-lookup"><span data-stu-id="dd450-131">Sign-in Activity</span></span>       | <span data-ttu-id="dd450-132">7 jours</span><span class="sxs-lookup"><span data-stu-id="dd450-132">7 days</span></span>        | <span data-ttu-id="dd450-133">30 jours</span><span class="sxs-lookup"><span data-stu-id="dd450-133">30 days</span></span>             | <span data-ttu-id="dd450-134">30 jours</span><span class="sxs-lookup"><span data-stu-id="dd450-134">30 days</span></span>             |

<span data-ttu-id="dd450-135">**Signaux de sécurité**</span><span class="sxs-lookup"><span data-stu-id="dd450-135">**Security Signals**</span></span>

| <span data-ttu-id="dd450-136">Rapport</span><span class="sxs-lookup"><span data-stu-id="dd450-136">Report</span></span>         | <span data-ttu-id="dd450-137">Azure AD Gratuit</span><span class="sxs-lookup"><span data-stu-id="dd450-137">Azure AD Free</span></span> | <span data-ttu-id="dd450-138">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="dd450-138">Azure AD Premium P1</span></span> | <span data-ttu-id="dd450-139">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="dd450-139">Azure AD Premium P2</span></span> |
| :--            | :--           | :--                 | :--                 |
| <span data-ttu-id="dd450-140">Les utilisateurs à risque</span><span class="sxs-lookup"><span data-stu-id="dd450-140">Users at risk</span></span>  | <span data-ttu-id="dd450-141">7 jours</span><span class="sxs-lookup"><span data-stu-id="dd450-141">7 days</span></span>        | <span data-ttu-id="dd450-142">30 jours</span><span class="sxs-lookup"><span data-stu-id="dd450-142">30 days</span></span>             | <span data-ttu-id="dd450-143">90 jours</span><span class="sxs-lookup"><span data-stu-id="dd450-143">90 days</span></span>             |
| <span data-ttu-id="dd450-144">Connexions risquées</span><span class="sxs-lookup"><span data-stu-id="dd450-144">Risky sign-ins</span></span> | <span data-ttu-id="dd450-145">7 jours</span><span class="sxs-lookup"><span data-stu-id="dd450-145">7 days</span></span>        | <span data-ttu-id="dd450-146">30 jours</span><span class="sxs-lookup"><span data-stu-id="dd450-146">30 days</span></span>             | <span data-ttu-id="dd450-147">90 jours</span><span class="sxs-lookup"><span data-stu-id="dd450-147">90 days</span></span>             |

---