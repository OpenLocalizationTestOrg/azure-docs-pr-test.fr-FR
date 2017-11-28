---
title: "Didacticiel : Intégration d’Azure Active Directory à Workplace par Facebook | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et l’espace de travail par Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: fd19b3f178a2aee7dd2f204d6d3cf6df8fe6b444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="8466b-103">Didacticiel : Intégration d’Azure Active Directory à Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="8466b-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="8466b-104">Dans ce didacticiel, vous apprendrez comment toointegrate espace de travail par Facebook avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8466b-104">In this tutorial, you learn how toointegrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8466b-105">Intégration d’espace de travail par Facebook à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="8466b-105">Integrating Workplace by Facebook with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8466b-106">Vous pouvez contrôler dans Azure AD qui a tooWorkplace d’accès par Facebook.</span><span class="sxs-lookup"><span data-stu-id="8466b-106">You can control in Azure AD who has access tooWorkplace by Facebook.</span></span>
- <span data-ttu-id="8466b-107">Vous pouvez autoriser les utilisateurs tooautomatically obtenir connecté tooWorkplace par Facebook (SSO) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8466b-107">You can enable your users tooautomatically get signed on tooWorkplace by Facebook (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8466b-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8466b-108">You can manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="8466b-109">Pour plus d’informations sur l’intégration d’applications SaaS (software as a service) à Azure AD, consultez l’article [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8466b-109">For more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8466b-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8466b-110">Prerequisites</span></span>

<span data-ttu-id="8466b-111">tooconfigure intégration d’Azure AD avec l’espace de travail par Facebook, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8466b-111">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="8466b-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="8466b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8466b-113">Un abonnement Workplace by Facebook pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="8466b-113">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="8466b-114">étapes de hello tootest dans ce didacticiel, suivez ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="8466b-114">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="8466b-115">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8466b-115">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8466b-116">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8466b-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8466b-117">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="8466b-117">Scenario description</span></span>
<span data-ttu-id="8466b-118">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="8466b-118">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="8466b-119">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="8466b-119">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8466b-120">Ajoutez l’espace de travail par Facebook à partir de la galerie de hello.</span><span class="sxs-lookup"><span data-stu-id="8466b-120">Add Workplace by Facebook from hello gallery.</span></span>
2. <span data-ttu-id="8466b-121">Configurez et testez l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8466b-121">Configure and test Azure AD single sign-on.</span></span>

## <a name="add-workplace-by-facebook-from-hello-gallery"></a><span data-ttu-id="8466b-122">Ajouter un espace de travail par Facebook à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="8466b-122">Add Workplace by Facebook from hello gallery</span></span>
<span data-ttu-id="8466b-123">intégration de hello tooconfigure du poste de travail par Facebook dans Azure AD, ajouter un espace de travail par Facebook à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="8466b-123">tooconfigure hello integration of Workplace by Facebook into Azure AD, add Workplace by Facebook from hello gallery tooyour list of managed SaaS apps.</span></span>

1. <span data-ttu-id="8466b-124">Bonjour [portail Azure](https://portal.azure.com)hello du volet gauche, dans Sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8466b-124">In hello [Azure portal](https://portal.azure.com), in hello left pane, select **Azure Active Directory**.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="8466b-126">Parcourir trop**des applications d’entreprise** > **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8466b-126">Browse too**Enterprise applications** > **All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="8466b-128">tooadd hello nouvelle application, sélectionnez **nouvelle application** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="8466b-128">tooadd hello new application, select **New application** on hello top of hello dialog box.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="8466b-130">Dans la zone de recherche de hello, tapez **espace de travail par Facebook**, puis sélectionnez **espace de travail par Facebook** à partir des résultats.</span><span class="sxs-lookup"><span data-stu-id="8466b-130">In hello search box, type **Workplace by Facebook**, and select **Workplace by Facebook** from results.</span></span> <span data-ttu-id="8466b-131">Puis sélectionnez **ajouter**, application de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8466b-131">Then select **Add**, tooadd hello application.</span></span>

    ![Espace de travail dans la liste des résultats hello par Facebook](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8466b-133">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8466b-133">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="8466b-134">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Workplace by Facebook, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="8466b-134">In this section, you configure and test Azure AD SSO with Workplace by Facebook, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8466b-135">Pour l’authentification unique toowork, Azure AD doit tooknow quel utilisateur d’équivalent hello dans l’espace de travail par Facebook est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8466b-135">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Workplace by Facebook is tooa user in Azure AD.</span></span> <span data-ttu-id="8466b-136">En d’autres termes, une relation entre des liens entre un utilisateur Azure AD et un utilisateur dans l’espace de travail par Facebook hello doit être établie.</span><span class="sxs-lookup"><span data-stu-id="8466b-136">In other words, a linked relationship between an Azure AD user and hello related user in Workplace by Facebook should be established.</span></span>

<span data-ttu-id="8466b-137">Établir cette relation en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans l’espace de travail par Facebook.</span><span class="sxs-lookup"><span data-stu-id="8466b-137">Establish this relationship by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workplace by Facebook.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8466b-138">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8466b-138">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8466b-139">Dans cette section, vous activez l’authentification unique de Azure AD dans hello portail Azure, et vous configurez l’authentification unique dans votre espace de travail par application Facebook.</span><span class="sxs-lookup"><span data-stu-id="8466b-139">In this section, you enable Azure AD SSO in hello Azure portal, and you configure SSO in your Workplace by Facebook application.</span></span>

1. <span data-ttu-id="8466b-140">Bonjour portail Azure, sur hello **espace de travail par Facebook** page d’intégration d’application, sélectionnez **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="8466b-140">In hello Azure portal, on hello **Workplace by Facebook** application integration page, select **Single sign-on**.</span></span>

    ![Configurer le lien d’authentification unique][4]

2. <span data-ttu-id="8466b-142">Bonjour **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="8466b-142">In hello **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on** tooenable SSO.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="8466b-144">Bonjour **espace de travail par le domaine de Facebook et URL** section, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="8466b-144">In hello **Workplace by Facebook Domain and URLs** section, do hello following:</span></span>

    <span data-ttu-id="8466b-145">a.</span><span class="sxs-lookup"><span data-stu-id="8466b-145">a.</span></span> <span data-ttu-id="8466b-146">Bonjour **URL de connexion** zone de texte, tapez une URL qui utilise hello modèle :`https://<company subdomain>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="8466b-146">In hello **Sign-on URL** text box, type a URL that uses hello following pattern: `https://<company subdomain>.facebook.com`</span></span>

    <span data-ttu-id="8466b-147">b.</span><span class="sxs-lookup"><span data-stu-id="8466b-147">b.</span></span> <span data-ttu-id="8466b-148">Bonjour **identificateur** zone de texte, tapez une URL qui utilise hello modèle :`https://www.facebook.com/company/<scim company id>`</span><span class="sxs-lookup"><span data-stu-id="8466b-148">In hello **Identifier** text box, type a URL that uses hello following pattern: `https://www.facebook.com/company/<scim company id>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="8466b-149">Ces valeurs sont données à titre d’exemple uniquement.</span><span class="sxs-lookup"><span data-stu-id="8466b-149">These values are an example only.</span></span> <span data-ttu-id="8466b-150">Mettre à jour ces valeurs avec l’URL de connexion réel hello et identificateur.</span><span class="sxs-lookup"><span data-stu-id="8466b-150">Update these values with hello actual sign-on URL and identifier.</span></span> <span data-ttu-id="8466b-151">Contact hello [espace de travail par équipe de support Facebook Client](https://workplace.fb.com/faq/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="8466b-151">Contact hello [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) tooget these values.</span></span> 

4. <span data-ttu-id="8466b-152">Bonjour **le certificat de signature SAML** section, sélectionnez **certificat (Base64)**, puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8466b-152">In hello **SAML Signing Certificate** section, select **Certificate (Base64)**, and then save hello certificate file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="8466b-154">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="8466b-154">Select **Save**.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8466b-156">Bonjour **espace de travail par la Configuration de Facebook** section, sélectionnez **configurer le poste de travail par Facebook** tooopen hello **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="8466b-156">In hello **Workplace by Facebook Configuration** section, select **Configure Workplace by Facebook** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="8466b-157">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **aide-mémoire** section.</span><span class="sxs-lookup"><span data-stu-id="8466b-157">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference** section.</span></span>

    ![Configuration de Workplace by Facebook](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. <span data-ttu-id="8466b-159">Dans une fenêtre de navigateur web, connectez-vous tooyour espace de travail par site d’entreprise Facebook en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="8466b-159">In a different web browser window, sign in tooyour Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="8466b-160">Dans le cadre du processus d’authentification SAML de hello, espace de travail pouvez utiliser des chaînes de requête de configuration too2.5 kilo-octets dans la taille de la commande toopass paramètres tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="8466b-160">As part of hello SAML authentication process, Workplace can use query strings of up too2.5 kilobytes in size in order toopass parameters tooAzure AD.</span></span>

8. <span data-ttu-id="8466b-161">Bonjour **tableau de bord entreprise**, accédez toohello **authentification** onglet.</span><span class="sxs-lookup"><span data-stu-id="8466b-161">In hello **Company Dashboard**, go toohello **Authentication** tab.</span></span>

9. <span data-ttu-id="8466b-162">Sous **l’authentification SAML**, sélectionnez **SSO uniquement** à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="8466b-162">Under **SAML Authentication**, select **SSO Only** from hello drop-down list.</span></span>

10. <span data-ttu-id="8466b-163">Entrez les valeurs hello copiés à partir de hello **espace de travail par la Configuration de Facebook** section Hello Azure portal dans les champs correspondants hello :</span><span class="sxs-lookup"><span data-stu-id="8466b-163">Enter hello values copied from hello **Workplace by Facebook Configuration** section of hello Azure portal into hello corresponding fields:</span></span>

    *   <span data-ttu-id="8466b-164">Dans le **URL SAML** zone de texte, valeur hello coller **-Service URL d’authentification**, qui vous avez copié à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8466b-164">In the **SAML URL** text box, paste hello value of **Single Sign-On Service URL**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="8466b-165">Dans le **URL de l’émetteur SAML** zone de texte, valeur hello coller **ID d’entité SAML**, lequel vous avez copié à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8466b-165">In the **SAML Issuer URL** text box, paste hello value of **SAML Entity ID**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="8466b-166">Dans **redirection de déconnexion SAML (facultatif)**, collez la valeur hello **URL de déconnexion**, lequel vous avez copié à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8466b-166">In **SAML Logout Redirect (optional)**, paste hello value of **Sign-Out URL**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="8466b-167">Ouvrez votre **certificat codé en base 64** dans le bloc-notes, téléchargé à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8466b-167">Open your **base-64 encoded certificate** in Notepad, downloaded from hello Azure portal.</span></span> <span data-ttu-id="8466b-168">Copiez le contenu de hello de celui-ci dans le Presse-papiers, puis collez-la toothe **certificat SAML** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="8466b-168">Copy hello content of it into your clipboard, and then paste it toothe **SAML Certificate** text box.</span></span>

11. <span data-ttu-id="8466b-169">Vous devrez peut-être audience de hello tooenter URL destinataire URL et des services ACS (Assertion Consumer Service) URL, répertorié sous hello **Configuration SAML** section.</span><span class="sxs-lookup"><span data-stu-id="8466b-169">You might need tooenter hello audience URL, recipient URL, and ACS (Assertion Consumer Service) URL, listed under hello **SAML Configuration** section.</span></span>

12. <span data-ttu-id="8466b-170">Faites défiler bas toohello de section de hello et sélectionnez **Test SSO**.</span><span class="sxs-lookup"><span data-stu-id="8466b-170">Scroll toohello bottom of hello section, and select **Test SSO**.</span></span> <span data-ttu-id="8466b-171">Une fenêtre contextuelle s’affiche, hello Azure AD-page de connexion.</span><span class="sxs-lookup"><span data-stu-id="8466b-171">A pop-up window appears, with hello Azure AD sign-in page.</span></span> <span data-ttu-id="8466b-172">tooauthenticate, entrez vos informations d’identification comme d’habitude.</span><span class="sxs-lookup"><span data-stu-id="8466b-172">tooauthenticate, enter your credentials as normal.</span></span> <span data-ttu-id="8466b-173">Vérifiez l’adresse de messagerie hello retourné à partir d’Azure AD est hello identique hello compte espace de travail que vous êtes connecté.</span><span class="sxs-lookup"><span data-stu-id="8466b-173">Ensure hello email address returned back from Azure AD is hello same as hello Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="8466b-174">Si le test de hello terminée avec succès, faites défiler bas toohello de page de hello et sélectionnez **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="8466b-174">If hello test has finished successfully, scroll toohello bottom of hello page and select **Save**.</span></span>

14. <span data-ttu-id="8466b-175">La page de connexion à Azure AD sera désormais présentée à tous les utilisateurs de Workplace pour qu’ils s’authentifient.</span><span class="sxs-lookup"><span data-stu-id="8466b-175">Anyone using Workplace is now presented with Azure AD sign-in page for authentication.</span></span>

<span data-ttu-id="8466b-176">Vous pouvez choisir tooconfigure une déconnexion SAML de l’URL, qui peut être toopoint utilisé dans la page de déconnexion hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8466b-176">You can choose tooconfigure a SAML sign out URL, which can be used toopoint at hello Azure AD sign-out page.</span></span> <span data-ttu-id="8466b-177">Lorsque ce paramètre est activé et configuré, hello utilisateur n’est plus redirigée toohello page de déconnexion de poste de travail.</span><span class="sxs-lookup"><span data-stu-id="8466b-177">When this setting is enabled and configured, hello user is no longer directed toohello Workplace sign-out page.</span></span> <span data-ttu-id="8466b-178">Au lieu de cela, utilisateur de hello est redirigé toohello URL qui a été ajoutée dans le paramètre de redirection de déconnexion SAML hello.</span><span class="sxs-lookup"><span data-stu-id="8466b-178">Instead, hello user is redirected toohello URL that was added in hello SAML sign-out redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="8466b-179">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="8466b-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app.</span></span> <span data-ttu-id="8466b-180">Après l’ajout de cette application à partir de hello **Active Directory** > **des Applications d’entreprise** , sélectionnez simplement les hello **Single Sign-On** onglet et hello d’accès incorporé documentation via hello **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="8466b-180">After adding this app from hello **Active Directory** > **Enterprise Applications** section, simply select hello **Single Sign-On** tab, and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8466b-181">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello Bonjour [AD Azure incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="8466b-181">You can read more about hello embedded documentation feature in hello [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="configure-reauthentication-frequency"></a><span data-ttu-id="8466b-182">Configuration de la fréquence de réauthentification</span><span class="sxs-lookup"><span data-stu-id="8466b-182">Configure reauthentication frequency</span></span>

<span data-ttu-id="8466b-183">Vous pouvez configurer tooprompt d’espace de travail pour une vérification SAML chaque jour, trois jours, une semaine, deux semaines, mois, ou jamais.</span><span class="sxs-lookup"><span data-stu-id="8466b-183">You can configure Workplace tooprompt for a SAML check every day, three days, one week, two weeks, one month, or never.</span></span>

> [!NOTE] 
><span data-ttu-id="8466b-184">Hello valeur minimale pour la vérification de SAML hello sur des applications mobiles est définie tooone semaine.</span><span class="sxs-lookup"><span data-stu-id="8466b-184">hello minimum value for hello SAML check on mobile applications is set tooone week.</span></span>

<span data-ttu-id="8466b-185">Vous pouvez également forcer une réinitialisation SAML pour tous les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8466b-185">You can also force a SAML reset for all users.</span></span> <span data-ttu-id="8466b-186">toodo, hello utilisation **requièrent l’authentification SAML pour tous les utilisateurs désormais** bouton.</span><span class="sxs-lookup"><span data-stu-id="8466b-186">toodo this, use hello **Require SAML authentication for all users now** button.</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8466b-187">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8466b-187">Create an Azure AD test user</span></span>
<span data-ttu-id="8466b-188">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="8466b-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

1. <span data-ttu-id="8466b-190">Bonjour **portail Azure**hello du volet gauche, dans Sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8466b-190">In hello **Azure portal**, in hello left pane, select **Azure Active Directory**.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8466b-192">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis sélectionnez **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8466b-192">toodisplay hello list of users, go too**Users and groups**, and select **All users**.</span></span>
    
    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8466b-194">tooopen hello **utilisateur** boîte de dialogue, sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8466b-194">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8466b-196">Bonjour **utilisateur** boîte de dialogue zone, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="8466b-196">In hello **User** dialog box, do hello following:</span></span>
 
    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8466b-198">a.</span><span class="sxs-lookup"><span data-stu-id="8466b-198">a.</span></span> <span data-ttu-id="8466b-199">Bonjour **nom** zone de texte, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8466b-199">In hello **Name** text box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8466b-200">b.</span><span class="sxs-lookup"><span data-stu-id="8466b-200">b.</span></span> <span data-ttu-id="8466b-201">Bonjour **nom d’utilisateur** zone de texte, hello de type **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8466b-201">In hello **User name** text box, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8466b-202">c.</span><span class="sxs-lookup"><span data-stu-id="8466b-202">c.</span></span> <span data-ttu-id="8466b-203">Sélectionnez **Afficher le mot de passe** et prenez-en note.</span><span class="sxs-lookup"><span data-stu-id="8466b-203">Select **Show Password**, and write it down.</span></span>

    <span data-ttu-id="8466b-204">d.</span><span class="sxs-lookup"><span data-stu-id="8466b-204">d.</span></span> <span data-ttu-id="8466b-205">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="8466b-205">Select **Create**.</span></span>
 
### <a name="create-a-workplace-by-facebook-test-user"></a><span data-ttu-id="8466b-206">Création d’un utilisateur de test Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="8466b-206">Create a Workplace by Facebook test user</span></span>

<span data-ttu-id="8466b-207">Dans cette section, un utilisateur appelé Britta Simon est créé dans Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="8466b-207">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="8466b-208">Workplace by Facebook prend en charge l’approvisionnement juste-à-temps, qui est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="8466b-208">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="8466b-209">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="8466b-209">There is no action for you in this section.</span></span> <span data-ttu-id="8466b-210">Si un utilisateur n’existe pas dans l’espace de travail par Facebook, un nouveau est créé lors de l’espace de travail de tooaccess par Facebook.</span><span class="sxs-lookup"><span data-stu-id="8466b-210">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt tooaccess Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="8466b-211">Si vous avez besoin de toocreate un utilisateur manuellement, contactez hello [espace de travail par équipe de support Facebook Client](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="8466b-211">If you need toocreate a user manually, contact hello [Workplace by Facebook Client support team](https://workplace.fb.com/faq/).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="8466b-212">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8466b-212">Assign hello Azure AD test user</span></span>

<span data-ttu-id="8466b-213">Dans cette section, vous activez Britta Simon toouse Azure SSO en accordant l’accès des tooWorkplace par Facebook.</span><span class="sxs-lookup"><span data-stu-id="8466b-213">In this section, you enable Britta Simon toouse Azure SSO by granting access tooWorkplace by Facebook.</span></span>

![Affecter des utilisateurs][200] 

1. <span data-ttu-id="8466b-215">Bonjour Azure afficher les applications de portail, ouvrez hello.</span><span class="sxs-lookup"><span data-stu-id="8466b-215">In hello Azure portal, open hello applications view.</span></span> <span data-ttu-id="8466b-216">Atteindre la vue de répertoire toohello, accédez trop**des applications d’entreprise**, puis sélectionnez **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8466b-216">Go toohello directory view, go too**Enterprise applications**, and then select **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="8466b-218">Dans la liste des applications hello, sélectionnez **espace de travail par Facebook**.</span><span class="sxs-lookup"><span data-stu-id="8466b-218">In hello applications list, select **Workplace by Facebook**.</span></span>

    ![Hello, espace de travail par un lien de Facebook dans la liste des Applications hello](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="8466b-220">Dans le menu hello hello gauche, sélectionnez **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8466b-220">In hello menu on hello left, select **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202] 

4. <span data-ttu-id="8466b-222">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8466b-222">Select **Add**.</span></span> <span data-ttu-id="8466b-223">Ensuite, dans hello **ajouter l’affectation** volet, sélectionnez **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8466b-223">Then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="8466b-225">Bonjour **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="8466b-225">In hello **Users and groups** dialog box, select **Britta Simon** in hello users list.</span></span>

6. <span data-ttu-id="8466b-226">Bonjour **utilisateurs et groupes** boîte de dialogue, sélectionnez **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="8466b-226">In hello **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="8466b-227">Bonjour **ajouter l’affectation** boîte de dialogue, sélectionnez **affecter**.</span><span class="sxs-lookup"><span data-stu-id="8466b-227">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8466b-228">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="8466b-228">Test single sign-on</span></span>

<span data-ttu-id="8466b-229">Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="8466b-229">If you want tootest your SSO settings, open hello Access Panel.</span></span>
<span data-ttu-id="8466b-230">Pour plus d’informations, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8466b-230">For more information, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="8466b-231">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8466b-231">Next steps</span></span>

* <span data-ttu-id="8466b-232">Consultez hello [liste des didacticiels sur la façon de toointegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="8466b-232">See hello [list of tutorials on how toointegrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md).</span></span>
* <span data-ttu-id="8466b-233">Voir [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8466b-233">Read [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>
* <span data-ttu-id="8466b-234">En savoir plus sur la façon trop[configuration d’utilisateur](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="8466b-234">Learn more about how too[configure user provisioning](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span></span>



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

