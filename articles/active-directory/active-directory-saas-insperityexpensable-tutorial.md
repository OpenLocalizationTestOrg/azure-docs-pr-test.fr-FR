---
title: "Didacticiel : Intégration d’Azure Active Directory à Insperity ExpensAble | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Insperity ExpensAble."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c579c453-580e-417d-8a5e-9b6b352795c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 204d5435c6ba1f23bb98701381e165a9a66add62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insperity-expensable"></a><span data-ttu-id="9963c-103">Didacticiel : Intégration d’Azure Active Directory à Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="9963c-103">Tutorial: Azure Active Directory integration with Insperity ExpensAble</span></span>

<span data-ttu-id="9963c-104">Dans ce didacticiel, vous apprendrez comment toointegrate Insperity ExpensAble avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9963c-104">In this tutorial, you learn how toointegrate Insperity ExpensAble with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9963c-105">Intégration Insperity ExpensAble à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="9963c-105">Integrating Insperity ExpensAble with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9963c-106">Vous pouvez contrôler dans Azure AD qui a accès tooInsperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="9963c-106">You can control in Azure AD who has access tooInsperity ExpensAble</span></span>
- <span data-ttu-id="9963c-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooInsperity ExpensAble (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="9963c-107">You can enable your users tooautomatically get signed-on tooInsperity ExpensAble (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9963c-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="9963c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9963c-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9963c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9963c-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9963c-110">Prerequisites</span></span>

<span data-ttu-id="9963c-111">tooconfigure intégration d’Azure AD avec Insperity ExpensAble, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9963c-111">tooconfigure Azure AD integration with Insperity ExpensAble, you need hello following items:</span></span>

- <span data-ttu-id="9963c-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="9963c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9963c-113">Un abonnement Insperity ExpensAble pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="9963c-113">An Insperity ExpensAble single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9963c-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="9963c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9963c-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="9963c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9963c-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9963c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9963c-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9963c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9963c-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="9963c-118">Scenario description</span></span>
<span data-ttu-id="9963c-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="9963c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9963c-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="9963c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9963c-121">Ajout de Insperity ExpensAble à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="9963c-121">Adding Insperity ExpensAble from hello gallery</span></span>
2. <span data-ttu-id="9963c-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9963c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insperity-expensable-from-hello-gallery"></a><span data-ttu-id="9963c-123">Ajout de Insperity ExpensAble à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="9963c-123">Adding Insperity ExpensAble from hello gallery</span></span>
<span data-ttu-id="9963c-124">intégration de hello tooconfigure de Insperity ExpensAble dans Azure AD, vous devez tooadd Insperity ExpensAble à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="9963c-124">tooconfigure hello integration of Insperity ExpensAble into Azure AD, you need tooadd Insperity ExpensAble from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9963c-125">**tooadd Insperity ExpensAble à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9963c-125">**tooadd Insperity ExpensAble from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9963c-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="9963c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9963c-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="9963c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9963c-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9963c-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="9963c-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9963c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="9963c-133">Dans la zone de recherche de hello, tapez **Insperity ExpensAble**.</span><span class="sxs-lookup"><span data-stu-id="9963c-133">In hello search box, type **Insperity ExpensAble**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_search.png)

5. <span data-ttu-id="9963c-135">Dans le volet de résultats hello, sélectionnez **Insperity ExpensAble**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9963c-135">In hello results panel, select **Insperity ExpensAble**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9963c-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9963c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9963c-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Insperity ExpensAble avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="9963c-138">In this section, you configure and test Azure AD single sign-on with Insperity ExpensAble based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9963c-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello Insperity ExpensAble est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9963c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Insperity ExpensAble is tooa user in Azure AD.</span></span> <span data-ttu-id="9963c-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Insperity ExpensAble doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="9963c-140">In other words, a link relationship between an Azure AD user and hello related user in Insperity ExpensAble needs toobe established.</span></span>

<span data-ttu-id="9963c-141">Dans le ExpensAble Insperity, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="9963c-141">In Insperity ExpensAble, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9963c-142">tooconfigure et test Azure AD l’authentification unique avec Insperity ExpensAble, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="9963c-142">tooconfigure and test Azure AD single sign-on with Insperity ExpensAble, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9963c-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="9963c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9963c-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9963c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9963c-145">**[Création d’un utilisateur test Insperity ExpensAble](#creating-an-insperity-expensable-test-user)**  -toohave un équivalent de Britta Simon dans Insperity ExpensAble qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9963c-145">**[Creating an Insperity ExpensAble test user](#creating-an-insperity-expensable-test-user)** - toohave a counterpart of Britta Simon in Insperity ExpensAble that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9963c-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9963c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9963c-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="9963c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9963c-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9963c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9963c-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="9963c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Insperity ExpensAble application.</span></span>

<span data-ttu-id="9963c-150">**tooconfigure Azure AD single sign-on avec ExpensAble Insperity, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9963c-150">**tooconfigure Azure AD single sign-on with Insperity ExpensAble, perform hello following steps:**</span></span>

1. <span data-ttu-id="9963c-151">Bonjour portail Azure, sur hello **Insperity ExpensAble** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="9963c-151">In hello Azure portal, on hello **Insperity ExpensAble** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="9963c-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9963c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_samlbase.png)

3. <span data-ttu-id="9963c-155">Sur hello **URL et le domaine de ExpensAble Insperity** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9963c-155">On hello **Insperity ExpensAble Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_url.png)

    <span data-ttu-id="9963c-157">a.</span><span class="sxs-lookup"><span data-stu-id="9963c-157">a.</span></span> <span data-ttu-id="9963c-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`</span><span class="sxs-lookup"><span data-stu-id="9963c-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9963c-159">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="9963c-159">This value is not real.</span></span> <span data-ttu-id="9963c-160">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="9963c-160">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="9963c-161">Contact [équipe de support Client de ExpensAble Insperity](http://expensable.com/support/support-overview) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="9963c-161">Contact [Insperity ExpensAble Client support team](http://expensable.com/support/support-overview) tooget this value.</span></span> 
 
4. <span data-ttu-id="9963c-162">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="9963c-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_certificate.png) 

5. <span data-ttu-id="9963c-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="9963c-164">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9963c-166">Sur hello **Configuration de ExpensAble Insperity** , cliquez sur **configurer le ExpensAble Insperity** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="9963c-166">On hello **Insperity ExpensAble Configuration** section, click **Configure Insperity ExpensAble** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9963c-167">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="9963c-167">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_configure.png) 

7. <span data-ttu-id="9963c-169">tooconfigure l’authentification unique sur **Insperity ExpensAble** côté, vous devez hello toosend téléchargé **Metadata XML**, **SAML Sign-On URL du Service unique** et **ID d’entité SAML** trop[Insperity ExpensAble équipe de support](http://expensable.com/support/support-overview).</span><span class="sxs-lookup"><span data-stu-id="9963c-169">tooconfigure single sign-on on **Insperity ExpensAble** side, you need toosend hello downloaded **Metadata XML**, **SAML Single Sign-On Service URL** and **SAML Entity ID** too[Insperity ExpensAble support team](http://expensable.com/support/support-overview).</span></span> <span data-ttu-id="9963c-170">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="9963c-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9963c-171">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="9963c-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9963c-172">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="9963c-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9963c-173">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9963c-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9963c-174">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9963c-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="9963c-175">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="9963c-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="9963c-177">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9963c-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9963c-178">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="9963c-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9963c-180">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="9963c-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9963c-182">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="9963c-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9963c-184">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9963c-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9963c-186">a.</span><span class="sxs-lookup"><span data-stu-id="9963c-186">a.</span></span> <span data-ttu-id="9963c-187">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9963c-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9963c-188">b.</span><span class="sxs-lookup"><span data-stu-id="9963c-188">b.</span></span> <span data-ttu-id="9963c-189">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9963c-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9963c-190">c.</span><span class="sxs-lookup"><span data-stu-id="9963c-190">c.</span></span> <span data-ttu-id="9963c-191">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="9963c-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9963c-192">d.</span><span class="sxs-lookup"><span data-stu-id="9963c-192">d.</span></span> <span data-ttu-id="9963c-193">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="9963c-193">Click **Create**.</span></span>
 
### <a name="creating-an-insperity-expensable-test-user"></a><span data-ttu-id="9963c-194">Création d’un utilisateur de test Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="9963c-194">Creating an Insperity ExpensAble test user</span></span>

<span data-ttu-id="9963c-195">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="9963c-195">hello objective of this section is toocreate a user called Britta Simon in Insperity ExpensAble.</span></span> <span data-ttu-id="9963c-196">Collaborez avec [Insperity ExpensAble équipe de support](http://expensable.com/support/support-overview) utilisateurs hello tooadd hello Insperity ExpensAble compte.</span><span class="sxs-lookup"><span data-stu-id="9963c-196">Please work with [Insperity ExpensAble support team](http://expensable.com/support/support-overview) tooadd hello users in hello Insperity ExpensAble account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9963c-197">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9963c-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9963c-198">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooInsperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="9963c-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInsperity ExpensAble.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="9963c-200">**tooassign Britta Simon tooInsperity ExpensAble, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9963c-200">**tooassign Britta Simon tooInsperity ExpensAble, perform hello following steps:**</span></span>

1. <span data-ttu-id="9963c-201">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9963c-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="9963c-203">Dans la liste des applications hello, sélectionnez **Insperity ExpensAble**.</span><span class="sxs-lookup"><span data-stu-id="9963c-203">In hello applications list, select **Insperity ExpensAble**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_app.png) 

3. <span data-ttu-id="9963c-205">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9963c-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="9963c-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9963c-207">Click **Add** button.</span></span> <span data-ttu-id="9963c-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9963c-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="9963c-210">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="9963c-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9963c-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9963c-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9963c-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9963c-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9963c-213">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="9963c-213">Testing single sign-on</span></span>

<span data-ttu-id="9963c-214">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="9963c-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9963c-215">Lorsque vous cliquez sur mosaïque Insperity ExpensAble hello hello volet d’accès, vous devez obtenir l’application de Insperity ExpensAble tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="9963c-215">When you click hello Insperity ExpensAble tile in hello Access Panel, you should get automatically signed-on tooyour Insperity ExpensAble application.</span></span>
<span data-ttu-id="9963c-216">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9963c-216">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9963c-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="9963c-217">Additional resources</span></span>

* [<span data-ttu-id="9963c-218">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9963c-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9963c-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="9963c-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_203.png

