---
title: "Didacticiel : Intégration d’Azure Active Directory à 8x8 Virtual Office | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et 8 x 8 virtuel Office."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b34a6edf-e745-4aec-b0b2-7337473d64c5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: df5c5de77285cd3912b68cc3b1e3eee274aa951c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-8x8-virtual-office"></a><span data-ttu-id="f8bf8-103">Didacticiel : Intégration d’Azure Active Directory à 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="f8bf8-103">Tutorial: Azure Active Directory integration with 8x8 Virtual Office</span></span>

<span data-ttu-id="f8bf8-104">Dans ce didacticiel, vous apprendrez comment toointegrate 8 x 8 bureau virtuel avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f8bf8-104">In this tutorial, you learn how toointegrate 8x8 Virtual Office with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f8bf8-105">Intégration de 8 x 8 bureau virtuel avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="f8bf8-105">Integrating 8x8 Virtual Office with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f8bf8-106">Vous pouvez contrôler dans Azure AD qui a accès too8x8 virtuel Office</span><span class="sxs-lookup"><span data-stu-id="f8bf8-106">You can control in Azure AD who has access too8x8 Virtual Office</span></span>
- <span data-ttu-id="f8bf8-107">Vous pouvez activer vos utilisateurs tooautomatically obtenir authentifiés sur too8x8 de bureau virtuel (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8bf8-107">You can enable your users tooautomatically get signed-on too8x8 Virtual Office (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f8bf8-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="f8bf8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f8bf8-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f8bf8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8bf8-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f8bf8-110">Prerequisites</span></span>

<span data-ttu-id="f8bf8-111">tooconfigure intégration d’Azure AD avec 8 x 8 virtuel Office, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f8bf8-111">tooconfigure Azure AD integration with 8x8 Virtual Office, you need hello following items:</span></span>

- <span data-ttu-id="f8bf8-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8bf8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f8bf8-113">Un abonnement 8x8 Virtual Office pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="f8bf8-113">A 8x8 Virtual Office single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f8bf8-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f8bf8-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="f8bf8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f8bf8-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f8bf8-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f8bf8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f8bf8-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="f8bf8-118">Scenario description</span></span>
<span data-ttu-id="f8bf8-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f8bf8-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="f8bf8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f8bf8-121">Ajout de 8 x 8 virtuel Office à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f8bf8-121">Adding 8x8 Virtual Office from hello gallery</span></span>
2. <span data-ttu-id="f8bf8-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8bf8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-8x8-virtual-office-from-hello-gallery"></a><span data-ttu-id="f8bf8-123">Ajout de 8 x 8 virtuel Office à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f8bf8-123">Adding 8x8 Virtual Office from hello gallery</span></span>
<span data-ttu-id="f8bf8-124">tooconfigure hello intégration d’Office de virtuel 8 x 8 dans Azure AD, vous devez tooadd 8 x 8 bureau virtuel à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-124">tooconfigure hello integration of 8x8 Virtual Office into Azure AD, you need tooadd 8x8 Virtual Office from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f8bf8-125">**effectuer de bureau virtuel à partir de la galerie hello, tooadd 8 x 8 hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f8bf8-125">**tooadd 8x8 Virtual Office from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8bf8-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f8bf8-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f8bf8-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="f8bf8-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="f8bf8-133">Dans la zone de recherche de hello, tapez **8 x 8 virtuelle Office**.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-133">In hello search box, type **8x8 Virtual Office**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_search.png)

5. <span data-ttu-id="f8bf8-135">Dans le volet de résultats hello, sélectionnez **8 x 8 virtuelle Office**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-135">In hello results panel, select **8x8 Virtual Office**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f8bf8-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8bf8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f8bf8-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec 8x8 Virtual Office, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="f8bf8-138">In this section, you configure and test Azure AD single sign-on with 8x8 Virtual Office based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f8bf8-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans 8 x 8 virtuel Office est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 8x8 Virtual Office is tooa user in Azure AD.</span></span> <span data-ttu-id="f8bf8-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans 8 x 8 bureau virtuel doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-140">In other words, a link relationship between an Azure AD user and hello related user in 8x8 Virtual Office needs toobe established.</span></span>

<span data-ttu-id="f8bf8-141">Bureau virtuel de 8 x 8, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-141">In 8x8 Virtual Office, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f8bf8-142">tooconfigure et test Azure AD l’authentification unique avec 8 x 8 virtuel Office, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="f8bf8-142">tooconfigure and test Azure AD single sign-on with 8x8 Virtual Office, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f8bf8-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f8bf8-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f8bf8-145">**[Création d’un utilisateur de test de bureau virtuel 8 x 8](#creating-a-8x8-virtual-office-test-user)**  -toohave un équivalent de Britta Simon de bureau virtuel 8 x 8 qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-145">**[Creating a 8x8 Virtual Office test user](#creating-a-8x8-virtual-office-test-user)** - toohave a counterpart of Britta Simon in 8x8 Virtual Office that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f8bf8-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f8bf8-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f8bf8-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8bf8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f8bf8-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de bureau virtuel 8 x 8.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 8x8 Virtual Office application.</span></span>

<span data-ttu-id="f8bf8-150">**tooconfigure Azure AD l’authentification unique avec 8 x 8 virtuel Office, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f8bf8-150">**tooconfigure Azure AD single sign-on with 8x8 Virtual Office, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8bf8-151">Bonjour portail Azure, sur hello **8 x 8 virtuelle Office** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-151">In hello Azure portal, on hello **8x8 Virtual Office** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="f8bf8-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_samlbase.png)

3. <span data-ttu-id="f8bf8-155">Sur hello **URL et domaine virtuel 8 x 8** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f8bf8-155">On hello **8x8 Virtual Office Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_url.png)

    <span data-ttu-id="f8bf8-157">a.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-157">a.</span></span> <span data-ttu-id="f8bf8-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="f8bf8-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="f8bf8-159">| `https://sso.8x8.com/<companyname>` |
    | `https://www.8x8.com/<companyname>` |
    | `https://sso.8x8pilot.com/<companyname>` |</span><span class="sxs-lookup"><span data-stu-id="f8bf8-159">| `https://sso.8x8.com/<companyname>` |
 | `https://www.8x8.com/<companyname>` |
 | `https://sso.8x8pilot.com/<companyname>` |</span></span>

    <span data-ttu-id="f8bf8-160">b.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-160">b.</span></span> <span data-ttu-id="f8bf8-161">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="f8bf8-161">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="f8bf8-162">| `https://<subdomain>.8x8.com/saml2` |
    | `https://<subdomain>.8x8pilot.com/saml2`|</span><span class="sxs-lookup"><span data-stu-id="f8bf8-162">| `https://<subdomain>.8x8.com/saml2` |
 | `https://<subdomain>.8x8pilot.com/saml2`|</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f8bf8-163">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-163">These values are not real.</span></span> <span data-ttu-id="f8bf8-164">Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-164">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="f8bf8-165">Contact [équipe de support technique de bureau virtuel 8 x 8](https://www.8x8.com/about-us/contact-us) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-165">Contact [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us) tooget these values.</span></span>
 


4. <span data-ttu-id="f8bf8-166">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Raw)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-166">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_certificate.png) 

5. <span data-ttu-id="f8bf8-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="f8bf8-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f8bf8-170">Sur hello **8 x 8 virtuel Office Configuration** , cliquez sur **configurer 8 x 8 Virtual Office** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-170">On hello **8x8 Virtual Office Configuration** section, click **Configure 8x8 Virtual Office** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f8bf8-171">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="f8bf8-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_configure.png) 

7. <span data-ttu-id="f8bf8-173">Authentification tooyour 8 x 8 client de bureau virtuel en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-173">Sign-on tooyour 8x8 Virtual Office tenant as an administrator.</span></span>

8. <span data-ttu-id="f8bf8-174">Sélectionnez **Virtual Office Account Mgr** (Gestionnaire de compte Virtual Office) dans le volet Applications.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-174">Select **Virtual Office Account Mgr** on Application Panel.</span></span>
   
    ![Configurer l’authentification côté application](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_001.png)

9. <span data-ttu-id="f8bf8-176">Sélectionnez **Business** toomanage de compte, cliquez sur **connexion** bouton.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-176">Select **Business** account toomanage and click **Sign In** button.</span></span>
   
    ![Configurer l’authentification côté application](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_002.png)

10. <span data-ttu-id="f8bf8-178">Cliquez sur **comptes** onglet dans la liste de menus hello.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-178">Click **Accounts** tab in hello menu list.</span></span>
   
    ![Configurer l’authentification côté application](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_003.png)

11. <span data-ttu-id="f8bf8-180">Cliquez sur **Single Sign On** dans la liste hello de comptes.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-180">Click **Single Sign On** in hello list of Accounts.</span></span>
   
    ![Configurer l’authentification côté application](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_004.png)

12. <span data-ttu-id="f8bf8-182">Sélectionnez **Authentification unique** sous la section Méthode d’authentification, puis cliquez sur **SAML**.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-182">Select **Single Sign On** under Authentication method and click **SAML**.</span></span>
    
    ![Configurer l’authentification côté application](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_005.png)

13. <span data-ttu-id="f8bf8-184">Copie **URL SSO SAML**, **unique à l’aide des URL du Service** et **URL de l’émetteur** d’Azure AD trop**URL de connexion**, **URL de déconnexion**  et **URL de l’émetteur** de bureau virtuel de 8 x 8.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-184">Copy **SAML SSO URL**, **Single Sing Out Service URL** and **Issuer URL** from Azure AD too**Sign In URL**, **Sign Out URL** and **Issuer URL** in 8x8 Virtual Office.</span></span> 
    
    ![Configurer l’authentification côté application](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_006.png)
    
14. <span data-ttu-id="f8bf8-186">Cliquez sur **navigateur** certificat de hello tooupload que vous avez téléchargé à partir d’Azure AD, puis cliquez sur hello **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-186">Click **Browser** button tooupload hello certificate which you downloaded from Azure AD, and click hello **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="f8bf8-187">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="f8bf8-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f8bf8-188">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f8bf8-189">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f8bf8-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f8bf8-190">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8bf8-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="f8bf8-191">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="f8bf8-193">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f8bf8-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8bf8-194">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f8bf8-196">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f8bf8-198">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f8bf8-200">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f8bf8-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f8bf8-202">a.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-202">a.</span></span> <span data-ttu-id="f8bf8-203">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f8bf8-204">b.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-204">b.</span></span> <span data-ttu-id="f8bf8-205">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f8bf8-206">c.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-206">c.</span></span> <span data-ttu-id="f8bf8-207">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f8bf8-208">d.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-208">d.</span></span> <span data-ttu-id="f8bf8-209">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-209">Click **Create**.</span></span>
 
### <a name="creating-a-8x8-virtual-office-test-user"></a><span data-ttu-id="f8bf8-210">Création d’un utilisateur de test 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="f8bf8-210">Creating a 8x8 Virtual Office test user</span></span>

<span data-ttu-id="f8bf8-211">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans 8 x 8 virtuel Office.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-211">hello objective of this section is toocreate a user called Britta Simon in 8x8 Virtual Office.</span></span> <span data-ttu-id="f8bf8-212">8x8 Virtual Office prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-212">8x8 Virtual Office supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="f8bf8-213">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-213">There is no action item for you in this section.</span></span> <span data-ttu-id="f8bf8-214">Un nouvel utilisateur est créé au cours d’une tentative de tooaccess 8 x 8 virtuel Office s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-214">A new user is created during an attempt tooaccess 8x8 Virtual Office if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="f8bf8-215">Si vous devez manuellement toocreate un utilisateur, vous devez toocontact hello [équipe de support technique de bureau virtuel 8 x 8](https://www.8x8.com/about-us/contact-us).</span><span class="sxs-lookup"><span data-stu-id="f8bf8-215">If you need toocreate a user manually, you need toocontact hello [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f8bf8-216">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8bf8-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f8bf8-217">Dans cette section, vous activez Britta Simon toouse Azure l’authentification unique en accordant l’accès too8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too8x8 Virtual Office.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="f8bf8-219">**tooassign Britta Simon too8x8 Virtual Office, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f8bf8-219">**tooassign Britta Simon too8x8 Virtual Office, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8bf8-220">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="f8bf8-222">Dans la liste des applications hello, sélectionnez **8 x 8 virtuelle Office**.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-222">In hello applications list, select **8x8 Virtual Office**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_app.png) 

3. <span data-ttu-id="f8bf8-224">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="f8bf8-226">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-226">Click **Add** button.</span></span> <span data-ttu-id="f8bf8-227">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="f8bf8-229">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f8bf8-230">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f8bf8-231">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f8bf8-232">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="f8bf8-232">Testing single sign-on</span></span>

<span data-ttu-id="f8bf8-233">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f8bf8-234">Lorsque vous cliquez sur mosaïque de bureau virtuel hello 8 x 8 Bonjour volet d’accès, vous devez obtenir l’application de bureau virtuel tooyour automatiquement signé sur 8 x 8.</span><span class="sxs-lookup"><span data-stu-id="f8bf8-234">When you click hello 8x8 Virtual Office tile in hello Access Panel, you should get automatically signed-on tooyour 8x8 Virtual Office application.</span></span>
<span data-ttu-id="f8bf8-235">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello panneau d’accès](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="f8bf8-235">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f8bf8-236">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f8bf8-236">Additional resources</span></span>

* [<span data-ttu-id="f8bf8-237">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f8bf8-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f8bf8-238">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="f8bf8-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_203.png

