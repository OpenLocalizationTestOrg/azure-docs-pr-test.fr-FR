---
title: "Didacticiel : Intégration d’Azure Active Directory à Cornerstone OnDemand | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory à Cornerstone OnDemand."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f57c5fef-49b0-4591-91ef-fc0de6d654ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 85fd6eb4e93010d8f7477df236403e205e9f2d83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cornerstone-ondemand"></a><span data-ttu-id="53ff1-103">Didacticiel : Intégration d’Azure Active Directory à Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="53ff1-103">Tutorial: Azure Active Directory integration with Cornerstone OnDemand</span></span>

<span data-ttu-id="53ff1-104">Dans ce didacticiel, vous apprendrez comment toointegrate Cornerstone OnDemand avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="53ff1-104">In this tutorial, you learn how toointegrate Cornerstone OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="53ff1-105">Intégration Cornerstone OnDemand à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="53ff1-105">Integrating Cornerstone OnDemand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="53ff1-106">Vous pouvez contrôler dans Azure AD qui a tooCornerstone d’accès à la demande</span><span class="sxs-lookup"><span data-stu-id="53ff1-106">You can control in Azure AD who has access tooCornerstone OnDemand</span></span>
- <span data-ttu-id="53ff1-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooCornerstone OnDemand (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="53ff1-107">You can enable your users tooautomatically get signed-on tooCornerstone OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="53ff1-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="53ff1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="53ff1-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="53ff1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53ff1-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="53ff1-110">Prerequisites</span></span>

<span data-ttu-id="53ff1-111">tooconfigure intégration d’Azure AD à Cornerstone OnDemand, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="53ff1-111">tooconfigure Azure AD integration with Cornerstone OnDemand, you need hello following items:</span></span>

- <span data-ttu-id="53ff1-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="53ff1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="53ff1-113">Un abonnement Cornerstone OnDemand pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="53ff1-113">A Cornerstone OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="53ff1-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="53ff1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="53ff1-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="53ff1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="53ff1-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="53ff1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="53ff1-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="53ff1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="53ff1-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="53ff1-118">Scenario description</span></span>
<span data-ttu-id="53ff1-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="53ff1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="53ff1-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="53ff1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="53ff1-121">Ajout de Cornerstone OnDemand à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="53ff1-121">Adding Cornerstone OnDemand from hello gallery</span></span>
2. <span data-ttu-id="53ff1-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="53ff1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cornerstone-ondemand-from-hello-gallery"></a><span data-ttu-id="53ff1-123">Ajout de Cornerstone OnDemand à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="53ff1-123">Adding Cornerstone OnDemand from hello gallery</span></span>
<span data-ttu-id="53ff1-124">intégration de hello tooconfigure de Cornerstone OnDemand dans Azure AD, vous devez tooadd Cornerstone OnDemand à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="53ff1-124">tooconfigure hello integration of Cornerstone OnDemand into Azure AD, you need tooadd Cornerstone OnDemand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="53ff1-125">**tooadd Cornerstone OnDemand à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="53ff1-125">**tooadd Cornerstone OnDemand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="53ff1-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="53ff1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="53ff1-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="53ff1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="53ff1-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="53ff1-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="53ff1-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="53ff1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="53ff1-133">Dans la zone de recherche de hello, tapez **Cornerstone OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="53ff1-133">In hello search box, type **Cornerstone OnDemand**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_search.png)

5. <span data-ttu-id="53ff1-135">Dans le volet de résultats hello, sélectionnez **Cornerstone OnDemand**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="53ff1-135">In hello results panel, select **Cornerstone OnDemand**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="53ff1-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="53ff1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="53ff1-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Cornerstone OnDemand avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="53ff1-138">In this section, you configure and test Azure AD single sign-on with Cornerstone OnDemand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="53ff1-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Cornerstone OnDemand est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53ff1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cornerstone OnDemand is tooa user in Azure AD.</span></span> <span data-ttu-id="53ff1-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Cornerstone OnDemand doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="53ff1-140">In other words, a link relationship between an Azure AD user and hello related user in Cornerstone OnDemand needs toobe established.</span></span>

<span data-ttu-id="53ff1-141">Dans Cornerstone OnDemand, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="53ff1-141">In Cornerstone OnDemand, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="53ff1-142">tooconfigure et test Azure AD l’authentification unique à Cornerstone OnDemand, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="53ff1-142">tooconfigure and test Azure AD single sign-on with Cornerstone OnDemand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="53ff1-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="53ff1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="53ff1-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="53ff1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="53ff1-145">**[Création d’un utilisateur de test Cornerstone OnDemand](#creating-a-cornerstone-ondemand-test-user)**  -toohave un équivalent de Britta Simon dans Cornerstone OnDemand qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="53ff1-145">**[Creating a Cornerstone OnDemand test user](#creating-a-cornerstone-ondemand-test-user)** - toohave a counterpart of Britta Simon in Cornerstone OnDemand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="53ff1-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="53ff1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="53ff1-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="53ff1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="53ff1-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="53ff1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="53ff1-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="53ff1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cornerstone OnDemand application.</span></span>

<span data-ttu-id="53ff1-150">**tooconfigure Azure AD single sign-on avec Cornerstone OnDemand, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="53ff1-150">**tooconfigure Azure AD single sign-on with Cornerstone OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="53ff1-151">Bonjour portail Azure, sur hello **Cornerstone OnDemand** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="53ff1-151">In hello Azure portal, on hello **Cornerstone OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="53ff1-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="53ff1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_samlbase.png)

3. <span data-ttu-id="53ff1-155">Sur hello **Cornerstone OnDemand domaine et les URL** section, effectuer hello suivant l’étape :</span><span class="sxs-lookup"><span data-stu-id="53ff1-155">On hello **Cornerstone OnDemand Domain and URLs** section, perform hello following step:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_url.png)

    <span data-ttu-id="53ff1-157">a.</span><span class="sxs-lookup"><span data-stu-id="53ff1-157">a.</span></span> <span data-ttu-id="53ff1-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company>.csod.com`</span><span class="sxs-lookup"><span data-stu-id="53ff1-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.csod.com`</span></span>

    <span data-ttu-id="53ff1-159">b.</span><span class="sxs-lookup"><span data-stu-id="53ff1-159">b.</span></span> <span data-ttu-id="53ff1-160">Dans **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company>.csod.com`</span><span class="sxs-lookup"><span data-stu-id="53ff1-160">In **Identifier** textbox, type a URL using hello following pattern: `https://<company>.csod.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="53ff1-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="53ff1-161">These values are not real.</span></span> <span data-ttu-id="53ff1-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="53ff1-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="53ff1-163">Contact [équipe de support Cornerstone OnDemand Client](mailTo:moreinfo@csod.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="53ff1-163">Contact [Cornerstone OnDemand Client support team](mailTo:moreinfo@csod.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="53ff1-164">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="53ff1-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_certificate.png) 

5. <span data-ttu-id="53ff1-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="53ff1-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="53ff1-168">Sur hello **Cornerstone OnDemand Configuration** , cliquez sur **configurer Cornerstone OnDemand** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="53ff1-168">On hello **Cornerstone OnDemand Configuration** section, click **Configure Cornerstone OnDemand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="53ff1-169">Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="53ff1-169">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_configure.png) 

7. <span data-ttu-id="53ff1-171">tooconfigure l’authentification unique sur **Cornerstone OnDemand** côté, vous devez hello toosend téléchargé **certificat**, **URL de déconnexion** et **unique SAML URL de Service d’authentification** trop[équipe de support Cornerstone OnDemand](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="53ff1-171">tooconfigure single sign-on on **Cornerstone OnDemand** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL** and **SAML Single Sign-On Service URL**  too[Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span> <span data-ttu-id="53ff1-172">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="53ff1-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="53ff1-173">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="53ff1-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="53ff1-174">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="53ff1-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="53ff1-175">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="53ff1-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="53ff1-176">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="53ff1-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="53ff1-177">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="53ff1-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="53ff1-179">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="53ff1-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="53ff1-180">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="53ff1-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="53ff1-182">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="53ff1-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="53ff1-184">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="53ff1-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="53ff1-186">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="53ff1-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="53ff1-188">a.</span><span class="sxs-lookup"><span data-stu-id="53ff1-188">a.</span></span> <span data-ttu-id="53ff1-189">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="53ff1-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="53ff1-190">b.</span><span class="sxs-lookup"><span data-stu-id="53ff1-190">b.</span></span> <span data-ttu-id="53ff1-191">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="53ff1-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="53ff1-192">c.</span><span class="sxs-lookup"><span data-stu-id="53ff1-192">c.</span></span> <span data-ttu-id="53ff1-193">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="53ff1-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="53ff1-194">d.</span><span class="sxs-lookup"><span data-stu-id="53ff1-194">d.</span></span> <span data-ttu-id="53ff1-195">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="53ff1-195">Click **Create**.</span></span>
 
### <a name="creating-a-cornerstone-ondemand-test-user"></a><span data-ttu-id="53ff1-196">Création d’un utilisateur de test Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="53ff1-196">Creating a Cornerstone OnDemand test user</span></span>

<span data-ttu-id="53ff1-197">Dans l’ordre tooenable le toolog d’utilisateurs Azure AD à Cornerstone OnDemand, vous devez les configurer dans Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="53ff1-197">In order tooenable Azure AD users toolog into Cornerstone OnDemand, they must be provisioned into Cornerstone OnDemand.</span></span> <span data-ttu-id="53ff1-198">Dans les cas de hello de Cornerstone OnDemand, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="53ff1-198">In hello case of Cornerstone OnDemand, provisioning is a manual task.</span></span>

<span data-ttu-id="53ff1-199">utilisateur tooconfigure mise en service, envoyer des informations hello (par exemple : nom, envoyer par courrier électronique) sur l’utilisateur de hello Azure AD vous souhaitez tooprovision toohello [équipe de support Cornerstone OnDemand](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="53ff1-199">tooconfigure user provisioning, send hello information (e.g.: Name, Email) about hello Azure AD user you want tooprovision toohello [Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span>

>[!NOTE]
><span data-ttu-id="53ff1-200">Vous pouvez utiliser n’importe quel autre Cornerstone OnDemand utilisateur compte outil de création ou API fournie par Cornerstone OnDemand tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="53ff1-200">You can use any other Cornerstone OnDemand user account creation tools or APIs provided by Cornerstone OnDemand tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="53ff1-201">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="53ff1-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="53ff1-202">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooCornerstone à la demande.</span><span class="sxs-lookup"><span data-stu-id="53ff1-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCornerstone OnDemand.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="53ff1-204">**tooassign Britta Simon tooCornerstone OnDemand, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="53ff1-204">**tooassign Britta Simon tooCornerstone OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="53ff1-205">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="53ff1-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="53ff1-207">Dans la liste des applications hello, sélectionnez **Cornerstone OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="53ff1-207">In hello applications list, select **Cornerstone OnDemand**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_app.png) 

3. <span data-ttu-id="53ff1-209">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="53ff1-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="53ff1-211">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="53ff1-211">Click **Add** button.</span></span> <span data-ttu-id="53ff1-212">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="53ff1-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="53ff1-214">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="53ff1-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="53ff1-215">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="53ff1-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="53ff1-216">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="53ff1-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="53ff1-217">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="53ff1-217">Testing single sign-on</span></span>

<span data-ttu-id="53ff1-218">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="53ff1-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="53ff1-219">Lorsque vous cliquez sur mosaïque Cornerstone OnDemand hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Cornerstone OnDemand application.</span><span class="sxs-lookup"><span data-stu-id="53ff1-219">When you click hello Cornerstone OnDemand tile in hello Access Panel, you should get automatically signed-on tooyour Cornerstone OnDemand application.</span></span>
<span data-ttu-id="53ff1-220">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="53ff1-220">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="53ff1-221">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="53ff1-221">Additional resources</span></span>

* [<span data-ttu-id="53ff1-222">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="53ff1-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="53ff1-223">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="53ff1-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_203.png

