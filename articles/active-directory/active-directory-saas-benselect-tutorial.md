---
title: "Didacticiel : Intégration d’Azure Active Directory à BenSelect | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et BenSelect."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffa17478-3ea1-4356-a289-545b5b9a4494
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: c3705da337bf8f6e76de58cd21c5b047c8f5e12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benselect"></a><span data-ttu-id="8a47f-103">Didacticiel : Intégration d'Azure Active Directory à BenSelect</span><span class="sxs-lookup"><span data-stu-id="8a47f-103">Tutorial: Azure Active Directory integration with BenSelect</span></span>

<span data-ttu-id="8a47f-104">Dans ce didacticiel, vous apprendrez comment toointegrate BenSelect avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8a47f-104">In this tutorial, you learn how toointegrate BenSelect with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8a47f-105">Intégration BenSelect à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="8a47f-105">Integrating BenSelect with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8a47f-106">Vous pouvez contrôler dans Azure AD qui a accès tooBenSelect</span><span class="sxs-lookup"><span data-stu-id="8a47f-106">You can control in Azure AD who has access tooBenSelect</span></span>
- <span data-ttu-id="8a47f-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooBenSelect (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a47f-107">You can enable your users tooautomatically get signed-on tooBenSelect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8a47f-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="8a47f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8a47f-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8a47f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a47f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8a47f-110">Prerequisites</span></span>

<span data-ttu-id="8a47f-111">tooconfigure intégration d’Azure AD avec BenSelect, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8a47f-111">tooconfigure Azure AD integration with BenSelect, you need hello following items:</span></span>

- <span data-ttu-id="8a47f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a47f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8a47f-113">Un abonnement BenSelect pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="8a47f-113">A BenSelect single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8a47f-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="8a47f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8a47f-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="8a47f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8a47f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8a47f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8a47f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8a47f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8a47f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="8a47f-118">Scenario description</span></span>
<span data-ttu-id="8a47f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="8a47f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8a47f-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="8a47f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8a47f-121">Ajout de BenSelect à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="8a47f-121">Adding BenSelect from hello gallery</span></span>
2. <span data-ttu-id="8a47f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a47f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benselect-from-hello-gallery"></a><span data-ttu-id="8a47f-123">Ajout de BenSelect à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="8a47f-123">Adding BenSelect from hello gallery</span></span>
<span data-ttu-id="8a47f-124">intégration de hello tooconfigure de BenSelect dans Azure AD, vous devez tooadd BenSelect à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="8a47f-124">tooconfigure hello integration of BenSelect into Azure AD, you need tooadd BenSelect from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8a47f-125">**tooadd BenSelect à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8a47f-125">**tooadd BenSelect from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a47f-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="8a47f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8a47f-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="8a47f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8a47f-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8a47f-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="8a47f-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8a47f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="8a47f-133">Dans la zone de recherche de hello, tapez **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="8a47f-133">In hello search box, type **BenSelect**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_search.png)

5. <span data-ttu-id="8a47f-135">Dans le volet de résultats hello, sélectionnez **BenSelect**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8a47f-135">In hello results panel, select **BenSelect**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8a47f-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a47f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8a47f-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec BenSelect avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="8a47f-138">In this section, you configure and test Azure AD single sign-on with BenSelect based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8a47f-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans BenSelect est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a47f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BenSelect is tooa user in Azure AD.</span></span> <span data-ttu-id="8a47f-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans BenSelect doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="8a47f-140">In other words, a link relationship between an Azure AD user and hello related user in BenSelect needs toobe established.</span></span>

<span data-ttu-id="8a47f-141">Dans BenSelect, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="8a47f-141">In BenSelect, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8a47f-142">tooconfigure et test Azure AD l’authentification unique avec BenSelect, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="8a47f-142">tooconfigure and test Azure AD single sign-on with BenSelect, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8a47f-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8a47f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8a47f-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8a47f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8a47f-145">**[Création d’un utilisateur de test BenSelect](#creating-a-benselect-test-user)**  -toohave un équivalent de Britta Simon dans BenSelect est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8a47f-145">**[Creating a BenSelect test user](#creating-a-benselect-test-user)** - toohave a counterpart of Britta Simon in BenSelect that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8a47f-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8a47f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8a47f-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="8a47f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8a47f-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a47f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8a47f-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application BenSelect.</span><span class="sxs-lookup"><span data-stu-id="8a47f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BenSelect application.</span></span>

<span data-ttu-id="8a47f-150">**tooconfigure Azure AD single sign-on avec BenSelect, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8a47f-150">**tooconfigure Azure AD single sign-on with BenSelect, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a47f-151">Bonjour portail Azure, sur hello **BenSelect** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="8a47f-151">In hello Azure portal, on hello **BenSelect** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="8a47f-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8a47f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_samlbase.png)

3. <span data-ttu-id="8a47f-155">Sur hello **BenSelect domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8a47f-155">On hello **BenSelect Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_url.png)

    <span data-ttu-id="8a47f-157">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="8a47f-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8a47f-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="8a47f-158">This value is not real.</span></span> <span data-ttu-id="8a47f-159">Mettre à jour cette valeur avec l’URL de réponse réelle hello.</span><span class="sxs-lookup"><span data-stu-id="8a47f-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="8a47f-160">Contact [équipe de support BenSelect](mailto:support@selerix.com) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="8a47f-160">Contact [BenSelect support team](mailto:support@selerix.com) tooget this value.</span></span>
 
4. <span data-ttu-id="8a47f-161">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Raw)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8a47f-161">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_certificate.png) 

5. <span data-ttu-id="8a47f-163">BenSelect application attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="8a47f-163">BenSelect application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="8a47f-164">Configurer hello suivant des revendications pour cette application.</span><span class="sxs-lookup"><span data-stu-id="8a47f-164">Configure hello following claims for this application.</span></span> <span data-ttu-id="8a47f-165">Vous pouvez gérer les valeurs de ces attributs hello depuis hello **attributs utilisateur** section sur la page d’intégration d’application.</span><span class="sxs-lookup"><span data-stu-id="8a47f-165">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="8a47f-166">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="8a47f-166">hello following screenshot shows an example for this.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_06.png)

6. <span data-ttu-id="8a47f-168">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="8a47f-168">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="8a47f-169">a.</span><span class="sxs-lookup"><span data-stu-id="8a47f-169">a.</span></span> <span data-ttu-id="8a47f-170">Bonjour **identificateur de l’utilisateur** liste déroulante, sélectionnez **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="8a47f-170">In hello **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="8a47f-171">b.</span><span class="sxs-lookup"><span data-stu-id="8a47f-171">b.</span></span> <span data-ttu-id="8a47f-172">Bonjour **Mail** liste déroulante, sélectionnez **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="8a47f-172">In hello **Mail** dropdown list, select **user.userprincipalname**.</span></span>

7. <span data-ttu-id="8a47f-173">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="8a47f-173">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-benselect-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8a47f-175">Sur hello **BenSelect Configuration** , cliquez sur **BenSelect de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="8a47f-175">On hello **BenSelect Configuration** section, click **Configure BenSelect** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8a47f-176">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="8a47f-176">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_configure.png) 

9. <span data-ttu-id="8a47f-178">tooconfigure l’authentification unique sur **BenSelect** côté, vous devez hello toosend téléchargé **Certificate(Raw)** et **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique**trop[équipe de support BenSelect](mailto:support@selerix.com).</span><span class="sxs-lookup"><span data-stu-id="8a47f-178">tooconfigure single sign-on on **BenSelect** side, you need toosend hello downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[BenSelect support team](mailto:support@selerix.com).</span></span>

   >[!NOTE]
   ><span data-ttu-id="8a47f-179">Vous devez toomention cette intégration nécessite une algorithme hello SHA256 (SHA1 n’est pas pris en charge) tooset hello SSO sur serveur approprié de hello comme app2101 etc..</span><span class="sxs-lookup"><span data-stu-id="8a47f-179">You need toomention that this integration requires hello SHA256 algorithm (SHA1 is not supported) tooset hello SSO on hello appropriate server like app2101 etc.</span></span> 
   
> [!TIP]
> <span data-ttu-id="8a47f-180">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="8a47f-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8a47f-181">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="8a47f-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8a47f-182">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8a47f-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8a47f-183">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a47f-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="8a47f-184">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="8a47f-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="8a47f-186">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8a47f-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a47f-187">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="8a47f-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8a47f-189">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8a47f-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8a47f-191">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="8a47f-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8a47f-193">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8a47f-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8a47f-195">a.</span><span class="sxs-lookup"><span data-stu-id="8a47f-195">a.</span></span> <span data-ttu-id="8a47f-196">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8a47f-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8a47f-197">b.</span><span class="sxs-lookup"><span data-stu-id="8a47f-197">b.</span></span> <span data-ttu-id="8a47f-198">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8a47f-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8a47f-199">c.</span><span class="sxs-lookup"><span data-stu-id="8a47f-199">c.</span></span> <span data-ttu-id="8a47f-200">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="8a47f-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8a47f-201">d.</span><span class="sxs-lookup"><span data-stu-id="8a47f-201">d.</span></span> <span data-ttu-id="8a47f-202">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="8a47f-202">Click **Create**.</span></span>
 
### <a name="creating-a-benselect-test-user"></a><span data-ttu-id="8a47f-203">Création d’un utilisateur test BenSelect</span><span class="sxs-lookup"><span data-stu-id="8a47f-203">Creating a BenSelect test user</span></span>

<span data-ttu-id="8a47f-204">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans BenSelect.</span><span class="sxs-lookup"><span data-stu-id="8a47f-204">hello objective of this section is toocreate a user called Britta Simon in BenSelect.</span></span> <span data-ttu-id="8a47f-205">Travailler avec [équipe de support BenSelect](mailto:support@selerix.com) utilisateurs hello tooadd hello BenSelect compte.</span><span class="sxs-lookup"><span data-stu-id="8a47f-205">Work with [BenSelect support team](mailto:support@selerix.com) tooadd hello users in hello BenSelect account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8a47f-206">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a47f-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8a47f-207">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooBenSelect.</span><span class="sxs-lookup"><span data-stu-id="8a47f-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBenSelect.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="8a47f-209">**tooassign Britta Simon tooBenSelect, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8a47f-209">**tooassign Britta Simon tooBenSelect, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a47f-210">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8a47f-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="8a47f-212">Dans la liste des applications hello, sélectionnez **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="8a47f-212">In hello applications list, select **BenSelect**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_app.png) 

3. <span data-ttu-id="8a47f-214">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8a47f-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="8a47f-216">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8a47f-216">Click **Add** button.</span></span> <span data-ttu-id="8a47f-217">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8a47f-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="8a47f-219">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="8a47f-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8a47f-220">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8a47f-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8a47f-221">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8a47f-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8a47f-222">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="8a47f-222">Testing single sign-on</span></span>

<span data-ttu-id="8a47f-223">Dans cette section, vous tester votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="8a47f-223">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="8a47f-224">Lorsque vous cliquez sur mosaïque BenSelect hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour BenSelect application.</span><span class="sxs-lookup"><span data-stu-id="8a47f-224">When you click hello BenSelect tile in hello Access Panel, you should get automatically signed-on tooyour BenSelect application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8a47f-225">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8a47f-225">Additional resources</span></span>

* [<span data-ttu-id="8a47f-226">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a47f-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8a47f-227">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="8a47f-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_203.png

