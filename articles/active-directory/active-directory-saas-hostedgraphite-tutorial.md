---
title: "Didacticiel : Intégration d’Azure Active Directory à Hosted Graphite | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Graphite de hébergé."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a1ac4d7f-d079-4f3c-b6da-0f520d427ceb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: d8914f6417ba8fbdef1a48e1b36635200ba130d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hosted-graphite"></a><span data-ttu-id="13579-103">Didacticiel : Intégration d’Azure Active Directory à Hosted Graphite</span><span class="sxs-lookup"><span data-stu-id="13579-103">Tutorial: Azure Active Directory integration with Hosted Graphite</span></span>

<span data-ttu-id="13579-104">Dans ce didacticiel, vous apprendrez comment toointegrate Graphite hébergé avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="13579-104">In this tutorial, you learn how toointegrate Hosted Graphite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="13579-105">Intégration hébergée de Graphite à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="13579-105">Integrating Hosted Graphite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="13579-106">Vous pouvez contrôler dans Azure AD qui a accès tooHosted Graphite</span><span class="sxs-lookup"><span data-stu-id="13579-106">You can control in Azure AD who has access tooHosted Graphite</span></span>
- <span data-ttu-id="13579-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooHosted Graphite (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="13579-107">You can enable your users tooautomatically get signed-on tooHosted Graphite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="13579-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="13579-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="13579-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="13579-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13579-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="13579-110">Prerequisites</span></span>

<span data-ttu-id="13579-111">tooconfigure intégration d’Azure AD avec Graphite de hébergé, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="13579-111">tooconfigure Azure AD integration with Hosted Graphite, you need hello following items:</span></span>

- <span data-ttu-id="13579-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="13579-112">An Azure AD subscription</span></span>
- <span data-ttu-id="13579-113">Un abonnement Hosted Graphite pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="13579-113">A Hosted Graphite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="13579-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="13579-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="13579-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="13579-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="13579-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="13579-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="13579-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="13579-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="13579-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="13579-118">Scenario description</span></span>
<span data-ttu-id="13579-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="13579-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="13579-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="13579-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="13579-121">Ajout Graphite hébergé à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="13579-121">Adding Hosted Graphite from hello gallery</span></span>
2. <span data-ttu-id="13579-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="13579-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hosted-graphite-from-hello-gallery"></a><span data-ttu-id="13579-123">Ajout Graphite hébergé à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="13579-123">Adding Hosted Graphite from hello gallery</span></span>
<span data-ttu-id="13579-124">tooconfigure hello intégration de Graphite de hébergé dans Azure AD, vous devez tooadd Graphite hébergé à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="13579-124">tooconfigure hello integration of Hosted Graphite into Azure AD, you need tooadd Hosted Graphite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="13579-125">**tooadd Graphite hébergé à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="13579-125">**tooadd Hosted Graphite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="13579-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="13579-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="13579-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="13579-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="13579-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="13579-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="13579-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="13579-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="13579-133">Dans la zone de recherche de hello, tapez **hébergé de Graphite**.</span><span class="sxs-lookup"><span data-stu-id="13579-133">In hello search box, type **Hosted Graphite**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_search.png)

5. <span data-ttu-id="13579-135">Dans le volet de résultats hello, sélectionnez **hébergé de Graphite**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="13579-135">In hello results panel, select **Hosted Graphite**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="13579-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="13579-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="13579-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Hosted Graphite avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="13579-138">In this section, you configure and test Azure AD single sign-on with Hosted Graphite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="13579-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello Graphite de hébergé est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13579-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Hosted Graphite is tooa user in Azure AD.</span></span> <span data-ttu-id="13579-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans hébergé de Graphite doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="13579-140">In other words, a link relationship between an Azure AD user and hello related user in Hosted Graphite needs toobe established.</span></span>

<span data-ttu-id="13579-141">Dans Graphite hébergé, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="13579-141">In Hosted Graphite, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="13579-142">tooconfigure et test Azure AD l’authentification unique avec Graphite de hébergé, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="13579-142">tooconfigure and test Azure AD single sign-on with Hosted Graphite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="13579-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="13579-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="13579-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="13579-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="13579-145">**[Création d’un utilisateur de test hébergé de Graphite](#creating-a-hosted-graphite-test-user)**  -toohave un équivalent de Britta Simon dans Graphite hébergé qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="13579-145">**[Creating a Hosted Graphite test user](#creating-a-hosted-graphite-test-user)** - toohave a counterpart of Britta Simon in Hosted Graphite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="13579-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="13579-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="13579-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="13579-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="13579-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="13579-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="13579-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application hébergée de Graphite.</span><span class="sxs-lookup"><span data-stu-id="13579-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Hosted Graphite application.</span></span>

<span data-ttu-id="13579-150">**tooconfigure Azure AD single sign-on avec Graphite hébergé, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="13579-150">**tooconfigure Azure AD single sign-on with Hosted Graphite, perform hello following steps:**</span></span>

1. <span data-ttu-id="13579-151">Bonjour portail Azure, sur hello **hébergé de Graphite** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="13579-151">In hello Azure portal, on hello **Hosted Graphite** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="13579-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="13579-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_samlbase.png)

3. <span data-ttu-id="13579-155">Sur hello **URL et le domaine de Graphite hébergé** section, si vous le souhaitez application hello tooconfigure **mode initialisée par IDP**, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="13579-155">On hello **Hosted Graphite Domain and URLs** section, if you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_url.png)

    <span data-ttu-id="13579-157">a.</span><span class="sxs-lookup"><span data-stu-id="13579-157">a.</span></span> <span data-ttu-id="13579-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://www.hostedgraphite.com/metadata/<user id>`</span><span class="sxs-lookup"><span data-stu-id="13579-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.hostedgraphite.com/metadata/<user id>`</span></span>

    <span data-ttu-id="13579-159">b.</span><span class="sxs-lookup"><span data-stu-id="13579-159">b.</span></span> <span data-ttu-id="13579-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://www.hostedgraphite.com/complete/saml/<user id>`</span><span class="sxs-lookup"><span data-stu-id="13579-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.hostedgraphite.com/complete/saml/<user id>`</span></span>

4. <span data-ttu-id="13579-161">Sur hello **URL et domaine hébergé de Graphite** section, si vous le souhaitez application hello tooconfigure **mode initiée par SP**, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="13579-161">On hello **Hosted Graphite Domain and URLs** section, if you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_10.png)
  
    <span data-ttu-id="13579-163">a.</span><span class="sxs-lookup"><span data-stu-id="13579-163">a.</span></span> <span data-ttu-id="13579-164">Cliquez sur hello **afficher les paramètres d’URL avancés** option</span><span class="sxs-lookup"><span data-stu-id="13579-164">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="13579-165">b.</span><span class="sxs-lookup"><span data-stu-id="13579-165">b.</span></span> <span data-ttu-id="13579-166">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://www.hostedgraphite.com/login/saml/<user id>/`</span><span class="sxs-lookup"><span data-stu-id="13579-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://www.hostedgraphite.com/login/saml/<user id>/`</span></span>   

    > [!NOTE] 
    > <span data-ttu-id="13579-167">Notez qu’il s’agit pas des valeurs réelles hello.</span><span class="sxs-lookup"><span data-stu-id="13579-167">Please note that these are not hello real values.</span></span> <span data-ttu-id="13579-168">Vous avez défini ces valeurs avec hello tooupdate réel identificateur, les URL de réponse et les URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="13579-168">You have tooupdate these values with hello actual Identifier, Reply URL and Sign On URL.</span></span> <span data-ttu-id="13579-169">tooget ces valeurs, vous pouvez accéder tooAccess -> configuration de SAML sur votre côté Application ou d’un Contact [équipe de support hébergé de Graphite](mailto:help@hostedgraphite.com).</span><span class="sxs-lookup"><span data-stu-id="13579-169">tooget these values, you can go tooAccess->SAML setup on your Application side or Contact [Hosted Graphite support team](mailto:help@hostedgraphite.com).</span></span>
    >
 
5. <span data-ttu-id="13579-170">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="13579-170">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_certificate.png) 

6. <span data-ttu-id="13579-172">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="13579-172">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="13579-174">Sur hello **hébergé la Configuration de Graphite** , cliquez sur **configurer le Graphite hébergé** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="13579-174">On hello **Hosted Graphite Configuration** section, click **Configure Hosted Graphite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="13579-175">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="13579-175">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_configure.png) 

8. <span data-ttu-id="13579-177">Authentification tooyour client de Graphite de hébergé en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="13579-177">Sign-on tooyour Hosted Graphite tenant as an administrator.</span></span>

9. <span data-ttu-id="13579-178">Accédez toohello **page de configuration de SAML** dans le volet hello (**accès -> configuration de SAML**).</span><span class="sxs-lookup"><span data-stu-id="13579-178">Go toohello **SAML Setup page** in hello sidebar (**Access -> SAML Setup**).</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_000.png)

10. <span data-ttu-id="13579-180">Confirmez ces URL correspondant à votre configuration effectuée sur hello **URL et domaine hébergé de Graphite** section Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="13579-180">Confirm these URls match your configuration done on hello **Hosted Graphite Domain and URLs** section of hello Azure portal.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_001.png)

11. <span data-ttu-id="13579-182">Dans **entité ou l’ID de l’émetteur** et **URL de connexion SSO** zones de texte, collez la valeur hello **ID d’entité SAML** et **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="13579-182">In  **Entity or Issuer ID** and **SSO Login URL** textboxes, paste hello value of **SAML Entity ID** and **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_002.png)
   

12. <span data-ttu-id="13579-184">Sélectionnez « **Lecture seule** » comme **Rôle d’utilisateur par défaut**.</span><span class="sxs-lookup"><span data-stu-id="13579-184">Select "**Read-only**" as **Default User Role**.</span></span>
    
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_004.png)

13. <span data-ttu-id="13579-186">Ouvrez votre certificat codé en base 64 dans le bloc-notes téléchargé à partir du portail Azure, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat X.509** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="13579-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
    
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_005.png)

14. <span data-ttu-id="13579-188">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="13579-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="13579-189">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="13579-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="13579-190">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="13579-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="13579-191">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="13579-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="13579-192">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="13579-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="13579-193">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="13579-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="13579-195">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="13579-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="13579-196">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="13579-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="13579-198">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="13579-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="13579-200">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="13579-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="13579-202">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="13579-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="13579-204">a.</span><span class="sxs-lookup"><span data-stu-id="13579-204">a.</span></span> <span data-ttu-id="13579-205">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="13579-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="13579-206">b.</span><span class="sxs-lookup"><span data-stu-id="13579-206">b.</span></span> <span data-ttu-id="13579-207">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="13579-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="13579-208">c.</span><span class="sxs-lookup"><span data-stu-id="13579-208">c.</span></span> <span data-ttu-id="13579-209">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="13579-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="13579-210">d.</span><span class="sxs-lookup"><span data-stu-id="13579-210">d.</span></span> <span data-ttu-id="13579-211">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="13579-211">Click **Create**.</span></span>
 
### <a name="creating-a-hosted-graphite-test-user"></a><span data-ttu-id="13579-212">Création d’un utilisateur de test Hosted Graphite</span><span class="sxs-lookup"><span data-stu-id="13579-212">Creating a Hosted Graphite test user</span></span>

<span data-ttu-id="13579-213">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Graphite de hébergé.</span><span class="sxs-lookup"><span data-stu-id="13579-213">hello objective of this section is toocreate a user called Britta Simon in Hosted Graphite.</span></span> <span data-ttu-id="13579-214">Hosted Graphite prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="13579-214">Hosted Graphite supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="13579-215">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="13579-215">There is no action item for you in this section.</span></span> <span data-ttu-id="13579-216">Un nouvel utilisateur s’affichera pendant une tentative de tooaccess Hosted Graphite s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="13579-216">A new user will be created during an attempt tooaccess Hosted Graphite if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="13579-217">Si vous devez manuellement toocreate un utilisateur, vous avez besoin d’équipe de support toocontact hello Graphite de hébergé via < mailto:help@hostedgraphite.com >.</span><span class="sxs-lookup"><span data-stu-id="13579-217">If you need toocreate a user manually, you need toocontact hello Hosted Graphite support team via <mailto:help@hostedgraphite.com>.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="13579-218">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="13579-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="13579-219">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooHosted Graphite.</span><span class="sxs-lookup"><span data-stu-id="13579-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHosted Graphite.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="13579-221">**tooassign Britta Simon tooHosted Graphite, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="13579-221">**tooassign Britta Simon tooHosted Graphite, perform hello following steps:**</span></span>

1. <span data-ttu-id="13579-222">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="13579-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="13579-224">Dans la liste des applications hello, sélectionnez **hébergé de Graphite**.</span><span class="sxs-lookup"><span data-stu-id="13579-224">In hello applications list, select **Hosted Graphite**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_app.png) 

3. <span data-ttu-id="13579-226">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="13579-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="13579-228">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="13579-228">Click **Add** button.</span></span> <span data-ttu-id="13579-229">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="13579-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="13579-231">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="13579-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="13579-232">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="13579-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="13579-233">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="13579-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="13579-234">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="13579-234">Testing single sign-on</span></span>

<span data-ttu-id="13579-235">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="13579-235">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="13579-236">Lorsque vous cliquez sur mosaïque hébergé de Graphite hello hello volet d’accès, vous devez obtenir l’application hébergée de Graphite d’automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="13579-236">When you click hello Hosted Graphite tile in hello Access Panel, you should get automatically signed-on tooyour Hosted Graphite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="13579-237">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="13579-237">Additional resources</span></span>

* [<span data-ttu-id="13579-238">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="13579-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="13579-239">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="13579-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_203.png

