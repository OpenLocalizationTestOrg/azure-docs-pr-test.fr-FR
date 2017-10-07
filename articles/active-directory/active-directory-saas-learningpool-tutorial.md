---
title: "Didacticiel : Intégration d’Azure Active Directory avec Learningpool Act | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Learningpool Act."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 51e8695f-31e1-4d09-8eb3-13241999d99f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: f343623f08bb60e143aaff07d93e4ef773232e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learningpool-act"></a><span data-ttu-id="f8295-103">Didacticiel : Intégration d’Azure Active Directory à Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="f8295-103">Tutorial: Azure Active Directory integration with Learningpool Act</span></span>

<span data-ttu-id="f8295-104">Dans ce didacticiel, vous apprendrez comment toointegrate Learningpool agissent avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f8295-104">In this tutorial, you learn how toointegrate Learningpool Act with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f8295-105">Intégration Act de Learningpool à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="f8295-105">Integrating Learningpool Act with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f8295-106">Vous pouvez contrôler dans Azure AD qui a accès tooLearningpool Act</span><span class="sxs-lookup"><span data-stu-id="f8295-106">You can control in Azure AD who has access tooLearningpool Act</span></span>
- <span data-ttu-id="f8295-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooLearningpool Act (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8295-107">You can enable your users tooautomatically get signed-on tooLearningpool Act (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f8295-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="f8295-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f8295-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f8295-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8295-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f8295-110">Prerequisites</span></span>

<span data-ttu-id="f8295-111">tooconfigure intégration d’Azure AD avec Learningpool Act, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f8295-111">tooconfigure Azure AD integration with Learningpool Act, you need hello following items:</span></span>

- <span data-ttu-id="f8295-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8295-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f8295-113">Un abonnement Learningpool Act pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="f8295-113">A Learningpool Act single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f8295-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="f8295-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f8295-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="f8295-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f8295-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f8295-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f8295-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f8295-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f8295-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="f8295-118">Scenario description</span></span>
<span data-ttu-id="f8295-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="f8295-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f8295-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="f8295-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f8295-121">Ajout d’Act de Learningpool à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f8295-121">Adding Learningpool Act from hello gallery</span></span>
2. <span data-ttu-id="f8295-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8295-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learningpool-act-from-hello-gallery"></a><span data-ttu-id="f8295-123">Ajout d’Act de Learningpool à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f8295-123">Adding Learningpool Act from hello gallery</span></span>
<span data-ttu-id="f8295-124">intégration de hello tooconfigure de Learningpool Act dans Azure AD, vous devez tooadd Act de Learningpool à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="f8295-124">tooconfigure hello integration of Learningpool Act into Azure AD, you need tooadd Learningpool Act from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f8295-125">**tooadd Act de Learningpool à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f8295-125">**tooadd Learningpool Act from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8295-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f8295-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f8295-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="f8295-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f8295-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f8295-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="f8295-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f8295-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="f8295-133">Dans la zone de recherche de hello, tapez **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="f8295-133">In hello search box, type **Learningpool Act**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_search.png)

5. <span data-ttu-id="f8295-135">Dans le volet de résultats hello, sélectionnez **Learningpool Act**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f8295-135">In hello results panel, select **Learningpool Act**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f8295-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8295-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f8295-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Learningpool Act avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="f8295-138">In this section, you configure and test Azure AD single sign-on with Learningpool Act based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f8295-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Learningpool Act est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8295-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Learningpool Act is tooa user in Azure AD.</span></span> <span data-ttu-id="f8295-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Learningpool Act doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="f8295-140">In other words, a link relationship between an Azure AD user and hello related user in Learningpool Act needs toobe established.</span></span>

<span data-ttu-id="f8295-141">Dans Learningpool Act, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="f8295-141">In Learningpool Act, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f8295-142">tooconfigure et test Azure AD l’authentification unique sur Learningpool ACT, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="f8295-142">tooconfigure and test Azure AD single sign-on with Learningpool Act, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f8295-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="f8295-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f8295-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f8295-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f8295-145">**[Création d’un utilisateur de test Act de Learningpool](#creating-a-learningpool-act-test-user)**  -toohave un équivalent de Britta Simon dans Learningpool Act qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f8295-145">**[Creating a Learningpool Act test user](#creating-a-learningpool-act-test-user)** - toohave a counterpart of Britta Simon in Learningpool Act that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f8295-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f8295-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f8295-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="f8295-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f8295-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8295-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f8295-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="f8295-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Learningpool Act application.</span></span>

<span data-ttu-id="f8295-150">**tooconfigure Azure AD l’authentification unique sur Learningpool ACT, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f8295-150">**tooconfigure Azure AD single sign-on with Learningpool Act, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8295-151">Bonjour portail Azure, sur hello **Learningpool Act** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="f8295-151">In hello Azure portal, on hello **Learningpool Act** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="f8295-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f8295-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_samlbase.png)

3. <span data-ttu-id="f8295-155">Sur hello **Learningpool Act domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f8295-155">On hello **Learningpool Act Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_url.png)

    <span data-ttu-id="f8295-157">a.</span><span class="sxs-lookup"><span data-stu-id="f8295-157">a.</span></span> <span data-ttu-id="f8295-158">Bonjour **URL de connexion** zone de texte, tapez l’URL hello :`https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span><span class="sxs-lookup"><span data-stu-id="f8295-158">In hello **Sign-on URL** textbox, type hello URL: `https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span></span>

    <span data-ttu-id="f8295-159">b.</span><span class="sxs-lookup"><span data-stu-id="f8295-159">b.</span></span> <span data-ttu-id="f8295-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="f8295-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.Learningpool.com/shibboleth` |
    | `https://<subdomain>.preview.Learningpool.com/shibboleth` |

    > [!NOTE] 
    > <span data-ttu-id="f8295-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="f8295-161">These values are not real.</span></span> <span data-ttu-id="f8295-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="f8295-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f8295-163">Contact [équipe de support technique Learningpool Act Client](https://www.Learningpool.com/support) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="f8295-163">Contact [Learningpool Act Client support team](https://www.Learningpool.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="f8295-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f8295-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_certificate.png) 

5. <span data-ttu-id="f8295-166">Application de la loi de Learningpool attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="f8295-166">Learningpool Act application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="f8295-167">Veuillez configurer hello suivant des revendications pour cette application.</span><span class="sxs-lookup"><span data-stu-id="f8295-167">Please configure hello following claims for this application.</span></span> <span data-ttu-id="f8295-168">Vous pouvez gérer les valeurs de ces attributs hello depuis hello **« Mémoire »** onglet de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="f8295-168">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="f8295-169">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="f8295-169">hello following screenshot shows an example for this.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_attribute.png) 

6. <span data-ttu-id="f8295-171">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image de hello et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f8295-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="f8295-172">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="f8295-172">Attribute Name</span></span> | <span data-ttu-id="f8295-173">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="f8295-173">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="f8295-174">urn:oid:1.2.840.113556.1.4.221</span><span class="sxs-lookup"><span data-stu-id="f8295-174">urn:oid:1.2.840.113556.1.4.221</span></span> | <span data-ttu-id="f8295-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="f8295-175">user.userprincipalname</span></span> |
    | <span data-ttu-id="f8295-176">urn:oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="f8295-176">urn:oid:2.5.4.42</span></span> | <span data-ttu-id="f8295-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="f8295-177">user.givenname</span></span> |
    | <span data-ttu-id="f8295-178">urn:oid:0.9.2342.19200300.100.1.3</span><span class="sxs-lookup"><span data-stu-id="f8295-178">urn:oid:0.9.2342.19200300.100.1.3</span></span> | <span data-ttu-id="f8295-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="f8295-179">user.mail</span></span> |    
    | <span data-ttu-id="f8295-180">urn:oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="f8295-180">urn:oid:2.5.4.4</span></span> | <span data-ttu-id="f8295-181">user.surname</span><span class="sxs-lookup"><span data-stu-id="f8295-181">user.surname</span></span> |
    
    <span data-ttu-id="f8295-182">a.</span><span class="sxs-lookup"><span data-stu-id="f8295-182">a.</span></span> <span data-ttu-id="f8295-183">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f8295-183">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="f8295-186">b.</span><span class="sxs-lookup"><span data-stu-id="f8295-186">b.</span></span> <span data-ttu-id="f8295-187">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="f8295-187">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="f8295-188">c.</span><span class="sxs-lookup"><span data-stu-id="f8295-188">c.</span></span> <span data-ttu-id="f8295-189">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="f8295-189">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="f8295-190">d.</span><span class="sxs-lookup"><span data-stu-id="f8295-190">d.</span></span> <span data-ttu-id="f8295-191">Laissez hello **Namespace** vide.</span><span class="sxs-lookup"><span data-stu-id="f8295-191">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="f8295-192">e.</span><span class="sxs-lookup"><span data-stu-id="f8295-192">e.</span></span> <span data-ttu-id="f8295-193">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f8295-193">Click **Ok**.</span></span>

7. <span data-ttu-id="f8295-194">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="f8295-194">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Learningpool-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f8295-196">tooconfigure l’authentification unique sur **Learningpool Act** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support technique Learningpool Act](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="f8295-196">tooconfigure single sign-on on **Learningpool Act** side, you need toosend hello downloaded **Metadata XML** too[Learningpool Act support team](https://www.Learningpool.com/support).</span></span> <span data-ttu-id="f8295-197">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="f8295-197">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f8295-198">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="f8295-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f8295-199">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="f8295-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f8295-200">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f8295-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f8295-201">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8295-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="f8295-202">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="f8295-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="f8295-204">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f8295-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8295-205">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f8295-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f8295-207">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f8295-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f8295-209">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="f8295-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f8295-211">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f8295-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f8295-213">a.</span><span class="sxs-lookup"><span data-stu-id="f8295-213">a.</span></span> <span data-ttu-id="f8295-214">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f8295-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f8295-215">b.</span><span class="sxs-lookup"><span data-stu-id="f8295-215">b.</span></span> <span data-ttu-id="f8295-216">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f8295-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f8295-217">c.</span><span class="sxs-lookup"><span data-stu-id="f8295-217">c.</span></span> <span data-ttu-id="f8295-218">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="f8295-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f8295-219">d.</span><span class="sxs-lookup"><span data-stu-id="f8295-219">d.</span></span> <span data-ttu-id="f8295-220">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="f8295-220">Click **Create**.</span></span>
 
### <a name="creating-a-learningpool-act-test-user"></a><span data-ttu-id="f8295-221">Création d’un utilisateur de test Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="f8295-221">Creating a Learningpool Act test user</span></span>

<span data-ttu-id="f8295-222">tooenable Azure AD les utilisateurs toolog dans tooLearningpool Act, vous devez les configurer dans Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="f8295-222">tooenable Azure AD users toolog in tooLearningpool Act, they must be provisioned into Learningpool Act.</span></span>

<span data-ttu-id="f8295-223">Il n’existe aucun élément d’action pour vous tooconfigure configuration de l’utilisateur tooLearningpool Act.</span><span class="sxs-lookup"><span data-stu-id="f8295-223">There is no action item for you tooconfigure user provisioning tooLearningpool Act.</span></span>  
<span data-ttu-id="f8295-224">Les utilisateurs doivent toobe créé par votre [équipe de support technique Learningpool Act](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="f8295-224">Users need toobe created by your [Learningpool Act support team](https://www.Learningpool.com/support).</span></span>

>[!NOTE]
><span data-ttu-id="f8295-225">Vous pouvez utiliser n’importe quel autre Learningpool Act utilisateur compte outil de création ou API fournie par Learningpool Act tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="f8295-225">You can use any other Learningpool Act user account creation tools or APIs provided by Learningpool Act tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f8295-226">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8295-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f8295-227">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooLearningpool Act.</span><span class="sxs-lookup"><span data-stu-id="f8295-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearningpool Act.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="f8295-229">**tooassign Britta Simon tooLearningpool Act, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f8295-229">**tooassign Britta Simon tooLearningpool Act, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8295-230">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f8295-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="f8295-232">Dans la liste des applications hello, sélectionnez **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="f8295-232">In hello applications list, select **Learningpool Act**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_app.png) 

3. <span data-ttu-id="f8295-234">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f8295-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="f8295-236">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f8295-236">Click **Add** button.</span></span> <span data-ttu-id="f8295-237">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f8295-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="f8295-239">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="f8295-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f8295-240">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f8295-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f8295-241">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f8295-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f8295-242">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="f8295-242">Testing single sign-on</span></span>

<span data-ttu-id="f8295-243">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="f8295-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f8295-244">Lorsque vous cliquez sur hello Learningpool Act vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application de Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="f8295-244">When you click hello Learningpool Act tile in hello Access Panel, you should get automatically signed-on tooyour Learningpool Act application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f8295-245">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f8295-245">Additional resources</span></span>

* [<span data-ttu-id="f8295-246">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f8295-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f8295-247">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="f8295-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_203.png

