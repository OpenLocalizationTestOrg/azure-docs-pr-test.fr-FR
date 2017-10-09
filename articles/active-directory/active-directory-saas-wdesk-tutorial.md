---
title: "Didacticiel : Intégration d’Azure Active Directory à Wdesk | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Wdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 2c278a5e4f50cc362663efc0f826ff0c0fcf6e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a><span data-ttu-id="42d64-103">Didacticiel : Intégration d’Azure Active Directory à Wdesk</span><span class="sxs-lookup"><span data-stu-id="42d64-103">Tutorial: Azure Active Directory integration with Wdesk</span></span>

<span data-ttu-id="42d64-104">Dans ce didacticiel, vous apprendrez comment toointegrate Wdesk avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="42d64-104">In this tutorial, you learn how toointegrate Wdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="42d64-105">Intégration Wdesk à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="42d64-105">Integrating Wdesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="42d64-106">Vous pouvez contrôler dans Azure AD qui a accès tooWdesk</span><span class="sxs-lookup"><span data-stu-id="42d64-106">You can control in Azure AD who has access tooWdesk</span></span>
- <span data-ttu-id="42d64-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooWdesk (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="42d64-107">You can enable your users tooautomatically get signed-on tooWdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="42d64-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="42d64-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="42d64-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez.</span><span class="sxs-lookup"><span data-stu-id="42d64-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="42d64-110">[Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="42d64-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42d64-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="42d64-111">Prerequisites</span></span>

<span data-ttu-id="42d64-112">tooconfigure intégration d’Azure AD avec Wdesk, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="42d64-112">tooconfigure Azure AD integration with Wdesk, you need hello following items:</span></span>

- <span data-ttu-id="42d64-113">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="42d64-113">An Azure AD subscription</span></span>
- <span data-ttu-id="42d64-114">Un abonnement Wdesk avec authentification unique activée</span><span class="sxs-lookup"><span data-stu-id="42d64-114">A Wdesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="42d64-115">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="42d64-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="42d64-116">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="42d64-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="42d64-117">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="42d64-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="42d64-118">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="42d64-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="42d64-119">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="42d64-119">Scenario description</span></span>
<span data-ttu-id="42d64-120">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="42d64-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="42d64-121">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="42d64-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="42d64-122">Ajout de Wdesk à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="42d64-122">Adding Wdesk from hello gallery</span></span>
2. <span data-ttu-id="42d64-123">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="42d64-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wdesk-from-hello-gallery"></a><span data-ttu-id="42d64-124">Ajout de Wdesk à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="42d64-124">Adding Wdesk from hello gallery</span></span>
<span data-ttu-id="42d64-125">intégration de hello tooconfigure de Wdesk dans Azure AD, vous devez tooadd Wdesk à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="42d64-125">tooconfigure hello integration of Wdesk into Azure AD, you need tooadd Wdesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="42d64-126">**tooadd Wdesk à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42d64-126">**tooadd Wdesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="42d64-127">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="42d64-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="42d64-129">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="42d64-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="42d64-130">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="42d64-130">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="42d64-132">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="42d64-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="42d64-134">Dans la zone de recherche de hello, tapez **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="42d64-134">In hello search box, type **Wdesk**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. <span data-ttu-id="42d64-136">Dans le volet de résultats hello, sélectionnez **Wdesk**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="42d64-136">In hello results panel, select **Wdesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="42d64-138">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="42d64-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="42d64-139">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Wdesk, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="42d64-139">In this section, you configure and test Azure AD single sign-on with Wdesk based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="42d64-140">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Wdesk est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42d64-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Wdesk is tooa user in Azure AD.</span></span> <span data-ttu-id="42d64-141">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Wdesk doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="42d64-141">In other words, a link relationship between an Azure AD user and hello related user in Wdesk needs toobe established.</span></span>

<span data-ttu-id="42d64-142">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Wdesk.</span><span class="sxs-lookup"><span data-stu-id="42d64-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wdesk.</span></span>

<span data-ttu-id="42d64-143">tooconfigure et test Azure AD l’authentification unique avec Wdesk, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="42d64-143">tooconfigure and test Azure AD single sign-on with Wdesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="42d64-144">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="42d64-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="42d64-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42d64-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="42d64-146">**[Création d’un utilisateur de test Wdesk](#creating-a-wdesk-test-user)**  -toohave un équivalent de Britta Simon dans Wdesk est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="42d64-146">**[Creating a Wdesk test user](#creating-a-wdesk-test-user)** - toohave a counterpart of Britta Simon in Wdesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="42d64-147">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="42d64-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="42d64-148">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="42d64-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="42d64-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="42d64-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="42d64-150">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Wdesk.</span><span class="sxs-lookup"><span data-stu-id="42d64-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Wdesk application.</span></span>

<span data-ttu-id="42d64-151">**tooconfigure Azure AD single sign-on avec Wdesk, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42d64-151">**tooconfigure Azure AD single sign-on with Wdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="42d64-152">Bonjour portail Azure, sur hello **Wdesk** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="42d64-152">In hello Azure portal, on hello **Wdesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="42d64-154">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="42d64-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. <span data-ttu-id="42d64-156">Sur hello **Wdesk domaine et les URL** section, si vous le souhaitez application hello tooconfigure **IDP** mode initié effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="42d64-156">On hello **Wdesk Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    <span data-ttu-id="42d64-158">a.</span><span class="sxs-lookup"><span data-stu-id="42d64-158">a.</span></span> <span data-ttu-id="42d64-159">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="42d64-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span></span>

    <span data-ttu-id="42d64-160">b.</span><span class="sxs-lookup"><span data-stu-id="42d64-160">b.</span></span> <span data-ttu-id="42d64-161">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="42d64-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span></span>

4. <span data-ttu-id="42d64-162">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="42d64-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="42d64-163">Si vous le souhaitez application hello tooconfigure **SP** initiée par le mode, effectuer hello suivant l’étape :</span><span class="sxs-lookup"><span data-stu-id="42d64-163">If you wish tooconfigure hello application in **SP** initiated mode, perform hello following step:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    <span data-ttu-id="42d64-165">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="42d64-165">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="42d64-166">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="42d64-166">These values are not real.</span></span> <span data-ttu-id="42d64-167">Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="42d64-167">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="42d64-168">Vous obtenez ces valeurs à partir du portail de WDesk lorsque vous configurez l’authentification unique de hello.</span><span class="sxs-lookup"><span data-stu-id="42d64-168">You get these values from WDesk portal when you configure hello SSO.</span></span> 
  
5. <span data-ttu-id="42d64-169">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="42d64-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. <span data-ttu-id="42d64-171">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="42d64-171">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="42d64-173">Dans une fenêtre de navigateur web, tooWdesk de connexion en tant qu’administrateur de sécurité.</span><span class="sxs-lookup"><span data-stu-id="42d64-173">In a different web browser window, login tooWdesk as a Security Administrator.</span></span>

8. <span data-ttu-id="42d64-174">Dans hello inférieur gauche, cliquez sur **Admin** et choisissez **Admin. compte**:</span><span class="sxs-lookup"><span data-stu-id="42d64-174">In hello bottom left, click **Admin** and choose **Account Admin**:</span></span>
 
     ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. <span data-ttu-id="42d64-176">Dans Wdesk Admin, accédez trop**sécurité**, puis **SAML** > **paramètres SAML**:</span><span class="sxs-lookup"><span data-stu-id="42d64-176">In Wdesk Admin, navigate too**Security**, then **SAML** > **SAML Settings**:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. <span data-ttu-id="42d64-178">Sous **paramètres généraux**, vérifiez hello **activer SAML Single Sign On**:</span><span class="sxs-lookup"><span data-stu-id="42d64-178">Under **General Settings**, check hello **Enable SAML Single Sign On**:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. <span data-ttu-id="42d64-180">Sous **détails du fournisseur de Service**, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="42d64-180">Under **Service Provider Details**, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      <span data-ttu-id="42d64-182">a.</span><span class="sxs-lookup"><span data-stu-id="42d64-182">a.</span></span> <span data-ttu-id="42d64-183">Hello de copie **URL de connexion** et collez-le dans **Url de connexion** zone de texte sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="42d64-183">Copy hello **Login URL** and paste it in **Sign-on Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="42d64-184">b.</span><span class="sxs-lookup"><span data-stu-id="42d64-184">b.</span></span> <span data-ttu-id="42d64-185">Hello de copie **Url de métadonnées** et collez-le dans **identificateur** zone de texte sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="42d64-185">Copy hello **Metadata Url** and paste it in **Identifier** textbox on Azure portal.</span></span>
       
      <span data-ttu-id="42d64-186">c.</span><span class="sxs-lookup"><span data-stu-id="42d64-186">c.</span></span> <span data-ttu-id="42d64-187">Hello de copie **consommateur url** et collez-le dans **Url de réponse** zone de texte sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="42d64-187">Copy hello **Consumer url** and paste it in **Reply Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="42d64-188">d.</span><span class="sxs-lookup"><span data-stu-id="42d64-188">d.</span></span> <span data-ttu-id="42d64-189">Cliquez sur **enregistrer** sur les modifications de hello toosave portail Azure.</span><span class="sxs-lookup"><span data-stu-id="42d64-189">Click **Save** on Azure portal toosave hello changes.</span></span>      

12. <span data-ttu-id="42d64-190">Cliquez sur **configurer les paramètres IdP** tooopen **modifier les paramètres de fournisseurs d’identité** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="42d64-190">Click **Configure IdP Settings** tooopen **Edit IdP Settings** dialog.</span></span> <span data-ttu-id="42d64-191">Cliquez sur **choisir un fichier** toolocate hello **Metadata.xml** fichier que vous avez enregistré à partir du portail Azure, puis le télécharger.</span><span class="sxs-lookup"><span data-stu-id="42d64-191">Click **Choose File** toolocate hello **Metadata.xml** file you saved from Azure portal, then upload it.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. <span data-ttu-id="42d64-193">Cliquez sur **Save changes**.</span><span class="sxs-lookup"><span data-stu-id="42d64-193">Click **Save changes**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> <span data-ttu-id="42d64-195">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="42d64-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="42d64-196">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="42d64-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="42d64-197">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="42d64-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="42d64-198">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="42d64-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="42d64-199">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="42d64-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="42d64-201">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42d64-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="42d64-202">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="42d64-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="42d64-204">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="42d64-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="42d64-206">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="42d64-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="42d64-208">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="42d64-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="42d64-210">a.</span><span class="sxs-lookup"><span data-stu-id="42d64-210">a.</span></span> <span data-ttu-id="42d64-211">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="42d64-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="42d64-212">b.</span><span class="sxs-lookup"><span data-stu-id="42d64-212">b.</span></span> <span data-ttu-id="42d64-213">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="42d64-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="42d64-214">c.</span><span class="sxs-lookup"><span data-stu-id="42d64-214">c.</span></span> <span data-ttu-id="42d64-215">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="42d64-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="42d64-216">d.</span><span class="sxs-lookup"><span data-stu-id="42d64-216">d.</span></span> <span data-ttu-id="42d64-217">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="42d64-217">Click **Create**.</span></span>
 
### <a name="creating-a-wdesk-test-user"></a><span data-ttu-id="42d64-218">Création d’un utilisateur de test Wdesk</span><span class="sxs-lookup"><span data-stu-id="42d64-218">Creating a Wdesk test user</span></span>

<span data-ttu-id="42d64-219">tooenable Azure AD les utilisateurs toolog dans tooWdesk, vous devez les configurer dans Wdesk.</span><span class="sxs-lookup"><span data-stu-id="42d64-219">tooenable Azure AD users toolog in tooWdesk, they must be provisioned into Wdesk.</span></span> <span data-ttu-id="42d64-220">Dans Wdesk, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="42d64-220">In Wdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="42d64-221">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42d64-221">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="42d64-222">Connectez-vous en tant qu’administrateur de sécurité tooWdesk.</span><span class="sxs-lookup"><span data-stu-id="42d64-222">Log in tooWdesk as a Security Administrator.</span></span>
2. <span data-ttu-id="42d64-223">Accédez trop**Admin** > **Admin. compte**.</span><span class="sxs-lookup"><span data-stu-id="42d64-223">Navigate too**Admin** > **Account Admin**.</span></span>

     ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. <span data-ttu-id="42d64-225">Dans **Personnes**, cliquez sur **Membres**.</span><span class="sxs-lookup"><span data-stu-id="42d64-225">Click **Members** under **People**.</span></span>

4. <span data-ttu-id="42d64-226">Maintenant, cliquez sur **Add Member** tooopen **Add Member** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="42d64-226">Now click **Add Member** tooopen **Add Member** dialog box.</span></span> 
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. <span data-ttu-id="42d64-228">Dans **utilisateur** texte, entrez le nom d’utilisateur hello d’utilisateur comme  **brittasimon@contoso.com**  et cliquez sur **continuer** bouton.</span><span class="sxs-lookup"><span data-stu-id="42d64-228">In **User** text box, enter hello username of user like **brittasimon@contoso.com** and click **Continue** button.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  <span data-ttu-id="42d64-230">Entrez les détails de hello comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="42d64-230">Enter hello details as shown below:</span></span>
  
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    <span data-ttu-id="42d64-232">a.</span><span class="sxs-lookup"><span data-stu-id="42d64-232">a.</span></span> <span data-ttu-id="42d64-233">Dans **messagerie** texte, entrez l’e-mail hello d’utilisateur comme  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="42d64-233">In **E-mail** text box, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="42d64-234">b.</span><span class="sxs-lookup"><span data-stu-id="42d64-234">b.</span></span> <span data-ttu-id="42d64-235">Dans **prénom** texte, entrez le nom d’utilisateur comme hello **Brian**.</span><span class="sxs-lookup"><span data-stu-id="42d64-235">In **First Name** text box, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="42d64-236">c.</span><span class="sxs-lookup"><span data-stu-id="42d64-236">c.</span></span> <span data-ttu-id="42d64-237">Dans **nom** texte, entrez le nom d’utilisateur comme hello **Simon**.</span><span class="sxs-lookup"><span data-stu-id="42d64-237">In **Last Name** text box, enter hello last name of user like **Simon**.</span></span>

7. <span data-ttu-id="42d64-238">Cliquez sur **Enregistrer membre**.</span><span class="sxs-lookup"><span data-stu-id="42d64-238">Click **Save Member** button.</span></span>  

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="42d64-240">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="42d64-240">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="42d64-241">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooWdesk.</span><span class="sxs-lookup"><span data-stu-id="42d64-241">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWdesk.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="42d64-243">**tooassign Britta Simon tooWdesk, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42d64-243">**tooassign Britta Simon tooWdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="42d64-244">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="42d64-244">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="42d64-246">Dans la liste des applications hello, sélectionnez **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="42d64-246">In hello applications list, select **Wdesk**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. <span data-ttu-id="42d64-248">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="42d64-248">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="42d64-250">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="42d64-250">Click **Add** button.</span></span> <span data-ttu-id="42d64-251">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="42d64-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="42d64-253">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="42d64-253">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="42d64-254">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="42d64-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="42d64-255">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="42d64-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="42d64-256">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="42d64-256">Testing single sign-on</span></span>

<span data-ttu-id="42d64-257">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="42d64-257">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="42d64-258">Lorsque vous cliquez sur mosaïque Wdesk hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Wdesk application.</span><span class="sxs-lookup"><span data-stu-id="42d64-258">When you click hello Wdesk tile in hello Access Panel, you should get automatically signed-on tooyour Wdesk application.</span></span>
<span data-ttu-id="42d64-259">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="42d64-259">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="42d64-260">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="42d64-260">Additional resources</span></span>

* [<span data-ttu-id="42d64-261">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42d64-261">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="42d64-262">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="42d64-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

