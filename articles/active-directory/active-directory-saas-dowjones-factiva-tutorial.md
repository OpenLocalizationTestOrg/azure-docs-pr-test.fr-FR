---
title: "Didacticiel : Intégration d’Azure Active Directory dans Dow Jones Factiva | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Vali Jones Factiva."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b36e97e8-37a6-4096-a894-530427ee1331
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: jeedes
ms.openlocfilehash: 7c42b5d64433c7bdcb512771a3e68115cc5f6874
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dow-jones-factiva"></a><span data-ttu-id="e58cc-103">Didacticiel : Intégration d’Azure Active Directory dans Dow Jones Factiva</span><span class="sxs-lookup"><span data-stu-id="e58cc-103">Tutorial: Azure Active Directory integration with Dow Jones Factiva</span></span>

<span data-ttu-id="e58cc-104">Dans ce didacticiel, vous apprendrez comment toointegrate Factiva de Jones Vali avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e58cc-104">In this tutorial, you learn how toointegrate Dow Jones Factiva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e58cc-105">Intégration Vali Jones Factiva à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="e58cc-105">Integrating Dow Jones Factiva with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e58cc-106">Vous pouvez contrôler dans Azure AD qui a accès tooDow Jones Factiva</span><span class="sxs-lookup"><span data-stu-id="e58cc-106">You can control in Azure AD who has access tooDow Jones Factiva</span></span>
- <span data-ttu-id="e58cc-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooDow Factiva Jones (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="e58cc-107">You can enable your users tooautomatically get signed-on tooDow Jones Factiva (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e58cc-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="e58cc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e58cc-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e58cc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e58cc-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e58cc-110">Prerequisites</span></span>

<span data-ttu-id="e58cc-111">tooconfigure intégration d’Azure AD avec Vali Jones Factiva, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e58cc-111">tooconfigure Azure AD integration with Dow Jones Factiva, you need hello following items:</span></span>

- <span data-ttu-id="e58cc-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="e58cc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e58cc-113">Un abonnement Dow Jones Factiva avec authentification unique activée</span><span class="sxs-lookup"><span data-stu-id="e58cc-113">A Dow Jones Factiva single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e58cc-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="e58cc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e58cc-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="e58cc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e58cc-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e58cc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e58cc-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e58cc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e58cc-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="e58cc-118">Scenario description</span></span>
<span data-ttu-id="e58cc-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="e58cc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e58cc-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="e58cc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e58cc-121">Ajout de Vali Jones Factiva à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e58cc-121">Adding Dow Jones Factiva from hello gallery</span></span>
2. <span data-ttu-id="e58cc-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e58cc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dow-jones-factiva-from-hello-gallery"></a><span data-ttu-id="e58cc-123">Ajout de Vali Jones Factiva à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e58cc-123">Adding Dow Jones Factiva from hello gallery</span></span>
<span data-ttu-id="e58cc-124">tooconfigure hello intégration de Vali Jones Factiva dans Azure AD, vous devez tooadd Vali Jones Factiva à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="e58cc-124">tooconfigure hello integration of Dow Jones Factiva into Azure AD, you need tooadd Dow Jones Factiva from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e58cc-125">**tooadd Factiva de Jones Vali à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e58cc-125">**tooadd Dow Jones Factiva from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e58cc-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="e58cc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e58cc-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="e58cc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e58cc-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e58cc-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="e58cc-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e58cc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="e58cc-133">Dans la zone de recherche de hello, tapez **Vali Jones Factiva**.</span><span class="sxs-lookup"><span data-stu-id="e58cc-133">In hello search box, type **Dow Jones Factiva**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_search.png)

5. <span data-ttu-id="e58cc-135">Dans le volet de résultats hello, sélectionnez **Vali Jones Factiva**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e58cc-135">In hello results panel, select **Dow Jones Factiva**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e58cc-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e58cc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e58cc-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Dow Jones Factiva avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="e58cc-138">In this section, you configure and test Azure AD single sign-on with Dow Jones Factiva based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e58cc-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello Vali Jones Factiva est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e58cc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Dow Jones Factiva is tooa user in Azure AD.</span></span> <span data-ttu-id="e58cc-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Vali Jones Factiva doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="e58cc-140">In other words, a link relationship between an Azure AD user and hello related user in Dow Jones Factiva needs toobe established.</span></span>

<span data-ttu-id="e58cc-141">Dans Vali Jones Factiva, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="e58cc-141">In Dow Jones Factiva, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e58cc-142">tooconfigure et test Azure AD l’authentification unique avec Vali Jones Factiva, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="e58cc-142">tooconfigure and test Azure AD single sign-on with Dow Jones Factiva, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e58cc-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="e58cc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e58cc-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e58cc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e58cc-145">**[Création d’un utilisateur de test Vali Jones Factiva](#creating-a-dow-jones-factiva-test-user)**  -toohave un équivalent de Britta Simon dans Vali Jones Factiva qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e58cc-145">**[Creating a Dow Jones Factiva test user](#creating-a-dow-jones-factiva-test-user)** - toohave a counterpart of Britta Simon in Dow Jones Factiva that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e58cc-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e58cc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e58cc-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="e58cc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e58cc-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e58cc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e58cc-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Vali Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="e58cc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Dow Jones Factiva application.</span></span>

<span data-ttu-id="e58cc-150">**tooconfigure Azure AD l’authentification unique avec Vali Jones Factiva, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e58cc-150">**tooconfigure Azure AD single sign-on with Dow Jones Factiva, perform hello following steps:**</span></span>

1. <span data-ttu-id="e58cc-151">Bonjour portail Azure, sur hello **Vali Jones Factiva** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="e58cc-151">In hello Azure portal, on hello **Dow Jones Factiva** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="e58cc-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e58cc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_samlbase.png)

3. <span data-ttu-id="e58cc-155">Sur hello **Vali Jones Factiva domaine et les URL** section, hello utilisateur n’est pas tooperform toutes les étapes que l’application hello est déjà pré-intégration à Azure.</span><span class="sxs-lookup"><span data-stu-id="e58cc-155">On hello **Dow Jones Factiva Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_url.png)

4. <span data-ttu-id="e58cc-157">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e58cc-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_certificate.png) 

5. <span data-ttu-id="e58cc-159">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="e58cc-159">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e58cc-161">tooconfigure l’authentification unique sur **Vali Jones Factiva** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support Vali Jones Factiva](https://www.dowjones.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="e58cc-161">tooconfigure single sign-on on **Dow Jones Factiva** side, you need toosend hello downloaded **Metadata XML** too[Dow Jones Factiva support team](https://www.dowjones.com/contact/).</span></span> <span data-ttu-id="e58cc-162">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="e58cc-162">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e58cc-163">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="e58cc-163">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e58cc-164">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="e58cc-164">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e58cc-165">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e58cc-165">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e58cc-166">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="e58cc-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="e58cc-167">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="e58cc-167">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="e58cc-169">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e58cc-169">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e58cc-170">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="e58cc-170">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e58cc-172">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="e58cc-172">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e58cc-174">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="e58cc-174">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e58cc-176">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e58cc-176">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e58cc-178">a.</span><span class="sxs-lookup"><span data-stu-id="e58cc-178">a.</span></span> <span data-ttu-id="e58cc-179">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e58cc-179">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e58cc-180">b.</span><span class="sxs-lookup"><span data-stu-id="e58cc-180">b.</span></span> <span data-ttu-id="e58cc-181">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e58cc-181">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e58cc-182">c.</span><span class="sxs-lookup"><span data-stu-id="e58cc-182">c.</span></span> <span data-ttu-id="e58cc-183">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="e58cc-183">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e58cc-184">d.</span><span class="sxs-lookup"><span data-stu-id="e58cc-184">d.</span></span> <span data-ttu-id="e58cc-185">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="e58cc-185">Click **Create**.</span></span>
 
### <a name="creating-a-dow-jones-factiva-test-user"></a><span data-ttu-id="e58cc-186">Création d’un utilisateur de test Dow Jones Factiva</span><span class="sxs-lookup"><span data-stu-id="e58cc-186">Creating a Dow Jones Factiva test user</span></span>

<span data-ttu-id="e58cc-187">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="e58cc-187">In this section, you create a user called Britta Simon in Dow Jones Factiva.</span></span> <span data-ttu-id="e58cc-188">Collaborez avec Vali [équipe de support Jones Factiva](https://www.dowjones.com/contact/) tooadd les utilisateurs de hello dans la plateforme de Vali Jones Factiva hello.</span><span class="sxs-lookup"><span data-stu-id="e58cc-188">Please work with Dow [Jones Factiva support team](https://www.dowjones.com/contact/) tooadd hello users in hello Dow Jones Factiva platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e58cc-189">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e58cc-189">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e58cc-190">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooDow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="e58cc-190">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDow Jones Factiva.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="e58cc-192">**tooassign Britta Simon tooDow Jones Factiva, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e58cc-192">**tooassign Britta Simon tooDow Jones Factiva, perform hello following steps:**</span></span>

1. <span data-ttu-id="e58cc-193">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e58cc-193">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="e58cc-195">Dans la liste des applications hello, sélectionnez **Vali Jones Factiva**.</span><span class="sxs-lookup"><span data-stu-id="e58cc-195">In hello applications list, select **Dow Jones Factiva**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_app.png) 

3. <span data-ttu-id="e58cc-197">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e58cc-197">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="e58cc-199">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e58cc-199">Click **Add** button.</span></span> <span data-ttu-id="e58cc-200">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e58cc-200">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="e58cc-202">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="e58cc-202">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e58cc-203">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e58cc-203">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e58cc-204">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e58cc-204">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e58cc-205">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="e58cc-205">Testing single sign-on</span></span>

<span data-ttu-id="e58cc-206">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="e58cc-206">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e58cc-207">Lorsque vous cliquez sur mosaïque Vali Jones Factiva hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Vali Jones Factiva application.</span><span class="sxs-lookup"><span data-stu-id="e58cc-207">When you click hello Dow Jones Factiva tile in hello Access Panel, you should get automatically signed-on tooyour Dow Jones Factiva application.</span></span>
<span data-ttu-id="e58cc-208">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e58cc-208">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e58cc-209">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e58cc-209">Additional resources</span></span>

* [<span data-ttu-id="e58cc-210">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e58cc-210">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e58cc-211">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="e58cc-211">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_203.png

