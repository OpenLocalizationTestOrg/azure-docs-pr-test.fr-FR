---
title: "Didacticiel : Intégration d’Azure Active Directory à Novatus | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Novatus."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2f13779-bdb7-4408-9738-be67ed3de4e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2017
ms.author: jeedes
ms.openlocfilehash: 7ff13f56f0f47d0c2667c9ca555801a7a06a2fa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-novatus"></a><span data-ttu-id="781c5-103">Didacticiel : Intégration d’Azure Active Directory à Novatus</span><span class="sxs-lookup"><span data-stu-id="781c5-103">Tutorial: Azure Active Directory integration with Novatus</span></span>

<span data-ttu-id="781c5-104">Dans ce didacticiel, vous apprendrez comment toointegrate Novatus avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="781c5-104">In this tutorial, you learn how toointegrate Novatus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="781c5-105">Intégration Novatus à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="781c5-105">Integrating Novatus with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="781c5-106">Vous pouvez contrôler dans Azure AD qui a accès tooNovatus</span><span class="sxs-lookup"><span data-stu-id="781c5-106">You can control in Azure AD who has access tooNovatus</span></span>
- <span data-ttu-id="781c5-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooNovatus (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="781c5-107">You can enable your users tooautomatically get signed-on tooNovatus (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="781c5-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="781c5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="781c5-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="781c5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="781c5-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="781c5-110">Prerequisites</span></span>

<span data-ttu-id="781c5-111">tooconfigure intégration d’Azure AD avec Novatus, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="781c5-111">tooconfigure Azure AD integration with Novatus, you need hello following items:</span></span>

- <span data-ttu-id="781c5-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="781c5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="781c5-113">Un abonnement Novatus pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="781c5-113">A Novatus single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="781c5-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="781c5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="781c5-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="781c5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="781c5-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="781c5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="781c5-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="781c5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="781c5-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="781c5-118">Scenario description</span></span>
<span data-ttu-id="781c5-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="781c5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="781c5-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="781c5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="781c5-121">Ajout de Novatus à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="781c5-121">Adding Novatus from hello gallery</span></span>
2. <span data-ttu-id="781c5-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="781c5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-novatus-from-hello-gallery"></a><span data-ttu-id="781c5-123">Ajout de Novatus à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="781c5-123">Adding Novatus from hello gallery</span></span>
<span data-ttu-id="781c5-124">intégration de hello tooconfigure de Novatus dans Azure AD, vous devez tooadd Novatus à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="781c5-124">tooconfigure hello integration of Novatus into Azure AD, you need tooadd Novatus from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="781c5-125">**tooadd Novatus à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="781c5-125">**tooadd Novatus from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="781c5-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="781c5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="781c5-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="781c5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="781c5-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="781c5-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="781c5-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="781c5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="781c5-133">Dans la zone de recherche de hello, tapez **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="781c5-133">In hello search box, type **Novatus**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_search.png)

5. <span data-ttu-id="781c5-135">Dans le volet de résultats hello, sélectionnez **Novatus**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="781c5-135">In hello results panel, select **Novatus**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="781c5-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="781c5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="781c5-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Novatus avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="781c5-138">In this section, you configure and test Azure AD single sign-on with Novatus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="781c5-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Novatus est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="781c5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Novatus is tooa user in Azure AD.</span></span> <span data-ttu-id="781c5-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Novatus doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="781c5-140">In other words, a link relationship between an Azure AD user and hello related user in Novatus needs toobe established.</span></span>

<span data-ttu-id="781c5-141">Dans Novatus, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="781c5-141">In Novatus, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="781c5-142">tooconfigure et test Azure AD l’authentification unique avec Novatus, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="781c5-142">tooconfigure and test Azure AD single sign-on with Novatus, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="781c5-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="781c5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="781c5-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="781c5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="781c5-145">**[Création d’un utilisateur de test Novatus](#creating-a-novatus-test-user)**  -toohave un équivalent de Britta Simon dans Novatus est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="781c5-145">**[Creating a Novatus test user](#creating-a-novatus-test-user)** - toohave a counterpart of Britta Simon in Novatus that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="781c5-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="781c5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="781c5-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="781c5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="781c5-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="781c5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="781c5-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Novatus.</span><span class="sxs-lookup"><span data-stu-id="781c5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Novatus application.</span></span>

<span data-ttu-id="781c5-150">**tooconfigure Azure AD single sign-on avec Novatus, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="781c5-150">**tooconfigure Azure AD single sign-on with Novatus, perform hello following steps:**</span></span>

1. <span data-ttu-id="781c5-151">Bonjour portail Azure, sur hello **Novatus** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="781c5-151">In hello Azure portal, on hello **Novatus** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="781c5-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="781c5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_samlbase.png)

3. <span data-ttu-id="781c5-155">Sur hello **Novatus domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="781c5-155">On hello **Novatus Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_url.png)

     <span data-ttu-id="781c5-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://sso.novatuscontracts.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="781c5-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sso.novatuscontracts.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="781c5-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="781c5-158">This value is not real.</span></span> <span data-ttu-id="781c5-159">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="781c5-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="781c5-160">Contact [équipe de support Client de Novatus](mailto:jvinci@novatusinc.com) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="781c5-160">Contact [Novatus Client support team](mailto:jvinci@novatusinc.com) tooget this value.</span></span> 
 


4. <span data-ttu-id="781c5-161">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="781c5-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_certificate.png) 

5. <span data-ttu-id="781c5-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="781c5-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-novatus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="781c5-165">Sur hello **Novatus Configuration** , cliquez sur **Novatus de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="781c5-165">On hello **Novatus Configuration** section, click **Configure Novatus** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="781c5-166">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="781c5-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_configure.png) 

7. <span data-ttu-id="781c5-168">tooget l’authentification unique configurée pour votre application, contactez votre [Novatus l’équipe de support](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="781c5-168">tooget SSO configured for your application, contact your [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> <span data-ttu-id="781c5-169">Attacher hello **téléchargé le certificat** hello de messagerie et le partage de tooyour fichier **les URL des métadonnées** (**URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique**) avec Équipe Novatus tooset configuration de SSO sur son côté.</span><span class="sxs-lookup"><span data-stu-id="781c5-169">Attach hello **downloaded certificate** file tooyour mail and share hello **metadata urls** (**Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL**) with Novatus team tooset up SSO on their side.</span></span>

> [!TIP]
> <span data-ttu-id="781c5-170">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="781c5-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="781c5-171">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="781c5-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="781c5-172">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="781c5-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="781c5-173">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="781c5-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="781c5-174">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="781c5-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="781c5-176">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="781c5-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="781c5-177">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="781c5-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="781c5-179">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="781c5-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="781c5-181">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="781c5-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="781c5-183">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="781c5-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="781c5-185">a.</span><span class="sxs-lookup"><span data-stu-id="781c5-185">a.</span></span> <span data-ttu-id="781c5-186">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="781c5-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="781c5-187">b.</span><span class="sxs-lookup"><span data-stu-id="781c5-187">b.</span></span> <span data-ttu-id="781c5-188">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="781c5-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="781c5-189">c.</span><span class="sxs-lookup"><span data-stu-id="781c5-189">c.</span></span> <span data-ttu-id="781c5-190">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="781c5-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="781c5-191">d.</span><span class="sxs-lookup"><span data-stu-id="781c5-191">d.</span></span> <span data-ttu-id="781c5-192">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="781c5-192">Click **Create**.</span></span>
 
### <a name="creating-a-novatus-test-user"></a><span data-ttu-id="781c5-193">Création d’un utilisateur de test Novatus</span><span class="sxs-lookup"><span data-stu-id="781c5-193">Creating a Novatus test user</span></span>

<span data-ttu-id="781c5-194">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Novatus.</span><span class="sxs-lookup"><span data-stu-id="781c5-194">hello objective of this section is toocreate a user called Britta Simon in Novatus.</span></span> <span data-ttu-id="781c5-195">Novatus prend en charge l’approvisionnement juste-à-temps, qui est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="781c5-195">Novatus supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="781c5-196">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="781c5-196">There is no action item for you in this section.</span></span> <span data-ttu-id="781c5-197">Un nouvel utilisateur s’affichera pendant une tentative de tooaccess Novatus s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="781c5-197">A new user will be created during an attempt tooaccess Novatus if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="781c5-198">Si vous devez manuellement toocreate un utilisateur, vous devez toocontact hello [Novatus l’équipe de support](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="781c5-198">If you need toocreate an user manually, you need toocontact hello [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="781c5-199">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="781c5-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="781c5-200">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooNovatus.</span><span class="sxs-lookup"><span data-stu-id="781c5-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNovatus.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="781c5-202">**tooassign Britta Simon tooNovatus, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="781c5-202">**tooassign Britta Simon tooNovatus, perform hello following steps:**</span></span>

1. <span data-ttu-id="781c5-203">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="781c5-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="781c5-205">Dans la liste des applications hello, sélectionnez **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="781c5-205">In hello applications list, select **Novatus**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_app.png) 

3. <span data-ttu-id="781c5-207">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="781c5-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="781c5-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="781c5-209">Click **Add** button.</span></span> <span data-ttu-id="781c5-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="781c5-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="781c5-212">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="781c5-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="781c5-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="781c5-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="781c5-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="781c5-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="781c5-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="781c5-215">Testing single sign-on</span></span>

<span data-ttu-id="781c5-216">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="781c5-216">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="781c5-217">Lorsque vous cliquez sur hello Novatus vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour Novatus application.</span><span class="sxs-lookup"><span data-stu-id="781c5-217">When you click hello Novatus tile in hello Access Panel, you should get automatically signed-on tooyour Novatus application.</span></span> <span data-ttu-id="781c5-218">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="781c5-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="781c5-219">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="781c5-219">Additional resources</span></span>

* [<span data-ttu-id="781c5-220">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="781c5-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="781c5-221">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="781c5-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_203.png

