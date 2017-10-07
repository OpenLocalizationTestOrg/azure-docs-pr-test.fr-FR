---
title: "aaaGet a démarré avec un accès conditionnel dans Azure Active Directory | Documents Microsoft"
description: "Testez l’accès conditionnel à l’aide d’une condition d’emplacement."
services: active-directory
keywords: "tooapps d’accès conditionnel, l’accès conditionnel avec Azure AD, sécuriser l’accès aux ressources toocompany, les stratégies d’accès conditionnel"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4521f5a34f5882e026f5e58a7127d8c55cba2f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a><span data-ttu-id="385f7-104">Bien démarrer avec l’accès conditionnel dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="385f7-104">Get started with conditional access in Azure Active Directory</span></span>

<span data-ttu-id="385f7-105">Accès conditionnel est une fonctionnalité d’Azure Active Directory qui permet des conditions toodefine vous sous lequel les utilisateurs autorisés peuvent accéder à vos applications.</span><span class="sxs-lookup"><span data-stu-id="385f7-105">Conditional access is a capability of Azure Active Directory that enables you toodefine conditions under which authorized users can access your apps.</span></span> 

<span data-ttu-id="385f7-106">Cette rubrique fournit des instructions pour tester un accès conditionnel en fonction d’une condition d’emplacement dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="385f7-106">This topic provides you with instructions for testing a conditional access based on a location condition in your environment.</span></span>  


## <a name="scenario-description"></a><span data-ttu-id="385f7-107">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="385f7-107">Scenario description</span></span>

<span data-ttu-id="385f7-108">Une condition courante dans de nombreuses organisations est tooonly exiger l’authentification multifacteur pour tooapps d’accès qui n’est pas effectuée à partir de l’intranet d’entreprise de hello.</span><span class="sxs-lookup"><span data-stu-id="385f7-108">One common requirement in many organizations is tooonly require multi-factor authentication for access tooapps that is not performed from hello corporate intranet.</span></span> <span data-ttu-id="385f7-109">Azure Active Directory vous permet d’atteindre cet objectif facilement grâce à une stratégie d’accès conditionnel basée sur l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="385f7-109">With Azure Active Directory, you can easily accomplish this goal by configuring a location-based conditional access policy.</span></span> <span data-ttu-id="385f7-110">Cette rubrique fournit des instructions détaillées pour configurer une stratégie de ce type.</span><span class="sxs-lookup"><span data-stu-id="385f7-110">This topic provides you with detailed instructions for configuring a related policy.</span></span> <span data-ttu-id="385f7-111">Hello tire parti de la stratégie [des adresses IP approuvées](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish entre les tentatives d’accès effectuées à partir de hello d’entreprise de l’intranet et tous les autres emplacements.</span><span class="sxs-lookup"><span data-stu-id="385f7-111">hello policy leverages [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish between access attempts made from hello corporate's intranet and all other locations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="385f7-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="385f7-112">Prerequisites</span></span>

<span data-ttu-id="385f7-113">Hello scénario décrit dans cette rubrique part du principe que vous êtes familiarisé avec les concepts de hello décrites dans [accès conditionnel Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="385f7-113">hello scenario outlined in this topic assumes that you are familiar with hello concepts outlined in [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="385f7-114">tootest ce scénario, vous devez :</span><span class="sxs-lookup"><span data-stu-id="385f7-114">tootest this scenario, you need to:</span></span>

- <span data-ttu-id="385f7-115">Créer un utilisateur de test</span><span class="sxs-lookup"><span data-stu-id="385f7-115">Create a test user</span></span> 

- <span data-ttu-id="385f7-116">Attribuer un utilisateur de test de toohello licence Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="385f7-116">Assign an Azure AD Premium license toohello test user</span></span>

- <span data-ttu-id="385f7-117">Configurer une application gérée et affecter votre tooit d’utilisateur de test</span><span class="sxs-lookup"><span data-stu-id="385f7-117">Configure a managed app and assign your test user tooit</span></span>

- <span data-ttu-id="385f7-118">Configurer les adresses IP approuvées</span><span class="sxs-lookup"><span data-stu-id="385f7-118">Configure trusted IPs</span></span>

<span data-ttu-id="385f7-119">Pour plus d’informations sur les adresses IP approuvées, consultez [Adresses IP approuvées](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="385f7-119">If you need more details about Trusted IPs, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="policy-configuration-steps"></a><span data-ttu-id="385f7-120">Configuration de la stratégie</span><span class="sxs-lookup"><span data-stu-id="385f7-120">Policy configuration steps</span></span>

<span data-ttu-id="385f7-121">**tooconfigure votre stratégie d’accès conditionnel, faire :**</span><span class="sxs-lookup"><span data-stu-id="385f7-121">**tooconfigure your conditional access policy, do:**</span></span>

1. <span data-ttu-id="385f7-122">Bonjour portail Azure, sur hello barre de navigation gauche, cliquez sur **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="385f7-122">In hello Azure portal, on hello left navbar, click **Azure Active Directory**.</span></span> 

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. <span data-ttu-id="385f7-124">Sur hello **Azure Active Directory** panneau, Bonjour **gérer** , cliquez sur **accès conditionnel**.</span><span class="sxs-lookup"><span data-stu-id="385f7-124">On hello **Azure Active Directory** blade, in hello **Manage** section, click **Conditional access**.</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. <span data-ttu-id="385f7-126">Sur hello **accès conditionnel** panneau, tooopen hello **nouveau** lame, dans la barre d’outils hello en haut de hello, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="385f7-126">On hello **Conditional Access** blade, tooopen hello **New** blade, in hello toolbar on hello top, click **Add**.</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. <span data-ttu-id="385f7-128">Sur hello **nouveau** panneau, Bonjour **nom** zone de texte, tapez un nom pour votre stratégie.</span><span class="sxs-lookup"><span data-stu-id="385f7-128">On hello **New** blade, in hello **Name** textbox, type a name for your policy.</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. <span data-ttu-id="385f7-130">Bonjour **affectation** , cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="385f7-130">In hello **Assignment** section, click **Users and groups**.</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. <span data-ttu-id="385f7-132">Sur hello **utilisateurs et groupes** panneau, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="385f7-132">On hello **Users and groups** blade, perform hello following steps:</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    <span data-ttu-id="385f7-134">a.</span><span class="sxs-lookup"><span data-stu-id="385f7-134">a.</span></span> <span data-ttu-id="385f7-135">Cliquez sur **Sélectionner des utilisateurs et des groupes**.</span><span class="sxs-lookup"><span data-stu-id="385f7-135">Click **Select users and groups**.</span></span>

    <span data-ttu-id="385f7-136">b.</span><span class="sxs-lookup"><span data-stu-id="385f7-136">b.</span></span> <span data-ttu-id="385f7-137">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="385f7-137">Click **Select**.</span></span>

    <span data-ttu-id="385f7-138">c.</span><span class="sxs-lookup"><span data-stu-id="385f7-138">c.</span></span> <span data-ttu-id="385f7-139">Sur hello **sélectionnez** panneau, sélectionnez votre utilisateur test, puis cliquez sur **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="385f7-139">On hello **Select** blade, select your test user, and then click **Select**.</span></span>

    <span data-ttu-id="385f7-140">d.</span><span class="sxs-lookup"><span data-stu-id="385f7-140">d.</span></span> <span data-ttu-id="385f7-141">Sur hello **utilisateurs et groupes** panneau, cliquez sur **fait**.</span><span class="sxs-lookup"><span data-stu-id="385f7-141">On hello **Users and groups** blade, click **Done**.</span></span>

7. <span data-ttu-id="385f7-142">Sur hello **nouveau** panneau, tooopen hello **applications Cloud** panneau, Bonjour **affectation** , cliquez sur **applications Cloud**.</span><span class="sxs-lookup"><span data-stu-id="385f7-142">On hello **New** blade, tooopen hello **Cloud apps** blade, in hello **Assignment** section, click **Cloud apps**.</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. <span data-ttu-id="385f7-144">Sur hello **applications Cloud** panneau, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="385f7-144">On hello **Cloud apps** blade, perform hello following steps:</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    <span data-ttu-id="385f7-146">a.</span><span class="sxs-lookup"><span data-stu-id="385f7-146">a.</span></span> <span data-ttu-id="385f7-147">Cliquez sur **Sélectionner les applications**.</span><span class="sxs-lookup"><span data-stu-id="385f7-147">Click **Select apps**.</span></span>

    <span data-ttu-id="385f7-148">b.</span><span class="sxs-lookup"><span data-stu-id="385f7-148">b.</span></span> <span data-ttu-id="385f7-149">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="385f7-149">Click **Select**.</span></span>

    <span data-ttu-id="385f7-150">c.</span><span class="sxs-lookup"><span data-stu-id="385f7-150">c.</span></span> <span data-ttu-id="385f7-151">Sur hello **sélectionnez** panneau, sélectionnez votre application cloud, puis cliquez sur **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="385f7-151">On hello **Select** blade, select your cloud app, and then click **Select**.</span></span>

    <span data-ttu-id="385f7-152">d.</span><span class="sxs-lookup"><span data-stu-id="385f7-152">d.</span></span> <span data-ttu-id="385f7-153">Sur hello **applications Cloud** panneau, cliquez sur **fait**.</span><span class="sxs-lookup"><span data-stu-id="385f7-153">On hello **Cloud apps** blade, click **Done**.</span></span>

9. <span data-ttu-id="385f7-154">Sur hello **nouveau** panneau, tooopen hello **Conditions** panneau, Bonjour **affectation** , cliquez sur **Conditions**.</span><span class="sxs-lookup"><span data-stu-id="385f7-154">On hello **New** blade, tooopen hello **Conditions** blade, in hello **Assignment** section, click **Conditions**.</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. <span data-ttu-id="385f7-156">Sur hello **Conditions** panneau, tooopen hello **emplacements** panneau, cliquez sur **emplacements**.</span><span class="sxs-lookup"><span data-stu-id="385f7-156">On hello **Conditions** blade, tooopen hello **Locations** blade, click **Locations**.</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. <span data-ttu-id="385f7-158">Sur hello **emplacements** panneau, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="385f7-158">On hello **Locations** blade, perform hello following steps:</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    <span data-ttu-id="385f7-160">a.</span><span class="sxs-lookup"><span data-stu-id="385f7-160">a.</span></span> <span data-ttu-id="385f7-161">Sous **Configurer**, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="385f7-161">Under **Configure**, click **Yes**.</span></span>

    <span data-ttu-id="385f7-162">b.</span><span class="sxs-lookup"><span data-stu-id="385f7-162">b.</span></span> <span data-ttu-id="385f7-163">Sous **Inclure**, cliquez sur **All locations (Tous les emplacements)**.</span><span class="sxs-lookup"><span data-stu-id="385f7-163">Under **Include**, click **All locations**.</span></span>

    <span data-ttu-id="385f7-164">c.</span><span class="sxs-lookup"><span data-stu-id="385f7-164">c.</span></span> <span data-ttu-id="385f7-165">Cliquez sur **Exclure**, puis sur **All trusted IPs (Toutes les adresses IP approuvées)**.</span><span class="sxs-lookup"><span data-stu-id="385f7-165">Click **Exclude**, and then click **All trusted IPs**.</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    <span data-ttu-id="385f7-167">d.</span><span class="sxs-lookup"><span data-stu-id="385f7-167">d.</span></span> <span data-ttu-id="385f7-168">Cliquez sur **Done**.</span><span class="sxs-lookup"><span data-stu-id="385f7-168">Click **Done**.</span></span>

12. <span data-ttu-id="385f7-169">Sur hello **Conditions** panneau, cliquez sur **fait**.</span><span class="sxs-lookup"><span data-stu-id="385f7-169">On hello **Conditions** blade, click **Done**.</span></span>

13. <span data-ttu-id="385f7-170">Sur hello **nouveau** panneau, tooopen hello **Grant** panneau, Bonjour **contrôles** , cliquez sur **Grant**.</span><span class="sxs-lookup"><span data-stu-id="385f7-170">On hello **New** blade, tooopen hello **Grant** blade, in hello **Controls** section, click **Grant**.</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. <span data-ttu-id="385f7-172">Sur hello **Grant** panneau, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="385f7-172">On hello **Grant** blade, perform hello following steps:</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    <span data-ttu-id="385f7-174">a.</span><span class="sxs-lookup"><span data-stu-id="385f7-174">a.</span></span> <span data-ttu-id="385f7-175">Sélectionnez **Exiger une authentification multifacteur**.</span><span class="sxs-lookup"><span data-stu-id="385f7-175">Select **Require multi-factor authentication**.</span></span>

    <span data-ttu-id="385f7-176">b.</span><span class="sxs-lookup"><span data-stu-id="385f7-176">b.</span></span> <span data-ttu-id="385f7-177">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="385f7-177">Click **Select**.</span></span>

15. <span data-ttu-id="385f7-178">Sur hello **nouveau** panneau, sous **activer la stratégie**, cliquez sur **sur**.</span><span class="sxs-lookup"><span data-stu-id="385f7-178">On hello **New** blade, under **Enable policy**, click **On**.</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. <span data-ttu-id="385f7-180">Sur hello **nouveau** panneau, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="385f7-180">On hello **New** blade, click **Create**.</span></span>


## <a name="testing-hello-policy"></a><span data-ttu-id="385f7-181">Test de la stratégie de hello</span><span class="sxs-lookup"><span data-stu-id="385f7-181">Testing hello policy</span></span>

<span data-ttu-id="385f7-182">tootest votre stratégie, vous devez accéder à votre application à partir d’un appareil qui :</span><span class="sxs-lookup"><span data-stu-id="385f7-182">tootest your policy, you should access your app from a device that:</span></span> 

1. <span data-ttu-id="385f7-183">dont l’adresse IP figure parmi les adresses IP approuvées que vous avez configurées ;</span><span class="sxs-lookup"><span data-stu-id="385f7-183">Has an IP address that is within your configured Trusted IPs</span></span> 

1. <span data-ttu-id="385f7-184">dont l’adresse IP ne figure pas parmi les adresses IP approuvées que vous avez configurées.</span><span class="sxs-lookup"><span data-stu-id="385f7-184">Has an IP address that is not within your configured Trusted IPs</span></span>

<span data-ttu-id="385f7-185">L’authentification multifacteur ne doit être requise que si la tentative de connexion émane d’un appareil qui ne figure pas parmi les adresses IP approuvées que vous avez configurées.</span><span class="sxs-lookup"><span data-stu-id="385f7-185">Multi-factor authentication should only be required during a connection attempt that was made from a device that is not within your configured Trusted IPs.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="385f7-186">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="385f7-186">Next steps</span></span>

<span data-ttu-id="385f7-187">Si vous souhaitez que toolearn plus d’informations sur l’accès conditionnel, consultez [accès conditionnel Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="385f7-187">If you would like toolearn more about conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

