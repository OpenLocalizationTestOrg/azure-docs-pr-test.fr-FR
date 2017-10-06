---
title: "Didacticiel : Intégration d’Azure Active Directory à BlueJeans | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de BlueJeans."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: jeedes
ms.openlocfilehash: 67613303a9f854afbf4619418cc1607d329caf94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a><span data-ttu-id="d5efd-103">Didacticiel : Intégration d’Azure Active Directory à BlueJeans</span><span class="sxs-lookup"><span data-stu-id="d5efd-103">Tutorial: Azure Active Directory integration with BlueJeans</span></span>

<span data-ttu-id="d5efd-104">Dans ce didacticiel, vous apprendrez comment toointegrate BlueJeans avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d5efd-104">In this tutorial, you learn how toointegrate BlueJeans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d5efd-105">Intégration de BlueJeans avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="d5efd-105">Integrating BlueJeans with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d5efd-106">Vous pouvez contrôler dans Azure AD qui a accès tooBlueJeans</span><span class="sxs-lookup"><span data-stu-id="d5efd-106">You can control in Azure AD who has access tooBlueJeans</span></span>
- <span data-ttu-id="d5efd-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooBlueJeans (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5efd-107">You can enable your users tooautomatically get signed-on tooBlueJeans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d5efd-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="d5efd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d5efd-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d5efd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5efd-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d5efd-110">Prerequisites</span></span>

<span data-ttu-id="d5efd-111">tooconfigure intégration d’Azure AD à BlueJeans, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d5efd-111">tooconfigure Azure AD integration with BlueJeans, you need hello following items:</span></span>

- <span data-ttu-id="d5efd-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5efd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d5efd-113">Un abonnement BlueJeans pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="d5efd-113">A BlueJeans single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d5efd-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="d5efd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d5efd-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="d5efd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d5efd-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d5efd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d5efd-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d5efd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d5efd-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="d5efd-118">Scenario description</span></span>
<span data-ttu-id="d5efd-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="d5efd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d5efd-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="d5efd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d5efd-121">Ajout de BlueJeans à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="d5efd-121">Adding BlueJeans from hello gallery</span></span>
2. <span data-ttu-id="d5efd-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5efd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bluejeans-from-hello-gallery"></a><span data-ttu-id="d5efd-123">Ajout de BlueJeans à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="d5efd-123">Adding BlueJeans from hello gallery</span></span>
<span data-ttu-id="d5efd-124">intégration de hello tooconfigure de BlueJeans dans Azure AD, vous devez tooadd BlueJeans à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="d5efd-124">tooconfigure hello integration of BlueJeans into Azure AD, you need tooadd BlueJeans from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d5efd-125">**tooadd BlueJeans à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d5efd-125">**tooadd BlueJeans from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5efd-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="d5efd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d5efd-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="d5efd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d5efd-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d5efd-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="d5efd-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d5efd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="d5efd-133">Dans la zone de recherche de hello, tapez **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="d5efd-133">In hello search box, type **BlueJeans**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_search.png)

5. <span data-ttu-id="d5efd-135">Dans le volet de résultats hello, sélectionnez **BlueJeans**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d5efd-135">In hello results panel, select **BlueJeans**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d5efd-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5efd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d5efd-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec BlueJeans avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="d5efd-138">In this section, you configure and test Azure AD single sign-on with BlueJeans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d5efd-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans BlueJeans est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d5efd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BlueJeans is tooa user in Azure AD.</span></span> <span data-ttu-id="d5efd-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans BlueJeans doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="d5efd-140">In other words, a link relationship between an Azure AD user and hello related user in BlueJeans needs toobe established.</span></span>

<span data-ttu-id="d5efd-141">En l’occurrence, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="d5efd-141">In BlueJeans, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d5efd-142">tooconfigure et test Azure AD l’authentification unique à BlueJeans, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="d5efd-142">tooconfigure and test Azure AD single sign-on with BlueJeans, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d5efd-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d5efd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d5efd-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d5efd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d5efd-145">**[Création d’un utilisateur de test de BlueJeans](#creating-a-bluejeans-test-user)**  -toohave un équivalent de Britta Simon dans BlueJeans qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d5efd-145">**[Creating a BlueJeans test user](#creating-a-bluejeans-test-user)** - toohave a counterpart of Britta Simon in BlueJeans that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d5efd-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d5efd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d5efd-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="d5efd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d5efd-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5efd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d5efd-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="d5efd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BlueJeans application.</span></span>

<span data-ttu-id="d5efd-150">**tooconfigure Azure AD single sign-on avec BlueJeans, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d5efd-150">**tooconfigure Azure AD single sign-on with BlueJeans, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5efd-151">Bonjour portail Azure, sur hello **BlueJeans** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="d5efd-151">In hello Azure portal, on hello **BlueJeans** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="d5efd-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d5efd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

3. <span data-ttu-id="d5efd-155">Sur hello **BlueJeans domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d5efd-155">On hello **BlueJeans Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_url.png)

    <span data-ttu-id="d5efd-157">a.</span><span class="sxs-lookup"><span data-stu-id="d5efd-157">a.</span></span> <span data-ttu-id="d5efd-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="d5efd-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    <span data-ttu-id="d5efd-159">b.</span><span class="sxs-lookup"><span data-stu-id="d5efd-159">b.</span></span> <span data-ttu-id="d5efd-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="d5efd-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d5efd-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="d5efd-161">These values are not real.</span></span> <span data-ttu-id="d5efd-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="d5efd-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d5efd-163">Contact [équipe de support Client de BlueJeans](https://support.bluejeans.com/contact) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="d5efd-163">Contact [BlueJeans Client support team](https://support.bluejeans.com/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="d5efd-164">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d5efd-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

5. <span data-ttu-id="d5efd-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="d5efd-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bluejeans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d5efd-168">Sur hello **BlueJeans Configuration** , cliquez sur **configurer de BlueJeans** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="d5efd-168">On hello **BlueJeans Configuration** section, click **Configure BlueJeans** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d5efd-169">Hello de copie **URL de déconnexion, URL de modification du mot de passe et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="d5efd-169">Copy hello **Sign-Out URL, Change Password URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_configure.png) 

7. <span data-ttu-id="d5efd-171">Dans une fenêtre de navigateur web, connectez-vous tooyour **BlueJeans** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d5efd-171">In a different web browser window, log in tooyour **BlueJeans** company site as an administrator.</span></span>

8. <span data-ttu-id="d5efd-172">Accédez trop**ADMIN \> les paramètres de groupe \> sécurité**.</span><span class="sxs-lookup"><span data-stu-id="d5efd-172">Go too**ADMIN \> Group Settings \> Security**.</span></span>
   
   <span data-ttu-id="d5efd-173">![Administrateur](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="d5efd-173">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")</span></span>

9. <span data-ttu-id="d5efd-174">Bonjour **sécurité** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d5efd-174">In hello **Security** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="d5efd-175">![Authentification unique SAML](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "Authentification unique SAML")</span><span class="sxs-lookup"><span data-stu-id="d5efd-175">![SAML Single Sign On](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML Single Sign On")</span></span>   
   
   <span data-ttu-id="d5efd-176">a.</span><span class="sxs-lookup"><span data-stu-id="d5efd-176">a.</span></span> <span data-ttu-id="d5efd-177">Sélectionnez **SAML Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="d5efd-177">Select **SAML Single Sign On**.</span></span>
  
   <span data-ttu-id="d5efd-178">b.</span><span class="sxs-lookup"><span data-stu-id="d5efd-178">b.</span></span> <span data-ttu-id="d5efd-179">Sélectionnez **Enable automatic provisioning**.</span><span class="sxs-lookup"><span data-stu-id="d5efd-179">Select **Enable automatic provisioning**.</span></span>

10. <span data-ttu-id="d5efd-180">Poursuivez en hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d5efd-180">Move on with hello following steps:</span></span>

    <span data-ttu-id="d5efd-181">![Chemin d’accès du certificat](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Chemin d’accès du certificat")</span><span class="sxs-lookup"><span data-stu-id="d5efd-181">![Certificate Path](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Certificate Path")</span></span>
    
    <span data-ttu-id="d5efd-182">a.</span><span class="sxs-lookup"><span data-stu-id="d5efd-182">a.</span></span> <span data-ttu-id="d5efd-183">Cliquez sur **choisir un fichier**, puis téléchargez le certificat de hello téléchargé.</span><span class="sxs-lookup"><span data-stu-id="d5efd-183">Click **Choose File**, and then upload hello downloaded certificate.</span></span>
   
    <span data-ttu-id="d5efd-184">b.</span><span class="sxs-lookup"><span data-stu-id="d5efd-184">b.</span></span> <span data-ttu-id="d5efd-185">Coller **SAML Sign-On URL du Service unique** dans hello **URL de connexion** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="d5efd-185">Paste **SAML Single Sign-On Service URL** into hello **Login URL** textbox.</span></span>
   
    <span data-ttu-id="d5efd-186">c.</span><span class="sxs-lookup"><span data-stu-id="d5efd-186">c.</span></span> <span data-ttu-id="d5efd-187">Coller **URL de modification du mot de passe** dans hello **URL de modification du mot de passe** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="d5efd-187">Paste **Change Password URL** into hello **Password Change URL** textbox.</span></span>
   
    <span data-ttu-id="d5efd-188">d.</span><span class="sxs-lookup"><span data-stu-id="d5efd-188">d.</span></span> <span data-ttu-id="d5efd-189">Coller **URL de déconnexion** dans hello **URL de déconnexion** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="d5efd-189">Paste **Sign-Out URL** into hello **Logout URL** textbox.</span></span>

11. <span data-ttu-id="d5efd-190">Poursuivez en hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d5efd-190">Move on with hello following steps:</span></span>
    
    <span data-ttu-id="d5efd-191">![Enregistrer les modifications](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Enregistrer les modifications")</span><span class="sxs-lookup"><span data-stu-id="d5efd-191">![Save Changes](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Save Changes")</span></span>
    
    <span data-ttu-id="d5efd-192">a.</span><span class="sxs-lookup"><span data-stu-id="d5efd-192">a.</span></span> <span data-ttu-id="d5efd-193">Bonjour **id utilisateur** zone de texte, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="d5efd-193">In hello **User id** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="d5efd-194">b.</span><span class="sxs-lookup"><span data-stu-id="d5efd-194">b.</span></span> <span data-ttu-id="d5efd-195">Bonjour **messagerie** zone de texte, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="d5efd-195">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="d5efd-196">c.</span><span class="sxs-lookup"><span data-stu-id="d5efd-196">c.</span></span> <span data-ttu-id="d5efd-197">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="d5efd-197">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="d5efd-198">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="d5efd-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d5efd-199">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="d5efd-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d5efd-200">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d5efd-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d5efd-201">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5efd-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="d5efd-202">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="d5efd-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="d5efd-204">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d5efd-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5efd-205">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="d5efd-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d5efd-207">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d5efd-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d5efd-209">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="d5efd-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d5efd-211">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d5efd-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d5efd-213">a.</span><span class="sxs-lookup"><span data-stu-id="d5efd-213">a.</span></span> <span data-ttu-id="d5efd-214">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d5efd-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d5efd-215">b.</span><span class="sxs-lookup"><span data-stu-id="d5efd-215">b.</span></span> <span data-ttu-id="d5efd-216">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d5efd-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d5efd-217">c.</span><span class="sxs-lookup"><span data-stu-id="d5efd-217">c.</span></span> <span data-ttu-id="d5efd-218">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="d5efd-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d5efd-219">d.</span><span class="sxs-lookup"><span data-stu-id="d5efd-219">d.</span></span> <span data-ttu-id="d5efd-220">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="d5efd-220">Click **Create**.</span></span>
 
### <a name="creating-a-bluejeans-test-user"></a><span data-ttu-id="d5efd-221">Création d’un utilisateur de test BlueJeans</span><span class="sxs-lookup"><span data-stu-id="d5efd-221">Creating a BlueJeans test user</span></span>

<span data-ttu-id="d5efd-222">tooenable Azure AD les utilisateurs toolog dans tooBlueJeans, vous devez les configurer dans BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="d5efd-222">tooenable Azure AD users toolog in tooBlueJeans, they must be provisioned into BlueJeans.</span></span>  

<span data-ttu-id="d5efd-223">Pour BlueJeans, cet approvisionnement doit se faire manuellement.</span><span class="sxs-lookup"><span data-stu-id="d5efd-223">In case of BlueJeans, provisioning is a manual task.</span></span>

<span data-ttu-id="d5efd-224">**effectuer des comptes d’utilisateur, tooprovision hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d5efd-224">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5efd-225">Connectez-vous à tooyour **BlueJeans** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d5efd-225">Log in tooyour **BlueJeans** company site as an administrator.</span></span>

2. <span data-ttu-id="d5efd-226">Accédez trop**ADMIN \> gérer les utilisateurs \> ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="d5efd-226">Go too**ADMIN \> Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="d5efd-227">![Administrateur](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="d5efd-227">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")</span></span>
   
   >[!IMPORTANT]
   ><span data-ttu-id="d5efd-228">Hello **ajouter un utilisateur** onglet est disponible uniquement en cas, de hello **onglet sécurité**, **activer l’approvisionnement automatique** est désactivée.</span><span class="sxs-lookup"><span data-stu-id="d5efd-228">hello **Add User** tab is only available if, in hello **Security tab**, **Enable automatic provisioning** is unchecked.</span></span> 
   
3. <span data-ttu-id="d5efd-229">Bonjour **ajouter un utilisateur** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d5efd-229">In hello **Add User** section, perform hello following steps:</span></span>

    <span data-ttu-id="d5efd-230">![Ajouter un utilisateur](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="d5efd-230">![Add User](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Add User")</span></span>
    
    <span data-ttu-id="d5efd-231">a.</span><span class="sxs-lookup"><span data-stu-id="d5efd-231">a.</span></span> <span data-ttu-id="d5efd-232">Tapez un **BlueJeans Username**, un **adresse de messagerie**, un **BlueJeans Meeting ID**, un **Moderator code**, un **nom complet** , hello **société** d’un compte AAD valide que vous voulez tooprovision dans hello relatives des zones de texte.</span><span class="sxs-lookup"><span data-stu-id="d5efd-232">Type a **BlueJeans Username**, an **Email address**, a **BlueJeans Meeting ID**, a **Moderator Passcode**, a **Full Name**, hello **Company** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
    
    <span data-ttu-id="d5efd-233">b.</span><span class="sxs-lookup"><span data-stu-id="d5efd-233">b.</span></span> <span data-ttu-id="d5efd-234">Cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="d5efd-234">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="d5efd-235">Vous pouvez utiliser n’importe quel autre occurrence utilisateur compte outil de création ou API fournie par BlueJeans tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="d5efd-235">You can use any other BlueJeans user account creation tools or APIs provided by BlueJeans tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d5efd-236">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5efd-236">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d5efd-237">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooBlueJeans.</span><span class="sxs-lookup"><span data-stu-id="d5efd-237">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlueJeans.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="d5efd-239">**tooassign Britta Simon tooBlueJeans, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d5efd-239">**tooassign Britta Simon tooBlueJeans, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5efd-240">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d5efd-240">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="d5efd-242">Dans la liste des applications hello, sélectionnez **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="d5efd-242">In hello applications list, select **BlueJeans**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_app.png) 

3. <span data-ttu-id="d5efd-244">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d5efd-244">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="d5efd-246">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d5efd-246">Click **Add** button.</span></span> <span data-ttu-id="d5efd-247">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d5efd-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="d5efd-249">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="d5efd-249">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d5efd-250">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d5efd-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d5efd-251">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d5efd-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d5efd-252">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d5efd-252">Testing single sign-on</span></span>

<span data-ttu-id="d5efd-253">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="d5efd-253">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d5efd-254">Lorsque vous cliquez sur hello BlueJeans vignette Bonjour volet d’accès, vous devez obtenir la page de connexion de l’application de BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="d5efd-254">When you click hello BlueJeans tile in hello Access Panel, you should get login page of BlueJeans application.</span></span>
<span data-ttu-id="d5efd-255">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d5efd-255">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d5efd-256">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d5efd-256">Additional resources</span></span>

* [<span data-ttu-id="d5efd-257">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5efd-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d5efd-258">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="d5efd-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_203.png

