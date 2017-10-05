---
title: "Didacticiel : Intégration d’Azure Active Directory à TimeOffManager | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et TimeOffManager."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 3f944ffbf704694b293b4b1e5bdb4f2c93ae35a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a><span data-ttu-id="f0d1e-103">Didacticiel : Intégration d’Azure AD à TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="f0d1e-103">Tutorial: Azure Active Directory integration with TimeOffManager</span></span>

<span data-ttu-id="f0d1e-104">Dans ce didacticiel, vous allez apprendre à intégrer TimeOffManager dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f0d1e-104">In this tutorial, you learn how to integrate TimeOffManager with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f0d1e-105">L’intégration de TimeOffManager dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="f0d1e-105">Integrating TimeOffManager with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f0d1e-106">Dans Azure AD, vous pouvez contrôler qui a accès à TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="f0d1e-106">You can control in Azure AD who has access to TimeOffManager</span></span>
- <span data-ttu-id="f0d1e-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à TimeOffManager (par le biais de l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0d1e-107">You can enable your users to automatically get signed-on to TimeOffManager (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f0d1e-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="f0d1e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f0d1e-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f0d1e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0d1e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f0d1e-110">Prerequisites</span></span>

<span data-ttu-id="f0d1e-111">Pour configurer l’intégration d’Azure AD dans TimeOffManager, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f0d1e-111">To configure Azure AD integration with TimeOffManager, you need the following items:</span></span>

- <span data-ttu-id="f0d1e-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0d1e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f0d1e-113">Un abonnement TimeOffManager pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="f0d1e-113">A TimeOffManager single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f0d1e-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f0d1e-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f0d1e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f0d1e-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f0d1e-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f0d1e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f0d1e-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="f0d1e-118">Scenario description</span></span>
<span data-ttu-id="f0d1e-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f0d1e-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="f0d1e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f0d1e-121">Ajouter TimeOffManager à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="f0d1e-121">Add TimeOffManager from the gallery</span></span>
2. <span data-ttu-id="f0d1e-122">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0d1e-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-timeoffmanager-from-the-gallery"></a><span data-ttu-id="f0d1e-123">Ajouter TimeOffManager à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="f0d1e-123">Add TimeOffManager from the gallery</span></span>
<span data-ttu-id="f0d1e-124">Pour configurer l’intégration de TimeOffManager avec Azure AD, vous devez ajouter TimeOffManager, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-124">To configure the integration of TimeOffManager into Azure AD, you need to add TimeOffManager from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f0d1e-125">**Pour ajouter TimeOffManager à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f0d1e-125">**To add TimeOffManager from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f0d1e-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f0d1e-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f0d1e-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="f0d1e-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="f0d1e-133">Dans la zone de recherche, tapez **TimeOffManager**, sélectionnez **TimeOffManager** dans le panneau de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-133">In the search box, type **TimeOffManager**, select **TimeOffManager** from result panel and then click **Add** button to add the application.</span></span>

    ![Ajouter à partir de la galerie](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f0d1e-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0d1e-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="f0d1e-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec TimeOffManager, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="f0d1e-136">In this section, you configure and test Azure AD single sign-on with TimeOffManager based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f0d1e-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur TimeOffManager équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TimeOffManager is to a user in Azure AD.</span></span> <span data-ttu-id="f0d1e-138">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur TimeOffManager associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-138">In other words, a link relationship between an Azure AD user and the related user in TimeOffManager needs to be established.</span></span>

<span data-ttu-id="f0d1e-139">Dans TimeOffManager, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-139">In TimeOffManager, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f0d1e-140">Pour configurer et tester l’authentification unique Azure AD avec TimeOffManager, vous devez vous conformer aux indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="f0d1e-140">To configure and test Azure AD single sign-on with TimeOffManager, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f0d1e-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f0d1e-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f0d1e-143">**[Créer un utilisateur de test TimeOffManager](#create-a-timeoffmanager-test-user)** pour avoir un équivalent de Britta Simon dans TimeOffManager lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-143">**[Create a TimeOffManager test user](#create-a-timeoffmanager-test-user)** - to have a counterpart of Britta Simon in TimeOffManager that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f0d1e-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f0d1e-145">**[Tester l’authentification unique](#test-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f0d1e-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0d1e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f0d1e-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TimeOffManager application.</span></span>

<span data-ttu-id="f0d1e-148">**Pour configurer l’authentification unique Azure AD avec TimeOffManager, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f0d1e-148">**To configure Azure AD single sign-on with TimeOffManager, perform the following steps:**</span></span>

1. <span data-ttu-id="f0d1e-149">Dans le portail Azure, sur la page d’intégration de l’application **TimeOffManager**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-149">In the Azure portal, on the **TimeOffManager** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="f0d1e-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Authentification basée sur SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. <span data-ttu-id="f0d1e-153">Dans la section **Domaine et URL TimeOffManager**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f0d1e-153">On the **TimeOffManager Domain and URLs** section, perform the following:</span></span>

     ![Section Domaine et URL TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    <span data-ttu-id="f0d1e-155">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span><span class="sxs-lookup"><span data-stu-id="f0d1e-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f0d1e-156">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-156">This value is not real.</span></span> <span data-ttu-id="f0d1e-157">Mettez à jour la valeur avec l’URL de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-157">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="f0d1e-158">Vous pouvez obtenir cette valeur à partir de la **page des paramètres d’authentification unique**, décrite plus loin dans le didacticiel, ou contacter l’[équipe de support technique TimeOffManager](http://www.timeoffmanager.com/contact-us.aspx).</span><span class="sxs-lookup"><span data-stu-id="f0d1e-158">You can get this value from **Single Sign on settings page** which is explained later in the tutorial or Contact [TimeOffManager support team](http://www.timeoffmanager.com/contact-us.aspx).</span></span>
 
4. <span data-ttu-id="f0d1e-159">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Section Certificat de signature SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. <span data-ttu-id="f0d1e-161">Cette section explique comment permettre aux utilisateurs de s’authentifier sur TimeOffManager avec leur compte Azure AD en utilisant la fédération basée sur le protocole SAML.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-161">The objective of this section is to outline how to enable users to authenticate to TimeOffManger with their account in Azure AD using federation based on the SAML protocol.</span></span>
    
    <span data-ttu-id="f0d1e-162">Votre application TimeOffManager s’attend à recevoir les assertions SAML dans un format spécifique, ce qui vous oblige à ajouter des mappages d’attributs personnalisés à votre configuration des attributs du jeton SAML.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-162">Your TimeOffManger application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="f0d1e-163">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="f0d1e-163">The following screenshot shows an example for this.</span></span>

    <span data-ttu-id="f0d1e-164">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml token attributes")</span><span class="sxs-lookup"><span data-stu-id="f0d1e-164">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml token attributes")</span></span>
    
    | <span data-ttu-id="f0d1e-165">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="f0d1e-165">Attribute Name</span></span> | <span data-ttu-id="f0d1e-166">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="f0d1e-166">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="f0d1e-167">Firstname</span><span class="sxs-lookup"><span data-stu-id="f0d1e-167">Firstname</span></span> |<span data-ttu-id="f0d1e-168">User.givenname</span><span class="sxs-lookup"><span data-stu-id="f0d1e-168">User.givenname</span></span> |
    | <span data-ttu-id="f0d1e-169">Lastname</span><span class="sxs-lookup"><span data-stu-id="f0d1e-169">Lastname</span></span> |<span data-ttu-id="f0d1e-170">User.Surname</span><span class="sxs-lookup"><span data-stu-id="f0d1e-170">User.surname</span></span> |
    | <span data-ttu-id="f0d1e-171">Email</span><span class="sxs-lookup"><span data-stu-id="f0d1e-171">Email</span></span> |<span data-ttu-id="f0d1e-172">User.mail</span><span class="sxs-lookup"><span data-stu-id="f0d1e-172">User.mail</span></span> |
    
    <span data-ttu-id="f0d1e-173">a.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-173">a.</span></span>  <span data-ttu-id="f0d1e-174">Pour chaque ligne de données dans le tableau ci-dessus, cliquez sur **ajouter un attribut utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-174">For each data row in the table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="f0d1e-175">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml token attributes")</span><span class="sxs-lookup"><span data-stu-id="f0d1e-175">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml token attributes")</span></span>
    
    <span data-ttu-id="f0d1e-176">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml token attributes")</span><span class="sxs-lookup"><span data-stu-id="f0d1e-176">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml token attributes")</span></span>
    
    <span data-ttu-id="f0d1e-177">b.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-177">b.</span></span>  <span data-ttu-id="f0d1e-178">Dans la zone de texte **Nom de l’attribut** , indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-178">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="f0d1e-179">c.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-179">c.</span></span>  <span data-ttu-id="f0d1e-180">Dans la zone de texte **Valeur de l’attribut**, sélectionnez la valeur d’attribut indiquée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-180">In the **Attribute Value** textbox, select the attribute  value shown for that row.</span></span>
    
    <span data-ttu-id="f0d1e-181">d.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-181">d.</span></span>  <span data-ttu-id="f0d1e-182">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-182">Click **Ok**.</span></span>
    
6. <span data-ttu-id="f0d1e-183">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="f0d1e-183">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="f0d1e-185">Dans la section **Configuration de TimeOffManager**, cliquez sur **Configurer TimeOffManager** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-185">On the **TimeOffManager Configuration** section, click **Configure TimeOffManager** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f0d1e-186">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="f0d1e-186">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Section Configuration de TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. <span data-ttu-id="f0d1e-188">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise TimeOffManager en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-188">In a different web browser window, log into your TimeOffManager company site as an administrator.</span></span>

9. <span data-ttu-id="f0d1e-189">Accédez à **Account \> Account Options \> Single Sign-On Settings**.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-189">Go to **Account \> Account Options \> Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="f0d1e-190">![Paramètres d’authentification unique](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "paramètres d’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="f0d1e-190">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On Settings")</span></span>
7. <span data-ttu-id="f0d1e-191">Dans la section **Single Sign-On Settings** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f0d1e-191">In the **Single Sign-On Settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="f0d1e-192">![Paramètres d’authentification unique](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "paramètres d’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="f0d1e-192">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="f0d1e-193">a.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-193">a.</span></span> <span data-ttu-id="f0d1e-194">Ouvrez votre certificat codé en base 64 dans le bloc-notes, copiez son contenu dans le Presse-papiers et collez-le dans la zone de texte **X.509 Certificate** .</span><span class="sxs-lookup"><span data-stu-id="f0d1e-194">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>
   
   <span data-ttu-id="f0d1e-195">b.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-195">b.</span></span> <span data-ttu-id="f0d1e-196">Dans la zone de texte **Émetteur IdP**, collez la valeur de **ID d’entité SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-196">In **Idp Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="f0d1e-197">c.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-197">c.</span></span> <span data-ttu-id="f0d1e-198">Dans la zone de texte **IdP Endpoint URL** (URL du point de terminaison IdP), collez la valeur de l’**URL du service d’authentification unique SAML** que vous avez copiée sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-198">In **IdP Endpoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="f0d1e-199">d.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-199">d.</span></span> <span data-ttu-id="f0d1e-200">Dans **Enforce SAML**, sélectionnez **No**.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-200">As **Enforce SAML**, select **No**.</span></span>
   
   <span data-ttu-id="f0d1e-201">e.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-201">e.</span></span> <span data-ttu-id="f0d1e-202">Dans **Auto-Create Users**, sélectionnez **Yes**.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-202">As **Auto-Create Users**, select **Yes**.</span></span>
   
   <span data-ttu-id="f0d1e-203">f.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-203">f.</span></span> <span data-ttu-id="f0d1e-204">Dans la zone de texte **Logout URL (URL de déconnexion)**, collez la valeur **URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-204">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="f0d1e-205">g.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-205">g.</span></span> <span data-ttu-id="f0d1e-206">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-206">click **Save Changes**.</span></span>

11. <span data-ttu-id="f0d1e-207">Sur la page **Paramètres de l’authentification unique**, copiez la valeur **URL Assertion Consumer Service**  et collez-la dans la zone de texte **URL de réponse** de la section **Domaine et URL TimeOffManager** dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-207">In **Single Sign on settings** page, copy the value of **Assertion Consumer Service URL** and paste it in the **Reply URL** text box under **TimeOffManager Domain and URLs** section in Azure portal.</span></span> 

      <span data-ttu-id="f0d1e-208">![Paramètres d’authentification unique](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "paramètres d’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="f0d1e-208">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On Settings")</span></span>

> [!TIP]
> <span data-ttu-id="f0d1e-209">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-209">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f0d1e-210">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-210">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f0d1e-211">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f0d1e-211">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f0d1e-212">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0d1e-212">Create an Azure AD test user</span></span>
<span data-ttu-id="f0d1e-213">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="f0d1e-215">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f0d1e-215">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f0d1e-216">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-216">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f0d1e-218">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-218">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Utilisateurs et groupes --> Tous les utilisateurs](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f0d1e-220">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-220">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bouton Ajouter](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f0d1e-222">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f0d1e-222">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Boîte de dialogue utilisateur](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f0d1e-224">a.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-224">a.</span></span> <span data-ttu-id="f0d1e-225">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-225">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f0d1e-226">b.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-226">b.</span></span> <span data-ttu-id="f0d1e-227">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-227">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f0d1e-228">c.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-228">c.</span></span> <span data-ttu-id="f0d1e-229">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-229">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f0d1e-230">d.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-230">d.</span></span> <span data-ttu-id="f0d1e-231">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-231">Click **Create**.</span></span>
 
### <a name="create-a-timeoffmanager-test-user"></a><span data-ttu-id="f0d1e-232">Créer un utilisateur de test TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="f0d1e-232">Create a TimeOffManager test user</span></span>

<span data-ttu-id="f0d1e-233">Pour se connecter à TimeOffManager, les utilisateurs d’Azure AD doivent être approvisionnés dans TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-233">In order to enable Azure AD users to log into TimeOffManager, they must be provisioned to TimeOffManager.</span></span>  

<span data-ttu-id="f0d1e-234">TimeOffManager prend en charge l’approvisionnement juste-à-temps des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-234">TimeOffManager supports just in time user provisioning.</span></span> <span data-ttu-id="f0d1e-235">Vous n’avez rien à faire.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-235">There is no action item for you.</span></span>  

<span data-ttu-id="f0d1e-236">Les utilisateurs sont ajoutés automatiquement lors de la première connexion à l’aide de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-236">The users are added automatically during the first login using single sign on.</span></span>

>[!NOTE]
><span data-ttu-id="f0d1e-237">Vous pouvez utiliser n’importe quel autre outil ou API de création de compte d’utilisateur, fourni par TimeOffManager, pour approvisionner des comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-237">You can use any other TimeOffManager user account creation tools or APIs provided by TimeOffManager to provision Azure AD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f0d1e-238">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0d1e-238">Assign the Azure AD test user</span></span>

<span data-ttu-id="f0d1e-239">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TimeOffManager.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="f0d1e-241">**Pour assigner Britta Simon à TimeOffManager, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f0d1e-241">**To assign Britta Simon to TimeOffManager, perform the following steps:**</span></span>

1. <span data-ttu-id="f0d1e-242">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="f0d1e-244">Dans la liste des applications, sélectionnez **TimeOffManager**.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-244">In the applications list, select **TimeOffManager**.</span></span>

    ![TimeOffManager dans la liste des applications](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. <span data-ttu-id="f0d1e-246">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="f0d1e-248">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-248">Click **Add** button.</span></span> <span data-ttu-id="f0d1e-249">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="f0d1e-251">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f0d1e-252">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f0d1e-253">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f0d1e-254">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="f0d1e-254">Test single sign-on</span></span>

<span data-ttu-id="f0d1e-255">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-255">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f0d1e-256">Lorsque vous cliquez sur la vignette TimeOffManager dans le panneau d’accès, vous devez être connecté automatiquement à votre application TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="f0d1e-256">When you click the TimeOffManager tile in the Access Panel, you should get automatically signed-on to your TimeOffManager application.</span></span> <span data-ttu-id="f0d1e-257">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f0d1e-257">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f0d1e-258">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f0d1e-258">Additional resources</span></span>

* [<span data-ttu-id="f0d1e-259">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0d1e-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f0d1e-260">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="f0d1e-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

