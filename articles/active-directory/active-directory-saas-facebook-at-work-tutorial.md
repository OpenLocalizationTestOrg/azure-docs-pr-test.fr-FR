---
title: "Didacticiel : Intégration d’Azure Active Directory à Workplace par Facebook | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Workplace by Facebook."
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
ms.openlocfilehash: 27e62a00832484667117d8718db9f2fc05e2f4e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="64766-103">Didacticiel : Intégration d’Azure Active Directory à Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="64766-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="64766-104">Dans ce didacticiel, vous allez apprendre à intégrer Workplace by Facebook à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="64766-104">In this tutorial, you learn how to integrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="64766-105">L’intégration de Workplace by Facebook à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="64766-105">Integrating Workplace by Facebook with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="64766-106">Dans Azure AD, vous pouvez contrôler qui a accès à Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="64766-106">You can control in Azure AD who has access to Workplace by Facebook.</span></span>
- <span data-ttu-id="64766-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Workplace by Facebook (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64766-107">You can enable your users to automatically get signed on to Workplace by Facebook (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="64766-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="64766-108">You can manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="64766-109">Pour plus d’informations sur l’intégration d’applications SaaS (software as a service) à Azure AD, consultez l’article [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="64766-109">For more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64766-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="64766-110">Prerequisites</span></span>

<span data-ttu-id="64766-111">Pour configurer l’intégration d’Azure AD avec Workplace by Facebook, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="64766-111">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="64766-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="64766-112">An Azure AD subscription</span></span>
- <span data-ttu-id="64766-113">Un abonnement Workplace by Facebook pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="64766-113">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="64766-114">Pour tester la procédure de ce didacticiel, suivez les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="64766-114">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="64766-115">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="64766-115">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="64766-116">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="64766-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="64766-117">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="64766-117">Scenario description</span></span>
<span data-ttu-id="64766-118">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="64766-118">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="64766-119">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="64766-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="64766-120">Ajoutez Workplace by Facebook à partir de la galerie.</span><span class="sxs-lookup"><span data-stu-id="64766-120">Add Workplace by Facebook from the gallery.</span></span>
2. <span data-ttu-id="64766-121">Configurez et testez l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64766-121">Configure and test Azure AD single sign-on.</span></span>

## <a name="add-workplace-by-facebook-from-the-gallery"></a><span data-ttu-id="64766-122">Ajout de Workplace by Facebook à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="64766-122">Add Workplace by Facebook from the gallery</span></span>
<span data-ttu-id="64766-123">Pour configurer l’intégration de Workplace by Facebook avec Azure AD, ajoutez Workplace by Facebook à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="64766-123">To configure the integration of Workplace by Facebook into Azure AD, add Workplace by Facebook from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="64766-124">Dans le volet gauche du [portail Azure](https://portal.azure.com), sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="64766-124">In the [Azure portal](https://portal.azure.com), in the left pane, select **Azure Active Directory**.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="64766-126">Accédez à **Applications d’entreprise** > **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="64766-126">Browse to **Enterprise applications** > **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="64766-128">Pour ajouter une nouvelle application, sélectionnez **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="64766-128">To add the new application, select **New application** on the top of the dialog box.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="64766-130">Dans la zone de recherche, saisissez **Workspace by Facebook**, puis sélectionnez **Workspace by Facebook** dans les résultats.</span><span class="sxs-lookup"><span data-stu-id="64766-130">In the search box, type **Workplace by Facebook**, and select **Workplace by Facebook** from results.</span></span> <span data-ttu-id="64766-131">Sélectionnez ensuite **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="64766-131">Then select **Add**, to add the application.</span></span>

    ![Workplace by Facebook dans la liste des résultats](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="64766-133">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="64766-133">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="64766-134">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Workplace by Facebook, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="64766-134">In this section, you configure and test Azure AD SSO with Workplace by Facebook, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="64766-135">Pour que l’authentification unique fonctionne, Azure AD doit connaître l’utilisateur Workplace by Facebook équivalant à un utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64766-135">For SSO to work, Azure AD needs to know what the counterpart user in Workplace by Facebook is to a user in Azure AD.</span></span> <span data-ttu-id="64766-136">En d’autres termes, une relation doit être établie entre l’utilisateur Azure AD et l’utilisateur Workplace by Facebook associé.</span><span class="sxs-lookup"><span data-stu-id="64766-136">In other words, a linked relationship between an Azure AD user and the related user in Workplace by Facebook should be established.</span></span>

<span data-ttu-id="64766-137">Pour cela, assignez la valeur du **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="64766-137">Establish this relationship by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workplace by Facebook.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="64766-138">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="64766-138">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="64766-139">Dans cette section, vous allez activer l’authentification unique Azure AD sur le portail Azure et configurer l’authentification unique dans votre application Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="64766-139">In this section, you enable Azure AD SSO in the Azure portal, and you configure SSO in your Workplace by Facebook application.</span></span>

1. <span data-ttu-id="64766-140">Sur le portail Azure, à la page d’intégration de l’application **Workplace by Facebook**, sélectionnez **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="64766-140">In the Azure portal, on the **Workplace by Facebook** application integration page, select **Single sign-on**.</span></span>

    ![Configurer le lien d’authentification unique][4]

2. <span data-ttu-id="64766-142">Dans la boîte de dialogue **Authentification unique**, sous la zone **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="64766-142">In the **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on** to enable SSO.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="64766-144">Dans la section **Domaine et URL Workplace by Facebook**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="64766-144">In the **Workplace by Facebook Domain and URLs** section, do the following:</span></span>

    <span data-ttu-id="64766-145">a.</span><span class="sxs-lookup"><span data-stu-id="64766-145">a.</span></span> <span data-ttu-id="64766-146">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<company subdomain>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="64766-146">In the **Sign-on URL** text box, type a URL that uses the following pattern: `https://<company subdomain>.facebook.com`</span></span>

    <span data-ttu-id="64766-147">b.</span><span class="sxs-lookup"><span data-stu-id="64766-147">b.</span></span> <span data-ttu-id="64766-148">Dans la zone de texte **Identificateur**, saisissez une URL au format suivant : `https://www.facebook.com/company/<scim company id>`</span><span class="sxs-lookup"><span data-stu-id="64766-148">In the **Identifier** text box, type a URL that uses the following pattern: `https://www.facebook.com/company/<scim company id>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="64766-149">Ces valeurs sont données à titre d’exemple uniquement.</span><span class="sxs-lookup"><span data-stu-id="64766-149">These values are an example only.</span></span> <span data-ttu-id="64766-150">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="64766-150">Update these values with the actual sign-on URL and identifier.</span></span> <span data-ttu-id="64766-151">Pour obtenir ces valeurs, contactez l’[équipe de prise en charge des clients Workplace by Facebook](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="64766-151">Contact the [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) to get these values.</span></span> 

4. <span data-ttu-id="64766-152">Dans la section **Certificat de signature SAML**, sélectionnez **Certificat (Base64)**, puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="64766-152">In the **SAML Signing Certificate** section, select **Certificate (Base64)**, and then save the certificate file on your computer.</span></span>

    ![Lien Téléchargement de certificat](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="64766-154">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="64766-154">Select **Save**.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="64766-156">Dans la section **Configuration de Workplace by Facebook**, sélectionnez **Configurer Workplace by Facebook** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="64766-156">In the **Workplace by Facebook Configuration** section, select **Configure Workplace by Facebook** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="64766-157">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la section **Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="64766-157">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference** section.</span></span>

    ![Configuration de Workplace by Facebook](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. <span data-ttu-id="64766-159">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise Workplace by Facebook en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="64766-159">In a different web browser window, sign in to your Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="64766-160">Dans le cadre du processus d’authentification SAML, Workplace peut utiliser des chaînes de requête d’une taille pouvant aller jusqu’à 2,5 Ko pour transmettre des paramètres à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64766-160">As part of the SAML authentication process, Workplace can use query strings of up to 2.5 kilobytes in size in order to pass parameters to Azure AD.</span></span>

8. <span data-ttu-id="64766-161">Dans **Company Dashboard**, accédez à l’onglet **Authentication**.</span><span class="sxs-lookup"><span data-stu-id="64766-161">In the **Company Dashboard**, go to the **Authentication** tab.</span></span>

9. <span data-ttu-id="64766-162">Sous **SAML Authentication**, sélectionnez **SSO Only** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="64766-162">Under **SAML Authentication**, select **SSO Only** from the drop-down list.</span></span>

10. <span data-ttu-id="64766-163">Entrez les valeurs copiées à partir de la section **Configuration de Workplace by Facebook** du portail Azure dans les champs correspondants :</span><span class="sxs-lookup"><span data-stu-id="64766-163">Enter the values copied from the **Workplace by Facebook Configuration** section of the Azure portal into the corresponding fields:</span></span>

    *   <span data-ttu-id="64766-164">Dans la zone de texte **SAML URL**, collez la valeur de l’**URL du service d’authentification unique**, copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="64766-164">In the **SAML URL** text box, paste the value of **Single Sign-On Service URL**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="64766-165">Dans la zone de texte **SAML Issuer URL** (URL de l’émetteur SAML), collez la valeur de l’**ID d’entité SAML**, que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="64766-165">In the **SAML Issuer URL** text box, paste the value of **SAML Entity ID**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="64766-166">Dans **SAML Logout Redirect** (Redirection de déconnexion SAML) (facultatif), collez la valeur de l’**URL de déconnexion**, que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="64766-166">In **SAML Logout Redirect (optional)**, paste the value of **Sign-Out URL**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="64766-167">Dans le bloc-notes, ouvrez votre **certificat codé en base 64**, téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="64766-167">Open your **base-64 encoded certificate** in Notepad, downloaded from the Azure portal.</span></span> <span data-ttu-id="64766-168">Copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **Certificat SAML**.</span><span class="sxs-lookup"><span data-stu-id="64766-168">Copy the content of it into your clipboard, and then paste it to the **SAML Certificate** text box.</span></span>

11. <span data-ttu-id="64766-169">Vous devrez peut-être entrer l’URL d’audience, l’URL de destinataire et l’URL du service consommateur d’assertion (ACS), répertoriées sous la section **SAML Configuration** (Configuration SAML).</span><span class="sxs-lookup"><span data-stu-id="64766-169">You might need to enter the audience URL, recipient URL, and ACS (Assertion Consumer Service) URL, listed under the **SAML Configuration** section.</span></span>

12. <span data-ttu-id="64766-170">Faites défiler l’affichage jusqu’au bas de la section et sélectionnez **Test SSO**.</span><span class="sxs-lookup"><span data-stu-id="64766-170">Scroll to the bottom of the section, and select **Test SSO**.</span></span> <span data-ttu-id="64766-171">Une fenêtre indépendante contenant la page de connexion à Azure AD s’affiche.</span><span class="sxs-lookup"><span data-stu-id="64766-171">A pop-up window appears, with the Azure AD sign-in page.</span></span> <span data-ttu-id="64766-172">Pour vous authentifier, entrez vos informations d’identification comme à votre habitude.</span><span class="sxs-lookup"><span data-stu-id="64766-172">To authenticate, enter your credentials as normal.</span></span> <span data-ttu-id="64766-173">Vérifiez que l’adresse e-mail retournée par Azure AD est identique au compte Workplace avec lequel vous êtes connecté.</span><span class="sxs-lookup"><span data-stu-id="64766-173">Ensure the email address returned back from Azure AD is the same as the Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="64766-174">Si le test se termine avec succès, faites défiler la page vers le bas et sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="64766-174">If the test has finished successfully, scroll to the bottom of the page and select **Save**.</span></span>

14. <span data-ttu-id="64766-175">La page de connexion à Azure AD sera désormais présentée à tous les utilisateurs de Workplace pour qu’ils s’authentifient.</span><span class="sxs-lookup"><span data-stu-id="64766-175">Anyone using Workplace is now presented with Azure AD sign-in page for authentication.</span></span>

<span data-ttu-id="64766-176">Vous pouvez choisir de configurer une URL de déconnexion SAML, qui peut être utilisée pour pointer vers la page de déconnexion d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64766-176">You can choose to configure a SAML sign out URL, which can be used to point at the Azure AD sign-out page.</span></span> <span data-ttu-id="64766-177">Quand ce paramètre est activé et configuré, l’utilisateur n’est plus dirigé vers la page de déconnexion de Workplace.</span><span class="sxs-lookup"><span data-stu-id="64766-177">When this setting is enabled and configured, the user is no longer directed to the Workplace sign-out page.</span></span> <span data-ttu-id="64766-178">Au lieu de cela, il est redirigé vers l’URL qui a été ajoutée dans le paramètre de redirection de déconnexion SAML.</span><span class="sxs-lookup"><span data-stu-id="64766-178">Instead, the user is redirected to the URL that was added in the SAML sign-out redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="64766-179">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="64766-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app.</span></span> <span data-ttu-id="64766-180">Après avoir ajouté cette application à partir de la section **Active Directory** > **Applications d’entreprise**, sélectionnez simplement l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="64766-180">After adding this app from the **Active Directory** > **Enterprise Applications** section, simply select the **Single Sign-On** tab, and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="64766-181">Pour en savoir plus sur la fonctionnalité de documentation incorporée, consultez [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="64766-181">You can read more about the embedded documentation feature in the [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="configure-reauthentication-frequency"></a><span data-ttu-id="64766-182">Configuration de la fréquence de réauthentification</span><span class="sxs-lookup"><span data-stu-id="64766-182">Configure reauthentication frequency</span></span>

<span data-ttu-id="64766-183">Vous pouvez configurer Workplace pour demander une vérification SAML chaque jour, tous les trois jours, toutes les semaines, toutes les deux semaines, tous les mois ou jamais.</span><span class="sxs-lookup"><span data-stu-id="64766-183">You can configure Workplace to prompt for a SAML check every day, three days, one week, two weeks, one month, or never.</span></span>

> [!NOTE] 
><span data-ttu-id="64766-184">La valeur minimale pour la vérification SAML sur les applications mobiles est toutes les semaines.</span><span class="sxs-lookup"><span data-stu-id="64766-184">The minimum value for the SAML check on mobile applications is set to one week.</span></span>

<span data-ttu-id="64766-185">Vous pouvez également forcer une réinitialisation SAML pour tous les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="64766-185">You can also force a SAML reset for all users.</span></span> <span data-ttu-id="64766-186">Pour ce faire, utilisez le bouton **Require SAML authentication for all users now** (Demander une authentification SAML pour tous les utilisateurs).</span><span class="sxs-lookup"><span data-stu-id="64766-186">To do this, use the **Require SAML authentication for all users now** button.</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="64766-187">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="64766-187">Create an Azure AD test user</span></span>
<span data-ttu-id="64766-188">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="64766-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

1. <span data-ttu-id="64766-190">Dans le volet gauche du **portail Azure**, sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="64766-190">In the **Azure portal**, in the left pane, select **Azure Active Directory**.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="64766-192">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, et sélectionnez **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="64766-192">To display the list of users, go to **Users and groups**, and select **All users**.</span></span>
    
    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="64766-194">Pour ouvrir la boîte de dialogue **Utilisateur**, sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="64766-194">To open the **User** dialog box, select **Add**.</span></span>
 
    ![Bouton Ajouter](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="64766-196">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="64766-196">In the **User** dialog box, do the following:</span></span>
 
    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="64766-198">a.</span><span class="sxs-lookup"><span data-stu-id="64766-198">a.</span></span> <span data-ttu-id="64766-199">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="64766-199">In the **Name** text box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="64766-200">b.</span><span class="sxs-lookup"><span data-stu-id="64766-200">b.</span></span> <span data-ttu-id="64766-201">Dans la zone de texte **Nom d’utilisateur**, saisissez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="64766-201">In the **User name** text box, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="64766-202">c.</span><span class="sxs-lookup"><span data-stu-id="64766-202">c.</span></span> <span data-ttu-id="64766-203">Sélectionnez **Afficher le mot de passe** et prenez-en note.</span><span class="sxs-lookup"><span data-stu-id="64766-203">Select **Show Password**, and write it down.</span></span>

    <span data-ttu-id="64766-204">d.</span><span class="sxs-lookup"><span data-stu-id="64766-204">d.</span></span> <span data-ttu-id="64766-205">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="64766-205">Select **Create**.</span></span>
 
### <a name="create-a-workplace-by-facebook-test-user"></a><span data-ttu-id="64766-206">Création d’un utilisateur de test Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="64766-206">Create a Workplace by Facebook test user</span></span>

<span data-ttu-id="64766-207">Dans cette section, un utilisateur appelé Britta Simon est créé dans Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="64766-207">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="64766-208">Workplace by Facebook prend en charge l’approvisionnement juste-à-temps, qui est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="64766-208">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="64766-209">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="64766-209">There is no action for you in this section.</span></span> <span data-ttu-id="64766-210">S’il n’existe pas d’utilisateur dans Workplace by Facebook, un nouvel utilisateur est créé quand vous tentez d’accéder à Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="64766-210">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt to access Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="64766-211">Si vous avez besoin de créer un utilisateur manuellement, contactez l’[équipe de prise en charge des clients Workplace by Facebook](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="64766-211">If you need to create a user manually, contact the [Workplace by Facebook Client support team](https://workplace.fb.com/faq/).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="64766-212">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="64766-212">Assign the Azure AD test user</span></span>

<span data-ttu-id="64766-213">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="64766-213">In this section, you enable Britta Simon to use Azure SSO by granting access to Workplace by Facebook.</span></span>

![Affecter des utilisateurs][200] 

1. <span data-ttu-id="64766-215">Dans le portail Azure, ouvrez la vue des applications.</span><span class="sxs-lookup"><span data-stu-id="64766-215">In the Azure portal, open the applications view.</span></span> <span data-ttu-id="64766-216">Accédez à la vue des répertoires, puis sélectionnez **Applications d’entreprise** et **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="64766-216">Go to the directory view, go to **Enterprise applications**, and then select **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="64766-218">Dans la liste des applications, sélectionnez **Workplace by Facebook**.</span><span class="sxs-lookup"><span data-stu-id="64766-218">In the applications list, select **Workplace by Facebook**.</span></span>

    ![Lien Workplace by Facebook dans la liste des applications](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="64766-220">Dans le menu de gauche, sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="64766-220">In the menu on the left, select **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202] 

4. <span data-ttu-id="64766-222">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="64766-222">Select **Add**.</span></span> <span data-ttu-id="64766-223">Ensuite, dans le volet **Ajouter une attribution**, sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="64766-223">Then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="64766-225">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="64766-225">In the **Users and groups** dialog box, select **Britta Simon** in the users list.</span></span>

6. <span data-ttu-id="64766-226">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="64766-226">In the **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="64766-227">Dans la boîte de dialogue **Ajouter une attribution**, sélectionnez **Affecter**.</span><span class="sxs-lookup"><span data-stu-id="64766-227">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="64766-228">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="64766-228">Test single sign-on</span></span>

<span data-ttu-id="64766-229">Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="64766-229">If you want to test your SSO settings, open the Access Panel.</span></span>
<span data-ttu-id="64766-230">Pour plus d’informations, consultez [Présentation du volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="64766-230">For more information, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="64766-231">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="64766-231">Next steps</span></span>

* <span data-ttu-id="64766-232">Consultez la [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="64766-232">See the [list of tutorials on how to integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md).</span></span>
* <span data-ttu-id="64766-233">Voir [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="64766-233">Read [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>
* <span data-ttu-id="64766-234">En savoir plus sur la [configuration de l’approvisionnement d’utilisateurs](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="64766-234">Learn more about how to [configure user provisioning](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span></span>



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

