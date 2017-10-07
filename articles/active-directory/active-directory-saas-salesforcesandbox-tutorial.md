---
title: "Didacticiel : intégration d’Azure Active Directory à Salesforce Sandbox | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Salesforce Sandbox."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7539f08356568a17ebfcee2764bbbefa129b0553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="4f37f-103">Didacticiel : Intégration d’Azure Active Directory à Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="4f37f-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="4f37f-104">Dans ce didacticiel, vous apprendrez comment toointegrate Salesforce Sandbox avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4f37f-104">In this tutorial, you learn how toointegrate Salesforce Sandbox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4f37f-105">Intégration de Salesforce Sandbox avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="4f37f-105">Integrating Salesforce Sandbox with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4f37f-106">Vous pouvez contrôler dans Azure AD qui a accès tooSalesforce bac à sable</span><span class="sxs-lookup"><span data-stu-id="4f37f-106">You can control in Azure AD who has access tooSalesforce Sandbox</span></span>
- <span data-ttu-id="4f37f-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSalesforce bac à sable (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f37f-107">You can enable your users tooautomatically get signed-on tooSalesforce Sandbox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4f37f-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="4f37f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4f37f-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4f37f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f37f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4f37f-110">Prerequisites</span></span>

<span data-ttu-id="4f37f-111">tooconfigure intégration d’Azure AD à Salesforce Sandbox, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4f37f-111">tooconfigure Azure AD integration with Salesforce Sandbox, you need hello following items:</span></span>

- <span data-ttu-id="4f37f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f37f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4f37f-113">Un abonnement Salesforce Sandbox pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="4f37f-113">A Salesforce Sandbox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4f37f-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="4f37f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4f37f-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="4f37f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4f37f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4f37f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4f37f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4f37f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4f37f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="4f37f-118">Scenario description</span></span>
<span data-ttu-id="4f37f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="4f37f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4f37f-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="4f37f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4f37f-121">Ajout de bac à sable Salesforce à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4f37f-121">Adding Salesforce Sandbox from hello gallery</span></span>
2. <span data-ttu-id="4f37f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f37f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-sandbox-from-hello-gallery"></a><span data-ttu-id="4f37f-123">Ajout de bac à sable Salesforce à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4f37f-123">Adding Salesforce Sandbox from hello gallery</span></span>
<span data-ttu-id="4f37f-124">tooconfigure hello intégration de Salesforce Sandbox dans Azure AD, vous devez tooadd bac à sable Salesforce à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="4f37f-124">tooconfigure hello integration of Salesforce Sandbox into Azure AD, you need tooadd Salesforce Sandbox from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4f37f-125">**tooadd bac à sable Salesforce à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4f37f-125">**tooadd Salesforce Sandbox from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f37f-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="4f37f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4f37f-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4f37f-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="4f37f-131">Cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="4f37f-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="4f37f-133">Dans la zone de recherche de hello, tapez **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-133">In hello search box, type **Salesforce Sandbox**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. <span data-ttu-id="4f37f-135">Dans le volet de résultats hello, sélectionnez **Salesforce Sandbox**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4f37f-135">In hello results panel, select **Salesforce Sandbox**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4f37f-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f37f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4f37f-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Salesforce Sandbox sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="4f37f-138">In this section, you configure and test Azure AD single sign-on with Salesforce Sandbox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4f37f-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Salesforce Sandbox est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f37f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Salesforce Sandbox is tooa user in Azure AD.</span></span> <span data-ttu-id="4f37f-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans un bac à sable Salesforce hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="4f37f-140">In other words, a link relationship between an Azure AD user and hello related user in Salesforce Sandbox needs toobe established.</span></span>

<span data-ttu-id="4f37f-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="4f37f-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Salesforce Sandbox.</span></span>

<span data-ttu-id="4f37f-142">tooconfigure et test Azure AD l’authentification unique avec Salesforce Sandbox, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="4f37f-142">tooconfigure and test Azure AD single sign-on with Salesforce Sandbox, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4f37f-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="4f37f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4f37f-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4f37f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4f37f-145">**[Création d’un utilisateur de test de Salesforce Sandbox](#creating-a-salesforce-sandbox-test-user)**  -toohave un équivalent de Britta Simon dans Salesforce Sandbox qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4f37f-145">**[Creating a Salesforce Sandbox test user](#creating-a-salesforce-sandbox-test-user)** - toohave a counterpart of Britta Simon in Salesforce Sandbox that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4f37f-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4f37f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4f37f-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="4f37f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4f37f-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f37f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4f37f-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="4f37f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Salesforce Sandbox application.</span></span>

<span data-ttu-id="4f37f-150">**tooconfigure Azure AD single sign-on avec Salesforce Sandbox, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4f37f-150">**tooconfigure Azure AD single sign-on with Salesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f37f-151">Bonjour portail Azure, sur hello **Salesforce Sandbox** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-151">In hello Azure portal, on hello **Salesforce Sandbox** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="4f37f-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4f37f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. <span data-ttu-id="4f37f-155">Sur hello **URL et le domaine de bac à sable Salesforce** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4f37f-155">On hello **Salesforce Sandbox Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     <span data-ttu-id="4f37f-157">Bonjour **URL de connexion** zone de texte, valeur hello de type hello suivant le modèle à l’aide de :`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="4f37f-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<subdomain>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4f37f-158">Cette valeur n’est pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="4f37f-158">This value is not hello real.</span></span> <span data-ttu-id="4f37f-159">Mettre à jour cette valeur avec l’URL de connexion réel hello. Contact [équipe de support Client de bac à sable Salesforce](https://help.salesforce.com/support) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="4f37f-159">Update this value with hello actual Sign-on URL.Contact [Salesforce Sandbox Client support team](https://help.salesforce.com/support) tooget this value.</span></span>


4. <span data-ttu-id="4f37f-160">Si vous avez déjà configuré l’authentification unique pour une autre instance Salesforce Sandbox dans votre annuaire, vous devez également configurer hello **identificateur** toohave hello la même valeur que hello **URL de connexion**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-160">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure hello **Identifier** toohave hello same value as hello **Sign on URL**.</span></span> 
    
    >[!Note]
    ><span data-ttu-id="4f37f-161">Hello **identificateur** champ sont accessibles en vérifiant hello **afficher les paramètres avancés** case à cocher sur hello **Configure App URL** page de boîte de dialogue hello</span><span class="sxs-lookup"><span data-stu-id="4f37f-161">hello **Identifier** field can be found by checking hello **Show advanced settings** checkbox on hello **Configure App URL** page of hello dialog</span></span> 


5. <span data-ttu-id="4f37f-162">Sur hello **le certificat de signature SAML** , cliquez sur **certificat** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4f37f-162">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. <span data-ttu-id="4f37f-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="4f37f-164">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="4f37f-166">Sur hello **Configuration du bac à sable Salesforce** , cliquez sur **configurer Salesforce Sandbox** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="4f37f-166">On hello **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4f37f-167">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="4f37f-167">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="4f37f-168">![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="4f37f-168">![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span></span>
8. <span data-ttu-id="4f37f-169">Ouvrez un nouvel onglet dans votre navigateur et connectez-vous à tooyour compte d’administrateur Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="4f37f-169">Open a new tab in your browser and log in tooyour Salesforce Sandbox administrator account.</span></span>

9. <span data-ttu-id="4f37f-170">Dans le menu hello haut de hello, cliquez sur **le programme d’installation**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-170">In hello menu on hello top, click **Setup**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. <span data-ttu-id="4f37f-172">Dans le volet de navigation hello hello gauche, cliquez sur **des contrôles de sécurité**, puis cliquez sur **paramètres d’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-172">In hello navigation pane on hello left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. <span data-ttu-id="4f37f-174">Sur hello section de paramètres d’authentification unique, procédez hello comme suit : ![configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span><span class="sxs-lookup"><span data-stu-id="4f37f-174">On hello Single Sign-On Settings section, perform hello following steps:  ![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span></span>
     
     <span data-ttu-id="4f37f-175">a.</span><span class="sxs-lookup"><span data-stu-id="4f37f-175">a.</span></span>  <span data-ttu-id="4f37f-176">Sélectionnez **SAML Enabled**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-176">Select **SAML Enabled**.</span></span> 

     <span data-ttu-id="4f37f-177">b.</span><span class="sxs-lookup"><span data-stu-id="4f37f-177">b.</span></span>  <span data-ttu-id="4f37f-178">Cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-178">Click **New**.</span></span>

12. <span data-ttu-id="4f37f-179">Sur hello section de paramètres d’authentification unique SAML, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4f37f-179">On hello SAML Single Sign-On Settings section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    <span data-ttu-id="4f37f-181">zone de texte nom a.In hello, entrez un nom hello de configuration de hello (par exemple : *SPSSOWAAD\_Test*).</span><span class="sxs-lookup"><span data-stu-id="4f37f-181">a.In hello Name textbox, type hello name of hello configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 

    <span data-ttu-id="4f37f-182">b.</span><span class="sxs-lookup"><span data-stu-id="4f37f-182">b.</span></span> <span data-ttu-id="4f37f-183">Coller **ID d’entité SMAL** valeur hello **émetteur** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="4f37f-183">Paste **SMAL Entity ID** value into hello **Issuer** textbox.</span></span>

    <span data-ttu-id="4f37f-184">c.</span><span class="sxs-lookup"><span data-stu-id="4f37f-184">c.</span></span> <span data-ttu-id="4f37f-185">Bonjour **Id d’entité** zone de texte, type **https://test.salesforce.com** s’il s’agit de hello première instance Salesforce Sandbox que vous ajoutez tooyour active.</span><span class="sxs-lookup"><span data-stu-id="4f37f-185">In hello **Entity Id** textbox, type **https://test.salesforce.com** if it is hello first Salesforce Sandbox instance that you are adding tooyour directory.</span></span> <span data-ttu-id="4f37f-186">Si vous avez déjà ajouté une instance de bac à sable Salesforce, puis pour hello **ID d’entité** type Bonjour **URL de connexion**, qui doit être au format suivant :`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="4f37f-186">If you have already added an instance of Salesforce Sandbox, then for hello **Entity ID** type in hello **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>  
 
    <span data-ttu-id="4f37f-187">d.</span><span class="sxs-lookup"><span data-stu-id="4f37f-187">d.</span></span> <span data-ttu-id="4f37f-188">Cliquez sur **Parcourir** hello de tooupload téléchargé le certificat.</span><span class="sxs-lookup"><span data-stu-id="4f37f-188">Click **Browse** tooupload hello downloaded certificate.</span></span>  

    <span data-ttu-id="4f37f-189">e.</span><span class="sxs-lookup"><span data-stu-id="4f37f-189">e.</span></span> <span data-ttu-id="4f37f-190">En tant que **SAML Identity Type**, sélectionnez **Assertion contient hello ID de fédération à partir de l’objet utilisateur de hello**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-190">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>
 
    <span data-ttu-id="4f37f-191">f.</span><span class="sxs-lookup"><span data-stu-id="4f37f-191">f.</span></span> <span data-ttu-id="4f37f-192">En tant que **emplacement d’identité SAML**, sélectionnez **identité figure dans l’élément NameIdentifier de hello Hello Subject statement**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-192">As **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>

    <span data-ttu-id="4f37f-193">g.</span><span class="sxs-lookup"><span data-stu-id="4f37f-193">g.</span></span> <span data-ttu-id="4f37f-194">Coller **-Service URL d’authentification** dans hello **Identity Provider Login URL** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="4f37f-194">Paste **Single Sign-On Service URL** into hello **Identity Provider Login URL** textbox.</span></span> 

    <span data-ttu-id="4f37f-195">h.</span><span class="sxs-lookup"><span data-stu-id="4f37f-195">h.</span></span> <span data-ttu-id="4f37f-196">SFDC ne prend pas en charge la déconnexion SAML.</span><span class="sxs-lookup"><span data-stu-id="4f37f-196">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="4f37f-197">Pour résoudre ce problème, collez 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' dans hello **Identity Provider Logout URL** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="4f37f-197">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="4f37f-198">i.</span><span class="sxs-lookup"><span data-stu-id="4f37f-198">i.</span></span> <span data-ttu-id="4f37f-199">Pour **Service Provider Initiated Request Binding (Liaison de demande initiée par le fournisseur de services)**, sélectionnez **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-199">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 

    <span data-ttu-id="4f37f-200">j.</span><span class="sxs-lookup"><span data-stu-id="4f37f-200">j.</span></span> <span data-ttu-id="4f37f-201">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-201">Click **Save**.</span></span>

### <a name="enable-your-domain"></a><span data-ttu-id="4f37f-202">Activer votre domaine</span><span class="sxs-lookup"><span data-stu-id="4f37f-202">Enable your domain</span></span>
<span data-ttu-id="4f37f-203">Cette section suppose que vous avez déjà créé un domaine.</span><span class="sxs-lookup"><span data-stu-id="4f37f-203">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="4f37f-204">Pour plus d’informations, voir [Définition de votre nom de domaine](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="4f37f-204">For more information, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="4f37f-205">**tooenable votre domaine, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4f37f-205">**tooenable your domain, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f37f-206">Dans le volet de navigation gauche hello, cliquez sur **gestion des domaines**, puis cliquez sur **mon domaine.**</span><span class="sxs-lookup"><span data-stu-id="4f37f-206">In hello left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
     ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   ><span data-ttu-id="4f37f-208">Vérifiez que votre domaine a été correctement configuré.</span><span class="sxs-lookup"><span data-stu-id="4f37f-208">Please make sure that your domain has been configured correctly.</span></span> 

2. <span data-ttu-id="4f37f-209">Bonjour **les paramètres de Page de connexion** , cliquez sur **modifier**, puis, en tant que **Service d’authentification**, sélectionnez nom hello Hello SAML unique Sign-On Setting de hello précédente et enfin cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-209">In hello **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select hello name of hello SAML Single Sign-On Setting from hello previous section, and finally click **Save**.</span></span>
   
   ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

<span data-ttu-id="4f37f-211">Dès que vous avez un domaine configuré, vos utilisateurs doivent utiliser le bac à sable hello domaine URL toologin toohello Salesforce.</span><span class="sxs-lookup"><span data-stu-id="4f37f-211">As soon as you have a domain configured, your users should use hello domain URL toologin toohello Salesforce sandbox.</span></span>  

<span data-ttu-id="4f37f-212">valeur hello tooget hello URL, cliquez sur profil d’authentification unique hello que vous avez créé dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="4f37f-212">tooget hello value of hello URL, click hello SSO profile you have created in hello previous section.</span></span>    

> [!TIP]
> <span data-ttu-id="4f37f-213">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="4f37f-213">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4f37f-214">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="4f37f-214">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4f37f-215">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4f37f-215">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4f37f-216">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f37f-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="4f37f-217">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="4f37f-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="4f37f-219">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4f37f-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f37f-220">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="4f37f-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4f37f-222">liste de hello toodisplay des utilisateurs Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-222">toodisplay hello list of users go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4f37f-224">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4f37f-224">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4f37f-226">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4f37f-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4f37f-228">a.</span><span class="sxs-lookup"><span data-stu-id="4f37f-228">a.</span></span> <span data-ttu-id="4f37f-229">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4f37f-230">b.</span><span class="sxs-lookup"><span data-stu-id="4f37f-230">b.</span></span> <span data-ttu-id="4f37f-231">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4f37f-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4f37f-232">c.</span><span class="sxs-lookup"><span data-stu-id="4f37f-232">c.</span></span> <span data-ttu-id="4f37f-233">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4f37f-234">d.</span><span class="sxs-lookup"><span data-stu-id="4f37f-234">d.</span></span> <span data-ttu-id="4f37f-235">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-235">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-sandbox-test-user"></a><span data-ttu-id="4f37f-236">Création d’un utilisateur de test Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="4f37f-236">Creating a Salesforce Sandbox test user</span></span>

<span data-ttu-id="4f37f-237">Dans cette section, un utilisateur nommé Britta Simon est créé dans Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="4f37f-237">In this section, a user called Britta Simon is created in Salesforce Sandbox.</span></span> <span data-ttu-id="4f37f-238">Salesforce Sandbox prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="4f37f-238">Salesforce Sandbox supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="4f37f-239">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="4f37f-239">There is no action item for you in this section.</span></span> <span data-ttu-id="4f37f-240">Si un utilisateur n’existe pas déjà dans le bac à sable Salesforce, un nouveau est créé lorsque vous essayez de tooaccess Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="4f37f-240">If a user doesn't already exist in Salesforce Sandbox, a new one is created when you attempt tooaccess Salesforce Sandbox.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4f37f-241">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f37f-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4f37f-242">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSalesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="4f37f-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSalesforce Sandbox.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="4f37f-244">**tooassign Britta Simon tooSalesforce bac à sable, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4f37f-244">**tooassign Britta Simon tooSalesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f37f-245">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="4f37f-247">Dans la liste des applications hello, sélectionnez **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-247">In hello applications list, select **Salesforce Sandbox**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. <span data-ttu-id="4f37f-249">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="4f37f-251">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-251">Click **Add** button.</span></span> <span data-ttu-id="4f37f-252">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="4f37f-254">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="4f37f-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4f37f-255">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4f37f-256">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4f37f-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4f37f-257">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="4f37f-257">Testing single sign-on</span></span>

<span data-ttu-id="4f37f-258">Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="4f37f-258">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="4f37f-259">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4f37f-259">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4f37f-260">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4f37f-260">Additional resources</span></span>

* [<span data-ttu-id="4f37f-261">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4f37f-261">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4f37f-262">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="4f37f-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="4f37f-263">Configurer l’approvisionnement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="4f37f-263">Configure User Provisioning</span></span>](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

