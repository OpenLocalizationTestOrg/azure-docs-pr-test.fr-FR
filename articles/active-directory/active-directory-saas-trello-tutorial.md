---
title: "Didacticiel : intégration d’Azure Active Directory à Trello | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Trello."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: de2f2ba6a0e5545983c351f26f99d14f436618c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a><span data-ttu-id="bacf8-103">Didacticiel : Intégration d’Azure Active Directory avec Trello</span><span class="sxs-lookup"><span data-stu-id="bacf8-103">Tutorial: Azure Active Directory integration with Trello</span></span>

<span data-ttu-id="bacf8-104">Dans ce didacticiel, vous apprendrez comment toointegrate Trello avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bacf8-104">In this tutorial, you learn how toointegrate Trello with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bacf8-105">Intégration Trello avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="bacf8-105">Integrating Trello with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bacf8-106">Vous pouvez contrôler dans Azure AD qui a accès tooTrello</span><span class="sxs-lookup"><span data-stu-id="bacf8-106">You can control in Azure AD who has access tooTrello</span></span>
- <span data-ttu-id="bacf8-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooTrello (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="bacf8-107">You can enable your users tooautomatically get signed-on tooTrello (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bacf8-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="bacf8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bacf8-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bacf8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bacf8-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bacf8-110">Prerequisites</span></span>

<span data-ttu-id="bacf8-111">tooconfigure intégration d’Azure AD avec Trello, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="bacf8-111">tooconfigure Azure AD integration with Trello, you need hello following items:</span></span>

- <span data-ttu-id="bacf8-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="bacf8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bacf8-113">Un abonnement Trello pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="bacf8-113">A Trello single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bacf8-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="bacf8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bacf8-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="bacf8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bacf8-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="bacf8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bacf8-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bacf8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bacf8-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="bacf8-118">Scenario description</span></span>
<span data-ttu-id="bacf8-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="bacf8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bacf8-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="bacf8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bacf8-121">Ajout de Trello à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="bacf8-121">Adding Trello from hello gallery</span></span>
2. <span data-ttu-id="bacf8-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bacf8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trello-from-hello-gallery"></a><span data-ttu-id="bacf8-123">Ajout de Trello à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="bacf8-123">Adding Trello from hello gallery</span></span>
<span data-ttu-id="bacf8-124">intégration de hello tooconfigure de Trello dans Azure AD, vous devez tooadd Trello à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="bacf8-124">tooconfigure hello integration of Trello into Azure AD, you need tooadd Trello from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bacf8-125">**tooadd Trello à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bacf8-125">**tooadd Trello from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bacf8-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="bacf8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bacf8-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="bacf8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bacf8-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bacf8-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="bacf8-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="bacf8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="bacf8-133">Dans la zone de recherche de hello, tapez **Trello**.</span><span class="sxs-lookup"><span data-stu-id="bacf8-133">In hello search box, type **Trello**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trello-tutorial/tutorial_trello_search.png)

5. <span data-ttu-id="bacf8-135">Dans le volet de résultats hello, sélectionnez **Trello**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="bacf8-135">In hello results panel, select **Trello**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trello-tutorial/tutorial_trello_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bacf8-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bacf8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bacf8-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Trello avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="bacf8-138">In this section, you configure and test Azure AD single sign-on with Trello based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bacf8-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Trello est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bacf8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Trello is tooa user in Azure AD.</span></span> <span data-ttu-id="bacf8-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Trello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="bacf8-140">In other words, a link relationship between an Azure AD user and hello related user in Trello needs toobe established.</span></span>

<span data-ttu-id="bacf8-141">Dans Trello, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="bacf8-141">In Trello, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bacf8-142">tooconfigure et test Azure AD l’authentification unique avec Trello, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="bacf8-142">tooconfigure and test Azure AD single sign-on with Trello, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bacf8-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="bacf8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bacf8-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bacf8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bacf8-145">**[Création d’un utilisateur de test Trello](#creating-a-trello-test-user)**  -toohave un équivalent de Britta Simon dans Trello est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bacf8-145">**[Creating a Trello test user](#creating-a-trello-test-user)** - toohave a counterpart of Britta Simon in Trello that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bacf8-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="bacf8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bacf8-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="bacf8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bacf8-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bacf8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bacf8-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Trello.</span><span class="sxs-lookup"><span data-stu-id="bacf8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Trello application.</span></span>

<span data-ttu-id="bacf8-150">**tooconfigure Azure AD single sign-on avec Trello, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bacf8-150">**tooconfigure Azure AD single sign-on with Trello, perform hello following steps:**</span></span>

1. <span data-ttu-id="bacf8-151">Bonjour portail Azure, sur hello **Trello** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="bacf8-151">In hello Azure portal, on hello **Trello** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="bacf8-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="bacf8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-trello-tutorial/tutorial_trello_samlbase.png)

3. <span data-ttu-id="bacf8-155">Sur hello **Trello domaine et les URL** section, si vous le souhaitez application hello tooconfigure **mode initialisée par IDP**, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bacf8-155">On hello **Trello Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trello-tutorial/tutorial_trello_url.png)

    <span data-ttu-id="bacf8-157">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="bacf8-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

4. <span data-ttu-id="bacf8-158">Sur hello **Trello domaine et les URL** section, si vous le souhaitez application hello tooconfigure **mode initiée par SP**, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bacf8-158">On hello **Trello Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-trello-tutorial/tutorial_trello_url1.png)

    <span data-ttu-id="bacf8-160">a.</span><span class="sxs-lookup"><span data-stu-id="bacf8-160">a.</span></span> <span data-ttu-id="bacf8-161">Cliquez sur hello **afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="bacf8-161">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="bacf8-162">b.</span><span class="sxs-lookup"><span data-stu-id="bacf8-162">b.</span></span> <span data-ttu-id="bacf8-163">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="bacf8-163">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

    >[!NOTE]
    ><span data-ttu-id="bacf8-164">Vous devez obtenir hello  **\<enterprise\>**  slug dans Trello.</span><span class="sxs-lookup"><span data-stu-id="bacf8-164">You should get hello **\<enterprise\>** slug from Trello.</span></span> <span data-ttu-id="bacf8-165">Si vous n’avez pas valeur slug de hello, contactez [équipe de support Trello](mailto:support@trello.com) slug de hello tooget pour vous d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="bacf8-165">If you don't have hello slug value, contact [Trello support team](mailto:support@trello.com) tooget hello slug for you enterprise.</span></span>
    > 

5. <span data-ttu-id="bacf8-166">Application de Trello attend des attributs spécifiques du toocontain assertions SAML hello.</span><span class="sxs-lookup"><span data-stu-id="bacf8-166">Trello application expects hello SAML assertions toocontain specific attributes.</span></span> <span data-ttu-id="bacf8-167">Configurer hello suivant des attributs pour cette application.</span><span class="sxs-lookup"><span data-stu-id="bacf8-167">Configure hello following attributes  for this application.</span></span> <span data-ttu-id="bacf8-168">Vous pouvez gérer les valeurs de ces attributs hello depuis hello **« Attributs de l’utilisateur »** de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="bacf8-168">You can manage hello values of these attributes from hello **"User Attributes"** of hello application.</span></span> <span data-ttu-id="bacf8-169">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="bacf8-169">hello following screenshot shows an example for this.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trello-tutorial/tutorial_trello_attribute.png)

6. <span data-ttu-id="bacf8-171">Sur hello **attributs du jeton SAML** boîte de dialogue, pour chaque ligne de la table hello ci-dessous, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bacf8-171">On hello **SAML token attributes** dialog, for each row shown in hello table below, perform hello following steps:</span></span>
 
    | <span data-ttu-id="bacf8-172">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="bacf8-172">Attribute Name</span></span> | <span data-ttu-id="bacf8-173">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="bacf8-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="bacf8-174">User.Email</span><span class="sxs-lookup"><span data-stu-id="bacf8-174">User.Email</span></span> | <span data-ttu-id="bacf8-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="bacf8-175">user.mail</span></span> |
    | <span data-ttu-id="bacf8-176">User.FirstName</span><span class="sxs-lookup"><span data-stu-id="bacf8-176">User.FirstName</span></span> | <span data-ttu-id="bacf8-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="bacf8-177">user.givenname</span></span> |
    | <span data-ttu-id="bacf8-178">User.LastName</span><span class="sxs-lookup"><span data-stu-id="bacf8-178">User.LastName</span></span> | <span data-ttu-id="bacf8-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="bacf8-179">user.surname</span></span> |

    <span data-ttu-id="bacf8-180">a.</span><span class="sxs-lookup"><span data-stu-id="bacf8-180">a.</span></span> <span data-ttu-id="bacf8-181">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="bacf8-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trello-tutorial/tutorial_officespace_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-trello-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="bacf8-184">b.</span><span class="sxs-lookup"><span data-stu-id="bacf8-184">b.</span></span> <span data-ttu-id="bacf8-185">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="bacf8-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span> 

    <span data-ttu-id="bacf8-186">c.</span><span class="sxs-lookup"><span data-stu-id="bacf8-186">c.</span></span> <span data-ttu-id="bacf8-187">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="bacf8-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="bacf8-188">d.</span><span class="sxs-lookup"><span data-stu-id="bacf8-188">d.</span></span> <span data-ttu-id="bacf8-189">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="bacf8-189">Click **Ok**.</span></span> 
 
7. <span data-ttu-id="bacf8-190">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="bacf8-190">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trello-tutorial/tutorial_trello_certificate.png) 

8. <span data-ttu-id="bacf8-192">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="bacf8-192">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trello-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bacf8-194">Sur hello **Trello Configuration** , cliquez sur **Trello de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="bacf8-194">On hello **Trello Configuration** section, click **Configure Trello** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bacf8-195">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="bacf8-195">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trello-tutorial/tutorial_trello_configure.png) 

9. <span data-ttu-id="bacf8-197">tooget SSO configuré pour votre application, accédez trop[configuration de l’authentification unique d’entreprise Trello](https://trello.com/sso-configuration) page toosend [équipe de support Trello](mailto:support@trello.com) hello **SAML Sign-On URL du Service unique** et attacher hello **certificat (Base64)**.</span><span class="sxs-lookup"><span data-stu-id="bacf8-197">tooget SSO configured for your application, go too[Trello enterprise SSO configuration](https://trello.com/sso-configuration) page toosend [Trello support team](mailto:support@trello.com) hello **SAML Single Sign-On Service URL** and attach hello **Certificate (Base64)**.</span></span>

> [!TIP]
> <span data-ttu-id="bacf8-198">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="bacf8-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bacf8-199">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="bacf8-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bacf8-200">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bacf8-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bacf8-201">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="bacf8-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="bacf8-202">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="bacf8-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="bacf8-204">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bacf8-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bacf8-205">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="bacf8-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bacf8-207">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="bacf8-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bacf8-209">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="bacf8-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bacf8-211">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bacf8-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bacf8-213">a.</span><span class="sxs-lookup"><span data-stu-id="bacf8-213">a.</span></span> <span data-ttu-id="bacf8-214">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bacf8-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bacf8-215">b.</span><span class="sxs-lookup"><span data-stu-id="bacf8-215">b.</span></span> <span data-ttu-id="bacf8-216">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bacf8-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bacf8-217">c.</span><span class="sxs-lookup"><span data-stu-id="bacf8-217">c.</span></span> <span data-ttu-id="bacf8-218">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="bacf8-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bacf8-219">d.</span><span class="sxs-lookup"><span data-stu-id="bacf8-219">d.</span></span> <span data-ttu-id="bacf8-220">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="bacf8-220">Click **Create**.</span></span>
 
### <a name="creating-a-trello-test-user"></a><span data-ttu-id="bacf8-221">Création d’un utilisateur de test Trello</span><span class="sxs-lookup"><span data-stu-id="bacf8-221">Creating a Trello test user</span></span>

<span data-ttu-id="bacf8-222">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Trello.</span><span class="sxs-lookup"><span data-stu-id="bacf8-222">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="bacf8-223">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Trello.</span><span class="sxs-lookup"><span data-stu-id="bacf8-223">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="bacf8-224">Trello prend en charge l’approvisionnement juste-à-temps et un nouveau compte est créé hello première fois que vous vous connectez à partir d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bacf8-224">Trello supports just-in-time provisioning and a new account is created hello first time you sign in from Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bacf8-225">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bacf8-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bacf8-226">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooTrello.</span><span class="sxs-lookup"><span data-stu-id="bacf8-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTrello.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="bacf8-228">**tooassign Britta Simon tooTrello, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bacf8-228">**tooassign Britta Simon tooTrello, perform hello following steps:**</span></span>

1. <span data-ttu-id="bacf8-229">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bacf8-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="bacf8-231">Dans la liste des applications hello, sélectionnez **Trello**.</span><span class="sxs-lookup"><span data-stu-id="bacf8-231">In hello applications list, select **Trello**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trello-tutorial/tutorial_trello_app.png) 

3. <span data-ttu-id="bacf8-233">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="bacf8-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="bacf8-235">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bacf8-235">Click **Add** button.</span></span> <span data-ttu-id="bacf8-236">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="bacf8-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="bacf8-238">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="bacf8-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bacf8-239">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="bacf8-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bacf8-240">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="bacf8-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bacf8-241">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="bacf8-241">Testing single sign-on</span></span>

<span data-ttu-id="bacf8-242">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="bacf8-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="bacf8-243">Lorsque vous cliquez sur mosaïque Trello hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Trello application.</span><span class="sxs-lookup"><span data-stu-id="bacf8-243">When you click hello Trello tile in hello Access Panel, you should get automatically signed-on tooyour Trello application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bacf8-244">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="bacf8-244">Additional resources</span></span>

* [<span data-ttu-id="bacf8-245">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bacf8-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bacf8-246">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="bacf8-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trello-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trello-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trello-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trello-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trello-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trello-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trello-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trello-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trello-tutorial/tutorial_general_203.png

