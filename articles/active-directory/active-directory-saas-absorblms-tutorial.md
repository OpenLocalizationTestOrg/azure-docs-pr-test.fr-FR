---
title: "Didacticiel : Intégration d’Azure Active Directory à Absorb LMS | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Absorb LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 3c68c3ac7d6be593476d419f8c015931b206eead
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a><span data-ttu-id="74e07-103">Didacticiel : Intégration d’Azure Active Directory avec Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="74e07-103">Tutorial: Azure Active Directory integration with Absorb LMS</span></span>

<span data-ttu-id="74e07-104">Dans ce didacticiel, vous allez apprendre à intégrer Absorb LMS avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="74e07-104">In this tutorial, you learn how to integrate Absorb LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="74e07-105">L’intégration d’Absorb LMS avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="74e07-105">Integrating Absorb LMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="74e07-106">Dans Azure AD, vous pouvez contrôler qui a accès à Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="74e07-106">You can control in Azure AD who has access to Absorb LMS</span></span>
- <span data-ttu-id="74e07-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Absorb LMS (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="74e07-107">You can enable your users to automatically get signed-on to Absorb LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="74e07-108">Vous pouvez gérer vos comptes depuis un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="74e07-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="74e07-109">Pour en savoir plus sur l’intégration de l’application SaaS avec Azure AD, consultez</span><span class="sxs-lookup"><span data-stu-id="74e07-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="74e07-110">[Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="74e07-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74e07-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="74e07-111">Prerequisites</span></span>

<span data-ttu-id="74e07-112">Pour configurer l’intégration d’Azure AD avec Absorb LMS, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="74e07-112">To configure Azure AD integration with Absorb LMS, you need the following items:</span></span>

- <span data-ttu-id="74e07-113">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="74e07-113">An Azure AD subscription</span></span>
- <span data-ttu-id="74e07-114">Un abonnement Absorb LMS pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="74e07-114">An Absorb LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="74e07-115">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="74e07-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="74e07-116">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="74e07-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="74e07-117">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="74e07-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="74e07-118">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="74e07-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="74e07-119">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="74e07-119">Scenario description</span></span>
<span data-ttu-id="74e07-120">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="74e07-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="74e07-121">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="74e07-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="74e07-122">Ajout d’Absorb LMS à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="74e07-122">Adding Absorb LMS from the gallery</span></span>
2. <span data-ttu-id="74e07-123">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="74e07-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-absorb-lms-from-the-gallery"></a><span data-ttu-id="74e07-124">Ajout d’Absorb LMS à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="74e07-124">Adding Absorb LMS from the gallery</span></span>
<span data-ttu-id="74e07-125">Pour configurer l’intégration d’Absorb LMS avec Azure AD, vous devez ajouter Absorb LMS à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="74e07-125">To configure the integration of Absorb LMS in to Azure AD, you need to add Absorb LMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="74e07-126">**Pour ajouter Absorb LMS à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="74e07-126">**To add Absorb LMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="74e07-127">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="74e07-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="74e07-129">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="74e07-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="74e07-130">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="74e07-130">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="74e07-132">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="74e07-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="74e07-134">Dans la zone de recherche, tapez **Absorb LMS**, sélectionnez **Absorb LMS** dans le panneau de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="74e07-134">In the search box, type **Absorb LMS**, select **Absorb LMS** from result panel then click **Add** button to add the application.</span></span>

    ![Absorb LMS dans la liste des résultats](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="74e07-136">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="74e07-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="74e07-137">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Absorb LMS, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="74e07-137">In this section, you configure and test Azure AD single sign-on with Absorb LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="74e07-138">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Absorb LMS équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="74e07-138">For single sign-on to work, Azure AD needs to know what the counterpart user in Absorb LMS is to a user in Azure AD.</span></span> <span data-ttu-id="74e07-139">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Absorb LMS associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="74e07-139">In other words, a link relationship between an Azure AD user and the related user in Absorb LMS needs to be established.</span></span>

<span data-ttu-id="74e07-140">Pour ce faire, affectez la valeur du champ **nom d’utilisateur** d’Azure AD comme valeur du champ **Username** (Nom d’utilisateur) dans Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="74e07-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Absorb LMS.</span></span>

<span data-ttu-id="74e07-141">Pour configurer et tester l’authentification unique Azure AD avec Absorb LMS, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="74e07-141">To configure and test Azure AD single sign-on with Absorb LMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="74e07-142">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="74e07-142">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="74e07-143">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="74e07-143">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="74e07-144">**[Créer un utilisateur test Absorb LMS](#create-an-absorb-lms-test-user)** pour avoir un équivalent de Britta Simon dans Absorb LMS lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="74e07-144">**[Create an Absorb LMS test user](#create-an-absorb-lms-test-user)** - to have a counterpart of Britta Simon in Absorb LMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="74e07-145">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="74e07-145">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="74e07-146">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="74e07-146">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="74e07-147">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="74e07-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="74e07-148">Dans cette section, vous allez activer l’authentification unique Azure AD dans le nouveau portail Azure et configurer l’authentification unique dans votre application Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="74e07-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Absorb LMS application.</span></span>

<span data-ttu-id="74e07-149">**Pour configurer l’authentification unique Azure AD avec Absorb LMS, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="74e07-149">**To configure Azure AD single sign-on with Absorb LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="74e07-150">Dans le portail Azure, sur la page d’intégration de l’application **Absorb LMS**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="74e07-150">In the Azure portal, on the **Absorb LMS** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="74e07-152">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="74e07-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. <span data-ttu-id="74e07-154">Dans la section **Domaine et URL Absorb LMS**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="74e07-154">On the **Absorb LMS Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    <span data-ttu-id="74e07-156">a.</span><span class="sxs-lookup"><span data-stu-id="74e07-156">a.</span></span> <span data-ttu-id="74e07-157">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="74e07-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>

    <span data-ttu-id="74e07-158">b.</span><span class="sxs-lookup"><span data-stu-id="74e07-158">b.</span></span> <span data-ttu-id="74e07-159">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="74e07-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="74e07-160">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="74e07-160">These values are not the real.</span></span> <span data-ttu-id="74e07-161">Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="74e07-161">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="74e07-162">Pour obtenir ces valeurs, contactez l’[équipe de support technique Absorb LMS](https://www.absorblms.com/support).</span><span class="sxs-lookup"><span data-stu-id="74e07-162">Contact [Absorb LMS Client support team](https://www.absorblms.com/support) to get these values.</span></span> 

4. <span data-ttu-id="74e07-163">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="74e07-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Lien Téléchargement de certificat](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. <span data-ttu-id="74e07-165">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="74e07-165">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="74e07-167">Dans la section **Configuration de Absorb LMS** , cliquez sur **Configurer Absorb LMS** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="74e07-167">On the **Absorb LMS Configuration** section, click **Configure Absorb LMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="74e07-168">Copiez **l’URL de déconnexion et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="74e07-168">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuration d’Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. <span data-ttu-id="74e07-170">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise Absorb LMS en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="74e07-170">In a different web browser window, log in to your Absorb LMS company site as an administrator.</span></span>

9. <span data-ttu-id="74e07-171">Cliquez sur **l’icône du compte** dans l’interface d’administration.</span><span class="sxs-lookup"><span data-stu-id="74e07-171">Click the **Account Icon** on the admin interface.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-absorblms-tutorial/1.png)

10. <span data-ttu-id="74e07-173">Cliquez sur **Paramètres du portail**.</span><span class="sxs-lookup"><span data-stu-id="74e07-173">Click **Portal Settings**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. <span data-ttu-id="74e07-175">Cliquez sur l’onglet **Users** .</span><span class="sxs-lookup"><span data-stu-id="74e07-175">Click the **Users** tab.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-absorblms-tutorial/3.png)

12. <span data-ttu-id="74e07-177">Pour accéder aux champs de configuration de l’authentification unique, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="74e07-177">Perform the following steps to access the Single Sign-On configuration fields:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-absorblms-tutorial/4.png)

    <span data-ttu-id="74e07-179">a.</span><span class="sxs-lookup"><span data-stu-id="74e07-179">a.</span></span> <span data-ttu-id="74e07-180">Sélectionnez le **Mode** approprié.</span><span class="sxs-lookup"><span data-stu-id="74e07-180">Select the appropriate **Mode**.</span></span>

    <span data-ttu-id="74e07-181">b.</span><span class="sxs-lookup"><span data-stu-id="74e07-181">b.</span></span> <span data-ttu-id="74e07-182">Ouvrez le certificat que vous avez téléchargé à partir du portail Azure dans le bloc-notes, supprimez les balises **---BEGIN CERTIFICATE---** et **---END CERTIFICATE---**, puis collez le contenu restant dans la zone de texte **Key** (Clé).</span><span class="sxs-lookup"><span data-stu-id="74e07-182">Open the Certificate that you have downloaded from the Azure portal in notepad, remove the **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste the remaining content in the **Key** textbox.</span></span>
    
    <span data-ttu-id="74e07-183">c.</span><span class="sxs-lookup"><span data-stu-id="74e07-183">c.</span></span> <span data-ttu-id="74e07-184">Dans **Id Property** (Propriété d’ID), sélectionnez l’attribut approprié configuré comme identificateur d’utilisateur dans Azure AD (par exemple, si userprinciplename est sélectionné dans Azure AD, ici vous devez sélectionner Username.)</span><span class="sxs-lookup"><span data-stu-id="74e07-184">In the **Id Property**, select the appropriate attribute which you have configured as the user identifier in the Azure AD (For example, If the userprinciplename is selected in Azure AD, then Username would be selected here.)</span></span>

    <span data-ttu-id="74e07-185">d.</span><span class="sxs-lookup"><span data-stu-id="74e07-185">d.</span></span> <span data-ttu-id="74e07-186">Dans **Login URL** (URL de connexion), collez la valeur **« URL du service d’authentification unique »** que vous avez copiée dans la fenêtre **Configurer l’authentification** du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="74e07-186">In the **Login URL**, paste the **“SAML Single Sign-On Service URL”** value you have copied from the **Configure sign-on** window of the Azure portal.</span></span>

    <span data-ttu-id="74e07-187">e.</span><span class="sxs-lookup"><span data-stu-id="74e07-187">e.</span></span> <span data-ttu-id="74e07-188">Dans **Logout URL** (URL de connexion), collez la valeur **« URL de déconnexion »** que vous avez copiée dans la fenêtre **Configurer l’authentification** du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="74e07-188">In the **Logout URL**, paste the **“Sign-Out URL”** value you have copied from the **Configure sign-on** window of the Azure portal.</span></span>

13. <span data-ttu-id="74e07-189">Activez **« Autoriser uniquement la connexion SSO »**.</span><span class="sxs-lookup"><span data-stu-id="74e07-189">Enable **‘Only Allow SSO Login’**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-absorblms-tutorial/5.png)

14. <span data-ttu-id="74e07-191">Cliquez sur **Save** (Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="74e07-191">Click **"Save."**</span></span>

> [!TIP]
> <span data-ttu-id="74e07-192">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="74e07-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="74e07-193">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="74e07-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="74e07-194">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="74e07-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="74e07-195">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="74e07-195">Create an Azure AD test user</span></span>

<span data-ttu-id="74e07-196">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="74e07-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="74e07-198">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="74e07-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="74e07-199">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="74e07-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="74e07-201">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="74e07-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="74e07-203">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="74e07-203">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Bouton Ajouter](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="74e07-205">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="74e07-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="74e07-207">a.</span><span class="sxs-lookup"><span data-stu-id="74e07-207">a.</span></span> <span data-ttu-id="74e07-208">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="74e07-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="74e07-209">b.</span><span class="sxs-lookup"><span data-stu-id="74e07-209">b.</span></span> <span data-ttu-id="74e07-210">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="74e07-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="74e07-211">c.</span><span class="sxs-lookup"><span data-stu-id="74e07-211">c.</span></span> <span data-ttu-id="74e07-212">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="74e07-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="74e07-213">d.</span><span class="sxs-lookup"><span data-stu-id="74e07-213">d.</span></span> <span data-ttu-id="74e07-214">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="74e07-214">Click **Create**.</span></span>

### <a name="create-an-absorb-lms-test-user"></a><span data-ttu-id="74e07-215">Créer un utilisateur de test Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="74e07-215">Create an Absorb LMS test user</span></span>

<span data-ttu-id="74e07-216">Pour se connecter à Absorb LMS, les utilisateurs d’Azure AD doivent être approvisionnés dans Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="74e07-216">To enable Azure AD users to log in to Absorb LMS, they must be provisioned in to Absorb LMS.</span></span>  
<span data-ttu-id="74e07-217">Pour Absorb LMS, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="74e07-217">For Absorb LMS, provisioning is a manual task.</span></span>

<span data-ttu-id="74e07-218">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="74e07-218">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="74e07-219">Connectez-vous à votre site d’entreprise Absorb LMS en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="74e07-219">Log in to your Absorb LMS company site as an administrator.</span></span>

2. <span data-ttu-id="74e07-220">Cliquez sur l’onglet **Users** (Utilisateurs).</span><span class="sxs-lookup"><span data-stu-id="74e07-220">Click **Users** tab.</span></span>

    ![Inviter des personnes](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. <span data-ttu-id="74e07-222">Cliquez sur **Users** (Utilisateurs) sous l’onglet **Users**.</span><span class="sxs-lookup"><span data-stu-id="74e07-222">Click **Users** under the **Users** tab.</span></span>

    ![Inviter des personnes](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  <span data-ttu-id="74e07-224">Sélectionnez **User** (Utilisateur) dans la liste déroulante **Add New** (Ajouter nouveau).</span><span class="sxs-lookup"><span data-stu-id="74e07-224">Select **User** from **Add New** drop-down.</span></span>

    ![Inviter des personnes](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. <span data-ttu-id="74e07-226">Dans la page **Add user** (Ajouter un utilisateur), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="74e07-226">On the **Add User** page, perform the following steps:</span></span>

    ![Inviter des personnes](./media/active-directory-saas-absorblms-tutorial/user.png)

    <span data-ttu-id="74e07-228">a.</span><span class="sxs-lookup"><span data-stu-id="74e07-228">a.</span></span> <span data-ttu-id="74e07-229">Dans la zone de texte **First Name** (Prénom), tapez le prénom, par exemple Britta.</span><span class="sxs-lookup"><span data-stu-id="74e07-229">In the **First Name** textbox, type the first name like Britta.</span></span>

    <span data-ttu-id="74e07-230">b.</span><span class="sxs-lookup"><span data-stu-id="74e07-230">b.</span></span> <span data-ttu-id="74e07-231">Dans la zone de texte **Last Name** (Nom), tapez le nom, par exemple Simon.</span><span class="sxs-lookup"><span data-stu-id="74e07-231">In the **Last Name** textbox, type the last name like Simon.</span></span>
    
    <span data-ttu-id="74e07-232">c.</span><span class="sxs-lookup"><span data-stu-id="74e07-232">c.</span></span> <span data-ttu-id="74e07-233">Dans la zone de texte **Username** (Nom d’utilisateur), tapez le nom d’utilisateur, par exemple Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="74e07-233">In the **Username** textbox, type the user name like Britta Simon.</span></span>

    <span data-ttu-id="74e07-234">d.</span><span class="sxs-lookup"><span data-stu-id="74e07-234">d.</span></span> <span data-ttu-id="74e07-235">Dans la zone de texte **Password** (Mot de passe), tapez le mot de passe de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="74e07-235">In the **Password** textbox, type the password of Britta Simon.</span></span>

    <span data-ttu-id="74e07-236">e.</span><span class="sxs-lookup"><span data-stu-id="74e07-236">e.</span></span> <span data-ttu-id="74e07-237">Dans la zone de texte **Confirmer le mot de passe**, tapez le même mot de passe.</span><span class="sxs-lookup"><span data-stu-id="74e07-237">In the **Confirm Password** textbox, type the same password.</span></span>
    
    <span data-ttu-id="74e07-238">f.</span><span class="sxs-lookup"><span data-stu-id="74e07-238">f.</span></span> <span data-ttu-id="74e07-239">Définissez-le comme **ACTIVE** (Actif).</span><span class="sxs-lookup"><span data-stu-id="74e07-239">Make it as **ACTIVE**.</span></span>   

6. <span data-ttu-id="74e07-240">Cliquez sur **Save** (Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="74e07-240">Click **"Save."**</span></span>
 
### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="74e07-241">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="74e07-241">Assign the Azure AD test user</span></span>

<span data-ttu-id="74e07-242">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="74e07-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Absorb LMS.</span></span>

![Attribuer le rôle utilisateur][200]

<span data-ttu-id="74e07-244">**Pour affecter Britta Simon à Absorb LMS, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="74e07-244">**To assign Britta Simon to Absorb LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="74e07-245">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="74e07-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="74e07-247">Dans la liste des applications, sélectionnez **Absorb LMS**.</span><span class="sxs-lookup"><span data-stu-id="74e07-247">In the applications list, select **Absorb LMS**.</span></span>

    ![Lien Absorb LMS dans la liste des applications](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. <span data-ttu-id="74e07-249">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="74e07-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202] 

4. <span data-ttu-id="74e07-251">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="74e07-251">Click **Add** button.</span></span> <span data-ttu-id="74e07-252">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="74e07-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="74e07-254">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="74e07-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="74e07-255">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="74e07-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="74e07-256">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="74e07-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="74e07-257">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="74e07-257">Test single sign-on</span></span>

<span data-ttu-id="74e07-258">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="74e07-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="74e07-259">Lorsque vous cliquez sur la vignette Absorb LMS dans le volet d’accès, vous êtes automatiquement connecté à votre application Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="74e07-259">Click the Absorb LMS tile in the Access Panel, you will get automatically signed-on to your Absorb LMS application.</span></span> <span data-ttu-id="74e07-260">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="74e07-260">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="74e07-261">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="74e07-261">Additional resources</span></span>

* [<span data-ttu-id="74e07-262">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="74e07-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="74e07-263">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="74e07-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

