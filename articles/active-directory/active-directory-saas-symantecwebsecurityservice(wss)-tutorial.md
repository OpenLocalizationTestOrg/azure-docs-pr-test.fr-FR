---
title: "Didacticiel : Intégration d’Azure Active Directory à Symantec Web Security Service (WSS) | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et le Service de sécurité Web Symantec (WSS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: f4575e6f5eb63cd0e1d63edd35e30be3cacc3382
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="340d9-103">Didacticiel : Intégration d’Azure Active Directory à Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="340d9-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="340d9-104">Dans ce didacticiel, vous apprendrez comment toointegrate Symantec Web sécurité Service (WSS) avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="340d9-104">In this tutorial, you learn how toointegrate Symantec Web Security Service (WSS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="340d9-105">Intégration de Service de sécurité Web Symantec (WSS) avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="340d9-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="340d9-106">Vous pouvez contrôler dans Azure AD qui a accès tooSymantec sécurité Service WSS (Web)</span><span class="sxs-lookup"><span data-stu-id="340d9-106">You can control in Azure AD who has access tooSymantec Web Security Service (WSS)</span></span>
- <span data-ttu-id="340d9-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSymantec Web sécurité Service (WSS) (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="340d9-107">You can enable your users tooautomatically get signed-on tooSymantec Web Security Service (WSS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="340d9-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="340d9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="340d9-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="340d9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="340d9-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="340d9-110">Prerequisites</span></span>

<span data-ttu-id="340d9-111">tooconfigure intégration d’Azure AD avec Symantec Security Service WSS (Web), vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="340d9-111">tooconfigure Azure AD integration with Symantec Web Security Service (WSS), you need hello following items:</span></span>

- <span data-ttu-id="340d9-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="340d9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="340d9-113">Un abonnement Symantec Web Security Service (WSS) pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="340d9-113">A Symantec Web Security Service (WSS) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="340d9-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="340d9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="340d9-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="340d9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="340d9-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="340d9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="340d9-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="340d9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="340d9-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="340d9-118">Scenario description</span></span>
<span data-ttu-id="340d9-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="340d9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="340d9-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="340d9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="340d9-121">Ajout de Service de sécurité Web Symantec (WSS) à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="340d9-121">Adding Symantec Web Security Service (WSS) from hello gallery</span></span>
2. <span data-ttu-id="340d9-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="340d9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a><span data-ttu-id="340d9-123">Ajout de Service de sécurité Web Symantec (WSS) à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="340d9-123">Adding Symantec Web Security Service (WSS) from hello gallery</span></span>
<span data-ttu-id="340d9-124">intégration de hello tooconfigure de Symantec Security Service WSS (Web) dans Azure AD, vous devez tooadd Symantec Security Service WSS (Web) à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="340d9-124">tooconfigure hello integration of Symantec Web Security Service (WSS) into Azure AD, you need tooadd Symantec Web Security Service (WSS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="340d9-125">**tooadd Symantec Security Service WSS (Web) à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="340d9-125">**tooadd Symantec Web Security Service (WSS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="340d9-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="340d9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="340d9-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="340d9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="340d9-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="340d9-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="340d9-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="340d9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="340d9-133">Dans la zone de recherche de hello, tapez **Symantec Web sécurité Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="340d9-133">In hello search box, type **Symantec Web Security Service (WSS)**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_search.png)

5. <span data-ttu-id="340d9-135">Dans le volet de résultats hello, sélectionnez **Symantec Web sécurité Service (WSS)**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="340d9-135">In hello results panel, select **Symantec Web Security Service (WSS)**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="340d9-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="340d9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="340d9-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD auprès de Symantec Web Security Service (WSS) avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="340d9-138">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="340d9-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Symantec Web sécurité Service (WSS) est tooa dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="340d9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Symantec Web Security Service (WSS) is tooa user in Azure AD.</span></span> <span data-ttu-id="340d9-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Symantec Security Service WSS (Web) doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="340d9-140">In other words, a link relationship between an Azure AD user and hello related user in Symantec Web Security Service (WSS) needs toobe established.</span></span>

<span data-ttu-id="340d9-141">Dans Symantec Web sécurité Service (WSS), affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="340d9-141">In Symantec Web Security Service (WSS), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="340d9-142">tooconfigure et test Azure AD l’authentification unique avec Symantec Security Service WSS (Web), vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="340d9-142">tooconfigure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="340d9-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="340d9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="340d9-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="340d9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="340d9-145">**[Création d’un utilisateur de test du Service de sécurité Web Symantec (WSS)](#creating-a-symantec-web-security-service-wss-test-user)**  -toohave un équivalent de Britta Simon dans Symantec Security Service WSS (Web) qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="340d9-145">**[Creating a Symantec Web Security Service (WSS) test user](#creating-a-symantec-web-security-service-wss-test-user)** - toohave a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="340d9-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="340d9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="340d9-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="340d9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="340d9-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="340d9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="340d9-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Service de sécurité Web Symantec (WSS).</span><span class="sxs-lookup"><span data-stu-id="340d9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="340d9-150">**tooconfigure Azure AD l’authentification unique avec Symantec Web sécurité Service (WSS), effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="340d9-150">**tooconfigure Azure AD single sign-on with Symantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="340d9-151">Bonjour portail Azure, sur hello **Symantec Web sécurité Service (WSS)** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="340d9-151">In hello Azure portal, on hello **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="340d9-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="340d9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="340d9-155">Sur hello **URL et le domaine de Service (WSS) de sécurité Web Symantec** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="340d9-155">On hello **Symantec Web Security Service (WSS) Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="340d9-157">a.</span><span class="sxs-lookup"><span data-stu-id="340d9-157">a.</span></span> <span data-ttu-id="340d9-158">Bonjour **URL de connexion** zone de texte, url mention hello, que vous souhaitez tooblock selon la stratégie de blocage toohello Hello Symantec Security Service WSS (Web).</span><span class="sxs-lookup"><span data-stu-id="340d9-158">In hello **Sign-on URL** textbox, mention hello url, which you want tooblock according toohello blocking policy of hello Symantec Web Security Service (WSS).</span></span>  
    
    <span data-ttu-id="340d9-159">b.</span><span class="sxs-lookup"><span data-stu-id="340d9-159">b.</span></span> <span data-ttu-id="340d9-160">Bonjour **identificateur** zone de texte, tapez l’URL hello :`https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="340d9-160">In hello **Identifier** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="340d9-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="340d9-161">These values are not real.</span></span> <span data-ttu-id="340d9-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="340d9-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="340d9-163">Contact [équipe de support Client de Service de sécurité Web Symantec (WSS)](https://www.symantec.com/contact-us) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="340d9-163">Contact [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) tooget these values.</span></span> 

4. <span data-ttu-id="340d9-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="340d9-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="340d9-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="340d9-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="340d9-168">tooconfigure l’authentification unique sur **Symantec Web sécurité Service (WSS)** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipedesupportdeSymantecSecurityServiceWSS(Web)](https://www.symantec.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="340d9-168">tooconfigure single sign-on on **Symantec Web Security Service (WSS)** side, you need toosend hello downloaded **Metadata XML** too[Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="340d9-169">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="340d9-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="340d9-170">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="340d9-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="340d9-171">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="340d9-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="340d9-172">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="340d9-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="340d9-173">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="340d9-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="340d9-175">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="340d9-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="340d9-176">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="340d9-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="340d9-178">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="340d9-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="340d9-180">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="340d9-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="340d9-182">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="340d9-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="340d9-184">a.</span><span class="sxs-lookup"><span data-stu-id="340d9-184">a.</span></span> <span data-ttu-id="340d9-185">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="340d9-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="340d9-186">b.</span><span class="sxs-lookup"><span data-stu-id="340d9-186">b.</span></span> <span data-ttu-id="340d9-187">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="340d9-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="340d9-188">c.</span><span class="sxs-lookup"><span data-stu-id="340d9-188">c.</span></span> <span data-ttu-id="340d9-189">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="340d9-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="340d9-190">d.</span><span class="sxs-lookup"><span data-stu-id="340d9-190">d.</span></span> <span data-ttu-id="340d9-191">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="340d9-191">Click **Create**.</span></span>
 
### <a name="creating-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="340d9-192">Création d’un utilisateur de test Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="340d9-192">Creating a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="340d9-193">Dans cette section, vous créez un utilisateur appelé Britta Simon dans Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="340d9-193">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="340d9-194">Travailler avec [équipe de support du Service de sécurité Web Symantec (WSS)](https://www.symantec.com/contact-us) pour ajouter des utilisateurs de hello de plateforme de Service de sécurité Web Symantec (WSS) hello.</span><span class="sxs-lookup"><span data-stu-id="340d9-194">Work with [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) to add hello users in hello Symantec Web Security Service (WSS) platform.</span></span> <span data-ttu-id="340d9-195">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="340d9-195">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="340d9-196">En même temps que hello utilisateur détaille également vous devez toosend hello adresse IP publique de l’ordinateur hello à partir de laquelle vous essayez d’application de tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="340d9-196">Also along with hello user details you need toosend hello public IPaddress of hello machine from which you are trying tooaccess hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="340d9-197">Veuillez [cliquez ici](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget votre machine de publique IPaddress.</span><span class="sxs-lookup"><span data-stu-id="340d9-197">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget your machine's public IPaddress.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="340d9-198">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="340d9-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="340d9-199">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSymantec sécurité Service WSS (Web).</span><span class="sxs-lookup"><span data-stu-id="340d9-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSymantec Web Security Service (WSS).</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="340d9-201">**tooassign Britta Simon tooSymantec Web sécurité Service (WSS), effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="340d9-201">**tooassign Britta Simon tooSymantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="340d9-202">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="340d9-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="340d9-204">Dans la liste des applications hello, sélectionnez **Symantec Web sécurité Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="340d9-204">In hello applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_app.png) 

3. <span data-ttu-id="340d9-206">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="340d9-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="340d9-208">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="340d9-208">Click **Add** button.</span></span> <span data-ttu-id="340d9-209">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="340d9-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="340d9-211">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="340d9-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="340d9-212">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="340d9-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="340d9-213">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="340d9-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="340d9-214">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="340d9-214">Testing single sign-on</span></span>

<span data-ttu-id="340d9-215">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="340d9-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="340d9-216">Lorsque vous cliquez sur hello Symantec Web sécurité Service (WSS) vignette Bonjour volet d’accès, vous obtenez redirigé toohello blocage de page pour laquelle hello stratégie de blocage a été configuré.</span><span class="sxs-lookup"><span data-stu-id="340d9-216">When you click hello Symantec Web Security Service (WSS) tile in hello Access Panel, you get redirected toohello blocking page for which hello blocking policy has been configured.</span></span>
<span data-ttu-id="340d9-217">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="340d9-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="340d9-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="340d9-218">Additional resources</span></span>

* [<span data-ttu-id="340d9-219">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="340d9-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="340d9-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="340d9-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_203.png

