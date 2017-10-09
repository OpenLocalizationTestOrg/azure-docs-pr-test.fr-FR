---
title: "Didacticiel : intégration d’Azure Active Directory à Projectplace | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Projectplace."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 298059ca-b652-4577-916a-c31393d53d7a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 95d109052096161f995ff26a18f8d64f0c4a3dc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-projectplace"></a><span data-ttu-id="add81-103">Didacticiel : Intégration d’Azure Active Directory à Projectplace</span><span class="sxs-lookup"><span data-stu-id="add81-103">Tutorial: Azure Active Directory integration with Projectplace</span></span>

<span data-ttu-id="add81-104">Dans ce didacticiel, vous apprendrez comment toointegrate Projectplace avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="add81-104">In this tutorial, you learn how toointegrate Projectplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="add81-105">Intégration de Projectplace à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="add81-105">Integrating Projectplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="add81-106">Vous pouvez contrôler dans Azure AD qui a accès tooProjectplace</span><span class="sxs-lookup"><span data-stu-id="add81-106">You can control in Azure AD who has access tooProjectplace</span></span>
- <span data-ttu-id="add81-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooProjectplace (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="add81-107">You can enable your users tooautomatically get signed-on tooProjectplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="add81-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="add81-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="add81-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="add81-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="add81-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="add81-110">Prerequisites</span></span>

<span data-ttu-id="add81-111">tooconfigure intégration d’Azure AD à Projectplace, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="add81-111">tooconfigure Azure AD integration with Projectplace, you need hello following items:</span></span>

- <span data-ttu-id="add81-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="add81-112">An Azure AD subscription</span></span>
- <span data-ttu-id="add81-113">Un abonnement Projectplace pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="add81-113">A Projectplace single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="add81-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="add81-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="add81-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="add81-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="add81-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="add81-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="add81-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="add81-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="add81-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="add81-118">Scenario description</span></span>
<span data-ttu-id="add81-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="add81-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="add81-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="add81-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="add81-121">Ajout de Projectplace à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="add81-121">Adding Projectplace from hello gallery</span></span>
2. <span data-ttu-id="add81-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="add81-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-projectplace-from-hello-gallery"></a><span data-ttu-id="add81-123">Ajout de Projectplace à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="add81-123">Adding Projectplace from hello gallery</span></span>
<span data-ttu-id="add81-124">intégration de hello tooconfigure de Projectplace dans Azure AD, vous devez tooadd Projectplace à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="add81-124">tooconfigure hello integration of Projectplace into Azure AD, you need tooadd Projectplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="add81-125">**tooadd Projectplace à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="add81-125">**tooadd Projectplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="add81-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="add81-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="add81-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="add81-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="add81-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="add81-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="add81-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="add81-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="add81-133">Dans la zone de recherche de hello, tapez **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="add81-133">In hello search box, type **Projectplace**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_search.png)

5. <span data-ttu-id="add81-135">Dans le volet de résultats hello, sélectionnez **Projectplace**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="add81-135">In hello results panel, select **Projectplace**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="add81-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="add81-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="add81-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Projectplace, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="add81-138">In this section, you configure and test Azure AD single sign-on with Projectplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="add81-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Projectplace est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="add81-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Projectplace is tooa user in Azure AD.</span></span> <span data-ttu-id="add81-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur de Projectplace hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="add81-140">In other words, a link relationship between an Azure AD user and hello related user in Projectplace needs toobe established.</span></span>

<span data-ttu-id="add81-141">Dans Projectplace, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="add81-141">In Projectplace, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="add81-142">tooconfigure et test Azure AD l’authentification unique avec Projectplace, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="add81-142">tooconfigure and test Azure AD single sign-on with Projectplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="add81-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="add81-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="add81-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="add81-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="add81-145">**[Création d’un utilisateur de test de Projectplace](#creating-a-projectplace-test-user)**  -toohave un équivalent de Britta Simon dans Projectplace est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="add81-145">**[Creating a Projectplace test user](#creating-a-projectplace-test-user)** - toohave a counterpart of Britta Simon in Projectplace that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="add81-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="add81-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="add81-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="add81-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="add81-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="add81-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="add81-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Projectplace.</span><span class="sxs-lookup"><span data-stu-id="add81-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Projectplace application.</span></span>

<span data-ttu-id="add81-150">**tooconfigure Azure AD single sign-on avec Projectplace, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="add81-150">**tooconfigure Azure AD single sign-on with Projectplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="add81-151">Bonjour portail Azure, sur hello **Projectplace** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="add81-151">In hello Azure portal, on hello **Projectplace** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="add81-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="add81-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_samlbase.png)

3. <span data-ttu-id="add81-155">Sur hello **Projectplace domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="add81-155">On hello **Projectplace Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_url.png)

    <span data-ttu-id="add81-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company>.projectplace.com`</span><span class="sxs-lookup"><span data-stu-id="add81-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.projectplace.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="add81-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="add81-158">This value is not real.</span></span> <span data-ttu-id="add81-159">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="add81-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="add81-160">Contact [équipe de support Projectplace Client](https://success.planview.com/Projectplace/Support) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="add81-160">Contact [Projectplace Client support team](https://success.planview.com/Projectplace/Support) tooget this value.</span></span> 
 
4. <span data-ttu-id="add81-161">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="add81-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_certificate.png) 

5. <span data-ttu-id="add81-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="add81-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-projectplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="add81-165">tooconfigure l’authentification unique sur **Projectplace** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support Projectplace](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="add81-165">tooconfigure single sign-on on **Projectplace** side, you need toosend hello downloaded **Metadata XML** too[Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="add81-166">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="add81-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="add81-167">configuration de l’authentification unique de l’Hello a toobe effectuée par hello [équipe de support Projectplace](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="add81-167">hello single sign-on configuration has toobe performed by hello [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="add81-168">Vous recevez une notification dès que hello configuration a été effectuée.</span><span class="sxs-lookup"><span data-stu-id="add81-168">You will get a notification as soon as hello configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="add81-169">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="add81-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="add81-170">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="add81-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="add81-171">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="add81-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="add81-172">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="add81-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="add81-173">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="add81-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="add81-175">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="add81-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="add81-176">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="add81-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="add81-178">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="add81-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="add81-180">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="add81-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="add81-182">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="add81-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="add81-184">a.</span><span class="sxs-lookup"><span data-stu-id="add81-184">a.</span></span> <span data-ttu-id="add81-185">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="add81-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="add81-186">b.</span><span class="sxs-lookup"><span data-stu-id="add81-186">b.</span></span> <span data-ttu-id="add81-187">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="add81-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="add81-188">c.</span><span class="sxs-lookup"><span data-stu-id="add81-188">c.</span></span> <span data-ttu-id="add81-189">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="add81-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="add81-190">d.</span><span class="sxs-lookup"><span data-stu-id="add81-190">d.</span></span> <span data-ttu-id="add81-191">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="add81-191">Click **Create**.</span></span>
 
### <a name="creating-a-projectplace-test-user"></a><span data-ttu-id="add81-192">Création d’un utilisateur de test Projectplace</span><span class="sxs-lookup"><span data-stu-id="add81-192">Creating a Projectplace test user</span></span>

<span data-ttu-id="add81-193">Dans l’ordre tooenable Azure AD les utilisateurs toolog à Projectplace, vous devez les configurer dans Projectplace.</span><span class="sxs-lookup"><span data-stu-id="add81-193">In order tooenable Azure AD users toolog into Projectplace, they must be provisioned into Projectplace.</span></span> <span data-ttu-id="add81-194">Dans les cas de hello de Projectplace, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="add81-194">In hello case of Projectplace, provisioning is a manual task.</span></span>

<span data-ttu-id="add81-195">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="add81-195">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="add81-196">Connectez-vous à tooyour **Projectplace** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="add81-196">Log in tooyour **Projectplace** company site as an administrator.</span></span>

2. <span data-ttu-id="add81-197">Accédez trop**personnes**, puis cliquez sur **membres**.</span><span class="sxs-lookup"><span data-stu-id="add81-197">Go too**People**, and then click **Members**.</span></span>
   
    <span data-ttu-id="add81-198">![Personnes](./media/active-directory-saas-projectplace-tutorial/ic790228.png "Personnes")</span><span class="sxs-lookup"><span data-stu-id="add81-198">![People](./media/active-directory-saas-projectplace-tutorial/ic790228.png "People")</span></span>

3. <span data-ttu-id="add81-199">Cliquez sur **Add Member**.</span><span class="sxs-lookup"><span data-stu-id="add81-199">Click **Add Member**.</span></span>
   
    <span data-ttu-id="add81-200">![Ajouter des membres](./media/active-directory-saas-projectplace-tutorial/ic790232.png "ajouter des membres")</span><span class="sxs-lookup"><span data-stu-id="add81-200">![Add Members](./media/active-directory-saas-projectplace-tutorial/ic790232.png "Add Members")</span></span>

4. <span data-ttu-id="add81-201">Bonjour **Add Member** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="add81-201">In hello **Add Member** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="add81-202">![Nouveaux membres](./media/active-directory-saas-projectplace-tutorial/ic790233.png "nouveaux membres")</span><span class="sxs-lookup"><span data-stu-id="add81-202">![New Members](./media/active-directory-saas-projectplace-tutorial/ic790233.png "New Members")</span></span>
   
    <span data-ttu-id="add81-203">a.</span><span class="sxs-lookup"><span data-stu-id="add81-203">a.</span></span> <span data-ttu-id="add81-204">Bonjour **nouveaux membres** zone de texte, tapez Bonjour adresse de messagerie d’un compte AAD valide que vous voulez tooprovision dans hello relatives des zones de texte.</span><span class="sxs-lookup"><span data-stu-id="add81-204">In hello **New Members** textbox, type hello email address of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="add81-205">b.</span><span class="sxs-lookup"><span data-stu-id="add81-205">b.</span></span> <span data-ttu-id="add81-206">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="add81-206">Click **Send**.</span></span>

   <span data-ttu-id="add81-207">Un message électronique contenant un compte de hello tooconfirm lien avant son activation est envoyé à son compte Azure Active Directory toohello.</span><span class="sxs-lookup"><span data-stu-id="add81-207">An email including a link tooconfirm hello account before it becomes active is sent toohello Azure Active Directory account holder.</span></span>

>[!NOTE]
><span data-ttu-id="add81-208">Vous pouvez utiliser n’importe quel autre Projectplace utilisateur compte outil de création ou API fournie par Projectplace tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="add81-208">You can use any other Projectplace user account creation tools or APIs provided by Projectplace tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="add81-209">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="add81-209">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="add81-210">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooProjectplace.</span><span class="sxs-lookup"><span data-stu-id="add81-210">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooProjectplace.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="add81-212">**tooassign Britta Simon tooProjectplace, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="add81-212">**tooassign Britta Simon tooProjectplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="add81-213">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="add81-213">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="add81-215">Dans la liste des applications hello, sélectionnez **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="add81-215">In hello applications list, select **Projectplace**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_app.png) 

3. <span data-ttu-id="add81-217">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="add81-217">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="add81-219">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="add81-219">Click **Add** button.</span></span> <span data-ttu-id="add81-220">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="add81-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="add81-222">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="add81-222">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="add81-223">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="add81-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="add81-224">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="add81-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="add81-225">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="add81-225">Testing single sign-on</span></span>

<span data-ttu-id="add81-226">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="add81-226">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="add81-227">Lorsque vous cliquez sur mosaïque Projectplace hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Projectplace application.</span><span class="sxs-lookup"><span data-stu-id="add81-227">When you click hello Projectplace tile in hello Access Panel, you should get automatically signed-on tooyour Projectplace application.</span></span>
<span data-ttu-id="add81-228">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="add81-228">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="add81-229">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="add81-229">Additional resources</span></span>

* [<span data-ttu-id="add81-230">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="add81-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="add81-231">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="add81-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_203.png

