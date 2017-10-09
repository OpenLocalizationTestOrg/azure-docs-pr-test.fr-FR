---
title: "Didacticiel : Intégration d’Azure Active Directory avec SCC LifeCycle | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de SCC LifeCycle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 63623c5bd2d951612040f0121615a406bf83e890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="78dd4-103">Didacticiel : Intégration d’Azure AD avec SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="78dd4-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>

<span data-ttu-id="78dd4-104">Dans ce didacticiel, vous apprendrez comment toointegrate SCC LifeCycle avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="78dd4-104">In this tutorial, you learn how toointegrate SCC LifeCycle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="78dd4-105">Intégration de SCC LifeCycle à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="78dd4-105">Integrating SCC LifeCycle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="78dd4-106">Vous pouvez contrôler dans Azure AD qui a accès tooSCC du cycle de vie</span><span class="sxs-lookup"><span data-stu-id="78dd4-106">You can control in Azure AD who has access tooSCC LifeCycle</span></span>
- <span data-ttu-id="78dd4-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSCC du cycle de vie (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="78dd4-107">You can enable your users tooautomatically get signed-on tooSCC LifeCycle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="78dd4-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="78dd4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="78dd4-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="78dd4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78dd4-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="78dd4-110">Prerequisites</span></span>

<span data-ttu-id="78dd4-111">tooconfigure intégration d’Azure AD avec SCC LifeCycle, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="78dd4-111">tooconfigure Azure AD integration with SCC LifeCycle, you need hello following items:</span></span>

- <span data-ttu-id="78dd4-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="78dd4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="78dd4-113">Un abonnement SCC LifeCycle pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="78dd4-113">An SCC LifeCycle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="78dd4-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="78dd4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="78dd4-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="78dd4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="78dd4-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="78dd4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="78dd4-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="78dd4-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="78dd4-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="78dd4-118">Scenario description</span></span>
<span data-ttu-id="78dd4-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="78dd4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="78dd4-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="78dd4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="78dd4-121">Ajout de SCC LifeCycle à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="78dd4-121">Adding SCC LifeCycle from hello gallery</span></span>
2. <span data-ttu-id="78dd4-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="78dd4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scc-lifecycle-from-hello-gallery"></a><span data-ttu-id="78dd4-123">Ajout de SCC LifeCycle à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="78dd4-123">Adding SCC LifeCycle from hello gallery</span></span>
<span data-ttu-id="78dd4-124">tooconfigure hello intégration de SCC LifeCycle dans Azure AD, vous devez tooadd SCC LifeCycle à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="78dd4-124">tooconfigure hello integration of SCC LifeCycle into Azure AD, you need tooadd SCC LifeCycle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="78dd4-125">**tooadd SCC LifeCycle à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="78dd4-125">**tooadd SCC LifeCycle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="78dd4-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="78dd4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="78dd4-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="78dd4-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="78dd4-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="78dd4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="78dd4-133">Dans la zone de recherche de hello, tapez **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-133">In hello search box, type **SCC LifeCycle**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_search.png)

5. <span data-ttu-id="78dd4-135">Dans le volet de résultats hello, sélectionnez **SCC LifeCycle**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="78dd4-135">In hello results panel, select **SCC LifeCycle**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="78dd4-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="78dd4-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="78dd4-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SCC LifeCycle sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="78dd4-138">In this section, you configure and test Azure AD single sign-on with SCC LifeCycle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="78dd4-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans SCC LifeCycle est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78dd4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SCC LifeCycle is tooa user in Azure AD.</span></span> <span data-ttu-id="78dd4-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans SCC LifeCycle doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="78dd4-140">In other words, a link relationship between an Azure AD user and hello related user in SCC LifeCycle needs toobe established.</span></span>

<span data-ttu-id="78dd4-141">Dans SCC LifeCycle, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="78dd4-141">In SCC LifeCycle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="78dd4-142">tooconfigure et test Azure AD l’authentification unique avec SCC LifeCycle, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="78dd4-142">tooconfigure and test Azure AD single sign-on with SCC LifeCycle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="78dd4-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="78dd4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="78dd4-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="78dd4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="78dd4-145">**[Création d’un utilisateur de test SCC LifeCycle](#creating-an-scc-lifecycle-test-user)**  -toohave un équivalent de Britta Simon dans le cycle de vie de contrôle de code source qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="78dd4-145">**[Creating an SCC LifeCycle test user](#creating-an-scc-lifecycle-test-user)** - toohave a counterpart of Britta Simon in SCC LifeCycle that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="78dd4-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="78dd4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="78dd4-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="78dd4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="78dd4-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="78dd4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="78dd4-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="78dd4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SCC LifeCycle application.</span></span>

<span data-ttu-id="78dd4-150">**tooconfigure Azure AD single sign-on avec SCC LifeCycle, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="78dd4-150">**tooconfigure Azure AD single sign-on with SCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="78dd4-151">Bonjour portail Azure, sur hello **SCC LifeCycle** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-151">In hello Azure portal, on hello **SCC LifeCycle** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="78dd4-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="78dd4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_samlbase.png)

3. <span data-ttu-id="78dd4-155">Sur hello **SCC LifeCycle domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="78dd4-155">On hello **SCC LifeCycle Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_url.png)

    <span data-ttu-id="78dd4-157">a.</span><span class="sxs-lookup"><span data-stu-id="78dd4-157">a.</span></span> <span data-ttu-id="78dd4-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<sub-domain>.scc.com/ic7/welcome/customer/PICTtest.aspx`</span><span class="sxs-lookup"><span data-stu-id="78dd4-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<sub-domain>.scc.com/ic7/welcome/customer/PICTtest.aspx`</span></span>

    <span data-ttu-id="78dd4-159">b.</span><span class="sxs-lookup"><span data-stu-id="78dd4-159">b.</span></span> <span data-ttu-id="78dd4-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="78dd4-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|--|
    | `https://bs1.scc.com/<entity>`|
    | `https://lifecycle.scc.com/<entity>`|
    
    > [!NOTE] 
    > <span data-ttu-id="78dd4-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="78dd4-161">These values are not real.</span></span> <span data-ttu-id="78dd4-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="78dd4-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="78dd4-163">Contact [équipe de support technique SCC LifeCycle Client](mailto:lifecycle.support@scc.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="78dd4-163">Contact [SCC LifeCycle Client support team](mailto:lifecycle.support@scc.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="78dd4-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="78dd4-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_certificate.png) 

5. <span data-ttu-id="78dd4-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="78dd4-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="78dd4-168">tooconfigure l’authentification unique sur **SCC LifeCycle** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support technique SCC LifeCycle](mailto:lifecycle.support@scc.com).</span><span class="sxs-lookup"><span data-stu-id="78dd4-168">tooconfigure single sign-on on **SCC LifeCycle** side, you need toosend hello downloaded **Metadata XML** too[SCC LifeCycle support team](mailto:lifecycle.support@scc.com).</span></span> <span data-ttu-id="78dd4-169">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="78dd4-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

     >[!NOTE]
   ><span data-ttu-id="78dd4-170">L’authentification unique a toobe activé par l’équipe de support technique SCC LifeCycle de hello.</span><span class="sxs-lookup"><span data-stu-id="78dd4-170">Single sign-on has toobe enabled by hello SCC LifeCycle support team.</span></span>
   > 
   > 

> [!TIP]
> <span data-ttu-id="78dd4-171">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="78dd4-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="78dd4-172">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="78dd4-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="78dd4-173">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="78dd4-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="78dd4-174">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="78dd4-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="78dd4-175">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="78dd4-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="78dd4-177">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="78dd4-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="78dd4-178">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="78dd4-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="78dd4-180">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="78dd4-182">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="78dd4-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="78dd4-184">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="78dd4-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="78dd4-186">a.</span><span class="sxs-lookup"><span data-stu-id="78dd4-186">a.</span></span> <span data-ttu-id="78dd4-187">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="78dd4-188">b.</span><span class="sxs-lookup"><span data-stu-id="78dd4-188">b.</span></span> <span data-ttu-id="78dd4-189">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="78dd4-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="78dd4-190">c.</span><span class="sxs-lookup"><span data-stu-id="78dd4-190">c.</span></span> <span data-ttu-id="78dd4-191">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="78dd4-192">d.</span><span class="sxs-lookup"><span data-stu-id="78dd4-192">d.</span></span> <span data-ttu-id="78dd4-193">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-193">Click **Create**.</span></span>
 
### <a name="creating-an-scc-lifecycle-test-user"></a><span data-ttu-id="78dd4-194">Création d’un utilisateur de test SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="78dd4-194">Creating an SCC LifeCycle test user</span></span>

<span data-ttu-id="78dd4-195">Dans l’ordre tooenable Azure AD les utilisateurs toolog à SCC LifeCycle, ils doivent être configurés à SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="78dd4-195">In order tooenable Azure AD users toolog into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="78dd4-196">Il n’existe aucun élément d’action pour vous tooconfigure configuration de l’utilisateur tooSCC du cycle de vie.</span><span class="sxs-lookup"><span data-stu-id="78dd4-196">There is no action item for you tooconfigure user provisioning tooSCC LifeCycle.</span></span>

<span data-ttu-id="78dd4-197">Lorsqu’un toolog tentatives utilisateur affecté à SCC LifeCycle, un compte SCC LifeCycle est créé automatiquement si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="78dd4-197">When an assigned user tries toolog into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

> [!NOTE]
    > <span data-ttu-id="78dd4-198">titulaire du compte Azure Active Directory Hello reçoit un message électronique et suit un tooconfirm de lier leur compte avant son activation.</span><span class="sxs-lookup"><span data-stu-id="78dd4-198">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="78dd4-199">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="78dd4-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="78dd4-200">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSCC du cycle de vie.</span><span class="sxs-lookup"><span data-stu-id="78dd4-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSCC LifeCycle.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="78dd4-202">**tooassign Britta Simon tooSCC cycle de vie, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="78dd4-202">**tooassign Britta Simon tooSCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="78dd4-203">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="78dd4-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications.**</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="78dd4-205">Dans la liste des applications hello, sélectionnez **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-205">In hello applications list, select **SCC LifeCycle**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_app.png) 

3. <span data-ttu-id="78dd4-207">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="78dd4-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-209">Click **Add** button.</span></span> <span data-ttu-id="78dd4-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="78dd4-212">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="78dd4-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="78dd4-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="78dd4-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="78dd4-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="78dd4-215">Testing single sign-on</span></span>

<span data-ttu-id="78dd4-216">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="78dd4-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="78dd4-217">Lorsque vous cliquez sur hello SCC LifeCycle vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooSCC cycle de vie des applications.</span><span class="sxs-lookup"><span data-stu-id="78dd4-217">When you click hello SCC LifeCycle tile in hello Access Panel, you should get automatically signed-on tooSCC LifeCycle application.</span></span>
<span data-ttu-id="78dd4-218">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="78dd4-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="78dd4-219">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="78dd4-219">Additional resources</span></span>

* [<span data-ttu-id="78dd4-220">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="78dd4-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="78dd4-221">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="78dd4-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_203.png

