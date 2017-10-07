---
title: "Didacticiel : Intégration d’Azure Active Directory à Mindflash | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Mindflash."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdf91993-aaaa-4598-89b7-77ef8ca065d5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: a1bc327ea3867287103acbb64d30f0a8d7d4c5e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mindflash"></a><span data-ttu-id="628b3-103">Didacticiel : Intégration d’Azure Active Directory avec Mindflash</span><span class="sxs-lookup"><span data-stu-id="628b3-103">Tutorial: Azure Active Directory integration with Mindflash</span></span>

<span data-ttu-id="628b3-104">Dans ce didacticiel, vous apprendrez comment toointegrate Mindflash avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="628b3-104">In this tutorial, you learn how toointegrate Mindflash with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="628b3-105">Intégration de Mindflash à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="628b3-105">Integrating Mindflash with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="628b3-106">Vous pouvez contrôler dans Azure AD qui a accès tooMindflash</span><span class="sxs-lookup"><span data-stu-id="628b3-106">You can control in Azure AD who has access tooMindflash</span></span>
- <span data-ttu-id="628b3-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooMindflash (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="628b3-107">You can enable your users tooautomatically get signed-on tooMindflash (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="628b3-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="628b3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="628b3-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="628b3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="628b3-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="628b3-110">Prerequisites</span></span>

<span data-ttu-id="628b3-111">tooconfigure intégration d’Azure AD à Mindflash, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="628b3-111">tooconfigure Azure AD integration with Mindflash, you need hello following items:</span></span>

- <span data-ttu-id="628b3-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="628b3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="628b3-113">Un abonnement Mindflash pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="628b3-113">A Mindflash single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="628b3-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="628b3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="628b3-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="628b3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="628b3-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="628b3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="628b3-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="628b3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="628b3-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="628b3-118">Scenario description</span></span>
<span data-ttu-id="628b3-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="628b3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="628b3-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="628b3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="628b3-121">Ajout de Mindflash à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="628b3-121">Adding Mindflash from hello gallery</span></span>
2. <span data-ttu-id="628b3-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="628b3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mindflash-from-hello-gallery"></a><span data-ttu-id="628b3-123">Ajout de Mindflash à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="628b3-123">Adding Mindflash from hello gallery</span></span>
<span data-ttu-id="628b3-124">intégration de hello tooconfigure de Mindflash dans Azure AD, vous devez tooadd Mindflash à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="628b3-124">tooconfigure hello integration of Mindflash into Azure AD, you need tooadd Mindflash from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="628b3-125">**tooadd Mindflash à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="628b3-125">**tooadd Mindflash from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="628b3-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="628b3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="628b3-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="628b3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="628b3-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="628b3-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="628b3-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="628b3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="628b3-133">Dans la zone de recherche de hello, tapez **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="628b3-133">In hello search box, type **Mindflash**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_search.png)

5. <span data-ttu-id="628b3-135">Dans le volet de résultats hello, sélectionnez **Mindflash**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="628b3-135">In hello results panel, select **Mindflash**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="628b3-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="628b3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="628b3-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Mindflash avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="628b3-138">In this section, you configure and test Azure AD single sign-on with Mindflash based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="628b3-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Mindflash est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="628b3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mindflash is tooa user in Azure AD.</span></span> <span data-ttu-id="628b3-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Mindflash doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="628b3-140">In other words, a link relationship between an Azure AD user and hello related user in Mindflash needs toobe established.</span></span>

<span data-ttu-id="628b3-141">Dans Mindflash, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="628b3-141">In Mindflash, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="628b3-142">tooconfigure et test Azure AD l’authentification unique avec Mindflash, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="628b3-142">tooconfigure and test Azure AD single sign-on with Mindflash, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="628b3-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="628b3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="628b3-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="628b3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="628b3-145">**[Création d’un utilisateur de test Mindflash](#creating-a-mindflash-test-user)**  -toohave un équivalent de Britta Simon dans Mindflash est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="628b3-145">**[Creating a Mindflash test user](#creating-a-mindflash-test-user)** - toohave a counterpart of Britta Simon in Mindflash that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="628b3-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="628b3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="628b3-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="628b3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="628b3-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="628b3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="628b3-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Mindflash.</span><span class="sxs-lookup"><span data-stu-id="628b3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mindflash application.</span></span>

<span data-ttu-id="628b3-150">**tooconfigure Azure AD single sign-on avec Mindflash, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="628b3-150">**tooconfigure Azure AD single sign-on with Mindflash, perform hello following steps:**</span></span>

1. <span data-ttu-id="628b3-151">Bonjour portail Azure, sur hello **Mindflash** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="628b3-151">In hello Azure portal, on hello **Mindflash** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="628b3-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="628b3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_samlbase.png)

3. <span data-ttu-id="628b3-155">Sur hello **Mindflash domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="628b3-155">On hello **Mindflash Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_url.png)

    <span data-ttu-id="628b3-157">a.</span><span class="sxs-lookup"><span data-stu-id="628b3-157">a.</span></span> <span data-ttu-id="628b3-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="628b3-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.mindflash.com`</span></span>

    <span data-ttu-id="628b3-159">b.</span><span class="sxs-lookup"><span data-stu-id="628b3-159">b.</span></span> <span data-ttu-id="628b3-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="628b3-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.mindflash.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="628b3-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="628b3-161">These values are not real.</span></span> <span data-ttu-id="628b3-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="628b3-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="628b3-163">Contact [équipe de support Mindflash Client](https://www.mindflash.com/contact/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="628b3-163">Contact [Mindflash Client support team](https://www.mindflash.com/contact/) tooget these values.</span></span> 
 


4. <span data-ttu-id="628b3-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="628b3-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_certificate.png) 

5. <span data-ttu-id="628b3-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="628b3-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mindflash-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="628b3-168">tooconfigure l’authentification unique sur **Mindflash** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support Mindflash](https://www.mindflash.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="628b3-168">tooconfigure single sign-on on **Mindflash** side, you need toosend hello downloaded **Metadata XML** too[Mindflash support team](https://www.mindflash.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="628b3-169">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="628b3-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="628b3-170">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="628b3-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="628b3-171">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="628b3-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="628b3-172">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="628b3-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="628b3-173">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="628b3-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="628b3-175">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="628b3-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="628b3-176">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="628b3-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="628b3-178">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="628b3-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="628b3-180">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="628b3-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="628b3-182">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="628b3-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="628b3-184">a.</span><span class="sxs-lookup"><span data-stu-id="628b3-184">a.</span></span> <span data-ttu-id="628b3-185">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="628b3-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="628b3-186">b.</span><span class="sxs-lookup"><span data-stu-id="628b3-186">b.</span></span> <span data-ttu-id="628b3-187">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="628b3-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="628b3-188">c.</span><span class="sxs-lookup"><span data-stu-id="628b3-188">c.</span></span> <span data-ttu-id="628b3-189">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="628b3-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="628b3-190">d.</span><span class="sxs-lookup"><span data-stu-id="628b3-190">d.</span></span> <span data-ttu-id="628b3-191">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="628b3-191">Click **Create**.</span></span>
 
### <a name="creating-a-mindflash-test-user"></a><span data-ttu-id="628b3-192">Création d’un utilisateur de test Mindflash</span><span class="sxs-lookup"><span data-stu-id="628b3-192">Creating a Mindflash test user</span></span>

<span data-ttu-id="628b3-193">Dans l’ordre tooenable Azure AD les utilisateurs toolog à Mindflash, vous devez les configurer dans Mindflash.</span><span class="sxs-lookup"><span data-stu-id="628b3-193">In order tooenable Azure AD users toolog into Mindflash, they must be provisioned into Mindflash.</span></span> <span data-ttu-id="628b3-194">Dans les cas de hello de Mindflash, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="628b3-194">In hello case of Mindflash, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="628b3-195">effectuer des comptes d’utilisateur, tooprovision hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="628b3-195">tooprovision a user accounts, perform hello following steps:</span></span>

1. <span data-ttu-id="628b3-196">Connectez-vous à tooyour **Mindflash** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="628b3-196">Log in tooyour **Mindflash** company site as an administrator.</span></span>

2. <span data-ttu-id="628b3-197">Accédez trop**gérer les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="628b3-197">Go too**Manage Users**.</span></span>
   
    <span data-ttu-id="628b3-198">![Gestion des utilisateurs](./media/active-directory-saas-mindflash-tutorial/ic787140.png "Gestion des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="628b3-198">![Manage Users](./media/active-directory-saas-mindflash-tutorial/ic787140.png "Manage Users")</span></span>

3. <span data-ttu-id="628b3-199">Cliquez sur hello **ajouter des utilisateurs**, puis cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="628b3-199">Click hello **Add Users**, and then click **New**.</span></span>

4. <span data-ttu-id="628b3-200">Bonjour **ajouter de nouveaux utilisateurs** section, effectuer hello suivant les étapes d’un Azure valide compte AD tooprovision :</span><span class="sxs-lookup"><span data-stu-id="628b3-200">In hello **Add New Users** section, perform hello following steps of a valid Azure AD account you want tooprovision:</span></span>
   
    <span data-ttu-id="628b3-201">![Ajouter de nouveaux utilisateurs](./media/active-directory-saas-mindflash-tutorial/ic787141.png "Ajouter de nouveaux utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="628b3-201">![Add New Users](./media/active-directory-saas-mindflash-tutorial/ic787141.png "Add New Users")</span></span>
   
    <span data-ttu-id="628b3-202">a.</span><span class="sxs-lookup"><span data-stu-id="628b3-202">a.</span></span> <span data-ttu-id="628b3-203">Bonjour **prénom** zone de texte, type **prénom** d’utilisateur hello en tant que **Brian**.</span><span class="sxs-lookup"><span data-stu-id="628b3-203">In hello **First name** textbox, type **First name** of hello user as **Britta**.</span></span>

    <span data-ttu-id="628b3-204">b.</span><span class="sxs-lookup"><span data-stu-id="628b3-204">b.</span></span> <span data-ttu-id="628b3-205">Bonjour **nom** zone de texte, type **nom** d’utilisateur hello en tant que **Simon**.</span><span class="sxs-lookup"><span data-stu-id="628b3-205">In hello **Last name** textbox, type **Last name** of hello user as **Simon**.</span></span>
    
    <span data-ttu-id="628b3-206">c.</span><span class="sxs-lookup"><span data-stu-id="628b3-206">c.</span></span> <span data-ttu-id="628b3-207">Bonjour **messagerie** zone de texte, type **adresse de messagerie** d’utilisateur hello en tant que  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="628b3-207">In hello **Email** textbox, type **Email Address** of hello user as **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="628b3-208">b.</span><span class="sxs-lookup"><span data-stu-id="628b3-208">b.</span></span> <span data-ttu-id="628b3-209">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="628b3-209">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="628b3-210">Vous pouvez utiliser n’importe quel autre Mindflash utilisateur compte outil de création ou API fournie par Mindflash tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="628b3-210">You can use any other Mindflash user account creation tools or APIs provided by Mindflash tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="628b3-211">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="628b3-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="628b3-212">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooMindflash.</span><span class="sxs-lookup"><span data-stu-id="628b3-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMindflash.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="628b3-214">**tooassign Britta Simon tooMindflash, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="628b3-214">**tooassign Britta Simon tooMindflash, perform hello following steps:**</span></span>

1. <span data-ttu-id="628b3-215">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="628b3-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="628b3-217">Dans la liste des applications hello, sélectionnez **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="628b3-217">In hello applications list, select **Mindflash**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_app.png) 

3. <span data-ttu-id="628b3-219">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="628b3-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="628b3-221">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="628b3-221">Click **Add** button.</span></span> <span data-ttu-id="628b3-222">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="628b3-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="628b3-224">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="628b3-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="628b3-225">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="628b3-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="628b3-226">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="628b3-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="628b3-227">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="628b3-227">Testing single sign-on</span></span>

<span data-ttu-id="628b3-228">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="628b3-228">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="628b3-229">Lorsque vous cliquez sur mosaïque Mindflash hello hello volet d’accès, vous devez obtenir la page de connexion de l’application de Mindflash.</span><span class="sxs-lookup"><span data-stu-id="628b3-229">When you click hello Mindflash tile in hello Access Panel, you should get login page of Mindflash application.</span></span>
<span data-ttu-id="628b3-230">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="628b3-230">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="628b3-231">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="628b3-231">Additional resources</span></span>

* [<span data-ttu-id="628b3-232">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="628b3-232">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="628b3-233">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="628b3-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_203.png

