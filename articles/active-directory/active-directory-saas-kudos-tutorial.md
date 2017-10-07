---
title: "Didacticiel : Intégration d’Azure Active Directory avec Kudos | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Kudos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 39c47ce6-4944-47ba-8f53-3afa95398034
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: c1b481463574461f9948db2b83843fefa5d74e99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kudos"></a><span data-ttu-id="19293-103">Didacticiel : Intégration d’Azure Active Directory à Kudos</span><span class="sxs-lookup"><span data-stu-id="19293-103">Tutorial: Azure Active Directory integration with Kudos</span></span>

<span data-ttu-id="19293-104">Dans ce didacticiel, vous apprendrez comment toointegrate Kudos avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="19293-104">In this tutorial, you learn how toointegrate Kudos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="19293-105">Intégration de Kudos à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="19293-105">Integrating Kudos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="19293-106">Vous pouvez contrôler dans Azure AD qui a accès tooKudos</span><span class="sxs-lookup"><span data-stu-id="19293-106">You can control in Azure AD who has access tooKudos</span></span>
- <span data-ttu-id="19293-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooKudos (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="19293-107">You can enable your users tooautomatically get signed-on tooKudos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="19293-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="19293-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="19293-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="19293-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19293-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="19293-110">Prerequisites</span></span>

<span data-ttu-id="19293-111">tooconfigure intégration d’Azure AD à Kudos, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="19293-111">tooconfigure Azure AD integration with Kudos, you need hello following items:</span></span>

- <span data-ttu-id="19293-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="19293-112">An Azure AD subscription</span></span>
- <span data-ttu-id="19293-113">Un abonnement Kudos pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="19293-113">A Kudos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="19293-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="19293-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="19293-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="19293-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="19293-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="19293-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="19293-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="19293-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="19293-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="19293-118">Scenario description</span></span>
<span data-ttu-id="19293-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="19293-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="19293-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="19293-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="19293-121">Ajout de Kudos à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="19293-121">Adding Kudos from hello gallery</span></span>
2. <span data-ttu-id="19293-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="19293-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kudos-from-hello-gallery"></a><span data-ttu-id="19293-123">Ajout de Kudos à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="19293-123">Adding Kudos from hello gallery</span></span>
<span data-ttu-id="19293-124">intégration de hello tooconfigure de Kudos dans Azure AD, vous devez tooadd Kudos à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="19293-124">tooconfigure hello integration of Kudos into Azure AD, you need tooadd Kudos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="19293-125">**tooadd Kudos à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="19293-125">**tooadd Kudos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="19293-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="19293-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="19293-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="19293-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="19293-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="19293-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="19293-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="19293-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="19293-133">Dans la zone de recherche de hello, tapez **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="19293-133">In hello search box, type **Kudos**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_search.png)

5. <span data-ttu-id="19293-135">Dans le volet de résultats hello, sélectionnez **Kudos**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="19293-135">In hello results panel, select **Kudos**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="19293-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="19293-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="19293-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Kudos à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="19293-138">In this section, you configure and test Azure AD single sign-on with Kudos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="19293-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Kudos est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19293-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kudos is tooa user in Azure AD.</span></span> <span data-ttu-id="19293-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Kudos doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="19293-140">In other words, a link relationship between an Azure AD user and hello related user in Kudos needs toobe established.</span></span>

<span data-ttu-id="19293-141">Dans Kudos, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="19293-141">In Kudos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="19293-142">tooconfigure et test Azure AD l’authentification unique avec Kudos, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="19293-142">tooconfigure and test Azure AD single sign-on with Kudos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="19293-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="19293-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="19293-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="19293-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="19293-145">**[Création d’un utilisateur de test de Kudos](#creating-a-kudos-test-user)**  -toohave un équivalent de Britta Simon dans Kudos est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="19293-145">**[Creating a Kudos test user](#creating-a-kudos-test-user)** - toohave a counterpart of Britta Simon in Kudos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="19293-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="19293-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="19293-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="19293-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="19293-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="19293-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="19293-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Kudos.</span><span class="sxs-lookup"><span data-stu-id="19293-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kudos application.</span></span>

<span data-ttu-id="19293-150">**tooconfigure Azure AD single sign-on avec Kudos, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="19293-150">**tooconfigure Azure AD single sign-on with Kudos, perform hello following steps:**</span></span>

1. <span data-ttu-id="19293-151">Bonjour portail Azure, sur hello **Kudos** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="19293-151">In hello Azure portal, on hello **Kudos** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="19293-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="19293-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_samlbase.png)

3. <span data-ttu-id="19293-155">Sur hello **Kudos domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="19293-155">On hello **Kudos Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_url.png)

    <span data-ttu-id="19293-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company>.kudosnow.com`</span><span class="sxs-lookup"><span data-stu-id="19293-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.kudosnow.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="19293-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="19293-158">This value is not real.</span></span> <span data-ttu-id="19293-159">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="19293-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="19293-160">Contact [équipe de support Client de Kudos](http://success.kudosnow.com/home) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="19293-160">Contact [Kudos Client support team](http://success.kudosnow.com/home) tooget this value.</span></span> 
 
4. <span data-ttu-id="19293-161">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="19293-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_certificate.png) 

5. <span data-ttu-id="19293-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="19293-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kudos-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="19293-165">Sur hello **Kudos Configuration** , cliquez sur **configurer de Kudos** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="19293-165">On hello **Kudos Configuration** section, click **Configure Kudos** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="19293-166">Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="19293-166">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_configure.png) 

7. <span data-ttu-id="19293-168">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Kudos en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="19293-168">In a different web browser window, log into your Kudos company site as an administrator.</span></span>

8. <span data-ttu-id="19293-169">Dans le menu hello haut de hello, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="19293-169">In hello menu on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="19293-170">![Paramètres](./media/active-directory-saas-kudos-tutorial/ic787806.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="19293-170">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

9. <span data-ttu-id="19293-171">Cliquez sur **Integrations \> SSO**.</span><span class="sxs-lookup"><span data-stu-id="19293-171">Click **Integrations \> SSO**.</span></span>

10. <span data-ttu-id="19293-172">Bonjour **SSO** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="19293-172">In hello **SSO** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="19293-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span><span class="sxs-lookup"><span data-stu-id="19293-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span></span>
   
    <span data-ttu-id="19293-174">a.</span><span class="sxs-lookup"><span data-stu-id="19293-174">a.</span></span> <span data-ttu-id="19293-175">Dans **URL de connexion** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="19293-175">In **Sign on URL** textbox, paste hello value of  **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="19293-176">b.</span><span class="sxs-lookup"><span data-stu-id="19293-176">b.</span></span> <span data-ttu-id="19293-177">Ouvrez votre certificat codé en base 64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat X.509** zone de texte</span><span class="sxs-lookup"><span data-stu-id="19293-177">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 certificate** textbox</span></span>
   
    <span data-ttu-id="19293-178">c.</span><span class="sxs-lookup"><span data-stu-id="19293-178">c.</span></span> <span data-ttu-id="19293-179">Dans **déconnexion tooURL**, collez la valeur hello **URL de déconnexion** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="19293-179">In **Logout tooURL**, paste hello value of  **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="19293-180">d.</span><span class="sxs-lookup"><span data-stu-id="19293-180">d.</span></span> <span data-ttu-id="19293-181">Bonjour **votre URL Kudos** zone de texte, tapez le nom de votre société.</span><span class="sxs-lookup"><span data-stu-id="19293-181">In hello **Your Kudos URL** textbox, type your company name.</span></span>
   
    <span data-ttu-id="19293-182">e.</span><span class="sxs-lookup"><span data-stu-id="19293-182">e.</span></span> <span data-ttu-id="19293-183">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="19293-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="19293-184">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="19293-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="19293-185">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="19293-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="19293-186">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="19293-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="19293-187">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="19293-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="19293-188">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="19293-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="19293-190">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="19293-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="19293-191">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="19293-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="19293-193">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="19293-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="19293-195">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="19293-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="19293-197">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="19293-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="19293-199">a.</span><span class="sxs-lookup"><span data-stu-id="19293-199">a.</span></span> <span data-ttu-id="19293-200">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="19293-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="19293-201">b.</span><span class="sxs-lookup"><span data-stu-id="19293-201">b.</span></span> <span data-ttu-id="19293-202">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="19293-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="19293-203">c.</span><span class="sxs-lookup"><span data-stu-id="19293-203">c.</span></span> <span data-ttu-id="19293-204">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="19293-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="19293-205">d.</span><span class="sxs-lookup"><span data-stu-id="19293-205">d.</span></span> <span data-ttu-id="19293-206">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="19293-206">Click **Create**.</span></span>
 
### <a name="creating-a-kudos-test-user"></a><span data-ttu-id="19293-207">Création d’un utilisateur de test Kudos</span><span class="sxs-lookup"><span data-stu-id="19293-207">Creating a Kudos test user</span></span>

<span data-ttu-id="19293-208">Dans l’ordre tooenable Azure AD les utilisateurs toolog à Kudos, vous devez les configurer dans Kudos.</span><span class="sxs-lookup"><span data-stu-id="19293-208">In order tooenable Azure AD users toolog into Kudos, they must be provisioned into Kudos.</span></span> 

<span data-ttu-id="19293-209">Dans les cas de hello de Kudos, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="19293-209">In hello case of Kudos, provisioning is a manual task.</span></span>

<span data-ttu-id="19293-210">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="19293-210">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="19293-211">Connectez-vous à tooyour **Kudos** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="19293-211">Log in tooyour **Kudos** company site as administrator.</span></span>

2. <span data-ttu-id="19293-212">Dans le menu hello haut de hello, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="19293-212">In hello menu on hello top, click **Settings**.</span></span>
   
   <span data-ttu-id="19293-213">![Paramètres](./media/active-directory-saas-kudos-tutorial/ic787806.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="19293-213">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

3. <span data-ttu-id="19293-214">Cliquez sur **User Admin**.</span><span class="sxs-lookup"><span data-stu-id="19293-214">Click **User Admin**.</span></span>

4. <span data-ttu-id="19293-215">Cliquez sur hello **utilisateurs** onglet, puis cliquez sur **ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="19293-215">Click hello **Users** tab, and then click **Add a User**.</span></span>
   
   <span data-ttu-id="19293-216">![User Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "User Admin")</span><span class="sxs-lookup"><span data-stu-id="19293-216">![User Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "User Admin")</span></span>

5. <span data-ttu-id="19293-217">Bonjour **ajouter un utilisateur** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="19293-217">In hello **Add a User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="19293-218">![Ajouter un utilisateur](./media/active-directory-saas-kudos-tutorial/ic787810.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="19293-218">![Add a User](./media/active-directory-saas-kudos-tutorial/ic787810.png "Add a User")</span></span>
   
    <span data-ttu-id="19293-219">a.</span><span class="sxs-lookup"><span data-stu-id="19293-219">a.</span></span> <span data-ttu-id="19293-220">Hello de type **prénom**, **nom**, **messagerie** et d’autres détails d’un compte Azure Active Directory valide que vous voulez tooprovision dans hello les zones de texte.</span><span class="sxs-lookup"><span data-stu-id="19293-220">Type hello **First Name**, **Last Name**, **Email** and other details of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="19293-221">b.</span><span class="sxs-lookup"><span data-stu-id="19293-221">b.</span></span> <span data-ttu-id="19293-222">Cliquez sur **Create User**.</span><span class="sxs-lookup"><span data-stu-id="19293-222">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="19293-223">Vous pouvez utiliser n’importe quel autre Kudos utilisateur compte outil de création ou API fournie par Kudos tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="19293-223">You can use any other Kudos user account creation tools or APIs provided by Kudos tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="19293-224">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="19293-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="19293-225">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooKudos.</span><span class="sxs-lookup"><span data-stu-id="19293-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKudos.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="19293-227">**tooassign Britta Simon tooKudos, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="19293-227">**tooassign Britta Simon tooKudos, perform hello following steps:**</span></span>

1. <span data-ttu-id="19293-228">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="19293-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="19293-230">Dans la liste des applications hello, sélectionnez **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="19293-230">In hello applications list, select **Kudos**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_app.png) 

3. <span data-ttu-id="19293-232">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="19293-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="19293-234">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="19293-234">Click **Add** button.</span></span> <span data-ttu-id="19293-235">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="19293-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="19293-237">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="19293-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="19293-238">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="19293-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="19293-239">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="19293-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="19293-240">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="19293-240">Testing single sign-on</span></span>

<span data-ttu-id="19293-241">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="19293-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="19293-242">Lorsque vous cliquez sur mosaïque Kudos hello hello volet d’accès, vous devez obtenir l’application de Kudos automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="19293-242">When you click hello Kudos tile in hello Access Panel, you should get automatically signed-on tooyour Kudos application.</span></span> <span data-ttu-id="19293-243">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="19293-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="19293-244">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="19293-244">Additional resources</span></span>

* [<span data-ttu-id="19293-245">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="19293-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="19293-246">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="19293-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_203.png

