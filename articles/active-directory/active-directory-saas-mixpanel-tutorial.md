---
title: "Didacticiel : Intégration d’Azure Active Directory à Mixpanel | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Mixpanel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2df26ef-d441-44ac-a9f3-b37bf9709bcb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 8da8aaefee3558c37babe3e10aeba4224ceffa16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mixpanel"></a><span data-ttu-id="ba826-103">Didacticiel : Intégration d’Azure Active Directory à Mixpanel</span><span class="sxs-lookup"><span data-stu-id="ba826-103">Tutorial: Azure Active Directory integration with Mixpanel</span></span>

<span data-ttu-id="ba826-104">Dans ce didacticiel, vous apprendrez comment toointegrate Mixpanel avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ba826-104">In this tutorial, you learn how toointegrate Mixpanel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ba826-105">Intégration Mixpanel à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ba826-105">Integrating Mixpanel with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ba826-106">Vous pouvez contrôler dans Azure AD qui a accès tooMixpanel</span><span class="sxs-lookup"><span data-stu-id="ba826-106">You can control in Azure AD who has access tooMixpanel</span></span>
- <span data-ttu-id="ba826-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooMixpanel (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba826-107">You can enable your users tooautomatically get signed-on tooMixpanel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ba826-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="ba826-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ba826-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ba826-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba826-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ba826-110">Prerequisites</span></span>

<span data-ttu-id="ba826-111">tooconfigure intégration d’Azure AD avec Mixpanel, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ba826-111">tooconfigure Azure AD integration with Mixpanel, you need hello following items:</span></span>

- <span data-ttu-id="ba826-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba826-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ba826-113">Un abonnement Mixpanel pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="ba826-113">A Mixpanel single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ba826-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="ba826-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ba826-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="ba826-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ba826-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ba826-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ba826-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ba826-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ba826-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="ba826-118">Scenario description</span></span>
<span data-ttu-id="ba826-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="ba826-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ba826-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="ba826-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ba826-121">Ajout de Mixpanel à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="ba826-121">Adding Mixpanel from hello gallery</span></span>
2. <span data-ttu-id="ba826-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba826-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mixpanel-from-hello-gallery"></a><span data-ttu-id="ba826-123">Ajout de Mixpanel à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="ba826-123">Adding Mixpanel from hello gallery</span></span>
<span data-ttu-id="ba826-124">intégration de hello tooconfigure de Mixpanel dans Azure AD, vous devez tooadd Mixpanel à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="ba826-124">tooconfigure hello integration of Mixpanel into Azure AD, you need tooadd Mixpanel from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ba826-125">**tooadd Mixpanel à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ba826-125">**tooadd Mixpanel from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba826-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="ba826-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ba826-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="ba826-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ba826-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ba826-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="ba826-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ba826-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="ba826-133">Dans la zone de recherche de hello, tapez **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="ba826-133">In hello search box, type **Mixpanel**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_search.png)

5. <span data-ttu-id="ba826-135">Dans le volet de résultats hello, sélectionnez **Mixpanel**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ba826-135">In hello results panel, select **Mixpanel**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ba826-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba826-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ba826-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Mixpanel avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="ba826-138">In this section, you configure and test Azure AD single sign-on with Mixpanel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ba826-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Mixpanel est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba826-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mixpanel is tooa user in Azure AD.</span></span> <span data-ttu-id="ba826-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Mixpanel doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="ba826-140">In other words, a link relationship between an Azure AD user and hello related user in Mixpanel needs toobe established.</span></span>

<span data-ttu-id="ba826-141">Dans Mixpanel, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="ba826-141">In Mixpanel, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ba826-142">tooconfigure et test Azure AD l’authentification unique avec Mixpanel, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="ba826-142">tooconfigure and test Azure AD single sign-on with Mixpanel, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ba826-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ba826-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ba826-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ba826-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ba826-145">**[Création d’un utilisateur de test Mixpanel](#creating-a-mixpanel-test-user)**  -toohave un équivalent de Britta Simon dans Mixpanel est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ba826-145">**[Creating a Mixpanel test user](#creating-a-mixpanel-test-user)** - toohave a counterpart of Britta Simon in Mixpanel that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ba826-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ba826-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ba826-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="ba826-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ba826-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba826-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ba826-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="ba826-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mixpanel application.</span></span>

<span data-ttu-id="ba826-150">**tooconfigure Azure AD single sign-on avec Mixpanel, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ba826-150">**tooconfigure Azure AD single sign-on with Mixpanel, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba826-151">Bonjour portail Azure, sur hello **Mixpanel** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="ba826-151">In hello Azure portal, on hello **Mixpanel** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="ba826-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ba826-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_samlbase.png)

3. <span data-ttu-id="ba826-155">Sur hello **Mixpanel domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ba826-155">On hello **Mixpanel Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_url.png)

     <span data-ttu-id="ba826-157">Bonjour **URL de connexion** zone de texte, tapez une URL en tant que :`https://mixpanel.com/login/`</span><span class="sxs-lookup"><span data-stu-id="ba826-157">In hello **Sign-on URL** textbox, type a URL as: `https://mixpanel.com/login/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ba826-158">Inscrivez-vous à [https://mixpanel.com/register/](https://mixpanel.com/register/) tooset vos informations d’identification et de contact hello [équipe de support Mixpanel](mailto:support@mixpanel.com) tooenable les paramètres d’authentification unique pour votre client.</span><span class="sxs-lookup"><span data-stu-id="ba826-158">Please register at [https://mixpanel.com/register/](https://mixpanel.com/register/) tooset up your login credentials and  contact hello [Mixpanel support team](mailto:support@mixpanel.com) tooenable SSO settings for your tenant.</span></span> <span data-ttu-id="ba826-159">Vous pouvez également obtenir la valeur de l’URL de connexion si nécessaire à partir de votre équipe de support Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="ba826-159">You can also get your Sign On URL value if necessary from your Mixpanel support team.</span></span> 
 
4. <span data-ttu-id="ba826-160">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ba826-160">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_certificate.png) 

5. <span data-ttu-id="ba826-162">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="ba826-162">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mixpanel-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ba826-164">Sur hello **Mixpanel Configuration** , cliquez sur **Mixpanel de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="ba826-164">On hello **Mixpanel Configuration** section, click **Configure Mixpanel** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ba826-165">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="ba826-165">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_configure.png) 

7. <span data-ttu-id="ba826-167">Dans une autre fenêtre de navigateur, l’authentification tooyour application Mixpanel en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ba826-167">In a different browser window, sign-on tooyour Mixpanel application as an administrator.</span></span>

8. <span data-ttu-id="ba826-168">Bas de page de hello, cliquez sur hello peu **ENGRENAGE** icône dans le coin supérieur gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="ba826-168">On bottom of hello page, click hello little **gear** icon in hello left corner.</span></span> 
   
    ![Authentification unique Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_06.png) 

9. <span data-ttu-id="ba826-170">Cliquez sur hello **de sécurité d’accès** onglet, puis cliquez sur **modifier les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="ba826-170">Click hello **Access security** tab, and then click **Change settings**.</span></span>
   
    ![Paramètres Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_08.png) 

10. <span data-ttu-id="ba826-172">Sur hello **modifier votre certificat** page de boîte de dialogue, cliquez sur **choisir un fichier** tooupload votre certificat téléchargé, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="ba826-172">On hello **Change your certificate** dialog page, click **Choose file** tooupload your downloaded certificate, and then click **NEXT**.</span></span>
   
    ![Paramètres Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_09.png) 

11.  <span data-ttu-id="ba826-174">Dans la zone de texte URL de l’authentification hello sur hello **modifier votre URL d’authentification** page de boîte de dialogue, valeur hello coller **SAML Sign-On URL du Service unique** que vous avez copiée à partir du portail Azure, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ba826-174">In hello authentication URL textbox on hello **Change your authentication  URL** dialog page, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal, and then click **NEXT**.</span></span>
   
   ![Paramètres Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_10.png) 

12. <span data-ttu-id="ba826-176">Cliquez sur **Done**.</span><span class="sxs-lookup"><span data-stu-id="ba826-176">Click **Done**.</span></span>

> [!TIP]
> <span data-ttu-id="ba826-177">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="ba826-177">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ba826-178">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="ba826-178">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ba826-179">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ba826-179">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ba826-180">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba826-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="ba826-181">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="ba826-181">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="ba826-183">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ba826-183">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba826-184">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="ba826-184">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ba826-186">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ba826-186">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ba826-188">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="ba826-188">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ba826-190">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ba826-190">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ba826-192">a.</span><span class="sxs-lookup"><span data-stu-id="ba826-192">a.</span></span> <span data-ttu-id="ba826-193">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ba826-193">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ba826-194">b.</span><span class="sxs-lookup"><span data-stu-id="ba826-194">b.</span></span> <span data-ttu-id="ba826-195">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ba826-195">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ba826-196">c.</span><span class="sxs-lookup"><span data-stu-id="ba826-196">c.</span></span> <span data-ttu-id="ba826-197">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="ba826-197">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ba826-198">d.</span><span class="sxs-lookup"><span data-stu-id="ba826-198">d.</span></span> <span data-ttu-id="ba826-199">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="ba826-199">Click **Create**.</span></span>
 
### <a name="creating-a-mixpanel-test-user"></a><span data-ttu-id="ba826-200">Création d’un utilisateur de test Mixpanel</span><span class="sxs-lookup"><span data-stu-id="ba826-200">Creating a Mixpanel test user</span></span>

<span data-ttu-id="ba826-201">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="ba826-201">hello objective of this section is toocreate a user called Britta Simon in Mixpanel.</span></span> 

1. <span data-ttu-id="ba826-202">Se connecter tooyour Mixpanel site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ba826-202">Sign on tooyour Mixpanel company site as an administrator.</span></span>

2. <span data-ttu-id="ba826-203">Hello le bas de page de hello, cliquez sur hello ENGRENAGE peu bouton hello de tooopen à gauche hello **paramètres** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="ba826-203">On hello bottom of hello page, click hello little gear button on hello left corner tooopen hello **Settings** window.</span></span>

3. <span data-ttu-id="ba826-204">Cliquez sur hello **Team** onglet.</span><span class="sxs-lookup"><span data-stu-id="ba826-204">Click hello **Team** tab.</span></span>

4. <span data-ttu-id="ba826-205">Bonjour **membre de l’équipe** zone de texte, tapez l’adresse de messagerie de Brian Bonjour Azure.</span><span class="sxs-lookup"><span data-stu-id="ba826-205">In hello **team member** textbox, type Britta's email address in hello Azure.</span></span>
   
    ![Paramètres Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_11.png) 

5. <span data-ttu-id="ba826-207">Cliquez sur **Invite**.</span><span class="sxs-lookup"><span data-stu-id="ba826-207">Click **Invite**.</span></span> 

> [!Note]
> <span data-ttu-id="ba826-208">Hello utilisateur obtient un tooset par courrier électronique un profil de hello.</span><span class="sxs-lookup"><span data-stu-id="ba826-208">hello user will get an email tooset up hello profile.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ba826-209">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba826-209">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ba826-210">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooMixpanel.</span><span class="sxs-lookup"><span data-stu-id="ba826-210">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMixpanel.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="ba826-212">**tooassign Britta Simon tooMixpanel, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ba826-212">**tooassign Britta Simon tooMixpanel, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba826-213">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ba826-213">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="ba826-215">Dans la liste des applications hello, sélectionnez **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="ba826-215">In hello applications list, select **Mixpanel**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_app.png) 

3. <span data-ttu-id="ba826-217">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ba826-217">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="ba826-219">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ba826-219">Click **Add** button.</span></span> <span data-ttu-id="ba826-220">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ba826-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="ba826-222">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="ba826-222">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ba826-223">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ba826-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ba826-224">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ba826-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ba826-225">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ba826-225">Testing single sign-on</span></span>

<span data-ttu-id="ba826-226">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="ba826-226">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ba826-227">Lorsque vous cliquez sur mosaïque Mixpanel hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Mixpanel application.</span><span class="sxs-lookup"><span data-stu-id="ba826-227">When you click hello Mixpanel tile in hello Access Panel, you should get automatically signed-on tooyour Mixpanel application.</span></span>
<span data-ttu-id="ba826-228">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ba826-228">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ba826-229">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ba826-229">Additional resources</span></span>

* [<span data-ttu-id="ba826-230">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ba826-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ba826-231">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="ba826-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_203.png

