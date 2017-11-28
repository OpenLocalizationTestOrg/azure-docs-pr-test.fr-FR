---
title: "Didacticiel : Intégration d’Azure Active Directory à UNIFI | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et UNIFI."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1f49ee4-d2d4-4a82-9baf-0587ca1f20f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: af7cc1167b5c0cff2a1f4cdaa8a2b93f5a718f81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-unifi"></a><span data-ttu-id="d026a-103">Didacticiel : Intégration d’Azure Active Directory à UNIFI</span><span class="sxs-lookup"><span data-stu-id="d026a-103">Tutorial: Azure Active Directory integration with UNIFI</span></span>

<span data-ttu-id="d026a-104">Dans ce didacticiel, vous apprendrez comment toointegrate UNIFI avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d026a-104">In this tutorial, you learn how toointegrate UNIFI with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d026a-105">Intégration UNIFI à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="d026a-105">Integrating UNIFI with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d026a-106">Vous pouvez contrôler dans Azure AD qui a accès tooUNIFI</span><span class="sxs-lookup"><span data-stu-id="d026a-106">You can control in Azure AD who has access tooUNIFI</span></span>
- <span data-ttu-id="d026a-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooUNIFI (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="d026a-107">You can enable your users tooautomatically get signed-on tooUNIFI (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d026a-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="d026a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d026a-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d026a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d026a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d026a-110">Prerequisites</span></span>

<span data-ttu-id="d026a-111">tooconfigure intégration d’Azure AD avec UNIFI, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d026a-111">tooconfigure Azure AD integration with UNIFI, you need hello following items:</span></span>

- <span data-ttu-id="d026a-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="d026a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d026a-113">Un abonnement UNIFI pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="d026a-113">A UNIFI single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d026a-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="d026a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d026a-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="d026a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d026a-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d026a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d026a-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d026a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d026a-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="d026a-118">Scenario description</span></span>
<span data-ttu-id="d026a-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="d026a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d026a-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="d026a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d026a-121">Ajout de UNIFI à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="d026a-121">Adding UNIFI from hello gallery</span></span>
2. <span data-ttu-id="d026a-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d026a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-unifi-from-hello-gallery"></a><span data-ttu-id="d026a-123">Ajout de UNIFI à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="d026a-123">Adding UNIFI from hello gallery</span></span>
<span data-ttu-id="d026a-124">tooconfigure hello intégration de UNIFI dans Azure AD, vous devez tooadd UNIFI à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="d026a-124">tooconfigure hello integration of UNIFI into Azure AD, you need tooadd UNIFI from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d026a-125">**tooadd UNIFI à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d026a-125">**tooadd UNIFI from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d026a-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="d026a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d026a-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="d026a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d026a-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d026a-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="d026a-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d026a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="d026a-133">Dans la zone de recherche de hello, tapez **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="d026a-133">In hello search box, type **UNIFI**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_search.png)

5. <span data-ttu-id="d026a-135">Dans le volet de résultats hello, sélectionnez **UNIFI**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d026a-135">In hello results panel, select **UNIFI**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d026a-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d026a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d026a-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec UNIFI, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="d026a-138">In this section, you configure and test Azure AD single sign-on with UNIFI based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d026a-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello UNIFI est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d026a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UNIFI is tooa user in Azure AD.</span></span> <span data-ttu-id="d026a-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans UNIFI doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="d026a-140">In other words, a link relationship between an Azure AD user and hello related user in UNIFI needs toobe established.</span></span>

<span data-ttu-id="d026a-141">Dans UNIFI, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="d026a-141">In UNIFI, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d026a-142">tooconfigure et test Azure AD l’authentification unique avec UNIFI, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="d026a-142">tooconfigure and test Azure AD single sign-on with UNIFI, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d026a-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d026a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d026a-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d026a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d026a-145">**[Création d’un UNIFI utilisateur de test](#creating-a-unifi-test-user)**  -toohave un équivalent de Britta Simon dans UNIFI est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d026a-145">**[Creating a UNIFI test user](#creating-a-unifi-test-user)** - toohave a counterpart of Britta Simon in UNIFI that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d026a-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d026a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d026a-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="d026a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d026a-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d026a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d026a-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application UNIFI.</span><span class="sxs-lookup"><span data-stu-id="d026a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UNIFI application.</span></span>

<span data-ttu-id="d026a-150">**tooconfigure Azure AD single sign-on avec UNIFI, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d026a-150">**tooconfigure Azure AD single sign-on with UNIFI, perform hello following steps:**</span></span>

1. <span data-ttu-id="d026a-151">Bonjour portail Azure, sur hello **UNIFI** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="d026a-151">In hello Azure portal, on hello **UNIFI** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="d026a-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d026a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_samlbase.png)

3. <span data-ttu-id="d026a-155">Sur hello **UNIFI domaine et les URL** section, si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="d026a-155">On hello **UNIFI Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url1.png)

    <span data-ttu-id="d026a-157">Bonjour **identificateur** zone de texte, valeur de type hello :`INVIEWlabs`</span><span class="sxs-lookup"><span data-stu-id="d026a-157">In hello **Identifier** textbox, type hello value: `INVIEWlabs`</span></span> 

4. <span data-ttu-id="d026a-158">Vérifiez **afficher les paramètres d’URL avancés**, si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="d026a-158">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url2.png)

    <span data-ttu-id="d026a-160">Bonjour **URL de connexion** zone de texte, tapez l’URL hello :`https://app.discoverunifi.com/login`</span><span class="sxs-lookup"><span data-stu-id="d026a-160">In hello **Sign-on URL** textbox, type hello URL: `https://app.discoverunifi.com/login`</span></span>

5. <span data-ttu-id="d026a-161">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d026a-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_certificate.png) 

6. <span data-ttu-id="d026a-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="d026a-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-unifi-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="d026a-165">Sur hello **UNIFI Configuration** , cliquez sur **UNIFI de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="d026a-165">On hello **UNIFI Configuration** section, click **Configure UNIFI** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d026a-166">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="d026a-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_configure.png)

8. <span data-ttu-id="d026a-168">Dans une fenêtre de navigateur web, connectez-vous tooyour **UNIFI** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d026a-168">In a different web browser window, sign on tooyour **UNIFI** company site as administrator.</span></span>

9. <span data-ttu-id="d026a-169">Cliquez sur hello **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d026a-169">Click on hello **Users**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-unifi-tutorial/app1.png) 

10. <span data-ttu-id="d026a-171">Cliquez sur hello **Ajouter nouveau fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="d026a-171">Click on hello **Add New Identity Provider**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-unifi-tutorial/app2.png)

11. <span data-ttu-id="d026a-173">Bonjour **ajouter un fournisseur d’identité** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d026a-173">In hello **Add Identity Provider** section, perform hello following steps:</span></span>   

    ![Configurer l’authentification unique](./media/active-directory-saas-unifi-tutorial/app3.png) 

    <span data-ttu-id="d026a-175">a.</span><span class="sxs-lookup"><span data-stu-id="d026a-175">a.</span></span> <span data-ttu-id="d026a-176">Bonjour **nom du fournisseur** zone de texte, nom du type hello Hello fournisseur d’identité...</span><span class="sxs-lookup"><span data-stu-id="d026a-176">In hello **Provider Name** textbox, type hello name of hello Identity Provider..</span></span>

    <span data-ttu-id="d026a-177">b.</span><span class="sxs-lookup"><span data-stu-id="d026a-177">b.</span></span> <span data-ttu-id="d026a-178">Bonjour de hello **URL du fournisseur** textbox coller hello **SAML Sign-On URL du Service unique** valeur, qui vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d026a-178">In hello hello **Provider URL** textbox paste hello **SAML Single Sign-On Service URL** value, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d026a-179">c.</span><span class="sxs-lookup"><span data-stu-id="d026a-179">c.</span></span> <span data-ttu-id="d026a-180">Ouvrez hello de certificat que vous avez téléchargé à partir de hello portail Azure dans le bloc-notes, supprimez hello **---BEGIN CERTIFICATE---** et **---END CERTIFICATE---** balise, puis collez hello restant contenu dans Hello **certificat** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="d026a-180">Open hello Certificate that you have downloaded from hello Azure portal in notepad, remove hello **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste hello remaining content in hello **Certificate** textbox.</span></span>

    <span data-ttu-id="d026a-181">d.</span><span class="sxs-lookup"><span data-stu-id="d026a-181">d.</span></span> <span data-ttu-id="d026a-182">Sélectionnez hello **est le fournisseur par défaut** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="d026a-182">Select hello **is Default Provider** checkbox.</span></span>

> [!TIP]
> <span data-ttu-id="d026a-183">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="d026a-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d026a-184">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="d026a-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d026a-185">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d026a-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d026a-186">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d026a-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="d026a-187">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="d026a-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="d026a-189">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d026a-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d026a-190">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="d026a-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d026a-192">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d026a-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d026a-194">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="d026a-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d026a-196">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d026a-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d026a-198">a.</span><span class="sxs-lookup"><span data-stu-id="d026a-198">a.</span></span> <span data-ttu-id="d026a-199">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d026a-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d026a-200">b.</span><span class="sxs-lookup"><span data-stu-id="d026a-200">b.</span></span> <span data-ttu-id="d026a-201">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d026a-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d026a-202">c.</span><span class="sxs-lookup"><span data-stu-id="d026a-202">c.</span></span> <span data-ttu-id="d026a-203">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="d026a-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d026a-204">d.</span><span class="sxs-lookup"><span data-stu-id="d026a-204">d.</span></span> <span data-ttu-id="d026a-205">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="d026a-205">Click **Create**.</span></span>
 
### <a name="creating-a-unifi-test-user"></a><span data-ttu-id="d026a-206">Création d’un utilisateur de test UNIFI</span><span class="sxs-lookup"><span data-stu-id="d026a-206">Creating a UNIFI test user</span></span>

<span data-ttu-id="d026a-207">Dans cette section, vous allez créer un utilisateur appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d026a-207">In this section, you create a user called Britta Simon.</span></span> <span data-ttu-id="d026a-208">**UNIFI** prend en charge l’approvisionnement automatique de l’utilisateur. Par conséquent, aucune action manuelle n’est requise.</span><span class="sxs-lookup"><span data-stu-id="d026a-208">**UNIFI** supports automatic user provisioning so no manual steps are required.</span></span> <span data-ttu-id="d026a-209">Les utilisateurs sont créés automatiquement après une authentification réussie à partir de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d026a-209">Users are created automatically after successful authentication from hello Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d026a-210">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d026a-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d026a-211">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooUNIFI.</span><span class="sxs-lookup"><span data-stu-id="d026a-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUNIFI.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="d026a-213">**tooassign Britta Simon tooUNIFI, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d026a-213">**tooassign Britta Simon tooUNIFI, perform hello following steps:**</span></span>

1. <span data-ttu-id="d026a-214">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d026a-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="d026a-216">Dans la liste des applications hello, sélectionnez **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="d026a-216">In hello applications list, select **UNIFI**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_app.png) 

3. <span data-ttu-id="d026a-218">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d026a-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="d026a-220">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d026a-220">Click **Add** button.</span></span> <span data-ttu-id="d026a-221">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d026a-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="d026a-223">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="d026a-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d026a-224">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d026a-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d026a-225">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d026a-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d026a-226">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d026a-226">Testing single sign-on</span></span>

<span data-ttu-id="d026a-227">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="d026a-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d026a-228">Lorsque vous cliquez sur hello UNIFI vignette Bonjour volet d’accès, vous devez obtenir l’application de UNIFI tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="d026a-228">When you click hello UNIFI tile in hello Access Panel, you should get automatically signed-on tooyour UNIFI application.</span></span>
<span data-ttu-id="d026a-229">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d026a-229">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d026a-230">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d026a-230">Additional resources</span></span>

* [<span data-ttu-id="d026a-231">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d026a-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d026a-232">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="d026a-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_203.png

