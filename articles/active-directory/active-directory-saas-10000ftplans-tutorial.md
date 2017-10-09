---
title: "Didacticiel : Intégration d’Azure Active Directory à 10,000ft Plans | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et 10 000 pieds Plans."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b60c955e-8fa3-4872-a897-c4e81fd7beac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 9aa6fd079da4f931d4dd7277407a07e56091d7c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-10000ft-plans"></a><span data-ttu-id="aa050-103">Didacticiel : Intégration d’Azure Active Directory à 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="aa050-103">Tutorial: Azure Active Directory integration with 10,000ft Plans</span></span>

<span data-ttu-id="aa050-104">Dans ce didacticiel, vous apprendrez comment toointegrate 10 000 pieds Plans avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="aa050-104">In this tutorial, you learn how toointegrate 10,000ft Plans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aa050-105">Intégration des Plans de ft de 10 000 à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="aa050-105">Integrating 10,000ft Plans with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="aa050-106">Vous pouvez contrôler dans Azure AD qui a accès too10, Plans de texte intégral 000</span><span class="sxs-lookup"><span data-stu-id="aa050-106">You can control in Azure AD who has access too10,000ft Plans</span></span>
- <span data-ttu-id="aa050-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté too10, Plans 000ft (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa050-107">You can enable your users tooautomatically get signed-on too10,000ft Plans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="aa050-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="aa050-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="aa050-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aa050-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa050-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="aa050-110">Prerequisites</span></span>

<span data-ttu-id="aa050-111">tooconfigure intégration d’Azure AD avec des Plans de ft de 10 000, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="aa050-111">tooconfigure Azure AD integration with 10,000ft Plans, you need hello following items:</span></span>

- <span data-ttu-id="aa050-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa050-112">An Azure AD subscription</span></span>
- <span data-ttu-id="aa050-113">Un abonnement à 10,000ft Plans pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="aa050-113">A 10,000ft Plans single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="aa050-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="aa050-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="aa050-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="aa050-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aa050-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="aa050-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="aa050-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez bénéficier de [l’offre d’essai](https://azure.microsoft.com/pricing/free-trial/) d’un mois.</span><span class="sxs-lookup"><span data-stu-id="aa050-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="aa050-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="aa050-118">Scenario description</span></span>
<span data-ttu-id="aa050-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="aa050-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aa050-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="aa050-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aa050-121">Ajout de 10 000 pieds Plans à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="aa050-121">Adding 10,000ft Plans from hello gallery</span></span>
2. <span data-ttu-id="aa050-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa050-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-10000ft-plans-from-hello-gallery"></a><span data-ttu-id="aa050-123">Ajout de 10 000 pieds Plans à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="aa050-123">Adding 10,000ft Plans from hello gallery</span></span>
<span data-ttu-id="aa050-124">tooconfigure hello intégration des Plans de 10 000 pieds dans Azure AD, vous devez tooadd 10 000 pieds Plans à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="aa050-124">tooconfigure hello integration of 10,000ft Plans into Azure AD, you need tooadd 10,000ft Plans from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="aa050-125">**tooadd 10 000 pieds Plans à partir de la galerie de hello, procédez de hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="aa050-125">**tooadd 10,000ft Plans from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa050-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="aa050-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="aa050-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="aa050-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="aa050-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="aa050-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="aa050-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="aa050-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="aa050-133">Dans la zone de recherche de hello, tapez **10 000 pieds Plans**.</span><span class="sxs-lookup"><span data-stu-id="aa050-133">In hello search box, type **10,000ft Plans**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_search.png)

5. <span data-ttu-id="aa050-135">Dans le volet de résultats hello, sélectionnez **10 000 pieds Plans**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="aa050-135">In hello results panel, select **10,000ft Plans**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="aa050-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa050-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="aa050-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec 10,000ft Plans avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="aa050-138">In this section, you configure and test Azure AD single sign-on with 10,000ft Plans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="aa050-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans les Plans de 10 000 ft est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa050-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 10,000ft Plans is tooa user in Azure AD.</span></span> <span data-ttu-id="aa050-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et l’utilisateur dans les 10 000 pieds hello Plans doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="aa050-140">In other words, a link relationship between an Azure AD user and hello related user in 10,000ft Plans needs toobe established.</span></span>

<span data-ttu-id="aa050-141">Dans les Plans de ft de 10 000, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="aa050-141">In 10,000ft Plans, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="aa050-142">tooconfigure et test Azure AD l’authentification unique avec des Plans de ft de 10 000, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="aa050-142">tooconfigure and test Azure AD single sign-on with 10,000ft Plans, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="aa050-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="aa050-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="aa050-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aa050-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aa050-145">**[Création d’un 10 000 pieds Plans de test utilisateur](#creating-a-10000ft-plans-test-user)**  -toohave un homologue de Britta Simon dans 10 000 pieds Plans qui est lié à la représentation sous forme de toohello Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="aa050-145">**[Creating a 10,000ft Plans test user](#creating-a-10000ft-plans-test-user)** - toohave a counterpart of Britta Simon in 10,000ft Plans that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="aa050-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="aa050-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aa050-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="aa050-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="aa050-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa050-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="aa050-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Plans de ft de 10 000.</span><span class="sxs-lookup"><span data-stu-id="aa050-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 10,000ft Plans application.</span></span>

<span data-ttu-id="aa050-150">**tooconfigure Azure AD authentification unique avec des Plans de ft de 10 000, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="aa050-150">**tooconfigure Azure AD single sign-on with 10,000ft Plans, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa050-151">Bonjour portail Azure, sur hello **10 000 pieds Plans** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="aa050-151">In hello Azure portal, on hello **10,000ft Plans** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="aa050-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="aa050-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_samlbase.png)

3. <span data-ttu-id="aa050-155">Sur hello **10 000 ft Plans de domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="aa050-155">On hello **10,000ft Plans Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_url.png)

    <span data-ttu-id="aa050-157">a.</span><span class="sxs-lookup"><span data-stu-id="aa050-157">a.</span></span> <span data-ttu-id="aa050-158">Bonjour **URL de connexion** zone de texte, tapez l’URL hello :`https://app.10000ft.com`</span><span class="sxs-lookup"><span data-stu-id="aa050-158">In hello **Sign-on URL** textbox, type hello URL: `https://app.10000ft.com`</span></span>

    <span data-ttu-id="aa050-159">b.</span><span class="sxs-lookup"><span data-stu-id="aa050-159">b.</span></span> <span data-ttu-id="aa050-160">Bonjour **identificateur** zone de texte, tapez l’URL hello :`https://app.10000ft.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="aa050-160">In hello **Identifier** textbox, type hello URL: `https://app.10000ft.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="aa050-161">Hello valeur pour **identificateur** est différente si vous avez un domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="aa050-161">hello value for **Identifier** is different if you have a custom domain.</span></span> <span data-ttu-id="aa050-162">Contact [équipe de support technique de Plans de 10 000 pieds](https://www.10000ft.com/plans/support) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="aa050-162">Contact [10,000ft Plans support team](https://www.10000ft.com/plans/support) tooget this value.</span></span> 
 
4. <span data-ttu-id="aa050-163">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Raw)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="aa050-163">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_certificate.png) 

5. <span data-ttu-id="aa050-165">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="aa050-165">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="aa050-167">Sur hello **10 000 pieds Plans de Configuration** , cliquez sur **configurer les Plans de 10 000 pieds** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="aa050-167">On hello **10,000ft Plans Configuration** section, click **Configure 10,000ft Plans** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="aa050-168">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="aa050-168">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_configure.png) 

7. <span data-ttu-id="aa050-170">tooconfigure l’authentification unique sur **10 000 pieds Plans** côté, vous devez hello toosend téléchargé **Certificate(Raw), l’URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** trop[ équipe de support technique de Plans de 10 000 pieds](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="aa050-170">tooconfigure single sign-on on **10,000ft Plans** side, you need toosend hello downloaded **Certificate(Raw), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

> [!TIP]
> <span data-ttu-id="aa050-171">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="aa050-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="aa050-172">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="aa050-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="aa050-173">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="aa050-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="aa050-174">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa050-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="aa050-175">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="aa050-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="aa050-177">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="aa050-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa050-178">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="aa050-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aa050-180">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="aa050-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aa050-182">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="aa050-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aa050-184">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="aa050-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="aa050-186">a.</span><span class="sxs-lookup"><span data-stu-id="aa050-186">a.</span></span> <span data-ttu-id="aa050-187">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="aa050-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="aa050-188">b.</span><span class="sxs-lookup"><span data-stu-id="aa050-188">b.</span></span> <span data-ttu-id="aa050-189">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="aa050-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="aa050-190">c.</span><span class="sxs-lookup"><span data-stu-id="aa050-190">c.</span></span> <span data-ttu-id="aa050-191">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="aa050-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="aa050-192">d.</span><span class="sxs-lookup"><span data-stu-id="aa050-192">d.</span></span> <span data-ttu-id="aa050-193">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="aa050-193">Click **Create**.</span></span>
 
### <a name="creating-a-10000ft-plans-test-user"></a><span data-ttu-id="aa050-194">Création d’un utilisateur de test 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="aa050-194">Creating a 10,000ft Plans test user</span></span>

<span data-ttu-id="aa050-195">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans les Plans de ft de 10 000.</span><span class="sxs-lookup"><span data-stu-id="aa050-195">hello objective of this section is toocreate a user called Britta Simon in 10,000ft Plans.</span></span> <span data-ttu-id="aa050-196">10,000ft Plans prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="aa050-196">10,000ft Plans supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="aa050-197">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="aa050-197">There is no action item for you in this section.</span></span> <span data-ttu-id="aa050-198">Un nouvel utilisateur est créé au cours d’une tooaccess de tentative de 10 000 ft Plans s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="aa050-198">A new user is created during an attempt tooaccess 10,000ft Plans if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="aa050-199">Si vous devez manuellement toocreate un utilisateur, vous devez toocontact hello [équipe de support technique de Plans de 10 000 pieds](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="aa050-199">If you need toocreate a user manually, you need toocontact hello [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="aa050-200">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa050-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="aa050-201">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès too10, 000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="aa050-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too10,000ft Plans.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="aa050-203">**tooassign Britta Simon too10, Plans de texte intégral 000, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="aa050-203">**tooassign Britta Simon too10,000ft Plans, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa050-204">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="aa050-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="aa050-206">Dans la liste des applications hello, sélectionnez **10 000 pieds Plans**.</span><span class="sxs-lookup"><span data-stu-id="aa050-206">In hello applications list, select **10,000ft Plans**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_app.png) 

3. <span data-ttu-id="aa050-208">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="aa050-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="aa050-210">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="aa050-210">Click **Add** button.</span></span> <span data-ttu-id="aa050-211">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="aa050-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="aa050-213">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="aa050-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="aa050-214">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="aa050-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aa050-215">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="aa050-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="aa050-216">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="aa050-216">Testing single sign-on</span></span>

<span data-ttu-id="aa050-217">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="aa050-217">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="aa050-218">Lorsque vous cliquez sur hello 10 000 ft Plans vignette Bonjour volet d’accès, vous devez obtenir l’application de Plans tooyour automatiquement signé sur 10 000 ft.</span><span class="sxs-lookup"><span data-stu-id="aa050-218">When you click hello 10,000ft Plans tile in hello Access Panel, you should get automatically signed-on tooyour 10,000ft Plans application.</span></span>
 
## <a name="additional-resources"></a><span data-ttu-id="aa050-219">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="aa050-219">Additional resources</span></span>

* [<span data-ttu-id="aa050-220">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aa050-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aa050-221">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="aa050-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_203.png

