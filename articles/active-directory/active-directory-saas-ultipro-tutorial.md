---
title: "Didacticiel : Intégration d’Azure Active Directory avec UltiPro | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et UltiPro."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: afc0f2b9-2eac-47ec-af04-65ed0fb0ca5a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 8cb613228893e8cbf997957452d55d0ab7939171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ultipro"></a><span data-ttu-id="bf8db-103">Didacticiel : Intégration d’Azure Active Directory à UltiPro</span><span class="sxs-lookup"><span data-stu-id="bf8db-103">Tutorial: Azure Active Directory integration with UltiPro</span></span>

<span data-ttu-id="bf8db-104">Dans ce didacticiel, vous apprendrez comment toointegrate UltiPro avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bf8db-104">In this tutorial, you learn how toointegrate UltiPro with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bf8db-105">Intégration UltiPro à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="bf8db-105">Integrating UltiPro with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bf8db-106">Vous pouvez contrôler dans Azure AD qui a accès tooUltiPro</span><span class="sxs-lookup"><span data-stu-id="bf8db-106">You can control in Azure AD who has access tooUltiPro</span></span>
- <span data-ttu-id="bf8db-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooUltiPro (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf8db-107">You can enable your users tooautomatically get signed-on tooUltiPro (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bf8db-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="bf8db-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bf8db-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bf8db-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf8db-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bf8db-110">Prerequisites</span></span>

<span data-ttu-id="bf8db-111">tooconfigure intégration d’Azure AD avec UltiPro, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="bf8db-111">tooconfigure Azure AD integration with UltiPro, you need hello following items:</span></span>

- <span data-ttu-id="bf8db-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf8db-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bf8db-113">Un abonnement UltiPro pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="bf8db-113">A UltiPro single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bf8db-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="bf8db-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bf8db-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="bf8db-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bf8db-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="bf8db-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bf8db-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bf8db-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bf8db-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="bf8db-118">Scenario description</span></span>
<span data-ttu-id="bf8db-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="bf8db-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bf8db-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="bf8db-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bf8db-121">Ajout de UltiPro à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="bf8db-121">Adding UltiPro from hello gallery</span></span>
2. <span data-ttu-id="bf8db-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf8db-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ultipro-from-hello-gallery"></a><span data-ttu-id="bf8db-123">Ajout de UltiPro à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="bf8db-123">Adding UltiPro from hello gallery</span></span>
<span data-ttu-id="bf8db-124">intégration de hello tooconfigure de UltiPro dans Azure AD, vous devez tooadd UltiPro à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="bf8db-124">tooconfigure hello integration of UltiPro into Azure AD, you need tooadd UltiPro from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bf8db-125">**tooadd UltiPro à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bf8db-125">**tooadd UltiPro from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf8db-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="bf8db-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bf8db-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="bf8db-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bf8db-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bf8db-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="bf8db-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="bf8db-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="bf8db-133">Dans la zone de recherche de hello, tapez **UltiPro**.</span><span class="sxs-lookup"><span data-stu-id="bf8db-133">In hello search box, type **UltiPro**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_search.png)

5. <span data-ttu-id="bf8db-135">Dans le volet de résultats hello, sélectionnez **UltiPro**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="bf8db-135">In hello results panel, select **UltiPro**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bf8db-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf8db-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bf8db-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec UltiPro avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="bf8db-138">In this section, you configure and test Azure AD single sign-on with UltiPro based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bf8db-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans UltiPro est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf8db-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UltiPro is tooa user in Azure AD.</span></span> <span data-ttu-id="bf8db-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans UltiPro doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="bf8db-140">In other words, a link relationship between an Azure AD user and hello related user in UltiPro needs toobe established.</span></span>

<span data-ttu-id="bf8db-141">Dans UltiPro, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="bf8db-141">In UltiPro, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bf8db-142">tooconfigure et test Azure AD l’authentification unique avec UltiPro, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="bf8db-142">tooconfigure and test Azure AD single sign-on with UltiPro, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bf8db-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="bf8db-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bf8db-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bf8db-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bf8db-145">**[Création d’un utilisateur de test UltiPro](#creating-a-ultipro-test-user)**  -toohave un équivalent de Britta Simon dans UltiPro est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bf8db-145">**[Creating a UltiPro test user](#creating-a-ultipro-test-user)** - toohave a counterpart of Britta Simon in UltiPro that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bf8db-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="bf8db-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bf8db-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="bf8db-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bf8db-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf8db-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bf8db-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application UltiPro.</span><span class="sxs-lookup"><span data-stu-id="bf8db-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UltiPro application.</span></span>

<span data-ttu-id="bf8db-150">**tooconfigure Azure AD single sign-on avec UltiPro, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bf8db-150">**tooconfigure Azure AD single sign-on with UltiPro, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf8db-151">Bonjour portail Azure, sur hello **UltiPro** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="bf8db-151">In hello Azure portal, on hello **UltiPro** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="bf8db-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="bf8db-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_samlbase.png)

3. <span data-ttu-id="bf8db-155">Sur hello **UltiPro domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bf8db-155">On hello **UltiPro Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_url.png)

    <span data-ttu-id="bf8db-157">a.</span><span class="sxs-lookup"><span data-stu-id="bf8db-157">a.</span></span> <span data-ttu-id="bf8db-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="bf8db-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/`|
    | `https://<companyname>.ultiproworkplace.com?cpi=AZUREADISSSUERURL`|
    | ` https://<companyname>.ultipro.ca`|
    
    <span data-ttu-id="bf8db-159">b.</span><span class="sxs-lookup"><span data-stu-id="bf8db-159">b.</span></span> <span data-ttu-id="bf8db-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="bf8db-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/adfs/services/trust`|
    | `https://<companyname>.ultiproworkplace.com/adfs/services/trust`|
    | `https://<companyname>.ultipro.ca/adfs/services/trust`|
    
    <span data-ttu-id="bf8db-161">c.</span><span class="sxs-lookup"><span data-stu-id="bf8db-161">c.</span></span> <span data-ttu-id="bf8db-162">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="bf8db-162">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/<instancename>`|
    | `https://<companyname>.ultiproworkplace.com/<instancename>`|
    | `https://<companyname>.ultipro.ca/<instancename>`|
    
    > [!NOTE] 
    > <span data-ttu-id="bf8db-163">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="bf8db-163">These values are not real.</span></span> <span data-ttu-id="bf8db-164">Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="bf8db-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="bf8db-165">Contact [équipe de support Client de UltiPro](https://www.ultimatesoftware.com/ContactUs) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="bf8db-165">Contact [UltiPro Client support team](https://www.ultimatesoftware.com/ContactUs) tooget these values.</span></span> 

5. <span data-ttu-id="bf8db-166">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="bf8db-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_certificate.png) 

6. <span data-ttu-id="bf8db-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="bf8db-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ultipro-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="bf8db-170">Sur hello **UltiPro Configuration** , cliquez sur **UltiPro de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="bf8db-170">On hello **UltiPro Configuration** section, click **Configure UltiPro** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bf8db-171">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="bf8db-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_configure.png) 

8. <span data-ttu-id="bf8db-173">tooconfigure l’authentification unique sur **UltiPro** côté, vous devez hello toosend téléchargé **Certificate(Base64), l’URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** trop[UltiPro l’équipe de support](https://www.ultimatesoftware.com/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="bf8db-173">tooconfigure single sign-on on **UltiPro** side, you need toosend hello downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[UltiPro support team](https://www.ultimatesoftware.com/ContactUs).</span></span>

> [!TIP]
> <span data-ttu-id="bf8db-174">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="bf8db-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bf8db-175">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="bf8db-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bf8db-176">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bf8db-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bf8db-177">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf8db-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="bf8db-178">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="bf8db-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="bf8db-180">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bf8db-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf8db-181">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="bf8db-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bf8db-183">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="bf8db-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bf8db-185">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="bf8db-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bf8db-187">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bf8db-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bf8db-189">a.</span><span class="sxs-lookup"><span data-stu-id="bf8db-189">a.</span></span> <span data-ttu-id="bf8db-190">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bf8db-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bf8db-191">b.</span><span class="sxs-lookup"><span data-stu-id="bf8db-191">b.</span></span> <span data-ttu-id="bf8db-192">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bf8db-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bf8db-193">c.</span><span class="sxs-lookup"><span data-stu-id="bf8db-193">c.</span></span> <span data-ttu-id="bf8db-194">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="bf8db-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bf8db-195">d.</span><span class="sxs-lookup"><span data-stu-id="bf8db-195">d.</span></span> <span data-ttu-id="bf8db-196">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="bf8db-196">Click **Create**.</span></span>
 
### <a name="creating-a-ultipro-test-user"></a><span data-ttu-id="bf8db-197">Création d’un utilisateur de test UltiPro</span><span class="sxs-lookup"><span data-stu-id="bf8db-197">Creating a UltiPro test user</span></span>

<span data-ttu-id="bf8db-198">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans UltiPro.</span><span class="sxs-lookup"><span data-stu-id="bf8db-198">In this section, you create a user called Britta Simon in UltiPro.</span></span> <span data-ttu-id="bf8db-199">Travailler avec [équipe de support UltiPro](https://www.ultimatesoftware.com/ContactUs) pour ajouter des utilisateurs de hello de plateforme de UltiPro hello.</span><span class="sxs-lookup"><span data-stu-id="bf8db-199">Work with [UltiPro support team](https://www.ultimatesoftware.com/ContactUs) to add hello users in hello UltiPro platform.</span></span> <span data-ttu-id="bf8db-200">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="bf8db-200">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bf8db-201">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf8db-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bf8db-202">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooUltiPro.</span><span class="sxs-lookup"><span data-stu-id="bf8db-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUltiPro.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="bf8db-204">**tooassign Britta Simon tooUltiPro, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bf8db-204">**tooassign Britta Simon tooUltiPro, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf8db-205">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bf8db-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="bf8db-207">Dans la liste des applications hello, sélectionnez **UltiPro**.</span><span class="sxs-lookup"><span data-stu-id="bf8db-207">In hello applications list, select **UltiPro**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_app.png) 

3. <span data-ttu-id="bf8db-209">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="bf8db-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="bf8db-211">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bf8db-211">Click **Add** button.</span></span> <span data-ttu-id="bf8db-212">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="bf8db-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="bf8db-214">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="bf8db-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bf8db-215">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="bf8db-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bf8db-216">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="bf8db-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bf8db-217">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="bf8db-217">Testing single sign-on</span></span>

<span data-ttu-id="bf8db-218">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="bf8db-218">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="bf8db-219">Lorsque vous cliquez sur mosaïque UltiPro hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour UltiPro application.</span><span class="sxs-lookup"><span data-stu-id="bf8db-219">When you click hello UltiPro tile in hello Access Panel, you should get automatically signed-on tooyour UltiPro application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bf8db-220">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="bf8db-220">Additional resources</span></span>

* [<span data-ttu-id="bf8db-221">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bf8db-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bf8db-222">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="bf8db-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_203.png

