---
title: aaaAzure Active Directory Reporting Forum aux questions | Documents Microsoft
description: FAQ sur les rapports Azure Active Directory.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 534da0b1-7858-4167-9986-7a62fbd10439
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: be65a05574ea3b5b190cd02a96b211c571ba70bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-faq"></a><span data-ttu-id="6d7e6-103">FAQ sur les rapports Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6d7e6-103">Azure Active Directory reporting FAQ</span></span>

<span data-ttu-id="6d7e6-104">Cet article inclut elles sonttrop des réponses aux questions (FAQ) sur les rapports d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6d7e6-104">This article includes answers toofrequently asked questions (FAQs) about Azure Active Directory reporting.</span></span>  
<span data-ttu-id="6d7e6-105">Pour plus d’informations, consultez la page [Rapports Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6d7e6-105">For more details, see [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span> 

<span data-ttu-id="6d7e6-106">**Q : quelle est la rétention des données pour les journaux d’activité (d’Audit et de connexions) hello Bonjour portail Azure ?**</span><span class="sxs-lookup"><span data-stu-id="6d7e6-106">**Q: What is hello data retention for activity logs (Audit and Sign-ins) in hello Azure portal?**</span></span> 

<span data-ttu-id="6d7e6-107">**R :** nous fournir 7 jours de données pour nos clients libres et en basculant tooan Azure AD Premium 1 ou une licence Premium 2, vous pouvez accéder aux données pour too30 jours.</span><span class="sxs-lookup"><span data-stu-id="6d7e6-107">**A:** We provide 7 days of data for our free customers and by switching tooan Azure AD Premium 1 or Premium 2 license, you can access data for up too30 days.</span></span> <span data-ttu-id="6d7e6-108">Pour plus d’informations sur la rétention, consultez la page [Stratégies de rétention des rapports Azure Active Directory](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="6d7e6-108">For more details on retention, see [Azure Active Directory report retention policies](active-directory-reporting-retention.md)</span></span>

--- 

<span data-ttu-id="6d7e6-109">**Q : combien de temps faut-il jusqu'à ce que je peux voir les données d’activité hello une fois que j’ai terminé ma tâche ?**</span><span class="sxs-lookup"><span data-stu-id="6d7e6-109">**Q: How long does it take until I can see hello Activity data after I have completed my task?**</span></span>

<span data-ttu-id="6d7e6-110">**R :** journaux d’activité d’Audit ont une latence comprise entre 15 minutes tooan heure.</span><span class="sxs-lookup"><span data-stu-id="6d7e6-110">**A:** Audit activity logs have a latency ranging from 15 mins tooan hour.</span></span> <span data-ttu-id="6d7e6-111">Les journaux d’activité de connexion ont une latence comprise entre 15 minutes pour la plupart des enregistrements et les heures de too2 pour quelques enregistrements.</span><span class="sxs-lookup"><span data-stu-id="6d7e6-111">Sign-in activity logs have a latency ranging from 15 mins for most records and up too2 hours for a few records.</span></span>

---

<span data-ttu-id="6d7e6-112">**Q : dois-je toobe qu'une activité de hello toosee administrateur général établie hello portail Azure ou données tooget via hello API ?**</span><span class="sxs-lookup"><span data-stu-id="6d7e6-112">**Q: Do I need toobe a global admin toosee hello activity logs in hello Azure Portal or tooget data through hello API?**</span></span>

<span data-ttu-id="6d7e6-113">**R :** Non.</span><span class="sxs-lookup"><span data-stu-id="6d7e6-113">**A:** No.</span></span> <span data-ttu-id="6d7e6-114">Vous pouvez être un **sécurité lecteur**, un **administrateur de la sécurité** ou un **administrateur Global** toosee rapportent des données dans le portail Azure ou en y accédant via hello API.</span><span class="sxs-lookup"><span data-stu-id="6d7e6-114">You can either be a **Security Reader**, a **Security Admin** or a **Global Admin** toosee reporting data in Azure Portal or by accessing it through hello API.</span></span>

---

<span data-ttu-id="6d7e6-115">**Q : puis-je obtenir des informations du journal d’activité Office 365 via hello portail Azure ?**</span><span class="sxs-lookup"><span data-stu-id="6d7e6-115">**Q: Can I get Office 365 activity log information through hello Azure portal?**</span></span>

<span data-ttu-id="6d7e6-116">**R :** bien activité d’Office 365 et Azure AD activité journaux partage un grand nombre des ressources d’annuaire hello, si vous souhaitez une vue complète de hello journaux d’activité Office 365, vous devez passer des informations du journal toohello centre d’administration Office 365 tooget Office 365 activité.</span><span class="sxs-lookup"><span data-stu-id="6d7e6-116">**A:** Even though Office 365 activity and Azure AD activity logs share a lot of hello directory resources, if you want a full view of hello Office 365 activity logs, you should go toohello Office 365 Admin Center tooget Office 365 Activity log information.</span></span>

---


<span data-ttu-id="6d7e6-117">**Q : qui les API utiliser tooget d’informations sur les journaux d’Office 365 activité ?**</span><span class="sxs-lookup"><span data-stu-id="6d7e6-117">**Q: Which APIs do I use tooget information about Office 365 Activity logs?**</span></span>

<span data-ttu-id="6d7e6-118">**R :** utilisez Bonjour API de gestion Office 365 tooaccess Bonjour [Office 365 activité se connecte via une API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span><span class="sxs-lookup"><span data-stu-id="6d7e6-118">**A:** Use hello Office 365 Management APIs tooaccess hello [Office 365 Activity logs through an API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span></span>

---

<span data-ttu-id="6d7e6-119">**Q : Combien d’enregistrements peut-on télécharger à partir du Portail Azure ?**</span><span class="sxs-lookup"><span data-stu-id="6d7e6-119">**Q: How many records I can download from Azure portal?**</span></span>

<span data-ttu-id="6d7e6-120">**R :** que vous pouvez télécharger des enregistrements de too120K de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6d7e6-120">**A:** You can download up too120K records from hello Azure portal.</span></span> <span data-ttu-id="6d7e6-121">Hello enregistrements sont triés par *plus récente* et par défaut, vous obtenez des enregistrements de hello plus récent 120 Ko.</span><span class="sxs-lookup"><span data-stu-id="6d7e6-121">hello records are sorted by *most recent* and by default, you get hello most recent 120K records.</span></span> 

---

<span data-ttu-id="6d7e6-122">**Q : le nombre d’enregistrements puis-je rechercher parmi les activités de hello API ?**</span><span class="sxs-lookup"><span data-stu-id="6d7e6-122">**Q: How many records can I query through hello activities API?**</span></span>

<span data-ttu-id="6d7e6-123">**R :** vous pouvez interroger les enregistrements de millions de too1 (si vous n’utilisez pas opérateur top hello, qui trie les enregistrement hello plus récente).</span><span class="sxs-lookup"><span data-stu-id="6d7e6-123">**A:** You can query up too1 million records (if you don’t use hello top operator, which sorts hello record by most recent).</span></span> <span data-ttu-id="6d7e6-124">Si vous utilisez l’opérateur « top » de hello, vous pouvez interroger les enregistrements de too500K.</span><span class="sxs-lookup"><span data-stu-id="6d7e6-124">If you do use hello “top” operator, you can query up too500K records.</span></span> <span data-ttu-id="6d7e6-125">Vous trouverez des exemples de requêtes sur la façon dont toouse hello API ici [ici](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="6d7e6-125">You can find sample queries on how toouse hello API here [here](active-directory-reporting-api-getting-started.md).</span></span>

---

<span data-ttu-id="6d7e6-126">**Q : Comment obtenir une licence Premium ?**</span><span class="sxs-lookup"><span data-stu-id="6d7e6-126">**Q: How do I get a premium license?**</span></span>

<span data-ttu-id="6d7e6-127">**R :** consultez [prise en main d’Azure Active Directory Premium](active-directory-get-started-premium.md) pour un toothis répondre à la question.</span><span class="sxs-lookup"><span data-stu-id="6d7e6-127">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer toothis question.</span></span>

---

<span data-ttu-id="6d7e6-128">**Q : Au bout de combien de temps peut-on consulter les données d’activité après avoir obtenu une licence Premium ?**</span><span class="sxs-lookup"><span data-stu-id="6d7e6-128">**Q: How soon should I see activities data after getting a premium license?**</span></span>

<span data-ttu-id="6d7e6-129">**R :** si vous avez déjà des données d’activités sous la forme d’une licence gratuite, vous pouvez voir hello des mêmes données.</span><span class="sxs-lookup"><span data-stu-id="6d7e6-129">**A:** If you already have activities data as a free license, then you can see hello same data.</span></span> <span data-ttu-id="6d7e6-130">Si vous n’avez pas de données, cela prendra un ou deux jours.</span><span class="sxs-lookup"><span data-stu-id="6d7e6-130">If you don’t have any data, then it will take one or two days.</span></span>

---

<span data-ttu-id="6d7e6-131">**Q : Peut-on voir les données du mois dernier après avoir obtenu une licence Azure AD Premium ?**</span><span class="sxs-lookup"><span data-stu-id="6d7e6-131">**Q: Do I see last month's data after getting an Azure AD premium license?**</span></span>

<span data-ttu-id="6d7e6-132">**R :** si vous avez récemment échangé version Premium de tooa (y compris une version d’évaluation), vous pouvez voir les données des jours de too7 initialement.</span><span class="sxs-lookup"><span data-stu-id="6d7e6-132">**A:** If you have recently switched tooa Premium version (including a trial version), you can see data up too7 days initially.</span></span> <span data-ttu-id="6d7e6-133">Lorsque les données s’accumulent, vous verrez too30 jours.</span><span class="sxs-lookup"><span data-stu-id="6d7e6-133">When data accumulates, you will see up too30 days.</span></span>

---

<span data-ttu-id="6d7e6-134">**Q : il existe un événement à risque dans la Protection d’identité, mais je ne vois pas connectez-vous correspondant Bonjour toutes les connexions. Est-ce normal ?**</span><span class="sxs-lookup"><span data-stu-id="6d7e6-134">**Q: There is a risk event in Identity Protection but I’m not seeing corresponding sign-in in hello all sign-ins. Is this expected?**</span></span>

<span data-ttu-id="6d7e6-135">**R :** Oui, Identity Protection évalue les risques pour tous les flux d’authentification, qu’ils soient interactifs ou non.</span><span class="sxs-lookup"><span data-stu-id="6d7e6-135">**A:** Yes, Identity Protection evaluates risk for all authentication flows whether if be interactive or non-interactive.</span></span> <span data-ttu-id="6d7e6-136">Toutefois, seul rapport de toutes les connexions affiche hello uniquement les connexions interactives.</span><span class="sxs-lookup"><span data-stu-id="6d7e6-136">However, all sign-ins only report shows only hello interactive sign-ins.</span></span>

---

<span data-ttu-id="6d7e6-137">**Q : Comment puis-je télécharger hello « Utilisateurs avec indicateur risque de » rapport dans le portail Azure ?**</span><span class="sxs-lookup"><span data-stu-id="6d7e6-137">**Q: How can I download hello “Users flagged for risk” report in Azure portal?**</span></span>

<span data-ttu-id="6d7e6-138">**R :** toodownload d’option hello *utilisateurs marqués pour risque* rapport est bientôt.</span><span class="sxs-lookup"><span data-stu-id="6d7e6-138">**A:** hello option toodownload *Users flagged for risk* report will be added soon.</span></span>

---

<span data-ttu-id="6d7e6-139">**Q : Comment puis-je savoir pourquoi une connexion ou un utilisateur a été signalé risquée Bonjour portail Azure ?**</span><span class="sxs-lookup"><span data-stu-id="6d7e6-139">**Q: How do I know why a sign-in or a user was flagged risky in hello Azure portal?**</span></span>

<span data-ttu-id="6d7e6-140">**R :** clients d’édition Premium en savoir plus sur hello sous-jacent risque en cliquant sur utilisateur hello dans « Utilisateurs avec indicateur risque » ou en cliquant sur hello « Risquées connexions ».</span><span class="sxs-lookup"><span data-stu-id="6d7e6-140">**A:** Premium edition customers can learn more about hello underlying risk events by clicking on hello user in “Users flagged for risk” or by clicking on hello “Risky sign-ins”.</span></span> <span data-ttu-id="6d7e6-141">Clients de l’édition gratuite et de base obtenir les utilisateurs à risque de toosee hello et les connexions sans hello sous-jacente des informations sur les événements de risque.</span><span class="sxs-lookup"><span data-stu-id="6d7e6-141">Free and Basic edition customers get toosee hello at-risk users and sign-ins without hello underlying risk event information.</span></span>

---

<span data-ttu-id="6d7e6-142">**Q : comment les adresses IP sont calculées dans les connexions hello et rapport de connexions risquée ??**</span><span class="sxs-lookup"><span data-stu-id="6d7e6-142">**Q: How are IP addresses calculated in hello sign-ins and risky sign-ins report??**</span></span>

<span data-ttu-id="6d7e6-143">**R :** les adresses IP sont émises de manière à ce qu’il n’existe aucune connexion définitive entre une adresse IP et où se trouve physiquement ordinateur hello avec cette adresse.</span><span class="sxs-lookup"><span data-stu-id="6d7e6-143">**A:** IP addresses are issued in such a way that there is no definitive connection between an IP address and where hello computer with that address is physically located.</span></span> <span data-ttu-id="6d7e6-144">Ceci est compliqué par des facteurs tels que les fournisseurs mobiles et VPN à émettre des adresses IP à partir de pools centrales souvent très éloignés où DISPOSITIF hello est utilisé.</span><span class="sxs-lookup"><span data-stu-id="6d7e6-144">This is complicated by factors such as mobile providers and VPNs issuing IP addresses from central pools often very far from where hello client device is actually used.</span></span> <span data-ttu-id="6d7e6-145">Hello ci-dessus, la conversion d’emplacement physique des tooa adresse IP est un meilleur effort basé sur des traces, les données du Registre, les recherches inversées et d’autres informations.</span><span class="sxs-lookup"><span data-stu-id="6d7e6-145">Given hello above, converting IP address tooa physical location is a best effort based on traces, registry data, reverse look ups and other information.</span></span> 

---
