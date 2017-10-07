---
title: "Azure AD Connect : Activation de l’écriture différée des appareils | Microsoft Docs"
description: "Ce document explique comment activer l’écriture différée des appareils à l’aide d’Azure AD Connect"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c0ff679c-7ed5-4d6e-ac6c-b2b6392e7892
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 3b14013894b7fabdd4658a64f8fdfd29216ba268
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-enabling-device-writeback"></a><span data-ttu-id="332bf-103">Azure AD Connect : Activation de l’écriture différée des appareils</span><span class="sxs-lookup"><span data-stu-id="332bf-103">Azure AD Connect: Enabling device writeback</span></span>
> [!NOTE]
> <span data-ttu-id="332bf-104">L’écriture différée sur appareil nécessite un abonnement Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="332bf-104">A subscription to Azure AD Premium is required for device writeback.</span></span>
> 
> 

<span data-ttu-id="332bf-105">La documentation suivante fournit des informations sur l’activation de la fonctionnalité d’écriture différée des appareils dans Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="332bf-105">The following documentation provides information on how to enable the device writeback feature in Azure AD Connect.</span></span> <span data-ttu-id="332bf-106">L’écriture différée des appareils est utilisée dans les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="332bf-106">Device Writeback is used in the following scenarios:</span></span>

* <span data-ttu-id="332bf-107">Activer l’accès conditionnel basé sur les appareils pour les applications protégées ADFS (2012 R2 ou version ultérieure) (approbations de la partie de confiance).</span><span class="sxs-lookup"><span data-stu-id="332bf-107">Enable conditional access based on devices to ADFS (2012 R2 or higher) protected applications (relying party trusts).</span></span>

<span data-ttu-id="332bf-108">Cela fournit une sécurité supplémentaire et l’assurance que l’accès aux applications est accordé uniquement aux appareils de confiance.</span><span class="sxs-lookup"><span data-stu-id="332bf-108">This provides additional security and assurance that access to applications is granted only to trusted devices.</span></span> <span data-ttu-id="332bf-109">Pour plus d’informations sur l’accès conditionnel, consultez [Gestion des risques avec accès conditionnel](../active-directory-conditional-access.md) et [Configuration d’un accès conditionnel en local à l’aide du service d’inscription d’appareils Azure Active Directory](../active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="332bf-109">For more information on conditional access, see [Managing Risk with Conditional Access](../active-directory-conditional-access.md) and [Setting up On-premises Conditional Access using Azure Active Directory Device Registration](../active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>

> [!IMPORTANT]
> <li><span data-ttu-id="332bf-110">Les appareils doivent se trouver dans la même forêt que les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="332bf-110">Devices must be located in the same forest as the users.</span></span> <span data-ttu-id="332bf-111">Étant donné que les appareils doivent être réécrits dans une seule forêt, cette fonctionnalité ne prend pas en charge un déploiement à plusieurs forêts d’utilisateurs pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="332bf-111">Since devices must be written back to a single forest, this feature does not currently support a deployment with multiple user forests.</span></span></li>
> <li><span data-ttu-id="332bf-112">Vous ne pouvez ajouter qu’un seul objet de configuration d’enregistrement d’appareil à la forêt Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="332bf-112">Only one device registration configuration object can be added to the on-premises Active Directory forest.</span></span> <span data-ttu-id="332bf-113">Cette fonctionnalité n’est pas compatible avec une topologie dans laquelle le domaine Active Directory local est synchronisé à plusieurs annuaires Azure AD.</span><span class="sxs-lookup"><span data-stu-id="332bf-113">This feature is not compatible with a topology where the on-premises Active Directory is synchronized to multiple Azure AD directories.</span></span></li>> 

## <a name="part-1-install-azure-ad-connect"></a><span data-ttu-id="332bf-114">1re partie : Installer Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="332bf-114">Part 1: Install Azure AD Connect</span></span>
1. <span data-ttu-id="332bf-115">Installez Azure AD Connect à l’aide de paramètres personnalisés ou Express.</span><span class="sxs-lookup"><span data-stu-id="332bf-115">Install Azure AD Connect using Custom or Express settings.</span></span> <span data-ttu-id="332bf-116">Microsoft recommande de commencer par synchroniser correctement tous les utilisateurs et groupes avant d’activer l’écriture différée des appareils.</span><span class="sxs-lookup"><span data-stu-id="332bf-116">Microsoft recommends to start with all users and groups successfully synchronized before you enable device writeback.</span></span>

## <a name="part-2-prepare-active-directory"></a><span data-ttu-id="332bf-117">Partie 2 : Préparer Active Directory</span><span class="sxs-lookup"><span data-stu-id="332bf-117">Part 2: Prepare Active Directory</span></span>
<span data-ttu-id="332bf-118">Utilisez les étapes suivantes pour préparer l’utilisation de l’écriture différée des appareils.</span><span class="sxs-lookup"><span data-stu-id="332bf-118">Use the following steps to prepare for using device writeback.</span></span>

1. <span data-ttu-id="332bf-119">À partir de l’ordinateur sur lequel est installé Azure AD Connect, lancez PowerShell en mode élevé.</span><span class="sxs-lookup"><span data-stu-id="332bf-119">From the machine where Azure AD Connect is installed, launch PowerShell in elevated mode.</span></span>
2. <span data-ttu-id="332bf-120">Si le module Active Directory PowerShell n’est PAS installé, installez-le à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="332bf-120">If the Active Directory PowerShell module is NOT installed, install it using the following command:</span></span>
   
   `Add-WindowsFeature RSAT-AD-PowerShell`
3. <span data-ttu-id="332bf-121">Si le module Azure Active Directory PowerShell n’est PAS installé, téléchargez-le et installez-le à partir du [Module Azure Active Directory pour Windows PowerShell (version 64 bits)](http://go.microsoft.com/fwlink/p/?linkid=236297).</span><span class="sxs-lookup"><span data-stu-id="332bf-121">If the Azure Active Directory PowerShell module is NOT installed, then download and install it from [Azure Active Directory Module for Windows PowerShell (64-bit version)](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span> <span data-ttu-id="332bf-122">Ce composant a une dépendance à l’assistant de connexion, qui est installé avec Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="332bf-122">This component has a dependency on the sign-in assistant, which is installed with Azure AD Connect.</span></span>
4. <span data-ttu-id="332bf-123">Avec les informations d’identification d’administrateur d’entreprise, exécutez les commandes suivantes, puis quittez PowerShell.</span><span class="sxs-lookup"><span data-stu-id="332bf-123">With enterprise admin credentials, run the following commands and then exit PowerShell.</span></span>
   
   `Import-Module 'C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1'`
   
   `Initialize-ADSyncDeviceWriteback {Optional:–DomainName [name] Optional:-AdConnectorAccount [account]}`

<span data-ttu-id="332bf-124">Les informations d’identification d’administrateur d’entreprise sont requises, car des modifications à l’espace de noms de configuration sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="332bf-124">Enterprise admin credentials are required since changes to the configuration namespace are needed.</span></span> <span data-ttu-id="332bf-125">Un administrateur de domaine ne dispose pas des autorisations suffisantes.</span><span class="sxs-lookup"><span data-stu-id="332bf-125">A domain admin will not have enough permissions.</span></span>

![Powershell pour l’activation de l’écriture différée des appareils](./media/active-directory-aadconnect-feature-device-writeback/powershell.png)

<span data-ttu-id="332bf-127">Description :</span><span class="sxs-lookup"><span data-stu-id="332bf-127">Description:</span></span>

* <span data-ttu-id="332bf-128">Si elles n’existent pas, des conteneurs et des objets sont créés et configurés sous CN=Device Registration Configuration,CN=Services,CN=Configuration,[forest-dn].</span><span class="sxs-lookup"><span data-stu-id="332bf-128">If they do not exist already, creates and configures new containers and objects under CN=Device Registration Configuration,CN=Services,CN=Configuration,[forest-dn].</span></span>
* <span data-ttu-id="332bf-129">Si elles existent, des conteneurs et des objets sont créés et configurés sous CN=RegisteredDevices,[domain-dn].</span><span class="sxs-lookup"><span data-stu-id="332bf-129">If they do not exist already, creates and configures new containers and objects under CN=RegisteredDevices,[domain-dn].</span></span> <span data-ttu-id="332bf-130">Les objets d’appareil seront créés dans ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="332bf-130">Device objects will be created in this container.</span></span>
* <span data-ttu-id="332bf-131">Définit les autorisations nécessaires sur le compte Azure AD Connector pour gérer des appareils sur votre Active Directory.</span><span class="sxs-lookup"><span data-stu-id="332bf-131">Sets necessary permissions on the Azure AD Connector account, to manage devices on your Active Directory.</span></span>
* <span data-ttu-id="332bf-132">Ne doit s’exécuter que sur une seule forêt, même si Azure AD Connect est installé sur plusieurs forêts.</span><span class="sxs-lookup"><span data-stu-id="332bf-132">Only needs to run on one forest, even if Azure AD Connect is being installed on multiple forests.</span></span>

<span data-ttu-id="332bf-133">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="332bf-133">Parameters:</span></span>

* <span data-ttu-id="332bf-134">DomainName : domaine Active Directory où les objets d’appareil seront créés.</span><span class="sxs-lookup"><span data-stu-id="332bf-134">DomainName: Active Directory Domain where device objects will be created.</span></span> <span data-ttu-id="332bf-135">Remarque : tous les appareils pour une forêt Active Directory donnée seront créés dans un domaine unique.</span><span class="sxs-lookup"><span data-stu-id="332bf-135">Note: All devices for a given Active Directory forest will be created in a single domain.</span></span>
* <span data-ttu-id="332bf-136">AdConnectorAccount : compte Active Directory qui servira à Azure AD Connect pour gérer des objets dans le répertoire.</span><span class="sxs-lookup"><span data-stu-id="332bf-136">AdConnectorAccount: Active Directory account that will be used by Azure AD Connect to manage objects in the directory.</span></span> <span data-ttu-id="332bf-137">C'est le compte utilisé par la synchronisation Azure AD Connect pour se connecter à AD.</span><span class="sxs-lookup"><span data-stu-id="332bf-137">This is the account used by Azure AD Connect sync to connect to AD.</span></span> <span data-ttu-id="332bf-138">Si vous avez procédé à l'installation à l'aide de paramètres Express, c'est le compte précédé de MSOL_.</span><span class="sxs-lookup"><span data-stu-id="332bf-138">If you installed using express settings, it is the account prefixed with MSOL_.</span></span>

## <a name="part-3-enable-device-writeback-in-azure-ad-connect"></a><span data-ttu-id="332bf-139">3ème partie : Activer l’écriture différée des appareils dans Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="332bf-139">Part 3: Enable device writeback in Azure AD Connect</span></span>
<span data-ttu-id="332bf-140">Utilisez la procédure suivante pour activer l’écriture différée des appareils dans Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="332bf-140">Use the following procedure to enable device writeback in Azure AD Connect.</span></span>

1. <span data-ttu-id="332bf-141">Réexécutez l’Assistant d’installation.</span><span class="sxs-lookup"><span data-stu-id="332bf-141">Run the installation wizard again.</span></span> <span data-ttu-id="332bf-142">Sélectionnez **Personnalisation des options de synchronisation** à partir de la page Tâches supplémentaires et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="332bf-142">Select **customize synchronization options** from the Additional Tasks page and click **Next**.</span></span>
   <span data-ttu-id="332bf-143">![Installation personnalisée - Personnaliser les options de synchronisation](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback2.png)</span><span class="sxs-lookup"><span data-stu-id="332bf-143">![Custom Install customize synchronization options](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback2.png)</span></span>
2. <span data-ttu-id="332bf-144">Sur la page Fonctionnalités facultatives, l’écriture différée des appareils ne sera plus grisée.</span><span class="sxs-lookup"><span data-stu-id="332bf-144">In the Optional Features page, device writeback will no longer be grayed out.</span></span> <span data-ttu-id="332bf-145">Notez que si les étapes de préparation d’Azure AD Connect ne sont pas terminées, l’écriture différée des appareils sera grisée sur la page Fonctionnalités facultatives.</span><span class="sxs-lookup"><span data-stu-id="332bf-145">Please note that if the Azure AD Connect prep steps are not completed device writeback will be grayed out in the Optional features page.</span></span> <span data-ttu-id="332bf-146">Cochez la case correspondant à l’écriture différée des appareils, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="332bf-146">Check the box for device writeback and click **next**.</span></span> <span data-ttu-id="332bf-147">Si la case à cocher est toujours décochée, consultez la [section de résolution des problèmes](#the-writeback-checkbox-is-still-disabled).</span><span class="sxs-lookup"><span data-stu-id="332bf-147">If the checkbox is still disabled, see the [troubleshooting section](#the-writeback-checkbox-is-still-disabled).</span></span>
   <span data-ttu-id="332bf-148">![Installation personnalisée - Fonctionnalités facultatives de l’écriture différée des appareils](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback3.png)</span><span class="sxs-lookup"><span data-stu-id="332bf-148">![Custom install Device Writeback optional features](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback3.png)</span></span>
3. <span data-ttu-id="332bf-149">Dans la page de l’écriture différée, vous verrez le domaine fourni en tant que forêt d’écriture différée d’appareil par défaut.</span><span class="sxs-lookup"><span data-stu-id="332bf-149">On the writeback page, you will see the supplied domain as the default Device writeback forest.</span></span>
   <span data-ttu-id="332bf-150">![Installation personnalisée - Forêt cible de l’écriture différée des appareils](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback4.png)</span><span class="sxs-lookup"><span data-stu-id="332bf-150">![Custom Install device writeback target forest](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback4.png)</span></span>
4. <span data-ttu-id="332bf-151">Terminez l’installation de l’Assistant sans autre modification de la configuration.</span><span class="sxs-lookup"><span data-stu-id="332bf-151">Complete the installation of the Wizard with no additional configuration changes.</span></span> <span data-ttu-id="332bf-152">Si nécessaire, consultez [Installation personnalisée d’Azure AD Connect](active-directory-aadconnect-get-started-custom.md)</span><span class="sxs-lookup"><span data-stu-id="332bf-152">If needed, refer to [Custom installation of Azure AD Connect.](active-directory-aadconnect-get-started-custom.md)</span></span>

## <a name="enable-conditional-access"></a><span data-ttu-id="332bf-153">Activer l’accès conditionnel</span><span class="sxs-lookup"><span data-stu-id="332bf-153">Enable conditional access</span></span>
<span data-ttu-id="332bf-154">Des instructions détaillées pour activer ce scénario sont disponibles dans [Configuration d’un accès conditionnel en local à l’aide du service d’inscription d’appareils Azure Active Directory](../active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="332bf-154">Detailed instructions to enable this scenario are available within [Setting up On-premises Conditional Access using Azure Active Directory Device Registration](../active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>

## <a name="verify-devices-are-synchronized-to-active-directory"></a><span data-ttu-id="332bf-155">Vérifier la synchronisation des appareils avec Active Directory</span><span class="sxs-lookup"><span data-stu-id="332bf-155">Verify Devices are synchronized to Active Directory</span></span>
<span data-ttu-id="332bf-156">L’écriture différée des appareils doit désormais fonctionner correctement.</span><span class="sxs-lookup"><span data-stu-id="332bf-156">Device writeback should now be working properly.</span></span> <span data-ttu-id="332bf-157">Sachez que la réécriture des objets d’appareil dans AD peut prendre jusqu’à 3 heures.</span><span class="sxs-lookup"><span data-stu-id="332bf-157">Be aware that it can take up to 3 hours for device objects to be written-back to AD.</span></span>  <span data-ttu-id="332bf-158">Pour vérifier que vos appareils sont correctement synchronisés, procédez comme suit après la fin des règles de synchronisation :</span><span class="sxs-lookup"><span data-stu-id="332bf-158">To verify that your devices are being synced properly, do the following after the sync rules complete:</span></span>

1. <span data-ttu-id="332bf-159">Lancez le Centre d’administration Active Directory.</span><span class="sxs-lookup"><span data-stu-id="332bf-159">Launch Active Directory Administrative Center.</span></span>
2. <span data-ttu-id="332bf-160">Développez RegisteredDevices au sein du domaine en cours de fédération.</span><span class="sxs-lookup"><span data-stu-id="332bf-160">Expand RegisteredDevices, within the Domain that is being federated.</span></span>
   <span data-ttu-id="332bf-161">![Active Directory - Appareils inscrits au Centre d’administration](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback5.png)</span><span class="sxs-lookup"><span data-stu-id="332bf-161">![Active Directory Admin Center Registered Devices](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback5.png)</span></span>
3. <span data-ttu-id="332bf-162">Les appareils enregistrés actuels sont répertoriés à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="332bf-162">Current registered devices will be listed there.</span></span>
   <span data-ttu-id="332bf-163">![Active Directory - Liste des appareils inscrits au Centre d’administration](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback6.png)</span><span class="sxs-lookup"><span data-stu-id="332bf-163">![Active Directory Admin Center Registered Devices List](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback6.png)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="332bf-164">Résolution de problèmes</span><span class="sxs-lookup"><span data-stu-id="332bf-164">Troubleshooting</span></span>
### <a name="the-writeback-checkbox-is-still-disabled"></a><span data-ttu-id="332bf-165">La case à cocher de l'écriture différée est toujours désactivée.</span><span class="sxs-lookup"><span data-stu-id="332bf-165">The writeback checkbox is still disabled</span></span>
<span data-ttu-id="332bf-166">Si la case à cocher pour l'écriture différée des appareils n'est pas activée alors que vous avez suivi les étapes ci-dessus, la procédure suivante vous guidera dans ce que l'Assistant d'installation vérifie avant l'activation de la case.</span><span class="sxs-lookup"><span data-stu-id="332bf-166">If the checkbox for device writeback is not enabled even though you have followed the steps above, the following steps will guide you through what the installation wizard is verifying before the box is enabled.</span></span>

<span data-ttu-id="332bf-167">Commençons par le début :</span><span class="sxs-lookup"><span data-stu-id="332bf-167">First things first:</span></span>

* <span data-ttu-id="332bf-168">Assurez-vous qu'au moins une forêt a Windows Server 2012R2.</span><span class="sxs-lookup"><span data-stu-id="332bf-168">Make sure at least one forest has Windows Server 2012R2.</span></span> <span data-ttu-id="332bf-169">Le type d'objet d'appareil doit être présent.</span><span class="sxs-lookup"><span data-stu-id="332bf-169">The device object type must be present.</span></span>
* <span data-ttu-id="332bf-170">Si l'Assistant d'installation est déjà en cours d'exécution, les modifications ne seront pas détectées.</span><span class="sxs-lookup"><span data-stu-id="332bf-170">If the installation wizard is already running, then any changes will not be detected.</span></span> <span data-ttu-id="332bf-171">Dans ce cas, terminez l'Assistant installation et exécutez-le à nouveau.</span><span class="sxs-lookup"><span data-stu-id="332bf-171">In this case, complete the installation wizard and run it again.</span></span>
* <span data-ttu-id="332bf-172">Assurez-vous que le compte que vous fournissez dans le script d'initialisation est bien l'utilisateur utilisé par le connecteur Active Directory.</span><span class="sxs-lookup"><span data-stu-id="332bf-172">Make sure the account you provide in the initialization script is actually the correct user used by the Active Directory Connector.</span></span> <span data-ttu-id="332bf-173">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="332bf-173">To verify this, follow these steps:</span></span>
  * <span data-ttu-id="332bf-174">Dans le menu Démarrer, ouvrez **Service de synchronisation**.</span><span class="sxs-lookup"><span data-stu-id="332bf-174">From the start menu, open **Synchronization Service**.</span></span>
  * <span data-ttu-id="332bf-175">Ouvrez l’onglet **Connecteurs** .</span><span class="sxs-lookup"><span data-stu-id="332bf-175">Open the **Connectors** tab.</span></span>
  * <span data-ttu-id="332bf-176">Trouvez le connecteur de type services de domaine Active Directory et sélectionnez-le.</span><span class="sxs-lookup"><span data-stu-id="332bf-176">Find the Connector with type Active Directory Domain Services and select it.</span></span>
  * <span data-ttu-id="332bf-177">Sous **Actions**, sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="332bf-177">Under **Actions**, select **Properties**.</span></span>
  * <span data-ttu-id="332bf-178">Accédez à **Se connecter à la forêt Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="332bf-178">Go to **Connect to Active Directory Forest**.</span></span> <span data-ttu-id="332bf-179">Vérifiez que le nom de domaine et le nom d’utilisateur spécifiés sur cet écran correspondent au compte fourni pour le script.</span><span class="sxs-lookup"><span data-stu-id="332bf-179">Verify that the domain and user name specified on this screen match the account provided to the script.</span></span>
    <span data-ttu-id="332bf-180">![Compte de connecteur dans Sync Service Manager](./media/active-directory-aadconnect-feature-device-writeback/connectoraccount.png)</span><span class="sxs-lookup"><span data-stu-id="332bf-180">![Connector account in Sync Service Manager](./media/active-directory-aadconnect-feature-device-writeback/connectoraccount.png)</span></span>

<span data-ttu-id="332bf-181">Vérifiez la configuration dans Active Directory :</span><span class="sxs-lookup"><span data-stu-id="332bf-181">Verify configuration in Active Directory:</span></span>

* <span data-ttu-id="332bf-182">Vérifiez que le Service d’inscription de l’appareil se trouve à l’emplacement ci-dessous (CN = DeviceRegistrationService, CN = Services d’inscription de périphérique, CN = Inscription de l’appareil, CN = Services, CN = Configuration) dans le contexte d’appellation de configuration.</span><span class="sxs-lookup"><span data-stu-id="332bf-182">Verify that the Device Registration Service is located in the location below (CN=DeviceRegistrationService,CN=Device Registration Services,CN=Device Registration Configuration,CN=Services,CN=Configuration) under configuration naming context.</span></span>

![Résoudre les problèmes, DeviceRegistrationService dans l’espace de noms de configuration](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot1.png)

* <span data-ttu-id="332bf-184">Vérifiez qu'il n'y a qu'un seul objet de configuration en recherchant l'espace de noms de configuration.</span><span class="sxs-lookup"><span data-stu-id="332bf-184">Verify there is only one configuration object by searching the configuration namespace.</span></span> <span data-ttu-id="332bf-185">S'il en existe plusieurs, supprimez le doublon.</span><span class="sxs-lookup"><span data-stu-id="332bf-185">If there is more than one, delete the duplicate.</span></span>

![Résoudre les problèmes, rechercher les objets en double](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot2.png)

* <span data-ttu-id="332bf-187">Sur l'objet Service d'inscription de l'appareil, assurez-vous que l'attribut msDS-DeviceLocation est présent et a une valeur.</span><span class="sxs-lookup"><span data-stu-id="332bf-187">On the Device Registration Service object, make sure the attribute msDS-DeviceLocation is present and has a value.</span></span> <span data-ttu-id="332bf-188">Recherchez cet emplacement et assurez-vous qu'il est présent avec l'attribut objectType msDS-DeviceContainer.</span><span class="sxs-lookup"><span data-stu-id="332bf-188">Lookup this location and make sure it is present with the objectType msDS-DeviceContainer.</span></span>

![Résoudre les problèmes, msDS-DeviceLocation](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot3.png)

![Résoudre les problèmes, classe d’objet RegisteredDevices](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot4.png)

* <span data-ttu-id="332bf-191">Vérifiez que le compte utilisé par le connecteur Active Directory dispose des autorisations requise sur le conteneur d’appareils inscrits trouvé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="332bf-191">Verify the account used by the Active Directory Connector has required permissions on the Registered Devices container found by the previous step.</span></span> <span data-ttu-id="332bf-192">Voici les autorisations attendues sur ce conteneur :</span><span class="sxs-lookup"><span data-stu-id="332bf-192">This is the expected permissions on this container:</span></span>

![Résoudre les problèmes, vérifier les autorisations du conteneur](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot5.png)

* <span data-ttu-id="332bf-194">Vérifiez que le compte Active Directory dispose des autorisations sur CN = Inscription de l’appareil, CN = Services, CN = Objet de Configuration.</span><span class="sxs-lookup"><span data-stu-id="332bf-194">Verify the Active Directory account has permissions on the CN=Device Registration Configuration,CN=Services,CN=Configuration object.</span></span>

![Résoudre les problèmes, vérifier les autorisations de la configuration de l’inscription des appareils](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot6.png)

## <a name="additional-information"></a><span data-ttu-id="332bf-196">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="332bf-196">Additional Information</span></span>
* [<span data-ttu-id="332bf-197">Gestion des risques avec accès conditionnel</span><span class="sxs-lookup"><span data-stu-id="332bf-197">Managing Risk With Conditional Access</span></span>](../active-directory-conditional-access.md)
* [<span data-ttu-id="332bf-198">Configuration d’un accès conditionnel en local à l’aide du service d’inscription d’appareils Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="332bf-198">Setting up On-premises Conditional Access using Azure Active Directory Device Registration</span></span>](../active-directory-device-registration-on-premises-setup.md)

## <a name="next-steps"></a><span data-ttu-id="332bf-199">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="332bf-199">Next steps</span></span>
<span data-ttu-id="332bf-200">En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="332bf-200">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
