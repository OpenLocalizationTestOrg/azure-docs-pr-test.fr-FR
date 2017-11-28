---
title: "Didacticiel : Intégration d’Azure Active Directory à Nomadesk | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Nomadesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d261b776-b48e-45f0-9722-0297adefabb8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 9aa55ba6106ea24f556217cfe84d21d7415d9c78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nomadesk"></a><span data-ttu-id="84648-103">Didacticiel : Intégration d’Azure Active Directory à Nomadesk</span><span class="sxs-lookup"><span data-stu-id="84648-103">Tutorial: Azure Active Directory integration with Nomadesk</span></span>

<span data-ttu-id="84648-104">Dans ce didacticiel, vous apprendrez comment toointegrate Nomadesk avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="84648-104">In this tutorial, you learn how toointegrate Nomadesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="84648-105">Intégration Nomadesk à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="84648-105">Integrating Nomadesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="84648-106">Vous pouvez contrôler dans Azure AD qui a accès tooNomadesk</span><span class="sxs-lookup"><span data-stu-id="84648-106">You can control in Azure AD who has access tooNomadesk</span></span>
- <span data-ttu-id="84648-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooNomadesk (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="84648-107">You can enable your users tooautomatically get signed-on tooNomadesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="84648-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="84648-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="84648-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="84648-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84648-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="84648-110">Prerequisites</span></span>

<span data-ttu-id="84648-111">tooconfigure intégration d’Azure AD avec Nomadesk, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="84648-111">tooconfigure Azure AD integration with Nomadesk, you need hello following items:</span></span>

- <span data-ttu-id="84648-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="84648-112">An Azure AD subscription</span></span>
- <span data-ttu-id="84648-113">Un abonnement Nomadesk pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="84648-113">A Nomadesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="84648-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="84648-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="84648-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="84648-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="84648-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="84648-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="84648-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="84648-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="84648-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="84648-118">Scenario description</span></span>
<span data-ttu-id="84648-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="84648-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="84648-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="84648-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="84648-121">Ajout de Nomadesk à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="84648-121">Adding Nomadesk from hello gallery</span></span>
2. <span data-ttu-id="84648-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="84648-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nomadesk-from-hello-gallery"></a><span data-ttu-id="84648-123">Ajout de Nomadesk à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="84648-123">Adding Nomadesk from hello gallery</span></span>
<span data-ttu-id="84648-124">intégration de hello tooconfigure de Nomadesk dans Azure AD, vous devez tooadd Nomadesk à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="84648-124">tooconfigure hello integration of Nomadesk into Azure AD, you need tooadd Nomadesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="84648-125">**tooadd Nomadesk à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="84648-125">**tooadd Nomadesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="84648-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="84648-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="84648-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="84648-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="84648-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="84648-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="84648-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="84648-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="84648-133">Dans la zone de recherche de hello, tapez **Nomadesk**.</span><span class="sxs-lookup"><span data-stu-id="84648-133">In hello search box, type **Nomadesk**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_search.png)

5. <span data-ttu-id="84648-135">Dans le volet de résultats hello, sélectionnez **Nomadesk**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="84648-135">In hello results panel, select **Nomadesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="84648-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="84648-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="84648-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Nomadesk, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="84648-138">In this section, you configure and test Azure AD single sign-on with Nomadesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="84648-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Nomadesk est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="84648-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Nomadesk is tooa user in Azure AD.</span></span> <span data-ttu-id="84648-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Nomadesk doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="84648-140">In other words, a link relationship between an Azure AD user and hello related user in Nomadesk needs toobe established.</span></span>

<span data-ttu-id="84648-141">Dans Nomadesk, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="84648-141">In Nomadesk, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="84648-142">tooconfigure et test Azure AD l’authentification unique avec Nomadesk, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="84648-142">tooconfigure and test Azure AD single sign-on with Nomadesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="84648-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="84648-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="84648-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="84648-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="84648-145">**[Création d’un utilisateur de test Nomadesk](#creating-a-nomadesk-test-user)**  -toohave un équivalent de Britta Simon dans Nomadesk est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="84648-145">**[Creating a Nomadesk test user](#creating-a-nomadesk-test-user)** - toohave a counterpart of Britta Simon in Nomadesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="84648-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="84648-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="84648-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="84648-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="84648-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="84648-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="84648-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Nomadesk.</span><span class="sxs-lookup"><span data-stu-id="84648-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Nomadesk application.</span></span>

<span data-ttu-id="84648-150">**tooconfigure Azure AD single sign-on avec Nomadesk, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="84648-150">**tooconfigure Azure AD single sign-on with Nomadesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="84648-151">Bonjour portail Azure, sur hello **Nomadesk** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="84648-151">In hello Azure portal, on hello **Nomadesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="84648-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="84648-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_samlbase.png)

3. <span data-ttu-id="84648-155">Sur hello **Nomadesk domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="84648-155">On hello **Nomadesk Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_url.png)

    <span data-ttu-id="84648-157">a.</span><span class="sxs-lookup"><span data-stu-id="84648-157">a.</span></span> <span data-ttu-id="84648-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://mynomadesk.com/logon/saml/<TENANTID>`</span><span class="sxs-lookup"><span data-stu-id="84648-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://mynomadesk.com/logon/saml/<TENANTID>`</span></span>

    <span data-ttu-id="84648-159">b.</span><span class="sxs-lookup"><span data-stu-id="84648-159">b.</span></span> <span data-ttu-id="84648-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://secure.nomadesk.com/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="84648-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://secure.nomadesk.com/saml/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="84648-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="84648-161">These values are not real.</span></span> <span data-ttu-id="84648-162">Mettre à jour ces valeurs avec l’URL de connexion réel hello et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="84648-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="84648-163">Contact [équipe de support Client de Nomadesk](mailto:support@nomadesk.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="84648-163">Contact [Nomadesk Client support team](mailto:support@nomadesk.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="84648-164">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="84648-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_certificate.png) 

5. <span data-ttu-id="84648-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="84648-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-nomadesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="84648-168">Sur hello **Nomadesk Configuration** , cliquez sur **Nomadesk de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="84648-168">On hello **Nomadesk Configuration** section, click **Configure Nomadesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="84648-169">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="84648-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_configure.png) 

7. <span data-ttu-id="84648-171">tooconfigure l’authentification unique sur **Nomadesk** côté, vous devez hello toosend téléchargé **certificat**, **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** trop[équipe de support Nomadesk](mailto:support@nomadesk.com).</span><span class="sxs-lookup"><span data-stu-id="84648-171">tooconfigure single sign-on on **Nomadesk** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Nomadesk support team](mailto:support@nomadesk.com).</span></span> <span data-ttu-id="84648-172">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="84648-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="84648-173">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="84648-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="84648-174">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="84648-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="84648-175">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="84648-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="84648-176">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="84648-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="84648-177">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="84648-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="84648-179">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="84648-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="84648-180">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="84648-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="84648-182">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="84648-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="84648-184">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="84648-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="84648-186">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="84648-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="84648-188">a.</span><span class="sxs-lookup"><span data-stu-id="84648-188">a.</span></span> <span data-ttu-id="84648-189">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="84648-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="84648-190">b.</span><span class="sxs-lookup"><span data-stu-id="84648-190">b.</span></span> <span data-ttu-id="84648-191">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="84648-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="84648-192">c.</span><span class="sxs-lookup"><span data-stu-id="84648-192">c.</span></span> <span data-ttu-id="84648-193">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="84648-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="84648-194">d.</span><span class="sxs-lookup"><span data-stu-id="84648-194">d.</span></span> <span data-ttu-id="84648-195">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="84648-195">Click **Create**.</span></span>
 
### <a name="creating-a-nomadesk-test-user"></a><span data-ttu-id="84648-196">Création d’un utilisateur de test Nomadesk</span><span class="sxs-lookup"><span data-stu-id="84648-196">Creating a Nomadesk test user</span></span>

<span data-ttu-id="84648-197">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Nomadesk.</span><span class="sxs-lookup"><span data-stu-id="84648-197">hello objective of this section is toocreate a user called Britta Simon in Nomadesk.</span></span> <span data-ttu-id="84648-198">Nomadesk prend en charge l’approvisionnement juste-à-temps, qui est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="84648-198">Nomadesk supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="84648-199">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="84648-199">There is no action item for you in this section.</span></span> <span data-ttu-id="84648-200">Un nouvel utilisateur est créé au cours d’une tentative de tooaccess Nomadesk s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="84648-200">A new user is created during an attempt tooaccess Nomadesk if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="84648-201">Si vous devez manuellement toocreate un utilisateur, vous devez toocontact hello [équipe de support Nomadesk](mailto:support@nomadesk.com).</span><span class="sxs-lookup"><span data-stu-id="84648-201">If you need toocreate a user manually, you need toocontact hello [Nomadesk support team](mailto:support@nomadesk.com).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="84648-202">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="84648-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="84648-203">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooNomadesk.</span><span class="sxs-lookup"><span data-stu-id="84648-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNomadesk.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="84648-205">**tooassign Britta Simon tooNomadesk, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="84648-205">**tooassign Britta Simon tooNomadesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="84648-206">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="84648-206">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="84648-208">Dans la liste des applications hello, sélectionnez **Nomadesk**.</span><span class="sxs-lookup"><span data-stu-id="84648-208">In hello applications list, select **Nomadesk**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_app.png) 

3. <span data-ttu-id="84648-210">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="84648-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="84648-212">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="84648-212">Click **Add** button.</span></span> <span data-ttu-id="84648-213">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="84648-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="84648-215">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="84648-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="84648-216">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="84648-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="84648-217">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="84648-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="84648-218">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="84648-218">Testing single sign-on</span></span>

<span data-ttu-id="84648-219">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="84648-219">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="84648-220">Lorsque vous cliquez sur mosaïque Nomadesk hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Nomadesk application.</span><span class="sxs-lookup"><span data-stu-id="84648-220">When you click hello Nomadesk tile in hello Access Panel,  you should get automatically signed-on tooyour Nomadesk application.</span></span>
<span data-ttu-id="84648-221">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="84648-221">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="84648-222">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="84648-222">Additional resources</span></span>

* [<span data-ttu-id="84648-223">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="84648-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="84648-224">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="84648-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_203.png

