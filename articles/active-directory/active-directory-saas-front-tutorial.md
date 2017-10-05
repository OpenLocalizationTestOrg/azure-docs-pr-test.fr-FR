---
title: "Didacticiel : Intégration d’Azure Active Directory à Front | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Front."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: d936bc50a66ac2a3c17038ff08351edf9902c99f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a><span data-ttu-id="0c7d4-103">Didacticiel : Intégration d’Azure Active Directory avec Front</span><span class="sxs-lookup"><span data-stu-id="0c7d4-103">Tutorial: Azure Active Directory integration with Front</span></span>

<span data-ttu-id="0c7d4-104">Dans ce didacticiel, vous allez apprendre à intégrer Front dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0c7d4-104">In this tutorial, you learn how to integrate Front with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0c7d4-105">L’intégration de Front dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="0c7d4-105">Integrating Front with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0c7d4-106">Dans Azure AD, vous pouvez contrôler qui a accès à Front.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-106">You can control in Azure AD who has access to Front.</span></span>
- <span data-ttu-id="0c7d4-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Front (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-107">You can enable your users to automatically get signed-on to Front (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0c7d4-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="0c7d4-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0c7d4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c7d4-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0c7d4-110">Prerequisites</span></span>

<span data-ttu-id="0c7d4-111">Pour configurer l’intégration d’Azure AD avec Front, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0c7d4-111">To configure Azure AD integration with Front, you need the following items:</span></span>

- <span data-ttu-id="0c7d4-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c7d4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0c7d4-113">Un abonnement Front pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="0c7d4-113">A Front single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0c7d4-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0c7d4-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="0c7d4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0c7d4-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0c7d4-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0c7d4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0c7d4-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="0c7d4-118">Scenario description</span></span>
<span data-ttu-id="0c7d4-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0c7d4-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="0c7d4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0c7d4-121">Ajout de Front depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="0c7d4-121">Adding Front from the gallery</span></span>
2. <span data-ttu-id="0c7d4-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c7d4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-front-from-the-gallery"></a><span data-ttu-id="0c7d4-123">Ajout de Front depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="0c7d4-123">Adding Front from the gallery</span></span>
<span data-ttu-id="0c7d4-124">Pour configurer l’intégration de Front avec Azure AD, vous devez ajouter Front, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-124">To configure the integration of Front into Azure AD, you need to add Front from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0c7d4-125">**Pour ajouter Front à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0c7d4-125">**To add Front from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0c7d4-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="0c7d4-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0c7d4-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="0c7d4-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="0c7d4-133">Dans la zone de recherche, tapez **Front**, sélectionnez **Front** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-133">In the search box, type **Front**, select **Front** from result panel then click **Add** button to add the application.</span></span>

    ![Front dans la liste des résultats](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0c7d4-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c7d4-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0c7d4-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Front, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="0c7d4-136">In this section, you configure and test Azure AD single sign-on with Front based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0c7d4-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Front correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Front is to a user in Azure AD.</span></span> <span data-ttu-id="0c7d4-138">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Front associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-138">In other words, a link relationship between an Azure AD user and the related user in Front needs to be established.</span></span>

<span data-ttu-id="0c7d4-139">Dans Front, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-139">In Front, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0c7d4-140">Pour configurer et tester l’authentification unique Azure AD avec Front, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="0c7d4-140">To configure and test Azure AD single sign-on with Front, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0c7d4-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0c7d4-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0c7d4-143">**[Créer un utilisateur de test Front](#create-a-front-test-user)** pour avoir un équivalent de Britta Simon dans Front lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-143">**[Create a Front test user](#create-a-front-test-user)** - to have a counterpart of Britta Simon in Front that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0c7d4-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0c7d4-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0c7d4-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c7d4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0c7d4-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Front.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Front application.</span></span>

<span data-ttu-id="0c7d4-148">**Pour configurer l’authentification unique Azure AD avec Front, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0c7d4-148">**To configure Azure AD single sign-on with Front, perform the following steps:**</span></span>

1. <span data-ttu-id="0c7d4-149">Dans le portail Azure, sur la page d’intégration de l’application **Front**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-149">In the Azure portal, on the **Front** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="0c7d4-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. <span data-ttu-id="0c7d4-153">Dans la section **Domaine et URL Front**, si vous souhaitez configurer l’application en mode initié par **IDP**, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="0c7d4-153">On the **Front Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    <span data-ttu-id="0c7d4-155">a.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-155">a.</span></span> <span data-ttu-id="0c7d4-156">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="0c7d4-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com`</span></span>

    <span data-ttu-id="0c7d4-157">b.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-157">b.</span></span> <span data-ttu-id="0c7d4-158">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<companyname>.frontapp.com/sso/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="0c7d4-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com/sso/saml/callback`</span></span>

4. <span data-ttu-id="0c7d4-159">Cochez **Afficher les paramètres d’URL avancés** si vous souhaitez configurer l’application en mode initié par le **fournisseur de service** :</span><span class="sxs-lookup"><span data-stu-id="0c7d4-159">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    <span data-ttu-id="0c7d4-161">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="0c7d4-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="0c7d4-162">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-162">These values are not real.</span></span> <span data-ttu-id="0c7d4-163">Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL d’authentification unique réels qui sont décrits plus loin dans le didacticiel, ou contactez l’[équipe de support technique Front](mailto:support@frontapp.com) pour obtenir ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL which are explained later in tutorial or contact [Front Client support team](mailto:support@frontapp.com) to get these values.</span></span> 

5. <span data-ttu-id="0c7d4-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. <span data-ttu-id="0c7d4-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="0c7d4-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="0c7d4-168">Dans la section **Configuration de Front** , cliquez sur **Configurer Front** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-168">On the **Front Configuration** section, click **Configure Front** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0c7d4-169">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="0c7d4-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. <span data-ttu-id="0c7d4-171">Connectez-vous à votre client Front en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-171">Sign-on to your Front tenant as an administrator.</span></span>

9. <span data-ttu-id="0c7d4-172">Accédez à **Paramètres (icône représentant une roue dentée en bas de la barre latérale gauche) > Préférences**.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-172">Go to **Settings (cog icon at the bottom of the left sidebar) > Preferences**.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. <span data-ttu-id="0c7d4-174">Cliquez sur le lien **Authentification unique** .</span><span class="sxs-lookup"><span data-stu-id="0c7d4-174">Click **Single Sign On** link.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. <span data-ttu-id="0c7d4-176">Sélectionnez **SAML** dans la liste déroulante **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-176">Select **SAML** in the drop-down list of **Single Sign On**.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. <span data-ttu-id="0c7d4-178">Dans la zone de texte **Point d’entrée** copiez la valeur de **URL du service d’authentification unique** indiquée dans l’Assistant Configuration de l’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-178">In the **Entry Point** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
    
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. <span data-ttu-id="0c7d4-180">Ouvrez dans le Bloc-notes votre fichier **Certificate(Base64)** téléchargé, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **Certificat de signature**.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-180">Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Signing certificate** textbox.</span></span>
    
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. <span data-ttu-id="0c7d4-182">Dans la section **Service provider settings** (Paramètres du fournisseur de services), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0c7d4-182">On the **Service provider settings** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    <span data-ttu-id="0c7d4-184">a.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-184">a.</span></span> <span data-ttu-id="0c7d4-185">Copiez la valeur de l’**ID d’entité** et collez-la dans la zone de texte **Identificateur** de la section **Domaine et URL Front** du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-185">Copy the value of **Entity ID** and paste it into the **Identifier** textbox in **Front Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="0c7d4-186">b.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-186">b.</span></span> <span data-ttu-id="0c7d4-187">Copiez la valeur de l’**URL ACS** et collez-la dans la zone de texte **URL de connexion** de la section **Domaine et URL Front** du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-187">Copy the value of **ACS URL** and paste it into the **Sign-on URL** textbox in **Front Domain and URLs** section in Azure portal.</span></span>
    
15. <span data-ttu-id="0c7d4-188">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="0c7d4-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="0c7d4-189">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0c7d4-190">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0c7d4-191">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0c7d4-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0c7d4-192">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c7d4-192">Create an Azure AD test user</span></span>

<span data-ttu-id="0c7d4-193">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="0c7d4-195">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0c7d4-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0c7d4-196">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="0c7d4-198">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="0c7d4-200">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="0c7d4-202">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0c7d4-202">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    <span data-ttu-id="0c7d4-204">a.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-204">a.</span></span> <span data-ttu-id="0c7d4-205">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-205">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0c7d4-206">b.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-206">b.</span></span> <span data-ttu-id="0c7d4-207">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-207">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="0c7d4-208">c.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-208">c.</span></span> <span data-ttu-id="0c7d4-209">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="0c7d4-210">d.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-210">d.</span></span> <span data-ttu-id="0c7d4-211">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-211">Click **Create**.</span></span>
 
### <a name="create-a-front-test-user"></a><span data-ttu-id="0c7d4-212">Créer un utilisateur de test Front</span><span class="sxs-lookup"><span data-stu-id="0c7d4-212">Create a Front test user</span></span>

<span data-ttu-id="0c7d4-213">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Front.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-213">In this section, you create a user called Britta Simon in Front.</span></span> <span data-ttu-id="0c7d4-214">Collaborez avec l’[équipe de support technique Front](mailto:support@frontapp.com) pour ajouter des utilisateurs dans la plateforme Front.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-214">Work with [Front Client support team](mailto:support@frontapp.com) to add the users in the Front platform.</span></span> <span data-ttu-id="0c7d4-215">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-215">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="0c7d4-216">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c7d4-216">Assign the Azure AD test user</span></span>

<span data-ttu-id="0c7d4-217">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Front.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Front.</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="0c7d4-219">**Pour affecter Britta Simon à Front, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0c7d4-219">**To assign Britta Simon to Front, perform the following steps:**</span></span>

1. <span data-ttu-id="0c7d4-220">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="0c7d4-222">Dans la liste des applications, sélectionnez **Front**.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-222">In the applications list, select **Front**.</span></span>

    ![Lien Front dans la liste des applications](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. <span data-ttu-id="0c7d4-224">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="0c7d4-226">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-226">Click **Add** button.</span></span> <span data-ttu-id="0c7d4-227">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="0c7d4-229">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0c7d4-230">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0c7d4-231">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0c7d4-232">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="0c7d4-232">Test single sign-on</span></span>

<span data-ttu-id="0c7d4-233">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-233">The objective of this section is to test your Azure AD SSOconfiguration using the Access Panel.</span></span>

<span data-ttu-id="0c7d4-234">Lorsque vous cliquez sur la vignette Front dans le volet d’accès, vous devez être connecté automatiquement à votre application Front.</span><span class="sxs-lookup"><span data-stu-id="0c7d4-234">When you click the Front tile in the Access Panel, you should get automatically signed-on to your Front application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0c7d4-235">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="0c7d4-235">Additional resources</span></span>

* [<span data-ttu-id="0c7d4-236">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0c7d4-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0c7d4-237">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="0c7d4-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png

