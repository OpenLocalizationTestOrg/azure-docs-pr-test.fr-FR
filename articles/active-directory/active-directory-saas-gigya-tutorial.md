---
title: "Didacticiel : Intégration d’Azure Active Directory à Gigya | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Gigya."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2c7d200b-9242-44a5-ac8a-ab3214a78e41
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 1992c5ad09b097563377a488fbf5a375f6511020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gigya"></a><span data-ttu-id="5d088-103">Didacticiel : Intégration d’Azure Active Directory à Gigya</span><span class="sxs-lookup"><span data-stu-id="5d088-103">Tutorial: Azure Active Directory integration with Gigya</span></span>

<span data-ttu-id="5d088-104">Dans ce didacticiel, vous apprendrez comment toointegrate Gigya avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5d088-104">In this tutorial, you learn how toointegrate Gigya with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5d088-105">Intégration de Gigya à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5d088-105">Integrating Gigya with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5d088-106">Vous pouvez contrôler dans Azure AD qui a accès tooGigya</span><span class="sxs-lookup"><span data-stu-id="5d088-106">You can control in Azure AD who has access tooGigya</span></span>
- <span data-ttu-id="5d088-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooGigya (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d088-107">You can enable your users tooautomatically get signed-on tooGigya (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5d088-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="5d088-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5d088-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5d088-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d088-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5d088-110">Prerequisites</span></span>

<span data-ttu-id="5d088-111">tooconfigure intégration d’Azure AD à Gigya, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5d088-111">tooconfigure Azure AD integration with Gigya, you need hello following items:</span></span>

- <span data-ttu-id="5d088-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d088-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5d088-113">Un abonnement Gigya pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5d088-113">A Gigya single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5d088-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5d088-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5d088-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="5d088-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5d088-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5d088-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5d088-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5d088-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5d088-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5d088-118">Scenario description</span></span>
<span data-ttu-id="5d088-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5d088-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5d088-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="5d088-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5d088-121">Ajout de Gigya à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5d088-121">Adding Gigya from hello gallery</span></span>
2. <span data-ttu-id="5d088-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d088-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gigya-from-hello-gallery"></a><span data-ttu-id="5d088-123">Ajout de Gigya à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5d088-123">Adding Gigya from hello gallery</span></span>
<span data-ttu-id="5d088-124">intégration de hello tooconfigure de Gigya dans Azure AD, vous devez tooadd Gigya à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="5d088-124">tooconfigure hello integration of Gigya into Azure AD, you need tooadd Gigya from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5d088-125">**tooadd Gigya à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5d088-125">**tooadd Gigya from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d088-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="5d088-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5d088-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5d088-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5d088-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5d088-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="5d088-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5d088-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="5d088-133">Dans la zone de recherche de hello, tapez **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="5d088-133">In hello search box, type **Gigya**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_search.png)

5. <span data-ttu-id="5d088-135">Dans le volet de résultats hello, sélectionnez **Gigya**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5d088-135">In hello results panel, select **Gigya**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5d088-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d088-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5d088-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Gigya à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5d088-138">In this section, you configure and test Azure AD single sign-on with Gigya based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5d088-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Gigya est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d088-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Gigya is tooa user in Azure AD.</span></span> <span data-ttu-id="5d088-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Gigya doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="5d088-140">In other words, a link relationship between an Azure AD user and hello related user in Gigya needs toobe established.</span></span>

<span data-ttu-id="5d088-141">Dans Gigya, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="5d088-141">In Gigya, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5d088-142">tooconfigure et test Azure AD l’authentification unique avec Gigya, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="5d088-142">tooconfigure and test Azure AD single sign-on with Gigya, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5d088-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5d088-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5d088-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5d088-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5d088-145">**[Création d’un utilisateur de test de Gigya](#creating-a-gigya-test-user)**  -toohave un équivalent de Britta Simon dans Gigya est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5d088-145">**[Creating a Gigya test user](#creating-a-gigya-test-user)** - toohave a counterpart of Britta Simon in Gigya that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5d088-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5d088-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5d088-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="5d088-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5d088-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d088-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5d088-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Gigya.</span><span class="sxs-lookup"><span data-stu-id="5d088-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Gigya application.</span></span>

<span data-ttu-id="5d088-150">**tooconfigure Azure AD single sign-on avec Gigya, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5d088-150">**tooconfigure Azure AD single sign-on with Gigya, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d088-151">Bonjour portail Azure, sur hello **Gigya** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5d088-151">In hello Azure portal, on hello **Gigya** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="5d088-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5d088-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_samlbase.png)

3. <span data-ttu-id="5d088-155">Sur hello **Gigya domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5d088-155">On hello **Gigya Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_url.png)

    <span data-ttu-id="5d088-157">a.</span><span class="sxs-lookup"><span data-stu-id="5d088-157">a.</span></span> <span data-ttu-id="5d088-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`http://<companyname>.gigya.com`</span><span class="sxs-lookup"><span data-stu-id="5d088-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<companyname>.gigya.com`</span></span>

    <span data-ttu-id="5d088-159">b.</span><span class="sxs-lookup"><span data-stu-id="5d088-159">b.</span></span> <span data-ttu-id="5d088-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://fidm.gigya.com/saml/v2.0/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="5d088-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://fidm.gigya.com/saml/v2.0/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5d088-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="5d088-161">These values are not real.</span></span> <span data-ttu-id="5d088-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="5d088-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5d088-163">Contact [équipe de support Client de Gigya](https://www.gigya.com/support-policy/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="5d088-163">Contact [Gigya Client support team](https://www.gigya.com/support-policy/) tooget these values.</span></span> 
 
4. <span data-ttu-id="5d088-164">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5d088-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_certificate.png) 

5. <span data-ttu-id="5d088-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="5d088-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-gigya-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5d088-168">Sur hello **Gigya Configuration** , cliquez sur **configurer de Gigya** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="5d088-168">On hello **Gigya Configuration** section, click **Configure Gigya** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5d088-169">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="5d088-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_configure.png) 

7. <span data-ttu-id="5d088-171">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Gigya en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5d088-171">In a different web browser window, log into your Gigya company site as an administrator.</span></span>

8. <span data-ttu-id="5d088-172">Accédez trop**paramètres \> connexion SAML**, puis cliquez sur hello **ajouter** bouton.</span><span class="sxs-lookup"><span data-stu-id="5d088-172">Go too**Settings \> SAML Login**, and then click hello **Add** button.</span></span>
   
    <span data-ttu-id="5d088-173">![Connexion SAML](./media/active-directory-saas-gigya-tutorial/ic789532.png "Connexion SAML")</span><span class="sxs-lookup"><span data-stu-id="5d088-173">![SAML Login](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML Login")</span></span>

9. <span data-ttu-id="5d088-174">Bonjour **connexion SAML** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5d088-174">In hello **SAML Login** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="5d088-175">![Configuration SAML](./media/active-directory-saas-gigya-tutorial/ic789533.png "Configuration SAML")</span><span class="sxs-lookup"><span data-stu-id="5d088-175">![SAML Configuration](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML Configuration")</span></span>
   
    <span data-ttu-id="5d088-176">a.</span><span class="sxs-lookup"><span data-stu-id="5d088-176">a.</span></span> <span data-ttu-id="5d088-177">Bonjour **nom** zone de texte, tapez un nom pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="5d088-177">In hello **Name** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="5d088-178">b.</span><span class="sxs-lookup"><span data-stu-id="5d088-178">b.</span></span> <span data-ttu-id="5d088-179">Dans **émetteur** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5d088-179">In **Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure Portal.</span></span> 
   
    <span data-ttu-id="5d088-180">c.</span><span class="sxs-lookup"><span data-stu-id="5d088-180">c.</span></span> <span data-ttu-id="5d088-181">Dans **unique Sign-On URL du Service** zone de texte, valeur hello coller **-Service URL d’authentification** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5d088-181">In **Single Sign-On Service URL** textbox, paste hello value of **Single Sign-On Service URL** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="5d088-182">d.</span><span class="sxs-lookup"><span data-stu-id="5d088-182">d.</span></span> <span data-ttu-id="5d088-183">Dans **Format d’ID de nom** zone de texte, valeur hello coller **Name Identifier Format** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5d088-183">In **Name ID Format** textbox, paste hello value of **Name Identifier Format** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="5d088-184">e.</span><span class="sxs-lookup"><span data-stu-id="5d088-184">e.</span></span> <span data-ttu-id="5d088-185">Ouvrez votre certificat codé en base 64 dans le bloc-notes téléchargé à partir du portail Azure, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat X.509** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="5d088-185">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="5d088-186">f.</span><span class="sxs-lookup"><span data-stu-id="5d088-186">f.</span></span> <span data-ttu-id="5d088-187">Cliquez sur **Save Settings**.</span><span class="sxs-lookup"><span data-stu-id="5d088-187">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="5d088-188">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="5d088-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5d088-189">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="5d088-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5d088-190">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5d088-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5d088-191">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d088-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="5d088-192">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="5d088-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="5d088-194">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5d088-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d088-195">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="5d088-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5d088-197">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5d088-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5d088-199">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="5d088-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5d088-201">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5d088-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5d088-203">a.</span><span class="sxs-lookup"><span data-stu-id="5d088-203">a.</span></span> <span data-ttu-id="5d088-204">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5d088-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5d088-205">b.</span><span class="sxs-lookup"><span data-stu-id="5d088-205">b.</span></span> <span data-ttu-id="5d088-206">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5d088-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5d088-207">c.</span><span class="sxs-lookup"><span data-stu-id="5d088-207">c.</span></span> <span data-ttu-id="5d088-208">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5d088-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5d088-209">d.</span><span class="sxs-lookup"><span data-stu-id="5d088-209">d.</span></span> <span data-ttu-id="5d088-210">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5d088-210">Click **Create**.</span></span>
 
### <a name="creating-a-gigya-test-user"></a><span data-ttu-id="5d088-211">Création d’un utilisateur de test Gigya</span><span class="sxs-lookup"><span data-stu-id="5d088-211">Creating a Gigya test user</span></span>

<span data-ttu-id="5d088-212">Dans l’ordre tooenable Azure AD les utilisateurs toolog à Gigya, vous devez les configurer dans Gigya.</span><span class="sxs-lookup"><span data-stu-id="5d088-212">In order tooenable Azure AD users toolog into Gigya, they must be provisioned into Gigya.</span></span>  
<span data-ttu-id="5d088-213">Dans les cas de hello de Gigya, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="5d088-213">In hello case of Gigya, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="5d088-214">effectuer des comptes d’utilisateur, tooprovision hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5d088-214">tooprovision a user accounts, perform hello following steps:</span></span>

1. <span data-ttu-id="5d088-215">Connectez-vous à tooyour **Gigya** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5d088-215">Log in tooyour **Gigya** company site as an administrator.</span></span>

2. <span data-ttu-id="5d088-216">Accédez trop**Admin \> gérer les utilisateurs**, puis cliquez sur **inviter des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5d088-216">Go too**Admin \> Manage Users**, and then click **Invite Users**.</span></span>
   
    <span data-ttu-id="5d088-217">![Gestion des utilisateurs](./media/active-directory-saas-gigya-tutorial/ic789535.png "Gestion des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="5d088-217">![Manage Users](./media/active-directory-saas-gigya-tutorial/ic789535.png "Manage Users")</span></span>

3. <span data-ttu-id="5d088-218">Dans la boîte de dialogue inviter des utilisateurs hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5d088-218">On hello Invite Users dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="5d088-219">![Inviter des utilisateurs](./media/active-directory-saas-gigya-tutorial/ic789536.png "inviter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="5d088-219">![Invite Users](./media/active-directory-saas-gigya-tutorial/ic789536.png "Invite Users")</span></span>
   
    <span data-ttu-id="5d088-220">a.</span><span class="sxs-lookup"><span data-stu-id="5d088-220">a.</span></span> <span data-ttu-id="5d088-221">Bonjour **messagerie** zone de texte, les alias de messagerie de type hello d’un compte Azure Active Directory valide que vous souhaitez tooprovision.</span><span class="sxs-lookup"><span data-stu-id="5d088-221">In hello **Email** textbox, type hello email alias of a valid Azure Active Directory account you want tooprovision.</span></span>
    
    <span data-ttu-id="5d088-222">b.</span><span class="sxs-lookup"><span data-stu-id="5d088-222">b.</span></span> <span data-ttu-id="5d088-223">Cliquez sur **Invite User**.</span><span class="sxs-lookup"><span data-stu-id="5d088-223">Click **Invite User**.</span></span>
      
    > [!NOTE]
    > <span data-ttu-id="5d088-224">titulaire du compte Azure Active Directory Hello recevra un e-mail contenant un compte de hello tooconfirm lien avant son activation.</span><span class="sxs-lookup"><span data-stu-id="5d088-224">hello Azure Active Directory account holder will receive an email that includes a link tooconfirm hello account before it becomes active.</span></span>
    > 
    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5d088-225">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d088-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5d088-226">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooGigya.</span><span class="sxs-lookup"><span data-stu-id="5d088-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGigya.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="5d088-228">**tooassign Britta Simon tooGigya, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5d088-228">**tooassign Britta Simon tooGigya, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d088-229">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5d088-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5d088-231">Dans la liste des applications hello, sélectionnez **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="5d088-231">In hello applications list, select **Gigya**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_app.png) 

3. <span data-ttu-id="5d088-233">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5d088-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="5d088-235">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5d088-235">Click **Add** button.</span></span> <span data-ttu-id="5d088-236">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5d088-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="5d088-238">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="5d088-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5d088-239">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5d088-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5d088-240">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5d088-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5d088-241">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5d088-241">Testing single sign-on</span></span>

<span data-ttu-id="5d088-242">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="5d088-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="5d088-243">Lorsque vous cliquez sur mosaïque Gigya hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Gigya application.</span><span class="sxs-lookup"><span data-stu-id="5d088-243">When you click hello Gigya tile in hello Access Panel, you should get automatically signed-on tooyour Gigya application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5d088-244">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5d088-244">Additional resources</span></span>

* [<span data-ttu-id="5d088-245">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d088-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5d088-246">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5d088-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_203.png

