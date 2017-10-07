---
title: "Didacticiel : Intégration d’Azure Active Directory à Image Relay | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de relais de l’Image."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: baf39e4437b85c2de5b524984ad5ca39badbab63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a><span data-ttu-id="7f543-103">Didacticiel : Intégration d’Azure Active Directory à ImageRelay</span><span class="sxs-lookup"><span data-stu-id="7f543-103">Tutorial: Azure Active Directory integration with Image Relay</span></span>

<span data-ttu-id="7f543-104">Dans ce didacticiel, vous apprendrez comment toointegrate relais Image avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7f543-104">In this tutorial, you learn how toointegrate Image Relay with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7f543-105">Intégration de relais d’Image avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="7f543-105">Integrating Image Relay with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7f543-106">Vous pouvez contrôler dans Azure AD qui a accès tooImage relais</span><span class="sxs-lookup"><span data-stu-id="7f543-106">You can control in Azure AD who has access tooImage Relay</span></span>
- <span data-ttu-id="7f543-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooImage relais (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f543-107">You can enable your users tooautomatically get signed-on tooImage Relay (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7f543-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="7f543-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7f543-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7f543-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f543-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7f543-110">Prerequisites</span></span>

<span data-ttu-id="7f543-111">tooconfigure intégration d’Azure AD avec l’Image de relais, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7f543-111">tooconfigure Azure AD integration with Image Relay, you need hello following items:</span></span>

- <span data-ttu-id="7f543-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f543-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7f543-113">Un abonnement Image Relay pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="7f543-113">An Image Relay single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7f543-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="7f543-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7f543-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="7f543-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7f543-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7f543-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7f543-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7f543-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7f543-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="7f543-118">Scenario description</span></span>
<span data-ttu-id="7f543-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="7f543-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7f543-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="7f543-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7f543-121">Ajout de relais de l’Image à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="7f543-121">Adding Image Relay from hello gallery</span></span>
2. <span data-ttu-id="7f543-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f543-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-image-relay-from-hello-gallery"></a><span data-ttu-id="7f543-123">Ajout de relais de l’Image à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="7f543-123">Adding Image Relay from hello gallery</span></span>
<span data-ttu-id="7f543-124">tooconfigure hello intégration de relais d’Image dans Azure AD, vous devez tooadd relais de l’Image à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="7f543-124">tooconfigure hello integration of Image Relay into Azure AD, you need tooadd Image Relay from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7f543-125">**tooadd relais d’Image à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7f543-125">**tooadd Image Relay from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f543-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="7f543-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7f543-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="7f543-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7f543-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7f543-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="7f543-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7f543-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="7f543-133">Dans la zone de recherche de hello, tapez **Image relais**.</span><span class="sxs-lookup"><span data-stu-id="7f543-133">In hello search box, type **Image Relay**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. <span data-ttu-id="7f543-135">Dans le volet de résultats hello, sélectionnez **Image relais**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7f543-135">In hello results panel, select **Image Relay**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7f543-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f543-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7f543-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Image Relay, en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="7f543-138">In this section, you configure and test Azure AD single sign-on with Image Relay based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7f543-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans l’Image de relais est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f543-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Image Relay is tooa user in Azure AD.</span></span> <span data-ttu-id="7f543-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans l’Image de relais hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="7f543-140">In other words, a link relationship between an Azure AD user and hello related user in Image Relay needs toobe established.</span></span>

<span data-ttu-id="7f543-141">Dans l’Image de relais, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="7f543-141">In Image Relay, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7f543-142">tooconfigure et test Azure AD l’authentification unique avec l’Image de relais, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="7f543-142">tooconfigure and test Azure AD single sign-on with Image Relay, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7f543-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="7f543-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7f543-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7f543-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7f543-145">**[Création d’un utilisateur de test de relais d’Image](#creating-an-image-relay-test-user)**  -toohave un équivalent de Britta Simon de relais d’Image qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7f543-145">**[Creating an Image Relay test user](#creating-an-image-relay-test-user)** - toohave a counterpart of Britta Simon in Image Relay that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7f543-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7f543-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7f543-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="7f543-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7f543-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f543-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7f543-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de relais d’Image.</span><span class="sxs-lookup"><span data-stu-id="7f543-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Image Relay application.</span></span>

<span data-ttu-id="7f543-150">**tooconfigure Azure AD authentification unique avec l’Image de relais, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7f543-150">**tooconfigure Azure AD single sign-on with Image Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f543-151">Bonjour portail Azure, sur hello **Image relais** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="7f543-151">In hello Azure portal, on hello **Image Relay** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="7f543-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7f543-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. <span data-ttu-id="7f543-155">Sur hello **domaine de relais d’Image et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7f543-155">On hello **Image Relay Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    <span data-ttu-id="7f543-157">a.</span><span class="sxs-lookup"><span data-stu-id="7f543-157">a.</span></span> <span data-ttu-id="7f543-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.imagerelay.com/`</span><span class="sxs-lookup"><span data-stu-id="7f543-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.imagerelay.com/`</span></span>

    <span data-ttu-id="7f543-159">b.</span><span class="sxs-lookup"><span data-stu-id="7f543-159">b.</span></span> <span data-ttu-id="7f543-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.imagerelay.com/sso/metadata`</span><span class="sxs-lookup"><span data-stu-id="7f543-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.imagerelay.com/sso/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7f543-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="7f543-161">These values are not real.</span></span> <span data-ttu-id="7f543-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="7f543-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7f543-163">Contact [équipe de support Client de relais d’Image](http://support.imagerelay.com/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="7f543-163">Contact [Image Relay Client support team](http://support.imagerelay.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="7f543-164">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7f543-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. <span data-ttu-id="7f543-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="7f543-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7f543-168">Sur hello **Image relais Configuration** , cliquez sur **configurer le relais Image** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="7f543-168">On hello **Image Relay Configuration** section, click **Configure Image Relay** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7f543-169">Hello de copie **URL du Service de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="7f543-169">Copy hello **Sign-Out Service URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. <span data-ttu-id="7f543-171">Dans une autre fenêtre de navigateur, connectez-vous dans un site d’entreprise tooyour relais de l’Image en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="7f543-171">In another browser window, sign in tooyour Image Relay company site as an administrator.</span></span>

8. <span data-ttu-id="7f543-172">Dans la barre d’outils de hello en haut de hello, cliquez sur hello **utilisateurs et autorisations** la charge de travail.</span><span class="sxs-lookup"><span data-stu-id="7f543-172">In hello toolbar on hello top, click hello **Users & Permissions** workload.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. <span data-ttu-id="7f543-174">Cliquez sur **Créer une nouvelle autorisation**.</span><span class="sxs-lookup"><span data-stu-id="7f543-174">Click **Create New Permission**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. <span data-ttu-id="7f543-176">Bonjour **Single Sign On Settings** la charge de travail, sélectionnez hello **ce groupe peut uniquement se connecter à l’aide de l’authentification unique** case à cocher, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7f543-176">In hello **Single Sign On Settings** workload, select hello **This Group can only sign-in via Single Sign On** check box, and then click **Save**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. <span data-ttu-id="7f543-178">Accédez trop**les paramètres de compte**.</span><span class="sxs-lookup"><span data-stu-id="7f543-178">Go too**Account Settings**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. <span data-ttu-id="7f543-180">Accédez toohello **Single Sign On Settings** la charge de travail.</span><span class="sxs-lookup"><span data-stu-id="7f543-180">Go toohello **Single Sign On Settings** workload.</span></span>
    
     ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. <span data-ttu-id="7f543-182">Sur hello **paramètres SAML** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7f543-182">On hello **SAML Settings** dialog, perform hello following steps:</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    <span data-ttu-id="7f543-184">a.</span><span class="sxs-lookup"><span data-stu-id="7f543-184">a.</span></span> <span data-ttu-id="7f543-185">Dans **URL de connexion** zone de texte, valeur hello coller **-Service URL d’authentification** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7f543-185">In **Login URL** textbox, paste hello value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7f543-186">b.</span><span class="sxs-lookup"><span data-stu-id="7f543-186">b.</span></span> <span data-ttu-id="7f543-187">Dans **URL de déconnexion** zone de texte, valeur hello coller **URL de Service de déconnexion unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7f543-187">In **Logout URL**  textbox, paste hello value of **Single Sign-Out Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7f543-188">c.</span><span class="sxs-lookup"><span data-stu-id="7f543-188">c.</span></span> <span data-ttu-id="7f543-189">Sous **Name Id Format** (Format d’ID de nom), sélectionnez **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="7f543-189">As **Name Id Format**, select **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="7f543-190">d.</span><span class="sxs-lookup"><span data-stu-id="7f543-190">d.</span></span> <span data-ttu-id="7f543-191">En tant que **les Options de liaison pour les demandes de hello fournisseur de services (Image relais)**, sélectionnez **POST liaison**.</span><span class="sxs-lookup"><span data-stu-id="7f543-191">As **Binding Options for Requests from hello Service Provider (Image Relay)**, select **POST Binding**.</span></span>

    <span data-ttu-id="7f543-192">e.</span><span class="sxs-lookup"><span data-stu-id="7f543-192">e.</span></span> <span data-ttu-id="7f543-193">Sous **Certificat x.509**, cliquez sur **Mettre à jour le certificat**.</span><span class="sxs-lookup"><span data-stu-id="7f543-193">Under **x.509 Certificate**, click **Update Certificate**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    <span data-ttu-id="7f543-195">f.</span><span class="sxs-lookup"><span data-stu-id="7f543-195">f.</span></span> <span data-ttu-id="7f543-196">Ouvrir le certificat de hello téléchargé dans le bloc-notes, copier le contenu de hello, puis collez-la dans la zone de texte hello x.509 certificat.</span><span class="sxs-lookup"><span data-stu-id="7f543-196">Open hello downloaded certificate in notepad, copy hello content, and then paste it into hello x.509 Certificate textbox.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    <span data-ttu-id="7f543-198">g.</span><span class="sxs-lookup"><span data-stu-id="7f543-198">g.</span></span> <span data-ttu-id="7f543-199">Dans **juste à temps de configuration de l’utilisateur** section, sélectionnez hello **activer l’approvisionnement des utilisateurs juste à temps**.</span><span class="sxs-lookup"><span data-stu-id="7f543-199">In **Just-In-Time User Provisioning** section, select hello **Enable Just-In-Time User Provisioning**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    <span data-ttu-id="7f543-201">h.</span><span class="sxs-lookup"><span data-stu-id="7f543-201">h.</span></span> <span data-ttu-id="7f543-202">Groupe d’autorisations SELECT hello (par exemple, **base SSO**) qui n’est autorisé toosign dans via l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7f543-202">Select hello permission group (for example, **SSO Basic**) which is allowed toosign in only through single sign-on.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    <span data-ttu-id="7f543-204">i.</span><span class="sxs-lookup"><span data-stu-id="7f543-204">i.</span></span> <span data-ttu-id="7f543-205">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7f543-205">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7f543-206">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="7f543-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7f543-207">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="7f543-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7f543-208">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7f543-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7f543-209">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f543-209">Creating an Azure AD test user</span></span>
<span data-ttu-id="7f543-210">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="7f543-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="7f543-212">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7f543-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f543-213">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="7f543-213">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7f543-215">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="7f543-215">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7f543-217">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="7f543-217">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7f543-219">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7f543-219">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7f543-221">a.</span><span class="sxs-lookup"><span data-stu-id="7f543-221">a.</span></span> <span data-ttu-id="7f543-222">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7f543-222">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7f543-223">b.</span><span class="sxs-lookup"><span data-stu-id="7f543-223">b.</span></span> <span data-ttu-id="7f543-224">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7f543-224">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7f543-225">c.</span><span class="sxs-lookup"><span data-stu-id="7f543-225">c.</span></span> <span data-ttu-id="7f543-226">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="7f543-226">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7f543-227">d.</span><span class="sxs-lookup"><span data-stu-id="7f543-227">d.</span></span> <span data-ttu-id="7f543-228">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="7f543-228">Click **Create**.</span></span>
 
### <a name="creating-an-image-relay-test-user"></a><span data-ttu-id="7f543-229">Création d’un utilisateur de test Image Relay</span><span class="sxs-lookup"><span data-stu-id="7f543-229">Creating an Image Relay test user</span></span>

<span data-ttu-id="7f543-230">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans l’Image de relais.</span><span class="sxs-lookup"><span data-stu-id="7f543-230">hello objective of this section is toocreate a user called Britta Simon in Image Relay.</span></span>

<span data-ttu-id="7f543-231">**toocreate un utilisateur appelé Britta Simon dans l’Image de relais, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7f543-231">**toocreate a user called Britta Simon in Image Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f543-232">Site d’entreprise tooyour authentification relais de l’Image en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="7f543-232">Sign-on tooyour Image Relay company site as an administrator.</span></span>

2. <span data-ttu-id="7f543-233">Accédez trop**utilisateurs et autorisations** et sélectionnez **créer un utilisateur SSO**.</span><span class="sxs-lookup"><span data-stu-id="7f543-233">Go too**Users & Permissions**     and select **Create SSO User**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. <span data-ttu-id="7f543-235">Entrez hello **messagerie**, **prénom**, **nom**, et **société** d’utilisateur de hello souhaité tooprovision et le groupe d’autorisations select hello (par exemple, l’authentification unique de base) qui est le groupe hello qui peut se connecter via l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7f543-235">Enter hello **Email**, **First Name**, **Last Name**, and **Company** of hello user you want tooprovision and select hello permission group (for example, SSO Basic) which is hello group that can sign in only through single sign-on.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. <span data-ttu-id="7f543-237">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="7f543-237">Click **Create**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7f543-238">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f543-238">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7f543-239">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooImage relais.</span><span class="sxs-lookup"><span data-stu-id="7f543-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooImage Relay.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="7f543-241">**tooassign Britta Simon tooImage relais, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7f543-241">**tooassign Britta Simon tooImage Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f543-242">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7f543-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="7f543-244">Dans la liste des applications hello, sélectionnez **Image relais**.</span><span class="sxs-lookup"><span data-stu-id="7f543-244">In hello applications list, select **Image Relay**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. <span data-ttu-id="7f543-246">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7f543-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="7f543-248">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7f543-248">Click **Add** button.</span></span> <span data-ttu-id="7f543-249">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7f543-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="7f543-251">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="7f543-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7f543-252">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7f543-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7f543-253">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7f543-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7f543-254">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="7f543-254">Testing single sign-on</span></span>

<span data-ttu-id="7f543-255">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="7f543-255">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>    

<span data-ttu-id="7f543-256">Lorsque vous cliquez sur hello relais de l’Image de vignette dans hello volet d’accès, vous devez obtenir l’application d’Image relais automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="7f543-256">When you click hello Image Relay tile in hello Access Panel, you should get automatically signed-on tooyour Image Relay application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7f543-257">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7f543-257">Additional resources</span></span>

* [<span data-ttu-id="7f543-258">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7f543-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7f543-259">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="7f543-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png

