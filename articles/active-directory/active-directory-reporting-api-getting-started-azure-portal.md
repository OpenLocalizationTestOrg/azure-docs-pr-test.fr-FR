---
title: "aaaGetting a démarré avec l’API de création de rapports hello Azure AD | Documents Microsoft"
description: Comment tooget main hello rapport API Azure Active Directory
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/18/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: bb7d72ba445daa367d7502889c38a605a16f26d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-active-directory-reporting-api"></a><span data-ttu-id="26f23-103">Prise en main de hello Azure Active Directory API de création de rapports</span><span class="sxs-lookup"><span data-stu-id="26f23-103">Getting started with hello Azure Active Directory reporting API</span></span>

<span data-ttu-id="26f23-104">Azure Active Directory vous fournit plusieurs rapports.</span><span class="sxs-lookup"><span data-stu-id="26f23-104">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="26f23-105">données de Hello de ces rapports peuvent être très utile tooyour applications, telles que les systèmes SIEM, l’audit et les outils Business intelligence.</span><span class="sxs-lookup"><span data-stu-id="26f23-105">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="26f23-106">Bonjour Azure AD reporting Qu'api fournit des données de toohello de l’accès par programme via un ensemble d’API REST.</span><span class="sxs-lookup"><span data-stu-id="26f23-106">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="26f23-107">Vous pouvez appeler ces API à partir de divers outils et langages de programmation.</span><span class="sxs-lookup"><span data-stu-id="26f23-107">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="26f23-108">Cet article fournit des informations de hello vous devez tooget main hello Azure AD reporting API.</span><span class="sxs-lookup"><span data-stu-id="26f23-108">This article provides you with hello information you need tooget started with hello Azure AD reporting APIs.</span></span>
<span data-ttu-id="26f23-109">Dans la section suivante de hello, vous découvrez plus d’informations sur l’utilisation de hello d’audit et de connexion dans les API.</span><span class="sxs-lookup"><span data-stu-id="26f23-109">In hello next section, you find more details about using hello audit and sign-in APIs.</span></span> 

<span data-ttu-id="26f23-110">Pour consulter les questions les plus fréquentes, lisez notre [FAQ](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span><span class="sxs-lookup"><span data-stu-id="26f23-110">For frequently asked questions,read our [FAQ](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span></span> <span data-ttu-id="26f23-111">En cas de problème, [Envoyez un ticket de support](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span><span class="sxs-lookup"><span data-stu-id="26f23-111">For issues, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span></span>

## <a name="learning-map"></a><span data-ttu-id="26f23-112">Carte d’apprentissage</span><span class="sxs-lookup"><span data-stu-id="26f23-112">Learning map</span></span>
1. <span data-ttu-id="26f23-113">**Préparer** -avant de pouvoir tester vos exemples d’API, vous devez toocomplete hello [API reporting de conditions préalables tooaccess hello Azure AD](active-directory-reporting-api-prerequisites-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="26f23-113">**Prepare** - Before you can test your API samples, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites-azure-portal.md).</span></span>
2. <span data-ttu-id="26f23-114">**Explorer** -obtenir une première impression de hello API de création de rapports :</span><span class="sxs-lookup"><span data-stu-id="26f23-114">**Explore** - Get a first impression of hello reporting APIs:</span></span>
   
   * [<span data-ttu-id="26f23-115">À l’aide des exemples de hello pour l’audit hello API</span><span class="sxs-lookup"><span data-stu-id="26f23-115">Using hello samples for hello audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="26f23-116">À l’aide des exemples de hello pour l’API de rapport d’activité de connexion hello</span><span class="sxs-lookup"><span data-stu-id="26f23-116">Using hello samples for hello sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="26f23-117">**Personnaliser** : créez votre propre solution :</span><span class="sxs-lookup"><span data-stu-id="26f23-117">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="26f23-118">À l’aide de la référence de l’API hello d’audit</span><span class="sxs-lookup"><span data-stu-id="26f23-118">Using hello audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="26f23-119">À l’aide de rapports d’activité de connexion hello font référence des API</span><span class="sxs-lookup"><span data-stu-id="26f23-119">Using hello sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="26f23-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="26f23-120">Next Steps</span></span>
<span data-ttu-id="26f23-121">Si vous êtes toosee obtenir des informations toutes les API Azure AD Graph points de terminaison disponibles, utilisez ce lien : [https://graph.windows.net/tenant-name/activities/$ métadonnées ? api-version = beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="26f23-121">If you are curious toosee all available Azure AD Graph API endpoints, use this link: [https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span></span>

