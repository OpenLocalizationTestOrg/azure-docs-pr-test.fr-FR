---
title: "Tutorial: Intégration d'Azure Active Directory à Skilljar | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Skilljar."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c572f556-98a3-48e6-8e4c-e634b7a2ba70
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: f0f433d82a0b5510ec568ab610863bcade047697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skilljar"></a><span data-ttu-id="5aa12-103">Didacticiel : Intégration d'Azure Active Directory avec Skilljar</span><span class="sxs-lookup"><span data-stu-id="5aa12-103">Tutorial: Azure Active Directory integration with Skilljar</span></span>

<span data-ttu-id="5aa12-104">Dans ce didacticiel, vous apprendrez comment toointegrate Skilljar avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5aa12-104">In this tutorial, you learn how toointegrate Skilljar with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5aa12-105">Intégration Skilljar à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5aa12-105">Integrating Skilljar with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5aa12-106">Vous pouvez contrôler dans Azure AD qui a accès tooSkilljar</span><span class="sxs-lookup"><span data-stu-id="5aa12-106">You can control in Azure AD who has access tooSkilljar</span></span>
- <span data-ttu-id="5aa12-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSkilljar (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="5aa12-107">You can enable your users tooautomatically get signed-on tooSkilljar (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5aa12-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="5aa12-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5aa12-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5aa12-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5aa12-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5aa12-110">Prerequisites</span></span>

<span data-ttu-id="5aa12-111">tooconfigure intégration d’Azure AD avec Skilljar, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5aa12-111">tooconfigure Azure AD integration with Skilljar, you need hello following items:</span></span>

- <span data-ttu-id="5aa12-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5aa12-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5aa12-113">Un abonnement Skilljar pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5aa12-113">A Skilljar single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5aa12-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5aa12-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5aa12-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="5aa12-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5aa12-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5aa12-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5aa12-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5aa12-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5aa12-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5aa12-118">Scenario description</span></span>
<span data-ttu-id="5aa12-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5aa12-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5aa12-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="5aa12-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5aa12-121">Ajout de Skilljar à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5aa12-121">Adding Skilljar from hello gallery</span></span>
2. <span data-ttu-id="5aa12-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5aa12-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skilljar-from-hello-gallery"></a><span data-ttu-id="5aa12-123">Ajout de Skilljar à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5aa12-123">Adding Skilljar from hello gallery</span></span>
<span data-ttu-id="5aa12-124">intégration de hello tooconfigure de Skilljar dans Azure AD, vous devez tooadd Skilljar à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="5aa12-124">tooconfigure hello integration of Skilljar into Azure AD, you need tooadd Skilljar from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5aa12-125">**tooadd Skilljar à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5aa12-125">**tooadd Skilljar from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5aa12-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="5aa12-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5aa12-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5aa12-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5aa12-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5aa12-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="5aa12-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5aa12-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="5aa12-133">Dans la zone de recherche de hello, tapez **Skilljar**.</span><span class="sxs-lookup"><span data-stu-id="5aa12-133">In hello search box, type **Skilljar**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_search.png)

5. <span data-ttu-id="5aa12-135">Dans le volet de résultats hello, sélectionnez **Skilljar**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5aa12-135">In hello results panel, select **Skilljar**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5aa12-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5aa12-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5aa12-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD auprès de Skilljar, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5aa12-138">In this section, you configure and test Azure AD single sign-on with Skilljar based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5aa12-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Skilljar est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5aa12-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Skilljar is tooa user in Azure AD.</span></span> <span data-ttu-id="5aa12-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Skilljar doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="5aa12-140">In other words, a link relationship between an Azure AD user and hello related user in Skilljar needs toobe established.</span></span>

<span data-ttu-id="5aa12-141">Dans Skilljar, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="5aa12-141">In Skilljar, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5aa12-142">tooconfigure et test Azure AD l’authentification unique avec Skilljar, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="5aa12-142">tooconfigure and test Azure AD single sign-on with Skilljar, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5aa12-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5aa12-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5aa12-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5aa12-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5aa12-145">**[Création d’un utilisateur de test Skilljar](#creating-a-skilljar-test-user)**  -toohave un équivalent de Britta Simon dans Skilljar est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5aa12-145">**[Creating a Skilljar test user](#creating-a-skilljar-test-user)** - toohave a counterpart of Britta Simon in Skilljar that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5aa12-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5aa12-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5aa12-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="5aa12-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5aa12-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5aa12-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5aa12-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Skilljar.</span><span class="sxs-lookup"><span data-stu-id="5aa12-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Skilljar application.</span></span>

<span data-ttu-id="5aa12-150">**tooconfigure Azure AD single sign-on avec Skilljar, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5aa12-150">**tooconfigure Azure AD single sign-on with Skilljar, perform hello following steps:**</span></span>

1. <span data-ttu-id="5aa12-151">Bonjour portail Azure, sur hello **Skilljar** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5aa12-151">In hello Azure portal, on hello **Skilljar** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="5aa12-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5aa12-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_samlbase.png)

3. <span data-ttu-id="5aa12-155">Sur hello **Skilljar domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5aa12-155">On hello **Skilljar Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_url.png)

    <span data-ttu-id="5aa12-157">a.</span><span class="sxs-lookup"><span data-stu-id="5aa12-157">a.</span></span> <span data-ttu-id="5aa12-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.skilljar.com/`</span><span class="sxs-lookup"><span data-stu-id="5aa12-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.skilljar.com/`</span></span>

    <span data-ttu-id="5aa12-159">b.</span><span class="sxs-lookup"><span data-stu-id="5aa12-159">b.</span></span> <span data-ttu-id="5aa12-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.skilljar.com/`</span><span class="sxs-lookup"><span data-stu-id="5aa12-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.skilljar.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5aa12-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="5aa12-161">These values are not real.</span></span> <span data-ttu-id="5aa12-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="5aa12-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5aa12-163">Contact [équipe de support Client de Skilljar](http://support.skilljar.com/hc/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="5aa12-163">Contact [Skilljar Client support team](http://support.skilljar.com/hc/) tooget these values.</span></span> 
 
4. <span data-ttu-id="5aa12-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5aa12-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_certificate.png) 

5. <span data-ttu-id="5aa12-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="5aa12-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-skilljar-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5aa12-168">tooconfigure l’authentification unique sur **Skilljar** côté, vous devez hello toosend téléchargé **Metadata XML**, et **nom urn : oasis : noms : tc : SAML:1.1:nameid - valeur de Format de l’identificateur-format : emailAddress** trop[équipe de support Skilljar](http://support.skilljar.com/hc/).</span><span class="sxs-lookup"><span data-stu-id="5aa12-168">tooconfigure single sign-on on **Skilljar** side, you need toosend hello downloaded **Metadata XML**, and **Name Identifier Format Value - urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress** too[Skilljar support team](http://support.skilljar.com/hc/).</span></span> <span data-ttu-id="5aa12-169">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="5aa12-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="5aa12-170">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="5aa12-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5aa12-171">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="5aa12-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5aa12-172">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5aa12-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5aa12-173">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5aa12-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="5aa12-174">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="5aa12-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="5aa12-176">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5aa12-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5aa12-177">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="5aa12-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skilljar-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5aa12-179">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5aa12-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skilljar-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5aa12-181">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="5aa12-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skilljar-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5aa12-183">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5aa12-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skilljar-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5aa12-185">a.</span><span class="sxs-lookup"><span data-stu-id="5aa12-185">a.</span></span> <span data-ttu-id="5aa12-186">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5aa12-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5aa12-187">b.</span><span class="sxs-lookup"><span data-stu-id="5aa12-187">b.</span></span> <span data-ttu-id="5aa12-188">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5aa12-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5aa12-189">c.</span><span class="sxs-lookup"><span data-stu-id="5aa12-189">c.</span></span> <span data-ttu-id="5aa12-190">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5aa12-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5aa12-191">d.</span><span class="sxs-lookup"><span data-stu-id="5aa12-191">d.</span></span> <span data-ttu-id="5aa12-192">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5aa12-192">Click **Create**.</span></span>
 
### <a name="creating-a-skilljar-test-user"></a><span data-ttu-id="5aa12-193">Création d'un utilisateur de test Skilljar</span><span class="sxs-lookup"><span data-stu-id="5aa12-193">Creating a Skilljar test user</span></span>

<span data-ttu-id="5aa12-194">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Skilljar.</span><span class="sxs-lookup"><span data-stu-id="5aa12-194">hello objective of this section is toocreate a user called Britta Simon in Skilljar.</span></span> <span data-ttu-id="5aa12-195">Skilljar prend en charge l'approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="5aa12-195">Skilljar supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="5aa12-196">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="5aa12-196">There is no action item for you in this section.</span></span> <span data-ttu-id="5aa12-197">Un nouvel utilisateur est créé au cours d’une tentative de tooaccess Skilljar s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="5aa12-197">A new user is created during an attempt tooaccess Skilljar if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="5aa12-198">Si vous devez manuellement toocreate un utilisateur, vous devez toocontact hello [équipe de support Skilljar](http://support.skilljar.com/hc/).</span><span class="sxs-lookup"><span data-stu-id="5aa12-198">If you need toocreate a user manually, you need toocontact hello [Skilljar support team](http://support.skilljar.com/hc/).</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5aa12-199">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5aa12-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5aa12-200">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSkilljar.</span><span class="sxs-lookup"><span data-stu-id="5aa12-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSkilljar.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="5aa12-202">**tooassign Britta Simon tooSkilljar, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5aa12-202">**tooassign Britta Simon tooSkilljar, perform hello following steps:**</span></span>

1. <span data-ttu-id="5aa12-203">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5aa12-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5aa12-205">Dans la liste des applications hello, sélectionnez **Skilljar**.</span><span class="sxs-lookup"><span data-stu-id="5aa12-205">In hello applications list, select **Skilljar**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_app.png) 

3. <span data-ttu-id="5aa12-207">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5aa12-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="5aa12-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5aa12-209">Click **Add** button.</span></span> <span data-ttu-id="5aa12-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5aa12-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="5aa12-212">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="5aa12-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5aa12-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5aa12-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5aa12-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5aa12-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5aa12-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5aa12-215">Testing single sign-on</span></span>

<span data-ttu-id="5aa12-216">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="5aa12-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="5aa12-217">Lorsque vous cliquez sur mosaïque Skilljar hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Skilljar application.</span><span class="sxs-lookup"><span data-stu-id="5aa12-217">When you click hello Skilljar tile in hello Access Panel, you should get automatically signed-on tooyour Skilljar application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5aa12-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5aa12-218">Additional resources</span></span>

* [<span data-ttu-id="5aa12-219">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5aa12-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5aa12-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5aa12-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_203.png

