---
title: "Didacticiel : Intégration d’Azure Active Directory à OpsGenie | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et OpsGenie."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 41b59b22-a61d-4fe6-ab0d-6c3991d1375f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 50d31c234fb9716d05d681b9bc4164740a3a662b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-opsgenie"></a><span data-ttu-id="f245e-103">Didacticiel : Intégration d’Azure Active Directory à OpsGenie</span><span class="sxs-lookup"><span data-stu-id="f245e-103">Tutorial: Azure Active Directory integration with OpsGenie</span></span>

<span data-ttu-id="f245e-104">Dans ce didacticiel, vous apprendrez comment toointegrate OpsGenie avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f245e-104">In this tutorial, you learn how toointegrate OpsGenie with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f245e-105">Intégration OpsGenie à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="f245e-105">Integrating OpsGenie with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f245e-106">Vous pouvez contrôler dans Azure AD qui a accès tooOpsGenie</span><span class="sxs-lookup"><span data-stu-id="f245e-106">You can control in Azure AD who has access tooOpsGenie</span></span>
- <span data-ttu-id="f245e-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooOpsGenie (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="f245e-107">You can enable your users tooautomatically get signed-on tooOpsGenie (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f245e-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="f245e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f245e-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f245e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f245e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f245e-110">Prerequisites</span></span>

<span data-ttu-id="f245e-111">tooconfigure intégration d’Azure AD avec OpsGenie, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f245e-111">tooconfigure Azure AD integration with OpsGenie, you need hello following items:</span></span>

- <span data-ttu-id="f245e-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="f245e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f245e-113">Un abonnement OpsGenie pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="f245e-113">A OpsGenie single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f245e-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="f245e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f245e-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="f245e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f245e-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f245e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f245e-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f245e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f245e-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="f245e-118">Scenario description</span></span>
<span data-ttu-id="f245e-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="f245e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f245e-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="f245e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f245e-121">Ajout de OpsGenie à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f245e-121">Adding OpsGenie from hello gallery</span></span>
2. <span data-ttu-id="f245e-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f245e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-opsgenie-from-hello-gallery"></a><span data-ttu-id="f245e-123">Ajout de OpsGenie à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f245e-123">Adding OpsGenie from hello gallery</span></span>
<span data-ttu-id="f245e-124">intégration de hello tooconfigure de OpsGenie dans Azure AD, vous devez tooadd OpsGenie à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="f245e-124">tooconfigure hello integration of OpsGenie into Azure AD, you need tooadd OpsGenie from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f245e-125">**tooadd OpsGenie à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f245e-125">**tooadd OpsGenie from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f245e-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f245e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f245e-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="f245e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f245e-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f245e-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="f245e-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f245e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="f245e-133">Dans la zone de recherche de hello, tapez **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="f245e-133">In hello search box, type **OpsGenie**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_search.png)

5. <span data-ttu-id="f245e-135">Dans le volet de résultats hello, sélectionnez **OpsGenie**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f245e-135">In hello results panel, select **OpsGenie**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f245e-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f245e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f245e-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec OpsGenie, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="f245e-138">In this section, you configure and test Azure AD single sign-on with OpsGenie based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f245e-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans OpsGenie est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f245e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in OpsGenie is tooa user in Azure AD.</span></span> <span data-ttu-id="f245e-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans OpsGenie doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="f245e-140">In other words, a link relationship between an Azure AD user and hello related user in OpsGenie needs toobe established.</span></span>

<span data-ttu-id="f245e-141">Dans OpsGenie, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="f245e-141">In OpsGenie, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f245e-142">tooconfigure et test Azure AD l’authentification unique avec OpsGenie, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="f245e-142">tooconfigure and test Azure AD single sign-on with OpsGenie, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f245e-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="f245e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f245e-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f245e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f245e-145">**[Création d’un utilisateur de test OpsGenie](#creating-a-opsgenie-test-user)**  -toohave un équivalent de Britta Simon dans OpsGenie est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f245e-145">**[Creating a OpsGenie test user](#creating-a-opsgenie-test-user)** - toohave a counterpart of Britta Simon in OpsGenie that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f245e-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f245e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f245e-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="f245e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f245e-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f245e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f245e-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="f245e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your OpsGenie application.</span></span>

<span data-ttu-id="f245e-150">**tooconfigure Azure AD single sign-on avec OpsGenie, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f245e-150">**tooconfigure Azure AD single sign-on with OpsGenie, perform hello following steps:**</span></span>

1. <span data-ttu-id="f245e-151">Bonjour portail Azure, sur hello **OpsGenie** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="f245e-151">In hello Azure portal, on hello **OpsGenie** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="f245e-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f245e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_samlbase.png)

3. <span data-ttu-id="f245e-155">Sur hello **OpsGenie domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f245e-155">On hello **OpsGenie Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_url.png)

    <span data-ttu-id="f245e-157">Bonjour **URL de connexion** zone de texte, tapez l’URL hello :`https://app.opsgenie.com/auth/login`</span><span class="sxs-lookup"><span data-stu-id="f245e-157">In hello **Sign-on URL** textbox, type hello URL: `https://app.opsgenie.com/auth/login`</span></span>

4. <span data-ttu-id="f245e-158">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f245e-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_certificate.png) 

5. <span data-ttu-id="f245e-160">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="f245e-160">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-opsgenie-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f245e-162">Sur hello **OpsGenie Configuration** , cliquez sur **OpsGenie de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="f245e-162">On hello **OpsGenie Configuration** section, click **Configure OpsGenie** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f245e-163">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="f245e-163">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_configure.png) 

7. <span data-ttu-id="f245e-165">Ouvrez une autre instance du navigateur et puis reconnectez-vous tooOpsGenie en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f245e-165">Open another browser instance, and then log-in tooOpsGenie as an administrator.</span></span>

8. <span data-ttu-id="f245e-166">Cliquez sur **paramètres**, puis cliquez sur hello **Single Sign On** onglet.</span><span class="sxs-lookup"><span data-stu-id="f245e-166">Click **Settings**, and then click hello **Single Sign On** tab.</span></span>
   
    ![Authentification unique OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_06.png)

9. <span data-ttu-id="f245e-168">tooenable l’authentification unique, sélectionnez **activé**.</span><span class="sxs-lookup"><span data-stu-id="f245e-168">tooenable SSO, select **Enabled**.</span></span>
   
    ![Paramètres OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_07.png) 

10. <span data-ttu-id="f245e-170">Bonjour **fournisseur** , cliquez sur hello **Azure Active Directory** onglet.</span><span class="sxs-lookup"><span data-stu-id="f245e-170">In hello **Provider** section, click hello **Azure Active Directory** tab.</span></span>
   
    ![Paramètres OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_08.png) 

11. <span data-ttu-id="f245e-172">Sur la page de boîte de dialogue d’Azure Active Directory de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f245e-172">On hello Azure Active Directory dialog page, perform hello following steps:</span></span>
   
    ![Paramètres OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_09.png)
    
    <span data-ttu-id="f245e-174">a.</span><span class="sxs-lookup"><span data-stu-id="f245e-174">a.</span></span> <span data-ttu-id="f245e-175">Coller **Service URL d’authentification unique**, lequel vous avez copié à partir de hello portail Azure en hello **le point de terminaison SAML 2.0** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="f245e-175">Paste **Single Sign On Service URL**, which you have copied from hello Azure portal into hello **SAML 2.0 Endpoint** textbox.</span></span>
    
    <span data-ttu-id="f245e-176">b.</span><span class="sxs-lookup"><span data-stu-id="f245e-176">b.</span></span> <span data-ttu-id="f245e-177">Ouvrez votre certificat codé en base 64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite dans hello **X.500 certificat** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="f245e-177">Open your downloaded base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it into hello **X.500 Certificate** textbox.</span></span>
    
    <span data-ttu-id="f245e-178">c.</span><span class="sxs-lookup"><span data-stu-id="f245e-178">c.</span></span> <span data-ttu-id="f245e-179">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="f245e-179">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="f245e-180">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="f245e-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f245e-181">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="f245e-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f245e-182">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f245e-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f245e-183">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f245e-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="f245e-184">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="f245e-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="f245e-186">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f245e-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f245e-187">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f245e-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f245e-189">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f245e-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f245e-191">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="f245e-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f245e-193">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f245e-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f245e-195">a.</span><span class="sxs-lookup"><span data-stu-id="f245e-195">a.</span></span> <span data-ttu-id="f245e-196">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f245e-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f245e-197">b.</span><span class="sxs-lookup"><span data-stu-id="f245e-197">b.</span></span> <span data-ttu-id="f245e-198">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f245e-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f245e-199">c.</span><span class="sxs-lookup"><span data-stu-id="f245e-199">c.</span></span> <span data-ttu-id="f245e-200">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="f245e-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f245e-201">d.</span><span class="sxs-lookup"><span data-stu-id="f245e-201">d.</span></span> <span data-ttu-id="f245e-202">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="f245e-202">Click **Create**.</span></span>
 
### <a name="creating-a-opsgenie-test-user"></a><span data-ttu-id="f245e-203">Création d’un utilisateur de test OpsGenie</span><span class="sxs-lookup"><span data-stu-id="f245e-203">Creating a OpsGenie test user</span></span>

<span data-ttu-id="f245e-204">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="f245e-204">hello objective of this section is toocreate a user called Britta Simon in OpsGenie.</span></span> 

1. <span data-ttu-id="f245e-205">Dans une fenêtre de navigateur web, connectez-vous à votre client OpsGenie en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f245e-205">In a web browser window, log into your OpsGenie tenant as an administrator.</span></span>

2. <span data-ttu-id="f245e-206">Accédez tooUsers liste en cliquant sur **utilisateur** dans le volet gauche.</span><span class="sxs-lookup"><span data-stu-id="f245e-206">Navigate tooUsers list by clicking **User** in left panel.</span></span>
   
   ![Paramètres OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_10.png) 

3. <span data-ttu-id="f245e-208">Cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="f245e-208">Click **Add User**.</span></span>

4. <span data-ttu-id="f245e-209">Sur hello **ajouter un utilisateur** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f245e-209">On hello **Add User** dialog, perform hello following steps:</span></span>
   
   ![Paramètres OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_11.png)
   
   <span data-ttu-id="f245e-211">a.</span><span class="sxs-lookup"><span data-stu-id="f245e-211">a.</span></span> <span data-ttu-id="f245e-212">Bonjour **messagerie** zone de texte, adresse de messagerie de type hello de BrittaSimon adressé dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f245e-212">In hello **Email** textbox, type hello email address of BrittaSimon addressed in Azure Active Directory.</span></span>
   
   <span data-ttu-id="f245e-213">b.</span><span class="sxs-lookup"><span data-stu-id="f245e-213">b.</span></span> <span data-ttu-id="f245e-214">Bonjour **nom complet** zone de texte, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f245e-214">In hello **Full Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="f245e-215">c.</span><span class="sxs-lookup"><span data-stu-id="f245e-215">c.</span></span> <span data-ttu-id="f245e-216">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="f245e-216">Click **Save**.</span></span> 

>[!NOTE]
><span data-ttu-id="f245e-217">Britta reçoit un e-mail contenant des instructions pour configurer son profil.</span><span class="sxs-lookup"><span data-stu-id="f245e-217">Britta gets an email with instructions for setting up her profile.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f245e-218">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f245e-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f245e-219">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooOpsGenie.</span><span class="sxs-lookup"><span data-stu-id="f245e-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOpsGenie.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="f245e-221">**tooassign Britta Simon tooOpsGenie, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f245e-221">**tooassign Britta Simon tooOpsGenie, perform hello following steps:**</span></span>

1. <span data-ttu-id="f245e-222">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f245e-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="f245e-224">Dans la liste des applications hello, sélectionnez **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="f245e-224">In hello applications list, select **OpsGenie**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_app.png) 

3. <span data-ttu-id="f245e-226">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f245e-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="f245e-228">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f245e-228">Click **Add** button.</span></span> <span data-ttu-id="f245e-229">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f245e-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="f245e-231">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="f245e-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f245e-232">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f245e-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f245e-233">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f245e-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f245e-234">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="f245e-234">Testing single sign-on</span></span>

<span data-ttu-id="f245e-235">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="f245e-235">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="f245e-236">Lorsque vous cliquez sur mosaïque OpsGenie hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour OpsGenie application.</span><span class="sxs-lookup"><span data-stu-id="f245e-236">When you click hello OpsGenie tile in hello Access Panel, you should get automatically signed-on tooyour OpsGenie application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f245e-237">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f245e-237">Additional resources</span></span>

* [<span data-ttu-id="f245e-238">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f245e-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f245e-239">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="f245e-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_203.png

