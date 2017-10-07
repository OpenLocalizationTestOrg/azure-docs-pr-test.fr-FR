---
title: "Didacticiel : Intégration d’Azure Active Directory à TeamSeer | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de TeamSeer."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 876d13e446115acd50b01c7f44db99357045e429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a><span data-ttu-id="e84c8-103">Didacticiel : Intégration d’Azure AD à TeamSeer</span><span class="sxs-lookup"><span data-stu-id="e84c8-103">Tutorial: Azure Active Directory integration with TeamSeer</span></span>

<span data-ttu-id="e84c8-104">Dans ce didacticiel, vous apprendrez comment toointegrate TeamSeer avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e84c8-104">In this tutorial, you learn how toointegrate TeamSeer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e84c8-105">Intégration de TeamSeer à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="e84c8-105">Integrating TeamSeer with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e84c8-106">Vous pouvez contrôler dans Azure AD qui a accès tooTeamSeer</span><span class="sxs-lookup"><span data-stu-id="e84c8-106">You can control in Azure AD who has access tooTeamSeer</span></span>
- <span data-ttu-id="e84c8-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooTeamSeer (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="e84c8-107">You can enable your users tooautomatically get signed-on tooTeamSeer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e84c8-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="e84c8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e84c8-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e84c8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e84c8-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e84c8-110">Prerequisites</span></span>

<span data-ttu-id="e84c8-111">tooconfigure intégration d’Azure AD à TeamSeer, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e84c8-111">tooconfigure Azure AD integration with TeamSeer, you need hello following items:</span></span>

- <span data-ttu-id="e84c8-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="e84c8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e84c8-113">Un abonnement TeamSeer pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="e84c8-113">A TeamSeer single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e84c8-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="e84c8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e84c8-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="e84c8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e84c8-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e84c8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e84c8-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e84c8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e84c8-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="e84c8-118">Scenario description</span></span>
<span data-ttu-id="e84c8-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="e84c8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e84c8-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="e84c8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e84c8-121">Ajout de TeamSeer à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e84c8-121">Adding TeamSeer from hello gallery</span></span>
2. <span data-ttu-id="e84c8-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e84c8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamseer-from-hello-gallery"></a><span data-ttu-id="e84c8-123">Ajout de TeamSeer à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e84c8-123">Adding TeamSeer from hello gallery</span></span>
<span data-ttu-id="e84c8-124">intégration de hello tooconfigure de TeamSeer dans tooAzure AD, vous devez tooadd TeamSeer à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="e84c8-124">tooconfigure hello integration of TeamSeer in tooAzure AD, you need tooadd TeamSeer from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e84c8-125">**tooadd TeamSeer à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e84c8-125">**tooadd TeamSeer from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e84c8-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="e84c8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e84c8-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="e84c8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e84c8-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e84c8-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="e84c8-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e84c8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="e84c8-133">Dans la zone de recherche de hello, tapez **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="e84c8-133">In hello search box, type **TeamSeer**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_search.png)

5. <span data-ttu-id="e84c8-135">Dans le volet de résultats hello, sélectionnez **TeamSeer**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e84c8-135">In hello results panel, select **TeamSeer**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e84c8-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e84c8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e84c8-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec TeamSeer à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="e84c8-138">In this section, you configure and test Azure AD single sign-on with TeamSeer based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e84c8-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans TeamSeer est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e84c8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TeamSeer is tooa user in Azure AD.</span></span> <span data-ttu-id="e84c8-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans TeamSeer doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="e84c8-140">In other words, a link relationship between an Azure AD user and hello related user in TeamSeer needs toobe established.</span></span>

<span data-ttu-id="e84c8-141">Dans TeamSeer, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="e84c8-141">In TeamSeer, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e84c8-142">tooconfigure et test Azure AD l’authentification unique avec TeamSeer, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="e84c8-142">tooconfigure and test Azure AD single sign-on with TeamSeer, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e84c8-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="e84c8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e84c8-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e84c8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e84c8-145">**[Création d’un utilisateur de test de TeamSeer](#creating-a-teamseer-test-user)**  -toohave un équivalent de Britta Simon dans TeamSeer est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e84c8-145">**[Creating a TeamSeer test user](#creating-a-teamseer-test-user)** - toohave a counterpart of Britta Simon in TeamSeer that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e84c8-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e84c8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e84c8-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="e84c8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e84c8-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e84c8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e84c8-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="e84c8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TeamSeer application.</span></span>

<span data-ttu-id="e84c8-150">**tooconfigure Azure AD single sign-on avec TeamSeer, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e84c8-150">**tooconfigure Azure AD single sign-on with TeamSeer, perform hello following steps:**</span></span>

1. <span data-ttu-id="e84c8-151">Bonjour portail Azure, sur hello **TeamSeer** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="e84c8-151">In hello Azure portal, on hello **TeamSeer** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="e84c8-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e84c8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_samlbase.png)

3. <span data-ttu-id="e84c8-155">Sur hello **TeamSeer domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e84c8-155">On hello **TeamSeer Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_url.png)

     <span data-ttu-id="e84c8-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://www.teamseer.com/<companyid>`</span><span class="sxs-lookup"><span data-stu-id="e84c8-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.teamseer.com/<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e84c8-158">valeur de Hello n’est pas réelle.</span><span class="sxs-lookup"><span data-stu-id="e84c8-158">hello value is not real.</span></span> <span data-ttu-id="e84c8-159">Valeur de hello de mise à jour avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="e84c8-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="e84c8-160">Contact [équipe de support Client de TeamSeer](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) valeur hello de tooget.</span><span class="sxs-lookup"><span data-stu-id="e84c8-160">Contact [TeamSeer Client support team](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) tooget hello value.</span></span> 
 
4. <span data-ttu-id="e84c8-161">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e84c8-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_certificate.png) 

5. <span data-ttu-id="e84c8-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="e84c8-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamseer-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e84c8-165">Sur hello **TeamSeer Configuration** , cliquez sur **configurer de TeamSeer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="e84c8-165">On hello **TeamSeer Configuration** section, click **Configure TeamSeer** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e84c8-166">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="e84c8-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_configure.png)

7. <span data-ttu-id="e84c8-168">Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise TeamSeer tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="e84c8-168">In a different web browser window, log in tooyour TeamSeer company site as an administrator.</span></span>

8. <span data-ttu-id="e84c8-169">Accédez trop**administrateur RH**.</span><span class="sxs-lookup"><span data-stu-id="e84c8-169">Go too**HR Admin**.</span></span>
   
    <span data-ttu-id="e84c8-170">![Administrateur RH](./media/active-directory-saas-teamseer-tutorial/ic789634.png "Administrateur RH")</span><span class="sxs-lookup"><span data-stu-id="e84c8-170">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR Admin")</span></span>

9. <span data-ttu-id="e84c8-171">Cliquez sur **Setup**.</span><span class="sxs-lookup"><span data-stu-id="e84c8-171">Click **Setup**.</span></span>
   
    <span data-ttu-id="e84c8-172">![Configuration](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Configuration")</span><span class="sxs-lookup"><span data-stu-id="e84c8-172">![Setup](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Setup")</span></span>

10. <span data-ttu-id="e84c8-173">Cliquez sur **Set up SAML provider details**.</span><span class="sxs-lookup"><span data-stu-id="e84c8-173">Click **Set up SAML provider details**.</span></span>
   
    <span data-ttu-id="e84c8-174">![Paramètres SAML](./media/active-directory-saas-teamseer-tutorial/ic789636.png "Paramètres SAML")</span><span class="sxs-lookup"><span data-stu-id="e84c8-174">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML Settings")</span></span>

11. <span data-ttu-id="e84c8-175">Dans la section Détails du fournisseur SAML de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e84c8-175">In hello SAML provider details section, perform hello following steps:</span></span>
   
    <span data-ttu-id="e84c8-176">![Paramètres SAML](./media/active-directory-saas-teamseer-tutorial/ic789637.png "Paramètres SAML")</span><span class="sxs-lookup"><span data-stu-id="e84c8-176">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML Settings")</span></span>   

    <span data-ttu-id="e84c8-177">a.</span><span class="sxs-lookup"><span data-stu-id="e84c8-177">a.</span></span> <span data-ttu-id="e84c8-178">Hello de coller **-Service URL d’authentification** valeur toohello **URL** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="e84c8-178">Paste hello **Single Sign-On Service URL** value in toohello **URL** textbox.</span></span>
          
    <span data-ttu-id="e84c8-179">b.</span><span class="sxs-lookup"><span data-stu-id="e84c8-179">b.</span></span> <span data-ttu-id="e84c8-180">Ouvrez votre certificat codé en base 64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers tooyour et le coller ensuite toohello **certificat Public IdP** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="e84c8-180">Open your base-64 encoded certificate in notepad, copy hello content of it in tooyour clipboard, and then paste it toohello **IdP Public Certificate** textbox.</span></span>

12. <span data-ttu-id="e84c8-181">toocomplete hello configuration du fournisseur SAML, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e84c8-181">toocomplete hello SAML provider configuration, perform hello following steps:</span></span>
    
    <span data-ttu-id="e84c8-182">![Paramètres SAML](./media/active-directory-saas-teamseer-tutorial/ic789638.png "Paramètres SAML")</span><span class="sxs-lookup"><span data-stu-id="e84c8-182">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML Settings")</span></span> 

    <span data-ttu-id="e84c8-183">a.</span><span class="sxs-lookup"><span data-stu-id="e84c8-183">a.</span></span> <span data-ttu-id="e84c8-184">Bonjour **tester les adresses de messagerie**, tapez l’adresse de messagerie de l’utilisateur de test hello.</span><span class="sxs-lookup"><span data-stu-id="e84c8-184">In hello **Test Email Addresses**, type hello test user’s email address.</span></span> 
  
    <span data-ttu-id="e84c8-185">b.</span><span class="sxs-lookup"><span data-stu-id="e84c8-185">b.</span></span> <span data-ttu-id="e84c8-186">Bonjour **émetteur** zone de texte, hello de type URL de l’émetteur hello fournisseur de services.</span><span class="sxs-lookup"><span data-stu-id="e84c8-186">In hello **Issuer** textbox, type hello Issuer URL of hello service provider.</span></span> 
  
    <span data-ttu-id="e84c8-187">c.</span><span class="sxs-lookup"><span data-stu-id="e84c8-187">c.</span></span> <span data-ttu-id="e84c8-188">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e84c8-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e84c8-189">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="e84c8-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e84c8-190">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="e84c8-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e84c8-191">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e84c8-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e84c8-192">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="e84c8-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="e84c8-193">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="e84c8-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="e84c8-195">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e84c8-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e84c8-196">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="e84c8-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e84c8-198">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="e84c8-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e84c8-200">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="e84c8-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e84c8-202">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e84c8-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e84c8-204">a.</span><span class="sxs-lookup"><span data-stu-id="e84c8-204">a.</span></span> <span data-ttu-id="e84c8-205">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e84c8-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e84c8-206">b.</span><span class="sxs-lookup"><span data-stu-id="e84c8-206">b.</span></span> <span data-ttu-id="e84c8-207">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e84c8-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e84c8-208">c.</span><span class="sxs-lookup"><span data-stu-id="e84c8-208">c.</span></span> <span data-ttu-id="e84c8-209">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="e84c8-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e84c8-210">d.</span><span class="sxs-lookup"><span data-stu-id="e84c8-210">d.</span></span> <span data-ttu-id="e84c8-211">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="e84c8-211">Click **Create**.</span></span>
 
### <a name="creating-a-teamseer-test-user"></a><span data-ttu-id="e84c8-212">Création d’un utilisateur de test TeamSeer</span><span class="sxs-lookup"><span data-stu-id="e84c8-212">Creating a TeamSeer test user</span></span>

<span data-ttu-id="e84c8-213">tooenable Azure AD les utilisateurs toolog dans tooTeamSeer, ils doivent être configurés dans tooShiftPlanning.</span><span class="sxs-lookup"><span data-stu-id="e84c8-213">tooenable Azure AD users toolog in tooTeamSeer, they must be provisioned in tooShiftPlanning.</span></span> <span data-ttu-id="e84c8-214">Dans les cas de hello de TeamSeer, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="e84c8-214">In hello case of TeamSeer, provisioning is a manual task.</span></span>

<span data-ttu-id="e84c8-215">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e84c8-215">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="e84c8-216">Connectez-vous à tooyour **TeamSeer** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="e84c8-216">Log in tooyour **TeamSeer** company site as an administrator.</span></span>

2. <span data-ttu-id="e84c8-217">Effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e84c8-217">Perform hello following steps:</span></span>
   
    <span data-ttu-id="e84c8-218">![Administrateur RH](./media/active-directory-saas-teamseer-tutorial/ic789640.png "Administrateur RH")</span><span class="sxs-lookup"><span data-stu-id="e84c8-218">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR Admin")</span></span>  
 
    <span data-ttu-id="e84c8-219">a.</span><span class="sxs-lookup"><span data-stu-id="e84c8-219">a.</span></span> <span data-ttu-id="e84c8-220">Accédez trop**administrateur RH \> utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="e84c8-220">Go too**HR Admin \> Users**.</span></span>
  
    <span data-ttu-id="e84c8-221">b.</span><span class="sxs-lookup"><span data-stu-id="e84c8-221">b.</span></span> <span data-ttu-id="e84c8-222">Cliquez sur **exécuter l’Assistant du nouvel utilisateur hello**.</span><span class="sxs-lookup"><span data-stu-id="e84c8-222">Click **Run hello New User wizard**.</span></span>

3. <span data-ttu-id="e84c8-223">Bonjour **détails de l’utilisateur** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e84c8-223">In hello **User Details** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="e84c8-224">![Détails de l’utilisateur](./media/active-directory-saas-teamseer-tutorial/ic789641.png "Détails de l’utilisateur")</span><span class="sxs-lookup"><span data-stu-id="e84c8-224">![User Details](./media/active-directory-saas-teamseer-tutorial/ic789641.png "User Details")</span></span>

    <span data-ttu-id="e84c8-225">a.</span><span class="sxs-lookup"><span data-stu-id="e84c8-225">a.</span></span> <span data-ttu-id="e84c8-226">Hello de type **prénom**, **Surname**, **nom d’utilisateur (adresse de messagerie)** d’un compte AAD valide que vous souhaitez tooprovision dans toohello relatives des zones de texte.</span><span class="sxs-lookup"><span data-stu-id="e84c8-226">Type hello **First Name**, **Surname**, **User name (Email address)** of a valid AAD account you want tooprovision in toohello related textboxes.</span></span>
  
    <span data-ttu-id="e84c8-227">b.</span><span class="sxs-lookup"><span data-stu-id="e84c8-227">b.</span></span> <span data-ttu-id="e84c8-228">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e84c8-228">Click **Next**.</span></span>

4. <span data-ttu-id="e84c8-229">Suivez hello à l’écran des instructions pour l’ajout d’un nouvel utilisateur, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="e84c8-229">Follow hello on-screen instructions for adding a new user, and click **Finish**.</span></span>

>[!NOTE]
><span data-ttu-id="e84c8-230">Vous pouvez utiliser n’importe quel autre TeamSeer utilisateur compte outil de création ou API fournie par TeamSeer tooprovision comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e84c8-230">You can use any other TeamSeer user account creation tools or APIs provided by TeamSeer tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e84c8-231">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e84c8-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e84c8-232">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooTeamSeer.</span><span class="sxs-lookup"><span data-stu-id="e84c8-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTeamSeer.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="e84c8-234">**tooassign Britta Simon tooTeamSeer, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e84c8-234">**tooassign Britta Simon tooTeamSeer, perform hello following steps:**</span></span>

1. <span data-ttu-id="e84c8-235">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e84c8-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="e84c8-237">Dans la liste des applications hello, sélectionnez **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="e84c8-237">In hello applications list, select **TeamSeer**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_app.png) 

3. <span data-ttu-id="e84c8-239">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e84c8-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="e84c8-241">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e84c8-241">Click **Add** button.</span></span> <span data-ttu-id="e84c8-242">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e84c8-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="e84c8-244">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="e84c8-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e84c8-245">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e84c8-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e84c8-246">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e84c8-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e84c8-247">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="e84c8-247">Testing single sign-on</span></span>

<span data-ttu-id="e84c8-248">Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="e84c8-248">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="e84c8-249">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e84c8-249">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e84c8-250">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e84c8-250">Additional resources</span></span>

* [<span data-ttu-id="e84c8-251">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e84c8-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e84c8-252">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="e84c8-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_203.png
