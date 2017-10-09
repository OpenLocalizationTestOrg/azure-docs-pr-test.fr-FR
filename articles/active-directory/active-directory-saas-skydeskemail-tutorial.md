---
title: "Didacticiel : intégration d’Azure Active Directory à SkyDesk Email | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et par courrier électronique SkyDesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9d0bbcb-ddb5-473f-a4aa-028ae88ced1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 19c670a60f581a2be55b74eacdb5393a36e38be3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skydesk-email"></a><span data-ttu-id="24596-103">Didacticiel : Intégration d’Azure Active Directory à SkyDesk Email</span><span class="sxs-lookup"><span data-stu-id="24596-103">Tutorial: Azure Active Directory integration with SkyDesk Email</span></span>

<span data-ttu-id="24596-104">Dans ce didacticiel, vous apprendrez comment envoyer par courrier électronique SkyDesk toointegrate avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="24596-104">In this tutorial, you learn how toointegrate SkyDesk Email with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="24596-105">Intégration SkyDesk E-mail à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="24596-105">Integrating SkyDesk Email with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="24596-106">Vous pouvez contrôler dans Azure AD qui a accès tooSkyDesk par courrier électronique</span><span class="sxs-lookup"><span data-stu-id="24596-106">You can control in Azure AD who has access tooSkyDesk Email</span></span>
- <span data-ttu-id="24596-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSkyDesk par courrier électronique (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="24596-107">You can enable your users tooautomatically get signed-on tooSkyDesk Email (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="24596-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="24596-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="24596-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="24596-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24596-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="24596-110">Prerequisites</span></span>

<span data-ttu-id="24596-111">tooconfigure intégration d’Azure AD avec SkyDesk adresse de messagerie, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="24596-111">tooconfigure Azure AD integration with SkyDesk Email, you need hello following items:</span></span>

- <span data-ttu-id="24596-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="24596-112">An Azure AD subscription</span></span>
- <span data-ttu-id="24596-113">Un abonnement SkyDesk Email pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="24596-113">A SkyDesk Email single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="24596-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="24596-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="24596-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="24596-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="24596-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="24596-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="24596-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici [Offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="24596-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="24596-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="24596-118">Scenario description</span></span>
<span data-ttu-id="24596-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="24596-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="24596-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="24596-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="24596-121">Ajout de SkyDesk messagerie à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="24596-121">Adding SkyDesk Email from hello gallery</span></span>
2. <span data-ttu-id="24596-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="24596-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skydesk-email-from-hello-gallery"></a><span data-ttu-id="24596-123">Ajout de SkyDesk messagerie à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="24596-123">Adding SkyDesk Email from hello gallery</span></span>
<span data-ttu-id="24596-124">tooconfigure hello intégration des messages électroniques de SkyDesk dans Azure AD, vous devez tooadd SkyDesk messagerie à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="24596-124">tooconfigure hello integration of SkyDesk Email into Azure AD, you need tooadd SkyDesk Email from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="24596-125">**tooadd messagerie SkyDesk à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="24596-125">**tooadd SkyDesk Email from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="24596-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="24596-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="24596-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="24596-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="24596-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="24596-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="24596-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="24596-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="24596-133">Dans la zone de recherche de hello, tapez **SkyDesk E-mail**.</span><span class="sxs-lookup"><span data-stu-id="24596-133">In hello search box, type **SkyDesk Email**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_search.png)

5. <span data-ttu-id="24596-135">Dans le volet de résultats hello, sélectionnez **SkyDesk messagerie**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="24596-135">In hello results panel, select **SkyDesk Email**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="24596-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="24596-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="24596-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD auprès de SkyDesk Email, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="24596-138">In this section, you configure and test Azure AD single sign-on with SkyDesk Email based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="24596-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello par courrier électronique SkyDesk est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24596-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SkyDesk Email is tooa user in Azure AD.</span></span> <span data-ttu-id="24596-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur par courrier électronique SkyDesk hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="24596-140">In other words, a link relationship between an Azure AD user and hello related user in SkyDesk Email needs toobe established.</span></span>

<span data-ttu-id="24596-141">Courrier électronique SkyDesk, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="24596-141">In SkyDesk Email, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="24596-142">tooconfigure et test Azure AD l’authentification unique avec SkyDesk adresse de messagerie, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="24596-142">tooconfigure and test Azure AD single sign-on with SkyDesk Email, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="24596-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="24596-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="24596-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="24596-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="24596-145">**[Création d’un utilisateur de test par courrier électronique SkyDesk](#creating-a-skydesk-email-test-user)**  -toohave un équivalent de Britta Simon par courrier électronique SkyDesk qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="24596-145">**[Creating a SkyDesk Email test user](#creating-a-skydesk-email-test-user)** - toohave a counterpart of Britta Simon in SkyDesk Email that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="24596-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="24596-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="24596-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="24596-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="24596-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="24596-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="24596-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de messagerie de SkyDesk.</span><span class="sxs-lookup"><span data-stu-id="24596-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SkyDesk Email application.</span></span>

<span data-ttu-id="24596-150">**tooconfigure Azure AD authentification unique avec les E-mails SkyDesk effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="24596-150">**tooconfigure Azure AD single sign-on with SkyDesk Email, perform hello following steps:**</span></span>

1. <span data-ttu-id="24596-151">Bonjour portail Azure, sur hello **SkyDesk messagerie** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="24596-151">In hello Azure portal, on hello **SkyDesk Email** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="24596-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="24596-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_samlbase.png)

3. <span data-ttu-id="24596-155">Sur hello **URL et le domaine de messagerie SkyDesk** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="24596-155">On hello **SkyDesk Email Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_url.png)

    <span data-ttu-id="24596-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://mail.skydesk.jp/portal/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="24596-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://mail.skydesk.jp/portal/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="24596-158">valeur de Hello n’est pas réelle.</span><span class="sxs-lookup"><span data-stu-id="24596-158">hello value is not real.</span></span> <span data-ttu-id="24596-159">Valeur de hello de mise à jour avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="24596-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="24596-160">Contact [équipe de support Client de messagerie SkyDesk](https://www.skydesk.sg/support/) valeur hello de tooget.</span><span class="sxs-lookup"><span data-stu-id="24596-160">Contact [SkyDesk Email Client support team](https://www.skydesk.sg/support/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="24596-161">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="24596-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_certificate.png) 

5. <span data-ttu-id="24596-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="24596-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="24596-165">Sur hello **Configuration des E-mails SkyDesk** , cliquez sur **configurer la messagerie de SkyDesk** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="24596-165">On hello **SkyDesk Email Configuration** section, click **Configure SkyDesk Email** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="24596-166">Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="24596-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_configure.png) 

7. <span data-ttu-id="24596-168">tooenable SSO dans **SkyDesk messagerie**, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="24596-168">tooenable SSO in **SkyDesk Email**, perform hello following steps:</span></span>

    <span data-ttu-id="24596-169">a.</span><span class="sxs-lookup"><span data-stu-id="24596-169">a.</span></span> <span data-ttu-id="24596-170">Authentification tooyour SkyDesk courriel en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="24596-170">Sign-on tooyour SkyDesk Email account as administrator.</span></span>

    <span data-ttu-id="24596-171">b.</span><span class="sxs-lookup"><span data-stu-id="24596-171">b.</span></span> <span data-ttu-id="24596-172">Dans le menu hello haut de hello, cliquez sur **le programme d’installation**, puis sélectionnez **Org**.</span><span class="sxs-lookup"><span data-stu-id="24596-172">In hello menu on hello top, click **Setup**, and select **Org**.</span></span> 
    
      ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_51.png)
  
    <span data-ttu-id="24596-174">c.</span><span class="sxs-lookup"><span data-stu-id="24596-174">c.</span></span> <span data-ttu-id="24596-175">Cliquez sur **domaines** à partir du volet de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="24596-175">Click on **Domains** from hello left panel.</span></span>
    
      ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_53.png)

    <span data-ttu-id="24596-177">d.</span><span class="sxs-lookup"><span data-stu-id="24596-177">d.</span></span> <span data-ttu-id="24596-178">Cliquez sur **Add Domain**.</span><span class="sxs-lookup"><span data-stu-id="24596-178">Click on **Add Domain**.</span></span>
    
      ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_54.png)

    <span data-ttu-id="24596-180">e.</span><span class="sxs-lookup"><span data-stu-id="24596-180">e.</span></span> <span data-ttu-id="24596-181">Entrez votre nom de domaine et vérifiez hello domaine.</span><span class="sxs-lookup"><span data-stu-id="24596-181">Enter your Domain name, and then verify hello Domain.</span></span>
    
      ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_55.png)

    <span data-ttu-id="24596-183">f.</span><span class="sxs-lookup"><span data-stu-id="24596-183">f.</span></span> <span data-ttu-id="24596-184">Cliquez sur **l’authentification SAML** à partir du volet de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="24596-184">Click on **SAML Authentication** from hello left panel.</span></span>
    
      ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_52.png)

8. <span data-ttu-id="24596-186">Sur hello **l’authentification SAML** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="24596-186">On hello **SAML Authentication** dialog page, perform hello following steps:</span></span>
   
      ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_56.png)
   
    >[!NOTE]
    ><span data-ttu-id="24596-188">authentification basée sur les toouse SAML, vous devez avoir **vérifié domaine** ou **portail URL** le programme d’installation.</span><span class="sxs-lookup"><span data-stu-id="24596-188">toouse SAML based authentication, you should either have **verified domain** or **portal URL** setup.</span></span> <span data-ttu-id="24596-189">Vous pouvez définir le portail de hello URL avec un nom unique hello.</span><span class="sxs-lookup"><span data-stu-id="24596-189">You can set hello portal URL with hello unique name.</span></span>
    > 
    > 
   
    ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_57.png)

    <span data-ttu-id="24596-191">a.</span><span class="sxs-lookup"><span data-stu-id="24596-191">a.</span></span> <span data-ttu-id="24596-192">Bonjour **URL de connexion** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="24596-192">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="24596-193">b.</span><span class="sxs-lookup"><span data-stu-id="24596-193">b.</span></span> <span data-ttu-id="24596-194">Bonjour **déconnexion** zone de texte URL, valeur hello coller **URL de déconnexion**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="24596-194">In hello **Logout** URL textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="24596-195">c.</span><span class="sxs-lookup"><span data-stu-id="24596-195">c.</span></span> <span data-ttu-id="24596-196">**Modifier l’URL de mot de passe** est facultative, vous pouvez donc laisser cette valeur vide.</span><span class="sxs-lookup"><span data-stu-id="24596-196">**Change Password URL** is optional so leave it blank.</span></span>

    <span data-ttu-id="24596-197">d.</span><span class="sxs-lookup"><span data-stu-id="24596-197">d.</span></span> <span data-ttu-id="24596-198">Cliquez sur **obtenir une clé à partir du fichier** tooselect votre certificat téléchargé dans le portail Azure, puis cliquez sur **ouvrir** certificat de hello tooupload.</span><span class="sxs-lookup"><span data-stu-id="24596-198">Click on **Get Key From File** tooselect your downloaded certificate from Azure portal, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="24596-199">e.</span><span class="sxs-lookup"><span data-stu-id="24596-199">e.</span></span> <span data-ttu-id="24596-200">Comme **Algorithme**, sélectionnez **RSA**.</span><span class="sxs-lookup"><span data-stu-id="24596-200">As **Algorithm**, select **RSA**.</span></span>

    <span data-ttu-id="24596-201">f.</span><span class="sxs-lookup"><span data-stu-id="24596-201">f.</span></span> <span data-ttu-id="24596-202">Cliquez sur **Ok** modifications de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="24596-202">Click **Ok** toosave hello changes.</span></span>

> [!TIP]
> <span data-ttu-id="24596-203">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="24596-203">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="24596-204">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="24596-204">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="24596-205">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="24596-205">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="24596-206">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="24596-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="24596-207">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="24596-207">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="24596-209">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="24596-209">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="24596-210">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="24596-210">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="24596-212">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="24596-212">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="24596-214">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="24596-214">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="24596-216">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="24596-216">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="24596-218">a.</span><span class="sxs-lookup"><span data-stu-id="24596-218">a.</span></span> <span data-ttu-id="24596-219">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="24596-219">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="24596-220">b.</span><span class="sxs-lookup"><span data-stu-id="24596-220">b.</span></span> <span data-ttu-id="24596-221">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="24596-221">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="24596-222">c.</span><span class="sxs-lookup"><span data-stu-id="24596-222">c.</span></span> <span data-ttu-id="24596-223">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="24596-223">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="24596-224">d.</span><span class="sxs-lookup"><span data-stu-id="24596-224">d.</span></span> <span data-ttu-id="24596-225">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="24596-225">Click **Create**.</span></span>
 
### <a name="creating-a-skydesk-email-test-user"></a><span data-ttu-id="24596-226">Création d’un utilisateur de test SkyDesk Email</span><span class="sxs-lookup"><span data-stu-id="24596-226">Creating a SkyDesk Email test user</span></span>

<span data-ttu-id="24596-227">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans SkyDesk Email.</span><span class="sxs-lookup"><span data-stu-id="24596-227">In this section, you create a user called Britta Simon in SkyDesk Email.</span></span>

1. <span data-ttu-id="24596-228">Cliquez sur **accès utilisateur** de hello gauche du panneau par courrier électronique SkyDesk et puis entrez votre nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="24596-228">Click on **User Access** from hello left panel in SkyDesk Email and then enter your username.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_58.png)

>[!NOTE] 
><span data-ttu-id="24596-230">Si vous avez besoin des utilisateurs en bloc de toocreate, vous devez toocontact hello [équipe de support Client de messagerie SkyDesk](https://www.skydesk.sg/support/).</span><span class="sxs-lookup"><span data-stu-id="24596-230">If you need toocreate bulk users, you need toocontact hello [SkyDesk Email Client support team](https://www.skydesk.sg/support/).</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="24596-231">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="24596-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="24596-232">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSkyDesk par courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="24596-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSkyDesk Email.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="24596-234">**tooassign Britta Simon tooSkyDesk par courrier électronique, exécutez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="24596-234">**tooassign Britta Simon tooSkyDesk Email, perform hello following steps:**</span></span>

1. <span data-ttu-id="24596-235">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="24596-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="24596-237">Dans la liste des applications hello, sélectionnez **SkyDesk E-mail**.</span><span class="sxs-lookup"><span data-stu-id="24596-237">In hello applications list, select **SkyDesk Email**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_app.png) 

3. <span data-ttu-id="24596-239">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="24596-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="24596-241">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="24596-241">Click **Add** button.</span></span> <span data-ttu-id="24596-242">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="24596-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="24596-244">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="24596-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="24596-245">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="24596-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="24596-246">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="24596-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="24596-247">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="24596-247">Testing single sign-on</span></span>

<span data-ttu-id="24596-248">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="24596-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="24596-249">Lorsque vous cliquez sur hello SkyDesk messagerie vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur application de messagerie de SkyDesk tooyour.</span><span class="sxs-lookup"><span data-stu-id="24596-249">When you click hello SkyDesk Email tile in hello Access Panel, you should get automatically signed-on tooyour SkyDesk Email application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="24596-250">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="24596-250">Additional resources</span></span>

* [<span data-ttu-id="24596-251">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="24596-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="24596-252">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="24596-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_203.png

