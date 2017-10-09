---
title: "Didacticiel : Intégration d’Azure Active Directory à People | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et les personnes."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c9b6202-11dd-4bb6-a679-8fb0a7a0ef4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: d540c31867c92c4dc09db9c0833f8a8a7c02b371
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-people"></a><span data-ttu-id="a2a5a-103">Didacticiel : Intégration d’Azure Active Directory à People</span><span class="sxs-lookup"><span data-stu-id="a2a5a-103">Tutorial: Azure Active Directory integration with People</span></span>

<span data-ttu-id="a2a5a-104">Dans ce didacticiel, vous apprendrez comment toointegrate personnes avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a2a5a-104">In this tutorial, you learn how toointegrate People with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a2a5a-105">Intégration des personnes à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a2a5a-105">Integrating People with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a2a5a-106">Vous pouvez contrôler dans Azure AD qui a accès tooPeople</span><span class="sxs-lookup"><span data-stu-id="a2a5a-106">You can control in Azure AD who has access tooPeople</span></span>
- <span data-ttu-id="a2a5a-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooPeople (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2a5a-107">You can enable your users tooautomatically get signed-on tooPeople (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a2a5a-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="a2a5a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a2a5a-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a2a5a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2a5a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a2a5a-110">Prerequisites</span></span>

<span data-ttu-id="a2a5a-111">tooconfigure intégration d’Azure AD avec des personnes, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a2a5a-111">tooconfigure Azure AD integration with People, you need hello following items:</span></span>

- <span data-ttu-id="a2a5a-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2a5a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a2a5a-113">Un abonnement People pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="a2a5a-113">A People single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a2a5a-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a2a5a-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="a2a5a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a2a5a-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a2a5a-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a2a5a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a2a5a-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="a2a5a-118">Scenario description</span></span>
<span data-ttu-id="a2a5a-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a2a5a-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="a2a5a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a2a5a-121">Ajout de membres à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a2a5a-121">Adding People from hello gallery</span></span>
2. <span data-ttu-id="a2a5a-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2a5a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-people-from-hello-gallery"></a><span data-ttu-id="a2a5a-123">Ajout de membres à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a2a5a-123">Adding People from hello gallery</span></span>
<span data-ttu-id="a2a5a-124">intégration de hello tooconfigure des personnes dans Azure AD, vous devez tooadd personnes à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-124">tooconfigure hello integration of People into Azure AD, you need tooadd People from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a2a5a-125">**tooadd personnes à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a2a5a-125">**tooadd People from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2a5a-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a2a5a-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a2a5a-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a2a5a-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a2a5a-133">Dans la zone de recherche de hello, tapez **personnes**.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-133">In hello search box, type **People**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-people-tutorial/tutorial_people_search.png)

5. <span data-ttu-id="a2a5a-135">Dans le volet de résultats hello, sélectionnez **personnes**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-135">In hello results panel, select **People**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-people-tutorial/tutorial_people_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a2a5a-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2a5a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a2a5a-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec People avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="a2a5a-138">In this section, you configure and test Azure AD single sign-on with People based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a2a5a-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans personnes est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in People is tooa user in Azure AD.</span></span> <span data-ttu-id="a2a5a-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans personnes doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-140">In other words, a link relationship between an Azure AD user and hello related user in People needs toobe established.</span></span>

<span data-ttu-id="a2a5a-141">Dans personnes, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-141">In People, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a2a5a-142">tooconfigure et test Azure AD l’authentification unique avec des personnes, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="a2a5a-142">tooconfigure and test Azure AD single sign-on with People, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a2a5a-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a2a5a-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a2a5a-145">**[Création d’un utilisateur de test de personnes](#creating-a-people-test-user)**  -toohave un équivalent de Britta Simon de personnes qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-145">**[Creating a People test user](#creating-a-people-test-user)** - toohave a counterpart of Britta Simon in People that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a2a5a-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a2a5a-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a2a5a-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2a5a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a2a5a-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application personnes.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your People application.</span></span>

<span data-ttu-id="a2a5a-150">**tooconfigure Azure AD authentification unique avec des personnes, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a2a5a-150">**tooconfigure Azure AD single sign-on with People, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2a5a-151">Bonjour portail Azure, sur hello **personnes** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-151">In hello Azure portal, on hello **People** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="a2a5a-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-people-tutorial/tutorial_people_samlbase.png)

3. <span data-ttu-id="a2a5a-155">Sur hello **domaine des personnes et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a2a5a-155">On hello **People Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-people-tutorial/tutorial_people_url.png)

    <span data-ttu-id="a2a5a-157">a.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-157">a.</span></span> <span data-ttu-id="a2a5a-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.peoplehr.com/`</span><span class="sxs-lookup"><span data-stu-id="a2a5a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.peoplehr.com/`</span></span>

    <span data-ttu-id="a2a5a-159">b.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-159">b.</span></span> <span data-ttu-id="a2a5a-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://www.peoplehr.com`</span><span class="sxs-lookup"><span data-stu-id="a2a5a-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.peoplehr.com`</span></span>

    <span data-ttu-id="a2a5a-161">c.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-161">c.</span></span> <span data-ttu-id="a2a5a-162">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span><span class="sxs-lookup"><span data-stu-id="a2a5a-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a2a5a-163">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-163">These values are not real.</span></span> <span data-ttu-id="a2a5a-164">Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="a2a5a-165">Contact [équipe de support Client de personnes](mailto:customerservices@peoplehr.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-165">Contact [People Client support team](mailto:customerservices@peoplehr.com) tooget these values.</span></span>

5. <span data-ttu-id="a2a5a-166">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-people-tutorial/tutorial_people_certificate.png) 

6. <span data-ttu-id="a2a5a-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="a2a5a-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-people-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="a2a5a-170">tooget SSO configuré pour votre application, vous devez le locataire de personnes sur toosign tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-170">tooget SSO configured for your application, you need toosign-on tooyour People tenant as an administrator.</span></span>
   
8. <span data-ttu-id="a2a5a-171">Dans le menu hello hello situé à gauche, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-171">In hello menu on hello left side, click **Settings**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-people-tutorial/tutorial_people_001.png)

9. <span data-ttu-id="a2a5a-173">Cliquez sur **Company**.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-173">Click **Company**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-people-tutorial/tutorial_people_002.png)

10. <span data-ttu-id="a2a5a-175">Sur hello **fichier de métadonnées de téléchargement 'Single Sign On' SAML**, cliquez sur **Parcourir** hello de tooupload téléchargé le fichier de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-175">On hello **Upload 'Single Sign On' SAML meta-data file**, click **Browse** tooupload hello downloaded metadata file.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-people-tutorial/tutorial_people_003.png)

> [!TIP]
> <span data-ttu-id="a2a5a-177">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="a2a5a-177">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a2a5a-178">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-178">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a2a5a-179">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a2a5a-179">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a2a5a-180">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2a5a-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="a2a5a-181">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-181">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="a2a5a-183">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a2a5a-183">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2a5a-184">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-184">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a2a5a-186">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-186">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a2a5a-188">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-188">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a2a5a-190">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a2a5a-190">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a2a5a-192">a.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-192">a.</span></span> <span data-ttu-id="a2a5a-193">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-193">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a2a5a-194">b.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-194">b.</span></span> <span data-ttu-id="a2a5a-195">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-195">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a2a5a-196">c.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-196">c.</span></span> <span data-ttu-id="a2a5a-197">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-197">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a2a5a-198">d.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-198">d.</span></span> <span data-ttu-id="a2a5a-199">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-199">Click **Create**.</span></span>
 
### <a name="creating-a-people-test-user"></a><span data-ttu-id="a2a5a-200">Création d’un utilisateur de test People</span><span class="sxs-lookup"><span data-stu-id="a2a5a-200">Creating a People test user</span></span>

<span data-ttu-id="a2a5a-201">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans People.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-201">In this section, you create a user called Britta Simon in People.</span></span> <span data-ttu-id="a2a5a-202">Travailler avec [équipe de support Client de personnes](mailto:customerservices@peoplehr.com) pour ajouter des utilisateurs de hello de plateforme de personnes hello.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-202">Work with [People Client support team](mailto:customerservices@peoplehr.com) to add hello users in hello People platform.</span></span> <span data-ttu-id="a2a5a-203">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-203">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a2a5a-204">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2a5a-204">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a2a5a-205">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooPeople.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-205">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPeople.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="a2a5a-207">**tooassign Britta Simon tooPeople, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a2a5a-207">**tooassign Britta Simon tooPeople, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2a5a-208">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-208">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="a2a5a-210">Dans la liste des applications hello, sélectionnez **personnes**.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-210">In hello applications list, select **People**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-people-tutorial/tutorial_people_app.png) 

3. <span data-ttu-id="a2a5a-212">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-212">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="a2a5a-214">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-214">Click **Add** button.</span></span> <span data-ttu-id="a2a5a-215">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-215">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="a2a5a-217">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-217">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a2a5a-218">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-218">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a2a5a-219">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-219">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a2a5a-220">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a2a5a-220">Testing single sign-on</span></span>

<span data-ttu-id="a2a5a-221">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-221">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="a2a5a-222">Lorsque vous cliquez sur hello personnes vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application de personnes.</span><span class="sxs-lookup"><span data-stu-id="a2a5a-222">When you click hello People tile in hello Access Panel, you should get automatically signed-on tooyour People application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a2a5a-223">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a2a5a-223">Additional resources</span></span>

* [<span data-ttu-id="a2a5a-224">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2a5a-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a2a5a-225">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a2a5a-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-people-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-people-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-people-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-people-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-people-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-people-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-people-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-people-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-people-tutorial/tutorial_general_203.png

