---
title: "Didacticiel : intégration d’Azure Active Directory à Tidemark | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Tidemark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5cf80d4e-6e8b-48ec-81c8-27872af5e5d5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 4fffee30370d928ae8070a5904c58ba8a7a06343
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tidemark"></a><span data-ttu-id="aca5a-103">Didacticiel : Intégration d’Azure Active Directory à Tidemark</span><span class="sxs-lookup"><span data-stu-id="aca5a-103">Tutorial: Azure Active Directory integration with Tidemark</span></span>

<span data-ttu-id="aca5a-104">Dans ce didacticiel, vous apprendrez comment toointegrate Tidemark avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="aca5a-104">In this tutorial, you learn how toointegrate Tidemark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aca5a-105">Intégration Tidemark à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="aca5a-105">Integrating Tidemark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="aca5a-106">Vous pouvez contrôler dans Azure AD qui a accès tooTidemark</span><span class="sxs-lookup"><span data-stu-id="aca5a-106">You can control in Azure AD who has access tooTidemark</span></span>
- <span data-ttu-id="aca5a-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooTidemark (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="aca5a-107">You can enable your users tooautomatically get signed-on tooTidemark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="aca5a-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="aca5a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="aca5a-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aca5a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aca5a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="aca5a-110">Prerequisites</span></span>

<span data-ttu-id="aca5a-111">tooconfigure intégration d’Azure AD avec Tidemark, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="aca5a-111">tooconfigure Azure AD integration with Tidemark, you need hello following items:</span></span>

- <span data-ttu-id="aca5a-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="aca5a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="aca5a-113">Un abonnement Tidemark pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="aca5a-113">A Tidemark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="aca5a-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="aca5a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="aca5a-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="aca5a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aca5a-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="aca5a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="aca5a-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aca5a-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="aca5a-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="aca5a-118">Scenario description</span></span>
<span data-ttu-id="aca5a-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="aca5a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aca5a-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="aca5a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aca5a-121">Ajout de Tidemark à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="aca5a-121">Adding Tidemark from hello gallery</span></span>
2. <span data-ttu-id="aca5a-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="aca5a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tidemark-from-hello-gallery"></a><span data-ttu-id="aca5a-123">Ajout de Tidemark à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="aca5a-123">Adding Tidemark from hello gallery</span></span>
<span data-ttu-id="aca5a-124">intégration de hello tooconfigure de Tidemark dans Azure AD, vous devez tooadd Tidemark à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="aca5a-124">tooconfigure hello integration of Tidemark into Azure AD, you need tooadd Tidemark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="aca5a-125">**tooadd Tidemark à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="aca5a-125">**tooadd Tidemark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="aca5a-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="aca5a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="aca5a-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="aca5a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="aca5a-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="aca5a-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="aca5a-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="aca5a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="aca5a-133">Dans la zone de recherche de hello, tapez **Tidemark**.</span><span class="sxs-lookup"><span data-stu-id="aca5a-133">In hello search box, type **Tidemark**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_search.png)

5. <span data-ttu-id="aca5a-135">Dans le volet de résultats hello, sélectionnez **Tidemark**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="aca5a-135">In hello results panel, select **Tidemark**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="aca5a-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="aca5a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="aca5a-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Tidemark, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="aca5a-138">In this section, you configure and test Azure AD single sign-on with Tidemark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="aca5a-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Tidemark est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aca5a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tidemark is tooa user in Azure AD.</span></span> <span data-ttu-id="aca5a-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Tidemark doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="aca5a-140">In other words, a link relationship between an Azure AD user and hello related user in Tidemark needs toobe established.</span></span>

<span data-ttu-id="aca5a-141">Dans Tidemark, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="aca5a-141">In Tidemark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="aca5a-142">tooconfigure et test Azure AD l’authentification unique avec Tidemark, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="aca5a-142">tooconfigure and test Azure AD single sign-on with Tidemark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="aca5a-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="aca5a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="aca5a-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aca5a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aca5a-145">**[Création d’un utilisateur de test Tidemark](#creating-a-tidemark-test-user)**  -toohave un équivalent de Britta Simon dans Tidemark est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="aca5a-145">**[Creating a Tidemark test user](#creating-a-tidemark-test-user)** - toohave a counterpart of Britta Simon in Tidemark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="aca5a-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="aca5a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aca5a-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="aca5a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="aca5a-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="aca5a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="aca5a-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Tidemark.</span><span class="sxs-lookup"><span data-stu-id="aca5a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tidemark application.</span></span>

<span data-ttu-id="aca5a-150">**tooconfigure Azure AD single sign-on avec Tidemark, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="aca5a-150">**tooconfigure Azure AD single sign-on with Tidemark, perform hello following steps:**</span></span>

1. <span data-ttu-id="aca5a-151">Bonjour portail Azure, sur hello **Tidemark** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="aca5a-151">In hello Azure portal, on hello **Tidemark** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="aca5a-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="aca5a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_samlbase.png)

3. <span data-ttu-id="aca5a-155">Sur hello **Tidemark domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="aca5a-155">On hello **Tidemark Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_url.png)

    <span data-ttu-id="aca5a-157">a.</span><span class="sxs-lookup"><span data-stu-id="aca5a-157">a.</span></span> <span data-ttu-id="aca5a-158">Bonjour **URL de connexion** modèles de zone de texte, tapez une URL à l’aide de hello suivant :</span><span class="sxs-lookup"><span data-stu-id="aca5a-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
    | |
    |--|
    | `https://<subdomain>.tidemark.com/login` |
    | `https://<subdomain>.tidemark.net/login` |

    <span data-ttu-id="aca5a-159">b.</span><span class="sxs-lookup"><span data-stu-id="aca5a-159">b.</span></span> <span data-ttu-id="aca5a-160">Bonjour **identificateur** modèles de zone de texte, tapez une URL à l’aide de hello suivant :</span><span class="sxs-lookup"><span data-stu-id="aca5a-160">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
    | |
    |--|
    | `https://<subdomain>.tidemark.com/saml` |
    | `https://<subdomain>.tidemark.net/saml` |

    > [!NOTE] 
    > <span data-ttu-id="aca5a-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="aca5a-161">These values are not real.</span></span> <span data-ttu-id="aca5a-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="aca5a-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="aca5a-163">Contact [équipe de support Client de Tidemark](http://www.tidemark.com/contact-us) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="aca5a-163">Contact [Tidemark Client support team](http://www.tidemark.com/contact-us) tooget these values.</span></span> 
 
4. <span data-ttu-id="aca5a-164">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="aca5a-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_certificate.png) 

5. <span data-ttu-id="aca5a-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="aca5a-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tidemark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="aca5a-168">Sur hello **Tidemark Configuration** , cliquez sur **Tidemark de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="aca5a-168">On hello **Tidemark Configuration** section, click **Configure Tidemark** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="aca5a-169">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="aca5a-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_configure.png) 

7. <span data-ttu-id="aca5a-171">tooconfigure l’authentification unique sur **Tidemark** côté, vous devez hello toosend téléchargé **Certificate(Base64), ID d’entité SAML, URL de déconnexion et SAML Sign-On URL du Service unique** trop[Tidemark l’équipe de support](http://www.tidemark.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="aca5a-171">tooconfigure single sign-on on **Tidemark** side, you need toosend hello downloaded **Certificate(Base64), SAML Entity ID, Sign-Out URL and SAML Single Sign-On Service URL** too[Tidemark support team](http://www.tidemark.com/contact-us).</span></span> <span data-ttu-id="aca5a-172">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="aca5a-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="aca5a-173">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="aca5a-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="aca5a-174">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="aca5a-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="aca5a-175">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="aca5a-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="aca5a-176">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="aca5a-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="aca5a-177">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="aca5a-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="aca5a-179">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="aca5a-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="aca5a-180">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="aca5a-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tidemark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aca5a-182">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="aca5a-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tidemark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aca5a-184">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="aca5a-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tidemark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aca5a-186">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="aca5a-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tidemark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="aca5a-188">a.</span><span class="sxs-lookup"><span data-stu-id="aca5a-188">a.</span></span> <span data-ttu-id="aca5a-189">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="aca5a-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="aca5a-190">b.</span><span class="sxs-lookup"><span data-stu-id="aca5a-190">b.</span></span> <span data-ttu-id="aca5a-191">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="aca5a-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="aca5a-192">c.</span><span class="sxs-lookup"><span data-stu-id="aca5a-192">c.</span></span> <span data-ttu-id="aca5a-193">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="aca5a-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="aca5a-194">d.</span><span class="sxs-lookup"><span data-stu-id="aca5a-194">d.</span></span> <span data-ttu-id="aca5a-195">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="aca5a-195">Click **Create**.</span></span>
 
### <a name="creating-a-tidemark-test-user"></a><span data-ttu-id="aca5a-196">Création d’un utilisateur de test Tidemark</span><span class="sxs-lookup"><span data-stu-id="aca5a-196">Creating a Tidemark test user</span></span>

<span data-ttu-id="aca5a-197">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Tidemark.</span><span class="sxs-lookup"><span data-stu-id="aca5a-197">hello objective of this section is toocreate a user called Britta Simon in Tidemark.</span></span> <span data-ttu-id="aca5a-198">Collaborez avec [équipe de support Tidemark](http://www.tidemark.com/contact-us) utilisateurs hello tooadd hello compte de Tidemark.</span><span class="sxs-lookup"><span data-stu-id="aca5a-198">Please work with [Tidemark support team](http://www.tidemark.com/contact-us) tooadd hello users in hello Tidemark account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="aca5a-199">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="aca5a-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="aca5a-200">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooTidemark.</span><span class="sxs-lookup"><span data-stu-id="aca5a-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTidemark.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="aca5a-202">**tooassign Britta Simon tooTidemark, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="aca5a-202">**tooassign Britta Simon tooTidemark, perform hello following steps:**</span></span>

1. <span data-ttu-id="aca5a-203">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="aca5a-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="aca5a-205">Dans la liste des applications hello, sélectionnez **Tidemark**.</span><span class="sxs-lookup"><span data-stu-id="aca5a-205">In hello applications list, select **Tidemark**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_app.png) 

3. <span data-ttu-id="aca5a-207">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="aca5a-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="aca5a-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="aca5a-209">Click **Add** button.</span></span> <span data-ttu-id="aca5a-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="aca5a-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="aca5a-212">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="aca5a-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="aca5a-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="aca5a-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aca5a-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="aca5a-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="aca5a-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="aca5a-215">Testing single sign-on</span></span>

<span data-ttu-id="aca5a-216">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="aca5a-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="aca5a-217">Lorsque vous cliquez sur mosaïque Tidemark hello hello volet d’accès, vous devez obtenir l’application de Tidemark automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="aca5a-217">When you click hello Tidemark tile in hello Access Panel, you should get automatically signed-on tooyour Tidemark application.</span></span>
<span data-ttu-id="aca5a-218">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="aca5a-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="aca5a-219">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="aca5a-219">Additional resources</span></span>

* [<span data-ttu-id="aca5a-220">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aca5a-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aca5a-221">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="aca5a-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_203.png

