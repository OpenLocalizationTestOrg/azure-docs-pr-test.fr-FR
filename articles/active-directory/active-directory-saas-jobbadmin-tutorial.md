---
title: "Didacticiel : Intégration d’Azure Active Directory à Jobbadmin | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Jobbadmin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c5208b0d-66a3-49ed-9aad-70d21f54aee0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 0796abd2934c0f94648b2c11e7fdf69304f835c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobbadmin"></a><span data-ttu-id="8f261-103">Didacticiel : Intégration d’Azure Active Directory à Jobbadmin</span><span class="sxs-lookup"><span data-stu-id="8f261-103">Tutorial: Azure Active Directory integration with Jobbadmin</span></span>

<span data-ttu-id="8f261-104">Dans ce didacticiel, vous apprendrez comment toointegrate Jobbadmin avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8f261-104">In this tutorial, you learn how toointegrate Jobbadmin with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8f261-105">Intégration Jobbadmin à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="8f261-105">Integrating Jobbadmin with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8f261-106">Vous pouvez contrôler dans Azure AD qui a accès tooJobbadmin</span><span class="sxs-lookup"><span data-stu-id="8f261-106">You can control in Azure AD who has access tooJobbadmin</span></span>
- <span data-ttu-id="8f261-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooJobbadmin (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f261-107">You can enable your users tooautomatically get signed-on tooJobbadmin (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8f261-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="8f261-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8f261-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8f261-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f261-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8f261-110">Prerequisites</span></span>

<span data-ttu-id="8f261-111">tooconfigure intégration d’Azure AD avec Jobbadmin, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8f261-111">tooconfigure Azure AD integration with Jobbadmin, you need hello following items:</span></span>

- <span data-ttu-id="8f261-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f261-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8f261-113">Un abonnement Jobbadmin pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="8f261-113">A Jobbadmin single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8f261-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="8f261-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8f261-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="8f261-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8f261-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8f261-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8f261-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8f261-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8f261-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="8f261-118">Scenario description</span></span>
<span data-ttu-id="8f261-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="8f261-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8f261-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="8f261-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8f261-121">Ajout de Jobbadmin à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="8f261-121">Adding Jobbadmin from hello gallery</span></span>
2. <span data-ttu-id="8f261-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f261-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobbadmin-from-hello-gallery"></a><span data-ttu-id="8f261-123">Ajout de Jobbadmin à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="8f261-123">Adding Jobbadmin from hello gallery</span></span>
<span data-ttu-id="8f261-124">intégration de hello tooconfigure de Jobbadmin dans Azure AD, vous devez tooadd Jobbadmin à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="8f261-124">tooconfigure hello integration of Jobbadmin into Azure AD, you need tooadd Jobbadmin from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8f261-125">**tooadd Jobbadmin à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8f261-125">**tooadd Jobbadmin from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f261-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="8f261-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8f261-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="8f261-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8f261-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8f261-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="8f261-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8f261-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="8f261-133">Dans la zone de recherche de hello, tapez **Jobbadmin**.</span><span class="sxs-lookup"><span data-stu-id="8f261-133">In hello search box, type **Jobbadmin**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_search.png)

5. <span data-ttu-id="8f261-135">Dans le volet de résultats hello, sélectionnez **Jobbadmin**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8f261-135">In hello results panel, select **Jobbadmin**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8f261-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f261-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8f261-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Jobbadmin à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="8f261-138">In this section, you configure and test Azure AD single sign-on with Jobbadmin based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8f261-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Jobbadmin est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f261-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jobbadmin is tooa user in Azure AD.</span></span> <span data-ttu-id="8f261-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Jobbadmin doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="8f261-140">In other words, a link relationship between an Azure AD user and hello related user in Jobbadmin needs toobe established.</span></span>

<span data-ttu-id="8f261-141">Dans Jobbadmin, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="8f261-141">In Jobbadmin, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8f261-142">tooconfigure et test Azure AD l’authentification unique avec Jobbadmin, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="8f261-142">tooconfigure and test Azure AD single sign-on with Jobbadmin, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8f261-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8f261-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8f261-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8f261-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8f261-145">**[Création d’un utilisateur de test Jobbadmin](#creating-a-jobbadmin-test-user)**  -toohave un équivalent de Britta Simon dans Jobbadmin est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8f261-145">**[Creating a Jobbadmin test user](#creating-a-jobbadmin-test-user)** - toohave a counterpart of Britta Simon in Jobbadmin that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8f261-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8f261-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8f261-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="8f261-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8f261-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f261-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8f261-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Jobbadmin.</span><span class="sxs-lookup"><span data-stu-id="8f261-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jobbadmin application.</span></span>

<span data-ttu-id="8f261-150">**tooconfigure Azure AD single sign-on avec Jobbadmin, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8f261-150">**tooconfigure Azure AD single sign-on with Jobbadmin, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f261-151">Bonjour portail Azure, sur hello **Jobbadmin** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="8f261-151">In hello Azure portal, on hello **Jobbadmin** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="8f261-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8f261-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_samlbase.png)

3. <span data-ttu-id="8f261-155">Sur hello **Jobbadmin domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8f261-155">On hello **Jobbadmin Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_url.png)

    <span data-ttu-id="8f261-157">a.</span><span class="sxs-lookup"><span data-stu-id="8f261-157">a.</span></span> <span data-ttu-id="8f261-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span><span class="sxs-lookup"><span data-stu-id="8f261-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span></span>

    <span data-ttu-id="8f261-159">b.</span><span class="sxs-lookup"><span data-stu-id="8f261-159">b.</span></span> <span data-ttu-id="8f261-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<instancename>.jobnorge.no`</span><span class="sxs-lookup"><span data-stu-id="8f261-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.jobnorge.no`</span></span>

    <span data-ttu-id="8f261-161">c.</span><span class="sxs-lookup"><span data-stu-id="8f261-161">c.</span></span> <span data-ttu-id="8f261-162">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span><span class="sxs-lookup"><span data-stu-id="8f261-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8f261-163">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="8f261-163">These values are not real.</span></span> <span data-ttu-id="8f261-164">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="8f261-164">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8f261-165">Contact [équipe de support Client de Jobbadmin](https://www.jobbnorge.no/om-oss/kontakt-oss) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="8f261-165">Contact [Jobbadmin Client support team](https://www.jobbnorge.no/om-oss/kontakt-oss) tooget these values.</span></span> 
 


4. <span data-ttu-id="8f261-166">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8f261-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_certificate.png) 

5. <span data-ttu-id="8f261-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="8f261-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8f261-170">tooconfigure l’authentification unique sur **Jobbadmin** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support Jobbadmin](https://www.jobbnorge.no/om-oss/kontakt-oss).</span><span class="sxs-lookup"><span data-stu-id="8f261-170">tooconfigure single sign-on on **Jobbadmin** side, you need toosend hello downloaded **Metadata XML** too[Jobbadmin support team](https://www.jobbnorge.no/om-oss/kontakt-oss).</span></span> <span data-ttu-id="8f261-171">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="8f261-171">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8f261-172">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="8f261-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8f261-173">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="8f261-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8f261-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8f261-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8f261-175">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f261-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="8f261-176">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="8f261-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="8f261-178">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8f261-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f261-179">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="8f261-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8f261-181">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8f261-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8f261-183">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="8f261-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8f261-185">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8f261-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8f261-187">a.</span><span class="sxs-lookup"><span data-stu-id="8f261-187">a.</span></span> <span data-ttu-id="8f261-188">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8f261-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8f261-189">b.</span><span class="sxs-lookup"><span data-stu-id="8f261-189">b.</span></span> <span data-ttu-id="8f261-190">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8f261-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8f261-191">c.</span><span class="sxs-lookup"><span data-stu-id="8f261-191">c.</span></span> <span data-ttu-id="8f261-192">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="8f261-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8f261-193">d.</span><span class="sxs-lookup"><span data-stu-id="8f261-193">d.</span></span> <span data-ttu-id="8f261-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="8f261-194">Click **Create**.</span></span>
 
### <a name="creating-a-jobbadmin-test-user"></a><span data-ttu-id="8f261-195">Création d’un utilisateur de test Jobbadmin</span><span class="sxs-lookup"><span data-stu-id="8f261-195">Creating a Jobbadmin test user</span></span>

<span data-ttu-id="8f261-196">tooenable Azure AD les utilisateurs toolog dans tooJobbadmin, vous devez les configurer dans Jobbadmin.</span><span class="sxs-lookup"><span data-stu-id="8f261-196">tooenable Azure AD users toolog in tooJobbadmin, they must be provisioned into Jobbadmin.</span></span>
 
<span data-ttu-id="8f261-197">Veuillez contacter [équipe de support Jobbadmin](https://www.jobbnorge.no/om-oss/kontakt-oss) tooget hello les utilisateurs sur leur côté.</span><span class="sxs-lookup"><span data-stu-id="8f261-197">Please contact [Jobbadmin support team](https://www.jobbnorge.no/om-oss/kontakt-oss) tooget hello users added on their side.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8f261-198">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f261-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8f261-199">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooJobbadmin.</span><span class="sxs-lookup"><span data-stu-id="8f261-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJobbadmin.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="8f261-201">**tooassign Britta Simon tooJobbadmin, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8f261-201">**tooassign Britta Simon tooJobbadmin, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f261-202">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8f261-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="8f261-204">Dans la liste des applications hello, sélectionnez **Jobbadmin**.</span><span class="sxs-lookup"><span data-stu-id="8f261-204">In hello applications list, select **Jobbadmin**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_app.png) 

3. <span data-ttu-id="8f261-206">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8f261-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="8f261-208">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8f261-208">Click **Add** button.</span></span> <span data-ttu-id="8f261-209">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8f261-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="8f261-211">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="8f261-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8f261-212">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8f261-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8f261-213">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8f261-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8f261-214">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="8f261-214">Testing single sign-on</span></span>

<span data-ttu-id="8f261-215">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="8f261-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8f261-216">Lorsque vous cliquez sur mosaïque Jobbadmin hello hello volet d’accès, vous devez obtenir la page de connexion de l’application de Jobbadmin.</span><span class="sxs-lookup"><span data-stu-id="8f261-216">When you click hello Jobbadmin tile in hello Access Panel, you should get login page of Jobbadmin application.</span></span>
<span data-ttu-id="8f261-217">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8f261-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8f261-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8f261-218">Additional resources</span></span>

* [<span data-ttu-id="8f261-219">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8f261-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8f261-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="8f261-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_203.png

