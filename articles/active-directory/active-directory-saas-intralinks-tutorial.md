---
title: "Didacticiel : intégration d’Azure Active Directory à Intralinks | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Intralinks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 6fa49c932d0c48d4b48e04fe91af9fc86a0c1cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a><span data-ttu-id="f6c91-103">Didacticiel : intégration d’Azure Active Directory à Intralinks</span><span class="sxs-lookup"><span data-stu-id="f6c91-103">Tutorial: Azure Active Directory integration with Intralinks</span></span>

<span data-ttu-id="f6c91-104">Dans ce didacticiel, vous apprendrez comment toointegrate Intralinks avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f6c91-104">In this tutorial, you learn how toointegrate Intralinks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f6c91-105">Intégration Intralinks à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="f6c91-105">Integrating Intralinks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f6c91-106">Vous pouvez contrôler dans Azure AD qui a accès tooIntralinks</span><span class="sxs-lookup"><span data-stu-id="f6c91-106">You can control in Azure AD who has access tooIntralinks</span></span>
- <span data-ttu-id="f6c91-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooIntralinks (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6c91-107">You can enable your users tooautomatically get signed-on tooIntralinks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f6c91-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="f6c91-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f6c91-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f6c91-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6c91-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f6c91-110">Prerequisites</span></span>

<span data-ttu-id="f6c91-111">tooconfigure intégration d’Azure AD avec Intralinks, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f6c91-111">tooconfigure Azure AD integration with Intralinks, you need hello following items:</span></span>

- <span data-ttu-id="f6c91-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6c91-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f6c91-113">Un abonnement Intralinks pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="f6c91-113">An Intralinks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f6c91-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="f6c91-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f6c91-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="f6c91-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f6c91-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f6c91-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f6c91-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f6c91-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f6c91-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="f6c91-118">Scenario description</span></span>
<span data-ttu-id="f6c91-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="f6c91-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f6c91-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="f6c91-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f6c91-121">Ajout de Intralinks à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f6c91-121">Adding Intralinks from hello gallery</span></span>
2. <span data-ttu-id="f6c91-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6c91-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intralinks-from-hello-gallery"></a><span data-ttu-id="f6c91-123">Ajout de Intralinks à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f6c91-123">Adding Intralinks from hello gallery</span></span>
<span data-ttu-id="f6c91-124">intégration de hello tooconfigure de Intralinks dans Azure AD, vous devez tooadd Intralinks à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="f6c91-124">tooconfigure hello integration of Intralinks into Azure AD, you need tooadd Intralinks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f6c91-125">**tooadd Intralinks à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f6c91-125">**tooadd Intralinks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6c91-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f6c91-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f6c91-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="f6c91-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f6c91-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f6c91-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="f6c91-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f6c91-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="f6c91-133">Dans la zone de recherche de hello, tapez **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="f6c91-133">In hello search box, type **Intralinks**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="f6c91-135">Dans le volet de résultats hello, sélectionnez **Intralinks**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f6c91-135">In hello results panel, select **Intralinks**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f6c91-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6c91-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f6c91-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Intralinks, en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="f6c91-138">In this section, you configure and test Azure AD single sign-on with Intralinks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f6c91-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Intralinks est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6c91-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Intralinks is tooa user in Azure AD.</span></span> <span data-ttu-id="f6c91-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Intralinks doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="f6c91-140">In other words, a link relationship between an Azure AD user and hello related user in Intralinks needs toobe established.</span></span>

<span data-ttu-id="f6c91-141">Dans Intralinks, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="f6c91-141">In Intralinks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f6c91-142">tooconfigure et test Azure AD l’authentification unique avec Intralinks, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="f6c91-142">tooconfigure and test Azure AD single sign-on with Intralinks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f6c91-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="f6c91-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f6c91-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f6c91-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f6c91-145">**[Création d’un utilisateur de test Intralinks](#creating-an-intralinks-test-user)**  -toohave un équivalent de Britta Simon dans Intralinks est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f6c91-145">**[Creating an Intralinks test user](#creating-an-intralinks-test-user)** - toohave a counterpart of Britta Simon in Intralinks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f6c91-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f6c91-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f6c91-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="f6c91-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f6c91-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6c91-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f6c91-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Intralinks.</span><span class="sxs-lookup"><span data-stu-id="f6c91-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Intralinks application.</span></span>

<span data-ttu-id="f6c91-150">**tooconfigure Azure AD single sign-on avec Intralinks, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f6c91-150">**tooconfigure Azure AD single sign-on with Intralinks, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6c91-151">Bonjour portail Azure, sur hello **Intralinks** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="f6c91-151">In hello Azure portal, on hello **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="f6c91-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f6c91-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. <span data-ttu-id="f6c91-155">Sur hello **Intralinks domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f6c91-155">On hello **Intralinks Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    <span data-ttu-id="f6c91-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span><span class="sxs-lookup"><span data-stu-id="f6c91-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:  `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f6c91-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="f6c91-158">This value is not real.</span></span> <span data-ttu-id="f6c91-159">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="f6c91-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="f6c91-160">Contact [équipe de support Client de Intralinks](https://www.intralinks.com/contact-1) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="f6c91-160">Contact [Intralinks Client support team](https://www.intralinks.com/contact-1) tooget this value.</span></span> 
 
4. <span data-ttu-id="f6c91-161">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f6c91-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. <span data-ttu-id="f6c91-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="f6c91-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f6c91-165">tooconfigure l’authentification unique sur **Intralinks** côté, vous devez hello toosend téléchargé **Metadata XML** [Intralinks l’équipe de support](https://www.intralinks.com/contact-1).</span><span class="sxs-lookup"><span data-stu-id="f6c91-165">tooconfigure single sign-on on **Intralinks** side, you need toosend hello downloaded **Metadata XML** [Intralinks support team](https://www.intralinks.com/contact-1).</span></span> <span data-ttu-id="f6c91-166">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="f6c91-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f6c91-167">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="f6c91-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f6c91-168">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="f6c91-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f6c91-169">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f6c91-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f6c91-170">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6c91-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="f6c91-171">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="f6c91-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="f6c91-173">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f6c91-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6c91-174">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f6c91-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f6c91-176">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f6c91-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f6c91-178">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="f6c91-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f6c91-180">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f6c91-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f6c91-182">a.</span><span class="sxs-lookup"><span data-stu-id="f6c91-182">a.</span></span> <span data-ttu-id="f6c91-183">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f6c91-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f6c91-184">b.</span><span class="sxs-lookup"><span data-stu-id="f6c91-184">b.</span></span> <span data-ttu-id="f6c91-185">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f6c91-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f6c91-186">c.</span><span class="sxs-lookup"><span data-stu-id="f6c91-186">c.</span></span> <span data-ttu-id="f6c91-187">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="f6c91-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f6c91-188">d.</span><span class="sxs-lookup"><span data-stu-id="f6c91-188">d.</span></span> <span data-ttu-id="f6c91-189">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="f6c91-189">Click **Create**.</span></span>
 
### <a name="creating-an-intralinks-test-user"></a><span data-ttu-id="f6c91-190">Création d’un utilisateur de test Intralinks</span><span class="sxs-lookup"><span data-stu-id="f6c91-190">Creating an Intralinks test user</span></span>

<span data-ttu-id="f6c91-191">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Intralinks.</span><span class="sxs-lookup"><span data-stu-id="f6c91-191">In this section, you create a user called Britta Simon in Intralinks.</span></span> <span data-ttu-id="f6c91-192">Collaborez avec [Intralinks l’équipe de support](https://www.intralinks.com/contact-1) utilisateurs hello tooadd plate-forme de Intralinks hello.</span><span class="sxs-lookup"><span data-stu-id="f6c91-192">Please work with [Intralinks support team](https://www.intralinks.com/contact-1) tooadd hello users in hello Intralinks platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f6c91-193">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6c91-193">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f6c91-194">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooIntralinks.</span><span class="sxs-lookup"><span data-stu-id="f6c91-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIntralinks.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="f6c91-196">**tooassign Britta Simon tooIntralinks, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f6c91-196">**tooassign Britta Simon tooIntralinks, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6c91-197">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f6c91-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="f6c91-199">Dans la liste des applications hello, sélectionnez **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="f6c91-199">In hello applications list, select **Intralinks**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. <span data-ttu-id="f6c91-201">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f6c91-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="f6c91-203">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f6c91-203">Click **Add** button.</span></span> <span data-ttu-id="f6c91-204">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f6c91-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="f6c91-206">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="f6c91-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f6c91-207">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f6c91-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f6c91-208">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f6c91-208">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="add-intralinks-via-or-elite-application"></a><span data-ttu-id="f6c91-209">Ajouter une application Intralinks VIA ou Elite</span><span class="sxs-lookup"><span data-stu-id="f6c91-209">Add Intralinks VIA or Elite application</span></span>

<span data-ttu-id="f6c91-210">Intralinks utilise hello même plateforme d’identité de l’authentification unique pour toutes les autres applications Intralinks à l’exception d’application de transaction Nexus.</span><span class="sxs-lookup"><span data-stu-id="f6c91-210">Intralinks uses hello same SSO identity platform for all other Intralinks applications excluding Deal Nexus application.</span></span> <span data-ttu-id="f6c91-211">Par conséquent, si vous envisagez de toute autre application Intralinks toouse tout d’abord vous devez tooconfigure l’authentification unique pour une application Intralinks principal à l’aide de la procédure hello décrite ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="f6c91-211">So if you plan toouse any other Intralinks application then first you have tooconfigure SSO for one Primary Intralinks application using hello procedure described above.</span></span>

<span data-ttu-id="f6c91-212">Une fois que vous pouvez suivre une autre application Intralinks hello ci-dessous procédure tooadd dans votre client qui permettre tirer parti de cette application principale pour l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f6c91-212">After that you can follow hello below procedure tooadd another Intralinks application in your tenant which can leverage this primary application for SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="f6c91-213">Cette fonctionnalité est disponible uniquement tooAzure AD Premium SKU aux clients et non disponible pour les clients gratuit ou de la base de référence (SKU).</span><span class="sxs-lookup"><span data-stu-id="f6c91-213">This feature is available only tooAzure AD Premium SKU Customers and not available for Free or Basic SKU customers.</span></span>

1. <span data-ttu-id="f6c91-214">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f6c91-214">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]


2. <span data-ttu-id="f6c91-216">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="f6c91-216">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f6c91-217">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f6c91-217">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="f6c91-219">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f6c91-219">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="f6c91-221">Dans la zone de recherche de hello, tapez **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="f6c91-221">In hello search box, type **Intralinks**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="f6c91-223">Sur **Intralinks ajouter une application** effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f6c91-223">On **Intralinks Add app** perform hello following steps:</span></span>

    ![Ajout d’une application Intralinks VIA ou Elite](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    <span data-ttu-id="f6c91-225">a.</span><span class="sxs-lookup"><span data-stu-id="f6c91-225">a.</span></span> <span data-ttu-id="f6c91-226">Dans **nom** zone de texte, entrez un nom approprié de l’application hello, par exemple **Intralinks Elite**.</span><span class="sxs-lookup"><span data-stu-id="f6c91-226">In **Name** textbox, enter appropriate name of hello application e.g. **Intralinks Elite**.</span></span>

    <span data-ttu-id="f6c91-227">b.</span><span class="sxs-lookup"><span data-stu-id="f6c91-227">b.</span></span> <span data-ttu-id="f6c91-228">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f6c91-228">Click **Add** button.</span></span>

6.  <span data-ttu-id="f6c91-229">Bonjour portail Azure, sur hello **Intralinks** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="f6c91-229">In hello Azure portal, on hello **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

7. <span data-ttu-id="f6c91-231">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **lié Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f6c91-231">On hello **Single sign-on** dialog, select **Mode** as   **Linked Sign-on**.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. <span data-ttu-id="f6c91-233">Obtenir l’URL de l’authentification unique a été initiée hello hello SP de [Intralinks équipe](https://www.intralinks.com/contact-1) pour hello autre application Intralinks et entrez-la dans **configurer l’authentification sur l’URL** comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f6c91-233">Get hello hello SP Initiated SSO URL from [Intralinks team](https://www.intralinks.com/contact-1) for hello other Intralinks application and enter it in **Configure Sign-on URL** as shown below.</span></span> 
    
     ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     <span data-ttu-id="f6c91-235">Dans la zone de texte URL de connexion hello, tapez hello l’URL utilisée par votre application de Intralinks tooyour toosign sur les utilisateurs à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="f6c91-235">In hello Sign On URL textbox, type hello URL used by your users toosign-on tooyour Intralinks application using hello following pattern:</span></span>
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. <span data-ttu-id="f6c91-236">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="f6c91-236">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="f6c91-238">Affecter des hello application toouser ou des groupes comme indiqué dans la section de hello  **[utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**.</span><span class="sxs-lookup"><span data-stu-id="f6c91-238">Assign hello application toouser or groups as shown in hello section **[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)**.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="f6c91-239">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="f6c91-239">Testing single sign-on</span></span>

<span data-ttu-id="f6c91-240">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="f6c91-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f6c91-241">Lorsque vous cliquez sur hello Intralinks vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour Intralinks application.</span><span class="sxs-lookup"><span data-stu-id="f6c91-241">When you click hello Intralinks tile in hello Access Panel, you should get automatically signed-on tooyour Intralinks application.</span></span>
<span data-ttu-id="f6c91-242">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f6c91-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f6c91-243">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f6c91-243">Additional resources</span></span>

* [<span data-ttu-id="f6c91-244">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6c91-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f6c91-245">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="f6c91-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png

