---
title: "Didacticiel : Intégration d’Azure Active Directory à Front | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de premier plan."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 4be363a3d338ec9268f3324daab4a80346ec3131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a><span data-ttu-id="64132-103">Didacticiel : Intégration d’Azure Active Directory avec Front</span><span class="sxs-lookup"><span data-stu-id="64132-103">Tutorial: Azure Active Directory integration with Front</span></span>

<span data-ttu-id="64132-104">Dans ce didacticiel, vous apprendrez comment toointegrate avant avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="64132-104">In this tutorial, you learn how toointegrate Front with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="64132-105">Intégration de début avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="64132-105">Integrating Front with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="64132-106">Vous pouvez contrôler dans Azure AD qui a accès tooFront.</span><span class="sxs-lookup"><span data-stu-id="64132-106">You can control in Azure AD who has access tooFront.</span></span>
- <span data-ttu-id="64132-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooFront (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64132-107">You can enable your users tooautomatically get signed-on tooFront (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="64132-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="64132-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="64132-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="64132-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64132-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="64132-110">Prerequisites</span></span>

<span data-ttu-id="64132-111">intégration tooconfigure Azure AD avec avant, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="64132-111">tooconfigure Azure AD integration with Front, you need hello following items:</span></span>

- <span data-ttu-id="64132-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="64132-112">An Azure AD subscription</span></span>
- <span data-ttu-id="64132-113">Un abonnement Front pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="64132-113">A Front single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="64132-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="64132-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="64132-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="64132-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="64132-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="64132-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="64132-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="64132-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="64132-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="64132-118">Scenario description</span></span>
<span data-ttu-id="64132-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="64132-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="64132-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="64132-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="64132-121">Ajout de premier plan à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="64132-121">Adding Front from hello gallery</span></span>
2. <span data-ttu-id="64132-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="64132-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-front-from-hello-gallery"></a><span data-ttu-id="64132-123">Ajout de premier plan à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="64132-123">Adding Front from hello gallery</span></span>
<span data-ttu-id="64132-124">tooconfigure hello intégration de premier plan dans Azure AD, vous devez tooadd avant à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="64132-124">tooconfigure hello integration of Front into Azure AD, you need tooadd Front from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="64132-125">**tooadd avant de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="64132-125">**tooadd Front from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="64132-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="64132-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="64132-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="64132-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="64132-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="64132-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="64132-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="64132-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="64132-133">Dans la zone de recherche de hello, tapez **avant**, sélectionnez **avant** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="64132-133">In hello search box, type **Front**, select **Front** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Premier plan dans la liste des résultats hello](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="64132-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="64132-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="64132-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Front, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="64132-136">In this section, you configure and test Azure AD single sign-on with Front based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="64132-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur au début de hello équivalent est tooa dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64132-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Front is tooa user in Azure AD.</span></span> <span data-ttu-id="64132-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur connexes de hello devant doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="64132-138">In other words, a link relationship between an Azure AD user and hello related user in Front needs toobe established.</span></span>

<span data-ttu-id="64132-139">Affecter au premier plan, de valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="64132-139">In Front, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="64132-140">tooconfigure et test Azure AD l’authentification unique avec avant, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="64132-140">tooconfigure and test Azure AD single sign-on with Front, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="64132-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="64132-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="64132-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="64132-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="64132-143">**[Créer un utilisateur de test avant](#create-a-front-test-user)**  -toohave de contrepartie Britta Simon à l’avant qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="64132-143">**[Create a Front test user](#create-a-front-test-user)** - toohave a counterpart of Britta Simon in Front that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="64132-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="64132-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="64132-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="64132-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="64132-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="64132-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="64132-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application avant.</span><span class="sxs-lookup"><span data-stu-id="64132-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Front application.</span></span>

<span data-ttu-id="64132-148">**tooconfigure Azure AD l’authentification unique avec avant, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="64132-148">**tooconfigure Azure AD single sign-on with Front, perform hello following steps:**</span></span>

1. <span data-ttu-id="64132-149">Bonjour portail Azure, sur hello **avant** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="64132-149">In hello Azure portal, on hello **Front** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="64132-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="64132-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. <span data-ttu-id="64132-153">Sur hello **avant de domaine et les URL** section, si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="64132-153">On hello **Front Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    <span data-ttu-id="64132-155">a.</span><span class="sxs-lookup"><span data-stu-id="64132-155">a.</span></span> <span data-ttu-id="64132-156">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="64132-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com`</span></span>

    <span data-ttu-id="64132-157">b.</span><span class="sxs-lookup"><span data-stu-id="64132-157">b.</span></span> <span data-ttu-id="64132-158">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.frontapp.com/sso/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="64132-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com/sso/saml/callback`</span></span>

4. <span data-ttu-id="64132-159">Vérifiez **afficher les paramètres d’URL avancés**, si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="64132-159">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    <span data-ttu-id="64132-161">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="64132-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="64132-162">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="64132-162">These values are not real.</span></span> <span data-ttu-id="64132-163">Mise à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion qui sont expliquées plus loin dans le didacticiel ou contactez [équipe de support Client avant](mailto:support@frontapp.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="64132-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL which are explained later in tutorial or contact [Front Client support team](mailto:support@frontapp.com) tooget these values.</span></span> 

5. <span data-ttu-id="64132-164">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="64132-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. <span data-ttu-id="64132-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="64132-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="64132-168">Sur hello **avant Configuration** , cliquez sur **configurer avant** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="64132-168">On hello **Front Configuration** section, click **Configure Front** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="64132-169">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="64132-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. <span data-ttu-id="64132-171">Client avant de l’authentification tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="64132-171">Sign-on tooyour Front tenant as an administrator.</span></span>

9. <span data-ttu-id="64132-172">Accédez trop**(icône représentant une roue dentée bas hello du volet de gauche hello) de paramètres > Préférences**.</span><span class="sxs-lookup"><span data-stu-id="64132-172">Go too**Settings (cog icon at hello bottom of hello left sidebar) > Preferences**.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. <span data-ttu-id="64132-174">Cliquez sur le lien **Authentification unique** .</span><span class="sxs-lookup"><span data-stu-id="64132-174">Click **Single Sign On** link.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. <span data-ttu-id="64132-176">Sélectionnez **SAML** dans la liste déroulante de hello de **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="64132-176">Select **SAML** in hello drop-down list of **Single Sign On**.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. <span data-ttu-id="64132-178">Bonjour **Point d’entrée** zone de texte placer la valeur hello **-Service URL d’authentification** à partir de l’Assistant configuration d’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64132-178">In hello **Entry Point** textbox put hello value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
    
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. <span data-ttu-id="64132-180">Ouvrez votre téléchargé **Certificate(Base64)** dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et collez-la toohello **certificat de signature** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="64132-180">Open your downloaded **Certificate(Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Signing certificate** textbox.</span></span>
    
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. <span data-ttu-id="64132-182">Sur hello **paramètres du fournisseur de Service** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="64132-182">On hello **Service provider settings** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    <span data-ttu-id="64132-184">a.</span><span class="sxs-lookup"><span data-stu-id="64132-184">a.</span></span> <span data-ttu-id="64132-185">Copiez la valeur hello **ID d’entité** et collez-le dans hello **identificateur** zone de texte dans **avant de domaine et les URL** section dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="64132-185">Copy hello value of **Entity ID** and paste it into hello **Identifier** textbox in **Front Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="64132-186">b.</span><span class="sxs-lookup"><span data-stu-id="64132-186">b.</span></span> <span data-ttu-id="64132-187">Copiez la valeur hello **URL ACS** et collez-le dans hello **URL de connexion** zone de texte dans **avant de domaine et les URL** section dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="64132-187">Copy hello value of **ACS URL** and paste it into hello **Sign-on URL** textbox in **Front Domain and URLs** section in Azure portal.</span></span>
    
15. <span data-ttu-id="64132-188">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="64132-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="64132-189">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="64132-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="64132-190">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="64132-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="64132-191">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="64132-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="64132-192">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="64132-192">Create an Azure AD test user</span></span>

<span data-ttu-id="64132-193">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="64132-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="64132-195">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="64132-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="64132-196">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="64132-196">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="64132-198">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="64132-198">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="64132-200">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="64132-200">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="64132-202">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="64132-202">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    <span data-ttu-id="64132-204">a.</span><span class="sxs-lookup"><span data-stu-id="64132-204">a.</span></span> <span data-ttu-id="64132-205">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="64132-205">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="64132-206">b.</span><span class="sxs-lookup"><span data-stu-id="64132-206">b.</span></span> <span data-ttu-id="64132-207">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="64132-207">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="64132-208">c.</span><span class="sxs-lookup"><span data-stu-id="64132-208">c.</span></span> <span data-ttu-id="64132-209">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="64132-209">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="64132-210">d.</span><span class="sxs-lookup"><span data-stu-id="64132-210">d.</span></span> <span data-ttu-id="64132-211">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="64132-211">Click **Create**.</span></span>
 
### <a name="create-a-front-test-user"></a><span data-ttu-id="64132-212">Créer un utilisateur de test Front</span><span class="sxs-lookup"><span data-stu-id="64132-212">Create a Front test user</span></span>

<span data-ttu-id="64132-213">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Front.</span><span class="sxs-lookup"><span data-stu-id="64132-213">In this section, you create a user called Britta Simon in Front.</span></span> <span data-ttu-id="64132-214">Travailler avec [équipe de support Client avant](mailto:support@frontapp.com) pour ajouter des utilisateurs de hello de plateforme avant de hello.</span><span class="sxs-lookup"><span data-stu-id="64132-214">Work with [Front Client support team](mailto:support@frontapp.com) to add hello users in hello Front platform.</span></span> <span data-ttu-id="64132-215">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="64132-215">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="64132-216">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="64132-216">Assign hello Azure AD test user</span></span>

<span data-ttu-id="64132-217">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooFront.</span><span class="sxs-lookup"><span data-stu-id="64132-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFront.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="64132-219">**tooassign Britta Simon tooFront, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="64132-219">**tooassign Britta Simon tooFront, perform hello following steps:**</span></span>

1. <span data-ttu-id="64132-220">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="64132-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="64132-222">Dans la liste des applications hello, sélectionnez **avant**.</span><span class="sxs-lookup"><span data-stu-id="64132-222">In hello applications list, select **Front**.</span></span>

    ![lien de début Hello dans la liste des Applications hello](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. <span data-ttu-id="64132-224">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="64132-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="64132-226">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="64132-226">Click **Add** button.</span></span> <span data-ttu-id="64132-227">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="64132-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="64132-229">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="64132-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="64132-230">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="64132-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="64132-231">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="64132-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="64132-232">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="64132-232">Test single sign-on</span></span>

<span data-ttu-id="64132-233">objectif Hello de cette section est tootest votre Azure AD SSOconfiguration à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="64132-233">hello objective of this section is tootest your Azure AD SSOconfiguration using hello Access Panel.</span></span>

<span data-ttu-id="64132-234">Lorsque vous cliquez sur hello avant de vignette dans hello volet d’accès, vous devez obtenir l’application avant de tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="64132-234">When you click hello Front tile in hello Access Panel, you should get automatically signed-on tooyour Front application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="64132-235">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="64132-235">Additional resources</span></span>

* [<span data-ttu-id="64132-236">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="64132-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="64132-237">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="64132-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png

