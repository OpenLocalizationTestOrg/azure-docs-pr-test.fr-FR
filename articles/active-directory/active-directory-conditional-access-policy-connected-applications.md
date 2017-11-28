---
title: "stratégies d’accès conditionnel périphérique Azure Active Directory aaaConfigure | Documents Microsoft"
description: "Découvrez comment stratégies d’accès conditionnel de périphérique Azure Active Directory tooconfigure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a27862a6-d513-43ba-97c1-1c0d400bf243
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc5923b8ccee4335442c17ef63b2ee6f098e104e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a><span data-ttu-id="dc2a2-103">Configurer les stratégies d’accès conditionnel basé sur les appareils dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc2a2-103">Configure Azure Active Directory device-based conditional access policies</span></span>

<span data-ttu-id="dc2a2-104">Avec l’[accès conditionnel Azure Active Directory (Azure AD)](active-directory-conditional-access-azure-portal.md), vous pouvez préciser les méthodes d’accès des utilisateurs autorisés aux ressources.</span><span class="sxs-lookup"><span data-stu-id="dc2a2-104">With [Azure Active Directory (Azure AD) conditional access](active-directory-conditional-access-azure-portal.md), you can fine-tune how authorized users can access your resources.</span></span> <span data-ttu-id="dc2a2-105">Par exemple, vous limitez hello aux toocertain ressources tootrusted appareils.</span><span class="sxs-lookup"><span data-stu-id="dc2a2-105">For example, you limit hello access toocertain resources tootrusted devices.</span></span> <span data-ttu-id="dc2a2-106">Une stratégie d’accès conditionnel qui requiert un appareil de confiance est aussi appelée stratégie d’accès conditionnel basé sur les appareils.</span><span class="sxs-lookup"><span data-stu-id="dc2a2-106">A conditional access policy that requires a trusted device is also known as device-based conditional access policy.</span></span>

<span data-ttu-id="dc2a2-107">Cette rubrique fournit des informations sur comment stratégies pour les applications Azure AD connectés d’accès conditionnel basé sur le périphérique de tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="dc2a2-107">This topic provides you with information on how tooconfigure device-based conditional access policies for Azure AD-connected applications.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="dc2a2-108">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="dc2a2-108">Before you begin</span></span>

<span data-ttu-id="dc2a2-109">L’accès conditionnel basé sur les appareils fait le lien entre l’**accès conditionnel Azure AD** et la **gestion des appareils Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="dc2a2-109">Device-based conditional access ties **Azure AD conditional access** and **Azure AD device management together**.</span></span> <span data-ttu-id="dc2a2-110">Si vous n’êtes pas familiarisé avec une de ces zones, vous devez lire hello suivant rubriques, tout d’abord :</span><span class="sxs-lookup"><span data-stu-id="dc2a2-110">If you are not familiar with one of these areas yet, you should read hello following topics, first:</span></span>

- <span data-ttu-id="dc2a2-111">**[Accès conditionnel dans Azure Active Directory](active-directory-conditional-access-azure-portal.md)**  -cette rubrique fournit d’une vue d’ensemble conceptuelle de la condition d’accès et hello la terminologie associée.</span><span class="sxs-lookup"><span data-stu-id="dc2a2-111">**[Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)** - This topic provides you with a conceptual overview of conditional access and hello related terminology.</span></span>

- <span data-ttu-id="dc2a2-112">**[Gestion de toodevice introduction dans Azure Active Directory](device-management-introduction.md)**  -cette rubrique fournit une vue d’ensemble de hello différentes options vous disposez de périphériques tooconnect avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc2a2-112">**[Introduction toodevice management in Azure Active Directory](device-management-introduction.md)** - This topic gives you an overview of hello various options you have tooconnect devices with Azure AD.</span></span> 


## <a name="trusted-devices"></a><span data-ttu-id="dc2a2-113">Appareils de confiance</span><span class="sxs-lookup"><span data-stu-id="dc2a2-113">Trusted devices</span></span>

<span data-ttu-id="dc2a2-114">Dans un monde mobile en premier, privilégie le cloud, Azure Active Directory permet toodevices de l’authentification unique, les applications et services à partir de n’importe quel endroit.</span><span class="sxs-lookup"><span data-stu-id="dc2a2-114">In a mobile-first, cloud-first world, Azure Active Directory enables single sign-on toodevices, apps, and services from anywhere.</span></span> <span data-ttu-id="dc2a2-115">Pour certaines ressources dans votre environnement, accorder l’accès aux utilisateurs de droite toohello peut-être pas suffisant.</span><span class="sxs-lookup"><span data-stu-id="dc2a2-115">For certain resources in your environment, granting access toohello right users might not be good enough.</span></span> <span data-ttu-id="dc2a2-116">En outre toohello des utilisateurs appropriés, vous pouvez également nécessiter qu'un toobe appareil de confiance utilisé tooaccess une ressource.</span><span class="sxs-lookup"><span data-stu-id="dc2a2-116">In addition toohello right users, you might also require a trusted device toobe used tooaccess a resource.</span></span> <span data-ttu-id="dc2a2-117">Dans votre environnement, vous pouvez définir un appareil de confiance qui est basé sur hello suivants des composants :</span><span class="sxs-lookup"><span data-stu-id="dc2a2-117">In your environment, you can define what a trusted device is based on hello following components:</span></span>

- <span data-ttu-id="dc2a2-118">Hello [plateformes d’appareils](active-directory-conditional-access-azure-portal.md#device-platforms) sur un appareil</span><span class="sxs-lookup"><span data-stu-id="dc2a2-118">hello [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) on a device</span></span>
- <span data-ttu-id="dc2a2-119">Si un appareil est conforme ou non</span><span class="sxs-lookup"><span data-stu-id="dc2a2-119">Whether a device is compliant</span></span>
- <span data-ttu-id="dc2a2-120">Si un appareil est joint à un domaine</span><span class="sxs-lookup"><span data-stu-id="dc2a2-120">Whether a device is domain-joined</span></span> 

<span data-ttu-id="dc2a2-121">Hello [plateformes d’appareils](active-directory-conditional-access-azure-portal.md#device-platforms) se caractérise par le système d’exploitation hello qui s’exécute sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="dc2a2-121">hello [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) is characterized by hello operating system that is running on your device.</span></span> <span data-ttu-id="dc2a2-122">Dans votre stratégie d’accès conditionnel basés sur un appareil, vous pouvez limiter l’accès toocertain ressources toospecific des plateformes d’appareils.</span><span class="sxs-lookup"><span data-stu-id="dc2a2-122">In your device-based conditional access policy, you can limit access toocertain resources toospecific device platforms.</span></span>



<span data-ttu-id="dc2a2-123">Dans une stratégie d’accès conditionnel basés sur un appareil, vous pouvez exiger toobe appareils de confiance marqué comme conforme.</span><span class="sxs-lookup"><span data-stu-id="dc2a2-123">In a device-based conditional access policy, you can require trusted devices toobe marked as compliant.</span></span>

![Applications cloud](./media/active-directory-conditional-access-policy-connected-applications/24.png)

<span data-ttu-id="dc2a2-125">Les appareils peuvent être marqués comme conformes dans le répertoire hello par :</span><span class="sxs-lookup"><span data-stu-id="dc2a2-125">Devices can be marked as compliant in hello directory by:</span></span>

- <span data-ttu-id="dc2a2-126">Intune</span><span class="sxs-lookup"><span data-stu-id="dc2a2-126">Intune</span></span> 
- <span data-ttu-id="dc2a2-127">Un système de gestion de périphériques mobile tiers qui s’intègre avec Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc2a2-127">A third-party mobile device management system that integrates with Azure AD</span></span>  

<span data-ttu-id="dc2a2-128">Seuls les appareils qui sont connecté tooAzure AD peuvent être marqués comme conformes.</span><span class="sxs-lookup"><span data-stu-id="dc2a2-128">Only devices that are connected tooAzure AD can be marked as compliant.</span></span> <span data-ttu-id="dc2a2-129">tooconnect un tooAzure périphérique Active Directory, vous avez hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="dc2a2-129">tooconnect a device tooAzure Active Directory, you have hello following options:</span></span> 

- <span data-ttu-id="dc2a2-130">Appareils inscrits sur Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc2a2-130">Azure AD registered</span></span>
- <span data-ttu-id="dc2a2-131">Appareil joints Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc2a2-131">Azure AD joined</span></span>
- <span data-ttu-id="dc2a2-132">Appareils joints Azure AD hybrides</span><span class="sxs-lookup"><span data-stu-id="dc2a2-132">Hybrid Azure AD joined</span></span>

    ![Applications cloud](./media/active-directory-conditional-access-policy-connected-applications/26.png)

<span data-ttu-id="dc2a2-134">Si vous avez un encombrement de Active Directory (AD) local, vous pouvez envisager d’appareils qui ne sont pas connecté tooAzure AD mais toobe tooyour jointes AD approuvé.</span><span class="sxs-lookup"><span data-stu-id="dc2a2-134">If you have an on-premises Active Directory (AD) footprint, you might consider devices that are not connected tooAzure AD but joined tooyour AD toobe trusted.</span></span>

![Applications cloud](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a><span data-ttu-id="dc2a2-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dc2a2-136">Next steps</span></span>

<span data-ttu-id="dc2a2-137">Avant de configurer une stratégie d’accès conditionnel basés sur l’appareil dans votre environnement, vous devez examiner hello [meilleures pratiques pour l’accès conditionnel dans Azure Active Directory](active-directory-conditional-access-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="dc2a2-137">Before configuring a device-based conditional access policy in your environment, you should take a look at hello [best practices for conditional access in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span></span>

