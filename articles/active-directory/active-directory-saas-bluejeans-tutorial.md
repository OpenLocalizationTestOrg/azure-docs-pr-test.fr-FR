---
title: "Didacticiel : Intégration d’Azure Active Directory à BlueJeans | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et BlueJeans."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: jeedes
ms.openlocfilehash: 03bf65852b8d3cf14aebf155891a028db86e78d0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a><span data-ttu-id="13d5a-103">Didacticiel : Intégration d’Azure Active Directory à BlueJeans</span><span class="sxs-lookup"><span data-stu-id="13d5a-103">Tutorial: Azure Active Directory integration with BlueJeans</span></span>

<span data-ttu-id="13d5a-104">Dans ce didacticiel, vous allez apprendre à intégrer BlueJeans à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="13d5a-104">In this tutorial, you learn how to integrate BlueJeans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="13d5a-105">L’intégration de BlueJeans à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="13d5a-105">Integrating BlueJeans with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="13d5a-106">Dans Azure AD, vous pouvez contrôler qui a accès à BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="13d5a-106">You can control in Azure AD who has access to BlueJeans</span></span>
- <span data-ttu-id="13d5a-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à BlueJeans (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13d5a-107">You can enable your users to automatically get signed-on to BlueJeans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="13d5a-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="13d5a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="13d5a-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="13d5a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13d5a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="13d5a-110">Prerequisites</span></span>

<span data-ttu-id="13d5a-111">Pour configurer l’intégration d’Azure AD à BlueJeans, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="13d5a-111">To configure Azure AD integration with BlueJeans, you need the following items:</span></span>

- <span data-ttu-id="13d5a-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="13d5a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="13d5a-113">Un abonnement BlueJeans pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="13d5a-113">A BlueJeans single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="13d5a-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="13d5a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="13d5a-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="13d5a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="13d5a-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="13d5a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="13d5a-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="13d5a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="13d5a-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="13d5a-118">Scenario description</span></span>
<span data-ttu-id="13d5a-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="13d5a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="13d5a-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="13d5a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="13d5a-121">Ajout de BlueJeans à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="13d5a-121">Adding BlueJeans from the gallery</span></span>
2. <span data-ttu-id="13d5a-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="13d5a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bluejeans-from-the-gallery"></a><span data-ttu-id="13d5a-123">Ajout de BlueJeans à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="13d5a-123">Adding BlueJeans from the gallery</span></span>
<span data-ttu-id="13d5a-124">Pour configurer l’intégration de BlueJeans à Azure AD, vous devez ajouter BlueJeans à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="13d5a-124">To configure the integration of BlueJeans into Azure AD, you need to add BlueJeans from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="13d5a-125">**Pour ajouter BlueJeans à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="13d5a-125">**To add BlueJeans from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="13d5a-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="13d5a-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="13d5a-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="13d5a-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="13d5a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="13d5a-133">Dans la zone de recherche, tapez **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-133">In the search box, type **BlueJeans**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_search.png)

5. <span data-ttu-id="13d5a-135">Dans le volet de résultats, sélectionnez **BlueJeans**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="13d5a-135">In the results panel, select **BlueJeans**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="13d5a-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="13d5a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="13d5a-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec BlueJeans avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="13d5a-138">In this section, you configure and test Azure AD single sign-on with BlueJeans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="13d5a-139">Pour que l’authentification unique fonctionne, Azure AD doit connaître l’utilisateur BlueJeans correspondant à l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13d5a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BlueJeans is to a user in Azure AD.</span></span> <span data-ttu-id="13d5a-140">En d’autres termes, une relation doit être établie entre l’utilisateur Azure AD et l’utilisateur BlueJeans associé.</span><span class="sxs-lookup"><span data-stu-id="13d5a-140">In other words, a link relationship between an Azure AD user and the related user in BlueJeans needs to be established.</span></span>

<span data-ttu-id="13d5a-141">Dans BlueJeans, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="13d5a-141">In BlueJeans, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="13d5a-142">Pour configurer et tester l’authentification unique Azure AD avec BlueJeans, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="13d5a-142">To configure and test Azure AD single sign-on with BlueJeans, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="13d5a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="13d5a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="13d5a-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="13d5a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="13d5a-145">**[Création d’un utilisateur de test BlueJeans](#creating-a-bluejeans-test-user)** pour avoir un équivalent de Britta Simon dans BlueJeans lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="13d5a-145">**[Creating a BlueJeans test user](#creating-a-bluejeans-test-user)** - to have a counterpart of Britta Simon in BlueJeans that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="13d5a-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13d5a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="13d5a-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="13d5a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="13d5a-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="13d5a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="13d5a-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="13d5a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BlueJeans application.</span></span>

<span data-ttu-id="13d5a-150">**Pour configurer l’authentification unique Azure AD avec BlueJeans, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="13d5a-150">**To configure Azure AD single sign-on with BlueJeans, perform the following steps:**</span></span>

1. <span data-ttu-id="13d5a-151">Dans le portail Azure, dans la page d’intégration de l’application **BlueJeans**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-151">In the Azure portal, on the **BlueJeans** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="13d5a-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="13d5a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

3. <span data-ttu-id="13d5a-155">Dans la section **Domaine et URL BlueJeans**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="13d5a-155">On the **BlueJeans Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_url.png)

    <span data-ttu-id="13d5a-157">a.</span><span class="sxs-lookup"><span data-stu-id="13d5a-157">a.</span></span> <span data-ttu-id="13d5a-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="13d5a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    <span data-ttu-id="13d5a-159">b.</span><span class="sxs-lookup"><span data-stu-id="13d5a-159">b.</span></span> <span data-ttu-id="13d5a-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="13d5a-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="13d5a-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="13d5a-161">These values are not real.</span></span> <span data-ttu-id="13d5a-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="13d5a-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="13d5a-163">Pour obtenir ces valeurs, contactez [l’équipe du support BlueJeans](https://support.bluejeans.com/contact).</span><span class="sxs-lookup"><span data-stu-id="13d5a-163">Contact [BlueJeans Client support team](https://support.bluejeans.com/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="13d5a-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="13d5a-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

5. <span data-ttu-id="13d5a-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="13d5a-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bluejeans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="13d5a-168">Dans la section **Configuration de BlueJeans**, cliquez sur **Configurer BlueJeans** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-168">On the **BlueJeans Configuration** section, click **Configure BlueJeans** to open **Configure sign-on** window.</span></span> <span data-ttu-id="13d5a-169">Copiez **l’URL de déconnexion, l’URL de modification du mot de passe et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-169">Copy the **Sign-Out URL, Change Password URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_configure.png) 

7. <span data-ttu-id="13d5a-171">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise **BlueJeans** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="13d5a-171">In a different web browser window, log in to your **BlueJeans** company site as an administrator.</span></span>

8. <span data-ttu-id="13d5a-172">Accédez à **ADMIN \> Group Settings \> Security**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-172">Go to **ADMIN \> Group Settings \> Security**.</span></span>
   
   <span data-ttu-id="13d5a-173">![Administrateur](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="13d5a-173">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")</span></span>

9. <span data-ttu-id="13d5a-174">Dans la section **Security** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="13d5a-174">In the **Security** section, perform the following steps:</span></span>
   
   <span data-ttu-id="13d5a-175">![Authentification unique SAML](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "Authentification unique SAML")</span><span class="sxs-lookup"><span data-stu-id="13d5a-175">![SAML Single Sign On](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML Single Sign On")</span></span>   
   
   <span data-ttu-id="13d5a-176">a.</span><span class="sxs-lookup"><span data-stu-id="13d5a-176">a.</span></span> <span data-ttu-id="13d5a-177">Sélectionnez **SAML Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-177">Select **SAML Single Sign On**.</span></span>
  
   <span data-ttu-id="13d5a-178">b.</span><span class="sxs-lookup"><span data-stu-id="13d5a-178">b.</span></span> <span data-ttu-id="13d5a-179">Sélectionnez **Enable automatic provisioning**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-179">Select **Enable automatic provisioning**.</span></span>

10. <span data-ttu-id="13d5a-180">Poursuivez en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="13d5a-180">Move on with the following steps:</span></span>

    <span data-ttu-id="13d5a-181">![Chemin d’accès du certificat](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Chemin d’accès du certificat")</span><span class="sxs-lookup"><span data-stu-id="13d5a-181">![Certificate Path](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Certificate Path")</span></span>
    
    <span data-ttu-id="13d5a-182">a.</span><span class="sxs-lookup"><span data-stu-id="13d5a-182">a.</span></span> <span data-ttu-id="13d5a-183">Cliquez sur **Choose File**, puis chargez le certificat téléchargé.</span><span class="sxs-lookup"><span data-stu-id="13d5a-183">Click **Choose File**, and then upload the downloaded certificate.</span></span>
   
    <span data-ttu-id="13d5a-184">b.</span><span class="sxs-lookup"><span data-stu-id="13d5a-184">b.</span></span> <span data-ttu-id="13d5a-185">Collez la valeur du champ **URL du service d’authentification unique SAML** dans la zone de texte **Login URL** (URL de connexion).</span><span class="sxs-lookup"><span data-stu-id="13d5a-185">Paste **SAML Single Sign-On Service URL** into the **Login URL** textbox.</span></span>
   
    <span data-ttu-id="13d5a-186">c.</span><span class="sxs-lookup"><span data-stu-id="13d5a-186">c.</span></span> <span data-ttu-id="13d5a-187">Collez la valeur du champ **Modifier l’URL de mot de passe** dans la zone de texte **Password Change URL** (URL de modification du mot de passe).</span><span class="sxs-lookup"><span data-stu-id="13d5a-187">Paste **Change Password URL** into the **Password Change URL** textbox.</span></span>
   
    <span data-ttu-id="13d5a-188">d.</span><span class="sxs-lookup"><span data-stu-id="13d5a-188">d.</span></span> <span data-ttu-id="13d5a-189">Collez la valeur du champ **URL de déconnexion** dans la zone de texte **Logout URL** (URL de déconnexion).</span><span class="sxs-lookup"><span data-stu-id="13d5a-189">Paste **Sign-Out URL** into the **Logout URL** textbox.</span></span>

11. <span data-ttu-id="13d5a-190">Poursuivez en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="13d5a-190">Move on with the following steps:</span></span>
    
    <span data-ttu-id="13d5a-191">![Enregistrer les modifications](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Enregistrer les modifications")</span><span class="sxs-lookup"><span data-stu-id="13d5a-191">![Save Changes](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Save Changes")</span></span>
    
    <span data-ttu-id="13d5a-192">a.</span><span class="sxs-lookup"><span data-stu-id="13d5a-192">a.</span></span> <span data-ttu-id="13d5a-193">Dans la zone de texte **User ID** (ID utilisateur), tapez `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="13d5a-193">In the **User id** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="13d5a-194">b.</span><span class="sxs-lookup"><span data-stu-id="13d5a-194">b.</span></span> <span data-ttu-id="13d5a-195">Dans la zone de texte **Email**, tapez `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="13d5a-195">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="13d5a-196">c.</span><span class="sxs-lookup"><span data-stu-id="13d5a-196">c.</span></span> <span data-ttu-id="13d5a-197">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-197">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="13d5a-198">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="13d5a-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="13d5a-199">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="13d5a-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="13d5a-200">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="13d5a-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="13d5a-201">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="13d5a-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="13d5a-202">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="13d5a-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="13d5a-204">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="13d5a-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="13d5a-205">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="13d5a-207">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="13d5a-209">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="13d5a-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="13d5a-211">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="13d5a-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="13d5a-213">a.</span><span class="sxs-lookup"><span data-stu-id="13d5a-213">a.</span></span> <span data-ttu-id="13d5a-214">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="13d5a-215">b.</span><span class="sxs-lookup"><span data-stu-id="13d5a-215">b.</span></span> <span data-ttu-id="13d5a-216">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="13d5a-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="13d5a-217">c.</span><span class="sxs-lookup"><span data-stu-id="13d5a-217">c.</span></span> <span data-ttu-id="13d5a-218">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="13d5a-219">d.</span><span class="sxs-lookup"><span data-stu-id="13d5a-219">d.</span></span> <span data-ttu-id="13d5a-220">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-220">Click **Create**.</span></span>
 
### <a name="creating-a-bluejeans-test-user"></a><span data-ttu-id="13d5a-221">Création d’un utilisateur de test BlueJeans</span><span class="sxs-lookup"><span data-stu-id="13d5a-221">Creating a BlueJeans test user</span></span>

<span data-ttu-id="13d5a-222">Pour permettre aux utilisateurs Azure AD de se connecter à BlueJeans, vous devez les attribuer dans BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="13d5a-222">To enable Azure AD users to log in to BlueJeans, they must be provisioned into BlueJeans.</span></span>  

<span data-ttu-id="13d5a-223">Pour BlueJeans, cet approvisionnement doit se faire manuellement.</span><span class="sxs-lookup"><span data-stu-id="13d5a-223">In case of BlueJeans, provisioning is a manual task.</span></span>

<span data-ttu-id="13d5a-224">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="13d5a-224">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="13d5a-225">Connectez-vous à votre site d’entreprise **BlueJeans** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="13d5a-225">Log in to your **BlueJeans** company site as an administrator.</span></span>

2. <span data-ttu-id="13d5a-226">Accédez à **ADMIN \> Manage Users \> Add User**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-226">Go to **ADMIN \> Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="13d5a-227">![Administrateur](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="13d5a-227">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")</span></span>
   
   >[!IMPORTANT]
   ><span data-ttu-id="13d5a-228">L’onglet **Add User** est disponible uniquement si, sous l’onglet **Security**, l’option **Enable automatic provisioning** est décochée.</span><span class="sxs-lookup"><span data-stu-id="13d5a-228">The **Add User** tab is only available if, in the **Security tab**, **Enable automatic provisioning** is unchecked.</span></span> 
   
3. <span data-ttu-id="13d5a-229">Dans la section **Add User** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="13d5a-229">In the **Add User** section, perform the following steps:</span></span>

    <span data-ttu-id="13d5a-230">![Ajouter un utilisateur](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="13d5a-230">![Add User](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Add User")</span></span>
    
    <span data-ttu-id="13d5a-231">a.</span><span class="sxs-lookup"><span data-stu-id="13d5a-231">a.</span></span> <span data-ttu-id="13d5a-232">Tapez un **nom d’utilisateur BlueJeans**, une **adresse de messagerie**, un **ID de réunion BlueJeans**, un **code secret de modérateur**, un **nom complet** et la **société** d’un compte AAD valide que vous souhaitez approvisionner dans les zones de texte correspondantes.</span><span class="sxs-lookup"><span data-stu-id="13d5a-232">Type a **BlueJeans Username**, an **Email address**, a **BlueJeans Meeting ID**, a **Moderator Passcode**, a **Full Name**, the **Company** of a valid AAD account you want to provision into the related textboxes.</span></span>
    
    <span data-ttu-id="13d5a-233">b.</span><span class="sxs-lookup"><span data-stu-id="13d5a-233">b.</span></span> <span data-ttu-id="13d5a-234">Cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-234">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="13d5a-235">Vous pouvez utiliser tout autre outil ou n’importe quelle API de création de compte d’utilisateur fournis par BlueJeans pour approvisionner des comptes d’utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="13d5a-235">You can use any other BlueJeans user account creation tools or APIs provided by BlueJeans to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="13d5a-236">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="13d5a-236">Assigning the Azure AD test user</span></span>

<span data-ttu-id="13d5a-237">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="13d5a-237">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BlueJeans.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="13d5a-239">**Pour attribuer Britta Simon à BlueJeans, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="13d5a-239">**To assign Britta Simon to BlueJeans, perform the following steps:**</span></span>

1. <span data-ttu-id="13d5a-240">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-240">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="13d5a-242">Dans la liste des applications, sélectionnez **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-242">In the applications list, select **BlueJeans**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_app.png) 

3. <span data-ttu-id="13d5a-244">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-244">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="13d5a-246">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-246">Click **Add** button.</span></span> <span data-ttu-id="13d5a-247">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="13d5a-249">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="13d5a-249">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="13d5a-250">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="13d5a-251">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="13d5a-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="13d5a-252">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="13d5a-252">Testing single sign-on</span></span>

<span data-ttu-id="13d5a-253">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="13d5a-253">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="13d5a-254">Quand vous cliquez sur la vignette BlueJeans dans le panneau d’accès, la page de connexion de l’application BlueJeans doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="13d5a-254">When you click the BlueJeans tile in the Access Panel, you should get login page of BlueJeans application.</span></span>
<span data-ttu-id="13d5a-255">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="13d5a-255">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="13d5a-256">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="13d5a-256">Additional resources</span></span>

* [<span data-ttu-id="13d5a-257">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="13d5a-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="13d5a-258">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="13d5a-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_203.png

