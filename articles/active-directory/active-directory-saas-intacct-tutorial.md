---
title: "Didacticiel : Intégration d’Azure Active Directory avec Intacct | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Intacct."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3500039615166c2f61fb408d85bb82dfaefba134
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a><span data-ttu-id="fd695-103">Didacticiel : Intégration d’Azure Active Directory à Intacct</span><span class="sxs-lookup"><span data-stu-id="fd695-103">Tutorial: Azure Active Directory integration with Intacct</span></span>

<span data-ttu-id="fd695-104">Dans ce didacticiel, vous apprendrez comment toointegrate Intacct avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fd695-104">In this tutorial, you learn how toointegrate Intacct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fd695-105">Intégration d’Intacct à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="fd695-105">Integrating Intacct with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fd695-106">Vous pouvez contrôler dans Azure AD qui a accès tooIntacct</span><span class="sxs-lookup"><span data-stu-id="fd695-106">You can control in Azure AD who has access tooIntacct</span></span>
- <span data-ttu-id="fd695-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooIntacct (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd695-107">You can enable your users tooautomatically get signed-on tooIntacct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fd695-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="fd695-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fd695-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fd695-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd695-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fd695-110">Prerequisites</span></span>

<span data-ttu-id="fd695-111">tooconfigure intégration d’Azure AD à Intacct, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="fd695-111">tooconfigure Azure AD integration with Intacct, you need hello following items:</span></span>

- <span data-ttu-id="fd695-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd695-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fd695-113">Un abonnement Intacct pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="fd695-113">An Intacct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fd695-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="fd695-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fd695-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="fd695-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fd695-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="fd695-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fd695-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fd695-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fd695-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="fd695-118">Scenario description</span></span>
<span data-ttu-id="fd695-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="fd695-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fd695-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="fd695-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fd695-121">Ajout d’Intacct à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="fd695-121">Adding Intacct from hello gallery</span></span>
2. <span data-ttu-id="fd695-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd695-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intacct-from-hello-gallery"></a><span data-ttu-id="fd695-123">Ajout d’Intacct à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="fd695-123">Adding Intacct from hello gallery</span></span>
<span data-ttu-id="fd695-124">intégration de hello tooconfigure de Intacct dans Azure AD, vous devez tooadd Intacct à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="fd695-124">tooconfigure hello integration of Intacct into Azure AD, you need tooadd Intacct from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fd695-125">**tooadd Intacct à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fd695-125">**tooadd Intacct from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fd695-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="fd695-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fd695-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="fd695-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fd695-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="fd695-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="fd695-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="fd695-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="fd695-133">Dans la zone de recherche de hello, tapez **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="fd695-133">In hello search box, type **Intacct**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. <span data-ttu-id="fd695-135">Dans le volet de résultats hello, sélectionnez **Intacct**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="fd695-135">In hello results panel, select **Intacct**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fd695-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd695-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fd695-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Intacct avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="fd695-138">In this section, you configure and test Azure AD single sign-on with Intacct based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fd695-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Intacct est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd695-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Intacct is tooa user in Azure AD.</span></span> <span data-ttu-id="fd695-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Intacct doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="fd695-140">In other words, a link relationship between an Azure AD user and hello related user in Intacct needs toobe established.</span></span>

<span data-ttu-id="fd695-141">En l’occurrence, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="fd695-141">In Intacct, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fd695-142">tooconfigure et test Azure AD l’authentification unique à Intacct, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="fd695-142">tooconfigure and test Azure AD single sign-on with Intacct, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fd695-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="fd695-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fd695-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fd695-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fd695-145">**[Création d’un utilisateur de test Intacct](#creating-an-intacct-test-user)**  -toohave un équivalent de Britta Simon dans Intacct est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fd695-145">**[Creating an Intacct test user](#creating-an-intacct-test-user)** - toohave a counterpart of Britta Simon in Intacct that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fd695-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="fd695-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fd695-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="fd695-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fd695-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd695-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fd695-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Intacct.</span><span class="sxs-lookup"><span data-stu-id="fd695-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Intacct application.</span></span>

<span data-ttu-id="fd695-150">**tooconfigure Azure AD single sign-on avec Intacct, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fd695-150">**tooconfigure Azure AD single sign-on with Intacct, perform hello following steps:**</span></span>

1. <span data-ttu-id="fd695-151">Bonjour portail Azure, sur hello **Intacct** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="fd695-151">In hello Azure portal, on hello **Intacct** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="fd695-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="fd695-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. <span data-ttu-id="fd695-155">Sur hello **Intacct domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="fd695-155">On hello **Intacct Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    <span data-ttu-id="fd695-157">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="fd695-157">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > <span data-ttu-id="fd695-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="fd695-158">This value is not real.</span></span> <span data-ttu-id="fd695-159">Mettre à jour cette valeur avec l’URL de réponse réelle hello.</span><span class="sxs-lookup"><span data-stu-id="fd695-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="fd695-160">Contact [équipe de support Intacct](https://us.intacct.com/support) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="fd695-160">Contact [Intacct support team](https://us.intacct.com/support) tooget this value.</span></span>

4. <span data-ttu-id="fd695-161">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="fd695-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. <span data-ttu-id="fd695-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="fd695-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fd695-165">Sur hello **Intacct Configuration** , cliquez sur **Intacct de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="fd695-165">On hello **Intacct Configuration** section, click **Configure Intacct** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fd695-166">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="fd695-166">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. <span data-ttu-id="fd695-168">Dans une fenêtre de navigateur web, connectez-vous dans un site d’entreprise Intacct tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="fd695-168">In a different web browser window, sign in tooyour Intacct company site as an administrator.</span></span>

8. <span data-ttu-id="fd695-169">Cliquez sur hello **société** onglet, puis cliquez sur **Infos société**.</span><span class="sxs-lookup"><span data-stu-id="fd695-169">Click hello **Company** tab, and then click **Company Info**.</span></span>

    <span data-ttu-id="fd695-170">![Company](./media/active-directory-saas-intacct-tutorial/ic790037.png "Company")</span><span class="sxs-lookup"><span data-stu-id="fd695-170">![Company](./media/active-directory-saas-intacct-tutorial/ic790037.png "Company")</span></span>

9. <span data-ttu-id="fd695-171">Cliquez sur hello **sécurité** onglet, puis cliquez sur **modifier**.</span><span class="sxs-lookup"><span data-stu-id="fd695-171">Click hello **Security** tab, and then click **Edit**.</span></span>

    <span data-ttu-id="fd695-172">![Sécurité](./media/active-directory-saas-intacct-tutorial/ic790038.png "Sécurité")</span><span class="sxs-lookup"><span data-stu-id="fd695-172">![Security](./media/active-directory-saas-intacct-tutorial/ic790038.png "Security")</span></span>

10. <span data-ttu-id="fd695-173">Bonjour **Single sign on (SSO)** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="fd695-173">In hello **Single sign on (SSO)** section, perform hello following steps:</span></span>

    <span data-ttu-id="fd695-174">![Single sign On](./media/active-directory-saas-intacct-tutorial/ic790039.png "Single sign On")</span><span class="sxs-lookup"><span data-stu-id="fd695-174">![Single sign on](./media/active-directory-saas-intacct-tutorial/ic790039.png "single sign on")</span></span>

    <span data-ttu-id="fd695-175">a.</span><span class="sxs-lookup"><span data-stu-id="fd695-175">a.</span></span> <span data-ttu-id="fd695-176">Sélectionnez **Enable Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="fd695-176">Select **Enable single sign on**.</span></span>

    <span data-ttu-id="fd695-177">b.</span><span class="sxs-lookup"><span data-stu-id="fd695-177">b.</span></span> <span data-ttu-id="fd695-178">Pour **Identity provider type**, sélectionnez **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="fd695-178">As **Identity provider type**, select **SAML 2.0**.</span></span>

    <span data-ttu-id="fd695-179">c.</span><span class="sxs-lookup"><span data-stu-id="fd695-179">c.</span></span> <span data-ttu-id="fd695-180">Dans **URL de l’émetteur** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fd695-180">In **Issuer URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="fd695-181">d.</span><span class="sxs-lookup"><span data-stu-id="fd695-181">d.</span></span> <span data-ttu-id="fd695-182">Dans **URL de connexion** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fd695-182">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="fd695-183">e.</span><span class="sxs-lookup"><span data-stu-id="fd695-183">e.</span></span> <span data-ttu-id="fd695-184">Ouvrez votre **base 64** certificat dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat** boîte.</span><span class="sxs-lookup"><span data-stu-id="fd695-184">Open your **base-64** encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** box.</span></span>
   
    <span data-ttu-id="fd695-185">f.</span><span class="sxs-lookup"><span data-stu-id="fd695-185">f.</span></span> <span data-ttu-id="fd695-186">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="fd695-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="fd695-187">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="fd695-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fd695-188">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="fd695-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fd695-189">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fd695-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fd695-190">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd695-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="fd695-191">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="fd695-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="fd695-193">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fd695-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fd695-194">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="fd695-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fd695-196">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="fd695-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fd695-198">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="fd695-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fd695-200">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="fd695-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fd695-202">a.</span><span class="sxs-lookup"><span data-stu-id="fd695-202">a.</span></span> <span data-ttu-id="fd695-203">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fd695-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fd695-204">b.</span><span class="sxs-lookup"><span data-stu-id="fd695-204">b.</span></span> <span data-ttu-id="fd695-205">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fd695-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fd695-206">c.</span><span class="sxs-lookup"><span data-stu-id="fd695-206">c.</span></span> <span data-ttu-id="fd695-207">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="fd695-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fd695-208">d.</span><span class="sxs-lookup"><span data-stu-id="fd695-208">d.</span></span> <span data-ttu-id="fd695-209">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="fd695-209">Click **Create**.</span></span>
 
### <a name="creating-an-intacct-test-user"></a><span data-ttu-id="fd695-210">Création d’un utilisateur de test Intacct</span><span class="sxs-lookup"><span data-stu-id="fd695-210">Creating an Intacct test user</span></span>

<span data-ttu-id="fd695-211">tooset des utilisateurs d’Azure AD afin de pouvoir se connecter dans tooIntacct, vous devez les configurer dans Intacct.</span><span class="sxs-lookup"><span data-stu-id="fd695-211">tooset up Azure AD users so they can sign in tooIntacct, they must be provisioned into Intacct.</span></span> <span data-ttu-id="fd695-212">Pour Intacct, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="fd695-212">For Intacct, provisioning is a manual task.</span></span>

<span data-ttu-id="fd695-213">**comptes d’utilisateur tooprovision, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fd695-213">**tooprovision user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="fd695-214">Connectez-vous à tooyour **Intacct** client.</span><span class="sxs-lookup"><span data-stu-id="fd695-214">Sign in tooyour **Intacct** tenant.</span></span>

2. <span data-ttu-id="fd695-215">Cliquez sur hello **société** onglet, puis cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="fd695-215">Click hello **Company** tab, and then click **Users**.</span></span>

    <span data-ttu-id="fd695-216">![Utilisateurs](./media/active-directory-saas-intacct-tutorial/ic790041.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="fd695-216">![Users](./media/active-directory-saas-intacct-tutorial/ic790041.png "Users")</span></span>
3. <span data-ttu-id="fd695-217">Cliquez sur hello **ajouter** onglet.</span><span class="sxs-lookup"><span data-stu-id="fd695-217">Click hello **Add** tab.</span></span>

    <span data-ttu-id="fd695-218">![Add](./media/active-directory-saas-intacct-tutorial/ic790042.png "Add")</span><span class="sxs-lookup"><span data-stu-id="fd695-218">![Add](./media/active-directory-saas-intacct-tutorial/ic790042.png "Add")</span></span>
4. <span data-ttu-id="fd695-219">Bonjour **informations utilisateur** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="fd695-219">In hello **User Information** section, perform hello following steps:</span></span>

    <span data-ttu-id="fd695-220">![User Information](./media/active-directory-saas-intacct-tutorial/ic790043.png "User Information")</span><span class="sxs-lookup"><span data-stu-id="fd695-220">![User Information](./media/active-directory-saas-intacct-tutorial/ic790043.png "User Information")</span></span>

    <span data-ttu-id="fd695-221">a.</span><span class="sxs-lookup"><span data-stu-id="fd695-221">a.</span></span> <span data-ttu-id="fd695-222">Entrez hello **ID utilisateur**, hello **nom**, **prénom**, hello **adresse de messagerie**, hello **titre**, et hello **téléphone** d’un compte Azure AD que vous voulez tooprovision dans hello **informations utilisateur** section.</span><span class="sxs-lookup"><span data-stu-id="fd695-222">Enter hello **User ID**, hello **Last name**, **First name**, hello **Email address**, hello **Title**, and hello **Phone** of an Azure AD account that you want tooprovision into hello **User Information** section.</span></span>

    <span data-ttu-id="fd695-223">b.</span><span class="sxs-lookup"><span data-stu-id="fd695-223">b.</span></span> <span data-ttu-id="fd695-224">Sélectionnez hello **des privilèges d’administration** d’un compte Azure AD que vous souhaitez tooprovision.</span><span class="sxs-lookup"><span data-stu-id="fd695-224">Select hello **Admin privileges** of an Azure AD account that you want tooprovision.</span></span>
   
    <span data-ttu-id="fd695-225">c.</span><span class="sxs-lookup"><span data-stu-id="fd695-225">c.</span></span> <span data-ttu-id="fd695-226">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="fd695-226">Click **Save**.</span></span> <span data-ttu-id="fd695-227">titulaire du compte Azure AD Hello reçoit un message électronique et suit un tooconfirm de lier leur compte avant son activation.</span><span class="sxs-lookup"><span data-stu-id="fd695-227">hello Azure AD account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

>[!NOTE]
><span data-ttu-id="fd695-228">tooprovision comptes d’utilisateur Azure AD, vous pouvez utiliser des autres outils de création de compte utilisateur Intacct ou les API fournies par Intacct.</span><span class="sxs-lookup"><span data-stu-id="fd695-228">tooprovision Azure AD user accounts, you can use other Intacct user account creation tools or APIs that are provided by Intacct.</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fd695-229">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd695-229">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fd695-230">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooIntacct.</span><span class="sxs-lookup"><span data-stu-id="fd695-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIntacct.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="fd695-232">**tooassign Britta Simon tooIntacct, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fd695-232">**tooassign Britta Simon tooIntacct, perform hello following steps:**</span></span>

1. <span data-ttu-id="fd695-233">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="fd695-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="fd695-235">Dans la liste des applications hello, sélectionnez **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="fd695-235">In hello applications list, select **Intacct**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. <span data-ttu-id="fd695-237">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="fd695-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="fd695-239">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="fd695-239">Click **Add** button.</span></span> <span data-ttu-id="fd695-240">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="fd695-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="fd695-242">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="fd695-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fd695-243">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="fd695-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fd695-244">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="fd695-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fd695-245">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="fd695-245">Testing single sign-on</span></span>

<span data-ttu-id="fd695-246">Dans cette section, vous testez votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="fd695-246">In this section, you test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="fd695-247">Lorsque vous cliquez sur mosaïque Intacct hello hello volet d’accès, vous devez être connecté automatiquement dans tooyour Intacct application.</span><span class="sxs-lookup"><span data-stu-id="fd695-247">When you click hello Intacct tile in hello Access Panel, you should be automatically signed in tooyour Intacct application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fd695-248">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="fd695-248">Additional resources</span></span>

* [<span data-ttu-id="fd695-249">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fd695-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fd695-250">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="fd695-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

