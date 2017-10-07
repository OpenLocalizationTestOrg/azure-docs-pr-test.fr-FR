---
title: "Didacticiel : Intégration d’Azure Active Directory à RunMyProcess | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et RunMyProcess."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f02acda015aeb8d131d8e3ef88bf50c4e8e94750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a><span data-ttu-id="81611-103">Didacticiel : Intégration d’Azure Active Directory à RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="81611-103">Tutorial: Azure Active Directory integration with RunMyProcess</span></span>

<span data-ttu-id="81611-104">Dans ce didacticiel, vous apprendrez comment toointegrate RunMyProcess avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="81611-104">In this tutorial, you learn how toointegrate RunMyProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="81611-105">Intégration de RunMyProcess à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="81611-105">Integrating RunMyProcess with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="81611-106">Vous pouvez contrôler dans Azure AD qui a accès tooRunMyProcess</span><span class="sxs-lookup"><span data-stu-id="81611-106">You can control in Azure AD who has access tooRunMyProcess</span></span>
- <span data-ttu-id="81611-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooRunMyProcess (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="81611-107">You can enable your users tooautomatically get signed-on tooRunMyProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="81611-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="81611-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="81611-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="81611-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81611-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="81611-110">Prerequisites</span></span>

<span data-ttu-id="81611-111">tooconfigure intégration d’Azure AD à RunMyProcess, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="81611-111">tooconfigure Azure AD integration with RunMyProcess, you need hello following items:</span></span>

- <span data-ttu-id="81611-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="81611-112">An Azure AD subscription</span></span>
- <span data-ttu-id="81611-113">Un abonnement RunMyProcess pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="81611-113">A RunMyProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="81611-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="81611-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="81611-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="81611-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="81611-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="81611-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="81611-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez bénéficier de l’[offre d’essai](https://azure.microsoft.com/pricing/free-trial/) d’un mois.</span><span class="sxs-lookup"><span data-stu-id="81611-117">If you don't have an Azure AD trial environment, you can get a one-month trial here:[Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="81611-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="81611-118">Scenario description</span></span>
<span data-ttu-id="81611-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="81611-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="81611-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="81611-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="81611-121">Ajout de RunMyProcess à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="81611-121">Adding RunMyProcess from hello gallery</span></span>
2. <span data-ttu-id="81611-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="81611-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-runmyprocess-from-hello-gallery"></a><span data-ttu-id="81611-123">Ajout de RunMyProcess à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="81611-123">Adding RunMyProcess from hello gallery</span></span>
<span data-ttu-id="81611-124">intégration de hello tooconfigure de RunMyProcess dans Azure AD, vous devez tooadd RunMyProcess à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="81611-124">tooconfigure hello integration of RunMyProcess into Azure AD, you need tooadd RunMyProcess from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="81611-125">**tooadd RunMyProcess à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="81611-125">**tooadd RunMyProcess from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="81611-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="81611-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="81611-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="81611-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="81611-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="81611-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="81611-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="81611-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="81611-133">Dans la zone de recherche de hello, tapez **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="81611-133">In hello search box, type **RunMyProcess**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_search.png)

5. <span data-ttu-id="81611-135">Dans le volet de résultats hello, sélectionnez **RunMyProcess**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="81611-135">In hello results panel, select **RunMyProcess**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="81611-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="81611-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="81611-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec RunMyProcess sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="81611-138">In this section, you configure and test Azure AD single sign-on with RunMyProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="81611-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans RunMyProcess est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81611-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RunMyProcess is tooa user in Azure AD.</span></span> <span data-ttu-id="81611-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans RunMyProcess doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="81611-140">In other words, a link relationship between an Azure AD user and hello related user in RunMyProcess needs toobe established.</span></span>

<span data-ttu-id="81611-141">Dans RunMyProcess, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="81611-141">In RunMyProcess, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="81611-142">tooconfigure et test Azure AD l’authentification unique avec RunMyProcess, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="81611-142">tooconfigure and test Azure AD single sign-on with RunMyProcess, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="81611-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="81611-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="81611-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="81611-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="81611-145">**[Création d’un utilisateur de test de RunMyProcess](#creating-a-runmyprocess-test-user)**  -toohave un équivalent de Britta Simon dans RunMyProcess est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="81611-145">**[Creating a RunMyProcess test user](#creating-a-runmyprocess-test-user)** - toohave a counterpart of Britta Simon in RunMyProcess that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="81611-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="81611-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="81611-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="81611-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="81611-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="81611-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="81611-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="81611-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RunMyProcess application.</span></span>

<span data-ttu-id="81611-150">**tooconfigure Azure AD single sign-on avec RunMyProcess, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="81611-150">**tooconfigure Azure AD single sign-on with RunMyProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="81611-151">Bonjour portail Azure, sur hello **RunMyProcess** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="81611-151">In hello Azure portal, on hello **RunMyProcess** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="81611-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="81611-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_samlbase.png)

3. <span data-ttu-id="81611-155">Sur hello **RunMyProcess domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="81611-155">On hello **RunMyProcess Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_url.png)

    <span data-ttu-id="81611-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://live.runmyprocess.com/live/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="81611-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://live.runmyprocess.com/live/<tenant id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="81611-158">valeur de Hello n’est pas réelle.</span><span class="sxs-lookup"><span data-stu-id="81611-158">hello value is not real.</span></span> <span data-ttu-id="81611-159">Valeur de hello de mise à jour avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="81611-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="81611-160">Contact [équipe de support Client de RunMyProcess](mailto:support@runmyprocess.com) valeur hello de tooget.</span><span class="sxs-lookup"><span data-stu-id="81611-160">Contact [RunMyProcess Client support team](mailto:support@runmyprocess.com) tooget hello value.</span></span> 

4. <span data-ttu-id="81611-161">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="81611-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_certificate.png) 

5. <span data-ttu-id="81611-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="81611-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="81611-165">Sur hello **RunMyProcess Configuration** , cliquez sur **configurer de RunMyProcess** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="81611-165">On hello **RunMyProcess Configuration** section, click **Configure RunMyProcess** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="81611-166">Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="81611-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_configure.png) 

7. <span data-ttu-id="81611-168">Dans une fenêtre de navigateur web, client de RunMyProcess tooyour ouverture de session en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="81611-168">In a different web browser window, sign-on tooyour RunMyProcess tenant as an administrator.</span></span>

8. <span data-ttu-id="81611-169">Dans le volet de navigation à gauche, cliquez sur **Compte** et sélectionnez **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="81611-169">In left navigation panel, click **Account** and select **Configuration**.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_001.png)

9. <span data-ttu-id="81611-171">Accédez trop**méthode d’authentification** section et suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="81611-171">Go too**Authentication method** section and perform below steps:</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_002.png)

    <span data-ttu-id="81611-173">a.</span><span class="sxs-lookup"><span data-stu-id="81611-173">a.</span></span> <span data-ttu-id="81611-174">Pour **Method**, sélectionnez **SSO with Samlv2**.</span><span class="sxs-lookup"><span data-stu-id="81611-174">As **Method**, select **SSO with Samlv2**.</span></span> 

    <span data-ttu-id="81611-175">b.</span><span class="sxs-lookup"><span data-stu-id="81611-175">b.</span></span> <span data-ttu-id="81611-176">Bonjour **redirection de l’authentification unique** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="81611-176">In hello **SSO redirect** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="81611-177">c.</span><span class="sxs-lookup"><span data-stu-id="81611-177">c.</span></span> <span data-ttu-id="81611-178">Bonjour **redirection de déconnexion** zone de texte, valeur hello coller **URL de déconnexion**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="81611-178">In hello **Logout redirect** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="81611-179">d.</span><span class="sxs-lookup"><span data-stu-id="81611-179">d.</span></span> <span data-ttu-id="81611-180">Bonjour **Format d’Id de nom** zone de texte, valeur type hello **Name Identifier Format** en tant que **urn : oasis : noms : tc : SAML:1.1:nameid-format : emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="81611-180">In hello **Name Id Format** textbox, type hello value of **Name Identifier Format** as **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="81611-181">e.</span><span class="sxs-lookup"><span data-stu-id="81611-181">e.</span></span> <span data-ttu-id="81611-182">Copier le contenu du fichier de certificat téléchargé hello hello et le coller ensuite dans hello **certificat** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="81611-182">Copy hello content of hello downloaded certificate file and then paste it into hello **Certificate** textbox.</span></span> 
 
    <span data-ttu-id="81611-183">f.</span><span class="sxs-lookup"><span data-stu-id="81611-183">f.</span></span> <span data-ttu-id="81611-184">Cliquez sur l’icône **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="81611-184">Click **Save** icon.</span></span>

> [!TIP]
> <span data-ttu-id="81611-185">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="81611-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="81611-186">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="81611-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="81611-187">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="81611-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="81611-188">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="81611-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="81611-189">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="81611-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="81611-191">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="81611-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="81611-192">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="81611-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="81611-194">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="81611-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="81611-196">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="81611-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="81611-198">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="81611-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="81611-200">a.</span><span class="sxs-lookup"><span data-stu-id="81611-200">a.</span></span> <span data-ttu-id="81611-201">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="81611-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="81611-202">b.</span><span class="sxs-lookup"><span data-stu-id="81611-202">b.</span></span> <span data-ttu-id="81611-203">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="81611-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="81611-204">c.</span><span class="sxs-lookup"><span data-stu-id="81611-204">c.</span></span> <span data-ttu-id="81611-205">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="81611-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="81611-206">d.</span><span class="sxs-lookup"><span data-stu-id="81611-206">d.</span></span> <span data-ttu-id="81611-207">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="81611-207">Click **Create**.</span></span>
 
### <a name="creating-a-runmyprocess-test-user"></a><span data-ttu-id="81611-208">Création d’un utilisateur de test de RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="81611-208">Creating a RunMyProcess test user</span></span>

<span data-ttu-id="81611-209">Dans l’ordre tooenable Azure AD les utilisateurs toolog dans tooRunMyProcess, vous devez les configurer dans RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="81611-209">In order tooenable Azure AD users toolog in tooRunMyProcess, they must be provisioned into RunMyProcess.</span></span> <span data-ttu-id="81611-210">Dans les cas de hello de RunMyProcess, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="81611-210">In hello case of RunMyProcess, provisioning is a manual task.</span></span>

<span data-ttu-id="81611-211">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="81611-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="81611-212">Ouvrez une session dans tooyour site d’entreprise RunMyProcess en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="81611-212">Log in tooyour RunMyProcess company site as an administrator.</span></span>

2. <span data-ttu-id="81611-213">Dans le volet de navigation à gauche, cliquez sur **Compte** et sélectionnez **Utilisateurs**, puis cliquez sur **Nouvel utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="81611-213">Click **Account** and select **Users** in left navigation panel, then click **New User**.</span></span>
   
    <span data-ttu-id="81611-214">![Nouvel utilisateur](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "Nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="81611-214">![New User](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "New User")</span></span>

3. <span data-ttu-id="81611-215">Bonjour **paramètres utilisateur** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="81611-215">In hello **User Settings** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="81611-216">![Profil](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profil")</span><span class="sxs-lookup"><span data-stu-id="81611-216">![Profile](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profile")</span></span> 
  
    <span data-ttu-id="81611-217">a.</span><span class="sxs-lookup"><span data-stu-id="81611-217">a.</span></span> <span data-ttu-id="81611-218">Hello de type **nom** et **messagerie** d’un Azure valide compte AD tooprovision dans hello relatives des zones de texte.</span><span class="sxs-lookup"><span data-stu-id="81611-218">Type hello **Name** and **E-mail** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span> 

    <span data-ttu-id="81611-219">b.</span><span class="sxs-lookup"><span data-stu-id="81611-219">b.</span></span> <span data-ttu-id="81611-220">Sélectionnez des options pour **IDE language**, **Language** et **Profile**.</span><span class="sxs-lookup"><span data-stu-id="81611-220">Select an **IDE language**, **Language**, and **Profile**.</span></span> 

    <span data-ttu-id="81611-221">c.</span><span class="sxs-lookup"><span data-stu-id="81611-221">c.</span></span> <span data-ttu-id="81611-222">Sélectionnez **toome de courrier électronique de la création de compte d’envoi**.</span><span class="sxs-lookup"><span data-stu-id="81611-222">Select **Send account creation e-mail toome**.</span></span> 

    <span data-ttu-id="81611-223">d.</span><span class="sxs-lookup"><span data-stu-id="81611-223">d.</span></span> <span data-ttu-id="81611-224">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="81611-224">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="81611-225">Vous pouvez utiliser n’importe quel autre RunMyProcess utilisateur compte outil de création ou API fournie par RunMyProcess tooprovision Azure Active Directory des comptes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="81611-225">You can use any other RunMyProcess user account creation tools or APIs provided by RunMyProcess tooprovision Azure Active Directory user accounts.</span></span> 
    > 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="81611-226">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="81611-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="81611-227">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooRunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="81611-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRunMyProcess.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="81611-229">**tooassign Britta Simon tooRunMyProcess, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="81611-229">**tooassign Britta Simon tooRunMyProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="81611-230">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="81611-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="81611-232">Dans la liste des applications hello, sélectionnez **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="81611-232">In hello applications list, select **RunMyProcess**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_app.png) 

3. <span data-ttu-id="81611-234">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="81611-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="81611-236">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="81611-236">Click **Add** button.</span></span> <span data-ttu-id="81611-237">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="81611-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="81611-239">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="81611-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="81611-240">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="81611-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="81611-241">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="81611-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="81611-242">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="81611-242">Testing single sign-on</span></span>

<span data-ttu-id="81611-243">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="81611-243">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="81611-244">Lorsque vous cliquez sur hello RunMyProcess vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour RunMyProcess application.</span><span class="sxs-lookup"><span data-stu-id="81611-244">When you click hello RunMyProcess tile in hello Access Panel, you should get automatically signed-on tooyour RunMyProcess application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="81611-245">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="81611-245">Additional resources</span></span>

* [<span data-ttu-id="81611-246">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="81611-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="81611-247">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="81611-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_203.png

