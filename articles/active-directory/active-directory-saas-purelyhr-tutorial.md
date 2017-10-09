---
title: "Didacticiel : Intégration d’Azure Active Directory avec PurelyHR | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et PurelyHR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 86a9c454-596d-4902-829a-fe126708f739
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: bdc1748ed650cff36b1ef7d7330dd2a17b3bc760
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-purelyhr"></a><span data-ttu-id="bf704-103">Didacticiel : Intégration d’Azure Active Directory avec PurelyHR</span><span class="sxs-lookup"><span data-stu-id="bf704-103">Tutorial: Azure Active Directory integration with PurelyHR</span></span>

<span data-ttu-id="bf704-104">Dans ce didacticiel, vous apprendrez comment toointegrate PurelyHR avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bf704-104">In this tutorial, you learn how toointegrate PurelyHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bf704-105">Intégration PurelyHR à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="bf704-105">Integrating PurelyHR with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bf704-106">Vous pouvez contrôler dans Azure AD qui a accès tooPurelyHR</span><span class="sxs-lookup"><span data-stu-id="bf704-106">You can control in Azure AD who has access tooPurelyHR</span></span>
- <span data-ttu-id="bf704-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooPurelyHR (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf704-107">You can enable your users tooautomatically get signed-on tooPurelyHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bf704-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="bf704-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bf704-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bf704-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf704-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bf704-110">Prerequisites</span></span>

<span data-ttu-id="bf704-111">tooconfigure intégration d’Azure AD avec PurelyHR, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="bf704-111">tooconfigure Azure AD integration with PurelyHR, you need hello following items:</span></span>

- <span data-ttu-id="bf704-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf704-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bf704-113">Un abonnement PurelyHR pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="bf704-113">A PurelyHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bf704-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="bf704-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bf704-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="bf704-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bf704-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="bf704-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bf704-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bf704-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bf704-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="bf704-118">Scenario description</span></span>
<span data-ttu-id="bf704-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="bf704-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bf704-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="bf704-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bf704-121">Ajout de PurelyHR à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="bf704-121">Adding PurelyHR from hello gallery</span></span>
2. <span data-ttu-id="bf704-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf704-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-purelyhr-from-hello-gallery"></a><span data-ttu-id="bf704-123">Ajout de PurelyHR à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="bf704-123">Adding PurelyHR from hello gallery</span></span>
<span data-ttu-id="bf704-124">intégration de hello tooconfigure de PurelyHR dans Azure AD, vous devez tooadd PurelyHR à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="bf704-124">tooconfigure hello integration of PurelyHR into Azure AD, you need tooadd PurelyHR from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bf704-125">**tooadd PurelyHR à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bf704-125">**tooadd PurelyHR from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf704-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="bf704-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bf704-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="bf704-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bf704-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bf704-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="bf704-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="bf704-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="bf704-133">Dans la zone de recherche de hello, tapez **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="bf704-133">In hello search box, type **PurelyHR**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_search.png)

5. <span data-ttu-id="bf704-135">Dans le volet de résultats hello, sélectionnez **PurelyHR**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="bf704-135">In hello results panel, select **PurelyHR**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bf704-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf704-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bf704-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec PurelyHR, par le biais d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="bf704-138">In this section, you configure and test Azure AD single sign-on with PurelyHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bf704-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans PurelyHR est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf704-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PurelyHR is tooa user in Azure AD.</span></span> <span data-ttu-id="bf704-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans PurelyHR doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="bf704-140">In other words, a link relationship between an Azure AD user and hello related user in PurelyHR needs toobe established.</span></span>

<span data-ttu-id="bf704-141">Dans PurelyHR, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="bf704-141">In PurelyHR, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bf704-142">tooconfigure et test Azure AD l’authentification unique avec PurelyHR, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="bf704-142">tooconfigure and test Azure AD single sign-on with PurelyHR, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bf704-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="bf704-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bf704-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bf704-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bf704-145">**[Création d’un utilisateur de test PurelyHR](#creating-a-purelyhr-test-user)**  -toohave un équivalent de Britta Simon dans PurelyHR est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bf704-145">**[Creating a PurelyHR test user](#creating-a-purelyhr-test-user)** - toohave a counterpart of Britta Simon in PurelyHR that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bf704-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="bf704-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bf704-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="bf704-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bf704-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf704-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bf704-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="bf704-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PurelyHR application.</span></span>

<span data-ttu-id="bf704-150">**tooconfigure Azure AD single sign-on avec PurelyHR, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bf704-150">**tooconfigure Azure AD single sign-on with PurelyHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf704-151">Bonjour portail Azure, sur hello **PurelyHR** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="bf704-151">In hello Azure portal, on hello **PurelyHR** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="bf704-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="bf704-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_samlbase.png)

3. <span data-ttu-id="bf704-155">Sur hello **PurelyHR domaine et les URL** section, effectuer hello comme suit si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="bf704-155">On hello **PurelyHR Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url.png)
   
    <span data-ttu-id="bf704-157">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyID>.purelyhr.com/sso-consume`</span><span class="sxs-lookup"><span data-stu-id="bf704-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyID>.purelyhr.com/sso-consume`</span></span>

4. <span data-ttu-id="bf704-158">Vérifiez **afficher les paramètres d’URL avancés**, si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="bf704-158">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url1.png)
    
    <span data-ttu-id="bf704-160">Bonjour **URL de connexion** zone de texte, valeur hello de type hello suivant le modèle à l’aide de :`https://<companyID>.purelyhr.com/sso-initiate`</span><span class="sxs-lookup"><span data-stu-id="bf704-160">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<companyID>.purelyhr.com/sso-initiate`</span></span>
     
    > [!NOTE]
    > <span data-ttu-id="bf704-161">Ces valeurs ne sont pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="bf704-161">These values are not hello real.</span></span> <span data-ttu-id="bf704-162">Mettre à jour ces valeurs avec l’URL de réponse réelle hello et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="bf704-162">Update these values with hello actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="bf704-163">Contact [équipe de support Client de PurelyHR](http://support.purelyhr.com/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="bf704-163">Contact [PurelyHR Client support team](http://support.purelyhr.com/) tooget these values.</span></span> 

5. <span data-ttu-id="bf704-164">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="bf704-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_certificate.png) 

6. <span data-ttu-id="bf704-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="bf704-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-purelyhr-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="bf704-168">Sur hello **PurelyHR Configuration** , cliquez sur **PurelyHR de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="bf704-168">On hello **PurelyHR Configuration** section, click **Configure PurelyHR** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bf704-169">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="bf704-169">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_configure.png) 

8. <span data-ttu-id="bf704-171">tooconfigure l’authentification unique sur **PurelyHR** côté, le site Web de tootheir de connexion en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="bf704-171">tooconfigure single sign-on on **PurelyHR** side, login tootheir website as an administrator.</span></span>

9. <span data-ttu-id="bf704-172">Ouvrez hello **tableau de bord** dans la barre d’outils hello et cliquez sur une des options hello **paramètres d’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="bf704-172">Open hello **Dashboard** from hello options in hello toolbar and click **SSO Settings**.</span></span>

10. <span data-ttu-id="bf704-173">Hello coller des valeurs dans les zones hello comme décrit ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="bf704-173">Paste hello values in hello boxes as described below-</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-purelyhr-tutorial/purelyhr-dashboard-sso-settings.png)    

    <span data-ttu-id="bf704-175">a.</span><span class="sxs-lookup"><span data-stu-id="bf704-175">a.</span></span> <span data-ttu-id="bf704-176">Ouvrez hello **Certificate(Bas64)** hello provient de portail Azure dans le bloc-notes, puis copiez valeur de certificat hello.</span><span class="sxs-lookup"><span data-stu-id="bf704-176">Open hello **Certificate(Bas64)** downloaded from hello Azure portal in notepad and copy hello certificate value.</span></span> <span data-ttu-id="bf704-177">Hello de coller copiées valeur hello **certificat X.509** boîte.</span><span class="sxs-lookup"><span data-stu-id="bf704-177">Paste hello copied value into hello **X.509 Certificate** box.</span></span>

    <span data-ttu-id="bf704-178">b.</span><span class="sxs-lookup"><span data-stu-id="bf704-178">b.</span></span> <span data-ttu-id="bf704-179">Bonjour **URL de l’émetteur Idp** zone, collez hello **ID d’entité SAML** copiés à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bf704-179">In hello **Idp Issuer URL** box, paste hello **SAML Entity ID** copied from hello Azure portal.</span></span>

    <span data-ttu-id="bf704-180">c.</span><span class="sxs-lookup"><span data-stu-id="bf704-180">c.</span></span> <span data-ttu-id="bf704-181">Bonjour **URL de point de terminaison Idp** zone, collez hello **SAML Sign-On URL du Service unique** copiés à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bf704-181">In hello **Idp Endpoint URL** box, paste hello **SAML Single Sign-On Service URL** copied from hello Azure portal.</span></span> 

    <span data-ttu-id="bf704-182">d.</span><span class="sxs-lookup"><span data-stu-id="bf704-182">d.</span></span> <span data-ttu-id="bf704-183">Vérifiez hello **créer automatiquement des utilisateurs** case à cocher tooenable le provisionnement utilisateur automatique dans PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="bf704-183">Check hello **Auto-Create Users** checkbox tooenable automatic user provisioning in PurelyHR.</span></span>

    <span data-ttu-id="bf704-184">e.</span><span class="sxs-lookup"><span data-stu-id="bf704-184">e.</span></span> <span data-ttu-id="bf704-185">Cliquez sur **enregistrer les modifications** toosave les paramètres hello.</span><span class="sxs-lookup"><span data-stu-id="bf704-185">Click **Save Changes** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="bf704-186">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="bf704-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bf704-187">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="bf704-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bf704-188">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bf704-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bf704-189">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf704-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="bf704-190">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="bf704-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="bf704-192">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bf704-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf704-193">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="bf704-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bf704-195">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="bf704-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bf704-197">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="bf704-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bf704-199">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bf704-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bf704-201">a.</span><span class="sxs-lookup"><span data-stu-id="bf704-201">a.</span></span> <span data-ttu-id="bf704-202">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bf704-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bf704-203">b.</span><span class="sxs-lookup"><span data-stu-id="bf704-203">b.</span></span> <span data-ttu-id="bf704-204">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bf704-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bf704-205">c.</span><span class="sxs-lookup"><span data-stu-id="bf704-205">c.</span></span> <span data-ttu-id="bf704-206">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="bf704-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bf704-207">d.</span><span class="sxs-lookup"><span data-stu-id="bf704-207">d.</span></span> <span data-ttu-id="bf704-208">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="bf704-208">Click **Create**.</span></span>
 
### <a name="creating-a-purelyhr-test-user"></a><span data-ttu-id="bf704-209">Création d’un utilisateur de test PurelyHR</span><span class="sxs-lookup"><span data-stu-id="bf704-209">Creating a PurelyHR test user</span></span>

<span data-ttu-id="bf704-210">tooenable Azure AD les utilisateurs toolog dans tooPurelyHR, vous devez les configurer dans PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="bf704-210">tooenable Azure AD users toolog in tooPurelyHR, they must be provisioned into PurelyHR.</span></span> <span data-ttu-id="bf704-211">Dans PurelyHR, l’approvisionnement est une tâche automatique. Aucune opération manuelle n’est nécessaire lorsque l’approvisionnement automatique de l’utilisateur est activé.</span><span class="sxs-lookup"><span data-stu-id="bf704-211">In PurelyHR, provisioning is an automatic task and no manual steps are required when automatic user provisioning is enabled.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bf704-212">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf704-212">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bf704-213">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooPurelyHR.</span><span class="sxs-lookup"><span data-stu-id="bf704-213">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPurelyHR.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="bf704-215">**tooassign Britta Simon tooPurelyHR, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bf704-215">**tooassign Britta Simon tooPurelyHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf704-216">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bf704-216">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="bf704-218">Dans la liste des applications hello, sélectionnez **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="bf704-218">In hello applications list, select **PurelyHR**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_app.png) 

3. <span data-ttu-id="bf704-220">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="bf704-220">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="bf704-222">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bf704-222">Click **Add** button.</span></span> <span data-ttu-id="bf704-223">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="bf704-223">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="bf704-225">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="bf704-225">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bf704-226">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="bf704-226">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bf704-227">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="bf704-227">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bf704-228">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="bf704-228">Testing single sign-on</span></span>

<span data-ttu-id="bf704-229">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="bf704-229">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bf704-230">Cliquez sur hello absorber les LMS vignette Bonjour volet d’accès, vous obtenez automatiquement signé sur tooyour absorber les LMS application.</span><span class="sxs-lookup"><span data-stu-id="bf704-230">Click hello Absorb LMS tile in hello Access Panel, you get automatically signed-on tooyour Absorb LMS application.</span></span>

<span data-ttu-id="bf704-231">Pour plus d’informations sur hello volet d’accès, consultez.</span><span class="sxs-lookup"><span data-stu-id="bf704-231">For more information about hello Access Panel, see.</span></span> <span data-ttu-id="bf704-232">[Introduction toohello volet d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="bf704-232">[Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bf704-233">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="bf704-233">Additional resources</span></span>

* [<span data-ttu-id="bf704-234">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bf704-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bf704-235">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="bf704-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_203.png

