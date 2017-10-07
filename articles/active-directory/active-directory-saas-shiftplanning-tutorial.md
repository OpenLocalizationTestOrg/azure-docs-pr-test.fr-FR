---
title: "Didacticiel : intégration d’Azure Active Directory à Humanity | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et l’humanité."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 7d8a04a2eb3c997f86f1e199c47809fa3dad60e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a><span data-ttu-id="ae568-103">Didacticiel : intégration d’Azure Active Directory à Humanity</span><span class="sxs-lookup"><span data-stu-id="ae568-103">Tutorial: Azure Active Directory integration with Humanity</span></span>

<span data-ttu-id="ae568-104">Dans ce didacticiel, vous apprendrez comment toointegrate humanité avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ae568-104">In this tutorial, you learn how toointegrate Humanity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae568-105">Intégration humanité à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ae568-105">Integrating Humanity with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ae568-106">Vous pouvez contrôler dans Azure AD qui a accès tooHumanity</span><span class="sxs-lookup"><span data-stu-id="ae568-106">You can control in Azure AD who has access tooHumanity</span></span>
- <span data-ttu-id="ae568-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooHumanity (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae568-107">You can enable your users tooautomatically get signed-on tooHumanity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ae568-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="ae568-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ae568-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ae568-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae568-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ae568-110">Prerequisites</span></span>

<span data-ttu-id="ae568-111">tooconfigure intégration d’Azure AD avec l’humanité, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ae568-111">tooconfigure Azure AD integration with Humanity, you need hello following items:</span></span>

- <span data-ttu-id="ae568-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae568-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ae568-113">Un abonnement Humanity pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="ae568-113">A Humanity single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ae568-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="ae568-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ae568-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="ae568-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ae568-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ae568-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ae568-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae568-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ae568-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="ae568-118">Scenario description</span></span>
<span data-ttu-id="ae568-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="ae568-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ae568-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="ae568-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ae568-121">Ajout de l’humanité à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="ae568-121">Adding Humanity from hello gallery</span></span>
2. <span data-ttu-id="ae568-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae568-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-humanity-from-hello-gallery"></a><span data-ttu-id="ae568-123">Ajout de l’humanité à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="ae568-123">Adding Humanity from hello gallery</span></span>
<span data-ttu-id="ae568-124">intégration de hello tooconfigure de l’humanité dans Azure AD, vous devez tooadd humanité à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="ae568-124">tooconfigure hello integration of Humanity into Azure AD, you need tooadd Humanity from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ae568-125">**tooadd humanité à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ae568-125">**tooadd Humanity from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae568-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="ae568-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ae568-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="ae568-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ae568-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ae568-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="ae568-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ae568-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="ae568-133">Dans la zone de recherche de hello, tapez **humanité**.</span><span class="sxs-lookup"><span data-stu-id="ae568-133">In hello search box, type **Humanity**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. <span data-ttu-id="ae568-135">Dans le volet de résultats hello, sélectionnez **humanité**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ae568-135">In hello results panel, select **Humanity**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ae568-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae568-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ae568-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Humanity, grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="ae568-138">In this section, you configure and test Azure AD single sign-on with Humanity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ae568-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello humanité est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae568-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Humanity is tooa user in Azure AD.</span></span> <span data-ttu-id="ae568-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans l’humanité hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="ae568-140">In other words, a link relationship between an Azure AD user and hello related user in Humanity needs toobe established.</span></span>

<span data-ttu-id="ae568-141">Dans l’humanité, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="ae568-141">In Humanity, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ae568-142">tooconfigure et test Azure AD l’authentification unique avec l’humanité, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="ae568-142">tooconfigure and test Azure AD single sign-on with Humanity, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ae568-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ae568-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ae568-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae568-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ae568-145">**[Création d’un utilisateur de test humanité](#creating-a-humanity-test-user)**  -toohave un équivalent de Britta Simon dans humanité est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ae568-145">**[Creating a Humanity test user](#creating-a-humanity-test-user)** - toohave a counterpart of Britta Simon in Humanity that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ae568-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ae568-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ae568-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="ae568-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ae568-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae568-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ae568-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application l’humanité.</span><span class="sxs-lookup"><span data-stu-id="ae568-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Humanity application.</span></span>

<span data-ttu-id="ae568-150">**tooconfigure Azure AD single sign-on avec humanité, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ae568-150">**tooconfigure Azure AD single sign-on with Humanity, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae568-151">Bonjour portail Azure, sur hello **humanité** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="ae568-151">In hello Azure portal, on hello **Humanity** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="ae568-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ae568-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. <span data-ttu-id="ae568-155">Sur hello **URL et le domaine de l’humanité** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ae568-155">On hello **Humanity Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    <span data-ttu-id="ae568-157">a.</span><span class="sxs-lookup"><span data-stu-id="ae568-157">a.</span></span> <span data-ttu-id="ae568-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://company.humanity.com/includes/saml/`</span><span class="sxs-lookup"><span data-stu-id="ae568-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://company.humanity.com/includes/saml/`</span></span>

    <span data-ttu-id="ae568-159">b.</span><span class="sxs-lookup"><span data-stu-id="ae568-159">b.</span></span> <span data-ttu-id="ae568-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://company.humanity.com/app/`</span><span class="sxs-lookup"><span data-stu-id="ae568-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://company.humanity.com/app/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ae568-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="ae568-161">These values are not real.</span></span> <span data-ttu-id="ae568-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="ae568-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ae568-163">Contact [équipe de support Client de l’humanité](https://www.humanity.com/support/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="ae568-163">Contact [Humanity Client support team](https://www.humanity.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="ae568-164">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ae568-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. <span data-ttu-id="ae568-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="ae568-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ae568-168">Sur hello **humanité Configuration** , cliquez sur **configurer l’humanité** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="ae568-168">On hello **Humanity Configuration** section, click **Configure Humanity** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ae568-169">Hello de copie **SAML Sign-On URL du Service unique et l’URL de déconnexion** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="ae568-169">Copy hello **SAML Single Sign-On Service URL, and Sign-Out URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. <span data-ttu-id="ae568-171">Dans une fenêtre de navigateur web, connectez-vous tooyour **humanité** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ae568-171">In a different web browser window, log in tooyour **Humanity** company site as an administrator.</span></span>

8. <span data-ttu-id="ae568-172">Dans le menu hello haut de hello, cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="ae568-172">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="ae568-173">![Administrateur](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="ae568-173">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

9. <span data-ttu-id="ae568-174">Sous **Integration**, cliquez sur **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="ae568-174">Under **Integration**, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="ae568-175">![Authentification unique](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="ae568-175">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Single Sign-On")</span></span>

10. <span data-ttu-id="ae568-176">Bonjour **Single Sign-On** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ae568-176">In hello **Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="ae568-177">![Authentification unique](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="ae568-177">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="ae568-178">a.</span><span class="sxs-lookup"><span data-stu-id="ae568-178">a.</span></span> <span data-ttu-id="ae568-179">Sélectionnez **SAML Enabled**.</span><span class="sxs-lookup"><span data-stu-id="ae568-179">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="ae568-180">b.</span><span class="sxs-lookup"><span data-stu-id="ae568-180">b.</span></span> <span data-ttu-id="ae568-181">Sélectionnez **Allow Password Login**.</span><span class="sxs-lookup"><span data-stu-id="ae568-181">Select **Allow Password Login**.</span></span>

    <span data-ttu-id="ae568-182">c.</span><span class="sxs-lookup"><span data-stu-id="ae568-182">c.</span></span> <span data-ttu-id="ae568-183">Hello de coller **SAML Sign-On URL du Service unique** valeur hello **URL de l’émetteur SAML** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="ae568-183">Paste hello **SAML Single Sign-On Service URL** value into hello **SAML Issuer URL** textbox.</span></span>

    <span data-ttu-id="ae568-184">d.</span><span class="sxs-lookup"><span data-stu-id="ae568-184">d.</span></span> <span data-ttu-id="ae568-185">Hello de coller **URL de déconnexion** valeur hello **URL de déconnexion distante** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="ae568-185">Paste hello **Sign-Out URL** value into hello **Remote Logout URL** textbox.</span></span>
   
    <span data-ttu-id="ae568-186">e.</span><span class="sxs-lookup"><span data-stu-id="ae568-186">e.</span></span> <span data-ttu-id="ae568-187">Ouvrez votre certificat codé en base 64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat X.509** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="ae568-187">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>

11. <span data-ttu-id="ae568-188">Cliquez sur **Save Settings**.</span><span class="sxs-lookup"><span data-stu-id="ae568-188">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="ae568-189">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="ae568-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ae568-190">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="ae568-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ae568-191">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ae568-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ae568-192">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae568-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="ae568-193">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="ae568-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="ae568-195">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ae568-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae568-196">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="ae568-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ae568-198">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ae568-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ae568-200">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="ae568-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ae568-202">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ae568-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ae568-204">a.</span><span class="sxs-lookup"><span data-stu-id="ae568-204">a.</span></span> <span data-ttu-id="ae568-205">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ae568-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ae568-206">b.</span><span class="sxs-lookup"><span data-stu-id="ae568-206">b.</span></span> <span data-ttu-id="ae568-207">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ae568-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ae568-208">c.</span><span class="sxs-lookup"><span data-stu-id="ae568-208">c.</span></span> <span data-ttu-id="ae568-209">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="ae568-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ae568-210">d.</span><span class="sxs-lookup"><span data-stu-id="ae568-210">d.</span></span> <span data-ttu-id="ae568-211">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="ae568-211">Click **Create**.</span></span>
 
### <a name="creating-a-humanity-test-user"></a><span data-ttu-id="ae568-212">Créer un utilisateur de test Humanity</span><span class="sxs-lookup"><span data-stu-id="ae568-212">Creating a Humanity test user</span></span>

<span data-ttu-id="ae568-213">Dans l’ordre tooenable Azure AD les utilisateurs toolog dans tooHumanity, vous devez les configurer dans l’humanité.</span><span class="sxs-lookup"><span data-stu-id="ae568-213">In order tooenable Azure AD users toolog in tooHumanity, they must be provisioned into Humanity.</span></span> <span data-ttu-id="ae568-214">Dans les cas de hello de l’humanité, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="ae568-214">In hello case of Humanity, provisioning is a manual task.</span></span>

<span data-ttu-id="ae568-215">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ae568-215">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae568-216">Connectez-vous à tooyour **humanité** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ae568-216">Log in tooyour **Humanity** company site as an administrator.</span></span>

2. <span data-ttu-id="ae568-217">Cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="ae568-217">Click **Admin**.</span></span>
   
    <span data-ttu-id="ae568-218">![Administrateur](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="ae568-218">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

3. <span data-ttu-id="ae568-219">Cliquez sur **Staff**.</span><span class="sxs-lookup"><span data-stu-id="ae568-219">Click **Staff**.</span></span>
   
    <span data-ttu-id="ae568-220">![Staff](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Staff")</span><span class="sxs-lookup"><span data-stu-id="ae568-220">![Staff](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Staff")</span></span>

4. <span data-ttu-id="ae568-221">Sous **Actions**, cliquez sur **Ajouter des employés**.</span><span class="sxs-lookup"><span data-stu-id="ae568-221">Under **Actions**, click **Add Employees**.</span></span>
   
    <span data-ttu-id="ae568-222">![Add Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Add Employees")</span><span class="sxs-lookup"><span data-stu-id="ae568-222">![Add Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Add Employees")</span></span>

5. <span data-ttu-id="ae568-223">Bonjour **ajouter des employés** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ae568-223">In hello **Add Employees** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="ae568-224">![Save Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Save Employees")</span><span class="sxs-lookup"><span data-stu-id="ae568-224">![Save Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Save Employees")</span></span>
   
    <span data-ttu-id="ae568-225">a.</span><span class="sxs-lookup"><span data-stu-id="ae568-225">a.</span></span> <span data-ttu-id="ae568-226">Hello de type **prénom**, **nom**, et **messagerie** d’un compte AAD valide que vous voulez tooprovision dans hello relatives des zones de texte.</span><span class="sxs-lookup"><span data-stu-id="ae568-226">Type hello **First Name**, **Last Name**, and **Email** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="ae568-227">b.</span><span class="sxs-lookup"><span data-stu-id="ae568-227">b.</span></span> <span data-ttu-id="ae568-228">Cliquez sur **Save Employees**.</span><span class="sxs-lookup"><span data-stu-id="ae568-228">Click **Save Employees**.</span></span>

>[!NOTE]
><span data-ttu-id="ae568-229">Vous pouvez utiliser n’importe quel autre humanité utilisateur compte outil de création ou API fournie par l’humanité tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="ae568-229">You can use any other Humanity user account creation tools or APIs provided by Humanity tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ae568-230">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae568-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ae568-231">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooHumanity.</span><span class="sxs-lookup"><span data-stu-id="ae568-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHumanity.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="ae568-233">**tooassign Britta Simon tooHumanity, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ae568-233">**tooassign Britta Simon tooHumanity, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae568-234">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ae568-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="ae568-236">Dans la liste des applications hello, sélectionnez **humanité**.</span><span class="sxs-lookup"><span data-stu-id="ae568-236">In hello applications list, select **Humanity**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. <span data-ttu-id="ae568-238">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ae568-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="ae568-240">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ae568-240">Click **Add** button.</span></span> <span data-ttu-id="ae568-241">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ae568-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="ae568-243">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="ae568-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ae568-244">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ae568-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ae568-245">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ae568-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ae568-246">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ae568-246">Testing single sign-on</span></span>

<span data-ttu-id="ae568-247">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="ae568-247">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ae568-248">Lorsque vous cliquez sur mosaïque humanité hello hello volet d’accès, vous devez obtenir l’application de l’humanité tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="ae568-248">When you click hello Humanity tile in hello Access Panel, you should get automatically signed-on tooyour Humanity application.</span></span>
<span data-ttu-id="ae568-249">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ae568-249">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ae568-250">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ae568-250">Additional resources</span></span>

* [<span data-ttu-id="ae568-251">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae568-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ae568-252">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="ae568-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png

