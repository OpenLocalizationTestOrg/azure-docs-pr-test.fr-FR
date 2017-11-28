---
title: "Didacticiel : Intégration d’Azure Active Directory à Workplace par Facebook | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et l’espace de travail par Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f71a59527394730757d501a973251dc293fd3683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="2214c-103">Didacticiel : Intégration d’Azure Active Directory à Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="2214c-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="2214c-104">Dans ce didacticiel, vous apprendrez comment toointegrate espace de travail par Facebook avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2214c-104">In this tutorial, you learn how toointegrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2214c-105">Intégration d’espace de travail par Facebook à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="2214c-105">Integrating Workplace by Facebook with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2214c-106">Vous pouvez contrôler dans Azure AD qui a tooWorkplace d’accès par Facebook</span><span class="sxs-lookup"><span data-stu-id="2214c-106">You can control in Azure AD who has access tooWorkplace by Facebook</span></span>
- <span data-ttu-id="2214c-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooWorkplace par Facebook (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="2214c-107">You can enable your users tooautomatically get signed-on tooWorkplace by Facebook (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2214c-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="2214c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2214c-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2214c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2214c-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2214c-110">Prerequisites</span></span>

<span data-ttu-id="2214c-111">tooconfigure intégration d’Azure AD avec l’espace de travail par Facebook, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2214c-111">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="2214c-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="2214c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2214c-113">Un abonnement Workplace by Facebook pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="2214c-113">A Workplace by Facebook single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2214c-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="2214c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2214c-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="2214c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2214c-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2214c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2214c-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2214c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2214c-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="2214c-118">Scenario description</span></span>
<span data-ttu-id="2214c-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="2214c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2214c-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="2214c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2214c-121">Ajout d’espace de travail par Facebook à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="2214c-121">Adding Workplace by Facebook from hello gallery</span></span>
2. <span data-ttu-id="2214c-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2214c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workplace-by-facebook-from-hello-gallery"></a><span data-ttu-id="2214c-123">Ajout d’espace de travail par Facebook à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="2214c-123">Adding Workplace by Facebook from hello gallery</span></span>
<span data-ttu-id="2214c-124">intégration de hello tooconfigure du poste de travail par Facebook dans Azure AD, vous devez tooadd espace de travail par Facebook à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="2214c-124">tooconfigure hello integration of Workplace by Facebook into Azure AD, you need tooadd Workplace by Facebook from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2214c-125">**tooadd espace de travail par Facebook à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2214c-125">**tooadd Workplace by Facebook from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2214c-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="2214c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2214c-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="2214c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2214c-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2214c-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="2214c-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2214c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="2214c-133">Dans la zone de recherche de hello, tapez **espace de travail par Facebook**.</span><span class="sxs-lookup"><span data-stu-id="2214c-133">In hello search box, type **Workplace by Facebook**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. <span data-ttu-id="2214c-135">Dans le volet de résultats hello, sélectionnez **espace de travail par Facebook**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="2214c-135">In hello results panel, select **Workplace by Facebook**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2214c-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2214c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2214c-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Workplace by Facebook, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="2214c-138">In this section, you configure and test Azure AD single sign-on with Workplace by Facebook based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2214c-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans l’espace de travail par Facebook est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2214c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workplace by Facebook is tooa user in Azure AD.</span></span> <span data-ttu-id="2214c-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans l’espace de travail par Facebook hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="2214c-140">In other words, a link relationship between an Azure AD user and hello related user in Workplace by Facebook needs toobe established.</span></span>

<span data-ttu-id="2214c-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans l’espace de travail par Facebook.</span><span class="sxs-lookup"><span data-stu-id="2214c-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workplace by Facebook.</span></span>

<span data-ttu-id="2214c-142">tooconfigure et test Azure AD l’authentification unique avec l’espace de travail par Facebook, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="2214c-142">tooconfigure and test Azure AD single sign-on with Workplace by Facebook, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2214c-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="2214c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2214c-144">**[Configuration de la fréquence de la réauthentification](#configuring-reauthentication-frequency)**  -tooprompt d’espace de travail tooconfigure pour une vérification SAML.</span><span class="sxs-lookup"><span data-stu-id="2214c-144">**[Configuring Reauthentication Frequency](#configuring-reauthentication-frequency)** - tooconfigure Workplace tooprompt for a SAML check.</span></span>
3. <span data-ttu-id="2214c-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2214c-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="2214c-146">**[Création d’un espace de travail par l’utilisateur de test Facebook](#creating-a-workplace-by-facebook-test-user)**  -toohave un équivalent de Britta Simon dans l’espace de travail par Facebook est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2214c-146">**[Creating a Workplace by Facebook test user](#creating-a-workplace-by-facebook-test-user)** - toohave a counterpart of Britta Simon in Workplace by Facebook that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="2214c-147">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2214c-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="2214c-148">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="2214c-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2214c-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2214c-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2214c-150">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre espace de travail par application Facebook.</span><span class="sxs-lookup"><span data-stu-id="2214c-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workplace by Facebook application.</span></span>

<span data-ttu-id="2214c-151">**tooconfigure Azure AD authentification unique avec l’espace de travail par Facebook, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2214c-151">**tooconfigure Azure AD single sign-on with Workplace by Facebook, perform hello following steps:**</span></span>

1. <span data-ttu-id="2214c-152">Bonjour portail Azure, sur hello **espace de travail par Facebook** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="2214c-152">In hello Azure portal, on hello **Workplace by Facebook** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="2214c-154">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2214c-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="2214c-156">Sur hello **espace de travail par le domaine de Facebook et URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2214c-156">On hello **Workplace by Facebook Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    <span data-ttu-id="2214c-158">a.</span><span class="sxs-lookup"><span data-stu-id="2214c-158">a.</span></span> <span data-ttu-id="2214c-159">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<instancename>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="2214c-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.facebook.com`</span></span>

    <span data-ttu-id="2214c-160">b.</span><span class="sxs-lookup"><span data-stu-id="2214c-160">b.</span></span> <span data-ttu-id="2214c-161">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://www.facebook.com/company/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="2214c-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.facebook.com/company/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2214c-162">Ces valeurs ne sont pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="2214c-162">These values are not hello real.</span></span> <span data-ttu-id="2214c-163">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="2214c-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2214c-164">Contact [espace de travail par équipe de support Facebook Client](https://workplace.fb.com/faq/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="2214c-164">Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) tooget these values.</span></span> 

4. <span data-ttu-id="2214c-165">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2214c-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="2214c-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="2214c-167">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2214c-169">Sur hello **espace de travail par la Configuration de Facebook** , cliquez sur **configurer le poste de travail par Facebook** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="2214c-169">On hello **Workplace by Facebook Configuration** section, click **Configure Workplace by Facebook** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2214c-170">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="2214c-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. <span data-ttu-id="2214c-172">Dans une fenêtre de navigateur web, connexion tooyour espace de travail par site d’entreprise Facebook en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2214c-172">In a different web browser window, login tooyour Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="2214c-173">Dans le cadre du processus d’authentification SAML de hello, espace de travail peut-être utiliser des chaînes de requête de configuration taille dans l’ordre toopass paramètres tooAzure AD too2.5 kilo-octets.</span><span class="sxs-lookup"><span data-stu-id="2214c-173">As part of hello SAML authentication process, Workplace may utilize query strings of up too2.5 kilobytes in size in order toopass parameters tooAzure AD.</span></span>

8. <span data-ttu-id="2214c-174">Bonjour **tableau de bord entreprise**, accédez toohello **authentification** onglet.</span><span class="sxs-lookup"><span data-stu-id="2214c-174">In hello **Company Dashboard**, go toohello **Authentication** tab.</span></span>

9. <span data-ttu-id="2214c-175">Sous **l’authentification SAML**, sélectionnez **SSO uniquement** à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="2214c-175">Under **SAML Authentication**, select **SSO Only** from hello drop-down list.</span></span>

10. <span data-ttu-id="2214c-176">Les valeurs d’entrée hello copiés à partir de **espace de travail par la Configuration de Facebook** section Hello Azure portal dans les champs correspondants hello :</span><span class="sxs-lookup"><span data-stu-id="2214c-176">Input hello values copied from **Workplace by Facebook Configuration** section of hello Azure portal into hello corresponding fields:</span></span>

    *   <span data-ttu-id="2214c-177">Dans **URL SAML** zone de texte, valeur hello coller **-Service URL d’authentification**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2214c-177">In **SAML URL** textbox, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="2214c-178">Dans **zone de texte URL de l’émetteur SAML**, collez la valeur hello **ID d’entité SAML**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2214c-178">In **SAML Issuer URL textbox**, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="2214c-179">Dans **redirection de déconnexion SAML** (facultatif), collez la valeur hello **URL de déconnexion**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2214c-179">In **SAML Logout Redirect** (Optional), paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="2214c-180">Ouvrez votre **certificat codé en base 64** dans le bloc-notes est téléchargé à partir du portail Azure, copiez le contenu de hello de celui-ci dans le Presse-papiers, puis collez-la toothe **certificat SAML** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="2214c-180">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toothe **SAML Certificate** textbox.</span></span>

11. <span data-ttu-id="2214c-181">Vous devrez peut-être tooenter hello Audience URL, URL de destinataire, et les URL des services ACS (Assertion Consumer Service) répertoriées sous hello **Configuration SAML** section.</span><span class="sxs-lookup"><span data-stu-id="2214c-181">You may need tooenter hello Audience URL, Recipient URL, and ACS (Assertion Consumer Service) URL listed under hello **SAML Configuration** section.</span></span>

12. <span data-ttu-id="2214c-182">Faites défiler bas toohello de section de hello, puis cliquez sur hello **Test SSO** bouton.</span><span class="sxs-lookup"><span data-stu-id="2214c-182">Scroll toohello bottom of hello section and click hello **Test SSO** button.</span></span> <span data-ttu-id="2214c-183">Une fenêtre contextuelle apparaît, avec la page de connexion Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2214c-183">This results in a popup window appearing with Azure AD login page presented.</span></span> <span data-ttu-id="2214c-184">Entrez vos informations d’identification dans tooauthenticate normal.</span><span class="sxs-lookup"><span data-stu-id="2214c-184">Enter your credentials in as normal tooauthenticate.</span></span> 

    <span data-ttu-id="2214c-185">**Résolution des problèmes :** adresse de messagerie Vérifiez hello renvoyé à partir d’Azure AD est hello identique hello compte espace de travail que vous êtes connecté.</span><span class="sxs-lookup"><span data-stu-id="2214c-185">**Troubleshooting:** Ensure hello email address being returned back from Azure AD is hello same as hello Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="2214c-186">Une fois le test de hello a été effectuée correctement, faites défiler bas toohello de page de hello, puis cliquez sur hello **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="2214c-186">Once hello test has been completed successfully, scroll toohello bottom of hello page and click hello **Save** button.</span></span>

14. <span data-ttu-id="2214c-187">La page de connexion à Azure AD sera désormais présentée à tous les utilisateurs de Workplace pour qu’ils s’authentifient.</span><span class="sxs-lookup"><span data-stu-id="2214c-187">All users using Workplace will now be presented with Azure AD login page for authentication.</span></span>

15. <span data-ttu-id="2214c-188">**Redirection de déconnexion SAML (facultatif)** -</span><span class="sxs-lookup"><span data-stu-id="2214c-188">**SAML Logout Redirect (optional)** -</span></span> 

    <span data-ttu-id="2214c-189">Vous pouvez choisir toooptionally configurer une Url de déconnexion SAML, qui peut être utilisé toopoint à la page de déconnexion d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2214c-189">You can choose toooptionally configure a SAML Logout Url, which can be used toopoint at Azure AD's logout page.</span></span> <span data-ttu-id="2214c-190">Lorsque ce paramètre est activé et configuré, les utilisateurs hello ne pourra plus être page de déconnexion toohello un espace de travail.</span><span class="sxs-lookup"><span data-stu-id="2214c-190">When this setting is enabled and configured, hello user will no longer be directed toohello Workplace logout page.</span></span> <span data-ttu-id="2214c-191">Au lieu de cela, utilisateur de hello sera redirigé toohello url qui a été ajoutée dans le paramètre de redirection de déconnexion SAML hello.</span><span class="sxs-lookup"><span data-stu-id="2214c-191">Instead, hello user will be redirected toohello url that was added in hello SAML Logout Redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="2214c-192">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="2214c-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2214c-193">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="2214c-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2214c-194">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2214c-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="configuring-reauthentication-frequency"></a><span data-ttu-id="2214c-195">Configuration de la fréquence de réauthentification</span><span class="sxs-lookup"><span data-stu-id="2214c-195">Configuring Reauthentication Frequency</span></span>

<span data-ttu-id="2214c-196">Vous pouvez configurer tooprompt d’espace de travail pour une vérification SAML chaque jour, trois jours, semaine, deux semaines, mois ou jamais.</span><span class="sxs-lookup"><span data-stu-id="2214c-196">You can configure Workplace tooprompt for a SAML check every day, three days, week, two weeks, month or never.</span></span>

> [!NOTE] 
><span data-ttu-id="2214c-197">Hello valeur minimale pour la vérification de SAML hello sur des applications mobiles est définie tooone semaine.</span><span class="sxs-lookup"><span data-stu-id="2214c-197">hello minimum value for hello SAML check on mobile applications is set tooone week.</span></span>

<span data-ttu-id="2214c-198">Vous pouvez également forcer une réinitialisation de tous les utilisateurs à l’aide du bouton de hello SAML : exiger l’authentification SAML pour tous les utilisateurs désormais.</span><span class="sxs-lookup"><span data-stu-id="2214c-198">You can also force a SAML reset for all users using hello button: Require SAML authentication for all users now.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2214c-199">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2214c-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="2214c-200">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="2214c-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="2214c-202">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2214c-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2214c-203">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="2214c-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2214c-205">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2214c-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2214c-207">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="2214c-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2214c-209">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2214c-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2214c-211">a.</span><span class="sxs-lookup"><span data-stu-id="2214c-211">a.</span></span> <span data-ttu-id="2214c-212">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2214c-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2214c-213">b.</span><span class="sxs-lookup"><span data-stu-id="2214c-213">b.</span></span> <span data-ttu-id="2214c-214">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2214c-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2214c-215">c.</span><span class="sxs-lookup"><span data-stu-id="2214c-215">c.</span></span> <span data-ttu-id="2214c-216">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="2214c-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2214c-217">d.</span><span class="sxs-lookup"><span data-stu-id="2214c-217">d.</span></span> <span data-ttu-id="2214c-218">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="2214c-218">Click **Create**.</span></span>
 
### <a name="creating-a-workplace-by-facebook-test-user"></a><span data-ttu-id="2214c-219">Création d’un utilisateur de test Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="2214c-219">Creating a Workplace by Facebook test user</span></span>

<span data-ttu-id="2214c-220">Dans cette section, un utilisateur appelé Britta Simon est créé dans Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="2214c-220">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="2214c-221">Workplace by Facebook prend en charge l’approvisionnement juste-à-temps, qui est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="2214c-221">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="2214c-222">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="2214c-222">There is no action for you in this section.</span></span> <span data-ttu-id="2214c-223">Si un utilisateur n’existe pas dans l’espace de travail par Facebook, un nouveau est créé lors de l’espace de travail de tooaccess par Facebook.</span><span class="sxs-lookup"><span data-stu-id="2214c-223">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt tooaccess Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="2214c-224">Si vous avez besoin de toocreate un utilisateur manuellement, contactez [espace de travail par équipe de support Facebook Client](https://workplace.fb.com/faq/)</span><span class="sxs-lookup"><span data-stu-id="2214c-224">If you need toocreate a user manually, Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/)</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2214c-225">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2214c-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2214c-226">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès des tooWorkplace par Facebook.</span><span class="sxs-lookup"><span data-stu-id="2214c-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkplace by Facebook.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="2214c-228">**tooassign tooWorkplace Britta Simon par Facebook, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2214c-228">**tooassign Britta Simon tooWorkplace by Facebook, perform hello following steps:**</span></span>

1. <span data-ttu-id="2214c-229">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2214c-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="2214c-231">Dans la liste des applications hello, sélectionnez **espace de travail par Facebook**.</span><span class="sxs-lookup"><span data-stu-id="2214c-231">In hello applications list, select **Workplace by Facebook**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="2214c-233">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2214c-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="2214c-235">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2214c-235">Click **Add** button.</span></span> <span data-ttu-id="2214c-236">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2214c-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="2214c-238">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="2214c-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2214c-239">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2214c-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2214c-240">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2214c-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2214c-241">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="2214c-241">Testing single sign-on</span></span>

<span data-ttu-id="2214c-242">Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="2214c-242">If you want tootest your single sign-on settings, open hello Access Panel.</span></span>
<span data-ttu-id="2214c-243">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2214c-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2214c-244">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2214c-244">Additional resources</span></span>

* [<span data-ttu-id="2214c-245">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2214c-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2214c-246">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="2214c-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="2214c-247">Configurer l’approvisionnement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="2214c-247">Configure User Provisioning</span></span>](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

