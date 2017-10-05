---
title: "Didacticiel : Intégration d'Azure Active Directory à Blackboard Learn | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Blackboard Learn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b8ca505-61ea-487c-9a3e-fa50c936df0c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jeedes
ms.openlocfilehash: c2b7638e99fa46ff41a7f2202bdf0e7a2b017c19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn"></a><span data-ttu-id="9d944-103">Didacticiel : Intégration d'Azure Active Directory à Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="9d944-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span></span>

<span data-ttu-id="9d944-104">Dans ce didacticiel, vous allez apprendre à intégrer Blackboard Learn à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9d944-104">In this tutorial, you learn how to integrate Blackboard Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9d944-105">L’intégration de Blackboard Learn dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="9d944-105">Integrating Blackboard Learn with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9d944-106">Dans Azure AD, vous pouvez contrôler qui a accès à Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="9d944-106">You can control in Azure AD who has access to Blackboard Learn</span></span>
- <span data-ttu-id="9d944-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Blackboard Learn (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d944-107">You can enable your users to automatically get signed-on to Blackboard Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9d944-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="9d944-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9d944-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9d944-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d944-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9d944-110">Prerequisites</span></span>

<span data-ttu-id="9d944-111">Pour configurer l’intégration d’Azure AD à Blackboard Learn, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9d944-111">To configure Azure AD integration with Blackboard Learn, you need the following items:</span></span>

- <span data-ttu-id="9d944-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d944-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9d944-113">Un abonnement avec authentification unique à Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="9d944-113">A Blackboard Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9d944-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="9d944-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9d944-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="9d944-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9d944-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9d944-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9d944-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9d944-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9d944-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="9d944-118">Scenario description</span></span>
<span data-ttu-id="9d944-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="9d944-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9d944-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="9d944-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9d944-121">Ajout de Blackboard Learn à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="9d944-121">Adding Blackboard Learn from the gallery</span></span>
2. <span data-ttu-id="9d944-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d944-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn-from-the-gallery"></a><span data-ttu-id="9d944-123">Ajout de Blackboard Learn à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="9d944-123">Adding Blackboard Learn from the gallery</span></span>
<span data-ttu-id="9d944-124">Pour configurer l’intégration de Blackboard Learn à Azure AD, vous devez ajouter Blackboard Learn de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="9d944-124">To configure the integration of Blackboard Learn into Azure AD, you need to add Blackboard Learn from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9d944-125">**Pour ajouter Blackboard Learn à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9d944-125">**To add Blackboard Learn from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9d944-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9d944-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9d944-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="9d944-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9d944-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9d944-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="9d944-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9d944-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="9d944-133">Dans la zone de recherche, tapez **Blackboard Learn**.</span><span class="sxs-lookup"><span data-stu-id="9d944-133">In the search box, type **Blackboard Learn**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_search.png)

5. <span data-ttu-id="9d944-135">Dans le volet de résultats, sélectionnez **Blackboard Learn**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="9d944-135">In the results panel, select **Blackboard Learn**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9d944-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d944-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9d944-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Blackboard Learn avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="9d944-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9d944-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Blackboard Learn équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d944-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Blackboard Learn is to a user in Azure AD.</span></span> <span data-ttu-id="9d944-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Blackboard Learn associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="9d944-140">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn needs to be established.</span></span>

<span data-ttu-id="9d944-141">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="9d944-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Blackboard Learn.</span></span>

<span data-ttu-id="9d944-142">Pour configurer et tester l’authentification unique Azure AD avec Blackboard Learn, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="9d944-142">To configure and test Azure AD single sign-on with Blackboard Learn, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9d944-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="9d944-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9d944-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d944-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9d944-145">**[Création d’un utilisateur de test Blackboard Learn](#creating-a-blackboard-learn-test-user)** pour avoir un équivalent de Britta Simon dans Blackboard Learn lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="9d944-145">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9d944-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d944-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9d944-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="9d944-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9d944-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d944-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9d944-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="9d944-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Blackboard Learn application.</span></span>

<span data-ttu-id="9d944-150">**Pour configurer l’authentification unique Azure AD avec Blackboard Learn, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9d944-150">**To configure Azure AD single sign-on with Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="9d944-151">Dans le portail Azure, dans la page d’intégration de l’application **Blackboard Learn**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="9d944-151">In the Azure portal, on the **Blackboard Learn** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="9d944-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9d944-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_samlbase.png)

3. <span data-ttu-id="9d944-155">Dans la section **Domaine et URL Blackboard Learn**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="9d944-155">On the **Blackboard Learn Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_url.png)

    <span data-ttu-id="9d944-157">a.</span><span class="sxs-lookup"><span data-stu-id="9d944-157">a.</span></span> <span data-ttu-id="9d944-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.blackboard.com/`</span><span class="sxs-lookup"><span data-stu-id="9d944-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/`</span></span>

    <span data-ttu-id="9d944-159">b.</span><span class="sxs-lookup"><span data-stu-id="9d944-159">b.</span></span> <span data-ttu-id="9d944-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span><span class="sxs-lookup"><span data-stu-id="9d944-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="9d944-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="9d944-161">These values are not real.</span></span> <span data-ttu-id="9d944-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="9d944-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9d944-163">Pour obtenir ces valeurs, contactez [l’équipe du support Blackboard Learn](https://www.blackboard.com/support/index.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d944-163">Contact [Blackboard Learn Client support team](https://www.blackboard.com/support/index.aspx) to get these values.</span></span> 

4. <span data-ttu-id="9d944-164">L’application Blackboard Learn attend les assertions SAML dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="9d944-164">Blackboard Learn application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="9d944-165">Configurez les revendications suivantes pour cette application.</span><span class="sxs-lookup"><span data-stu-id="9d944-165">Configure the following claims for this application.</span></span> <span data-ttu-id="9d944-166">Vous pouvez gérer les valeurs de ces attributs à partir de la section **Attributs utilisateur** sur la page d’intégration des applications.</span><span class="sxs-lookup"><span data-stu-id="9d944-166">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span>
 <span data-ttu-id="9d944-167">La capture d’écran suivante en présente un exemple.</span><span class="sxs-lookup"><span data-stu-id="9d944-167">The following screenshot shows an example about it.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="9d944-169">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, configurez les attributs du jeton SAML comme indiqué dans l’image, puis effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="9d944-169">In the **User Attributes** section on **Single sign-on** dialog, configure SAML token attributes as shown in the image and perform the following steps.</span></span> <span data-ttu-id="9d944-170">Nous avons mappé Userprincipalname comme seul attribut utilisateur ici, mais vous pouvez le mapper à la valeur appropriée qui identifie de façon unique l’utilisateur dans l’organisation et se mappe avec le champ de nom d’utilisateur Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="9d944-170">We have mapped the Userprincipalname as the unique user attribute here but you can map it to the appropriate value, which uniquely distinguishes the user in the organization and that maps to Blackboard Learn username field.</span></span>
           
    | <span data-ttu-id="9d944-171">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="9d944-171">Attribute Name</span></span> | <span data-ttu-id="9d944-172">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="9d944-172">Attribute Value</span></span> |   
    | ---------------| ----------------|
    | <span data-ttu-id="9d944-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span><span class="sxs-lookup"><span data-stu-id="9d944-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span></span> |<span data-ttu-id="9d944-174">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="9d944-174">user.userprincipalname</span></span> |

    <span data-ttu-id="9d944-175">a.</span><span class="sxs-lookup"><span data-stu-id="9d944-175">a.</span></span> <span data-ttu-id="9d944-176">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="9d944-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_04.png)
    
    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="9d944-179">b.</span><span class="sxs-lookup"><span data-stu-id="9d944-179">b.</span></span> <span data-ttu-id="9d944-180">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="9d944-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="9d944-181">c.</span><span class="sxs-lookup"><span data-stu-id="9d944-181">c.</span></span> <span data-ttu-id="9d944-182">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="9d944-182">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="9d944-183">d.</span><span class="sxs-lookup"><span data-stu-id="9d944-183">d.</span></span> <span data-ttu-id="9d944-184">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="9d944-184">Click **Ok**.</span></span>

4. <span data-ttu-id="9d944-185">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier XML sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="9d944-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_certificate.png)

7. <span data-ttu-id="9d944-187">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="9d944-187">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="9d944-189">Dans la section **Configuration de Blackboard Learn**, cliquez sur **Configurer Blackboard Learn** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="9d944-189">On the **Blackboard Learn Configuration** section, click **Configure Blackboard Learn** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9d944-190">Copiez **l’ID d’entité SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="9d944-190">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_configure.png) 

9. <span data-ttu-id="9d944-192">Pour configurer l’authentification unique côté **Blackboard Learn**, vous devez envoyer le fichier **XML de métadonnées** téléchargé et **l’ID d’entité SAML** à [l’équipe du support Blackboard Learn](https://www.blackboard.com/support/index.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d944-192">To configure single sign-on on **Blackboard Learn** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID** to [Blackboard Learn support](https://www.blackboard.com/support/index.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="9d944-193">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="9d944-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9d944-194">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="9d944-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9d944-195">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9d944-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9d944-196">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d944-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="9d944-197">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9d944-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="9d944-199">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9d944-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9d944-200">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9d944-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9d944-202">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="9d944-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9d944-204">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9d944-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9d944-206">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9d944-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9d944-208">a.</span><span class="sxs-lookup"><span data-stu-id="9d944-208">a.</span></span> <span data-ttu-id="9d944-209">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9d944-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9d944-210">b.</span><span class="sxs-lookup"><span data-stu-id="9d944-210">b.</span></span> <span data-ttu-id="9d944-211">Dans la zone de texte **Nom d’utilisateur** , tapez l’**adresse de messagerie** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d944-211">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="9d944-212">c.</span><span class="sxs-lookup"><span data-stu-id="9d944-212">c.</span></span> <span data-ttu-id="9d944-213">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="9d944-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9d944-214">d.</span><span class="sxs-lookup"><span data-stu-id="9d944-214">d.</span></span> <span data-ttu-id="9d944-215">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="9d944-215">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn-test-user"></a><span data-ttu-id="9d944-216">Création d’un utilisateur de test Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="9d944-216">Creating a Blackboard Learn test user</span></span>
<span data-ttu-id="9d944-217">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="9d944-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span></span> 

<span data-ttu-id="9d944-218">L'application Blackboard Learn prend en charge la configuration de l'utilisateur au moment opportun.</span><span class="sxs-lookup"><span data-stu-id="9d944-218">Blackboard Learn application support just in time user provisioning.</span></span> <span data-ttu-id="9d944-219">Vérifiez que vous avez configuré les revendications comme décrit dans la section **[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)**.</span><span class="sxs-lookup"><span data-stu-id="9d944-219">Make sure that you have configured the claims as described in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span></span>
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9d944-220">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d944-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9d944-221">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="9d944-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Blackboard Learn.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="9d944-223">**Pour affecter Britta Simon à Blackboard Learn, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9d944-223">**To assign Britta Simon to Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="9d944-224">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9d944-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="9d944-226">Dans la liste des applications, sélectionnez **Blackboard Learn**.</span><span class="sxs-lookup"><span data-stu-id="9d944-226">In the applications list, select **Blackboard Learn**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_app.png) 

3. <span data-ttu-id="9d944-228">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9d944-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="9d944-230">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9d944-230">Click **Add** button.</span></span> <span data-ttu-id="9d944-231">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9d944-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="9d944-233">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9d944-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9d944-234">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9d944-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9d944-235">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9d944-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9d944-236">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="9d944-236">Testing single sign-on</span></span>

<span data-ttu-id="9d944-237">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="9d944-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9d944-238">Lorsque vous cliquez sur la vignette Blackboard Learn dans le volet d’accès, vous devez être connecté automatiquement à votre application Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="9d944-238">When you click the Blackboard Learn tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn application.</span></span> <span data-ttu-id="9d944-239">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9d944-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9d944-240">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="9d944-240">Additional resources</span></span>

* [<span data-ttu-id="9d944-241">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9d944-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9d944-242">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="9d944-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_203.png

