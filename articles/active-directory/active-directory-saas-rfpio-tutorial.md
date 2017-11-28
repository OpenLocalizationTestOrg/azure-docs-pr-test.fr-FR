---
title: "Didacticiel : Intégration d’Azure Active Directory à RFPIO | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et RFPIO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: e0c692276276edd8f859e73d81cf54d75a65957a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a><span data-ttu-id="08ed6-103">Didacticiel : Intégration d’Azure Active Directory à RFPIO</span><span class="sxs-lookup"><span data-stu-id="08ed6-103">Tutorial: Azure Active Directory integration with RFPIO</span></span>

<span data-ttu-id="08ed6-104">Dans ce didacticiel, vous apprendrez comment toointegrate RFPIO avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="08ed6-104">In this tutorial, you learn how toointegrate RFPIO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="08ed6-105">Intégration RFPIO à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="08ed6-105">Integrating RFPIO with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="08ed6-106">Vous pouvez contrôler qui dans Azure AD qui a accès tooRFPIO.</span><span class="sxs-lookup"><span data-stu-id="08ed6-106">You can control who in Azure AD who has access tooRFPIO.</span></span>
- <span data-ttu-id="08ed6-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooRFPIO (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08ed6-107">You can enable your users tooautomatically get signed-on tooRFPIO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="08ed6-108">Vous pouvez gérer vos comptes dans un emplacement central--hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="08ed6-108">You can manage your accounts in one central location--hello Azure portal.</span></span>

<span data-ttu-id="08ed6-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="08ed6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08ed6-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="08ed6-110">Prerequisites</span></span>

<span data-ttu-id="08ed6-111">tooconfigure intégration d’Azure AD avec RFPIO, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="08ed6-111">tooconfigure Azure AD integration with RFPIO, you need hello following items:</span></span>

- <span data-ttu-id="08ed6-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="08ed6-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="08ed6-113">Un abonnement RFPIO pour lequel l’authentification unique est activée.</span><span class="sxs-lookup"><span data-stu-id="08ed6-113">A RFPIO single sign-on-enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="08ed6-114">Nous ne vous recommandons d’utiliser une procédure de production environnement tootest hello dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="08ed6-114">We don't recommend that you use a production environment tootest hello steps in this tutorial.</span></span>

<span data-ttu-id="08ed6-115">étapes de hello tootest dans ce didacticiel, suivez ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="08ed6-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="08ed6-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="08ed6-116">Do not use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="08ed6-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="08ed6-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="08ed6-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="08ed6-118">Scenario description</span></span>
<span data-ttu-id="08ed6-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="08ed6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="08ed6-120">scénario de Hello est décrit dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="08ed6-120">hello scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="08ed6-121">Ajout de RFPIO à partir de la galerie de hello.</span><span class="sxs-lookup"><span data-stu-id="08ed6-121">Adding RFPIO from hello gallery.</span></span>
2. <span data-ttu-id="08ed6-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="08ed6-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-rfpio-from-hello-gallery"></a><span data-ttu-id="08ed6-123">Ajouter des RFPIO à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="08ed6-123">Add RFPIO from hello gallery</span></span>
<span data-ttu-id="08ed6-124">intégration de hello tooconfigure de RFPIO dans Azure AD, vous devez tooadd RFPIO à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="08ed6-124">tooconfigure hello integration of RFPIO into Azure AD, you need tooadd RFPIO from hello gallery tooyour list of managed SaaS apps.</span></span>

### <a name="tooadd-rfpio-from-hello-gallery"></a><span data-ttu-id="08ed6-125">tooadd RFPIO à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="08ed6-125">tooadd RFPIO from hello gallery</span></span>

1. <span data-ttu-id="08ed6-126">Bonjour  **[portail Azure](https://portal.azure.com)**, sur hello du volet de navigation gauche, sélectionnez hello **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="08ed6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="08ed6-128">Sélectionnez **Applications d’entreprise**, puis **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="08ed6-130">tooadd une nouvelle application, sélectionnez hello **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="08ed6-130">tooadd a new application, select hello **New application** button on hello top of dialog box.</span></span>

    ![Applications][3]

4. <span data-ttu-id="08ed6-132">Dans la zone de recherche de hello, tapez **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-132">In hello search box, type **RFPIO**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. <span data-ttu-id="08ed6-134">Dans le volet de résultats hello, sélectionnez **RFPIO**, puis sélectionnez hello **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="08ed6-134">In hello results panel, select **RFPIO**, and then select hello **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="08ed6-136">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="08ed6-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="08ed6-137">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec RFPIO, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="08ed6-137">In this section, you configure and test Azure AD single sign-on with RFPIO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="08ed6-138">Pour toowork de l’authentification unique, Azure AD doit tooknow quelle relation hello est entre équivalent dans RFPIO un utilisateur et dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08ed6-138">For single sign-on toowork, Azure AD needs tooknow what hello relationship is between counterpart user in RFPIO and a user in Azure AD.</span></span> <span data-ttu-id="08ed6-139">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans RFPIO doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="08ed6-139">In other words, a link relationship between an Azure AD user and hello related user in RFPIO needs toobe established.</span></span>

<span data-ttu-id="08ed6-140">Dans RFPIO, affecter la valeur de hello de **nom d’utilisateur** dans Azure AD en tant que valeur hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="08ed6-140">In RFPIO, assign hello value of **user name** in Azure AD as hello value of  **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="08ed6-141">tooconfigure et test Azure AD l’authentification unique avec RFPIO, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="08ed6-141">tooconfigure and test Azure AD single sign-on with RFPIO, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="08ed6-142">**[Configurer Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--tooenable votre toouse utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="08ed6-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="08ed6-143">**[Créer un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**--tootest Azure AD l’authentification unique avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="08ed6-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)**-- tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="08ed6-144">**[Créer un utilisateur de test RFPIO](#creating-a-rfpio-test-user)**  toohave--un équivalent de Britta Simon dans RFPIO est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="08ed6-144">**[Create a RFPIO test user](#creating-a-rfpio-test-user)** --toohave a counterpart of Britta Simon in RFPIO that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="08ed6-145">**[Affecter l’utilisateur de test hello Azure AD](#assigning-the-azure-ad-test-user)**tooenable--Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="08ed6-145">**[Assign hello Azure AD test user](#assigning-the-azure-ad-test-user)**--tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="08ed6-146">**[Tester l’authentification unique sur](#testing-single-sign-on)**  --tooverify si hello configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="08ed6-146">**[Test Single Sign-On](#testing-single-sign-on)** --tooverify if hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="08ed6-147">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="08ed6-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="08ed6-148">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application RFPIO.</span><span class="sxs-lookup"><span data-stu-id="08ed6-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RFPIO application.</span></span>

<span data-ttu-id="08ed6-149">**tooconfigure Azure AD single sign-on avec RFPIO, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="08ed6-149">**tooconfigure Azure AD single sign-on with RFPIO, perform hello following steps:**</span></span>

1. <span data-ttu-id="08ed6-150">Bonjour portail Azure, sur hello **RFPIO** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-150">In hello Azure portal, on hello **RFPIO** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="08ed6-152">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="08ed6-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. <span data-ttu-id="08ed6-154">Sur hello **RFPIO domaine et les URL** section, si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="08ed6-154">On hello **RFPIO Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    <span data-ttu-id="08ed6-156">a.</span><span class="sxs-lookup"><span data-stu-id="08ed6-156">a.</span></span> <span data-ttu-id="08ed6-157">Bonjour **identificateur** zone de texte, tapez l’URL hello :`https://www.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="08ed6-157">In hello **Identifier** textbox, type hello URL: `https://www.rfpio.com`</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    <span data-ttu-id="08ed6-159">b.</span><span class="sxs-lookup"><span data-stu-id="08ed6-159">b.</span></span> <span data-ttu-id="08ed6-160">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-160">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="08ed6-161">c.</span><span class="sxs-lookup"><span data-stu-id="08ed6-161">c.</span></span> <span data-ttu-id="08ed6-162">Bonjour **relais état** zone de texte Entrez une valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="08ed6-162">In hello **Relay State** textbox enter a string value.</span></span> <span data-ttu-id="08ed6-163">Contact [RFPIO l’équipe de support](https://www.rfpio.com/contact/) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="08ed6-163">Contact [RFPIO support team](https://www.rfpio.com/contact/) tooget this value.</span></span> 

4. <span data-ttu-id="08ed6-164">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-164">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="08ed6-165">Si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="08ed6-165">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>   

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    <span data-ttu-id="08ed6-167">Bonjour **URL de connexion** zone de texte, tapez l’URL hello :`https://www.app.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="08ed6-167">In hello **Sign on URL** textbox, type hello URL: `https://www.app.rfpio.com`</span></span>

5. <span data-ttu-id="08ed6-168">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="08ed6-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. <span data-ttu-id="08ed6-170">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="08ed6-170">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="08ed6-172">Dans une fenêtre de navigateur web, connexion toohello **RFPIO** site Web en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="08ed6-172">In a different web browser window, login toohello **RFPIO** website as an administrator.</span></span>

8. <span data-ttu-id="08ed6-173">Cliquez sur la liste déroulante de hello en bas à gauche.</span><span class="sxs-lookup"><span data-stu-id="08ed6-173">Click on hello bottom left corner dropdown.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. <span data-ttu-id="08ed6-175">Cliquez sur hello **paramètres de l’organisation**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-175">Click on hello **Organization Settings**.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. <span data-ttu-id="08ed6-177">Cliquez sur hello **intégration et fonctionnalités**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-177">Click on hello **FEATURES & INTEGRATION**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. <span data-ttu-id="08ed6-179">Bonjour **Configuration de l’authentification unique SAML** cliquez sur **modifier**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-179">In hello **SAML SSO Configuration** Click **Edit**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. <span data-ttu-id="08ed6-181">Dans cette section, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="08ed6-181">In this Section perform following actions:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    <span data-ttu-id="08ed6-183">a.</span><span class="sxs-lookup"><span data-stu-id="08ed6-183">a.</span></span> <span data-ttu-id="08ed6-184">Copier le contenu de hello Hello **XML de métadonnées téléchargé** et collez-le dans hello **configuration d’identité** champ.</span><span class="sxs-lookup"><span data-stu-id="08ed6-184">Copy hello content of hello **Downloaded Metadata XML** and paste it into hello **identity configuration** field.</span></span>

    > [!NOTE]
    ><span data-ttu-id="08ed6-185">hello toocopy contenu de téléchargé **Metadata XML** utilisez **bloc-notes ++** ou appropriée **éditeur XML**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-185">toocopy hello content of downloaded **Metadata XML** Use **Notepad++** or proper **XML Editor**.</span></span> 

    <span data-ttu-id="08ed6-186">b.</span><span class="sxs-lookup"><span data-stu-id="08ed6-186">b.</span></span> <span data-ttu-id="08ed6-187">Cliquez sur **Valider**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-187">Click **Validate**.</span></span>

    <span data-ttu-id="08ed6-188">c.</span><span class="sxs-lookup"><span data-stu-id="08ed6-188">c.</span></span> <span data-ttu-id="08ed6-189">Après avoir fait de cliquer sur **Validate**, retourner **SAML(Enabled)** tooon.</span><span class="sxs-lookup"><span data-stu-id="08ed6-189">After Clicking **Validate**, Flip **SAML(Enabled)** tooon.</span></span>

    <span data-ttu-id="08ed6-190">d.</span><span class="sxs-lookup"><span data-stu-id="08ed6-190">d.</span></span> <span data-ttu-id="08ed6-191">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-191">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="08ed6-192">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="08ed6-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="08ed6-193">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="08ed6-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="08ed6-194">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="08ed6-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="08ed6-195">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="08ed6-195">Create an Azure AD test user</span></span>
<span data-ttu-id="08ed6-196">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="08ed6-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="08ed6-198">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="08ed6-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="08ed6-199">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="08ed6-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="08ed6-201">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="08ed6-203">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="08ed6-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="08ed6-205">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="08ed6-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="08ed6-207">a.</span><span class="sxs-lookup"><span data-stu-id="08ed6-207">a.</span></span> <span data-ttu-id="08ed6-208">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="08ed6-209">b.</span><span class="sxs-lookup"><span data-stu-id="08ed6-209">b.</span></span> <span data-ttu-id="08ed6-210">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="08ed6-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="08ed6-211">c.</span><span class="sxs-lookup"><span data-stu-id="08ed6-211">c.</span></span> <span data-ttu-id="08ed6-212">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="08ed6-213">d.</span><span class="sxs-lookup"><span data-stu-id="08ed6-213">d.</span></span> <span data-ttu-id="08ed6-214">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-214">Click **Create**.</span></span>
 
### <a name="create-a-rfpio-test-user"></a><span data-ttu-id="08ed6-215">Créer un utilisateur de test RFPIO</span><span class="sxs-lookup"><span data-stu-id="08ed6-215">Create a RFPIO test user</span></span>

<span data-ttu-id="08ed6-216">tooenable Azure AD les utilisateurs toolog dans tooRFPIO, vous devez les configurer dans RFPIO.</span><span class="sxs-lookup"><span data-stu-id="08ed6-216">tooenable Azure AD users toolog in tooRFPIO, they must be provisioned into RFPIO.</span></span>  
<span data-ttu-id="08ed6-217">Dans les cas de hello de RFPIO, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="08ed6-217">In hello case of RFPIO, provisioning is a manual task.</span></span>

<span data-ttu-id="08ed6-218">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="08ed6-218">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="08ed6-219">Ouvrez une session dans tooyour site d’entreprise RFPIO en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="08ed6-219">Log in tooyour RFPIO company site as an administrator.</span></span>

2. <span data-ttu-id="08ed6-220">Cliquez sur la liste déroulante de hello en bas à gauche.</span><span class="sxs-lookup"><span data-stu-id="08ed6-220">Click on hello bottom left corner dropdown.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. <span data-ttu-id="08ed6-222">Cliquez sur hello **paramètres de l’organisation**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-222">Click on hello **Organization Settings**.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. <span data-ttu-id="08ed6-224">Cliquez sur **MEMBRES DE L’ÉQUIPE**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-224">Click **TEAM MEMBERS**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. <span data-ttu-id="08ed6-226">Cliquez sur **AJOUTER DES MEMBRES**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-226">Click on **ADD MEMBERS**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. <span data-ttu-id="08ed6-228">Bonjour **ajouter de nouveaux membres** section.</span><span class="sxs-lookup"><span data-stu-id="08ed6-228">In hello **Add New Members** section.</span></span> <span data-ttu-id="08ed6-229">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="08ed6-229">Perform following actions:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app8.png)

    <span data-ttu-id="08ed6-231">a.</span><span class="sxs-lookup"><span data-stu-id="08ed6-231">a.</span></span> <span data-ttu-id="08ed6-232">Entrée **adresse de messagerie** Bonjour **Entrez une adresse de messagerie par ligne** champ.</span><span class="sxs-lookup"><span data-stu-id="08ed6-232">Enter **Email address** in hello **Enter one email per line** field.</span></span>

    <span data-ttu-id="08ed6-233">b.</span><span class="sxs-lookup"><span data-stu-id="08ed6-233">b.</span></span> <span data-ttu-id="08ed6-234">Sélectionnez le **Rôle** selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="08ed6-234">Plese select **Role** according your requirements.</span></span>

    <span data-ttu-id="08ed6-235">c.</span><span class="sxs-lookup"><span data-stu-id="08ed6-235">c.</span></span> <span data-ttu-id="08ed6-236">Cliquez sur **AJOUTER DES MEMBRES**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-236">Click **ADD MEMBERS**.</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="08ed6-237">titulaire du compte Azure Active Directory Hello reçoit un message électronique et suit un tooconfirm de lier leur compte avant son activation.</span><span class="sxs-lookup"><span data-stu-id="08ed6-237">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="08ed6-238">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="08ed6-238">Assign hello Azure AD test user</span></span>

<span data-ttu-id="08ed6-239">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooRFPIO.</span><span class="sxs-lookup"><span data-stu-id="08ed6-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRFPIO.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="08ed6-241">**tooassign Britta Simon tooRFPIO, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="08ed6-241">**tooassign Britta Simon tooRFPIO, perform hello following steps:**</span></span>

1. <span data-ttu-id="08ed6-242">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="08ed6-244">Dans la liste des applications hello, sélectionnez **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-244">In hello applications list, select **RFPIO**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. <span data-ttu-id="08ed6-246">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="08ed6-248">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-248">Click **Add** button.</span></span> <span data-ttu-id="08ed6-249">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="08ed6-251">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="08ed6-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="08ed6-252">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="08ed6-253">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="08ed6-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="08ed6-254">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="08ed6-254">Test single sign-on</span></span>

<span data-ttu-id="08ed6-255">Dans cette section, vous testez votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="08ed6-255">In this section, you test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="08ed6-256">Lorsque vous cliquez sur hello RFPIO vignette dans le volet d’accès de hello, vous devez obtenir l’application de RFPIO tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="08ed6-256">When you click hello RFPIO tile in hello Access Panel, you should get automatically signed-on tooyour RFPIO application.</span></span>
<span data-ttu-id="08ed6-257">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="08ed6-257">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="08ed6-258">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="08ed6-258">Additional resources</span></span>

* [<span data-ttu-id="08ed6-259">Liste des didacticiels sur la façon de toointegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="08ed6-259">List of tutorials about how toointegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="08ed6-260">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="08ed6-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

