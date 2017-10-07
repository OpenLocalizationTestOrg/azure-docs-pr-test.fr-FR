---
title: "Didacticiel : Intégration d’Azure Active Directory à Citrix GoToMeeting | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7d7897f6-b88e-4dd5-8f3a-e612337b1413
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 46a5da7504806202a5ec29f73c504e772c61bc2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-gotomeeting"></a><span data-ttu-id="a27d9-103">Didacticiel : Intégration d’Azure Active Directory à Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="a27d9-103">Tutorial: Azure Active Directory integration with Citrix GoToMeeting</span></span>

<span data-ttu-id="a27d9-104">Dans ce didacticiel, vous apprendrez comment toointegrate Citrix GoToMeeting avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a27d9-104">In this tutorial, you learn how toointegrate Citrix GoToMeeting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a27d9-105">Intégration de Citrix GoToMeeting à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a27d9-105">Integrating Citrix GoToMeeting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a27d9-106">Vous pouvez contrôler dans Azure AD qui a accès tooCitrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="a27d9-106">You can control in Azure AD who has access tooCitrix GoToMeeting</span></span>
- <span data-ttu-id="a27d9-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooCitrix GoToMeeting (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="a27d9-107">You can enable your users tooautomatically get signed-on tooCitrix GoToMeeting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a27d9-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="a27d9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a27d9-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a27d9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a27d9-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a27d9-110">Prerequisites</span></span>

<span data-ttu-id="a27d9-111">tooconfigure intégration d’Azure AD avec Citrix GoToMeeting, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a27d9-111">tooconfigure Azure AD integration with Citrix GoToMeeting, you need hello following items:</span></span>

- <span data-ttu-id="a27d9-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="a27d9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a27d9-113">Un abonnement Citrix GoToMeeting pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="a27d9-113">A Citrix GoToMeeting single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a27d9-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a27d9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a27d9-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="a27d9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a27d9-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a27d9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a27d9-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a27d9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a27d9-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="a27d9-118">Scenario description</span></span>
<span data-ttu-id="a27d9-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a27d9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a27d9-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="a27d9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a27d9-121">Ajout de Citrix GoToMeeting à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a27d9-121">Adding Citrix GoToMeeting from hello gallery</span></span>
2. <span data-ttu-id="a27d9-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a27d9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-citrix-gotomeeting-from-hello-gallery"></a><span data-ttu-id="a27d9-123">Ajout de Citrix GoToMeeting à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a27d9-123">Adding Citrix GoToMeeting from hello gallery</span></span>
<span data-ttu-id="a27d9-124">tooconfigure hello intégration de Citrix GoToMeeting dans Azure AD, vous devez tooadd Citrix GoToMeeting à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="a27d9-124">tooconfigure hello integration of Citrix GoToMeeting into Azure AD, you need tooadd Citrix GoToMeeting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a27d9-125">**tooadd Citrix GoToMeeting à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a27d9-125">**tooadd Citrix GoToMeeting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a27d9-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a27d9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a27d9-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="a27d9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a27d9-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a27d9-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a27d9-131">Cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="a27d9-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a27d9-133">Dans la zone de recherche de hello, tapez **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="a27d9-133">In hello search box, type **Citrix GoToMeeting**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_search.png)

5. <span data-ttu-id="a27d9-135">Dans le volet de résultats hello, sélectionnez **Citrix GoToMeeting**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a27d9-135">In hello results panel, select **Citrix GoToMeeting**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a27d9-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a27d9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a27d9-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Citrix GoToMeeting avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="a27d9-138">In this section, you configure and test Azure AD single sign-on with Citrix GoToMeeting based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a27d9-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Citrix GoToMeeting est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a27d9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Citrix GoToMeeting is tooa user in Azure AD.</span></span> <span data-ttu-id="a27d9-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Citrix GoToMeeting doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="a27d9-140">In other words, a link relationship between an Azure AD user and hello related user in Citrix GoToMeeting needs toobe established.</span></span>

<span data-ttu-id="a27d9-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="a27d9-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Citrix GoToMeeting.</span></span>

<span data-ttu-id="a27d9-142">tooconfigure et test Azure AD l’authentification unique avec Citrix GoToMeeting, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="a27d9-142">tooconfigure and test Azure AD single sign-on with Citrix GoToMeeting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a27d9-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a27d9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a27d9-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a27d9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a27d9-145">**[Création d’un utilisateur de test de Citrix GoToMeeting](#creating-a-citrix-gotomeeting-test-user)**  -toohave un équivalent de Britta Simon dans Citrix GoToMeeting qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a27d9-145">**[Creating a Citrix GoToMeeting test user](#creating-a-citrix-gotomeeting-test-user)** - toohave a counterpart of Britta Simon in Citrix GoToMeeting that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a27d9-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a27d9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a27d9-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="a27d9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a27d9-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a27d9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a27d9-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="a27d9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Citrix GoToMeeting application.</span></span>

<span data-ttu-id="a27d9-150">**tooconfigure Azure AD single sign-on avec Citrix GoToMeeting, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a27d9-150">**tooconfigure Azure AD single sign-on with Citrix GoToMeeting, perform hello following steps:**</span></span>

1. <span data-ttu-id="a27d9-151">Bonjour portail Azure, sur hello **Citrix GoToMeeting** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a27d9-151">In hello Azure portal, on hello **Citrix GoToMeeting** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="a27d9-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a27d9-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_samlbase.png)

3. <span data-ttu-id="a27d9-155">Sur hello **Citrix GoToMeeting domaine et les URL** section, sans nécessité tooperform toutes les étapes.</span><span class="sxs-lookup"><span data-stu-id="a27d9-155">On hello **Citrix GoToMeeting Domain and URLs** section, no need tooperform any steps.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_url.png)


3. <span data-ttu-id="a27d9-157">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a27d9-157">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_certificate.png) 

4. <span data-ttu-id="a27d9-159">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="a27d9-159">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_400.png)
    
5. <span data-ttu-id="a27d9-161">Dans hello section de Configuration de Citrix GoToMeeting SAML, cliquez sur fenêtre Configurer de Citrix GoToMeeting SAML tooopen configurer l’authentification.</span><span class="sxs-lookup"><span data-stu-id="a27d9-161">On hello Citrix GoToMeeting SAML Configuration section, click Configure Citrix GoToMeeting SAML tooopen Configure sign-on window.</span></span> <span data-ttu-id="a27d9-162">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="a27d9-162">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

6. <span data-ttu-id="a27d9-163">Dans une autre fenêtre de navigateur, connectez-vous tooyour [Citrix organisation centre](https://account.citrixonline.com/organization/administration/).</span><span class="sxs-lookup"><span data-stu-id="a27d9-163">In a different browser window, log in tooyour [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span></span>

7. <span data-ttu-id="a27d9-164">Cliquez sur hello **fournisseur d’identité** onglet, puis effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a27d9-164">Click hello **Identity Provider** tab, and then perform hello following steps:</span></span>  
   
    <span data-ttu-id="a27d9-165">![Configuration SAML](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "Configuration SAML")</span><span class="sxs-lookup"><span data-stu-id="a27d9-165">![SAML setup](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span></span>
   
    <span data-ttu-id="a27d9-166">a.</span><span class="sxs-lookup"><span data-stu-id="a27d9-166">a.</span></span> <span data-ttu-id="a27d9-167">Sélectionnez **Manual**</span><span class="sxs-lookup"><span data-stu-id="a27d9-167">Select **Manual**</span></span>

    <span data-ttu-id="a27d9-168">b.</span><span class="sxs-lookup"><span data-stu-id="a27d9-168">b.</span></span> <span data-ttu-id="a27d9-169">Bonjour portail Azure, sur hello **configurer l’authentification unique sur Citrix GoToMeeting** page de boîte de dialogue, hello de copie **SAML Sign-On URL du Service unique** valeur, puis collez-le dans hello **page de connexion URL** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="a27d9-169">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Sign-in page URL** textbox.</span></span> 

    <span data-ttu-id="a27d9-170">c.</span><span class="sxs-lookup"><span data-stu-id="a27d9-170">c.</span></span> <span data-ttu-id="a27d9-171">Bonjour portail Azure, sur hello **configurer l’authentification unique sur Citrix GoToMeeting** page de boîte de dialogue, hello de copie **URL de déconnexion** valeur, puis collez-le dans hello **URL de la page de déconnexion**zone de texte.</span><span class="sxs-lookup"><span data-stu-id="a27d9-171">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **Sign-Out URL** value, and then paste it into hello **Sign-out page URL** textbox.</span></span>

    <span data-ttu-id="a27d9-172">d.</span><span class="sxs-lookup"><span data-stu-id="a27d9-172">d.</span></span> <span data-ttu-id="a27d9-173">Bonjour portail Azure, sur hello **configurer l’authentification unique sur Citrix GoToMeeting** page de boîte de dialogue, hello de copie **ID d’entité SAML** valeur, puis collez-le dans hello **Entity ID fournisseur d’identité**  zone de texte.</span><span class="sxs-lookup"><span data-stu-id="a27d9-173">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **SAML Entity ID** value, and then paste it into hello **Identity Provider Entity ID** textbox.</span></span>

    <span data-ttu-id="a27d9-174">e.</span><span class="sxs-lookup"><span data-stu-id="a27d9-174">e.</span></span> <span data-ttu-id="a27d9-175">tooupload votre certificat téléchargé, cliquez sur **télécharger un certificat**.</span><span class="sxs-lookup"><span data-stu-id="a27d9-175">tooupload your downloaded certificate, click **Upload Certificate**.</span></span>

    <span data-ttu-id="a27d9-176">f.</span><span class="sxs-lookup"><span data-stu-id="a27d9-176">f.</span></span> <span data-ttu-id="a27d9-177">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a27d9-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a27d9-178">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="a27d9-178">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a27d9-179">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="a27d9-179">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a27d9-180">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a27d9-180">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a27d9-181">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a27d9-181">Creating an Azure AD test user</span></span>
<span data-ttu-id="a27d9-182">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="a27d9-182">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="a27d9-184">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a27d9-184">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a27d9-185">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a27d9-185">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a27d9-187">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a27d9-187">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a27d9-189">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="a27d9-189">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a27d9-191">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a27d9-191">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a27d9-193">a.</span><span class="sxs-lookup"><span data-stu-id="a27d9-193">a.</span></span> <span data-ttu-id="a27d9-194">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a27d9-194">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a27d9-195">b.</span><span class="sxs-lookup"><span data-stu-id="a27d9-195">b.</span></span> <span data-ttu-id="a27d9-196">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a27d9-196">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a27d9-197">c.</span><span class="sxs-lookup"><span data-stu-id="a27d9-197">c.</span></span> <span data-ttu-id="a27d9-198">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a27d9-198">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a27d9-199">d.</span><span class="sxs-lookup"><span data-stu-id="a27d9-199">d.</span></span> <span data-ttu-id="a27d9-200">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="a27d9-200">Click **Create**.</span></span>
 
### <a name="creating-a-citrix-gotomeeting-test-user"></a><span data-ttu-id="a27d9-201">Création d’un utilisateur de test Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="a27d9-201">Creating a Citrix GoToMeeting test user</span></span>

<span data-ttu-id="a27d9-202">Dans cette section, un utilisateur appelé Britta Simon est créé dans Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="a27d9-202">In this section, a user called Britta Simon is created in Citrix GoToMeeting.</span></span> <span data-ttu-id="a27d9-203">Citrix GoToMeeting prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="a27d9-203">Citrix GoToMeeting supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="a27d9-204">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="a27d9-204">There is no action item for you in this section.</span></span> <span data-ttu-id="a27d9-205">Si un utilisateur n’existe pas déjà dans Citrix GoToMeeting, un nouveau est créé lorsque vous essayez de tooaccess Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="a27d9-205">If a user doesn't already exist in Citrix GoToMeeting, a new one is created when you attempt tooaccess Citrix GoToMeeting.</span></span>

>[!Note]
><span data-ttu-id="a27d9-206">Si vous avez besoin de toocreate un utilisateur manuellement, contactez [équipe de support technique de Citrix GoToMeeting](https://care.citrixonline.com/gotomeeting)</span><span class="sxs-lookup"><span data-stu-id="a27d9-206">If you need toocreate a user manually, Contact [Citrix GoToMeeting support team](https://care.citrixonline.com/gotomeeting)</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a27d9-207">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a27d9-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a27d9-208">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooCitrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="a27d9-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCitrix GoToMeeting.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="a27d9-210">**tooassign Britta Simon tooCitrix GoToMeeting, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a27d9-210">**tooassign Britta Simon tooCitrix GoToMeeting, perform hello following steps:**</span></span>

1. <span data-ttu-id="a27d9-211">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a27d9-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="a27d9-213">Dans la liste des applications hello, sélectionnez **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="a27d9-213">In hello applications list, select **Citrix GoToMeeting**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_app.png) 

3. <span data-ttu-id="a27d9-215">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a27d9-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="a27d9-217">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a27d9-217">Click **Add** button.</span></span> <span data-ttu-id="a27d9-218">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a27d9-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="a27d9-220">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="a27d9-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a27d9-221">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a27d9-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a27d9-222">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a27d9-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a27d9-223">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a27d9-223">Testing single sign-on</span></span>

<span data-ttu-id="a27d9-224">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="a27d9-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a27d9-225">Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="a27d9-225">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="a27d9-226">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a27d9-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a27d9-227">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a27d9-227">Additional resources</span></span>

* [<span data-ttu-id="a27d9-228">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a27d9-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a27d9-229">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a27d9-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="a27d9-230">Configurer l’approvisionnement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="a27d9-230">Configure User Provisioning</span></span>](active-directory-saas-citrixgotomeeting-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_203.png

