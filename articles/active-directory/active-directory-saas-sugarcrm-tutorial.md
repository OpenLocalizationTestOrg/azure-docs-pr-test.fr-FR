---
title: "Didacticiel : Intégration d’Azure Active Directory avec Sugar CRM | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Sugar CRM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 108d2f8125e410743ee7bc48883a1d0b00602615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sugar-crm"></a><span data-ttu-id="dd767-103">Didacticiel : Intégration d’Azure AD avec Sugar CRM</span><span class="sxs-lookup"><span data-stu-id="dd767-103">Tutorial: Azure Active Directory integration with Sugar CRM</span></span>

<span data-ttu-id="dd767-104">Dans ce didacticiel, vous apprendrez comment toointegrate Sugar CRM avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dd767-104">In this tutorial, you learn how toointegrate Sugar CRM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dd767-105">Intégration Sugar CRM à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="dd767-105">Integrating Sugar CRM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dd767-106">Vous pouvez contrôler dans Azure AD qui a accès tooSugar CRM</span><span class="sxs-lookup"><span data-stu-id="dd767-106">You can control in Azure AD who has access tooSugar CRM</span></span>
- <span data-ttu-id="dd767-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSugar CRM (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd767-107">You can enable your users tooautomatically get signed-on tooSugar CRM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dd767-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="dd767-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dd767-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dd767-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd767-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="dd767-110">Prerequisites</span></span>

<span data-ttu-id="dd767-111">tooconfigure intégration d’Azure AD avec Sugar CRM, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="dd767-111">tooconfigure Azure AD integration with Sugar CRM, you need hello following items:</span></span>

- <span data-ttu-id="dd767-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd767-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dd767-113">Un abonnement Sugar CRM pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="dd767-113">A Sugar CRM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dd767-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="dd767-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dd767-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="dd767-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dd767-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="dd767-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dd767-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dd767-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dd767-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="dd767-118">Scenario description</span></span>
<span data-ttu-id="dd767-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="dd767-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dd767-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="dd767-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dd767-121">Ajout de Sugar CRM à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="dd767-121">Adding Sugar CRM from hello gallery</span></span>
2. <span data-ttu-id="dd767-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd767-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sugar-crm-from-hello-gallery"></a><span data-ttu-id="dd767-123">Ajout de Sugar CRM à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="dd767-123">Adding Sugar CRM from hello gallery</span></span>
<span data-ttu-id="dd767-124">tooconfigure hello intégration de Sugar CRM dans Azure AD, vous devez tooadd Sugar CRM à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="dd767-124">tooconfigure hello integration of Sugar CRM into Azure AD, you need tooadd Sugar CRM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dd767-125">**tooadd Sugar CRM à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd767-125">**tooadd Sugar CRM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd767-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="dd767-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dd767-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="dd767-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dd767-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="dd767-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="dd767-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="dd767-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="dd767-133">Dans la zone de recherche de hello, tapez **Sugar CRM**.</span><span class="sxs-lookup"><span data-stu-id="dd767-133">In hello search box, type **Sugar CRM**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_search.png)

5. <span data-ttu-id="dd767-135">Dans le volet de résultats hello, sélectionnez **Sugar CRM**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="dd767-135">In hello results panel, select **Sugar CRM**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dd767-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd767-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dd767-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Sugar CRM avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="dd767-138">In this section, you configure and test Azure AD single sign-on with Sugar CRM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dd767-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Sugar CRM est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd767-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sugar CRM is tooa user in Azure AD.</span></span> <span data-ttu-id="dd767-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Sugar CRM doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="dd767-140">In other words, a link relationship between an Azure AD user and hello related user in Sugar CRM needs toobe established.</span></span>

<span data-ttu-id="dd767-141">Dans Sugar CRM, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="dd767-141">In Sugar CRM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dd767-142">tooconfigure et test Azure AD l’authentification unique sur Sugar CRM, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="dd767-142">tooconfigure and test Azure AD single sign-on with Sugar CRM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dd767-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="dd767-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dd767-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dd767-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dd767-145">**[Création d’un utilisateur de test Sugar CRM](#creating-a-sugar-crm-test-user)**  -toohave un équivalent de Britta Simon dans Sugar CRM qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dd767-145">**[Creating a Sugar CRM test user](#creating-a-sugar-crm-test-user)** - toohave a counterpart of Britta Simon in Sugar CRM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dd767-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="dd767-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dd767-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="dd767-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dd767-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd767-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dd767-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="dd767-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sugar CRM application.</span></span>

<span data-ttu-id="dd767-150">**tooconfigure Azure AD l’authentification unique sur Sugar CRM, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd767-150">**tooconfigure Azure AD single sign-on with Sugar CRM, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd767-151">Bonjour portail Azure, sur hello **Sugar CRM** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="dd767-151">In hello Azure portal, on hello **Sugar CRM** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="dd767-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="dd767-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_samlbase.png)

3. <span data-ttu-id="dd767-155">Sur hello **Sugar CRM domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd767-155">On hello **Sugar CRM Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_url.png)

    <span data-ttu-id="dd767-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="dd767-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.sugarondemand.com` |
    | `https://<companyname>.trial.sugarcrm` |

    > [!NOTE] 
    > <span data-ttu-id="dd767-158">valeur de Hello n’est pas réelle.</span><span class="sxs-lookup"><span data-stu-id="dd767-158">hello value is not real.</span></span> <span data-ttu-id="dd767-159">Valeur de hello de mise à jour avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="dd767-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="dd767-160">Contact [équipe de support Client de Sugar CRM](https://support.sugarcrm.com/) valeur hello de tooget.</span><span class="sxs-lookup"><span data-stu-id="dd767-160">Contact [Sugar CRM Client support team](https://support.sugarcrm.com/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="dd767-161">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="dd767-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_certificate.png) 

5. <span data-ttu-id="dd767-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="dd767-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dd767-165">Sur hello **Sugar CRM Configuration** , cliquez sur **configurer Sugar CRM** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="dd767-165">On hello **Sugar CRM Configuration** section, click **Configure Sugar CRM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="dd767-166">Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="dd767-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_configure.png) 

7. <span data-ttu-id="dd767-168">Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise Sugar CRM tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="dd767-168">In a different web browser window, log in tooyour Sugar CRM company site as an administrator.</span></span>

8. <span data-ttu-id="dd767-169">Accédez trop**Admin**.</span><span class="sxs-lookup"><span data-stu-id="dd767-169">Go too**Admin**.</span></span>
   
    <span data-ttu-id="dd767-170">![Administrateur](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="dd767-170">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

9. <span data-ttu-id="dd767-171">Bonjour **Administration** , cliquez sur **gestion de mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="dd767-171">In hello **Administration** section, click **Password Management**.</span></span>
   
    <span data-ttu-id="dd767-172">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="dd767-172">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Administration")</span></span>

10. <span data-ttu-id="dd767-173">Sélectionnez **Enable SAML Authentication**.</span><span class="sxs-lookup"><span data-stu-id="dd767-173">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="dd767-174">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="dd767-174">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Administration")</span></span>

11. <span data-ttu-id="dd767-175">Bonjour **l’authentification SAML** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd767-175">In hello **SAML Authentication** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="dd767-176">![Authentification SAML](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "Authentification SAML")</span><span class="sxs-lookup"><span data-stu-id="dd767-176">![SAML Authentication](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "SAML Authentication")</span></span>  
 
    <span data-ttu-id="dd767-177">a.</span><span class="sxs-lookup"><span data-stu-id="dd767-177">a.</span></span> <span data-ttu-id="dd767-178">Bonjour **URL de connexion** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dd767-178">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="dd767-179">b.</span><span class="sxs-lookup"><span data-stu-id="dd767-179">b.</span></span> <span data-ttu-id="dd767-180">Bonjour **URL SLO** zone de texte, valeur hello coller **URL de déconnexion**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dd767-180">In hello **SLO URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="dd767-181">c.</span><span class="sxs-lookup"><span data-stu-id="dd767-181">c.</span></span> <span data-ttu-id="dd767-182">Ouvrez votre certificat codé en base 64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et collez hello l’intégralité du certificat dans **certificat X.509** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="dd767-182">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="dd767-183">d.</span><span class="sxs-lookup"><span data-stu-id="dd767-183">d.</span></span> <span data-ttu-id="dd767-184">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="dd767-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="dd767-185">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="dd767-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dd767-186">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="dd767-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dd767-187">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dd767-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dd767-188">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd767-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="dd767-189">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="dd767-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="dd767-191">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd767-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd767-192">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="dd767-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dd767-194">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="dd767-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dd767-196">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="dd767-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dd767-198">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd767-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dd767-200">a.</span><span class="sxs-lookup"><span data-stu-id="dd767-200">a.</span></span> <span data-ttu-id="dd767-201">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dd767-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dd767-202">b.</span><span class="sxs-lookup"><span data-stu-id="dd767-202">b.</span></span> <span data-ttu-id="dd767-203">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dd767-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dd767-204">c.</span><span class="sxs-lookup"><span data-stu-id="dd767-204">c.</span></span> <span data-ttu-id="dd767-205">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="dd767-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dd767-206">d.</span><span class="sxs-lookup"><span data-stu-id="dd767-206">d.</span></span> <span data-ttu-id="dd767-207">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="dd767-207">Click **Create**.</span></span>
 
### <a name="creating-a-sugar-crm-test-user"></a><span data-ttu-id="dd767-208">Création d’un utilisateur de test Sugar CRM</span><span class="sxs-lookup"><span data-stu-id="dd767-208">Creating a Sugar CRM test user</span></span>

<span data-ttu-id="dd767-209">Dans l’ordre tooenable Azure AD les utilisateurs toolog dans tooSugar CRM, ils doivent être mis en service tooSugar CRM.</span><span class="sxs-lookup"><span data-stu-id="dd767-209">In order tooenable Azure AD users toolog in tooSugar CRM, they must be provisioned tooSugar CRM.</span></span>

<span data-ttu-id="dd767-210">Dans les cas de hello de Sugar CRM, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="dd767-210">In hello case of Sugar CRM, provisioning is a manual task.</span></span>

<span data-ttu-id="dd767-211">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd767-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd767-212">Connectez-vous à tooyour **Sugar CRM** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="dd767-212">Log in tooyour **Sugar CRM** company site as administrator.</span></span>

2. <span data-ttu-id="dd767-213">Accédez trop**Admin**.</span><span class="sxs-lookup"><span data-stu-id="dd767-213">Go too**Admin**.</span></span>
   
    <span data-ttu-id="dd767-214">![Administrateur](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="dd767-214">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

3. <span data-ttu-id="dd767-215">Bonjour **Administration** , cliquez sur **gestion des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="dd767-215">In hello **Administration** section, click **User Management**.</span></span>
   
    <span data-ttu-id="dd767-216">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="dd767-216">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Administration")</span></span>

4. <span data-ttu-id="dd767-217">Accédez trop**utilisateurs \> créer un nouvel utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="dd767-217">Go too**Users \> Create New User**.</span></span>
   
    <span data-ttu-id="dd767-218">![Créer un nouvel utilisateur](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Créer un nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="dd767-218">![Create New User](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Create New User")</span></span>

5. <span data-ttu-id="dd767-219">Sur hello **profil utilisateur** onglet, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd767-219">On hello **User Profile** tab, perform hello following steps:</span></span>
   
    <span data-ttu-id="dd767-220">![Nouvel utilisateur](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "Nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="dd767-220">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "New User")</span></span>

    <span data-ttu-id="dd767-221">a.</span><span class="sxs-lookup"><span data-stu-id="dd767-221">a.</span></span> <span data-ttu-id="dd767-222">Hello de type **nom d’utilisateur**, **nom**, et **adresse de messagerie** d’un utilisateur Azure Active Directory valid dans hello relatives des zones de texte.</span><span class="sxs-lookup"><span data-stu-id="dd767-222">Type hello **user name**, **last name**, and **email address** of a valid Azure Active Directory user into hello related textboxes.</span></span>
  
6. <span data-ttu-id="dd767-223">Pour **Status (Statut)**, sélectionnez **Active (Actif)**.</span><span class="sxs-lookup"><span data-stu-id="dd767-223">As **Status**, select **Active**.</span></span>

7. <span data-ttu-id="dd767-224">Sous l’onglet mot de passe de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd767-224">On hello Password tab, perform hello following steps:</span></span>
   
    <span data-ttu-id="dd767-225">![Nouvel utilisateur](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "Nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="dd767-225">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "New User")</span></span>

    <span data-ttu-id="dd767-226">a.</span><span class="sxs-lookup"><span data-stu-id="dd767-226">a.</span></span> <span data-ttu-id="dd767-227">Mot de passe type hello en hello liés de zone de texte.</span><span class="sxs-lookup"><span data-stu-id="dd767-227">Type hello password into hello related textbox.</span></span>

    <span data-ttu-id="dd767-228">b.</span><span class="sxs-lookup"><span data-stu-id="dd767-228">b.</span></span> <span data-ttu-id="dd767-229">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="dd767-229">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="dd767-230">Vous pouvez utiliser n’importe quel autre Sugar CRM utilisateur compte outil de création ou API fournie par Sugar CRM tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="dd767-230">You can use any other Sugar CRM user account creation tools or APIs provided by Sugar CRM tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dd767-231">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd767-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dd767-232">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSugar CRM.</span><span class="sxs-lookup"><span data-stu-id="dd767-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSugar CRM.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="dd767-234">**tooassign Britta Simon tooSugar CRM, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd767-234">**tooassign Britta Simon tooSugar CRM, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd767-235">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="dd767-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="dd767-237">Dans la liste des applications hello, sélectionnez **Sugar CRM**.</span><span class="sxs-lookup"><span data-stu-id="dd767-237">In hello applications list, select **Sugar CRM**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_app.png) 

3. <span data-ttu-id="dd767-239">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="dd767-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="dd767-241">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="dd767-241">Click **Add** button.</span></span> <span data-ttu-id="dd767-242">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="dd767-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="dd767-244">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="dd767-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dd767-245">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="dd767-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dd767-246">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="dd767-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dd767-247">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="dd767-247">Testing single sign-on</span></span>

<span data-ttu-id="dd767-248">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="dd767-248">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dd767-249">Lorsque vous cliquez sur mosaïque Sugar CRM hello hello volet d’accès, vous devez obtenir l’application de Sugar CRM tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="dd767-249">When you click hello Sugar CRM tile in hello Access Panel, you should get automatically signed-on tooyour Sugar CRM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dd767-250">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="dd767-250">Additional resources</span></span>

* [<span data-ttu-id="dd767-251">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd767-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dd767-252">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="dd767-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_203.png

