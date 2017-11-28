---
title: Activer Microsoft Windows Hello Entreprise dans votre organisation | Microsoft Docs
description: "Instructions de déploiement pour activer Microsoft Passport dans votre organisation."
services: active-directory
documentationcenter: 
keywords: "configurer le déploiement Microsoft Passport, Microsoft Windows Hello Entreprise"
author: MarkusVi
manager: femila
tags: azure-classic-portal
ms.assetid: 7dbbe3c6-1cd7-429c-a9b2-115fcbc02416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: 58943e1e29755c983e55c675dd4fe7b75ac47b34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-microsoft-windows-hello-for-business-in-your-organization"></a><span data-ttu-id="998a4-104">Activer Microsoft Windows Hello Entreprise dans votre organisation</span><span class="sxs-lookup"><span data-stu-id="998a4-104">Enable Microsoft Windows Hello for Business in your organization</span></span>
<span data-ttu-id="998a4-105">Après avoir [connecté les appareils du domaine Windows 10 à Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), procédez comme suit pour activer Microsoft Windows Hello Entreprise dans votre organisation :</span><span class="sxs-lookup"><span data-stu-id="998a4-105">After [connecting Windows 10 domain-joined devices with Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), do the following to enable Microsoft Windows Hello for Business in your organization:</span></span>

1. <span data-ttu-id="998a4-106">Déployer System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="998a4-106">Deploy System Center Configuration Manager</span></span>  
2. <span data-ttu-id="998a4-107">Configuration des paramètres de stratégie</span><span class="sxs-lookup"><span data-stu-id="998a4-107">Configure policy settings</span></span>
3. <span data-ttu-id="998a4-108">Configurer le profil de certificat</span><span class="sxs-lookup"><span data-stu-id="998a4-108">Configure the certificate profile</span></span>  

## <a name="deploy-system-center-configuration-manager"></a><span data-ttu-id="998a4-109">Déployer System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="998a4-109">Deploy System Center Configuration Manager</span></span>
<span data-ttu-id="998a4-110">Pour déployer des certificats utilisateur en fonction des clés de Windows Hello Entreprise, vous avez besoin des ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="998a4-110">To deploy user certificates based on Windows Hello for Business keys, you need the following:</span></span>

* <span data-ttu-id="998a4-111">**System Center Configuration Manager Current Branch** - Vous devez installer la version 1606 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="998a4-111">**System Center Configuration Manager Current Branch** - You need to install version 1606 or better.</span></span> <span data-ttu-id="998a4-112">Pour plus d’informations, consultez [Documentation de System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) et [Blog de l’équipe System Center Configuration Manager](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).</span><span class="sxs-lookup"><span data-stu-id="998a4-112">For more information, see the [Documentation for System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) and [System Center Configuration Manager Team Blog](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).</span></span>
* <span data-ttu-id="998a4-113">**Infrastructure à clé publique (PKI)** : pour activer Microsoft Windows Hello Entreprise à l’aide de certificats utilisateur, vous devez disposer d’une infrastructure PKI.</span><span class="sxs-lookup"><span data-stu-id="998a4-113">**Public key infrastructure (PKI)** - To enable Microsoft Windows Hello for Business by using user certificates, you must have a PKI in place.</span></span> <span data-ttu-id="998a4-114">Si vous n’en avez pas ou si vous ne souhaitez pas l’utiliser pour les certificats utilisateur, vous pouvez déployer un nouveau contrôleur de domaine disposant de Windows Server 2016 version 10551 (ou version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="998a4-114">If you don’t have one, or you don’t want to use it for user certificates, you can deploy a new domain controller that has Windows Server 2016 build 10551 (or better) installed.</span></span> <span data-ttu-id="998a4-115">Suivez les étapes pour [installer un contrôleur de domaine réplica dans un domaine existant](https://technet.microsoft.com/library/jj574134.aspx) ou [installer une nouvelle forêt Active Directory, si vous créez un nouvel environnement](https://technet.microsoft.com/library/jj574166).</span><span class="sxs-lookup"><span data-stu-id="998a4-115">Follow the steps to [install a replica domain controller in an existing domain](https://technet.microsoft.com/library/jj574134.aspx) or to [install a new Active Directory forest, if you're creating a new environment](https://technet.microsoft.com/library/jj574166).</span></span> <span data-ttu-id="998a4-116">(Les fichiers ISO sont disponibles en téléchargement sur [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)</span><span class="sxs-lookup"><span data-stu-id="998a4-116">(The ISOs are available for download on [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)</span></span>

## <a name="configure-policy-settings"></a><span data-ttu-id="998a4-117">Configuration des paramètres de stratégie</span><span class="sxs-lookup"><span data-stu-id="998a4-117">Configure policy settings</span></span>
<span data-ttu-id="998a4-118">Pour configurer les paramètres de stratégie de Microsoft Windows Hello Entreprise, vous avez deux options :</span><span class="sxs-lookup"><span data-stu-id="998a4-118">To configure the Microsoft Windows Hello for Business policy settings, you have two options:</span></span>

* <span data-ttu-id="998a4-119">Stratégie de groupe dans Active Directory</span><span class="sxs-lookup"><span data-stu-id="998a4-119">Group Policy in Active Directory</span></span> 
* <span data-ttu-id="998a4-120">System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="998a4-120">The System Center Configuration Manager</span></span> 

<span data-ttu-id="998a4-121">Il est conseillé d’utiliser la stratégie de groupe dans Active Directory pour configurer les paramètres de stratégie de Microsoft Windows Hello Entreprise.</span><span class="sxs-lookup"><span data-stu-id="998a4-121">Using Group Policy in Active Directory is the recommended method to configure Microsoft Windows Hello for Business policy settings.</span></span> 

<span data-ttu-id="998a4-122">Il est conseillé d’utiliser System Center Configuration Manager lorsque vous l’utilisez également pour déployer des certificats.</span><span class="sxs-lookup"><span data-stu-id="998a4-122">Using System Center Configuration Manager is the preferred method when you also use it to deploy certificates.</span></span> <span data-ttu-id="998a4-123">Ce scénario :</span><span class="sxs-lookup"><span data-stu-id="998a4-123">This scenario:</span></span>

* <span data-ttu-id="998a4-124">Garantit la compatibilité avec les scénarios de déploiement plus récents</span><span class="sxs-lookup"><span data-stu-id="998a4-124">Ensures compatibility with the newer deployment scenarios</span></span>
* <span data-ttu-id="998a4-125">Requiert Windows 10 Version 1607 ou version ultérieure du côté client.</span><span class="sxs-lookup"><span data-stu-id="998a4-125">Requires on the client side Windows 10 Version 1607 or better.</span></span>

### <a name="configure-microsoft-windows-hello-for-business-via-group-policy-in-active-directory"></a><span data-ttu-id="998a4-126">Configurer Microsoft Windows Hello Entreprise via la stratégie de groupe dans Active Directory</span><span class="sxs-lookup"><span data-stu-id="998a4-126">Configure Microsoft Windows Hello for Business via group policy in Active Directory</span></span>
<span data-ttu-id="998a4-127">**Étapes** :</span><span class="sxs-lookup"><span data-stu-id="998a4-127">**Steps**:</span></span>

1. <span data-ttu-id="998a4-128">Ouvrez le Gestionnaire de serveur et accédez à **Outils** > **Gestion des stratégies de groupe**.</span><span class="sxs-lookup"><span data-stu-id="998a4-128">Open Server Manager, and navigate to **Tools** > **Group Policy Management**.</span></span>
2. <span data-ttu-id="998a4-129">Dans Gestion des stratégies de groupe, accédez au nœud du domaine qui correspond au domaine dans lequel vous voulez activer Rejoindre Azure AD.</span><span class="sxs-lookup"><span data-stu-id="998a4-129">From Group Policy Management, navigate to the domain node that corresponds to the domain in which you want to enable Azure AD Join.</span></span>
3. <span data-ttu-id="998a4-130">Cliquez avec le bouton droit sur **Objets de stratégie de groupe** et sélectionnez **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="998a4-130">Right-click **Group Policy Objects**, and select **New**.</span></span> <span data-ttu-id="998a4-131">Donnez un nom à votre objet de stratégie de groupe, par exemple Activer Windows Hello Entreprise.</span><span class="sxs-lookup"><span data-stu-id="998a4-131">Give your Group Policy Object a name, for example, Enable Windows Hello for Business.</span></span> <span data-ttu-id="998a4-132">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="998a4-132">Click **OK**.</span></span>
4. <span data-ttu-id="998a4-133">Cliquez avec le bouton droit sur votre nouvel objet de stratégie de groupe, puis sélectionnez **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="998a4-133">Right-click your new Group Policy Object, and then select **Edit**.</span></span>
5. <span data-ttu-id="998a4-134">Accédez à **Configuration ordinateur** > **Stratégies** > **Modèles d’administration** > **Composants Windows** > **Windows Hello Entreprise**.</span><span class="sxs-lookup"><span data-stu-id="998a4-134">Navigate to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Windows Hello for Business**.</span></span>
6. <span data-ttu-id="998a4-135">Avec le bouton droit, cliquez sur **Activer Windows Hello Entreprise**, puis sélectionnez **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="998a4-135">Right-click **Enable Windows Hello for Business**, and then select **Edit**.</span></span>
7. <span data-ttu-id="998a4-136">Sélectionnez l’option **Activé**, puis cliquez sur **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="998a4-136">Select the **Enabled** option button, and then click **Apply**.</span></span> <span data-ttu-id="998a4-137">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="998a4-137">Click **OK**.</span></span>
8. <span data-ttu-id="998a4-138">Vous pouvez maintenant lier l’objet de stratégie de groupe à l’emplacement de votre choix.</span><span class="sxs-lookup"><span data-stu-id="998a4-138">You can now link the Group Policy Object to a location of your choice.</span></span> <span data-ttu-id="998a4-139">Pour activer cette stratégie pour tous les appareils joints à un domaine Windows 10 de votre organisation, liez la stratégie de groupe au domaine.</span><span class="sxs-lookup"><span data-stu-id="998a4-139">To enable this policy for all of the domain-joined Windows 10 devices in your organization, link the Group Policy to the domain.</span></span> <span data-ttu-id="998a4-140">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="998a4-140">For example:</span></span>
   * <span data-ttu-id="998a4-141">Une unité d’organisation spécifique dans Active Directory où les ordinateurs Windows 10 joints au domaine seront situés</span><span class="sxs-lookup"><span data-stu-id="998a4-141">A specific organizational unit (OU) in Active Directory where Windows 10 domain-joined computers will be located</span></span>
   * <span data-ttu-id="998a4-142">Un groupe de sécurité spécifique contenant des ordinateurs Windows 10 joints au domaine qui sera inscrit automatiquement auprès d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="998a4-142">A specific security group that contains Windows 10 domain-joined computers that will be automatically registered with Azure AD</span></span>

### <a name="configure-windows-hello-for-business-using-system-center-configuration-manager"></a><span data-ttu-id="998a4-143">Configurer Windows Hello Entreprise à l’aide de System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="998a4-143">Configure Windows Hello for Business using System Center Configuration Manager</span></span>
<span data-ttu-id="998a4-144">**Étapes** :</span><span class="sxs-lookup"><span data-stu-id="998a4-144">**Steps**:</span></span>

1. <span data-ttu-id="998a4-145">Ouvrez **System Center Configuration Manager**, puis accédez à **Actifs et compatibilité > Paramètres de compatibilité > Accès aux ressources de l’entreprise > Profils Windows Hello Entreprise**.</span><span class="sxs-lookup"><span data-stu-id="998a4-145">Open the **System Center Configuration Manager**, and then navigate to **Assets & Compliance > Compliance Settings > Company Resource Access > Windows Hello for Business Profiles**.</span></span>
   
    ![Configurer Windows Hello Entreprise](./media/active-directory-azureadjoin-passport-deployment/01.png)
2. <span data-ttu-id="998a4-147">Dans la barre d’outils en haut, cliquez sur **Créer un profil Windows Hello Entreprise**.</span><span class="sxs-lookup"><span data-stu-id="998a4-147">In the toolbar on the top, click **Create Windows Hello for business Profile**.</span></span>
   
    ![Configurer Windows Hello Entreprise](./media/active-directory-azureadjoin-passport-deployment/02.png)
3. <span data-ttu-id="998a4-149">Dans la boîte de dialogue **Général** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="998a4-149">On the **General** dialog, perform the following steps:</span></span>
   
    ![Configurer Windows Hello Entreprise](./media/active-directory-azureadjoin-passport-deployment/03.png)
   
    <span data-ttu-id="998a4-151">a.</span><span class="sxs-lookup"><span data-stu-id="998a4-151">a.</span></span> <span data-ttu-id="998a4-152">Dans la zone de texte **Nom**, entrez un nom pour votre profil, par exemple, **Mon profil WHfB**.</span><span class="sxs-lookup"><span data-stu-id="998a4-152">In the **Name** textbox, type a name for your profile, for example, **My WHfB Profile**.</span></span>
   
    <span data-ttu-id="998a4-153">b.</span><span class="sxs-lookup"><span data-stu-id="998a4-153">b.</span></span> <span data-ttu-id="998a4-154">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="998a4-154">Click **Next**.</span></span>
4. <span data-ttu-id="998a4-155">Dans la boîte de dialogue **Plateformes prises en charge**, sélectionnez les plateformes qui seront configurées avec ce profil Windows Hello Entreprise, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="998a4-155">On the **Supported Platforms** dialog, select the platforms that will be provisioned with this Windows Hello for business profile, and then click **Next**.</span></span>
   
    ![Configurer Windows Hello Entreprise](./media/active-directory-azureadjoin-passport-deployment/04.png)
5. <span data-ttu-id="998a4-157">Dans la boîte de dialogue **Paramètres** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="998a4-157">On the **Settings** dialog, perform the following steps:</span></span>
   
    ![Configurer Windows Hello Entreprise](./media/active-directory-azureadjoin-passport-deployment/05.png)
   
    <span data-ttu-id="998a4-159">a.</span><span class="sxs-lookup"><span data-stu-id="998a4-159">a.</span></span> <span data-ttu-id="998a4-160">Pour **Configurer Windows Hello Entreprise**, sélectionnez **Activé**.</span><span class="sxs-lookup"><span data-stu-id="998a4-160">As **Configure Windows Hello for Business**, select **Enabled**.</span></span>
   
    <span data-ttu-id="998a4-161">b.</span><span class="sxs-lookup"><span data-stu-id="998a4-161">b.</span></span> <span data-ttu-id="998a4-162">Pour **Utiliser un module de plateforme sécurisée (TPM)**, sélectionnez **Obligatoire**.</span><span class="sxs-lookup"><span data-stu-id="998a4-162">As **Use a Trusted Platform Module (TPM)**, select **Required**.</span></span> 
   
    <span data-ttu-id="998a4-163">c.</span><span class="sxs-lookup"><span data-stu-id="998a4-163">c.</span></span> <span data-ttu-id="998a4-164">En tant que **Méthode d’authentification**, sélectionnez **Basée sur un certificat**.</span><span class="sxs-lookup"><span data-stu-id="998a4-164">As **Authentication method**, select **Certificate-based**.</span></span>
   
    <span data-ttu-id="998a4-165">d.</span><span class="sxs-lookup"><span data-stu-id="998a4-165">d.</span></span> <span data-ttu-id="998a4-166">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="998a4-166">Click **Next**.</span></span>
6. <span data-ttu-id="998a4-167">Sur la page **Résumé**, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="998a4-167">On the **Summary** dialog, click **Next**.</span></span>
7. <span data-ttu-id="998a4-168">Dans la boîte de dialogue **Exécution terminée**, cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="998a4-168">On the **Completion** dialog, click **Close**.</span></span>
8. <span data-ttu-id="998a4-169">Dans la barre d’outils en haut, cliquez sur **Déployer**.</span><span class="sxs-lookup"><span data-stu-id="998a4-169">In the toolbar on the top, click **Deploy**.</span></span>
   
    ![Configurer Windows Hello Entreprise](./media/active-directory-azureadjoin-passport-deployment/06.png)

## <a name="configure-the-certificate-profile"></a><span data-ttu-id="998a4-171">Configurer le profil de certificat</span><span class="sxs-lookup"><span data-stu-id="998a4-171">Configure the certificate profile</span></span>
<span data-ttu-id="998a4-172">Si vous utilisez l’authentification basée sur un certificat pour l’authentification locale, vous devez configurer et déployer un profil de certificat.</span><span class="sxs-lookup"><span data-stu-id="998a4-172">If you are using certificate-based authentication for on-premises authentication, you need to configure and deploy a certificate profile.</span></span> <span data-ttu-id="998a4-173">Pour ce faire, vous devez configurer un serveur NDES et le rôle de site Point d’enregistrement de certificat dans System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="998a4-173">This task requires you to set up an NDES server and Certificate Registration Point site role in the System Center Configuration Manager.</span></span> <span data-ttu-id="998a4-174">Pour plus d’informations, consultez [Configuration requise pour les profils de certificat dans Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).</span><span class="sxs-lookup"><span data-stu-id="998a4-174">For more details, see the [Prerequisites for Certificate Profiles in Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).</span></span>

1. <span data-ttu-id="998a4-175">Ouvrez **System Center Configuration Manager**, puis accédez à **Actifs et compatibilité > Paramètres de compatibilité > Accès aux ressources de l’entreprise > Profils de certificat**.</span><span class="sxs-lookup"><span data-stu-id="998a4-175">Open the **System Center Configuration Manager**, and then navigate to **Assets & Compliance > Compliance Settings > Company Resource Access > Certificate Profiles**.</span></span>
2. <span data-ttu-id="998a4-176">Sélectionnez un modèle qui dispose d’une ouverture de session avec carte à puce EKU.</span><span class="sxs-lookup"><span data-stu-id="998a4-176">Select a template that has Smart Card sign-in extended key usage (EKU).</span></span>

<span data-ttu-id="998a4-177">Sur la page **Enregistrement SCEP** du profil de certificat, vous devez choisir **Installer dans Passport for Work, sinon mettre en échec** en tant que **Fournisseur de stockage de clés**.</span><span class="sxs-lookup"><span data-stu-id="998a4-177">On the **SCEP Enrollment** page of the certificate profile, you need to choose **Install to Passport for Work otherwise fail** as the **Key Storage Provider**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="998a4-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="998a4-178">Next steps</span></span>
* [<span data-ttu-id="998a4-179">Windows 10 pour l’entreprise : plusieurs manières d’utiliser des appareils professionnels</span><span class="sxs-lookup"><span data-stu-id="998a4-179">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="998a4-180">Extension des fonctionnalités du cloud aux appareils Windows 10 via Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="998a4-180">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="998a4-181">Authentification des identités sans mot de passe avec Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="998a4-181">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="998a4-182">En savoir plus sur les scénarios d’utilisation pour Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="998a4-182">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="998a4-183">Connecter des appareils joints au domaine à Azure AD pour des expériences Windows 10</span><span class="sxs-lookup"><span data-stu-id="998a4-183">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="998a4-184">Configuration d’Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="998a4-184">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

