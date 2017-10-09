---
title: "Didacticiel : Intégration d’Azure Active Directory à Weekdone | Microsoft Azure"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Weekdone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 34921f9a-5637-4420-ab4c-9beb34421909
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f997f1b49ff1aa0659a2409fdd945c6f96413b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-weekdone"></a><span data-ttu-id="58fd9-103">Didacticiel : Intégration d’Azure Active Directory à Weekdone</span><span class="sxs-lookup"><span data-stu-id="58fd9-103">Tutorial: Azure Active Directory integration with Weekdone</span></span>

<span data-ttu-id="58fd9-104">Dans ce didacticiel, vous apprendrez comment toointegrate Weekdone avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="58fd9-104">In this tutorial, you learn how toointegrate Weekdone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="58fd9-105">Intégration Weekdone à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="58fd9-105">Integrating Weekdone with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="58fd9-106">Vous pouvez contrôler dans Azure AD qui a accès tooWeekdone</span><span class="sxs-lookup"><span data-stu-id="58fd9-106">You can control in Azure AD who has access tooWeekdone</span></span>
- <span data-ttu-id="58fd9-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooWeekdone (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="58fd9-107">You can enable your users tooautomatically get signed-on tooWeekdone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="58fd9-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="58fd9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="58fd9-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="58fd9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58fd9-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="58fd9-110">Prerequisites</span></span>

<span data-ttu-id="58fd9-111">tooconfigure intégration d’Azure AD avec Weekdone, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="58fd9-111">tooconfigure Azure AD integration with Weekdone, you need hello following items:</span></span>

- <span data-ttu-id="58fd9-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="58fd9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="58fd9-113">Un abonnement Weekdone pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="58fd9-113">A Weekdone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="58fd9-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="58fd9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="58fd9-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="58fd9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="58fd9-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="58fd9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="58fd9-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="58fd9-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="58fd9-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="58fd9-118">Scenario description</span></span>
<span data-ttu-id="58fd9-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="58fd9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="58fd9-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="58fd9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="58fd9-121">Ajout de Weekdone à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="58fd9-121">Adding Weekdone from hello gallery</span></span>
2. <span data-ttu-id="58fd9-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="58fd9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-weekdone-from-hello-gallery"></a><span data-ttu-id="58fd9-123">Ajout de Weekdone à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="58fd9-123">Adding Weekdone from hello gallery</span></span>
<span data-ttu-id="58fd9-124">intégration de hello tooconfigure de Weekdone dans Azure AD, vous devez tooadd Weekdone à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="58fd9-124">tooconfigure hello integration of Weekdone into Azure AD, you need tooadd Weekdone from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="58fd9-125">**tooadd Weekdone à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="58fd9-125">**tooadd Weekdone from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="58fd9-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="58fd9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="58fd9-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="58fd9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="58fd9-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="58fd9-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="58fd9-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="58fd9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="58fd9-133">Dans la zone de recherche de hello, tapez **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="58fd9-133">In hello search box, type **Weekdone**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_search.png)

5. <span data-ttu-id="58fd9-135">Dans le volet de résultats hello, sélectionnez **Weekdone**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="58fd9-135">In hello results panel, select **Weekdone**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="58fd9-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="58fd9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="58fd9-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Weekdone avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="58fd9-138">In this section, you configure and test Azure AD single sign-on with Weekdone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="58fd9-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Weekdone est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="58fd9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Weekdone is tooa user in Azure AD.</span></span> <span data-ttu-id="58fd9-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Weekdone doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="58fd9-140">In other words, a link relationship between an Azure AD user and hello related user in Weekdone needs toobe established.</span></span>

<span data-ttu-id="58fd9-141">Dans Weekdone, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="58fd9-141">In Weekdone, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="58fd9-142">tooconfigure et test Azure AD l’authentification unique avec Weekdone, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="58fd9-142">tooconfigure and test Azure AD single sign-on with Weekdone, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="58fd9-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="58fd9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="58fd9-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="58fd9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="58fd9-145">**[Création d’un utilisateur de test Weekdone](#creating-a-weekdone-test-user)**  -toohave un équivalent de Britta Simon dans Weekdone est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="58fd9-145">**[Creating a Weekdone test user](#creating-a-weekdone-test-user)** - toohave a counterpart of Britta Simon in Weekdone that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="58fd9-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="58fd9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="58fd9-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="58fd9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="58fd9-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="58fd9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="58fd9-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Weekdone.</span><span class="sxs-lookup"><span data-stu-id="58fd9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Weekdone application.</span></span>

<span data-ttu-id="58fd9-150">**tooconfigure Azure AD single sign-on avec Weekdone, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="58fd9-150">**tooconfigure Azure AD single sign-on with Weekdone, perform hello following steps:**</span></span>

1. <span data-ttu-id="58fd9-151">Bonjour portail Azure, sur hello **Weekdone** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="58fd9-151">In hello Azure portal, on hello **Weekdone** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="58fd9-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="58fd9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_samlbase.png)

3. <span data-ttu-id="58fd9-155">Sur hello **Weekdone domaine et les URL** section, si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="58fd9-155">On hello **Weekdone Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url1.png)

    <span data-ttu-id="58fd9-157">a.</span><span class="sxs-lookup"><span data-stu-id="58fd9-157">a.</span></span> <span data-ttu-id="58fd9-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="58fd9-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

    <span data-ttu-id="58fd9-159">b.</span><span class="sxs-lookup"><span data-stu-id="58fd9-159">b.</span></span> <span data-ttu-id="58fd9-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="58fd9-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

4. <span data-ttu-id="58fd9-161">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="58fd9-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="58fd9-162">Si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="58fd9-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url2.png)

    <span data-ttu-id="58fd9-164">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="58fd9-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="58fd9-165">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="58fd9-165">These values are not real.</span></span> <span data-ttu-id="58fd9-166">Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="58fd9-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="58fd9-167">Contact [équipe de support Client de Weekdone](mailto:hello@weekdone.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="58fd9-167">Contact [Weekdone Client support team](mailto:hello@weekdone.com) tooget these values.</span></span> 

5. <span data-ttu-id="58fd9-168">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="58fd9-168">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_certificate.png) 

6. <span data-ttu-id="58fd9-170">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="58fd9-170">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-weekdone-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="58fd9-172">Sur hello **Weekdone Configuration** , cliquez sur **Weekdone de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="58fd9-172">On hello **Weekdone Configuration** section, click **Configure Weekdone** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="58fd9-173">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="58fd9-173">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_configure.png) 

8. <span data-ttu-id="58fd9-175">tooconfigure l’authentification unique sur **Weekdone** côté, vous devez hello toosend téléchargé **Metadata XML, l’URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** trop[prise en charge Weekdone équipe](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="58fd9-175">tooconfigure single sign-on on **Weekdone** side, you need toosend hello downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Weekdone support team](mailto:hello@weekdone.com).</span></span>

> [!TIP]
> <span data-ttu-id="58fd9-176">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="58fd9-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="58fd9-177">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="58fd9-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="58fd9-178">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="58fd9-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="58fd9-179">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="58fd9-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="58fd9-180">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="58fd9-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="58fd9-182">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="58fd9-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="58fd9-183">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="58fd9-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="58fd9-185">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="58fd9-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="58fd9-187">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="58fd9-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="58fd9-189">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="58fd9-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="58fd9-191">a.</span><span class="sxs-lookup"><span data-stu-id="58fd9-191">a.</span></span> <span data-ttu-id="58fd9-192">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="58fd9-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="58fd9-193">b.</span><span class="sxs-lookup"><span data-stu-id="58fd9-193">b.</span></span> <span data-ttu-id="58fd9-194">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="58fd9-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="58fd9-195">c.</span><span class="sxs-lookup"><span data-stu-id="58fd9-195">c.</span></span> <span data-ttu-id="58fd9-196">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="58fd9-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="58fd9-197">d.</span><span class="sxs-lookup"><span data-stu-id="58fd9-197">d.</span></span> <span data-ttu-id="58fd9-198">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="58fd9-198">Click **Create**.</span></span>
 
### <a name="creating-a-weekdone-test-user"></a><span data-ttu-id="58fd9-199">Création d’un utilisateur de test Weekdone</span><span class="sxs-lookup"><span data-stu-id="58fd9-199">Creating a Weekdone test user</span></span>

<span data-ttu-id="58fd9-200">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Weekdone.</span><span class="sxs-lookup"><span data-stu-id="58fd9-200">hello objective of this section is toocreate a user called Britta Simon in Weekdone.</span></span> <span data-ttu-id="58fd9-201">Weekdone prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="58fd9-201">Weekdone supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="58fd9-202">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="58fd9-202">There is no action item for you in this section.</span></span> <span data-ttu-id="58fd9-203">Un nouvel utilisateur est créé au cours d’une tentative de tooaccess Weekdone s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="58fd9-203">A new user is created during an attempt tooaccess Weekdone if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="58fd9-204">Si vous devez manuellement toocreate un utilisateur, vous devez toocontact hello [équipe de support Client de Weekdone](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="58fd9-204">If you need toocreate a user manually, you need toocontact hello [Weekdone Client support team](mailto:hello@weekdone.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="58fd9-205">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="58fd9-205">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="58fd9-206">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooWeekdone.</span><span class="sxs-lookup"><span data-stu-id="58fd9-206">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWeekdone.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="58fd9-208">**tooassign Britta Simon tooWeekdone, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="58fd9-208">**tooassign Britta Simon tooWeekdone, perform hello following steps:**</span></span>

1. <span data-ttu-id="58fd9-209">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="58fd9-209">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="58fd9-211">Dans la liste des applications hello, sélectionnez **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="58fd9-211">In hello applications list, select **Weekdone**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_app.png) 

3. <span data-ttu-id="58fd9-213">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="58fd9-213">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="58fd9-215">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="58fd9-215">Click **Add** button.</span></span> <span data-ttu-id="58fd9-216">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="58fd9-216">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="58fd9-218">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="58fd9-218">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="58fd9-219">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="58fd9-219">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="58fd9-220">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="58fd9-220">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="58fd9-221">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="58fd9-221">Testing single sign-on</span></span>

<span data-ttu-id="58fd9-222">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="58fd9-222">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="58fd9-223">Lorsque vous cliquez sur mosaïque Weekdone hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Weekdone application.</span><span class="sxs-lookup"><span data-stu-id="58fd9-223">When you click hello Weekdone tile in hello Access Panel, you should get automatically signed-on tooyour Weekdone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="58fd9-224">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="58fd9-224">Additional resources</span></span>

* [<span data-ttu-id="58fd9-225">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="58fd9-225">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="58fd9-226">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="58fd9-226">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_203.png

