---
title: "Didacticiel : Intégration d’Azure Active Directory avec LogicMonitor | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de LogicMonitor."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 496156c3-0e22-4492-b36f-2c29c055e087
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: ea5cb8b574d763cb114286e3b2a5c94ab5546756
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-logicmonitor"></a><span data-ttu-id="41585-103">Didacticiel : Intégration d’Azure Active Directory à LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="41585-103">Tutorial: Azure Active Directory integration with LogicMonitor</span></span>

<span data-ttu-id="41585-104">Dans ce didacticiel, vous apprendrez comment toointegrate LogicMonitor avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="41585-104">In this tutorial, you learn how toointegrate LogicMonitor with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="41585-105">Intégration de LogicMonitor à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="41585-105">Integrating LogicMonitor with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="41585-106">Vous pouvez contrôler dans Azure AD qui a accès tooLogicMonitor</span><span class="sxs-lookup"><span data-stu-id="41585-106">You can control in Azure AD who has access tooLogicMonitor</span></span>
- <span data-ttu-id="41585-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooLogicMonitor (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="41585-107">You can enable your users tooautomatically get signed-on tooLogicMonitor (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="41585-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="41585-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="41585-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="41585-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41585-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="41585-110">Prerequisites</span></span>

<span data-ttu-id="41585-111">tooconfigure intégration d’Azure AD à LogicMonitor, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="41585-111">tooconfigure Azure AD integration with LogicMonitor, you need hello following items:</span></span>

- <span data-ttu-id="41585-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="41585-112">An Azure AD subscription</span></span>
- <span data-ttu-id="41585-113">Un abonnement LogicMonitor pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="41585-113">A LogicMonitor single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="41585-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="41585-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="41585-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="41585-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="41585-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="41585-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="41585-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="41585-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="41585-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="41585-118">Scenario description</span></span>
<span data-ttu-id="41585-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="41585-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="41585-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="41585-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="41585-121">Ajout de LogicMonitor à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="41585-121">Adding LogicMonitor from hello gallery</span></span>
2. <span data-ttu-id="41585-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="41585-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-logicmonitor-from-hello-gallery"></a><span data-ttu-id="41585-123">Ajout de LogicMonitor à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="41585-123">Adding LogicMonitor from hello gallery</span></span>
<span data-ttu-id="41585-124">intégration de hello tooconfigure de LogicMonitor dans Azure AD, vous devez tooadd LogicMonitor à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="41585-124">tooconfigure hello integration of LogicMonitor into Azure AD, you need tooadd LogicMonitor from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="41585-125">**tooadd LogicMonitor à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="41585-125">**tooadd LogicMonitor from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="41585-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="41585-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="41585-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="41585-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="41585-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="41585-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="41585-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="41585-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="41585-133">Dans la zone de recherche de hello, tapez **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="41585-133">In hello search box, type **LogicMonitor**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_search.png)

5. <span data-ttu-id="41585-135">Dans le volet de résultats hello, sélectionnez **LogicMonitor**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="41585-135">In hello results panel, select **LogicMonitor**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="41585-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="41585-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="41585-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec LogicMonitor, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="41585-138">In this section, you configure and test Azure AD single sign-on with LogicMonitor based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="41585-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans LogicMonitor est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="41585-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LogicMonitor is tooa user in Azure AD.</span></span> <span data-ttu-id="41585-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans LogicMonitor doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="41585-140">In other words, a link relationship between an Azure AD user and hello related user in LogicMonitor needs toobe established.</span></span>

<span data-ttu-id="41585-141">Dans LogicMonitor, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="41585-141">In LogicMonitor, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="41585-142">tooconfigure et test Azure AD l’authentification unique avec LogicMonitor, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="41585-142">tooconfigure and test Azure AD single sign-on with LogicMonitor, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="41585-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="41585-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="41585-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="41585-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="41585-145">**[Création d’un utilisateur de test de LogicMonitor](#creating-a-logicmonitor-test-user)**  -toohave un équivalent de Britta Simon dans LogicMonitor est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="41585-145">**[Creating a LogicMonitor test user](#creating-a-logicmonitor-test-user)** - toohave a counterpart of Britta Simon in LogicMonitor that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="41585-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="41585-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="41585-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="41585-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="41585-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="41585-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="41585-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="41585-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LogicMonitor application.</span></span>

<span data-ttu-id="41585-150">**tooconfigure Azure AD single sign-on avec LogicMonitor, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="41585-150">**tooconfigure Azure AD single sign-on with LogicMonitor, perform hello following steps:**</span></span>

1. <span data-ttu-id="41585-151">Bonjour portail Azure, sur hello **LogicMonitor** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="41585-151">In hello Azure portal, on hello **LogicMonitor** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="41585-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="41585-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_samlbase.png)

3. <span data-ttu-id="41585-155">Sur hello **LogicMonitor domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="41585-155">On hello **LogicMonitor Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_url.png)

    <span data-ttu-id="41585-157">a.</span><span class="sxs-lookup"><span data-stu-id="41585-157">a.</span></span> <span data-ttu-id="41585-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="41585-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    <span data-ttu-id="41585-159">b.</span><span class="sxs-lookup"><span data-stu-id="41585-159">b.</span></span> <span data-ttu-id="41585-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="41585-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="41585-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="41585-161">These values are not real.</span></span> <span data-ttu-id="41585-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="41585-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="41585-163">Contact [équipe de support Client de LogicMonitor](https://www.logicmonitor.com/contact/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="41585-163">Contact [LogicMonitor Client support team](https://www.logicmonitor.com/contact/) tooget these values.</span></span> 
 


4. <span data-ttu-id="41585-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="41585-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_certificate.png) 

5. <span data-ttu-id="41585-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="41585-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="41585-168">Connectez-vous à tooyour **LogicMonitor** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="41585-168">Log in tooyour **LogicMonitor** company site as an administrator.</span></span>

7. <span data-ttu-id="41585-169">Dans le menu hello haut de hello, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="41585-169">In hello menu on hello top, click **Settings**.</span></span>
   
   <span data-ttu-id="41585-170">![Paramètres](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="41585-170">![Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Settings")</span></span>

8. <span data-ttu-id="41585-171">Dans la barre de navigation de hello sur le côté gauche de hello, cliquez sur **Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="41585-171">In hello navigation bat on hello left side, click **Single Sign On**</span></span>
   
   <span data-ttu-id="41585-172">![Authentification unique](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="41585-172">![Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Single Sign-On")</span></span>

9. <span data-ttu-id="41585-173">Bonjour **Single Sign-on (SSO) paramètres** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="41585-173">In hello **Single Sign-on (SSO) settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="41585-174">![Paramètres d’authentification unique](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "paramètres d’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="41585-174">![Single Sign-On Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="41585-175">a.</span><span class="sxs-lookup"><span data-stu-id="41585-175">a.</span></span> <span data-ttu-id="41585-176">Sélectionnez **Enable Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="41585-176">Select **Enable Single Sign-on**.</span></span>

   <span data-ttu-id="41585-177">b.</span><span class="sxs-lookup"><span data-stu-id="41585-177">b.</span></span> <span data-ttu-id="41585-178">Pour **Default Role Assignment**, sélectionnez **readonly**.</span><span class="sxs-lookup"><span data-stu-id="41585-178">As **Default Role Assignment**, select **readonly**.</span></span>
   
   <span data-ttu-id="41585-179">c.</span><span class="sxs-lookup"><span data-stu-id="41585-179">c.</span></span> <span data-ttu-id="41585-180">Ouvrez le fichier de métadonnées hello téléchargé dans le bloc-notes, puis collez le contenu du fichier de hello en hello **métadonnées du fournisseur d’identité** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="41585-180">Open hello downloaded metadata file in notepad, and then paste content of hello file into hello **Identity Provider Metadata** textbox.</span></span>
   
   <span data-ttu-id="41585-181">d.</span><span class="sxs-lookup"><span data-stu-id="41585-181">d.</span></span> <span data-ttu-id="41585-182">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="41585-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="41585-183">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="41585-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="41585-184">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="41585-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="41585-185">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="41585-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="41585-186">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="41585-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="41585-187">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="41585-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="41585-189">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="41585-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="41585-190">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="41585-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="41585-192">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="41585-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="41585-194">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="41585-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="41585-196">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="41585-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="41585-198">a.</span><span class="sxs-lookup"><span data-stu-id="41585-198">a.</span></span> <span data-ttu-id="41585-199">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="41585-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="41585-200">b.</span><span class="sxs-lookup"><span data-stu-id="41585-200">b.</span></span> <span data-ttu-id="41585-201">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="41585-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="41585-202">c.</span><span class="sxs-lookup"><span data-stu-id="41585-202">c.</span></span> <span data-ttu-id="41585-203">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="41585-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="41585-204">d.</span><span class="sxs-lookup"><span data-stu-id="41585-204">d.</span></span> <span data-ttu-id="41585-205">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="41585-205">Click **Create**.</span></span>
 
### <a name="creating-a-logicmonitor-test-user"></a><span data-ttu-id="41585-206">Création d’un utilisateur de test de LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="41585-206">Creating a LogicMonitor test user</span></span>

<span data-ttu-id="41585-207">Pour AAD utilisateurs toobe en mesure de toosign dans, ils doivent être mis en service toohello application LogicMonitor à l’aide de leur nom d’utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="41585-207">For AAD users toobe able toosign in, they must be provisioned toohello LogicMonitor application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="41585-208">**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="41585-208">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="41585-209">Ouvrez une session dans tooyour site d’entreprise LogicMonitor en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="41585-209">Log in tooyour LogicMonitor company site as an administrator.</span></span>

2. <span data-ttu-id="41585-210">Dans le menu hello haut de hello, cliquez sur **paramètres**, puis cliquez sur **rôles et les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="41585-210">In hello menu on hello top, click **Settings**, and then click **Roles and Users**.</span></span>
   
   <span data-ttu-id="41585-211">![Rôles et utilisateurs](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Rôles et utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="41585-211">![Roles and Users](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Roles and Users")</span></span>

3. <span data-ttu-id="41585-212">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="41585-212">Click **Add**.</span></span>

4. <span data-ttu-id="41585-213">Bonjour **ajouter un compte** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="41585-213">In hello **Add an account** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="41585-214">![Ajouter un compte](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Ajouter un compte")</span><span class="sxs-lookup"><span data-stu-id="41585-214">![Add an account](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Add an account")</span></span>
   
   <span data-ttu-id="41585-215">a.</span><span class="sxs-lookup"><span data-stu-id="41585-215">a.</span></span> <span data-ttu-id="41585-216">Hello de type **nom d’utilisateur**, **messagerie**, **mot de passe**, et **retapez le mot de passe** valeurs de hello Azure Active Directory utilisateur tooprovision dans hello relatives des zones de texte.</span><span class="sxs-lookup"><span data-stu-id="41585-216">Type hello **Username**, **Email**, **Password**, and **Retype password** values of hello Azure Active Directory user you want tooprovision into hello related textboxes.</span></span>
   
   <span data-ttu-id="41585-217">b.</span><span class="sxs-lookup"><span data-stu-id="41585-217">b.</span></span> <span data-ttu-id="41585-218">Sélectionnez **rôles**, **les autorisations d’affichage**et hello **état**.</span><span class="sxs-lookup"><span data-stu-id="41585-218">Select **Roles**, **View Permissions**, and hello **Status**.</span></span>
   
   <span data-ttu-id="41585-219">c.</span><span class="sxs-lookup"><span data-stu-id="41585-219">c.</span></span> <span data-ttu-id="41585-220">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="41585-220">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="41585-221">Vous pouvez utiliser n’importe quel autre LogicMonitor utilisateur compte outil de création ou API fournie par LogicMonitor tooprovision Azure Active Directory des comptes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="41585-221">You can use any other LogicMonitor user account creation tools or APIs provided by LogicMonitor tooprovision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="41585-222">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="41585-222">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="41585-223">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooLogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="41585-223">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLogicMonitor.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="41585-225">**tooassign Britta Simon tooLogicMonitor, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="41585-225">**tooassign Britta Simon tooLogicMonitor, perform hello following steps:**</span></span>

1. <span data-ttu-id="41585-226">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="41585-226">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="41585-228">Dans la liste des applications hello, sélectionnez **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="41585-228">In hello applications list, select **LogicMonitor**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_app.png) 

3. <span data-ttu-id="41585-230">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="41585-230">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="41585-232">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="41585-232">Click **Add** button.</span></span> <span data-ttu-id="41585-233">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="41585-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="41585-235">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="41585-235">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="41585-236">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="41585-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="41585-237">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="41585-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="41585-238">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="41585-238">Testing single sign-on</span></span>

<span data-ttu-id="41585-239">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="41585-239">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="41585-240">Lorsque vous cliquez sur mosaïque LogicMonitor hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour LogicMonitor application.</span><span class="sxs-lookup"><span data-stu-id="41585-240">When you click hello LogicMonitor tile in hello Access Panel, you should get automatically signed-on tooyour LogicMonitor application.</span></span>
<span data-ttu-id="41585-241">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="41585-241">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="41585-242">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="41585-242">Additional resources</span></span>

* [<span data-ttu-id="41585-243">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="41585-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="41585-244">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="41585-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_203.png

