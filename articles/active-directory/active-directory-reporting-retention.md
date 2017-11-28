---
title: "Stratégies de rétention des rapports Azure Active Directory | Microsoft Docs"
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
ms.openlocfilehash: ffeba8a6c32a21c75af21f948bbd6ea88dd9278c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-report-retention-policies"></a><span data-ttu-id="7de9b-103">Stratégies de rétention des rapports Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7de9b-103">Azure Active Directory report retention policies</span></span>


<span data-ttu-id="7de9b-104">Cette rubrique fournit des réponses aux questions plus courantes en rapport avec la conservation des données pour les différents rapports d’activité dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7de9b-104">This topic provides you with answers to the most common questions in conjunction with the data retention for the different activity reports in Azure Active Directory.</span></span> 

<span data-ttu-id="7de9b-105">**Q : Comment obtenir la collecte des données des activités démarrée ?**</span><span class="sxs-lookup"><span data-stu-id="7de9b-105">**Q: How can you get the collection of activity data started?**</span></span>

<span data-ttu-id="7de9b-106">**R :**</span><span class="sxs-lookup"><span data-stu-id="7de9b-106">**A:**</span></span>

| <span data-ttu-id="7de9b-107">Édition d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="7de9b-107">Azure AD Edition</span></span> | <span data-ttu-id="7de9b-108">Début de la collection</span><span class="sxs-lookup"><span data-stu-id="7de9b-108">Collection Start</span></span> |
| :--              | :--   |
| <span data-ttu-id="7de9b-109">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="7de9b-109">Azure AD Premium P1</span></span> <br /> <span data-ttu-id="7de9b-110">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="7de9b-110">Azure AD Premium P2</span></span> | <span data-ttu-id="7de9b-111">Lorsque vous vous inscrivez pour un abonnement</span><span class="sxs-lookup"><span data-stu-id="7de9b-111">When you sign-up for a subscription</span></span> |
| <span data-ttu-id="7de9b-112">Azure AD Gratuit</span><span class="sxs-lookup"><span data-stu-id="7de9b-112">Azure AD Free</span></span> | <span data-ttu-id="7de9b-113">La première fois que vous ouvrez le [panneau Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) ou utilisez les [API de création de rapports](https://aka.ms/aadreports)</span><span class="sxs-lookup"><span data-stu-id="7de9b-113">The first time you open the [Azure Active Directory blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) or use the [reporting APIs](https://aka.ms/aadreports)</span></span>  |

---
<span data-ttu-id="7de9b-114">**Q: Quand vos données d’activité sont-elles disponibles dans le portail Azure ?**</span><span class="sxs-lookup"><span data-stu-id="7de9b-114">**Q: When is your activity data available in the Azure portal?**</span></span>

<span data-ttu-id="7de9b-115">**R :**</span><span class="sxs-lookup"><span data-stu-id="7de9b-115">**A:**</span></span>

- <span data-ttu-id="7de9b-116">**Immédiatement** : si vous avez déjà travaillé avec des rapports dans le portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="7de9b-116">**Immediately** - If you have already been working with reports in the Azure classic portal</span></span>
- <span data-ttu-id="7de9b-117">**Dans les 2 heures** : si vous n’avez pas encore activé la création de rapports dans le portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="7de9b-117">**Within 2 hours** - If you haven’t turned reporting on  in the Azure classic portal</span></span>

---
<span data-ttu-id="7de9b-118">**Q : Comment obtenir la collecte des signaux de sécurité démarrée ?**</span><span class="sxs-lookup"><span data-stu-id="7de9b-118">**Q: How can you get the collection of security signals started?**</span></span>  

<span data-ttu-id="7de9b-119">**R :** Pour les signaux de sécurité, le processus de collecte démarre quand vous choisissez d’utiliser Identity Protection Center.</span><span class="sxs-lookup"><span data-stu-id="7de9b-119">**A:** For security signals, the collection process starts when you opt-in to use the Identity Protection Center.</span></span> 


---
<span data-ttu-id="7de9b-120">**Q : Pendant combien de temps les données collectées sont-elles stockées ?**</span><span class="sxs-lookup"><span data-stu-id="7de9b-120">**Q: For how long is the collected data stored?**</span></span>

<span data-ttu-id="7de9b-121">**R :**</span><span class="sxs-lookup"><span data-stu-id="7de9b-121">**A:**</span></span>

<span data-ttu-id="7de9b-122">**Rapports d’activité**</span><span class="sxs-lookup"><span data-stu-id="7de9b-122">**Activity reports**</span></span>    

| <span data-ttu-id="7de9b-123">Rapport</span><span class="sxs-lookup"><span data-stu-id="7de9b-123">Report</span></span>                 | <span data-ttu-id="7de9b-124">Azure AD Gratuit</span><span class="sxs-lookup"><span data-stu-id="7de9b-124">Azure AD Free</span></span> | <span data-ttu-id="7de9b-125">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="7de9b-125">Azure AD Premium P1</span></span> | <span data-ttu-id="7de9b-126">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="7de9b-126">Azure AD Premium P2</span></span> |
| :--                    | :--           | :--                 | :--                 |
| <span data-ttu-id="7de9b-127">Audit de répertoire</span><span class="sxs-lookup"><span data-stu-id="7de9b-127">Directory Audit</span></span>        | <span data-ttu-id="7de9b-128">7 jours</span><span class="sxs-lookup"><span data-stu-id="7de9b-128">7 days</span></span>        | <span data-ttu-id="7de9b-129">30 jours</span><span class="sxs-lookup"><span data-stu-id="7de9b-129">30 days</span></span>             | <span data-ttu-id="7de9b-130">30 jours</span><span class="sxs-lookup"><span data-stu-id="7de9b-130">30 days</span></span>             |
| <span data-ttu-id="7de9b-131">Activité de connexion</span><span class="sxs-lookup"><span data-stu-id="7de9b-131">Sign-in Activity</span></span>       | <span data-ttu-id="7de9b-132">7 jours</span><span class="sxs-lookup"><span data-stu-id="7de9b-132">7 days</span></span>        | <span data-ttu-id="7de9b-133">30 jours</span><span class="sxs-lookup"><span data-stu-id="7de9b-133">30 days</span></span>             | <span data-ttu-id="7de9b-134">30 jours</span><span class="sxs-lookup"><span data-stu-id="7de9b-134">30 days</span></span>             |

<span data-ttu-id="7de9b-135">**Signaux de sécurité**</span><span class="sxs-lookup"><span data-stu-id="7de9b-135">**Security Signals**</span></span>

| <span data-ttu-id="7de9b-136">Rapport</span><span class="sxs-lookup"><span data-stu-id="7de9b-136">Report</span></span>         | <span data-ttu-id="7de9b-137">Azure AD Gratuit</span><span class="sxs-lookup"><span data-stu-id="7de9b-137">Azure AD Free</span></span> | <span data-ttu-id="7de9b-138">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="7de9b-138">Azure AD Premium P1</span></span> | <span data-ttu-id="7de9b-139">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="7de9b-139">Azure AD Premium P2</span></span> |
| :--            | :--           | :--                 | :--                 |
| <span data-ttu-id="7de9b-140">Les utilisateurs à risque</span><span class="sxs-lookup"><span data-stu-id="7de9b-140">Users at risk</span></span>  | <span data-ttu-id="7de9b-141">7 jours</span><span class="sxs-lookup"><span data-stu-id="7de9b-141">7 days</span></span>        | <span data-ttu-id="7de9b-142">30 jours</span><span class="sxs-lookup"><span data-stu-id="7de9b-142">30 days</span></span>             | <span data-ttu-id="7de9b-143">90 jours</span><span class="sxs-lookup"><span data-stu-id="7de9b-143">90 days</span></span>             |
| <span data-ttu-id="7de9b-144">Connexions risquées</span><span class="sxs-lookup"><span data-stu-id="7de9b-144">Risky sign-ins</span></span> | <span data-ttu-id="7de9b-145">7 jours</span><span class="sxs-lookup"><span data-stu-id="7de9b-145">7 days</span></span>        | <span data-ttu-id="7de9b-146">30 jours</span><span class="sxs-lookup"><span data-stu-id="7de9b-146">30 days</span></span>             | <span data-ttu-id="7de9b-147">90 jours</span><span class="sxs-lookup"><span data-stu-id="7de9b-147">90 days</span></span>             |

---