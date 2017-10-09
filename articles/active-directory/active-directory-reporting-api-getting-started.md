---
title: "aaaGetting a démarré avec l’API de création de rapports hello Azure AD sur le portail classique hello Azure AD | Documents Microsoft"
description: Comment tooget main hello rapport API Azure Active Directory
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/18/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 52e22d442650731fc6ed28991fc65f9182af0540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-active-directory-reporting-api-on-hello-azure-ad-classic-portal"></a><span data-ttu-id="564a2-103">Prise en main de hello Azure Active Directory API de création de rapports sur le portail classique hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="564a2-103">Getting started with hello Azure Active Directory reporting API on hello Azure AD classic portal</span></span>
<span data-ttu-id="564a2-104">*Cette rubrique fait partie de hello [Guide Azure Active Directory Reporting](active-directory-reporting-guide.md).*</span><span class="sxs-lookup"><span data-stu-id="564a2-104">*This topic is part of hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="564a2-105">Azure Active Directory vous fournit plusieurs rapports.</span><span class="sxs-lookup"><span data-stu-id="564a2-105">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="564a2-106">données de Hello de ces rapports peuvent être très utile tooyour applications, telles que les systèmes SIEM, l’audit et les outils Business intelligence.</span><span class="sxs-lookup"><span data-stu-id="564a2-106">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="564a2-107">Bonjour Azure AD reporting Qu'api fournit des données de toohello de l’accès par programme via un ensemble d’API REST.</span><span class="sxs-lookup"><span data-stu-id="564a2-107">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="564a2-108">Vous pouvez appeler ces API à partir de divers outils et langages de programmation.</span><span class="sxs-lookup"><span data-stu-id="564a2-108">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="564a2-109">Cet article fournit des informations de hello vous devez tooget main hello Azure AD reporting API.</span><span class="sxs-lookup"><span data-stu-id="564a2-109">This article provides you with hello information you need tooget started with hello Azure AD reporting APIs.</span></span>
<span data-ttu-id="564a2-110">Dans la section suivante de hello, vous découvrez plus d’informations sur l’utilisation de hello d’audit et de connexion dans les API.</span><span class="sxs-lookup"><span data-stu-id="564a2-110">In hello next section, you find more details about using hello audit and sign-in APIs.</span></span> <span data-ttu-id="564a2-111">Pour toutes les autres API, consultez hello [les rapports Azure AD et events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) l’article.</span><span class="sxs-lookup"><span data-stu-id="564a2-111">For all other APIs, see hello [Azure AD reports and events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) article.</span></span>

<span data-ttu-id="564a2-112">Si vous avez des questions, des problèmes ou des commentaires, veuillez contacter [Aide à la création de rapports AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="564a2-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="learning-map"></a><span data-ttu-id="564a2-113">Carte d’apprentissage</span><span class="sxs-lookup"><span data-stu-id="564a2-113">Learning map</span></span>
1. <span data-ttu-id="564a2-114">**Préparer** -avant de pouvoir tester vos exemples d’API, vous devez toocomplete hello [API reporting de conditions préalables tooaccess hello Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="564a2-114">**Prepare** - Before you can test your API samples, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>
2. <span data-ttu-id="564a2-115">**Explorer** -obtenir une première impression de hello API de création de rapports :</span><span class="sxs-lookup"><span data-stu-id="564a2-115">**Explore** - Get a first impression of hello reporting APIs:</span></span>
   
   * [<span data-ttu-id="564a2-116">À l’aide des exemples de hello pour l’audit hello API</span><span class="sxs-lookup"><span data-stu-id="564a2-116">Using hello samples for hello audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="564a2-117">À l’aide des exemples de hello pour l’API de rapport d’activité de connexion hello</span><span class="sxs-lookup"><span data-stu-id="564a2-117">Using hello samples for hello sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="564a2-118">**Personnaliser** : créez votre propre solution :</span><span class="sxs-lookup"><span data-stu-id="564a2-118">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="564a2-119">À l’aide de la référence de l’API hello d’audit</span><span class="sxs-lookup"><span data-stu-id="564a2-119">Using hello audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="564a2-120">À l’aide de rapports d’activité de connexion hello font référence des API</span><span class="sxs-lookup"><span data-stu-id="564a2-120">Using hello sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="564a2-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="564a2-121">Next Steps</span></span>
<span data-ttu-id="564a2-122">Si vous êtes toosee obtenir des informations tous hello des points de terminaison API graphique Azure AD disponibles en naviguant trop[https://graph.windows.net/tenant-name/reports/$ métadonnées ? api-version = beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="564a2-122">If you are curious toosee all of hello available Azure AD Graph API endpoints by navigating too[https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span></span>

