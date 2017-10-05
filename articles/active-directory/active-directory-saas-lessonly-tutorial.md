---
title: "Didacticiel : Intégration d’Azure Active Directory à Lesson.ly | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Lesson.ly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c9dc6e6-5d85-4553-8a35-c7137064b928
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: fc1e1b2de0a138dbe88d794f802b002321948ab8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lessonly"></a><span data-ttu-id="5d29f-103">Didacticiel : Intégration d’Azure Active Directory à Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="5d29f-103">Tutorial: Azure Active Directory integration with Lesson.ly</span></span>

<span data-ttu-id="5d29f-104">Dans ce didacticiel, vous allez apprendre à intégrer Lesson.ly avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5d29f-104">In this tutorial, you learn how to integrate Lesson.ly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5d29f-105">L’intégration de Lesson.ly dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5d29f-105">Integrating Lesson.ly with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5d29f-106">Dans Azure AD, vous pouvez contrôler qui a accès à Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="5d29f-106">You can control in Azure AD who has access to Lesson.ly</span></span>
- <span data-ttu-id="5d29f-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Lesson.ly (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d29f-107">You can enable your users to automatically get signed-on to Lesson.ly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5d29f-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="5d29f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5d29f-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5d29f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d29f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5d29f-110">Prerequisites</span></span>

<span data-ttu-id="5d29f-111">Pour configurer l’intégration d’Azure AD à Lesson.ly, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5d29f-111">To configure Azure AD integration with Lesson.ly, you need the following items:</span></span>

- <span data-ttu-id="5d29f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d29f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5d29f-113">Un abonnement Lesson.ly pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5d29f-113">A Lesson.ly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5d29f-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5d29f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5d29f-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5d29f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5d29f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5d29f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5d29f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5d29f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5d29f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5d29f-118">Scenario description</span></span>
<span data-ttu-id="5d29f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5d29f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5d29f-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="5d29f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5d29f-121">Ajout de Lesson.ly à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="5d29f-121">Adding Lesson.ly from the gallery</span></span>
2. <span data-ttu-id="5d29f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d29f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lessonly-from-the-gallery"></a><span data-ttu-id="5d29f-123">Ajout de Lesson.ly à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="5d29f-123">Adding Lesson.ly from the gallery</span></span>
<span data-ttu-id="5d29f-124">Pour configurer l’intégration de Lesson.ly à Azure AD, vous devez ajouter Lesson.ly de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="5d29f-124">To configure the integration of Lesson.ly into Azure AD, you need to add Lesson.ly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5d29f-125">**Pour ajouter Lesson.ly à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5d29f-125">**To add Lesson.ly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5d29f-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5d29f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5d29f-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5d29f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5d29f-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5d29f-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="5d29f-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5d29f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="5d29f-133">Dans la zone de recherche, entrez **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="5d29f-133">In the search box, type **Lesson.ly**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_search.png)

5. <span data-ttu-id="5d29f-135">Dans le panneau des résultats, sélectionnez **Lesson.ly**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="5d29f-135">In the results panel, select **Lesson.ly**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5d29f-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d29f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5d29f-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Lesson.ly, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5d29f-138">In this section, you configure and test Azure AD single sign-on with Lesson.ly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5d29f-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir quel utilisateur de Lesson.ly correspond à l’utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d29f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lesson.ly is to a user in Azure AD.</span></span> <span data-ttu-id="5d29f-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur de Lesson.ly associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="5d29f-140">In other words, a link relationship between an Azure AD user and the related user in Lesson.ly needs to be established.</span></span>

<span data-ttu-id="5d29f-141">Dans Lesson.ly, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="5d29f-141">In Lesson.ly, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5d29f-142">Pour configurer et tester l’authentification unique avec Azure AD avec Lesson.ly, vous devez compléter les blocs de construction suivants :</span><span class="sxs-lookup"><span data-stu-id="5d29f-142">To configure and test Azure AD single sign-on with Lesson.ly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5d29f-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5d29f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5d29f-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5d29f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5d29f-145">**[Création d’un utilisateur de test Lesson.ly](#creating-a-lessonly-test-user)** pour obtenir un équivalent de Britta Simon dans Lesson.ly lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="5d29f-145">**[Creating a Lesson.ly test user](#creating-a-lessonly-test-user)** - to have a counterpart of Britta Simon in Lesson.ly that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5d29f-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d29f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5d29f-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="5d29f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5d29f-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d29f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5d29f-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="5d29f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lesson.ly application.</span></span>

<span data-ttu-id="5d29f-150">**Pour configurer l’authentification unique avec Azure AD avec Lesson.ly, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5d29f-150">**To configure Azure AD single sign-on with Lesson.ly, perform the following steps:**</span></span>

1. <span data-ttu-id="5d29f-151">Dans le portail Azure, sur la page d’intégration de l’application **Lesson.ly**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5d29f-151">In the Azure portal, on the **Lesson.ly** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="5d29f-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5d29f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_samlbase.png)

3. <span data-ttu-id="5d29f-155">Dans la section **Domaine et URL Lesson.ly**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="5d29f-155">On the **Lesson.ly Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_url.png)

    <span data-ttu-id="5d29f-157">a.</span><span class="sxs-lookup"><span data-stu-id="5d29f-157">a.</span></span> <span data-ttu-id="5d29f-158">Dans la zone de texte **URL de connexion**, saisissez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="5d29f-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/signin`|
    | `https://<companyname>.lessonly.com/signin`|

    >[!NOTE]
    ><span data-ttu-id="5d29f-159">Lors du référencement d’un nom générique, la partie **nomentreprise** doit être remplacée par un nom réel.</span><span class="sxs-lookup"><span data-stu-id="5d29f-159">When referencing a generic name that **companyname** needs to be replaced by an actual name.</span></span>
    
    <span data-ttu-id="5d29f-160">b.</span><span class="sxs-lookup"><span data-stu-id="5d29f-160">b.</span></span> <span data-ttu-id="5d29f-161">Dans la zone de texte **Identificateur**, entrez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="5d29f-161">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/auth/saml/metadata`|
    | `https://<companyname>.lessonly.com/auth/saml/metadata`|

    > [!NOTE] 
    > <span data-ttu-id="5d29f-162">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="5d29f-162">These values are not real.</span></span> <span data-ttu-id="5d29f-163">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="5d29f-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5d29f-164">Pour obtenir ces valeurs, contactez l’[équipe de support technique Lesson.ly](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="5d29f-164">Contact [Lesson.ly Client support team](mailto:dev@lessonly.com) to get these values.</span></span> 

4. <span data-ttu-id="5d29f-165">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5d29f-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_certificate.png)

5. <span data-ttu-id="5d29f-167">L’application Lesson.ly s’attend à recevoir les assertions SAML dans un format spécifique, ce qui vous oblige à ajouter des mappages d’attributs personnalisés à votre configuration **Attributs du jeton SAML**. Les captures d’écran suivantes illustrent un exemple.</span><span class="sxs-lookup"><span data-stu-id="5d29f-167">The Lesson.ly application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.The following screenshot shows an example for this.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lessonly-tutorial/tutorial_lessonly_06.png)
           
6. <span data-ttu-id="5d29f-169">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, configurez l’attribut du jeton SAML comme sur l’image précédente, puis procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5d29f-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>

    | <span data-ttu-id="5d29f-170">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="5d29f-170">Attribute Name</span></span>   | <span data-ttu-id="5d29f-171">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="5d29f-171">Attribute Value</span></span> |
    | ---------------  | ----------------|
    | <span data-ttu-id="5d29f-172">urn:oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="5d29f-172">urn:oid:2.5.4.42</span></span> |<span data-ttu-id="5d29f-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="5d29f-173">user.givenname</span></span> |
    | <span data-ttu-id="5d29f-174">urn:oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="5d29f-174">urn:oid:2.5.4.4</span></span>  |<span data-ttu-id="5d29f-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="5d29f-175">user.surname</span></span> |
    | <span data-ttu-id="5d29f-176">urn:oid:0.9.2342.19200300.1001.3</span><span class="sxs-lookup"><span data-stu-id="5d29f-176">urn:oid:0.9.2342.19200300.1001.3</span></span> |<span data-ttu-id="5d29f-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="5d29f-177">user.mail</span></span> |

    <span data-ttu-id="5d29f-178">a.</span><span class="sxs-lookup"><span data-stu-id="5d29f-178">a.</span></span> <span data-ttu-id="5d29f-179">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="5d29f-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="5d29f-182">b.</span><span class="sxs-lookup"><span data-stu-id="5d29f-182">b.</span></span> <span data-ttu-id="5d29f-183">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="5d29f-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="5d29f-184">c.</span><span class="sxs-lookup"><span data-stu-id="5d29f-184">c.</span></span> <span data-ttu-id="5d29f-185">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="5d29f-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="5d29f-186">d.</span><span class="sxs-lookup"><span data-stu-id="5d29f-186">d.</span></span> <span data-ttu-id="5d29f-187">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5d29f-187">Click **Ok**.</span></span>     

7. <span data-ttu-id="5d29f-188">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="5d29f-188">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lessonly-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="5d29f-190">Dans la section **Configuration de Lesson.ly**, cliquez sur **Configurer Lesson.ly** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="5d29f-190">On the **Lesson.ly Configuration** section, click **Configure Lesson.ly** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5d29f-191">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="5d29f-191">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_configure.png)

9. <span data-ttu-id="5d29f-193">Pour configurer l’authentification unique côté **Lesson.ly**, vous devez envoyer le **Certificat (Base64)** téléchargé et **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à [l’équipe de support Lesson.ly](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="5d29f-193">To configure single sign-on on **Lesson.ly** side, you need to send the downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

> [!TIP]
> <span data-ttu-id="5d29f-194">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="5d29f-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5d29f-195">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="5d29f-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5d29f-196">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5d29f-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5d29f-197">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d29f-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="5d29f-198">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5d29f-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="5d29f-200">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5d29f-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5d29f-201">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5d29f-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5d29f-203">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5d29f-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5d29f-205">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5d29f-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5d29f-207">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5d29f-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5d29f-209">a.</span><span class="sxs-lookup"><span data-stu-id="5d29f-209">a.</span></span> <span data-ttu-id="5d29f-210">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5d29f-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5d29f-211">b.</span><span class="sxs-lookup"><span data-stu-id="5d29f-211">b.</span></span> <span data-ttu-id="5d29f-212">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5d29f-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5d29f-213">c.</span><span class="sxs-lookup"><span data-stu-id="5d29f-213">c.</span></span> <span data-ttu-id="5d29f-214">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5d29f-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5d29f-215">d.</span><span class="sxs-lookup"><span data-stu-id="5d29f-215">d.</span></span> <span data-ttu-id="5d29f-216">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5d29f-216">Click **Create**.</span></span>
 
### <a name="creating-a-lessonly-test-user"></a><span data-ttu-id="5d29f-217">Création d’un utilisateur de test Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="5d29f-217">Creating a Lesson.ly test user</span></span>

<span data-ttu-id="5d29f-218">L’objectif de cette section est de créer l’utilisateur Britta Simon dans Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="5d29f-218">The objective of this section is to create a user called Britta Simon in Lesson.ly.</span></span> <span data-ttu-id="5d29f-219">Lesson.ly. prend en charge l’approvisionnement juste-à-temps, qui est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="5d29f-219">Lesson.ly supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="5d29f-220">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="5d29f-220">There is no action item for you in this section.</span></span> <span data-ttu-id="5d29f-221">Un utilisateur sera créé lors d’une tentative d’accès à Lesson.ly s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="5d29f-221">A new user will be created during an attempt to access Lesson.ly if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="5d29f-222">Si vous devez créer un utilisateur manuellement, contactez [l’équipe du support technique Lesson.ly](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="5d29f-222">If you need to create an user manually, you need to contact the [Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5d29f-223">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d29f-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5d29f-224">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="5d29f-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lesson.ly.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="5d29f-226">**Pour affecter Britta Simon à Lesson.ly, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5d29f-226">**To assign Britta Simon to Lesson.ly, perform the following steps:**</span></span>

1. <span data-ttu-id="5d29f-227">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5d29f-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5d29f-229">Dans la liste des applications, sélectionnez **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="5d29f-229">In the applications list, select **Lesson.ly**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_app.png) 

3. <span data-ttu-id="5d29f-231">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5d29f-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="5d29f-233">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5d29f-233">Click **Add** button.</span></span> <span data-ttu-id="5d29f-234">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5d29f-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="5d29f-236">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5d29f-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5d29f-237">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5d29f-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5d29f-238">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5d29f-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5d29f-239">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5d29f-239">Testing single sign-on</span></span>

<span data-ttu-id="5d29f-240">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="5d29f-240">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5d29f-241">Lorsque vous cliquez sur la vignette Lesson.ly dans le volet d’accès, vous devez être connecté automatiquement à votre application Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="5d29f-241">When you click the Lesson.ly tile in the Access Panel, you should get automatically signed-on to your Lesson.ly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5d29f-242">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5d29f-242">Additional resources</span></span>

* [<span data-ttu-id="5d29f-243">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d29f-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5d29f-244">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5d29f-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_203.png

