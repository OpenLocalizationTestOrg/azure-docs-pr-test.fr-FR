---
title: aaaActive Directory Federation Services administration et personnalisation avec Azure AD Connect | Documents Microsoft
description: "Gestion d’AD FS avec Azure AD Connect et personnalisation de la connexion de l’utilisateur à AD FS avec Azure AD Connect et PowerShell."
keywords: "AD FS, ADFS, gestion AD FS, AAD Connect, Connect, connexion, personnalisation d’AD FS, réparer l’approbation, O365, fédération, partie de confiance"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 2593b6c6-dc3f-46ef-8e02-a8e2dc4e9fb9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 361a2bfd6d7a6993dbe773d6ea039ad1afc6346a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a><span data-ttu-id="ed335-104">Gérer et personnaliser Active Directory Federation Services à l’aide d’Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="ed335-104">Manage and customize Active Directory Federation Services by using Azure AD Connect</span></span>
<span data-ttu-id="ed335-105">Cet article décrit comment toomanage et personnaliser des Services de fédération Active Directory (AD FS) à l’aide de Connect de Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ed335-105">This article describes how toomanage and customize Active Directory Federation Services (AD FS) by using Azure Active Directory (Azure AD) Connect.</span></span> <span data-ttu-id="ed335-106">Il inclut également d’autres tâches courantes de AD FS que vous devrez peut-être toodo pour terminer la configuration d’une batterie de serveurs AD FS.</span><span class="sxs-lookup"><span data-stu-id="ed335-106">It also includes other common AD FS tasks that you might need toodo for a complete configuration of an AD FS farm.</span></span>

| <span data-ttu-id="ed335-107">Rubrique</span><span class="sxs-lookup"><span data-stu-id="ed335-107">Topic</span></span> | <span data-ttu-id="ed335-108">Sujet traité</span><span class="sxs-lookup"><span data-stu-id="ed335-108">What it covers</span></span> |
|:--- |:--- |
| <span data-ttu-id="ed335-109">**Gérer AD FS**</span><span class="sxs-lookup"><span data-stu-id="ed335-109">**Manage AD FS**</span></span> | |
| [<span data-ttu-id="ed335-110">Réparation hello approbation</span><span class="sxs-lookup"><span data-stu-id="ed335-110">Repair hello trust</span></span>](#repairthetrust) |<span data-ttu-id="ed335-111">Comment la fédération de hello toorepair faire confiance à Office 365.</span><span class="sxs-lookup"><span data-stu-id="ed335-111">How toorepair hello federation trust with Office 365.</span></span> |
| [<span data-ttu-id="ed335-112">Fédérer avec Azure AD à l’aide d’un ID de connexion de substitution</span><span class="sxs-lookup"><span data-stu-id="ed335-112">Federate with Azure AD using alternate login ID </span></span>](#alternateid) | <span data-ttu-id="ed335-113">Configurer la fédération à l’aide d’un ID de connexion de substitution</span><span class="sxs-lookup"><span data-stu-id="ed335-113">Configure federation using alternate login ID</span></span>  |
| [<span data-ttu-id="ed335-114">Ajout d’un serveur AD FS</span><span class="sxs-lookup"><span data-stu-id="ed335-114">Add an AD FS server</span></span>](#addadfsserver) |<span data-ttu-id="ed335-115">Comment tooexpand un AD FS de batterie de serveurs avec un serveur AD FS supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="ed335-115">How tooexpand an AD FS farm with an additional AD FS server.</span></span> |
| [<span data-ttu-id="ed335-116">Ajouter un serveur de proxy d’application web AD FS</span><span class="sxs-lookup"><span data-stu-id="ed335-116">Add an AD FS Web Application Proxy server</span></span>](#addwapserver) |<span data-ttu-id="ed335-117">Comment tooexpand un AD FS de batterie de serveurs avec un autre serveur Web Application Proxy (WAP).</span><span class="sxs-lookup"><span data-stu-id="ed335-117">How tooexpand an AD FS farm with an additional Web Application Proxy (WAP) server.</span></span> |
| [<span data-ttu-id="ed335-118">Ajout d’un domaine fédéré</span><span class="sxs-lookup"><span data-stu-id="ed335-118">Add a federated domain</span></span>](#addfeddomain) |<span data-ttu-id="ed335-119">Comment tooadd un domaine fédéré.</span><span class="sxs-lookup"><span data-stu-id="ed335-119">How tooadd a federated domain.</span></span> |
| [<span data-ttu-id="ed335-120">Mettre à jour le certificat SSL de hello</span><span class="sxs-lookup"><span data-stu-id="ed335-120">Update hello SSL certificate</span></span>](active-directory-aadconnectfed-ssl-update.md)| <span data-ttu-id="ed335-121">Comment tooupdate hello SSL de certificats pour une batterie de serveurs AD FS.</span><span class="sxs-lookup"><span data-stu-id="ed335-121">How tooupdate hello SSL certificate for an AD FS farm.</span></span> |
| <span data-ttu-id="ed335-122">**Personnaliser AD FS**</span><span class="sxs-lookup"><span data-stu-id="ed335-122">**Customize AD FS**</span></span> | |
| [<span data-ttu-id="ed335-123">Ajout d’une illustration ou d’un logo de société personnalisé</span><span class="sxs-lookup"><span data-stu-id="ed335-123">Add a custom company logo or illustration</span></span>](#customlogo) |<span data-ttu-id="ed335-124">Comment toocustomize un AD FS sign-dans la page avec un logo de société et l’illustration.</span><span class="sxs-lookup"><span data-stu-id="ed335-124">How toocustomize an AD FS sign-in page with a company logo and illustration.</span></span> |
| [<span data-ttu-id="ed335-125">Ajout d’une description de connexion</span><span class="sxs-lookup"><span data-stu-id="ed335-125">Add a sign-in description</span></span>](#addsignindescription) |<span data-ttu-id="ed335-126">Comment tooadd une connexion dans la page description.</span><span class="sxs-lookup"><span data-stu-id="ed335-126">How tooadd a sign-in page description.</span></span> |
| [<span data-ttu-id="ed335-127">Modification des règles de revendication AD FS</span><span class="sxs-lookup"><span data-stu-id="ed335-127">Modify AD FS claim rules</span></span>](#modclaims) |<span data-ttu-id="ed335-128">Comment toomodify AD FS des revendications pour différents scénarios de fédération.</span><span class="sxs-lookup"><span data-stu-id="ed335-128">How toomodify AD FS claims for various federation scenarios.</span></span> |

## <a name="manage-ad-fs"></a><span data-ttu-id="ed335-129">Gérer AD FS</span><span class="sxs-lookup"><span data-stu-id="ed335-129">Manage AD FS</span></span>
<span data-ttu-id="ed335-130">Vous pouvez effectuer diverses tâches AD FS dans Azure AD Connect avec une intervention minime de l’utilisateur à l’aide d’Assistant de hello Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="ed335-130">You can perform various AD FS-related tasks in Azure AD Connect with minimal user intervention by using hello Azure AD Connect wizard.</span></span> <span data-ttu-id="ed335-131">Une fois que vous avez terminé l’installation d’Azure AD Connect à l’exécution de l’Assistant hello, vous pouvez exécuter les Assistant hello tooperform à nouveau des tâches supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="ed335-131">After you've finished installing Azure AD Connect by running hello wizard, you can run hello wizard again tooperform additional tasks.</span></span>

## <span data-ttu-id="ed335-132">Réparation hello approbation<a name=repairthetrust></a></span><span class="sxs-lookup"><span data-stu-id="ed335-132">Repair hello trust <a name=repairthetrust></a></span></span>
<span data-ttu-id="ed335-133">Vous pouvez utiliser Azure AD Connect toocheck hello actuel d’intégrité de hello AD FS et de confiance Azure AD et prendre les mesures appropriées toorepair hello approbation.</span><span class="sxs-lookup"><span data-stu-id="ed335-133">You can use Azure AD Connect toocheck hello current health of hello AD FS and Azure AD trust and take appropriate actions toorepair hello trust.</span></span> <span data-ttu-id="ed335-134">Suivez ces étapes toorepair votre Azure AD et AD FS de confiance.</span><span class="sxs-lookup"><span data-stu-id="ed335-134">Follow these steps toorepair your Azure AD and AD FS trust.</span></span>

1. <span data-ttu-id="ed335-135">Sélectionnez **AAD de réparation et de faire confiance à ADFS** à partir de la liste de hello des tâches supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="ed335-135">Select **Repair AAD and ADFS Trust** from hello list of additional tasks.</span></span>
   <span data-ttu-id="ed335-136">![Réparer la confiance AAD et ADFS](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span><span class="sxs-lookup"><span data-stu-id="ed335-136">![Repair AAD and ADFS Trust](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span></span>

2. <span data-ttu-id="ed335-137">Sur hello **connecter tooAzure AD** page, fournissez vos informations d’identification d’administrateur global pour Azure AD, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="ed335-137">On hello **Connect tooAzure AD** page, provide your global administrator credentials for Azure AD, and click **Next**.</span></span>
   <span data-ttu-id="ed335-138">![Se connecter tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span><span class="sxs-lookup"><span data-stu-id="ed335-138">![Connect tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span></span>

3. <span data-ttu-id="ed335-139">Sur hello **informations d’identification de l’accès à distance** , entrez les informations d’identification hello pour l’administrateur de domaine hello.</span><span class="sxs-lookup"><span data-stu-id="ed335-139">On hello **Remote access credentials** page, enter hello credentials for hello domain administrator.</span></span>

   ![Informations d’identification d’accès à distance](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    <span data-ttu-id="ed335-141">Lorsque vous cliquez sur **Suivant**, Azure AD Connect vérifie l’intégrité du certificat et affiche les éventuels problèmes.</span><span class="sxs-lookup"><span data-stu-id="ed335-141">After you click **Next**, Azure AD Connect checks for certificate health and shows any issues.</span></span>

    ![État des certificats](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    <span data-ttu-id="ed335-143">Hello **tooconfigure prêt** page liste de hello affiche des actions qui seront effectuées approbation de hello toorepair.</span><span class="sxs-lookup"><span data-stu-id="ed335-143">hello **Ready tooconfigure** page shows hello list of actions that will be performed toorepair hello trust.</span></span>

    ![Tooconfigure prêt](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. <span data-ttu-id="ed335-145">Cliquez sur **installer** toorepair une confiance hello.</span><span class="sxs-lookup"><span data-stu-id="ed335-145">Click **Install** toorepair hello trust.</span></span>

> [!NOTE]
> <span data-ttu-id="ed335-146">Azure AD Connect peut seulement réparer ou modifier les certificats auto-signés.</span><span class="sxs-lookup"><span data-stu-id="ed335-146">Azure AD Connect can only repair or act on certificates that are self-signed.</span></span> <span data-ttu-id="ed335-147">Azure AD Connect ne permet pas de réparer les certificats tiers.</span><span class="sxs-lookup"><span data-stu-id="ed335-147">Azure AD Connect can't repair third-party certificates.</span></span>

## <span data-ttu-id="ed335-148">Fédération avec Azure AD en utilisant AlternateID <a name=alternateid></a></span><span class="sxs-lookup"><span data-stu-id="ed335-148">Federate with Azure AD using AlternateID <a name=alternateid></a></span></span>
<span data-ttu-id="ed335-149">Il est recommandé que hello locaux d’utilisateur Principal Name(UPN) et cloud hello nom d’utilisateur Principal sont conservés hello identiques.</span><span class="sxs-lookup"><span data-stu-id="ed335-149">It is recommended that hello on-premises User Principal Name(UPN) and hello cloud User Principal Name are kept hello same.</span></span> <span data-ttu-id="ed335-150">Si hello UPN sur site utilise un domaine non routable (par ex.</span><span class="sxs-lookup"><span data-stu-id="ed335-150">If hello on-premises UPN uses a non-routable domain (ex.</span></span> <span data-ttu-id="ed335-151">Contoso.local) ou ne peut pas être modifiée en raison des dépendances des applications toolocal, nous vous recommandons de configurer des ID de connexion de remplacement.</span><span class="sxs-lookup"><span data-stu-id="ed335-151">Contoso.local) or cannot be changed due toolocal application dependencies, we recommend setting up alternate login ID.</span></span> <span data-ttu-id="ed335-152">ID de connexion de remplacement vous permet de tooconfigure un signe de rencontrer dans lequel les utilisateurs peuvent se connecter avec un attribut autre que leur UPN, comme le courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="ed335-152">Alternate login ID allows you tooconfigure a sign-in experience where users can sign in with an attribute other than their UPN, such as mail.</span></span> <span data-ttu-id="ed335-153">choix de Hello pour le nom d’utilisateur Principal dans l’attribut de Azure AD Connect par défaut toohello userPrincipalName dans Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ed335-153">hello choice for User Principal Name in Azure AD Connect defaults toohello userPrincipalName attribute in Active Directory.</span></span> <span data-ttu-id="ed335-154">Si vous choisissez n’importe quel autre attribut pour le nom d’utilisateur principal et fédérez avec AD FS, Azure AD Connect configurera AD FS pour l’ID de connexion de substitution.</span><span class="sxs-lookup"><span data-stu-id="ed335-154">If you choose any other attribute for User Principal Name and are federating using AD FS, then Azure AD Connect will configure AD FS for alternate login ID.</span></span> <span data-ttu-id="ed335-155">Vous trouverez ci-dessous un exemple de choix d’un autre attribut pour le nom d’utilisateur principal :</span><span class="sxs-lookup"><span data-stu-id="ed335-155">An example of choosing a different attribute for User Principal Name is shown below:</span></span>

![Sélection d’un attribut d’ID de substitution](media/active-directory-aadconnect-federation-management/attributeselection.png)

<span data-ttu-id="ed335-157">La configuration d’un ID de connexion de substitution pour AD FS comprend deux étapes principales :</span><span class="sxs-lookup"><span data-stu-id="ed335-157">Configuring alternate login ID for AD FS consists of two main steps:</span></span>
1. <span data-ttu-id="ed335-158">**Configurer l’ensemble approprié de hello de revendications d’émission**: règles de revendication d’émission hello dans la partie de confiance hello Azure AD d’approbation sont modifiées toouse hello sélectionné UserPrincipalName attribut comme hello d’un autre ID d’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="ed335-158">**Configure hello right set of issuance claims**: hello issuance claim rules in hello Azure AD relying party trust are modified toouse hello selected UserPrincipalName attribute as hello alternate ID of hello user.</span></span>
2. <span data-ttu-id="ed335-159">**Activer l’ID de connexion de remplacement dans la configuration de hello AD FS**: configuration de hello AD FS est mis à jour afin que les services AD FS peut rechercher des utilisateurs dans les forêts approprié hello utilisait autre hello</span><span class="sxs-lookup"><span data-stu-id="ed335-159">**Enable alternate login ID in hello AD FS configuration**: hello AD FS configuration is updated so that AD FS can look up users in hello appropriate forests using hello alternate ID.</span></span> <span data-ttu-id="ed335-160">Cette configuration est prise en charge pour AD FS sur Windows Server 2012 R2 (avec KB2919355) ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="ed335-160">This configuration is supported for AD FS on Windows Server 2012 R2 (with KB2919355) or later.</span></span> <span data-ttu-id="ed335-161">Si les serveurs hello AD FS sont 2012 R2, les vérifications de Azure AD Connect présence hello Hello requis Ko.</span><span class="sxs-lookup"><span data-stu-id="ed335-161">If hello AD FS servers are 2012 R2, Azure AD Connect checks for hello presence of hello required KB.</span></span> <span data-ttu-id="ed335-162">Si hello Ko n’est pas détecté, un avertissement s’affiche après la fin de la configuration, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ed335-162">If hello KB is not detected, a warning will be displayed after configuration completes, as shown below:</span></span>

    ![Avertissement d’absence de base de connaissances sur 2012 R2](media/active-directory-aadconnect-federation-management/kbwarning.png)

    <span data-ttu-id="ed335-164">configuration de hello toorectify en cas de Ko manquant, installez hello requis [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) , puis réparez à l’aide de confiance hello [AAD de réparer et de niveau de confiance AD FS](#repairthetrust).</span><span class="sxs-lookup"><span data-stu-id="ed335-164">toorectify hello configuration in case of missing KB, install hello required [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) and then repair hello trust using [Repair AAD and AD FS Trust](#repairthetrust).</span></span>

> [!NOTE]
> <span data-ttu-id="ed335-165">Pour plus d’informations sur toomanually alternateID et les étapes de configuration, lire [configuration d’un autre ID de connexion](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span><span class="sxs-lookup"><span data-stu-id="ed335-165">For more information on alternateID and steps toomanually configure, read [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span></span>

## <span data-ttu-id="ed335-166">Ajout d’un serveur AD FS <a name=addadfsserver></a></span><span class="sxs-lookup"><span data-stu-id="ed335-166">Add an AD FS server <a name=addadfsserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="ed335-167">serveur de tooadd un AD FS, Azure AD Connect requiert un certificat PFX hello.</span><span class="sxs-lookup"><span data-stu-id="ed335-167">tooadd an AD FS server, Azure AD Connect requires hello PFX certificate.</span></span> <span data-ttu-id="ed335-168">Par conséquent, vous pouvez effectuer cette opération uniquement si vous avez configuré la batterie de serveurs hello AD FS à l’aide d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="ed335-168">Therefore, you can perform this operation only if you configured hello AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="ed335-169">Sélectionnez **Déploiement d’un serveur de fédération supplémentaire**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ed335-169">Select **Deploy an additional Federation Server**, and click **Next**.</span></span>

   ![Serveur de fédération supplémentaire](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. <span data-ttu-id="ed335-171">Sur hello **connecter tooAzure AD** page, entrez vos informations d’identification d’administrateur global pour Azure AD, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="ed335-171">On hello **Connect tooAzure AD** page, enter your global administrator credentials for Azure AD, and click **Next**.</span></span>

   ![Se connecter tooAzure AD](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. <span data-ttu-id="ed335-173">Fournissez les informations d’identification d’administrateur de domaine hello.</span><span class="sxs-lookup"><span data-stu-id="ed335-173">Provide hello domain administrator credentials.</span></span>

   ![Informations d’identification de l’administrateur de domaine](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. <span data-ttu-id="ed335-175">Azure AD Connect demande hello de mot de passe du fichier PFX hello que vous avez fourni lors de la configuration de votre nouvelle batterie AD FS avec Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="ed335-175">Azure AD Connect asks for hello password of hello PFX file that you provided while configuring your new AD FS farm with Azure AD Connect.</span></span> <span data-ttu-id="ed335-176">Cliquez sur **entrer le mot de passe** mot de passe tooprovide hello pour le fichier PFX hello.</span><span class="sxs-lookup"><span data-stu-id="ed335-176">Click **Enter Password** tooprovide hello password for hello PFX file.</span></span>

   ![Mot de passe du certificat](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![Spécifiez le certificat SSL](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. <span data-ttu-id="ed335-179">Sur hello **serveurs AD FS** , entrez le nom du serveur hello ou toobe d’adresse IP ajoutée batterie de serveurs toohello AD FS.</span><span class="sxs-lookup"><span data-stu-id="ed335-179">On hello **AD FS Servers** page, enter hello server name or IP address toobe added toohello AD FS farm.</span></span>

   ![Serveurs AD FS](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. <span data-ttu-id="ed335-181">Cliquez sur **suivant**et parcourez hello final **configurer** page.</span><span class="sxs-lookup"><span data-stu-id="ed335-181">Click **Next**, and go through hello final **Configure** page.</span></span> <span data-ttu-id="ed335-182">Une fois Azure AD Connect a fini d’ajouter de batterie de serveurs hello serveurs toohello AD FS, vous aurez connectivité de hello option tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="ed335-182">After Azure AD Connect has finished adding hello servers toohello AD FS farm, you will be given hello option tooverify hello connectivity.</span></span>

   ![Tooconfigure prêt](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![Installation terminée](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## <span data-ttu-id="ed335-185">Ajout d’un serveur de proxy d’application web AD FS <a name=addwapserver></a></span><span class="sxs-lookup"><span data-stu-id="ed335-185">Add an AD FS WAP server <a name=addwapserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="ed335-186">tooadd un serveur WAP, Azure AD Connect requiert un certificat PFX hello.</span><span class="sxs-lookup"><span data-stu-id="ed335-186">tooadd a WAP server, Azure AD Connect requires hello PFX certificate.</span></span> <span data-ttu-id="ed335-187">Par conséquent, vous ne pouvez effectuer cette opération que si vous avez configuré la batterie de serveurs hello AD FS à l’aide d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="ed335-187">Therefore, you can only perform this operation if you configured hello AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="ed335-188">Sélectionnez **déployer le Proxy d’Application Web** à partir de la liste de hello des tâches disponibles.</span><span class="sxs-lookup"><span data-stu-id="ed335-188">Select **Deploy Web Application Proxy** from hello list of available tasks.</span></span>

   ![Déployer le proxy d’application web](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. <span data-ttu-id="ed335-190">Fournir les informations d’identification d’administrateur général Azure de hello.</span><span class="sxs-lookup"><span data-stu-id="ed335-190">Provide hello Azure global administrator credentials.</span></span>

   ![Se connecter tooAzure AD](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. <span data-ttu-id="ed335-192">Sur hello **certificat SSL de spécifier** , fournissez le mot de passe hello pour le fichier PFX hello que vous avez fourni lors de la configuration de la batterie de serveurs hello AD FS avec Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="ed335-192">On hello **Specify SSL certificate** page, provide hello password for hello PFX file that you provided when you configured hello AD FS farm with Azure AD Connect.</span></span>
   <span data-ttu-id="ed335-193">![Mot de passe du certificat](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span><span class="sxs-lookup"><span data-stu-id="ed335-193">![Certificate password](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span></span>

    ![Spécifiez le certificat SSL](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. <span data-ttu-id="ed335-195">Ajoutez hello server toobe est ajouté comme un serveur WAP.</span><span class="sxs-lookup"><span data-stu-id="ed335-195">Add hello server toobe added as a WAP server.</span></span> <span data-ttu-id="ed335-196">Étant donné que le serveur WAP de hello n’est peut-être pas toohello joint à un domaine, hello dernier demande pour le serveur de toohello les informations d’identification d’administration à ajouter.</span><span class="sxs-lookup"><span data-stu-id="ed335-196">Because hello WAP server might not be joined toohello domain, hello wizard asks for administrative credentials toohello server being added.</span></span>

   ![Informations d’identification du serveur d’administration](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. <span data-ttu-id="ed335-198">Sur hello **informations d’identification de Proxy approbation** , fournissez proxy de hello tooconfigure les informations d’identification d’administration de confiance et accès serveur principal hello dans la batterie de serveurs hello AD FS.</span><span class="sxs-lookup"><span data-stu-id="ed335-198">On hello **Proxy trust credentials** page, provide administrative credentials tooconfigure hello proxy trust and access hello primary server in hello AD FS farm.</span></span>

   ![Informations d’identification de confiance du proxy](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. <span data-ttu-id="ed335-200">Sur hello **tooconfigure prêt** page, Assistant de hello affiche la liste de hello des actions qui seront effectuées.</span><span class="sxs-lookup"><span data-stu-id="ed335-200">On hello **Ready tooconfigure** page, hello wizard shows hello list of actions that will be performed.</span></span>

   ![Tooconfigure prêt](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. <span data-ttu-id="ed335-202">Cliquez sur **installer** configuration de hello toofinish.</span><span class="sxs-lookup"><span data-stu-id="ed335-202">Click **Install** toofinish hello configuration.</span></span> <span data-ttu-id="ed335-203">Une fois la configuration de hello est terminée, Assistant vous propose hello vous hello option tooverify hello serveurs toohello de connectivité.</span><span class="sxs-lookup"><span data-stu-id="ed335-203">After hello configuration is complete, hello wizard gives you hello option tooverify hello connectivity toohello servers.</span></span> <span data-ttu-id="ed335-204">Cliquez sur **Vérifiez** toocheck connectivité.</span><span class="sxs-lookup"><span data-stu-id="ed335-204">Click **Verify** toocheck connectivity.</span></span>

   ![Installation terminée](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## <span data-ttu-id="ed335-206">Ajout d’un domaine fédéré <a name=addfeddomain></a></span><span class="sxs-lookup"><span data-stu-id="ed335-206">Add a federated domain <a name=addfeddomain></a></span></span>

<span data-ttu-id="ed335-207">Il est facile tooadd un toobe domaine fédéré avec Azure AD à l’aide d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="ed335-207">It's easy tooadd a domain toobe federated with Azure AD by using Azure AD Connect.</span></span> <span data-ttu-id="ed335-208">Azure AD Connect ajoute le domaine hello pour la fédération et modifie la revendication hello règles toocorrectly reflètent l’émetteur de hello lorsque vous avez plusieurs domaines fédérés avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed335-208">Azure AD Connect adds hello domain for federation and modifies hello claim rules toocorrectly reflect hello issuer when you have multiple domains federated with Azure AD.</span></span>

1. <span data-ttu-id="ed335-209">tooadd un domaine fédéré, tâche hello sélectionnez **ajouter un domaine Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="ed335-209">tooadd a federated domain, select hello task **Add an additional Azure AD domain**.</span></span>

   ![Domaine Azure AD supplémentaire](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. <span data-ttu-id="ed335-211">Sur la page suivante de hello d’Assistant de hello, fournissent des informations d’identification d’administrateur global de hello pour Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed335-211">On hello next page of hello wizard, provide hello global administrator credentials for Azure AD.</span></span>

   ![Se connecter tooAzure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. <span data-ttu-id="ed335-213">Sur hello **informations d’identification de l’accès à distance** , fournissez les informations d’identification d’administrateur de domaine hello.</span><span class="sxs-lookup"><span data-stu-id="ed335-213">On hello **Remote access credentials** page, provide hello domain administrator credentials.</span></span>

   ![Informations d’identification d’accès à distance](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. <span data-ttu-id="ed335-215">Sur la page suivante de hello, Assistant de hello fournit une liste de domaines Azure AD que vous pouvez fédérer votre annuaire local avec.</span><span class="sxs-lookup"><span data-stu-id="ed335-215">On hello next page, hello wizard provides a list of Azure AD domains that you can federate your on-premises directory with.</span></span> <span data-ttu-id="ed335-216">Choisissez le domaine de hello à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="ed335-216">Choose hello domain from hello list.</span></span>

   ![Domaine Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    <span data-ttu-id="ed335-218">Après avoir choisi le domaine de hello, Assistant de hello fournit des informations appropriées sur les autres actions hello Assistant prend et hello l’impact de la configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="ed335-218">After you choose hello domain, hello wizard provides you with appropriate information about further actions that hello wizard will take and hello impact of hello configuration.</span></span> <span data-ttu-id="ed335-219">Dans certains cas, si vous sélectionnez un domaine qui n’est pas encore vérifié dans Azure AD, Assistant de hello vous fournit des informations toohelp vous vérifiez le domaine de hello.</span><span class="sxs-lookup"><span data-stu-id="ed335-219">In some cases, if you select a domain that isn't yet verified in Azure AD, hello wizard provides you with information toohelp you verify hello domain.</span></span> <span data-ttu-id="ed335-220">Consultez [ajouter votre tooAzure de nom de domaine personnalisé Active Directory](../active-directory-add-domain.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="ed335-220">See [Add your custom domain name tooAzure Active Directory](../active-directory-add-domain.md) for more details.</span></span>

5. <span data-ttu-id="ed335-221">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ed335-221">Click **Next**.</span></span> <span data-ttu-id="ed335-222">Hello **tooconfigure prêt** page affiche la liste de hello des actions qui effectue Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="ed335-222">hello **Ready tooconfigure** page shows hello list of actions that Azure AD Connect will perform.</span></span> <span data-ttu-id="ed335-223">Cliquez sur **installer** configuration de hello toofinish.</span><span class="sxs-lookup"><span data-stu-id="ed335-223">Click **Install** toofinish hello configuration.</span></span>

   ![Tooconfigure prêt](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> <span data-ttu-id="ed335-225">Ajouter des utilisateurs à partir de hello domaine fédéré doit être synchronisée qu’elles soient en mesure de toologin tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="ed335-225">Users from hello added federated domain must be synchronized before they will be able toologin tooAzure AD.</span></span>

## <a name="ad-fs-customization"></a><span data-ttu-id="ed335-226">Personnalisation d’AD FS</span><span class="sxs-lookup"><span data-stu-id="ed335-226">AD FS customization</span></span>
<span data-ttu-id="ed335-227">Hello sections suivantes fournissent plus d’informations sur les tâches courantes de hello que vous pouvez avoir tooperform lorsque vous personnalisez votre page de connexion AD FS.</span><span class="sxs-lookup"><span data-stu-id="ed335-227">hello following sections provide details about some of hello common tasks that you might have tooperform when you customize your AD FS sign-in page.</span></span>

## <span data-ttu-id="ed335-228">Ajout d’une illustration ou d’un logo de société personnalisé <a name=customlogo></a></span><span class="sxs-lookup"><span data-stu-id="ed335-228">Add a custom company logo or illustration <a name=customlogo></a></span></span>
<span data-ttu-id="ed335-229">logo de hello toochange de société hello qui s’affiche sur hello **connexion** page, utilisez hello suivant l’applet de commande Windows PowerShell et la syntaxe.</span><span class="sxs-lookup"><span data-stu-id="ed335-229">toochange hello logo of hello company that's displayed on hello **Sign-in** page, use hello following Windows PowerShell cmdlet and syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="ed335-230">Hello recommandée pour le logo de hello sont 260 x 35 96 PPP avec une taille de fichier non supérieure à 10 Ko.</span><span class="sxs-lookup"><span data-stu-id="ed335-230">hello recommended dimensions for hello logo are 260 x 35 @ 96 dpi with a file size no greater than 10 KB.</span></span>

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> <span data-ttu-id="ed335-231">Hello *TargetName* paramètre est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="ed335-231">hello *TargetName* parameter is required.</span></span> <span data-ttu-id="ed335-232">thème par défaut Hello fourni avec AD FS est nommé par défaut.</span><span class="sxs-lookup"><span data-stu-id="ed335-232">hello default theme that's released with AD FS is named Default.</span></span>

## <span data-ttu-id="ed335-233">Ajout d’une description de connexion <a name=addsignindescription></a></span><span class="sxs-lookup"><span data-stu-id="ed335-233">Add a sign-in description <a name=addsignindescription></a></span></span>
<span data-ttu-id="ed335-234">tooadd un toohello de description de page de connexion **page de connexion**, utilisez hello suivant l’applet de commande Windows PowerShell et la syntaxe.</span><span class="sxs-lookup"><span data-stu-id="ed335-234">tooadd a sign-in page description toohello **Sign-in page**, use hello following Windows PowerShell cmdlet and syntax.</span></span>

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in tooContoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## <span data-ttu-id="ed335-235">Modification des règles de revendication AD FS <a name=modclaims></a></span><span class="sxs-lookup"><span data-stu-id="ed335-235">Modify AD FS claim rules <a name=modclaims></a></span></span>
<span data-ttu-id="ed335-236">AD FS prend en charge un langage de revendication complet que vous pouvez utiliser les règles de revendication toocreate personnalisé.</span><span class="sxs-lookup"><span data-stu-id="ed335-236">AD FS supports a rich claim language that you can use toocreate custom claim rules.</span></span> <span data-ttu-id="ed335-237">Pour plus d’informations, consultez [hello rôle Hello Claim Rule Language](https://technet.microsoft.com/library/dd807118.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed335-237">For more information, see [hello Role of hello Claim Rule Language](https://technet.microsoft.com/library/dd807118.aspx).</span></span>

<span data-ttu-id="ed335-238">Hello sections suivantes décrivent comment vous pouvez écrire des règles personnalisées pour certains scénarios qui se rapportent tooAzure AD et fédération AD FS.</span><span class="sxs-lookup"><span data-stu-id="ed335-238">hello following sections describe how you can write custom rules for some scenarios that relate tooAzure AD and AD FS federation.</span></span>

### <a name="immutable-id-conditional-on-a-value-being-present-in-hello-attribute"></a><span data-ttu-id="ed335-239">ID non modifiable conditionnel sur une valeur qui est présent dans l’attribut de hello</span><span class="sxs-lookup"><span data-stu-id="ed335-239">Immutable ID conditional on a value being present in hello attribute</span></span>
<span data-ttu-id="ed335-240">Azure AD Connect vous permet de spécifier un toobe de l’attribut utilisé comme une ancre source lorsque les objets sont synchronisés tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="ed335-240">Azure AD Connect lets you specify an attribute toobe used as a source anchor when objects are synced tooAzure AD.</span></span> <span data-ttu-id="ed335-241">Si la valeur hello dans l’attribut personnalisé de hello n’est pas vide, vous pourriez tooissue une revendication d’ID immuable.</span><span class="sxs-lookup"><span data-stu-id="ed335-241">If hello value in hello custom attribute is not empty, you might want tooissue an immutable ID claim.</span></span>

<span data-ttu-id="ed335-242">Par exemple, vous pouvez sélectionner **ms-ds-consistencyguid** en tant qu’attribut hello pour ancre source de hello et problème **ImmutableID** en tant que **ms-ds-consistencyguid** cas Bonjour attribut a la valeur par rapport à elle.</span><span class="sxs-lookup"><span data-stu-id="ed335-242">For example, you might select **ms-ds-consistencyguid** as hello attribute for hello source anchor and issue **ImmutableID** as **ms-ds-consistencyguid** in case hello attribute has a value against it.</span></span> <span data-ttu-id="ed335-243">S’il n’existe aucune valeur par rapport à l’attribut de hello, émettre **objectGuid** comme hello immuable ID.</span><span class="sxs-lookup"><span data-stu-id="ed335-243">If there's no value against hello attribute, issue **objectGuid** as hello immutable ID.</span></span> <span data-ttu-id="ed335-244">Vous pouvez construire ensemble hello de règles de revendication personnalisée comme décrit dans hello suivant la section.</span><span class="sxs-lookup"><span data-stu-id="ed335-244">You can construct hello set of custom claim rules as described in hello following section.</span></span>

<span data-ttu-id="ed335-245">**Règle 1 : attributs de la requête**</span><span class="sxs-lookup"><span data-stu-id="ed335-245">**Rule 1: Query attributes**</span></span>

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

<span data-ttu-id="ed335-246">Dans cette règle, vous interrogez les valeurs hello de **ms-ds-consistencyguid** et **objectGuid** pour utilisateur hello à partir d’Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ed335-246">In this rule, you're querying hello values of **ms-ds-consistencyguid** and **objectGuid** for hello user from Active Directory.</span></span> <span data-ttu-id="ed335-247">Renommer hello magasin nom tooan magasin approprié dans votre déploiement AD FS.</span><span class="sxs-lookup"><span data-stu-id="ed335-247">Change hello store name tooan appropriate store name in your AD FS deployment.</span></span> <span data-ttu-id="ed335-248">Modifiez également hello revendications de type tooa revendications appropriées en type de votre fédération, tel que défini pour **objectGuid** et **ms-ds-consistencyguid**.</span><span class="sxs-lookup"><span data-stu-id="ed335-248">Also change hello claims type tooa proper claims type for your federation, as defined for **objectGuid** and **ms-ds-consistencyguid**.</span></span>

<span data-ttu-id="ed335-249">En outre, à l’aide **ajouter** et non **problème**, vous évitez d’ajouter un problème sortant pour l’entité de hello et que vous pouvez utiliser des valeurs de hello en tant que valeurs intermédiaires.</span><span class="sxs-lookup"><span data-stu-id="ed335-249">Also, by using **add** and not **issue**, you avoid adding an outgoing issue for hello entity, and can use hello values as intermediate values.</span></span> <span data-ttu-id="ed335-250">Vous prévoyez d’émettre revendication hello dans une règle ultérieure après avoir établi le toouse valeur comme hello immuable ID.</span><span class="sxs-lookup"><span data-stu-id="ed335-250">You will issue hello claim in a later rule after you establish which value toouse as hello immutable ID.</span></span>

<span data-ttu-id="ed335-251">**Règle 2 : Vérifier l’existence de ms-ds-consistencyguid pour l’utilisateur de hello**</span><span class="sxs-lookup"><span data-stu-id="ed335-251">**Rule 2: Check if ms-ds-consistencyguid exists for hello user**</span></span>

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

<span data-ttu-id="ed335-252">Cette règle définit un indicateur temporaire appelé **idflag** qui est défini trop**useguid** s’il existe aucune **ms-ds-consistencyguid** remplie pour les utilisateurs de hello.</span><span class="sxs-lookup"><span data-stu-id="ed335-252">This rule defines a temporary flag called **idflag** that is set too**useguid** if there's no **ms-ds-consistencyguid** populated for hello user.</span></span> <span data-ttu-id="ed335-253">logique de Hello derrière cela est fait hello que AD FS n’autorise pas les revendications vides.</span><span class="sxs-lookup"><span data-stu-id="ed335-253">hello logic behind this is hello fact that AD FS doesn't allow empty claims.</span></span> <span data-ttu-id="ed335-254">Donc lorsque vous ajoutez des revendications http://contoso.com/ws/2016/02/identity/claims/objectguid et http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid dans la règle 1, vous vous retrouvez avec une **msdsconsistencyguid** revendication uniquement si valeur de Hello est remplie pour les utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="ed335-254">So when you add claims http://contoso.com/ws/2016/02/identity/claims/objectguid and http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid in Rule 1, you end up with an **msdsconsistencyguid** claim only if hello value is populated for hello user.</span></span> <span data-ttu-id="ed335-255">Si elle n’est pas indiquée, AD FS voit que sa valeur sera vide et le supprime immédiatement.</span><span class="sxs-lookup"><span data-stu-id="ed335-255">If it isn't populated, AD FS sees that it will have an empty value and drops it immediately.</span></span> <span data-ttu-id="ed335-256">Tous les objets auront un **objectGuid**. Donc, cette revendication sera toujours là après l’exécution de la règle 1.</span><span class="sxs-lookup"><span data-stu-id="ed335-256">All objects will have **objectGuid**, so that claim will always be there after Rule 1 is executed.</span></span>

<span data-ttu-id="ed335-257">**Règle 3 : émettre ms-ds-consistencyguid comme ID non modifiable s’il est présent**</span><span class="sxs-lookup"><span data-stu-id="ed335-257">**Rule 3: Issue ms-ds-consistencyguid as immutable ID if it's present**</span></span>

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

<span data-ttu-id="ed335-258">Il s’agit d’un contrôle **Exist** implicite.</span><span class="sxs-lookup"><span data-stu-id="ed335-258">This is an implicit **Exist** check.</span></span> <span data-ttu-id="ed335-259">Si la valeur hello pour hello revendication existe, puis émettre que comme hello immuable ID.</span><span class="sxs-lookup"><span data-stu-id="ed335-259">If hello value for hello claim exists, then issue that as hello immutable ID.</span></span> <span data-ttu-id="ed335-260">Hello l’exemple précédent utilise hello **nameidentifier** de revendication.</span><span class="sxs-lookup"><span data-stu-id="ed335-260">hello previous example uses hello **nameidentifier** claim.</span></span> <span data-ttu-id="ed335-261">Vous aurez toochange ce type de revendication appropriées toohello pour l’ID immuable de hello dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="ed335-261">You'll have toochange this toohello appropriate claim type for hello immutable ID in your environment.</span></span>

<span data-ttu-id="ed335-262">**Règle 4 : émettre objectGuid comme ID non modifiable si ms-ds-consistencyGuid n’est pas présent**</span><span class="sxs-lookup"><span data-stu-id="ed335-262">**Rule 4: Issue objectGuid as immutable ID if ms-ds-consistencyGuid is not present**</span></span>

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

<span data-ttu-id="ed335-263">Dans cette règle, vous vérifiez simplement indicateur temporaire de hello **idflag**.</span><span class="sxs-lookup"><span data-stu-id="ed335-263">In this rule, you're simply checking hello temporary flag **idflag**.</span></span> <span data-ttu-id="ed335-264">Vous décidez si tooissue hello revendication basée sur sa valeur.</span><span class="sxs-lookup"><span data-stu-id="ed335-264">You decide whether tooissue hello claim based on its value.</span></span>

> [!NOTE]
> <span data-ttu-id="ed335-265">séquence Hello de ces règles est important.</span><span class="sxs-lookup"><span data-stu-id="ed335-265">hello sequence of these rules is important.</span></span>

### <a name="sso-with-a-subdomain-upn"></a><span data-ttu-id="ed335-266">Authentification unique avec un UPN de sous-domaine</span><span class="sxs-lookup"><span data-stu-id="ed335-266">SSO with a subdomain UPN</span></span>
<span data-ttu-id="ed335-267">Vous pouvez ajouter plusieurs toobe domaine fédéré à l’aide d’Azure AD Connect, comme décrit dans [ajouter un nouveau domaine fédéré](active-directory-aadconnect-federation-management.md#addfeddomain).</span><span class="sxs-lookup"><span data-stu-id="ed335-267">You can add more than one domain toobe federated by using Azure AD Connect, as described in [Add a new federated domain](active-directory-aadconnect-federation-management.md#addfeddomain).</span></span> <span data-ttu-id="ed335-268">Vous devez modifier la revendication de nom principal (UPN) d’utilisateur hello afin que hello ID de l’émetteur correspondant domaine racine de toohello et non de sous-domaine hello, car le domaine racine fédérée de hello couvre également les enfants hello.</span><span class="sxs-lookup"><span data-stu-id="ed335-268">You must modify hello user principal name (UPN) claim so that hello issuer ID corresponds toohello root domain and not hello subdomain, because hello federated root domain also covers hello child.</span></span>

<span data-ttu-id="ed335-269">Par défaut, hello de règles de revendication pour l’émetteur de l’ID est défini en tant que :</span><span class="sxs-lookup"><span data-stu-id="ed335-269">By default, hello claim rule for issuer ID is set as:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![Revendication de l’ID d’émetteur par défaut](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

<span data-ttu-id="ed335-271">règle par défaut de Hello simplement prend suffixe hello et l’utilise dans une revendication d’ID de l’émetteur hello.</span><span class="sxs-lookup"><span data-stu-id="ed335-271">hello default rule simply takes hello UPN suffix and uses it in hello issuer ID claim.</span></span> <span data-ttu-id="ed335-272">Par exemple, John est un utilisateur de sub.contoso.com et contoso.com est fédéré à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed335-272">For example, John is a user in sub.contoso.com, and contoso.com is federated with Azure AD.</span></span> <span data-ttu-id="ed335-273">John insère john@sub.contoso.com comme hello du nom d’utilisateur lors de la signature dans tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="ed335-273">John enters john@sub.contoso.com as hello username while signing in tooAzure AD.</span></span> <span data-ttu-id="ed335-274">règle revendication d’ID de l’émetteur par défaut Hello dans AD FS prend en charge Bonjour suivant de manière :</span><span class="sxs-lookup"><span data-stu-id="ed335-274">hello default issuer ID claim rule in AD FS handles it in hello following manner:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

<span data-ttu-id="ed335-275">**Valeur de revendication :**  http://sub.contoso.com/adfs/services/trust/</span><span class="sxs-lookup"><span data-stu-id="ed335-275">**Claim value:**  http://sub.contoso.com/adfs/services/trust/</span></span>

<span data-ttu-id="ed335-276">toohave uniquement hello domaine racine de l’émetteur de hello valeur de revendication, modifier hello revendication règle toomatch hello suivants :</span><span class="sxs-lookup"><span data-stu-id="ed335-276">toohave only hello root domain in hello issuer claim value, change hello claim rule toomatch hello following:</span></span>

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a><span data-ttu-id="ed335-277">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ed335-277">Next steps</span></span>
<span data-ttu-id="ed335-278">En savoir plus sur les [options de connexion de l’utilisateur](active-directory-aadconnect-user-signin.md).</span><span class="sxs-lookup"><span data-stu-id="ed335-278">Learn more about [user sign-in options](active-directory-aadconnect-user-signin.md).</span></span>
