---
title: "Didacticiel : Intégration d’Azure Active Directory à Workplace par Facebook | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Workplace by Facebook."
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
ms.openlocfilehash: 1590a66f215f0c093d24ff602c0ad951ba1e1eea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="170a0-103">Didacticiel : Intégration d’Azure Active Directory à Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="170a0-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="170a0-104">Dans ce didacticiel, vous allez apprendre à intégrer Workplace by Facebook à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="170a0-104">In this tutorial, you learn how to integrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="170a0-105">L’intégration de Workplace by Facebook à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="170a0-105">Integrating Workplace by Facebook with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="170a0-106">Dans Azure AD, vous pouvez contrôler qui a accès à Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="170a0-106">You can control in Azure AD who has access to Workplace by Facebook</span></span>
- <span data-ttu-id="170a0-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Workplace by Facebook (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="170a0-107">You can enable your users to automatically get signed-on to Workplace by Facebook (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="170a0-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="170a0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="170a0-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="170a0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="170a0-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="170a0-110">Prerequisites</span></span>

<span data-ttu-id="170a0-111">Pour configurer l’intégration d’Azure AD avec Workplace by Facebook, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="170a0-111">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="170a0-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="170a0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="170a0-113">Un abonnement Workplace by Facebook pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="170a0-113">A Workplace by Facebook single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="170a0-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="170a0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="170a0-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="170a0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="170a0-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="170a0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="170a0-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="170a0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="170a0-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="170a0-118">Scenario description</span></span>
<span data-ttu-id="170a0-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="170a0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="170a0-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="170a0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="170a0-121">Ajout de Workplace by Facebook à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="170a0-121">Adding Workplace by Facebook from the gallery</span></span>
2. <span data-ttu-id="170a0-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="170a0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workplace-by-facebook-from-the-gallery"></a><span data-ttu-id="170a0-123">Ajout de Workplace by Facebook à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="170a0-123">Adding Workplace by Facebook from the gallery</span></span>
<span data-ttu-id="170a0-124">Pour configurer l’intégration de Workplace by Facebook à Azure AD, vous devez ajouter Workplace by Facebook à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="170a0-124">To configure the integration of Workplace by Facebook into Azure AD, you need to add Workplace by Facebook from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="170a0-125">**Pour ajouter Workplace by Facebook à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="170a0-125">**To add Workplace by Facebook from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="170a0-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="170a0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="170a0-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="170a0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="170a0-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="170a0-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="170a0-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="170a0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="170a0-133">Dans la zone de recherche, tapez **Workplace by Facebook**.</span><span class="sxs-lookup"><span data-stu-id="170a0-133">In the search box, type **Workplace by Facebook**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. <span data-ttu-id="170a0-135">Dans le volet de résultats, sélectionnez **Workplace by Facebook**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="170a0-135">In the results panel, select **Workplace by Facebook**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="170a0-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="170a0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="170a0-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Workplace by Facebook, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="170a0-138">In this section, you configure and test Azure AD single sign-on with Workplace by Facebook based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="170a0-139">Pour que l’authentification unique fonctionne, Azure AD doit connaître l’utilisateur Workplace by Facebook équivalent à un utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="170a0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workplace by Facebook is to a user in Azure AD.</span></span> <span data-ttu-id="170a0-140">En d’autres termes, une relation doit être établie entre l’utilisateur Azure AD et l’utilisateur Workplace by Facebook associé.</span><span class="sxs-lookup"><span data-stu-id="170a0-140">In other words, a link relationship between an Azure AD user and the related user in Workplace by Facebook needs to be established.</span></span>

<span data-ttu-id="170a0-141">Pour cela, assignez la valeur du **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="170a0-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workplace by Facebook.</span></span>

<span data-ttu-id="170a0-142">Pour configurer et tester l’authentification unique Azure AD avec Workplace by Facebook, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="170a0-142">To configure and test Azure AD single sign-on with Workplace by Facebook, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="170a0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="170a0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="170a0-144">**[Configuration de la fréquence de réauthentification](#configuring-reauthentication-frequency)** pour configurer Workplace pour qu’il affiche une invite de vérification SAML.</span><span class="sxs-lookup"><span data-stu-id="170a0-144">**[Configuring Reauthentication Frequency](#configuring-reauthentication-frequency)** - to configure Workplace to prompt for a SAML check.</span></span>
3. <span data-ttu-id="170a0-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="170a0-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="170a0-146">**[Création d’un utilisateur de test Workplace by Facebook](#creating-a-workplace-by-facebook-test-user)** pour avoir un équivalent de Britta Simon dans Workplace by Facebook, associé à sa représentation dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="170a0-146">**[Creating a Workplace by Facebook test user](#creating-a-workplace-by-facebook-test-user)** - to have a counterpart of Britta Simon in Workplace by Facebook that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="170a0-147">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="170a0-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="170a0-148">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="170a0-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="170a0-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="170a0-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="170a0-150">Dans cette section, vous allez activer l’authentification unique Azure AD sur le portail Azure et configurer l’authentification unique dans votre application Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="170a0-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workplace by Facebook application.</span></span>

<span data-ttu-id="170a0-151">**Pour configurer l’authentification unique Azure AD avec Workplace by Facebook, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="170a0-151">**To configure Azure AD single sign-on with Workplace by Facebook, perform the following steps:**</span></span>

1. <span data-ttu-id="170a0-152">Sur le portail Azure, à la page d’intégration de l’application **Workplace by Facebook**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="170a0-152">In the Azure portal, on the **Workplace by Facebook** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="170a0-154">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="170a0-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="170a0-156">Dans la section **Domaine et URL Workplace by Facebook**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="170a0-156">On the **Workplace by Facebook Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    <span data-ttu-id="170a0-158">a.</span><span class="sxs-lookup"><span data-stu-id="170a0-158">a.</span></span> <span data-ttu-id="170a0-159">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<instancename>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="170a0-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.facebook.com`</span></span>

    <span data-ttu-id="170a0-160">b.</span><span class="sxs-lookup"><span data-stu-id="170a0-160">b.</span></span> <span data-ttu-id="170a0-161">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://www.facebook.com/company/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="170a0-161">In the **Identifier** textbox, type a URL using the following pattern: `https://www.facebook.com/company/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="170a0-162">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="170a0-162">These values are not the real.</span></span> <span data-ttu-id="170a0-163">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="170a0-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="170a0-164">Pour obtenir ces valeurs, contactez l’[équipe de prise en charge des clients Workplace by Facebook](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="170a0-164">Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) to get these values.</span></span> 

4. <span data-ttu-id="170a0-165">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="170a0-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="170a0-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="170a0-167">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="170a0-169">Dans la section **Configuration de Workplace by Facebook**, cliquez sur **Configurer Workplace by Facebook** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="170a0-169">On the **Workplace by Facebook Configuration** section, click **Configure Workplace by Facebook** to open **Configure sign-on** window.</span></span> <span data-ttu-id="170a0-170">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="170a0-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. <span data-ttu-id="170a0-172">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise Workplace by Facebook en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="170a0-172">In a different web browser window, login to your Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="170a0-173">Dans le cadre du processus d’authentification SAML, Workplace peut utiliser des chaînes de requête d’une taille pouvant aller jusqu’à 2,5 Ko pour transmettre des paramètres à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="170a0-173">As part of the SAML authentication process, Workplace may utilize query strings of up to 2.5 kilobytes in size in order to pass parameters to Azure AD.</span></span>

8. <span data-ttu-id="170a0-174">Dans **Company Dashboard**, accédez à l’onglet **Authentication**.</span><span class="sxs-lookup"><span data-stu-id="170a0-174">In the **Company Dashboard**, go to the **Authentication** tab.</span></span>

9. <span data-ttu-id="170a0-175">Sous **SAML Authentication**, sélectionnez **SSO Only** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="170a0-175">Under **SAML Authentication**, select **SSO Only** from the drop-down list.</span></span>

10. <span data-ttu-id="170a0-176">Entrez les valeurs copiées à partir de la section **Configuration de Workplace by Facebook** du portail Azure dans les champs correspondants :</span><span class="sxs-lookup"><span data-stu-id="170a0-176">Input the values copied from **Workplace by Facebook Configuration** section of the Azure portal into the corresponding fields:</span></span>

    *   <span data-ttu-id="170a0-177">Dans la zone de texte **SAML URL**, collez la valeur de l’**URL du service d’authentification unique**, copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="170a0-177">In **SAML URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="170a0-178">Dans la zone de texte **SAML Issuer URL** (URL de l’émetteur SAML), collez la valeur de l’**ID d’entité SAML**, que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="170a0-178">In **SAML Issuer URL textbox**, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="170a0-179">Dans **SAML Logout Redirect** (Redirection de déconnexion SAML) (facultatif), collez la valeur de l’**URL de déconnexion**, que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="170a0-179">In **SAML Logout Redirect** (Optional), paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="170a0-180">Ouvrez dans le Bloc-notes votre **certificat codé en base 64**, téléchargé à partir du portail Azure, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **SAML Certificate** (Certificat SAML).</span><span class="sxs-lookup"><span data-stu-id="170a0-180">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **SAML Certificate** textbox.</span></span>

11. <span data-ttu-id="170a0-181">Vous devrez peut-être entrer l’URL d’audience, l’URL de destinataire et l’URL du service consommateur d’assertion (ACS), répertoriées sous la section **SAML Configuration** (Configuration SAML).</span><span class="sxs-lookup"><span data-stu-id="170a0-181">You may need to enter the Audience URL, Recipient URL, and ACS (Assertion Consumer Service) URL listed under the **SAML Configuration** section.</span></span>

12. <span data-ttu-id="170a0-182">Faites défiler l’affichage jusqu’au bas de la section et cliquez sur le bouton **Test SSO**.</span><span class="sxs-lookup"><span data-stu-id="170a0-182">Scroll to the bottom of the section and click the **Test SSO** button.</span></span> <span data-ttu-id="170a0-183">Une fenêtre contextuelle apparaît, avec la page de connexion Azure AD.</span><span class="sxs-lookup"><span data-stu-id="170a0-183">This results in a popup window appearing with Azure AD login page presented.</span></span> <span data-ttu-id="170a0-184">Entrez normalement vos informations d’identification pour vous authentifier.</span><span class="sxs-lookup"><span data-stu-id="170a0-184">Enter your credentials in as normal to authenticate.</span></span> 

    <span data-ttu-id="170a0-185">**Résolution des problèmes :** Vérifiez que l’adresse e-mail retournée par Azure AD est identique au compte Workplace avec lequel vous êtes connecté.</span><span class="sxs-lookup"><span data-stu-id="170a0-185">**Troubleshooting:** Ensure the email address being returned back from Azure AD is the same as the Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="170a0-186">Une fois le test terminé, faites défiler jusqu’au bas de la page et cliquez sur le bouton **Save** (Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="170a0-186">Once the test has been completed successfully, scroll to the bottom of the page and click the **Save** button.</span></span>

14. <span data-ttu-id="170a0-187">La page de connexion à Azure AD sera désormais présentée à tous les utilisateurs de Workplace pour qu’ils s’authentifient.</span><span class="sxs-lookup"><span data-stu-id="170a0-187">All users using Workplace will now be presented with Azure AD login page for authentication.</span></span>

15. <span data-ttu-id="170a0-188">**Redirection de déconnexion SAML (facultatif)** -</span><span class="sxs-lookup"><span data-stu-id="170a0-188">**SAML Logout Redirect (optional)** -</span></span> 

    <span data-ttu-id="170a0-189">Vous pouvez choisir de configurer une URL de déconnexion SAML, qui peut être utilisée pour pointer vers la page de déconnexion d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="170a0-189">You can choose to optionally configure a SAML Logout Url, which can be used to point at Azure AD's logout page.</span></span> <span data-ttu-id="170a0-190">Quand ce paramètre est activé et configuré, l’utilisateur n’est plus dirigé vers la page de déconnexion de Workplace.</span><span class="sxs-lookup"><span data-stu-id="170a0-190">When this setting is enabled and configured, the user will no longer be directed to the Workplace logout page.</span></span> <span data-ttu-id="170a0-191">Au lieu de cela, il est redirigé vers l’URL qui a été ajoutée dans le paramètre SAML Logout Redirect.</span><span class="sxs-lookup"><span data-stu-id="170a0-191">Instead, the user will be redirected to the url that was added in the SAML Logout Redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="170a0-192">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="170a0-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="170a0-193">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="170a0-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="170a0-194">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="170a0-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="configuring-reauthentication-frequency"></a><span data-ttu-id="170a0-195">Configuration de la fréquence de réauthentification</span><span class="sxs-lookup"><span data-stu-id="170a0-195">Configuring Reauthentication Frequency</span></span>

<span data-ttu-id="170a0-196">Vous pouvez configurer Workplace pour demander une vérification SAML chaque jour, tous les trois jours, toutes les deux semaines, tous les mois ou jamais.</span><span class="sxs-lookup"><span data-stu-id="170a0-196">You can configure Workplace to prompt for a SAML check every day, three days, week, two weeks, month or never.</span></span>

> [!NOTE] 
><span data-ttu-id="170a0-197">La valeur minimale pour la vérification SAML sur les applications mobiles est d’une semaine.</span><span class="sxs-lookup"><span data-stu-id="170a0-197">The minimum value for the SAML check on mobile applications is set to one week.</span></span>

<span data-ttu-id="170a0-198">Vous pouvez également forcer une réinitialisation SAML pour tous les utilisateurs à l’aide du bouton Require SAML authentication for all users now.</span><span class="sxs-lookup"><span data-stu-id="170a0-198">You can also force a SAML reset for all users using the button: Require SAML authentication for all users now.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="170a0-199">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="170a0-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="170a0-200">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="170a0-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="170a0-202">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="170a0-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="170a0-203">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="170a0-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="170a0-205">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="170a0-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="170a0-207">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="170a0-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="170a0-209">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="170a0-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="170a0-211">a.</span><span class="sxs-lookup"><span data-stu-id="170a0-211">a.</span></span> <span data-ttu-id="170a0-212">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="170a0-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="170a0-213">b.</span><span class="sxs-lookup"><span data-stu-id="170a0-213">b.</span></span> <span data-ttu-id="170a0-214">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="170a0-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="170a0-215">c.</span><span class="sxs-lookup"><span data-stu-id="170a0-215">c.</span></span> <span data-ttu-id="170a0-216">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="170a0-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="170a0-217">d.</span><span class="sxs-lookup"><span data-stu-id="170a0-217">d.</span></span> <span data-ttu-id="170a0-218">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="170a0-218">Click **Create**.</span></span>
 
### <a name="creating-a-workplace-by-facebook-test-user"></a><span data-ttu-id="170a0-219">Création d’un utilisateur de test Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="170a0-219">Creating a Workplace by Facebook test user</span></span>

<span data-ttu-id="170a0-220">Dans cette section, un utilisateur appelé Britta Simon est créé dans Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="170a0-220">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="170a0-221">Workplace by Facebook prend en charge l’approvisionnement juste-à-temps, qui est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="170a0-221">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="170a0-222">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="170a0-222">There is no action for you in this section.</span></span> <span data-ttu-id="170a0-223">S’il n’existe pas d’utilisateur dans Workplace by Facebook, un nouvel utilisateur est créé quand vous tentez d’accéder à Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="170a0-223">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt to access Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="170a0-224">Si vous avez besoin de créer un utilisateur manuellement, contactez l’[équipe de prise en charge des clients Workplace by Facebook](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="170a0-224">If you need to create a user manually, Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/)</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="170a0-225">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="170a0-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="170a0-226">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="170a0-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workplace by Facebook.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="170a0-228">**Pour assigner Britta Simon à Workplace by Facebook, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="170a0-228">**To assign Britta Simon to Workplace by Facebook, perform the following steps:**</span></span>

1. <span data-ttu-id="170a0-229">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="170a0-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="170a0-231">Dans la liste des applications, sélectionnez **Workplace by Facebook**.</span><span class="sxs-lookup"><span data-stu-id="170a0-231">In the applications list, select **Workplace by Facebook**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="170a0-233">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="170a0-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="170a0-235">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="170a0-235">Click **Add** button.</span></span> <span data-ttu-id="170a0-236">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="170a0-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="170a0-238">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="170a0-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="170a0-239">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="170a0-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="170a0-240">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="170a0-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="170a0-241">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="170a0-241">Testing single sign-on</span></span>

<span data-ttu-id="170a0-242">Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="170a0-242">If you want to test your single sign-on settings, open the Access Panel.</span></span>
<span data-ttu-id="170a0-243">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="170a0-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="170a0-244">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="170a0-244">Additional resources</span></span>

* [<span data-ttu-id="170a0-245">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="170a0-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="170a0-246">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="170a0-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="170a0-247">Configurer l’approvisionnement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="170a0-247">Configure User Provisioning</span></span>](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



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

