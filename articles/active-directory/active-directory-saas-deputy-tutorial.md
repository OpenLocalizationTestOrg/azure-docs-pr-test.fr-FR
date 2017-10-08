---
title: "Didacticiel : intégration d’Azure Active Directory à Deputy | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et adjoint."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 42f65b758682ce2513b6bb38ef40a19f955c88c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a><span data-ttu-id="873d2-103">Didacticiel : Intégration d’Azure Active Directory avec Deputy</span><span class="sxs-lookup"><span data-stu-id="873d2-103">Tutorial: Azure Active Directory integration with Deputy</span></span>

<span data-ttu-id="873d2-104">Dans ce didacticiel, vous apprendrez comment toointegrate adjoint avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="873d2-104">In this tutorial, you learn how toointegrate Deputy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="873d2-105">Intégration adjoint à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="873d2-105">Integrating Deputy with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="873d2-106">Vous pouvez contrôler dans Azure AD qui a accès tooDeputy</span><span class="sxs-lookup"><span data-stu-id="873d2-106">You can control in Azure AD who has access tooDeputy</span></span>
- <span data-ttu-id="873d2-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooDeputy (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="873d2-107">You can enable your users tooautomatically get signed-on tooDeputy (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="873d2-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="873d2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="873d2-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="873d2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="873d2-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="873d2-110">Prerequisites</span></span>

<span data-ttu-id="873d2-111">tooconfigure intégration d’Azure AD avec adjoint, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="873d2-111">tooconfigure Azure AD integration with Deputy, you need hello following items:</span></span>

- <span data-ttu-id="873d2-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="873d2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="873d2-113">Un abonnement Deputy pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="873d2-113">A Deputy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="873d2-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="873d2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="873d2-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="873d2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="873d2-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="873d2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="873d2-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="873d2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="873d2-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="873d2-118">Scenario description</span></span>
<span data-ttu-id="873d2-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="873d2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="873d2-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="873d2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="873d2-121">Ajout d’adjoint à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="873d2-121">Adding Deputy from hello gallery</span></span>
2. <span data-ttu-id="873d2-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="873d2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-deputy-from-hello-gallery"></a><span data-ttu-id="873d2-123">Ajout d’adjoint à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="873d2-123">Adding Deputy from hello gallery</span></span>
<span data-ttu-id="873d2-124">tooconfigure hello intégration d’adjoint dans Azure AD, vous devez tooadd adjoint à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="873d2-124">tooconfigure hello integration of Deputy into Azure AD, you need tooadd Deputy from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="873d2-125">**tooadd adjoint à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="873d2-125">**tooadd Deputy from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="873d2-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="873d2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="873d2-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="873d2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="873d2-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="873d2-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="873d2-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="873d2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="873d2-133">Dans la zone de recherche de hello, tapez **adjoint**.</span><span class="sxs-lookup"><span data-stu-id="873d2-133">In hello search box, type **Deputy**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_search.png)

5. <span data-ttu-id="873d2-135">Dans le volet de résultats hello, sélectionnez **adjoint**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="873d2-135">In hello results panel, select **Deputy**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="873d2-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="873d2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="873d2-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Deputy, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="873d2-138">In this section, you configure and test Azure AD single sign-on with Deputy based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="873d2-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello adjoint est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="873d2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Deputy is tooa user in Azure AD.</span></span> <span data-ttu-id="873d2-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans adjoint doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="873d2-140">In other words, a link relationship between an Azure AD user and hello related user in Deputy needs toobe established.</span></span>

<span data-ttu-id="873d2-141">Dans adjoint, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="873d2-141">In Deputy, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="873d2-142">tooconfigure et test Azure AD l’authentification unique avec adjoint, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="873d2-142">tooconfigure and test Azure AD single sign-on with Deputy, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="873d2-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="873d2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="873d2-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="873d2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="873d2-145">**[Création d’un utilisateur de test adjoint](#creating-a-deputy-test-user)**  -toohave un équivalent de Britta Simon dans adjoint est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="873d2-145">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - toohave a counterpart of Britta Simon in Deputy that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="873d2-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="873d2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="873d2-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="873d2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="873d2-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="873d2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="873d2-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application adjoint.</span><span class="sxs-lookup"><span data-stu-id="873d2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Deputy application.</span></span>

<span data-ttu-id="873d2-150">**tooconfigure Azure AD single sign-on avec adjoint, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="873d2-150">**tooconfigure Azure AD single sign-on with Deputy, perform hello following steps:**</span></span>

1. <span data-ttu-id="873d2-151">Bonjour portail Azure, sur hello **adjoint** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="873d2-151">In hello Azure portal, on hello **Deputy** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="873d2-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="873d2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_samlbase.png)

3. <span data-ttu-id="873d2-155">Sur hello **adjoint domaine et les URL** section, si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="873d2-155">On hello **Deputy Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url1.png)

    <span data-ttu-id="873d2-157">a.</span><span class="sxs-lookup"><span data-stu-id="873d2-157">a.</span></span> <span data-ttu-id="873d2-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="873d2-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    |  |
    | ----|
    | `https://<subdomain>.<region>.au.deputy.com` |
    | `https://<subdomain>.<region>.ent-au.deputy.com` |
    | `https://<subdomain>.<region>.na.deputy.com`|
    | `https://<subdomain>.<region>.ent-na.deputy.com`|
    | `https://<subdomain>.<region>.eu.deputy.com` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com` |
    | `https://<subdomain>.<region>.as.deputy.com` |
    | `https://<subdomain>.<region>.ent-as.deputy.com` |
    | `https://<subdomain>.<region>.la.deputy.com` |
    | `https://<subdomain>.<region>.ent-la.deputy.com` |
    | `https://<subdomain>.<region>.af.deputy.com` |
    | `https://<subdomain>.<region>.ent-af.deputy.com` |
    | `https://<subdomain>.<region>.an.deputy.com` |
    | `https://<subdomain>.<region>.ent-an.deputy.com` |
    | `https://<subdomain>.<region>.deputy.com` |

    <span data-ttu-id="873d2-159">b.</span><span class="sxs-lookup"><span data-stu-id="873d2-159">b.</span></span> <span data-ttu-id="873d2-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="873d2-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |----|
    | `https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs.` |

4. <span data-ttu-id="873d2-161">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="873d2-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="873d2-162">Si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="873d2-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url2.png)

    <span data-ttu-id="873d2-164">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<your-subdomain>.<region>.deputy.com`</span><span class="sxs-lookup"><span data-stu-id="873d2-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<your-subdomain>.<region>.deputy.com`</span></span>
    
    >[!NOTE]
    > <span data-ttu-id="873d2-165">Le suffixe de région Deputy est facultatif ou il doit utiliser l’une des valeurs suivantes : au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span><span class="sxs-lookup"><span data-stu-id="873d2-165">Deputy region suffix is optional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span></span>

    > [!NOTE] 
    > <span data-ttu-id="873d2-166">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="873d2-166">These values are not real.</span></span> <span data-ttu-id="873d2-167">Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="873d2-167">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="873d2-168">Contact [équipe de support technique adjoint](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="873d2-168">Contact [Deputy support team](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget these values.</span></span> 

5. <span data-ttu-id="873d2-169">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="873d2-169">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_certificate.png) 

6. <span data-ttu-id="873d2-171">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="873d2-171">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-deputy-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="873d2-173">Sur hello **adjoint Configuration** , cliquez sur **adjoint de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="873d2-173">On hello **Deputy Configuration** section, click **Configure Deputy** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="873d2-174">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="873d2-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_configure.png) 

8. <span data-ttu-id="873d2-176">Accédez toohello suivant l’URL :[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span><span class="sxs-lookup"><span data-stu-id="873d2-176">Navigate toohello following URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span></span> <span data-ttu-id="873d2-177">Accédez trop**paramètres de sécurité** et cliquez sur **modifier**.</span><span class="sxs-lookup"><span data-stu-id="873d2-177">Go too**Security Settings** and click **Edit**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)

9. <span data-ttu-id="873d2-179">Sur cette page **Paramètres de sécurité** , procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="873d2-179">On this **Security Settings** page, perform below steps.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)
    
    <span data-ttu-id="873d2-181">a.</span><span class="sxs-lookup"><span data-stu-id="873d2-181">a.</span></span> <span data-ttu-id="873d2-182">Activez la **connexion à partir de réseaux sociaux**.</span><span class="sxs-lookup"><span data-stu-id="873d2-182">Enable **Social Login**.</span></span>
   
    <span data-ttu-id="873d2-183">b.</span><span class="sxs-lookup"><span data-stu-id="873d2-183">b.</span></span> <span data-ttu-id="873d2-184">Ouvrez votre certificat codé en Base64 téléchargé à partir du portail Azure dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat OpenSSL** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="873d2-184">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **OpenSSL Certificate** textbox.</span></span>
   
    <span data-ttu-id="873d2-185">c.</span><span class="sxs-lookup"><span data-stu-id="873d2-185">c.</span></span> <span data-ttu-id="873d2-186">Dans la zone de texte URL SSO SAML hello, tapez`https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span><span class="sxs-lookup"><span data-stu-id="873d2-186">In hello SAML SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span></span>
    
    <span data-ttu-id="873d2-187">d.</span><span class="sxs-lookup"><span data-stu-id="873d2-187">d.</span></span> <span data-ttu-id="873d2-188">Dans la zone de texte URL SSO SAML hello, remplacez `<your subdomain>` avec votre sous-domaine.</span><span class="sxs-lookup"><span data-stu-id="873d2-188">In hello SAML SSO URL textbox, replace `<your subdomain>` with your subdomain.</span></span>
   
    <span data-ttu-id="873d2-189">e.</span><span class="sxs-lookup"><span data-stu-id="873d2-189">e.</span></span> <span data-ttu-id="873d2-190">Dans la zone de texte URL SSO SAML hello, remplacez `<saml sso url>` avec hello **SAML Sign-On URL du Service unique** que vous avez copié à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="873d2-190">In hello SAML SSO URL textbox, replace `<saml sso url>` with hello **SAML Single Sign-On Service URL** you have copied from hello Azure portal.</span></span>
   
    <span data-ttu-id="873d2-191">f.</span><span class="sxs-lookup"><span data-stu-id="873d2-191">f.</span></span> <span data-ttu-id="873d2-192">Cliquez sur **Save Settings**.</span><span class="sxs-lookup"><span data-stu-id="873d2-192">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="873d2-193">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="873d2-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="873d2-194">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="873d2-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="873d2-195">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="873d2-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="873d2-196">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="873d2-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="873d2-197">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="873d2-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="873d2-199">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="873d2-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="873d2-200">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="873d2-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="873d2-202">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="873d2-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="873d2-204">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="873d2-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="873d2-206">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="873d2-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="873d2-208">a.</span><span class="sxs-lookup"><span data-stu-id="873d2-208">a.</span></span> <span data-ttu-id="873d2-209">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="873d2-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="873d2-210">b.</span><span class="sxs-lookup"><span data-stu-id="873d2-210">b.</span></span> <span data-ttu-id="873d2-211">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="873d2-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="873d2-212">c.</span><span class="sxs-lookup"><span data-stu-id="873d2-212">c.</span></span> <span data-ttu-id="873d2-213">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="873d2-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="873d2-214">d.</span><span class="sxs-lookup"><span data-stu-id="873d2-214">d.</span></span> <span data-ttu-id="873d2-215">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="873d2-215">Click **Create**.</span></span>
 
### <a name="creating-a-deputy-test-user"></a><span data-ttu-id="873d2-216">Création d’un utilisateur de test Deputy</span><span class="sxs-lookup"><span data-stu-id="873d2-216">Creating a Deputy test user</span></span>

<span data-ttu-id="873d2-217">tooenable Azure AD les utilisateurs toolog dans tooDeputy, vous devez les configurer dans adjoint.</span><span class="sxs-lookup"><span data-stu-id="873d2-217">tooenable Azure AD users toolog in tooDeputy, they must be provisioned into Deputy.</span></span> <span data-ttu-id="873d2-218">Dans le cas de Deputy, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="873d2-218">In case of Deputy, provisioning is a manual task.</span></span>

#### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="873d2-219">tooprovision un compte d’utilisateur, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="873d2-219">tooprovision a user account, perform hello following steps:</span></span>
1. <span data-ttu-id="873d2-220">Ouvrez une session en tant qu’administrateur dans le site d’entreprise tooyour adjoint.</span><span class="sxs-lookup"><span data-stu-id="873d2-220">Log in tooyour Deputy company site as an administrator.</span></span>

2. <span data-ttu-id="873d2-221">Dans le volet de navigation supérieur de hello, cliquez sur **personnes**.</span><span class="sxs-lookup"><span data-stu-id="873d2-221">On hello top navigation pane, click **People**.</span></span>
   
   <span data-ttu-id="873d2-222">![Personnes](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "Personnes")</span><span class="sxs-lookup"><span data-stu-id="873d2-222">![People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "People")</span></span>

3. <span data-ttu-id="873d2-223">Cliquez sur hello **ajouter des personnes** , puis cliquez sur **ajouter une seule personne**.</span><span class="sxs-lookup"><span data-stu-id="873d2-223">Click hello **Add People** button and click **Add a single person**.</span></span>
   
   <span data-ttu-id="873d2-224">![Ajouter des personnes](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "ajouter des personnes")</span><span class="sxs-lookup"><span data-stu-id="873d2-224">![Add People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Add People")</span></span>

4. <span data-ttu-id="873d2-225">Effectuer hello comme suit, puis cliquez sur **Enregistrer & Inviter**.</span><span class="sxs-lookup"><span data-stu-id="873d2-225">Perform hello following steps and click **Save & Invite**.</span></span>
   
   <span data-ttu-id="873d2-226">![Nouvel utilisateur](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "Nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="873d2-226">![New User](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "New User")</span></span>

   <span data-ttu-id="873d2-227">a.</span><span class="sxs-lookup"><span data-stu-id="873d2-227">a.</span></span> <span data-ttu-id="873d2-228">Bonjour **nom** zone de texte, nom du type d’utilisateur hello comme **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="873d2-228">In hello **Name** textbox, type name of hello user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="873d2-229">b.</span><span class="sxs-lookup"><span data-stu-id="873d2-229">b.</span></span> <span data-ttu-id="873d2-230">Bonjour **messagerie** zone de texte, tapez Bonjour adresse de messagerie d’un compte Azure AD que vous souhaitez tooprovision.</span><span class="sxs-lookup"><span data-stu-id="873d2-230">In hello **Email** textbox, type hello email address of an Azure AD account you want tooprovision.</span></span>
   
   <span data-ttu-id="873d2-231">c.</span><span class="sxs-lookup"><span data-stu-id="873d2-231">c.</span></span> <span data-ttu-id="873d2-232">Bonjour **travailler à** zone de texte, nom de type hello entreprise.</span><span class="sxs-lookup"><span data-stu-id="873d2-232">In hello **Work at** textbox, type hello business name.</span></span>
   
   <span data-ttu-id="873d2-233">d.</span><span class="sxs-lookup"><span data-stu-id="873d2-233">d.</span></span> <span data-ttu-id="873d2-234">Cliquez sur le bouton **Save & Invite**.</span><span class="sxs-lookup"><span data-stu-id="873d2-234">Click **Save & Invite** button.</span></span>

5. <span data-ttu-id="873d2-235">titulaire du compte AAD Hello reçoit un message électronique et suit un tooconfirm de lier leur compte avant son activation.</span><span class="sxs-lookup"><span data-stu-id="873d2-235">hello AAD account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span> <span data-ttu-id="873d2-236">Vous pouvez utiliser n’importe quel autre adjoint utilisateur compte outil de création ou API fournie par adjoint tooprovision AAD comptes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="873d2-236">You can use any other Deputy user account creation tools or APIs provided by Deputy tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="873d2-237">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="873d2-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="873d2-238">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooDeputy.</span><span class="sxs-lookup"><span data-stu-id="873d2-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDeputy.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="873d2-240">**tooassign Britta Simon tooDeputy, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="873d2-240">**tooassign Britta Simon tooDeputy, perform hello following steps:**</span></span>

1. <span data-ttu-id="873d2-241">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="873d2-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="873d2-243">Dans la liste des applications hello, sélectionnez **adjoint**.</span><span class="sxs-lookup"><span data-stu-id="873d2-243">In hello applications list, select **Deputy**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_app.png) 

3. <span data-ttu-id="873d2-245">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="873d2-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="873d2-247">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="873d2-247">Click **Add** button.</span></span> <span data-ttu-id="873d2-248">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="873d2-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="873d2-250">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="873d2-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="873d2-251">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="873d2-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="873d2-252">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="873d2-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="873d2-253">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="873d2-253">Testing single sign-on</span></span>

<span data-ttu-id="873d2-254">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="873d2-254">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="873d2-255">Lorsque vous cliquez sur hello adjoint vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour adjoint application.</span><span class="sxs-lookup"><span data-stu-id="873d2-255">When you click hello Deputy tile in hello Access Panel, you should get automatically signed-on tooyour Deputy application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="873d2-256">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="873d2-256">Additional resources</span></span>

* [<span data-ttu-id="873d2-257">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="873d2-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="873d2-258">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="873d2-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_203.png

