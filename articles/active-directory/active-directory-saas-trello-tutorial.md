---
title: "Didacticiel : intégration d’Azure Active Directory à Trello | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Trello."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: d93667f16f2d72995e4a42e79e9125b8e3f6b07c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a><span data-ttu-id="69973-103">Didacticiel : Intégration d’Azure Active Directory avec Trello</span><span class="sxs-lookup"><span data-stu-id="69973-103">Tutorial: Azure Active Directory integration with Trello</span></span>

<span data-ttu-id="69973-104">Dans ce didacticiel, vous allez apprendre à intégrer Trello à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="69973-104">In this tutorial, you learn how to integrate Trello with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="69973-105">L’intégration de Trello dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="69973-105">Integrating Trello with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="69973-106">Dans Azure AD, vous pouvez contrôler qui a accès à Trello</span><span class="sxs-lookup"><span data-stu-id="69973-106">You can control in Azure AD who has access to Trello</span></span>
- <span data-ttu-id="69973-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Trello (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="69973-107">You can enable your users to automatically get signed-on to Trello (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="69973-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="69973-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="69973-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="69973-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69973-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="69973-110">Prerequisites</span></span>

<span data-ttu-id="69973-111">Pour configurer l’intégration d’Azure AD avec Trello, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="69973-111">To configure Azure AD integration with Trello, you need the following items:</span></span>

- <span data-ttu-id="69973-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="69973-112">An Azure AD subscription</span></span>
- <span data-ttu-id="69973-113">Un abonnement Trello pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="69973-113">A Trello single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="69973-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="69973-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="69973-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="69973-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="69973-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="69973-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="69973-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="69973-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="69973-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="69973-118">Scenario description</span></span>
<span data-ttu-id="69973-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="69973-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="69973-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="69973-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="69973-121">Ajout de Trello depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="69973-121">Adding Trello from the gallery</span></span>
2. <span data-ttu-id="69973-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="69973-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trello-from-the-gallery"></a><span data-ttu-id="69973-123">Ajout de Trello depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="69973-123">Adding Trello from the gallery</span></span>
<span data-ttu-id="69973-124">Pour configurer l’intégration de Trello avec Azure AD, vous devez ajouter Trello, à partir de la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="69973-124">To configure the integration of Trello into Azure AD, you need to add Trello from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="69973-125">**Pour ajouter Trello à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="69973-125">**To add Trello from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="69973-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="69973-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="69973-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="69973-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="69973-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="69973-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="69973-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="69973-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="69973-133">Dans la zone de recherche, tapez **Trello**.</span><span class="sxs-lookup"><span data-stu-id="69973-133">In the search box, type **Trello**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trello-tutorial/tutorial_trello_search.png)

5. <span data-ttu-id="69973-135">Dans le volet de résultats, sélectionnez **Trello**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="69973-135">In the results panel, select **Trello**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trello-tutorial/tutorial_trello_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="69973-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="69973-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="69973-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Trello avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="69973-138">In this section, you configure and test Azure AD single sign-on with Trello based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="69973-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Trello équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="69973-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Trello is to a user in Azure AD.</span></span> <span data-ttu-id="69973-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Trello associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="69973-140">In other words, a link relationship between an Azure AD user and the related user in Trello needs to be established.</span></span>

<span data-ttu-id="69973-141">Dans Workday, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Username** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="69973-141">In Trello, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="69973-142">Pour configurer et tester l’authentification unique Azure AD avec Trello, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="69973-142">To configure and test Azure AD single sign-on with Trello, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="69973-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="69973-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="69973-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="69973-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="69973-145">**[Création d’un utilisateur de test Trello](#creating-a-trello-test-user)** pour avoir un équivalent de Britta Simon dans Trello lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="69973-145">**[Creating a Trello test user](#creating-a-trello-test-user)** - to have a counterpart of Britta Simon in Trello that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="69973-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="69973-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="69973-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="69973-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="69973-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="69973-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="69973-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Trello.</span><span class="sxs-lookup"><span data-stu-id="69973-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Trello application.</span></span>

<span data-ttu-id="69973-150">**Pour configurer l’authentification unique Azure AD avec Trello, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="69973-150">**To configure Azure AD single sign-on with Trello, perform the following steps:**</span></span>

1. <span data-ttu-id="69973-151">Dans le portail Azure, dans la page d’intégration de l’application **Trello**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="69973-151">In the Azure portal, on the **Trello** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="69973-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="69973-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-trello-tutorial/tutorial_trello_samlbase.png)

3. <span data-ttu-id="69973-155">Dans la section **Domaines et URL Trello**, si vous souhaitez configurer l’application en **Mode initié par IDP**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="69973-155">On the **Trello Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trello-tutorial/tutorial_trello_url.png)

    <span data-ttu-id="69973-157">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="69973-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

4. <span data-ttu-id="69973-158">Dans la section **Domaine et URL Trello**, si vous souhaitez configurer l’application en **Mode initié par SP**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="69973-158">On the **Trello Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-trello-tutorial/tutorial_trello_url1.png)

    <span data-ttu-id="69973-160">a.</span><span class="sxs-lookup"><span data-stu-id="69973-160">a.</span></span> <span data-ttu-id="69973-161">Cliquez sur l’option **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="69973-161">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="69973-162">b.</span><span class="sxs-lookup"><span data-stu-id="69973-162">b.</span></span> <span data-ttu-id="69973-163">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="69973-163">In the **Sign On URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

    >[!NOTE]
    ><span data-ttu-id="69973-164">Vous devez obtenir le champ de données dynamiques **\<enterprise\>** de Trello.</span><span class="sxs-lookup"><span data-stu-id="69973-164">You should get the **\<enterprise\>** slug from Trello.</span></span> <span data-ttu-id="69973-165">Si vous n’avez pas la valeur de ce champ, contactez l’[équipe de support de Trello](mailto:support@trello.com) pour obtenir le champ de données dynamiques pour votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="69973-165">If you don't have the slug value, contact [Trello support team](mailto:support@trello.com) to get the slug for you enterprise.</span></span>
    > 

5. <span data-ttu-id="69973-166">L’application Trello s’attend à ce que les assertions SAML contiennent des attributs spécifiques.</span><span class="sxs-lookup"><span data-stu-id="69973-166">Trello application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="69973-167">Configurez les attributs suivants pour cette application.</span><span class="sxs-lookup"><span data-stu-id="69973-167">Configure the following attributes  for this application.</span></span> <span data-ttu-id="69973-168">Vous pouvez gérer les valeurs de ces attributs à partir des « **Attributs utilisateur** » de l’application.</span><span class="sxs-lookup"><span data-stu-id="69973-168">You can manage the values of these attributes from the **"User Attributes"** of the application.</span></span> <span data-ttu-id="69973-169">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="69973-169">The following screenshot shows an example for this.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trello-tutorial/tutorial_trello_attribute.png)

6. <span data-ttu-id="69973-171">Dans la boîte de dialogue **Attributs du jeton SAML** , pour chaque ligne indiquée dans le tableau ci-dessous, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="69973-171">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
 
    | <span data-ttu-id="69973-172">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="69973-172">Attribute Name</span></span> | <span data-ttu-id="69973-173">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="69973-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="69973-174">User.Email</span><span class="sxs-lookup"><span data-stu-id="69973-174">User.Email</span></span> | <span data-ttu-id="69973-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="69973-175">user.mail</span></span> |
    | <span data-ttu-id="69973-176">User.FirstName</span><span class="sxs-lookup"><span data-stu-id="69973-176">User.FirstName</span></span> | <span data-ttu-id="69973-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="69973-177">user.givenname</span></span> |
    | <span data-ttu-id="69973-178">User.LastName</span><span class="sxs-lookup"><span data-stu-id="69973-178">User.LastName</span></span> | <span data-ttu-id="69973-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="69973-179">user.surname</span></span> |

    <span data-ttu-id="69973-180">a.</span><span class="sxs-lookup"><span data-stu-id="69973-180">a.</span></span> <span data-ttu-id="69973-181">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="69973-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trello-tutorial/tutorial_officespace_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-trello-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="69973-184">b.</span><span class="sxs-lookup"><span data-stu-id="69973-184">b.</span></span> <span data-ttu-id="69973-185">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="69973-185">In the **Name** textbox, type the attribute name shown for that row.</span></span> 

    <span data-ttu-id="69973-186">c.</span><span class="sxs-lookup"><span data-stu-id="69973-186">c.</span></span> <span data-ttu-id="69973-187">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="69973-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="69973-188">d.</span><span class="sxs-lookup"><span data-stu-id="69973-188">d.</span></span> <span data-ttu-id="69973-189">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="69973-189">Click **Ok**.</span></span> 
 
7. <span data-ttu-id="69973-190">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="69973-190">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trello-tutorial/tutorial_trello_certificate.png) 

8. <span data-ttu-id="69973-192">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="69973-192">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trello-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="69973-194">Dans la section **Configuration de Trello**, cliquez sur **Configurer Trello** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="69973-194">On the **Trello Configuration** section, click **Configure Trello** to open **Configure sign-on** window.</span></span> <span data-ttu-id="69973-195">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="69973-195">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trello-tutorial/tutorial_trello_configure.png) 

9. <span data-ttu-id="69973-197">Pour configurer l’authentification unique pour votre application, accédez à la page [Configuration de l’authentification unique d’entreprise Trello](https://trello.com/sso-configuration) pour envoyer à l’[équipe de support technique de Trello](mailto:support@trello.com) l’**URL d’authentification unique SAML** et joignez le **Certificat (Base64)**.</span><span class="sxs-lookup"><span data-stu-id="69973-197">To get SSO configured for your application, go to [Trello enterprise SSO configuration](https://trello.com/sso-configuration) page to send [Trello support team](mailto:support@trello.com) the **SAML Single Sign-On Service URL** and attach the **Certificate (Base64)**.</span></span>

> [!TIP]
> <span data-ttu-id="69973-198">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="69973-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="69973-199">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="69973-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="69973-200">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="69973-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="69973-201">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="69973-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="69973-202">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="69973-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="69973-204">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="69973-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="69973-205">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="69973-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="69973-207">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="69973-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="69973-209">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="69973-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="69973-211">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="69973-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="69973-213">a.</span><span class="sxs-lookup"><span data-stu-id="69973-213">a.</span></span> <span data-ttu-id="69973-214">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="69973-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="69973-215">b.</span><span class="sxs-lookup"><span data-stu-id="69973-215">b.</span></span> <span data-ttu-id="69973-216">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="69973-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="69973-217">c.</span><span class="sxs-lookup"><span data-stu-id="69973-217">c.</span></span> <span data-ttu-id="69973-218">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="69973-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="69973-219">d.</span><span class="sxs-lookup"><span data-stu-id="69973-219">d.</span></span> <span data-ttu-id="69973-220">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="69973-220">Click **Create**.</span></span>
 
### <a name="creating-a-trello-test-user"></a><span data-ttu-id="69973-221">Création d’un utilisateur de test Trello</span><span class="sxs-lookup"><span data-stu-id="69973-221">Creating a Trello test user</span></span>

<span data-ttu-id="69973-222">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Trello.</span><span class="sxs-lookup"><span data-stu-id="69973-222">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="69973-223">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Trello.</span><span class="sxs-lookup"><span data-stu-id="69973-223">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="69973-224">Trello prend en charge l’approvisionnement juste à temps et un nouveau compte est créé la première fois que vous vous connectez à partir d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="69973-224">Trello supports just-in-time provisioning and a new account is created the first time you sign in from Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="69973-225">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="69973-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="69973-226">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Trello.</span><span class="sxs-lookup"><span data-stu-id="69973-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Trello.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="69973-228">**Pour affecter Britta Simon à Trello, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="69973-228">**To assign Britta Simon to Trello, perform the following steps:**</span></span>

1. <span data-ttu-id="69973-229">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="69973-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="69973-231">Dans la liste des applications, sélectionnez **Trello**.</span><span class="sxs-lookup"><span data-stu-id="69973-231">In the applications list, select **Trello**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trello-tutorial/tutorial_trello_app.png) 

3. <span data-ttu-id="69973-233">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="69973-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="69973-235">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="69973-235">Click **Add** button.</span></span> <span data-ttu-id="69973-236">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="69973-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="69973-238">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="69973-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="69973-239">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="69973-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="69973-240">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="69973-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="69973-241">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="69973-241">Testing single sign-on</span></span>

<span data-ttu-id="69973-242">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="69973-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="69973-243">Lorsque vous cliquez sur la mosaïque Trello dans le volet d'accès, vous devez être connecté automatiquement à votre application Trello.</span><span class="sxs-lookup"><span data-stu-id="69973-243">When you click the Trello tile in the Access Panel, you should get automatically signed-on to your Trello application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="69973-244">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="69973-244">Additional resources</span></span>

* [<span data-ttu-id="69973-245">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="69973-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="69973-246">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="69973-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trello-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trello-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trello-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trello-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trello-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trello-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trello-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trello-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trello-tutorial/tutorial_general_203.png

