---
title: "Bien démarrer avec l’accès conditionnel dans Azure Active Directory | Microsoft Docs"
description: "Testez l’accès conditionnel à l’aide d’une condition d’emplacement."
services: active-directory
keywords: "accès conditionnel aux applications, accès conditionnel à Azure AD, accès sécurisé aux ressources d’entreprise, stratégies d’accès conditionnel"
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
ms.openlocfilehash: cd53e8be32d1e98aaf9f72177895871dba69df86
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a><span data-ttu-id="c6569-104">Bien démarrer avec l’accès conditionnel dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c6569-104">Get started with conditional access in Azure Active Directory</span></span>

<span data-ttu-id="c6569-105">L’accès conditionnel est une fonctionnalité d’Azure Active Directory, qui vous permet de définir les conditions dans lesquelles les utilisateurs autorisés peuvent accéder à vos applications.</span><span class="sxs-lookup"><span data-stu-id="c6569-105">Conditional access is a capability of Azure Active Directory that enables you to define conditions under which authorized users can access your apps.</span></span> 

<span data-ttu-id="c6569-106">Cette rubrique fournit des instructions pour tester un accès conditionnel en fonction d’une condition d’emplacement dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="c6569-106">This topic provides you with instructions for testing a conditional access based on a location condition in your environment.</span></span>  


## <a name="scenario-description"></a><span data-ttu-id="c6569-107">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c6569-107">Scenario description</span></span>

<span data-ttu-id="c6569-108">De nombreuses organisations veulent limiter l’utilisation de l’authentification multifacteur aux tentatives d’accès aux applications, qui n’émanent pas de l’intranet de l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="c6569-108">One common requirement in many organizations is to only require multi-factor authentication for access to apps that is not performed from the corporate intranet.</span></span> <span data-ttu-id="c6569-109">Azure Active Directory vous permet d’atteindre cet objectif facilement grâce à une stratégie d’accès conditionnel basée sur l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="c6569-109">With Azure Active Directory, you can easily accomplish this goal by configuring a location-based conditional access policy.</span></span> <span data-ttu-id="c6569-110">Cette rubrique fournit des instructions détaillées pour configurer une stratégie de ce type.</span><span class="sxs-lookup"><span data-stu-id="c6569-110">This topic provides you with detailed instructions for configuring a related policy.</span></span> <span data-ttu-id="c6569-111">Celle-ci utilise des [adresses IP approuvées](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) pour faire la distinction entre les tentatives d’accès provenant de l’intranet de l’entreprise et celles provenant de tous les autres emplacements.</span><span class="sxs-lookup"><span data-stu-id="c6569-111">The policy leverages [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) to distinguish between access attempts made from the corporate's intranet and all other locations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="c6569-112">Prérequis</span><span class="sxs-lookup"><span data-stu-id="c6569-112">Prerequisites</span></span>

<span data-ttu-id="c6569-113">Le scénario décrit dans cette rubrique suppose que vous connaissiez les concepts abordés dans [Accès conditionnel Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c6569-113">The scenario outlined in this topic assumes that you are familiar with the concepts outlined in [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="c6569-114">Pour tester ce scénario, vous allez :</span><span class="sxs-lookup"><span data-stu-id="c6569-114">To test this scenario, you need to:</span></span>

- <span data-ttu-id="c6569-115">Créer un utilisateur de test</span><span class="sxs-lookup"><span data-stu-id="c6569-115">Create a test user</span></span> 

- <span data-ttu-id="c6569-116">Affecter une licence Azure AD Premium à cet utilisateur</span><span class="sxs-lookup"><span data-stu-id="c6569-116">Assign an Azure AD Premium license to the test user</span></span>

- <span data-ttu-id="c6569-117">Configurer une application gérée et lui affecter votre utilisateur de test</span><span class="sxs-lookup"><span data-stu-id="c6569-117">Configure a managed app and assign your test user to it</span></span>

- <span data-ttu-id="c6569-118">Configurer les adresses IP approuvées</span><span class="sxs-lookup"><span data-stu-id="c6569-118">Configure trusted IPs</span></span>

<span data-ttu-id="c6569-119">Pour plus d’informations sur les adresses IP approuvées, consultez [Adresses IP approuvées](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="c6569-119">If you need more details about Trusted IPs, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="policy-configuration-steps"></a><span data-ttu-id="c6569-120">Configuration de la stratégie</span><span class="sxs-lookup"><span data-stu-id="c6569-120">Policy configuration steps</span></span>

<span data-ttu-id="c6569-121">**Pour configurer votre stratégie d’accès conditionnel, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c6569-121">**To configure your conditional access policy, do:**</span></span>

1. <span data-ttu-id="c6569-122">Dans la barre de navigation gauche du portail Azure, cliquez sur **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c6569-122">In the Azure portal, on the left navbar, click **Azure Active Directory**.</span></span> 

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. <span data-ttu-id="c6569-124">Dans le panneau **Azure Active Directory**, sous la section **Gérer**, cliquez sur **Accès conditionnel**.</span><span class="sxs-lookup"><span data-stu-id="c6569-124">On the **Azure Active Directory** blade, in the **Manage** section, click **Conditional access**.</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. <span data-ttu-id="c6569-126">Dans le panneau **Accès conditionnel**, pour ouvrir le panneau **Nouveau**, cliquez sur **Ajouter** dans la barre d’outils située en haut.</span><span class="sxs-lookup"><span data-stu-id="c6569-126">On the **Conditional Access** blade, to open the **New** blade, in the toolbar on the top, click **Add**.</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. <span data-ttu-id="c6569-128">Dans le champ **Nom** du panneau **Nouveau**, indiquez le nom de votre stratégie.</span><span class="sxs-lookup"><span data-stu-id="c6569-128">On the **New** blade, in the **Name** textbox, type a name for your policy.</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. <span data-ttu-id="c6569-130">Dans la section **Affectation**, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c6569-130">In the **Assignment** section, click **Users and groups**.</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. <span data-ttu-id="c6569-132">Dans le panneau **Utilisateurs et groupes**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c6569-132">On the **Users and groups** blade, perform the following steps:</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    <span data-ttu-id="c6569-134">a.</span><span class="sxs-lookup"><span data-stu-id="c6569-134">a.</span></span> <span data-ttu-id="c6569-135">Cliquez sur **Sélectionner des utilisateurs et des groupes**.</span><span class="sxs-lookup"><span data-stu-id="c6569-135">Click **Select users and groups**.</span></span>

    <span data-ttu-id="c6569-136">b.</span><span class="sxs-lookup"><span data-stu-id="c6569-136">b.</span></span> <span data-ttu-id="c6569-137">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="c6569-137">Click **Select**.</span></span>

    <span data-ttu-id="c6569-138">c.</span><span class="sxs-lookup"><span data-stu-id="c6569-138">c.</span></span> <span data-ttu-id="c6569-139">Dans le panneau **Sélectionner**, sélectionnez votre utilisateur de test, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="c6569-139">On the **Select** blade, select your test user, and then click **Select**.</span></span>

    <span data-ttu-id="c6569-140">d.</span><span class="sxs-lookup"><span data-stu-id="c6569-140">d.</span></span> <span data-ttu-id="c6569-141">Dans le panneau **Utilisateurs et groupes**, cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="c6569-141">On the **Users and groups** blade, click **Done**.</span></span>

7. <span data-ttu-id="c6569-142">Dans le panneau **Nouveau**, pour ouvrir le panneau **Applications cloud**, cliquez sur **Applications cloud** dans la section **Affectation**.</span><span class="sxs-lookup"><span data-stu-id="c6569-142">On the **New** blade, to open the **Cloud apps** blade, in the **Assignment** section, click **Cloud apps**.</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. <span data-ttu-id="c6569-144">Dans le panneau **Applications cloud**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c6569-144">On the **Cloud apps** blade, perform the following steps:</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    <span data-ttu-id="c6569-146">a.</span><span class="sxs-lookup"><span data-stu-id="c6569-146">a.</span></span> <span data-ttu-id="c6569-147">Cliquez sur **Sélectionner les applications**.</span><span class="sxs-lookup"><span data-stu-id="c6569-147">Click **Select apps**.</span></span>

    <span data-ttu-id="c6569-148">b.</span><span class="sxs-lookup"><span data-stu-id="c6569-148">b.</span></span> <span data-ttu-id="c6569-149">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="c6569-149">Click **Select**.</span></span>

    <span data-ttu-id="c6569-150">c.</span><span class="sxs-lookup"><span data-stu-id="c6569-150">c.</span></span> <span data-ttu-id="c6569-151">Dans le panneau **Sélectionner**, sélectionnez votre application cloud, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="c6569-151">On the **Select** blade, select your cloud app, and then click **Select**.</span></span>

    <span data-ttu-id="c6569-152">d.</span><span class="sxs-lookup"><span data-stu-id="c6569-152">d.</span></span> <span data-ttu-id="c6569-153">Dans le panneau **Applications cloud**, cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="c6569-153">On the **Cloud apps** blade, click **Done**.</span></span>

9. <span data-ttu-id="c6569-154">Dans le panneau **Nouveau**, pour ouvrir le panneau **Conditions**, cliquez sur **Conditions** dans la section **Affectation**.</span><span class="sxs-lookup"><span data-stu-id="c6569-154">On the **New** blade, to open the **Conditions** blade, in the **Assignment** section, click **Conditions**.</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. <span data-ttu-id="c6569-156">Dans le panneau **Conditions**, pour ouvrir le panneau **Emplacements**, cliquez sur **Emplacements**.</span><span class="sxs-lookup"><span data-stu-id="c6569-156">On the **Conditions** blade, to open the **Locations** blade, click **Locations**.</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. <span data-ttu-id="c6569-158">Dans le panneau **Emplacements**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c6569-158">On the **Locations** blade, perform the following steps:</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    <span data-ttu-id="c6569-160">a.</span><span class="sxs-lookup"><span data-stu-id="c6569-160">a.</span></span> <span data-ttu-id="c6569-161">Sous **Configurer**, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="c6569-161">Under **Configure**, click **Yes**.</span></span>

    <span data-ttu-id="c6569-162">b.</span><span class="sxs-lookup"><span data-stu-id="c6569-162">b.</span></span> <span data-ttu-id="c6569-163">Sous **Inclure**, cliquez sur **All locations (Tous les emplacements)**.</span><span class="sxs-lookup"><span data-stu-id="c6569-163">Under **Include**, click **All locations**.</span></span>

    <span data-ttu-id="c6569-164">c.</span><span class="sxs-lookup"><span data-stu-id="c6569-164">c.</span></span> <span data-ttu-id="c6569-165">Cliquez sur **Exclure**, puis sur **All trusted IPs (Toutes les adresses IP approuvées)**.</span><span class="sxs-lookup"><span data-stu-id="c6569-165">Click **Exclude**, and then click **All trusted IPs**.</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    <span data-ttu-id="c6569-167">d.</span><span class="sxs-lookup"><span data-stu-id="c6569-167">d.</span></span> <span data-ttu-id="c6569-168">Cliquez sur **Done**.</span><span class="sxs-lookup"><span data-stu-id="c6569-168">Click **Done**.</span></span>

12. <span data-ttu-id="c6569-169">Dans le panneau **Conditions**, cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="c6569-169">On the **Conditions** blade, click **Done**.</span></span>

13. <span data-ttu-id="c6569-170">Dans le panneau **Nouveau**, pour ouvrir le panneau **Octroyer**, cliquez sur **Octroyer** dans la section **Contrôles**.</span><span class="sxs-lookup"><span data-stu-id="c6569-170">On the **New** blade, to open the **Grant** blade, in the **Controls** section, click **Grant**.</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. <span data-ttu-id="c6569-172">Dans le panneau **Grant (Autoriser)**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c6569-172">On the **Grant** blade, perform the following steps:</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    <span data-ttu-id="c6569-174">a.</span><span class="sxs-lookup"><span data-stu-id="c6569-174">a.</span></span> <span data-ttu-id="c6569-175">Sélectionnez **Exiger une authentification multifacteur**.</span><span class="sxs-lookup"><span data-stu-id="c6569-175">Select **Require multi-factor authentication**.</span></span>

    <span data-ttu-id="c6569-176">b.</span><span class="sxs-lookup"><span data-stu-id="c6569-176">b.</span></span> <span data-ttu-id="c6569-177">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="c6569-177">Click **Select**.</span></span>

15. <span data-ttu-id="c6569-178">Dans le panneau **Nouveau**, sous **Activer la stratégie**, cliquez sur **Activé**.</span><span class="sxs-lookup"><span data-stu-id="c6569-178">On the **New** blade, under **Enable policy**, click **On**.</span></span>

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. <span data-ttu-id="c6569-180">Dans le panneau **Nouveau**, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="c6569-180">On the **New** blade, click **Create**.</span></span>


## <a name="testing-the-policy"></a><span data-ttu-id="c6569-181">Test de la stratégie</span><span class="sxs-lookup"><span data-stu-id="c6569-181">Testing the policy</span></span>

<span data-ttu-id="c6569-182">Pour tester votre stratégie, vous devez accéder à votre application à partir d’un appareil :</span><span class="sxs-lookup"><span data-stu-id="c6569-182">To test your policy, you should access your app from a device that:</span></span> 

1. <span data-ttu-id="c6569-183">dont l’adresse IP figure parmi les adresses IP approuvées que vous avez configurées ;</span><span class="sxs-lookup"><span data-stu-id="c6569-183">Has an IP address that is within your configured Trusted IPs</span></span> 

1. <span data-ttu-id="c6569-184">dont l’adresse IP ne figure pas parmi les adresses IP approuvées que vous avez configurées.</span><span class="sxs-lookup"><span data-stu-id="c6569-184">Has an IP address that is not within your configured Trusted IPs</span></span>

<span data-ttu-id="c6569-185">L’authentification multifacteur ne doit être requise que si la tentative de connexion émane d’un appareil qui ne figure pas parmi les adresses IP approuvées que vous avez configurées.</span><span class="sxs-lookup"><span data-stu-id="c6569-185">Multi-factor authentication should only be required during a connection attempt that was made from a device that is not within your configured Trusted IPs.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="c6569-186">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c6569-186">Next steps</span></span>

<span data-ttu-id="c6569-187">Pour en savoir plus sur l’accès conditionnel, consultez [Accès conditionnel Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c6569-187">If you would like to learn more about conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

