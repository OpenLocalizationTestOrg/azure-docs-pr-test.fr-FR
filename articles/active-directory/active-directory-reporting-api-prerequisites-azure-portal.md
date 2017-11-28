---
title: "API de création de rapports aaaPrerequisites tooaccess hello Azure AD | Documents Microsoft"
description: "En savoir plus sur les API reporting de hello conditions préalables tooaccess hello Azure AD"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ec28a7530f341dda31268a978754b615c727d66f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a><span data-ttu-id="d69a6-103">API de création de rapports conditions préalables tooaccess hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d69a6-103">Prerequisites tooaccess hello Azure AD reporting API</span></span>

<span data-ttu-id="d69a6-104">Hello [AD Azure reporting API](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) vous fournir des données de toohello de l’accès par programme via un ensemble d’API REST.</span><span class="sxs-lookup"><span data-stu-id="d69a6-104">hello [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="d69a6-105">Vous pouvez appeler ces API à partir de divers outils et langages de programmation.</span><span class="sxs-lookup"><span data-stu-id="d69a6-105">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="d69a6-106">Hello reporting utilise des API [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) API tooauthorize toohello web à l’accès.</span><span class="sxs-lookup"><span data-stu-id="d69a6-106">hello reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize access toohello web APIs.</span></span> 

<span data-ttu-id="d69a6-107">tooget accéder aux données de rapport toohello via les API de hello, vous devez toohave d'entre hello suivant des rôles attribués :</span><span class="sxs-lookup"><span data-stu-id="d69a6-107">tooget access toohello reporting data through hello API, you need toohave one of hello following roles assigned:</span></span>

- <span data-ttu-id="d69a6-108">Lecteur de sécurité</span><span class="sxs-lookup"><span data-stu-id="d69a6-108">Security Reader</span></span>
- <span data-ttu-id="d69a6-109">Administrateur de la sécurité</span><span class="sxs-lookup"><span data-stu-id="d69a6-109">Security Admin</span></span>
- <span data-ttu-id="d69a6-110">Administrateur général</span><span class="sxs-lookup"><span data-stu-id="d69a6-110">Global Admin</span></span>


<span data-ttu-id="d69a6-111">tooprepare toohello de votre accès aux API de création de rapports, vous devez :</span><span class="sxs-lookup"><span data-stu-id="d69a6-111">tooprepare your access toohello reporting API, you must:</span></span>

1. <span data-ttu-id="d69a6-112">Inscrire une application</span><span class="sxs-lookup"><span data-stu-id="d69a6-112">Register an application</span></span> 
2. <span data-ttu-id="d69a6-113">Accorder des autorisations</span><span class="sxs-lookup"><span data-stu-id="d69a6-113">Grant permissions</span></span> 
3. <span data-ttu-id="d69a6-114">Rassembler les paramètres de configuration</span><span class="sxs-lookup"><span data-stu-id="d69a6-114">Gather configuration settings</span></span> 

<span data-ttu-id="d69a6-115">Si vous avez des questions, des problèmes ou des commentaires, [créez un ticket de support](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span><span class="sxs-lookup"><span data-stu-id="d69a6-115">For questions, issues or feedback, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span></span>

## <a name="register-an-azure-active-directory-application"></a><span data-ttu-id="d69a6-116">Inscrire une application Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d69a6-116">Register an Azure Active Directory application</span></span>

<span data-ttu-id="d69a6-117">Vous devez tooregister une application même si vous accédez à hello API à l’aide d’un script de création de rapports.</span><span class="sxs-lookup"><span data-stu-id="d69a6-117">You need tooregister an app even if you are accessing hello reporting API using a script.</span></span> <span data-ttu-id="d69a6-118">Cela vous donne une **ID de l’Application**, qui est requis pour un appel d’autorisation, et il permet à vos jetons tooreceive de code.</span><span class="sxs-lookup"><span data-stu-id="d69a6-118">This gives you an **Application ID**, which is required for an authorization call and it enables your code tooreceive tokens.</span></span>

<span data-ttu-id="d69a6-119">tooconfigure votre API directory tooaccess hello AD Azure reporting, vous devez vous connecter toohello portail Azure avec un compte d’administrateur Azure qui est également un membre de hello **administrateur Global** rôle d’annuaire dans votre locataire Azure AD .</span><span class="sxs-lookup"><span data-stu-id="d69a6-119">tooconfigure your directory tooaccess hello Azure AD reporting API, you must sign in toohello Azure portal with an Azure administrator account that is also a member of hello **Global Administrator** directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d69a6-120">Applications qui s’exécutent sous les informations d’identification avec des privilèges « admin », comme cela peuvent être très puissantes, donc Veuillez être des informations d’identification de l’application que tookeep hello ID/secret sécurisé.</span><span class="sxs-lookup"><span data-stu-id="d69a6-120">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure tookeep hello application's ID/secret credentials secure.</span></span>
> 


<span data-ttu-id="d69a6-121">**tooregister une application Azure Active Directory :**</span><span class="sxs-lookup"><span data-stu-id="d69a6-121">**tooregister an Azure Active Directory application:**</span></span>

1. <span data-ttu-id="d69a6-122">Bonjour [portail Azure](https://portal.azure.com), on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d69a6-122">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="d69a6-124">Sur hello **Azure Active Directory** panneau, cliquez sur **inscriptions d’application**.</span><span class="sxs-lookup"><span data-stu-id="d69a6-124">On hello **Azure Active Directory** blade, click **App registrations**.</span></span>

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. <span data-ttu-id="d69a6-126">Sur hello **inscriptions d’application** lame, dans la barre d’outils hello en haut de hello, cliquez sur **nouvelle inscription de l’application**.</span><span class="sxs-lookup"><span data-stu-id="d69a6-126">On hello **App registrations** blade, in hello toolbar on hello top, click **New application registration**.</span></span>

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. <span data-ttu-id="d69a6-128">Sur hello **créer** panneau, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d69a6-128">On hello **Create** blade, perform hello following steps:</span></span>

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    <span data-ttu-id="d69a6-130">a.</span><span class="sxs-lookup"><span data-stu-id="d69a6-130">a.</span></span> <span data-ttu-id="d69a6-131">Bonjour **nom** zone de texte, type `Reporting API application`.</span><span class="sxs-lookup"><span data-stu-id="d69a6-131">In hello **Name** textbox, type `Reporting API application`.</span></span>

    <span data-ttu-id="d69a6-132">b.</span><span class="sxs-lookup"><span data-stu-id="d69a6-132">b.</span></span> <span data-ttu-id="d69a6-133">Sous **Type d’application**, sélectionnez **Application web/API**.</span><span class="sxs-lookup"><span data-stu-id="d69a6-133">As **Application type**, select **Web app / API**.</span></span>

    <span data-ttu-id="d69a6-134">c.</span><span class="sxs-lookup"><span data-stu-id="d69a6-134">c.</span></span> <span data-ttu-id="d69a6-135">Bonjour **URL de connexion** zone de texte, type `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="d69a6-135">In hello **Sign-on URL** textbox, type `https://localhost`.</span></span>

    <span data-ttu-id="d69a6-136">d.</span><span class="sxs-lookup"><span data-stu-id="d69a6-136">d.</span></span> <span data-ttu-id="d69a6-137">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="d69a6-137">Click **Create**.</span></span> 


## <a name="grant-permissions"></a><span data-ttu-id="d69a6-138">Accorder des autorisations</span><span class="sxs-lookup"><span data-stu-id="d69a6-138">Grant permissions</span></span> 

<span data-ttu-id="d69a6-139">objectif Hello de cette étape correspond à votre application toogrant **lire les données d’annuaire** autorisations toohello **Windows Azure Active Directory** API.</span><span class="sxs-lookup"><span data-stu-id="d69a6-139">hello objective of this step is toogrant your application **Read directory data** permissions toohello **Windows Azure Active Directory** API.</span></span>

![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

<span data-ttu-id="d69a6-141">**toogrant votre hello de toouse autorisation application API :**</span><span class="sxs-lookup"><span data-stu-id="d69a6-141">**toogrant your application permission toouse hello API:**</span></span>

1. <span data-ttu-id="d69a6-142">Sur hello **inscriptions d’application** lame, dans la liste des applications hello, cliquez sur **application API de création de rapports**.</span><span class="sxs-lookup"><span data-stu-id="d69a6-142">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>

2. <span data-ttu-id="d69a6-143">Sur hello **application API de création de rapports** lame, dans la barre d’outils hello en haut de hello, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="d69a6-143">On hello **Reporting API application** blade, in hello toolbar on hello top, click **Settings**.</span></span> 

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. <span data-ttu-id="d69a6-145">Sur hello **paramètres** panneau, cliquez sur **autorisations requises**.</span><span class="sxs-lookup"><span data-stu-id="d69a6-145">On hello **Settings** blade, click **Required permissions**.</span></span> 

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. <span data-ttu-id="d69a6-147">Sur hello **autorisations requises** panneau, Bonjour **API** , cliquez sur **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d69a6-147">On hello **Required permissions** blade, in hello **API** list, click **Windows Azure Active Directory**.</span></span> 

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. <span data-ttu-id="d69a6-149">Sur hello **activer l’accès** panneau, sélectionnez **lire les données d’annuaire**.</span><span class="sxs-lookup"><span data-stu-id="d69a6-149">On hello **Enable Access** blade, select **Read directory data**.</span></span> 

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. <span data-ttu-id="d69a6-151">Dans la barre d’outils de hello en haut de hello, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d69a6-151">In hello toolbar on hello top, click **Save**.</span></span>

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a><span data-ttu-id="d69a6-153">Rassembler les paramètres de configuration</span><span class="sxs-lookup"><span data-stu-id="d69a6-153">Gather configuration settings</span></span> 
<span data-ttu-id="d69a6-154">Cette section vous montre comment hello tooget suivant les paramètres de votre annuaire :</span><span class="sxs-lookup"><span data-stu-id="d69a6-154">This section shows you how tooget hello following settings from your directory:</span></span>

* <span data-ttu-id="d69a6-155">Nom de domaine</span><span class="sxs-lookup"><span data-stu-id="d69a6-155">Domain name</span></span>
* <span data-ttu-id="d69a6-156">ID client</span><span class="sxs-lookup"><span data-stu-id="d69a6-156">Client ID</span></span>
* <span data-ttu-id="d69a6-157">Clé secrète client</span><span class="sxs-lookup"><span data-stu-id="d69a6-157">Client secret</span></span>

<span data-ttu-id="d69a6-158">Vous avez besoin de ces valeurs lors de la configuration d’API de création de rapports appelle toohello.</span><span class="sxs-lookup"><span data-stu-id="d69a6-158">You need these values when configuring calls toohello reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="d69a6-159">Obtenir votre nom de domaine</span><span class="sxs-lookup"><span data-stu-id="d69a6-159">Get your domain name</span></span>

<span data-ttu-id="d69a6-160">**tooget votre nom de domaine :**</span><span class="sxs-lookup"><span data-stu-id="d69a6-160">**tooget your domain name:**</span></span>

1. <span data-ttu-id="d69a6-161">Bonjour [portail Azure](https://portal.azure.com), on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d69a6-161">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="d69a6-163">Sur hello **Azure Active Directory** panneau, cliquez sur **les noms de domaine**.</span><span class="sxs-lookup"><span data-stu-id="d69a6-163">On hello **Azure Active Directory** blade, click **Domain names**.</span></span>

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. <span data-ttu-id="d69a6-165">Copiez votre nom de domaine à partir de la liste hello des domaines.</span><span class="sxs-lookup"><span data-stu-id="d69a6-165">Copy your domain name from hello list of domains.</span></span>


### <a name="get-your-applications-client-id"></a><span data-ttu-id="d69a6-166">Obtenir l’ID client de l’application</span><span class="sxs-lookup"><span data-stu-id="d69a6-166">Get your application's client ID</span></span>

<span data-ttu-id="d69a6-167">**tooget ID de client de votre application :**</span><span class="sxs-lookup"><span data-stu-id="d69a6-167">**tooget your application's client ID:**</span></span>

1. <span data-ttu-id="d69a6-168">Bonjour [portail Azure](https://portal.azure.com), on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d69a6-168">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="d69a6-170">Sur hello **inscriptions d’application** lame, dans la liste des applications hello, cliquez sur **application API de création de rapports**.</span><span class="sxs-lookup"><span data-stu-id="d69a6-170">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>

3. <span data-ttu-id="d69a6-171">Sur hello **application API de création de rapports** panneau, à hello **ID d’Application**, cliquez sur **cliquez sur toocopy**.</span><span class="sxs-lookup"><span data-stu-id="d69a6-171">On hello **Reporting API application** blade, at hello **Application ID**, click **Click toocopy**.</span></span>

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a><span data-ttu-id="d69a6-173">Obtenir la clé secrète client de l’application</span><span class="sxs-lookup"><span data-stu-id="d69a6-173">Get your application's client secret</span></span>
<span data-ttu-id="d69a6-174">tooget cliente de votre application secrète, vous devez toocreate une nouvelle clé et enregistrer, sa valeur lors de l’enregistrement de clé hello, car il n’est pas possible de tooretrieve cette valeur ultérieurement plus.</span><span class="sxs-lookup"><span data-stu-id="d69a6-174">tooget your application's client secret, you need toocreate a new key and save its value upon saving hello new key because it is not possible tooretrieve this value later anymore.</span></span>

<span data-ttu-id="d69a6-175">**tooget question secrète du client de votre application :**</span><span class="sxs-lookup"><span data-stu-id="d69a6-175">**tooget your application's client secret:**</span></span>

1. <span data-ttu-id="d69a6-176">Bonjour [portail Azure](https://portal.azure.com), on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d69a6-176">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="d69a6-178">Sur hello **inscriptions d’application** lame, dans la liste des applications hello, cliquez sur **application API de création de rapports**.</span><span class="sxs-lookup"><span data-stu-id="d69a6-178">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>


3. <span data-ttu-id="d69a6-179">Sur hello **application API de création de rapports** lame, dans la barre d’outils hello en haut de hello, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="d69a6-179">On hello **Reporting API application** blade, in hello toolbar on hello top, click **Settings**.</span></span> 

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. <span data-ttu-id="d69a6-181">Sur hello **paramètres** panneau, Bonjour **APIR accès** , cliquez sur **clés**.</span><span class="sxs-lookup"><span data-stu-id="d69a6-181">On hello **Settings** blade, in hello **APIR Access** section, click **Keys**.</span></span> 

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. <span data-ttu-id="d69a6-183">Sur hello **clés** panneau, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d69a6-183">On hello **Keys** blade, perform hello following steps:</span></span>

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    <span data-ttu-id="d69a6-185">a.</span><span class="sxs-lookup"><span data-stu-id="d69a6-185">a.</span></span> <span data-ttu-id="d69a6-186">Bonjour **Description** zone de texte, type `Reporting API`.</span><span class="sxs-lookup"><span data-stu-id="d69a6-186">In hello **Description** textbox, type `Reporting API`.</span></span>

    <span data-ttu-id="d69a6-187">b.</span><span class="sxs-lookup"><span data-stu-id="d69a6-187">b.</span></span> <span data-ttu-id="d69a6-188">Dans **Expire le**, sélectionnez **Dans 2 ans**.</span><span class="sxs-lookup"><span data-stu-id="d69a6-188">As **Expires**, select **In 2 years**.</span></span>

    <span data-ttu-id="d69a6-189">c.</span><span class="sxs-lookup"><span data-stu-id="d69a6-189">c.</span></span> <span data-ttu-id="d69a6-190">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d69a6-190">Click **Save**.</span></span>

    <span data-ttu-id="d69a6-191">d.</span><span class="sxs-lookup"><span data-stu-id="d69a6-191">d.</span></span> <span data-ttu-id="d69a6-192">Copiez la valeur de clé hello.</span><span class="sxs-lookup"><span data-stu-id="d69a6-192">Copy hello key value.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d69a6-193">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d69a6-193">Next Steps</span></span>
* <span data-ttu-id="d69a6-194">Serait vous comme tooaccess hello des données à partir d’Azure AD de hello reporting API de manière programmée ?</span><span class="sxs-lookup"><span data-stu-id="d69a6-194">Would you like tooaccess hello data from hello Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="d69a6-195">Extraire [prise en main de hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="d69a6-195">Check out [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="d69a6-196">Si vous souhaitez que toofind plus d’informations sur la création de rapports Azure Active Directory, consultez hello [Guide Azure Active Directory Reporting](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="d69a6-196">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

