---
title: "Didacticiel : Intégration d'Azure Active Directory à Dropbox for Business | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Dropbox for Business."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: a56a5af171eaca259db29f25fee4331a77313420
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a><span data-ttu-id="b569c-103">Didacticiel : Intégration d'Azure Active Directory à Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="b569c-103">Tutorial: Azure Active Directory integration with Dropbox for Business</span></span>

<span data-ttu-id="b569c-104">Dans ce didacticiel, vous allez apprendre à intégrer Dropbox for Business à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b569c-104">In this tutorial, you learn how to integrate Dropbox for Business with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b569c-105">L’intégration de Dropbox for Business à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="b569c-105">Integrating Dropbox for Business with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b569c-106">Dans Azure AD, vous pouvez contrôler qui a accès à Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="b569c-106">You can control in Azure AD who has access to Dropbox for Business</span></span>
- <span data-ttu-id="b569c-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Dropbox for Business (par le biais de l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="b569c-107">You can enable your users to automatically get signed-on to Dropbox for Business (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b569c-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="b569c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b569c-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b569c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b569c-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b569c-110">Prerequisites</span></span>

<span data-ttu-id="b569c-111">Pour configurer l’intégration d’Azure AD avec Dropbox for Business, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b569c-111">To configure Azure AD integration with Dropbox for Business, you need the following items:</span></span>

- <span data-ttu-id="b569c-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="b569c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b569c-113">Un abonnement Dropbox for Business pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="b569c-113">A Dropbox for Business single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b569c-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="b569c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b569c-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b569c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b569c-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b569c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b569c-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b569c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b569c-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="b569c-118">Scenario description</span></span>
<span data-ttu-id="b569c-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="b569c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b569c-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="b569c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b569c-121">Ajout de Dropbox for Business à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="b569c-121">Adding Dropbox for Business from the gallery</span></span>
2. <span data-ttu-id="b569c-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b569c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dropbox-for-business-from-the-gallery"></a><span data-ttu-id="b569c-123">Ajout de Dropbox for Business à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="b569c-123">Adding Dropbox for Business from the gallery</span></span>
<span data-ttu-id="b569c-124">Pour configurer l’intégration de Dropbox for Business à Azure AD, vous devez ajouter Dropbox for Business depuis la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="b569c-124">To configure the integration of Dropbox for Business into Azure AD, you need to add Dropbox for Business from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b569c-125">**Pour ajouter Dropbox for Business à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="b569c-125">**To add Dropbox for Business from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b569c-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b569c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b569c-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="b569c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b569c-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b569c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="b569c-131">Cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b569c-131">Click **New application** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="b569c-133">Dans la zone de recherche, tapez **Dropbox for Business**.</span><span class="sxs-lookup"><span data-stu-id="b569c-133">In the search box, type **Dropbox for Business**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. <span data-ttu-id="b569c-135">Dans le volet des résultats, sélectionnez **Dropbox for Business**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="b569c-135">In the results panel, select **Dropbox for Business**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b569c-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b569c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b569c-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Dropbox for Business, en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="b569c-138">In this section, you configure and test Azure AD single sign-on with Dropbox for Business based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b569c-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Dropbox for Business équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b569c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Dropbox for Business is to a user in Azure AD.</span></span> <span data-ttu-id="b569c-140">En d’autres termes, un lien entre un utilisateur Azure AD et l’utilisateur Dropbox for Business associé doit être établi.</span><span class="sxs-lookup"><span data-stu-id="b569c-140">In other words, a link relationship between an Azure AD user and the related user in Dropbox for Business needs to be established.</span></span>

<span data-ttu-id="b569c-141">Pour ce faire, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="b569c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Dropbox for Business.</span></span>

<span data-ttu-id="b569c-142">Pour configurer et tester l’authentification unique Azure AD avec Dropbox for Business, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="b569c-142">To configure and test Azure AD single sign-on with Dropbox for Business, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b569c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="b569c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b569c-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b569c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b569c-145">**[Création d’un utilisateur de test Dropbox for Business](#creating-a-dropbox-for-business-test-user)** pour avoir un équivalent de Britta Simon dans Dropbox for Business lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="b569c-145">**[Creating a Dropbox for Business test user](#creating-a-dropbox-for-business-test-user)** - to have a counterpart of Britta Simon in Dropbox for Business that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b569c-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b569c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b569c-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="b569c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b569c-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b569c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b569c-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="b569c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dropbox for Business application.</span></span>

<span data-ttu-id="b569c-150">**Pour configurer l’authentification unique Azure AD avec Dropbox for Business, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="b569c-150">**To configure Azure AD single sign-on with Dropbox for Business, perform the following steps:**</span></span>

1. <span data-ttu-id="b569c-151">Dans le portail Azure, dans la page d’intégration de l’application **Dropbox for Business**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="b569c-151">In the Azure portal, on the **Dropbox for Business** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="b569c-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b569c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. <span data-ttu-id="b569c-155">Dans la section **Domaine et URL Dropbox for Business**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="b569c-155">On the **Dropbox for Business Domain and URLs** section, perform the following steps:</span></span>

    <span data-ttu-id="b569c-156">a.</span><span class="sxs-lookup"><span data-stu-id="b569c-156">a.</span></span> <span data-ttu-id="b569c-157">Connectez-vous à votre abonné Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="b569c-157">Sign on to your Dropbox for business tenant.</span></span> 
   
    <span data-ttu-id="b569c-158">![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="b569c-158">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="b569c-159">b.</span><span class="sxs-lookup"><span data-stu-id="b569c-159">b.</span></span> <span data-ttu-id="b569c-160">À gauche du volet de navigation, cliquez sur **Console d’administration**.</span><span class="sxs-lookup"><span data-stu-id="b569c-160">In the navigation pane on the left side, click **Admin Console**.</span></span> 
   
    <span data-ttu-id="b569c-161">![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="b569c-161">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="b569c-162">c.</span><span class="sxs-lookup"><span data-stu-id="b569c-162">c.</span></span> <span data-ttu-id="b569c-163">Dans la **Console d’administration**, cliquez sur **Authentification** dans le volet de navigation gauche.</span><span class="sxs-lookup"><span data-stu-id="b569c-163">On the **Admin Console**, click **Authentication** in the left navigation pane.</span></span> 
   
    <span data-ttu-id="b569c-164">![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="b569c-164">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="b569c-165">d.</span><span class="sxs-lookup"><span data-stu-id="b569c-165">d.</span></span> <span data-ttu-id="b569c-166">Dans la section **Authentification unique**, sélectionnez **Activer l’authentification unique**, puis cliquez sur **Plus** pour développer cette section.</span><span class="sxs-lookup"><span data-stu-id="b569c-166">In the **Single sign-on** section, select **Enable single sign-on**, and then click **More** to expand this section.</span></span>  
   
    <span data-ttu-id="b569c-167">![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="b569c-167">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="b569c-168">e.</span><span class="sxs-lookup"><span data-stu-id="b569c-168">e.</span></span> <span data-ttu-id="b569c-169">Copiez l’URL en regard de **Les utilisateurs peuvent se connecter en entrant leur adresse e-mail ou accéder directement à**.</span><span class="sxs-lookup"><span data-stu-id="b569c-169">Copy the URL next to **Users can sign in by entering their email address or they can go directly to**.</span></span> 
    
    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    <span data-ttu-id="b569c-171">f.</span><span class="sxs-lookup"><span data-stu-id="b569c-171">f.</span></span> <span data-ttu-id="b569c-172">Sur le portail Azure, dans la zone de texte **URL de connexion**, collez l’URL.</span><span class="sxs-lookup"><span data-stu-id="b569c-172">On the Azure portal, in the **Sign-on URL** textbox, paste the URL.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     <span data-ttu-id="b569c-174">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://www.dropbox.com/sso/<id>`</span><span class="sxs-lookup"><span data-stu-id="b569c-174">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.dropbox.com/sso/<id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b569c-175">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="b569c-175">This value is not real value.</span></span> <span data-ttu-id="b569c-176">Mettez à jour la valeur avec l’URL de connexion réelle que vous obtenez à partir de la section Authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b569c-176">Update the value with the actual Sign-on URL you get from their Single sign-on section.</span></span> <span data-ttu-id="b569c-177">Contactez [l’équipe de prise en charge des clients Dropbox for Business ](https://www.dropbox.com/business/contact) pour obtenir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="b569c-177">Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact) to get this value.</span></span> 
 
4. <span data-ttu-id="b569c-178">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b569c-178">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. <span data-ttu-id="b569c-180">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="b569c-180">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b569c-182">Dans la section **Configuration de Dropbox for Business**, cliquez sur **Configurer Dropbox for Business** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="b569c-182">On the **Dropbox for Business Configuration** section, click **Configure Dropbox for Business** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b569c-183">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="b569c-183">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. <span data-ttu-id="b569c-185">Pour configurer l’authentification unique coté **Dropbox for Business**, accédez à votre abonné Dropbox for Business, dans la section **Authentification unique** de la page **Authentification**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="b569c-185">To configure single sign-on on **Dropbox for Business** side, Go on your Dropbox for Business tenant, in the **Single sign-on** section of the **Authentication** page, perform the following steps:</span></span> 
   
    <span data-ttu-id="b569c-186">![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="b569c-186">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="b569c-187">a.</span><span class="sxs-lookup"><span data-stu-id="b569c-187">a.</span></span> <span data-ttu-id="b569c-188">Cliquez sur **Obligatoire**.</span><span class="sxs-lookup"><span data-stu-id="b569c-188">Click **Required**.</span></span>
   
    <span data-ttu-id="b569c-189">b.</span><span class="sxs-lookup"><span data-stu-id="b569c-189">b.</span></span> <span data-ttu-id="b569c-190">Sur le portail Azure, dans la fenêtre **Configurer l’authentification**, copiez la valeur **URL du service d’authentification unique SAML**, puis collez-la dans la zone de texte **URL de connexion**.</span><span class="sxs-lookup"><span data-stu-id="b569c-190">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Sign-in URL** textbox.</span></span>

    <span data-ttu-id="b569c-191">c.</span><span class="sxs-lookup"><span data-stu-id="b569c-191">c.</span></span> <span data-ttu-id="b569c-192">Cliquez sur **Choisir un certificat**, puis recherchez votre **fichier de certificat codé en base 64**.</span><span class="sxs-lookup"><span data-stu-id="b569c-192">Click **Choose certificate**, and then browse to your **Base64 encoded certificate file**.</span></span>

    <span data-ttu-id="b569c-193">d.</span><span class="sxs-lookup"><span data-stu-id="b569c-193">d.</span></span> <span data-ttu-id="b569c-194">Cliquez sur **Enregistrer les modifications** pour terminer la configuration de votre client DropBox for Business.</span><span class="sxs-lookup"><span data-stu-id="b569c-194">Click **Save changes** to complete the configuration on your DropBox for Business tenant.</span></span>

> [!TIP]
> <span data-ttu-id="b569c-195">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="b569c-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b569c-196">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="b569c-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b569c-197">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b569c-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b569c-198">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b569c-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="b569c-199">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b569c-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="b569c-201">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b569c-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b569c-202">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b569c-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="b569c-204">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="b569c-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b569c-206">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="b569c-206">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b569c-208">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b569c-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b569c-210">a.</span><span class="sxs-lookup"><span data-stu-id="b569c-210">a.</span></span> <span data-ttu-id="b569c-211">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b569c-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b569c-212">b.</span><span class="sxs-lookup"><span data-stu-id="b569c-212">b.</span></span> <span data-ttu-id="b569c-213">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b569c-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b569c-214">c.</span><span class="sxs-lookup"><span data-stu-id="b569c-214">c.</span></span> <span data-ttu-id="b569c-215">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="b569c-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b569c-216">d.</span><span class="sxs-lookup"><span data-stu-id="b569c-216">d.</span></span> <span data-ttu-id="b569c-217">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="b569c-217">Click **Create**.</span></span>
 
### <a name="creating-a-dropbox-for-business-test-user"></a><span data-ttu-id="b569c-218">Création d’un utilisateur de test Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="b569c-218">Creating a Dropbox for Business test user</span></span>

<span data-ttu-id="b569c-219">Dans cette section, un utilisateur appelé Britta Simon est créé dans Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="b569c-219">In this section, a user called Britta Simon is created in Dropbox for Business.</span></span> <span data-ttu-id="b569c-220">Dropbox for Business prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="b569c-220">Dropbox for Business supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="b569c-221">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="b569c-221">There is no action item for you in this section.</span></span> <span data-ttu-id="b569c-222">Si un utilisateur n’existe pas dans Dropbox for Business, un nouveau est créé lorsque vous tentez d’accéder à Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="b569c-222">If a user doesn't already exist in Dropbox for Business, a new one is created when you attempt to access Dropbox for Business.</span></span>

>[!Note]
><span data-ttu-id="b569c-223">Si vous devez créer un utilisateur manuellement, contactez l’[équipe de prise en charge des clients Dropbox for Business](https://www.dropbox.com/business/contact).</span><span class="sxs-lookup"><span data-stu-id="b569c-223">If you need to create a user manually, Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact)</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b569c-224">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b569c-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b569c-225">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="b569c-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dropbox for Business.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="b569c-227">**Pour assigner des utilisateurs à Dropbox for Business, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="b569c-227">**To assign Britta Simon to Dropbox for Business, perform the following steps:**</span></span>

1. <span data-ttu-id="b569c-228">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b569c-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="b569c-230">Dans la liste des applications, sélectionnez **Dropbox for Business**.</span><span class="sxs-lookup"><span data-stu-id="b569c-230">In the applications list, select **Dropbox for Business**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. <span data-ttu-id="b569c-232">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b569c-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="b569c-234">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b569c-234">Click **Add** button.</span></span> <span data-ttu-id="b569c-235">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b569c-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="b569c-237">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b569c-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b569c-238">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b569c-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b569c-239">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b569c-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b569c-240">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="b569c-240">Testing single sign-on</span></span>

<span data-ttu-id="b569c-241">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="b569c-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b569c-242">Lorsque vous cliquez sur la vignette Dropbox for Business dans le volet d’accès, vous devez obtenir la page de connexion de votre application Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="b569c-242">When you click the Dropbox for Business tile in the Access Panel, you should get login page of your Dropbox for Business application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b569c-243">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="b569c-243">Additional resources</span></span>

* [<span data-ttu-id="b569c-244">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b569c-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b569c-245">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="b569c-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="b569c-246">Configurer l’approvisionnement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="b569c-246">Configure User Provisioning</span></span>](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

